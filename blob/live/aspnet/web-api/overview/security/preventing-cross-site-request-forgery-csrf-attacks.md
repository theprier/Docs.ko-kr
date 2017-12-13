---
uid: web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
title: "ASP.NET Web API의에서 교차 사이트 요청 위조 (CSRF) 공격 방지 | Microsoft Docs"
author: MikeWasson
description: "교차 사이트 요청 위조 (CSRF) 공격 및 앤티 CSRF 조치 ASP.NET Web API를 구현 하는 방법에 설명 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/12/2012
ms.topic: article
ms.assetid: 81d46f14-8f48-4d8c-830d-cc8d594dc11b
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
msc.type: authoredcontent
ms.openlocfilehash: 1cd03f3b396cc2ece1d8dbe6820f6277c02d8e62
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="preventing-cross-site-request-forgery-csrf-attacks-in-aspnet-web-api"></a><span data-ttu-id="8ccd2-103">ASP.NET Web API의에서 교차 사이트 요청 위조 (CSRF) 공격 방지</span><span class="sxs-lookup"><span data-stu-id="8ccd2-103">Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API</span></span>
====================
<span data-ttu-id="8ccd2-104">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="8ccd2-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="8ccd2-105">교차 사이트 요청 위조 CSRF ()은 악성 사이트를 사용자가 현재 로그인 취약 한 사이트에 요청을 보냅니다는 방식의 공격</span><span class="sxs-lookup"><span data-stu-id="8ccd2-105">Cross-Site Request Forgery (CSRF) is an attack where a malicious site sends a request to a vulnerable site where the user is currently logged in</span></span>

<span data-ttu-id="8ccd2-106">CSRF 공격의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-106">Here is an example of a CSRF attack:</span></span>

1. <span data-ttu-id="8ccd2-107">Www.example.com에 사용자가 사용 하 여 폼 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-107">A user logs into www.example.com, using forms authentication.</span></span>
2. <span data-ttu-id="8ccd2-108">서버에서 사용자를 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-108">The server authenticates the user.</span></span> <span data-ttu-id="8ccd2-109">서버 로부터 응답 하면 인증 쿠키가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-109">The response from the server includes an authentication cookie.</span></span>
3. <span data-ttu-id="8ccd2-110">사용자 로그 아웃을 하지 않고 악성 웹 사이트를 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-110">Without logging out, the user visits a malicious web site.</span></span> <span data-ttu-id="8ccd2-111">이 악성 사이트 다음 HTML 폼을 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-111">This malicious site contains the following HTML form:</span></span> 

    [!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample1.html)]

    <span data-ttu-id="8ccd2-112">Form action에는 취약 한 사이트 악성 사이트에 게시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-112">Notice that the form action posts to the vulnerable site, not to the malicious site.</span></span> <span data-ttu-id="8ccd2-113">CSRF의 "사이트 간" 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-113">This is the "cross-site" part of CSRF.</span></span>
4. <span data-ttu-id="8ccd2-114">사용자가 제출 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-114">The user clicks the submit button.</span></span> <span data-ttu-id="8ccd2-115">브라우저에는 요청과 함께 인증 쿠키가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-115">The browser includes the authentication cookie with the request.</span></span>
5. <span data-ttu-id="8ccd2-116">요청은 사용자의 인증 컨텍스트를 사용 하 여 서버에서 실행 되며 인증된 된 사용자가 수행할 수 있는 모든 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-116">The request runs on the server with the user's authentication context, and can do anything that an authenticated user is allowed to do.</span></span>

<span data-ttu-id="8ccd2-117">하지만이 예제에서는 양식 단추를 클릭 하 여 사용자, 악의적인 페이지 것 처럼 쉽게 폼을 자동으로 전송 하는 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-117">Although this example requires the user to click the form button, the malicious page could just as easily run a script that submits the form automatically.</span></span> <span data-ttu-id="8ccd2-118">또한 악성 사이트 "https://" 요청을 보낼 수 있으므로 SSL을 사용 하 여 CSRF 공격을 방지 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-118">Moreover, using SSL does not prevent a CSRF attack, because the malicious site can send an "https://" request.</span></span>

<span data-ttu-id="8ccd2-119">일반적으로 CSRF 공격은 브라우저가 대상 웹 사이트에 모든 관련 쿠키를 전송 하기 때문에 인증을 위한 쿠키를 사용 하는 웹 사이트에 대해 가능한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-119">Typically, CSRF attacks are possible against web sites that use cookies for authentication, because browsers send all relevant cookies to the destination web site.</span></span> <span data-ttu-id="8ccd2-120">그러나 CSRF 공격 쿠키 악용에 제한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-120">However, CSRF attacks are not limited to exploiting cookies.</span></span> <span data-ttu-id="8ccd2-121">예를 들어, 기본 및 다이제스트 인증 취약 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-121">For example, Basic and Digest authentication are also vulnerable.</span></span> <span data-ttu-id="8ccd2-122">기본 또는 다이제스트 인증을 사용 하 여 사용자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-122">After a user logs in with Basic or Digest authentication.</span></span> <span data-ttu-id="8ccd2-123">브라우저는 세션이 종료 될 때까지 자격 증명을 자동으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-123">the browser automatically sends the credentials until the session ends.</span></span>

## <a name="anti-forgery-tokens"></a><span data-ttu-id="8ccd2-124">위조 방지 토큰</span><span class="sxs-lookup"><span data-stu-id="8ccd2-124">Anti-Forgery Tokens</span></span>

<span data-ttu-id="8ccd2-125">CSRF 공격을 방지 하려면 ASP.NET MVC에서 라고도 하는 위조 방지 토큰 사용 *확인 토큰을 요청할*합니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-125">To help prevent CSRF attacks, ASP.NET MVC uses anti-forgery tokens, also called *request verification tokens*.</span></span>

1. <span data-ttu-id="8ccd2-126">클라이언트는 양식을 포함 하는 HTML 페이지를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-126">The client requests an HTML page that contains a form.</span></span>
2. <span data-ttu-id="8ccd2-127">서버 응답에 두 개의 토큰을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-127">The server includes two tokens in the response.</span></span> <span data-ttu-id="8ccd2-128">하나의 토큰은 쿠키로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-128">One token is sent as a cookie.</span></span> <span data-ttu-id="8ccd2-129">다른 숨겨진된 폼 필드에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-129">The other is placed in a hidden form field.</span></span> <span data-ttu-id="8ccd2-130">토큰은 악의적 사용자 값을 예상할 수 있도록 임의로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-130">The tokens are generated randomly so that an adversary cannot guess the values.</span></span>
3. <span data-ttu-id="8ccd2-131">클라이언트 양식을 전송 하는 경우 서버에 다시 두 토큰이 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-131">When the client submits the form, it must send both tokens back to the server.</span></span> <span data-ttu-id="8ccd2-132">클라이언트는 쿠키 토큰을를 쿠키로 보내고 양식 데이터 내 폼 토큰을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-132">The client sends the cookie token as a cookie, and it sends the form token inside the form data.</span></span> <span data-ttu-id="8ccd2-133">(브라우저 클라이언트가 자동으로이 사용자가 폼을 제출 합니다.)</span><span class="sxs-lookup"><span data-stu-id="8ccd2-133">(A browser client automatically does this when the user submits the form.)</span></span>
4. <span data-ttu-id="8ccd2-134">요청에는 두 토큰이 포함 되어 있지 않으면, 서버 요청을 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-134">If a request does not include both tokens, the server disallows the request.</span></span>

<span data-ttu-id="8ccd2-135">숨겨진된 폼 토큰을 사용 하 여 HTML 폼의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-135">Here is an example of an HTML form with a hidden form token:</span></span>

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample2.html)]

<span data-ttu-id="8ccd2-136">위조 방지 토큰에는 악의적인 페이지 동일 원본 정책으로 인해 사용자의 토큰을 읽을 수 없으므로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-136">Anti-forgery tokens work because the malicious page cannot read the user's tokens, due to same-origin policies.</span></span> <span data-ttu-id="8ccd2-137">([동일 원본 정책](http://www.w3.org/Security/wiki/Same_Origin_Policy) 다른 사용자의 내용에 액세스 하지 못하도록 하는 두 개의 다른 사이트에서 호스팅되는 문서를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-137">([Same-origin policies](http://www.w3.org/Security/wiki/Same_Origin_Policy) prevent documents hosted on two different sites from accessing each other's content.</span></span> <span data-ttu-id="8ccd2-138">따라서 앞의 예제에서 악의적인 페이지 요청을 보낼 수 example.com, 하지만 응답을 읽을 수 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="8ccd2-138">So in the earlier example, the malicious page can send requests to example.com, but it cannot read the response.)</span></span>

<span data-ttu-id="8ccd2-139">CSRF 공격을 방지 브라우저가 자동으로 보내는 모든 인증 프로토콜 함께 위조 방지 토큰을 사용 하십시오 사용자가 로그인 한 후 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-139">To prevent CSRF attacks, use anti-forgery tokens with any authentication protocol where the browser silently sends credentials after the user logs in.</span></span> <span data-ttu-id="8ccd2-140">이 같은 폼 인증 쿠키 기반 인증 프로토콜을 포함으로 기본 및 다이제스트 인증과 같은 프로토콜을 통해.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-140">This includes cookie-based authentication protocols, such as forms authentication, as well as protocols such as Basic and Digest authentication.</span></span>

<span data-ttu-id="8ccd2-141">위조 방지 토큰 nonsafe 메서드 (POST, PUT, DELETE) 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-141">You should require anti-forgery tokens for any nonsafe methods (POST, PUT, DELETE).</span></span> <span data-ttu-id="8ccd2-142">안전 메서드 (GET, HEAD) 모든 부작용을 포함 하지 않는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-142">Also, make sure that safe methods (GET, HEAD) do not have any side effects.</span></span> <span data-ttu-id="8ccd2-143">또한 JSONP 또는 CORS와 같은 도메인 간 지원을 사용 하도록 설정 하면 다음도 안전 메서드 GET 같은 공격자가 잠재적으로 중요 한 데이터를 읽을 수 있도록 하는 CSRF 공격에 취약할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-143">Moreover, if you enable cross-domain support, such as CORS or JSONP, then even safe methods like GET are potentially vulnerable to CSRF attacks, allowing the attacker to read potentially sensitive data.</span></span>

## <a name="anti-forgery-tokens-in-aspnet-mvc"></a><span data-ttu-id="8ccd2-144">ASP.NET MVC에서 위조 방지 토큰</span><span class="sxs-lookup"><span data-stu-id="8ccd2-144">Anti-Forgery Tokens in ASP.NET MVC</span></span>

<span data-ttu-id="8ccd2-145">위조 방지 토큰에는 Razor 페이지를 추가 하려면 사용 하 여는 **HtmlHelper.AntiForgeryToken** 도우미 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-145">To add the anti-forgery tokens to a Razor page, use the **HtmlHelper.AntiForgeryToken** helper method:</span></span>

[!code-cshtml[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample3.cshtml)]

<span data-ttu-id="8ccd2-146">이 메서드는 숨겨진된 양식 필드를 추가 하 고 쿠키 토큰을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-146">This method adds the hidden form field and also sets the cookie token.</span></span>

## <a name="anti-csrf-and-ajax"></a><span data-ttu-id="8ccd2-147">앤티 CSRF 및 AJAX</span><span class="sxs-lookup"><span data-stu-id="8ccd2-147">Anti-CSRF and AJAX</span></span>

<span data-ttu-id="8ccd2-148">AJAX 요청 JSON 데이터를 하지 HTML 폼 데이터를 보낼 수 있습니다 폼 토큰 AJAX 요청에 대 한 문제일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-148">The form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="8ccd2-149">한 가지 해결 방법은 사용자 지정 HTTP 헤더에 토큰을 보내려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-149">One solution is to send the tokens in a custom HTTP header.</span></span> <span data-ttu-id="8ccd2-150">다음 코드에서는 Razor 구문을 사용 하 여 토큰을 생성 하 고 AJAX 요청에 토큰을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-150">The following code uses Razor syntax to generate the tokens, and then adds the tokens to an AJAX request.</span></span> <span data-ttu-id="8ccd2-151">토큰은 호출 하 여 서버에 생성 된 **AntiForgery.GetTokens**합니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-151">The tokens are generated at the server by calling **AntiForgery.GetTokens**.</span></span>

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample4.html)]

<span data-ttu-id="8ccd2-152">요청을 처리 하는 경우 요청 헤더에서 토큰을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-152">When you process the request, extract the tokens from the request header.</span></span> <span data-ttu-id="8ccd2-153">그런 다음 호출에서 **AntiForgery.Validate** 메서드는 토큰 유효성 검사를 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-153">Then call the **AntiForgery.Validate** method to validate the tokens.</span></span> <span data-ttu-id="8ccd2-154">**유효성 검사** 메서드 토큰이 유효 하지 않은 경우 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ccd2-154">The **Validate** method throws an exception if the tokens are not valid.</span></span>

[!code-csharp[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample5.cs)]
