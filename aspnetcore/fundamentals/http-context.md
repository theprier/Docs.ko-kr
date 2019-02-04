---
title: ASP.NET Core에서 HttpContext에 액세스
author: coderandhiker
description: ASP.NET Core에서 HttpContext에 액세스하는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 07/27/2018
uid: fundamentals/httpcontext
ms.openlocfilehash: babc637cdec8590ac14f7924c17e862e5b2f6a81
ms.sourcegitcommit: d22b3c23c45a076c4f394a70b1c8df2fbcdf656d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2019
ms.locfileid: "55428488"
---
# <a name="access-httpcontext-in-aspnet-core"></a>ASP.NET Core에서 HttpContext에 액세스

ASP.NET Core 앱은 [IHttpContextAccessor](/dotnet/api/microsoft.aspnetcore.http.ihttpcontextaccessor) 인터페이스 및 기본 구현 [HttpContextAccessor](/dotnet/api/microsoft.aspnetcore.http.httpcontextaccessor)를 통해 `HttpContext`에 액세스합니다. 서비스 내에서 `HttpContext`에 액세스가 필요한 경우에만 `IHttpContextAccessor`를 사용할 필요가 있습니다.

::: moniker range=">= aspnetcore-2.0"

## <a name="use-httpcontext-from-razor-pages"></a>Razor Pages에서 HttpContext 사용

Razor Pages [PageModel](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel)은 다음과 같이 [HttpContext](/dotnet/api/microsoft.aspnetcore.mvc.razorpages.pagemodel.httpcontext) 속성을 공개합니다.

```csharp
public class AboutModel : PageModel
{
    public string Message { get; set; }

    public void OnGet()
    {
        Message = HttpContext.Request.PathBase;
    }
}
```

::: moniker-end

## <a name="use-httpcontext-from-a-razor-view"></a>Razor 보기에서 HttpContext 사용

Razor 보기는 보기에서 [RazorPage.Context](/dotnet/api/microsoft.aspnetcore.mvc.razor.razorpage.context#Microsoft_AspNetCore_Mvc_Razor_RazorPage_Context) 속성을 통해 `HttpContext`를 직접 노출합니다. 다음 예제에서는 Windows 인증을 사용하여 인트라넷 앱에서 현재 사용자 이름을 검색합니다.

```cshtml
@{
    var username = Context.User.Identity.Name;
}
```

## <a name="use-httpcontext-from-a-controller"></a>컨트롤러에서 HttpContext 사용

컨트롤러는 다음과 같이 [ControllerBase.HttpContext](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.httpcontext) 속성을 공개합니다.

```csharp
public class HomeController : Controller
{
    public IActionResult About()
    {
        var pathBase = HttpContext.Request.PathBase;
        // Do something with the PathBase.

        return View();
    }
}
```

## <a name="use-httpcontext-from-middleware"></a>미들웨어에서 HttpContext 사용

사용자 지정 미들웨어 구성 요소를 사용할 경우 `HttpContext`는 `Invoke` 또는 `InvokeAsync` 메서드로 전달되며 미들웨어가 구성될 때 액세스할 수 있습니다.

```csharp
public class MyCustomMiddleware
{
    public Task InvokeAsync(HttpContext context)
    {
        // Middleware initialization optionally using HttpContext
    }
}
```

## <a name="use-httpcontext-from-custom-components"></a>사용자 지정 구성 요소에서 HttpContext 사용

`HttpContext`에 액세스해야 하는 기타 프레임워크 및 사용자 지정 구성 요소의 경우 기본 제공 [종속성 주입](xref:fundamentals/dependency-injection) 컨테이너를 사용하여 종속성을 등록하는 것이 좋습니다. 종속성 주입 컨테이너는 `IHttpContextAccessor`를 해당 생성자에서 종속성으로 선언하는 모든 클래스에 이를 제공합니다.

::: moniker range=">= aspnetcore-2.1"

```csharp
public void ConfigureServices(IServiceCollection services)
{
     services.AddMvc()
         .SetCompatibilityVersion(CompatibilityVersion.Version_2_1);
     services.AddHttpContextAccessor();
     services.AddTransient<IUserRepository, UserRepository>();
}
```

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

```csharp
public void ConfigureServices(IServiceCollection services)
{
     services.AddMvc();
     services.AddSingleton<IHttpContextAccessor, HttpContextAccessor>();
     services.AddTransient<IUserRepository, UserRepository>();
}
```

::: moniker-end

다음 예제에서는

* `UserRepository`는 `IHttpContextAccessor`에 대한 종속성을 선언합니다.
* 종속성 주입이 종속성 체인을 확인하고 `UserRepository` 인스턴스를 만들 경우 종속성이 제공됩니다.

```csharp
public class UserRepository : IUserRepository
{
    private readonly IHttpContextAccessor _httpContextAccessor;

    public UserRepository(IHttpContextAccessor httpContextAccessor)
    {
        _httpContextAccessor = httpContextAccessor;
    }

    public void LogCurrentUser()
    {
        var username = _httpContextAccessor.HttpContext.User.Identity.Name;
        service.LogAccessRequest(username);
    }
}
```
