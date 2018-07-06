---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
title: 먼저 Entity Framework 4.0 Database를 사용 하 여 시작 및 ASP.NET 4 Web Forms-4 부 | Microsoft Docs
author: tdykstra
description: Contoso University 샘플 웹 응용 프로그램에는 Entity Framework를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 샘플 응용 프로그램은...
ms.author: aspnetcontent
ms.date: 12/03/2010
ms.assetid: ceb9e60f-957c-4d25-9331-cc527de96a33
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
msc.type: authoredcontent
ms.openlocfilehash: 5f8b1c15fbfd2d65b603013db3902b42faa40665
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37836790"
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-4"></a>먼저 Entity Framework 4.0 Database를 사용 하 여 시작 및 ASP.NET 4 Web Forms-4 부
====================
[Tom Dykstra](https://github.com/tdykstra)

> Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 4.0 및 Visual Studio 2010을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대 한 정보를 참조 하세요. [시리즈의 첫 번째 자습서](the-entity-framework-and-aspnet-getting-started-part-1.md)


## <a name="working-with-related-data"></a>관련 된 데이터 사용

이전 자습서에서 사용한는 `EntityDataSource` 필터, 정렬 및 그룹 데이터를 제어 합니다. 이 자습서에 표시 하 고 관련된 데이터를 업데이트 합니다.

강사의 목록을 보여 주는 강사 페이지를 만들어야 합니다. 강사를 선택 하면 해당 강사가가 르 친 과정의 목록이 표시 됩니다. 강좌를 선택 하면 자세한 과정 및 과정에 등록 한 학생의 목록을 표시 됩니다. 강사 이름, 고용 날짜별 및 사무실 할당을 편집할 수 있습니다. 사무실 할당은 탐색 속성을 통해 액세스 하는 별도 엔터티 집합.

코드 또는 태그에 정보 데이터에 마스터 데이터를 연결할 수 있습니다. 자습서의이 부분에서는 두 방법 모두를 사용 합니다.

[![Image01](the-entity-framework-and-aspnet-getting-started-part-4/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image1.png)

## <a name="displaying-and-updating-related-entities-in-a-gridview-control"></a>표시 및 GridView 컨트롤에서 관련된 엔터티를 업데이트 하는 중

라는 새 웹 페이지를 만듭니다 *Instructors.aspx* 를 사용 하는 *Site.Master* 마스터 페이지, 다음 태그를 추가한 합니다 `Content` 라는 컨트롤 `Content2`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample1.aspx)]

이 태그를 만듭니다는 `EntityDataSource` 강사를 선택 하 고 업데이트를 사용 하도록 설정 하는 컨트롤입니다. `div` 나중에 오른쪽에 열을 추가할 수 있습니다 있도록 왼쪽에서 렌더링할 태그 요소를 구성 합니다.

간의 합니다 `EntityDataSource` 태그와 닫는 `</div>` 태그를 만든 다음 태그를 추가 `GridView` 컨트롤 및 `Label` 오류 메시지를 사용 하는 컨트롤:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample2.aspx)]

이 `GridView` 컨트롤이 행을 선택할 수 있습니다 밝은 회색 배경 색을 사용 하 여 선택된 된 행을 강조 표시 하 고 처리기 (나중에 만들)에 대 한 지정 된 `SelectedIndexChanged` 및 `Updating` 이벤트입니다. 또한 지정 `PersonID` 에 대 한는 `DataKeyNames` 속성을 선택된 된 행의 키 값을 나중에 추가할 다른 컨트롤에 전달할 수 있도록 합니다.

탐색 속성에 저장 된 강사의 사무실 할당을 포함 하는 마지막 열은 `Person` 엔터티 연결 된 엔터티에서 제공 하므로 합니다. `EditItemTemplate` 요소를 지정 `Eval` 대신 `Bind`이므로 `GridView` 업데이트 하기 위해 컨트롤 탐색 속성에 바인딩할 직접 수 없습니다. 코드에서 사무실 할당을 업데이트 하겠습니다. 에 대 한 참조를 위해 필요 합니다 `TextBox` 제어를 가져오고 코드를 저장 하는 합니다 `TextBox` 컨트롤의 `Init` 이벤트.

다음은 `GridView` 컨트롤은을 `Label` 오류 메시지에 사용 되는 컨트롤입니다. 컨트롤의 `Visible` 속성은 `false`를 뷰 상태 해제 된 경우 레이블이 표시만 경우 코드를 사용 하면 오류에 대 한 응답에 표시 되도록 하 고 있습니다.

엽니다는 *Instructors.aspx.cs* 파일을 추가한 다음 `using` 문:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample3.cs)]

Office 할당 텍스트 상자에 대 한 참조를 보유 하는 partial 클래스 이름 선언 바로 뒤 private 클래스 필드를 추가 합니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample4.cs)]

에 대 한 스텁을 추가 `SelectedIndexChanged` 이벤트 처리기를 나중에 코드를 추가 하겠습니다. 사무실 할당에 대 한 처리기를 추가할 수도 `TextBox` 컨트롤의 `Init` 이벤트에 대 한 참조를 저장할 수 있도록는 `TextBox` 제어 합니다. 사용자가 탐색 속성과 연결 된 엔터티를 업데이트 하기 위해 입력 한 값을 가져오려면이 참조를 사용 합니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample5.cs)]

사용 하 여 합니다 `GridView` 컨트롤의 `Updating` 업데이트할 이벤트를 `Location` 속성은 연결 된 `OfficeAssignment` 엔터티. 에 대 한 다음 처리기를 추가 합니다 `Updating` 이벤트:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample6.cs)]

이 코드는 사용자가 클릭할 때 실행 됩니다 **업데이트** 에 `GridView` 행. 코드는 LINQ to Entities 사용 하 여 검색할 합니다 `OfficeAssignment` 현재 연결 된 엔터티 `Person` 엔터티를 사용 하 여를 `PersonID` 이벤트 인수에서 선택한 행의 합니다.

코드를 다음 값에 따라 다음 작업 중 사용 된 `InstructorOfficeTextBox` 제어:

- 경우 텍스트 상자에 값 및 방법이 없는 `OfficeAssignment` 엔터티 업데이트를 하나 만듭니다.
- 텍스트 상자에 값 및 없는 경우는 `OfficeAssignment` 엔터티를 업데이트는 `Location` 속성 값입니다.
- 텍스트 상자가 비어 있으면와 `OfficeAssignment` 엔터티가, 엔터티를 삭제 합니다.

그러면 데이터베이스에 변경 내용을 저장합니다. 예외가 발생 하는 경우 오류 메시지가 표시 됩니다.

페이지를 실행 합니다.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-4/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image3.png)

클릭 **편집** 텍스트 상자에 모든 필드를 변경 합니다.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-4/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image5.png)

이러한 값을 포함 하 여 변경할 **사무실 할당**합니다. 클릭 **업데이트** 목록에 반영 된 변경 내용을 확인할 수 있습니다.

## <a name="displaying-related-entities-in-a-separate-control"></a>별도 컨트롤에 관련된 엔터티를 표시합니다.

각 강사가 추가할 수 있도록 하나 이상의 강의 학습할 수 있습니다는 `EntityDataSource` 컨트롤 및 `GridView` 컨트롤을 연결 된 강사에 어떤 강사가 선택 된 과정 목록 `GridView` 제어 합니다. 제목을 만들려면 하며 `EntityDataSource` 강좌 엔터티에 대 한 컨트롤에 오류 메시지 사이 다음 태그를 추가 합니다 `Label` 컨트롤과 닫는 `</div>` 태그:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample7.aspx)]

`Where` 의 값을 포함 하는 매개 변수를 `PersonID` 인 행을 선택한 강사의는 `InstructorsGridView` 컨트롤입니다. `Where` 속성에 모두 연결 된 하위 select 명령이 `Person` 에서 엔터티를 `Course` 엔터티의 `People` 탐색 속성 및 선택은 `Course` 경우에만 엔터티 연결된 중`Person`엔터티에 포함 선택한 `PersonID` 값입니다.

만들려는 합니다 `GridView` 제어 합니다. 바로 뒤에 다음 태그를 추가 합니다 `CoursesEntityDataSource` 컨트롤 (닫기 전에 `</div>` 태그):

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample8.aspx)]

강좌가 없다는 없는 강사를 선택 하면 표시 되는 `EmptyDataTemplate` 요소가 포함 됩니다.

페이지를 실행 합니다.

[![Image04](the-entity-framework-and-aspnet-getting-started-part-4/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image7.png)

강사에 할당 하는 하나 이상의 강의 권한이 있는 사용자를 선택 하 고 과정을 과정 목록에 표시 합니다. (참고: 데이터베이스 스키마에서는 여러 코스를 수 있지만 데이터베이스와 함께 제공 되는 테스트 데이터 없음 강사 실제로 둘 이상의 과정입니다. 직접 추가할 수 있습니다 과정 데이터베이스에 사용 하는 **서버 탐색기** 창 또는 *CoursesAdd.aspx* 자습서의 뒷부분에서 추가 하는 페이지입니다.)

[![Image05](the-entity-framework-and-aspnet-getting-started-part-4/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image9.png)

`CoursesGridView` 컨트롤이 몇 과정 필드만 표시 합니다. 강좌에 대 한 모든 세부 정보를 표시 하려면 사용할지는 `DetailsView` 사용자가 선택한 과정에 대 한 제어 합니다. *Instructors.aspx*를 닫은 후 다음 태그를 추가 `</div>` 태그 (이 태그를 배치 해야 **후** 닫는 div 태그를 그 이전이 아님).

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample9.aspx)]

이 태그를 만듭니다는 `EntityDataSource` 컨트롤에 바인딩되는 `Courses` 엔터티 집합입니다. 합니다 `Where` 속성을 사용 하 여 과정을 선택 합니다 `CourseID` 과정에서 선택한 행의 값 `GridView` 컨트롤입니다. 태그 지정에 대 한 처리기를 `Selected` 이벤트 학생 성적을 표시 하기 위해 나중에 사용할 수는 계층의 다른 수준이 있습니다.

*Instructors.aspx.cs*에 대 한 다음 스텁 만들기는 `CourseDetailsEntityDataSource_Selected` 메서드. (이 자습서의 뒷부분에 나오는이 스텁 채웁니다; 지금은 필요한 페이지 컴파일 및 실행 되도록 합니다.)

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample10.cs)]

페이지를 실행 합니다.

[![Image06](the-entity-framework-and-aspnet-getting-started-part-4/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image11.png)

처음에 없는 과정 선택 되었기 때문에 강좌 세부 정보가 있습니다. 강사 강좌에 할당 된 권한이 있는 사용자를 선택 하 고 세부 정보를 보려면 강좌를 선택 합니다.

[![Image07](the-entity-framework-and-aspnet-getting-started-part-4/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image13.png)

## <a name="using-the-entitydatasource-selected-event-to-display-related-data"></a>EntityDataSource를 사용 하 여 "선택" 관련된 데이터를 표시 하는 이벤트

마지막으로 등록 된 학생 및 해당 등급 선택한 과정의 모든 표시 하려고 합니다. 이 위해 사용 하 여 합니다 `Selected` 의 이벤트를 `EntityDataSource` 강좌에 바인딩된 컨트롤 `DetailsView`합니다.

*Instructors.aspx*, 뒤에 다음 태그를 추가 합니다 `DetailsView` 제어:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample11.aspx)]

이 태그를 만듭니다를 `ListView` 학생 및 선택한 과정에 대 한 해당 등급의 목록을 표시 하는 컨트롤입니다. 데이터 소스 코드에서 컨트롤 databind를 해야 하기 때문에 지정 됩니다. `EmptyDataTemplate` 없습니다 강좌가 선택 된 경우 표시할 메시지를 제공 하는 요소-경우에 표시할 학생이 없는 합니다. 합니다 `LayoutTemplate` 요소를 목록에 표시할 HTML 테이블을 만듭니다 및 `ItemTemplate` 표시할 열을 지정 합니다. 학생 ID와 학생 등급은는 `StudentGrade` 에서 학생 이름과 엔터티는 `Person` Entity Framework에서 사용할 수 있도록 엔터티는 `Person` 의 탐색 속성은 `StudentGrade` 엔터티.

*Instructors.aspx.cs*, 스텁 아웃 대체 `CourseDetailsEntityDataSource_Selected` 메서드를 다음 코드로:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample12.cs)]

이 이벤트에 대 한 이벤트 인수 형식 아무것도 선택 하지 않으면 항목이 0 또는 1 개의 항목을 포함 하는 컬렉션으로 선택한 데이터를 제공 하는 경우는 `Course` 엔터티를 선택 합니다. 경우는 `Course` 엔터티를 선택 하면 코드를 사용 하는 `First` 단일 개체 컬렉션으로 변환 하는 방법입니다. 다음 가져옵니다 `StudentGrade` 탐색 속성에서 엔터티 컬렉션으로 변환 합니다 및 바인딩하는 `GradesListView` 컨트롤을 컬렉션입니다.

표시할 등급 있지만 빈 데이터 템플릿에서 메시지 페이지는 처음으로 표시 되어 있는지 확인 하려면 충분 한 이며 때마다 과정을 선택 하지 않습니다. 이렇게 하려면 두 위치에서 호출 하는 다음 메서드를 만듭니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample13.cs)]

이 새 메서드를 호출 합니다 `Page_Load` 페이지를 표시할 빈 데이터 템플릿 첫 번째 시간을 표시 하는 방법입니다. 호출을 `InstructorsGridView_SelectedIndexChanged` 메서드는 강사가 선택 된 경우 해당 이벤트가 발생 하기 때문에 새 강의 의미 하는 로드 되는 과정 `GridView` 컨트롤과 none 아직 선택 합니다. 두 개의 호출은 다음과 같습니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample14.cs)]

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample15.cs)]

페이지를 실행 합니다.

[![Image08](the-entity-framework-and-aspnet-getting-started-part-4/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image15.png)

강좌에 할당 된 강사를 선택 하 고 과정을 선택 합니다.

[![Image09](the-entity-framework-and-aspnet-getting-started-part-4/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image17.png)

이제 관련 데이터로 작업 하는 몇 가지 방법을 살펴보았습니다. 다음 자습서에서는 기존 엔터티 간의 관계를 추가 하는 방법을 알아봅니다 관계를 제거 하는 방법 및 기존 엔터티에 관계가 있는 새 엔터티를 추가 하는 방법입니다.

> [!div class="step-by-step"]
> [이전](the-entity-framework-and-aspnet-getting-started-part-3.md)
> [다음](the-entity-framework-and-aspnet-getting-started-part-5.md)
