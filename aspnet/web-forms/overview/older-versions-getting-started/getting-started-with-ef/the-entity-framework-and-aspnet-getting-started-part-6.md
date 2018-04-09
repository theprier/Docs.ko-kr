---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-6
title: 먼저 Entity Framework 4.0 데이터베이스와 시작 및 ASP.NET 4 Web Forms-6 부 | Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 샘플 응용 프로그램은...
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/03/2010
ms.topic: article
ms.assetid: 994a5496-c648-4830-b03c-55bb43f325d2
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-6
msc.type: authoredcontent
ms.openlocfilehash: b76be25501275ba676c9a9acca8e73333439ee70
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-6"></a>먼저 Entity Framework 4.0 데이터베이스와 시작 및 ASP.NET 4 Web Forms-6 부
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

> Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 4.0 및 Visual Studio 2010을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대 한 정보를 참조 하세요. [시리즈의 첫 번째 자습서](the-entity-framework-and-aspnet-getting-started-part-1.md)


## <a name="implementing-table-per-hierarchy-inheritance"></a>계층당 하나의 테이블 상속 구현

이전 자습서에서 사용한 관련된 데이터를 추가 하 고 관계를 삭제 하 고 기존 엔터티에 대 한 관계 수 있었던 새 엔터티를 추가 하 여 합니다. 이 자습서에서는 데이터 모델에서 상속을 구현하는 방법을 보여 줍니다.

개체 지향 프로그래밍 관련된 클래스를 사용 하 여 쉽게 수행할 수 있도록 상속을 사용할 수 있습니다. 만들 수는 예를 들어 `Instructor` 및 `Student` 에서 파생 된 클래스는 `Person` 기본 클래스입니다. Entity Framework에서 동일한 종류의 엔터티 간에 상속 구조를 만들 수 있습니다.

자습서의이 부분에서는 새 웹 페이지를 만들지 않습니다. 대신 엔터티 데이터 모델에 파생 된 추가 하 고 새 엔터티를 사용 하도록 기존 페이지를 수정 합니다.

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a>형식당 하나의 테이블 상속 및 계층 당 테이블

데이터베이스는 여러 테이블에서 하나 이상의 테이블이 나 관련된 개체에 대 한 정보를 저장할 수 있습니다. 예를 들어는 `School` 데이터베이스는 `Person` 학생과 단일 테이블에서 강사에 대 한 정보가 포함 됩니다. 강사에만 적용의 일부 열 (`HireDate`), 학생에만 일부 (`EnrollmentDate`), 둘 다에 일부 (`LastName`, `FirstName`).

[![image11](the-entity-framework-and-aspnet-getting-started-part-6/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image1.png)

만들려는 Entity Framework를 구성할 수 있습니다 `Instructor` 및 `Student` 에서 상속 하는 엔터티는 `Person` 엔터티. 이 패턴의 단일 데이터베이스 테이블에서 엔터티 상속 구조를 생성 하 라고 *테이블 계층당* TPH () 상속 합니다.

과정을에 대 한는 `School` 데이터베이스는 다른 패턴을 사용 합니다. 온라인 강좌 및 온사이트 과정을 가리키는 외래 키가 각각 별도 테이블에 저장 됩니다는 `Course` 테이블입니다. 두 과정 유형 모두에 공통적인 정보에만 저장 됩니다는 `Course` 테이블입니다.

[![image12](the-entity-framework-and-aspnet-getting-started-part-6/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image3.png)

Entity Framework 데이터 모델을 구성할 수 있도록 `OnlineCourse` 및 `OnsiteCourse` 에서 상속 하는 엔터티는 `Course` 엔터티. 이 패턴의 모든 형식에 공통 된 데이터를 저장 하는 테이블을 다시 가리키는 별도 각 테이블의 각 유형에 대해 별도 테이블에서 엔터티 상속 구조를 생성 하 라고 *형식당 하나의 테이블* (TPT) 상속 합니다.

TPH 상속 패턴 일반적으로 더 나은 성능을 제공 TPT 상속 패턴 보다 Entity Framework에서 TPT 패턴 복잡 한 조인 쿼리에서 발생할 수 있기 때문입니다. 이 연습에서는 TPH 상속 구현 하는 방법을 보여 줍니다. 다음 단계를 수행 하 여 수행 합니다.

- 만들 `Instructor` 및 `Student` 엔터티 형식에서 파생 되는 `Person`합니다.
- 파생 된 엔터티에 관련 된 이동 속성은 `Person` 파생된 엔터티.
- 파생된 형식에서 속성에 대 한 제약 조건을 설정 합니다.
- 확인 된 `Person` 엔터티는 추상 엔터티입니다.
- 지도는 각 엔터티를 파생는 `Person` 확인 하는 방법을 지정 하는 조건 포함 된 테이블 여부는 `Person` 행 파생 형식을 나타냅니다.

## <a name="adding-instructor-and-student-entities"></a>강사 및 학생 엔터티 추가

열기는 <em>SchoolModel.edmx</em> 파일, 선택 디자이너에서 빈된 영역을 마우스 오른쪽 단추로 클릭 <strong>추가</strong>을 선택한 후 <strong>엔터티</strong><em>합니다.</em>

[![image01](the-entity-framework-and-aspnet-getting-started-part-6/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image5.png)

에 **엔터티 추가** 대화 상자에서 엔터티 이름 `Instructor` 설정 하 고 해당 **기본 형식** 옵션을 `Person`합니다.

[![image02](the-entity-framework-and-aspnet-getting-started-part-6/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image7.png)

**확인**을 클릭합니다. 디자이너에서 만듭니다는 `Instructor` 에서 파생 되는 엔터티는 `Person` 엔터티. 새 엔터티가 아직 없는 모든 속성.

[![image03](the-entity-framework-and-aspnet-getting-started-part-6/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image9.png)

만드는 절차를 반복 하는 `Student` 또한에서 파생 된 엔터티 `Person`합니다.

해당 속성을 이동 해야 하므로 강사가 고용 날짜는 `Person` 엔터티를는 `Instructor` 엔터티. 에 `Person` 엔터티를 마우스 오른쪽 단추로 클릭는 `HireDate` 속성 **잘라내기**합니다. 마우스 오른쪽 단추로 클릭 한 다음 **속성** 에 `Instructor` 엔터티와 클릭 **붙여넣기**합니다.

[![image04](the-entity-framework-and-aspnet-getting-started-part-6/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image11.png)

고용 날짜는 `Instructor` 엔터티는 null 일 수 없습니다. 마우스 오른쪽 단추로 클릭는 `HireDate` 속성을 클릭 하 여 **속성**, 한 다음는 **속성** 창 변경 `Nullable` 를 `False`합니다.

[![image05](the-entity-framework-and-aspnet-getting-started-part-6/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image13.png)

이동 하는 절차를 반복 하는 `EnrollmentDate` 속성은 `Person` 엔터티를는 `Student` 엔터티. 설정 하 고 있는지 확인 `Nullable` 를 `False` 에 대 한는 `EnrollmentDate` 속성입니다.

이제는 `Person` 엔터티에에 공통 된 속성만 `Instructor` 및 `Student` 엔터티 (외에도 탐색 속성을 이동 하지 않는), 엔터티 에서만 사용할 수 있습니다에 상속 구조를 기준 엔터티로 합니다. 따라서 독립 엔터티로 처리 되지 있는지 확인 해야 합니다. 마우스 오른쪽 단추로 클릭는 `Person` 엔터티를 **속성**, 한 다음는 **속성** 의 값을 변경 하는 창 고 **추상** 속성을  **True 이면**합니다.

[![image06](the-entity-framework-and-aspnet-getting-started-part-6/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image15.png)

## <a name="mapping-instructor-and-student-entities-to-the-person-table"></a>Person 테이블에 강사 및 학생 엔터티 매핑

이제 Entity Framework를 구별 하는 방법만 알리면 `Instructor` 및 `Student` 데이터베이스의 엔터티.

마우스 오른쪽 단추로 클릭는 `Instructor` 엔터티와 선택 **테이블 매핑**합니다. 에 **매핑 정보** 창 클릭 **테이블 또는 뷰 추가** 선택 **사람**합니다.

[![image07](the-entity-framework-and-aspnet-getting-started-part-6/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image17.png)

클릭 **조건을 추가**를 선택한 후 **HireDate**합니다.

[![image09](the-entity-framework-and-aspnet-getting-started-part-6/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image19.png)

변경 **연산자** 를 **은** 및 **값 / 속성** 를 **Not Null**합니다.

[![image10](the-entity-framework-and-aspnet-getting-started-part-6/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image21.png)

에 대 한 절차를 반복 하는 `Students` 엔터티를이 엔터티에 매핑됩니다 지정 하는 `Person` 하면 테이블의 `EnrollmentDate` 열이 null입니다. 그런 다음 저장 하 고 데이터 모델을 닫습니다.

새 엔터티 클래스를 만들고 디자이너에서 사용할 수 있도록 하기 위해 프로젝트를 빌드하십시오.

## <a name="using-the-instructor-and-student-entities"></a>강사 및 학생 엔터티를 사용 하 여

학생과 강사 데이터를 데이터 바인딩된 있습니다를 사용 하는 웹 페이지를 만들 때는 `Person` 엔터티 집합에 필터링 및는 `HireDate` 또는 `EnrollmentDate` 학생 또는 강사에 반환된 된 데이터를 제한 하는 속성입니다. 그러나 이제 바인딩하는 경우 각 데이터 소스 제어에는 `Person` 엔터티 집합만 지정할 수 있습니다 `Student` 또는 `Instructor` 엔터티 형식을 선택 해야 합니다. Entity Framework에서 강사 학생을 구분 하는 방법을 알기 때문에 `Person` 엔터티 집합을 제거할 수 있습니다는 `Where` 속성 설정 작업을 수행 하는 직접 입력 합니다.

Visual Studio 디자이너에서 지정할 수 있습니다 하는 엔터티 유형는 `EntityDataSource` 컨트롤에서 선택 해야는 **EntityTypeFilter** 의 드롭다운 목록 상자는 `Configure Data Source` 마법사에서 다음 예제와 같이 합니다.

[![image13](the-entity-framework-and-aspnet-getting-started-part-6/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image23.png)

및에 **속성** 창을 제거할 수 없습니다 `Where` 더 이상 필요 없는, 다음 예제와 같이 절 값입니다.

[![image14](the-entity-framework-and-aspnet-getting-started-part-6/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image25.png)

그러나에 대 한 태그를 변경한 후 때문에 `EntityDataSource` 사용할 수 있는 컨트롤의 `ContextTypeName` 특성을 실행할 수 없습니다.는 **데이터 소스 구성** 에서 마법사 `EntityDataSource` 이미 작성 하는 컨트롤입니다. 따라서 대신 태그를 변경 하 여 필요한 변경 작업을 확인 합니다.

열기는 *Students.aspx* 페이지. 에 `StudentsEntityDataSource` 컨트롤을 제거는 `Where` 특성을 추가 `EntityTypeFilter="Student"` 특성입니다. 이제 태그 다음 예와 비슷하게 표시 됩니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample1.aspx)]

설정의 `EntityTypeFilter` 되도록 특성의 `EntityDataSource` 컨트롤에 지정 된 엔터티 형식에만 선택 됩니다. 모두 검색 하려면 `Student` 및 `Instructor` 엔터티 형식에는 설정 하면이 특성입니다. (하나를 사용 하는 여러 엔터티 형식을 검색 하는 옵션이 제공 `EntityDataSource` 읽기 전용 데이터 액세스를 위한 컨트롤을 사용 하는 경우에 제어 합니다. 사용 중인 경우는 `EntityDataSource` 컨트롤을 삽입, 업데이트 또는 엔터티를 삭제 하 고 엔터티 집합에 바인딩되어 여러 형식을 포함할 수 있으면 하나의 엔터티 형식에만 사용할 수 있습니다이 특성을 설정 해야 합니다.)

에 대 한 절차를 반복 하는 `SearchEntityDataSource` 제거 부분에만 제외 하 고 제어는 `Where` 특성을 선택 하 `Student` 엔터티 속성을 모두 제거 하는 대신 합니다. 이제 컨트롤의 여는 태그 다음 예와 비슷하게 표시 됩니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample2.aspx)]

이전 동작을 확인 하려면 페이지를 실행 합니다.

[![image15](the-entity-framework-and-aspnet-getting-started-part-6/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image27.png)

새 사용할 수 있도록 이전 자습서에서 만든 다음 페이지를 업데이트 `Student` 및 `Instructor` 엔터티 대신 `Person` 엔터티, 한 다음 실행 전과 마찬가지로 작동 하는지 확인 하려면:

- *StudentsAdd.aspx*, 추가 `EntityTypeFilter="Student"` 에 `StudentsEntityDataSource` 제어 합니다. 이제 태그 다음 예와 비슷하게 표시 됩니다. 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample3.aspx)]

    [![image16](the-entity-framework-and-aspnet-getting-started-part-6/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image29.png)
- *About.aspx*, 추가 `EntityTypeFilter="Student"` 에 `StudentStatisticsEntityDataSource` 제어 하 고 제거 `Where="it.EnrollmentDate is not null"`합니다. 이제 태그 다음 예와 비슷하게 표시 됩니다. 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample4.aspx)]

    [![image17](the-entity-framework-and-aspnet-getting-started-part-6/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image31.png)
- *Instructors.aspx* 및 *InstructorsCourses.aspx*, 추가 `EntityTypeFilter="Instructor"` 에 `InstructorsEntityDataSource` 제어 하 고 제거 `Where="it.HireDate is not null"`합니다. 에 있는 태그 *Instructors.aspx* 이제 다음 예제와 유사 합니다. 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample5.aspx)]

    [![image18](the-entity-framework-and-aspnet-getting-started-part-6/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image33.png)

    에 있는 태그 *InstructorsCourses.aspx* 는 이제 다음 예제와 비슷합니다.

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample6.aspx)]

    [![image19](the-entity-framework-and-aspnet-getting-started-part-6/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image35.png)

이러한 변경으로 인해 여러 가지 방법으로 Contoso 대학 응용 프로그램의 유지 관리를 개선 했습니다. 선택 및 유효성 검사 논리 UI 계층 제외 이동한 (*.aspx* 태그) 및 데이터 액세스 계층의 필수적인 부분을 수행 합니다. 이렇게 하면 변경 된 내용 데이터베이스 스키마 나 데이터 모델을 나중에 하도록 할 수 있는 응용 프로그램 코드를 격리할 수 있습니다. 예를 들어 학생 교사 보조 기능으로 고용 수 및 따라서 고용 날짜를 가져오는 것을 결정할 수 있습니다. 다음에서 강사 학생을 구분 하 고 데이터 모델을 업데이트 하려면 새 속성을 추가할 수 있습니다. 웹 응용 프로그램에서 코드가 없는 학생용 고용 날짜를 표시 하려는 제외 하 고 변경 해야 합니다. 추가 하는 또 다른 이점은 `Instructor` 및 `Student` 엔터티를 참조할 때 보다 더 쉽게 이해할 수 있는 코드 된다는 점입니다 `Person` 실제로 학생 했던 개체 또는 강사 합니다.

이제 Entity Framework에서 한 상속 패턴을 구현 하는 방법을 살펴보았습니다. 다음 자습서에서는 Entity Framework 데이터베이스를 액세스 하는 방법을 보다 자세하게 제어 하기 위해 저장된 프로시저를 사용 하는 방법을 설명 합니다.

> [!div class="step-by-step"]
> [이전](the-entity-framework-and-aspnet-getting-started-part-5.md)
> [다음](the-entity-framework-and-aspnet-getting-started-part-7.md)
