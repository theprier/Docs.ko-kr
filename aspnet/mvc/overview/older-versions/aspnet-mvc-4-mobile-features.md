---
uid: mvc/overview/older-versions/aspnet-mvc-4-mobile-features
title: ASP.NET MVC 4 모바일 기능 | Microsoft Docs
author: Rick-Anderson
description: 이제 ASP.NET MVC 5 모바일 웹 응용 프로그램에서 Azure 웹 사이트 배포에서 코드 샘플을 사용 하 여이 자습서는 MVC 5 버전이입니다.
ms.author: riande
ms.date: 08/15/2012
ms.assetid: 27dc4fc8-1b51-43b0-933f-fc1b52476523
msc.legacyurl: /mvc/overview/older-versions/aspnet-mvc-4-mobile-features
msc.type: authoredcontent
ms.openlocfilehash: 6fe55a14b40f8c50dee91cdc7f59d0378f2a1ea2
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "48912334"
---
<a name="aspnet-mvc-4-mobile-features"></a><span data-ttu-id="d998a-103">ASP.NET MVC 4 모바일 기능</span><span class="sxs-lookup"><span data-stu-id="d998a-103">ASP.NET MVC 4 Mobile Features</span></span>
====================
<span data-ttu-id="d998a-104">[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="d998a-104">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

> <span data-ttu-id="d998a-105">이제는 MVC 5의 버전이이 자습서에서 샘플 코드 [ASP.NET MVC 5 모바일 웹 응용 프로그램이 Azure 웹 사이트에서 배포](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-105">There is now an MVC 5 version of this tutorial with code samples at [Deploy an ASP.NET MVC 5 Mobile Web Application on Azure Web Sites](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/).</span></span>


<span data-ttu-id="d998a-106">이 자습서는 ASP.NET MVC 4 웹 응용 프로그램에서 모바일 기능을 사용 하는 방법의 기본 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-106">This tutorial will teach you the basics of how to work with mobile features in an ASP.NET MVC 4 Web application.</span></span> <span data-ttu-id="d998a-107">이 자습서에서는 사용할 수 있습니다 [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) 또는 Visual Web Developer 2010 Express 서비스 팩 1 (&quot;VWD 또는 Visual Web Developer&quot;).</span><span class="sxs-lookup"><span data-stu-id="d998a-107">For this tutorial, you can use [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) or Visual Web Developer 2010 Express Service Pack 1 (&quot;Visual Web Developer or VWD&quot;).</span></span> <span data-ttu-id="d998a-108">이미 있는 경우 Visual Studio professional 버전을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-108">You can use the professional version of Visual Studio if you already have that.</span></span>

<span data-ttu-id="d998a-109">시작 하기 전에 아래에 나열 된 필수 구성 요소를 설치한 다음 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-109">Before you start, make sure you've installed the prerequisites listed below.</span></span>

- <span data-ttu-id="d998a-110">[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) (권장) 또는 Visual Studio Web Developer Express SP1.</span><span class="sxs-lookup"><span data-stu-id="d998a-110">[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) (recommended) or Visual Studio Web Developer Express SP1.</span></span> <span data-ttu-id="d998a-111">Visual Studio 2012에 ASP.NET MVC 4 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-111">Visual Studio 2012 contains ASP.NET MVC 4.</span></span> <span data-ttu-id="d998a-112">Visual Web Developer 2010를 사용 하는 경우 설치 해야 [ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392)합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-112">If you are using Visual Web Developer 2010, you must install [ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392).</span></span>

<span data-ttu-id="d998a-113">모바일 브라우저 에뮬레이터를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-113">You will also need a mobile browser emulator.</span></span> <span data-ttu-id="d998a-114">다음 중 하나라도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-114">Any of the following will work:</span></span>

- <span data-ttu-id="d998a-115">[Windows 7 Phone 에뮬레이터](https://msdn.microsoft.com/library/ff402563(VS.92).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-115">[Windows 7 Phone Emulator](https://msdn.microsoft.com/library/ff402563(VS.92).aspx).</span></span> <span data-ttu-id="d998a-116">(이 자습서에서는 대부분의 스크린 샷 사용 되는 에뮬레이터입니다.)</span><span class="sxs-lookup"><span data-stu-id="d998a-116">(This is the emulator that's used in most of the screen shots in this tutorial.)</span></span>
- <span data-ttu-id="d998a-117">IPhone을 에뮬레이트하는 데 사용자 에이전트 문자열을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-117">Change the user agent string to emulate an iPhone.</span></span> <span data-ttu-id="d998a-118">참조 [이](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) 블로그 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-118">See [this](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) blog entry.</span></span>
- [<span data-ttu-id="d998a-119">Opera Mobile 에뮬레이터</span><span class="sxs-lookup"><span data-stu-id="d998a-119">Opera Mobile Emulator</span></span>](http://www.opera.com/developer/tools/mobile/)
- <span data-ttu-id="d998a-120">[Apple Safari](http://www.apple.com/safari/download/) iPhone로 사용자 에이전트를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-120">[Apple Safari](http://www.apple.com/safari/download/) with the user agent set to iPhone.</span></span> <span data-ttu-id="d998a-121">Safari에서 사용자 에이전트를 "iPhone"로 하는 방법에 대 한 지침을 참조 하세요 [하도록 Safari IE 것으로 가정 하는 방법을](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) David Alison 블로그.</span><span class="sxs-lookup"><span data-stu-id="d998a-121">For instructions on how to set the user agent in Safari to "iPhone", see [How to let Safari pretend it's IE](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) on David Alison's blog.</span></span>

<span data-ttu-id="d998a-122">C# 소스 코드를 사용 하 여 visual Studio 프로젝트는 다음이 항목과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-122">Visual Studio projects with C# source code are available to accompany this topic:</span></span>

- [<span data-ttu-id="d998a-123">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="d998a-123">Starter project download</span></span>](https://go.microsoft.com/fwlink/?linkid=228307&amp;clcid=0x409)
- [<span data-ttu-id="d998a-124">완성 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="d998a-124">Completed project download</span></span>](https://go.microsoft.com/fwlink/?linkid=228306&amp;clcid=0x409)

### <a name="what-youll-build"></a><span data-ttu-id="d998a-125">만들 내용</span><span class="sxs-lookup"><span data-stu-id="d998a-125">What You'll Build</span></span>

<span data-ttu-id="d998a-126">이 자습서에서는 추가 모바일 기능에 제공 된 간단한 회의 목록 응용 프로그램에는 [시작 프로젝트](https://go.microsoft.com/fwlink/?LinkId=228307)합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-126">For this tutorial, you'll add mobile features to the simple conference-listing application that's provided in the [starter project](https://go.microsoft.com/fwlink/?LinkId=228307).</span></span> <span data-ttu-id="d998a-127">다음 스크린샷은 완성된 된 응용 프로그램의 태그 페이지에서 볼 수 있듯이 합니다 [Windows 7 Phone Emulator](https://msdn.microsoft.com/library/ff402563(VS.92).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-127">The following screenshot shows the tags page of the completed application as seen in the [Windows 7 Phone Emulator](https://msdn.microsoft.com/library/ff402563(VS.92).aspx).</span></span> <span data-ttu-id="d998a-128">참조 [키보드 매핑에 대 한 Windows Phone 에뮬레이터](https://msdn.microsoft.com/library/ff754352(v=vs.92).aspx) 키보드 입력을 단순화 하기 위해.</span><span class="sxs-lookup"><span data-stu-id="d998a-128">See [Keyboard Mapping for Windows Phone Emulator](https://msdn.microsoft.com/library/ff754352(v=vs.92).aspx) to simplify keyboard input.</span></span>

<span data-ttu-id="d998a-129">[![p1_Tags_CompletedProj](aspnet-mvc-4-mobile-features/_static/image2.png)](aspnet-mvc-4-mobile-features/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d998a-129">[![p1_Tags_CompletedProj](aspnet-mvc-4-mobile-features/_static/image2.png)](aspnet-mvc-4-mobile-features/_static/image1.png)</span></span>

<span data-ttu-id="d998a-130">Internet Explorer 9 또는 10, FireFox 또는 Chrome을 설정 하 여 모바일 응용 프로그램을 개발 하는 버전을 사용할 수는 [사용자 에이전트 문자열](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-130">You can use Internet Explorer version 9 or 10, FireFox or Chrome to develop your mobile application by setting the [user agent string](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/).</span></span> <span data-ttu-id="d998a-131">다음 이미지에서는 iPhone을 에뮬레이션 하는 Internet Explorer를 사용 하 여 완성된 된 자습서를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-131">The following image shows the completed tutorial using Internet Explorer emulating an iPhone.</span></span> <span data-ttu-id="d998a-132">Internet Explorer F-12 개발자 도구를 사용할 수 있습니다 및 [Fiddler 도구](http://www.fiddler2.com/fiddler2/) 응용 프로그램을 디버깅할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-132">You can use the Internet Explorer F-12 developer tools and the [Fiddler tool](http://www.fiddler2.com/fiddler2/) to help debug your application.</span></span>

![](aspnet-mvc-4-mobile-features/_static/image3.png)

### <a name="skills-youll-learn"></a><span data-ttu-id="d998a-133">학습할 기술</span><span class="sxs-lookup"><span data-stu-id="d998a-133">Skills You'll Learn</span></span>

<span data-ttu-id="d998a-134">학습할 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-134">Here's what you'll learn:</span></span>

- <span data-ttu-id="d998a-135">ASP.NET MVC 4 템플릿인 HTML5를 사용 하는 방법을 `viewport` 특성 및 개선 하기 위해 적응형 렌더링 모바일 장치를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-135">How the ASP.NET MVC 4 templates use the HTML5 `viewport` attribute and adaptive rendering to improve display on mobile devices.</span></span>
- <span data-ttu-id="d998a-136">모바일 전용 뷰를 만드는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-136">How to create mobile-specific views.</span></span>
- <span data-ttu-id="d998a-137">모바일 보기 및 응용 프로그램의 데스크톱 보기 사이 해당 사용 사용자 전환 뷰 전환기를 만드는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-137">How to create a view switcher that lets users toggle between a mobile view and a desktop view of the application.</span></span>

### <a name="getting-started"></a><span data-ttu-id="d998a-138">시작</span><span class="sxs-lookup"><span data-stu-id="d998a-138">Getting Started</span></span>

<span data-ttu-id="d998a-139">다음 링크를 사용 하 여 시작 프로젝트에 대 한 회의 목록 응용 프로그램을 다운로드 합니다. [다운로드](https://go.microsoft.com/fwlink/?LinkId=228307)합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-139">Download the conference-listing application for the starter project using the following link: [Download](https://go.microsoft.com/fwlink/?LinkId=228307).</span></span> <span data-ttu-id="d998a-140">그런 다음 Windows 탐색기에서 마우스 오른쪽 단추로 클릭 합니다 *MvcMobile.zip* 파일을 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-140">Then in Windows Explorer, right-click the *MvcMobile.zip* file and choose **Properties**.</span></span> <span data-ttu-id="d998a-141">에 **MvcMobile.zip 속성** 대화 상자를 선택 합니다 **차단 해제** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-141">In the **MvcMobile.zip Properties** dialog box, choose the **Unblock** button.</span></span> <span data-ttu-id="d998a-142">(사용 하려고 할 때 발생 하는 보안 경고를 방지 차단 해제 된 *.zip* 웹에서 다운로드 한 파일입니다.)</span><span class="sxs-lookup"><span data-stu-id="d998a-142">(Unblocking prevents a security warning that occurs when you try to use a *.zip* file that you've downloaded from the web.)</span></span>

![p1_unBlock](aspnet-mvc-4-mobile-features/_static/image4.png)

<span data-ttu-id="d998a-144">마우스 오른쪽 단추로 클릭 합니다 *MvcMobile.zip* 파일을 선택 **풀기** 파일 압축을 풀 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-144">Right-click the *MvcMobile.zip* file and select **Extract All** to unzip the file.</span></span> <span data-ttu-id="d998a-145">Visual Studio에서 엽니다는 *MvcMobile.sln* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-145">In Visual Studio, open the *MvcMobile.sln* file.</span></span>

<span data-ttu-id="d998a-146">데스크톱 브라우저에서 표시 하는 응용 프로그램을 실행 하려면 CTRL + F5 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-146">Press CTRL+F5 to run the application, which will display it in your desktop browser.</span></span> <span data-ttu-id="d998a-147">모바일 브라우저 에뮬레이터를 시작 회의 응용 프로그램에 대 한 URL을 에뮬레이터에 복사한 다음를 클릭 합니다 **태그로 찾아보기** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-147">Start your mobile browser emulator, copy the URL for the conference application into the emulator, and then click the **Browse by tag** link.</span></span> <span data-ttu-id="d998a-148">Windows Phone 에뮬레이터를 사용 하는 경우 URL 표시줄에서 클릭 하 고 키보드 액세스를 일시 중지 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-148">If you are using the Windows Phone Emulator, click in the URL bar and press the Pause key to get keyboard access.</span></span> <span data-ttu-id="d998a-149">아래 이미지는 *AllTags* 보기 (선택 **태그로 찾아보기**).</span><span class="sxs-lookup"><span data-stu-id="d998a-149">The image below shows the *AllTags* view (from choosing **Browse by tag**).</span></span>

<span data-ttu-id="d998a-150">[![p1_browseTag](aspnet-mvc-4-mobile-features/_static/image6.png)](aspnet-mvc-4-mobile-features/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="d998a-150">[![p1_browseTag](aspnet-mvc-4-mobile-features/_static/image6.png)](aspnet-mvc-4-mobile-features/_static/image5.png)</span></span>

<span data-ttu-id="d998a-151">이 화면은 모바일 장치에서 가독성이 뛰어납니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-151">The display is very readable on a mobile device.</span></span> <span data-ttu-id="d998a-152">ASP.NET 링크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-152">Choose the ASP.NET link.</span></span>

<span data-ttu-id="d998a-153">[![p1_tagged_ASPNET](aspnet-mvc-4-mobile-features/_static/image8.png)](aspnet-mvc-4-mobile-features/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="d998a-153">[![p1_tagged_ASPNET](aspnet-mvc-4-mobile-features/_static/image8.png)](aspnet-mvc-4-mobile-features/_static/image7.png)</span></span>

<span data-ttu-id="d998a-154">ASP.NET 태그 뷰는 매우 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-154">The ASP.NET tag view is very cluttered.</span></span> <span data-ttu-id="d998a-155">예를 들어 합니다 **날짜** 열 읽기 하기가 매우 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-155">For example, the **Date** column is very difficult to read.</span></span> <span data-ttu-id="d998a-156">자습서 뒷부분에서의 버전을 만든 합니다 *AllTags* 모바일 브라우저에 맞게 이며 하 게 되 면 표시를 읽을 수 있는 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-156">Later in the tutorial you'll create a version of the *AllTags* view that's specifically for mobile browsers and that will make the display readable.</span></span>

<span data-ttu-id="d998a-157">참고: 현재 버그 모바일 캐싱 엔진 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-157">Note: Currently a bug exists in the mobile caching engine.</span></span> <span data-ttu-id="d998a-158">프로덕션 응용 프로그램을 설치 해야 합니다 [고정 DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) nugget 패키지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-158">For production applications, you must install the [Fixed DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) nugget package.</span></span> <span data-ttu-id="d998a-159">참조 [ASP.NET MVC 4 모바일 캐싱 버그 고정](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) 수정 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-159">See [ASP.NET MVC 4 Mobile Caching Bug Fixed](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) for details on the fix.</span></span>

## <a name="css-media-queries"></a><span data-ttu-id="d998a-160">CSS 미디어 쿼리</span><span class="sxs-lookup"><span data-stu-id="d998a-160">CSS Media Queries</span></span>

<span data-ttu-id="d998a-161">[CSS 미디어 쿼리](http://www.w3.org/TR/css3-mediaqueries/) 는 미디어 형식에 대 한 CSS 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-161">[CSS media queries](http://www.w3.org/TR/css3-mediaqueries/) are an extension to CSS for media types.</span></span> <span data-ttu-id="d998a-162">그러면 특정 브라우저 (사용자 에이전트)에 대 한 기본 CSS 규칙을 재정의 하는 규칙을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-162">They allow you to create rules that override the default CSS rules for specific browsers (user agents).</span></span> <span data-ttu-id="d998a-163">모바일 브라우저를 대상으로 하는 CSS에 대 한 일반적인 규칙은 최대 화면 크기를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-163">A common rule for CSS that targets mobile browsers is defining the maximum screen size.</span></span> <span data-ttu-id="d998a-164">합니다 *Content\Site.css* 다음 미디어 쿼리를 포함 하는 새 ASP.NET MVC 4 인터넷 프로젝트를 만들 때 생성 되는 파일:</span><span class="sxs-lookup"><span data-stu-id="d998a-164">The *Content\Site.css* file that's created when you create a new ASP.NET MVC 4 Internet project contains the following media query:</span></span>

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample1.css)]

<span data-ttu-id="d998a-165">브라우저 창의 픽셀 이하로 850 픽셀 인 경우이 미디어 블록 내에서 CSS 규칙을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-165">If the browser window is 850 pixels wide or less, it will use the CSS rules inside this media block.</span></span> <span data-ttu-id="d998a-166">데스크톱 브라우저의 광범위 한 디스플레이 대 한 설계 된 기본 CSS 규칙 보다 작은 브라우저 (예: 모바일 브라우저)에서 HTML 콘텐츠를 더 나은 표시를 위해 다음과 같은 CSS 미디어 쿼리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-166">You can use CSS media queries like this to provide a better display of HTML content on small browsers (like mobile browsers) than the default CSS rules that are designed for the wider displays of desktop browsers.</span></span>

## <a name="the-viewport-meta-tag"></a><span data-ttu-id="d998a-167">뷰포트 메타 태그</span><span class="sxs-lookup"><span data-stu-id="d998a-167">The Viewport Meta Tag</span></span>

<span data-ttu-id="d998a-168">가상 브라우저 창 너비를 정의 하는 대부분의 모바일 브라우저 (합니다 *뷰포트*) 모바일 장치의 실제 너비 보다 훨씬 큰 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-168">Most mobile browsers define a virtual browser window width (the *viewport*) that's much larger than the actual width of the mobile device.</span></span> <span data-ttu-id="d998a-169">따라서 가상 표시 내의 전체 웹 페이지에 맞게 모바일 브라우저.</span><span class="sxs-lookup"><span data-stu-id="d998a-169">This allows mobile browsers to fit the entire web page inside the virtual display.</span></span> <span data-ttu-id="d998a-170">흥미로운 콘텐츠 사용자 확대 다음 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-170">Users can then zoom in on interesting content.</span></span> <span data-ttu-id="d998a-171">그러나 실제 장치 너비 뷰포트 너비를 설정 하는 경우 없습니다 확대/축소 되므로 필요한 경우 모바일 브라우저에서 적합 한 콘텐츠 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-171">However, if you set the viewport width to the actual device width, no zooming is required, because the content fits in the mobile browser.</span></span>

<span data-ttu-id="d998a-172">뷰포트 `<meta>` ASP.NET MVC 4 레이아웃 파일에서 태그를 장치 너비로 뷰포트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-172">The viewport `<meta>` tag in the ASP.NET MVC 4 layout file sets the viewport to the device width.</span></span> <span data-ttu-id="d998a-173">다음 줄은 뷰포트를 보여 줍니다. `<meta>` ASP.NET MVC 4 레이아웃 파일의 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-173">The following line shows the viewport `<meta>` tag in the ASP.NET MVC 4 layout file.</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample2.html)]

## <a name="examining-the-effect-of-css-media-queries-and-the-viewport-meta-tag"></a><span data-ttu-id="d998a-174">CSS 미디어 쿼리 및 뷰포트 Meta 태그의 효과 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-174">Examining the Effect of CSS Media Queries and the Viewport Meta Tag</span></span>

<span data-ttu-id="d998a-175">엽니다는 *Views\Shared\\_Layout.cshtml* 뷰포트 주석 편집기에서 파일 `<meta>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-175">Open the *Views\Shared\\_Layout.cshtml* file in the editor and comment out the viewport `<meta>` tag.</span></span> <span data-ttu-id="d998a-176">다음 태그 주석 줄을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-176">The following markup shows the commented-out line.</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample3.cshtml)]

<span data-ttu-id="d998a-177">엽니다는 *MvcMobile\Content\Site.css* 편집기에서 파일 및 미디어 쿼리에서 최대 너비를 0 픽셀로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-177">Open the *MvcMobile\Content\Site.css* file in the editor and change the maximum width in the media query to zero pixels.</span></span> <span data-ttu-id="d998a-178">이렇게 하면 모바일 브라우저에서 사용 되는 CSS 규칙 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-178">This will prevent the CSS rules from being used in mobile browsers.</span></span> <span data-ttu-id="d998a-179">다음 줄에서는 수정 된 미디어 쿼리를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-179">The following line shows the modified media query:</span></span>

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample4.css)]

<span data-ttu-id="d998a-180">변경 내용을 저장 하 고 모바일 브라우저 에뮬레이터에서 회의 응용 프로그램으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-180">Save your changes and browse to the Conference application in a mobile browser emulator.</span></span> <span data-ttu-id="d998a-181">다음 이미지에 작은 텍스트는 뷰포트를 제거한 결과 `<meta>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-181">The tiny text in the following image is the result of removing the viewport `<meta>` tag.</span></span> <span data-ttu-id="d998a-182">하지 뷰포트를 사용 하 여 `<meta>` 태그 브라우저 축소 되어 기본 뷰포트 너비 (850 픽셀 또는 대부분의 모바일 브라우저에 대 한 광범위 한 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="d998a-182">With no viewport `<meta>` tag, the browser is zooming out to the default viewport width (850 pixels or wider for most mobile browsers.)</span></span>

<span data-ttu-id="d998a-183">[![p1_noViewPort](aspnet-mvc-4-mobile-features/_static/image10.png)](aspnet-mvc-4-mobile-features/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="d998a-183">[![p1_noViewPort](aspnet-mvc-4-mobile-features/_static/image10.png)](aspnet-mvc-4-mobile-features/_static/image9.png)</span></span>

<span data-ttu-id="d998a-184">변경 내용을 실행 취소-뷰포트를 주석 처리 제거 `<meta>` 레이아웃 파일에서 태그 및 850 픽셀을 미디어 쿼리를 복원 합니다 *Site.css* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-184">Undo your changes — uncomment the viewport `<meta>` tag in the layout file and restore the media query to 850 pixels in the *Site.css* file.</span></span> <span data-ttu-id="d998a-185">변경 내용을 저장 하 고 모바일 친화적인 디스플레이가 복원 되었는지 확인 하려면 모바일 브라우저를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-185">Save your changes and refresh the mobile browser to verify that the mobile-friendly display has been restored.</span></span>

<span data-ttu-id="d998a-186">뷰포트 `<meta>` 태그와 CSS 미디어 쿼리 관련이 없는 ASP.NET MVC 4 및 모든 웹 응용 프로그램에서 이러한 기능을 수행할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-186">The viewport `<meta>` tag and the CSS media query are not specific to ASP.NET MVC 4, and you can take advantage of these features in any web application.</span></span> <span data-ttu-id="d998a-187">하지만 이제 새 ASP.NET MVC 4 프로젝트를 만들 때 생성 되는 파일로 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-187">But they are now built into the files that are generated when you create a new ASP.NET MVC 4 project.</span></span>

<span data-ttu-id="d998a-188">뷰포트에 대 한 자세한 내용은 `<meta>` 태그를 참조 하십시오 [의 두 개의 뷰포트 A tale-2 부](http://www.quirksmode.org/mobile/viewports2.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-188">For more information about the viewport `<meta>` tag, see [A tale of two viewports — part two](http://www.quirksmode.org/mobile/viewports2.html).</span></span>

<span data-ttu-id="d998a-189">다음 섹션에서는 모바일 브라우저 전용 뷰를 제공 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-189">In the next section you'll see how to provide mobile-browser specific views.</span></span>

## <a name="overriding-views-layouts-and-partial-views"></a><span data-ttu-id="d998a-190">뷰, 레이아웃 및 부분 뷰 재정의</span><span class="sxs-lookup"><span data-stu-id="d998a-190">Overriding Views, Layouts, and Partial Views</span></span>

<span data-ttu-id="d998a-191">ASP.NET MVC 4의 중요 한 새로운 기능에는 모바일 브라우저는 개별 모바일 브라우저에 대 한 일반적으로 또는 특정 브라우저용 뷰 (레이아웃 및 부분 뷰 포함)를 재정의할 수 있도록 간단한 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-191">A significant new feature in ASP.NET MVC 4 is a simple mechanism that lets you override any view (including layouts and partial views) for mobile browsers in general, for an individual mobile browser, or for any specific browser.</span></span> <span data-ttu-id="d998a-192">모바일 전용 뷰를 제공 하려면 뷰 파일을 복사한 추가 *합니다. 모바일* 파일 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-192">To provide a mobile-specific view, you can copy a view file and add *.Mobile* to the file name.</span></span> <span data-ttu-id="d998a-193">예를 들어 모바일을 만들려는 *인덱스* 보기, 복사 *Views\Home\Index.cshtml* 하 *Views\Home\Index.Mobile.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-193">For example, to create a mobile *Index* view, copy *Views\Home\Index.cshtml* to *Views\Home\Index.Mobile.cshtml*.</span></span>

<span data-ttu-id="d998a-194">이 섹션에서는 모바일 전용 레이아웃 파일을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-194">In this section, you'll create a mobile-specific layout file.</span></span>

<span data-ttu-id="d998a-195">복사를 시작 하려면 *Views\Shared\\_Layout.cshtml* 하려면 *Views\Shared\\_Layout.Mobile.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-195">To start, copy *Views\Shared\\_Layout.cshtml* to *Views\Shared\\_Layout.Mobile.cshtml*.</span></span> <span data-ttu-id="d998a-196">오픈  *\_Layout.Mobile.cshtml* 에서 제목을 변경 하 고 **MVC4 회의** 하 **회의 (모바일)** 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-196">Open *\_Layout.Mobile.cshtml* and change the title from **MVC4 Conference** to **Conference (Mobile)**.</span></span>

<span data-ttu-id="d998a-197">각 `Html.ActionLink` 호출에서 "Browse by" 각 링크를 제거 *ActionLink*합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-197">In each `Html.ActionLink` call, remove "Browse by" in each link *ActionLink*.</span></span> <span data-ttu-id="d998a-198">다음 코드는 모바일 레이아웃 파일의 전체 본문 섹션을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-198">The following code shows the completed body section of the mobile layout file.</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample5.cshtml)]

<span data-ttu-id="d998a-199">복사 합니다 *Views\Home\AllTags.cshtml* 파일을 *Views\Home\AllTags.Mobile.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-199">Copy the *Views\Home\AllTags.cshtml* file to *Views\Home\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="d998a-200">새 파일을 열고 변경 된 `<h2>` 요소를 "Tags"를 "Tags (M)".</span><span class="sxs-lookup"><span data-stu-id="d998a-200">Open the new file and change the `<h2>` element from "Tags" to "Tags (M)":</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample6.html)]

<span data-ttu-id="d998a-201">데스크톱 브라우저 및 모바일 브라우저 에뮬레이터를 사용 하 여 태그 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-201">Browse to the tags page using a desktop browser and using mobile browser emulator.</span></span> <span data-ttu-id="d998a-202">모바일 브라우저 에뮬레이터에는 두 가지 변경 내용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-202">The mobile browser emulator shows the two changes you made.</span></span>

<span data-ttu-id="d998a-203">[![p2m_layoutTags.mobile](aspnet-mvc-4-mobile-features/_static/image12.png)](aspnet-mvc-4-mobile-features/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="d998a-203">[![p2m_layoutTags.mobile](aspnet-mvc-4-mobile-features/_static/image12.png)](aspnet-mvc-4-mobile-features/_static/image11.png)</span></span>

<span data-ttu-id="d998a-204">반대로 데스크톱 화면은 변경 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-204">In contrast, the desktop display has not changed.</span></span>

<span data-ttu-id="d998a-205">[![p2_layoutTagsDesktop](aspnet-mvc-4-mobile-features/_static/image14.png)](aspnet-mvc-4-mobile-features/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="d998a-205">[![p2_layoutTagsDesktop](aspnet-mvc-4-mobile-features/_static/image14.png)](aspnet-mvc-4-mobile-features/_static/image13.png)</span></span>

## <a name="browser-specific-views"></a><span data-ttu-id="d998a-206">브라우저 전용 뷰</span><span class="sxs-lookup"><span data-stu-id="d998a-206">Browser-Specific Views</span></span>

<span data-ttu-id="d998a-207">모바일 및 데스크톱 전용 뷰 외에도 개별 브라우저에 대 한 보기를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-207">In addition to mobile-specific and desktop-specific views, you can create views for an individual browser.</span></span> <span data-ttu-id="d998a-208">예를 들어 iPhone 브라우저에만 사용 되는 뷰를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-208">For example, you can create views that are specifically for the iPhone browser.</span></span> <span data-ttu-id="d998a-209">이 섹션에서는 iPhone 브라우저와의 iPhone 버전에 대 한 레이아웃을 만든 합니다 *AllTags* 보기.</span><span class="sxs-lookup"><span data-stu-id="d998a-209">In this section, you'll create a layout for the iPhone browser and an iPhone version of the *AllTags* view.</span></span>

<span data-ttu-id="d998a-210">엽니다는 *Global.asax* 파일과 다음 코드를 추가 합니다 `Application_Start` 메서드.</span><span class="sxs-lookup"><span data-stu-id="d998a-210">Open the *Global.asax* file and add the following code to the `Application_Start` method.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample7.cs)]

<span data-ttu-id="d998a-211">이 코드는 들어오는 각 요청에 맞출 "iPhone" 이라는 새로운 디스플레이 모드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-211">This code defines a new display mode named "iPhone" that will be matched against each incoming request.</span></span> <span data-ttu-id="d998a-212">들어오는 요청 (즉, 하는 경우 사용자 에이전트가 "iPhone" 문자열을 포함)를 정의한 조건과 일치 하는 경우 ASP.NET MVC는 이름에 "iPhone" 접미사가 포함 된 뷰를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-212">If the incoming request matches the condition you defined (that is, if the user agent contains the string "iPhone"), ASP.NET MVC will look for views whose name contains the "iPhone" suffix.</span></span>

<span data-ttu-id="d998a-213">코드에서 마우스 오른쪽 단추로 클릭 `DefaultDisplayMode`, 선택 **해결**를 선택한 후 `using System.Web.WebPages;`합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-213">In the code, right-click `DefaultDisplayMode`, choose **Resolve**, and then choose `using System.Web.WebPages;`.</span></span> <span data-ttu-id="d998a-214">에 대 한 참조를 추가 하는이 `System.Web.WebPages` 네임 스페이스에 위치를 `DisplayModes` 및 `DefaultDisplayMode` 유형이 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-214">This adds a reference to the `System.Web.WebPages` namespace, which is where the `DisplayModes` and `DefaultDisplayMode` types are defined.</span></span>

<span data-ttu-id="d998a-215">[![p2_resolve](aspnet-mvc-4-mobile-features/_static/image16.png)](aspnet-mvc-4-mobile-features/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="d998a-215">[![p2_resolve](aspnet-mvc-4-mobile-features/_static/image16.png)](aspnet-mvc-4-mobile-features/_static/image15.png)</span></span>

<span data-ttu-id="d998a-216">또는 다음 줄을 직접 추가할 수는 `using` 파일의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-216">Alternatively, you can just manually add the following line to the `using` section of the file.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample8.cs)]

<span data-ttu-id="d998a-217">전체 콘텐츠를 *Global.asax* 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-217">The complete contents of the *Global.asax* file is shown below.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample9.cs)]

<span data-ttu-id="d998a-218">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-218">Save the changes.</span></span> <span data-ttu-id="d998a-219">복사 합니다 *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* 파일을 *MvcMobile\Views\Shared\\_Layout.iPhone.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-219">Copy the *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* file to *MvcMobile\Views\Shared\\_Layout.iPhone.cshtml*.</span></span> <span data-ttu-id="d998a-220">새 파일을 열고 변경 합니다 `h1` 에서 제목 `Conference (Mobile)` 에 `Conference (iPhone)`입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-220">Open the new file and then change the `h1` heading from `Conference (Mobile)` to `Conference (iPhone)`.</span></span>

<span data-ttu-id="d998a-221">복사 합니다 *MvcMobile\Views\Home\AllTags.Mobile.cshtml* 파일을 *MvcMobile\Views\Home\AllTags.iPhone.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-221">Copy the *MvcMobile\Views\Home\AllTags.Mobile.cshtml* file to *MvcMobile\Views\Home\AllTags.iPhone.cshtml*.</span></span> <span data-ttu-id="d998a-222">새 파일에서 변경 된 `<h2>` 요소에서 "Tags (M)" "Tags (iPhone)"를 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-222">In the new file, change the `<h2>` element from "Tags (M)" to "Tags (iPhone)".</span></span>

<span data-ttu-id="d998a-223">응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-223">Run the application.</span></span> <span data-ttu-id="d998a-224">모바일 브라우저 에뮬레이터를 실행, 사용자 에이전트가 "iPhone"으로 설정 되어 있는지 확인 및 이동 합니다 *AllTags* 보기.</span><span class="sxs-lookup"><span data-stu-id="d998a-224">Run a mobile browser emulator, make sure its user agent is set to "iPhone", and browse to the *AllTags* view.</span></span> <span data-ttu-id="d998a-225">다음 스크린 샷에 표시 된 *AllTags* 보기에서 렌더링 합니다 [Safari](http://www.apple.com/safari/download/) 브라우저.</span><span class="sxs-lookup"><span data-stu-id="d998a-225">The following screenshot shows the *AllTags* view rendered in the [Safari](http://www.apple.com/safari/download/) browser.</span></span> <span data-ttu-id="d998a-226">Safari에 대 한 Windows를 다운로드할 수 있습니다 [여기](https://support.apple.com/kb/DL1531)합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-226">You can download Safari for Windows [here](https://support.apple.com/kb/DL1531).</span></span>

<span data-ttu-id="d998a-227">[![p2_iphoneView](aspnet-mvc-4-mobile-features/_static/image18.png)](aspnet-mvc-4-mobile-features/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="d998a-227">[![p2_iphoneView](aspnet-mvc-4-mobile-features/_static/image18.png)](aspnet-mvc-4-mobile-features/_static/image17.png)</span></span>

<span data-ttu-id="d998a-228">이 섹션에서는 모바일 레이아웃 및 뷰를 만드는 방법 및 레이아웃과 iPhone과 같은 특정 장치에 대 한 보기를 만드는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-228">In this section we've seen how to create mobile layouts and views and how to create layouts and views for specific devices such as the iPhone.</span></span> <span data-ttu-id="d998a-229">다음 섹션에서 더 많은 매력적인 모바일 보기에 대 한 jQuery Mobile을 활용 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-229">In the next section you'll see how to leverage jQuery Mobile for more compelling mobile views.</span></span>

## <a name="using-jquery-mobile"></a><span data-ttu-id="d998a-230">JQuery Mobile을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="d998a-230">Using jQuery Mobile</span></span>

<span data-ttu-id="d998a-231">합니다 [jQuery Mobile](http://jquerymobile.com/demos/1.0b3/#/demos/1.0b3/docs/about/intro.html) 라이브러리 모바일 브라우저는 모든 주요에서 작동 하는 사용자 인터페이스 프레임 워크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-231">The [jQuery Mobile](http://jquerymobile.com/demos/1.0b3/#/demos/1.0b3/docs/about/intro.html) library provides a user interface framework that works on all the major mobile browsers.</span></span> <span data-ttu-id="d998a-232">jQuery Mobile 적용 *점진적인 기능 향상* CSS 및 JavaScript를 지 원하는 모바일 브라우저에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-232">jQuery Mobile applies *progressive enhancement* to mobile browsers that support CSS and JavaScript.</span></span> <span data-ttu-id="d998a-233">점진적인 기능 향상에 모든 브라우저가 더 강력한 브라우저 및 장치를 다양 한 표시를 허용 하는 동안 웹 페이지의 기본 콘텐츠를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-233">Progressive enhancement allows all browsers to display the basic content of a web page, while allowing more powerful browsers and devices to have a richer display.</span></span> <span data-ttu-id="d998a-234">JQuery Mobile 사용 하 여 포함 된 JavaScript 및 CSS 파일에 태그를 변경 하지 않고 모바일 브라우저에 맞게 여러 요소 스타일입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-234">The JavaScript and CSS files that are included with jQuery Mobile style many elements to fit mobile browsers without making any markup changes.</span></span>

<span data-ttu-id="d998a-235">이 섹션에서는 설치를 *jQuery.Mobile.MVC* 뷰 전환기 위젯 및 jQuery Mobile을 설치 하는 NuGet 패키지.</span><span class="sxs-lookup"><span data-stu-id="d998a-235">In this section you'll install the *jQuery.Mobile.MVC* NuGet package, which installs jQuery Mobile and a view-switcher widget.</span></span>

<span data-ttu-id="d998a-236">삭제를 시작 하려면 합니다 *공유\\_Layout.Mobile.cshtml* 하 고 *공유\\_Layout.iPhone.cshtml* 이전에 만든 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-236">To start, delete the *Shared\\_Layout.Mobile.cshtml* and *Shared\\_Layout.iPhone.cshtml* files that you created earlier.</span></span>

<span data-ttu-id="d998a-237">이름 바꾸기 *Views\Home\AllTags.Mobile.cshtml* 하 고 *Views\Home\AllTags.iPhone.cshtml* 파일을 *Views\Home\AllTags.iPhone.cshtml.hide* 고  *Views\Home\AllTags.Mobile.cshtml.hide*합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-237">Rename *Views\Home\AllTags.Mobile.cshtml* and *Views\Home\AllTags.iPhone.cshtml* files to *Views\Home\AllTags.iPhone.cshtml.hide* and *Views\Home\AllTags.Mobile.cshtml.hide*.</span></span> <span data-ttu-id="d998a-238">파일이 더 이상 없으므로 *.cshtml* 확장을 렌더링 하는 ASP.NET MVC 런타임에서 사용 되지 않으므로 합니다 *AllTags* 보기.</span><span class="sxs-lookup"><span data-stu-id="d998a-238">Because the files no longer have a *.cshtml* extension, they won't be used by the ASP.NET MVC runtime to render the *AllTags* view.</span></span>

<span data-ttu-id="d998a-239">설치 합니다 *jQuery.Mobile.MVC* 이 수행 하 여 NuGet 패키지:</span><span class="sxs-lookup"><span data-stu-id="d998a-239">Install the *jQuery.Mobile.MVC* NuGet package by doing this:</span></span>

1. <span data-ttu-id="d998a-240">**도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 후 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-240">From the **Tools** menu, select **NuGet Package Manager**, and then select **Package Manager Console**.</span></span>

    <span data-ttu-id="d998a-241">[![p3_packageMgr](aspnet-mvc-4-mobile-features/_static/image20.png)](aspnet-mvc-4-mobile-features/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="d998a-241">[![p3_packageMgr](aspnet-mvc-4-mobile-features/_static/image20.png)](aspnet-mvc-4-mobile-features/_static/image19.png)</span></span>
2. <span data-ttu-id="d998a-242">에 **패키지 관리자 콘솔**, 입력 `Install-Package jQuery.Mobile.MVC -version 1.0.0`</span><span class="sxs-lookup"><span data-stu-id="d998a-242">In the **Package Manager Console**, enter `Install-Package jQuery.Mobile.MVC -version 1.0.0`</span></span>

<span data-ttu-id="d998a-243">다음 이미지는 추가 및 MvcMobile 프로젝트에 NuGet jQuery.Mobile.MVC 패키지에서 변경 된 파일을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-243">The following image shows the files added and changed to the MvcMobile project by the NuGet jQuery.Mobile.MVC package.</span></span> <span data-ttu-id="d998a-244">파일 이름 뒤에 오는 추가 [추가]가 추가 된 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-244">Files which are added have [add] appended after the file name.</span></span> <span data-ttu-id="d998a-245">이미지 GIF를 표시 하지 않습니다 하 고 PNG 파일을 추가 합니다 *Content\images* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-245">The image does not show the GIF and PNG files added to the *Content\images* folder.</span></span>

![](aspnet-mvc-4-mobile-features/_static/image21.png)

<span data-ttu-id="d998a-246">다음 jQuery.Mobile.MVC NuGet 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-246">The jQuery.Mobile.MVC NuGet package installs the following:</span></span>

- <span data-ttu-id="d998a-247">합니다 *앱\_Start\BundleMobileConfig.cs* 추가 jQuery JavaScript 및 CSS 파일을 참조 하는 데 필요한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-247">The *App\_Start\BundleMobileConfig.cs* file, which is needed to reference the jQuery JavaScript and CSS files added.</span></span> <span data-ttu-id="d998a-248">아래 지침에 따라를이 파일에 정의 된 모바일 번들을 참조 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-248">You must follow the instructions below and reference the mobile bundle defined in this file.</span></span>
- <span data-ttu-id="d998a-249">jQuery Mobile CSS 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-249">jQuery Mobile CSS files.</span></span>
- <span data-ttu-id="d998a-250">A `ViewSwitcher` 컨트롤러 위젯 (*Controllers\ViewSwitcherController.cs*).</span><span class="sxs-lookup"><span data-stu-id="d998a-250">A `ViewSwitcher` controller widget (*Controllers\ViewSwitcherController.cs*).</span></span>
- <span data-ttu-id="d998a-251">jQuery Mobile JavaScript 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-251">jQuery Mobile JavaScript files.</span></span>
- <span data-ttu-id="d998a-252">JQuery Mobile 스타일 레이아웃 파일 (*Views\Shared\\_Layout.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="d998a-252">A jQuery Mobile-styled layout file (*Views\Shared\\_Layout.Mobile.cshtml*).</span></span>
- <span data-ttu-id="d998a-253">뷰 전환기 부분 뷰 *(MvcMobile\Views\Shared\\_ViewSwitcher.cshtml*) 모바일 뷰로 이동 하 고 그 반대의 경우 바탕 화면 보기에서 전환 하려면 각 페이지의 맨 위에 있는 링크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-253">A view-switcher partial view *(MvcMobile\Views\Shared\\_ViewSwitcher.cshtml*) that provides a link at the top of each page to switch from desktop view to mobile view and vice versa.</span></span>
- <span data-ttu-id="d998a-254">여러<em>.png</em> 하 고 <em>.gif</em> 이미지 파일을 <em>Content\images</em> 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-254">Several<em>.png</em> and <em>.gif</em> image files in the <em>Content\images</em> folder.</span></span>

<span data-ttu-id="d998a-255">엽니다는 *Global.asax* 파일과 다음 코드의 마지막 줄으로 추가 `Application_Start` 메서드.</span><span class="sxs-lookup"><span data-stu-id="d998a-255">Open the *Global.asax* file and add the following code as the last line of the `Application_Start` method.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample10.cs)]

<span data-ttu-id="d998a-256">다음 코드에서는 전체 *Global.asax* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-256">The following code shows the complete *Global.asax* file.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample11.cs?highlight=26)]

> [!NOTE]
> <span data-ttu-id="d998a-257">Internet Explorer 9를 사용 하 고 표시 되지 않는 경우는 `BundleMobileConfig` 줄 위에 노란색 강조 표시를 클릭 합니다 [호환성 보기 단추](https://windows.microsoft.com/windows7/How-to-use-Compatibility-View-in-Internet-Explorer-9)![(해제) 호환성 뷰 단추 그림](http://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg " (해제) 호환성 뷰 단추 그림") 개요에서 변경 아이콘을 ie ![(해제) 호환성 뷰 단추 그림](http://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "(해제) 호환성 뷰 단추 그림 ") 단색 ![(켜기) 호환성 뷰 단추 그림](http://res1.windows.microsoft.com/resbox/en/Windows 7/main/156805ff-3130-481b-a12d-4d3a96470f36_14.jpg "(on) 호환성 뷰 단추 그림")합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-257">If you are using Internet Explorer 9 and you don't see the `BundleMobileConfig` line above in yellow highlight, click the [Compatibility View button](https://windows.microsoft.com/windows7/How-to-use-Compatibility-View-in-Internet-Explorer-9)![Picture of the Compatibility View button (off)](http://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "Picture of the Compatibility View button (off)") in IE to make the icon change from an outline ![Picture of the Compatibility View button (off)](http://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "Picture of the Compatibility View button (off)") to a solid color ![Picture of the Compatibility View button (on)](http://res1.windows.microsoft.com/resbox/en/Windows 7/main/156805ff-3130-481b-a12d-4d3a96470f36_14.jpg "Picture of the Compatibility View button (on)").</span></span> <span data-ttu-id="d998a-258">또는 FireFox 또는 Chrome에서이 자습서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-258">Alternatively you can view this tutorial in FireFox or Chrome.</span></span>


<span data-ttu-id="d998a-259">엽니다는 *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* 파일과 후 직접 다음 태그를 추가 합니다 `Html.Partial` 호출:</span><span class="sxs-lookup"><span data-stu-id="d998a-259">Open the *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* file and add the following markup directly after the `Html.Partial` call:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample12.cshtml)]

<span data-ttu-id="d998a-260">전체 *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-260">The complete *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* file is shown below:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample13.cshtml)]

<span data-ttu-id="d998a-261">응용 프로그램을 빌드하고 모바일 브라우저 에뮬레이터에서로 이동 합니다 *AllTags* 보기.</span><span class="sxs-lookup"><span data-stu-id="d998a-261">Build the application, and in your mobile browser emulator browse to the *AllTags* view.</span></span> <span data-ttu-id="d998a-262">다음 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-262">You see the following:</span></span>

<span data-ttu-id="d998a-263">[![p3_afterNuGet](aspnet-mvc-4-mobile-features/_static/image23.png)](aspnet-mvc-4-mobile-features/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="d998a-263">[![p3_afterNuGet](aspnet-mvc-4-mobile-features/_static/image23.png)](aspnet-mvc-4-mobile-features/_static/image22.png)</span></span>

> [!NOTE]
> <span data-ttu-id="d998a-264">특정 모바일 코드를 디버깅할 수 있습니다 [사용자 에이전트 문자열을 설정](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) IE 또는 iPhone 및 다음 F-12 개발자 도구를 사용 하 여 Chrome에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-264">You can debug the mobile specific code by [setting the user agent string](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) for IE or Chrome to iPhone and then using the F-12 developer tools.</span></span> <span data-ttu-id="d998a-265">모바일 브라우저가 표시 되지 않는 경우는 **홈**를 **발표자**를 **태그**, 및 **날짜** 단추 링크로, jQuery Mobile에 대 한 참조 스크립트 및 CSS 파일은 올바른 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-265">If your mobile browser doesn't display the **Home**, **Speaker**, **Tag**, and **Date** links as buttons, the references to jQuery Mobile scripts and CSS files are probably not correct.</span></span>


<span data-ttu-id="d998a-266">표시 스타일이 변경 하는 것 외에도 **모바일 보기 표시** 및 모바일 보기에서 데스크톱 보기로 전환할 수 있는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-266">In addition to the style changes, you see **Displaying mobile view** and a link that lets you switch from mobile view to desktop view.</span></span> <span data-ttu-id="d998a-267">선택 된 **바탕 화면 보기** 링크 및 바탕 화면 보기에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-267">Choose the **Desktop view** link, and the desktop view is displayed.</span></span>

<span data-ttu-id="d998a-268">[![p3_desktopView](aspnet-mvc-4-mobile-features/_static/image25.png)](aspnet-mvc-4-mobile-features/_static/image24.png)</span><span class="sxs-lookup"><span data-stu-id="d998a-268">[![p3_desktopView](aspnet-mvc-4-mobile-features/_static/image25.png)](aspnet-mvc-4-mobile-features/_static/image24.png)</span></span>

<span data-ttu-id="d998a-269">바탕 화면 보기에는 모바일 보기로 직접 이동 하는 방법을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-269">The desktop view doesn't provide a way to directly navigate back to the mobile view.</span></span> <span data-ttu-id="d998a-270">이제 수정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-270">You'll fix that now.</span></span> <span data-ttu-id="d998a-271">엽니다는 *Views\Shared\\_Layout.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-271">Open the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="d998a-272">페이지에서 방금 `body` 요소인 뷰 전환기 위젯을 렌더링 하는 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-272">Just under the page `body` element, add the following code, which renders the view-switcher widget:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample14.cshtml)]

<span data-ttu-id="d998a-273">새로 고침 합니다 *AllTags* 모바일 브라우저에서 보기.</span><span class="sxs-lookup"><span data-stu-id="d998a-273">Refresh the *AllTags* view in the mobile browser.</span></span> <span data-ttu-id="d998a-274">이제 데스크톱 및 모바일 뷰 간에 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-274">You can now navigate between desktop and mobile views.</span></span>

<span data-ttu-id="d998a-275">[![p3_desktopViewWithMobileLink](aspnet-mvc-4-mobile-features/_static/image27.png)](aspnet-mvc-4-mobile-features/_static/image26.png)</span><span class="sxs-lookup"><span data-stu-id="d998a-275">[![p3_desktopViewWithMobileLink](aspnet-mvc-4-mobile-features/_static/image27.png)](aspnet-mvc-4-mobile-features/_static/image26.png)</span></span>

> [!NOTE]
> <span data-ttu-id="d998a-276">참고 디버그:는 Views\Shared의 끝에 다음 코드를 추가할 수 있습니다\\_ViewSwitcher.cshtml 브라우저 사용자 에이전트 문자열을 사용 하 여 모바일 장치를 설정 하는 경우 뷰를 디버깅할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-276">Debug note: You can add the following code to the end of the Views\Shared\\_ViewSwitcher.cshtml to help debug views when using a browser the user agent string set to a mobile device.</span></span>
>
> [!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample15.cs)]
>
>  <span data-ttu-id="d998a-277">다음 머리글을 추가 합니다 *Views\Shared\\_Layout.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-277">and adding the following heading to the *Views\Shared\\_Layout.cshtml* file.</span></span>
>
> [!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample16.html)]


<span data-ttu-id="d998a-278">로 이동 합니다 *AllTags* 데스크톱 브라우저에서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-278">Browse to the *AllTags* page in a desktop browser.</span></span> <span data-ttu-id="d998a-279">뷰 전환기 위젯 모바일 레이아웃 페이지에만 추가 되므로 데스크톱 브라우저에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-279">The view-switcher widget is not displayed in a desktop browser because it's added only to the mobile layout page.</span></span> <span data-ttu-id="d998a-280">이 자습서의 뒷부분에 나오는 데스크톱 뷰로 뷰 전환기 위젯을 추가 하는 방법을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-280">Later in the tutorial you'll see how you can add the view-switcher widget to the desktop view.</span></span>

<span data-ttu-id="d998a-281">[![p3_desktopBrowser](aspnet-mvc-4-mobile-features/_static/image29.png)](aspnet-mvc-4-mobile-features/_static/image28.png)</span><span class="sxs-lookup"><span data-stu-id="d998a-281">[![p3_desktopBrowser](aspnet-mvc-4-mobile-features/_static/image29.png)](aspnet-mvc-4-mobile-features/_static/image28.png)</span></span>

## <a name="improving-the-speakers-list"></a><span data-ttu-id="d998a-282">발표자 목록 개선</span><span class="sxs-lookup"><span data-stu-id="d998a-282">Improving the Speakers List</span></span>

<span data-ttu-id="d998a-283">모바일 브라우저에서 선택 합니다 **발표자** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-283">In the mobile browser, select the **Speakers** link.</span></span> <span data-ttu-id="d998a-284">모바일 뷰가 있기 때문에 (*AllSpeakers.Mobile.cshtml*), 기본 발표자 표시 (*AllSpeakers.cshtml*) 모바일 레이아웃 뷰를 사용 하 여 렌더링 됩니다 ( *\_ Layout.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="d998a-284">Because there's no mobile view(*AllSpeakers.Mobile.cshtml*), the default speakers display (*AllSpeakers.cshtml*) is rendered using the mobile layout view (*\_Layout.Mobile.cshtml*).</span></span>

<span data-ttu-id="d998a-285">[![p3_speakersDeskTop](aspnet-mvc-4-mobile-features/_static/image31.png)](aspnet-mvc-4-mobile-features/_static/image30.png)</span><span class="sxs-lookup"><span data-stu-id="d998a-285">[![p3_speakersDeskTop](aspnet-mvc-4-mobile-features/_static/image31.png)](aspnet-mvc-4-mobile-features/_static/image30.png)</span></span>

<span data-ttu-id="d998a-286">렌더링 모바일 레이아웃 내에서 기본 (모바일 아님) 뷰를 설정 하 여 전역적으로 비활성화할 수 있습니다 `RequireConsistentDisplayMode` 에 `true` 에 *뷰\\_ViewStart.cshtml* 같이 파일:</span><span class="sxs-lookup"><span data-stu-id="d998a-286">You can globally disable a default (non-mobile) view from rendering inside a mobile layout by setting `RequireConsistentDisplayMode` to `true` in the *Views\\_ViewStart.cshtml* file, like this:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample17.cshtml)]

<span data-ttu-id="d998a-287">때 `RequireConsistentDisplayMode` 로 설정 된 `true`, 모바일 레이아웃 (<em>\_Layout.Mobile.cshtml</em>) 모바일 뷰에 대해서만 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-287">When `RequireConsistentDisplayMode` is set to `true`, the mobile layout (<em>\_Layout.Mobile.cshtml</em>) is used only for mobile views.</span></span> <span data-ttu-id="d998a-288">(뷰 파일 즉, 양식의 <em>\* \* ViewName</em><em>합니다. Mobile.cshtml</em>.) 설정 하려는 `RequireConsistentDisplayMode` 에 `true` 모바일 레이아웃이 비모바일 보기에서 잘 작동 하지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="d998a-288">(That is, the view file is of the form <em>\*\*ViewName</em><em>.Mobile.cshtml</em>.) You might want to set `RequireConsistentDisplayMode` to `true` if your mobile layout doesn't work well with your non-mobile views.</span></span> <span data-ttu-id="d998a-289">아래 스크린샷에서 하는 방법을 <em>발표자</em> 페이지를 렌더링 하는 경우 `RequireConsistentDisplayMode` 로 설정 된 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-289">The screenshot below shows how the <em>Speakers</em> page renders when `RequireConsistentDisplayMode` is set to `true`.</span></span>

<span data-ttu-id="d998a-290">[![p3_speakersConsistent](aspnet-mvc-4-mobile-features/_static/image33.png)](aspnet-mvc-4-mobile-features/_static/image32.png)</span><span class="sxs-lookup"><span data-stu-id="d998a-290">[![p3_speakersConsistent](aspnet-mvc-4-mobile-features/_static/image33.png)](aspnet-mvc-4-mobile-features/_static/image32.png)</span></span>

<span data-ttu-id="d998a-291">보기에서 일관 된 표시 모드가 설정 하 여 비활성화할 수 있습니다 `RequireConsistentDisplayMode` 에 `false` 뷰 파일에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-291">You can disable consistent display mode in a view by setting `RequireConsistentDisplayMode` to `false` in the view file.</span></span> <span data-ttu-id="d998a-292">다음 태그는 *Views\Home\AllSpeakers.cshtml* 파일 집합 `RequireConsistentDisplayMode` 하려면 `false`:</span><span class="sxs-lookup"><span data-stu-id="d998a-292">The following markup in the *Views\Home\AllSpeakers.cshtml* file sets `RequireConsistentDisplayMode` to `false`:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample18.cshtml)]

## <a name="creating-a-mobile-speakers-view"></a><span data-ttu-id="d998a-293">모바일 발표자 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="d998a-293">Creating a Mobile Speakers View</span></span>

<span data-ttu-id="d998a-294">방금 본 것 처럼 합니다 *발표자* 뷰도 가독성은 있지만 링크가 작은 되며 모바일 장치에서 누르기 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-294">As you just saw, the *Speakers* view is readable, but the links are small and are difficult to tap on a mobile device.</span></span> <span data-ttu-id="d998a-295">이 섹션에서는 모바일 전용을 만든 *발표자* 다음과 같은 최신 모바일 응용 프로그램 보기-큰 표시, 누르기 쉬운 링크 및 스피커를 신속 하 게 찾을 수 있는 검색 상자가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-295">In this section, you'll create a mobile-specific *Speakers* view that looks like a modern mobile application — it displays large, easy-to-tap links and contains a search box to quickly find speakers.</span></span>

<span data-ttu-id="d998a-296">복사본 *AllSpeakers.cshtml* 하 *AllSpeakers.Mobile.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-296">Copy *AllSpeakers.cshtml* to *AllSpeakers.Mobile.cshtml*.</span></span> <span data-ttu-id="d998a-297">엽니다는 *AllSpeakers.Mobile.cshtml* 파일을 제거는 `<h2>` 제목 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-297">Open the *AllSpeakers.Mobile.cshtml* file and remove the `<h2>` heading element.</span></span>

<span data-ttu-id="d998a-298">에 `<ul>` 태그를 추가 합니다 `data-role` 특성 및 해당 값을 설정 `listview`합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-298">In the `<ul>` tag, add the `data-role` attribute and set its value to `listview`.</span></span> <span data-ttu-id="d998a-299">와 같은 다른 [ `data-*` 특성](http://html5doctor.com/html5-custom-data-attributes/), `data-role="listview"` 큰 목록 항목을 쉽게 탭에 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-299">Like other [`data-*` attributes](http://html5doctor.com/html5-custom-data-attributes/), `data-role="listview"` makes the large list items easier to tap.</span></span> <span data-ttu-id="d998a-300">완료 된 태그의 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-300">This is what the completed markup looks like:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample19.cshtml)]

<span data-ttu-id="d998a-301">모바일 브라우저를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-301">Refresh the mobile browser.</span></span> <span data-ttu-id="d998a-302">업데이트 된 뷰는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-302">The updated view looks like this:</span></span>

<span data-ttu-id="d998a-303">[![p3_updatedSpeakerView1](aspnet-mvc-4-mobile-features/_static/image35.png)](aspnet-mvc-4-mobile-features/_static/image34.png)</span><span class="sxs-lookup"><span data-stu-id="d998a-303">[![p3_updatedSpeakerView1](aspnet-mvc-4-mobile-features/_static/image35.png)](aspnet-mvc-4-mobile-features/_static/image34.png)</span></span>

<span data-ttu-id="d998a-304">모바일 뷰를 향상 되어 있지만 긴 발표자 목록을 탐색 하기가 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-304">Although the mobile view has improved, it's difficult to navigate the long list of speakers.</span></span> <span data-ttu-id="d998a-305">이 문제를 해결 하는 `<ul>` 태그를 추가 합니다 `data-filter` 특성 및 설정 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-305">To fix this, in the `<ul>` tag, add the `data-filter` attribute and set it to `true`.</span></span> <span data-ttu-id="d998a-306">아래 코드는 `ul` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-306">The code below shows the `ul` markup.</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample20.html)]

<span data-ttu-id="d998a-307">다음 이미지는 결과로 생성 되는 페이지의 맨 위에 있는 검색 필터 상자를 표시 합니다 `data-filter` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-307">The following image shows the search filter box at the top of the page that results from the `data-filter` attribute.</span></span>

<span data-ttu-id="d998a-308">[![ps_Data_Filter](aspnet-mvc-4-mobile-features/_static/image37.png)](aspnet-mvc-4-mobile-features/_static/image36.png)</span><span class="sxs-lookup"><span data-stu-id="d998a-308">[![ps_Data_Filter](aspnet-mvc-4-mobile-features/_static/image37.png)](aspnet-mvc-4-mobile-features/_static/image36.png)</span></span>

<span data-ttu-id="d998a-309">검색 상자에 각 문자를 입력할 jQuery Mobile 아래 그림과에서 같이 표시 된 목록을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-309">As you type each letter in the search box, jQuery Mobile filters the displayed list as shown in the image below.</span></span>

<span data-ttu-id="d998a-310">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image39.png)](aspnet-mvc-4-mobile-features/_static/image38.png)</span><span class="sxs-lookup"><span data-stu-id="d998a-310">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image39.png)](aspnet-mvc-4-mobile-features/_static/image38.png)</span></span>

## <a name="improving-the-tags-list"></a><span data-ttu-id="d998a-311">태그 목록 개선</span><span class="sxs-lookup"><span data-stu-id="d998a-311">Improving the Tags List</span></span>

<span data-ttu-id="d998a-312">기본값이 마음 *스피커* 뷰를 *태그* 뷰도 가독성은 있지만 링크가 작고 모바일 장치에서 누르기 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-312">Like the default *Speakers* view, the *Tags* view is readable, but the links are small and difficult to tap on a mobile device.</span></span> <span data-ttu-id="d998a-313">수정이 섹션에서는 합니다 *태그* 수정한 동일한 방식으로 보기를 *발표자* 보기.</span><span class="sxs-lookup"><span data-stu-id="d998a-313">In this section, you'll fix the *Tags* view the same way you fixed the *Speakers* view.</span></span>

<span data-ttu-id="d998a-314">제거는 &quot;숨기기&quot; 접미사는 *Views\Home\AllTags.Mobile.cshtml.hide* 파일 이름 이므로 *Views\Home\AllTags.Mobile.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-314">Remove the &quot;hide&quot; suffix to the *Views\Home\AllTags.Mobile.cshtml.hide* file so the name is *Views\Home\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="d998a-315">이름이 바뀐된 파일을 열고 제거는 `<h2>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-315">Open the renamed file and remove the `<h2>` element.</span></span>

<span data-ttu-id="d998a-316">추가 된 `data-role` 하 고 `data-filter` 특성을 `<ul>` 태그를 다음과 같이:</span><span class="sxs-lookup"><span data-stu-id="d998a-316">Add the `data-role` and `data-filter` attributes to the `<ul>` tag, as shown here:</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample21.html)]

<span data-ttu-id="d998a-317">아래 이미지에서 문자 필터링 태그 페이지를 보여 줍니다. `J`합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-317">The image below shows the tags page filtering on the letter `J`.</span></span>

<span data-ttu-id="d998a-318">[![p3_tags_J](aspnet-mvc-4-mobile-features/_static/image41.png)](aspnet-mvc-4-mobile-features/_static/image40.png)</span><span class="sxs-lookup"><span data-stu-id="d998a-318">[![p3_tags_J](aspnet-mvc-4-mobile-features/_static/image41.png)](aspnet-mvc-4-mobile-features/_static/image40.png)</span></span>

## <a name="improving-the-dates-list"></a><span data-ttu-id="d998a-319">날짜 목록 개선</span><span class="sxs-lookup"><span data-stu-id="d998a-319">Improving the Dates List</span></span>

<span data-ttu-id="d998a-320">향상 시킬 수 있습니다는 *날짜* 향상 같은 보기를 *발표자* 및 *태그* 뷰를 쉽게 모바일 장치에서 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-320">You can improve the *Dates* view like you improved the *Speakers* and *Tags* views, so that it's easier to use on a mobile device.</span></span>

<span data-ttu-id="d998a-321">복사 합니다 *Views\Home\AllDates.cshtml* 파일을 *Views\Home\AllDates.Mobile.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-321">Copy the *Views\Home\AllDates.cshtml* file to *Views\Home\AllDates.Mobile.cshtml*.</span></span> <span data-ttu-id="d998a-322">새 파일을 열고 제거는 `<h2>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-322">Open the new file and remove the `<h2>` element.</span></span>

<span data-ttu-id="d998a-323">추가 `data-role="listview"` 에 `<ul>` 다음과 같은 태그:</span><span class="sxs-lookup"><span data-stu-id="d998a-323">Add `data-role="listview"` to the `<ul>` tag, like this:</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample22.html)]

<span data-ttu-id="d998a-324">아래 이미지 보여 줍니다 합니다 **날짜** 사용 하 여 페이지는 다음과 같은 `data-role` 진행에서 특성.</span><span class="sxs-lookup"><span data-stu-id="d998a-324">The image below shows what the **Date** page looks like with the `data-role` attribute in place.</span></span>

<span data-ttu-id="d998a-325">[![p3_dates1](aspnet-mvc-4-mobile-features/_static/image43.png)](aspnet-mvc-4-mobile-features/_static/image42.png) 의 내용을 대체 합니다 *Views\Home\AllDates.Mobile.cshtml* 를 다음 코드로 파일:</span><span class="sxs-lookup"><span data-stu-id="d998a-325">[![p3_dates1](aspnet-mvc-4-mobile-features/_static/image43.png)](aspnet-mvc-4-mobile-features/_static/image42.png) Replace the contents of the *Views\Home\AllDates.Mobile.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample23.cshtml)]

<span data-ttu-id="d998a-326">이 코드는 일까 지 모든 세션을 그룹화합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-326">This code groups all sessions by days.</span></span> <span data-ttu-id="d998a-327">각 날마다 목록 구분선을 생성 및 구분선 아래에서 각 날짜에 대 한 모든 세션을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-327">It creates a list divider for each new day, and it lists all the sessions for each day under a divider.</span></span> <span data-ttu-id="d998a-328">모양이 코드를 실행할 때 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-328">Here's what it looks like when this code runs:</span></span>

<span data-ttu-id="d998a-329">[![p3_dates2](aspnet-mvc-4-mobile-features/_static/image45.png)](aspnet-mvc-4-mobile-features/_static/image44.png)</span><span class="sxs-lookup"><span data-stu-id="d998a-329">[![p3_dates2](aspnet-mvc-4-mobile-features/_static/image45.png)](aspnet-mvc-4-mobile-features/_static/image44.png)</span></span>

## <a name="improving-the-sessionstable-view"></a><span data-ttu-id="d998a-330">SessionsTable 뷰 개선</span><span class="sxs-lookup"><span data-stu-id="d998a-330">Improving the SessionsTable View</span></span>

<span data-ttu-id="d998a-331">이 섹션에서는 세션의 모바일 전용 뷰를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-331">In this section, you'll create a mobile-specific view of sessions.</span></span> <span data-ttu-id="d998a-332">우리가 변경 내용을 만들었습니다 다른 보기에서는 보다 더 광범위 한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-332">The changes we make will be more extensive than in other views we have created.</span></span>

<span data-ttu-id="d998a-333">모바일 브라우저에서 탭의 **스피커** 단추를 선택한 다음 입력 `Sc` 검색 상자에 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-333">In the mobile browser, tap the **Speaker** button, then enter `Sc` in the search box.</span></span>

<span data-ttu-id="d998a-334">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image47.png)](aspnet-mvc-4-mobile-features/_static/image46.png)</span><span class="sxs-lookup"><span data-stu-id="d998a-334">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image47.png)](aspnet-mvc-4-mobile-features/_static/image46.png)</span></span>

<span data-ttu-id="d998a-335">탭의 **Scott hanselman이** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-335">Tap the **Scott Hanselman** link.</span></span>

<span data-ttu-id="d998a-336">[![p3_scottHa](aspnet-mvc-4-mobile-features/_static/image49.png)](aspnet-mvc-4-mobile-features/_static/image48.png)</span><span class="sxs-lookup"><span data-stu-id="d998a-336">[![p3_scottHa](aspnet-mvc-4-mobile-features/_static/image49.png)](aspnet-mvc-4-mobile-features/_static/image48.png)</span></span>

<span data-ttu-id="d998a-337">알 수 있듯이 표시를 모바일 브라우저에서는 읽기가 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-337">As you can see, the display is difficult to read on a mobile browser.</span></span> <span data-ttu-id="d998a-338">날짜 열이 읽기 어려운 및 태그 열 뷰를 벗어났습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-338">The date column is hard to read and the tags column is out of the view.</span></span> <span data-ttu-id="d998a-339">이 문제를 해결 하려면 복사 *Views\Home\SessionsTable.cshtml* 하 *Views\Home\SessionsTable.Mobile.cshtml*, 파일의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-339">To fix this, copy *Views\Home\SessionsTable.cshtml* to *Views\Home\SessionsTable.Mobile.cshtml*, and then replace the contents of the file with the following code:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample24.cshtml)]

<span data-ttu-id="d998a-340">코드 열 태그 및이 모든 정보를 모바일 브라우저에서 읽을 수 있도록 제목, 강연자 및 날짜를 세로로 형식 대화방을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-340">The code removes the room and tags columns, and formats the title, speaker, and date vertically, so that all this information is readable on a mobile browser.</span></span> <span data-ttu-id="d998a-341">아래 이미지에 코드 변경 내용을 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-341">The image below reflects the code changes.</span></span>

<span data-ttu-id="d998a-342">[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image51.png)](aspnet-mvc-4-mobile-features/_static/image50.png)</span><span class="sxs-lookup"><span data-stu-id="d998a-342">[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image51.png)](aspnet-mvc-4-mobile-features/_static/image50.png)</span></span>

## <a name="improving-the-sessionbycode-view"></a><span data-ttu-id="d998a-343">SessionByCode 뷰 개선</span><span class="sxs-lookup"><span data-stu-id="d998a-343">Improving the SessionByCode View</span></span>

<span data-ttu-id="d998a-344">모바일 전용 뷰를 마지막으로 만들어야 합니다 *SessionByCode* 보기.</span><span class="sxs-lookup"><span data-stu-id="d998a-344">Finally, you'll create a mobile-specific view of the *SessionByCode* view.</span></span> <span data-ttu-id="d998a-345">모바일 브라우저에서 탭의 **스피커** 단추를 선택한 다음 입력 `Sc` 검색 상자에 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-345">In the mobile browser, tap the **Speaker** button, then enter `Sc` in the search box.</span></span>

<span data-ttu-id="d998a-346">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image53.png)](aspnet-mvc-4-mobile-features/_static/image52.png)</span><span class="sxs-lookup"><span data-stu-id="d998a-346">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image53.png)](aspnet-mvc-4-mobile-features/_static/image52.png)</span></span>

<span data-ttu-id="d998a-347">탭의 **Scott hanselman이** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-347">Tap the **Scott Hanselman** link.</span></span> <span data-ttu-id="d998a-348">Scott Hanselman의 세션이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-348">Scott Hanselman's sessions are displayed.</span></span>

<span data-ttu-id="d998a-349">[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image55.png)](aspnet-mvc-4-mobile-features/_static/image54.png)</span><span class="sxs-lookup"><span data-stu-id="d998a-349">[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image55.png)](aspnet-mvc-4-mobile-features/_static/image54.png)</span></span>

<span data-ttu-id="d998a-350">선택 된 **MS 웹 Love 스택의 개요** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-350">Choose the **An Overview of the MS Web Stack of Love** link.</span></span>

<span data-ttu-id="d998a-351">[![ps_love](aspnet-mvc-4-mobile-features/_static/image57.png)](aspnet-mvc-4-mobile-features/_static/image56.png)</span><span class="sxs-lookup"><span data-stu-id="d998a-351">[![ps_love](aspnet-mvc-4-mobile-features/_static/image57.png)](aspnet-mvc-4-mobile-features/_static/image56.png)</span></span>

<span data-ttu-id="d998a-352">기본 바탕 화면 보기 정상 이지만 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-352">The default desktop view is fine, but you can improve it.</span></span>

<span data-ttu-id="d998a-353">복사 합니다 *Views\Home\SessionByCode.cshtml* 에 *Views\Home\SessionByCode.Mobile.cshtml* 의 내용을 바꾸고는 *Views\Home\SessionByCode.Mobile.cshtml*파일에 다음 태그를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="d998a-353">Copy the *Views\Home\SessionByCode.cshtml* to *Views\Home\SessionByCode.Mobile.cshtml* and replace the contents of the *Views\Home\SessionByCode.Mobile.cshtml* file with the following markup:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample25.cshtml)]

<span data-ttu-id="d998a-354">새 태그를 사용 하는 `data-role` 특성 뷰의 레이아웃을 개선 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-354">The new markup uses the `data-role` attribute to improve the layout of the view.</span></span>

<span data-ttu-id="d998a-355">모바일 브라우저를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-355">Refresh the mobile browser.</span></span> <span data-ttu-id="d998a-356">다음 이미지는 방금 만든 코드 변경 내용을 반영 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-356">The following image reflects the code changes that you just made:</span></span>

<span data-ttu-id="d998a-357">[![p3_love2](aspnet-mvc-4-mobile-features/_static/image59.png)](aspnet-mvc-4-mobile-features/_static/image58.png)</span><span class="sxs-lookup"><span data-stu-id="d998a-357">[![p3_love2](aspnet-mvc-4-mobile-features/_static/image59.png)](aspnet-mvc-4-mobile-features/_static/image58.png)</span></span>

## <a name="wrapup-and-review"></a><span data-ttu-id="d998a-358">Wrapup 및 검토</span><span class="sxs-lookup"><span data-stu-id="d998a-358">Wrapup and Review</span></span>

<span data-ttu-id="d998a-359">이 자습서는 ASP.NET MVC 4 Developer Preview의 새로운 모바일 기능을 도입 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-359">This tutorial has introduced the new mobile features of ASP.NET MVC 4 Developer Preview.</span></span> <span data-ttu-id="d998a-360">모바일 기능에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-360">The mobile features include:</span></span>

- <span data-ttu-id="d998a-361">전역적으로 그리고 개별 뷰에 대해 레이아웃, 뷰 및 부분 뷰를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-361">The ability to override layout, views, and partial views, both globally and for an individual view.</span></span>
- <span data-ttu-id="d998a-362">레이아웃 및 부분 재정의 하 여에 대 한 제어를 `RequireConsistentDisplayMode` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-362">Control over layout and partial override enforcement using the `RequireConsistentDisplayMode` property.</span></span>
- <span data-ttu-id="d998a-363">모바일 뷰 전환기 위젯 데스크톱 보기에 표시할 수 있는 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-363">A view-switcher widget for mobile views than can also be displayed in desktop views.</span></span>
- <span data-ttu-id="d998a-364">IPhone 브라우저 등 특정 브라우저를 지원 하기 위한 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-364">Support for supporting specific browsers, such as the iPhone browser.</span></span>

## <a name="see-also"></a><span data-ttu-id="d998a-365">참고 항목</span><span class="sxs-lookup"><span data-stu-id="d998a-365">See Also</span></span>

- <span data-ttu-id="d998a-366">[jQuery Mobile](http://jquerymobile.com) 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="d998a-366">[jQuery Mobile](http://jquerymobile.com) site.</span></span>
- [<span data-ttu-id="d998a-367">jQuery Mobile 개요</span><span class="sxs-lookup"><span data-stu-id="d998a-367">jQuery Mobile Overview</span></span>](http://jquerymobile.com/demos/1.0b3/docs/about/intro.html)
- [<span data-ttu-id="d998a-368">W3C 권장 사항 모바일 웹 응용 프로그램 모범 사례</span><span class="sxs-lookup"><span data-stu-id="d998a-368">W3C Recommendation Mobile Web Application Best Practices</span></span>](http://www.w3.org/TR/mwabp/)
- [<span data-ttu-id="d998a-369">미디어 쿼리에 대 한 W3C 후보 권장 사항</span><span class="sxs-lookup"><span data-stu-id="d998a-369">W3C Candidate Recommendation for media queries</span></span>](http://www.w3.org/TR/css3-mediaqueries/)
