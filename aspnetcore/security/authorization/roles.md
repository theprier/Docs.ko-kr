---
title: "역할 기반 권한 부여"
author: rick-anderson
description: "이 문서에는 역할 권한 부여 속성에 전달 하 여 ASP.NET Core 컨트롤러 및 작업 액세스를 제한 하는 방법을 보여 줍니다."
keywords: "ASP.NET Core, 역할, 권한 부여"
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: 5e014da1-8bc0-409b-951a-88b92c661fdf
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authorization/roles
ms.openlocfilehash: 26babef1a296aaa1fa11f36d30c4d911d73808ce
ms.sourcegitcommit: df2157ae9aeea0075772719c29784425c783e82a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/10/2018
---
# <a name="role-based-authorization"></a>역할 기반 권한 부여

<a name="security-authorization-role-based"></a>

신원(Identity)이 생성될 때 해당 신원은 하나 이상의 역할에 속할 수 있습니다. 예를 들어, Tracy는 Administrator 및 User 역할에 동시에 속하지만 Scott은 User 역할에만 속하는 것처럼 말입니다. 이런 역할들이 생성되고 관리되는 방식은 권한 부여 프로세스에 사용되는 백업 저장소에 따라서 달라집니다. 개발자는 [ClaimsPrincipal](https://docs.microsoft.com/dotnet/api/system.security.claims.claimsprincipal) 클래스의 [IsInRole](https://docs.microsoft.com/dotnet/api/system.security.principal.genericprincipal.isinrole) 메서드를 이용해서 역할에 접근할 수 있습니다.

## <a name="adding-role-checks"></a>역할 검사 추가하기

역할 기반 권한 부여의 검사는 선언적으로 구성됩니다. 개발자는 컨트롤러나 컨트롤러 내의 개별 액션에 대해 현재 사용자가 요청한 리소스에 접근하기 위해 반드시 속해 있어야만 하는 역할을 지정해서 이를 코드 내부에 포함시킵니다.

예를 들어, 다음 코드는 `Administrator` 역할에 속한 사용자만 `AdministrationController`의 모든 액션에 접근할 수 있도록 제한합니다:

```csharp
[Authorize(Roles = "Administrator")]
public class AdministrationController : Controller
{
}
```

쉼표(,)로 구분된 목록을 지정해서 여러 역할을 지정할 수도 있습니다:

```csharp
[Authorize(Roles = "HRManager,Finance")]
public class SalaryController : Controller
{
}
```

이 컨트롤러는 `HRManager` 역할이나 `Finance` 역할에 속한 사용자만 접근할 수 있습니다.

만약 여러 특성을 지정했다면, 접근하는 사용자는 지정된 모든 역할에 속해야만 합니다. 다음 예제에서 사용자는 `PowerUser` 및 `ControlPanelUser` 역할 모두에 속해 있어야만 합니다:

```csharp
[Authorize(Roles = "PowerUser")]
[Authorize(Roles = "ControlPanelUser")]
public class ControlPanelController : Controller
{
}
```

액션 수준에 역할 권한 부여 특성을 추가로 적용해서 접근을 더욱 제한할 수도 있습니다:

```csharp
[Authorize(Roles = "Administrator, PowerUser")]
public class ControlPanelController : Controller
{
    public ActionResult SetTime()
    {
    }

    [Authorize(Roles = "Administrator")]
    public ActionResult ShutDown()
    {
    }
}
```

위의 코드 조각의 경우, `Administrator` 역할이나 `PowerUser` 역할에 속한 사용자는 컨트롤러와 `SetTime` 액션에 접근할 수 있지만, `ShutDown` 액션은 `Administrator` 역할에 속한 사용자만 접근이 가능합니다.

또는 컨트롤러 자체는 잠그지만, 개별 액션에 대한 인증되지 않은 익명 사용자의 접근은 허용할 수도 있습니다:

```csharp
[Authorize]
public class ControlPanelController : Controller
{
    public ActionResult SetTime()
    {
    }

    [AllowAnonymous]
    public ActionResult Login()
    {
    }
}
```

<a name="security-authorization-role-policy"></a>

## <a name="policy-based-role-checks"></a>정책 기반 역할 검사

역할 요구 사항은 응용 프로그램 시작 시 개발자가 Authorization 서비스 구성의 일부로 정책을 등록하는 새로운 Policy 구문을 사용해서 표현할 수도 있습니다. 일반적으로 이 작업은 *Startup.cs* 파일의 `ConfigureServices()`에서 수행됩니다:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();

    services.AddAuthorization(options =>
    {
        options.AddPolicy("RequireAdministratorRole", policy => policy.RequireRole("Administrator"));
    });
}
```

정책은 `Authorize` 특성의 `Policy` 속성을 통해서 적용됩니다:

```csharp
[Authorize(Policy = "RequireAdministratorRole")]
public IActionResult Shutdown()
{
    return View();
}
```

하나의 요구 사항에 허용되는 여러 역할을 지정하고 싶다면 해당 역할들을 `RequireRole` 메서드에 매개 변수로 전달하면 됩니다:

```csharp
options.AddPolicy("ElevatedRights", policy =>
                  policy.RequireRole("Administrator", "PowerUser", "BackupAdministrator"));
```

이 예제는 `Administrator`, `PowerUser` 또는 `BackupAdministrator` 역할에 속한 사용자에게 권한을 부여합니다.
