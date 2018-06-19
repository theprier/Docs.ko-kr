---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
title: 'Entity Framework 4.0 및 ObjectDataSource 컨트롤을 사용 하 여 단계 3: 정렬 및 필터링 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈의 Entity Framework 4.0 자습서 시리즈 시작 하기에 의해 만들어진 Contoso 대학 웹 응용 프로그램 기반으로 합니다. I 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/26/2011
ms.topic: article
ms.assetid: 2990bd10-590d-43d5-9529-6b503ce5455d
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
msc.type: authoredcontent
ms.openlocfilehash: e412d3ad98a37931e7190a4909cb09fa2abfb3d0
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30887657"
---
<a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-3-sorting-and-filtering"></a>Entity Framework 4.0 및 ObjectDataSource 컨트롤을 사용 하 여 단계 3: 정렬 및 필터링
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

> 에 의해 만들어진 Contoso 대학 웹 응용 프로그램을 기반으로 하는이 자습서 시리즈의 [Entity Framework 4.0이 있는 시작](https://asp.net/entity-framework/tutorials#Getting%20Started) 자습서 시리즈 합니다. 이전 자습서를 완료 하지 않은 경우이 자습서에 대 한 시작 점으로 하면 [응용 프로그램을 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) 만들어졌을 것입니다. 수도 있습니다 [응용 프로그램을 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) 완료 하는 자습서 시리즈에서 만들어진 합니다. 이 자습서에 대 한 질문이 있으면에 게시할 수 있습니다는 [ASP.NET Entity Framework 포럼](https://forums.asp.net/1227.aspx)합니다.


Entity Framework를 사용 하는 n 계층 웹 응용 프로그램에서 리포지토리 패턴을 구현 하기 이전 자습서에서 및 `ObjectDataSource` 제어 합니다. 이 자습서에서는 정렬 및 필터링을 수행 하 고 마스터-세부 정보 시나리오를 처리 하는 방법을 보여 줍니다. 다음과 같은 향상 기능이 추가 된 *Departments.aspx* 페이지:

- 부서 이름으로 선택할 수 있도록 하려면 텍스트 상자입니다.
- 눈금에 표시 되는 각 부서에 대 한 교육 과정의 목록.
- 열 머리글을 클릭 하 여 정렬할 수 있습니다.

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)

## <a name="adding-the-ability-to-sort-gridview-columns"></a>GridView 열을 정렬 하는 기능을 추가합니다.

열기는 *Departments.aspx* 페이지 및 추가 `SortParameterName="sortExpression"` 특성을 `ObjectDataSource` 라는 컨트롤 `DepartmentsObjectDataSource`합니다. (만들어 나중에 `GetDepartments` 라는 매개 변수를 갖는 메서드의 `sortExpression`.) 컨트롤의 여는 태그에 대 한 태그에는 이제 다음 예제와 유사 합니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample1.aspx)]

추가 `AllowSorting="true"` 특성을 여는 태그는 `GridView` 제어 합니다. 컨트롤의 여는 태그에 대 한 태그에는 이제 다음 예제와 유사 합니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample2.aspx)]

*Departments.aspx.cs*를 호출 하 여 기본 정렬 순서를 설정의 `GridView` 컨트롤의 `Sort` 에서 메서드는 `Page_Load` 메서드:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample3.cs)]

비즈니스 논리 클래스 또는 저장소 클래스 중 하나에서 정렬 또는 필터 하는 코드를 추가할 수 있습니다. 비즈니스 논리 클래스에서 하면 정렬 또는 필터링 작업 수행 됩니다, 데이터베이스에서 데이터를 검색 후 비즈니스 논리 클래스 사용 하기 때문에 프로그램 `IEnumerable` 저장소에서 반환 된 개체입니다. 정렬 및 필터링 저장소 클래스의 코드를 추가 LINQ 식 앞 그렇게 또는 개체 쿼리 변환 된 경우는 `IEnumerable` 개체는 일반적으로 보다 효율적 처리를 위해 데이터베이스에 명령을 전달 됩니다. 이 자습서에서는 데이터베이스에서 수행 해야 하는 처리 하는 방법으로에서 정렬 및 필터링을 구현 합니다-즉, 저장소에 있습니다.

정렬 기능을 추가 하려면 리포지토리 인터페이스와 비즈니스 논리 클래스에 대 한 저장소 클래스를 에서도에 새 메서드를 추가 해야 합니다. 에 *ISchoolRepository.cs* 파일, 새 추가 `GetDepartments` 를 받는 메서드에 `sortExpression` 반환 되는 부서 목록을 정렬 하는 데 사용할 매개 변수:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample4.cs)]

`sortExpression` 매개 변수에서 정렬할 열과 정렬 방향을 지정 합니다.

새로운 메서드를 위한 코드를 추가 *SchoolRepository.cs* 파일:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample5.cs)]

매개 변수가 없는 기존 변경 `GetDepartments` 새 메서드를 호출 하는 메서드:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample6.cs)]

테스트 프로젝트에서 다음과 같은 새로운 메서드를 추가 *MockSchoolRepository.cs*:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample7.cs)]

이 메서드는 정렬 된 목록 반환에 의존 하는 모든 단위 테스트를 만드는 하려던 목록을 반환 하기 전에 정렬 해야 합니다. 않습니다 만드시겠습니까 테스트 그렇게이 자습서에서는 메서드가 정렬 되지 않은 부서 목록을 반환할 수 있도록 합니다.

에 *SchoolBL.cs* 파일, 비즈니스 논리 클래스에 다음과 같은 새 메서드 추가:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample8.cs)]

이 코드는 저장소 메서드를 정렬 매개 변수를 전달합니다.

실행 된 *Departments.aspx* 페이지.

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)

해당 열으로 정렬 하려면 열 머리글을 클릭할 수 있습니다. 열이 이미 정렬, 머리글을 클릭 하면 정렬 방향을 취소 됩니다.

## <a name="adding-a-search-box"></a>검색 상자를 추가합니다.

이 섹션의 검색 텍스트 상자를 추가, 연결 합니다는 `ObjectDataSource` 제어 매개 변수를 사용 하 여 제어 하 고 필터링을 지원 하려면 비즈니스 논리 클래스는 메서드를 추가 합니다.

열기는 *Departments.aspx* 페이지 머리글 및 첫 번째 사이 다음 태그를 추가 하 고 `ObjectDataSource` 제어:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample9.aspx)]

에 `ObjectDataSource` 라는 컨트롤 `DepartmentsObjectDataSource`에서 다음을 수행 합니다.

- 추가 `SelectParameters` 매개 변수 이름에 대 한 요소 `nameSearchString` 를 가져옴에 입력 된 값은 `SearchTextBox` 제어 합니다.
- 변경 된 `SelectMethod` 특성 값을 `GetDepartmentsByName`합니다. (나중에 만들이 이렇게 합니다.)

에 대 한 태그는 `ObjectDataSource` 컨트롤에는 이제 다음 예제와 유사 합니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample10.aspx)]

*ISchoolRepository.cs*, 추가 `GetDepartmentsByName` 메서드 둘 다 사용 `sortExpression` 및 `nameSearchString` 매개 변수:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample11.cs)]

*SchoolRepository.cs*, 다음 새 메서드 추가:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample12.cs)]

사용 하 여이 코드는 `Where` 메서드 검색 문자열이 포함 된 항목을 선택 합니다. 검색 문자열이 비어 있으면 모든 레코드는 선택 됩니다. 메서드를 다음과 같이 하나의 문에서 함께 호출을 지정 하는 경우 유의 (`Include`, 다음 `OrderBy`, 다음 `Where`), `Where` 메서드가 항상 마지막 이어야 합니다.

기존 변경 `GetDepartments` 를 받는 메서드에 `sortExpression` 새 메서드를 호출 하는 매개 변수:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample13.cs)]

*MockSchoolRepository.cs* 테스트 프로젝트에서 다음과 같은 새 메서드를 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample14.cs)]

*SchoolBL.cs*, 다음 새 메서드 추가:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample15.cs)]

실행 된 *Departments.aspx* 페이지 하 고 선택 논리 작동 하는지 확인 하는 검색 문자열을 입력 합니다. 텍스트 상자를 비워 두고 모든 레코드가 반환 되도록 검색을 시도 합니다.

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)

## <a name="adding-a-details-column-for-each-grid-row"></a>각 그리드 행에 대 한 세부 정보 열을 추가합니다.

다음으로 눈금의 오른쪽 셀에 표시 되는 각 부서에 대 한 교육 과정의 모든 참조 하려고 합니다. 이 작업을 수행 하려면 중첩 된 사용 합니다 `GridView` 컨트롤과 databind에서 데이터에는 `Courses` 의 탐색 속성은 `Department` 엔터티.

열기 *Departments.aspx* 및에 대 한 태그는 `GridView` 제어 처리기를 지정에 대 한는 `RowDataBound` 이벤트입니다. 컨트롤의 여는 태그에 대 한 태그에는 이제 다음 예제와 유사 합니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample16.aspx)]

새로 추가 `TemplateField` 요소 뒤의 `Administrator` 템플릿 필드:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample17.aspx)]

이 태그는 중첩 된 만듭니다 `GridView` 과정 번호 및 courses 목록 제목 표시 하는 컨트롤입니다. Databind 것 때문에 데이터 소스를 지정 하지의 코드에는 `RowDataBound` 처리기입니다.

열기 *Departments.aspx.cs* 에 대 한 다음 처리기를 추가 하 고는 `RowDataBound` 이벤트:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample18.cs)]

이 코드는 `Department` 이벤트 인수에서 엔터티를 변환는 `Courses` 탐색 속성을는 `List` 컬렉션 및 중첩 된 데이터 바인딩합니다 `GridView` 컬렉션에 있습니다.

열기는 *SchoolRepository.cs* 파일을 즉시 로드에 대 한 지정는 `Courses` 호출 하 여 탐색 속성은 `Include` 에서 만드는 개체 쿼리에 대 한 메서드는 `GetDepartmentsByName` 메서드. `return` 의 문에서 `GetDepartmentsByName` 메서드에는 이제 다음 예제와 유사 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample19.cs)]

페이지를 실행 합니다. 정렬 및 필터링 이전에 추가한 기능을 실행 하는 것 외에도 GridView 컨트롤 이제 각 부서에 대 한 중첩된 강좌 세부 정보를 표시 합니다.

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)

이로써 정렬, 필터링, 및 마스터-세부 정보 시나리오를 소개 합니다. 다음 자습서에서는 동시성을 처리 하는 방법을 볼 수 있습니다.

> [!div class="step-by-step"]
> [이전](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
> [다음](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)
