---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: "정렬, 필터링 및 (3 / 10) ASP.NET MVC 응용 프로그램에서 Entity Framework와 함께 페이징 | Microsoft Docs"
author: tdykstra
description: "Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/30/2013
ms.topic: article
ms.assetid: 8af630e0-fffa-4110-9eca-c96e201b2724
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: f9b68abeba19561a327bad5ee4be80d79af1a550
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application-3-of-10"></a>정렬, 필터링 및 (3 / 10) ASP.NET MVC 응용 프로그램에서 Entity Framework와 함께 페이징
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트를 다운로드 합니다.](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio 2012를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대 한 정보를 참조 하십시오. [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다. 시작 부분에서 자습서 시리즈를 시작할 수 있습니다 또는 [이 장의 대 한 시작 프로젝트 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 여기에서 시작 하 고 있습니다.
> 
> > [!NOTE] 
> > 
> > 해결할 수 없는 문제에 직면 하는 경우 [완료 장 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 문제를 재현 하려고 합니다. 일반적으로 코드 완성 된 코드를 비교 하 여 문제에 솔루션을 찾을 수 있습니다. 몇 가지 일반적인 오류 및 해결 하는 방법에 대 한 참조 [오류 및 해결 방법입니다.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)


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

메서드에서 사용 [LINQ to Entities](https://msdn.microsoft.com/library/bb386964.aspx) 기준으로 정렬 하려면 열을 지정 합니다. 코드를 만듭니다는 [IQueryable](https://msdn.microsoft.com/library/bb351562.aspx) 하기 전에 변수는 `switch` 문을 수정에 `switch` 문 및 호출은 `ToList` 후 메서드는 `switch` 문. 생성 및 수정할 `IQueryable` 변수 쿼리가 없는 데이터베이스에 전송 됩니다. 변환 될 때까지 쿼리가 실행 되지 않습니다는 `IQueryable` 개체와 같은 메서드를 호출 하 여 컬렉션에 `ToList`합니다. 따라서이 코드 발생 되어야 실행 하는 단일 쿼리는 `return View` 문.

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

사용자가 추가한는 `searchString` 매개 변수는 `Index` 메서드. 또한 LINQ 명령문을 추가 했으므로 `where` clausethat 해당 이름 또는 성을 검색 문자열을 포함 하는 학생만을 선택 합니다. 검색 문자열 값이 인덱스 뷰를 추가 하는 텍스트 상자가에서 수신 합니다. 추가 하는 문에 [여기서](https://msdn.microsoft.com/library/bb535040.aspx) 절이 검색 하려면 값이 있는 경우에 실행 됩니다.

> [!NOTE]
> 대부분의 경우에서 Entity Framework 엔터티 집합 또는 메모리 내 컬렉션에 대 한 확장 메서드이기 같은 메서드를 호출할 수 있습니다. 결과 일반적으로 동일 하지만 경우에 따라 다를 수 있습니다. 예를 들어의.NET Framework 구현은 `Contains` 메서드, 빈 문자열을 전달 있지만 Entity Framework provider for SQL Server Compact 4.0 빈 문자열에 대 한 행이 반환 하는 경우 모든 행을 반환 합니다. 따라서 예제의 코드 (배치는 `Where` 내 문을 `if` 문)는 모든 버전의 SQL Server에 대 한 동일한 결과 얻었는지 확인 합니다. 또한의.NET Framework 구현은 `Contains` 메서드는 기본적으로 대/소문자 구분 비교를 수행 하지만 엔터티 프레임 워크 SQL Server 공급자는 기본적으로 대/소문자 구분 비교를 수행 합니다. 따라서 호출는 `ToUpper` 테스트를 만들려면 명시적으로 대/소문자 구분 메서드를 사용 하면 결과가 반환 하는 저장소를 사용 하 여 나중에 코드를 변경할 때 변경 되지 않습니다는 `IEnumerable` 컬렉션 대신 한 `IQueryable` 개체입니다. (호출 하는 경우는 `Contains` 에서 메서드는 `IEnumerable` .NET Framework 구현은 가져올 컬렉션을; 호출 하는 경우 그에 `IQueryable` 개체, 데이터베이스 공급자 구현을 가져옵니다.)


### <a name="add-a-search-box-to-the-student-index-view"></a>검색 상자 학생 인덱스 뷰를 추가

*Views\Student\Index.cshtml*, 열기 직전 강조 표시 된 코드를 추가 `table` 텍스트 상자 캡션을 만들기 위해 태그 및 **검색** 단추입니다.

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=5-10)]

페이지 실행 검색 문자열을 입력 하 고 클릭 **검색** 필터링 작동 하는지 확인 합니다.

![Students_Index_page_with_search_box](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

알림 URL "an" 검색 문자열을이 페이지에 책갈피 받지 않는 필터링된 된 목록을 책갈피를 사용 하는 경우 의미를 포함 하지 않습니다. 변경 합니다.는 **검색** 자습서의 뒷부분에 나오는 필터 조건에 대 한 쿼리 문자열을 사용 하는 단추입니다.

## <a name="add-paging-to-the-students-index-page"></a>페이징 학생 인덱스 페이지에 추가

페이징에 학생 인덱스 페이지를 추가 하려면 설치 하 여 시작 합니다는 **PagedList.Mvc** NuGet 패키지 합니다. 다음에 추가로 변경할 수는 `Index` 메서드 페이징 링크를 추가 하 고는 `Index` 보기. **PagedList.Mvc** 많은 좋은 페이징 및 ASP.NET MVC에 대 한 패키지 정렬 중 하나 이며 여기에서 사용 예를 들어, 다른 옵션과 것에 대 한 권장 아니라로 제공 됩니다. 다음은 페이징 파일에 대 한 링크입니다.

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

### <a name="install-the-pagedlistmvc-nuget-package"></a>PagedList.MVC NuGet 패키지 설치

NuGet **PagedList.Mvc** 패키지는 자동으로 설치 된 **PagedList** 종속성으로 패키지 합니다. **PagedList** 설치 패키지는 `PagedList` 컬렉션 형식 및 확장명 메서드를 `IQueryable` 및 `IEnumerable` 컬렉션입니다. 확장 메서드 만들기에 데이터의 단일 페이지는 `PagedList` 컬렉션 중 프로그램 `IQueryable` 또는 `IEnumerable`, 및 `PagedList` 컬렉션 여러 속성 및 페이징 용이 하 게 하는 메서드를 제공 합니다. **PagedList.Mvc** 패키지 페이징 단추를 표시 하는 페이징 도우미를 설치 합니다.

**도구** 메뉴 선택 **라이브러리 패키지 관리자** 차례로 **솔루션에 대 한 NuGet 패키지 관리**합니다.

에 **NuGet 패키지 관리** 대화 상자를 클릭는 **온라인** 왼쪽 탭 한 다음 검색 상자에 "페이지"를 입력 합니다. 표시 되 면는 **PagedList.Mvc** 클릭, 패키지 **설치**합니다.

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

에 **프로젝트 선택** 상자 **확인**합니다.

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

### <a name="add-paging-functionality-to-the-index-method"></a>인덱스 메서드에 페이징 기능을 추가 합니다.

*Controllers\StudentController.cs*, 추가 `using` 문에 `PagedList` 네임 스페이스:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

`Index` 메서드를 다음 코드로 바꿉니다.

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

이 코드는 추가 `page` 매개 변수, 현재 정렬 순서 매개 변수, 및 메서드 서명을 다음과 같이 현재 필터 매개 변수:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

처음으로 페이지 표시 되거나, 사용자 하지 않은 한 페이징 또는 정렬 링크를 클릭 한 경우 모든 매개 변수가 null이 됩니다. 페이징 링크를 클릭 하는 경우는 `page` 변수에 표시할 페이지 번호를 포함 됩니다.

`A ViewBag`이 페이징 하는 동안 동일한 정렬 순서를 유지 하기 위해 페이징 파일에 대 한 링크에 포함 되어야 하기 때문에 현재 정렬 순서를 사용 하 여 뷰를 제공 하는 속성:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

다른 속성 `ViewBag.CurrentFilter`, 현재 필터 문자열로 보기를 제공 합니다. 이 값, 페이징 하는 동안 필터 설정을 유지 하기 위해 페이징 링크에 포함 되어야 하며 페이지 다시 표시 하는 경우 텍스트 상자에 복원 해야 합니다. 검색 문자열 페이징 하는 동안 변경 되 면 표시할 다른 데이터를 새 필터 발생할 수 있기 때문 1로 다시 설정 되는 페이지에 있습니다. 검색 문자열 값이 텍스트 상자에 입력 하 고 전송 단추를 누를 때 변경 됩니다. 이 경우에 `searchString` 매개 변수는 null입니다.

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

메서드의 끝에는 `ToPagedList` 학생에 확장 메서드 `IQueryable` 개체 학생 페이징을 지원 되는 컬렉션 형식에는 단일 페이지로 학생 쿼리를 변환 합니다. 학생 들의 해당 단일 페이지 보기 전달 됩니다.

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

`ToPagedList` 메서드는 페이지 번호를 사용 합니다. 물음표는 두 개의 나타냅니다는 [null 병합 연산자](https://msdn.microsoft.com/library/ms173224.aspx)합니다. Null 병합 연산자는 null 허용 형식에 대 한 기본값을 정의 식 `(page ?? 1)` 의 값을 반환 하는 수단 `page` 값을 가진 또는 이면 1을 반환 하는 경우 `page` null입니다.

### <a name="add-paging-links-to-the-student-index-view"></a>학생 인덱스 뷰를 페이징 링크 추가

*Views\Student\Index.cshtml*, 기존 코드를 다음 코드로 바꿉니다.

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=6,9,14-20,56-58)]

`@model` 페이지 맨 위에 있는 문은 보기 이제 가져옴을 지정는 `PagedList` 개체가 아니라는 `List` 개체입니다.

`using` 문을 `PagedList.Mvc` 페이징 단추에 대 한 MVC 도우미에 대 한 액세스를 제공 합니다.

코드의 오버 로드를 사용 하 여 [BeginForm](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) 지정 하도록 허용 하는 [FormMethod.Get](https://msdn.microsoft.com/library/system.web.mvc.formmethod(v=vs.100).aspx/css)합니다.

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

기본 [BeginForm](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx) 매개 변수가 URL 아니라 HTTP 메시지 본문에 쿼리 문자열로 전달 하는 POST 사용 하 여 양식 데이터를 전송 합니다. HTTP GET을 지정 하면 양식 데이터 변수로 전달 됩니다 URL에 쿼리 문자열, URL에 책갈피를 있습니다. [HTTP GET 사용에 대 한 W3C 지침](http://www.w3.org/2001/tag/doc/whenToUseGet.html) 작업이 업데이트 되지 않습니다는 경우 GET을 사용 하도록 지정 합니다.

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

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

페이징 작동 하는지 확인 하려면 서로 다른 정렬 순서에서 페이징 링크를 클릭 합니다. 검색 문자열을 입력 하 고 페이징 페이징도 제대로 작동 하는지 확인 된 정렬 및 필터링을 다시 시도 하십시오.

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="create-an-about-page-that-shows-student-statistics"></a>만들기는 학생 통계를 보여 주는 페이지에 대 한

Contoso 대학 웹 사이트의 페이지에 대 한 개수 학생 각 등록 날짜에 대해 등록을 표시 합니다. 이 그룹에 그룹화 및 간단한 계산 해야합니다. 이렇게 하려면 다음을 수행 합니다.

- 보기를 전달 해야 하는 데이터에 대 한 보기 모델 클래스를 만듭니다.
- 수정 된 `About` 에서 메서드는 `Home` 컨트롤러입니다.
- 수정 된 `About` 보기.

### <a name="create-the-view-model"></a>뷰 모델 만들기

만들기는 *Viewmodel* 폴더입니다. 해당 폴더에서 클래스 파일 추가 *EnrollmentDateGroup.cs* 기존 코드를 다음 코드로 바꿉니다.

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

![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

## <a name="optional-deploy-the-app-to-windows-azure"></a>선택 사항: Windows Azure에 응용 프로그램 배포

지금까지 응용 프로그램에 되었습니다에서 로컬로 실행 중 IIS Express에서 개발 컴퓨터. 인터넷을 통해 사용 하도록 다른 사용자가 사용할 수 있도록 하려면 웹 호스팅 공급자를 배포 해야 합니다. 에서는 자습서의이 선택적 섹션이 배포 합니다 것 Windows Azure 웹 사이트입니다.

### <a name="using-code-first-migrations-to-deploy-the-database"></a>Code First 마이그레이션을 사용 하 여 데이터베이스를 배포

데이터베이스를 배포 하는 Code First 마이그레이션을 사용 합니다. Visual Studio에서 배포에 대 한 설정을 구성 하는 데 사용할 수 있는 게시 프로필을 만들 때에 레이블이 있는 확인란을 선택 합니다 **실행 Code First 마이그레이션을 (응용 프로그램 시작 시 실행)**합니다. 이 설정을 사용 하면 배포 프로세스를 자동으로 응용 프로그램을 구성할 *Web.config* Code First 사용 하 여 있도록 대상 서버에서 파일의 `MigrateDatabaseToLatestVersion` 이니셜라이저 클래스입니다.

Visual Studio 배포 과정에서 데이터베이스를 사용 하 여 작업을 수행 하지 않습니다. 배포 응용 프로그램 배포 후 처음으로 데이터베이스에 액세스 하면 Code First 자동으로 데이터베이스를 만들거나 데이터베이스 스키마를 최신 버전으로 업데이트 합니다. 응용 프로그램에는 마이그레이션이 구현 하는 경우 `Seed` 메서드, 데이터베이스를 만들거나 스키마 업데이트 후의 메서드를 실행 합니다.

마이그레이션을 `Seed` 메서드 테스트 데이터를 삽입 합니다. 프로덕션 환경에 배포 하는 경우 변경 해야 합니다는 `Seed` 메서드 한다는 프로덕션 데이터베이스에 삽입할 수 있는 데이터를 삽입 합니다. 예를 들어, 현재 데이터 모델에서 실제 courses 하지만 가상의 학생 개발 데이터베이스에 대 한 수 있습니다. 작성할 수 있습니다는 `Seed` 메서드를 둘 다 개발에서 로드 하 고 다음 주석으로 처리 가상의 학생 프로덕션에 배포 하기 전에. 작성할 수 있습니다는 `Seed` 과정만 로드 하는 응용 프로그램의 UI를 사용 하 여 가상의 학생에 테스트 데이터베이스에 직접 입력 메서드입니다.

### <a name="get-a-windows-azure-account"></a>Windows Azure 계정 얻기

Windows Azure 계정이 필요 합니다. 아직 없는 하나, 몇 분에서에서 무료 평가판 계정을 만들 수 있습니다. 자세한 내용은 참조 [Windows Azure 무료 평가판](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)합니다.

### <a name="create-a-web-site-and-a-sql-database-in-windows-azure"></a>Windows Azure에서 웹 사이트 및 SQL 데이터베이스 만들기

Windows Azure 웹 사이트는 다른 Windows Azure 클라이언트와 공유 되는 가상 컴퓨터 (Vm)에서 실행 되는 공유 호스팅 환경에서 실행 됩니다. 공유 호스팅 환경 수 있는 방법이 저렴 한 비용 클라우드에서 시작 합니다. 이상 버전에서는 웹 트래픽 증가 하는 경우 응용 프로그램 전용된 Vm에서 실행 하 여 필요에 맞게 확장할 수 있습니다. 더 복잡 한 아키텍처를 해야 하는 경우 Windows Azure 클라우드 서비스를 마이그레이션할 수 있습니다. 클라우드 서비스 요구 사항에 따라 구성할 수 있는 전용된 Vm에서 실행 합니다.

Windows Azure SQL 데이터베이스는 SQL Server 기술을 기반으로 하는 클라우드 기반의 관계형 데이터베이스 서비스입니다. SQL 데이터베이스 도구와 SQL Server와 함께 작동 하는 응용 프로그램 에서도 작동 합니다.

1. 에 [Windows Azure 관리 포털](https://manage.windowsazure.com/), 클릭 **웹 사이트** 클릭 한 다음 확인 하 고 왼쪽된 탭에서 **새로**합니다.

    ![관리 포털에서 새로 만들기 단추](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image11.png)
2. 클릭 **사용자 지정 만들기**합니다.

    ![관리 포털에서 데이터베이스 링크를 사용 하 여 만들기](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image12.png)

 **사용자 지정 만들기-새 웹 사이트** 마법사가 열립니다.
3. 에 **새 웹 사이트** 단계 마법사에 문자열을 입력는 **URL** 상자 응용 프로그램에 대 한 고유 URL로 사용할 수 있습니다. 전체 URL 텍스트 상자 옆에 볼 수 있는 접미사 함께 내용을 여기에 입력으로 구성 됩니다. 그림에 나와 있는 "ConU" 하지만 해당 URL은 아마도 가져오므로 다른 선택 해야 합니다.

    ![관리 포털에서 데이터베이스 링크를 사용 하 여 만들기](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)
4. 에 **지역** 드롭 다운 목록에서 사용자의 인근 지역을 선택 합니다. 이 설정은 웹 사이트에서 실행 되는 데이터 센터를 지정 합니다.
5. 에 **데이터베이스** 드롭 다운 목록에서 선택 **무료 20MB SQL 데이터베이스 만들기**합니다.

    ![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)
6. 에 **DB 연결 문자열 이름**, 입력 *SchoolContext*합니다.

    ![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)
7. 오른쪽 상자의 맨 아래에 있는 화살표를 클릭 합니다. 마법사 열립니다는 **데이터베이스 설정** 단계입니다.
8. 에 **이름** 상자에 입력 *ContosoUniversityDB*합니다.
9. 에 **서버** 상자 **새 SQL 데이터베이스 서버**합니다. 또는 이전에 서버를 만든 경우 드롭다운 목록에서 해당 서버를 선택할 수 있습니다.
10. 관리자가 입력 **로그인 이름** 및 **암호**합니다. 선택한 경우 **새 SQL 데이터베이스 서버** 기존 이름 및 암호를 여기 입력 되지, 새 이름 및 데이터베이스에 액세스할 때 나중에 다시 사용할 이제 정의 하는 암호를 입력 합니다. 이전에 만든 서버를 선택한 경우에 해당 서버에 대 한 자격 증명을 입력 합니다. 이 자습서에 대 한 선택 되지 않습니다는 ***고급*** 확인란 합니다. ***고급*** 옵션을 사용 하면 데이터베이스를 설정 하려면 [데이터 정렬](https://msdn.microsoft.com/library/aa174903(v=SQL.80).aspx)합니다.
11. 지점과 같은 **지역** 웹 사이트에 대해 선택한 합니다.
12. 작업이 완료 되 나타내려면 상자의 오른쪽 맨 아래에 있는 확인 표시를 클릭 합니다.   
  
    ![데이터베이스 설정 단계 새 웹 사이트의-데이터베이스 마법사로 만들기](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image16.png)  

 다음 이미지는 기존 SQL Server 및 로그인을 사용 하 여 표시 합니다.   
  
    ![데이터베이스 설정 단계 새 웹 사이트의-데이터베이스 마법사로 만들기](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image17.png)  
  
 관리 포털 웹 사이트 페이지를 반환 및 **상태** 열 사이트가 생성 되 고 있음을 표시 합니다. 잠시 후 (일반적으로 보다 작음 1 분)는 **상태** 열 사이트를 만들었음을 표시 합니다. 왼쪽 탐색 모음에서 계정에 제공 하는 사이트 수 옆에 표시는 **웹 사이트** 아이콘과 데이터베이스 수가 옆에 표시 된 **SQL 데이터베이스** 아이콘입니다.

## <a name="deploy-the-application-to-windows-azure"></a>Windows Azure에 응용 프로그램 배포

1. Visual Studio에서 프로젝트를 마우스 오른쪽 단추로 클릭 **솔루션 탐색기** 선택 **게시** 상황에 맞는 메뉴입니다.  
  
    ![프로젝트 상황에 맞는 메뉴에서 게시](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image18.png)
2. 에 **프로필** 탭은 **웹 게시** 마법사를 클릭 하 여 **가져오기**합니다.  
  
    ![게시 설정 가져오기](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image19.png)
3. Visual Studio에서 Windows Azure 구독을 이전에 추가 하지 않은 경우 다음 단계를 수행 합니다. 다음이 단계에서 추가한 구독 드롭 다운 목록에서 있도록 **Windows Azure 웹 사이트에서 가져오기** 웹 사이트가 포함 됩니다.

    a. 에 **게시 프로필 가져오기** 대화 상자를 클릭 **Windows Azure 웹 사이트에서 가져오기**, 클릭 하 고 **추가 Windows Azure 구독**합니다.

    ![Windows Azure 구독 추가](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image20.png)

    b. 에 **Windows Azure 구독 가져오기** 대화 상자를 클릭 **구독 파일을 다운로드**합니다.

    ![구독 파일을 다운로드 합니다.](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image21.png)

    c. 브라우저 창에서 저장 된 *.publishsettings* 파일입니다.

    ![.publishsettings 파일을 다운로드](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image22.png)

    > [!WARNING]
    > 보안-는 *publishsettings* 자격 증명 (인코딩되지 않음) Windows Azure 구독 및 서비스를 관리 하는 데 사용 되는 파일에 포함 되어 있습니다. 원본 디렉터리 외부에 임시로 저장 하는이 파일에 대 한 보안 모범 사례 (예를 들어는 *Libraries\Documents* 폴더), 한 다음 가져오기가 완료 되 면 삭제 합니다. 에 액세스할 수 있는 악의적인 사용자는 `.publishsettings` 파일 수 편집, 생성 및 Windows Azure 서비스를 삭제 합니다.

    d. 에 **Windows Azure 구독 가져오기** 대화 상자를 클릭 **찾아보기** 로 이동 하 고는 *.publishsettings* 파일입니다.

    ![sub 다운로드](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image23.png)

    e. **가져오기**를 클릭합니다.

    ![import](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image24.png)
4. 에 **게시 프로필 가져오기** 대화 상자에서 **Windows Azure 웹 사이트에서 가져오기**, 드롭 다운 목록에서 웹 사이트를 선택 하 고 클릭 **확인**합니다.  
  
    ![게시 프로필 가져오기](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image25.png)
5. 에 **연결** 탭을 클릭 **연결 유효성 검사** 를 설정이 정확한 지 확인 합니다.  
  
    ![연결 확인](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image26.png)
6. 연결 검증 된 녹색 확인 표시가 옆에 표시 되는 **연결 유효성 검사** 단추입니다. **다음**을 클릭합니다.  
  
    ![성공적으로 유효성이 검사 된 연결](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image27.png)
7. 열기는 **원격 연결 문자열** 드롭 다운 목록에서 **SchoolContext** 만든 데이터베이스에 대 한 연결 문자열을 선택 합니다.
8. 선택 **실행 Code First 마이그레이션을 (응용 프로그램 시작 시 실행)**합니다.
9. 선택을 취소 **런타임에이 연결 문자열을 사용 하 여** 에 대 한는 **UserContext (DefaultConnection)**이 응용 프로그램은 멤버 자격 데이터베이스를 사용 하지 않아야 하므로 합니다.   
  
    ![설정 탭](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image28.png)
10. **다음**을 클릭합니다.
11. 에 **미리 보기** 탭을 클릭 **미리 보기 시작**합니다.  
  
    ![미리 보기 탭에서 미리 단추](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image29.png)  
  
 탭에는 서버에 복사 되는 파일의 목록이 표시 됩니다. 미리 보기를 표시할 응용 프로그램을 게시 하 필요 하지 않지만 알아두어야 하는 유용한 기능을 합니다. 이 경우 표시 되는 파일의 목록으로 아무 작업도 수행할 필요가 없습니다. 이 응용 프로그램을 배포한 다음에이 목록에 변경 된 파일만 됩니다.  
  
    ![미리 파일 출력](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image30.png)
12. **게시**를 클릭합니다.  
 Visual Studio는 Windows Azure 서버에 파일을 복사 프로세스를 시작 합니다.
13. **출력** 창 수행 된 배포 작업을 표시 및 배포를 성공적으로 완료를 보고 합니다.  
  
    ![성공적인 배포를 보고 하는 출력 창](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image31.png)
14. 배포가 성공 하면 기본 브라우저가 자동으로 배포 된 웹 사이트의 URL로 열립니다.  
 만든 응용 프로그램은 클라우드에서 실행 됩니다. 학생 탭을 클릭 합니다.  
  
    ![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image32.png)

이 시점에서 프로그램 *SchoolContext* 데이터베이스 선택 했기 때문에 Windows Azure SQL 데이터베이스에 생성 되었음을 **실행 Code First 마이그레이션을 (응용 프로그램 시작 시 실행)**합니다. *Web.config* 배포 된 웹 사이트의 파일이 변경 되어 있도록는 [MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) 이니셜라이저 코드에서 읽거나 데이터베이스에 데이터를 쓸 처음으로 실행 됩니다 ( 발생 한 선택한 경우에 **학생** 탭):

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image33.png)

배포 프로세스에도 새 연결 문자열을 생성 *(SchoolContext\_의 DatabasePublish*) 데이터베이스 스키마를 업데이트 하 고 시드 데이터베이스에 사용할 Code First 마이그레이션에 대 한 합니다.

![Database_Publish 연결 문자열](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image34.png)

*DefaultConnection* (함이 자습서에서 사용 하지) 멤버 자격 데이터베이스에 대 한 연결 문자열은입니다. *SchoolContext* ContosoUniversity 데이터베이스에 대 한 연결 문자열은입니다.

배포 된 버전에서 자신의 컴퓨터에서 Web.config 파일을 찾을 수 있습니다 *ContosoUniversity\obj\Release\Package\PackageTmp\Web.config*합니다. 가 배포에 액세스할 수 있습니다 *Web.config* FTP를 사용 하 여 자체 파일입니다. 자세한 내용은 [Visual Studio를 사용 하 여 ASP.NET 웹 배포: 코드 업데이트 배포](../../../../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md)합니다. 로 시작 하는 지침에 따라 "FTP 도구를 사용 하려면 다음 세 가지: FTP URL, 사용자 이름 및 암호."

> [!NOTE]
> 웹 앱 URL을 검색 하는 모든 사람이 데이터를 변경할 수 보안을 구현 하지 않습니다. 웹 사이트를 보호 하는 방법에 지침은 [Windows Azure 웹 사이트 멤버 자격, OAuth, SQL 데이터베이스와 보안 ASP.NET MVC 응용 프로그램 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다. 중이거나 다른 사용자가 Windows Azure 관리 포털을 사용 하 여 사이트를 사용 하 여 또는 **서버 탐색기** 사이트를 중지 하려면 Visual Studio에서 합니다.


![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image35.png)

## <a name="code-first-initializers"></a>코드의 첫 번째 이니셜라이저

배포 섹션에서 언급 했 듯이 [MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) 이니셜라이저를 사용 하 고 있습니다. 먼저 또한 제공 등을 사용할 수 있는 다른 이니셜라이저 [CreateDatabaseIfNotExists](https://msdn.microsoft.com/library/gg679221(v=vs.103).aspx) (기본값) 이면 [DropCreateDatabaseIfModelChanges](https://msdn.microsoft.com/library/gg679604(v=VS.103).aspx) 및 [ DropCreateDatabaseAlways](https://msdn.microsoft.com/library/gg679506(v=VS.103).aspx)합니다. `DropCreateAlways` 이니셜라이저는 단위 테스트에 대 한 조건을 설정 하는 데 유용할 수 있습니다. 사용자 고유의 이니셜라이저를 작성할 수 있습니다 및 응용 프로그램에서 읽거나 데이터베이스에 기록 될 때까지 대기 하지 않을 경우 이니셜라이저를 명시적으로 호출할 수 있습니다. 책의 6 장 참조에 대 한 이니셜라이저는 포괄적인 설명은 [프로그래밍 Entity Framework: Code First](http://shop.oreilly.com/product/0636920022220.do) Julie Lerman 및 Rowan Miller 합니다.

## <a name="summary"></a>요약

이 자습서에서는 데이터 모델을 만들고 기본 CRUD, 정렬, 필터링, 페이징 및 그룹화 기능을 구현 하는 방법을 살펴보았습니다. 다음 자습서에서는 데이터 모델을 확장 하 여 더 많은 고급 항목을 살펴보고 먼저 하겠습니다.

다른 Entity Framework 리소스에 대 한 링크에서 확인할 수 있습니다는 [ASP.NET 데이터 액세스 콘텐츠 맵](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.

>[!div class="step-by-step"]
[이전](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
[다음](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
