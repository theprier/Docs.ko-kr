---
title: "ASP.NET Core에서 정책 기반 사용자 지정 권한 부여"
author: rick-anderson
description: "만들고 ASP.NET Core 응용 프로그램에서 권한 부여 요구 사항을 적용 하기 위한 사용자 지정 권한 부여 정책 처리기를 사용 하는 방법을 알아봅니다."
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
# <a name="custom-policy-based-authorization"></a><span data-ttu-id="8eb37-104">사용자 지정 정책 기반 권한 부여</span><span class="sxs-lookup"><span data-stu-id="8eb37-104">Custom policy-based authorization</span></span>

<span data-ttu-id="8eb37-105">내부적 [역할 기반 권한 부여](xref:security/authorization/roles) 및 [클레임 기반 권한 부여](xref:security/authorization/claims) 요구, 요구 사항 처리기 및 미리 구성 된 정책을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-105">Underneath the covers, [role-based authorization](xref:security/authorization/roles) and [claims-based authorization](xref:security/authorization/claims) use a requirement, a requirement handler, and a pre-configured policy.</span></span> <span data-ttu-id="8eb37-106">이러한 빌딩 블록 코드에서 권한 부여 평가 식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-106">These building blocks support the expression of authorization evaluations in code.</span></span> <span data-ttu-id="8eb37-107">결과 다양 한 재사용 가능한 하 고 테스트 가능 권한 부여 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-107">The result is a richer, reusable, testable authorization structure.</span></span>

<span data-ttu-id="8eb37-108">권한 부여 정책 하나 이상의 요구 사항으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-108">An authorization policy consists of one or more requirements.</span></span> <span data-ttu-id="8eb37-109">에 등록 되어 있는 권한 부여 서비스 구성의 일부로 `ConfigureServices` 의 메서드는 `Startup` 클래스:</span><span class="sxs-lookup"><span data-stu-id="8eb37-109">It's registered as part of the authorization service configuration, in the `ConfigureServices` method of the `Startup` class:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Startup.cs?range=40-41,50-55,63,72)]

<span data-ttu-id="8eb37-110">앞의 예제에서 "AtLeast21" 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-110">In the preceding example, an "AtLeast21" policy is created.</span></span> <span data-ttu-id="8eb37-111">단일 반드시 그래야 하의 최소 연령 제공 되는 요구 사항에 매개 변수로 가집니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-111">It has a single requirement, that of a minimum age, which is supplied as a parameter to the requirement.</span></span>

<span data-ttu-id="8eb37-112">사용 하 여 정책이 적용 되는 `[Authorize]` 정책 이름 가진 특성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-112">Policies are applied by using the `[Authorize]` attribute with the policy name.</span></span> <span data-ttu-id="8eb37-113">예:</span><span class="sxs-lookup"><span data-stu-id="8eb37-113">For example:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Controllers/AlcoholPurchaseController.cs?name=snippet_AlcoholPurchaseControllerClass&highlight=4)]

## <a name="requirements"></a><span data-ttu-id="8eb37-114">요구 사항</span><span class="sxs-lookup"><span data-stu-id="8eb37-114">Requirements</span></span>

<span data-ttu-id="8eb37-115">권한 부여 요구 사항은 현재 사용자 보안 주체를 평가 하는 정책을 사용할 수 있는 데이터 매개 변수 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-115">An authorization requirement is a collection of data parameters that a policy can use to evaluate the current user principal.</span></span> <span data-ttu-id="8eb37-116">보호 "AtLeast21" 정책 요구 사항이 단일 매개 변수는&mdash;최소 보존 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-116">In our "AtLeast21" policy, the requirement is a single parameter&mdash;the minimum age.</span></span> <span data-ttu-id="8eb37-117">요구 사항 구현 `IAuthorizationRequirement`, 빈 표식 인터페이스인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-117">A requirement implements `IAuthorizationRequirement`, which is an empty marker interface.</span></span> <span data-ttu-id="8eb37-118">매개 변수가 있는 최소 연령 요구 사항 다음과 같이 구현 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-118">A parameterized minimum age requirement could be implemented as follows:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Requirements/MinimumAgeRequirement.cs?name=snippet_MinimumAgeRequirementClass)]

> [!NOTE]
> <span data-ttu-id="8eb37-119">데이터 또는 속성 요구 사항 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-119">A requirement doesn't need to have data or properties.</span></span>

<a name="security-authorization-policies-based-authorization-handler"></a>

## <a name="authorization-handlers"></a><span data-ttu-id="8eb37-120">권한 부여 처리기</span><span class="sxs-lookup"><span data-stu-id="8eb37-120">Authorization handlers</span></span>

<span data-ttu-id="8eb37-121">권한 부여 처리기는 평가 요구 사항 속성의 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-121">An authorization handler is responsible for the evaluation of a requirement's properties.</span></span> <span data-ttu-id="8eb37-122">제공 된 작업에 대 한 요구 사항을 평가 하는 권한 부여 처리기 `AuthorizationHandlerContext` 액세스 허용 확인 하려면.</span><span class="sxs-lookup"><span data-stu-id="8eb37-122">The authorization handler evaluates the requirements against a provided `AuthorizationHandlerContext` to determine if access is allowed.</span></span> <span data-ttu-id="8eb37-123">요구 사항이 있을 수 있습니다 [여러 처리기](#security-authorization-policies-based-multiple-handlers)합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-123">A requirement can have [multiple handlers](#security-authorization-policies-based-multiple-handlers).</span></span> <span data-ttu-id="8eb37-124">처리기 상속 `AuthorizationHandler<T>`여기서 `T` 처리 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-124">Handlers inherit `AuthorizationHandler<T>`, where `T` is the requirement to be handled.</span></span>

<a name="security-authorization-handler-example"></a>

<span data-ttu-id="8eb37-125">최소 보존 기간 처리기는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-125">The minimum age handler might look like this:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/MinimumAgeHandler.cs?name=snippet_MinimumAgeHandlerClass)]

<span data-ttu-id="8eb37-126">위의 코드에 알려지고 신뢰할 수 있는 발급자가 발급 하는 클레임 생년월일 날짜는 현재 사용자 계정이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-126">The preceding code determines if the current user principal has a date of birth claim which has been issued by a known and trusted Issuer.</span></span> <span data-ttu-id="8eb37-127">권한 부여 클레임 누락 되었을 때 발생할 수 없습니다, 그리고 완료 된 작업 반환 되는 경우.</span><span class="sxs-lookup"><span data-stu-id="8eb37-127">Authorization can't occur when the claim is missing, in which case a completed task is returned.</span></span> <span data-ttu-id="8eb37-128">클레임에 있는 경우 사용자의 나이 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-128">When a claim is present, the user's age is calculated.</span></span> <span data-ttu-id="8eb37-129">사용자 요구 사항에 정의 된 최소 보존 기간을 충족할 경우 권한 부여를 성공적으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-129">If the user meets the minimum age defined by the requirement, authorization is deemed successful.</span></span> <span data-ttu-id="8eb37-130">부여 된, `context.Succeed` 매개 변수로 만족된 요구를 사용 하 여 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-130">When authorization is successful, `context.Succeed` is invoked with the satisfied requirement as a parameter.</span></span>

<a name="security-authorization-policies-based-handler-registration"></a>

### <a name="handler-registration"></a><span data-ttu-id="8eb37-131">처리기를 등록</span><span class="sxs-lookup"><span data-stu-id="8eb37-131">Handler registration</span></span>

<span data-ttu-id="8eb37-132">처리기는 구성 하는 동안 서비스 컬렉션에 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-132">Handlers are registered in the services collection during configuration.</span></span> <span data-ttu-id="8eb37-133">예:</span><span class="sxs-lookup"><span data-stu-id="8eb37-133">For example:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Startup.cs?range=40-41,50-55,63-65,72)]

<span data-ttu-id="8eb37-134">각 처리기가 호출 하 여 서비스 컬렉션에 추가 `services.AddSingleton<IAuthorizationHandler, YourHandlerClass>();`합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-134">Each handler is added to the services collection by invoking `services.AddSingleton<IAuthorizationHandler, YourHandlerClass>();`.</span></span>

## <a name="what-should-a-handler-return"></a><span data-ttu-id="8eb37-135">처리기를 반환 해야?</span><span class="sxs-lookup"><span data-stu-id="8eb37-135">What should a handler return?</span></span>

<span data-ttu-id="8eb37-136">`Handle` 에서 메서드는 [처리기 예제](#security-authorization-handler-example) 아무 값도 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-136">Note that the `Handle` method in the [handler example](#security-authorization-handler-example) returns no value.</span></span> <span data-ttu-id="8eb37-137">성공 또는 실패를 표시 된 상태는 어떻게 합니까?</span><span class="sxs-lookup"><span data-stu-id="8eb37-137">How is a status of either success or failure indicated?</span></span>

* <span data-ttu-id="8eb37-138">처리기를 호출 하 여이 성공 했음을 의미 `context.Succeed(IAuthorizationRequirement requirement)`, 된 요구 사항을 전달 성공적으로 확인 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-138">A handler indicates success by calling `context.Succeed(IAuthorizationRequirement requirement)`, passing the requirement that has been successfully validated.</span></span>

* <span data-ttu-id="8eb37-139">처리기를 배포할 수 있습니다. 동일한 요구 사항에 대해 다른 처리기 처럼 일반적으로 오류를 처리 하도록 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-139">A handler does not need to handle failures generally, as other handlers for the same requirement may succeed.</span></span>

* <span data-ttu-id="8eb37-140">오류, 다른 요구 사항을 처리기 성공 하는 경우에, 호출 `context.Fail`합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-140">To guarantee failure, even if other requirement handlers succeed, call `context.Fail`.</span></span>

<span data-ttu-id="8eb37-141">어떤 내부 처리기를 호출 하는 것에 관계 없이 정책 요구 사항에서 요구 하는 경우 요구 사항에 대 한 모든 처리기가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-141">Regardless of what you call inside your handler, all handlers for a requirement will be called when a policy requires the requirement.</span></span> <span data-ttu-id="8eb37-142">이렇게 하면 요구 사항에는 항상 적용 하는 로깅 같은 의도 하지 않은 경우에 `context.Fail()` 다른 처리기에서 호출 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-142">This allows requirements to have side effects, such as logging, which will always take place even if `context.Fail()` has been called in another handler.</span></span>

<a name="security-authorization-policies-based-multiple-handlers"></a>

## <a name="why-would-i-want-multiple-handlers-for-a-requirement"></a><span data-ttu-id="8eb37-143">이유는 여러 처리기는 요구 사항에 대 한?</span><span class="sxs-lookup"><span data-stu-id="8eb37-143">Why would I want multiple handlers for a requirement?</span></span>

<span data-ttu-id="8eb37-144">에 있는 것으로 평가 하려는 경우에는 **또는** 별로 단일 요구 사항에 대해 여러 처리기를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-144">In cases where you want evaluation to be on an **OR** basis, implement multiple handlers for a single requirement.</span></span> <span data-ttu-id="8eb37-145">예를 들어 Microsoft는 주요 카드를 사용 하는 열만 있는 문.</span><span class="sxs-lookup"><span data-stu-id="8eb37-145">For example, Microsoft has doors which only open with key cards.</span></span> <span data-ttu-id="8eb37-146">키 카드를 집에 두면 접수원 임시 스티커 인쇄 하 고 사용자에 대 한 문을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-146">If you leave your key card at home, the receptionist prints a temporary sticker and opens the door for you.</span></span> <span data-ttu-id="8eb37-147">이 시나리오에서는 단일 요구 사항, 갖기 *BuildingEntry*, 하지만 단일 요구 사항 검사 하나씩 여러 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-147">In this scenario, you'd have a single requirement, *BuildingEntry*, but multiple handlers, each one examining a single requirement.</span></span>

<span data-ttu-id="8eb37-148">*BuildingEntryRequirement.cs*</span><span class="sxs-lookup"><span data-stu-id="8eb37-148">*BuildingEntryRequirement.cs*</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Requirements/BuildingEntryRequirement.cs?name=snippet_BuildingEntryRequirementClass)]

<span data-ttu-id="8eb37-149">*BadgeEntryHandler.cs*</span><span class="sxs-lookup"><span data-stu-id="8eb37-149">*BadgeEntryHandler.cs*</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/BadgeEntryHandler.cs?name=snippet_BadgeEntryHandlerClass)]

<span data-ttu-id="8eb37-150">*TemporaryStickerHandler.cs*</span><span class="sxs-lookup"><span data-stu-id="8eb37-150">*TemporaryStickerHandler.cs*</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/TemporaryStickerHandler.cs?name=snippet_TemporaryStickerHandlerClass)]

<span data-ttu-id="8eb37-151">이 두 처리기 되는지 확인 [등록](xref:security/authorization/policies#security-authorization-policies-based-handler-registration)합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-151">Ensure that both handlers are [registered](xref:security/authorization/policies#security-authorization-policies-based-handler-registration).</span></span> <span data-ttu-id="8eb37-152">어느 처리기 성공 때 정책을 평가 `BuildingEntryRequirement`, 정책 평가 성공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-152">If either handler succeeds when a policy evaluates the `BuildingEntryRequirement`, the policy evaluation succeeds.</span></span>

## <a name="using-a-func-to-fulfill-a-policy"></a><span data-ttu-id="8eb37-153">Func는 정책을 처리 하는 데 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="8eb37-153">Using a func to fulfill a policy</span></span>

<span data-ttu-id="8eb37-154">정책을 코드에서 표현 하기 간단 따르는 데는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-154">There may be situations in which fulfilling a policy is simple to express in code.</span></span> <span data-ttu-id="8eb37-155">제공 하는 것이 불가능 한 `Func<AuthorizationHandlerContext, bool>` 와 정책을 구성할 때는 `RequireAssertion` 정책 작성기.</span><span class="sxs-lookup"><span data-stu-id="8eb37-155">It's possible to supply a `Func<AuthorizationHandlerContext, bool>` when configuring your policy with the `RequireAssertion` policy builder.</span></span>

<span data-ttu-id="8eb37-156">예를 들어 이전 `BadgeEntryHandler` 다음과 같이 다시 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-156">For example, the previous `BadgeEntryHandler` could be rewritten as follows:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Startup.cs?range=52-53,57-63)]

## <a name="accessing-mvc-request-context-in-handlers"></a><span data-ttu-id="8eb37-157">처리기에서 MVC 요청 컨텍스트 액세스</span><span class="sxs-lookup"><span data-stu-id="8eb37-157">Accessing MVC request context in handlers</span></span>

<span data-ttu-id="8eb37-158">`HandleRequirementAsync` 권한 부여 처리기에서 구현 하는 메서드에 두 개의 매개 변수가:는 `AuthorizationHandlerContext` 및 `TRequirement` 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-158">The `HandleRequirementAsync` method you implement in an authorization handler has two parameters: an `AuthorizationHandlerContext` and the `TRequirement` you are handling.</span></span> <span data-ttu-id="8eb37-159">MVC 또는 Jabbr 등의 프레임 워크는에 개체를 추가할 수는 `Resource` 속성에는 `AuthorizationHandlerContext` 추가 정보를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-159">Frameworks such as MVC or Jabbr are free to add any object to the `Resource` property on the `AuthorizationHandlerContext` to pass extra information.</span></span>

<span data-ttu-id="8eb37-160">MVC의 인스턴스를 전달 하는 예를 들어 [AuthorizationFilterContext](/dotnet/api/?term=AuthorizationFilterContext) 에 `Resource` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-160">For example, MVC passes an instance of [AuthorizationFilterContext](/dotnet/api/?term=AuthorizationFilterContext) in the `Resource` property.</span></span> <span data-ttu-id="8eb37-161">이 속성에 대 한 액세스를 제공 `HttpContext`, `RouteData`, 그리고 다른 MVC 및 Razor 페이지에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-161">This property provides access to `HttpContext`, `RouteData`, and everything else provided by MVC and Razor Pages.</span></span>

<span data-ttu-id="8eb37-162">사용 하 여 `Resource` 속성은 특정 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-162">The use of the `Resource` property is framework specific.</span></span> <span data-ttu-id="8eb37-163">정보를 사용 하는 `Resource` 속성 권한 부여 정책을 특정 프레임 워크를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8eb37-163">Using information in the `Resource` property limits your authorization policies to particular frameworks.</span></span> <span data-ttu-id="8eb37-164">캐스팅 해야는 `Resource` 사용 하 여 속성은 `as` 키워드를 선택한 다음 해당 캐스트의 코드 충돌 하지 않습니다 확인에 성공 했습니다 확인으로 `InvalidCastException` 다른 프레임 워크에서 실행할 때:</span><span class="sxs-lookup"><span data-stu-id="8eb37-164">You should cast the `Resource` property using the `as` keyword, and then confirm the cast has succeed to ensure your code doesn't crash with an `InvalidCastException` when run on other frameworks:</span></span>

```csharp
// Requires the following import:
//     using Microsoft.AspNetCore.Mvc.Filters;
if (context.Resource is AuthorizationFilterContext mvcContext)
{
    // Examine MVC-specific things like routing data.
}
```
