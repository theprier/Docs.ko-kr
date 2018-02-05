---
title: "ASP.NET Core의 사용자 지정 정책 기반 권한 부여"
author: rick-anderson
description: "ASP.NET Core 응용 프로그램에서 사용자 지정 권한 정책 처리기를 작성 및 사용해서 권한 부여 요구 사항을 적용하는 방법을 알아봅니다."
keywords: "ASP.NET Core, 권한 부여, 사용자 지정 정책, 권한 부여 정책"
ms.author: riande
ms.custom: mvc
manager: wpickett
ms.date: 11/21/2017
ms.topic: article
ms.assetid: e422a1b2-dc4a-4bcc-b8d9-7ee62009b6a3
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authorization/policies
ms.openlocfilehash: 280dd72b75e39546061d8455931f597f50c829fe
ms.sourcegitcommit: f1436107b4c022b26f5235dddef103cec5aa6bff
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/15/2017
---
# <a name="custom-policy-based-authorization"></a>사용자 지정 정책 기반 권한 부여

[역할 기반 권한 부여](xref:security/authorization/roles) 및 [클레임 기반 권한 부여](xref:security/authorization/claims)는 내부적으로 요구 사항, 요구 사항 처리기, 그리고 미리 구성된 정책을 사용합니다. 이런 빌딩 블록들은 권한 부여 평가를 코드로 표현할 수 있는 기능을 지원합니다. 결과적으로 보다 풍부하고 재사용 가능하며 테스트 가능한 권한 부여 구조를 만들 수 있습니다.

권한 부여 정책은 하나 이상의 요구 사항으로 구성됩니다. 그리고 응용 프로그램 시작 시에 `Startup` 클래스의 `ConfigureServices` 메서드에서 Authorization 서비스 구성의 일부로 등록됩니다:

[!code-csharp[](policies/samples/PoliciesAuthApp1/Startup.cs?range=40-41,50-55,63,72)]

위의 예제는 "AtLeast21"이라는 정책을 생성합니다. 이 정책은 요구 사항의 매개 변수로 제공되는, 최소 연령을 뜻하는 단일 요구 사항을 갖습니다.

정책은 정책 이름을 지정한 `[Authorize]` 특성을 통해서 적용됩니다. 다음은 그 예입니다:

[!code-csharp[](policies/samples/PoliciesAuthApp1/Controllers/AlcoholPurchaseController.cs?name=snippet_AlcoholPurchaseControllerClass&highlight=4)]

## <a name="requirements"></a>요구 사항

권한 부여 요구 사항은 정책이 현재 사용자의 신원을 평가하기 위해서 사용할 수 있는 데이터 매개 변수들의 모음입니다. 본문의 "AtLeast21" 정책의 경우, 요구 사항은 단일 매개 변수, 즉 최소 연령입니다. 요구 사항은 빈 표식 인터페이스인 `IAuthorizationRequirement` 인터페이스를 구현합니다. 매개변수화 된 최소 연령 요구 사항은 다음과 같이 구현할 수 있습니다:

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Requirements/MinimumAgeRequirement.cs?name=snippet_MinimumAgeRequirementClass)]

> [!NOTE]
> 요구 사항의 데이터나 속성은 필수가 아닙니다.

<a name="security-authorization-policies-based-authorization-handler"></a>

## <a name="authorization-handlers"></a>권한 부여 처리기

권한 부여 처리기는 요구 사항의 속성을 평가하는 역할을 담당합니다. 권한 부여 처리기는 제공된 `AuthorizationHandlerContext`를 대상으로 요구 사항 평가를 수행해서 권한 허용 여부를 결정합니다. 하나의 요구 사항에 [여러 개의 처리기](#security-authorization-policies-based-multiple-handlers)가 존재할 수 있습니다. 처리기는 `AuthorizationHandler<T>`를 상속받으며, 여기서 `T`는 처리해야 할 요구 사항입니다.

<a name="security-authorization-handler-example"></a>

최소 연령 처리기는 다음처럼 구현할 수 있습니다:

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/MinimumAgeHandler.cs?name=snippet_MinimumAgeHandlerClass)]

이 코드는 먼저 현재 사용자의 신원이 우리가 알고 있고 신뢰할 수 있는 발급자로부터 발급된 생년월일 클레임을 갖고 있는지부터 확인합니다. 만약 클레임이 누락되었다면 권한을 부여할 수 없으므로 완료된 작업이 반환됩니다. 반면 클레임이 존재할 경우, 사용자의 나이가 계산됩니다. 그리고 나이가 요구 사항에 의해 정의된 최소 연령을 만족할 경우 권한 부여가 성공한 것으로 간주됩니다. 권한 부여가 성공하면 만족한 요구 사항을 매개 변수로 전달해서 `context.Succeed` 메서드를 호출합니다.

<a name="security-authorization-policies-based-handler-registration"></a>

### <a name="handler-registration"></a>처리기 등록하기

처리기는 구성 과정 중 서비스 컬렉션에 등록됩니다. 다음은 그 예입니다:

[!code-csharp[](policies/samples/PoliciesAuthApp1/Startup.cs?range=40-41,50-55,63-65,72)]

각각의 처리기는 `services.AddSingleton<IAuthorizationHandler, YourHandlerClass>();`을 호출해서 서비스 컬렉션에 추가됩니다.

## <a name="what-should-a-handler-return"></a>처리기가 반환해야 하는 결과는?

본문의 [처리기 예제](#security-authorization-handler-example)에서 `Handle` 메서드가 아무런 값도 반환하지 않는다는 점에 주목하시기 바랍니다. 그렇다면 성공 혹은 실패 여부는 어떻게 확인할 수 있을까요?

* 처리기는 성공적으로 검증된 요구 사항을 `context.Succeed(IAuthorizationRequirement requirement)`에 매개 변수로 전달하여 호출함으로써 성공했음을 나타냅니다.

* 일반적으로 처리기는 실패를 처리할 필요가 없는데, 동일한 요구 사항에 대한 다른 처리기가 성공할 수도 있기 때문입니다.

* 다른 처리기의 성공 여부와 관계없이 무조건 실패한 것으로 나타내려면 `context.Fail`을 호출합니다.

정책이 임의의 요구 사항을 필요로 할 경우, 처리기 내부에서 무엇을 호출하는 지와 무관하게 요구 사항과 관련된 모든 처리기가 호출됩니다. 따라서 다른 처리기에서 `context.Fail()`이 호출되는 경우에도, 로깅 같은 요구 사항의 부수적인 작업들은 항상 수행됩니다.

<a name="security-authorization-policies-based-multiple-handlers"></a>

## <a name="why-would-i-want-multiple-handlers-for-a-requirement"></a>요구 사항에 대해 여러 개의 처기리가 필요한 이유는?

만약 **OR** 기반의 평가를 수행하고 싶다면 단일 요구 사항에 대한 여러 개의 처리기를 구현해야 합니다. 예를 들어, Microsoft에는 키 카드로만 열 수 있는 문이 있습니다. 그런데 만약 키 카드를 집에 두고 왔다면 접수원이 임시 스티커를 인쇄하고 대신 문을 열어줍니다. 이 시나리오의 경우, 요구 사항은 *EnterBuilding* 하나지만 여러 처리기가 단일 요구 사항을 각각 개별적으로 검토하게 됩니다.

*BuildingEntryRequirement.cs*

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Requirements/BuildingEntryRequirement.cs?name=snippet_BuildingEntryRequirementClass)]

*BadgeEntryHandler.cs*

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/BadgeEntryHandler.cs?name=snippet_BadgeEntryHandlerClass)]

*TemporaryStickerHandler.cs*

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/TemporaryStickerHandler.cs?name=snippet_TemporaryStickerHandlerClass)]

두 처리기가 모두 [등록되어 있는지](xref:security/authorization/policies#security-authorization-policies-based-handler-registration) 확인합니다. 정책이 `EnterBuildingRequirement`를 평가할 때, 두 처리기 중 하나라도 성공하면 정책 평가가 성공한 것으로 간주됩니다.

## <a name="using-a-func-to-fulfill-a-policy"></a>func를 이용해서 정책 구성하기

코드로 정책을 표현해서 구성하는 편이 더 간단한 경우도 있습니다. 정책을 구성할 때 `RequireAssertion` 정책 빌더에 `Func<AuthorizationHandlerContext, bool>`을 전달할 수 있습니다.

예를 들어, 앞에서 살펴본 `BadgeEntryHandler`는 다음과 같이 재작성할 수 있습니다:

[!code-csharp[](policies/samples/PoliciesAuthApp1/Startup.cs?range=52-53,57-63)]

## <a name="accessing-mvc-request-context-in-handlers"></a>처리기에서 MVC 요청 컨텍스트 접근하기

권한 부여 처리기에서 구현해야 하는 `HandleRequirementAsync` 메서드에는 `AuthorizationHandlerContext`와 처리 중인 `TRequirement`라는 두 개의 매개 변수가 존재합니다. MVC나 Jabbr 같은 프레임워크는 `AuthorizationHandlerContext`의 `Resource` 속성에 자유롭게 개체를 추가해서 추가적인 정보를 전달할 수 있습니다.

예를 들어, MVC는 `Resource` 속성에 [AuthorizationFilterContext](/dotnet/api/?term=AuthorizationFilterContext)의 인스턴스를 전달합니다. 이 속성은 `HttpContext`나 `RouteData`를 비롯한, MVC 및 Razor 페이지가 제공하는 다양한 정보들에 대한 접근을 제공합니다.

`Resource` 속성을 사용하는 방식은 프레임워크에 따라서 달라집니다. 따라서 `Resource` 속성의 정보를 사용할 경우 권한 부여 정책이 특정 프레임워크에 제한될 수 있습니다. 따라서 먼저 `as` 키워드를 사용해서 `Resource` 속성의 형변환을 시도한 다음, 형변환이 성공했는지 여부를 확인해서 처리기가 다른 프레임워크에서 실행될 때 `InvalidCastExceptions` 예외가 발생하지 않도록 주의해야 합니다:

```csharp
// Requires the following import:
//     using Microsoft.AspNetCore.Mvc.Filters;
if (context.Resource is AuthorizationFilterContext mvcContext)
{
    // Examine MVC-specific things like routing data.
}
```
