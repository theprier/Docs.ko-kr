---
uid: mvc/overview/views/using-page-inspector-in-aspnet-mvc
title: ASP.NET MVC에서 페이지 검사기 사용 | Microsoft Docs
author: rick-anderson
description: Visual Studio 2012에서 페이지 검사기는 통합 된 브라우저를 사용 하 여 웹 개발 도구입니다. 통합 된 브라우저 및 페이지 검사기 i 요소를 선택 하는 중...
ms.author: aspnetcontent
ms.date: 08/15/2012
ms.assetid: c7e4e1ab-4932-4614-9f53-aaf7c706d498
msc.legacyurl: /mvc/overview/views/using-page-inspector-in-aspnet-mvc
msc.type: authoredcontent
ms.openlocfilehash: e3a6b79811cae15ec69ba3c5babe38b117b697a5
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37806088"
---
<a name="using-page-inspector-in-aspnet-mvc"></a><span data-ttu-id="fa836-104">ASP.NET MVC에서 페이지 검사기 사용</span><span class="sxs-lookup"><span data-stu-id="fa836-104">Using Page Inspector in ASP.NET MVC</span></span>
====================
<span data-ttu-id="fa836-105">Tim Ammann 여</span><span class="sxs-lookup"><span data-stu-id="fa836-105">by Tim Ammann</span></span>

> <span data-ttu-id="fa836-106">Visual Studio 2012에서 페이지 검사기는 통합 된 브라우저를 사용 하 여 웹 개발 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-106">Page Inspector in Visual Studio 2012 is a web development tool with an integrated browser.</span></span> <span data-ttu-id="fa836-107">통합 된 브라우저에서 모든 요소를 선택 하 고 요소의 소스 및 CSS 페이지 검사기를 즉시 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-107">Select any element in the integrated browser, and Page Inspector instantly highlights the element's source and CSS.</span></span> <span data-ttu-id="fa836-108">MVC 보기 찾아보기, 신속 하 게 렌더링 된 태그의 원본을 살펴봅니다를 Visual Studio 환경 내에서 바로 브라우저 도구를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-108">You can browse any MVC view, quickly find the sources of rendered markup, and use browser tools right within the Visual Studio environment.</span></span>
> 
> [<span data-ttu-id="fa836-109">비디오를 시청 하세요.</span><span class="sxs-lookup"><span data-stu-id="fa836-109">Watch the Video</span></span>](../../videos/mvc-4/using-page-inspector-in-aspnet-mvc.md)
> 
> <span data-ttu-id="fa836-110">이 자습서에서는 검사 모드를 활성화 한 후 신속 하 게 찾아 웹 프로젝트 내에서 태그와 CSS를 편집 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-110">This tutorial shows how to enable Inspection Mode, and then quickly locate and edit markup and CSS within your web project.</span></span> <span data-ttu-id="fa836-111">이 자습서에서는 MVC 프로젝트를 사용 하지만 용 페이지 검사기를 사용할 수도 있습니다 [Web Forms](https://go.microsoft.com/?linkid=9802001) 및 다른 ASP.NET 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-111">The tutorial uses an MVC Project, but you can also use Page Inspector for [Web Forms](https://go.microsoft.com/?linkid=9802001) and other ASP.NET applications.</span></span>
> 
> <span data-ttu-id="fa836-112">이 자습서에는 다음 섹션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-112">The tutorial has the following sections:</span></span>
> 
> - [<span data-ttu-id="fa836-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fa836-113">Prerequisites</span></span>](#_1_prerequisites)
> - [<span data-ttu-id="fa836-114">웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="fa836-114">Create a Web Application</span></span>](#_2_creating_a)
> - [<span data-ttu-id="fa836-115">뷰를 탐색 페이지 검사기 사용</span><span class="sxs-lookup"><span data-stu-id="fa836-115">Use Page Inspector to Browse to a View</span></span>](#_3_using_page)
> - [<span data-ttu-id="fa836-116">검사 모드를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="fa836-116">Enable Inspection Mode</span></span>](#_4_inspection_mode)
> - [<span data-ttu-id="fa836-117">페이지 검사기를 사용 하 여 태그를 변경 하려면</span><span class="sxs-lookup"><span data-stu-id="fa836-117">Use Page Inspector to Make Changes to Markup</span></span>](#_5_using_page)
> - [<span data-ttu-id="fa836-118">HTML 창과 검사 모드</span><span class="sxs-lookup"><span data-stu-id="fa836-118">Inspection Mode and the HTML Window</span></span>](#_6_inspection_mode)
> - [<span data-ttu-id="fa836-119">스타일 창에서 CSS 변경 내용 미리 보기</span><span class="sxs-lookup"><span data-stu-id="fa836-119">Preview CSS Changes in the Styles window</span></span>](#_7_previewing_css)
> - [<span data-ttu-id="fa836-120">CSS 자동 동기화</span><span class="sxs-lookup"><span data-stu-id="fa836-120">CSS Auto Sync</span></span>](#css_auto_sync)
> - [<span data-ttu-id="fa836-121">CSS 색 선택을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="fa836-121">Using the CSS Color Picker</span></span>](#css_color_picker)
> - [<span data-ttu-id="fa836-122">동적 페이지 요소를 JavaScript에 매핑</span><span class="sxs-lookup"><span data-stu-id="fa836-122">Mapping Dynamic Page Elements to JavaScript</span></span>](#map_dynamic_elements)


<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="fa836-123">전제 조건</span><span class="sxs-lookup"><span data-stu-id="fa836-123">Prerequisites</span></span>

- <span data-ttu-id="fa836-124">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11) 나 [Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-124">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11) or [Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span>

> [!NOTE]
> <span data-ttu-id="fa836-125">페이지 검사기의 최신 버전을 사용 [웹 플랫폼 설치 관리자](https://go.microsoft.com/fwlink/?LinkId=255386) .NET 2.0에 대 한 Windows Azure SDK를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-125">To get the latest version of Page Inspector, use [Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386) to install the Windows Azure SDK for .NET 2.0.</span></span>


<span data-ttu-id="fa836-126">페이지 검사기는 Microsoft Web 개발자 도구를 사용 하 여 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-126">Page Inspector is bundled with Microsoft Web Developer Tools.</span></span> <span data-ttu-id="fa836-127">최신 버전 1.3입니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-127">The latest version is 1.3.</span></span> <span data-ttu-id="fa836-128">어떤 버전을 확인 하려면, Visual Studio를 실행 있고 선택 **Microsoft Visual Studio 정보** 에서 합니다 **도움말** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="fa836-128">To check which version you have, run Visual Studio and select **About Microsoft Visual Studio** from the **Help** menu.</span></span>

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a><span data-ttu-id="fa836-129">웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="fa836-129">Create a Web Application</span></span>

<span data-ttu-id="fa836-130">먼저 사용 하 여 페이지 검사기 사용 하 여 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-130">First, create a web application that you will use Page Inspector with.</span></span> <span data-ttu-id="fa836-131">Visual Studio에서 선택 **파일** &gt; **새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-131">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="fa836-132">왼쪽의 확장 **Visual C#** 를 선택 **웹**를 선택한 후 **ASP.NET MVC4 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-132">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET MVC4 Web Application**.</span></span>

![새 ASP.NET MVC 응용 프로그램](using-page-inspector-in-aspnet-mvc/_static/image2.png)

<span data-ttu-id="fa836-134">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-134">Click **OK**.</span></span>

<span data-ttu-id="fa836-135">에 **새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **인터넷 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-135">In the **New ASP.NET MVC 4 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="fa836-136">둡니다 **Razor** 기본 뷰 엔진으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-136">Leave **Razor** as the default view engine.</span></span>

![새 ASP.NET MVC 프로젝트-인터넷 응용 프로그램](using-page-inspector-in-aspnet-mvc/_static/image4.png)

<span data-ttu-id="fa836-138">응용 프로그램에서 엽니다 **원본** 보기.</span><span class="sxs-lookup"><span data-stu-id="fa836-138">The application opens in **Source** view.</span></span>

![소스 뷰에서 새 ASP.NET MVC 응용 프로그램](using-page-inspector-in-aspnet-mvc/_static/image6.png)

<span data-ttu-id="fa836-140">응용 프로그램 사용을 설정 했으므로 점검 하 여 수정 페이지 검사기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-140">Now that you have an application to work with, you can use Page Inspector to examine and modify it.</span></span>

<a id="_starting_page_inspector"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-browse-to-a-view"></a><span data-ttu-id="fa836-141">뷰를 탐색 페이지 검사기 사용</span><span class="sxs-lookup"><span data-stu-id="fa836-141">Use Page Inspector to Browse to a View</span></span>

<span data-ttu-id="fa836-142">Visual Studio 2012에서 단추로 보기에서 프로젝트를 선택 **페이지 검사기에서 보기**, 페이지 검사기는 경로 파악 하 고 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-142">In Visual Studio 2012, you can right-click any view in your project, select **View in Page Inspector**, and Page Inspector will figure out the route and display the page.</span></span>

<span data-ttu-id="fa836-143">**솔루션 탐색기**를 확장 합니다 **뷰** 폴더 차례로 **홈** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-143">In **Solution Explorer**, expand the **Views** folder and then the **Home** folder.</span></span> <span data-ttu-id="fa836-144">Index.cshtml 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 **페이지 검사기에서 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-144">Right click the Index.cshtml file and choose **View in Page Inspector**.</span></span>

![페이지 검사기에서 보기 Index.cshtml](using-page-inspector-in-aspnet-mvc/_static/image8.png)

<span data-ttu-id="fa836-146">기본적으로 Visual Studio 환경의 왼쪽에서 페이지 검사기 창으로 도킹 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-146">By default, Page Inspector is docked as a window on the left side of the Visual Studio environment.</span></span> <span data-ttu-id="fa836-147">원하는 경우 다른 곳에서 도킹 하거나 창의 도킹을 해제 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-147">If you prefer, you can dock it elsewhere, or undock the window.</span></span> <span data-ttu-id="fa836-148">참조 [방법: 정렬 및 도킹 Windows](https://msdn.microsoft.com/library/z4y0hsax.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-148">See [How to: Arrange and Dock Windows](https://msdn.microsoft.com/library/z4y0hsax.aspx).</span></span>

<span data-ttu-id="fa836-149">페이지 검사기 창 상단의 브라우저 창에서 현재 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-149">The top pane of the Page Inspector window shows the current page in a browser window.</span></span> <span data-ttu-id="fa836-150">아래쪽 창의 페이지의 다양 한 측면을 검사할 수 있도록 탭도 함께 HTML 태그에서 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-150">The bottom pane shows the page in HTML markup, along with some tabs that let you inspect different aspects of the page.</span></span> <span data-ttu-id="fa836-151">아래쪽 창은 비슷합니다는 [F12 개발자 도구](https://msdn.microsoft.com/ie/aa740478) Internet Explorer에서.</span><span class="sxs-lookup"><span data-stu-id="fa836-151">The bottom pane is similar to the [F12 Developer Tools](https://msdn.microsoft.com/ie/aa740478) in Internet Explorer.</span></span>

![페이지 검사기에서 ASP.NET MVC 응용 프로그램](using-page-inspector-in-aspnet-mvc/_static/image10.png)

<span data-ttu-id="fa836-153">이 자습서에서는 사용 하 여는 **HTML** 하 고 **스타일** 신속 하 게 이동 하 고 응용 프로그램을 변경 하는 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-153">In this tutorial, you will use the **HTML** and **Styles** tabs to navigate quickly and make changes to the application.</span></span>

<a id="_examining_(&quot;decomposing&quot;)_the"></a><a id="_inspection_mode_and"></a><a id="_4_inspection_mode"></a>

## <a name="enableinspection-mode"></a><span data-ttu-id="fa836-154">EnableInspection 모드</span><span class="sxs-lookup"><span data-stu-id="fa836-154">EnableInspection Mode</span></span>

<span data-ttu-id="fa836-155">페이지 검사기를 검사 모드에 두려면를 클릭 합니다 **검사** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-155">To put Page Inspector into Inspection Mode, click the **Inspect** button.</span></span> <span data-ttu-id="fa836-156">검사 모드에서 렌더링된 된 페이지 부분 위로 마우스 포인터를 가져가면 해당 소스 태그나 코드가 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-156">In Inspection Mode, when you hold the mouse pointer over any part of the rendered page, the corresponding source markup or code is highlighted.</span></span>

![검사 모드 설정/해제](using-page-inspector-in-aspnet-mvc/_static/image12.png)

<span data-ttu-id="fa836-158">이제 페이지 검사기 내에서 페이지의 다른 부분 위로 마우스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-158">Now move your mouse over different parts of the page within Page Inspector.</span></span> <span data-ttu-id="fa836-159">마찬가지로, 마우스 포인터 큰 더하기 기호를으로 변경 되 고 아래에 있는 요소가 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-159">As you do, the mouse pointer changes to a large plus sign, and the element underneath is highlighted:</span></span>

![Div.content 래퍼를 가리키면](using-page-inspector-in-aspnet-mvc/_static/image14.png)

<span data-ttu-id="fa836-161">마우스 포인터를 이동 하면 Visual Studio에는 소스 파일의 해당 Razor 구문 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-161">As you move the mouse pointer, Visual Studio highlights the corresponding Razor syntax in the source file.</span></span> <span data-ttu-id="fa836-162">다른 소스 파일에서 HTML 요소 상태가 되 면 Visual Studio는 자동으로 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-162">If the HTML element comes from another source file, Visual Studio automatically opens the file.</span></span>

<span data-ttu-id="fa836-163">페이지 검사기에는 **HTML** 탭 Razor 구문에서 생성 된 HTML을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-163">In Page Inspector, the **HTML** tab shows the HTML that was generated from the Razor syntax.</span></span> <span data-ttu-id="fa836-164">마우스 포인터를 이동 하면 HTML 요소를 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-164">As you move the mouse pointer, the HTML elements are highlighted.</span></span> <span data-ttu-id="fa836-165">합니다 **스타일** 탭 요소에 대 한 CSS 규칙을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-165">The **Styles** tab shows the CSS rules for the element.</span></span>

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a><span data-ttu-id="fa836-166">페이지 검사기를 사용 하 여 태그를 변경 하려면</span><span class="sxs-lookup"><span data-stu-id="fa836-166">Use Page Inspector to Make Changes to Markup</span></span>

<span data-ttu-id="fa836-167">페이지 검사기를 사용 하면 위치가 명확 하지 않을 태그를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-167">Page Inspector lets you find markup whose location might not be obvious.</span></span> <span data-ttu-id="fa836-168">다음 태그를 수정 하 고 결과 변경 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-168">Then you can modify the markup and see the resulting changes.</span></span>

<span data-ttu-id="fa836-169">이 확인 하려면 클릭 **검사** 페이지 검사기 창의 페이지의 아래쪽으로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-169">To see this, click **Inspect** and then scroll to the bottom of the page in the Page Inspector window.</span></span>

<span data-ttu-id="fa836-170">영역의 바닥글 부분에 마우스 포인터를 이동 하는 경우 페이지 검사기 열립니다는 \_Layout.cshtml 파일 선택한 레이아웃 페이지의 섹션을 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-170">When you move the mouse pointer into the footer area, Page Inspector opens the \_Layout.cshtml file and highlights the section of the layout page that you have selected.</span></span> <span data-ttu-id="fa836-171">알 수 있듯이 바닥글은 레이아웃 파일 뷰 자체에 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-171">As you can see, the footer are is defined in the layout file, and not the view itself.</span></span>

![바닥글](using-page-inspector-in-aspnet-mvc/_static/image16.png)

<span data-ttu-id="fa836-173">이제 저작권 정보를 사용 하 여 선 위로 마우스 포인터를 이동 <a id="a"> </a>알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-173">Now move your mouse pointer over the line with the copyright <a id="a"></a>notice.</span></span> <span data-ttu-id="fa836-174">에 \_Layout.cshtml 페이지에서 해당 줄이 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-174">In the \_Layout.cshtml page, the corresponding line is highlighted.</span></span>

![바닥글 저작권 줄 강조 표시](using-page-inspector-in-aspnet-mvc/_static/image18.png)

<span data-ttu-id="fa836-176">텍스트 줄의 끝에 추가 된 \_Layout.cshtml 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-176">Add some text to the end of the line in the \_Layout.cshtml file.</span></span>

<span data-ttu-id="fa836-177">&lt;p&gt;&amp;복사 합니다. @DateTime.Now.Year -내 ASP.NET MVC 응용 프로그램이 최고인!  &lt; /p&gt;</span><span class="sxs-lookup"><span data-stu-id="fa836-177">&lt;p&gt;&amp;copy; @DateTime.Now.Year - My ASP.NET MVC Application Rocks!&lt;/p&gt;</span></span>

<span data-ttu-id="fa836-178">이제 Ctrl + Alt + Enter를 누르거나 페이지 검사기 브라우저 창에서 결과 볼 수 업데이트 표시줄을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-178">Now, press Ctrl+Alt+Enter or click the Update Bar to see the results in the Page Inspector browser window.</span></span>

![내 ASP.NET 응용 프로그램 Rocks!](using-page-inspector-in-aspnet-mvc/_static/image20.png)

<span data-ttu-id="fa836-180">바닥글 Index.cshtml에서 정의 되지만 평범한 일에 생각을 \_Layout.cshtml, 및 페이지 검사기를 발견 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-180">You might have thought that the footer defined in Index.cshtml, but it turned out to be in the \_Layout.cshtml, and Page Inspector found it for you.</span></span>

<a id="_inspection_mode_and_1"></a><a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a><span data-ttu-id="fa836-181">HTML 창과 검사 모드</span><span class="sxs-lookup"><span data-stu-id="fa836-181">Inspection Mode and the HTML Window</span></span>

<span data-ttu-id="fa836-182">다음으로, HTML 창과 요소를 매핑되는 방법을 빠르게 확인을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-182">Next, you will have a quick look at the HTML window and how it maps elements for you.</span></span>

<span data-ttu-id="fa836-183">클릭 **검사** 를 검사 모드에서 페이지 검사기를 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-183">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="fa836-184">"Logohere" 라고 표시 되는 페이지의 위쪽을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-184">Click the top part of the page that says "Your logohere".</span></span> <span data-ttu-id="fa836-185">보다 세부적으로 마우스 포인터를 이동 하면 브라우저 창에 표시를 변경 하는 더 이상 특정 요소를 검사 하 고 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-185">You are examining a particular element in more detail, so the display in the browser window no longer changes as you move the mouse pointer.</span></span>

<span data-ttu-id="fa836-186">이제 마우스 포인터를 이동 합니다 **HTML** 창입니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-186">Now move the mouse pointer to the **HTML** window.</span></span> <span data-ttu-id="fa836-187">마우스 포인터를 이동 하면 페이지 검사기 내의 요소를 설명 합니다 **HTML** 창 고 브라우저 창에서 해당 요소를 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-187">As you move the mouse pointer, Page Inspector outlines the element within the **HTML** window and highlights the corresponding element in the browser window.</span></span>

![HTML 창](using-page-inspector-in-aspnet-mvc/_static/image22.png)

<span data-ttu-id="fa836-189">페이지 검사기가 열리면 이전에 \_임시 탭에서 Layout.cshtml 파일입니다. 클릭 합니다 \_Layout.cshtml 임시 탭 및 해당 태그에서 강조 표시 됩니다는 &lt;헤더&gt; 를 섹션:</span><span class="sxs-lookup"><span data-stu-id="fa836-189">As before, Page Inspector opens the \_Layout.cshtml file for you in a temporary tab. Click the \_Layout.cshtml temporary tab, and the corresponding markup will be highlighted in the &lt;header&gt; section for you:</span></span>

![강조 표시 된 태그](using-page-inspector-in-aspnet-mvc/_static/image24.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a><span data-ttu-id="fa836-191">스타일 창에서 CSS 변경 내용 미리 보기</span><span class="sxs-lookup"><span data-stu-id="fa836-191">Preview CSS Changes in the Styles Window</span></span>

<span data-ttu-id="fa836-192">다음으로, 페이지 검사기 사용할지 **스타일** css 변경 내용 미리 보기 창입니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-192">Next, you will use the Page Inspector **Styles** window to preview changes to CSS.</span></span>

<span data-ttu-id="fa836-193">클릭 **검사** 를 검사 모드에서 페이지 검사기를 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-193">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="fa836-194">페이지 검사기 브라우저 창에서 마우스 포인터를 이동 될 때까지 "홈 페이지" 섹션을 마우스로 합니다 **div.content 래퍼** 레이블이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-194">In the Page Inspector browser window, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span>

![Div.content 래퍼를 가리키면](using-page-inspector-in-aspnet-mvc/_static/image26.png)

<span data-ttu-id="fa836-196">Div.content 래퍼 섹션 내에서 한 번 클릭 하 고 다음으로 마우스 포인터를 이동 합니다 **스타일** 창입니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-196">Click within the div.content-wrapper section once, and then move the mouse pointer to the **Styles** window.</span></span> <span data-ttu-id="fa836-197">합니다 **스타일** 이 요소에 대 한 CSS 규칙의 모든 창을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-197">The **Syles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="fa836-198">찾기.featured.content 래퍼 클래스 선택기까지 아래로 스크롤하십시오.</span><span class="sxs-lookup"><span data-stu-id="fa836-198">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="fa836-199">이제 배경색 속성에 대 한 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-199">Now clear the checkbox for the background-color property.</span></span>

![투명 한 배경이 색](using-page-inspector-in-aspnet-mvc/_static/image28.png)

<span data-ttu-id="fa836-201">방법 변경 내용을 미리 봅니다. 즉시 페이지 검사기 브라우저 창에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-201">Notice how the change previews instantly in the Page Inspector browser window.</span></span>

<span data-ttu-id="fa836-202">다시 확인란을 선택 하, 속성 값을 두 번 클릭 및 빨강으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-202">Select the checkbox again, then double-click the property value and change it to red.</span></span> <span data-ttu-id="fa836-203">변경 내용을 즉시 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-203">The change shows immediately:</span></span>

![빨강 배경색.](using-page-inspector-in-aspnet-mvc/_static/image30.png)

<span data-ttu-id="fa836-205">합니다 **스타일** 스타일으로 변경 내용을 커밋하기 전에 변경 하는 쉽게 테스트 하 고 CSS를 미리 보기 창을 사용 하면 자체 시트입니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-205">The **Styles** window makes it easy to test and preview CSS changes before you commit the changes to the style sheet itself.</span></span>

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a><span data-ttu-id="fa836-206">CSS 자동 동기화</span><span class="sxs-lookup"><span data-stu-id="fa836-206">CSS Auto Sync</span></span>

> [!NOTE]
> <span data-ttu-id="fa836-207">이 기능은 페이지 검사기의 버전 1.3을 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-207">This feature requires version 1.3 of Page Inspector.</span></span>


<span data-ttu-id="fa836-208">CSS 자동 동기화 기능을 사용 하면 CSS 파일을 직접 편집 하 고 페이지 검사기 브라우저에서 즉시 변경 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-208">The CSS Auto-Sync feature allows you to edit a CSS file directly, and see the changes immediately in the Page Inspector browser.</span></span>

<span data-ttu-id="fa836-209">클릭 **검사** 를 검사 모드에서 페이지 검사기를 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-209">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="fa836-210">페이지 검사기 브라우저에서 "홈 페이지" 섹션까지 위로 마우스 포인터를 이동 합니다 **div.content 래퍼** 레이블이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-210">In the Page Inspector browser, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span> <span data-ttu-id="fa836-211">이 요소를 한 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-211">Click once to select this element.</span></span>

<span data-ttu-id="fa836-212">합니다 **스타일** 이 요소에 대 한 CSS 규칙의 모든 창을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-212">The **Syles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="fa836-213">찾기.featured.content 래퍼 클래스 선택기까지 아래로 스크롤하십시오.</span><span class="sxs-lookup"><span data-stu-id="fa836-213">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="fa836-214">".Featured.content-래퍼"를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-214">Click on ".featured .content-wrapper".</span></span> <span data-ttu-id="fa836-215">페이지 검사기 (Site.css)이이 스타일을 정의 하 고 해당 CSS 스타일을 강조 표시 하는 CSS 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-215">Page Inspector opens the CSS file that defines this style (Site.css) and highlights the corresponding CSS style.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image32.png)

<span data-ttu-id="fa836-216">이제 값을 변경 `background-color` "red"로 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-216">Now change the value for `background-color` to "red".</span></span> <span data-ttu-id="fa836-217">페이지 검사기 브라우저에 변경 내용을 즉시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-217">The change appears immediately in the Page Inspector browser.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image34.png)

<a id="css_color_picker"></a>
## <a name="using-the-css-color-picker"></a><span data-ttu-id="fa836-218">CSS 색 선택을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="fa836-218">Using the CSS Color Picker</span></span>

<span data-ttu-id="fa836-219">Visual Studio 2012에서 CSS 편집기에 쉽게 선택 하 고 색을 삽입 하는 색 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-219">The CSS editor in Visual Studio 2012 has a color picker that makes it easy to choose and insert colors.</span></span> <span data-ttu-id="fa836-220">색 선택 표준 색 팔레트가 포함 표준 색 이름, 해시 코드, RGB, RGBA, HSL 및 HSLA 색을 지원 하며 문서에서 가장 최근에 사용 했던 색 목록을 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-220">The color picker includes a standard palette of colors, supports standard color names, hash codes, RGB, RGBA, HSL, and HSLA colors, and maintains a list of the colors you've used most recently in the document.</span></span>

<span data-ttu-id="fa836-221">이전 섹션에서 값을 변경 하 여 `background-color` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-221">In the previous section, you changed the value of the `background-color` property.</span></span> <span data-ttu-id="fa836-222">색 선택기를 호출 하려면 속성 이름 및 형식을 후 삽입 포인터를 놓습니다 **#** 하거나 **rgb (** 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-222">To invoke the color picker, place the insertion point after the property name and type **#** or **rgb(**.</span></span>

![CSS 색 선택 막대](using-page-inspector-in-aspnet-mvc/_static/image36.png)

<span data-ttu-id="fa836-224">아래쪽 화살표 키를 누르거나 선택한 색을 클릭 하 고 왼쪽 및 오른쪽 화살표 키를 사용 하 여 색을 트래버스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-224">Click on a color to select it, or press the down arrow key and then use the left and right arrow keys to traverse the colors.</span></span> <span data-ttu-id="fa836-225">색을 방문 하면 해당 16 진수 값을 미리 보기:</span><span class="sxs-lookup"><span data-stu-id="fa836-225">When you visit a color, the corresponding hex value is previewed:</span></span>

![미리 보기 배경 색 속성 값](using-page-inspector-in-aspnet-mvc/_static/image38.png)

<span data-ttu-id="fa836-227">색 막대 없는 경우 원하는 정확한 색, 색 선택 팝업 목록을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-227">If the color bar doesn't have the exact color you want, you can use the color picker pop-down.</span></span> <span data-ttu-id="fa836-228">를 열려면 색 막대의 오른쪽 끝에서 이중 펼침 단추를 클릭 하거나 키보드의 아래쪽 화살표 또는 두 번 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-228">To open it, click the double chevron at the right end of the color bar, or press the Down Arrow once or twice on the keyboard.</span></span>

![CSS 색 선택 팝업 다운](using-page-inspector-in-aspnet-mvc/_static/image40.png)

<span data-ttu-id="fa836-230">오른쪽에 있는 세로 막대에서 색을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-230">Click a color from the vertical bar on the right.</span></span> <span data-ttu-id="fa836-231">주 창에서 해당 색 그라데이션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-231">This shows a gradient for that color in the main window.</span></span> <span data-ttu-id="fa836-232">Enter 키를 눌러 세로 막대에서 직접 색을 선택 하거나 더 높은 정밀도 사용 하 여 선택할 수 주 창의 시점을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-232">Choose a color directly from the vertical bar by pressing Enter, or click any point in the main window to choose with greater precision.</span></span>

<span data-ttu-id="fa836-233">사용 하려는 컴퓨터 화면에서 색을 있는지 (Visual Studio 사용자 인터페이스 내에 없는 함), 오른쪽 아래에 스 포 이트 도구를 사용 하 여 해당 값을 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-233">If there is a color on your computer screen that you want to use (it doesn't have to be inside the Visual Studio user interface), you can capture its value by using the eyedropper tool on the lower right.</span></span>

<span data-ttu-id="fa836-234">색 편집기의 맨 아래에서 슬라이더를 이동 하 여 색의 불투명도 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-234">You also can change the opacity of a color by moving the slider at the bottom of the color picker.</span></span> <span data-ttu-id="fa836-235">이렇게 하면 변경 내용을 색 값을 RGBA 값 RGBA 형식을 불투명도 나타낼 수 있으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-235">Doing so changes color values to RGBA values, because the RGBA format can represent opacity.</span></span>

<span data-ttu-id="fa836-236">색을 선택한 후 enter 키를 한 다음 배경색 항목을 완료 하려면 세미콜론을 입력 합니다 *Site.css* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-236">After you have chosen a color, press Enter, and then type a semicolon to complete the background-color entry in the *Site.css* file.</span></span>

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a><span data-ttu-id="fa836-237">페이지 검사기 업데이트 표시줄</span><span class="sxs-lookup"><span data-stu-id="fa836-237">The Page Inspector Update Bar</span></span>

<span data-ttu-id="fa836-238">페이지 검사기는 즉시 변경 감지 합니다 *Site.css* 파일과 업데이트 표시줄이에 경고를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-238">Page Inspector immediately detects the change to the *Site.css* file and displays an alert in an update bar.</span></span>

![업데이트 표시줄](using-page-inspector-in-aspnet-mvc/_static/image42.png)

<span data-ttu-id="fa836-240">모든 파일을 저장 하 고 페이지 검사기 브라우저 새로 고침을 Ctrl + Alt + Enter 누르거나 업데이트 표시줄을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-240">To save all your files and refresh the Page Inspector browser, press Ctrl+Alt+Enter or click the update bar.</span></span> <span data-ttu-id="fa836-241">강조 표시 색 변화는 브라우저에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-241">The change in the highlight color appears in the browser.</span></span>

<a id="map_dynamic_elements"></a>
## <a name="mapping-dynamic-page-elements-to-javascript"></a><span data-ttu-id="fa836-242">동적 페이지 요소를 JavaScript에 매핑</span><span class="sxs-lookup"><span data-stu-id="fa836-242">Mapping Dynamic Page Elements to JavaScript</span></span>

<span data-ttu-id="fa836-243">최신 웹 응용 프로그램에서 페이지의 요소는 JavaScript를 사용 하 여 동적으로 생성 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-243">In modern web applications, elements in the page are often generated dynamically with JavaScript.</span></span> <span data-ttu-id="fa836-244">즉, 이러한 페이지 요소에 해당 하는 없는 정적 태그 (HTML 또는 Razor).</span><span class="sxs-lookup"><span data-stu-id="fa836-244">That means there is no static markup (either HTML or Razor) that corresponds to these page elements.</span></span>

<span data-ttu-id="fa836-245">버전 1.3 사용 하 여 페이지 검사기에 페이지를 다시 해당 JavaScript 코드에 동적으로 추가 된 항목에 이제 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-245">With version 1.3, Page Inspector can now map items that were dynamically added to the page back to the corresponding JavaScript code.</span></span> <span data-ttu-id="fa836-246">이 기능을 보여 주기 위해 사용 합니다 [단일 페이지 응용 프로그램 (SPA) 템플릿](../../../single-page-application/overview/introduction/knockoutjs-template.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-246">To demonstrate this feature, we'll use the [Single Page Application (SPA) template](../../../single-page-application/overview/introduction/knockoutjs-template.md).</span></span>

> [!NOTE]
> <span data-ttu-id="fa836-247">SPA 템플릿에 필요 합니다 [ASP.NET 및 웹 도구 2012.2](https://go.microsoft.com/fwlink/?LinkId=282650) 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-247">The SPA template requires the [ASP.NET and Web Tools 2012.2](https://go.microsoft.com/fwlink/?LinkId=282650) update.</span></span>


<span data-ttu-id="fa836-248">Visual Studio에서 선택 **파일** &gt; **새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-248">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="fa836-249">왼쪽의 확장 **Visual C#** 를 선택 **웹**를 선택한 후 **ASP.NET MVC4 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-249">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET MVC4 Web Application**.</span></span> <span data-ttu-id="fa836-250">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-250">Click **OK**.</span></span>

<span data-ttu-id="fa836-251">에 **새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **단일 페이지 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-251">In the **New ASP.NET MVC 4 Project** dialog, select **Single Page Application**.</span></span>

<span data-ttu-id="fa836-252">솔루션 탐색기에서 확장을 **뷰** 폴더 차례로 합니다 **홈** 폴더.</span><span class="sxs-lookup"><span data-stu-id="fa836-252">In Solution Explorer, expand the **Views** folder and then the **Home** folder.</span></span> <span data-ttu-id="fa836-253">Index.cshtml 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 **페이지 검사기에서 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-253">Right click the Index.cshtml file and choose **View in Page Inspector**.</span></span>

<span data-ttu-id="fa836-254">페이지 검사기 브라우저에서이 먼저 표시 되는 로그인 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-254">The first thing that is displayed in the Page Inspector browser is a login page.</span></span> <span data-ttu-id="fa836-255">"등록"을 클릭 하 고 사용자 이름 및 암호를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-255">Click "Sign Up" and create a user name and password.</span></span> <span data-ttu-id="fa836-256">등록 하면 응용 프로그램 로그인 하 고 몇 가지 샘플 항목 할 일 목록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-256">Once you sign up, the application logs you in and creates a to-do list with some sample items.</span></span>

<span data-ttu-id="fa836-257">클릭 **검사** 를 검사 모드에서 페이지 검사기를 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-257">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span> <span data-ttu-id="fa836-258">페이지 검사기 브라우저에서 할 일 항목 중 하나를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-258">In the Page Inspector browser, click on one of the to-do items.</span></span> <span data-ttu-id="fa836-259">파란색으로 강조 표시 되는 대신 요소는 주황색으로 강조 표시, "JS"를 사용 하 여 요소 이름 옆에 있는 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-259">Notice that instead of being highlighted in blue, the element is highlighted in orange, with "JS" next to the element name.</span></span> <span data-ttu-id="fa836-260">이 스크립트를 통해 동적으로 요소 만들어졌음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-260">This indicates that the element was created dynamically through script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image44.png)

<span data-ttu-id="fa836-261">에 주황색 밑줄이 표시 되는 또한 합니다 **호출 스택** 탭 합니다. 이 나타내는 합니다 **호출 스택** 창에는 요소에 대 한 자세한 정보.</span><span class="sxs-lookup"><span data-stu-id="fa836-261">In addition, an orange underline appears on the **Call Stack** tab. This indicates that the **Call Stack** pane has more information about the element.</span></span>

<span data-ttu-id="fa836-262">클릭 합니다 **호출 스택** 탭 합니다. 합니다 **호출 스택** 요소를 만든 JavaScript 호출이 다소 어렵게 호출 스택 창에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-262">Click on the **Call Stack** tab. The **Call Stack** pane shows the call stack for the JavaScript call that created the element.</span></span> <span data-ttu-id="fa836-263">외부 라이브러리에 jQuery 축소 되어 있으면 같은 있도록 호출 응용 프로그램 스크립트에 대 한 호출을 쉽게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-263">Calls to external libraries such as jQuery are collapsed, so that you can easily see the calls to your application script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image46.png)

<span data-ttu-id="fa836-264">외부 라이브러리에 대 한 호출을 포함 하 여 전체 스택을 보려면 "외부 라이브러리" 이라는 노드를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-264">To see the full stack, including calls to external libraries, you can expand the nodes labeled "External Libraries":</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image48.png)

<span data-ttu-id="fa836-265">호출 스택의 항목을 클릭 하면 Visual Studio 코드 파일이 열리고 해당 스크립트를 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa836-265">If you click an item in the call stack, Visual Studio opens the code file and highlights the corresponding script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image50.png)

## <a name="see-also"></a><span data-ttu-id="fa836-266">참고 항목</span><span class="sxs-lookup"><span data-stu-id="fa836-266">See Also</span></span>

<span data-ttu-id="fa836-267">[Visual Studio를 사용 하 여 ASP.NET MVC 4 소개](../older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md) (ASP.net 웹 사이트)</span><span class="sxs-lookup"><span data-stu-id="fa836-267">[Intro to ASP.NET MVC 4 with Visual Studio](../older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md) (ASP.net website)</span></span>

<span data-ttu-id="fa836-268">[페이지 검사기 소개](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector/) (채널 9 비디오)</span><span class="sxs-lookup"><span data-stu-id="fa836-268">[Introducing Page Inspector](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector/) (Channel 9 video)</span></span>

<span data-ttu-id="fa836-269">[페이지 검사자 오류 메시지](https://go.microsoft.com/?linkid=9813062) (MSDN)</span><span class="sxs-lookup"><span data-stu-id="fa836-269">[Page Inspector Error Messages](https://go.microsoft.com/?linkid=9813062) (MSDN)</span></span>
