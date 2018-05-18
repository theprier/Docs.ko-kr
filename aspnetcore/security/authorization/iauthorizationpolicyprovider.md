---
title: ASP.NET Core의 사용자 지정 권한 부여 정책 공급자
author: mjrousos
description: ASP.NET Core 응용 프로그램의 사용자 지정 IAuthorizationPolicyProvider를 사용 하 여 권한 부여 정책을 동적으로 생성 하는 방법에 알아봅니다.
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 05/02/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authorization/iauthorizationpolicyprovider
ms.openlocfilehash: a5bad88b37d38b819b960b1eb27808d891268c01
ms.sourcegitcommit: a66f38071e13685bbe59d48d22aa141ac702b432
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/17/2018
---
# <a name="custom-authorization-policy-providers-using-iauthorizationpolicyprovider-in-aspnet-core"></a><span data-ttu-id="79494-103">ASP.NET Core에서 IAuthorizationPolicyProvider를 사용 하 여 사용자 지정 권한 부여 정책 공급자</span><span class="sxs-lookup"><span data-stu-id="79494-103">Custom Authorization Policy Providers using IAuthorizationPolicyProvider in ASP.NET Core</span></span> 

<span data-ttu-id="79494-104">으로 [Mike Rousos](https://github.com/mjrousos)</span><span class="sxs-lookup"><span data-stu-id="79494-104">By [Mike Rousos](https://github.com/mjrousos)</span></span>

<span data-ttu-id="79494-105">일반적으로 사용 하는 경우 [권한 부여 정책 기반](xref:security/authorization/policies), 정책을 호출 하 여 등록 된 `AuthorizationOptions.AddPolicy` 권한 부여 서비스 구성의 일부분으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="79494-105">Typically when using [policy-based authorization](xref:security/authorization/policies), policies are registered by calling `AuthorizationOptions.AddPolicy` as part of authorization service configuration.</span></span> <span data-ttu-id="79494-106">일부 시나리오에서는 아닐 수 (없거나 에이전트 설치가 바람직하지)를 이러한 방식으로 권한 부여 정책을 모두 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="79494-106">In some scenarios, it may not be possible (or desirable) to register all authorization policies in this way.</span></span> <span data-ttu-id="79494-107">이러한 경우에는 사용자 지정을 사용할 수 있습니다 `IAuthorizationPolicyProvider` 권한 부여 정책을 제공 하는 방법을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79494-107">In those cases, you can use a custom `IAuthorizationPolicyProvider` to control how authorization policies are supplied.</span></span>

<span data-ttu-id="79494-108">시나리오의 예제를 사용자 지정 [IAuthorizationPolicyProvider](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationpolicyprovider) 유용할 수 포함:</span><span class="sxs-lookup"><span data-stu-id="79494-108">Examples of scenarios where a custom [IAuthorizationPolicyProvider](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationpolicyprovider) may be useful include:</span></span>

* <span data-ttu-id="79494-109">외부 서비스를 사용 하 여 정책 평가 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="79494-109">Using an external service to provide policy evaluation.</span></span>
* <span data-ttu-id="79494-110">정책의 큰 범위를 사용 하 여 (다른 방 번호 또는 예: 연령)에, 따라서은 바람직하지 않습니다 각 개별 인증 정책으로 추가 하는 `AuthorizationOptions.AddPolicy` 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="79494-110">Using a large range of policies (for different room numbers or ages, for example), so it doesn’t make sense to add each individual authorization policy with an `AuthorizationOptions.AddPolicy` call.</span></span>
* <span data-ttu-id="79494-111">외부 데이터 원본 (예: 데이터베이스)의 정보에 따라 런타임에 정책 만들기 또는 다른 메커니즘을 통해 권한 부여 요구 사항을 동적으로 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="79494-111">Creating policies at runtime based on information in an external data source (like a database) or determining authorization requirements dynamically through another mechanism.</span></span>

## <a name="customizing-policy-retrieval"></a><span data-ttu-id="79494-112">정책 검색을 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="79494-112">Customizing policy retrieval</span></span>

<span data-ttu-id="79494-113">ASP.NET Core 응용 프로그램의 구현을 사용는 `IAuthorizationPolicyProvider` 권한 부여 정책을 검색 하는 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="79494-113">ASP.NET Core apps use an implementation of the `IAuthorizationPolicyProvider` interface to retrieve authorization policies.</span></span> <span data-ttu-id="79494-114">기본적으로 [DefaultAuthorizationPolicyProvider](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.authorization.defaultauthorizationpolicyprovider) 등록 되 고 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="79494-114">By default, [DefaultAuthorizationPolicyProvider](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.authorization.defaultauthorizationpolicyprovider) is registered and used.</span></span> <span data-ttu-id="79494-115">`DefaultAuthorizationPolicyProvider` 정책을 반환는 `AuthorizationOptions` 에서 제공 되는 `IServiceCollection.AddAuthorization` 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="79494-115">`DefaultAuthorizationPolicyProvider` returns policies from the `AuthorizationOptions` provided in an `IServiceCollection.AddAuthorization` call.</span></span>

<span data-ttu-id="79494-116">다른 등록 하 여이 동작을 사용자 지정할 수 있습니다 `IAuthorizationPolicyProvider` 응용 프로그램의 구현이 [종속성 주입](xref:fundamentals/dependency-injection) 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="79494-116">You can customize this behavior by registering a different `IAuthorizationPolicyProvider` implementation in the app’s [dependency injection](xref:fundamentals/dependency-injection) container.</span></span> 

<span data-ttu-id="79494-117">`IAuthorizationPolicyProvider` 인터페이스는 두 개의 Api를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="79494-117">The `IAuthorizationPolicyProvider` interface contains two APIs:</span></span>

* <span data-ttu-id="79494-118">[GetPolicyAsync](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationpolicyprovider.getpolicyasync?view=aspnetcore-2.0#Microsoft_AspNetCore_Authorization_IAuthorizationPolicyProvider_GetPolicyAsync_System_String_) 지정 된 이름에 대 한 권한 부여 정책을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="79494-118">[GetPolicyAsync](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationpolicyprovider.getpolicyasync?view=aspnetcore-2.0#Microsoft_AspNetCore_Authorization_IAuthorizationPolicyProvider_GetPolicyAsync_System_String_) returns an authorization policy for a given name.</span></span>
* <span data-ttu-id="79494-119">[GetDefaultPolicyAsync](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationpolicyprovider.getdefaultpolicyasync?view=aspnetcore-2.0) 기본 권한 부여 정책을 반환 (에 사용 되는 정책 `[Authorize]` 특성 없이 지정 된 정책).</span><span class="sxs-lookup"><span data-stu-id="79494-119">[GetDefaultPolicyAsync](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationpolicyprovider.getdefaultpolicyasync?view=aspnetcore-2.0) returns the default authorization policy (the policy used for `[Authorize]` attributes without a policy specified).</span></span> 

<span data-ttu-id="79494-120">이 두 Api를 구현 하 여 권한 부여 정책을 제공 방법을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79494-120">By implementing these two APIs, you can customize how authorization policies are provided.</span></span>

## <a name="parameterized-authorize-attribute-example"></a><span data-ttu-id="79494-121">매개 변수가 있는 특성 예제 권한 부여</span><span class="sxs-lookup"><span data-stu-id="79494-121">Parameterized authorize attribute example</span></span>

<span data-ttu-id="79494-122">한 가지 시나리오를 `IAuthorizationPolicyProvider` 유용 있도록 설정 하 고 사용자 지정 `[Authorize]` 특성 요구 사항이 매개 변수에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="79494-122">One scenario where `IAuthorizationPolicyProvider` is useful is enabling custom `[Authorize]` attributes whose requirements depend on a parameter.</span></span> <span data-ttu-id="79494-123">예를 들어 [권한 부여 정책 기반](xref:security/authorization/policies) 설명서는 보존 기간 기반 ("AtLeast21") 정책 샘플을 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="79494-123">For example, in [policy-based authorization](xref:security/authorization/policies) documentation, an age-based (“AtLeast21”) policy was used as a sample.</span></span> <span data-ttu-id="79494-124">하는 경우 다른 컨트롤러 작업 서 응용 프로그램에서 사용할 수 있어야 사용자에 게 *다른* 연령에가 여러 다른 보존 기간 기반 정책을 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79494-124">If different controller actions in an app should be made available to users of *different* ages, it might be useful to have many different age-based policies.</span></span> <span data-ttu-id="79494-125">모든 다른 보존 기간 기반 정책을 응용 프로그램에 해야 하는 등록 하는 대신 `AuthorizationOptions`, 정책을 사용자 지정 동적으로 생성할 수 있습니다 `IAuthorizationPolicyProvider`합니다.</span><span class="sxs-lookup"><span data-stu-id="79494-125">Instead of registering all the different age-based policies that the application will need in `AuthorizationOptions`, you can generate the policies dynamically with a custom `IAuthorizationPolicyProvider`.</span></span> <span data-ttu-id="79494-126">더 쉽게 정책을 사용 하 여을 하려면와 같은 사용자 지정 권한 부여 특성을 사용 하 여 동작을 주석을 달 수 `[MinimumAgeAuthorize(20)]`합니다.</span><span class="sxs-lookup"><span data-stu-id="79494-126">To make using the policies easier, you can annotate actions with custom authorization attribute like `[MinimumAgeAuthorize(20)]`.</span></span>

## <a name="custom-authorization-attributes"></a><span data-ttu-id="79494-127">사용자 지정 권한 부여 특성</span><span class="sxs-lookup"><span data-stu-id="79494-127">Custom Authorization Attributes</span></span>

<span data-ttu-id="79494-128">권한 부여 정책 이름으로 식별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="79494-128">Authorization policies are identified by their names.</span></span> <span data-ttu-id="79494-129">사용자 지정 `MinimumAgeAuthorizeAttribute` 설명 된 이전에 해당 권한 부여 정책을 검색 하는 데 사용할 수 있는 문자열에 인수를 매핑할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79494-129">The custom `MinimumAgeAuthorizeAttribute` described previously needs to map arguments into a string that can be used to retrieve the corresponding authorization policy.</span></span> <span data-ttu-id="79494-130">파생 하 여 이렇게 하려면 `AuthorizeAttribute` 하 고는 `Age` 속성 래핑은 `AuthorizeAttribute.Policy` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="79494-130">You can do this by deriving from `AuthorizeAttribute` and making the `Age` property wrap the `AuthorizeAttribute.Policy` property.</span></span>

```CSharp
internal class MinimumAgeAuthorizeAttribute : AuthorizeAttribute
{
    const string POLICY_PREFIX = "MinimumAge";

    public MinimumAgeAuthorizeAttribute(int age) => Age = age;

    // Get or set the Age property by manipulating the underlying Policy property
    public int Age
    {
        get
        {
            if (int.TryParse(Policy.Substring(POLICY_PREFIX.Length), out var age))
            {
                return age;
            }
            return default(int);
        }
        set
        {
            Policy = $"{POLICY_PREFIX}{value.ToString()}";
        }
    }
}
```

<span data-ttu-id="79494-131">이 특성 형식에는 `Policy` 하드 코드 된 접두사를 바탕으로 한 문자열 (`"MinimumAge"`)는 정수 생성자를 통해 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="79494-131">This attribute type has a `Policy` string based on the hard-coded prefix (`"MinimumAge"`) and an integer passed in via the constructor.</span></span>

<span data-ttu-id="79494-132">동일한 방식으로 다른 작업에 적용할 수 `Authorize` 한다는 매개 변수로 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="79494-132">You can apply it to actions in the same way as other `Authorize` attributes except that it takes an integer as a parameter.</span></span>

```CSharp
[MinimumAgeAuthorize(10)]
public IActionResult RequiresMinimumAge10()
```

## <a name="custom-iauthorizationpolicyprovider"></a><span data-ttu-id="79494-133">사용자 지정 IAuthorizationPolicyProvider</span><span class="sxs-lookup"><span data-stu-id="79494-133">Custom IAuthorizationPolicyProvider</span></span>

<span data-ttu-id="79494-134">사용자 지정 `MinimumAgeAuthorizeAttribute` 필요한 모든 최소 보존 기간에 대 한 요청 권한 부여 정책 하기가 쉬워졌습니다.</span><span class="sxs-lookup"><span data-stu-id="79494-134">The custom `MinimumAgeAuthorizeAttribute` makes it easy to request authorization policies for any minimum age desired.</span></span> <span data-ttu-id="79494-135">다음 문제를 해결가 모든 이러한 서로 다른 연령에 대 한 권한 부여 정책을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="79494-135">The next problem to solve is making sure that authorization policies are available for all of those different ages.</span></span> <span data-ttu-id="79494-136">여기에 한 `IAuthorizationPolicyProvider` 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="79494-136">This is where an `IAuthorizationPolicyProvider` is useful.</span></span>

<span data-ttu-id="79494-137">사용 하는 경우 `MinimumAgeAuthorizationAttribute`, 권한 부여 정책 이름 패턴을 따를 것 `"MinimumAge" + Age`하므로 사용자 지정 `IAuthorizationPolicyProvider` 권한 부여 정책에서 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79494-137">When using `MinimumAgeAuthorizationAttribute`, the authorization policy names will follow the pattern `"MinimumAge" + Age`, so the custom `IAuthorizationPolicyProvider` should generate authorization policies by:</span></span>

* <span data-ttu-id="79494-138">정책 이름에서 나 구문 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="79494-138">Parsing the age from the policy name.</span></span>
* <span data-ttu-id="79494-139">사용 하 여 `AuthorizationPolicyBuiler` 새로 만들려면 `AuthorizationPolicy`</span><span class="sxs-lookup"><span data-stu-id="79494-139">Using `AuthorizationPolicyBuiler` to create a new `AuthorizationPolicy`</span></span>
* <span data-ttu-id="79494-140">와 나가에 따라 정책에 요구 사항 추가 `AuthorizationPolicyBuilder.AddRequirements`합니다.</span><span class="sxs-lookup"><span data-stu-id="79494-140">Adding requirements to the policy based on the age with `AuthorizationPolicyBuilder.AddRequirements`.</span></span> <span data-ttu-id="79494-141">다른 시나리오에서 사용할 수 있습니다 `RequireClaim`, `RequireRole`, 또는 `RequireUserName` 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="79494-141">In other scenarios, you might use `RequireClaim`, `RequireRole`, or `RequireUserName` instead.</span></span>

```CSharp
internal class MinimumAgePolicyProvider : IAuthorizationPolicyProvider
{
    const string POLICY_PREFIX = "MinimumAge";

    // Policies are looked up by string name, so expect 'parameters' (like age)
    // to be embedded in the policy names. This is abstracted away from developers
    // by the more strongly-typed attributes derived from AuthorizeAttribute
    // (like [MinimumAgeAuthorize()] in this sample)
    public Task<AuthorizationPolicy> GetPolicyAsync(string policyName)
    {
        if (policyName.StartsWith(POLICY_PREFIX, StringComparison.OrdinalIgnoreCase) &&
            int.TryParse(policyName.Substring(POLICY_PREFIX.Length), out var age))
        {
            var policy = new AuthorizationPolicyBuilder();
            policy.AddRequirements(new MinimumAgeRequirement(age));
            return Task.FromResult(policy.Build());
        }

        return Task.FromResult<AuthorizationPolicy>(null);
    }
}
```

## <a name="multiple-authorization-policy-providers"></a><span data-ttu-id="79494-142">여러 권한 부여 정책 공급자</span><span class="sxs-lookup"><span data-stu-id="79494-142">Multiple authorization policy providers</span></span>

<span data-ttu-id="79494-143">사용자 지정을 사용 하는 경우 `IAuthorizationPolicyProvider` 구현에서는의 인스턴스 하나에 사용 하 여 ASP.NET Core를 염두에서에 둬야 `IAuthorizationPolicyProvider`합니다.</span><span class="sxs-lookup"><span data-stu-id="79494-143">When using custom `IAuthorizationPolicyProvider` implementations, keep in mind that ASP.NET Core only uses one instance of `IAuthorizationPolicyProvider`.</span></span> <span data-ttu-id="79494-144">사용자 지정 공급자를 권한 부여 정책에 대 한 모든 정책 이름을 제공할 수 없는 경우 백업 공급자에 게 다시 속해 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79494-144">If a custom provider isn't able to provide authorization policies for all policy names, it should fall back to a backup provider.</span></span> <span data-ttu-id="79494-145">정책 이름에 대 한 기본 정책을에서 발생 하는 경고만 포함 될 수 있습니다 `[Authorize]` 이름 없이 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="79494-145">Policy names might include those that come from a default policy for `[Authorize]` attributes without a name.</span></span>

<span data-ttu-id="79494-146">예를 들어 응용 프로그램 필요한 사용자 지정 보존 기간 정책와 더 많은 기존 역할 기반 정책 검색 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="79494-146">For example, consider an application needed both custom age policies and more traditional role-based policy retrieval.</span></span> <span data-ttu-id="79494-147">이러한 응용 프로그램에서 사용자 지정 권한 부여 정책 공급자를 사용할 수 있는:</span><span class="sxs-lookup"><span data-stu-id="79494-147">Such an app could use a custom authorization policy provider that:</span></span>

* <span data-ttu-id="79494-148">정책 이름을 구문 분석을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="79494-148">Attempts to parse policy names.</span></span> 
* <span data-ttu-id="79494-149">서로 다른 정책 공급자를 호출 (같은 `DefaultAuthorizationPolicyProvider`) 정책 이름에는 나이 포함 되지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="79494-149">Calls into a different policy provider (like `DefaultAuthorizationPolicyProvider`) if the policy name doesn't contain an age.</span></span>

## <a name="default-policy"></a><span data-ttu-id="79494-150">기본 정책</span><span class="sxs-lookup"><span data-stu-id="79494-150">Default policy</span></span>

<span data-ttu-id="79494-151">사용자 지정 하는 명명 된 권한 부여 규칙을 제공할 뿐만 아니라 `IAuthorizationPolicyProvider` 를 구현 해야 `GetDefaultPolicyAsync` 에 대 한 권한 부여 정책을 제공 하기 `[Authorize]` 정책 이름 지정 하지 않고 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="79494-151">In addition to providing named authorization policies, a custom `IAuthorizationPolicyProvider` needs to implement `GetDefaultPolicyAsync` to provide an authorization policy for `[Authorize]` attributes without a policy name specified.</span></span>

<span data-ttu-id="79494-152">대부분의 경우에서이 권한 부여 특성 하기만 인증된 된 사용자를 호출 하 여 필요한 정책을 확인할 수 있도록 `RequireAuthenticatedUser`:</span><span class="sxs-lookup"><span data-stu-id="79494-152">In many cases, this authorization attribute only requires an authenticated user, so you can make the necessary policy with a call to `RequireAuthenticatedUser`:</span></span>

```CSharp
public Task<AuthorizationPolicy> GetDefaultPolicyAsync() => 
    Task.FromResult(new AuthorizationPolicyBuilder().RequireAuthenticatedUser().Build());
```

<span data-ttu-id="79494-153">사용자 지정의 모든 측면와 마찬가지로 `IAuthorizationPolicyProvider`를 사용자 지정할 수 있습니다이 필요에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="79494-153">As with all aspects of a custom `IAuthorizationPolicyProvider`, you can customize this, as needed.</span></span> <span data-ttu-id="79494-154">일부의 경우:</span><span class="sxs-lookup"><span data-stu-id="79494-154">In some cases:</span></span>

* <span data-ttu-id="79494-155">기본 권한 부여 정책에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79494-155">Default authorization policies might not be used.</span></span>
* <span data-ttu-id="79494-156">기본 정책을 검색 하는 대체 (fallback)에 위임할 수 `IAuthorizationPolicyProvider`합니다.</span><span class="sxs-lookup"><span data-stu-id="79494-156">Retrieving the default policy can be delegated to a fallback `IAuthorizationPolicyProvider`.</span></span>

## <a name="using-a-custom-iauthorizationpolicyprovider"></a><span data-ttu-id="79494-157">사용자 지정 IAuthorizationPolicyProvider를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="79494-157">Using a Custom IAuthorizationPolicyProvider</span></span>

<span data-ttu-id="79494-158">사용자 지정 정책을 사용 하는 `IAuthorizationPolicyProvider`를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79494-158">To use custom policies from an `IAuthorizationPolicyProvider`, you must:</span></span>

* <span data-ttu-id="79494-159">적절 한 등록 `AuthorizationHandler` 종속성 주입을 사용 하는 형식 (에 설명 된 [권한 부여 정책 기반](xref:security/authorization/policies#authorization-handlers)), 모든 권한 부여 정책 기반 시나리오와 마찬가지로 합니다.</span><span class="sxs-lookup"><span data-stu-id="79494-159">Register the appropriate `AuthorizationHandler` types with dependency injection (described in [policy-based authorization](xref:security/authorization/policies#authorization-handlers)), as with all policy-based authorization scenarios.</span></span>
* <span data-ttu-id="79494-160">사용자 지정 등록 `IAuthorizationPolicyProvider` 응용 프로그램의 종속성 주입 서비스 컬렉션 형식에에서 (에서 `Startup.ConfigureServices`) 기본 정책 공급자를 교체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79494-160">Register the custom `IAuthorizationPolicyProvider` type in the app's dependency injection service collection (in `Startup.ConfigureServices`) to replace the default policy provider.</span></span>

```CSharp
services.AddTransient<IAuthorizationPolicyProvider, MinimumAgePolicyProvider>();
```

<span data-ttu-id="79494-161">전체 사용자 지정 `IAuthorizationPolicyProvider` 샘플은 영어로 [aspnet/AuthSamples GitHub 리포지토리](https://github.com/aspnet/AuthSamples/tree/dev/samples/CustomPolicyProvider)합니다.</span><span class="sxs-lookup"><span data-stu-id="79494-161">A complete custom `IAuthorizationPolicyProvider` sample is available in the [aspnet/AuthSamples GitHub repository](https://github.com/aspnet/AuthSamples/tree/dev/samples/CustomPolicyProvider).</span></span>
