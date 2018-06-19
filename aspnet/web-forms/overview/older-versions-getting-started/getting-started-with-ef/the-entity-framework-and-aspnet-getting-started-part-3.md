---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-3
title: 먼저 Entity Framework 4.0 데이터베이스와 시작 및 ASP.NET 4 Web Forms-3 부 | Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 샘플 응용 프로그램은...
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/03/2010
ms.topic: article
ms.assetid: ccdc3f8c-2568-40a7-8f8b-3c23d2e05388
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-3
msc.type: authoredcontent
ms.openlocfilehash: 654f3556af5d05ec186e1811421966bbaffd2e21
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30889256"
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-3"></a>먼저 Entity Framework 4.0 데이터베이스와 시작 및 ASP.NET 4 Web Forms-3 부
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

> Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 4.0 및 Visual Studio 2010을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대 한 정보를 참조 하세요. [시리즈의 첫 번째 자습서](the-entity-framework-and-aspnet-getting-started-part-1.md)


## <a name="filtering-ordering-and-grouping-data"></a>필터링, 정렬 및 데이터 그룹화

이전 자습서에서 사용 되는 `EntityDataSource` 컨트롤 표시 하 고 데이터를 편집 합니다. 이 자습서에서는 필터링, 순서, 및 데이터를 그룹화 합니다. 작업을 수행 하면이 속성을 설정 하 여는 `EntityDataSource` 컨트롤 구문이 다른 데이터 소스 컨트롤에서 달라 집니다. 그러나 알 수 있듯이 있습니다 사용할 수는 `QueryExtender` 컨트롤을 이러한 차이 최소화 합니다.

변경 합니다.는 *Students.aspx* 학생을 필터링 할 페이지 이름과 이름에 대 한 검색으로 정렬 합니다. 또한 변경는 *Courses.aspx* courses 선택한 부서 및 과정에 대 한 검색에 대 한 이름으로 표시 하려면 페이지를 합니다. 학생 통계를 마지막으로 추가 된 *About.aspx* 페이지.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-3/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image1.png)

[![Image11](the-entity-framework-and-aspnet-getting-started-part-3/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image3.png)

[![Image10](the-entity-framework-and-aspnet-getting-started-part-3/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image5.png)

[![Image14](the-entity-framework-and-aspnet-getting-started-part-3/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image7.png)

## <a name="using-the-entitydatasource-where-property-to-filter-data"></a>EntityDataSource "Where" 필터링 할 속성 데이터를 사용 하 여

열기는 *Students.aspx* 이전 자습서에서 만든 페이지입니다. 현재 구성 된 `GridView` 페이지에서 컨트롤에서 모든 이름을 표시는 `People` 엔터티 집합입니다. 그러나 학생 들만 표시 하려면 선택 하 여 찾을 수 있는 `Person` null이 아닌 등록 날짜가 포함 된 엔터티.

로 전환 **디자인** 표시 하 고 선택 된 `EntityDataSource` 제어 합니다. 에 **속성** 창에서 설정 된 `Where` 속성을 `it.EnrollmentDate is not null`합니다.

[![Image01](the-entity-framework-and-aspnet-getting-started-part-3/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image9.png)

사용 하는 구문은 `Where` 의 속성은 `EntityDataSource` 컨트롤 Entity SQL은 합니다. Entity SQL Transact SQL 유사 하지만 데이터베이스 개체를 사용 하지 않고 엔터티를 사용 하기 위해 사용자 지정 된 합니다. 식에서 `it.EnrollmentDate is not null`, 단어 `it` 쿼리에서 반환 된 엔터티에 대 한 참조를 나타냅니다. 따라서 `it.EnrollmentDate` 참조 하는 `EnrollmentDate` 의 속성은 `Person` 엔터티 하는 `EntityDataSource` 반환을 제어 합니다.

페이지를 실행 합니다. 학생 목록에는 이제 학생 들만 포함 됩니다. (여기서 표시 된 행이 없는 등록 날짜가 없습니다.)

[![Image02](the-entity-framework-and-aspnet-getting-started-part-3/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image11.png)

## <a name="using-the-entitydatasource-orderby-property-to-order-data"></a>EntityDataSource "y" 속성 주문 데이터를 사용 하 여

처음 표시 된 이름 순서에 포함 되도록이 목록을 사용할 수 있습니다. 와 *Students.aspx* 열려 있는 상태에서 페이지 **디자인** 보기와는 `EntityDataSource` 선택 되어 있는 상태에서 제어는 **속성** 창 집합은  **OrderBy** 속성을 `it.LastName`합니다.

[![Image05](the-entity-framework-and-aspnet-getting-started-part-3/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image13.png)

페이지를 실행 합니다. 학생 목록 성 기준으로 순서에 포함 되었습니다.

[![Image04](the-entity-framework-and-aspnet-getting-started-part-3/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image15.png)

## <a name="using-a-control-parameter-to-set-the-where-property"></a>제어 매개 변수를 사용 하 여 "Where" 속성을 설정 하려면

처럼 다른 데이터 소스 컨트롤과 매개 변수 값을 전달할 수 있습니다는 `Where` 속성입니다. 에 *Courses.aspx* 페이지 자습서의 2 단계에서 만든, 연결 된 부서는 사용자가 드롭다운 목록에서 선택 하는 과정을 표시 하려면이 메서드를 사용할 수 있습니다.

열기 *Courses.aspx* 전환할 **디자인** 보기. 두 번째 추가 `EntityDataSource` 페이지와 제어 하 고 이름을 `CoursesEntityDataSource`합니다. 에 연결 하는 `SchoolEntities` 모델을 마우스 선택 `Courses` 로 **EntitySetName** 값입니다.

에 **속성** 창에서 줄임표를 클릭는 **여기서** 속성 상자입니다. (있는지 확인은 `CoursesEntityDataSource` 컨트롤을 사용 하기 전에 선택 여전히는 **속성** 창입니다.)

[![Image06](the-entity-framework-and-aspnet-getting-started-part-3/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image17.png)

**식 편집기** 대화 상자가 표시 됩니다. 이 대화 상자에서 선택 **Where를 자동으로 생성 식은 제공된 된 매개 변수 기반**, 클릭 하 고 **매개 변수 추가**합니다. 매개 변수 이름을 `DepartmentID`선택, **제어** 로 **매개 변수 소스** 값을 선택 **DepartmentsDropDownList** 로 **ControlID**  값입니다.

[![Image07](the-entity-framework-and-aspnet-getting-started-part-3/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image19.png)

클릭 **고급 속성 표시**, 및는 **속성** 의 창은 **식 편집기** 대화 상자에서 변경 된 `Type` 속성을 `Int32`합니다.

[![Image15](the-entity-framework-and-aspnet-getting-started-part-3/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image21.png)

완료 되 면 클릭 **확인**합니다.

드롭다운 목록 아래 추가 `GridView` 페이지를 제어 하 고 이름을 `CoursesGridView`합니다. 에 연결 하는 `CoursesEntityDataSource` 데이터 소스 제어, 클릭 **스키마 새로 고침**, 클릭 **열 편집**, 제거 하 고는 `DepartmentID` 열입니다. `GridView` 컨트롤 태그에는 다음 예제와 유사 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample1.aspx)]

드롭다운 목록에서 선택 된 부서를 변경할 때 자동으로 변경 하려면 연결된 과정의 목록을 원하는 합니다. 드롭다운 목록을 선택 합니다. 이렇게 하려면 및의 **속성** 창 집합은 `AutoPostBack` 속성을 `True`합니다.

[![Image08](the-entity-framework-and-aspnet-getting-started-part-3/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image23.png)

전환 디자이너를 사용 하 여 작업을 완료 했으므로 **소스** 보기 및 대체는 `ConnectionString` 및 `DefaultContainer` 속성의 이름은 `CoursesEntityDataSource` 보호로 `ContextTypeName="ContosoUniversity.DAL.SchoolEntities"` 특성입니다. 완료 되 면 컨트롤에 대 한 태그는 다음 예제에서는 같습니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample2.aspx)]

페이지를 실행 하 고 드롭다운 목록을 사용 하 여 다른 부서를 선택 합니다. 에 선택한 부서에서 제공 되는 과정에만 표시 되는 `GridView` 제어 합니다.

[![Image09](the-entity-framework-and-aspnet-getting-started-part-3/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image25.png)

## <a name="using-the-entitydatasource-groupby-property-to-group-data"></a>데이터를 그룹화 EntityDataSource "GroupBy" 속성을 사용 하 여

에 대 한 해당 페이지에 몇 가지 학생 본문 통계를 저장 하려면 Contoso 대학이 가정해 봅니다. 특히, 등록은 날짜별 학생 수에 대 한 분석을 표시 하도록 하려고 합니다.

열기 *About.aspx*, 및 **소스** 보기의 기존 내용을 대체는 `BodyContent` 사이 "학생 본문 통계"로 제어 `h2` 태그:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample3.aspx)]

제목 추가 `EntityDataSource` 제어 하 고 이름을 `StudentStatisticsEntityDataSource`합니다. 에 연결 `SchoolEntities`선택는 `People` 엔터티 집합과 둡니다는 **선택** 상자에 변경 하지 않고 마법사. 다음 속성을 설정는 **속성** 창:

- 학생 들만을 필터링 하려면 설정는 `Where` 속성을 `it.EnrollmentDate is not null`합니다.
- 등록 날짜 기준으로 결과 그룹화 하려면 설정는 `GroupBy` 속성을 `it.EnrollmentDate`합니다.
- 등록 날짜와 학생 수를 선택 하려면 설정는 `Select` 속성을 `it.EnrollmentDate, Count(it.EnrollmentDate) AS NumberOfStudents`합니다.
- 등록 날짜 기준으로 결과 정렬 하려면 설정는 `OrderBy` 속성을 `it.EnrollmentDate`합니다.

**소스** 보기, 대체는 `ConnectionString` 및 `DefaultContainer` 이름을 사용 하 여 속성을 `ContextTypeName` 속성입니다. `EntityDataSource` 컨트롤 태그에는 이제 다음 예제와 유사 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample4.aspx)]

구문은 `Select`, `GroupBy`, 및 `Where` 속성에 대 한 제외 하 고 TRANSACT-SQL과 비슷한는 `it` 현재 엔터티를 지정 하는 키워드입니다.

만들려면 다음 태그를 추가 `GridView` 컨트롤에 데이터를 표시 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample5.aspx)]

등록 날짜 여 학생 수를 보여 주는 목록을 보려면 페이지를 실행 합니다.

[![Image10](the-entity-framework-and-aspnet-getting-started-part-3/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image27.png)

## <a name="using-the-queryextender-control-for-filtering-and-ordering"></a>QueryExtender 컨트롤을 사용 하 여 필터링 및 정렬

`QueryExtender` 컨트롤은 필터링 및 정렬 태그에 지정 하는 방법을 제공 합니다. 구문은 사용 중인 데이터베이스 관리 시스템 (DBMS)와 무관 합니다. Entity Framework에 대 한 탐색 속성에 대 한 사용 구문 고유함 예외와 함께 Entity Framework의 일반적으로 독립 이기도 합니다.

이 자습서의이 부분에서는 `QueryExtender` 컨트롤을 데이터에 필터 문과 order 한 order by 필드 중 하나는 탐색 속성 포함 됩니다.

(태그 대신 코드를 사용 하 여 자동으로 생성 되는 쿼리를 확장 하는 경우는 `EntityDataSource` 제어를 수행할 수 있습니다 하 처리는 `QueryCreated` 이벤트입니다. 이것은 방법을 `QueryExtender` 확장 `EntityDataSource` 쿼리도 제어 합니다.)

열기는 *Courses.aspx* 페이지와 이전에 추가한 태그 아래는 제목을 입력 된 검색 문자열을 검색 단추에 대 한 텍스트 상자 만들 다음 태그를 삽입 및 `EntityDataSource` 는 에바인딩되는컨트롤`Courses` 엔터티 집합입니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample6.aspx)]

에 `EntityDataSource` 컨트롤의 `Include` 속성이 `Department`합니다. 데이터베이스에는 `Course` 테이블 부서 이름을 포함 하지 않으며 포함 한 `DepartmentID` 외래 키 열입니다. 가입 해야 데이터베이스를 직접 과정 데이터와 함께 부서 이름을 가져올 수를 쿼리 된 경우는 `Course` 및 `Department` 테이블입니다. 설정 하 여는 `Include` 속성을 `Department`, Entity Framework 관련 가져오기 작업을 수행 해야 한다는 지정 `Department` 도달할 때 엔터티는 `Course` 엔터티. `Department` 엔터티에 저장 됩니다는 `Department` 의 탐색 속성은 `Course` 엔터티. (기본적으로는 `SchoolEntities` 필요 하므로 해당 클래스에 포함 된 데이터 소스 컨트롤을 바인딩한 때 데이터 모델 디자이너에서 생성 된 클래스에 관련된 데이터를 검색 된 `Include` 속성은 필요 하지 않습니다. 그러나 설정 하면 성능이 향상 페이지의 수 없는 경우 Entity Framework는 확인에 대 한 데이터를 검색 하는 데이터베이스에 대 한 호출을 구분 하기 때문에 `Course` 엔터티 및 관련 된 `Department` 엔터티.)

후의 `EntityDataSource` 방금 컨트롤을 만든를 만들려면 다음 태그를 삽입 하는 한 `QueryExtender` 하에 바인딩되는 컨트롤 `EntityDataSource` 제어 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample7.aspx)]

`SearchExpression` 요소 제목에 해당 어구가 텍스트 상자에 입력 된 값과 일치 하는 과정을 선택 하려면 지정 합니다. 텍스트 상자에 입력 하는 수 만큼의 문자 때문에 비교할 수 만큼만 `SearchType` 속성 지정 `StartsWith`합니다.

`OrderByExpression` 요소 지정 결과 집합은 부서 이름 내 과정 제목별으로 정렬 됩니다. 부서 이름 지정 방법을 확인: `Department.Name`합니다. 때문에 간의 연결은 `Course` 엔터티 및 `Department` 엔터티는 일대일는 `Department` 탐색 속성을 포함 한 `Department` 엔터티. (대 다 관계에 것일 경우 속성은에 포함 컬렉션.) 부서 이름을 가져오려면 지정 해야 합니다는 `Name` 의 속성은 `Department` 엔터티.

마지막으로 추가 된 `GridView` 과정의 목록을 표시 하도록 컨트롤:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample8.aspx)]

첫 번째 열은 부서 이름을 표시 하는 서식 파일 필드입니다. 데이터 바인딩 식을 지정 `Department.Name`에서 본 것 처럼,는 `QueryExtender` 제어 합니다.

페이지를 실행 합니다. 초기 표시 부서와 과정 제목 순서로 모든 과정의 목록을 보여 줍니다.

[![Image11](the-entity-framework-and-aspnet-getting-started-part-3/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image29.png)

"M"을 입력 하 고 클릭 **검색** 제목에 해당 어구가 "m" (검색은 하지 대/소문자 구분)으로 시작 하는 모든 과정을 볼 수 있습니다.

[![Image12](the-entity-framework-and-aspnet-getting-started-part-3/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image31.png)

## <a name="using-the-like-operator-to-filter-data"></a>"좋아요" 연산자를 사용 하 여 데이터를 필터링 하려면

비슷한 효과 얻을 수 있습니다는 `QueryExtender` 컨트롤의 `StartsWith`, `Contains`, 및 `EndsWith` 형식을 사용 하 여 검색 한 `Like` 연산자에는 `EntityDataSource` 컨트롤의 `Where` 속성입니다. 자습서의이 부분에 사용 하는 방법을 표시 됩니다는 `Like` 학생에 대 한 이름으로 검색 하려면 연산자입니다.

열기 *Students.aspx* 에 **소스** 보기. 이후에 `GridView` 컨트롤에 다음 태그를 추가 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample9.aspx)]

이 태그를 제외 하 고 이전 보았을 무엇 비슷합니다는 `Where` 속성 값입니다. 두 번째 부분에서 `Where` 부분 문자열 검색을 정의 하는 식 (`LIKE %FirstMidName% or LIKE %LastName%`) 텍스트 상자에 입력 항목에 대 한 첫 번째 및 마지막 이름이 모두 검색 하 합니다.

페이지를 실행 합니다. 처음에 일부 표시 들의 기본 값을 포함 하기 때문에 `StudentName` 매개 변수는 "%"입니다.

[![Image13](the-entity-framework-and-aspnet-getting-started-part-3/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image33.png)

텍스트 상자에 "g" 문자를 입력 하 고 클릭 **검색**합니다. 이름이 "g" 중 하나에서 첫 번째 또는 마지막 학생의 목록을 표시 합니다.

[![Image14](the-entity-framework-and-aspnet-getting-started-part-3/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image35.png)

이제 표시, 업데이트, 필터링, 정렬 되었으며 개별 테이블의에서 데이터를 그룹화 합니다. 다음 자습서에서 관련된 데이터 (마스터-세부 시나리오)와 함께 작동 하도록 되기 시작 합니다.

> [!div class="step-by-step"]
> [이전](the-entity-framework-and-aspnet-getting-started-part-2.md)
> [다음](the-entity-framework-and-aspnet-getting-started-part-4.md)
