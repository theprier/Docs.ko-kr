---
uid: mvc/overview/getting-started/database-first-development/generating-views
title: 'ASP.NET MVC를 사용 하 여 먼저 EF Database: 뷰 생성 | Microsoft Docs'
author: tfitzmac
description: MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여, 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 seri...
ms.author: aspnetcontent
ms.date: 12/29/2014
ms.assetid: 669367cf-8e30-4eb6-821d-10a7d9bb906c
msc.legacyurl: /mvc/overview/getting-started/database-first-development/generating-views
msc.type: authoredcontent
ms.openlocfilehash: 9c85b330ac415d8c73d58b31a5108197b754669f
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37835330"
---
<a name="ef-database-first-with-aspnet-mvc-generating-views"></a><span data-ttu-id="bcb63-104">ASP.NET MVC를 사용 하 여 먼저 EF Database: 뷰를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-104">EF Database First with ASP.NET MVC: Generating Views</span></span>
====================
<span data-ttu-id="bcb63-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="bcb63-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="bcb63-106">MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여, 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-106">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="bcb63-107">이 자습서 시리즈에서는 자동으로 표시, 편집, 만들기, 사용자를 사용 하는 코드를 생성 하 고 데이터베이스 테이블에 있는 데이터를 삭제 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-107">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="bcb63-108">생성된 된 코드는 데이터베이스 테이블의 열에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-108">The generated code corresponds to the columns in the database table.</span></span>
> 
> <span data-ttu-id="bcb63-109">시리즈의이 부분 컨트롤러 및 뷰를 생성 하려면 ASP.NET 스 캐 폴딩을 사용에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-109">This part of the series focuses on using ASP.NET Scaffolding to generate the controllers and views.</span></span>


## <a name="add-scaffold"></a><span data-ttu-id="bcb63-110">스 캐 폴드 추가</span><span class="sxs-lookup"><span data-stu-id="bcb63-110">Add scaffold</span></span>

<span data-ttu-id="bcb63-111">모델 클래스에 대 한 표준 데이터 작업을 제공 하는 코드를 생성할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-111">You are ready to generate code that will provide standard data operations for the model classes.</span></span> <span data-ttu-id="bcb63-112">스 캐 폴드 항목을 추가 하 여 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-112">You add the code by adding a scaffold item.</span></span> <span data-ttu-id="bcb63-113">다음을 추가할 수 있습니다; 스 캐 폴딩 유형에 대 한 여러 가지 이 자습서에서는 이전 섹션에서 만든 학생 및 등록 모델에 해당 하는 뷰와 컨트롤러 스 캐 폴드 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-113">There are many options for the type of scaffolding you can add; in this tutorial, the scaffold will include a controller and views that correspond to the Student and Enrollment models you created in the previous section.</span></span>

<span data-ttu-id="bcb63-114">프로젝트에서 일관성을 유지 하려면 기존에 새 컨트롤러를 추가 합니다 **컨트롤러** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-114">To maintain consistency in your project, you will add the new controller to the existing **Controllers** folder.</span></span> <span data-ttu-id="bcb63-115">마우스 오른쪽 단추로 클릭 합니다 **컨트롤러** 선택한 폴더 **추가** – **스 캐 폴드 된 새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-115">Right-click the **Controllers** folder, and select **Add** – **New Scaffolded Item**.</span></span>

![스 캐 폴드 추가](generating-views/_static/image1.png)

<span data-ttu-id="bcb63-117">선택 된 **Entity Framework를 사용 하 여 뷰를 사용 하 여 MVC 5 컨트롤러** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-117">Select the **MVC 5 Controller with views, using Entity Framework** option.</span></span> <span data-ttu-id="bcb63-118">이 옵션은 컨트롤러 및 업데이트, 삭제, 만들기 및 모델의 데이터를 표시 하는 것에 대 한 뷰를 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-118">This option will generate the controller and views for updating, deleting, creating and displaying the data in your model.</span></span>

![mvc 컨트롤러 추가](generating-views/_static/image2.png)

<span data-ttu-id="bcb63-120">선택 **학생** 모델 클래스를 선택 합니다 **ContosoUniversityEntities** 컨텍스트 클래스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-120">Select **Student** for the model class, and select the **ContosoUniversityEntities** for the context class.</span></span> <span data-ttu-id="bcb63-121">컨트롤러 이름으로 유지할 **StudentsController**,</span><span class="sxs-lookup"><span data-stu-id="bcb63-121">Keep the controller name as **StudentsController**,</span></span>

![컨트롤러를 지정 합니다.](generating-views/_static/image3.png)

<span data-ttu-id="bcb63-123">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-123">Click **Add**.</span></span>

<span data-ttu-id="bcb63-124">오류가 발생 하는 경우 이전 섹션에서 프로젝트를 빌드하지 않은 때문에 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-124">If you receive an error, it may be because you did not build the project in the previous section.</span></span> <span data-ttu-id="bcb63-125">그렇다면 프로젝트를 빌드하지 및 다음 스 캐 폴드 된 항목을 다시 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-125">If so, try building the project, and then add the scaffolded item again.</span></span>

<span data-ttu-id="bcb63-126">코드 생성 프로세스를 완료 한 후 새 컨트롤러 및 뷰를 참조 하십시오는 프로젝트에서.</span><span class="sxs-lookup"><span data-stu-id="bcb63-126">After the code generation process is complete, you will see a new controller and views in your project.</span></span>

![뷰를 표시 합니다.](generating-views/_static/image4.png)

<span data-ttu-id="bcb63-128">동일한 단계를 다시 수행 하지만 등록 클래스에 대 한 스 캐 폴드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-128">Perform the same steps again, but add a scaffold for the Enrollment class.</span></span> <span data-ttu-id="bcb63-129">완료 되 면 해야는 **EnrollmentsController.cs** 파일 및 하위 폴더 **뷰** 이라는 **등록** 만들기, 삭제, 세부 정보, 편집 및 인덱스를 사용 하 여 레이아웃.</span><span class="sxs-lookup"><span data-stu-id="bcb63-129">When finished, you should have an **EnrollmentsController.cs** file, and a folder under **Views** named **Enrollments** with the Create, Delete, Details, Edit and Index views.</span></span>

![뷰를 표시 합니다.](generating-views/_static/image5.png)

## <a name="add-links-to-new-views"></a><span data-ttu-id="bcb63-131">새 보기에 대 한 링크 추가</span><span class="sxs-lookup"><span data-stu-id="bcb63-131">Add links to new views</span></span>

<span data-ttu-id="bcb63-132">새 보기를 탐색 하기 쉽게 학생 및 등록에 대 한 하이퍼링크의 몇 인덱스 뷰를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-132">To make it easier for you to navigate to your new views, you can add a couple of hyperlinks to the Index views for students and enrollments.</span></span> <span data-ttu-id="bcb63-133">파일을 엽니다 **Views/Home/Index.cshtml**는 사이트에 대 한 홈 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-133">Open the file at **Views/Home/Index.cshtml**, which is the home page for your site.</span></span> <span data-ttu-id="bcb63-134">Jumbotron는 아래에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-134">Add the following code below the jumbotron.</span></span>

[!code-cshtml[Main](generating-views/samples/sample1.cshtml)]

<span data-ttu-id="bcb63-135">ActionLink 메서드에 대 한 첫 번째 매개 변수 링크에 표시할 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-135">For the ActionLink method, the first parameter is the text to display in the link.</span></span> <span data-ttu-id="bcb63-136">두 번째 매개 변수는 작업 및 세 번째 매개 변수는 컨트롤러의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-136">The second parameter is the action and the third parameter is the name of the controller.</span></span> <span data-ttu-id="bcb63-137">예를 들어, 첫 번째 링크 StudentsController에서 인덱스 작업을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-137">For example, the first link points to the Index action in StudentsController.</span></span> <span data-ttu-id="bcb63-138">실제 하이퍼링크는 이러한 값에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-138">The actual hyperlink is constructed from these values.</span></span> <span data-ttu-id="bcb63-139">궁극적으로 첫 번째 링크를 통해 사용자는 **Index.cshtml** 내에서 파일을 **뷰/학생** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-139">The first link ultimately takes users to the **Index.cshtml** file within the **Views/Students** folder.</span></span>

## <a name="display-student-views"></a><span data-ttu-id="bcb63-140">학생 뷰를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-140">Display student views</span></span>

<span data-ttu-id="bcb63-141">프로젝트에 올바르게 추가 코드는 학생의 목록을 표시 하 고 편집, 생성 또는 데이터베이스의 학생 레코드를 삭제 하면을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-141">You will verify that the code added to your project correctly displays a list of the students, and enables users to edit, create, or delete the student records in the database.</span></span>

<span data-ttu-id="bcb63-142">마우스 오른쪽 단추로 클릭 합니다 **Views/Home/Index.cshtml** 파일을 열고 선택 **브라우저에서 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-142">Right-click the **Views/Home/Index.cshtml** file, and select **View in Browser**.</span></span> <span data-ttu-id="bcb63-143">이 페이지에서는 학생 목록에 대 한 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-143">On this page, click the link for the list of students.</span></span>

![](generating-views/_static/image6.png)

<span data-ttu-id="bcb63-144">이 페이지에서는이 데이터를 수정 하는 학생과 링크 목록을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-144">On this page, notice the list of the students and links to modify this data.</span></span>

![학생 목록](generating-views/_static/image7.png)

<span data-ttu-id="bcb63-146">클릭 합니다 **새로 만들기** 에 연결 하 고 새 학생에 대 한 일부 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-146">Click the **Create New** link and provide some values for a new student.</span></span>

![새 학생을 만들려면](generating-views/_static/image8.png)

<span data-ttu-id="bcb63-148">클릭 **만들기**, 및 새 학생 목록에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-148">Click **Create**, and notice the new student is added to your list.</span></span>

![새 학생을 사용 하 여 목록](generating-views/_static/image9.png)

<span data-ttu-id="bcb63-150">선택 된 **편집** 링크를 선택한 학생에 대 한 일부 값을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-150">Select the **Edit** link, and change some of the values for a student.</span></span>

![학생 편집](generating-views/_static/image10.png)

<span data-ttu-id="bcb63-152">클릭 **저장할**, 학생 레코드가 변경 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-152">Click **Save**, and notice the student record has been changed.</span></span>

<span data-ttu-id="bcb63-153">마지막으로 선택 합니다 **삭제** 에 연결 하 고 클릭 하 여 레코드를 삭제할 것인지 확인 합니다 **삭제** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-153">Finally, select the **Delete** link and confirm that you want to delete the record by clicking the **Delete** button.</span></span>

![학생 삭제](generating-views/_static/image11.png)

<span data-ttu-id="bcb63-155">모든 코드를 작성 하지 않고도 Student 테이블에서 데이터에 대 한 일반적인 작업을 수행 하는 뷰를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-155">Without writing any code, you have added views that perform common operations on the data in the Student table.</span></span>

<span data-ttu-id="bcb63-156">알 수 있습니다는 필드의 텍스트 레이블을 속성을 기반으로 데이터베이스 (같은 **LastName**) 없는 반드시 웹 페이지에 표시 하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-156">You may have noticed that the text label for a field is based on the database property (such as **LastName**) which is not necessarily what you want to display on the web page.</span></span> <span data-ttu-id="bcb63-157">예를 들어 되도록 레이블 수도 **Last Name**합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-157">For example, you may prefer the label to be **Last Name**.</span></span> <span data-ttu-id="bcb63-158">이 자습서의 뒷부분에 나오는이 디스플레이 문제를 해결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-158">You will fix this display issue later in the tutorial.</span></span>

## <a name="display-enrollment-views"></a><span data-ttu-id="bcb63-159">등록 보기를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-159">Display enrollment views</span></span>

<span data-ttu-id="bcb63-160">데이터베이스에는 학생 및 등록 테이블 사이의 강좌 및 등록 테이블 사이 일 대 다 관계에 일 대 다 관계를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-160">Your database includes a one-to-many relationship between the Student and Enrollment tables, and a one-to-many relationship between the Course and Enrollment tables.</span></span> <span data-ttu-id="bcb63-161">등록에 대 한 뷰는 이러한 관계를 올바르게 처리.</span><span class="sxs-lookup"><span data-stu-id="bcb63-161">The views for Enrollment correctly handle these relationships.</span></span> <span data-ttu-id="bcb63-162">선택한 서버 사이트에 대 한 홈 페이지로 이동 합니다 **등록 목록** 링크 차례로 합니다 **새로 만들기** 링크.</span><span class="sxs-lookup"><span data-stu-id="bcb63-162">Navigate to the home page for your site and select the **List of enrollments** link and then the **Create New** link.</span></span> <span data-ttu-id="bcb63-163">보기에는 새 등록 레코드를 만드는 양식이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-163">The view displays a form for creating a new enrollment record.</span></span> <span data-ttu-id="bcb63-164">특히, 형식 관련된 테이블의 값으로 채워지는 드롭다운 목록 두 개 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-164">In particular, notice that the form contains two drop-down lists that are populated with values from the related tables.</span></span>

![등록 만들기](generating-views/_static/image12.png)

<span data-ttu-id="bcb63-166">또한 필드의 데이터 형식에 제공된 된 값의 유효성 검사는 따라 적용 자동으로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-166">Furthermore, validation of the provided values is automatically applied based on the data type of the field.</span></span> <span data-ttu-id="bcb63-167">등급 호환 되지 않는 값을 제공 하려고 하면 오류 메시지가 표시 됩니다 있도록 숫자로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-167">Grade requires a number, so an error message is displayed if you try to provide an incompatible value.</span></span>

![유효성 검사 메시지](generating-views/_static/image13.png)

<span data-ttu-id="bcb63-169">자동으로 생성 된 뷰를 사용 하는 사용자가 데이터베이스의 데이터로 작업할 수 있도록 확인 했습니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-169">You have verified that the automatically-generated views enable users to work with the data in the database.</span></span> <span data-ttu-id="bcb63-170">이 시리즈의 다음 자습서에서는 데이터베이스를 업데이트 하 고 웹 응용 프로그램에서 해당 변경 됩니다 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcb63-170">In the next tutorial in this series, you will update the database and make the corresponding changes in the web application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="bcb63-171">[이전](creating-the-web-application.md)
> [다음](changing-the-database.md)</span><span class="sxs-lookup"><span data-stu-id="bcb63-171">[Previous](creating-the-web-application.md)
[Next](changing-the-database.md)</span></span>
