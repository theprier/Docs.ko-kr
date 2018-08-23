---
uid: visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
title: '실습: 하나의 ASP.NET: ASP.NET Web Forms, MVC 및 Web API 통합 | Microsoft Docs'
author: rick-anderson
description: ASP.NET은 웹 사이트, 앱 및 MVC, Web API 등과 같은 특수 한 기술을 사용 하 여 서비스를 빌드하기 위한 프레임 워크입니다. 확장과 ASP.NET h...
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 4fe2558d-67cc-4d12-a5c1-6fb9f6f16137
msc.legacyurl: /visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
msc.type: authoredcontent
ms.openlocfilehash: b6ac0dca92ab3d75eb871099882dcea549264354
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41836587"
---
<a name="hands-on-lab-one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api"></a><span data-ttu-id="29030-104">실습: 하나의 ASP.NET: ASP.NET Web Forms, MVC 및 Web API 통합</span><span class="sxs-lookup"><span data-stu-id="29030-104">Hands On Lab: One ASP.NET: Integrating ASP.NET Web Forms, MVC and Web API</span></span>
====================
<span data-ttu-id="29030-105">[웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="29030-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="29030-106">웹 캠프 학습 키트 다운로드</span><span class="sxs-lookup"><span data-stu-id="29030-106">Download Web Camps Training Kit</span></span>](http://aka.ms/webcamps-training-kit)

> <span data-ttu-id="29030-107">ASP.NET은 웹 사이트, 앱 및 MVC, Web API 등과 같은 특수 한 기술을 사용 하 여 서비스를 빌드하기 위한 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-107">ASP.NET is a framework for building Web sites, apps and services using specialized technologies such as MVC, Web API and others.</span></span> <span data-ttu-id="29030-108">확장을 사용 하 여 ASP.NET에서 생성 된 후 표시를 표현 해야 이러한 기술을 통합 하 고 있었는지 최근 작업으로 작업 **One ASP.NET**합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-108">With the expansion ASP.NET has seen since its creation and the expressed need to have these technologies integrated, there have been recent efforts in working towards **One ASP.NET**.</span></span>
> 
> <span data-ttu-id="29030-109">Visual Studio 2013 응용 프로그램을 빌드하고 프로젝트 중 하나에 모든 ASP.NET 기술을 사용 하 여 수 있는 새로운 통합형된 프로젝트 시스템인을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-109">Visual Studio 2013 introduces a new unified project system which lets you build an application and use all the ASP.NET technologies in one project.</span></span> <span data-ttu-id="29030-110">이 기능은, 스틱을 프로젝트의 시작 부분에 한 기술을 선택 하지 않아도 되며 대신 하나의 프로젝트 내에서 여러 ASP.NET 프레임 워크를 사용 하도록 할.</span><span class="sxs-lookup"><span data-stu-id="29030-110">This feature eliminates the need to pick one technology at the start of a project and stick with it, and instead encourages the use of multiple ASP.NET frameworks within one project.</span></span>
> 
> <span data-ttu-id="29030-111">웹 캠프 교육 키트에서에서 사용할 수 있는 모든 샘플 코드 및 코드 조각 포함 됩니다 [ http://aka.ms/webcamps-training-kit ](http://aka.ms/webcamps-training-kit)합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-111">All sample code and snippets are included in the Web Camps Training Kit, available at [http://aka.ms/webcamps-training-kit](http://aka.ms/webcamps-training-kit).</span></span>


<a id="Overview"></a>
## <a name="overview"></a><span data-ttu-id="29030-112">개요</span><span class="sxs-lookup"><span data-stu-id="29030-112">Overview</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="29030-113">목표</span><span class="sxs-lookup"><span data-stu-id="29030-113">Objectives</span></span>

<span data-ttu-id="29030-114">이 실습 랩에서 학습할 방법:</span><span class="sxs-lookup"><span data-stu-id="29030-114">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="29030-115">기반 웹 사이트 만들기는 **One ASP.NET** 프로젝트 형식</span><span class="sxs-lookup"><span data-stu-id="29030-115">Create a Web site based on the **One ASP.NET** project type</span></span>
- <span data-ttu-id="29030-116">사용 하 여 다른 **ASP.NET** 같은 프레임 워크 **MVC** 하 고 **Web API** 동일한 프로젝트에서</span><span class="sxs-lookup"><span data-stu-id="29030-116">Use different **ASP.NET** frameworks like **MVC** and **Web API** in the same project</span></span>
- <span data-ttu-id="29030-117">주요 구성 요소를 식별 한 **ASP.NET** 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="29030-117">Identify the main components of an **ASP.NET** application</span></span>
- <span data-ttu-id="29030-118">활용 합니다 **ASP.NET 스 캐 폴딩** 모델 클래스를 기반으로 자동으로 만들고 컨트롤러 뷰 CRUD 작업을 수행 하기 위해 프레임 워크</span><span class="sxs-lookup"><span data-stu-id="29030-118">Take advantage of the **ASP.NET Scaffolding** framework to automatically create Controllers and Views to perform CRUD operations based on your model classes</span></span>
- <span data-ttu-id="29030-119">동일한 집합의 각 작업에 대 한 적합 한 도구를 사용 하 여 컴퓨터 및 사람이 인식할 수 형식으로 정보를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-119">Expose the same set of information in machine- and human-readable formats using the right tool for each job</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="29030-120">전제 조건</span><span class="sxs-lookup"><span data-stu-id="29030-120">Prerequisites</span></span>

<span data-ttu-id="29030-121">다음는이 실습을 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-121">The following is required to complete this hands-on lab:</span></span>

- <span data-ttu-id="29030-122">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) 이상</span><span class="sxs-lookup"><span data-stu-id="29030-122">[Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/) or greater</span></span>
- [<span data-ttu-id="29030-123">Visual Studio 2013 업데이트 1</span><span class="sxs-lookup"><span data-stu-id="29030-123">Visual Studio 2013 Update 1</span></span>](https://go.microsoft.com/fwlink/?LinkId=301714)

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="29030-124">설정</span><span class="sxs-lookup"><span data-stu-id="29030-124">Setup</span></span>

<span data-ttu-id="29030-125">이 실습에서는 연습을 실행 하려면 먼저 환경 설정을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-125">In order to run the exercises in this hands-on lab, you will need to set up your environment first.</span></span>

1. <span data-ttu-id="29030-126">Windows 탐색기를 열고 실습용 **원본** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-126">Open Windows Explorer and browse to the lab's **Source** folder.</span></span>
2. <span data-ttu-id="29030-127">마우스 오른쪽 단추로 클릭 **Setup.cmd** 선택한 **관리자 권한으로 실행** 환경을 구성 하 고이 랩에 대 한 Visual Studio 코드 조각을 설치는 설치 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-127">Right-click on **Setup.cmd** and select **Run as administrator** to launch the setup process that will configure your environment and install the Visual Studio code snippets for this lab.</span></span>
3. <span data-ttu-id="29030-128">사용자 계정 컨트롤 대화 상자를 표시 하는 경우 계속 하려면 작업을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-128">If the User Account Control dialog box is shown, confirm the action to proceed.</span></span>

> [!NOTE]
> <span data-ttu-id="29030-129">설치 프로그램을 실행 하기 전에이 랩에 대 한 모든 종속성을 선택 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-129">Make sure you have checked all the dependencies for this lab before running the setup.</span></span>


<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a><span data-ttu-id="29030-130">코드 조각 사용</span><span class="sxs-lookup"><span data-stu-id="29030-130">Using the Code Snippets</span></span>

<span data-ttu-id="29030-131">랩 문서 전체에서 코드 블록을 삽입할 지시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29030-131">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="29030-132">사용자 편의 위해이 코드의 대부분은 수동으로 추가할 필요가 없도록 하려면 Visual Studio 2013 내에서 액세스할 수 있는 Visual Studio 코드 조각으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29030-132">For your convenience, most of this code is provided as Visual Studio Code Snippets, which you can access from within Visual Studio 2013 to avoid having to add it manually.</span></span>

> [!NOTE]
> <span data-ttu-id="29030-133">각 실습에 시작 솔루션을 함께 표시 됩니다는 **시작** 다른 독립적으로 각 연습에 따라 할 수 있는 연습 하는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-133">Each exercise is accompanied by a starting solution located in the **Begin** folder of the exercise that allows you to follow each exercise independently of the others.</span></span> <span data-ttu-id="29030-134">주의 하십시오 연습 하는 동안 추가 되는 코드 조각은 솔루션부터 이러한 누락 되어 연습을 완료 될 때까지 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29030-134">Please be aware that the code snippets that are added during an exercise are missing from these starting solutions and may not work until you have completed the exercise.</span></span> <span data-ttu-id="29030-135">연습에 대 한 소스 코드 안에 있습니다.는 **최종** 해당 연습에서 단계를 완료 합니다. 결과로 생성 되는 코드를 사용 하 여 Visual Studio 솔루션에 포함 된 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-135">Inside the source code for an exercise, you will also find an **End** folder containing a Visual Studio solution with the code that results from completing the steps in the corresponding exercise.</span></span> <span data-ttu-id="29030-136">이 실습을 통해 작업 하는 동안 추가 도움이 필요한 경우 지침으로 이러한 솔루션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29030-136">You can use these solutions as guidance if you need additional help as you work through this hands-on lab.</span></span>


* * *

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="29030-137">연습</span><span class="sxs-lookup"><span data-stu-id="29030-137">Exercises</span></span>

<span data-ttu-id="29030-138">이 실습 랩에서 다음 연습에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29030-138">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="29030-139">새 웹 폼 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="29030-139">Creating a New Web Forms Project</span></span>](#Exercise1)
2. [<span data-ttu-id="29030-140">스 캐 폴딩을 사용 하 여 MVC 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="29030-140">Creating an MVC Controller Using Scaffolding</span></span>](#Exercise2)
3. [<span data-ttu-id="29030-141">스 캐 폴딩을 사용 하 여 웹 API 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="29030-141">Creating a Web API Controller Using Scaffolding</span></span>](#Exercise3)

<span data-ttu-id="29030-142">이 랩을 완료 하기 위한 예상 시간: **60 분**</span><span class="sxs-lookup"><span data-stu-id="29030-142">Estimated time to complete this lab: **60 minutes**</span></span>

> [!NOTE]
> <span data-ttu-id="29030-143">Visual Studio를 처음 시작 하면 미리 정의 된 설정 컬렉션 중 하나를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-143">When you first start Visual Studio, you must select one of the predefined settings collections.</span></span> <span data-ttu-id="29030-144">미리 정의 된 각 컬렉션에는 특정 개발 스타일에 맞게 설계 되었습니다 및 창 레이아웃, 동작 편집기, IntelliSense 코드 조각 및 대화 상자 옵션을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-144">Each predefined collection is designed to match a particular development style and determines window layouts, editor behavior, IntelliSense code snippets, and dialog box options.</span></span> <span data-ttu-id="29030-145">이 랩의 절차에서는 사용 하는 경우 Visual Studio에서 지정된 된 태스크를 수행 하는 데 필요한 작업을 설명 합니다 **일반 개발 설정** 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-145">The procedures in this lab describe the actions necessary to accomplish a given task in Visual Studio when using the **General Development Settings** collection.</span></span> <span data-ttu-id="29030-146">개발 환경에 대 한 다양 한 설정 컬렉션을 선택 하는 경우를 고려해 야 하는 단계에 차이가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29030-146">If you choose a different settings collection for your development environment, there may be differences in the steps that you should take into account.</span></span>


<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-new-web-forms-project"></a><span data-ttu-id="29030-147">연습 1: 새 웹 폼 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="29030-147">Exercise 1: Creating a New Web Forms Project</span></span>

<span data-ttu-id="29030-148">이 연습에서 사용 하 여 Visual Studio 2013에서 새 Web Forms 사이트를 만듭니다는 **One ASP.NET** 통합 프로젝트 경험을 사용 하면 동일한 응용 프로그램에서 Web Forms, MVC 및 Web API 구성 요소를 쉽게 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29030-148">In this exercise you will create a new Web Forms site in Visual Studio 2013 using the **One ASP.NET** unified project experience, which will allow you to easily integrate Web Forms, MVC and Web API components in the same application.</span></span> <span data-ttu-id="29030-149">그런 다음 생성 된 솔루션을 탐색 하 고 해당 파트를 식별 합니다 및 웹 사이트의 작업을 마지막으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29030-149">You will then explore the generated solution and identify its parts, and finally you will see the Web site in action.</span></span>

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-a-new-site-using-the-one-aspnet-experience"></a><span data-ttu-id="29030-150">작업 1 – 하나의 ASP.NET 환경을 사용 하 여 새 사이트 만들기</span><span class="sxs-lookup"><span data-stu-id="29030-150">Task 1 – Creating a New Site Using the One ASP.NET Experience</span></span>

<span data-ttu-id="29030-151">먼저이 작업에 따라 Visual Studio에서 새 웹 사이트 만들기는 **One ASP.NET** 형식 프로젝션 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-151">In this task you will start creating a new Web site in Visual Studio based on the **One ASP.NET** project type.</span></span> <span data-ttu-id="29030-152">**One ASP.NET** 를 모든 ASP.NET 기술을 통합 하 고 혼합 하 고 필요에 따라 일치 하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29030-152">**One ASP.NET** unifies all ASP.NET technologies and gives you the option to mix and match them as desired.</span></span> <span data-ttu-id="29030-153">응용 프로그램 내에서 나란히 상주 하는 Web Forms, MVC 및 Web API의 다른 구성 요소를 인식 다음 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29030-153">You will then recognize the different components of Web Forms, MVC and Web API that live side by side within your application.</span></span>

1. <span data-ttu-id="29030-154">오픈 **Visual Studio Express 2013 for Web** 선택한 **파일 | 새 프로젝트...**  새 솔루션을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-154">Open **Visual Studio Express 2013 for Web** and select **File | New Project...** to start a new solution.</span></span>

    ![새 프로젝트 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image1.png)

    <span data-ttu-id="29030-156">*새 프로젝트 만들기*</span><span class="sxs-lookup"><span data-stu-id="29030-156">*Creating a New Project*</span></span>
2. <span data-ttu-id="29030-157">에 **새 프로젝트** 대화 상자에서 **ASP.NET 웹 응용 프로그램** 아래에서 **Visual C# | 웹** 탭을 했는지 **.NET Framework 4.5** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-157">In the **New Project** dialog box, select **ASP.NET Web Application** under the **Visual C# | Web** tab, and make sure **.NET Framework 4.5** is selected.</span></span> <span data-ttu-id="29030-158">프로젝트 이름을 *MyHybridSite*, 선택 된 **위치** 클릭 **확인**.</span><span class="sxs-lookup"><span data-stu-id="29030-158">Name the project *MyHybridSite*, choose a **Location** and click **OK**.</span></span>

    ![새 ASP.NET 웹 응용 프로그램 프로젝트](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image2.png)

    <span data-ttu-id="29030-160">*새 ASP.NET 웹 응용 프로그램 프로젝트 만들기*</span><span class="sxs-lookup"><span data-stu-id="29030-160">*Creating a new ASP.NET Web Application project*</span></span>
3. <span data-ttu-id="29030-161">에 **새 ASP.NET 프로젝트** 대화 상자에서를 **Web Forms** 템플릿을 선택한 합니다 **MVC** 및 **Web API** 옵션.</span><span class="sxs-lookup"><span data-stu-id="29030-161">In the **New ASP.NET Project** dialog box, select the **Web Forms** template and select the **MVC** and **Web API** options.</span></span> <span data-ttu-id="29030-162">또한 있는지 확인 합니다 **인증** 옵션을 설정 **개별 사용자 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-162">Also, make sure that the **Authentication** option is set to **Individual User Accounts**.</span></span> <span data-ttu-id="29030-163">계속하려면 **확인** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-163">Click **OK** to continue.</span></span>

    ![Web API 및 MVC 구성 요소를 포함 하 여 Web Forms 템플릿을 사용 하 여 새 프로젝트 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image3.png)

    <span data-ttu-id="29030-165">*Web API 및 MVC 구성 요소를 포함 하 여 Web Forms 템플릿을 사용 하 여 새 프로젝트 만들기*</span><span class="sxs-lookup"><span data-stu-id="29030-165">*Creating a new project with the Web Forms template, including Web API and MVC components*</span></span>
4. <span data-ttu-id="29030-166">이제 생성 된 솔루션의 구조를 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29030-166">You can now explore the structure of the generated solution.</span></span>

    ![생성 된 솔루션 탐색](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image4.png)

    <span data-ttu-id="29030-168">*생성 된 솔루션 탐색*</span><span class="sxs-lookup"><span data-stu-id="29030-168">*Exploring the generated solution*</span></span>

    1. <span data-ttu-id="29030-169">**계정:** 이 폴더에는 Web Form 페이지 등록, 로그인 및 응용 프로그램의 사용자 계정 관리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-169">**Account:** This folder contains the Web Form pages to register, log in to and manage the application's user accounts.</span></span> <span data-ttu-id="29030-170">이 폴더를 추가 하는 경우는 **개별 사용자 계정** Web Forms 프로젝트 템플릿 구성 하는 동안 인증 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-170">This folder is added when the **Individual User Accounts** authentication option is selected during the configuration of the Web Forms project template.</span></span>
    2. <span data-ttu-id="29030-171">**모델:** 이 폴더에는 응용 프로그램 데이터를 나타내는 클래스가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29030-171">**Models:** This folder will contain the classes that represent your application data.</span></span>
    3. <span data-ttu-id="29030-172">**컨트롤러** 하 고 **뷰**: 이러한 폴더는 필요 합니다 **ASP.NET MVC** 및 **ASP.NET Web API** 구성 요소.</span><span class="sxs-lookup"><span data-stu-id="29030-172">**Controllers** and **Views**: These folders are required for the **ASP.NET MVC** and **ASP.NET Web API** components.</span></span> <span data-ttu-id="29030-173">다음 연습에서는 MVC 및 Web API 기술을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="29030-173">You will explore the MVC and Web API technologies in the next exercises.</span></span>
    4. <span data-ttu-id="29030-174">**Default.aspx**, **Contact.aspx** 하 고 **About.aspx** 파일이 빌드 관련 페이지를 시작 점으로 사용할 수 있는 미리 정의 된 Web Form 페이지에 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-174">The **Default.aspx**, **Contact.aspx** and **About.aspx** files are pre-defined Web Form pages that you can use as starting points to build the pages specific to your application.</span></span> <span data-ttu-id="29030-175">이라고 하는 별도 파일에 있는 해당 파일의 프로그래밍 논리는 &quot;코드 숨김&quot; 포함 된 파일을 &quot;합니다.에서는&quot; 또는 &quot;. aspx.cs&quot; 확장 (에 따라는 언어 사용)입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-175">The programming logic of those files resides in a separate file referred to as the &quot;code-behind&quot; file, which has an &quot;.aspx.vb&quot; or &quot;.aspx.cs&quot; extension (depending on the language used).</span></span> <span data-ttu-id="29030-176">코드 숨김 논리 서버에서 실행 하 고 동적으로 페이지에 대 한 HTML 출력을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-176">The code-behind logic runs on the server and dynamically produces the HTML output for your page.</span></span>
    5. <span data-ttu-id="29030-177">합니다 **Site.Master** 하 고 **Site.Mobile.Master** 페이지 응용 프로그램의 모양과 느낌 및 모든 페이지의 표준 동작을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-177">The **Site.Master** and **Site.Mobile.Master** pages define the look and feel and the standard behavior of all the pages in the application.</span></span>
5. <span data-ttu-id="29030-178">두 번 클릭 합니다 **Default.aspx** 페이지의 내용을 탐색 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-178">Double-click the **Default.aspx** file to explore the content of the page.</span></span>

    ![Default.aspx 페이지를 탐색합니다.](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image5.png)

    <span data-ttu-id="29030-180">*Default.aspx 페이지를 탐색합니다.*</span><span class="sxs-lookup"><span data-stu-id="29030-180">*Exploring the Default.aspx page*</span></span>

    > [!NOTE]
    > <span data-ttu-id="29030-181">합니다 **페이지** 지시문 파일의 맨 위에 있는 Web Forms 페이지의 특성을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-181">The **Page** directive at the top of the file defines the attributes of the Web Forms page.</span></span> <span data-ttu-id="29030-182">예를 들어, 합니다 **MasterPageFile** 마스터에 대 한 경로 지정 하는 특성 페이지-이 경우에 *Site.Master* 페이지 및 **Inherits** 특성 정의 상속 하도록 페이지에 대 한 코드 숨김 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-182">For example, the **MasterPageFile** attribute specifies the path to the master page -in this case, the *Site.Master* page- and the **Inherits** attribute defines the code-behind class for the page to inherit.</span></span> <span data-ttu-id="29030-183">이 클래스에 의해 결정 되는 파일에는 **코드 숨김** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-183">This class is located in the file determined by the **CodeBehind** attribute.</span></span>
    > 
    > <span data-ttu-id="29030-184">합니다 **asp: Content** 컨트롤 (텍스트, 태그 및 컨트롤) 페이지의 실제 콘텐츠를 보유 하 고에 매핑되는 **asp: ContentPlaceHolder** 마스터 페이지의 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-184">The **asp:Content** control holds the actual content of the page (text, markup and controls) and is mapped to a **asp:ContentPlaceHolder** control on the master page.</span></span> <span data-ttu-id="29030-185">내에서 페이지 콘텐츠를 렌더링 하는 경우에 *MainContent* 에 정의 된 컨트롤을 *Site.Master* 페이지.</span><span class="sxs-lookup"><span data-stu-id="29030-185">In this case, the page content will be rendered inside the *MainContent* control defined in the *Site.Master* page.</span></span>
6. <span data-ttu-id="29030-186">확장을 **앱\_시작** 폴더 및 통지를 **WebApiConfig.cs** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-186">Expand the **App\_Start** folder and notice the **WebApiConfig.cs** file.</span></span> <span data-ttu-id="29030-187">Visual Studio One ASP.NET 템플릿을 사용 하 여 프로젝트를 구성 하는 경우 웹 API를 포함 하기 때문에 생성 된 솔루션에 해당 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-187">Visual Studio included that file in the generated solution because you included Web API when configuring your project with the One ASP.NET template.</span></span>
7. <span data-ttu-id="29030-188">엽니다는 **WebApiConfig.cs** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-188">Open the **WebApiConfig.cs** file.</span></span> <span data-ttu-id="29030-189">에 *WebApiConfig* 있습니다. HTTP를 매핑하는 Web API 사용 하 여 관련 된 구성 클래스 라우팅합니다 **Web API 컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-189">In the *WebApiConfig* class you will find the configuration associated with Web API, which maps HTTP routes to **Web API controllers**.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample1.cs)]
8. <span data-ttu-id="29030-190">엽니다는 **RouteConfig.cs** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-190">Open the **RouteConfig.cs** file.</span></span> <span data-ttu-id="29030-191">내 합니다 *RegisterRoutes* 메서드를 HTTP 경로 매핑하는 MVC와 연관 된 구성을 찾을 수 있습니다 **MVC 컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-191">Inside the *RegisterRoutes* method you will find the configuration associated with MVC, which maps HTTP routes to **MVC controllers**.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample2.cs)]

<a id="Ex1Task2"></a>
#### <a name="task-2--running-the-solution"></a><span data-ttu-id="29030-192">작업 2-솔루션 실행</span><span class="sxs-lookup"><span data-stu-id="29030-192">Task 2 – Running the Solution</span></span>

<span data-ttu-id="29030-193">이 작업에서 생성 된 솔루션을 실행를 하는 앱과 같은 URL 재작성 및 기본 제공 인증 기능을 일부를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-193">In this task you will run the generated solution, explore the app and some of its features, like URL rewriting and built-in authentication.</span></span>

1. <span data-ttu-id="29030-194">키를 눌러 솔루션을 실행 하려면 **F5** 누르거나를 **시작** 도구 모음에 있는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-194">To run the solution, press **F5** or click the **Start** button located on the toolbar.</span></span> <span data-ttu-id="29030-195">브라우저에서 응용 프로그램 홈 페이지를 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-195">The application home page should open in the browser.</span></span>

    ![솔루션 실행](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image6.png)
2. <span data-ttu-id="29030-197">Web Forms 페이지 호출 되는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-197">Verify that the Web Forms pages are being invoked.</span></span> <span data-ttu-id="29030-198">이 작업을 수행 하려면 추가 **/contact.aspx** 누릅니다 주소 표시줄에서 URL로 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-198">To do this, append **/contact.aspx** to the URL in the address bar and press **Enter**.</span></span>

    ![친화적 Url](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image7.png)

    <span data-ttu-id="29030-200">*친화적 Url*</span><span class="sxs-lookup"><span data-stu-id="29030-200">*Friendly URLs*</span></span>

    > [!NOTE]
    > <span data-ttu-id="29030-201">URL로 변경 알 수 있듯이 **에문의/** 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-201">As you can see, the URL changes to **/contact**.</span></span> <span data-ttu-id="29030-202">시작 **ASP.NET 4**URL 라우팅 기능이 Web Forms에 추가 된, Url 등 작성할 수 있습니다 *[ http://www.mysite.com/products/software ](http://www.mysite.com/products/software)* 대신  *[http://www.mysite.com/products.aspx?category=software](http://www.mysite.com/products.aspx?category=software)*.</span><span class="sxs-lookup"><span data-stu-id="29030-202">Starting from **ASP.NET 4**, URL routing capabilities were added to Web Forms, so you can write URLs like *[http://www.mysite.com/products/software](http://www.mysite.com/products/software)* instead of *[http://www.mysite.com/products.aspx?category=software](http://www.mysite.com/products.aspx?category=software)*.</span></span> <span data-ttu-id="29030-203">자세한 내용은를 참조 [URL 라우팅](../../../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-203">For more information refer to [URL Routing](../../../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing.md).</span></span>
3. <span data-ttu-id="29030-204">이제 응용 프로그램에 통합 된 인증 흐름을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="29030-204">You will now explore the authentication flow integrated into the application.</span></span> <span data-ttu-id="29030-205">이 작업을 수행 하려면 **등록** 페이지의 오른쪽 위 모퉁이에서.</span><span class="sxs-lookup"><span data-stu-id="29030-205">To do this, click **Register** in the upper-right corner of the page.</span></span>

    ![새 사용자 등록](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image8.png)

    <span data-ttu-id="29030-207">*새 사용자 등록*</span><span class="sxs-lookup"><span data-stu-id="29030-207">*Registering a new user*</span></span>
4. <span data-ttu-id="29030-208">에 **등록** 페이지에서 입력을 **사용자 이름** 및 **암호**를 클릭 하 고 **등록**합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-208">In the **Register** page, enter a **User name** and **Password**, and then click **Register**.</span></span>

    ![등록 페이지](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image9.png)

    <span data-ttu-id="29030-210">*등록 페이지*</span><span class="sxs-lookup"><span data-stu-id="29030-210">*Register page*</span></span>
5. <span data-ttu-id="29030-211">응용 프로그램에서 새 계정을 등록 하 고 사용자가 인증 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="29030-211">The application registers the new account, and the user is authenticated.</span></span>

    ![인증 된 사용자](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image10.png)

    <span data-ttu-id="29030-213">*인증 된 사용자*</span><span class="sxs-lookup"><span data-stu-id="29030-213">*User authenticated*</span></span>
6. <span data-ttu-id="29030-214">Visual Studio 및 키를 눌러도 돌아가 **shift+f5** 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-214">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Exercise2"></a>
### <a name="exercise-2-creating-an-mvc-controller-using-scaffolding"></a><span data-ttu-id="29030-215">연습 2: 스 캐 폴딩을 사용 하 여 MVC 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="29030-215">Exercise 2: Creating an MVC Controller Using Scaffolding</span></span>

<span data-ttu-id="29030-216">이 연습에서 작업 및 코드 한 줄도 작성 하지 않고 CRUD 작업을 수행 하는 Razor 뷰를 사용 하 여 ASP.NET MVC 5 컨트롤러를 만들려면 Visual Studio에서 제공 하는 ASP.NET 스 캐 폴딩 프레임 워크를 활용을 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="29030-216">In this exercise you will take advantage of the ASP.NET Scaffolding framework provided by Visual Studio to create an ASP.NET MVC 5 controller with actions and Razor views to perform CRUD operations, without writing a single line of code.</span></span> <span data-ttu-id="29030-217">SQL database에서 데이터 컨텍스트 및 데이터베이스 스키마를 생성 하는 스 캐 폴딩 프로세스 Entity Framework Code First 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-217">The scaffolding process will use Entity Framework Code First to generate the data context and the database schema in the SQL database.</span></span>

<span data-ttu-id="29030-218">**Entity framework Code First**</span><span class="sxs-lookup"><span data-stu-id="29030-218">**About Entity Framework Code First**</span></span>

<span data-ttu-id="29030-219">EF (entity Framework)는 관계형 저장소 스키마를 사용 하 여 직접 프로그래밍 하는 대신 개념적 응용 프로그램 모델을 사용 하 여 프로그래밍 하 여 데이터 액세스 응용 프로그램을 만들 수 있게 하는 개체 관계형 매퍼 (ORM).</span><span class="sxs-lookup"><span data-stu-id="29030-219">Entity Framework (EF) is an object-relational mapper (ORM) that enables you to create data access applications by programming with a conceptual application model instead of programming directly using a relational storage schema.</span></span>

<span data-ttu-id="29030-220">Entity Framework Code First 모델링 워크플로가 있습니다 나타내기 위해 사용할 고유한 도메인 클래스는 쿼리를 수행 하는 경우 EF가 의존 하는 모델 변경 내용 추적 및 업데이트 함수.</span><span class="sxs-lookup"><span data-stu-id="29030-220">The Entity Framework Code First modeling workflow allows you to use your own domain classes to represent the model that EF relies on when performing querying, change-tracking and updating functions.</span></span> <span data-ttu-id="29030-221">Code First 개발 워크플로 사용 하면 필요가 없습니다 데이터베이스를 만들거나 스키마를 지정 하 여 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-221">Using the Code First development workflow, you do not need to begin your application by creating a database or specifying a schema.</span></span> <span data-ttu-id="29030-222">대신, 응용 프로그램에 가장 적합 한 도메인 모델 개체를 정의 하는 표준.NET 클래스를 작성할 수 있습니다 하 고 Entity Framework에서 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29030-222">Instead, you can write standard .NET classes that define the most appropriate domain model objects for your application, and Entity Framework will create the database for you.</span></span>

> [!NOTE]
> <span data-ttu-id="29030-223">Entity Framework에 대 한 자세히 알아볼 수 있습니다 [여기](../../../entity-framework.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-223">You can learn more about Entity Framework [here](../../../entity-framework.md).</span></span>


<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-new-model"></a><span data-ttu-id="29030-224">작업 1-새 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="29030-224">Task 1 – Creating a New Model</span></span>

<span data-ttu-id="29030-225">이제 정의 **Person** 모델 스 캐 폴딩 프로세스에서 MVC 컨트롤러 및 뷰를 만드는 데 될 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-225">You will now define a **Person** class, which will be the model used by the scaffolding process to create the MVC controller and the views.</span></span> <span data-ttu-id="29030-226">만들어 시작 합니다는 **Person** 모델 클래스와 컨트롤러의 CRUD 작업은 자동으로 만들어집니다 스 캐 폴딩 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-226">You will start by creating a **Person** model class, and the CRUD operations in the controller will be automatically created using scaffolding features.</span></span>

1. <span data-ttu-id="29030-227">열기 **Visual Studio Express 2013 for Web** 하며 **MyHybridSite.sln** 솔루션에는 **소스/e x 2-MvcScaffolding/시작** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-227">Open **Visual Studio Express 2013 for Web** and the **MyHybridSite.sln** solution located in the **Source/Ex2-MvcScaffolding/Begin** folder.</span></span> <span data-ttu-id="29030-228">또는 계속할 수 있습니다 솔루션을 사용 하 여 이전 연습에서 얻은.</span><span class="sxs-lookup"><span data-stu-id="29030-228">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>
2. <span data-ttu-id="29030-229">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **모델** 폴더를 **MyHybridSite** 프로젝트를 마우스 **추가 | 클래스...** .</span><span class="sxs-lookup"><span data-stu-id="29030-229">In **Solution Explorer**, right-click the **Models** folder of the **MyHybridSite** project and select **Add | Class...**.</span></span>

    ![사용자 모델 클래스 추가](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image11.png)

    <span data-ttu-id="29030-231">*사용자 모델 클래스 추가*</span><span class="sxs-lookup"><span data-stu-id="29030-231">*Adding the Person model class*</span></span>
3. <span data-ttu-id="29030-232">에 **새 항목 추가** 대화 상자에서 파일 이름 *Person.cs* 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-232">In the **Add New Item** dialog box, name the file *Person.cs* and click **Add**.</span></span>

    ![사용자 모델 클래스 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image12.png)

    <span data-ttu-id="29030-234">*사용자 모델 클래스 만들기*</span><span class="sxs-lookup"><span data-stu-id="29030-234">*Creating the Person model class*</span></span>
4. <span data-ttu-id="29030-235">콘텐츠를 대체 합니다 **Person.cs** 를 다음 코드로 파일.</span><span class="sxs-lookup"><span data-stu-id="29030-235">Replace the content of the **Person.cs** file with the following code.</span></span> <span data-ttu-id="29030-236">키를 눌러 **CTRL + S** 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-236">Press **CTRL + S** to save the changes.</span></span>

    <span data-ttu-id="29030-237">(코드 조각- *BringingTogetherOneAspNet-e x 2-PersonClass*)</span><span class="sxs-lookup"><span data-stu-id="29030-237">(Code Snippet - *BringingTogetherOneAspNet - Ex2 - PersonClass*)</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample3.cs)]
5. <span data-ttu-id="29030-238">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **MyHybridSite** 프로젝트를 마우스 **빌드**를 누르거나 **CTRL + SHIFT + B** 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-238">In **Solution Explorer**, right-click the **MyHybridSite** project and select **Build**, or press **CTRL + SHIFT + B** to build the project.</span></span>

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-an-mvc-controller"></a><span data-ttu-id="29030-239">작업 2-MVC 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="29030-239">Task 2 – Creating an MVC Controller</span></span>

<span data-ttu-id="29030-240">이제는 **Person** 모델을 만들, Entity Framework를 사용 하 여 ASP.NET MVC 스 캐 폴딩의 CRUD 컨트롤러 작업 및 보기를 만드는 데 사용할 **Person**.</span><span class="sxs-lookup"><span data-stu-id="29030-240">Now that the **Person** model is created, you will use ASP.NET MVC scaffolding with Entity Framework to create the CRUD controller actions and views for **Person**.</span></span>

1. <span data-ttu-id="29030-241">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **컨트롤러** 폴더를 **MyHybridSite** 프로젝트를 마우스 **추가 | 스 캐 폴드 된 새 항목...** .</span><span class="sxs-lookup"><span data-stu-id="29030-241">In **Solution Explorer**, right-click the **Controllers** folder of the **MyHybridSite** project and select **Add | New Scaffolded Item...**.</span></span>

    ![새 스 캐 폴드 된 컨트롤러 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image13.png)

    <span data-ttu-id="29030-243">*새 스 캐 폴드 된 컨트롤러 만들기*</span><span class="sxs-lookup"><span data-stu-id="29030-243">*Creating a new Scaffolded Controller*</span></span>
2. <span data-ttu-id="29030-244">에 **스 캐 폴드 추가** 대화 상자에서 **Entity Framework를 사용 하 여 뷰를 사용 하 여 MVC 5 컨트롤러** 클릭 하 고 **추가 합니다.**</span><span class="sxs-lookup"><span data-stu-id="29030-244">In the **Add Scaffold** dialog box, select **MVC 5 Controller with views, using Entity Framework** and then click **Add.**</span></span>

    ![뷰 및 Entity Framework를 사용 하 여 선택한 MVC 5 컨트롤러](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image14.png)

    <span data-ttu-id="29030-246">*뷰 및 Entity Framework를 사용 하 여 선택한 MVC 5 컨트롤러*</span><span class="sxs-lookup"><span data-stu-id="29030-246">*Selecting MVC 5 Controller with views and Entity Framework*</span></span>
3. <span data-ttu-id="29030-247">설정 *MvcPersonController* 으로 **컨트롤러 이름**를 선택 합니다 **비동기 컨트롤러 동작을 사용 하 여** 옵션을 선택 **사람 (MyHybridSite.Models)**  으로 **모델 클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-247">Set *MvcPersonController* as the **Controller name**, select the **Use async controller actions** option and select **Person (MyHybridSite.Models)** as the **Model class**.</span></span>

    ![스 캐 폴딩 사용 하 여 MVC 컨트롤러 추가](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image15.png)

    <span data-ttu-id="29030-249">*스 캐 폴딩 사용 하 여 MVC 컨트롤러 추가*</span><span class="sxs-lookup"><span data-stu-id="29030-249">*Adding an MVC controller with scaffolding*</span></span>
4. <span data-ttu-id="29030-250">아래 **데이터 컨텍스트 클래스**, 클릭 **새 데이터 컨텍스트...** .</span><span class="sxs-lookup"><span data-stu-id="29030-250">Under **Data context class**, click **New data context...**.</span></span>

    ![새 데이터 컨텍스트 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image16.png)

    <span data-ttu-id="29030-252">*새 데이터 컨텍스트 만들기*</span><span class="sxs-lookup"><span data-stu-id="29030-252">*Creating a new data context*</span></span>
5. <span data-ttu-id="29030-253">에 **새 데이터 컨텍스트에** 대화 상자에서 이름 새 데이터 컨텍스트에 *PersonContext* 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-253">In the **New Data Context** dialog box, name the new data context *PersonContext* and click **Add**.</span></span>

    ![새 PersonContext 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image17.png)

    <span data-ttu-id="29030-255">*새 PersonContext 형식 만들기*</span><span class="sxs-lookup"><span data-stu-id="29030-255">*Creating the new PersonContext type*</span></span>
6. <span data-ttu-id="29030-256">클릭 **추가** 에 대 한 새 컨트롤러에 만들려는 **Person** 스 캐 폴딩을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-256">Click **Add** to create the new controller for **Person** with scaffolding.</span></span> <span data-ttu-id="29030-257">Visual Studio에서 컨트롤러 작업, 사용자 데이터 컨텍스트 및 Razor 뷰 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-257">Visual Studio will then generate the controller actions, the Person data context and the Razor views.</span></span>

    ![MVC 컨트롤러 스 캐 폴딩을 사용 하 여 만든 후](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image18.png)

    <span data-ttu-id="29030-259">*MVC 컨트롤러 스 캐 폴딩을 사용 하 여 만든 후*</span><span class="sxs-lookup"><span data-stu-id="29030-259">*After creating the MVC controller with scaffolding*</span></span>
7. <span data-ttu-id="29030-260">엽니다는 **MvcPersonController.cs** 파일을 **컨트롤러** 폴더.</span><span class="sxs-lookup"><span data-stu-id="29030-260">Open the **MvcPersonController.cs** file in the **Controllers** folder.</span></span> <span data-ttu-id="29030-261">CRUD 작업 메서드에 자동으로 생성 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-261">Notice that the CRUD action methods have been generated automatically.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample4.cs)]

    > [!NOTE]
    > <span data-ttu-id="29030-262">선택 하 여 합니다 **비동기 컨트롤러 동작을 사용 하 여** 이전 단계에서 스 캐 폴딩에서 확인란 옵션, Visual Studio 사용자 데이터 컨텍스트에 대 한 액세스와 관련 된 모든 작업에 대 한 비동기 동작 메서드를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-262">By selecting the **Use async controller actions** check box from the scaffolding options in the previous steps, Visual Studio generates asynchronous action methods for all actions that involve access to the Person data context.</span></span> <span data-ttu-id="29030-263">CPU 바인딩되지 않은 요청을 처리 하는 동안 작업을 수행할 수 없도록 웹 서버를 차단 하지 않도록 요청을 비동기 작업 메서드를 사용 하 여 장기 실행에 대 한 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="29030-263">It is recommended that you use asynchronous action methods for long-running, non-CPU bound requests to avoid blocking the Web server from performing work while the request is being processed.</span></span>

<a id="Ex2Task3"></a>
#### <a name="task-3--running-the-solution"></a><span data-ttu-id="29030-264">작업 3 – 솔루션 실행</span><span class="sxs-lookup"><span data-stu-id="29030-264">Task 3 – Running the Solution</span></span>

<span data-ttu-id="29030-265">이 태스크에서는 실행 되었는지 확인 하려면 다시 솔루션에 대 한 보기 **Person** 예상 대로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-265">In this task, you will run the solution again to verify that the views for **Person** are working as expected.</span></span> <span data-ttu-id="29030-266">데이터베이스에 성공적으로 저장 되는 확인 하려면 새 사용자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-266">You will add a new person to verify that it is successfully saved to the database.</span></span>

1. <span data-ttu-id="29030-267">키를 눌러 **F5** 솔루션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-267">Press **F5** to run the solution.</span></span>
2. <span data-ttu-id="29030-268">이동할 **/MvcPerson**합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-268">Navigate to **/MvcPerson**.</span></span> <span data-ttu-id="29030-269">사용자의 목록을 보여 주는 스 캐 폴드 된 뷰에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="29030-269">The scaffolded view that shows the list of people should appear.</span></span>
3. <span data-ttu-id="29030-270">클릭 **새로 만들기** 새 사용자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-270">Click **Create New** to add a new person.</span></span>

    ![스 캐 폴드 된 MVC 뷰로 이동](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image19.png)

    <span data-ttu-id="29030-272">*스 캐 폴드 된 MVC 뷰로 이동*</span><span class="sxs-lookup"><span data-stu-id="29030-272">*Navigating to the scaffolded MVC views*</span></span>
4. <span data-ttu-id="29030-273">에 **만들기** 보기에서 제공를 **이름** 및 **Age** 사람과 클릭에 대 한 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-273">In the **Create** view, provide a **Name** and an **Age** for the person, and click **Create**.</span></span>

    ![새 사람 추가](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image20.png)

    <span data-ttu-id="29030-275">*새 사람 추가*</span><span class="sxs-lookup"><span data-stu-id="29030-275">*Adding a new person*</span></span>
5. <span data-ttu-id="29030-276">새 사람 목록에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29030-276">The new person is added to the list.</span></span> <span data-ttu-id="29030-277">요소 목록에서 클릭 **세부 정보** 사람의 세부 정보 보기를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-277">In the element list, click **Details** to display the person's details view.</span></span> <span data-ttu-id="29030-278">그런 다음 합니다 **세부 정보** 보기를 클릭 **목록으로 돌아가기** 목록 보기로 다시 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-278">Then, in the **Details** view, click **Back to List** to go back to the list view.</span></span>

    ![사용자의 세부 정보 보기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image21.png)

    <span data-ttu-id="29030-280">*사용자의 세부 정보 보기*</span><span class="sxs-lookup"><span data-stu-id="29030-280">*Person's details view*</span></span>
6. <span data-ttu-id="29030-281">클릭 합니다 **삭제** 사용자를 삭제 하는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-281">Click the **Delete** link to delete the person.</span></span> <span data-ttu-id="29030-282">에 **삭제** 보기에서 클릭 **삭제** 작업을 확인 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-282">In the **Delete** view, click **Delete** to confirm the operation.</span></span>

    ![사용자 삭제](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image22.png)

    <span data-ttu-id="29030-284">*사용자 삭제*</span><span class="sxs-lookup"><span data-stu-id="29030-284">*Deleting a person*</span></span>
7. <span data-ttu-id="29030-285">Visual Studio 및 키를 눌러도 돌아가 **shift+f5** 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-285">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>

<a id="Exercise3"></a>
### <a name="exercise-3-creating-a-web-api-controller-using-scaffolding"></a><span data-ttu-id="29030-286">연습 3: Web API 컨트롤러 스 캐 폴딩을 사용 하 여 만들기</span><span class="sxs-lookup"><span data-stu-id="29030-286">Exercise 3: Creating a Web API Controller Using Scaffolding</span></span>

<span data-ttu-id="29030-287">Web API 프레임 워크 ASP.NET 스택에의 일부 이며 쉽게 구현 하는 HTTP 서비스, 일반적으로 보내고 RESTful API를 통해 JSON 또는 XML 형식의 데이터를 받는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29030-287">The Web API framework is part of the ASP.NET Stack and designed to make implementing HTTP services easier, generally sending and receiving JSON- or XML-formatted data through a RESTful API.</span></span>

<span data-ttu-id="29030-288">이 연습에서는 Web API 컨트롤러를 생성 하려면 ASP.NET 스 캐 폴딩을 다시 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-288">In this exercise, you will use ASP.NET Scaffolding again to generate a Web API controller.</span></span> <span data-ttu-id="29030-289">사용 하 여 동일한 **Person** 하 고 **PersonContext** JSON 형식에서 같은 사용자 데이터를 제공 하 여 이전 연습에서 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-289">You will use the same **Person** and **PersonContext** classes from the previous exercise to provide the same person data in JSON format.</span></span> <span data-ttu-id="29030-290">동일한 리소스를 동일한 ASP.NET 응용 프로그램 내에서 다른 방법으로 노출할 수 있습니다 하는 방법을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29030-290">You will see how you can expose the same resources in different ways within the same ASP.NET application.</span></span>

<a id="Ex3Task1"></a>
#### <a name="task-1--creating-a-web-api-controller"></a><span data-ttu-id="29030-291">작업 1-웹 API 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="29030-291">Task 1 – Creating a Web API Controller</span></span>

<span data-ttu-id="29030-292">이 작업을 만든 새 **Web API 컨트롤러** JSON과 같은 컴퓨터에서 사용할 수 있는 형식으로 사용자 데이터를 노출 하는 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29030-292">In this task you will create a new **Web API Controller** that will expose the person data in a machine-consumable format like JSON.</span></span>

1. <span data-ttu-id="29030-293">열려 있지 않으면 엽니다 **Visual Studio Express 2013 for Web** 연 합니다 **MyHybridSite.sln** 솔루션을 **소스/Ex3-WebAPI/시작** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-293">If not already opened, open **Visual Studio Express 2013 for Web** and open the **MyHybridSite.sln** solution located in the **Source/Ex3-WebAPI/Begin** folder.</span></span> <span data-ttu-id="29030-294">또는 계속할 수 있습니다 솔루션을 사용 하 여 이전 연습에서 얻은.</span><span class="sxs-lookup"><span data-stu-id="29030-294">Alternatively, you can continue with the solution that you obtained in the previous exercise.</span></span>

    > [!NOTE]
    > <span data-ttu-id="29030-295">연습 3에서 시작 솔루션을 사용 하 여 시작 하는 경우 키를 눌러 **CTRL + SHIFT + B** 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-295">If you start with the Begin solution from Exercise 3, press **CTRL + SHIFT + B** to build the solution.</span></span>
2. <span data-ttu-id="29030-296">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **컨트롤러** 폴더를 **MyHybridSite** 프로젝트를 마우스 **추가 | 스 캐 폴드 된 새 항목...** .</span><span class="sxs-lookup"><span data-stu-id="29030-296">In **Solution Explorer**, right-click the **Controllers** folder of the **MyHybridSite** project and select **Add | New Scaffolded Item...**.</span></span>

    ![새 스 캐 폴드 된 컨트롤러 만들기](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image23.png)

    <span data-ttu-id="29030-298">*새 스 캐 폴드 된 컨트롤러 만들기*</span><span class="sxs-lookup"><span data-stu-id="29030-298">*Creating a new scaffolded Controller*</span></span>
3. <span data-ttu-id="29030-299">에 **스 캐 폴드 추가** 대화 상자에서 **Web API** 한 다음 왼쪽된 창에서 **Entity Framework를 사용 하 여 작업을 사용 하 여 Web API 2 컨트롤러** 가운데 창에서 를클릭하고 **추가 합니다.**</span><span class="sxs-lookup"><span data-stu-id="29030-299">In the **Add Scaffold** dialog box, select **Web API** in the left pane, then **Web API 2 Controller with actions, using Entity Framework** in the middle pane and then click **Add.**</span></span>

    <span data-ttu-id="29030-300">![작업 및 Entity Framework를 사용 하 여 Web API 2 컨트롤러를 선택 하면](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image24.png "작업 및 Entity Framework를 사용 하 여 Web API 2 컨트롤러 선택")</span><span class="sxs-lookup"><span data-stu-id="29030-300">![Selecting Web API 2 Controller with actions and Entity Framework](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image24.png "Selecting Web API 2 Controller with actions and Entity Framework")</span></span>

    <span data-ttu-id="29030-301">*작업 및 Entity Framework를 사용 하 여 Web API 2 컨트롤러 선택*</span><span class="sxs-lookup"><span data-stu-id="29030-301">*Selecting Web API 2 Controller with actions and Entity Framework*</span></span>
4. <span data-ttu-id="29030-302">설정 *ApiPersonController* 으로 **컨트롤러 이름**를 선택 합니다 **비동기 컨트롤러 동작을 사용 하 여** 옵션을 선택 **사람 (MyHybridSite.Models)**  하 고 **PersonContext (MyHybridSite.Models)** 으로 **모델** 및 **데이터 컨텍스트** 각각 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-302">Set *ApiPersonController* as the **Controller name**, select the **Use async controller actions** option and select **Person (MyHybridSite.Models)** and **PersonContext (MyHybridSite.Models)** as the **Model** and **Data context** classes respectively.</span></span> <span data-ttu-id="29030-303">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-303">Then click **Add**.</span></span>

    <span data-ttu-id="29030-304">![스 캐 폴딩 사용 하 여 웹 API 컨트롤러 추가](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image25.png "스 캐 폴딩 사용 하 여 Web API 컨트롤러 추가")</span><span class="sxs-lookup"><span data-stu-id="29030-304">![Adding a Web API Controller with scaffolding](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image25.png "Adding a Web API controller with scaffolding")</span></span>

    <span data-ttu-id="29030-305">*스 캐 폴딩 사용 하 여 Web API 컨트롤러 추가*</span><span class="sxs-lookup"><span data-stu-id="29030-305">*Adding a Web API controller with scaffolding*</span></span>
5. <span data-ttu-id="29030-306">Visual Studio에서 생성 한 다음 합니다 **ApiPersonController** 데이터와 함께 작동 하도록 4 개의 CRUD 동작이 포함 된 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-306">Visual Studio will then generate the **ApiPersonController** class with the four CRUD actions to work with your data.</span></span>

    <span data-ttu-id="29030-307">![Web API 컨트롤러 스 캐 폴딩을 사용 하 여 만들었으면](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image26.png "Web API 컨트롤러 스 캐 폴딩을 사용 하 여 만든 후")</span><span class="sxs-lookup"><span data-stu-id="29030-307">![After creating the Web API controller with scaffolding](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image26.png "After creating the Web API controller with scaffolding")</span></span>

    <span data-ttu-id="29030-308">*Web API 컨트롤러 스 캐 폴딩을 사용 하 여 만든 후*</span><span class="sxs-lookup"><span data-stu-id="29030-308">*After creating the Web API controller with scaffolding*</span></span>
6. <span data-ttu-id="29030-309">열기는 **ApiPersonController.cs** 파일을 검사 합니다 *GetPeople* 작업 메서드.</span><span class="sxs-lookup"><span data-stu-id="29030-309">Open the **ApiPersonController.cs** file and inspect the *GetPeople* action method.</span></span> <span data-ttu-id="29030-310">이 메서드는 db 필드 쿼리 **PersonContext** 사용자 데이터를 가져오기 위해 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-310">This method queries the db field of **PersonContext** type in order to get the people data.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample5.cs)]
7. <span data-ttu-id="29030-311">이제 메서드 정의 위의 설명을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29030-311">Now notice the comment above the method definition.</span></span> <span data-ttu-id="29030-312">다음 태스크에서 사용 하는이 작업을 노출 하는 URI를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-312">It provides the URI that exposes this action which you will use in the next task.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample6.cs)]

    > [!NOTE]
    > <span data-ttu-id="29030-313">기본적으로 웹 API가 catch에 대 한 쿼리로 구성 된 */a p i* MVC 컨트롤러를 사용 하 여 충돌을 방지 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-313">By default, Web API is configured to catch the queries to the */api* path to avoid collisions with MVC controllers.</span></span> <span data-ttu-id="29030-314">이 설정을 변경 해야 할 경우 가리킵니다 [ASP.NET Web API에서 라우팅](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-314">If you need to change this setting, refer to [Routing in ASP.NET Web API](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

<a id="Ex3Task2"></a>
#### <a name="task-2--running-the-solution"></a><span data-ttu-id="29030-315">작업 2-솔루션 실행</span><span class="sxs-lookup"><span data-stu-id="29030-315">Task 2 – Running the Solution</span></span>

<span data-ttu-id="29030-316">이 작업에서는 사용 하 여 Internet Explorer **F12 개발자 도구** Web API 컨트롤러에서 전체 응답을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-316">In this task you will use the Internet Explorer **F12 developer tools** to inspect the full response from the Web API controller.</span></span> <span data-ttu-id="29030-317">응용 프로그램 데이터에 대 한 자세한 정보를 가져오려는 네트워크 트래픽을 캡처할 수 있습니다 하는 방법을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29030-317">You will see how you can capture network traffic to get more insight into your application data.</span></span>

> [!NOTE]
> <span data-ttu-id="29030-318">했는지 **Internet Explorer** 가 선택 합니다 **시작** Visual Studio 도구 모음에 있는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-318">Make sure that **Internet Explorer** is selected in the **Start** button located on the Visual Studio toolbar.</span></span>
> 
> ![Internet Explorer 옵션](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image27.png)
> 
> <span data-ttu-id="29030-320">합니다 **F12 개발자 도구** 와이드이 실습 랩에 적용 되지 않는 기능 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29030-320">The **F12 developer tools** have a wide set of functionality that is not covered in this hands-on-lab.</span></span> <span data-ttu-id="29030-321">자세한 내용을 원한다 면 가리킵니다 [F12 개발자 도구를 사용 하 여](https://msdn.microsoft.com/library/ie/bg182326(v=vs.85))입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-321">If you want to learn more about it, refer to [Using the F12 developer tools](https://msdn.microsoft.com/library/ie/bg182326(v=vs.85)).</span></span>


1. <span data-ttu-id="29030-322">키를 눌러 **F5** 솔루션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-322">Press **F5** to run the solution.</span></span>

    > [!NOTE]
    > <span data-ttu-id="29030-323">이 작업을 올바르게 수행 하려면 응용 프로그램에 데이터가 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-323">In order to follow this task correctly, your application needs to have data.</span></span> <span data-ttu-id="29030-324">데이터베이스가 비어 있는 경우 연습 2에서 작업 3으로 돌아가서 하 수 MVC 뷰를 사용 하 여 새 사용자를 만드는 방법의 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-324">If your database is empty, you can go back to Task 3 in Exercise 2 and follow the steps on how to create a new person using the MVC views.</span></span>
2. <span data-ttu-id="29030-325">키를 눌러 브라우저에서 **F12** 열려는 합니다 **개발자 도구** 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-325">In the browser, press **F12** to open the **Developer Tools** panel.</span></span> <span data-ttu-id="29030-326">키를 눌러 **CTRL** + **4** 누르거나를 **네트워크** 아이콘을 한 다음 단추를 클릭 하 고 녹색 화살표 네트워크 트래픽 캡처를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-326">Press **CTRL** + **4** or click the **Network** icon, and then click the green arrow button to begin capturing network traffic.</span></span>

    <span data-ttu-id="29030-327">![Web API 네트워크 캡처를 시작](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image28.png "Web API 시작 네트워크 캡처")</span><span class="sxs-lookup"><span data-stu-id="29030-327">![Initiating Web API network capture](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image28.png "Initiating Web API network capture")</span></span>

    <span data-ttu-id="29030-328">*Web API 네트워크 캡처를 시작합니다.*</span><span class="sxs-lookup"><span data-stu-id="29030-328">*Initiating Web API network capture*</span></span>
3. <span data-ttu-id="29030-329">추가 **api/ApiPerson** 브라우저의 주소 표시줄에서 URL로 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-329">Append **api/ApiPerson** to the URL in the browser's address bar.</span></span> <span data-ttu-id="29030-330">이제 응답의 세부 정보를 검사 하는 합니다 **ApiPersonController**합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-330">You will now inspect the details of the response from the **ApiPersonController**.</span></span>

    <span data-ttu-id="29030-331">![웹 API를 통해 사용자 데이터를 검색할](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image29.png "웹 API를 통해 사용자 데이터를 검색 합니다.")</span><span class="sxs-lookup"><span data-stu-id="29030-331">![Retrieving person data through Web API](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image29.png "Retrieving person data through Web API")</span></span>

    <span data-ttu-id="29030-332">*웹 API를 통해 사용자 데이터를 검색합니다.*</span><span class="sxs-lookup"><span data-stu-id="29030-332">*Retrieving person data through Web API*</span></span>

    > [!NOTE]
    > <span data-ttu-id="29030-333">다운로드가 완료 되 면 다운로드 한 파일을 사용 하 여 작업을 할 수 있도록 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="29030-333">Once the download finishes, you will be prompted to make an action with the downloaded file.</span></span> <span data-ttu-id="29030-334">대화 상자는 개발자 도구 창을 통해 응답 콘텐츠를 볼 수 있도록 열어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="29030-334">Leave the dialog box open in order to be able to watch the response content through the Developers Tool window.</span></span>
4. <span data-ttu-id="29030-335">이제는 응답의 본문을 조사 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-335">Now you will inspect the body of the response.</span></span> <span data-ttu-id="29030-336">이렇게 하려면 클릭 합니다 **세부 정보** 탭을 클릭 한 다음 **응답 본문**합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-336">To do this, click the **Details** tab and then click **Response body**.</span></span> <span data-ttu-id="29030-337">다운로드 한 데이터는 속성을 사용 하 여 개체의 목록을 확인할 수 있습니다 **Id**, **이름** 및 **Age** 에 해당 하는 **사용자** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-337">You can check that the downloaded data is a list of objects with the properties **Id**, **Name** and **Age** that correspond to the **Person** class.</span></span>

    <span data-ttu-id="29030-338">![보기 웹 API 응답 본문이](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image30.png "보기 웹 API 응답 본문")</span><span class="sxs-lookup"><span data-stu-id="29030-338">![Viewing Web API Response Body](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image30.png "Viewing Web API Response Body")</span></span>

    <span data-ttu-id="29030-339">*웹 API 응답 본문 보기*</span><span class="sxs-lookup"><span data-stu-id="29030-339">*Viewing Web API Response Body*</span></span>

<a id="Ex3Task3"></a>
#### <a name="task-3--adding-web-api-help-pages"></a><span data-ttu-id="29030-340">작업 3 – Web API 도움말 페이지 추가</span><span class="sxs-lookup"><span data-stu-id="29030-340">Task 3 – Adding Web API Help Pages</span></span>

<span data-ttu-id="29030-341">Web API를 만들 때 다른 개발자가 API를 호출 하는 방법을 알 수 있도록 도움말 페이지를 만드는 것이 유용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-341">When you create a Web API, it is useful to create a help page so that other developers will know how to call your API.</span></span> <span data-ttu-id="29030-342">만들고 설명서 페이지를 수동으로 업데이트할 수 있지만 유지 관리 작업을 수행할 것을 방지 하도록 자동으로 생성 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="29030-342">You could create and update the documentation pages manually, but it is better to auto-generate them to avoid having to do maintenance work.</span></span> <span data-ttu-id="29030-343">이 작업에서는 솔루션에 Web API 도움말 페이지를 자동으로 생성 하는 Nuget 패키지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-343">In this task you will use a Nuget package to automatically generate Web API help pages to the solution.</span></span>

1. <span data-ttu-id="29030-344">**도구** Visual Studio에서 메뉴 **라이브러리 패키지 관리자**를 클릭 하 고 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-344">From the **Tools** menu in Visual Studio, select **Library Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="29030-345">에 **패키지 관리자 콘솔** 창에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-345">In the **Package Manager Console** window, execute the following command:</span></span>

    [!code-powershell[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample7.ps1)]

    > [!NOTE]
    > <span data-ttu-id="29030-346">**Microsoft.AspNet.WebApi.HelpPage** 패키지는 필요한 어셈블리를 설치 하 고 아래에 있는 도움말 페이지에 대 한 MVC 뷰를 추가 합니다 **영역/HelpPage** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-346">The **Microsoft.AspNet.WebApi.HelpPage** package installs the necessary assemblies and adds MVC Views for the help pages under the **Areas/HelpPage** folder.</span></span>

    <span data-ttu-id="29030-347">![HelpPage 영역](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image31.png "HelpPage 영역")</span><span class="sxs-lookup"><span data-stu-id="29030-347">![HelpPage Area](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image31.png "HelpPage Area")</span></span>

    <span data-ttu-id="29030-348">*HelpPage 영역*</span><span class="sxs-lookup"><span data-stu-id="29030-348">*HelpPage Area*</span></span>
3. <span data-ttu-id="29030-349">기본적으로 도움말 페이지에 설명서에 대 한 자리 표시자 문자열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-349">By default, the help pages have placeholder strings for documentation.</span></span> <span data-ttu-id="29030-350">문서를 만들려면 XML 문서 주석을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29030-350">You can use XML documentation comments to create the documentation.</span></span> <span data-ttu-id="29030-351">이 기능을 사용 하려면 엽니다는 **HelpPageConfig.cs** 에 있는 파일을 **영역/HelpPage/앱\_시작** 폴더 다음 줄을 주석 처리 제거:</span><span class="sxs-lookup"><span data-stu-id="29030-351">To enable this feature, open the **HelpPageConfig.cs** file located in the **Areas/HelpPage/App\_Start** folder and uncomment the following line:</span></span>

    [!code-javascript[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample8.js)]
4. <span data-ttu-id="29030-352">**솔루션 탐색기**, 프로젝트를 마우스 오른쪽 단추로 클릭 **MyHybridSite**를 선택 **속성** 을 클릭 합니다 **빌드** 탭.</span><span class="sxs-lookup"><span data-stu-id="29030-352">In **Solution Explorer**, right-click the project **MyHybridSite**, select **Properties** and click the **Build** tab.</span></span>

    <span data-ttu-id="29030-353">![빌드 탭](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image32.png "빌드 섹션")</span><span class="sxs-lookup"><span data-stu-id="29030-353">![Build tab](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image32.png "Build section")</span></span>

    <span data-ttu-id="29030-354">*빌드 탭*</span><span class="sxs-lookup"><span data-stu-id="29030-354">*Build tab*</span></span>
5. <span data-ttu-id="29030-355">아래 **출력**를 선택 **XML 문서 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-355">Under **Output**, select **XML documentation file**.</span></span> <span data-ttu-id="29030-356">편집 상자에 입력 **앱\_Data/XmlDocument.xml**합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-356">In the edit box, type **App\_Data/XmlDocument.xml**.</span></span>

    <span data-ttu-id="29030-357">![출력 섹션의 빌드 탭](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image33.png "출력 섹션의 빌드 탭")</span><span class="sxs-lookup"><span data-stu-id="29030-357">![Output section in Build tab](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image33.png "Output section in build tab")</span></span>

    <span data-ttu-id="29030-358">*빌드 탭에서 출력 섹션*</span><span class="sxs-lookup"><span data-stu-id="29030-358">*Output section in Build tab*</span></span>
6. <span data-ttu-id="29030-359">키를 눌러 **CTRL** + **S** 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-359">Press **CTRL** + **S** to save the changes.</span></span>
7. <span data-ttu-id="29030-360">엽니다는 **ApiPersonController.cs** 에서 파일을 **컨트롤러** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-360">Open the **ApiPersonController.cs** file from the **Controllers** folder.</span></span>
8. <span data-ttu-id="29030-361">간의 새 줄을 입력 합니다 *GetPeople* 메서드 시그니처 및 */ / api/ApiPerson GET* 주석 처리 한 다음 3 개의 슬래시를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-361">Enter a new line between the *GetPeople* method signature and the *// GET api/ApiPerson* comment, and then type three forward slashes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="29030-362">Visual Studio는 자동으로 메서드 설명서를 정의 하는 XML 요소를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-362">Visual Studio automatically inserts the XML elements which define the method documentation.</span></span>
9. <span data-ttu-id="29030-363">요약 텍스트 및 반환 값을 추가 합니다 *GetPeople* 메서드.</span><span class="sxs-lookup"><span data-stu-id="29030-363">Add a summary text and the return value for the *GetPeople* method.</span></span> <span data-ttu-id="29030-364">다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29030-364">It should look like the following.</span></span>

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample9.cs)]
10. <span data-ttu-id="29030-365">키를 눌러 **F5** 솔루션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-365">Press **F5** to run the solution.</span></span>
11. <span data-ttu-id="29030-366">추가 **/help** 도움말 페이지로 이동할 주소 표시줄에서 URL로 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-366">Append **/help** to the URL in the address bar to browse to the help page.</span></span>

    <span data-ttu-id="29030-367">![ASP.NET Web API 도움말 페이지](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image34.png "ASP.NET Web API 도움말 페이지")</span><span class="sxs-lookup"><span data-stu-id="29030-367">![ASP.NET Web API Help Page](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image34.png "ASP.NET Web API Help Page")</span></span>

    <span data-ttu-id="29030-368">*ASP.NET Web API 도움말 페이지*</span><span class="sxs-lookup"><span data-stu-id="29030-368">*ASP.NET Web API Help Page*</span></span>

    > [!NOTE]
    > <span data-ttu-id="29030-369">페이지의 주요 내용에는 api, 컨트롤러 별로 그룹화 된 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-369">The main content of the page is a table of APIs, grouped by controller.</span></span> <span data-ttu-id="29030-370">사용 하 여 테이블 항목을 동적으로 생성 합니다 **IApiExplorer** 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="29030-370">The table entries are generated dynamically, using the **IApiExplorer** interface.</span></span> <span data-ttu-id="29030-371">를 추가 하거나 API 컨트롤러를 업데이트 하는 경우 테이블 자동으로 업데이트 됩니다 다음에 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-371">If you add or update an API controller, the table will be automatically updated the next time you build the application.</span></span>
    > 
    > <span data-ttu-id="29030-372">합니다 **API** 열에는 HTTP 메서드 및 상대 URI를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-372">The **API** column lists the HTTP method and relative URI.</span></span> <span data-ttu-id="29030-373">합니다 **설명을** 열 메서드의 설명서에서 추출 된 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-373">The **Description** column contains information that has been extracted from the method's documentation.</span></span>
12. <span data-ttu-id="29030-374">메서드 정의 위에 추가 설명을 참고 설명 열에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29030-374">Note that the description you added above the method definition is displayed in the description column.</span></span>

    <span data-ttu-id="29030-375">![API 메서드 설명을](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image35.png "API 메서드 설명")</span><span class="sxs-lookup"><span data-stu-id="29030-375">![API method description](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image35.png "API method description")</span></span>

    <span data-ttu-id="29030-376">*API 메서드 설명*</span><span class="sxs-lookup"><span data-stu-id="29030-376">*API method description*</span></span>
13. <span data-ttu-id="29030-377">샘플 응답 본문을 포함 하 여 자세한 정보를 사용 하 여 페이지로 이동 하는 API 방법 중 하나를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-377">Click one of the API methods to navigate to a page with more detailed information, including sample response bodies.</span></span>

    <span data-ttu-id="29030-378">![세부 정보 페이지](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image36.png "세부 정보 페이지")</span><span class="sxs-lookup"><span data-stu-id="29030-378">![Detail Information page](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image36.png "Detail Information page")</span></span>

    <span data-ttu-id="29030-379">*세부 정보 페이지*</span><span class="sxs-lookup"><span data-stu-id="29030-379">*Detailed information page*</span></span>

* * *

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="29030-380">요약</span><span class="sxs-lookup"><span data-stu-id="29030-380">Summary</span></span>

<span data-ttu-id="29030-381">이 실습을 완료 하 여 배웠습니다 방법:</span><span class="sxs-lookup"><span data-stu-id="29030-381">By completing this hands-on lab you have learned how to:</span></span>

- <span data-ttu-id="29030-382">하나는 ASP.NET 환경을 사용 하 여 Visual Studio 2013에서 새 웹 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="29030-382">Create a new Web application using the One ASP.NET Experience in Visual Studio 2013</span></span>
- <span data-ttu-id="29030-383">하나의 단일 프로젝트에 여러 ASP.NET 기술을 통합합니다</span><span class="sxs-lookup"><span data-stu-id="29030-383">Integrate multiple ASP.NET technologies into one single project</span></span>
- <span data-ttu-id="29030-384">ASP.NET 스 캐 폴딩을 사용 하 여 모델 클래스에서 MVC 컨트롤러 및 뷰를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-384">Generate MVC controllers and views from your model classes using ASP.NET Scaffolding</span></span>
- <span data-ttu-id="29030-385">비동기 프로그래밍 및 Entity Framework를 통해 데이터 액세스와 같은 기능을 사용 하는 Web API 컨트롤러를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="29030-385">Generate Web API controllers, which use features such as Async Programming and data access through Entity Framework</span></span>
- <span data-ttu-id="29030-386">컨트롤러에 대 한 Web API 도움말 페이지를 자동으로 생성</span><span class="sxs-lookup"><span data-stu-id="29030-386">Automatically generate Web API Help Pages for your controllers</span></span>
