---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: ASP.NET MVC 응용 프로그램에서 Entity Framework를 사용 하 여 관련된 데이터 업데이트 | Microsoft Docs
author: tdykstra
description: Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 6 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다...
ms.author: riande
ms.date: 05/01/2015
ms.assetid: 7ba88418-5d0a-437d-b6dc-7c3816d4ec07
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 647793a65dec8feaf37de561ad77b4585bb869a8
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "48912217"
---
<a name="updating-related-data-with-the-entity-framework-in-an-aspnet-mvc-application"></a><span data-ttu-id="480e3-103">ASP.NET MVC 응용 프로그램에서 Entity Framework를 사용 하 여 관련된 데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="480e3-103">Updating Related Data with the Entity Framework in an ASP.NET MVC Application</span></span>
====================
<span data-ttu-id="480e3-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="480e3-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="480e3-105">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="480e3-105">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)

> <span data-ttu-id="480e3-106">Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 6 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 5 applications using the Entity Framework 6 Code First and Visual Studio.</span></span> <span data-ttu-id="480e3-107">자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="480e3-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>


<span data-ttu-id="480e3-108">이전 자습서에서 관련된 데이터 표시 이 자습서에서는 관련된 데이터를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-108">In the previous tutorial you displayed related data; in this tutorial you'll update related data.</span></span> <span data-ttu-id="480e3-109">대부분의 관계에 대 한 외래 키 필드 또는 탐색 속성을 업데이트 하 여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-109">For most relationships, this can be done by updating either foreign key fields or navigation properties.</span></span> <span data-ttu-id="480e3-110">다 대 다 관계에 대 한 Entity Framework 노출 하지 조인 테이블을 직접 추가 하 고 해당 탐색 속성에서 엔터티를 제거할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-110">For many-to-many relationships, the Entity Framework doesn't expose the join table directly, so you add and remove entities to and from the appropriate navigation properties.</span></span>

<span data-ttu-id="480e3-111">다음 그림에서는 사용할 일부 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-111">The following illustrations show some of the pages that you'll work with.</span></span>

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

![과정을 사용 하 여 강사 편집](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="customize-the-create-and-edit-pages-for-courses"></a><span data-ttu-id="480e3-115">강좌에 대한 만들기 및 편집 페이지 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="480e3-115">Customize the Create and Edit Pages for Courses</span></span>

<span data-ttu-id="480e3-116">새 강좌 엔터티가 만들어질 때 기존 부서에 대한 관계가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-116">When a new course entity is created, it must have a relationship to an existing department.</span></span> <span data-ttu-id="480e3-117">이를 수행하기 위해 스캐폴드 코드는 컨트롤러 메서드 및 부서를 선택하기 위한 드롭다운 목록을 포함하는 만들기 및 편집 보기를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-117">To facilitate this, the scaffolded code includes controller methods and Create and Edit views that include a drop-down list for selecting the department.</span></span> <span data-ttu-id="480e3-118">드롭다운 목록에서 집합을 `Course.DepartmentID` 외래 키 속성을 로드 하기 위해 Entity Framework에 필요한 모든입니다를 `Department` 적절 한 탐색 속성 `Department` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="480e3-118">The drop-down list sets the `Course.DepartmentID` foreign key property, and that's all the Entity Framework needs in order to load the `Department` navigation property with the appropriate `Department` entity.</span></span> <span data-ttu-id="480e3-119">스캐폴드 코드를 사용하지만 오류 처리를 추가하고 드롭다운 목록을 정렬하도록 약간 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-119">You'll use the scaffolded code, but change it slightly to add error handling and sort the drop-down list.</span></span>

<span data-ttu-id="480e3-120">*CourseController.cs*, 네 개의 삭제 `Create` 및 `Edit` 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-120">In *CourseController.cs*, delete the four `Create` and `Edit` methods and replace them with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,11-12,19-25,40,44,46,48-78)]

<span data-ttu-id="480e3-121">다음 추가 `using` 파일의 시작 부분에 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-121">Add the following `using` statement at the beginning of the file:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="480e3-122">`PopulateDepartmentsDropDownList` 메서드를 이름별로 정렬 하는 모든 부서의 목록을 가져오거나 만듭니다를 `SelectList` 드롭 다운 목록에 대 한 컬렉션 컬렉션 보기에 전달 하 고는 `ViewBag` 속성.</span><span class="sxs-lookup"><span data-stu-id="480e3-122">The `PopulateDepartmentsDropDownList` method gets a list of all departments sorted by name, creates a `SelectList` collection for a drop-down list, and passes the collection to the view in a `ViewBag` property.</span></span> <span data-ttu-id="480e3-123">메서드는 호출 코드가 드롭다운 목록이 렌더링될 때 선택될 항목을 지정하도록 허용하는 선택적 `selectedDepartment` 매개 변수를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-123">The method accepts the optional `selectedDepartment` parameter that allows the calling code to specify the item that will be selected when the drop-down list is rendered.</span></span> <span data-ttu-id="480e3-124">이름을 전달 하면 `DepartmentID` 에 [DropDownList](../../older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md) helper 및 도우미 보는 것을 압니다는 `ViewBag` 개체에 대 한를 `SelectList` 라는 `DepartmentID`합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-124">The view will pass the name `DepartmentID` to the [DropDownList](../../older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md) helper, and the helper then knows to look in the `ViewBag` object for a `SelectList` named `DepartmentID`.</span></span>

<span data-ttu-id="480e3-125">합니다 `HttpGet` `Create` 메서드 호출을 `PopulateDepartmentsDropDownList` 새 강좌에 대 한 부서 설정 되지 않으며 아직 때문에 선택한 항목을 설정 하지 않고 메서드:</span><span class="sxs-lookup"><span data-stu-id="480e3-125">The `HttpGet` `Create` method calls the `PopulateDepartmentsDropDownList` method without setting the selected item, because for a new course the department is not established yet:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

<span data-ttu-id="480e3-126">합니다 `HttpGet` `Edit` 메서드 편집 중인 강좌에 이미 할당 되어 있는 부서의 ID에 따라 선택한 항목을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-126">The `HttpGet` `Edit` method sets the selected item, based on the ID of the department that is already assigned to the course being edited:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=12)]

<span data-ttu-id="480e3-127">합니다 `HttpPost` 둘 다에 대 한 메서드 `Create` 및 `Edit` 오류가 발생 한 후 페이지를 다시 표시 하려면 해당 하는 경우 선택한 항목을 설정 하는 코드를 포함:</span><span class="sxs-lookup"><span data-stu-id="480e3-127">The `HttpPost` methods for both `Create` and `Edit` also include code that sets the selected item when they redisplay the page after an error:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=6)]

<span data-ttu-id="480e3-128">이 코드는 오류 메시지를 표시 하는 페이지를 다시 표시를 하는 경우 부서에 관계 없이 선택 된 선택 된 상태로 유지 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-128">This code ensures that when the page is redisplayed to show the error message, whatever department was selected stays selected.</span></span>

<span data-ttu-id="480e3-129">강좌 보기는 이미 스 캐 폴드 된 부서 필드에 대 한 드롭다운 목록을 사용 하 여 않으려는 DepartmentID 캡션이이 필드에 대 한 확인을 다음 강조 표시를 변경 합니다 *Views\Course\Create.cshtml* 파일 캡션을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-129">The Course views are already scaffolded with drop-down lists for the department field, but you don't want the DepartmentID caption for this field, so make the following highlighted change to the *Views\Course\Create.cshtml* file to change the caption.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml?highlight=43)]

<span data-ttu-id="480e3-130">에 동일한 변경을 *Views\Course\Edit.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-130">Make the same change in *Views\Course\Edit.cshtml*.</span></span>

<span data-ttu-id="480e3-131">일반적으로 스 캐 폴더 키 값을 변경할 수 없습니다 및 의미 있는 값을 사용자에 게 표시 되지 않습니다. 데이터베이스에서 생성 됩니다 때문에 기본 키 스 캐 폴딩 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-131">Normally the scaffolder doesn't scaffold a primary key because the key value is generated by the database and can't be changed and isn't a meaningful value to be displayed to users.</span></span> <span data-ttu-id="480e3-132">강좌 엔터티를 스 캐 폴더는 텍스트 상자에 대 한 포함지 않습니다 합니다 `CourseID` 파악 하는 필드는 `DatabaseGeneratedOption.None` 특성에 있어야 함을 의미 사용자 수 기본 키 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-132">For Course entities the scaffolder does include an text box for the `CourseID` field because it understands that the `DatabaseGeneratedOption.None` attribute means the user should be able enter the primary key value.</span></span> <span data-ttu-id="480e3-133">하지만 수가 더 의미 있는 되도록 하므로 수동으로 추가 해야 다른 보기에 표시를 이해 하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-133">But it doesn't understand that because the number is meaningful you want to see it in the other views, so you need to add it manually.</span></span>

<span data-ttu-id="480e3-134">*Views\Course\Edit.cshtml*, 전에 강좌 번호 필드를 추가 합니다 **Title** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-134">In *Views\Course\Edit.cshtml*, add a course number field before the **Title** field.</span></span> <span data-ttu-id="480e3-135">기본 키 이기 때문에 표시 되는, 있지만 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-135">Because it's the primary key, it's displayed, but it can't be changed.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cshtml)]

<span data-ttu-id="480e3-136">이미 숨겨진된 필드 (`Html.HiddenFor` 도우미) 편집 보기에 강좌 번호에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-136">There's already a hidden field (`Html.HiddenFor` helper) for the course number in the Edit view.</span></span> <span data-ttu-id="480e3-137">추가 *Html.LabelFor* 를 클릭할 때 게시 된 데이터에 포함 되도록 강좌 번호 하지 발생할 도우미 숨겨진된 필드에 대 한 필요성이 없어지지는 **저장** 편집 페이지.</span><span class="sxs-lookup"><span data-stu-id="480e3-137">Adding an *Html.LabelFor* helper doesn't eliminate the need for the hidden field because it doesn't cause the course number to be included in the posted data when the user clicks **Save** on the Edit page.</span></span>

<span data-ttu-id="480e3-138">*Views\Course\Delete.cshtml* 하 고 *Views\Course\Details.cshtml*, "부서" "Name"에서 부서 이름을 캡션을 변경 하 고 전에 강좌 번호 필드를 추가 합니다 **제목**  필드입니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-138">In *Views\Course\Delete.cshtml* and *Views\Course\Details.cshtml*, change the department name caption from "Name" to "Department" and add a course number field before the **Title** field.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cshtml?highlight=2,9-15)]

<span data-ttu-id="480e3-139">실행 합니다 **만들기** 페이지 (과정 인덱스 페이지를 표시 하 고 클릭 **새로 만들기**) 새 강좌에 대 한 데이터를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-139">Run the **Create** page (display the Course Index page and click **Create New**) and enter data for a new course:</span></span>

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

<span data-ttu-id="480e3-141">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-141">Click **Create**.</span></span> <span data-ttu-id="480e3-142">강좌 인덱스 페이지가 목록에 추가 된 새 강좌로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-142">The Course Index page is displayed with the new course added to the list.</span></span> <span data-ttu-id="480e3-143">인덱스 페이지 목록의 부서 이름은 관계가 올바르게 설정되었음을 표시하는 탐색 속성에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-143">The department name in the Index page list comes from the navigation property, showing that the relationship was established correctly.</span></span>

![Course_Index_page_showing_new_course](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

<span data-ttu-id="480e3-145">실행 합니다 **편집할** 페이지 (과정 인덱스 페이지를 표시 하 고 클릭 **편집** 과정에서).</span><span class="sxs-lookup"><span data-stu-id="480e3-145">Run the **Edit** page (display the Course Index page and click **Edit** on a course).</span></span>

![Course_edit_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="480e3-147">페이지에서 데이터를 변경하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-147">Change data on the page and click **Save**.</span></span> <span data-ttu-id="480e3-148">강좌 인덱스 페이지가 업데이트 된 강좌 데이터로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-148">The Course Index page is displayed with the updated course data.</span></span>

## <a name="adding-an-edit-page-for-instructors"></a><span data-ttu-id="480e3-149">강사에 대 한 편집 페이지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-149">Adding an Edit Page for Instructors</span></span>

<span data-ttu-id="480e3-150">강사 레코드를 편집할 때 강사의 사무실 할당을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-150">When you edit an instructor record, you want to be able to update the instructor's office assignment.</span></span> <span data-ttu-id="480e3-151">`Instructor` 엔터티 간의 관계가 0 또는 1을 하나는 `OfficeAssignment` 엔터티 즉, 다음과 같은 경우를 처리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-151">The `Instructor` entity has a one-to-zero-or-one relationship with the `OfficeAssignment` entity, which means you must handle the following situations:</span></span>

- <span data-ttu-id="480e3-152">사용자가 사무실 할당 선택을 취소 하 고 원래 값이 있었던 것을 제거 하 고 삭제 해야 합니다는 `OfficeAssignment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="480e3-152">If the user clears the office assignment and it originally had a value, you must remove and delete the `OfficeAssignment` entity.</span></span>
- <span data-ttu-id="480e3-153">사용자가 사무실 할당 값을 입력 하 고 원래 비어 있던 경우 새 작성 해야 `OfficeAssignment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="480e3-153">If the user enters an office assignment value and it originally was empty, you must create a new `OfficeAssignment` entity.</span></span>
- <span data-ttu-id="480e3-154">기존 값을 변경 해야 하는 경우 사용자가 사무실 할당의 값을 변경, `OfficeAssignment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="480e3-154">If the user changes the value of an office assignment, you must change the value in an existing `OfficeAssignment` entity.</span></span>

<span data-ttu-id="480e3-155">오픈 *InstructorController.cs* 살펴봅니다 합니다 `HttpGet` `Edit` 메서드:</span><span class="sxs-lookup"><span data-stu-id="480e3-155">Open *InstructorController.cs* and look at the `HttpGet` `Edit` method:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="480e3-156">여기에서 스 캐 폴드 된 코드는 원하는 결과가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-156">The scaffolded code here isn't what you want.</span></span> <span data-ttu-id="480e3-157">데이터 설정 되는 텍스트 상자를 필요한 수 있지만 드롭 다운 목록에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-157">It's setting up data for a drop-down list, but you what you need is a text box.</span></span> <span data-ttu-id="480e3-158">이 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-158">Replace this method with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs?highlight=7-10)]

<span data-ttu-id="480e3-159">이 코드를 삭제 합니다 `ViewBag` 문을 연결에 대 한 즉시 로드를 추가 하 고 `OfficeAssignment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="480e3-159">This code drops the `ViewBag` statement and adds eager loading for the associated `OfficeAssignment` entity.</span></span> <span data-ttu-id="480e3-160">즉시 로드를 수행할 수 없습니다는 `Find` 메서드를 하므로 `Where` 고 `Single` 메서드는 강사를 선택 하려면 대신 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-160">You can't perform eager loading with the `Find` method, so the `Where` and `Single` methods are used instead to select the instructor.</span></span>

<span data-ttu-id="480e3-161">대체는 `HttpPost` `Edit` 메서드를 다음 코드로 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-161">Replace the `HttpPost` `Edit` method with the following code.</span></span> <span data-ttu-id="480e3-162">사무실 할당 업데이트를 처리 하는:</span><span class="sxs-lookup"><span data-stu-id="480e3-162">which handles office assignment updates:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="480e3-163">에 대 한 참조 `RetryLimitExceededException` 필요를 `using` 문에 추가 하려면 마우스 오른쪽 단추로 클릭 `RetryLimitExceededException`를 클릭 하 고 **해결** - **System.Data.Entity.Infrastructure를사용하여**.</span><span class="sxs-lookup"><span data-stu-id="480e3-163">The reference to `RetryLimitExceededException` requires a `using` statement; to add it, right-click `RetryLimitExceededException`, and then click **Resolve** - **using System.Data.Entity.Infrastructure**.</span></span>

![다시 시도 예외 해결](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

<span data-ttu-id="480e3-165">코드는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-165">The code does the following:</span></span>

- <span data-ttu-id="480e3-166">메서드 이름을 변경 `EditPost` 서명이 동일 이제 되어 합니다 `HttpGet` 메서드 (의 `ActionName` 특성 /Edit/ URL을 계속 사용 되도록 지정).</span><span class="sxs-lookup"><span data-stu-id="480e3-166">Changes the method name to `EditPost` because the signature is now the same as the `HttpGet` method (the `ActionName` attribute specifies that the /Edit/ URL is still used).</span></span>
- <span data-ttu-id="480e3-167">`OfficeAssignment` 탐색 속성에 대한 즉시 로드를 사용하여 데이터베이스에서 현재 `Instructor` 엔터티를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-167">Gets the current `Instructor` entity from the database using eager loading for the `OfficeAssignment` navigation property.</span></span> <span data-ttu-id="480e3-168">수행한 작업으로 동일 합니다 `HttpGet` `Edit` 메서드.</span><span class="sxs-lookup"><span data-stu-id="480e3-168">This is the same as what you did in the `HttpGet` `Edit` method.</span></span>
- <span data-ttu-id="480e3-169">모델 바인더의 값으로 검색된 `Instructor` 엔터티를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-169">Updates the retrieved `Instructor` entity with values from the model binder.</span></span> <span data-ttu-id="480e3-170">합니다 [tryupdatemodel에 전달](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) 사용 하는 오버 로드를 사용 하면 *화이트 리스트* 포함 하려는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-170">The [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) overload used enables you to *whitelist* the properties you want to include.</span></span> <span data-ttu-id="480e3-171">에 설명 된 대로 초과 게시를 이렇게 [두 번째 자습서](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-171">This prevents over-posting, as explained in [the second tutorial](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md).</span></span>

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]
- <span data-ttu-id="480e3-172">사무실 위치가 비어 있는 경우 설정 합니다 `Instructor.OfficeAssignment` 속성을 null로 있도록의 관련된 행은 `OfficeAssignment` 테이블은 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-172">If the office location is blank, sets the `Instructor.OfficeAssignment` property to null so that the related row in the `OfficeAssignment` table will be deleted.</span></span>

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]
- <span data-ttu-id="480e3-173">변경 내용을 데이터베이스에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-173">Saves the changes to the database.</span></span>

<span data-ttu-id="480e3-174">*Views\Instructor\Edit.cshtml*뒤를 `div` 요소에 대 한 합니다 **Hire Date** 필드에서 사무실 위치를 편집 하는 것에 대 한 새 필드 추가:</span><span class="sxs-lookup"><span data-stu-id="480e3-174">In *Views\Instructor\Edit.cshtml*, after the `div` elements for the **Hire Date** field, add a new field for editing the office location:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml)]

<span data-ttu-id="480e3-175">페이지를 실행 합니다 (선택 된 **강사** 탭을 클릭 한 다음 **편집** 강사에).</span><span class="sxs-lookup"><span data-stu-id="480e3-175">Run the page (select the **Instructors** tab and then click **Edit** on an instructor).</span></span> <span data-ttu-id="480e3-176">**사무실 위치**를 변경하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-176">Change the **Office Location** and click **Save**.</span></span>

![Changing_the_office_location](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

## <a name="adding-course-assignments-to-the-instructor-edit-page"></a><span data-ttu-id="480e3-178">강사에 강좌 할당 추가 편집 페이지</span><span class="sxs-lookup"><span data-stu-id="480e3-178">Adding Course Assignments to the Instructor Edit Page</span></span>

<span data-ttu-id="480e3-179">강사는 강좌 수에 관계 없이 가르칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-179">Instructors may teach any number of courses.</span></span> <span data-ttu-id="480e3-180">이제 다음 스크린샷에 표시된 것처럼 확인란 그룹을 사용하여 강좌 할당을 변경하는 기능을 추가하여 강사 편집 페이지를 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-180">Now you'll enhance the Instructor Edit page by adding the ability to change course assignments using a group of check boxes, as shown in the following screen shot:</span></span>

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

<span data-ttu-id="480e3-182">관계는 `Course` 및 `Instructor` 엔터티는 다 대 다 조인 테이블에 있는 외래 키 속성에 직접 액세스할 수 없는 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-182">The relationship between the `Course` and `Instructor` entities is many-to-many, which means you do not have direct access to the foreign key properties which are in the join table.</span></span> <span data-ttu-id="480e3-183">추가 하 고에서 엔터티를 제거 하는 대신는 `Instructor.Courses` 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-183">Instead, you add and remove entities to and from the `Instructor.Courses` navigation property.</span></span>

<span data-ttu-id="480e3-184">강사에게 할당된 강좌를 변경할 수 있도록 하는 UI는 확인란의 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-184">The UI that enables you to change which courses an instructor is assigned to is a group of check boxes.</span></span> <span data-ttu-id="480e3-185">데이터베이스의 모든 강좌에 대한 확인란이 표시되고 강사에게 현재 할당되어 있는 것이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-185">A check box for every course in the database is displayed, and the ones that the instructor is currently assigned to are selected.</span></span> <span data-ttu-id="480e3-186">사용자는 확인란을 선택하거나 선택 취소하여 강좌 할당을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-186">The user can select or clear check boxes to change course assignments.</span></span> <span data-ttu-id="480e3-187">강좌의 번호가 훨씬 더 큰 경우 보기에서 데이터를 나타내는 다른 방법을 사용 하려는 것 하지만 관계 만들기 또는 삭제 하려면 탐색 속성을 조작 하는 동일한 방법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-187">If the number of courses were much greater, you would probably want to use a different method of presenting the data in the view, but you'd use the same method of manipulating navigation properties in order to create or delete relationships.</span></span>

<span data-ttu-id="480e3-188">확인란의 목록에 대한 보기에 데이터를 제공하려면 보기 모델 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-188">To provide data to the view for the list of check boxes, you'll use a view model class.</span></span> <span data-ttu-id="480e3-189">만들 *AssignedCourseData.cs* 에 *Viewmodel* 폴더 및 기존 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-189">Create *AssignedCourseData.cs* in the *ViewModels* folder and replace the existing code with the following code:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

<span data-ttu-id="480e3-190">*InstructorController.cs*을 대체 합니다 `HttpGet` `Edit` 메서드를 다음 코드로 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-190">In *InstructorController.cs*, replace the `HttpGet` `Edit` method with the following code.</span></span> <span data-ttu-id="480e3-191">변경 내용은 강조 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-191">The changes are highlighted.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs?highlight=9,12,20-35)]

<span data-ttu-id="480e3-192">코드는 `Courses` 탐색 속성에 대해 즉시 로드를 추가하고 새 `PopulateAssignedCourseData` 메서드를 호출하여 `AssignedCourseData` 보기 모델 클래스를 사용하여 확인란 배열에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-192">The code adds eager loading for the `Courses` navigation property and calls the new `PopulateAssignedCourseData` method to provide information for the check box array using the `AssignedCourseData` view model class.</span></span>

<span data-ttu-id="480e3-193">코드를 `PopulateAssignedCourseData` 메서드는 모두 읽은 `Course` 보기를 사용 하는 강좌의 목록을 로드 하기 위해 엔터티 모델 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-193">The code in the `PopulateAssignedCourseData` method reads through all `Course` entities in order to load a list of courses using the view model class.</span></span> <span data-ttu-id="480e3-194">각 강좌의 경우 코드는 강좌가 강사의 `Courses` 탐색 속성에 있는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-194">For each course, the code checks whether the course exists in the instructor's `Courses` navigation property.</span></span> <span data-ttu-id="480e3-195">강사에 강좌 할당 되었는지 여부를 확인할 때 효율적인 조회를 만들려면, 강사에 할당 된 강좌에 배치 됩니다는 [HashSet](https://msdn.microsoft.com/library/bb359438.aspx) 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-195">To create efficient lookup when checking whether a course is assigned to the instructor, the courses assigned to the instructor are put into a [HashSet](https://msdn.microsoft.com/library/bb359438.aspx) collection.</span></span> <span data-ttu-id="480e3-196">합니다 `Assigned` 속성이 `true` 강사 강좌에 대 한 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-196">The `Assigned` property is set to `true` for courses the instructor is assigned.</span></span> <span data-ttu-id="480e3-197">보기는 이 속성을 사용하여 선택된 것으로 표시되어야 하는 확인란을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-197">The view will use this property to determine which check boxes must be displayed as selected.</span></span> <span data-ttu-id="480e3-198">목록 보기에 전달 되는 마지막으로 `ViewBag` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-198">Finally, the list is passed to the view in a `ViewBag` property.</span></span>

<span data-ttu-id="480e3-199">다음으로 사용자가 **저장**을 클릭할 때 실행되는 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-199">Next, add the code that's executed when the user clicks **Save**.</span></span> <span data-ttu-id="480e3-200">대체는 `EditPost` 메서드를 다음 코드로 업데이트 하는 새 메서드를 호출 하는 합니다 `Courses` 의 탐색 속성을 `Instructor` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="480e3-200">Replace the `EditPost` method with the following code, which calls a new method that updates the `Courses` navigation property of the `Instructor` entity.</span></span> <span data-ttu-id="480e3-201">변경 내용은 강조 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-201">The changes are highlighted.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs?highlight=3,11,25,37,40-68)]

<span data-ttu-id="480e3-202">메서드 서명은 이제 다른 합니다 `HttpGet` `Edit` 메서드를 메서드 이름에서 변경 `EditPost` 돌아가기 `Edit`합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-202">The method signature is now different from the `HttpGet` `Edit` method, so the method name changes from `EditPost` back to `Edit`.</span></span>

<span data-ttu-id="480e3-203">보기의 컬렉션인 없으므로 `Course` 엔터티를 모델 바인더를 자동으로 업데이트할 수는 `Courses` 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-203">Since the view doesn't have a collection of `Course` entities, the model binder can't automatically update the `Courses` navigation property.</span></span> <span data-ttu-id="480e3-204">업데이트할 모델 바인더를 사용 하는 대신 합니다 `Courses` 탐색 속성이 새 로그인 할 수 있습니다 `UpdateInstructorCourses` 메서드.</span><span class="sxs-lookup"><span data-stu-id="480e3-204">Instead of using the model binder to update the `Courses` navigation property, you'll do that in the new `UpdateInstructorCourses` method.</span></span> <span data-ttu-id="480e3-205">따라서 모델 바인딩에서 `Courses` 속성을 제외해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-205">Therefore you need to exclude the `Courses` property from model binding.</span></span> <span data-ttu-id="480e3-206">이 호출 하는 코드를 변경 하지 않아도 [tryupdatemodel에 전달](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) 를 사용 중 이므로 *허용 목록* 오버 로드 및 `Courses` 포함 목록에 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-206">This doesn't require any change to the code that calls [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) because you're using the *whitelisting* overload and `Courses` isn't in the include list.</span></span>

<span data-ttu-id="480e3-207">경우 확인란과 선택 된 코드 검사가 `UpdateInstructorCourses` 초기화를 `Courses` 빈 컬렉션을 사용 하 여 탐색 속성:</span><span class="sxs-lookup"><span data-stu-id="480e3-207">If no check boxes were selected, the code in `UpdateInstructorCourses` initializes the `Courses` navigation property with an empty collection:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

<span data-ttu-id="480e3-208">그런 다음, 코드는 데이터베이스의 모든 강좌를 반복하고 현재 강사에게 할당된 것과 보기에서 선택되었던 것에 대해 각 강좌를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-208">The code then loops through all courses in the database and checks each course against the ones currently assigned to the instructor versus the ones that were selected in the view.</span></span> <span data-ttu-id="480e3-209">효율적인 조회를 수행하기 위해 후자의 두 컬렉션은 `HashSet` 개체에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-209">To facilitate efficient lookups, the latter two collections are stored in `HashSet` objects.</span></span>

<span data-ttu-id="480e3-210">강좌에 대한 확인란이 선택됐지만 강좌가 `Instructor.Courses` 탐색 속성에 없는 경우 강좌는 탐색 속성의 컬렉션에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-210">If the check box for a course was selected but the course isn't in the `Instructor.Courses` navigation property, the course is added to the collection in the navigation property.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

<span data-ttu-id="480e3-211">강좌에 대한 확인란이 선택되지 않았지만 강좌가 `Instructor.Courses` 탐색 속성에 있는 경우 강좌는 탐색 속성에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-211">If the check box for a course wasn't selected, but the course is in the `Instructor.Courses` navigation property, the course is removed from the navigation property.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs)]

<span data-ttu-id="480e3-212">*Views\Instructor\Edit.cshtml*, 추가 **과정** 다음을 추가 하 여 확인란 배열 필드 바로 뒤에 코드를 `div` 요소에 대 한는 `OfficeAssignment` 필드 및 전에 `div` 요소를 **저장** 단추:</span><span class="sxs-lookup"><span data-stu-id="480e3-212">In *Views\Instructor\Edit.cshtml*, add a **Courses** field with an array of check boxes by adding the following code immediately after the `div` elements for the `OfficeAssignment` field and before the `div` element for the **Save** button:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml)]

<span data-ttu-id="480e3-213">붙여 넣은 후 코드를 줄 바꿈 및 들여쓰기를 보이지 않을 여기 것 처럼, 여기 같이 되도록 모든 수동으로 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-213">After you paste the code, if line breaks and indentation don't look like they do here, manually fix everything so that it looks like what you see here.</span></span> <span data-ttu-id="480e3-214">들여쓰기는 완벽할 필요가 없지만 `@</tr><tr>`, `@:<td>`, `@:</td>` 및 `@</tr>` 줄은 표시된 것처럼 각각 한 줄에 있어야 합니다. 그렇지 않으면 런타임 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-214">The indentation doesn't have to be perfect, but the `@</tr><tr>`, `@:<td>`, `@:</td>`, and `@</tr>` lines must each be on a single line as shown or you'll get a runtime error.</span></span>

<span data-ttu-id="480e3-215">이 코드는 세 개의 열이 있는 HTML 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-215">This code creates an HTML table that has three columns.</span></span> <span data-ttu-id="480e3-216">각 열은 강좌 번호 및 제목으로 구성된 캡션이 뒤에 오는 확인란입니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-216">In each column is a check box followed by a caption that consists of the course number and title.</span></span> <span data-ttu-id="480e3-217">확인란은 모두 동일한 이름 ("selectedCourses")을 그룹으로 간주 된 모델 바인더를 알리는 경우</span><span class="sxs-lookup"><span data-stu-id="480e3-217">The check boxes all have the same name ("selectedCourses"), which informs the model binder that they are to be treated as a group.</span></span> <span data-ttu-id="480e3-218">합니다 `value` 각 확인란의 특성 값으로 설정 되어 `CourseID.` 모델 바인더로 구성 된 컨트롤러에 배열 전달 페이지가 게시 되 면는 `CourseID` 확인란만 선택 하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-218">The `value` attribute of each check box is set to the value of `CourseID.` When the page is posted, the model binder passes an array to the controller that consists of the `CourseID` values for only the check boxes which are selected.</span></span>

<span data-ttu-id="480e3-219">확인란이 처음으로 렌더링 강사에 게 할당 된 강좌에 대 한 수 있는 경우 `checked` (선택 된 것으로 표시) 항목을 선택 하는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-219">When the check boxes are initially rendered, those that are for courses assigned to the instructor have `checked` attributes, which selects them (displays them checked).</span></span>

<span data-ttu-id="480e3-220">강좌 할당을 변경한 후 사이트를 반환할 때 변경 내용을 확인할 수 하려는 `Index` 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-220">After changing course assignments, you'll want to be able to verify the changes when the site returns to the `Index` page.</span></span> <span data-ttu-id="480e3-221">따라서 해당 페이지에 있는 테이블에 열을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-221">Therefore, you need to add a column to the table in that page.</span></span> <span data-ttu-id="480e3-222">이 경우 사용할 필요가 없습니다를 `ViewBag` 개체를 표시 하려는 정보를 이미 있으므로 `Courses` 의 탐색 속성을 `Instructor` 모델로 페이지로 전달 하는 엔터티.</span><span class="sxs-lookup"><span data-stu-id="480e3-222">In this case you don't need to use the `ViewBag` object, because the information you want to display is already in the `Courses` navigation property of the `Instructor` entity that you're passing to the page as the model.</span></span>

<span data-ttu-id="480e3-223">*Views\Instructor\Index.cshtml*, 추가 **과정** 머리글 바로 다음을 **Office** 다음 예제에서와 같이 제목:</span><span class="sxs-lookup"><span data-stu-id="480e3-223">In *Views\Instructor\Index.cshtml*, add a **Courses** heading immediately following the **Office** heading, as shown in the following example:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cshtml?highlight=6)]

<span data-ttu-id="480e3-224">새 정보 셀이 사무실 위치 정보 셀 바로 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-224">Then add a new detail cell immediately following the office location detail cell:</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml?highlight=7-14)]

<span data-ttu-id="480e3-225">실행 합니다 **강사 인덱스** 각 강사에 할당 된 강좌 페이지:</span><span class="sxs-lookup"><span data-stu-id="480e3-225">Run the **Instructor Index** page to see the courses assigned to each instructor:</span></span>

![Instructor_index_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

<span data-ttu-id="480e3-227">클릭 **편집** 에서 강사 편집 페이지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-227">Click **Edit** on an instructor to see the Edit page.</span></span>

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image11.png)

<span data-ttu-id="480e3-229">일부 강좌 할당을 변경 하 고 클릭 **저장할**합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-229">Change some course assignments and click **Save**.</span></span> <span data-ttu-id="480e3-230">변경 내용은 인덱스 페이지에 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-230">The changes you make are reflected on the Index page.</span></span>

 <span data-ttu-id="480e3-231">참고: 강사 강좌 데이터를 편집 하려면 다음을 수행 하는 방법은 제한 된 수의 과정 필요한 경우에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-231">Note: The approach taken here to edit instructor course data works well when there is a limited number of courses.</span></span> <span data-ttu-id="480e3-232">훨씬 큰 컬렉션의 경우 다른 UI 및 다른 업데이트 메서드가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-232">For collections that are much larger, a different UI and a different updating method would be required.</span></span>


## <a name="update-the-deleteconfirmed-method"></a><span data-ttu-id="480e3-233">DeleteConfirmed 메서드 업데이트</span><span class="sxs-lookup"><span data-stu-id="480e3-233">Update the DeleteConfirmed Method</span></span>

<span data-ttu-id="480e3-234">*InstructorController.cs*, 삭제는 `DeleteConfirmed` 그 자리에 다음 코드 메서드 및 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-234">In *InstructorController.cs*, delete the `DeleteConfirmed` method and insert the following code in its place.</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample24.cs?highlight=5-8,12-18)]

<span data-ttu-id="480e3-235">이 코드에서는 다음과 같이 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-235">This code makes the following change:</span></span>

- <span data-ttu-id="480e3-236">강사는 모든 부서의 관리자로 할당 되 면 해당 부서에서 강사 할당을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-236">If the instructor is assigned as administrator of any department, removes the instructor assignment from that department.</span></span> <span data-ttu-id="480e3-237">이 코드 없이 참조 무결성 오류가 표시 부서의 관리자로 할당 된 강사를 삭제 하 려 한 경우.</span><span class="sxs-lookup"><span data-stu-id="480e3-237">Without this code, you would get a referential integrity error if you tried to delete an instructor who was assigned as administrator for a department.</span></span>

<span data-ttu-id="480e3-238">이 코드는 한 명의 강사 여러 부서에 대 한 관리자 권한으로 할당 하는 시나리오를 처리 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-238">This code doesn't handle the scenario of one instructor assigned as administrator for multiple departments.</span></span> <span data-ttu-id="480e3-239">마지막 자습서에서에서 해당 시나리오를 방지 하는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-239">In the last tutorial you'll add code that prevents that scenario from happening.</span></span>

## <a name="add-office-location-and-courses-to-the-create-page"></a><span data-ttu-id="480e3-240">만들기 페이지에 사무실 위치 및 강좌 추가</span><span class="sxs-lookup"><span data-stu-id="480e3-240">Add office location and courses to the Create page</span></span>

<span data-ttu-id="480e3-241">*InstructorController.cs*, 삭제 합니다 `HttpGet` 하 고 `HttpPost` `Create` 메서드 그 자리에 다음 코드를 추가:</span><span class="sxs-lookup"><span data-stu-id="480e3-241">In *InstructorController.cs*, delete the `HttpGet` and `HttpPost` `Create` methods, and then add the following code in their place:</span></span>


[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample25.cs)]

<span data-ttu-id="480e3-242">이 코드 했던 편집 방법에 대 한 제외 하 고 처음 강좌가 없다는 선택 되는 것과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-242">This code is similar to what you saw for the Edit methods except that initially no courses are selected.</span></span> <span data-ttu-id="480e3-243">합니다 `HttpGet` `Create` 메서드 호출을 `PopulateAssignedCourseData` 에 빈 컬렉션을 제공 하기 위해 선택 된 강좌가 있을 때문이 아니라 메서드를 `foreach` (그렇지 않은 경우 코드 보기는는 null 참조 예외를 throw 하는 보기에서 루프 ).</span><span class="sxs-lookup"><span data-stu-id="480e3-243">The `HttpGet` `Create` method calls the `PopulateAssignedCourseData` method not because there might be courses selected but in order to provide an empty collection for the `foreach` loop in the view (otherwise the view code would throw a null reference exception).</span></span>

<span data-ttu-id="480e3-244">HttpPost 만들 메서드 선택된 된 각 강좌 유효성 검사 오류를 검사 하 고 데이터베이스에 새 강사를 추가 하는 템플릿 코드 전에 강좌 탐색 속성이 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-244">The HttpPost Create method adds each selected course to the Courses navigation property before the template code that checks for validation errors and adds the new instructor to the database.</span></span> <span data-ttu-id="480e3-245">모델 오류가 있더라도 강좌가 추가 있도록 (예를 들어 잘못 된 날짜 키가 지정 된 사용자) 모델 오류가 있을 때 수행한 선택한 모든 강좌 경우 페이지는 오류 메시지와 함께 다시 표시 됩니다 있도록 자동으로 복원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-245">Courses are added even if there are model errors so that when there are model errors (for an example, the user keyed an invalid date) so that when the page is redisplayed with an error message, any course selections that were made are automatically restored.</span></span>

<span data-ttu-id="480e3-246">`Courses` 탐색 속성에 강좌를 추가할 수 있도록 빈 컬렉션으로 속성을 초기화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-246">Notice that in order to be able to add courses to the `Courses` navigation property you have to initialize the property as an empty collection:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample26.cs)]

<span data-ttu-id="480e3-247">컨트롤러 코드에서 이 작업을 수행하는 대안으로 다음 예제와 같이 존재하지 않는 경우 자동으로 컬렉션을 만들도록 getter 속성을 변경하여 강사 모델에서 해당 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-247">As an alternative to doing this in controller code, you could do it in the Instructor model by changing the property getter to automatically create the collection if it doesn't exist, as shown in the following example:</span></span>

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample27.cs)]

<span data-ttu-id="480e3-248">이러한 방식으로 `Courses` 속성을 수정하는 경우 컨트롤러에서 명시적 속성 초기화 코드를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-248">If you modify the `Courses` property in this way, you can remove the explicit property initialization code in the controller.</span></span>

<span data-ttu-id="480e3-249">*Views\Instructor\Create.cshtml*사무실 위치 텍스트 상자를 추가 하 고는 고용 날짜 필드 후 및 하기 전에 확인란 과정 합니다 **제출** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-249">In *Views\Instructor\Create.cshtml*, add an office location text box and course check boxes after the hire date field and before the **Submit** button.</span></span>

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample28.cshtml)]

<span data-ttu-id="480e3-250">코드를 붙여 넣은 후 수정 줄 바꿈 및 들여쓰기 편집 페이지에 대 한 이전 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-250">After you paste the code, fix line breaks and indentation as you did earlier for the Edit page.</span></span>

<span data-ttu-id="480e3-251">만들기 페이지를 실행 하 고 강사를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-251">Run the Create page and add an instructor.</span></span>

![강사 강좌를 사용 하 여 만들기](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image12.png)

<a id="transactions"></a>
## <a name="handling-transactions"></a><span data-ttu-id="480e3-253">트랜잭션 처리</span><span class="sxs-lookup"><span data-stu-id="480e3-253">Handling Transactions</span></span>

<span data-ttu-id="480e3-254">에 설명 된 대로 합니다 [기본 CRUD 기능 자습서](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md), 기본적으로 Entity Framework 트랜잭션을 암시적으로 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-254">As explained in the [Basic CRUD Functionality tutorial](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md), by default the Entity Framework implicitly implements transactions.</span></span> <span data-ttu-id="480e3-255">여기서 더 본격적인 제어가 필요한-예를 들어 트랜잭션의 Entity Framework 밖에 서 수행한 작업을 포함 하려는 경우 시나리오를 참조 하세요 [트랜잭션과 작업](https://msdn.microsoft.com/data/dn456843) MSDN에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-255">For scenarios where you need more control -- for example, if you want to include operations done outside of Entity Framework in a transaction -- see [Working with Transactions](https://msdn.microsoft.com/data/dn456843) on MSDN.</span></span>

## <a name="summary"></a><span data-ttu-id="480e3-256">요약</span><span class="sxs-lookup"><span data-stu-id="480e3-256">Summary</span></span>

<span data-ttu-id="480e3-257">이제 관련된 데이터를 사용 하 여 작업 한이 소개를 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-257">You have now completed this introduction to working with related data.</span></span> <span data-ttu-id="480e3-258">지금까지 이러한 자습서에서 사용한 동기 I/O를 수행 하는 코드를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-258">So far in these tutorials you've worked with code that does synchronous I/O.</span></span> <span data-ttu-id="480e3-259">비동기 코드를 구현 하 여 웹 서버 리소스를 보다 효율적으로 사용할 응용 프로그램을 만들고 자습서에서 수행할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-259">You can make the application use web server resources more efficiently by implementing asynchronous code, and that's what you'll do in the next tutorial.</span></span>

<span data-ttu-id="480e3-260">이 자습서를 연결 하는 방법을 개선할 수 것에 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="480e3-260">Please leave feedback on how you liked this tutorial and what we could improve.</span></span>

<span data-ttu-id="480e3-261">다른 Entity Framework 리소스에 대 한 링크에서 찾을 수 있습니다 [ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="480e3-261">Links to other Entity Framework resources can be found in [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="480e3-262">[이전](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [다음](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="480e3-262">[Previous](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[Next](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application.md)</span></span>
