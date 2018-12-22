---
title: ASP.NET Core의 정책 기반 권한 부여
author: rick-anderson
description: ASP.NET Core 응용 프로그램에서 사용자 지정 권한 정책 처리기를 작성 및 사용해서 권한 부여 요구 사항을 적용하는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 11/21/2017
uid: security/authorization/policies
ms.openlocfilehash: 81ca6ad9ddba3de094762f5608bb6a5719bca7a1
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36277984"
---
# <a name="policy-based-authorization-in-aspnet-core"></a><span data-ttu-id="30526-103">ASP.NET Core의 정책 기반 권한 부여</span><span class="sxs-lookup"><span data-stu-id="30526-103">Policy-based authorization in ASP.NET Core</span></span>

<span data-ttu-id="30526-104">[역할 기반 권한 부여](xref:security/authorization/roles) 및 [클레임 기반 권한 부여](xref:security/authorization/claims) 는 내부적으로 요구 사항, 요구 사항 처리기, 그리고 미리 구성된 정책을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="30526-104">Underneath the covers, [role-based authorization](xref:security/authorization/roles) and [claims-based authorization](xref:security/authorization/claims) use a requirement, a requirement handler, and a pre-configured policy.</span></span> <span data-ttu-id="30526-105">이런 빌딩 블록들은 권한 부여 평가를 코드로 표현할 수 있는 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="30526-105">These building blocks support the expression of authorization evaluations in code.</span></span> <span data-ttu-id="30526-106">결과적으로 보다 풍부하고 재사용 가능하며 테스트 가능한 권한 부여 구조를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30526-106">The result is a richer, reusable, testable authorization structure.</span></span>

<span data-ttu-id="30526-107">권한 부여 정책은 하나 이상의 요구 사항으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="30526-107">An authorization policy consists of one or more requirements.</span></span> <span data-ttu-id="30526-108">그리고 `Startup.ConfigureServices`에서 권한 부여 서비스 구성의 일부로 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="30526-108">It's registered as part of the authorization service configuration, in the `Startup.ConfigureServices` method:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Startup.cs?range=40-41,50-55,63,72)]

<span data-ttu-id="30526-109">위의 예제는 "AtLeast21"이라는 정책을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="30526-109">In the preceding example, an "AtLeast21" policy is created.</span></span> <span data-ttu-id="30526-110">이 정책은 요구 사항의 &mdash; 매개 변수로 제공되는, 최소 연령을 뜻하는 단일 요구 사항을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="30526-110">It has a single requirement&mdash;that of a minimum age, which is supplied as a parameter to the requirement.</span></span>

<span data-ttu-id="30526-111">정책은 정책 이름이 지정된 `[Authorize]` 특성을 통해서 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="30526-111">Policies are applied by using the `[Authorize]` attribute with the policy name.</span></span> <span data-ttu-id="30526-112">예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="30526-112">For example:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Controllers/AlcoholPurchaseController.cs?name=snippet_AlcoholPurchaseControllerClass&highlight=4)]

## <a name="requirements"></a><span data-ttu-id="30526-113">요구 사항</span><span class="sxs-lookup"><span data-stu-id="30526-113">Requirements</span></span>

<span data-ttu-id="30526-114">권한 부여 요구 사항은 현재 사용자 보안 주체를 평가 하는 정책을 사용할 수 있는 데이터 매개 변수 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="30526-114">An authorization requirement is a collection of data parameters that a policy can use to evaluate the current user principal.</span></span> <span data-ttu-id="30526-115">보호 "AtLeast21" 정책 요구 사항이 단일 매개 변수는&mdash;최소 보존 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="30526-115">In our "AtLeast21" policy, the requirement is a single parameter&mdash;the minimum age.</span></span> <span data-ttu-id="30526-116">요구 사항 구현 [IAuthorizationRequirement](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationrequirement), 빈 표식 인터페이스인 합니다.</span><span class="sxs-lookup"><span data-stu-id="30526-116">A requirement implements [IAuthorizationRequirement](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationrequirement), which is an empty marker interface.</span></span> <span data-ttu-id="30526-117">매개 변수가 있는 최소 연령 요구 사항 다음과 같이 구현 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="30526-117">A parameterized minimum age requirement could be implemented as follows:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Requirements/MinimumAgeRequirement.cs?name=snippet_MinimumAgeRequirementClass)]

> [!NOTE]
> <span data-ttu-id="30526-118">요구 사항이 데이터나 속성을 가져야 할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="30526-118">A requirement doesn't need to have data or properties.</span></span>

<a name="security-authorization-policies-based-authorization-handler"></a>

## <a name="authorization-handlers"></a><span data-ttu-id="30526-119">권한 부여 처리기</span><span class="sxs-lookup"><span data-stu-id="30526-119">Authorization handlers</span></span>

<span data-ttu-id="30526-120">권한 부여 처리기는 요구 사항의 속성을 평가하는 역할을 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="30526-120">An authorization handler is responsible for the evaluation of a requirement's properties.</span></span> <span data-ttu-id="30526-121">권한 부여 처리기는 제공된 [AuthorizationHandlerContext](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext)에 대해 요구 사항을 평가하여 접근 허용 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="30526-121">The authorization handler evaluates the requirements against a provided [AuthorizationHandlerContext](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext) to determine if access is allowed.</span></span>

<span data-ttu-id="30526-122">하나의 요구 사항에 [여러 개의 처리기](#security-authorization-policies-based-multiple-handlers) 가 존재할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30526-122">A requirement can have [multiple handlers](#security-authorization-policies-based-multiple-handlers).</span></span> <span data-ttu-id="30526-123">처리기는 [AuthorizationHandler\<TRequirement>](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandler-1)를 상속받으며, 여기서 `TRequirement` 는 처리해야 할 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="30526-123">A handler may inherit [AuthorizationHandler\<TRequirement>](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandler-1), where `TRequirement` is the requirement to be handled.</span></span> <span data-ttu-id="30526-124">처리기를 구현할 수 있습니다 또는 [IAuthorizationHandler](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationhandler) 요구 사항을 둘 이상의 유형을 처리 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="30526-124">Alternatively, a handler may implement [IAuthorizationHandler](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationhandler) to handle more than one type of requirement.</span></span>

### <a name="use-a-handler-for-one-requirement"></a><span data-ttu-id="30526-125">한 가지 요구 사항에 대한 처리기 사용하기</span><span class="sxs-lookup"><span data-stu-id="30526-125">Use a handler for one requirement</span></span>

<a name="security-authorization-handler-example"></a>

<span data-ttu-id="30526-126">다음은 최소 연령 처리기에서 단일 요구 사항을 사용하는 일대일 관계의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="30526-126">The following is an example of a one-to-one relationship in which a minimum age handler utilizes a single requirement:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/MinimumAgeHandler.cs?name=snippet_MinimumAgeHandlerClass)]

<span data-ttu-id="30526-127">이 코드는 먼저 현재 사용자의 신원이 우리가 알고 있고 신뢰할 수 있는 발급자로부터 발급된 생년월일 클레임을 갖고 있는지부터 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="30526-127">The preceding code determines if the current user principal has a date of birth claim which has been issued by a known and trusted Issuer.</span></span> <span data-ttu-id="30526-128">만약 클레임이 누락되었다면 권한을 부여할 수 없으므로 완료된 작업이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="30526-128">Authorization can't occur when the claim is missing, in which case a completed task is returned.</span></span> <span data-ttu-id="30526-129">반면 클레임이 존재할 경우, 사용자의 나이가 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="30526-129">When a claim is present, the user's age is calculated.</span></span> <span data-ttu-id="30526-130">그리고 나이가 요구 사항에 의해 정의된 최소 연령을 만족할 경우 권한 부여가 성공한 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="30526-130">If the user meets the minimum age defined by the requirement, authorization is deemed successful.</span></span> <span data-ttu-id="30526-131">권한 부여에 성공하면 만족한 요구 사항을 매개 변수로 전달해서 `context.Succeed` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="30526-131">When authorization is successful, `context.Succeed` is invoked with the satisfied requirement as its sole parameter.</span></span>

### <a name="use-a-handler-for-multiple-requirements"></a><span data-ttu-id="30526-132">여러 요구 사항에 대한 처리기 사용하기</span><span class="sxs-lookup"><span data-stu-id="30526-132">Use a handler for multiple requirements</span></span>

<span data-ttu-id="30526-133">다음은 권한 처리기가 세 가지 요구 사항을 사용하는 일대다 관계의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="30526-133">The following is an example of a one-to-many relationship in which a permission handler utilizes three requirements:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/PermissionHandler.cs?name=snippet_PermissionHandlerClass)]

<span data-ttu-id="30526-134">앞의 코드를 통과 [PendingRequirements](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.pendingrequirements#Microsoft_AspNetCore_Authorization_AuthorizationHandlerContext_PendingRequirements)&mdash;성공으로 표시 되지 않습니다 요구 사항을 포함 하는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="30526-134">The preceding code traverses [PendingRequirements](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.pendingrequirements#Microsoft_AspNetCore_Authorization_AuthorizationHandlerContext_PendingRequirements)&mdash;a property containing requirements not marked as successful.</span></span> <span data-ttu-id="30526-135">사용자에 읽기 권한이 요청 된 리소스에 액세스 하는 소유자 이거나 스폰서 자신이 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30526-135">If the user has read permission, he or she must be either an owner or a sponsor to access the requested resource.</span></span> <span data-ttu-id="30526-136">사용자가 편집 또는 삭제 권한이, 하는 경우 자신이 요청한 리소스에 액세스 하기 위해 소유자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30526-136">If the user has edit or delete permission, he or she must be an owner to access the requested resource.</span></span> <span data-ttu-id="30526-137">권한 부여에 성공하면 만족한 요구 사항을 매개 변수로 전달해서 `context.Succeed` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="30526-137">When authorization is successful, `context.Succeed` is invoked with the satisfied requirement as its sole parameter.</span></span>

<a name="security-authorization-policies-based-handler-registration"></a>

### <a name="handler-registration"></a><span data-ttu-id="30526-138">처리기 등록하기</span><span class="sxs-lookup"><span data-stu-id="30526-138">Handler registration</span></span>

<span data-ttu-id="30526-139">처리기는 구성 과정 중 서비스 컬렉션에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="30526-139">Handlers are registered in the services collection during configuration.</span></span> <span data-ttu-id="30526-140">예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="30526-140">For example:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Startup.cs?range=40-41,50-55,63-65,72)]

<span data-ttu-id="30526-141">각 처리기는 `services.AddSingleton<IAuthorizationHandler, YourHandlerClass>();` 호출을 통해서 서비스 컬렉션에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="30526-141">Each handler is added to the services collection by invoking `services.AddSingleton<IAuthorizationHandler, YourHandlerClass>();`.</span></span>

## <a name="what-should-a-handler-return"></a><span data-ttu-id="30526-142">처리기가 반환해야 하는 결과는?</span><span class="sxs-lookup"><span data-stu-id="30526-142">What should a handler return?</span></span>

<span data-ttu-id="30526-143">본문의 [처리기 예제](#security-authorization-handler-example)에서 `Handle` 메서드가 아무런 값도 반환하지 않는다는 점에 주목하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="30526-143">Note that the `Handle` method in the [handler example](#security-authorization-handler-example) returns no value.</span></span> <span data-ttu-id="30526-144">그렇다면 성공 혹은 실패 여부는 어떻게 확인할 수 있을까요?</span><span class="sxs-lookup"><span data-stu-id="30526-144">How is a status of either success or failure indicated?</span></span>

* <span data-ttu-id="30526-145">처리기는 성공적으로 검증된 요구 사항을 `context.Succeed(IAuthorizationRequirement requirement)`에 매개 변수로 전달하여 호출함으로써 성공했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="30526-145">A handler indicates success by calling `context.Succeed(IAuthorizationRequirement requirement)`, passing the requirement that has been successfully validated.</span></span>

* <span data-ttu-id="30526-146">일반적으로 처리기는 실패를 처리할 필요가 없는데, 동일한 요구 사항에 대한 다른 처리기가 성공할 수도 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="30526-146">A handler doesn't need to handle failures generally, as other handlers for the same requirement may succeed.</span></span>

* <span data-ttu-id="30526-147">다른 처리기의 성공 여부와 관계없이 무조건 실패한 것으로 나타내려면 `context.Fail`을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="30526-147">To guarantee failure, even if other requirement handlers succeed, call `context.Fail`.</span></span>

<span data-ttu-id="30526-148">로 설정 하면 `false`, [InvokeHandlersAfterFailure](/dotnet/api/microsoft.aspnetcore.authorization.authorizationoptions.invokehandlersafterfailure#Microsoft_AspNetCore_Authorization_AuthorizationOptions_InvokeHandlersAfterFailure) 속성 (ASP.NET Core 1.1의 사용 가능 하 고 이후) 처리기가 실행 short-circuits 때 `context.Fail` 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="30526-148">When set to `false`, the [InvokeHandlersAfterFailure](/dotnet/api/microsoft.aspnetcore.authorization.authorizationoptions.invokehandlersafterfailure#Microsoft_AspNetCore_Authorization_AuthorizationOptions_InvokeHandlersAfterFailure) property (available in ASP.NET Core 1.1 and later) short-circuits the execution of handlers when `context.Fail` is called.</span></span> <span data-ttu-id="30526-149">`InvokeHandlersAfterFailure` 기본적으로 `true`,이 경우 모든 처리기가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30526-149">`InvokeHandlersAfterFailure` defaults to `true`, in which case all handlers are called.</span></span> <span data-ttu-id="30526-150">이렇게 하면 항상 실행 되는 로깅, 같은 파생 작업이 생성 하기 위한 요구 사항은 경우에 `context.Fail` 다른 처리기에서 호출 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="30526-150">This allows requirements to produce side effects, such as logging, which always take place even if `context.Fail` has been called in another handler.</span></span>

<a name="security-authorization-policies-based-multiple-handlers"></a>

## <a name="why-would-i-want-multiple-handlers-for-a-requirement"></a><span data-ttu-id="30526-151">요구 사항에 대해 여러 개의 처기리가 필요한 이유는?</span><span class="sxs-lookup"><span data-stu-id="30526-151">Why would I want multiple handlers for a requirement?</span></span>

<span data-ttu-id="30526-152">만약 **OR** 기반의 평가를 수행하고 싶다면 단일 요구 사항에 대해 여러 개의 처리기를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30526-152">In cases where you want evaluation to be on an **OR** basis, implement multiple handlers for a single requirement.</span></span> <span data-ttu-id="30526-153">예를 들어, Microsoft에는 키 카드로만 열 수 있는 문이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30526-153">For example, Microsoft has doors which only open with key cards.</span></span> <span data-ttu-id="30526-154">만약 키 카드를 집에 두고 왔다면 접수원이 임시 스티커를 인쇄하고 대신 문을 열어줍니다.</span><span class="sxs-lookup"><span data-stu-id="30526-154">If you leave your key card at home, the receptionist prints a temporary sticker and opens the door for you.</span></span> <span data-ttu-id="30526-155">이 시나리오의 경우, 요구 사항은 *BuildingEntry* 하나지만 여러 처리기가 단일 요구 사항을 각각 개별적으로 검토하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30526-155">In this scenario, you'd have a single requirement, *BuildingEntry*, but multiple handlers, each one examining a single requirement.</span></span>

<span data-ttu-id="30526-156">*BuildingEntryRequirement.cs*</span><span class="sxs-lookup"><span data-stu-id="30526-156">*BuildingEntryRequirement.cs*</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Requirements/BuildingEntryRequirement.cs?name=snippet_BuildingEntryRequirementClass)]

<span data-ttu-id="30526-157">*BadgeEntryHandler.cs*</span><span class="sxs-lookup"><span data-stu-id="30526-157">*BadgeEntryHandler.cs*</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/BadgeEntryHandler.cs?name=snippet_BadgeEntryHandlerClass)]

<span data-ttu-id="30526-158">*TemporaryStickerHandler.cs*</span><span class="sxs-lookup"><span data-stu-id="30526-158">*TemporaryStickerHandler.cs*</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Services/Handlers/TemporaryStickerHandler.cs?name=snippet_TemporaryStickerHandlerClass)]

<span data-ttu-id="30526-159">두 처리기가 모두 [등록되어 있는지](xref:security/authorization/policies#security-authorization-policies-based-handler-registration) 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="30526-159">Ensure that both handlers are [registered](xref:security/authorization/policies#security-authorization-policies-based-handler-registration).</span></span> <span data-ttu-id="30526-160">정책이 `BuildingEntryRequirement` 를 평가할 때, 두 처리기 중 하나라도 성공하면 정책 평가가 성공한 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="30526-160">If either handler succeeds when a policy evaluates the `BuildingEntryRequirement`, the policy evaluation succeeds.</span></span>

## <a name="using-a-func-to-fulfill-a-policy"></a><span data-ttu-id="30526-161">func를 이용해서 정책 구성하기</span><span class="sxs-lookup"><span data-stu-id="30526-161">Using a func to fulfill a policy</span></span>

<span data-ttu-id="30526-162">코드로 정책을 표현해서 구성하는 편이 더 간단한 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30526-162">There may be situations in which fulfilling a policy is simple to express in code.</span></span> <span data-ttu-id="30526-163">정책을 구성할 때 `RequireAssertion` 정책 빌더에 `Func<AuthorizationHandlerContext, bool>`을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30526-163">It's possible to supply a `Func<AuthorizationHandlerContext, bool>` when configuring your policy with the `RequireAssertion` policy builder.</span></span>

<span data-ttu-id="30526-164">예를 들어 이전 `BadgeEntryHandler`를 다음과 같이 다시 작성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30526-164">For example, the previous `BadgeEntryHandler` could be rewritten as follows:</span></span>

[!code-csharp[](policies/samples/PoliciesAuthApp1/Startup.cs?range=52-53,57-63)]

## <a name="accessing-mvc-request-context-in-handlers"></a><span data-ttu-id="30526-165">처리기에서 MVC 요청 컨텍스트 접근하기</span><span class="sxs-lookup"><span data-stu-id="30526-165">Accessing MVC request context in handlers</span></span>

<span data-ttu-id="30526-166">권한 부여 처리기에서 구현해야 하는 `HandleRequirementAsync` 메서드에는 `AuthorizationHandlerContext`와 처리해야 할 대상인 `TRequirement`라는 두 개의 매개 변수가 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="30526-166">The `HandleRequirementAsync` method you implement in an authorization handler has two parameters: an `AuthorizationHandlerContext` and the `TRequirement` you are handling.</span></span> <span data-ttu-id="30526-167">MVC나 Jabbr 같은 프레임워크는 `AuthorizationHandlerContext`의 `Resource` 속성에 자유롭게 개체를 추가해서 추가적인 정보를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30526-167">Frameworks such as MVC or Jabbr are free to add any object to the `Resource` property on the `AuthorizationHandlerContext` to pass extra information.</span></span>

<span data-ttu-id="30526-168">예를 들어, MVC는 `Resource` 속성에 [AuthorizationFilterContext](/dotnet/api/?term=AuthorizationFilterContext)의 인스턴스를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="30526-168">For example, MVC passes an instance of [AuthorizationFilterContext](/dotnet/api/?term=AuthorizationFilterContext) in the `Resource` property.</span></span> <span data-ttu-id="30526-169">이 속성은 `HttpContext`나 `RouteData`를 비롯한, MVC 및 Razor 페이지가 제공하는 다양한 정보들에 대한 접근을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30526-169">This property provides access to `HttpContext`, `RouteData`, and everything else provided by MVC and Razor Pages.</span></span>

<span data-ttu-id="30526-170">`Resource` 속성을 사용하는 방식은 프레임워크에 따라서 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="30526-170">The use of the `Resource` property is framework specific.</span></span> <span data-ttu-id="30526-171">따라서 `Resource` 속성의 정보를 사용할 경우 권한 부여 정책이 특정 프레임워크를 대상으로 제한될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30526-171">Using information in the `Resource` property limits your authorization policies to particular frameworks.</span></span> <span data-ttu-id="30526-172">그러므로 먼저 `as` 키워드를 사용해서 `Resource` 속성의 캐스팅을 시도한 다음, 캐스팅의 성공 여부를 확인해서 처리기가 다른 프레임워크에서 실행될 때 `InvalidCastException` 예외가 발생하지 않도록 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30526-172">You should cast the `Resource` property using the `as` keyword, and then confirm the cast has succeed to ensure your code doesn't crash with an `InvalidCastException` when run on other frameworks:</span></span>

```csharp
// Requires the following import:
//     using Microsoft.AspNetCore.Mvc.Filters;
if (context.Resource is AuthorizationFilterContext mvcContext)
{
    // Examine MVC-specific things like routing data.
}
```
