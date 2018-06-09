---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
title: ASP.NET MVC 4 도우미, 폼 및 유효성 검사 | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4 모델 및 데이터 액세스 실습 랩 하면 로드 되어 데이터베이스에서 데이터를 표시 합니다. 에 추가 합니다이 실습 랩에서 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 187ee9cd-bc70-479b-bfed-f568b8da96eb
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
msc.type: authoredcontent
ms.openlocfilehash: 4cfa98144919c3f1bdb3608970af1a7952fe6ea7
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2018
ms.locfileid: "30878180"
---
# <a name="aspnet-mvc-4-helpers-forms-and-validation"></a><span data-ttu-id="4cf50-104">ASP.NET MVC 4 도우미, 폼 및 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="4cf50-104">ASP.NET MVC 4 Helpers, Forms and Validation</span></span>

<span data-ttu-id="4cf50-105">으로 [웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="4cf50-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="4cf50-106">웹 캠프 학습 키트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="4cf50-107">**ASP.NET MVC 4 모델 및 데이터 액세스** 실습 랩 되었습니다 로드 하 고 데이터베이스에서 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-107">In **ASP.NET MVC 4 Models and Data Access** Hands-on Lab, you have been loading and displaying data from the database.</span></span> <span data-ttu-id="4cf50-108">에 추가 합니다이 실습 랩에서 **Music Store** 응용 프로그램이 해당 데이터를 편집할 수 있는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-108">In this Hands-on Lab, you will add to the **Music Store** application the ability to edit that data.</span></span>

<span data-ttu-id="4cf50-109">해당 목표를 염두에서에 두고 앨범의 만들기, 읽기, 업데이트 및 삭제 (CRUD) 작업을 지 원하는 컨트롤러는 먼저 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-109">With that goal in mind, you will first create the controller that will support the Create, Read, Update and Delete (CRUD) actions of albums.</span></span> <span data-ttu-id="4cf50-110">HTML 표에 앨범 속성을 표시 하려면 ASP.NET MVC 스 캐 폴딩 기능을 활용 하는 인덱스 뷰 서식 파일을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-110">You will generate an Index View template taking advantage of ASP.NET MVC's scaffolding feature to display the albums' properties in an HTML table.</span></span> <span data-ttu-id="4cf50-111">해당 보기를 강화 하려면 긴 설명을 잘립니다 하는 사용자 지정 HTML 도우미를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-111">To enhance that view, you will add a custom HTML helper that will truncate long descriptions.</span></span>

<span data-ttu-id="4cf50-112">그 후에 편집 하며 수 있는 뷰 만들기 alter 앨범 드롭다운 같은 폼 요소를 사용 하 여 데이터베이스에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-112">Afterwards, you will add the Edit and Create Views that will let you alter the albums in the database, with the help of form elements like dropdowns.</span></span>

<span data-ttu-id="4cf50-113">마지막으로, 앨범을 삭제 하는 사용자 수와 있습니다 됩니다 수 없게 입력을 확인 하 여 잘못 된 데이터를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-113">Lastly, you will let users delete an album and also you will prevent them from entering wrong data by validating their input.</span></span>

<span data-ttu-id="4cf50-114">이 실습 랩 대 한 기본 지식이 있다고 가정 하 고 **ASP.NET MVC**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-114">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="4cf50-115">사용 하지 않은 경우 **ASP.NET MVC** 를 권장 앞, **ASP.NET MVC의 기본 사항** 실습 랩입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-115">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC Fundamentals** Hands-on Lab.</span></span>

<span data-ttu-id="4cf50-116">이 랩에서 원본 폴더에 제공 된 샘플 웹 응용 프로그램에 사소한 변경 내용을 적용 하 여 이전에 설명 된 새로운 기능 및 향상 된 기능을 통해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-116">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>

> [!NOTE]
> <span data-ttu-id="4cf50-117">모든 샘플 코드와 코드 조각을 웹 캠프 교육 키트에서 사용할 수에 포함 된 [Microsoft-웹/WebCampTrainingKit 릴리스](https://aka.ms/webcamps-training-kit)합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-117">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="4cf50-118">이 랩에 특정 프로젝트에서 사용할 수는 [ASP.NET MVC 4 도우미, 폼 및 유효성 검사](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation)합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-118">The project specific to this lab is available at [ASP.NET MVC 4 Helpers, Forms and Validation](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="4cf50-119">목표</span><span class="sxs-lookup"><span data-stu-id="4cf50-119">Objectives</span></span>

<span data-ttu-id="4cf50-120">이 실습 랩에서 배우게 됩니다 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="4cf50-120">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="4cf50-121">CRUD 작업을 지 원하는 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="4cf50-121">Create a controller to support CRUD operations</span></span>
- <span data-ttu-id="4cf50-122">HTML 테이블에 엔터티 속성을 표시 하는 인덱스 뷰를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-122">Generate an Index View to display entity properties in an HTML table</span></span>
- <span data-ttu-id="4cf50-123">사용자 지정 HTML 도우미를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-123">Add a custom HTML helper</span></span>
- <span data-ttu-id="4cf50-124">만들기 및 편집 보기를 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="4cf50-124">Create and customize an Edit View</span></span>
- <span data-ttu-id="4cf50-125">HTTP GET 또는 HTTP POST 호출에 반응 하는 작업 메서드를 구별</span><span class="sxs-lookup"><span data-stu-id="4cf50-125">Differentiate between action methods that react to either HTTP-GET or HTTP-POST calls</span></span>
- <span data-ttu-id="4cf50-126">추가 및 Create View를 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="4cf50-126">Add and customize a Create View</span></span>
- <span data-ttu-id="4cf50-127">엔터티 삭제 처리</span><span class="sxs-lookup"><span data-stu-id="4cf50-127">Handle the deletion of an entity</span></span>
- <span data-ttu-id="4cf50-128">사용자 입력 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="4cf50-128">Validate user input</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="4cf50-129">전제 조건</span><span class="sxs-lookup"><span data-stu-id="4cf50-129">Prerequisites</span></span>

<span data-ttu-id="4cf50-130">이 랩을 완료 하려면 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-130">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="4cf50-131">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) 하거나 그 보다 뛰어난 (읽기 [부록 A](#AppendixA) 설치 하는 방법에 대 한 지침은).</span><span class="sxs-lookup"><span data-stu-id="4cf50-131">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="4cf50-132">설정</span><span class="sxs-lookup"><span data-stu-id="4cf50-132">Setup</span></span>

<span data-ttu-id="4cf50-133">**설치 하는 코드 조각**</span><span class="sxs-lookup"><span data-stu-id="4cf50-133">**Installing Code Snippets**</span></span>

<span data-ttu-id="4cf50-134">편의 위해는이 랩에 따라 관리 코드의 대부분 Visual Studio 코드 조각 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-134">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="4cf50-135">실행 코드 조각을 설치 하려면 **.\Source\Setup\CodeSnippets.vsi** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-135">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="4cf50-136">이 문서에서 부록을 참조할 수 사용 하는 방법에 알아봅니다 사용 하 고 Visual Studio 코드 조각에 익숙한 경우 &quot; [부록 b:를 사용 하 여 코드 조각을](#AppendixB)&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-136">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="4cf50-137">연습</span><span class="sxs-lookup"><span data-stu-id="4cf50-137">Exercises</span></span>

<span data-ttu-id="4cf50-138">다음 연습 실습 랩이를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-138">The following exercises make up this Hands-On Lab:</span></span>

1. [<span data-ttu-id="4cf50-139">저장소 관리자 컨트롤러 및 해당 인덱스 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="4cf50-139">Creating the Store Manager controller and its Index view</span></span>](#Exercise1)
2. [<span data-ttu-id="4cf50-140">HTML 도우미를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-140">Adding an HTML Helper</span></span>](#Exercise2)
3. [<span data-ttu-id="4cf50-141">편집 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="4cf50-141">Creating the Edit View</span></span>](#Exercise3)
4. [<span data-ttu-id="4cf50-142">만들기 뷰 추가</span><span class="sxs-lookup"><span data-stu-id="4cf50-142">Adding a Create View</span></span>](#Exercise4)
5. [<span data-ttu-id="4cf50-143">삭제를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-143">Handling Deletion</span></span>](#Exercise5)
6. [<span data-ttu-id="4cf50-144">유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="4cf50-144">Adding Validation</span></span>](#Exercise6)
7. [<span data-ttu-id="4cf50-145">클라이언트 쪽에서 비 가시적인 jQuery를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="4cf50-145">Using Unobtrusive jQuery at Client Side</span></span>](#Exercise7)

> [!NOTE]
> <span data-ttu-id="4cf50-146">각 연습 동반 되는 **끝** 연습을 완료 한 후 가져와야 생성 되는 솔루션에 포함 된 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-146">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="4cf50-147">연습을 통해 작업 하는 추가 도움이 필요한 경우이 솔루션 가이드로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-147">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<span data-ttu-id="4cf50-148">예상 소요 시간: **60 분**</span><span class="sxs-lookup"><span data-stu-id="4cf50-148">Estimated time to complete this lab: **60 minutes**</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_the_Store_Manager_controller_and_its_Index_view"></a>
### <a name="exercise-1-creating-the-store-manager-controller-and-its-index-view"></a><span data-ttu-id="4cf50-149">연습 1: 저장소 관리자 컨트롤러 및 해당 인덱스 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="4cf50-149">Exercise 1: Creating the Store Manager controller and its Index view</span></span>

<span data-ttu-id="4cf50-150">이 연습에서는 데이터베이스와 마지막으로 ASP.NET MVC 스 캐 폴딩을 활용 하는 인덱스 뷰 서식 파일 생성 중에서 앨범의 목록을 반환 하는 인덱스 작업 메서드를 사용자 지정을 CRUD 작업을 지원 하려면 새 컨트롤러를 만드는 방법을 배우게 됩니다. HTML 표에 앨범 속성을 표시 하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-150">In this exercise, you will learn how to create a new controller to support CRUD operations, customize its Index action method to return a list of albums from the database and finally generating an Index View template taking advantage of ASP.NET MVC's scaffolding feature to display the albums' properties in an HTML table.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_StoreManagerController"></a>
#### <a name="task-1---creating-the-storemanagercontroller"></a><span data-ttu-id="4cf50-151">작업 1-는 StoreManagerController 만들기</span><span class="sxs-lookup"><span data-stu-id="4cf50-151">Task 1 - Creating the StoreManagerController</span></span>

<span data-ttu-id="4cf50-152">이 작업을 호출 하는 새 컨트롤러 만듭니다 **StoreManagerController** CRUD 작업을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-152">In this task, you will create a new controller called **StoreManagerController** to support CRUD operations.</span></span>

1. <span data-ttu-id="4cf50-153">열기는 **시작** 솔루션에 있는 **소스/e x 1-CreatingTheStoreManagerController/시작/** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-153">Open the **Begin** solution located at **Source/Ex1-CreatingTheStoreManagerController/Begin/** folder.</span></span>

   1. <span data-ttu-id="4cf50-154">일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 전에 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-154">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="4cf50-155">이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-155">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="4cf50-156">에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="4cf50-156">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="4cf50-157">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-157">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="4cf50-158">NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-158">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="4cf50-159">NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-159">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="4cf50-160">이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-160">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="4cf50-161">새 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-161">Add a new controller.</span></span> <span data-ttu-id="4cf50-162">이렇게 하려면 마우스 오른쪽 단추로 클릭는 **컨트롤러** 선택 솔루션 탐색기에서 폴더 **추가** 차례로 **컨트롤러** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-162">To do this, right-click the **Controllers** folder within the Solution Explorer, select **Add** and then the **Controller** command.</span></span> <span data-ttu-id="4cf50-163">변경 된 **컨트롤러** **이름** 를 **StoreManagerController** 옵션 있는지 확인 하 고 **빈읽기/쓰기동작이포함된MVC컨트롤러**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-163">Change the **Controller** **Name** to **StoreManagerController** and make sure the option **MVC controller with empty read/write actions** is selected.</span></span> <span data-ttu-id="4cf50-164">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-164">Click **Add**.</span></span>

    <span data-ttu-id="4cf50-165">![추가 컨트롤러 대화](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "추가 컨트롤러 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="4cf50-165">![Add controller dialog](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "Add controller dialog")</span></span>

    <span data-ttu-id="4cf50-166">*컨트롤러 추가 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="4cf50-166">*Add Controller Dialog*</span></span>

    <span data-ttu-id="4cf50-167">새 컨트롤러 클래스가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-167">A new Controller class is generated.</span></span> <span data-ttu-id="4cf50-168">스텁 메서드,에 대 한 읽기/쓰기에 대 한 작업을 추가 하려면 표시 된 이후 응용 프로그램별 논리를 포함 하는 메시지를 입력할 TODO 주석을 사용 하 여 일반적인 위한 CRUD 동작이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-168">Since you indicated to add actions for read/write, stub methods for those, common CRUD actions are created with TODO comments filled in, prompting to include the application specific logic.</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Customizing_the_StoreManager_Index"></a>
#### <a name="task-2---customizing-the-storemanager-index"></a><span data-ttu-id="4cf50-169">작업 2-StoreManager 인덱스를 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="4cf50-169">Task 2 - Customizing the StoreManager Index</span></span>

<span data-ttu-id="4cf50-170">이 작업에서는 데이터베이스에서 앨범 목록 사용 하 여 뷰를 반환 하기 StoreManager Index 동작 메서드를 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-170">In this task, you will customize the StoreManager Index action method to return a View with the list of albums from the database.</span></span>

1. <span data-ttu-id="4cf50-171">StoreManagerController 클래스에 다음 추가 *를 사용 하 여* 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-171">In the StoreManagerController class, add the following *using* directives.</span></span>

    <span data-ttu-id="4cf50-172">(코드 조각- *ASP.NET MVC 4 도우미와 폼과 유효성 검사-e x 1 MvcMusicStore를 사용 하 여*)</span><span class="sxs-lookup"><span data-stu-id="4cf50-172">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 using MvcMusicStore*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample1.cs)]
2. <span data-ttu-id="4cf50-173">필드를 추가 하는 **StoreManagerController** 의 인스턴스를 포함 하려면 **MusicStoreEntities 합니다.**</span><span class="sxs-lookup"><span data-stu-id="4cf50-173">Add a field to the **StoreManagerController** to hold an instance of **MusicStoreEntities.**</span></span>

    <span data-ttu-id="4cf50-174">(코드 조각- *ASP.NET MVC 4 도우미와 폼과 유효성 검사-e x 1 MusicStoreEntities*)</span><span class="sxs-lookup"><span data-stu-id="4cf50-174">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 MusicStoreEntities*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample2.cs)]
3. <span data-ttu-id="4cf50-175">앨범 목록 사용 하 여 뷰를 반환 하 여 StoreManagerController 인덱스 작업을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-175">Implement the StoreManagerController Index action to return a View with the list of albums.</span></span>

    <span data-ttu-id="4cf50-176">컨트롤러 동작 논리 매우 유사 StoreController의 인덱스 동작이 이전에 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-176">The Controller action logic will be very similar to the StoreController's Index action written earlier.</span></span> <span data-ttu-id="4cf50-177">LINQ를 사용 하 여 표시를 위해 Genre 및 음악가 정보를 포함 한 모든 앨범, 검색할.</span><span class="sxs-lookup"><span data-stu-id="4cf50-177">Use LINQ to retrieve all albums, including Genre and Artist information for display.</span></span>

    <span data-ttu-id="4cf50-178">(코드 조각- *ASP.NET MVC 4 도우미와 폼과 유효성 검사-e x 1 StoreManagerController 인덱스*)</span><span class="sxs-lookup"><span data-stu-id="4cf50-178">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 StoreManagerController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample3.cs)]

<a id="Ex1Task3"></a>

<a id="strongTask_3_-_Creating_the_Index_Viewstrong"></a>
#### <a name="task-3---creating-the-index-view"></a><span data-ttu-id="4cf50-179">작업 3-인덱스 보기를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="4cf50-179">Task 3 - Creating the Index View</span></span>

<span data-ttu-id="4cf50-180">이 태스크에서는에서 반환 되는 앨범의 목록을 표시 하려면 인덱스 뷰 템플릿을 만들어집니다는 **StoreManager** 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-180">In this task, you will create the Index View template to display the list of albums returned by the **StoreManager** Controller.</span></span>

1. <span data-ttu-id="4cf50-181">새 보기 서식 파일을 만들기 전에 프로젝트를 작성 해야 하는 **보기 대화 상자 추가** 에 대해 알고는 **앨범** 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-181">Before creating the new View template, you should build the project so that the **Add View Dialog** knows about the **Album** class to use.</span></span> <span data-ttu-id="4cf50-182">선택 **빌드 | 빌드 MvcMusicStore** 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-182">Select **Build | Build MvcMusicStore** to build the project.</span></span>
2. <span data-ttu-id="4cf50-183">마우스 오른쪽 단추로 클릭는 **인덱스** 동작 메서드와 선택 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-183">Right-click inside the **Index** action method and select **Add View**.</span></span> <span data-ttu-id="4cf50-184">그러면 표시 됩니다는 **뷰 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="4cf50-184">This will bring up the **Add View** dialog.</span></span>

    <span data-ttu-id="4cf50-185">![뷰 추가](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "뷰 추가")</span><span class="sxs-lookup"><span data-stu-id="4cf50-185">![Add view](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "Add view")</span></span>

    <span data-ttu-id="4cf50-186">*Index 메서드 내에서 뷰를 추가합니다.*</span><span class="sxs-lookup"><span data-stu-id="4cf50-186">*Adding a View from within the Index method*</span></span>
3. <span data-ttu-id="4cf50-187">뷰 추가 대화 상자에서 보기 이름 인지 확인 **인덱스**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-187">In the Add View dialog, verify that the View Name is **Index**.</span></span> <span data-ttu-id="4cf50-188">선택 된 **강력한 형식의 뷰 만들기** 옵션을 선택 **앨범 (MvcMusicStore.Models)** 에서 **모델 클래스** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-188">Select the **Create a strongly-typed view** option, and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down.</span></span> <span data-ttu-id="4cf50-189">선택 **목록** 에서 **스 캐 폴드 템플릿이** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-189">Select **List** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="4cf50-190">둡니다는 **뷰 엔진** 를 **Razor** 와 해당 기본값은 다른 필드 값을 클릭 한 다음 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-190">Leave the **View engine** to **Razor** and the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="4cf50-191">![인덱스 뷰 추가](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "인덱스 뷰 추가")</span><span class="sxs-lookup"><span data-stu-id="4cf50-191">![Adding an index view](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "Adding an index view")</span></span>

    <span data-ttu-id="4cf50-192">*인덱스 뷰 추가*</span><span class="sxs-lookup"><span data-stu-id="4cf50-192">*Adding an Index View*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Customizing_the_scaffold_of_the_Index_View"></a>
#### <a name="task-4---customizing-the-scaffold-of-the-index-view"></a><span data-ttu-id="4cf50-193">작업 4-인덱스 보기의 스 캐 폴드를 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="4cf50-193">Task 4 - Customizing the scaffold of the Index View</span></span>

<span data-ttu-id="4cf50-194">이 태스크에서는 원하는 필드를 표시 하도록 ASP.NET MVC 스 캐 폴딩 기능을 사용 하 여 만든 간단한 뷰 템플릿을 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-194">In this task, you will adjust the simple View template created with ASP.NET MVC scaffolding feature to have it display the fields you want.</span></span>

> [!NOTE]
> <span data-ttu-id="4cf50-195">**스 캐 폴딩** 앨범 모델의 모든 필드를 나열 하는 간단한 보기 서식 파일을 생성 하는 ASP.NET MVC 내에서 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-195">The **scaffolding** support within ASP.NET MVC generates a simple View template which lists all fields in the Album model.</span></span> <span data-ttu-id="4cf50-196">**스 캐 폴딩** 강력한 형식의 뷰에서 시작 하는 빠른 방법을 제공: 신속 하 게 스 캐 폴딩 템플릿 보기를 수동으로 작성 하는 대신 기본 템플릿을 생성 하 고 그런 다음 생성된 된 코드를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-196">**Scaffolding** provides a quick way to get started on a strongly typed view: rather than having to write the View template manually, scaffolding quickly generates a default template and then you can modify the generated code.</span></span>


1. <span data-ttu-id="4cf50-197">작성 한 코드를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-197">Review the code created.</span></span> <span data-ttu-id="4cf50-198">생성 된 필드 목록에는 다음의 일부가 될 HTML 테이블 **스 캐 폴딩** 표 형식 데이터를 표시 하기 위해 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-198">The generated list of fields will be part of the following HTML table that **Scaffolding** is using for displaying tabular data.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample4.cshtml)]
2. <span data-ttu-id="4cf50-199">대체는 **&lt;테이블&gt;** 만 표시 하는 다음 코드를 사용 하 여 코드의 **장르**, **아티스트**, **앨범 제목**, 및 **가격** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-199">Replace the **&lt;table&gt;** code with the following code to display only the **Genre**, **Artist**, **Album Title**, and **Price** fields.</span></span> <span data-ttu-id="4cf50-200">그러면 삭제는 **AlbumId** 및 **앨범 아트 URL** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-200">This deletes the **AlbumId** and **Album Art URL** columns.</span></span> <span data-ttu-id="4cf50-201">또한 해당 연결 된 클래스 속성을 표시 GenreId 및 ArtistId 열을 변경 **Artist.Name** 및 **Genre.Name**를 제거 하 고는 **세부 정보** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-201">Also, it changes GenreId and ArtistId columns to display their linked class properties of **Artist.Name** and **Genre.Name**, and removes the **Details** link.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample5.cshtml)]
3. <span data-ttu-id="4cf50-202">다음 설명을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-202">Change the following descriptions.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample6.cshtml)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="4cf50-203">5-응용 프로그램 실행 작업</span><span class="sxs-lookup"><span data-stu-id="4cf50-203">Task 5 - Running the Application</span></span>

<span data-ttu-id="4cf50-204">에서는이 작업을 테스트 하는 **StoreManager** **인덱스** 템플릿 보기에는 이전 단계의 디자인에 따라 앨범 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-204">In this task, you will test that the **StoreManager** **Index** View template displays a list of albums according to the design of the previous steps.</span></span>

1. <span data-ttu-id="4cf50-205">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-205">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="4cf50-206">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-206">The project starts in the Home page.</span></span> <span data-ttu-id="4cf50-207">URL을 변경 **/StoreManager** 보여 주는 목록이 앨범 표시 되는지 확인 하려면 해당 **제목**, **아티스트** 및 **장르**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-207">Change the URL to **/StoreManager** to verify that a list of albums is displayed, showing their **Title**, **Artist** and **Genre**.</span></span>

    <span data-ttu-id="4cf50-208">![앨범 목록을 찾는](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "앨범 목록 탐색")</span><span class="sxs-lookup"><span data-stu-id="4cf50-208">![Browsing the list of albums](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "Browsing the list of albums")</span></span>

    <span data-ttu-id="4cf50-209">*앨범 목록 탐색*</span><span class="sxs-lookup"><span data-stu-id="4cf50-209">*Browsing the list of albums*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Adding_an_HTML_Helper"></a>
### <a name="exercise-2-adding-an-html-helper"></a><span data-ttu-id="4cf50-210">연습 2: HTML 도우미를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-210">Exercise 2: Adding an HTML Helper</span></span>

<span data-ttu-id="4cf50-211">StoreManager 인덱스 페이지에 하나 이상의 잠재적인 문제가: 제목 및 아티스트 Name 속성은 모두 테이블 서식 지정에 충분 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-211">The StoreManager Index page has one potential issue: Title and Artist Name properties can both be long enough to throw off the table formatting.</span></span> <span data-ttu-id="4cf50-212">이 연습에서는 해당 텍스트를 잘라내려면 사용자 지정 HTML 도우미를 추가 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-212">In this exercise you will learn how to add a custom HTML helper to truncate that text.</span></span>

<span data-ttu-id="4cf50-213">다음 그림에는 작은 브라우저 크기를 사용 하는 경우 텍스트의 길이 때문에 형식이 수정 되는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-213">In the following figure, you can see how the format is modified because of the length of the text when you use a small browser size.</span></span>

<span data-ttu-id="4cf50-214">![잘린 텍스트와 앨범의 목록을 검색 하지](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "텍스트 잘리지 앨범으로 목록 검색")</span><span class="sxs-lookup"><span data-stu-id="4cf50-214">![Browsing the list of Albums with not truncated text](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "Browsing the list of Albums with not truncated text")</span></span>

<span data-ttu-id="4cf50-215">*텍스트 잘리지와 앨범 목록 탐색*</span><span class="sxs-lookup"><span data-stu-id="4cf50-215">*Browsing the list of Albums with not truncated text*</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Extending_the_HTML_Helper"></a>
#### <a name="task-1---extending-the-html-helper"></a><span data-ttu-id="4cf50-216">작업 1-확장 된 HTML 도우미</span><span class="sxs-lookup"><span data-stu-id="4cf50-216">Task 1 - Extending the HTML Helper</span></span>

<span data-ttu-id="4cf50-217">이 태스크에서는 새 메서드 추가 **Truncate** 에 **HTML** ASP.NET MVC 뷰 내에서 노출 된 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-217">In this task, you will add a new method **Truncate** to the **HTML** object exposed within ASP.NET MVC Views.</span></span> <span data-ttu-id="4cf50-218">이 수행 하려면 구현 합니다는 **확장 메서드** 기본 제공 되 **System.Web.Mvc.HtmlHelper** ASP.NET MVC에서 제공 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-218">To do this, you will implement an **extension method** to the built-in **System.Web.Mvc.HtmlHelper** class provided by ASP.NET MVC.</span></span>

> [!NOTE]
> <span data-ttu-id="4cf50-219">에 대 한 자세한 내용은 **확장 메서드**,이 msdn 문서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4cf50-219">To read more about **Extension Methods**, please visit this msdn article.</span></span> <span data-ttu-id="4cf50-220">[https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx).</span><span class="sxs-lookup"><span data-stu-id="4cf50-220">[https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx).</span></span>


1. <span data-ttu-id="4cf50-221">열기는 **시작** 솔루션에 있는 **소스/e x 2-AddingAnHTMLHelper/시작/** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-221">Open the **Begin** solution located at **Source/Ex2-AddingAnHTMLHelper/Begin/** folder.</span></span> <span data-ttu-id="4cf50-222">그렇지 않은 경우 계속 사용할 수도 있습니다는 **끝** 솔루션, 이전 연습을 완료 하 여 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-222">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="4cf50-223">제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면.</span><span class="sxs-lookup"><span data-stu-id="4cf50-223">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="4cf50-224">이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-224">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="4cf50-225">에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="4cf50-225">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="4cf50-226">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-226">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="4cf50-227">NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-227">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="4cf50-228">NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-228">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="4cf50-229">이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-229">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="4cf50-230">StoreManager의 인덱스 뷰를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-230">Open StoreManager's Index View.</span></span> <span data-ttu-id="4cf50-231">이렇게 하려면 솔루션 탐색기에서 확장 하 고는 **뷰** 폴더는 다음 **StoreManager** 엽니다는 **Index.cshtml** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-231">To do this, in the Solution Explorer expand the **Views** folder, then the **StoreManager** and open the **Index.cshtml** file.</span></span>
3. <span data-ttu-id="4cf50-232">아래에 다음 코드를 추가 <strong>@model</strong> 지시문을 정의 하는 <strong>Truncate</strong> 도우미 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-232">Add the following code below the <strong>@model</strong> directive to define the <strong>Truncate</strong> helper method.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample7.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Truncating_Text_in_the_Page"></a>
#### <a name="task-2---truncating-text-in-the-page"></a><span data-ttu-id="4cf50-233">작업 2-잘라내기가 텍스트 페이지</span><span class="sxs-lookup"><span data-stu-id="4cf50-233">Task 2 - Truncating Text in the Page</span></span>

<span data-ttu-id="4cf50-234">이 작업을 사용 하 여는 **Truncate** 템플릿 보기에에서 있는 텍스트를 잘라내려면 메서드.</span><span class="sxs-lookup"><span data-stu-id="4cf50-234">In this task, you will use the **Truncate** method to truncate the text in the View template.</span></span>

1. <span data-ttu-id="4cf50-235">StoreManager의 인덱스 뷰를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-235">Open StoreManager's Index View.</span></span> <span data-ttu-id="4cf50-236">이렇게 하려면 솔루션 탐색기에서 확장 하 고는 **뷰** 폴더는 다음 **StoreManager** 엽니다는 **Index.cshtml** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-236">To do this, in the Solution Explorer expand the **Views** folder, then the **StoreManager** and open the **Index.cshtml** file.</span></span>
2. <span data-ttu-id="4cf50-237">표시 된 줄을 바꿀는 **음악가 이름** 및 앨범 **제목**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-237">Replace the lines that show the **Artist Name** and Album's **Title**.</span></span> <span data-ttu-id="4cf50-238">이 작업을 수행 하려면 다음 줄을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-238">To do this, replace the following lines.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample8.cshtml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="4cf50-239">작업 3-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="4cf50-239">Task 3 - Running the Application</span></span>

<span data-ttu-id="4cf50-240">에서는이 작업을 테스트 하는 **StoreManager** **인덱스** 앨범의 제목 및 아티스트 이름 템플릿 보기를 자릅니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-240">In this task, you will test that the **StoreManager** **Index** View template truncates the Album's Title and Artist Name.</span></span>

1. <span data-ttu-id="4cf50-241">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-241">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="4cf50-242">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-242">The project starts in the Home page.</span></span> <span data-ttu-id="4cf50-243">URL을 변경 **/StoreManager** 해당 장기 확인 하려면 텍스트에는 **제목** 및 **아티스트** 열은 잘립니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-243">Change the URL to **/StoreManager** to verify that long texts in the **Title** and **Artist** column are truncated.</span></span>

    <span data-ttu-id="4cf50-244">![제목 및 예술가 이름이 잘립니다](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "잘린 제목과 예술가 이름")</span><span class="sxs-lookup"><span data-stu-id="4cf50-244">![Truncated titles and artists names](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "Truncated titles and artists names")</span></span>

    <span data-ttu-id="4cf50-245">*잘린 제목과 아티스트 이름*</span><span class="sxs-lookup"><span data-stu-id="4cf50-245">*Truncated Titles and Artist Names*</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Creating_the_Edit_View"></a>
### <a name="exercise-3-creating-the-edit-view"></a><span data-ttu-id="4cf50-246">연습 3: 편집 보기를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="4cf50-246">Exercise 3: Creating the Edit View</span></span>

<span data-ttu-id="4cf50-247">이 연습에서는 매장 관리자 앨범을 편집할 수 있도록 폼을 만드는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-247">In this exercise, you will learn how to create a form to allow store managers to edit an Album.</span></span> <span data-ttu-id="4cf50-248">찾아보기 됩니다는 **/StoreManager/Edit/id** URL (**id** 되 편집 하는 앨범의 고유 id), 서버에 대 한 HTTP GET 호출 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-248">They will browse the **/StoreManager/Edit/id** URL (**id** being the unique id of the album to edit), thus making an HTTP-GET call to the server.</span></span>

<span data-ttu-id="4cf50-249">컨트롤러 Edit 동작 메서드는 데이터베이스에서 적절 한 앨범 검색, 만들기는 **StoreManagerViewModel** 목록 아티스트, 장르), (함께 캡슐화 한 다음 보기 서식 파일에 전달할 개체 다시 사용자에 게 HTML 페이지를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-249">The Controller Edit action method will retrieve the appropriate Album from the database, create a **StoreManagerViewModel** object to encapsulate it (along with a list of Artists and Genres), and then pass it off to a View template to render the HTML page back to the user.</span></span> <span data-ttu-id="4cf50-250">이 페이지에 포함 됩니다는 **&lt;양식&gt;** 텍스트 상자 및 드롭다운 앨범 속성 편집에 있는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-250">This page will contain a **&lt;form&gt;** element with textboxes and dropdowns for editing the Album properties.</span></span>

<span data-ttu-id="4cf50-251">사용자 앨범 양식 값을 업데이트 하 고 클릭 한 후의 **저장** 의 변경 내용을 통해 제출 단추를 HTTP POST를 다시 호출 **/StoreManager/Edit/id**합니다. URL 마지막 호출에서와 동일 하 게 유지, 있지만 ASP.NET MVC 식별 하는 HTTP 게시 되 고 다른 편집 동작 메서드를 실행 하므로이 시간 (로 데코레이팅 하나 **[HttpPost]**).</span><span class="sxs-lookup"><span data-stu-id="4cf50-251">Once the user updates the Album form values and clicks the **Save** button, the changes are submitted via an HTTP-POST call back to **/StoreManager/Edit/id**. Although the URL remains the same as in the last call, ASP.NET MVC identifies that this time it is an HTTP-POST and therefore executes a different Edit action method (one decorated with **[HttpPost]**).</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Edit_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-edit-action-method"></a><span data-ttu-id="4cf50-252">작업 1-HTTP GET 편집 동작 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-252">Task 1 - Implementing the HTTP-GET Edit Action Method</span></span>

<span data-ttu-id="4cf50-253">이 작업에서는 HTTP GET 버전의 데이터베이스에서 적절 한 앨범을 가져오려는 편집 작업 메서드 뿐 아니라 모든 장르 및 예술가 목록을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-253">In this task, you will implement the HTTP-GET version of the Edit action method to retrieve the appropriate Album from the database, as well as a list of all Genres and Artists.</span></span> <span data-ttu-id="4cf50-254">로이 데이터 패키징하고 것은 **StoreManagerViewModel** 다음 응답을 렌더링 하는 보기 템플릿을에 전달 될는 마지막 단계에서 정의 된 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-254">It will package this data up into the **StoreManagerViewModel** object defined in the last step, which will then be passed to a View template to render the response with.</span></span>

1. <span data-ttu-id="4cf50-255">열기는 **시작** 솔루션에 있는 **소스/Ex3-CreatingTheEditView/시작/** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-255">Open the **Begin** solution located at **Source/Ex3-CreatingTheEditView/Begin/** folder.</span></span> <span data-ttu-id="4cf50-256">그렇지 않은 경우 계속 사용할 수도 있습니다는 **끝** 솔루션, 이전 연습을 완료 하 여 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-256">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="4cf50-257">제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면.</span><span class="sxs-lookup"><span data-stu-id="4cf50-257">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="4cf50-258">이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-258">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="4cf50-259">에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="4cf50-259">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="4cf50-260">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-260">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="4cf50-261">NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-261">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="4cf50-262">NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-262">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="4cf50-263">이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-263">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="4cf50-264">열기는 **StoreManagerController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-264">Open the **StoreManagerController** class.</span></span> <span data-ttu-id="4cf50-265">이 작업을 수행 하려면 확장 된 **컨트롤러** 폴더를 두 번 클릭 **StoreManagerController.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-265">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="4cf50-266">대체는 **HTTP GET 편집** 동작 메서드를 다음 코드로를 적절 한 검색 **앨범** 으로 **장르** 및 **예술가**나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-266">Replace the **HTTP-GET Edit** action method with the following code to retrieve the appropriate **Album** as well as the **Genres** and **Artists** lists.</span></span>

    <span data-ttu-id="4cf50-267">(코드 조각- *ASP.NET MVC 4 도우미와 폼 및 유효성 검사-작업 Ex3 StoreManagerController HTTP GET 편집*)</span><span class="sxs-lookup"><span data-stu-id="4cf50-267">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex3 StoreManagerController HTTP-GET Edit action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample9.cs)]

    > [!NOTE]
    > <span data-ttu-id="4cf50-268">사용 중인 **System.Web.Mvc** **SelectList** 아티스트, 대신 장르에 대 한는 **System.Collections.Generic** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-268">You are using **System.Web.Mvc** **SelectList** for Artists and Genres instead of the **System.Collections.Generic** List.</span></span>
    > 
    > <span data-ttu-id="4cf50-269">**SelectList** HTML 드롭다운 목록 채우기 등으로 현재 선택 영역을 관리 하는 보다 명확한 방법이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-269">**SelectList** is a cleaner way to populate HTML dropdowns and manage things like current selection.</span></span> <span data-ttu-id="4cf50-270">하 고 컨트롤러 작업에서 이러한 ViewModel 개체를 이상으로 설정 하면 편집 폼 시나리오 클리너 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-270">Instantiating and later setting up these ViewModel objects in the controller action will make the Edit form scenario cleaner.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Creating_the_Edit_View"></a>
#### <a name="task-2---creating-the-edit-view"></a><span data-ttu-id="4cf50-271">작업 2-편집 보기를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="4cf50-271">Task 2 - Creating the Edit View</span></span>

<span data-ttu-id="4cf50-272">이 태스크에서는 나중에 앨범 속성을 표시 하는 보기 편집 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-272">In this task, you will create an Edit View template that will later display the album properties.</span></span>

1. <span data-ttu-id="4cf50-273">편집 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-273">Create the Edit View.</span></span> <span data-ttu-id="4cf50-274">이렇게 하려면 마우스 오른쪽 단추로 클릭는 **편집** 동작 메서드와 선택 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-274">To do this, right-click inside the **Edit** action method and select **Add View**.</span></span>
2. <span data-ttu-id="4cf50-275">뷰 추가 대화 상자에서 보기 이름 인지 확인 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-275">In the Add View dialog, verify that the View Name is **Edit**.</span></span> <span data-ttu-id="4cf50-276">확인는 **강력한 형식의 뷰 만들기** 확인란을 선택 하 고 **앨범 (MvcMusicStore.Models)** 에서 **데이터 클래스 보기** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-276">Check the **Create a strongly-typed view** checkbox and select **Album (MvcMusicStore.Models)** from the **View data class** drop-down.</span></span> <span data-ttu-id="4cf50-277">선택 **편집** 에서 **스 캐 폴드 템플릿이** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-277">Select **Edit** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="4cf50-278">다른 필드를 기본값으로 두고 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-278">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="4cf50-279">![편집 뷰 추가](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "편집 뷰 추가")</span><span class="sxs-lookup"><span data-stu-id="4cf50-279">![Adding an Edit view](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "Adding an Edit view")</span></span>

    <span data-ttu-id="4cf50-280">*편집 뷰 추가*</span><span class="sxs-lookup"><span data-stu-id="4cf50-280">*Adding an Edit view*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="4cf50-281">작업 3-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="4cf50-281">Task 3 - Running the Application</span></span>

<span data-ttu-id="4cf50-282">에서는이 작업을 테스트 하는 **StoreManager** **편집** 보기 페이지에 매개 변수로 전달 된 앨범에 대 한 속성의 값이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-282">In this task, you will test that the **StoreManager** **Edit** View page displays the properties' values for the album passed as parameter.</span></span>

1. <span data-ttu-id="4cf50-283">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-283">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="4cf50-284">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-284">The project starts in the Home page.</span></span> <span data-ttu-id="4cf50-285">URL을 변경 **/StoreManager/Edit/1** 에 전달 된 앨범에 대 한 속성의 값이 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-285">Change the URL to **/StoreManager/Edit/1** to verify that the properties' values for the album passed are displayed.</span></span>

    <span data-ttu-id="4cf50-286">![앨범 편집 보기 찾아보기](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "앨범 편집 보기 찾아보기")</span><span class="sxs-lookup"><span data-stu-id="4cf50-286">![Browsing Album's Edit View](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "Browsing Album's Edit View")</span></span>

    <span data-ttu-id="4cf50-287">*앨범 편집 보기 찾아보기*</span><span class="sxs-lookup"><span data-stu-id="4cf50-287">*Browsing Album's Edit view*</span></span>

<a id="Ex3Task4"></a>

<a id="Task_4_-_Implementing_drop-downs_on_the_Album_Editor_Template"></a>
#### <a name="task-4---implementing-drop-downs-on-the-album-editor-template"></a><span data-ttu-id="4cf50-288">작업 4-앨범 편집기 서식 파일에서 구현 하는 드롭다운 목록</span><span class="sxs-lookup"><span data-stu-id="4cf50-288">Task 4 - Implementing drop-downs on the Album Editor Template</span></span>

<span data-ttu-id="4cf50-289">이 태스크에서는 추가 합니다 드롭다운 목록 마지막 작업에서 만든 템플릿 보기에 사용자 예술가 및 장르 목록에서 선택할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-289">In this task, you will add drop-downs to the View template created in the last task, so that the user can select from a list of Artists and Genres.</span></span>

1. <span data-ttu-id="4cf50-290">모두 바꾸기는 **앨범** 필드 집합 코드를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="4cf50-290">Replace all the **Album** fieldset code with the following:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample10.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="4cf50-291">**Html.DropDownList** 도우미 렌더링 아티스트, 장르 선택에 대 한 드롭다운 목록에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-291">An **Html.DropDownList** helper has been added to render drop-downs for choosing Artists and Genres.</span></span> <span data-ttu-id="4cf50-292">매개 변수가 전달 **Html.DropDownList** 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-292">The parameters passed to **Html.DropDownList** are:</span></span>
    > 
    > 1. <span data-ttu-id="4cf50-293">양식 필드의 이름 (**&quot;ArtistId&quot;**).</span><span class="sxs-lookup"><span data-stu-id="4cf50-293">The name of the form field (**&quot;ArtistId&quot;**).</span></span>
    > 2. <span data-ttu-id="4cf50-294">**SelectList** 드롭다운 목록에 대 한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-294">The **SelectList** of values for the drop-down.</span></span>

<a id="Ex3Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="4cf50-295">5-응용 프로그램 실행 작업</span><span class="sxs-lookup"><span data-stu-id="4cf50-295">Task 5 - Running the Application</span></span>

<span data-ttu-id="4cf50-296">에서는이 작업을 테스트 하는 **StoreManager** **편집** 보기 페이지 아티스트 및 장르 ID 텍스트 필드 대신 드롭다운 목록에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-296">In this task, you will test that the **StoreManager** **Edit** View page displays drop-downs instead of Artist and Genre ID text fields.</span></span>

1. <span data-ttu-id="4cf50-297">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-297">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="4cf50-298">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-298">The project starts in the Home page.</span></span> <span data-ttu-id="4cf50-299">URL을 변경 **/StoreManager/Edit/1** 아티스트 및 장르 ID 텍스트 필드 대신 드롭다운을 표시 되는지 확인 하려면.</span><span class="sxs-lookup"><span data-stu-id="4cf50-299">Change the URL to **/StoreManager/Edit/1** to verify that it displays drop-downs instead of Artist and Genre ID text fields.</span></span>

    <span data-ttu-id="4cf50-300">![검색 드롭다운 있는 앨범 편집 뷰](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "검색 앨범 드롭다운와 보기 편집")</span><span class="sxs-lookup"><span data-stu-id="4cf50-300">![Browsing Album's Edit View with drop downs](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "Browsing Album's Edit View with drop downs")</span></span>

    <span data-ttu-id="4cf50-301">*검색 앨범 편집 보기,이 이번에는 드롭다운 목록*</span><span class="sxs-lookup"><span data-stu-id="4cf50-301">*Browsing Album's Edit view, this time with dropdowns*</span></span>

<a id="Ex3Task6"></a>

<a id="Task_6_-_Implementing_the_HTTP-POST_Edit_action_method"></a>
#### <a name="task-6---implementing-the-http-post-edit-action-method"></a><span data-ttu-id="4cf50-302">태스크 6-HTTP POST Edit 동작 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-302">Task 6 - Implementing the HTTP-POST Edit action method</span></span>

<span data-ttu-id="4cf50-303">보기 편집 예상 대로 나타나면 했으므로 앨범에 변경한 내용을 저장 하려면 작업을 편집 하는 HTTP POST 메서드를 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-303">Now that the Edit View displays as expected, you need to implement the HTTP-POST Edit Action method to save the changes made to the Album.</span></span>

1. <span data-ttu-id="4cf50-304">Visual Studio 창에 반환 하는 데 필요한 경우 브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-304">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="4cf50-305">열기 **StoreManagerController** 에서 **컨트롤러** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-305">Open **StoreManagerController** from the **Controllers** folder.</span></span>
2. <span data-ttu-id="4cf50-306">대체 **HTTP POST 편집** 동작 메서드 코드를 다음 코드로 (참고: 두 개의 매개 변수를 수신 하는 오버 로드 된 버전을 교체 해야 하는 방법).</span><span class="sxs-lookup"><span data-stu-id="4cf50-306">Replace **HTTP-POST Edit** action method code with the following (note that the method that must be replaced is overloaded version that receives two parameters):</span></span>

    <span data-ttu-id="4cf50-307">(코드 조각- *ASP.NET MVC 4 도우미와 폼과 유효성 검사-작업 Ex3 StoreManagerController HTTP POST 편집*)</span><span class="sxs-lookup"><span data-stu-id="4cf50-307">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex3 StoreManagerController HTTP-POST Edit action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample11.cs)]

    > [!NOTE]
    > <span data-ttu-id="4cf50-308">이 메서드는 사용자가 클릭할 때 실행 됩니다는 **저장** 보기의 단추는 HTTP-POST 서버에 다시 폼 값의 데이터베이스에 유지 하도록를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-308">This method will be executed when the user clicks the **Save** button of the View and performs an HTTP-POST of the form values back to the server to persist them in the database.</span></span> <span data-ttu-id="4cf50-309">Decorator **[HttpPost]** HTTP POST 한 시나리오에 메서드를 사용 해야을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-309">The decorator **[HttpPost]** indicates that the method should be used for those HTTP-POST scenarios.</span></span> <span data-ttu-id="4cf50-310">메서드를 사용 하며는 **앨범** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-310">The method takes an **Album** object.</span></span> <span data-ttu-id="4cf50-311">ASP.NET MVC는 게시 된에서 앨범 개체를 자동으로 만들 됩니다 &lt;양식&gt; 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-311">ASP.NET MVC will automatically create the Album object from the posted &lt;form&gt; values.</span></span>
    > 
    > <span data-ttu-id="4cf50-312">메서드는 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-312">The method will perform these steps:</span></span>
    > 
    > 1. <span data-ttu-id="4cf50-313">모델이 유효한 경우:</span><span class="sxs-lookup"><span data-stu-id="4cf50-313">If model is valid:</span></span>
    > 
    >     1. <span data-ttu-id="4cf50-314">수정된 된 개체로 표시 하는 컨텍스트에서 앨범 항목을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-314">Update the album entry in the context to mark it as a modified object.</span></span>
    >     2. <span data-ttu-id="4cf50-315">변경 내용을 저장 하 고 인덱스 뷰 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-315">Save the changes and redirect to the index view.</span></span>
    > 2. <span data-ttu-id="4cf50-316">모델이 유효 하지 않을 경우와 ViewBag 채웁니다는 **GenreId** 및 **ArtistId**, 사용자 수를 받은 앨범 개체를 사용 하 여 뷰 반환 됩니다 모든 필수 업데이트를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-316">If the model is not valid, it will populate the ViewBag with the **GenreId** and **ArtistId**, then it will return the view with the received Album object to allow the user perform any required update.</span></span>

<a id="Ex3Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a><span data-ttu-id="4cf50-317">7-응용 프로그램 실행 작업</span><span class="sxs-lookup"><span data-stu-id="4cf50-317">Task 7 - Running the Application</span></span>

<span data-ttu-id="4cf50-318">에서는이 작업을 테스트 하는 **StoreManager 편집** 뷰 페이지는 데이터베이스에 실제로 업데이트 된 앨범 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-318">In this task, you will test that the **StoreManager Edit** View page actually saves the updated Album data in the database.</span></span>

1. <span data-ttu-id="4cf50-319">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-319">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="4cf50-320">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-320">The project starts in the Home page.</span></span> <span data-ttu-id="4cf50-321">URL을 변경 **/StoreManager/Edit/1**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-321">Change the URL to **/StoreManager/Edit/1**.</span></span> <span data-ttu-id="4cf50-322">앨범 제목을 변경 **부하** 을 클릭할 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-322">Change the Album title to **Load** and click on **Save**.</span></span> <span data-ttu-id="4cf50-323">앨범 제목 앨범 목록에서 실제로 변경 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-323">Verify that album's title actually changed in the list of albums.</span></span>

    <span data-ttu-id="4cf50-324">![앨범 업데이트](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "앨범 업데이트")</span><span class="sxs-lookup"><span data-stu-id="4cf50-324">![Updating an album](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "Updating an album")</span></span>

    <span data-ttu-id="4cf50-325">*앨범 업데이트*</span><span class="sxs-lookup"><span data-stu-id="4cf50-325">*Updating an Album*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Adding_a_Create_View"></a>
### <a name="exercise-4-adding-a-create-view"></a><span data-ttu-id="4cf50-326">만들기 뷰를 추가 하는 연습 4:</span><span class="sxs-lookup"><span data-stu-id="4cf50-326">Exercise 4: Adding a Create View</span></span>

<span data-ttu-id="4cf50-327">이제는 **StoreManagerController** 지원는 **편집** 기능 저장할 수 있도록 Create View 템플릿을 추가 하는 방법을 배우게 됩니다이 연습에서는 응용 프로그램에 새 앨범을 추가 하는 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-327">Now that the **StoreManagerController** supports the **Edit** ability, in this exercise you will learn how to add a Create View template to let store managers add new Albums to the application.</span></span>

<span data-ttu-id="4cf50-328">내에서 두 개의 별도 메서드를 사용 하 여 만들기 시나리오를 구현 합니다 편집 기능을 갖춘 했던 것 처럼는 **StoreManagerController** 클래스:</span><span class="sxs-lookup"><span data-stu-id="4cf50-328">Like you did with the Edit functionality, you will implement the Create scenario using two separate methods within the **StoreManagerController** class:</span></span>

1. <span data-ttu-id="4cf50-329">저장소 관리자를 처음 방문할 때 하나의 작업 메서드가 빈 폼 표시 됩니다는 **/StoreManager/만들기** URL입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-329">One action method will display an empty form when store managers first visit the **/StoreManager/Create** URL.</span></span>
2. <span data-ttu-id="4cf50-330">두 번째 동작 메서드를 처리할 시나리오 저장소 관리자는 클릭할 수 있는 **저장** 폼 내에서 단추에 값을 다시 전송 하는 **/StoreManager/만들기** HTTP POST로 써는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-330">A second action method will handle the scenario where the store manager clicks the **Save** button within the form and submits the values back to the **/StoreManager/Create** URL as an HTTP-POST.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Create_action_method"></a>
#### <a name="task-1---implementing-the-http-get-create-action-method"></a><span data-ttu-id="4cf50-331">작업 1-HTTP GET 만들 동작 메서드 구현</span><span class="sxs-lookup"><span data-stu-id="4cf50-331">Task 1 - Implementing the HTTP-GET Create action method</span></span>

<span data-ttu-id="4cf50-332">이 작업에서는 HTTP GET 버전의 모든 장르와 예술가 목록을 검색,이 데이터에 패키지를 만들기 작업 메서드를 구현 합니다는 **StoreManagerViewModel** 개체 보기 서식 파일에 전달 될 다음입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-332">In this task, you will implement the HTTP-GET version of the Create action method to retrieve a list of all Genres and Artists, package this data up into a **StoreManagerViewModel** object, which will then be passed to a View template.</span></span>

1. <span data-ttu-id="4cf50-333">열기는 **시작** 솔루션에 있는 **소스/Ex4-AddingACreateView/시작/** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-333">Open the **Begin** solution located at **Source/Ex4-AddingACreateView/Begin/** folder.</span></span> <span data-ttu-id="4cf50-334">그렇지 않은 경우 계속 사용할 수도 있습니다는 **끝** 솔루션, 이전 연습을 완료 하 여 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-334">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="4cf50-335">제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면.</span><span class="sxs-lookup"><span data-stu-id="4cf50-335">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="4cf50-336">이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-336">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="4cf50-337">에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="4cf50-337">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="4cf50-338">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-338">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="4cf50-339">NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-339">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="4cf50-340">NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-340">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="4cf50-341">이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-341">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="4cf50-342">열기 **StoreManagerController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-342">Open **StoreManagerController** class.</span></span> <span data-ttu-id="4cf50-343">이 작업을 수행 하려면 확장 된 **컨트롤러** 폴더를 두 번 클릭 **StoreManagerController.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-343">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="4cf50-344">대체는 **만들기** 동작 메서드 코드를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="4cf50-344">Replace the **Create** action method code with the following:</span></span>

    <span data-ttu-id="4cf50-345">(코드 조각- *ASP.NET MVC 4 도우미와 폼과 유효성 검사-Ex4 StoreManagerController HTTP GET 만들기 동작*)</span><span class="sxs-lookup"><span data-stu-id="4cf50-345">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex4 StoreManagerController HTTP-GET Create action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample12.cs)]

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_the_Create_View"></a>
#### <a name="task-2---adding-the-create-view"></a><span data-ttu-id="4cf50-346">작업 2-만들기 뷰 추가</span><span class="sxs-lookup"><span data-stu-id="4cf50-346">Task 2 - Adding the Create View</span></span>

<span data-ttu-id="4cf50-347">이 태스크에서는 새 (비어 있음) 앨범 폼을 표시 하는 Create View 서식 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-347">In this task, you will add the Create View template that will display a new (empty) Album form.</span></span>

1. <span data-ttu-id="4cf50-348">마우스 오른쪽 단추로 클릭는 **만들기** 동작 메서드와 선택 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-348">Right-click inside the **Create** action method and select **Add View**.</span></span> <span data-ttu-id="4cf50-349">이 뷰 추가 대화 상자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-349">This will bring up the Add View dialog.</span></span>
2. <span data-ttu-id="4cf50-350">뷰 추가 대화 상자에서 보기 이름 인지 확인 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-350">In the Add View dialog, verify that the View Name is **Create**.</span></span> <span data-ttu-id="4cf50-351">선택 된 **강력한 형식의 뷰 만들기** 및 옵션을 선택 **앨범 (MvcMusicStore.Models)** 에서 **모델 클래스** 드롭 다운 및 **만들기** 에서 **스 캐 폴드 템플릿이** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-351">Select the **Create a strongly-typed view** option and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down and **Create** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="4cf50-352">다른 필드를 기본값으로 두고 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-352">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="4cf50-353">![만들기 뷰 추가](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "추가-a-만들기-view.png")</span><span class="sxs-lookup"><span data-stu-id="4cf50-353">![Adding a create view](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "adding-a-create-view.png")</span></span>

    <span data-ttu-id="4cf50-354">*만들기 뷰 추가*</span><span class="sxs-lookup"><span data-stu-id="4cf50-354">*Adding the Create View*</span></span>
3. <span data-ttu-id="4cf50-355">업데이트는 **GenreId** 및 **ArtistId** 아래 표시 된 것 처럼 드롭 다운 목록을 사용 하는 필드:</span><span class="sxs-lookup"><span data-stu-id="4cf50-355">Update the **GenreId** and **ArtistId** fields to use a drop-down list as shown below:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample13.cshtml)]

<a id="Ex4Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="4cf50-356">작업 3-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="4cf50-356">Task 3 - Running the Application</span></span>

<span data-ttu-id="4cf50-357">에서는이 작업을 테스트 하는 **StoreManager** **만들기** 빈 앨범 폼 보기 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-357">In this task, you will test that the **StoreManager** **Create** View page displays an empty Album form.</span></span>

1. <span data-ttu-id="4cf50-358">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-358">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="4cf50-359">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-359">The project starts in the Home page.</span></span> <span data-ttu-id="4cf50-360">URL을 변경 **/StoreManager/만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-360">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="4cf50-361">새 앨범 속성을 채우기 위한 빈 폼이 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-361">Verify that an empty form is displayed for filling the new Album properties.</span></span>

    <span data-ttu-id="4cf50-362">![Create View 빈 양식으로](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "빈 양식으로 보기 만들기")</span><span class="sxs-lookup"><span data-stu-id="4cf50-362">![Create View with an empty form](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "Create View with an empty form")</span></span>

    <span data-ttu-id="4cf50-363">*빈 폼 보기 만들기*</span><span class="sxs-lookup"><span data-stu-id="4cf50-363">*Create View with an empty form*</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_-_Implementing_the_HTTP-POST_Create_Action_Method"></a>
#### <a name="task-4---implementing-the-http-post-create-action-method"></a><span data-ttu-id="4cf50-364">작업 4-구현 HTTP POST 작업 메서드 만들기</span><span class="sxs-lookup"><span data-stu-id="4cf50-364">Task 4 - Implementing the HTTP-POST Create Action Method</span></span>

<span data-ttu-id="4cf50-365">이 작업에서는 Create 작업 메서드는 사용자가 클릭할 때 호출 되는 HTTP POST 버전을 구현 합니다는 **저장** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-365">In this task, you will implement the HTTP-POST version of the Create action method that will be invoked when a user clicks the **Save** button.</span></span> <span data-ttu-id="4cf50-366">메서드는 데이터베이스에 새 앨범을 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-366">The method should save the new album in the database.</span></span>

1. <span data-ttu-id="4cf50-367">Visual Studio 창에 반환 하는 데 필요한 경우 브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-367">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="4cf50-368">열기 **StoreManagerController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-368">Open **StoreManagerController** class.</span></span> <span data-ttu-id="4cf50-369">이 작업을 수행 하려면 확장 된 **컨트롤러** 폴더를 두 번 클릭 **StoreManagerController.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-369">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
2. <span data-ttu-id="4cf50-370">대체 **HTTP POST 만들** 동작 메서드 코드를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="4cf50-370">Replace **HTTP-POST Create** action method code with the following:</span></span>

    <span data-ttu-id="4cf50-371">(코드 조각- *ASP.NET MVC 4 도우미와 폼과 유효성 검사-Ex4 StoreManagerController HTTP POST 만들기 작업*)</span><span class="sxs-lookup"><span data-stu-id="4cf50-371">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex4 StoreManagerController HTTP- POST Create action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample14.cs)]

    > [!NOTE]
    > <span data-ttu-id="4cf50-372">만들기 작업은 이전 편집 작업 메서드와 매우 유사 하지만 수정 된 개체를 설정 하는 대신 컨텍스트에 추가 되 고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-372">The Create action is pretty similar to the previous Edit action method but instead of setting the object as modified, it is being added to the context.</span></span>

<a id="Ex4Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="4cf50-373">5-응용 프로그램 실행 작업</span><span class="sxs-lookup"><span data-stu-id="4cf50-373">Task 5 - Running the Application</span></span>

<span data-ttu-id="4cf50-374">에서는이 작업을 테스트 하는 **StoreManager 만들** 보기 페이지 새 앨범을 만들 수 있습니다 및 StoreManager 인덱스 뷰를 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-374">In this task, you will test that the **StoreManager Create** View page lets you create a new Album and then redirects to the StoreManager Index View.</span></span>

1. <span data-ttu-id="4cf50-375">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-375">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="4cf50-376">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-376">The project starts in the Home page.</span></span> <span data-ttu-id="4cf50-377">URL을 변경 **/StoreManager/만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-377">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="4cf50-378">다음 그림에서와 같은 새 앨범에 대 한 데이터 사용 모든 양식 필드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-378">Fill all the form fields with data for a new Album, like the one in the following figure:</span></span>

    <span data-ttu-id="4cf50-379">![앨범 만드는](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "앨범 만들기")</span><span class="sxs-lookup"><span data-stu-id="4cf50-379">![Creating an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "Creating an Album")</span></span>

    <span data-ttu-id="4cf50-380">*앨범 만들기*</span><span class="sxs-lookup"><span data-stu-id="4cf50-380">*Creating an Album*</span></span>
3. <span data-ttu-id="4cf50-381">방금 만든 새 앨범을 포함 하는 StoreManager 인덱스 보기도 리디렉션됩니다 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-381">Verify that you get redirected to the StoreManager Index View that includes the new Album just created.</span></span>

    <span data-ttu-id="4cf50-382">![만든 새 앨범](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "만든 새 앨범")</span><span class="sxs-lookup"><span data-stu-id="4cf50-382">![New Album Created](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "New Album Created")</span></span>

    <span data-ttu-id="4cf50-383">*만든 새 앨범*</span><span class="sxs-lookup"><span data-stu-id="4cf50-383">*New Album Created*</span></span>

<a id="Exercise5"></a>

<a id="Exercise_5_Handling_Deletion"></a>
### <a name="exercise-5-handling-deletion"></a><span data-ttu-id="4cf50-384">삭제를 처리 하는 연습 5:</span><span class="sxs-lookup"><span data-stu-id="4cf50-384">Exercise 5: Handling Deletion</span></span>

<span data-ttu-id="4cf50-385">앨범을 삭제 하는 기능이 아직 구현 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-385">The ability to delete albums is not yet implemented.</span></span> <span data-ttu-id="4cf50-386">에 대 한이 연습은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-386">This is what this exercise will be about.</span></span> <span data-ttu-id="4cf50-387">내에서 두 개의 별도 메서드를 사용 하 여 Delete 시나리오를 구현 합니다 이전 처럼는 **StoreManagerController** 클래스:</span><span class="sxs-lookup"><span data-stu-id="4cf50-387">Like before, you will implement the Delete scenario using two separate methods within the **StoreManagerController** class:</span></span>

1. <span data-ttu-id="4cf50-388">하나의 작업 메서드 확인 폼이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-388">One action method will display a confirmation form</span></span>
2. <span data-ttu-id="4cf50-389">두 번째 동작 메서드를 처리할 양식 전송</span><span class="sxs-lookup"><span data-stu-id="4cf50-389">A second action method will handle the form submission</span></span>

<a id="Ex5Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Delete_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-delete-action-method"></a><span data-ttu-id="4cf50-390">작업 1-HTTP GET Delete 동작 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-390">Task 1 - Implementing the HTTP-GET Delete Action Method</span></span>

<span data-ttu-id="4cf50-391">이 태스크는 앨범의 정보를 검색 하는 Delete 동작 메서드의 GET HTTP 버전을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-391">In this task, you will implement the HTTP-GET version of the Delete action method to retrieve the album's information.</span></span>

1. <span data-ttu-id="4cf50-392">열기는 **시작** 솔루션에 있는 **소스/Ex5-HandlingDeletion/시작/** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-392">Open the **Begin** solution located at **Source/Ex5-HandlingDeletion/Begin/** folder.</span></span> <span data-ttu-id="4cf50-393">그렇지 않은 경우 계속 사용할 수도 있습니다는 **끝** 솔루션, 이전 연습을 완료 하 여 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-393">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="4cf50-394">제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면.</span><span class="sxs-lookup"><span data-stu-id="4cf50-394">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="4cf50-395">이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-395">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="4cf50-396">에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="4cf50-396">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="4cf50-397">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-397">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="4cf50-398">NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-398">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="4cf50-399">NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-399">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="4cf50-400">이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-400">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="4cf50-401">열기 **StoreManagerController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-401">Open **StoreManagerController** class.</span></span> <span data-ttu-id="4cf50-402">이 작업을 수행 하려면 확장 된 **컨트롤러** 폴더를 두 번 클릭 **StoreManagerController.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-402">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="4cf50-403">Delete 컨트롤러 작업은 정확 하 게 이전 저장소 세부 정보 컨트롤러 작업와 동일: 쿼리하여는 **앨범** 사용 하 여 데이터베이스에서 개체는 **id** URL과 반환에서 제공 되는 적절 한 **보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-403">The Delete controller action is exactly the same as the previous Store Details controller action: it queries the **album** object from the database using the **id** provided in the URL and returns the appropriate **View**.</span></span> <span data-ttu-id="4cf50-404">이 작업을 수행 하려면 HTTP GET을 대체 **삭제** 동작 메서드 코드를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="4cf50-404">To do this, replace the HTTP-GET **Delete** action method code with the following:</span></span>

    <span data-ttu-id="4cf50-405">(코드 조각- *ASP.NET MVC 4 도우미와 폼과 유효성 검사-Ex5 처리 삭제 HTTP GET 삭제 작업*)</span><span class="sxs-lookup"><span data-stu-id="4cf50-405">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex5 Handling Deletion HTTP-GET Delete action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample15.cs)]
4. <span data-ttu-id="4cf50-406">마우스 오른쪽 단추로 클릭는 **삭제** 동작 메서드와 선택 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-406">Right-click inside the **Delete** action method and select **Add View**.</span></span> <span data-ttu-id="4cf50-407">이 뷰 추가 대화 상자를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-407">This will bring up the Add View dialog.</span></span>
5. <span data-ttu-id="4cf50-408">뷰 추가 대화 상자에서 보기 이름 인지 확인 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-408">In the Add View dialog, verify that the View name is **Delete**.</span></span> <span data-ttu-id="4cf50-409">선택 된 **강력한 형식의 뷰 만들기** 및 옵션을 선택 **앨범 (MvcMusicStore.Models)** 에서 **모델 클래스** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-409">Select the **Create a strongly-typed view** option and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down.</span></span> <span data-ttu-id="4cf50-410">선택 **삭제** 에서 **스 캐 폴드 템플릿이** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-410">Select **Delete** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="4cf50-411">다른 필드를 기본값으로 두고 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-411">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="4cf50-412">![삭제 뷰 추가](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "삭제 뷰 추가")</span><span class="sxs-lookup"><span data-stu-id="4cf50-412">![Adding a Delete View](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "Adding a Delete View")</span></span>

    <span data-ttu-id="4cf50-413">*삭제 뷰 추가*</span><span class="sxs-lookup"><span data-stu-id="4cf50-413">*Adding a Delete View*</span></span>
6. <span data-ttu-id="4cf50-414">Delete 템플릿 모델에서 모든 필드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-414">The Delete template shows all the fields from the model.</span></span> <span data-ttu-id="4cf50-415">앨범 제목에만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-415">You will show only the album's title.</span></span> <span data-ttu-id="4cf50-416">이렇게 하려면 보기의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-416">To do this, replace the content of the view with the following code:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample16.cshtml)]

<a id="Ex05Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="4cf50-417">작업 2-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="4cf50-417">Task 2 - Running the Application</span></span>

<span data-ttu-id="4cf50-418">에서는이 작업을 테스트 하는 **StoreManager** **삭제** 확인 삭제 양식 보기 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-418">In this task, you will test that the **StoreManager** **Delete** View page displays a confirmation deletion form.</span></span>

1. <span data-ttu-id="4cf50-419">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-419">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="4cf50-420">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-420">The project starts in the Home page.</span></span> <span data-ttu-id="4cf50-421">URL을 변경 **/StoreManager**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-421">Change the URL to **/StoreManager**.</span></span> <span data-ttu-id="4cf50-422">클릭 하 여 삭제할 하나 앨범 선택 **삭제** 새 보기는 업로드 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-422">Select one album to delete by clicking **Delete** and verify that the new view is uploaded.</span></span>

    <span data-ttu-id="4cf50-423">![앨범 삭제](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "앨범 삭제")</span><span class="sxs-lookup"><span data-stu-id="4cf50-423">![Deleting an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "Deleting an Album")</span></span>

    <span data-ttu-id="4cf50-424">*앨범 삭제*</span><span class="sxs-lookup"><span data-stu-id="4cf50-424">*Deleting an Album*</span></span>

<a id="Ex05Task3"></a>

<a id="Task_3-_Implementing_the_HTTP-POST_Delete_Action_Method"></a>
#### <a name="task-3--implementing-the-http-post-delete-action-method"></a><span data-ttu-id="4cf50-425">작업 3-HTTP POST Delete 동작 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-425">Task 3- Implementing the HTTP-POST Delete Action Method</span></span>

<span data-ttu-id="4cf50-426">이 작업을 클릭할 때 호출 되는 Delete 동작 메서드의 POST HTTP 버전을 구현 합니다는 **삭제** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-426">In this task, you will implement the HTTP-POST version of the Delete action method that will be invoked when a user clicks the **Delete** button.</span></span> <span data-ttu-id="4cf50-427">메서드는 앨범의 데이터베이스에서 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-427">The method should delete the album in the database.</span></span>

1. <span data-ttu-id="4cf50-428">Visual Studio 창에 반환 하는 데 필요한 경우 브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-428">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="4cf50-429">열기 **StoreManagerController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-429">Open **StoreManagerController** class.</span></span> <span data-ttu-id="4cf50-430">이 작업을 수행 하려면 확장 된 **컨트롤러** 폴더를 두 번 클릭 **StoreManagerController.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-430">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
2. <span data-ttu-id="4cf50-431">대체 **HTTP POST 삭제** 동작 메서드 코드를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="4cf50-431">Replace **HTTP-POST Delete** action method code with the following:</span></span>

    <span data-ttu-id="4cf50-432">(코드 조각- *ASP.NET MVC 4 도우미와 폼과 유효성 검사-Ex5 처리 삭제 HTTP POST 삭제 작업*)</span><span class="sxs-lookup"><span data-stu-id="4cf50-432">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex5 Handling Deletion HTTP-POST Delete action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample17.cs)]

<a id="Ex5Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="4cf50-433">작업 4-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="4cf50-433">Task 4 - Running the Application</span></span>

<span data-ttu-id="4cf50-434">에서는이 작업을 테스트 하는 **StoreManager Delete** 보기 페이지에서는 앨범을 삭제할 수 있습니다 및 StoreManager 인덱스 뷰를 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-434">In this task, you will test that the **StoreManager Delete** View page lets you delete an Album and then redirects to the StoreManager Index View.</span></span>

1. <span data-ttu-id="4cf50-435">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-435">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="4cf50-436">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-436">The project starts in the Home page.</span></span> <span data-ttu-id="4cf50-437">URL을 변경 **/StoreManager**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-437">Change the URL to **/StoreManager**.</span></span> <span data-ttu-id="4cf50-438">클릭 하 여 삭제할 하나 앨범 선택 **삭제 합니다.**</span><span class="sxs-lookup"><span data-stu-id="4cf50-438">Select one album to delete by clicking **Delete.**</span></span> <span data-ttu-id="4cf50-439">클릭 하 여 삭제를 확인 **삭제** 단추:</span><span class="sxs-lookup"><span data-stu-id="4cf50-439">Confirm the deletion by clicking **Delete** button:</span></span>

    <span data-ttu-id="4cf50-440">![앨범 삭제](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "앨범 삭제")</span><span class="sxs-lookup"><span data-stu-id="4cf50-440">![Deleting an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "Deleting an Album")</span></span>

    <span data-ttu-id="4cf50-441">*앨범 삭제*</span><span class="sxs-lookup"><span data-stu-id="4cf50-441">*Deleting an Album*</span></span>
3. <span data-ttu-id="4cf50-442">앨범에 나타나지 않도록 이후 삭제 되었는지 확인는 **인덱스** 페이지.</span><span class="sxs-lookup"><span data-stu-id="4cf50-442">Verify that the album was deleted since it does not appear in the **Index** page.</span></span>

<a id="Exercise6"></a>

<a id="Exercise_6_Adding_Validation"></a>
### <a name="exercise-6-adding-validation"></a><span data-ttu-id="4cf50-443">실습 6: 유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="4cf50-443">Exercise 6: Adding Validation</span></span>

<span data-ttu-id="4cf50-444">현재 위치에 있는 만들기 및 편집 폼 유효성 검사를 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-444">Currently, the Create and Edit forms you have in place do not perform any kind of validation.</span></span> <span data-ttu-id="4cf50-445">사용자가 필수 필드를 비워 또는 형식 편지 price 필드에서를 완료 하는 경우에 데이터베이스에서 첫 번째 오류를 받게 됩니다 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-445">If the user leaves a required field blank or type letters in the price field, the first error you will get will be from the database.</span></span>

<span data-ttu-id="4cf50-446">데이터 주석 모델 클래스를 추가 하 여 응용 프로그램에 유효성 검사를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-446">You can add validation to the application by adding Data Annotations to your model class.</span></span> <span data-ttu-id="4cf50-447">ASP.NET MVC에서 자동으로 처리를 적용 하 고 사용자에 게 적절 한 메시지를 표시 및 데이터 주석 모델 속성을 적용할 규칙을 설명 하는 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-447">Data Annotations allow describing the rules you want applied to your model properties, and ASP.NET MVC will take care of enforcing and displaying appropriate message to users.</span></span>

<a id="Ex06Task1"></a>

<a id="Task_1_-_Adding_Data_Annotations"></a>
#### <a name="task-1---adding-data-annotations"></a><span data-ttu-id="4cf50-448">작업 1-데이터 주석 추가</span><span class="sxs-lookup"><span data-stu-id="4cf50-448">Task 1 - Adding Data Annotations</span></span>

<span data-ttu-id="4cf50-449">이 작업에서는 적절 한 경우 유효성 검사 메시지를 표시 하는 데이터 주석 만들기 및 편집 페이지에 있도록 앨범 모델에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-449">In this task, you will add Data Annotations to the Album Model that will make the Create and Edit page display validation messages when appropriate.</span></span>

<span data-ttu-id="4cf50-450">간단한 모델 클래스에 대 한 데이터 주석이 방금 처리 추가 추가 하 여 한 **를 사용 하 여** 문을 **System.ComponentModel.DataAnnotation**, 다음 배치는 **[필수]** 적절 한 속성에는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-450">For a simple Model class, adding a Data Annotation is just handled by adding a **using** statement for **System.ComponentModel.DataAnnotation**, then placing a **[Required]** attribute on the appropriate properties.</span></span> <span data-ttu-id="4cf50-451">다음 예제에서는 하 게 만드는 **이름** 속성 보기에서 필수 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-451">The following example would make the **Name** property a required field in the View.</span></span>

[!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample18.cs)]

<span data-ttu-id="4cf50-452">이 엔터티 데이터 모델 생성은이 응용 프로그램 같은 경우 좀 더 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-452">This is a little more complex in cases like this application where the Entity Data Model is generated.</span></span> <span data-ttu-id="4cf50-453">데이터 주석 모델 클래스에 직접 추가한 데이터베이스에서 모델을 업데이트 하는 경우 덮어쓰게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-453">If you added Data Annotations directly to the model classes, they would be overwritten if you update the model from the database.</span></span> <span data-ttu-id="4cf50-454">만들 수는 대신, 됩니다 주석을 저장할 수 있고 모델에 연결 된 메타 데이터 부분 클래스를 사용 하 여 클래스를 사용 하는 **[MetadataType]** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-454">Instead, you can make use of metadata partial classes which will exist to hold the annotations and are associated with the model classes using the **[MetadataType]** attribute.</span></span>

1. <span data-ttu-id="4cf50-455">열기는 **시작** 솔루션에 있는 **소스/Ex6-AddingValidation/시작/** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-455">Open the **Begin** solution located at **Source/Ex6-AddingValidation/Begin/** folder.</span></span> <span data-ttu-id="4cf50-456">그렇지 않은 경우 계속 사용할 수도 있습니다는 **끝** 솔루션, 이전 연습을 완료 하 여 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-456">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="4cf50-457">제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면.</span><span class="sxs-lookup"><span data-stu-id="4cf50-457">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="4cf50-458">이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-458">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="4cf50-459">에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="4cf50-459">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="4cf50-460">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-460">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="4cf50-461">NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-461">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="4cf50-462">NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-462">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="4cf50-463">이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-463">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="4cf50-464">열기는 **Album.cs** 에서 **모델** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-464">Open the **Album.cs** from the **Models** folder.</span></span>
3. <span data-ttu-id="4cf50-465">대체 **Album.cs** 을 다음과 같이 강조 표시 된 코드를 있는 콘텐츠:</span><span class="sxs-lookup"><span data-stu-id="4cf50-465">Replace **Album.cs** content with the highlighted code, so that it looks like the following:</span></span>

    > [!NOTE]
    > <span data-ttu-id="4cf50-466">줄 **[DisplayFormat(ConvertEmptyStringToNull=false)]** 빈 문자열은 모델에서 데이터 원본에서 데이터 필드가 업데이트 되는 경우 null로 변환 되지 않습니다 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-466">The line **[DisplayFormat(ConvertEmptyStringToNull=false)]** indicates that empty strings from the model won't be converted to null when the data field is updated in the data source.</span></span> <span data-ttu-id="4cf50-467">이 설정은 데이터 주석 필드의 유효성을 검사 하기 전에 Entity Framework 모델에 null 값을 할당 하는 경우 예외가 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-467">This setting will avoid an exception when the Entity Framework assigns null values to the model before Data Annotation validates the fields.</span></span>

    <span data-ttu-id="4cf50-468">(코드 조각- *ASP.NET MVC 4 도우미와 폼과 유효성 검사-Ex6 앨범 메타 데이터에 대 한 partial 클래스*)</span><span class="sxs-lookup"><span data-stu-id="4cf50-468">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex6 Album metadata partial class*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample19.cs)]

    > [!NOTE]
    > <span data-ttu-id="4cf50-469">이 **앨범** 부분 클래스에는 **MetadataType** 가리키는 특성은 **AlbumMetaData** 데이터 주석에 대 한 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-469">This **Album** partial class has a **MetadataType** attribute which points to the **AlbumMetaData** class for the Data Annotations.</span></span> <span data-ttu-id="4cf50-470">다음은 앨범 모델 주석을 사용 하는 데이터 주석을 특성 중 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-470">These are some of the Data Annotation attributes you are using to annotate the Album model:</span></span>
    > 
    > - <span data-ttu-id="4cf50-471">필수-속성이 필수 필드 임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-471">Required - Indicates that the property is a required field</span></span>
    > - <span data-ttu-id="4cf50-472">DisplayName-양식 필드 및 유효성 검사 메시지에 사용할 텍스트를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-472">DisplayName - Defines the text to be used on form fields and validation messages</span></span>
    > - <span data-ttu-id="4cf50-473">DisplayFormat-데이터 필드가 표시 되 고 서식이 지정 되는 방식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-473">DisplayFormat - Specifies how data fields are displayed and formatted.</span></span>
    > - <span data-ttu-id="4cf50-474">StringLength-문자열 필드에 대 한 최대 길이 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-474">StringLength - Defines a maximum length for a string field</span></span>
    > - <span data-ttu-id="4cf50-475">범위가-숫자 필드에 대 한 최대 및 최소 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-475">Range - Gives a maximum and minimum value for a numeric field</span></span>
    > - <span data-ttu-id="4cf50-476">ScaffoldColumn-편집기 양식에서 필드를 숨길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-476">ScaffoldColumn - Allows hiding fields from editor forms</span></span>

<a id="Ex06Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="4cf50-477">작업 2-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="4cf50-477">Task 2 - Running the Application</span></span>

<span data-ttu-id="4cf50-478">에서는이 작업을 테스트 만들기 및 편집 페이지 필드의 유효성을 검사 마지막 작업에서 선택한 표시 이름을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-478">In this task, you will test that the Create and Edit pages validate fields, using the display names chosen in the last task.</span></span>

1. <span data-ttu-id="4cf50-479">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-479">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="4cf50-480">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-480">The project starts in the Home page.</span></span> <span data-ttu-id="4cf50-481">URL을 변경 **/StoreManager/만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-481">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="4cf50-482">표시 이름이 partial 클래스에서 일치 하는지 확인 하십시오 (같은 **앨범 아트 URL** 대신 **AlbumArtUrl**)</span><span class="sxs-lookup"><span data-stu-id="4cf50-482">Verify that the display names match the ones in the partial class (like **Album Art URL** instead of **AlbumArtUrl**)</span></span>
3. <span data-ttu-id="4cf50-483">클릭 **만들기**를 폼 입력 하지 않고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-483">Click **Create**, without filling the form.</span></span> <span data-ttu-id="4cf50-484">해당 하는 유효성 검사 메시지 얻어지는 지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-484">Verify that you get the corresponding validation messages.</span></span>

    <span data-ttu-id="4cf50-485">![필드 만들기 페이지에 유효성을 검사할](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "만들기 페이지의 필드 유효성 검사")</span><span class="sxs-lookup"><span data-stu-id="4cf50-485">![Validated fields in the Create page](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "Validated fields in the Create page")</span></span>

    <span data-ttu-id="4cf50-486">*유효성 검사 필드 만들기 페이지*</span><span class="sxs-lookup"><span data-stu-id="4cf50-486">*Validated fields in the Create page*</span></span>
4. <span data-ttu-id="4cf50-487">와 동일한 발생 하는지 확인할 수 있습니다는 **편집** 페이지.</span><span class="sxs-lookup"><span data-stu-id="4cf50-487">You can verify that the same occurs with the **Edit** page.</span></span> <span data-ttu-id="4cf50-488">URL을 변경 **/StoreManager/Edit/1** 표시 이름에서 partial 클래스와 일치 하는지 확인 하 고 (같은 **앨범 아트 URL** 대신 **AlbumArtUrl**).</span><span class="sxs-lookup"><span data-stu-id="4cf50-488">Change the URL to **/StoreManager/Edit/1** and verify that the display names match the ones in the partial class (like **Album Art URL** instead of **AlbumArtUrl**).</span></span> <span data-ttu-id="4cf50-489">빈는 **제목** 및 **가격** 필드와 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-489">Empty the **Title** and **Price** fields and click **Save**.</span></span> <span data-ttu-id="4cf50-490">해당 하는 유효성 검사 메시지 얻어지는 지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-490">Verify that you get the corresponding validation messages.</span></span>

    ![편집 페이지의 유효성이 검사 된 필드](aspnet-mvc-4-helpers-forms-and-validation/_static/image19.png)

    <span data-ttu-id="4cf50-492">*편집 페이지의 유효성이 검사 된 필드*</span><span class="sxs-lookup"><span data-stu-id="4cf50-492">*Validated fields in the Edit page*</span></span>

<a id="Exercise7"></a>

<a id="Exercise_7_Using_Unobtrusive_jQuery_at_Client_Side"></a>
### <a name="exercise-7-using-unobtrusive-jquery-at-client-side"></a><span data-ttu-id="4cf50-493">7 연습: 클라이언트 쪽에서 비 가시적인 jQuery를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="4cf50-493">Exercise 7: Using Unobtrusive jQuery at Client Side</span></span>

<span data-ttu-id="4cf50-494">이 연습에서는 클라이언트 쪽에서 MVC 4 비 가시적인 jQuery 유효성 검사를 사용 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-494">In this exercise, you will learn how to enable MVC 4 Unobtrusive jQuery validation at client side.</span></span>

> [!NOTE]
> <span data-ttu-id="4cf50-495">비 가시적인 jQuery 데이터 ajax 접두사 JavaScript를 사용 하 여 영향을 주지 않고 내보내는 인라인 클라이언트 스크립트 아닌 서버에서 작업 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-495">The Unobtrusive jQuery uses data-ajax prefix JavaScript to invoke action methods on the server rather than intrusively emitting inline client scripts.</span></span>


<a id="Ex7Task1"></a>

<a id="Task_1_-_Running_the_Application_before_Enabling_Unobtrusive_jQuery"></a>
#### <a name="task-1---running-the-application-before-enabling-unobtrusive-jquery"></a><span data-ttu-id="4cf50-496">작업 1-사용 하도록 설정 비 가시적인 jQuery 전에 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="4cf50-496">Task 1 - Running the Application before Enabling Unobtrusive jQuery</span></span>

<span data-ttu-id="4cf50-497">이 작업을 모두 유효성 검사 모델을 비교 하기 위해 jQuery를 포함 하기 전에 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-497">In this task, you will run the application before including jQuery in order to compare both validation models.</span></span>

1. <span data-ttu-id="4cf50-498">열기는 **시작** 솔루션에 있는 **소스/Ex7-UnobtrusivejQueryValidation/시작/** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-498">Open the **Begin** solution located at **Source/Ex7-UnobtrusivejQueryValidation/Begin/** folder.</span></span> <span data-ttu-id="4cf50-499">그렇지 않은 경우 계속 사용할 수도 있습니다는 **끝** 솔루션, 이전 연습을 완료 하 여 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-499">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="4cf50-500">제공 된 연 경우 **시작** 를 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다 솔루션을 계속 하려면.</span><span class="sxs-lookup"><span data-stu-id="4cf50-500">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="4cf50-501">이 작업을 수행 하려면는 **프로젝트** 메뉴와 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-501">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="4cf50-502">에 **NuGet 패키지 관리** 대화 상자를 클릭 하 여 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="4cf50-502">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="4cf50-503">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-503">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="4cf50-504">NuGet을 사용 하 여의 장점 중 하나 없습니다 있는입니다 써 해당 프로젝트의 모든 라이브러리를 프로젝트 크기를 줄이면 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-504">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="4cf50-505">NuGet 파워 도구 Packages.config 파일에서 패키지 버전을 지정 하 여 해야 합니다를 처음으로 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-505">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="4cf50-506">이 때문에이 랩에서 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-506">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="4cf50-507">**F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-507">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="4cf50-508">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-508">The project starts in the Home page.</span></span> <span data-ttu-id="4cf50-509">찾아보기 **/StoreManager/만들기** 클릭 **만들기** 폼 유효성 검사 메시지 얻어지는 지 확인을 채우지 않고:</span><span class="sxs-lookup"><span data-stu-id="4cf50-509">Browse **/StoreManager/Create** and click **Create** without filling the form to verify that you get validation messages:</span></span>

    <span data-ttu-id="4cf50-510">![사용 하지 않도록 설정 하는 클라이언트 유효성 검사](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "사용 하지 않도록 설정 하는 클라이언트 유효성 검사")</span><span class="sxs-lookup"><span data-stu-id="4cf50-510">![Client validation disabled](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "Client validation disabled")</span></span>

    <span data-ttu-id="4cf50-511">*클라이언트 유효성 검사를 사용 하지 않도록 설정*</span><span class="sxs-lookup"><span data-stu-id="4cf50-511">*Client validation disabled*</span></span>
4. <span data-ttu-id="4cf50-512">브라우저에서 HTML 소스 코드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-512">In the browser, open the HTML source code:</span></span>

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample20.html)]

<a id="Ex7Task2"></a>

<a id="Task_2_-_Enabling_Unobtrusive_Client_Validation"></a>
#### <a name="task-2---enabling-unobtrusive-client-validation"></a><span data-ttu-id="4cf50-513">작업 2-비 가시적인 클라이언트 유효성 검사를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="4cf50-513">Task 2 - Enabling Unobtrusive Client Validation</span></span>

<span data-ttu-id="4cf50-514">이 태스크에서는 jQuery 하면 **비간섭 클라이언트 유효성 검사** 에서 **Web.config** 기본적으로 모든 새 ASP.NET MVC 4 프로젝트에는 false로 설정 된 파일을 가져오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-514">In this task, you will enable jQuery **unobtrusive client validation** from **Web.config** file, which is by default set to false in all new ASP.NET MVC 4 projects.</span></span> <span data-ttu-id="4cf50-515">또한 필요한 스크립트 jQuery 비 가시적인 클라이언트 유효성 검사 작업 확인에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-515">Additionally, you will add the necessary scripts references to make jQuery Unobtrusive Client Validation work.</span></span>

1. <span data-ttu-id="4cf50-516">열기 **Web.Config** 파일을 프로젝트 루트에 있는지 확인 하 고는 **ClientValidationEnabled** 및 **UnobtrusiveJavaScriptEnabled** 키 값 로설정되며**true**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-516">Open **Web.Config** file at project root, and make sure that the **ClientValidationEnabled** and **UnobtrusiveJavaScriptEnabled** keys values are set to **true**.</span></span>

    [!code-xml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample21.xml)]

    > [!NOTE]
    > <span data-ttu-id="4cf50-517">또한 동일한 결과 얻기 위해 Global.asax.cs에서 코드에 의해 클라이언트 유효성 검사를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-517">You can also enable client validation by code at Global.asax.cs to get the same results:</span></span>
    > 
    > <span data-ttu-id="4cf50-518">**HtmlHelper.ClientValidationEnabled = true;**</span><span class="sxs-lookup"><span data-stu-id="4cf50-518">**HtmlHelper.ClientValidationEnabled = true;**</span></span>
    > 
    > <span data-ttu-id="4cf50-519">또한 ClientValidationEnabled 특성을 사용자 지정 동작을 갖는 모든 컨트롤러에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-519">Additionally, you can assign ClientValidationEnabled attribute into any controller to have a custom behavior.</span></span>
2. <span data-ttu-id="4cf50-520">열기 **Create.cshtml** 에서 **Views\StoreManager**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-520">Open **Create.cshtml** at **Views\StoreManager**.</span></span>
3. <span data-ttu-id="4cf50-521">다음 스크립트 파일을 확인 **jquery.validate** 및 **jquery.validate.unobtrusive**, 보기 제외에서 참조 되는 &quot; **~/bundles/jqueryval** &quot; 번들입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-521">Make sure the following script files, **jquery.validate** and **jquery.validate.unobtrusive**, are referenced in the view throught the &quot;**~/bundles/jqueryval**&quot; bundle.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample22.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="4cf50-522">새 MVC 4 프로젝트에 이러한 모든 jQuery 라이브러리가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-522">All these jQuery libraries are included in MVC 4 new projects.</span></span> <span data-ttu-id="4cf50-523">더 많은 라이브러리를 찾을 수 있습니다는 **스크립트/** 있습니다 프로젝트의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-523">You can find more libraries in the **/Scripts** folder of you project.</span></span>
    > 
    > <span data-ttu-id="4cf50-524">이 유효성 검사를 확인 하려면 라이브러리가 작동, jQuery 프레임 워크 라이브러리에 대 한 참조를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-524">In order to make this validation libraries work, you need to add a reference to the jQuery framework library.</span></span> <span data-ttu-id="4cf50-525">이 참조에 이미 추가 하므로  **\_Layout.cshtml** 파일인 않아도이 특정 뷰에 추가할 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-525">Since this reference is already added in the **\_Layout.cshtml** file, you do not need to add it in this particular view.</span></span>

<a id="Ex7Task3"></a>

<a id="Task_3_-_Running_the_Application_Using_Unobtrusive_jQuery_Validation"></a>
#### <a name="task-3---running-the-application-using-unobtrusive-jquery-validation"></a><span data-ttu-id="4cf50-526">작업 3-응용 프로그램 사용 하 여 비 가시적인 jQuery 유효성 검사를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-526">Task 3 - Running the Application Using Unobtrusive jQuery Validation</span></span>

<span data-ttu-id="4cf50-527">에서는이 작업을 테스트 하는 **StoreManager** 템플릿을 사용자가 새 앨범을 만들 때 jQuery 라이브러리를 사용 하 여 클라이언트 쪽 유효성 검사를 수행 하는 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-527">In this task, you will test that the **StoreManager** create view template performs client side validation using jQuery libraries when the user creates a new album.</span></span>

1. <span data-ttu-id="4cf50-528">**F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-528">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="4cf50-529">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-529">The project starts in the Home page.</span></span> <span data-ttu-id="4cf50-530">찾아보기 **/StoreManager/만들기** 클릭 **만들기** 폼 유효성 검사 메시지 얻어지는 지 확인을 채우지 않고:</span><span class="sxs-lookup"><span data-stu-id="4cf50-530">Browse **/StoreManager/Create** and click **Create** without filling the form to verify that you get validation messages:</span></span>

    <span data-ttu-id="4cf50-531">![사용 하도록 설정 하는 jQuery 사용 하 여 클라이언트 유효성](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "jQuery 사용 하도록 설정 된 클라이언트 유효성 검사")</span><span class="sxs-lookup"><span data-stu-id="4cf50-531">![Client validation with jQuery enabled](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "Client validation with jQuery enabled")</span></span>

    <span data-ttu-id="4cf50-532">*JQuery 사용 하도록 설정 된 클라이언트 유효성 검사*</span><span class="sxs-lookup"><span data-stu-id="4cf50-532">*Client validation with jQuery enabled*</span></span>
3. <span data-ttu-id="4cf50-533">브라우저에서 뷰 만들기에 대 한 소스 코드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-533">In the browser, open the source code for Create view:</span></span>

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample23.html)]

   > [!NOTE]
   > <span data-ttu-id="4cf50-534">각 클라이언트 유효성 검사 규칙에 대해 비 가시적인 jQuery 추가 데이터를 사용 하 여 특성-val-*rulename*=&quot;*메시지*&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-534">For each client validation rule, Unobtrusive jQuery adds an attribute with data-val-*rulename*=&quot;*message*&quot;.</span></span> <span data-ttu-id="4cf50-535">아래 해당 Unobtrusive는 태그의 목록 jQuery 클라이언트 유효성 검사를 수행 하려면 html 입력된 필드에 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-535">Below is a list of tags that Unobtrusive jQuery inserts into the html input field to perform client validation:</span></span>
   > 
   > - <span data-ttu-id="4cf50-536">데이터 val</span><span class="sxs-lookup"><span data-stu-id="4cf50-536">Data-val</span></span>
   > - <span data-ttu-id="4cf50-537">데이터-val 수</span><span class="sxs-lookup"><span data-stu-id="4cf50-537">Data-val-number</span></span>
   > - <span data-ttu-id="4cf50-538">데이터 val 범위</span><span class="sxs-lookup"><span data-stu-id="4cf50-538">Data-val-range</span></span>
   > - <span data-ttu-id="4cf50-539">데이터 val-범위 min/데이터 val-범위 최대값</span><span class="sxs-lookup"><span data-stu-id="4cf50-539">Data-val-range-min / Data-val-range-max</span></span>
   > - <span data-ttu-id="4cf50-540">데이터 val 필요</span><span class="sxs-lookup"><span data-stu-id="4cf50-540">Data-val-required</span></span>
   > - <span data-ttu-id="4cf50-541">데이터 val 길이</span><span class="sxs-lookup"><span data-stu-id="4cf50-541">Data-val-length</span></span>
   > - <span data-ttu-id="4cf50-542">Val 길이 최대 데이터/val 길이 min 데이터</span><span class="sxs-lookup"><span data-stu-id="4cf50-542">Data-val-length-max / Data-val-length-min</span></span>
   > 
   > <span data-ttu-id="4cf50-543">모든 데이터 값이 모델 채워집니다 **데이터 주석을**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-543">All the data values are filled with model **Data Annotation**.</span></span> <span data-ttu-id="4cf50-544">그런 다음 클라이언트 쪽에서 서버 쪽에서 작동 하는 모든 논리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-544">Then, all the logic that works at server side can be run at client side.</span></span> <span data-ttu-id="4cf50-545">예를 들어 Price 특성에 다음 데이터 주석을 모델에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-545">For example, Price attribute has the following data annotation in the model:</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample24.cs)]
   > 
   > <span data-ttu-id="4cf50-546">비 가시적인 jQuery를 사용한 후 생성 된 코드는입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-546">After using Unobtrusive jQuery, the generated code is:</span></span>
   > 
   > [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample25.html)]

* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="4cf50-547">요약</span><span class="sxs-lookup"><span data-stu-id="4cf50-547">Summary</span></span>

<span data-ttu-id="4cf50-548">이 실습 랩을 완료 하 여 사용자가 다음를 사용 하 여 데이터베이스에 저장 된 데이터를 변경할 수 있게 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-548">By completing this Hands-On Lab you have learned how to enable users to change the data stored in the database with the use of the following:</span></span>

- <span data-ttu-id="4cf50-549">인덱스, 만들기, 편집, 삭제와 같은 컨트롤러 작업</span><span class="sxs-lookup"><span data-stu-id="4cf50-549">Controller actions like Index, Create, Edit, Delete</span></span>
- <span data-ttu-id="4cf50-550">HTML 표에 속성을 표시 하기 위한 ASP.NET MVC 스 캐 폴딩 기능</span><span class="sxs-lookup"><span data-stu-id="4cf50-550">ASP.NET MVC's scaffolding feature for displaying properties in an HTML table</span></span>
- <span data-ttu-id="4cf50-551">사용자를 개선 하기 위해 사용자 지정 HTML 도우미 경험</span><span class="sxs-lookup"><span data-stu-id="4cf50-551">Custom HTML helpers to improve user experience</span></span>
- <span data-ttu-id="4cf50-552">HTTP GET 또는 HTTP POST 호출에 반응 하는 작업 메서드</span><span class="sxs-lookup"><span data-stu-id="4cf50-552">Action methods that react to either HTTP-GET or HTTP-POST calls</span></span>
- <span data-ttu-id="4cf50-553">템플릿 만들기 및 편집와 같은 비슷한 보기에 대 한 공유 편집기 서식 파일</span><span class="sxs-lookup"><span data-stu-id="4cf50-553">A shared editor template for similar View templates like Create and Edit</span></span>
- <span data-ttu-id="4cf50-554">드롭다운 목록 같은 form 요소</span><span class="sxs-lookup"><span data-stu-id="4cf50-554">Form elements like drop-downs</span></span>
- <span data-ttu-id="4cf50-555">모델 유효성 검사에 대 한 데이터 주석</span><span class="sxs-lookup"><span data-stu-id="4cf50-555">Data annotations for Model validation</span></span>
- <span data-ttu-id="4cf50-556">비 가시적인 jQuery 라이브러리를 사용 하 여 클라이언트 쪽 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="4cf50-556">Client Side Validation using jQuery Unobtrusive library</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="4cf50-557">부록 a: 설치 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="4cf50-557">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="4cf50-558">설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 버전을 사용 하 여 **[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="4cf50-558">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="4cf50-559">다음 지침을 설치 하는 데 필요한 단계를 안내 하 *Visual studio Express 2012 for Web* 를 사용 하 여 *Microsoft 웹 플랫폼 설치 관리자*합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-559">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="4cf50-560">로 이동 [ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-560">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="4cf50-561">또는 이미 설치 된 웹 플랫폼 설치 관리자를 열 수 있습니다 및 제품에 대 한 검색 &quot; <em>Visual Studio Express 2012 for Web Windows Azure SDK와</em>&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-561">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="4cf50-562">클릭 **지금 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-562">Click on **Install Now**.</span></span> <span data-ttu-id="4cf50-563">없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-563">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="4cf50-564">한 번 **웹 플랫폼 설치 관리자** 열려 클릭 **설치** 는 설치 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-564">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="4cf50-565">![Visual Studio Express 설치](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "Visual Studio Express 설치")</span><span class="sxs-lookup"><span data-stu-id="4cf50-565">![Install Visual Studio Express](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="4cf50-566">*Visual Studio Express 설치*</span><span class="sxs-lookup"><span data-stu-id="4cf50-566">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="4cf50-567">모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-567">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![사용 조건 동의](aspnet-mvc-4-helpers-forms-and-validation/_static/image23.png)

    <span data-ttu-id="4cf50-569">*사용 조건 동의*</span><span class="sxs-lookup"><span data-stu-id="4cf50-569">*Accepting the license terms*</span></span>
5. <span data-ttu-id="4cf50-570">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-570">Wait until the downloading and installation process completes.</span></span>

    ![설치 진행률](aspnet-mvc-4-helpers-forms-and-validation/_static/image24.png)

    <span data-ttu-id="4cf50-572">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="4cf50-572">*Installation progress*</span></span>
6. <span data-ttu-id="4cf50-573">설치가 완료 되 면 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-573">When the installation completes, click **Finish**.</span></span>

    ![설치 완료](aspnet-mvc-4-helpers-forms-and-validation/_static/image25.png)

    <span data-ttu-id="4cf50-575">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="4cf50-575">*Installation completed*</span></span>
7. <span data-ttu-id="4cf50-576">클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-576">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="4cf50-577">Visual Studio Express for Web을 열려면로 이동는 **시작** 화면를 쓰기 시작할 &quot; **VS Express**&quot;, 클릭는 **VS Express for Web** 바둑판식 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-577">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![웹 타일에 대 한 VS Express](aspnet-mvc-4-helpers-forms-and-validation/_static/image26.png)

    <span data-ttu-id="4cf50-579">*웹 타일에 대 한 VS Express*</span><span class="sxs-lookup"><span data-stu-id="4cf50-579">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="4cf50-580">부록 b: 코드 조각을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="4cf50-580">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="4cf50-581">코드 조각 바로 쉽게 얻습니다 필요한 코드를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-581">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="4cf50-582">랩 문서는 알려 정확 하 게 사용 가능 시기, 다음 그림에 나와 있는 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-582">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="4cf50-583">![Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "Visual Studio를 사용 하 여 코드 조각을 프로젝트에 코드를 삽입 하려면")</span><span class="sxs-lookup"><span data-stu-id="4cf50-583">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="4cf50-584">*Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여*</span><span class="sxs-lookup"><span data-stu-id="4cf50-584">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="4cf50-585">***키보드 (C#만)를 사용 하 여 코드 조각을 추가 하려면***</span><span class="sxs-lookup"><span data-stu-id="4cf50-585">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="4cf50-586">코드를 삽입 하려는 위치에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-586">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="4cf50-587">공백 또는 하이픈만) (없이 코드 조각 이름을 입력 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-587">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="4cf50-588">IntelliSense 표시 조각 이름과 일치 하는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-588">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="4cf50-589">올바른 코드 조각 선택 (또는 전체 코드 조각이 이름이 선택 될 때까지 입력 유지).</span><span class="sxs-lookup"><span data-stu-id="4cf50-589">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="4cf50-590">커서 위치에 코드 조각을 삽입 하려면 두 번 탭 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-590">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="4cf50-591">![코드 조각 이름을 입력 하기 시작](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "조각 이름을 입력 하기 시작")</span><span class="sxs-lookup"><span data-stu-id="4cf50-591">![Start typing the snippet name](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "Start typing the snippet name")</span></span>

<span data-ttu-id="4cf50-592">*코드 조각 이름을 입력 하기 시작*</span><span class="sxs-lookup"><span data-stu-id="4cf50-592">*Start typing the snippet name*</span></span>

<span data-ttu-id="4cf50-593">![Tab 키를 눌러 강조 표시 된 코드 조각 선택](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "Tab 키를 눌러 강조 표시 된 코드 조각 선택")</span><span class="sxs-lookup"><span data-stu-id="4cf50-593">![Press Tab to select the highlighted snippet](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="4cf50-594">*Tab 키를 눌러 강조 표시 된 코드 조각 선택*</span><span class="sxs-lookup"><span data-stu-id="4cf50-594">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="4cf50-595">![확장 하 고 Tab 키를 눌러 다시 코드 조각](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "확장 하 고 Tab 키를 눌러 다시 코드 조각")</span><span class="sxs-lookup"><span data-stu-id="4cf50-595">![Press Tab again and the snippet will expand](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="4cf50-596">*확장 하 고 Tab 키를 눌러 다시 코드 조각*</span><span class="sxs-lookup"><span data-stu-id="4cf50-596">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="4cf50-597">***마우스 (C#, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면*** 1입니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-597">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="4cf50-598">코드 조각을 삽입 하려면 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-598">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="4cf50-599">선택 **조각 삽입** 이어서 **내 코드 조각**합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-599">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="4cf50-600">클릭 하 여 목록에서 관련 조각을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cf50-600">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="4cf50-601">![코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추 클릭")</span><span class="sxs-lookup"><span data-stu-id="4cf50-601">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="4cf50-602">*코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭*</span><span class="sxs-lookup"><span data-stu-id="4cf50-602">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="4cf50-603">![클릭 하 여 목록에서 관련 조각을 선택](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "클릭 하 여 목록에서 관련 조각을 선택")</span><span class="sxs-lookup"><span data-stu-id="4cf50-603">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="4cf50-604">*클릭 하 여 목록에서 관련 조각을 선택합니다*</span><span class="sxs-lookup"><span data-stu-id="4cf50-604">*Pick the relevant snippet from the list, by clicking on it*</span></span>
