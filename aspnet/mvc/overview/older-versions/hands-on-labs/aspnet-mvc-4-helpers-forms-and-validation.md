---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
title: ASP.NET MVC 4 도우미, 폼 및 유효성 검사 | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4 모델 및 데이터 액세스 실습에서는 있습니다 로드 되어 데이터베이스에서 데이터를 표시 합니다. 이 실습을 추가 하는 중...
ms.author: aspnetcontent
ms.date: 02/18/2013
ms.assetid: 187ee9cd-bc70-479b-bfed-f568b8da96eb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
msc.type: authoredcontent
ms.openlocfilehash: a84e35695fa08ac1bd4834d2803d2be76f863e5b
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37815923"
---
# <a name="aspnet-mvc-4-helpers-forms-and-validation"></a><span data-ttu-id="66c61-104">ASP.NET MVC 4 도우미, 폼 및 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="66c61-104">ASP.NET MVC 4 Helpers, Forms and Validation</span></span>

<span data-ttu-id="66c61-105">[웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="66c61-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="66c61-106">웹 캠프 학습 키트 다운로드</span><span class="sxs-lookup"><span data-stu-id="66c61-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="66c61-107">**ASP.NET MVC 4 모델 및 데이터 액세스** 실습 랩 되었습니다. 로드 하 고 데이터베이스에서 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-107">In **ASP.NET MVC 4 Models and Data Access** Hands-on Lab, you have been loading and displaying data from the database.</span></span> <span data-ttu-id="66c61-108">이 실습 랩에서를 추가 합니다 **Music Store** 응용 프로그램 데이터를 편집 하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-108">In this Hands-on Lab, you will add to the **Music Store** application the ability to edit that data.</span></span>

<span data-ttu-id="66c61-109">해당 목표를 염두에서에 두고 앨범의 만들기, 읽기, 업데이트 및 삭제 (CRUD) 작업에서 지원 되는 컨트롤러를 먼저 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-109">With that goal in mind, you will first create the controller that will support the Create, Read, Update and Delete (CRUD) actions of albums.</span></span> <span data-ttu-id="66c61-110">HTML 표에 있는 앨범 속성을 표시 하는 ASP.NET MVC 스 캐 폴딩 기능을 활용 하는 인덱스 보기 템플릿을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-110">You will generate an Index View template taking advantage of ASP.NET MVC's scaffolding feature to display the albums' properties in an HTML table.</span></span> <span data-ttu-id="66c61-111">해당 보기를 강화 하려면 긴 설명을 잘립니다 하는 사용자 지정 HTML 도우미를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-111">To enhance that view, you will add a custom HTML helper that will truncate long descriptions.</span></span>

<span data-ttu-id="66c61-112">그런 다음의 편집 및 만들기 보기 수 있는 alter 앨범 드롭다운과 같은 폼 요소 활용 하 여 데이터베이스에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-112">Afterwards, you will add the Edit and Create Views that will let you alter the albums in the database, with the help of form elements like dropdowns.</span></span>

<span data-ttu-id="66c61-113">마지막으로, album을 삭제 하는 데 수는 고 수도 있습니다는 못하도록 해당 입력의 유효성을 검사 하 여 잘못 된 데이터를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-113">Lastly, you will let users delete an album and also you will prevent them from entering wrong data by validating their input.</span></span>

<span data-ttu-id="66c61-114">이 실습 랩 기본 지식이 있다고 가정 **ASP.NET MVC**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-114">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="66c61-115">사용 하지 않은 경우 **ASP.NET MVC** 이전 좋습니다 이동해 **ASP.NET MVC 기본 사항** 실습 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-115">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC Fundamentals** Hands-on Lab.</span></span>

<span data-ttu-id="66c61-116">이 실습을 이용 하면 향상 된 기능 및 원본 폴더에 제공 된 샘플 웹 응용 프로그램에 사소한 변경 내용을 적용 하 여 이전에 설명 된 새 기능을 통해 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-116">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>

> [!NOTE]
> <span data-ttu-id="66c61-117">웹 캠프 교육 키트에서에서 사용할 수 있는 모든 샘플 코드 및 코드 조각 포함 됩니다 [Microsoft-웹/WebCampTrainingKit 릴리스](https://aka.ms/webcamps-training-kit)합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-117">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="66c61-118">이 랩에 특정 프로젝트에서 제공 됩니다 [ASP.NET MVC 4 도우미, 폼 및 유효성 검사](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation)합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-118">The project specific to this lab is available at [ASP.NET MVC 4 Helpers, Forms and Validation](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="66c61-119">목표</span><span class="sxs-lookup"><span data-stu-id="66c61-119">Objectives</span></span>

<span data-ttu-id="66c61-120">이 실습 랩에서 학습할 방법:</span><span class="sxs-lookup"><span data-stu-id="66c61-120">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="66c61-121">CRUD 작업을 지 원하는 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="66c61-121">Create a controller to support CRUD operations</span></span>
- <span data-ttu-id="66c61-122">HTML 테이블에 엔터티 속성을 표시 하는 인덱스 뷰를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-122">Generate an Index View to display entity properties in an HTML table</span></span>
- <span data-ttu-id="66c61-123">사용자 지정 HTML 도우미를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-123">Add a custom HTML helper</span></span>
- <span data-ttu-id="66c61-124">만들기 및 편집 보기를 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="66c61-124">Create and customize an Edit View</span></span>
- <span data-ttu-id="66c61-125">HTTP-GET 또는 HTTP-POST 호출에 대응 하는 작업 메서드를 구별</span><span class="sxs-lookup"><span data-stu-id="66c61-125">Differentiate between action methods that react to either HTTP-GET or HTTP-POST calls</span></span>
- <span data-ttu-id="66c61-126">추가 및 Create View를 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="66c61-126">Add and customize a Create View</span></span>
- <span data-ttu-id="66c61-127">엔터티 삭제를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-127">Handle the deletion of an entity</span></span>
- <span data-ttu-id="66c61-128">사용자 입력 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="66c61-128">Validate user input</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="66c61-129">전제 조건</span><span class="sxs-lookup"><span data-stu-id="66c61-129">Prerequisites</span></span>

<span data-ttu-id="66c61-130">이 랩을 완료 하려면 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-130">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="66c61-131">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) 하거나 그 보다 뛰어난 (읽을 [부록 A](#AppendixA) 설치 하는 방법에 대 한 지침은).</span><span class="sxs-lookup"><span data-stu-id="66c61-131">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="66c61-132">설정</span><span class="sxs-lookup"><span data-stu-id="66c61-132">Setup</span></span>

<span data-ttu-id="66c61-133">**설치 코드 조각**</span><span class="sxs-lookup"><span data-stu-id="66c61-133">**Installing Code Snippets**</span></span>

<span data-ttu-id="66c61-134">편의 위해이 랩에서 함께 관리 하려는 코드의 대부분 제품은 Visual Studio 코드 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-134">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="66c61-135">설치를 실행 하는 코드 조각 **.\Source\Setup\CodeSnippets.vsi** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-135">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="66c61-136">이 문서의 부록 참조할 수 있습니다 사용 하는 방법을 알아보려면 원하는 고 Visual Studio 코드 조각을 사용 하 여 잘 모르는 경우 &quot; [부록 b:를 사용 하 여 코드 조각](#AppendixB)&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-136">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="66c61-137">연습</span><span class="sxs-lookup"><span data-stu-id="66c61-137">Exercises</span></span>

<span data-ttu-id="66c61-138">다음 연습 실습 랩이를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-138">The following exercises make up this Hands-On Lab:</span></span>

1. [<span data-ttu-id="66c61-139">저장소 관리자 컨트롤러 및 해당 인덱스 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="66c61-139">Creating the Store Manager controller and its Index view</span></span>](#Exercise1)
2. [<span data-ttu-id="66c61-140">HTML 도우미를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-140">Adding an HTML Helper</span></span>](#Exercise2)
3. [<span data-ttu-id="66c61-141">편집 보기 만들기</span><span class="sxs-lookup"><span data-stu-id="66c61-141">Creating the Edit View</span></span>](#Exercise3)
4. [<span data-ttu-id="66c61-142">만들기 뷰 추가</span><span class="sxs-lookup"><span data-stu-id="66c61-142">Adding a Create View</span></span>](#Exercise4)
5. [<span data-ttu-id="66c61-143">삭제를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-143">Handling Deletion</span></span>](#Exercise5)
6. [<span data-ttu-id="66c61-144">유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="66c61-144">Adding Validation</span></span>](#Exercise6)
7. [<span data-ttu-id="66c61-145">비 가시적인 jQuery 클라이언트 쪽에서 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="66c61-145">Using Unobtrusive jQuery at Client Side</span></span>](#Exercise7)

> [!NOTE]
> <span data-ttu-id="66c61-146">각 실습 동반 되는 **최종** 연습을 완료 한 후 가져와야 결과 솔루션이 포함 된 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-146">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="66c61-147">이 연습을 진행 하는 추가 도움이 필요한 경우이 솔루션 가이드로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-147">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<span data-ttu-id="66c61-148">이 랩을 완료 하기 위한 예상 시간: **60 분**</span><span class="sxs-lookup"><span data-stu-id="66c61-148">Estimated time to complete this lab: **60 minutes**</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_the_Store_Manager_controller_and_its_Index_view"></a>
### <a name="exercise-1-creating-the-store-manager-controller-and-its-index-view"></a><span data-ttu-id="66c61-149">연습 1: 저장소 관리자 컨트롤러를 만들고 해당 인덱스 보기</span><span class="sxs-lookup"><span data-stu-id="66c61-149">Exercise 1: Creating the Store Manager controller and its Index view</span></span>

<span data-ttu-id="66c61-150">이 연습에서는 CRUD 작업 지원, 데이터베이스 및 마지막으로 ASP.NET MVC 스 캐 폴딩을 활용 하는 인덱스 보기 템플릿을 생성에서 앨범의 목록을 반환 하는 Index 작업 메서드에 사용자 지정 하는 새 컨트롤러를 만드는 방법을 알아봅니다. HTML 표에 있는 앨범 속성을 표시 하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-150">In this exercise, you will learn how to create a new controller to support CRUD operations, customize its Index action method to return a list of albums from the database and finally generating an Index View template taking advantage of ASP.NET MVC's scaffolding feature to display the albums' properties in an HTML table.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_StoreManagerController"></a>
#### <a name="task-1---creating-the-storemanagercontroller"></a><span data-ttu-id="66c61-151">작업 1-는 StoreManagerController 만들기</span><span class="sxs-lookup"><span data-stu-id="66c61-151">Task 1 - Creating the StoreManagerController</span></span>

<span data-ttu-id="66c61-152">이 태스크에서는 라는 새 컨트롤러를 만듭니다 **StoreManagerController** CRUD 작업을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-152">In this task, you will create a new controller called **StoreManagerController** to support CRUD operations.</span></span>

1. <span data-ttu-id="66c61-153">엽니다는 **시작할** 솔루션에 있는 **소스/e x 1-CreatingTheStoreManagerController/시작/** 폴더.</span><span class="sxs-lookup"><span data-stu-id="66c61-153">Open the **Begin** solution located at **Source/Ex1-CreatingTheStoreManagerController/Begin/** folder.</span></span>

   1. <span data-ttu-id="66c61-154">일부 누락 된 NuGet 패키지를 다운로드 해야 하기 전에 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-154">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="66c61-155">이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-155">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="66c61-156">에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="66c61-156">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="66c61-157">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-157">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="66c61-158">NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-158">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="66c61-159">NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-159">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="66c61-160">이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-160">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="66c61-161">새 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-161">Add a new controller.</span></span> <span data-ttu-id="66c61-162">이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 **컨트롤러** 선택 솔루션 탐색기 내에서 폴더 **추가** 차례로 **컨트롤러** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-162">To do this, right-click the **Controllers** folder within the Solution Explorer, select **Add** and then the **Controller** command.</span></span> <span data-ttu-id="66c61-163">변경 된 **컨트롤러** **이름** 에 **StoreManagerController** 옵션을 확인 하 고 **빈읽기/쓰기동작이포함된MVC컨트롤러**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-163">Change the **Controller** **Name** to **StoreManagerController** and make sure the option **MVC controller with empty read/write actions** is selected.</span></span> <span data-ttu-id="66c61-164">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-164">Click **Add**.</span></span>

    <span data-ttu-id="66c61-165">![추가 컨트롤러 대화](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "추가 컨트롤러 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="66c61-165">![Add controller dialog](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "Add controller dialog")</span></span>

    <span data-ttu-id="66c61-166">*컨트롤러 추가 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="66c61-166">*Add Controller Dialog*</span></span>

    <span data-ttu-id="66c61-167">컨트롤러 클래스가 새로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-167">A new Controller class is generated.</span></span> <span data-ttu-id="66c61-168">읽기/쓰기를 위한 스텁 메서드에 대 한 작업을 추가 하려면 표시 하므로 일반적인 CRUD 작업 TODO 주석 입력 응용 프로그램별 논리를 포함 하는 메시지를 사용 하 여 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-168">Since you indicated to add actions for read/write, stub methods for those, common CRUD actions are created with TODO comments filled in, prompting to include the application specific logic.</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Customizing_the_StoreManager_Index"></a>
#### <a name="task-2---customizing-the-storemanager-index"></a><span data-ttu-id="66c61-169">작업 2-StoreManager 인덱스를 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="66c61-169">Task 2 - Customizing the StoreManager Index</span></span>

<span data-ttu-id="66c61-170">이 태스크에서는 데이터베이스에서 앨범의 목록으로 보기를 반환할 StoreManager Index 작업 메서드에 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-170">In this task, you will customize the StoreManager Index action method to return a View with the list of albums from the database.</span></span>

1. <span data-ttu-id="66c61-171">StoreManagerController 클래스에 다음을 추가 *를 사용 하 여* 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-171">In the StoreManagerController class, add the following *using* directives.</span></span>

    <span data-ttu-id="66c61-172">(코드 조각- *ASP.NET MVC 4 도우미, 폼 및 유효성 검사-e x 1 MvcMusicStore를 사용 하 여*)</span><span class="sxs-lookup"><span data-stu-id="66c61-172">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 using MvcMusicStore*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample1.cs)]
2. <span data-ttu-id="66c61-173">필드를 추가 합니다 **StoreManagerController** 의 인스턴스를 보관할 **MusicStoreEntities 합니다.**</span><span class="sxs-lookup"><span data-stu-id="66c61-173">Add a field to the **StoreManagerController** to hold an instance of **MusicStoreEntities.**</span></span>

    <span data-ttu-id="66c61-174">(코드 조각- *ASP.NET MVC 4 도우미, 폼 및 유효성 검사-e x 1 MusicStoreEntities*)</span><span class="sxs-lookup"><span data-stu-id="66c61-174">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 MusicStoreEntities*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample2.cs)]
3. <span data-ttu-id="66c61-175">앨범의 목록으로 보기를 반환할 StoreManagerController 인덱스 작업을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-175">Implement the StoreManagerController Index action to return a View with the list of albums.</span></span>

    <span data-ttu-id="66c61-176">컨트롤러 작업 논리 작성 이전 StoreController의 인덱스 작업에 매우 비슷할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-176">The Controller action logic will be very similar to the StoreController's Index action written earlier.</span></span> <span data-ttu-id="66c61-177">표시에 대 한 장르 및 음악가 정보를 포함 하 여 모든 앨범 검색할 LINQ를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-177">Use LINQ to retrieve all albums, including Genre and Artist information for display.</span></span>

    <span data-ttu-id="66c61-178">(코드 조각- *ASP.NET MVC 4 도우미, 폼 및 유효성 검사-e x 1 StoreManagerController 인덱스*)</span><span class="sxs-lookup"><span data-stu-id="66c61-178">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 StoreManagerController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample3.cs)]

<a id="Ex1Task3"></a>

<a id="strongTask_3_-_Creating_the_Index_Viewstrong"></a>
#### <a name="task-3---creating-the-index-view"></a><span data-ttu-id="66c61-179">작업 3-인덱스 보기 만들기</span><span class="sxs-lookup"><span data-stu-id="66c61-179">Task 3 - Creating the Index View</span></span>

<span data-ttu-id="66c61-180">이 작업에서 반환한 앨범의 목록을 표시 하려면 인덱스 보기 템플릿을 만들지 합니다 **StoreManager** 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-180">In this task, you will create the Index View template to display the list of albums returned by the **StoreManager** Controller.</span></span>

1. <span data-ttu-id="66c61-181">새 템플릿 보기를 만들기 전에 프로젝트를 작성 해야 있도록를 **추가 보기 대화 상자** 알고 합니다 **앨범** 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-181">Before creating the new View template, you should build the project so that the **Add View Dialog** knows about the **Album** class to use.</span></span> <span data-ttu-id="66c61-182">선택 **빌드 | 빌드 MvcMusicStore** 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-182">Select **Build | Build MvcMusicStore** to build the project.</span></span>
2. <span data-ttu-id="66c61-183">마우스 오른쪽 단추로 클릭 합니다 **인덱스** 선택한 동작 메서드가 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-183">Right-click inside the **Index** action method and select **Add View**.</span></span> <span data-ttu-id="66c61-184">그러면 합니다 **뷰 추가** 대화 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-184">This will bring up the **Add View** dialog.</span></span>

    <span data-ttu-id="66c61-185">![뷰 추가](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "뷰 추가")</span><span class="sxs-lookup"><span data-stu-id="66c61-185">![Add view](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "Add view")</span></span>

    <span data-ttu-id="66c61-186">*인덱스 메서드 내에서 뷰 추가*</span><span class="sxs-lookup"><span data-stu-id="66c61-186">*Adding a View from within the Index method*</span></span>
3. <span data-ttu-id="66c61-187">뷰 추가 대화 상자에서 보기 이름 인지를 확인 **인덱스**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-187">In the Add View dialog, verify that the View Name is **Index**.</span></span> <span data-ttu-id="66c61-188">선택 합니다 **강력한 형식의 뷰를 만들** 옵션을 선택 **앨범 (MvcMusicStore.Models)** 에서 **모델 클래스** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-188">Select the **Create a strongly-typed view** option, and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down.</span></span> <span data-ttu-id="66c61-189">선택 **목록을** 에서 합니다 **스 캐 폴드 템플릿** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-189">Select **List** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="66c61-190">유지 된 **뷰 엔진** 에 **Razor** 기본값을 사용 하 여 다른 필드 값을 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-190">Leave the **View engine** to **Razor** and the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="66c61-191">![인덱스 뷰를 추가](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "인덱스 뷰를 추가 합니다.")</span><span class="sxs-lookup"><span data-stu-id="66c61-191">![Adding an index view](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "Adding an index view")</span></span>

    <span data-ttu-id="66c61-192">*인덱스 뷰를 추가합니다.*</span><span class="sxs-lookup"><span data-stu-id="66c61-192">*Adding an Index View*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Customizing_the_scaffold_of_the_Index_View"></a>
#### <a name="task-4---customizing-the-scaffold-of-the-index-view"></a><span data-ttu-id="66c61-193">작업 4-인덱스 뷰의 스 캐 폴드를 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="66c61-193">Task 4 - Customizing the scaffold of the Index View</span></span>

<span data-ttu-id="66c61-194">이 작업에서는 원하는 필드를 표시 하도록 ASP.NET MVC 스 캐 폴딩 기능을 사용 하 여 만든 간단한 보기 템플릿이 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-194">In this task, you will adjust the simple View template created with ASP.NET MVC scaffolding feature to have it display the fields you want.</span></span>

> [!NOTE]
> <span data-ttu-id="66c61-195">합니다 **스 캐 폴딩** ASP.NET MVC에서 지원 앨범 모델에서 모든 필드를 나열 하는 간단한 보기 템플릿을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-195">The **scaffolding** support within ASP.NET MVC generates a simple View template which lists all fields in the Album model.</span></span> <span data-ttu-id="66c61-196">**스 캐 폴딩** 강력한 형식의 뷰를 시작 하는 빠른 방법을 제공 합니다: 템플릿 보기를 수동으로 작성 하는 대신 기본 템플릿이 생성 신속 하 게 스 캐 폴딩 하 고 그런 다음 생성된 된 코드를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-196">**Scaffolding** provides a quick way to get started on a strongly typed view: rather than having to write the View template manually, scaffolding quickly generates a default template and then you can modify the generated code.</span></span>


1. <span data-ttu-id="66c61-197">작성 한 코드를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-197">Review the code created.</span></span> <span data-ttu-id="66c61-198">생성 된 필드 목록에는 다음의 일부가 될 HTML 테이블 **스 캐 폴딩** 를 표 형식 데이터를 표시 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-198">The generated list of fields will be part of the following HTML table that **Scaffolding** is using for displaying tabular data.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample4.cshtml)]
2. <span data-ttu-id="66c61-199">대체는 **&lt;테이블&gt;** 만 표시 하는 다음 코드를 사용 하 여 코드를 **장르**를 **음악가**, **앨범 제목**, 및 **가격** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-199">Replace the **&lt;table&gt;** code with the following code to display only the **Genre**, **Artist**, **Album Title**, and **Price** fields.</span></span> <span data-ttu-id="66c61-200">이 삭제 합니다 **AlbumId** 하 고 **앨범 아트 URL** 열.</span><span class="sxs-lookup"><span data-stu-id="66c61-200">This deletes the **AlbumId** and **Album Art URL** columns.</span></span> <span data-ttu-id="66c61-201">GenreId 및 ArtistId 표시할 열을 해당 연결 된 클래스 속성의 변경 뿐만 **Artist.Name** 및 **Genre.Name**를 제거 합니다 **세부 정보** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-201">Also, it changes GenreId and ArtistId columns to display their linked class properties of **Artist.Name** and **Genre.Name**, and removes the **Details** link.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample5.cshtml)]
3. <span data-ttu-id="66c61-202">다음 설명을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-202">Change the following descriptions.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample6.cshtml)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="66c61-203">작업 5-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="66c61-203">Task 5 - Running the Application</span></span>

<span data-ttu-id="66c61-204">이 작업을 테스트 하는 **StoreManager** **인덱스** 템플릿 보기에는 이전 단계의 디자인에 따라 앨범 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-204">In this task, you will test that the **StoreManager** **Index** View template displays a list of albums according to the design of the previous steps.</span></span>

1. <span data-ttu-id="66c61-205">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-205">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="66c61-206">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-206">The project starts in the Home page.</span></span> <span data-ttu-id="66c61-207">URL을 변경 **/StoreManager** 보여 주는 앨범의 목록을 표시 되는지 확인 하려면 해당 **Title**, **Artist** 및 **장르**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-207">Change the URL to **/StoreManager** to verify that a list of albums is displayed, showing their **Title**, **Artist** and **Genre**.</span></span>

    <span data-ttu-id="66c61-208">![앨범의 목록 검색](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "앨범의 목록 검색")</span><span class="sxs-lookup"><span data-stu-id="66c61-208">![Browsing the list of albums](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "Browsing the list of albums")</span></span>

    <span data-ttu-id="66c61-209">*앨범의 목록 검색*</span><span class="sxs-lookup"><span data-stu-id="66c61-209">*Browsing the list of albums*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Adding_an_HTML_Helper"></a>
### <a name="exercise-2-adding-an-html-helper"></a><span data-ttu-id="66c61-210">연습 2:는 HTML 도우미를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-210">Exercise 2: Adding an HTML Helper</span></span>

<span data-ttu-id="66c61-211">StoreManager 인덱스 페이지는 한 가지 잠재적인 문제가: 제목과 Artist 이름 속성은 모두 테이블 서식 지정에 충분 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-211">The StoreManager Index page has one potential issue: Title and Artist Name properties can both be long enough to throw off the table formatting.</span></span> <span data-ttu-id="66c61-212">이 연습에서 해당 텍스트를 자를 사용자 지정 HTML 도우미를 추가 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-212">In this exercise you will learn how to add a custom HTML helper to truncate that text.</span></span>

<span data-ttu-id="66c61-213">다음 그림에서는 작은 브라우저 크기를 사용 하는 경우 형식으로 텍스트의 길이 때문 수정 하는 방법을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-213">In the following figure, you can see how the format is modified because of the length of the text when you use a small browser size.</span></span>

<span data-ttu-id="66c61-214">![와 앨범의 목록 검색 텍스트가 잘리지](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "텍스트가 잘리지와 앨범의 목록 검색")</span><span class="sxs-lookup"><span data-stu-id="66c61-214">![Browsing the list of Albums with not truncated text](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "Browsing the list of Albums with not truncated text")</span></span>

<span data-ttu-id="66c61-215">*텍스트가 잘리지와 앨범의 목록 검색*</span><span class="sxs-lookup"><span data-stu-id="66c61-215">*Browsing the list of Albums with not truncated text*</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Extending_the_HTML_Helper"></a>
#### <a name="task-1---extending-the-html-helper"></a><span data-ttu-id="66c61-216">작업 1-확장 된 HTML 도우미</span><span class="sxs-lookup"><span data-stu-id="66c61-216">Task 1 - Extending the HTML Helper</span></span>

<span data-ttu-id="66c61-217">이 태스크에서는 새 메서드를 추가 합니다 **Truncate** 에 **HTML** ASP.NET MVC 뷰 내에서 노출 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-217">In this task, you will add a new method **Truncate** to the **HTML** object exposed within ASP.NET MVC Views.</span></span> <span data-ttu-id="66c61-218">이렇게 하려면 구현 합니다는 **확장 메서드** 기본 제공 **System.Web.Mvc.HtmlHelper** ASP.NET MVC에서 제공 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-218">To do this, you will implement an **extension method** to the built-in **System.Web.Mvc.HtmlHelper** class provided by ASP.NET MVC.</span></span>

> [!NOTE]
> <span data-ttu-id="66c61-219">에 대 한 자세한 **확장 메서드**,이 msdn 문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="66c61-219">To read more about **Extension Methods**, please visit this msdn article.</span></span> <span data-ttu-id="66c61-220">[https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx).</span><span class="sxs-lookup"><span data-stu-id="66c61-220">[https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx).</span></span>


1. <span data-ttu-id="66c61-221">엽니다는 **시작할** 솔루션에 있는 **소스/e x 2-AddingAnHTMLHelper/시작/** 폴더.</span><span class="sxs-lookup"><span data-stu-id="66c61-221">Open the **Begin** solution located at **Source/Ex2-AddingAnHTMLHelper/Begin/** folder.</span></span> <span data-ttu-id="66c61-222">그렇지 않은 경우 계속 사용할 수도 있습니다는 **최종** 이전 연습을 완료 하 여 가져온 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-222">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="66c61-223">제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-223">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="66c61-224">이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-224">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="66c61-225">에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="66c61-225">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="66c61-226">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-226">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="66c61-227">NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-227">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="66c61-228">NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-228">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="66c61-229">이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-229">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="66c61-230">StoreManager의 인덱스 뷰를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-230">Open StoreManager's Index View.</span></span> <span data-ttu-id="66c61-231">이렇게 하려면 솔루션 탐색기에서 확장 하 고는 **뷰** 폴더를 해당 **StoreManager** 연 합니다 **Index.cshtml** 파일.</span><span class="sxs-lookup"><span data-stu-id="66c61-231">To do this, in the Solution Explorer expand the **Views** folder, then the **StoreManager** and open the **Index.cshtml** file.</span></span>
3. <span data-ttu-id="66c61-232">아래 다음 코드를 추가 합니다 <strong>@model</strong> 지시어 정의할 수는 <strong>Truncate</strong> 도우미 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-232">Add the following code below the <strong>@model</strong> directive to define the <strong>Truncate</strong> helper method.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample7.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Truncating_Text_in_the_Page"></a>
#### <a name="task-2---truncating-text-in-the-page"></a><span data-ttu-id="66c61-233">작업 2-페이지에서 텍스트를 잘라내기</span><span class="sxs-lookup"><span data-stu-id="66c61-233">Task 2 - Truncating Text in the Page</span></span>

<span data-ttu-id="66c61-234">이 작업을 사용 하 여 합니다 **Truncate** 보기 템플릿에서 텍스트를 잘라내려면 메서드.</span><span class="sxs-lookup"><span data-stu-id="66c61-234">In this task, you will use the **Truncate** method to truncate the text in the View template.</span></span>

1. <span data-ttu-id="66c61-235">StoreManager의 인덱스 뷰를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-235">Open StoreManager's Index View.</span></span> <span data-ttu-id="66c61-236">이렇게 하려면 솔루션 탐색기에서 확장 하 고는 **뷰** 폴더를 해당 **StoreManager** 연 합니다 **Index.cshtml** 파일.</span><span class="sxs-lookup"><span data-stu-id="66c61-236">To do this, in the Solution Explorer expand the **Views** folder, then the **StoreManager** and open the **Index.cshtml** file.</span></span>
2. <span data-ttu-id="66c61-237">줄을 표시 합니다 **Artist 이름** 및 앨범 **제목**.</span><span class="sxs-lookup"><span data-stu-id="66c61-237">Replace the lines that show the **Artist Name** and Album's **Title**.</span></span> <span data-ttu-id="66c61-238">이 작업을 수행 하려면 다음 줄을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-238">To do this, replace the following lines.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample8.cshtml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="66c61-239">작업 3-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="66c61-239">Task 3 - Running the Application</span></span>

<span data-ttu-id="66c61-240">이 작업을 테스트 하는 **StoreManager** **인덱스** 템플릿 보기 앨범의 제목과 Artist 이름을 자릅니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-240">In this task, you will test that the **StoreManager** **Index** View template truncates the Album's Title and Artist Name.</span></span>

1. <span data-ttu-id="66c61-241">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-241">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="66c61-242">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-242">The project starts in the Home page.</span></span> <span data-ttu-id="66c61-243">URL을 변경 **/StoreManager** 는 확인 하려면에서 텍스트를 **Title** 및 **Artist** 열은 잘립니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-243">Change the URL to **/StoreManager** to verify that long texts in the **Title** and **Artist** column are truncated.</span></span>

    <span data-ttu-id="66c61-244">![제목 및 아티스트가 이름이 잘립니다](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "제목 및 아티스트가 이름이 잘립니다")</span><span class="sxs-lookup"><span data-stu-id="66c61-244">![Truncated titles and artists names](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "Truncated titles and artists names")</span></span>

    <span data-ttu-id="66c61-245">*잘린 제목과 Artist 이름*</span><span class="sxs-lookup"><span data-stu-id="66c61-245">*Truncated Titles and Artist Names*</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Creating_the_Edit_View"></a>
### <a name="exercise-3-creating-the-edit-view"></a><span data-ttu-id="66c61-246">편집 뷰를 만드는 연습 3:</span><span class="sxs-lookup"><span data-stu-id="66c61-246">Exercise 3: Creating the Edit View</span></span>

<span data-ttu-id="66c61-247">이 연습에서는 저장소 관리자 앨범을 편집할 수 있도록 폼을 만드는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-247">In this exercise, you will learn how to create a form to allow store managers to edit an Album.</span></span> <span data-ttu-id="66c61-248">찾아볼 합니다 **/StoreManager/Edit/id** URL (**id** 편집 앨범의 고유 id가), 서버에 대 한 HTTP GET 호출 하므로.</span><span class="sxs-lookup"><span data-stu-id="66c61-248">They will browse the **/StoreManager/Edit/id** URL (**id** being the unique id of the album to edit), thus making an HTTP-GET call to the server.</span></span>

<span data-ttu-id="66c61-249">컨트롤러 편집 작업 메서드는 데이터베이스에서 적절 한 앨범을 검색, 만들기를 **StoreManagerViewModel** (목록과 함께 아티스트, 장르)를 캡슐화 하 고 다음 전달 하기 위해 뷰 템플릿을 개체 다시 사용자에 게 HTML 페이지를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-249">The Controller Edit action method will retrieve the appropriate Album from the database, create a **StoreManagerViewModel** object to encapsulate it (along with a list of Artists and Genres), and then pass it off to a View template to render the HTML page back to the user.</span></span> <span data-ttu-id="66c61-250">이 페이지에 포함 됩니다는 **&lt;양식&gt;** 텍스트 상자 및 앨범 속성을 편집 하는 것에 대 한 드롭다운을 사용 하 여 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-250">This page will contain a **&lt;form&gt;** element with textboxes and dropdowns for editing the Album properties.</span></span>

<span data-ttu-id="66c61-251">사용자 앨범 양식 값을 업데이트 하 고 클릭 합니다 **저장** 의 변경 내용을 통해 제출 단추를 HTTP POST를 콜백할 **/StoreManager/Edit/id**. URL 마지막 호출에서와 동일 하지만, ASP.NET MVC 식별 하는 HTTP POST 이며 따라서 다양 한 편집 작업 메서드 실행이 시간 (하나 데코 레이트 **[HttpPost]**).</span><span class="sxs-lookup"><span data-stu-id="66c61-251">Once the user updates the Album form values and clicks the **Save** button, the changes are submitted via an HTTP-POST call back to **/StoreManager/Edit/id**. Although the URL remains the same as in the last call, ASP.NET MVC identifies that this time it is an HTTP-POST and therefore executes a different Edit action method (one decorated with **[HttpPost]**).</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Edit_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-edit-action-method"></a><span data-ttu-id="66c61-252">작업 1-HTTP-GET 편집 작업 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-252">Task 1 - Implementing the HTTP-GET Edit Action Method</span></span>

<span data-ttu-id="66c61-253">이 작업에서는 HTTP GET 버전의 데이터베이스에서 적절 한 앨범 검색할 편집 작업 메서드 뿐 아니라 모든 장르 및 아티스트가 목록을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-253">In this task, you will implement the HTTP-GET version of the Edit action method to retrieve the appropriate Album from the database, as well as a list of all Genres and Artists.</span></span> <span data-ttu-id="66c61-254">이 패키징하고이 데이터에는 **StoreManagerViewModel** 다음 전달할 뷰 템플릿을 사용 하 여 응답을 렌더링 하는 마지막 단계에서 정의 된 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-254">It will package this data up into the **StoreManagerViewModel** object defined in the last step, which will then be passed to a View template to render the response with.</span></span>

1. <span data-ttu-id="66c61-255">엽니다는 **시작할** 솔루션에 있는 **소스/Ex3-CreatingTheEditView/시작/** 폴더.</span><span class="sxs-lookup"><span data-stu-id="66c61-255">Open the **Begin** solution located at **Source/Ex3-CreatingTheEditView/Begin/** folder.</span></span> <span data-ttu-id="66c61-256">그렇지 않은 경우 계속 사용할 수도 있습니다는 **최종** 이전 연습을 완료 하 여 가져온 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-256">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="66c61-257">제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-257">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="66c61-258">이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-258">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="66c61-259">에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="66c61-259">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="66c61-260">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-260">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="66c61-261">NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-261">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="66c61-262">NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-262">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="66c61-263">이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-263">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="66c61-264">엽니다는 **StoreManagerController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-264">Open the **StoreManagerController** class.</span></span> <span data-ttu-id="66c61-265">이 작업을 수행 하려면 확장 합니다 **컨트롤러** 폴더를 두 번 클릭 **StoreManagerController.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-265">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="66c61-266">대체는 **HTTP-GET 편집** 적절 한 검색 하는 다음 코드를 사용 하 여 작업 메서드에 **앨범** 뿐 **장르** 및 **아티스트**나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-266">Replace the **HTTP-GET Edit** action method with the following code to retrieve the appropriate **Album** as well as the **Genres** and **Artists** lists.</span></span>

    <span data-ttu-id="66c61-267">(코드 조각- *ASP.NET MVC 4 도우미, 폼과 유효성 검사 동작 Ex3 StoreManagerController HTTP-GET 편집*)</span><span class="sxs-lookup"><span data-stu-id="66c61-267">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex3 StoreManagerController HTTP-GET Edit action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample9.cs)]

    > [!NOTE]
    > <span data-ttu-id="66c61-268">사용 중인 **System.Web.Mvc** **SelectList** 아티스트, 대신 장르에 대 한 합니다 **System.Collections.Generic** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-268">You are using **System.Web.Mvc** **SelectList** for Artists and Genres instead of the **System.Collections.Generic** List.</span></span>
    > 
    > <span data-ttu-id="66c61-269">**SelectList** HTML 드롭다운을 채우고 등 현재 선택 영역을 관리 하는 깔끔한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-269">**SelectList** is a cleaner way to populate HTML dropdowns and manage things like current selection.</span></span> <span data-ttu-id="66c61-270">인스턴스화하고 컨트롤러 작업에서 이러한 ViewModel 개체를 이상 설정 하 게 편집 양식 시나리오를 청소 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-270">Instantiating and later setting up these ViewModel objects in the controller action will make the Edit form scenario cleaner.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Creating_the_Edit_View"></a>
#### <a name="task-2---creating-the-edit-view"></a><span data-ttu-id="66c61-271">작업 2-편집 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="66c61-271">Task 2 - Creating the Edit View</span></span>

<span data-ttu-id="66c61-272">이 태스크에서는 나중에 album 속성을 표시 하는 편집 보기 템플릿을 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-272">In this task, you will create an Edit View template that will later display the album properties.</span></span>

1. <span data-ttu-id="66c61-273">편집 보기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-273">Create the Edit View.</span></span> <span data-ttu-id="66c61-274">이렇게 하려면 마우스 오른쪽 단추로 클릭 합니다 **편집** 선택한 동작 메서드가 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-274">To do this, right-click inside the **Edit** action method and select **Add View**.</span></span>
2. <span data-ttu-id="66c61-275">뷰 추가 대화 상자에서 보기 이름 인지를 확인 **편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-275">In the Add View dialog, verify that the View Name is **Edit**.</span></span> <span data-ttu-id="66c61-276">확인는 **강력한 형식의 뷰를 만들** 확인란을 선택한 **앨범 (MvcMusicStore.Models)** 에서 **데이터 클래스 보기** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-276">Check the **Create a strongly-typed view** checkbox and select **Album (MvcMusicStore.Models)** from the **View data class** drop-down.</span></span> <span data-ttu-id="66c61-277">선택 **편집할** 에서 **스 캐 폴드 템플릿** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-277">Select **Edit** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="66c61-278">기본값을 사용 하 여 다른 필드를 그대로 두고을 누릅니다 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-278">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="66c61-279">![편집 뷰 추가](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "편집 뷰 추가")</span><span class="sxs-lookup"><span data-stu-id="66c61-279">![Adding an Edit view](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "Adding an Edit view")</span></span>

    <span data-ttu-id="66c61-280">*편집 뷰 추가*</span><span class="sxs-lookup"><span data-stu-id="66c61-280">*Adding an Edit view*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="66c61-281">작업 3-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="66c61-281">Task 3 - Running the Application</span></span>

<span data-ttu-id="66c61-282">이 작업을 테스트 하는 **StoreManager** **편집** 보기 페이지에 매개 변수로 전달 된 앨범에 대 한 속성의 값이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-282">In this task, you will test that the **StoreManager** **Edit** View page displays the properties' values for the album passed as parameter.</span></span>

1. <span data-ttu-id="66c61-283">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-283">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="66c61-284">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-284">The project starts in the Home page.</span></span> <span data-ttu-id="66c61-285">URL을 변경 **/StoreManager/Edit/1** 에 전달 된 앨범에 대 한 속성의 값이 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-285">Change the URL to **/StoreManager/Edit/1** to verify that the properties' values for the album passed are displayed.</span></span>

    <span data-ttu-id="66c61-286">![앨범의 편집 보기를 탐색](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "앨범의 편집 보기를 검색 합니다.")</span><span class="sxs-lookup"><span data-stu-id="66c61-286">![Browsing Album's Edit View](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "Browsing Album's Edit View")</span></span>

    <span data-ttu-id="66c61-287">*앨범의 편집 보기를 검색합니다.*</span><span class="sxs-lookup"><span data-stu-id="66c61-287">*Browsing Album's Edit view*</span></span>

<a id="Ex3Task4"></a>

<a id="Task_4_-_Implementing_drop-downs_on_the_Album_Editor_Template"></a>
#### <a name="task-4---implementing-drop-downs-on-the-album-editor-template"></a><span data-ttu-id="66c61-288">작업 4-앨범 편집기 템플릿의 드롭다운 구현</span><span class="sxs-lookup"><span data-stu-id="66c61-288">Task 4 - Implementing drop-downs on the Album Editor Template</span></span>

<span data-ttu-id="66c61-289">이 태스크에서는 추가할 사항이 드롭다운 마지막 작업에서 만든 뷰 템플릿을 아티스트, 장르 목록에서 선택할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-289">In this task, you will add drop-downs to the View template created in the last task, so that the user can select from a list of Artists and Genres.</span></span>

1. <span data-ttu-id="66c61-290">모두 바꾸기 합니다 **앨범** 필드 집합 코드를 다음:</span><span class="sxs-lookup"><span data-stu-id="66c61-290">Replace all the **Album** fieldset code with the following:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample10.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="66c61-291">**Html.DropDownList** 도우미 아티스트, 장르를 선택 하기 위한 드롭다운 렌더링에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-291">An **Html.DropDownList** helper has been added to render drop-downs for choosing Artists and Genres.</span></span> <span data-ttu-id="66c61-292">매개 변수를 전달할 **Html.DropDownList** 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-292">The parameters passed to **Html.DropDownList** are:</span></span>
    > 
    > 1. <span data-ttu-id="66c61-293">폼 필드의 이름 (**&quot;ArtistId&quot;**).</span><span class="sxs-lookup"><span data-stu-id="66c61-293">The name of the form field (**&quot;ArtistId&quot;**).</span></span>
    > 2. <span data-ttu-id="66c61-294">합니다 **SelectList** 드롭다운 목록에 대 한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-294">The **SelectList** of values for the drop-down.</span></span>

<a id="Ex3Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="66c61-295">작업 5-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="66c61-295">Task 5 - Running the Application</span></span>

<span data-ttu-id="66c61-296">이 작업을 테스트 하는 **StoreManager** **편집** 보기 페이지 음악가 및 장르 ID 텍스트 필드 대신 드롭다운에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-296">In this task, you will test that the **StoreManager** **Edit** View page displays drop-downs instead of Artist and Genre ID text fields.</span></span>

1. <span data-ttu-id="66c61-297">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-297">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="66c61-298">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-298">The project starts in the Home page.</span></span> <span data-ttu-id="66c61-299">URL을 변경 **/StoreManager/Edit/1** 음악가 및 장르 ID 텍스트 필드 대신 드롭다운 표시를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-299">Change the URL to **/StoreManager/Edit/1** to verify that it displays drop-downs instead of Artist and Genre ID text fields.</span></span>

    <span data-ttu-id="66c61-300">![앨범의 드롭다운을 사용 하 여 뷰 편집 찾아보기](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "검색 앨범의 드롭다운을 사용 하 여 뷰 편집")</span><span class="sxs-lookup"><span data-stu-id="66c61-300">![Browsing Album's Edit View with drop downs](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "Browsing Album's Edit View with drop downs")</span></span>

    <span data-ttu-id="66c61-301">*앨범의 편집 보기 드롭다운을 사용 하 여이 시간 검색*</span><span class="sxs-lookup"><span data-stu-id="66c61-301">*Browsing Album's Edit view, this time with dropdowns*</span></span>

<a id="Ex3Task6"></a>

<a id="Task_6_-_Implementing_the_HTTP-POST_Edit_action_method"></a>
#### <a name="task-6---implementing-the-http-post-edit-action-method"></a><span data-ttu-id="66c61-302">태스크 6-HTTP-POST 편집 작업 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-302">Task 6 - Implementing the HTTP-POST Edit action method</span></span>

<span data-ttu-id="66c61-303">편집 보기에는 예상 대로 표시 됩니다, 했으므로 Album에 변경한 내용을 저장 하려면 작업을 편집 하는 HTTP POST 메서드를 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-303">Now that the Edit View displays as expected, you need to implement the HTTP-POST Edit Action method to save the changes made to the Album.</span></span>

1. <span data-ttu-id="66c61-304">Visual Studio 창으로 돌아가려면 필요한 경우 브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-304">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="66c61-305">오픈 **StoreManagerController** 에서 합니다 **컨트롤러** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-305">Open **StoreManagerController** from the **Controllers** folder.</span></span>
2. <span data-ttu-id="66c61-306">바꿉니다 **HTTP-POST 편집** 작업 메서드 코드를 다음 (참고: 교체 해야 하는 메서드는 두 개의 매개 변수를 받는 오버 로드 된 버전):</span><span class="sxs-lookup"><span data-stu-id="66c61-306">Replace **HTTP-POST Edit** action method code with the following (note that the method that must be replaced is overloaded version that receives two parameters):</span></span>

    <span data-ttu-id="66c61-307">(코드 조각- *ASP.NET MVC 4 도우미, 폼과 유효성 검사 동작 Ex3 StoreManagerController HTTP-POST 편집*)</span><span class="sxs-lookup"><span data-stu-id="66c61-307">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex3 StoreManagerController HTTP-POST Edit action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample11.cs)]

    > [!NOTE]
    > <span data-ttu-id="66c61-308">이 메서드는 사용자가 클릭할 때 실행 됩니다는 **저장** 뷰의 단추는 HTTP 게시 서버에 다시 폼 값의 데이터베이스에 유지 하도록 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-308">This method will be executed when the user clicks the **Save** button of the View and performs an HTTP-POST of the form values back to the server to persist them in the database.</span></span> <span data-ttu-id="66c61-309">데코레이터 **[HttpPost]** 이러한 HTTP POST 시나리오에 메서드를 사용 해야을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-309">The decorator **[HttpPost]** indicates that the method should be used for those HTTP-POST scenarios.</span></span> <span data-ttu-id="66c61-310">메서드는 **앨범** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-310">The method takes an **Album** object.</span></span> <span data-ttu-id="66c61-311">ASP.NET MVC는 게시 된에서 앨범 개체를 자동으로 생성 됩니다 &lt;폼&gt; 값입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-311">ASP.NET MVC will automatically create the Album object from the posted &lt;form&gt; values.</span></span>
    > 
    > <span data-ttu-id="66c61-312">메서드는 이러한 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-312">The method will perform these steps:</span></span>
    > 
    > 1. <span data-ttu-id="66c61-313">모델이 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-313">If model is valid:</span></span>
    > 
    >     1. <span data-ttu-id="66c61-314">수정 된 개체로 표시 컨텍스트에서 앨범 항목을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-314">Update the album entry in the context to mark it as a modified object.</span></span>
    >     2. <span data-ttu-id="66c61-315">변경 내용을 저장 하 고 인덱스 보기를 리디렉션하십시오.</span><span class="sxs-lookup"><span data-stu-id="66c61-315">Save the changes and redirect to the index view.</span></span>
    > 2. <span data-ttu-id="66c61-316">사용 하 여 ViewBag을 채워집니다 모델 올바르지 않으면 합니다 **GenreId** 및 **ArtistId**, 뷰 사용자 수 있도록 받은 앨범 개체를 반환 됩니다 모든 필수 업데이트를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-316">If the model is not valid, it will populate the ViewBag with the **GenreId** and **ArtistId**, then it will return the view with the received Album object to allow the user perform any required update.</span></span>

<a id="Ex3Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a><span data-ttu-id="66c61-317">태스크 7-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="66c61-317">Task 7 - Running the Application</span></span>

<span data-ttu-id="66c61-318">이 작업을 테스트 하는 **StoreManager 편집** 뷰 페이지는 데이터베이스에 실제로 업데이트 된 앨범 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-318">In this task, you will test that the **StoreManager Edit** View page actually saves the updated Album data in the database.</span></span>

1. <span data-ttu-id="66c61-319">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-319">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="66c61-320">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-320">The project starts in the Home page.</span></span> <span data-ttu-id="66c61-321">URL을 변경 **/StoreManager/Edit/1**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-321">Change the URL to **/StoreManager/Edit/1**.</span></span> <span data-ttu-id="66c61-322">앨범 제목을 변경 **부하** 를 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-322">Change the Album title to **Load** and click on **Save**.</span></span> <span data-ttu-id="66c61-323">앨범 제목 앨범의 목록에서 실제로 변경 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-323">Verify that album's title actually changed in the list of albums.</span></span>

    <span data-ttu-id="66c61-324">![업데이트 앨범](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "앨범을 업데이트 하는 중")</span><span class="sxs-lookup"><span data-stu-id="66c61-324">![Updating an album](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "Updating an album")</span></span>

    <span data-ttu-id="66c61-325">*앨범을 업데이트 하는 중*</span><span class="sxs-lookup"><span data-stu-id="66c61-325">*Updating an Album*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Adding_a_Create_View"></a>
### <a name="exercise-4-adding-a-create-view"></a><span data-ttu-id="66c61-326">실습 4: 만들기 뷰 추가</span><span class="sxs-lookup"><span data-stu-id="66c61-326">Exercise 4: Adding a Create View</span></span>

<span data-ttu-id="66c61-327">이제는 **StoreManagerController** 지원 합니다 **편집** 저장할 수 있도록 Create View 템플릿을 추가 하는 방법을 배우게 됩니다이 연습에서 기능을 응용 프로그램에 새 앨범을 추가 하는 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-327">Now that the **StoreManagerController** supports the **Edit** ability, in this exercise you will learn how to add a Create View template to let store managers add new Albums to the application.</span></span>

<span data-ttu-id="66c61-328">내에서 두 개의 별도 메서드를 사용 하 여 만들기 시나리오를 구현 하는 편집 기능을 사용 하 여 했던 것 처럼 합니다 **StoreManagerController** 클래스:</span><span class="sxs-lookup"><span data-stu-id="66c61-328">Like you did with the Edit functionality, you will implement the Create scenario using two separate methods within the **StoreManagerController** class:</span></span>

1. <span data-ttu-id="66c61-329">저장소 관리자를 처음 방문할 때 메서드에서 빈 폼 표시 됩니다는 **StoreManager/만들기** URL입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-329">One action method will display an empty form when store managers first visit the **/StoreManager/Create** URL.</span></span>
2. <span data-ttu-id="66c61-330">두 번째 작업 메서드는 시나리오를 처리할 저장소 관리자를 클릭할 수 있는 합니다 **저장** 양식 내에서 단추 및 값을 다시 제출 합니다 **StoreManager/만들기** 는 HTTP POST URL.</span><span class="sxs-lookup"><span data-stu-id="66c61-330">A second action method will handle the scenario where the store manager clicks the **Save** button within the form and submits the values back to the **/StoreManager/Create** URL as an HTTP-POST.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Create_action_method"></a>
#### <a name="task-1---implementing-the-http-get-create-action-method"></a><span data-ttu-id="66c61-331">작업 1-HTTP-GET Create 작업 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-331">Task 1 - Implementing the HTTP-GET Create action method</span></span>

<span data-ttu-id="66c61-332">이 태스크에서는 모든 장르 및 아티스트가 목록을 검색 하려면이 데이터에 패키지 만들기 동작 메서드의 GET HTTP 버전을 구현 합니다는 **StoreManagerViewModel** 개체를 뷰 템플릿으로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-332">In this task, you will implement the HTTP-GET version of the Create action method to retrieve a list of all Genres and Artists, package this data up into a **StoreManagerViewModel** object, which will then be passed to a View template.</span></span>

1. <span data-ttu-id="66c61-333">엽니다는 **시작할** 솔루션에 있는 **소스/Ex4-AddingACreateView/시작/** 폴더.</span><span class="sxs-lookup"><span data-stu-id="66c61-333">Open the **Begin** solution located at **Source/Ex4-AddingACreateView/Begin/** folder.</span></span> <span data-ttu-id="66c61-334">그렇지 않은 경우 계속 사용할 수도 있습니다는 **최종** 이전 연습을 완료 하 여 가져온 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-334">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="66c61-335">제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-335">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="66c61-336">이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-336">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="66c61-337">에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="66c61-337">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="66c61-338">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-338">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="66c61-339">NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-339">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="66c61-340">NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-340">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="66c61-341">이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-341">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="66c61-342">오픈 **StoreManagerController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-342">Open **StoreManagerController** class.</span></span> <span data-ttu-id="66c61-343">이 작업을 수행 하려면 확장 합니다 **컨트롤러** 폴더를 두 번 클릭 **StoreManagerController.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-343">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="66c61-344">대체는 **만들기** 작업 메서드 코드를 다음:</span><span class="sxs-lookup"><span data-stu-id="66c61-344">Replace the **Create** action method code with the following:</span></span>

    <span data-ttu-id="66c61-345">(코드 조각- *ASP.NET MVC 4 도우미와 폼 및 유효성 검사-Ex4 StoreManagerController HTTP-GET 만들기 작업*)</span><span class="sxs-lookup"><span data-stu-id="66c61-345">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex4 StoreManagerController HTTP-GET Create action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample12.cs)]

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_the_Create_View"></a>
#### <a name="task-2---adding-the-create-view"></a><span data-ttu-id="66c61-346">작업 2-만들기 뷰 추가</span><span class="sxs-lookup"><span data-stu-id="66c61-346">Task 2 - Adding the Create View</span></span>

<span data-ttu-id="66c61-347">이 태스크에서는 새 (비어 있음) 앨범 양식을 표시 하는 Create View 템플릿을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-347">In this task, you will add the Create View template that will display a new (empty) Album form.</span></span>

1. <span data-ttu-id="66c61-348">마우스 오른쪽 단추로 클릭 합니다 **만들기** 선택한 동작 메서드가 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-348">Right-click inside the **Create** action method and select **Add View**.</span></span> <span data-ttu-id="66c61-349">뷰 추가 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-349">This will bring up the Add View dialog.</span></span>
2. <span data-ttu-id="66c61-350">뷰 추가 대화 상자에서 보기 이름 인지를 확인 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-350">In the Add View dialog, verify that the View Name is **Create**.</span></span> <span data-ttu-id="66c61-351">선택 된 **강력한 형식의 뷰를 만들** 옵션을 선택 **앨범 (MvcMusicStore.Models)** 에서 **모델 클래스** 드롭다운 목록 및 **만들기** 에서 합니다 **스 캐 폴드 템플릿** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-351">Select the **Create a strongly-typed view** option and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down and **Create** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="66c61-352">기본값을 사용 하 여 다른 필드를 그대로 두고을 누릅니다 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-352">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="66c61-353">![만들기 뷰 추가](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "추가-a-만들기-view.png")</span><span class="sxs-lookup"><span data-stu-id="66c61-353">![Adding a create view](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "adding-a-create-view.png")</span></span>

    <span data-ttu-id="66c61-354">*만들기 뷰 추가*</span><span class="sxs-lookup"><span data-stu-id="66c61-354">*Adding the Create View*</span></span>
3. <span data-ttu-id="66c61-355">업데이트를 **GenreId** 하 고 **ArtistId** 드롭 다운 목록을 사용 하 여 아래와 같이 필드:</span><span class="sxs-lookup"><span data-stu-id="66c61-355">Update the **GenreId** and **ArtistId** fields to use a drop-down list as shown below:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample13.cshtml)]

<a id="Ex4Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="66c61-356">작업 3-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="66c61-356">Task 3 - Running the Application</span></span>

<span data-ttu-id="66c61-357">이 작업을 테스트 하는 **StoreManager** **만들기** 빈 앨범 폼 보기 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-357">In this task, you will test that the **StoreManager** **Create** View page displays an empty Album form.</span></span>

1. <span data-ttu-id="66c61-358">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-358">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="66c61-359">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-359">The project starts in the Home page.</span></span> <span data-ttu-id="66c61-360">URL을 변경 **/StoreManager/만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-360">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="66c61-361">새 앨범 속성을 채우기 위한 빈 폼이 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-361">Verify that an empty form is displayed for filling the new Album properties.</span></span>

    <span data-ttu-id="66c61-362">![빈 폼을 사용 하 여 뷰를 만듭니다](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "빈 폼을 사용 하 여 Create View")</span><span class="sxs-lookup"><span data-stu-id="66c61-362">![Create View with an empty form](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "Create View with an empty form")</span></span>

    <span data-ttu-id="66c61-363">*빈 폼을 사용 하 여 뷰 만들기*</span><span class="sxs-lookup"><span data-stu-id="66c61-363">*Create View with an empty form*</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_-_Implementing_the_HTTP-POST_Create_Action_Method"></a>
#### <a name="task-4---implementing-the-http-post-create-action-method"></a><span data-ttu-id="66c61-364">작업 4-HTTP POST를 구현 작업 메서드 만들기</span><span class="sxs-lookup"><span data-stu-id="66c61-364">Task 4 - Implementing the HTTP-POST Create Action Method</span></span>

<span data-ttu-id="66c61-365">이 태스크에서는 만들기 작업 메서드를 클릭할 때 호출 되는 HTTP POST 버전을 구현 합니다 **저장할** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-365">In this task, you will implement the HTTP-POST version of the Create action method that will be invoked when a user clicks the **Save** button.</span></span> <span data-ttu-id="66c61-366">메서드는 데이터베이스에 새 앨범을 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-366">The method should save the new album in the database.</span></span>

1. <span data-ttu-id="66c61-367">Visual Studio 창으로 돌아가려면 필요한 경우 브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-367">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="66c61-368">오픈 **StoreManagerController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-368">Open **StoreManagerController** class.</span></span> <span data-ttu-id="66c61-369">이 작업을 수행 하려면 확장 합니다 **컨트롤러** 폴더를 두 번 클릭 **StoreManagerController.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-369">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
2. <span data-ttu-id="66c61-370">바꿉니다 **HTTP-POST 만들기** 작업 메서드 코드를 다음:</span><span class="sxs-lookup"><span data-stu-id="66c61-370">Replace **HTTP-POST Create** action method code with the following:</span></span>

    <span data-ttu-id="66c61-371">(코드 조각- *ASP.NET MVC 4 도우미와 폼 및 유효성 검사-Ex4 StoreManagerController HTTP POST 만들기 작업*)</span><span class="sxs-lookup"><span data-stu-id="66c61-371">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex4 StoreManagerController HTTP- POST Create action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample14.cs)]

    > [!NOTE]
    > <span data-ttu-id="66c61-372">만들기 작업은 이전 편집 작업 메서드와 매우 유사 하지만 수정 된 개체를 설정 하는 대신 추가 되는 컨텍스트를 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-372">The Create action is pretty similar to the previous Edit action method but instead of setting the object as modified, it is being added to the context.</span></span>

<a id="Ex4Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="66c61-373">작업 5-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="66c61-373">Task 5 - Running the Application</span></span>

<span data-ttu-id="66c61-374">이 작업을 테스트 하는 **StoreManager 만들기** 뷰 페이지 앨범을 만들 수 있습니다 및 StoreManager 인덱스 뷰로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-374">In this task, you will test that the **StoreManager Create** View page lets you create a new Album and then redirects to the StoreManager Index View.</span></span>

1. <span data-ttu-id="66c61-375">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-375">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="66c61-376">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-376">The project starts in the Home page.</span></span> <span data-ttu-id="66c61-377">URL을 변경 **/StoreManager/만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-377">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="66c61-378">다음 그림에서와 같은 새 앨범이에 대 한 데이터를 사용 하 여 모든 양식 필드를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-378">Fill all the form fields with data for a new Album, like the one in the following figure:</span></span>

    <span data-ttu-id="66c61-379">![앨범을 만드는](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "앨범 만들기")</span><span class="sxs-lookup"><span data-stu-id="66c61-379">![Creating an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "Creating an Album")</span></span>

    <span data-ttu-id="66c61-380">*앨범 만들기*</span><span class="sxs-lookup"><span data-stu-id="66c61-380">*Creating an Album*</span></span>
3. <span data-ttu-id="66c61-381">방금 만든 새 앨범이 포함 하는 StoreManager 인덱스 보기로 리디렉션됩니다 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-381">Verify that you get redirected to the StoreManager Index View that includes the new Album just created.</span></span>

    <span data-ttu-id="66c61-382">![만든 새 앨범이](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "만든 새 앨범")</span><span class="sxs-lookup"><span data-stu-id="66c61-382">![New Album Created](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "New Album Created")</span></span>

    <span data-ttu-id="66c61-383">*만든 새 앨범*</span><span class="sxs-lookup"><span data-stu-id="66c61-383">*New Album Created*</span></span>

<a id="Exercise5"></a>

<a id="Exercise_5_Handling_Deletion"></a>
### <a name="exercise-5-handling-deletion"></a><span data-ttu-id="66c61-384">실습 5: 삭제 처리</span><span class="sxs-lookup"><span data-stu-id="66c61-384">Exercise 5: Handling Deletion</span></span>

<span data-ttu-id="66c61-385">앨범을 삭제 하는 기능을 아직 구현 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-385">The ability to delete albums is not yet implemented.</span></span> <span data-ttu-id="66c61-386">이이 연습에 대 한 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-386">This is what this exercise will be about.</span></span> <span data-ttu-id="66c61-387">내에서 두 개의 별도 메서드를 사용 하 여 삭제 시나리오 구현 이전 처럼 합니다 **StoreManagerController** 클래스:</span><span class="sxs-lookup"><span data-stu-id="66c61-387">Like before, you will implement the Delete scenario using two separate methods within the **StoreManagerController** class:</span></span>

1. <span data-ttu-id="66c61-388">메서드에서 확인 폼에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-388">One action method will display a confirmation form</span></span>
2. <span data-ttu-id="66c61-389">두 번째 작업 메서드를 폼 제출을 처리할 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-389">A second action method will handle the form submission</span></span>

<a id="Ex5Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Delete_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-delete-action-method"></a><span data-ttu-id="66c61-390">작업 1-HTTP-GET Delete 동작 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-390">Task 1 - Implementing the HTTP-GET Delete Action Method</span></span>

<span data-ttu-id="66c61-391">이 작업에서는 HTTP GET 버전의 앨범의 정보를 검색할 Delete 동작 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-391">In this task, you will implement the HTTP-GET version of the Delete action method to retrieve the album's information.</span></span>

1. <span data-ttu-id="66c61-392">엽니다는 **시작할** 솔루션에 있는 **소스/Ex5-HandlingDeletion/시작/** 폴더.</span><span class="sxs-lookup"><span data-stu-id="66c61-392">Open the **Begin** solution located at **Source/Ex5-HandlingDeletion/Begin/** folder.</span></span> <span data-ttu-id="66c61-393">그렇지 않은 경우 계속 사용할 수도 있습니다는 **최종** 이전 연습을 완료 하 여 가져온 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-393">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="66c61-394">제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-394">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="66c61-395">이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-395">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="66c61-396">에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="66c61-396">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="66c61-397">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-397">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="66c61-398">NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-398">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="66c61-399">NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-399">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="66c61-400">이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-400">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="66c61-401">오픈 **StoreManagerController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-401">Open **StoreManagerController** class.</span></span> <span data-ttu-id="66c61-402">이 작업을 수행 하려면 확장 합니다 **컨트롤러** 폴더를 두 번 클릭 **StoreManagerController.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-402">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="66c61-403">Delete 컨트롤러 작업이 정확 하 게 이전 저장소 세부 정보 컨트롤러 작업으로 동일한: 쿼리를 **앨범** 사용 하 여 데이터베이스에서 개체를 **id** 반환 URL에 제공 된는 적절 한 **보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-403">The Delete controller action is exactly the same as the previous Store Details controller action: it queries the **album** object from the database using the **id** provided in the URL and returns the appropriate **View**.</span></span> <span data-ttu-id="66c61-404">이 위해 대체 HTTP GET **삭제** 작업 메서드 코드를 다음:</span><span class="sxs-lookup"><span data-stu-id="66c61-404">To do this, replace the HTTP-GET **Delete** action method code with the following:</span></span>

    <span data-ttu-id="66c61-405">(코드 조각- *ASP.NET MVC 4 도우미와 폼 및 유효성 검사-Ex5 처리 삭제 HTTP-GET 삭제 작업*)</span><span class="sxs-lookup"><span data-stu-id="66c61-405">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex5 Handling Deletion HTTP-GET Delete action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample15.cs)]
4. <span data-ttu-id="66c61-406">마우스 오른쪽 단추로 클릭 합니다 **삭제** 선택한 동작 메서드가 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-406">Right-click inside the **Delete** action method and select **Add View**.</span></span> <span data-ttu-id="66c61-407">뷰 추가 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-407">This will bring up the Add View dialog.</span></span>
5. <span data-ttu-id="66c61-408">뷰 추가 대화 상자에서 보기 이름 인지를 확인 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-408">In the Add View dialog, verify that the View name is **Delete**.</span></span> <span data-ttu-id="66c61-409">선택 합니다 **강력한 형식의 뷰를 만들** 옵션을 선택 **앨범 (MvcMusicStore.Models)** 에서 **모델 클래스** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-409">Select the **Create a strongly-typed view** option and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down.</span></span> <span data-ttu-id="66c61-410">선택 **삭제할** 에서 **스 캐 폴드 템플릿** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-410">Select **Delete** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="66c61-411">기본값을 사용 하 여 다른 필드를 그대로 두고을 누릅니다 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-411">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="66c61-412">![삭제 뷰 추가](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "삭제 뷰 추가")</span><span class="sxs-lookup"><span data-stu-id="66c61-412">![Adding a Delete View](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "Adding a Delete View")</span></span>

    <span data-ttu-id="66c61-413">*삭제 뷰 추가*</span><span class="sxs-lookup"><span data-stu-id="66c61-413">*Adding a Delete View*</span></span>
6. <span data-ttu-id="66c61-414">Delete 템플릿 모델의 모든 필드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-414">The Delete template shows all the fields from the model.</span></span> <span data-ttu-id="66c61-415">앨범의 제목만을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-415">You will show only the album's title.</span></span> <span data-ttu-id="66c61-416">이렇게 하려면 보기의 콘텐츠를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-416">To do this, replace the content of the view with the following code:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample16.cshtml)]

<a id="Ex05Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="66c61-417">작업 2-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="66c61-417">Task 2 - Running the Application</span></span>

<span data-ttu-id="66c61-418">이 작업을 테스트 하는 **StoreManager** **삭제** 뷰 페이지 확인 삭제 양식 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-418">In this task, you will test that the **StoreManager** **Delete** View page displays a confirmation deletion form.</span></span>

1. <span data-ttu-id="66c61-419">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-419">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="66c61-420">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-420">The project starts in the Home page.</span></span> <span data-ttu-id="66c61-421">URL을 변경 **/StoreManager**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-421">Change the URL to **/StoreManager**.</span></span> <span data-ttu-id="66c61-422">선택 클릭 하 여 삭제할 하나 앨범 **삭제** 새 보기는 업로드 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-422">Select one album to delete by clicking **Delete** and verify that the new view is uploaded.</span></span>

    <span data-ttu-id="66c61-423">![삭제 해도 앨범](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "삭제 해도 앨범")</span><span class="sxs-lookup"><span data-stu-id="66c61-423">![Deleting an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "Deleting an Album")</span></span>

    <span data-ttu-id="66c61-424">*삭제 해도 앨범*</span><span class="sxs-lookup"><span data-stu-id="66c61-424">*Deleting an Album*</span></span>

<a id="Ex05Task3"></a>

<a id="Task_3-_Implementing_the_HTTP-POST_Delete_Action_Method"></a>
#### <a name="task-3--implementing-the-http-post-delete-action-method"></a><span data-ttu-id="66c61-425">작업 3-HTTP-POST Delete 동작 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-425">Task 3- Implementing the HTTP-POST Delete Action Method</span></span>

<span data-ttu-id="66c61-426">이 작업을 클릭할 때 호출 되는 Delete 동작 메서드의 POST HTTP 버전을 구현 합니다 **삭제** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-426">In this task, you will implement the HTTP-POST version of the Delete action method that will be invoked when a user clicks the **Delete** button.</span></span> <span data-ttu-id="66c61-427">메서드는 데이터베이스에 album을 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-427">The method should delete the album in the database.</span></span>

1. <span data-ttu-id="66c61-428">Visual Studio 창으로 돌아가려면 필요한 경우 브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-428">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="66c61-429">오픈 **StoreManagerController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-429">Open **StoreManagerController** class.</span></span> <span data-ttu-id="66c61-430">이 작업을 수행 하려면 확장 합니다 **컨트롤러** 폴더를 두 번 클릭 **StoreManagerController.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-430">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
2. <span data-ttu-id="66c61-431">바꿉니다 **HTTP POST, Delete** 작업 메서드 코드를 다음:</span><span class="sxs-lookup"><span data-stu-id="66c61-431">Replace **HTTP-POST Delete** action method code with the following:</span></span>

    <span data-ttu-id="66c61-432">(코드 조각- *ASP.NET MVC 4 도우미와 폼 및 유효성 검사-Ex5 처리 삭제 HTTP-POST 삭제 작업*)</span><span class="sxs-lookup"><span data-stu-id="66c61-432">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex5 Handling Deletion HTTP-POST Delete action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample17.cs)]

<a id="Ex5Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="66c61-433">작업 4-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="66c61-433">Task 4 - Running the Application</span></span>

<span data-ttu-id="66c61-434">이 작업을 테스트 하는 **StoreManager 삭제** 뷰 페이지 앨범을 삭제할 수 있습니다 및 StoreManager 인덱스 뷰로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-434">In this task, you will test that the **StoreManager Delete** View page lets you delete an Album and then redirects to the StoreManager Index View.</span></span>

1. <span data-ttu-id="66c61-435">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-435">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="66c61-436">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-436">The project starts in the Home page.</span></span> <span data-ttu-id="66c61-437">URL을 변경 **/StoreManager**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-437">Change the URL to **/StoreManager**.</span></span> <span data-ttu-id="66c61-438">클릭 하 여 삭제할 하나 앨범 선택 **삭제 합니다.**</span><span class="sxs-lookup"><span data-stu-id="66c61-438">Select one album to delete by clicking **Delete.**</span></span> <span data-ttu-id="66c61-439">클릭 하 여 삭제를 확인 **삭제** 단추:</span><span class="sxs-lookup"><span data-stu-id="66c61-439">Confirm the deletion by clicking **Delete** button:</span></span>

    <span data-ttu-id="66c61-440">![삭제 해도 앨범](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "삭제 해도 앨범")</span><span class="sxs-lookup"><span data-stu-id="66c61-440">![Deleting an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "Deleting an Album")</span></span>

    <span data-ttu-id="66c61-441">*삭제 해도 앨범*</span><span class="sxs-lookup"><span data-stu-id="66c61-441">*Deleting an Album*</span></span>
3. <span data-ttu-id="66c61-442">앨범에 나타나지 않으면 이후 삭제 되었는지 확인 합니다 **인덱스** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-442">Verify that the album was deleted since it does not appear in the **Index** page.</span></span>

<a id="Exercise6"></a>

<a id="Exercise_6_Adding_Validation"></a>
### <a name="exercise-6-adding-validation"></a><span data-ttu-id="66c61-443">실습 6: 유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="66c61-443">Exercise 6: Adding Validation</span></span>

<span data-ttu-id="66c61-444">현재, 만들기 및 편집 양식이 있는 모든 종류의 유효성 검사를 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-444">Currently, the Create and Edit forms you have in place do not perform any kind of validation.</span></span> <span data-ttu-id="66c61-445">가격 필드에 필수 필드를 빈 또는 형식 문자를 유지 하는 사용자, 데이터베이스에서 첫 번째 오류를 받게 됩니다 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-445">If the user leaves a required field blank or type letters in the price field, the first error you will get will be from the database.</span></span>

<span data-ttu-id="66c61-446">데이터 주석 모델 클래스를 추가 하 여 응용 프로그램에 유효성 검사를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-446">You can add validation to the application by adding Data Annotations to your model class.</span></span> <span data-ttu-id="66c61-447">데이터 주석 모델 속성을 적용 하려는 규칙을 설명 하는 허용 하 고 ASP.NET MVC에서 자동으로 처리를 적용 하 고 사용자에 게 적절 한 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-447">Data Annotations allow describing the rules you want applied to your model properties, and ASP.NET MVC will take care of enforcing and displaying appropriate message to users.</span></span>

<a id="Ex06Task1"></a>

<a id="Task_1_-_Adding_Data_Annotations"></a>
#### <a name="task-1---adding-data-annotations"></a><span data-ttu-id="66c61-448">작업 1-데이터 주석 추가</span><span class="sxs-lookup"><span data-stu-id="66c61-448">Task 1 - Adding Data Annotations</span></span>

<span data-ttu-id="66c61-449">이 태스크에서는 해당 하는 경우 유효성 검사 메시지를 표시 하는 데이터 주석 만들기 및 편집 페이지에 있도록 앨범 모델에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-449">In this task, you will add Data Annotations to the Album Model that will make the Create and Edit page display validation messages when appropriate.</span></span>

<span data-ttu-id="66c61-450">단순 모델 클래스를 데이터 주석 추가 방금 처리를 추가 하 여는 **를 사용 하 여** 문을 **System.ComponentModel.DataAnnotation**에 다음 배치를 **[필수]** 적절 한 속성에는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-450">For a simple Model class, adding a Data Annotation is just handled by adding a **using** statement for **System.ComponentModel.DataAnnotation**, then placing a **[Required]** attribute on the appropriate properties.</span></span> <span data-ttu-id="66c61-451">다음 예제에서는 없게 합니다 **이름을** 속성 보기에서 필수 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-451">The following example would make the **Name** property a required field in the View.</span></span>

[!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample18.cs)]

<span data-ttu-id="66c61-452">이 엔터티 데이터 모델 생성은 여기서이 응용 프로그램의 경우에서 좀 더 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-452">This is a little more complex in cases like this application where the Entity Data Model is generated.</span></span> <span data-ttu-id="66c61-453">데이터 주석 모델 클래스에 직접 추가한 데이터베이스에서 모델을 업데이트 하는 경우 덮어쓰게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-453">If you added Data Annotations directly to the model classes, they would be overwritten if you update the model from the database.</span></span> <span data-ttu-id="66c61-454">가능 대신 사용 하 여 메타 데이터는 주석을 저장할 존재 하며 모델을 사용 하 여 연결 된 partial 클래스의 클래스를 사용 하 여 합니다 **[MetadataType]** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-454">Instead, you can make use of metadata partial classes which will exist to hold the annotations and are associated with the model classes using the **[MetadataType]** attribute.</span></span>

1. <span data-ttu-id="66c61-455">엽니다는 **시작할** 솔루션에 있는 **소스/Ex6-AddingValidation/시작/** 폴더.</span><span class="sxs-lookup"><span data-stu-id="66c61-455">Open the **Begin** solution located at **Source/Ex6-AddingValidation/Begin/** folder.</span></span> <span data-ttu-id="66c61-456">그렇지 않은 경우 계속 사용할 수도 있습니다는 **최종** 이전 연습을 완료 하 여 가져온 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-456">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="66c61-457">제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-457">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="66c61-458">이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-458">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="66c61-459">에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="66c61-459">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="66c61-460">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-460">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="66c61-461">NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-461">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="66c61-462">NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-462">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="66c61-463">이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-463">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="66c61-464">엽니다는 **Album.cs** 에서 합니다 **모델** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-464">Open the **Album.cs** from the **Models** folder.</span></span>
3. <span data-ttu-id="66c61-465">바꿉니다 **Album.cs** 다음과 같이 표시 되도록 강조 표시 된 코드를 사용 하 여 콘텐츠:</span><span class="sxs-lookup"><span data-stu-id="66c61-465">Replace **Album.cs** content with the highlighted code, so that it looks like the following:</span></span>

    > [!NOTE]
    > <span data-ttu-id="66c61-466">줄 **[DisplayFormat(ConvertEmptyStringToNull=false)]** 빈 문자열 모델에서 데이터 원본에서 데이터 필드가 업데이트 되 면 null로 변환 되지 않습니다 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-466">The line **[DisplayFormat(ConvertEmptyStringToNull=false)]** indicates that empty strings from the model won't be converted to null when the data field is updated in the data source.</span></span> <span data-ttu-id="66c61-467">Entity Framework 데이터 주석 필드의 유효성을 검사 하기 전에 모델에 null 값을 할당 하는 경우이 설정은 예외가 발생 하지 않게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-467">This setting will avoid an exception when the Entity Framework assigns null values to the model before Data Annotation validates the fields.</span></span>

    <span data-ttu-id="66c61-468">(코드 조각- *ASP.NET MVC 4 도우미와 폼 및 유효성 검사-Ex6 앨범 메타 데이터에 대 한 partial 클래스*)</span><span class="sxs-lookup"><span data-stu-id="66c61-468">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex6 Album metadata partial class*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample19.cs)]

    > [!NOTE]
    > <span data-ttu-id="66c61-469">이 **앨범** partial 클래스에는 **MetadataType** 가리키는 특성을 **AlbumMetaData** 데이터 주석을 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-469">This **Album** partial class has a **MetadataType** attribute which points to the **AlbumMetaData** class for the Data Annotations.</span></span> <span data-ttu-id="66c61-470">다음은 앨범 모델 주석을 추가 하는 데 사용할 데이터 주석 특성의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-470">These are some of the Data Annotation attributes you are using to annotate the Album model:</span></span>
    > 
    > - <span data-ttu-id="66c61-471">필수-속성이 필수 필드 임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-471">Required - Indicates that the property is a required field</span></span>
    > - <span data-ttu-id="66c61-472">DisplayName-양식 필드 유효성 검사 메시지에 사용할 텍스트를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-472">DisplayName - Defines the text to be used on form fields and validation messages</span></span>
    > - <span data-ttu-id="66c61-473">DisplayFormat-데이터 필드 표시 되 고 형식이 지정 되는 방식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-473">DisplayFormat - Specifies how data fields are displayed and formatted.</span></span>
    > - <span data-ttu-id="66c61-474">StringLength-문자열 필드에 대 한 최대 길이 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-474">StringLength - Defines a maximum length for a string field</span></span>
    > - <span data-ttu-id="66c61-475">범위는-숫자 필드에 대 한 최대 및 최소 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-475">Range - Gives a maximum and minimum value for a numeric field</span></span>
    > - <span data-ttu-id="66c61-476">ScaffoldColumn-편집기 폼에서 필드를 숨길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-476">ScaffoldColumn - Allows hiding fields from editor forms</span></span>

<a id="Ex06Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="66c61-477">작업 2-응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="66c61-477">Task 2 - Running the Application</span></span>

<span data-ttu-id="66c61-478">이 태스크에서는 테스트 만들기 및 편집 페이지에서 필드의 유효성을 검사는 마지막 작업에서 선택한 표시 이름을 사용 하 여.</span><span class="sxs-lookup"><span data-stu-id="66c61-478">In this task, you will test that the Create and Edit pages validate fields, using the display names chosen in the last task.</span></span>

1. <span data-ttu-id="66c61-479">키를 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-479">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="66c61-480">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-480">The project starts in the Home page.</span></span> <span data-ttu-id="66c61-481">URL을 변경 **/StoreManager/만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-481">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="66c61-482">표시 이름을 partial 클래스에서 일치 하는지 확인 (같은 **앨범 아트 URL** of **AlbumArtUrl**)</span><span class="sxs-lookup"><span data-stu-id="66c61-482">Verify that the display names match the ones in the partial class (like **Album Art URL** instead of **AlbumArtUrl**)</span></span>
3. <span data-ttu-id="66c61-483">클릭 **만들기**, 폼을 채우지 않고 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-483">Click **Create**, without filling the form.</span></span> <span data-ttu-id="66c61-484">해당 유효성 검사 메시지 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-484">Verify that you get the corresponding validation messages.</span></span>

    <span data-ttu-id="66c61-485">![만들기 페이지에 있는 필드의 유효성을 검사](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "만들기 페이지에서 필드 유효성 검사")</span><span class="sxs-lookup"><span data-stu-id="66c61-485">![Validated fields in the Create page](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "Validated fields in the Create page")</span></span>

    <span data-ttu-id="66c61-486">*만들기 페이지의 유효성이 검사 된 필드*</span><span class="sxs-lookup"><span data-stu-id="66c61-486">*Validated fields in the Create page*</span></span>
4. <span data-ttu-id="66c61-487">사용 하 여 동일한 발생 하는지 확인할 수 있습니다 합니다 **편집** 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-487">You can verify that the same occurs with the **Edit** page.</span></span> <span data-ttu-id="66c61-488">URL을 변경 **/StoreManager/Edit/1** 표시 이름을 partial 클래스에서 일치 하는지 확인 하 고 (같은 **앨범 아트 URL** 대신 **AlbumArtUrl**).</span><span class="sxs-lookup"><span data-stu-id="66c61-488">Change the URL to **/StoreManager/Edit/1** and verify that the display names match the ones in the partial class (like **Album Art URL** instead of **AlbumArtUrl**).</span></span> <span data-ttu-id="66c61-489">빈 합니다 **제목** 하 고 **가격** 필드 및 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-489">Empty the **Title** and **Price** fields and click **Save**.</span></span> <span data-ttu-id="66c61-490">해당 유효성 검사 메시지 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-490">Verify that you get the corresponding validation messages.</span></span>

    ![편집 페이지의 유효성이 검사 된 필드](aspnet-mvc-4-helpers-forms-and-validation/_static/image19.png)

    <span data-ttu-id="66c61-492">*편집 페이지의 유효성이 검사 된 필드*</span><span class="sxs-lookup"><span data-stu-id="66c61-492">*Validated fields in the Edit page*</span></span>

<a id="Exercise7"></a>

<a id="Exercise_7_Using_Unobtrusive_jQuery_at_Client_Side"></a>
### <a name="exercise-7-using-unobtrusive-jquery-at-client-side"></a><span data-ttu-id="66c61-493">실습 7: 비 가시적인 jQuery 클라이언트 쪽에서 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="66c61-493">Exercise 7: Using Unobtrusive jQuery at Client Side</span></span>

<span data-ttu-id="66c61-494">이 연습에서는 클라이언트 쪽에서 MVC 4 비 가시적인 jQuery 유효성 검사를 사용 하도록 설정 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-494">In this exercise, you will learn how to enable MVC 4 Unobtrusive jQuery validation at client side.</span></span>

> [!NOTE]
> <span data-ttu-id="66c61-495">비 가시적인 jQuery ajax 데이터 접두사 JavaScript를 사용 하 여 영향을 주지 않고 내보내는 인라인 클라이언트 스크립트 대신 서버에서 작업 메서드를 호출.</span><span class="sxs-lookup"><span data-stu-id="66c61-495">The Unobtrusive jQuery uses data-ajax prefix JavaScript to invoke action methods on the server rather than intrusively emitting inline client scripts.</span></span>


<a id="Ex7Task1"></a>

<a id="Task_1_-_Running_the_Application_before_Enabling_Unobtrusive_jQuery"></a>
#### <a name="task-1---running-the-application-before-enabling-unobtrusive-jquery"></a><span data-ttu-id="66c61-496">작업 1-jQuery 비간섭 사용 하도록 설정 하기 전에 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="66c61-496">Task 1 - Running the Application before Enabling Unobtrusive jQuery</span></span>

<span data-ttu-id="66c61-497">이 태스크에서는 모두 유효성 검사 모델을 비교 하기 위해 jQuery를 포함 하기 전에 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-497">In this task, you will run the application before including jQuery in order to compare both validation models.</span></span>

1. <span data-ttu-id="66c61-498">엽니다는 **시작할** 솔루션에 있는 **소스/Ex7-UnobtrusivejQueryValidation/시작/** 폴더.</span><span class="sxs-lookup"><span data-stu-id="66c61-498">Open the **Begin** solution located at **Source/Ex7-UnobtrusivejQueryValidation/Begin/** folder.</span></span> <span data-ttu-id="66c61-499">그렇지 않은 경우 계속 사용할 수도 있습니다는 **최종** 이전 연습을 완료 하 여 가져온 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-499">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="66c61-500">제공 된를 열면 **시작** 일부 누락 된 NuGet 패키지를 다운로드 해야 솔루션을 계속 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-500">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="66c61-501">이 작업을 수행 하려면 클릭 합니다 **프로젝트** 선택한 메뉴 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-501">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="66c61-502">에 **NuGet 패키지 관리** 대화 상자에서 클릭 **복원** 누락 된 패키지를 다운로드 하려면.</span><span class="sxs-lookup"><span data-stu-id="66c61-502">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="66c61-503">마지막으로,를 클릭 하 여 솔루션을 빌드합니다 **빌드합니다** | **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-503">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="66c61-504">NuGet을 사용 하는 이점은 중 하나는 필요가 프로젝트에서 모든 라이브러리를 제공 합니다. 프로젝트 크기를 줄이면입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-504">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="66c61-505">NuGet 파워 도구를 사용 하 여 Packages.config 파일에서 패키지 버전을 지정 하 여 있습니다 됩니다 처음 프로젝트를 실행 하면 필요한 라이브러리를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-505">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="66c61-506">이 때문에이 랩의 기존 솔루션을 연 후 다음이 단계를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-506">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="66c61-507">**F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-507">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="66c61-508">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-508">The project starts in the Home page.</span></span> <span data-ttu-id="66c61-509">찾아보기 **StoreManager/만들기** 누릅니다 **만들기** 폼 유효성 검사 메시지가 확인을 채우지 않고:</span><span class="sxs-lookup"><span data-stu-id="66c61-509">Browse **/StoreManager/Create** and click **Create** without filling the form to verify that you get validation messages:</span></span>

    <span data-ttu-id="66c61-510">![사용 하지 않도록 설정 하는 클라이언트 유효성 검사](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "사용 하지 않도록 설정 하는 클라이언트 유효성 검사")</span><span class="sxs-lookup"><span data-stu-id="66c61-510">![Client validation disabled](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "Client validation disabled")</span></span>

    <span data-ttu-id="66c61-511">*사용 하지 않도록 설정 하는 클라이언트 유효성 검사*</span><span class="sxs-lookup"><span data-stu-id="66c61-511">*Client validation disabled*</span></span>
4. <span data-ttu-id="66c61-512">브라우저에서 HTML 소스 코드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-512">In the browser, open the HTML source code:</span></span>

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample20.html)]

<a id="Ex7Task2"></a>

<a id="Task_2_-_Enabling_Unobtrusive_Client_Validation"></a>
#### <a name="task-2---enabling-unobtrusive-client-validation"></a><span data-ttu-id="66c61-513">작업 2-비 가시적인 클라이언트 유효성 검사를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="66c61-513">Task 2 - Enabling Unobtrusive Client Validation</span></span>

<span data-ttu-id="66c61-514">이 태스크에서는 jQuery는 설정한 **비간섭 클라이언트 유효성 검사** 에서 **Web.config** 파일이 기본적으로 모든 새 ASP.NET MVC 4 프로젝트에서 false로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-514">In this task, you will enable jQuery **unobtrusive client validation** from **Web.config** file, which is by default set to false in all new ASP.NET MVC 4 projects.</span></span> <span data-ttu-id="66c61-515">또한 필요한 스크립트 jQuery 비간섭 클라이언트 유효성 검사 작업 확인에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-515">Additionally, you will add the necessary scripts references to make jQuery Unobtrusive Client Validation work.</span></span>

1. <span data-ttu-id="66c61-516">열기 **Web.Config** 프로젝트 루트에 파일을 확인 합니다 **ClientValidationEnabled** 하 고 **UnobtrusiveJavaScriptEnabled** 키 값 로설정됩니다**true**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-516">Open **Web.Config** file at project root, and make sure that the **ClientValidationEnabled** and **UnobtrusiveJavaScriptEnabled** keys values are set to **true**.</span></span>

    [!code-xml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample21.xml)]

    > [!NOTE]
    > <span data-ttu-id="66c61-517">또한 동일한 결과 얻기 위해 Global.asax.cs에서 코드에 의해 클라이언트 유효성 검사를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-517">You can also enable client validation by code at Global.asax.cs to get the same results:</span></span>
    > 
    > <span data-ttu-id="66c61-518">**HtmlHelper.ClientValidationEnabled = true;**</span><span class="sxs-lookup"><span data-stu-id="66c61-518">**HtmlHelper.ClientValidationEnabled = true;**</span></span>
    > 
    > <span data-ttu-id="66c61-519">또한 사용자 지정 동작을 갖는 모든 컨트롤러에 ClientValidationEnabled 특성을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-519">Additionally, you can assign ClientValidationEnabled attribute into any controller to have a custom behavior.</span></span>
2. <span data-ttu-id="66c61-520">오픈 **Create.cshtml** 언제 **Views\StoreManager**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-520">Open **Create.cshtml** at **Views\StoreManager**.</span></span>
3. <span data-ttu-id="66c61-521">다음 스크립트 파일이 있는지 확인 **jquery.validate** 하 고 **jquery.validate.unobtrusive**, 보기 통해 참조 되는 &quot; **~/bundles/jqueryval** &quot; 번들입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-521">Make sure the following script files, **jquery.validate** and **jquery.validate.unobtrusive**, are referenced in the view throught the &quot;**~/bundles/jqueryval**&quot; bundle.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample22.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="66c61-522">이러한 모든 jQuery 라이브러리는 새 MVC 4 프로젝트에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-522">All these jQuery libraries are included in MVC 4 new projects.</span></span> <span data-ttu-id="66c61-523">더 많은 라이브러리를 찾을 수 있습니다 합니다 **스크립트/** 프로젝트의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-523">You can find more libraries in the **/Scripts** folder of you project.</span></span>
    > 
    > <span data-ttu-id="66c61-524">이 유효성 검사를 확인 하려면 라이브러리가 작동, jQuery 프레임 워크 라이브러리에 대 한 참조를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-524">In order to make this validation libraries work, you need to add a reference to the jQuery framework library.</span></span> <span data-ttu-id="66c61-525">이 참조에 이미 추가 되므로  **\_Layout.cshtml** 파일인 필요가 없습니다이 특정 뷰에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-525">Since this reference is already added in the **\_Layout.cshtml** file, you do not need to add it in this particular view.</span></span>

<a id="Ex7Task3"></a>

<a id="Task_3_-_Running_the_Application_Using_Unobtrusive_jQuery_Validation"></a>
#### <a name="task-3---running-the-application-using-unobtrusive-jquery-validation"></a><span data-ttu-id="66c61-526">작업 3-응용 프로그램 사용 하 여 비 가시적인 jQuery 유효성 검사를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-526">Task 3 - Running the Application Using Unobtrusive jQuery Validation</span></span>

<span data-ttu-id="66c61-527">이 작업을 테스트 하는 합니다 **StoreManager** 템플릿을 사용자가 새 앨범이 때 jQuery 라이브러리를 사용 하 여 클라이언트 쪽 유효성 검사를 수행 하는 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-527">In this task, you will test that the **StoreManager** create view template performs client side validation using jQuery libraries when the user creates a new album.</span></span>

1. <span data-ttu-id="66c61-528">**F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-528">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="66c61-529">프로젝트 홈 페이지에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-529">The project starts in the Home page.</span></span> <span data-ttu-id="66c61-530">찾아보기 **StoreManager/만들기** 누릅니다 **만들기** 폼 유효성 검사 메시지가 확인을 채우지 않고:</span><span class="sxs-lookup"><span data-stu-id="66c61-530">Browse **/StoreManager/Create** and click **Create** without filling the form to verify that you get validation messages:</span></span>

    <span data-ttu-id="66c61-531">![사용 하도록 설정 하는 jQuery 사용 하 여 클라이언트 유효성 검사](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "사용 하도록 설정 하는 jQuery 사용 하 여 클라이언트 유효성 검사")</span><span class="sxs-lookup"><span data-stu-id="66c61-531">![Client validation with jQuery enabled](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "Client validation with jQuery enabled")</span></span>

    <span data-ttu-id="66c61-532">*사용 하도록 설정 하는 jQuery 사용 하 여 클라이언트 유효성 검사*</span><span class="sxs-lookup"><span data-stu-id="66c61-532">*Client validation with jQuery enabled*</span></span>
3. <span data-ttu-id="66c61-533">브라우저에서 뷰 만들기에 대 한 소스 코드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-533">In the browser, open the source code for Create view:</span></span>

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample23.html)]

   > [!NOTE]
   > <span data-ttu-id="66c61-534">각 클라이언트 유효성 검사 규칙에 대해 비 가시적인 jQuery 추가 데이터를 사용 하 여 특성-val-*rulename*=&quot;*메시지*&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-534">For each client validation rule, Unobtrusive jQuery adds an attribute with data-val-*rulename*=&quot;*message*&quot;.</span></span> <span data-ttu-id="66c61-535">태그의 목록을 해당 Unobtrusive 같습니다 jQuery 클라이언트 유효성 검사를 수행 하려면 html 입력된 필드에 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-535">Below is a list of tags that Unobtrusive jQuery inserts into the html input field to perform client validation:</span></span>
   > 
   > - <span data-ttu-id="66c61-536">데이터 값</span><span class="sxs-lookup"><span data-stu-id="66c61-536">Data-val</span></span>
   > - <span data-ttu-id="66c61-537">데이터-val-번호</span><span class="sxs-lookup"><span data-stu-id="66c61-537">Data-val-number</span></span>
   > - <span data-ttu-id="66c61-538">데이터 값 범위</span><span class="sxs-lookup"><span data-stu-id="66c61-538">Data-val-range</span></span>
   > - <span data-ttu-id="66c61-539">데이터 val-범위 min/데이터 val-범위 최대값</span><span class="sxs-lookup"><span data-stu-id="66c61-539">Data-val-range-min / Data-val-range-max</span></span>
   > - <span data-ttu-id="66c61-540">Val-필요한 데이터</span><span class="sxs-lookup"><span data-stu-id="66c61-540">Data-val-required</span></span>
   > - <span data-ttu-id="66c61-541">데이터 값 길이</span><span class="sxs-lookup"><span data-stu-id="66c61-541">Data-val-length</span></span>
   > - <span data-ttu-id="66c61-542">Val 길이 최대 데이터/데이터 val-길이 min</span><span class="sxs-lookup"><span data-stu-id="66c61-542">Data-val-length-max / Data-val-length-min</span></span>
   > 
   > <span data-ttu-id="66c61-543">모델을 사용 하 여 데이터 값이 모두 채워져 **데이터 주석**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-543">All the data values are filled with model **Data Annotation**.</span></span> <span data-ttu-id="66c61-544">그런 다음 클라이언트 쪽에서 서버 쪽에서 작동 하는 모든 논리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-544">Then, all the logic that works at server side can be run at client side.</span></span> <span data-ttu-id="66c61-545">예를 들어, Price 특성을 모델에 다음 데이터 주석:</span><span class="sxs-lookup"><span data-stu-id="66c61-545">For example, Price attribute has the following data annotation in the model:</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample24.cs)]
   > 
   > <span data-ttu-id="66c61-546">비 가시적인 jQuery를 사용한 후 생성 된 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-546">After using Unobtrusive jQuery, the generated code is:</span></span>
   > 
   > [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample25.html)]

* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="66c61-547">요약</span><span class="sxs-lookup"><span data-stu-id="66c61-547">Summary</span></span>

<span data-ttu-id="66c61-548">이 실습을 완료 하 여 사용자가 다음을 사용 하 여 데이터베이스에 저장 된 데이터를 변경할 수 있게 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-548">By completing this Hands-On Lab you have learned how to enable users to change the data stored in the database with the use of the following:</span></span>

- <span data-ttu-id="66c61-549">인덱스 만들기, 편집, 삭제 등의 컨트롤러 작업</span><span class="sxs-lookup"><span data-stu-id="66c61-549">Controller actions like Index, Create, Edit, Delete</span></span>
- <span data-ttu-id="66c61-550">HTML 표에 있는 속성을 표시 하기 위한 ASP.NET MVC 스 캐 폴딩 기능</span><span class="sxs-lookup"><span data-stu-id="66c61-550">ASP.NET MVC's scaffolding feature for displaying properties in an HTML table</span></span>
- <span data-ttu-id="66c61-551">사용자를 개선 하기 위해 사용자 지정 HTML 도우미 환경</span><span class="sxs-lookup"><span data-stu-id="66c61-551">Custom HTML helpers to improve user experience</span></span>
- <span data-ttu-id="66c61-552">HTTP-GET 또는 HTTP-POST 호출에 대응 하는 작업 메서드</span><span class="sxs-lookup"><span data-stu-id="66c61-552">Action methods that react to either HTTP-GET or HTTP-POST calls</span></span>
- <span data-ttu-id="66c61-553">템플릿 만들기 및 편집 같은 유사한 보기에 대 한 공유 편집기 템플릿</span><span class="sxs-lookup"><span data-stu-id="66c61-553">A shared editor template for similar View templates like Create and Edit</span></span>
- <span data-ttu-id="66c61-554">드롭다운 메뉴와 같은 양식 요소</span><span class="sxs-lookup"><span data-stu-id="66c61-554">Form elements like drop-downs</span></span>
- <span data-ttu-id="66c61-555">모델 유효성 검사에 대 한 데이터 주석</span><span class="sxs-lookup"><span data-stu-id="66c61-555">Data annotations for Model validation</span></span>
- <span data-ttu-id="66c61-556">JQuery 비간섭 라이브러리를 사용 하 여 클라이언트 쪽 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="66c61-556">Client Side Validation using jQuery Unobtrusive library</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="66c61-557">부록 a: 설치 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="66c61-557">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="66c61-558">설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 사용 하 여 버전을 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="66c61-558">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="66c61-559">다음 지침을 설치 하는 데 필요한 단계를 안내 *Visual studio Express 2012 for Web* 사용 하 여 *Microsoft Web Platform Installer*합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-559">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="66c61-560">로 이동 [ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-560">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="66c61-561">또는, 이미 설치한 경우 웹 플랫폼 설치 관리자를 열 수 있습니다 하 고 제품에 대 한 검색 &quot; <em>Visual Studio Express 2012 for Windows Azure SDK를 사용 하 여 Web</em>&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-561">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="66c61-562">클릭할 **지금 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-562">Click on **Install Now**.</span></span> <span data-ttu-id="66c61-563">없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-563">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="66c61-564">한 번 **웹 플랫폼 설치 관리자** 열려 있는 경우 클릭 **설치** 는 설치를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-564">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="66c61-565">![Visual Studio Express를 설치](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "Visual Studio Express를 설치 합니다.")</span><span class="sxs-lookup"><span data-stu-id="66c61-565">![Install Visual Studio Express](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="66c61-566">*Visual Studio Express를 설치 합니다.*</span><span class="sxs-lookup"><span data-stu-id="66c61-566">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="66c61-567">모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-567">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![사용 조건에 동의](aspnet-mvc-4-helpers-forms-and-validation/_static/image23.png)

    <span data-ttu-id="66c61-569">*사용 조건에 동의*</span><span class="sxs-lookup"><span data-stu-id="66c61-569">*Accepting the license terms*</span></span>
5. <span data-ttu-id="66c61-570">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-570">Wait until the downloading and installation process completes.</span></span>

    ![설치 진행률](aspnet-mvc-4-helpers-forms-and-validation/_static/image24.png)

    <span data-ttu-id="66c61-572">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="66c61-572">*Installation progress*</span></span>
6. <span data-ttu-id="66c61-573">설치가 완료 되 면 클릭 **완료**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-573">When the installation completes, click **Finish**.</span></span>

    ![설치 완료](aspnet-mvc-4-helpers-forms-and-validation/_static/image25.png)

    <span data-ttu-id="66c61-575">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="66c61-575">*Installation completed*</span></span>
7. <span data-ttu-id="66c61-576">클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-576">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="66c61-577">로 Visual Studio Express for Web을 열려면 합니다 **시작** 화면 및 쓰기를 시작 &quot; **VS Express**&quot;를 클릭 합니다 **VS Express for Web** 타일입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-577">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 타일](aspnet-mvc-4-helpers-forms-and-validation/_static/image26.png)

    <span data-ttu-id="66c61-579">*VS Express for Web 타일*</span><span class="sxs-lookup"><span data-stu-id="66c61-579">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="66c61-580">부록 b: 코드 조각 사용</span><span class="sxs-lookup"><span data-stu-id="66c61-580">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="66c61-581">코드 조각을 사용 하 여 결정적인 순간에 필요한 모든 코드를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-581">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="66c61-582">랩 문서가 알려줍니다 정확 하 게 사용할 수 있는 시기를 다음 그림과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-582">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="66c61-583">![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드를 삽입할](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "프로젝트에 코드를 삽입 하는 Visual Studio를 사용 하 여 코드 조각을")</span><span class="sxs-lookup"><span data-stu-id="66c61-583">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="66c61-584">*프로젝트에 코드를 삽입 하려면 Visual Studio 코드 조각 사용*</span><span class="sxs-lookup"><span data-stu-id="66c61-584">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="66c61-585">***키보드 (C#만 해당)를 사용 하 여 코드 조각을 추가 하려면***</span><span class="sxs-lookup"><span data-stu-id="66c61-585">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="66c61-586">코드를 삽입 하려는 위치에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-586">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="66c61-587">시작 (공백 없이 하이픈) 조각 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-587">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="66c61-588">IntelliSense 표시 조각 이름과 일치 하는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-588">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="66c61-589">올바른 코드 조각을 선택 합니다 (또는 전체 코드 조각 이름을 선택 될 때까지 입력 유지).</span><span class="sxs-lookup"><span data-stu-id="66c61-589">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="66c61-590">커서 위치에 코드 조각을 삽입 하려면 두 번 탭 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-590">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="66c61-591">![코드 조각 이름을 입력](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "조각 이름을 입력 하기 시작")</span><span class="sxs-lookup"><span data-stu-id="66c61-591">![Start typing the snippet name](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "Start typing the snippet name")</span></span>

<span data-ttu-id="66c61-592">*코드 조각 이름을 입력 하기 시작*</span><span class="sxs-lookup"><span data-stu-id="66c61-592">*Start typing the snippet name*</span></span>

<span data-ttu-id="66c61-593">![Tab 키를 눌러 강조 표시 된 코드 조각을](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "Tab 키를 눌러 강조 표시 된 코드 조각 선택")</span><span class="sxs-lookup"><span data-stu-id="66c61-593">![Press Tab to select the highlighted snippet](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="66c61-594">*Tab 키를 눌러 강조 표시 된 코드 조각 선택*</span><span class="sxs-lookup"><span data-stu-id="66c61-594">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="66c61-595">![Tab 키를 다시 코드 조각 확장 됩니다](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "다시 Tab 키를 누릅니다 하 고 코드 조각에서는 확장")</span><span class="sxs-lookup"><span data-stu-id="66c61-595">![Press Tab again and the snippet will expand](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="66c61-596">*Tab 키를 다시 및 코드 조각에서는 확장*</span><span class="sxs-lookup"><span data-stu-id="66c61-596">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="66c61-597">***마우스 (C#, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가할*** 1입니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-597">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="66c61-598">코드 조각을 삽입 하려면 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-598">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="66c61-599">선택 **코드 조각 삽입** 뒤 **내 코드 조각**합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-599">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="66c61-600">클릭 하 여 목록에서 관련 코드 조각을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="66c61-600">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="66c61-601">![코드 조각을 삽입 하 고 코드 조각 삽입을 선택 하려는 마우스 오른쪽 단추로 클릭](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "코드 조각을 삽입 하 고 코드 조각 삽입을 선택 하려는 마우스 오른쪽 단추로 클릭")</span><span class="sxs-lookup"><span data-stu-id="66c61-601">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="66c61-602">*코드 조각을 삽입할 선택한 코드 조각 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭*</span><span class="sxs-lookup"><span data-stu-id="66c61-602">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="66c61-603">![클릭 하 여 목록에서 관련 코드 조각 선택](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "클릭 하 여 목록에서 관련 코드 조각 선택")</span><span class="sxs-lookup"><span data-stu-id="66c61-603">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="66c61-604">*클릭 하 여 목록에서 관련 코드 조각 선택*</span><span class="sxs-lookup"><span data-stu-id="66c61-604">*Pick the relevant snippet from the list, by clicking on it*</span></span>
