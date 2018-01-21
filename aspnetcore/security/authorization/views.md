---
title: "ASP.NET Core MVC에서 보기 기반 권한 부여"
author: rick-anderson
description: "이 문서에 삽입 하 고 ASP.NET Core Razor 뷰 내에 권한 부여 서비스를 사용 하는 방법을 보여 줍니다."
ms.author: riande
manager: wpickett
ms.date: 10/30/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authorization/views
ms.openlocfilehash: 8f87ca90b77be1efd75688e8203cb57b1a3360ad
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="view-based-authorization"></a>보기 기반 권한 부여

하려는 개발자는 종종 표시, 숨기기, 그렇지 않으면 현재 사용자 id에 따라 UI를 수정 합니다. 권한 부여 서비스를 통해 MVC 뷰 내에서 액세스할 수 있습니다 [종속성 주입](xref:fundamentals/dependency-injection#fundamentals-dependency-injection)합니다. 에 삽입 하는 권한 부여 서비스 Razor 뷰를 사용 하 여는 `@inject` 지시문:

```cshtml
@using Microsoft.AspNetCore.Authorization
@inject IAuthorizationService AuthorizationService
```

모든 보기에서 권한 부여 서비스 배치는 `@inject` 지시문에 *_ViewImports.cshtml* 의 파일은 *뷰* 디렉터리입니다. 자세한 내용은 참조 [뷰로 종속성 주입](xref:mvc/views/dependency-injection)합니다.

삽입 된 권한 부여 서비스를 사용 하 여 호출할 `AuthorizeAsync` 정확히 같은 방식 중 체크 [리소스 기반 권한 부여](xref:security/authorization/resourcebased#security-authorization-resource-based-imperative):

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```cshtml
@if ((await AuthorizationService.AuthorizeAsync(User, "PolicyName")).Succeeded)
{
    <p>This paragraph is displayed because you fulfilled PolicyName.</p>
}
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

```cshtml
@if (await AuthorizationService.AuthorizeAsync(User, "PolicyName"))
{
    <p>This paragraph is displayed because you fulfilled PolicyName.</p>
}
```

---

경우에 따라 리소스 보기 모델 됩니다. 호출 `AuthorizeAsync` 정확히 같은 방식 중 체크 [리소스 기반 권한 부여](xref:security/authorization/resourcebased#security-authorization-resource-based-imperative):

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

```cshtml
@if ((await AuthorizationService.AuthorizeAsync(User, Model, Operations.Edit)).Succeeded)
{
    <p><a class="btn btn-default" role="button"
        href="@Url.Action("Edit", "Document", new { id = Model.Id })">Edit</a></p>
}
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

```cshtml
@if (await AuthorizationService.AuthorizeAsync(User, Model, Operations.Edit))
{
    <p><a class="btn btn-default" role="button"
        href="@Url.Action("Edit", "Document", new { id = Model.Id })">Edit</a></p>
}
```

---

위의 코드에서 모델을 고려 정책 평가 수행 해야 하는 리소스로 전달 됩니다.

> [!WARNING]
> 유일한 권한 확인으로 응용 프로그램의 UI 요소의 토글 표시 여부에 의존 하지 마십시오. UI 요소를 숨기 거 수 있습니다 완전히 되지 액세스 하는 연결 된 컨트롤러 작업이 있습니다. 예를 들어 앞의 코드 조각에 있는 단추를 것이 좋습니다. 사용자가 호출할 수는 `Edit` 동작 메서드는 상대 리소스를 자신이 알고 있는 경우 URL이 */Document/Edit/1*합니다. 이러한 이유로 `Edit` 동작 메서드는 자체 권한 부여 확인을 수행 해야 합니다.
