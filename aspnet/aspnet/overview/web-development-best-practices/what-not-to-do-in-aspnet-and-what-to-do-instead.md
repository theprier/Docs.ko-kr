---
uid: aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
title: "Asp.net에서 수행할 작업을 하지 및 실행 | Microsoft Docs"
author: tfitzmac
description: "이 항목에서는 ASP.NET 웹 프로젝트 내에서 사용자를 확인 하는 몇 가지 일반적인 실수를 설명 합니다. 이러한 commo를 방지 하기 위해 수행 해야 하는 것에 대 한 권장 사항을 제공..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/08/2014
ms.topic: article
ms.assetid: c39b9965-545c-4b04-8f55-21be7f28a9e5
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
msc.type: authoredcontent
ms.openlocfilehash: 24c6a35a6b663ebb0f8d0e3e7988322fa5d9018c
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="what-not-to-do-in-aspnet-and-what-to-do-instead"></a><span data-ttu-id="15367-104">ASP.NET 및 대신 수행할 작업에서 작업을 수행 하지 않의 사항을</span><span class="sxs-lookup"><span data-stu-id="15367-104">What not to do in ASP.NET, and what to do instead</span></span>
====================
<span data-ttu-id="15367-105">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="15367-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="15367-106">이 항목에서는 ASP.NET 웹 프로젝트 내에서 사용자를 확인 하는 몇 가지 일반적인 실수를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-106">This topic describes several common mistakes people make within ASP.NET web projects.</span></span> <span data-ttu-id="15367-107">이러한 일반적인 실수를 방지 하기 위해 수행 해야 하는 것에 대 한 권장 사항을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-107">It provides recommendations for what you should do to avoid these common mistakes.</span></span> <span data-ttu-id="15367-108">에 기반 하는 한 [프레젠테이션](http://vimeo.com/68390507) 여 **Damian Edwards** 노르웨이어 개발자가 회의에 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-108">It is based on a [presentation](http://vimeo.com/68390507) by **Damian Edwards** at Norwegian Developers Conference.</span></span>


## <a name="disclaimer"></a><span data-ttu-id="15367-109">고지 사항</span><span class="sxs-lookup"><span data-stu-id="15367-109">Disclaimer</span></span>

<span data-ttu-id="15367-110">이 항목은 응용 프로그램을 안전 하 고 효율적인를 완벽 가이드로 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-110">This topic is not intended as a complete guide to ensure your application is secure and efficient.</span></span> <span data-ttu-id="15367-111">이 항목에서 설명 하지 보안 및 성능에 대 한 모범 사례에 따라 여전히 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-111">You still need to follow best practices for security and performance that are not outlined in this topic.</span></span> <span data-ttu-id="15367-112">만.NET 클래스 및 프로세스와 관련 된 일반적인 실수를 방지 하는 방법을 제안 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-112">It only suggests how to avoid common mistakes related to .NET classes and processes.</span></span>

## <a name="overview"></a><span data-ttu-id="15367-113">개요</span><span class="sxs-lookup"><span data-stu-id="15367-113">Overview</span></span>

<span data-ttu-id="15367-114">이 항목에는 다음과 같은 단원이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-114">This topic contains the following sections:</span></span>

- [<span data-ttu-id="15367-115">표준 준수</span><span class="sxs-lookup"><span data-stu-id="15367-115">Standards Compliance</span></span>](#standards)

    - [<span data-ttu-id="15367-116">컨트롤 어댑터</span><span class="sxs-lookup"><span data-stu-id="15367-116">Control Adapters</span></span>](#adapters)
    - [<span data-ttu-id="15367-117">컨트롤의 스타일 속성</span><span class="sxs-lookup"><span data-stu-id="15367-117">Style Properties on Controls</span></span>](#styleprop)
    - [<span data-ttu-id="15367-118">페이지 및 컨트롤 콜백을</span><span class="sxs-lookup"><span data-stu-id="15367-118">Page and Control Callbacks</span></span>](#callback)
    - [<span data-ttu-id="15367-119">브라우저 기능 검색</span><span class="sxs-lookup"><span data-stu-id="15367-119">Browser Capability Detection</span></span>](#browsercap)
- [<span data-ttu-id="15367-120">보안</span><span class="sxs-lookup"><span data-stu-id="15367-120">Security</span></span>](#security)

    - [<span data-ttu-id="15367-121">요청 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="15367-121">Request Validation</span></span>](#validation)
    - [<span data-ttu-id="15367-122">Cookieless 폼 인증 및 세션</span><span class="sxs-lookup"><span data-stu-id="15367-122">Cookieless Forms Authentication and Session</span></span>](#cookieless)
    - [<span data-ttu-id="15367-123">EnableViewStateMac</span><span class="sxs-lookup"><span data-stu-id="15367-123">EnableViewStateMac</span></span>](#viewstatemac)
    - [<span data-ttu-id="15367-124">보통 신뢰</span><span class="sxs-lookup"><span data-stu-id="15367-124">Medium Trust</span></span>](#medium)
    - [<span data-ttu-id="15367-125">&lt;appSettings&gt;</span><span class="sxs-lookup"><span data-stu-id="15367-125">&lt;appSettings&gt;</span></span>](#appsettings)
    - [<span data-ttu-id="15367-126">UrlPathEncode</span><span class="sxs-lookup"><span data-stu-id="15367-126">UrlPathEncode</span></span>](#urlpathencode)
- [<span data-ttu-id="15367-127">안정성 및 성능</span><span class="sxs-lookup"><span data-stu-id="15367-127">Reliability and Performance</span></span>](#performance)

    - [<span data-ttu-id="15367-128">PreSendRequestHeaders 및 PreSendRequestContext</span><span class="sxs-lookup"><span data-stu-id="15367-128">PreSendRequestHeaders and PreSendRequestContext</span></span>](#presend)
    - [<span data-ttu-id="15367-129">Web Forms 사용 하 여 비동기 페이지 이벤트</span><span class="sxs-lookup"><span data-stu-id="15367-129">Asynchronous Page Events with Web Forms</span></span>](#asyncevents)
    - [<span data-ttu-id="15367-130">실행 하 고 잊어 작업</span><span class="sxs-lookup"><span data-stu-id="15367-130">Fire-and-Forget Work</span></span>](#fire)
    - [<span data-ttu-id="15367-131">요청 엔터티 본문</span><span class="sxs-lookup"><span data-stu-id="15367-131">Request Entity Body</span></span>](#requestentity)
    - [<span data-ttu-id="15367-132">명확한 Response.Redirect 및 Response.End</span><span class="sxs-lookup"><span data-stu-id="15367-132">Response.Redirect and Response.End</span></span>](#redirect)
    - [<span data-ttu-id="15367-133">EnableViewState 및 ViewStateMode</span><span class="sxs-lookup"><span data-stu-id="15367-133">EnableViewState and ViewStateMode</span></span>](#viewstatemode)
    - [<span data-ttu-id="15367-134">SqlMembershipProvider</span><span class="sxs-lookup"><span data-stu-id="15367-134">SqlMembershipProvider</span></span>](#sqlprovider)
    - [<span data-ttu-id="15367-135">긴 실행 요청 (> 110 초)</span><span class="sxs-lookup"><span data-stu-id="15367-135">Long Running Requests (>110 seconds)</span></span>](#long)

<a id="standards"></a>

## <a name="standards-compliance"></a><span data-ttu-id="15367-136">표준 준수</span><span class="sxs-lookup"><span data-stu-id="15367-136">Standards Compliance</span></span>

<a id="adapters"></a>

### <a name="control-adapters"></a><span data-ttu-id="15367-137">컨트롤 어댑터</span><span class="sxs-lookup"><span data-stu-id="15367-137">Control Adapters</span></span>

<span data-ttu-id="15367-138">권장 사항: 컨트롤 어댑터를 사용 하 여 자동 선택 렌더링을 중지 하 고 대신 표준 규격 HTML 및 CSS 미디어 쿼리를 사용 하 여 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="15367-138">Recommendation: Stop using control adapters for adaptive rendering, and instead use CSS media queries and standards-compliant HTML.</span></span>

<span data-ttu-id="15367-139">컨트롤 어댑터는 다양 한 장치 및 환경에 대 한 사용자 지정 프레젠테이션 코드를 표시할.NET 2.0에서 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-139">Controls Adapters were introduced in .NET 2.0 to render presentation code that was customized for different devices and environments.</span></span> <span data-ttu-id="15367-140">이제, HTML 및 CSS와이 자동 선택 렌더링을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-140">Now, this adaptive rendering can be accomplished with CSS and HTML.</span></span> <span data-ttu-id="15367-141">컨트롤 어댑터 사용을 중지 하 고 HTML 및 CSS를 기존 어댑터를 모두 변환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-141">You should stop using Control Adapters and convert any existing adapters to CSS and HTML.</span></span>

<span data-ttu-id="15367-142">자세한 내용은 참조 [미디어 쿼리](http://www.w3.org/TR/css3-mediaqueries/) 및 [How To: Your ASP.NET Web Forms에 모바일 페이지 추가 / MVC 응용 프로그램](../../../whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-142">For more information, see [Media Queries](http://www.w3.org/TR/css3-mediaqueries/) and [How To: Add Mobile Pages to Your ASP.NET Web Forms / MVC Application](../../../whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application.md).</span></span>

<a id="styleprop"></a>

### <a name="style-properties-on-controls"></a><span data-ttu-id="15367-143">컨트롤의 스타일 속성</span><span class="sxs-lookup"><span data-stu-id="15367-143">Style Properties on Controls</span></span>

<span data-ttu-id="15367-144">권장 사항: 컨트롤 태그에 스타일 값을 설정 멈추고 대신 CSS 스타일 시트에서 형식 지정 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-144">Recommendation: Stop setting style values in the control markup, and instead set formatting values in CSS stylesheets.</span></span>

<span data-ttu-id="15367-145">웹 서버 컨트롤에는 수십 개의 인라인 스타일 속성을 설정 하는 데 사용할 수 있는 속성이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15367-145">Web server controls contain dozens of properties which can be used to set in-line style properties.</span></span> <span data-ttu-id="15367-146">예를 들어 ForeColor 속성 컨트롤에 대 한 텍스트의 색을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-146">For example, the ForeColor property sets the color of the text for a control.</span></span> <span data-ttu-id="15367-147">CSS 스타일 시트를 통해 보다 효율적으로이 동일한 효과 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-147">You can accomplish this same effect more efficiently through CSS stylesheets.</span></span> <span data-ttu-id="15367-148">스타일 시트를 사용 하 여 응용 프로그램에서 이러한 값을 설정 하지 마십시오 및 스타일 값을 중앙 집중화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-148">Stylesheets enable you to centralize style values and avoid setting these values throughout your application.</span></span>

<span data-ttu-id="15367-149">다음 예제에서는 CSS 클래스를 빨강 집합 텍스트를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15367-149">The following example shows a CSS class the sets text to red.</span></span>

[!code-css[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample1.css)]

<span data-ttu-id="15367-150">다음 예제에는 CSS 클래스를 동적으로 적용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15367-150">The next example shows how to dynamically apply the CSS class.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample2.cs)]

<a id="callback"></a>

### <a name="page-and-control-callbacks"></a><span data-ttu-id="15367-151">페이지 및 컨트롤 콜백을</span><span class="sxs-lookup"><span data-stu-id="15367-151">Page and Control Callbacks</span></span>

<span data-ttu-id="15367-152">권장 사항: 페이지 및 컨트롤 콜백을 사용 중지 하 고 대신 다음 중 하나를 사용 하 여: AJAX, UpdatePanel, MVC 동작 메서드, 웹 API 또는 SignalR 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-152">Recommendation: Stop using page and control callbacks, and instead use any of the following: AJAX, UpdatePanel, MVC action methods, Web API, or SignalR.</span></span>

<span data-ttu-id="15367-153">이전 버전의 ASP.NET 페이지 및 컨트롤 콜백 메서드를 사용 전체 페이지를 새로 고치지 않고는 웹 페이지의 일부를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-153">In earlier versions of ASP.NET, Page and Control callback methods enabled you to update part of the web page without refreshing an entire page.</span></span> <span data-ttu-id="15367-154">이제 부분 페이지 업데이트를 통해 수행할 수 있는 [AJAX](../../../ajax/index.md), [UpdatePanel](https://msdn.microsoft.com/en-US/library/bb386454.aspx), [MVC](../../../mvc/index.md), [웹 API](../../../web-api/index.md) 또는 [SignalR](../../../signalr/index.md).</span><span class="sxs-lookup"><span data-stu-id="15367-154">You can now accomplish partial-page updates through [AJAX](../../../ajax/index.md), [UpdatePanel](https://msdn.microsoft.com/en-US/library/bb386454.aspx), [MVC](../../../mvc/index.md), [Web API](../../../web-api/index.md) or [SignalR](../../../signalr/index.md).</span></span> <span data-ttu-id="15367-155">친화적 Url로 문제가 발생할 수 있으므로 콜백 메서드를 사용 하 여 및 라우팅 중지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-155">You should stop using callback methods because they can cause issues with friendly URLs and routing.</span></span> <span data-ttu-id="15367-156">기본적으로 컨트롤에 콜백 메서드를 사용 하지 않는 있지만 컨트롤에서이 기능을 사용 하도록 설정한 경우 파일을 비활성화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-156">By default, controls do not enable callback methods, but if you enabled this feature in a control, you should disable it.</span></span>

<a id="browsercap"></a>

### <a name="browser-capability-detection"></a><span data-ttu-id="15367-157">브라우저 기능 검색</span><span class="sxs-lookup"><span data-stu-id="15367-157">Browser Capability Detection</span></span>

<span data-ttu-id="15367-158">권장 사항: 정적 브라우저 기능 검색을 사용 하 여 중지 하 고 대신 동적 기능 감지를 사용 하 여 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="15367-158">Recommendation: Stop using static browser capability detection, and instead use dynamic feature detection.</span></span>

<span data-ttu-id="15367-159">이전 버전의 ASP.NET에서는 지원 되는 각 브라우저에 대 한 기능 XML 파일에 저장 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-159">In earlier versions of ASP.NET, the supported features for each browser were stored in an XML file.</span></span> <span data-ttu-id="15367-160">정적 조회를 통해 검색 기능 지원 가장 좋은 방법이 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-160">Detecting feature support through a static lookup is not the best approach.</span></span> <span data-ttu-id="15367-161">이제, 검색할 수 있습니다 동적으로 브라우저에서 같은 기능 검색 프레임 워크를 사용 하 여 지 원하는 기능 [Modernizr](http://modernizr.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-161">Now, you can dynamically detect a browser's supported features by using a feature detection framework, such as [Modernizr](http://modernizr.com/).</span></span> <span data-ttu-id="15367-162">기능 검색 메서드 또는 속성을 사용 하 고 브라우저 원하는 결과 생성 하는 경우 참조를 확인 하 여 지원을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-162">Feature detection determines support by attempting to use a method or property and then checking to see if the browser produced the desired result.</span></span> <span data-ttu-id="15367-163">기본적으로 Modernizr 웹 응용 프로그램 서식 파일에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15367-163">By default, Modernizr is included in the Web application templates.</span></span>

<a id="security"></a>

## <a name="security"></a><span data-ttu-id="15367-164">보안</span><span class="sxs-lookup"><span data-stu-id="15367-164">Security</span></span>

<a id="validation"></a>

### <a name="request-validation"></a><span data-ttu-id="15367-165">요청 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="15367-165">Request Validation</span></span>

<span data-ttu-id="15367-166">권장 사항: 사용자 입력의 유효성을 검사 하 고 사용자의 출력 인코딩.</span><span class="sxs-lookup"><span data-stu-id="15367-166">Recommendation: Validate user input, and encode output from users.</span></span>

<span data-ttu-id="15367-167">요청 유효성 검사는 각 요청을 검사 하 고 인식된 위협이 발견 된 경우 요청을 중지 하는 ASP.NET의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="15367-167">Request validation is a feature of ASP.NET that inspects each request and stops the request if a perceived threat is found.</span></span> <span data-ttu-id="15367-168">사이트 간 스크립팅 공격에 대 한 응용 프로그램 보안에 대 한 요청 유효성 검사에 종속 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-168">Do not depend on request validation for securing your application against cross-site scripting attacks.</span></span> <span data-ttu-id="15367-169">대신 사용자의 모든 입력의 유효성을 검사 하 고 출력을 인코딩하십시오.</span><span class="sxs-lookup"><span data-stu-id="15367-169">Instead, validate all input from users and encode the output.</span></span> <span data-ttu-id="15367-170">일부 제한 된 경우에서에 입력 유효성 검사 정규식을 사용할 수 있습니다 하지만 값과 일치 하는 경우를 결정 하는.NET 클래스를 사용 하 여 사용자 입력 유효성을 검사 해야 하는 더 복잡 한 경우에 값을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-170">In some limited cases, you can use regular expressions to validate the input, but in more complicated cases you should validate user input by using .NET classes that determine if the value matches allowed values.</span></span>

<span data-ttu-id="15367-171">다음 예제에서는 사용자가 제공 하는 Uri 올바른지 여부를 확인 하려면 Uri 클래스의 정적 메서드를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15367-171">The following example shows how to use a static method in the Uri class to determine whether the Uri provided by a user is valid.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample3.cs)]

<span data-ttu-id="15367-172">그러나 Uri를 충분히 확인 하는 경우에 확인 해야 지정 하는지 확인 하려면 `http` 또는 `https`합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-172">However, to sufficiently verify the Uri, you should also check to make sure it specifies `http` or `https`.</span></span> <span data-ttu-id="15367-173">다음 예제에서는 Uri가 유효한 지 확인 하려면 인스턴스 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-173">The following example uses instance methods to verify that the Uri is valid.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample4.cs)]

<span data-ttu-id="15367-174">사용자 입력 HTML로 렌더링 또는 사용자 입력을 포함 하 여 SQL 쿼리에서를 하기 전에 악성 코드가 포함 되지 않습니다. 되도록 값을 인코딩하십시오.</span><span class="sxs-lookup"><span data-stu-id="15367-174">Before rendering user input as HTML or including user input in a SQL query, encode the values to ensure malicious code is not included.</span></span>

<span data-ttu-id="15367-175">HTML 수 사용 하 여 태그에 값을 인코드는 &lt;%: %&gt; 아래와 같이 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="15367-175">You can HTML encode the value in markup with the &lt;%: %&gt; syntax, as shown below.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample5.aspx?highlight=1)]

<span data-ttu-id="15367-176">또는 Razor 구문으로 수행할 수 있습니다 HTML로 인코딩 @ 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-176">Or, in Razor syntax, you can HTML encode with @, as shown below.</span></span>

[!code-cshtml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample6.cshtml?highlight=1)]

<span data-ttu-id="15367-177">다음 예제와 방법을 HTML로 인코딩 코드 숨김에서 값입니다.</span><span class="sxs-lookup"><span data-stu-id="15367-177">The next example shows how to HTML encode a value in code-behind.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample7.cs)]

<span data-ttu-id="15367-178">SQL 명령에 대 한 값을 안전 하 게 인코딩하려면 명령 매개 변수 사용 등의 [SqlParameter](https://msdn.microsoft.com/en-us/library/system.data.sqlclient.sqlparameter.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-178">To safely encode a value for SQL commands, use command parameters such as the [SqlParameter](https://msdn.microsoft.com/en-us/library/system.data.sqlclient.sqlparameter.aspx).</span></span> <a id="cookieless"></a>

### <a name="cookieless-forms-authentication-and-session"></a><span data-ttu-id="15367-179">Cookieless 폼 인증 및 세션</span><span class="sxs-lookup"><span data-stu-id="15367-179">Cookieless Forms Authentication and Session</span></span>

<span data-ttu-id="15367-180">권장 사항: 쿠키 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-180">Recommendation: Require cookies.</span></span>

<span data-ttu-id="15367-181">쿼리 문자열의 인증 정보를 전달 안전 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-181">Passing authentication information in the query string is not secure.</span></span> <span data-ttu-id="15367-182">응용 프로그램에 인증 하는 경우에 따라서 쿠키를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-182">Therefore, require cookies when your application includes authentication.</span></span> <span data-ttu-id="15367-183">중요 한 정보를 저장 하는 여 쿠키를 쿠키에 SSL을 필요로 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-183">If your cookie stores sensitive information, consider requiring SSL for the cookie.</span></span>

<span data-ttu-id="15367-184">다음 예제에서는 폼 인증에서는 SSL을 통해 전송 되는 쿠키를 해야 하는 Web.config 파일에 지정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15367-184">The following example shows how to specify in the Web.config file that Forms Authentication requires a cookie that is transmitted over SSL.</span></span>

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample8.xml)]

<a id="viewstatemac"></a>

### <a name="enableviewstatemac"></a><span data-ttu-id="15367-185">EnableViewStateMac</span><span class="sxs-lookup"><span data-stu-id="15367-185">EnableViewStateMac</span></span>

<span data-ttu-id="15367-186">권장 사항: 되지 false로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-186">Recommendation: Never set to false.</span></span>

<span data-ttu-id="15367-187">기본적으로 EnbableViewStateMac 설정을 true로 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-187">By default, EnbableViewStateMac is set to true.</span></span> <span data-ttu-id="15367-188">응용 프로그램 뷰 상태를 사용 하지 않는 경우에 EnableViewStateMac false로 설정 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="15367-188">Even if your application is not using view state, do not set EnableViewStateMac to false.</span></span> <span data-ttu-id="15367-189">이 값을 false로 설정 하면 응용 프로그램 사이트 간 스크립팅에 취약 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15367-189">Setting this value to false will make your application vulnerable to cross-site scripting.</span></span>

<span data-ttu-id="15367-190">런타임에서 적용 ASP.NET 4.5.2 부터는 **EnableViewStateMac = true**합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-190">Starting with ASP.NET 4.5.2, the runtime enforces **EnableViewStateMac=true**.</span></span> <span data-ttu-id="15367-191">False로 설정 하는 경우에 런타임은이 값을 무시 하 고 true로 설정 된 값으로 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15367-191">Even if you set it to false, the runtime ignores this value and proceeds with the value set to true.</span></span> <span data-ttu-id="15367-192">자세한 내용은 참조 [ASP.NET 4.5.2 및 EnableViewStateMac](https://blogs.msdn.com/b/webdev/archive/2014/05/07/asp-net-4-5-2-and-enableviewstatemac.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-192">For more information, see [ASP.NET 4.5.2 and EnableViewStateMac](https://blogs.msdn.com/b/webdev/archive/2014/05/07/asp-net-4-5-2-and-enableviewstatemac.aspx).</span></span>

<span data-ttu-id="15367-193">다음 예제에서는 EnableViewStateMac true로 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15367-193">The following example shows how to set EnableViewStateMac to true.</span></span> <span data-ttu-id="15367-194">실제로이 값을 기본적으로 true 이기 때문에 true로 설정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-194">You do not need to actually set this value to true because it is true by default.</span></span> <span data-ttu-id="15367-195">그러나 설정한 false로 아무 페이지에서 응용 프로그램에서이 값을 수정 즉시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-195">However, if you have set it to false on any page in your application, you must immediately correct this value.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample9.aspx)]

<a id="medium"></a>

### <a name="medium-trust"></a><span data-ttu-id="15367-196">보통 신뢰</span><span class="sxs-lookup"><span data-stu-id="15367-196">Medium Trust</span></span>

<span data-ttu-id="15367-197">권장 사항: 보안 경계로 보통 신뢰 (또는 다른 신뢰 수준)에 종속 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-197">Recommendation: Do not depend on Medium Trust (or any other trust level) as a security boundary.</span></span>

<span data-ttu-id="15367-198">부분 신뢰 응용 프로그램을 적절 하 게 보호 하지 않습니다 및 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-198">Partial trust does not adequately protect your application and should not be used.</span></span> <span data-ttu-id="15367-199">대신, 완전 신뢰를 사용 하 고 별도 응용 프로그램 풀에서 신뢰할 수 없는 응용 프로그램을 격리 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-199">Instead, use Full Trust, and isolate untrusted applications in separate application pools.</span></span> <span data-ttu-id="15367-200">또한 고유 id 아래에서 각 응용 프로그램 풀을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-200">Also, run each application pool under a unique identity.</span></span> <span data-ttu-id="15367-201">자세한 내용은 참조 [ASP.NET 부분 신뢰 응용 프로그램 격리를 보장 하지 않습니다](https://support.microsoft.com/kb/2698981)합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-201">For more information, see [ASP.NET Partial Trust does not guarantee application isolation](https://support.microsoft.com/kb/2698981).</span></span>

<a id="appsettings"></a>

### <a name="ltappsettingsgt"></a><span data-ttu-id="15367-202">&lt;appSettings&gt;</span><span class="sxs-lookup"><span data-stu-id="15367-202">&lt;appSettings&gt;</span></span>

<span data-ttu-id="15367-203">권장 사항:의 보안 설정 해제 하지 않으면 &lt;appSettings&gt; 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="15367-203">Recommendation: Do not disable security settings in &lt;appSettings&gt; element.</span></span>

<span data-ttu-id="15367-204">AppSettings 요소는 보안 업데이트에 필요한 많은 값을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-204">The appSettings element contains many values which are required for security updates.</span></span> <span data-ttu-id="15367-205">하지 변경 하거나 이러한 값을 사용 하지 않도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-205">You should not change or disable these values.</span></span> <span data-ttu-id="15367-206">업데이트를 배포할 때 이러한 값을 해제 해야 하는 경우 즉시 다시 설정 배포를 완료 한 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-206">If you must disable these values when deploying an update, immediately re-enable after completing deployment.</span></span>

<span data-ttu-id="15367-207">자세한 내용은 참조 [ASP.NET appSettings 요소](https://msdn.microsoft.com/en-us/library/hh975440.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-207">For details, see [ASP.NET appSettings Element](https://msdn.microsoft.com/en-us/library/hh975440.aspx).</span></span>

<a id="urlpathencode"></a>

### <a name="urlpathencode"></a><span data-ttu-id="15367-208">UrlPathEncode</span><span class="sxs-lookup"><span data-stu-id="15367-208">UrlPathEncode</span></span>

<span data-ttu-id="15367-209">권장 사항: 사용 [UrlEncode](https://msdn.microsoft.com/en-us/library/zttxte6w.aspx) 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-209">Recommendation: Use [UrlEncode](https://msdn.microsoft.com/en-us/library/zttxte6w.aspx) instead.</span></span>

<span data-ttu-id="15367-210">UrlPathEncode 메서드는 매우 구체적인 브라우저 호환성 문제를 해결 하려면.NET Framework에 대 한 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-210">The UrlPathEncode method was added to the .NET Framework to resolve a very specific browser compatibility problem.</span></span> <span data-ttu-id="15367-211">적절 한 URL를 인코딩하지 않습니다 하 고 사이트 간 스크립팅에서 응용 프로그램을 보호 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-211">It does not adequately encode a URL, and does not protect your application from cross-site scripting.</span></span> <span data-ttu-id="15367-212">하지 응용 프로그램에서 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-212">You should never use it in your application.</span></span> <span data-ttu-id="15367-213">대신를 사용 하 여 [UrlEncode](https://msdn.microsoft.com/en-us/library/zttxte6w.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-213">Instead, use [UrlEncode](https://msdn.microsoft.com/en-us/library/zttxte6w.aspx).</span></span>

<span data-ttu-id="15367-214">다음 예제에서는 인코딩된 URL 하이퍼링크 컨트롤에 대 한 쿼리 문자열 매개 변수로 전달 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15367-214">The following example shows how to pass an encoded URL as a query string parameter for a hyperlink control.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample10.cs)]

<a id="performance"></a>

## <a name="reliability-and-performance"></a><span data-ttu-id="15367-215">안정성 및 성능</span><span class="sxs-lookup"><span data-stu-id="15367-215">Reliability and Performance</span></span>

<a id="presend"></a>

### <a name="presendrequestheaders-and-presendrequestcontext"></a><span data-ttu-id="15367-216">PreSendRequestHeaders 및 PreSendRequestContext</span><span class="sxs-lookup"><span data-stu-id="15367-216">PreSendRequestHeaders and PreSendRequestContext</span></span>

<span data-ttu-id="15367-217">권장 사항: 관리 되는 모듈 함께 이러한 이벤트를 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="15367-217">Recommendation: Do not use these events with managed modules.</span></span> <span data-ttu-id="15367-218">대신, 필요한 작업을 수행 하는 네이티브 IIS 모듈을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-218">Instead, write a native IIS module to perform the required task.</span></span> <span data-ttu-id="15367-219">참조 [네이티브 코드 HTTP 모듈을 만들고](https://msdn.microsoft.com/en-us/library/ms693629.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-219">See [Creating Native-Code HTTP Modules](https://msdn.microsoft.com/en-us/library/ms693629.aspx).</span></span>

<span data-ttu-id="15367-220">사용할 수는 [PreSendRequestHeaders](https://msdn.microsoft.com/en-us/library/system.web.httpapplication.presendrequestheaders.aspx) 및 [PreSendRequestContext](https://msdn.microsoft.com/en-us/library/system.web.httpapplication.presendrequestcontent.aspx) 네이티브 IIS 모듈을 사용 하 여 이벤트 하지만 IHttpModule을 구현 하는 관리 되는 모듈을 함께 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="15367-220">You can use the [PreSendRequestHeaders](https://msdn.microsoft.com/en-us/library/system.web.httpapplication.presendrequestheaders.aspx) and [PreSendRequestContext](https://msdn.microsoft.com/en-us/library/system.web.httpapplication.presendrequestcontent.aspx) events with native IIS modules, but do not use them with managed modules that implement IHttpModule.</span></span> <span data-ttu-id="15367-221">이러한 속성을 설정 비동기 요청에 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-221">Setting these properties can cause issues with asynchronous requests.</span></span>

<a id="asyncevents"></a>

### <a name="asynchronous-page-events-with-web-forms"></a><span data-ttu-id="15367-222">Web Forms 사용 하 여 비동기 페이지 이벤트</span><span class="sxs-lookup"><span data-stu-id="15367-222">Asynchronous Page Events with Web Forms</span></span>

<span data-ttu-id="15367-223">권장 사항: Web Forms에서 하지 않도록 비동기 페이지 수명 주기 이벤트에 대 한 void 메서드를 작성 하 고 대신 사용 하 여 [Page.RegisterAsyncTask](https://msdn.microsoft.com/en-us/library/system.web.ui.page.registerasynctask.aspx) 비동기 코드에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-223">Recommendation: In Web Forms, avoid writing async void methods for Page lifecycle events, and instead use [Page.RegisterAsyncTask](https://msdn.microsoft.com/en-us/library/system.web.ui.page.registerasynctask.aspx) for asynchronous code.</span></span>

<span data-ttu-id="15367-224">포함 된 페이지 이벤트를 표시 하는 경우 **비동기** 및 **void**,이 비동기 코드를 완료할 때 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-224">When you mark a page event with **async** and **void**, you cannot determine when the asynchronous code has finished.</span></span> <span data-ttu-id="15367-225">대신, Page.RegisterAsyncTask를 사용 하 여 완료를 추적할 수 있도록 하는 방법에서 비동기 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-225">Instead, use Page.RegisterAsyncTask to run the asynchronous code in a way that enables you to track its completion.</span></span>

<span data-ttu-id="15367-226">단추는 다음 예제에서는 비동기 코드를 포함 하는 처리기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-226">The following example shows a button click handler that contains asynchronous code.</span></span> <span data-ttu-id="15367-227">이 예에서는 권장 되는 방법은 아닌 비동기 작업의 간단한 예제로만 제공 하는 문자열 값을 비동기적으로 읽는 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15367-227">This example includes reading a string value asynchronously, which is provided only as a simplified example of an asynchronous task and not as a recommended practice.</span></span>

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample11.cs)]

<span data-ttu-id="15367-228">비동기 작업을 사용 하는 경우 Web.config 파일에 Http 런타임 대상 프레임 워크가 4.5로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-228">If you are using asynchronous Tasks, set the Http runtime target framework to 4.5 in the Web.config file.</span></span> <span data-ttu-id="15367-229">대상 프레임 워크를으로 설정 설정 4.5는 새 동기화 컨텍스트에서.NET 4.5에서 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-229">Setting the target framework to 4.5 turns on the new synchronization context that was added in .NET 4.5.</span></span> <span data-ttu-id="15367-230">이 값은 Visual Studio 2012에서 새 프로젝트에서 기본적으로 설정 되지만 수 설정 기존 프로젝트를 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="15367-230">This value is set by default in new projects in Visual Studio 2012, but is not be set if you are working with an existing project.</span></span>

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample12.xml)]

<a id="fire"></a>

### <a name="fire-and-forget-work"></a><span data-ttu-id="15367-231">실행 하 고 잊어 작업</span><span class="sxs-lookup"><span data-stu-id="15367-231">Fire-and-Forget Work</span></span>

<span data-ttu-id="15367-232">권장 사항: 내의 ASP.NET 요청을 처리할 때에--합니다 (이러한 ThreadPool.QueueUserWorkItem이 메서드를 호출 또는 작업 대리자를 반복적으로 호출 하는 타이머를 만드는) 시작 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-232">Recommendation: When handling a request within ASP.NET, avoid launching fire-and-forget work (such calling the ThreadPool.QueueUserWorkItem method or creating a timer that repeatedly calls a delegate).</span></span>

<span data-ttu-id="15367-233">응용 프로그램의 응용 프로그램에 ASP.NET 내에서 실행 되 고 잊어 화재 작업 동기화 가져올 수 있습니다. 언제 든 지 응용 프로그램 도메인 제거할 수 없습니다. 진행 중인 프로세스에 응용 프로그램의 현재 상태를 더 이상 일치 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-233">If your application has fire-and-forget work that runs within ASP.NET, your application can get out of sync. At any time, the app domain can be destroyed which means your ongoing process may no longer match the current state of the application.</span></span>

<span data-ttu-id="15367-234">이 유형의 ASP.NET 외부에서 작업을 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-234">You should move this type of work outside of ASP.NET.</span></span> <span data-ttu-id="15367-235">진행 중인 작업을 수행 하려면 Azure에서 웹 작업, Windows 서비스 또는 작업자 역할을 사용 하 고 다른 프로세스에서 해당 코드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-235">You can use a Web Jobs, Windows Service or a Worker role in Azure to perform ongoing work, and run that code from another process.</span></span>

<span data-ttu-id="15367-236">ASP.NET 내에서이 작업을 수행 해야 하는 경우 호출 하는 Nuget 패키지를 추가할 수 있습니다 [WebBackgrounder](http://www.nuget.org/packages/webbackgrounder) 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-236">If you must perform this work within ASP.NET, you can add the Nuget package called [WebBackgrounder](http://www.nuget.org/packages/webbackgrounder) to run the code.</span></span>

<a id="requestentity"></a>

### <a name="request-entity-body"></a><span data-ttu-id="15367-237">요청 엔터티 본문</span><span class="sxs-lookup"><span data-stu-id="15367-237">Request Entity Body</span></span>

<span data-ttu-id="15367-238">권장 사항: 처리기의 이벤트를 실행 하기 전에 Request.Form 또는 Request.InputStream를 읽는 것을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-238">Recommendation: Avoid reading Request.Form or Request.InputStream before the handler's execute event.</span></span>

<span data-ttu-id="15367-239">가능한 한 빨리 Request.Form 또는 Request.InputStream에서 읽어야 하는 처리기에서 이벤트를 실행할 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-239">The earliest you should read from Request.Form or Request.InputStream is during the handler's execute event.</span></span> <span data-ttu-id="15367-240">MVC 컨트롤러 처리기 이며 동작 메서드가 실행 될 때 execute 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="15367-240">In MVC, the Controller is the handler and the execute event is when the action method runs.</span></span> <span data-ttu-id="15367-241">Web Forms 페이지가 처리기 고 Page.Init 이벤트가 발생할 때의 execute 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="15367-241">In Web Forms, the Page is the handler and the execute event is when the Page.Init event fires.</span></span> <span data-ttu-id="15367-242">Execute 이벤트 이전에 요청 엔터티 본문을 읽는 경우 방해 하는 요청을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-242">If you read the request entity body earlier than the execute event, you interfere with the processing of the request.</span></span>

<span data-ttu-id="15367-243">Execute 이벤트 이전에 요청 엔터티 본문을 읽는 데 필요한 경우 사용 하 여 [Request.GetBufferlessInputStream](https://msdn.microsoft.com/en-us/library/ff406798.aspx) 또는 [Request.GetBufferedInputStream](https://msdn.microsoft.com/en-us/library/system.web.httprequest.getbufferedinputstream.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-243">If you need to read the request entity body before the execute event, use either [Request.GetBufferlessInputStream](https://msdn.microsoft.com/en-us/library/ff406798.aspx) or [Request.GetBufferedInputStream](https://msdn.microsoft.com/en-us/library/system.web.httprequest.getbufferedinputstream.aspx).</span></span> <span data-ttu-id="15367-244">GetBufferlessInputStream를 사용 하면 원시 스트림을 요청에서 가져오고 전체 요청을 처리 하는 것에 대 한 책임 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-244">When you use GetBufferlessInputStream, you get the raw stream from the request, and assume responsibility for processing the entire request.</span></span> <span data-ttu-id="15367-245">GetBufferlessInputStream를 호출한 후 Request.Form 및 Request.InputStream 사용할 수 없는 채워지지 않은 ASP.NET에서 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-245">After calling GetBufferlessInputStream, Request.Form and Request.InputStream are not available because they have not been populated by ASP.NET.</span></span> <span data-ttu-id="15367-246">GetBufferedInputStream를 사용 하는 경우 요청에서 스트림의 복사본을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="15367-246">When you use GetBufferedInputStream, you get a copy of the stream from the request.</span></span> <span data-ttu-id="15367-247">ASP.NET 다른 복사본을 채우므로 Request.Form 및 Request.InputStream 요청에서 나중에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-247">Request.Form and Request.InputStream are still available later in the request because ASP.NET populates the other copy.</span></span>

<a id="redirect"></a>

### <a name="responseredirect-and-responseend"></a><span data-ttu-id="15367-248">명확한 Response.Redirect 및 Response.End</span><span class="sxs-lookup"><span data-stu-id="15367-248">Response.Redirect and Response.End</span></span>

<span data-ttu-id="15367-249">권장 사항: 호출한 후 스레드가 처리 하는 방법을의 차이에 주의 [Response.Redirect(String)](https://msdn.microsoft.com/en-us/library/t9dwyts4.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-249">Recommendation: Be aware of differences in how thread is handled after calling [Response.Redirect(String)](https://msdn.microsoft.com/en-us/library/t9dwyts4.aspx).</span></span>

<span data-ttu-id="15367-250">[Response.Redirect(String)](https://msdn.microsoft.com/en-us/library/t9dwyts4.aspx) 메서드 Response.End 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-250">The [Response.Redirect(String)](https://msdn.microsoft.com/en-us/library/t9dwyts4.aspx) method calls the Response.End method.</span></span> <span data-ttu-id="15367-251">동기 프로세스 Request.Redirect를 호출 하면 현재 스레드를 즉시 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15367-251">In a synchronous process, calling Request.Redirect causes the current thread to immediately abort.</span></span> <span data-ttu-id="15367-252">그러나 비동기 프로세스에서 Response.Redirect를 호출 하면 중단 되지 않는 현재 스레드 코드 실행이 요청에 대해 계속 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-252">However, in an asynchronous process, calling Response.Redirect does not abort the current thread, so code execution continues for the request.</span></span> <span data-ttu-id="15367-253">비동기 프로세스에서 코드 실행을 중지 하는 메서드의 작업을 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-253">In an asynchronous process, you must return the Task from the method to stop the code execution.</span></span>

<span data-ttu-id="15367-254">MVC 프로젝트 Response.Redirect를 호출 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-254">In an MVC project, you should not call Response.Redirect.</span></span> <span data-ttu-id="15367-255">된 RedirectResult를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-255">Instead, return a RedirectResult.</span></span>

<a id="viewstatemode"></a>

### <a name="enableviewstate-and-viewstatemode"></a><span data-ttu-id="15367-256">EnableViewState 및 ViewStateMode</span><span class="sxs-lookup"><span data-stu-id="15367-256">EnableViewState and ViewStateMode</span></span>

<span data-ttu-id="15367-257">권장 사항: 사용 ViewStateMode EnableViewState 매길 컨트롤 뷰 상태를 사용 하는 세분화 된 제어를 제공 하는 대신, 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-257">Recommendation: Use ViewStateMode, instead of EnableViewState, to provide granular control over which controls use view state.</span></span>

<span data-ttu-id="15367-258">EnableViewState Page 지시문에서 false로 설정한 경우 뷰 상태 페이지 내에서 모든 컨트롤에 대해 비활성화 되 고 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-258">When you set EnableViewState to false in the Page directive, view state is disabled for all controls within the page and cannot be enabled.</span></span> <span data-ttu-id="15367-259">뷰 상태를 페이지의 특정 컨트롤에만 사용할 수 있도록 하려는 경우 페이지에 대 한 ViewStateMode 사용 안 함으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-259">If you want to enable view state for only certain controls in your page, set ViewStateMode to Disabled for the Page.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample13.aspx)]

<span data-ttu-id="15367-260">실제 뷰 상태를 필요한 컨트롤에 ViewStateMode 사용으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-260">Then, set ViewStateMode to Enabled on only the controls that actually need view state.</span></span>

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample14.aspx)]

<span data-ttu-id="15367-261">뷰 상태를 필요로 하는 컨트롤에 대해서만 사용 하면 웹 페이지에 대 한 상태 보기의 크기를 축소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-261">By enabling view state for only the controls that need it, you can shrink the size of the view state for your web pages.</span></span>

<a id="sqlprovider"></a>

### <a name="sqlmembershipprovider"></a><span data-ttu-id="15367-262">SqlMembershipProvider</span><span class="sxs-lookup"><span data-stu-id="15367-262">SqlMembershipProvider</span></span>

<span data-ttu-id="15367-263">권장 사항: Universal Providers를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-263">Recommendation: Use Universal Providers.</span></span>

<span data-ttu-id="15367-264">현재 프로젝트 템플릿에서 SqlMembershipProvider로 대체 되었습니다 [ASP.NET Universal Providers](http://www.nuget.org/packages/Microsoft.AspNet.Providers), NuGet 패키지로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-264">In the current project templates, SqlMembershipProvider has been replaced by [ASP.NET Universal Providers](http://www.nuget.org/packages/Microsoft.AspNet.Providers), which is available as a NuGet package.</span></span> <span data-ttu-id="15367-265">SqlMembershipProvider 템플릿의 이전 버전으로 작성 된 프로젝트를 사용 하는 경우 Universal Providers 하도록 전환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-265">If you are using SqlMembershipProvider in a project that was built with an earlier version of the templates, you should switch to Universal Providers.</span></span> <span data-ttu-id="15367-266">유니버설 공급자는 Entity Framework에서 지원 되는 모든 데이터베이스와 함께 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-266">The Universal Providers work with all databases that are supported by Entity Framework.</span></span>

<span data-ttu-id="15367-267">자세한 내용은 참조 [Introducing ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-267">For more information, see [Introducing ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx).</span></span>

<a id="long"></a>

### <a name="long-running-requests-110-seconds"></a><span data-ttu-id="15367-268">장기 실행 요청 (> 110 초)</span><span class="sxs-lookup"><span data-stu-id="15367-268">Long-running Requests (>110 seconds)</span></span>

<span data-ttu-id="15367-269">권장 사항: 사용 [Websocket](https://msdn.microsoft.com/en-us/library/system.net.websockets.websocket.aspx) 또는 [SignalR](../../../signalr/index.md) 연결 된 클라이언트 및 사용 하 여 비동기 I/O 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-269">Recommendation: Use [WebSockets](https://msdn.microsoft.com/en-us/library/system.net.websockets.websocket.aspx) or [SignalR](../../../signalr/index.md) for connected clients, and use asynchronous I/O operations.</span></span>

<span data-ttu-id="15367-270">장기 실행 요청 웹 응용 프로그램에서 예기치 않은 결과 및 성능 저하를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-270">Long-running requests can cause unpredictable results and poor performance in your web application.</span></span> <span data-ttu-id="15367-271">요청에 대 한 기본 시간 제한 설정을 110 초입니다.</span><span class="sxs-lookup"><span data-stu-id="15367-271">The default timeout setting for a request is 110 seconds.</span></span> <span data-ttu-id="15367-272">세션 상태를 사용 하는 장기 실행 요청으로, ASP.NET 세션 개체에 대 한 잠금을 110 초 후 해제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15367-272">If you are using session state with a long-running request, ASP.NET will release the lock on the Session object after 110 seconds.</span></span> <span data-ttu-id="15367-273">그러나 잠금이 해제 되 고 작업을 성공적으로 완료 되지 않을 수 있습니다 때 세션 개체에 대 한 작업 중에 응용 프로그램 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-273">However, your application might be in the middle of an operation on the Session object when the lock is released, and the operation might not complete successfully.</span></span> <span data-ttu-id="15367-274">첫 번째 요청이 실행 되는 동안 사용자의 두 번째 요청을 차단 된 경우 두 번째 요청 일관성 없는 상태로 세션 개체를 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-274">If a second request from the user is blocked while the first request is running, the second request might access the Session object in an inconsistent state.</span></span>

<span data-ttu-id="15367-275">응용 프로그램 차단 (또는 동기) I/O 작업을 포함 하는 경우 응용 프로그램 응답 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-275">If your application includes blocking (or synchronous) I/O operations, the application will be unresponsive.</span></span>

<span data-ttu-id="15367-276">성능 향상을 위해.NET Framework에서 비동기 I/O 작업을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-276">To improve performance, use the asynchronous I/O operations in the .NET Framework.</span></span> <span data-ttu-id="15367-277">또한 서버에 연결 하는 클라이언트에 대 한 Websocket 또는 SignalR를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15367-277">Also, use WebSockets or SignalR for connecting clients to the server.</span></span> <span data-ttu-id="15367-278">이러한 기능은 효율적으로 장기 실행 요청을 처리 하도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15367-278">These features are designed to efficiently handle long-running requests.</span></span>
