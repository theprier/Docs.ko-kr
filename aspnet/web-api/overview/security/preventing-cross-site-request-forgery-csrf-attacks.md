---
uid: web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
title: ASP.NET Web API에서에서 교차 사이트 요청 위조 (CSRF) 공격 방지 | Microsoft Docs
author: MikeWasson
description: 교차 사이트 요청 위조 (CSRF) 공격 및 ASP.NET Web API에서 CSRF 방지 조치를 구현 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 12/12/2012
ms.assetid: 81d46f14-8f48-4d8c-830d-cc8d594dc11b
msc.legacyurl: /web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
msc.type: authoredcontent
ms.openlocfilehash: cd7d978190d28a028285746781a380d9bb5f91d4
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829114"
---
<a name="preventing-cross-site-request-forgery-csrf-attacks-in-aspnet-web-api"></a><span data-ttu-id="d609a-103">ASP.NET Web API에서에서 교차 사이트 요청 위조 (CSRF) 공격 방지</span><span class="sxs-lookup"><span data-stu-id="d609a-103">Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API</span></span>
====================
<span data-ttu-id="d609a-104">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="d609a-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="d609a-105">교차 사이트 요청 위조 (CSRF) 공격 악성 사이트 여기서 사용자가 현재 로그인 한 취약 한 사이트에 요청을 보냅니다 하는 위치는</span><span class="sxs-lookup"><span data-stu-id="d609a-105">Cross-Site Request Forgery (CSRF) is an attack where a malicious site sends a request to a vulnerable site where the user is currently logged in</span></span>

<span data-ttu-id="d609a-106">CSRF 공격의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-106">Here is an example of a CSRF attack:</span></span>

1. <span data-ttu-id="d609a-107">사용자가 로그인 `www.example.com` 폼 인증을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-107">A user logs into `www.example.com` using forms authentication.</span></span>
2. <span data-ttu-id="d609a-108">서버에서 사용자를 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-108">The server authenticates the user.</span></span> <span data-ttu-id="d609a-109">인증 쿠키를 포함 하는 서버에서 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-109">The response from the server includes an authentication cookie.</span></span>
3. <span data-ttu-id="d609a-110">로그 아웃을 하지 않고 사용자가 악성 웹 사이트를 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-110">Without logging out, the user visits a malicious web site.</span></span> <span data-ttu-id="d609a-111">다음 HTML 양식을 포함 하는이 악성 사이트:</span><span class="sxs-lookup"><span data-stu-id="d609a-111">This malicious site contains the following HTML form:</span></span> 

    [!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample1.html)]

    <span data-ttu-id="d609a-112">Form action는 취약 한 사이트 악의적인 사이트에 게시 하는 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-112">Notice that the form action posts to the vulnerable site, not to the malicious site.</span></span> <span data-ttu-id="d609a-113">CSRF의 "교차 사이트" 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-113">This is the "cross-site" part of CSRF.</span></span>
4. <span data-ttu-id="d609a-114">제출 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-114">The user clicks the submit button.</span></span> <span data-ttu-id="d609a-115">브라우저 요청을 사용 하 여 인증 쿠키를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-115">The browser includes the authentication cookie with the request.</span></span>
5. <span data-ttu-id="d609a-116">요청은 사용자의 인증 컨텍스트를 사용 하 여 서버에서 실행 되 고 인증된 된 사용자가 수행할 수 있는 아무 것도 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-116">The request runs on the server with the user's authentication context, and can do anything that an authenticated user is allowed to do.</span></span>

<span data-ttu-id="d609a-117">이 예제에서는 사용자가 폼 단추 클릭, 되지만 폼을 자동으로 전송 하는 스크립트를 실행 하는 쉽게와 마찬가지로 악의적인 페이지 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-117">Although this example requires the user to click the form button, the malicious page could just as easily run a script that submits the form automatically.</span></span> <span data-ttu-id="d609a-118">또한 악성 사이트 "https://" 요청을 보낼 수 있기 때문에 SSL을 사용 하 여 CSRF 공격을 방지 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-118">Moreover, using SSL does not prevent a CSRF attack, because the malicious site can send an "https://" request.</span></span>

<span data-ttu-id="d609a-119">일반적으로 CSRF 공격은 인증용 쿠키를 사용 하는 웹 사이트에 대해 가능한 브라우저 대상 웹 사이트에 모든 관련 쿠키를 보낼 수 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-119">Typically, CSRF attacks are possible against web sites that use cookies for authentication, because browsers send all relevant cookies to the destination web site.</span></span> <span data-ttu-id="d609a-120">그러나 CSRF 공격 쿠키 악용에 제한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-120">However, CSRF attacks are not limited to exploiting cookies.</span></span> <span data-ttu-id="d609a-121">예를 들어, 기본 및 다이제스트 인증은 또한 취약 합니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-121">For example, Basic and Digest authentication are also vulnerable.</span></span> <span data-ttu-id="d609a-122">이후에 사용자가 기본 또는 다이제스트 인증을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-122">After a user logs in with Basic or Digest authentication.</span></span> <span data-ttu-id="d609a-123">브라우저는 세션이 종료 될 때까지 자격 증명을 자동으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-123">the browser automatically sends the credentials until the session ends.</span></span>

## <a name="anti-forgery-tokens"></a><span data-ttu-id="d609a-124">위조 방지 토큰</span><span class="sxs-lookup"><span data-stu-id="d609a-124">Anti-Forgery Tokens</span></span>

<span data-ttu-id="d609a-125">CSRF 공격을 방지 하기 위해 ASP.NET MVC 위해 위조 방지 토큰을 라고도 *요청 확인 토큰*합니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-125">To help prevent CSRF attacks, ASP.NET MVC uses anti-forgery tokens, also called *request verification tokens*.</span></span>

1. <span data-ttu-id="d609a-126">클라이언트는 양식을 포함 하는 HTML 페이지를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-126">The client requests an HTML page that contains a form.</span></span>
2. <span data-ttu-id="d609a-127">서버 응답에서 두 개의 토큰을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-127">The server includes two tokens in the response.</span></span> <span data-ttu-id="d609a-128">하나의 토큰은 쿠키로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-128">One token is sent as a cookie.</span></span> <span data-ttu-id="d609a-129">다른 숨겨진된 폼 필드에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-129">The other is placed in a hidden form field.</span></span> <span data-ttu-id="d609a-130">악의적 사용자가 값을 예상할 수 있도록 토큰을 임의로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-130">The tokens are generated randomly so that an adversary cannot guess the values.</span></span>
3. <span data-ttu-id="d609a-131">클라이언트가 폼을 제출 하면 서버에 두 토큰이 모두 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-131">When the client submits the form, it must send both tokens back to the server.</span></span> <span data-ttu-id="d609a-132">클라이언트는 쿠키 토큰을 쿠키로 보내고 양식 데이터 내에서 폼 토큰을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-132">The client sends the cookie token as a cookie, and it sends the form token inside the form data.</span></span> <span data-ttu-id="d609a-133">(브라우저 클라이언트가 자동으로 수행이 사용자가 폼을 전송 합니다.)</span><span class="sxs-lookup"><span data-stu-id="d609a-133">(A browser client automatically does this when the user submits the form.)</span></span>
4. <span data-ttu-id="d609a-134">요청에 토큰이 모두 포함 되어 있지 않으면, 서버 요청을 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-134">If a request does not include both tokens, the server disallows the request.</span></span>

<span data-ttu-id="d609a-135">숨겨진된 폼 토큰을 사용 하 여 HTML 폼의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-135">Here is an example of an HTML form with a hidden form token:</span></span>

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample2.html)]

<span data-ttu-id="d609a-136">위조 방지 토큰에는 악의적인 페이지 동일 원본 정책으로 인해 사용자의 토큰을 읽을 수 없으므로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-136">Anti-forgery tokens work because the malicious page cannot read the user's tokens, due to same-origin policies.</span></span> <span data-ttu-id="d609a-137">([동일 원본 정책](http://www.w3.org/Security/wiki/Same_Origin_Policy) 서로 콘텐츠를 액세스 하지 못하도록 하는 두 개의 다른 사이트에 호스트 된 문서를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-137">([Same-origin policies](http://www.w3.org/Security/wiki/Same_Origin_Policy) prevent documents hosted on two different sites from accessing each other's content.</span></span> <span data-ttu-id="d609a-138">따라서 이전 예제에서는 악의적인 페이지 요청을 보낼 수 example.com, 있지만 응답 읽을 수 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="d609a-138">So in the earlier example, the malicious page can send requests to example.com, but it cannot read the response.)</span></span>

<span data-ttu-id="d609a-139">CSRF 공격 방지, 브라우저를 자동으로 보내는 모든 인증 프로토콜을 사용 하 여 위조 방지 토큰을 사용 하 여 사용자가 로그인 한 후 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-139">To prevent CSRF attacks, use anti-forgery tokens with any authentication protocol where the browser silently sends credentials after the user logs in.</span></span> <span data-ttu-id="d609a-140">이 폼 인증과 같은 쿠키 기반 인증 프로토콜을 포함 합니다. 뿐만 아니라 기본 및 다이제스트 인증과 같은 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-140">This includes cookie-based authentication protocols, such as forms authentication, as well as protocols such as Basic and Digest authentication.</span></span>

<span data-ttu-id="d609a-141">Nonsafe 메서드 (POST, PUT, DELETE)에 대 한 위조 방지 토큰을 요청 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-141">You should require anti-forgery tokens for any nonsafe methods (POST, PUT, DELETE).</span></span> <span data-ttu-id="d609a-142">또한 안전한 메서드 (GET, HEAD) 모든 파생 작업이 없는 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-142">Also, make sure that safe methods (GET, HEAD) do not have any side effects.</span></span> <span data-ttu-id="d609a-143">또한 JSONP 또는 CORS와 같은 도메인 간 지원을 사용 하도록 설정 하면 다음 GET 등의 더 안전한 방법을 잠재적으로 취약할 CSRF 공격에 공격자가 잠재적으로 중요 한 데이터를 읽을 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-143">Moreover, if you enable cross-domain support, such as CORS or JSONP, then even safe methods like GET are potentially vulnerable to CSRF attacks, allowing the attacker to read potentially sensitive data.</span></span>

## <a name="anti-forgery-tokens-in-aspnet-mvc"></a><span data-ttu-id="d609a-144">ASP.NET MVC에서 위조 방지 토큰</span><span class="sxs-lookup"><span data-stu-id="d609a-144">Anti-Forgery Tokens in ASP.NET MVC</span></span>

<span data-ttu-id="d609a-145">Razor 페이지에 위조 방지 토큰을 추가 하려면 사용 합니다 **HtmlHelper.AntiForgeryToken** 도우미 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-145">To add the anti-forgery tokens to a Razor page, use the **HtmlHelper.AntiForgeryToken** helper method:</span></span>

[!code-cshtml[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample3.cshtml)]

<span data-ttu-id="d609a-146">이 메서드는 숨겨진된 폼 필드를 추가 하 고 쿠키 토큰을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-146">This method adds the hidden form field and also sets the cookie token.</span></span>

## <a name="anti-csrf-and-ajax"></a><span data-ttu-id="d609a-147">CSRF 방지 및 AJAX</span><span class="sxs-lookup"><span data-stu-id="d609a-147">Anti-CSRF and AJAX</span></span>

<span data-ttu-id="d609a-148">AJAX 요청이 HTML 양식 데이터가 아닌 JSON 데이터를 보낼 수 있으므로 폼 토큰에서 AJAX 요청에 대 한 문제를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-148">The form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="d609a-149">하나의 솔루션 사용자 지정 HTTP 헤더에 토큰을 보내는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-149">One solution is to send the tokens in a custom HTTP header.</span></span> <span data-ttu-id="d609a-150">다음 코드는 Razor 구문을 사용 하 여 토큰을 생성 하 고 AJAX 요청에 토큰을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-150">The following code uses Razor syntax to generate the tokens, and then adds the tokens to an AJAX request.</span></span> <span data-ttu-id="d609a-151">토큰을 호출 하 여 서버에 생성 됩니다 **AntiForgery.GetTokens**합니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-151">The tokens are generated at the server by calling **AntiForgery.GetTokens**.</span></span>

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample4.html)]

<span data-ttu-id="d609a-152">요청을 처리 하는 경우 요청 헤더에서 토큰을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-152">When you process the request, extract the tokens from the request header.</span></span> <span data-ttu-id="d609a-153">그런 다음 호출을 **AntiForgery.Validate** 토큰의 유효성을 검사 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-153">Then call the **AntiForgery.Validate** method to validate the tokens.</span></span> <span data-ttu-id="d609a-154">합니다 **유효성 검사** 메서드는 토큰이 유효 하지 않은 경우 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="d609a-154">The **Validate** method throws an exception if the tokens are not valid.</span></span>

[!code-csharp[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample5.cs)]
