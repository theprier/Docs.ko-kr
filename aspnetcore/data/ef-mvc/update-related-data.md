---
title: ASP.NET Core MVC 및 EF Core - 관련 데이터 업데이트 - 7/10
author: rick-anderson
description: 이 자습서에서는 외래 키 필드 및 탐색 속성을 업데이트하여 관련된 데이터를 업데이트합니다.
ms.author: tdykstra
ms.custom: mvc
ms.date: 10/24/2018
uid: data/ef-mvc/update-related-data
ms.openlocfilehash: 37985c945f2e4b15cfcefb0c126c3209e0bdeac4
ms.sourcegitcommit: 4d74644f11e0dac52b4510048490ae731c691496
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50090735"
---
# <a name="aspnet-core-mvc-with-ef-core---update-related-data---7-of-10"></a><span data-ttu-id="c024a-103">ASP.NET Core MVC 및 EF Core - 관련 데이터 업데이트 - 7/10</span><span class="sxs-lookup"><span data-stu-id="c024a-103">ASP.NET Core MVC with EF Core - Update Related Data - 7 of 10</span></span>

[!INCLUDE [RP better than MVC](~/includes/RP-EF/rp-over-mvc-21.md)]

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="c024a-104">작성자: [Tom Dykstra](https://github.com/tdykstra) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="c024a-104">By [Tom Dykstra](https://github.com/tdykstra) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="c024a-105">Contoso University 웹 응용 프로그램 예제는 Entity Framework Core 및 Visual Studio를 사용하여 ASP.NET Core MVC 웹 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-105">The Contoso University sample web application demonstrates how to create ASP.NET Core MVC web applications using Entity Framework Core and Visual Studio.</span></span> <span data-ttu-id="c024a-106">자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](intro.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c024a-106">For information about the tutorial series, see [the first tutorial in the series](intro.md).</span></span>

<span data-ttu-id="c024a-107">이전 자습서에서는 관련 데이터를 표시했습니다. 이 자습서에서는 외래 키 필드 및 탐색 속성을 업데이트하여 관련된 데이터를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-107">In the previous tutorial you displayed related data; in this tutorial you'll update related data by updating foreign key fields and navigation properties.</span></span>

<span data-ttu-id="c024a-108">다음 그림에서는 사용할 일부 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-108">The following illustrations show some of the pages that you'll work with.</span></span>

![강좌 편집 페이지](update-related-data/_static/course-edit.png)

![강사 편집 페이지](update-related-data/_static/instructor-edit-courses.png)

## <a name="customize-the-create-and-edit-pages-for-courses"></a><span data-ttu-id="c024a-111">강좌에 대한 만들기 및 편집 페이지 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="c024a-111">Customize the Create and Edit Pages for Courses</span></span>

<span data-ttu-id="c024a-112">새 강좌 엔터티가 만들어질 때 기존 부서에 대한 관계가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-112">When a new course entity is created, it must have a relationship to an existing department.</span></span> <span data-ttu-id="c024a-113">이를 수행하기 위해 스캐폴드 코드는 컨트롤러 메서드 및 부서를 선택하기 위한 드롭다운 목록을 포함하는 만들기 및 편집 보기를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-113">To facilitate this, the scaffolded code includes controller methods and Create and Edit views that include a drop-down list for selecting the department.</span></span> <span data-ttu-id="c024a-114">드롭다운 목록은 `Course.DepartmentID` 외래 키 속성을 설정하고, 이는 적절한 부서 엔터티로 `Department` 탐색 속성을 로드하기 위해 필요한 모든 Entity Framework입니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-114">The drop-down list sets the `Course.DepartmentID` foreign key property, and that's all the Entity Framework needs in order to load the `Department` navigation property with the appropriate Department entity.</span></span> <span data-ttu-id="c024a-115">스캐폴드 코드를 사용하지만 오류 처리를 추가하고 드롭다운 목록을 정렬하도록 약간 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-115">You'll use the scaffolded code, but change it slightly to add error handling and sort the drop-down list.</span></span>

<span data-ttu-id="c024a-116">*CoursesController.cs*에서 4개의 만들기 및 편집 메서드를 삭제하고 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-116">In *CoursesController.cs*, delete the four Create and Edit methods and replace them with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_CreateGet)]

[!code-csharp[](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_CreatePost)]

[!code-csharp[](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_EditGet)]

[!code-csharp[](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_EditPost)]

<span data-ttu-id="c024a-117">`Edit` HttpPost 메서드 후에 드롭다운 목록에 대한 부서 정보를 로드하는 새 메서드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-117">After the `Edit` HttpPost method, create a new method that loads department info for the drop-down list.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/CoursesController.cs?name=snippet_Departments)]

<span data-ttu-id="c024a-118">`PopulateDepartmentsDropDownList` 메서드는 이름을 기준으로 정렬하는 모든 부서의 목록을 가져오고, 드롭다운 목록에 대한 `SelectList` 컬렉션을 만들고, 컬렉션을 `ViewBag`의 보기에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-118">The `PopulateDepartmentsDropDownList` method gets a list of all departments sorted by name, creates a `SelectList` collection for a drop-down list, and passes the collection to the view in `ViewBag`.</span></span> <span data-ttu-id="c024a-119">메서드는 호출 코드가 드롭다운 목록이 렌더링될 때 선택될 항목을 지정하도록 허용하는 선택적 `selectedDepartment` 매개 변수를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-119">The method accepts the optional `selectedDepartment` parameter that allows the calling code to specify the item that will be selected when the drop-down list is rendered.</span></span> <span data-ttu-id="c024a-120">보기가 "DepartmentID"라는 이름을 `<select>` 태그 도우미에 전달하면 도우미는 "DepartmentID"라는 `SelectList`에 대한 `ViewBag` 개체에서 보는 것을 압니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-120">The view will pass the name "DepartmentID" to the `<select>` tag helper, and the helper then knows to look in the `ViewBag` object for a `SelectList` named "DepartmentID".</span></span>

<span data-ttu-id="c024a-121">새 강좌의 경우 부서는 아직 설정되지 않기 때문에 HttpGet `Create` 메서드는 선택한 항목을 설정하지 않고 `PopulateDepartmentsDropDownList` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-121">The HttpGet `Create` method calls the `PopulateDepartmentsDropDownList` method without setting the selected item, because for a new course the department isn't established yet:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/CoursesController.cs?highlight=3&name=snippet_CreateGet)]

<span data-ttu-id="c024a-122">HttpGet `Edit` 메서드는 편집 중인 강좌에 이미 할당되어 있는 부서의 ID에 따라 선택한 항목을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-122">The HttpGet `Edit` method sets the selected item, based on the ID of the department that's already assigned to the course being edited:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/CoursesController.cs?highlight=15&name=snippet_EditGet)]

<span data-ttu-id="c024a-123">`Create` 및 `Edit` 모두에 대한 HttpPost 메서드는 오류가 발생한 후 페이지를 다시 표시할 때 선택한 항목을 설정하는 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-123">The HttpPost methods for both `Create` and `Edit` also include code that sets the selected item when they redisplay the page after an error.</span></span> <span data-ttu-id="c024a-124">이렇게 하면 오류 메시지를 표시하기 위해 페이지가 다시 표시될 때 선택한 부서에 관계 없이 선택된 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-124">This ensures that when the page is redisplayed to show the error message, whatever department was selected stays selected.</span></span>

### <a name="add-asnotracking-to-details-and-delete-methods"></a><span data-ttu-id="c024a-125">세부 정보 및 삭제 메서드에 AsNoTracking 추가</span><span class="sxs-lookup"><span data-stu-id="c024a-125">Add .AsNoTracking to Details and Delete methods</span></span>

<span data-ttu-id="c024a-126">강좌 세부 정보 및 삭제 페이지의 성능을 최적화하기 위해 `Details` 및 HttpGet `Delete` 메서드에 `AsNoTracking` 호출을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-126">To optimize performance of the Course Details and Delete pages, add `AsNoTracking` calls in the `Details` and HttpGet `Delete` methods.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/CoursesController.cs?highlight=10&name=snippet_Details)]

[!code-csharp[](intro/samples/cu/Controllers/CoursesController.cs?highlight=10&name=snippet_DeleteGet)]

### <a name="modify-the-course-views"></a><span data-ttu-id="c024a-127">강좌 보기 수정</span><span class="sxs-lookup"><span data-stu-id="c024a-127">Modify the Course views</span></span>

<span data-ttu-id="c024a-128">*Views/Courses/Create.cshtml*에서 **부서** 드롭다운 목록에 "부서 선택" 옵션을 추가하고, **DepartmentID**에서  **부서**로 캡션을 변경하고, 유효성 검사 메시지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-128">In *Views/Courses/Create.cshtml*, add a "Select Department" option to the **Department** drop-down list, change the caption from **DepartmentID** to **Department**, and add a validation message.</span></span>

[!code-html[](intro/samples/cu/Views/Courses/Create.cshtml?highlight=2-6&range=29-34)]

<span data-ttu-id="c024a-129">*Views/Courses/Edit.cshtml*에서 부서 필드에 대해 *Create.cshtml*에서 수행한 동일한 변경 내용을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-129">In *Views/Courses/Edit.cshtml*, make the same change for the Department field that you just did in *Create.cshtml*.</span></span>

<span data-ttu-id="c024a-130">또한 *Views/Courses/Edit.cshtml*에서 **제목** 필드 전에 강좌 번호 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-130">Also in *Views/Courses/Edit.cshtml*, add a course number field before the **Title** field.</span></span> <span data-ttu-id="c024a-131">강좌 번호는 기본 키이기 때문에 표시되지만 변경될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-131">Because the course number is the primary key, it's displayed, but it can't be changed.</span></span>

[!code-html[](intro/samples/cu/Views/Courses/Edit.cshtml?range=15-18)]

<span data-ttu-id="c024a-132">편집 보기에 강좌 번호에 대해 이미 숨겨진 필드(`<input type="hidden">`)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-132">There's already a hidden field (`<input type="hidden">`) for the course number in the Edit view.</span></span> <span data-ttu-id="c024a-133">사용자가 **편집** 페이지에서 **저장**을 클릭할 때 강좌 번호가 게시된 데이터에 삽입되도록 하지 않으므로 `<label>` 태그 도우미를 추가하는 것은 숨겨진 필드에 대한 필요성을 없애지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-133">Adding a `<label>` tag helper doesn't eliminate the need for the hidden field because it doesn't cause the course number to be included in the posted data when the user clicks **Save** on the **Edit** page.</span></span>

<span data-ttu-id="c024a-134">*Views/Courses/Delete.cshtml*에서 위쪽에 강좌 번호 필드를 추가하고 부서 ID를 부서 이름으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-134">In *Views/Courses/Delete.cshtml*, add a course number field at the top and change department ID to department name.</span></span>

[!code-html[](intro/samples/cu/Views/Courses/Delete.cshtml?highlight=14-19,36)]

<span data-ttu-id="c024a-135">*Views/Courses/Details.cshtml*에서 *Delete.cshtml*에 대해 수행한 동일한 변경 내용을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-135">In *Views/Courses/Details.cshtml*, make the same change that you just did for *Delete.cshtml*.</span></span>

### <a name="test-the-course-pages"></a><span data-ttu-id="c024a-136">강좌 페이지 테스트</span><span class="sxs-lookup"><span data-stu-id="c024a-136">Test the Course pages</span></span>

<span data-ttu-id="c024a-137">앱을 실행하고, **강좌** 탭을 선택하고, **새로 만들기**를 클릭하고, 새 강좌에 대한 데이터를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-137">Run the app, select the **Courses** tab, click **Create New**, and enter data for a new course:</span></span>

![강좌 만들기 페이지](update-related-data/_static/course-create.png)

<span data-ttu-id="c024a-139">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-139">Click **Create**.</span></span> <span data-ttu-id="c024a-140">강좌 인덱스 페이지가 목록에 추가된 새 강좌로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-140">The Courses Index page is displayed with the new course added to the list.</span></span> <span data-ttu-id="c024a-141">인덱스 페이지 목록의 부서 이름은 관계가 올바르게 설정되었음을 표시하는 탐색 속성에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-141">The department name in the Index page list comes from the navigation property, showing that the relationship was established correctly.</span></span>

<span data-ttu-id="c024a-142">강좌 인덱스 페이지의 강좌에서 **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-142">Click **Edit** on a course in the Courses Index page.</span></span>

![강좌 편집 페이지](update-related-data/_static/course-edit.png)

<span data-ttu-id="c024a-144">페이지에서 데이터를 변경하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-144">Change data on the page and click **Save**.</span></span> <span data-ttu-id="c024a-145">강좌 인덱스 페이지가 업데이트된 강좌 데이터로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-145">The Courses Index page is displayed with the updated course data.</span></span>

## <a name="add-an-edit-page-for-instructors"></a><span data-ttu-id="c024a-146">강사에 대한 편집 페이지 추가</span><span class="sxs-lookup"><span data-stu-id="c024a-146">Add an Edit Page for Instructors</span></span>

<span data-ttu-id="c024a-147">강사 레코드를 편집할 때 강사의 사무실 할당을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-147">When you edit an instructor record, you want to be able to update the instructor's office assignment.</span></span> <span data-ttu-id="c024a-148">강사 엔터티에는 OfficeAssignment 엔터티와 일대영 또는 일 관계가 있으며 코드가 다음과 같은 경우를 처리해야 함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-148">The Instructor entity has a one-to-zero-or-one relationship with the OfficeAssignment entity, which means your code has to handle the following situations:</span></span>

* <span data-ttu-id="c024a-149">사용자가 사무실 할당 선택을 취소하고 원래 값이 있었던 경우 OfficeAssignment 엔터티를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-149">If the user clears the office assignment and it originally had a value, delete the OfficeAssignment entity.</span></span>

* <span data-ttu-id="c024a-150">사용자가 사무실 할당 값을 입력하고 원래 값이 비어 있었던 경우 새 OfficeAssignment 엔터티를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-150">If the user enters an office assignment value and it originally was empty, create a new OfficeAssignment entity.</span></span>

* <span data-ttu-id="c024a-151">사용자가 사무실 할당의 값을 변경하는 경우 기존 OfficeAssignment 엔터티의 값을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-151">If the user changes the value of an office assignment, change the value in an existing OfficeAssignment entity.</span></span>

### <a name="update-the-instructors-controller"></a><span data-ttu-id="c024a-152">강사 컨트롤러 업데이트</span><span class="sxs-lookup"><span data-stu-id="c024a-152">Update the Instructors controller</span></span>

<span data-ttu-id="c024a-153">*InstructorsController.cs*에서 강사 엔터티의 `OfficeAssignment` 탐색 속성을 로드하고 `AsNoTracking`을 호출하도록 HttpGet `Edit` 메서드에서 코드를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-153">In *InstructorsController.cs*, change the code in the HttpGet `Edit` method so that it loads the Instructor entity's `OfficeAssignment` navigation property and calls `AsNoTracking`:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?highlight=9,10&name=snippet_EditGetOA)]

<span data-ttu-id="c024a-154">HttpPost `Edit` 메서드를 다음 코드로 바꿔 사무실 할당 업데이트를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-154">Replace the HttpPost `Edit` method with the following code to handle office assignment updates:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_EditPostOA)]

<span data-ttu-id="c024a-155">코드는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-155">The code does the following:</span></span>

-  <span data-ttu-id="c024a-156">서명은 이제 HttpGet `Edit` 메서드와 동일하므로 메서드 이름을 `EditPost`로 변경합니다(`ActionName` 특성은 `/Edit/` URL이 여전히 사용됨을 지정함).</span><span class="sxs-lookup"><span data-stu-id="c024a-156">Changes the method name to `EditPost` because the signature is now the same as the HttpGet `Edit` method (the `ActionName` attribute specifies that the `/Edit/` URL is still used).</span></span>

-  <span data-ttu-id="c024a-157">`OfficeAssignment` 탐색 속성에 대한 즉시 로드를 사용하여 데이터베이스에서 현재 강사 엔터티를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-157">Gets the current Instructor entity from the database using eager loading for the `OfficeAssignment` navigation property.</span></span> <span data-ttu-id="c024a-158">이는 HttpGet `Edit` 메서드에서 수행한 것과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-158">This is the same as what you did in the HttpGet `Edit` method.</span></span>

-  <span data-ttu-id="c024a-159">모델 바인더의 값으로 검색된 강사 엔터티를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-159">Updates the retrieved Instructor entity with values from the model binder.</span></span> <span data-ttu-id="c024a-160">`TryUpdateModel` 오버로드를 통해 포함하려는 속성을 허용 목록에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-160">The `TryUpdateModel` overload enables you to whitelist the properties you want to include.</span></span> <span data-ttu-id="c024a-161">이렇게 하면 [두 번째 자습서](crud.md)에 설명된 대로 초과 게시를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-161">This prevents over-posting, as explained in the [second tutorial](crud.md).</span></span>

    <!-- Snippets don't play well with <ul> [!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?range=241-244)] -->

    ```csharp
    if (await TryUpdateModelAsync<Instructor>(
        instructorToUpdate,
        "",
        i => i.FirstMidName, i => i.LastName, i => i.HireDate, i => i.OfficeAssignment))
    ```

-   <span data-ttu-id="c024a-162">사무실 위치가 비어 있는 경우 OfficeAssignment 테이블의 관련된 행이 삭제되도록 Instructor.OfficeAssignment 속성을 Null로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-162">If the office location is blank, sets the Instructor.OfficeAssignment property to null so that the related row in the OfficeAssignment table will be deleted.</span></span>

    <!-- Snippets don't play well with <ul>  "intro/samples/cu/Controllers/InstructorsController.cs"} -->

    ```csharp
    if (String.IsNullOrWhiteSpace(instructorToUpdate.OfficeAssignment?.Location))
    {
        instructorToUpdate.OfficeAssignment = null;
    }
    ```

- <span data-ttu-id="c024a-163">변경 내용을 데이터베이스에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-163">Saves the changes to the database.</span></span>

### <a name="update-the-instructor-edit-view"></a><span data-ttu-id="c024a-164">강사 편집 보기 업데이트</span><span class="sxs-lookup"><span data-stu-id="c024a-164">Update the Instructor Edit view</span></span>

<span data-ttu-id="c024a-165">*Views/Instructors/Edit.cshtml*에서 **저장** 단추 앞의 끝에 사무실 위치를 편집하기 위해 새 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-165">In *Views/Instructors/Edit.cshtml*, add a new field for editing the office location, at the end before the **Save** button:</span></span>

[!code-html[](intro/samples/cu/Views/Instructors/Edit.cshtml?range=30-34)]

<span data-ttu-id="c024a-166">앱을 실행하고, **강사** 탭을 선택한 다음, 강사에서 **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-166">Run the app, select the **Instructors** tab, and then click **Edit** on an instructor.</span></span> <span data-ttu-id="c024a-167">**사무실 위치**를 변경하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-167">Change the **Office Location** and click **Save**.</span></span>

![강사 편집 페이지](update-related-data/_static/instructor-edit-office.png)

## <a name="add-course-assignments-to-the-instructor-edit-page"></a><span data-ttu-id="c024a-169">강사 편집 페이지에 강좌 할당 추가</span><span class="sxs-lookup"><span data-stu-id="c024a-169">Add Course assignments to the Instructor Edit page</span></span>

<span data-ttu-id="c024a-170">강사는 강좌 수에 관계 없이 가르칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-170">Instructors may teach any number of courses.</span></span> <span data-ttu-id="c024a-171">이제 다음 스크린샷에 표시된 것처럼 확인란 그룹을 사용하여 강좌 할당을 변경하는 기능을 추가하여 강사 편집 페이지를 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-171">Now you'll enhance the Instructor Edit page by adding the ability to change course assignments using a group of check boxes, as shown in the following screen shot:</span></span>

![강좌가 있는 강사 편집 페이지](update-related-data/_static/instructor-edit-courses.png)

<span data-ttu-id="c024a-173">강좌와 강사 엔터티 간의 관계는 다대다입니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-173">The relationship between the Course and Instructor entities is many-to-many.</span></span> <span data-ttu-id="c024a-174">관계를 추가하고 제거하려면 CourseAssignments 조인 엔터티 집합 간에 엔터티를 추가하고 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-174">To add and remove relationships, you add and remove entities to and from the CourseAssignments join entity set.</span></span>

<span data-ttu-id="c024a-175">강사에게 할당된 강좌를 변경할 수 있도록 하는 UI는 확인란의 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-175">The UI that enables you to change which courses an instructor is assigned to is a group of check boxes.</span></span> <span data-ttu-id="c024a-176">데이터베이스의 모든 강좌에 대한 확인란이 표시되고 강사에게 현재 할당되어 있는 것이 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-176">A check box for every course in the database is displayed, and the ones that the instructor is currently assigned to are selected.</span></span> <span data-ttu-id="c024a-177">사용자는 확인란을 선택하거나 선택 취소하여 강좌 할당을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-177">The user can select or clear check boxes to change course assignments.</span></span> <span data-ttu-id="c024a-178">강좌의 수가 훨씬 큰 경우 보기에서 데이터를 나타내는 다른 방법을 사용하길 원할 것입니다. 하지만 관계를 만들거나 삭제하기 위해 조인 엔터티를 조작하는 동일한 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-178">If the number of courses were much greater, you would probably want to use a different method of presenting the data in the view, but you'd use the same method of manipulating a join entity to create or delete relationships.</span></span>

### <a name="update-the-instructors-controller"></a><span data-ttu-id="c024a-179">강사 컨트롤러 업데이트</span><span class="sxs-lookup"><span data-stu-id="c024a-179">Update the Instructors controller</span></span>

<span data-ttu-id="c024a-180">확인란의 목록에 대한 보기에 데이터를 제공하려면 보기 모델 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-180">To provide data to the view for the list of check boxes, you'll use a view model class.</span></span>

<span data-ttu-id="c024a-181">*SchoolViewModels* 폴더에서 *AssignedCourseData.cs*를 만들고 기존 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-181">Create *AssignedCourseData.cs* in the *SchoolViewModels* folder and replace the existing code with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Models/SchoolViewModels/AssignedCourseData.cs)]

<span data-ttu-id="c024a-182">*InstructorsController.cs*에서 HttpGet `Edit` 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-182">In *InstructorsController.cs*, replace the HttpGet `Edit` method with the following code.</span></span> <span data-ttu-id="c024a-183">변경 내용은 강조 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-183">The changes are highlighted.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?highlight=10,17,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36&name=snippet_EditGetCourses)]

<span data-ttu-id="c024a-184">코드는 `Courses` 탐색 속성에 대해 즉시 로드를 추가하고 새 `PopulateAssignedCourseData` 메서드를 호출하여 `AssignedCourseData` 보기 모델 클래스를 사용하여 확인란 배열에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-184">The code adds eager loading for the `Courses` navigation property and calls the new `PopulateAssignedCourseData` method to provide information for the check box array using the `AssignedCourseData` view model class.</span></span>

<span data-ttu-id="c024a-185">`PopulateAssignedCourseData` 메서드의 코드는 보기 모델 클래스를 사용하는 강좌의 목록을 로드하기 위해 모든 강좌 엔터티를 통해 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-185">The code in the `PopulateAssignedCourseData` method reads through all Course entities in order to load a list of courses using the view model class.</span></span> <span data-ttu-id="c024a-186">각 강좌의 경우 코드는 강좌가 강사의 `Courses` 탐색 속성에 있는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-186">For each course, the code checks whether the course exists in the instructor's `Courses` navigation property.</span></span> <span data-ttu-id="c024a-187">강좌가 강사에게 할당되었는지 여부를 확인할 때 효율적인 조회를 만들기 위해 강사에게 할당된 강좌는 `HashSet` 컬렉션에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-187">To create efficient lookup when checking whether a course is assigned to the instructor, the courses assigned to the instructor are put into a `HashSet` collection.</span></span> <span data-ttu-id="c024a-188">`Assigned` 속성은 강사에게 할당된 강좌에 대해 true로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-188">The `Assigned` property  is set to true for courses the instructor is assigned to.</span></span> <span data-ttu-id="c024a-189">보기는 이 속성을 사용하여 선택된 것으로 표시되어야 하는 확인란을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-189">The view will use this property to determine which check boxes must be displayed as selected.</span></span> <span data-ttu-id="c024a-190">마지막으로 목록은 `ViewData`의 보기에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-190">Finally, the list is passed to the view in `ViewData`.</span></span>

<span data-ttu-id="c024a-191">다음으로 사용자가 **저장**을 클릭할 때 실행되는 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-191">Next, add the code that's executed when the user clicks **Save**.</span></span> <span data-ttu-id="c024a-192">`EditPost` 메서드를 다음 코드를 바꾸고, 강사 엔터티의 `Courses` 탐색 속성을 업데이트하는 새 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-192">Replace the `EditPost` method with the following code, and add a new method that updates the `Courses` navigation property of the Instructor entity.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?highlight=1,3,12,13,25,39-40&name=snippet_EditPostCourses)]

[!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_UpdateCourses&highlight=1-31)]

<span data-ttu-id="c024a-193">메서드 서명은 이제 HttpGet `Edit` 메서드와 다르므로 메서드 이름은 `EditPost`에서 `Edit`로 다시 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-193">The method signature is now different from the HttpGet `Edit` method, so the method name changes from `EditPost` back to `Edit`.</span></span>

<span data-ttu-id="c024a-194">보기에는 강좌 엔터티의 컬렉션이 없으므로 모델 바인더는 `CourseAssignments` 탐색 속성을 자동으로 업데이트할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-194">Since the view doesn't have a collection of Course entities, the model binder can't automatically update the `CourseAssignments` navigation property.</span></span> <span data-ttu-id="c024a-195">`CourseAssignments` 탐색 속성을 업데이트하는 데 모델 바인더를 사용하는 대신 새 `UpdateInstructorCourses` 메서드에서 해당 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-195">Instead of using the model binder to update the `CourseAssignments` navigation property, you do that in the new `UpdateInstructorCourses` method.</span></span> <span data-ttu-id="c024a-196">따라서 모델 바인딩에서 `CourseAssignments` 속성을 제외해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-196">Therefore you need to exclude the `CourseAssignments` property from model binding.</span></span> <span data-ttu-id="c024a-197">허용 목록 오버로드를 사용하고 있으며 `CourseAssignments`는 포함 목록에 있지 않으므로 `TryUpdateModel`을 호출하는 코드에 변경 내용을 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-197">This doesn't require any change to the code that calls `TryUpdateModel` because you're using the whitelisting overload and `CourseAssignments` isn't in the include list.</span></span>

<span data-ttu-id="c024a-198">확인란이 선택되지 않은 경우 `UpdateInstructorCourses`의 코드는 빈 컬렉션으로 `CourseAssignments` 탐색 속성을 초기화하고 다음을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-198">If no check boxes were selected, the code in `UpdateInstructorCourses` initializes the `CourseAssignments` navigation property with an empty collection and returns:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_UpdateCourses&highlight=3-7)]

<span data-ttu-id="c024a-199">그런 다음, 코드는 데이터베이스의 모든 강좌를 반복하고 현재 강사에게 할당된 것과 보기에서 선택되었던 것에 대해 각 강좌를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-199">The code then loops through all courses in the database and checks each course against the ones currently assigned to the instructor versus the ones that were selected in the view.</span></span> <span data-ttu-id="c024a-200">효율적인 조회를 수행하기 위해 후자의 두 컬렉션은 `HashSet` 개체에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-200">To facilitate efficient lookups, the latter two collections are stored in `HashSet` objects.</span></span>

<span data-ttu-id="c024a-201">강좌에 대한 확인란이 선택됐지만 강좌가 `Instructor.CourseAssignments` 탐색 속성에 없는 경우 강좌는 탐색 속성의 컬렉션에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-201">If the check box for a course was selected but the course isn't in the `Instructor.CourseAssignments` navigation property, the course is added to the collection in the navigation property.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?highlight=14-20&name=snippet_UpdateCourses)]

<span data-ttu-id="c024a-202">강좌에 대한 확인란이 선택되지 않았지만 강좌가 `Instructor.CourseAssignments` 탐색 속성에 있는 경우 강좌는 탐색 속성에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-202">If the check box for a course wasn't selected, but the course is in the `Instructor.CourseAssignments` navigation property, the course is removed from the navigation property.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?highlight=21-29&name=snippet_UpdateCourses)]

### <a name="update-the-instructor-views"></a><span data-ttu-id="c024a-203">강사 보기 업데이트</span><span class="sxs-lookup"><span data-stu-id="c024a-203">Update the Instructor views</span></span>

<span data-ttu-id="c024a-204">*Views/Instructors/Edit.cshtml*에서 **사무실** 필드에 대한 `div` 요소 후와 **저장** 단추에 대한 `div` 요소 전에 다음 코드를 즉시 추가하여 확인란의 배열로 **강좌** 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-204">In *Views/Instructors/Edit.cshtml*, add a **Courses** field with an array of check boxes by adding the following code immediately after the `div` elements for the **Office** field and before the `div` element for the **Save** button.</span></span>

<a id="notepad"></a>
> [!NOTE]
> <span data-ttu-id="c024a-205">Visual Studio에서 코드를 붙여 넣을 때 줄 바꿈이 코드를 중단하는 방식으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-205">When you paste the code in Visual Studio, line breaks will be changed in a way that breaks the code.</span></span>  <span data-ttu-id="c024a-206">자동 서식 지정을 실행 취소하려면 Ctrl+Z를 한 번 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-206">Press Ctrl+Z one time to undo the automatic formatting.</span></span>  <span data-ttu-id="c024a-207">여기와 같은 모양이 되도록 줄 바꿈을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-207">This will fix the line breaks so that they look like what you see here.</span></span> <span data-ttu-id="c024a-208">들여쓰기는 완벽할 필요가 없지만 `@</tr><tr>`, `@:<td>`, `@:</td>` 및 `@:</tr>` 줄은 표시된 것처럼 각각 한 줄에 있어야 합니다. 그렇지 않으면 런타임 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-208">The indentation doesn't have to be perfect, but the `@</tr><tr>`, `@:<td>`, `@:</td>`, and `@:</tr>` lines must each be on a single line as shown or you'll get a runtime error.</span></span> <span data-ttu-id="c024a-209">선택된 새 코드의 블록과 함께 Tab 키를 세 번 눌러 기존 코드와 함께 새 코드를 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-209">With the block of new code selected, press Tab three times to line up the new code with the existing code.</span></span> <span data-ttu-id="c024a-210">[여기](https://developercommunity.visualstudio.com/content/problem/147795/razor-editor-malforms-pasted-markup-and-creates-in.html)합니다.에서 이 문제의 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-210">You can check the status of this problem [here](https://developercommunity.visualstudio.com/content/problem/147795/razor-editor-malforms-pasted-markup-and-creates-in.html).</span></span>

[!code-html[](intro/samples/cu/Views/Instructors/Edit.cshtml?range=35-61)]

<span data-ttu-id="c024a-211">이 코드는 세 개의 열이 있는 HTML 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-211">This code creates an HTML table that has three columns.</span></span> <span data-ttu-id="c024a-212">각 열은 강좌 번호 및 제목으로 구성된 캡션이 뒤에 오는 확인란입니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-212">In each column is a check box followed by a caption that consists of the course number and title.</span></span> <span data-ttu-id="c024a-213">확인란은 모두 모델 바인더에게 그룹으로 간주된다는 것을 알리는 동일한 이름("selectedCourses")을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-213">The check boxes all have the same name ("selectedCourses"), which informs the model binder that they're to be treated as a group.</span></span> <span data-ttu-id="c024a-214">각 확인란의 값 특성은 `CourseID`의 값으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-214">The value attribute of each check box is set to the value of `CourseID`.</span></span> <span data-ttu-id="c024a-215">페이지가 게시되면 모델 바인더는 선택된 확인란에 대한 `CourseID` 값으로 구성된 배열을 컨트롤러에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-215">When the page is posted, the model binder passes an array to the controller that consists of the `CourseID` values for only the check boxes which are selected.</span></span>

<span data-ttu-id="c024a-216">확인란이 처음으로 렌더링될 때 강사에게 할당된 강좌에 대한 것은 해당 항목을 선택하는 특성을 선택했습니다(선택된 것으로 표시).</span><span class="sxs-lookup"><span data-stu-id="c024a-216">When the check boxes are initially rendered, those that are for courses assigned to the instructor have checked attributes, which selects them (displays them checked).</span></span>

<span data-ttu-id="c024a-217">앱을 실행하고, **강사** 탭을 선택하고, 강사에서 **편집**을 클릭하여 **편집** 페이지를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-217">Run the app, select the **Instructors** tab, and click **Edit** on an instructor to see the **Edit** page.</span></span>

![강좌가 있는 강사 편집 페이지](update-related-data/_static/instructor-edit-courses.png)

<span data-ttu-id="c024a-219">일부 강좌 할당을 변경하고 저장을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-219">Change some course assignments and click Save.</span></span> <span data-ttu-id="c024a-220">변경 내용은 인덱스 페이지에 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-220">The changes you make are reflected on the Index page.</span></span>

> [!NOTE]
> <span data-ttu-id="c024a-221">강사 강좌 데이터를 편집하기 위해 여기에 적용되는 방법은 제한된 수의 강좌가 있는 경우에 잘 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-221">The approach taken here to edit instructor course data works well when there's a limited number of courses.</span></span> <span data-ttu-id="c024a-222">훨씬 큰 컬렉션의 경우 다른 UI 및 다른 업데이트 메서드가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-222">For collections that are much larger, a different UI and a different updating method would be required.</span></span>

## <a name="update-the-delete-page"></a><span data-ttu-id="c024a-223">삭제 페이지 업데이트</span><span class="sxs-lookup"><span data-stu-id="c024a-223">Update the Delete page</span></span>

<span data-ttu-id="c024a-224">*InstructorsController.cs*에서 `DeleteConfirmed` 메서드를 삭제하고 해당 위치에 다음 코드를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-224">In *InstructorsController.cs*, delete the `DeleteConfirmed` method and insert the following code in its place.</span></span>

[!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?highlight=5-7,9-12&name=snippet_DeleteConfirmed)]

<span data-ttu-id="c024a-225">이 코드로 다음이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-225">This code makes the following changes:</span></span>

* <span data-ttu-id="c024a-226">`CourseAssignments` 탐색 속성에 대해 즉시 로드를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-226">Does eager loading for the `CourseAssignments` navigation property.</span></span>  <span data-ttu-id="c024a-227">이를 포함해야 합니다. 그렇지 않으면 EF는 관련된 `CourseAssignment` 엔터티에 대해 알지 못하고 삭제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-227">You have to include this or EF won't know about related `CourseAssignment` entities and won't delete them.</span></span>  <span data-ttu-id="c024a-228">읽을 필요가 없도록 하려면 여기에서 데이터베이스에 계단식 삭제를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-228">To avoid needing to read them here you could configure cascade delete in the database.</span></span>

* <span data-ttu-id="c024a-229">삭제될 강사가 부서의 관리자로 할당된 경우 해당 부서에서 강사 할당을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-229">If the instructor to be deleted is assigned as administrator of any departments, removes the instructor assignment from those departments.</span></span>

## <a name="add-office-location-and-courses-to-the-create-page"></a><span data-ttu-id="c024a-230">만들기 페이지에 사무실 위치 및 강좌 추가</span><span class="sxs-lookup"><span data-stu-id="c024a-230">Add office location and courses to the Create page</span></span>

<span data-ttu-id="c024a-231">*InstructorsController.cs*에서 HttpGet 및 HttpPost `Create` 메서드를 삭제한 다음, 해당 위치에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-231">In *InstructorsController.cs*, delete the HttpGet and HttpPost `Create` methods, and then add the following code in their place:</span></span>

[!code-csharp[](intro/samples/cu/Controllers/InstructorsController.cs?name=snippet_Create&highlight=3-5,12,14-22,29)]

<span data-ttu-id="c024a-232">이 코드는 처음에 선택된 강좌가 없다는 것을 제외하고 `Edit` 메서드에 대해 확인한 것과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-232">This code is similar to what you saw for the `Edit` methods except that initially no courses are selected.</span></span> <span data-ttu-id="c024a-233">선택된 강좌가 있을 수 있기 때문이 아니라 보기의 `foreach` 반복에 대해 빈 컬렉션을 제공하기 위해 HttpGet `Create` 메서드는 `PopulateAssignedCourseData` 메서드를 호출합니다(그렇지 않은 경우 보기 코드는 null 참조 예외를 throw함).</span><span class="sxs-lookup"><span data-stu-id="c024a-233">The HttpGet `Create` method calls the `PopulateAssignedCourseData` method not because there might be courses selected but in order to provide an empty collection for the `foreach` loop in the view (otherwise the view code would throw a null reference exception).</span></span>

<span data-ttu-id="c024a-234">HttpPost `Create` 메서드는 유효성 검사 오류를 확인하고 데이터베이스에 새 강사를 추가하기 전에 `CourseAssignments` 탐색 속성에 선택된 각 강좌를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-234">The HttpPost `Create` method adds each selected course to the `CourseAssignments` navigation property before it checks for validation errors and adds the new instructor to the database.</span></span> <span data-ttu-id="c024a-235">모델 오류가 있더라도 강좌가 추가되므로 모델 오류가 있는 경우(예: 사용자가 잘못된 날짜를 키 지정함) 페이지는 오류 메시지와 함께 다시 표시되고, 선택한 모든 강좌는 자동으로 다시 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-235">Courses are added even if there are model errors so that when there are model errors (for an example, the user keyed an invalid date), and the page is redisplayed with an error message, any course selections that were made are automatically restored.</span></span>

<span data-ttu-id="c024a-236">`CourseAssignments` 탐색 속성에 강좌를 추가할 수 있도록 빈 컬렉션으로 속성을 초기화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-236">Notice that in order to be able to add courses to the `CourseAssignments` navigation property you have to initialize the property as an empty collection:</span></span>

```csharp
instructor.CourseAssignments = new List<CourseAssignment>();
```

<span data-ttu-id="c024a-237">컨트롤러 코드에서 이 작업을 수행하는 대안으로 다음 예제와 같이 존재하지 않는 경우 자동으로 컬렉션을 만들도록 getter 속성을 변경하여 강사 모델에서 해당 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-237">As an alternative to doing this in controller code, you could do it in the Instructor model by changing the property getter to automatically create the collection if it doesn't exist, as shown in the following example:</span></span>

```csharp
private ICollection<CourseAssignment> _courseAssignments;
public ICollection<CourseAssignment> CourseAssignments
{
    get
    {
        return _courseAssignments ?? (_courseAssignments = new List<CourseAssignment>());
    }
    set
    {
        _courseAssignments = value;
    }
}
```

<span data-ttu-id="c024a-238">이러한 방식으로 `CourseAssignments` 속성을 수정하는 경우 컨트롤러에서 명시적 속성 초기화 코드를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-238">If you modify the `CourseAssignments` property in this way, you can remove the explicit property initialization code in the controller.</span></span>

<span data-ttu-id="c024a-239">*Views/Instructor/Create.cshtml*에서 사무실 위치 텍스트 상자와 제출 단추 전에 강좌에 대한 확인란을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-239">In *Views/Instructor/Create.cshtml*, add an office location text box and check boxes for courses before the Submit button.</span></span> <span data-ttu-id="c024a-240">편집 페이지의 경우와 같이 [Visual Studio에서 붙여넣을 때 코드의 서식을 다시 지정하는 경우 서식 지정을 수정합니다](#notepad).</span><span class="sxs-lookup"><span data-stu-id="c024a-240">As in the case of the Edit page, [fix the formatting if Visual Studio reformats the code when you paste it](#notepad).</span></span>

[!code-html[](intro/samples/cu/Views/Instructors/Create.cshtml?range=29-61)]

<span data-ttu-id="c024a-241">앱을 실행하고 강사를 만들어 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-241">Test by running the app and creating an instructor.</span></span>

## <a name="handling-transactions"></a><span data-ttu-id="c024a-242">트랜잭션 처리</span><span class="sxs-lookup"><span data-stu-id="c024a-242">Handling Transactions</span></span>

<span data-ttu-id="c024a-243">[CRUD 자습서](crud.md)에 설명된 대로 Entity Framework는 트랜잭션을 암시적으로 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-243">As explained in the [CRUD tutorial](crud.md), the Entity Framework implicitly implements transactions.</span></span> <span data-ttu-id="c024a-244">더 많은 컨트롤이 필요한 시나리오의 경우, 예를 들어 트랜잭션의 Entity Framework 밖에서 수행한 작업을 포함하려는 경우 [트랜잭션](/ef/core/saving/transactions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c024a-244">For scenarios where you need more control -- for example, if you want to include operations done outside of Entity Framework in a transaction -- see [Transactions](/ef/core/saving/transactions).</span></span>

## <a name="summary"></a><span data-ttu-id="c024a-245">요약</span><span class="sxs-lookup"><span data-stu-id="c024a-245">Summary</span></span>

<span data-ttu-id="c024a-246">이제 관련된 데이터 사용에 대한 소개를 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-246">You have now completed the introduction to working with related data.</span></span> <span data-ttu-id="c024a-247">다음 자습서에서는 동시성 충돌을 처리하는 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c024a-247">In the next tutorial you'll see how to handle concurrency conflicts.</span></span>

::: moniker-end

> [!div class="step-by-step"]
> <span data-ttu-id="c024a-248">[이전](read-related-data.md)
> [다음](concurrency.md)</span><span class="sxs-lookup"><span data-stu-id="c024a-248">[Previous](read-related-data.md)
[Next](concurrency.md)</span></span>
