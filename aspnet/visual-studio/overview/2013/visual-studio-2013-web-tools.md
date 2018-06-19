---
uid: visual-studio/overview/2013/visual-studio-2013-web-tools
title: '실습 랩: Visual Studio 2013 웹 도구 | Microsoft Docs'
author: rick-anderson
description: Visual Studio는에 대 한 뛰어난 개발 환경입니다. 또한 Windows 및 웹 프로젝트입니다. 쉽게 사용할 수 있는 강력한 텍스트 편집기를 포함...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/16/2014
ms.topic: article
ms.assetid: 09e82351-816b-402d-acd1-0f9ac6901d16
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /visual-studio/overview/2013/visual-studio-2013-web-tools
msc.type: authoredcontent
ms.openlocfilehash: ef8ab82f9043ef9da3a3e6a146a97f083149534d
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2018
ms.locfileid: "26507132"
---
<a name="hands-on-lab-visual-studio-2013-web-tools"></a><span data-ttu-id="fbb56-104">실습 랩: Visual Studio 2013 웹 도구</span><span class="sxs-lookup"><span data-stu-id="fbb56-104">Hands On Lab: Visual Studio 2013 Web Tools</span></span>
====================
<span data-ttu-id="fbb56-105">으로 [웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="fbb56-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="fbb56-106">웹 캠프 학습 키트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-106">Download Web Camps Training Kit</span></span>](http://aka.ms/webcamps-training-kit)

> <span data-ttu-id="fbb56-107">Visual Studio는에 대 한 뛰어난 개발 환경입니다. 또한 Windows 및 웹 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-107">Visual Studio is an excellent development environment for .NET-based Windows and web projects.</span></span> <span data-ttu-id="fbb56-108">쉽게 프로젝트 없이 독립 실행형 파일을 편집 하는 데 사용할 수 있는 강력한 텍스트 편집기를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-108">It includes a powerful text editor that can easily be used to edit standalone files without a project.</span></span>
> 
> <span data-ttu-id="fbb56-109">각 파일을 편집할 때 visual Studio는 모든 기능을 갖춘 구문 분석 트리를 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-109">Visual Studio maintains a full-featured parse tree as you edit each file.</span></span> <span data-ttu-id="fbb56-110">이렇게 하면 훨씬 빠르고 더 쾌적 한 개발 환경을 만드는 동안 최상의 자동 완성 기능 및 문서 기반 동작을 제공 하는 Visual Studio 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-110">This allows Visual Studio to provide unparalleled auto-completion and document-based actions while making the development experience much faster and more pleasant.</span></span> <span data-ttu-id="fbb56-111">이러한 기능은 HTML 및 CSS 문서에서 특히 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-111">These features are especially powerful in HTML and CSS documents.</span></span>
> 
> <span data-ttu-id="fbb56-112">이 전원의 모든 확장의 경우 필요에 따라 강력한 새 기능으로 편집기를 확장 하 여 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-112">All of this power is also available for extensions, making it simple to extend the editors with powerful new features to suit your needs.</span></span> <span data-ttu-id="fbb56-113">웹 Essentials은 대부분 웹 관련 향상 된 Visual Studio의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-113">Web Essentials is a collection of (mostly) web-related enhancements to Visual Studio.</span></span> <span data-ttu-id="fbb56-114">(특히 CSS)에 대해 새 IntelliSense 완성, 새로운 브라우저 링크 기능으로, 자동 많이 포함 JSHint JavaScript에 대 한 파일, HTML 및 CSS 및 최신 웹 개발에 꼭 필요한 기타 많은 기능에 대 한 새 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-114">It includes lots of new IntelliSense completions (especially for CSS), new Browser Link features, automatic JSHint for JavaScript files, new warnings for HTML and CSS, and many other features that are essential to modern web development.</span></span>
> 
> <span data-ttu-id="fbb56-115">모든 샘플 코드와 코드 조각을 웹 캠프 교육 키트에서 사용할 수에 포함 된 [ http://aka.ms/webcamps-training-kit ](http://aka.ms/webcamps-training-kit)합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-115">All sample code and snippets are included in the Web Camps Training Kit, available at [http://aka.ms/webcamps-training-kit](http://aka.ms/webcamps-training-kit).</span></span>


<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="fbb56-116">개요</span><span class="sxs-lookup"><span data-stu-id="fbb56-116">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="fbb56-117">목표</span><span class="sxs-lookup"><span data-stu-id="fbb56-117">Objectives</span></span>

<span data-ttu-id="fbb56-118">이 실습 랩에서 배웁니다 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="fbb56-118">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="fbb56-119">풍부한 HTML5 코드 조각 및 Zen 코딩 등 웹 Essentials에 포함 된 새 HTML 편집기 기능을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="fbb56-119">Use new HTML editor features included in Web Essentials such as rich HTML5 code snippets and Zen coding</span></span>
- <span data-ttu-id="fbb56-120">색 선택 및 브라우저 매트릭스 도구 설명 같은 웹 Essentials에 포함 된 새 CSS 편집기 기능을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="fbb56-120">Use new CSS editor features included in Web Essentials such as the Color picker and Browser matrix tooltip</span></span>
- <span data-ttu-id="fbb56-121">모든 HTML 요소에 대 한 IntelliSense 파일을 추출 같은 웹 Essentials에 포함 된 새로운 JavaScript 편집기 기능을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="fbb56-121">Use new JavaScript editor features included in Web Essentials such as Extract to File and IntelliSense for all HTML elements</span></span>
- <span data-ttu-id="fbb56-122">브라우저 및 브라우저 링크를 사용 하 여 Visual Studio 사이 데이터 교환</span><span class="sxs-lookup"><span data-stu-id="fbb56-122">Exchange data between your browser and Visual Studio using Browser Link</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="fbb56-123">전제 조건</span><span class="sxs-lookup"><span data-stu-id="fbb56-123">Prerequisites</span></span>

<span data-ttu-id="fbb56-124">다음은이 실습 랩을 완료 하려면 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-124">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="fbb56-125">[Microsoft Visual Studio Professional 2013](https://www.microsoft.com/visualstudio/) 이상</span><span class="sxs-lookup"><span data-stu-id="fbb56-125">[Microsoft Visual Studio Professional 2013](https://www.microsoft.com/visualstudio/) or greater</span></span>
- [<span data-ttu-id="fbb56-126">Web Essentials 2013</span><span class="sxs-lookup"><span data-stu-id="fbb56-126">Web Essentials 2013</span></span>](http://vswebessentials.com/)
- [<span data-ttu-id="fbb56-127">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="fbb56-127">Google Chrome</span></span>](https://www.google.com/chrome/)

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="fbb56-128">설정</span><span class="sxs-lookup"><span data-stu-id="fbb56-128">Setup</span></span>

<span data-ttu-id="fbb56-129">이 실습 랩에서 연습을 실행 하려면 먼저 환경을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-129">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="fbb56-130">Windows 탐색기 창을 열고 다음을 찾아보기에 랩 **소스** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-130">Open a Windows Explorer window and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="fbb56-131">마우스 오른쪽 단추로 클릭 **Setup.cmd** 선택 **관리자 권한으로 실행** 환경을 구성 되며이 랩에 대 한 Visual Studio 코드 조각을 설치 하는 설치 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-131">Right-click **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="fbb56-132">사용자 계정 컨트롤 대화 상자가 표시 되 면 계속 하려면 작업을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-132">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="fbb56-133">설치 프로그램을 실행 하기 전에이 랩에 대 한 모든 종속성을 선택 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-133">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>


<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="fbb56-134">코드 조각을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="fbb56-134">Using the Code Snippets</span></span>

<span data-ttu-id="fbb56-135">랩 문서를 통해 코드 블록을 삽입 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-135">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="fbb56-136">사용자 편의 위해이 코드의 대부분을 수동으로 추가할 필요가 없도록 하려면 Visual Studio 2013 내에서 액세스할 수 있는 Visual Studio 코드 조각으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-136">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="fbb56-137">각 연습에는 시작 솔루션 동반 되는 **시작** 개별적으로 각 연습에 따라 할 수 있는 작업의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-137">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="fbb56-138">주의 하십시오 연습 하는 동안 추가 된 코드 조각은 솔루션 시작이 항목에서 누락 되어 연습을 완료 될 때까지 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-138">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="fbb56-139">실행에 대 한 소스 코드에서 찾아볼 수 있습니다는 **끝** 해당 연습에서 단계를 완료 한 결과인 코드와 함께 Visual Studio 솔루션에 포함 된 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-139">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="fbb56-140">이 실습 랩에서 진행할 때는 추가 도움이 필요한 경우 이러한 솔루션 가이드로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-140">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>


* * *

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="fbb56-141">연습</span><span class="sxs-lookup"><span data-stu-id="fbb56-141">Exercises</span></span>

<span data-ttu-id="fbb56-142">이 실습 랩에서 다음 연습에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-142">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="fbb56-143">브라우저 링크 및 웹 Essentials 작업</span><span class="sxs-lookup"><span data-stu-id="fbb56-143">Working with Browser Link and Web Essentials</span></span>](#Exercise1)
2. [<span data-ttu-id="fbb56-144">코드 조각 및 IntelliSense를 활용 하기 위해</span><span class="sxs-lookup"><span data-stu-id="fbb56-144">Taking Advantage of Code Snippets and IntelliSense</span></span>](#Exercise2)

> [!NOTE]
> <span data-ttu-id="fbb56-145">Visual Studio를 처음 시작 하면 미리 정의 된 설정 컬렉션 중 하나를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-145">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="fbb56-146">미리 정의 된 각 컬렉션 특정 개발 스타일에 맞게 설계 하 고 창 레이아웃, 편집기 동작, IntelliSense 코드 조각 및 대화 상자 옵션을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-146">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="fbb56-147">이 랩의 절차를 사용 하는 경우 Visual Studio에서 지정 된 작업을 수행 하는 데 필요한 작업 설명에서 **일반 개발 설정** 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-147">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="fbb56-148">개발 환경에 대 한 서로 다른 설정 컬렉션을 선택 하면 고려해 야 하는 단계에 차이가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-148">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>


<a id="Exercise1"></a>
### <a name="exercise-1-working-with-browser-link-and-web-essentials"></a><span data-ttu-id="fbb56-149">브라우저 링크 및 웹 Essentials 연습 1: 작업</span><span class="sxs-lookup"><span data-stu-id="fbb56-149">Exercise 1: Working with Browser Link and Web Essentials</span></span>

<span data-ttu-id="fbb56-150">**Essentials 웹** 다양 한 웹 개발 환경을 훨씬 빠르고 편리한에 주로 초점을 최신 웹 개발을 위한 유용한 기능을 추가 하는 Visual Studio 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-150">**Web Essentials** is a Visual Studio extension that adds a variety of useful features for modern web development, mostly focused on making the web development experience much faster and more pleasant.</span></span> <span data-ttu-id="fbb56-151">Visual Studio에서 확장 갤러리에서 웹 Essentials를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-151">You can install Web Essentials from the Extension Gallery in Visual Studio.</span></span>

<span data-ttu-id="fbb56-152">**브라우저 링크** 웹 응용 프로그램 및 Visual Studio 간에 데이터를 교환 하기 위해 Visual Studio IDE와 모든 열려 있는 브라우저 간의 채널을 제공 하는 Visual Studio 2013에 포함 된 새로운 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-152">**Browser Link** is a new feature included in Visual Studio 2013 that provides a channel between the Visual Studio IDE and any open browser to exchange data between your web application and Visual Studio.</span></span> <span data-ttu-id="fbb56-153">웹 Essentials DOM 개체 모델 및 브라우저에서 직접 웹 페이지의 CSS 스타일을 조작 하는 도구와 함께 브라우저 링크 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-153">Web Essentials extends Browser Link with tools to manipulate the DOM object model and the CSS styles of your web pages directly from the browser.</span></span>

<span data-ttu-id="fbb56-154">이 연습에서는 탐색에서 지 원하는 기능 중 일부 **웹 Essentials** 및 **브라우저 링크** 간단한 퀴즈 페이지를 향상 시키기 위해.</span><span class="sxs-lookup"><span data-stu-id="fbb56-154">In this exercise, you will explore some of the features supported by **Web Essentials** and **Browser Link** to enhance a simple quiz page.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1---running-the-project-in-multiple-browsers"></a><span data-ttu-id="fbb56-155">작업 1-다중 브라우저에서 프로젝트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-155">Task 1 - Running the Project in Multiple Browsers</span></span>

<span data-ttu-id="fbb56-156">이 작업에서는 다중 브라우저 테스트에 한 번에 여러 브라우저에서 실행 되도록 웹 응용 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-156">In this task, you will configure your web application to run in multiple browsers at once, which is useful for cross-browser testing.</span></span>

1. <span data-ttu-id="fbb56-157">열기 **Microsoft Visual Studio**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-157">Open **Microsoft Visual Studio**.</span></span>
2. <span data-ttu-id="fbb56-158">에 **파일** 메뉴 선택 **열기 | 프로젝트/솔루션...**  을 찾아서 **e x 1 WorkingwithBrowserLinkandWebEssentials\Begin** 에 **소스** 랩 (C:\WebCampsTK\HOL\VSWebTooling\Source)의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-158">In the **File** menu, select **Open | Project/Solution...** and browse to **Ex1-WorkingwithBrowserLinkandWebEssentials\Begin** in the **Source** folder of the lab (C:\WebCampsTK\HOL\VSWebTooling\Source).</span></span> <span data-ttu-id="fbb56-159">선택 **Begin.sln** 클릭 **열려**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-159">Select **Begin.sln** and click **Open**.</span></span>
3. <span data-ttu-id="fbb56-160">Visual Studio 도구 모음에서 브라우저 메뉴를 확장 하 고 선택 **브라우저 중...** .</span><span class="sxs-lookup"><span data-stu-id="fbb56-160">In the Visual Studio toolbar, expand the browser menu and select **Browse With...**.</span></span>

    <span data-ttu-id="fbb56-161">![메뉴 옵션 브라우저](visual-studio-2013-web-tools/_static/image1.png "브라우저 선택... 브라우저 메뉴에")</span><span class="sxs-lookup"><span data-stu-id="fbb56-161">![Browse With menu option](visual-studio-2013-web-tools/_static/image1.png "Browse with... in browser menu")</span></span>

    <span data-ttu-id="fbb56-162">*브라우저 메뉴 옵션*</span><span class="sxs-lookup"><span data-stu-id="fbb56-162">*Browse With menu option*</span></span>
4. <span data-ttu-id="fbb56-163">에 **브라우저** 대화 상자에서 선택 **Google Chrome** 및 **Internet Explorer** 누른는 **CTRL** 누른키 **기본값으로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-163">In the **Browse With** dialog box, select both **Google Chrome** and **Internet Explorer** by holding down the **CTRL** key and click **Set as Default**.</span></span>

    <span data-ttu-id="fbb56-164">![브라우저 대화 상자](visual-studio-2013-web-tools/_static/image2.png "브라우저 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="fbb56-164">![Browse with dialog box](visual-studio-2013-web-tools/_static/image2.png "Browse with dialog box")</span></span>

    <span data-ttu-id="fbb56-165">*여러 기본 브라우저를 선택합니다.*</span><span class="sxs-lookup"><span data-stu-id="fbb56-165">*Selecting multiple default browsers*</span></span>
5. <span data-ttu-id="fbb56-166">Google Chrome 및 Internet Explorer 모두 기본 브라우저 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-166">Both Google Chrome and Internet Explorer should now appear as the default browsers.</span></span> <span data-ttu-id="fbb56-167">클릭 **취소** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-167">Click **Cancel** to close the dialog box.</span></span>

    <span data-ttu-id="fbb56-168">![Internet Explorer를 기본 브라우저 및 Google Chrome](visual-studio-2013-web-tools/_static/image3.png "Google Chrome 및 Internet Explorer 기본 브라우저")</span><span class="sxs-lookup"><span data-stu-id="fbb56-168">![Google Chrome and Internet Explorer as default browsers](visual-studio-2013-web-tools/_static/image3.png "Google Chrome and Internet Explorer default browsers")</span></span>

    <span data-ttu-id="fbb56-169">*Google Chrome 및 Internet Explorer를 기본 브라우저*</span><span class="sxs-lookup"><span data-stu-id="fbb56-169">*Google Chrome and Internet Explorer as default browsers*</span></span>

    > [!NOTE]
    > <span data-ttu-id="fbb56-170">기본 브라우저를 구성한 후의 **여러 브라우저** 브라우저 메뉴에서 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-170">After configuring the default browsers, the **Multiple Browsers** option is selected in the browser menu.</span></span>
    > 
    > <span data-ttu-id="fbb56-171">![여러 브라우저](visual-studio-2013-web-tools/_static/image4.png "여러 브라우저")</span><span class="sxs-lookup"><span data-stu-id="fbb56-171">![Multiple browsers](visual-studio-2013-web-tools/_static/image4.png "Multiple browsers")</span></span>
6. <span data-ttu-id="fbb56-172">키를 눌러 **CTRL** + **F5** 디버깅 하지 않고 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-172">Press **CTRL** + **F5** to run the application without debugging.</span></span>
7. <span data-ttu-id="fbb56-173">두 브라우저 창을 열면 브라우저 모두에서 동시에 업데이트를 확인 하기 위해 상하로 둘 중 하나를 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-173">When both browser windows open, place one of them above the other in order to see the updates on both browsers simultaneously.</span></span> <span data-ttu-id="fbb56-174">브라우저는 연한 파란색 사각형에 포함 된 웹 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-174">The browsers should display a web page with a light-blue rectangle.</span></span>

    <span data-ttu-id="fbb56-175">![하나의 브라우저 상하로 배치](visual-studio-2013-web-tools/_static/image5.png "브라우저 상하로 배치")</span><span class="sxs-lookup"><span data-stu-id="fbb56-175">![Placing one browser above the other](visual-studio-2013-web-tools/_static/image5.png "Placing one browser above the other")</span></span>

    <span data-ttu-id="fbb56-176">*하나의 브라우저 상하로 배치*</span><span class="sxs-lookup"><span data-stu-id="fbb56-176">*Placing one browser above the other*</span></span>
8. <span data-ttu-id="fbb56-177">브라우저를 닫지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="fbb56-177">Do not close the browsers.</span></span> <span data-ttu-id="fbb56-178">다음 태스크에서에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-178">You will use them in the next task.</span></span>

<a id="Ex1Task2"></a>
#### <a name="task-2---using-zen-coding-to-create-html-elements"></a><span data-ttu-id="fbb56-179">작업 2-를 사용 하 여 Zen HTML 요소를 만드는 코딩</span><span class="sxs-lookup"><span data-stu-id="fbb56-179">Task 2 - Using Zen Coding to Create HTML Elements</span></span>

<span data-ttu-id="fbb56-180">**Zen 코딩** 은 편집기 고속 HTML, XML, XSL (또는 다른 구조적된 코드 형식)에 대 한 플러그 인을 코딩 하 고 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-180">**Zen Coding** is an editor plugin for high-speed HTML, XML, XSL (or any other structured code format) coding and editing.</span></span> <span data-ttu-id="fbb56-181">이 플러그 인의 핵심은 식을-CSS 선택기 비슷합니다-HTML 코드도 확장할 수 있는 강력한 약어 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-181">The core of this plugin is a powerful abbreviation engine which allows you to expand expressions -similar to CSS selectors- into HTML code.</span></span> <span data-ttu-id="fbb56-182">Zen 코딩을 빠르게 CSS를 사용 하 여 HTML 스타일 선택기 구문을 쓰려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-182">Zen Coding is a fast way to write HTML using a CSS style selector syntax.</span></span>

<span data-ttu-id="fbb56-183">이 연습에서는 질문의 옵션을 나타내는 HTML 단추를 생성 하려면 웹 Essentials에서 제공 Zen 코딩 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-183">In this exercise, you will use the Zen Coding feature provided by Web Essentials to generate the HTML buttons that represent the options of the question.</span></span>

1. <span data-ttu-id="fbb56-184">Visual Studio로 다시 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-184">Switch back to Visual Studio.</span></span>
2. <span data-ttu-id="fbb56-185">열기는 **Index.cshtml** 에 있는 파일의 **뷰** | **홈** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-185">Open the **Index.cshtml** file located in the **Views** | **Home** folder.</span></span>
3. <span data-ttu-id="fbb56-186">대체는 **&lt;!-TODO: 여기-옵션 추가&gt;** 메모 앞에 다음 코드 및 키를 눌러 **탭**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-186">Replace the **&lt;!-- TODO: add options here--&gt;** comment with the following code, and press **TAB**.</span></span>

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample1.css)]
4. <span data-ttu-id="fbb56-187">코드를 HTML로 확장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-187">The code should be expanded to HTML.</span></span>

    <span data-ttu-id="fbb56-188">![HTML 확장](visual-studio-2013-web-tools/_static/image6.png "HTML 확장")</span><span class="sxs-lookup"><span data-stu-id="fbb56-188">![Expanded HTML](visual-studio-2013-web-tools/_static/image6.png "Expanded HTML")</span></span>

    <span data-ttu-id="fbb56-189">*확장 된 HTML*</span><span class="sxs-lookup"><span data-stu-id="fbb56-189">*Expanded HTML*</span></span>

    > [!NOTE]
    > <span data-ttu-id="fbb56-190">Zen 코딩 구문에 대 한 자세한 내용은 다음을 참조 [문서](http://www.johnpapa.net/zen-coding-in-visual-studio-2012/)합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-190">To learn more about Zen Coding syntax, see the following [article](http://www.johnpapa.net/zen-coding-in-visual-studio-2012/).</span></span>
5. <span data-ttu-id="fbb56-191">클릭는 **연결 된 브라우저를 새로 고칠** 단추를 두는 브라우저를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-191">Click the **Refresh linked browsers** button to update both browsers.</span></span>

    <span data-ttu-id="fbb56-192">![연결 된 브라우저를 새로 고침](visual-studio-2013-web-tools/_static/image7.png "연결 된 브라우저를 새로 고칩니다.")</span><span class="sxs-lookup"><span data-stu-id="fbb56-192">![Refresh linked browsers](visual-studio-2013-web-tools/_static/image7.png "Refresh linked browsers")</span></span>

    <span data-ttu-id="fbb56-193">*연결 된 브라우저를 새로 고칩니다.*</span><span class="sxs-lookup"><span data-stu-id="fbb56-193">*Refresh linked browsers*</span></span>

    <span data-ttu-id="fbb56-194">![단추가 네 개 있는 Internet Explorer-페이지가 업데이트](visual-studio-2013-web-tools/_static/image8.png "단추가 네 개 있는 Internet Explorer-페이지가 업데이트")</span><span class="sxs-lookup"><span data-stu-id="fbb56-194">![Internet Explorer - Page updated with four buttons](visual-studio-2013-web-tools/_static/image8.png "Internet Explorer - Page updated with four buttons")</span></span>

    <span data-ttu-id="fbb56-195">*단추가 네 개 있는 Internet Explorer-페이지가 업데이트*</span><span class="sxs-lookup"><span data-stu-id="fbb56-195">*Internet Explorer - Page updated with four buttons*</span></span>

    <span data-ttu-id="fbb56-196">![Google Chrome-페이지가 업데이트 단추가 네 개 있는](visual-studio-2013-web-tools/_static/image9.png "단추가 네 개 있는 Google Chrome-페이지가 업데이트")</span><span class="sxs-lookup"><span data-stu-id="fbb56-196">![Google Chrome - Page updated with four buttons](visual-studio-2013-web-tools/_static/image9.png "Google Chrome - Page updated with four buttons")</span></span>

    <span data-ttu-id="fbb56-197">*단추가 네 개 있는 Google Chrome-페이지가 업데이트*</span><span class="sxs-lookup"><span data-stu-id="fbb56-197">*Google Chrome - Page updated with four buttons*</span></span>
6. <span data-ttu-id="fbb56-198">Visual Studio로 다시 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-198">Switch back to Visual Studio.</span></span>
7. <span data-ttu-id="fbb56-199">단추는 페이지에 추가 했지만 여전히 템플릿 질문 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-199">You have added the buttons to the page, but you still need to add a template question.</span></span> <span data-ttu-id="fbb56-200">이렇게 하려면 호출 하는 웹 Essentials의 새로운 기능을 사용 합니다 **Lorem Ipsum 생성기**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-200">To do so, you will use a new feature in Web Essentials called **Lorem Ipsum generator**.</span></span> <span data-ttu-id="fbb56-201">찾을 **div** 인 요소는 **클래스** 특성 **앞**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-201">Locate the **div** element with the **class** attribute **front**.</span></span>
8. <span data-ttu-id="fbb56-202">다음 코드의 첫 번째 자식 요소로 추가 **div**, 누릅니다 **탭**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-202">Add the following code as the first child element of the **div**, and press **TAB**.</span></span>

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample2.css)]
9. <span data-ttu-id="fbb56-203">코드를 HTML로 확장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-203">The code should be expanded to HTML.</span></span>

    <span data-ttu-id="fbb56-204">![자동 생성 된 Lorem Ipsum](visual-studio-2013-web-tools/_static/image10.png "Lorem Ipsum 자동 생성")</span><span class="sxs-lookup"><span data-stu-id="fbb56-204">![Lorem Ipsum autogenerated](visual-studio-2013-web-tools/_static/image10.png "Lorem Ipsum autogenerated")</span></span>

    <span data-ttu-id="fbb56-205">*Lorem Ipsum 자동 생성*</span><span class="sxs-lookup"><span data-stu-id="fbb56-205">*Lorem Ipsum autogenerated*</span></span>

    > [!NOTE]
    > <span data-ttu-id="fbb56-206">Zen 코딩의 일환으로, HTML 편집기에서 직접 이제 Lorem Ipsum 코드를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-206">As part of Zen Coding, you can now generate Lorem Ipsum code directly in the HTML editor.</span></span> <span data-ttu-id="fbb56-207">입력 **lorem** 적중 및 **탭** 30 Lorem Ipsum 텍스트가 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-207">Simply type **lorem** and hit **TAB** and a 30 word Lorem Ipsum text will be inserted.</span></span> <span data-ttu-id="fbb56-208">예:</span><span class="sxs-lookup"><span data-stu-id="fbb56-208">E.g.</span></span> <span data-ttu-id="fbb56-209">*lorem10* 10 Lorem Ipsum 단어를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-209">*lorem10* inserts 10 Lorem Ipsum words.</span></span>
10. <span data-ttu-id="fbb56-210">호출 웹 Essentials의 또 다른 새로운 기능을 사용 하 여 질문 맨 위에 있는 로고를 추가 합니다 **Lorem 픽셀 생성기**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-210">You will add a logo at the top of the question by using another new feature in Web Essentials called **Lorem Pixel generator**.</span></span> <span data-ttu-id="fbb56-211">다음 코드의 첫 번째 자식 요소로 추가 **div** 요소 **컨테이너** 으로 **클래스** 값 및 키를 눌러 **탭**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-211">Add the following code as the first child element of the **div** element with **container** as **class** value, and press **TAB**.</span></span>

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample3.css)]
11. <span data-ttu-id="fbb56-212">코드는 HTML을 확장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-212">The code should expand to HTML.</span></span>

    <span data-ttu-id="fbb56-213">![자동 생성 된 Lorem 픽셀](visual-studio-2013-web-tools/_static/image11.png "Lorem 픽셀 자동 생성")</span><span class="sxs-lookup"><span data-stu-id="fbb56-213">![Lorem Pixel autogenerated](visual-studio-2013-web-tools/_static/image11.png "Lorem Pixel autogenerated")</span></span>

    <span data-ttu-id="fbb56-214">*Lorem 픽셀 자동 생성*</span><span class="sxs-lookup"><span data-stu-id="fbb56-214">*Lorem Pixel autogenerated*</span></span>

    > [!NOTE]
    > <span data-ttu-id="fbb56-215">Zen 코딩의 일환으로, HTML 편집기에서 직접 Lorem 픽셀 코드를 생성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-215">As part of Zen Coding, you can also generate Lorem Pixel code directly in the HTML editor.</span></span> <span data-ttu-id="fbb56-216">입력 **pix-200 x 200-동물** 적중 및 **탭** 및 **img** 태그 동물의 200 x 200 이미지와 함께 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-216">Simply type **pix-200x200-animals** and hit **TAB** and an **img** tag with a 200x200 image of an animal will be inserted.</span></span> <span data-ttu-id="fbb56-217">자세한 내용은를 참조 [Lorem 픽셀](http://www.lorempixel.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-217">For more information, refer to [Lorem Pixel](http://www.lorempixel.com).</span></span>
12. <span data-ttu-id="fbb56-218">클릭는 **연결 된 브라우저를 새로 고칠** 단추를 두는 브라우저를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-218">Click the **Refresh linked browsers** button to update both browsers.</span></span>

    <span data-ttu-id="fbb56-219">![Internet Explorer-자동으로 생성 된 이미지 및 텍스트](visual-studio-2013-web-tools/_static/image12.png "Internet Explorer-자동으로 생성 된 이미지 및 텍스트")</span><span class="sxs-lookup"><span data-stu-id="fbb56-219">![Internet Explorer - Autogenerated image and text](visual-studio-2013-web-tools/_static/image12.png "Internet Explorer - Autogenerated image and text")</span></span>

    <span data-ttu-id="fbb56-220">*Internet Explorer-자동으로 생성 된 이미지 및 텍스트*</span><span class="sxs-lookup"><span data-stu-id="fbb56-220">*Internet Explorer - Autogenerated image and text*</span></span>

    <span data-ttu-id="fbb56-221">![Google Chrome-자동으로 생성 된 이미지 및 텍스트](visual-studio-2013-web-tools/_static/image13.png "Google Chrome-자동으로 생성 된 이미지 및 텍스트")</span><span class="sxs-lookup"><span data-stu-id="fbb56-221">![Google Chrome - Autogenerated image and text](visual-studio-2013-web-tools/_static/image13.png "Google Chrome - Autogenerated image and text")</span></span>

    <span data-ttu-id="fbb56-222">*Google Chrome-자동으로 생성 된 이미지 및 텍스트*</span><span class="sxs-lookup"><span data-stu-id="fbb56-222">*Google Chrome - Autogenerated image and text*</span></span>

    > [!NOTE]
    > <span data-ttu-id="fbb56-223">코드 조각을 추가 하는 경우 이미지를 임의로 선택, 때문에 브라우저에 표시 되는 이미지 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-223">Because the image is selected randomly when adding the code snippet, the image shown in the browsers may differ.</span></span>
13. <span data-ttu-id="fbb56-224">브라우저를 닫지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="fbb56-224">Do not close the browsers.</span></span> <span data-ttu-id="fbb56-225">다음 태스크에서에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-225">You will use them in the next task.</span></span>

<a id="Ex1Task3"></a>
#### <a name="task-3---updating-a-style-property"></a><span data-ttu-id="fbb56-226">작업 3-스타일 속성 업데이트</span><span class="sxs-lookup"><span data-stu-id="fbb56-226">Task 3 - Updating a Style Property</span></span>

<span data-ttu-id="fbb56-227">이 작업을 사용 하 여 브라우저 링크 **검사 모드** 여기서 특정 DOM 요소는 생성 된 정확한 위치를 검색 하 고 다음 웹에서 제공 되는 색상 선택기를 사용 하 여 해당 요소의 color 속성을 업데이트 하는 기능 필수 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-227">In this task, you will use the Browser Link's **Inspect Mode** feature to detect the exact location where the specific DOM element is generated and then update the color property of that element using a color picker provided by Web Essentials.</span></span>

1. <span data-ttu-id="fbb56-228">Internet Explorer 브라우저에서 눌러 **CTRL** + **ALT** + **I** 검사 모드를 사용 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-228">In the Internet Explorer browser, press **CTRL** + **ALT** + **I** to enable Inspect Mode.</span></span>
2. <span data-ttu-id="fbb56-229">밝은 파란색 테두리가 위로 포인터를 이동 하 고를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-229">Move the pointer over the light blue border and click.</span></span>

    <span data-ttu-id="fbb56-230">![밝은 파란색 테두리가 위로 포인터를 이동](visual-studio-2013-web-tools/_static/image14.png "밝은 파란색 테두리가 위로 포인터를 이동")</span><span class="sxs-lookup"><span data-stu-id="fbb56-230">![Moving the pointer over the light blue border](visual-studio-2013-web-tools/_static/image14.png "Moving the pointer over the light blue border")</span></span>

    <span data-ttu-id="fbb56-231">*밝은 파란색 테두리가 위로 포인터를 이동*</span><span class="sxs-lookup"><span data-stu-id="fbb56-231">*Moving the pointer over the light blue border*</span></span>
3. <span data-ttu-id="fbb56-232">Visual Studio로 다시 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-232">Switch back to Visual Studio.</span></span> <span data-ttu-id="fbb56-233">브라우저에서 선택 하는 HTML 요소 Visual Studio HTML 편집기에서 선택도 방법을 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="fbb56-233">Notice how the HTML element that you selected in the browser is also selected in the Visual Studio HTML editor.</span></span>

    <span data-ttu-id="fbb56-234">![Visual Studio HTML 편집기에서 선택 된 HTML 요소](visual-studio-2013-web-tools/_static/image15.png "HTML 요소를 Visual Studio HTML 편집기에서 선택 합니다.")</span><span class="sxs-lookup"><span data-stu-id="fbb56-234">![HTML element selected in the Visual Studio HTML editor](visual-studio-2013-web-tools/_static/image15.png "HTML element selected in the Visual Studio HTML editor")</span></span>

    <span data-ttu-id="fbb56-235">*Visual Studio HTML 편집기에서 선택 된 HTML 요소*</span><span class="sxs-lookup"><span data-stu-id="fbb56-235">*HTML element selected in the Visual Studio HTML editor*</span></span>
4. <span data-ttu-id="fbb56-236">가 지금 업데이트는 **앞** 선택한 요소의 스타일을 변경 하기 위해 CSS 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-236">You will now update the **front** CSS class in order to change the styling of the selected element.</span></span> <span data-ttu-id="fbb56-237">이렇게 하려면 다음을 눌러 **CTRL** + **,** 열려는 **탐색** 검색 상자.</span><span class="sxs-lookup"><span data-stu-id="fbb56-237">To do so, press **CTRL** + **,** to open the **Navigate To** search box.</span></span> <span data-ttu-id="fbb56-238">형식 **site.css** 누릅니다 **ENTER** 파일을 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-238">Type **site.css** and press **ENTER** to open the file.</span></span>

    <span data-ttu-id="fbb56-239">![Site.css 파일을 열면](visual-studio-2013-web-tools/_static/image16.png "Site.css 파일을 여는")</span><span class="sxs-lookup"><span data-stu-id="fbb56-239">![Opening file Site.css](visual-studio-2013-web-tools/_static/image16.png "Opening file Site.css")</span></span>

    <span data-ttu-id="fbb56-240">*Site.css 파일 열기*</span><span class="sxs-lookup"><span data-stu-id="fbb56-240">*Opening file Site.css*</span></span>
5. <span data-ttu-id="fbb56-241">키를 눌러 **CTRL** + **F** 유형과 **.flip 컨테이너.front** CSS 선택기를 찾으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-241">Press **CTRL** + **F** and type **.flip-containter .front** to find the CSS selector.</span></span>
6. <span data-ttu-id="fbb56-242">색상 선택기를 열려는 클래스의 테두리 속성에 있는 밝은 파란색 사각형을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-242">Click the light blue square in the border property of the class to open the Color Picker.</span></span>

    <span data-ttu-id="fbb56-243">![색 선택 열기](visual-studio-2013-web-tools/_static/image17.png "색 선택 열기")</span><span class="sxs-lookup"><span data-stu-id="fbb56-243">![Opening the Color Picker](visual-studio-2013-web-tools/_static/image17.png "Opening the Color Picker")</span></span>

    <span data-ttu-id="fbb56-244">*색 선택 열기*</span><span class="sxs-lookup"><span data-stu-id="fbb56-244">*Opening the Color Picker*</span></span>
7. <span data-ttu-id="fbb56-245">펼침 단추를 클릭 하 여 색상 선택기를 확장 하 고 새 색을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-245">Expand the Color Picker by clicking the chevron button and select a new color.</span></span>

    <span data-ttu-id="fbb56-246">![색 선택 확장](visual-studio-2013-web-tools/_static/image18.png "색상 선택기를 확장 합니다.")</span><span class="sxs-lookup"><span data-stu-id="fbb56-246">![Expanding the Color Picker](visual-studio-2013-web-tools/_static/image18.png "Expanding the Color Picker")</span></span>

    <span data-ttu-id="fbb56-247">*색상 선택기를 확장합니다.*</span><span class="sxs-lookup"><span data-stu-id="fbb56-247">*Expanding the Color Picker*</span></span>
8. <span data-ttu-id="fbb56-248">키를 눌러 **CTRL** + **ALT** + **ENTER** 연결 된 브라우저를 새로 고칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-248">Press **CTRL** + **ALT** + **ENTER** to refresh linked browsers.</span></span>
9. <span data-ttu-id="fbb56-249">Internet Explorer로 전환한 테두리의 색 어떻게 변경 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-249">Switch to Internet Explorer and notice how the color of the border has changed.</span></span>

    <span data-ttu-id="fbb56-250">![Internet Explorer-업데이트 테두리 색](visual-studio-2013-web-tools/_static/image19.png "Internet Explorer-업데이트 테두리 색입니다.")</span><span class="sxs-lookup"><span data-stu-id="fbb56-250">![Internet Explorer - Border color updated](visual-studio-2013-web-tools/_static/image19.png "Internet Explorer - Border color updated")</span></span>

    <span data-ttu-id="fbb56-251">*Internet Explorer-업데이트 테두리 색입니다.*</span><span class="sxs-lookup"><span data-stu-id="fbb56-251">*Internet Explorer - Border color updated*</span></span>
10. <span data-ttu-id="fbb56-252">Google Chrome 전환한 테두리의 색 어떻게 변경 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-252">Switch to Google Chrome and notice how the color of the border has changed.</span></span>

    <span data-ttu-id="fbb56-253">![Google Chrome-업데이트 테두리 색](visual-studio-2013-web-tools/_static/image20.png "Google Chrome-업데이트 테두리 색입니다.")</span><span class="sxs-lookup"><span data-stu-id="fbb56-253">![Google Chrome - Border color updated](visual-studio-2013-web-tools/_static/image20.png "Google Chrome - Border color updated")</span></span>

    <span data-ttu-id="fbb56-254">*Google Chrome-업데이트 테두리 색입니다.*</span><span class="sxs-lookup"><span data-stu-id="fbb56-254">*Google Chrome - Border color updated*</span></span>
11. <span data-ttu-id="fbb56-255">Visual Studio로 다시 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-255">Switch back to Visual Studio.</span></span>
12. <span data-ttu-id="fbb56-256">끝으로 이동는 **Site.css** 파일 및 키를 눌러 **CTRL** + **F** 찾으려고는 **.btn** 선택기입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-256">Go to the end of the **Site.css** file and press **CTRL** + **F** to locate the **.btn** selector.</span></span>
13. <span data-ttu-id="fbb56-257">다음에 유의 **-webkit 테두리 반지름** 속성은 녹색으로 밑줄이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-257">Notice that the **-webkit-border-radius** property is underlined in green.</span></span>

    <span data-ttu-id="fbb56-258">![-webkit 테두리 반지름 속성 btn 선택기의](visual-studio-2013-web-tools/_static/image21.png "btn 선택기의-webkit 테두리 반지름 속성")</span><span class="sxs-lookup"><span data-stu-id="fbb56-258">![-webkit-border-radius property of the btn selector](visual-studio-2013-web-tools/_static/image21.png "-webkit-border-radius property of the btn selector")</span></span>

    <span data-ttu-id="fbb56-259">*btn 선택기의-webkit 테두리 반지름 속성*</span><span class="sxs-lookup"><span data-stu-id="fbb56-259">*-webkit-border-radius property of the btn selector*</span></span>
14. <span data-ttu-id="fbb56-260">에 캐럿 배치는 **-webkit 테두리 반지름** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-260">Place the caret in the **-webkit-border-radius** property.</span></span> <span data-ttu-id="fbb56-261">속성의 첫 번째 단어의 첫 문자 아래 파란색 선이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-261">A blue line should appear under the first letter of the first word of the property.</span></span> <span data-ttu-id="fbb56-262">이는 **스마트 태그**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-262">This is the **smart tag**.</span></span>
15. <span data-ttu-id="fbb56-263">키를 눌러 **CTRL** + **합니다.**</span><span class="sxs-lookup"><span data-stu-id="fbb56-263">Press **CTRL** + **.**</span></span> <span data-ttu-id="fbb56-264">제안 메뉴를 열고 클릭 **표준 속성 (테두리 radius) 누락 된 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-264">to open the suggestions menu and click **Add missing standard property (border-radius)**.</span></span>

    <span data-ttu-id="fbb56-265">![표준 속성 제안 누락 추가](visual-studio-2013-web-tools/_static/image22.png "표준 속성 제안 누락 추가")</span><span class="sxs-lookup"><span data-stu-id="fbb56-265">![Add missing standard property suggestion](visual-studio-2013-web-tools/_static/image22.png "Add missing standard property suggestion")</span></span>

    <span data-ttu-id="fbb56-266">*표준 속성 제안 누락 된 추가*</span><span class="sxs-lookup"><span data-stu-id="fbb56-266">*Add missing standard property suggestion*</span></span>
16. <span data-ttu-id="fbb56-267">**테두리 radius** 속성 CSS 규칙에 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-267">The **border-radius** property is automatically added to the CSS rule.</span></span>

    <span data-ttu-id="fbb56-268">![추가 표준 속성이 누락](visual-studio-2013-web-tools/_static/image23.png "누락를 추가 하는 표준 속성")</span><span class="sxs-lookup"><span data-stu-id="fbb56-268">![Missing standard property added](visual-studio-2013-web-tools/_static/image23.png "Missing standard property added")</span></span>

    <span data-ttu-id="fbb56-269">*표준 속성 추가*</span><span class="sxs-lookup"><span data-stu-id="fbb56-269">*Missing standard property added*</span></span>
17. <span data-ttu-id="fbb56-270">포인터를 가져가서는 **테두리 radius** 속성을 표시는 **브라우저 매트릭스 도구 설명**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-270">Move the pointer over the **border-radius** property to display the **Browser matrix tooltip**.</span></span> <span data-ttu-id="fbb56-271">**브라우저 매트릭스 도구 설명** 각 브라우저에서 속성의 가용성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-271">The **Browser matrix tooltip** shows the availability of the property in each browser.</span></span>

    <span data-ttu-id="fbb56-272">![브라우저 매트릭스 도구 설명](visual-studio-2013-web-tools/_static/image24.png "브라우저 매트릭스 도구 설명")</span><span class="sxs-lookup"><span data-stu-id="fbb56-272">![Browser matrix tooltip](visual-studio-2013-web-tools/_static/image24.png "Browser matrix tooltip")</span></span>

    <span data-ttu-id="fbb56-273">*브라우저 매트릭스 도구 설명*</span><span class="sxs-lookup"><span data-stu-id="fbb56-273">*Browser matrix tooltip*</span></span>
18. <span data-ttu-id="fbb56-274">다음에 유의 값은 **테두리 radius** 속성은 여전히 밑줄 서식을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-274">Notice that the value of the **border-radius** property is still underlined.</span></span> <span data-ttu-id="fbb56-275">경고 메시지를 보려면 값 위로 포인터를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-275">Move the pointer over the value to see the warning message.</span></span>

    <span data-ttu-id="fbb56-276">![테두리 radius 속성 값 경고](visual-studio-2013-web-tools/_static/image25.png "테두리 radius 속성 값 경고")</span><span class="sxs-lookup"><span data-stu-id="fbb56-276">![Border-radius property value warning](visual-studio-2013-web-tools/_static/image25.png "Border-radius property value warning")</span></span>

    <span data-ttu-id="fbb56-277">*테두리 radius 속성 값 경고*</span><span class="sxs-lookup"><span data-stu-id="fbb56-277">*Border-radius property value warning*</span></span>
19. <span data-ttu-id="fbb56-278">단위를 제거는 **테두리 radius** 도구 설명에서 제시한 대로 속성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-278">Remove the unit of the **border-radius** property value as suggested by the tooltip.</span></span>
20. <span data-ttu-id="fbb56-279">으로 **테두리 radius** 모서리는 제거할 수 있습니다 어떻게 모서리가 둥근된 테두리를 정의 하기 위한 표준 속성는 **-webkit 테두리 반지름** 속성 및 CSS 규칙에서 값입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-279">As **border-radius** is the standard property for defining how rounded border corners are, you can remove the **-webkit-border-radius** property and value from the CSS rule.</span></span>
21. <span data-ttu-id="fbb56-280">에 캐럿 배치는 **바꿈** 속성 및 스마트 태그 아래도 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-280">Place the caret in the **word-wrap** property and notice that the smart tag also appears below.</span></span>
22. <span data-ttu-id="fbb56-281">메뉴를 열고 클릭 **누락 된 공급 업체 비슷하므로 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-281">Open the menu and click **Add missing vendor specifics**.</span></span>

    <span data-ttu-id="fbb56-282">![누락 된 공급 업체에 대 한 구체적인 제안 사항을 추가](visual-studio-2013-web-tools/_static/image26.png "누락 된 공급 업체에 대 한 구체적인 제안 사항을 추가")</span><span class="sxs-lookup"><span data-stu-id="fbb56-282">![Add missing vendor specifics suggestion](visual-studio-2013-web-tools/_static/image26.png "Add missing vendor specifics suggestion")</span></span>

    <span data-ttu-id="fbb56-283">*누락 된 공급 업체에 대 한 구체적인 제안 사항을 추가합니다*</span><span class="sxs-lookup"><span data-stu-id="fbb56-283">*Add missing vendor specifics suggestion*</span></span>
23. <span data-ttu-id="fbb56-284">**ms 단어 잘림** 속성 CSS 규칙에 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-284">The **-ms-word-wrap** property is automatically added to the CSS rule.</span></span>

    <span data-ttu-id="fbb56-285">![공급 업체 관련 속성 추가](visual-studio-2013-web-tools/_static/image27.png "공급 업체 관련 속성 추가")</span><span class="sxs-lookup"><span data-stu-id="fbb56-285">![Vendor specific property added](visual-studio-2013-web-tools/_static/image27.png "Vendor specific property added")</span></span>

    <span data-ttu-id="fbb56-286">*공급 업체 관련 속성 추가*</span><span class="sxs-lookup"><span data-stu-id="fbb56-286">*Vendor specific property added*</span></span>

<a id="Ex1Task4"></a>
#### <a name="task-4---updating-the-html-code-from-the-browser"></a><span data-ttu-id="fbb56-287">작업 4-브라우저에서 HTML 코드 업데이트</span><span class="sxs-lookup"><span data-stu-id="fbb56-287">Task 4 - Updating the HTML Code from the Browser</span></span>

<span data-ttu-id="fbb56-288">이 작업을 사용 하 여 브라우저 링크 **디자인 모드** 브라우저에서 DOM 개체를 편집 및 Visual Studio에서 HTML 소스 파일에 변경 내용을 전송 하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-288">In this task, you will use the Browser Link's **Design Mode** feature to edit the DOM object from the browser and transfer the changes to the HTML source file in Visual Studio.</span></span>

1. <span data-ttu-id="fbb56-289">Google Chrome에서 눌러 **CTRL** + **ALT** + **D** 디자인 모드를 사용 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-289">In Google Chrome, press **CTRL** + **ALT** + **D** to enable Design Mode.</span></span>
2. <span data-ttu-id="fbb56-290">위로 포인터를 이동는 **Lorem Ipsum dolor sit amet** 레이블을 지정 하 고를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-290">Move the pointer over the **Lorem Ipsum dolor sit amet** label and click.</span></span>

    <span data-ttu-id="fbb56-291">![질문 편집](visual-studio-2013-web-tools/_static/image28.png "질문 편집")</span><span class="sxs-lookup"><span data-stu-id="fbb56-291">![Editing the question](visual-studio-2013-web-tools/_static/image28.png "Editing the question")</span></span>

    <span data-ttu-id="fbb56-292">*질문을 편집합니다.*</span><span class="sxs-lookup"><span data-stu-id="fbb56-292">*Editing the question*</span></span>
3. <span data-ttu-id="fbb56-293">커서가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-293">A cursor should appear.</span></span> <span data-ttu-id="fbb56-294">원래 텍스트를 대체 *않습니다 것 모양을 긴 질문을 쓸 때?*, 한 다음 키를 누릅니다 **ESC** 디자인 모드를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-294">Replace the original text with *What does it look like when I write a longer question?*, and then press **ESC** to exit Design Mode.</span></span>

    <span data-ttu-id="fbb56-295">![편집할 질문](visual-studio-2013-web-tools/_static/image29.png "질문 편집")</span><span class="sxs-lookup"><span data-stu-id="fbb56-295">![Question edited](visual-studio-2013-web-tools/_static/image29.png "Question edited")</span></span>

    <span data-ttu-id="fbb56-296">*편집할 질문*</span><span class="sxs-lookup"><span data-stu-id="fbb56-296">*Question edited*</span></span>
4. <span data-ttu-id="fbb56-297">Visual Studio로 다시 및 open 스위치 **Index.cshtml**열려 있지 않으면, 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-297">Switch back to Visual Studio and open **Index.cshtml**, if not already opened.</span></span> <span data-ttu-id="fbb56-298">다음에 유의의 내부 텍스트는 **&lt;p&gt;** 요소가 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-298">Notice that the inner text of the **&lt;p&gt;** element has been updated.</span></span>

    <span data-ttu-id="fbb56-299">![HTML 페이지에 업데이트 된 질문](visual-studio-2013-web-tools/_static/image30.png "HTML 페이지에 업데이트 된 질문")</span><span class="sxs-lookup"><span data-stu-id="fbb56-299">![Updated question in the HTML page](visual-studio-2013-web-tools/_static/image30.png "Updated question in the HTML page")</span></span>

    <span data-ttu-id="fbb56-300">*HTML 페이지에 업데이트 된 질문*</span><span class="sxs-lookup"><span data-stu-id="fbb56-300">*Updated question in the HTML page*</span></span>

<a id="Ex1Task5"></a>
#### <a name="task-5---reviewing-seo-related-warnings"></a><span data-ttu-id="fbb56-301">작업 5-검토 SEO 관련 경고</span><span class="sxs-lookup"><span data-stu-id="fbb56-301">Task 5 - Reviewing SEO Related Warnings</span></span>

<span data-ttu-id="fbb56-302">**검색 엔진 최적화** SEO ()은 검색 엔진 결과 목록에 더 높은 순위 웹 사이트를 만드는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-302">**Search Engine Optimization** (SEO) is the process of making a website rank higher on a search engine's list of results.</span></span> <span data-ttu-id="fbb56-303">사이트의 순위가 높을수록, 나열 된 더 일관 되 게, 더 많은 방문자 사이트 해당 검색 엔진에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-303">The higher the site ranks and the more consistently it is listed, the more visitors the site will get from that search engine.</span></span> <span data-ttu-id="fbb56-304">웹 Essentials 통합 HTML을 검사 하는 분석 도구, 보고서 문제 발견 하 고 수정 지원을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-304">Web Essentials incorporates an analytical tool that examines HTML, reports the issues found and provides assistance to fix them.</span></span>

1. <span data-ttu-id="fbb56-305">이동 하는 **보기** 메뉴를 클릭 **오류 목록** 열려는 **오류 목록** 창.</span><span class="sxs-lookup"><span data-stu-id="fbb56-305">Go to the **View** menu and click **Error List** to open the **Error List** window.</span></span>

    <span data-ttu-id="fbb56-306">![오류 목록 보기에 메뉴](visual-studio-2013-web-tools/_static/image31.png "보기 메뉴의 오류 목록")</span><span class="sxs-lookup"><span data-stu-id="fbb56-306">![Error List in View menu](visual-studio-2013-web-tools/_static/image31.png "Error List in View menu")</span></span>

    <span data-ttu-id="fbb56-307">*오류 목록 보기에 메뉴*</span><span class="sxs-lookup"><span data-stu-id="fbb56-307">*Error List in View menu*</span></span>
2. <span data-ttu-id="fbb56-308">한 SEO을 알리는 경고를 하는 한 **&lt;메타&gt;** 페이지 설명에 대 한 태그를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-308">Notice that there is an SEO warning notifying that a **&lt;meta&gt;** tag for the page description is missing.</span></span> <span data-ttu-id="fbb56-309">이 문제를 해결할 SEO 경고 항목을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-309">Double-click the SEO warning entry to fix it.</span></span>

    <span data-ttu-id="fbb56-310">![오류 목록 창](visual-studio-2013-web-tools/_static/image32.png "오류 목록 창")</span><span class="sxs-lookup"><span data-stu-id="fbb56-310">![Error List window](visual-studio-2013-web-tools/_static/image32.png "Error List window")</span></span>

    <span data-ttu-id="fbb56-311">*오류 목록 창*</span><span class="sxs-lookup"><span data-stu-id="fbb56-311">*Error List window*</span></span>
3. <span data-ttu-id="fbb56-312">에 **웹 Essentials** 대화 상자에서 클릭 **예** 설명은 삽입 하려면 &lt;메타&gt; 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-312">In the **Web Essentials** dialog box, click **Yes** to insert a description &lt;meta&gt; tag.</span></span>

    <span data-ttu-id="fbb56-313">![웹 Essentials 대화 상자](visual-studio-2013-web-tools/_static/image33.png "웹 Essentials 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="fbb56-313">![Web Essentials dialog box](visual-studio-2013-web-tools/_static/image33.png "Web Essentials dialog box")</span></span>

    <span data-ttu-id="fbb56-314">*웹 Essentials 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="fbb56-314">*Web Essentials dialog box*</span></span>
4. <span data-ttu-id="fbb56-315">에 대 한 편집기  **\_Layout.cshtml** 열립니다 및 **&lt;메타&gt;** 태그 자동으로 추가 되는 **h e a d** 의 섹션의 HTML 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-315">The editor for **\_Layout.cshtml** opens and the **&lt;meta&gt;** tag is automatically added to the **head** section of the HTML file.</span></span>

    <span data-ttu-id="fbb56-316">![_Layout 페이지에 자동으로 추가 하는 메타 태그](visual-studio-2013-web-tools/_static/image34.png "_Layout 페이지에 자동으로 추가 하는 메타 태그")</span><span class="sxs-lookup"><span data-stu-id="fbb56-316">![Meta tag automatically added in _Layout page](visual-studio-2013-web-tools/_static/image34.png "Meta tag automatically added in _Layout page")</span></span>

    <span data-ttu-id="fbb56-317">*에 자동으로 추가 하는 메타 태그 \_페이지 레이아웃*</span><span class="sxs-lookup"><span data-stu-id="fbb56-317">*Meta tag automatically added to \_Layout page*</span></span>
5. <span data-ttu-id="fbb56-318">값을 변경는 **콘텐츠** 특성을 *GeekQuiz* 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-318">Change the value of the **content** attribute to *GeekQuiz* and save the file.</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-taking-advantage-of-code-snippets-and-intellisense"></a><span data-ttu-id="fbb56-319">연습 2: 코드 조각 및 IntelliSense를 활용 하기 위해</span><span class="sxs-lookup"><span data-stu-id="fbb56-319">Exercise 2: Taking Advantage of Code Snippets and IntelliSense</span></span>

<span data-ttu-id="fbb56-320">웹 essentials HTML 편집기는 추가 기능으로 확장 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-320">With Web Essentials, the HTML editor has been extended with extra functionality.</span></span> <span data-ttu-id="fbb56-321">이 연습에서는 웹 응용 프로그램을 개발할 때 도움이 되는 일부 새로운 기능은 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-321">In this exercise, you will see some new features that are helpful when developing web applications.</span></span>

<a id="Ex2Task1"></a>
#### <a name="task-1---using-intellisense-in-html-documents"></a><span data-ttu-id="fbb56-322">작업 1-HTML 문서에 IntelliSense 사용</span><span class="sxs-lookup"><span data-stu-id="fbb56-322">Task 1 - Using IntelliSense in HTML Documents</span></span>

<span data-ttu-id="fbb56-323">이 작업에 표시 되는 첫 번째 새 기능을 라고 **동적 IntelliSense**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-323">The first new feature you will see in this task is called **Dynamic IntelliSense**.</span></span> <span data-ttu-id="fbb56-324">동적 IntelliSense에는 다른 태그 및 특성을 사용 하 여 가능한 id 유추 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-324">Dynamic IntelliSense reads other tags and attributes to infer the possible ids you will use.</span></span>

<span data-ttu-id="fbb56-325">이 태스크에서는 레이블 및 입력된 필드를 포함 하는 새 HTML 폼 요소에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-325">In this task, you will create a new HTML form element which contains a label and an input field.</span></span> <span data-ttu-id="fbb56-326">다음 추가 됩니다 한 **에 대 한** 입력을 바인딩할 레이블에 특성 범위에서 입력의 id에 따라 IntelliSense 제안 사항이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-326">Then you will add a **for** attribute to the label to bind it to the input, and you will see IntelliSense suggestions based on the ids of the inputs in scope.</span></span>

1. <span data-ttu-id="fbb56-327">열기 **Visual Studio Express 2013 for Web** 및 **Begin.sln** 솔루션에 있는 **소스/e x 2-TakingAdvantageofCodeSnippetsandIntelliSense/시작** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-327">Open **Visual Studio Express 2013 for Web** and the **Begin.sln** solution located in the **Source/Ex2-TakingAdvantageofCodeSnippetsandIntelliSense/Begin** folder.</span></span> <span data-ttu-id="fbb56-328">또는 계속할 수 있습니다 솔루션으로, 이전 연습에서 가져올 있음을.</span><span class="sxs-lookup"><span data-stu-id="fbb56-328">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>
2. <span data-ttu-id="fbb56-329">**솔루션 탐색기**열고는 **Index.cshtml** 에 있는 파일의 **뷰** | **홈** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-329">In **Solution Explorer**, open the **Index.cshtml** file located in the **Views** | **Home** folder.</span></span>
3. <span data-ttu-id="fbb56-330">내부 다음 양식을 추가 **&lt;섹션&gt;** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-330">Add the following form inside the **&lt;section&gt;** element.</span></span>

    <span data-ttu-id="fbb56-331">(코드 조각- *VisualStudio2013WebTooling* - *e x 2* - *양식*)</span><span class="sxs-lookup"><span data-stu-id="fbb56-331">(Code Snippet - *VisualStudio2013WebTooling* - *Ex2* - *Form*)</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample4.html)]
4. <span data-ttu-id="fbb56-332">입력된 태그 일부 설명은 필드 레이블 뒤에 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-332">The input tag should be preceded by a label with some description of the field.</span></span> <span data-ttu-id="fbb56-333">입력된 태그 앞에 다음 레이블을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-333">Add the following label before the input tag.</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample5.html)]
5. <span data-ttu-id="fbb56-334">**에 대 한** 특성에는 **&lt;레이블&gt;** 레이블이 폼 요소에 바인딩된 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-334">The **for** attribute of a **&lt;label&gt;** specifies which form element a label is bound to.</span></span> <span data-ttu-id="fbb56-335">특성의 값은 관련 된 요소의 id로 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-335">The attribute's value should be equal to the id of the related element.</span></span> <span data-ttu-id="fbb56-336">추가 **에 대 한** 특성을 **&lt;레이블&gt;** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-336">Add the **for** attribute to the **&lt;label&gt;** element.</span></span> <span data-ttu-id="fbb56-337">다음 그림에 나와 있는 것 처럼는 &quot;이름&quot; 값 팝업 IntelliSense 상자에서 동일한 범위 내 요소의 id에 따라 (묶는  **&lt;양식&gt;**).</span><span class="sxs-lookup"><span data-stu-id="fbb56-337">As shown in the following figure, the &quot;name&quot; value pops up in the IntelliSense box, based on the id of the elements within the same scope (the enclosing **&lt;form&gt;**).</span></span>

    <span data-ttu-id="fbb56-338">![IntelliSense의 id를 보여 주는](visual-studio-2013-web-tools/_static/image35.png "IntelliSense에 id를 표시 합니다.")</span><span class="sxs-lookup"><span data-stu-id="fbb56-338">![Showing the id in IntelliSense](visual-studio-2013-web-tools/_static/image35.png "Showing the id in IntelliSense")</span></span>

    <span data-ttu-id="fbb56-339">*IntelliSense에 id를 표시합니다.*</span><span class="sxs-lookup"><span data-stu-id="fbb56-339">*Showing the id in IntelliSense*</span></span>
6. <span data-ttu-id="fbb56-340">최근에 추가 된 삭제 **&lt;양식&gt;** 요소와 해당 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-340">Delete the recently added **&lt;form&gt;** element and its content.</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2---using-html-code-snippets"></a><span data-ttu-id="fbb56-341">작업 2-HTML 코드 조각을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="fbb56-341">Task 2 - Using HTML Code Snippets</span></span>

<span data-ttu-id="fbb56-342">HTML5 25 개 이상의 새로운 의미 체계 태그를 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-342">HTML5 introduced more than 25 new semantic tags.</span></span> <span data-ttu-id="fbb56-343">Visual Studio가 이미 이러한 태그에 대 한 IntelliSense 지원 하지만 Visual Studio 2013을 사용 하면 빠르고 쉽게 새 코드 조각을 추가 하 여 태그를 작성 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-343">Visual Studio already had IntelliSense support for these tags, but Visual Studio 2013 makes it faster and easier to write markup by adding new code snippets.</span></span> <span data-ttu-id="fbb56-344">에 대 한 올바른 코덱을 대체를 추가 하는 등 몇 가지 작은 미묘한 함께 제공 되는 경우에 이러한 태그 크게 복잡 하지 않습니다는 *오디오* 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-344">Though these tags are not complicated, they come with a few small subtleties, such as adding the correct codec fallbacks for the *audio* tag.</span></span> <span data-ttu-id="fbb56-345">이 태스크에서는 오디오 태그에 대 한 HTML 코드 조각을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-345">In this task, you will see the HTML code snippets for the audio tag.</span></span>

1. <span data-ttu-id="fbb56-346">에 **Index.cshtml** 파일, 입력  **&lt;aud** 내는 **&lt;섹션&gt;** 요소는 다음 그림에 나와 있는 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-346">In the **Index.cshtml** file, type **&lt;aud** inside the **&lt;section&gt;** element as shown in the following figure.</span></span>

    <span data-ttu-id="fbb56-347">![오디오 요소를 삽입할](visual-studio-2013-web-tools/_static/image36.png "오디오 요소 삽입")</span><span class="sxs-lookup"><span data-stu-id="fbb56-347">![Inserting an audio element](visual-studio-2013-web-tools/_static/image36.png "Inserting an audio element")</span></span>

    <span data-ttu-id="fbb56-348">*오디오 요소 삽입*</span><span class="sxs-lookup"><span data-stu-id="fbb56-348">*Inserting an audio element*</span></span>
2. <span data-ttu-id="fbb56-349">키를 눌러 **탭** 두 번과 페이지에서 다음 코드에 어떻게 추가 되었는지를에 커서가 놓입니다는 **src** 첫 번째 소스의 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-349">Press **TAB** twice and notice how the following code is added on the page and the cursor is placed on the **src** attribute of the first source.</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample6.html)]

    > [!NOTE]
    > <span data-ttu-id="fbb56-350">키를 눌러는 **탭** 키를 두 번 코드 조각을 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-350">By pressing the **TAB** key twice, the code snippet is inserted.</span></span> <span data-ttu-id="fbb56-351">오디오 조각 대 한 일반 사용법을 보여 줍니다.는 *오디오* 지원 향상된에 대 한 소스 파일의 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-351">The audio snippet shows the standard usage of the *audio* tag, with two source files for improved support.</span></span>
3. <span data-ttu-id="fbb56-352">두 번째 줄을 삭제 하 고 다음 링크를 WebCampsTV Katana 표시도 첫 번째 줄의 소스를 업데이트: [ http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3 ](http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3)합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-352">Delete the second line and update the source of the first line with the following link to the WebCampsTV Katana show: [http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3](http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3).</span></span> <span data-ttu-id="fbb56-353">결과 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-353">The resulting code is shown below.</span></span>

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample7.html)]

    > [!NOTE]
    > <span data-ttu-id="fbb56-354">소스 파일 *KatanaProject.mp3* 예제로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-354">The source file *KatanaProject.mp3* is used as an example.</span></span> <span data-ttu-id="fbb56-355">다른 소스 원할 경우 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-355">You can use another source if you prefer.</span></span>
4. <span data-ttu-id="fbb56-356">키를 눌러 **CTRL** + **S** 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-356">Press **CTRL** + **S** to save the file.</span></span>
5. <span data-ttu-id="fbb56-357">키를 눌러 **CTRL** + **F5** 는 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-357">Press **CTRL** + **F5** to start the application.</span></span>
6. <span data-ttu-id="fbb56-358">오디오 플레이어 응용 프로그램에 추가 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-358">Notice that an audio player was added to the application.</span></span>

    <span data-ttu-id="fbb56-359">![Internet Explorer에서 오디오 플레이어](visual-studio-2013-web-tools/_static/image37.png "Internet Explorer에서 오디오 플레이어")</span><span class="sxs-lookup"><span data-stu-id="fbb56-359">![Audio player in Internet Explorer](visual-studio-2013-web-tools/_static/image37.png "Audio player in Internet Explorer")</span></span>

    <span data-ttu-id="fbb56-360">*Internet Explorer에서 오디오 플레이어*</span><span class="sxs-lookup"><span data-stu-id="fbb56-360">*Audio player in Internet Explorer*</span></span>

    <span data-ttu-id="fbb56-361">![Google Chrome의 오디오 플레이어](visual-studio-2013-web-tools/_static/image38.png "Google Chrome의 오디오 플레이어")</span><span class="sxs-lookup"><span data-stu-id="fbb56-361">![Audio player in Google Chrome](visual-studio-2013-web-tools/_static/image38.png "Audio player in Google Chrome")</span></span>

    <span data-ttu-id="fbb56-362">*Google Chrome의 오디오 플레이어*</span><span class="sxs-lookup"><span data-stu-id="fbb56-362">*Audio player in Google Chrome*</span></span>
7. <span data-ttu-id="fbb56-363">브라우저를 닫지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="fbb56-363">Do not close the browsers.</span></span> <span data-ttu-id="fbb56-364">다음 태스크에서에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-364">You will use them in the next task.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3---using-intellisense-in-javascript-documents"></a><span data-ttu-id="fbb56-365">작업 3-JavaScript 문서에 IntelliSense 사용</span><span class="sxs-lookup"><span data-stu-id="fbb56-365">Task 3 - Using IntelliSense in JavaScript Documents</span></span>

<span data-ttu-id="fbb56-366">웹 Essentials 2013과 함께 스타일 시트 및 HTML 페이지의 Id 및 클래스 이름 목록을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-366">With Web Essentials 2013, style sheets and HTML pages produce a list of IDs and class names.</span></span> <span data-ttu-id="fbb56-367">이 태스크에서는 해당 목록의 웹 Essentials 2013의 JavaScript IntelliSense 지원 개선 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-367">In this task, you will learn how those lists improve JavaScript IntelliSense support in Web Essentials 2013.</span></span>

1. <span data-ttu-id="fbb56-368">에 **Index.cshtml** 파일에서 다음 코드를 추가 정의 **스크립트** JavaScript 코드에 대 한 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-368">In the **Index.cshtml** file, add the following code to define a **script** tag for JavaScript code.</span></span>

    [!code-cshtml[Main](visual-studio-2013-web-tools/samples/sample8.cshtml)]
2. <span data-ttu-id="fbb56-369">다음 코드를 추가 **스크립트** 준비 콜백 함수를 정의 하는 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-369">Add the following code inside the **script** tag to define the ready callback function.</span></span>

    <span data-ttu-id="fbb56-370">(코드 조각- *VisualStudio2013WebTooling* - *e x 2* - *ReadyFunction*)</span><span class="sxs-lookup"><span data-stu-id="fbb56-370">(Code Snippet - *VisualStudio2013WebTooling* - *Ex2* - *ReadyFunction*)</span></span>

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample9.js)]
3. <span data-ttu-id="fbb56-371">에 캐럿 배치는 **스크립트** 태그 및 키를 눌러 **CTRL** + **합니다.**</span><span class="sxs-lookup"><span data-stu-id="fbb56-371">Place the caret in the **script** tag and press **CTRL** + **.**</span></span> <span data-ttu-id="fbb56-372">메뉴를 열려면 제안 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-372">to open the suggestion menu.</span></span>
4. <span data-ttu-id="fbb56-373">클릭 **파일로 추출할**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-373">Click **Extract To File**.</span></span>

    <span data-ttu-id="fbb56-374">![JavaScript 파일 제안 추출할](visual-studio-2013-web-tools/_static/image39.png "JavaScript 파일 제안에 추출")</span><span class="sxs-lookup"><span data-stu-id="fbb56-374">![JavaScript extract to file suggestion](visual-studio-2013-web-tools/_static/image39.png "JavaScript extract to file suggestion")</span></span>

    <span data-ttu-id="fbb56-375">*JavaScript 파일 제안에 추출*</span><span class="sxs-lookup"><span data-stu-id="fbb56-375">*JavaScript extract to file suggestion*</span></span>
5. <span data-ttu-id="fbb56-376">에 **다른 이름으로 저장** 창에서는 **스크립트** 폴더에서 파일 이름 **init.js** 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-376">In the **Save As** window, select the **Scripts** folder, name the file **init.js** and click **Save**.</span></span>

    <span data-ttu-id="fbb56-377">![다른 이름으로 저장 창](visual-studio-2013-web-tools/_static/image40.png "이름으로 저장 창")</span><span class="sxs-lookup"><span data-stu-id="fbb56-377">![Save As window](visual-studio-2013-web-tools/_static/image40.png "Save As window")</span></span>

    <span data-ttu-id="fbb56-378">*다른 이름으로 저장 창*</span><span class="sxs-lookup"><span data-stu-id="fbb56-378">*Save As window*</span></span>

    > [!NOTE]
    > <span data-ttu-id="fbb56-379">**init.js** 파일을 만들고 파일에 스크립트의 내용을 이동 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-379">The **init.js** file is created and the content of the script is moved to the file.</span></span>
    > 
    > <span data-ttu-id="fbb56-380">![포함 된 콘텐츠를 사용 하 여 만든 Init.js 파일](visual-studio-2013-web-tools/_static/image41.png "포함 된 콘텐츠를 사용 하 여 만든 Init.js 파일")</span><span class="sxs-lookup"><span data-stu-id="fbb56-380">![Init.js file created with the content included](visual-studio-2013-web-tools/_static/image41.png "Init.js file created with the content included")</span></span>
    > 
    > <span data-ttu-id="fbb56-381">*포함 된 콘텐츠를 사용 하 여 만든 Init.js 파일*</span><span class="sxs-lookup"><span data-stu-id="fbb56-381">*Init.js file created with the content included*</span></span>
6. <span data-ttu-id="fbb56-382">열기는 **Index.cshtml** 파일 및 스크립트 태그에 대 한 참조로 교체 되었습니다 확인는 **init.js** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-382">Open the **Index.cshtml** file and check that the script tag was replaced with a reference to the **init.js** file.</span></span>

    <span data-ttu-id="fbb56-383">![Init.js html 참조](visual-studio-2013-web-tools/_static/image42.png "Init.js html 참조")</span><span class="sxs-lookup"><span data-stu-id="fbb56-383">![Init.js html reference](visual-studio-2013-web-tools/_static/image42.png "Init.js html reference")</span></span>

    <span data-ttu-id="fbb56-384">*Init.js html 참조*</span><span class="sxs-lookup"><span data-stu-id="fbb56-384">*Init.js html reference*</span></span>
7. <span data-ttu-id="fbb56-385">이동 하는 **솔루션 탐색기** 과 **init.js** 파일이 솔루션에 자동으로 포함 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-385">Go to the **Solution Explorer** and notice that the **init.js** file was included automatically in the solution.</span></span>

    <span data-ttu-id="fbb56-386">![솔루션에 포함 된 Init.js 파일](visual-studio-2013-web-tools/_static/image43.png "솔루션에 포함 된 Init.js 파일")</span><span class="sxs-lookup"><span data-stu-id="fbb56-386">![Init.js file included in solution](visual-studio-2013-web-tools/_static/image43.png "Init.js file included in solution")</span></span>

    <span data-ttu-id="fbb56-387">*솔루션에 포함 된 Init.js 파일*</span><span class="sxs-lookup"><span data-stu-id="fbb56-387">*Init.js file included in solution*</span></span>
8. <span data-ttu-id="fbb56-388">로 다시 전환는 **init.js** 업데이트할 파일을 여 **준비** 콜백 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-388">Switch back to the **init.js** file to update the **ready** function callback.</span></span>
9. <span data-ttu-id="fbb56-389">에 전달 되는 함수 콜백 정의 내 *준비*, 요소를 가져오는 모든 특정 클래스 특성으로 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-389">Inside the function callback definition that is passed to *ready*, add the following code to get all the elements by a specific class attribute.</span></span>

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample10.js)]
10. <span data-ttu-id="fbb56-390">키를 눌러 **CTRL** + **공간** 내 고 따옴표 사이 **getElementsByClassName** 함수 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-390">Press **CTRL** + **Space** between the quotes inside the **getElementsByClassName** function call.</span></span>

    <span data-ttu-id="fbb56-391">![GetElementsByClassName 함수에 대 한 IntelliSense를 보여 주는](visual-studio-2013-web-tools/_static/image44.png "getElementsByClassName 함수에 대 한 보여 주는 IntelliSense")</span><span class="sxs-lookup"><span data-stu-id="fbb56-391">![Showing IntelliSense for the getElementsByClassName function](visual-studio-2013-web-tools/_static/image44.png "Showing IntelliSense for the getElementsByClassName function")</span></span>

    <span data-ttu-id="fbb56-392">*IntelliSense getElementsByClassName 함수에 대 한 표시*</span><span class="sxs-lookup"><span data-stu-id="fbb56-392">*Showing IntelliSense for the getElementsByClassName function*</span></span>

    > [!NOTE]
    > <span data-ttu-id="fbb56-393">IntelliSense 프로젝트 스타일 시트에 정의 된 클래스에 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-393">Notice that IntelliSense shows the classes defined in the project style sheets.</span></span>
11. <span data-ttu-id="fbb56-394">다음 코드를 사용 하 여 생성 하는 줄을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-394">Replace the line that you have created with the following code.</span></span>

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample11.js)]
12. <span data-ttu-id="fbb56-395">뒤에 커서를 놓습니다 **au** 에서 따옴표에 포함 된 **getElementsByTagName** 함수 및 키를 눌러 **CTRL** + **공간**.</span><span class="sxs-lookup"><span data-stu-id="fbb56-395">Position the cursor after **au** inside the quotes in the **getElementsByTagName** function and press **CTRL** + **Space**.</span></span>

    <span data-ttu-id="fbb56-396">![GetElementByTagName 메서드에 대 한 IntelliSense를 보여 주는](visual-studio-2013-web-tools/_static/image45.png "getElementByTagName 메서드를 보여 주는 IntelliSense")</span><span class="sxs-lookup"><span data-stu-id="fbb56-396">![Showing IntelliSense for the getElementByTagName method](visual-studio-2013-web-tools/_static/image45.png "Showing IntelliSense for the getElementByTagName method")</span></span>

    <span data-ttu-id="fbb56-397">*IntelliSense getElementsByTagName 메서드에 대 한 표시*</span><span class="sxs-lookup"><span data-stu-id="fbb56-397">*Showing IntelliSense for the getElementsByTagName method*</span></span>
13. <span data-ttu-id="fbb56-398">선택 **&quot;오디오&quot;** 목록 및 키를 눌러 **ENTER**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-398">Select **&quot;audio&quot;** from the list and press **ENTER**.</span></span> <span data-ttu-id="fbb56-399">결과는 다음 그림에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-399">The result is shown in the following figure.</span></span>

    <span data-ttu-id="fbb56-400">![오디오 요소 검색](visual-studio-2013-web-tools/_static/image46.png "오디오으로 요소 검색")</span><span class="sxs-lookup"><span data-stu-id="fbb56-400">![Retrieving Audio Elements](visual-studio-2013-web-tools/_static/image46.png "Retrieving Audio Elements")</span></span>

    <span data-ttu-id="fbb56-401">*오디오 요소 검색*</span><span class="sxs-lookup"><span data-stu-id="fbb56-401">*Retrieving Audio Elements*</span></span>
14. <span data-ttu-id="fbb56-402">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **init.js** 파일에 **스크립트** 폴더를 선택 **축소할 JavaScript 파일** 에서 **웹 Essentials** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="fbb56-402">In **Solution Explorer**, right-click the **init.js** file in the **Scripts** folder and select **Minify JavaScript file(s)** from the **Web Essentials** menu.</span></span>

    <span data-ttu-id="fbb56-403">![JavaScript 파일을 축소할](visual-studio-2013-web-tools/_static/image47.png "축소할 JavaScript 파일")</span><span class="sxs-lookup"><span data-stu-id="fbb56-403">![Minify JavaScript file(s)](visual-studio-2013-web-tools/_static/image47.png "Minify JavaScript files")</span></span>

    <span data-ttu-id="fbb56-404">*JavaScript 파일을 축소합니다*</span><span class="sxs-lookup"><span data-stu-id="fbb56-404">*Minify JavaScript file(s)*</span></span>
15. <span data-ttu-id="fbb56-405">소스 파일 변경 내용을 클릭할 때 자동 축소를 사용 하도록 설정 하 라는 메시지가 나타나면 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-405">When prompted to enable automatic minification when the source file changes click **Yes**.</span></span>

    <span data-ttu-id="fbb56-406">![자동 축소 경고를 사용 하도록 설정](visual-studio-2013-web-tools/_static/image48.png "자동 축소 경고를 사용 하도록 설정")</span><span class="sxs-lookup"><span data-stu-id="fbb56-406">![Enabling automatic minification warning](visual-studio-2013-web-tools/_static/image48.png "Enabling automatic minification warning")</span></span>

    <span data-ttu-id="fbb56-407">*자동 축소 경고를 사용 하도록 설정*</span><span class="sxs-lookup"><span data-stu-id="fbb56-407">*Enabling automatic minification warning*</span></span>

    > [!NOTE]
    > <span data-ttu-id="fbb56-408">**init.min.js** 생성 되 고의 종속 항목으로 추가 된 **init.js** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-408">The **init.min.js** is created and is added as a dependency of the **init.js** file.</span></span>
    > 
    > <span data-ttu-id="fbb56-409">![만든 Init.min.js 파일](visual-studio-2013-web-tools/_static/image49.png "만든 Init.min.js 파일")</span><span class="sxs-lookup"><span data-stu-id="fbb56-409">![Init.min.js file created](visual-studio-2013-web-tools/_static/image49.png "Init.min.js file created")</span></span>
    > 
    > <span data-ttu-id="fbb56-410">*만든 Init.min.js 파일*</span><span class="sxs-lookup"><span data-stu-id="fbb56-410">*Init.min.js file created*</span></span>
16. <span data-ttu-id="fbb56-411">열기는 **init.min.js** 파일 및 파일 축소는 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-411">Open the **init.min.js** file and notice that the file is minified.</span></span>

    <span data-ttu-id="fbb56-412">![Init.min.js 파일 내용을](visual-studio-2013-web-tools/_static/image50.png "Init.min.js 파일 콘텐츠")</span><span class="sxs-lookup"><span data-stu-id="fbb56-412">![Init.min.js file content](visual-studio-2013-web-tools/_static/image50.png "Init.min.js file content")</span></span>

    <span data-ttu-id="fbb56-413">*Init.min.js 파일 콘텐츠*</span><span class="sxs-lookup"><span data-stu-id="fbb56-413">*Init.min.js file content*</span></span>
17. <span data-ttu-id="fbb56-414">에 **init.js** 파일, 아래 다음 코드를 추가 **getElementsByTagName** 함수 호출에 오디오 모든 요소를 재생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-414">In the **init.js** file, add the following code below the **getElementsByTagName** function call to play all the audio elements.</span></span>

    <span data-ttu-id="fbb56-415">(코드 조각- *VisualStudio2013WebTooling* - *e x 2* - *PlayAudioElements*)</span><span class="sxs-lookup"><span data-stu-id="fbb56-415">(Code Snippet - *VisualStudio2013WebTooling* - *Ex2* - *PlayAudioElements*)</span></span>

    [!code-csharp[Main](visual-studio-2013-web-tools/samples/sample12.cs)]
18. <span data-ttu-id="fbb56-416">클릭 **CTRL** + **S** 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-416">Click **CTRL** + **S** to save the file.</span></span> <span data-ttu-id="fbb56-417">축소 된 파일을 열면 이미 있으므로 파일이 소스 편집기 외부에서 수정 된 없다는 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-417">Since the minified file is already opened, you will see a dialog box saying that the file was modified outside of the source editor.</span></span> <span data-ttu-id="fbb56-418">**예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-418">Click **Yes**.</span></span>

    <span data-ttu-id="fbb56-419">![Microsoft Visual Studio 경고](visual-studio-2013-web-tools/_static/image51.png "Microsoft Visual Studio 경고")</span><span class="sxs-lookup"><span data-stu-id="fbb56-419">![Microsoft Visual Studio warning](visual-studio-2013-web-tools/_static/image51.png "Microsoft Visual Studio warning")</span></span>

    <span data-ttu-id="fbb56-420">*Microsoft Visual Studio 경고*</span><span class="sxs-lookup"><span data-stu-id="fbb56-420">*Microsoft Visual Studio warning*</span></span>
19. <span data-ttu-id="fbb56-421">로 다시 전환는 **init.min.js** 파일을 새 코드 파일을 업데이트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-421">Switch back to the **init.min.js** file to verify that the file was updated with the new code.</span></span>

    <span data-ttu-id="fbb56-422">![업데이트 Init.min.js 파일](visual-studio-2013-web-tools/_static/image52.png "Init.min.js 파일 업데이트")</span><span class="sxs-lookup"><span data-stu-id="fbb56-422">![Init.min.js file updated](visual-studio-2013-web-tools/_static/image52.png "Init.min.js file updated")</span></span>

    <span data-ttu-id="fbb56-423">*Init.min.js 파일 업데이트*</span><span class="sxs-lookup"><span data-stu-id="fbb56-423">*Init.min.js file updated*</span></span>
20. <span data-ttu-id="fbb56-424">클릭는 **브라우저 링크 새로 고침** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-424">Click the **Browser Link Refresh** button.</span></span>
21. <span data-ttu-id="fbb56-425">두 브라우저 새로 고침 되 면 이전 작업에서 표시 오디오 플레이어는 자동으로 재생이 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbb56-425">Once both browsers are refreshed the audio players you saw in the previous task will start playing automatically.</span></span>

    <span data-ttu-id="fbb56-426">![보기에 포함 되는 오디오 플레이어](visual-studio-2013-web-tools/_static/image53.png "오디오 플레이어 보기에 포함")</span><span class="sxs-lookup"><span data-stu-id="fbb56-426">![Audio player included in view](visual-studio-2013-web-tools/_static/image53.png "Audio player included in view")</span></span>

    <span data-ttu-id="fbb56-427">*보기에 포함 되는 오디오 플레이어*</span><span class="sxs-lookup"><span data-stu-id="fbb56-427">*Audio player included in view*</span></span>

* * *

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="fbb56-428">요약</span><span class="sxs-lookup"><span data-stu-id="fbb56-428">Summary</span></span>

<span data-ttu-id="fbb56-429">이 실습 랩을 완료 하 여 배웠습니다 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="fbb56-429">By completing this hands-on lab you have learned how to:</span></span>

- <span data-ttu-id="fbb56-430">풍부한 HTML5 코드 조각 및 Zen 코딩 등 웹 Essentials에 포함 된 새 HTML 편집기 기능을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="fbb56-430">Use new HTML editor features included in Web Essentials such as rich HTML5 code snippets and Zen coding</span></span>
- <span data-ttu-id="fbb56-431">색 선택 및 브라우저 매트릭스 도구 설명 같은 웹 Essentials에 포함 된 새 CSS 편집기 기능을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="fbb56-431">Use new CSS editor features included in Web Essentials such as the Color picker and Browser matrix tooltip</span></span>
- <span data-ttu-id="fbb56-432">모든 HTML 요소에 대 한 IntelliSense 파일을 추출 같은 웹 Essentials에 포함 된 새로운 JavaScript 편집기 기능을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="fbb56-432">Use new JavaScript editor features included in Web Essentials such as Extract to File and IntelliSense for all HTML elements</span></span>
- <span data-ttu-id="fbb56-433">브라우저 및 브라우저 링크를 사용 하 여 Visual Studio 사이 데이터 교환</span><span class="sxs-lookup"><span data-stu-id="fbb56-433">Exchange data between your browser and Visual Studio using Browser Link</span></span>
