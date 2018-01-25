---
title: "EF 코어-를 사용 하 여 razor 페이지 관련된 데이터-7/8 업데이트"
author: rick-anderson
description: "이 자습서에서는 외래 키 필드와 탐색 속성을 업데이트 하 여 관련된 데이터를 업데이트 합니다."
ms.author: riande
manager: wpickett
ms.date: 11/15/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: data/ef-rp/update-related-data
ms.openlocfilehash: 236589d0202a7f30f1e1a9d69902000fd9a2dd71
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
# <a name="updating-related-data---ef-core-razor-pages-7-of-8"></a>관련된 데이터 요금-EF 핵심 Razor 페이지 (7/8)를 업데이트합니다.

여 [Tom Dykstra](https://github.com/tdykstra), 및 [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE[about the series](../../includes/RP-EF/intro.md)]

이 자습서에서는 관련된 데이터를 업데이트 하는 방법을 보여 줍니다. 문제를 해결할 수 없는를 실행 하는 경우 다운로드는 [이 단계에 대 한 완성 된 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part7)합니다.

다음 그림은 완료 된 페이지의 일부를 보여 줍니다.

![과정 편집 페이지](update-related-data/_static/course-edit.png)
![강사 편집 페이지](update-related-data/_static/instructor-edit-courses.png)

테스트 만들기 및 편집 과정 페이지를 검사 합니다. 새 과정을 만듭니다. 부서에서 해당 이름이 아닌 기본 키 (정수)으로 선택 됩니다. 새 과정을 편집 합니다. 테스트를 완료 하는 경우 새 과정을 삭제 합니다.

## <a name="create-a-base-class-to-share-common-code"></a>공통 코드를 공유 하는 기본 클래스 만들기

Courses/만들기 및 편집 과정/페이지 부서 이름 목록이 필요 합니다. 만들기는 *Pages/Courses/DepartmentNamePageModel.cshtml.cs* 기본 만들기 및 편집 페이지에 대 한 클래스:

[!code-csharp[Main](intro/samples/cu/Pages/Courses/DepartmentNamePageModel.cshtml.cs?highlight=9,11,20-21)]

위의 코드에서는 [SelectList](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.mvc.rendering.selectlist?view=aspnetcore-2.0) 부서 이름 목록을 포함 합니다. 경우 `selectedDepartment` 해당 부서에서 선택 된 지정 된는 `SelectList`합니다.

만들기 및 편집 페이지 모델 클래스에서 파생 됩니다 `DepartmentNamePageModel`합니다.

## <a name="customize-the-courses-pages"></a>Courses 페이지를 사용자 지정

새 과목 엔터티를 만들 때 기존 부서에는 관계가 있어야 합니다. 만들기 및 편집에 대 한 기본 클래스는 과정을 만드는 동안 부서를 추가 하려면 부서를 선택 하기 위한 드롭 다운 목록을 포함 합니다. 드롭다운 목록에서 설정 된 `Course.DepartmentID` 외래 키 (FK) 속성입니다. EF 코어를 사용 하 여는 `Course.DepartmentID` FK 로드 하는 `Department` 탐색 속성입니다.

![강좌를 만들기](update-related-data/_static/ddl.png)

업데이트를 다음 코드로 페이지 모델 만들기:

[!code-csharp[Main](intro/samples/cu/Pages/Courses/Create.cshtml.cs?highlight=7,18,32-)]

위의 코드:

* `DepartmentNamePageModel`에서 파생됩니다.
* 사용 하 여 `TryUpdateModelAsync` 방지 하기 위해 [초과 게시](xref:data/ef-rp/crud#overposting)합니다.
* 대체 `ViewData["DepartmentID"]` 와 `DepartmentNameSL` (기본 클래스)에서 사용 합니다.

`ViewData["DepartmentID"]`대체 되는 강력한 형식의와 `DepartmentNameSL`합니다. 강력한 형식의 모델이 선호 되는 값을 통해 약하게 형식화 합니다. 자세한 내용은 참조 [데이터 (ViewData 및 ViewBag) 약하게 형식화](xref:mvc/views/overview#VD_VB)합니다.

### <a name="update-the-courses-create-page"></a>업데이트 과정 만들기 페이지

업데이트 *Pages/Courses/Create.cshtml* 다음 태그로:

[!code-cshtml[Main](intro/samples/cu/Pages/Courses/Create.cshtml?highlight=29-34)]

위의 태그에서는 다음과 같이 변경 합니다.

* 캡션이 변경 **DepartmentID** 를 **부서**합니다.
* 대체 `"ViewBag.DepartmentID"` 와 `DepartmentNameSL` (기본 클래스)에서 사용 합니다.
* "부서 선택" 옵션을 추가합니다. 이 변경 하는 대신 첫 번째 부서 "부서 선택"을 렌더링합니다.
* 부서 선택 되지 않은 경우 유효성 검사 메시지를 추가 합니다.

Razor 페이지를 사용 하 여 [태그 도우미 선택](xref:mvc/views/working-with-forms#the-select-tag-helper):

[!code-cshtml[Main](intro/samples/cu/Pages/Courses/Create.cshtml?range=28-35&highlight=3-6)]

만들기 페이지를 테스트 합니다. 부서 ID 보다는 부서 이름 만들기 페이지 표시

### <a name="update-the-courses-edit-page"></a>Courses 편집 페이지를 업데이트 합니다.

다음 코드와 편집 페이지 모델을 업데이트 합니다.

[!code-csharp[Main](intro/samples/cu/Pages/Courses/Edit.cshtml.cs?highlight=8,28,35,36,40,47-)]

변경이 페이지 모델 만들기에서에서 만든 것과 비슷합니다. 위의 코드에서 `PopulateDepartmentsDropDownList` 드롭 다운 목록에 지정 된 부서를 선택 하는 부서 ID 전달 합니다.

업데이트 *Pages/Courses/Edit.cshtml* 다음 태그로:

[!code-cshtml[Main](intro/samples/cu/Pages/Courses/Edit.cshtml?highlight=17-20,32-35)]

위의 태그에서는 다음과 같이 변경 합니다.

* 과정 ID를 표시 합니다. 일반적으로 엔터티의 기본 키 (PK) 표시 되지 않습니다. PKs는 사용자에 게 일반적으로 아무런 의미가 없습니다. 이 경우에 PK 과정 수입니다.
* 캡션이 변경 **DepartmentID** 를 **부서**합니다.
* 대체 `"ViewBag.DepartmentID"` 와 `DepartmentNameSL` (기본 클래스)에서 사용 합니다.
* "부서 선택" 옵션을 추가합니다. 이 변경 하는 대신 첫 번째 부서 "부서 선택"을 렌더링합니다.
* 부서 선택 되지 않은 경우 유효성 검사 메시지를 추가 합니다.

페이지에 포함 하 여 숨겨진된 필드 (`<input type="hidden">`) 과정 번호에 대 한 합니다. 추가 `<label>` 으로 도우미를 태그 `asp-for="Course.CourseID"` 숨겨진된 필드에 대 한 필요성을 제거 하지 않습니다. `<input type="hidden">`사용자가 게시 된 데이터에 포함 되도록 과정 번호에 대 한 필요 **저장**합니다.

업데이트 된 코드를 테스트 합니다. 만들기, 편집 및 과정을 삭제 합니다.

## <a name="add-asnotracking-to-the-details-and-delete-page-models"></a>AsNoTracking 세부 정보를 추가 하 고 페이지 모델 삭제

[AsNoTracking](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.entityframeworkqueryableextensions.asnotracking?view=efcore-2.0#Microsoft_EntityFrameworkCore_EntityFrameworkQueryableExtensions_AsNoTracking__1_System_Linq_IQueryable___0__) 관리할 필요 없는 때 성능을 향상 시킬 수 있습니다. 추가 `AsNoTracking` 삭제 및 세부 정보 페이지 모델에 있습니다. 다음 코드는 업데이트 된 Delete 페이지 모델을 보여 줍니다.

[!code-csharp[Main](intro/samples/cu/Pages/Courses/Delete.cshtml.cs?name=snippet&highlight=21,23,40,41)]

업데이트는 `OnGetAsync` 에서 메서드는 *Pages/Courses/Details.cshtml.cs* 파일:

[!code-csharp[Main](intro/samples/cu/Pages/Courses/Details.cshtml.cs?name=snippet)]

### <a name="modify-the-delete-and-details-pages"></a>삭제 및 세부 정보 페이지를 수정 합니다.

다음 태그로 삭제 Razor 페이지를 업데이트 합니다.

[!code-cshtml[Main](intro/samples/cu/Pages/Courses/Delete.cshtml?highlight=15-20)]

세부 정보 페이지에 동일한 변경 내용을 확인 하십시오.

### <a name="test-the-course-pages"></a>테스트 과정 페이지

테스트 만들기, 세부 정보를 편집 및 삭제 합니다.

## <a name="update-the-instructor-pages"></a>강사 페이지를 업데이트 합니다.

다음 섹션에서는 강사 페이지를 업데이트 합니다.

### <a name="add-office-location"></a>사무실 위치를 추가 합니다.

강사 레코드를 편집할 때 강의 사무실 할당을 업데이트 하는 것이 좋습니다. `Instructor` 엔터티 간의 관계가 0 또는 1을 하나는 `OfficeAssignment` 엔터티. 강사 코드 처리 해야 합니다.

* 사무실 할당을 해제 하는 경우 삭제 된 `OfficeAssignment` 엔터티.
* 사용자가 사무실 할당 되었으며 빈 경우 만들 새 `OfficeAssignment` 엔터티.
* 사용자가 사무실 할당을 변경 하는 경우 업데이트 된 `OfficeAssignment` 엔터티.

다음 코드로 강사 편집 페이지 모델을 업데이트 합니다.

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Edit1.cshtml.cs?name=snippet&highlight=20-23,32,39-)]

위의 코드:

- 현재 가져옵니다 `Instructor` 에 대 한 즉시 로드를 사용 하 여 데이터베이스에서 엔터티는 `OfficeAssignment` 탐색 속성입니다.
- 검색 된 업데이트 `Instructor` 엔터티 모델 바인더의 값으로. `TryUpdateModel`방지 [초과 게시](xref:data/ef-rp/crud#overposting)합니다.
- 사무실 위치 비어 있으면 설정 `Instructor.OfficeAssignment` null로 합니다. 때 `Instructor.OfficeAssignment` 가 null 이면에 있는 관련된 행의 `OfficeAssignment` 테이블이 삭제 됩니다.

### <a name="update-the-instructor-edit-page"></a>강사 편집 페이지를 업데이트 합니다.

업데이트 *Pages/Instructors/Edit.cshtml* 사무실 위치와:

[!code-cshtml[Main](intro/samples/cu/Pages/Instructors/Edit1.cshtml?highlight=29-33)]

강사 사무실 위치를 변경할 수를 확인 합니다.

## <a name="add-course-assignments-to-the-instructor-edit-page"></a>강사 편집 페이지를 과정 할당을 추가 합니다.

강사는 courses 개수에 관계 없이 지정할 수 있습니다. 이 섹션에서는 과정 할당을 변경 하는 기능을 추가 합니다. 다음 그림에서는 업데이트 된 강사 편집 페이지를 보여 줍니다.

![Courses와 강사 편집 페이지](update-related-data/_static/instructor-edit-courses.png)

`Course`및 `Instructor` 다 대 다 관계입니다. 추가 하 고 관계를 추가 하거나 제거에서 엔터티는 `CourseAssignments` 엔터티 집합을 조인 합니다.

확인란을 courses 강사에 할당 된 변경 내용을 사용 합니다. 데이터베이스의 모든 과정에 대 한 확인란이 표시 됩니다. Courses 강사에 할당 된 확인 됩니다. 사용자가 선택 하거나 과정 할당을 변경 하려면 확인란의 선택을 취소 합니다. Courses 수가 훨씬 더 클 경우:

* 아마도 코스 표시 하려면 다른 사용자 인터페이스를 사용 합니다.
* 관계 만들기 또는 삭제 하는 조인 엔터티를 조작 하는 방법을 변경 하지 않습니다.

### <a name="add-classes-to-support-create-and-edit-instructor-pages"></a>지 원하는 클래스를 추가 강사 페이지 만들고 편집

만들 *SchoolViewModels/AssignedCourseData.cs* 를 다음 코드로:

[!code-csharp[Main](intro/samples/cu/Models/SchoolViewModels/AssignedCourseData.cs)]

`AssignedCourseData` 클래스 강사 하 여 할당 된 과정에 대 한 확인란을 만들기 위해 데이터를 포함 합니다.

만들기는 *Pages/Instructors/InstructorCoursesPageModel.cshtml.cs* 기본 클래스:

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/InstructorCoursesPageModel.cshtml.cs)]

`InstructorCoursesPageModel` 의 기본 클래스에서는 편집을 위한 사용 하 고 페이지 모델을 만듭니다. `PopulateAssignedCourseData`모든 읽고 `Course` 엔터티를 채우는 `AssignedCourseDataList`합니다. 코드에서는 각 과정에 대 한 설정에서 `CourseID`, 제목 및 강의 과정에 할당 된 여부. A [HashSet](https://docs.microsoft.com/dotnet/api/system.collections.generic.hashset-1) 효율적인 조회를 만드는 데 사용 됩니다.

### <a name="instructors-edit-page-model"></a>강사 편집 페이지 모델

다음 코드로 강사 편집 페이지 모델을 업데이트 합니다.

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Edit.cshtml.cs?name=snippet&highlight=1,20-24,30,34,41-)]

위의 코드에는 office 할당 변경을 처리합니다.

Razor 뷰 강사를 업데이트 합니다.

[!code-cshtml[Main](intro/samples/cu/Pages/Instructors/Edit.cshtml?highlight=34-59)]

<a id="notepad"></a>
> [!NOTE]
> Visual Studio에서 코드를 붙여 넣을 때 줄 바꿈 코드를 중단 하는 방식으로 변경 됩니다. 자동 서식 지정을 실행 취소 하려면 Ctrl + Z를 한 번 누릅니다. Ctrl + Z 여기와 같은 모양 줄 바꿈 해결 합니다. 들여쓰기 완벽 하지 않아도 되지만 `@</tr><tr>`, `@:<td>`, `@:</td>`, 및 `@:</tr>` 줄은 각각 여야 한 줄에 표시 된 것 처럼 합니다. 선택 된 새 코드 블록과 Tab 세 번 키를 눌러 줄 기존 코드와 함께 새 코드를 합니다. 투표 하거나이 버그의 상태를 검토할 [이 링크를 통해](https://developercommunity.visualstudio.com/content/problem/147795/razor-editor-malforms-pasted-markup-and-creates-in.html)합니다.

위의 코드는 세 개의 열이 있는 HTML 테이블을 만듭니다. 각 열에는 확인란과 과정 번호 및 제목에 포함 된 캡션에 있습니다. 모든 확인란의 이름이 같은 ("selectedCourses"). 동일한 이름을 사용 하 여 모델 바인더를 그룹으로 취급 하도록 알립니다. 각 확인란의 값 특성이로 설정 된 `CourseID`합니다. 모델 바인더 구성 된 배열을 전달 페이지가 게시 되는 경우는 `CourseID` 확인란만 선택 된에 대 한 값입니다.

확인란은 처음 렌더링 됩니다 courses 강사에 할당 된 특성 확인 했습니다.

응용 프로그램을 실행 하 고 업데이트 된 instructors 편집 페이지를 테스트 합니다. 일부 과정 할당을 변경 합니다. 인덱스 페이지에 변경 내용이 반영 됩니다.

참고: 강사 과정 데이터를 편집 하려면 여기에 적용 되는 방법을 제한 된 수의 과목 필요한 경우에 작동 합니다. 훨씬 큰 경우에 컬렉션의 경우 다른 UI 하는 다른 업데이트 방법을 것 에서도 효율성을 향상 합니다.

### <a name="update-the-instructors-create-page"></a>강사 만들기 페이지를 업데이트 합니다.

다음 코드와 함께 모델 강사 만들기 페이지를 업데이트 합니다.

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Create.cshtml.cs)]

위의 코드는 비슷합니다는 *Pages/Instructors/Edit.cshtml.cs* 코드입니다.

다음 태그로 강사 만들 Razor 페이지를 업데이트 합니다.

[!code-cshtml[Main](intro/samples/cu/Pages/Instructors/Create.cshtml?highlight=32-62)]

강사 만들기 페이지를 테스트 합니다.

## <a name="update-the-delete-page"></a>업데이트 페이지 삭제

다음 코드로 Delete 페이지 모델을 업데이트 합니다.

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Delete.cshtml.cs?highlight=5,40-)]

위의 코드는 다음과 같이 변경 합니다.

* 에 대 한 즉시 로드를 사용 하 여는 `CourseAssignments` 탐색 속성입니다. `CourseAssignments`포함 되어야 합니다 또는 강사 삭제 될 때 삭제 되지 않습니다. 읽이 필요를 방지 하려면 데이터베이스에 cascade delete를 구성 합니다.

* 삭제할 강사 부서의 관리자로 할당 된 경우 해당 부서에서 강사 할당을 제거 합니다.

>[!div class="step-by-step"]
[이전](xref:data/ef-rp/read-related-data)
[다음](xref:data/ef-rp/concurrency)
