---
uid: mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
title: ASP.NET MVC 4의에서 새로운 기능 | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4는 ASP.NET의 능력에 대 한 체계적인 디자인 패턴을 사용 하 여 확장 가능 하 고 표준 기반 웹 응용 프로그램을 구축 하기 위한 프레임 워크 및...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 48f7feb3-872f-485d-b96f-e30011ff8c4a
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 977a6b5a84825ebd087752dcc2ebc0c5410e1657
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2018
---
# <a name="whats-new-in-aspnet-mvc-4"></a><span data-ttu-id="966f0-103">ASP.NET MVC 4의에서 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="966f0-103">What's New in ASP.NET MVC 4</span></span>

<span data-ttu-id="966f0-104">으로 [웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="966f0-104">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="966f0-105">웹 캠프 학습 키트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="966f0-106">ASP.NET MVC 4는 ASP.NET 및.NET framework의 능력에 대 한 체계적인 디자인 패턴을 사용 하 여 확장 가능 하 고 표준 기반 웹 응용 프로그램을 구축 하기 위한 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="966f0-106">ASP.NET MVC 4 is a framework for building scalable, standards-based web applications using well-established design patterns and the power of the ASP.NET and the .NET framework.</span></span> <span data-ttu-id="966f0-107">이 새로운, 네 번째 버전의 framework 모바일 웹 응용 프로그램 개발을 보다 쉽게에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-107">This new, fourth version of the framework focuses on making mobile web application development easier.</span></span>

<span data-ttu-id="966f0-108">처음에 새 ASP.NET MVC 4 프로젝트를 만들 때 이제 되어 모바일 응용 프로그램 프로젝트 템플릿을 모바일 장치용으로 독립 실행형 응용 프로그램을 만드는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-108">To begin with, when you create a new ASP.NET MVC 4 project there is now a mobile application project template you can use to build a standalone app specifically for mobile devices.</span></span> <span data-ttu-id="966f0-109">또한 ASP.NET MVC 4 jQuery Mobile jQuery.Mobile.MVC NuGet 패키지를 통해 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-109">Additionally, ASP.NET MVC 4 integrates with jQuery Mobile through a jQuery.Mobile.MVC NuGet package.</span></span> <span data-ttu-id="966f0-110">jQuery Mobile 등의 Windows Phone, iPhone, Android를 포함 하 여 모든 인기 있는 모바일 장치 플랫폼에 호환 되는 웹 응용 프로그램을 개발 하기 위한 HTML5 기반 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-110">jQuery Mobile is an HTML5-based framework for developing web apps that are compatible with all popular mobile device platforms, including Windows Phone, iPhone, Android and so on.</span></span> <span data-ttu-id="966f0-111">그러나 특수화 해야 할 경우 ASP.NET MVC 4도 사용 하면 다양 한 장치에 대해 개별 보기를 처리 하 고 장치별 최적화를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-111">However, if you need specialization, ASP.NET MVC 4 also enables you to serve different views for different devices and provide device-specific optimizations.</span></span>

<span data-ttu-id="966f0-112">ASP.NET MVC 4로 시작 됩니다이 실습 랩에서 &quot;인터넷 응용 프로그램&quot; 사진 갤러리 응용 프로그램을 만드는 프로젝트 템플릿을 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-112">In this hands-on lab, you will start with the ASP.NET MVC 4 &quot;Internet Application&quot; project template to create a Photo Gallery application.</span></span> <span data-ttu-id="966f0-113">JQuery Mobile 및 ASP.NET MVC 4의 새로운 기능을 사용 하 여 다양 한 모바일 장치 및 데스크톱 웹 브라우저와 호환 되도록 하려면 앱을 점진적으로 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-113">You will progressively enhance the app using jQuery Mobile and ASP.NET MVC 4's new features to make it compatible with different mobile devices and desktop web browsers.</span></span> <span data-ttu-id="966f0-114">코드 생성 및 ASP.NET MVC 4 사용을 쉽게 방법 작업을 지원 하 여 비동기 작업 메서드를 작성할 수에 대 한 새 코드 레시피에 대 한 배웁니다&lt;ActionResult&gt; 형식을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-114">You will also learn about new code recipes for code generation and how ASP.NET MVC 4 makes it easier for you to write asynchronous action methods by supporting Task&lt;ActionResult&gt; return types.</span></span>

> [!NOTE]
> <span data-ttu-id="966f0-115">모든 샘플 코드와 코드 조각을 웹 캠프 교육 키트에서 사용할 수에 포함 된 [Microsoft-웹/WebCampTrainingKit 릴리스](https://aka.ms/webcamps-training-kit)합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-115">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="966f0-116">이 랩에 특정 프로젝트에서 사용할 수는 [What's New in ASP.NET 4.5에서 Web Forms](https://github.com/Microsoft-Web/HOL-ASPNETWebForms)합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-116">The project specific to this lab is available at [What's New in Web Forms in ASP.NET 4.5](https://github.com/Microsoft-Web/HOL-ASPNETWebForms).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="966f0-117">목표</span><span class="sxs-lookup"><span data-stu-id="966f0-117">Objectives</span></span>

<span data-ttu-id="966f0-118">이 실습 랩에서 배웁니다 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="966f0-118">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="966f0-119">ASP.NET MVC 프로젝트 템플릿을 포함 한 새로운 모바일 응용 프로그램 프로젝트 템플릿을에 향상 된 기능을 활용</span><span class="sxs-lookup"><span data-stu-id="966f0-119">Take advantage of the enhancements to the ASP.NET MVC project templates-including the new mobile application project template</span></span>
- <span data-ttu-id="966f0-120">HTML5 뷰포트 특성 및 CSS 미디어 쿼리를 사용 하 여 모바일 장치에 표시를 향상 시키기</span><span class="sxs-lookup"><span data-stu-id="966f0-120">Use the HTML5 viewport attribute and CSS media queries to improve the display on mobile devices</span></span>
- <span data-ttu-id="966f0-121">JQuery Mobile 점진적 향상 된 기능에 대 한 터치에 최적화 된 웹 UI를 작성 하기 위한 사용</span><span class="sxs-lookup"><span data-stu-id="966f0-121">Use jQuery Mobile for progressive enhancements and for building touch-optimized web UI</span></span>
- <span data-ttu-id="966f0-122">모바일 전용 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="966f0-122">Create mobile-specific views</span></span>
- <span data-ttu-id="966f0-123">뷰 전환기 구성 요소를 사용 하 여 응용 프로그램에 모바일 및 데스크톱 뷰 사이 전환 하려면</span><span class="sxs-lookup"><span data-stu-id="966f0-123">Use the view-switcher component to toggle between mobile and desktop views in the application</span></span>
- <span data-ttu-id="966f0-124">비동기 컨트롤러 작업 지원을 사용 하 여 만들기</span><span class="sxs-lookup"><span data-stu-id="966f0-124">Create asynchronous controllers using task support</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="966f0-125">전제 조건</span><span class="sxs-lookup"><span data-stu-id="966f0-125">Prerequisites</span></span>

<span data-ttu-id="966f0-126">이 랩을 완료 하려면 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-126">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="966f0-127">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) 하거나 그 보다 뛰어난 (읽기 [부록 B](#AppendixB) 설치 하는 방법에 대 한 지침은).</span><span class="sxs-lookup"><span data-stu-id="966f0-127">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix B](#AppendixB) for instructions on how to install it).</span></span>
- <span data-ttu-id="966f0-128">[ASP.NET MVC 4](../../../mvc4.md) (Microsoft Visual Studio 2012 설치에 포함 됨)</span><span class="sxs-lookup"><span data-stu-id="966f0-128">[ASP.NET MVC 4](../../../mvc4.md) (included in the Microsoft Visual Studio 2012 installation)</span></span>
- <span data-ttu-id="966f0-129">Windows Phone 에뮬레이터 (에 포함 된 [7.1.1 Windows Phone SDK](https://www.microsoft.com/download/details.aspx?id=29233))</span><span class="sxs-lookup"><span data-stu-id="966f0-129">Windows Phone Emulator (included in the [Windows Phone 7.1.1 SDK](https://www.microsoft.com/download/details.aspx?id=29233))</span></span>
- <span data-ttu-id="966f0-130">선택 사항- [WebMatrix 2](https://www.microsoft.com/web/webmatrix/) 와 **Electric Plum iPhone 시뮬레이터** (iPhone 시뮬레이터와 웹 응용 프로그램을 탐색 하는 데 사용 하는 연습 3)에 확장</span><span class="sxs-lookup"><span data-stu-id="966f0-130">Optional - [WebMatrix 2](https://www.microsoft.com/web/webmatrix/) with **Electric Plum iPhone Simulator** extension (only for Exercise 3 used to browse the web application with an iPhone simulator)</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="966f0-131">설정</span><span class="sxs-lookup"><span data-stu-id="966f0-131">Setup</span></span>

<span data-ttu-id="966f0-132">랩 문서를 통해 코드 블록을 삽입 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-132">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="966f0-133">사용자 편의 위해 해당 코드의 대부분을 수동으로 추가할 필요가 없도록 하려면 Visual Studio 내에서 사용할 수 있는 Visual Studio 코드 조각으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-133">For your convenience, most of that code is provided as Visual Studio Code Snippets, which you can use from within Visual Studio to avoid having to add it manually.</span></span>

<span data-ttu-id="966f0-134">설치 하려면 코드 조각:</span><span class="sxs-lookup"><span data-stu-id="966f0-134">To install the code snippets:</span></span>

1. <span data-ttu-id="966f0-135">Windows 탐색기 창을 열고 다음을 찾아보기에 랩 **Source\Setup** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-135">Open a Windows Explorer window and browse to the lab's **Source\Setup** folder.</span></span>
2. <span data-ttu-id="966f0-136">두 번 클릭은 **Setup.cmd** Visual Studio 코드 조각을 설치 하려면이 폴더에는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-136">Double-click the **Setup.cmd** file in this folder to install the Visual Studio code snippets.</span></span>

<span data-ttu-id="966f0-137">이 문서에서 부록을 참조할 수 사용 하는 방법에 알아봅니다 사용 하 고 Visual Studio 코드 조각에 익숙한 경우 &quot; [부록 a:를 사용 하 여 코드 조각을](#AppendixA)&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-137">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix A: Using Code Snippets](#AppendixA)&quot;.</span></span>

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="966f0-138">연습</span><span class="sxs-lookup"><span data-stu-id="966f0-138">Exercises</span></span>

<span data-ttu-id="966f0-139">이 실습 랩에서 다음 연습에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-139">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="966f0-140">새 ASP.NET MVC 4 프로젝트 템플릿</span><span class="sxs-lookup"><span data-stu-id="966f0-140">New ASP.NET MVC 4 Project Templates</span></span>](#Exercise1)
2. [<span data-ttu-id="966f0-141">사진 갤러리 웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="966f0-141">Creating the Photo Gallery Web Application</span></span>](#Exercise2)
3. [<span data-ttu-id="966f0-142">모바일 장치에 대 한 지원 추가</span><span class="sxs-lookup"><span data-stu-id="966f0-142">Adding Support for Mobile Devices</span></span>](#Exercise3)
4. [<span data-ttu-id="966f0-143">비동기 컨트롤러를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="966f0-143">Using Asynchronous Controllers</span></span>](#Exercise4)

> [!NOTE]
> <span data-ttu-id="966f0-144">각 연습 동반 되는 **끝** 연습을 완료 한 후 가져와야 생성 되는 솔루션에 포함 된 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-144">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="966f0-145">연습을 통해 작업 하는 추가 도움이 필요한 경우이 솔루션 가이드로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-145">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<span data-ttu-id="966f0-146">예상 소요 시간: **60 분**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-146">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_New_ASPNET_MVC_4_Project_Templates"></a>
### <a name="exercise-1-new-aspnet-mvc-4-project-templates"></a><span data-ttu-id="966f0-147">연습 1: 새 ASP.NET MVC 4 프로젝트 템플릿</span><span class="sxs-lookup"><span data-stu-id="966f0-147">Exercise 1: New ASP.NET MVC 4 Project Templates</span></span>

<span data-ttu-id="966f0-148">이 연습에서는 ASP.NET MVC 4 프로젝트 템플릿의 향상 된 기능을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-148">In this exercise, you will explore the enhancements in the ASP.NET MVC 4 Project templates.</span></span> <span data-ttu-id="966f0-149">인터넷 응용 프로그램 템플릿 외에 MVC 3에 이미 있는이 버전 이제 포함 된 별도 템플릿이 모바일 응용 프로그램에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-149">In addition to the Internet Application template, already present in MVC 3, this version now includes a separate template for Mobile applications.</span></span> <span data-ttu-id="966f0-150">먼저, 각 템플릿의 몇 가지 관련 기능에 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-150">First, you will look at some relevant features of each of the templates.</span></span> <span data-ttu-id="966f0-151">그런 다음에서 적합 한 접근 방식을 사용 하 여 서로 다른 플랫폼에서 올바르게 페이지 렌더링에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-151">Then, you will work on rendering your page properly on the different platforms by using the right approach.</span></span>

<a id="Task_1_-_Exploring_the_Internet_Application_Template"></a>
#### <a name="task-1---exploring-the-internet-application-template"></a><span data-ttu-id="966f0-152">작업 1-인터넷 응용 프로그램 템플릿에서 탐색</span><span class="sxs-lookup"><span data-stu-id="966f0-152">Task 1 - Exploring the Internet Application Template</span></span>

1. <span data-ttu-id="966f0-153">열기 **Visual Studio**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-153">Open **Visual Studio**.</span></span>
2. <span data-ttu-id="966f0-154">선택 된 **파일 | 새로 만들기 | 프로젝트** 메뉴 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-154">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="966f0-155">에 **새 프로젝트** 대화 상자에서 선택 된 **Visual C# | 웹** 서식 파일의 왼쪽된 창에서 선택한 트리의 **ASP.NET MVC 4 웹 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="966f0-155">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="966f0-156">프로젝트 이름을 **PhotoGallery**, 위치를 선택 (또는 기본값을 그대로 적용)를 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-156">Name the project **PhotoGallery**, select a location (or leave the default) and click **OK**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="966f0-157">지금 만들려는 PhotoGallery ASP.NET MVC 4 솔루션 나중에 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-157">You will later customize the PhotoGallery ASP.NET MVC 4 solution you are now creating.</span></span>

    <span data-ttu-id="966f0-158">![새 프로젝트를 만드는](whats-new-in-aspnet-mvc-4/_static/image1.png "새 프로젝트 만들기")</span><span class="sxs-lookup"><span data-stu-id="966f0-158">![Creating a new project](whats-new-in-aspnet-mvc-4/_static/image1.png "Creating a new project")</span></span>

    <span data-ttu-id="966f0-159">*새 프로젝트 만들기*</span><span class="sxs-lookup"><span data-stu-id="966f0-159">*Creating a new project*</span></span>
3. <span data-ttu-id="966f0-160">에 **새 ASP.NET MVC 4 프로젝트** 대화 상자에서는 **인터넷 응용 프로그램** 프로젝트 템플릿과 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-160">In the **New ASP.NET MVC 4 Project** dialog, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="966f0-161">Razor 뷰 엔진으로 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-161">Make sure you have selected Razor as the view engine.</span></span>

    <span data-ttu-id="966f0-162">![새 ASP.NET MVC 4 인터넷 응용 프로그램을 만드는](whats-new-in-aspnet-mvc-4/_static/image2.png "새 ASP.NET MVC 4 인터넷 응용 프로그램 만들기")</span><span class="sxs-lookup"><span data-stu-id="966f0-162">![Creating a new ASP.NET MVC 4 Internet Application](whats-new-in-aspnet-mvc-4/_static/image2.png "Creating a new ASP.NET MVC 4 Internet Application")</span></span>

    <span data-ttu-id="966f0-163">*새 ASP.NET MVC 4 인터넷 응용 프로그램 만들기*</span><span class="sxs-lookup"><span data-stu-id="966f0-163">*Creating a new ASP.NET MVC 4 Internet Application*</span></span>

    > [!NOTE]
    > <span data-ttu-id="966f0-164">ASP.NET MVC 3에서 razor 구문이 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-164">Razor syntax has been introduced in ASP.NET MVC 3.</span></span> <span data-ttu-id="966f0-165">목표의 문자 및 fast 및 워크플로 코딩 하는 유체 파일에 필요한 키 입력의 수를 최소화 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-165">Its goal is to minimize the number of characters and keystrokes required in a file, enabling a fast and fluid coding workflow.</span></span> <span data-ttu-id="966f0-166">Razor를 활용 하 여 기존 C# / VB 또는 다른 언어 기술을 놀라운 HTML 생성 워크플로 수 있도록 하는 템플릿 태그 구문을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-166">Razor leverages existing C# / VB (or other) language skills and delivers a template markup syntax that enables an awesome HTML construction workflow.</span></span>
4. <span data-ttu-id="966f0-167">키를 눌러 **F5** 하는 솔루션을 실행 하 고 갱신 된 템플릿을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-167">Press **F5** to run the solution and see the renewed templates.</span></span> <span data-ttu-id="966f0-168">다음 기능을 사용해 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-168">You can check out the following features:</span></span>

    <span data-ttu-id="966f0-169">**최신 스타일 템플릿**</span><span class="sxs-lookup"><span data-stu-id="966f0-169">**Modern-style templates**</span></span>

    <span data-ttu-id="966f0-170">서식 파일 갱신 된, 더 많은 현대 수준의 스타일을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-170">The templates have been renewed, providing more modern-looking styles.</span></span>

    <span data-ttu-id="966f0-171">![ASP.NET MVC 4 맞게 스타일을 다시 템플릿](whats-new-in-aspnet-mvc-4/_static/image3.png "맞게 템플릿 스타일을 다시 MVC 4")</span><span class="sxs-lookup"><span data-stu-id="966f0-171">![ASP.NET MVC 4 restyled templates](whats-new-in-aspnet-mvc-4/_static/image3.png "MVC 4 restyled templates")</span></span>

    <span data-ttu-id="966f0-172">*ASP.NET MVC 4 맞게 스타일을 다시 템플릿*</span><span class="sxs-lookup"><span data-stu-id="966f0-172">*ASP.NET MVC 4 restyled templates*</span></span>

    <span data-ttu-id="966f0-173">![새 연락처 페이지](whats-new-in-aspnet-mvc-4/_static/image4.png "새 연락처 페이지")</span><span class="sxs-lookup"><span data-stu-id="966f0-173">![New Contact page](whats-new-in-aspnet-mvc-4/_static/image4.png "New Contact page")</span></span>

    <span data-ttu-id="966f0-174">*새 연락처 페이지*</span><span class="sxs-lookup"><span data-stu-id="966f0-174">*New Contact page*</span></span>

    <span data-ttu-id="966f0-175">**자동 선택 렌더링**</span><span class="sxs-lookup"><span data-stu-id="966f0-175">**Adaptive Rendering**</span></span>

    <span data-ttu-id="966f0-176">체크 아웃 브라우저 창 크기 조정 고 페이지 레이아웃 새 창 크기를 동적으로 반응 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-176">Check out resizing the browser window and notice how the page layout dynamically adapts to the new window size.</span></span> <span data-ttu-id="966f0-177">이러한 템플릿은 자동 선택 렌더링 기술을 사용 하 여 사용자 지정 하지 않고 데스크톱 및 모바일 플랫폼에서 모두 올바르게 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-177">These templates use the adaptive rendering technique to render properly in both desktop and mobile platforms without any customization.</span></span>

    <span data-ttu-id="966f0-178">![다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿에서](whats-new-in-aspnet-mvc-4/_static/image5.png "다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿")</span><span class="sxs-lookup"><span data-stu-id="966f0-178">![ASP.NET MVC 4 project template in different browser sizes](whats-new-in-aspnet-mvc-4/_static/image5.png "ASP.NET MVC 4 project template in different browser sizes")</span></span>

    <span data-ttu-id="966f0-179">*다른 브라우저 크기의 ASP.NET MVC 4 프로젝트 템플릿*</span><span class="sxs-lookup"><span data-stu-id="966f0-179">*ASP.NET MVC 4 project template in different browser sizes*</span></span>

    <span data-ttu-id="966f0-180">**JavaScript와 함께 다양 한 UI**</span><span class="sxs-lookup"><span data-stu-id="966f0-180">**Richer UI with JavaScript**</span></span>

    <span data-ttu-id="966f0-181">기본 프로젝트 템플릿과 다른 향상 좀 더 대화형 JavaScript를 제공 하는 JavaScript 사용 하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-181">Another enhancement to default project templates is the use of JavaScript to provide a more interactive JavaScript.</span></span> <span data-ttu-id="966f0-182">서식 파일에 사용 된 로그인 및 등록 링크를 jQuery 유효성 검사를 사용 하 여 클라이언트 쪽에서 입력된 필드의 유효성을 검사 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-182">The Login and Register links used in the template exemplify how to use the jQuery Validations to validate the input fields from client-side.</span></span>

    ![jQuery 유효성 검사](whats-new-in-aspnet-mvc-4/_static/image6.png)

    <span data-ttu-id="966f0-184">*jQuery 유효성 검사*</span><span class="sxs-lookup"><span data-stu-id="966f0-184">*jQuery Validation*</span></span>

    > [!NOTE]
    > <span data-ttu-id="966f0-185">두 섹션에서는 첫 번째 섹션에 로그인 하는 예 고 두 번째 섹션 altenativelly google (기본적으로 해제 됨)와 같은 다른 인증 서비스를 사용 하 여 로그인 할 수 있습니다 및 사이트에서 registerd 계정을 사용 하 여 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-185">Notice the two log in sections, in the first section you can log in using a registerd account from the site and in the second section you can altenativelly log in using another authentication service like google (disabled by default).</span></span>
5. <span data-ttu-id="966f0-186">디버거를 중지 하려면 Visual Studio로 되돌아가려면 브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-186">Close the browser to stop the debugger and return to Visual Studio.</span></span>
6. <span data-ttu-id="966f0-187">파일을 열고 **AuthConfig.cs** 아래에 **앱\_시작** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-187">Open the file **AuthConfig.cs** located under the **App\_Start** folder.</span></span>
7. <span data-ttu-id="966f0-188">에 대 한 Google 클라이언트를 등록 하 고 마지막 줄에서 주석 제거 *OAuth* 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-188">Remove the comment from the last line to register Google client for *OAuth* authentication.</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample1.cs)]

> [!NOTE]
> Notice you can easily enable authentication using any OpenID or OAuth service like Facebook, Twitter, Microsoft, etc.
~~~
8. <span data-ttu-id="966f0-189">키를 눌러 **F5** 하는 솔루션을 실행 하 고 로그인 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-189">Press **F5** to run the solution and navigate to the login page.</span></span>
9. <span data-ttu-id="966f0-190">선택 **Google** 서비스에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-190">Select **Google** service to log in.</span></span>

    ![서비스에서 로그를 선택합니다.](whats-new-in-aspnet-mvc-4/_static/image7.png)

    <span data-ttu-id="966f0-192">*서비스에서 로그를 선택합니다.*</span><span class="sxs-lookup"><span data-stu-id="966f0-192">*Selecting the log in service*</span></span>
10. <span data-ttu-id="966f0-193">Google 계정을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-193">Log in using your Google account.</span></span>
11. <span data-ttu-id="966f0-194">Google 계정에서 정보를 검색할 사이트 (localhost)를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-194">Allow the site (localhost) to retrieve information from Google account.</span></span>
12. <span data-ttu-id="966f0-195">마지막으로, Google 계정을 연결 하는 사이트에 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-195">Finally, you will have to register in the site to associate the Google account.</span></span>

   ![Google 계정 연결](whats-new-in-aspnet-mvc-4/_static/image8.png)

   <span data-ttu-id="966f0-197">*Google 계정 연결*</span><span class="sxs-lookup"><span data-stu-id="966f0-197">*Associating your Google account*</span></span>
13. <span data-ttu-id="966f0-198">디버거를 중지 하려면 Visual Studio로 되돌아가려면 브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-198">Close the browser to stop the debugger and return to Visual Studio.</span></span>
14. <span data-ttu-id="966f0-199">이제 솔루션을 체크 아웃 프로젝트 템플릿에 있는 ASP.NET MVC 4에서 도입 된 몇 가지 다른 새로운 기능을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-199">Now explore the solution to check out some other new features introduced by ASP.NET MVC 4 in the project template.</span></span>

   <span data-ttu-id="966f0-200">![ASP.NET MVC 4 인터넷 응용 프로그램 프로젝트 템플릿을](whats-new-in-aspnet-mvc-4/_static/image9.png "ASP.NET MVC 4 인터넷 응용 프로그램 프로젝트 템플릿을")</span><span class="sxs-lookup"><span data-stu-id="966f0-200">![The ASP.NET MVC 4 Internet Application Project Template](whats-new-in-aspnet-mvc-4/_static/image9.png "The ASP.NET MVC 4 Internet Application Project Template")</span></span>

   <span data-ttu-id="966f0-201">*ASP.NET MVC 4 인터넷 응용 프로그램 프로젝트 템플릿*</span><span class="sxs-lookup"><span data-stu-id="966f0-201">*The ASP.NET MVC 4 Internet Application Project Template*</span></span>

   - <span data-ttu-id="966f0-202">**HTML 5 태그**</span><span class="sxs-lookup"><span data-stu-id="966f0-202">**HTML 5 Markup**</span></span>

       <span data-ttu-id="966f0-203">새 테마 마크업 알아보려면 템플릿을 뷰를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-203">Browse template views to find out the new theme markup.</span></span>

       <span data-ttu-id="966f0-204">![Razor 및 HTML5 태그 About.cshtml를 사용 하 여 새 템플릿. ] (whats-new-in-aspnet-mvc-4/_static/image10.png "About.cshtml Razor 및 HTML5 태그를 사용 하 여 새 서식 파일입니다.")</span><span class="sxs-lookup"><span data-stu-id="966f0-204">![New template, using Razor and HTML5 markup About.cshtml.](whats-new-in-aspnet-mvc-4/_static/image10.png "New template, using Razor and HTML5 markup About.cshtml.")</span></span>

       <span data-ttu-id="966f0-205">*Razor 및 HTML5 태그 (About.cshtml)를 사용 하 여 새 템플릿.*</span><span class="sxs-lookup"><span data-stu-id="966f0-205">*New template, using Razor and HTML5 markup (About.cshtml).*</span></span>
   - <span data-ttu-id="966f0-206">**업데이트 된 JavaScript 라이브러리**</span><span class="sxs-lookup"><span data-stu-id="966f0-206">**Updated JavaScript libraries**</span></span>

       <span data-ttu-id="966f0-207">ASP.NET MVC 4 기본 서식 파일에는 이제 KnockoutJS, 풍부한 만들 수 있는 JavaScript MVVM 프레임 워크 및 JavaScript 및 HTML을 사용 하 여 응답성이 높은 웹 응용 프로그램 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-207">The ASP.NET MVC 4 default template now includes KnockoutJS, a JavaScript MVVM framework that lets you create rich and highly responsive web applications using JavaScript and HTML.</span></span> <span data-ttu-id="966f0-208">마찬가지로 mvc 3, jQuery 및 jQuery UI 라이브러리도 포함 되어 ASP.NET MVC 4입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-208">Like in MVC3, jQuery and jQuery UI libraries are also included in ASP.NET MVC 4.</span></span>

     > [!NOTE]
     > <span data-ttu-id="966f0-209">이 링크에 KnockOutJS 라이브러리에 대 한 자세한 정보를 얻을 수 있습니다: [ [ http://learn.knockoutjs.com/ ](http://learn.knockoutjs.com/) ](http://learn.knockoutjs.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-209">You can get more information about KnockOutJS library in this link: [[http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)](http://learn.knockoutjs.com/).</span></span> <span data-ttu-id="966f0-210">또한, jQuery 및 jQuery UI에 대해 알아볼 수 있습니다에 [ [ http://docs.jquery.com/ ](http://docs.jquery.com/) ](http://docs.jquery.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-210">Additionally, you can learn about jQuery and jQuery UI in [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/).</span></span>

<a id="Task_2_-_Exploring_the_Mobile_Application_Template"></a>
#### <a name="task-2---exploring-the-mobile-application-template"></a><span data-ttu-id="966f0-211">작업 2-탐색 모바일 응용 프로그램 템플릿</span><span class="sxs-lookup"><span data-stu-id="966f0-211">Task 2 - Exploring the Mobile Application Template</span></span>

<span data-ttu-id="966f0-212">ASP.NET MVC 4 모바일 앱을 위해 웹 사이트 및 태블릿 브라우저의 개발을 용이 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-212">ASP.NET MVC 4 facilitates the development of websites for mobile and tablet browsers.</span></span> <span data-ttu-id="966f0-213">이 템플릿은 인터넷 응용 프로그램 템플릿 (통지는 컨트롤러 코드가 거의 동일)와 동일한 응용 프로그램 구조를 갖지만 스타일은 터치 기반 모바일 장치에서 제대로 렌더링 하도록 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-213">This template has the same application structure as the Internet Application template (notice that the controller code is practically identical), but its style was modified to render properly in touch-based mobile devices.</span></span>

1. <span data-ttu-id="966f0-214">선택 된 **파일 | 새로 만들기 | 프로젝트** 메뉴 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-214">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="966f0-215">에 **새 프로젝트** 대화 상자에서 선택 된 **Visual C# | 웹** 서식 파일의 왼쪽된 창에서 트리를 선택 하 고는 **ASP.NET MVC 4 웹 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="966f0-215">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose the **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="966f0-216">프로젝트 이름을 **PhotoGallery.Mobile**, 위치를 선택 (또는 기본값을 그대로 적용) 선택 &quot;솔루션에 추가&quot; 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-216">Name the project **PhotoGallery.Mobile**, select a location (or leave the default), select &quot;Add to solution&quot; and click **OK**.</span></span>
2. <span data-ttu-id="966f0-217">에 **새 ASP.NET MVC 4 프로젝트** 대화 상자에서는 **모바일 응용 프로그램** 프로젝트 템플릿과 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-217">In the **New ASP.NET MVC 4 Project** dialog, select the **Mobile Application** project template and click **OK**.</span></span> <span data-ttu-id="966f0-218">Razor 뷰 엔진으로 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-218">Make sure you have selected Razor as the view engine.</span></span>

    <span data-ttu-id="966f0-219">![새 ASP.NET MVC 4 모바일 응용 프로그램을 만드는](whats-new-in-aspnet-mvc-4/_static/image11.png "새 ASP.NET MVC 4 모바일 응용 프로그램 만들기")</span><span class="sxs-lookup"><span data-stu-id="966f0-219">![Creating a new ASP.NET MVC 4 Mobile Application](whats-new-in-aspnet-mvc-4/_static/image11.png "Creating a new ASP.NET MVC 4 Mobile Application")</span></span>

    <span data-ttu-id="966f0-220">*새 ASP.NET MVC 4 모바일 응용 프로그램 만들기*</span><span class="sxs-lookup"><span data-stu-id="966f0-220">*Creating a new ASP.NET MVC 4 Mobile Application*</span></span>
3. <span data-ttu-id="966f0-221">이제 사용자는 솔루션을 탐색 하 고 체크 아웃 모바일용 ASP.NET MVC 4 솔루션 템플릿을 의해 도입 된 새로운 기능 중 일부를 수 있습니다:</span><span class="sxs-lookup"><span data-stu-id="966f0-221">Now you are able to explore the solution and check out some of the new features introduced by the ASP.NET MVC 4 solution template for mobile:</span></span>

    - <span data-ttu-id="966f0-222">**jQuery Mobile 라이브러리**</span><span class="sxs-lookup"><span data-stu-id="966f0-222">**jQuery Mobile Library**</span></span>

        <span data-ttu-id="966f0-223">모바일 응용 프로그램 프로젝트 템플릿을 있는 오픈 소스 라이브러리 모바일 브라우저 호환성을 위해 jQuery 모바일 라이브러리에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-223">The Mobile Application project template includes the jQuery Mobile library, which is an open source library for mobile browser compatibility.</span></span> <span data-ttu-id="966f0-224">jQuery Mobile CSS 및 JavaScript를 지 원하는 모바일 브라우저에 점진적인 기능 향상을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-224">jQuery Mobile applies progressive enhancement to mobile browsers that support CSS and JavaScript.</span></span> <span data-ttu-id="966f0-225">점진적인 기능 향상에 사용 하도록 콘텐츠를 표시 하는 경우 가장 강력한 브라우저가 설정 하는 동안 웹 페이지의 기본 콘텐츠를 표시 하려면 모든 브라우저 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-225">Progressive enhancement enables all browsers to display the basic content of a web page, while it only enables the most powerful browsers to display the rich content.</span></span> <span data-ttu-id="966f0-226">JQuery 모바일 스타일에에서 포함 된 JavaScript 및 CSS 파일, 페이지 태그에서 변경 하지 않고 화면에서 내용에 맞게 모바일 브라우저 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-226">The JavaScript and CSS files, included in the jQuery Mobile style, help mobile browsers to fit the content in the screen without making any change in the page markup.</span></span>

        ![jQuery-mobile-library-included-in-the-template](whats-new-in-aspnet-mvc-4/_static/image12.png)

        <span data-ttu-id="966f0-228">*서식 파일에 포함 된 jQuery 모바일 라이브러리*</span><span class="sxs-lookup"><span data-stu-id="966f0-228">*jQuery mobile library included in the template*</span></span>
    - <span data-ttu-id="966f0-229">**HTML5 기반 태그**</span><span class="sxs-lookup"><span data-stu-id="966f0-229">**HTML5 based markup**</span></span>

        ![Mobile-application-template-using-HTML5-markup](whats-new-in-aspnet-mvc-4/_static/image13.png)

        <span data-ttu-id="966f0-231">*HTML5 태그, (Login.cshtml 및 index.cshtml)를 사용 하 여 모바일 응용 프로그램 템플릿*</span><span class="sxs-lookup"><span data-stu-id="966f0-231">*Mobile application template using HTML5 markup, (Login.cshtml and index.cshtml)*</span></span>
4. <span data-ttu-id="966f0-232">키를 눌러 **F5** 솔루션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-232">Press **F5** to run the solution.</span></span>
5. <span data-ttu-id="966f0-233">열기는 **Windows Phone 7 에뮬레이터**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-233">Open the **Windows Phone 7 Emulator**.</span></span>
6. <span data-ttu-id="966f0-234">Phone 시작 화면에서 Internet Explorer를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-234">In the phone start screen, open Internet Explorer.</span></span> <span data-ttu-id="966f0-235">데스크톱 응용 프로그램의 시작 위치 URL을 확인 하 고 전화를 통해 해당 URL로 이동 (예: `http://localhost:[PortNumber]/`).</span><span class="sxs-lookup"><span data-stu-id="966f0-235">Check out the URL where the desktop application started and browse to that URL from the phone (e.g. `http://localhost:[PortNumber]/`).</span></span>
7. <span data-ttu-id="966f0-236">로그인 페이지를 입력 하거나 체크 아웃할 수 이제는 페이지에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-236">Now you are able to enter the login page or check out the about page.</span></span> <span data-ttu-id="966f0-237">웹 사이트의 스타일은 모바일 앱을 위해 새 Metro 응용 프로그램에 따라 있는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-237">Notice that the style of the website is based on the new Metro app for mobile.</span></span> <span data-ttu-id="966f0-238">ASP.NET MVC 4 프로젝트 템플릿은 모든 페이지의 요소가 표시 되 고 사용할 수 있도록 하는 모바일 장치에 올바르게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-238">The ASP.NET MVC 4 project template is correctly displayed on mobile devices, making sure all the elements of the page are visible and enabled.</span></span> <span data-ttu-id="966f0-239">헤더에 대 한 링크를 클릭 하거나 누를 충분히 큰 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-239">Notice that the links on the header are big enough to be clicked or tapped.</span></span>

    <span data-ttu-id="966f0-240">![모바일 장치에서 서식 파일 페이지 프로젝트](whats-new-in-aspnet-mvc-4/_static/image14.png "서식 파일 페이지에서 모바일 장치 프로젝트")</span><span class="sxs-lookup"><span data-stu-id="966f0-240">![Project template pages in a mobile device](whats-new-in-aspnet-mvc-4/_static/image14.png "Project template pages in a mobile device")</span></span>

    <span data-ttu-id="966f0-241">*모바일 장치에서 프로젝트 템플릿 페이지*</span><span class="sxs-lookup"><span data-stu-id="966f0-241">*Project template pages in a mobile device*</span></span>
8. <span data-ttu-id="966f0-242">새 템플릿을 사용 하 여도 **뷰포트 메타 태그**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-242">The new template also uses the **Viewport meta tag**.</span></span> <span data-ttu-id="966f0-243">대부분의 모바일 브라우저 가상 브라우저 창에 대 한 너비를 정의 하거나 &quot;뷰포트&quot;, 모바일 장치에서의 실제 너비 보다 큰 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-243">Most mobile browsers define a width for a virtual browser window or &quot;viewport&quot;, which is larger than the actual width of the mobile device.</span></span> <span data-ttu-id="966f0-244">이 통해 모바일 브라우저 가상 디스플레이로 내 전체 웹 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-244">This enables mobile browsers to display the entire web page inside the virtual display.</span></span> <span data-ttu-id="966f0-245">**뷰포트 메타 태그** 웹 개발자가 모바일 장치에 너비, 높이 및 브라우저 영역 사이의 값을 설정할 수 있도록 **합니다.**</span><span class="sxs-lookup"><span data-stu-id="966f0-245">The **Viewport meta tag** allows web developers to set the width, height and scale of the browser area on mobile devices **.**</span></span> <span data-ttu-id="966f0-246">장치 너비에 뷰포트를 설정 하는 모바일 응용 프로그램에 대 한 ASP.NET MVC 4 템플릿 (&quot;너비 장치 너비 =&quot;) 레이아웃 템플릿에 (*Views\Shared\_Layout.cshtml*) 되도록 모든는 페이지의 뷰포트 장치 화면 너비를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-246">The ASP.NET MVC 4 template for Mobile Applications sets the viewport to the device width (&quot;width=device-width&quot;) in the layout template (*Views\Shared\_Layout.cshtml*), so that all the pages will have their viewport set to the device screen width.</span></span> <span data-ttu-id="966f0-247">뷰포트 메타 태그에서 기본 브라우저 보기를 변경 하지 않는다는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-247">Notice that the Viewport meta tag will not change the default browser view.</span></span>
9. <span data-ttu-id="966f0-248">열기  **\_Layout.cshtml**에 있는 **보기 | 공유** 폴더 및 주석 뷰포트 메타 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-248">Open **\_Layout.cshtml**, located in the **Views | Shared** folder, and comment the Viewport meta tag.</span></span> <span data-ttu-id="966f0-249">응용 프로그램을 실행 하지 않은 경우 이미 열리고 차이 확인해 보세요.</span><span class="sxs-lookup"><span data-stu-id="966f0-249">Run the application, if not already opened, and check out the differences.</span></span>


~~~
[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample2.cshtml)]

![The site after commenting the viewport meta tag](whats-new-in-aspnet-mvc-4/_static/image15.png "The site after commenting the viewport meta tag")

*The site after commenting the viewport meta tag*
~~~
10. <span data-ttu-id="966f0-250">키를 눌러 Visual Studio에서 **SHIFT** + **F5** 응용 프로그램 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-250">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
11. <span data-ttu-id="966f0-251">뷰포트 메타 태그 주석 처리를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-251">Uncomment the viewport meta tag.</span></span>


~~~
[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample3.cshtml)]
~~~

<a id="Task_3_-_Using_Adaptive_Rendering"></a>
#### <a name="task-3---using-adaptive-rendering"></a><span data-ttu-id="966f0-252">작업 3-자동 선택 렌더링을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="966f0-252">Task 3 - Using Adaptive Rendering</span></span>

<span data-ttu-id="966f0-253">이 태스크에서는 사용자 지정 하지 않고 동시에 올바르게 모바일 장치 및 웹 브라우저에서 웹 페이지를 렌더링 하는 다른 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-253">In this task, you will learn another method to render a Web page correctly on mobile devices and Web browsers at the same time without any customization.</span></span> <span data-ttu-id="966f0-254">유사한 용도의 뷰포트 메타 태그를 이미 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-254">You have already used Viewport meta tag with a similar purpose.</span></span> <span data-ttu-id="966f0-255">다른 강력한 방법을 부합 하는 이제: *자동 선택 렌더링*합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-255">Now you will meet another powerful method: *adaptive rendering*.</span></span>

<span data-ttu-id="966f0-256">자동 선택 렌더링은 사용 하는 기술 **CSS3 미디어 쿼리** 페이지에 적용 되는 스타일을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-256">Adaptive rendering is a technique that uses **CSS3 media queries** to customize the style applied to a page.</span></span> <span data-ttu-id="966f0-257">미디어 쿼리 조건 내 특정 조건에서 CSS 스타일을 그룹화 하 여 스타일 시트를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-257">Media queries define conditions inside a style sheet, grouping CSS styles under a certain condition.</span></span> <span data-ttu-id="966f0-258">조건이 true 이면 하는 경우에 스타일 선언 된 개체에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-258">Only when the condition is true, the style is applied to the declared objects.</span></span>

<span data-ttu-id="966f0-259">자동 선택 렌더링 방법에서 제공 하는 유연성에 서로 다른 장치에서 사이트를 표시 하기 위한 모든 사용자 지정 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-259">The flexibility provided by the adaptive rendering technique enables any customization for displaying the site on different devices.</span></span> <span data-ttu-id="966f0-260">원하는 만큼 하나의 스타일 시트에서 논리 코드를 작성 하지 않고 스타일을 선택할 수 만큼 스타일을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-260">You can define as many styles as you want on a single style sheet without writing logic code to choose the style.</span></span> <span data-ttu-id="966f0-261">따라서 중복 된 코드와 목적으로 렌더링 하기 위한 논리의 양이 줄어 대로 페이지 스타일 적용의 매우 유용한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-261">Therefore, it is a very neat way of adapting page styles, as it reduces the amount of duplicated code and logic for rendering purposes.</span></span> <span data-ttu-id="966f0-262">반면에 대역폭 소비 늘어나기, CSS 파일의 크기 미미 늘어나면 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-262">On the other hand, bandwidth consumption would increase, as the size of your CSS files could grow marginally.</span></span>

<span data-ttu-id="966f0-263">자동 선택 렌더링 기술을 사용 하 여 해당 사이트 수 **브라우저와 상관 없이 적절 하 게 표시 합니다.**</span><span class="sxs-lookup"><span data-stu-id="966f0-263">By using the adaptive rendering technique, your site will be **displayed properly, regardless of the browser.**</span></span> <span data-ttu-id="966f0-264">하지만 추가 대역폭 로드 되는 문제를 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-264">However, you should consider if the bandwidth extra load is a concern.</span></span>

> [!NOTE]
> <span data-ttu-id="966f0-265">미디어 쿼리의 기본 형식은: @media \[범위: 모든 | 핸드헬드 | 인쇄 | 프로젝션 | 화면\] ([속성: 값] 및... [속성: 값])</span><span class="sxs-lookup"><span data-stu-id="966f0-265">The basic format of a media query is: @media \[Scope: all | handheld | print | projection | screen\] ([property:value] and ... [property:value])</span></span>


<span data-ttu-id="966f0-266">미디어 쿼리 예제: &gt;  <strong>@media 모든 및 (최대 너비: 1000px) 및 (최소 너비: 700px) {}:</strong> 700px 1000px 사이의 모든 해상도 대해 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-266">Examples of media queries: &gt;<strong>@media all and (max-width: 1000px) and (min-width: 700px) {}:</strong> For all the resolutions between 700px and 1000px.</span></span>

> <span data-ttu-id="966f0-267"><strong>@media 화면 및 (최소 너비: 400px) 및 (최대 너비: 700px) {...}:</strong> 화면에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-267"><strong>@media screen and (min-width: 400px) and (max-width: 700px) { ... }:</strong> Only for screens.</span></span> <span data-ttu-id="966f0-268">해상도 400에서 700px 사이 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-268">The resolution must be between 400 and 700px.</span></span>
> 
> <span data-ttu-id="966f0-269"><strong>@media 핸드헬드 장치 및 (최소 너비: 20em), 화면 및 (최소 너비: 20em) {...}:</strong> (모바일 및 장치) 휴대 장치 및 화면에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-269"><strong>@media handheld and (min-width: 20em), screen and (min-width: 20em) { ... }:</strong> For handhelds(mobile and devices) and screens.</span></span> <span data-ttu-id="966f0-270">최소 너비 20em 보다 커야 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-270">The minimum width must be greater than 20em.</span></span>
> 
> <span data-ttu-id="966f0-271">이 대 한 자세한 정보를 찾을 수 있습니다는 [W3C 사이트](http://www.w3.org/TR/css3-mediaqueries/)합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-271">You can find more information about this on the [W3C site](http://www.w3.org/TR/css3-mediaqueries/).</span></span>


<span data-ttu-id="966f0-272">이제 자동 선택 렌더링의 작동 원리를 탐색, 4는 웹 사이트 템플릿을 기본 ASP.NET MVC의 가독성을 향상 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-272">You will now explore how the adaptive rendering works, improving the readability of the ASP.NET MVC 4 default website template.</span></span>

1. <span data-ttu-id="966f0-273">열기는 **PhotoGallery.sln** 솔루션 작업 1에서 만든 하 고 선택 된 **PhotoGallery** 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="966f0-273">Open the **PhotoGallery.sln** solution you have created at Task 1 and select the **PhotoGallery** project.</span></span> <span data-ttu-id="966f0-274">키를 눌러 **F5** 솔루션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-274">Press **F5** to run the solution.</span></span>
2. <span data-ttu-id="966f0-275">브라우저의 너비 절반 또는 원래 크기의 1/4 보다 작은 창을 설정의 크기를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-275">Resize the browser's width, setting the windows to half or to less than a quarter of its original size.</span></span> <span data-ttu-id="966f0-276">이 어떻게 바뀌는지 헤더의 항목과: 일부 요소 헤더의 표시 영역에 나타나지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-276">Notice what happens with the items in the header: Some elements will not appear in the visible area of the header.</span></span>
3. <span data-ttu-id="966f0-277">열기 <strong>Site.css</strong> 파일에 있는 Visual Studio 솔루션 탐색기에서 <strong>콘텐츠</strong> 프로젝트 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-277">Open <strong>Site.css</strong> file from the Visual Studio Solution explorer, located in <strong>Content</strong> project folder.</span></span> <span data-ttu-id="966f0-278">키를 눌러 <strong>CTRL + F</strong> Visual Studio 통합된 검색을 열고 쓸 <strong>@media</strong> 찾으려고는 <strong>CSS 미디어 쿼리</strong>합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-278">Press <strong>CTRL + F</strong> to open Visual Studio integrated search, and write <strong>@media</strong> to locate the <strong>CSS media query</strong>.</span></span>

    <span data-ttu-id="966f0-279">이 서식 파일에 정의 된 경우 미디어 쿼리 조건이이 방식으로 작동: 브라우저의 창 크기 미만인 **850 px**를 위해 CSS 규칙이 적용 되는이 미디어 블록 내에 정의 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-279">The media query condition defined in this template works in this way: When the browser's window size is below **850 px**, the CSS rules applied are the ones defined inside this media block.</span></span>

    <span data-ttu-id="966f0-280">![미디어 쿼리 찾기](whats-new-in-aspnet-mvc-4/_static/image16.png "미디어 쿼리 찾기")</span><span class="sxs-lookup"><span data-stu-id="966f0-280">![Locating the media query](whats-new-in-aspnet-mvc-4/_static/image16.png "Locating the media query")</span></span>

    <span data-ttu-id="966f0-281">*미디어 쿼리 찾기*</span><span class="sxs-lookup"><span data-stu-id="966f0-281">*Locating the media query*</span></span>
4. <span data-ttu-id="966f0-282">850에 설정 된 최대 너비 특성 값을 대체와 px **10px**자동 선택 렌더링을 사용 하지 않도록 설정 하려면 한 키를 누릅니다 **CTRL + S** 여 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-282">Replace the max-width attribute value set in 850 px with **10px**, in order to disable the adaptive rendering, and press **CTRL + S** to save the changes.</span></span> <span data-ttu-id="966f0-283">브라우저와 키를 눌러 돌아갑니다 **CTRL + f 5를 눌러** 변경 내용을 사용 하 여 페이지를 새로 고칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-283">Return to the browser and press **CTRL + F5** to refresh the page with the changes you have made.</span></span> <span data-ttu-id="966f0-284">창의 너비를 조정할 때 두 페이지에서 차이 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-284">Notice the differences in both pages when adjusting the width of the window.</span></span>

    <span data-ttu-id="966f0-285">![페이지 왼쪽에 적용 하는 @media 스타일 오른쪽에 스타일을 생략 하면](whats-new-in-aspnet-mvc-4/_static/image17.png "페이지 왼쪽에 적용 하는 @media 스타일을 스타일 오른쪽에서을 생략 하면")</span><span class="sxs-lookup"><span data-stu-id="966f0-285">![In the left, the page is applying the @media style, in the right, the style is omitted](whats-new-in-aspnet-mvc-4/_static/image17.png "In the left, the page is applying the @media style, in the right, the style is omitted")</span></span>

    <span data-ttu-id="966f0-286"><em>페이지 왼쪽에 적용 하는 @media 스타일을 스타일 오른쪽에서을 생략 하면</em></span><span class="sxs-lookup"><span data-stu-id="966f0-286"><em>In the left, the page is applying the @media style, in the right, the style is omitted</em></span></span>

    <span data-ttu-id="966f0-287">이제 모바일 장치에서 어떤 일이 생기 확인해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-287">Now, let's check out what happens on mobile devices:</span></span>

    <span data-ttu-id="966f0-288">![페이지 왼쪽에 적용 하는 @media 스타일 오른쪽에 스타일을 생략 하면](whats-new-in-aspnet-mvc-4/_static/image18.png "페이지 왼쪽에 적용 하는 @media 스타일을 스타일 오른쪽에서을 생략 하면")</span><span class="sxs-lookup"><span data-stu-id="966f0-288">![In the left, the page is applying the @media style, in the right, the style is omitted](whats-new-in-aspnet-mvc-4/_static/image18.png "In the left, the page is applying the @media style, in the right, the style is omitted")</span></span>

    <span data-ttu-id="966f0-289"><em>페이지 왼쪽에 적용 하는 @media 스타일을 스타일 오른쪽에서을 생략 하면</em></span><span class="sxs-lookup"><span data-stu-id="966f0-289"><em>In the left, the page is applying the @media style, in the right, the style is omitted</em></span></span>

    <span data-ttu-id="966f0-290">모바일 장치를 사용 하는 경우 페이지는 웹 브라우저에서 렌더링 될 때 변경 내용을 매우 중요 한 없는지 확인할 수 있지만 차이점 더욱 명확 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-290">Although you will notice that the changes when the page is rendered in a Web browser are not very significant, when using a mobile device the differences become more obvious.</span></span> <span data-ttu-id="966f0-291">이미지의 왼쪽에 사용자 지정 스타일 가독성 향상 되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-291">On the left side of the image, we can see that the custom style improved the readability.</span></span>

    <span data-ttu-id="966f0-292">자동 선택 렌더링에 쉽게 조건부 웹 사이트에 스타일을 지정 하 고는 깔끔한 접근 방식으로 일반 스타일 문제를 해결 하기 위해 적용 하 여 더 많은 시나리오를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-292">Adaptive rendering can be used in many more scenarios, making it easier to apply conditional styling to a Web site and solving common style issues with a neat approach.</span></span>

    <span data-ttu-id="966f0-293">뷰포트 메타 태그 및 CSS 미디어 쿼리 ASP.NET MVC 4에 한정 되지 않는 모든 웹 응용 프로그램에서 이러한 기능을 활용 될 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-293">The Viewport meta tag and CSS media queries are not specific to ASP.NET MVC 4, so you can take advantage of these features in any web application.</span></span>
5. <span data-ttu-id="966f0-294">키를 눌러 Visual Studio에서 **SHIFT** + **F5** 응용 프로그램 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-294">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_the_Photo_Gallery_Web_Application"></a>
### <a name="exercise-2-creating-the-photo-gallery-web-application"></a><span data-ttu-id="966f0-295">연습 2: 사진 갤러리 웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="966f0-295">Exercise 2: Creating the Photo Gallery Web Application</span></span>

<span data-ttu-id="966f0-296">이 연습에서는 사진을 표시 하는 사진 갤러리 응용 프로그램에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-296">In this exercise, you will work on a Photo Gallery application to display photos.</span></span> <span data-ttu-id="966f0-297">ASP.NET MVC 4 프로젝트 템플릿을 사용 하 여 먼저 및 서비스에서 사진을 검색 하 고 홈 페이지에 표시 하는 기능에서 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-297">You will start with the ASP.NET MVC 4 project template, and then you will add a feature to retrieve photos from a service and display them in the home page.</span></span>

<span data-ttu-id="966f0-298">다음 연습에서는 모바일 장치에 표시 되는 방식을 강화 하기 위해이 솔루션을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-298">In the following exercise, you will update this solution to enhance the way it is displayed on mobile devices.</span></span>

<a id="Task_1_-_Creating_a_Mock_Photo_Service"></a>
#### <a name="task-1---creating-a-mock-photo-service"></a><span data-ttu-id="966f0-299">작업 1-모의 사진 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="966f0-299">Task 1 - Creating a Mock Photo Service</span></span>

<span data-ttu-id="966f0-300">이 태스크에서는 갤러리에 표시 되는 콘텐츠를 검색 하는 사진 서비스의 모의 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-300">In this task, you will create a mock of the photo service to retrieve the content that will be displayed in the gallery.</span></span> <span data-ttu-id="966f0-301">이렇게 하려면 단순히 각 사진 데이터와 함께 JSON 파일을 반환 하는 새로운 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-301">To do this, you will add a new controller that will simply return a JSON file with the data of each photo.</span></span>

1. <span data-ttu-id="966f0-302">열기 **Visual Studio** 열려 있지 않으면입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-302">Open **Visual Studio** if not already opened.</span></span>
2. <span data-ttu-id="966f0-303">선택 된 **파일 | 새로 만들기 | 프로젝트** 메뉴 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-303">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="966f0-304">에 **새 프로젝트** 대화 상자에서 선택 된 **Visual C# | 웹** 서식 파일의 왼쪽된 창에서 선택한 트리의 **ASP.NET MVC 4 웹 응용 프로그램입니다.**</span><span class="sxs-lookup"><span data-stu-id="966f0-304">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="966f0-305">프로젝트 이름을 **PhotoGallery**, 위치를 선택 (또는 기본값을 그대로 적용)를 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-305">Name the project **PhotoGallery**, select a location (or leave the default) and click **OK**.</span></span> <span data-ttu-id="966f0-306">기존 ASP.NET MVC 4 프로그램에서 작업을 계속할 수 또는 **인터넷 응용 프로그램** 솔루션에서 **연습 1** 하 고 다음 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-306">Alternatively, you can continue working from your existing ASP.NET MVC 4 **Internet Application** solution from **Exercise 1** and skip the next step.</span></span>
3. <span data-ttu-id="966f0-307">에 **새 ASP.NET MVC 4 프로젝트** 대화 상자는 **인터넷 응용 프로그램** 프로젝트 템플릿과 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-307">In the **New ASP.NET MVC 4 Project** dialog box, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="966f0-308">Razor 뷰 엔진으로 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-308">Make sure you have Razor selected as the View Engine.</span></span>
4. <span data-ttu-id="966f0-309">에 **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **앱\_데이터** 프로젝트 및 선택의 폴더 **추가 | 기존 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-309">In the **Solution Explorer**, right-click the **App\_Data** folder of your project, and select **Add | Existing Item**.</span></span> <span data-ttu-id="966f0-310">찾아는 **Source\Assets\App\_데이터** 이 랩의 폴더를 추가 하 고는 **Photos.json** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-310">Browse to the **Source\Assets\App\_Data** folder of this lab and add the **Photos.json** file.</span></span>
5. <span data-ttu-id="966f0-311">만들 새 컨트롤러 이름의 **PhotoController**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-311">Create a new controller with the name **PhotoController**.</span></span> <span data-ttu-id="966f0-312">이렇게 하려면 마우스 오른쪽 단추로 클릭는 **컨트롤러** 폴더를 이동 **추가** 선택 **컨트롤러입니다.**</span><span class="sxs-lookup"><span data-stu-id="966f0-312">To do this, right-click on the **Controllers** folder, go to **Add** and select **Controller.**</span></span> <span data-ttu-id="966f0-313">컨트롤러 이름을 작성, 둡니다는 **빈 MVC 컨트롤러** 템플릿을 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-313">Complete the controller name, leave the **Empty MVC controller** template and click **Add**.</span></span>

    <span data-ttu-id="966f0-314">![추가 PhotoController](whats-new-in-aspnet-mvc-4/_static/image19.png "는 PhotoController 추가")</span><span class="sxs-lookup"><span data-stu-id="966f0-314">![Adding the PhotoController](whats-new-in-aspnet-mvc-4/_static/image19.png "Adding the PhotoController")</span></span>

    <span data-ttu-id="966f0-315">*PhotoController 추가*</span><span class="sxs-lookup"><span data-stu-id="966f0-315">*Adding the PhotoController*</span></span>
6. <span data-ttu-id="966f0-316">대체는 **인덱스** 메서드를 다음 **갤러리** 작업 및 최근에 프로젝트에 추가한 JSON 파일에서 콘텐츠를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-316">Replace the **Index** method with the following **Gallery** action, and return the content from the JSON file you have recently added to the project.</span></span>

    <span data-ttu-id="966f0-317">(코드 조각- *ASP.NET MVC 4-Ex02-랩 갤러리 실행*)</span><span class="sxs-lookup"><span data-stu-id="966f0-317">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Gallery Action*)</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample4.cs)]
~~~
7. <span data-ttu-id="966f0-318">키를 눌러 **F5** 솔루션을 실행 하 여 다음 모의 사진 서비스를 테스트 하려면 다음 URL로 이동: `http://localhost:[port]/photo/gallery` ([port] 값 응용 프로그램이 시작 된 현재 포트에 따라 다름).</span><span class="sxs-lookup"><span data-stu-id="966f0-318">Press **F5** to run the solution, and then browse to the following URL in order to test the mocked photo service: `http://localhost:[port]/photo/gallery` (the [port] value depends on the current port where the application was launched).</span></span> <span data-ttu-id="966f0-319">이 URL로 요청 콘텐츠를 검색 해야는 **Photos.json** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-319">The request to this URL should retrieve the content of the **Photos.json** file.</span></span>

    <span data-ttu-id="966f0-320">![모의 사진 서비스 테스트](whats-new-in-aspnet-mvc-4/_static/image20.png "모의 사진 서비스 테스트")</span><span class="sxs-lookup"><span data-stu-id="966f0-320">![Testing the mocked photo service](whats-new-in-aspnet-mvc-4/_static/image20.png "Testing the mocked photo service")</span></span>

    <span data-ttu-id="966f0-321">*모의 사진 서비스 테스트*</span><span class="sxs-lookup"><span data-stu-id="966f0-321">*Testing the mocked photo service*</span></span>

<span data-ttu-id="966f0-322">실제 구현에서 사용할 수 있습니다 [ASP.NET Web API](../../../../web-api/index.md) 사진 갤러리 서비스를 구현 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-322">In a real implementation you could use [ASP.NET Web API](../../../../web-api/index.md) to implement the Photo Gallery service.</span></span> <span data-ttu-id="966f0-323">ASP.NET Web API는 다양 한 브라우저 및 모바일 장치를 포함 한 클라이언트를 연결할 HTTP 서비스를 작성을 용이 하 게 하는 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-323">ASP.NET Web API is a framework that makes it easy to build HTTP services that reach a broad range of clients, including browsers and mobile devices.</span></span> <span data-ttu-id="966f0-324">ASP.NET Web API는 .NET Framework에서 RESTful 응용 프로그램을 빌드하는 데 이상적인 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-324">ASP.NET Web API is an ideal platform for building RESTful applications on the .NET Framework.</span></span>

<a id="Task_2_-_Displaying_the_Photo_Gallery"></a>
#### <a name="task-2---displaying-the-photo-gallery"></a><span data-ttu-id="966f0-325">작업 2-사진 갤러리를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-325">Task 2 - Displaying the Photo Gallery</span></span>

<span data-ttu-id="966f0-326">이 작업에서는이 작업의 첫 번째 작업에서 만든 모의 서비스를 사용 하 여 사진 갤러리를 표시 하려면 홈 페이지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-326">In this task, you will update the Home page to show the photo gallery by using the mocked service you created in the first task of this exercise.</span></span> <span data-ttu-id="966f0-327">모델 파일을 추가 하 고 갤러리 보기를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-327">You will add model files and update the gallery views.</span></span>

1. <span data-ttu-id="966f0-328">키를 눌러 Visual Studio에서 **SHIFT** + **F5** 응용 프로그램 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-328">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
2. <span data-ttu-id="966f0-329">만들기는 **사진** 클래스에 **모델** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-329">Create the **Photo** class in the **Models** folder.</span></span> <span data-ttu-id="966f0-330">이렇게 하려면 마우스 오른쪽 단추로 클릭는 **모델** 폴더를 **추가** 클릭 **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-330">To do this, right-click on the **Models** folder, select **Add** and click **Class**.</span></span> <span data-ttu-id="966f0-331">그런 다음 이름으로 설정할 **Photo.cs** 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-331">Then, set the name to **Photo.cs** and click **Add**.</span></span>
3. <span data-ttu-id="966f0-332">다음 멤버를 추가할는 **사진** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-332">Add the following members to the **Photo** class.</span></span>

    <span data-ttu-id="966f0-333">(코드 조각- *ASP.NET MVC 4 랩-Ex02-사진 모델*)</span><span class="sxs-lookup"><span data-stu-id="966f0-333">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Photo model*)</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample5.cs)]
~~~
4. <span data-ttu-id="966f0-334">**컨트롤러** 폴더에서 **HomeController.cs** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-334">Open the **HomeController.cs** file from the **Controllers** folder.</span></span>
5. <span data-ttu-id="966f0-335">다음 using 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-335">Add the following using statements.</span></span>

    <span data-ttu-id="966f0-336">(코드 조각- *ASP.NET MVC 4-Ex02-랩 HomeController Using*)</span><span class="sxs-lookup"><span data-stu-id="966f0-336">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - HomeController Usings*)</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample6.cs)]
~~~
6. <span data-ttu-id="966f0-337">업데이트는 **인덱스** 동작을 사용 하 여 **HttpClient** 갤러리 데이터 검색을 사용 하 여는 **JavaScriptSerializer** 뷰 모델을 deserialize 하는 데 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-337">Update the **Index** action to use **HttpClient** to retrieve the gallery data, and then use the **JavaScriptSerializer** to deserialize it to the view model.</span></span>

    <span data-ttu-id="966f0-338">(코드 조각- *ASP.NET MVC 4-Ex02-랩 인덱스 동작*)</span><span class="sxs-lookup"><span data-stu-id="966f0-338">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Index Action*)</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample7.cs)]
~~~
7. <span data-ttu-id="966f0-339">열기는 **Index.cshtml** 아래에 있는 파일의 **Views\Home** 폴더 및 모든 콘텐츠를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-339">Open the **Index.cshtml** file located under the **Views\Home** folder and replace all the content with the following code.</span></span>

    <span data-ttu-id="966f0-340">이 코드는 서비스에서 검색 된 모든 사진 하는 순서가 지정 되지 않은 목록으로 표시입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-340">This code loops through all the photos retrieved from the service and displays them into an unordered list.</span></span>

    <span data-ttu-id="966f0-341">(코드 조각- *ASP.NET MVC 4-Ex02-랩 사진 목록*)</span><span class="sxs-lookup"><span data-stu-id="966f0-341">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Photo List*)</span></span>


~~~
[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample8.cshtml)]
~~~
8. <span data-ttu-id="966f0-342">에 **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **콘텐츠** 프로젝트 및 선택의 폴더 **추가 | 기존 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-342">In the **Solution Explorer**, right-click the **Content** folder of your project, and select **Add | Existing Item**.</span></span> <span data-ttu-id="966f0-343">찾아는 **Source\Assets\Content** 이 랩의 폴더를 추가 하 고는 **Site.css** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-343">Browse to the **Source\Assets\Content** folder of this lab and add the **Site.css** file.</span></span> <span data-ttu-id="966f0-344">대체를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-344">You will have to confirm its replacement.</span></span> <span data-ttu-id="966f0-345">있는 경우는 **Site.css** 파일을 열 수, 파일을 다시 로드할지도 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-345">If you have the **Site.css** file open, you will have to confirm to reload the file also.</span></span>
9. <span data-ttu-id="966f0-346">파일 탐색기를 열고 전체를 복사 **사진** 폴더 아래에 **Source\Assets** 솔루션 탐색기에서 프로젝트의 루트 폴더에이 랩의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-346">Open File Explorer and copy the entire **Photos** folder located under the **Source\Assets** folder of this lab to the root folder of your project in Solution Explorer.</span></span>
10. <span data-ttu-id="966f0-347">응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-347">Run the application.</span></span> <span data-ttu-id="966f0-348">이제 갤러리에는 사진 표시 홈 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-348">You should now see the home page displaying the photos in the gallery.</span></span>

    <span data-ttu-id="966f0-349">![사진 갤러리](whats-new-in-aspnet-mvc-4/_static/image21.png "사진 갤러리")</span><span class="sxs-lookup"><span data-stu-id="966f0-349">![Photo Gallery](whats-new-in-aspnet-mvc-4/_static/image21.png "Photo Gallery")</span></span>

    <span data-ttu-id="966f0-350">*사진 갤러리*</span><span class="sxs-lookup"><span data-stu-id="966f0-350">*Photo Gallery*</span></span>
11. <span data-ttu-id="966f0-351">키를 눌러 Visual Studio에서 **SHIFT** + **F5** 응용 프로그램 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-351">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Adding_support_for_mobile_devices"></a>
### <a name="exercise-3-adding-support-for-mobile-devices"></a><span data-ttu-id="966f0-352">연습 3: 모바일 장치에 대 한 지원 추가</span><span class="sxs-lookup"><span data-stu-id="966f0-352">Exercise 3: Adding support for mobile devices</span></span>

<span data-ttu-id="966f0-353">ASP.NET MVC 4에서 키 업데이트 중 하나에 모바일 개발에 대 한 지원입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-353">One of the key updates in ASP.NET MVC 4 is the support for mobile development.</span></span> <span data-ttu-id="966f0-354">이 연습에서는, 이전 연습에서 만든 PhotoGallery 솔루션을 확장 하 여 ASP.NET MVC 4 모바일 응용 프로그램에 대 한 새로운 기능을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-354">In this exercise, you will explore ASP.NET MVC 4 new features for mobile applications by extending the PhotoGallery solution you have created in the previous exercise.</span></span>

<a id="Task_1_-_Installing_jQuery_Mobile_in_an_ASPNET_MVC_4_Application"></a>
#### <a name="task-1---installing-jquery-mobile-in-an-aspnet-mvc-4-application"></a><span data-ttu-id="966f0-355">작업 1-ASP.NET MVC 4 응용 프로그램에서 jQuery Mobile 설치</span><span class="sxs-lookup"><span data-stu-id="966f0-355">Task 1 - Installing jQuery Mobile in an ASP.NET MVC 4 Application</span></span>

1. <span data-ttu-id="966f0-356">열기는 **시작** 솔루션에 있는 **소스/Ex3-MobileSupport/시작/** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-356">Open the **Begin** solution located at **Source/Ex3-MobileSupport/Begin/** folder.</span></span> <span data-ttu-id="966f0-357">그렇지 않은 경우 계속 사용할 수도 있습니다는 **끝** 솔루션, 이전 연습을 완료 하 여 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-357">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="966f0-358">제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면.</span><span class="sxs-lookup"><span data-stu-id="966f0-358">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="966f0-359">이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-359">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="966f0-360">에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="966f0-360">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="966f0-361">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-361">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="966f0-362">NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-362">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="966f0-363">NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-363">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="966f0-364">이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-364">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="966f0-365">열기는 **패키지 관리자 콘솔** 클릭 하 여는 **도구** &gt; **라이브러리 패키지 관리자** &gt; **패키지 관리자 콘솔** 메뉴 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-365">Open the **Package Manager Console** by clicking the **Tools** &gt; **Library Package Manager** &gt; **Package Manager Console** menu option.</span></span>

    <span data-ttu-id="966f0-366">![NuGet 패키지 관리자 콘솔을 열고](whats-new-in-aspnet-mvc-4/_static/image22.png "NuGet 패키지 관리자 콘솔을 열고")</span><span class="sxs-lookup"><span data-stu-id="966f0-366">![Opening the NuGet Package Manager Console](whats-new-in-aspnet-mvc-4/_static/image22.png "Opening the NuGet Package Manager Console")</span></span>

    <span data-ttu-id="966f0-367">*NuGet 패키지 관리자 콘솔 열기*</span><span class="sxs-lookup"><span data-stu-id="966f0-367">*Opening the NuGet Package Manager Console*</span></span>
3. <span data-ttu-id="966f0-368">패키지 관리자 콘솔에서 설치 하려면 다음 명령을 실행 하는 **jQuery.Mobile.MVC** 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-368">In the Package Manager Console run the following command to install the **jQuery.Mobile.MVC** package.</span></span>

    <span data-ttu-id="966f0-369">jQuery Mobile은 터치에 최적화 된 웹 UI를 작성 하기 위한 오픈 소스 라이브러리.</span><span class="sxs-lookup"><span data-stu-id="966f0-369">jQuery Mobile is an open source library for building touch-optimized web UI.</span></span> <span data-ttu-id="966f0-370">JQuery Mobile ASP.NET MVC 4 응용 프로그램을 사용 하는 도우미 jQuery.Mobile.MVC NuGet 패키지에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-370">The jQuery.Mobile.MVC NuGet package includes helpers to use jQuery Mobile with an ASP.NET MVC 4 application.</span></span>

    > [!NOTE]
    > <span data-ttu-id="966f0-371">다음 명령은 실행 하 여 있습니다 됩니다 수 jQuery.Mobile.MVC 라이브러리에서에서 다운로드 Nuget 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-371">By running the following command, you will be downloading the jQuery.Mobile.MVC library from Nuget.</span></span>

    <span data-ttu-id="966f0-372">PM</span><span class="sxs-lookup"><span data-stu-id="966f0-372">PM</span></span>

    [!code-powershell[Main](whats-new-in-aspnet-mvc-4/samples/sample9.ps1)]

    <span data-ttu-id="966f0-373">이 명령은 jQuery Mobile 및 다음을 비롯 한 일부 도우미 파일을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-373">This command installs jQuery Mobile and some helper files, including the following:</span></span>

    - <span data-ttu-id="966f0-374">**뷰/공유/\_Layout.Mobile.cshtml**: jQuery Mobile 기반 레이아웃을 더 작은 화면에 맞게 최적화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-374">**Views/Shared/\_Layout.Mobile.cshtml**: is a jQuery Mobile-based layout optimized for a smaller screen.</span></span> <span data-ttu-id="966f0-375">웹 사이트의 모바일 브라우저에서 요청을 받으면 원래 레이아웃 바뀝니다 (\_Layout.cshtml)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-375">When the website receives a request from a mobile browser, it will replace the original layout (\_Layout.cshtml) with this one.</span></span>
    - <span data-ttu-id="966f0-376">뷰 전환기 구성 요소: 이루어져는 **뷰/공유/\_ViewSwitcher.cshtml** 부분 뷰 및 **ViewSwitcherController.cs** 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-376">A view-switcher component: consists of the **Views/Shared/\_ViewSwitcher.cshtml** partial view and the **ViewSwitcherController.cs** controller.</span></span> <span data-ttu-id="966f0-377">이 구성 요소는 사용자가 페이지의 데스크톱 버전으로 전환할 수 있도록 모바일 브라우저에 링크를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-377">This component will show a link on mobile browsers to enable users to switch to the desktop version of the page.</span></span>  
        <span data-ttu-id="966f0-378">![모바일 지원 사진 갤러리 프로젝트](whats-new-in-aspnet-mvc-4/_static/image23.png "사진 갤러리 프로젝트 모바일 지원")</span><span class="sxs-lookup"><span data-stu-id="966f0-378">![Photo Gallery project with mobile support](whats-new-in-aspnet-mvc-4/_static/image23.png "Photo Gallery project with mobile support")</span></span>

        <span data-ttu-id="966f0-379">*사진 갤러리 프로젝트 모바일 지원*</span><span class="sxs-lookup"><span data-stu-id="966f0-379">*Photo Gallery project with mobile support*</span></span>
4. <span data-ttu-id="966f0-380">모바일 번들을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-380">Register the Mobile bundles.</span></span> <span data-ttu-id="966f0-381">이 작업을 수행 하려면 엽니다는 **Global.asax.cs** 파일을 다음 줄을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-381">To do this, open the **Global.asax.cs** file and add the following line.</span></span>

    <span data-ttu-id="966f0-382">(코드 조각- *ASP.NET MVC 4-Ex03-랩 레지스터 모바일 번들*)</span><span class="sxs-lookup"><span data-stu-id="966f0-382">(Code Snippet - *ASP.NET MVC 4 Lab - Ex03 - Register Mobile Bundles*)</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample10.cs)]
~~~
5. <span data-ttu-id="966f0-383">데스크톱 웹 브라우저를 사용 하 여 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-383">Run the application using a desktop web browser.</span></span>
6. <span data-ttu-id="966f0-384">열기는 **Windows Phone 7 Emulator** 에 **시작 메뉴 | 모든 프로그램 | Windows Phone SDK 7.1 | Windows Phone 에뮬레이터입니다.**</span><span class="sxs-lookup"><span data-stu-id="966f0-384">Open the **Windows Phone 7 Emulator,** located in **Start Menu | All Programs | Windows Phone SDK 7.1 | Windows Phone Emulator.**</span></span>
7. <span data-ttu-id="966f0-385">Phone 시작 화면에서 Internet Explorer를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-385">In the phone start screen, open Internet Explorer.</span></span> <span data-ttu-id="966f0-386">응용 프로그램을 시작할 URL을 확인 하 고 전화 브라우저와 해당 URL로 이동 (예: `http://localhost:[PortNumber]/`).</span><span class="sxs-lookup"><span data-stu-id="966f0-386">Check out the URL where the application started and browse to that URL with the phone browser (e.g. `http://localhost:[PortNumber]/`).</span></span>

    <span data-ttu-id="966f0-387">jQuery.Mobile.MVC 모바일 장치에 대 한 액세스에 최적화 된 뷰를 표시 하는 프로젝트에서 새 자산을 만들 때 응용 프로그램이 Windows Phone 에뮬레이터에서 다르게 표시를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-387">You will notice that your application will look different in the Windows Phone emulator, as the jQuery.Mobile.MVC has created new assets in your project that show views optimized for mobile devices.</span></span>

    <span data-ttu-id="966f0-388">데스크톱 보기로 전환 하는 링크를 보여 주는 전화를 맨 위에 있는 메시지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-388">Notice the message at the top of the phone, showing the link that switches to the Desktop view.</span></span> <span data-ttu-id="966f0-389">또한는  **\_Layout.Mobile.cshtml** 레이아웃 설치 패키지에 의해 생성 된 응용 프로그램에서 다른 레이아웃이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-389">Additionally, the **\_Layout.Mobile.cshtml** layout that was created by the package you have installed is including a different layout in the application.</span></span>

    > [!NOTE]
    > <span data-ttu-id="966f0-390">지금까지 모바일 보기에 복귀할의 연결이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-390">So far, there is no link to get back to mobile view.</span></span> <span data-ttu-id="966f0-391">이상 버전에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-391">It will be included in later versions.</span></span>

    <span data-ttu-id="966f0-392">![사진 갤러리 홈 페이지의 모바일 뷰](whats-new-in-aspnet-mvc-4/_static/image24.png "사진 갤러리 홈 페이지의 모바일 뷰")</span><span class="sxs-lookup"><span data-stu-id="966f0-392">![Mobile view of the Photo Gallery Home page](whats-new-in-aspnet-mvc-4/_static/image24.png "Mobile view of the Photo Gallery Home page")</span></span>

    <span data-ttu-id="966f0-393">*사진 갤러리 홈 페이지의 모바일 뷰*</span><span class="sxs-lookup"><span data-stu-id="966f0-393">*Mobile view of the Photo Gallery Home page*</span></span>
8. <span data-ttu-id="966f0-394">키를 눌러 Visual Studio에서 **SHIFT** + **F5** 응용 프로그램 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-394">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Task_2_-_Creating_Mobile_Views"></a>
#### <a name="task-2---creating-mobile-views"></a><span data-ttu-id="966f0-395">작업 2-모바일 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="966f0-395">Task 2 - Creating Mobile Views</span></span>

<span data-ttu-id="966f0-396">이 태스크에서는 모바일 장치에서 더 나은 appareance에 적용할 콘텐츠로 인덱스 보기의 모바일 버전이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-396">In this task, you will create a mobile version of the index view with content adapted for better appareance in mobile devices.</span></span>

1. <span data-ttu-id="966f0-397">복사는 **Views\Home\Index.cshtml** 확인 하 고 붙여 넣어 복사본을 만들고, 새 파일을 이름를 **Index.Mobile.cshtml**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-397">Copy the **Views\Home\Index.cshtml** view and paste it to create a copy, rename the new file to **Index.Mobile.cshtml**.</span></span>
2. <span data-ttu-id="966f0-398">새 만든 열기 **Index.Mobile.cshtml** 보기 및 기존 바꾸기 &lt;ul&gt; 이 코드로 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-398">Open the new created **Index.Mobile.cshtml** view and replace the existing &lt;ul&gt; tag with this code.</span></span> <span data-ttu-id="966f0-399">이 통해 업데이트 됩니다.는 &lt;ul&gt; jQuery 모바일 데이터의 주석에서 jQuery 모바일 테마를 사용 하는 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-399">By doing this, you will be updating the &lt;ul&gt; tag with jQuery Mobile data annotations to use the mobile themes from jQuery.</span></span>


~~~
[!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample11.html)]

> [!NOTE] 
> 
> Notice that:
> 
> - The **data-role** attribute set to **listview** will render the list using the listview styles.
> 
> - The **data-inset** attribute set to true will show the list with rounded border and margin.
> 
> - The **data-filter** attribute set to **true** will generate a search box.
> 
> You can learn more about jQuery Mobile conventions in the project documentation: [[http://jquerymobile.com/demos/1.1.1/](http://jquerymobile.com/demos/1.1.1/)](http://jquerymobile.com/demos/1.1.1/)
~~~
3. <span data-ttu-id="966f0-400">키를 눌러 **CTRL + S** 여 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-400">Press **CTRL + S** to save the changes.</span></span>
4. <span data-ttu-id="966f0-401">전환 하는 **Windows Phone 에뮬레이터** 사이트를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-401">Switch to the **Windows Phone Emulator** and refresh the site.</span></span> <span data-ttu-id="966f0-402">갤러리 목록 뿐만 아니라 새로운 검색 상자 위쪽에 있는의 새로운 디자인을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-402">Notice the new look and feel of the gallery list, as well as the new search box located on the top.</span></span> <span data-ttu-id="966f0-403">그런 다음 검색 상자에 단어를 입력 (예를 들어, **Tulips**) 사진 갤러리에서 검색을 시작 하려면.</span><span class="sxs-lookup"><span data-stu-id="966f0-403">Then, type a word in the search box (for instance, **Tulips**) to start a search in the photo gallery.</span></span>

    <span data-ttu-id="966f0-404">![필터링 된 listview 스타일을 사용 하 여 갤러리](whats-new-in-aspnet-mvc-4/_static/image25.png "listview 스타일을 사용 하 여 필터링 된 갤러리")</span><span class="sxs-lookup"><span data-stu-id="966f0-404">![Gallery using listview style with filtering](whats-new-in-aspnet-mvc-4/_static/image25.png "Gallery using listview style with filtering")</span></span>

    <span data-ttu-id="966f0-405">*필터링 된 listview 스타일을 사용 하 여 갤러리*</span><span class="sxs-lookup"><span data-stu-id="966f0-405">*Gallery using listview style with filtering*</span></span>

    <span data-ttu-id="966f0-406">요약 하면,를 사용 하 여 보기 Mobilizer 조리법 사용 하 여 인덱스 뷰의 복사본을 만들고는 &quot;모바일&quot; 접미사입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-406">To summarize, you have used the View Mobilizer recipe to create a copy of the Index view with the &quot;mobile&quot; suffix.</span></span> <span data-ttu-id="966f0-407">이 접미사 모바일 장치에서 생성 된 모든 요청은 인덱스의이 복사본 사용 하 여 ASP.NET MVC 4를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-407">This suffix indicates to ASP.NET MVC 4 that every request generated from a mobile device will use this copy of the index.</span></span> <span data-ttu-id="966f0-408">또한 모바일 장치에 있는 사이트 디자인을 향상 시키기 위한 jQuery Mobile을 사용 하 여 인덱스 뷰의 모바일 버전을 업데이트 했습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-408">Additionally, you have updated the mobile version of the Index view to use jQuery Mobile for enhancing the site look and feel in mobile devices.</span></span>
5. <span data-ttu-id="966f0-409">Visual Studio로 다시 이동 및 열기 **Site.Mobile.css** 아래에 **콘텐츠** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-409">Go back to Visual Studio and open **Site.Mobile.css** located under the **Content** folder.</span></span>
6. <span data-ttu-id="966f0-410">이미지의 오른쪽에 표시 되도록 사진 제목의 위치를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-410">Fix the positioning of the photo title to make it show at the right side of the image.</span></span> <span data-ttu-id="966f0-411">이렇게 하려면 다음 코드를 추가 **Site.Mobile.css** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-411">To do this, add the following code to the **Site.Mobile.css** file.</span></span>

    <span data-ttu-id="966f0-412">CSS</span><span class="sxs-lookup"><span data-stu-id="966f0-412">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-mvc-4/samples/sample12.css)]
7. <span data-ttu-id="966f0-413">키를 눌러 **CTRL + S** 여 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-413">Press **CTRL + S** to save the changes.</span></span>
8. <span data-ttu-id="966f0-414">로 다시 전환는 **Windows Phone 에뮬레이터** 사이트를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-414">Switch back to the **Windows Phone Emulator** and refresh the site.</span></span> <span data-ttu-id="966f0-415">공지 사진 제목 제대로 이제에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-415">Notice the photo title is properly positioned now.</span></span>

    <span data-ttu-id="966f0-416">![이미지의 오른쪽에 배치 하는 제목](whats-new-in-aspnet-mvc-4/_static/image26.png "이미지의 오른쪽에 배치 하는 제목")</span><span class="sxs-lookup"><span data-stu-id="966f0-416">![Title positioned on the right side of the image](whats-new-in-aspnet-mvc-4/_static/image26.png "Title positioned on the right side of the image")</span></span>

    <span data-ttu-id="966f0-417">*이미지의 오른쪽에 배치 하는 제목*</span><span class="sxs-lookup"><span data-stu-id="966f0-417">*Title positioned on the right side of the image*</span></span>

<a id="Task_3_-_jQuery_Mobile_Themes"></a>
#### <a name="task-3---jquery-mobile-themes"></a><span data-ttu-id="966f0-418">작업 3-jQuery Mobile 테마</span><span class="sxs-lookup"><span data-stu-id="966f0-418">Task 3 - jQuery Mobile Themes</span></span>

<span data-ttu-id="966f0-419">모든 레이아웃 및 jQuery Mobile 위젯의 새로운 개체 지향 CSS 프레임 워크 사이트 및 응용 프로그램에 완전히 통합 된 비주얼 디자인 테마를 적용할 수 있도록 하 여 설계 됩니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-419">Every layout and widget in jQuery Mobile is designed around a new object-oriented CSS framework that makes it possible to apply a complete unified visual design theme to sites and applications.</span></span>

<span data-ttu-id="966f0-420">jQuery Mobile 기본 테마 문자 권한이 부여 된 5 견본 포함 (a, b, c, d, e)에 대해 빠른 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-420">jQuery Mobile's default Theme includes 5 swatches that are given letters (a, b, c, d, e) for quick reference.</span></span>

<span data-ttu-id="966f0-421">이 태스크에서는 모바일 사용할 레이아웃을 기본값 보다 다양 한 테마를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-421">In this task, you will update the mobile layout to use a different theme than the default.</span></span>

1. <span data-ttu-id="966f0-422">Visual Studio로 다시 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-422">Switch back to Visual Studio.</span></span>
2. <span data-ttu-id="966f0-423">열기는  **\_Layout.Mobile.cshtml** 에 있는 파일 **Views\Shared**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-423">Open the **\_Layout.Mobile.cshtml** file located in **Views\Shared**.</span></span>
3. <span data-ttu-id="966f0-424">로 설정 하는 데이터-역할 div 요소를 찾은 &quot;페이지&quot; 하 고 업데이트는 **데이터 테마** 를 &quot; **e**&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-424">Find the div element with the data-role set to &quot;page&quot; and update the **data-theme** to &quot;**e**&quot;.</span></span>


~~~
[!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample13.html)]
~~~
4. <span data-ttu-id="966f0-425">키를 눌러 **CTRL + S** 여 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-425">Press **CTRL + S** to save the changes.</span></span>
5. <span data-ttu-id="966f0-426">사이트 새로 고침의 **Windows Phone 에뮬레이터** 새 색 구성표를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-426">Refresh the site in the **Windows Phone Emulator** and notice the new colors scheme.</span></span>

    <span data-ttu-id="966f0-427">![다른 색 구성표를 사용 하는 모바일 레이아웃](whats-new-in-aspnet-mvc-4/_static/image27.png "다른 색 구성표를 사용 하는 모바일 레이아웃")</span><span class="sxs-lookup"><span data-stu-id="966f0-427">![Mobile layout with a different color scheme](whats-new-in-aspnet-mvc-4/_static/image27.png "Mobile layout with a different color scheme")</span></span>

    <span data-ttu-id="966f0-428">*다른 색 구성표를 사용 하는 모바일 레이아웃*</span><span class="sxs-lookup"><span data-stu-id="966f0-428">*Mobile layout with a different color scheme*</span></span>

<a id="Task_4_-_Using_the_View-Switcher_Component_and_the_Browser_Overriding_Features"></a>
#### <a name="task-4---using-the-view-switcher-component-and-the-browser-overriding-features"></a><span data-ttu-id="966f0-429">4-뷰 전환기 구성 요소 및 기능을 재정의 하는 브라우저를 사용 하 여 작업</span><span class="sxs-lookup"><span data-stu-id="966f0-429">Task 4 - Using the View-Switcher Component and the Browser Overriding Features</span></span>

<span data-ttu-id="966f0-430">모바일 액세스에 최적화 된 웹 페이지에 대 한 규칙 텍스트가 리 바탕 화면 보기 또는 사용자가 페이지의 데스크톱 버전으로 전환할 수 있는 전체 사이트 모드와 같은 링크를 추가 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-430">A convention for mobile-optimized web pages is to add a link whose text is something like Desktop view or Full site mode that lets users switch to a desktop version of the page.</span></span> <span data-ttu-id="966f0-431">JQuery.Mobile.MVC 패키지에는 샘플이 들어 **뷰 전환기** 에 사용 되는이 목적을 위해 구성 요소는  **\_Layout.Mobile.cshtml** 보기.</span><span class="sxs-lookup"><span data-stu-id="966f0-431">The jQuery.Mobile.MVC package includes a sample **view-switcher** component for this purpose used in the **\_Layout.Mobile.cshtml** view.</span></span>

<span data-ttu-id="966f0-432">![데스크톱 보기로 전환 하려면 링크](whats-new-in-aspnet-mvc-4/_static/image28.png "링크 데스크톱 보기로 전환 하려면")</span><span class="sxs-lookup"><span data-stu-id="966f0-432">![Link to switch to Desktop View](whats-new-in-aspnet-mvc-4/_static/image28.png "Link to switch to Desktop View")</span></span>

<span data-ttu-id="966f0-433">*데스크톱 보기로 전환에 연결*</span><span class="sxs-lookup"><span data-stu-id="966f0-433">*Link to switch to Desktop View*</span></span>

<span data-ttu-id="966f0-434">라는 새로운 기능을 사용 하 여 뷰 전환기 **브라우저 재정의**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-434">The view switcher uses a new feature called **Browser Overriding**.</span></span> <span data-ttu-id="966f0-435">이 기능에는 다른 브라우저 (사용자 에이전트)에서 실제로 생성 되는 것에서 온 요청 처럼 처리할 응용을 프로그램 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-435">This feature lets your application treat requests as if they were coming from a different browser (user agent) than the one they are actually coming from.</span></span>

<span data-ttu-id="966f0-436">이 태스크에서는 샘플 구현 jQuery.Mobile.MVC 및 ASP.NET MVC 4의 기능을 재정의 하는 새 브라우저 추가 뷰 전환기를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-436">In this task, you will explore the sample implementation of a view-switcher added by jQuery.Mobile.MVC and the new browser overriding features in ASP.NET MVC 4.</span></span>

1. <span data-ttu-id="966f0-437">Visual Studio로 다시 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-437">Switch back to Visual Studio.</span></span>
2. <span data-ttu-id="966f0-438">열기는  **\_Layout.Mobile.cshtml** 보기 아래에 **Views\Shared** 폴더 및 부분 뷰로 참조 하 고 뷰 전환기 구성 요소를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-438">Open the **\_Layout.Mobile.cshtml** view located under the **Views\Shared** folder and notice the view-switcher component being referenced as a partial view.</span></span>

    <span data-ttu-id="966f0-439">![뷰 전환기 구성 요소를 사용 하 여 모바일 레이아웃](whats-new-in-aspnet-mvc-4/_static/image29.png "뷰 전환기 구성 요소를 사용 하 여 모바일 레이아웃")</span><span class="sxs-lookup"><span data-stu-id="966f0-439">![Mobile layout using View-Switcher component](whats-new-in-aspnet-mvc-4/_static/image29.png "Mobile layout using View-Switcher component")</span></span>

    <span data-ttu-id="966f0-440">*뷰 전환기 구성 요소를 사용 하 여 모바일 레이아웃*</span><span class="sxs-lookup"><span data-stu-id="966f0-440">*Mobile layout using View-Switcher component*</span></span>
3. <span data-ttu-id="966f0-441">열기는  **\_ViewSwitcher.cshtml** 부분 뷰입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-441">Open the **\_ViewSwitcher.cshtml** partial view.</span></span>

    <span data-ttu-id="966f0-442">새 메서드를 사용 하는 부분 뷰 **ViewContext.HttpContext.GetOverriddenBrowser()** 하 웹 요청의 원점을 확인 하 고 데스크톱 또는 모바일 뷰를 전환 하려면 해당 링크를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-442">The partial view uses the new method **ViewContext.HttpContext.GetOverriddenBrowser()** to determine the origin of the web request and show the corresponding link to switch either to the Desktop or Mobile views.</span></span>

    <span data-ttu-id="966f0-443">**GetOverridenBrowser** 메서드가 반환 되는 **HttpBrowserCapabilitiesBase** 사용자 에이전트 요청에 대 한 현재 설정에 해당 하는 인스턴스 (실제 또는 재정의).</span><span class="sxs-lookup"><span data-stu-id="966f0-443">The **GetOverridenBrowser** method returns an **HttpBrowserCapabilitiesBase** instance that corresponds to the user agent currently set for the request (actual or overridden).</span></span> <span data-ttu-id="966f0-444">이 값을 사용 하 여 같은 속성을 가져오는 **IsMobileDevice**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-444">You can use this value to get properties such as **IsMobileDevice**.</span></span>

    <span data-ttu-id="966f0-445">![부분 뷰 ViewSwitcher](whats-new-in-aspnet-mvc-4/_static/image30.png "ViewSwitcher 부분 뷰")</span><span class="sxs-lookup"><span data-stu-id="966f0-445">![ViewSwitcher partial view](whats-new-in-aspnet-mvc-4/_static/image30.png "ViewSwitcher partial view")</span></span>

    <span data-ttu-id="966f0-446">*ViewSwitcher 부분 뷰*</span><span class="sxs-lookup"><span data-stu-id="966f0-446">*ViewSwitcher partial view*</span></span>
4. <span data-ttu-id="966f0-447">열기는 **ViewSwitcherController.cs** 클래스는 **컨트롤러** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-447">Open the **ViewSwitcherController.cs** class located in the **Controllers** folder.</span></span> <span data-ttu-id="966f0-448">체크 아웃 해당 SwitchView 작업 ViewSwitcher 구성 요소에 있는 링크에 의해 호출 되 고 새 HttpContext 메서드 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-448">Check out that SwitchView action is called by the link in the ViewSwitcher component, and notice the new HttpContext methods.</span></span>

    - <span data-ttu-id="966f0-449">**HttpContext.ClearOverridenBrowser()** 메서드는 현재 요청에 대 한 재정의 된 사용자 에이전트를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-449">The **HttpContext.ClearOverridenBrowser()** method removes any overridden user agent for the current request.</span></span>
    - <span data-ttu-id="966f0-450">**HttpContext.SetOverridenBrowser()** 메서드가 지정된 된 사용자 에이전트를 사용 하 여 요청의 실제 사용자 에이전트 값을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-450">The **HttpContext.SetOverridenBrowser()** method overrides the request's actual user agent value using the specified user agent.</span></span>  
        <span data-ttu-id="966f0-451">![ViewSwitcher 컨트롤러](whats-new-in-aspnet-mvc-4/_static/image31.png "ViewSwitcher 컨트롤러")</span><span class="sxs-lookup"><span data-stu-id="966f0-451">![ViewSwitcher Controller](whats-new-in-aspnet-mvc-4/_static/image31.png "ViewSwitcher Controller")</span></span>  
<span data-ttu-id="966f0-452">*ViewSwitcher 컨트롤러*</span><span class="sxs-lookup"><span data-stu-id="966f0-452">*ViewSwitcher Controller*</span></span>

        <span data-ttu-id="966f0-453">브라우저 재정의 사용 하지 않는 jQuery.Mobile.MVC 패키지를 설치 하지 않는 경우에 ASP.NET MVC 4의 핵심 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-453">Browser Overriding is a core feature of ASP.NET MVC 4, which is also available even if you do not install the jQuery.Mobile.MVC package.</span></span> <span data-ttu-id="966f0-454">그러나이 기능에는 뷰, 레이아웃 및 부분 뷰 영향을 받으며 Request.Browser 개체에 종속 되는 기능의 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-454">However, this feature affects only view, layout, and partial-view, and it does not affect any of the features that depend on the Request.Browser object.</span></span>

<a id="Task_5_-_Adding_the_View-Switcher_in_the_Desktop_View"></a>
#### <a name="task-5---adding-the-view-switcher-in-the-desktop-view"></a><span data-ttu-id="966f0-455">작업 5-바탕 화면 보기에 있는 뷰 전환기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-455">Task 5 - Adding the View-Switcher in the Desktop View</span></span>

<span data-ttu-id="966f0-456">이 태스크에서는 데스크톱 레이아웃 뷰 전환기를 포함 하도록 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-456">In this task, you will update the desktop layout to include the view-switcher.</span></span> <span data-ttu-id="966f0-457">이렇게 하면 모바일 사용자가 바탕 화면 보기를 탐색할 때 모바일 보기도 다시 돌아가십시오.</span><span class="sxs-lookup"><span data-stu-id="966f0-457">This will allow mobile users to go back to the mobile view when browsing the desktop view.</span></span>

1. <span data-ttu-id="966f0-458">사이트를 새로 고 **Windows Phone 에뮬레이터**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-458">Refresh the site in the **Windows Phone Emulator**.</span></span>
2. <span data-ttu-id="966f0-459">클릭는 **바탕 화면 보기** 갤러리의 위쪽에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-459">Click on the **Desktop view** link at the top of the gallery.</span></span> <span data-ttu-id="966f0-460">모바일 보기를 반환할 수 있도록 바탕 화면 보기에 없는 뷰 전환기 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-460">Notice there is no view-switcher in the desktop view to allow you return to the mobile view.</span></span>
3. <span data-ttu-id="966f0-461">Visual Studio로 다시 이동 및 열기는  **\_Layout.cshtml** 보기.</span><span class="sxs-lookup"><span data-stu-id="966f0-461">Go back to Visual Studio and open the **\_Layout.cshtml** view.</span></span>
4. <span data-ttu-id="966f0-462">로그인 섹션을 찾아 렌더링에 대 한 호출을 삽입의  **\_ViewSwitcher** 아래 부분 뷰는  **\_LogOnPartial** 부분 뷰입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-462">Find the login section and insert a call to render the **\_ViewSwitcher** partial view below the **\_LogOnPartial** partial view.</span></span> <span data-ttu-id="966f0-463">그런 다음 눌러 **CTRL + S** 여 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-463">Then, press **CTRL + S** to save the changes.</span></span>


~~~
[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample14.cshtml)]
~~~
5. <span data-ttu-id="966f0-464">키를 눌러 **CTRL + S** 여 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-464">Press **CTRL + S** to save the changes.</span></span>
6. <span data-ttu-id="966f0-465">Windows Phone 에뮬레이터에서 페이지를 새로 고치고 확대 하려면 화면을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-465">Refresh the page in the Windows Phone Emulator and double-click the screen to zoom in.</span></span> <span data-ttu-id="966f0-466">홈 페이지에 이제 표시에 **모바일 보기** 모바일에서 데스크톱 보기로 전환 하는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-466">Notice that the home page now shows the **Mobile view** link that switches from mobile to desktop view.</span></span>

    <span data-ttu-id="966f0-467">![바탕 화면 보기에서 렌더링 전환기 볼](whats-new-in-aspnet-mvc-4/_static/image32.png "뷰 전환기 바탕 화면 보기에서 렌더링")</span><span class="sxs-lookup"><span data-stu-id="966f0-467">![View Switcher rendered in desktop view](whats-new-in-aspnet-mvc-4/_static/image32.png "View Switcher rendered in desktop view")</span></span>

    <span data-ttu-id="966f0-468">*바탕 화면 보기에서 렌더링 된 뷰 전환기*</span><span class="sxs-lookup"><span data-stu-id="966f0-468">*View Switcher rendered in desktop view*</span></span>
7. <span data-ttu-id="966f0-469">모바일 뷰로 다시 전환 하 고 찾아보기 <strong>에 대 한</strong> 페이지 (http://localhost[port] / Home/에 대 한).</span><span class="sxs-lookup"><span data-stu-id="966f0-469">Switch to the Mobile view again and browse to <strong>About</strong> page (http://localhost[port]/Home/About).</span></span> <span data-ttu-id="966f0-470">About.Mobile.cshtml 보기를 만들지 않은 경우에 정보 페이지 표시 되는지 확인 모바일 레이아웃을 사용 하 여 (\_Layout.Mobile.cshtml).</span><span class="sxs-lookup"><span data-stu-id="966f0-470">Notice that, even if you haven't created an About.Mobile.cshtml view, the About page is displayed using the mobile layout (\_Layout.Mobile.cshtml).</span></span>

    <span data-ttu-id="966f0-471">![페이지에 대 한](whats-new-in-aspnet-mvc-4/_static/image33.png "페이지에 대 한")</span><span class="sxs-lookup"><span data-stu-id="966f0-471">![About page](whats-new-in-aspnet-mvc-4/_static/image33.png "About page")</span></span>

    <span data-ttu-id="966f0-472">*페이지 정보*</span><span class="sxs-lookup"><span data-stu-id="966f0-472">*About page*</span></span>
8. <span data-ttu-id="966f0-473">마지막으로, 데스크톱 웹 브라우저에서 사이트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-473">Finally, open the site in a desktop Web browser.</span></span> <span data-ttu-id="966f0-474">이전 업데이트에 영향을 미치지 않습니다 바탕 화면 보기를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-474">Notice that none of the previous updates has affected the desktop view.</span></span>

    <span data-ttu-id="966f0-475">![바탕 화면 보기 PhotoGallery](whats-new-in-aspnet-mvc-4/_static/image34.png "PhotoGallery 바탕 화면 보기")</span><span class="sxs-lookup"><span data-stu-id="966f0-475">![PhotoGallery desktop view](whats-new-in-aspnet-mvc-4/_static/image34.png "PhotoGallery desktop view")</span></span>

    <span data-ttu-id="966f0-476">*PhotoGallery 바탕 화면 보기*</span><span class="sxs-lookup"><span data-stu-id="966f0-476">*PhotoGallery desktop view*</span></span>

<a id="Task_6_-_Creating_New_Display_Modes"></a>
#### <a name="task-6---creating-new-display-modes"></a><span data-ttu-id="966f0-477">태스크 6-새 디스플레이 모드 만들기</span><span class="sxs-lookup"><span data-stu-id="966f0-477">Task 6 - Creating New Display Modes</span></span>

<span data-ttu-id="966f0-478">새 디스플레이 모드 기능을 사용 하는 응용 프로그램 요청을 생성 하는 브라우저에 따라 보기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-478">The new display modes feature lets an application select views depending on the browser that is generating the request.</span></span> <span data-ttu-id="966f0-479">예를 들어 데스크톱 브라우저 홈 페이지를 요청 하는 경우 응용 프로그램은 반환 된 **Views\Home\Index.cshtml** 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-479">For example, if a desktop browser requests the Home page, the application will return the **Views\Home\Index.cshtml** template.</span></span> <span data-ttu-id="966f0-480">그런 다음 모바일 브라우저 홈 페이지를 요청 하는 경우 응용 프로그램은 반환 된 **Views\Home\Index.mobile.cshtml** 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-480">Then, if a mobile browser requests the Home page, the application will return the **Views\Home\Index.mobile.cshtml** template.</span></span>

<span data-ttu-id="966f0-481">이 태스크에서는 iPhone 장치에 대 한 사용자 지정된 레이아웃을 만듭니다 및 iPhone 장치에서 요청을 시뮬레이션 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-481">In this task, you will create a customized layout for iPhone devices, and you will have to simulate requests from iPhone devices.</span></span> <span data-ttu-id="966f0-482">이 위해 중 하나는 iPhone 에뮬레이터/시뮬레이터를 사용할 수 있습니다 (같은 [Electric 모바일 시뮬레이터](http://www.electricplum.com/)) 또는 사용자 에이전트를 수정 하는 추가 기능을 사용 하 여 브라우저.</span><span class="sxs-lookup"><span data-stu-id="966f0-482">To do this, you can use either an iPhone emulator/simulator (like [Electric Mobile Simulator](http://www.electricplum.com/)) or a browser with add-ons that modify the user agent.</span></span> <span data-ttu-id="966f0-483">Safari 브라우저에서 사용자 에이전트 문자열을 설정 하는 방법에는 iPhone을 에뮬레이션 하기 위해 지침은 [Safari 있다고 생각 IE 되 게 하는 방법](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) David Alison 블로그에서.</span><span class="sxs-lookup"><span data-stu-id="966f0-483">For instructions on how to set the user agent string in an Safari browser to emulate an iPhone, see [How to let Safari pretend it's IE](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) in David Alison's blog.</span></span>

<span data-ttu-id="966f0-484">**이 작업은 선택 사항 실행 하지 않고 랩 전체에서 계속 수에 유의 하십시오.**</span><span class="sxs-lookup"><span data-stu-id="966f0-484">**Notice that this task is optional and you can continue throughout the lab without executing it.**</span></span>

1. <span data-ttu-id="966f0-485">키를 눌러 Visual Studio에서 **SHIFT** + **F5** 응용 프로그램 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-485">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
2. <span data-ttu-id="966f0-486">열기 **Global.asax.cs** 다음 추가 문을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-486">Open **Global.asax.cs** and add the following using statement.</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample15.cs)]
~~~
3. <span data-ttu-id="966f0-487">응용 프로그램에 다음 강조 표시 된 코드를 추가\_메서드를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-487">Add the following highlighted code into the Application\_Start method.</span></span>

    <span data-ttu-id="966f0-488">(코드 조각- *ASP.NET MVC 4 랩-Ex03-iPhone DisplayMode*)</span><span class="sxs-lookup"><span data-stu-id="966f0-488">(Code Snippet - *ASP.NET MVC 4 Lab - Ex03 - iPhone DisplayMode*)</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample16.cs)]

You have registered a new **DefaultDisplayMode named &quot;iPhone&quot;**, within the static **DisplayModeProvider.Instance.Modes** static list, that will be matched against each incoming request. If the incoming request contains the string &quot;iPhone&quot;, ASP.NET MVC will find the views whose name contain the &quot;iPhone&quot; suffix. The 0 parameter indicates how specific is the new mode; for instance, this view is more specific than the general &quot;.mobile&quot; rule that matches requests from mobile devices.

After this code runs, when an iPhone browser generates a request, your application will use the **Views\Shared\\_Layout.iPhone.cshtml** layout you will create in the next steps.

> [!NOTE]
> This way of testing the request for iPhone has been simplified for demo purposes and might not work as expected for every iPhone user agent string (for example test is case sensitive).
~~~
4. <span data-ttu-id="966f0-489">복사본을 만듭니다는  **\_Layout.Mobile.cshtml** 파일에 **Views\Shared** 폴더에 복사본의 이름을 바꾼 및 &quot; **\_Layout.iPhone.csthml**&quot;.</span><span class="sxs-lookup"><span data-stu-id="966f0-489">Create a copy of the **\_Layout.Mobile.cshtml** file in the **Views\Shared** folder and rename the copy to &quot;**\_Layout.iPhone.csthml**&quot;.</span></span>
5. <span data-ttu-id="966f0-490">열기  **\_Layout.iPhone.csthml** 이전 단계에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-490">Open **\_Layout.iPhone.csthml** you created in the previous step.</span></span>
6. <span data-ttu-id="966f0-491">데이터 역할 특성 설정 하 여 div 요소를 찾아 **페이지** 변경 하 고는 **데이터 테마** 특성을 &quot; **는**&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-491">Find the div element with the data-role attribute set to **page** and change the **data-theme** attribute to &quot;**a**&quot;.</span></span>


~~~
[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample17.cshtml)]

Now you have 3 layouts in your ASP.NET MVC 4 application:

1. **\_Layout.cshtml**: default layout used for desktop browsers.
2. **\_Layout.mobile.cshtml**: default layout used for mobile devices.
3. **\_Layout.iPhone.cshtml**: specific layout for iPhone devices, using a different color scheme to differentiate from \_Layout.mobile.cshtml.
~~~
7. <span data-ttu-id="966f0-492">키를 눌러 **F5** 응용 프로그램을 실행 하 고 사이트에서 탐색 하 고 **Windows Phone 에뮬레이터**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-492">Press **F5** to run the application and browse the site in the **Windows Phone Emulator**.</span></span>
8. <span data-ttu-id="966f0-493">열기는 **iPhone 시뮬레이터** (참조 [부록 C](#AppendixC) 설치 하 고 iPhone 시뮬레이터가 구성 하는 방법에 대 한 지침은), 너무 사이트를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-493">Open an **iPhone simulator** (see [Appendix C](#AppendixC) for instructions on how to install and configure an iPhone simulator), and browse to the site too.</span></span> <span data-ttu-id="966f0-494">각 전화는 특정 템플릿을 사용 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-494">Notice that each phone is using the specific template.</span></span>

    ![Using-different-views-for-each-mobile-device2](whats-new-in-aspnet-mvc-4/_static/image35.png)

    <span data-ttu-id="966f0-496">*서로 다른 뷰를 사용 하 여 각 모바일 장치에 대 한*</span><span class="sxs-lookup"><span data-stu-id="966f0-496">*Using different views for each mobile device*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Using_Asynchronous_Controllers"></a>
### <a name="exercise-4-using-asynchronous-controllers"></a><span data-ttu-id="966f0-497">연습 4: 비동기 컨트롤러를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="966f0-497">Exercise 4: Using Asynchronous Controllers</span></span>

<span data-ttu-id="966f0-498">Microsoft.NET Framework 4.5에서는 C# 및 Visual Basic로 비동기.NET 프로그래밍에 대 한 새 기초를 제공 하는 새로운 언어 기능을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-498">Microsoft .NET Framework 4.5 introduces new language features in C# and Visual Basic to provide a new foundation for asynchrony in .NET programming.</span></span> <span data-ttu-id="966f0-499">이 새 foundation 비슷합니다-쉽고 약-동기 프로그래밍으로 간단한 비동기 프로그래밍을 사용 하십시오.</span><span class="sxs-lookup"><span data-stu-id="966f0-499">This new foundation makes asynchronous programming similar to - and about as straightforward as - synchronous programming.</span></span> <span data-ttu-id="966f0-500">ASP.NET MVC 4의 비동기 작업 메서드를 사용 하 여 쓸 수는 **AsyncController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-500">You are now able to write asynchronous action methods in ASP.NET MVC 4 by using the **AsyncController** class.</span></span> <span data-ttu-id="966f0-501">장기 실행에 대 한 비동기 작업 메서드를 사용할 수 있는데, CPU 바인딩되지 않은 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-501">You can use asynchronous action methods for long-running, non-CPU bound requests.</span></span> <span data-ttu-id="966f0-502">이렇게 차단 하는 웹 서버의 요청 처리 되는 동안 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-502">This avoids blocking the Web server from performing work while the request is being processed.</span></span> <span data-ttu-id="966f0-503">AsyncController 클래스는 일반적으로 장기 실행 웹 서비스 호출에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-503">The AsyncController class is typically used for long-running Web service calls.</span></span>

<span data-ttu-id="966f0-504">이 연습에서는 ASP.NET MVC 4의 비동기 작업의 기본 사항을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-504">This exercise explains the basics of asynchronous operation in ASP.NET MVC 4.</span></span> <span data-ttu-id="966f0-505">심층 분석 하려는 경우에 다음 문서 아웃 확인할 수 있습니다. [[https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="966f0-505">If you want a deeper dive, you can check out the following article: [[https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)</span></span>

<a id="Task_1_-_Implementing_an_Asynchronous_Controller"></a>
#### <a name="task-1---implementing-an-asynchronous-controller"></a><span data-ttu-id="966f0-506">작업 1-비동기 컨트롤러를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-506">Task 1 - Implementing an Asynchronous Controller</span></span>

1. <span data-ttu-id="966f0-507">열기는 **시작** 솔루션에 있는 **소스/Ex4-Async/시작/** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-507">Open the **Begin** solution located at **Source/Ex4-Async/Begin/** folder.</span></span> <span data-ttu-id="966f0-508">그렇지 않은 경우 계속 사용할 수도 있습니다는 **끝** 솔루션, 이전 연습을 완료 하 여 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-508">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="966f0-509">제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면.</span><span class="sxs-lookup"><span data-stu-id="966f0-509">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="966f0-510">이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-510">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="966f0-511">에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="966f0-511">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="966f0-512">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-512">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="966f0-513">NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-513">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="966f0-514">NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-514">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="966f0-515">이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-515">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="966f0-516">열기는 **HomeController.cs** 에서 클래스는 **컨트롤러** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-516">Open the **HomeController.cs** class from the **Controllers** folder.</span></span>
3. <span data-ttu-id="966f0-517">다음 추가 문을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-517">Add the following using statement.</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample18.cs)]
~~~
4. <span data-ttu-id="966f0-518">업데이트는 **HomeController** 클래스에서 상속 하도록 **AsyncController**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-518">Update the **HomeController** class to inherit from **AsyncController**.</span></span> <span data-ttu-id="966f0-519">컨트롤러 AsyncController에서 파생 되는 비동기 요청을 처리 하는 ASP.NET을 사용 하 고 여전히 서비스 동기 작업 메서드 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-519">Controllers that derive from AsyncController enable ASP.NET to process asynchronous requests, and they can still service synchronous action methods.</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample19.cs)]
~~~
5. <span data-ttu-id="966f0-520">추가 **비동기** 키워드를는 **인덱스** 메서드 형식을 반환 하 고 **작업&lt;ActionResult&gt;**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-520">Add the **async** keyword to the **Index** method and make it return the type **Task&lt;ActionResult&gt;**.</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample20.cs)]

> [!NOTE]
> The **async** keyword is one of the new keywords the .NET Framework 4.5 provides; it tells the compiler that this method contains asynchronous code. A **Task** object represents an asynchronous operation that may complete at some point in the future.
~~~
6. <span data-ttu-id="966f0-521">대체는 **클라이언트입니다. GetAsync()** 아래와 같이 await 키워드를 사용 하 여 전체 비동기 버전 사용 하 여 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-521">Replace the **client.GetAsync()** call with the full async version using await keyword as shown below.</span></span>

    <span data-ttu-id="966f0-522">(코드 조각- *ASP.NET MVC 4-Ex04-랩 GetAsync*)</span><span class="sxs-lookup"><span data-stu-id="966f0-522">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - GetAsync*)</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample21.cs)]

> [!NOTE]
> In the previous version, you were using the **Result** property from the **Task** object to block the thread until the result is returned (sync version).
> 
> Adding the **await** keyword tells the compiler to asynchronously wait for the task returned from the method call. This means that the rest of the code will be executed as a callback only after the awaited method completes. Another thing to notice is that you do not need to change your try-catch block in order to make this work: the exceptions that happen in background or in foreground will still be caught without any extra work using a handler provided by the framework.
~~~
7. <span data-ttu-id="966f0-523">아래와 같이 새 코드 줄을 대체 하 여 비동기 구현의을 계속 하는 코드 변경</span><span class="sxs-lookup"><span data-stu-id="966f0-523">Change the code to continue with the asynchronous implementation by replacing the lines with the new code as shown below</span></span>

    <span data-ttu-id="966f0-524">(코드 조각- *ASP.NET MVC 4-Ex04-랩 ReadAsStringAsync*)</span><span class="sxs-lookup"><span data-stu-id="966f0-524">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - ReadAsStringAsync*)</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample22.cs)]
~~~
8. <span data-ttu-id="966f0-525">응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-525">Run the application.</span></span> <span data-ttu-id="966f0-526">크게 변경 되지를 확인할 수 있지만 코드 스레드 풀은 서버 리소스의 더 나은 사용량 및 성능 향상에서 스레드를 차단 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-526">You will notice no major changes, but your code will not block a thread from the thread pool making a better usage of the server resources and improving performance.</span></span>

    > [!NOTE]
    > <span data-ttu-id="966f0-527">랩에 새로운 비동기 프로그래밍 기능에 대 한 자세히 알아볼 수 있습니다 &quot; **C# 및 Visual Basic.NET 4.5의 비동기 프로그래밍** &quot; Visual Studio 트레이닝 키트에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-527">You can learn more about the new asynchronous programming features in the lab &quot;**Asynchronous Programming in .NET 4.5 with C# and Visual Basic**&quot; included in the Visual Studio Training Kit.</span></span>

<a id="Task_2_-_Handling_Time-Outs_with_Cancellation_Tokens"></a>
#### <a name="task-2---handling-time-outs-with-cancellation-tokens"></a><span data-ttu-id="966f0-528">작업 2-취소 토큰 인 처리 제한 시간</span><span class="sxs-lookup"><span data-stu-id="966f0-528">Task 2 - Handling Time-Outs with Cancellation Tokens</span></span>

<span data-ttu-id="966f0-529">작업 인스턴스를 반환 하는 비동기 작업 메서드에 시간 제한도 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-529">Asynchronous action methods that return Task instances can also support time-outs.</span></span> <span data-ttu-id="966f0-530">이 작업의 취소 토큰을 사용 하 여 제한 시간 시나리오를 처리 하는 인덱스 메서드 코드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-530">In this task, you will update the Index method code to handle a time-out scenario using a cancellation token.</span></span>

1. <span data-ttu-id="966f0-531">Visual Studio 및 키를 눌러로 돌아가서 **SHIFT + f 5를 눌러** 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-531">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>
2. <span data-ttu-id="966f0-532">다음 코드를 추가 하는 문을 사용 하는 **HomeController.cs** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-532">Add the following using statement to the **HomeController.cs** file.</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample23.cs)]
~~~
3. <span data-ttu-id="966f0-533">받을 인덱스 동작을 업데이트 한 **CancellationToken** 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-533">Update the Index action to receive a **CancellationToken** argument.</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample24.cs)]
~~~
4. <span data-ttu-id="966f0-534">업데이트는 **GetAsync** 호출 취소 토큰을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-534">Update the **GetAsync** call to pass the cancellation token.</span></span>

    <span data-ttu-id="966f0-535">(코드 조각- *CancellationToken과 함께 ASP.NET MVC 4-Ex04-랩 SendAsync*)</span><span class="sxs-lookup"><span data-stu-id="966f0-535">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - SendAsync with CancellationToken*)</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample25.cs)]
~~~
5. <span data-ttu-id="966f0-536">데코 레이트는 *인덱스* 메서드는 **AsyncTimeout** 특성이 500 밀리초로 설정 및 **HandleError** 처리 하도록 구성 하는 특성  **TaskCanceledException** 리디렉션하여는 **TimedOut** 보기.</span><span class="sxs-lookup"><span data-stu-id="966f0-536">Decorate the *Index* method with an **AsyncTimeout** attribute set to 500 milliseconds and a **HandleError** attribute configured to handle **TaskCanceledException** by redirecting to a **TimedOut** view.</span></span>

    <span data-ttu-id="966f0-537">(코드 조각- *ASP.NET MVC 4-Ex04-랩 특성*)</span><span class="sxs-lookup"><span data-stu-id="966f0-537">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - Attributes*)</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample26.cs)]
~~~
6. <span data-ttu-id="966f0-538">열기는 **PhotoController** 클래스 및 업데이트는 **갤러리** 메서드를 장기 실행 작업을 시뮬레이션 하는 실행 1000 밀리초 (1 초)을 지연 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-538">Open the **PhotoController** class and update the **Gallery** method to delay the execution 1000 miliseconds (1 second) to simulate a long running task.</span></span>


~~~
[!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample27.cs)]
~~~
7. <span data-ttu-id="966f0-539">열기는 **Web.config** 파일을 다음 요소를 추가 하 여 사용자 지정 오류를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-539">Open the **Web.config** file and enable custom errors by adding the following element.</span></span>


~~~
[!code-xml[Main](whats-new-in-aspnet-mvc-4/samples/sample28.xml)]
~~~
8. <span data-ttu-id="966f0-540">새 보기 만들기 **Views\Shared** 라는 **TimedOut** 및 기본 레이아웃을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-540">Create a new view in **Views\Shared** named **TimedOut** and use the default layout.</span></span> <span data-ttu-id="966f0-541">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭는 **Views\Shared** 폴더를 선택 **추가 | 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-541">In the Solution Explorer, right-click the **Views\Shared** folder and select **Add | View**.</span></span>

    <span data-ttu-id="966f0-542">![각 모바일 장치에 대 한 서로 다른 뷰를 사용 하 여](whats-new-in-aspnet-mvc-4/_static/image36.png "서로 다른 뷰를 사용 하 여 각 모바일 장치에 대 한")</span><span class="sxs-lookup"><span data-stu-id="966f0-542">![Using different views for each mobile device](whats-new-in-aspnet-mvc-4/_static/image36.png "Using different views for each mobile device")</span></span>

    <span data-ttu-id="966f0-543">*서로 다른 뷰를 사용 하 여 각 모바일 장치에 대 한*</span><span class="sxs-lookup"><span data-stu-id="966f0-543">*Using different views for each mobile device*</span></span>
9. <span data-ttu-id="966f0-544">업데이트는 **TimedOut** 아래와 같이 콘텐츠를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-544">Update the **TimedOut** view content as shown below.</span></span>


~~~
[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample29.cshtml)]
~~~
10. <span data-ttu-id="966f0-545">응용 프로그램을 실행 하 고 루트 URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-545">Run the application and navigate to the root URL.</span></span> <span data-ttu-id="966f0-546">추가한는 **Thread.Sleep** 1000 밀리초에서 생성 된 시간 제한 오류를 얻게 됩니다는 **AsyncTimeout** 특성과 여 catch는 **HandleError** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-546">As you have added a **Thread.Sleep** of 1000 milliseconds, you will get a time-out error, generated by the **AsyncTimeout** attribute and catch by the **HandleError** attribute.</span></span>

    <span data-ttu-id="966f0-547">![처리 시간 제한 예외](whats-new-in-aspnet-mvc-4/_static/image37.png "처리 시간 제한 예외")</span><span class="sxs-lookup"><span data-stu-id="966f0-547">![Time-out exception handled](whats-new-in-aspnet-mvc-4/_static/image37.png "Time-out exception handled")</span></span>

    <span data-ttu-id="966f0-548">*처리 시간 제한 예외*</span><span class="sxs-lookup"><span data-stu-id="966f0-548">*Time-out exception handled*</span></span>

> [!NOTE]
> <span data-ttu-id="966f0-549">다음 Windows Azure 웹 사이트에이 응용 프로그램을 배포할 수는 또한 [부록 d: 게시 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램](#AppendixD)합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-549">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix D: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixD).</span></span>


<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="966f0-550">요약</span><span class="sxs-lookup"><span data-stu-id="966f0-550">Summary</span></span>

<span data-ttu-id="966f0-551">이 실습 랩에서 있습니다 한 관찰 된 새로운 기능 중 일부에 ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="966f0-551">In this hands-on-lab, you've observed some of the new features resident in ASP.NET MVC 4.</span></span> <span data-ttu-id="966f0-552">다음과 같은 개념을 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-552">The following concepts have been discussed:</span></span>

- <span data-ttu-id="966f0-553">ASP.NET MVC 프로젝트 템플릿을 포함 한 새로운 모바일 응용 프로그램 프로젝트 템플릿을에 향상 된 기능을 활용</span><span class="sxs-lookup"><span data-stu-id="966f0-553">Take advantage of the enhancements to the ASP.NET MVC project templates-including the new mobile application project template</span></span>
- <span data-ttu-id="966f0-554">HTML5 뷰포트 특성 및 CSS 미디어 쿼리를 사용 하 여 모바일 장치에 표시를 향상 시키기</span><span class="sxs-lookup"><span data-stu-id="966f0-554">Use the HTML5 viewport attribute and CSS media queries to improve the display on mobile devices</span></span>
- <span data-ttu-id="966f0-555">JQuery Mobile 점진적 향상 된 기능에 대 한 터치에 최적화 된 웹 UI를 작성 하기 위한 사용</span><span class="sxs-lookup"><span data-stu-id="966f0-555">Use jQuery Mobile for progressive enhancements and for building touch-optimized web UI</span></span>
- <span data-ttu-id="966f0-556">모바일 전용 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="966f0-556">Create mobile-specific views</span></span>
- <span data-ttu-id="966f0-557">뷰 전환기 구성 요소를 사용 하 여 응용 프로그램에 모바일 및 데스크톱 뷰 사이 전환 하려면</span><span class="sxs-lookup"><span data-stu-id="966f0-557">Use the view-switcher component to toggle between mobile and desktop views in the application</span></span>
- <span data-ttu-id="966f0-558">비동기 컨트롤러 작업 지원을 사용 하 여 만들기</span><span class="sxs-lookup"><span data-stu-id="966f0-558">Create asynchronous controllers using task support</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a><span data-ttu-id="966f0-559">부록 a: 코드 조각을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="966f0-559">Appendix A: Using Code Snippets</span></span>

<span data-ttu-id="966f0-560">코드 조각 바로 쉽게 얻습니다 필요한 코드를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-560">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="966f0-561">랩 문서는 알려 정확 하 게 사용 가능 시기, 다음 그림에 나와 있는 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-561">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="966f0-562">![Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여](whats-new-in-aspnet-mvc-4/_static/image38.png "Visual Studio를 사용 하 여 코드 조각을 프로젝트에 코드를 삽입 하려면")</span><span class="sxs-lookup"><span data-stu-id="966f0-562">![Using Visual Studio code snippets to insert code into your project](whats-new-in-aspnet-mvc-4/_static/image38.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="966f0-563">*Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여*</span><span class="sxs-lookup"><span data-stu-id="966f0-563">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="966f0-564">***키보드 (C#만)를 사용 하 여 코드 조각을 추가 하려면***</span><span class="sxs-lookup"><span data-stu-id="966f0-564">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="966f0-565">코드를 삽입 하려는 위치에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-565">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="966f0-566">공백 또는 하이픈만) (없이 코드 조각 이름을 입력 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-566">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="966f0-567">IntelliSense 표시 조각 이름과 일치 하는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-567">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="966f0-568">올바른 코드 조각 선택 (또는 전체 코드 조각이 이름이 선택 될 때까지 입력 유지).</span><span class="sxs-lookup"><span data-stu-id="966f0-568">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="966f0-569">커서 위치에 코드 조각을 삽입 하려면 두 번 탭 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-569">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="966f0-570">![코드 조각 이름을 입력 하기 시작](whats-new-in-aspnet-mvc-4/_static/image39.png "조각 이름을 입력 하기 시작")</span><span class="sxs-lookup"><span data-stu-id="966f0-570">![Start typing the snippet name](whats-new-in-aspnet-mvc-4/_static/image39.png "Start typing the snippet name")</span></span>

<span data-ttu-id="966f0-571">*코드 조각 이름을 입력 하기 시작*</span><span class="sxs-lookup"><span data-stu-id="966f0-571">*Start typing the snippet name*</span></span>

<span data-ttu-id="966f0-572">![Tab 키를 눌러 강조 표시 된 코드 조각 선택](whats-new-in-aspnet-mvc-4/_static/image40.png "Tab 키를 눌러 강조 표시 된 코드 조각 선택")</span><span class="sxs-lookup"><span data-stu-id="966f0-572">![Press Tab to select the highlighted snippet](whats-new-in-aspnet-mvc-4/_static/image40.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="966f0-573">*Tab 키를 눌러 강조 표시 된 코드 조각 선택*</span><span class="sxs-lookup"><span data-stu-id="966f0-573">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="966f0-574">![확장 하 고 Tab 키를 눌러 다시 코드 조각](whats-new-in-aspnet-mvc-4/_static/image41.png "확장 하 고 Tab 키를 눌러 다시 코드 조각")</span><span class="sxs-lookup"><span data-stu-id="966f0-574">![Press Tab again and the snippet will expand](whats-new-in-aspnet-mvc-4/_static/image41.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="966f0-575">*확장 하 고 Tab 키를 눌러 다시 코드 조각*</span><span class="sxs-lookup"><span data-stu-id="966f0-575">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="966f0-576">***마우스 (C#, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면***</span><span class="sxs-lookup"><span data-stu-id="966f0-576">***To add a code snippet using the mouse (C#, Visual Basic and XML)***</span></span>

1. <span data-ttu-id="966f0-577">코드 조각을 삽입 하려면 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-577">Right-click where you want to insert the code snippet.</span></span>
2. <span data-ttu-id="966f0-578">선택 **조각 삽입** 이어서 **내 코드 조각**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-578">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
3. <span data-ttu-id="966f0-579">클릭 하 여 목록에서 관련 조각을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-579">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="966f0-580">![코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭](whats-new-in-aspnet-mvc-4/_static/image42.png "코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추 클릭")</span><span class="sxs-lookup"><span data-stu-id="966f0-580">![Right-click where you want to insert the code snippet and select Insert Snippet](whats-new-in-aspnet-mvc-4/_static/image42.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="966f0-581">*코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭*</span><span class="sxs-lookup"><span data-stu-id="966f0-581">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="966f0-582">![클릭 하 여 목록에서 관련 조각을 선택](whats-new-in-aspnet-mvc-4/_static/image43.png "클릭 하 여 목록에서 관련 조각을 선택")</span><span class="sxs-lookup"><span data-stu-id="966f0-582">![Pick the relevant snippet from the list, by clicking on it](whats-new-in-aspnet-mvc-4/_static/image43.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="966f0-583">*클릭 하 여 목록에서 관련 조각을 선택합니다*</span><span class="sxs-lookup"><span data-stu-id="966f0-583">*Pick the relevant snippet from the list, by clicking on it*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="966f0-584">부록 b: 설치 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="966f0-584">Appendix B: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="966f0-585">설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 버전을 사용 하 여 **[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="966f0-585">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="966f0-586">다음 지침을 설치 하는 데 필요한 단계를 안내 하 *Visual studio Express 2012 for Web* 를 사용 하 여 *Microsoft 웹 플랫폼 설치 관리자*합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-586">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="966f0-587">로 이동 [ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-587">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="966f0-588">또는 이미 설치 된 웹 플랫폼 설치 관리자를 열 수 있습니다 및 제품에 대 한 검색 &quot; <em>Visual Studio Express 2012 for Web Windows Azure SDK와</em>&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-588">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="966f0-589">클릭 **지금 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-589">Click on **Install Now**.</span></span> <span data-ttu-id="966f0-590">없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-590">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="966f0-591">한 번 **웹 플랫폼 설치 관리자** 열려 클릭 **설치** 는 설치 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-591">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="966f0-592">![Visual Studio Express 설치](whats-new-in-aspnet-mvc-4/_static/image44.png "Visual Studio Express 설치")</span><span class="sxs-lookup"><span data-stu-id="966f0-592">![Install Visual Studio Express](whats-new-in-aspnet-mvc-4/_static/image44.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="966f0-593">*Visual Studio Express 설치*</span><span class="sxs-lookup"><span data-stu-id="966f0-593">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="966f0-594">모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-594">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![사용 조건 동의](whats-new-in-aspnet-mvc-4/_static/image45.png)

    <span data-ttu-id="966f0-596">*사용 조건 동의*</span><span class="sxs-lookup"><span data-stu-id="966f0-596">*Accepting the license terms*</span></span>
5. <span data-ttu-id="966f0-597">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-597">Wait until the downloading and installation process completes.</span></span>

    ![설치 진행률](whats-new-in-aspnet-mvc-4/_static/image46.png)

    <span data-ttu-id="966f0-599">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="966f0-599">*Installation progress*</span></span>
6. <span data-ttu-id="966f0-600">설치가 완료 되 면 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-600">When the installation completes, click **Finish**.</span></span>

    ![설치 완료](whats-new-in-aspnet-mvc-4/_static/image47.png)

    <span data-ttu-id="966f0-602">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="966f0-602">*Installation completed*</span></span>
7. <span data-ttu-id="966f0-603">클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-603">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="966f0-604">Visual Studio Express for Web을 열려면로 이동는 **시작** 화면를 쓰기 시작할 &quot; **VS Express**&quot;, 클릭는 **VS Express for Web** 바둑판식 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-604">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![웹 타일에 대 한 VS Express](whats-new-in-aspnet-mvc-4/_static/image48.png)

    <span data-ttu-id="966f0-606">*웹 타일에 대 한 VS Express*</span><span class="sxs-lookup"><span data-stu-id="966f0-606">*VS Express for Web tile*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Installing_WebMatrix_2_and_iPhone_Simulator"></a>
## <a name="appendix-c-installing-webmatrix-2-and-iphone-simulator"></a><span data-ttu-id="966f0-607">부록 c: 설치 WebMatrix 2 및 iPhone 시뮬레이터</span><span class="sxs-lookup"><span data-stu-id="966f0-607">Appendix C: Installing WebMatrix 2 and iPhone Simulator</span></span>

<span data-ttu-id="966f0-608">시뮬레이션 된 iPhone 장치에서 사이트를 실행 하려면 WebMatrix 확장을 사용할 수 있습니다 &quot;iPhone에 대 한 전기 모바일 시뮬레이터&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-608">To run your site in a simulated iPhone device you can use the WebMatrix extension &quot;Electric Mobile Simulator for the iPhone&quot;.</span></span> <span data-ttu-id="966f0-609">또한 Visual Studio 2012에서 시뮬레이터를 실행 하려면 같은 확장 프로그램을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-609">Also, you can configure the same extension to run the simulator from Visual Studio 2012.</span></span>

<a id="ApxCTask1"></a>

<a id="Task_1_-_Installing_WebMatrix_2"></a>
#### <a name="task-1---installing-webmatrix-2"></a><span data-ttu-id="966f0-610">작업 1-WebMatrix 2 설치</span><span class="sxs-lookup"><span data-stu-id="966f0-610">Task 1 - Installing WebMatrix 2</span></span>

1. <span data-ttu-id="966f0-611">로 이동 [ [ https://go.microsoft.com/?linkid=9809776 ](https://go.microsoft.com/?linkid=9809776) ](https://go.microsoft.com/?linkid=9810169)합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-611">Go to [[https://go.microsoft.com/?linkid=9809776](https://go.microsoft.com/?linkid=9809776)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="966f0-612">또는 이미 설치 된 웹 플랫폼 설치 관리자를 열 수 있습니다 및 제품에 대 한 검색 &quot; <em>WebMatrix 2</em>&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-612">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>WebMatrix 2</em>&quot;.</span></span>
2. <span data-ttu-id="966f0-613">클릭 **지금 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-613">Click on **Install Now**.</span></span> <span data-ttu-id="966f0-614">없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-614">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="966f0-615">한 번 **웹 플랫폼 설치 관리자** 열려 클릭 **설치** 는 설치 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-615">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="966f0-616">![WebMatrix 2 설치](whats-new-in-aspnet-mvc-4/_static/image49.png "WebMatrix 2를 설치 합니다.")</span><span class="sxs-lookup"><span data-stu-id="966f0-616">![Install WebMatrix 2](whats-new-in-aspnet-mvc-4/_static/image49.png "Install WebMatrix 2")</span></span>

    <span data-ttu-id="966f0-617">*WebMatrix 2를 설치 합니다.*</span><span class="sxs-lookup"><span data-stu-id="966f0-617">*Install WebMatrix 2*</span></span>
4. <span data-ttu-id="966f0-618">모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-618">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    <span data-ttu-id="966f0-619">![사용 조건 동의](whats-new-in-aspnet-mvc-4/_static/image50.png "사용 조건 동의")</span><span class="sxs-lookup"><span data-stu-id="966f0-619">![Accepting the license terms](whats-new-in-aspnet-mvc-4/_static/image50.png "Accepting the license terms")</span></span>

    <span data-ttu-id="966f0-620">*사용 조건 동의*</span><span class="sxs-lookup"><span data-stu-id="966f0-620">*Accepting the license terms*</span></span>
5. <span data-ttu-id="966f0-621">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-621">Wait until the downloading and installation process completes.</span></span>

    <span data-ttu-id="966f0-622">![설치 진행률](whats-new-in-aspnet-mvc-4/_static/image51.png "설치 진행률")</span><span class="sxs-lookup"><span data-stu-id="966f0-622">![Installation progress](whats-new-in-aspnet-mvc-4/_static/image51.png "Installation progress")</span></span>

    <span data-ttu-id="966f0-623">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="966f0-623">*Installation progress*</span></span>
6. <span data-ttu-id="966f0-624">설치가 완료 되 면 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-624">When the installation completes, click **Finish**.</span></span>

    <span data-ttu-id="966f0-625">![설치가 완료](whats-new-in-aspnet-mvc-4/_static/image52.png "설치 완료")</span><span class="sxs-lookup"><span data-stu-id="966f0-625">![Installation completed](whats-new-in-aspnet-mvc-4/_static/image52.png "Installation completed")</span></span>

    <span data-ttu-id="966f0-626">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="966f0-626">*Installation completed*</span></span>
7. <span data-ttu-id="966f0-627">클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-627">Click **Exit** to close Web Platform Installer.</span></span>

<a id="ApxCTask2"></a>

<a id="Task_2_-_Installing_the_iPhone_Simulator_Extension"></a>
#### <a name="task-2---installing-the-iphone-simulator-extension"></a><span data-ttu-id="966f0-628">작업 2-iPhone 시뮬레이터 확장 설치</span><span class="sxs-lookup"><span data-stu-id="966f0-628">Task 2 - Installing the iPhone Simulator Extension</span></span>

1. <span data-ttu-id="966f0-629">실행 **WebMatrix** 및 모든 기존 웹 사이트를 열거나 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-629">Run **WebMatrix** and open any existing Web site or create a new one.</span></span>
2. <span data-ttu-id="966f0-630">클릭는 **실행** 에서 단추는 **홈** 리본 및 선택 **새로 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-630">Click the **Run** button from the **Home** ribbon and select **Add new**.</span></span>

    <span data-ttu-id="966f0-631">![새 WebMatrix 확장을 추가](whats-new-in-aspnet-mvc-4/_static/image53.png "새 WebMatrix 확장을 추가 합니다.")</span><span class="sxs-lookup"><span data-stu-id="966f0-631">![Adding new WebMatrix extension](whats-new-in-aspnet-mvc-4/_static/image53.png "Adding new WebMatrix extension")</span></span>

    <span data-ttu-id="966f0-632">*새 WebMatrix 확장을 추가합니다.*</span><span class="sxs-lookup"><span data-stu-id="966f0-632">*Adding new WebMatrix extension*</span></span>
3. <span data-ttu-id="966f0-633">선택 **iPhone 시뮬레이터** 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-633">Select **iPhone Simulator** and click **Install**.</span></span>

    <span data-ttu-id="966f0-634">![WebMatrix 확장을 검색](whats-new-in-aspnet-mvc-4/_static/image54.png "WebMatrix 검색 확장")</span><span class="sxs-lookup"><span data-stu-id="966f0-634">![Browsing WebMatrix extensions](whats-new-in-aspnet-mvc-4/_static/image54.png "Browsing WebMatrix extensions")</span></span>

    <span data-ttu-id="966f0-635">*WebMatrix 확장 검색*</span><span class="sxs-lookup"><span data-stu-id="966f0-635">*Browsing WebMatrix extensions*</span></span>
4. <span data-ttu-id="966f0-636">패키지 세부 정보 클릭 **설치** 확장 설치를 계속 하려면.</span><span class="sxs-lookup"><span data-stu-id="966f0-636">In the package details, click **Install** to continue with the extension installation.</span></span>

    <span data-ttu-id="966f0-637">![iPhone 시뮬레이터 확장](whats-new-in-aspnet-mvc-4/_static/image55.png "iPhone 시뮬레이터 확장")</span><span class="sxs-lookup"><span data-stu-id="966f0-637">![iPhone Simulator extension](whats-new-in-aspnet-mvc-4/_static/image55.png "iPhone Simulator extension")</span></span>

    <span data-ttu-id="966f0-638">*iPhone 시뮬레이터 확장*</span><span class="sxs-lookup"><span data-stu-id="966f0-638">*iPhone Simulator extension*</span></span>
5. <span data-ttu-id="966f0-639">읽고 확장 EULA에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-639">Read and accept the extension EULA.</span></span>

    <span data-ttu-id="966f0-640">![WebMatrix 확장 EULA](whats-new-in-aspnet-mvc-4/_static/image56.png "WebMatrix 확장 EULA")</span><span class="sxs-lookup"><span data-stu-id="966f0-640">![WebMatrix extension EULA](whats-new-in-aspnet-mvc-4/_static/image56.png "WebMatrix extension EULA")</span></span>

    <span data-ttu-id="966f0-641">*WebMatrix 확장 EULA*</span><span class="sxs-lookup"><span data-stu-id="966f0-641">*WebMatrix extension EULA*</span></span>
6. <span data-ttu-id="966f0-642">이제, 실행할 수 있습니다 웹 사이트가 WebMatrix에서 iPhone 시뮬레이터 옵션을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-642">Now, you can run your Web site from WebMatrix using the iPhone Simulator option.</span></span>

    <span data-ttu-id="966f0-643">![IPhone을 사용 하 여 실행](whats-new-in-aspnet-mvc-4/_static/image57.png "iPhone을 사용 하 여 실행")</span><span class="sxs-lookup"><span data-stu-id="966f0-643">![Run using iPhone](whats-new-in-aspnet-mvc-4/_static/image57.png "Run using iPhone")</span></span>

    <span data-ttu-id="966f0-644">*IPhone을 사용 하 여 실행*</span><span class="sxs-lookup"><span data-stu-id="966f0-644">*Run using iPhone*</span></span>

<a id="ApxCTask3"></a>

<a id="Task_3_-_Configuring_Visual_Studio_2012_to_run_iPhone_Simulator"></a>
#### <a name="task-3---configuring-visual-studio-2012-to-run-iphone-simulator"></a><span data-ttu-id="966f0-645">작업 3-iPhone 시뮬레이터를 실행 하려면 Visual Studio 2012를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-645">Task 3 - Configuring Visual Studio 2012 to run iPhone Simulator</span></span>

1. <span data-ttu-id="966f0-646">열고 **Visual Studio 2012** 및 모든 웹 사이트를 열거나 새 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-646">Open **Visual Studio 2012** and open any Web site or create a new project.</span></span>
2. <span data-ttu-id="966f0-647">실행 단추에서 아래쪽 화살표를 클릭 하 고 선택 **브라우저 선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-647">Click the down arrow from the Run button and select **Browse with**.</span></span>

    <span data-ttu-id="966f0-648">![브라우저 선택](whats-new-in-aspnet-mvc-4/_static/image58.png "브라우저 선택")</span><span class="sxs-lookup"><span data-stu-id="966f0-648">![Browse with](whats-new-in-aspnet-mvc-4/_static/image58.png "Browse with")</span></span>

    <span data-ttu-id="966f0-649">*브라우저 선택*</span><span class="sxs-lookup"><span data-stu-id="966f0-649">*Browse with*</span></span>
3. <span data-ttu-id="966f0-650">에 &quot;브라우저&quot; 대화 상자를 클릭 하 여 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-650">In the &quot;Browse With&quot; dialog, click **Add**.</span></span>
4. <span data-ttu-id="966f0-651">에 &quot;프로그램 추가&quot; 대화 상자에서 다음 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-651">In the &quot;Add Program&quot; dialog, use the following values:</span></span>

   - <span data-ttu-id="966f0-652"><strong>프로그램</strong>: C:\Users\*{CurrentUser}<em>\AppData\Local\Microsoft\WebMatrix\Extensions\20\iPhoneSimulator\ElectricMobileSim\ElectricMobileSim.exe * (경로 적절 하 게 업데이트)</em></span><span class="sxs-lookup"><span data-stu-id="966f0-652"><strong>Program</strong>: C:\Users\*{CurrentUser}<em>\AppData\Local\Microsoft\WebMatrix\Extensions\20\iPhoneSimulator\ElectricMobileSim\ElectricMobileSim.exe *(update the path accordingly)</em></span></span>
   - <span data-ttu-id="966f0-653">**인수**: &quot;1&quot;</span><span class="sxs-lookup"><span data-stu-id="966f0-653">**Arguments**: &quot;1&quot;</span></span>
   - <span data-ttu-id="966f0-654">**식별 이름**: iPhone 시뮬레이터</span><span class="sxs-lookup"><span data-stu-id="966f0-654">**Friendly name**: iPhone Simulator</span></span>

     <span data-ttu-id="966f0-655">![프로그램 추가](whats-new-in-aspnet-mvc-4/_static/image59.png "프로그램 추가")</span><span class="sxs-lookup"><span data-stu-id="966f0-655">![Add program](whats-new-in-aspnet-mvc-4/_static/image59.png "Add program")</span></span>

     <span data-ttu-id="966f0-656">*로 검색 하도록 프로그램 추가*</span><span class="sxs-lookup"><span data-stu-id="966f0-656">*Add program to browse with*</span></span>
5. <span data-ttu-id="966f0-657">클릭 **확인** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-657">Click **OK** and close the dialogs.</span></span>
6. <span data-ttu-id="966f0-658">이제 Visual Studio 2012에서 iPhone 시뮬레이터에서 웹 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-658">Now you are able to run your Web applications in the iPhone simulator from Visual Studio 2012.</span></span>

    <span data-ttu-id="966f0-659">![브라우저 선택 iPhone 시뮬레이터](whats-new-in-aspnet-mvc-4/_static/image60.png "iPhone 시뮬레이터 브라우저 선택")</span><span class="sxs-lookup"><span data-stu-id="966f0-659">![Browse with iPhone Simulator](whats-new-in-aspnet-mvc-4/_static/image60.png "Browse with iPhone Simulator")</span></span>

    <span data-ttu-id="966f0-660">*IPhone 시뮬레이터 브라우저 선택*</span><span class="sxs-lookup"><span data-stu-id="966f0-660">*Browse with iPhone Simulator*</span></span>

<a id="AppendixD"></a>

<a id="Appendix_D_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-d-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="966f0-661">부록 d: 웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="966f0-661">Appendix D: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="966f0-662">이 부록에서는 Windows Azure 관리 포털에서 새 웹 사이트를 만들고 Windows Azure에서 제공 하는 웹 배포 게시 기능을 활용 하기 위해 랩에서 수행 하 여 가져온 응용 프로그램을 게시 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-662">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxDTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="966f0-663">작업 1-Windows에서 새 웹 사이트를 만드는 Azure 포털</span><span class="sxs-lookup"><span data-stu-id="966f0-663">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="966f0-664">이동 하 여 [Windows Azure 관리 포털](https://manage.windowsazure.com/) 구독에 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-664">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="966f0-665">Windows Azure를 무료로 10 개 ASP.NET 웹 사이트를 호스트 하 고 트래픽이 증가 됨을 확장 한 다음 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-665">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="966f0-666">등록할 수 [여기](http://aka.ms/aspnet-hol-azure)합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-666">You can sign up [here](http://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="966f0-667">![Windows Azure 포털에 로그온](whats-new-in-aspnet-mvc-4/_static/image61.png "Windows Azure 포털에 로그인")</span><span class="sxs-lookup"><span data-stu-id="966f0-667">![Log on to Windows Azure portal](whats-new-in-aspnet-mvc-4/_static/image61.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="966f0-668">*Windows Azure 관리 포털에 로그온*</span><span class="sxs-lookup"><span data-stu-id="966f0-668">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="966f0-669">클릭 **새로** 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-669">Click **New** on the command bar.</span></span>

    <span data-ttu-id="966f0-670">![새 웹 사이트를 만드는](whats-new-in-aspnet-mvc-4/_static/image62.png "새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="966f0-670">![Creating a new Web Site](whats-new-in-aspnet-mvc-4/_static/image62.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="966f0-671">*새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="966f0-671">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="966f0-672">클릭 **계산** | **웹 사이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-672">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="966f0-673">그런 다음 선택 **빠른 생성** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-673">Then select **Quick Create** option.</span></span> <span data-ttu-id="966f0-674">새 웹 사이트에 대 한 사용 가능한 URL을 입력 하 고 클릭 **웹 사이트 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-674">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="966f0-675">Windows Azure 웹 사이트는 호스트를 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-675">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="966f0-676">빨리 만들기 옵션을 사용 하면 완성 된 웹 응용 프로그램을 Windows Azure 웹 사이트에서 포털 외부에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-676">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="966f0-677">데이터베이스를 설정 하기 위한 단계는 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-677">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="966f0-678">![빠른 생성을 사용 하 여 새 웹 사이트를 만드는](whats-new-in-aspnet-mvc-4/_static/image63.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")</span><span class="sxs-lookup"><span data-stu-id="966f0-678">![Creating a new Web Site using Quick Create](whats-new-in-aspnet-mvc-4/_static/image63.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="966f0-679">*빠른 생성을 사용 하 여 새 웹 사이트 만들기*</span><span class="sxs-lookup"><span data-stu-id="966f0-679">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="966f0-680">새 될 때까지 기다렸다가 **웹 사이트** 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-680">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="966f0-681">웹 사이트가 만들어지면 아래 링크를 클릭 하 고 **URL** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-681">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="966f0-682">새 웹 사이트가 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-682">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="966f0-683">![새 웹 사이트를 찾아](whats-new-in-aspnet-mvc-4/_static/image64.png "새 웹 사이트를 검색 합니다.")</span><span class="sxs-lookup"><span data-stu-id="966f0-683">![Browsing to the new web site](whats-new-in-aspnet-mvc-4/_static/image64.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="966f0-684">*새 웹 사이트를 검색합니다.*</span><span class="sxs-lookup"><span data-stu-id="966f0-684">*Browsing to the new web site*</span></span>

    <span data-ttu-id="966f0-685">![실행 중인 웹 사이트](whats-new-in-aspnet-mvc-4/_static/image65.png "실행 중인 웹 사이트")</span><span class="sxs-lookup"><span data-stu-id="966f0-685">![Web site running](whats-new-in-aspnet-mvc-4/_static/image65.png "Web site running")</span></span>

    <span data-ttu-id="966f0-686">*실행 중인 웹 사이트*</span><span class="sxs-lookup"><span data-stu-id="966f0-686">*Web site running*</span></span>
6. <span data-ttu-id="966f0-687">포털로 돌아가서 아래에서 웹 사이트의 이름을 클릭는 **이름** 관리 페이지를 표시 하는 열입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-687">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="966f0-688">![웹 사이트 관리 페이지 열기](whats-new-in-aspnet-mvc-4/_static/image66.png "웹 사이트 관리 페이지 열기")</span><span class="sxs-lookup"><span data-stu-id="966f0-688">![Opening the web site management pages](whats-new-in-aspnet-mvc-4/_static/image66.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="966f0-689">*웹 사이트 관리 페이지 열기*</span><span class="sxs-lookup"><span data-stu-id="966f0-689">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="966f0-690">에 **대시보드** 페이지의 **눈에 보는** 섹션에서 클릭는 **게시 프로필 다운로드** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-690">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="966f0-691">*게시 프로필* 각각의 활성화 된 게시 방법에 대 한 Windows Azure 웹 사이트에 웹 응용 프로그램을 게시 하는 데 필요한 정보가 모두 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-691">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="966f0-692">게시 프로필에는 Url, 사용자 자격 증명 및 연결 하 고 각 게시 메서드를 사용할 수 있는 끝점에 대해 인증 하는 데 필요한 데이터베이스 문자열이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-692">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="966f0-693">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** 및 **Microsoft Visual Studio 2012** 읽는 지원 하기 위해 게시 프로필에 대 한 이러한 프로그램의 구성을 자동화 Windows Azure 웹 사이트에 웹 응용 프로그램을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-693">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="966f0-694">![게시 프로필 다운로드 웹 사이트](whats-new-in-aspnet-mvc-4/_static/image67.png "게시 프로필 다운로드 웹 사이트")</span><span class="sxs-lookup"><span data-stu-id="966f0-694">![Downloading the web site publish profile](whats-new-in-aspnet-mvc-4/_static/image67.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="966f0-695">*게시 프로필 다운로드 웹 사이트*</span><span class="sxs-lookup"><span data-stu-id="966f0-695">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="966f0-696">알려진된 위치에 게시 프로필 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-696">Download the publish profile file to a known location.</span></span> <span data-ttu-id="966f0-697">더 이상이 연습에서는 Visual Studio에서 웹 응용 프로그램 Windows Azure 웹 사이트를 게시 하려면이 파일을 사용 하는 방법을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-697">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="966f0-698">![게시 프로필 파일을 저장](whats-new-in-aspnet-mvc-4/_static/image68.png "게시 프로필 저장")</span><span class="sxs-lookup"><span data-stu-id="966f0-698">![Saving the publish profile file](whats-new-in-aspnet-mvc-4/_static/image68.png "Saving the publish profile")</span></span>

    <span data-ttu-id="966f0-699">*게시 프로필 파일을 저장합니다.*</span><span class="sxs-lookup"><span data-stu-id="966f0-699">*Saving the publish profile file*</span></span>

<a id="ApxDTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="966f0-700">작업 2-데이터베이스 서버 구성</span><span class="sxs-lookup"><span data-stu-id="966f0-700">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="966f0-701">응용 프로그램에서 SQL Server를 활용 하는 경우 데이터베이스를 SQL 데이터베이스 서버 만들기 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-701">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="966f0-702">SQL Server를 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 태스크를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-702">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="966f0-703">응용 프로그램 데이터베이스를 저장 하기 위해 SQL 데이터베이스 서버를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-703">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="966f0-704">Windows Azure 관리 포털에서 구독의 SQL 데이터베이스 서버를 볼 수 있습니다 **Sql 데이터베이스** | **서버** | **서버 대시보드**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-704">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="966f0-705">만든 서버 없는 경우 수행 하 여 만들 수 있습니다는 **추가** 명령 모음에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-705">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="966f0-706">기록해는 **서버 이름 및 URL, 관리자 로그인 이름 및 암호**, 다음 작업에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-706">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="966f0-707">만들지 마십시오 데이터베이스 아직 대로 이후 단계에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-707">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="966f0-708">![SQL 데이터베이스 서버 대시보드](whats-new-in-aspnet-mvc-4/_static/image69.png "SQL 데이터베이스 서버 대시보드")</span><span class="sxs-lookup"><span data-stu-id="966f0-708">![SQL Database Server Dashboard](whats-new-in-aspnet-mvc-4/_static/image69.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="966f0-709">*SQL 데이터베이스 서버 대시보드*</span><span class="sxs-lookup"><span data-stu-id="966f0-709">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="966f0-710">다음 태스크에서는 서버 목록에 사용자의 로컬 IP 주소를 포함 해야 이러한 이유로 Visual Studio에서 데이터베이스 연결을 테스트 **허용 IP 주소**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-710">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="966f0-711">작업을 수행 하려면 **구성**에서 IP 주소를 선택 **현재 클라이언트 IP 주소** 에 붙여넣습니다는 **시작 IP 주소** 및 **끝IP주소** 클릭 하 고 텍스트 상자는 ![add-client-ip-address-ok-button](whats-new-in-aspnet-mvc-4/_static/image70.png) 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-711">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](whats-new-in-aspnet-mvc-4/_static/image70.png) button.</span></span>

    ![클라이언트 IP 주소를 추가합니다.](whats-new-in-aspnet-mvc-4/_static/image71.png)

    <span data-ttu-id="966f0-713">*클라이언트 IP 주소를 추가합니다.*</span><span class="sxs-lookup"><span data-stu-id="966f0-713">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="966f0-714">한 번는 **클라이언트 IP 주소** 허용된 된 IP 주소에 추가 됩니다 목록에서 클릭 **저장** 하 여 변경 사항을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-714">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![변경 확인](whats-new-in-aspnet-mvc-4/_static/image72.png)

    <span data-ttu-id="966f0-716">*변경 확인*</span><span class="sxs-lookup"><span data-stu-id="966f0-716">*Confirm Changes*</span></span>

<a id="ApxDTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="966f0-717">작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="966f0-717">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="966f0-718">ASP.NET MVC 4 솔루션으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-718">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="966f0-719">에 **솔루션 탐색기**웹 사이트 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-719">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="966f0-720">![응용 프로그램을 게시](whats-new-in-aspnet-mvc-4/_static/image73.png "응용 프로그램을 게시")</span><span class="sxs-lookup"><span data-stu-id="966f0-720">![Publishing the Application](whats-new-in-aspnet-mvc-4/_static/image73.png "Publishing the Application")</span></span>

    <span data-ttu-id="966f0-721">*웹 사이트를 게시*</span><span class="sxs-lookup"><span data-stu-id="966f0-721">*Publishing the web site*</span></span>
2. <span data-ttu-id="966f0-722">첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-722">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="966f0-723">![게시 프로필 가져오기](whats-new-in-aspnet-mvc-4/_static/image74.png "게시 프로필 가져오기")</span><span class="sxs-lookup"><span data-stu-id="966f0-723">![Importing the publish profile](whats-new-in-aspnet-mvc-4/_static/image74.png "Importing the publish profile")</span></span>

    <span data-ttu-id="966f0-724">*게시 프로필 가져오기*</span><span class="sxs-lookup"><span data-stu-id="966f0-724">*Importing publish profile*</span></span>
3. <span data-ttu-id="966f0-725">클릭 **연결 확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-725">Click **Validate Connection**.</span></span> <span data-ttu-id="966f0-726">유효성 검사가 완료 되 면 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-726">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="966f0-727">연결 유효성 검사 단추 옆에 표시 녹색 확인 표시가 표시 되 면 유효성 검사가 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-727">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="966f0-728">![연결 유효성 검사](whats-new-in-aspnet-mvc-4/_static/image75.png "연결 유효성 검사")</span><span class="sxs-lookup"><span data-stu-id="966f0-728">![Validating connection](whats-new-in-aspnet-mvc-4/_static/image75.png "Validating connection")</span></span>

    <span data-ttu-id="966f0-729">*연결 유효성 검사*</span><span class="sxs-lookup"><span data-stu-id="966f0-729">*Validating connection*</span></span>
4. <span data-ttu-id="966f0-730">에 **설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆의 단추 클릭 (즉, **DefaultConnection**).</span><span class="sxs-lookup"><span data-stu-id="966f0-730">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="966f0-731">![웹 배포 구성](whats-new-in-aspnet-mvc-4/_static/image76.png "웹 배포 구성")</span><span class="sxs-lookup"><span data-stu-id="966f0-731">![Web deploy configuration](whats-new-in-aspnet-mvc-4/_static/image76.png "Web deploy configuration")</span></span>

    <span data-ttu-id="966f0-732">*웹 배포 구성*</span><span class="sxs-lookup"><span data-stu-id="966f0-732">*Web deploy configuration*</span></span>
5. <span data-ttu-id="966f0-733">다음과 같이 데이터베이스 연결을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-733">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="966f0-734">에 **서버 이름** SQL 데이터베이스 서버 URL 사용 하 여 입력 된 *tcp:* 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-734">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="966f0-735">**사용자 이름** 서버 관리자 로그인 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-735">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="966f0-736">**암호** 서버 관리자 로그인 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-736">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="966f0-737">예를 들어 새 데이터베이스 이름 입력: *MVC4SampleDB*합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-737">Type a new database name, for example: *MVC4SampleDB*.</span></span>

     <span data-ttu-id="966f0-738">![대상 연결 문자열 구성](whats-new-in-aspnet-mvc-4/_static/image77.png "대상 연결 문자열 구성")</span><span class="sxs-lookup"><span data-stu-id="966f0-738">![Configuring destination connection string](whats-new-in-aspnet-mvc-4/_static/image77.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="966f0-739">*대상 연결 문자열 구성*</span><span class="sxs-lookup"><span data-stu-id="966f0-739">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="966f0-740">그런 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-740">Then click **OK**.</span></span> <span data-ttu-id="966f0-741">데이터베이스를 만들려는 대화 상자가 나타나면 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-741">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="966f0-742">![데이터베이스를 만드는](whats-new-in-aspnet-mvc-4/_static/image78.png "데이터베이스 문자열 만들기")</span><span class="sxs-lookup"><span data-stu-id="966f0-742">![Creating the database](whats-new-in-aspnet-mvc-4/_static/image78.png "Creating the database string")</span></span>

    <span data-ttu-id="966f0-743">*데이터베이스를 만드는 중*</span><span class="sxs-lookup"><span data-stu-id="966f0-743">*Creating the database*</span></span>
7. <span data-ttu-id="966f0-744">Windows azure에서 SQL 데이터베이스에 연결 하기 위해 사용할 연결 문자열은 기본 연결 텍스트 상자 내에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-744">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="966f0-745">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-745">Then click **Next**.</span></span>

    <span data-ttu-id="966f0-746">![SQL 데이터베이스를 가리키는 연결 문자열](whats-new-in-aspnet-mvc-4/_static/image79.png "SQL 데이터베이스를 가리키는 연결 문자열")</span><span class="sxs-lookup"><span data-stu-id="966f0-746">![Connection string pointing to SQL Database](whats-new-in-aspnet-mvc-4/_static/image79.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="966f0-747">*SQL 데이터베이스를 가리키는 연결 문자열*</span><span class="sxs-lookup"><span data-stu-id="966f0-747">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="966f0-748">에 **미리 보기** 페이지 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-748">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="966f0-749">![웹 응용 프로그램을 게시](whats-new-in-aspnet-mvc-4/_static/image80.png "웹 응용 프로그램 게시")</span><span class="sxs-lookup"><span data-stu-id="966f0-749">![Publishing the web application](whats-new-in-aspnet-mvc-4/_static/image80.png "Publishing the web application")</span></span>

    <span data-ttu-id="966f0-750">*웹 응용 프로그램 게시*</span><span class="sxs-lookup"><span data-stu-id="966f0-750">*Publishing the web application*</span></span>
9. <span data-ttu-id="966f0-751">게시 프로세스가 완료 되 면 게시 된 웹 사이트 기본 브라우저가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="966f0-751">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="966f0-752">![Windows Azure에 게시 된 응용 프로그램](whats-new-in-aspnet-mvc-4/_static/image81.png "Windows Azure에 게시 된 응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="966f0-752">![Application published to Windows Azure](whats-new-in-aspnet-mvc-4/_static/image81.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="966f0-753">*Windows Azure에 게시 된 응용 프로그램*</span><span class="sxs-lookup"><span data-stu-id="966f0-753">*Application published to Windows Azure*</span></span>
