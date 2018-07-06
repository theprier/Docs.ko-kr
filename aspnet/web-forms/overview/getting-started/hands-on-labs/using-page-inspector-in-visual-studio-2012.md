---
uid: web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
title: Visual Studio 2012에서 페이지 검사기 사용 | Microsoft Docs
author: rick-anderson
description: 이 실습 랩에서 찾기 및 페이지 검사기 Visual Studio에서 웹 페이지 문제를 해결 하는 새 도구를 알게 됩니다. 페이지 검사기는 새 도구는 b가...
ms.author: aspnetcontent
ms.date: 02/18/2013
ms.assetid: 73232292-a5fe-4720-82a1-8f6553effd1f
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: ac945a23dc6ef060340320d047f13c8e81057138
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37833674"
---
<a name="using-page-inspector-in-visual-studio-2012"></a><span data-ttu-id="c0096-104">Visual Studio 2012에서 페이지 검사기 사용</span><span class="sxs-lookup"><span data-stu-id="c0096-104">Using Page Inspector in Visual Studio 2012</span></span>
====================
<span data-ttu-id="c0096-105">[웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="c0096-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="c0096-106">이 실습 랩에서 찾기 및 페이지 검사기 Visual Studio에서 웹 페이지 문제를 해결 하는 새 도구를 알게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-106">In this Hands-on Lab, you will discover a new tool to find and fix web page issues in Visual Studio - the Page Inspector.</span></span>
> 
> <span data-ttu-id="c0096-107">페이지 검사기는 Visual Studio에 브라우저 진단 도구를 제공 하 고 브라우저, ASP.NET 및 소스 코드 간에 통합된 된 환경을 제공 하는 새로운 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-107">Page Inspector is a new tool that brings browser diagnostics tools to Visual Studio and provides an integrated experience among the browser, ASP.NET, and source code.</span></span> <span data-ttu-id="c0096-108">Visual Studio IDE 내에서 직접 웹 페이지 (HTML, Web Forms, ASP.NET MVC 또는 웹 페이지)를 렌더링 하 고 소스 코드 및 결과 출력을 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-108">It renders a web page (HTML, Web Forms, ASP.NET MVC, or Web Pages) directly within the Visual Studio IDE and lets you examine both the source code and the resulting output.</span></span> <span data-ttu-id="c0096-109">페이지 검사기를 사용 하면 웹 사이트를 쉽게 분해, 신속 하 게,부터 페이지를 빌드 및 신속 하 게 문제를 진단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-109">Page Inspector enables you to easily decompose a website, rapidly build pages from the ground up, and quickly diagnose issues.</span></span>
> 
> <span data-ttu-id="c0096-110">오늘날 많은 Asp.net WebForms 등 적절 한 시간에서 유연 하 고 확장 가능한 웹 사이트를 만드는 웹 프레임 워크가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-110">Nowadays we have a number of Web frameworks that create flexible and scalable websites in a timely manner, such as ASP.NET MVC and WebForms.</span></span> <span data-ttu-id="c0096-111">반면에 어렵습니다 아래에 도달할 때 IDE 템플릿 기반 페이지에 동적 콘텐츠 디자이너 뷰를 지원 하지 않으므로 페이지에는 문제를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-111">On the other hand, it gets harder to find issues on the pages because the IDE does not support the designer view in template-based pages and dynamic content.</span></span> <span data-ttu-id="c0096-112">따라서 이러한 웹 사이트 사용자에 게 어떻게 표시 되는지 확인 하려면 브라우저에서 열려 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-112">Therefore, these websites have to be opened in a browser to see how they appear to a user.</span></span>
> 
> <span data-ttu-id="c0096-113">웹 개발자 외부 도구를 사용 하 여 브라우저에서 정기적으로 실행 되는 문제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-113">Web developers use external tools to find issues that regularly run in the browser.</span></span> <span data-ttu-id="c0096-114">그런 다음 IDE를 반환 하며 해결을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-114">Then, they return to the IDE and start fixing.</span></span> <span data-ttu-id="c0096-115">이 앞뒤로 IDE, 브라우저 및 프로 파일링 도구는 작업, 비효율적일 수 있습니다 하며 경우에 따라 문제를 재현 하려는 때마다 정리 캐시를 새로 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-115">This back and forth activity among the IDE, the browser and the profiling tools can be inefficient, and sometimes requires a fresh deployment and cache cleaning each time you want to reproduce an issue.</span></span>
> 
> <span data-ttu-id="c0096-116">페이지 검사기의 장점만 결합 된 기능 집합을 사용 하 여 최고를 결합 하 여 웹 개발 (브라우저 도구) 클라이언트와 서버 (ASP.NET 및 소스 코드) 사이에서 간격이 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-116">Page Inspector bridges a gap in Web development between the client (browser tools) and the server (ASP.NET and source code) by bringing together the best of both worlds using a combined set of features.</span></span>
> 
> <span data-ttu-id="c0096-117">Page Inspector를 사용 (서버 쪽 코드 포함)를 원본 파일의 요소를 생성 한 브라우저에서 렌더링할 HTML 태그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-117">Using Page Inspector, you can see which elements in the source files (including server-side code) have produced the HTML markup to be rendered in the browser.</span></span> <span data-ttu-id="c0096-118">페이지 검사기에서는 CSS 속성과 DOM 요소 특성을 보려면 브라우저에서 즉시 반영 된 변경 내용을 수정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-118">Page Inspector also lets you modify CSS properties and DOM element attributes to see the changes reflected immediately in the browser.</span></span>
> 
> <span data-ttu-id="c0096-119">이 실습 페이지 검사기 기능을 통해 안내를 사용 하 여 웹 응용 프로그램에서 문제를 해결 하도록 하는 방법을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-119">This hands-on lab will walk you through the Page Inspector features and show you how you can use them to fix issues in Web applications.</span></span> <span data-ttu-id="c0096-120">**이 랩에서 비슷한 흐름을 사용 하 여 다양 한 기술을 대상으로 하지만 두 연습을 포함 합니다. ASP.NET MVC 개발자 인 경우에 따라 하나; 연습 두 WebForms 개발자에 따라 연습 경우**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-120">**This lab contains two exercises using similar flows but targeting different technologies. If you are an ASP.NET MVC Developer, follow exercise one; if you are a WebForms developer follow exercise two**.</span></span>
> 
> <span data-ttu-id="c0096-121">이 실습을 이용 하면 향상 된 기능 및 원본 폴더에 제공 된 샘플 웹 응용 프로그램에 사소한 변경 내용을 적용 하 여 이전에 설명 된 새 기능을 통해 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-121">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>
> 
> <span data-ttu-id="c0096-122">웹 캠프 교육 키트에서에서 사용할 수 있는 모든 샘플 코드 및 코드 조각 포함 됩니다 [ https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409 ](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-122">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>


<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="c0096-123">목표</span><span class="sxs-lookup"><span data-stu-id="c0096-123">Objectives</span></span>

<span data-ttu-id="c0096-124">이 실습 랩에서 학습할 방법:</span><span class="sxs-lookup"><span data-stu-id="c0096-124">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="c0096-125">페이지 검사기를 사용 하 여 웹 사이트를 분해 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-125">Decompose a Web Site using Page Inspector</span></span>
- <span data-ttu-id="c0096-126">검사 하 고 페이지 검사기를 사용 하 여 CSS 스타일 변경 내용 미리 보기</span><span class="sxs-lookup"><span data-stu-id="c0096-126">Inspect and preview CSS styles changes with Page Inspector</span></span>
- <span data-ttu-id="c0096-127">검색 하 고 페이지 검사기를 사용 하 여 웹 페이지에서 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-127">Detect and fix issues in your web pages using Page Inspector</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="c0096-128">전제 조건</span><span class="sxs-lookup"><span data-stu-id="c0096-128">Prerequisites</span></span>

<span data-ttu-id="c0096-129">이 랩을 완료 하려면 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-129">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="c0096-130">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) 하거나 그 보다 뛰어난 (읽을 [부록 A](#AppendixA) 설치 하는 방법에 대 한 지침은).</span><span class="sxs-lookup"><span data-stu-id="c0096-130">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>
- <span data-ttu-id="c0096-131">Internet Explorer 9 이상</span><span class="sxs-lookup"><span data-stu-id="c0096-131">Internet Explorer 9 or higher</span></span>

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="c0096-132">연습</span><span class="sxs-lookup"><span data-stu-id="c0096-132">Exercises</span></span>

<span data-ttu-id="c0096-133">이 실습 랩에서 다음 연습에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-133">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="c0096-134">ASP.NET MVC 프로젝트에서 페이지 검사기를 사용 하는 연습 1:</span><span class="sxs-lookup"><span data-stu-id="c0096-134">Exercise 1: Using Page Inspector in ASP.NET MVC Projects</span></span>](#Exercise1)
2. [<span data-ttu-id="c0096-135">WebForms 프로젝트에서 페이지 검사기를 사용 하는 연습 2:</span><span class="sxs-lookup"><span data-stu-id="c0096-135">Exercise 2: Using Page Inspector in WebForms Projects</span></span>](#Exercise2)

> [!NOTE]
> <span data-ttu-id="c0096-136">각 실습은 다른 독립적으로 각 연습에 따라 할 수 있는 실습 시작 폴더에 있는 시작 솔루션에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-136">Each exercise is accompanied by a starting solution, located in the Begin folder of the exercise, that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="c0096-137">연습에 대 한 소스 코드 내에 해당 연습에서 단계를 완료 합니다. 결과로 생성 되는 코드를 사용 하 여 Visual Studio 솔루션을 포함 하는 최종 폴더를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-137">Inside the source code for an exercise, you will also find an End folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="c0096-138">이 실습을 통해 작업 하는 동안 추가 도움이 필요한 경우 지침으로 이러한 솔루션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-138">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>


<span data-ttu-id="c0096-139">이 랩을 완료 하기 위한 예상 시간: **30 분**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-139">Estimated time to complete this lab: **30 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Using_Page_Inspector_in_ASPNET_MVC_Projects"></a>
### <a name="exercise-1-using-page-inspector-in-aspnet-mvc-projects"></a><span data-ttu-id="c0096-140">ASP.NET MVC 프로젝트에서 페이지 검사기를 사용 하는 연습 1:</span><span class="sxs-lookup"><span data-stu-id="c0096-140">Exercise 1: Using Page Inspector in ASP.NET MVC Projects</span></span>

<span data-ttu-id="c0096-141">이 연습에서는 미리 보기 및 디버그 하는 방법을 배우게 됩니다는 **ASP.NET MVC 4** 사용 하 여 솔루션 **페이지 검사기**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-141">In this exercise, you will learn how to preview and debug an **ASP.NET MVC 4** solution using **Page Inspector**.</span></span> <span data-ttu-id="c0096-142">첫째, 프로세스를 디버깅 하는 웹을 쉽게 수행할 수 있는 기능을 알아보려면 간략 한 둘러보기 도구 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-142">First, you will perform a brief lap around the tool to learn the features that facilitate the Web debugging process.</span></span> <span data-ttu-id="c0096-143">그런 다음 스타일 문제를 포함 하는 웹 페이지에서 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-143">Then, you will work in a web page that contains styling issues.</span></span> <span data-ttu-id="c0096-144">페이지 검사기를 사용 하 여 문제를 생성 하는 소스 코드를 수정 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-144">You will learn how to use Page Inspector to find the source code that generates the issue and fix it.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a><span data-ttu-id="c0096-145">작업 1-페이지 검사기를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-145">Task 1 - Exploring Page Inspector</span></span>

<span data-ttu-id="c0096-146">이 태스크에서는 사진 갤러리를 표시 하는 ASP.NET MVC 4 프로젝트의 컨텍스트에서 페이지 검사기를 사용 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-146">In this task, you will learn how to use the Page Inspector in the context of an ASP.NET MVC 4 project that shows a photo gallery.</span></span>

1. <span data-ttu-id="c0096-147">엽니다는 **시작할** 솔루션에 있는 **소스/e x 1-MVC4/시작/** 폴더.</span><span class="sxs-lookup"><span data-stu-id="c0096-147">Open the **Begin** solution located at **Source/Ex1-MVC4/Begin/** folder.</span></span>

   1. <span data-ttu-id="c0096-148">일부 누락 된 NuGet 패키지를 다운로드 해야 하기 전에 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-148">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="c0096-149">이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-149">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="c0096-150">에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="c0096-150">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="c0096-151">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-151">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c0096-152">NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-152">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="c0096-153">NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-153">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="c0096-154">이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-154">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="c0096-155">솔루션 탐색기에서 찾습니다 **Index.cshtml** 보기는 **/뷰/홈** 프로젝트 폴더를 마우스 오른쪽 단추로 클릭 및 선택 **페이지 검사기에서 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-155">In the Solution Explorer, locate **Index.cshtml** view under the **/Views/Home** project folder, right-click it and select **View in Page Inspector**.</span></span>

    <span data-ttu-id="c0096-156">![페이지 검사기에서 미리 보기 위해 파일을 선택 하면](using-page-inspector-in-visual-studio-2012/_static/image1.png "페이지 검사기에서 미리 보기 위해 파일을 선택 하면")</span><span class="sxs-lookup"><span data-stu-id="c0096-156">![Selecting a file to preview in Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image1.png "Selecting a file to preview in Page Inspector")</span></span>

    <span data-ttu-id="c0096-157">*페이지 검사기에서 미리 보기 위해 파일을 선택 하면*</span><span class="sxs-lookup"><span data-stu-id="c0096-157">*Selecting a file to preview in Page Inspector*</span></span>
3. <span data-ttu-id="c0096-158">페이지 검사기 창에 표시 됩니다는 */Home/Index* URL 소스 선택한 보기에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-158">The Page Inspector window will show the */Home/Index* URL mapped to the source View you selected.</span></span>

    ![ThefirstcontactwithPageInspector](using-page-inspector-in-visual-studio-2012/_static/image2.png)

    <span data-ttu-id="c0096-160">*페이지 검사기를 사용 하 여 첫 번째 연락처*</span><span class="sxs-lookup"><span data-stu-id="c0096-160">*The first contact with Page Inspector*</span></span>

    <span data-ttu-id="c0096-161">페이지 검사기 도구는 Visual Studio 환경에 통합 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-161">The Page Inspector tool is integrated in your Visual Studio environment.</span></span> <span data-ttu-id="c0096-162">검사기는 강력한 HTML 프로파일러 함께 포함 된 브라우저를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-162">The inspector contains an embedded browser, together with a powerful HTML profiler.</span></span> <span data-ttu-id="c0096-163">확인 페이지에 표시 되는 방식을 확인 하려면 솔루션을 실행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-163">Notice that you do not have to run the solution to see how your pages look.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c0096-164">페이지 검사기 브라우저의 너비 열린된 페이지의 너비 보다 작은 경우 표시 되지 않습니다 페이지 적절 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-164">When the width of Page Inspector browser is less than the width of the opened page, you will not see the page properly.</span></span> <span data-ttu-id="c0096-165">이 경우 페이지 검사기의 너비를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-165">If that happens, adjust the width of the Page Inspector.</span></span>
4. <span data-ttu-id="c0096-166">클릭 합니다 **파일** 페이지 검사기에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-166">Click the **Files** tab in Page Inspector.</span></span>

    <span data-ttu-id="c0096-167">인덱스 페이지를 작성 하는 모든 소스 파일에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-167">You will see all the source files that are composing the Index page.</span></span> <span data-ttu-id="c0096-168">이 기능은 부분 뷰 및 템플릿을 사용 하 여 작업 하는 경우에 특히 눈에 모든 요소를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-168">This feature helps to identify all the elements at a glance, especially when you are working with partial views and templates.</span></span> <span data-ttu-id="c0096-169">열 수 있습니다도 각 파일의 링크를 클릭 하면 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-169">Notice that you can also open each of the files if you click the links.</span></span>

    ![파일 탭](using-page-inspector-in-visual-studio-2012/_static/image3.png)

    <span data-ttu-id="c0096-171">*파일 탭*</span><span class="sxs-lookup"><span data-stu-id="c0096-171">*The Files tab*</span></span>
5. <span data-ttu-id="c0096-172">클릭 합니다 **검사 모드 설정/해제** 탭의 왼쪽에 있는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-172">Click the **Toggle Inspection Mode** button, located at the left of the tabs.</span></span>

    <span data-ttu-id="c0096-173">이 도구를 사용 하면 페이지의 모든 요소를 선택 하 고 HTML 및 Razor 코드를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="c0096-173">This tool will let you select any element of the page and see its HTML and Razor code.</span></span>

    ![검사 모드 단추 설정/해제](using-page-inspector-in-visual-studio-2012/_static/image4.png)

    <span data-ttu-id="c0096-175">*설정/해제 검사 모드 단추*</span><span class="sxs-lookup"><span data-stu-id="c0096-175">*Toggle Inspection Mode button*</span></span>
6. <span data-ttu-id="c0096-176">페이지 검사기 브라우저에서 페이지 요소 위에 마우스 포인터를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-176">In the Page Inspector browser, move the mouse pointer over the page elements.</span></span> <span data-ttu-id="c0096-177">렌더링된 된 페이지 부분 위로 마우스 포인터를 이동 하는 동안 요소 형식이 표시 되 고 Visual Studio 편집기에서 해당 소스 태그나 코드가 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-177">While you move the mouse pointer over any part of the rendered page, the element type is displayed and the corresponding source markup or code is highlighted in the Visual Studio editor.</span></span>

    ![Inspectionmodeinaction](using-page-inspector-in-visual-studio-2012/_static/image5.png)

    <span data-ttu-id="c0096-179">*실행 중인 검사 모드*</span><span class="sxs-lookup"><span data-stu-id="c0096-179">*Inspection mode in action*</span></span>

    > [!NOTE]
    > <span data-ttu-id="c0096-180">페이지 검사기 창을 최대화 하지 않습니다 또는 소스 코드를 보여 주는 미리 보기 탭을 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-180">Do not maximize the Page Inspector window or you will not be able to see the preview tab showing the source code.</span></span> <span data-ttu-id="c0096-181">최대화 되었을 때 페이지 검사기에서 요소를 클릭 하면 선택 항목의 소스 코드를 나타나지만 페이지 검사기 창에 게 숨겨집니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-181">If you click the element in Page Inspector when it is maximized, the source code of the selection will appear but it will hide the Page Inspector window.</span></span>

    <span data-ttu-id="c0096-182">에 주의 기울여야 하는 경우는 **Index.cshtml** 파일인 선택한 요소를 생성 하는 소스 코드의 부분을 강조 표시 되어 있는지을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-182">If you pay attention to the **Index.cshtml** file, you will notice that the portion of source code that generates the selected element is highlighted.</span></span> <span data-ttu-id="c0096-183">이 기능을 사용 하면 코드에 액세스 하는 직접 및 빠른 방법을 제공 하는 긴 소스 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-183">This feature facilitates the editing of long source files, providing a direct and fast way to access the code.</span></span>

    ![Inspectingelements](using-page-inspector-in-visual-studio-2012/_static/image6.png)

    <span data-ttu-id="c0096-185">*요소를 검사합니다.*</span><span class="sxs-lookup"><span data-stu-id="c0096-185">*Inspecting elements*</span></span>
7. <span data-ttu-id="c0096-186">클릭 합니다 **검사 모드 설정/해제** 단추 (![HTML 탭을 선택 하 고 페이지 검사기 브라우저에서 렌더링 된 HTML 코드를 표시 합니다.] (using-page-inspector-in-visual-studio-2012/_static/image7.png "페이지 검사기 브라우저에서 렌더링 된 HTML 코드를 표시할 HTML 탭을 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="c0096-186">Click the **Toggle Inspection Mode** button (![Select the HTML tab to display the HTML code rendered in the Page Inspector browser.](using-page-inspector-in-visual-studio-2012/_static/image7.png "Select the HTML tab to display the HTML code rendered in the Page Inspector browser.")</span></span> <span data-ttu-id="c0096-187">) 커서를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-187">) to disable the cursor.</span></span>
8. <span data-ttu-id="c0096-188">선택 된 **HTML** 탭 페이지 검사기 브라우저에서 렌더링 된 HTML 코드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-188">Select the **HTML** tab to display the HTML code rendered in the Page Inspector browser.</span></span>
9. <span data-ttu-id="c0096-189">HTML 태그에서 Koala 링크를 사용 하 여 목록 항목을 찾아 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-189">In the HTML markup, locate the list item with the Koala link and select it.</span></span>

    <span data-ttu-id="c0096-190">코드를 선택 하면 해당 출력을 자동으로 강조 표시 하는 브라우저에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-190">Notice that when you select the code, the corresponding output is automatically highlighted in the browser.</span></span> <span data-ttu-id="c0096-191">이 기능은 HTML 블록을 페이지에 렌더링 되는 방법을 참조 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-191">This feature is useful to see how an HTML block is rendered on the page.</span></span>

    <span data-ttu-id="c0096-192">![페이지의 HTML 요소를 선택 하면](using-page-inspector-in-visual-studio-2012/_static/image8.png "페이지의 HTML 선택 요소")</span><span class="sxs-lookup"><span data-stu-id="c0096-192">![Selecting HTML element in the page](using-page-inspector-in-visual-studio-2012/_static/image8.png "Selecting HTML element in the page")</span></span>

    <span data-ttu-id="c0096-193">*페이지에서 HTML 요소를 선택합니다.*</span><span class="sxs-lookup"><span data-stu-id="c0096-193">*Selecting HTML element in the page*</span></span>
10. <span data-ttu-id="c0096-194">클릭 합니다 **검사 모드 설정/해제** 단추를 사용 하도록 설정 *검사 모드* 탐색 모음을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-194">Click the **Toggle Inspection Mode** button to enable *Inspection Mode* and click the navigation bar.</span></span> <span data-ttu-id="c0096-195">오른쪽의 HTML 코드의 스타일 창에서 선택한 요소에 적용 된 CSS 스타일을 사용 하 여 목록이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-195">On the right of the HTML code, in the Styles pane, you will see a list with the CSS styles applied to the selected element.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c0096-196">페이지 검사기를 열 수도 헤더 사이트 레이아웃의 일부 이므로 \_Layout.cshtml 파일 및 영향을 받는 코드의 세그먼트를 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-196">Since the header is a part of the site layout, Page Inspector will also open \_Layout.cshtml file and highlight the segment of code affected.</span></span>

    ![Discoveringstyles](using-page-inspector-in-visual-studio-2012/_static/image9.png)

    <span data-ttu-id="c0096-198">*스타일 및 선택한 요소의 소스 파일 검색*</span><span class="sxs-lookup"><span data-stu-id="c0096-198">*Discovering styles and source files of a selected element*</span></span>
11. <span data-ttu-id="c0096-199">사용 설정/해제 검사 포인터를 사용 하 여 주요 파란색 막대 아래 마우스 포인터를 이동 하 고 절반 원을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-199">With the toggle inspection pointer enabled, move the mouse pointer below the blue featured bar and click the half circle.</span></span>

    <span data-ttu-id="c0096-200">![요소 선택](using-page-inspector-in-visual-studio-2012/_static/image10.png "요소 선택")</span><span class="sxs-lookup"><span data-stu-id="c0096-200">![Selecting an element](using-page-inspector-in-visual-studio-2012/_static/image10.png "Selecting an element")</span></span>

    <span data-ttu-id="c0096-201">*요소 선택*</span><span class="sxs-lookup"><span data-stu-id="c0096-201">*Selecting an element*</span></span>
12. <span data-ttu-id="c0096-202">스타일 창에서 찾을 합니다 **배경 이미지** 아래에 있는 항목을 **.main 콘텐츠** 그룹.</span><span class="sxs-lookup"><span data-stu-id="c0096-202">In the Styles pane, locate the **background-image** item under the **.main-content** group.</span></span> <span data-ttu-id="c0096-203">**선택 취소** 는 **배경 이미지** 를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-203">**Uncheck** the **background-image** and see what happens.</span></span> <span data-ttu-id="c0096-204">브라우저는 변경 내용의 즉시 반영 됩니다 하 원 숨겨지는지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-204">You will notice that the browser will reflect the changes immediately and the circle is hidden.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c0096-205">페이지 검사기 스타일 탭에 적용할 변경 내용을 원래 스타일 시트는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-205">The changes you apply on the Page Inspector Styles tab do not affect the original stylesheet.</span></span> <span data-ttu-id="c0096-206">스타일을 선택 취소 하거나 만큼 있지만 페이지를 새로 고친 후 복원할 수는 해당 값을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-206">You can uncheck styles or change their values as many times as you want, but they will be restored after refreshing the page.</span></span>

    <span data-ttu-id="c0096-207">![CSS 스타일을 설정 하거나 해제](using-page-inspector-in-visual-studio-2012/_static/image11.png "및 CSS 스타일을 사용 하지 않도록 설정")</span><span class="sxs-lookup"><span data-stu-id="c0096-207">![Enabling and disabling CSS styles](using-page-inspector-in-visual-studio-2012/_static/image11.png "Enabling and disabling CSS styles")</span></span>

    <span data-ttu-id="c0096-208">*설정 및 CSS 스타일을 사용 하지 않도록 설정*</span><span class="sxs-lookup"><span data-stu-id="c0096-208">*Enabling and disabling CSS styles*</span></span>
13. <span data-ttu-id="c0096-209">이제 클릭을 '**사용자 로고는 여기**' 검사 모드를 사용 하 여 헤더 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-209">Now, click the '**your logo here**' text on the header using the inspection mode.</span></span>
14. <span data-ttu-id="c0096-210">에 **스타일** 탭에서 찾을 **글꼴 크기** 에서 CSS 특성를 **.site 제목** 그룹.</span><span class="sxs-lookup"><span data-stu-id="c0096-210">In the **Styles** tab, locate the **font-size** CSS attribute under the **.site-title** group.</span></span> <span data-ttu-id="c0096-211">특성 값을 두 번 클릭 하 고 2.3 em 값을 바꿉니다 **3 em**, 누릅니다 **ENTER**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-211">Double-click the attribute value and replace the 2.3 em value with **3 em**, and then press **ENTER**.</span></span> <span data-ttu-id="c0096-212">제목을 더 큰 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-212">Notice that the title looks bigger.</span></span>

    <span data-ttu-id="c0096-213">![페이지 검사기에서 CSS 값을 변경](using-page-inspector-in-visual-studio-2012/_static/image12.png "페이지 검사기에서 CSS 변경 값")</span><span class="sxs-lookup"><span data-stu-id="c0096-213">![Changing CSS values in the Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image12.png "Changing CSS values in the Page Inspector")</span></span>

    <span data-ttu-id="c0096-214">*페이지 검사기에서 CSS 값을 변경*</span><span class="sxs-lookup"><span data-stu-id="c0096-214">*Changing CSS values in the Page Inspector*</span></span>
15. <span data-ttu-id="c0096-215">클릭 합니다 **스타일 추적** 페이지 검사기의 오른쪽 창에 있는 탭입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-215">Click the **Trace Styles** tab, located in the right pane of Page Inspector.</span></span> <span data-ttu-id="c0096-216">이것이 특성 이름별으로 정렬 하 고 선택 항목을 적용할 모든 스타일을 참조 하는 대체 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-216">This is an alternative way to see all the styles applied to the selection, ordered by attribute name.</span></span>

    ![CSSstylestracing](using-page-inspector-in-visual-studio-2012/_static/image13.png)

    <span data-ttu-id="c0096-218">*선택한 요소의 CSS 스타일 추적*</span><span class="sxs-lookup"><span data-stu-id="c0096-218">*CSS styles tracing of the selected element*</span></span>
16. <span data-ttu-id="c0096-219">페이지 검사기의 또 다른 기능은 레이아웃 창입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-219">Another feature of Page Inspector is the Layout pane.</span></span> <span data-ttu-id="c0096-220">탐색 모음을 선택한 다음 클릭 검사 모드를 사용 하 여 **레이아웃** 오른쪽 창에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-220">Using the inspection mode, select the navigation bar and then click the **Layout** tab on the right pane.</span></span> <span data-ttu-id="c0096-221">선택한 요소의 정확한 크기와 오프셋, 여백, 안쪽 여백 및 테두리 크기를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-221">You will see the exact size of the selected element, as well as its offset, margin, padding and border size.</span></span> <span data-ttu-id="c0096-222">이 보기에서 값을 수정할 수도 있습니다 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-222">Notice that you can also modify the values from this view.</span></span>

    <span data-ttu-id="c0096-223">![페이지 검사기에서 요소 레이아웃](using-page-inspector-in-visual-studio-2012/_static/image14.png "페이지 검사기에서 요소 레이아웃")</span><span class="sxs-lookup"><span data-stu-id="c0096-223">![Element layout in Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image14.png "Element layout in Page Inspector")</span></span>

    <span data-ttu-id="c0096-224">*페이지 검사기에서 요소 레이아웃*</span><span class="sxs-lookup"><span data-stu-id="c0096-224">*Element layout in Page Inspector*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a><span data-ttu-id="c0096-225">작업 2-찾기 및 사진 갤러리에서 스타일 문제 해결</span><span class="sxs-lookup"><span data-stu-id="c0096-225">Task 2 - Finding and Fixing Style Issues in the Photo Gallery</span></span>

<span data-ttu-id="c0096-226">이전 버전의 Visual Studio를 사용 하 여 웹 페이지 문제를 진단 하는 어떻게는?</span><span class="sxs-lookup"><span data-stu-id="c0096-226">How would you diagnose Web pages issues with previous versions of Visual Studio?</span></span> <span data-ttu-id="c0096-227">Internet Explorer 개발자 도구 또는 Firebug와 같은 Visual Studio IDE 외부에서 실행 되는 도구를 디버깅 하는 웹 익숙할 것 이며</span><span class="sxs-lookup"><span data-stu-id="c0096-227">You are likely familiar with web debugging tools that run outside the Visual Studio IDE, like Internet Explorer Developer Tools or Firebug.</span></span> <span data-ttu-id="c0096-228">브라우저에만 HTML 이해 스크립팅 및 스타일, 기본 프레임 워크를 렌더링할 HTML을 생성 하는 동안.</span><span class="sxs-lookup"><span data-stu-id="c0096-228">Browsers only understand HTML, scripting and styles, while an underlying framework generates the HTML that will be rendered.</span></span> <span data-ttu-id="c0096-229">이런 이유로 웹 페이지와 같은 어떻게 표시 되는지 확인 하려면 전체 사이트를 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-229">For that reason, you often need to deploy the whole site to see how web pages look like.</span></span>

<span data-ttu-id="c0096-230">아마도 감지 하 고 웹 사이트에서 문제를 해결 하려는 경우 다음이 단계를 수행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-230">You had probably followed these steps when you wanted to detect and fix an issue in your web site:</span></span>

1. <span data-ttu-id="c0096-231">Visual Studio에서 솔루션을 실행 하거나 웹 서버에서 페이지를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-231">Run the Solution from Visual Studio, or deploy the page on the web server.</span></span>
2. <span data-ttu-id="c0096-232">브라우저에서 개발자 도구를 사용 하거나 단순히 소스 코드와 스타일을 열고 문제 일치 시 키 려를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-232">In the browser, open the developer tools you use, or simply open the source code and the styles and try to match the issue.</span></span> <span data-ttu-id="c0096-233">관련 된 파일을 찾을 사용 하는 합니다 &quot;검색&quot; 또는 &quot;파일에서 검색&quot; 스타일 클래스 이름 사용 하 여 기능 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-233">To find the files involved, you would have used the &quot;Search&quot; or &quot;Search in files&quot; features with the name of the style classes.</span></span>
3. <span data-ttu-id="c0096-234">오류가 감지 되 면 웹 브라우저 및 서버를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-234">Once the error is detected, stop the Web browser and the server.</span></span>
4. <span data-ttu-id="c0096-235">브라우저 캐시를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-235">Clear the browser cache.</span></span>
5. <span data-ttu-id="c0096-236">수정 프로그램을 적용 하려면 Visual Studio로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-236">Return to Visual Studio to apply a fix.</span></span> <span data-ttu-id="c0096-237">테스트 하는 모든 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-237">Repeat all the steps to test.</span></span>

<span data-ttu-id="c0096-238">ASP.NET MVC 4에서 없는 실제 WYSIWYG 그대로 스타일 문제를 대부분 실행 또는 웹 응용 프로그램을 배포 후 이후 단계에서 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-238">As there is no real WYSIWYG in ASP.NET MVC 4, most of the style issues are detected on a later stage, after running or deploying the web application.</span></span> <span data-ttu-id="c0096-239">이제 페이지 검사기를 사용 하 여 솔루션을 실행 하지 않고 모든 페이지를 미리 보려면는 것이 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-239">Now, with Page Inspector, it is possible to preview any page without running the solution.</span></span>

<span data-ttu-id="c0096-240">이 태스크에서는 페이지 검사기 사용 및 사진 갤러리 응용 프로그램 몇 가지 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-240">In this task, you will use the Page inspector and fix some issues the Photo Gallery application.</span></span>

1. <span data-ttu-id="c0096-241">페이지 검사기를 사용 하 여 찾습니다 합니다 **등록** 하며 **로그인** 헤더의 왼쪽에 있는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-241">Using Page Inspector, locate the **Register** and the **Log in** links at the left side of the header.</span></span>

    <span data-ttu-id="c0096-242">링크를 오른쪽의 예상된 된 위치에 표시 되지 않습니다 글머리 기호 목록 처럼 표시 됩니다에 유의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c0096-242">Notice that the links are not displayed at the expected place on the right, and they are shown like a bulleted list.</span></span> <span data-ttu-id="c0096-243">이제 링크를 오른쪽 맞춤 하 고 스타일을 다시 지정을 적절 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-243">You will now align the links to the right and restyle them accordingly.</span></span>

    <span data-ttu-id="c0096-244">![링크에서 등록 및 로그를 찾는](using-page-inspector-in-visual-studio-2012/_static/image15.png "링크에서 등록 및 로그 찾기")</span><span class="sxs-lookup"><span data-stu-id="c0096-244">![Locating the Register and Log in links](using-page-inspector-in-visual-studio-2012/_static/image15.png "Locating the Register and Log in links")</span></span>

    <span data-ttu-id="c0096-245">*링크에서 등록 및 로그 찾기*</span><span class="sxs-lookup"><span data-stu-id="c0096-245">*Locating the Register and Log in links*</span></span>
2. <span data-ttu-id="c0096-246">선택한 검사 모드를 설정/해제, 가까이에 없지만, 해당 코드를 열려면 등록 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-246">With Toggle Inspection Mode selected, click close to, but not on, the Register link to open its code.</span></span>

    <span data-ttu-id="c0096-247">링크의 소스 코드에는  **\_LoginPartial.cshtml** 하지 Index.cshtml 파일 또는 \_Layout.cshtml 첫 번째 위치에서 찾을 수 있습니다 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-247">Notice that the source code of the links is located in the **\_LoginPartial.cshtml** file, not the Index.cshtml nor the \_Layout.cshtml, which are the places you might look in first place.</span></span> <span data-ttu-id="c0096-248">올바른 소스 파일에 직접 배치 된 했으면 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-248">You have been placed directly in the correct source file.</span></span>
3. <span data-ttu-id="c0096-249">에 **스타일** 탭을 찾아 클릭 합니다 **<section> #login</section>** 항목 이러한 링크의 HTML 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-249">In the **Styles** tab, locate and click the **<section> #login</section>** item, which is the HTML container for these links.</span></span>

    <span data-ttu-id="c0096-250">있음을 합니다 **#login** 스타일에 자동으로 위치한 **Site.css** 클릭 한 후입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-250">Notice that the **#login** style is automatically located in **Site.css** after you click.</span></span> <span data-ttu-id="c0096-251">또한 코드는 이제 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-251">Moreover, the code is now highlighted.</span></span>

    <span data-ttu-id="c0096-252">![CSS 스타일을 선택 하면](using-page-inspector-in-visual-studio-2012/_static/image16.png "CSS 스타일을 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="c0096-252">![Selecting the CSS styles](using-page-inspector-in-visual-studio-2012/_static/image16.png "Selecting the CSS styles")</span></span>

    <span data-ttu-id="c0096-253">*CSS 스타일을 선택합니다.*</span><span class="sxs-lookup"><span data-stu-id="c0096-253">*Selecting the CSS styles*</span></span>
4. <span data-ttu-id="c0096-254">주석 처리를 제거 합니다 **텍스트 맞춤** 을 열고 닫는 문자를 제거 하 여 강조 표시 된 코드에서 특성 및 저장 합니다 **Site.css** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-254">Uncomment the **text-align** attribute in the highlighted code by removing the opening and closing characters and save the **Site.css** file.</span></span>

    <span data-ttu-id="c0096-255">페이지 검사기는 현재 페이지를 구성 하는 모든 다른 파일을 인식 하 고 이러한 파일 중 하나를 변경 하는 경우 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-255">Page Inspector is aware of all the different files that compose the current page, and it can detect when any of these files change.</span></span> <span data-ttu-id="c0096-256">사용자에 게 경고 때마다 브라우저에서 현재 페이지 원본 파일과 함께 동기화 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-256">It alerts you whenever the current page in browser is not in sync with the source files.</span></span>
5. <span data-ttu-id="c0096-257">페이지 검사기 브라우저에서 페이지를 다시 로드 주소 표시줄 아래에 있는 막대를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-257">In the Page Inspector browser, click the bar located below the address bar to reload the page.</span></span>

    ![페이지를 다시 로드](using-page-inspector-in-visual-studio-2012/_static/image17.png)

    <span data-ttu-id="c0096-259">*페이지를 다시 로드*</span><span class="sxs-lookup"><span data-stu-id="c0096-259">*Reloading the page*</span></span>

    <span data-ttu-id="c0096-260">오른쪽에서 링크 됩니다 있지만 여전히 글머리 기호 목록 처럼 보입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-260">The links are now at the right, but they still look like a bulleted list.</span></span> <span data-ttu-id="c0096-261">이제 글머리 기호 제거 및 링크를 가로로 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-261">Now, you will remove the bullets and align the links horizontally.</span></span>

    ![업데이트 된 페이지](using-page-inspector-in-visual-studio-2012/_static/image18.png)

    <span data-ttu-id="c0096-263">*업데이트 된 페이지*</span><span class="sxs-lookup"><span data-stu-id="c0096-263">*Updated page*</span></span>
6. <span data-ttu-id="c0096-264">중 하나를 선택 하는 검사 모드를 사용 하 여 합니다 **&lt;li&gt;** 포함 된 항목을 &quot;등록&quot; 및 &quot;로그인&quot; 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-264">Using the inspection mode, select any of the **&lt;li&gt;** items that contain the &quot;Register&quot; and &quot;Log in&quot; links.</span></span> <span data-ttu-id="c0096-265">클릭 합니다  **&lt;섹션&gt; #login** 액세스 항목 **Styles.css** 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-265">Then, click the **&lt;section&gt; #login** item to access **Styles.css** code.</span></span>

    <span data-ttu-id="c0096-266">![스타일 찾기](using-page-inspector-in-visual-studio-2012/_static/image19.png "스타일 찾기")</span><span class="sxs-lookup"><span data-stu-id="c0096-266">![Finding the style](using-page-inspector-in-visual-studio-2012/_static/image19.png "Finding the style")</span></span>

    <span data-ttu-id="c0096-267">*스타일 찾기*</span><span class="sxs-lookup"><span data-stu-id="c0096-267">*Finding the style*</span></span>
7. <span data-ttu-id="c0096-268">**Style.css**에 대 한 코드를 주석 처리 제거 **#login li** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-268">In **Style.css**, uncomment the code for **#login li** items.</span></span> <span data-ttu-id="c0096-269">추가할 스타일 글머리 숨기고 항목 가로로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-269">The style you are adding will hide the bullet and display the items horizontally.</span></span>

    <span data-ttu-id="c0096-270">![로그인 링크를 재지정](using-page-inspector-in-visual-studio-2012/_static/image20.png "로그인 링크를 재지정")</span><span class="sxs-lookup"><span data-stu-id="c0096-270">![Restyling the login links](using-page-inspector-in-visual-studio-2012/_static/image20.png "Restyling the login links")</span></span>

    <span data-ttu-id="c0096-271">*로그인 링크를 재지정*</span><span class="sxs-lookup"><span data-stu-id="c0096-271">*Restyling the login links*</span></span>
8. <span data-ttu-id="c0096-272">저장할 **Style.css** 파일 및 페이지를 다시 로드 하는 주소 아래에 있는 표시줄에서 한 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-272">Save **Style.css** file and click once on the bar located below the address to reload the page.</span></span> <span data-ttu-id="c0096-273">링크를 올바르게 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-273">Notice that the links appear correctly.</span></span>

    <span data-ttu-id="c0096-274">![링크는 왼쪽에서 오른쪽으로 정렬](using-page-inspector-in-visual-studio-2012/_static/image21.png "링크는 왼쪽에서 오른쪽으로 정렬")</span><span class="sxs-lookup"><span data-stu-id="c0096-274">![Links aligned to the right side](using-page-inspector-in-visual-studio-2012/_static/image21.png "Links aligned to the right side")</span></span>

    <span data-ttu-id="c0096-275">*왼쪽에서 오른쪽으로 정렬 하는 링크*</span><span class="sxs-lookup"><span data-stu-id="c0096-275">*Links aligned to the right side*</span></span>
9. <span data-ttu-id="c0096-276">마지막으로 머리글 제목을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-276">Finally, you will change the header title.</span></span> <span data-ttu-id="c0096-277">검사 모드를 사용 하 여 **사용자 로고는 여기** 텍스트 및 생성 하는 소스 코드를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-277">Use the inspection mode to click **your logo here** text and get to the source code that generates it.</span></span>
10. <span data-ttu-id="c0096-278">에 이제  **\_Layout.cshtml**, 대체 '**여기에 로고**'텍스트'**사진 갤러리**'.</span><span class="sxs-lookup"><span data-stu-id="c0096-278">Now you are in **\_Layout.cshtml**, replace '**your logo here**' text with '**Photo Gallery**'.</span></span> <span data-ttu-id="c0096-279">저장 하 고 페이지 검사기 브라우저를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-279">Save and update the Page Inspector browser.</span></span>

    <span data-ttu-id="c0096-280">![새 제목을 할당](using-page-inspector-in-visual-studio-2012/_static/image22.png "새 제목을 할당")</span><span class="sxs-lookup"><span data-stu-id="c0096-280">![Assigning a new title](using-page-inspector-in-visual-studio-2012/_static/image22.png "Assigning a new title")</span></span>

    <span data-ttu-id="c0096-281">*새 제목을 할당*</span><span class="sxs-lookup"><span data-stu-id="c0096-281">*Assigning a new title*</span></span>

    ![PhotoGallerypage](using-page-inspector-in-visual-studio-2012/_static/image23.png)

    <span data-ttu-id="c0096-283">*사진 갤러리 페이지 업데이트*</span><span class="sxs-lookup"><span data-stu-id="c0096-283">*Photo Gallery page updated*</span></span>
11. <span data-ttu-id="c0096-284">마지막으로 선택 합니다 **PhotoGallery** 프로젝트 및 키를 눌러 **F5** 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-284">Finally, selet the **PhotoGallery** project and press **F5** to run the app.</span></span> <span data-ttu-id="c0096-285">모든 변경 내용이 예상 대로 작동을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-285">Check out all the changes work as expected.</span></span>

* * *

<a id="Exercise2"></a>

<a id="Exercise_2_Using_Page_Inspector_in_WebForms_Projects"></a>
### <a name="exercise-2-using-page-inspector-in-webforms-projects"></a><span data-ttu-id="c0096-286">WebForms 프로젝트에서 페이지 검사기를 사용 하는 연습 2:</span><span class="sxs-lookup"><span data-stu-id="c0096-286">Exercise 2: Using Page Inspector in WebForms Projects</span></span>

<span data-ttu-id="c0096-287">이 연습에서는 미리 보기 및 페이지 검사기를 사용 하 여 WebForms 솔루션을 디버그 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-287">In this exercise, you will learn how to preview and debug a WebForms solution using Page Inspector.</span></span> <span data-ttu-id="c0096-288">먼저 웹 디버깅 프로세스에 도움이 되는 페이지 검사기 기능에 대 한 간략 한 둘러보기 도구를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-288">You will first perform a brief lap around the tool to learn the Page Inspector features that facilitate the Web debugging process.</span></span> <span data-ttu-id="c0096-289">그런 다음 스타일 문제를 포함 하는 웹 페이지에서 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-289">Then, you will work in a web page that contains styling issues.</span></span> <span data-ttu-id="c0096-290">페이지 검사기를 사용 하 여 문제를 생성 하는 소스 코드를 수정 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-290">You will learn how to use Page Inspector to find the source code that generates the issue and fix it.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a><span data-ttu-id="c0096-291">작업 1-페이지 검사기를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-291">Task 1 - Exploring Page Inspector</span></span>

<span data-ttu-id="c0096-292">이 태스크에서는 사진 갤러리를 보여 주는 WebForms 프로젝트의 컨텍스트에서 페이지 검사기 기능을 사용 하는 방법을 배우게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-292">In this task, you will learn how to use the Page Inspector features in the context of a WebForms project that shows a photo gallery.</span></span>

1. <span data-ttu-id="c0096-293">엽니다는 **시작할** 솔루션에 있는 **소스/e x 2-WebForms/시작/** 폴더.</span><span class="sxs-lookup"><span data-stu-id="c0096-293">Open the **Begin** solution located at **Source/Ex2-WebForms/Begin/** folder.</span></span>

   1. <span data-ttu-id="c0096-294">일부 누락 된 NuGet 패키지를 다운로드 해야 하기 전에 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-294">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="c0096-295">이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-295">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="c0096-296">에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="c0096-296">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="c0096-297">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-297">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c0096-298">NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-298">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="c0096-299">NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-299">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="c0096-300">이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-300">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="c0096-301">솔루션 탐색기에서 찾습니다 **Default.aspx** 페이지를 마우스 오른쪽 단추로 클릭 하 고 선택 **페이지 검사기에서 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-301">In the Solution Explorer, locate **Default.aspx** page, right-click it and select **View in Page Inspector**.</span></span>

    <span data-ttu-id="c0096-302">![Default.aspx 페이지 검사기로 열기](using-page-inspector-in-visual-studio-2012/_static/image24.png "Default.aspx 페이지 검사기를 사용 하 여 열기")</span><span class="sxs-lookup"><span data-stu-id="c0096-302">![Opening Default.aspx with Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image24.png "Opening Default.aspx with Page Inspector")</span></span>

    <span data-ttu-id="c0096-303">*페이지 검사기를 사용 하 여 열기 Default.aspx*</span><span class="sxs-lookup"><span data-stu-id="c0096-303">*Opening Default.aspx with Page Inspector*</span></span>
3. <span data-ttu-id="c0096-304">페이지 검사기 창에는 Default.aspx 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-304">The Page Inspector window will show Default.aspx.</span></span>

    <span data-ttu-id="c0096-305">![페이지 검사기에서 Default.aspx를 보는](using-page-inspector-in-visual-studio-2012/_static/image25.png "Default.aspx 페이지 검사기에서 보기")</span><span class="sxs-lookup"><span data-stu-id="c0096-305">![Viewing Default.aspx in Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image25.png "Viewing Default.aspx in Page Inspector")</span></span>

    <span data-ttu-id="c0096-306">*Default.aspx 페이지 검사기에서 보기*</span><span class="sxs-lookup"><span data-stu-id="c0096-306">*Viewing Default.aspx in Page Inspector*</span></span>

    <span data-ttu-id="c0096-307">페이지 검사기 도구는 Visual Studio 환경에 통합 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-307">The Page Inspector tool is integrated in your Visual Studio environment.</span></span> <span data-ttu-id="c0096-308">검사기는 선택한 코드를 보여 주는 강력한 HTML 프로파일러 함께 포함 된 브라우저를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-308">The inspector contains an embedded browser, together with a powerful HTML profiler that will show the selected code.</span></span> <span data-ttu-id="c0096-309">확인 페이지에 표시 되는 방식을 확인 하려면 솔루션을 실행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-309">Notice that you do not have to run the solution to see how your pages look.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c0096-310">페이지 검사기 브라우저의 너비 열린된 페이지의 너비 보다 작은 경우 표시 되지 않습니다 페이지 적절 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-310">When the width of Page Inspector browser is less than the width of the opened page, you will not see the page properly.</span></span> <span data-ttu-id="c0096-311">이 경우 페이지 검사기의 너비를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-311">If that happens, adjust the width of the Page Inspector.</span></span>
4. <span data-ttu-id="c0096-312">클릭 합니다 **파일** 페이지 검사기에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-312">Click the **Files** tab in Page Inspector.</span></span>

    <span data-ttu-id="c0096-313">렌더링된 된 기본 페이지를 작성 하는 모든 소스 파일에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-313">You will see all the source files that are composing the rendered Default page.</span></span> <span data-ttu-id="c0096-314">이것이 사용자 컨트롤과 마스터 페이지를 사용 하 여 작업 하는 경우에 특히 눈에 모든 요소를 식별 하는 유용한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-314">This is a useful feature to identify all the elements at a glance, especially when you are working with User Controls and Master Pages.</span></span> <span data-ttu-id="c0096-315">각 파일을 이동할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-315">Notice that you can also navigate to each of the files.</span></span>

    <span data-ttu-id="c0096-316">![파일 탭](using-page-inspector-in-visual-studio-2012/_static/image26.png "The 파일 탭")</span><span class="sxs-lookup"><span data-stu-id="c0096-316">![The Files tab](using-page-inspector-in-visual-studio-2012/_static/image26.png "The Files tab")</span></span>

    <span data-ttu-id="c0096-317">*파일 탭*</span><span class="sxs-lookup"><span data-stu-id="c0096-317">*The Files tab*</span></span>
5. <span data-ttu-id="c0096-318">클릭 합니다 **검사 모드 설정/해제** 탭의 왼쪽에 있는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-318">Click the **Toggle Inspection Mode** button, located at the left of the tabs.</span></span>

    <span data-ttu-id="c0096-319">이 도구를 사용 하면 페이지의 모든 요소를 선택 하 고 해당 HTML 코드와.aspx 소스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="c0096-319">This tool will let you select any element of the page and see its HTML code and .aspx source.</span></span>

    <span data-ttu-id="c0096-320">![검사 모드 단추 토글](using-page-inspector-in-visual-studio-2012/_static/image27.png "검사 모드 설정/해제 단추")</span><span class="sxs-lookup"><span data-stu-id="c0096-320">![Toggle Inspection Mode button](using-page-inspector-in-visual-studio-2012/_static/image27.png "Toggle Inspection Mode button")</span></span>

    <span data-ttu-id="c0096-321">*설정/해제 검사 모드 단추*</span><span class="sxs-lookup"><span data-stu-id="c0096-321">*Toggle Inspection Mode button*</span></span>
6. <span data-ttu-id="c0096-322">페이지 검사기 브라우저에서 페이지 요소 위로 마우스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-322">In the Page Inspector browser, move the mouse over the page elements.</span></span> <span data-ttu-id="c0096-323">렌더링된 된 페이지 부분 위로 마우스 포인터를 이동 하는 동안 요소 형식이 표시 되 고 Visual Studio 편집기에서 해당 소스 태그나 코드가 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-323">While you move the mouse pointer over any part of the rendered page, the element type is displayed and the corresponding source markup or code is highlighted in the Visual Studio editor.</span></span>

    <span data-ttu-id="c0096-324">![실행 중인 검사 모드](using-page-inspector-in-visual-studio-2012/_static/image28.png "실행 중인 검사 모드")</span><span class="sxs-lookup"><span data-stu-id="c0096-324">![Inspection mode in action](using-page-inspector-in-visual-studio-2012/_static/image28.png "Inspection mode in action")</span></span>

    <span data-ttu-id="c0096-325">*실행 중인 검사 모드*</span><span class="sxs-lookup"><span data-stu-id="c0096-325">*Inspection mode in action*</span></span>

    > [!NOTE]
    > <span data-ttu-id="c0096-326">페이지 검사기 창을 최대화 하지 않습니다 또는 소스 코드를 보여 주는 미리 보기 탭을 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-326">Do not maximize the Page Inspector window or you will not be able to see the preview tab showing the source code.</span></span> <span data-ttu-id="c0096-327">최대화 되었을 때 페이지 검사기에서 요소를 클릭 하면 선택 항목의 소스 코드를 나타나지만 페이지 검사기 창에 게 숨겨집니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-327">If you click the element in Page Inspector when it is maximized, the source code of the selection will appear but it will hide the Page Inspector window.</span></span>

    <span data-ttu-id="c0096-328">경우에 주의 기울여야 **Default.aspx** 파일인 선택한 요소를 생성 하는 소스 코드의 부분을 강조 표시 되어 있는지을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-328">If you pay attention to **Default.aspx** file, you will notice that the portion of source code that generates the selected element is highlighted.</span></span> <span data-ttu-id="c0096-329">이 기능은 코드에 액세스 하는 직접 및 빠른 방법을 제공 하는 긴 원본 파일의 버전을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-329">This feature facilitates the edition of long source files, providing a direct and fast way to access the code.</span></span>

    <span data-ttu-id="c0096-330">![요소를 검사할](using-page-inspector-in-visual-studio-2012/_static/image29.png "요소를 검사 합니다.")</span><span class="sxs-lookup"><span data-stu-id="c0096-330">![Inspecting elements](using-page-inspector-in-visual-studio-2012/_static/image29.png "Inspecting elements")</span></span>

    <span data-ttu-id="c0096-331">*요소를 검사합니다.*</span><span class="sxs-lookup"><span data-stu-id="c0096-331">*Inspecting elements*</span></span>
7. <span data-ttu-id="c0096-332">클릭 합니다 **검사 모드 설정/해제** 단추 (![Select-the-HTML-tab-to-display-the-HTML-code-rendered-in-the-Page-Inspector-browser.] (using-page-inspector-in-visual-studio-2012/_static/image30.png "Select-the-HTML-tab-to-display-the-HTML-code-rendered-in-the-Page-Inspector-browser 합니다.")</span><span class="sxs-lookup"><span data-stu-id="c0096-332">Click the **Toggle Inspection Mode** button (![Select-the-HTML-tab-to-display-the-HTML-code-rendered-in-the-Page-Inspector-browser.](using-page-inspector-in-visual-studio-2012/_static/image30.png "Select-the-HTML-tab-to-display-the-HTML-code-rendered-in-the-Page-Inspector-browser.")</span></span> <span data-ttu-id="c0096-333">), 커서를 사용 하지 않도록 설정 페이지 검사기 탭에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-333">), located in Page Inspector tabs, to disable the cursor.</span></span>
8. <span data-ttu-id="c0096-334">선택 된 **HTML** 탭 페이지 검사기 브라우저에서 렌더링 된 HTML 코드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-334">Select the **HTML** tab to display the HTML code rendered in the Page Inspector browser.</span></span>
9. <span data-ttu-id="c0096-335">HTML 코드에서 Koala 링크를 사용 하 여 목록 항목을 찾아 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-335">In the HTML code, locate the list item with the Koala link and select it.</span></span>

    <span data-ttu-id="c0096-336">코드를 선택 하면 해당 출력은 자동으로 강조 표시 된 브라우저를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-336">Notice that when you select the code, the corresponding output is automatically highlighted browser.</span></span> <span data-ttu-id="c0096-337">이 기능은 HTML 블록을 페이지에 렌더링 되는 방법을 참조 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-337">This feature is useful to see how an HTML block is rendered on the page.</span></span>

    <span data-ttu-id="c0096-338">![페이지에서 HTML 요소 선택](using-page-inspector-in-visual-studio-2012/_static/image31.png "페이지에서 HTML 요소를 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="c0096-338">![Selecting an HTML element in the page](using-page-inspector-in-visual-studio-2012/_static/image31.png "Selecting an HTML element in the page")</span></span>

    <span data-ttu-id="c0096-339">*페이지에서 HTML 요소를 선택합니다.*</span><span class="sxs-lookup"><span data-stu-id="c0096-339">*Selecting an HTML element in the page*</span></span>
10. <span data-ttu-id="c0096-340">클릭 합니다 **검사 모드 설정/해제** 단추를 사용 하도록 설정 *검사 모드* 탐색 모음을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-340">Click the **Toggle Inspection Mode** button to enable *Inspection Mode* and click the navigation bar.</span></span> <span data-ttu-id="c0096-341">오른쪽의 HTML 코드의 스타일 창에서 선택한 요소에 적용 된 CSS 스타일을 사용 하 여 목록이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-341">On the right of the HTML code, in the Styles pane, you will see a list with the CSS styles applied to the selected element.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c0096-342">헤더 사이트 레이아웃의 일부분 이므로 페이지 검사기는 Site.Master 파일 열고 영향을 받는 코드의 세그먼트를 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-342">since the header is a part of the site layout, Page Inspector will also open Site.Master file and highlight the segment of code affected.</span></span>

    <span data-ttu-id="c0096-343">![DiscoveringstylesWebForms](using-page-inspector-in-visual-studio-2012/_static/image32.png "스타일 및 선택한 요소의 소스 파일 검색")</span><span class="sxs-lookup"><span data-stu-id="c0096-343">![DiscoveringstylesWebForms](using-page-inspector-in-visual-studio-2012/_static/image32.png "Discovering styles and source files of a selected element")</span></span>

    <span data-ttu-id="c0096-344">*스타일 및 선택한 요소의 소스 파일 검색*</span><span class="sxs-lookup"><span data-stu-id="c0096-344">*Discovering styles and source files of a selected element*</span></span>
11. <span data-ttu-id="c0096-345">사용 설정/해제 검사 포인터를 사용 하 여 메뉴 모음 아래 마우스 포인터를 이동 하 고 빈 절반 원을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-345">With the toggle inspection pointer enabled, move the mouse pointer below the menu bar and click the blank half circle.</span></span>

    <span data-ttu-id="c0096-346">![요소 선택](using-page-inspector-in-visual-studio-2012/_static/image33.png "요소 선택")</span><span class="sxs-lookup"><span data-stu-id="c0096-346">![Selecting an element](using-page-inspector-in-visual-studio-2012/_static/image33.png "Selecting an element")</span></span>

    <span data-ttu-id="c0096-347">*요소 선택*</span><span class="sxs-lookup"><span data-stu-id="c0096-347">*Selecting an element*</span></span>
12. <span data-ttu-id="c0096-348">스타일 창에서 찾을 합니다 **배경 이미지** 아래에 있는 항목을 **.main 콘텐츠** 그룹.</span><span class="sxs-lookup"><span data-stu-id="c0096-348">In the Styles pane, locate the **background-image** item under the **.main-content** group.</span></span> <span data-ttu-id="c0096-349">**선택 취소** 는 **배경 이미지** 를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-349">**Uncheck** the **background-image** and see what happens.</span></span> <span data-ttu-id="c0096-350">브라우저는 변경 내용의 즉시 반영 됩니다 하 원 숨겨지는지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-350">You will notice that the browser will reflect the changes immediately and the circle is hidden.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c0096-351">페이지 검사기 스타일 탭에 적용할 변경 내용을 원래 스타일 시트는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-351">The changes you apply on the Page Inspector Styles tab do not affect the original stylesheet.</span></span> <span data-ttu-id="c0096-352">스타일을 선택 취소 하거나 만큼 있지만 페이지를 새로 고친 후 복원할 수는 해당 값을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-352">You can uncheck styles or change their values as many times as you want, but they will be restored after refreshing the page.</span></span>

    <span data-ttu-id="c0096-353">![설정 및 해제 CSS styles2](using-page-inspector-in-visual-studio-2012/_static/image34.png "및 CSS 스타일을 사용 하지 않도록 설정")</span><span class="sxs-lookup"><span data-stu-id="c0096-353">![Enabling and disabling CSS styles2](using-page-inspector-in-visual-studio-2012/_static/image34.png "Enabling and disabling CSS styles")</span></span>

    <span data-ttu-id="c0096-354">*설정 및 CSS 스타일을 사용 하지 않도록 설정*</span><span class="sxs-lookup"><span data-stu-id="c0096-354">*Enabling and disabling CSS styles*</span></span>
13. <span data-ttu-id="c0096-355">이제 클릭을 '**프로그램** **로고는 여기 '** 검사 모드를 사용 하 여 헤더 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-355">Now, click the '**your** **logo here'** text on the header using the inspection mode.</span></span>
14. <span data-ttu-id="c0096-356">에 **스타일** 탭에서 찾을 **글꼴 크기** 에서 CSS 특성를 **.site 제목** 그룹.</span><span class="sxs-lookup"><span data-stu-id="c0096-356">In the **Styles** tab, locate the **font-size** CSS attribute under the **.site-title** group.</span></span> <span data-ttu-id="c0096-357">해당 값을 편집 하려면 특성을 한 번를 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-357">Double-click the attribute once to edit its value.</span></span> <span data-ttu-id="c0096-358">값 바꾸기는 2.3em **3em**, 한 다음 ENTER를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-358">Replace the 2.3em value with **3em**, and then press ENTER.</span></span> <span data-ttu-id="c0096-359">제목을 더 큰 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-359">Notice that the title looks bigger.</span></span>

    <span data-ttu-id="c0096-360">![페이지 Inspector2에서 CSS 값을 변경](using-page-inspector-in-visual-studio-2012/_static/image35.png "페이지 검사기에서 CSS 변경 값")</span><span class="sxs-lookup"><span data-stu-id="c0096-360">![Changing CSS values in the Page Inspector2](using-page-inspector-in-visual-studio-2012/_static/image35.png "Changing CSS values in the Page Inspector")</span></span>

    <span data-ttu-id="c0096-361">*페이지 검사기에서 CSS 값을 변경*</span><span class="sxs-lookup"><span data-stu-id="c0096-361">*Changing CSS values in the Page Inspector*</span></span>
15. <span data-ttu-id="c0096-362">클릭 합니다 **스타일 추적** 페이지 검사기의 오른쪽 창에 있는 탭입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-362">Click the **Trace Styles** tab, located in the right pane of Page Inspector.</span></span> <span data-ttu-id="c0096-363">이것이 특성 이름별으로 정렬 하 고 선택 항목을 적용할 모든 스타일을 참조 하는 대체 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-363">This is an alternative way to see all the styles applied to the selection, ordered by attribute name.</span></span>

    <span data-ttu-id="c0096-364">![선택한 요소의 CSS 스타일 추적](using-page-inspector-in-visual-studio-2012/_static/image36.png "선택한 요소의 CSS 스타일 추적")</span><span class="sxs-lookup"><span data-stu-id="c0096-364">![CSS styles tracing of the selected element](using-page-inspector-in-visual-studio-2012/_static/image36.png "CSS styles tracing of the selected element")</span></span>

    <span data-ttu-id="c0096-365">*선택한 요소의 CSS 스타일 추적*</span><span class="sxs-lookup"><span data-stu-id="c0096-365">*CSS styles tracing of the selected element*</span></span>
16. <span data-ttu-id="c0096-366">페이지 검사기의 또 다른 기능은 레이아웃 창입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-366">Another feature of Page Inspector is the Layout pane.</span></span> <span data-ttu-id="c0096-367">탐색 모음을 선택한 다음 클릭 검사 모드를 사용 하 여 **레이아웃** 오른쪽 창에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-367">Using the inspection mode, select the navigation bar and then click the **Layout** tab on the right pane.</span></span> <span data-ttu-id="c0096-368">선택한 요소의 정확한 크기와 오프셋, 여백, 안쪽 여백 및 테두리 크기를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-368">You will see the exact size of the selected element, as well as its offset, margin, padding and border size.</span></span> <span data-ttu-id="c0096-369">이 보기에서 값을 수정할 수도 있습니다 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-369">Notice that you can also modify the values from this view.</span></span>

    <span data-ttu-id="c0096-370">![페이지 검사기에서 요소 레이아웃](using-page-inspector-in-visual-studio-2012/_static/image37.png "페이지 검사기에서 요소 레이아웃")</span><span class="sxs-lookup"><span data-stu-id="c0096-370">![Element layout in Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image37.png "Element layout in Page Inspector")</span></span>

    <span data-ttu-id="c0096-371">*페이지 검사기에서 요소 레이아웃*</span><span class="sxs-lookup"><span data-stu-id="c0096-371">*Element layout in Page Inspector*</span></span>

<a id="Ex2Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a><span data-ttu-id="c0096-372">작업 2-찾기 및 사진 갤러리에서 스타일 문제 해결</span><span class="sxs-lookup"><span data-stu-id="c0096-372">Task 2 - Finding and Fixing Style Issues in the Photo Gallery</span></span>

<span data-ttu-id="c0096-373">이전 버전의 Visual Studio를 사용 하 여 웹 페이지 문제를 진단 하는 어떻게는?</span><span class="sxs-lookup"><span data-stu-id="c0096-373">How would you diagnose Web pages issues with previous versions of Visual Studio?</span></span> <span data-ttu-id="c0096-374">Internet Explorer 개발자 도구 또는 Firebug와 같은 Visual Studio IDE 외부에서 실행 되는 도구를 디버깅 하는 웹 익숙할 것 이며</span><span class="sxs-lookup"><span data-stu-id="c0096-374">You are likely familiar with web debugging tools that run outside the Visual Studio IDE, like Internet Explorer Developer Tools or Firebug.</span></span> <span data-ttu-id="c0096-375">브라우저에만 HTML 이해 스크립팅 및 스타일, 기본 프레임 워크를 렌더링할 HTML을 생성 하는 동안.</span><span class="sxs-lookup"><span data-stu-id="c0096-375">Browsers only understand HTML, scripting and styles, while an underlying framework generates the HTML that will be rendered.</span></span> <span data-ttu-id="c0096-376">이런 이유로 웹 페이지와 같은 어떻게 표시 되는지 확인 하려면 전체 사이트를 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-376">For that reason, you often need to deploy the whole site to see how web pages look like.</span></span>

<span data-ttu-id="c0096-377">아마도 감지 하 고 웹 사이트에서 문제를 해결 하려는 경우 다음이 단계를 수행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-377">You had probably followed these steps when you wanted to detect and fix an issue in your web site:</span></span>

1. <span data-ttu-id="c0096-378">Visual Studio에서 솔루션을 실행 하거나 웹 서버에서 페이지를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-378">Run the Solution from Visual Studio, or deploy the page on the web server.</span></span>
2. <span data-ttu-id="c0096-379">브라우저에서 개발자 도구를 사용 하거나 단순히 소스 코드와 스타일을 열고 문제 일치 시 키 려를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-379">In the browser, open the developer tools you use, or simply open the source code and the styles and try to match the issue.</span></span> <span data-ttu-id="c0096-380">관련 된 파일을 찾을 사용 하는 합니다 &quot;검색&quot; 또는 &quot;파일에서 검색&quot; 스타일 클래스 이름 사용 하 여 기능 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-380">To find the files involved, you'd have used the &quot;Search&quot; or &quot;Search in files&quot; features with the name of the style classes.</span></span>
3. <span data-ttu-id="c0096-381">오류가 감지 되 면 웹 브라우저 및 서버를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-381">Once the error is detected, stop the Web browser and the server.</span></span>
4. <span data-ttu-id="c0096-382">브라우저 캐시를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-382">Clear the browser cache.</span></span>
5. <span data-ttu-id="c0096-383">수정 프로그램을 적용 하려면 Visual Studio로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-383">Return to Visual Studio to apply a fix.</span></span> <span data-ttu-id="c0096-384">테스트 하는 모든 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-384">Repeat all the steps to test.</span></span>

<span data-ttu-id="c0096-385">더 실제 wysiwyg (위지윅)에서 ASP.NET WebForms, 일부 스타일 문제를 실행 또는 배포 후 이후 단계에서 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-385">As there is no real WYSIWYG in ASP.NET WebForms, some style issues are detected on a later stage, after running or deploying.</span></span> <span data-ttu-id="c0096-386">이제 페이지 검사기를 사용 하 여 솔루션을 실행 하지 않고 모든 페이지를 미리 보려면는 것이 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-386">Now, with Page Inspector, it is possible to preview any page without running the solution.</span></span>

<span data-ttu-id="c0096-387">이 태스크에서는 사진 갤러리 응용 프로그램의 몇 가지 문제를 해결 하기 위한 페이지 검사기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-387">In this task, you will use the Page inspector for fixing some issues of the Photo Gallery application.</span></span> <span data-ttu-id="c0096-388">다음 단계에서 검색 한 신속 하 게 헤더에 몇 가지 간단한 스타일 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-388">In the following steps, you will detect and quickly fix some simple styling issue in the header.</span></span>

1. <span data-ttu-id="c0096-389">페이지 검사를 사용 하 여 찾습니다 합니다 **등록** 하며 **로그인** 헤더의 왼쪽에 있는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-389">Using Page Inspection, locate the **Register** and the **Log In** links at the left side of the header.</span></span>

    <span data-ttu-id="c0096-390">링크를 오른쪽에 예상된 된 위치에 표시 되지 않도록 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-390">Notice that the link is not displayed at the expected place on the right.</span></span> <span data-ttu-id="c0096-391">이제 오른쪽에 대 한 링크를 정렬 하 고 적절 하 게 스타일을 다시 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-391">You will now align the link to the right and restyle it accordingly.</span></span>

    <span data-ttu-id="c0096-392">![왼쪽에 배치 하는 링크에 로그인](using-page-inspector-in-visual-studio-2012/_static/image38.png "왼쪽에 배치 하는 링크에 로그인")</span><span class="sxs-lookup"><span data-stu-id="c0096-392">![Log in link positioned on the left](using-page-inspector-in-visual-studio-2012/_static/image38.png "Log in link positioned on the left")</span></span>

    <span data-ttu-id="c0096-393">*로그인 링크는 왼쪽에 배치*</span><span class="sxs-lookup"><span data-stu-id="c0096-393">*Log In link positioned on the left*</span></span>
2. <span data-ttu-id="c0096-394">선택한 검사 모드를 설정/해제를 사용 하 여 해당 코드를 열고 로그인 링크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-394">With Toggle Inspection Mode selected, select the Log In link to open its code.</span></span>

    <span data-ttu-id="c0096-395">링크 소스 코드에 있는 알림 합니다 **Site.Master** 파일 위치는 Default.aspx 페이지의 첫 번째 위치에서 볼 수 있습니다 하지; 올바른 소스 파일에서 직접 전환할 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-395">Notice that the link source code is located in the **Site.Master** file, not in the Default.aspx page which is the place you might look in first place; you have been placed directly in the correct source file.</span></span>
3. <span data-ttu-id="c0096-396">에 **스타일** 탭을 찾아 클릭 합니다  **&lt;섹션&gt; #login** 항목 이러한 링크의 HTML 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-396">In the **Styles** tab, locate and click the **&lt;section&gt; #login** item, which is the HTML container for these links.</span></span>

    <span data-ttu-id="c0096-397">있음을 합니다 **#login** 스타일에 자동으로 위치한 **Site.css** 클릭 한 후입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-397">Notice that the **#login** style is automatically located in **Site.css** after you click.</span></span> <span data-ttu-id="c0096-398">또한 코드는 이제 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-398">Moreover, the code is now highlighted.</span></span>

    <span data-ttu-id="c0096-399">![CSS 스타일을 선택 하면](using-page-inspector-in-visual-studio-2012/_static/image39.png "CSS 스타일을 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="c0096-399">![Selecting the CSS styles](using-page-inspector-in-visual-studio-2012/_static/image39.png "Selecting the CSS styles")</span></span>

    <span data-ttu-id="c0096-400">*CSS 스타일을 선택합니다.*</span><span class="sxs-lookup"><span data-stu-id="c0096-400">*Selecting the CSS styles*</span></span>
4. <span data-ttu-id="c0096-401">주석 처리를 제거 합니다 **텍스트 맞춤** 을 열고 닫는 문자를 제거 하 여 강조 표시 된 코드에서 특성 및 저장 합니다 **Site.css** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-401">Uncomment the **text-align** attribute in the highlighted code by removing the opening and closing characters and save the **Site.css** file.</span></span>

    <span data-ttu-id="c0096-402">페이지 검사기는 현재 페이지를 구성 하는 모든 다른 파일을 인식 하 고 이러한 파일 중 하나를 변경 하는 경우 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-402">Page Inspector is aware of all the different files that compose the current page, and it can detect when any of these files change.</span></span> <span data-ttu-id="c0096-403">사용자에 게 경고 때마다 브라우저에서 현재 페이지 원본 파일과 함께 동기화 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-403">It alerts you whenever the current page in browser is not in sync with the source files.</span></span>
5. <span data-ttu-id="c0096-404">페이지 검사기 브라우저에서 변경 내용을 저장 하 고 페이지를 다시 로드 주소 표시줄 아래에 있는 막대를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-404">In the Page Inspector browser, click the bar located below the address bar to save the changes and reload the page.</span></span>

    ![Reloadingthepage](using-page-inspector-in-visual-studio-2012/_static/image40.png)

    <span data-ttu-id="c0096-406">*페이지를 다시 로드*</span><span class="sxs-lookup"><span data-stu-id="c0096-406">*Reloading the page*</span></span>

    <span data-ttu-id="c0096-407">오른쪽에서 링크 됩니다 있지만 여전히 글머리 기호 목록 처럼 보입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-407">The links are now at the right, but they still look like a bulleted list.</span></span> <span data-ttu-id="c0096-408">이제 글머리 기호 제거 및 링크를 가로로 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-408">Now, you will remove the bullets and align the links horizontally.</span></span>

    ![업데이트 된 페이지](using-page-inspector-in-visual-studio-2012/_static/image41.png)

    <span data-ttu-id="c0096-410">*업데이트 된 페이지*</span><span class="sxs-lookup"><span data-stu-id="c0096-410">*Updated page*</span></span>
6. <span data-ttu-id="c0096-411">중 하나를 선택 하는 검사 모드를 사용 하 여 합니다 **&lt;li&gt;** 포함 된 항목을 &quot;등록&quot; 및 &quot;로그인&quot; 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-411">Using the inspection mode, select any of the **&lt;li&gt;** items that contain the &quot;Register&quot; and &quot;Log in&quot; links.</span></span> <span data-ttu-id="c0096-412">클릭 합니다  **&lt;섹션&gt; #login** 액세스 항목 **Styles.css** 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-412">Then, click the **&lt;section&gt; #login** item to access **Styles.css** code.</span></span>

    <span data-ttu-id="c0096-413">![스타일 찾기](using-page-inspector-in-visual-studio-2012/_static/image42.png "스타일 찾기")</span><span class="sxs-lookup"><span data-stu-id="c0096-413">![Finding the style](using-page-inspector-in-visual-studio-2012/_static/image42.png "Finding the style")</span></span>

    <span data-ttu-id="c0096-414">*스타일 찾기*</span><span class="sxs-lookup"><span data-stu-id="c0096-414">*Finding the style*</span></span>
7. <span data-ttu-id="c0096-415">**Style.css**에 대 한 코드를 주석 처리 제거 **#login li** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-415">In **Style.css**, uncomment the code for **#login li** items.</span></span> <span data-ttu-id="c0096-416">추가할 스타일 글머리 숨기고 항목 가로로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-416">The style you are adding will hide the bullet and display the items horizontally.</span></span>

    <span data-ttu-id="c0096-417">![로그인 링크를 재지정](using-page-inspector-in-visual-studio-2012/_static/image43.png "로그인 링크를 재지정")</span><span class="sxs-lookup"><span data-stu-id="c0096-417">![Restyling the login links](using-page-inspector-in-visual-studio-2012/_static/image43.png "Restyling the login links")</span></span>

    <span data-ttu-id="c0096-418">*로그인 링크를 재지정*</span><span class="sxs-lookup"><span data-stu-id="c0096-418">*Restyling the login links*</span></span>
8. <span data-ttu-id="c0096-419">저장할 **Style.css** 파일 및 페이지를 다시 로드 하는 주소 아래에 있는 표시줄에서 한 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-419">Save **Style.css** file and click once on the bar located below the address to reload the page.</span></span> <span data-ttu-id="c0096-420">링크를 올바르게 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-420">Notice that the links appear correctly.</span></span>

    <span data-ttu-id="c0096-421">![링크는 왼쪽에서 오른쪽으로 정렬](using-page-inspector-in-visual-studio-2012/_static/image44.png "링크는 왼쪽에서 오른쪽으로 정렬")</span><span class="sxs-lookup"><span data-stu-id="c0096-421">![Links aligned to the right side](using-page-inspector-in-visual-studio-2012/_static/image44.png "Links aligned to the right side")</span></span>

    <span data-ttu-id="c0096-422">*왼쪽에서 오른쪽으로 정렬 하는 링크*</span><span class="sxs-lookup"><span data-stu-id="c0096-422">*Links aligned to the right side*</span></span>
9. <span data-ttu-id="c0096-423">마지막으로 머리글 제목을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-423">Finally, you will change the header title.</span></span> <span data-ttu-id="c0096-424">에 대 한 검색 하는 대신는 '**사용자 로고는 여기 '** 검사 모드는 텍스트를 클릭 하 고 생성 하는 소스 코드를 가져오면를 사용 하는 모든 파일에 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-424">Instead of searching for the '**your logo here'** text in all the files, use the inspection mode to click the text and get to source code that generates it.</span></span>

    <span data-ttu-id="c0096-425">![사이트 제목 찾기](using-page-inspector-in-visual-studio-2012/_static/image45.png "사이트 제목 찾기")</span><span class="sxs-lookup"><span data-stu-id="c0096-425">![Finding the site title](using-page-inspector-in-visual-studio-2012/_static/image45.png "Finding the site title")</span></span>

    <span data-ttu-id="c0096-426">*사이트 제목 찾기*</span><span class="sxs-lookup"><span data-stu-id="c0096-426">*Finding the site title*</span></span>
10. <span data-ttu-id="c0096-427">에 이제 **Site.Master**, 대체는 '**사용자 로고는 여기**'텍스트'**사진 갤러리**'.</span><span class="sxs-lookup"><span data-stu-id="c0096-427">Now you are in **Site.Master**, replace the '**your logo here**' text with '**Photo Gallery**'.</span></span> <span data-ttu-id="c0096-428">저장 하 고 페이지 검사기 브라우저를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-428">Save and update the Page Inspector browser.</span></span>

    <span data-ttu-id="c0096-429">![사진 갤러리 페이지 업데이트](using-page-inspector-in-visual-studio-2012/_static/image46.png "사진 갤러리 페이지 업데이트")</span><span class="sxs-lookup"><span data-stu-id="c0096-429">![Photo Gallery page updated](using-page-inspector-in-visual-studio-2012/_static/image46.png "Photo Gallery page updated")</span></span>

    <span data-ttu-id="c0096-430">*사진 갤러리 페이지 업데이트*</span><span class="sxs-lookup"><span data-stu-id="c0096-430">*Photo Gallery page updated*</span></span>
11. <span data-ttu-id="c0096-431">마지막으로 누릅니다 **F5** 체크 아웃 변경 내용이 예상 대로 작동 하는 모든 앱을 실행 하려면.</span><span class="sxs-lookup"><span data-stu-id="c0096-431">Finally press **F5** to run the app the check out all the changes work as expected.</span></span>

* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="c0096-432">요약</span><span class="sxs-lookup"><span data-stu-id="c0096-432">Summary</span></span>

<span data-ttu-id="c0096-433">이 실습을 완료 하면 페이지 검사기를 사용 하 여 웹 응용 프로그램을 다시 빌드하고 브라우저에서 웹 사이트를 실행 하지 않고도 미리 하는 방법을 배웠습니다 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-433">By completing this Hands-On Lab, you have learnt how to use Page Inspector to preview your Web application without having to rebuild and run the Web site in a browser.</span></span> <span data-ttu-id="c0096-434">또한 신속 하 게 찾기 및 소스 코드에 렌더링된 된 출력에서 직접 액세스 하 여 버그를 수정 하는 방법에 배운 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-434">In addition, you have learnt how to quickly find and fix bugs by accessing directly from the rendered output to the source code.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="c0096-435">부록 a: 설치 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="c0096-435">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="c0096-436">설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 사용 하 여 버전을 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="c0096-436">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="c0096-437">다음 지침을 설치 하는 데 필요한 단계를 안내 *Visual studio Express 2012 for Web* 사용 하 여 *Microsoft Web Platform Installer*합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-437">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="c0096-438">로 이동 [ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-438">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="c0096-439">또는, 이미 설치한 경우 웹 플랫폼 설치 관리자를 열 수 있습니다 하 고 제품에 대 한 검색 &quot; <em>Visual Studio Express 2012 for Windows Azure SDK를 사용 하 여 Web</em>&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-439">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="c0096-440">클릭할 **지금 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-440">Click on **Install Now**.</span></span> <span data-ttu-id="c0096-441">없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-441">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="c0096-442">한 번 **웹 플랫폼 설치 관리자** 열려 있는 경우 클릭 **설치** 는 설치를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-442">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="c0096-443">![Visual Studio Express를 설치](using-page-inspector-in-visual-studio-2012/_static/image47.png "Visual Studio Express를 설치 합니다.")</span><span class="sxs-lookup"><span data-stu-id="c0096-443">![Install Visual Studio Express](using-page-inspector-in-visual-studio-2012/_static/image47.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="c0096-444">*Visual Studio Express를 설치 합니다.*</span><span class="sxs-lookup"><span data-stu-id="c0096-444">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="c0096-445">모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-445">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![사용 조건에 동의](using-page-inspector-in-visual-studio-2012/_static/image48.png)

    <span data-ttu-id="c0096-447">*사용 조건에 동의*</span><span class="sxs-lookup"><span data-stu-id="c0096-447">*Accepting the license terms*</span></span>
5. <span data-ttu-id="c0096-448">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-448">Wait until the downloading and installation process completes.</span></span>

    ![설치 진행률](using-page-inspector-in-visual-studio-2012/_static/image49.png)

    <span data-ttu-id="c0096-450">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="c0096-450">*Installation progress*</span></span>
6. <span data-ttu-id="c0096-451">설치가 완료 되 면 클릭 **완료**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-451">When the installation completes, click **Finish**.</span></span>

    ![설치 완료](using-page-inspector-in-visual-studio-2012/_static/image50.png)

    <span data-ttu-id="c0096-453">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="c0096-453">*Installation completed*</span></span>
7. <span data-ttu-id="c0096-454">클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-454">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="c0096-455">로 Visual Studio Express for Web을 열려면 합니다 **시작** 화면 및 쓰기를 시작 &quot; **VS Express**&quot;를 클릭 합니다 **VS Express for Web** 타일입니다.</span><span class="sxs-lookup"><span data-stu-id="c0096-455">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 타일](using-page-inspector-in-visual-studio-2012/_static/image51.png)

    <span data-ttu-id="c0096-457">*VS Express for Web 타일*</span><span class="sxs-lookup"><span data-stu-id="c0096-457">*VS Express for Web tile*</span></span>
