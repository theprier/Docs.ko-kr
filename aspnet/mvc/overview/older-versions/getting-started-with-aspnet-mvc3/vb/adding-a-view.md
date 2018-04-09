---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-view
title: 뷰 (VB) 추가 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 즉를 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: d3633f64-5d3c-45c9-ae4b-cb1563e3739f
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: c9675eb7776116ecbe910d5515abfe9b4391df22
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="adding-a-view-vb"></a><span data-ttu-id="23e56-103">(VB) 뷰 추가</span><span class="sxs-lookup"><span data-stu-id="23e56-103">Adding a View (VB)</span></span>
====================
<span data-ttu-id="23e56-104">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="23e56-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="23e56-105">이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1, 즉 Microsoft Visual Studio의 무료 버전을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 구축 하는 기초 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="23e56-106">시작 하기 전에 아래에 나열 된 필수 구성 요소가 설치 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="23e56-107">다음 링크를 클릭 하 여 모두를 설치할 수 있습니다: [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="23e56-108">또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="23e56-109">Visual Studio Web Developer Express SP1 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="23e56-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="23e56-110">ASP.NET MVC 3 도구 업데이트</span><span class="sxs-lookup"><span data-stu-id="23e56-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="23e56-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)</span><span class="sxs-lookup"><span data-stu-id="23e56-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="23e56-112">Visual Studio 2010 Visual Web Developer 2010 대신를 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소 설치: [Visual Studio 2010 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="23e56-113">이 항목에 수반 VB.NET 소스 코드를 사용 하 여 Visual Web Developer 프로젝트 ´ ù.</span><span class="sxs-lookup"><span data-stu-id="23e56-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="23e56-114">[VB.NET 버전을 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="23e56-115">원하는 경우 C#으로 전환 된 [C# 버전](../cs/adding-a-view.md) 이 자습서의 합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-115">If you prefer C#, switch to the [C# version](../cs/adding-a-view.md) of this tutorial.</span></span>


<span data-ttu-id="23e56-116">이 섹션에서는 여기 수정 하는 `HelloWorldController` 을 명확 하 게 보기 템플릿 파일을 사용 하는 클래스 클라이언트에 HTML 응답을 생성 하는 과정을 캡슐화 합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-116">In this section we're going to modify the `HelloWorldController` class to use a view template file to cleanly encapsulate the process of generating HTML responses to a client.</span></span>

<span data-ttu-id="23e56-117">와 뷰 템플릿을 사용 하 여 시작 하겠습니다는 `Index` 에서 메서드는 `HelloWorldController` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-117">Let's start by using a view template with the `Index` method in the `HelloWorldController` class.</span></span> <span data-ttu-id="23e56-118">현재는 `Index` 메서드 컨트롤러 클래스 내에서 하드 코드 하는 메시지 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-118">Currently the `Index` method returns a string with a message that is hard-coded within the controller class.</span></span> <span data-ttu-id="23e56-119">변경 된 `Index` 반환 하는 메서드는 `View` 다음과 같이 개체:</span><span class="sxs-lookup"><span data-stu-id="23e56-119">Change the `Index` method to return a `View` object, as shown in the following:</span></span>

[!code-vb[Main](adding-a-view/samples/sample1.vb)]

<span data-ttu-id="23e56-120">이제 템플릿 보기에 추가으로 호출할 수 있습니다이 프로젝트는 `Index` 메서드.</span><span class="sxs-lookup"><span data-stu-id="23e56-120">Let's now add a view template to our project that we can invoke with the `Index` method.</span></span> <span data-ttu-id="23e56-121">이렇게 하려면 마우스 오른쪽 단추로 클릭는 `Index` 클릭 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-121">To do this, right-click inside the `Index` method and click **Add View**.</span></span>

<span data-ttu-id="23e56-122">[![IndexAddView](adding-a-view/_static/image2.png "IndexAddView")](adding-a-view/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="23e56-122">[![IndexAddView](adding-a-view/_static/image2.png "IndexAddView")](adding-a-view/_static/image1.png)</span></span>

<span data-ttu-id="23e56-123">**뷰 추가** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-123">The **Add View** dialog box appears.</span></span> <span data-ttu-id="23e56-124">기본 항목을 두고 클릭는 **추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-124">Leave the default entries and click the **Add** button.</span></span>

<span data-ttu-id="23e56-125">[![3addView](adding-a-view/_static/image4.png "3addView")](adding-a-view/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="23e56-125">[![3addView](adding-a-view/_static/image4.png "3addView")](adding-a-view/_static/image3.png)</span></span>

<span data-ttu-id="23e56-126">*MvcMovie\Views\HelloWorld* 폴더 및 *MvcMovie\Views\HelloWorld\Index.vbhtml* 파일이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-126">The *MvcMovie\Views\HelloWorld* folder and the *MvcMovie\Views\HelloWorld\Index.vbhtml* file are created.</span></span> <span data-ttu-id="23e56-127">한꺼번에 보일 **솔루션 탐색기**:</span><span class="sxs-lookup"><span data-stu-id="23e56-127">You can see them in **Solution Explorer**:</span></span>

<span data-ttu-id="23e56-128">[![SolnExpHelloWorldIndx](adding-a-view/_static/image6.png "SolnExpHelloWorldIndx")](adding-a-view/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="23e56-128">[![SolnExpHelloWorldIndx](adding-a-view/_static/image6.png "SolnExpHelloWorldIndx")](adding-a-view/_static/image5.png)</span></span>

<span data-ttu-id="23e56-129">일부 HTML에서 추가 된 `<h2>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-129">Add some HTML under the `<h2>` tag.</span></span> <span data-ttu-id="23e56-130">수정 된 *MvcMovie\Views\HelloWorld\Index.vbhtml* 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-130">The modified *MvcMovie\Views\HelloWorld\Index.vbhtml* file is shown below.</span></span>

[!code-vbhtml[Main](adding-a-view/samples/sample2.vbhtml)]

<span data-ttu-id="23e56-131">응용 프로그램을 실행 하 고를 찾습니다는 &quot;hello world&quot; 컨트롤러 (`http://localhost:xxxx/HelloWorld`).</span><span class="sxs-lookup"><span data-stu-id="23e56-131">Run the application and browse to the &quot;hello world&quot; controller (`http://localhost:xxxx/HelloWorld`).</span></span> <span data-ttu-id="23e56-132">`Index` 메서드 컨트롤러에서 많은 작업을 수행 하지 않으면 문은 단순히 실행 `return View()`는 표시 된 보기 템플릿 파일을 사용 하 여 클라이언트에 대 한 응답을 렌더링 하 려 합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-132">The `Index` method in your controller didn't do much work; it simply ran the statement `return View()`, which indicated that we wanted to use a view template file to render a response to the client.</span></span> <span data-ttu-id="23e56-133">ASP.NET MVC를 사용 하 여 기본값으로 사용할 보기 템플릿 파일의 이름, 명시적으로 지정 되지 않았기 때문는 *Index.vbhtml* 파일 내에서 보기는 *\Views\HelloWorld* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-133">Because we did not explicitly specify the name of the view template file to use, ASP.NET MVC defaulted to using the *Index.vbhtml* view file within the *\Views\HelloWorld* folder.</span></span> <span data-ttu-id="23e56-134">아래 이미지 보기에 하드 코드 된 문자열을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-134">The image below shows the string hard-coded in the view.</span></span>

<span data-ttu-id="23e56-135">[![3HelloWorld](adding-a-view/_static/image8.png "3HelloWorld")](adding-a-view/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="23e56-135">[![3HelloWorld](adding-a-view/_static/image8.png "3HelloWorld")](adding-a-view/_static/image7.png)</span></span>

<span data-ttu-id="23e56-136">잘 보입니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-136">Looks pretty good.</span></span> <span data-ttu-id="23e56-137">그러나 브라우저의 제목 표시줄에 표시 하는 것을 알 &quot;인덱스&quot; 페이지에서 큰 제목을 얘기 &quot;내 MVC 응용 프로그램입니다.&quot; 이러한 변경 해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-137">However, notice that the browser's title bar says &quot;Index&quot; and the big title on the page says &quot;My MVC Application.&quot; Let's change those.</span></span>

## <a name="changing-views-and-layout-pages"></a><span data-ttu-id="23e56-138">보기 및 레이아웃 페이지 변경</span><span class="sxs-lookup"><span data-stu-id="23e56-138">Changing views and layout pages</span></span>

<span data-ttu-id="23e56-139">첫째, 텍스트를 변경해 보겠습니다 &quot;내 MVC 응용 프로그램입니다.&quot; 해당 텍스트를 공유 하 고 모든 페이지에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-139">First, let's change the text &quot;My MVC Application.&quot; That text is shared and appears on every page.</span></span> <span data-ttu-id="23e56-140">것에 실제로 표시 한 위치는 프로젝트에만 응용 프로그램의 모든 페이지에는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-140">It actually appears in only one place in our project, even though it's on every page in our application.</span></span> <span data-ttu-id="23e56-141">이동 하는 */뷰/공유* 폴더에 **솔루션 탐색기** 엽니다는  *\_Layout.vbhtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-141">Go to the */Views/Shared* folder in **Solution Explorer** and open the *\_Layout.vbhtml* file.</span></span> <span data-ttu-id="23e56-142">이 파일은 레이아웃 페이지 라고 이며 공유 &quot;셸&quot; 다른 모든 페이지를 사용 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-142">This file is called a layout page and it's the shared &quot;shell&quot; that all other pages use.</span></span>

<span data-ttu-id="23e56-143">참고는 `@RenderBody()` 파일의 아래쪽에 있는 코드 줄을 합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-143">Note the `@RenderBody()` line of code near the bottom of the file.</span></span> <span data-ttu-id="23e56-144">`RenderBody` 여기서 만드는 모든 페이지 표시, 자리 표시자 &quot;래핑된&quot; 레이아웃 페이지에서.</span><span class="sxs-lookup"><span data-stu-id="23e56-144">`RenderBody` is a placeholder where all the pages you create show up, &quot;wrapped&quot; in the layout page.</span></span> <span data-ttu-id="23e56-145">변경 된 `<h1>` 에서 머리글 **&quot;** 내 MVC 응용 프로그램&quot; 를 &quot;MVC 만든 동영상 앱&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-145">Change the `<h1>` heading from **&quot;** My MVC Application&quot; to &quot;MVC Movie App&quot;.</span></span>

[!code-html[Main](adding-a-view/samples/sample3.html)]

<span data-ttu-id="23e56-146">응용 프로그램을 실행 하 고 이제 표시 참고 &quot;MVC 만든 동영상 앱&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-146">Run the application and note it now says &quot;MVC Movie App&quot;.</span></span> <span data-ttu-id="23e56-147">클릭는 **에 대 한** 링크를 지정 하 고 있는 페이지 표시 &quot;MVC 만든 동영상 앱&quot;도 합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-147">Click the **About** link, and that page shows &quot;MVC Movie App&quot;, too.</span></span>

<span data-ttu-id="23e56-148">전체  *\_Layout.vbhtml* 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-148">The complete *\_Layout.vbhtml* file is shown below:</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

<span data-ttu-id="23e56-149">이제 인덱스 페이지 (뷰)의 제목을 변경 해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-149">Now, let's change the title of the Index page (view).</span></span>

[!code-vbhtml[Main](adding-a-view/samples/sample5.vbhtml)]

<span data-ttu-id="23e56-150">Open *MvcMovie\Views\HelloWorld\Index.vbhtml*.</span><span class="sxs-lookup"><span data-stu-id="23e56-150">Open *MvcMovie\Views\HelloWorld\Index.vbhtml*.</span></span> <span data-ttu-id="23e56-151">변경 하는 두 곳: 먼저 텍스트 표시 되는 브라우저의 제목에 찾은 다음 보조 헤더에서 (의 `<h2>` 요소).</span><span class="sxs-lookup"><span data-stu-id="23e56-151">There are two places to make a change: first, the text that appears in the title of the browser, and then in the secondary header (the `<h2>` element).</span></span> <span data-ttu-id="23e56-152">म 수 있도록 약간 다른는 약간의 코드 변경 응용 프로그램의 어느 부분을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-152">We'll make them slightly different so you can see which bit of code changes which part of the app.</span></span>

<span data-ttu-id="23e56-153">응용 프로그램을 실행 하 고 찾아보기`http://localhost:xx/HelloWorld`합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-153">Run the application and browse to`http://localhost:xx/HelloWorld`.</span></span> <span data-ttu-id="23e56-154">브라우저 제목, 기본 제목 및 작은 제목이 변경된 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-154">Notice that the browser title, the primary heading, and the secondary headings have changed.</span></span> <span data-ttu-id="23e56-155">크게 변경 약간 변경 된 응용 프로그램에서 보기에 두는 것이 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-155">It's easy to make big changes in your application with small changes to a view.</span></span> <span data-ttu-id="23e56-156">(브라우저에서 변경 내용을 확인할 수 없는 경우 캐시된 콘텐츠를 보고 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-156">(If you don't see changes in the browser, you might be viewing cached content.</span></span> <span data-ttu-id="23e56-157">브라우저에서 Ctrl+F5 키를 눌러 로드될 서버에서 응답을 강제로 적용합니다.)</span><span class="sxs-lookup"><span data-stu-id="23e56-157">Press Ctrl+F5 in your browser to force the response from the server to be loaded.)</span></span>

<span data-ttu-id="23e56-158">[![3_MyMovieList](adding-a-view/_static/image10.png "3_MyMovieList")](adding-a-view/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="23e56-158">[![3_MyMovieList](adding-a-view/_static/image10.png "3_MyMovieList")](adding-a-view/_static/image9.png)</span></span>

<span data-ttu-id="23e56-159">우리의 약간의 &quot;데이터&quot; (이 경우에 &quot;Hello World!&quot; 메시지) 하지만 하드 코드 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-159">Our little bit of &quot;data&quot; (in this case the &quot;Hello World!&quot; message) is hard-coded, though.</span></span> <span data-ttu-id="23e56-160">MVC 응용 프로그램 (views) V 있으며 C (컨트롤러) 하지만 없는 M (모델) 아직 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-160">Our MVC application has V (views) and we've got C (controllers), but no M (model) yet.</span></span> <span data-ttu-id="23e56-161">곧 살펴봅니다 방법 데이터베이스를 만들고 여기에서 모델 데이터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-161">Shortly, we'll walk through how create a database and retrieve model data from it.</span></span>

## <a name="passing-data-from-the-controller-to-the-view"></a><span data-ttu-id="23e56-162">컨트롤러에서 보기로 데이터 전달</span><span class="sxs-lookup"><span data-stu-id="23e56-162">Passing Data from the Controller to the View</span></span>

<span data-ttu-id="23e56-163">데이터베이스를 이동 하 고 모델에 대해 설명 하는, 하지만 먼저에 대해 살펴보기 보기에는 컨트롤러에서 정보를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-163">Before we go to a database and talk about models, though, let's first talk about passing information from the Controller to a View.</span></span> <span data-ttu-id="23e56-164">클라이언트에 대 한 HTML 응답을 렌더링 하는 데 필요한 내용을 보기 서식 파일을 전달 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-164">We want to pass what a view template requires in order to render an HTML response to a client.</span></span> <span data-ttu-id="23e56-165">데이터 보기 템플릿에 필요를 포함 해야 하 고 이러한 개체는 일반적으로 만들어지고 보기 서식 파일을 컨트롤러 클래스에 의해 전달-및 더 이상 없습니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-165">These objects are typically created and passed by a controller class to a view template, and they should contain only the data that the view template requires — and no more.</span></span>

<span data-ttu-id="23e56-166">이전에 `HelloWorldController` 클래스는 `Welcome` 동작 메서드가 걸린는 `name` 및 `numTimes` 매개 변수 및 매개 변수 값은 브라우저에 다음 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-166">Previously with the `HelloWorldController` class, the `Welcome` action method took a `name` and a `numTimes` parameter and then output the parameter values to the browser.</span></span> <span data-ttu-id="23e56-167">이 응답을 직접 렌더링 하 계속 컨트롤러가 보겠습니다 대신 합니다 살펴보는 대신 해당 데이터 봉투에는 보기에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-167">Rather than have the controller continue to render this response directly, let's instead we'll put that data in a bag for the View.</span></span> <span data-ttu-id="23e56-168">컨트롤러와 뷰를 사용할 수는 `ViewBag` 해당 데이터를 보유 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-168">Controllers and Views can use a `ViewBag` object to hold that data.</span></span> <span data-ttu-id="23e56-169">자동으로 템플릿 보기를 통해 전달 되며 데이터로 모음의 내용을 사용 하 여 HTML 응답을 렌더링 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-169">That will be passed over to a view template automatically, and used to render the HTML response using the contents of the bag as data.</span></span> <span data-ttu-id="23e56-170">이런 방식으로 한 가지 및 다른 뷰 템플릿을 사용 하 여 컨트롤러 우려-유지 관리 정리를 &quot;문제의 분리&quot; 응용 프로그램 내에서.</span><span class="sxs-lookup"><span data-stu-id="23e56-170">That way the controller is concerned with one thing and the view template with another — enabling us to maintain clean &quot;separation of concerns&quot; within the application.</span></span>

<span data-ttu-id="23e56-171">또는 우리 수는 사용자 지정 클래스를 정의 다음 자체에서 해당 개체의 인스턴스를 만듭니다, 그리고 데이터로 채울 및 보기에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-171">Alternatively, we could define a custom class, then create an instance of that object on our own, fill it with data and pass it to the View.</span></span> <span data-ttu-id="23e56-172">일반적 라고는 ViewModel 뷰에 대 한 사용자 지정 모델 이므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-172">That is often called a ViewModel, because it's a custom Model for the View.</span></span> <span data-ttu-id="23e56-173">그러나 적은 양의 데이터를 ViewBag는 매우 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-173">For small amounts of data, however, the ViewBag works great.</span></span>

<span data-ttu-id="23e56-174">돌아가서는 *HelloWorldController.vb* 파일이 변경 된 `Welcome` ViewBag 메시지와 NumTimes 모드로 컨트롤러 내에서 메서드.</span><span class="sxs-lookup"><span data-stu-id="23e56-174">Return to the *HelloWorldController.vb* file change the `Welcome` method inside the controller to put the Message and NumTimes into the ViewBag.</span></span> <span data-ttu-id="23e56-175">ViewBag 동적 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-175">The ViewBag is a dynamic object.</span></span> <span data-ttu-id="23e56-176">즉,에 원하는 것을 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-176">That means you can put whatever you want in to it.</span></span> <span data-ttu-id="23e56-177">ViewBag에 내부 요소를 넣으면 될 때까지 정의 된 속성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-177">The ViewBag has no defined properties until you put something inside it.</span></span>

<span data-ttu-id="23e56-178">전체 `HelloWorldController.vb` 를 같은 파일에서 새 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-178">The complete `HelloWorldController.vb` with the new class in the same file.</span></span>

[!code-vb[Main](adding-a-view/samples/sample6.vb)]

<span data-ttu-id="23e56-179">이제 우리 ViewBag 전달 되는는 보기를 자동으로 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-179">Now our ViewBag contains data that will be passed over to the View automatically.</span></span> <span data-ttu-id="23e56-180">다시, 또는 우리 수 경과한 다음과 같은 고유한 개체에 빴 म 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="23e56-180">Again, alternatively we could have passed in our own object like this if we liked:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample7.cs)]

<span data-ttu-id="23e56-181">필요한 이제는 `WelcomeView` 템플릿을!</span><span class="sxs-lookup"><span data-stu-id="23e56-181">Now we need a `WelcomeView` template!</span></span> <span data-ttu-id="23e56-182">새 코드를 컴파일하는 하므로 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-182">Run the application so the new code is compiled.</span></span> <span data-ttu-id="23e56-183">브라우저를 닫고, 마우스 오른쪽 단추로 클릭는 `Welcome` 메서드와 클릭 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-183">Close the browser, right-click inside the `Welcome` method, and then click **Add View**.</span></span>

<span data-ttu-id="23e56-184">다음은 무엇 프로그램 **뷰 추가** 같은 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-184">Here's what your **Add View** dialog box looks like.</span></span>

<span data-ttu-id="23e56-185">[![3AddWelcomeView](adding-a-view/_static/image12.png "3AddWelcomeView")](adding-a-view/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="23e56-185">[![3AddWelcomeView](adding-a-view/_static/image12.png "3AddWelcomeView")](adding-a-view/_static/image11.png)</span></span>

<span data-ttu-id="23e56-186">아래에 다음 코드를 추가 `<h2>` 새로운 요소 <em>시작.</em> vbhtml 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-186">Add the following code under the `<h2>` element in the new <em>Welcome.</em>vbhtml file.</span></span> <span data-ttu-id="23e56-187">예를 들어 알아보고 루프 확인 하겠습니다 &quot;Hello&quot; 사용자가 중요 횟수 만큼!</span><span class="sxs-lookup"><span data-stu-id="23e56-187">We'll make a loop and say &quot;Hello&quot; as many times as the user says we should!</span></span>

[!code-vbhtml[Main](adding-a-view/samples/sample8.vbhtml)]

<span data-ttu-id="23e56-188">응용 프로그램을 실행 하 고 찾아보기 `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`</span><span class="sxs-lookup"><span data-stu-id="23e56-188">Run the application and browse to `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`</span></span>

<span data-ttu-id="23e56-189">이제 데이터 URL에서 수행 되 고 컨트롤러에 자동으로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-189">Now data is taken from the URL and passed to the controller automatically.</span></span> <span data-ttu-id="23e56-190">컨트롤러에 대 한 데이터를 패키지 한 `Model` 개체 및 보기에 해당 개체를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-190">The controller packages up the data into a `Model` object and passes that object to the view.</span></span> <span data-ttu-id="23e56-191">사용자에 게 데이터를 HTML로 표시 하는 보다 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-191">The view than displays the data as HTML to the user.</span></span>

<span data-ttu-id="23e56-192">[![3Hello_Scott_4](adding-a-view/_static/image14.png "3Hello_Scott_4")](adding-a-view/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="23e56-192">[![3Hello_Scott_4](adding-a-view/_static/image14.png "3Hello_Scott_4")](adding-a-view/_static/image13.png)</span></span>

<span data-ttu-id="23e56-193">하 한 종류의는 &quot;M&quot; 모델을 제외한 데이터베이스 종류 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-193">Well, that was a kind of an &quot;M&quot; for model, but not the database kind.</span></span> <span data-ttu-id="23e56-194">지금까지 학습한 것을 살펴보고 동영상의 데이터베이스를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="23e56-194">Let's take what we've learned and create a database of movies.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="23e56-195">[이전](adding-a-controller.md)
> [다음](adding-a-model.md)</span><span class="sxs-lookup"><span data-stu-id="23e56-195">[Previous](adding-a-controller.md)
[Next](adding-a-model.md)</span></span>
