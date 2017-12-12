---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
title: "먼저 Entity Framework 4.0 데이터베이스와 시작 및 ASP.NET 4 Web Forms-5 부 | Microsoft Docs"
author: tdykstra
description: "Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 샘플 응용 프로그램은..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/03/2010
ms.topic: article
ms.assetid: 24ad4379-3fb2-44dc-ba59-85fe0ffcb2ae
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
msc.type: authoredcontent
ms.openlocfilehash: 7200899d54585cd09e0a648e3aaaf839db2649e0
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-5"></a>먼저 Entity Framework 4.0 데이터베이스와 시작 및 ASP.NET 4 Web Forms-5 부
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

> Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 4.0 및 Visual Studio 2010을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대 한 정보를 참조 하세요. [시리즈의 첫 번째 자습서](the-entity-framework-and-aspnet-getting-started-part-1.md)


## <a name="working-with-related-data-continued"></a>데이터 관련된 작업을 계속

이전 자습서에서 사용 하기 시작는 `EntityDataSource` 관련 데이터로 작업 하는 컨트롤입니다. 프로젝트 관리자는 여러 수준의 계층을 표시 하 고이 정보를 탐색 속성의 데이터를 편집 합니다. 이 자습서에서는 계속 해 서 추가 하 고 관계를 삭제 하 고 기존 엔터티와 관계를 맺고 있는 새 엔터티를 추가 하 여 관련된 데이터와 함께 작동 하도록 합니다.

부서에 할당 된 과정을 추가 하는 페이지를 만들어야 합니다. 부서 이미 존재 하며, 새 과정을 만들 때 동시에 있습니다 수 간의 관계를 설정 하 고 기존 부서입니다.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image1.png)

또한 만들고 강사 (추가 선택 하는 두 엔터티 간의 관계) 과정을 할당 하 여 다 대 다 관계와 작동 하는 페이지 또는 강사 과정에서 제거 (두 엔터티 간의 관계를 제거 했는지 선택.) 새 행에 추가 되 고 데이터베이스에서 강사 및 일련 간의 관계 추가 됩니다는 `CourseInstructor` 연결 테이블; 제거 관계에서 행을 삭제 하는 `CourseInstructor` 연관 테이블입니다. 그러나 이렇게 하면 Entity framework에서를 참조 하지 않고 탐색 속성을 설정 하 여는 `CourseInstructor` 명시적으로 테이블입니다.

[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image3.png)

## <a name="adding-an-entity-with-a-relationship-to-an-existing-entity"></a>관계가 있는 엔터티를 기존 엔터티에 추가

라는 새 웹 페이지 생성 *CoursesAdd.aspx* 를 사용 하는 *Site.Master* 마스터 페이지, 다음 태그를 추가 하 고는 `Content` 라는 컨트롤 `Content2`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample1.aspx)]

이 태그를 만듭니다는 `EntityDataSource` 컨트롤을 선택 하는 과정을를 삽입할 수 있도록 하 고에 대 한 처리기를 지정 하는 `Inserting` 이벤트입니다. 사용 하 여 처리기 업데이트는 `Department` 새 탐색 속성 `Course` 엔터티에 합니다.

태그를 만듭니다는 `DetailsView` 새로 추가에 사용할 컨트롤 `Course` 엔터티. 에 대 한 바인딩된 필드를 사용 하는 태그 `Course` 엔터티 속성입니다. 입력 해야 하는 `CourseID` 아니므로이 시스템에서 생성 된 ID 필드 값입니다. 만으로도 과정을 만들 때 수동으로 지정 해야 하는 과정 번호입니다.

에 대 한 서식 파일 필드를 사용 하는 `Department` 탐색 속성으로 탐색 속성을 사용할 수 없으므로 `BoundField` 컨트롤입니다. 서식 파일 필드 부서를 선택 하려면 드롭다운 목록이 표시 됩니다. 드롭다운 목록에 바인딩된는 `Departments` 엔터티를 사용 하 여 집합 `Eval` 대신 `Bind`, 다시 이므로 탐색 속성을 업데이트 하려면 직접 바인딩할 수 없습니다. 에 대 한 처리기를 지정 하면는 `DropDownList` 컨트롤의 `Init` 이벤트를 업데이트 하는 코드에서 사용할 컨트롤에 대 한 참조를 저장할 수 있도록는 `DepartmentID` 외래 키입니다.

*CoursesAdd.aspx.cs* partial 클래스 선언 바로 뒤 클래스 필드에 대 한 참조를 추가 하는 `DepartmentsDropDownList` 제어:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample2.cs)]

에 대 한 처리기를 추가 `DepartmentsDropDownList` 컨트롤의 `Init` 이벤트 컨트롤에 대 한 참조를 저장할 수 있도록 합니다. 이렇게 하면 사용자가 입력 값을 가져오고 업데이트 하는 데 사용할 수 있습니다는 `DepartmentID` 의 값은 `Course` 엔터티.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample3.cs)]

에 대 한 처리기를 추가 `DetailsView` 컨트롤의 `Inserting` 이벤트:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample4.cs)]

사용자가 클릭할 때 `Insert`, `Inserting` 이벤트는 새 레코드를 삽입 하기 전에 발생 합니다. 처리기의 코드를 가져옵니다는 `DepartmentID` 에서 `DropDownList` 제어 하 고 사용 하 여에 사용할 값을 설정 하는 `DepartmentID` 의 속성은 `Course` 엔터티.

이 과정에이 참여를 추가 하므로 Entity Framework는 `Courses` 탐색 속성은 연결 된 `Department` 엔터티. 또한 추가 하 고 부서는 `Department` 의 탐색 속성은 `Course` 엔터티.

페이지를 실행 합니다.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image5.png)

ID, 제목, 다양 한 크레딧, 입력 한 부서를 선택한 다음 클릭 **삽입**합니다.

실행 된 *Courses.aspx* 페이지 하 고 새 과정을 보려면 같은 동일 부서를 선택 합니다.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-5/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image7.png)

## <a name="working-with-many-to-many-relationships"></a>다 대 다 관계 작업

간의 관계는 `Courses` 엔터티 집합 및 `People` 엔터티 집합은 다 대 다 관계입니다. A `Course` 엔터티 탐색 라는 속성이 `People` 0 개 이상의 관련 포함 될 수 있는 `Person` 엔터티 (해당 과정에 지정할 할당 강사를 나타냄). 및 `Person` 엔터티 탐색 라는 속성이 `Courses` 0 개 이상의 관련 포함 될 수 있는 `Course` 엔터티 (해당 강사에 게 할당 된 과정을 나타냄). 하나의 강사 여러 과정에 지정할 수 있습니다 및 한 과정으로 여러 강사 뿐만 아니라 수 있습니다. 이 연습 섹션에서는 추가 하 고 간의 관계를 제거할 `Person` 및 `Course` 관련 엔터티의 탐색 속성을 업데이트 하 여 엔터티.

라는 새 웹 페이지 생성 *InstructorsCourses.aspx* 를 사용 하는 *Site.Master* 마스터 페이지, 다음 태그를 추가 하 고는 `Content` 라는 컨트롤 `Content2`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample5.aspx)]

이 태그를 만듭니다는 `EntityDataSource` 이름을 검색 하는 컨트롤 및 `PersonID` 의 `Person` 강사에 게 엔터티. A `DropDrownList` 컨트롤이 바인딩되는 `EntityDataSource` 제어 합니다. `DropDownList` 컨트롤에 대 한 처리기를 지정 된 `DataBound` 이벤트입니다. 과정을 표시 하는 두 개의 databind 드롭 다운 목록에이 처리기를 사용 합니다.

태그는 또한 과정 선택한 강사를 할당 하는 데 사용할 수 있는 컨트롤의 다음 그룹을 만듭니다.

- A `DropDownList` 할당 하는 과정을 선택 하기 위한 제어 합니다. 이 컨트롤은 선택한 강사에 현재 할당 되지 않은 과정으로 채워집니다.
- A `Button` 할당을 시작 하는 컨트롤입니다.
- A `Label` 컨트롤에는 할당은 실패 하는 경우 오류 메시지가 표시 됩니다.

마지막으로, 태그는 또한 선택한 강사에서 제거 하는 과정에 대해 사용할 수 있는 컨트롤의 그룹을 만듭니다.

*InstructorsCourses.aspx.cs*를 사용 하는 추가 문:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample6.cs)]

과정을 표시 하는 두 드롭다운 목록을 채우는 데 사용 하는 메서드를 추가 합니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample7.cs)]

이 코드는 모든 과정에서 가져옵니다는 `Courses` 엔터티 집합과 과정을 가져옵니다는 `Courses` 의 탐색 속성은 `Person` 선택한 강사에 대 한 엔터티. 그런 다음 해당 강사에 할당 되는 과정을 결정 하 고 그에 따라 드롭 다운 목록을 채웁니다.

에 대 한 처리기를 추가 `Assign` 단추의 `Click` 이벤트:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample8.cs)]

이 코드는 `Person` 선택한 강사에 대 한 엔터티를 가져옵니다는 `Course` 선택한 과정에 대 한 엔터티 추가 선택 된 과정에 참여 하는 `Courses` 강의의 탐색 속성 `Person` 엔터티. 다음 데이터베이스에 변경 내용을 저장 하 고 결과 즉시 볼 수 있도록 드롭 다운 목록을 다시 채웁니다.

에 대 한 처리기를 추가 `Remove` 단추의 `Click` 이벤트:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample9.cs)]

이 코드는 `Person` 선택한 강사에 대 한 엔터티를 가져옵니다는 `Course` 선택한 과정에 대 한 엔터티 선택한 과정에서 제거 하 고는 `Person` 엔터티의 `Courses` 탐색 속성입니다. 다음 데이터베이스에 변경 내용을 저장 하 고 결과 즉시 볼 수 있도록 드롭 다운 목록을 다시 채웁니다.

코드를 추가 하는 `Page_Load` 없음 오류를 보고에 대 한 처리기를 추가 하는 메서드를 사용 하면 오류 메시지가 표시 되지 않습니다는 `DataBound` 및 `SelectedIndexChanged` courses 드롭 다운 목록을 채우는 데 강사 드롭 다운 목록의 이벤트:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample10.cs)]

페이지를 실행 합니다.

[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image9.png)

강사를 선택 합니다. **과정 할당** 드롭다운 목록에서 강사 설명 하지 않는 하는 강의 표시 됩니다 및 **제거 과정** 드롭다운 목록에서 강사에 이미 할당 되어 있는 강의 표시 됩니다. 에 **과정 할당** 섹션 과정을 선택한 다음 클릭 **할당**합니다. 과정을 이동는 **제거 과정** 드롭 다운 목록입니다. 과정 선택는 **제거 과정** 섹션 및 클릭 **제거***합니다.* 과정을 이동는 **과정 할당** 드롭 다운 목록입니다.

관련된 데이터에 사용할 수 있는 몇 가지 다른 방법을 살펴 보았습니다. 다음 자습서에서는 응용 프로그램의 관리 효율을 개선 하기 위해 데이터 모델에서 상속을 사용 하는 방법을 설명 합니다.

>[!div class="step-by-step"]
[이전](the-entity-framework-and-aspnet-getting-started-part-4.md)
[다음](the-entity-framework-and-aspnet-getting-started-part-6.md)
