---
title: ASP.NET Core로 인증 및 Id 마이그레이션
author: ardalis
description: ASP.NET Core MVC 프로젝트를 ASP.NET MVC 프로젝트에서 인증 및 id를 마이그레이션하는 방법에 알아봅니다.
ms.author: riande
ms.date: 10/14/2016
uid: migration/identity
ms.openlocfilehash: e05d72ca78c7b8191a47f78cda31ee40e04d0706
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36275699"
---
# <a name="migrate-authentication-and-identity-to-aspnet-core"></a>ASP.NET Core로 인증 및 Id 마이그레이션

작성자: [Steve Smith](https://ardalis.com/)

이전 문서에서에서는 [ASP.NET MVC 프로젝트에서 ASP.NET Core MVC 구성을 마이그레이션할](xref:migration/configuration)합니다. 이 문서에서는 등록, 로그인 및 사용자 관리 기능을 마이그레이션할 했습니다.

## <a name="configure-identity-and-membership"></a>Id 및 멤버 자격을 구성 합니다.

ASP.NET MVC에서 인증 및 id 기능에는 ASP.NET Identity를 사용 하 여 구성 됩니다 *Startup.Auth.cs* 및 *IdentityConfig.cs*에 있는 *App_Start* 폴더입니다. ASP.NET Core MVC에서 이러한 기능에 구성 된 *Startup.cs*합니다.

설치는 `Microsoft.AspNetCore.Identity.EntityFrameworkCore` 및 `Microsoft.AspNetCore.Authentication.Cookies` NuGet 패키지 합니다.

그런 다음을 열고 *Startup.cs* 하 고 업데이트는 `Startup.ConfigureServices` Entity Framework 및 Id 서비스를 사용 하는 메서드:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Add EF services to the services container.
    services.AddDbContext<ApplicationDbContext>(options =>
        options.UseSqlServer(Configuration.GetConnectionString("DefaultConnection")));

    services.AddIdentity<ApplicationUser, IdentityRole>()
        .AddEntityFrameworkStores<ApplicationDbContext>()
        .AddDefaultTokenProviders();

     services.AddMvc();
}
```

이 시점에서 ASP.NET MVC 프로젝트에서 사용한 아직 하지 않은 위의 코드에서 참조 하는 형식은 두 가지가: `ApplicationDbContext` 및 `ApplicationUser`합니다. 새 *모델* 폴더에서 ASP.NET Core 프로젝트를 하 고 이러한 형식에 해당를 두 개의 클래스를 추가 합니다. ASP.NET MVC에서 이러한 클래스의 버전을 찾이 됩니다 */Models/IdentityModels.cs*, 있지만 명확 하 게 되므로 마이그레이션된 프로젝트에서 클래스 마다 파일 하나를 사용 하는 것입니다.

*ApplicationUser.cs*:

```csharp
using Microsoft.AspNetCore.Identity.EntityFrameworkCore;

namespace NewMvcProject.Models
{
  public class ApplicationUser : IdentityUser
  {
  }
}
```

*ApplicationDbContext.cs*:

```csharp
using Microsoft.AspNetCore.Identity.EntityFramework;
using Microsoft.Data.Entity;

namespace NewMvcProject.Models
{
    public class ApplicationDbContext : IdentityDbContext<ApplicationUser>
    {
        public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
            : base(options)
        {
        }

        protected override void OnModelCreating(ModelBuilder builder)
        {
            base.OnModelCreating(builder);
            // Customize the ASP.NET Identity model and override the defaults if needed.
            // For example, you can rename the ASP.NET Identity table names and more.
            // Add your customizations after calling base.OnModelCreating(builder);
        }
    }
}
```

ASP.NET Core MVC 시작 웹 프로젝트에 사용자가의 많은 사용자 지정이 포함 되어 있지 않습니다 또는 `ApplicationDbContext`합니다. 실제 앱으로 마이그레이션할 경우도 마이그레이션해야 할 모든 사용자 지정 속성 및 응용 프로그램의 사용자의 메서드 및 `DbContext` 클래스 뿐만 아니라 앱은 사용 하 여 다른 모델 클래스입니다. 예를 들어 경우 프로그램 `DbContext` 에 `DbSet<Album>`를 마이그레이션해야 하는 `Album` 클래스입니다.

현재 위치에서 이러한 파일에는 *Startup.cs* 업데이트 하 여 컴파일할 파일을 만들 수 있습니다는 `using` 문:

```csharp
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Identity;
using Microsoft.AspNetCore.Hosting;
using Microsoft.EntityFrameworkCore;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;
```

이제이 앱을 인증 및 Id 서비스를 지원 하도록 준비 합니다. 사용자에 게 이러한 기능을 갖추고 하기만 합니다.

## <a name="migrate-registration-and-login-logic"></a>등록 및 로그인 논리 마이그레이션

응용 프로그램에 대해 구성 하는 Id 서비스 및 Entity Framework 및 SQL Server를 사용 하 여 구성 하는 데이터 액세스를 사용 하 여 준비가 응용 프로그램에 등록 및 로그인에 대 한 지원을 추가 합니다. 이전에 설명한 대로 [마이그레이션 프로세스의 앞부분에 나오는](xref:migration/mvc#migrate-the-layout-file) 에 대 한 참조를 주석 우리 *_LoginPartial* 에 *_Layout.cshtml*합니다. 이제 해당 코드를 반환 합니다. 주석 처리를 제거, 로그인 기능을 지 원하는 데 필요한 컨트롤러를 추가 하는 시간입니다.

주석 처리 제거는 `@Html.Partial` 줄 *_Layout.cshtml*:

```cshtml
      <li>@Html.ActionLink("Contact", "Contact", "Home")</li>
    </ul>
    @*@Html.Partial("_LoginPartial")*@
  </div>
</div>
```

이제 라는 새로운 Razor 뷰 추가 *_LoginPartial* 에 *뷰/공유* 폴더:

업데이트 *_LoginPartial.cshtml* 를 다음 코드로 (모든 내용을 바꾸기):

```cshtml
@inject SignInManager<ApplicationUser> SignInManager
@inject UserManager<ApplicationUser> UserManager

@if (SignInManager.IsSignedIn(User))
{
    <form asp-area="" asp-controller="Account" asp-action="Logout" method="post" id="logoutForm" class="navbar-right">
        <ul class="nav navbar-nav navbar-right">
            <li>
                <a asp-area="" asp-controller="Manage" asp-action="Index" title="Manage">Hello @UserManager.GetUserName(User)!</a>
            </li>
            <li>
                <button type="submit" class="btn btn-link navbar-btn navbar-link">Log out</button>
            </li>
        </ul>
    </form>
}
else
{
    <ul class="nav navbar-nav navbar-right">
        <li><a asp-area="" asp-controller="Account" asp-action="Register">Register</a></li>
        <li><a asp-area="" asp-controller="Account" asp-action="Login">Log in</a></li>
    </ul>
}
```

이 시점에서 브라우저에서 사이트를 새로 고칠 수 있습니다.

## <a name="summary"></a>요약

ASP.NET Core에서는 ASP.NET Id 기능을 변경 합니다. 이 문서에서 ASP.NET Core를 ASP.NET Identity의 인증 및 사용자 관리 기능을 마이그레이션하는 방법에 알아보았습니다.
