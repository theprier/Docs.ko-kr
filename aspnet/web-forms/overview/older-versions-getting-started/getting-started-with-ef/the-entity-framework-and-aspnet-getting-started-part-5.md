---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
title: "먼저 Entity Framework 4.0 데이터베이스와 시작 및 ASP.NET 4 Web Forms-5 부 | Microsoft Docs"
author: tdykstra
description: "Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 샘플 응용 프로그램은..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/03/2010
ms.topic: article
ms.assetid: 24ad4379-3fb2-44dc-ba59-85fe0ffcb2ae
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
msc.type: authoredcontent
ms.openlocfilehash: 5efc5ff367d5da5df060eba0028399af898a69fa
ms.sourcegitcommit: 016f4d58663bcd442930227022de23fb3abee0b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2018
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-5"></a><span data-ttu-id="c998b-104">먼저 Entity Framework 4.0 데이터베이스와 시작 및 ASP.NET 4 Web Forms-5 부</span><span class="sxs-lookup"><span data-stu-id="c998b-104">Getting Started with Entity Framework 4.0 Database First and ASP.NET 4 Web Forms - Part 5</span></span>
====================
<span data-ttu-id="c998b-105">으로 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="c998b-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="c998b-106">Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 4.0 및 Visual Studio 2010을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-106">The Contoso University sample web application demonstrates how to create ASP.NET Web Forms applications using the Entity Framework 4.0 and Visual Studio 2010.</span></span> <span data-ttu-id="c998b-107">자습서 시리즈에 대 한 정보를 참조 하세요. [시리즈의 첫 번째 자습서](the-entity-framework-and-aspnet-getting-started-part-1.md)</span><span class="sxs-lookup"><span data-stu-id="c998b-107">For information about the tutorial series, see [the first tutorial in the series](the-entity-framework-and-aspnet-getting-started-part-1.md)</span></span>


## <a name="working-with-related-data-continued"></a><span data-ttu-id="c998b-108">데이터 관련된 작업을 계속</span><span class="sxs-lookup"><span data-stu-id="c998b-108">Working with Related Data, Continued</span></span>

<span data-ttu-id="c998b-109">이전 자습서에서 사용 하기 시작는 `EntityDataSource` 관련 데이터로 작업 하는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-109">In the previous tutorial you began to use the `EntityDataSource` control to work with related data.</span></span> <span data-ttu-id="c998b-110">프로젝트 관리자는 여러 수준의 계층을 표시 하 고이 정보를 탐색 속성의 데이터를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-110">You displayed multiple levels of hierarchy and edited data in navigation properties.</span></span> <span data-ttu-id="c998b-111">이 자습서에서는 계속 해 서 추가 하 고 관계를 삭제 하 고 기존 엔터티와 관계를 맺고 있는 새 엔터티를 추가 하 여 관련된 데이터와 함께 작동 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-111">In this tutorial you'll continue to work with related data by adding and deleting relationships and by adding a new entity that has a relationship to an existing entity.</span></span>

<span data-ttu-id="c998b-112">부서에 할당 된 과정을 추가 하는 페이지를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-112">You'll create a page that adds courses that are assigned to departments.</span></span> <span data-ttu-id="c998b-113">부서 이미 존재 하며, 새 과정을 만들 때 동시에 있습니다 수 간의 관계를 설정 하 고 기존 부서입니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-113">The departments already exist, and when you create a new course, at the same time you'll establish a relationship between it and an existing department.</span></span>

<span data-ttu-id="c998b-114">[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c998b-114">[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image1.png)</span></span>

<span data-ttu-id="c998b-115">또한 만들고 강사 (추가 선택 하는 두 엔터티 간의 관계) 과정을 할당 하 여 다 대 다 관계와 작동 하는 페이지 또는 강사 과정에서 제거 (두 엔터티 간의 관계를 제거 했는지 선택.)</span><span class="sxs-lookup"><span data-stu-id="c998b-115">You'll also create a page that works with a many-to-many relationship by assigning an instructor to a course (adding a relationship between two entities that you select) or removing an instructor from a course (removing a relationship between two entities that you select).</span></span> <span data-ttu-id="c998b-116">새 행에 추가 되 고 데이터베이스에서 강사 및 일련 간의 관계 추가 됩니다는 `CourseInstructor` 연결 테이블; 제거 관계에서 행을 삭제 하는 `CourseInstructor` 연관 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-116">In the database, adding a relationship between an instructor and a course results in a new row being added to the `CourseInstructor` association table; removing a relationship involves deleting a row from the `CourseInstructor` association table.</span></span> <span data-ttu-id="c998b-117">그러나 이렇게 하면 Entity framework에서를 참조 하지 않고 탐색 속성을 설정 하 여는 `CourseInstructor` 명시적으로 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-117">However, you do this in the Entity Framework by setting navigation properties, without referring to the `CourseInstructor` table explicitly.</span></span>

<span data-ttu-id="c998b-118">[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="c998b-118">[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image3.png)</span></span>

## <a name="adding-an-entity-with-a-relationship-to-an-existing-entity"></a><span data-ttu-id="c998b-119">관계가 있는 엔터티를 기존 엔터티에 추가</span><span class="sxs-lookup"><span data-stu-id="c998b-119">Adding an Entity with a Relationship to an Existing Entity</span></span>

<span data-ttu-id="c998b-120">라는 새 웹 페이지 생성 *CoursesAdd.aspx* 를 사용 하는 *Site.Master* 마스터 페이지, 다음 태그를 추가 하 고는 `Content` 라는 컨트롤 `Content2`:</span><span class="sxs-lookup"><span data-stu-id="c998b-120">Create a new web page named *CoursesAdd.aspx* that uses the *Site.Master* master page, and add the following markup to the `Content` control named `Content2`:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample1.aspx)]

<span data-ttu-id="c998b-121">이 태그를 만듭니다는 `EntityDataSource` 컨트롤을 선택 하는 과정을를 삽입할 수 있도록 하 고에 대 한 처리기를 지정 하는 `Inserting` 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-121">This markup creates an `EntityDataSource` control that selects courses, that enables inserting, and that specifies a handler for the `Inserting` event.</span></span> <span data-ttu-id="c998b-122">사용 하 여 처리기 업데이트는 `Department` 새 탐색 속성 `Course` 엔터티에 합니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-122">You'll use the handler to update the `Department` navigation property when a new `Course` entity is created.</span></span>

<span data-ttu-id="c998b-123">태그를 만듭니다는 `DetailsView` 새로 추가에 사용할 컨트롤 `Course` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c998b-123">The markup also creates a `DetailsView` control to use for adding new `Course` entities.</span></span> <span data-ttu-id="c998b-124">에 대 한 바인딩된 필드를 사용 하는 태그 `Course` 엔터티 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-124">The markup uses bound fields for `Course` entity properties.</span></span> <span data-ttu-id="c998b-125">입력 해야 하는 `CourseID` 아니므로이 시스템에서 생성 된 ID 필드 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-125">You have to enter the `CourseID` value because this is not a system-generated ID field.</span></span> <span data-ttu-id="c998b-126">만으로도 과정을 만들 때 수동으로 지정 해야 하는 과정 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-126">Instead, it's a course number that must be specified manually when the course is created.</span></span>

<span data-ttu-id="c998b-127">에 대 한 서식 파일 필드를 사용 하는 `Department` 탐색 속성으로 탐색 속성을 사용할 수 없으므로 `BoundField` 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-127">You use a template field for the `Department` navigation property because navigation properties cannot be used with `BoundField` controls.</span></span> <span data-ttu-id="c998b-128">서식 파일 필드 부서를 선택 하려면 드롭다운 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-128">The template field provides a drop-down list to select the department.</span></span> <span data-ttu-id="c998b-129">드롭다운 목록에 바인딩된는 `Departments` 엔터티를 사용 하 여 집합 `Eval` 대신 `Bind`, 다시 이므로 탐색 속성을 업데이트 하려면 직접 바인딩할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-129">The drop-down list is bound to the `Departments` entity set by using `Eval` rather than `Bind`, again because you cannot directly bind navigation properties in order to update them.</span></span> <span data-ttu-id="c998b-130">에 대 한 처리기를 지정 하면는 `DropDownList` 컨트롤의 `Init` 이벤트를 업데이트 하는 코드에서 사용할 컨트롤에 대 한 참조를 저장할 수 있도록는 `DepartmentID` 외래 키입니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-130">You specify a handler for the `DropDownList` control's `Init` event so that you can store a reference to the control for use by the code that updates the `DepartmentID` foreign key.</span></span>

<span data-ttu-id="c998b-131">*CoursesAdd.aspx.cs* partial 클래스 선언 바로 뒤 클래스 필드에 대 한 참조를 추가 하는 `DepartmentsDropDownList` 제어:</span><span class="sxs-lookup"><span data-stu-id="c998b-131">In *CoursesAdd.aspx.cs* just after the partial-class declaration, add a class field to hold a reference to the `DepartmentsDropDownList` control:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample2.cs)]

<span data-ttu-id="c998b-132">에 대 한 처리기를 추가 `DepartmentsDropDownList` 컨트롤의 `Init` 이벤트 컨트롤에 대 한 참조를 저장할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-132">Add a handler for the `DepartmentsDropDownList` control's `Init` event so that you can store a reference to the control.</span></span> <span data-ttu-id="c998b-133">이렇게 하면 사용자가 입력 값을 가져오고 업데이트 하는 데 사용할 수 있습니다는 `DepartmentID` 의 값은 `Course` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c998b-133">This lets you get the value the user has entered and use it to update the `DepartmentID` value of the `Course` entity.</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample3.cs)]

<span data-ttu-id="c998b-134">에 대 한 처리기를 추가 `DetailsView` 컨트롤의 `Inserting` 이벤트:</span><span class="sxs-lookup"><span data-stu-id="c998b-134">Add a handler for the `DetailsView` control's `Inserting` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample4.cs)]

<span data-ttu-id="c998b-135">사용자가 클릭할 때 `Insert`, `Inserting` 이벤트는 새 레코드를 삽입 하기 전에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-135">When the user clicks `Insert`, the `Inserting` event is raised before the new record is inserted.</span></span> <span data-ttu-id="c998b-136">처리기의 코드를 가져옵니다는 `DepartmentID` 에서 `DropDownList` 제어 하 고 사용 하 여에 사용할 값을 설정 하는 `DepartmentID` 의 속성은 `Course` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c998b-136">The code in the handler gets the `DepartmentID` from the `DropDownList` control and uses it to set the value that will be used for the `DepartmentID` property of the `Course` entity.</span></span>

<span data-ttu-id="c998b-137">이 과정에이 참여를 추가 하므로 Entity Framework는 `Courses` 탐색 속성은 연결 된 `Department` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c998b-137">The Entity Framework will take care of adding this course to the `Courses` navigation property of the associated `Department` entity.</span></span> <span data-ttu-id="c998b-138">또한 추가 하 고 부서는 `Department` 의 탐색 속성은 `Course` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c998b-138">It also adds the department to the `Department` navigation property of the `Course` entity.</span></span>

<span data-ttu-id="c998b-139">페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-139">Run the page.</span></span>

<span data-ttu-id="c998b-140">[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="c998b-140">[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image5.png)</span></span>

<span data-ttu-id="c998b-141">ID, 제목, 다양 한 크레딧, 입력 한 부서를 선택한 다음 클릭 **삽입**합니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-141">Enter an ID, a title, a number of credits, and select a department, then click **Insert**.</span></span>

<span data-ttu-id="c998b-142">실행 된 *Courses.aspx* 페이지 하 고 새 과정을 보려면 같은 동일 부서를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-142">Run the *Courses.aspx* page, and select the same department to see the new course.</span></span>

<span data-ttu-id="c998b-143">[![Image03](the-entity-framework-and-aspnet-getting-started-part-5/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="c998b-143">[![Image03](the-entity-framework-and-aspnet-getting-started-part-5/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image7.png)</span></span>

## <a name="working-with-many-to-many-relationships"></a><span data-ttu-id="c998b-144">다 대 다 관계 작업</span><span class="sxs-lookup"><span data-stu-id="c998b-144">Working with Many-to-Many Relationships</span></span>

<span data-ttu-id="c998b-145">간의 관계는 `Courses` 엔터티 집합 및 `People` 엔터티 집합은 다 대 다 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-145">The relationship between the `Courses` entity set and the `People` entity set is a many-to-many relationship.</span></span> <span data-ttu-id="c998b-146">A `Course` 엔터티 탐색 라는 속성이 `People` 0 개 이상의 관련 포함 될 수 있는 `Person` 엔터티 (해당 과정에 지정할 할당 강사를 나타냄).</span><span class="sxs-lookup"><span data-stu-id="c998b-146">A `Course` entity has a navigation property named `People` that can contain zero, one, or more related `Person` entities (representing instructors assigned to teach that course).</span></span> <span data-ttu-id="c998b-147">및 `Person` 엔터티 탐색 라는 속성이 `Courses` 0 개 이상의 관련 포함 될 수 있는 `Course` 엔터티 (courses 나타내는 해당 강사에 게 할당 된).</span><span class="sxs-lookup"><span data-stu-id="c998b-147">And a `Person` entity has a navigation property named `Courses` that can contain zero, one, or more related `Course` entities (representing courses that instructor is assigned to teach).</span></span> <span data-ttu-id="c998b-148">하나의 강사 여러 과정에 지정할 수 있습니다 및 한 과정으로 여러 강사 뿐만 아니라 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-148">One instructor might teach multiple courses, and one course might be taught by multiple instructors.</span></span> <span data-ttu-id="c998b-149">이 연습 섹션에서는 추가 하 고 간의 관계를 제거할 `Person` 및 `Course` 관련 엔터티의 탐색 속성을 업데이트 하 여 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c998b-149">In this section of the walkthrough, you'll add and remove relationships between `Person` and `Course` entities by updating the navigation properties of the related entities.</span></span>

<span data-ttu-id="c998b-150">라는 새 웹 페이지 생성 *InstructorsCourses.aspx* 를 사용 하는 *Site.Master* 마스터 페이지, 다음 태그를 추가 하 고는 `Content` 라는 컨트롤 `Content2`:</span><span class="sxs-lookup"><span data-stu-id="c998b-150">Create a new web page named *InstructorsCourses.aspx* that uses the *Site.Master* master page, and add the following markup to the `Content` control named `Content2`:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample5.aspx)]

<span data-ttu-id="c998b-151">이 태그를 만듭니다는 `EntityDataSource` 이름을 검색 하는 컨트롤 및 `PersonID` 의 `Person` 강사에 게 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c998b-151">This markup creates an `EntityDataSource` control that retrieves the name and `PersonID` of `Person` entities for instructors.</span></span> <span data-ttu-id="c998b-152">A `DropDrownList` 컨트롤이 바인딩되는 `EntityDataSource` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-152">A `DropDrownList` control is bound to the `EntityDataSource` control.</span></span> <span data-ttu-id="c998b-153">`DropDownList` 컨트롤에 대 한 처리기를 지정 된 `DataBound` 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-153">The `DropDownList` control specifies a handler for the `DataBound` event.</span></span> <span data-ttu-id="c998b-154">과정을 표시 하는 두 개의 databind 드롭 다운 목록에이 처리기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-154">You'll use this handler to databind the two drop-down lists that display courses.</span></span>

<span data-ttu-id="c998b-155">태그는 또한 과정 선택한 강사를 할당 하는 데 사용할 수 있는 컨트롤의 다음 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-155">The markup also creates the following group of controls to use for assigning a course to the selected instructor:</span></span>

- <span data-ttu-id="c998b-156">A `DropDownList` 할당 하는 과정을 선택 하기 위한 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-156">A `DropDownList` control for selecting a course to assign.</span></span> <span data-ttu-id="c998b-157">이 컨트롤은 선택한 강사에 현재 할당 되지 않은 과정으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-157">This control will be populated with courses that are currently not assigned to the selected instructor.</span></span>
- <span data-ttu-id="c998b-158">A `Button` 할당을 시작 하는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-158">A `Button` control to initiate the assignment.</span></span>
- <span data-ttu-id="c998b-159">A `Label` 컨트롤에는 할당은 실패 하는 경우 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-159">A `Label` control to display an error message if the assignment fails.</span></span>

<span data-ttu-id="c998b-160">마지막으로, 태그는 또한 선택한 강사에서 제거 하는 과정에 대해 사용할 수 있는 컨트롤의 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-160">Finally, the markup also creates a group of controls to use for removing a course from the selected instructor.</span></span>

<span data-ttu-id="c998b-161">*InstructorsCourses.aspx.cs*를 사용 하는 추가 문:</span><span class="sxs-lookup"><span data-stu-id="c998b-161">In *InstructorsCourses.aspx.cs*, add a using statement:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample6.cs)]

<span data-ttu-id="c998b-162">과정을 표시 하는 두 드롭다운 목록을 채우는 데 사용 하는 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-162">Add a method for populating the two drop-down lists that display courses:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample7.cs)]

<span data-ttu-id="c998b-163">이 코드는 모든 과정에서 가져옵니다는 `Courses` 엔터티 집합과 과정을 가져옵니다는 `Courses` 의 탐색 속성은 `Person` 선택한 강사에 대 한 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c998b-163">This code gets all courses from the `Courses` entity set and gets the courses from the `Courses` navigation property of the `Person` entity for the selected instructor.</span></span> <span data-ttu-id="c998b-164">그런 다음 해당 강사에 할당 되는 과정을 결정 하 고 그에 따라 드롭 다운 목록을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-164">It then determines which courses are assigned to that instructor and populates the drop-down lists accordingly.</span></span>

<span data-ttu-id="c998b-165">에 대 한 처리기를 추가 `Assign` 단추의 `Click` 이벤트:</span><span class="sxs-lookup"><span data-stu-id="c998b-165">Add a handler for the `Assign` button's `Click` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample8.cs)]

<span data-ttu-id="c998b-166">이 코드는 `Person` 선택한 강사에 대 한 엔터티를 가져옵니다는 `Course` 선택한 과정에 대 한 엔터티 추가 선택 된 과정에 참여 하는 `Courses` 강의의 탐색 속성 `Person` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c998b-166">This code gets the `Person` entity for the selected instructor, gets the `Course` entity for the selected course, and adds the selected course to the `Courses` navigation property of the instructor's `Person` entity.</span></span> <span data-ttu-id="c998b-167">다음 데이터베이스에 변경 내용을 저장 하 고 결과 즉시 볼 수 있도록 드롭 다운 목록을 다시 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-167">It then saves the changes to the database and repopulates the drop-down lists so the results can be seen immediately.</span></span>

<span data-ttu-id="c998b-168">에 대 한 처리기를 추가 `Remove` 단추의 `Click` 이벤트:</span><span class="sxs-lookup"><span data-stu-id="c998b-168">Add a handler for the `Remove` button's `Click` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample9.cs)]

<span data-ttu-id="c998b-169">이 코드는 `Person` 선택한 강사에 대 한 엔터티를 가져옵니다는 `Course` 선택한 과정에 대 한 엔터티 선택한 과정에서 제거 하 고는 `Person` 엔터티의 `Courses` 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-169">This code gets the `Person` entity for the selected instructor, gets the `Course` entity for the selected course, and removes the selected course from the `Person` entity's `Courses` navigation property.</span></span> <span data-ttu-id="c998b-170">다음 데이터베이스에 변경 내용을 저장 하 고 결과 즉시 볼 수 있도록 드롭 다운 목록을 다시 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-170">It then saves the changes to the database and repopulates the drop-down lists so the results can be seen immediately.</span></span>

<span data-ttu-id="c998b-171">코드를 추가 하는 `Page_Load` 없음 오류를 보고에 대 한 처리기를 추가 하는 메서드를 사용 하면 오류 메시지가 표시 되지 않습니다는 `DataBound` 및 `SelectedIndexChanged` courses 드롭 다운 목록을 채우는 데 강사 드롭 다운 목록의 이벤트:</span><span class="sxs-lookup"><span data-stu-id="c998b-171">Add code to the `Page_Load` method that makes sure the error messages are not visible when there's no error to report, and add handlers for the `DataBound` and `SelectedIndexChanged` events of the instructors drop-down list to populate the courses drop-down lists:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample10.cs)]

<span data-ttu-id="c998b-172">페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-172">Run the page.</span></span>

<span data-ttu-id="c998b-173">[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="c998b-173">[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image9.png)</span></span>

<span data-ttu-id="c998b-174">강사를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-174">Select an instructor.</span></span> <span data-ttu-id="c998b-175">**과정 할당** 드롭다운 목록에서 강사 설명 하지 않는 하는 강의 표시 됩니다 및 **제거 과정** 드롭다운 목록에서 강사에 이미 할당 되어 있는 강의 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-175">The **Assign a Course** drop-down list displays the courses that the instructor doesn't teach, and the **Remove a Course** drop-down list displays the courses that the instructor is already assigned to.</span></span> <span data-ttu-id="c998b-176">에 **과정 할당** 섹션 과정을 선택한 다음 클릭 **할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-176">In the **Assign a Course** section, select a course and then click **Assign**.</span></span> <span data-ttu-id="c998b-177">과정을 이동는 **제거 과정** 드롭 다운 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-177">The course moves to the **Remove a Course** drop-down list.</span></span> <span data-ttu-id="c998b-178">과정 선택는 **제거 과정** 섹션 및 클릭 **제거 * * * 합니다.*</span><span class="sxs-lookup"><span data-stu-id="c998b-178">Select a course in the **Remove a Course** section and click **Remove***.*</span></span> <span data-ttu-id="c998b-179">과정을 이동는 **과정 할당** 드롭 다운 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-179">The course moves to the **Assign a Course** drop-down list.</span></span>

<span data-ttu-id="c998b-180">관련된 데이터에 사용할 수 있는 몇 가지 다른 방법을 살펴 보았습니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-180">You have now seen some more ways to work with related data.</span></span> <span data-ttu-id="c998b-181">다음 자습서에서는 응용 프로그램의 관리 효율을 개선 하기 위해 데이터 모델에서 상속을 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c998b-181">In the following tutorial, you'll learn how to use inheritance in the data model to improve the maintainability of your application.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="c998b-182">[이전](the-entity-framework-and-aspnet-getting-started-part-4.md)
[다음](the-entity-framework-and-aspnet-getting-started-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="c998b-182">[Previous](the-entity-framework-and-aspnet-getting-started-part-4.md)
[Next](the-entity-framework-and-aspnet-getting-started-part-6.md)</span></span>
