---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
title: ASP.NET MVC 4 Entity Framework 스 캐 폴딩 및 마이그레이션 | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4 컨트롤러 메서드에 익숙한 경우 또는 완료에서 &quot;도우미, 폼 및 유효성 검사&quot; 실습 랩 알고 있어야...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 093c1362-f10b-407c-a708-be370f4b62b0
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
msc.type: authoredcontent
ms.openlocfilehash: 548afe1926eed49841251832d54dc213da0cb753
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="aspnet-mvc-4-entity-framework-scaffolding-and-migrations"></a><span data-ttu-id="37afd-103">ASP.NET MVC 4 Entity Framework 스 캐 폴딩 및 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="37afd-103">ASP.NET MVC 4 Entity Framework Scaffolding and Migrations</span></span>

<span data-ttu-id="37afd-104">으로 [웹 캠프 팀](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="37afd-104">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="37afd-105">웹 캠프 학습 키트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="37afd-106">ASP.NET MVC 4 컨트롤러 메서드에 익숙한 경우 또는 완료에서 &quot;도우미, 폼 및 유효성 검사&quot; 실습 랩 수 있는지, 만들 논리를 다양 한 업데이트, 목록 및 반복 되는 데이터 엔터티를 제거 합니다. 간에 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-106">If you are familiar with ASP.NET MVC 4 controller methods, or have completed the &quot;Helpers, Forms and Validation&quot; Hands-On lab, you should be aware that many of the logic to create, update, list and remove any data entity it is repeated among the application.</span></span> <span data-ttu-id="37afd-107">있음은 물론, 하는 모델을 조작 하는 여러 클래스에 있으면 각 엔터티 작업 뿐만 아니라 각 보기에 대 한 POST 및 GET 작업 메서드를 작성 하는 시간이 많이 소요 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-107">Not to mention that, if your model has several classes to manipulate, you will be likely to spend a considerable time writing the POST and GET action methods for each entity operation, as well as each of the views.</span></span>

<span data-ttu-id="37afd-108">이 랩에서 자동으로 응용 프로그램의 CRUD (만들기, 읽기, 업데이트 및 삭제)의 기준선을 생성 하는 ASP.NET MVC 4 기반 구조를 사용 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-108">In this lab you will learn how to use the ASP.NET MVC 4 scaffolding to automatically generate the baseline of your application's CRUD (Create, Read, Update and Delete).</span></span> <span data-ttu-id="37afd-109">시작 간단한 모델 클래스에서 코드의 한 줄도 작성 하지 않고, 만듭니다으로 모든 CRUD 작업의 모든 필요한 뷰를 포함 하는 컨트롤러.</span><span class="sxs-lookup"><span data-stu-id="37afd-109">Starting from a simple model class, and, without writing a single line of code, you will create a controller that will contain all the CRUD operations, as well as the all the necessary views.</span></span> <span data-ttu-id="37afd-110">빌드하고 간단한 솔루션을 실행 한 후 응용 프로그램 데이터베이스의 MVC 논리 및 데이터 조작에 대 한 보기와 함께 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-110">After building and running the simple solution, you will have the application database generated, together with the MVC logic and views for data manipulation.</span></span>

<span data-ttu-id="37afd-111">또한 전체 응용 프로그램 전반에 걸쳐 모델 업데이트를 수행 하려면 Entity Framework 마이그레이션을 사용 하는 것이 얼마나 쉬운지에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-111">In addition, you will learn how easy it is to use Entity Framework Migrations to perform model updates throughout your entire application.</span></span> <span data-ttu-id="37afd-112">Entity Framework 마이그레이션 간단한 단계만 거치면 모델 변경 된 후 데이터베이스를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-112">Entity Framework Migrations will let you modify your database after the model has changed with simple steps.</span></span> <span data-ttu-id="37afd-113">이러한 모든 염두에서,와 됩니다 구축 하 고 웹 응용 프로그램을 보다 효율적으로 관리할 수 ASP.NET MVC 4의 최신 기능을 활용 하기 위해.</span><span class="sxs-lookup"><span data-stu-id="37afd-113">With all these in mind, you will be able to build and maintain web applications more efficiently, taking advantage of the latest features of ASP.NET MVC 4.</span></span>

> [!NOTE]
> <span data-ttu-id="37afd-114">모든 샘플 코드와 코드 조각을 웹 캠프 교육 키트에서 사용할 수에 포함 된 [Microsoft-웹/WebCampTrainingKit 릴리스](https://aka.ms/webcamps-training-kit)합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-114">All sample code and snippets are included in the Web Camps Training Kit, available from at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="37afd-115">이 랩에 특정 프로젝트에서 사용할 수는 [ASP.NET MVC 4 Entity Framework 스 캐 폴딩 및 마이그레이션을](https://github.com/Microsoft-Web/HOL-EntityFrameworkScaffoldingAndMigrations)합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-115">The project specific to this lab is available at [ASP.NET MVC 4 Entity Framework Scaffolding and Migrations](https://github.com/Microsoft-Web/HOL-EntityFrameworkScaffoldingAndMigrations).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="37afd-116">목표</span><span class="sxs-lookup"><span data-stu-id="37afd-116">Objectives</span></span>

<span data-ttu-id="37afd-117">이 실습 랩에서 배우게 됩니다 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="37afd-117">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="37afd-118">컨트롤러의 CRUD 작업에 대해 ASP.NET 스 캐 폴딩을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-118">Use ASP.NET scaffolding for CRUD operations in controllers.</span></span>
- <span data-ttu-id="37afd-119">Entity Framework 마이그레이션을 사용 하 여 데이터베이스 모델을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-119">Change the database model using Entity Framework Migrations.</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="37afd-120">전제 조건</span><span class="sxs-lookup"><span data-stu-id="37afd-120">Prerequisites</span></span>

<span data-ttu-id="37afd-121">이 랩을 완료 하려면 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-121">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="37afd-122">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) 하거나 그 보다 뛰어난 (읽기 [부록 A](#AppendixA) 설치 하는 방법에 대 한 지침은).</span><span class="sxs-lookup"><span data-stu-id="37afd-122">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="37afd-123">설정</span><span class="sxs-lookup"><span data-stu-id="37afd-123">Setup</span></span>

<span data-ttu-id="37afd-124">**설치 하는 코드 조각**</span><span class="sxs-lookup"><span data-stu-id="37afd-124">**Installing Code Snippets**</span></span>

<span data-ttu-id="37afd-125">편의 위해는이 랩에 따라 관리 코드의 대부분 Visual Studio 코드 조각 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-125">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="37afd-126">실행 코드 조각을 설치 하려면 **.\Source\Setup\CodeSnippets.vsi** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-126">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="37afd-127">이 문서에서 부록을 참조할 수 사용 하는 방법에 알아봅니다 사용 하 고 Visual Studio 코드 조각에 익숙한 경우 &quot; [부록 b:를 사용 하 여 코드 조각을](#AppendixB)&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-127">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="37afd-128">연습</span><span class="sxs-lookup"><span data-stu-id="37afd-128">Exercises</span></span>

<span data-ttu-id="37afd-129">다음 연습 실습 랩이를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-129">The following exercise make up this Hands-On Lab:</span></span>

1. [<span data-ttu-id="37afd-130">ASP.NET MVC 4 스 캐 폴딩을 사용 하 여 Entity Framework 마이그레이션과 함께</span><span class="sxs-lookup"><span data-stu-id="37afd-130">Using ASP.NET MVC 4 Scaffolding with Entity Framework Migrations</span></span>](#Exercise1)

> [!NOTE]
> <span data-ttu-id="37afd-131">이 연습 동반 되는 **끝** 연습을 완료 한 후 가져와야 생성 되는 솔루션에 포함 된 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-131">This exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercise.</span></span> <span data-ttu-id="37afd-132">연습을 통해 작업 하 고 추가 도움이 필요한 경우이 솔루션 가이드로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-132">You can use this solution as a guide if you need additional help working through the exercise.</span></span>


<span data-ttu-id="37afd-133">예상 소요 시간: **30 분**</span><span class="sxs-lookup"><span data-stu-id="37afd-133">Estimated time to complete this lab: **30 minutes**</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Using_ASPNET_MVC_4_Scaffolding_with_Entity_Framework_Migrations"></a>
### <a name="exercise-1-using-aspnet-mvc-4-scaffolding-with-entity-framework-migrations"></a><span data-ttu-id="37afd-134">연습 1: 스 캐 폴딩 ASP.NET MVC 4 사용 하 여 Entity Framework 마이그레이션과 함께</span><span class="sxs-lookup"><span data-stu-id="37afd-134">Exercise 1: Using ASP.NET MVC 4 Scaffolding with Entity Framework Migrations</span></span>

<span data-ttu-id="37afd-135">ASP.NET MVC 스 캐 폴딩 데이터베이스 계층 상호 작용 하는 응용 프로그램 수 있도록 하는 데 필요한 논리를 만드는 표준화 된 방식으로 CRUD 작업을 생성 하는 빠른 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-135">ASP.NET MVC scaffolding provides a quick way to generate the CRUD operations in a standardized way, creating the necessary logic that lets your application interact with the database layer.</span></span>

<span data-ttu-id="37afd-136">이 연습에서는 CRUD 메서드를 만들려면 먼저 ASP.NET MVC 4 스 캐 폴딩 코드와 함께 사용 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-136">In this exercise, you will learn how to use ASP.NET MVC 4 scaffolding with code first to create the CRUD methods.</span></span> <span data-ttu-id="37afd-137">그런 다음 데이터베이스에 변경 내용을 적용 하는 Entity Framework 마이그레이션을 사용 하 여 모델을 업데이트 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-137">Then, you will learn how to update your model applying the changes in the database by using Entity Framework Migrations.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1-_Creating_a_new_ASPNET_MVC_4_project_using_Scaffolding"></a>
#### <a name="task-1--creating-a-new-aspnet-mvc-4-project-using-scaffolding"></a><span data-ttu-id="37afd-138">스 캐 폴딩을 사용 하 여 작업 1-Creating 새 ASP.NET MVC 4 프로젝트</span><span class="sxs-lookup"><span data-stu-id="37afd-138">Task 1- Creating a new ASP.NET MVC 4 project using Scaffolding</span></span>

1. <span data-ttu-id="37afd-139">아직 열지 않은 경우 시작 **Visual Studio 2012**합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-139">If not already open, start **Visual Studio 2012**.</span></span>
2. <span data-ttu-id="37afd-140">선택 **파일 | 새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-140">Select **File | New Project**.</span></span> <span data-ttu-id="37afd-141">새로 만들기 대화 상자에서를 아래에서 프로젝트는 **Visual C# | 웹** 섹션에서 **ASP.NET MVC 4 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-141">In the New Project dialog, under the **Visual C# | Web** section, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="37afd-142">에 프로젝트 이름을 **MVC4andEFMigrations** 위치를 설정 하 고 **Source\Ex1 UsingMVC4ScaffoldingEFMigrations** 이 랩의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-142">Name the project to **MVC4andEFMigrations** and set the location to **Source\Ex1-UsingMVC4ScaffoldingEFMigrations** folder of this lab.</span></span> <span data-ttu-id="37afd-143">설정의 **솔루션 이름** 를 **시작** 확인 **솔루션용 디렉터리 만들기** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-143">Set the **Solution name** to **Begin** and ensure **Create directory for solution** is checked.</span></span> <span data-ttu-id="37afd-144">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-144">Click **OK**.</span></span>

    <span data-ttu-id="37afd-145">![새 ASP.NET MVC 4 프로젝트 대화 상자](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image1.png "새 ASP.NET MVC 4 프로젝트 대화 상자")</span><span class="sxs-lookup"><span data-stu-id="37afd-145">![New ASP.NET MVC 4 Project Dialog Box](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image1.png "New ASP.NET MVC 4 Project Dialog Box")</span></span>

    <span data-ttu-id="37afd-146">*새 ASP.NET MVC 4 프로젝트 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="37afd-146">*New ASP.NET MVC 4 Project Dialog Box*</span></span>
3. <span data-ttu-id="37afd-147">에 **새 ASP.NET MVC 4 프로젝트** 대화 상자 선택은 **인터넷 응용 프로그램** 서식 파일을 있는지 확인 하 고 **Razor** 은 선택한 **뷰 엔진**.</span><span class="sxs-lookup"><span data-stu-id="37afd-147">In the **New ASP.NET MVC 4 Project** dialog box select the **Internet Application** template, and make sure that **Razor** is the selected **View engine**.</span></span> <span data-ttu-id="37afd-148">**확인**을 클릭해 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-148">Click **OK** to create the project.</span></span>

    <span data-ttu-id="37afd-149">![새 ASP.NET MVC 4 인터넷 응용 프로그램](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image2.png "새 ASP.NET MVC 4 인터넷 응용 프로그램")</span><span class="sxs-lookup"><span data-stu-id="37afd-149">![New ASP.NET MVC 4 Internet Application](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image2.png "New ASP.NET MVC 4 Internet Application")</span></span>

    <span data-ttu-id="37afd-150">*새 ASP.NET MVC 4 인터넷 응용 프로그램*</span><span class="sxs-lookup"><span data-stu-id="37afd-150">*New ASP.NET MVC 4 Internet Application*</span></span>
4. <span data-ttu-id="37afd-151">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 **모델** 선택 **추가 | 클래스** 간단한 클래스 사람 POCO ()를 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-151">In the Solution Explorer, right-click **Models** and select **Add | Class** to create a simple class person (POCO).</span></span> <span data-ttu-id="37afd-152">이름을 **사람** 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-152">Name it **Person** and click **OK**.</span></span>
5. <span data-ttu-id="37afd-153">사용자 클래스를 열고 다음 속성을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-153">Open the Person class and insert the following properties.</span></span>

    <span data-ttu-id="37afd-154">(코드 조각- *ASP.NET MVC 4 및 Entity Framework 마이그레이션-e x 1 사람 속성*)</span><span class="sxs-lookup"><span data-stu-id="37afd-154">(Code Snippet - *ASP.NET MVC 4 and Entity Framework Migrations - Ex1 Person Properties*)</span></span>


~~~
[!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample1.cs)]
~~~
6. <span data-ttu-id="37afd-155">클릭 **빌드 | 솔루션 빌드** 는 변경 내용을 저장 하는 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-155">Click **Build | Build Solution** to save the changes and build the project.</span></span>

    <span data-ttu-id="37afd-156">![응용 프로그램 빌드](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image3.png "응용 프로그램 빌드")</span><span class="sxs-lookup"><span data-stu-id="37afd-156">![Building the application](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image3.png "Building the application")</span></span>

    <span data-ttu-id="37afd-157">*응용 프로그램 빌드*</span><span class="sxs-lookup"><span data-stu-id="37afd-157">*Building the Application*</span></span>
7. <span data-ttu-id="37afd-158">솔루션 탐색기에서 controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가 | 컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-158">In the Solution Explorer, right-click the controllers folder and select **Add | Controller**.</span></span>
8. <span data-ttu-id="37afd-159">컨트롤러 이름을 *PersonController* 완료는 **스 캐 폴딩 옵션** 다음 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-159">Name the controller *PersonController* and complete the **Scaffolding options** with the following values.</span></span>

   1. <span data-ttu-id="37afd-160">에 **템플릿** 드롭 다운 목록에서 **읽기/쓰기 동작 및 뷰가, Entity Framework를 사용 하 여 포함 된 MVC 컨트롤러** 옵션.</span><span class="sxs-lookup"><span data-stu-id="37afd-160">In the **Template** drop-down list, select the **MVC controller with read/write actions and views, using Entity Framework** option.</span></span>
   2. <span data-ttu-id="37afd-161">에 **모델 클래스** 드롭 다운 목록에서 **사람** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-161">In the **Model class** drop-down list, select the **Person** class.</span></span>
   3. <span data-ttu-id="37afd-162">에 **데이터 컨텍스트 클래스** 목록에서  **&lt;새 데이터 컨텍스트에... &gt;**.</span><span class="sxs-lookup"><span data-stu-id="37afd-162">In the **Data Context class** list, select **&lt;New data context...&gt;**.</span></span> <span data-ttu-id="37afd-163">모든 이름을 선택 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-163">Choose any name and click **OK**.</span></span>
   4. <span data-ttu-id="37afd-164">에 **뷰** 드롭 다운 목록에서 다음 사항을 확인 **Razor** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-164">In the **Views** drop-down list, make sure that **Razor** is selected.</span></span>

      <span data-ttu-id="37afd-165">![스 캐 폴딩에 사람 컨트롤러 추가](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image4.png "스 캐 폴딩에 사람 컨트롤러 추가")</span><span class="sxs-lookup"><span data-stu-id="37afd-165">![Adding the Person controller with scaffolding](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image4.png "Adding the Person controller with scaffolding")</span></span>

      <span data-ttu-id="37afd-166">*스 캐 폴딩에 사람 컨트롤러 추가*</span><span class="sxs-lookup"><span data-stu-id="37afd-166">*Adding the Person controller with scaffolding*</span></span>
9. <span data-ttu-id="37afd-167">클릭 **추가** 사람에 대 한 새 컨트롤러 스 캐 폴딩을 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-167">Click **Add** to create the new controller for Person with scaffolding.</span></span> <span data-ttu-id="37afd-168">이제 컨트롤러 작업 뿐만 아니라 뷰를 생성 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-168">You have now generated the controller actions as well as the views.</span></span>

    <span data-ttu-id="37afd-169">![스 캐 폴딩을 사용 사람 컨트롤러를 만든 다음](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image5.png "스 캐 폴딩을 사용 사람 컨트롤러를 만든 다음")</span><span class="sxs-lookup"><span data-stu-id="37afd-169">![After creating the Person controller with scaffolding](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image5.png "After creating the Person controller with scaffolding")</span></span>

    <span data-ttu-id="37afd-170">*스 캐 폴딩을 사용 사람 컨트롤러를 만든 다음*</span><span class="sxs-lookup"><span data-stu-id="37afd-170">*After creating the Person controller with scaffolding*</span></span>
10. <span data-ttu-id="37afd-171">열기 **PersonController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-171">Open **PersonController** class.</span></span> <span data-ttu-id="37afd-172">전체 CRUD 작업 메서드를 자동으로 생성 된 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-172">Notice that the full CRUD action methods have been generated automatically.</span></span>

   <span data-ttu-id="37afd-173">![Person 컨트롤러 내](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image6.png "사람 내부 컨트롤러")</span><span class="sxs-lookup"><span data-stu-id="37afd-173">![Inside the Person controller](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image6.png "Inside the Person controller")</span></span>

   <span data-ttu-id="37afd-174">*사람 컨트롤러 내*</span><span class="sxs-lookup"><span data-stu-id="37afd-174">*Inside the Person controller*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2-_Running_the_application"></a>
#### <a name="task-2--running-the-application"></a><span data-ttu-id="37afd-175">작업 2-실행 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="37afd-175">Task 2- Running the application</span></span>

<span data-ttu-id="37afd-176">이 시점에서 데이터베이스 아직 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-176">At this point, the database is not yet created.</span></span> <span data-ttu-id="37afd-177">이 태스크에서는 처음으로 응용 프로그램을 실행 하 고 CRUD 작업을 테스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-177">In this task, you will run the application for the first time and test the CRUD operations.</span></span> <span data-ttu-id="37afd-178">데이터베이스에서 Code First를 사용 하 여 즉시 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-178">The database will be created on the fly with Code First.</span></span>

1. <span data-ttu-id="37afd-179">**F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-179">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="37afd-180">브라우저에서 추가 **/Person** 사용자 페이지를 열려면 URL에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-180">In the browser, add **/Person** to the URL to open the Person page.</span></span>

    <span data-ttu-id="37afd-181">![응용 프로그램 먼저 실행](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image7.png "응용 프로그램 먼저 실행")</span><span class="sxs-lookup"><span data-stu-id="37afd-181">![Application first run](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image7.png "Application first run")</span></span>

    <span data-ttu-id="37afd-182">*응용 프로그램: 먼저 실행 합니다.*</span><span class="sxs-lookup"><span data-stu-id="37afd-182">*Application: first run*</span></span>
3. <span data-ttu-id="37afd-183">이제 사용자 페이지 탐색 및 CRUD 작업을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-183">You will now explore the Person pages and test the CRUD operations.</span></span>

    1. <span data-ttu-id="37afd-184">클릭 **새로 만들기** 새 사람을 추가 하려면.</span><span class="sxs-lookup"><span data-stu-id="37afd-184">Click **Create New** to add a new person.</span></span> <span data-ttu-id="37afd-185">첫 번째 이름 및 성을 입력 하 고 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-185">Enter a first name and a last name and click **Create**.</span></span>

        <span data-ttu-id="37afd-186">![새로운 사람 추가](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image8.png "새 사용자 추가")</span><span class="sxs-lookup"><span data-stu-id="37afd-186">![Adding a new person](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image8.png "Adding a new person")</span></span>

        <span data-ttu-id="37afd-187">*새 사용자 추가*</span><span class="sxs-lookup"><span data-stu-id="37afd-187">*Adding a new person*</span></span>
    2. <span data-ttu-id="37afd-188">사용자의 목록에서 삭제, 편집 하거나 항목을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-188">In the person's list, you can delete, edit or add items.</span></span>

        <span data-ttu-id="37afd-189">![개인 목록](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image9.png "개인 목록")</span><span class="sxs-lookup"><span data-stu-id="37afd-189">![person list](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image9.png "person list")</span></span>

        <span data-ttu-id="37afd-190">*개인 목록*</span><span class="sxs-lookup"><span data-stu-id="37afd-190">*Person list*</span></span>
    3. <span data-ttu-id="37afd-191">클릭 **세부 정보** 를 사용자의 세부 정보를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-191">Click **Details** to open the person's details.</span></span>

        <span data-ttu-id="37afd-192">![사용자의 세부 정보](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image10.png "사용자의 세부 정보")</span><span class="sxs-lookup"><span data-stu-id="37afd-192">![Person's details](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image10.png "Person's details")</span></span>

        <span data-ttu-id="37afd-193">*사용자의 세부 정보*</span><span class="sxs-lookup"><span data-stu-id="37afd-193">*Person's details*</span></span>
4. <span data-ttu-id="37afd-194">브라우저를 닫고 Visual Studio로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-194">Close the browser and return to Visual Studio.</span></span> <span data-ttu-id="37afd-195">만든 사람 엔터티에 대 한 전체 CRUD 보기에 모델--에서 응용 프로그램 전체에서 코드를 전혀 작성 하지 않고도 점에 주의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="37afd-195">Notice that you have created the whole CRUD for the person entity throughout your application -from the model to the views- without having to write a single line of code!</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3-_Updating_the_database_using_Entity_Framework_Migrations"></a>
#### <a name="task-3--updating-the-database-using-entity-framework-migrations"></a><span data-ttu-id="37afd-196">작업 3-업데이트 Entity Framework 마이그레이션을 사용 하 여 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="37afd-196">Task 3- Updating the database using Entity Framework Migrations</span></span>

<span data-ttu-id="37afd-197">이 작업에서는 Entity Framework 마이그레이션을 사용 하 여 데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-197">In this task you will update the database using Entity Framework Migrations.</span></span> <span data-ttu-id="37afd-198">모델을 변경 하 고 Entity Framework 마이그레이션 기능을 사용 하 여 데이터베이스에서 변경 내용을 반영 하는 것이 얼마나 쉬운지에서 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-198">You will discover how easy it is to change the model and reflect the changes in your databases by using the Entity Framework Migrations feature.</span></span>

1. <span data-ttu-id="37afd-199">패키지 관리자 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-199">Open the Package Manager Console.</span></span> <span data-ttu-id="37afd-200">선택 **도구 | 라이브러리 패키지 관리자 | 패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-200">Select **Tools | Library Package Manager | Package Manager Console**.</span></span>
2. <span data-ttu-id="37afd-201">패키지 관리자 콘솔에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-201">In the Package Manager Console, enter the following command:</span></span>

    <span data-ttu-id="37afd-202">PMC</span><span class="sxs-lookup"><span data-stu-id="37afd-202">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample2.ps1)]

    <span data-ttu-id="37afd-203">![마이그레이션을 사용 하도록 설정](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image11.png "마이그레이션을 사용 하도록 설정")</span><span class="sxs-lookup"><span data-stu-id="37afd-203">![Enabling Migrations](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image11.png "Enabling Migrations")</span></span>

    <span data-ttu-id="37afd-204">*마이그레이션을 사용 하도록 설정*</span><span class="sxs-lookup"><span data-stu-id="37afd-204">*Enabling migrations*</span></span>

    <span data-ttu-id="37afd-205">마이그레이션을 사용 하도록 설정 명령은 만듭니다는 **마이그레이션** 데이터베이스 초기화에 스크립트가 들어 있는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-205">The Enable-Migration command creates the **Migrations** folder, which contains a script to initialize the database.</span></span>

    <span data-ttu-id="37afd-206">![Migrations 폴더](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image12.png "Migrations 폴더")</span><span class="sxs-lookup"><span data-stu-id="37afd-206">![Migrations folder](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image12.png "Migrations folder")</span></span>

    <span data-ttu-id="37afd-207">*Migrations 폴더*</span><span class="sxs-lookup"><span data-stu-id="37afd-207">*Migrations folder*</span></span>
3. <span data-ttu-id="37afd-208">열기는 **Configuration.cs** Migrations 폴더에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-208">Open the **Configuration.cs** file in the Migrations folder.</span></span> <span data-ttu-id="37afd-209">클래스 생성자를 찾아 변경는 **AutomaticMigrationsEnabled** 값을 *true*합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-209">Locate the class constructor and change the **AutomaticMigrationsEnabled** value to *true*.</span></span>


~~~
[!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample3.cs)]
~~~
4. <span data-ttu-id="37afd-210">사용자 클래스를 열고 있는 사람의 중간 이름을 대 한 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-210">Open the Person class and add an attribute for the person's middle name.</span></span> <span data-ttu-id="37afd-211">이 새 특성으로 모델을 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-211">With this new attribute, you are changing the model.</span></span>


~~~
[!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample4.cs)]
~~~
5. <span data-ttu-id="37afd-212">선택 **빌드 | 솔루션 빌드** 메뉴에서 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-212">Select **Build | Build Solution** on the menu to build the application.</span></span>

    <span data-ttu-id="37afd-213">![응용 프로그램 빌드](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image13.png "응용 프로그램 빌드")</span><span class="sxs-lookup"><span data-stu-id="37afd-213">![Building the application](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image13.png "Building the application")</span></span>

    <span data-ttu-id="37afd-214">*응용 프로그램 빌드*</span><span class="sxs-lookup"><span data-stu-id="37afd-214">*Building the application*</span></span>
6. <span data-ttu-id="37afd-215">패키지 관리자 콘솔에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-215">In the Package Manager Console, enter the following command:</span></span>

    <span data-ttu-id="37afd-216">PMC</span><span class="sxs-lookup"><span data-stu-id="37afd-216">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample5.ps1)]

    <span data-ttu-id="37afd-217">이 명령은 데이터 개체의 변경 내용을 찾아서 그런 다음 데이터베이스를 적절 하 게 수정 하는 데 필요한 명령을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-217">This command will look for changes in the data objects, and then, it will add the necessary commands to modify the database accordingly.</span></span>

    <span data-ttu-id="37afd-218">![중간 이름 추가](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image14.png "중간 이름 추가")</span><span class="sxs-lookup"><span data-stu-id="37afd-218">![Adding a middle name](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image14.png "Adding a middle name")</span></span>

    <span data-ttu-id="37afd-219">*중간 이름 추가*</span><span class="sxs-lookup"><span data-stu-id="37afd-219">*Adding a middle name*</span></span>
7. <span data-ttu-id="37afd-220">(선택 사항) 차등 업데이트와 함께 SQL 스크립트를 생성 하려면 다음 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-220">(Optional) You can run the following command to generate a SQL script with the differential update.</span></span> <span data-ttu-id="37afd-221">그러면 데이터베이스를 수동으로 업데이트할 수 있습니다 (이 경우에 필요 없는), 또는 다른 데이터베이스의 변경 내용을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-221">This will let you update the database manually (In this case it's not necessary), or apply the changes in other databases:</span></span>

    <span data-ttu-id="37afd-222">PMC</span><span class="sxs-lookup"><span data-stu-id="37afd-222">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample6.ps1)]

    <span data-ttu-id="37afd-223">![SQL 스크립트를 생성](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image15.png "SQL 스크립트 생성")</span><span class="sxs-lookup"><span data-stu-id="37afd-223">![Generating a SQL script](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image15.png "Generating a SQL script")</span></span>

    <span data-ttu-id="37afd-224">*SQL 스크립트 생성*</span><span class="sxs-lookup"><span data-stu-id="37afd-224">*Generating a SQL script*</span></span>

    <span data-ttu-id="37afd-225">![SQL 스크립트 업데이트](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image16.png "SQL 스크립트 업데이트")</span><span class="sxs-lookup"><span data-stu-id="37afd-225">![SQL Script update](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image16.png "SQL Script update")</span></span>

    <span data-ttu-id="37afd-226">*SQL 스크립트 업데이트*</span><span class="sxs-lookup"><span data-stu-id="37afd-226">*SQL Script update*</span></span>
8. <span data-ttu-id="37afd-227">패키지 관리자 콘솔에서 데이터베이스를 업데이트 하려면 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-227">In the Package Manager Console, enter the following command to update the database:</span></span>

    <span data-ttu-id="37afd-228">PMC</span><span class="sxs-lookup"><span data-stu-id="37afd-228">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample7.ps1)]

    <span data-ttu-id="37afd-229">![데이터베이스 업데이트](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image17.png "데이터베이스 업데이트")</span><span class="sxs-lookup"><span data-stu-id="37afd-229">![Updating the Database](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image17.png "Updating the Database")</span></span>

    <span data-ttu-id="37afd-230">*데이터베이스 업데이트*</span><span class="sxs-lookup"><span data-stu-id="37afd-230">*Updating the Database*</span></span>

    <span data-ttu-id="37afd-231">이렇게 하면 추가 됩니다는 **MiddleName** 열에는 **사람** 테이블의 현재 정의가 일치 하도록는 **사람** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-231">This will add the **MiddleName** column in the **People** table to match the current definition of the **Person** class.</span></span>
9. <span data-ttu-id="37afd-232">데이터베이스를 업데이트 후 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가 | 컨트롤러** 컨트롤러 추가 하는 사람 다시 (동일한 값을 가진 전체).</span><span class="sxs-lookup"><span data-stu-id="37afd-232">Once the database is updated, right-click the Controller folder and select **Add | Controller** to add the Person controller again (Complete with the same values).</span></span> <span data-ttu-id="37afd-233">이렇게 하면 기존 방법 및 새 특성을 추가 하는 뷰 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-233">This will update the existing methods and views adding the new attribute.</span></span>

    <span data-ttu-id="37afd-234">![컨트롤러 업데이트 추가](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image18.png "컨트롤러 업데이트 추가")</span><span class="sxs-lookup"><span data-stu-id="37afd-234">![Adding a controller update](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image18.png "Adding a controller update")</span></span>

    <span data-ttu-id="37afd-235">*컨트롤러 업데이트*</span><span class="sxs-lookup"><span data-stu-id="37afd-235">*Updating the controller*</span></span>
10. <span data-ttu-id="37afd-236">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-236">Click **Add**.</span></span> <span data-ttu-id="37afd-237">값을 선택한 다음, **덮어쓰기 PersonController.cs** 및 **덮어쓰기 관련 뷰** 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-237">Then, select the values **Overwrite PersonController.cs** and the **Overwrite associated views** and click **OK**.</span></span>

   ![컨트롤러 덮어쓰기 추가](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image19.png)

   <span data-ttu-id="37afd-239">*컨트롤러 업데이트*</span><span class="sxs-lookup"><span data-stu-id="37afd-239">*Updating the controller*</span></span>

<a id="Ex1Task4"></a>

<a id="Task4-_Running_the_application"></a>
#### <a name="task4--running-the-application"></a><span data-ttu-id="37afd-240">Task4-응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-240">Task4- Running the application</span></span>

1. <span data-ttu-id="37afd-241">**F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-241">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="37afd-242">열기 **/Person**합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-242">Open **/Person**.</span></span> <span data-ttu-id="37afd-243">중간 이름 열이 추가 하는 동안 데이터를 보존 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-243">Notice that the data was preserved, while the middle name column was added.</span></span>

    <span data-ttu-id="37afd-244">![중간 이름 추가](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image20.png "중간 이름 추가")</span><span class="sxs-lookup"><span data-stu-id="37afd-244">![Middle Name added](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image20.png "Middle Name added")</span></span>

    <span data-ttu-id="37afd-245">*중간 이름 추가*</span><span class="sxs-lookup"><span data-stu-id="37afd-245">*Middle Name added*</span></span>
3. <span data-ttu-id="37afd-246">클릭 하면 **편집**, 현재 사용자에 게 중간 이름을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-246">If you click **Edit**, you will be able to add a middle name to the current person.</span></span>

    <span data-ttu-id="37afd-247">![중간 이름 버전](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image21.png "중간 이름 버전")</span><span class="sxs-lookup"><span data-stu-id="37afd-247">![Middle Name edition](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image21.png "Middle Name edition")</span></span>

* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="37afd-248">요약</span><span class="sxs-lookup"><span data-stu-id="37afd-248">Summary</span></span>

<span data-ttu-id="37afd-249">이 실습 랩에서 간단한 단계를 ASP.NET MVC 4 스 캐 폴딩이 모든 모델 클래스를 사용 하 여와 CRUD 작업을 만드는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-249">In this Hands-On lab, you have learned simple steps to create CRUD operations with ASP.NET MVC 4 Scaffolding using any model class.</span></span> <span data-ttu-id="37afd-250">그런 다음 엔터티 프레임 워크 마이그레이션을 사용 하 여 보기에는 데이터베이스에서 응용 프로그램에 대 한 종단 간 업데이트를 수행 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-250">Then, you have learned how to perform an end to end update in your application -from the database to the views- by using Entity Framework Migrations.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="37afd-251">부록 a: 설치 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="37afd-251">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="37afd-252">설치할 수 있습니다 **Microsoft Visual Studio Express 2012 for Web** 또는 다른 &quot;Express&quot; 버전을 사용 하 여 **[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="37afd-252">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="37afd-253">다음 지침을 설치 하는 데 필요한 단계를 안내 하 *Visual studio Express 2012 for Web* 를 사용 하 여 *Microsoft 웹 플랫폼 설치 관리자*합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-253">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="37afd-254">로 이동 [ [ https://go.microsoft.com/? linkid = 9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-254">Go to [[https://go.microsoft.com/? linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="37afd-255">또는 이미 설치 된 웹 플랫폼 설치 관리자를 열 수 있습니다 및 제품에 대 한 검색 &quot; <em>Visual Studio Express 2012 for Web Windows Azure SDK와</em>&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-255">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="37afd-256">클릭 **지금 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-256">Click on **Install Now**.</span></span> <span data-ttu-id="37afd-257">없는 경우 **웹 플랫폼 설치 관리자** 를 다운로드 하 여 앱을 먼저 설치 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-257">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="37afd-258">한 번 **웹 플랫폼 설치 관리자** 열려 클릭 **설치** 는 설치 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-258">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="37afd-259">![Visual Studio Express 설치](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image22.png "Visual Studio Express 설치")</span><span class="sxs-lookup"><span data-stu-id="37afd-259">![Install Visual Studio Express](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image22.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="37afd-260">*Visual Studio Express 설치*</span><span class="sxs-lookup"><span data-stu-id="37afd-260">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="37afd-261">모든 제품의 라이선스 및 용어를 읽고 클릭 **동의** 를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-261">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![사용 조건 동의](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image23.png)

    <span data-ttu-id="37afd-263">*사용 조건 동의*</span><span class="sxs-lookup"><span data-stu-id="37afd-263">*Accepting the license terms*</span></span>
5. <span data-ttu-id="37afd-264">다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-264">Wait until the downloading and installation process completes.</span></span>

    ![설치 진행률](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image24.png)

    <span data-ttu-id="37afd-266">*설치 진행률*</span><span class="sxs-lookup"><span data-stu-id="37afd-266">*Installation progress*</span></span>
6. <span data-ttu-id="37afd-267">설치가 완료 되 면 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-267">When the installation completes, click **Finish**.</span></span>

    ![설치 완료](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image25.png)

    <span data-ttu-id="37afd-269">*설치 완료*</span><span class="sxs-lookup"><span data-stu-id="37afd-269">*Installation completed*</span></span>
7. <span data-ttu-id="37afd-270">클릭 **종료** 를 웹 플랫폼 설치 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-270">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="37afd-271">Visual Studio Express for Web을 열려면로 이동는 **시작** 화면를 쓰기 시작할 &quot; **VS Express**&quot;, 클릭는 **VS Express for Web** 바둑판식 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-271">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![웹 타일에 대 한 VS Express](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image26.png)

    <span data-ttu-id="37afd-273">*웹 타일에 대 한 VS Express*</span><span class="sxs-lookup"><span data-stu-id="37afd-273">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="37afd-274">부록 b: 코드 조각을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="37afd-274">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="37afd-275">코드 조각 바로 쉽게 얻습니다 필요한 코드를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-275">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="37afd-276">랩 문서는 알려 정확 하 게 사용 가능 시기, 다음 그림에 나와 있는 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-276">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="37afd-277">![Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image27.png "Visual Studio를 사용 하 여 코드 조각을 프로젝트에 코드를 삽입 하려면")</span><span class="sxs-lookup"><span data-stu-id="37afd-277">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image27.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="37afd-278">*Visual Studio 코드 조각을 프로젝트에 코드 삽입을 사용 하 여*</span><span class="sxs-lookup"><span data-stu-id="37afd-278">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="37afd-279">***키보드 (C#만)를 사용 하 여 코드 조각을 추가 하려면***</span><span class="sxs-lookup"><span data-stu-id="37afd-279">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="37afd-280">코드를 삽입 하려는 위치에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-280">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="37afd-281">공백 또는 하이픈만) (없이 코드 조각 이름을 입력 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-281">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="37afd-282">IntelliSense 표시 조각 이름과 일치 하는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-282">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="37afd-283">올바른 코드 조각 선택 (또는 전체 코드 조각이 이름이 선택 될 때까지 입력 유지).</span><span class="sxs-lookup"><span data-stu-id="37afd-283">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="37afd-284">커서 위치에 코드 조각을 삽입 하려면 두 번 탭 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-284">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="37afd-285">![코드 조각 이름을 입력 하기 시작](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image28.png "조각 이름을 입력 하기 시작")</span><span class="sxs-lookup"><span data-stu-id="37afd-285">![Start typing the snippet name](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image28.png "Start typing the snippet name")</span></span>

<span data-ttu-id="37afd-286">*코드 조각 이름을 입력 하기 시작*</span><span class="sxs-lookup"><span data-stu-id="37afd-286">*Start typing the snippet name*</span></span>

<span data-ttu-id="37afd-287">![Tab 키를 눌러 강조 표시 된 코드 조각 선택](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image29.png "Tab 키를 눌러 강조 표시 된 코드 조각 선택")</span><span class="sxs-lookup"><span data-stu-id="37afd-287">![Press Tab to select the highlighted snippet](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image29.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="37afd-288">*Tab 키를 눌러 강조 표시 된 코드 조각 선택*</span><span class="sxs-lookup"><span data-stu-id="37afd-288">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="37afd-289">![확장 하 고 Tab 키를 눌러 다시 코드 조각](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image30.png "확장 하 고 Tab 키를 눌러 다시 코드 조각")</span><span class="sxs-lookup"><span data-stu-id="37afd-289">![Press Tab again and the snippet will expand](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image30.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="37afd-290">*확장 하 고 Tab 키를 눌러 다시 코드 조각*</span><span class="sxs-lookup"><span data-stu-id="37afd-290">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="37afd-291">***마우스 (C#, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면*** 1입니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-291">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="37afd-292">코드 조각을 삽입 하려면 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-292">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="37afd-293">선택 **조각 삽입** 이어서 **내 코드 조각**합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-293">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="37afd-294">클릭 하 여 목록에서 관련 조각을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="37afd-294">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="37afd-295">![코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image31.png "코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추 클릭")</span><span class="sxs-lookup"><span data-stu-id="37afd-295">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image31.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="37afd-296">*코드 조각을 삽입 하 고 코드 조각 삽입 선택 하려는 마우스 오른쪽 단추로 클릭*</span><span class="sxs-lookup"><span data-stu-id="37afd-296">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="37afd-297">![클릭 하 여 목록에서 관련 조각을 선택](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image32.png "클릭 하 여 목록에서 관련 조각을 선택")</span><span class="sxs-lookup"><span data-stu-id="37afd-297">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image32.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="37afd-298">*클릭 하 여 목록에서 관련 조각을 선택합니다*</span><span class="sxs-lookup"><span data-stu-id="37afd-298">*Pick the relevant snippet from the list, by clicking on it*</span></span>
