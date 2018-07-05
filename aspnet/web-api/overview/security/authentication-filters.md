---
uid: web-api/overview/security/authentication-filters
title: ASP.NET Web API 2에서에서의 인증 필터 | Microsoft Docs
author: MikeWasson
description: 인증 필터를는 HTTP 요청을 인증 하는 구성 요소입니다. 인증 필터를 모두 지 원하는 web API 2 및 MVC 5 하지만 약간 다릅니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/25/2014
ms.topic: article
ms.assetid: b9882e53-b3ca-4def-89b0-322846973ccb
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/security/authentication-filters
msc.type: authoredcontent
ms.openlocfilehash: be2dcb246597f90ed7f00b2cf647b92e44aa254c
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37385679"
---
<a name="authentication-filters-in-aspnet-web-api-2"></a><span data-ttu-id="39fe2-104">ASP.NET Web API 2에서에서의 인증 필터</span><span class="sxs-lookup"><span data-stu-id="39fe2-104">Authentication Filters in ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="39fe2-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="39fe2-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="39fe2-106">인증 필터를는 HTTP 요청을 인증 하는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-106">An authentication filter is a component that authenticates an HTTP request.</span></span> <span data-ttu-id="39fe2-107">인증 필터를 모두 지 원하는 web API 2 및 MVC 5 있지만 필터 인터페이스에 대 한 명명 규칙에서 주로 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-107">Web API 2 and MVC 5 both support authentication filters, but they differ slightly, mostly in the naming conventions for the filter interface.</span></span> <span data-ttu-id="39fe2-108">이 항목에서는 Web API 인증 필터를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-108">This topic describes Web API authentication filters.</span></span>


<span data-ttu-id="39fe2-109">인증 필터 개별 컨트롤러 또는 작업에 대 한 인증 체계를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-109">Authentication filters let you set an authentication scheme for individual controllers or actions.</span></span> <span data-ttu-id="39fe2-110">이런 방식으로 앱 다른 HTTP 리소스에 대 한 다양 한 인증 메커니즘을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-110">That way, your app can support different authentication mechanisms for different HTTP resources.</span></span>

<span data-ttu-id="39fe2-111">이 문서에서는 코드에서 보여 드리 려 합니다 [기본 인증](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/BasicAuthentication/ReadMe.txt) 에서 샘플 [ http://aspnet.codeplex.com ](http://aspnet.codeplex.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-111">In this article, I'll show code from the [Basic Authentication](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/BasicAuthentication/ReadMe.txt) sample on [http://aspnet.codeplex.com](http://aspnet.codeplex.com).</span></span> <span data-ttu-id="39fe2-112">샘플에서는 HTTP 기본 액세스 인증 체계 (RFC 2617)를 구현 하는 인증 필터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-112">The sample shows an authentication filter that implements the HTTP Basic Access Authentication scheme (RFC 2617).</span></span> <span data-ttu-id="39fe2-113">필터 라는 클래스에서 구현 됩니다 `IdentityBasicAuthenticationAttribute`합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-113">The filter is implemented in a class named `IdentityBasicAuthenticationAttribute`.</span></span> <span data-ttu-id="39fe2-114">이 샘플에서는 코드의 모든 인증 필터를 작성 하는 방법을 설명 하는 부분적 으로만 소개 하지.</span><span class="sxs-lookup"><span data-stu-id="39fe2-114">I won't show all of the code from the sample, just the parts that illustrate how to write an authentication filter.</span></span>

## <a name="setting-an-authentication-filter"></a><span data-ttu-id="39fe2-115">인증 필터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-115">Setting an Authentication Filter</span></span>

<span data-ttu-id="39fe2-116">다른 필터와 마찬가지로 인증 필터는 적용 된 컨트롤러, 작업 별로 또는 전 세계 모든 Web API 컨트롤러를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-116">Like other filters, authentication filters can be applied per-controller, per-action, or globally to all Web API controllers.</span></span>

<span data-ttu-id="39fe2-117">컨트롤러에 인증 필터를 적용 하려면 필터 특성을 사용 하 여 컨트롤러 클래스를 데코 레이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-117">To apply an authentication filter to a controller, decorate the controller class with the filter attribute.</span></span> <span data-ttu-id="39fe2-118">다음 코드에서는 `[IdentityBasicAuthentication]` 모든 컨트롤러의 작업에 대 한 기본 인증을 사용 하도록 설정 하는 컨트롤러 클래스를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-118">The following code sets the `[IdentityBasicAuthentication]` filter on a controller class, which enables Basic Authentication for all of the controller's actions.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample1.cs)]

<span data-ttu-id="39fe2-119">하나의 작업에 필터를 적용할 필터를 사용 하 여 작업을 데코 레이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-119">To apply the filter to one action, decorate the action with the filter.</span></span> <span data-ttu-id="39fe2-120">다음 코드에서는 합니다 `[IdentityBasicAuthentication]` 컨트롤러의 필터링 `Post` 메서드.</span><span class="sxs-lookup"><span data-stu-id="39fe2-120">The following code sets the `[IdentityBasicAuthentication]` filter on the controller's `Post` method.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample2.cs)]

<span data-ttu-id="39fe2-121">모든 Web API 컨트롤러에 필터를 적용할 추가 **GlobalConfiguration.Filters**합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-121">To apply the filter to all Web API controllers, add it to **GlobalConfiguration.Filters**.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample3.cs)]

## <a name="implementing-a-web-api-authentication-filter"></a><span data-ttu-id="39fe2-122">웹 API 인증 필터를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-122">Implementing a Web API Authentication Filter</span></span>

<span data-ttu-id="39fe2-123">Web API 인증 필터 구현 된 [System.Web.Http.Filters.IAuthenticationFilter](https://msdn.microsoft.com/library/system.web.http.filters.iauthenticationfilter.aspx) 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-123">In Web API, authentication filters implement the [System.Web.Http.Filters.IAuthenticationFilter](https://msdn.microsoft.com/library/system.web.http.filters.iauthenticationfilter.aspx) interface.</span></span> <span data-ttu-id="39fe2-124">또한에서 상속 해야 **System.Attribute**특성으로 적용 하기 위해.</span><span class="sxs-lookup"><span data-stu-id="39fe2-124">They should also inherit from **System.Attribute**, in order to be applied as attributes.</span></span>

<span data-ttu-id="39fe2-125">합니다 **IAuthenticationFilter** 인터페이스에 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-125">The **IAuthenticationFilter** interface has two methods:</span></span>

- <span data-ttu-id="39fe2-126">**AuthenticateAsync** 있으면 요청에 자격 증명의 유효성을 검사 하 여 요청을 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-126">**AuthenticateAsync** authenticates the request by validating credentials in the request, if present.</span></span>
- <span data-ttu-id="39fe2-127">**ChallengeAsync** 필요한 경우 인증 챌린지를 HTTP 응답에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-127">**ChallengeAsync** adds an authentication challenge to the HTTP response, if needed.</span></span>

<span data-ttu-id="39fe2-128">에 정의 된 인증 흐름에 해당 하는 이러한 메서드 [RFC 2612](http://tools.ietf.org/html/rfc2616) 하 고 [RFC 2617](http://tools.ietf.org/html/rfc2617):</span><span class="sxs-lookup"><span data-stu-id="39fe2-128">These methods correspond to the authentication flow defined in [RFC 2612](http://tools.ietf.org/html/rfc2616) and [RFC 2617](http://tools.ietf.org/html/rfc2617):</span></span>

1. <span data-ttu-id="39fe2-129">클라이언트 자격 증명 권한 부여 헤더를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-129">The client sends credentials in the Authorization header.</span></span> <span data-ttu-id="39fe2-130">이 문제는 일반적으로 클라이언트가 서버에서 401 (권한 없음된) 응답을 받으면 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-130">This typically happens after the client receives a 401 (Unauthorized) response from the server.</span></span> <span data-ttu-id="39fe2-131">그러나 클라이언트는 401 가져오기 후 뿐 아니라 모든 요청과 함께 자격 증명을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-131">However, a client can send credentials with any request, not just after getting a 401.</span></span>
2. <span data-ttu-id="39fe2-132">서버 자격 증명을 허용 하지 않는 경우 401 (권한 없음된) 응답을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-132">If the server does not accept the credentials, it returns a 401 (Unauthorized) response.</span></span> <span data-ttu-id="39fe2-133">응답에는 하나 이상의 문제를 포함 하는 Www-authenticate 헤더가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-133">The response includes a Www-Authenticate header that contains one or more challenges.</span></span> <span data-ttu-id="39fe2-134">각 문제는 서버에서 인식 하는 인증 체계를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-134">Each challenge specifies an authentication scheme recognized by the server.</span></span>

<span data-ttu-id="39fe2-135">서버는 익명 요청에 401을 반환할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-135">The server can also return 401 from an anonymous request.</span></span> <span data-ttu-id="39fe2-136">사실, 일반적으로 이것은 인증 프로세스를 시작 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-136">In fact, that's typically how the authentication process is initiated:</span></span>

1. <span data-ttu-id="39fe2-137">클라이언트는 익명 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-137">The client sends an anonymous request.</span></span>
2. <span data-ttu-id="39fe2-138">서버 401을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-138">The server returns 401.</span></span>
3. <span data-ttu-id="39fe2-139">클라이언트 자격 증명을 사용 하 여 요청을 다시 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-139">The clients resends the request with credentials.</span></span>

<span data-ttu-id="39fe2-140">이 흐름 모두 포함 *인증* 하 고 *권한 부여* 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-140">This flow includes both *authentication* and *authorization* steps.</span></span>

- <span data-ttu-id="39fe2-141">클라이언트의 id를 증명 하는 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-141">Authentication proves the identity of the client.</span></span>
- <span data-ttu-id="39fe2-142">권한 부여는 클라이언트가 특정 리소스에 액세스할 수 있는지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-142">Authorization determines whether the client can access a particular resource.</span></span>

<span data-ttu-id="39fe2-143">Web API에서 인증 필터 처리 인증을 지원 하지만 권한 부여 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-143">In Web API, authentication filters handle authentication, but not authorization.</span></span> <span data-ttu-id="39fe2-144">권한 부여 필터 또는 내부 컨트롤러 작업 권한 부여 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-144">Authorization should be done by an authorization filter or inside the controller action.</span></span>

<span data-ttu-id="39fe2-145">Web API 2 파이프라인의 흐름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-145">Here is the flow in the Web API 2 pipeline:</span></span>

1. <span data-ttu-id="39fe2-146">작업을 호출 하기 전에 Web API는 해당 작업에 대 한 인증 필터의 목록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-146">Before invoking an action, Web API creates a list of the authentication filters for that action.</span></span> <span data-ttu-id="39fe2-147">이 동작 범위, 컨트롤러 범위 및 전역 범위를 사용 하 여 필터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-147">This includes filters with action scope, controller scope, and global scope.</span></span>
2. <span data-ttu-id="39fe2-148">웹 API 호출 **AuthenticateAsync** 목록의 모든 필터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-148">Web API calls **AuthenticateAsync** on every filter in the list.</span></span> <span data-ttu-id="39fe2-149">각 필터는 요청에 자격 증명 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-149">Each filter can validate credentials in the request.</span></span> <span data-ttu-id="39fe2-150">필터에서 만드는 모든 필터 성공적으로 자격 증명의 유효성을 검사 합니다는 **IPrincipal** 요청에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-150">If any filter successfully validates credentials, the filter creates an **IPrincipal** and attaches it to the request.</span></span> <span data-ttu-id="39fe2-151">필터 오류가 시점에서 트리거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-151">A filter can also trigger an error at this point.</span></span> <span data-ttu-id="39fe2-152">그렇다면 나머지 파이프라인 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-152">If so, the rest of the pipeline does not run.</span></span>
3. <span data-ttu-id="39fe2-153">요청은 파이프라인의 rest를 통해 흐름 오류가 없는 것으로 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-153">Assuming there is no error, the request flows through the rest of the pipeline.</span></span>
4. <span data-ttu-id="39fe2-154">마지막으로 Web API 호출 마다 인증 필터 **ChallengeAsync** 메서드.</span><span class="sxs-lookup"><span data-stu-id="39fe2-154">Finally, Web API calls every authentication filter's **ChallengeAsync** method.</span></span> <span data-ttu-id="39fe2-155">필요한 경우 응답에 챌린지를 추가 하려면이 메서드를 사용 하는 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-155">Filters use this method to add a challenge to the response, if needed.</span></span> <span data-ttu-id="39fe2-156">일반적으로 (항상 그렇지는 않지만)는 에서처럼 발생 401 오류에 대 한 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-156">Typically (but not always) that would happen in response to a 401 error.</span></span>

<span data-ttu-id="39fe2-157">다음 다이어그램은 두 가지 가능한 경우를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-157">The following diagrams show two possible cases.</span></span> <span data-ttu-id="39fe2-158">첫 번째에서 인증 필터는 요청을 성공적으로 인증, 권한 부여 필터는 요청에 권한을 부여 하 고 컨트롤러 작업 200 (정상)를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-158">In the first, the authentication filter successfully authenticates the request, an authorization filter authorizes the request, and the controller action returns 200 (OK).</span></span>

![](authentication-filters/_static/image1.png)

<span data-ttu-id="39fe2-159">두 번째 예제에서는 요청을 인증 하는 인증 필터는 있지만 권한 부여 필터를 401 (권한 없음)를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-159">In the second example, the authentication filter authenticates the request, but the authorization filter returns 401 (Unauthorized).</span></span> <span data-ttu-id="39fe2-160">이 경우 컨트롤러 작업이 호출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-160">In this case, the controller action is not invoked.</span></span> <span data-ttu-id="39fe2-161">인증 필터를 응답에 Www-authenticate 헤더를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-161">The authentication filter adds a Www-Authenticate header to the response.</span></span>

![](authentication-filters/_static/image2.png)

<span data-ttu-id="39fe2-162">다른 조합은 가능&mdash;예를 들어, 익명 요청을 허용 하는 컨트롤러 작업을 할 경우 인증 필터를 있지만 권한이 부여 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-162">Other combinations are possible&mdash;for example, if the controller action allows anonymous requests, you might have an authentication filter but no authorization.</span></span>

## <a name="implementing-the-authenticateasync-method"></a><span data-ttu-id="39fe2-163">AuthenticateAsync 메서드 구현</span><span class="sxs-lookup"><span data-stu-id="39fe2-163">Implementing the AuthenticateAsync Method</span></span>

<span data-ttu-id="39fe2-164">합니다 **AuthenticateAsync** 메서드 요청을 인증 하려고 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-164">The **AuthenticateAsync** method tries to authenticate the request.</span></span> <span data-ttu-id="39fe2-165">메서드 시그니처는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-165">Here is the method signature:</span></span>

[!code-csharp[Main](authentication-filters/samples/sample4.cs)]

<span data-ttu-id="39fe2-166">합니다 **AuthenticateAsync** 메서드 중 하나를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-166">The **AuthenticateAsync** method must do one of the following:</span></span>

1. <span data-ttu-id="39fe2-167">Nothing (작동 하지 않습니다).</span><span class="sxs-lookup"><span data-stu-id="39fe2-167">Nothing (no-op).</span></span>
2. <span data-ttu-id="39fe2-168">만들기는 **IPrincipal** 요청에 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-168">Create an **IPrincipal** and set it on the request.</span></span>
3. <span data-ttu-id="39fe2-169">오류 결과 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-169">Set an error result.</span></span>

<span data-ttu-id="39fe2-170">요청 필터를 이해 하는 모든 자격 증명이 (1)은 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-170">Option (1) means the request did not have any credentials that the filter understands.</span></span> <span data-ttu-id="39fe2-171">옵션 (2) 이면 필터에서 요청을 성공적으로 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-171">Option (2) means the filter successfully authenticated the request.</span></span> <span data-ttu-id="39fe2-172">요청 옵션 (3) 의미 오류 응답을 트리거하는 잘못 된 자격 증명 (예: 잘못 된 암호)를 했습니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-172">Option (3) means the request had invalid credentials (like the wrong password), which triggers an error response.</span></span>

<span data-ttu-id="39fe2-173">구현에 대 한 일반적인 개요는 다음과 같습니다 **AuthenticateAsync**합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-173">Here is a general outline for implementing **AuthenticateAsync**.</span></span>

1. <span data-ttu-id="39fe2-174">요청에 자격 증명을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-174">Look for credentials in the request.</span></span>
2. <span data-ttu-id="39fe2-175">자격 증명이 없는 경우 아무 작업도 수행 하 고 (아무)를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-175">If there are no credentials, do nothing and return (no-op).</span></span>
3. <span data-ttu-id="39fe2-176">자격 증명이 필터 인증 체계를 인식 하지 않습니다 하지만 아무 작업도 수행 하 고 (아무)를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-176">If there are credentials but the filter does not recognize the authentication scheme, do nothing and return (no-op).</span></span> <span data-ttu-id="39fe2-177">파이프라인에서 다른 필터 체계를 이해 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-177">Another filter in the pipeline might understand the scheme.</span></span>
4. <span data-ttu-id="39fe2-178">필터를 이해 하는 자격 증명의 경우 인증 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-178">If there are credentials that the filter understands, try to authenticate them.</span></span>
5. <span data-ttu-id="39fe2-179">자격 증명에 잘못 된 경우 설정 하 여 401 반환 `context.ErrorResult`합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-179">If the credentials are bad, return 401 by setting `context.ErrorResult`.</span></span>
6. <span data-ttu-id="39fe2-180">자격 증명에 유효한 경우 만들기는 **IPrincipal** 설정 `context.Principal`합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-180">If the credentials are valid, create an **IPrincipal** and set `context.Principal`.</span></span>

<span data-ttu-id="39fe2-181">다음 코드와 **AuthenticateAsync** 메서드에서 [기본 인증](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/BasicAuthentication/ReadMe.txt) 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-181">The follow code shows the **AuthenticateAsync** method from the [Basic Authentication](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/BasicAuthentication/ReadMe.txt) sample.</span></span> <span data-ttu-id="39fe2-182">주석은 각 단계를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-182">The comments indicate each step.</span></span> <span data-ttu-id="39fe2-183">코드는 여러 유형의 오류를 보여 줍니다: 없는 자격 증명, 잘못 된 자격 증명 및 잘못 된 사용자 이름/암호를 사용 하 여는 권한 부여 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-183">The code shows several types of error: An Authorization header with no credentials, malformed credentials, and bad username/password.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample5.cs)]

## <a name="setting-an-error-result"></a><span data-ttu-id="39fe2-184">오류 결과 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-184">Setting an Error Result</span></span>

<span data-ttu-id="39fe2-185">자격 증명이 잘못 된 경우에 필터를 설정 해야 합니다 `context.ErrorResult` 에 **IHttpActionResult** 오류 응답을 야기 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-185">If the credentials are invalid, the filter must set `context.ErrorResult` to an **IHttpActionResult** that creates an error response.</span></span> <span data-ttu-id="39fe2-186">에 대 한 자세한 내용은 **IHttpActionResult**를 참조 하십시오 [Web API 2에서 작업 결과](../getting-started-with-aspnet-web-api/action-results.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-186">For more information about **IHttpActionResult**, see [Action Results in Web API 2](../getting-started-with-aspnet-web-api/action-results.md).</span></span>

<span data-ttu-id="39fe2-187">기본 인증 샘플는 `AuthenticationFailureResult` 이 용도에 적합 한 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-187">The Basic Authentication sample includes an `AuthenticationFailureResult` class that is suitable for this purpose.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample6.cs)]

## <a name="implementing-challengeasync"></a><span data-ttu-id="39fe2-188">ChallengeAsync 구현</span><span class="sxs-lookup"><span data-stu-id="39fe2-188">Implementing ChallengeAsync</span></span>

<span data-ttu-id="39fe2-189">용도 **ChallengeAsync** 방법은 필요한 경우 인증 챌린지에 응답에 추가 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-189">The purpose of the **ChallengeAsync** method is to add authentication challenges to the response, if needed.</span></span> <span data-ttu-id="39fe2-190">메서드 시그니처는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-190">Here is the method signature:</span></span>

[!code-csharp[Main](authentication-filters/samples/sample7.cs)]

<span data-ttu-id="39fe2-191">메서드는 요청 파이프라인의 모든 인증 필터에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-191">The method is called on every authentication filter in the request pipeline.</span></span>

<span data-ttu-id="39fe2-192">알아야 하는 것 **ChallengeAsync** 라고 *하기 전에* 만들어지고 컨트롤러 작업 실행 되기 전에 HTTP 응답 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-192">It's important to understand that **ChallengeAsync** is called *before* the HTTP response is created, and possibly even before the controller action runs.</span></span> <span data-ttu-id="39fe2-193">때 **ChallengeAsync** 가 호출 `context.Result` 포함을 **IHttpActionResult**, HTTP 응답을 만들려면 나중에 사용 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-193">When **ChallengeAsync** is called, `context.Result` contains an **IHttpActionResult**, which is used later to create the HTTP response.</span></span> <span data-ttu-id="39fe2-194">있으므로 **ChallengeAsync** 는 호출을 알 수 없는 HTTP 응답에 대 한 아무 것도 아직 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-194">So when **ChallengeAsync** is called, you don't know anything about the HTTP response yet.</span></span> <span data-ttu-id="39fe2-195">합니다 **ChallengeAsync** 메서드는 원래 값으로 대체 해야 `context.Result` 새 **IHttpActionResult**합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-195">The **ChallengeAsync** method should replace the original value of `context.Result` with a new **IHttpActionResult**.</span></span> <span data-ttu-id="39fe2-196">이렇게 **IHttpActionResult** 원래 래핑해야 `context.Result`합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-196">This **IHttpActionResult** must wrap the original `context.Result`.</span></span>

![](authentication-filters/_static/image3.png)

<span data-ttu-id="39fe2-197">원래 라고 하겠습니다 **IHttpActionResult** 는 *내부 결과*, 및 새로운 **IHttpActionResult** 합니다 *외부 결과*합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-197">I'll call the original **IHttpActionResult** the *inner result*, and the new **IHttpActionResult** the *outer result*.</span></span> <span data-ttu-id="39fe2-198">외부 결과 다음을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-198">The outer result must do the following:</span></span>

1. <span data-ttu-id="39fe2-199">HTTP 응답을 만드는 내부 결과 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-199">Invoke the inner result to create the HTTP response.</span></span>
2. <span data-ttu-id="39fe2-200">응답을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-200">Examine the response.</span></span>
3. <span data-ttu-id="39fe2-201">필요한 경우 인증 챌린지를 응답에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-201">Add an authentication challenge to the response, if needed.</span></span>

<span data-ttu-id="39fe2-202">다음 예제에서는 기본 인증 샘플에서 가져온 것입니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-202">The following example is taken from the Basic Authentication sample.</span></span> <span data-ttu-id="39fe2-203">정의 **IHttpActionResult** 외부 결과 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-203">It defines an **IHttpActionResult** for the outer result.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample8.cs)]

<span data-ttu-id="39fe2-204">합니다 `InnerResult` 속성 내부에 저장 **IHttpActionResult**합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-204">The `InnerResult` property holds the inner **IHttpActionResult**.</span></span> <span data-ttu-id="39fe2-205">`Challenge` 속성 Www 인증 헤더를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-205">The `Challenge` property represents a Www-Authentication header.</span></span> <span data-ttu-id="39fe2-206">있음을 **ExecuteAsync** 는 먼저 호출 `InnerResult.ExecuteAsync` HTTP 응답을 만들려면 다음 필요한 경우 문제를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-206">Notice that **ExecuteAsync** first calls `InnerResult.ExecuteAsync` to create the HTTP response, and then adds the challenge if needed.</span></span>

<span data-ttu-id="39fe2-207">챌린지를 추가 하기 전에 응답 코드를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-207">Check the response code before adding the challenge.</span></span> <span data-ttu-id="39fe2-208">대부분의 인증 체계에만 챌린지를 추가할 경우 다음과 같이 응답은 401입니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-208">Most authentication schemes only add a challenge if the response is 401, as shown here.</span></span> <span data-ttu-id="39fe2-209">그러나 일부 인증 체계 수행 성공 응답에 챌린지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-209">However, some authentication schemes do add a challenge to a success response.</span></span> <span data-ttu-id="39fe2-210">예를 들어, 참조 [Negotiate](http://tools.ietf.org/html/rfc4559#section-5) (RFC 4559).</span><span class="sxs-lookup"><span data-stu-id="39fe2-210">For example, see [Negotiate](http://tools.ietf.org/html/rfc4559#section-5) (RFC 4559).</span></span>

<span data-ttu-id="39fe2-211">지정 된 `AddChallengeOnUnauthorizedResult` 클래스의 실제 코드 **ChallengeAsync** 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-211">Given the `AddChallengeOnUnauthorizedResult` class, the actual code in **ChallengeAsync** is simple.</span></span> <span data-ttu-id="39fe2-212">에 연결을 하면 결과 만들고 `context.Result`합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-212">You just create the result and attach it to `context.Result`.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample9.cs)]

<span data-ttu-id="39fe2-213">참고: 기본 인증 예제는 확장 메서드를 배치 하 여 약간이 논리를 추상화 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-213">Note: The Basic Authentication sample abstracts this logic a bit, by placing it in an extension method.</span></span>

## <a name="combining-authentication-filters-with-host-level-authentication"></a><span data-ttu-id="39fe2-214">호스트 수준 인증을 사용 하 여 인증 필터를 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-214">Combining Authentication Filters with Host-Level Authentication</span></span>

<span data-ttu-id="39fe2-215">"호스트 수준 인증"는 요청에 도달 하면 Web API 프레임 워크를 하기 전에 (예: IIS) 호스트에서 수행 하는 인증입니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-215">"Host-level authentication" is authentication performed by the host (such as IIS), before the request reaches the Web API framework.</span></span>

<span data-ttu-id="39fe2-216">대개 다음 응용 프로그램의 나머지 부분에 대 한 호스트 수준 인증을 사용 하도록 설정 하면 Web API 컨트롤러에 대 한 사용 하지 않도록 설정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-216">Often, you may want to enable host-level authentication for the rest of your application, but disable it for your Web API controllers.</span></span> <span data-ttu-id="39fe2-217">예를 들어, 호스트 수준에서 폼 인증을 사용 하도록 설정 하지만 웹 API에 대 한 토큰 기반 인증을 사용 하는 일반적인 시나리오가입니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-217">For example, a typical scenario is to enable Forms Authentication at the host level, but use token-based authentication for Web API.</span></span>

<span data-ttu-id="39fe2-218">Web API 파이프라인 내에서 호스트 수준 인증을 사용 하지 않으려면 호출 `config.SuppressHostPrincipal()` 구성에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-218">To disable host-level authentication inside the Web API pipeline, call `config.SuppressHostPrincipal()` in your configuration.</span></span> <span data-ttu-id="39fe2-219">이렇게 하면 Web API를 제거 하는 **IPrincipal** Web API 파이프라인을 입력 하는 모든 요청에서.</span><span class="sxs-lookup"><span data-stu-id="39fe2-219">This causes Web API to remove the **IPrincipal** from any request that enters the Web API pipeline.</span></span> <span data-ttu-id="39fe2-220">이 사실상 &quot;취소-인증&quot; 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="39fe2-220">Effectively, it &quot;un-authenticates&quot; the request.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample10.cs)]

## <a name="additional-resources"></a><span data-ttu-id="39fe2-221">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="39fe2-221">Additional Resources</span></span>

<span data-ttu-id="39fe2-222">[ASP.NET 웹 API 보안 필터가](https://msdn.microsoft.com/magazine/dn781361.aspx) (MSDN Magazine)</span><span class="sxs-lookup"><span data-stu-id="39fe2-222">[ASP.NET Web API Security Filters](https://msdn.microsoft.com/magazine/dn781361.aspx) (MSDN Magazine)</span></span>
