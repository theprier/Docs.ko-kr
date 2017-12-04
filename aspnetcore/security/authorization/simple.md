---
title: "단순 권한 부여"
author: rick-anderson
description: 
keywords: ASP.NET Core
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: 391bcaad-205f-43e4-badc-fa592d6f79f3
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authorization/simple
ms.openlocfilehash: 013ce0d9ac1e9c1b6bb541b9fa66218c3fd799bb
ms.sourcegitcommit: 0b6c8e6d81d2b3c161cd375036eecbace46a9707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/11/2017
---
# 단순 권한 부여

<a name=security-authorization-simple></a>

MVC에서 권한부여는 `AuthorizeAttribute` 특성과 이 특성의 여러 매개 변수를 통해 제어됩니다. 가장 단순한 경우, 컨트롤러나 동작에 `AuthorizeAttribute` 특성을 적용하면 인증된 사용자만 해당 컨트롤러나 동작에 접근할 수 있도록 제한됩니다.

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

만약 권한부여를 컨트롤러가 아니라 동작에 적용하고 싶다면 단순하게 동작 자체에 `AuthorizeAttribute` 특성을 적용하세요.

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

이제 인증된 사용자만 `Logout` 함수에 접근할 수 있습니다.

개별 동작에 인증되지 않은 사용자의 접근을 허용하기 위해 `AllowAnonymousAttribute` 특성을 사용할 수도 있습니다. 예를 들어:

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
