---
title: "ASP.NET Core에서 정책 기반 사용자 지정 권한 부여"
author: rick-anderson
description: "만들고 ASP.NET Core 응용 프로그램에서 권한 부여 요구 사항을 적용 하기 위한 사용자 지정 권한 부여 정책 처리기를 사용 하는 방법을 알아봅니다."
ms.author: riande
ms.custom: mvc
manager: wpickett
ms.date: 11/21/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authorization/policies
ms.openlocfilehash: 1067e97dd6e71021929aa3690b0c3f5bfc6c9724
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="custom-policy-based-authorization"></a>사용자 지정 정책 기반 권한 부여

내부적 [역할 기반 권한 부여](xref:security/authorization/roles) 및 [클레임 기반 권한 부여](xref:security/authorization/claims) 요구, 요구 사항 처리기 및 미리 구성 된 정책을 사용 합니다. 이러한 빌딩 블록 코드에서 권한 부여 평가 식을 지원합니다. 결과 다양 한 재사용 가능한 하 고 테스트 가능 권한 부여 구조입니다.

권한 부여 정책 하나 이상의 요구 사항으로 구성 됩니다. 에 등록 되어 있는 권한 부여 서비스 구성의 일부로 `ConfigureServices` 의 메서드는 `Startup` 클래스:

[!code-csharp[](policies/samples/PoliciesAuthApp1/Startup.cs?range=40-41,50-55,63,72)]

앞의 예제에서 "AtLeast21" 정책을 만듭니다. 단일 반드시 그래야 하의 최소 연령 제공 되는 요구 사항에 매개 변수로 가집니다.

사용 하 여 정책이 적용 되는 `[Authorize]` 정책 이름 가진 특성이 있습니다. 예:

[!code-csharp[](policies/samples/PoliciesAuthApp1/Controllers/AlcoholPurchaseController.cs?name=snippet_AlcoholPurchaseControllerClass&highlight=4)]

## <a name="requirements"></a>요구 사항

권한 부여 요구 사항은 현재 사용자 보안 주체를 평가 하는 정책을 사용할 수 있는 데이터 매개 변수 컬렉션입니다. 보호 "AtLeast21" 정책 요구 사항이 단일 매개 변수는&mdash;최소 보존 기간입니다. 요구 사항 구현 `IAuthorizationRequirement`, 빈 표식 인터페이스인 합니다. 매개 변수가 있는 최소 연령 요구 사항 다음과 같이 구현 될 수 없습니다.

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Requirements/MinimumAgeRequirement.cs?name=snippet_MinimumAgeRequirementClass)]

> [!NOTE]
> 데이터 또는 속성 요구 사항 필요 하지 않습니다.

<a name="security-authorization-policies-based-authorization-handler"></a>

## <a name="authorization-handlers"></a>권한 부여 처리기

권한 부여 처리기는 평가 요구 사항 속성의 담당 합니다. 제공 된 작업에 대 한 요구 사항을 평가 하는 권한 부여 처리기 `AuthorizationHandlerContext` 액세스 허용 확인 하려면. 요구 사항이 있을 수 있습니다 [여러 처리기](#security-authorization-policies-based-multiple-handlers)합니다. 처리기 상속 `AuthorizationHandler<T>`여기서 `T` 처리 요구 사항입니다.

<a name="security-authorization-handler-example"></a>

최소 보존 기간 처리기는 다음과 같습니다.

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/MinimumAgeHandler.cs?name=snippet_MinimumAgeHandlerClass)]

위의 코드에 알려지고 신뢰할 수 있는 발급자가 발급 하는 클레임 생년월일 날짜는 현재 사용자 계정이 있는지 확인 합니다. 권한 부여 클레임 누락 되었을 때 발생할 수 없습니다, 그리고 완료 된 작업 반환 되는 경우. 클레임에 있는 경우 사용자의 나이 계산 됩니다. 사용자 요구 사항에 정의 된 최소 보존 기간을 충족할 경우 권한 부여를 성공적으로 간주 됩니다. 부여 된, `context.Succeed` 매개 변수로 만족된 요구를 사용 하 여 호출 합니다.

<a name="security-authorization-policies-based-handler-registration"></a>

### <a name="handler-registration"></a>처리기를 등록

처리기는 구성 하는 동안 서비스 컬렉션에 등록 됩니다. 예:

[!code-csharp[](policies/samples/PoliciesAuthApp1/Startup.cs?range=40-41,50-55,63-65,72)]

각 처리기가 호출 하 여 서비스 컬렉션에 추가 `services.AddSingleton<IAuthorizationHandler, YourHandlerClass>();`합니다.

## <a name="what-should-a-handler-return"></a>처리기를 반환 해야?

`Handle` 에서 메서드는 [처리기 예제](#security-authorization-handler-example) 아무 값도 반환 합니다. 성공 또는 실패를 표시 된 상태는 어떻게 합니까?

* 처리기를 호출 하 여이 성공 했음을 의미 `context.Succeed(IAuthorizationRequirement requirement)`, 된 요구 사항을 전달 성공적으로 확인 되었습니다.

* 처리기를 배포할 수 있습니다. 동일한 요구 사항에 대해 다른 처리기 처럼 일반적으로 오류를 처리 하도록 필요는 없습니다.

* 오류, 다른 요구 사항을 처리기 성공 하는 경우에, 호출 `context.Fail`합니다.

어떤 내부 처리기를 호출 하는 것에 관계 없이 정책 요구 사항에서 요구 하는 경우 요구 사항에 대 한 모든 처리기가 호출 됩니다. 이렇게 하면 요구 사항에는 항상 적용 하는 로깅 같은 의도 하지 않은 경우에 `context.Fail()` 다른 처리기에서 호출 되었습니다.

<a name="security-authorization-policies-based-multiple-handlers"></a>

## <a name="why-would-i-want-multiple-handlers-for-a-requirement"></a>이유는 여러 처리기는 요구 사항에 대 한?

에 있는 것으로 평가 하려는 경우에는 **또는** 별로 단일 요구 사항에 대해 여러 처리기를 구현 합니다. 예를 들어 Microsoft는 주요 카드를 사용 하는 열만 있는 문. 키 카드를 집에 두면 접수원 임시 스티커 인쇄 하 고 사용자에 대 한 문을 엽니다. 이 시나리오에서는 단일 요구 사항, 갖기 *BuildingEntry*, 하지만 단일 요구 사항 검사 하나씩 여러 처리기입니다.

*BuildingEntryRequirement.cs*

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Requirements/BuildingEntryRequirement.cs?name=snippet_BuildingEntryRequirementClass)]

*BadgeEntryHandler.cs*

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/BadgeEntryHandler.cs?name=snippet_BadgeEntryHandlerClass)]

*TemporaryStickerHandler.cs*

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/TemporaryStickerHandler.cs?name=snippet_TemporaryStickerHandlerClass)]

이 두 처리기 되는지 확인 [등록](xref:security/authorization/policies#security-authorization-policies-based-handler-registration)합니다. 어느 처리기 성공 때 정책을 평가 `BuildingEntryRequirement`, 정책 평가 성공 합니다.

## <a name="using-a-func-to-fulfill-a-policy"></a>Func는 정책을 처리 하는 데 사용 하 여

정책을 코드에서 표현 하기 간단 따르는 데는 경우가 있습니다. 제공 하는 것이 불가능 한 `Func<AuthorizationHandlerContext, bool>` 와 정책을 구성할 때는 `RequireAssertion` 정책 작성기.

예를 들어 이전 `BadgeEntryHandler` 다음과 같이 다시 작성할 수 있습니다.

[!code-csharp[](policies/samples/PoliciesAuthApp1/Startup.cs?range=52-53,57-63)]

## <a name="accessing-mvc-request-context-in-handlers"></a>처리기에서 MVC 요청 컨텍스트 액세스

`HandleRequirementAsync` 권한 부여 처리기에서 구현 하는 메서드에 두 개의 매개 변수가:는 `AuthorizationHandlerContext` 및 `TRequirement` 처리 됩니다. MVC 또는 Jabbr 등의 프레임 워크는에 개체를 추가할 수는 `Resource` 속성에는 `AuthorizationHandlerContext` 추가 정보를 전달 합니다.

MVC의 인스턴스를 전달 하는 예를 들어 [AuthorizationFilterContext](/dotnet/api/?term=AuthorizationFilterContext) 에 `Resource` 속성입니다. 이 속성에 대 한 액세스를 제공 `HttpContext`, `RouteData`, 그리고 다른 MVC 및 Razor 페이지에서 제공 합니다.

사용 하 여 `Resource` 속성은 특정 프레임 워크입니다. 정보를 사용 하는 `Resource` 속성 권한 부여 정책을 특정 프레임 워크를 제한 합니다. 캐스팅 해야는 `Resource` 사용 하 여 속성은 `as` 키워드를 선택한 다음 해당 캐스트의 코드 충돌 하지 않습니다 확인에 성공 했습니다 확인으로 `InvalidCastException` 다른 프레임 워크에서 실행할 때:

```csharp
// Requires the following import:
//     using Microsoft.AspNetCore.Mvc.Filters;
if (context.Resource is AuthorizationFilterContext mvcContext)
{
    // Examine MVC-specific things like routing data.
}
```
