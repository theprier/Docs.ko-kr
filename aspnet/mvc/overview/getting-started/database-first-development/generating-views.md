---
uid: mvc/overview/getting-started/database-first-development/generating-views
title: '자습서: ASP.NET MVC 앱을 사용 하 여 EF Database First에 대 한 뷰를 생성'
description: 이 문서는 컨트롤러 및 뷰를 생성 하려면 ASP.NET 스 캐 폴딩을 사용에 중점을 둡니다.
author: Rick-Anderson
ms.author: riande
ms.date: 01/23/2019
ms.topic: tutorial
ms.assetid: 669367cf-8e30-4eb6-821d-10a7d9bb906c
msc.legacyurl: /mvc/overview/getting-started/database-first-development/generating-views
msc.type: authoredcontent
ms.openlocfilehash: e1f6646cdf10d293268b92f44b018709e70c0f86
ms.sourcegitcommit: d5223cf6a2cf80b4f5dc54169b0e376d493d2d3a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54889784"
---
# <a name="tutorial-generate-views-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="907cd-103">자습서: ASP.NET MVC 앱을 사용 하 여 EF Database First에 대 한 뷰를 생성</span><span class="sxs-lookup"><span data-stu-id="907cd-103">Tutorial: Generate views for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="907cd-104">MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여, 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="907cd-105">이 자습서 시리즈에서는 자동으로 표시, 편집, 만들기, 사용자를 사용 하는 코드를 생성 하 고 데이터베이스 테이블에 있는 데이터를 삭제 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="907cd-106">생성된 된 코드는 데이터베이스 테이블의 열에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="907cd-107">이 문서는 컨트롤러 및 뷰를 생성 하려면 ASP.NET 스 캐 폴딩을 사용에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-107">This article focuses on using ASP.NET Scaffolding to generate the controllers and views.</span></span>

<span data-ttu-id="907cd-108">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="907cd-109">스 캐 폴드 추가</span><span class="sxs-lookup"><span data-stu-id="907cd-109">Add scaffold</span></span>
> * <span data-ttu-id="907cd-110">새 보기에 대 한 링크 추가</span><span class="sxs-lookup"><span data-stu-id="907cd-110">Add links to new views</span></span>
> * <span data-ttu-id="907cd-111">학생 뷰를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-111">Display student views</span></span>
> * <span data-ttu-id="907cd-112">등록 보기를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-112">Display enrollment views</span></span>

## <a name="prerequisite"></a><span data-ttu-id="907cd-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="907cd-113">Prerequisite</span></span>

* [<span data-ttu-id="907cd-114">웹 응용 프로그램 및 데이터 모델 만들기</span><span class="sxs-lookup"><span data-stu-id="907cd-114">Create the web application and data models</span></span>](creating-the-web-application.md)

## <a name="add-scaffold"></a><span data-ttu-id="907cd-115">스 캐 폴드 추가</span><span class="sxs-lookup"><span data-stu-id="907cd-115">Add scaffold</span></span>

<span data-ttu-id="907cd-116">모델 클래스에 대 한 표준 데이터 작업을 제공 하는 코드를 생성할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-116">You are ready to generate code that will provide standard data operations for the model classes.</span></span> <span data-ttu-id="907cd-117">스 캐 폴드 항목을 추가 하 여 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-117">You add the code by adding a scaffold item.</span></span> <span data-ttu-id="907cd-118">다음을 추가할 수 있습니다; 스 캐 폴딩 유형에 대 한 여러 가지 이 자습서에서는 이전 섹션에서 만든 학생 및 등록 모델에 해당 하는 뷰와 컨트롤러 스 캐 폴드 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-118">There are many options for the type of scaffolding you can add; in this tutorial, the scaffold will include a controller and views that correspond to the Student and Enrollment models you created in the previous section.</span></span>

<span data-ttu-id="907cd-119">프로젝트에서 일관성을 유지 하려면 기존에 새 컨트롤러를 추가 합니다 **컨트롤러** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-119">To maintain consistency in your project, you will add the new controller to the existing **Controllers** folder.</span></span> <span data-ttu-id="907cd-120">마우스 오른쪽 단추로 클릭 합니다 **컨트롤러** 선택한 폴더 **추가** > **스 캐 폴드 된 새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-120">Right-click the **Controllers** folder, and select **Add** > **New Scaffolded Item**.</span></span>

<span data-ttu-id="907cd-121">선택 된 **Entity Framework를 사용 하 여 뷰를 사용 하 여 MVC 5 컨트롤러** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-121">Select the **MVC 5 Controller with views, using Entity Framework** option.</span></span> <span data-ttu-id="907cd-122">이 옵션은 컨트롤러 및 업데이트, 삭제, 만들기 및 모델의 데이터를 표시 하는 것에 대 한 뷰를 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-122">This option will generate the controller and views for updating, deleting, creating and displaying the data in your model.</span></span>

![mvc 컨트롤러 추가](generating-views/_static/image2.png)

<span data-ttu-id="907cd-124">선택 **학생 (ContosoSite.Models)** 모델 클래스를 선택 합니다 **ContosoUniversityDataEntities (ContosoSite.Models)** 컨텍스트 클래스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-124">Select **Student (ContosoSite.Models)** for the model class and select the **ContosoUniversityDataEntities (ContosoSite.Models)** for the context class.</span></span> <span data-ttu-id="907cd-125">컨트롤러 이름으로 유지할 **StudentsController**합니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-125">Keep the controller name as **StudentsController**.</span></span>

<span data-ttu-id="907cd-126">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-126">Click **Add**.</span></span>

<span data-ttu-id="907cd-127">오류가 발생 하는 경우 이전 섹션에서 프로젝트를 빌드하지 않은 때문에 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-127">If you receive an error, it may be because you did not build the project in the previous section.</span></span> <span data-ttu-id="907cd-128">그렇다면 프로젝트를 빌드하지 및 다음 스 캐 폴드 된 항목을 다시 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-128">If so, try building the project, and then add the scaffolded item again.</span></span>

<span data-ttu-id="907cd-129">새 컨트롤러와 보기를 프로젝트의 참조는 코드 생성 프로세스를 완료 한 후 **컨트롤러** 하 고 **뷰** > **학생** 폴더 .</span><span class="sxs-lookup"><span data-stu-id="907cd-129">After the code generation process is complete, you will see a new controller and views in your project's **Controllers** and **Views** > **Students** folders.</span></span>


<span data-ttu-id="907cd-130">동일한 단계를 다시 수행 하지만 대 한 스 캐 폴드를 추가 합니다 **등록** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-130">Perform the same steps again, but add a scaffold for the **Enrollment** class.</span></span> <span data-ttu-id="907cd-131">가 완료 되 면를 **EnrollmentsController.cs** 파일 및 하위 폴더 **뷰** 이라는 **등록** 만들기, 삭제, 세부 정보, 편집 및 인덱스 보기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-131">When finished, you have an **EnrollmentsController.cs** file, and a folder under **Views** named **Enrollments** with the Create, Delete, Details, Edit and Index views.</span></span>

## <a name="add-links-to-new-views"></a><span data-ttu-id="907cd-132">새 보기에 대 한 링크 추가</span><span class="sxs-lookup"><span data-stu-id="907cd-132">Add links to new views</span></span>

<span data-ttu-id="907cd-133">새 보기를 탐색 하기 쉽게 학생 및 등록에 대 한 하이퍼링크의 몇 인덱스 뷰를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-133">To make it easier for you to navigate to your new views, you can add a couple of hyperlinks to the Index views for students and enrollments.</span></span> <span data-ttu-id="907cd-134">파일을 엽니다 **뷰** > **홈** > *Index.cshtml*는 사이트에 대 한 홈 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-134">Open the file at **Views** > **Home** > *Index.cshtml*, which is the home page for your site.</span></span> <span data-ttu-id="907cd-135">Jumbotron는 아래에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-135">Add the following code below the jumbotron.</span></span>

[!code-cshtml[Main](generating-views/samples/sample1.cshtml)]

<span data-ttu-id="907cd-136">ActionLink 메서드에 대 한 첫 번째 매개 변수 링크에 표시할 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-136">For the ActionLink method, the first parameter is the text to display in the link.</span></span> <span data-ttu-id="907cd-137">두 번째 매개 변수는 작업 및 세 번째 매개 변수는 컨트롤러의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-137">The second parameter is the action and the third parameter is the name of the controller.</span></span> <span data-ttu-id="907cd-138">예를 들어, 첫 번째 링크 StudentsController에서 인덱스 작업을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-138">For example, the first link points to the Index action in StudentsController.</span></span> <span data-ttu-id="907cd-139">실제 하이퍼링크는 이러한 값에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-139">The actual hyperlink is constructed from these values.</span></span> <span data-ttu-id="907cd-140">궁극적으로 첫 번째 링크를 통해 사용자는 **Index.cshtml** 내에서 파일을 **뷰/학생** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-140">The first link ultimately takes users to the **Index.cshtml** file within the **Views/Students** folder.</span></span>

## <a name="display-student-views"></a><span data-ttu-id="907cd-141">학생 뷰를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-141">Display student views</span></span>

<span data-ttu-id="907cd-142">프로젝트에 올바르게 추가 코드는 학생의 목록을 표시 하 고 편집, 생성 또는 데이터베이스의 학생 레코드를 삭제 하면을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-142">You will verify that the code added to your project correctly displays a list of the students, and enables users to edit, create, or delete the student records in the database.</span></span>

<span data-ttu-id="907cd-143">마우스 오른쪽 단추로 클릭 합니다 **뷰** > **홈** > *Index.cshtml* 파일을 열고 선택 **브라우저에서 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-143">Right-click the **Views** > **Home** > *Index.cshtml* file, and select **View in Browser**.</span></span> <span data-ttu-id="907cd-144">응용 프로그램 홈 페이지에서 선택 **학생의 목록을**합니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-144">On the application home page, select **List of students**.</span></span>

![](generating-views/_static/image6.png)

<span data-ttu-id="907cd-145">에 **인덱스** 페이지에서이 데이터를 수정 하는 학생과 링크 목록을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-145">On the **Index** page, notice the list of the students and links to modify this data.</span></span> <span data-ttu-id="907cd-146">선택 된 **새로 만들기** 에 연결 하 고 새 학생에 대 한 일부 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-146">Select the **Create New** link and provide some values for a new student.</span></span> <span data-ttu-id="907cd-147">클릭 **만들기**, 및 새 학생 목록에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-147">Click **Create**, and notice the new student is added to your list.</span></span>

<span data-ttu-id="907cd-148">다시를 **인덱스** 페이지에서 선택 합니다 **편집** 링크를 선택한 학생에 대 한 일부 값을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-148">Back on the **Index** page, select the **Edit** link, and change some of the values for a student.</span></span> <span data-ttu-id="907cd-149">클릭 **저장할**, 학생 레코드가 변경 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-149">Click **Save**, and notice the student record has been changed.</span></span>

<span data-ttu-id="907cd-150">마지막으로 선택 합니다 **삭제** 에 연결 하 고 클릭 하 여 레코드를 삭제할 것인지 확인 합니다 **삭제** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-150">Finally, select the **Delete** link and confirm that you want to delete the record by clicking the **Delete** button.</span></span>

<span data-ttu-id="907cd-151">모든 코드를 작성 하지 않고도 Student 테이블에서 데이터에 대 한 일반적인 작업을 수행 하는 뷰를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-151">Without writing any code, you have added views that perform common operations on the data in the Student table.</span></span>

<span data-ttu-id="907cd-152">알 수 있습니다는 필드의 텍스트 레이블을 속성을 기반으로 데이터베이스 (같은 **LastName**) 없는 반드시 웹 페이지에 표시 하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-152">You may have noticed that the text label for a field is based on the database property (such as **LastName**) which is not necessarily what you want to display on the web page.</span></span> <span data-ttu-id="907cd-153">예를 들어 되도록 레이블 수도 **Last Name**합니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-153">For example, you may prefer the label to be **Last Name**.</span></span> <span data-ttu-id="907cd-154">이 자습서의 뒷부분에 나오는이 디스플레이 문제를 해결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-154">You will fix this display issue later in the tutorial.</span></span>

## <a name="display-enrollment-views"></a><span data-ttu-id="907cd-155">등록 보기를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-155">Display enrollment views</span></span>

<span data-ttu-id="907cd-156">데이터베이스에는 학생 및 등록 테이블 사이의 강좌 및 등록 테이블 사이 일 대 다 관계에 일 대 다 관계를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-156">Your database includes a one-to-many relationship between the Student and Enrollment tables, and a one-to-many relationship between the Course and Enrollment tables.</span></span> <span data-ttu-id="907cd-157">등록에 대 한 뷰는 이러한 관계를 올바르게 처리.</span><span class="sxs-lookup"><span data-stu-id="907cd-157">The views for Enrollment correctly handle these relationships.</span></span> <span data-ttu-id="907cd-158">선택한 서버 사이트에 대 한 홈 페이지로 이동 합니다 **등록 목록** 링크 차례로 합니다 **새로 만들기** 링크.</span><span class="sxs-lookup"><span data-stu-id="907cd-158">Navigate to the home page for your site and select the **List of enrollments** link and then the **Create New** link.</span></span>

<span data-ttu-id="907cd-159">보기에는 새 등록 레코드를 만드는 양식이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-159">The view displays a form for creating a new enrollment record.</span></span> <span data-ttu-id="907cd-160">특히, 폼에 포함 되어 있음을 알 수 있습니다는 **CourseID** 드롭 다운 목록 및 **StudentID** 드롭 다운 목록.</span><span class="sxs-lookup"><span data-stu-id="907cd-160">In particular, notice that the form contains a **CourseID** drop-down list and a **StudentID** drop-down list.</span></span> <span data-ttu-id="907cd-161">두 관련된 테이블의 값으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-161">Both are populated with values from the related tables.</span></span>

<span data-ttu-id="907cd-162">또한 필드의 데이터 형식에 제공된 된 값의 유효성 검사는 따라 적용 자동으로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-162">Furthermore, validation of the provided values is automatically applied based on the data type of the field.</span></span> <span data-ttu-id="907cd-163">**등급** 호환 되지 않는 값을 제공 하려고 하면 오류 메시지가 표시 됩니다 있도록 숫자로 필요 합니다. *엔터프라이즈급 필드는 숫자 여야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="907cd-163">**Grade** requires a number, so an error message is displayed if you try to provide an incompatible value: *The field Grade must be a number.*</span></span>

<span data-ttu-id="907cd-164">자동으로 생성 된 뷰를 사용 하는 사용자가 데이터베이스의 데이터로 작업할 수 있도록 확인 했습니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-164">You have verified that the automatically-generated views enable users to work with the data in the database.</span></span> <span data-ttu-id="907cd-165">이 시리즈의 다음 자습서에서는 데이터베이스를 업데이트 하 고 웹 응용 프로그램에서 해당 변경 됩니다 합니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-165">In the next tutorial in this series, you will update the database and make the corresponding changes in the web application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="907cd-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="907cd-166">Next steps</span></span>

<span data-ttu-id="907cd-167">이 자습서에서는 다음을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-167">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="907cd-168">추가 스 캐 폴드</span><span class="sxs-lookup"><span data-stu-id="907cd-168">Added scaffold</span></span>
> * <span data-ttu-id="907cd-169">새 보기에 대 한 추가 링크</span><span class="sxs-lookup"><span data-stu-id="907cd-169">Added links to new views</span></span>
> * <span data-ttu-id="907cd-170">표시 된 학생 뷰</span><span class="sxs-lookup"><span data-stu-id="907cd-170">Displayed student views</span></span>
> * <span data-ttu-id="907cd-171">표시 된 등록 보기</span><span class="sxs-lookup"><span data-stu-id="907cd-171">Displayed enrollment views</span></span>

<span data-ttu-id="907cd-172">데이터베이스를 변경 하는 방법을 알아보려면 다음 문서로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="907cd-172">Advance to the next article to learn how to change the database.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="907cd-173">데이터베이스 변경</span><span class="sxs-lookup"><span data-stu-id="907cd-173">Change the database</span></span>](changing-the-database.md)