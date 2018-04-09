---
uid: web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
title: 페이지 검사기를 사용 하 여 Visual Studio 2012에서 | Microsoft Docs
author: rick-anderson
description: 이 실습 랩에서 새로운 도구를 찾아 Visual Studio-에서 페이지 검사기에서에서 웹 페이지 문제 해결에서 검색 합니다. 페이지 검사기는 새 도구 b는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 73232292-a5fe-4720-82a1-8f6553effd1f
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 052d29dba170d403c2b1c1667c55fc2c34045615
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="using-page-inspector-in-visual-studio-2012"></a><span data-ttu-id="5f57b-104">페이지 검사기를 사용 하 여 Visual Studio 2012에서</span><span class="sxs-lookup"><span data-stu-id="5f57b-104">Using Page Inspector in Visual Studio 2012</span></span>
====================
<span data-ttu-id="5f57b-105">으로 [웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="5f57b-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="5f57b-106">이 실습 랩에서 새로운 도구를 찾아 Visual Studio-에서 페이지 검사기에서에서 웹 페이지 문제 해결에서 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-106">In this Hands-on Lab, you will discover a new tool to find and fix web page issues in Visual Studio - the Page Inspector.</span></span>
> 
> <span data-ttu-id="5f57b-107">페이지 검사기는 Visual Studio에 브라우저 진단 도구를 제공 하 고 브라우저, ASP.NET 및 소스 코드 간에 통합된 된 환경을 제공 하는 새로운 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-107">Page Inspector is a new tool that brings browser diagnostics tools to Visual Studio and provides an integrated experience among the browser, ASP.NET, and source code.</span></span> <span data-ttu-id="5f57b-108">Visual Studio IDE 내에서 직접 웹 페이지 (HTML, Web Forms, ASP.NET MVC 또는 웹 페이지)를 렌더링 하 고 소스 코드와 출력 결과 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-108">It renders a web page (HTML, Web Forms, ASP.NET MVC, or Web Pages) directly within the Visual Studio IDE and lets you examine both the source code and the resulting output.</span></span> <span data-ttu-id="5f57b-109">페이지 검사기를 사용 하면 웹 사이트를 쉽게 분해 하 고, up, 처음부터 페이지를 빠르게 작성할 신속 하 게 문제를 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-109">Page Inspector enables you to easily decompose a website, rapidly build pages from the ground up, and quickly diagnose issues.</span></span>
> 
> <span data-ttu-id="5f57b-110">오늘날 여러 가지 ASP.NET MVC WebForms 등의 적절 한 시기에 유연 하 고 확장 가능한 웹 사이트를 생성 하는 웹 프레임 워크 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-110">Nowadays we have a number of Web frameworks that create flexible and scalable websites in a timely manner, such as ASP.NET MVC and WebForms.</span></span> <span data-ttu-id="5f57b-111">반면에 도달할 더 어려워지므로 IDE에서 템플릿 기반 페이지 및 동적 콘텐츠에 디자이너 뷰를 지원 하지 않으므로 페이지에는 문제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-111">On the other hand, it gets harder to find issues on the pages because the IDE does not support the designer view in template-based pages and dynamic content.</span></span> <span data-ttu-id="5f57b-112">따라서 이러한 타사 웹 사이트가 사용자에 게 표시 되는 방식을 보려면 브라우저에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-112">Therefore, these websites have to be opened in a browser to see how they appear to a user.</span></span>
> 
> <span data-ttu-id="5f57b-113">웹 개발자 외부 도구를 사용 하 여 브라우저에서 정기적으로 실행 하는 문제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-113">Web developers use external tools to find issues that regularly run in the browser.</span></span> <span data-ttu-id="5f57b-114">그런 다음 이러한 IDE 돌아가서 해결을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-114">Then, they return to the IDE and start fixing.</span></span> <span data-ttu-id="5f57b-115">이 전환 IDE, 브라우저 및 프로 파일링 도구, 비효율적일 수 있습니다 활동과 경우에 따라 새로운 배포 및 정리 하는 문제를 재현 하 려 할 때마다 캐시를 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-115">This back and forth activity among the IDE, the browser and the profiling tools can be inefficient, and sometimes requires a fresh deployment and cache cleaning each time you want to reproduce an issue.</span></span>
> 
> <span data-ttu-id="5f57b-116">페이지 검사기의 결합된 된 일련의 기능을 사용 하 여 두 장점 결합 하 여 웹 개발 (브라우저 도구) 클라이언트와 서버 (ASP.NET 및 소스 코드) 사이에서 간격이 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-116">Page Inspector bridges a gap in Web development between the client (browser tools) and the server (ASP.NET and source code) by bringing together the best of both worlds using a combined set of features.</span></span>
> 
> <span data-ttu-id="5f57b-117">페이지 검사기를 사용 하는 원본 파일 (서버 쪽 코드 포함)의 요소를 브라우저에 렌더링 하는 HTML 태그를 생성 해야 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-117">Using Page Inspector, you can see which elements in the source files (including server-side code) have produced the HTML markup to be rendered in the browser.</span></span> <span data-ttu-id="5f57b-118">페이지 검사기도 CSS 속성 및 브라우저에 바로 반영 되 변경 내용을 보려면 DOM 요소 특성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-118">Page Inspector also lets you modify CSS properties and DOM element attributes to see the changes reflected immediately in the browser.</span></span>
> 
> <span data-ttu-id="5f57b-119">이 실습 랩에서 페이지 검사기 기능 있습니다 안내 하 고 사용 하 여 웹 응용 프로그램의 문제를 해결 하도록 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-119">This hands-on lab will walk you through the Page Inspector features and show you how you can use them to fix issues in Web applications.</span></span> <span data-ttu-id="5f57b-120">**이 랩에서 비슷한 흐름을 사용 하 여 다양 한 기술을 대상으로 하지만 두 연습을 포함 합니다. ASP.NET MVC 개발자 인 경우에 따라 요소가 연습 두 WebForms 개발자에 따라 실행 중인 경우**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-120">**This lab contains two exercises using similar flows but targeting different technologies. If you are an ASP.NET MVC Developer, follow exercise one; if you are a WebForms developer follow exercise two**.</span></span>
> 
> <span data-ttu-id="5f57b-121">이 랩에서 원본 폴더에 제공 된 샘플 웹 응용 프로그램에 사소한 변경 내용을 적용 하 여 이전에 설명 된 새로운 기능 및 향상 된 기능을 통해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-121">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>
> 
> <span data-ttu-id="5f57b-122">모든 샘플 코드와 코드 조각을 웹 캠프 교육 키트에서 사용할 수에 포함 된 [ https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409 ](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-122">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>


<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="5f57b-123">목표</span><span class="sxs-lookup"><span data-stu-id="5f57b-123">Objectives</span></span>

<span data-ttu-id="5f57b-124">이 실습 랩에서 배웁니다 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="5f57b-124">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="5f57b-125">페이지 검사기를 사용 하 여 웹 사이트를 구성 해제</span><span class="sxs-lookup"><span data-stu-id="5f57b-125">Decompose a Web Site using Page Inspector</span></span>
- <span data-ttu-id="5f57b-126">검사 하 고 페이지 검사기로 CSS 스타일 변경 내용 미리 보기</span><span class="sxs-lookup"><span data-stu-id="5f57b-126">Inspect and preview CSS styles changes with Page Inspector</span></span>
- <span data-ttu-id="5f57b-127">검색 하 고 페이지 검사기를 사용 하 여 웹 페이지에서 문제 해결</span><span class="sxs-lookup"><span data-stu-id="5f57b-127">Detect and fix issues in your web pages using Page Inspector</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="5f57b-128">전제 조건</span><span class="sxs-lookup"><span data-stu-id="5f57b-128">Prerequisites</span></span>

<span data-ttu-id="5f57b-129">이 랩을 완료 하려면 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-129">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="5f57b-130">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) 하거나 그 보다 뛰어난 (읽기 [부록 A](#AppendixA) 설치 하는 방법에 대 한 지침은).</span><span class="sxs-lookup"><span data-stu-id="5f57b-130">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>
- <span data-ttu-id="5f57b-131">Internet Explorer 9 이상이</span><span class="sxs-lookup"><span data-stu-id="5f57b-131">Internet Explorer 9 or higher</span></span>

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="5f57b-132">연습</span><span class="sxs-lookup"><span data-stu-id="5f57b-132">Exercises</span></span>

<span data-ttu-id="5f57b-133">이 실습 랩에서 다음 연습에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-133">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="5f57b-134">연습 1: 페이지 검사기를 사용 하 여 ASP.NET MVC 프로젝트의</span><span class="sxs-lookup"><span data-stu-id="5f57b-134">Exercise 1: Using Page Inspector in ASP.NET MVC Projects</span></span>](#Exercise1)
2. [<span data-ttu-id="5f57b-135">연습 2: WebForms 프로젝트에서 페이지 검사기를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="5f57b-135">Exercise 2: Using Page Inspector in WebForms Projects</span></span>](#Exercise2)

> [!NOTE]
> <span data-ttu-id="5f57b-136">각 연습 시작 솔루션을 개별적으로 각 연습에 따라 할 수 있는 작업의 시작 폴더에 있는 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-136">Each exercise is accompanied by a starting solution, located in the Begin folder of the exercise, that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="5f57b-137">실행에 대 한 소스 코드에서 해당 연습에서 단계를 완료 한 결과인 코드와 함께 Visual Studio 솔루션을 포함 하는 최종 폴더를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-137">Inside the source code for an exercise, you will also find an End folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="5f57b-138">이 실습 랩에서 진행할 때는 추가 도움이 필요한 경우 이러한 솔루션 가이드로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-138">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>


<span data-ttu-id="5f57b-139">예상 소요 시간: **30 분**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-139">Estimated time to complete this lab: **30 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Using_Page_Inspector_in_ASPNET_MVC_Projects"></a>
### <a name="exercise-1-using-page-inspector-in-aspnet-mvc-projects"></a><span data-ttu-id="5f57b-140">연습 1: 페이지 검사기를 사용 하 여 ASP.NET MVC 프로젝트의</span><span class="sxs-lookup"><span data-stu-id="5f57b-140">Exercise 1: Using Page Inspector in ASP.NET MVC Projects</span></span>

<span data-ttu-id="5f57b-141">이 연습에서는 미리 보기 및 디버그 하는 방법을 배우게 됩니다는 **ASP.NET MVC 4** 사용 하 여 솔루션 **페이지 검사기**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-141">In this exercise, you will learn how to preview and debug an **ASP.NET MVC 4** solution using **Page Inspector**.</span></span> <span data-ttu-id="5f57b-142">첫째, 웹 디버깅 프로세스를 용이 하 게 하는 기능에 알아보려면이 도구는 간략 한 및을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-142">First, you will perform a brief lap around the tool to learn the features that facilitate the Web debugging process.</span></span> <span data-ttu-id="5f57b-143">그런 다음 스타일 문제를 포함 하는 웹 페이지에서 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-143">Then, you will work in a web page that contains styling issues.</span></span> <span data-ttu-id="5f57b-144">페이지 검사기를 사용 하 여 문제를 생성 하는 소스 코드를 찾을 하 고 해결 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-144">You will learn how to use Page Inspector to find the source code that generates the issue and fix it.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a><span data-ttu-id="5f57b-145">작업 1-탐색 페이지 검사기</span><span class="sxs-lookup"><span data-stu-id="5f57b-145">Task 1 - Exploring Page Inspector</span></span>

<span data-ttu-id="5f57b-146">이 태스크에서는 페이지 검사기 사진 갤러리를 표시 하는 ASP.NET MVC 4 프로젝트의 컨텍스트에서 사용 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-146">In this task, you will learn how to use the Page Inspector in the context of an ASP.NET MVC 4 project that shows a photo gallery.</span></span>

1. <span data-ttu-id="5f57b-147">열기는 **시작** 솔루션에 있는 **소스/e x 1-MVC4/시작/** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-147">Open the **Begin** solution located at **Source/Ex1-MVC4/Begin/** folder.</span></span>

   1. <span data-ttu-id="5f57b-148">일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 전에 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-148">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="5f57b-149">이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-149">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="5f57b-150">에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="5f57b-150">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="5f57b-151">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-151">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="5f57b-152">NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-152">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="5f57b-153">NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-153">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="5f57b-154">이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-154">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="5f57b-155">솔루션 탐색기에서 찾을 **Index.cshtml** 뷰에 **/뷰/홈** 폴더를 프로젝트 마우스 오른쪽 단추로 클릭 한 다음 선택 **페이지 검사기에서 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-155">In the Solution Explorer, locate **Index.cshtml** view under the **/Views/Home** project folder, right-click it and select **View in Page Inspector**.</span></span>

    <span data-ttu-id="5f57b-156">![페이지 검사기에서 미리 보기 위해 파일을 선택 하면](using-page-inspector-in-visual-studio-2012/_static/image1.png "페이지 검사기에서 미리 보기 위해 파일을 선택 하면")</span><span class="sxs-lookup"><span data-stu-id="5f57b-156">![Selecting a file to preview in Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image1.png "Selecting a file to preview in Page Inspector")</span></span>

    <span data-ttu-id="5f57b-157">*페이지 검사기에서 미리 보기 위해 파일을 선택 하면*</span><span class="sxs-lookup"><span data-stu-id="5f57b-157">*Selecting a file to preview in Page Inspector*</span></span>
3. <span data-ttu-id="5f57b-158">페이지 검사기 창에 표시 됩니다는 */Home/Index* 소스 선택한 뷰에 매핑되는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-158">The Page Inspector window will show the */Home/Index* URL mapped to the source View you selected.</span></span>

    ![ThefirstcontactwithPageInspector](using-page-inspector-in-visual-studio-2012/_static/image2.png)

    <span data-ttu-id="5f57b-160">*페이지 검사기를 사용 하 여 첫 번째 연락처*</span><span class="sxs-lookup"><span data-stu-id="5f57b-160">*The first contact with Page Inspector*</span></span>

    <span data-ttu-id="5f57b-161">페이지 검사기 도구는 Visual Studio 환경에 통합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-161">The Page Inspector tool is integrated in your Visual Studio environment.</span></span> <span data-ttu-id="5f57b-162">검사기 내장된 브라우저, 강력한 HTML 프로파일러 함께 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-162">The inspector contains an embedded browser, together with a powerful HTML profiler.</span></span> <span data-ttu-id="5f57b-163">확인 페이지에 표시 되는 모양을 보려면 솔루션을 실행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-163">Notice that you do not have to run the solution to see how your pages look.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5f57b-164">페이지 검사기 브라우저의 너비는이 페이지의 너비 보다 작은 경우 표시 되지 않습니다 페이지 제대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-164">When the width of Page Inspector browser is less than the width of the opened page, you will not see the page properly.</span></span> <span data-ttu-id="5f57b-165">이 경우 페이지 검사기의 너비를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-165">If that happens, adjust the width of the Page Inspector.</span></span>
4. <span data-ttu-id="5f57b-166">클릭는 **파일** 페이지 검사기의 탭에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-166">Click the **Files** tab in Page Inspector.</span></span>

    <span data-ttu-id="5f57b-167">인덱스 페이지를 작성 하는 모든 소스 파일에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-167">You will see all the source files that are composing the Index page.</span></span> <span data-ttu-id="5f57b-168">이 기능은 부분 뷰 및 템플릿을 사용 하 여 작업할 때 특히 한 눈에 모든 요소를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-168">This feature helps to identify all the elements at a glance, especially when you are working with partial views and templates.</span></span> <span data-ttu-id="5f57b-169">또한 열 수 각 파일의 링크를 클릭 하는 경우를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-169">Notice that you can also open each of the files if you click the links.</span></span>

    ![파일 탭](using-page-inspector-in-visual-studio-2012/_static/image3.png)

    <span data-ttu-id="5f57b-171">*파일 탭*</span><span class="sxs-lookup"><span data-stu-id="5f57b-171">*The Files tab*</span></span>
5. <span data-ttu-id="5f57b-172">클릭는 **검사 모드를 설정/해제** 탭의 왼쪽에 있는 단추를 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-172">Click the **Toggle Inspection Mode** button, located at the left of the tabs.</span></span>

    <span data-ttu-id="5f57b-173">이 도구는 페이지의 모든 요소를 선택 하 고 HTML 및 Razor 코드를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-173">This tool will let you select any element of the page and see its HTML and Razor code.</span></span>

    ![검사 모드 단추 설정/해제](using-page-inspector-in-visual-studio-2012/_static/image4.png)

    <span data-ttu-id="5f57b-175">*토글 검사 모드 단추*</span><span class="sxs-lookup"><span data-stu-id="5f57b-175">*Toggle Inspection Mode button*</span></span>
6. <span data-ttu-id="5f57b-176">페이지 검사기 브라우저에서 페이지 요소 위로 마우스 포인터를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-176">In the Page Inspector browser, move the mouse pointer over the page elements.</span></span> <span data-ttu-id="5f57b-177">렌더링된 된 페이지 부분 위로 마우스 포인터를 이동 하는 동안 요소 형식이 표시 되 고 해당 소스 태그 또는 코드가 Visual Studio 편집기에서 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-177">While you move the mouse pointer over any part of the rendered page, the element type is displayed and the corresponding source markup or code is highlighted in the Visual Studio editor.</span></span>

    ![Inspectionmodeinaction](using-page-inspector-in-visual-studio-2012/_static/image5.png)

    <span data-ttu-id="5f57b-179">*작업에서 검사 모드*</span><span class="sxs-lookup"><span data-stu-id="5f57b-179">*Inspection mode in action*</span></span>

    > [!NOTE]
    > <span data-ttu-id="5f57b-180">페이지 검사기 창을 최대화 하지 않는 또는 소스 코드를 보여 주는 미리 보기 탭을 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-180">Do not maximize the Page Inspector window or you will not be able to see the preview tab showing the source code.</span></span> <span data-ttu-id="5f57b-181">가 최대화 될 때 페이지 검사기에 요소를 클릭 하면 선택 항목의 소스 코드는 표시 되지만 페이지 검사기 창이 숨겨집니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-181">If you click the element in Page Inspector when it is maximized, the source code of the selection will appear but it will hide the Page Inspector window.</span></span>

    <span data-ttu-id="5f57b-182">에 주의 해야 하는 경우는 **Index.cshtml** 파일을 선택 된 요소를 생성 하는 소스 코드의 부분을 강조 표시 되어 있는지을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-182">If you pay attention to the **Index.cshtml** file, you will notice that the portion of source code that generates the selected element is highlighted.</span></span> <span data-ttu-id="5f57b-183">이 기능은 코드에 액세스 하는 직접 및 빠른 방법을 제공 하 긴 소스 파일을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-183">This feature facilitates the editing of long source files, providing a direct and fast way to access the code.</span></span>

    ![Inspectingelements](using-page-inspector-in-visual-studio-2012/_static/image6.png)

    <span data-ttu-id="5f57b-185">*요소를 검사합니다.*</span><span class="sxs-lookup"><span data-stu-id="5f57b-185">*Inspecting elements*</span></span>
7. <span data-ttu-id="5f57b-186">클릭는 **검사 모드를 설정/해제** 단추 (![페이지 검사기 브라우저에서 렌더링 된 HTML 코드를 표시 하려면 HTML 탭을 선택 합니다.] (using-page-inspector-in-visual-studio-2012/_static/image7.png "페이지 검사기 브라우저에서 렌더링 된 HTML 코드를 표시 하려면 HTML 탭을 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="5f57b-186">Click the **Toggle Inspection Mode** button (![Select the HTML tab to display the HTML code rendered in the Page Inspector browser.](using-page-inspector-in-visual-studio-2012/_static/image7.png "Select the HTML tab to display the HTML code rendered in the Page Inspector browser.")</span></span> <span data-ttu-id="5f57b-187">)를 커서를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-187">) to disable the cursor.</span></span>
8. <span data-ttu-id="5f57b-188">선택 된 **HTML** 탭 페이지 검사기 브라우저에서 렌더링 된 HTML 코드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-188">Select the **HTML** tab to display the HTML code rendered in the Page Inspector browser.</span></span>
9. <span data-ttu-id="5f57b-189">HTML 태그에서 Koala 링크와 목록 항목을 찾아 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-189">In the HTML markup, locate the list item with the Koala link and select it.</span></span>

    <span data-ttu-id="5f57b-190">코드를 선택 하면 해당 출력은 자동으로 강조 표시 되어 있는지 브라우저에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-190">Notice that when you select the code, the corresponding output is automatically highlighted in the browser.</span></span> <span data-ttu-id="5f57b-191">이 기능은 미리 HTML 블록 페이지에 렌더링 되는 방식을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-191">This feature is useful to see how an HTML block is rendered on the page.</span></span>

    <span data-ttu-id="5f57b-192">![페이지의 HTML 요소를 선택 하면](using-page-inspector-in-visual-studio-2012/_static/image8.png "페이지의 HTML을 선택 하면 요소")</span><span class="sxs-lookup"><span data-stu-id="5f57b-192">![Selecting HTML element in the page](using-page-inspector-in-visual-studio-2012/_static/image8.png "Selecting HTML element in the page")</span></span>

    <span data-ttu-id="5f57b-193">*페이지의 HTML 요소를 선택합니다.*</span><span class="sxs-lookup"><span data-stu-id="5f57b-193">*Selecting HTML element in the page*</span></span>
10. <span data-ttu-id="5f57b-194">클릭는 **검사 모드를 설정/해제** 사용할 수 있도록 단추 *검사 모드* 탐색 모음을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-194">Click the **Toggle Inspection Mode** button to enable *Inspection Mode* and click the navigation bar.</span></span> <span data-ttu-id="5f57b-195">오른쪽의 HTML 코드의 스타일 창에서 선택한 요소에 적용 된 CSS 스타일으로 목록이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-195">On the right of the HTML code, in the Styles pane, you will see a list with the CSS styles applied to the selected element.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5f57b-196">페이지 검사기는 또한 열지 헤더 사이트 레이아웃에 포함 되므로 \_Layout.cshtml 파일 및 코드의 세그먼트에 영향을 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-196">Since the header is a part of the site layout, Page Inspector will also open \_Layout.cshtml file and highlight the segment of code affected.</span></span>

    ![Discoveringstyles](using-page-inspector-in-visual-studio-2012/_static/image9.png)

    <span data-ttu-id="5f57b-198">*스타일 및 선택 된 요소의 소스 파일 검색*</span><span class="sxs-lookup"><span data-stu-id="5f57b-198">*Discovering styles and source files of a selected element*</span></span>
11. <span data-ttu-id="5f57b-199">토글 검사 포인터를 사용 하도록 설정 기능 갖춘된 파란색 막대 아래 마우스 포인터를 이동 하 고 절반 원을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-199">With the toggle inspection pointer enabled, move the mouse pointer below the blue featured bar and click the half circle.</span></span>

    <span data-ttu-id="5f57b-200">![요소 선택](using-page-inspector-in-visual-studio-2012/_static/image10.png "요소 선택")</span><span class="sxs-lookup"><span data-stu-id="5f57b-200">![Selecting an element](using-page-inspector-in-visual-studio-2012/_static/image10.png "Selecting an element")</span></span>

    <span data-ttu-id="5f57b-201">*요소 선택*</span><span class="sxs-lookup"><span data-stu-id="5f57b-201">*Selecting an element*</span></span>
12. <span data-ttu-id="5f57b-202">스타일 창에서 찾습니다는 **배경 이미지** 항목 아래에서 **.main 콘텐츠** 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-202">In the Styles pane, locate the **background-image** item under the **.main-content** group.</span></span> <span data-ttu-id="5f57b-203">**선택을 취소** 는 **배경 이미지** 를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-203">**Uncheck** the **background-image** and see what happens.</span></span> <span data-ttu-id="5f57b-204">브라우저는 변경 내용이 즉시 반영 됩니다 및 원 숨겨지는지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-204">You will notice that the browser will reflect the changes immediately and the circle is hidden.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5f57b-205">페이지 검사기 스타일 탭에 적용 하면 변경 내용이 원래 스타일 시트는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-205">The changes you apply on the Page Inspector Styles tab do not affect the original stylesheet.</span></span> <span data-ttu-id="5f57b-206">스타일을 선택 취소 하거나 원하는 하지만 페이지를 새로 고친 후 복원 됩니다 만큼 여러 번 해당 값을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-206">You can uncheck styles or change their values as many times as you want, but they will be restored after refreshing the page.</span></span>

    <span data-ttu-id="5f57b-207">![CSS 스타일을 설정 하거나 해제](using-page-inspector-in-visual-studio-2012/_static/image11.png "활성화 및 CSS 스타일 사용 안 함")</span><span class="sxs-lookup"><span data-stu-id="5f57b-207">![Enabling and disabling CSS styles](using-page-inspector-in-visual-studio-2012/_static/image11.png "Enabling and disabling CSS styles")</span></span>

    <span data-ttu-id="5f57b-208">*사용 하도록 설정 및 CSS 스타일 사용 안 함*</span><span class="sxs-lookup"><span data-stu-id="5f57b-208">*Enabling and disabling CSS styles*</span></span>
13. <span data-ttu-id="5f57b-209">이제 클릭는 '**사용자 로고는 여기**' 검사 모드를 사용 하 여 헤더에는 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-209">Now, click the '**your logo here**' text on the header using the inspection mode.</span></span>
14. <span data-ttu-id="5f57b-210">에 **스타일** 탭에서 찾을 **글꼴 크기** CSS 특성에서 **.site 제목** 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-210">In the **Styles** tab, locate the **font-size** CSS attribute under the **.site-title** group.</span></span> <span data-ttu-id="5f57b-211">특성 값을 두 번 클릭 하 고 2.3 em 값을 바꿀 내용 **3 em**, 누릅니다 **ENTER**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-211">Double-click the attribute value and replace the 2.3 em value with **3 em**, and then press **ENTER**.</span></span> <span data-ttu-id="5f57b-212">제목 큰 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-212">Notice that the title looks bigger.</span></span>

    <span data-ttu-id="5f57b-213">![페이지 검사기의 CSS 값을 변경](using-page-inspector-in-visual-studio-2012/_static/image12.png "페이지 검사기에 CSS 변경 값")</span><span class="sxs-lookup"><span data-stu-id="5f57b-213">![Changing CSS values in the Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image12.png "Changing CSS values in the Page Inspector")</span></span>

    <span data-ttu-id="5f57b-214">*페이지 검사기의 CSS 값 변경*</span><span class="sxs-lookup"><span data-stu-id="5f57b-214">*Changing CSS values in the Page Inspector*</span></span>
15. <span data-ttu-id="5f57b-215">클릭는 **스타일 추적** 페이지 검사기의 오른쪽 창에 있는 탭입니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-215">Click the **Trace Styles** tab, located in the right pane of Page Inspector.</span></span> <span data-ttu-id="5f57b-216">이것이 특성 이름으로 정렬 된 선택 항목에 적용 되는 모든 스타일을 참조 하는 대체 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-216">This is an alternative way to see all the styles applied to the selection, ordered by attribute name.</span></span>

    ![CSSstylestracing](using-page-inspector-in-visual-studio-2012/_static/image13.png)

    <span data-ttu-id="5f57b-218">*선택 된 요소의 CSS 스타일 추적*</span><span class="sxs-lookup"><span data-stu-id="5f57b-218">*CSS styles tracing of the selected element*</span></span>
16. <span data-ttu-id="5f57b-219">페이지 검사기의 다른 기능에는 레이아웃 창입니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-219">Another feature of Page Inspector is the Layout pane.</span></span> <span data-ttu-id="5f57b-220">탐색 모음을 선택한 다음 클릭 검사 모드를 사용 하 여 **레이아웃** 오른쪽 창에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-220">Using the inspection mode, select the navigation bar and then click the **Layout** tab on the right pane.</span></span> <span data-ttu-id="5f57b-221">선택한 창의 정확한 크기와 오프셋, 여백, 안쪽 여백 및 테두리 크기가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-221">You will see the exact size of the selected element, as well as its offset, margin, padding and border size.</span></span> <span data-ttu-id="5f57b-222">이 보기에서 값을 수정할 수도 수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-222">Notice that you can also modify the values from this view.</span></span>

    <span data-ttu-id="5f57b-223">![페이지 검사기에서 요소 레이아웃](using-page-inspector-in-visual-studio-2012/_static/image14.png "페이지 검사기에서 요소 레이아웃")</span><span class="sxs-lookup"><span data-stu-id="5f57b-223">![Element layout in Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image14.png "Element layout in Page Inspector")</span></span>

    <span data-ttu-id="5f57b-224">*페이지 검사기에서 요소 레이아웃*</span><span class="sxs-lookup"><span data-stu-id="5f57b-224">*Element layout in Page Inspector*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a><span data-ttu-id="5f57b-225">작업 2-확인 및 사진 갤러리 스타일 문제 수정</span><span class="sxs-lookup"><span data-stu-id="5f57b-225">Task 2 - Finding and Fixing Style Issues in the Photo Gallery</span></span>

<span data-ttu-id="5f57b-226">이전 버전의 Visual Studio 웹 페이지 문제를 진단할 어떻게는?</span><span class="sxs-lookup"><span data-stu-id="5f57b-226">How would you diagnose Web pages issues with previous versions of Visual Studio?</span></span> <span data-ttu-id="5f57b-227">Internet Explorer의 도구 개발자 또는 Firebug와 같은 Visual Studio IDE 외부에서 실행 되는 도구를 디버깅 하는 웹 익숙할 것 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-227">You are likely familiar with web debugging tools that run outside the Visual Studio IDE, like Internet Explorer Developer Tools or Firebug.</span></span> <span data-ttu-id="5f57b-228">브라우저에 HTML, 이해 스크립팅 및 스타일, 기본 프레임 워크는 렌더링할 HTML을 생성 하는 동안 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-228">Browsers only understand HTML, scripting and styles, while an underlying framework generates the HTML that will be rendered.</span></span> <span data-ttu-id="5f57b-229">이런 이유로 전체 사이트와 같은 웹 페이지의 모양을 확인를 배포 해야 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-229">For that reason, you often need to deploy the whole site to see how web pages look like.</span></span>

<span data-ttu-id="5f57b-230">아마도 검색 하 고 웹 사이트에서 문제를 해결 하려는 경우 다음이 단계를 따라 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-230">You had probably followed these steps when you wanted to detect and fix an issue in your web site:</span></span>

1. <span data-ttu-id="5f57b-231">Visual Studio에서 솔루션을 실행 하거나 웹 서버에서 페이지를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-231">Run the Solution from Visual Studio, or deploy the page on the web server.</span></span>
2. <span data-ttu-id="5f57b-232">브라우저에서 사용 하 여, 또는 단순히 소스 코드와 스타일을 열고 문제를 일치 시 키 려 개발자 도구를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-232">In the browser, open the developer tools you use, or simply open the source code and the styles and try to match the issue.</span></span> <span data-ttu-id="5f57b-233">관련 된 파일을 찾을 사용 했을 것은 &quot;검색&quot; 또는 &quot;파일에서 검색&quot; 스타일 클래스의 이름으로는 기능.</span><span class="sxs-lookup"><span data-stu-id="5f57b-233">To find the files involved, you would have used the &quot;Search&quot; or &quot;Search in files&quot; features with the name of the style classes.</span></span>
3. <span data-ttu-id="5f57b-234">오류가 감지 되 면 웹 브라우저와 서버를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-234">Once the error is detected, stop the Web browser and the server.</span></span>
4. <span data-ttu-id="5f57b-235">브라우저 캐시를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-235">Clear the browser cache.</span></span>
5. <span data-ttu-id="5f57b-236">수정 프로그램을 적용 하려면 Visual Studio로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-236">Return to Visual Studio to apply a fix.</span></span> <span data-ttu-id="5f57b-237">테스트 하는 모든 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-237">Repeat all the steps to test.</span></span>

<span data-ttu-id="5f57b-238">ASP.NET MVC 4의 없는 실제 WYSIWYG 그대로 스타일 문제를 대부분 실행 하거나 웹 응용 프로그램을 배포한 후에 이후 단계에서 검색 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-238">As there is no real WYSIWYG in ASP.NET MVC 4, most of the style issues are detected on a later stage, after running or deploying the web application.</span></span> <span data-ttu-id="5f57b-239">이제 페이지 검사기 이므로 솔루션을 실행 하지 않고 모든 페이지를 미리 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-239">Now, with Page Inspector, it is possible to preview any page without running the solution.</span></span>

<span data-ttu-id="5f57b-240">이 태스크에서는 페이지 검사기를 사용 하 여 쿼리하고 사진 갤러리 응용 프로그램의 몇 가지 문제를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-240">In this task, you will use the Page inspector and fix some issues the Photo Gallery application.</span></span>

1. <span data-ttu-id="5f57b-241">페이지 검사기를 사용 하 여 찾습니다는 **등록** 및 **로그인** 머리글의 왼쪽에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-241">Using Page Inspector, locate the **Register** and the **Log in** links at the left side of the header.</span></span>

    <span data-ttu-id="5f57b-242">링크의 오른쪽에 예상된 위치에 표시 되지 않습니다는 글머리 기호 목록 처럼 표시 된에 유의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="5f57b-242">Notice that the links are not displayed at the expected place on the right, and they are shown like a bulleted list.</span></span> <span data-ttu-id="5f57b-243">이제 오른쪽에 대 한 링크를 정렬 하 고 스타일을 다시 지정을 적절 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-243">You will now align the links to the right and restyle them accordingly.</span></span>

    <span data-ttu-id="5f57b-244">![링크에서 레지스터 및 로그 찾기](using-page-inspector-in-visual-studio-2012/_static/image15.png "링크에서 레지스터 및 로그 찾기")</span><span class="sxs-lookup"><span data-stu-id="5f57b-244">![Locating the Register and Log in links](using-page-inspector-in-visual-studio-2012/_static/image15.png "Locating the Register and Log in links")</span></span>

    <span data-ttu-id="5f57b-245">*링크에서 레지스터 및 로그 찾기*</span><span class="sxs-lookup"><span data-stu-id="5f57b-245">*Locating the Register and Log in links*</span></span>
2. <span data-ttu-id="5f57b-246">선택한 검사 모드를 설정/해제를 사용 닫기를는 없지만, 해당 코드를 열려는 레지스터 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-246">With Toggle Inspection Mode selected, click close to, but not on, the Register link to open its code.</span></span>

    <span data-ttu-id="5f57b-247">링크의 소스 코드에 있는 공지는  **\_LoginPartial.cshtml** 파일, Index.cshtml 하지와 \_Layout.cshtml는는 첫 번째 위치에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-247">Notice that the source code of the links is located in the **\_LoginPartial.cshtml** file, not the Index.cshtml nor the \_Layout.cshtml, which are the places you might look in first place.</span></span> <span data-ttu-id="5f57b-248">올바른 소스 파일에서 직접 넣었습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-248">You have been placed directly in the correct source file.</span></span>
3. <span data-ttu-id="5f57b-249">에 **스타일** 탭을 찾아서 클릭는 **<section> #login</section>** 항목 이러한 링크에 대 한 HTML 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-249">In the **Styles** tab, locate and click the **<section> #login</section>** item, which is the HTML container for these links.</span></span>

    <span data-ttu-id="5f57b-250">다음에 유의 **#login** 스타일에 있는 자동으로 **Site.css** 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-250">Notice that the **#login** style is automatically located in **Site.css** after you click.</span></span> <span data-ttu-id="5f57b-251">또한 코드는 이제 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-251">Moreover, the code is now highlighted.</span></span>

    <span data-ttu-id="5f57b-252">![CSS 스타일을 선택 하면](using-page-inspector-in-visual-studio-2012/_static/image16.png "CSS 스타일 선택")</span><span class="sxs-lookup"><span data-stu-id="5f57b-252">![Selecting the CSS styles](using-page-inspector-in-visual-studio-2012/_static/image16.png "Selecting the CSS styles")</span></span>

    <span data-ttu-id="5f57b-253">*CSS 스타일을 선택 하면*</span><span class="sxs-lookup"><span data-stu-id="5f57b-253">*Selecting the CSS styles*</span></span>
4. <span data-ttu-id="5f57b-254">주석 처리 제거는 **-** 강조 표시 된 코드에서 여는 태그와 닫는 문자를 제거 하 여 특성을 저장할는 **Site.css** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-254">Uncomment the **text-align** attribute in the highlighted code by removing the opening and closing characters and save the **Site.css** file.</span></span>

    <span data-ttu-id="5f57b-255">페이지 검사기를 현재 페이지를 구성 하는 다른 모든 파일의 인식 하며 이러한 파일을 변경 하는 경우를 감지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-255">Page Inspector is aware of all the different files that compose the current page, and it can detect when any of these files change.</span></span> <span data-ttu-id="5f57b-256">브라우저에서 현재 페이지 원본 파일과 함께 동기화 되지 않았습니다. 때마다 경우 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-256">It alerts you whenever the current page in browser is not in sync with the source files.</span></span>
5. <span data-ttu-id="5f57b-257">페이지 검사기 브라우저에서 페이지를 다시 로드 하려면 주소 표시줄 아래에 있는 막대를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-257">In the Page Inspector browser, click the bar located below the address bar to reload the page.</span></span>

    ![페이지를 다시 로드](using-page-inspector-in-visual-studio-2012/_static/image17.png)

    <span data-ttu-id="5f57b-259">*페이지를 다시 로드*</span><span class="sxs-lookup"><span data-stu-id="5f57b-259">*Reloading the page*</span></span>

    <span data-ttu-id="5f57b-260">오른쪽에 있는 링크는 이제 하지만 여전히 글머리 기호 목록 처럼 보입니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-260">The links are now at the right, but they still look like a bulleted list.</span></span> <span data-ttu-id="5f57b-261">이제 글머리 기호를 제거 및 링크를 가로 방향으로 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-261">Now, you will remove the bullets and align the links horizontally.</span></span>

    ![업데이트 페이지](using-page-inspector-in-visual-studio-2012/_static/image18.png)

    <span data-ttu-id="5f57b-263">*업데이트 페이지*</span><span class="sxs-lookup"><span data-stu-id="5f57b-263">*Updated page*</span></span>
6. <span data-ttu-id="5f57b-264">검사 모드를 사용 하 여 중 하나를 선택는 **&lt;li&gt;** 포함 된 항목의 &quot;등록&quot; 및 &quot;로그인&quot; 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-264">Using the inspection mode, select any of the **&lt;li&gt;** items that contain the &quot;Register&quot; and &quot;Log in&quot; links.</span></span> <span data-ttu-id="5f57b-265">클릭는  **&lt;섹션&gt; #login** 항목의 액세스 **Styles.css** 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-265">Then, click the **&lt;section&gt; #login** item to access **Styles.css** code.</span></span>

    <span data-ttu-id="5f57b-266">![스타일 찾기](using-page-inspector-in-visual-studio-2012/_static/image19.png "스타일 찾기")</span><span class="sxs-lookup"><span data-stu-id="5f57b-266">![Finding the style](using-page-inspector-in-visual-studio-2012/_static/image19.png "Finding the style")</span></span>

    <span data-ttu-id="5f57b-267">*스타일 찾기*</span><span class="sxs-lookup"><span data-stu-id="5f57b-267">*Finding the style*</span></span>
7. <span data-ttu-id="5f57b-268">**Style.css**에 대 한 코드를 주석 처리 제거 **#login li** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-268">In **Style.css**, uncomment the code for **#login li** items.</span></span> <span data-ttu-id="5f57b-269">추가 하는 스타일 글머리 기호 숨기고 항목 가로로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-269">The style you are adding will hide the bullet and display the items horizontally.</span></span>

    <span data-ttu-id="5f57b-270">![로그인 링크 스타일 재설정](using-page-inspector-in-visual-studio-2012/_static/image20.png "스타일의 로그인 링크를 재설정")</span><span class="sxs-lookup"><span data-stu-id="5f57b-270">![Restyling the login links](using-page-inspector-in-visual-studio-2012/_static/image20.png "Restyling the login links")</span></span>

    <span data-ttu-id="5f57b-271">*로그인 링크 스타일 재설정*</span><span class="sxs-lookup"><span data-stu-id="5f57b-271">*Restyling the login links*</span></span>
8. <span data-ttu-id="5f57b-272">저장 **Style.css** 파일 및 페이지를 다시 로드 하는 주소 아래에 있는 표시줄에 한 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-272">Save **Style.css** file and click once on the bar located below the address to reload the page.</span></span> <span data-ttu-id="5f57b-273">링크는 올바르게 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-273">Notice that the links appear correctly.</span></span>

    <span data-ttu-id="5f57b-274">![오른쪽으로 정렬 하는 링크](using-page-inspector-in-visual-studio-2012/_static/image21.png "오른쪽으로 정렬 하는 링크")</span><span class="sxs-lookup"><span data-stu-id="5f57b-274">![Links aligned to the right side](using-page-inspector-in-visual-studio-2012/_static/image21.png "Links aligned to the right side")</span></span>

    <span data-ttu-id="5f57b-275">*오른쪽으로 정렬 하는 링크*</span><span class="sxs-lookup"><span data-stu-id="5f57b-275">*Links aligned to the right side*</span></span>
9. <span data-ttu-id="5f57b-276">마지막으로, 머리글 제목을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-276">Finally, you will change the header title.</span></span> <span data-ttu-id="5f57b-277">검사 모드를 사용 하 여 클릭 하 여 **사용자 로고는 여기** 텍스트 및 get을 생성 하는 소스 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-277">Use the inspection mode to click **your logo here** text and get to the source code that generates it.</span></span>
10. <span data-ttu-id="5f57b-278">에 이제  **\_Layout.cshtml**, 대체 '**사용자 로고는 여기**'텍스트와 '**사진 갤러리**'.</span><span class="sxs-lookup"><span data-stu-id="5f57b-278">Now you are in **\_Layout.cshtml**, replace '**your logo here**' text with '**Photo Gallery**'.</span></span> <span data-ttu-id="5f57b-279">저장 하 고 페이지 검사기 브라우저를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-279">Save and update the Page Inspector browser.</span></span>

    <span data-ttu-id="5f57b-280">![새 제목을 할당](using-page-inspector-in-visual-studio-2012/_static/image22.png "새 제목을 할당")</span><span class="sxs-lookup"><span data-stu-id="5f57b-280">![Assigning a new title](using-page-inspector-in-visual-studio-2012/_static/image22.png "Assigning a new title")</span></span>

    <span data-ttu-id="5f57b-281">*새 제목을 할당*</span><span class="sxs-lookup"><span data-stu-id="5f57b-281">*Assigning a new title*</span></span>

    ![PhotoGallerypage](using-page-inspector-in-visual-studio-2012/_static/image23.png)

    <span data-ttu-id="5f57b-283">*업데이트 사진 갤러리 페이지*</span><span class="sxs-lookup"><span data-stu-id="5f57b-283">*Photo Gallery page updated*</span></span>
11. <span data-ttu-id="5f57b-284">마지막으로, 선택은 **PhotoGallery** 프로젝트 및 키를 눌러 **F5** 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-284">Finally, selet the **PhotoGallery** project and press **F5** to run the app.</span></span> <span data-ttu-id="5f57b-285">모든 체크 아웃 변경 내용이 예상 대로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-285">Check out all the changes work as expected.</span></span>

* * *

<a id="Exercise2"></a>

<a id="Exercise_2_Using_Page_Inspector_in_WebForms_Projects"></a>
### <a name="exercise-2-using-page-inspector-in-webforms-projects"></a><span data-ttu-id="5f57b-286">연습 2: WebForms 프로젝트에서 페이지 검사기를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="5f57b-286">Exercise 2: Using Page Inspector in WebForms Projects</span></span>

<span data-ttu-id="5f57b-287">이 연습에서는 미리 보기 및 페이지 검사기를 사용 하 여 WebForms 솔루션을 디버그 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-287">In this exercise, you will learn how to preview and debug a WebForms solution using Page Inspector.</span></span> <span data-ttu-id="5f57b-288">웹 프로세스를 디버깅을 용이 하 게 하는 페이지 검사기 기능에 알아보려면 도구 관련 간략 한 랩을 먼저 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-288">You will first perform a brief lap around the tool to learn the Page Inspector features that facilitate the Web debugging process.</span></span> <span data-ttu-id="5f57b-289">그런 다음 스타일 문제를 포함 하는 웹 페이지에서 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-289">Then, you will work in a web page that contains styling issues.</span></span> <span data-ttu-id="5f57b-290">페이지 검사기를 사용 하 여 문제를 생성 하는 소스 코드를 찾을 하 고 해결 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-290">You will learn how to use Page Inspector to find the source code that generates the issue and fix it.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a><span data-ttu-id="5f57b-291">작업 1-탐색 페이지 검사기</span><span class="sxs-lookup"><span data-stu-id="5f57b-291">Task 1 - Exploring Page Inspector</span></span>

<span data-ttu-id="5f57b-292">이 태스크에서는 사진 갤러리를 보여 주는 WebForms 프로젝트의 컨텍스트에서 페이지 검사기 기능을 사용 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-292">In this task, you will learn how to use the Page Inspector features in the context of a WebForms project that shows a photo gallery.</span></span>

1. <span data-ttu-id="5f57b-293">열기는 **시작** 솔루션에 있는 **소스/e x 2-WebForms/시작/** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-293">Open the **Begin** solution located at **Source/Ex2-WebForms/Begin/** folder.</span></span>

   1. <span data-ttu-id="5f57b-294">일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 전에 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-294">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="5f57b-295">이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-295">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="5f57b-296">에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="5f57b-296">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="5f57b-297">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-297">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="5f57b-298">NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-298">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="5f57b-299">NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-299">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="5f57b-300">이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-300">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="5f57b-301">솔루션 탐색기에서 찾아 **Default.aspx** 페이지 마우스 오른쪽 단추로 클릭 한 다음 선택 **페이지 검사기에서 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-301">In the Solution Explorer, locate **Default.aspx** page, right-click it and select **View in Page Inspector**.</span></span>

    <span data-ttu-id="5f57b-302">![Default.aspx 페이지 검사기를 사용 하 여 열기](using-page-inspector-in-visual-studio-2012/_static/image24.png "Default.aspx 페이지 검사기를 사용 하 여 열기")</span><span class="sxs-lookup"><span data-stu-id="5f57b-302">![Opening Default.aspx with Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image24.png "Opening Default.aspx with Page Inspector")</span></span>

    <span data-ttu-id="5f57b-303">*페이지 검사기로 열기 Default.aspx*</span><span class="sxs-lookup"><span data-stu-id="5f57b-303">*Opening Default.aspx with Page Inspector*</span></span>
3. <span data-ttu-id="5f57b-304">페이지 검사기 창에는 Default.aspx 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-304">The Page Inspector window will show Default.aspx.</span></span>

    <span data-ttu-id="5f57b-305">![Default.aspx 페이지 검사기에서 보기](using-page-inspector-in-visual-studio-2012/_static/image25.png "Default.aspx 페이지 검사기에서 보기")</span><span class="sxs-lookup"><span data-stu-id="5f57b-305">![Viewing Default.aspx in Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image25.png "Viewing Default.aspx in Page Inspector")</span></span>

    <span data-ttu-id="5f57b-306">*Default.aspx 페이지 검사기에서 보기*</span><span class="sxs-lookup"><span data-stu-id="5f57b-306">*Viewing Default.aspx in Page Inspector*</span></span>

    <span data-ttu-id="5f57b-307">페이지 검사기 도구는 Visual Studio 환경에 통합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-307">The Page Inspector tool is integrated in your Visual Studio environment.</span></span> <span data-ttu-id="5f57b-308">검사기 내장된 브라우저, 선택한 코드를 표시 하는 강력한 HTML 프로파일러 함께 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-308">The inspector contains an embedded browser, together with a powerful HTML profiler that will show the selected code.</span></span> <span data-ttu-id="5f57b-309">확인 페이지에 표시 되는 모양을 보려면 솔루션을 실행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-309">Notice that you do not have to run the solution to see how your pages look.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5f57b-310">페이지 검사기 브라우저의 너비는이 페이지의 너비 보다 작은 경우 표시 되지 않습니다 페이지 제대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-310">When the width of Page Inspector browser is less than the width of the opened page, you will not see the page properly.</span></span> <span data-ttu-id="5f57b-311">이 경우 페이지 검사기의 너비를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-311">If that happens, adjust the width of the Page Inspector.</span></span>
4. <span data-ttu-id="5f57b-312">클릭는 **파일** 페이지 검사기의 탭에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-312">Click the **Files** tab in Page Inspector.</span></span>

    <span data-ttu-id="5f57b-313">렌더링된 된 기본 페이지를 작성 하는 모든 소스 파일에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-313">You will see all the source files that are composing the rendered Default page.</span></span> <span data-ttu-id="5f57b-314">이것은 사용자 정의 컨트롤 및 마스터 페이지를 사용 하 여 작업할 때 특히 한 눈에 모든 요소를 식별 하는 유용한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-314">This is a useful feature to identify all the elements at a glance, especially when you are working with User Controls and Master Pages.</span></span> <span data-ttu-id="5f57b-315">각 파일을 이동할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-315">Notice that you can also navigate to each of the files.</span></span>

    <span data-ttu-id="5f57b-316">![파일 탭](using-page-inspector-in-visual-studio-2012/_static/image26.png "파일 탭")</span><span class="sxs-lookup"><span data-stu-id="5f57b-316">![The Files tab](using-page-inspector-in-visual-studio-2012/_static/image26.png "The Files tab")</span></span>

    <span data-ttu-id="5f57b-317">*파일 탭*</span><span class="sxs-lookup"><span data-stu-id="5f57b-317">*The Files tab*</span></span>
5. <span data-ttu-id="5f57b-318">클릭는 **검사 모드를 설정/해제** 탭의 왼쪽에 있는 단추를 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-318">Click the **Toggle Inspection Mode** button, located at the left of the tabs.</span></span>

    <span data-ttu-id="5f57b-319">이 도구는 페이지의 모든 요소를 선택 하 고 해당 HTML 코드와.aspx 소스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-319">This tool will let you select any element of the page and see its HTML code and .aspx source.</span></span>

    <span data-ttu-id="5f57b-320">![토글 검사 모드 단추](using-page-inspector-in-visual-studio-2012/_static/image27.png "검사 모드를 설정/해제 단추")</span><span class="sxs-lookup"><span data-stu-id="5f57b-320">![Toggle Inspection Mode button](using-page-inspector-in-visual-studio-2012/_static/image27.png "Toggle Inspection Mode button")</span></span>

    <span data-ttu-id="5f57b-321">*토글 검사 모드 단추*</span><span class="sxs-lookup"><span data-stu-id="5f57b-321">*Toggle Inspection Mode button*</span></span>
6. <span data-ttu-id="5f57b-322">페이지 검사기 브라우저에서 페이지 요소 위로 마우스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-322">In the Page Inspector browser, move the mouse over the page elements.</span></span> <span data-ttu-id="5f57b-323">렌더링된 된 페이지 부분 위로 마우스 포인터를 이동 하는 동안 요소 형식이 표시 되 고 해당 소스 태그 또는 코드가 Visual Studio 편집기에서 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-323">While you move the mouse pointer over any part of the rendered page, the element type is displayed and the corresponding source markup or code is highlighted in the Visual Studio editor.</span></span>

    <span data-ttu-id="5f57b-324">![작업에서 검사 모드](using-page-inspector-in-visual-studio-2012/_static/image28.png "동작에서 검사 모드")</span><span class="sxs-lookup"><span data-stu-id="5f57b-324">![Inspection mode in action](using-page-inspector-in-visual-studio-2012/_static/image28.png "Inspection mode in action")</span></span>

    <span data-ttu-id="5f57b-325">*작업에서 검사 모드*</span><span class="sxs-lookup"><span data-stu-id="5f57b-325">*Inspection mode in action*</span></span>

    > [!NOTE]
    > <span data-ttu-id="5f57b-326">페이지 검사기 창을 최대화 하지 않는 또는 소스 코드를 보여 주는 미리 보기 탭을 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-326">Do not maximize the Page Inspector window or you will not be able to see the preview tab showing the source code.</span></span> <span data-ttu-id="5f57b-327">가 최대화 될 때 페이지 검사기에 요소를 클릭 하면 선택 항목의 소스 코드는 표시 되지만 페이지 검사기 창이 숨겨집니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-327">If you click the element in Page Inspector when it is maximized, the source code of the selection will appear but it will hide the Page Inspector window.</span></span>

    <span data-ttu-id="5f57b-328">에 주의 해야 하는 경우 **Default.aspx** 파일을 선택 된 요소를 생성 하는 소스 코드의 부분을 강조 표시 되어 있는지을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-328">If you pay attention to **Default.aspx** file, you will notice that the portion of source code that generates the selected element is highlighted.</span></span> <span data-ttu-id="5f57b-329">이 기능은 코드에 액세스 하는 직접 및 빠른 방법을 제공 하 긴 소스 파일의 버전을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-329">This feature facilitates the edition of long source files, providing a direct and fast way to access the code.</span></span>

    <span data-ttu-id="5f57b-330">![요소를 검사](using-page-inspector-in-visual-studio-2012/_static/image29.png "요소를 검사 합니다.")</span><span class="sxs-lookup"><span data-stu-id="5f57b-330">![Inspecting elements](using-page-inspector-in-visual-studio-2012/_static/image29.png "Inspecting elements")</span></span>

    <span data-ttu-id="5f57b-331">*요소를 검사합니다.*</span><span class="sxs-lookup"><span data-stu-id="5f57b-331">*Inspecting elements*</span></span>
7. <span data-ttu-id="5f57b-332">클릭는 **검사 모드를 설정/해제** 단추 (![Select-the-HTML-tab-to-display-the-HTML-code-rendered-in-the-Page-Inspector-browser.] (using-page-inspector-in-visual-studio-2012/_static/image30.png "Select-the-HTML-tab-to-display-the-HTML-code-rendered-in-the-Page-Inspector-browser 합니다.")</span><span class="sxs-lookup"><span data-stu-id="5f57b-332">Click the **Toggle Inspection Mode** button (![Select-the-HTML-tab-to-display-the-HTML-code-rendered-in-the-Page-Inspector-browser.](using-page-inspector-in-visual-studio-2012/_static/image30.png "Select-the-HTML-tab-to-display-the-HTML-code-rendered-in-the-Page-Inspector-browser.")</span></span> <span data-ttu-id="5f57b-333">), 커서를 사용 하지 않도록 설정 하려면 페이지 검사기 탭에 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-333">), located in Page Inspector tabs, to disable the cursor.</span></span>
8. <span data-ttu-id="5f57b-334">선택 된 **HTML** 탭 페이지 검사기 브라우저에서 렌더링 된 HTML 코드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-334">Select the **HTML** tab to display the HTML code rendered in the Page Inspector browser.</span></span>
9. <span data-ttu-id="5f57b-335">HTML 코드에서 Koala 링크 된 목록 항목을 찾아 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-335">In the HTML code, locate the list item with the Koala link and select it.</span></span>

    <span data-ttu-id="5f57b-336">코드를 선택 하면 해당 출력은 자동으로 강조 표시 된 브라우저를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-336">Notice that when you select the code, the corresponding output is automatically highlighted browser.</span></span> <span data-ttu-id="5f57b-337">이 기능은 미리 HTML 블록 페이지에 렌더링 되는 방식을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-337">This feature is useful to see how an HTML block is rendered on the page.</span></span>

    <span data-ttu-id="5f57b-338">![페이지의 HTML 요소를 선택 하면](using-page-inspector-in-visual-studio-2012/_static/image31.png "페이지의 HTML 요소를 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="5f57b-338">![Selecting an HTML element in the page](using-page-inspector-in-visual-studio-2012/_static/image31.png "Selecting an HTML element in the page")</span></span>

    <span data-ttu-id="5f57b-339">*페이지의 HTML 요소를 선택합니다.*</span><span class="sxs-lookup"><span data-stu-id="5f57b-339">*Selecting an HTML element in the page*</span></span>
10. <span data-ttu-id="5f57b-340">클릭는 **검사 모드를 설정/해제** 사용할 수 있도록 단추 *검사 모드* 탐색 모음을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-340">Click the **Toggle Inspection Mode** button to enable *Inspection Mode* and click the navigation bar.</span></span> <span data-ttu-id="5f57b-341">오른쪽의 HTML 코드의 스타일 창에서 선택한 요소에 적용 된 CSS 스타일으로 목록이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-341">On the right of the HTML code, in the Styles pane, you will see a list with the CSS styles applied to the selected element.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5f57b-342">헤더 사이트 레이아웃의 일부 이므로, 페이지 검사기는 Site.Master 파일 열고 영향을 받는 코드의 세그먼트를 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-342">since the header is a part of the site layout, Page Inspector will also open Site.Master file and highlight the segment of code affected.</span></span>

    <span data-ttu-id="5f57b-343">![DiscoveringstylesWebForms](using-page-inspector-in-visual-studio-2012/_static/image32.png "스타일과 선택 된 요소의 소스 파일 검색")</span><span class="sxs-lookup"><span data-stu-id="5f57b-343">![DiscoveringstylesWebForms](using-page-inspector-in-visual-studio-2012/_static/image32.png "Discovering styles and source files of a selected element")</span></span>

    <span data-ttu-id="5f57b-344">*스타일 및 선택 된 요소의 소스 파일 검색*</span><span class="sxs-lookup"><span data-stu-id="5f57b-344">*Discovering styles and source files of a selected element*</span></span>
11. <span data-ttu-id="5f57b-345">설정/해제 검사 포인터를 사용 하도록 설정, 메뉴 모음 아래 마우스 포인터를 이동 하 고 빈 반원을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-345">With the toggle inspection pointer enabled, move the mouse pointer below the menu bar and click the blank half circle.</span></span>

    <span data-ttu-id="5f57b-346">![요소 선택](using-page-inspector-in-visual-studio-2012/_static/image33.png "요소 선택")</span><span class="sxs-lookup"><span data-stu-id="5f57b-346">![Selecting an element](using-page-inspector-in-visual-studio-2012/_static/image33.png "Selecting an element")</span></span>

    <span data-ttu-id="5f57b-347">*요소 선택*</span><span class="sxs-lookup"><span data-stu-id="5f57b-347">*Selecting an element*</span></span>
12. <span data-ttu-id="5f57b-348">스타일 창에서 찾습니다는 **배경 이미지** 항목 아래에서 **.main 콘텐츠** 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-348">In the Styles pane, locate the **background-image** item under the **.main-content** group.</span></span> <span data-ttu-id="5f57b-349">**선택을 취소** 는 **배경 이미지** 를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-349">**Uncheck** the **background-image** and see what happens.</span></span> <span data-ttu-id="5f57b-350">브라우저는 변경 내용이 즉시 반영 됩니다 및 원 숨겨지는지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-350">You will notice that the browser will reflect the changes immediately and the circle is hidden.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5f57b-351">페이지 검사기 스타일 탭에 적용 하면 변경 내용이 원래 스타일 시트는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-351">The changes you apply on the Page Inspector Styles tab do not affect the original stylesheet.</span></span> <span data-ttu-id="5f57b-352">스타일을 선택 취소 하거나 원하는 하지만 페이지를 새로 고친 후 복원 됩니다 만큼 여러 번 해당 값을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-352">You can uncheck styles or change their values as many times as you want, but they will be restored after refreshing the page.</span></span>

    <span data-ttu-id="5f57b-353">![설정 및 해제 CSS styles2](using-page-inspector-in-visual-studio-2012/_static/image34.png "활성화 및 CSS 스타일 사용 안 함")</span><span class="sxs-lookup"><span data-stu-id="5f57b-353">![Enabling and disabling CSS styles2](using-page-inspector-in-visual-studio-2012/_static/image34.png "Enabling and disabling CSS styles")</span></span>

    <span data-ttu-id="5f57b-354">*사용 하도록 설정 및 CSS 스타일 사용 안 함*</span><span class="sxs-lookup"><span data-stu-id="5f57b-354">*Enabling and disabling CSS styles*</span></span>
13. <span data-ttu-id="5f57b-355">이제를 클릭 합니다는 '**프로그램** **로고는 여기 '** 검사 모드를 사용 하 여 헤더에는 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-355">Now, click the '**your** **logo here'** text on the header using the inspection mode.</span></span>
14. <span data-ttu-id="5f57b-356">에 **스타일** 탭에서 찾을 **글꼴 크기** CSS 특성에서 **.site 제목** 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-356">In the **Styles** tab, locate the **font-size** CSS attribute under the **.site-title** group.</span></span> <span data-ttu-id="5f57b-357">특성을 한 번를 두 번 클릭 해당 값을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-357">Double-click the attribute once to edit its value.</span></span> <span data-ttu-id="5f57b-358">Replace는 2.3em 값과 **3em**, 한 다음 ENTER 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-358">Replace the 2.3em value with **3em**, and then press ENTER.</span></span> <span data-ttu-id="5f57b-359">제목 큰 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-359">Notice that the title looks bigger.</span></span>

    <span data-ttu-id="5f57b-360">![페이지 Inspector2에서 CSS 값을 변경](using-page-inspector-in-visual-studio-2012/_static/image35.png "페이지 검사기에 CSS 변경 값")</span><span class="sxs-lookup"><span data-stu-id="5f57b-360">![Changing CSS values in the Page Inspector2](using-page-inspector-in-visual-studio-2012/_static/image35.png "Changing CSS values in the Page Inspector")</span></span>

    <span data-ttu-id="5f57b-361">*페이지 검사기의 CSS 값 변경*</span><span class="sxs-lookup"><span data-stu-id="5f57b-361">*Changing CSS values in the Page Inspector*</span></span>
15. <span data-ttu-id="5f57b-362">클릭는 **스타일 추적** 페이지 검사기의 오른쪽 창에 있는 탭입니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-362">Click the **Trace Styles** tab, located in the right pane of Page Inspector.</span></span> <span data-ttu-id="5f57b-363">이것이 특성 이름으로 정렬 된 선택 항목에 적용 되는 모든 스타일을 참조 하는 대체 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-363">This is an alternative way to see all the styles applied to the selection, ordered by attribute name.</span></span>

    <span data-ttu-id="5f57b-364">![선택 된 요소의 CSS 스타일 추적](using-page-inspector-in-visual-studio-2012/_static/image36.png "선택 된 요소의 CSS 스타일 추적")</span><span class="sxs-lookup"><span data-stu-id="5f57b-364">![CSS styles tracing of the selected element](using-page-inspector-in-visual-studio-2012/_static/image36.png "CSS styles tracing of the selected element")</span></span>

    <span data-ttu-id="5f57b-365">*선택 된 요소의 CSS 스타일 추적*</span><span class="sxs-lookup"><span data-stu-id="5f57b-365">*CSS styles tracing of the selected element*</span></span>
16. <span data-ttu-id="5f57b-366">페이지 검사기의 다른 기능에는 레이아웃 창입니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-366">Another feature of Page Inspector is the Layout pane.</span></span> <span data-ttu-id="5f57b-367">탐색 모음을 선택한 다음 클릭 검사 모드를 사용 하 여 **레이아웃** 오른쪽 창에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-367">Using the inspection mode, select the navigation bar and then click the **Layout** tab on the right pane.</span></span> <span data-ttu-id="5f57b-368">선택한 창의 정확한 크기와 오프셋, 여백, 안쪽 여백 및 테두리 크기가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-368">You will see the exact size of the selected element, as well as its offset, margin, padding and border size.</span></span> <span data-ttu-id="5f57b-369">이 보기에서 값을 수정할 수도 수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-369">Notice that you can also modify the values from this view.</span></span>

    <span data-ttu-id="5f57b-370">![페이지 검사기에서 요소 레이아웃](using-page-inspector-in-visual-studio-2012/_static/image37.png "페이지 검사기에서 요소 레이아웃")</span><span class="sxs-lookup"><span data-stu-id="5f57b-370">![Element layout in Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image37.png "Element layout in Page Inspector")</span></span>

    <span data-ttu-id="5f57b-371">*페이지 검사기에서 요소 레이아웃*</span><span class="sxs-lookup"><span data-stu-id="5f57b-371">*Element layout in Page Inspector*</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a><span data-ttu-id="5f57b-372">작업 2-확인 및 사진 갤러리 스타일 문제 수정</span><span class="sxs-lookup"><span data-stu-id="5f57b-372">Task 2 - Finding and Fixing Style Issues in the Photo Gallery</span></span>

<span data-ttu-id="5f57b-373">이전 버전의 Visual Studio 웹 페이지 문제를 진단할 어떻게는?</span><span class="sxs-lookup"><span data-stu-id="5f57b-373">How would you diagnose Web pages issues with previous versions of Visual Studio?</span></span> <span data-ttu-id="5f57b-374">Internet Explorer의 도구 개발자 또는 Firebug와 같은 Visual Studio IDE 외부에서 실행 되는 도구를 디버깅 하는 웹 익숙할 것 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-374">You are likely familiar with web debugging tools that run outside the Visual Studio IDE, like Internet Explorer Developer Tools or Firebug.</span></span> <span data-ttu-id="5f57b-375">브라우저에 HTML, 이해 스크립팅 및 스타일, 기본 프레임 워크는 렌더링할 HTML을 생성 하는 동안 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-375">Browsers only understand HTML, scripting and styles, while an underlying framework generates the HTML that will be rendered.</span></span> <span data-ttu-id="5f57b-376">이런 이유로 전체 사이트와 같은 웹 페이지의 모양을 확인를 배포 해야 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-376">For that reason, you often need to deploy the whole site to see how web pages look like.</span></span>

<span data-ttu-id="5f57b-377">아마도 검색 하 고 웹 사이트에서 문제를 해결 하려는 경우 다음이 단계를 따라 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-377">You had probably followed these steps when you wanted to detect and fix an issue in your web site:</span></span>

1. <span data-ttu-id="5f57b-378">Visual Studio에서 솔루션을 실행 하거나 웹 서버에서 페이지를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-378">Run the Solution from Visual Studio, or deploy the page on the web server.</span></span>
2. <span data-ttu-id="5f57b-379">브라우저에서 사용 하 여, 또는 단순히 소스 코드와 스타일을 열고 문제를 일치 시 키 려 개발자 도구를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-379">In the browser, open the developer tools you use, or simply open the source code and the styles and try to match the issue.</span></span> <span data-ttu-id="5f57b-380">관련 된 파일을 찾을 사용 했을 것은 &quot;검색&quot; 또는 &quot;파일에서 검색&quot; 스타일 클래스의 이름으로는 기능.</span><span class="sxs-lookup"><span data-stu-id="5f57b-380">To find the files involved, you'd have used the &quot;Search&quot; or &quot;Search in files&quot; features with the name of the style classes.</span></span>
3. <span data-ttu-id="5f57b-381">오류가 감지 되 면 웹 브라우저와 서버를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-381">Once the error is detected, stop the Web browser and the server.</span></span>
4. <span data-ttu-id="5f57b-382">브라우저 캐시를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-382">Clear the browser cache.</span></span>
5. <span data-ttu-id="5f57b-383">수정 프로그램을 적용 하려면 Visual Studio로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-383">Return to Visual Studio to apply a fix.</span></span> <span data-ttu-id="5f57b-384">테스트 하는 모든 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-384">Repeat all the steps to test.</span></span>

<span data-ttu-id="5f57b-385">ASP.NET WebForms의 실제 WYSIWYG 더 있으면, 일부 스타일 문제를 실행 하거나 배포한 후에 이후 단계에서 검색 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-385">As there is no real WYSIWYG in ASP.NET WebForms, some style issues are detected on a later stage, after running or deploying.</span></span> <span data-ttu-id="5f57b-386">이제 페이지 검사기 이므로 솔루션을 실행 하지 않고 모든 페이지를 미리 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-386">Now, with Page Inspector, it is possible to preview any page without running the solution.</span></span>

<span data-ttu-id="5f57b-387">이 태스크에서는 사진 갤러리 응용 프로그램의 몇 가지 문제를 해결 하기 위한 페이지 검사기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-387">In this task, you will use the Page inspector for fixing some issues of the Photo Gallery application.</span></span> <span data-ttu-id="5f57b-388">다음 단계에서 검색 한 신속 하 게 헤더에 몇 가지 간단한 스타일 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-388">In the following steps, you will detect and quickly fix some simple styling issue in the header.</span></span>

1. <span data-ttu-id="5f57b-389">검사 페이지를 사용 하 여 찾습니다는 **등록** 및 **로그인** 머리글의 왼쪽에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-389">Using Page Inspection, locate the **Register** and the **Log In** links at the left side of the header.</span></span>

    <span data-ttu-id="5f57b-390">알림 오른쪽에 예상된 위치에는 링크가 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-390">Notice that the link is not displayed at the expected place on the right.</span></span> <span data-ttu-id="5f57b-391">이제 오른쪽에 대 한 링크를 정렬 하 고 그에 따라 스타일을 다시 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-391">You will now align the link to the right and restyle it accordingly.</span></span>

    <span data-ttu-id="5f57b-392">![왼쪽에 배치 하는 링크 로그인](using-page-inspector-in-visual-studio-2012/_static/image38.png "왼쪽에 배치 하는 링크에 로그인")</span><span class="sxs-lookup"><span data-stu-id="5f57b-392">![Log in link positioned on the left](using-page-inspector-in-visual-studio-2012/_static/image38.png "Log in link positioned on the left")</span></span>

    <span data-ttu-id="5f57b-393">*로그인 링크 왼쪽에 배치*</span><span class="sxs-lookup"><span data-stu-id="5f57b-393">*Log In link positioned on the left*</span></span>
2. <span data-ttu-id="5f57b-394">선택한 검사 모드를 설정/해제를 해당 코드를 열려는 로그인 링크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-394">With Toggle Inspection Mode selected, select the Log In link to open its code.</span></span>

    <span data-ttu-id="5f57b-395">링크 소스 코드에 있는 통지는 **Site.Master** 안함 첫 번째 위치에서 찾을 수 있습니다 여기에서 Default.aspx 페이지에; 올바른 소스 파일에 직접 배치 했으면 파일을 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-395">Notice that the link source code is located in the **Site.Master** file, not in the Default.aspx page which is the place you might look in first place; you have been placed directly in the correct source file.</span></span>
3. <span data-ttu-id="5f57b-396">에 **스타일** 탭을 찾아서 클릭는  **&lt;섹션&gt; #login** 항목 이러한 링크에 대 한 HTML 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-396">In the **Styles** tab, locate and click the **&lt;section&gt; #login** item, which is the HTML container for these links.</span></span>

    <span data-ttu-id="5f57b-397">다음에 유의 **#login** 스타일에 있는 자동으로 **Site.css** 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-397">Notice that the **#login** style is automatically located in **Site.css** after you click.</span></span> <span data-ttu-id="5f57b-398">또한 코드는 이제 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-398">Moreover, the code is now highlighted.</span></span>

    <span data-ttu-id="5f57b-399">![CSS 스타일을 선택 하면](using-page-inspector-in-visual-studio-2012/_static/image39.png "CSS 스타일 선택")</span><span class="sxs-lookup"><span data-stu-id="5f57b-399">![Selecting the CSS styles](using-page-inspector-in-visual-studio-2012/_static/image39.png "Selecting the CSS styles")</span></span>

    <span data-ttu-id="5f57b-400">*CSS 스타일을 선택 하면*</span><span class="sxs-lookup"><span data-stu-id="5f57b-400">*Selecting the CSS styles*</span></span>
4. <span data-ttu-id="5f57b-401">주석 처리 제거는 **-** 강조 표시 된 코드에서 여는 태그와 닫는 문자를 제거 하 여 특성을 저장할는 **Site.css** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-401">Uncomment the **text-align** attribute in the highlighted code by removing the opening and closing characters and save the **Site.css** file.</span></span>

    <span data-ttu-id="5f57b-402">페이지 검사기를 현재 페이지를 구성 하는 다른 모든 파일의 인식 하며 이러한 파일을 변경 하는 경우를 감지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-402">Page Inspector is aware of all the different files that compose the current page, and it can detect when any of these files change.</span></span> <span data-ttu-id="5f57b-403">브라우저에서 현재 페이지 원본 파일과 함께 동기화 되지 않았습니다. 때마다 경우 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-403">It alerts you whenever the current page in browser is not in sync with the source files.</span></span>
5. <span data-ttu-id="5f57b-404">페이지 검사기 브라우저에서 변경 내용을 저장 하 고 페이지를 다시 로드 하려면 주소 표시줄 아래에 있는 막대를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-404">In the Page Inspector browser, click the bar located below the address bar to save the changes and reload the page.</span></span>

    ![Reloadingthepage](using-page-inspector-in-visual-studio-2012/_static/image40.png)

    <span data-ttu-id="5f57b-406">*페이지를 다시 로드*</span><span class="sxs-lookup"><span data-stu-id="5f57b-406">*Reloading the page*</span></span>

    <span data-ttu-id="5f57b-407">오른쪽에 있는 링크는 이제 하지만 여전히 글머리 기호 목록 처럼 보입니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-407">The links are now at the right, but they still look like a bulleted list.</span></span> <span data-ttu-id="5f57b-408">이제 글머리 기호를 제거 및 링크를 가로 방향으로 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-408">Now, you will remove the bullets and align the links horizontally.</span></span>

    ![업데이트 페이지](using-page-inspector-in-visual-studio-2012/_static/image41.png)

    <span data-ttu-id="5f57b-410">*업데이트 페이지*</span><span class="sxs-lookup"><span data-stu-id="5f57b-410">*Updated page*</span></span>
6. <span data-ttu-id="5f57b-411">검사 모드를 사용 하 여 중 하나를 선택는 **&lt;li&gt;** 포함 된 항목의 &quot;등록&quot; 및 &quot;로그인&quot; 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-411">Using the inspection mode, select any of the **&lt;li&gt;** items that contain the &quot;Register&quot; and &quot;Log in&quot; links.</span></span> <span data-ttu-id="5f57b-412">클릭는  **&lt;섹션&gt; #login** 항목의 액세스 **Styles.css** 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-412">Then, click the **&lt;section&gt; #login** item to access **Styles.css** code.</span></span>

    <span data-ttu-id="5f57b-413">![스타일 찾기](using-page-inspector-in-visual-studio-2012/_static/image42.png "스타일 찾기")</span><span class="sxs-lookup"><span data-stu-id="5f57b-413">![Finding the style](using-page-inspector-in-visual-studio-2012/_static/image42.png "Finding the style")</span></span>

    <span data-ttu-id="5f57b-414">*스타일 찾기*</span><span class="sxs-lookup"><span data-stu-id="5f57b-414">*Finding the style*</span></span>
7. <span data-ttu-id="5f57b-415">**Style.css**에 대 한 코드를 주석 처리 제거 **#login li** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-415">In **Style.css**, uncomment the code for **#login li** items.</span></span> <span data-ttu-id="5f57b-416">추가 하는 스타일 글머리 기호 숨기고 항목 가로로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-416">The style you are adding will hide the bullet and display the items horizontally.</span></span>

    <span data-ttu-id="5f57b-417">![로그인 링크 스타일 재설정](using-page-inspector-in-visual-studio-2012/_static/image43.png "스타일의 로그인 링크를 재설정")</span><span class="sxs-lookup"><span data-stu-id="5f57b-417">![Restyling the login links](using-page-inspector-in-visual-studio-2012/_static/image43.png "Restyling the login links")</span></span>

    <span data-ttu-id="5f57b-418">*로그인 링크 스타일 재설정*</span><span class="sxs-lookup"><span data-stu-id="5f57b-418">*Restyling the login links*</span></span>
8. <span data-ttu-id="5f57b-419">저장 **Style.css** 파일 및 페이지를 다시 로드 하는 주소 아래에 있는 표시줄에 한 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-419">Save **Style.css** file and click once on the bar located below the address to reload the page.</span></span> <span data-ttu-id="5f57b-420">링크는 올바르게 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-420">Notice that the links appear correctly.</span></span>

    <span data-ttu-id="5f57b-421">![오른쪽으로 정렬 하는 링크](using-page-inspector-in-visual-studio-2012/_static/image44.png "오른쪽으로 정렬 하는 링크")</span><span class="sxs-lookup"><span data-stu-id="5f57b-421">![Links aligned to the right side](using-page-inspector-in-visual-studio-2012/_static/image44.png "Links aligned to the right side")</span></span>

    <span data-ttu-id="5f57b-422">*오른쪽으로 정렬 하는 링크*</span><span class="sxs-lookup"><span data-stu-id="5f57b-422">*Links aligned to the right side*</span></span>
9. <span data-ttu-id="5f57b-423">마지막으로, 머리글 제목을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-423">Finally, you will change the header title.</span></span> <span data-ttu-id="5f57b-424">에 대 한 검색 하는 대신는 '**사용자 로고는 여기 '** 의 모든 파일을 텍스트를 클릭 하 고 생성 하는 소스 코드를 검사 모드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-424">Instead of searching for the '**your logo here'** text in all the files, use the inspection mode to click the text and get to source code that generates it.</span></span>

    <span data-ttu-id="5f57b-425">![사이트 제목 찾기](using-page-inspector-in-visual-studio-2012/_static/image45.png "사이트 제목 찾기")</span><span class="sxs-lookup"><span data-stu-id="5f57b-425">![Finding the site title](using-page-inspector-in-visual-studio-2012/_static/image45.png "Finding the site title")</span></span>

    <span data-ttu-id="5f57b-426">*사이트 제목 찾기*</span><span class="sxs-lookup"><span data-stu-id="5f57b-426">*Finding the site title*</span></span>
10. <span data-ttu-id="5f57b-427">에 이제 **Site.Master**, 대체는 '**사용자 로고는 여기**'텍스트와 '**사진 갤러리**'.</span><span class="sxs-lookup"><span data-stu-id="5f57b-427">Now you are in **Site.Master**, replace the '**your logo here**' text with '**Photo Gallery**'.</span></span> <span data-ttu-id="5f57b-428">저장 하 고 페이지 검사기 브라우저를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-428">Save and update the Page Inspector browser.</span></span>

    <span data-ttu-id="5f57b-429">![업데이트 사진 갤러리 페이지](using-page-inspector-in-visual-studio-2012/_static/image46.png "업데이트 사진 갤러리 페이지")</span><span class="sxs-lookup"><span data-stu-id="5f57b-429">![Photo Gallery page updated](using-page-inspector-in-visual-studio-2012/_static/image46.png "Photo Gallery page updated")</span></span>

    <span data-ttu-id="5f57b-430">*업데이트 사진 갤러리 페이지*</span><span class="sxs-lookup"><span data-stu-id="5f57b-430">*Photo Gallery page updated*</span></span>
11. <span data-ttu-id="5f57b-431">마지막으로 키를 눌러 **F5** 체크 아웃 변경 내용이 예상 대로 작동 하는 모든 앱을 실행 하려면.</span><span class="sxs-lookup"><span data-stu-id="5f57b-431">Finally press **F5** to run the app the check out all the changes work as expected.</span></span>

* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="5f57b-432">요약</span><span class="sxs-lookup"><span data-stu-id="5f57b-432">Summary</span></span>

<span data-ttu-id="5f57b-433">이 실습 랩을 완료 하면 다시 작성 하 여 브라우저에서 웹 사이트를 실행할 필요 없이 웹 응용 프로그램을 미리 보려면 페이지 검사기를 사용 하는 방법을 배운 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-433">By completing this Hands-On Lab, you have learnt how to use Page Inspector to preview your Web application without having to rebuild and run the Web site in a browser.</span></span> <span data-ttu-id="5f57b-434">신속 하 게 찾아서 소스 코드에 렌더링된 된 출력에서 직접 액세스 하 여 버그를 수정 하는 방법을 배운 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-434">In addition, you have learnt how to quickly find and fix bugs by accessing directly from the rendered output to the source code.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="5f57b-435">부록 a: 설치 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="5f57b-435">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="5f57b-436">설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 버전을 사용 하 여 **[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="5f57b-436">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="5f57b-437">다음 지침을 설치 하는 데 필요한 단계를 안내 하 *Visual studio Express 2012 for Web* 를 사용 하 여 *Microsoft 웹 플랫폼 설치 관리자*합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-437">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="5f57b-438">로 이동 [ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-438">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="5f57b-439">또는 이미 설치 된 웹 플랫폼 설치 관리자를 열 수 있습니다 및 제품에 대 한 검색 &quot; <em>Visual Studio Express 2012 for Web Windows Azure SDK와</em>&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-439">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="5f57b-440">클릭 **지금 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-440">Click on **Install Now**.</span></span> <span data-ttu-id="5f57b-441">없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-441">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="5f57b-442">한 번 **웹 플랫폼 설치 관리자** 열려 클릭 **설치** 는 설치 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-442">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="5f57b-443">![Visual Studio Express 설치](using-page-inspector-in-visual-studio-2012/_static/image47.png "Visual Studio Express 설치")</span><span class="sxs-lookup"><span data-stu-id="5f57b-443">![Install Visual Studio Express](using-page-inspector-in-visual-studio-2012/_static/image47.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="5f57b-444">*Visual Studio Express 설치*</span><span class="sxs-lookup"><span data-stu-id="5f57b-444">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="5f57b-445">모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-445">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![사용 조건 동의](using-page-inspector-in-visual-studio-2012/_static/image48.png)

    <span data-ttu-id="5f57b-447">*사용 조건 동의*</span><span class="sxs-lookup"><span data-stu-id="5f57b-447">*Accepting the license terms*</span></span>
5. <span data-ttu-id="5f57b-448">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-448">Wait until the downloading and installation process completes.</span></span>

    ![설치 진행률](using-page-inspector-in-visual-studio-2012/_static/image49.png)

    <span data-ttu-id="5f57b-450">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="5f57b-450">*Installation progress*</span></span>
6. <span data-ttu-id="5f57b-451">설치가 완료 되 면 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-451">When the installation completes, click **Finish**.</span></span>

    ![설치 완료](using-page-inspector-in-visual-studio-2012/_static/image50.png)

    <span data-ttu-id="5f57b-453">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="5f57b-453">*Installation completed*</span></span>
7. <span data-ttu-id="5f57b-454">클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-454">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="5f57b-455">Visual Studio Express for Web을 열려면로 이동는 **시작** 화면를 쓰기 시작할 &quot; **VS Express**&quot;, 클릭는 **VS Express for Web** 바둑판식 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="5f57b-455">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![웹 타일에 대 한 VS Express](using-page-inspector-in-visual-studio-2012/_static/image51.png)

    <span data-ttu-id="5f57b-457">*웹 타일에 대 한 VS Express*</span><span class="sxs-lookup"><span data-stu-id="5f57b-457">*VS Express for Web tile*</span></span>
