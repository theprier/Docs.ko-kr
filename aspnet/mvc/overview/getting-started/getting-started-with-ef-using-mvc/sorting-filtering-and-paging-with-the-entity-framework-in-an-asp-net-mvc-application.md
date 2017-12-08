---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: "정렬, 필터링 및 ASP.NET MVC 응용 프로그램에서 Entity Framework와 함께 페이징 | Microsoft Docs"
author: tdykstra
description: "Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 6 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/01/2015
ms.topic: article
ms.assetid: d5723e46-41fe-4d09-850a-e03b9e285bfa
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 8d11bf47f8c43040ef30d7132f0bb756748dbacd
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application"></a>정렬, 필터링 및 ASP.NET MVC 응용 프로그램에서 Entity Framework와 함께 페이징
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트를 다운로드](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8) 또는 [PDF 다운로드](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)

> Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 6 Code First 및 Visual Studio 2013을 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대 한 정보를 참조 하십시오. [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.


이전 자습서에서에 대 한 기본적인 CRUD 작업에 대 한 웹 페이지의 집합을 구현 하기 `Student` 엔터티. 이 자습서에서는 정렬, 필터링 및 페이징 기능을를 추가 합니다는 **학생** 인덱스 페이지입니다. 단순 그룹화를 수행 하는 페이지를 만들 수 있습니다.

다음은 페이지 모양은 완료 되 면입니다. 열 머리글은 해당 열으로 정렬 하기 위해 클릭할 수 있는 링크입니다. 열 머리글을 반복 해 서 클릭 하면 오름차순 및 내림차순 정렬 순서 사이 토글합니다.

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

## <a name="add-column-sort-links-to-the-students-index-page"></a>학생 인덱스 페이지에 열 정렬 링크 추가

학생 인덱스 페이지에 정렬를 추가 하려면 변경는 `Index` 의 메서드는 `Student` 컨트롤러 코드를 추가 하는 `Student` 뷰.

### <a name="add-sorting-functionality-to-the-index-method"></a>Index 메서드에 정렬 기능 추가

*Controllers\StudentController.cs*, 대체 된 `Index` 메서드를 다음 코드로:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

이 코드는 수신 된 `sortOrder` URL에 쿼리 문자열에서 매개 변수입니다. 쿼리 문자열 값은 ASP.NET MVC에서 작업 메서드에 매개 변수로 제공 됩니다. 매개 변수는 "Name" 또는 "날짜" 밑줄과 문자열 "desc" 내림차순을 지정 하 여 필요에 따라 문자열로 됩니다. 기본 정렬 순서는 오름차순입니다.

인덱스 페이지를 요청 하 고, 처음으로 쿼리 문자열이 없는 합니다. 학생 오름차순으로 표시 됩니다 `LastName`, 기본값인의 fall 통해 사례에서 설정한는 `switch` 문. 적절 한 열 머리글 하이퍼링크를 클릭 하면 `sortOrder` 쿼리 문자열에 값을 제공 합니다.

두 `ViewBag` 뷰 열 머리글 하이퍼링크를 적절 한 쿼리 문자열 값으로 구성할 수 있도록 변수는 사용:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

이들은 삼항 문입니다. 첫 번째 지정 되는 경우는 `sortOrder` 매개 변수는 null 이거나 비어 있는 경우 `ViewBag.NameSortParm` 로 설정 해야 "이름\_desc", 그렇지 않으면 빈 문자열로 설정 해야 합니다. 열 머리글 하이퍼링크를 다음과 같이 설정 하려면 보기를 사용 하는이 두 개의 문:

| 현재 정렬 순서 | 마지막 이름 하이퍼링크 | 날짜 하이퍼링크 |
| --- | --- | --- |
| 이름 오름차순 마지막 | descending | ascending |
| 이름 내림차순 마지막 | ascending | ascending |
| 오름차순 날짜 | ascending | descending |
| 내림차순 날짜 | ascending | ascending |

메서드에서 사용 [LINQ to Entities](https://msdn.microsoft.com/en-us/library/bb386964.aspx) 기준으로 정렬 하려면 열을 지정 합니다. 코드를 만듭니다는 [IQueryable](https://msdn.microsoft.com/en-us/library/bb351562.aspx) 하기 전에 변수는 `switch` 문을 수정에 `switch` 문 및 호출은 `ToList` 후 메서드는 `switch` 문. 생성 및 수정할 `IQueryable` 변수 쿼리가 없는 데이터베이스에 전송 됩니다. 변환 될 때까지 쿼리가 실행 되지 않습니다는 `IQueryable` 개체와 같은 메서드를 호출 하 여 컬렉션에 `ToList`합니다. 따라서이 코드 발생 되어야 실행 하는 단일 쿼리는 `return View` 문.

각 정렬 순서에 대 한 다른 LINQ 문을 작성 하는 대신, LINQ 명령문을 동적으로 만들 수 있습니다. 동적 LINQ에 대 한 정보를 참조 하십시오. [동적 LINQ](https://go.microsoft.com/fwlink/?LinkID=323957)합니다.

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a>열 머리글을 학생 인덱스 보기에 대 한 하이퍼링크를 추가 합니다.

*Views\Student\Index.cshtml*, 대체 된 `<tr>` 및 `<th>` 강조 표시 된 코드와 함께 제목 행에 대 한 요소:

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

이 코드의 정보를 사용 하 여는 `ViewBag` 적절 한 쿼리 된 하이퍼링크를 설정 하는 속성 문자열 값입니다.

페이지를 실행 하 고 클릭는 **성** 및 **등록 날짜** 확인 해당 정렬 하려면 열 머리글 작동 합니다.

![Students_Index_page_with_sort_hyperlinks](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

클릭 한 후의 **성** 제목에서 학생 내림차순 마지막 이름 순서로 표시 됩니다.

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="add-a-search-box-to-the-students-index-page"></a>검색 상자 학생 인덱스 페이지에 추가

학생 인덱스 페이지에 필터링을 추가 하려면 추가 텍스트 상자 및 전송 단추가 보기로 및에 해당 변경는 `Index` 메서드. 입력란 이름 및 성 필드에서 검색할 문자열을 입력할 수 있습니다.

### <a name="add-filtering-functionality-to-the-index-method"></a>Index 메서드에 필터링 기능 추가

*Controllers\StudentController.cs*, 대체 된 `Index` 메서드를 다음 코드로 (변경 내용을 강조 표시):

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

사용자가 추가한는 `searchString` 매개 변수는 `Index` 메서드. 검색 문자열 값이 인덱스 뷰를 추가 하는 텍스트 상자가에서 수신 합니다. 또한 LINQ 명령문을 추가 했으므로 `where` 해당 이름 또는 성을 검색 문자열을 포함 하는 학생만을 선택 하는 절. 추가 하는 문에 [여기서](https://msdn.microsoft.com/en-us/library/bb535040.aspx) 절이 검색 하려면 값이 있는 경우에 실행 됩니다.

> [!NOTE]
> 대부분의 경우에서 Entity Framework 엔터티 집합 또는 메모리 내 컬렉션에 대 한 확장 메서드이기 같은 메서드를 호출할 수 있습니다. 결과 일반적으로 동일 하지만 경우에 따라 다를 수 있습니다.
> 
> 예를 들어의.NET Framework 구현은 `Contains` 메서드, 빈 문자열을 전달 있지만 Entity Framework provider for SQL Server Compact 4.0 빈 문자열에 대 한 행이 반환 하는 경우 모든 행을 반환 합니다. 따라서 예제의 코드 (배치는 `Where` 내 문을 `if` 문)는 모든 버전의 SQL Server에 대 한 동일한 결과 얻었는지 확인 합니다. 또한의.NET Framework 구현은 `Contains` 메서드는 기본적으로 대/소문자 구분 비교를 수행 하지만 엔터티 프레임 워크 SQL Server 공급자는 기본적으로 대/소문자 구분 비교를 수행 합니다. 따라서 호출는 `ToUpper` 테스트를 만들려면 명시적으로 대/소문자 구분 메서드를 사용 하면 결과가 반환 하는 저장소를 사용 하 여 나중에 코드를 변경할 때 변경 되지 않습니다는 `IEnumerable` 컬렉션 대신 한 `IQueryable` 개체입니다. (호출 하는 경우는 `Contains` 에서 메서드는 `IEnumerable` .NET Framework 구현은 가져올 컬렉션을; 호출 하는 경우 그에 `IQueryable` 개체, 데이터베이스 공급자 구현을 가져옵니다.)
> 
> Null 처리가 사용 하거나 다른 데이터베이스 공급자에 대 한 다른 수도 있습니다는 `IQueryable` 사용 하는 경우에 비해 개체는 `IEnumerable` 컬렉션입니다. 일부 시나리오에서는 예를 들어 한 `Where` 와 같은 조건 `table.Column != 0` 있는 열을 반환할 수 없습니다. `null` 값으로. 자세한 내용은 참조 ['where' 절에 변수를 null의 잘못 된 처리](https://data.uservoice.com/forums/72025-entity-framework-feature-suggestions/suggestions/1015361-incorrect-handling-of-null-variables-in-where-cl)합니다.


### <a name="add-a-search-box-to-the-student-index-view"></a>검색 상자 학생 인덱스 뷰를 추가

*Views\Student\Index.cshtml*, 열기 직전 강조 표시 된 코드를 추가 `table` 텍스트 상자 캡션을 만들기 위해 태그 및 **검색** 단추입니다.

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=5-10)]

페이지 실행 검색 문자열을 입력 하 고 클릭 **검색** 필터링 작동 하는지 확인 합니다.

![Students_Index_page_with_search_box](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

알림 URL "an" 검색 문자열을이 페이지에 책갈피 받지 않는 필터링된 된 목록을 책갈피를 사용 하는 경우 의미를 포함 하지 않습니다. 이에 적용 됩니다 열 정렬 링크 처럼 목록 전체를 정렬 합니다. 변경 합니다.는 **검색** 자습서의 뒷부분에 나오는 필터 조건에 대 한 쿼리 문자열을 사용 하는 단추입니다.

## <a name="add-paging-to-the-students-index-page"></a>페이징 학생 인덱스 페이지에 추가

페이징에 학생 인덱스 페이지를 추가 하려면 설치 하 여 시작 합니다는 **PagedList.Mvc** NuGet 패키지 합니다. 다음에 추가로 변경할 수는 `Index` 메서드 페이징 링크를 추가 하 고는 `Index` 보기. **PagedList.Mvc** 많은 좋은 페이징 및 ASP.NET MVC에 대 한 패키지 정렬 중 하나 이며 여기에서 사용 예를 들어, 다른 옵션과 것에 대 한 권장 아니라로 제공 됩니다. 다음은 페이징 파일에 대 한 링크입니다.

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

### <a name="install-the-pagedlistmvc-nuget-package"></a>PagedList.MVC NuGet 패키지 설치

NuGet **PagedList.Mvc** 패키지는 자동으로 설치 된 **PagedList** 종속성으로 패키지 합니다. **PagedList** 설치 패키지는 `PagedList` 컬렉션 형식 및 확장명 메서드를 `IQueryable` 및 `IEnumerable` 컬렉션입니다. 확장 메서드 만들기에 데이터의 단일 페이지는 `PagedList` 컬렉션 중 프로그램 `IQueryable` 또는 `IEnumerable`, 및 `PagedList` 컬렉션 여러 속성 및 페이징 용이 하 게 하는 메서드를 제공 합니다. **PagedList.Mvc** 패키지 페이징 단추를 표시 하는 페이징 도우미를 설치 합니다.

**도구** 메뉴 선택 **라이브러리 패키지 관리자** 차례로 **패키지 관리자 콘솔**합니다.

에 **패키지 관리자 콘솔** 창 있는지 확인는 **패키지 소스** 은 **nuget.org** 및 **기본 프로젝트** 는**ContosoUniversity**, 다음 명령을 입력 합니다.

`Install-Package PagedList.Mvc`

![PagedList.Mvc 설치](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

프로젝트를 빌드합니다. 

### <a name="add-paging-functionality-to-the-index-method"></a>인덱스 메서드에 페이징 기능을 추가 합니다.

*Controllers\StudentController.cs*, 추가 `using` 문에 `PagedList` 네임 스페이스:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

`Index` 메서드를 다음 코드로 바꿉니다.

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=1,3,7-16,41-43)]

이 코드는 추가 `page` 매개 변수, 현재 정렬 순서 매개 변수, 및 메서드 시그니처를 현재 필터 매개 변수:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

처음으로 페이지 표시 되거나, 사용자 하지 않은 한 페이징 또는 정렬 링크를 클릭 한 경우 모든 매개 변수가 null이 됩니다. 페이징 링크를 클릭 하는 경우는 `page` 변수에 표시할 페이지 번호를 포함 됩니다.

A `ViewBag` 속성은이 페이징 하는 동안 동일한 정렬 순서를 유지 하기 위해 페이징 파일에 대 한 링크에 포함 되어야 하기 때문에 현재 정렬 순서를 사용 하 여 뷰를 제공 합니다.

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

다른 속성 `ViewBag.CurrentFilter`, 현재 필터 문자열로 보기를 제공 합니다. 이 값, 페이징 하는 동안 필터 설정을 유지 하기 위해 페이징 링크에 포함 되어야 하며 페이지 다시 표시 하는 경우 텍스트 상자에 복원 해야 합니다. 검색 문자열 페이징 하는 동안 변경 되 면 표시할 다른 데이터를 새 필터 발생할 수 있기 때문 1로 다시 설정 되는 페이지에 있습니다. 검색 문자열 값이 텍스트 상자에 입력 하 고 전송 단추를 누를 때 변경 됩니다. 이 경우에 `searchString` 매개 변수는 null입니다.

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

메서드의 끝에는 `ToPagedList` 학생에 확장 메서드 `IQueryable` 개체 학생 페이징을 지원 되는 컬렉션 형식에는 단일 페이지로 학생 쿼리를 변환 합니다. 학생 들의 해당 단일 페이지 보기 전달 됩니다.

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

`ToPagedList` 메서드는 페이지 번호를 사용 합니다. 물음표는 두 개의 나타냅니다는 [null 병합 연산자](https://msdn.microsoft.com/en-us/library/ms173224.aspx)합니다. Null 병합 연산자는 null 허용 형식에 대 한 기본값을 정의 식 `(page ?? 1)` 의 값을 반환 하는 수단 `page` 값을 가진 또는 이면 1을 반환 하는 경우 `page` null입니다.

### <a name="add-paging-links-to-the-student-index-view"></a>학생 인덱스 뷰를 페이징 링크 추가

*Views\Student\Index.cshtml*, 기존 코드를 다음 코드로 바꿉니다. 변경 내용은 강조 표시 됩니다.

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=1-3,6,9,14,17,24,30,55-56,58-59)]

`@model` 페이지 맨 위에 있는 문은 보기 이제 가져옴을 지정는 `PagedList` 개체가 아니라는 `List` 개체입니다.

`using` 문을 `PagedList.Mvc` 페이징 단추에 대 한 MVC 도우미에 대 한 액세스를 제공 합니다.

코드의 오버 로드를 사용 하 여 [BeginForm](https://msdn.microsoft.com/en-us/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) 지정 하도록 허용 하는 [FormMethod.Get](https://msdn.microsoft.com/en-us/library/system.web.mvc.formmethod(v=vs.100).aspx/css)합니다.

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

기본 [BeginForm](https://msdn.microsoft.com/en-us/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) 매개 변수가 URL 아니라 HTTP 메시지 본문에 쿼리 문자열로 전달 하는 POST 사용 하 여 양식 데이터를 전송 합니다. HTTP GET을 지정 하면 양식 데이터 변수로 전달 됩니다 URL에 쿼리 문자열, URL에 책갈피를 있습니다. [HTTP GET 사용에 대 한 W3C 지침](http://www.w3.org/2001/tag/doc/whenToUseGet.html) 작업이 업데이트 되지 않습니다 때 GET 사용 해야 하는 것이 좋습니다.

입력란은 새 페이지를 클릭 하면 현재 검색 문자열을 볼 수 있도록 현재 검색 문자열으로 초기화 됩니다.

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml?highlight=1)]

열 머리글 링크 필터 결과 내에서 사용자를 정렬할 수 있도록 컨트롤러에 현재 검색 문자열을 전달 하는 쿼리 문자열을 사용 합니다.

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1)]

현재 페이지와 총 페이지 수가 표시 됩니다.

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]

표시 하는 페이지가 없는 경우 "0의 0 페이지"가 표시 됩니다. (페이지 번호는 페이지 수보다 큰 경우 때문에 `Model.PageNumber` 는 1, 및 `Model.PageCount` 은 0입니다.)

페이징 단추는 사용자가 `PagedListPager` 도우미:

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

`PagedListPager` 도우미는 다양 한 스타일 지정 및 Url을 포함 하 여 지정할 수 있는 옵션을 제공 합니다. 자세한 내용은 참조 [TroyGoode / PagedList](https://github.com/TroyGoode/PagedList) GitHub 사이트에서.

페이지를 실행 합니다.

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

페이징 작동 하는지 확인 하려면 서로 다른 정렬 순서에서 페이징 링크를 클릭 합니다. 검색 문자열을 입력 하 고 페이징 페이징도 제대로 작동 하는지 확인 된 정렬 및 필터링을 다시 시도 하십시오.

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

## <a name="create-an-about-page-that-shows-student-statistics"></a>만들기는 학생 통계를 보여 주는 페이지에 대 한

Contoso 대학 웹 사이트의 페이지에 대 한 개수 학생 각 등록 날짜에 대해 등록을 표시 합니다. 이 그룹에 그룹화 및 간단한 계산 해야합니다. 이렇게 하려면 다음을 수행 합니다.

- 보기를 전달 해야 하는 데이터에 대 한 보기 모델 클래스를 만듭니다.
- 수정 된 `About` 에서 메서드는 `Home` 컨트롤러입니다.
- 수정 된 `About` 보기.

### <a name="create-the-view-model"></a>뷰 모델 만들기

만들기는 *Viewmodel* 프로젝트 폴더의 폴더입니다. 해당 폴더에서 클래스 파일 추가 *EnrollmentDateGroup.cs* 템플릿 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a>Home 컨트롤러를 수정 합니다.

*HomeController.cs*, 다음 추가 `using` 문을 파일의 맨:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

여는 중괄호는 클래스에 대 한 후 즉시 데이터베이스 컨텍스트에 대 한 클래스 변수를 추가 합니다.

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

`About` 메서드를 다음 코드로 바꿉니다.

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

LINQ 명령문 학생 엔터티 등록 날짜별으로 그룹화 각 그룹에 있는 엔터티 수를 계산 하 고 컬렉션의 결과 저장할지 `EnrollmentDateGroup` 모델 개체를 보고 합니다.

추가 `Dispose` 메서드:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a>수정 된 보기에 대 한

코드는 *Views\Home\About.cshtml* 를 다음 코드로 파일:

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

응용 프로그램을 실행 하 고 클릭는 **에 대 한** 링크 합니다. 각 등록 날짜에 대 한 학생 수는 테이블에 표시 됩니다.

![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="summary"></a>요약

이 자습서에서는 데이터 모델을 만들고 기본 CRUD, 정렬, 필터링, 페이징 및 그룹화 기능을 구현 하는 방법을 살펴보았습니다. 다음 자습서에서는 데이터 모델을 확장 하 여 더 많은 고급 항목을 살펴보고 먼저 하겠습니다.

이 자습서를 연결 하는 방법 및 향상 될 수 있습니다에 의견을 남겨 주세요. 새 항목을 요청할 수도 있습니다 [Me 방법으로 코드 보기](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)합니다.

다른 Entity Framework 리소스에 대 한 링크에서 확인할 수 있습니다 [ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.

>[!div class="step-by-step"]
[이전](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
[다음](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)
