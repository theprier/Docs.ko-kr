---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
title: "먼저 Entity Framework 4.0 데이터베이스와 시작 및 ASP.NET 4 Web Forms-4 부 | Microsoft Docs"
author: tdykstra
description: "Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 샘플 응용 프로그램은..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/03/2010
ms.topic: article
ms.assetid: ceb9e60f-957c-4d25-9331-cc527de96a33
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
msc.type: authoredcontent
ms.openlocfilehash: 06d129384fc78db21ad1b9224781deab6a0e91a5
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-4"></a>먼저 Entity Framework 4.0 데이터베이스와 시작 및 ASP.NET 4 Web Forms-4 부
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

> Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 4.0 및 Visual Studio 2010을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대 한 정보를 참조 하세요. [시리즈의 첫 번째 자습서](the-entity-framework-and-aspnet-getting-started-part-1.md)


## <a name="working-with-related-data"></a>관련된 데이터 작업

이전 자습서에서 사용 되는 `EntityDataSource` 필터, 정렬 및 그룹 데이터를 제어 합니다. 이 자습서에서는 표시 하 고 관련된 데이터를 업데이트 합니다.

강사의 목록을 보여 주는 강사 페이지를 만듭니다. 강사를 선택 하면 해당 강사 여 courses 목록이 표시 됩니다. 과정을 선택 하면 등록 과정에 학생의 목록과 과정에 대 한 세부 정보 표시 됩니다. 강사 이름, 고용 날짜 및 사무실 할당을 편집할 수 있습니다. Office 할당 탐색 속성을 통해 액세스 하는 별도 엔터티 집합입니다.

마스터 데이터는 세부 데이터 또는 코드에서 태그를 연결할 수 있습니다. 자습서의이 부분에서는 두 방법 모두를 사용 합니다.

[![Image01](the-entity-framework-and-aspnet-getting-started-part-4/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image1.png)

## <a name="displaying-and-updating-related-entities-in-a-gridview-control"></a>표시 및 GridView 컨트롤에서 관련된 엔터티를 업데이트 합니다.

라는 새 웹 페이지 생성 *Instructors.aspx* 를 사용 하는 *Site.Master* 마스터 페이지, 다음 태그를 추가 하 고는 `Content` 라는 컨트롤 `Content2`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample1.aspx)]

이 태그를 만듭니다는 `EntityDataSource` 강사를 선택 하 고 업데이트 하는 컨트롤입니다. `div` 요소 오른쪽에 나중에 열을 추가할 수 있도록 왼쪽 렌더링 하도록 태그를 구성 합니다.

사이 `EntityDataSource` 태그와 닫는 `</div>` 태그에 다음 태그를 만드는 추가 `GridView` 제어 및 `Label` 제어 하는 오류 메시지에 대해 사용할:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample2.aspx)]

이 `GridView` 행을 선택할 수, 선택 된 행을 밝은 회색 배경 색으로 강조 표시 및 지정 하는 처리기 (나중에 만들)에 대 한 제어는 `SelectedIndexChanged` 및 `Updating` 이벤트입니다. 또한 지정 `PersonID` 에 대 한는 `DataKeyNames` 속성을 나중에 추가할 다른 컨트롤에 선택된 된 행의 키 값을 전달 될 수 있도록 합니다.

마지막 열이 포함 되어 강의 사무실 할당의 탐색 속성에 저장 되는 `Person` 엔터티 연결 된 엔터티의 있기 때문에 있습니다. 다음에 유의 `EditItemTemplate` 요소 지정 `Eval` 대신 `Bind`때문에 `GridView` 컨트롤을 업데이트 하려면 탐색 속성에 바인딩할 직접 수 없습니다. 코드에서 사무실 할당을 업데이트 합니다. 이렇게 하려면에 대 한 참조 해야 합니다는 `TextBox` 제어를 가져오고 저장에서 하는 것은 `TextBox` 컨트롤의 `Init` 이벤트입니다.

다음은 `GridView` 컨트롤은 한 `Label` 오류 메시지에 사용 되는 컨트롤입니다. 컨트롤의 `Visible` 속성은 `false`, 및 뷰 상태 꺼져만 때 코드 표시 되도록 오류에 대 한 응답으로 레이블이 표시 되도록 합니다.

열기는 *Instructors.aspx.cs* 파일을 다음 추가 `using` 문:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample3.cs)]

Office 할당 텍스트 상자에 대 한 참조를 보유 하는 partial 클래스 이름 선언 바로 뒤 전용 클래스 필드를 추가 합니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample4.cs)]

에 대 한 스텁 추가 `SelectedIndexChanged` 이벤트 처리기를 나중에 코드를 추가 합니다. 또한 사무실 할당에 대 한 처리기를 추가 `TextBox` 컨트롤의 `Init` 이벤트에 대 한 참조를 저장할 수 있도록는 `TextBox` 제어 합니다. 사용자가 탐색 속성에 연결 된 엔터티를 업데이트 하기 위해 입력 한 값을이 참조를 사용 합니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample5.cs)]

사용 하 여는 `GridView` 컨트롤의 `Updating` 업데이트 하는 이벤트는 `Location` 속성은 연결 된 `OfficeAssignment` 엔터티. 에 대 한 다음 처리기를 추가 `Updating` 이벤트:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample6.cs)]

이 코드를 클릭할 때 실행 **업데이트** 에 `GridView` 행입니다. 코드는 LINQ to Entities 사용 하 여 검색 된 `OfficeAssignment` 현재와 관련 된 엔터티 `Person` 엔터티를 사용 하 여는 `PersonID` 이벤트 인수에서 선택한 행의 합니다.

값에 따라 다음 작업 중 하나는 코드는 다음 됩니다는 `InstructorOfficeTextBox` 제어:

- 텍스트 상자에 값이 되 고 없습니다 `OfficeAssignment` 를 업데이트 하려면 엔터티 하나 만듭니다.
- 텍스트 상자에 값이 되 고는 `OfficeAssignment` 업데이트 엔터티에 `Location` 속성 값입니다.
- 텍스트 상자가 비어 고 `OfficeAssignment` 엔터티, 엔터티를 삭제 합니다.

이후에 데이터베이스에 변경 내용을 저장합니다. 예외가 발생 하면 오류 메시지가 표시 됩니다.

페이지를 실행 합니다.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-4/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image3.png)

클릭 **편집** 하 고 텍스트 상자에 모든 필드를 변경 합니다.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-4/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image5.png)

이러한 값을 포함 하 여 변경 **사무실 할당**합니다. 클릭 **업데이트** 목록에 반영 된 변경 내용을 볼 수 있습니다.

## <a name="displaying-related-entities-in-a-separate-control"></a>별도 컨트롤에 관련된 엔터티를 표시합니다.

각 강사를 추가할 수 있도록 하나 이상의 과정을 학습 시킬 수 있습니다는 `EntityDataSource` 제어 및 `GridView` 컨트롤을 나오든 이들 강사 강사에서 선택 된 연관 courses 목록 `GridView` 제어 합니다. 제목을 만들려면 및 `EntityDataSource` courses 엔터티에 대 한 제어, 오류 메시지 사이 다음 태그를 추가 `Label` 제어 및 닫는 `</div>` 태그:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample7.aspx)]

`Where` 의 값을 포함 하는 매개 변수는 `PersonID` 의 해당 행을 선택한 강사는 `InstructorsGridView` 제어 합니다. `Where` 속성을 가져오는 연결 된 모든 하위 select 명령을 포함 `Person` 에서 엔터티는 `Course` 엔터티의 `People` 탐색 속성을 선택은 `Course` 엔터티 경우에만 관련된 중`Person`엔터티 포함 선택한 `PersonID` 값입니다.

만들려는 `GridView` 컨트롤입니다. 바로 뒤에 다음 태그를 추가 `CoursesEntityDataSource` 컨트롤 (닫는 앞 `</div>` 태그):

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample8.aspx)]

없는 courses 없는 강사를 선택 하면 표시 됩니다 때문에 프로그램 `EmptyDataTemplate` 요소가 포함 됩니다.

페이지를 실행 합니다.

[![Image04](the-entity-framework-and-aspnet-getting-started-part-4/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image7.png)

에 할당 하는 하나 이상의 과정을 가진 강사 선택한 과정 또는 courses 목록에 표시 합니다. (참고: 데이터베이스 스키마에서는 여러 강좌를 수 있지만 데이터베이스와 함께 제공 되는 테스트 데이터의 없는 강사 권한이 실제로 둘 이상의 과정입니다. 추가할 수 있습니다 courses 데이터베이스에 직접 사용 하는 **서버 탐색기** 창 또는 *CoursesAdd.aspx* 페이지 자습서의 뒷부분에 추가 합니다.)

[![Image05](the-entity-framework-and-aspnet-getting-started-part-4/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image9.png)

`CoursesGridView` 컨트롤 과정 필드를 몇 개만 표시 합니다. 과정에 대 한 모든 세부 정보를 표시 하려면 사용 합니다는 `DetailsView` 사용자가을 선택 하는 과정에 대 한 제어 합니다. *Instructors.aspx*를 닫은 후 다음 태그를 추가 `</div>` 태그 (이 태그를 배치 해야 **후** 닫는 div 태그, 날짜부터 해당):

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample9.aspx)]

이 태그를 만듭니다는 `EntityDataSource` 에 바인딩되는 컨트롤은 `Courses` 엔터티 집합입니다. `Where` 를 사용 하 여 과정을 선택 하는 속성의 `CourseID` 코스에서 선택한 행의 값 `GridView` 제어 합니다. 에 대 한 처리기를 지정 하는 태그는 `Selected` 이벤트를 나중에 사용할 학생 등급을 표시 하기 위한을 하위 계층에 다른 수준입니다.

*Instructors.aspx.cs*에 대 한 다음 스텁을 `CourseDetailsEntityDataSource_Selected` 메서드. (이 자습서의 뒷부분에 나오는이 스텁을 채우는 속도가; 지금은 필요한 페이지를 컴파일하고 실행 되도록 합니다.)

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample10.cs)]

페이지를 실행 합니다.

[![Image06](the-entity-framework-and-aspnet-getting-started-part-4/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image11.png)

처음에 없는 과정 선택 되었기 때문에 과정 세부 정보가 있습니다. 할당 하는 과정을 가진 강사를 선택한 다음 세부 정보를 과정을 선택 합니다.

[![Image07](the-entity-framework-and-aspnet-getting-started-part-4/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image13.png)

## <a name="using-the-entitydatasource-selected-event-to-display-related-data"></a>EntityDataSource를 사용 하 여 "선택" 이벤트 관련된 데이터 표시

마지막으로 등록 된 학생 및 선택한 과정에 대 한 자신의 등급을 모두 표시 하려고 합니다. 이 작업을 수행 하려면을 사용 합니다는 `Selected` 의 이벤트는 `EntityDataSource` 과정에 바인딩된 컨트롤 `DetailsView`합니다.

*Instructors.aspx*, 다음 태그 뒤에 추가 `DetailsView` 제어:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample11.aspx)]

이 태그를 만듭니다는 `ListView` 학생 선택한 과정에 대 한 자신의 등급의 목록을 표시 하는 컨트롤입니다. 데이터 원본이 없는 databind 코드에서 컨트롤 수 때문에 지정 됩니다. `EmptyDataTemplate` 없는 과정을 선택 하는 경우 표시할 메시지를 제공 하는 요소-경우에 표시 하는 학생은 있습니다. `LayoutTemplate` 요소 목록을 표시 하는 HTML 테이블을 만듭니다 및 `ItemTemplate` 표시할 열을 지정 합니다. 학생 ID와 학생 등급이는 `StudentGrade` 엔터티와 학생 이름에서이 `Person` Entity Framework에서 사용할 수 있도록 하는 엔터티는 `Person` 의 탐색 속성은 `StudentGrade` 엔터티.

*Instructors.aspx.cs*, 대체 스텁 아웃 `CourseDetailsEntityDataSource_Selected` 메서드를 다음 코드로:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample12.cs)]

이 이벤트에 대 한 이벤트 인수 형식 아무것도 선택 하지 않으면 항목이 0 또는 1 개의 항목 포함 하는 컬렉션으로 선택한 데이터를 제공 하는 경우는 `Course` 엔터티를 선택 합니다. 경우는 `Course` 엔터티가 선택 되었는지, 코드를 사용 하 여는 `First` 메서드를 단일 개체 컬렉션으로 변환 합니다. 그런 다음 가져옵니다 `StudentGrade` 탐색 속성에서 엔터티 컬렉션으로 변환 및 바인딩하는 `GradesListView` 컨트롤 컬렉션을 합니다.

표시 하려면 등급, 하지만 빈 데이터 서식 파일에 메시지 페이지는 처음으로 표시 되는지 확인 하려면 충분 한 며이 과정을 선택 하지 않으면 때마다입니다. 이렇게 하려면 두 위치에서 호출 하는 다음 메서드를 만듭니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample13.cs)]

이 새 메서드를 호출 하는 `Page_Load` 메서드를 페이지가 표시 되는 빈 데이터 템플릿을 처음 시간을 표시 합니다. 호출에서 `InstructorsGridView_SelectedIndexChanged` 메서드 강사 선택 된 경우 해당 이벤트가 발생 하기 때문에 새 과정을 의미 하는 강의에 로드 `GridView` 컨트롤과 none 아직 선택 되어 있습니다. 다음은 두 번 호출입니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample14.cs)]

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample15.cs)]

페이지를 실행 합니다.

[![Image08](the-entity-framework-and-aspnet-getting-started-part-4/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image15.png)

할당 하는 과정을 가진 강사를 선택 하 고 과정을 선택 합니다.

[![Image09](the-entity-framework-and-aspnet-getting-started-part-4/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image17.png)

관련 된 데이터로 작업 하는 몇 가지 방법을 살펴 보았습니다. 다음 자습서에서는 기존 엔터티 간의 관계를 추가 하는 방법을 알아봅니다 관계를 제거 하는 방법 및 기존 엔터티와 관계를 맺고 있는 새 엔터티를 추가 하는 방법입니다.

>[!div class="step-by-step"]
[이전](the-entity-framework-and-aspnet-getting-started-part-3.md)
[다음](the-entity-framework-and-aspnet-getting-started-part-5.md)
