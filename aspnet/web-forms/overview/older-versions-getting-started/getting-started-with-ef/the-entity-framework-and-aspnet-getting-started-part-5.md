---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
title: 먼저 Entity Framework 4.0 Database를 사용 하 여 시작 및 ASP.NET 4 Web Forms-5 부 | Microsoft Docs
author: tdykstra
description: Contoso University 샘플 웹 응용 프로그램에는 Entity Framework를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 샘플 응용 프로그램은...
ms.author: aspnetcontent
ms.date: 12/03/2010
ms.assetid: 24ad4379-3fb2-44dc-ba59-85fe0ffcb2ae
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
msc.type: authoredcontent
ms.openlocfilehash: b175bb8d6edb8b59c14da59f4576e9029e663dde
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37835261"
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-5"></a>먼저 Entity Framework 4.0 Database를 사용 하 여 시작 및 ASP.NET 4 Web Forms-5 부
====================
[Tom Dykstra](https://github.com/tdykstra)

> Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 4.0 및 Visual Studio 2010을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대 한 정보를 참조 하세요. [시리즈의 첫 번째 자습서](the-entity-framework-and-aspnet-getting-started-part-1.md)


## <a name="working-with-related-data-continued"></a>관련된 데이터를 사용 하 여 작업을 계속

이전 자습서에서 사용 하기 시작 했을 `EntityDataSource` 관련 데이터로 작업 하는 컨트롤입니다. 여러 수준의 계층 구조를 표시 하 고 탐색 속성의 데이터를 편집 합니다. 이 자습서에 추가 하 고 관계를 삭제 하 고 기존 엔터티에 관계가 있는 새 엔터티를 추가 하 여 관련된 데이터를 사용 하 여 작업에 계속 있습니다.

부서에 할당 된 강좌를 추가 하는 페이지를 만들어야 합니다. 부서 이미 존재 하며 새 강의 만들 때 동시에에서는 관계를 설정 하 고 기존 부서 간에 합니다.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image1.png)

강사 강좌 (선택한 두 엔터티 간의 관계 추가)을 할당 하 여 다 대 다 관계를 사용 하는 페이지도 만듭니다 또는 강사 강좌에서 제거 (두 엔터티 간의 관계를 제거 했는지 선택)입니다. 데이터베이스에 추가 되 고 새 행에 결과 강사 및 강좌 간의 관계를 추가 합니다 `CourseInstructor` 연결 테이블, 관계에서 행을 삭제 하는 제거를 `CourseInstructor` 연결 테이블. 그러나 이렇게 하면 Entity Framework의를 참조 하지 않고 탐색 속성을 설정 하 여는 `CourseInstructor` 명시적으로 테이블입니다.

[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image3.png)

## <a name="adding-an-entity-with-a-relationship-to-an-existing-entity"></a>관계를 사용 하 여 엔터티를 기존 엔터티에 추가

라는 새 웹 페이지를 만듭니다 *CoursesAdd.aspx* 를 사용 하는 *Site.Master* 마스터 페이지, 다음 태그를 추가한 합니다 `Content` 라는 컨트롤 `Content2`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample1.aspx)]

이 태그를 만듭니다는 `EntityDataSource` 컨트롤 교육 코스를 선택 하는 수 있도록 하는 삽입에 대 한 처리기를 지정 하는 `Inserting` 이벤트입니다. 처리기를 사용 하 여 업데이트 합니다 `Department` 탐색 속성이 새 `Course` 엔터티가 만들어질 합니다.

태그 만들어지기를 `DetailsView` 컨트롤을 새로 추가 하는 데 `Course` 엔터티. 태그에 대해 바인딩된 필드를 사용 하 여 `Course` 엔터티 속성입니다. 입력 해야 합니다 `CourseID` 아니므로이 시스템에서 생성 된 ID 필드 값입니다. 대신 강좌 번호 과정 만들어질 때 수동으로 지정 해야 하는 것입니다.

에 대 한 서식 파일 필드를 사용 합니다 `Department` 탐색 속성 탐색 속성을 사용 하 여 사용할 수 없으므로 `BoundField` 컨트롤입니다. 템플릿 필드 부서를 선택 하려면 드롭다운 목록을 제공 합니다. 드롭다운 목록에 바인딩된 합니다 `Departments` 엔터티를 사용 하 여 집합 `Eval` 대신 `Bind`, 다시 업데이트 하기 위해 탐색 속성을 직접 바인딩할 수 없습니다 때문에 합니다. 에 대 한 처리기를 지정 합니다 `DropDownList` 컨트롤의 `Init` 이벤트를 업데이트 하는 코드에서 사용 하 여 컨트롤에 대 한 참조를 저장할 수 있도록는 `DepartmentID` 외래 키입니다.

*CoursesAdd.aspx.cs* partial 클래스 선언 바로 뒤 클래스 필드에 대 한 참조를 추가 하 여 `DepartmentsDropDownList` 제어:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample2.cs)]

에 대 한 처리기를 추가 합니다 `DepartmentsDropDownList` 컨트롤의 `Init` 이벤트 컨트롤에 대 한 참조를 저장할 수 있습니다. 이렇게 하면 사용자가 입력 값을 가져오고 업데이트 하기 위해 사용할 수 있습니다 합니다 `DepartmentID` 의 값을 `Course` 엔터티.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample3.cs)]

에 대 한 처리기를 추가 합니다 `DetailsView` 컨트롤의 `Inserting` 이벤트:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample4.cs)]

클릭할 때 `Insert`, `Inserting` 새 레코드를 삽입 하기 전에 이벤트가 발생 합니다. 처리기에서 코드를 가져옵니다를 `DepartmentID` 에서 `DropDownList` 컨트롤과에 사용할 값을 설정 하는 데 사용 합니다 `DepartmentID` 의 속성은 `Course` 엔터티.

이 과정을 추가 하는 Entity Framework을 고려 합니다 `Courses` 탐색 속성은 연결 된 `Department` 엔터티. 부서에도 추가 합니다 `Department` 의 탐색 속성은 `Course` 엔터티.

페이지를 실행 합니다.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image5.png)

ID, 제목, 크레딧 수를 입력 하 고 부서에 선택한 클릭 **삽입**합니다.

실행 합니다 *Courses.aspx* 페이지 및 새 강의를 동일한 부서를 선택 합니다.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-5/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image7.png)

## <a name="working-with-many-to-many-relationships"></a>다 대 다 관계 작업

관계는 `Courses` 엔터티 집합 및 `People` 엔터티 집합은 다 대 다 관계입니다. A `Course` 엔터티에 라는 탐색 속성이 포함 된 `People` 0 개 이상의 관련를 포함할 수 있는 `Person` 엔터티 (해당 과정을 설명 하는 할당 된 강사를 나타냄). 와 `Person` 엔터티에 라는 탐색 속성이 포함 된 `Courses` 0 개 이상의 관련를 포함할 수 있는 `Course` 엔터티 (과정을 나타내는 해당 강사에 게 할당 됩니다). 한 명의 강사 있습니다 여러 과정을 가르치고 여러 강사가 한 강좌를 수업 할 수 있습니다. 연습의이 섹션에서는 추가 하 고 간의 관계를 제거할 `Person` 고 `Course` 관련 엔터티의 탐색 속성을 업데이트 하 여 엔터티.

라는 새 웹 페이지를 만듭니다 *InstructorsCourses.aspx* 를 사용 하는 *Site.Master* 마스터 페이지, 다음 태그를 추가한 합니다 `Content` 라는 컨트롤 `Content2`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample5.aspx)]

이 태그를 만듭니다는 `EntityDataSource` 이름을 검색 하는 컨트롤 및 `PersonID` 의 `Person` 강사에 대 한 엔터티. A `DropDrownList` 컨트롤이 바인딩되는 `EntityDataSource` 제어 합니다. 합니다 `DropDownList` 컨트롤에 대 한 처리기를 지정 합니다 `DataBound` 이벤트입니다. 과정을 표시 하는 두 databind 드롭 다운 목록에이 처리기를 사용할 수 있습니다.

태그는 또한 선택된 된 강사에 강좌 할당 하는 데 사용할 컨트롤을 다음 그룹을 만듭니다.

- `DropDownList` 할당할 강좌를 선택 하는 컨트롤입니다. 이 컨트롤은 현재 선택된 된 강사에 할당 되지 않은 과정을 통해 채워집니다.
- `Button` 할당을 시작 하는 컨트롤입니다.
- `Label` 할당이 실패 하는 경우 오류 메시지를 표시 하는 컨트롤입니다.

마지막으로, 태그는 또한 컨트롤에서 선택된 된 강사 강좌를 제거 하는 데 그룹을 만듭니다.

*InstructorsCourses.aspx.cs*를 추가 하 여 문:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample6.cs)]

과정을 표시 하는 두 개의 드롭다운 목록을 채우는 메서드를 추가 합니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample7.cs)]

이 코드의 모든 과정을 가져옵니다는 `Courses` 엔터티 집합과의 과정을 가져옵니다는 `Courses` 의 탐색 속성을 `Person` 선택한 강사 엔터티. 그런 다음 해당 강사 강좌를 할당 하는 결정 하 고 그에 따라 드롭 다운 목록을 채웁니다.

에 대 한 처리기를 추가 합니다 `Assign` 단추의 `Click` 이벤트:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample8.cs)]

이 코드를 `Person` 선택된 된 강사에 대 한 엔터티를 가져옵니다를 `Course` 선택한 과정에 대 한 엔터티 선택된 된 강좌의 추가 합니다 `Courses` 강의의 탐색 속성 `Person` 엔터티. 그런 다음 데이터베이스에 변경 내용을 저장 하 고 결과 즉시 볼 수 있도록 드롭 다운 목록을 채웁니다.

에 대 한 처리기를 추가 합니다 `Remove` 단추의 `Click` 이벤트:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample9.cs)]

이 코드를 `Person` 선택된 된 강사에 대 한 엔터티를 가져옵니다를 `Course` 선택한 과정에 대 한 엔터티에서 선택한 과정을 제거 하 고는 `Person` 엔터티의 `Courses` 탐색 속성입니다. 그런 다음 데이터베이스에 변경 내용을 저장 하 고 결과 즉시 볼 수 있도록 드롭 다운 목록을 채웁니다.

코드를 추가 합니다 `Page_Load` 보고서에 대 한 처리기를 추가 하는 오류가 없는 경우 오류 메시지를 않았는지 확인 하는 메서드 표시 되지 않습니다 합니다 `DataBound` 및 `SelectedIndexChanged` 과정 드롭다운 목록을 채우는 데 강사 드롭다운 목록의 이벤트:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample10.cs)]

페이지를 실행 합니다.

[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image9.png)

강사를 선택 합니다. 합니다 <strong>강좌 할당</strong> 강사 설명 하지 않습니다 하는 과정을 표시 하는 드롭다운 목록 및 <strong>과정을 제거</strong> 드롭다운 목록에서 강사에 이미 할당 되어 있는 강의 표시 됩니다. 에 <strong>강좌 할당</strong> 섹션, 강좌를 선택 하 고, 클릭 <strong>할당</strong>합니다. 과정으로 이동 합니다 <strong>과정을 제거</strong> 드롭 다운 목록. 과정을 선택 합니다 <strong>제거 과정</strong> 섹션을 클릭 <strong>제거</strong><em>.</em> 과정으로 이동 합니다 <strong>강좌 할당</strong> 드롭 다운 목록.

관련 된 데이터로 작업 하는 몇 가지 방법은 살펴 보았습니다. 다음 자습서에서는 응용 프로그램의 관리 효율을 개선 하기 위해 데이터 모델에서 상속을 사용 하는 방법에 알아봅니다.

> [!div class="step-by-step"]
> [이전](the-entity-framework-and-aspnet-getting-started-part-4.md)
> [다음](the-entity-framework-and-aspnet-getting-started-part-6.md)
