---
title: "단순 권한 부여"
author: rick-anderson
description: "이 문서에서는 ASP.NET Core 컨트롤러 및 동작에 대 한 액세스를 제한 하려면 권한 부여 특성을 사용 하는 방법에 설명 합니다."
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authorization/simple
ms.openlocfilehash: 503ebc665efd460a85f49844ddc847eb12114308
ms.sourcegitcommit: b83a5f731a9c02bdb1cc1e3f9a8bf273eb5b33e0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2018
---
# 단순 권한 부여

<a name="security-authorization-simple"></a>

MVC에서 권한 부여를 통해 제어 됩니다는 `AuthorizeAttribute` 특성 및 해당 다양 한 매개 변수입니다. 가장 간단한 적용 된 `AuthorizeAttribute` 특성는 컨트롤러나 작업 제한에 대 한 액세스는 컨트롤러 또는 모든 인증 된 사용자 동작을 합니다.

예를 들어, 다음 코드는 `AccountController` 접근을 인증된 사용자로 제한합니다.

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

사용할 수도 있습니다는 `AllowAnonymous` 특성 개별 작업에 대 한 인증 되지 않은 사용자가 액세스할 수 있도록 합니다. 예:

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

이렇게 하면 인증된 사용자만 `AccountController`에 허용되는데 예외적으로 `Login` 동작은 인증 여부에 관계없이 모두가 접근할 수 있습니다.

>[!WARNING]
> `[AllowAnonymous]`는 모든 권한부여 구문을 무시합니다. 만약 `[AllowAnonymous]`와 어떤 `[Authorize]` 특성을 조합해 적용하면 `[Authorize]` 특성은 항상 무시됩니다. 예를 들어 `[AllowAnonymous]`를 컨트롤러 수준에 적용하면 해당 컨트롤러와 내부 동작의 모든 `[Authorize]` 특성은 무시됩니다.
