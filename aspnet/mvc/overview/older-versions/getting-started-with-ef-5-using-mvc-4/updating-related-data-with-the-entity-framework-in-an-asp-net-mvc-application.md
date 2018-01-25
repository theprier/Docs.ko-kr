---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: "(6 / 10) ASP.NET MVC 응용 프로그램에서 Entity Framework와 관련된 데이터를 업데이트 합니다. | Microsoft Docs"
author: tdykstra
description: "Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/30/2013
ms.topic: article
ms.assetid: 7871dc05-2750-470f-8b4c-3a52511949bc
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 2ca76364a2e9a71dc92644bd579345ae3c304a69
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="updating-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-6-of-10"></a><span data-ttu-id="6f675-103">(6 / 10) ASP.NET MVC 응용 프로그램에서 Entity Framework와 관련된 데이터를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-103">Updating Related Data with the Entity Framework in an ASP.NET MVC Application (6 of 10)</span></span>
====================
<span data-ttu-id="6f675-104">으로 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="6f675-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="6f675-105">완료 된 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-105">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="6f675-106">Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio 2012를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="6f675-107">자습서 시리즈에 대 한 정보를 참조 하십시오. [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="6f675-108">시작 부분에서 자습서 시리즈를 시작할 수 있습니다 또는 [이 장의 대 한 시작 프로젝트 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 여기에서 시작 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="6f675-109">해결할 수 없는 문제에 직면 하는 경우 [완료 장 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 문제를 재현 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="6f675-110">일반적으로 코드 완성 된 코드를 비교 하 여 문제에 솔루션을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="6f675-111">몇 가지 일반적인 오류 및 해결 하는 방법에 대 한 참조 [오류 및 해결 방법입니다.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span><span class="sxs-lookup"><span data-stu-id="6f675-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>


<span data-ttu-id="6f675-112">관련된 데이터; 이전 자습서에서 표시 이 자습서에서는 관련된 데이터를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-112">In the previous tutorial you displayed related data; in this tutorial you'll update related data.</span></span> <span data-ttu-id="6f675-113">대부분의 관계에 대 한 적절 한 외래 키 필드를 업데이트 하 여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-113">For most relationships, this can be done by updating the appropriate foreign key fields.</span></span> <span data-ttu-id="6f675-114">다 대 다 관계에 대 한 Entity Framework 노출 되는 것 조인 테이블을 직접 하므로 명시적으로 추가 하 고 엔터티 하 고 해당 탐색 속성에서 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-114">For many-to-many relationships, the Entity Framework doesn't expose the join table directly, so you must explicitly add and remove entities to and from the appropriate navigation properties.</span></span>

<span data-ttu-id="6f675-115">다음 그림에서는 보여 페이지와 협력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-115">The following illustrations show the pages that you'll work with.</span></span>

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="customize-the-create-and-edit-pages-for-courses"></a><span data-ttu-id="6f675-118">교육 과정에 대 한 만들기 및 편집 페이지를 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="6f675-118">Customize the Create and Edit Pages for Courses</span></span>

<span data-ttu-id="6f675-119">새 과목 엔터티를 만들 때 기존 부서에는 관계가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-119">When a new course entity is created, it must have a relationship to an existing department.</span></span> <span data-ttu-id="6f675-120">이 작업을 위해 스 캐 폴드 코드에는 컨트롤러 메서드 및 부서를 선택 하기 위한 드롭 다운 목록을 포함 하는 뷰 만들기 및 편집 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-120">To facilitate this, the scaffolded code includes controller methods and Create and Edit views that include a drop-down list for selecting the department.</span></span> <span data-ttu-id="6f675-121">드롭다운 목록에서 집합은 `Course.DepartmentID` 외래 키 속성 및 Entity Framework를 로드 하는 데 필요한 모든는 `Department` 는 적절 한 탐색 속성 `Department` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="6f675-121">The drop-down list sets the `Course.DepartmentID` foreign key property, and that's all the Entity Framework needs in order to load the `Department` navigation property with the appropriate `Department` entity.</span></span> <span data-ttu-id="6f675-122">스 캐 폴드 코드를 사용 하지만 오류 처리를 추가 하 고 드롭 다운 목록을 정렬 하도록 약간 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-122">You'll use the scaffolded code, but change it slightly to add error handling and sort the drop-down list.</span></span>

<span data-ttu-id="6f675-123">*CourseController.cs*, 4 개의 삭제 `Edit` 및 `Create` 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-123">In *CourseController.cs*, delete the four `Edit` and `Create` methods and replace them with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,10,13-14,21-27,34,41,44-45,52-58,62-68)]

<span data-ttu-id="6f675-124">`PopulateDepartmentsDropDownList` 메서드 이름을 기준으로 정렬 하는 모든 부서의 목록을 가져옵니다, 만듭니다는 `SelectList` 드롭 다운 목록에 대 한 컬렉션 뷰 컬렉션을 전달 하 고는 `ViewBag` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-124">The `PopulateDepartmentsDropDownList` method gets a list of all departments sorted by name, creates a `SelectList` collection for a drop-down list, and passes the collection to the view in a `ViewBag` property.</span></span> <span data-ttu-id="6f675-125">메서드에 선택적 `selectedDepartment` 드롭 다운 목록에서 렌더링 될 때 선택 항목을 지정 하는 호출 코드를 허용 하는 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-125">The method accepts the optional `selectedDepartment` parameter that allows the calling code to specify the item that will be selected when the drop-down list is rendered.</span></span> <span data-ttu-id="6f675-126">뷰 이름을 전달 됩니다 `DepartmentID` 를 [는 `DropDownList` 도우미](../working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md), 도우미를 찾는 다음 알고는 `ViewBag` 개체에 대 한는 `SelectList` 라는 `DepartmentID`합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-126">The view will pass the name `DepartmentID` to [the `DropDownList` helper](../working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md), and the helper then knows to look in the `ViewBag` object for a `SelectList` named `DepartmentID`.</span></span>

<span data-ttu-id="6f675-127">`HttpGet` `Create` 메서드 호출의 `PopulateDepartmentsDropDownList` 새 과정에 대 한 부서 설정 되지 않으며 아직 때문에 선택한 항목을 설정 하지 않고 메서드:</span><span class="sxs-lookup"><span data-stu-id="6f675-127">The `HttpGet` `Create` method calls the `PopulateDepartmentsDropDownList` method without setting the selected item, because for a new course the department is not established yet:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="6f675-128">`HttpGet` `Edit` 메서드 편집 중인 과정에 이미 할당 되어 있는 분야의 ID에 따라 선택한 항목을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-128">The `HttpGet` `Edit` method sets the selected item, based on the ID of the department that is already assigned to the course being edited:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

<span data-ttu-id="6f675-129">`HttpPost` 메서드 모두에 대 한 `Create` 및 `Edit` 도 오류가 발생 한 후 페이지를 다시 표시 될 때 선택한 항목을 설정 하는 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-129">The `HttpPost` methods for both `Create` and `Edit` also include code that sets the selected item when they redisplay the page after an error:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="6f675-130">이 코드는 오류 메시지를 표시 하기 페이지 다시 표시 됩니다 때 어떤 부서 선택한 선택 된 상태로 유지 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-130">This code ensures that when the page is redisplayed to show the error message, whatever department was selected stays selected.</span></span>

<span data-ttu-id="6f675-131">*Views\Course\Create.cshtml*, 강조 표시 된 코드를 추가 하기 전에 새 과정 숫자 필드를 만들어는 **제목** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-131">In *Views\Course\Create.cshtml*, add the highlighted code to create a new course number field before the **Title** field.</span></span> <span data-ttu-id="6f675-132">기본적으로 기본 키 필드가 아닌 스 캐 폴드 된 이전 자습서에서 설명 했 듯이 하지만이 기본 키 이므로 의미 있는 사용자 키 값을 입력할 수 있게 하려면 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-132">As explained in an earlier tutorial, primary key fields aren't scaffolded by default, but this primary key is meaningful, so you want the user to be able to enter the key value.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=17-23)]

<span data-ttu-id="6f675-133">*Views\Course\Edit.cshtml*, *Views\Course\Delete.cshtml*, 및 *Views\Course\Details.cshtml*를 추가 하기 전에 과정 숫자 필드는 **제목**  필드입니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-133">In *Views\Course\Edit.cshtml*, *Views\Course\Delete.cshtml*, and *Views\Course\Details.cshtml*, add a course number field before the **Title** field.</span></span> <span data-ttu-id="6f675-134">기본 키 이기 때문에 표시 되지만 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-134">Because it's the primary key, it's displayed, but it can't be changed.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

<span data-ttu-id="6f675-135">실행의 **만들기** 페이지 (과정 인덱스 페이지를 표시 하 고 클릭 **새로 만들기**) 새 과정에 대 한 데이터를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-135">Run the **Create** page (display the Course Index page and click **Create New**) and enter data for a new course:</span></span>

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

<span data-ttu-id="6f675-137">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-137">Click **Create**.</span></span> <span data-ttu-id="6f675-138">과정 인덱스 페이지가 목록에 추가 된 새 과정으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-138">The Course Index page is displayed with the new course added to the list.</span></span> <span data-ttu-id="6f675-139">인덱스 페이지 목록에 있는 부서 이름과 관계가 올바르게 설정 되었는지 표시 하는 탐색 속성에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-139">The department name in the Index page list comes from the navigation property, showing that the relationship was established correctly.</span></span>

![Course_Index_page_showing_new_course](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="6f675-141">실행 된 **편집** 페이지 (과정 인덱스 페이지를 표시 하 고 클릭 **편집** 는 과정에).</span><span class="sxs-lookup"><span data-stu-id="6f675-141">Run the **Edit** page (display the Course Index page and click **Edit** on a course).</span></span>

![Course_edit_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

<span data-ttu-id="6f675-143">페이지에서 데이터를 변경 하 고 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-143">Change data on the page and click **Save**.</span></span> <span data-ttu-id="6f675-144">과정 인덱스 페이지가 업데이트 과정 데이터와 함께 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-144">The Course Index page is displayed with the updated course data.</span></span>

## <a name="adding-an-edit-page-for-instructors"></a><span data-ttu-id="6f675-145">강사에 대 한 편집 페이지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-145">Adding an Edit Page for Instructors</span></span>

<span data-ttu-id="6f675-146">강사 레코드를 편집할 때 강의 사무실 할당을 업데이트할 수 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-146">When you edit an instructor record, you want to be able to update the instructor's office assignment.</span></span> <span data-ttu-id="6f675-147">`Instructor` 엔터티 간의 관계가 0 또는 1을 하나는 `OfficeAssignment` 엔터티는 다음과 같은 경우를 처리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-147">The `Instructor` entity has a one-to-zero-or-one relationship with the `OfficeAssignment` entity, which means you must handle the following situations:</span></span>

- <span data-ttu-id="6f675-148">사용자 선택을 사무실 할당을 취소 하는 경우 원래 값을 제거 하 고 삭제 해야 합니다는 `OfficeAssignment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="6f675-148">If the user clears the office assignment and it originally had a value, you must remove and delete the `OfficeAssignment` entity.</span></span>
- <span data-ttu-id="6f675-149">사용자가 office 할당 값을 입력 하 고 원래 비어 있던 경우 새 만들어 해야 `OfficeAssignment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="6f675-149">If the user enters an office assignment value and it originally was empty, you must create a new `OfficeAssignment` entity.</span></span>
- <span data-ttu-id="6f675-150">기존 값을 변경 해야 사용자가 사무실 할당의 값을 변경 해도 경우 `OfficeAssignment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="6f675-150">If the user changes the value of an office assignment, you must change the value in an existing `OfficeAssignment` entity.</span></span>

<span data-ttu-id="6f675-151">열기 *InstructorController.cs* 살펴보세요는 `HttpGet` `Edit` 메서드:</span><span class="sxs-lookup"><span data-stu-id="6f675-151">Open *InstructorController.cs* and look at the `HttpGet` `Edit` method:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

<span data-ttu-id="6f675-152">여기에 스 캐 폴드 코드 원하는 결과가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-152">The scaffolded code here isn't what you want.</span></span> <span data-ttu-id="6f675-153">데이터를 설정할 수 있지만 드롭 다운 목록에 대 한 텍스트 상자 방법이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-153">It's setting up data for a drop-down list, but you what you need is a text box.</span></span> <span data-ttu-id="6f675-154">이 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-154">Replace this method with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="6f675-155">이 코드는 `ViewBag` 문을 즉시 로드 관련 된 추가 `OfficeAssignment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="6f675-155">This code drops the `ViewBag` statement and adds eager loading for the associated `OfficeAssignment` entity.</span></span> <span data-ttu-id="6f675-156">즉시 로드를 수행할 수 없습니다는 `Find` 메서드를 하므로 `Where` 및 `Single` 메서드가 강의 선택 하려면 대신 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-156">You can't perform eager loading with the `Find` method, so the `Where` and `Single` methods are used instead to select the instructor.</span></span>

<span data-ttu-id="6f675-157">대체는 `HttpPost` `Edit` 메서드를 다음 코드로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-157">Replace the `HttpPost` `Edit` method with the following code.</span></span> <span data-ttu-id="6f675-158">office 할당 업데이트를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-158">which handles office assignment updates:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="6f675-159">코드는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-159">The code does the following:</span></span>

- <span data-ttu-id="6f675-160">현재 가져옵니다 `Instructor` 에 대 한 즉시 로드를 사용 하 여 데이터베이스에서 엔터티는 `OfficeAssignment` 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-160">Gets the current `Instructor` entity from the database using eager loading for the `OfficeAssignment` navigation property.</span></span> <span data-ttu-id="6f675-161">이에서 수행한 것과 동일는 `HttpGet` `Edit` 메서드.</span><span class="sxs-lookup"><span data-stu-id="6f675-161">This is the same as what you did in the `HttpGet` `Edit` method.</span></span>
- <span data-ttu-id="6f675-162">검색 된 업데이트 `Instructor` 엔터티 모델 바인더의 값으로.</span><span class="sxs-lookup"><span data-stu-id="6f675-162">Updates the retrieved `Instructor` entity with values from the model binder.</span></span> <span data-ttu-id="6f675-163">[TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) 사용 된 오버 로드를 사용 하면 *화이트 리스트* 포함할 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-163">The [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) overload used enables you to *whitelist* the properties you want to include.</span></span> <span data-ttu-id="6f675-164">이렇게 하면 과도 하 게 게시에 설명 된 대로 [두 번째 자습서](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-164">This prevents over-posting, as explained in [the second tutorial](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md).</span></span>

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]
- <span data-ttu-id="6f675-165">사무실 위치 비어 있으면 설정 하는 `Instructor.OfficeAssignment` 속성을 null로 되도록 관련된 행에는 `OfficeAssignment` 테이블은 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-165">If the office location is blank, sets the `Instructor.OfficeAssignment` property to null so that the related row in the `OfficeAssignment` table will be deleted.</span></span>

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]
- <span data-ttu-id="6f675-166">데이터베이스에 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-166">Saves the changes to the database.</span></span>

<span data-ttu-id="6f675-167">*Views\Instructor\Edit.cshtml*이후에 `div` 에 대 한 요소는 **Hire Date** 필드를 사무실 위치를 편집 하기 위해 새 필드 추가:</span><span class="sxs-lookup"><span data-stu-id="6f675-167">In *Views\Instructor\Edit.cshtml*, after the `div` elements for the **Hire Date** field, add a new field for editing the office location:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml)]

<span data-ttu-id="6f675-168">페이지 실행 (선택 된 **강사** 탭을 클릭 한 다음 **편집** 강사에).</span><span class="sxs-lookup"><span data-stu-id="6f675-168">Run the page (select the **Instructors** tab and then click **Edit** on an instructor).</span></span> <span data-ttu-id="6f675-169">변경 된 **사무실 위치** 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-169">Change the **Office Location** and click **Save**.</span></span>

![Changing_the_office_location](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

## <a name="adding-course-assignments-to-the-instructor-edit-page"></a><span data-ttu-id="6f675-171">강사에 대 한 추가 과정 할당 편집 페이지</span><span class="sxs-lookup"><span data-stu-id="6f675-171">Adding Course Assignments to the Instructor Edit Page</span></span>

<span data-ttu-id="6f675-172">강사는 courses 개수에 관계 없이 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-172">Instructors may teach any number of courses.</span></span> <span data-ttu-id="6f675-173">이제 다음 스크린 샷에 표시 된 것 처럼 확인란 그룹을 사용 하는 과정 할당을 변경 하는 기능을 추가 하 여 강사 편집 페이지를 향상 시켜:</span><span class="sxs-lookup"><span data-stu-id="6f675-173">Now you'll enhance the Instructor Edit page by adding the ability to change course assignments using a group of check boxes, as shown in the following screen shot:</span></span>

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="6f675-175">간의 관계는 `Course` 및 `Instructor` 은 다 대 다 조인 테이블에 직접 액세스할 수 없는 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-175">The relationship between the `Course` and `Instructor` entities is many-to-many, which means you do not have direct access to the join table.</span></span> <span data-ttu-id="6f675-176">대신 추가 하 고에서 엔터티를 제거는 `Instructor.Courses` 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-176">Instead, you will add and remove entities to and from the `Instructor.Courses` navigation property.</span></span>

<span data-ttu-id="6f675-177">과정을 변경할 수 있도록 하는 UI 강사는은 확인란의 그룹에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-177">The UI that enables you to change which courses an instructor is assigned to is a group of check boxes.</span></span> <span data-ttu-id="6f675-178">데이터베이스의 모든 과정에 대 한 확인란이 표시 되 고 강사에 현재 할당 되어 있는 것을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-178">A check box for every course in the database is displayed, and the ones that the instructor is currently assigned to are selected.</span></span> <span data-ttu-id="6f675-179">사용자가 선택 하거나 과정 할당을 변경 하려면 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-179">The user can select or clear check boxes to change course assignments.</span></span> <span data-ttu-id="6f675-180">Courses 수가 된 훨씬 큰을 뷰에서 데이터를 제공 합니다. 다른 방법을 사용 하 고 싶을 것 하지만 관계 만들기 또는 삭제 하려면 탐색 속성을 조작 하는 동일한 방법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-180">If the number of courses were much greater, you would probably want to use a different method of presenting the data in the view, but you'd use the same method of manipulating navigation properties in order to create or delete relationships.</span></span>

<span data-ttu-id="6f675-181">확인란 목록 보기에는 데이터를 제공 하려면 보기 모델 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-181">To provide data to the view for the list of check boxes, you'll use a view model class.</span></span> <span data-ttu-id="6f675-182">만들 *AssignedCourseData.cs* 에 *Viewmodel* 폴더와 기존 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-182">Create *AssignedCourseData.cs* in the *ViewModels* folder and replace the existing code with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

<span data-ttu-id="6f675-183">*InstructorController.cs*, 대체 된 `HttpGet` `Edit` 메서드를 다음 코드로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-183">In *InstructorController.cs*, replace the `HttpGet` `Edit` method with the following code.</span></span> <span data-ttu-id="6f675-184">변경 내용은 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-184">The changes are highlighted.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=5,8,12-27)]

<span data-ttu-id="6f675-185">에 대 한 즉시 로드를 추가 하는 코드는 `Courses` 탐색 속성 새 호출 `PopulateAssignedCourseData` 메서드를 사용 하 여 확인란 배열에 대 한 정보를 제공는 `AssignedCourseData` 모델 클래스를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-185">The code adds eager loading for the `Courses` navigation property and calls the new `PopulateAssignedCourseData` method to provide information for the check box array using the `AssignedCourseData` view model class.</span></span>

<span data-ttu-id="6f675-186">코드는 `PopulateAssignedCourseData` 메서드를 모두 읽습니다 `Course` 보기를 사용 하는 과정의 목록을 로드 하기 위해 엔터티 모델 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-186">The code in the `PopulateAssignedCourseData` method reads through all `Course` entities in order to load a list of courses using the view model class.</span></span> <span data-ttu-id="6f675-187">각 과정에 대 한 코드 과정 강의에 있는지 여부를 확인 `Courses` 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-187">For each course, the code checks whether the course exists in the instructor's `Courses` navigation property.</span></span> <span data-ttu-id="6f675-188">효율적인 조회를 만들려면 과정에서 강사에 할당 되었는지 여부를 확인할 때 강사에 할당 하는 과정에 저장 됩니다는 [HashSet](https://msdn.microsoft.com/library/bb359438.aspx) 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-188">To create efficient lookup when checking whether a course is assigned to the instructor, the courses assigned to the instructor are put into a [HashSet](https://msdn.microsoft.com/library/bb359438.aspx) collection.</span></span> <span data-ttu-id="6f675-189">`Assigned` 속성이 `true` courses 강사 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-189">The `Assigned` property is set to `true` for courses the instructor is assigned.</span></span> <span data-ttu-id="6f675-190">보기 선택 상자로 표시 되어야 하는 확인을 확인 하려면이 속성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-190">The view will use this property to determine which check boxes must be displayed as selected.</span></span> <span data-ttu-id="6f675-191">목록 보기에 전달 되는 마지막으로, 한 `ViewBag` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-191">Finally, the list is passed to the view in a `ViewBag` property.</span></span>

<span data-ttu-id="6f675-192">다음으로, 사용자가 클릭할 때 실행 되는 코드를 추가 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-192">Next, add the code that's executed when the user clicks **Save**.</span></span> <span data-ttu-id="6f675-193">대체는 `HttpPost` `Edit` 메서드를 업데이트 하는 새 메서드를 호출 하는 다음 코드로 `Courses` 의 탐색 속성은 `Instructor` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="6f675-193">Replace the `HttpPost` `Edit` method with the following code, which calls a new method that updates the `Courses` navigation property of the `Instructor` entity.</span></span> <span data-ttu-id="6f675-194">변경 내용은 강조 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-194">The changes are highlighted.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs?highlight=3,7,20,33,37-65)]

<span data-ttu-id="6f675-195">보기의 컬렉션인 없으므로 `Course` 엔터티, 모델 바인더 자동으로 업데이트할 수는 `Courses` 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-195">Since the view doesn't have a collection of `Course` entities, the model binder can't automatically update the `Courses` navigation property.</span></span> <span data-ttu-id="6f675-196">Courses 탐색 속성을 업데이트 하려면 모델 바인더를 사용 하는 대신 작업입니다 새 `UpdateInstructorCourses` 메서드.</span><span class="sxs-lookup"><span data-stu-id="6f675-196">Instead of using the model binder to update the Courses navigation property, you'll do that in the new `UpdateInstructorCourses` method.</span></span> <span data-ttu-id="6f675-197">따라서 제외 해야는 `Courses` 모델 바인딩에서 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-197">Therefore you need to exclude the `Courses` property from model binding.</span></span> <span data-ttu-id="6f675-198">호출 하는 코드를 변경 하지 않아도이 [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) 사용 중 이므로 *허용 목록이* 오버 로드 및 `Courses` include 목록에 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-198">This doesn't require any change to the code that calls [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) because you're using the *whitelisting* overload and `Courses` isn't in the include list.</span></span>

<span data-ttu-id="6f675-199">경우 없는 확인란이 선택 된을의 코드 `UpdateInstructorCourses` 초기화는 `Courses` 는 빈 컬렉션 탐색 속성:</span><span class="sxs-lookup"><span data-stu-id="6f675-199">If no check boxes were selected, the code in `UpdateInstructorCourses` initializes the `Courses` navigation property with an empty collection:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

<span data-ttu-id="6f675-200">코드 다음 데이터베이스의 모든 과정을 반복 하 고 각 과목와 보기에서 선택 된 강사에 현재 할당 된 것에 대해 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-200">The code then loops through all courses in the database and checks each course against the ones currently assigned to the instructor versus the ones that were selected in the view.</span></span> <span data-ttu-id="6f675-201">두 번째 컬렉션에 저장 된 효율적인 조회를 쉽게 `HashSet` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-201">To facilitate efficient lookups, the latter two collections are stored in `HashSet` objects.</span></span>

<span data-ttu-id="6f675-202">과정에 대 한 확인란을 선택 했지만 과정에 없는 경우는 `Instructor.Courses` 탐색 속성 과정 탐색 속성의 컬렉션에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-202">If the check box for a course was selected but the course isn't in the `Instructor.Courses` navigation property, the course is added to the collection in the navigation property.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

<span data-ttu-id="6f675-203">과정에 대 한 확인란 선택 되지 않은 과정에 속하지만 `Instructor.Courses` 과정 탐색 속성이 탐색 속성에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-203">If the check box for a course wasn't selected, but the course is in the `Instructor.Courses` navigation property, the course is removed from the navigation property.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

<span data-ttu-id="6f675-204">*Views\Instructor\Edit.cshtml*, 추가 **Courses** 강조 표시 하는 다음을 추가 하 여 확인란의 배열을 사용 하 여 필드 바로 다음 코드는 `div` 에 대 한 요소는 `OfficeAssignment` 필드:</span><span class="sxs-lookup"><span data-stu-id="6f675-204">In *Views\Instructor\Edit.cshtml*, add a **Courses** field with an array of check boxes by adding the following highlighted code immediately after the `div` elements for the `OfficeAssignment` field:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml?highlight=51-73)]

<span data-ttu-id="6f675-205">이 코드는 세 개의 열이 있는 HTML 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-205">This code creates an HTML table that has three columns.</span></span> <span data-ttu-id="6f675-206">각 열에는 확인란이 과정 번호 및 제목으로 구성 된 캡션 뒤 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-206">In each column is a check box followed by a caption that consists of the course number and title.</span></span> <span data-ttu-id="6f675-207">모든 확인란 있어야 그룹으로 처리 해야 하는 모델 바인더에 게 동일한 이름 ("selectedCourses").</span><span class="sxs-lookup"><span data-stu-id="6f675-207">The check boxes all have the same name ("selectedCourses"), which informs the model binder that they are to be treated as a group.</span></span> <span data-ttu-id="6f675-208">`value` 각 확인란의 특성의 값으로 설정 되어 `CourseID.` 모델 바인더 구성 된 컨트롤러에 배열을 전달 페이지가 게시 될 때는 `CourseID` 확인란만 선택 되에 대 한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-208">The `value` attribute of each check box is set to the value of `CourseID.` When the page is posted, the model binder passes an array to the controller that consists of the `CourseID` values for only the check boxes which are selected.</span></span>

<span data-ttu-id="6f675-209">강사에 할당 하는 과정에 사용 되는 것이 확인란은 처음 렌더링 됩니다 때 사용할 `checked` 특성 (에 확인 표시)을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-209">When the check boxes are initially rendered, those that are for courses assigned to the instructor have `checked` attributes, which selects them (displays them checked).</span></span>

<span data-ttu-id="6f675-210">사이트에 반환 될 때 변경 내용을 확인할 수 싶어하는 과정 할당을 변경한 후는 `Index` 페이지.</span><span class="sxs-lookup"><span data-stu-id="6f675-210">After changing course assignments, you'll want to be able to verify the changes when the site returns to the `Index` page.</span></span> <span data-ttu-id="6f675-211">따라서 해당 페이지에 있는 테이블에 열을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-211">Therefore, you need to add a column to the table in that page.</span></span> <span data-ttu-id="6f675-212">이 경우 있습니다 사용할 필요가 없습니다는 `ViewBag` 개체를 표시 하려는 정보를 이미 있으므로 `Courses` 의 탐색 속성은 `Instructor` 엔터티 모델로 페이지에 전달 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-212">In this case you don't need to use the `ViewBag` object, because the information you want to display is already in the `Courses` navigation property of the `Instructor` entity that you're passing to the page as the model.</span></span>

<span data-ttu-id="6f675-213">*Views\Instructor\Index.cshtml*, 추가 **Courses** 제목 바로 다음에 **Office** 다음 예제와 같이 제목:</span><span class="sxs-lookup"><span data-stu-id="6f675-213">In *Views\Instructor\Index.cshtml*, add a **Courses** heading immediately following the **Office** heading, as shown in the following example:</span></span>

[!code-html[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html?highlight=7)]

<span data-ttu-id="6f675-214">사무실 위치 정보 셀 바로 뒤에 새 세부 셀에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-214">Then add a new detail cell immediately following the office location detail cell:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=19,50-57)]

<span data-ttu-id="6f675-215">실행 된 **강사 인덱스** 각 강사에 할당 된 과정을 보려면 페이지를:</span><span class="sxs-lookup"><span data-stu-id="6f675-215">Run the **Instructor Index** page to see the courses assigned to each instructor:</span></span>

![Instructor_index_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

<span data-ttu-id="6f675-217">클릭 **편집** 에서 강사 편집 페이지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-217">Click **Edit** on an instructor to see the Edit page.</span></span>

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

<span data-ttu-id="6f675-219">일부 과정 할당을 변경 하 고 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-219">Change some course assignments and click **Save**.</span></span> <span data-ttu-id="6f675-220">인덱스 페이지에 변경 내용은 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-220">The changes you make are reflected on the Index page.</span></span>

 <span data-ttu-id="6f675-221">참고: 강사 과정 데이터를 편집 하려면 적용 되는 방법을 제한 된 수의 과목 필요한 경우에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-221">Note: The approach taken to edit instructor course data works well when there is a limited number of courses.</span></span> <span data-ttu-id="6f675-222">훨씬 큰 경우에 컬렉션의 경우 다른 UI와 다른 업데이트 방법을 필요한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-222">For collections that are much larger, a different UI and a different updating method would be required.</span></span>  
 

## <a name="update-the-delete-method"></a><span data-ttu-id="6f675-223">Delete 메서드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-223">Update the Delete Method</span></span>

<span data-ttu-id="6f675-224">강사 삭제 될 때 (있는 경우)에 해당 office 할당 레코드는 삭제 하므로 HttpPost Delete 메서드의 코드를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-224">Change the code in the HttpPost Delete method so the office assignment record (if any) is deleted when the instructor is deleted:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs?highlight=6,10)]


<span data-ttu-id="6f675-225">관리자 권한으로 부서에 배정 된 강사를 삭제 하려고 하면 참조 무결성 오류를 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-225">If you try to delete an instructor who is assigned to a department as administrator, you'll get a referential integrity error.</span></span> <span data-ttu-id="6f675-226">참조 [이 자습서의 현재 버전](../../getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) 추가 코드 강사 모든 부서 강사 관리자로 할당 된 위치에서 자동으로 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-226">See [the current version of this tutorial](../../getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) for additional code that will automatically remove the instructor from any department where the instructor is assigned as an administrator.</span></span>

## <a name="summary"></a><span data-ttu-id="6f675-227">요약</span><span class="sxs-lookup"><span data-stu-id="6f675-227">Summary</span></span>

<span data-ttu-id="6f675-228">이제이 소개 관련 데이터로 작업을 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-228">You have now completed this introduction to working with related data.</span></span> <span data-ttu-id="6f675-229">지금까지 전체 CRUD 작업을 완료 했으면이 자습서에 있지만 동시성 문제를 처리 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-229">So far in these tutorials you've done a full range of CRUD operations, but you haven't dealt with concurrency issues.</span></span> <span data-ttu-id="6f675-230">다음 자습서 동시성의 주제를 소개 하 고, 처리 옵션을 설명 하 고 동시성 처리 이미 작성 한 엔터티 형식에 대 한 CRUD 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-230">The next tutorial will introduce the topic of concurrency, explain options for handling it, and add concurrency handling to the CRUD code you've already written for one entity type.</span></span>

<span data-ttu-id="6f675-231">다른 Entity Framework 리소스에 대 한 링크의 끝에서 찾을 수 있습니다 [이 시리즈의 마지막 자습서](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6f675-231">Links to other Entity Framework resources, can be found at the end of [the last tutorial in this series](advanced-entity-framework-scenarios-for-an-mvc-web-application.md).</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="6f675-232">[이전](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[다음](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="6f675-232">[Previous](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span></span>
