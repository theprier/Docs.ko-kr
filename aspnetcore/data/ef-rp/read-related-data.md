---
title: "EF 코어-를 사용 하 여 razor 페이지 관련된 데이터 읽기-8 6"
author: rick-anderson
description: "이 자습서에서는 읽기 및 관련된 데이터-Entity Framework 탐색 속성에 로드 하는 데이터를 표시 합니다."
manager: wpickett
ms.author: riande
ms.date: 11/05/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: data/ef-rp/read-related-data
ms.openlocfilehash: ccb1e95ae2b43fd0a4c4b1ac9ed58a4d474ab3b6
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="reading-related-data---ef-core-with-razor-pages-6-of-8"></a>관련 데이터-EF 코어 Razor 페이지 (8 6)에 읽기

여 [Tom Dykstra](https://github.com/tdykstra), [Jon P Smith](https://twitter.com/thereformedprog), 및 [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE[about the series](../../includes/RP-EF/intro.md)]

이 자습서에서는 관련된 데이터를 읽고 표시 됩니다. 관련된 데이터는 데이터 탐색 속성에 로드 EF 코어입니다.

문제를 해결할 수 없는를 실행 하는 경우 다운로드는 [이 단계에 대 한 완성 된 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part6-related)합니다.

다음 그림은이 자습서에 대 한 완료 된 페이지를 보여 줍니다.

![Courses 인덱스 페이지](read-related-data/_static/courses-index.png)

![강사 인덱스 페이지](read-related-data/_static/instructors-index.png)

## <a name="eager-explicit-and-lazy-loading-of-related-data"></a>관련된 데이터를 신속 하 게, 명시적, 및 지연 로드

여러 가지 방법으로 EF 코어가 엔터티의 탐색 속성에 관련된 데이터를 로드할 수 있습니다.

* [즉시 로드](https://docs.microsoft.com/ef/core/querying/related-data#eager-loading)합니다. 즉시 로드 때 한 가지 유형의 엔터티에 대 한 쿼리도 관련된 엔터티를 로드 합니다. 엔터티를 읽을 때 관련된 데이터 검색 됩니다. 일반적으로 필요한 데이터를 모두 검색 하는 단일 조인 쿼리에서 발생 합니다. EF 코어는 일부 유형의 즉시 로드에 대 한 여러 개의 쿼리를 발행 합니다. 여러 쿼리를 실행 EF6에 일부 쿼리의 경우 보다 효율적일 수 있었던 다음 단일 쿼리 합니다. 즉시 로드로 지정 된 `Include` 및 `ThenInclude` 메서드.

 ![즉시 로드 예제](read-related-data/_static/eager-loading.png)
 
 즉시 로드 컬렉션 nvavigation 포함 되는 경우 여러 개의 쿼리를 보냅니다.

 * 주 쿼리에 대 한 쿼리 
 * "가장자리" 부하 트리의 각 컬렉션에 대해 하나의 쿼리만 합니다.

* 쿼리 구분 `Load`: 쿼리를 별도 데이터를 검색할 수 있습니다 및 EF 코어 "픽스" 탐색 속성입니다. "를 수정" 수단 EF 코어 탐색 속성을 자동으로 채웁니다. 쿼리 구분 `Load` 즉시 로드 보다 로드 explict 비슷합니다.

 ![별도 쿼리 예제](read-related-data/_static/separate-queries.png)

 참고: EF 코어 컨텍스트 인스턴스에 이전에 로드 된 다른 엔터티를 탐색 속성을 자동으로 해결 합니다. 탐색 속성에 대 한 데이터가 있는 경우에 *하지* 경우 일부 속성 채울 수 있습니다 또는 이전에 로드 된 모든 관련된 엔터티가 명시적으로 포함 합니다.

* [명시적 로드](https://docs.microsoft.com/ef/core/querying/related-data#explicit-loading)합니다. 먼저 엔터티를 읽으면 관련된 데이터가 검색 되지 않습니다. 코드를 작성 하는 필요할 때 관련된 데이터를 검색 되어야 합니다. 명시적 별도 쿼리 로드 DB에 전송 하는 여러 쿼리에서 발생 합니다. 명시적 로드 된 코드를 로드 탐색 속성을 지정 합니다. 사용 하 여는 `Load` 명시적 로딩 작업을 수행 하는 메서드. 예:

 ![명시적 로드 예제](read-related-data/_static/explicit-loading.png)

* [지연 로드](https://docs.microsoft.com/ef/core/querying/related-data#lazy-loading)합니다. [EF 코어 현재 지연 로드를 지원 하지 않습니다](https://github.com/aspnet/EntityFrameworkCore/issues/3797)합니다. 먼저 엔터티를 읽으면 관련된 데이터가 검색 되지 않습니다. 탐색 속성에 액세스 하는 처음으로 해당 탐색 속성에 필요한 데이터가 자동으로 검색 됩니다. 쿼리 될 때마다 처음에 대 한 탐색 속성에 액세스 하 여 DB에 전송 됩니다.

* `Select` 연산자 필요한 관련된 데이터를 로드 합니다.

## <a name="create-a-courses-page-that-displays-department-name"></a>부서 이름을 표시 하는 과정 페이지 만들기

포함 된 탐색 속성을 포함 하는 과정 엔터티는 `Department` 엔터티. `Department` 엔터티 과정에 할당 된 부서를 포함 합니다.

에 표시 하려면 할당 된 부서 이름을 과정의 목록:

* 가져오기는 `Name` 에서 속성의 `Department` 엔터티.
* `Department` 에서 제공 되는 엔터티는 `Course.Department` 탐색 속성입니다.

![ourse.Department](read-related-data/_static/dep-crs.png)

<a name="scaffold"></a>
### <a name="scaffold-the-course-model"></a>스 캐 폴드 과정 모델

* Visual Studio를 종료 합니다.
* 프로젝트 디렉터리(*Program.cs*, *Startup.cs* 및 *.csproj* 파일이 포함된 디렉터리)에서 명령 창을 엽니다.
* 다음 명령을 실행합니다.

 ```console
dotnet aspnet-codegenerator razorpage -m Course -dc SchoolContext -udl -outDir Pages\Courses --referenceScriptLibraries
 ```

위의 명령은 스 캐 폴드 된 `Course` 모델입니다. Visual Studio에서 프로젝트를 엽니다.

프로젝트를 빌드합니다. 빌드에서는 다음과 같은 오류를 생성합니다.

`1>Pages/Courses/Index.cshtml.cs(26,37,26,43): error CS1061: 'SchoolContext' does not
 contain a definition for 'Course' and no extension method 'Course' accepting a first
 argument of type 'SchoolContext' could be found (are you missing a using directive or
 an assembly reference?)`

 전역으로 변경 `_context.Course` 를 `_context.Courses` (즉, "s"에 추가 `Course`). 7 번 발견 되 고 업데이트 됩니다.

열기 *Pages/Courses/Index.cshtml.cs* 검사는 `OnGetAsync` 메서드. 스 캐 폴딩 엔진 지정에 대 한 즉시 로드는 `Department` 탐색 속성입니다. `Include` 메서드 즉시 로드를 지정 합니다.

응용 프로그램을 실행 하 고 선택 된 **Courses** 링크 합니다. Department 열에 표시 됩니다는 `DepartmentID`는 도움이 되지 않습니다.

`OnGetAsync` 메서드를 다음 코드로 업데이트합니다.

[!code-csharp[Main](intro/samples/cu/Pages/Courses/Index.cshtml.cs?name=snippet_RevisedIndexMethod)]

앞의 코드를 추가 `AsNoTracking`합니다. `AsNoTracking`반환 되는 엔터티 추적 되지 않으므로 성능이 향상 됩니다. 현재 컨텍스트에서 업데이트 되지 하는 엔터티를 추적 되지 않습니다.

업데이트 *Views/Courses/Index.cshtml* 강조 표시 된 다음 태그로:

[!code-html[](intro/samples/cu/Pages/Courses/Index.cshtml?highlight=4,7,15-17,34-36,44)]

스 캐 폴드 코드에 다음과 같은 변경은 적용 했습니다.

* 인덱스에서 제목 Courses로 변경 합니다.
* 추가 **번호** 보여 주는 열은 `CourseID` 속성 값입니다. 기본적으로 기본 키 있기 때문에 일반적으로 최종 사용자에 게 의미가 스 캐 폴드 되지 않습니다. 그러나이 경우 기본 키가 의미 합니다.
* 변경 된 **부서** 부서 이름을 표시 하는 열입니다. 코드 표시는 `Name` 의 속성은 `Department` 에 로드 된 엔터티는 `Department` 탐색 속성:

  ```html
  @Html.DisplayFor(modelItem => item.Department.Name)
  ```

응용 프로그램을 실행 하 고 선택 된 **Courses** 부서 이름의 목록을 보려면 탭 합니다.

![Courses 인덱스 페이지](read-related-data/_static/courses-index.png)

<a name="select"></a>
### <a name="loading-related-data-with-select"></a>관련 Select와 함께 데이터를 로드

`OnGetAsync` 메서드를 사용 하 여 관련된 데이터 로드는 `Include` 메서드:

[!code-csharp[Main](intro/samples/cu/Pages/Courses/Index.cshtml.cs?name=snippet_RevisedIndexMethod&highlight=4)]

`Select` 연산자 필요한 관련된 데이터를 로드 합니다. 단일 항목에 대 한 같은 `Department.Name` 는 SQL INNER JOIN을 사용 합니다. 컬렉션에 대 한 다른 데이터베이스 액세스를 사용 하 여 하지만 사라지면는 합니다.`Include` 컬렉션에 대 한 연산자입니다.

다음 코드를 사용 하 여 관련된 데이터 로드는 `Select` 메서드:

[!code-csharp[Main](intro/samples/cu/Pages/Courses/IndexSelect.cshtml.cs?name=snippet_RevisedIndexMethod&highlight=4)]

`CourseViewModel`:

[!code-csharp[Main](intro/samples/cu/Models/SchoolViewModels/CourseViewModel.cs?name=snippet)]

참조 [IndexSelect.cshtml](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu/Pages/Courses/IndexSelect.cshtml) 및 [IndexSelect.cshtml.cs](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/cu/Pages/Courses/IndexSelect.cshtml.cs) 는 전체 예제입니다.

## <a name="create-an-instructors-page-that-shows-courses-and-enrollments"></a>만들기 과정 및 등록을 보여 주는 강사 페이지

이 섹션에서는 강사 페이지가 생성 됩니다.

<a name="IP"></a>
![강사 인덱스 페이지](read-related-data/_static/instructors-index.png)

이 페이지를 읽고 다음과 같이 관련된 데이터를 표시 합니다.

* 강사 목록은의 관련된 데이터 표시는 `OfficeAssignment` 엔터티 (위 그림에서 사무실). `Instructor` 및 `OfficeAssignment` 엔터티는 0 또는 1을 한 관계에 있습니다. 즉시 로드에 사용 되는 `OfficeAssignment` 엔터티. 즉시 로드는 관련된 데이터를 표시 해야 하는 경우 일반적으로 더 효율적입니다. 이 경우 사무실 할당에서 강사에 게 표시 됩니다.
* 사용자가 관련 강사 (위 그림에서 Harui)를 선택 하는 경우 `Course` 엔터티 표시 됩니다. `Instructor` 및 `Course` 엔터티가 서로 다 대 다 관계에 있습니다. 에 대 한 로드 eager는 `Course` 엔터티 및 관련 `Department` 엔터티 사용 됩니다. 이 경우 선택한 강사에 대 한 과정만 더 필요 하므로 별개의 쿼리와 더 효율적일 수 있습니다. 이 예제에는 탐색 속성에 있는 엔터티에서 탐색 속성에 대 한 즉시 로드를 사용 하는 방법을 보여 줍니다.
* 데이터와 관련 된 사용자가 과정 (위 그림에서 화학)를 선택 하는 경우는 `Enrollments` 엔터티가 표시 됩니다. 위 그림에서는 학생 이름 및 등급 표시 됩니다. `Course` 및 `Enrollment` 엔터티가 서로 일 대 다 관계에 있습니다.

### <a name="create-a-view-model-for-the-instructor-index-view"></a>강사 인덱스 보기에 대 한 뷰 모델 만들기

강사 페이지는 서로 다른 세 테이블에서 데이터를 표시합니다. 뷰 모델 3 개의 테이블을 나타내는 세 개의 엔터티가 포함 된 만들어집니다.

에 *SchoolViewModels* 폴더를 만들 *InstructorIndexData.cs* 를 다음 코드로:

[!code-csharp[Main](intro/samples/cu/Models/SchoolViewModels/InstructorIndexData.cs)]

### <a name="scaffold-the-instructor-model"></a>스 캐 폴드 강사 모델

* Visual Studio를 종료 합니다.
* 프로젝트 디렉터리(*Program.cs*, *Startup.cs* 및 *.csproj* 파일이 포함된 디렉터리)에서 명령 창을 엽니다.
* 다음 명령을 실행합니다.

 ```console
dotnet aspnet-codegenerator razorpage -m Instructor -dc SchoolContext -udl -outDir Pages\Instructors --referenceScriptLibraries
 ```

위의 명령은 스 캐 폴드 된 `Instructor` 모델입니다. Visual Studio에서 프로젝트를 엽니다.

프로젝트를 빌드합니다. 빌드 오류를 생성 합니다.

전역으로 변경 `_context.Instructor` 를 `_context.Instructors` (즉, "s"에 추가 `Instructor`). 7 번 발견 되 고 업데이트 됩니다.

응용 프로그램을 실행 하 고 강사 페이지로 이동 합니다.

대체 *Pages/Instructors/Index.cshtml.cs* 를 다음 코드로:

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Index1.cshtml.cs?name=snippet_all&highlight=2,20-)]

`OnGetAsync` 메서드 선택한 강사의 ID에 대 한 선택적 경로 데이터를 적용 합니다.

쿼리를 검사는 *Pages/Instructors/Index.cshtml* 페이지:

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Index1.cshtml.cs?name=snippet_ThenInclude)]

에 쿼리는 두 개의 포함 됩니다.

* `OfficeAssignment`:에 표시 되는 [강사 보기](#IP)합니다.
* `CourseAssignments`:를 알게 과목에 제공 합니다.


### <a name="update-the-instructors-index-page"></a>강사 인덱스 페이지를 업데이트 합니다.

업데이트 *Pages/Instructors/Index.cshtml* 다음 태그로:

[!code-html[](intro/samples/cu/Pages/Instructors/IndexRRD.cshtml?range=1-65&highlight=1,5,8,16-21,25-32,43-57)]

위의 태그에서는 다음과 같이 변경 합니다.

* 업데이트는 `page` 지시어를 `@page` 를 `@page "{id:int?}"`합니다. `"{id:int?}"`경로 템플릿입니다. 경로 템플릿 경로 데이터를 URL에 쿼리 문자열을 정수를 변경합니다. 예를 들어,를 클릭 하 고 **선택** 강사 다음과 같은 URL을 생성 하는 page 지시문에 대 한 링크:

    `http://localhost:1234/Instructors?id=2`

    Page 지시문 경우 `@page "{id:int?}"`, 이전 URL이 있습니다.

    `http://localhost:1234/Instructors/2`

* 페이지 제목은 **강사**합니다.
* 추가 **Office** 표시 하는 열 `item.OfficeAssignment.Location` 경우에만 `item.OfficeAssignment` 이 null이 아닌 합니다. 0 또는 1을 한 관계 이기 때문에 있을 수 있습니다 하지 관련된 OfficeAssignment 엔터티.

  ```html
  @if (item.OfficeAssignment != null)
  {
      @item.OfficeAssignment.Location
  }
  ```

* 추가 **Courses** 과정을 표시 하는 열에서 각 강사 배웠습니다. 참조 [명시적 줄 전환을 `@:` ](xref:mvc/views/razor#explicit-line-transition-with-) 이 razor 구문에 대 한 자세한 합니다.

* 동적으로 추가 하는 추가 된 코드 `class="success"` 에 `tr` 선택한 강사의 요소입니다. 부트스트랩 클래스를 사용 하 여 선택된 된 행에 대 한 배경색을 설정 합니다.

  ```html
  string selectedRow = "";
  if (item.CourseID == Model.CourseID)
  {
      selectedRow = "success";
  }
  <tr class="@selectedRow">
  ```

* 레이블이 지정 된 새 하이퍼링크 추가 **선택**합니다. 이 링크를 선택한 강의 ID 보냅니다는 `Index` 메서드 배경색을 가져오거나 설정 합니다.

  ```html
  <a asp-action="Index" asp-route-id="@item.ID">Select</a> |
  ```

응용 프로그램을 실행 하 고 선택 된 **강사** 탭 합니다. 페이지에 표시 됩니다는 `Location` (사무실)에서 관련 `OfficeAssignment` 엔터티. 경우 OfficeAssignment'는 null, 빈 테이블 셀 표시 됩니다.

![강사 인덱스 페이지에는 아무 선택](read-related-data/_static/instructors-index-no-selection.png)

클릭는 **선택** 링크 합니다. 행 스타일 변경 됩니다.

### <a name="add-courses-taught-by-selected-instructor"></a>선택한 강사 여 강좌 추가

업데이트는 `OnGetAsync` 메서드에서 *Pages/Instructors/Index.cshtml.cs* 를 다음 코드로:

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Index2.cshtml.cs?name=snippet_OnGetAsync&highlight=1,8,16-)]

업데이트 된 쿼리를 검토 합니다.

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Index2.cshtml.cs?name=snippet_ThenInclude)]

추가 하는 앞의 쿼리는 `Department` 엔터티.

다음 코드를 실행 하는 강사가 선택 된 경우 (`id != null`). 선택한 강사 강사 보기 모델에 있는 목록에서 검색 됩니다. 뷰 모델 `Courses` 속성으로 로드 되는 `Course` 해당 강사에서 엔터티에 `CourseAssignments` 탐색 속성입니다.

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Index2.cshtml.cs?name=snippet_ID)]

`Where` 메서드 컬렉션을 반환 합니다. 앞에서 `Where` 메서드를 하나만 `Instructor` 엔터티가 반환 됩니다. `Single` 메서드를 하나의 컬렉션 변환 `Instructor` 엔터티. `Instructor` 에 대 한 액세스를 제공 하는 엔터티는 `CourseAssignments` 속성입니다. `CourseAssignments`관련 된 항목에 대 한 액세스를 제공 `Course` 엔터티.

![강사-Courses m:M](complex-data-model/_static/courseassignment.png)

`Single` 메서드는 컬렉션의 항목을 하나만 때 컬렉션에서 사용 됩니다. `Single` 컬렉션은 비어 있거나 둘 이상의 항목이 없는 경우 메서드에서 예외를 throw 합니다. 대신 `SingleOrDefault`, 값을 반환 하는 기본값 (이 경우 null) 컬렉션이 비어 있는 경우. 사용 하 여 `SingleOrDefault` 빈 컬렉션에:

* 예외가 발생 (에서 찾으려고 하는 `Courses` 속성에 null 참조).
* 예외 메시지는 문제의 원인을 477860 덜 명확 하 게 합니다.

다음 코드의 보기 모델을 채우는 `Enrollments` 속성 과정을 선택 합니다.

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Index2.cshtml.cs?name=snippet_courseID)]

끝에 다음 태그를 추가 *Pages/Courses/Index.cshtml* Razor 페이지:

[!code-html[](intro/samples/cu/Pages/Instructors/IndexRRD.cshtml?range=60-102&highlight=7-)]

위의 태그 courses 강사 강사 선택 된 경우와 관련 된 목록이 표시 됩니다.

응용 프로그램을 테스트 합니다. 클릭는 **선택** 강사 페이지에 링크 합니다.

![강사 인덱스 페이지 강사 선택](read-related-data/_static/instructors-index-instructor-selected.png)

### <a name="show-student-data"></a>학생 데이터를 표시 합니다.

이 섹션에서는 응용 프로그램은 선택한 과정에 학생 데이터를 표시 하도록 업데이트 됩니다.

업데이트에 대 한 쿼리는 `OnGetAsync` 메서드에서 *Pages/Instructors/Index.cshtml.cs* 를 다음 코드로:

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Index.cshtml.cs?name=snippet_ThenInclude&highlight=6-9)]

업데이트 *Pages/Instructors/Index.cshtml*합니다. 파일의 끝에 다음 태그를 추가 합니다.

[!code-html[](intro/samples/cu/Pages/Instructors/IndexRRD.cshtml?range=103-)]

위의 태그 선택한 과정에서 등록 된 학생의 목록이 표시 됩니다.

페이지를 새로 고치고 강사를 선택 합니다. 등록 된 학생 자신의 등급의 목록을 보려면 과정을 선택 합니다.

![강사 인덱스 페이지 강사 및 선택한 과정](read-related-data/_static/instructors-index.png)

## <a name="using-single"></a>단일를 사용 하 여

`Single` 에서 메서드를 전달할 수는 `Where` 조건을 호출 하는 대신는 `Where` 메서드 별도로:

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/IndexSingle.cshtml.cs?name=snippet_single&highlight=21,28-29)]

위의 `Single` 접근 방식을 사용 하 여에 비해 없습니다 장점을 제공 `Where`합니다. 일부 개발자는 `Single` 스타일에 접근 합니다.

## <a name="explicit-loading"></a>명시적 로드

현재 코드에 대 한 즉시 로드 지정 `Enrollments` 및 `Students`:

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/Index.cshtml.cs?name=snippet_ThenInclude&highlight=6-9)]

사용자가 등록 과정에서 참조 하려고 거의 가정 합니다. 이 경우 최적화 분석이 요청 된 경우에 등록 데이터를 로드 하는 것입니다. 이 섹션에서는 `OnGetAsync` 명시적 로드를 사용 하도록 업데이트 `Enrollments` 및 `Students`합니다.

업데이트는 `OnGetAsync` 다음 코드를 사용 합니다.

[!code-csharp[Main](intro/samples/cu/Pages/Instructors/IndexXp.cshtml.cs?name=snippet_OnGetAsync&highlight=9-13,29-35)]

위의 코드 삭제는 *ThenInclude* 등록 및 학생 데이터에 대 한 메서드를 호출 합니다. 과정을 선택 하면 강조 표시 된 코드를 검색 합니다.

* `Enrollment` 선택한 과정에 대 한 엔터티.
* `Student` 각각에 대 한 엔터티 `Enrollment`합니다.

위의 코드를 주석으로 표시 `.AsNoTracking()`합니다. 탐색 속성 추적 된 엔터티에 대 한 명시적으로 로드할만 있습니다.

응용 프로그램을 테스트 합니다. 사용자 관점에서 응용 프로그램에서 이전 버전으로 동일 하 게 동작합니다.

다음 자습서에는 관련된 데이터를 업데이트 하는 방법을 보여 줍니다.

>[!div class="step-by-step"]
>[이전](xref:data/ef-rp/complex-data-model)
>[다음](xref:data/ef-rp/update-related-data)
