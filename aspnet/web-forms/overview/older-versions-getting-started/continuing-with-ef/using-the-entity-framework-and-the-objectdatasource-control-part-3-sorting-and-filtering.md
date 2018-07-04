---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
title: '3 부 Entity Framework 4.0 및 ObjectDataSource 컨트롤 사용: 정렬 및 필터링 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈의 Entity Framework 4.0 자습서 시리즈를 사용 하 여 시작 하 여 만든 Contoso University 웹 응용 프로그램 기반으로 합니다. 필자는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/26/2011
ms.topic: article
ms.assetid: 2990bd10-590d-43d5-9529-6b503ce5455d
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
msc.type: authoredcontent
ms.openlocfilehash: 48d859191877ba951e233f19873d52625fe180ac
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37378912"
---
<a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-3-sorting-and-filtering"></a>3 부 Entity Framework 4.0 및 ObjectDataSource 컨트롤 사용: 정렬 및 필터링
====================
[Tom Dykstra](https://github.com/tdykstra)

> 이 자습서 시리즈에서 만든 Contoso University 웹 응용 프로그램 빌드를 [Entity Framework 4.0을 사용 하 여 시작](https://asp.net/entity-framework/tutorials#Getting%20Started) 자습서 시리즈입니다. 이전 자습서를 완료 하지 않은 경우이 자습서에 대 한 시작 지점으로 할 수 있습니다 [응용 프로그램을 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) 만들어졌을 것입니다. 할 수도 있습니다 [응용 프로그램을 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) 전체 자습서 시리즈에서 만들어집니다. 이 자습서에 대 한 질문이 있으면 하기를 게시할 수 있습니다 합니다 [ASP.NET Entity Framework 포럼](https://forums.asp.net/1227.aspx)합니다.


이전 자습서에서 Entity Framework를 사용 하는 n 계층 웹 응용 프로그램에서 리포지토리 패턴을 구현 하 고 `ObjectDataSource` 제어 합니다. 이 자습서에서는 정렬 및 필터링을 수행 하 여 마스터-세부 시나리오를 처리 하는 방법을 보여 줍니다. 다음과 같은 향상 된 기능을 추가 합니다 *Departments.aspx* 페이지:

- 입력란을 이름으로 부서를 선택할 수 있도록 합니다.
- 목록 표에 표시 되는 각 부서에 대 한 과정입니다.
- 열 머리글을 클릭 하 여 정렬할 수 있습니다.

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)

## <a name="adding-the-ability-to-sort-gridview-columns"></a>GridView 열 정렬 하는 기능을 추가합니다.

엽니다는 *Departments.aspx* 페이지 및 추가 `SortParameterName="sortExpression"` 특성을 `ObjectDataSource` 라는 컨트롤 `DepartmentsObjectDataSource`합니다. (만들어 나중에 `GetDepartments` 라는 매개 변수를 갖는 메서드의 `sortExpression`.) 컨트롤의 여는 태그에 대 한 태그에는 이제 다음 예제와 유사합니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample1.aspx)]

추가 된 `AllowSorting="true"` 특성을 여는 태그를 `GridView` 컨트롤입니다. 컨트롤의 여는 태그에 대 한 태그에는 이제 다음 예제와 유사합니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample2.aspx)]

*Departments.aspx.cs*를 호출 하 여 기본 정렬 순서를 설정 합니다 `GridView` 컨트롤의 `Sort` 메서드에서 `Page_Load` 메서드:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample3.cs)]

비즈니스 논리 클래스 또는 해당 리포지토리 클래스를 정렬 하거나 필터링 하는 코드를 추가할 수 있습니다. 비즈니스 논리 클래스에서 수행 하는 경우 정렬 또는 필터링 작업은 데이터베이스에서 데이터를 검색 한 후 있기 때문에 가능는 비즈니스 논리 클래스가 사용 되는 `IEnumerable` 저장소에서 반환 된 개체입니다. 정렬 및 필터링 리포지토리 클래스의 코드를 추가 하 고 그렇게 하는 LINQ 식 앞 또는 개체 쿼리 변환 된 경우는 `IEnumerable` 개체, 일반적으로 더 효율적인 처리를 위해 데이터베이스에 명령을 전달 됩니다. 이 자습서에서는 정렬 및 데이터베이스에서 완료 해야 하는 처리를 발생 시키는 방식으로 필터링를 구현 하-즉, 리포지토리에 있습니다.

정렬 기능을 추가 하 고 리포지토리 인터페이스는 비즈니스 논리 클래스에 대 한 리포지토리 클래스를도 새 메서드를 추가 해야 합니다. 에 *ISchoolRepository.cs* 파일에서 새 `GetDepartments` 메서드를는 `sortExpression` 반환 되는 부서 목록을 정렬 하는 데 사용할 수 있는 매개 변수:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample4.cs)]

`sortExpression` 매개 변수 열을 기준으로 정렬 및 정렬 방향을 지정 합니다.

새 메서드를 위한 코드를 추가 합니다 *SchoolRepository.cs* 파일:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample5.cs)]

매개 변수가 없는 기존 변경 `GetDepartments` 새 메서드를 호출 하는 방법.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample6.cs)]

테스트 프로젝트에서 다음 새 메서드를 추가 합니다 *MockSchoolRepository.cs*:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample7.cs)]

정렬 된 목록을 반환 합니다.이 메서드를 종속 되어 있는 모든 단위 테스트를 만드는 것을 사용 하는 경우에 반환 하기 전에 목록을 정렬 합니다. 않습니다 만드시겠습니까 테스트는이 자습서에서는 메서드 수 정렬 되지 않은 부서 목록을 반환 하므로 합니다.

에 *SchoolBL.cs* 파일에서 다음 새 메서드는 비즈니스 논리 클래스를 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample8.cs)]

이 코드는 리포지토리 메서드로 정렬 매개 변수를 전달합니다.

실행 합니다 *Departments.aspx* 페이지입니다.

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)

이제 해당 열으로 정렬 하려면 열 머리글을 클릭 수 있습니다. 열이 이미 정렬 하는 경우 제목을 클릭 하는 정렬 방향을 반대로 바꿉니다.

## <a name="adding-a-search-box"></a>검색 상자 추가

이 섹션의 검색 텍스트 상자 추가, 연결할 수는 `ObjectDataSource` 제어 매개 변수를 사용 하 여 제어 하 고 필터링을 지원 하도록 비즈니스 논리 클래스에 메서드를 추가 합니다.

엽니다는 *Departments.aspx* 첫 번째 머리글 사이 다음 태그를 추가한 페이지 `ObjectDataSource` 컨트롤:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample9.aspx)]

`ObjectDataSource` 라는 컨트롤 `DepartmentsObjectDataSource`, 다음을 수행 합니다.

- 추가 `SelectParameters` 라는 매개 변수 요소 `nameSearchString` 에 입력 된 값을 가져옵니다는 `SearchTextBox` 제어 합니다.
- 변경 된 `SelectMethod` 특성 값을 `GetDepartmentsByName`입니다. (나중에 만들이 메서드가 있습니다.)

에 대 한 태그는 `ObjectDataSource` 컨트롤에는 이제 다음 예제와 유사 합니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample10.aspx)]

*ISchoolRepository.cs*, 추가 된 `GetDepartmentsByName` 둘 다 사용 하는 메서드 `sortExpression` 및 `nameSearchString` 매개 변수:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample11.cs)]

*SchoolRepository.cs*, 다음 새 메서드를 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample12.cs)]

이 코드에 사용 된 `Where` 검색 문자열이 포함 된 항목을 선택 하는 방법입니다. 검색 문자열이 비어 있으면 모든 레코드 선택 됩니다. 메서드를 다음과 같이 하나의 문에서 함께 호출을 지정 하는 경우 사용자에 게 유의 (`Include`, 한 다음 `OrderBy`, 다음 `Where`), `Where` 메서드 항상 마지막 이어야 합니다.

기존 변경 `GetDepartments` 사용 하는 메서드를 `sortExpression` 새 메서드를 호출 하는 매개 변수:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample13.cs)]

*MockSchoolRepository.cs* 테스트 프로젝트에서 다음 새 메서드를 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample14.cs)]

*SchoolBL.cs*, 다음 새 메서드를 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample15.cs)]

실행 합니다 *Departments.aspx* 페이지 및 선택 논리 작동 하는지 확인 하려면 검색 문자열을 입력 합니다. 텍스트 상자를 비워 두고 모든 레코드가 반환 되도록 검색을 시도해 보세요.

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)

## <a name="adding-a-details-column-for-each-grid-row"></a>각 그리드 행에 대 한 세부 정보 열을 추가합니다.

다음으로, 모든 그리드의 오른쪽 셀에 표시 되는 각 부서에 대 한 강의 참조 하려고 합니다. 이 위해 사용 하 여 중첩 된 `GridView` 컨트롤과 databind 데이터로 하는 `Courses` 의 탐색 속성을 `Department` 엔터티.

열기 *Departments.aspx* 및 태그에는 `GridView` 컨트롤을 처리기를 지정에 대 한는 `RowDataBound` 이벤트입니다. 컨트롤의 여는 태그에 대 한 태그에는 이제 다음 예제와 유사합니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample16.aspx)]

새 `TemplateField` 요소 뒤의 `Administrator` 템플릿 필드:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample17.aspx)]

이 태그는 중첩 된 만듭니다 `GridView` 강좌 번호 및 제목 목록은 과정을 보여주는 컨트롤입니다. Databind 해야 하기 때문에 데이터 소스를 지정 하지에서 코드에는 `RowDataBound` 처리기입니다.

오픈 *Departments.aspx.cs* 에 대 한 다음 처리기를 추가 하 고는 `RowDataBound` 이벤트:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample18.cs)]

이 코드는 `Department` 이벤트 인수에서 엔터티 변환 합니다 `Courses` 탐색 속성을를 `List` 컬렉션 및 중첩 된 계열을 `GridView` 컬렉션에.

열기는 *SchoolRepository.cs* 파일과 대해 즉시 로드를 지정 합니다 `Courses` 호출 하 여 탐색 속성을 `Include` 에서 만든 개체 쿼리에서 메서드를 `GetDepartmentsByName` 메서드. 합니다 `return` 문에서 `GetDepartmentsByName` 메서드에는 이제 다음 예제와 유사 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample19.cs)]

페이지를 실행 합니다. 정렬 및 필터링 위에서 추가한 기능을 하는 것 외에도 GridView 컨트롤은 이제 각 부서에 대 한 중첩 된 강좌 세부 정보 표시 됩니다.

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)

정렬, 필터링 및 마스터-세부 시나리오에 대 한 소개를 완료 합니다. 다음 자습서에서는 동시성을 처리 하는 방법을 배웁니다.

> [!div class="step-by-step"]
> [이전](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
> [다음](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)
