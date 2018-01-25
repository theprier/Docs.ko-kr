---
uid: mvc/overview/older-versions/aspnet-mvc-4-mobile-features
title: "ASP.NET MVC 4 모바일 기능 | Microsoft Docs"
author: Rick-Anderson
description: "이 자습서에서는 ASP.NET MVC 5 모바일 웹 응용 프로그램에서 Azure 웹 사이트 배포에서 샘플 코드는 MVC 5 버전이 되었습니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/15/2012
ms.topic: article
ms.assetid: 27dc4fc8-1b51-43b0-933f-fc1b52476523
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/aspnet-mvc-4-mobile-features
msc.type: authoredcontent
ms.openlocfilehash: d47d8f61dc7af6e1dc5887338be862ea81d7bb17
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="aspnet-mvc-4-mobile-features"></a><span data-ttu-id="3bb0f-103">ASP.NET MVC 4 모바일 기능</span><span class="sxs-lookup"><span data-stu-id="3bb0f-103">ASP.NET MVC 4 Mobile Features</span></span>
====================
<span data-ttu-id="3bb0f-104">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="3bb0f-105">이제이 자습서에서 샘플 코드의 MVC 5 버전 [ASP.NET MVC 5 모바일 웹 응용 프로그램 배포 Azure 웹 사이트에](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/)합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-105">There is now an MVC 5 version of this tutorial with code samples at [Deploy an ASP.NET MVC 5 Mobile Web Application on Azure Web Sites](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/).</span></span>


<span data-ttu-id="3bb0f-106">이 자습서에서는 모바일 ASP.NET MVC 4 웹 응용 프로그램 기능을 사용 하는 방법의 기본 사항 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-106">This tutorial will teach you the basics of how to work with mobile features in an ASP.NET MVC 4 Web application.</span></span> <span data-ttu-id="3bb0f-107">이 자습서에서는 사용할 수 있습니다 [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) 또는 Visual Web Developer 2010 Express 서비스 팩 1 (&quot;Visual Web Developer 또는 VWD&quot;).</span><span class="sxs-lookup"><span data-stu-id="3bb0f-107">For this tutorial, you can use [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) or Visual Web Developer 2010 Express Service Pack 1 (&quot;Visual Web Developer or VWD&quot;).</span></span> <span data-ttu-id="3bb0f-108">이미 있는 경우 Visual studio professional 버전을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-108">You can use the professional version of Visual Studio if you already have that.</span></span>

<span data-ttu-id="3bb0f-109">시작 하기 전에 아래에 나열 된 필수 구성 요소가 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-109">Before you start, make sure you've installed the prerequisites listed below.</span></span>

- <span data-ttu-id="3bb0f-110">[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) (권장) 또는 Visual Studio Web Developer Express SP1.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-110">[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) (recommended) or Visual Studio Web Developer Express SP1.</span></span> <span data-ttu-id="3bb0f-111">Visual Studio 2012에 ASP.NET MVC 4 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-111">Visual Studio 2012 contains ASP.NET MVC 4.</span></span> <span data-ttu-id="3bb0f-112">Visual Web Developer 2010를 사용 하는 경우 설치 해야 [ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392)합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-112">If you are using Visual Web Developer 2010, you must install [ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392).</span></span>

<span data-ttu-id="3bb0f-113">모바일 브라우저 에뮬레이터에서 앱을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-113">You will also need a mobile browser emulator.</span></span> <span data-ttu-id="3bb0f-114">다음 중 하나를 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-114">Any of the following will work:</span></span>

- <span data-ttu-id="3bb0f-115">[Windows 7 Phone 에뮬레이터](https://msdn.microsoft.com/library/ff402563(VS.92).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-115">[Windows 7 Phone Emulator](https://msdn.microsoft.com/library/ff402563(VS.92).aspx).</span></span> <span data-ttu-id="3bb0f-116">(이 자습서에서는 대부분의 스크린 샷에 사용 되는 에뮬레이터입니다.)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-116">(This is the emulator that's used in most of the screen shots in this tutorial.)</span></span>
- <span data-ttu-id="3bb0f-117">IPhone을 에뮬레이션 하기 위해 사용자 에이전트 문자열을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-117">Change the user agent string to emulate an iPhone.</span></span> <span data-ttu-id="3bb0f-118">참조 [이](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) 블로그 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-118">See [this](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) blog entry.</span></span>
- [<span data-ttu-id="3bb0f-119">Opera Mobile Emulator</span><span class="sxs-lookup"><span data-stu-id="3bb0f-119">Opera Mobile Emulator</span></span>](http://www.opera.com/developer/tools/mobile/)
- <span data-ttu-id="3bb0f-120">[Apple Safari](http://www.apple.com/safari/download/) iPhone로 설정 하 고 사용자 에이전트와 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-120">[Apple Safari](http://www.apple.com/safari/download/) with the user agent set to iPhone.</span></span> <span data-ttu-id="3bb0f-121">Safari에서 "iPhone"로 사용자 에이전트를 설정 하는 방법에 지침은 [Safari 있다고 생각 IE 되 게 하는 방법](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) David Alison 블로그.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-121">For instructions on how to set the user agent in Safari to "iPhone", see [How to let Safari pretend it's IE](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) on David Alison's blog.</span></span>

<span data-ttu-id="3bb0f-122">C# 소스 코드를 visual Studio 프로젝트는이 항목을 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-122">Visual Studio projects with C# source code are available to accompany this topic:</span></span>

- [<span data-ttu-id="3bb0f-123">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="3bb0f-123">Starter project download</span></span>](https://go.microsoft.com/fwlink/?linkid=228307&amp;clcid=0x409)
- [<span data-ttu-id="3bb0f-124">프로젝트 다운로드를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-124">Completed project download</span></span>](https://go.microsoft.com/fwlink/?linkid=228306&amp;clcid=0x409)

### <a name="what-youll-build"></a><span data-ttu-id="3bb0f-125">만들 것인지</span><span class="sxs-lookup"><span data-stu-id="3bb0f-125">What You'll Build</span></span>

<span data-ttu-id="3bb0f-126">이 자습서에서는 모바일 기능에 추가할 간단한 회의 목록 응용 프로그램에 제공 되는 [시작 프로젝트](https://go.microsoft.com/fwlink/?LinkId=228307)합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-126">For this tutorial, you'll add mobile features to the simple conference-listing application that's provided in the [starter project](https://go.microsoft.com/fwlink/?LinkId=228307).</span></span> <span data-ttu-id="3bb0f-127">다음 스크린 샷에서 같이 완성된 된 응용 프로그램 태그 페이지가 나와 [Windows 7 Phone Emulator](https://msdn.microsoft.com/library/ff402563(VS.92).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-127">The following screenshot shows the tags page of the completed application as seen in the [Windows 7 Phone Emulator](https://msdn.microsoft.com/library/ff402563(VS.92).aspx).</span></span> <span data-ttu-id="3bb0f-128">참조 [키보드 매핑에 대 한 Windows Phone 에뮬레이터](https://msdn.microsoft.com/library/ff754352(v=vs.92).aspx) 키보드 입력을 간소화 하기 위해 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-128">See [Keyboard Mapping for Windows Phone Emulator](https://msdn.microsoft.com/library/ff754352(v=vs.92).aspx) to simplify keyboard input.</span></span>

<span data-ttu-id="3bb0f-129">[![p1_Tags_CompletedProj](aspnet-mvc-4-mobile-features/_static/image2.png)](aspnet-mvc-4-mobile-features/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-129">[![p1_Tags_CompletedProj](aspnet-mvc-4-mobile-features/_static/image2.png)](aspnet-mvc-4-mobile-features/_static/image1.png)</span></span>

<span data-ttu-id="3bb0f-130">Internet Explorer 버전 9, 10, FireFox 또는 Chrome을 설정 하 여 모바일 응용 프로그램을 개발 하는 데는 [사용자 에이전트 문자열](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-130">You can use Internet Explorer version 9 or 10, FireFox or Chrome to develop your mobile application by setting the [user agent string](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/).</span></span> <span data-ttu-id="3bb0f-131">다음 그림에서는 iPhone을 에뮬레이션 하는 Internet Explorer를 사용 하 여 완성 된 자습서를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-131">The following image shows the completed tutorial using Internet Explorer emulating an iPhone.</span></span> <span data-ttu-id="3bb0f-132">Internet Explorer F-12 개발자 도구를 사용할 수 있습니다 및 [Fiddler 도구](http://www.fiddler2.com/fiddler2/) 응용 프로그램을 디버깅할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-132">You can use the Internet Explorer F-12 developer tools and the [Fiddler tool](http://www.fiddler2.com/fiddler2/) to help debug your application.</span></span>

![](aspnet-mvc-4-mobile-features/_static/image3.png)

### <a name="skills-youll-learn"></a><span data-ttu-id="3bb0f-133">기술을 알아봅니다</span><span class="sxs-lookup"><span data-stu-id="3bb0f-133">Skills You'll Learn</span></span>

<span data-ttu-id="3bb0f-134">학습할 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-134">Here's what you'll learn:</span></span>

- <span data-ttu-id="3bb0f-135">ASP.NET MVC 4 템플릿에 HTML5를 사용 하는 방법 `viewport` 모바일 장치에 특성 및 개선 하기 위해 자동 선택 렌더링을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-135">How the ASP.NET MVC 4 templates use the HTML5 `viewport` attribute and adaptive rendering to improve display on mobile devices.</span></span>
- <span data-ttu-id="3bb0f-136">모바일 전용 뷰를 만드는 방법.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-136">How to create mobile-specific views.</span></span>
- <span data-ttu-id="3bb0f-137">만들기 뷰 전환기 모바일 보기와 응용 프로그램의 바탕 화면 보기 간에 사용 하면 사용자가 토글 해당 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-137">How to create a view switcher that lets users toggle between a mobile view and a desktop view of the application.</span></span>

### <a name="getting-started"></a><span data-ttu-id="3bb0f-138">시작</span><span class="sxs-lookup"><span data-stu-id="3bb0f-138">Getting Started</span></span>

<span data-ttu-id="3bb0f-139">다음 링크를 사용 하 여 시작 프로젝트에 대 한 목록 회의 응용 프로그램을 다운로드: [다운로드](https://go.microsoft.com/fwlink/?LinkId=228307)합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-139">Download the conference-listing application for the starter project using the following link: [Download](https://go.microsoft.com/fwlink/?LinkId=228307).</span></span> <span data-ttu-id="3bb0f-140">다음 Windows 탐색기에서 마우스 오른쪽 단추로 클릭는 *MvcMobile.zip* 파일을 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-140">Then in Windows Explorer, right-click the *MvcMobile.zip* file and choose **Properties**.</span></span> <span data-ttu-id="3bb0f-141">에 **MvcMobile.zip 속성** 대화 상자에서 선택 하는 **차단 해제** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-141">In the **MvcMobile.zip Properties** dialog box, choose the **Unblock** button.</span></span> <span data-ttu-id="3bb0f-142">(사용 하려고 할 때 발생 하는 보안 경고가 표시 되지 않도록 차단 해제는 *.zip* 웹에서 다운로드 한 파일입니다.)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-142">(Unblocking prevents a security warning that occurs when you try to use a *.zip* file that you've downloaded from the web.)</span></span>

![p1_unBlock](aspnet-mvc-4-mobile-features/_static/image4.png)

<span data-ttu-id="3bb0f-144">마우스 오른쪽 단추로 클릭는 *MvcMobile.zip* 파일을 선택 **압축 풀기** 에 파일 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-144">Right-click the *MvcMobile.zip* file and select **Extract All** to unzip the file.</span></span> <span data-ttu-id="3bb0f-145">Visual Studio에서 열고는 *MvcMobile.sln* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-145">In Visual Studio, open the *MvcMobile.sln* file.</span></span>

<span data-ttu-id="3bb0f-146">데스크톱 브라우저에 표시 하는 응용 프로그램을 실행 하려면 CTRL + f 5를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-146">Press CTRL+F5 to run the application, which will display it in your desktop browser.</span></span> <span data-ttu-id="3bb0f-147">모바일 브라우저 에뮬레이터 시작 회의 응용 프로그램에 대 한 URL의 에뮬레이터에 복사한 다음 클릭는 **태그에 의해 찾아보기** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-147">Start your mobile browser emulator, copy the URL for the conference application into the emulator, and then click the **Browse by tag** link.</span></span> <span data-ttu-id="3bb0f-148">Windows Phone 에뮬레이터를 사용 하는 경우 URL 표시줄에서 클릭를 키보드 액세스를 일시 중지 키를 누르십시오.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-148">If you are using the Windows Phone Emulator, click in the URL bar and press the Pause key to get keyboard access.</span></span> <span data-ttu-id="3bb0f-149">다음 이미지는 *AllTags* 보기 (선택 **태그에 의해 찾아보기**).</span><span class="sxs-lookup"><span data-stu-id="3bb0f-149">The image below shows the *AllTags* view (from choosing **Browse by tag**).</span></span>

<span data-ttu-id="3bb0f-150">[![p1_browseTag](aspnet-mvc-4-mobile-features/_static/image6.png)](aspnet-mvc-4-mobile-features/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-150">[![p1_browseTag](aspnet-mvc-4-mobile-features/_static/image6.png)](aspnet-mvc-4-mobile-features/_static/image5.png)</span></span>

<span data-ttu-id="3bb0f-151">디스플레이가 모바일 장치에서 읽을 수 있는 매우입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-151">The display is very readable on a mobile device.</span></span> <span data-ttu-id="3bb0f-152">ASP.NET 링크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-152">Choose the ASP.NET link.</span></span>

<span data-ttu-id="3bb0f-153">[![p1_tagged_ASPNET](aspnet-mvc-4-mobile-features/_static/image8.png)](aspnet-mvc-4-mobile-features/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-153">[![p1_tagged_ASPNET](aspnet-mvc-4-mobile-features/_static/image8.png)](aspnet-mvc-4-mobile-features/_static/image7.png)</span></span>

<span data-ttu-id="3bb0f-154">ASP.NET 태그 보기는 매우 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-154">The ASP.NET tag view is very cluttered.</span></span> <span data-ttu-id="3bb0f-155">예를 들어는 **날짜** 열 읽기 하기 매우 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-155">For example, the **Date** column is very difficult to read.</span></span> <span data-ttu-id="3bb0f-156">이 자습서의 뒷부분에 나오는 버전을 만듭니다는 *AllTags* 모바일 브라우저에 맞게 이며 하 게 되는 디스플레이 읽을 수 있는 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-156">Later in the tutorial you'll create a version of the *AllTags* view that's specifically for mobile browsers and that will make the display readable.</span></span>

<span data-ttu-id="3bb0f-157">참고: 현재는 버그가 있습니다 모바일 캐싱 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-157">Note: Currently a bug exists in the mobile caching engine.</span></span> <span data-ttu-id="3bb0f-158">프로덕션 응용 프로그램을 설치 해야는 [고정 DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) 덩어리 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-158">For production applications, you must install the [Fixed DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) nugget package.</span></span> <span data-ttu-id="3bb0f-159">참조 [ASP.NET MVC 4 모바일 캐싱 버그 고정](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) 수정 프로그램에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-159">See [ASP.NET MVC 4 Mobile Caching Bug Fixed](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) for details on the fix.</span></span>

## <a name="css-media-queries"></a><span data-ttu-id="3bb0f-160">CSS 미디어 쿼리</span><span class="sxs-lookup"><span data-stu-id="3bb0f-160">CSS Media Queries</span></span>

<span data-ttu-id="3bb0f-161">[CSS 미디어 쿼리](http://www.w3.org/TR/css3-mediaqueries/) 미디어 형식에 대 한 CSS에 대 한 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-161">[CSS media queries](http://www.w3.org/TR/css3-mediaqueries/) are an extension to CSS for media types.</span></span> <span data-ttu-id="3bb0f-162">특정 브라우저 (사용자 에이전트)에 대 한 기본 CSS 규칙을 재정의 하는 규칙을 만들 수 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-162">They allow you to create rules that override the default CSS rules for specific browsers (user agents).</span></span> <span data-ttu-id="3bb0f-163">모바일 브라우저를 대상으로 하는 CSS에 대 한 일반적인 규칙은 최대 화면 크기를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-163">A common rule for CSS that targets mobile browsers is defining the maximum screen size.</span></span> <span data-ttu-id="3bb0f-164">*Content\Site.css* 다음 미디어 쿼리를 포함 하는 새 ASP.NET MVC 4 인터넷 프로젝트를 만들 때 만들어지는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-164">The *Content\Site.css* file that's created when you create a new ASP.NET MVC 4 Internet project contains the following media query:</span></span>

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample1.css)]

<span data-ttu-id="3bb0f-165">브라우저 창을 850 픽셀 줄이거나 경우이 미디어 블록 CSS 규칙을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-165">If the browser window is 850 pixels wide or less, it will use the CSS rules inside this media block.</span></span> <span data-ttu-id="3bb0f-166">에 제공 하기 위해 HTML 콘텐츠의 표시를 더 나은 설계 된 기본 CSS 규칙 보다 작은 브라우저 (예: 모바일 브라우저) 데스크톱 브라우저의 넓은 디스플레이 대 한 다음과 같은 CSS 미디어 쿼리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-166">You can use CSS media queries like this to provide a better display of HTML content on small browsers (like mobile browsers) than the default CSS rules that are designed for the wider displays of desktop browsers.</span></span>

## <a name="the-viewport-meta-tag"></a><span data-ttu-id="3bb0f-167">뷰포트 메타 태그</span><span class="sxs-lookup"><span data-stu-id="3bb0f-167">The Viewport Meta Tag</span></span>

<span data-ttu-id="3bb0f-168">가상 브라우저 창의 너비를 정의 하는 대부분의 모바일 브라우저 (의 *뷰포트*) 하는 모바일 장치에서의 실제 너비 보다 훨씬 큰 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-168">Most mobile browsers define a virtual browser window width (the *viewport*) that's much larger than the actual width of the mobile device.</span></span> <span data-ttu-id="3bb0f-169">따라서 가상 디스플레이로 내 전체 웹 페이지에 맞게 모바일 브라우저 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-169">This allows mobile browsers to fit the entire web page inside the virtual display.</span></span> <span data-ttu-id="3bb0f-170">사용자가 다음 확대할 수 흥미로운 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-170">Users can then zoom in on interesting content.</span></span> <span data-ttu-id="3bb0f-171">그러나 실제 장치 너비로 뷰포트 너비를 설정 하는 경우 없습니다 확대/축소는 필요한 경우 모바일 브라우저에는 콘텐츠를 맞추는 때문에.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-171">However, if you set the viewport width to the actual device width, no zooming is required, because the content fits in the mobile browser.</span></span>

<span data-ttu-id="3bb0f-172">뷰포트 `<meta>` ASP.NET MVC 4 레이아웃 파일의 태그에에서 장치 너비에 뷰포트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-172">The viewport `<meta>` tag in the ASP.NET MVC 4 layout file sets the viewport to the device width.</span></span> <span data-ttu-id="3bb0f-173">다음 줄 뷰포트를 보여 줍니다. `<meta>` ASP.NET MVC 4 레이아웃 파일의 태그에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-173">The following line shows the viewport `<meta>` tag in the ASP.NET MVC 4 layout file.</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample2.html)]

## <a name="examining-the-effect-of-css-media-queries-and-the-viewport-meta-tag"></a><span data-ttu-id="3bb0f-174">CSS 미디어 쿼리 및 뷰포트 메타 태그의 효과 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-174">Examining the Effect of CSS Media Queries and the Viewport Meta Tag</span></span>

<span data-ttu-id="3bb0f-175">열기는 *Views\Shared\\_Layout.cshtml* 뷰포트 주석 고 편집기에서 파일 `<meta>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-175">Open the *Views\Shared\\_Layout.cshtml* file in the editor and comment out the viewport `<meta>` tag.</span></span> <span data-ttu-id="3bb0f-176">다음 태그 주석 줄을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-176">The following markup shows the commented-out line.</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample3.cshtml)]

<span data-ttu-id="3bb0f-177">열기는 *MvcMobile\Content\Site.css* 편집기에서 파일을 미디어 쿼리의 최대 너비를 0 픽셀로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-177">Open the *MvcMobile\Content\Site.css* file in the editor and change the maximum width in the media query to zero pixels.</span></span> <span data-ttu-id="3bb0f-178">이렇게 하면 모바일 브라우저에서 사용 되는 CSS 규칙이 방지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-178">This will prevent the CSS rules from being used in mobile browsers.</span></span> <span data-ttu-id="3bb0f-179">다음 줄에서는 수정 된 미디어 쿼리를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-179">The following line shows the modified media query:</span></span>

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample4.css)]

<span data-ttu-id="3bb0f-180">변경 내용을 저장 하 고 모바일 브라우저 에뮬레이터에서 회의 응용 프로그램을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-180">Save your changes and browse to the Conference application in a mobile browser emulator.</span></span> <span data-ttu-id="3bb0f-181">다음 그림에는 작은 텍스트 뷰포트를 제거할 경우의 결과 `<meta>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-181">The tiny text in the following image is the result of removing the viewport `<meta>` tag.</span></span> <span data-ttu-id="3bb0f-182">없는 뷰포트와 `<meta>` 태그 브라우저 축소 되어 표시 기본 뷰포트 너비에 (850 픽셀 대부분의 모바일 브라우저에 대 한 광범위 한 또는.)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-182">With no viewport `<meta>` tag, the browser is zooming out to the default viewport width (850 pixels or wider for most mobile browsers.)</span></span>

<span data-ttu-id="3bb0f-183">[![p1_noViewPort](aspnet-mvc-4-mobile-features/_static/image10.png)](aspnet-mvc-4-mobile-features/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-183">[![p1_noViewPort](aspnet-mvc-4-mobile-features/_static/image10.png)](aspnet-mvc-4-mobile-features/_static/image9.png)</span></span>

<span data-ttu-id="3bb0f-184">변경 내용을 실행 취소-뷰포트를 주석 처리 제거 `<meta>` 레이아웃 파일에 태그 및 850 픽셀에 미디어 쿼리 복원는 *Site.css* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-184">Undo your changes — uncomment the viewport `<meta>` tag in the layout file and restore the media query to 850 pixels in the *Site.css* file.</span></span> <span data-ttu-id="3bb0f-185">변경 내용을 저장 모바일에서 잘 작동 디스플레이 복원 되었는지 확인 하려면 모바일 브라우저를 새로 고 치세요.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-185">Save your changes and refresh the mobile browser to verify that the mobile-friendly display has been restored.</span></span>

<span data-ttu-id="3bb0f-186">뷰포트 `<meta>` 태그와 CSS 미디어 쿼리 ASP.NET MVC 4 관련 되어 있으며 웹 응용 프로그램에서 이러한 기능을 활용을 취할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-186">The viewport `<meta>` tag and the CSS media query are not specific to ASP.NET MVC 4, and you can take advantage of these features in any web application.</span></span> <span data-ttu-id="3bb0f-187">하지만 이제 새 ASP.NET MVC 4 프로젝트를 만들 때 생성 되는 파일에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-187">But they are now built into the files that are generated when you create a new ASP.NET MVC 4 project.</span></span>

<span data-ttu-id="3bb0f-188">뷰포트에 대 한 자세한 내용은 `<meta>` 태그, 참조 [두 개의 뷰포트 이야기-2 부](http://www.quirksmode.org/mobile/viewports2.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-188">For more information about the viewport `<meta>` tag, see [A tale of two viewports — part two](http://www.quirksmode.org/mobile/viewports2.html).</span></span>

<span data-ttu-id="3bb0f-189">다음 섹션에서 모바일 브라우저 특정 보기를 제공 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-189">In the next section you'll see how to provide mobile-browser specific views.</span></span>

## <a name="overriding-views-layouts-and-partial-views"></a><span data-ttu-id="3bb0f-190">뷰, 레이아웃 및 부분 뷰를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-190">Overriding Views, Layouts, and Partial Views</span></span>

<span data-ttu-id="3bb0f-191">ASP.NET MVC 4의 중요 한 새로운 기능은 개별 모바일 브라우저에 대 한 일반적으로 또는 모든 특정 브라우저에 대 한 모바일 브라우저에 대 한 모든 보기 (레이아웃 및 부분 뷰 포함)를 재정의할 수 있습니다 하는 간단한 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-191">A significant new feature in ASP.NET MVC 4 is a simple mechanism that lets you override any view (including layouts and partial views) for mobile browsers in general, for an individual mobile browser, or for any specific browser.</span></span> <span data-ttu-id="3bb0f-192">모바일 전용 보기를 제공 하려면 보기 파일 복사 추가 하는 *합니다. 모바일* 을 파일 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-192">To provide a mobile-specific view, you can copy a view file and add *.Mobile* to the file name.</span></span> <span data-ttu-id="3bb0f-193">예를 들어, 모바일 만들려는 *인덱스* 보기, 복사 *Views\Home\Index.cshtml* 를 *Views\Home\Index.Mobile.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-193">For example, to create a mobile *Index* view, copy *Views\Home\Index.cshtml* to *Views\Home\Index.Mobile.cshtml*.</span></span>

<span data-ttu-id="3bb0f-194">이 섹션에서는 모바일 전용 레이아웃 파일을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-194">In this section, you'll create a mobile-specific layout file.</span></span>

<span data-ttu-id="3bb0f-195">복사를 시작 하려면 *Views\Shared\\_Layout.cshtml* 를 *Views\Shared\\_Layout.Mobile.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-195">To start, copy *Views\Shared\\_Layout.cshtml* to *Views\Shared\\_Layout.Mobile.cshtml*.</span></span> <span data-ttu-id="3bb0f-196">열기  *\_Layout.Mobile.cshtml* 에서 제목을 변경 하 고 **MVC4 회의** 를 **회의 (모바일)**합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-196">Open *\_Layout.Mobile.cshtml* and change the title from **MVC4 Conference** to **Conference (Mobile)**.</span></span>

<span data-ttu-id="3bb0f-197">각 `Html.ActionLink` 호출, "찾아보기 기준" 각 링크에 제거 *ActionLink*합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-197">In each `Html.ActionLink` call, remove "Browse by" in each link *ActionLink*.</span></span> <span data-ttu-id="3bb0f-198">다음 코드는 모바일 레이아웃 파일의 완료 된 본문 섹션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-198">The following code shows the completed body section of the mobile layout file.</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample5.cshtml)]

<span data-ttu-id="3bb0f-199">복사는 *Views\Home\AllTags.cshtml* 파일을 *Views\Home\AllTags.Mobile.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-199">Copy the *Views\Home\AllTags.cshtml* file to *Views\Home\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="3bb0f-200">새 파일을 열고 변경는 `<h2>` "Tags"에서 요소를 "태그 (M)":</span><span class="sxs-lookup"><span data-stu-id="3bb0f-200">Open the new file and change the `<h2>` element from "Tags" to "Tags (M)":</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample6.html)]

<span data-ttu-id="3bb0f-201">데스크톱 브라우저 및 모바일 브라우저 에뮬레이터를 사용 하 여 태그 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-201">Browse to the tags page using a desktop browser and using mobile browser emulator.</span></span> <span data-ttu-id="3bb0f-202">모바일 브라우저 에뮬레이터에는 두 개의 변경 내용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-202">The mobile browser emulator shows the two changes you made.</span></span>

<span data-ttu-id="3bb0f-203">[![p2m_layoutTags.mobile](aspnet-mvc-4-mobile-features/_static/image12.png)](aspnet-mvc-4-mobile-features/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-203">[![p2m_layoutTags.mobile](aspnet-mvc-4-mobile-features/_static/image12.png)](aspnet-mvc-4-mobile-features/_static/image11.png)</span></span>

<span data-ttu-id="3bb0f-204">반면, 바탕 화면 변경 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-204">In contrast, the desktop display has not changed.</span></span>

<span data-ttu-id="3bb0f-205">[![p2_layoutTagsDesktop](aspnet-mvc-4-mobile-features/_static/image14.png)](aspnet-mvc-4-mobile-features/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-205">[![p2_layoutTagsDesktop](aspnet-mvc-4-mobile-features/_static/image14.png)](aspnet-mvc-4-mobile-features/_static/image13.png)</span></span>

## <a name="browser-specific-views"></a><span data-ttu-id="3bb0f-206">브라우저의 뷰</span><span class="sxs-lookup"><span data-stu-id="3bb0f-206">Browser-Specific Views</span></span>

<span data-ttu-id="3bb0f-207">모바일 및 데스크톱 관련 뷰 외에도 개별 브라우저에 대 한 보기를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-207">In addition to mobile-specific and desktop-specific views, you can create views for an individual browser.</span></span> <span data-ttu-id="3bb0f-208">예를 들어, iPhone 브라우저에만 사용 되는 뷰를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-208">For example, you can create views that are specifically for the iPhone browser.</span></span> <span data-ttu-id="3bb0f-209">이 섹션에서는 iPhone 버전과 iPhone 브라우저에 대 한 레이아웃 만듭니다는 *AllTags* 보기.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-209">In this section, you'll create a layout for the iPhone browser and an iPhone version of the *AllTags* view.</span></span>

<span data-ttu-id="3bb0f-210">열기는 *Global.asax* 파일을 다음 코드를 추가 하는 `Application_Start` 메서드.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-210">Open the *Global.asax* file and add the following code to the `Application_Start` method.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample7.cs)]

<span data-ttu-id="3bb0f-211">이 코드는 들어오는 각 요청에 대해 일치 시킬 "iPhone" 라는 새 디스플레이 모드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-211">This code defines a new display mode named "iPhone" that will be matched against each incoming request.</span></span> <span data-ttu-id="3bb0f-212">(즉, 포함 되 면 사용자 에이전트는 "iPhone")를 정의 된 조건과 일치 하는 들어오는 요청을 하면 ASP.NET MVC는 이름이 "iPhone" 접미사를 포함 하는 뷰를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-212">If the incoming request matches the condition you defined (that is, if the user agent contains the string "iPhone"), ASP.NET MVC will look for views whose name contains the "iPhone" suffix.</span></span>

<span data-ttu-id="3bb0f-213">코드에서 마우스 오른쪽 단추로 클릭 `DefaultDisplayMode`, 선택 **해결**를 선택한 후 `using System.Web.WebPages;`합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-213">In the code, right-click `DefaultDisplayMode`, choose **Resolve**, and then choose `using System.Web.WebPages;`.</span></span> <span data-ttu-id="3bb0f-214">에 대 한 참조를 추가 하는이 `System.Web.WebPages` 에 네임 스페이스는 `DisplayModes` 및 `DefaultDisplayMode` 형식은 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-214">This adds a reference to the `System.Web.WebPages` namespace, which is where the `DisplayModes` and `DefaultDisplayMode` types are defined.</span></span>

<span data-ttu-id="3bb0f-215">[![p2_resolve](aspnet-mvc-4-mobile-features/_static/image16.png)](aspnet-mvc-4-mobile-features/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-215">[![p2_resolve](aspnet-mvc-4-mobile-features/_static/image16.png)](aspnet-mvc-4-mobile-features/_static/image15.png)</span></span>

<span data-ttu-id="3bb0f-216">또는 다음 줄을 방금 수동으로 추가할 수는 `using` 파일의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-216">Alternatively, you can just manually add the following line to the `using` section of the file.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample8.cs)]

<span data-ttu-id="3bb0f-217">전체 내용을 *Global.asax* 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-217">The complete contents of the *Global.asax* file is shown below.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample9.cs)]

<span data-ttu-id="3bb0f-218">변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-218">Save the changes.</span></span> <span data-ttu-id="3bb0f-219">복사는 *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* 파일을 *MvcMobile\Views\Shared\\_Layout.iPhone.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-219">Copy the *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* file to *MvcMobile\Views\Shared\\_Layout.iPhone.cshtml*.</span></span> <span data-ttu-id="3bb0f-220">새 파일을 열고 변경 하는 `h1` 에서 머리글 `Conference (Mobile)` 를 `Conference (iPhone)`합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-220">Open the new file and then change the `h1` heading from `Conference (Mobile)` to `Conference (iPhone)`.</span></span>

<span data-ttu-id="3bb0f-221">복사는 *MvcMobile\Views\Home\AllTags.Mobile.cshtml* 파일을 *MvcMobile\Views\Home\AllTags.iPhone.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-221">Copy the *MvcMobile\Views\Home\AllTags.Mobile.cshtml* file to *MvcMobile\Views\Home\AllTags.iPhone.cshtml*.</span></span> <span data-ttu-id="3bb0f-222">새 파일에서 변경 된 `<h2>` 요소에서 "태그 (M)"을 "태그 (iPhone)"입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-222">In the new file, change the `<h2>` element from "Tags (M)" to "Tags (iPhone)".</span></span>

<span data-ttu-id="3bb0f-223">응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-223">Run the application.</span></span> <span data-ttu-id="3bb0f-224">모바일 브라우저 에뮬레이터에서 앱 실행에서 사용자 에이전트를 "iPhone"로 설정 되어 있는지 확인 한를 찾습니다는 *AllTags* 보기.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-224">Run a mobile browser emulator, make sure its user agent is set to "iPhone", and browse to the *AllTags* view.</span></span> <span data-ttu-id="3bb0f-225">다음 스크린 샷에 표시는 *AllTags* 보기에서 렌더링 된 [Safari](http://www.apple.com/safari/download/) 브라우저.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-225">The following screenshot shows the *AllTags* view rendered in the [Safari](http://www.apple.com/safari/download/) browser.</span></span> <span data-ttu-id="3bb0f-226">Windows 용 Safari를 다운로드할 수 있습니다 [여기](https://support.apple.com/kb/DL1531)합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-226">You can download Safari for Windows [here](https://support.apple.com/kb/DL1531).</span></span>

<span data-ttu-id="3bb0f-227">[![p2_iphoneView](aspnet-mvc-4-mobile-features/_static/image18.png)](aspnet-mvc-4-mobile-features/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-227">[![p2_iphoneView](aspnet-mvc-4-mobile-features/_static/image18.png)](aspnet-mvc-4-mobile-features/_static/image17.png)</span></span>

<span data-ttu-id="3bb0f-228">이 섹션에서는 모바일 레이아웃, 보기를 만드는 방법과 레이아웃, iPhone 등 특정 장치에 대 한 보기를 만드는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-228">In this section we've seen how to create mobile layouts and views and how to create layouts and views for specific devices such as the iPhone.</span></span> <span data-ttu-id="3bb0f-229">다음 섹션에서 더 많은 매력적인 모바일 보기에 대 한 jQuery Mobile을 활용 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-229">In the next section you'll see how to leverage jQuery Mobile for more compelling mobile views.</span></span>

## <a name="using-jquery-mobile"></a><span data-ttu-id="3bb0f-230">JQuery Mobile을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="3bb0f-230">Using jQuery Mobile</span></span>

<span data-ttu-id="3bb0f-231">[jQuery Mobile](http://jquerymobile.com/demos/1.0b3/#/demos/1.0b3/docs/about/intro.html) 라이브러리에서 작동 하는 모든 주요 모바일 브라우저는 사용자 인터페이스 프레임 워크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-231">The [jQuery Mobile](http://jquerymobile.com/demos/1.0b3/#/demos/1.0b3/docs/about/intro.html) library provides a user interface framework that works on all the major mobile browsers.</span></span> <span data-ttu-id="3bb0f-232">jQuery Mobile 적용 *점진적인 기능 향상* CSS 및 JavaScript를 지 원하는 모바일 브라우저에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-232">jQuery Mobile applies *progressive enhancement* to mobile browsers that support CSS and JavaScript.</span></span> <span data-ttu-id="3bb0f-233">점진적인 기능 향상에 보다 강력한 브라우저와 장치를 보다 다양 한 표시를 허용 하는 동안 웹 페이지의 기본 콘텐츠를 표시 하는 모든 브라우저 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-233">Progressive enhancement allows all browsers to display the basic content of a web page, while allowing more powerful browsers and devices to have a richer display.</span></span> <span data-ttu-id="3bb0f-234">JQuery Mobile에 포함 된 JavaScript 및 CSS 파일에 태그를 변경 하지 않고 모바일 브라우저에 맞게 많은 요소 스타일 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-234">The JavaScript and CSS files that are included with jQuery Mobile style many elements to fit mobile browsers without making any markup changes.</span></span>

<span data-ttu-id="3bb0f-235">이 섹션의 설치는 *jQuery.Mobile.MVC* 뷰 전환기 위젯 및 jQuery Mobile을 설치 하는 NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-235">In this section you'll install the *jQuery.Mobile.MVC* NuGet package, which installs jQuery Mobile and a view-switcher widget.</span></span>

<span data-ttu-id="3bb0f-236">삭제를 시작 하려면는 *Shared\\_Layout.Mobile.cshtml* 및 *Shared\\_Layout.iPhone.cshtml* 앞에서 만든 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-236">To start, delete the *Shared\\_Layout.Mobile.cshtml* and *Shared\\_Layout.iPhone.cshtml* files that you created earlier.</span></span>

<span data-ttu-id="3bb0f-237">이름 바꾸기 *Views\Home\AllTags.Mobile.cshtml* 및 *Views\Home\AllTags.iPhone.cshtml* 파일을 *Views\Home\AllTags.iPhone.cshtml.hide* 및  *Views\Home\AllTags.Mobile.cshtml.hide*합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-237">Rename *Views\Home\AllTags.Mobile.cshtml* and *Views\Home\AllTags.iPhone.cshtml* files to *Views\Home\AllTags.iPhone.cshtml.hide* and *Views\Home\AllTags.Mobile.cshtml.hide*.</span></span> <span data-ttu-id="3bb0f-238">파일이 더 이상 없으므로 *.cshtml* 확장, 렌더링 하는 ASP.NET MVC 런타임에서 사용 되지 않습니다는 *AllTags* 보기.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-238">Because the files no longer have a *.cshtml* extension, they won't be used by the ASP.NET MVC runtime to render the *AllTags* view.</span></span>

<span data-ttu-id="3bb0f-239">설치는 *jQuery.Mobile.MVC* 이 수행 하 여 NuGet 패키지:</span><span class="sxs-lookup"><span data-stu-id="3bb0f-239">Install the *jQuery.Mobile.MVC* NuGet package by doing this:</span></span>

1. <span data-ttu-id="3bb0f-240">**도구** 메뉴 선택 **라이브러리 패키지 관리자**를 선택한 후 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-240">From the **Tools** menu, select **Library Package Manager**, and then select **Package Manager Console**.</span></span>

    <span data-ttu-id="3bb0f-241">[![p3_packageMgr](aspnet-mvc-4-mobile-features/_static/image20.png)](aspnet-mvc-4-mobile-features/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-241">[![p3_packageMgr](aspnet-mvc-4-mobile-features/_static/image20.png)](aspnet-mvc-4-mobile-features/_static/image19.png)</span></span>
2. <span data-ttu-id="3bb0f-242">에 **패키지 관리자 콘솔**, 입력`Install-Package jQuery.Mobile.MVC -version 1.0.0`</span><span class="sxs-lookup"><span data-stu-id="3bb0f-242">In the **Package Manager Console**, enter `Install-Package jQuery.Mobile.MVC -version 1.0.0`</span></span>

<span data-ttu-id="3bb0f-243">다음 이미지는 추가 및 MvcMobile 프로젝트에 NuGet jQuery.Mobile.MVC 패키지에서 변경 된 파일을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-243">The following image shows the files added and changed to the MvcMobile project by the NuGet jQuery.Mobile.MVC package.</span></span> <span data-ttu-id="3bb0f-244">파일 이름 뒤에 추가 [추가]가 추가 되는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-244">Files which are added have [add] appended after the file name.</span></span> <span data-ttu-id="3bb0f-245">GIF 이미지는 표시 되지 않습니다 및 PNG 파일에 추가 된 *Content\images* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-245">The image does not show the GIF and PNG files added to the *Content\images* folder.</span></span>

![](aspnet-mvc-4-mobile-features/_static/image21.png)

<span data-ttu-id="3bb0f-246">다음 jQuery.Mobile.MVC NuGet 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-246">The jQuery.Mobile.MVC NuGet package installs the following:</span></span>

- <span data-ttu-id="3bb0f-247">*앱\_Start\BundleMobileConfig.cs* 추가 jQuery JavaScript 및 CSS 파일을 참조 하는 데 필요한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-247">The *App\_Start\BundleMobileConfig.cs* file, which is needed to reference the jQuery JavaScript and CSS files added.</span></span> <span data-ttu-id="3bb0f-248">아래 지침에 따라 해야 하며이 파일에 정의 된 모바일 번들 참조 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-248">You must follow the instructions below and reference the mobile bundle defined in this file.</span></span>
- <span data-ttu-id="3bb0f-249">jQuery Mobile CSS 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-249">jQuery Mobile CSS files.</span></span>
- <span data-ttu-id="3bb0f-250">A `ViewSwitcher` 컨트롤러 위젯 (*Controllers\ViewSwitcherController.cs*).</span><span class="sxs-lookup"><span data-stu-id="3bb0f-250">A `ViewSwitcher` controller widget (*Controllers\ViewSwitcherController.cs*).</span></span>
- <span data-ttu-id="3bb0f-251">jQuery Mobile JavaScript 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-251">jQuery Mobile JavaScript files.</span></span>
- <span data-ttu-id="3bb0f-252">JQuery Mobile 스타일의 레이아웃 파일 (*Views\Shared\\_Layout.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="3bb0f-252">A jQuery Mobile-styled layout file (*Views\Shared\\_Layout.Mobile.cshtml*).</span></span>
- <span data-ttu-id="3bb0f-253">뷰 전환기 부분 뷰 *(MvcMobile\Views\Shared\\_ViewSwitcher.cshtml*) 하는 모바일 보기로 그리고 반대로 바탕 화면 보기에서 전환 하려면 각 페이지의 위쪽에 대 한 링크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-253">A view-switcher partial view *(MvcMobile\Views\Shared\\_ViewSwitcher.cshtml*) that provides a link at the top of each page to switch from desktop view to mobile view and vice versa.</span></span>
- <span data-ttu-id="3bb0f-254">여러*.png* 및 *.gif* 이미지 파일의 *Content\images* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-254">Several*.png* and *.gif* image files in the *Content\images* folder.</span></span>

<span data-ttu-id="3bb0f-255">열기는 *Global.asax* 파일의 마지막 줄으로 다음 코드를 추가 하 고는 `Application_Start` 메서드.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-255">Open the *Global.asax* file and add the following code as the last line of the `Application_Start` method.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample10.cs)]

<span data-ttu-id="3bb0f-256">다음 코드에서는 전체 *Global.asax* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-256">The following code shows the complete *Global.asax* file.</span></span>

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample11.cs?highlight=26)]

> [!NOTE]
> <span data-ttu-id="3bb0f-257">Internet Explorer 9를 사용 하 고 표시 되지 않는 경우는 `BundleMobileConfig` 노란색 강조 표시에 위의 줄, 클릭는 [호환성 보기 단추](https://windows.microsoft.com/windows7/How-to-use-Compatibility-View-in-Internet-Explorer-9)![(off) 호환성 보기 단추 그림] (http://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg " (Off) 호환성 보기 단추 그림") 개요에서 변경 아이콘을 확인 하는 IE의 ![(off) 호환성 보기 단추 그림](http://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "(해제) 호환성 보기 단추 그림 ") 단색 ![(on) 호환성 보기 단추 그림](http://res1.windows.microsoft.com/resbox/en/Windows 7/main/156805ff-3130-481b-a12d-4d3a96470f36_14.jpg "(on) 호환성 보기 단추 그림")합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-257">If you are using Internet Explorer 9 and you don't see the `BundleMobileConfig` line above in yellow highlight, click the [Compatibility View button](https://windows.microsoft.com/windows7/How-to-use-Compatibility-View-in-Internet-Explorer-9)![Picture of the Compatibility View button (off)](http://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "Picture of the Compatibility View button (off)") in IE to make the icon change from an outline ![Picture of the Compatibility View button (off)](http://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "Picture of the Compatibility View button (off)") to a solid color ![Picture of the Compatibility View button (on)](http://res1.windows.microsoft.com/resbox/en/Windows 7/main/156805ff-3130-481b-a12d-4d3a96470f36_14.jpg "Picture of the Compatibility View button (on)").</span></span> <span data-ttu-id="3bb0f-258">또는 FireFox 또는 Chrome에서이 자습서를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-258">Alternatively you can view this tutorial in FireFox or Chrome.</span></span>


<span data-ttu-id="3bb0f-259">열기는 *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* 파일을 다음 태그 바로 뒤에 추가 된 `Html.Partial` 호출:</span><span class="sxs-lookup"><span data-stu-id="3bb0f-259">Open the *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* file and add the following markup directly after the `Html.Partial` call:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample12.cshtml)]

<span data-ttu-id="3bb0f-260">전체 *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-260">The complete *MvcMobile\Views\Shared\\_Layout.Mobile.cshtml* file is shown below:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample13.cshtml)]

<span data-ttu-id="3bb0f-261">응용 프로그램을 빌드 및 모바일 브라우저 에뮬레이터에서 찾은 *AllTags* 보기.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-261">Build the application, and in your mobile browser emulator browse to the *AllTags* view.</span></span> <span data-ttu-id="3bb0f-262">다음 화면이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-262">You see the following:</span></span>

<span data-ttu-id="3bb0f-263">[![p3_afterNuGet](aspnet-mvc-4-mobile-features/_static/image23.png)](aspnet-mvc-4-mobile-features/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-263">[![p3_afterNuGet](aspnet-mvc-4-mobile-features/_static/image23.png)](aspnet-mvc-4-mobile-features/_static/image22.png)</span></span>

> [!NOTE]
> <span data-ttu-id="3bb0f-264">모바일 특정 코드를 디버깅할 수 [사용자 에이전트 문자열을 설정](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) IE 또는 iPhone 및 다음 F-12 개발자 도구를 사용 하 여 Chrome에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-264">You can debug the mobile specific code by [setting the user agent string](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/) for IE or Chrome to iPhone and then using the F-12 developer tools.</span></span> <span data-ttu-id="3bb0f-265">모바일 브라우저에 표시 되지 않는 경우는 **홈**, **스피커**, **태그**, 및 **날짜** 단추로 링크, jQuery Mobile에 대 한 참조 스크립트 및 CSS 파일 아마도 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-265">If your mobile browser doesn't display the **Home**, **Speaker**, **Tag**, and **Date** links as buttons, the references to jQuery Mobile scripts and CSS files are probably not correct.</span></span>


<span data-ttu-id="3bb0f-266">참조 스타일 변경 내용 외에 **모바일 보기 표시** 및 바탕 화면 보기 모바일 보기에서 전환할 수 있는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-266">In addition to the style changes, you see **Displaying mobile view** and a link that lets you switch from mobile view to desktop view.</span></span> <span data-ttu-id="3bb0f-267">선택 된 **바탕 화면 보기** 링크 및 바탕 화면 보기에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-267">Choose the **Desktop view** link, and the desktop view is displayed.</span></span>

<span data-ttu-id="3bb0f-268">[![p3_desktopView](aspnet-mvc-4-mobile-features/_static/image25.png)](aspnet-mvc-4-mobile-features/_static/image24.png)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-268">[![p3_desktopView](aspnet-mvc-4-mobile-features/_static/image25.png)](aspnet-mvc-4-mobile-features/_static/image24.png)</span></span>

<span data-ttu-id="3bb0f-269">바탕 화면 보기에는 직접 모바일 보기로 다시 이동 하는 방법을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-269">The desktop view doesn't provide a way to directly navigate back to the mobile view.</span></span> <span data-ttu-id="3bb0f-270">지금 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-270">You'll fix that now.</span></span> <span data-ttu-id="3bb0f-271">열기는 *Views\Shared\\_Layout.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-271">Open the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="3bb0f-272">페이지 아래에서 방금 `body` 요소를 뷰 전환기 위젯 렌더링 하는 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-272">Just under the page `body` element, add the following code, which renders the view-switcher widget:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample14.cshtml)]

<span data-ttu-id="3bb0f-273">새로 고침의 *AllTags* 모바일 브라우저에서 보기.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-273">Refresh the *AllTags* view in the mobile browser.</span></span> <span data-ttu-id="3bb0f-274">데스크톱 및 모바일 뷰 간에 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-274">You can now navigate between desktop and mobile views.</span></span>

<span data-ttu-id="3bb0f-275">[![p3_desktopViewWithMobileLink](aspnet-mvc-4-mobile-features/_static/image27.png)](aspnet-mvc-4-mobile-features/_static/image26.png)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-275">[![p3_desktopViewWithMobileLink](aspnet-mvc-4-mobile-features/_static/image27.png)](aspnet-mvc-4-mobile-features/_static/image26.png)</span></span>

> [!NOTE]
> <span data-ttu-id="3bb0f-276">디버깅 참고:는 Views\Shared의 끝에 다음 코드를 추가할 수 있습니다\\_ViewSwitcher.cshtml 브라우저 사용자 에이전트 문자열을 사용 하 여 모바일 장치를 설정 하는 경우 뷰를 디버깅할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-276">Debug note: You can add the following code to the end of the Views\Shared\\_ViewSwitcher.cshtml to help debug views when using a browser the user agent string set to a mobile device.</span></span>
> 
> [!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample15.cs)]
> 
>  <span data-ttu-id="3bb0f-277">다음과 같은 머리글을 추가 하 고는 *Views\Shared\\_Layout.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-277">and adding the following heading to the *Views\Shared\\_Layout.cshtml* file.</span></span>  
> 
> [!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample16.html)]


<span data-ttu-id="3bb0f-278">찾아는 *AllTags* 데스크톱 브라우저에서 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-278">Browse to the *AllTags* page in a desktop browser.</span></span> <span data-ttu-id="3bb0f-279">뷰 전환기 위젯 모바일 레이아웃 페이지에만 추가 되므로 데스크톱 브라우저에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-279">The view-switcher widget is not displayed in a desktop browser because it's added only to the mobile layout page.</span></span> <span data-ttu-id="3bb0f-280">자습서의 뒷부분에 나오는 추가 하는 방법을 뷰 전환기 위젯 바탕 화면 보기에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-280">Later in the tutorial you'll see how you can add the view-switcher widget to the desktop view.</span></span>

<span data-ttu-id="3bb0f-281">[![p3_desktopBrowser](aspnet-mvc-4-mobile-features/_static/image29.png)](aspnet-mvc-4-mobile-features/_static/image28.png)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-281">[![p3_desktopBrowser](aspnet-mvc-4-mobile-features/_static/image29.png)](aspnet-mvc-4-mobile-features/_static/image28.png)</span></span>

## <a name="improving-the-speakers-list"></a><span data-ttu-id="3bb0f-282">스피커 목록 개선</span><span class="sxs-lookup"><span data-stu-id="3bb0f-282">Improving the Speakers List</span></span>

<span data-ttu-id="3bb0f-283">모바일 브라우저에서 선택 된 **스피커** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-283">In the mobile browser, select the **Speakers** link.</span></span> <span data-ttu-id="3bb0f-284">모바일 뷰가 있기 때문에 (*AllSpeakers.Mobile.cshtml*), 기본 스피커 표시 (*AllSpeakers.cshtml*) 모바일 레이아웃 보기를 사용 하 여 렌더링 됩니다 ( *\_ Layout.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="3bb0f-284">Because there's no mobile view(*AllSpeakers.Mobile.cshtml*), the default speakers display (*AllSpeakers.cshtml*) is rendered using the mobile layout view (*\_Layout.Mobile.cshtml*).</span></span>

<span data-ttu-id="3bb0f-285">[![p3_speakersDeskTop](aspnet-mvc-4-mobile-features/_static/image31.png)](aspnet-mvc-4-mobile-features/_static/image30.png)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-285">[![p3_speakersDeskTop](aspnet-mvc-4-mobile-features/_static/image31.png)](aspnet-mvc-4-mobile-features/_static/image30.png)</span></span>

<span data-ttu-id="3bb0f-286">전역으로 설정 하 여 렌더링 모바일 레이아웃 내에서 기본 (비모바일) 뷰를 비활성화할 수 있습니다 `RequireConsistentDisplayMode` 를 `true` 에 *뷰\\_viewstart.vbhtml* 다음과 같이 파일:</span><span class="sxs-lookup"><span data-stu-id="3bb0f-286">You can globally disable a default (non-mobile) view from rendering inside a mobile layout by setting `RequireConsistentDisplayMode` to `true` in the *Views\\_ViewStart.cshtml* file, like this:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample17.cshtml)]

<span data-ttu-id="3bb0f-287">때 `RequireConsistentDisplayMode` 로 설정 된 `true`, 모바일 레이아웃 (*\_Layout.Mobile.cshtml*) 모바일 보기에만 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-287">When `RequireConsistentDisplayMode` is set to `true`, the mobile layout (*\_Layout.Mobile.cshtml*) is used only for mobile views.</span></span> <span data-ttu-id="3bb0f-288">(즉, 파일 보기 된 형식인 ***ViewName**합니다. Mobile.cshtml*입니다.) 설정 하려는 경우 `RequireConsistentDisplayMode` 를 `true` 모바일 레이아웃 비모바일 보기와 잘 작동 하지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-288">(That is, the view file is of the form ***ViewName**.Mobile.cshtml*.) You might want to set `RequireConsistentDisplayMode` to `true` if your mobile layout doesn't work well with your non-mobile views.</span></span> <span data-ttu-id="3bb0f-289">다음 스크린샷에서 방법을 *스피커* 페이지를 렌더링 하는 경우 `RequireConsistentDisplayMode` 로 설정 된 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-289">The screenshot below shows how the *Speakers* page renders when `RequireConsistentDisplayMode` is set to `true`.</span></span>

<span data-ttu-id="3bb0f-290">[![p3_speakersConsistent](aspnet-mvc-4-mobile-features/_static/image33.png)](aspnet-mvc-4-mobile-features/_static/image32.png)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-290">[![p3_speakersConsistent](aspnet-mvc-4-mobile-features/_static/image33.png)](aspnet-mvc-4-mobile-features/_static/image32.png)</span></span>

<span data-ttu-id="3bb0f-291">설정 하 여 보기에 일관 된 표시 모드를 해제할 수 `RequireConsistentDisplayMode` 를 `false` 보기 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-291">You can disable consistent display mode in a view by setting `RequireConsistentDisplayMode` to `false` in the view file.</span></span> <span data-ttu-id="3bb0f-292">에 다음 태그는 *Views\Home\AllSpeakers.cshtml* 파일 집합 `RequireConsistentDisplayMode` 를 `false`:</span><span class="sxs-lookup"><span data-stu-id="3bb0f-292">The following markup in the *Views\Home\AllSpeakers.cshtml* file sets `RequireConsistentDisplayMode` to `false`:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample18.cshtml)]

## <a name="creating-a-mobile-speakers-view"></a><span data-ttu-id="3bb0f-293">모바일 스피커 보기를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="3bb0f-293">Creating a Mobile Speakers View</span></span>

<span data-ttu-id="3bb0f-294">본 것 처럼는 *스피커* 보기 사용자가 읽을 수 있지만 링크는 작은 이며 모바일 장치를 탭 하기 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-294">As you just saw, the *Speakers* view is readable, but the links are small and are difficult to tap on a mobile device.</span></span> <span data-ttu-id="3bb0f-295">이 섹션에서는 모바일 전용 만듭니다 *스피커* 최신 모바일 응용 프로그램 같은 보기-큰 표시, tap 쉽게 연결 하 고 스피커를 빠르게 찾기 위해 검색 상자를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-295">In this section, you'll create a mobile-specific *Speakers* view that looks like a modern mobile application — it displays large, easy-to-tap links and contains a search box to quickly find speakers.</span></span>

<span data-ttu-id="3bb0f-296">복사 *AllSpeakers.cshtml* 를 *AllSpeakers.Mobile.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-296">Copy *AllSpeakers.cshtml* to *AllSpeakers.Mobile.cshtml*.</span></span> <span data-ttu-id="3bb0f-297">열기는 *AllSpeakers.Mobile.cshtml* 파일을 제거는 `<h2>` 제목 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-297">Open the *AllSpeakers.Mobile.cshtml* file and remove the `<h2>` heading element.</span></span>

<span data-ttu-id="3bb0f-298">에 `<ul>` 태그, 추가 된 `data-role` 특성 및 값을 설정 `listview`합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-298">In the `<ul>` tag, add the `data-role` attribute and set its value to `listview`.</span></span> <span data-ttu-id="3bb0f-299">와 같은 다른 [ `data-*` 특성](http://html5doctor.com/html5-custom-data-attributes/), `data-role="listview"` 을 탭 하 큰 목록 항목을 더 쉽게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-299">Like other [`data-*` attributes](http://html5doctor.com/html5-custom-data-attributes/), `data-role="listview"` makes the large list items easier to tap.</span></span> <span data-ttu-id="3bb0f-300">다음은 완성 된 태그의 모양을입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-300">This is what the completed markup looks like:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample19.cshtml)]

<span data-ttu-id="3bb0f-301">모바일 브라우저를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-301">Refresh the mobile browser.</span></span> <span data-ttu-id="3bb0f-302">업데이트 된 보기는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-302">The updated view looks like this:</span></span>

<span data-ttu-id="3bb0f-303">[![p3_updatedSpeakerView1](aspnet-mvc-4-mobile-features/_static/image35.png)](aspnet-mvc-4-mobile-features/_static/image34.png)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-303">[![p3_updatedSpeakerView1](aspnet-mvc-4-mobile-features/_static/image35.png)](aspnet-mvc-4-mobile-features/_static/image34.png)</span></span>

<span data-ttu-id="3bb0f-304">모바일 보기 기능이 향상 되기는 하지만 스피커의 긴 목록을 탐색 하 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-304">Although the mobile view has improved, it's difficult to navigate the long list of speakers.</span></span> <span data-ttu-id="3bb0f-305">이 해결 하려면는 `<ul>` 태그, 추가 `data-filter` 로 설정 하 고 특성 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-305">To fix this, in the `<ul>` tag, add the `data-filter` attribute and set it to `true`.</span></span> <span data-ttu-id="3bb0f-306">다음 코드는 `ul` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-306">The code below shows the `ul` markup.</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample20.html)]

<span data-ttu-id="3bb0f-307">다음 이미지는 검색 필터 상자의 결과로 생성 되는 페이지의 위쪽에 표시 된 `data-filter` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-307">The following image shows the search filter box at the top of the page that results from the `data-filter` attribute.</span></span>

<span data-ttu-id="3bb0f-308">[![ps_Data_Filter](aspnet-mvc-4-mobile-features/_static/image37.png)](aspnet-mvc-4-mobile-features/_static/image36.png)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-308">[![ps_Data_Filter](aspnet-mvc-4-mobile-features/_static/image37.png)](aspnet-mvc-4-mobile-features/_static/image36.png)</span></span>

<span data-ttu-id="3bb0f-309">검색 상자에 각 문자를 입력할 때 jQuery Mobile 아래 이미지에 나와 있는 것 처럼 표시 된 목록을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-309">As you type each letter in the search box, jQuery Mobile filters the displayed list as shown in the image below.</span></span>

<span data-ttu-id="3bb0f-310">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image39.png)](aspnet-mvc-4-mobile-features/_static/image38.png)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-310">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image39.png)](aspnet-mvc-4-mobile-features/_static/image38.png)</span></span>

## <a name="improving-the-tags-list"></a><span data-ttu-id="3bb0f-311">태그 목록 개선</span><span class="sxs-lookup"><span data-stu-id="3bb0f-311">Improving the Tags List</span></span>

<span data-ttu-id="3bb0f-312">기본값이 마음에 *스피커* 보기는 *태그* 보기 사용자가 읽을 수 있지만 링크는 작은 모바일 장치를 탭 하기가 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-312">Like the default *Speakers* view, the *Tags* view is readable, but the links are small and difficult to tap on a mobile device.</span></span> <span data-ttu-id="3bb0f-313">이 섹션에서는 수정 합니다는 *태그* 고정 여부에 관계 없이 동일한 방식으로 볼는 *스피커* 보기.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-313">In this section, you'll fix the *Tags* view the same way you fixed the *Speakers* view.</span></span>

<span data-ttu-id="3bb0f-314">제거는 &quot;숨기기&quot; 에 접미사는 *Views\Home\AllTags.Mobile.cshtml.hide* 하므로 이름이 파일 *Views\Home\AllTags.Mobile.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-314">Remove the &quot;hide&quot; suffix to the the *Views\Home\AllTags.Mobile.cshtml.hide* file so the name is *Views\Home\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="3bb0f-315">이름이 바뀐된 파일을 열고 제거는 `<h2>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-315">Open the renamed file and remove the `<h2>` element.</span></span>

<span data-ttu-id="3bb0f-316">추가 `data-role` 및 `data-filter` 특성에 `<ul>` 태그를 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-316">Add the `data-role` and `data-filter` attributes to the `<ul>` tag, as shown here:</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample21.html)]

<span data-ttu-id="3bb0f-317">아래 이미지에서 문자 필터링 태그 페이지를 보여 줍니다. `J`합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-317">The image below shows the tags page filtering on the letter `J`.</span></span>

<span data-ttu-id="3bb0f-318">[![p3_tags_J](aspnet-mvc-4-mobile-features/_static/image41.png)](aspnet-mvc-4-mobile-features/_static/image40.png)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-318">[![p3_tags_J](aspnet-mvc-4-mobile-features/_static/image41.png)](aspnet-mvc-4-mobile-features/_static/image40.png)</span></span>

## <a name="improving-the-dates-list"></a><span data-ttu-id="3bb0f-319">날짜 목록 개선</span><span class="sxs-lookup"><span data-stu-id="3bb0f-319">Improving the Dates List</span></span>

<span data-ttu-id="3bb0f-320">향상 시킬 수 있습니다는 *날짜* 향상 된 처럼 볼는 *스피커* 및 *태그* 뷰를 보다 쉽게 모바일 장치에서 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-320">You can improve the *Dates* view like you improved the *Speakers* and *Tags* views, so that it's easier to use on a mobile device.</span></span>

<span data-ttu-id="3bb0f-321">복사는 *Views\Home\AllDates.cshtml* 파일을 *Views\Home\AllDates.Mobile.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-321">Copy the *Views\Home\AllDates.cshtml* file to *Views\Home\AllDates.Mobile.cshtml*.</span></span> <span data-ttu-id="3bb0f-322">새 파일을 열고 제거는 `<h2>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-322">Open the new file and remove the `<h2>` element.</span></span>

<span data-ttu-id="3bb0f-323">추가 `data-role="listview"` 에 `<ul>` 다음과 같은 태그:</span><span class="sxs-lookup"><span data-stu-id="3bb0f-323">Add `data-role="listview"` to the `<ul>` tag, like this:</span></span>

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample22.html)]

<span data-ttu-id="3bb0f-324">아래 이미지에서는 **날짜** 와 같이 페이지는 `data-role` 위치에 대 한 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-324">The image below shows what the **Date** page looks like with the `data-role` attribute in place.</span></span>

<span data-ttu-id="3bb0f-325">[![p3_dates1](aspnet-mvc-4-mobile-features/_static/image43.png)](aspnet-mvc-4-mobile-features/_static/image42.png) 의 내용을 대체는 *Views\Home\AllDates.Mobile.cshtml* 를 다음 코드로 파일:</span><span class="sxs-lookup"><span data-stu-id="3bb0f-325">[![p3_dates1](aspnet-mvc-4-mobile-features/_static/image43.png)](aspnet-mvc-4-mobile-features/_static/image42.png) Replace the contents of the *Views\Home\AllDates.Mobile.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample23.cshtml)]

<span data-ttu-id="3bb0f-326">이 코드는 일별로 모든 세션을 그룹화합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-326">This code groups all sessions by days.</span></span> <span data-ttu-id="3bb0f-327">새로운 각 날에 대 한 목록 구분선을 만들므로 목록과 구분선 아래에서 각 날짜에 대 한 모든 세션.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-327">It creates a list divider for each new day, and it lists all the sessions for each day under a divider.</span></span> <span data-ttu-id="3bb0f-328">이 코드를 실행할 때 모양 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-328">Here's what it looks like when this code runs:</span></span>

<span data-ttu-id="3bb0f-329">[![p3_dates2](aspnet-mvc-4-mobile-features/_static/image45.png)](aspnet-mvc-4-mobile-features/_static/image44.png)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-329">[![p3_dates2](aspnet-mvc-4-mobile-features/_static/image45.png)](aspnet-mvc-4-mobile-features/_static/image44.png)</span></span>

## <a name="improving-the-sessionstable-view"></a><span data-ttu-id="3bb0f-330">SessionsTable 보기 향상</span><span class="sxs-lookup"><span data-stu-id="3bb0f-330">Improving the SessionsTable View</span></span>

<span data-ttu-id="3bb0f-331">이 섹션에서는 세션 모바일 전용 보기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-331">In this section, you'll create a mobile-specific view of sessions.</span></span> <span data-ttu-id="3bb0f-332">변경 하도록 준비 되어 다른 보기에서 보다 더욱 광범위 한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-332">The changes we make will be more extensive than in other views we have created.</span></span>

<span data-ttu-id="3bb0f-333">모바일 브라우저 탭에서 **스피커** 입력 한 다음 단추를 `Sc` 검색 상자에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-333">In the mobile browser, tap the **Speaker** button, then enter `Sc` in the search box.</span></span>

<span data-ttu-id="3bb0f-334">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image47.png)](aspnet-mvc-4-mobile-features/_static/image46.png)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-334">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image47.png)](aspnet-mvc-4-mobile-features/_static/image46.png)</span></span>

<span data-ttu-id="3bb0f-335">탭의 **Scott Hanselman** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-335">Tap the **Scott Hanselman** link.</span></span>

<span data-ttu-id="3bb0f-336">[![p3_scottHa](aspnet-mvc-4-mobile-features/_static/image49.png)](aspnet-mvc-4-mobile-features/_static/image48.png)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-336">[![p3_scottHa](aspnet-mvc-4-mobile-features/_static/image49.png)](aspnet-mvc-4-mobile-features/_static/image48.png)</span></span>

<span data-ttu-id="3bb0f-337">볼 수 있듯이 디스플레이가 모바일 브라우저를 읽기가 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-337">As you can see, the display is difficult to read on a mobile browser.</span></span> <span data-ttu-id="3bb0f-338">날짜 열이 읽기 어려운 및은 보기에서 태그 열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-338">The date column is hard to read and the tags column is out of the view.</span></span> <span data-ttu-id="3bb0f-339">이 문제를 해결 하려면 복사 *Views\Home\SessionsTable.cshtml* 를 *Views\Home\SessionsTable.Mobile.cshtml*, 파일의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-339">To fix this, copy *Views\Home\SessionsTable.cshtml* to *Views\Home\SessionsTable.Mobile.cshtml*, and then replace the contents of the file with the following code:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample24.cshtml)]

<span data-ttu-id="3bb0f-340">코드 태그 열, 및이 모든 정보는 모바일 브라우저에서 읽을 수 있도록 제목과 스피커, 날짜를 세로로 서식을 대화방을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-340">The code removes the room and tags columns, and formats the title, speaker, and date vertically, so that all this information is readable on a mobile browser.</span></span> <span data-ttu-id="3bb0f-341">아래 이미지에는 코드 변경 내용을 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-341">The image below reflects the code changes.</span></span>

<span data-ttu-id="3bb0f-342">[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image51.png)](aspnet-mvc-4-mobile-features/_static/image50.png)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-342">[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image51.png)](aspnet-mvc-4-mobile-features/_static/image50.png)</span></span>

## <a name="improving-the-sessionbycode-view"></a><span data-ttu-id="3bb0f-343">SessionByCode 보기 향상</span><span class="sxs-lookup"><span data-stu-id="3bb0f-343">Improving the SessionByCode View</span></span>

<span data-ttu-id="3bb0f-344">모바일 전용 보기를 만듭니다 마지막으로 *SessionByCode* 보기.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-344">Finally, you'll create a mobile-specific view of the *SessionByCode* view.</span></span> <span data-ttu-id="3bb0f-345">모바일 브라우저 탭에서 **스피커** 입력 한 다음 단추를 `Sc` 검색 상자에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-345">In the mobile browser, tap the **Speaker** button, then enter `Sc` in the search box.</span></span>

<span data-ttu-id="3bb0f-346">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image53.png)](aspnet-mvc-4-mobile-features/_static/image52.png)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-346">[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image53.png)](aspnet-mvc-4-mobile-features/_static/image52.png)</span></span>

<span data-ttu-id="3bb0f-347">탭의 **Scott Hanselman** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-347">Tap the **Scott Hanselman** link.</span></span> <span data-ttu-id="3bb0f-348">Scott Hanselman 세션이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-348">Scott Hanselman's sessions are displayed.</span></span>

<span data-ttu-id="3bb0f-349">[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image55.png)](aspnet-mvc-4-mobile-features/_static/image54.png)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-349">[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image55.png)](aspnet-mvc-4-mobile-features/_static/image54.png)</span></span>

<span data-ttu-id="3bb0f-350">선택 된 **An MS 웹 Love 스택 개요** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-350">Choose the **An Overview of the MS Web Stack of Love** link.</span></span>

<span data-ttu-id="3bb0f-351">[![ps_love](aspnet-mvc-4-mobile-features/_static/image57.png)](aspnet-mvc-4-mobile-features/_static/image56.png)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-351">[![ps_love](aspnet-mvc-4-mobile-features/_static/image57.png)](aspnet-mvc-4-mobile-features/_static/image56.png)</span></span>

<span data-ttu-id="3bb0f-352">기본 바탕 화면 보기 하지만,이 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-352">The default desktop view is fine, but you can improve it.</span></span>

<span data-ttu-id="3bb0f-353">복사는 *Views\Home\SessionByCode.cshtml* 를 *Views\Home\SessionByCode.Mobile.cshtml* 의 내용을 대체 하 고는 *Views\Home\SessionByCode.Mobile.cshtml*다음 태그로 파일:</span><span class="sxs-lookup"><span data-stu-id="3bb0f-353">Copy the *Views\Home\SessionByCode.cshtml* to *Views\Home\SessionByCode.Mobile.cshtml* and replace the contents of the *Views\Home\SessionByCode.Mobile.cshtml* file with the following markup:</span></span>

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample25.cshtml)]

<span data-ttu-id="3bb0f-354">새 태그를 사용 하 여는 `data-role` 특성 보기의 레이아웃을 개선 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-354">The new markup uses the `data-role` attribute to improve the layout of the view.</span></span>

<span data-ttu-id="3bb0f-355">모바일 브라우저를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-355">Refresh the mobile browser.</span></span> <span data-ttu-id="3bb0f-356">다음 그림에는 방금 만든 코드 변경 내용을 반영 합니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-356">The following image reflects the code changes that you just made:</span></span>

<span data-ttu-id="3bb0f-357">[![p3_love2](aspnet-mvc-4-mobile-features/_static/image59.png)](aspnet-mvc-4-mobile-features/_static/image58.png)</span><span class="sxs-lookup"><span data-stu-id="3bb0f-357">[![p3_love2](aspnet-mvc-4-mobile-features/_static/image59.png)](aspnet-mvc-4-mobile-features/_static/image58.png)</span></span>

## <a name="wrapup-and-review"></a><span data-ttu-id="3bb0f-358">Wrapup 및 검토</span><span class="sxs-lookup"><span data-stu-id="3bb0f-358">Wrapup and Review</span></span>

<span data-ttu-id="3bb0f-359">이 자습서에 ASP.NET MVC 4 Developer Preview의 새로운 모바일 기능을 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-359">This tutorial has introduced the new mobile features of ASP.NET MVC 4 Developer Preview.</span></span> <span data-ttu-id="3bb0f-360">모바일 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-360">The mobile features include:</span></span>

- <span data-ttu-id="3bb0f-361">전역 및 개별 보기에 대 한 레이아웃, 뷰 및 부분 뷰를 재정의 하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-361">The ability to override layout, views, and partial views, both globally and for an individual view.</span></span>
- <span data-ttu-id="3bb0f-362">레이아웃 및 사용 하 여 부분 재정의 적용에 대 한 제어는 `RequireConsistentDisplayMode` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-362">Control over layout and partial override enforcement using the `RequireConsistentDisplayMode` property.</span></span>
- <span data-ttu-id="3bb0f-363">모바일 앱을 위해 뷰 전환기 위젯 데스크톱 보기에 표시할 수 있는 뷰.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-363">A view-switcher widget for mobile views than can also be displayed in desktop views.</span></span>
- <span data-ttu-id="3bb0f-364">IPhone 브라우저와 같은 특정 브라우저 지원에 대 한 지원.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-364">Support for supporting specific browsers, such as the iPhone browser.</span></span>

## <a name="see-also"></a><span data-ttu-id="3bb0f-365">참고 항목</span><span class="sxs-lookup"><span data-stu-id="3bb0f-365">See Also</span></span>

- <span data-ttu-id="3bb0f-366">[jQuery Mobile](http://jquerymobile.com) 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="3bb0f-366">[jQuery Mobile](http://jquerymobile.com) site.</span></span>
- [<span data-ttu-id="3bb0f-367">jQuery Mobile 개요</span><span class="sxs-lookup"><span data-stu-id="3bb0f-367">jQuery Mobile Overview</span></span>](http://jquerymobile.com/demos/1.0b3/docs/about/intro.html)
- [<span data-ttu-id="3bb0f-368">W3C 권장 사항 모바일 웹 응용 프로그램 모범 사례</span><span class="sxs-lookup"><span data-stu-id="3bb0f-368">W3C Recommendation Mobile Web Application Best Practices</span></span>](http://www.w3.org/TR/mwabp/)
- [<span data-ttu-id="3bb0f-369">미디어 쿼리에 대 한 W3C Candidate Recommendation</span><span class="sxs-lookup"><span data-stu-id="3bb0f-369">W3C Candidate Recommendation for media queries</span></span>](http://www.w3.org/TR/css3-mediaqueries/)
