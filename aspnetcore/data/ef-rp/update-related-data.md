---
title: "EF 코어-를 사용 하 여 razor 페이지 관련된 데이터-7/8 업데이트"
author: rick-anderson
description: "이 자습서에서는 외래 키 필드와 탐색 속성을 업데이트 하 여 관련된 데이터를 업데이트 합니다."
keywords: "ASP.NET Core, Entity Framework Core 관련된 데이터를 조인"
ms.author: riande
manager: wpickett
ms.date: 11/15/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: data/ef-rp/update-related-data
ms.openlocfilehash: f07a33c19ba1be623fae14228f8fbc909d766816
ms.sourcegitcommit: 6e46abd65973dea796d364a514de9ec2e3e1c1ed
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2017
---
# <a name="updating-related-data---ef-core-razor-pages-7-of-8"></a><span data-ttu-id="690b6-104">관련된 데이터 요금-EF 핵심 Razor 페이지 (7/8)를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-104">Updating related data - EF Core Razor Pages (7 of 8)</span></span>

<span data-ttu-id="690b6-105">여 [Tom Dykstra](https://github.com/tdykstra), 및 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="690b6-105">By [Tom Dykstra](https://github.com/tdykstra), and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE[about the series](../../includes/RP-EF/intro.md)]

<span data-ttu-id="690b6-106">이 자습서에서는 관련된 데이터를 업데이트 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-106">This tutorial demonstrates updating related data.</span></span> <span data-ttu-id="690b6-107">문제를 해결할 수 없는를 실행 하는 경우 다운로드는 [이 단계에 대 한 완성 된 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part7)합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-107">If you run into problems you can't solve, download the [completed app for this stage](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part7).</span></span>

<span data-ttu-id="690b6-108">다음 그림은 완료 된 페이지의 일부를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-108">The following illustrations shows some of the completed pages.</span></span>

<span data-ttu-id="690b6-109">![과정 편집 페이지](update-related-data/_static/course-edit.png)
![강사 편집 페이지](update-related-data/_static/instructor-edit-courses.png)</span><span class="sxs-lookup"><span data-stu-id="690b6-109">![Course Edit page](update-related-data/_static/course-edit.png)
![Instructor Edit page](update-related-data/_static/instructor-edit-courses.png)</span></span>

<span data-ttu-id="690b6-110">테스트 만들기 및 편집 과정 페이지를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-110">Examine and test the Create and Edit course pages.</span></span> <span data-ttu-id="690b6-111">새 과정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-111">Create a new course.</span></span> <span data-ttu-id="690b6-112">부서에서 해당 이름이 아닌 기본 키 (정수)으로 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-112">The department is selected by its primary key (an integer), not its name.</span></span> <span data-ttu-id="690b6-113">새 과정을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-113">Edit the new course.</span></span> <span data-ttu-id="690b6-114">테스트를 완료 하는 경우 새 과정을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-114">When you have finished testing, delete the new course.</span></span>

## <a name="create-a-base-class-to-share-common-code"></a><span data-ttu-id="690b6-115">공통 코드를 공유 하는 기본 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="690b6-115">Create a base class to share common code</span></span>

<span data-ttu-id="690b6-116">Courses/만들기 및 편집 과정/페이지 부서 이름 목록이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-116">The Courses/Create and Courses/Edit pages each need a list of department names.</span></span> <span data-ttu-id="690b6-117">만들기는 *Pages/Courses/DepartmentNamePageModel.cshtml.cs* 기본 만들기 및 편집 페이지에 대 한 클래스:</span><span class="sxs-lookup"><span data-stu-id="690b6-117">Create the *Pages/Courses/DepartmentNamePageModel.cshtml.cs* base class for the Create and Edit pages:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Courses/DepartmentNamePageModel.cshtml.cs?highlight=9,11,20-21)]

<span data-ttu-id="690b6-118">위의 코드에서는 [SelectList](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.rendering.selectlist?view=aspnetcore-2.0) 부서 이름 목록을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-118">The preceding code creates a [SelectList](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.rendering.selectlist?view=aspnetcore-2.0) to contain the list of department names.</span></span> <span data-ttu-id="690b6-119">경우 `selectedDepartment` 해당 부서에서 선택 된 지정 된는 `SelectList`합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-119">If `selectedDepartment` is specified, that department is selected in the `SelectList`.</span></span>

<span data-ttu-id="690b6-120">만들기 및 편집 페이지 모델 클래스에서 파생 됩니다 `DepartmentNamePageModel`합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-120">The Create and Edit page model classes will derive from `DepartmentNamePageModel`.</span></span>

## <a name="customize-the-courses-pages"></a><span data-ttu-id="690b6-121">Courses 페이지를 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="690b6-121">Customize the Courses Pages</span></span>

<span data-ttu-id="690b6-122">새 과목 엔터티를 만들 때 기존 부서에는 관계가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-122">When a new course entity is created, it must have a relationship to an existing department.</span></span> <span data-ttu-id="690b6-123">만들기 및 편집에 대 한 기본 클래스는 과정을 만드는 동안 부서를 추가 하려면 부서를 선택 하기 위한 드롭 다운 목록을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-123">To add a department while creating a course, the base class for Create and Edit contains a drop-down list for selecting the department.</span></span> <span data-ttu-id="690b6-124">드롭다운 목록에서 설정 된 `Course.DepartmentID` 외래 키 (FK) 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-124">The drop-down list sets the `Course.DepartmentID` foreign key (FK) property.</span></span> <span data-ttu-id="690b6-125">EF 코어를 사용 하 여는 `Course.DepartmentID` FK 로드 하는 `Department` 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-125">EF Core uses the `Course.DepartmentID` FK to load the `Department` navigation property.</span></span>

![강좌를 만들기](update-related-data/_static/ddl.png)

<span data-ttu-id="690b6-127">업데이트를 다음 코드로 페이지 모델 만들기:</span><span class="sxs-lookup"><span data-stu-id="690b6-127">Update the Create page model with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Courses/Create.cshtml.cs?highlight=7,18,32-)]

<span data-ttu-id="690b6-128">위의 코드:</span><span class="sxs-lookup"><span data-stu-id="690b6-128">The preceding code:</span></span>

* <span data-ttu-id="690b6-129">`DepartmentNamePageModel`에서 파생됩니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-129">Derives from `DepartmentNamePageModel`.</span></span>
* <span data-ttu-id="690b6-130">사용 하 여 `TryUpdateModelAsync` 방지 하기 위해 [초과 게시](xref:data/ef-rp/crud#overposting)합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-130">Uses `TryUpdateModelAsync` to prevent [overposting](xref:data/ef-rp/crud#overposting).</span></span>
* <span data-ttu-id="690b6-131">대체 `ViewData["DepartmentID"]` 와 `DepartmentNameSL` (기본 클래스)에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-131">Replaces `ViewData["DepartmentID"]` with `DepartmentNameSL` (from the base class).</span></span>

<span data-ttu-id="690b6-132">`ViewData["DepartmentID"]`대체 되는 강력한 형식의와 `DepartmentNameSL`합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-132">`ViewData["DepartmentID"]` is replaced with the strongly typed `DepartmentNameSL`.</span></span> <span data-ttu-id="690b6-133">강력한 형식의 모델이 선호 되는 값을 통해 약하게 형식화 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-133">Strongly typed models are preferred over weakly typed.</span></span> <span data-ttu-id="690b6-134">자세한 내용은 참조 [데이터 (ViewData 및 ViewBag) 약하게 형식화](xref:mvc/views/overview#VD_VB)합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-134">For more information, see [Weakly typed data (ViewData and ViewBag)](xref:mvc/views/overview#VD_VB).</span></span>

### <a name="update-the-courses-create-page"></a><span data-ttu-id="690b6-135">업데이트 과정 만들기 페이지</span><span class="sxs-lookup"><span data-stu-id="690b6-135">Update the Courses Create page</span></span>

<span data-ttu-id="690b6-136">업데이트 *Pages/Courses/Create.cshtml* 다음 태그로:</span><span class="sxs-lookup"><span data-stu-id="690b6-136">Update *Pages/Courses/Create.cshtml* with the following markup:</span></span>

[!code-cshtml[Main](intro/samples/cu/Pages/Courses/Create.cshtml?highlight=29-34)]

<span data-ttu-id="690b6-137">위의 태그에서는 다음과 같이 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-137">The preceding markup makes the following changes:</span></span>

* <span data-ttu-id="690b6-138">캡션이 변경 **DepartmentID** 를 **부서**합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-138">Changes the caption from **DepartmentID** to **Department**.</span></span>
* <span data-ttu-id="690b6-139">대체 `"ViewBag.DepartmentID"` 와 `DepartmentNameSL` (기본 클래스)에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-139">Replaces `"ViewBag.DepartmentID"` with `DepartmentNameSL` (from the base class).</span></span>
* <span data-ttu-id="690b6-140">"부서 선택" 옵션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-140">Adds the "Select Department" option.</span></span> <span data-ttu-id="690b6-141">이 변경 하는 대신 첫 번째 부서 "부서 선택"을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-141">This change renders "Select Department" rather than the first department.</span></span>
* <span data-ttu-id="690b6-142">부서 선택 하지 않은 경우 유효성 검사 메시지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-142">Adds a validation message when the department is not selected.</span></span>

<span data-ttu-id="690b6-143">Razor 페이지를 사용 하 여 [태그 도우미 선택](xref:mvc/views/working-with-forms#the-select-tag-helper):</span><span class="sxs-lookup"><span data-stu-id="690b6-143">The Razor Page uses the [Select Tag Helper](xref:mvc/views/working-with-forms#the-select-tag-helper):</span></span>

[!code-cshtml[Main](intro/samples/cu/Pages/Courses/Create.cshtml?range=28-35&highlight=3-6)]

<span data-ttu-id="690b6-144">만들기 페이지를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-144">Test the Create page.</span></span> <span data-ttu-id="690b6-145">부서 ID 보다는 부서 이름 만들기 페이지 표시</span><span class="sxs-lookup"><span data-stu-id="690b6-145">The Create page displays the department name rather than the department ID.</span></span>

### <a name="update-the-courses-edit-page"></a><span data-ttu-id="690b6-146">Courses 편집 페이지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-146">Update the Courses Edit page.</span></span>

<span data-ttu-id="690b6-147">다음 코드와 편집 페이지 모델을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-147">Update the edit page model with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Courses/Edit.cshtml.cs?highlight=8,28,35,36,40,47-)]

<span data-ttu-id="690b6-148">변경이 페이지 모델 만들기에서에서 만든 것과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-148">The changes are similar to those made in the Create page model.</span></span> <span data-ttu-id="690b6-149">위의 코드에서 `PopulateDepartmentsDropDownList` 드롭 다운 목록에 지정 된 부서를 선택 하는 부서 ID 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-149">In the preceding code, `PopulateDepartmentsDropDownList` passes in the department ID, which select the department specified in the drop-down list.</span></span>

<span data-ttu-id="690b6-150">업데이트 *Pages/Courses/Edit.cshtml* 다음 태그로:</span><span class="sxs-lookup"><span data-stu-id="690b6-150">Update *Pages/Courses/Edit.cshtml* with the following markup:</span></span>

[!code-cshtml[Main](intro/samples/cu/Pages/Courses/Edit.cshtml?highlight=17-20,32-35)]

<span data-ttu-id="690b6-151">위의 태그에서는 다음과 같이 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-151">The preceding markup makes the following changes:</span></span>

* <span data-ttu-id="690b6-152">과정 ID를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-152">Displays the course ID.</span></span> <span data-ttu-id="690b6-153">일반적으로 엔터티의 기본 키 (PK) 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-153">Generally the Primary Key (PK) of an entity is not displayed.</span></span> <span data-ttu-id="690b6-154">PKs는 사용자에 게 일반적으로 아무런 의미가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-154">PKs are usually meaningless to users.</span></span> <span data-ttu-id="690b6-155">이 경우에 PK 과정 수입니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-155">In this case, the PK is the course number.</span></span>
* <span data-ttu-id="690b6-156">캡션이 변경 **DepartmentID** 를 **부서**합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-156">Changes the caption from **DepartmentID** to **Department**.</span></span>
* <span data-ttu-id="690b6-157">대체 `"ViewBag.DepartmentID"` 와 `DepartmentNameSL` (기본 클래스)에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-157">Replaces `"ViewBag.DepartmentID"` with `DepartmentNameSL` (from the base class).</span></span>
* <span data-ttu-id="690b6-158">"부서 선택" 옵션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-158">Adds the "Select Department" option.</span></span> <span data-ttu-id="690b6-159">이 변경 하는 대신 첫 번째 부서 "부서 선택"을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-159">This change renders "Select Department" rather than the first department.</span></span>
* <span data-ttu-id="690b6-160">부서 선택 하지 않은 경우 유효성 검사 메시지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-160">Adds a validation message when the department is not selected.</span></span>

<span data-ttu-id="690b6-161">페이지에 포함 하 여 숨겨진된 필드 (`<input type="hidden">`) 과정 번호에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-161">The page contains a hidden field (`<input type="hidden">`) for the course number.</span></span> <span data-ttu-id="690b6-162">추가 `<label>` 으로 도우미를 태그 `asp-for="Course.CourseID"` 숨겨진된 필드에 대 한 필요성을 제거 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-162">Adding a `<label>` tag helper with `asp-for="Course.CourseID"` doesn't eliminate the need for the hidden field.</span></span> <span data-ttu-id="690b6-163">`<input type="hidden">`사용자가 게시 된 데이터에 포함 되도록 과정 번호에 대 한 필요 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-163">`<input type="hidden">` is required for the course number to be included in the posted data when the user clicks **Save**.</span></span>

<span data-ttu-id="690b6-164">업데이트 된 코드를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-164">Test the updated code.</span></span> <span data-ttu-id="690b6-165">만들기, 편집 및 과정을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-165">Create, edit, and delete a course.</span></span>

## <a name="add-asnotracking-to-the-details-and-delete-page-models"></a><span data-ttu-id="690b6-166">AsNoTracking 세부 정보를 추가 하 고 페이지 모델 삭제</span><span class="sxs-lookup"><span data-stu-id="690b6-166">Add AsNoTracking to the Details and Delete page models</span></span>

<span data-ttu-id="690b6-167">[AsNoTracking](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.asnotracking?view=efcore-2.0#Microsoft_EntityFrameworkCore_EntityFrameworkQueryableExtensions_AsNoTracking__1_System_Linq_IQueryable___0__) 추적 필요 하지 않은 경우 성능을 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-167">[AsNoTracking](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.asnotracking?view=efcore-2.0#Microsoft_EntityFrameworkCore_EntityFrameworkQueryableExtensions_AsNoTracking__1_System_Linq_IQueryable___0__) can improve performance when tracking is not required.</span></span> <span data-ttu-id="690b6-168">추가 `AsNoTracking` 삭제 및 세부 정보 페이지 모델에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-168">Add `AsNoTracking` to the Delete and Details page model.</span></span> <span data-ttu-id="690b6-169">다음 코드는 업데이트 된 Delete 페이지 모델을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-169">The following code shows the updated Delete page model:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Courses/Delete.cshtml.cs?name=snippet&highlight=21,23,40,41)]

<span data-ttu-id="690b6-170">업데이트는 `OnGetAsync` 에서 메서드는 *Pages/Courses/Details.cshtml.cs* 파일:</span><span class="sxs-lookup"><span data-stu-id="690b6-170">Update the `OnGetAsync` method in the *Pages/Courses/Details.cshtml.cs* file:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Courses/Details.cshtml.cs?name=snippet)]

### <a name="modify-the-delete-and-details-pages"></a><span data-ttu-id="690b6-171">삭제 및 세부 정보 페이지를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-171">Modify the Delete and Details pages</span></span>

<span data-ttu-id="690b6-172">다음 태그로 삭제 Razor 페이지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-172">Update the Delete Razor page with the following markup:</span></span>

[!code-cshtml[Main](intro/samples/cu/Pages/Courses/Delete.cshtml?highlight=15-20)]

<span data-ttu-id="690b6-173">세부 정보 페이지에 동일한 변경 내용을 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="690b6-173">Make the same changes to the Details page.</span></span>

### <a name="test-the-course-pages"></a><span data-ttu-id="690b6-174">테스트 과정 페이지</span><span class="sxs-lookup"><span data-stu-id="690b6-174">Test the Course pages</span></span>

<span data-ttu-id="690b6-175">테스트 만들기, 세부 정보를 편집 및 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-175">Test create, edit, details, and delete.</span></span>

## <a name="update-the-instructor-pages"></a><span data-ttu-id="690b6-176">강사 페이지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-176">Update the instructor pages</span></span>

<span data-ttu-id="690b6-177">다음 섹션에서는 강사 페이지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-177">The following sections update the instructor pages.</span></span>

### <a name="add-office-location"></a><span data-ttu-id="690b6-178">사무실 위치를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-178">Add office location</span></span>

<span data-ttu-id="690b6-179">강사 레코드를 편집할 때 강의 사무실 할당을 업데이트 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-179">When editing an instructor record, you may want to update the instructor's office assignment.</span></span> <span data-ttu-id="690b6-180">`Instructor` 엔터티 간의 관계가 0 또는 1을 하나는 `OfficeAssignment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="690b6-180">The `Instructor` entity has a one-to-zero-or-one relationship with the `OfficeAssignment` entity.</span></span> <span data-ttu-id="690b6-181">강사 코드 처리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-181">The instructor code must handle:</span></span>

* <span data-ttu-id="690b6-182">사무실 할당을 해제 하는 경우 삭제 된 `OfficeAssignment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="690b6-182">If the user clears the office assignment, delete the `OfficeAssignment` entity.</span></span>
* <span data-ttu-id="690b6-183">사용자가 사무실 할당 되었으며 빈 경우 만들 새 `OfficeAssignment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="690b6-183">If the user enters an office assignment and it was empty, create a new `OfficeAssignment` entity.</span></span>
* <span data-ttu-id="690b6-184">사용자가 사무실 할당을 변경 하는 경우 업데이트 된 `OfficeAssignment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="690b6-184">If the user changes the office assignment, update the `OfficeAssignment` entity.</span></span>

<span data-ttu-id="690b6-185">다음 코드로 강사 편집 페이지 모델을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-185">Update the instructors Edit page model with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Edit1.cshtml.cs?name=snippet&highlight=20-23,32,39-)]

<span data-ttu-id="690b6-186">위의 코드:</span><span class="sxs-lookup"><span data-stu-id="690b6-186">The preceding code:</span></span>

- <span data-ttu-id="690b6-187">현재 가져옵니다 `Instructor` 에 대 한 즉시 로드를 사용 하 여 데이터베이스에서 엔터티는 `OfficeAssignment` 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-187">Gets the current `Instructor` entity from the database using eager loading for the `OfficeAssignment` navigation property.</span></span>
- <span data-ttu-id="690b6-188">검색 된 업데이트 `Instructor` 엔터티 모델 바인더의 값으로.</span><span class="sxs-lookup"><span data-stu-id="690b6-188">Updates the retrieved `Instructor` entity with values from the model binder.</span></span> <span data-ttu-id="690b6-189">`TryUpdateModel`방지 [초과 게시](xref:data/ef-rp/crud#overposting)합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-189">`TryUpdateModel` prevents [overposting](xref:data/ef-rp/crud#overposting).</span></span>
- <span data-ttu-id="690b6-190">사무실 위치 비어 있으면 설정 `Instructor.OfficeAssignment` null로 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-190">If the office location is blank, sets `Instructor.OfficeAssignment` to null.</span></span> <span data-ttu-id="690b6-191">때 `Instructor.OfficeAssignment` 가 null 이면에 있는 관련된 행의 `OfficeAssignment` 테이블이 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-191">When `Instructor.OfficeAssignment` is null, the related row in the `OfficeAssignment` table is deleted.</span></span>

### <a name="update-the-instructor-edit-page"></a><span data-ttu-id="690b6-192">강사 편집 페이지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-192">Update the instructor Edit page</span></span>

<span data-ttu-id="690b6-193">업데이트 *Pages/Instructors/Edit.cshtml* 사무실 위치와:</span><span class="sxs-lookup"><span data-stu-id="690b6-193">Update *Pages/Instructors/Edit.cshtml* with the office location:</span></span>

[!code-cshtml[Main](intro/samples/cu/Pages/Instructors/Edit1.cshtml?highlight=29-33)]

<span data-ttu-id="690b6-194">강사 사무실 위치를 변경할 수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-194">Verify you can change an instructors office location.</span></span>

## <a name="add-course-assignments-to-the-instructor-edit-page"></a><span data-ttu-id="690b6-195">강사 편집 페이지를 과정 할당을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-195">Add Course assignments to the instructor Edit page</span></span>

<span data-ttu-id="690b6-196">강사는 courses 개수에 관계 없이 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-196">Instructors may teach any number of courses.</span></span> <span data-ttu-id="690b6-197">이 섹션에서는 과정 할당을 변경 하는 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-197">In this section, you add the ability to change course assignments.</span></span> <span data-ttu-id="690b6-198">다음 그림에서는 업데이트 된 강사 편집 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-198">The following image shows the updated instructor Edit page:</span></span>

![Courses와 강사 편집 페이지](update-related-data/_static/instructor-edit-courses.png)

<span data-ttu-id="690b6-200">`Course`및 `Instructor` 다 대 다 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-200">`Course` and `Instructor` has a many-to-many relationship.</span></span> <span data-ttu-id="690b6-201">추가 하 고 관계를 추가 하거나 제거에서 엔터티는 `CourseAssignments` 엔터티 집합을 조인 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-201">To add and remove relationships, you add and remove entities from the `CourseAssignments` join entity set.</span></span>

<span data-ttu-id="690b6-202">확인란을 courses 강사에 할당 된 변경 내용을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-202">Check boxes enable changes to courses an instructor is assigned to.</span></span> <span data-ttu-id="690b6-203">데이터베이스의 모든 과정에 대 한 확인란이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-203">A check box is displayed for every course in the database.</span></span> <span data-ttu-id="690b6-204">Courses 강사에 할당 된 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-204">Courses that the instructor is assigned to are checked.</span></span> <span data-ttu-id="690b6-205">사용자가 선택 하거나 과정 할당을 변경 하려면 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-205">The user can select or clear check boxes to change course assignments.</span></span> <span data-ttu-id="690b6-206">Courses 수가 훨씬 더 클 경우:</span><span class="sxs-lookup"><span data-stu-id="690b6-206">If the number of courses were much greater:</span></span>

* <span data-ttu-id="690b6-207">아마도 코스 표시 하려면 다른 사용자 인터페이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-207">You'd probably use a different user interface to display the courses.</span></span>
* <span data-ttu-id="690b6-208">관계 만들기 또는 삭제 하는 조인 엔터티를 조작 하는 방법은 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-208">The method of manipulating a join entity to create or delete relationships would not change.</span></span>

### <a name="add-classes-to-support-create-and-edit-instructor-pages"></a><span data-ttu-id="690b6-209">지 원하는 클래스를 추가 강사 페이지 만들고 편집</span><span class="sxs-lookup"><span data-stu-id="690b6-209">Add classes to support Create and Edit instructor pages</span></span>

<span data-ttu-id="690b6-210">만들 *SchoolViewModels/AssignedCourseData.cs* 를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="690b6-210">Create *SchoolViewModels/AssignedCourseData.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/SchoolViewModels/AssignedCourseData.cs)]

<span data-ttu-id="690b6-211">`AssignedCourseData` 클래스 강사 하 여 할당 된 과정에 대 한 확인란을 만들기 위해 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-211">The `AssignedCourseData` class contains data to create the check boxes for assigned courses by an instructor.</span></span>

<span data-ttu-id="690b6-212">만들기는 *Pages/Instructors/InstructorCoursesPageModel.cshtml.cs* 기본 클래스:</span><span class="sxs-lookup"><span data-stu-id="690b6-212">Create the *Pages/Instructors/InstructorCoursesPageModel.cshtml.cs* base class:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/InstructorCoursesPageModel.cshtml.cs)]

<span data-ttu-id="690b6-213">`InstructorCoursesPageModel` 의 기본 클래스에서는 편집을 위한 사용 하 고 페이지 모델을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-213">The `InstructorCoursesPageModel` is the base class you will use for the Edit and Create page models.</span></span> <span data-ttu-id="690b6-214">`PopulateAssignedCourseData`모든 읽고 `Course` 엔터티를 채우는 `AssignedCourseDataList`합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-214">`PopulateAssignedCourseData` reads all `Course` entities to populate `AssignedCourseDataList`.</span></span> <span data-ttu-id="690b6-215">코드에서는 각 과정에 대 한 설정에서 `CourseID`, 제목 및 강의 과정에 할당 된 여부.</span><span class="sxs-lookup"><span data-stu-id="690b6-215">For each course, the code sets the `CourseID`, title, and whether or not the instructor is assigned to the course.</span></span> <span data-ttu-id="690b6-216">A [HashSet](https://docs.microsoft.com/dotnet/api/system.collections.generic.hashset-1) 효율적인 조회를 만드는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-216">A [HashSet](https://docs.microsoft.com/dotnet/api/system.collections.generic.hashset-1) is used to create efficient lookups.</span></span>

### <a name="instructors-edit-page-model"></a><span data-ttu-id="690b6-217">강사 편집 페이지 모델</span><span class="sxs-lookup"><span data-stu-id="690b6-217">Instructors Edit page model</span></span>

<span data-ttu-id="690b6-218">다음 코드로 강사 편집 페이지 모델을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-218">Update the instructor Edit page model with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Edit.cshtml.cs?name=snippet&highlight=1,20-24,30,34,41-)]

<span data-ttu-id="690b6-219">위의 코드에는 office 할당 변경을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-219">The preceding code handles office assignment changes.</span></span>

<span data-ttu-id="690b6-220">Razor 뷰 강사를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-220">Update the instructor Razor View:</span></span>

[!code-cshtml[Main](intro/samples/cu/Pages/Instructors/Edit.cshtml?highlight=34-59)]

<a id="notepad"></a>
> [!NOTE]
> <span data-ttu-id="690b6-221">Visual Studio에서 코드를 붙여 넣을 때 줄 바꿈 코드를 중단 하는 방식으로 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-221">When you paste the code in Visual Studio, line breaks are changed in a way that breaks the code.</span></span> <span data-ttu-id="690b6-222">자동 서식 지정을 실행 취소 하려면 Ctrl + Z를 한 번 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-222">Press Ctrl+Z one time to undo the automatic formatting.</span></span> <span data-ttu-id="690b6-223">Ctrl + Z 여기와 같은 모양 줄 바꿈 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-223">Ctrl+Z fixes the line breaks so that they look like what you see here.</span></span> <span data-ttu-id="690b6-224">들여쓰기 완벽 하지 않아도 되지만 `@</tr><tr>`, `@:<td>`, `@:</td>`, 및 `@:</tr>` 줄은 각각 여야 한 줄에 표시 된 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-224">The indentation doesn't have to be perfect, but the `@</tr><tr>`, `@:<td>`, `@:</td>`, and `@:</tr>` lines must each be on a single line as shown.</span></span> <span data-ttu-id="690b6-225">선택 된 새 코드 블록과 Tab 세 번 키를 눌러 줄 기존 코드와 함께 새 코드를 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-225">With the block of new code selected, press Tab three times to line up the new code with the existing code.</span></span> <span data-ttu-id="690b6-226">투표 하거나이 버그의 상태를 검토할 [이 링크를 통해](https://developercommunity.visualstudio.com/content/problem/147795/razor-editor-malforms-pasted-markup-and-creates-in.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-226">Vote on or review the status of this bug [with this link](https://developercommunity.visualstudio.com/content/problem/147795/razor-editor-malforms-pasted-markup-and-creates-in.html).</span></span>

<span data-ttu-id="690b6-227">위의 코드는 세 개의 열이 있는 HTML 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-227">The preceding code creates an HTML table that has three columns.</span></span> <span data-ttu-id="690b6-228">각 열에는 확인란과 과정 번호 및 제목에 포함 된 캡션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-228">Each column has a check box and a caption containing the course number and title.</span></span> <span data-ttu-id="690b6-229">모든 확인란의 이름이 같은 ("selectedCourses").</span><span class="sxs-lookup"><span data-stu-id="690b6-229">The check boxes all have the same name ("selectedCourses").</span></span> <span data-ttu-id="690b6-230">동일한 이름을 사용 하 여 모델 바인더를 그룹으로 취급 하도록 알립니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-230">Using the same name informs the model binder to treat them as a group.</span></span> <span data-ttu-id="690b6-231">각 확인란의 값 특성이로 설정 된 `CourseID`합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-231">The value attribute of each check box is set to `CourseID`.</span></span> <span data-ttu-id="690b6-232">모델 바인더 구성 된 배열을 전달 페이지가 게시 되는 경우는 `CourseID` 확인란만 선택 된에 대 한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-232">When the page is posted, the model binder passes an array that consists of the `CourseID` values for only the check boxes that are selected.</span></span>

<span data-ttu-id="690b6-233">확인란은 처음 렌더링 됩니다 courses 강사에 할당 된 특성 확인 했습니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-233">When the check boxes are initially rendered, courses assigned to the instructor have checked attributes.</span></span>

<span data-ttu-id="690b6-234">응용 프로그램을 실행 하 고 업데이트 된 instructors 편집 페이지를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-234">Run the app and test the updated instructors Edit page.</span></span> <span data-ttu-id="690b6-235">일부 과정 할당을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-235">Change some course assignments.</span></span> <span data-ttu-id="690b6-236">인덱스 페이지에 변경 내용이 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-236">The changes are reflected on the Index page.</span></span>

<span data-ttu-id="690b6-237">참고: 강사 과정 데이터를 편집 하려면 여기에 적용 되는 방법을 제한 된 수의 과목 필요한 경우에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-237">Note: The approach taken here to edit instructor course data works well when there is a limited number of courses.</span></span> <span data-ttu-id="690b6-238">훨씬 큰 경우에 컬렉션의 경우 다른 UI 하는 다른 업데이트 방법을 것 에서도 효율성을 향상 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-238">For collections that are much larger, a different UI and a different updating method would be more useable and efficient.</span></span>

### <a name="update-the-instructors-create-page"></a><span data-ttu-id="690b6-239">강사 만들기 페이지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-239">Update the instructors Create page</span></span>

<span data-ttu-id="690b6-240">다음 코드와 함께 모델 강사 만들기 페이지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-240">Update the instructor Create page model with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Create.cshtml.cs)]

<span data-ttu-id="690b6-241">위의 코드는 비슷합니다는 *Pages/Instructors/Edit.cshtml.cs* 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-241">The preceding code is similar to the *Pages/Instructors/Edit.cshtml.cs* code.</span></span>

<span data-ttu-id="690b6-242">다음 태그로 강사 만들 Razor 페이지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-242">Update the instructor Create Razor page with the following markup:</span></span>

[!code-cshtml[Main](intro/samples/cu/Pages/Instructors/Create.cshtml?highlight=32-62)]

<span data-ttu-id="690b6-243">강사 만들기 페이지를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-243">Test the instructor Create page.</span></span>

## <a name="update-the-delete-page"></a><span data-ttu-id="690b6-244">업데이트 페이지 삭제</span><span class="sxs-lookup"><span data-stu-id="690b6-244">Update the Delete page</span></span>

<span data-ttu-id="690b6-245">다음 코드로 Delete 페이지 모델을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-245">Update the Delete page model with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Delete.cshtml.cs?highlight=5,40-)]

<span data-ttu-id="690b6-246">위의 코드는 다음과 같이 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-246">The preceding code makes the following changes:</span></span>

* <span data-ttu-id="690b6-247">에 대 한 즉시 로드를 사용 하 여는 `CourseAssignments` 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-247">Uses eager loading for the `CourseAssignments` navigation property.</span></span> <span data-ttu-id="690b6-248">`CourseAssignments`포함 되어야 합니다 또는 강사 삭제 될 때 삭제 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-248">`CourseAssignments` must be included or they aren't deleted when the instructor is deleted.</span></span> <span data-ttu-id="690b6-249">읽이 필요를 방지 하려면 데이터베이스에 cascade delete를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-249">To avoid needing to read them, configure cascade delete in the database.</span></span>

* <span data-ttu-id="690b6-250">삭제할 강사 부서의 관리자로 할당 된 경우 해당 부서에서 강사 할당을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="690b6-250">If the instructor to be deleted is assigned as administrator of any departments, removes the instructor assignment from those departments.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="690b6-251">[이전](xref:data/ef-rp/read-related-data)
[다음](xref:data/ef-rp/concurrency)</span><span class="sxs-lookup"><span data-stu-id="690b6-251">[Previous](xref:data/ef-rp/read-related-data)
[Next](xref:data/ef-rp/concurrency)</span></span>