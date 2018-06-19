---
uid: web-api/overview/security/authentication-filters
title: ASP.NET Web API 2의에서 인증 필터 | Microsoft Docs
author: MikeWasson
description: 인증 필터는 HTTP 요청을 인증 하는 구성 요소입니다. 인증 필터를 둘 다 지원 web API 2 및 MVC 5 하지만 약간 다른...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/25/2014
ms.topic: article
ms.assetid: b9882e53-b3ca-4def-89b0-322846973ccb
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/security/authentication-filters
msc.type: authoredcontent
ms.openlocfilehash: 16e451f52799625983368bc938091eff47019b52
ms.sourcegitcommit: 016f4d58663bcd442930227022de23fb3abee0b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2018
ms.locfileid: "29153520"
---
<a name="authentication-filters-in-aspnet-web-api-2"></a><span data-ttu-id="354ad-104">ASP.NET Web API 2의에서 인증 필터</span><span class="sxs-lookup"><span data-stu-id="354ad-104">Authentication Filters in ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="354ad-105">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="354ad-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="354ad-106">인증 필터는 HTTP 요청을 인증 하는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-106">An authentication filter is a component that authenticates an HTTP request.</span></span> <span data-ttu-id="354ad-107">인증 필터를 둘 다 지원 web API 2 및 MVC 5 있지만 필터 인터페이스에 대 한 명명 규칙에서 주로 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-107">Web API 2 and MVC 5 both support authentication filters, but they differ slightly, mostly in the naming conventions for the filter interface.</span></span> <span data-ttu-id="354ad-108">이 항목에서는 웹 API 인증 필터를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-108">This topic describes Web API authentication filters.</span></span>


<span data-ttu-id="354ad-109">인증 필터 개별 컨트롤러 또는 동작에 대 한 인증 체계를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-109">Authentication filters let you set an authentication scheme for individual controllers or actions.</span></span> <span data-ttu-id="354ad-110">이런 방식으로 앱 다른 HTTP 리소스에 대 한 다른 인증 메커니즘을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-110">That way, your app can support different authentication mechanisms for different HTTP resources.</span></span>

<span data-ttu-id="354ad-111">이 문서에서는 코드에서 보여 드리 려 고 [기본 인증](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/BasicAuthentication/ReadMe.txt) 샘플 [http://aspnet.codeplex.com](http://aspnet.codeplex.com)합니다. 이 샘플에서는 HTTP 기본 액세스 인증 체계 (RFC 2617)를 구현 하는 인증 필터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-111">In this article, I'll show code from the [Basic Authentication](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/BasicAuthentication/ReadMe.txt) sample on [http://aspnet.codeplex.com](http://aspnet.codeplex.com). The sample shows an authentication filter that implements the HTTP Basic Access Authentication scheme (RFC 2617).</span></span> <span data-ttu-id="354ad-112">필터 라는 클래스에서 구현 되 `IdentityBasicAuthenticationAttribute`합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-112">The filter is implemented in a class named `IdentityBasicAuthenticationAttribute`.</span></span> <span data-ttu-id="354ad-113">모든 샘플의 코드는 인증 필터를 작성 하는 방법을 보여 주는 해당 부분만 소개 하지 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-113">I won't show all of the code from the sample, just the parts that illustrate how to write an authentication filter.</span></span>

## <a name="setting-an-authentication-filter"></a><span data-ttu-id="354ad-114">인증 필터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-114">Setting an Authentication Filter</span></span>

<span data-ttu-id="354ad-115">다른 필터와 마찬가지로 인증 필터 적용 된 컨트롤러, 작업 별로 또는 전체적으로 모든 Web API 컨트롤러 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-115">Like other filters, authentication filters can be applied per-controller, per-action, or globally to all Web API controllers.</span></span>

<span data-ttu-id="354ad-116">컨트롤러에는 인증 필터를 적용 하려면 필터 특성으로 컨트롤러 클래스 데코 레이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-116">To apply an authentication filter to a controller, decorate the controller class with the filter attribute.</span></span> <span data-ttu-id="354ad-117">다음 코드에서는 `[IdentityBasicAuthentication]` 모든 컨트롤러의 작업에 대 한 기본 인증을 사용할 수 있는 컨트롤러 클래스에 대 한 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-117">The following code sets the `[IdentityBasicAuthentication]` filter on a controller class, which enables Basic Authentication for all of the controller's actions.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample1.cs)]

<span data-ttu-id="354ad-118">한 동작으로 필터를 적용 하려면 작업 필터와 데코 레이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-118">To apply the filter to one action, decorate the action with the filter.</span></span> <span data-ttu-id="354ad-119">다음 코드에서는 `[IdentityBasicAuthentication]` 컨트롤러의에 대 한 필터 `Post` 메서드.</span><span class="sxs-lookup"><span data-stu-id="354ad-119">The following code sets the `[IdentityBasicAuthentication]` filter on the controller's `Post` method.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample2.cs)]

<span data-ttu-id="354ad-120">모든 Web API 컨트롤러에 필터를 적용 하려면에 추가 **GlobalConfiguration.Filters**합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-120">To apply the filter to all Web API controllers, add it to **GlobalConfiguration.Filters**.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample3.cs)]

## <a name="implementing-a-web-api-authentication-filter"></a><span data-ttu-id="354ad-121">웹 API 인증 필터를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-121">Implementing a Web API Authentication Filter</span></span>

<span data-ttu-id="354ad-122">인증 필터 Web API에서 구현 된 [System.Web.Http.Filters.IAuthenticationFilter](https://msdn.microsoft.com/library/system.web.http.filters.iauthenticationfilter.aspx) 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-122">In Web API, authentication filters implement the [System.Web.Http.Filters.IAuthenticationFilter](https://msdn.microsoft.com/library/system.web.http.filters.iauthenticationfilter.aspx) interface.</span></span> <span data-ttu-id="354ad-123">상속 해야 **System.Attribute**을 특성으로 적용 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-123">They should also inherit from **System.Attribute**, in order to be applied as attributes.</span></span>

<span data-ttu-id="354ad-124">**IAuthenticationFilter** 인터페이스에는 두 가지 방법:</span><span class="sxs-lookup"><span data-stu-id="354ad-124">The **IAuthenticationFilter** interface has two methods:</span></span>

- <span data-ttu-id="354ad-125">**AuthenticateAsync** 있는 경우 요청에 자격 증명을 확인 하 여 요청을 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-125">**AuthenticateAsync** authenticates the request by validating credentials in the request, if present.</span></span>
- <span data-ttu-id="354ad-126">**ChallengeAsync** 필요한 경우 HTTP 응답에 대 한 인증 챌린지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-126">**ChallengeAsync** adds an authentication challenge to the HTTP response, if needed.</span></span>

<span data-ttu-id="354ad-127">에 정의 된 인증 흐름에 해당 하는 이러한 메서드 [RFC 2612](http://tools.ietf.org/html/rfc2616) 및 [RFC 2617](http://tools.ietf.org/html/rfc2617):</span><span class="sxs-lookup"><span data-stu-id="354ad-127">These methods correspond to the authentication flow defined in [RFC 2612](http://tools.ietf.org/html/rfc2616) and [RFC 2617](http://tools.ietf.org/html/rfc2617):</span></span>

1. <span data-ttu-id="354ad-128">클라이언트 자격 증명을 인증 헤더에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-128">The client sends credentials in the Authorization header.</span></span> <span data-ttu-id="354ad-129">이 문제는 일반적으로 클라이언트에서 서버에서 401 (권한 없음된) 응답을 받은 후에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-129">This typically happens after the client receives a 401 (Unauthorized) response from the server.</span></span> <span data-ttu-id="354ad-130">그러나 클라이언트는 401 가져오기 후 뿐 아니라 모든 요청에 자격 증명을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-130">However, a client can send credentials with any request, not just after getting a 401.</span></span>
2. <span data-ttu-id="354ad-131">서버 자격 증명을 허용 하지는 401 (권한 없음된) 응답을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-131">If the server does not accept the credentials, it returns a 401 (Unauthorized) response.</span></span> <span data-ttu-id="354ad-132">응답에는 하나 이상의 문제를 포함 하는 Www-authenticate 헤더가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-132">The response includes a Www-Authenticate header that contains one or more challenges.</span></span> <span data-ttu-id="354ad-133">각 시도 서버에서 인식 하는 인증 체계를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-133">Each challenge specifies an authentication scheme recognized by the server.</span></span>

<span data-ttu-id="354ad-134">서버는 익명 요청에서 401을 반환할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-134">The server can also return 401 from an anonymous request.</span></span> <span data-ttu-id="354ad-135">사실, 일반적으로 이것은 인증 프로세스가 시작 되는 방식:</span><span class="sxs-lookup"><span data-stu-id="354ad-135">In fact, that's typically how the authentication process is initiated:</span></span>

1. <span data-ttu-id="354ad-136">클라이언트는 익명 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-136">The client sends an anonymous request.</span></span>
2. <span data-ttu-id="354ad-137">서버 401을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-137">The server returns 401.</span></span>
3. <span data-ttu-id="354ad-138">클라이언트 자격 증명을 사용 하 여 요청을 다시 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-138">The clients resends the request with credentials.</span></span>

<span data-ttu-id="354ad-139">이 흐름을에 둘 다 *인증* 및 *권한 부여* 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-139">This flow includes both *authentication* and *authorization* steps.</span></span>

- <span data-ttu-id="354ad-140">인증은 클라이언트의 id를 증명합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-140">Authentication proves the identity of the client.</span></span>
- <span data-ttu-id="354ad-141">권한 부여 클라이언트 특정 리소스에 액세스할 수 있는지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-141">Authorization determines whether the client can access a particular resource.</span></span>

<span data-ttu-id="354ad-142">웹 API에 인증 필터 권한 부여 하지 않지만 인증을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-142">In Web API, authentication filters handle authentication, but not authorization.</span></span> <span data-ttu-id="354ad-143">컨트롤러 작업 내부에서 실행 되거나 권한 부여 필터에 의해 권한 부여를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-143">Authorization should be done by an authorization filter or inside the controller action.</span></span>

<span data-ttu-id="354ad-144">Web API 2 파이프라인에서 흐름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-144">Here is the flow in the Web API 2 pipeline:</span></span>

1. <span data-ttu-id="354ad-145">동작을 호출 하기 전에 웹 API에는 해당 작업에 대 한 인증 필터의 목록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-145">Before invoking an action, Web API creates a list of the authentication filters for that action.</span></span> <span data-ttu-id="354ad-146">동작 범위, 범위 컨트롤러 및 글로벌 범위를 사용 하 여 필터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-146">This includes filters with action scope, controller scope, and global scope.</span></span>
2. <span data-ttu-id="354ad-147">웹 API 호출 **AuthenticateAsync** 목록에는 모든 필터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-147">Web API calls **AuthenticateAsync** on every filter in the list.</span></span> <span data-ttu-id="354ad-148">각 필터에는 요청에 자격 증명 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-148">Each filter can validate credentials in the request.</span></span> <span data-ttu-id="354ad-149">모든 필터에 성공적으로 자격 증명 유효성을 검사 하는 경우 필터 만듭니다는 **IPrincipal** 요청에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-149">If any filter successfully validates credentials, the filter creates an **IPrincipal** and attaches it to the request.</span></span> <span data-ttu-id="354ad-150">또한 필터 오류가이 시점에서 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-150">A filter can also trigger an error at this point.</span></span> <span data-ttu-id="354ad-151">이 경우 나머지 파이프라인 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-151">If so, the rest of the pipeline does not run.</span></span>
3. <span data-ttu-id="354ad-152">요청은 오류가 없는 경우 파이프라인의 나머지 부분을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-152">Assuming there is no error, the request flows through the rest of the pipeline.</span></span>
4. <span data-ttu-id="354ad-153">Web API에서 모든 인증 필터를 호출 하는 마지막으로, **ChallengeAsync** 메서드.</span><span class="sxs-lookup"><span data-stu-id="354ad-153">Finally, Web API calls every authentication filter's **ChallengeAsync** method.</span></span> <span data-ttu-id="354ad-154">필요한 경우를 응답에 챌린지를 추가 하려면이 메서드를 사용 하는 필터.</span><span class="sxs-lookup"><span data-stu-id="354ad-154">Filters use this method to add a challenge to the response, if needed.</span></span> <span data-ttu-id="354ad-155">일반적으로 (항상 그렇지는 않지만)는에서 사용 하는 발생할 401 오류에 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-155">Typically (but not always) that would happen in response to a 401 error.</span></span>

<span data-ttu-id="354ad-156">다음 다이어그램은 두 가지 가능한 경우를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-156">The following diagrams show two possible cases.</span></span> <span data-ttu-id="354ad-157">첫 번째 호출 인증 필터를 성공적으로 요청 인증, 권한 부여 필터는 요청에 권한을 부여 하 고 컨트롤러 작업 200 (정상)를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-157">In the first, the authentication filter successfully authenticates the request, an authorization filter authorizes the request, and the controller action returns 200 (OK).</span></span>

![](authentication-filters/_static/image1.png)

<span data-ttu-id="354ad-158">두 번째 예제에서는 인증 필터는 요청을 인증 하지만 권한 부여 필터 401 (권한 없음)을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-158">In the second example, the authentication filter authenticates the request, but the authorization filter returns 401 (Unauthorized).</span></span> <span data-ttu-id="354ad-159">이 경우에 컨트롤러 동작 호출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-159">In this case, the controller action is not invoked.</span></span> <span data-ttu-id="354ad-160">인증 필터를 응답에 Www 인증 헤더를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-160">The authentication filter adds a Www-Authenticate header to the response.</span></span>

![](authentication-filters/_static/image2.png)

<span data-ttu-id="354ad-161">다른 조합은 가능한&mdash;예를 들어 컨트롤러 동작 익명 요청을 허용 하는 경우 할 수 있습니다는 인증 필터 하지만 없습니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-161">Other combinations are possible&mdash;for example, if the controller action allows anonymous requests, you might have an authentication filter but no authorization.</span></span>

## <a name="implementing-the-authenticateasync-method"></a><span data-ttu-id="354ad-162">AuthenticateAsync 메서드 구현</span><span class="sxs-lookup"><span data-stu-id="354ad-162">Implementing the AuthenticateAsync Method</span></span>

<span data-ttu-id="354ad-163">**AuthenticateAsync** 메서드는 요청을 인증 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-163">The **AuthenticateAsync** method tries to authenticate the request.</span></span> <span data-ttu-id="354ad-164">메서드 시그니처는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-164">Here is the method signature:</span></span>

[!code-csharp[Main](authentication-filters/samples/sample4.cs)]

<span data-ttu-id="354ad-165">**AuthenticateAsync** 메서드는 다음 중 하나를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-165">The **AuthenticateAsync** method must do one of the following:</span></span>

1. <span data-ttu-id="354ad-166">Nothing (아무)입니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-166">Nothing (no-op).</span></span>
2. <span data-ttu-id="354ad-167">만들기는 **IPrincipal** 요청에 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-167">Create an **IPrincipal** and set it on the request.</span></span>
3. <span data-ttu-id="354ad-168">오류 결과 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-168">Set an error result.</span></span>

<span data-ttu-id="354ad-169">요청 옵션 (1) 의미 필터 이해할 수 있는 자격 증명을 변수가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-169">Option (1) means the request did not have any credentials that the filter understands.</span></span> <span data-ttu-id="354ad-170">옵션 (2) 의미 필터에서 요청을 성공적으로 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-170">Option (2) means the filter successfully authenticated the request.</span></span> <span data-ttu-id="354ad-171">요청 옵션 (3) 이면 오류 응답을 트리거하는 잘못 된 자격 증명 (예: 잘못 된 암호)로, 했습니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-171">Option (3) means the request had invalid credentials (like the wrong password), which triggers an error response.</span></span>

<span data-ttu-id="354ad-172">다음은 구현에 대 한 일반 개요 **AuthenticateAsync**합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-172">Here is a general outline for implementing **AuthenticateAsync**.</span></span>

1. <span data-ttu-id="354ad-173">요청에 자격 증명을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-173">Look for credentials in the request.</span></span>
2. <span data-ttu-id="354ad-174">자격 증명이 없는 경우 아무 작업도 수행 하 고 (op)를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-174">If there are no credentials, do nothing and return (no-op).</span></span>
3. <span data-ttu-id="354ad-175">자격 증명 하는 경우 필터는 인증 체계를 인식 하지 않으므로 아무 작업도 수행 하 고 (op)를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-175">If there are credentials but the filter does not recognize the authentication scheme, do nothing and return (no-op).</span></span> <span data-ttu-id="354ad-176">파이프라인에서 다른 필터는 구성표를 이해할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-176">Another filter in the pipeline might understand the scheme.</span></span>
4. <span data-ttu-id="354ad-177">필터를 이해 하는 자격 증명 경우 인증 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-177">If there are credentials that the filter understands, try to authenticate them.</span></span>
5. <span data-ttu-id="354ad-178">잘못 된 자격 증명을 설정 하 여 401 반환 `context.ErrorResult`합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-178">If the credentials are bad, return 401 by setting `context.ErrorResult`.</span></span>
6. <span data-ttu-id="354ad-179">자격 증명이 유효 만들기는 **IPrincipal** 설정 `context.Principal`합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-179">If the credentials are valid, create an **IPrincipal** and set `context.Principal`.</span></span>

<span data-ttu-id="354ad-180">다음 코드에 나와 있는는 **AuthenticateAsync** 에서 메서드는 [기본 인증](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/BasicAuthentication/ReadMe.txt) 샘플.</span><span class="sxs-lookup"><span data-stu-id="354ad-180">The follow code shows the **AuthenticateAsync** method from the [Basic Authentication](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/BasicAuthentication/ReadMe.txt) sample.</span></span> <span data-ttu-id="354ad-181">주석은 각 단계를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-181">The comments indicate each step.</span></span> <span data-ttu-id="354ad-182">코드는 여러 유형의 오류를 보여 줍니다: 없고 자격 증명, 잘못 된 형식의 자격 증명이 잘못 된 사용자 이름/암호는 인증 헤더.</span><span class="sxs-lookup"><span data-stu-id="354ad-182">The code shows several types of error: An Authorization header with no credentials, malformed credentials, and bad username/password.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample5.cs)]

## <a name="setting-an-error-result"></a><span data-ttu-id="354ad-183">오류 결과 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-183">Setting an Error Result</span></span>

<span data-ttu-id="354ad-184">필터는 자격 증명이 유효 하는 경우 설정 해야 `context.ErrorResult` 에 **IHttpActionResult** 를 만드는 오류 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-184">If the credentials are invalid, the filter must set `context.ErrorResult` to an **IHttpActionResult** that creates an error response.</span></span> <span data-ttu-id="354ad-185">에 대 한 자세한 내용은 **IHttpActionResult**, 참조 [Web API 2에 대 한 작업 결과](../getting-started-with-aspnet-web-api/action-results.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-185">For more information about **IHttpActionResult**, see [Action Results in Web API 2](../getting-started-with-aspnet-web-api/action-results.md).</span></span>

<span data-ttu-id="354ad-186">기본 인증 샘플에 포함 되어는 `AuthenticationFailureResult` 이 목적을 위해 적합 한 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-186">The Basic Authentication sample includes an `AuthenticationFailureResult` class that is suitable for this purpose.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample6.cs)]

## <a name="implementing-challengeasync"></a><span data-ttu-id="354ad-187">ChallengeAsync 구현</span><span class="sxs-lookup"><span data-stu-id="354ad-187">Implementing ChallengeAsync</span></span>

<span data-ttu-id="354ad-188">용도 **ChallengeAsync** 방법은 필요한 경우 인증 챌린지를 응답에 추가 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-188">The purpose of the **ChallengeAsync** method is to add authentication challenges to the response, if needed.</span></span> <span data-ttu-id="354ad-189">메서드 시그니처는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-189">Here is the method signature:</span></span>

[!code-csharp[Main](authentication-filters/samples/sample7.cs)]

<span data-ttu-id="354ad-190">요청 파이프라인의 모든 인증 필터에 메서드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-190">The method is called on every authentication filter in the request pipeline.</span></span>

<span data-ttu-id="354ad-191">이러한 점을 이해 해야 **ChallengeAsync** 라고 *하기 전에* HTTP 응답을 만들고, 컨트롤러 동작 실행 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-191">It's important to understand that **ChallengeAsync** is called *before* the HTTP response is created, and possibly even before the controller action runs.</span></span> <span data-ttu-id="354ad-192">때 **ChallengeAsync** 호출 `context.Result` 포함는 **IHttpActionResult**, HTTP 응답을 만드는 나중에 사용 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-192">When **ChallengeAsync** is called, `context.Result` contains an **IHttpActionResult**, which is used later to create the HTTP response.</span></span> <span data-ttu-id="354ad-193">따라서 **ChallengeAsync** 는 호출을 알 수 없는 HTTP 응답에 대해 아직 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-193">So when **ChallengeAsync** is called, you don't know anything about the HTTP response yet.</span></span> <span data-ttu-id="354ad-194">**ChallengeAsync** 메서드의 원래 값을 대체 해야 `context.Result` 를 새 **IHttpActionResult**합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-194">The **ChallengeAsync** method should replace the original value of `context.Result` with a new **IHttpActionResult**.</span></span> <span data-ttu-id="354ad-195">이 **IHttpActionResult** 원래 래핑해야 `context.Result`합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-195">This **IHttpActionResult** must wrap the original `context.Result`.</span></span>

![](authentication-filters/_static/image3.png)

<span data-ttu-id="354ad-196">원래 이라고 부르겠습니다 **IHttpActionResult** 는 *내부 결과*와 새 **IHttpActionResult** 는 *외부 결과*합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-196">I'll call the original **IHttpActionResult** the *inner result*, and the new **IHttpActionResult** the *outer result*.</span></span> <span data-ttu-id="354ad-197">외부 결과 다음을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-197">The outer result must do the following:</span></span>

1. <span data-ttu-id="354ad-198">HTTP 응답을 만드는 내부 결과 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-198">Invoke the inner result to create the HTTP response.</span></span>
2. <span data-ttu-id="354ad-199">응답을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-199">Examine the response.</span></span>
3. <span data-ttu-id="354ad-200">필요에 따라 인증 챌린지를 응답에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-200">Add an authentication challenge to the response, if needed.</span></span>

<span data-ttu-id="354ad-201">다음 예제에서는 기본 인증 샘플에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-201">The following example is taken from the Basic Authentication sample.</span></span> <span data-ttu-id="354ad-202">정의 **IHttpActionResult** 외부 결과 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-202">It defines an **IHttpActionResult** for the outer result.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample8.cs)]

<span data-ttu-id="354ad-203">`InnerResult` 속성 내부에 저장 **IHttpActionResult**합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-203">The `InnerResult` property holds the inner **IHttpActionResult**.</span></span> <span data-ttu-id="354ad-204">`Challenge` 속성 Www 인증 헤더를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-204">The `Challenge` property represents a Www-Authentication header.</span></span> <span data-ttu-id="354ad-205">다음에 유의 **ExecuteAsync** 첫 번째로 호출 `InnerResult.ExecuteAsync` HTTP 응답을 만드는 다음 필요한 경우 챌린지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-205">Notice that **ExecuteAsync** first calls `InnerResult.ExecuteAsync` to create the HTTP response, and then adds the challenge if needed.</span></span>

<span data-ttu-id="354ad-206">챌린지를 추가 하기 전에 응답 코드를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-206">Check the response code before adding the challenge.</span></span> <span data-ttu-id="354ad-207">대부분 인증 스키마에만 챌린지를 추가할 경우 응답 401을 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-207">Most authentication schemes only add a challenge if the response is 401, as shown here.</span></span> <span data-ttu-id="354ad-208">그러나 일부 인증 스키마 성공 응답에 챌린지를 추가지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-208">However, some authentication schemes do add a challenge to a success response.</span></span> <span data-ttu-id="354ad-209">예를 들어 참조 [Negotiate](http://tools.ietf.org/html/rfc4559#section-5) (RFC 4559).</span><span class="sxs-lookup"><span data-stu-id="354ad-209">For example, see [Negotiate](http://tools.ietf.org/html/rfc4559#section-5) (RFC 4559).</span></span>

<span data-ttu-id="354ad-210">제공 된 `AddChallengeOnUnauthorizedResult` 클래스의 실제 코드 **ChallengeAsync** 은 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-210">Given the `AddChallengeOnUnauthorizedResult` class, the actual code in **ChallengeAsync** is simple.</span></span> <span data-ttu-id="354ad-211">방금 결과 만들어 하도록 `context.Result`합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-211">You just create the result and attach it to `context.Result`.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample9.cs)]

<span data-ttu-id="354ad-212">참고: 기본 인증 샘플 추상화이 논리 약간 확장 메서드에서 배치 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-212">Note: The Basic Authentication sample abstracts this logic a bit, by placing it in an extension method.</span></span>

## <a name="combining-authentication-filters-with-host-level-authentication"></a><span data-ttu-id="354ad-213">호스트 수준의 인증을 사용 하 여 인증 필터를 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-213">Combining Authentication Filters with Host-Level Authentication</span></span>

<span data-ttu-id="354ad-214">"호스트 수준" 인증은 (예: IIS), 호스트에서 수행 하는 인증 요청에 도달 Web API 프레임 워크 하기 전에입니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-214">"Host-level authentication" is authentication performed by the host (such as IIS), before the request reaches the Web API framework.</span></span>

<span data-ttu-id="354ad-215">대개 다음 응용 프로그램의 나머지 부분에 대 한 호스트 수준 인증을 사용 하도록 설정 하지만 Web API 컨트롤러에 대 한 사용 하지 않도록 설정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-215">Often, you may want to enable host-level authentication for the rest of your application, but disable it for your Web API controllers.</span></span> <span data-ttu-id="354ad-216">예를 들어 호스트 수준에서 폼 인증을 사용 하도록 설정 하지만 웹 API에 대 한 토큰 기반 인증을 사용 하는 일반적인 시나리오가입니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-216">For example, a typical scenario is to enable Forms Authentication at the host level, but use token-based authentication for Web API.</span></span>

<span data-ttu-id="354ad-217">Web API 파이프라인 내 호스트 수준의 인증을 사용 하지 않으려면 호출 `config.SuppressHostPrincipal()` 구성에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-217">To disable host-level authentication inside the Web API pipeline, call `config.SuppressHostPrincipal()` in your configuration.</span></span> <span data-ttu-id="354ad-218">이 인해 웹 API를 제거 하는 **IPrincipal** Web API 파이프라인이 입력 하는 모든 요청에서.</span><span class="sxs-lookup"><span data-stu-id="354ad-218">This causes Web API to remove the **IPrincipal** from any request that enters the Web API pipeline.</span></span> <span data-ttu-id="354ad-219">효과적으로 그 &quot;취소-인증&quot; 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="354ad-219">Effectively, it &quot;un-authenticates&quot; the request.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample10.cs)]

## <a name="additional-resources"></a><span data-ttu-id="354ad-220">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="354ad-220">Additional Resources</span></span>

<span data-ttu-id="354ad-221">[ASP.NET 웹 API 보안 필터가](https://msdn.microsoft.com/magazine/dn781361.aspx) (MSDN Magazine)</span><span class="sxs-lookup"><span data-stu-id="354ad-221">[ASP.NET Web API Security Filters](https://msdn.microsoft.com/magazine/dn781361.aspx) (MSDN Magazine)</span></span>
