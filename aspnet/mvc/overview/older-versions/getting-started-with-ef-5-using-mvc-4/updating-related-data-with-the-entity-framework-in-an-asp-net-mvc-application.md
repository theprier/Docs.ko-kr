---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: (6 / 10) ASP.NET MVC 응용 프로그램에서 Entity Framework를 사용 하 여 관련된 데이터 업데이트 | Microsoft Docs
author: tdykstra
description: Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 7871dc05-2750-470f-8b4c-3a52511949bc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: ceb311f16575f7aedf0fd789a28e7313daeeaceb
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41828702"
---
<a name="updating-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-6-of-10"></a><span data-ttu-id="c0450-103">(6 / 10) ASP.NET MVC 응용 프로그램에서 Entity Framework를 사용 하 여 관련된 데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="c0450-103">Updating Related Data with the Entity Framework in an ASP.NET MVC Application (6 of 10)</span></span>
====================
<span data-ttu-id="c0450-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="c0450-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="c0450-105">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="c0450-105">Download Completed Project</span></span>](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="c0450-106">Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio 2012를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="c0450-107">자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c0450-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="c0450-108">시작 부분에서 자습서 시리즈를 시작할 수 있습니다 또는 [이 장이에 대 한 시작 프로젝트 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 여기에서 시작 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-108">You can start the tutorial series from the beginning or [download a starter project for this chapter](building-the-ef5-mvc4-chapter-downloads.md) and start here.</span></span>
> 
> > [!NOTE] 
> > 
> > <span data-ttu-id="c0450-109">해결할 수 없는 문제가 발생 하는 경우 [완성 된 장 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 문제를 재현 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-109">If you run into a problem you can't resolve, [download the completed chapter](building-the-ef5-mvc4-chapter-downloads.md) and try to reproduce your problem.</span></span> <span data-ttu-id="c0450-110">일반적으로 코드의 완성 된 코드를 비교 하 여 문제에 솔루션을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-110">You can generally find the solution to the problem by comparing your code to the completed code.</span></span> <span data-ttu-id="c0450-111">몇 가지 일반적인 오류 및 해결 하는 방법에 대 한 참조 [오류 및 해결 방법입니다.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span><span class="sxs-lookup"><span data-stu-id="c0450-111">For some common errors and how to solve them, see [Errors and Workarounds.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)</span></span>


<span data-ttu-id="c0450-112">이전 자습서에서 관련된 데이터 표시 이 자습서에서는 관련된 데이터를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-112">In the previous tutorial you displayed related data; in this tutorial you'll update related data.</span></span> <span data-ttu-id="c0450-113">대부분의 관계에 대 한 해당 외래 키 필드를 업데이트 하 여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-113">For most relationships, this can be done by updating the appropriate foreign key fields.</span></span> <span data-ttu-id="c0450-114">다 대 다 관계에 대 한 Entity Framework 노출 하지 조인 테이블을 직접 않으므로 명시적으로 추가 하 고 해당 탐색 속성에서 엔터티를 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-114">For many-to-many relationships, the Entity Framework doesn't expose the join table directly, so you must explicitly add and remove entities to and from the appropriate navigation properties.</span></span>

<span data-ttu-id="c0450-115">다음 그림에서는 사용할 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-115">The following illustrations show the pages that you'll work with.</span></span>

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="customize-the-create-and-edit-pages-for-courses"></a><span data-ttu-id="c0450-118">강좌에 대한 만들기 및 편집 페이지 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="c0450-118">Customize the Create and Edit Pages for Courses</span></span>

<span data-ttu-id="c0450-119">새 강좌 엔터티가 만들어질 때 기존 부서에 대한 관계가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-119">When a new course entity is created, it must have a relationship to an existing department.</span></span> <span data-ttu-id="c0450-120">이를 수행하기 위해 스캐폴드 코드는 컨트롤러 메서드 및 부서를 선택하기 위한 드롭다운 목록을 포함하는 만들기 및 편집 보기를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-120">To facilitate this, the scaffolded code includes controller methods and Create and Edit views that include a drop-down list for selecting the department.</span></span> <span data-ttu-id="c0450-121">드롭다운 목록에서 집합을 `Course.DepartmentID` 외래 키 속성을 로드 하기 위해 Entity Framework에 필요한 모든입니다를 `Department` 적절 한 탐색 속성 `Department` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c0450-121">The drop-down list sets the `Course.DepartmentID` foreign key property, and that's all the Entity Framework needs in order to load the `Department` navigation property with the appropriate `Department` entity.</span></span> <span data-ttu-id="c0450-122">스캐폴드 코드를 사용하지만 오류 처리를 추가하고 드롭다운 목록을 정렬하도록 약간 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-122">You'll use the scaffolded code, but change it slightly to add error handling and sort the drop-down list.</span></span>

<span data-ttu-id="c0450-123">*CourseController.cs*, 네 개의 삭제 `Edit` 및 `Create` 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-123">In *CourseController.cs*, delete the four `Edit` and `Create` methods and replace them with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,10,13-14,21-27,34,41,44-45,52-58,62-68)]

<span data-ttu-id="c0450-124">`PopulateDepartmentsDropDownList` 메서드를 이름별로 정렬 하는 모든 부서의 목록을 가져오거나 만듭니다를 `SelectList` 드롭 다운 목록에 대 한 컬렉션 컬렉션 보기에 전달 하 고는 `ViewBag` 속성.</span><span class="sxs-lookup"><span data-stu-id="c0450-124">The `PopulateDepartmentsDropDownList` method gets a list of all departments sorted by name, creates a `SelectList` collection for a drop-down list, and passes the collection to the view in a `ViewBag` property.</span></span> <span data-ttu-id="c0450-125">메서드는 호출 코드가 드롭다운 목록이 렌더링될 때 선택될 항목을 지정하도록 허용하는 선택적 `selectedDepartment` 매개 변수를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-125">The method accepts the optional `selectedDepartment` parameter that allows the calling code to specify the item that will be selected when the drop-down list is rendered.</span></span> <span data-ttu-id="c0450-126">이름을 전달 하면 `DepartmentID` 를 [는 `DropDownList` 도우미](../working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md), 도우미에서 확인 한 다음 알고 합니다 `ViewBag` 개체에 대 한를 `SelectList` 라는 `DepartmentID`합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-126">The view will pass the name `DepartmentID` to [the `DropDownList` helper](../working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md), and the helper then knows to look in the `ViewBag` object for a `SelectList` named `DepartmentID`.</span></span>

<span data-ttu-id="c0450-127">합니다 `HttpGet` `Create` 메서드 호출을 `PopulateDepartmentsDropDownList` 새 강좌에 대 한 부서 설정 되지 않으며 아직 때문에 선택한 항목을 설정 하지 않고 메서드:</span><span class="sxs-lookup"><span data-stu-id="c0450-127">The `HttpGet` `Create` method calls the `PopulateDepartmentsDropDownList` method without setting the selected item, because for a new course the department is not established yet:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="c0450-128">합니다 `HttpGet` `Edit` 메서드 편집 중인 강좌에 이미 할당 되어 있는 부서의 ID에 따라 선택한 항목을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-128">The `HttpGet` `Edit` method sets the selected item, based on the ID of the department that is already assigned to the course being edited:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

<span data-ttu-id="c0450-129">합니다 `HttpPost` 둘 다에 대 한 메서드 `Create` 및 `Edit` 오류가 발생 한 후 페이지를 다시 표시 하려면 해당 하는 경우 선택한 항목을 설정 하는 코드를 포함:</span><span class="sxs-lookup"><span data-stu-id="c0450-129">The `HttpPost` methods for both `Create` and `Edit` also include code that sets the selected item when they redisplay the page after an error:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="c0450-130">이 코드는 오류 메시지를 표시 하는 페이지를 다시 표시를 하는 경우 부서에 관계 없이 선택 된 선택 된 상태로 유지 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-130">This code ensures that when the page is redisplayed to show the error message, whatever department was selected stays selected.</span></span>

<span data-ttu-id="c0450-131">*Views\Course\Create.cshtml*를 강조 표시 된 코드를 추가 하기 전에 새 강좌 번호 필드를 만듭니다 합니다 **Title** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-131">In *Views\Course\Create.cshtml*, add the highlighted code to create a new course number field before the **Title** field.</span></span> <span data-ttu-id="c0450-132">기본적으로 기본 키 필드 되지 스 캐 폴드 된 이전 자습서에서 설명 했 듯이 사용자가 키 값을 입력할 수 있으므로이 기본 키 이지만 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-132">As explained in an earlier tutorial, primary key fields aren't scaffolded by default, but this primary key is meaningful, so you want the user to be able to enter the key value.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=17-23)]

<span data-ttu-id="c0450-133">*Views\Course\Edit.cshtml*를 *Views\Course\Delete.cshtml*, 및 *Views\Course\Details.cshtml*, 전에 강좌 번호 필드를 추가 합니다 **제목**  필드입니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-133">In *Views\Course\Edit.cshtml*, *Views\Course\Delete.cshtml*, and *Views\Course\Details.cshtml*, add a course number field before the **Title** field.</span></span> <span data-ttu-id="c0450-134">기본 키 이기 때문에 표시 되는, 있지만 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-134">Because it's the primary key, it's displayed, but it can't be changed.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

<span data-ttu-id="c0450-135">실행 합니다 **만들기** 페이지 (과정 인덱스 페이지를 표시 하 고 클릭 **새로 만들기**) 새 강좌에 대 한 데이터를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-135">Run the **Create** page (display the Course Index page and click **Create New**) and enter data for a new course:</span></span>

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

<span data-ttu-id="c0450-137">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-137">Click **Create**.</span></span> <span data-ttu-id="c0450-138">강좌 인덱스 페이지가 목록에 추가 된 새 강좌로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-138">The Course Index page is displayed with the new course added to the list.</span></span> <span data-ttu-id="c0450-139">인덱스 페이지 목록의 부서 이름은 관계가 올바르게 설정되었음을 표시하는 탐색 속성에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-139">The department name in the Index page list comes from the navigation property, showing that the relationship was established correctly.</span></span>

![Course_Index_page_showing_new_course](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="c0450-141">실행 합니다 **편집할** 페이지 (과정 인덱스 페이지를 표시 하 고 클릭 **편집** 과정에서).</span><span class="sxs-lookup"><span data-stu-id="c0450-141">Run the **Edit** page (display the Course Index page and click **Edit** on a course).</span></span>

![Course_edit_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

<span data-ttu-id="c0450-143">페이지에서 데이터를 변경하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-143">Change data on the page and click **Save**.</span></span> <span data-ttu-id="c0450-144">강좌 인덱스 페이지가 업데이트 된 강좌 데이터로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-144">The Course Index page is displayed with the updated course data.</span></span>

## <a name="adding-an-edit-page-for-instructors"></a><span data-ttu-id="c0450-145">강사에 대 한 편집 페이지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-145">Adding an Edit Page for Instructors</span></span>

<span data-ttu-id="c0450-146">강사 레코드를 편집할 때 강사의 사무실 할당을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-146">When you edit an instructor record, you want to be able to update the instructor's office assignment.</span></span> <span data-ttu-id="c0450-147">`Instructor` 엔터티 간의 관계가 0 또는 1을 하나는 `OfficeAssignment` 엔터티 즉, 다음과 같은 경우를 처리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-147">The `Instructor` entity has a one-to-zero-or-one relationship with the `OfficeAssignment` entity, which means you must handle the following situations:</span></span>

- <span data-ttu-id="c0450-148">사용자가 사무실 할당 선택을 취소 하 고 원래 값이 있었던 것을 제거 하 고 삭제 해야 합니다는 `OfficeAssignment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c0450-148">If the user clears the office assignment and it originally had a value, you must remove and delete the `OfficeAssignment` entity.</span></span>
- <span data-ttu-id="c0450-149">사용자가 사무실 할당 값을 입력 하 고 원래 비어 있던 경우 새 작성 해야 `OfficeAssignment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c0450-149">If the user enters an office assignment value and it originally was empty, you must create a new `OfficeAssignment` entity.</span></span>
- <span data-ttu-id="c0450-150">기존 값을 변경 해야 하는 경우 사용자가 사무실 할당의 값을 변경, `OfficeAssignment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c0450-150">If the user changes the value of an office assignment, you must change the value in an existing `OfficeAssignment` entity.</span></span>

<span data-ttu-id="c0450-151">오픈 *InstructorController.cs* 살펴봅니다 합니다 `HttpGet` `Edit` 메서드:</span><span class="sxs-lookup"><span data-stu-id="c0450-151">Open *InstructorController.cs* and look at the `HttpGet` `Edit` method:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

<span data-ttu-id="c0450-152">여기에서 스 캐 폴드 된 코드는 원하는 결과가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-152">The scaffolded code here isn't what you want.</span></span> <span data-ttu-id="c0450-153">데이터 설정 되는 텍스트 상자를 필요한 수 있지만 드롭 다운 목록에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-153">It's setting up data for a drop-down list, but you what you need is a text box.</span></span> <span data-ttu-id="c0450-154">이 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-154">Replace this method with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

<span data-ttu-id="c0450-155">이 코드를 삭제 합니다 `ViewBag` 문을 연결에 대 한 즉시 로드를 추가 하 고 `OfficeAssignment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c0450-155">This code drops the `ViewBag` statement and adds eager loading for the associated `OfficeAssignment` entity.</span></span> <span data-ttu-id="c0450-156">즉시 로드를 수행할 수 없습니다는 `Find` 메서드를 하므로 `Where` 고 `Single` 메서드는 강사를 선택 하려면 대신 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-156">You can't perform eager loading with the `Find` method, so the `Where` and `Single` methods are used instead to select the instructor.</span></span>

<span data-ttu-id="c0450-157">대체는 `HttpPost` `Edit` 메서드를 다음 코드로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-157">Replace the `HttpPost` `Edit` method with the following code.</span></span> <span data-ttu-id="c0450-158">사무실 할당 업데이트를 처리 하는:</span><span class="sxs-lookup"><span data-stu-id="c0450-158">which handles office assignment updates:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="c0450-159">코드는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-159">The code does the following:</span></span>

- <span data-ttu-id="c0450-160">`OfficeAssignment` 탐색 속성에 대한 즉시 로드를 사용하여 데이터베이스에서 현재 `Instructor` 엔터티를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-160">Gets the current `Instructor` entity from the database using eager loading for the `OfficeAssignment` navigation property.</span></span> <span data-ttu-id="c0450-161">수행한 작업으로 동일 합니다 `HttpGet` `Edit` 메서드.</span><span class="sxs-lookup"><span data-stu-id="c0450-161">This is the same as what you did in the `HttpGet` `Edit` method.</span></span>
- <span data-ttu-id="c0450-162">모델 바인더의 값으로 검색된 `Instructor` 엔터티를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-162">Updates the retrieved `Instructor` entity with values from the model binder.</span></span> <span data-ttu-id="c0450-163">합니다 [tryupdatemodel에 전달](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) 사용 하는 오버 로드를 사용 하면 *화이트 리스트* 포함 하려는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-163">The [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) overload used enables you to *whitelist* the properties you want to include.</span></span> <span data-ttu-id="c0450-164">에 설명 된 대로 초과 게시를 이렇게 [두 번째 자습서](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-164">This prevents over-posting, as explained in [the second tutorial](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md).</span></span>

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]
- <span data-ttu-id="c0450-165">사무실 위치가 비어 있는 경우 설정 합니다 `Instructor.OfficeAssignment` 속성을 null로 있도록의 관련된 행은 `OfficeAssignment` 테이블은 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-165">If the office location is blank, sets the `Instructor.OfficeAssignment` property to null so that the related row in the `OfficeAssignment` table will be deleted.</span></span>

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]
- <span data-ttu-id="c0450-166">변경 내용을 데이터베이스에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-166">Saves the changes to the database.</span></span>

<span data-ttu-id="c0450-167">*Views\Instructor\Edit.cshtml*뒤를 `div` 요소에 대 한 합니다 **Hire Date** 필드에서 사무실 위치를 편집 하는 것에 대 한 새 필드 추가:</span><span class="sxs-lookup"><span data-stu-id="c0450-167">In *Views\Instructor\Edit.cshtml*, after the `div` elements for the **Hire Date** field, add a new field for editing the office location:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml)]

<span data-ttu-id="c0450-168">페이지를 실행 합니다 (선택 된 **강사** 탭을 클릭 한 다음 **편집** 강사에).</span><span class="sxs-lookup"><span data-stu-id="c0450-168">Run the page (select the **Instructors** tab and then click **Edit** on an instructor).</span></span> <span data-ttu-id="c0450-169">**사무실 위치**를 변경하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-169">Change the **Office Location** and click **Save**.</span></span>

![Changing_the_office_location](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

## <a name="adding-course-assignments-to-the-instructor-edit-page"></a><span data-ttu-id="c0450-171">강사에 강좌 할당 추가 편집 페이지</span><span class="sxs-lookup"><span data-stu-id="c0450-171">Adding Course Assignments to the Instructor Edit Page</span></span>

<span data-ttu-id="c0450-172">강사는 강좌 수에 관계 없이 가르칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-172">Instructors may teach any number of courses.</span></span> <span data-ttu-id="c0450-173">이제 다음 스크린샷에 표시된 것처럼 확인란 그룹을 사용하여 강좌 할당을 변경하는 기능을 추가하여 강사 편집 페이지를 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-173">Now you'll enhance the Instructor Edit page by adding the ability to change course assignments using a group of check boxes, as shown in the following screen shot:</span></span>

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="c0450-175">관계는 `Course` 및 `Instructor` 엔터티는 다 대 다 조인 테이블에 직접 액세스할 수 없는 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-175">The relationship between the `Course` and `Instructor` entities is many-to-many, which means you do not have direct access to the join table.</span></span> <span data-ttu-id="c0450-176">대신 추가 하 고에서 엔터티를 제거 합니다 `Instructor.Courses` 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-176">Instead, you will add and remove entities to and from the `Instructor.Courses` navigation property.</span></span>

<span data-ttu-id="c0450-177">강사에게 할당된 강좌를 변경할 수 있도록 하는 UI는 확인란의 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-177">The UI that enables you to change which courses an instructor is assigned to is a group of check boxes.</span></span> <span data-ttu-id="c0450-178">데이터베이스의 모든 강좌에 대한 확인란이 표시되고 강사에게 현재 할당되어 있는 것이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-178">A check box for every course in the database is displayed, and the ones that the instructor is currently assigned to are selected.</span></span> <span data-ttu-id="c0450-179">사용자는 확인란을 선택하거나 선택 취소하여 강좌 할당을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-179">The user can select or clear check boxes to change course assignments.</span></span> <span data-ttu-id="c0450-180">강좌의 번호가 훨씬 더 큰 경우 보기에서 데이터를 나타내는 다른 방법을 사용 하려는 것 하지만 관계 만들기 또는 삭제 하려면 탐색 속성을 조작 하는 동일한 방법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-180">If the number of courses were much greater, you would probably want to use a different method of presenting the data in the view, but you'd use the same method of manipulating navigation properties in order to create or delete relationships.</span></span>

<span data-ttu-id="c0450-181">확인란의 목록에 대한 보기에 데이터를 제공하려면 보기 모델 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-181">To provide data to the view for the list of check boxes, you'll use a view model class.</span></span> <span data-ttu-id="c0450-182">만들 *AssignedCourseData.cs* 에 *Viewmodel* 폴더 및 기존 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-182">Create *AssignedCourseData.cs* in the *ViewModels* folder and replace the existing code with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

<span data-ttu-id="c0450-183">*InstructorController.cs*을 대체 합니다 `HttpGet` `Edit` 메서드를 다음 코드로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-183">In *InstructorController.cs*, replace the `HttpGet` `Edit` method with the following code.</span></span> <span data-ttu-id="c0450-184">변경 내용은 강조 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-184">The changes are highlighted.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=5,8,12-27)]

<span data-ttu-id="c0450-185">코드는 `Courses` 탐색 속성에 대해 즉시 로드를 추가하고 새 `PopulateAssignedCourseData` 메서드를 호출하여 `AssignedCourseData` 보기 모델 클래스를 사용하여 확인란 배열에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-185">The code adds eager loading for the `Courses` navigation property and calls the new `PopulateAssignedCourseData` method to provide information for the check box array using the `AssignedCourseData` view model class.</span></span>

<span data-ttu-id="c0450-186">코드를 `PopulateAssignedCourseData` 메서드는 모두 읽은 `Course` 보기를 사용 하는 강좌의 목록을 로드 하기 위해 엔터티 모델 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-186">The code in the `PopulateAssignedCourseData` method reads through all `Course` entities in order to load a list of courses using the view model class.</span></span> <span data-ttu-id="c0450-187">각 강좌의 경우 코드는 강좌가 강사의 `Courses` 탐색 속성에 있는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-187">For each course, the code checks whether the course exists in the instructor's `Courses` navigation property.</span></span> <span data-ttu-id="c0450-188">강사에 강좌 할당 되었는지 여부를 확인할 때 효율적인 조회를 만들려면, 강사에 할당 된 강좌에 배치 됩니다는 [HashSet](https://msdn.microsoft.com/library/bb359438.aspx) 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-188">To create efficient lookup when checking whether a course is assigned to the instructor, the courses assigned to the instructor are put into a [HashSet](https://msdn.microsoft.com/library/bb359438.aspx) collection.</span></span> <span data-ttu-id="c0450-189">합니다 `Assigned` 속성이 `true` 강사 강좌에 대 한 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-189">The `Assigned` property is set to `true` for courses the instructor is assigned.</span></span> <span data-ttu-id="c0450-190">보기는 이 속성을 사용하여 선택된 것으로 표시되어야 하는 확인란을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-190">The view will use this property to determine which check boxes must be displayed as selected.</span></span> <span data-ttu-id="c0450-191">목록 보기에 전달 되는 마지막으로 `ViewBag` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-191">Finally, the list is passed to the view in a `ViewBag` property.</span></span>

<span data-ttu-id="c0450-192">다음으로 사용자가 **저장**을 클릭할 때 실행되는 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-192">Next, add the code that's executed when the user clicks **Save**.</span></span> <span data-ttu-id="c0450-193">대체는 `HttpPost` `Edit` 메서드를 다음 코드로 업데이트 하는 새 메서드를 호출 하는 합니다 `Courses` 의 탐색 속성을 `Instructor` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c0450-193">Replace the `HttpPost` `Edit` method with the following code, which calls a new method that updates the `Courses` navigation property of the `Instructor` entity.</span></span> <span data-ttu-id="c0450-194">변경 내용은 강조 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-194">The changes are highlighted.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs?highlight=3,7,20,33,37-65)]

<span data-ttu-id="c0450-195">보기의 컬렉션인 없으므로 `Course` 엔터티를 모델 바인더를 자동으로 업데이트할 수는 `Courses` 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-195">Since the view doesn't have a collection of `Course` entities, the model binder can't automatically update the `Courses` navigation property.</span></span> <span data-ttu-id="c0450-196">대신 모델 바인더를 사용 하 여 강좌 탐색 속성이 업데이트를 수행 하는 새 `UpdateInstructorCourses` 메서드.</span><span class="sxs-lookup"><span data-stu-id="c0450-196">Instead of using the model binder to update the Courses navigation property, you'll do that in the new `UpdateInstructorCourses` method.</span></span> <span data-ttu-id="c0450-197">따라서 모델 바인딩에서 `Courses` 속성을 제외해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-197">Therefore you need to exclude the `Courses` property from model binding.</span></span> <span data-ttu-id="c0450-198">이 호출 하는 코드를 변경 하지 않아도 [tryupdatemodel에 전달](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) 를 사용 중 이므로 *허용 목록* 오버 로드 및 `Courses` 포함 목록에 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-198">This doesn't require any change to the code that calls [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) because you're using the *whitelisting* overload and `Courses` isn't in the include list.</span></span>

<span data-ttu-id="c0450-199">경우 확인란과 선택 된 코드 검사가 `UpdateInstructorCourses` 초기화를 `Courses` 빈 컬렉션을 사용 하 여 탐색 속성:</span><span class="sxs-lookup"><span data-stu-id="c0450-199">If no check boxes were selected, the code in `UpdateInstructorCourses` initializes the `Courses` navigation property with an empty collection:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

<span data-ttu-id="c0450-200">그런 다음, 코드는 데이터베이스의 모든 강좌를 반복하고 현재 강사에게 할당된 것과 보기에서 선택되었던 것에 대해 각 강좌를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-200">The code then loops through all courses in the database and checks each course against the ones currently assigned to the instructor versus the ones that were selected in the view.</span></span> <span data-ttu-id="c0450-201">효율적인 조회를 수행하기 위해 후자의 두 컬렉션은 `HashSet` 개체에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-201">To facilitate efficient lookups, the latter two collections are stored in `HashSet` objects.</span></span>

<span data-ttu-id="c0450-202">강좌에 대한 확인란이 선택됐지만 강좌가 `Instructor.Courses` 탐색 속성에 없는 경우 강좌는 탐색 속성의 컬렉션에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-202">If the check box for a course was selected but the course isn't in the `Instructor.Courses` navigation property, the course is added to the collection in the navigation property.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

<span data-ttu-id="c0450-203">강좌에 대한 확인란이 선택되지 않았지만 강좌가 `Instructor.Courses` 탐색 속성에 있는 경우 강좌는 탐색 속성에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-203">If the check box for a course wasn't selected, but the course is in the `Instructor.Courses` navigation property, the course is removed from the navigation property.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

<span data-ttu-id="c0450-204">*Views\Instructor\Edit.cshtml*, 추가 **과정** 강조 표시 된 다음 추가 하 여 확인란 배열 필드 바로 뒤에 코드를 `div` 요소에 대 한는 `OfficeAssignment` 필드:</span><span class="sxs-lookup"><span data-stu-id="c0450-204">In *Views\Instructor\Edit.cshtml*, add a **Courses** field with an array of check boxes by adding the following highlighted code immediately after the `div` elements for the `OfficeAssignment` field:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml?highlight=51-73)]

<span data-ttu-id="c0450-205">이 코드는 세 개의 열이 있는 HTML 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-205">This code creates an HTML table that has three columns.</span></span> <span data-ttu-id="c0450-206">각 열은 강좌 번호 및 제목으로 구성된 캡션이 뒤에 오는 확인란입니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-206">In each column is a check box followed by a caption that consists of the course number and title.</span></span> <span data-ttu-id="c0450-207">확인란은 모두 동일한 이름 ("selectedCourses")을 그룹으로 간주 된 모델 바인더를 알리는 경우</span><span class="sxs-lookup"><span data-stu-id="c0450-207">The check boxes all have the same name ("selectedCourses"), which informs the model binder that they are to be treated as a group.</span></span> <span data-ttu-id="c0450-208">합니다 `value` 각 확인란의 특성 값으로 설정 되어 `CourseID.` 모델 바인더로 구성 된 컨트롤러에 배열 전달 페이지가 게시 되 면는 `CourseID` 확인란만 선택 하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-208">The `value` attribute of each check box is set to the value of `CourseID.` When the page is posted, the model binder passes an array to the controller that consists of the `CourseID` values for only the check boxes which are selected.</span></span>

<span data-ttu-id="c0450-209">확인란이 처음으로 렌더링 강사에 게 할당 된 강좌에 대 한 수 있는 경우 `checked` (선택 된 것으로 표시) 항목을 선택 하는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-209">When the check boxes are initially rendered, those that are for courses assigned to the instructor have `checked` attributes, which selects them (displays them checked).</span></span>

<span data-ttu-id="c0450-210">강좌 할당을 변경한 후 사이트를 반환할 때 변경 내용을 확인할 수 하려는 `Index` 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-210">After changing course assignments, you'll want to be able to verify the changes when the site returns to the `Index` page.</span></span> <span data-ttu-id="c0450-211">따라서 해당 페이지에 있는 테이블에 열을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-211">Therefore, you need to add a column to the table in that page.</span></span> <span data-ttu-id="c0450-212">이 경우 사용할 필요가 없습니다를 `ViewBag` 개체를 표시 하려는 정보를 이미 있으므로 `Courses` 의 탐색 속성을 `Instructor` 모델로 페이지로 전달 하는 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c0450-212">In this case you don't need to use the `ViewBag` object, because the information you want to display is already in the `Courses` navigation property of the `Instructor` entity that you're passing to the page as the model.</span></span>

<span data-ttu-id="c0450-213">*Views\Instructor\Index.cshtml*, 추가 **과정** 머리글 바로 다음을 **Office** 다음 예제에서와 같이 제목:</span><span class="sxs-lookup"><span data-stu-id="c0450-213">In *Views\Instructor\Index.cshtml*, add a **Courses** heading immediately following the **Office** heading, as shown in the following example:</span></span>

[!code-html[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html?highlight=7)]

<span data-ttu-id="c0450-214">새 정보 셀이 사무실 위치 정보 셀 바로 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-214">Then add a new detail cell immediately following the office location detail cell:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=19,50-57)]

<span data-ttu-id="c0450-215">실행 합니다 **강사 인덱스** 각 강사에 할당 된 강좌 페이지:</span><span class="sxs-lookup"><span data-stu-id="c0450-215">Run the **Instructor Index** page to see the courses assigned to each instructor:</span></span>

![Instructor_index_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

<span data-ttu-id="c0450-217">클릭 **편집** 에서 강사 편집 페이지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-217">Click **Edit** on an instructor to see the Edit page.</span></span>

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

<span data-ttu-id="c0450-219">일부 강좌 할당을 변경 하 고 클릭 **저장할**합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-219">Change some course assignments and click **Save**.</span></span> <span data-ttu-id="c0450-220">변경 내용은 인덱스 페이지에 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-220">The changes you make are reflected on the Index page.</span></span>

 <span data-ttu-id="c0450-221">참고: 강사 강좌 데이터를 편집을 수행 하는 방법은 제한 된 수의 과정 필요한 경우에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-221">Note: The approach taken to edit instructor course data works well when there is a limited number of courses.</span></span> <span data-ttu-id="c0450-222">훨씬 큰 컬렉션의 경우 다른 UI 및 다른 업데이트 메서드가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-222">For collections that are much larger, a different UI and a different updating method would be required.</span></span>  
 

## <a name="update-the-delete-method"></a><span data-ttu-id="c0450-223">Delete 메서드 업데이트</span><span class="sxs-lookup"><span data-stu-id="c0450-223">Update the Delete Method</span></span>

<span data-ttu-id="c0450-224">강사 삭제 되 면 office 할당 레코드 (해당 되는 경우)가 삭제 되도록 HttpPost Delete 메서드의 코드를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-224">Change the code in the HttpPost Delete method so the office assignment record (if any) is deleted when the instructor is deleted:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs?highlight=6,10)]


<span data-ttu-id="c0450-225">관리자 권한으로 부서에 배정 된 강사를 삭제 하려고 하면 참조 무결성 오류를 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-225">If you try to delete an instructor who is assigned to a department as administrator, you'll get a referential integrity error.</span></span> <span data-ttu-id="c0450-226">참조 [이 자습서의 현재 버전](../../getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) 강사 관리자로 할당 되는 모든 부서에서 강사를 자동으로 제거 됩니다는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-226">See [the current version of this tutorial](../../getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) for additional code that will automatically remove the instructor from any department where the instructor is assigned as an administrator.</span></span>

## <a name="summary"></a><span data-ttu-id="c0450-227">요약</span><span class="sxs-lookup"><span data-stu-id="c0450-227">Summary</span></span>

<span data-ttu-id="c0450-228">이제 관련된 데이터를 사용 하 여 작업 한이 소개를 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-228">You have now completed this introduction to working with related data.</span></span> <span data-ttu-id="c0450-229">지금이 자습서에서는 전체 CRUD 작업을 수행 했습니다 하지만 동시성 문제 처리 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-229">So far in these tutorials you've done a full range of CRUD operations, but you haven't dealt with concurrency issues.</span></span> <span data-ttu-id="c0450-230">다음 자습서 동시성의 항목을 소개 하 고이 처리 하는 것에 대 한 옵션을 설명 하 고 동시성 처리 한 엔터티 형식에 대해 이미 작성 한 CRUD 코드를 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-230">The next tutorial will introduce the topic of concurrency, explain options for handling it, and add concurrency handling to the CRUD code you've already written for one entity type.</span></span>

<span data-ttu-id="c0450-231">끝에 다른 Entity Framework 리소스에 대 한 링크를 찾을 수 있습니다 [이 시리즈의 마지막 자습서](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c0450-231">Links to other Entity Framework resources, can be found at the end of [the last tutorial in this series](advanced-entity-framework-scenarios-for-an-mvc-web-application.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c0450-232">[이전](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [다음](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="c0450-232">[Previous](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span></span>
