---
uid: mvc/overview/views/using-page-inspector-in-aspnet-mvc
title: "ASP.NET MVC에서 페이지 검사기를 사용 하 여 | Microsoft Docs"
author: rick-anderson
description: "Visual Studio 2012에서 페이지 검사기는 통합 된 브라우저와 웹 개발 도구입니다. 페이지 검사기 i 고 통합된 브라우저에서 모든 요소 선택..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/15/2012
ms.topic: article
ms.assetid: c7e4e1ab-4932-4614-9f53-aaf7c706d498
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/views/using-page-inspector-in-aspnet-mvc
msc.type: authoredcontent
ms.openlocfilehash: 5b443963a089f96a9dab11b7db4a25451075d6be
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="using-page-inspector-in-aspnet-mvc"></a><span data-ttu-id="98576-104">ASP.NET MVC에서 페이지 검사기 사용</span><span class="sxs-lookup"><span data-stu-id="98576-104">Using Page Inspector in ASP.NET MVC</span></span>
====================
<span data-ttu-id="98576-105">Tim Ammann으로</span><span class="sxs-lookup"><span data-stu-id="98576-105">by Tim Ammann</span></span>

> <span data-ttu-id="98576-106">Visual Studio 2012에서 페이지 검사기는 통합 된 브라우저와 웹 개발 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="98576-106">Page Inspector in Visual Studio 2012 is a web development tool with an integrated browser.</span></span> <span data-ttu-id="98576-107">통합된 브라우저에서 요소를 선택 하 고 페이지 검사기 강조 즉시 요소의 소스 및 CSS 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-107">Select any element in the integrated browser, and Page Inspector instantly highlights the element's source and CSS.</span></span> <span data-ttu-id="98576-108">모든 MVC 뷰, 신속 하 게 렌더링 된 태그의 원본을 살펴봅니다 찾아 수 Visual Studio 환경 내에서 직접 브라우저 도구를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-108">You can browse any MVC view, quickly find the sources of rendered markup, and use browser tools right within the Visual Studio environment.</span></span>
> 
> [<span data-ttu-id="98576-109">비디오를 보기</span><span class="sxs-lookup"><span data-stu-id="98576-109">Watch the Video</span></span>](../../videos/mvc-4/using-page-inspector-in-aspnet-mvc.md)
> 
> <span data-ttu-id="98576-110">이 자습서에서는 검사 모드를 활성화 한 후 신속 하 게 찾아 웹 프로젝트 내에서 태그와 CSS를 편집 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="98576-110">This tutorial shows how to enable Inspection Mode, and then quickly locate and edit markup and CSS within your web project.</span></span> <span data-ttu-id="98576-111">이 자습서는 MVC 프로젝트를 사용 하지만 대 한 페이지 검사기를 사용할 수도 있습니다 [Web Forms](https://go.microsoft.com/?linkid=9802001) 다른 ASP.NET 응용 프로그램 및입니다.</span><span class="sxs-lookup"><span data-stu-id="98576-111">The tutorial uses an MVC Project, but you can also use Page Inspector for [Web Forms](https://go.microsoft.com/?linkid=9802001) and other ASP.NET applications.</span></span>
> 
> <span data-ttu-id="98576-112">이 자습서에는 다음 섹션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98576-112">The tutorial has the following sections:</span></span>
> 
> - [<span data-ttu-id="98576-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="98576-113">Prerequisites</span></span>](#_1_prerequisites)
> - [<span data-ttu-id="98576-114">웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="98576-114">Create a Web Application</span></span>](#_2_creating_a)
> - [<span data-ttu-id="98576-115">보기에 찾아보는 페이지 검사기를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="98576-115">Use Page Inspector to Browse to a View</span></span>](#_3_using_page)
> - [<span data-ttu-id="98576-116">검사 모드를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="98576-116">Enable Inspection Mode</span></span>](#_4_inspection_mode)
> - [<span data-ttu-id="98576-117">페이지 검사기를 사용 하 여 태그를 변경 하려면</span><span class="sxs-lookup"><span data-stu-id="98576-117">Use Page Inspector to Make Changes to Markup</span></span>](#_5_using_page)
> - [<span data-ttu-id="98576-118">검사 모드 및 HTML 창</span><span class="sxs-lookup"><span data-stu-id="98576-118">Inspection Mode and the HTML Window</span></span>](#_6_inspection_mode)
> - [<span data-ttu-id="98576-119">스타일 창에서 CSS 변경 내용 미리 보기</span><span class="sxs-lookup"><span data-stu-id="98576-119">Preview CSS Changes in the Styles window</span></span>](#_7_previewing_css)
> - [<span data-ttu-id="98576-120">CSS Auto Sync</span><span class="sxs-lookup"><span data-stu-id="98576-120">CSS Auto Sync</span></span>](#css_auto_sync)
> - [<span data-ttu-id="98576-121">CSS 색 선택을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="98576-121">Using the CSS Color Picker</span></span>](#css_color_picker)
> - [<span data-ttu-id="98576-122">JavaScript에 매핑 동적 페이지 요소</span><span class="sxs-lookup"><span data-stu-id="98576-122">Mapping Dynamic Page Elements to JavaScript</span></span>](#map_dynamic_elements)


<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="98576-123">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="98576-123">Prerequisites</span></span>

- <span data-ttu-id="98576-124">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11) 또는 [Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-124">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11) or [Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span>

> [!NOTE]
> <span data-ttu-id="98576-125">페이지 검사기의 최신 버전을 사용 [웹 플랫폼 설치 관리자](https://go.microsoft.com/fwlink/?LinkId=255386) 를 Windows Azure SDK for.NET 2.0 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-125">To get the latest version of Page Inspector, use [Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386) to install the Windows Azure SDK for .NET 2.0.</span></span>


<span data-ttu-id="98576-126">페이지 검사기는 Microsoft 웹 개발자 도구와 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98576-126">Page Inspector is bundled with Microsoft Web Developer Tools.</span></span> <span data-ttu-id="98576-127">최신 버전은 1.3.</span><span class="sxs-lookup"><span data-stu-id="98576-127">The latest version is 1.3.</span></span> <span data-ttu-id="98576-128">어떤 버전을 확인 하려면, Visual Studio를 실행 있고 선택 **에 대 한 Microsoft Visual Studio** 에서 **도움말** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="98576-128">To check which version you have, run Visual Studio and select **About Microsoft Visual Studio** from the **Help** menu.</span></span>

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a><span data-ttu-id="98576-129">웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="98576-129">Create a Web Application</span></span>

<span data-ttu-id="98576-130">페이지 검사기를 사용 하는 웹 응용 프로그램을 먼저 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98576-130">First, create a web application that you will use Page Inspector with.</span></span> <span data-ttu-id="98576-131">Visual Studio에서 선택 **파일** &gt; **새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-131">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="98576-132">확장 왼쪽의 **Visual C#**선택, **웹**를 선택한 후 **ASP.NET MVC4 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-132">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET MVC4 Web Application**.</span></span>

![새 ASP.NET MVC 응용 프로그램](using-page-inspector-in-aspnet-mvc/_static/image2.png)

<span data-ttu-id="98576-134">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-134">Click **OK**.</span></span>

<span data-ttu-id="98576-135">에 **새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **인터넷 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-135">In the **New ASP.NET MVC 4 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="98576-136">둡니다 **Razor** 를 기본 뷰 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="98576-136">Leave **Razor** as the default view engine.</span></span>

![새 ASP.NET MVC 프로젝트-인터넷 응용 프로그램](using-page-inspector-in-aspnet-mvc/_static/image4.png)

<span data-ttu-id="98576-138">응용 프로그램에서 열립니다 **소스** 보기.</span><span class="sxs-lookup"><span data-stu-id="98576-138">The application opens in **Source** view.</span></span>

![소스 뷰에서 새 ASP.NET MVC 응용 프로그램](using-page-inspector-in-aspnet-mvc/_static/image6.png)

<span data-ttu-id="98576-140">이제 응용 프로그램을 사용 했으므로 검사 하 고 수정 페이지 검사기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98576-140">Now that you have an application to work with, you can use Page Inspector to examine and modify it.</span></span>

<a id="_starting_page_inspector"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-browse-to-a-view"></a><span data-ttu-id="98576-141">보기에 찾아보는 페이지 검사기를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="98576-141">Use Page Inspector to Browse to a View</span></span>

<span data-ttu-id="98576-142">Visual Studio 2012에서 있습니다 수 마우스 오른쪽 단추로 클릭 보기 중 하나 선택 하면 프로젝트에서 **페이지 검사기에서 보기**, 페이지 검사기에서 경로 파악 하 고 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-142">In Visual Studio 2012, you can right-click any view in your project, select **View in Page Inspector**, and Page Inspector will figure out the route and display the page.</span></span>

<span data-ttu-id="98576-143">**솔루션 탐색기**를 확장 하 고는 **뷰** 폴더 차례로 **홈** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="98576-143">In **Solution Explorer**, expand the **Views** folder and then the **Home** folder.</span></span> <span data-ttu-id="98576-144">Index.cshtml 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 **페이지 검사기에서 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-144">Right click the Index.cshtml file and choose **View in Page Inspector**.</span></span>

![페이지 검사기에서 보기 Index.cshtml](using-page-inspector-in-aspnet-mvc/_static/image8.png)

<span data-ttu-id="98576-146">기본적으로 Visual Studio 환경의 왼쪽에서 페이지 검사기 창으로 도킹 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98576-146">By default, Page Inspector is docked as a window on the left side of the Visual Studio environment.</span></span> <span data-ttu-id="98576-147">원하는 경우, 다른 위치에서 도킹 하거나 창을 도킹을 해제 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98576-147">If you prefer, you can dock it elsewhere, or undock the window.</span></span> <span data-ttu-id="98576-148">참조 [하는 방법: 창 정렬 및 도킹](https://msdn.microsoft.com/library/z4y0hsax.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-148">See [How to: Arrange and Dock Windows](https://msdn.microsoft.com/library/z4y0hsax.aspx).</span></span>

<span data-ttu-id="98576-149">페이지 검사기 창 상단의 브라우저 창에서 현재 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="98576-149">The top pane of the Page Inspector window shows the current page in a browser window.</span></span> <span data-ttu-id="98576-150">아래쪽 창의 페이지의 다양 한 측면을 검사할 수 있는 일부 탭 함께 HTML 태그에서 페이지를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="98576-150">The bottom pane shows the page in HTML markup, along with some tabs that let you inspect different aspects of the page.</span></span> <span data-ttu-id="98576-151">아래쪽 창의 비슷합니다는 [F12 개발자 도구](https://msdn.microsoft.com/ie/aa740478) Internet Explorer에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-151">The bottom pane is similar to the [F12 Developer Tools](https://msdn.microsoft.com/ie/aa740478) in Internet Explorer.</span></span>

![페이지 검사기에서 ASP.NET MVC 응용 프로그램](using-page-inspector-in-aspnet-mvc/_static/image10.png)

<span data-ttu-id="98576-153">이 자습서를 사용 하 여는 **HTML** 및 **스타일** 탭을 신속 하 게 이동 하 고 응용 프로그램을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-153">In this tutorial, you will use the **HTML** and **Styles** tabs to navigate quickly and make changes to the application.</span></span>

<a id="_examining_(&quot;decomposing&quot;)_the"></a><a id="_inspection_mode_and"></a><a id="_4_inspection_mode"></a>

## <a name="enableinspection-mode"></a><span data-ttu-id="98576-154">EnableInspection 모드</span><span class="sxs-lookup"><span data-stu-id="98576-154">EnableInspection Mode</span></span>

<span data-ttu-id="98576-155">페이지 검사기를 검사 모드에 두, 클릭는 **검사** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="98576-155">To put Page Inspector into Inspection Mode, click the **Inspect** button.</span></span> <span data-ttu-id="98576-156">검사 모드에서 렌더링된 된 페이지 부분 위로 마우스 포인터를 가져가면 해당 소스 태그 또는 코드가 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98576-156">In Inspection Mode, when you hold the mouse pointer over any part of the rendered page, the corresponding source markup or code is highlighted.</span></span>

![검사 모드를 설정/해제](using-page-inspector-in-aspnet-mvc/_static/image12.png)

<span data-ttu-id="98576-158">이제 페이지 검사기 내에서 해당 페이지의 다른 부분 위로 마우스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-158">Now move your mouse over different parts of the page within Page Inspector.</span></span> <span data-ttu-id="98576-159">와 마찬가지로, 마우스 포인터는 큰 더하기 기호를 변경 하 고 아래 요소가 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98576-159">As you do, the mouse pointer changes to a large plus sign, and the element underneath is highlighted:</span></span>

![마우스로 가리키면 div.content 래퍼](using-page-inspector-in-aspnet-mvc/_static/image14.png)

<span data-ttu-id="98576-161">마우스 포인터를 이동 하면 Visual Studio는 소스 파일에서 해당 Razor 구문 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98576-161">As you move the mouse pointer, Visual Studio highlights the corresponding Razor syntax in the source file.</span></span> <span data-ttu-id="98576-162">HTML 요소 다른 소스 파일의 경우, Visual Studio는 자동으로 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="98576-162">If the HTML element comes from another source file, Visual Studio automatically opens the file.</span></span>

<span data-ttu-id="98576-163">페이지 검사기에는 **HTML** Razor 구문에서 생성 된 HTML 탭에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-163">In Page Inspector, the **HTML** tab shows the HTML that was generated from the Razor syntax.</span></span> <span data-ttu-id="98576-164">마우스 포인터를 이동 하면 HTML 요소를 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98576-164">As you move the mouse pointer, the HTML elements are highlighted.</span></span> <span data-ttu-id="98576-165">**스타일** 탭 요소에 대 한 CSS 규칙을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-165">The **Styles** tab shows the CSS rules for the element.</span></span>

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a><span data-ttu-id="98576-166">페이지 검사기를 사용 하 여 태그를 변경 하려면</span><span class="sxs-lookup"><span data-stu-id="98576-166">Use Page Inspector to Make Changes to Markup</span></span>

<span data-ttu-id="98576-167">페이지 검사기를 사용 하면 위치 명확 하 게 드러나지 태그를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98576-167">Page Inspector lets you find markup whose location might not be obvious.</span></span> <span data-ttu-id="98576-168">다음 태그를 수정 하 고 결과 변경 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98576-168">Then you can modify the markup and see the resulting changes.</span></span>

<span data-ttu-id="98576-169">이 확인 하려면 클릭 **검사** 는 페이지 검사기 창에 있는 페이지의 아래쪽으로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-169">To see this, click **Inspect** and then scroll to the bottom of the page in the Page Inspector window.</span></span>

<span data-ttu-id="98576-170">바닥글 영역에 마우스 포인터를 이동 하면 페이지 검사기 열립니다는 \_Layout.cshtml 파일 선택한 레이아웃 페이지의 섹션을 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-170">When you move the mouse pointer into the footer area, Page Inspector opens the \_Layout.cshtml file and highlights the section of the layout page that you have selected.</span></span> <span data-ttu-id="98576-171">바닥글은 볼 수 있듯이 레이아웃 파일 및 뷰 자체에 정의 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98576-171">As you can see, the footer are is defined in the layout file, and not the view itself.</span></span>

![바닥글](using-page-inspector-in-aspnet-mvc/_static/image16.png)

<span data-ttu-id="98576-173">이제 저작권 정보를 선 위로 마우스 포인터를 이동 <a id="a"> </a>확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-173">Now move your mouse pointer over the line with the copyright <a id="a"></a>notice.</span></span> <span data-ttu-id="98576-174">에 \_Layout.cshtml 페이지에서 해당 줄이 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98576-174">In the \_Layout.cshtml page, the corresponding line is highlighted.</span></span>

![바닥글 저작권 줄 강조 표시](using-page-inspector-in-aspnet-mvc/_static/image18.png)

<span data-ttu-id="98576-176">텍스트 줄의 끝에 추가 \_Layout.cshtml 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="98576-176">Add some text to the end of the line in the \_Layout.cshtml file.</span></span>

<span data-ttu-id="98576-177">&lt;p&gt;&amp;; 복사 @DateTime.Now.Year -내 ASP.NET MVC 응용 프로그램의! &lt;/p&gt;</span><span class="sxs-lookup"><span data-stu-id="98576-177">&lt;p&gt;&amp;copy; @DateTime.Now.Year - My ASP.NET MVC Application Rocks!&lt;/p&gt;</span></span>

<span data-ttu-id="98576-178">Ctrl + Alt + Enter를 누르거나 업데이트 표시줄 페이지 검사기의 브라우저 창에서 결과를 보려면 클릭 이제 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-178">Now, press Ctrl+Alt+Enter or click the Update Bar to see the results in the Page Inspector browser window.</span></span>

![내 ASP.NET 응용 프로그램 돌!](using-page-inspector-in-aspnet-mvc/_static/image20.png)

<span data-ttu-id="98576-180">바닥글 Index.cshtml에 정의 되어 있지만 있는 것으로 판명 생각는 \_Layout.cshtml, 및 페이지 검사기를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98576-180">You might have thought that the footer defined in Index.cshtml, but it turned out to be in the \_Layout.cshtml, and Page Inspector found it for you.</span></span>

<a id="_inspection_mode_and_1"></a><a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a><span data-ttu-id="98576-181">검사 모드 및 HTML 창</span><span class="sxs-lookup"><span data-stu-id="98576-181">Inspection Mode and the HTML Window</span></span>

<span data-ttu-id="98576-182">다음으로, HTML 창과 요소 수에 대 한 매핑 방법을 빠르게 확인을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-182">Next, you will have a quick look at the HTML window and how it maps elements for you.</span></span>

<span data-ttu-id="98576-183">클릭 **검사** 검사 모드에서 페이지 검사기를 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98576-183">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="98576-184">"Logohere" 라고 표시 되는 페이지의 상단 부분을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-184">Click the top part of the page that says "Your logohere".</span></span> <span data-ttu-id="98576-185">좀 더 자세하게 하므로 브라우저 창에 표시 되는 마우스 포인터를 이동 하면 더 이상 변경의 특정 요소를 검사 하 고 없습니다.</span><span class="sxs-lookup"><span data-stu-id="98576-185">You are examining a particular element in more detail, so the display in the browser window no longer changes as you move the mouse pointer.</span></span>

<span data-ttu-id="98576-186">이제으로 마우스 포인터를 이동는 **HTML** 창.</span><span class="sxs-lookup"><span data-stu-id="98576-186">Now move the mouse pointer to the **HTML** window.</span></span> <span data-ttu-id="98576-187">페이지 검사기에서 요소를 간략하게 설명 하는 마우스 포인터를 이동 하면는 **HTML** 창 고 브라우저 창에서 해당 요소를 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-187">As you move the mouse pointer, Page Inspector outlines the element within the **HTML** window and highlights the corresponding element in the browser window.</span></span>

![HTML 창](using-page-inspector-in-aspnet-mvc/_static/image22.png)

<span data-ttu-id="98576-189">페이지 검사기 열리면 이전에 \_임시 탭에서 사용자에 대 한 Layout.cshtml 파일. 클릭는 \_Layout.cshtml 임시 탭 및 해당 태그에서 강조 표시 됩니다는 &lt;헤더&gt; 섹션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98576-189">As before, Page Inspector opens the \_Layout.cshtml file for you in a temporary tab. Click the \_Layout.cshtml temporary tab, and the corresponding markup will be highlighted in the &lt;header&gt; section for you:</span></span>

![강조 표시 된 태그](using-page-inspector-in-aspnet-mvc/_static/image24.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a><span data-ttu-id="98576-191">스타일 창에서 CSS 변경 내용 미리 보기</span><span class="sxs-lookup"><span data-stu-id="98576-191">Preview CSS Changes in the Styles Window</span></span>

<span data-ttu-id="98576-192">다음으로, 페이지 검사기 사용할지 **스타일** CSS 변경 내용이 미리 보기 위해 창을 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-192">Next, you will use the Page Inspector **Styles** window to preview changes to CSS.</span></span>

<span data-ttu-id="98576-193">클릭 **검사** 검사 모드에서 페이지 검사기를 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98576-193">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="98576-194">페이지 검사기 브라우저 창에서 마우스 포인터를 이동 될 때까지 "홈 페이지" 섹션에서 **div.content 래퍼** 레이블이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98576-194">In the Page Inspector browser window, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span>

![마우스로 가리키면 div.content 래퍼](using-page-inspector-in-aspnet-mvc/_static/image26.png)

<span data-ttu-id="98576-196">Div.content 래퍼 섹션 내에서 한 번 클릭 한 다음에 마우스 포인터를 이동는 **스타일** 창.</span><span class="sxs-lookup"><span data-stu-id="98576-196">Click within the div.content-wrapper section once, and then move the mouse pointer to the **Styles** window.</span></span> <span data-ttu-id="98576-197">**Syles** 창에이 요소에 대 한 CSS 규칙을 모두 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-197">The **Syles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="98576-198">찾기.featured.content 래퍼 클래스 선택기까지 아래로 스크롤하십시오.</span><span class="sxs-lookup"><span data-stu-id="98576-198">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="98576-199">이제 배경 색 속성에 대 한 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-199">Now clear the checkbox for the background-color property.</span></span>

![지우기 배경색](using-page-inspector-in-aspnet-mvc/_static/image28.png)

<span data-ttu-id="98576-201">변경 내용을 즉시 페이지 검사기 브라우저 창에서 미리 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-201">Notice how the change previews instantly in the Page Inspector browser window.</span></span>

<span data-ttu-id="98576-202">다시 확인란을 선택, 속성 값을 두 번 클릭 및 빨강으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-202">Select the checkbox again, then double-click the property value and change it to red.</span></span> <span data-ttu-id="98576-203">변경 내용을 즉시 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="98576-203">The change shows immediately:</span></span>

![빨간색 배경색](using-page-inspector-in-aspnet-mvc/_static/image30.png)

<span data-ttu-id="98576-205">**스타일** 자체 시트 스타일 창에서는 스타일에 변경 내용을 커밋하기 전에 변경 하는 것을 쉽게 테스트 하 고 CSS를 미리 봅니다.</span><span class="sxs-lookup"><span data-stu-id="98576-205">The **Styles** window makes it easy to test and preview CSS changes before you commit the changes to the style sheet itself.</span></span>

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a><span data-ttu-id="98576-206">CSS 자동 동기화</span><span class="sxs-lookup"><span data-stu-id="98576-206">CSS Auto Sync</span></span>

> [!NOTE]
> <span data-ttu-id="98576-207">이 기능을 사용 하려면 버전 1.3 페이지 검사기의 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-207">This feature requires version 1.3 of Page Inspector.</span></span>


<span data-ttu-id="98576-208">CSS 자동 동기화 기능을 사용 하면 CSS 파일을 직접 편집 하 고 페이지 검사기 브라우저에서 즉시 변경 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98576-208">The CSS Auto-Sync feature allows you to edit a CSS file directly, and see the changes immediately in the Page Inspector browser.</span></span>

<span data-ttu-id="98576-209">클릭 **검사** 검사 모드에서 페이지 검사기를 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98576-209">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="98576-210">페이지 검사기 브라우저에서 "홈 페이지" 섹션까지 위로 마우스 포인터를 이동는 **div.content 래퍼** 레이블이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98576-210">In the Page Inspector browser, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span> <span data-ttu-id="98576-211">이 요소를 한 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-211">Click once to select this element.</span></span>

<span data-ttu-id="98576-212">**Syles** 창에이 요소에 대 한 CSS 규칙을 모두 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-212">The **Syles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="98576-213">찾기.featured.content 래퍼 클래스 선택기까지 아래로 스크롤하십시오.</span><span class="sxs-lookup"><span data-stu-id="98576-213">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="98576-214">".Featured.content 래퍼"를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-214">Click on ".featured .content-wrapper".</span></span> <span data-ttu-id="98576-215">페이지 검사기 (Site.css)이이 스타일을 정의 하 고 해당 CSS 스타일을 강조 표시 하는 CSS 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="98576-215">Page Inspector opens the CSS file that defines this style (Site.css) and highlights the corresponding CSS style.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image32.png)

<span data-ttu-id="98576-216">이제에 대 한 값을 변경할 `background-color` "red"를 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-216">Now change the value for `background-color` to "red".</span></span> <span data-ttu-id="98576-217">변경은 페이지 검사기 브라우저에서 즉시 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="98576-217">The change appears immediately in the Page Inspector browser.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image34.png)

<a id="css_color_picker"></a>
## <a name="using-the-css-color-picker"></a><span data-ttu-id="98576-218">CSS 색 선택을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="98576-218">Using the CSS Color Picker</span></span>

<span data-ttu-id="98576-219">Visual Studio 2012에서 CSS 편집기에는 쉽게 선택 하 고 색을 삽입 하는 색 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-219">The CSS editor in Visual Studio 2012 has a color picker that makes it easy to choose and insert colors.</span></span> <span data-ttu-id="98576-220">색 선택 표준 색 팔레트가 포함 하 고 표준 색 이름, 해시 코드, RGB, RGBA, HSL 및 HSLA 색을 지원 하며 문서에서 가장 최근에 사용한 색 목록이 유지.</span><span class="sxs-lookup"><span data-stu-id="98576-220">The color picker includes a standard palette of colors, supports standard color names, hash codes, RGB, RGBA, HSL, and HSLA colors, and maintains a list of the colors you've used most recently in the document.</span></span>

<span data-ttu-id="98576-221">이전 섹션에서의 값을 변경 하는 `background-color` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="98576-221">In the previous section, you changed the value of the `background-color` property.</span></span> <span data-ttu-id="98576-222">색상 선택기를 호출 하려면 속성 이름 및 형식을 후 삽입점을 배치  **#**  또는 **rgb (**합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-222">To invoke the color picker, place the insertion point after the property name and type **#** or **rgb(**.</span></span>

![CSS 색 선택 막대](using-page-inspector-in-aspnet-mvc/_static/image36.png)

<span data-ttu-id="98576-224">다음 왼쪽 및 오른쪽 화살표 키를 사용 하 여 색을 통과 하 고 색을 선택 하거나 아래쪽 화살표 키를 눌러 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-224">Click on a color to select it, or press the down arrow key and then use the left and right arrow keys to traverse the colors.</span></span> <span data-ttu-id="98576-225">색을 방문 하면 해당 하는 16 진수 값을 미리 보기:</span><span class="sxs-lookup"><span data-stu-id="98576-225">When you visit a color, the corresponding hex value is previewed:</span></span>

![미리 볼 배경색 속성 값](using-page-inspector-in-aspnet-mvc/_static/image38.png)

<span data-ttu-id="98576-227">색 막대 없는 경우 원하는 정확한 색, 색 선택 팝업 다운을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98576-227">If the color bar doesn't have the exact color you want, you can use the color picker pop-down.</span></span> <span data-ttu-id="98576-228">도구를 열려면 색 막대 오른쪽 끝에서 이중 펼침 단추를 클릭 하거나 키보드에서 아래쪽 화살표를 한 번 또는 두 번 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="98576-228">To open it, click the double chevron at the right end of the color bar, or press the Down Arrow once or twice on the keyboard.</span></span>

![CSS 색 선택 팝업 다운](using-page-inspector-in-aspnet-mvc/_static/image40.png)

<span data-ttu-id="98576-230">오른쪽에 있는 세로 막대에서 색을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-230">Click a color from the vertical bar on the right.</span></span> <span data-ttu-id="98576-231">주 창에서 해당 색에 대 한 그라데이션을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-231">This shows a gradient for that color in the main window.</span></span> <span data-ttu-id="98576-232">Enter 키를 눌러 직접 세로 막대에서에서 색을 선택 하거나 더욱 세부적으로 선택할 수 주 창에 있는 점을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-232">Choose a color directly from the vertical bar by pressing Enter, or click any point in the main window to choose with greater precision.</span></span>

<span data-ttu-id="98576-233">사용 하려는 컴퓨터 화면에는 색이 경우 (Visual Studio 사용자 인터페이스 안에 없는 함), 오른쪽 아래에 스 포 이트 도구를 사용 하 여 해당 값을 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98576-233">If there is a color on your computer screen that you want to use (it doesn't have to be inside the Visual Studio user interface), you can capture its value by using the eyedropper tool on the lower right.</span></span>

<span data-ttu-id="98576-234">색상 선택기의 맨 아래에 있는 슬라이더를 이동 하 여 색의 불투명도 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98576-234">You also can change the opacity of a color by moving the slider at the bottom of the color picker.</span></span> <span data-ttu-id="98576-235">이렇게 하면 변경 내용을 색 값을 RGBA 값 RGBA 형식을 불투명도 나타낼 수 있기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98576-235">Doing so changes color values to RGBA values, because the RGBA format can represent opacity.</span></span>

<span data-ttu-id="98576-236">색을 선택한 후 enter 키를 한 다음에 배경색 입력을 완료 하려면 세미콜론을 입력에서 *Site.css* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="98576-236">After you have chosen a color, press Enter, and then type a semicolon to complete the background-color entry in the *Site.css* file.</span></span>

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a><span data-ttu-id="98576-237">페이지 검사기 업데이트 표시줄</span><span class="sxs-lookup"><span data-stu-id="98576-237">The Page Inspector Update Bar</span></span>

<span data-ttu-id="98576-238">에 대 한 변경을 즉시 검색 하는 페이지 검사기는 *Site.css* 파일을 업데이트 표시줄에서 경고를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-238">Page Inspector immediately detects the change to the *Site.css* file and displays an alert in an update bar.</span></span>

![업데이트 표시줄](using-page-inspector-in-aspnet-mvc/_static/image42.png)

<span data-ttu-id="98576-240">모든 파일을 저장 하 고 페이지 검사기 브라우저 새로 고침, Ctrl + Alt + Enter 키를 누르거나 업데이트 표시줄을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-240">To save all your files and refresh the Page Inspector browser, press Ctrl+Alt+Enter or click the update bar.</span></span> <span data-ttu-id="98576-241">강조 색의 변경 내용을 확인 브라우저에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="98576-241">The change in the highlight color appears in the browser.</span></span>

<a id="map_dynamic_elements"></a>
## <a name="mapping-dynamic-page-elements-to-javascript"></a><span data-ttu-id="98576-242">JavaScript에 매핑 동적 페이지 요소</span><span class="sxs-lookup"><span data-stu-id="98576-242">Mapping Dynamic Page Elements to JavaScript</span></span>

<span data-ttu-id="98576-243">최신 웹 응용 프로그램에서 페이지의 요소는 JavaScript로 동적으로 생성 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="98576-243">In modern web applications, elements in the page are often generated dynamically with JavaScript.</span></span> <span data-ttu-id="98576-244">즉, 이러한 페이지 요소에 해당 하는 없는 static 태그 (HTML 또는 Razor) 하는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-244">That means there is no static markup (either HTML or Razor) that corresponds to these page elements.</span></span>

<span data-ttu-id="98576-245">버전 1.3, 페이지 검사기 페이지에 해당 하는 JavaScript 코드에 동적으로 추가 된 항목 이제 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98576-245">With version 1.3, Page Inspector can now map items that were dynamically added to the page back to the corresponding JavaScript code.</span></span> <span data-ttu-id="98576-246">이 기능을 보여 주기 위해 사용 합니다는 [단일 페이지 응용 프로그램 (SPA) 템플릿](../../../single-page-application/overview/introduction/knockoutjs-template.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-246">To demonstrate this feature, we'll use the [Single Page Application (SPA) template](../../../single-page-application/overview/introduction/knockoutjs-template.md).</span></span>

> [!NOTE]
> <span data-ttu-id="98576-247">SPA 템플릿에 필요는 [ASP.NET 및 웹 도구 2012.2](https://go.microsoft.com/fwlink/?LinkId=282650) 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-247">The SPA template requires the [ASP.NET and Web Tools 2012.2](https://go.microsoft.com/fwlink/?LinkId=282650) update.</span></span>


<span data-ttu-id="98576-248">Visual Studio에서 선택 **파일** &gt; **새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-248">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="98576-249">확장 왼쪽의 **Visual C#**선택, **웹**를 선택한 후 **ASP.NET MVC4 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-249">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET MVC4 Web Application**.</span></span> <span data-ttu-id="98576-250">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-250">Click **OK**.</span></span>

<span data-ttu-id="98576-251">에 **새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **단일 페이지 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-251">In the **New ASP.NET MVC 4 Project** dialog, select **Single Page Application**.</span></span>

<span data-ttu-id="98576-252">솔루션 탐색기에서 확장 된 **뷰** 폴더 차례로 **홈** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="98576-252">In Solution Explorer, expand the **Views** folder and then the **Home** folder.</span></span> <span data-ttu-id="98576-253">Index.cshtml 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 **페이지 검사기에서 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-253">Right click the Index.cshtml file and choose **View in Page Inspector**.</span></span>

<span data-ttu-id="98576-254">페이지 검사기 브라우저에서 먼저 즉 표시 되는 로그인 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="98576-254">The first thing that is displayed in the Page Inspector browser is a login page.</span></span> <span data-ttu-id="98576-255">"등록"을 클릭 하 고 사용자 이름 및 암호를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98576-255">Click "Sign Up" and create a user name and password.</span></span> <span data-ttu-id="98576-256">에 등록 되 면 응용 프로그램 로그인 하 고 일부 예제 항목으로는 할 일 목록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="98576-256">Once you sign up, the application logs you in and creates a to-do list with some sample items.</span></span>

<span data-ttu-id="98576-257">클릭 **검사** 검사 모드에서 페이지 검사기를 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98576-257">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span> <span data-ttu-id="98576-258">페이지 검사기 브라우저에서 할 일 항목 중 하나를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-258">In the Page Inspector browser, click on one of the to-do items.</span></span> <span data-ttu-id="98576-259">파란색으로 강조 표시 되 고 대신 요소 강조 표시 되어 있는지와 "JS" 주황색에서 요소 이름 옆에 있는 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-259">Notice that instead of being highlighted in blue, the element is highlighted in orange, with "JS" next to the element name.</span></span> <span data-ttu-id="98576-260">이 요소는 스크립트를 통해 동적으로 생성 된 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="98576-260">This indicates that the element was created dynamically through script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image44.png)

<span data-ttu-id="98576-261">에 주황색 밑줄이 표시 되는 또한는 **호출 스택** 탭 합니다. 나타냅니다는 **호출 스택** 창에 있는 요소에 대 한 자세한 정보.</span><span class="sxs-lookup"><span data-stu-id="98576-261">In addition, an orange underline appears on the **Call Stack** tab. This indicates that the **Call Stack** pane has more information about the element.</span></span>

<span data-ttu-id="98576-262">클릭는 **호출 스택** 탭 합니다. **호출 스택** 창에는 요소를 만든 JavaScript 호출에 대 한 호출 스택을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-262">Click on the **Call Stack** tab. The **Call Stack** pane shows the call stack for the JavaScript call that created the element.</span></span> <span data-ttu-id="98576-263">호출 외부 라이브러리에 jQuery, 축소와 같은 응용 프로그램 스크립트에 대 한 호출을 쉽게 볼 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-263">Calls to external libraries such as jQuery are collapsed, so that you can easily see the calls to your application script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image46.png)

<span data-ttu-id="98576-264">외부 라이브러리에 대 한 호출을 포함 하 여 전체 스택을 보려면 라이브러리 "외부" 이라는 노드를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98576-264">To see the full stack, including calls to external libraries, you can expand the nodes labeled "External Libraries":</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image48.png)

<span data-ttu-id="98576-265">호출 스택에 있는 항목을 클릭 하면 Visual Studio의 코드 파일이 열립니다 하 고 해당 스크립트를 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="98576-265">If you click an item in the call stack, Visual Studio opens the code file and highlights the corresponding script.</span></span>

![](using-page-inspector-in-aspnet-mvc/_static/image50.png)

## <a name="see-also"></a><span data-ttu-id="98576-266">참고 항목</span><span class="sxs-lookup"><span data-stu-id="98576-266">See Also</span></span>

<span data-ttu-id="98576-267">[Visual Studio와 함께 ASP.NET MVC 4 소개](../older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md) (ASP.net 웹 사이트)</span><span class="sxs-lookup"><span data-stu-id="98576-267">[Intro to ASP.NET MVC 4 with Visual Studio](../older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md) (ASP.net website)</span></span>

<span data-ttu-id="98576-268">[페이지 검사기 소개](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector/) (Channel 9 비디오)</span><span class="sxs-lookup"><span data-stu-id="98576-268">[Introducing Page Inspector](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector/) (Channel 9 video)</span></span>

<span data-ttu-id="98576-269">[페이지 검사자 오류 메시지](https://go.microsoft.com/?linkid=9813062) (MSDN)</span><span class="sxs-lookup"><span data-stu-id="98576-269">[Page Inspector Error Messages](https://go.microsoft.com/?linkid=9813062) (MSDN)</span></span>
