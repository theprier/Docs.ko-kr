---
uid: mvc/overview/getting-started/database-first-development/changing-the-database
title: 'ASP.NET MVC를 사용 하 여 먼저 EF Database: 데이터베이스를 변경 | Microsoft Docs'
author: tfitzmac
description: MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여, 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 seri...
ms.author: aspnetcontent
ms.date: 10/01/2014
ms.assetid: cfd5c083-a319-482e-8f25-5b38caa93954
msc.legacyurl: /mvc/overview/getting-started/database-first-development/changing-the-database
msc.type: authoredcontent
ms.openlocfilehash: 0176274694426a527ed0862b5138919d4cf5c319
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37840943"
---
<a name="ef-database-first-with-aspnet-mvc-changing-the-database"></a><span data-ttu-id="a72ff-104">ASP.NET MVC를 사용 하 여 먼저 EF Database: 데이터베이스를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-104">EF Database First with ASP.NET MVC: Changing the Database</span></span>
====================
<span data-ttu-id="a72ff-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="a72ff-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="a72ff-106">MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여, 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-106">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="a72ff-107">이 자습서 시리즈에서는 자동으로 표시, 편집, 만들기, 사용자를 사용 하는 코드를 생성 하 고 데이터베이스 테이블에 있는 데이터를 삭제 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-107">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="a72ff-108">생성된 된 코드는 데이터베이스 테이블의 열에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-108">The generated code corresponds to the columns in the database table.</span></span>
> 
> <span data-ttu-id="a72ff-109">시리즈의이 부분 데이터베이스 구조를 업데이트 하 고 웹 응용 프로그램 전체에서 해당 변경 내용을 전파에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-109">This part of the series focuses on making an update to the database structure and propagating that change throughout the web application.</span></span>


## <a name="add-a-column"></a><span data-ttu-id="a72ff-110">열 추가</span><span class="sxs-lookup"><span data-stu-id="a72ff-110">Add a column</span></span>

<span data-ttu-id="a72ff-111">데이터베이스에서 테이블의 구조를 업데이트 하는 경우 변경 내용을 데이터 모델, 뷰 및 컨트롤러에 전파 되는 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-111">If you update the structure of a table in your database, you need to ensure that your change is propagated to the data model, views, and controller.</span></span>

<span data-ttu-id="a72ff-112">이 자습서에서는 학생의 중간 이름은 기록할 학생 테이블에 새 열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-112">For this tutorial, you will add a new column to the Student table to record the middle name of the student.</span></span> <span data-ttu-id="a72ff-113">이 열을 추가 하려면 데이터베이스 프로젝트를 열고 Student.sql 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-113">To add this column, open the database project, and open the Student.sql file.</span></span> <span data-ttu-id="a72ff-114">디자이너 또는 T-SQL 코드를 통해 라는 열을 추가 **MiddleName** 는 nvarchar (50)을 NULL 값을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-114">Through either the designer or the T-SQL code, add a column named **MiddleName** that is an NVARCHAR(50) and allows NULL values.</span></span>

![중간 이름 추가](changing-the-database/_static/image1.png)

<span data-ttu-id="a72ff-116">데이터베이스 프로젝트 (또는 f5 키)를 시작 하 여 로컬 데이터베이스에이 변경 내용을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-116">Deploy this change to your local database by starting your database project (or F5).</span></span> <span data-ttu-id="a72ff-117">새 필드를 테이블에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-117">The new field is added to the table.</span></span> <span data-ttu-id="a72ff-118">SQL Server 개체 탐색기에 표시 되지 않으면 창의 새로 고침 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-118">If you do not see it in the SQL Server Object Explorer, click the Refresh button in the pane.</span></span>

![새 열을 표시](changing-the-database/_static/image2.png)

<span data-ttu-id="a72ff-120">데이터베이스 테이블에 새 열이 있지만 데이터 모델 클래스에 현재 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-120">The new column exists in the database table, but it does not currently exist in the data model class.</span></span> <span data-ttu-id="a72ff-121">새 열을 포함 하도록 모델을 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-121">You must update the model to include your new column.</span></span> <span data-ttu-id="a72ff-122">에 **모델** 폴더를 열고 합니다 **ContosoModel.edmx** 모델 다이어그램을 표시 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-122">In the **Models** folder, open the **ContosoModel.edmx** file to display the model diagram.</span></span> <span data-ttu-id="a72ff-123">학생 모델 MiddleName 속성이 없는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-123">Notice that the Student model does not contain the MiddleName property.</span></span> <span data-ttu-id="a72ff-124">디자인 화면에서 아무 곳 이나 마우스 오른쪽 단추로 클릭 하 고 선택 **데이터베이스에서 모델 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-124">Right-click anywhere on the design surface, and select **Update Model from Database**.</span></span>

![모델 업데이트](changing-the-database/_static/image3.png)

<span data-ttu-id="a72ff-126">업데이트 마법사에서 선택 합니다 **새로 고침** 탭 및 **학생** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-126">In the Update Wizard, select the **Refresh** tab and the **Student** table.</span></span>

![업데이트 마법사](changing-the-database/_static/image4.png)

<span data-ttu-id="a72ff-128">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-128">Click **Finish**.</span></span>

<span data-ttu-id="a72ff-129">데이터베이스 다이어그램에 새 업데이트 프로세스가 완료 되 면 **MiddleName** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-129">After the update process is finished, the database diagram includes the new **MiddleName** property.</span></span> <span data-ttu-id="a72ff-130">저장 된 **ContosoModel.edmx** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-130">Save the **ContosoModel.edmx** file.</span></span> <span data-ttu-id="a72ff-131">새 속성에 전파에 대 한이 파일을 저장 해야 합니다 **Student.cs** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-131">You must save this file for the new property to be propagated to the **Student.cs** class.</span></span> <span data-ttu-id="a72ff-132">이제 데이터베이스 및 모델을 업데이트 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-132">You have now updated the database and the model.</span></span>

<span data-ttu-id="a72ff-133">솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-133">Build the solution.</span></span>

<span data-ttu-id="a72ff-134">그러나 뷰 여전히 없는 새 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-134">Unfortunately, the views still do not contain the new property.</span></span> <span data-ttu-id="a72ff-135">뷰를 업데이트 하려면 두 가지 옵션이 있습니다-Student 클래스에 대 한 스 캐 폴딩 다시 한 번 추가 하 여 뷰를 다시 생성 하거나 수 또는 기존 보기에 새 속성을 수동으로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-135">To update the views you have two options - you can either re-generate the views by once again adding scaffolding for the Student class, or you can manually add the new property to your existing views.</span></span> <span data-ttu-id="a72ff-136">이 자습서에서는 스 캐 폴딩을 추가 다시 하지 사용자 지정된 내용을 자동으로 생성 된 보기에 변경한 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-136">In this tutorial, you will add the scaffolding again because you have not made any customized changes to the automatically-generated views.</span></span> <span data-ttu-id="a72ff-137">뷰를 변경 하 고 해당 변경 내용을 손실 하지 않으려는 경우 속성을 수동으로 추가 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-137">You might consider manually adding the property when you have made changes to the views and do not want to lose those changes.</span></span>

<span data-ttu-id="a72ff-138">뷰는 다시 생성, 삭제 합니다 **학생** 아래에 폴더 **뷰**, 및 삭제를 **StudentsController**.</span><span class="sxs-lookup"><span data-stu-id="a72ff-138">To ensure the views are re-created, delete the **Students** folder under **Views**, and delete the **StudentsController**.</span></span> <span data-ttu-id="a72ff-139">마우스 오른쪽 단추로 클릭 합니다 **컨트롤러** 폴더에 대 한 스 캐 폴딩을 추가 및 합니다 **학생** 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-139">Then, right-click the **Controllers** folder and add scaffolding for the **Student** model.</span></span> <span data-ttu-id="a72ff-140">마찬가지로 컨트롤러 이름을 **StudentsController**합니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-140">Again, name the controller **StudentsController**.</span></span> <span data-ttu-id="a72ff-141">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-141">Select **OK**.</span></span>

<span data-ttu-id="a72ff-142">이제는 뷰 MiddleName 속성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-142">The views now contain the MiddleName property.</span></span>

![중간 이름 표시](changing-the-database/_static/image5.png)

<span data-ttu-id="a72ff-144">다음 섹션에서는 학생 레코드에 대 한 세부 정보를 표시 하는 것에 대 한 보기를 사용자 지정 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a72ff-144">In the next section, you will add code to customize the view for showing details about a student record.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a72ff-145">[이전](generating-views.md)
> [다음](customizing-a-view.md)</span><span class="sxs-lookup"><span data-stu-id="a72ff-145">[Previous](generating-views.md)
[Next](customizing-a-view.md)</span></span>
