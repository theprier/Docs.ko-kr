---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-7
title: 먼저 Entity Framework 4.0 Database를 사용 하 여 시작 및 ASP.NET 4 Web Forms-7 부 | Microsoft Docs
author: tdykstra
description: Contoso University 샘플 웹 응용 프로그램에는 Entity Framework를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 샘플 응용 프로그램은...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: f8afb245-b705-419c-8790-0b295e90d5e2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-7
msc.type: authoredcontent
ms.openlocfilehash: 48092838ac0b00137ae0a4e37391c31883afcd09
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824110"
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-7"></a>먼저 Entity Framework 4.0 Database를 사용 하 여 시작 및 ASP.NET 4 Web Forms-7 부
====================
[Tom Dykstra](https://github.com/tdykstra)

> Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 4.0 및 Visual Studio 2010을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대 한 정보를 참조 하세요. [시리즈의 첫 번째 자습서](the-entity-framework-and-aspnet-getting-started-part-1.md)


## <a name="using-stored-procedures"></a>저장 프로시저 사용

이전 자습서에서 계층당 하나의 테이블 상속 패턴을 구현 했습니다. 이 자습서에서는 저장된 프로시저를 사용 하 여 데이터베이스에 대 한 액세스를 더 잘 제어 하는 방법을 보여줍니다.

Entity Framework를 사용 하면 데이터베이스 액세스를 위한 저장된 프로시저를 사용 하도록 지정할 수 있습니다. 모든 엔터티 형식에 대 한 만들기, 업데이트 또는 해당 형식의 엔터티를 삭제 하는 데 저장된 프로시저를 지정할 수 있습니다. 그런 다음 데이터 모델의 엔터티 집합을 검색 하는 등 작업을 수행 하는 데 사용할 수 있는 저장된 프로시저에 대 한 참조를 추가할 수 있습니다.

저장된 프로시저를 사용 하 여 데이터베이스 액세스에 대 한 일반적인 요구 사항은 됩니다. 일부 경우에서 데이터베이스 관리자는 데이터베이스에 대 한 모든 액세스 보안을 위해 저장된 프로시저를 통과 필요할 수 있습니다. 다른 경우에는 일부 데이터베이스를 업데이트할 때 Entity Framework를 사용 하는 프로세스에 비즈니스 논리를 작성 하는 것이 좋습니다. 예를 들어, 엔터티가 삭제 될 때마다 보관 데이터베이스에 복사 하는 것이 좋습니다. 또는 행이 업데이트 될 때마다 변경을 수행한 기록 로깅 테이블에 행을 쓰기 위해 수도 있습니다. Entity Framework는 엔터티를 삭제 또는 엔터티를 업데이트 될 때마다 호출 되는 저장된 프로시저에서 이러한 종류의 작업을 수행할 수 있습니다.

이전 자습서와 같이 되지 모든 새 페이지를 만들어야 합니다. 대신, Entity Framework의 일부를 이미 만든 페이지에 대 한 데이터베이스에 액세스 하는 방식으로 변경 합니다.

이 자습서를 삽입 하기 위한 데이터베이스의 저장된 프로시저를 만듭니다 `Student` 고 `Instructor` 엔터티. 데이터 모델에 추가할 수 있습니다 및 Entity Framework 사용 해야 함을 추가 하기 위한 지정 `Student` 고 `Instructor` 데이터베이스로 엔터티. 검색 하는 데 사용할 수 있는 저장된 프로시저도 만듭니다 `Course` 엔터티.

## <a name="creating-stored-procedures-in-the-database"></a>데이터베이스의 저장된 프로시저 만들기

(사용 하는 경우는 *School.mdf* 파일에서이 자습서를 사용 하 여 다운로드할 수 있는 프로젝트를 건너뛸 수 있습니다이 섹션에서는 저장된 프로시저가 이미 존재 하므로.)

**서버 탐색기**, 확장 *School.mdf*를 마우스 오른쪽 단추로 클릭 **Stored Procedures**를 선택한 **새 저장 프로시저 추가**합니다.

[![image15](the-entity-framework-and-aspnet-getting-started-part-7/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image1.png)

다음 SQL 문을 복사 및 저장된 프로시저 창에 붙여넣고 스 켈 레 톤 저장된 프로시저를 대체 합니다.

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample1.sql)]

[![image14](the-entity-framework-and-aspnet-getting-started-part-7/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image3.png)

`Student` 엔터티는 4 개의 속성: `PersonID`, `LastName`를 `FirstName`, 및 `EnrollmentDate`합니다. 데이터베이스 ID 값을 자동으로 생성 하 고 저장된 프로시저가 다른 3 개에 대 한 매개 변수를 허용 합니다. 저장된 프로시저는 Entity Framework를 추적할 수 있는 메모리에 유지 하는 해당 엔터티의 버전에서 새 행의 레코드 키의 값을 반환 합니다.

저장 하 고 저장된 프로시저 창을 닫습니다.

만들기는 `InsertInstructor` 다음 SQL 문을 사용 하 여 동일한 방식으로 저장 프로시저:

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample2.sql)]

만들 `Update` 저장 프로시저에 대 한 `Student` 고 `Instructor` 엔터티도 합니다. (이미 데이터베이스를 `DeletePerson` 저장 프로시저 모두에 대해 작동 하는 `Instructor` 및 `Student` 엔터티.)

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample3.sql)]

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample4.sql)]

이 자습서에서는 세 함수를 모두-insert, update 및 delete-각 엔터티 형식에 매핑합니다. Entity Framework 버전 4 통해 하 하나만 매핑할 수 있습니다. 또는이 중 두 가지 예외를 사용 하 여 다른 매핑 없이 저장된 프로시저에 함수: 업데이트 함수가 있지만 not delete 함수를 매핑하는 경우 Entity Framework는 예외가 발생 하면 있습니다 엔터티를 삭제 하려고 시도 합니다. Entity Framework 버전 3.5에에서 없는 저장된 프로시저 매핑에 훨씬 유연 하 게: 함수 중 하나를 매핑한 경우 세 가지 모두에 매핑할 필요 합니다.

데이터를 업데이트 하는 것이 아니라 읽기를 제공 하는 저장된 프로시저를 만들려면 모든 선택 하 게 하나를 만들 `Course` 엔터티를 다음 SQL 문을 사용 하 여:

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample5.sql)]

## <a name="adding-the-stored-procedures-to-the-data-model"></a>데이터 모델에 저장된 프로시저를 추가합니다.

저장된 프로시저를 데이터베이스에 정의 된 하지만 Entity Framework를 사용할 수 있게 하려면 데이터 모델에 추가 해야 합니다. 오픈 *SchoolModel.edmx*, 디자인 화면을 마우스 오른쪽 단추로 **데이터베이스에서 모델 업데이트**합니다. 에 **추가** 탭의 **데이터베이스 개체 선택** 대화 상자에서 **저장 프로시저**, 새로 만든된 저장된 프로시저를 선택 및 `DeletePerson` 저장 프로시저 및 클릭 **완료**합니다.

[![image20](the-entity-framework-and-aspnet-getting-started-part-7/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image5.png)

## <a name="mapping-the-stored-procedures"></a>저장된 프로시저 매핑

데이터 모델 디자이너에서 마우스 오른쪽 단추로 클릭 합니다 `Student` 엔터티 및 선택 **저장 프로시저 매핑**합니다.

[![image21](the-entity-framework-and-aspnet-getting-started-part-7/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image7.png)

합니다 **매핑 정보** 삽입, 업데이트 및 이러한 종류의 엔터티를 삭제 하는 것에 대 한 Entity Framework 사용 해야 하는 저장된 프로시저를 지정할 수 있는 창이 나타납니다.

[![image22](the-entity-framework-and-aspnet-getting-started-part-7/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image9.png)

설정 된 **삽입** 함수를 **InsertStudent**합니다. 창에는 각 엔터티 속성에 매핑해야 저장된 프로시저 매개 변수 목록을 보여 줍니다. 이 중 두 가지는 자동으로 매핑될 이름이 같기 때문에 합니다. 라는 엔터티 속성이 없기 `FirstName`수동으로 선택 해야 하므로 `FirstMidName` 사용 가능한 엔터티 속성을 보여 주는 드롭다운 목록에서. (의 이름 변경 때문에 이것이 합니다 `FirstName` 속성을 `FirstMidName` 첫 번째 자습서에서입니다.)

[![image23](the-entity-framework-and-aspnet-getting-started-part-7/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image11.png)

동일한 **매핑 정보** 창, 맵 합니다 `Update` 함수를 `UpdateStudent` 저장 프로시저 (지정 해야 `FirstMidName` 매개 변수 값으로 `FirstName`에 대해 수행한 것 처럼는 `Insert` 저장 프로시저) 및 `Delete` 함수는 `DeletePerson` 저장 프로시저입니다.

[![image01](the-entity-framework-and-aspnet-getting-started-part-7/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image13.png)

수행 하는 강사에 대 한 저장 프로시저 insert, update 및 delete 매핑할 동일한 절차를 `Instructor` 엔터티.

[![image02](the-entity-framework-and-aspnet-getting-started-part-7/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image15.png)

데이터 업데이트 하는 대신 읽기는 저장 프로시저를 사용 합니다 **Model 브라우저** 저장된 프로시저를 엔터티에 매핑할 창 입력 반환 합니다. 데이터 모델 디자이너에서 디자인 화면을 마우스 오른쪽 단추로 **Model 브라우저**합니다. 엽니다는 **SchoolModel.Store** 노드 연 다음 합니다 **Stored Procedures** 노드. 마우스 오른쪽 단추로 클릭 합니다 `GetCourses` 저장 프로시저 및 선택 **Function Import 추가**합니다.

[![image24](the-entity-framework-and-aspnet-getting-started-part-7/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image17.png)

에 **Function Import 추가** 대화 상자의 **반환 된 컬렉션의** 선택 **엔터티**를 선택한 `Course` 엔터티 유형으로 반환 합니다. 완료 되 면 **확인**합니다. 저장 후 닫기 합니다 *.edmx* 파일입니다.

[![image25](the-entity-framework-and-aspnet-getting-started-part-7/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image19.png)

## <a name="using-insert-update-and-delete-stored-procedures"></a>업데이트 및 Delete 저장된 프로시저 Insert 사용

저장된 프로시저를 삽입, 업데이트 및 데이터를 삭제 합니다. 데이터 모델에 추가 하 고 적절 한 엔터티를 매핑할 해당 후 자동으로 Entity Framework에서 사용 됩니다. 이제 실행할 수 있습니다는 *StudentsAdd.aspx* 페이지에서 Entity Framework를 사용 하 여 새 학생을 만들 때마다를 `InsertStudent` 저장 프로시저에 새 행을 추가 하는 `Student` 테이블.

[![image03](the-entity-framework-and-aspnet-getting-started-part-7/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image21.png)

실행 합니다 *Students.aspx* 페이지와 새 학생 목록에 나타납니다.

[![image04](the-entity-framework-and-aspnet-getting-started-part-7/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image23.png)

업데이트 함수가 작동 하는지 확인 하려면 이름을 변경 하 고 delete 함수가 작동 하는지 확인 하려면 학생을 삭제 합니다.

[![image05](the-entity-framework-and-aspnet-getting-started-part-7/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image25.png)

## <a name="using-select-stored-procedures"></a>Select 저장된 프로시저를 사용 하 여

Entity Framework는 자동으로 실행 되지 저장된 프로시저와 같은 `GetCourses`를 사용 하 여 사용할 수 없습니다는 `EntityDataSource` 제어 합니다. 이 사용 하려면 해당 코드에서 호출 합니다.

엽니다는 *InstructorsCourses.aspx.cs* 파일입니다. `PopulateDropDownLists` 메서드는 LINQ-엔터티 쿼리를 사용 하 여 해당 목록을 반복 하 고 강사에 할당 되는 시나리오와는 할당 되지 않은 확인할 수 있도록 모든 강좌 엔터티를 검색 합니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample6.cs)]

이 다음 코드로 바꿉니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample7.cs)]

페이지를 사용 하 여 이제는 `GetCourses` 모든 과정 목록을 검색 하는 절차를 저장 합니다. 이전 처럼 작동 하는지 확인 하려면 페이지를 실행 합니다.

(저장된 프로시저에 의해 검색 되는 엔터티의 탐색 속성 수 자동으로 채워지지 않습니다에 따라 해당 엔터티를 관련 된 데이터를 사용 하 여 `ObjectContext` 기본 설정 합니다. 자세한 내용은 [관련 개체 로드](https://msdn.microsoft.com/library/bb896272.aspx) MSDN 라이브러리에서.)

다음 자습서에서는 Dynamic Data 기능을 사용 하 여 프로그램 및 테스트 데이터 서식 지정 및 유효성 검사 규칙을 쉽게 수행할 수 있도록 하는 방법에 알아봅니다. 데이터 형식 문자열 등의 각 웹 페이지 규칙 및 필수 필드를 여부를 지정 하는 대신 데이터 모델 메타 데이터에서 이러한 규칙을 지정할 수 있습니다 하 고 모든 페이지에 자동으로 적용 되는 합니다.

> [!div class="step-by-step"]
> [이전](the-entity-framework-and-aspnet-getting-started-part-6.md)
> [다음](the-entity-framework-and-aspnet-getting-started-part-8.md)
