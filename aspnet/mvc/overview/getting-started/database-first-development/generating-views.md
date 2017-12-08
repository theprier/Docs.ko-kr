---
uid: mvc/overview/getting-started/database-first-development/generating-views
title: "ASP.NET MVC를 사용 하 여 먼저 EF 데이터베이스: 뷰를 생성 | Microsoft Docs"
author: tfitzmac
description: "MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 seri 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/29/2014
ms.topic: article
ms.assetid: 669367cf-8e30-4eb6-821d-10a7d9bb906c
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/database-first-development/generating-views
msc.type: authoredcontent
ms.openlocfilehash: 5fccb3c56af0945ec448becff777a3e92dc160d7
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="ef-database-first-with-aspnet-mvc-generating-views"></a><span data-ttu-id="4c508-104">ASP.NET MVC를 사용 하 여 먼저 EF 데이터베이스: 뷰 생성</span><span class="sxs-lookup"><span data-stu-id="4c508-104">EF Database First with ASP.NET MVC: Generating Views</span></span>
====================
<span data-ttu-id="4c508-105">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="4c508-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="4c508-106">MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-106">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="4c508-107">이 자습서 시리즈 자동으로 표시, 편집를 만들 수 있도록 하는 코드를 생성 하 고 데이터베이스 테이블에 있는 데이터를 삭제 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-107">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="4c508-108">생성 된 코드는 데이터베이스 테이블의 열에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-108">The generated code corresponds to the columns in the database table.</span></span>
> 
> <span data-ttu-id="4c508-109">시리즈의이 부분 컨트롤러와 뷰를 생성 하려면 ASP.NET 스 캐 폴딩을 사용에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-109">This part of the series focuses on using ASP.NET Scaffolding to generate the controllers and views.</span></span>


## <a name="add-scaffold"></a><span data-ttu-id="4c508-110">스 캐 폴드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-110">Add scaffold</span></span>

<span data-ttu-id="4c508-111">모델 클래스에 대 한 표준 데이터 작업을 제공 하는 코드를 생성할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-111">You are ready to generate code that will provide standard data operations for the model classes.</span></span> <span data-ttu-id="4c508-112">스 캐 폴드 항목을 추가 하 여 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-112">You add the code by adding a scaffold item.</span></span> <span data-ttu-id="4c508-113">여러 가지 옵션이 있습니다 스 캐 폴드를 추가할 수 있습니다; 형식에 대 한 이 자습서에서는 이전 섹션에서 만든 학생과 등록 모델에 해당 하는 뷰와 컨트롤러는 스 캐 폴드 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-113">There are many options for the type of scaffolding you can add; in this tutorial, the scaffold will include a controller and views that correspond to the Student and Enrollment models you created in the previous section.</span></span>

<span data-ttu-id="4c508-114">프로젝트에서 일관성을 유지 하려면 기존에 새로운 컨트롤러를 추가 합니다 **컨트롤러** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-114">To maintain consistency in your project, you will add the new controller to the existing **Controllers** folder.</span></span> <span data-ttu-id="4c508-115">마우스 오른쪽 단추로 클릭는 **컨트롤러** 폴더를 찾아 선택 **추가** – **스 캐 폴드 된 새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-115">Right-click the **Controllers** folder, and select **Add** – **New Scaffolded Item**.</span></span>

![스 캐 폴드를 추가 합니다.](generating-views/_static/image1.png)

<span data-ttu-id="4c508-117">선택 된 **Entity Framework를 사용 하 여 뷰를 포함 된 MVC 5 컨트롤러** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-117">Select the **MVC 5 Controller with views, using Entity Framework** option.</span></span> <span data-ttu-id="4c508-118">이 옵션은 컨트롤러와 뷰 업데이트, 삭제, 만들고 표시 하기 위한 데이터 모델에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-118">This option will generate the controller and views for updating, deleting, creating and displaying the data in your model.</span></span>

![mvc 컨트롤러 추가](generating-views/_static/image2.png)

<span data-ttu-id="4c508-120">선택 **학생** 선택한 모델 클래스에 대 한는 **ContosoUniversityEntities** 컨텍스트 클래스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-120">Select **Student** for the model class, and select the **ContosoUniversityEntities** for the context class.</span></span> <span data-ttu-id="4c508-121">컨트롤러 이름으로 유지 **StudentsController**,</span><span class="sxs-lookup"><span data-stu-id="4c508-121">Keep the controller name as **StudentsController**,</span></span>

![컨트롤러를 지정 합니다.](generating-views/_static/image3.png)

<span data-ttu-id="4c508-123">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-123">Click **Add**.</span></span>

<span data-ttu-id="4c508-124">이전 섹션에서 프로젝트를 빌드하지 않은 오류가 발생 하는 경우 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-124">If you receive an error, it may be because you did not build the project in the previous section.</span></span> <span data-ttu-id="4c508-125">이 경우 프로젝트를 빌드하지 시도 하 고 다시 스 캐 폴드 된 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-125">If so, try building the project, and then add the scaffolded item again.</span></span>

<span data-ttu-id="4c508-126">코드 생성 프로세스가 완료 되 면 프로젝트에서 새로운 컨트롤러와 뷰를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-126">After the code generation process is complete, you will see a new controller and views in your project.</span></span>

![보기 표시](generating-views/_static/image4.png)

<span data-ttu-id="4c508-128">동일한 단계를 다시 수행 하지만 등록 클래스에 대 한 스 캐 폴드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-128">Perform the same steps again, but add a scaffold for the Enrollment class.</span></span> <span data-ttu-id="4c508-129">완료 되 면 나면는 **EnrollmentsController.cs** 파일과 하위 폴더 **뷰** 라는 **등록** 된 만들기, 삭제, 세부 정보, 편집 및 인덱스 레이아웃.</span><span class="sxs-lookup"><span data-stu-id="4c508-129">When finished, you should have an **EnrollmentsController.cs** file, and a folder under **Views** named **Enrollments** with the Create, Delete, Details, Edit and Index views.</span></span>

![보기 표시](generating-views/_static/image5.png)

## <a name="add-links-to-new-views"></a><span data-ttu-id="4c508-131">새 보기에 링크 추가</span><span class="sxs-lookup"><span data-stu-id="4c508-131">Add links to new views</span></span>

<span data-ttu-id="4c508-132">새 보기를 탐색할 수에 대 한 쉽게 학생 및 등록을 위한 인덱스 뷰를 몇 가지 하이퍼링크를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-132">To make it easier for you to navigate to your new views, you can add a couple of hyperlinks to the Index views for students and enrollments.</span></span> <span data-ttu-id="4c508-133">파일을 엽니다 **Views/Home/Index.cshtml**,이 사이트에 대 한 홈 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-133">Open the file at **Views/Home/Index.cshtml**, which is the home page for your site.</span></span> <span data-ttu-id="4c508-134">jumbotron 아래에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-134">Add the following code below the jumbotron.</span></span>

[!code-cshtml[Main](generating-views/samples/sample1.cshtml)]

<span data-ttu-id="4c508-135">ActionLink 메서드 첫 번째 매개 변수는 링크에 표시할 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-135">For the ActionLink method, the first parameter is the text to display in the link.</span></span> <span data-ttu-id="4c508-136">두 번째 매개 변수는 작업 및 세 번째 매개 변수는 컨트롤러의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-136">The second parameter is the action and the third parameter is the name of the controller.</span></span> <span data-ttu-id="4c508-137">예를 들어 첫 번째 링크 StudentsController 있는 인덱스 작업을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-137">For example, the first link points to the Index action in StudentsController.</span></span> <span data-ttu-id="4c508-138">실제 하이퍼링크는 다음이 값 중에서 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-138">The actual hyperlink is constructed from these values.</span></span> <span data-ttu-id="4c508-139">첫 번째 링크 궁극적으로 이동 하는 **Index.cshtml** 내에 파일이 **뷰/학생** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-139">The first link ultimately takes users to the **Index.cshtml** file within the **Views/Students** folder.</span></span>

## <a name="display-student-views"></a><span data-ttu-id="4c508-140">학생 보기 표시</span><span class="sxs-lookup"><span data-stu-id="4c508-140">Display student views</span></span>

<span data-ttu-id="4c508-141">프로젝트에 올바르게 추가 코드를 학습자의 목록을 표시 및 사용자가 편집 만들거나 데이터베이스에서 학생 레코드를 삭제할 수 있도록 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-141">You will verify that the code added to your project correctly displays a list of the students, and enables users to edit, create, or delete the student records in the database.</span></span>

<span data-ttu-id="4c508-142">마우스 오른쪽 단추로 클릭는 **Views/Home/Index.cshtml** 파일을 찾아 선택 **브라우저에서 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-142">Right-click the **Views/Home/Index.cshtml** file, and select **View in Browser**.</span></span> <span data-ttu-id="4c508-143">이 페이지에서는 학생 목록에 대 한 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-143">On this page, click the link for the list of students.</span></span>

![](generating-views/_static/image6.png)

<span data-ttu-id="4c508-144">이 페이지에서이 데이터를 수정 하는 학생 및 링크 목록을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-144">On this page, notice the list of the students and links to modify this data.</span></span>

![학생 목록](generating-views/_static/image7.png)

<span data-ttu-id="4c508-146">클릭는 **새로 만들기** 에 연결 하 고 새 학생에 대 한 일부 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-146">Click the **Create New** link and provide some values for a new student.</span></span>

![새 학생 만들기](generating-views/_static/image8.png)

<span data-ttu-id="4c508-148">클릭 **만들기**, 및 새 학생 목록에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-148">Click **Create**, and notice the new student is added to your list.</span></span>

![새 학생을 사용 하 여 목록](generating-views/_static/image9.png)

<span data-ttu-id="4c508-150">선택 된 **편집** 링크를 선택한 학생에 대 한 값 중 일부를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-150">Select the **Edit** link, and change some of the values for a student.</span></span>

![학생 편집](generating-views/_static/image10.png)

<span data-ttu-id="4c508-152">클릭 **저장**, 학생 레코드가 변경 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-152">Click **Save**, and notice the student record has been changed.</span></span>

<span data-ttu-id="4c508-153">마지막으로, 선택는 **삭제** 에 연결 하 고 확인을 클릭 하 여 레코드를 삭제 하는 **삭제** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-153">Finally, select the **Delete** link and confirm that you want to delete the record by clicking the **Delete** button.</span></span>

![학생을 삭제 합니다.](generating-views/_static/image11.png)

<span data-ttu-id="4c508-155">모든 코드를 작성 하지 않고도 학생 테이블의 데이터에 대 한 일반적인 작업을 수행 하는 뷰를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-155">Without writing any code, you have added views that perform common operations on the data in the Student table.</span></span>

<span data-ttu-id="4c508-156">필드에 대 한 텍스트 레이블을 데이터베이스 속성에 따라은 단어로 (같은 **LastName**) 되지 않습니다는 웹 페이지에 표시 하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-156">You may have noticed that the text label for a field is based on the database property (such as **LastName**) which is not necessarily what you want to display on the web page.</span></span> <span data-ttu-id="4c508-157">예를 들어 레이블이 되도록 할 수도 있습니다 **성**합니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-157">For example, you may prefer the label to be **Last Name**.</span></span> <span data-ttu-id="4c508-158">이 자습서의 뒷부분에 나오는이 디스플레이 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-158">You will fix this display issue later in the tutorial.</span></span>

## <a name="display-enrollment-views"></a><span data-ttu-id="4c508-159">등록 보기 표시</span><span class="sxs-lookup"><span data-stu-id="4c508-159">Display enrollment views</span></span>

<span data-ttu-id="4c508-160">데이터베이스에 학생과 등록 테이블 Course 및 등록 테이블 간의 일 대 다 관계 사이 일 대 다 관계에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-160">Your database includes a one-to-many relationship between the Student and Enrollment tables, and a one-to-many relationship between the Course and Enrollment tables.</span></span> <span data-ttu-id="4c508-161">등록에 대 한 보기 이러한 관계를 올바르게 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-161">The views for Enrollment correctly handle these relationships.</span></span> <span data-ttu-id="4c508-162">사이트 및 선택에 대 한 홈 페이지로 이동 하는 **등록 목록이** 링크 차례로 **새로 만들기** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-162">Navigate to the home page for your site and select the **List of enrollments** link and then the **Create New** link.</span></span> <span data-ttu-id="4c508-163">새 등록 레코드를 만들기 위한 폼에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-163">The view displays a form for creating a new enrollment record.</span></span> <span data-ttu-id="4c508-164">특히, 관련된 테이블의 값으로 채워진 두 드롭 다운 목록 폼에 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-164">In particular, notice that the form contains two drop-down lists that are populated with values from the related tables.</span></span>

![등록 만들기](generating-views/_static/image12.png)

<span data-ttu-id="4c508-166">또한 필드의 데이터 형식에 제공된 된 값의 유효성 검사는 따라 적용 자동으로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-166">Furthermore, validation of the provided values is automatically applied based on the data type of the field.</span></span> <span data-ttu-id="4c508-167">등급 호환 되지 않는 값을 제공 하려고 하면 오류 메시지가 보고서가 표시 되도록 숫자를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-167">Grade requires a number, so an error message is displayed if you try to provide an incompatible value.</span></span>

![유효성 검사 메시지](generating-views/_static/image13.png)

<span data-ttu-id="4c508-169">데이터베이스의 데이터로 작업 하는 사용자가 자동으로 생성 된 뷰를 사용 하면 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-169">You have verified that the automatically-generated views enable users to work with the data in the database.</span></span> <span data-ttu-id="4c508-170">이 시리즈의 다음 자습서에서는 데이터베이스를 업데이트 하 고 웹 응용 프로그램에서 해당 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c508-170">In the next tutorial in this series, you will update the database and make the corresponding changes in the web application.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="4c508-171">[이전](creating-the-web-application.md)
[다음](changing-the-database.md)</span><span class="sxs-lookup"><span data-stu-id="4c508-171">[Previous](creating-the-web-application.md)
[Next](changing-the-database.md)</span></span>
