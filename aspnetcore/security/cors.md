---
title: ASP.NET Core에서 원본 간 요청 (CORS)를 사용 하도록 설정
author: rick-anderson
description: 에 대해 알아봅니다 어떻게 CORS 허용 하거나 거부 하는 ASP.NET Core 앱에서 크로스-원본 요청에 대 한 표준으로 합니다.
ms.author: riande
ms.date: 08/17/2018
uid: security/cors
ms.openlocfilehash: 0dbb7933c76bb0d1d0cab519ea08c6c8f0ebedfd
ms.sourcegitcommit: 64c2ca86fff445944b155635918126165ee0f8aa
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2018
ms.locfileid: "41828625"
---
# <a name="enable-cross-origin-requests-cors-in-aspnet-core"></a><span data-ttu-id="8ca8c-103">ASP.NET Core에서 원본 간 요청 (CORS)를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="8ca8c-103">Enable Cross-Origin Requests (CORS) in ASP.NET Core</span></span>

<span data-ttu-id="8ca8c-104">작성자: [Mike Wasson](https://github.com/mikewasson), [Shayne Boyer](https://twitter.com/spboyer), 및 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="8ca8c-104">By [Mike Wasson](https://github.com/mikewasson), [Shayne Boyer](https://twitter.com/spboyer), and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="8ca8c-105">브라우저의 보안 기능은 웹 페이지에서 다른 도메인으로 AJAX 요청을 전송하는 것을 막습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-105">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="8ca8c-106">이 제약 사항을 *동일 원본 정책(Same-Origin Policy)* 이라고 부르며, 악의적인 사이트가 다른 사이트의 민감한 데이터를 무차별적으로 읽는 것을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-106">This restriction is called the *same-origin policy*, and prevents a malicious site from reading sensitive data from another site.</span></span> <span data-ttu-id="8ca8c-107">그러나 경우에 따라서는 다른 사이트가 여러분의 Web API에 교차 원본 요청(Cross-Origin Requests)을 전송하는 것을 허용해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-107">However, sometimes you might want to let other sites make cross-origin requests to your web API.</span></span>

<span data-ttu-id="8ca8c-108">[교차 원본 자원 공유](http://www.w3.org/TR/cors/) (CORS, Cross Origin Resource Sharing)는 서버 측에서 동일 원본 정책을 완화할 수 있게 해주는 W3C 표준입니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-108">[Cross Origin Resource Sharing](http://www.w3.org/TR/cors/) (CORS) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="8ca8c-109">CORS를 사용하면 서버가 명시적으로 특정 교차 원본 요청만 허용하고, 다른 요청은 거부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-109">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span> <span data-ttu-id="8ca8c-110">CORS는 [JSONP](https://wikipedia.org/wiki/JSONP) 같은 기존의 다른 기술보다 안전하고 유연합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-110">CORS is safer and more flexible than earlier techniques such as [JSONP](https://wikipedia.org/wiki/JSONP).</span></span> <span data-ttu-id="8ca8c-111">본문에서는 ASP.NET Core 응용 프로그램에서 CORS를 활성화시키는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-111">This topic shows how to enable CORS in an ASP.NET Core application.</span></span>

## <a name="what-is-same-origin"></a><span data-ttu-id="8ca8c-112">"동일 원본"이란?</span><span class="sxs-lookup"><span data-stu-id="8ca8c-112">What is "same origin"?</span></span>

<span data-ttu-id="8ca8c-113">두 URL의 스키마, 호스트 및 포트가 모두 동일한 경우, 두 URL의 원본이 동일하다고 말합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-113">Two URLs have the same origin if they have identical schemes, hosts, and ports.</span></span> <span data-ttu-id="8ca8c-114">([RFC 6454](http://tools.ietf.org/html/rfc6454))</span><span class="sxs-lookup"><span data-stu-id="8ca8c-114">([RFC 6454](http://tools.ietf.org/html/rfc6454))</span></span>

<span data-ttu-id="8ca8c-115">다음 두 URL은 동일한 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-115">These two URLs have the same origin:</span></span>

* `http://example.com/foo.html`

* `http://example.com/bar.html`

<span data-ttu-id="8ca8c-116">반면, 다음 URL들은 위의 두 URL과는 다른 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-116">These URLs have different origins than the previous two:</span></span>

* <span data-ttu-id="8ca8c-117">`http://example.net` -도메인이 다릅니다</span><span class="sxs-lookup"><span data-stu-id="8ca8c-117">`http://example.net` - Different domain</span></span>

* <span data-ttu-id="8ca8c-118">`http://www.example.com/foo.html` -하위 도메인이 다릅니다</span><span class="sxs-lookup"><span data-stu-id="8ca8c-118">`http://www.example.com/foo.html` - Different subdomain</span></span>

* <span data-ttu-id="8ca8c-119">`https://example.com/foo.html` -스키마가 다릅니다</span><span class="sxs-lookup"><span data-stu-id="8ca8c-119">`https://example.com/foo.html` - Different scheme</span></span>

* <span data-ttu-id="8ca8c-120">`http://example.com:9000/foo.html` -포트가 다릅니다</span><span class="sxs-lookup"><span data-stu-id="8ca8c-120">`http://example.com:9000/foo.html` - Different port</span></span>

> [!NOTE]
> <span data-ttu-id="8ca8c-121">Internet Explorer는 원본을 비교할 때 포트를 고려하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-121">Internet Explorer doesn't consider the port when comparing origins.</span></span>

## <a name="enable-cors"></a><span data-ttu-id="8ca8c-122">CORS를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="8ca8c-122">Enable CORS</span></span>

::: moniker range="<= aspnetcore-1.1"

<span data-ttu-id="8ca8c-123">ASP.NET Core 응용 프로그램에 CORS를 설정하려면 프로젝트에 `Microsoft.AspNetCore.Cors` 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-123">To set up CORS for your application add the `Microsoft.AspNetCore.Cors` package to your project.</span></span>

::: moniker-end

<span data-ttu-id="8ca8c-124">호출 [AddCors](/dotnet/api/microsoft.extensions.dependencyinjection.corsservicecollectionextensions.addcors) 에서 `Startup.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="8ca8c-124">Call [AddCors](/dotnet/api/microsoft.extensions.dependencyinjection.corsservicecollectionextensions.addcors) in `Startup.ConfigureServices`:</span></span>

[!code-csharp[](cors/sample/CorsExample1/Startup.cs?name=snippet_addcors)]

## <a name="enabling-cors-with-middleware"></a><span data-ttu-id="8ca8c-125">미들웨어를 이용해서 CORS 활성화시키기</span><span class="sxs-lookup"><span data-stu-id="8ca8c-125">Enabling CORS with middleware</span></span>

<span data-ttu-id="8ca8c-126">CORS를 사용 하도록 하 여 요청 파이프라인에 CORS 미들웨어를 추가 합니다 `UseCors` 확장 메서드.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-126">To enable CORS, add the CORS middleware to the request pipeline using the `UseCors` extension method.</span></span> <span data-ttu-id="8ca8c-127">CORS 미들웨어 앞에 야 정의 된 끝점이 모든 앱에서 크로스-원본 요청을 지원 하려면 (예를 들어 호출 하기 전에 `UseMvc`).</span><span class="sxs-lookup"><span data-stu-id="8ca8c-127">The CORS middleware must precede any defined endpoints in your app where you want to support cross-origin requests (For example, before any call to `UseMvc`).</span></span>

<span data-ttu-id="8ca8c-128">크로스-원본 정책을 사용 하 여 CORS 미들웨어를 추가할 때 지정할 수는 [CorsPolicyBuilder](/dotnet/api/microsoft.extensions.dependencyinjection.corsservicecollectionextensions.addcors) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-128">A cross-origin policy can be specified when adding the CORS middleware using the [CorsPolicyBuilder](/dotnet/api/microsoft.extensions.dependencyinjection.corsservicecollectionextensions.addcors) class.</span></span> <span data-ttu-id="8ca8c-129">구체적인 방법은 두 가지입니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-129">There are two ways to do this.</span></span> <span data-ttu-id="8ca8c-130">첫 번째 호출 방법은 `UseCors` 람다를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="8ca8c-130">The first is to call `UseCors` with a lambda:</span></span>

[!code-csharp[](cors/sample/CorsExample1/Startup.cs?highlight=11,12&range=22-38)]

<span data-ttu-id="8ca8c-131">**참고:** 반드시 후행 슬래시`/`가 없는 URL을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-131">**Note:** The URL must be specified without a trailing slash (`/`).</span></span> <span data-ttu-id="8ca8c-132">만약 URL이 `/` 로 끝나면, 비교 결과가 `false` 를 반환하여 아무런 헤더도 반환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-132">If the URL terminates with `/`, the comparison will return `false` and no header will be returned.</span></span>

<span data-ttu-id="8ca8c-133">람다는 `CorsPolicyBuilder` 개체를 전달받습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-133">The lambda takes a `CorsPolicyBuilder` object.</span></span> <span data-ttu-id="8ca8c-134">[구성 옵션](#cors-policy-options) 의 목록은 잠시 후 다시 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-134">You'll find a list of the [configuration options](#cors-policy-options) later in this topic.</span></span> <span data-ttu-id="8ca8c-135">이 예제 코드의 정책은 `http://example.com` 에서 전달된 교차 원본 요청은 허용하지만, 다른 원본의 요청은 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-135">In this example, the policy allows cross-origin requests from `http://example.com` and no other origins.</span></span>

<span data-ttu-id="8ca8c-136">다음과 같이 CorsPolicyBuilder fluent API에 있으므로 메서드 호출을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-136">CorsPolicyBuilder has a fluent API, so you can chain method calls:</span></span>

[!code-csharp[](../security/cors/sample/CorsExample3/Startup.cs?highlight=3&range=29-32)]

<span data-ttu-id="8ca8c-137">두 번째 방법은 미리 한 가지 이상의 명명된 CORS 정책을 정의한 다음, 런타임 시에 이름을 지정해서 정책을 선택하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-137">The second approach is to define one or more named CORS policies, and then select the policy by name at run time.</span></span>

[!code-csharp[](cors/sample/CorsExample2/Startup.cs?name=snippet_begin)]

<span data-ttu-id="8ca8c-138">이 예제는 "AllowSpecificOrigin"이라는 CORS 정책을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-138">This example adds a CORS policy named "AllowSpecificOrigin".</span></span> <span data-ttu-id="8ca8c-139">그리고 `UseCors` 메서드에 이름을 전달해서 정책을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-139">To select the policy, pass the name to `UseCors`.</span></span>

## <a name="enabling-cors-in-mvc"></a><span data-ttu-id="8ca8c-140">MVC에서 CORS 활성화시키기</span><span class="sxs-lookup"><span data-stu-id="8ca8c-140">Enabling CORS in MVC</span></span>

<span data-ttu-id="8ca8c-141">MVC를 이용해서 액션별, 컨트롤러별 또는 모든 컨트롤러에 대해 전역으로 특정 CORS를 적용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-141">You can alternatively use MVC to apply specific CORS per action, per controller, or globally for all controllers.</span></span> <span data-ttu-id="8ca8c-142">MVC를 이용해서 CORS를 활성화시키는 경우에도 동일한 CORS 서비스가 사용되지만, 이 경우 CORS 미들웨어는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-142">When using MVC to enable CORS the same CORS services are used, but the CORS middleware isn't.</span></span>

### <a name="per-action"></a><span data-ttu-id="8ca8c-143">액션 별</span><span class="sxs-lookup"><span data-stu-id="8ca8c-143">Per action</span></span>

<span data-ttu-id="8ca8c-144">특정 액션에 CORS 정책을 지정하려면 해당 액션에 `[EnableCors]` 특성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-144">To specify a CORS policy for a specific action add the `[EnableCors]` attribute to the action.</span></span> <span data-ttu-id="8ca8c-145">이때 정책 이름을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-145">Specify the policy name.</span></span>

[!code-csharp[](cors/sample/CorsMVC/Controllers/ValuesController.cs?name=EnableOnAction)]

### <a name="per-controller"></a><span data-ttu-id="8ca8c-146">컨트롤러 별</span><span class="sxs-lookup"><span data-stu-id="8ca8c-146">Per controller</span></span>

<span data-ttu-id="8ca8c-147">특정 컨트롤러에 CORS 정책을 지정하려면 해당 컨트롤러에 `[EnableCors]` 특성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-147">To specify the CORS policy for a specific controller add the `[EnableCors]` attribute to the controller class.</span></span> <span data-ttu-id="8ca8c-148">이때 정책 이름을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-148">Specify the policy name.</span></span>

[!code-csharp[](cors/sample/CorsMVC/Controllers/ValuesController.cs?name=EnableOnController)]

### <a name="globally"></a><span data-ttu-id="8ca8c-149">전 세계</span><span class="sxs-lookup"><span data-stu-id="8ca8c-149">Globally</span></span>

<span data-ttu-id="8ca8c-150">모든 컨트롤러에서 전역으로 CORS를 활성화시키려면, 전역 필터 컬렉션에 `CorsAuthorizationFilterFactory` 필터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-150">You can enable CORS globally for all controllers by adding the `CorsAuthorizationFilterFactory` filter to the global filter collection:</span></span>

[!code-csharp[](cors/sample/CorsMVC/Startup2.cs?name=snippet_configureservices)]

<span data-ttu-id="8ca8c-151">특성의 우선 순위는 액션, 컨트롤러, 전역 순입니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-151">The precedence order is: Action, controller, global.</span></span> <span data-ttu-id="8ca8c-152">다시 말해서, 액션 수준 정책은 컨트롤러 수준 정책보다 우선하며, 컨트롤러 수준 정책은 전역 정책보다 우선합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-152">Action-level policies take precedence over controller-level policies, and controller-level policies take precedence over global policies.</span></span>

### <a name="disable-cors"></a><span data-ttu-id="8ca8c-153">CORS 비활성시키기</span><span class="sxs-lookup"><span data-stu-id="8ca8c-153">Disable CORS</span></span>

<span data-ttu-id="8ca8c-154">컨트롤러나 액션의 CORS를 비활성화시키려면, `[DisableCors]` 특성을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-154">To disable CORS for a controller or action, use the `[DisableCors]` attribute.</span></span>

[!code-csharp[](cors/sample/CorsMVC/Controllers/ValuesController.cs?name=DisableOnAction)]

## <a name="cors-policy-options"></a><span data-ttu-id="8ca8c-155">CORS 정책 옵션</span><span class="sxs-lookup"><span data-stu-id="8ca8c-155">CORS policy options</span></span>

<span data-ttu-id="8ca8c-156">이번 섹션에서는 CORS 정책에서 설정할 수 있는 다양한 옵션들을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-156">This section describes the various options that you can set in a CORS policy.</span></span>

* [<span data-ttu-id="8ca8c-157">허용되는 원본 설정하기</span><span class="sxs-lookup"><span data-stu-id="8ca8c-157">Set the allowed origins</span></span>](#set-the-allowed-origins)

* [<span data-ttu-id="8ca8c-158">허용되는 HTTP 메서드 설정하기</span><span class="sxs-lookup"><span data-stu-id="8ca8c-158">Set the allowed HTTP methods</span></span>](#set-the-allowed-http-methods)

* [<span data-ttu-id="8ca8c-159">허용되는 요청 헤더 설정하기</span><span class="sxs-lookup"><span data-stu-id="8ca8c-159">Set the allowed request headers</span></span>](#set-the-allowed-request-headers)

* [<span data-ttu-id="8ca8c-160">노출되는 응답 헤더 설정하기</span><span class="sxs-lookup"><span data-stu-id="8ca8c-160">Set the exposed response headers</span></span>](#set-the-exposed-response-headers)

* [<span data-ttu-id="8ca8c-161">교차 원본 요청의 자격 증명</span><span class="sxs-lookup"><span data-stu-id="8ca8c-161">Credentials in cross-origin requests</span></span>](#credentials-in-cross-origin-requests)

* [<span data-ttu-id="8ca8c-162">예비 요청 만료 시간 설정하기</span><span class="sxs-lookup"><span data-stu-id="8ca8c-162">Set the preflight expiration time</span></span>](#set-the-preflight-expiration-time)

<span data-ttu-id="8ca8c-163">일부 옵션에 대 한 읽기 하면 도움이 될 [CORS 어떻게 작동](#how-cors-works) 첫 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-163">For some options, it may be helpful to read [How CORS works](#how-cors-works) first.</span></span>

### <a name="set-the-allowed-origins"></a><span data-ttu-id="8ca8c-164">허용되는 원본 설정하기</span><span class="sxs-lookup"><span data-stu-id="8ca8c-164">Set the allowed origins</span></span>

<span data-ttu-id="8ca8c-165">하나 이상의 특정 원본을 허용하려면 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-165">To allow one or more specific origins:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=19-23)]

<span data-ttu-id="8ca8c-166">모든 원본을 허용하려면 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-166">To allow all origins:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs??range=27-31)]

<span data-ttu-id="8ca8c-167">모든 원본의 요청을 허용하기 전에 신중히 고민하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-167">Consider carefully before allowing requests from any origin.</span></span> <span data-ttu-id="8ca8c-168">이는 문자 그대로 모든 웹 사이트에서 응용 프로그램에 AJAX 호출을 전송할 수 있음을 뜻합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-168">It means that literally any website can make AJAX calls to your API.</span></span>

### <a name="set-the-allowed-http-methods"></a><span data-ttu-id="8ca8c-169">허용되는 HTTP 메서드 설정하기</span><span class="sxs-lookup"><span data-stu-id="8ca8c-169">Set the allowed HTTP methods</span></span>

<span data-ttu-id="8ca8c-170">모든 HTTP 메서드를 허용하려면 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-170">To allow all HTTP methods:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=44-49)]

<span data-ttu-id="8ca8c-171">이 옵션은 예비 요청과 Access-Control-Allow-Methods 헤더에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-171">This affects pre-flight requests and Access-Control-Allow-Methods header.</span></span>

### <a name="set-the-allowed-request-headers"></a><span data-ttu-id="8ca8c-172">허용되는 요청 헤더 설정하기</span><span class="sxs-lookup"><span data-stu-id="8ca8c-172">Set the allowed request headers</span></span>

<span data-ttu-id="8ca8c-173">CORS의 예비 요청에는 클라이언트 응용 프로그램에서 설정한 HTTP 헤더들이 나열된 Access-Control-Request-Headers 헤더가 포함되어 있을 수 있습니다. 이를 일명 "사용자 지정 요청 헤더(Author Request Headers)"라고 부릅니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-173">A CORS preflight request might include an Access-Control-Request-Headers header, listing the HTTP headers set by the application (the so-called "author request headers").</span></span>

<span data-ttu-id="8ca8c-174">특정 헤더들에 대한 허용 목록을 만들려면 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-174">To whitelist specific headers:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=53-58)]

<span data-ttu-id="8ca8c-175">모든 사용자 지정 요청 헤더를 허용하려면 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-175">To allow all author request headers:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=62-67)]

<span data-ttu-id="8ca8c-176">브라우저가 Access-Control-Request-Headers를 설정하는 방법이 완전히 일관되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-176">Browsers are not entirely consistent in how they set Access-Control-Request-Headers.</span></span> <span data-ttu-id="8ca8c-177">따라서, "\*" 이외의 값으로 헤더를 설정할 때는, 지원하고자 하는 모든 사용자 정의 헤더 외에도 최소한 "accept", "content-type" 및 "origin"은 포함시켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-177">If you set headers to anything other than "\*", you should include at least "accept", "content-type", and "origin", plus any custom headers that you want to support.</span></span>

### <a name="set-the-exposed-response-headers"></a><span data-ttu-id="8ca8c-178">노출되는 응답 헤더 설정하기</span><span class="sxs-lookup"><span data-stu-id="8ca8c-178">Set the exposed response headers</span></span>

<span data-ttu-id="8ca8c-179">기본적으로 브라우저는 클라이언트 응용 프로그램에 모든 응답 헤더를 노출하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-179">By default, the browser doesn't expose all of the response headers to the application.</span></span> <span data-ttu-id="8ca8c-180">(참조 [ http://www.w3.org/TR/cors/#simple-response-header ](http://www.w3.org/TR/cors/#simple-response-header).) 기본적으로 사용 가능한 응답 헤더들은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-180">(See [http://www.w3.org/TR/cors/#simple-response-header](http://www.w3.org/TR/cors/#simple-response-header).) The response headers that are available by default are:</span></span>

* <span data-ttu-id="8ca8c-181">캐시 제어</span><span class="sxs-lookup"><span data-stu-id="8ca8c-181">Cache-Control</span></span>

* <span data-ttu-id="8ca8c-182">콘텐츠 언어</span><span class="sxs-lookup"><span data-stu-id="8ca8c-182">Content-Language</span></span>

* <span data-ttu-id="8ca8c-183">콘텐츠 형식</span><span class="sxs-lookup"><span data-stu-id="8ca8c-183">Content-Type</span></span>

* <span data-ttu-id="8ca8c-184">Expires</span><span class="sxs-lookup"><span data-stu-id="8ca8c-184">Expires</span></span>

* <span data-ttu-id="8ca8c-185">Last-Modified</span><span class="sxs-lookup"><span data-stu-id="8ca8c-185">Last-Modified</span></span>

* <span data-ttu-id="8ca8c-186">Pragma</span><span class="sxs-lookup"><span data-stu-id="8ca8c-186">Pragma</span></span>

<span data-ttu-id="8ca8c-187">CORS 명세에서는 이 헤더들을 *단순 응답 헤더(Simple Response Header)* 라고 부릅니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-187">The CORS spec calls these *simple response headers*.</span></span> <span data-ttu-id="8ca8c-188">응용 프로그램에서 다른 헤더들을 사용할 수 있게 하려면 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-188">To make other headers available to the application:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=71-76)]

### <a name="credentials-in-cross-origin-requests"></a><span data-ttu-id="8ca8c-189">교차 원본 요청의 자격 증명</span><span class="sxs-lookup"><span data-stu-id="8ca8c-189">Credentials in cross-origin requests</span></span>

<span data-ttu-id="8ca8c-190">CORS 요청에서 자격 증명(Credentials)은 특별한 처리를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-190">Credentials require special handling in a CORS request.</span></span> <span data-ttu-id="8ca8c-191">교차 원본 요청 시, 기본적으로 브라우저는 어떠한 자격 증명도 전송하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-191">By default, the browser doesn't send any credentials with a cross-origin request.</span></span> <span data-ttu-id="8ca8c-192">여기에서 말하는 자격 증명에는 쿠키뿐만 아니라 HTTP 인증 스킴도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-192">Credentials include cookies as well as HTTP authentication schemes.</span></span> <span data-ttu-id="8ca8c-193">교차 원본 요청 시 자격 증명을 함께 전송하려면, 클라이언트에서 XMLHttpRequest.withCredentials 속성을 true로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-193">To send credentials with a cross-origin request, the client must set XMLHttpRequest.withCredentials to true.</span></span>

<span data-ttu-id="8ca8c-194">직접 XMLHttpRequest를 사용할 경우:</span><span class="sxs-lookup"><span data-stu-id="8ca8c-194">Using XMLHttpRequest directly:</span></span>

```javascript
var xhr = new XMLHttpRequest();
xhr.open('get', 'http://www.example.com/api/test');
xhr.withCredentials = true;
```

<span data-ttu-id="8ca8c-195">jQuery를 사용할 경우:</span><span class="sxs-lookup"><span data-stu-id="8ca8c-195">In jQuery:</span></span>

```jQuery
$.ajax({
  type: 'get',
  url: 'http://www.example.com/home',
  xhrFields: {
    withCredentials: true
}
```

<span data-ttu-id="8ca8c-196">또한 서버에서도 자격 증명을 허용해야만 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-196">In addition, the server must allow the credentials.</span></span> <span data-ttu-id="8ca8c-197">교차 원본 자격 증명을 허용하려면 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-197">To allow cross-origin credentials:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=80-85)]

<span data-ttu-id="8ca8c-198">이 구성이 적용되면 HTTP 응답에 Access-Control-Allow-Credentials 헤더가 포함됩니다. 이 헤더는 서버가 교차 원본 요청에 대한 자격 증명을 허용한다는 것을 브라우저에 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-198">Now the HTTP response will include an Access-Control-Allow-Credentials header, which tells the browser that the server allows credentials for a cross-origin request.</span></span>

<span data-ttu-id="8ca8c-199">브라우저가 자격 증명을 전송하지만, 응답에 유효한 Access-Control-Allow-Credentials 헤더가 포함되어 있지 않다면, 브라우저가 응용 프로그램에게 응답을 노출하지 않으므로 AJAX 요청은 실패하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-199">If the browser sends credentials, but the response doesn't include a valid Access-Control-Allow-Credentials header, the browser won't expose the response to the application, and the AJAX request fails.</span></span>

<span data-ttu-id="8ca8c-200">크로스-원본 자격 증명을 허용 하는 경우 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-200">Be careful when allowing cross-origin credentials.</span></span> <span data-ttu-id="8ca8c-201">다른 도메인에서 웹 사이트 사용자의 지식 없이 사용자를 대신 하 여 앱에 로그인 한 사용자의 자격 증명을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-201">A website at another domain can send a logged-in user's credentials to the app on the user's behalf without the user's knowledge.</span></span> <span data-ttu-id="8ca8c-202">CORS 사양도 해당 설정에 따라 원본이 `"*"` (모든 원본) 올바르지 않습니다 경우는 `Access-Control-Allow-Credentials` 헤더가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-202">The CORS specification also states that setting origins to `"*"` (all origins) is invalid if the `Access-Control-Allow-Credentials` header is present.</span></span>

### <a name="set-the-preflight-expiration-time"></a><span data-ttu-id="8ca8c-203">예비 요청 만료 시간 설정하기</span><span class="sxs-lookup"><span data-stu-id="8ca8c-203">Set the preflight expiration time</span></span>

<span data-ttu-id="8ca8c-204">Access-Control-Max-Age 헤더는 예비 요청에 대한 응답을 캐시할 수 있는 기간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-204">The Access-Control-Max-Age header specifies how long the response to the preflight request can be cached.</span></span> <span data-ttu-id="8ca8c-205">이 헤더를 설정하려면 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-205">To set this header:</span></span>

[!code-csharp[](cors/sample/CorsExample4/Startup.cs?range=89-94)]

<a name="cors-how-cors-works"></a>

## <a name="how-cors-works"></a><span data-ttu-id="8ca8c-206">CORS의 동작 방식</span><span class="sxs-lookup"><span data-stu-id="8ca8c-206">How CORS works</span></span>

<span data-ttu-id="8ca8c-207">이번 섹션에서는 CORS 요청 시 HTTP 메시지 수준에서 발생하는 일들을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-207">This section describes what happens in a CORS request at the level of the HTTP messages.</span></span> <span data-ttu-id="8ca8c-208">CORS 정책을 올바르게 구성 하 고 예기치 않은 동작이 발생 하는 경우 디버깅할 수 있도록 CORS의 작동 방식을 이해 하는 것이 반드시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-208">It's important to understand how CORS works so that the CORS policy can be configured correctly and debugged when unexpected behaviors occur.</span></span>

<span data-ttu-id="8ca8c-209">CORS 명세에서는 교차 원본 요청을 활성화시키기 위한 용도로 몇 가지 새로운 HTTP 헤더들이 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-209">The CORS specification introduces several new HTTP headers that enable cross-origin requests.</span></span> <span data-ttu-id="8ca8c-210">브라우저에서 CORS를 지 원하는 경우 이러한 머리글 크로스-원본 요청을 자동으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-210">If a browser supports CORS, it sets these headers automatically for cross-origin requests.</span></span> <span data-ttu-id="8ca8c-211">CORS를 사용 하도록 사용자 지정 JavaScript 코드 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-211">Custom JavaScript code isn't required to enable CORS.</span></span>

<span data-ttu-id="8ca8c-212">크로스-원본 요청 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-212">Here is an example of a cross-origin request.</span></span> <span data-ttu-id="8ca8c-213">`Origin` 헤더는 요청 하는 사이트의 도메인을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-213">The `Origin` header provides the domain of the site that's making the request:</span></span>

```
GET http://myservice.azurewebsites.net/api/test HTTP/1.1
Referer: http://myclient.azurewebsites.net/
Accept: */*
Accept-Language: en-US
Origin: http://myclient.azurewebsites.net
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; WOW64; Trident/6.0)
Host: myservice.azurewebsites.net
```

<span data-ttu-id="8ca8c-214">서버는 요청을 허용하는 경우에 한해서 Access-Control-Allow-Origin 헤더를 지정해서 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-214">If the server allows the request, it sets the Access-Control-Allow-Origin header in the response.</span></span> <span data-ttu-id="8ca8c-215">이 헤더의 값은 Origin 헤더 값과 동일하거나, 모든 원본이 허용됨을 뜻하는 와일드카드 값인 "\*" 이어야 합니다</span><span class="sxs-lookup"><span data-stu-id="8ca8c-215">The value of this header either matches the Origin header from the request, or is the wildcard value "\*", meaning that any origin is allowed:</span></span>

```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Type: text/plain; charset=utf-8
Access-Control-Allow-Origin: http://myclient.azurewebsites.net
Date: Wed, 20 May 2015 06:27:30 GMT
Content-Length: 12

Test message
```

<span data-ttu-id="8ca8c-216">응답에는 액세스 제어-허용-원본 헤더가 포함 되지 않은, AJAX 요청이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-216">If the response doesn't include the Access-Control-Allow-Origin header, the AJAX request fails.</span></span> <span data-ttu-id="8ca8c-217">특히 브라우저 요청을 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-217">Specifically, the browser disallows the request.</span></span> <span data-ttu-id="8ca8c-218">서버 응답에 성공 하면 반환 하는 경우에 브라우저 되어도 응답 클라이언트 응용 프로그램에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-218">Even if the server returns a successful response, the browser doesn't make the response available to the client application.</span></span>

### <a name="preflight-requests"></a><span data-ttu-id="8ca8c-219">실행 전 요청</span><span class="sxs-lookup"><span data-stu-id="8ca8c-219">Preflight Requests</span></span>

<span data-ttu-id="8ca8c-220">브라우저는 일부 CORS 요청에 대 한 리소스에 대 한 실제 요청을 보내기 전에 "실행 전 요청을" 라는 추가 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-220">For some CORS requests, the browser sends an additional request, called a "preflight request", before it sends the actual request for the resource.</span></span> <span data-ttu-id="8ca8c-221">다음 조건이 true 인 경우 브라우저가 실행 전 요청을 건너뛸 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="8ca8c-221">The browser can skip the preflight request if the following conditions are true:</span></span>

* <span data-ttu-id="8ca8c-222">요청 메서드는 GET, HEAD 또는 POST 및</span><span class="sxs-lookup"><span data-stu-id="8ca8c-222">The request method is GET, HEAD, or POST, and</span></span>

* <span data-ttu-id="8ca8c-223">응용 프로그램 동의 수용-언어 Content-language 이외의 모든 요청 헤더를 설정 하지 않는 콘텐츠 형식 또는 마지막-이벤트-ID 및</span><span class="sxs-lookup"><span data-stu-id="8ca8c-223">The application doesn't set any request headers other than Accept, Accept-Language, Content-Language, Content-Type, or Last-Event-ID, and</span></span>

* <span data-ttu-id="8ca8c-224">Content-type 헤더 (하는 경우 설정) 다음 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-224">The Content-Type header (if set) is one of the following:</span></span>

  * <span data-ttu-id="8ca8c-225">application/x-www-form-urlencoded</span><span class="sxs-lookup"><span data-stu-id="8ca8c-225">application/x-www-form-urlencoded</span></span>

  * <span data-ttu-id="8ca8c-226">다중 파트/폼 데이터</span><span class="sxs-lookup"><span data-stu-id="8ca8c-226">multipart/form-data</span></span>

  * <span data-ttu-id="8ca8c-227">텍스트/일반</span><span class="sxs-lookup"><span data-stu-id="8ca8c-227">text/plain</span></span>

<span data-ttu-id="8ca8c-228">요청 헤더에 대 한 규칙 setRequestHeader XMLHttpRequest 개체에서 호출 하 여 응용 프로그램을 설정 하는 헤더에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-228">The rule about request headers applies to headers that the application sets by calling setRequestHeader on the XMLHttpRequest object.</span></span> <span data-ttu-id="8ca8c-229">(CORS 사양 이러한 "작성자 요청 헤더"를 호출 합니다.) 규칙은 브라우저 등을 설정할 수, 사용자 에이전트, 호스트 또는 Content-length 헤더에 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-229">(The CORS specification calls these "author request headers".) The rule doesn't apply to headers the browser can set, such as User-Agent, Host, or Content-Length.</span></span>

<span data-ttu-id="8ca8c-230">실행 전 요청의 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-230">Here is an example of a preflight request:</span></span>

```
OPTIONS http://myservice.azurewebsites.net/api/test HTTP/1.1
Accept: */*
Origin: http://myclient.azurewebsites.net
Access-Control-Request-Method: PUT
Access-Control-Request-Headers: accept, x-my-custom-header
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; WOW64; Trident/6.0)
Host: myservice.azurewebsites.net
Content-Length: 0
```

<span data-ttu-id="8ca8c-231">HTTP OPTIONS 메서드를 사용 하는 사전 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-231">The pre-flight request uses the HTTP OPTIONS method.</span></span> <span data-ttu-id="8ca8c-232">두 가지 특수 헤더를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-232">It includes two special headers:</span></span>

* <span data-ttu-id="8ca8c-233">액세스-컨트롤-요청-방법: 실제 요청에 사용 될 HTTP 메서드.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-233">Access-Control-Request-Method: The HTTP method that will be used for the actual request.</span></span>

* <span data-ttu-id="8ca8c-234">컨트롤-요청-헤더에 액세스: 응용 프로그램에 실제로 요청에 설정 된 요청 헤더의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-234">Access-Control-Request-Headers: A list of request headers that the application set on the actual request.</span></span> <span data-ttu-id="8ca8c-235">(다시이 포함 되지 않습니다 브라우저 설정 하는 헤더.)</span><span class="sxs-lookup"><span data-stu-id="8ca8c-235">(Again, this doesn't include headers that the browser sets.)</span></span>

<span data-ttu-id="8ca8c-236">예제 응답, 서버 요청을 허용 하는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-236">Here is an example response, assuming that the server allows the request:</span></span>

```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 0
Access-Control-Allow-Origin: http://myclient.azurewebsites.net
Access-Control-Allow-Headers: x-my-custom-header
Access-Control-Allow-Methods: PUT
Date: Wed, 20 May 2015 06:33:22 GMT
```

<span data-ttu-id="8ca8c-237">허용 된 메서드를 나열 하는 액세스-컨트롤-허용-메서드 헤더 및 필요에 따라 허용 되는 헤더를 나열 하는 액세스 제어-허용-헤더 헤더를 응답에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-237">The response includes an Access-Control-Allow-Methods header that lists the allowed methods, and optionally an Access-Control-Allow-Headers header, which lists the allowed headers.</span></span> <span data-ttu-id="8ca8c-238">실행 전 요청이 성공 하면 브라우저 앞에서 설명한 대로 실제 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8ca8c-238">If the preflight request succeeds, the browser sends the actual request, as described earlier.</span></span>
