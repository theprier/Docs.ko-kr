---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-vb
title: Entity Framework (VB)를 사용 하 여 모델 클래스 만들기 | Microsoft Docs
author: microsoft
description: 이 자습서에서는 Microsoft Entity Framework와 함께 ASP.NET MVC를 사용 하는 방법에 설명 합니다. ADO.NET 엔터티 Da 만들기 엔터티 마법사를 사용 하는 방법을 알아봅니다 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2009
ms.topic: article
ms.assetid: ff8322c9-12f3-4e24-aba6-a38046b9bb0d
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-vb
msc.type: authoredcontent
ms.openlocfilehash: 3442435c7b2b9ce2ce6bd016ba74fe671eb76f62
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30874449"
---
<a name="creating-model-classes-with-the-entity-framework-vb"></a><span data-ttu-id="407e4-104">Entity Framework (VB)를 사용 하 여 모델 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="407e4-104">Creating Model Classes with the Entity Framework (VB)</span></span>
====================
<span data-ttu-id="407e4-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="407e4-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="407e4-106">이 자습서에서는 Microsoft Entity Framework와 함께 ASP.NET MVC를 사용 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-106">In this tutorial, you learn how to use ASP.NET MVC with the Microsoft Entity Framework.</span></span> <span data-ttu-id="407e4-107">ADO.NET 엔터티 데이터 모델을 만들려는 엔터티 마법사를 사용 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-107">You learn how to use the Entity Wizard to create an ADO.NET Entity Data Model.</span></span> <span data-ttu-id="407e4-108">이 자습서의 과정 동안 선택, 삽입, 업데이트 및 Entity Framework를 사용 하 여 데이터베이스 데이터를 삭제 하는 방법을 설명 하는 웹 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-108">Over the course of this tutorial, we build a web application that illustrates how to select, insert, update, and delete database data by using the Entity Framework.</span></span>


<span data-ttu-id="407e4-109">이 자습서의 목표는 ASP.NET MVC 응용 프로그램을 빌드할 때 Microsoft Entity Framework를 사용 하 여 데이터 액세스 클래스를 만드는 방법을 설명 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-109">The goal of this tutorial is to explain how you can create data access classes using the Microsoft Entity Framework when building an ASP.NET MVC application.</span></span> <span data-ttu-id="407e4-110">이 자습서에서는 Microsoft Entity Framework의 이전 알지를 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-110">This tutorial assumes no previous knowledge of the Microsoft Entity Framework.</span></span> <span data-ttu-id="407e4-111">이 자습서를 마치면 하 여 선택, 삽입, 업데이트, Entity Framework를 사용 하 여 데이터베이스 레코드를 삭제 하는 방법을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-111">By the end of this tutorial, you'll understand how to use the Entity Framework to select, insert, update, and delete database records.</span></span>

<span data-ttu-id="407e4-112">Microsoft Entity Framework는 데이터베이스에서 데이터 액세스 계층을 자동으로 생성할 수 있도록 하는 개체 관계형 매핑 (O/RM) 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-112">The Microsoft Entity Framework is an Object Relational Mapping (O/RM) tool that enables you to generate a data access layer from a database automatically.</span></span> <span data-ttu-id="407e4-113">Entity Framework를 사용 하면 데이터 액세스 클래스를 직접 작성 지루한 작업을 피할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-113">The Entity Framework enables you to avoid the tedious work of building your data access classes by hand.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="407e4-114">ASP.NET MVC와 Microsoft Entity Framework 사이의 필수 연결이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-114">There is no essential connection between ASP.NET MVC and the Microsoft Entity Framework.</span></span> <span data-ttu-id="407e4-115">ASP.NET MVC와 함께 사용할 수 있는 Entity Framework에 대 한 대안 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-115">There are several alternatives to the Entity Framework that you can use with ASP.NET MVC.</span></span> <span data-ttu-id="407e4-116">예를 들어 Microsoft LINQ to SQL, NHibernate 또는 subsonic은 이러한 방식을 등의 다른 O/RM 도구를 사용 하 여 MVC 모델 클래스를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-116">For example, you can build your MVC Model classes using other O/RM tools such as Microsoft LINQ to SQL, NHibernate, or SubSonic.</span></span>


<span data-ttu-id="407e4-117">를 ASP.NET MVC와 함께 Microsoft Entity Framework를 사용 하는 방법을 보여 주기 위해 간단한 샘플 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-117">In order to illustrate how you can use the Microsoft Entity Framework with ASP.NET MVC, we'll build a simple sample application.</span></span> <span data-ttu-id="407e4-118">표시 하 고 동영상 데이터베이스 레코드를 편집할 수 있는 동영상 데이터베이스 응용 프로그램을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-118">We'll create a Movie Database application that enables you to display and edit movie database records.</span></span>

<span data-ttu-id="407e4-119">이 자습서는 Visual Studio 2008 또는 Visual Web Developer 2008 서비스 팩 1 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-119">This tutorial assumes that you have Visual Studio 2008 or Visual Web Developer 2008 with Service Pack 1.</span></span> <span data-ttu-id="407e4-120">Entity Framework를 사용 하려면 서비스 팩 1 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-120">You need Service Pack 1 in order to use the Entity Framework.</span></span> <span data-ttu-id="407e4-121">다음 주소에서 Visual Studio 2008 서비스 팩 1 또는 서비스 팩 1 Visual Web Developer를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-121">You can download Visual Studio 2008 Service Pack 1 or Visual Web Developer with Service Pack 1 from the following address:</span></span>

> [https://www.asp.net/downloads/](https://www.asp.net/downloads)


## <a name="creating-the-movie-sample-database"></a><span data-ttu-id="407e4-122">영화 샘플 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="407e4-122">Creating the Movie Sample Database</span></span>

<span data-ttu-id="407e4-123">다음 열이 포함 된 동영상 라는 데이터베이스 테이블을 사용 하는 영화 데이터베이스 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="407e4-123">The Movie Database application uses a database table named Movies that contains the following columns:</span></span>

| <span data-ttu-id="407e4-124">열 이름</span><span class="sxs-lookup"><span data-stu-id="407e4-124">Column Name</span></span> | <span data-ttu-id="407e4-125">데이터 형식</span><span class="sxs-lookup"><span data-stu-id="407e4-125">Data Type</span></span> | <span data-ttu-id="407e4-126">Null 허용 하 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="407e4-126">Allow Nulls?</span></span> | <span data-ttu-id="407e4-127">기본 키가?</span><span class="sxs-lookup"><span data-stu-id="407e4-127">Is Primary Key?</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="407e4-128">ID</span><span class="sxs-lookup"><span data-stu-id="407e4-128">Id</span></span> | <span data-ttu-id="407e4-129">int</span><span class="sxs-lookup"><span data-stu-id="407e4-129">int</span></span> | <span data-ttu-id="407e4-130">False</span><span class="sxs-lookup"><span data-stu-id="407e4-130">False</span></span> | <span data-ttu-id="407e4-131">True</span><span class="sxs-lookup"><span data-stu-id="407e4-131">True</span></span> |
| <span data-ttu-id="407e4-132">제목</span><span class="sxs-lookup"><span data-stu-id="407e4-132">Title</span></span> | <span data-ttu-id="407e4-133">nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="407e4-133">nvarchar(100)</span></span> | <span data-ttu-id="407e4-134">False</span><span class="sxs-lookup"><span data-stu-id="407e4-134">False</span></span> | <span data-ttu-id="407e4-135">False</span><span class="sxs-lookup"><span data-stu-id="407e4-135">False</span></span> |
| <span data-ttu-id="407e4-136">감독</span><span class="sxs-lookup"><span data-stu-id="407e4-136">Director</span></span> | <span data-ttu-id="407e4-137">nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="407e4-137">nvarchar(100)</span></span> | <span data-ttu-id="407e4-138">False</span><span class="sxs-lookup"><span data-stu-id="407e4-138">False</span></span> | <span data-ttu-id="407e4-139">False</span><span class="sxs-lookup"><span data-stu-id="407e4-139">False</span></span> |

<span data-ttu-id="407e4-140">다음이 단계를 수행 하 여 ASP.NET MVC 프로젝트에이 테이블을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-140">You can add this table to an ASP.NET MVC project by following these steps:</span></span>

1. <span data-ttu-id="407e4-141">응용 프로그램을 마우스 오른쪽 단추로 클릭\_메뉴 옵션을 선택 하는 솔루션 탐색기 창에서 데이터 폴더 **추가, 새 항목입니다.**</span><span class="sxs-lookup"><span data-stu-id="407e4-141">Right-click the App\_Data folder in the Solution Explorer window and select the menu option **Add, New Item.**</span></span>
2. <span data-ttu-id="407e4-142">**새 항목 추가** 대화 상자에서 **SQL Server 데이터베이스**, 이름을 MoviesDB.mdf, 데이터베이스를 지정 하 고 클릭는 **추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-142">From the **Add New Item** dialog box, select **SQL Server Database**, give the database the name MoviesDB.mdf, and click the **Add** button.</span></span>
3. <span data-ttu-id="407e4-143">서버 탐색기/데이터베이스 탐색기 창을 열려면 MoviesDB.mdf 파일을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-143">Double-click the MoviesDB.mdf file to open the Server Explorer/Database Explorer window.</span></span>
4. <span data-ttu-id="407e4-144">MoviesDB.mdf 데이터베이스 연결 확장 테이블 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **새 테이블 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-144">Expand the MoviesDB.mdf database connection, right-click the Tables folder, and select the menu option **Add New Table**.</span></span>
5. <span data-ttu-id="407e4-145">테이블 디자이너에서 Id, 제목 및 감독 열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-145">In the Table Designer, add the Id, Title, and Director columns.</span></span>
6. <span data-ttu-id="407e4-146">클릭는 **저장** 단추 (플로피의 아이콘에 포함)는 이름 동영상 새 테이블을 저장 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-146">Click the **Save** button (it has the icon of the floppy) to save the new table with the name Movies.</span></span>

<span data-ttu-id="407e4-147">영화 데이터베이스 테이블을 만든 후에 테이블에 몇 가지 샘플 데이터를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-147">After you create the Movies database table, you should add some sample data to the table.</span></span> <span data-ttu-id="407e4-148">영화 테이블을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **테이블 데이터 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-148">Right-click the Movies table and select the menu option **Show Table Data**.</span></span> <span data-ttu-id="407e4-149">표시 되는 표 형태에 가짜 동영상 데이터를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-149">You can enter fake movie data into the grid that appears.</span></span>

## <a name="creating-the-adonet-entity-data-model"></a><span data-ttu-id="407e4-150">ADO.NET 엔터티 데이터 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="407e4-150">Creating the ADO.NET Entity Data Model</span></span>

<span data-ttu-id="407e4-151">Entity Framework를 사용 하려면 엔터티 데이터 모델을 만드는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-151">In order to use the Entity Framework, you need to create an Entity Data Model.</span></span> <span data-ttu-id="407e4-152">Visual Studio의 이용할 수 있습니다 *엔터티 데이터 모델 마법사* 데이터베이스에서 엔터티 데이터 모델을 자동으로 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-152">You can take advantage of the Visual Studio *Entity Data Model Wizard* to generate an Entity Data Model from a database automatically.</span></span>

<span data-ttu-id="407e4-153">아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-153">Follow these steps:</span></span>

1. <span data-ttu-id="407e4-154">솔루션 탐색기 창에 모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션을 선택 **추가, 새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-154">Right-click the Models folder in the Solution Explorer window and select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="407e4-155">에 **새 항목 추가** 대화 상자에서 데이터 범주를 선택 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="407e4-155">In the **Add New Item** dialog, select the Data category (see Figure 1).</span></span>
3. <span data-ttu-id="407e4-156">선택 된 **ADO.NET 엔터티 데이터 모델** 템플릿을 엔터티 데이터 모델 MoviesDBModel.edmx, name을 지정 하 고 클릭는 **추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-156">Select the **ADO.NET Entity Data Model** template, give the Entity Data Model the name MoviesDBModel.edmx, and click the **Add** button.</span></span> <span data-ttu-id="407e4-157">클릭 하 고 **추가** 단추는 데이터 모델 마법사를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-157">Clicking the **Add** button launches the Data Model Wizard.</span></span>
4. <span data-ttu-id="407e4-158">에 **모델 콘텐츠 선택** 단계, 선택는 **는 데이터베이스에서 생성** 옵션의 **다음** 단추 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="407e4-158">In the **Choose Model Contents** step, choose the **Generate from a database** option and click the **Next** button (see Figure 2).</span></span>
5. <span data-ttu-id="407e4-159">에 **데이터 연결 선택** 단계 MoviesDB.mdf 데이터베이스 연결을 엔터티 연결 설정 MoviesDBEntities, 이름을 지정 하 고 클릭 하 여 입력의 **다음** 단추 (그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="407e4-159">In the **Choose Your Data Connection** step, select the MoviesDB.mdf database connection, enter the entities connection settings name MoviesDBEntities, and click the **Next** button (see Figure 3).</span></span>
6. <span data-ttu-id="407e4-160">에 **데이터베이스 개체 선택** 단계 영화 데이터베이스 테이블을 선택 하 고 클릭는 **마침** 단추 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="407e4-160">In the **Choose Your Database Objects** step, select the Movie database table and click the **Finish** button (see Figure 4).</span></span>

<span data-ttu-id="407e4-161">다음이 단계를 완료 한 후 ADO.NET 엔터티 데이터 모델 디자이너 (Entity Designer)가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-161">After you complete these steps, the ADO.NET Entity Data Model Designer (Entity Designer) opens.</span></span>

<span data-ttu-id="407e4-162">**그림 1-새 엔터티 데이터 모델 만들기**</span><span class="sxs-lookup"><span data-stu-id="407e4-162">**Figure 1 – Creating a new Entity Data Model**</span></span>

![clip_image002](creating-model-classes-with-the-entity-framework-vb/_static/image1.jpg)

<span data-ttu-id="407e4-164">**그림 2 – 모델 내용을 단계를 선택 합니다.**</span><span class="sxs-lookup"><span data-stu-id="407e4-164">**Figure 2 – Choose Model Contents Step**</span></span>

![clip_image004](creating-model-classes-with-the-entity-framework-vb/_static/image2.jpg)

<span data-ttu-id="407e4-166">**그림 3 – 데이터 연결 선택**</span><span class="sxs-lookup"><span data-stu-id="407e4-166">**Figure 3 – Choose Your Data Connection**</span></span>

![clip_image006](creating-model-classes-with-the-entity-framework-vb/_static/image3.jpg)

<span data-ttu-id="407e4-168">**그림 4-데이터베이스 개체 선택**</span><span class="sxs-lookup"><span data-stu-id="407e4-168">**Figure 4 – Choose Your Database Objects**</span></span>

![clip_image008](creating-model-classes-with-the-entity-framework-vb/_static/image4.jpg)

## <a name="modifying-the-adonet-entity-data-model"></a><span data-ttu-id="407e4-170">ADO.NET 엔터티 데이터 모델 수정</span><span class="sxs-lookup"><span data-stu-id="407e4-170">Modifying the ADO.NET Entity Data Model</span></span>

<span data-ttu-id="407e4-171">엔터티 데이터 모델을 만든 후 엔터티 디자이너의 사용 하 여 모델을 수정할 수 있습니다 (그림 5 참조).</span><span class="sxs-lookup"><span data-stu-id="407e4-171">After you create an Entity Data Model, you can modify the model by taking advantage of the Entity Designer (see Figure 5).</span></span> <span data-ttu-id="407e4-172">솔루션 탐색기 창 내에서 모델 폴더에 포함 된 MoviesDBModel.edmx 파일을 두 번 클릭 하 여 언제 든 지 엔터티 디자이너를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-172">You can open the Entity Designer at any time by double-clicking the MoviesDBModel.edmx file contained in the Models folder within the Solution Explorer window.</span></span>

<span data-ttu-id="407e4-173">**그림 5 – ADO.NET 엔터티 데이터 모델 디자이너**</span><span class="sxs-lookup"><span data-stu-id="407e4-173">**Figure 5 – The ADO.NET Entity Data Model Designer**</span></span>

![clip_image010](creating-model-classes-with-the-entity-framework-vb/_static/image5.jpg)

<span data-ttu-id="407e4-175">예를 들어 엔터티 모델 데이터 마법사에서 생성 하는 클래스의 이름을 변경 하는 Entity Designer를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-175">For example, you can use the Entity Designer to change the names of the classes that the Entity Model Data Wizard generates.</span></span> <span data-ttu-id="407e4-176">마법사가 영화 라는 새 데이터 액세스 클래스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-176">The Wizard created a new data access class named Movies.</span></span> <span data-ttu-id="407e4-177">즉, 마법사는 데이터베이스 테이블 이름이 매우 같은 클래스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-177">In other words, the Wizard gave the class the very same name as the database table.</span></span> <span data-ttu-id="407e4-178">이 클래스를 나타내는 특정 영화 인스턴스를 사용 합니다, 때문에 동영상에 대 한 동영상 클래스를 바꾼 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-178">Because we will use this class to represent a particular Movie instance, we should rename the class from Movies to Movie.</span></span>

<span data-ttu-id="407e4-179">엔터티 디자이너에서 클래스 이름을 두 번 클릭 하 고 새 이름을 입력할 수 엔터티 클래스 이름을 변경 하려는 경우 (그림 6 참조).</span><span class="sxs-lookup"><span data-stu-id="407e4-179">If you want to rename an entity class, you can double-click on the class name in the Entity Designer and enter a new name (see Figure 6).</span></span> <span data-ttu-id="407e4-180">또는 엔터티 디자이너의 엔터티를 선택한 후 속성 창에서 엔터티의 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-180">Alternatively, you can change the name of an entity in the Properties window after selecting an entity in the Entity Designer.</span></span>

<span data-ttu-id="407e4-181">**그림 6 – 엔터티 이름 변경**</span><span class="sxs-lookup"><span data-stu-id="407e4-181">**Figure 6 – Changing an entity name**</span></span>

![clip_image012](creating-model-classes-with-the-entity-framework-vb/_static/image6.jpg)

<span data-ttu-id="407e4-183">후 저장 단추 (플로피 디스크 아이콘)를 클릭 하 여 수정 하 여 엔터티 데이터 모델을 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-183">Remember to save your Entity Data Model after making a modification by clicking the Save button (the icon of the floppy disk).</span></span> <span data-ttu-id="407e4-184">내부적으로 엔터티 디자이너의 Visual Basic.NET 클래스 집합을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-184">Behind the scenes, the Entity Designer generates a set of Visual Basic .NET classes.</span></span> <span data-ttu-id="407e4-185">솔루션 탐색기 창에서 MoviesDBModel.Designer.vb 파일을 열어 이러한 클래스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-185">You can view these classes by opening the MoviesDBModel.Designer.vb file from the Solution Explorer window.</span></span>


<span data-ttu-id="407e4-186">다음에 Entity Designer를 사용 하 여 변경 내용을 덮어쓰게 됩니다 이후.designer.vb 파일의 코드를 수정 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="407e4-186">Don't modify the code in the Designer.vb file since your changes will be overwritten the next time you use the Entity Designer.</span></span> <span data-ttu-id="407e4-187">경우.designer.vb 파일에 정의 된 엔터티 클래스의 기능을 확장 하려면 다음 만들 수 있습니다 *partial 클래스* 를 별도 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-187">If you want to extend the functionality of the entity classes defined in the Designer.vb file then you can create *partial classes* in separate files.</span></span>


#### <a name="selecting-database-records-with-the-entity-framework"></a><span data-ttu-id="407e4-188">Entity Framework와 함께 데이터베이스 레코드 선택</span><span class="sxs-lookup"><span data-stu-id="407e4-188">Selecting Database Records with the Entity Framework</span></span>

<span data-ttu-id="407e4-189">영화 레코드의 목록을 표시 하는 페이지를 만들어 영화 데이터베이스 응용 프로그램 작성을 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-189">Let's start building our Movie Database application by creating a page that displays a list of movie records.</span></span> <span data-ttu-id="407e4-190">Home 컨트롤러 목록 1의 index () 라는 동작을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-190">The Home controller in Listing 1 exposes an action named Index().</span></span> <span data-ttu-id="407e4-191">Index () 작업 모두 반환 영화 레코드 영화 데이터베이스 테이블에서 엔터티 프레임 워크를 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-191">The Index() action returns all of the movie records from the Movie database table by taking advantage of the Entity Framework.</span></span>

<span data-ttu-id="407e4-192">**Listing 1 – Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="407e4-192">**Listing 1 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample1.vb)]

<span data-ttu-id="407e4-193">목록 1의 컨트롤러는 생성자를 포함 하는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-193">Notice that the controller in Listing 1 includes a constructor.</span></span> <span data-ttu-id="407e4-194">생성자 이라는 클래스 수준 필드를 초기화 합니다. \_db입니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-194">The constructor initializes a class-level field named \_db.</span></span> <span data-ttu-id="407e4-195">\_db 필드 Microsoft Entity Framework에 의해 생성 된 데이터베이스 엔터티를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-195">The \_db field represents the database entities generated by the Microsoft Entity Framework.</span></span> <span data-ttu-id="407e4-196">\_db 필드는 Entity Designer에서 생성 된 MoviesDBEntities 클래스의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-196">The \_db field is an instance of the MoviesDBEntities class that was generated by the Entity Designer.</span></span>

<span data-ttu-id="407e4-197">\_db 필드는 index () 작업 내에서 영화 데이터베이스 테이블에서 레코드를 검색 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-197">The \_db field is used within the Index() action to retrieve the records from the Movies database table.</span></span> <span data-ttu-id="407e4-198">식 \_db입니다. MovieSet 영화 데이터베이스 테이블에서 모든 레코드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-198">The expression \_db.MovieSet represents all of the records from the Movies database table.</span></span> <span data-ttu-id="407e4-199">영화 집합이 영화 개체의 제네릭 컬렉션으로 변환 하 고 tolist () 메서드를 사용 하는: 목록 (의 동영상).</span><span class="sxs-lookup"><span data-stu-id="407e4-199">The ToList() method is used to convert the set of movies into a generic collection of Movie objects: List( Of Movie).</span></span>

<span data-ttu-id="407e4-200">영화 레코드는 LINQ to Entities 사용 하 여 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-200">The movie records are retrieved with the help of LINQ to Entities.</span></span> <span data-ttu-id="407e4-201">목록 1의 index () 동작 LINQ를 사용 하 여 *메서드 구문을* 데이터베이스 레코드 집합을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-201">The Index() action in Listing 1 uses LINQ *method syntax* to retrieve the set of database records.</span></span> <span data-ttu-id="407e4-202">원하는 경우 LINQ를 사용할 수 있습니다 *쿼리 구문을* 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-202">If you prefer, you can use LINQ *query syntax* instead.</span></span> <span data-ttu-id="407e4-203">다음 두 문이 매우 동일한 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-203">The following two statements do the very same thing:</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample2.vb)]

<span data-ttu-id="407e4-204">가장 편리할 나오든 이들 LINQ 구문을 메서드 구문 또는 쿼리 구문을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-204">Use whichever LINQ syntax – method syntax or query syntax – that you find most intuitive.</span></span> <span data-ttu-id="407e4-205">두 방법 간의 성능에 차이가 – 유일한 차이점은 스타일입니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-205">There is no difference in performance between the two approaches – the only difference is style.</span></span>

<span data-ttu-id="407e4-206">영화 레코드를 표시 하려면 보기 목록 2에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-206">The view in Listing 2 is used to display the movie records.</span></span>

<span data-ttu-id="407e4-207">**Listing 2 – Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="407e4-207">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample3.aspx)]

<span data-ttu-id="407e4-208">보기 목록 2에 포함 한 **각** 각 영화 레코드를 반복 하 고 동영상 레코드의 제목 및 감독 속성의 값을 표시 하는 루프입니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-208">The view in Listing 2 contains a **For Each** loop that iterates through each movie record and displays the values of the movie record's Title and Director properties.</span></span> <span data-ttu-id="407e4-209">편집 및 삭제 링크 각 레코드 옆에 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-209">Notice that an Edit and Delete link is displayed next to each record.</span></span> <span data-ttu-id="407e4-210">동영상 추가 링크 보기의 아래쪽에 표시 되는 또한 (그림 7 참조).</span><span class="sxs-lookup"><span data-stu-id="407e4-210">Furthermore, an Add Movie link appears at the bottom of the view (see Figure 7).</span></span>

<span data-ttu-id="407e4-211">**그림 7-인덱스 뷰**</span><span class="sxs-lookup"><span data-stu-id="407e4-211">**Figure 7 – The Index view**</span></span>

![clip_image014](creating-model-classes-with-the-entity-framework-vb/_static/image7.jpg)

<span data-ttu-id="407e4-213">인덱스 뷰는 한 *보기를 입력 한*합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-213">The Index view is a *typed view*.</span></span> <span data-ttu-id="407e4-214">인덱스 보기에는 &lt;% 페이지 % @&gt; Inherits 특성이 포함 된 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-214">The Index view has a &lt;%@ Page %&gt; directive that includes an Inherits attribute.</span></span> <span data-ttu-id="407e4-215">Inherits 특성 ViewData.Model 속성 강력한 형식의 제네릭 목록 개체의 컬렉션 영화 – 목록 (의 동영상)을 캐스팅합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-215">The Inherits attribute casts the ViewData.Model property to a strongly typed generic List collection of Movie objects – a List(Of Movie).</span></span>

## <a name="inserting-database-records-with-the-entity-framework"></a><span data-ttu-id="407e4-216">Entity Framework와 함께 데이터베이스 레코드를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-216">Inserting Database Records with the Entity Framework</span></span>

<span data-ttu-id="407e4-217">쉽게 데이터베이스 테이블에 새 레코드를 삽입할 수 있도록 Entity Framework를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-217">You can use the Entity Framework to make it easy to insert new records into a database table.</span></span> <span data-ttu-id="407e4-218">코드 3 영화 데이터베이스 테이블에 새 레코드를 삽입 하는 데 사용할 수 있는 홈 컨트롤러 클래스에 추가 하는 두 개의 새 작업이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-218">Listing 3 contains two new actions added to the Home controller class that you can use to insert new records into the Movie database table.</span></span>

<span data-ttu-id="407e4-219">**3 – Controllers\HomeController.vb (추가 메서드)를 나열합니다.**</span><span class="sxs-lookup"><span data-stu-id="407e4-219">**Listing 3 – Controllers\HomeController.vb (Add methods)**</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample4.vb)]

<span data-ttu-id="407e4-220">첫 번째 add () 작업 보기를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-220">The first Add() action simply returns a view.</span></span> <span data-ttu-id="407e4-221">뷰에 새 동영상 데이터베이스 추가 대 한 양식이 있습니다 (그림 8 참조)를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-221">The view contains a form for adding a new movie database record (see Figure 8).</span></span> <span data-ttu-id="407e4-222">폼을 제출 하는 경우 두 번째 add () 동작 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-222">When you submit the form, the second Add() action is invoked.</span></span>

<span data-ttu-id="407e4-223">두 번째 add () 동작 AcceptVerbs 특성으로 데코레이팅되 어 있는지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-223">Notice that the second Add() action is decorated with the AcceptVerbs attribute.</span></span> <span data-ttu-id="407e4-224">HTTP POST 작업을 수행 하는 경우에이 작업을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-224">This action can be invoked only when performing an HTTP POST operation.</span></span> <span data-ttu-id="407e4-225">즉,이 작업은 HTML 폼을 게시할 때만 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-225">In other words, this action can only be invoked when posting an HTML form.</span></span>

<span data-ttu-id="407e4-226">두 번째 add () 동작 ASP.NET MVC TryUpdateModel() 메서드를 사용 하 여 Entity Framework 영화 클래스의 새 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-226">The second Add() action creates a new instance of the Entity Framework Movie class with the help of the ASP.NET MVC TryUpdateModel() method.</span></span> <span data-ttu-id="407e4-227">TryUpdateModel() 메서드 add () 메서드에 전달 된 FormCollection의 필드 하며 영화 클래스에 이러한 HTML 폼 필드의 값을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-227">The TryUpdateModel() method takes the fields in the FormCollection passed to the Add() method and assigns the values of these HTML form fields to the Movie class.</span></span>


<span data-ttu-id="407e4-228">Entity Framework를 사용할 때는 TryUpdateModel 또는 UpdateModel 메서드를 사용 하 여 엔터티 클래스의 속성을 업데이트 하는 경우 "white" 속성의 목록이 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-228">When using the Entity Framework, you must supply a "white list" of properties when using the TryUpdateModel or UpdateModel methods to update the properties of an entity class.</span></span>


<span data-ttu-id="407e4-229">다음으로, add () 작업 몇 가지 간단한 형태 유효성 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-229">Next, the Add() action performs some simple form validation.</span></span> <span data-ttu-id="407e4-230">작업 제목 및 감독 속성에 값을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-230">The action verifies that both the Title and Director properties have values.</span></span> <span data-ttu-id="407e4-231">유효성 검사 오류가 있으면 유효성 검사 오류 메시지는 ModelState에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-231">If there is a validation error, then a validation error message is added to ModelState.</span></span>

<span data-ttu-id="407e4-232">유효성 검사 오류가 없는 경우 새 동영상 레코드는 Entity Framework를 사용 하 여 영화 데이터베이스 테이블에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-232">If there are no validation errors then a new movie record is added to the Movies database table with the help of the Entity Framework.</span></span> <span data-ttu-id="407e4-233">다음 두 줄의 코드를 사용 하 여 데이터베이스에 새 레코드가 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-233">The new record is added to the database with the following two lines of code:</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample5.vb)]

<span data-ttu-id="407e4-234">첫 번째 코드 줄 Entity Framework에 의해 추적 되 고 영화 집합에 새 동영상 엔터티를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-234">The first line of code adds the new Movie entity to the set of movies being tracked by the Entity Framework.</span></span> <span data-ttu-id="407e4-235">기본 데이터베이스에 다시 추적 되 고 동영상에 변경 내용이 적용 된 두 번째 코드 줄에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-235">The second line of code saves whatever changes have been made to the Movies being tracked back to the underlying database.</span></span>

<span data-ttu-id="407e4-236">**그림 8 – 추가 보기**</span><span class="sxs-lookup"><span data-stu-id="407e4-236">**Figure 8 – The Add view**</span></span>

![clip_image016](creating-model-classes-with-the-entity-framework-vb/_static/image8.jpg)

## <a name="updating-database-records-with-the-entity-framework"></a><span data-ttu-id="407e4-238">Entity Framework와 함께 데이터베이스 레코드를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-238">Updating Database Records with the Entity Framework</span></span>

<span data-ttu-id="407e4-239">거의 사용 했던 방금 새 데이터베이스 레코드를 삽입 하는 방법으로 Entity Framework와 함께 데이터베이스 레코드를 편집 하려면 동일한 방법을 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-239">You can follow almost the same approach to edit a database record with the Entity Framework as the approach that we just followed to insert a new database record.</span></span> <span data-ttu-id="407e4-240">목록 4 Edit() 라는 두 개의 새 컨트롤러 작업을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-240">Listing 4 contains two new controller actions named Edit().</span></span> <span data-ttu-id="407e4-241">첫 번째 Edit() 동작이 영화 레코드 편집에 대 한 HTML 폼을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-241">The first Edit() action returns an HTML form for editing a movie record.</span></span> <span data-ttu-id="407e4-242">두 번째 Edit() 동작 데이터베이스를 업데이트 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-242">The second Edit() action attempts to update the database.</span></span>

<span data-ttu-id="407e4-243">**4 – Controllers\HomeController.vb (편집 메서드)를 나열합니다.**</span><span class="sxs-lookup"><span data-stu-id="407e4-243">**Listing 4 – Controllers\HomeController.vb (Edit methods)**</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample6.vb)]

<span data-ttu-id="407e4-244">두 번째 Edit() 동작 편집 중인 동영상의 Id와 일치 하는 데이터베이스에서 영화 레코드를 검색 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-244">The second Edit() action starts by retrieving the Movie record from the database that matches the Id of the movie being edited.</span></span> <span data-ttu-id="407e4-245">다음 LINQ to Entities 문은 특정 Id와 일치 하는 첫 번째 데이터베이스 레코드를 가져와:</span><span class="sxs-lookup"><span data-stu-id="407e4-245">The following LINQ to Entities statement grabs the first database record that matches a particular Id:</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample7.vb)]

<span data-ttu-id="407e4-246">다음으로, TryUpdateModel() 메서드 영화 엔터티 속성에 HTML 양식 필드의 값을 할당할 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-246">Next, the TryUpdateModel() method is used to assign the values of the HTML form fields to the properties of the movie entity.</span></span> <span data-ttu-id="407e4-247">허용 목록을 정확한 업데이트할 속성을 지정 하려면 제공 됨을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-247">Notice that a white list is supplied to specify the exact properties to update.</span></span>

<span data-ttu-id="407e4-248">다음으로 영화 제목 및 감독 속성에 값을 확인 하려면 몇 가지 간단한 유효성 검사가 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-248">Next, some simple validation is performed to verify that both the Movie Title and Director properties have values.</span></span> <span data-ttu-id="407e4-249">두 속성 중 하나는 값이 없으면 유효성 검사 오류 메시지를 ModelState에 추가 되 고 ModelState.IsValid 값 false를 반환 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-249">If either property is missing a value, then a validation error message is added to ModelState and ModelState.IsValid returns the value false.</span></span>

<span data-ttu-id="407e4-250">마지막으로 유효성 검사 오류가 있을 경우 다음 기본 영화 데이터베이스 테이블 업데이트 됩니다 변경으로 savechanges () 메서드를 호출 하 여.</span><span class="sxs-lookup"><span data-stu-id="407e4-250">Finally, if there are no validation errors, then the underlying Movies database table is updated with any changes by calling the SaveChanges() method.</span></span>

<span data-ttu-id="407e4-251">데이터베이스 레코드를 편집할 때 데이터베이스 업데이트를 수행 하는 컨트롤러 동작을 편집 하 고 레코드의 Id를 전달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-251">When editing database records, you need to pass the Id of the record being edited to the controller action that performs the database update.</span></span> <span data-ttu-id="407e4-252">그렇지 않으면 컨트롤러 작업은 기본 데이터베이스에서 업데이트할 레코드 알지 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-252">Otherwise, the controller action will not know which record to update in the underlying database.</span></span> <span data-ttu-id="407e4-253">목록 5에 포함 된 편집 보기, 편집 하 고 데이터베이스 레코드의 Id를 나타내는 숨겨진된 양식 필드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-253">The Edit view, contained in Listing 5, includes a hidden form field that represents the Id of the database record being edited.</span></span>

<span data-ttu-id="407e4-254">**Listing 5 – Views\Home\Edit.aspx**</span><span class="sxs-lookup"><span data-stu-id="407e4-254">**Listing 5 – Views\Home\Edit.aspx**</span></span>

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample8.aspx)]

## <a name="deleting-database-records-with-the-entity-framework"></a><span data-ttu-id="407e4-255">Entity Framework와 함께 데이터베이스 레코드를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-255">Deleting Database Records with the Entity Framework</span></span>

<span data-ttu-id="407e4-256">이므로이 자습서에서 해결할 필요가 최종 데이터베이스 작업은 데이터베이스 레코드를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-256">The final database operation, which we need to tackle in this tutorial, is deleting database records.</span></span> <span data-ttu-id="407e4-257">특정 데이터베이스 레코드를 삭제할 컨트롤러 동작 목록 6에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-257">You can use the controller action in Listing 6 to delete a particular database record.</span></span>

<span data-ttu-id="407e4-258">**6-나열 \Controllers\HomeController.vb (삭제 작업)**</span><span class="sxs-lookup"><span data-stu-id="407e4-258">**Listing 6 -- \Controllers\HomeController.vb (Delete action)**</span></span>

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample9.vb)]

<span data-ttu-id="407e4-259">먼저 delete () 동작 Id와 일치 하는 엔터티 작업에 전달 된 영화를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-259">The Delete() action first retrieves the Movie entity that matches the Id passed to the action.</span></span> <span data-ttu-id="407e4-260">다음으로 영화 뒤에 savechanges () 메서드에 의해 DeleteObject() 메서드를 호출 하 여 데이터베이스에서 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-260">Next, the movie is deleted from the database by calling the DeleteObject() method followed by the SaveChanges() method.</span></span> <span data-ttu-id="407e4-261">마지막으로, 사용자가 인덱스 보기로 다시 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-261">Finally, the user is redirected back to the Index view.</span></span>

## <a name="summary"></a><span data-ttu-id="407e4-262">요약</span><span class="sxs-lookup"><span data-stu-id="407e4-262">Summary</span></span>

<span data-ttu-id="407e4-263">이 자습서의 목적은 Microsoft Entity Framework 및 ASP.NET MVC의 이용 하 여 데이터베이스 기반 웹 응용 프로그램을 구축 하는 방법을 보여 주기 위한 것 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-263">The purpose of this tutorial was to demonstrate how you can build database-driven web applications by taking advantage of ASP.NET MVC and the Microsoft Entity Framework.</span></span> <span data-ttu-id="407e4-264">선택, 삽입, 업데이트를 사용 하면 응용 프로그램을 빌드하고 데이터베이스 레코드를 삭제 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-264">You learned how to build an application that enables you to select, insert, update, and delete database records.</span></span>

<span data-ttu-id="407e4-265">첫째, 엔터티 데이터 모델 마법사를 사용 하 여 Visual Studio 내에서 엔터티 데이터 모델을 생성 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-265">First, we discussed how you can use the Entity Data Model Wizard to generate an Entity Data Model from within Visual Studio.</span></span> <span data-ttu-id="407e4-266">다음으로 LINQ to Entities 사용 하 여 데이터베이스 테이블에서 데이터베이스 레코드의 집합을 검색 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-266">Next, you learn how to use LINQ to Entities to retrieve a set of database records from a database table.</span></span> <span data-ttu-id="407e4-267">마지막으로 삽입, 업데이트 및 데이터베이스 레코드를 삭제 하는 Entity Framework을 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="407e4-267">Finally, we used the Entity Framework to insert, update, and delete database records.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="407e4-268">[이전](validation-with-the-data-annotation-validators-cs.md)
> [다음](creating-model-classes-with-linq-to-sql-vb.md)</span><span class="sxs-lookup"><span data-stu-id="407e4-268">[Previous](validation-with-the-data-annotation-validators-cs.md)
[Next](creating-model-classes-with-linq-to-sql-vb.md)</span></span>
