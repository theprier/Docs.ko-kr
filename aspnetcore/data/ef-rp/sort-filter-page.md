---
title: "EF 코어-정렬, 필터, 페이징-8 3 razor 페이지"
author: rick-anderson
description: "이 자습서에서는 정렬, 필터링 및 페이징을 ASP.NET 코어 및 Entity Framework 코어를 사용 하 여 페이지 기능을 추가 합니다."
ms.author: riande
ms.date: 10/22/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: data/ef-rp/sort-filter-page
ms.openlocfilehash: 08f00e183dd8a8daa883d0b9ff15698b3a39f625
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="sorting-filtering-paging-and-grouping---ef-core-with-razor-pages-3-of-8"></a>정렬, 필터링, 페이징 및 그룹화-EF 코어 Razor 페이지 (3 / 8)

여 [Tom Dykstra](https://github.com/tdykstra), [Rick Anderson](https://twitter.com/RickAndMSFT), 및 [Jon P Smith](https://twitter.com/thereformedprog)

[!INCLUDE[about the series](../../includes/RP-EF/intro.md)]

이 자습서, 정렬, 필터링, 그룹화 및 페이징에 기능 추가 됩니다.

다음 그림은 완료 된 페이지를 보여 줍니다. 열 머리글은 열을 정렬에 대 한 링크가 있습니다. 열 머리글을 반복 해 서 클릭 하면 오름차순 및 내림차순 정렬 순서 사이 전환 합니다.

![학생 인덱스 페이지](sort-filter-page/_static/paging.png)

문제를 해결할 수 없는를 실행 하는 경우 다운로드는 [이 단계에 대 한 완성 된 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part3-sorting)합니다.

## <a name="add-sorting-to-the-index-page"></a>인덱스 페이지에 정렬을 추가합니다

문자열에 추가 *Students/Index.cshtml.cs* `PageModel` 정렬의 매개 변수를 포함 하도록 합니다.

[!code-csharp[Main](intro/samples/cu/Pages/Students/Index.cshtml.cs?name=snippet1&highlight=10-13)]


업데이트는 *Students/Index.cshtml.cs* `OnGetAsync` 를 다음 코드로:

[!code-csharp[Main](intro/samples/cu/Pages/Students/Index.cshtml.cs?name=snippet_SortOnly)]

위의 코드는 수신는 `sortOrder` URL에 쿼리 문자열에서 매개 변수입니다. URL (쿼리 문자열 포함)에서 생성 되는 [앵커 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper
)

`sortOrder` 매개 변수는 "Name" 또는 "날짜"입니다. `sortOrder` 매개 변수 "_desc" 내림차순을 지정 하 여 필요에 따라 됩니다. 기본 정렬 순서는 오름차순입니다.

인덱스 페이지를 요청 하는 경우는 **학생** 연결, 쿼리 문자열이 없습니다. 학생 성을 기준으로 오름차순 표시 됩니다. 값이 기본값 (fall 통해 경우) 성을 기준으로 오름차순의 `switch` 문. 적절 한 열 제목 링크를 클릭 하면 `sortOrder` 쿼리 문자열 값에 값을 제공 합니다.

`NameSort`및 `DateSort` Razor 페이지에서 적절 한 쿼리 문자열 값을 사용 하 여 열 머리글 하이퍼링크를 구성 하는 데 사용 됩니다.

[!code-csharp[Main](intro/samples/cu/Pages/Students/Index.cshtml.cs?name=snippet_SortOnly&highlight=3-4)]

다음 코드에 C# [?: 연산자](https://docs.microsoft.com/dotnet/csharp/language-reference/operators/conditional-operator):

[!code-csharp[Main](intro/samples/cu/Pages/Students/Index.cshtml.cs?name=snippet_Ternary)]

첫 번째 줄 지정 `sortOrder` null 이거나 비어 있어서 `NameSort` "name_desc"로 설정 되어 경우 `sortOrder` 은 **하지** null 이거나 비어 있는 경우 `NameSort` 빈 문자열로 설정 됩니다.

`?: operator` 삼항 연산자는 라고도 합니다.

열 머리글 하이퍼링크를 다음과 같이 설정 하려면 보기를 사용 하는이 두 개의 문:

| 현재 정렬 순서 | 마지막 이름 하이퍼링크 | 날짜 하이퍼링크 |
|:--------------------:|:-------------------:|:--------------:|
| 이름 오름차순 마지막 | descending        | ascending      |
| 이름 내림차순 마지막 | ascending           | ascending      |
| 오름차순 날짜       | ascending           | descending     |
| 내림차순 날짜      | ascending           | ascending      |

메서드가 LINQ to Entities 사용 하 여 기준으로 정렬 하려면 열을 지정 합니다. 코드를 초기화 한 `IQueryable<Student> ` switch 문의 하기 전에 switch 문에 수정:

[!code-csharp[Main](intro/samples/cu/Pages/Students/Index.cshtml.cs?name=snippet_SortOnly&highlight=6-)]

 경우는`IQueryable` 를 만들거나 수정 하 고, 데이터베이스에 쿼리가 전송 됩니다. 쿼리 될 때까지 실행 되지 않습니다는 `IQueryable` 개체 컬렉션으로 변환 됩니다. `IQueryable`와 같은 메서드를 호출 하 여 컬렉션으로 변환 됩니다 `ToListAsync`합니다. 따라서는 `IQueryable` 되어야 다음 문을 실행 하는 단일 쿼리 결과 코드:

[!code-csharp[Main](intro/samples/cu/Pages/Students/Index.cshtml.cs?name=snippet_SortOnlyRtn)]

`OnGetAsync`열의 다 수 포함 된 자세한 정보를 가져올 수 있습니다.

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a>열 머리글 하이퍼링크 학생 인덱스 뷰를 추가

코드 *Students/Index.cshtml*, 다음 코드를 강조 표시 합니다.

[!code-html[](intro/samples/cu/Pages/Students/Index2.cshtml?highlight=17-19,25-27)]

위의 코드:

* 하이퍼링크를 추가 하는 `LastName` 및 `EnrollmentDate` 열 머리글입니다.
* 정보를 사용 하 여 `NameSort` 및 `DateSort` 현재 정렬 순서 값으로 하이퍼링크를 설정 하려면.

확인 하려면 작동을 정렬 합니다.

* 응용 프로그램을 실행 하 고 선택 된 **학생** 탭 합니다.
* 클릭 **성**합니다.
* 클릭 **등록 날짜**합니다.

코드를 더 잘 이해 하려면 따릅니다.

* *Student/Index.cshtml.cs*에 중단점을 설정 `switch (sortOrder)`합니다.
* 에 대 한 조사식을 추가 `NameSort` 및 `DateSort`합니다.
* *Student/Index.cshtml*에 중단점을 설정 `@Html.DisplayNameFor(model => model.Student[0].LastName)`합니다.

디버거 단계별로 실행 합니다.

## <a name="add-a-search-box-to-the-students-index-page"></a>검색 상자 학생 인덱스 페이지에 추가

필터링을 추가 하려면 학생 인덱스 페이지에:

* 텍스트 상자 및 전송 단추가 Razor 페이지에 추가 됩니다. 텍스트 상자에서 첫 번째 또는 마지막 이름에 검색 문자열을 제공합니다.
* 코드 숨김 파일은 텍스트 상자 값을 사용 하도록 업데이트 됩니다.

### <a name="add-filtering-functionality-to-the-index-method"></a>Index 메서드에 필터링 기능 추가

업데이트는 *Students/Index.cshtml.cs* `OnGetAsync` 를 다음 코드로:

[!code-csharp[Main](intro/samples/cu/Pages/Students/Index.cshtml.cs?name=snippet_SortFilter&highlight=1,5,9-13)]

위의 코드:

* 추가 `searchString` 매개 변수는 `OnGetAsync` 메서드. 검색 문자열 값이 다음 섹션에 추가 된 텍스트 상자에서 수신 합니다.
* LINQ 명령문에 추가 `Where` 절. `Where` 절 해당 이름 또는 성을 검색 문자열을 포함 하는 학생만을 선택 합니다. LINQ 명령문에 대 한 검색 값이 있는 경우에 실행 됩니다.

참고: 위의 코드 호출은 `Where` 에서 메서드는 `IQueryable` 개체 및 필터는 서버에서 처리 됩니다. 일부 시나리오에서는 tha 응용 프로그램을 호출 수는 `Where` 메모리 내 컬렉션에 대 한 확장 메서드이기 메서드. 예를 들어 `_context.Students` EF 코어에서 변경 `DbSet` 반환 하는 저장소 메서드에 `IEnumerable` 컬렉션입니다. 결과 일반적으로 동일 하지만 경우에 따라 다를 수 있습니다.

예를 들어의.NET Framework 구현은 `Contains` 기본적으로 대/소문자 구분 비교를 수행 합니다. SQL Server에서 `Contains` 대/소문자 구분 SQL Server 인스턴스의 데이터 정렬 설정에 의해 결정 됩니다. SQL Serve 기본적으로 대/소문자 구분 됩니다. `ToUpper`명시적으로 대/소문자 구분 테스트를 호출할 수 있습니다.

`Where(s => s.LastName.ToUpper().Contains(searchString.ToUpper())`

위의 코드는 확인 결과 대/소문자를 사용 하는 코드가 변경 하는 경우 `IEnumerable`합니다. 때 `Contains` 라고 하는 `IEnumerable` 컬렉션,.NET Core 구현이 사용 됩니다. 때 `Contains` 라고 하는 `IQueryable` 개체, 데이터베이스 구현이 사용 됩니다. 반환 된 `IEnumerable` 리포지토리에서 상당한 성능 조기 결제 수수료를 가질 수 있습니다.

1. DB 서버에서 모든 행 반환 됩니다.
1. 필터는 응용 프로그램에서 반환된 된 모든 행에 적용 됩니다.

호출에 대 한 성능 저하는 `ToUpper`합니다. `ToUpper` 코드 TSQL SELECT 문의 WHERE 절에 함수를 추가 합니다. 추가 된 함수는 인덱스를 사용 하 여 최적화 프로그램을 방지 합니다. SQL 대/소문자 비구분으로 설치 되어 있다고 가정 것이 좋습니다는 `ToUpper` 필요 하지 않은 경우 호출 합니다.

### <a name="add-a-search-box-to-the-student-index-view"></a>검색 상자 학생 인덱스 뷰를 추가

*Views/Student/Index.cshtml*, 다음 강조 표시 된 코드를 추가 **검색** 단추와 다양 한 크롬 합니다.

[!code-html[](intro/samples/cu/Pages/Students/Index3.cshtml?highlight=14-23&range=1-25)]

앞의 코드를 사용 하 여는 `<form>` [태그 도우미](xref:mvc/views/tag-helpers/intro) 검색 텍스트 상자 및 단추를 추가 합니다. 기본적으로는 `<form>` 태그 도우미는 POST로 양식 데이터를 전송 합니다. Post, 매개 변수는 URL 및 HTTP 메시지 본문에 전달 됩니다. HTTP GET을 사용 하는 양식 데이터 URL에 쿼리 문자열로 전달 됩니다. URL에 책갈피를 사용 하면 쿼리 문자열을 사용 하 여 데이터를 전달 합니다. [W3C 지침](https://www.w3.org/2001/tag/doc/whenToUseGet.html) 작업이 업데이트 되지 않습니다 경우 GET를 사용 해야 하는 것이 좋습니다.

앱을 테스트합니다.

* 선택 된 **학생** 탭 하 고 검색 문자열을 입력 합니다.
* 선택 **검색**합니다.

검색 문자열은 URL에 포함 되어 있는지 확인 합니다.

```html
http://localhost:5000/Students?SearchString=an
```

책갈피 페이지에 대 한 URL이 포함 된 페이지의 책갈피가 설정 하는 경우와 `SearchString` 쿼리 문자열입니다. `method="get"` 에 `form` 태그는 원인을 쿼리 문자열을 생성할 수 있습니다.

현재 열 머리글 정렬 링크 옵션을 선택 하면 필터 값에서 **검색** 상자 손실 됩니다. 손실 된 필터 값은 다음 섹션에서 고정 되어 있습니다.

## <a name="add-paging-functionality-to-the-students-index-page"></a>학생 인덱스 페이지에 페이징 기능을 추가 합니다.

이 섹션에서는 `PaginatedList` 페이징을 지원 하기 위해 클래스가 만들어집니다. `PaginatedList` 사용 하 여 `Skip` 및 `Take` 문은 테이블의 모든 행을 검색 하는 대신 서버에서 데이터를 필터링 합니다. 다음 그림에는 페이징 단추가 나와 있습니다.

![학생 인덱스 페이징 링크가 있는 페이지](sort-filter-page/_static/paging.png)

프로젝트 폴더에서 만들 `PaginatedList.cs` 를 다음 코드로:

[!code-csharp[Main](intro/samples/cu/PaginatedList.cs)]

`CreateAsync` 위의 코드에서 메서드는 페이지 크기 및 페이지 번호를 사용 하 고 적절 한 적용 `Skip` 및 `Take` 문을 `IQueryable`합니다. 때 `ToListAsync` 라고 하는 `IQueryable`, 요청된 된 페이지를 포함 하는 목록을 반환 합니다. 속성 `HasPreviousPage` 및 `HasNextPage` 설정 또는 해제 하는 데 사용 된 **이전** 및 **다음** 단추 페이징 합니다.

`CreateAsync` 메서드 만드는 데 사용 되는 `PaginatedList<T>`합니다. 생성자를 만들 수 없습니다는 `PaginatedList<T>` 개체 생성자는 비동기 코드를 실행할 수 없습니다.

## <a name="add-paging-functionality-to-the-index-method"></a>인덱스 메서드에 페이징 기능을 추가 합니다.

*Students/Index.cshtml.cs*, 유형을 업데이트 `Student` 에서 `IList<Student>` 를 `PaginatedList<Student>`:

[!code-csharp[Main](intro/samples/cu/Pages/Students/Index.cshtml.cs?name=snippet_SortFilterPageType)]

업데이트는 *Students/Index.cshtml.cs* `OnGetAsync` 를 다음 코드로:

[!code-csharp[Main](intro/samples/cu/Pages/Students/Index.cshtml.cs?name=snippet_SortFilterPage&highlight=1-4,7-14,41-)]

현재 페이지 인덱스를 추가 하는 위의 코드 `sortOrder`, 및 `currentFilter` 메서드 서명을 합니다.

[!code-csharp[Main](intro/samples/cu/Pages/Students/Index.cshtml.cs?name=snippet_SortFilterPage2)]

모든 매개 변수는 다음 경우에 null:

* 페이지에서 호출 되는 **학생** 링크 합니다.
* 사용자는 페이징 또는 정렬 링크 클릭 하지 않았습니다.

페이징 링크를 클릭 하면 페이지 인덱스 변수는 표시할 페이지 번호를 포함 합니다.

`CurrentSort`현재 정렬 순서 Razor 페이지를 제공합니다. 현재 정렬 순서를 페이징 하는 동안 정렬 순서를 유지 하려면 페이징 링크에 포함 되어야 합니다.

`CurrentFilter`현재 필터 문자열로 Razor 페이지를 제공합니다. `CurrentFilter` 값:

* 페이징 하는 동안 필터 설정을 유지 하기 위해 페이징 링크에 포함 되어야 합니다.
* 페이지 다시 표시 하는 경우 텍스트 상자에 복원 합니다.

검색 문자열 페이징 하는 동안 변경 되 면 페이지 1로 다시 설정 됩니다. 페이지에서 표시할 다른 데이터를 새 필터 발생할 수 있기 때문에 1로 다시 사용 해야 합니다. 검색 값을 입력 하는 경우 및 **전송** 을 선택 합니다.

* 검색 문자열이 변경 됩니다.
* `searchString` 매개 변수는 null입니다.

[!code-csharp[Main](intro/samples/cu/Pages/Students/Index.cshtml.cs?name=snippet_SortFilterPage3)]

`PaginatedList.CreateAsync` 메서드 학생 페이징을 지원 되는 컬렉션 형식에는 단일 페이지로 학생 쿼리를 변환 합니다. 학생 들의 해당 단일 페이지 Razor 페이지에 전달 됩니다.

[!code-csharp[Main](intro/samples/cu/Pages/Students/Index.cshtml.cs?name=snippet_SortFilterPage4)]

두 물음표 `PaginatedList.CreateAsync` 나타냅니다는 [null 병합 연산자](https://docs.microsoft.com/ dotnet/csharp/language-reference/operators/null-conditional-operator)합니다. Null 병합 연산자는 null 허용 형식에 대 한 기본값을 정의합니다. 식 `(pageIndex ?? 1)` 의 값을 반환 하는 수단 `pageIndex` 값이 있는 경우. 경우 `pageIndex` 값, 1을 반환 하지 않습니다.

## <a name="add-paging-links-to-the-student-razor-page"></a>Razor 페이지 학생에 페이징 링크 추가

태그가 업데이트 *Students/Index.cshtml*합니다. 변경 내용은 강조 표시 됩니다.

[!code-html[](intro/samples/cu/Pages/Students/Index.cshtml?highlight=28-31,37-40,68-)]

열 머리글 링크 쿼리 문자열을 사용 하 여 현재 검색 문자열을 전달 하는 `OnGetAsync` 메서드 사용자 필터 결과 내에서 정렬할 수 있도록 합니다.

[!code-html[](intro/samples/cu/Pages/Students/Index.cshtml?range=28-31)]

태그 도우미에서 페이징 단추가 표시 됩니다.

[!code-html[](intro/samples/cu/Pages/Students/Index.cshtml?range=72-)]

응용 프로그램을 실행 하 고 학생 페이지로 이동 합니다.

* 있는지 페이징 작동을 위해 서로 다른 정렬 순서에서 페이징 링크를 클릭 합니다.
* 정렬 및 필터링 된 페이징 올바르게 작동 하는지 확인 하려면 검색 문자열을 입력 페이징을 시도 하십시오.

![학생 인덱스 페이징 링크가 있는 페이지](sort-filter-page/_static/paging.png)

코드를 더 잘 이해 하려면 따릅니다.

* *Student/Index.cshtml.cs*에 중단점을 설정 `switch (sortOrder)`합니다.
* 에 대 한 조사식을 추가 `NameSort`, `DateSort`, `CurrentSort`, 및 `Model.Student.PageIndex`합니다.
* *Student/Index.cshtml*에 중단점을 설정 `@Html.DisplayNameFor(model => model.Student[0].LastName)`합니다.

디버거 단계별로 실행 합니다.

## <a name="update-the-about-page-to-show-student-statistics"></a>학생 통계를 표시 하도록 정보 페이지를 업데이트

이 단계에서는 *Pages/About.cshtml* 각 등록 날짜에 대해 등록 한 학생 수를 표시 하도록 업데이트 됩니다. 업데이트는 그룹화를 사용 하며 다음 단계로 구성 됩니다.

* 사용 되는 데이터에 대 한 보기 모델 클래스 만들기는 **에 대 한** 페이지.
* Razor 페이지에 대 한 및 코드 숨김 파일을 수정 합니다.

### <a name="create-the-view-model"></a>뷰 모델 만들기

만들기는 *SchoolViewModels* 폴더에는 *모델* 폴더입니다.

에 *SchoolViewModels* 폴더를 추가 *EnrollmentDateGroup.cs* 를 다음 코드로:

[!code-csharp[Main](intro/samples/cu/Models/SchoolViewModels/EnrollmentDateGroup.cs)]

### <a name="update-the-about-code-behind-page"></a>업데이트 정보 코드 숨김 페이지

업데이트는 *Pages/About.cshtml.cs* 를 다음 코드로 파일:

[!code-csharp[Main](intro/samples/cu/Pages/About.cshtml.cs)]

LINQ 명령문 학생 엔터티 등록 날짜별으로 그룹화 각 그룹에 있는 엔터티 수를 계산 하 고 컬렉션의 결과 저장할지 `EnrollmentDateGroup` 모델 개체를 보고 합니다.

참고: LINQ `group` 명령 EF 코어에서 현재 지원 되지 않습니다. 위의 코드에서 모든 학생 레코드는 SQL Server에서 반환 됩니다. `group` 명령은 SQL 서버에 없는 Razor 페이지 응용 프로그램에 적용 됩니다. EF 코어 2.1이이 LINQ 지원할 `group` SQL Server에서 발생 하는 연산자와 그룹화 합니다. 참조 [관계: to SQL groupby () 함수의 변환 하는 기능이 지원](https://github.com/aspnet/EntityFrameworkCore/issues/2341)합니다. [EF 코어 2.1](https://github.com/aspnet/EntityFrameworkCore/wiki/roadmap) .NET Core 2.1을 사용 하 여 해제 됩니다. 자세한 내용은 참조는 [.NET Core 로드맵](https://github.com/dotnet/core/blob/master/roadmap.md)합니다.

### <a name="modify-the-about-razor-page"></a>수정 된 Razor 페이지에 대 한

코드는 *Views/Home/About.cshtml* 를 다음 코드로 파일:

[!code-html[](intro/samples/cu/Pages/About.cshtml)]

응용 프로그램을 실행 하 고 정보 페이지로 이동 합니다. 각 등록 날짜에 대 한 학생 수는 테이블에 표시 됩니다.

문제를 해결할 수 없는를 실행 하는 경우 다운로드는 [이 단계에 대 한 완성 된 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part3-sorting)합니다.

![페이지 정보](sort-filter-page/_static/about.png)

## <a name="additional-resources"></a>추가 리소스

* [ASP.NET Core 2.x 소스 디버깅](https://github.com/aspnet/Docs/issues/4155)

다음 자습서 응용 프로그램 마이그레이션을 사용 하 여 데이터 모델을 업데이트 합니다.

>[!div class="step-by-step"]
[이전](xref:data/ef-rp/crud)
[다음](xref:data/ef-rp/migrations)
