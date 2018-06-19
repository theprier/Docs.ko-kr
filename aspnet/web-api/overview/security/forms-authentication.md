---
uid: web-api/overview/security/forms-authentication
title: ASP.NET Web API의에서 폼 인증 | Microsoft Docs
author: MikeWasson
description: 폼 인증을 사용 하 여 ASP.NET Web API에 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/12/2012
ms.topic: article
ms.assetid: 9f06c1f2-ffaa-4831-94a0-2e4a3befdf07
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/security/forms-authentication
msc.type: authoredcontent
ms.openlocfilehash: 9027d76bcf8854fc85f11906d3651511f350cd32
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
ms.locfileid: "26508312"
---
<a name="forms-authentication-in-aspnet-web-api"></a><span data-ttu-id="ca70a-103">ASP.NET Web API에서에서 폼 인증</span><span class="sxs-lookup"><span data-stu-id="ca70a-103">Forms Authentication in ASP.NET Web API</span></span>
====================
<span data-ttu-id="ca70a-104">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ca70a-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="ca70a-105">폼 인증 HTML 폼을 사용 하 여 사용자의 자격 증명 서버에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-105">Forms authentication uses an HTML form to send the user's credentials to the server.</span></span> <span data-ttu-id="ca70a-106">인터넷 표준 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-106">It is not an Internet standard.</span></span> <span data-ttu-id="ca70a-107">폼 인증은 웹 응용 프로그램에서 호출 되는 web Api에 대 한 적절 한 사용자는 HTML 폼과 상호 작용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-107">Forms authentication is only appropriate for web APIs that are called from a web application, so that the user can interact with the HTML form.</span></span>

| <span data-ttu-id="ca70a-108">장점</span><span class="sxs-lookup"><span data-stu-id="ca70a-108">Advantages</span></span> | <span data-ttu-id="ca70a-109">단점</span><span class="sxs-lookup"><span data-stu-id="ca70a-109">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="ca70a-110">-구현 하기 쉬운: ASP.NET에 기본 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-110">- Easy to implement: Built into ASP.NET.</span></span> <span data-ttu-id="ca70a-111">-손쉽게 사용자 계정을 관리 하는 ASP.NET 멤버 자격 공급자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-111">- Uses ASP.NET membership provider, which makes it easy to manage user accounts.</span></span> | <span data-ttu-id="ca70a-112">--는 표준 HTTP 인증 메커니즘입니다. 표준 인증 헤더 대신 HTTP 쿠키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-112">- Not a standard HTTP authentication mechanism; uses HTTP cookies instead of the standard Authorization header.</span></span> <span data-ttu-id="ca70a-113">-브라우저 클라이언트가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-113">- Requires a browser client.</span></span> <span data-ttu-id="ca70a-114">-자격 증명은 텍스트로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-114">- Credentials are sent as plaintext.</span></span> <span data-ttu-id="ca70a-115">-에 취약 교차 사이트 요청 위조 CSRF (); 앤티 CSRF 측정값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-115">- Vulnerable to cross-site request forgery (CSRF); requires anti-CSRF measures.</span></span> <span data-ttu-id="ca70a-116">-비 브라우저 클라이언트에서 사용 하기 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-116">- Difficult to use from nonbrowser clients.</span></span> <span data-ttu-id="ca70a-117">로그인 하려면 브라우저를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-117">Login requires a browser.</span></span> <span data-ttu-id="ca70a-118">-사용자 자격 증명 요청에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-118">- User credentials are sent in the request.</span></span> <span data-ttu-id="ca70a-119">-일부 사용자가 쿠키를 비활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-119">- Some users disable cookies.</span></span> |

<span data-ttu-id="ca70a-120">간단히 말해서 asp.net에서 폼 인증은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-120">Briefly, forms authentication in ASP.NET works like this:</span></span>

1. <span data-ttu-id="ca70a-121">클라이언트 인증을 요구 하는 리소스를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-121">The client requests a resource that requires authentication.</span></span>
2. <span data-ttu-id="ca70a-122">사용자 인증 되지 않은 경우 서버는 HTTP 302 (있음)를 반환 하 고 로그인 페이지로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-122">If the user is not authenticated, the server returns HTTP 302 (Found) and redirects to a login page.</span></span>
3. <span data-ttu-id="ca70a-123">사용자 자격 증명을 입력 하 고 폼을 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-123">The user enters credentials and submits the form.</span></span>
4. <span data-ttu-id="ca70a-124">서버는 원래 URI로 다시 리디렉션하는 다른 HTTP 302를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-124">The server returns another HTTP 302 that redirects back to the original URI.</span></span> <span data-ttu-id="ca70a-125">이 응답 하면 인증 쿠키가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-125">This response includes an authentication cookie.</span></span>
5. <span data-ttu-id="ca70a-126">클라이언트에서 리소스를 다시 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-126">The client requests the resource again.</span></span> <span data-ttu-id="ca70a-127">서버 요청을 부여 하므로 인증 쿠키를 포함 하는 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-127">The request includes the authentication cookie, so the server grants the request.</span></span>

![](forms-authentication/_static/image1.png)

<span data-ttu-id="ca70a-128">자세한 내용은 참조 [는 폼 인증 개요입니다.](../../../web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs.md)</span><span class="sxs-lookup"><span data-stu-id="ca70a-128">For more information, see [An Overview of Forms Authentication.](../../../web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs.md)</span></span>

## <a name="using-forms-authentication-with-web-api"></a><span data-ttu-id="ca70a-129">폼 인증을 사용 하 여 web API</span><span class="sxs-lookup"><span data-stu-id="ca70a-129">Using Forms Authentication with Web API</span></span>

<span data-ttu-id="ca70a-130">폼 인증을 사용 하는 응용 프로그램을 만들려면 "인터넷 응용 프로그램" 템플릿은 MVC 4 프로젝트 마법사에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-130">To create an application that uses forms authentication, select the "Internet Application" template in the MVC 4 project wizard.</span></span> <span data-ttu-id="ca70a-131">이 템플릿은 계정 관리에 대 한 MVC 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-131">This template creates MVC controllers for account management.</span></span> <span data-ttu-id="ca70a-132">또한 ASP.NET Fall 2012 업데이트에서 사용할 수 있는 "단일 페이지 응용 프로그램" 서식 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-132">You can also use the "Single Page Application" template, available in the ASP.NET Fall 2012 Update.</span></span>

<span data-ttu-id="ca70a-133">web API 컨트롤러를 사용 하 여 액세스를 제한할 수는 `[Authorize]` 특성에 설명 된 대로 [[Authorize] 특성을 사용 하 여](authentication-and-authorization-in-aspnet-web-api.md#auth3)합니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-133">In your web API controllers, you can restrict access by using the `[Authorize]` attribute, as described in [Using the [Authorize] Attribute](authentication-and-authorization-in-aspnet-web-api.md#auth3).</span></span>

<span data-ttu-id="ca70a-134">폼 인증 요청을 인증 하는 세션 쿠키를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-134">Forms-authentication uses a session cookie to authenticate requests.</span></span> <span data-ttu-id="ca70a-135">브라우저가 자동으로 대상 웹 사이트에 모든 관련 쿠키를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-135">Browsers automatically send all relevant cookies to the destination web site.</span></span> <span data-ttu-id="ca70a-136">이 기능을 사용 하면 폼 인증 교차 사이트 요청 위조 (CSRF) 참조 공격에 취약할 수 [방지 교차 사이트 요청 위조 CSRF () 공격](preventing-cross-site-request-forgery-csrf-attacks.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-136">This feature makes forms authentication potentially vulnerable to cross-site request forgery (CSRF) attacks See [Preventing Cross-Site Request Forgery (CSRF) Attacks](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>

<span data-ttu-id="ca70a-137">폼 인증에서 사용자의 자격 증명을 암호화 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-137">Forms authentication does not encrypt the user's credentials.</span></span> <span data-ttu-id="ca70a-138">따라서 폼 인증 ssl을 사용 하지 않는 경우에 안전 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-138">Therefore, forms authentication is not secure unless used with SSL.</span></span> <span data-ttu-id="ca70a-139">참조 [Web API의에서 SSL 작업](working-with-ssl-in-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ca70a-139">See [Working with SSL in Web API](working-with-ssl-in-web-api.md).</span></span>
