---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
title: 데이터베이스 데이터 (VB)의 테이블 표시 | Microsoft Docs
author: microsoft
description: 이 자습서에서는 I에 데이터베이스 레코드의 집합을 표시 하는 두 가지 방법을 보여 줍니다. 두 가지 방법으로 서식을 html에서 데이터베이스 레코드 집합이 ta 표시...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/07/2008
ms.topic: article
ms.assetid: 5bb4587f-5bcd-44f5-b368-3c1709162b35
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
msc.type: authoredcontent
ms.openlocfilehash: dd871520f98aaae2d7b33d83b1646eb9eee88821
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="displaying-a-table-of-database-data-vb"></a><span data-ttu-id="bacb3-104">데이터베이스 데이터 (VB)의 테이블 표시</span><span class="sxs-lookup"><span data-stu-id="bacb3-104">Displaying a Table of Database Data (VB)</span></span>
====================
<span data-ttu-id="bacb3-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="bacb3-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="bacb3-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="bacb3-106">Download PDF</span></span>](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_VB.pdf)

> <span data-ttu-id="bacb3-107">이 자습서에서는 I에 데이터베이스 레코드의 집합을 표시 하는 두 가지 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-107">In this tutorial, I demonstrate two methods of displaying a set of database records.</span></span> <span data-ttu-id="bacb3-108">HTML 테이블에 데이터베이스 레코드 집합이 서식 지정 하는 두 가지 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-108">I show two methods of formatting a set of database records in an HTML table.</span></span> <span data-ttu-id="bacb3-109">첫째, 보기 내에서 직접 데이터베이스 레코드 서식을 지정할 수는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-109">First, I show how you can format the database records directly within a view.</span></span> <span data-ttu-id="bacb3-110">다음으로, 있습니다 사용할 수 있는 방법을 부분의 데이터베이스 레코드의 서식을 지정할 때 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-110">Next, I demonstrate how you can take advantage of partials when formatting database records.</span></span>


<span data-ttu-id="bacb3-111">이 자습서의 목표는 ASP.NET MVC 응용 프로그램에서 데이터베이스 데이터의 HTML 테이블을 표시 하는 방법을 설명 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-111">The goal of this tutorial is to explain how you can display an HTML table of database data in an ASP.NET MVC application.</span></span> <span data-ttu-id="bacb3-112">첫째, 레코드 집합을 자동으로 표시 하는 보기를 생성 하려면 Visual Studio에 포함 된 스 캐 폴딩 도구를 사용 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-112">First, you learn how to use the scaffolding tools included in Visual Studio to generate a view that displays a set of records automatically.</span></span> <span data-ttu-id="bacb3-113">다음으로, 데이터베이스 레코드의 서식을 지정할 때 부분을 템플릿으로 사용 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-113">Next, you learn how to use a partial as a template when formatting database records.</span></span>

## <a name="create-the-model-classes"></a><span data-ttu-id="bacb3-114">모델 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="bacb3-114">Create the Model Classes</span></span>

<span data-ttu-id="bacb3-115">영화 데이터베이스 테이블에서 레코드 집합을 표시 하려면 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-115">We are going to display the set of records from the Movies database table.</span></span> <span data-ttu-id="bacb3-116">영화 데이터베이스 테이블에는 다음과 같은 열을 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-116">The Movies database table contains the following columns:</span></span>

<a id="0.4_table01"></a>


| <span data-ttu-id="bacb3-117">**열 이름**</span><span class="sxs-lookup"><span data-stu-id="bacb3-117">**Column Name**</span></span> | <span data-ttu-id="bacb3-118">**데이터 형식**</span><span class="sxs-lookup"><span data-stu-id="bacb3-118">**Data Type**</span></span> | <span data-ttu-id="bacb3-119">**Null 허용**</span><span class="sxs-lookup"><span data-stu-id="bacb3-119">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bacb3-120">ID</span><span class="sxs-lookup"><span data-stu-id="bacb3-120">Id</span></span> | <span data-ttu-id="bacb3-121">Int</span><span class="sxs-lookup"><span data-stu-id="bacb3-121">Int</span></span> | <span data-ttu-id="bacb3-122">False</span><span class="sxs-lookup"><span data-stu-id="bacb3-122">False</span></span> |
| <span data-ttu-id="bacb3-123">제목</span><span class="sxs-lookup"><span data-stu-id="bacb3-123">Title</span></span> | <span data-ttu-id="bacb3-124">Nvarchar(200)</span><span class="sxs-lookup"><span data-stu-id="bacb3-124">Nvarchar(200)</span></span> | <span data-ttu-id="bacb3-125">False</span><span class="sxs-lookup"><span data-stu-id="bacb3-125">False</span></span> |
| <span data-ttu-id="bacb3-126">감독</span><span class="sxs-lookup"><span data-stu-id="bacb3-126">Director</span></span> | <span data-ttu-id="bacb3-127">NVarchar(50)</span><span class="sxs-lookup"><span data-stu-id="bacb3-127">NVarchar(50)</span></span> | <span data-ttu-id="bacb3-128">False</span><span class="sxs-lookup"><span data-stu-id="bacb3-128">False</span></span> |
| <span data-ttu-id="bacb3-129">DateReleased</span><span class="sxs-lookup"><span data-stu-id="bacb3-129">DateReleased</span></span> | <span data-ttu-id="bacb3-130">DateTime</span><span class="sxs-lookup"><span data-stu-id="bacb3-130">DateTime</span></span> | <span data-ttu-id="bacb3-131">False</span><span class="sxs-lookup"><span data-stu-id="bacb3-131">False</span></span> |


<span data-ttu-id="bacb3-132">ASP.NET MVC 응용 프로그램의 영화 테이블을 나타내기 위해 모델 클래스를 만드는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-132">In order to represent the Movies table in our ASP.NET MVC application, we need to create a model class.</span></span> <span data-ttu-id="bacb3-133">이 자습서에서는 사용 하 여 Microsoft Entity Framework 모델 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-133">In this tutorial, we use the Microsoft Entity Framework to create our model classes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="bacb3-134">이 자습서에서는 Microsoft Entity Framework를 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-134">In this tutorial, we use the Microsoft Entity Framework.</span></span> <span data-ttu-id="bacb3-135">그러나 되기 LINQ to SQL, NHibernate 또는 ADO.NET을 포함 하 여 ASP.NET MVC 응용 프로그램에서 데이터베이스와 상호 작용할 수의 여러 다른 기술 사용할 수 있는 것을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-135">However, it is important to understand that you can use a variety of different technologies to interact with a database from an ASP.NET MVC application including LINQ to SQL, NHibernate, or ADO.NET.</span></span>


<span data-ttu-id="bacb3-136">엔터티 데이터 모델 마법사를 시작 하려면 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-136">Follow these steps to launch the Entity Data Model Wizard:</span></span>

1. <span data-ttu-id="bacb3-137">솔루션 탐색기 창 및 메뉴 옵션 선택 모델 폴더를 마우스 오른쪽 단추로 클릭 **추가, 새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-137">Right-click the Models folder in the Solution Explorer window and the select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="bacb3-138">선택 된 **데이터** 범주를 선택은 **ADO.NET 엔터티 데이터 모델** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="bacb3-138">Select the **Data** category and select the **ADO.NET Entity Data Model** template.</span></span>
3. <span data-ttu-id="bacb3-139">데이터 모델 이름을 *MoviesDBModel.edmx* 클릭는 **추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-139">Give your data model the name *MoviesDBModel.edmx* and click the **Add** button.</span></span>

<span data-ttu-id="bacb3-140">추가 단추를 클릭 한 후에 엔터티 데이터 모델 마법사 나타납니다 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="bacb3-140">After you click the Add button, the Entity Data Model Wizard appears (see Figure 1).</span></span> <span data-ttu-id="bacb3-141">마법사를 완료 하려면 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-141">Follow these steps to complete the wizard:</span></span>

1. <span data-ttu-id="bacb3-142">에 **모델 콘텐츠 선택** 선택 단계는 **데이터베이스에서 생성** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-142">In the **Choose Model Contents** step, select the **Generate from database** option.</span></span>
2. <span data-ttu-id="bacb3-143">에 **데이터 연결 선택** 단계를 사용 하 여는 *MoviesDB.mdf* 데이터 연결 및 이름 *MoviesDBEntities* 연결 설정에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-143">In the **Choose Your Data Connection** step, use the *MoviesDB.mdf* data connection and the name *MoviesDBEntities* for the connection settings.</span></span> <span data-ttu-id="bacb3-144">클릭는 **다음** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-144">Click the **Next** button.</span></span>
3. <span data-ttu-id="bacb3-145">에 **데이터베이스 개체 선택** 단계, 테이블 노드를 확장 하 고, 영화 테이블을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-145">In the **Choose Your Database Objects** step, expand the Tables node, select the Movies table.</span></span> <span data-ttu-id="bacb3-146">네임 스페이스를 입력 *모델* 클릭는 **마침** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-146">Enter the namespace *Models* and click the **Finish** button.</span></span>


<span data-ttu-id="bacb3-147">[![LINQ to SQL 클래스 만들기](displaying-a-table-of-database-data-vb/_static/image1.jpg)](displaying-a-table-of-database-data-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="bacb3-147">[![Creating LINQ to SQL classes](displaying-a-table-of-database-data-vb/_static/image1.jpg)](displaying-a-table-of-database-data-vb/_static/image1.png)</span></span>

<span data-ttu-id="bacb3-148">**그림 01**: LINQ to SQL 클래스 만들기 ([전체 크기 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="bacb3-148">**Figure 01**: Creating LINQ to SQL classes ([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image2.png))</span></span>


<span data-ttu-id="bacb3-149">엔터티 데이터 모델 마법사를 완료 한 후 엔터티 데이터 모델 디자이너가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-149">After you complete the Entity Data Model Wizard, the Entity Data Model Designer opens.</span></span> <span data-ttu-id="bacb3-150">디자이너에는 영화 엔터티 표시 됩니다 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="bacb3-150">The Designer should display the Movies entity (see Figure 2).</span></span>


<span data-ttu-id="bacb3-151">[![엔터티 데이터 모델 디자이너](displaying-a-table-of-database-data-vb/_static/image2.jpg)](displaying-a-table-of-database-data-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="bacb3-151">[![The Entity Data Model Designer](displaying-a-table-of-database-data-vb/_static/image2.jpg)](displaying-a-table-of-database-data-vb/_static/image3.png)</span></span>

<span data-ttu-id="bacb3-152">**그림 02**: The 엔터티 데이터 모델 디자이너 ([전체 크기 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="bacb3-152">**Figure 02**: The Entity Data Model Designer ([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image4.png))</span></span>


<span data-ttu-id="bacb3-153">계속 하기 전에 하나의 변경 내용을 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-153">We need to make one change before we continue.</span></span> <span data-ttu-id="bacb3-154">라는 모델 클래스를 생성 하는 엔터티 데이터 마법사 *동영상* 영화 데이터베이스 테이블을 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-154">The Entity Data Wizard generates a model class named *Movies* that represents the Movies database table.</span></span> <span data-ttu-id="bacb3-155">영화 클래스 사용 하 여 특정 영화를 나타내는 합니다, 하므로 되려면 클래스의 이름을 수정 해야 *영화* 대신 *영화* (단 수 아님 복수).</span><span class="sxs-lookup"><span data-stu-id="bacb3-155">Because we'll use the Movies class to represent a particular movie, we need to modify the name of the class to be *Movie* instead of *Movies* (singular rather than plural).</span></span>

<span data-ttu-id="bacb3-156">디자이너 화면의 클래스 이름을 두 번 클릭 하 고 동영상에서 영화 클래스의 이름을 변경 하십시오.</span><span class="sxs-lookup"><span data-stu-id="bacb3-156">Double-click the name of the class on the designer surface and change the name of the class from Movies to Movie.</span></span> <span data-ttu-id="bacb3-157">이 변경 후 클릭는 **저장** 단추 (플로피 디스크 아이콘)를 영화 클래스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-157">After making this change, click the **Save** button (the icon of the floppy disk) to generate the Movie class.</span></span>

## <a name="create-the-movies-controller"></a><span data-ttu-id="bacb3-158">영화 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="bacb3-158">Create the Movies Controller</span></span>

<span data-ttu-id="bacb3-159">데이터베이스 레코드를 표시 하는 방법을 설정 했으므로 동영상의 컬렉션을 반환 하는 컨트롤러를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-159">Now that we have a way to represent our database records, we can create a controller that returns the collection of movies.</span></span> <span data-ttu-id="bacb3-160">Visual Studio 솔루션 탐색기 창 내에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **추가, 컨트롤러** (그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="bacb3-160">Within the Visual Studio Solution Explorer window, right-click the Controllers folder and select the menu option **Add, Controller** (see Figure 3).</span></span>


<span data-ttu-id="bacb3-161">[![메뉴 컨트롤러 추가](displaying-a-table-of-database-data-vb/_static/image3.jpg)](displaying-a-table-of-database-data-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="bacb3-161">[![The Add Controller Menu](displaying-a-table-of-database-data-vb/_static/image3.jpg)](displaying-a-table-of-database-data-vb/_static/image5.png)</span></span>

<span data-ttu-id="bacb3-162">**그림 03**: 컨트롤러 메뉴 추가 ([전체 크기 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="bacb3-162">**Figure 03**: The Add Controller Menu ([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image6.png))</span></span>


<span data-ttu-id="bacb3-163">경우는 **컨트롤러 추가** MovieController 컨트롤러 이름을 입력 대화 상자가 나타나면 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="bacb3-163">When the **Add Controller** dialog appears, enter the controller name MovieController (see Figure 4).</span></span> <span data-ttu-id="bacb3-164">클릭는 **추가** 단추를 새 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-164">Click the **Add** button to add the new controller.</span></span>


<span data-ttu-id="bacb3-165">[![컨트롤러 추가 대화 상자](displaying-a-table-of-database-data-vb/_static/image4.jpg)](displaying-a-table-of-database-data-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="bacb3-165">[![The Add Controller dialog](displaying-a-table-of-database-data-vb/_static/image4.jpg)](displaying-a-table-of-database-data-vb/_static/image7.png)</span></span>

<span data-ttu-id="bacb3-166">**그림 04**: 컨트롤러 추가 대화 상자 ([전체 크기 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="bacb3-166">**Figure 04**: The Add Controller dialog([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image8.png))</span></span>


<span data-ttu-id="bacb3-167">데이터베이스 레코드 집합 반환 되도록 영화 컨트롤러에 의해 노출 되는 index () 동작을 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-167">We need to modify the Index() action exposed by the Movie controller so that it returns the set of database records.</span></span> <span data-ttu-id="bacb3-168">목록 1의 컨트롤러 모양이 되도록 컨트롤러를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-168">Modify the controller so that it looks like the controller in Listing 1.</span></span>

<span data-ttu-id="bacb3-169">**Listing 1 – Controllers\MovieController.vb**</span><span class="sxs-lookup"><span data-stu-id="bacb3-169">**Listing 1 – Controllers\MovieController.vb**</span></span>

[!code-vb[Main](displaying-a-table-of-database-data-vb/samples/sample1.vb)]

<span data-ttu-id="bacb3-170">목록 1의 MoviesDBEntities 클래스 MoviesDB 데이터베이스를 나타내는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-170">In Listing 1, the MoviesDBEntities class is used to represent the MoviesDB database.</span></span> <span data-ttu-id="bacb3-171">식 *엔터티. MovieSet.ToList()* 영화 데이터베이스 테이블에서 모든 동영상의 집합을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-171">The expression *entities.MovieSet.ToList()* returns the set of all movies from the Movies database table.</span></span>

## <a name="create-the-view"></a><span data-ttu-id="bacb3-172">보기 만들기</span><span class="sxs-lookup"><span data-stu-id="bacb3-172">Create the View</span></span>

<span data-ttu-id="bacb3-173">HTML 테이블에 데이터베이스 레코드 집합을 표시 하는 가장 쉬운 방법은 Visual Studio에서 제공 하는 스 캐 폴딩 활용 하기 위해 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-173">The easiest way to display a set of database records in an HTML table is to take advantage of the scaffolding provided by Visual Studio.</span></span>

<span data-ttu-id="bacb3-174">메뉴 옵션을 선택 하 여 응용 프로그램을 빌드하도록 **빌드, 솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-174">Build your application by selecting the menu option **Build, Build Solution**.</span></span> <span data-ttu-id="bacb3-175">열기 전에 응용 프로그램을 작성 해야는 **뷰 추가** 대화 상자 또는 데이터 클래스 대화 상자에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-175">You must build your application before opening the **Add View** dialog or your data classes won't appear in the dialog.</span></span>

<span data-ttu-id="bacb3-176">Index () 작업을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **뷰 추가** (그림 5 참조).</span><span class="sxs-lookup"><span data-stu-id="bacb3-176">Right-click the Index() action and select the menu option **Add View** (see Figure 5).</span></span>


<span data-ttu-id="bacb3-177">[![뷰 추가](displaying-a-table-of-database-data-vb/_static/image5.jpg)](displaying-a-table-of-database-data-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="bacb3-177">[![Adding a view](displaying-a-table-of-database-data-vb/_static/image5.jpg)](displaying-a-table-of-database-data-vb/_static/image9.png)</span></span>

<span data-ttu-id="bacb3-178">**그림 05**: 뷰 추가 ([전체 크기 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="bacb3-178">**Figure 05**: Adding a view ([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image10.png))</span></span>


<span data-ttu-id="bacb3-179">에 **뷰 추가** 대화 상자에서 확인란 확인 **강력한 형식의 뷰 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-179">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="bacb3-180">로 영화 클래스를 선택 하는 **데이터 클래스 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-180">Select the Movie class as the **view data class**.</span></span> <span data-ttu-id="bacb3-181">선택 *목록* 로 **콘텐츠를 볼** (그림 6 참조).</span><span class="sxs-lookup"><span data-stu-id="bacb3-181">Select *List* as the **view content** (see Figure 6).</span></span> <span data-ttu-id="bacb3-182">이러한 옵션을 선택 하는 동영상 목록을 표시 하는 강력한 형식의 뷰를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-182">Selecting these options will generate a strongly-typed view that displays a list of movies.</span></span>


<span data-ttu-id="bacb3-183">[![뷰 추가 대화 상자](displaying-a-table-of-database-data-vb/_static/image6.jpg)](displaying-a-table-of-database-data-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="bacb3-183">[![The Add View dialog](displaying-a-table-of-database-data-vb/_static/image6.jpg)](displaying-a-table-of-database-data-vb/_static/image11.png)</span></span>

<span data-ttu-id="bacb3-184">**그림 06**: 뷰 추가 대화 상자 ([전체 크기 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="bacb3-184">**Figure 06**: The Add View dialog([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image12.png))</span></span>


<span data-ttu-id="bacb3-185">클릭 한 후의 **추가** 단추, 목록 2에서 보기를 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-185">After you click the **Add** button, the view in Listing 2 is generated automatically.</span></span> <span data-ttu-id="bacb3-186">이 보기는 동영상 컬렉션을 반복 하 고 각 동영상의 속성을 표시 하는 데 필요한 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-186">This view contains the code required to iterate through the collection of movies and display each of the properties of a movie.</span></span>

<span data-ttu-id="bacb3-187">**Listing 2 – Views\Movie\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="bacb3-187">**Listing 2 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample2.aspx)]

<span data-ttu-id="bacb3-188">메뉴 옵션을 선택 하 여 응용 프로그램을 실행할 수 있습니다 **디버그, 디버깅 시작** (또는 F5 키 누르기).</span><span class="sxs-lookup"><span data-stu-id="bacb3-188">You can run the application by selecting the menu option **Debug, Start Debugging** (or hitting the F5 key).</span></span> <span data-ttu-id="bacb3-189">Internet Explorer를 시작 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-189">Running the application launches Internet Explorer.</span></span> <span data-ttu-id="bacb3-190">그런 다음 /Movie URL로 이동 그림 7에 있는 페이지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-190">If you navigate to the /Movie URL then you'll see the page in Figure 7.</span></span>


<span data-ttu-id="bacb3-191">[![영화 테이블](displaying-a-table-of-database-data-vb/_static/image7.jpg)](displaying-a-table-of-database-data-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="bacb3-191">[![A table of movies](displaying-a-table-of-database-data-vb/_static/image7.jpg)](displaying-a-table-of-database-data-vb/_static/image13.png)</span></span>

<span data-ttu-id="bacb3-192">**그림 07**: 영화 테이블 ([전체 크기 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="bacb3-192">**Figure 07**: A table of movies([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image14.png))</span></span>


<span data-ttu-id="bacb3-193">그림 7에 데이터베이스 레코드의 눈금의 모양에 대해 마음에 들지 않는 경우 다음 수정할 수 인덱스 뷰.</span><span class="sxs-lookup"><span data-stu-id="bacb3-193">If you don't like anything about the appearance of the grid of database records in Figure 7 then you can simply modify the Index view.</span></span> <span data-ttu-id="bacb3-194">예를 들어, 변경할 수는 *DateReleased* 헤더를 *릴리스 날짜* 인덱스 뷰를 수정 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-194">For example, you can change the *DateReleased* header to *Date Released* by modifying the Index view.</span></span>

## <a name="create-a-template-with-a-partial"></a><span data-ttu-id="bacb3-195">Partial 서식 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="bacb3-195">Create a Template with a Partial</span></span>

<span data-ttu-id="bacb3-196">뷰 너무 복잡해 경우 시작 부분으로 보기를 분리 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-196">When a view gets too complicated, it is a good idea to start breaking the view into partials.</span></span> <span data-ttu-id="bacb3-197">사용 하 여 부분 쉽게 보기 이해 하 고 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-197">Using partials makes your views easier to understand and maintain.</span></span> <span data-ttu-id="bacb3-198">Partial를 만들 것 각 영화 데이터베이스 레코드의 서식을 지정 하려면는 템플릿으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-198">We'll create a partial that we can use as a template to format each of the movie database records.</span></span>

<span data-ttu-id="bacb3-199">부분을 만들려면 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-199">Follow these steps to create the partial:</span></span>

1. <span data-ttu-id="bacb3-200">Views\Movie 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-200">Right-click the Views\Movie folder and select the menu option **Add View**.</span></span>
2. <span data-ttu-id="bacb3-201">확인란 확인 *(.ascx) 부분 뷰를 만들*합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-201">Check the checkbox labeled *Create a partial view (.ascx)*.</span></span>
3. <span data-ttu-id="bacb3-202">Partial 이름을 *MovieTemplate*합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-202">Name the partial *MovieTemplate*.</span></span>
4. <span data-ttu-id="bacb3-203">확인란 확인 **강력한 형식의 뷰 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-203">Check the checkbox labeled **Create a strongly-typed view**.</span></span>
5. <span data-ttu-id="bacb3-204">동영상으로 선택 된 *데이터 클래스를 볼*합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-204">Select Movie as the *view data class*.</span></span>
6. <span data-ttu-id="bacb3-205">비어 있지도 선택 된 *콘텐츠를 볼*합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-205">Select Empty as the *view content*.</span></span>
7. <span data-ttu-id="bacb3-206">클릭는 **추가** partial 프로젝트에 추가 하려면 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-206">Click the **Add** button to add the partial to your project.</span></span>

<span data-ttu-id="bacb3-207">다음이 단계를 완료 한 후 목록 3 모양 MovieTemplate 부분을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-207">After you complete these steps, modify the MovieTemplate partial to look like Listing 3.</span></span>

<span data-ttu-id="bacb3-208">**3 – Views\Movie\MovieTemplate.ascx 나열**</span><span class="sxs-lookup"><span data-stu-id="bacb3-208">**Listing 3 – Views\Movie\MovieTemplate.ascx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample3.aspx)]

<span data-ttu-id="bacb3-209">보기 3의 부분에는 레코드의 단일 행에 대 한 템플릿을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-209">The partial in Listing 3 contains a template for a single row of records.</span></span>

<span data-ttu-id="bacb3-210">수정한 인덱스 뷰 목록 4에 부분 MovieTemplate를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-210">The modified Index view in Listing 4 uses the MovieTemplate partial.</span></span>

<span data-ttu-id="bacb3-211">**Listing 4 – Views\Movie\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="bacb3-211">**Listing 4 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample4.aspx)]

<span data-ttu-id="bacb3-212">목록 4에서 뷰에 For 동영상의 모든 반복 하는 각 루프입니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-212">The view in Listing 4 contains a For Each loop that iterates through all of the movies.</span></span> <span data-ttu-id="bacb3-213">각 동영상에 대 한 부분 MovieTemplate 동영상 서식을 지정 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-213">For each movie, the MovieTemplate partial is used to format the movie.</span></span> <span data-ttu-id="bacb3-214">MovieTemplate RenderPartial() 도우미 메서드를 호출 하 여 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-214">The MovieTemplate is rendered by calling the RenderPartial() helper method.</span></span>

<span data-ttu-id="bacb3-215">수정한 인덱스 뷰는 데이터베이스 레코드의 매우 같은 HTML 테이블을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-215">The modified Index view renders the very same HTML table of database records.</span></span> <span data-ttu-id="bacb3-216">그러나 뷰 크게 간소화 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-216">However, the view has been greatly simplified.</span></span>


<span data-ttu-id="bacb3-217">RenderPartial() 메서드는 문자열을 반환 하지 않으므로 대부분의 다른 도우미 메서드는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-217">The RenderPartial() method is different than most of the other helper methods because it does not return a string.</span></span> <span data-ttu-id="bacb3-218">사용 하 여 RenderPartial() 메서드를 호출 해야 따라서 &lt;% Html.RenderPartial() %&gt; 대신 &lt;% = Html.RenderPartial() %&gt;합니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-218">Therefore, you must call the RenderPartial() method using &lt;% Html.RenderPartial() %&gt; instead of &lt;%= Html.RenderPartial() %&gt;.</span></span>


## <a name="summary"></a><span data-ttu-id="bacb3-219">요약</span><span class="sxs-lookup"><span data-stu-id="bacb3-219">Summary</span></span>

<span data-ttu-id="bacb3-220">이 자습서의 목표 HTML 테이블에 데이터베이스 레코드 집합을 표시 하는 방법에 대해 설명 하는 것 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-220">The goal of this tutorial was to explain how you can display a set of database records in an HTML table.</span></span> <span data-ttu-id="bacb3-221">첫째, Microsoft Entity Framework을 이용 하 여 컨트롤러 작업에서 데이터베이스 레코드 집합을 반환 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-221">First, you learned how to return a set of database records from a controller action by taking advantage of the Microsoft Entity Framework.</span></span> <span data-ttu-id="bacb3-222">다음으로, Visual Studio 스 캐 폴딩을 사용 하 여 항목의 컬렉션을 자동으로 표시 하는 보기를 생성 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-222">Next, you learned how to use Visual Studio scaffolding to generate a view that displays a collection of items automatically.</span></span> <span data-ttu-id="bacb3-223">마지막으로, 부분을 이용 하 여 뷰를 단순화 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-223">Finally, you learned how to simplify the view by taking advantage of a partial.</span></span> <span data-ttu-id="bacb3-224">각 데이터베이스 레코드를 서식을 지정할 수 있도록 템플릿으로 부분을 사용 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="bacb3-224">You learned how to use a partial as a template so that you can format each database record.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="bacb3-225">[이전](creating-model-classes-with-linq-to-sql-vb.md)
> [다음](performing-simple-validation-vb.md)</span><span class="sxs-lookup"><span data-stu-id="bacb3-225">[Previous](creating-model-classes-with-linq-to-sql-vb.md)
[Next](performing-simple-validation-vb.md)</span></span>
