---
title: ASP.NET Core에서 단순 권한 부여
author: rick-anderson
description: ASP.NET Core 컨트롤러 및 동작에 대 한 액세스를 제한 하려면 권한 부여 특성을 사용 하는 방법에 알아봅니다.
ms.author: riande
ms.date: 10/14/2016
uid: security/authorization/simple
ms.openlocfilehash: 6409def0508b855d3d2a4a1f4d3a3d15bfe5dd32
ms.sourcegitcommit: 356c8d394aaf384c834e9c90cabab43bfe36e063
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2018
ms.locfileid: "36961125"
---
# <a name="simple-authorization-in-aspnet-core"></a>ASP.NET Core에서 단순 권한 부여

<a name="security-authorization-simple"></a>

MVC에서 권한 부여를 통해 제어 됩니다는 `AuthorizeAttribute` 특성 및 해당 다양 한 매개 변수입니다. 가장 간단한 적용 된 `AuthorizeAttribute` 특성는 컨트롤러나 작업 제한에 대 한 액세스는 컨트롤러 또는 모든 인증 된 사용자 동작을 합니다.

다음 코드에 대 한 액세스를 제한 하는 예를 들어는 `AccountController` 모든 인증 된 사용자입니다.

```csharp
[Authorize]
public class AccountController : Controller
{
    public ActionResult Login()
    {
    }

    public ActionResult Logout()
    {
    }
}
```

컨트롤러 아니라 작업에 권한 부여를 적용 하려면 적용 된 `AuthorizeAttribute` 동작 자체에 특성:

```csharp
public class AccountController : Controller
{
   public ActionResult Login()
   {
   }

   [Authorize]
   public ActionResult Logout()
   {
   }
}
```

이제 인증 된 사용자만 액세스할 수는 `Logout` 함수입니다.

사용할 수도 있습니다는 `AllowAnonymous` 특성 개별 작업에 대 한 인증 되지 않은 사용자가 액세스할 수 있도록 합니다. 예를 들어:

```csharp
[Authorize]
public class AccountController : Controller
{
    [AllowAnonymous]
    public ActionResult Login()
    {
    }

    public ActionResult Logout()
    {
    }
}
```

이렇게 하면 인증 된 사용자만는 `AccountController`를 제외 하 고는 `Login` / 익명 인증 된 인증 되지 않은 상태에 관계 없이 모든 사용자가 액세스할 수 있는 작업입니다.

> [!WARNING]
> `[AllowAnonymous]` 모든 권한 부여 문을 무시합니다. 결합 하면 `[AllowAnonymous]` 임의의 `[Authorize]` 특성에는 `[Authorize]` 특성은 무시 됩니다. 예를 적용 하는 경우 `[AllowAnonymous]` 컨트롤러 수준에서 모든 `[Authorize]` 동일한 컨트롤러에서 (또는 그 안에 모든 작업에) 특성은 무시 됩니다.
