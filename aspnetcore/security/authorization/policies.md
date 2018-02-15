---
title: "ASP.NET Core에서 정책 기반 권한 부여"
author: rick-anderson
description: "만들고 ASP.NET Core 응용 프로그램에서 권한 부여 요구 사항을 적용 하기 위한 권한 부여 정책 처리기를 사용 하는 방법을 알아봅니다."
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 11/21/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authorization/policies
ms.openlocfilehash: a9ee7e6fd06fa88485d7f578a9df74cbf87d9540
ms.sourcegitcommit: 7ee6e7582421195cbd675355c970d3d292ee668d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/14/2018
---
# <a name="policy-based-authorization"></a><span data-ttu-id="6e8ee-103">정책 기반 권한 부여</span><span class="sxs-lookup"><span data-stu-id="6e8ee-103">Policy-based authorization</span></span>

<span data-ttu-id="6e8ee-104">내부적 [역할 기반 권한 부여](xref:security/authorization/roles) 및 [클레임 기반 권한 부여](xref:security/authorization/claims) 요구, 요구 사항 처리기 및 미리 구성 된 정책을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-104">Underneath the covers, [role-based authorization](xref:security/authorization/roles) and [claims-based authorization](xref:security/authorization/claims) use a requirement, a requirement handler, and a pre-configured policy.</span></span> <span data-ttu-id="6e8ee-105">이러한 빌딩 블록 코드에서 권한 부여 평가 식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-105">These building blocks support the expression of authorization evaluations in code.</span></span> <span data-ttu-id="6e8ee-106">결과 다양 한 재사용 가능한 하 고 테스트 가능 권한 부여 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-106">The result is a richer, reusable, testable authorization structure.</span></span>

<span data-ttu-id="6e8ee-107">권한 부여 정책 하나 이상의 요구 사항으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-107">An authorization policy consists of one or more requirements.</span></span> <span data-ttu-id="6e8ee-108">에 등록 되어 있는 권한 부여 서비스 구성의 일부로 `Startup.ConfigureServices` 메서드:</span><span class="sxs-lookup"><span data-stu-id="6e8ee-108">It's registered as part of the authorization service configuration, in the `Startup.ConfigureServices` method:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Startup.cs?range=40-41,50-55,63,72)]

<span data-ttu-id="6e8ee-109">앞의 예제에서 "AtLeast21" 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-109">In the preceding example, an "AtLeast21" policy is created.</span></span> <span data-ttu-id="6e8ee-110">에 단일 요구 사항이&mdash;의 요구 사항에 대 한 매개 변수로 제공 되는 최소 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-110">It has a single requirement&mdash;that of a minimum age, which is supplied as a parameter to the requirement.</span></span>

<span data-ttu-id="6e8ee-111">사용 하 여 정책이 적용 되는 `[Authorize]` 정책 이름 가진 특성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-111">Policies are applied by using the `[Authorize]` attribute with the policy name.</span></span> <span data-ttu-id="6e8ee-112">예:</span><span class="sxs-lookup"><span data-stu-id="6e8ee-112">For example:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Controllers/AlcoholPurchaseController.cs?name=snippet_AlcoholPurchaseControllerClass&highlight=4)]

## <a name="requirements"></a><span data-ttu-id="6e8ee-113">요구 사항</span><span class="sxs-lookup"><span data-stu-id="6e8ee-113">Requirements</span></span>

<span data-ttu-id="6e8ee-114">권한 부여 요구 사항은 현재 사용자 보안 주체를 평가 하는 정책을 사용할 수 있는 데이터 매개 변수 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-114">An authorization requirement is a collection of data parameters that a policy can use to evaluate the current user principal.</span></span> <span data-ttu-id="6e8ee-115">보호 "AtLeast21" 정책 요구 사항이 단일 매개 변수는&mdash;최소 보존 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-115">In our "AtLeast21" policy, the requirement is a single parameter&mdash;the minimum age.</span></span> <span data-ttu-id="6e8ee-116">요구 사항 구현 [IAuthorizationRequirement](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationrequirement), 빈 표식 인터페이스인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-116">A requirement implements [IAuthorizationRequirement](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationrequirement), which is an empty marker interface.</span></span> <span data-ttu-id="6e8ee-117">매개 변수가 있는 최소 연령 요구 사항 다음과 같이 구현 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-117">A parameterized minimum age requirement could be implemented as follows:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Requirements/MinimumAgeRequirement.cs?name=snippet_MinimumAgeRequirementClass)]

> [!NOTE]
> <span data-ttu-id="6e8ee-118">데이터 또는 속성 요구 사항 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-118">A requirement doesn't need to have data or properties.</span></span>

<a name="security-authorization-policies-based-authorization-handler"></a>

## <a name="authorization-handlers"></a><span data-ttu-id="6e8ee-119">권한 부여 처리기</span><span class="sxs-lookup"><span data-stu-id="6e8ee-119">Authorization handlers</span></span>

<span data-ttu-id="6e8ee-120">권한 부여 처리기는 평가 요구 사항 속성의 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-120">An authorization handler is responsible for the evaluation of a requirement's properties.</span></span> <span data-ttu-id="6e8ee-121">제공 된 작업에 대 한 요구 사항을 평가 하는 권한 부여 처리기 [AuthorizationHandlerContext](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext) 액세스 허용 확인 하려면.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-121">The authorization handler evaluates the requirements against a provided [AuthorizationHandlerContext](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext) to determine if access is allowed.</span></span>

<span data-ttu-id="6e8ee-122">요구 사항이 있을 수 있습니다 [여러 처리기](#security-authorization-policies-based-multiple-handlers)합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-122">A requirement can have [multiple handlers](#security-authorization-policies-based-multiple-handlers).</span></span> <span data-ttu-id="6e8ee-123">처리기를 상속할 수 있습니다 [AuthorizationHandler\<TRequirement >](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandler-1)여기서 `TRequirement` 처리 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-123">A handler may inherit [AuthorizationHandler\<TRequirement>](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandler-1), where `TRequirement` is the requirement to be handled.</span></span> <span data-ttu-id="6e8ee-124">처리기를 구현할 수 있습니다 또는 [IAuthorizationHandler](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationhandler) 요구 사항을 둘 이상의 유형을 처리 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-124">Alternatively, a handler may implement [IAuthorizationHandler](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationhandler) to handle more than one type of requirement.</span></span>

### <a name="use-a-handler-for-one-requirement"></a><span data-ttu-id="6e8ee-125">한 가지 요구 사항에 대 한 처리기를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="6e8ee-125">Use a handler for one requirement</span></span>

<a name="security-authorization-handler-example"></a>

<span data-ttu-id="6e8ee-126">다음은 최소 보존 기간 처리기를 단일 요구 사항을 활용 일대일 관계의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-126">The following is an example of a one-to-one relationship in which a minimum age handler utilizes a single requirement:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/MinimumAgeHandler.cs?name=snippet_MinimumAgeHandlerClass)]

<span data-ttu-id="6e8ee-127">위의 코드에 알려지고 신뢰할 수 있는 발급자가 발급 하는 클레임 생년월일 날짜는 현재 사용자 계정이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-127">The preceding code determines if the current user principal has a date of birth claim which has been issued by a known and trusted Issuer.</span></span> <span data-ttu-id="6e8ee-128">권한 부여 클레임 누락 되었을 때 발생할 수 없습니다, 그리고 완료 된 작업 반환 되는 경우.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-128">Authorization can't occur when the claim is missing, in which case a completed task is returned.</span></span> <span data-ttu-id="6e8ee-129">클레임에 있는 경우 사용자의 나이 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-129">When a claim is present, the user's age is calculated.</span></span> <span data-ttu-id="6e8ee-130">사용자 요구 사항에 정의 된 최소 보존 기간을 충족할 경우 권한 부여를 성공적으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-130">If the user meets the minimum age defined by the requirement, authorization is deemed successful.</span></span> <span data-ttu-id="6e8ee-131">부여 된, `context.Succeed` 유일한 매개 변수로 만족된 요구를 사용 하 여 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-131">When authorization is successful, `context.Succeed` is invoked with the satisfied requirement as its sole parameter.</span></span>

### <a name="use-a-handler-for-multiple-requirements"></a><span data-ttu-id="6e8ee-132">여러 요구 사항에 대 한 처리기를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="6e8ee-132">Use a handler for multiple requirements</span></span>

<span data-ttu-id="6e8ee-133">다음은 사용 권한 처리기는 3 개 요구를 활용 하는 일 대 다 관계의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-133">The following is an example of a one-to-many relationship in which a permission handler utilizes three requirements:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/PermissionHandler.cs?name=snippet_PermissionHandlerClass)]

<span data-ttu-id="6e8ee-134">앞의 코드를 통과 [PendingRequirements](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.pendingrequirements#Microsoft_AspNetCore_Authorization_AuthorizationHandlerContext_PendingRequirements)&mdash;성공으로 표시 되지 않습니다 요구 사항을 포함 하는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-134">The preceding code traverses [PendingRequirements](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.pendingrequirements#Microsoft_AspNetCore_Authorization_AuthorizationHandlerContext_PendingRequirements)&mdash;a property containing requirements not marked as successful.</span></span> <span data-ttu-id="6e8ee-135">사용자에 읽기 권한이 요청 된 리소스에 액세스 하는 소유자 이거나 스폰서 자신이 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-135">If the user has read permission, he or she must be either an owner or a sponsor to access the requested resource.</span></span> <span data-ttu-id="6e8ee-136">사용자가 편집 또는 삭제 권한이, 하는 경우 자신이 요청한 리소스에 액세스 하기 위해 소유자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-136">If the user has edit or delete permission, he or she must be an owner to access the requested resource.</span></span> <span data-ttu-id="6e8ee-137">부여 된, `context.Succeed` 유일한 매개 변수로 만족된 요구를 사용 하 여 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-137">When authorization is successful, `context.Succeed` is invoked with the satisfied requirement as its sole parameter.</span></span>

<a name="security-authorization-policies-based-handler-registration"></a>

### <a name="handler-registration"></a><span data-ttu-id="6e8ee-138">처리기를 등록</span><span class="sxs-lookup"><span data-stu-id="6e8ee-138">Handler registration</span></span>

<span data-ttu-id="6e8ee-139">처리기는 구성 하는 동안 서비스 컬렉션에 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-139">Handlers are registered in the services collection during configuration.</span></span> <span data-ttu-id="6e8ee-140">예:</span><span class="sxs-lookup"><span data-stu-id="6e8ee-140">For example:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Startup.cs?range=40-41,50-55,63-65,72)]

<span data-ttu-id="6e8ee-141">각 처리기가 호출 하 여 서비스 컬렉션에 추가 `services.AddSingleton<IAuthorizationHandler, YourHandlerClass>();`합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-141">Each handler is added to the services collection by invoking `services.AddSingleton<IAuthorizationHandler, YourHandlerClass>();`.</span></span>

## <a name="what-should-a-handler-return"></a><span data-ttu-id="6e8ee-142">처리기를 반환 해야?</span><span class="sxs-lookup"><span data-stu-id="6e8ee-142">What should a handler return?</span></span>

<span data-ttu-id="6e8ee-143">`Handle` 에서 메서드는 [처리기 예제](#security-authorization-handler-example) 아무 값도 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-143">Note that the `Handle` method in the [handler example](#security-authorization-handler-example) returns no value.</span></span> <span data-ttu-id="6e8ee-144">성공 또는 실패를 표시 된 상태는 어떻게 합니까?</span><span class="sxs-lookup"><span data-stu-id="6e8ee-144">How is a status of either success or failure indicated?</span></span>

* <span data-ttu-id="6e8ee-145">처리기를 호출 하 여이 성공 했음을 의미 `context.Succeed(IAuthorizationRequirement requirement)`, 된 요구 사항을 전달 성공적으로 확인 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-145">A handler indicates success by calling `context.Succeed(IAuthorizationRequirement requirement)`, passing the requirement that has been successfully validated.</span></span>

* <span data-ttu-id="6e8ee-146">처리기를 배포할 수 있습니다. 동일한 요구 사항에 대해 다른 처리기 처럼 일반적으로 오류를 처리할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-146">A handler doesn't need to handle failures generally, as other handlers for the same requirement may succeed.</span></span>

* <span data-ttu-id="6e8ee-147">오류, 다른 요구 사항을 처리기 성공 하는 경우에, 호출 `context.Fail`합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-147">To guarantee failure, even if other requirement handlers succeed, call `context.Fail`.</span></span>

<span data-ttu-id="6e8ee-148">로 설정 하면 `false`, [InvokeHandlersAfterFailure](/dotnet/api/microsoft.aspnetcore.authorization.authorizationoptions.invokehandlersafterfailure#Microsoft_AspNetCore_Authorization_AuthorizationOptions_InvokeHandlersAfterFailure) 속성 (ASP.NET Core 1.1의 사용 가능 하 고 이후) 처리기가 실행 short-circuits 때 `context.Fail` 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-148">When set to `false`, the [InvokeHandlersAfterFailure](/dotnet/api/microsoft.aspnetcore.authorization.authorizationoptions.invokehandlersafterfailure#Microsoft_AspNetCore_Authorization_AuthorizationOptions_InvokeHandlersAfterFailure) property (available in ASP.NET Core 1.1 and later) short-circuits the execution of handlers when `context.Fail` is called.</span></span> <span data-ttu-id="6e8ee-149">`InvokeHandlersAfterFailure` 기본적으로 `true`,이 경우 모든 처리기가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-149">`InvokeHandlersAfterFailure` defaults to `true`, in which case all handlers are called.</span></span> <span data-ttu-id="6e8ee-150">이렇게 하면 항상 실행 되는 로깅, 같은 파생 작업이 생성 하기 위한 요구 사항은 경우에 `context.Fail` 다른 처리기에서 호출 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-150">This allows requirements to produce side effects, such as logging, which always take place even if `context.Fail` has been called in another handler.</span></span>

<a name="security-authorization-policies-based-multiple-handlers"></a>

## <a name="why-would-i-want-multiple-handlers-for-a-requirement"></a><span data-ttu-id="6e8ee-151">이유는 여러 처리기는 요구 사항에 대 한?</span><span class="sxs-lookup"><span data-stu-id="6e8ee-151">Why would I want multiple handlers for a requirement?</span></span>

<span data-ttu-id="6e8ee-152">에 있는 것으로 평가 하려는 경우에는 **또는** 별로 단일 요구 사항에 대해 여러 처리기를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-152">In cases where you want evaluation to be on an **OR** basis, implement multiple handlers for a single requirement.</span></span> <span data-ttu-id="6e8ee-153">예를 들어 Microsoft는 주요 카드를 사용 하는 열만 있는 문.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-153">For example, Microsoft has doors which only open with key cards.</span></span> <span data-ttu-id="6e8ee-154">키 카드를 집에 두면 접수원 임시 스티커 인쇄 하 고 사용자에 대 한 문을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-154">If you leave your key card at home, the receptionist prints a temporary sticker and opens the door for you.</span></span> <span data-ttu-id="6e8ee-155">이 시나리오에서는 단일 요구 사항, 갖기 *BuildingEntry*, 하지만 단일 요구 사항 검사 하나씩 여러 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-155">In this scenario, you'd have a single requirement, *BuildingEntry*, but multiple handlers, each one examining a single requirement.</span></span>

<span data-ttu-id="6e8ee-156">*BuildingEntryRequirement.cs*</span><span class="sxs-lookup"><span data-stu-id="6e8ee-156">*BuildingEntryRequirement.cs*</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Requirements/BuildingEntryRequirement.cs?name=snippet_BuildingEntryRequirementClass)]

<span data-ttu-id="6e8ee-157">*BadgeEntryHandler.cs*</span><span class="sxs-lookup"><span data-stu-id="6e8ee-157">*BadgeEntryHandler.cs*</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/BadgeEntryHandler.cs?name=snippet_BadgeEntryHandlerClass)]

<span data-ttu-id="6e8ee-158">*TemporaryStickerHandler.cs*</span><span class="sxs-lookup"><span data-stu-id="6e8ee-158">*TemporaryStickerHandler.cs*</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/TemporaryStickerHandler.cs?name=snippet_TemporaryStickerHandlerClass)]

<span data-ttu-id="6e8ee-159">이 두 처리기 되는지 확인 [등록](xref:security/authorization/policies#security-authorization-policies-based-handler-registration)합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-159">Ensure that both handlers are [registered](xref:security/authorization/policies#security-authorization-policies-based-handler-registration).</span></span> <span data-ttu-id="6e8ee-160">어느 처리기 성공 때 정책을 평가 `BuildingEntryRequirement`, 정책 평가 성공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-160">If either handler succeeds when a policy evaluates the `BuildingEntryRequirement`, the policy evaluation succeeds.</span></span>

## <a name="using-a-func-to-fulfill-a-policy"></a><span data-ttu-id="6e8ee-161">Func는 정책을 처리 하는 데 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="6e8ee-161">Using a func to fulfill a policy</span></span>

<span data-ttu-id="6e8ee-162">정책을 코드에서 표현 하기 간단 따르는 데는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-162">There may be situations in which fulfilling a policy is simple to express in code.</span></span> <span data-ttu-id="6e8ee-163">제공 하는 것이 불가능 한 `Func<AuthorizationHandlerContext, bool>` 와 정책을 구성할 때는 `RequireAssertion` 정책 작성기.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-163">It's possible to supply a `Func<AuthorizationHandlerContext, bool>` when configuring your policy with the `RequireAssertion` policy builder.</span></span>

<span data-ttu-id="6e8ee-164">예를 들어 이전 `BadgeEntryHandler` 다음과 같이 다시 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-164">For example, the previous `BadgeEntryHandler` could be rewritten as follows:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Startup.cs?range=52-53,57-63)]

## <a name="accessing-mvc-request-context-in-handlers"></a><span data-ttu-id="6e8ee-165">처리기에서 MVC 요청 컨텍스트 액세스</span><span class="sxs-lookup"><span data-stu-id="6e8ee-165">Accessing MVC request context in handlers</span></span>

<span data-ttu-id="6e8ee-166">`HandleRequirementAsync` 권한 부여 처리기에서 구현 하는 메서드에 두 개의 매개 변수가:는 `AuthorizationHandlerContext` 및 `TRequirement` 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-166">The `HandleRequirementAsync` method you implement in an authorization handler has two parameters: an `AuthorizationHandlerContext` and the `TRequirement` you are handling.</span></span> <span data-ttu-id="6e8ee-167">MVC 또는 Jabbr 등의 프레임 워크는에 개체를 추가할 수는 `Resource` 속성에는 `AuthorizationHandlerContext` 추가 정보를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-167">Frameworks such as MVC or Jabbr are free to add any object to the `Resource` property on the `AuthorizationHandlerContext` to pass extra information.</span></span>

<span data-ttu-id="6e8ee-168">MVC의 인스턴스를 전달 하는 예를 들어 [AuthorizationFilterContext](/dotnet/api/?term=AuthorizationFilterContext) 에 `Resource` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-168">For example, MVC passes an instance of [AuthorizationFilterContext](/dotnet/api/?term=AuthorizationFilterContext) in the `Resource` property.</span></span> <span data-ttu-id="6e8ee-169">이 속성에 대 한 액세스를 제공 `HttpContext`, `RouteData`, 그리고 다른 MVC 및 Razor 페이지에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-169">This property provides access to `HttpContext`, `RouteData`, and everything else provided by MVC and Razor Pages.</span></span>

<span data-ttu-id="6e8ee-170">사용 하 여 `Resource` 속성은 특정 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-170">The use of the `Resource` property is framework specific.</span></span> <span data-ttu-id="6e8ee-171">정보를 사용 하는 `Resource` 속성 권한 부여 정책을 특정 프레임 워크를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e8ee-171">Using information in the `Resource` property limits your authorization policies to particular frameworks.</span></span> <span data-ttu-id="6e8ee-172">캐스팅 해야는 `Resource` 사용 하 여 속성은 `as` 키워드를 선택한 다음 해당 캐스트의 코드 충돌 하지 않습니다 확인에 성공 했습니다 확인으로 `InvalidCastException` 다른 프레임 워크에서 실행할 때:</span><span class="sxs-lookup"><span data-stu-id="6e8ee-172">You should cast the `Resource` property using the `as` keyword, and then confirm the cast has succeed to ensure your code doesn't crash with an `InvalidCastException` when run on other frameworks:</span></span>

```csharp
// Requires the following import:
//     using Microsoft.AspNetCore.Mvc.Filters;
if (context.Resource is AuthorizationFilterContext mvcContext)
{
    // Examine MVC-specific things like routing data.
}
```
