---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-3
title: 먼저 Entity Framework 4.0 Database를 사용 하 여 시작 및 ASP.NET 4 Web Forms-3 부 | Microsoft Docs
author: tdykstra
description: Contoso University 샘플 웹 응용 프로그램에는 Entity Framework를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 샘플 응용 프로그램은...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: ccdc3f8c-2568-40a7-8f8b-3c23d2e05388
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-3
msc.type: authoredcontent
ms.openlocfilehash: 162f93c0249d8fa11d67ea10c68bc2ca8bae7259
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41823831"
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-3"></a>먼저 Entity Framework 4.0 Database를 사용 하 여 시작 및 ASP.NET 4 Web Forms-3 부
====================
[Tom Dykstra](https://github.com/tdykstra)

> Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 4.0 및 Visual Studio 2010을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대 한 정보를 참조 하세요. [시리즈의 첫 번째 자습서](the-entity-framework-and-aspnet-getting-started-part-1.md)


## <a name="filtering-ordering-and-grouping-data"></a>필터링, 정렬 및 데이터를 그룹화 합니다.

이전 자습서에서 사용한는 `EntityDataSource` 컨트롤을 표시 하 고 데이터를 편집 합니다. 이 자습서에서는 필터링, 순서 및 데이터를 그룹화 됩니다. 이렇게 하면 속성을 설정 하 여는 `EntityDataSource` 제어 구문은 다른 다른 데이터 소스 컨트롤입니다. 하지만 알 수 있듯이 사용할 수는 `QueryExtender` 이러한 차이 최소화 하는 컨트롤입니다.

변경 합니다 *Students.aspx* 학생을 필터링 할 페이지 이름과 이름을 검색 하 여 정렬 합니다. 또한 변경 합니다 *Courses.aspx* 강의 표시 하려면 선택한 부서 및 강좌에 대 한 검색에 대 한 이름으로 페이지입니다. 학생 통계를 마지막으로 추가 합니다 *About.aspx* 페이지입니다.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-3/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image1.png)

[![Image11](the-entity-framework-and-aspnet-getting-started-part-3/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image3.png)

[![Image10](the-entity-framework-and-aspnet-getting-started-part-3/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image5.png)

[![Image14](the-entity-framework-and-aspnet-getting-started-part-3/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image7.png)

## <a name="using-the-entitydatasource-where-property-to-filter-data"></a>EntityDataSource "Where" 필터링 할 속성 데이터를 사용 하 여

엽니다는 *Students.aspx* 이전 자습서에서 만든 페이지입니다. 현재 구성 합니다 `GridView` 페이지에서 컨트롤에서 모든 이름을 표시는 `People` 엔터티 집합입니다. 그러나 학생 들만을 표시 하려면 선택 하 여 찾을 수 있는 `Person` null이 아닌 등록 날짜를가지고 있는 엔터티.

전환할 **디자인** 표시 하 고 선택 된 `EntityDataSource` 컨트롤입니다. 에 **속성** 창에서 설정 합니다 `Where` 속성을 `it.EnrollmentDate is not null`합니다.

[![Image01](the-entity-framework-and-aspnet-getting-started-part-3/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image9.png)

사용 하는 구문을 `Where` 의 속성을 `EntityDataSource` 컨트롤은 Entity SQL입니다. Entity SQL TRANSACT-SQL 유사 하지만 데이터베이스 개체가 아니라 엔터티 사용에 대 한 사용자 지정 됩니다. 식에 `it.EnrollmentDate is not null`, 단어 `it` 쿼리에서 반환 된 엔터티에 대 한 참조를 나타냅니다. 따라서 `it.EnrollmentDate` 가리킵니다를 `EnrollmentDate` 의 속성을 `Person` 엔터티는는 `EntityDataSource` 반환을 제어 합니다.

페이지를 실행 합니다. 이제 학생 목록에는 학생 들만 포함 되어 있습니다. (여기서 표시 행이 없는 날짜는 없습니다 등록 합니다.)

[![Image02](the-entity-framework-and-aspnet-getting-started-part-3/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image11.png)

## <a name="using-the-entitydatasource-orderby-property-to-order-data"></a>EntityDataSource "OrderBy" 속성을 주문 데이터를 사용 하 여

처음 표시할 때 이름 순서로 되어이 목록을 수도 있습니다. 사용 하 여는 *Students.aspx* 페이지에 열려 **디자인** 보기와는 `EntityDataSource` 컨트롤을 계속 선택한에 **속성** 창 집합은  **OrderBy** 속성을 `it.LastName`입니다.

[![Image05](the-entity-framework-and-aspnet-getting-started-part-3/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image13.png)

페이지를 실행 합니다. 학생 목록 마지막 이름별으로 정렬 됩니다.

[![Image04](the-entity-framework-and-aspnet-getting-started-part-3/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image15.png)

## <a name="using-a-control-parameter-to-set-the-where-property"></a>컨트롤 매개 변수를 사용 하 여 "Where" 속성을 설정 하려면

다른 데이터 소스 컨트롤을 사용 하 여 매개 변수 값을 전달할 수 있습니다 하는 대로 `Where` 속성입니다. 에 *Courses.aspx* 페이지 자습서의 2 부에서 만든에 사용자가 드롭다운 목록에서 선택한 부서와 관련 된 강의 표시 하려면이 메서드를 사용할 수 있습니다.

오픈 *Courses.aspx* 으로 전환 **디자인** 보기. 두 번째 추가 `EntityDataSource` 페이지에서 제어 하 고 이름을 `CoursesEntityDataSource`입니다. 연결 된 `SchoolEntities` 모델을 선택한 `Courses` 으로 **EntitySetName** 값.

에 **속성** 창에서 줄임표를 클릭 합니다 **여기서** 속성 상자. (있는지 확인 합니다 `CoursesEntityDataSource` 컨트롤을 사용 하기 전에 선택 계속 합니다 **속성** 창입니다.)

[![Image06](the-entity-framework-and-aspnet-getting-started-part-3/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image17.png)

합니다 **식 편집기** 대화 상자가 표시 됩니다. 이 대화 상자에서 선택 **Where를 자동으로 생성 제공 된 매개 변수를 기반으로 식**를 클릭 하 고 **매개 변수 추가**합니다. 매개 변수에 `DepartmentID`을 선택 **제어** 으로 **매개 변수 원본** 값을 선택 **DepartmentsDropDownList** 으로 **ControlID**  값입니다.

[![Image07](the-entity-framework-and-aspnet-getting-started-part-3/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image19.png)

클릭 **고급 속성 표시**, 및는 **속성** 기간을 **식 편집기** 대화 상자에서 변경 합니다 `Type` 속성을 `Int32`.

[![Image15](the-entity-framework-and-aspnet-getting-started-part-3/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image21.png)

완료 되 면 **확인**합니다.

드롭다운 목록 아래에서 추가 `GridView` 페이지를 제어 하 고 이름을 `CoursesGridView`입니다. 연결 합니다 `CoursesEntityDataSource` 데이터 소스 컨트롤을 클릭 **스키마 새로 고침**, 클릭 **열 편집**, 및 제거는 `DepartmentID` 열. `GridView` 컨트롤 태그에는 다음 예제와 유사 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample1.aspx)]

사용자 드롭다운 목록에서 선택한 부서를 변경 하는 경우 자동으로 변경 하려면 연결 된 강좌의 목록을 원할입니다. 이렇게 드롭다운 목록을 선택 하 고는 **속성** 창 집합 합니다 `AutoPostBack` 속성을 `True`합니다.

[![Image08](the-entity-framework-and-aspnet-getting-started-part-3/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image23.png)

디자이너를 사용 하 여 작업을 완료 했으므로 전환할 **원본** 바꾸고 보기는 `ConnectionString` 및 `DefaultContainer` 속성의 이름을 합니다 `CoursesEntityDataSource` 컨트롤를 `ContextTypeName="ContosoUniversity.DAL.SchoolEntities"` 특성. 완료 되 면 다음 예제와 같이 컨트롤에 대 한 태그를 살펴보겠습니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample2.aspx)]

페이지를 실행 하 고 드롭 다운 목록을 사용 하 여 다른 부서를 선택 합니다. 선택한 학과에서 제공 하는 과정만 표시 됩니다는 `GridView` 제어 합니다.

[![Image09](the-entity-framework-and-aspnet-getting-started-part-3/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image25.png)

## <a name="using-the-entitydatasource-groupby-property-to-group-data"></a>EntityDataSource "GroupBy" 속성을 그룹 데이터를 사용 하 여

Contoso University에 대 한 페이지에서 일부 본문 학생 통계를 배치 하려고 한다고 가정 합니다. 특히 이러한 등록 날짜별으로 학생 수의 분석 결과 표시 하려고 합니다.

열기 *About.aspx*, 및 **원본** 보기에서의 기존 내용을 대체 합니다 `BodyContent` 간에 "학생 본문 통계"를 사용 하 여 제어 `h2` 태그:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample3.aspx)]

머리글 뒤에 추가 된 `EntityDataSource` 제어 하 고 이름을 `StudentStatisticsEntityDataSource`입니다. 연결 `SchoolEntities`를 선택 합니다 `People` 엔터티 집합과 유지를 **선택** 변경 하지 않고 마법사에서 상자입니다. 다음 속성을 설정 합니다 **속성** 창:

- 학생용만 필터를 설정 합니다 `Where` 속성을 `it.EnrollmentDate is not null`입니다.
- 등록 날짜별으로 결과 그룹화 하려면 설정 합니다 `GroupBy` 속성을 `it.EnrollmentDate`입니다.
- 등록 날짜 및 학생 수를 선택 하려면 설정 합니다 `Select` 속성을 `it.EnrollmentDate, Count(it.EnrollmentDate) AS NumberOfStudents`입니다.
- 등록 날짜별으로 결과 순서를 설정 합니다 `OrderBy` 속성을 `it.EnrollmentDate`입니다.

**소스** 보기에서 대체 합니다 `ConnectionString` 및 `DefaultContainer` 사용 하 여 속성 이름을 `ContextTypeName` 속성. `EntityDataSource` 컨트롤 태그에는 이제 다음 예제와 유사 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample4.aspx)]

구문의 합니다 `Select`, `GroupBy`, 및 `Where` 속성에는 제외 하 고 TRANSACT-SQL과 비슷한는 `it` 현재 엔터티를 지정 하는 키워드입니다.

만들기 위해 다음 태그가 추가 `GridView` 데이터를 표시 하는 컨트롤입니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample5.aspx)]

등록 날짜별으로 학생 수를 보여 주는 목록을 보려면 페이지를 실행 합니다.

[![Image10](the-entity-framework-and-aspnet-getting-started-part-3/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image27.png)

## <a name="using-the-queryextender-control-for-filtering-and-ordering"></a>QueryExtender 컨트롤을 사용 하 여 필터링 및 정렬

`QueryExtender` 컨트롤 태그의 필터링 및 정렬 지정 하는 방법을 제공 합니다. 구문을 사용 하는 데이터베이스 관리 시스템 (DBMS)와 무관 합니다. 탐색 속성에 대해 사용 하는 구문 Entity Framework를 고유 하 게 예외를 사용 하 여 Entity Framework에서 일반적으로 무관 이기도 합니다.

이 자습서의이 부분에서는 `QueryExtender` 필터 및 주문 데이터를 제어 한 order by 필드 중 하나는 탐색 속성 포함 됩니다.

(태그 대신 코드를 사용 하 여 자동으로 생성 되는 쿼리를 확장 하려는 경우는 `EntityDataSource` 컨트롤을 이렇게 할 수 있습니다 하 여 처리를 `QueryCreated` 이벤트입니다. 이 방법을 `QueryExtender` 컨트롤 `EntityDataSource` 쿼리도 제어 합니다.)

엽니다는 *Courses.aspx* 페이지 및 이전에 추가한 태그, 아래 제목을 검색 단추를 사용 하는 검색 문자열 입력에 대 한 텍스트 상자를 만들려면 다음 태그를 삽입 및 `EntityDataSource` 합니다 바인딩되는컨트롤`Courses` 엔터티 집합입니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample6.aspx)]

에 `EntityDataSource` 컨트롤의 `Include` 속성이 `Department`합니다. 데이터베이스에는 `Course` 테이블에 부서 이름이 없습니다; 있기를 `DepartmentID` 외래 키 열입니다. 데이터베이스를 직접 쿼리 된 하려는 과정 데이터와 함께 부서 이름을 가져올 수 있다면 조인 하는 `Course` 및 `Department` 테이블입니다. 설정 하 여 합니다 `Include` 속성을 `Department`, Entity Framework 가져오는 관련 작업을 수행 해야 하는 것이 지정할 `Department` 도달 하면 엔터티를 `Course` 엔터티. `Department` 엔터티에 저장 되는 `Department` 의 탐색 속성은 `Course` 엔터티. (기본적으로 `SchoolEntities` 필요할 때 설정 되므로 해당 클래스를 데이터 소스 컨트롤에 연결 했습니다 데이터 모델 디자이너에서 생성 된 클래스에 관련된 데이터를 검색 합니다 `Include` 속성은 필요 하지 않습니다. 그러나 설정 하면 성능이 향상 됩니다 페이지의 Entity Framework는 확인에 대 한 데이터를 검색 하는 데이터베이스에 대 한 호출을 구분 합니다 `Course` 엔터티 및 관련 `Department` 엔터티.)

후 합니다 `EntityDataSource` 방금 컨트롤 만들기 위해 다음 태그가 삽입 만들어지면를 `QueryExtender` 는 바인딩되는 컨트롤 `EntityDataSource` 컨트롤입니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample7.aspx)]

`SearchExpression` 제목에 해당 어구가 텍스트 상자에 입력 한 값과 일치 하는 과정을 선택 하려는 요소를 지정 합니다. 텍스트 상자에을 입력 하는 만큼의 문자가 있으므로 비교할 수 만큼만 합니다 `SearchType` 속성을 지정 `StartsWith`합니다.

`OrderByExpression` 과정 제목 부서 이름으로 결과 집합을 정렬할 요소를 지정 합니다. 부서 이름을 지정 하는 방법을 확인할 수 있습니다: `Department.Name`합니다. 때문에 간의 연결을 `Course` 엔터티 및 `Department` 엔터티가 일를 `Department` 탐색 속성이 포함를 `Department` 엔터티. (-다 관계의 경우 속성은 컬렉션을 포함 합니다.) 부서 이름을 가져오려면를 지정 해야 합니다 `Name` 의 속성을 `Department` 엔터티.

마지막으로 추가 된 `GridView` 강좌의 목록을 표시 하도록 컨트롤:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample8.aspx)]

첫 번째 열에는 부서 이름을 표시 하는 템플릿 필드입니다. 데이터 바인딩 식을 지정 `Department.Name`에서 볼 수 있듯이 마찬가지로 `QueryExtender` 제어 합니다.

페이지를 실행 합니다. 처음 표시 된 부서와 과정 제목으로 순서 대로 모든 강좌의 목록을 보여 줍니다.

[![Image11](the-entity-framework-and-aspnet-getting-started-part-3/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image29.png)

"M"을 입력 하 고 클릭 **검색** 제목에 해당 어구가 "m" (검색은 하지 소문자)로 시작 하는 모든 과정을 확인 합니다.

[![Image12](the-entity-framework-and-aspnet-getting-started-part-3/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image31.png)

## <a name="using-the-like-operator-to-filter-data"></a>"좋아요" 연산자를 사용 하 여 데이터를 필터링 하려면

비슷한 효과 얻을 수 있습니다는 `QueryExtender` 컨트롤의 `StartsWith`, `Contains`, 및 `EndsWith` 형식을 사용 하 여 검색을 `Like` 연산자에는 `EntityDataSource` 컨트롤의 `Where` 속성. 자습서의이 부분에서 사용 하는 방법을 볼는 `Like` 학생에 대 한 이름으로 검색 하려면 연산자입니다.

오픈 *Students.aspx* 에 **원본** 보기. 이후에 `GridView` 컨트롤에 다음 태그를 추가 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample9.aspx)]

이 태그를 살펴봤습니다 이전 제외한 비슷합니다는 `Where` 속성 값입니다. 두 번째 부분은 합니다 `Where` 하위 문자열 검색을 정의 하는 식 (`LIKE %FirstMidName% or LIKE %LastName%`) 텍스트 상자에 입력 한 모든 것에 대 한 첫 번째 및 마지막 이름이 모두 검색 하는 합니다.

페이지를 실행 합니다. 처음 표시 모든 학생 들에 대 한 기본값을 `StudentName` 매개 변수는 "%"입니다.

[![Image13](the-entity-framework-and-aspnet-getting-started-part-3/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image33.png)

텍스트 상자에 "g" 문자를 입력 하 고 클릭 **검색**합니다. "G"에서 첫 번째 또는 마지막 이름을 가진 학생 들의 목록이 표시 됩니다.

[![Image14](the-entity-framework-and-aspnet-getting-started-part-3/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image35.png)

했으므로 이제 표시, 업데이트, 필터링, 정렬 및 개별 테이블에서 데이터를 그룹화 합니다. 다음 자습서에서 관련된 데이터 (마스터-세부 시나리오)를 사용 하는 것이 먼저 합니다.

> [!div class="step-by-step"]
> [이전](the-entity-framework-and-aspnet-getting-started-part-2.md)
> [다음](the-entity-framework-and-aspnet-getting-started-part-4.md)
