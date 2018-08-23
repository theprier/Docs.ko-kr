---
uid: web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
title: Visual Studio 2012에 ASP.NET Web forms 페이지 검사기 사용 | Microsoft Docs
author: rick-anderson
description: Visual Studio 2012 용 페이지 검사기는 통합 된 브라우저를 사용 하 여 웹 개발 도구입니다. 통합 된 브라우저 및 페이지 검사기에서 모든 요소를 선택 하는 중...
ms.author: riande
ms.date: 08/15/2012
ms.assetid: 2ece0bf4-aae5-4ff4-8f62-28e0819d4f86
msc.legacyurl: /web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
msc.type: authoredcontent
ms.openlocfilehash: d2c377f8466f8f324b75ce60860aa00c11bc0ffe
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41837675"
---
<a name="using-page-inspector-for-visual-studio-2012-in-aspnet-web-forms"></a><span data-ttu-id="6c3b0-104">ASP.NET Web Forms에서 Visual Studio 2012 용 페이지 검사기 사용</span><span class="sxs-lookup"><span data-stu-id="6c3b0-104">Using Page Inspector for Visual Studio 2012 in ASP.NET Web Forms</span></span>
====================
<span data-ttu-id="6c3b0-105">Tim Ammann 여</span><span class="sxs-lookup"><span data-stu-id="6c3b0-105">by Tim Ammann</span></span>

> <span data-ttu-id="6c3b0-106">Visual Studio 2012 용 페이지 검사기는 통합 된 브라우저를 사용 하 여 웹 개발 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-106">Page Inspector for Visual Studio 2012 is a web development tool with an integrated browser.</span></span> <span data-ttu-id="6c3b0-107">통합 된 브라우저에서 모든 요소를 선택 하 고 요소의 소스 및 CSS 페이지 검사기를 즉시 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-107">Select any element in the integrated browser, and Page Inspector instantly highlights the element's source and CSS.</span></span> <span data-ttu-id="6c3b0-108">응용 프로그램에서 모든 페이지를 탐색, 신속 하 게 렌더링 된 태그의 원본을 살펴봅니다를 Visual Studio 환경 내에서 바로 브라우저 도구를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-108">You can browse any page in your application, quickly find the sources of rendered markup, and use browser tools right within the Visual Studio environment.</span></span>
> 
> <span data-ttu-id="6c3b0-109">이 자습서 shwos 검사 모드를 활성화 한 후 신속 하 게 찾아 CSS 규칙 및 웹 프로젝트 내에서 텍스트를 편집 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-109">This tutorial shwos how to enable Inspection Mode and then quickly locate and edit CSS rules and text within your web project.</span></span> <span data-ttu-id="6c3b0-110">이 자습서에서는 Web Forms 응용 프로그램 프로젝트를 사용 하지만 웹 사이트 프로젝트에 대 한 페이지 검사기를 사용할 수도 있습니다 및 [MVC](https://go.microsoft.com/?linkid=9802002) 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-110">The tutorial uses a Web Forms Application Project, but you can also use Page Inspector for Web Site projects and [MVC](https://go.microsoft.com/?linkid=9802002) applications.</span></span>
> 
> <span data-ttu-id="6c3b0-111">이 자습서에는 다음 섹션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-111">The tutorial has the following sections:</span></span>
> 
> [<span data-ttu-id="6c3b0-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6c3b0-112">Prerequisites</span></span>](#_1_prerequisites)
> 
> [<span data-ttu-id="6c3b0-113">웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="6c3b0-113">Create a Web Application</span></span>](#_2_creating_a)
> 
> [<span data-ttu-id="6c3b0-114">페이지 검사기를 사용 하 여 응용 프로그램을 보려면</span><span class="sxs-lookup"><span data-stu-id="6c3b0-114">Use Page Inspector to View the Application</span></span>](#_3_using_page)
> 
> [<span data-ttu-id="6c3b0-115">검사 모드를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="6c3b0-115">Enable Inspection Mode</span></span>](#_4_inspection_mode)
> 
> [<span data-ttu-id="6c3b0-116">페이지 검사기를 사용 하 여 태그를 변경 하려면</span><span class="sxs-lookup"><span data-stu-id="6c3b0-116">Use Page Inspector to Make Changes to Markup</span></span>](#_5_using_page)
> 
> [<span data-ttu-id="6c3b0-117">HTML 창과 검사 모드</span><span class="sxs-lookup"><span data-stu-id="6c3b0-117">Inspection Mode and the HTML Window</span></span>](#_6_inspection_mode)
> 
> [<span data-ttu-id="6c3b0-118">스타일 창에서 CSS 변경 내용 미리 보기</span><span class="sxs-lookup"><span data-stu-id="6c3b0-118">Preview CSS Changes in the Styles Window</span></span>](#_7_previewing_css)
> 
> [<span data-ttu-id="6c3b0-119">CSS 자동 동기화</span><span class="sxs-lookup"><span data-stu-id="6c3b0-119">CSS Auto Sync</span></span>](#css_auto_sync)
> 
> [<span data-ttu-id="6c3b0-120">CSS 색 선택을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="6c3b0-120">Using the CSS Color Picker</span></span>](#css_color_picker)


<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="6c3b0-121">전제 조건</span><span class="sxs-lookup"><span data-stu-id="6c3b0-121">Prerequisites</span></span>

- <span data-ttu-id="6c3b0-122">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11) 나 [Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-122">[Visual Studio 2012](https://www.microsoft.com/visualstudio/11) or [Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web).</span></span>

> [!NOTE]
> <span data-ttu-id="6c3b0-123">페이지 검사기의 최신 버전을 사용 [웹 플랫폼 설치 관리자](https://go.microsoft.com/fwlink/?LinkId=255386) .NET 2.0에 대 한 Azure SDK를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-123">To get the latest version of Page Inspector, use [Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=255386) to install the Azure SDK for .NET 2.0.</span></span>


<span data-ttu-id="6c3b0-124">페이지 검사기는 Microsoft Web 개발자 도구를 사용 하 여 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-124">Page Inspector is bundled with Microsoft Web Developer Tools.</span></span> <span data-ttu-id="6c3b0-125">최신 버전 1.3입니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-125">The latest version is 1.3.</span></span> <span data-ttu-id="6c3b0-126">어떤 버전을 확인 하려면, Visual Studio를 실행 있고 선택 **Microsoft Visual Studio 정보** 에서 합니다 **도움말** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-126">To check which version you have, run Visual Studio and select **About Microsoft Visual Studio** from the **Help** menu.</span></span>

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a><span data-ttu-id="6c3b0-127">웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="6c3b0-127">Create a Web Application</span></span>

<span data-ttu-id="6c3b0-128">먼저 사용 하 여 페이지 검사기 사용 하 여 웹 응용 프로그램을 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-128">First, you will create a web application that you will use Page Inspector with.</span></span> <span data-ttu-id="6c3b0-129">Visual Studio에서 선택 **파일** &gt; **새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-129">In Visual Studio, choose **File** &gt; **New Project**.</span></span> <span data-ttu-id="6c3b0-130">왼쪽의 확장 **Visual C#** 를 선택 **웹**를 선택한 후 **ASP.NET Web Forms 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-130">On the left, expand **Visual C#**, select **Web**, and then select **ASP.NET Web Forms Application**.</span></span>

![새 Web Forms 응용 프로그램](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image1.png)

<span data-ttu-id="6c3b0-132">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-132">Click **OK**.</span></span>

<span data-ttu-id="6c3b0-133">응용 프로그램에서 엽니다 **원본** 보기.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-133">The application opens in **Source** view.</span></span>

![소스 뷰에서 새 Web Forms 응용 프로그램](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image2.png)

<span data-ttu-id="6c3b0-135">응용 프로그램 사용을 설정 했으므로 점검 하 여 수정 페이지 검사기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-135">Now that you have an application to work with, you can use Page Inspector to examine and modify it.</span></span>

<a id="_starting_page_inspector"></a><a id="_3_starting_page"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-view-the-application"></a><span data-ttu-id="6c3b0-136">페이지 검사기를 사용 하 여 응용 프로그램을 보려면</span><span class="sxs-lookup"><span data-stu-id="6c3b0-136">Use Page Inspector to View the Application</span></span>

<span data-ttu-id="6c3b0-137">다음으로, 페이지 검사기를 사용 하 여 응용 프로그램에 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-137">Next, you will view the application with Page Inspector.</span></span> <span data-ttu-id="6c3b0-138">**솔루션 탐색기**프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택한 **페이지 검사기에서 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-138">In **Solution Explorer**, right click the project, and then choose **View in Page Inspector**.</span></span>

![페이지 검사기에서 보기](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image3.png)

<span data-ttu-id="6c3b0-140">기본적으로 페이지 검사기가 처음으로 시작 되 면 도킹 될 좁은 창으로 Visual Studio 환경의 왼쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-140">By default, when Page Inspector launches for the first time, it is docked as a narrow window on the left side of the Visual Studio environment.</span></span> <span data-ttu-id="6c3b0-141">도구 영역 중 하나에서 위쪽, 아래쪽 또는 오른쪽에 도킹 되거나를 편리 하 게 되는 너비를 설정 하 고 왼쪽에 도킹 된 상태로 두십시오.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-141">Leave it docked on the left side and set it to a width that is comfortable for you, or dock it in one of the tool areas on the top, bottom, or right:</span></span>

![페이지 검사기 도킹 위치](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image4.png)

<span data-ttu-id="6c3b0-143">페이지 검사기 창의 도킹을 해제 하는 경우 배치할 수 있습니다 Visual Studio 외부에서 또는 두 번째 모니터에도 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-143">If you undock the Page Inspector window, you can place it outside Visual Studio, or even on a second monitor if you have one.</span></span> <span data-ttu-id="6c3b0-144">그러나 하려면 ALT + TAB 페이지 검사기 및 Visual Studio 사이에서 페이지 검사기 창을 도킹 없는 경우 이동할 **도구가** &gt; **옵션** &gt;  **환경** &gt; **탭과 Windows**, 및 **탭도**호출 하는 확인란의 선택을 취소 **부동 도구 창 위쪽에 항상 유지 합니다 주 창**:</span><span class="sxs-lookup"><span data-stu-id="6c3b0-144">However, in order to ALT+TAB between Page Inspector and Visual Studio when the Page Inspector window is undocked, go to **Tools** &gt; **Options** &gt; **Environment** &gt; **Tabs and Windows**, and under **Tab Well**, clear the check box called **Floating tool windows always stay on top of the main window**:</span></span>

![ALT + TAB Visual Studio와 도킹 되지 않은 페이지 검사기 창 사이 부동 도구 windows 확인란의 선택을 취소합니다](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image5.png)

<span data-ttu-id="6c3b0-146">페이지 검사기 창 상단의 브라우저 창에서 현재 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-146">The top pane of the Page Inspector window shows the current page in a browser window.</span></span> <span data-ttu-id="6c3b0-147">아래쪽 창 왼쪽에서 HTML 태그에서 페이지가 표시 되 고 일부 탭 수 있도록 하는 오른쪽 페이지의 다양 한 측면을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-147">The bottom pane shows the page in HTML markup on the left, and some tabs on the right that let you inspect different aspects of the page.</span></span> <span data-ttu-id="6c3b0-148">아래쪽 창은 비슷합니다는 [F12 개발자 도구](https://msdn.microsoft.com/ie/aa740478) Internet Explorer에서.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-148">The bottom pane is similar to the [F12 Developer Tools](https://msdn.microsoft.com/ie/aa740478) in Internet Explorer.</span></span> <span data-ttu-id="6c3b0-149">그러나 (개발자 도구와는 달리 사용할 수 있습니다 Visual Studio 내에서 오른쪽 페이지 검사기.)</span><span class="sxs-lookup"><span data-stu-id="6c3b0-149">(However, unlike the developer tools, you can use Page Inspector right within Visual Studio.)</span></span>

![페이지 검사기](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image6.png)

<span data-ttu-id="6c3b0-151">이 자습서에서는 페이지 검사기 브라우저 창에서 사용할지 및 **HTML** 하 고 **스타일** 수 있도록 신속 하 게 탭 탐색 및 응용 프로그램에 대 한 변경.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-151">In this tutorial, you will use the Page Inspector browser pane, and the **HTML** and **Styles** tabs to help you rapidly navigate and make changes to the application.</span></span>

<a id="_4_inspection_mode"></a>
## <a name="enable-inspection-mode"></a><span data-ttu-id="6c3b0-152">검사 모드를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="6c3b0-152">Enable Inspection Mode</span></span>

<span data-ttu-id="6c3b0-153">다음으로, 페이지 검사기의 검사 모드의 작동 원리에 대해 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-153">Next, you will see how Page Inspector's Inspection Mode works.</span></span> <span data-ttu-id="6c3b0-154">페이지 검사기 창에서 클릭 합니다 **검사** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-154">In the Page Inspector window, click the **Inspect** button.</span></span>

![요소를 검사 합니다.](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image7.png)

<span data-ttu-id="6c3b0-156">실행 중인 검사 모드를 확인 하려면 페이지 검사기 브라우저 창 내에서 페이지의 다른 부분 위로 마우스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-156">To see inspection mode in action, move your mouse over different parts of the page within the Page Inspector browser window.</span></span> <span data-ttu-id="6c3b0-157">마찬가지로, 마우스 포인터 큰 더하기 기호를으로 변경 되 고 아래에 있는 요소가 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-157">As you do, the mouse pointer changes to a large plus sign, and the element underneath is highlighted:</span></span>

![Div.content 래퍼를 가리키면](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image8.png)

<span data-ttu-id="6c3b0-159">마우스 포인터를 이동 하면 note는</span><span class="sxs-lookup"><span data-stu-id="6c3b0-159">As you move the mouse pointer, note that</span></span>

- <span data-ttu-id="6c3b0-160">내용을 **원본** 보기 페이지에서 선택한 요소에 해당 태그를 표시 하도록 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-160">The content in **Source** view changes to show the markup corresponding to the selected element on the page.</span></span> <span data-ttu-id="6c3b0-161">관련 태그 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-161">The relevant markup is highlighted.</span></span> <span data-ttu-id="6c3b0-162">원본이 다른 파일에 있으면 해당 파일이 강조 표시 된 관련 태그를 사용 하 여 소스 뷰에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-162">If the source is in another file, that file is opened in Source view with the relevant markup highlighted.</span></span>

- <span data-ttu-id="6c3b0-163">에 표시 되는 태그를 **HTML** 페이지 검사기에서 탭 페이지에서 선택한 요소에 일치 하도록 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-163">The markup displayed in the **HTML** tab in Page Inspector also changes to correspond to the selected element on the page.</span></span> <span data-ttu-id="6c3b0-164">에 **HTML** 탭 관련 태그는 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-164">In the **HTML** tab, the relevant markup is outlined.</span></span>

- <span data-ttu-id="6c3b0-165">합니다 **스타일** 탭 현재 선택 영역에 관한 CSS 규칙이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-165">The **Styles** tab shows the CSS rules relevant to the current selection.</span></span>

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a><span data-ttu-id="6c3b0-166">페이지 검사기를 사용 하 여 태그를 변경 하려면</span><span class="sxs-lookup"><span data-stu-id="6c3b0-166">Use Page Inspector to Make Changes to Markup</span></span>

<span data-ttu-id="6c3b0-167">이제를 찾고 태그 또는 위치가 즉시 명확 하지 않을 텍스트 변경 페이지 검사기를 사용 하는 방법을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-167">Now you will see how you can use Page Inspector to find and make changes to markup or text whose location might not be immediately obvious.</span></span>

<span data-ttu-id="6c3b0-168">검사 모드에서 페이지 검사기를 배치 하 고 홈 페이지의 아래쪽으로 스크롤하십시오.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-168">Put Page Inspector in Inspection Mode and then scroll to the bottom of the home page.</span></span>

<span data-ttu-id="6c3b0-169">영역의 바닥글 부분을 입력 하면 즉시 페이지 검사기 열립니다는 *Site.Master* 레이아웃 파일의 **원본** 오른쪽에 다른 임시 탭에서 보기 탭 및 마스터 부분을 강조 표시는 페이지 선택 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-169">As soon as you enter the footer area, Page Inspector opens the *Site.Master* layout file in **Source** view in a temporary tab to the right of the other tabs and highlights the section of the master page that you have selected.</span></span> <span data-ttu-id="6c3b0-170">이렇게 하면 페이지 검사기 수 검색 하 고 원래 열과 다른 파일에서 실제로 수행할 수 있는 페이지에 콘텐츠를 표시 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-170">This shows you how Page Inspector can find and display content on a page that might actually come from a different file than the one you originally opened.</span></span>

![검사 모드에서 바닥글 강조 표시](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image9.png)

<span data-ttu-id="6c3b0-172">페이지 검사기 브라우저 창에서 저작권 정보를 사용 하 여 줄 위로 마우스 포인터를 이동 <a id="a"> </a>알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-172">In the Page Inspector browser window, move your mouse pointer over the line with the copyright <a id="a"></a>notice.</span></span>

<span data-ttu-id="6c3b0-173">에 *Site.Master* 페이지에서 해당 줄이 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-173">In the *Site.Master* page, the corresponding line is highlighted.</span></span>

![바닥글 저작권 줄 강조 표시](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image10.png)

<span data-ttu-id="6c3b0-175">줄의 끝에 일부 텍스트를 추가 합니다 *Site.Master* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-175">Add some text to the end of the line in the *Site.Master* file.</span></span>

<span data-ttu-id="6c3b0-176">&lt;p&gt;&amp;복사 합니다. &lt;%: DateTime.Now.Year %&gt; -내 ASP.NET 응용 프로그램 Rocks!&lt; / p&gt;</span><span class="sxs-lookup"><span data-stu-id="6c3b0-176">&lt;p&gt;&amp;copy; &lt;%: DateTime.Now.Year %&gt; - My ASP.NET Application Rocks!&lt;/p&gt;</span></span>

<span data-ttu-id="6c3b0-177">이제 Ctrl + Alt + Enter를 누르거나 페이지 검사기 브라우저 창에서 결과 볼 수 업데이트 표시줄을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-177">Now, press Ctrl+Alt+Enter or click the Update Bar to see the results in the Page Inspector browser window.</span></span>

![내 ASP.NET 응용 프로그램 Rocks!](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image11.png)

<span data-ttu-id="6c3b0-179">바닥글에 있었음을 생각 합니다 *Default.aspx* 페이지 하지만 탓에 마스터 레이아웃 페이지에서를 페이지 검사기를 찾았습니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-179">You might have thought that the footer was on the *Default.aspx* page, but it turned out to be in the master layout page, and Page Inspector found it for you.</span></span>

<a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a><span data-ttu-id="6c3b0-180">HTML 창과 검사 모드</span><span class="sxs-lookup"><span data-stu-id="6c3b0-180">Inspection Mode and the HTML Window</span></span>

<span data-ttu-id="6c3b0-181">다음으로, HTML 창과 요소를 매핑되는 방법을 빠르게 확인을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-181">Next, you will have a quick look at the HTML window and how it maps elements for you.</span></span>

<span data-ttu-id="6c3b0-182">검사 모드에서 페이지 검사기를 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-182">Put Page Inspector in Inspection Mode.</span></span>

![요소를 검사 합니다.](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image12.png)

<span data-ttu-id="6c3b0-184">"사용자 로고는 여기" 라고 표시 되는 페이지의 위쪽을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-184">Click the top part of the page that says "your logo here".</span></span> <span data-ttu-id="6c3b0-185">보다 세부적으로 마우스 포인터를 이동 하면 브라우저 창에 표시를 변경 하는 더 이상 특정 요소를 검사 하 고 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-185">You are examining a particular element in more detail, so the display in the browser window no longer changes as you move the mouse pointer.</span></span>

<span data-ttu-id="6c3b0-186">이제 마우스 포인터를 이동 합니다 **HTML** 창입니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-186">Now move the mouse pointer to the **HTML** window.</span></span> <span data-ttu-id="6c3b0-187">마우스 포인터를 이동 하면 페이지 검사기 내의 요소를 설명 합니다 **HTML** 창 고 브라우저 창에서 해당 요소를 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-187">As you move the mouse pointer, Page Inspector outlines the element within the **HTML** window and highlights the corresponding element in the browser window.</span></span>

![HTML 창](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image13.png)

<span data-ttu-id="6c3b0-189">페이지 검사기가 열리면 이전에 *Site.Master* 임시 탭에서 파일입니다. Site.Master 탭을 클릭 하 고 해당 태그에서 강조 표시 됩니다는 &lt;헤더&gt; 섹션:</span><span class="sxs-lookup"><span data-stu-id="6c3b0-189">As before, Page Inspector opens the *Site.Master* file for you in a temporary tab. Click the Site.Master tab, and the corresponding markup is highlighted in the &lt;header&gt; section:</span></span>

![강조 표시 된 태그](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image14.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a><span data-ttu-id="6c3b0-191">스타일 창에서 CSS 변경 내용 미리 보기</span><span class="sxs-lookup"><span data-stu-id="6c3b0-191">Preview CSS Changes in the Styles Window</span></span>

<span data-ttu-id="6c3b0-192">다음으로 표시 됩니다 페이지 검사기를 사용 하는 방법을 **스타일** css 변경 내용 미리 보기 창입니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-192">Next, you will see how you can use the Page Inspector **Styles** window to preview changes to CSS.</span></span>

<span data-ttu-id="6c3b0-193">클릭 합니다 **검사** 검사 모드에서 페이지 검사기를 배치 하는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-193">Click the **Inspect** button to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="6c3b0-194">페이지 검사기 브라우저 창에서 마우스 포인터를 이동 될 때까지 "홈 페이지" 섹션을 마우스로 합니다 **div.content 래퍼** 레이블이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-194">In the Page Inspector browser window, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span>

![요소를 마우스로 가리킬](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image15.png)

<span data-ttu-id="6c3b0-196">Div.content 래퍼 섹션 내에서 한 번 클릭 하 고 다음으로 마우스 포인터를 이동 합니다 **스타일** 창입니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-196">Click within the div.content-wrapper section once, and then move the mouse pointer to the **Styles** window.</span></span> <span data-ttu-id="6c3b0-197">아래.featured.content 래퍼 클래스 선택기를 지우고 배경색 속성에 대 한 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-197">Under the .featured .content-wrapper class selector, clear and select the checkbox for the background-color property.</span></span>

![투명 한 배경이 색](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image16.png)

<span data-ttu-id="6c3b0-199">방법 변경 내용을 미리 봅니다. 즉시 페이지 검사기 브라우저 창에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-199">Notice how the change previews instantly in the Page Inspector browser window.</span></span>

<span data-ttu-id="6c3b0-200">다시 확인란을 선택, 다음 속성 값을 두 번 클릭 하 고 변경 `red`합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-200">Select the checkbox again, then double-click the property value and change it to `red`.</span></span> <span data-ttu-id="6c3b0-201">변경 내용을 즉시 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-201">The change shows immediately:</span></span>

![빨강 배경색.](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image17.png)

<span data-ttu-id="6c3b0-203">합니다 **스타일** 스타일으로 변경 내용을 커밋하기 전에 변경 하는 쉽게 테스트 하 고 CSS를 미리 보기 창을 사용 하면 자체 시트입니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-203">The **Styles** window makes it easy to test and preview CSS changes before you commit the changes to the style sheet itself.</span></span>

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a><span data-ttu-id="6c3b0-204">CSS 자동 동기화</span><span class="sxs-lookup"><span data-stu-id="6c3b0-204">CSS Auto Sync</span></span>

> [!NOTE]
> <span data-ttu-id="6c3b0-205">이 기능은 페이지 검사기의 버전 1.3을 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-205">This feature requires version 1.3 of Page Inspector.</span></span>


<span data-ttu-id="6c3b0-206">CSS 자동 동기화 기능을 사용 하면 CSS 파일을 직접 편집 하 고 페이지 검사기 브라우저에서 즉시 변경 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-206">The CSS Auto-Sync feature allows you to edit a CSS file directly, and see the changes immediately in the Page Inspector browser.</span></span>

<span data-ttu-id="6c3b0-207">클릭 **검사** 를 검사 모드에서 페이지 검사기를 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-207">Click **Inspect** to put Page Inspector in Inspection Mode.</span></span>

<span data-ttu-id="6c3b0-208">페이지 검사기 브라우저에서 "홈 페이지" 섹션까지 위로 마우스 포인터를 이동 합니다 **div.content 래퍼** 레이블이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-208">In the Page Inspector browser, move the mouse pointer over the "Home Page" section until the **div.content-wrapper** label appears.</span></span> <span data-ttu-id="6c3b0-209">이 요소를 한 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-209">Click once to select this element.</span></span>

<span data-ttu-id="6c3b0-210">합니다 **스타일** 이 요소에 대 한 CSS 규칙의 모든 창을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-210">The **Syles** window shows all of the CSS rules for this element.</span></span> <span data-ttu-id="6c3b0-211">찾기.featured.content 래퍼 클래스 선택기까지 아래로 스크롤하십시오.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-211">Scroll down to find the .featured .content-wrapper class selector.</span></span> <span data-ttu-id="6c3b0-212">".Featured.content-래퍼"를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-212">Click on ".featured .content-wrapper".</span></span> <span data-ttu-id="6c3b0-213">페이지 검사기 (Site.css)이이 스타일을 정의 하 고 해당 CSS 스타일을 강조 표시 하는 CSS 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-213">Page Inspector opens the CSS file that defines this style (Site.css) and highlights the corresponding CSS style.</span></span>

![CSS 파일](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image18.png)

<span data-ttu-id="6c3b0-215">이제 값을 변경 `background-color` "red"로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-215">Now change the value for `background-color` to "red".</span></span> <span data-ttu-id="6c3b0-216">페이지 검사기 브라우저에 변경 내용을 즉시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-216">The change appears immediately in the Page Inspector browser.</span></span>

![페이지 검사기 브라우저](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image19.png)

<a id="css_color_picker"></a>

## <a name="using-the-css-color-picker"></a><span data-ttu-id="6c3b0-218">CSS 색 선택을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="6c3b0-218">Using the CSS Color Picker</span></span>

<span data-ttu-id="6c3b0-219">다음으로, 페이지 검사기를 사용 하 여 신속 하 게 찾아서 CSS 기본 응용 프로그램에서 강조 표시 된 텍스트를 변경 하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-219">Next, you'll learn how to use Page Inspector to quickly find and change the CSS for highlighted text in the default application.</span></span> <span data-ttu-id="6c3b0-220">이 예제에서는 없는 파란색 강조 표시 하 고 싶으면 다른 색으로 변경 하려면 결정 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-220">In this example, you've decided that you don't like the blue highlighting and want to change it to another color.</span></span>

<span data-ttu-id="6c3b0-221">클릭 합니다 **검사** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-221">Click the **Inspect** button.</span></span>

![요소를 검사 합니다.](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image20.png)

<span data-ttu-id="6c3b0-223">페이지 검사기 브라우저 창에서 위로 마우스 포인터를 강조 표시 된 "비디오, 자습서 및 샘플" 텍스트가 CSS "표시" 레이블 되도록 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-223">In the Page Inspector browser window, move the mouse pointer over the highlighted "videos, tutorials, and samples" text so that the CSS "mark" label appears.</span></span>

![표시 요소를 가리키면](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image21.png)

<span data-ttu-id="6c3b0-225">텍스트 선택를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-225">Click the text to select it.</span></span> <span data-ttu-id="6c3b0-226">해당 CSS 표시 선택기의 맨 아래에 표시 되는 **스타일** 창입니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-226">The corresponding CSS mark selector appears at the bottom of the **Styles** window.</span></span>

![스타일 창에서 선택기를 표시 합니다.](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image22.png)

<span data-ttu-id="6c3b0-228">Mark 선택기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-228">Click the mark selector.</span></span> <span data-ttu-id="6c3b0-229">열립니다는 *Site.css* 웹 응용 프로그램에 대 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-229">This opens the *Site.css* file for the web application.</span></span> <span data-ttu-id="6c3b0-230">Site.css 탭을 클릭 하 고 해당 CSS 선택기를 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-230">Click the Site.css tab, and the corresponding CSS for the selector is highlighted:</span></span>

![스타일 시트에서 선택기를 표시 합니다.](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image23.png)

<span data-ttu-id="6c3b0-232">선택한 배경색 속성을 사용 하 여 줄을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-232">Select and remove the line with the background-color property.</span></span>

<span data-ttu-id="6c3b0-233">새 Visual Studio 2012 CSS 색 편집기 새 색을 선택 하는 데 사용할 이제 합니다 **표시** 배경색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-233">You will now use the new Visual Studio 2012 CSS color picker to choose a new color for the **mark** background-color property.</span></span>

<a id="_using_the_visual"></a>

### <a name="using-the-visual-studio-2012-css-color-picker"></a><span data-ttu-id="6c3b0-234">Visual Studio 2012 CSS 색 선택을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="6c3b0-234">Using the Visual Studio 2012 CSS Color Picker</span></span>

<span data-ttu-id="6c3b0-235">Visual Studio 2012에서 CSS 편집기에 쉽게 선택 하 고 색을 삽입 하는 색 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-235">The CSS editor in Visual Studio 2012 has a color picker that makes it easy to choose and insert colors.</span></span> <span data-ttu-id="6c3b0-236">간단한 색 막대 및 보다 세부적으로 제어를 제공 하는 "pop 다운" 선택기를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-236">It has a simple color bar and a "pop-down" picker that offers finer control.</span></span>

<span data-ttu-id="6c3b0-237">색 선택 표준 색 팔레트가 포함 표준 색 이름, 해시 코드, RGB, RGBA, HSL 및 HSLA 색을 지원 하며 문서에서 가장 최근에 사용 했던 색 목록을 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-237">The color picker includes a standard palette of colors, supports standard color names, hash codes, RGB, RGBA, HSL, and HSLA colors, and maintains a list of the colors you've used most recently in the document.</span></span>

<span data-ttu-id="6c3b0-238">배경색 속성이 줄에서 "bc"를 입력 하 고 아래쪽 화살표를 한 번 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-238">On the line where the background-color property was, type "bc" and press the down arrow once.</span></span>

<span data-ttu-id="6c3b0-239">"배경색"와 같은 하이픈으로 구분 된 속성에서 각 단어의 첫 번째 문자를 입력할 때 IntelliSense와 일치 하는 속성만 표시 하기에 대 한 목록이 필터링:</span><span class="sxs-lookup"><span data-stu-id="6c3b0-239">When you type the first character of each word in a hyphen-separated property like "background-color", IntelliSense filters the list for you to show only the properties that match:</span></span>

![Intellisense 필터링 값](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image24.png)

<span data-ttu-id="6c3b0-241">이제 콜론을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-241">Now type a colon.</span></span> <span data-ttu-id="6c3b0-242">작업을 수행 하면 전체 배경색 속성 이름을 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-242">When you do, the full background-color property name is inserted.</span></span> <span data-ttu-id="6c3b0-243">형식 **#** 또는 **rgb (**, 색 선택 막대에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-243">Type **#** or **rgb(**, and the color picker bar appears:</span></span>

![CSS 색 선택 막대](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image25.png)

<span data-ttu-id="6c3b0-245">색 선택 막대의 작동 원리를 보려면 마우스 포인터를 사용 하 여 해당 색 또는 아래쪽 화살표 키를 누릅니다 및 다음 왼쪽 및 오른쪽 화살표 키를 사용 하 여 색을 트래버스 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-245">To see how the color picker bar works, click its colors with the mouse pointer, or press the down arrow key and then use the left and right arrow keys to traverse the colors.</span></span> <span data-ttu-id="6c3b0-246">색을 방문 하면 배경색 속성에 대 한 해당 값을 미리 보기:</span><span class="sxs-lookup"><span data-stu-id="6c3b0-246">When you visit a color, the corresponding value for the background-color property is previewed:</span></span>

![미리 보기 배경 색 속성 값](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image26.png)

<span data-ttu-id="6c3b0-248">이 시점에서 선택한 값을 다음 CSS 항목을 완료 하려면 세미콜론 (;) Enter 키를 눌러 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-248">At this point, you could press Enter to select the value and then a semicolon (;) to complete the CSS entry.</span></span> <span data-ttu-id="6c3b0-249">이제 이동 다음 섹션의 색 선택 팝업 목록의 작동 원리를 볼 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-249">For now, go on to the next section so that you can see how the color picker pop-down works.</span></span>

#### <a name="using-the-color-picker-pop-down"></a><span data-ttu-id="6c3b0-250">색 선택 팝업 목록 사용</span><span class="sxs-lookup"><span data-stu-id="6c3b0-250">Using the Color Picker Pop-Down</span></span>

<span data-ttu-id="6c3b0-251">색 막대에 대 한 원하는 색에 없는 경우 pop 다운 색 선택기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-251">When the color bar doesn't have the exact color that you're looking for, you can use the color picker pop-down.</span></span>

<span data-ttu-id="6c3b0-252">를 열려면 색 막대의 오른쪽 끝에서 이중 펼침 단추를 클릭 하거나 키보드의 아래쪽 화살표 또는 두 번 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-252">To open it, click the double chevron at the right end of the color bar, or press the Down Arrow once or twice on the keyboard.</span></span>

![CSS 색 선택 팝업 다운](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image27.png)

<span data-ttu-id="6c3b0-254">오른쪽에 있는 세로 막대에서 색을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-254">Click a color from the vertical bar on the right.</span></span> <span data-ttu-id="6c3b0-255">주 창에서 해당 색 그라데이션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-255">This shows a gradient for that color in the main window.</span></span> <span data-ttu-id="6c3b0-256">Enter 키를 눌러 세로 막대에서 직접 색을 선택 하거나 더 높은 정밀도 사용 하 여 선택할 수 주 창의 시점을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-256">Choose a color directly from the vertical bar by pressing Enter, or click any point in the main window to choose with greater precision.</span></span>

<span data-ttu-id="6c3b0-257">사용 하려는 컴퓨터 화면에서 색을 있는지 (Visual Studio 사용자 인터페이스 내에 없는 함), 오른쪽 아래에 스 포 이트 도구를 사용 하 여 해당 값을 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-257">If there is a color on your computer screen that you want to use (it doesn't have to be inside the Visual Studio user interface), you can capture its value by using the eyedropper tool on the lower right.</span></span>

<span data-ttu-id="6c3b0-258">색 편집기의 맨 아래에서 슬라이더를 이동 하 여 색의 불투명도 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-258">You also can change the opacity of a color by moving the slider at the bottom of the color picker.</span></span> <span data-ttu-id="6c3b0-259">이렇게 하면 RGBA 형식을 불투명도 나타낼 수 있으므로 색상 RGBA 값에 값을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-259">Doing so changes color values to RGBA values because the RGBA format can represent opacity.</span></span>

<span data-ttu-id="6c3b0-260">색을 선택한 후 enter 키를 한 다음 배경색 항목을 완료 하려면 세미콜론을 입력 합니다 *Site.css* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-260">After you have chosen a color, press Enter, and then type a semicolon to complete the background-color entry in the *Site.css* file.</span></span>

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a><span data-ttu-id="6c3b0-261">페이지 검사기 업데이트 표시줄</span><span class="sxs-lookup"><span data-stu-id="6c3b0-261">The Page Inspector Update Bar</span></span>

<span data-ttu-id="6c3b0-262">페이지 검사기를 즉시 변경 검색 합니다 *Site.css* 파일 (또는 응용 프로그램의 모든 파일)에 업데이트 표시줄이 경고를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-262">Page Inspector immediately detects the change to the *Site.css* file (or to any file in the application) and displays an alert in an update bar.</span></span>

![업데이트 표시줄](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image28.png)

<span data-ttu-id="6c3b0-264">모든 파일을 저장 하 고 페이지 검사기 브라우저 새로 고침을 Ctrl + Alt + Enter 누르거나 업데이트 표시줄을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-264">To save all your files and refresh the Page Inspector browser, press Ctrl+Alt+Enter or click the update bar.</span></span> <span data-ttu-id="6c3b0-265">강조 표시 색 변화는 브라우저에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-265">The change in the highlight color appears in the browser:</span></span>

![강조 색 변경](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image29.png)

<a id="_using_page_inspector_1"></a><span data-ttu-id="6c3b0-267">편리 하 게 Visual Studio 환경 내에서 오른쪽 페이지 검사기 브라우저를 새로 고치는 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-267">Notice that you conveniently refreshed the Page Inspector browser right from within the Visual Studio environment.</span></span> <span data-ttu-id="6c3b0-268">페이지 검사기를 사용 하 여 외부 브라우저를 대신 하 여 웹 응용 프로그램을 개발할 때 편집기에서 상태를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c3b0-268">Using Page Inspector instead of an external browser lets you stay in the editor when you develop your web applications.</span></span>

## <a name="see-also"></a><span data-ttu-id="6c3b0-269">참고 항목</span><span class="sxs-lookup"><span data-stu-id="6c3b0-269">See Also</span></span>

<span data-ttu-id="6c3b0-270">[페이지 검사기 소개](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector) (채널 9 비디오)</span><span class="sxs-lookup"><span data-stu-id="6c3b0-270">[Introducing Page Inspector](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector) (Channel 9 video)</span></span>

<span data-ttu-id="6c3b0-271">[페이지 검사자 오류 메시지](https://go.microsoft.com/?linkid=9813062) (MSDN)</span><span class="sxs-lookup"><span data-stu-id="6c3b0-271">[Page Inspector Error Messages](https://go.microsoft.com/?linkid=9813062) (MSDN)</span></span>
