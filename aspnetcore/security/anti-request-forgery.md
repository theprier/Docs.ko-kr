---
title: ASP.NET Core 공격 방지 교차 사이트 요청 위조 XSRF/CSRF)
author: steve-smith
description: 악성 웹 사이트 클라이언트 브라우저와 응용 프로그램 간의 상호 작용에 적용할 수 있는 웹 응용 프로그램에 대 한 공격을 방지 하는 방법을 검색 합니다.
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 03/19/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/anti-request-forgery
ms.openlocfilehash: 3bca96f4a2e247eeeb93140df93221371d88d4d3
ms.sourcegitcommit: 7e87671fea9a5f36ca516616fe3b40b537f428d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35341862"
---
# <a name="prevent-cross-site-request-forgery-xsrfcsrf-attacks-in-aspnet-core"></a><span data-ttu-id="28e52-103">ASP.NET Core 공격 방지 교차 사이트 요청 위조 XSRF/CSRF)</span><span class="sxs-lookup"><span data-stu-id="28e52-103">Prevent Cross-Site Request Forgery (XSRF/CSRF) attacks in ASP.NET Core</span></span>

<span data-ttu-id="28e52-104">여 [Steve Smith](https://ardalis.com/), [Fiyaz Hasan](https://twitter.com/FiyazBinHasan), 및 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="28e52-104">By [Steve Smith](https://ardalis.com/), [Fiyaz Hasan](https://twitter.com/FiyazBinHasan), and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="28e52-105">교차 사이트 요청 위조 (XSRF 또는 CSRF, 발음 함 *참조 surf*)가 악의적인 웹 앱 클라이언트 브라우저와를 신뢰 하는 웹 응용 프로그램 간의 상호 작용 영향을 줄 수는 그에 따라 웹 호스팅 응용 프로그램에 대 한 공격 브라우저.</span><span class="sxs-lookup"><span data-stu-id="28e52-105">Cross-site request forgery (also known as XSRF or CSRF, pronounced *see-surf*) is an attack against web-hosted apps whereby a malicious web app can influence the interaction between a client browser and a web app that trusts that browser.</span></span> <span data-ttu-id="28e52-106">이러한 공격은 웹 브라우저가 웹 사이트에 일부 유형의 인증 토큰 모든 요청에 자동으로 전송 하기 때문에 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-106">These attacks are possible because web browsers send some types of authentication tokens automatically with every request to a website.</span></span> <span data-ttu-id="28e52-107">이러한 형태의 악용은 라고도 *원클릭 공격* 또는 *세션 도용을* 사용자 세션의 이전에 인증 활용 하기 때문에 방지할 수 있었던 공격입니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-107">This form of exploit is also known as a *one-click attack* or *session riding* because the attack takes advantage of the user's previously authenticated session.</span></span>

<span data-ttu-id="28e52-108">CSRF 공격의 예:</span><span class="sxs-lookup"><span data-stu-id="28e52-108">An example of a CSRF attack:</span></span>

1. <span data-ttu-id="28e52-109">사용자가에 로그인 할 `www.good-banking-site.com` 폼 인증을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-109">A user signs into `www.good-banking-site.com` using forms authentication.</span></span> <span data-ttu-id="28e52-110">서버에서 사용자를 인증 하지 않으며 인증 쿠키를 포함 하는 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-110">The server authenticates the user and issues a response that includes an authentication cookie.</span></span> <span data-ttu-id="28e52-111">사이트는 유효한 인증 쿠키와 함께 수신 하는 모든 요청을 신뢰 하기 때문에 공격에 취약 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-111">The site is vulnerable to attack because it trusts any request that it receives with a valid authentication cookie.</span></span>
1. <span data-ttu-id="28e52-112">사용자가 악성 사이트를 방문 `www.bad-crook-site.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-112">The user visits a malicious site, `www.bad-crook-site.com`.</span></span>

   <span data-ttu-id="28e52-113">악성 사이트 `www.bad-crook-site.com`, 다음과 유사한 HTML 폼을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-113">The malicious site, `www.bad-crook-site.com`, contains an HTML form similar to the following:</span></span>

   ```html
   <h1>Congratulations! You're a Winner!</h1>
   <form action="http://good-banking-site.com/api/account" method="post">
       <input type="hidden" name="Transaction" value="withdraw">
       <input type="hidden" name="Amount" value="1000000">
       <input type="submit" value="Click to collect your prize!">
   </form>
   ```

   <span data-ttu-id="28e52-114">양식의 `action` 악성 사이트 아닌 취약 한 사이트에 대 한 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-114">Notice that the form's `action` posts to the vulnerable site, not to the malicious site.</span></span> <span data-ttu-id="28e52-115">CSRF의 "사이트 간" 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-115">This is the "cross-site" part of CSRF.</span></span>

1. <span data-ttu-id="28e52-116">제출 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-116">The user selects the submit button.</span></span> <span data-ttu-id="28e52-117">브라우저 요청을 수행 하 고 요청 된 도메인에 대 한 인증 쿠키를 자동으로 포함 `www.good-banking-site.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-117">The browser makes the request and automatically includes the authentication cookie for the requested domain, `www.good-banking-site.com`.</span></span>
1. <span data-ttu-id="28e52-118">요청에서 실행 되는 `www.good-banking-site.com` 사용자의 인증 컨텍스트를 사용 하는 서버 인증된 된 사용자가을 수행할 수 있는 모든 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-118">The request runs on the `www.good-banking-site.com` server with the user's authentication context and can perform any action that an authenticated user is allowed to perform.</span></span>

<span data-ttu-id="28e52-119">사용자가 양식을 전송 하는 단추를 선택 하는 시나리오 뿐 아니라 악성 사이트는 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-119">In addition to the scenario where the user selects the button to submit the form, the malicious site could:</span></span>

* <span data-ttu-id="28e52-120">폼을 자동으로 전송 하는 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-120">Run a script that automatically submits the form.</span></span>
* <span data-ttu-id="28e52-121">양식 전송이 AJAX 요청으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-121">Send the form submission as an AJAX request.</span></span>
* <span data-ttu-id="28e52-122">CSS를 사용 하 여 폼을 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-122">Hide the form using CSS.</span></span>

<span data-ttu-id="28e52-123">이러한 다양 한 시나리오는 모든 작업 또는 처음 악성 사이트를 방문 이외의 사용자의 입력에 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-123">These alternative scenarios don't require any action or input from the user other than initially visiting the malicious site.</span></span>

<span data-ttu-id="28e52-124">HTTPS를 사용 하 여 CSRF 공격을 방지 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-124">Using HTTPS doesn't prevent a CSRF attack.</span></span> <span data-ttu-id="28e52-125">악성 사이트로 보낼 수는 `https://www.good-banking-site.com/` 안전 하지 않은 요청을 보낼 수 처럼 손쉽게 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-125">The malicious site can send an `https://www.good-banking-site.com/` request just as easily as it can send an insecure request.</span></span>

<span data-ttu-id="28e52-126">일부 공격 대상 작업을 수행 하려면 이미지 태그를 사용할 수는 쿼리에서 GET 요청에 응답 하는 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-126">Some attacks target endpoints that respond to GET requests, in which case an image tag can be used to perform the action.</span></span> <span data-ttu-id="28e52-127">이 형태의 공격이 이미지를 허용 하지만 JavaScript를 차단 하는 포럼 사이트에서 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-127">This form of attack is common on forum sites that permit images but block JavaScript.</span></span> <span data-ttu-id="28e52-128">변수 또는 리소스 변경에 GET 요청에서 상태를 변경 하는 앱은 악의적인 공격에 취약 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-128">Apps that change state on GET requests, where variables or resources are altered, are vulnerable to malicious attacks.</span></span> <span data-ttu-id="28e52-129">**상태를 변경 하는 GET 요청은 안전 하지 않습니다. GET 요청에서 상태 변경 하는 것이 좋습니다.**</span><span class="sxs-lookup"><span data-stu-id="28e52-129">**GET requests that change state are insecure. A best practice is to never change state on a GET request.**</span></span>

<span data-ttu-id="28e52-130">CSRF 공격 되므로 인증용 쿠키를 사용 하는 웹 응용 프로그램에 대해 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-130">CSRF attacks are possible against web apps that use cookies for authentication because:</span></span>

* <span data-ttu-id="28e52-131">브라우저 웹 응용 프로그램에서 발급 하는 쿠키를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-131">Browsers store cookies issued by a web app.</span></span>
* <span data-ttu-id="28e52-132">저장 된 쿠키는 인증 된 사용자에 대 한 세션 쿠키를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-132">Stored cookies include session cookies for authenticated users.</span></span>
* <span data-ttu-id="28e52-133">브라우저가 모든 쿠키와 관련 된 도메인을 웹 응용 프로그램 브라우저 내에서 응용 프로그램에 요청 생성 방법에 관계 없이 모든 요청을 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-133">Browsers send all of the cookies associated with a domain to the web app every request regardless of how the request to app was generated within the browser.</span></span>

<span data-ttu-id="28e52-134">그러나 CSRF 공격에 제한 되지 않습니다 쿠키를 이용 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-134">However, CSRF attacks aren't limited to exploiting cookies.</span></span> <span data-ttu-id="28e52-135">예를 들어, 기본 및 다이제스트 인증 취약 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-135">For example, Basic and Digest authentication are also vulnerable.</span></span> <span data-ttu-id="28e52-136">브라우저에서 세션까지 자격 증명을 자동으로 전송 후 사용자가 기본 또는 다이제스트 인증 로그인을&dagger; 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-136">After a user signs in with Basic or Digest authentication, the browser automatically sends the credentials until the session&dagger; ends.</span></span>

<span data-ttu-id="28e52-137">&dagger;이 컨텍스트에서 *세션* 참조 하는 사용자가 인증 하는 클라이언트 세션입니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-137">&dagger;In this context, *session* refers to the client-side session during which the user is authenticated.</span></span> <span data-ttu-id="28e52-138">서버 쪽 세션에 관련 되지 않은 또는 [ASP.NET Core 세션 미들웨어](xref:fundamentals/app-state)합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-138">It's unrelated to server-side sessions or [ASP.NET Core Session Middleware](xref:fundamentals/app-state).</span></span>

<span data-ttu-id="28e52-139">사용자가 예방 조치를 수행 하 여 CSRF 취약점을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-139">Users can guard against CSRF vulnerabilities by taking precautions:</span></span>

* <span data-ttu-id="28e52-140">사용 하 여 완료 되 면 웹 앱에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-140">Sign off of web apps when finished using them.</span></span>
* <span data-ttu-id="28e52-141">주기적으로 지우기 브라우저 쿠키입니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-141">Clear browser cookies periodically.</span></span>

<span data-ttu-id="28e52-142">그러나 CSRF 취약점은 기본적으로 웹 앱을 최종 사용자가 아닌 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-142">However, CSRF vulnerabilities are fundamentally a problem with the web app, not the end user.</span></span>

## <a name="authentication-fundamentals"></a><span data-ttu-id="28e52-143">인증 기본 사항</span><span class="sxs-lookup"><span data-stu-id="28e52-143">Authentication fundamentals</span></span>

<span data-ttu-id="28e52-144">쿠키 기반 인증에는 인기 있는 형태의 인증입니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-144">Cookie-based authentication is a popular form of authentication.</span></span> <span data-ttu-id="28e52-145">토큰 기반 인증 시스템은 단일 페이지 응용 프로그램 (SPAs)를 위해 특별히에서 인기, 커지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-145">Token-based authentication systems are growing in popularity, especially for Single Page Applications (SPAs).</span></span>

### <a name="cookie-based-authentication"></a><span data-ttu-id="28e52-146">쿠키 기반 인증</span><span class="sxs-lookup"><span data-stu-id="28e52-146">Cookie-based authentication</span></span>

<span data-ttu-id="28e52-147">사용자가 자신의 사용자 이름과 암호를 사용 하 여 인증, 인증 및 권한 부여에 사용할 수 있는 인증 티켓을 포함 하는 토큰을 발급 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-147">When a user authenticates using their username and password, they're issued a token, containing an authentication ticket that can be used for authentication and authorization.</span></span> <span data-ttu-id="28e52-148">토큰이는 클라이언트는 모든 요청을 함께 제공 되는 쿠키 함에 따라 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-148">The token is stored as a cookie that accompanies every request the client makes.</span></span> <span data-ttu-id="28e52-149">생성 하 고이 쿠키를 유효성 검사 쿠키 인증 미들웨어에서 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-149">Generating and validating this cookie is performed by the Cookie Authentication Middleware.</span></span> <span data-ttu-id="28e52-150">[미들웨어](xref:fundamentals/middleware/index) 사용자 계정 암호화 된 쿠키에 serialize 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-150">The [middleware](xref:fundamentals/middleware/index) serializes a user principal into an encrypted cookie.</span></span> <span data-ttu-id="28e52-151">이후 요청에서 미들웨어 쿠키의 유효성을 검사, 주 서버를 다시 만드는 및 보안 주체에 할당 된 [사용자](/dotnet/api/microsoft.aspnetcore.http.httpcontext.user) 속성 [HttpContext](/dotnet/api/microsoft.aspnetcore.http.httpcontext)합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-151">On subsequent requests, the middleware validates the cookie, recreates the principal, and assigns the principal to the [User](/dotnet/api/microsoft.aspnetcore.http.httpcontext.user) property of [HttpContext](/dotnet/api/microsoft.aspnetcore.http.httpcontext).</span></span>

### <a name="token-based-authentication"></a><span data-ttu-id="28e52-152">토큰 기반 인증</span><span class="sxs-lookup"><span data-stu-id="28e52-152">Token-based authentication</span></span>

<span data-ttu-id="28e52-153">사용자가 인증 될 때 (하지 antiforgery 토큰) 토큰을 발급 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-153">When a user is authenticated, they're issued a token (not an antiforgery token).</span></span> <span data-ttu-id="28e52-154">형식으로 사용자 정보를 포함 하는 토큰 [클레임](/dotnet/framework/security/claims-based-identity-model) 또는 응용 프로그램에서 유지 관리 하는 사용자 상태를 응용 프로그램을 가리키는 참조 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-154">The token contains user information in the form of [claims](/dotnet/framework/security/claims-based-identity-model) or a reference token that points the app to user state maintained in the app.</span></span> <span data-ttu-id="28e52-155">사용자가 인증을 요구 하는 리소스에 액세스 하려고 하는 경우 응용 프로그램을 추가 인증 헤더에서 전달자 토큰의 형태로 토큰이 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-155">When a user attempts to access a resource requiring authentication, the token is sent to the app with an additional authorization header in form of Bearer token.</span></span> <span data-ttu-id="28e52-156">이렇게 하면 응용 프로그램 상태 비저장 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-156">This makes the app stateless.</span></span> <span data-ttu-id="28e52-157">각 후속 요청에 토큰은 서버 쪽 유효성 검사에 대 한 요청에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-157">In each subsequent request, the token is passed in the request for server-side validation.</span></span> <span data-ttu-id="28e52-158">이 토큰이 없는 *암호화 된*; 있기 *인코딩된*합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-158">This token isn't *encrypted*; it's *encoded*.</span></span> <span data-ttu-id="28e52-159">서버에서 해당 정보에 액세스 하는 토큰은 디코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-159">On the server, the token is decoded to access its information.</span></span> <span data-ttu-id="28e52-160">토큰 이후의 요청을 보내려면 토큰 브라우저의 로컬 저장소에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-160">To send the token on subsequent requests, store the token in the browser's local storage.</span></span> <span data-ttu-id="28e52-161">토큰은 브라우저의 로컬 저장소에 저장 되는 경우 CSRF 취약점에 대 한 관심이 해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-161">Don't be concerned about CSRF vulnerability if the token is stored in the browser's local storage.</span></span> <span data-ttu-id="28e52-162">CSRF 문제가 있으면 토큰 쿠키에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-162">CSRF is a concern when the token is stored in a cookie.</span></span>

### <a name="multiple-apps-hosted-at-one-domain"></a><span data-ttu-id="28e52-163">한 도메인에서 호스팅되는 여러 앱</span><span class="sxs-lookup"><span data-stu-id="28e52-163">Multiple apps hosted at one domain</span></span>

<span data-ttu-id="28e52-164">공유 호스팅 환경은 세션 하이재킹, CSRF, 로그인 및 기타 공격에 취약 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-164">Shared hosting environments are vulnerable to session hijacking, login CSRF, and other attacks.</span></span>

<span data-ttu-id="28e52-165">하지만 `example1.contoso.net` 및 `example2.contoso.net` 는 서로 다른 호스트에서 호스트 간의 암시적 트러스트 관계가 있는 `*.contoso.net` 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-165">Although `example1.contoso.net` and `example2.contoso.net` are different hosts, there's an implicit trust relationship between hosts under the `*.contoso.net` domain.</span></span> <span data-ttu-id="28e52-166">이 암시적 트러스트 관계에는 신뢰할 수 없는 호스트를 (AJAX 요청을 제어 하는 동일 원본 정책 반드시 HTTP 쿠키를 적용 하지 않는) 다른 사용자의 쿠키에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-166">This implicit trust relationship allows potentially untrusted hosts to affect each other's cookies (the same-origin policies that govern AJAX requests don't necessarily apply to HTTP cookies).</span></span>

<span data-ttu-id="28e52-167">도메인을 공유 하지 않고 함으로써 같은 도메인에 호스트 되는 앱 간에 신뢰할 수 있는 쿠키를 악용 하는 공격을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-167">Attacks that exploit trusted cookies between apps hosted on the same domain can be prevented by not sharing domains.</span></span> <span data-ttu-id="28e52-168">각 응용 프로그램은 자체 도메인에서 호스트 되는 경우 암시적 쿠키 트러스트 관계가 없는 악용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-168">When each app is hosted on its own domain, there is no implicit cookie trust relationship to exploit.</span></span>

## <a name="aspnet-core-antiforgery-configuration"></a><span data-ttu-id="28e52-169">ASP.NET Core antiforgery 구성</span><span class="sxs-lookup"><span data-stu-id="28e52-169">ASP.NET Core antiforgery configuration</span></span>

> [!WARNING]
> <span data-ttu-id="28e52-170">ASP.NET Core antiforgery를 사용 하 여 구현 [ASP.NET Core 데이터 보호](xref:security/data-protection/introduction)합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-170">ASP.NET Core implements antiforgery using [ASP.NET Core Data Protection](xref:security/data-protection/introduction).</span></span> <span data-ttu-id="28e52-171">데이터 보호 스택의 서버 팜에서 작동 하도록 구성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-171">The data protection stack must be configured to work in a server farm.</span></span> <span data-ttu-id="28e52-172">참조 [데이터 보호를 구성](xref:security/data-protection/configuration/overview) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-172">See [Configuring data protection](xref:security/data-protection/configuration/overview) for more information.</span></span>

<span data-ttu-id="28e52-173">ASP.NET Core 2.0 이상에서는 [FormTagHelper](xref:mvc/views/working-with-forms#the-form-tag-helper) antiforgery 토큰 HTML 폼 요소를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-173">In ASP.NET Core 2.0 or later, the [FormTagHelper](xref:mvc/views/working-with-forms#the-form-tag-helper) injects antiforgery tokens into HTML form elements.</span></span> <span data-ttu-id="28e52-174">Razor 파일에 다음 태그는 자동으로 antiforgery 토큰을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-174">The following markup in a Razor file automatically generates antiforgery tokens:</span></span>

```cshtml
<form method="post">
    ...
</form>
```

<span data-ttu-id="28e52-175">마찬가지로, [IHtmlHelper.BeginForm](/dotnet/api/microsoft.aspnetcore.mvc.rendering.ihtmlhelper.beginform) 폼의 메서드가 GET 실행 되지 않으면 기본적으로 antiforgery 토큰을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-175">Similarily, [IHtmlHelper.BeginForm](/dotnet/api/microsoft.aspnetcore.mvc.rendering.ihtmlhelper.beginform) generates antiforgery tokens by default if the form's method isn't GET.</span></span>

<span data-ttu-id="28e52-176">발생 하는 HTML 폼 요소에 대 한 자동 생성 antiforgery 토큰의 경우는 `<form>` 태그에는 `method="post"` 특성 및 다음 중 하나에 해당할:</span><span class="sxs-lookup"><span data-stu-id="28e52-176">The automatic generation of antiforgery tokens for HTML form elements happens when the `<form>` tag contains the `method="post"` attribute and either of the following are true:</span></span>

  * <span data-ttu-id="28e52-177">동작 특성이 비어 (`action=""`).</span><span class="sxs-lookup"><span data-stu-id="28e52-177">The action attribute is empty (`action=""`).</span></span>
  * <span data-ttu-id="28e52-178">작업 특성을 제공 하지 않으면 (`<form method="post">`).</span><span class="sxs-lookup"><span data-stu-id="28e52-178">The action attribute isn't supplied (`<form method="post">`).</span></span>

<span data-ttu-id="28e52-179">HTML 폼 요소에 대 한 antiforgery 토큰의 자동 생성을 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-179">Automatic generation of antiforgery tokens for HTML form elements can be disabled:</span></span>

* <span data-ttu-id="28e52-180">Antiforgery 토큰을 사용 하 여 명시적으로 비활성화할는 `asp-antiforgery` 특성:</span><span class="sxs-lookup"><span data-stu-id="28e52-180">Explicitly disable antiforgery tokens with the `asp-antiforgery` attribute:</span></span>

  ```cshtml
  <form method="post" asp-antiforgery="false">
      ...
  </form>
  ```

* <span data-ttu-id="28e52-181">Form 요소는 선택한 아웃 태그 도우미의 태그 도우미를 사용 하 여 [! 옵트아웃 기호](xref:mvc/views/tag-helpers/intro#opt-out):</span><span class="sxs-lookup"><span data-stu-id="28e52-181">The form element is opted-out of Tag Helpers by using the Tag Helper [! opt-out symbol](xref:mvc/views/tag-helpers/intro#opt-out):</span></span>

  ```cshtml
  <!form method="post">
      ...
  </!form>
  ```

* <span data-ttu-id="28e52-182">제거는 `FormTagHelper` 보기에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-182">Remove the `FormTagHelper` from the view.</span></span> <span data-ttu-id="28e52-183">`FormTagHelper` Razor 보기에는 다음 지시문을 추가 하 여 보기에서 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-183">The `FormTagHelper` can be removed from a view by adding the following directive to the Razor view:</span></span>

  ```cshtml
  @removeTagHelper Microsoft.AspNetCore.Mvc.TagHelpers.FormTagHelper, Microsoft.AspNetCore.Mvc.TagHelpers
  ```

> [!NOTE]
> <span data-ttu-id="28e52-184">[Razor 페이지](xref:mvc/razor-pages/index) XSRF/CSRF에서 자동으로 보호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-184">[Razor Pages](xref:mvc/razor-pages/index) are automatically protected from XSRF/CSRF.</span></span> <span data-ttu-id="28e52-185">자세한 내용은 참조 [XSRF/CSRF 및 Razor 페이지](xref:mvc/razor-pages/index#xsrf)합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-185">For more information, see [XSRF/CSRF and Razor Pages](xref:mvc/razor-pages/index#xsrf).</span></span>

<span data-ttu-id="28e52-186">가장 일반적인 방법은 CSRF 공격 으로부터 보호 하는 데 사용 하는 것은 *동기화 장치 토큰 패턴이* (STP).</span><span class="sxs-lookup"><span data-stu-id="28e52-186">The most common approach to defending against CSRF attacks is to use the *Synchronizer Token Pattern* (STP).</span></span> <span data-ttu-id="28e52-187">STP은 사용자 양식 데이터로 페이지를 요청할 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-187">STP is used when the user requests a page with form data:</span></span>

1. <span data-ttu-id="28e52-188">서버는 클라이언트에 현재 사용자의 id와 연결 된 토큰을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-188">The server sends a token associated with the current user's identity to the client.</span></span>
1. <span data-ttu-id="28e52-189">클라이언트가 보냅니다 확인을 위해 서버를 다시 토큰.</span><span class="sxs-lookup"><span data-stu-id="28e52-189">The client sends back the token to the server for verification.</span></span>
1. <span data-ttu-id="28e52-190">인증 된 사용자의 id와 일치 하지 않는 토큰을 수신 하는 서버, 요청이 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-190">If the server receives a token that doesn't match the authenticated user's identity, the request is rejected.</span></span>

<span data-ttu-id="28e52-191">토큰이 고유 하 고 예측할 수 없는 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-191">The token is unique and unpredictable.</span></span> <span data-ttu-id="28e52-192">토큰을 사용 하 여 일련의 요청을 적절 한 시퀀싱 할 수도 수 (요청 시퀀스의 예를 들어 보장: 1 페이지가 &ndash; 2 페이지 &ndash; 3 페이지).</span><span class="sxs-lookup"><span data-stu-id="28e52-192">The token can also be used to ensure proper sequencing of a series of requests (for example, ensuring the request sequence of: page 1 &ndash; page 2 &ndash; page 3).</span></span> <span data-ttu-id="28e52-193">모든 Razor 페이지 및 ASP.NET Core MVC 템플릿에서 양식의 antiforgery 토큰을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-193">All of the forms in ASP.NET Core MVC and Razor Pages templates generate antiforgery tokens.</span></span> <span data-ttu-id="28e52-194">다음 예제 보기 쌍 antiforgery 토큰을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-194">The following pair of view examples generate antiforgery tokens:</span></span>

```cshtml
<form asp-controller="Manage" asp-action="ChangePassword" method="post">
    ...
</form>

@using (Html.BeginForm("ChangePassword", "Manage"))
{
    ...
}
```

<span data-ttu-id="28e52-195">Antiforgery 토큰을 명시적으로 추가 된 `<form>` HTML 도우미와 태그 도우미를 사용 하지 않고 요소 [ @Html.AntiForgeryToken ](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.htmlhelper.antiforgerytoken):</span><span class="sxs-lookup"><span data-stu-id="28e52-195">Explicitly add an antiforgery token to a `<form>` element without using Tag Helpers with the HTML helper [@Html.AntiForgeryToken](/dotnet/api/microsoft.aspnetcore.mvc.viewfeatures.htmlhelper.antiforgerytoken):</span></span>

```cshtml
<form action="/" method="post">
    @Html.AntiForgeryToken()
</form>
```

<span data-ttu-id="28e52-196">위의 경우 중 각 ASP.NET Core 다음과 유사한 숨겨진된 양식 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-196">In each of the preceding cases, ASP.NET Core adds a hidden form field similar to the following:</span></span>

```cshtml
<input name="__RequestVerificationToken" type="hidden" value="CfDJ8NrAkS ... s2-m9Yw">
```

<span data-ttu-id="28e52-197">ASP.NET Core 3 개 포함 [필터](xref:mvc/controllers/filters) antiforgery 토큰을 사용 하기 위한:</span><span class="sxs-lookup"><span data-stu-id="28e52-197">ASP.NET Core includes three [filters](xref:mvc/controllers/filters) for working with antiforgery tokens:</span></span>

* [<span data-ttu-id="28e52-198">ValidateAntiForgeryToken</span><span class="sxs-lookup"><span data-stu-id="28e52-198">ValidateAntiForgeryToken</span></span>](/dotnet/api/microsoft.aspnetcore.mvc.validateantiforgerytokenattribute)
* [<span data-ttu-id="28e52-199">AutoValidateAntiforgeryToken</span><span class="sxs-lookup"><span data-stu-id="28e52-199">AutoValidateAntiforgeryToken</span></span>](/dotnet/api/microsoft.aspnetcore.mvc.autovalidateantiforgerytokenattribute)
* [<span data-ttu-id="28e52-200">IgnoreAntiforgeryToken</span><span class="sxs-lookup"><span data-stu-id="28e52-200">IgnoreAntiforgeryToken</span></span>](/dotnet/api/microsoft.aspnetcore.mvc.ignoreantiforgerytokenattribute)

## <a name="antiforgery-options"></a><span data-ttu-id="28e52-201">Antiforgery 옵션</span><span class="sxs-lookup"><span data-stu-id="28e52-201">Antiforgery options</span></span>

<span data-ttu-id="28e52-202">사용자 지정 [antiforgery 옵션](/dotnet/api/Microsoft.AspNetCore.Antiforgery.AntiforgeryOptions) 에 `Startup.ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="28e52-202">Customize [antiforgery options](/dotnet/api/Microsoft.AspNetCore.Antiforgery.AntiforgeryOptions) in `Startup.ConfigureServices`:</span></span>

```csharp
services.AddAntiforgery(options => 
{
    options.CookieDomain = "contoso.com";
    options.CookieName = "X-CSRF-TOKEN-COOKIENAME";
    options.CookiePath = "Path";
    options.FormFieldName = "AntiforgeryFieldname";
    options.HeaderName = "X-CSRF-TOKEN-HEADERNAME";
    options.RequireSsl = false;
    options.SuppressXFrameOptionsHeader = false;
});
```

| <span data-ttu-id="28e52-203">옵션</span><span class="sxs-lookup"><span data-stu-id="28e52-203">Option</span></span> | <span data-ttu-id="28e52-204">설명</span><span class="sxs-lookup"><span data-stu-id="28e52-204">Description</span></span> |
| ------ | ----------- |
| [<span data-ttu-id="28e52-205">쿠키</span><span class="sxs-lookup"><span data-stu-id="28e52-205">Cookie</span></span>](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.cookie) | <span data-ttu-id="28e52-206">Antiforgery 쿠키를 만드는 데 설정을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-206">Determines the settings used to create the antiforgery cookies.</span></span> |
| [<span data-ttu-id="28e52-207">CookieDomain</span><span class="sxs-lookup"><span data-stu-id="28e52-207">CookieDomain</span></span>](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.cookiedomain) | <span data-ttu-id="28e52-208">쿠키의 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-208">The domain of the cookie.</span></span> <span data-ttu-id="28e52-209">기본값은 `null`입니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-209">Defaults to `null`.</span></span> <span data-ttu-id="28e52-210">이 속성은 사용 되지 않으며 이후 버전에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-210">This property is obsolete and will be removed in a future version.</span></span> <span data-ttu-id="28e52-211">권장 방법은 Cookie.Domain입니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-211">The recommended alternative is Cookie.Domain.</span></span> |
| [<span data-ttu-id="28e52-212">CookieName</span><span class="sxs-lookup"><span data-stu-id="28e52-212">CookieName</span></span>](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.cookiename) | <span data-ttu-id="28e52-213">쿠키의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-213">The name of the cookie.</span></span> <span data-ttu-id="28e52-214">을 설정 하지 시스템 생성 고유 이름으로 시작 된 [DefaultCookiePrefix](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.defaultcookieprefix) (". AspNetCore.Antiforgery입니다. ")입니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-214">If not set, the system generates a unique name beginning with the [DefaultCookiePrefix](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.defaultcookieprefix) (".AspNetCore.Antiforgery.").</span></span> <span data-ttu-id="28e52-215">이 속성은 사용 되지 않으며 이후 버전에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-215">This property is obsolete and will be removed in a future version.</span></span> <span data-ttu-id="28e52-216">권장 방법은 Cookie.Name입니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-216">The recommended alternative is Cookie.Name.</span></span> |
| [<span data-ttu-id="28e52-217">CookiePath</span><span class="sxs-lookup"><span data-stu-id="28e52-217">CookiePath</span></span>](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.cookiepath) | <span data-ttu-id="28e52-218">쿠키에 설정 된 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-218">The path set on the cookie.</span></span> <span data-ttu-id="28e52-219">이 속성은 사용 되지 않으며 이후 버전에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-219">This property is obsolete and will be removed in a future version.</span></span> <span data-ttu-id="28e52-220">권장 방법은 Cookie.Path입니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-220">The recommended alternative is Cookie.Path.</span></span> |
| [<span data-ttu-id="28e52-221">FormFieldName</span><span class="sxs-lookup"><span data-stu-id="28e52-221">FormFieldName</span></span>](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.formfieldname) | <span data-ttu-id="28e52-222">뷰에서 antiforgery 토큰을 렌더링 하는 antiforgery 시스템에서 사용 하는 숨겨진된 폼 필드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-222">The name of the hidden form field used by the antiforgery system to render antiforgery tokens in views.</span></span> |
| [<span data-ttu-id="28e52-223">HeaderName</span><span class="sxs-lookup"><span data-stu-id="28e52-223">HeaderName</span></span>](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.headername) | <span data-ttu-id="28e52-224">Antiforgery 시스템에서 사용 하는 헤더의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-224">The name of the header used by the antiforgery system.</span></span> <span data-ttu-id="28e52-225">경우 `null`, 시스템에서는 양식 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-225">If `null`, the system considers only form data.</span></span> |
| [<span data-ttu-id="28e52-226">RequireSsl</span><span class="sxs-lookup"><span data-stu-id="28e52-226">RequireSsl</span></span>](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.requiressl) | <span data-ttu-id="28e52-227">Antiforgery 시스템에서 SSL이 필요한 지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-227">Specifies whether SSL is required by the antiforgery system.</span></span> <span data-ttu-id="28e52-228">경우 `true`, 비 SSL 요청이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-228">If `true`, non-SSL requests fail.</span></span> <span data-ttu-id="28e52-229">기본값은 `false`입니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-229">Defaults to `false`.</span></span> <span data-ttu-id="28e52-230">이 속성은 사용 되지 않으며 이후 버전에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-230">This property is obsolete and will be removed in a future version.</span></span> <span data-ttu-id="28e52-231">메서드 대신 Cookie.SecurePolicy를 설정 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-231">The recommended alternative is to set Cookie.SecurePolicy.</span></span> |
| [<span data-ttu-id="28e52-232">SuppressXFrameOptionsHeader</span><span class="sxs-lookup"><span data-stu-id="28e52-232">SuppressXFrameOptionsHeader</span></span>](/dotnet/api/microsoft.aspnetcore.antiforgery.antiforgeryoptions.suppressxframeoptionsheader) | <span data-ttu-id="28e52-233">생성을 표시 하지 않을 것인지를 지정 된 `X-Frame-Options` 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-233">Specifies whether to suppress generation of the `X-Frame-Options` header.</span></span> <span data-ttu-id="28e52-234">기본적으로 머리글은 "SAMEORIGIN"의 값으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-234">By default, the header is generated with a value of "SAMEORIGIN".</span></span> <span data-ttu-id="28e52-235">기본값은 `false`입니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-235">Defaults to `false`.</span></span> |

<span data-ttu-id="28e52-236">자세한 내용은 참조 [CookieAuthenticationOptions](/dotnet/api/Microsoft.AspNetCore.Builder.CookieAuthenticationOptions)합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-236">For more information, see [CookieAuthenticationOptions](/dotnet/api/Microsoft.AspNetCore.Builder.CookieAuthenticationOptions).</span></span>

## <a name="configure-antiforgery-features-with-iantiforgery"></a><span data-ttu-id="28e52-237">IAntiforgery와 antiforgery 기능을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-237">Configure antiforgery features with IAntiforgery</span></span>

<span data-ttu-id="28e52-238">[IAntiforgery](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgery) antiforgery 기능을 구성 하는 API를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-238">[IAntiforgery](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgery) provides the API to configure antiforgery features.</span></span> <span data-ttu-id="28e52-239">`IAntiforgery` 요청한 크기에 `Configure` 의 메서드는 `Startup` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-239">`IAntiforgery` can be requested in the `Configure` method of the `Startup` class.</span></span> <span data-ttu-id="28e52-240">다음 예제에서는 응용 프로그램의 홈 페이지에서 미들웨어를 사용 하 여 antiforgery 토큰을 생성 하 고 쿠키 (사용 하 여 기본 각도 명명 규칙이이 항목의 뒷부분에서 설명)으로 응답에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-240">The following example uses middleware from the app's home page to generate an antiforgery token and send it in the response as a cookie (using the default Angular naming convention described later in this topic):</span></span>

```csharp
public void Configure(IApplicationBuilder app, IAntiforgery antiforgery)
{
    app.Use(next => context =>
    {
        string path = context.Request.Path.Value;

        if (
            string.Equals(path, "/", StringComparison.OrdinalIgnoreCase) ||
            string.Equals(path, "/index.html", StringComparison.OrdinalIgnoreCase))
        {
            // The request token can be sent as a JavaScript-readable cookie, 
            // and Angular uses it by default.
            var tokens = antiforgery.GetAndStoreTokens(context);
            context.Response.Cookies.Append("XSRF-TOKEN", tokens.RequestToken, 
                new CookieOptions() { HttpOnly = false });
        }

        return next(context);
    });
}
```

### <a name="require-antiforgery-validation"></a><span data-ttu-id="28e52-241">Antiforgery 유효성 검사 필요</span><span class="sxs-lookup"><span data-stu-id="28e52-241">Require antiforgery validation</span></span>

<span data-ttu-id="28e52-242">[ValidateAntiForgeryToken](/dotnet/api/microsoft.aspnetcore.mvc.validateantiforgerytokenattribute) 는 개별 작업은 컨트롤러에 적용할 수 있는 작업 필터는 전역적으로 또는 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-242">[ValidateAntiForgeryToken](/dotnet/api/microsoft.aspnetcore.mvc.validateantiforgerytokenattribute) is an action filter that can be applied to an individual action, a controller, or globally.</span></span> <span data-ttu-id="28e52-243">요청에 유효한 antiforgery 토큰에 포함 되지 않으면이 필터 적용이 영향을 주는 작업에 대 한 요청 차단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-243">Requests made to actions that have this filter applied are blocked unless the request includes a valid antiforgery token.</span></span>

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<IActionResult> RemoveLogin(RemoveLoginViewModel account)
{
    ManageMessageId? message = ManageMessageId.Error;
    var user = await GetCurrentUserAsync();

    if (user != null)
    {
        var result = 
            await _userManager.RemoveLoginAsync(
                user, account.LoginProvider, account.ProviderKey);

        if (result.Succeeded)
        {
            await _signInManager.SignInAsync(user, isPersistent: false);
            message = ManageMessageId.RemoveLoginSuccess;
        }
    }

    return RedirectToAction(nameof(ManageLogins), new { Message = message });
}
```

<span data-ttu-id="28e52-244">`ValidateAntiForgeryToken` 특성에 대 한 요청 작업 메서드 HTTP GET 요청을 포함 하 여 데코레이팅되 토큰이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-244">The `ValidateAntiForgeryToken` attribute requires a token for requests to the action methods it decorates, including HTTP GET requests.</span></span> <span data-ttu-id="28e52-245">경우는 `ValidateAntiForgeryToken` 특성은 응용 프로그램의 컨트롤러에 적용 되며,으로 재정의 될 수는 `IgnoreAntiforgeryToken` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-245">If the `ValidateAntiForgeryToken` attribute is applied across the app's controllers, it can be overridden with the `IgnoreAntiforgeryToken` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="28e52-246">ASP.NET Core GET 요청에 antiforgery 토큰을 자동으로 추가 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-246">ASP.NET Core doesn't support adding antiforgery tokens to GET requests automatically.</span></span>

### <a name="automatically-validate-antiforgery-tokens-for-unsafe-http-methods-only"></a><span data-ttu-id="28e52-247">자동으로 안전 하지 않은 HTTP 메서드에 대 한 antiforgery 토큰 유효성을 검사합니다</span><span class="sxs-lookup"><span data-stu-id="28e52-247">Automatically validate antiforgery tokens for unsafe HTTP methods only</span></span>

<span data-ttu-id="28e52-248">ASP.NET Core 응용 프로그램 안전 HTTP 메서드 (GET, HEAD, 옵션 및 추적)에 대 한 antiforgery 토큰을 생성 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-248">ASP.NET Core apps don't generate antiforgery tokens for safe HTTP methods (GET, HEAD, OPTIONS, and TRACE).</span></span> <span data-ttu-id="28e52-249">광범위 하 게 적용 하는 대신는 `ValidateAntiForgeryToken` 특성 및 사용 하 여를 재정의 `IgnoreAntiforgeryToken` 특성은 [AutoValidateAntiforgeryToken](/dotnet/api/microsoft.aspnetcore.mvc.autovalidateantiforgerytokenattribute) 특성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-249">Instead of broadly applying the `ValidateAntiForgeryToken` attribute and then overriding it with `IgnoreAntiforgeryToken` attributes, the [AutoValidateAntiforgeryToken](/dotnet/api/microsoft.aspnetcore.mvc.autovalidateantiforgerytokenattribute) attribute can be used.</span></span> <span data-ttu-id="28e52-250">이 특성은 동일 하 게 작동는 `ValidateAntiForgeryToken` 특성을 제외 하 고 토큰에 대 한 다음과 같은 HTTP 메서드를 사용 하 여 요청 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-250">This attribute works identically to the `ValidateAntiForgeryToken` attribute, except that it doesn't require tokens for requests made using the following HTTP methods:</span></span>

* <span data-ttu-id="28e52-251">가져오기</span><span class="sxs-lookup"><span data-stu-id="28e52-251">GET</span></span>
* <span data-ttu-id="28e52-252">HEAD</span><span class="sxs-lookup"><span data-stu-id="28e52-252">HEAD</span></span>
* <span data-ttu-id="28e52-253">옵션</span><span class="sxs-lookup"><span data-stu-id="28e52-253">OPTIONS</span></span>
* <span data-ttu-id="28e52-254">TRACE</span><span class="sxs-lookup"><span data-stu-id="28e52-254">TRACE</span></span>

<span data-ttu-id="28e52-255">사용 권장 `AutoValidateAntiforgeryToken` 비 API 시나리오에 대 한 광범위 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-255">We recommend use of `AutoValidateAntiforgeryToken` broadly for non-API scenarios.</span></span> <span data-ttu-id="28e52-256">이렇게 하면 기본적으로 POST 작업 보호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-256">This ensures POST actions are protected by default.</span></span> <span data-ttu-id="28e52-257">대신 사용 하는 표시 되지 않으면 기본적으로 antiforgery 토큰을 무시 하도록 `ValidateAntiForgeryToken` 개별 작업 메서드에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-257">The alternative is to ignore antiforgery tokens by default, unless `ValidateAntiForgeryToken` is applied to individual action methods.</span></span> <span data-ttu-id="28e52-258">것에 쓰지만 대개 남겨둘 POST 작업 메서드에 대 한이 시나리오에서는 보호 되지 않은 상태로 실수로 CSRF 공격에 취약 한 응용 프로그램을 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-258">It's more likely in this scenario for a POST action method to be left unprotected by mistake, leaving the app vulnerable to CSRF attacks.</span></span> <span data-ttu-id="28e52-259">모든 게시물 antiforgery 토큰을 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-259">All POSTs should send the antiforgery token.</span></span>

<span data-ttu-id="28e52-260">Api는 토큰의 쿠키 일부로 보내기 위한 자동 메커니즘이 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-260">APIs don't have an automatic mechanism for sending the non-cookie part of the token.</span></span> <span data-ttu-id="28e52-261">아마도 구현 클라이언트 코드 구현에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-261">The implementation probably depends on the client code implementation.</span></span> <span data-ttu-id="28e52-262">몇 가지 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-262">Some examples are shown below:</span></span>

<span data-ttu-id="28e52-263">클래스 수준 예:</span><span class="sxs-lookup"><span data-stu-id="28e52-263">Class-level example:</span></span>

```csharp
[Authorize]
[AutoValidateAntiforgeryToken]
public class ManageController : Controller
{
```

<span data-ttu-id="28e52-264">전역 예:</span><span class="sxs-lookup"><span data-stu-id="28e52-264">Global example:</span></span>

```csharp
services.AddMvc(options => 
    options.Filters.Add(new AutoValidateAntiforgeryTokenAttribute()));
```

### <a name="override-global-or-controller-antiforgery-attributes"></a><span data-ttu-id="28e52-265">전역 재정의 또는 컨트롤러 antiforgery 특성</span><span class="sxs-lookup"><span data-stu-id="28e52-265">Override global or controller antiforgery attributes</span></span>

<span data-ttu-id="28e52-266">[IgnoreAntiforgeryToken](/dotnet/api/microsoft.aspnetcore.mvc.ignoreantiforgerytokenattribute) 필터는 지정 된 작업 (또는 컨트롤러)에 대 한 antiforgery 토큰에 대 한 필요성을 제거 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-266">The [IgnoreAntiforgeryToken](/dotnet/api/microsoft.aspnetcore.mvc.ignoreantiforgerytokenattribute) filter is used to eliminate the need for an antiforgery token for a given action (or controller).</span></span> <span data-ttu-id="28e52-267">이 필터 재정의 적용 하면 `ValidateAntiForgeryToken` 및 `AutoValidateAntiforgeryToken` (전역적으로 또는 컨트롤러)는 더 높은 수준에서 지정 된 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-267">When applied, this filter overrides `ValidateAntiForgeryToken` and `AutoValidateAntiforgeryToken` filters specified at a higher level (globally or on a controller).</span></span>

```csharp
[Authorize]
[AutoValidateAntiforgeryToken]
public class ManageController : Controller
{
    [HttpPost]
    [IgnoreAntiforgeryToken]
    public async Task<IActionResult> DoSomethingSafe(SomeViewModel model)
    {
        // no antiforgery token required
    }
}
```

## <a name="refresh-tokens-after-authentication"></a><span data-ttu-id="28e52-268">인증 후 새로 고침 토큰</span><span class="sxs-lookup"><span data-stu-id="28e52-268">Refresh tokens after authentication</span></span>

<span data-ttu-id="28e52-269">뷰 또는 Razor 페이지의 페이지에 사용자를 리디렉션하여 사용자가 인증 한 후 토큰 새로 고쳐야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-269">Tokens should be refreshed after the user is authenticated by redirecting the user to a view or Razor Pages page.</span></span>

## <a name="javascript-ajax-and-spas"></a><span data-ttu-id="28e52-270">JavaScript, AJAX 및 SPAs</span><span class="sxs-lookup"><span data-stu-id="28e52-270">JavaScript, AJAX, and SPAs</span></span>

<span data-ttu-id="28e52-271">기존 HTML 기반 앱에서 antiforgery 토큰 숨겨진된 양식 필드를 사용 하 여 서버에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-271">In traditional HTML-based apps, antiforgery tokens are passed to the server using hidden form fields.</span></span> <span data-ttu-id="28e52-272">최신 JavaScript 기반 응용 프로그램 및 SPAs 많은 요청이 프로그래밍 방식으로 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-272">In modern JavaScript-based apps and SPAs, many requests are made programmatically.</span></span> <span data-ttu-id="28e52-273">이러한 AJAX 요청 토큰 다른 기술 (예: 요청 헤더 또는 쿠키)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-273">These AJAX requests may use other techniques (such as request headers or cookies) to send the token.</span></span>

<span data-ttu-id="28e52-274">인증 토큰을 저장 하 고 서버에 대 한 API 요청을 인증 쿠키를 사용 하는 경우 CSRF 잠재적인 문제가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-274">If cookies are used to store authentication tokens and to authenticate API requests on the server, CSRF is a potential problem.</span></span> <span data-ttu-id="28e52-275">토큰을 저장할 로컬 저장소 사용 하는 경우 로컬 저장소에서 값은 모든 요청을 사용 하 여 서버에 자동으로 전송 되지 않습니다 때문에 CSRF 취약성을 완화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-275">If local storage is used to store the token, CSRF vulnerability might be mitigated because values from local storage aren't sent automatically to the server with every request.</span></span> <span data-ttu-id="28e52-276">따라서 요청 헤더는 권장된 방법으로 토큰을 보내는 클라이언트에 antiforgery 토큰을 저장할 로컬 저장소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-276">Thus, using local storage to store the antiforgery token on the client and sending the token as a request header is a recommended approach.</span></span>

### <a name="javascript"></a><span data-ttu-id="28e52-277">JavaScript</span><span class="sxs-lookup"><span data-stu-id="28e52-277">JavaScript</span></span>

<span data-ttu-id="28e52-278">JavaScript에서 뷰를 사용 하는 토큰 만들 수 있습니다 보기 내에서 서비스를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-278">Using JavaScript with views, the token can be created using a service from within the view.</span></span> <span data-ttu-id="28e52-279">삽입 된 [Microsoft.AspNetCore.Antiforgery.IAntiforgery](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgery) 보기 및 호출 계층에 서비스 [GetAndStoreTokens](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgery.getandstoretokens):</span><span class="sxs-lookup"><span data-stu-id="28e52-279">Inject the [Microsoft.AspNetCore.Antiforgery.IAntiforgery](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgery) service into the view and call [GetAndStoreTokens](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgery.getandstoretokens):</span></span>

[!code-csharp[](anti-request-forgery/sample/MvcSample/Views/Home/Ajax.cshtml?highlight=4-10,12-13,35-36)]

<span data-ttu-id="28e52-280">이 방법은 서버에서 쿠키를 설정 하거나 클라이언트에서 읽기를 직접 사용 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-280">This approach eliminates the need to deal directly with setting cookies from the server or reading them from the client.</span></span>

<span data-ttu-id="28e52-281">앞의 예제 JavaScript를 사용 하 여 AJAX POST 헤더에 대 한 숨겨진된 필드 값을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-281">The preceding example uses JavaScript to read the hidden field value for the AJAX POST header.</span></span>

<span data-ttu-id="28e52-282">JavaScript 쿠키의 토큰에 액세스할 수 있고 쿠키의 콘텐츠를 사용 하 여 토큰의 값을 사용 하는 헤더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-282">JavaScript can also access tokens in cookies and use the cookie's contents to create a header with the token's value.</span></span>

```csharp
context.Response.Cookies.Append("CSRF-TOKEN", tokens.RequestToken, 
    new Microsoft.AspNetCore.Http.CookieOptions { HttpOnly = false });
```

<span data-ttu-id="28e52-283">헤더에 토큰을 보낼 요청 스크립트 가정 `X-CSRF-TOKEN`, 찾으려는 antiforgery 서비스 구성의 `X-CSRF-TOKEN` 헤더:</span><span class="sxs-lookup"><span data-stu-id="28e52-283">Assuming the script requests to send the token in a header called `X-CSRF-TOKEN`, configure the antiforgery service to look for the `X-CSRF-TOKEN` header:</span></span>

```csharp
services.AddAntiforgery(options => options.HeaderName = "X-CSRF-TOKEN");
```

<span data-ttu-id="28e52-284">다음 예제에서는 JavaScript를 사용 하 여 적절 한 헤더를 사용 하는 AJAX 요청 확인.</span><span class="sxs-lookup"><span data-stu-id="28e52-284">The following example uses JavaScript to make an AJAX request with the appropriate header:</span></span>

```javascript
function getCookie(cname) {
    var name = cname + "=";
    var decodedCookie = decodeURIComponent(document.cookie);
    var ca = decodedCookie.split(';');
    for(var i = 0; i <ca.length; i++) {
        var c = ca[i];
        while (c.charAt(0) == ' ') {
            c = c.substring(1);
        }
        if (c.indexOf(name) == 0) {
            return c.substring(name.length, c.length);
        }
    }
    return "";
}

var csrfToken = getCookie("CSRF-TOKEN");

var xhttp = new XMLHttpRequest();
xhttp.onreadystatechange = function() {
    if (xhttp.readyState == XMLHttpRequest.DONE) {
        if (xhttp.status == 200) {
            alert(xhttp.responseText);
        } else {
            alert('There was an error processing the AJAX request.');
        }
    }
};
xhttp.open('POST', '/api/password/changepassword', true);
xhttp.setRequestHeader("Content-type", "application/json");
xhttp.setRequestHeader("X-CSRF-TOKEN", csrfToken);
xhttp.send(JSON.stringify({ "newPassword": "ReallySecurePassword999$$$" }));
```

### <a name="angularjs"></a><span data-ttu-id="28e52-285">AngularJS</span><span class="sxs-lookup"><span data-stu-id="28e52-285">AngularJS</span></span>

<span data-ttu-id="28e52-286">AngularJS는 CSRF 주소로 규칙을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-286">AngularJS uses a convention to address CSRF.</span></span> <span data-ttu-id="28e52-287">서버 이름으로 쿠키를 전송 하는 경우 `XSRF-TOKEN`, AngularJS `$http` 서비스 서버에 요청을 보낼 때 헤더에 쿠키 값을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-287">If the server sends a cookie with the name `XSRF-TOKEN`, the AngularJS `$http` service adds the cookie value to a header when it sends a request to the server.</span></span> <span data-ttu-id="28e52-288">이 프로세스는 자동.</span><span class="sxs-lookup"><span data-stu-id="28e52-288">This process is automatic.</span></span> <span data-ttu-id="28e52-289">헤더를 명시적으로 설정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-289">The header doesn't need to be set explicitly.</span></span> <span data-ttu-id="28e52-290">헤더 이름이 `X-XSRF-TOKEN`합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-290">The header name is `X-XSRF-TOKEN`.</span></span> <span data-ttu-id="28e52-291">서버는이 헤더를 검색 하 고 해당 내용의 유효성을 검사 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-291">The server should detect this header and validate its contents.</span></span>

<span data-ttu-id="28e52-292">ASP.NET Core API에 대 한이 규칙을 통해 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-292">For ASP.NET Core API work with this convention:</span></span>

* <span data-ttu-id="28e52-293">호출 하는 쿠키에 토큰을 제공할 앱을 구성 `XSRF-TOKEN`합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-293">Configure your app to provide a token in a cookie called `XSRF-TOKEN`.</span></span>
* <span data-ttu-id="28e52-294">라는 헤더 찾으려는 antiforgery 서비스 구성 `X-XSRF-TOKEN`합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-294">Configure the antiforgery service to look for a header named `X-XSRF-TOKEN`.</span></span>

```csharp
services.AddAntiforgery(options => options.HeaderName = "X-XSRF-TOKEN");
```

<span data-ttu-id="28e52-295">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/anti-request-forgery/sample/AngularSample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="28e52-295">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/anti-request-forgery/sample/AngularSample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="extend-antiforgery"></a><span data-ttu-id="28e52-296">Antiforgery 확장</span><span class="sxs-lookup"><span data-stu-id="28e52-296">Extend antiforgery</span></span>

<span data-ttu-id="28e52-297">[IAntiForgeryAdditionalDataProvider](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider) 형식에서는 개발자가 각 토큰의 추가 데이터를 왕복 하 여 앤티 CSRF 시스템의 동작을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-297">The [IAntiForgeryAdditionalDataProvider](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider) type allows developers to extend the behavior of the anti-CSRF system by round-tripping additional data in each token.</span></span> <span data-ttu-id="28e52-298">[GetAdditionalData](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider.getadditionaldata) 될 때마다 메서드는 필드 토큰이 생성 되 고 반환 값은 생성 되는 토큰 내에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-298">The [GetAdditionalData](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider.getadditionaldata) method is called each time a field token is generated, and the return value is embedded within the generated token.</span></span> <span data-ttu-id="28e52-299">구현 자가 수 타임 스탬프, nonce, 또는 다른 모든 값을 반환 하 고 호출 [ValidateAdditionalData](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider.validateadditionaldata) 토큰의 유효성을 검사할 때이 데이터를 유효성 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-299">An implementer could return a timestamp, a nonce, or any other value and then call [ValidateAdditionalData](/dotnet/api/microsoft.aspnetcore.antiforgery.iantiforgeryadditionaldataprovider.validateadditionaldata) to validate this data when the token is validated.</span></span> <span data-ttu-id="28e52-300">클라이언트의 사용자 이름은 이미 생성 된 토큰에 포함 되어 있으므로이 정보를 포함할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-300">The client's username is already embedded in the generated tokens, so there's no need to include this information.</span></span> <span data-ttu-id="28e52-301">아니지만 추가 데이터 토큰을 포함 하는 경우 `IAntiForgeryAdditionalDataProvider` 가 구성, 보조 데이터 확인 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="28e52-301">If a token includes supplemental data but no `IAntiForgeryAdditionalDataProvider` is configured, the supplemental data isn't validated.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="28e52-302">추가 자료</span><span class="sxs-lookup"><span data-stu-id="28e52-302">Additional resources</span></span>

* <span data-ttu-id="28e52-303">[CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)) 에 [웹 응용 프로그램 보안 프로젝트를 열고](https://www.owasp.org/index.php/Main_Page) (OWASP).</span><span class="sxs-lookup"><span data-stu-id="28e52-303">[CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)) on [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page) (OWASP).</span></span>
