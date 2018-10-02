---
title: ASP.NET Core에서 사용자 지정 권한 부여 정책 공급자
author: mjrousos
description: ASP.NET Core 앱에서 사용자 지정 IAuthorizationPolicyProvider를 사용 하 여 동적으로 권한 부여 정책을 생성 하는 방법에 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 05/02/2018
uid: security/authorization/iauthorizationpolicyprovider
ms.openlocfilehash: fdd8f9232c4332aa8307b9dbdfba6af48dfafa72
ms.sourcegitcommit: 317f9be24db600499e79d25872d743af74bd86c0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48045499"
---
# <a name="custom-authorization-policy-providers-using-iauthorizationpolicyprovider-in-aspnet-core"></a><span data-ttu-id="13ecd-103">ASP.NET Core에서 IAuthorizationPolicyProvider를 사용 하 여 사용자 지정 권한 부여 정책 공급자</span><span class="sxs-lookup"><span data-stu-id="13ecd-103">Custom Authorization Policy Providers using IAuthorizationPolicyProvider in ASP.NET Core</span></span> 

<span data-ttu-id="13ecd-104">[Mike Rousos](https://github.com/mjrousos)</span><span class="sxs-lookup"><span data-stu-id="13ecd-104">By [Mike Rousos](https://github.com/mjrousos)</span></span>

<span data-ttu-id="13ecd-105">일반적으로 사용 하는 경우 [정책 기반 권한 부여](xref:security/authorization/policies), 정책을 호출 하 여 등록 된 `AuthorizationOptions.AddPolicy` 권한 부여 서비스 구성의 일부분으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-105">Typically when using [policy-based authorization](xref:security/authorization/policies), policies are registered by calling `AuthorizationOptions.AddPolicy` as part of authorization service configuration.</span></span> <span data-ttu-id="13ecd-106">일부 시나리오에서는 없을 수 (또는 바람직하지) 권한 부여 정책을 모두 이러한 방식으로 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-106">In some scenarios, it may not be possible (or desirable) to register all authorization policies in this way.</span></span> <span data-ttu-id="13ecd-107">이러한 경우 사용자 지정을 사용할 수 있습니다 `IAuthorizationPolicyProvider` 권한 부여 정책을 제공 하는 방법을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-107">In those cases, you can use a custom `IAuthorizationPolicyProvider` to control how authorization policies are supplied.</span></span>

<span data-ttu-id="13ecd-108">예제 시나리오의 경우 사용자 지정 [IAuthorizationPolicyProvider](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationpolicyprovider) 유용할 수 있습니다 포함:</span><span class="sxs-lookup"><span data-stu-id="13ecd-108">Examples of scenarios where a custom [IAuthorizationPolicyProvider](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationpolicyprovider) may be useful include:</span></span>

* <span data-ttu-id="13ecd-109">외부 서비스를 사용 하 여 정책 평가 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-109">Using an external service to provide policy evaluation.</span></span>
* <span data-ttu-id="13ecd-110">(다른 방 번호 또는 예를 들어 연령대)에 광범위 한 정책 사용 하므로 것은 의미가 없습니다 사용 하 여 각 개별 권한 부여 정책을 추가 하는 `AuthorizationOptions.AddPolicy` 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-110">Using a large range of policies (for different room numbers or ages, for example), so it doesn’t make sense to add each individual authorization policy with an `AuthorizationOptions.AddPolicy` call.</span></span>
* <span data-ttu-id="13ecd-111">외부 데이터 원본 (예: 데이터베이스)에 대 한 정보를 기반으로 하는 런타임 시 정책 만들기 또는 다른 메커니즘을 통해 권한 부여 요구 사항을 동적으로 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-111">Creating policies at runtime based on information in an external data source (like a database) or determining authorization requirements dynamically through another mechanism.</span></span>

<span data-ttu-id="13ecd-112">[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/AuthSamples/tree/master/samples/CustomPolicyProvider) 에서 합니다 [aspnet/AuthSamples GitHub 리포지토리](https://github.com/aspnet/AuthSamples)합니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-112">[View or download sample code](https://github.com/aspnet/AuthSamples/tree/master/samples/CustomPolicyProvider) from the [aspnet/AuthSamples GitHub repository](https://github.com/aspnet/AuthSamples).</span></span> <span data-ttu-id="13ecd-113">Aspnet/AuthSamples 리포지토리 ZIP 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-113">Download the aspnet/AuthSamples repository ZIP file.</span></span>
<span data-ttu-id="13ecd-114">압축을 풉니다 합니다 *AuthSamples master.zip* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-114">Unzip the *AuthSamples-master.zip* file.</span></span> <span data-ttu-id="13ecd-115">로 이동 합니다 *샘플/CustomPolicyProvider* 프로젝트 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-115">Navigate to the *samples/CustomPolicyProvider* project folder.</span></span>

## <a name="customize-policy-retrieval"></a><span data-ttu-id="13ecd-116">정책 검색을 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="13ecd-116">Customize policy retrieval</span></span>

<span data-ttu-id="13ecd-117">ASP.NET Core 앱의 구현을 사용 합니다 `IAuthorizationPolicyProvider` 권한 부여 정책을 검색 하는 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-117">ASP.NET Core apps use an implementation of the `IAuthorizationPolicyProvider` interface to retrieve authorization policies.</span></span> <span data-ttu-id="13ecd-118">기본적으로 [DefaultAuthorizationPolicyProvider](/dotnet/api/microsoft.aspnetcore.authorization.defaultauthorizationpolicyprovider) 등록 되 고 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-118">By default, [DefaultAuthorizationPolicyProvider](/dotnet/api/microsoft.aspnetcore.authorization.defaultauthorizationpolicyprovider) is registered and used.</span></span> <span data-ttu-id="13ecd-119">`DefaultAuthorizationPolicyProvider` 정책을 반환 합니다.는 `AuthorizationOptions` 에서 제공 되는 `IServiceCollection.AddAuthorization` 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-119">`DefaultAuthorizationPolicyProvider` returns policies from the `AuthorizationOptions` provided in an `IServiceCollection.AddAuthorization` call.</span></span>

<span data-ttu-id="13ecd-120">다른 등록 하 여이 동작을 사용자 지정할 수 있습니다 `IAuthorizationPolicyProvider` 앱의 구현을 [종속성 주입](xref:fundamentals/dependency-injection) 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-120">You can customize this behavior by registering a different `IAuthorizationPolicyProvider` implementation in the app’s [dependency injection](xref:fundamentals/dependency-injection) container.</span></span> 

<span data-ttu-id="13ecd-121">`IAuthorizationPolicyProvider` 인터페이스 두 Api가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-121">The `IAuthorizationPolicyProvider` interface contains two APIs:</span></span>

* <span data-ttu-id="13ecd-122">[GetPolicyAsync](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationpolicyprovider.getpolicyasync#Microsoft_AspNetCore_Authorization_IAuthorizationPolicyProvider_GetPolicyAsync_System_String_) 지정 된 이름에 대 한 권한 부여 정책을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-122">[GetPolicyAsync](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationpolicyprovider.getpolicyasync#Microsoft_AspNetCore_Authorization_IAuthorizationPolicyProvider_GetPolicyAsync_System_String_) returns an authorization policy for a given name.</span></span>
* <span data-ttu-id="13ecd-123">[GetDefaultPolicyAsync](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationpolicyprovider.getdefaultpolicyasync) 기본 권한 부여 정책을 반환 합니다 (에 사용 된 정책 `[Authorize]` 지정 된 정책 없이 특성).</span><span class="sxs-lookup"><span data-stu-id="13ecd-123">[GetDefaultPolicyAsync](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizationpolicyprovider.getdefaultpolicyasync) returns the default authorization policy (the policy used for `[Authorize]` attributes without a policy specified).</span></span> 

<span data-ttu-id="13ecd-124">이러한 두 가지 Api를 구현 하 여 권한 부여 정책을 제공 하는 방식을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-124">By implementing these two APIs, you can customize how authorization policies are provided.</span></span>

## <a name="parameterized-authorize-attribute-example"></a><span data-ttu-id="13ecd-125">매개 변수가 특성 예제 권한 부여</span><span class="sxs-lookup"><span data-stu-id="13ecd-125">Parameterized authorize attribute example</span></span>

<span data-ttu-id="13ecd-126">시나리오 중 하나는 `IAuthorizationPolicyProvider` 유용 사용자 지정이 사용 가능 하도록 `[Authorize]` 특성 요구 사항이 있는 매개 변수에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-126">One scenario where `IAuthorizationPolicyProvider` is useful is enabling custom `[Authorize]` attributes whose requirements depend on a parameter.</span></span> <span data-ttu-id="13ecd-127">예를 들어 [정책 기반 권한 부여](xref:security/authorization/policies) 설명서에는 보존 기간 기반 ("AtLeast21") 정책 샘플을 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-127">For example, in [policy-based authorization](xref:security/authorization/policies) documentation, an age-based (“AtLeast21”) policy was used as a sample.</span></span> <span data-ttu-id="13ecd-128">하는 경우 다른 컨트롤러 작업 앱에서 사용할 수 있어야 사용자에 게 *다른* 연령에 많은 다른 보존 기간 기반 정책이 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-128">If different controller actions in an app should be made available to users of *different* ages, it might be useful to have many different age-based policies.</span></span> <span data-ttu-id="13ecd-129">모든 다른 보존 기간 기반 되는 정책 응용 프로그램의 필요를 등록 하는 대신 `AuthorizationOptions`, 정책을 사용자 지정 동적으로 생성할 수 있습니다 `IAuthorizationPolicyProvider`합니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-129">Instead of registering all the different age-based policies that the application will need in `AuthorizationOptions`, you can generate the policies dynamically with a custom `IAuthorizationPolicyProvider`.</span></span> <span data-ttu-id="13ecd-130">사용 하 여 정책을 쉽게, 같은 사용자 지정 권한 부여 특성을 사용 하 여 작업 주석을 달 수 `[MinimumAgeAuthorize(20)]`입니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-130">To make using the policies easier, you can annotate actions with custom authorization attribute like `[MinimumAgeAuthorize(20)]`.</span></span>

## <a name="custom-authorization-attributes"></a><span data-ttu-id="13ecd-131">사용자 지정 권한 부여 특성</span><span class="sxs-lookup"><span data-stu-id="13ecd-131">Custom Authorization Attributes</span></span>

<span data-ttu-id="13ecd-132">권한 부여 정책 이름으로 식별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-132">Authorization policies are identified by their names.</span></span> <span data-ttu-id="13ecd-133">사용자 지정 `MinimumAgeAuthorizeAttribute` 설명 이전에 해당 하는 권한 부여 정책을 검색 하는 문자열에 인수를 매핑하는 데 필요한 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-133">The custom `MinimumAgeAuthorizeAttribute` described previously needs to map arguments into a string that can be used to retrieve the corresponding authorization policy.</span></span> <span data-ttu-id="13ecd-134">파생 하 여이 수행할 수 있습니다 `AuthorizeAttribute` 줄어들고 합니다 `Age` 속성 줄 바꿈 합니다 `AuthorizeAttribute.Policy` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-134">You can do this by deriving from `AuthorizeAttribute` and making the `Age` property wrap the `AuthorizeAttribute.Policy` property.</span></span>

```csharp
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

<span data-ttu-id="13ecd-135">이 특성 형식에는 `Policy` 하드 코드 된 접두사를 바탕으로 한 문자열 (`"MinimumAge"`) 생성자를 통해 전달 된 정수 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-135">This attribute type has a `Policy` string based on the hard-coded prefix (`"MinimumAge"`) and an integer passed in via the constructor.</span></span>

<span data-ttu-id="13ecd-136">동일한 방식으로 다른 작업에 적용할 수 있습니다 `Authorize` 매개 변수로 정수 소요 되는 점을 제외 하 고 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-136">You can apply it to actions in the same way as other `Authorize` attributes except that it takes an integer as a parameter.</span></span>

```csharp
[MinimumAgeAuthorize(10)]
public IActionResult RequiresMinimumAge10()
```

## <a name="custom-iauthorizationpolicyprovider"></a><span data-ttu-id="13ecd-137">사용자 지정 IAuthorizationPolicyProvider</span><span class="sxs-lookup"><span data-stu-id="13ecd-137">Custom IAuthorizationPolicyProvider</span></span>

<span data-ttu-id="13ecd-138">사용자 지정 `MinimumAgeAuthorizeAttribute` 쉽게 요청 권한 부여 정책에 필요한 모든 최소 보존 기간에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-138">The custom `MinimumAgeAuthorizeAttribute` makes it easy to request authorization policies for any minimum age desired.</span></span> <span data-ttu-id="13ecd-139">다음 문제를 해결 하는 이러한 다른 연령대의 모든 권한 부여 정책을 사용할 수 있는지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-139">The next problem to solve is making sure that authorization policies are available for all of those different ages.</span></span> <span data-ttu-id="13ecd-140">이 경우는 `IAuthorizationPolicyProvider` 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-140">This is where an `IAuthorizationPolicyProvider` is useful.</span></span>

<span data-ttu-id="13ecd-141">사용 하는 경우 `MinimumAgeAuthorizationAttribute`, 권한 부여 정책 이름 패턴을 따릅니다 `"MinimumAge" + Age`이므로 사용자 지정 `IAuthorizationPolicyProvider` 권한 부여 정책을 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-141">When using `MinimumAgeAuthorizationAttribute`, the authorization policy names will follow the pattern `"MinimumAge" + Age`, so the custom `IAuthorizationPolicyProvider` should generate authorization policies by:</span></span>

* <span data-ttu-id="13ecd-142">정책 이름에서 나 구문 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-142">Parsing the age from the policy name.</span></span>
* <span data-ttu-id="13ecd-143">사용 하 여 `AuthorizationPolicyBuilder` 새로 만들려면 `AuthorizationPolicy`</span><span class="sxs-lookup"><span data-stu-id="13ecd-143">Using `AuthorizationPolicyBuilder` to create a new `AuthorizationPolicy`</span></span>
* <span data-ttu-id="13ecd-144">사용 하 여 보존 기간에 따라 정책에 요구 사항 추가 `AuthorizationPolicyBuilder.AddRequirements`합니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-144">Adding requirements to the policy based on the age with `AuthorizationPolicyBuilder.AddRequirements`.</span></span> <span data-ttu-id="13ecd-145">다른 시나리오에서는 사용할 수 있습니다 `RequireClaim`하십시오 `RequireRole`, 또는 `RequireUserName` 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-145">In other scenarios, you might use `RequireClaim`, `RequireRole`, or `RequireUserName` instead.</span></span>

```csharp
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

## <a name="multiple-authorization-policy-providers"></a><span data-ttu-id="13ecd-146">여러 권한 부여 정책 공급자</span><span class="sxs-lookup"><span data-stu-id="13ecd-146">Multiple authorization policy providers</span></span>

<span data-ttu-id="13ecd-147">사용자 지정을 사용 하는 경우 `IAuthorizationPolicyProvider` 구현에서는 ASP.NET Core의 인스턴스 하나에 사용 하 여 있다는 사실을 잊지 마십시오 `IAuthorizationPolicyProvider`합니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-147">When using custom `IAuthorizationPolicyProvider` implementations, keep in mind that ASP.NET Core only uses one instance of `IAuthorizationPolicyProvider`.</span></span> <span data-ttu-id="13ecd-148">사용자 지정 공급자를 모든 정책 이름에 대 한 권한 부여 정책을 제공할 수 없으면 백업 공급자에 다시 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-148">If a custom provider isn't able to provide authorization policies for all policy names, it should fall back to a backup provider.</span></span> <span data-ttu-id="13ecd-149">정책 이름에 대 한 기본 정책에서 발생 하는 포함 될 수 있습니다 `[Authorize]` 이름이 없는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-149">Policy names might include those that come from a default policy for `[Authorize]` attributes without a name.</span></span>

<span data-ttu-id="13ecd-150">예를 들어, 응용 프로그램에 필요한 사용자 지정 보존 기간 정책 및 기존의 역할 기반 정책 검색 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-150">For example, consider an application needed both custom age policies and more traditional role-based policy retrieval.</span></span> <span data-ttu-id="13ecd-151">이러한 앱을 사용자 지정 권한 부여 정책 공급자를 사용할 수 있는:</span><span class="sxs-lookup"><span data-stu-id="13ecd-151">Such an app could use a custom authorization policy provider that:</span></span>

* <span data-ttu-id="13ecd-152">정책 이름을 구문 분석 하려고 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-152">Attempts to parse policy names.</span></span> 
* <span data-ttu-id="13ecd-153">다른 정책 공급자에 대 한 호출 (같은 `DefaultAuthorizationPolicyProvider`) 정책 이름이 나 포함 되지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="13ecd-153">Calls into a different policy provider (like `DefaultAuthorizationPolicyProvider`) if the policy name doesn't contain an age.</span></span>

## <a name="default-policy"></a><span data-ttu-id="13ecd-154">기본 정책</span><span class="sxs-lookup"><span data-stu-id="13ecd-154">Default policy</span></span>

<span data-ttu-id="13ecd-155">명명 된 권한 부여 정책에 사용자 지정을 제공 하는 것 외에도 `IAuthorizationPolicyProvider` 를 구현 해야 `GetDefaultPolicyAsync` 에 대 한 권한 부여 정책을 제공 `[Authorize]` 정책 이름 지정 하지 않고 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-155">In addition to providing named authorization policies, a custom `IAuthorizationPolicyProvider` needs to implement `GetDefaultPolicyAsync` to provide an authorization policy for `[Authorize]` attributes without a policy name specified.</span></span>

<span data-ttu-id="13ecd-156">대부분의 경우이 권한 부여 특성 하기만 인증된 된 사용자에 대 한 호출을 사용 하 여 필요한 정책을 있도록 `RequireAuthenticatedUser`:</span><span class="sxs-lookup"><span data-stu-id="13ecd-156">In many cases, this authorization attribute only requires an authenticated user, so you can make the necessary policy with a call to `RequireAuthenticatedUser`:</span></span>

```csharp
public Task<AuthorizationPolicy> GetDefaultPolicyAsync() => 
    Task.FromResult(new AuthorizationPolicyBuilder().RequireAuthenticatedUser().Build());
```

<span data-ttu-id="13ecd-157">사용자 지정의 모든 측면으로 `IAuthorizationPolicyProvider`를 사용자 지정할 수 있습니다 따라서 필요에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-157">As with all aspects of a custom `IAuthorizationPolicyProvider`, you can customize this, as needed.</span></span> <span data-ttu-id="13ecd-158">일부의 경우:</span><span class="sxs-lookup"><span data-stu-id="13ecd-158">In some cases:</span></span>

* <span data-ttu-id="13ecd-159">기본 권한 부여 정책은 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-159">Default authorization policies might not be used.</span></span>
* <span data-ttu-id="13ecd-160">기본 정책을 검색 하는 대체 (fallback)에 위임할 수 있습니다 `IAuthorizationPolicyProvider`합니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-160">Retrieving the default policy can be delegated to a fallback `IAuthorizationPolicyProvider`.</span></span>

## <a name="use-a-custom-iauthorizationpolicyprovider"></a><span data-ttu-id="13ecd-161">사용자 지정 IAuthorizationPolicyProvider 사용</span><span class="sxs-lookup"><span data-stu-id="13ecd-161">Use a custom IAuthorizationPolicyProvider</span></span>

<span data-ttu-id="13ecd-162">사용자 지정 정책을 사용 하는 `IAuthorizationPolicyProvider`를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-162">To use custom policies from an `IAuthorizationPolicyProvider`, you must:</span></span>

* <span data-ttu-id="13ecd-163">적절 한 등록 `AuthorizationHandler` 종속성 주입을 사용 하 여 형식 (에서 설명한 [정책 기반 권한 부여](xref:security/authorization/policies#authorization-handlers)), 모든 정책 기반 권한 부여 시나리오와 마찬가지로 합니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-163">Register the appropriate `AuthorizationHandler` types with dependency injection (described in [policy-based authorization](xref:security/authorization/policies#authorization-handlers)), as with all policy-based authorization scenarios.</span></span>
* <span data-ttu-id="13ecd-164">사용자 지정 등록 `IAuthorizationPolicyProvider` 앱의 종속성 주입 서비스 컬렉션의 형식 (에서 `Startup.ConfigureServices`) 기본 정책 공급자를 교체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-164">Register the custom `IAuthorizationPolicyProvider` type in the app's dependency injection service collection (in `Startup.ConfigureServices`) to replace the default policy provider.</span></span>

```csharp
services.AddSingleton<IAuthorizationPolicyProvider, MinimumAgePolicyProvider>();
```

<span data-ttu-id="13ecd-165">전체 사용자 지정 `IAuthorizationPolicyProvider` 샘플에서 사용할 수는 [aspnet/AuthSamples GitHub 리포지토리](https://github.com/aspnet/AuthSamples/tree/master/samples/CustomPolicyProvider)합니다.</span><span class="sxs-lookup"><span data-stu-id="13ecd-165">A complete custom `IAuthorizationPolicyProvider` sample is available in the [aspnet/AuthSamples GitHub repository](https://github.com/aspnet/AuthSamples/tree/master/samples/CustomPolicyProvider).</span></span>
