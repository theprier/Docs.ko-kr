---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-7
title: 먼저 Entity Framework 4.0 데이터베이스와 시작 및 ASP.NET 4 Web Forms-7 부 | Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 샘플 응용 프로그램은...
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/03/2010
ms.topic: article
ms.assetid: f8afb245-b705-419c-8790-0b295e90d5e2
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-7
msc.type: authoredcontent
ms.openlocfilehash: cb84f4f3e130fedb3e2f1a17d630767ff65bfa05
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30886981"
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-7"></a>먼저 Entity Framework 4.0 데이터베이스와 시작 및 ASP.NET 4 Web Forms-7 부
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

> Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 4.0 및 Visual Studio 2010을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대 한 정보를 참조 하세요. [시리즈의 첫 번째 자습서](the-entity-framework-and-aspnet-getting-started-part-1.md)


## <a name="using-stored-procedures"></a>저장 프로시저 사용

이전 자습서에서 계층당 하나의 테이블 상속 패턴을 구현 합니다. 이 자습서에서는 데이터베이스 액세스를 제어 권한을 얻으려고 저장된 프로시저를 사용 하는 방법을 보여줍니다.

Entity Framework를 사용 하면 데이터베이스 액세스를 위한 저장된 프로시저를 사용 해야 것을 지정할 수 있습니다. 모든 엔터티 형식에 대 한 만들기, 업데이트 또는 해당 형식의 엔터티를 삭제 하는 중에 사용할 저장된 프로시저를 지정할 수 있습니다. 그런 다음 데이터 모델의 엔터티 집합을 검색 하는 등 작업을 수행 하는 데 사용할 수 있는 저장된 프로시저에 대 한 참조를 추가할 수 있습니다.

저장된 프로시저를 사용 하 여 데이터베이스 액세스에 대 한 일반적인 요구 사항입니다. 일부 경우에는 데이터베이스 관리자가 데이터베이스에 대 한 모든 액세스 보안상의 이유로 저장된 프로시저를 통과 필요할 수 있습니다. 다른 경우에는 일부 데이터베이스를 업데이트 하는 엔터티 프레임 워크에서 사용 하는 프로세스에 비즈니스 논리를 작성 하는 것이 좋습니다. 예를 들어 엔터티 삭제 될 때마다 보관 데이터베이스를 복사 하는 것이 좋습니다. 또는 행이 업데이트 될 때마다 기록 변경 내용을 적용 하는 로깅 테이블에 행을 작성 수 있습니다. Entity Framework는 엔터티를 삭제 또는 엔터티를 업데이트 될 때마다 호출 되는 저장된 프로시저에서 이러한 종류의 작업을 수행할 수 있습니다.

이전 자습서에서와 같이 하지 새 페이지를 만듭니다. 대신, Entity Framework 이미 만든 페이지 중 일부에 대해 데이터베이스에 액세스 하는 방법을 변경 합니다.

이 자습서에서는 삽입에 대 한 데이터베이스의 저장된 프로시저를 만듭니다 `Student` 및 `Instructor` 엔터티. 데이터 모델에 추가 합니다 및 Entity Framework 사용 해야 함을 추가 하는 데 지정 합니다 `Student` 및 `Instructor` 엔터티가 데이터베이스에 있습니다. 검색 하는 데 사용할 수 있는 저장된 프로시저 또한 만들어 `Course` 엔터티.

## <a name="creating-stored-procedures-in-the-database"></a>데이터베이스에 저장된 프로시저 만들기

(사용 중인 경우는 *School.mdf* 파일이이 자습서와 함께 다운로드할 수 있는 프로젝트에서이 단원을 건너뛸 수 있습니다이 저장된 프로시저가 이미 존재 하므로.)

**서버 탐색기**, 확장 *School.mdf*를 마우스 오른쪽 단추로 클릭 **저장 프로시저**를 선택 하 고 **새 저장 프로시저 추가**합니다.

[![image15](the-entity-framework-and-aspnet-getting-started-part-7/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image1.png)

다음 SQL 문을 복사 하 고 저장된 프로시저 창에 붙여 기초 저장된 프로시저를 대체 합니다.

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample1.sql)]

[![image14](the-entity-framework-and-aspnet-getting-started-part-7/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image3.png)

`Student` 엔터티는 4 개의 속성: `PersonID`, `LastName`, `FirstName`, 및 `EnrollmentDate`합니다. 데이터베이스에서 ID 값을 자동으로 생성 및 저장된 프로시저는 다른 세 개에 대 한 매개 변수를 허용 합니다. 저장된 프로시저를 Entity Framework의 추적할 수 있는 메모리에 유지 된 엔터티 버전에서 새 행의 레코드 키의 값을 반환 합니다.

저장 하 고 저장된 프로시저 창을 닫습니다.

만들기는 `InsertInstructor` 다음 SQL 문을 사용 하 여 동일한 방식으로 저장 프로시저:

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample2.sql)]

만들 `Update` 저장 프로시저에 대 한 `Student` 및 `Instructor` 엔터티도 합니다. (데이터베이스에 이미는 `DeletePerson` 저장 프로시저 모두에 `Instructor` 및 `Student` 엔터티.)

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample3.sql)]

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample4.sql)]

이 자습서에서는 각 엔터티 형식에 대 한 모든 세 함수를-예: insert, update 및 delete-매핑합니다. Entity Framework 버전 4 하나만 매핑할 수 있습니다. 또는 저장된 프로시저에는 다른 예외적으로 매핑하지 않고 함수 중 두 가지: Entity Framework에서 예외를 throw 합니다 업데이트 함수 하지만 삭제 기능이 아니라에 매핑할 경우 때 있습니다 엔터티를 삭제 하려고 시도 합니다. Entity Framework 버전 3.5에서에서 하지 않은 저장된 프로시저 매핑에 처럼 많은 유연성: 있습니다 함수가 두 개를 매핑한 경우 세 가지 모두에 매핑할 필요 했습니다.

데이터를 업데이트 하는 대신 표시 하는 저장된 프로시저를 만들려면 모든 선택 하나를 만들 `Course` 엔터티를 다음 SQL 문을 사용 하 여:

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample5.sql)]

## <a name="adding-the-stored-procedures-to-the-data-model"></a>데이터 모델에 저장된 프로시저에 추가

저장된 프로시저는 데이터베이스에 정의 되기 하지만 Entity Framework에 사용할 수 있도록 하 여 데이터 모델에 추가 해야 합니다. 열기 *SchoolModel.edmx*디자인 화면을 마우스 오른쪽 단추로 클릭 하 고 선택 **데이터베이스에서 모델 업데이트**합니다. 에 **추가** 탭은 **데이터베이스 개체 선택** 대화 상자에서 **Stored Procedures**, 새로 만든된 저장된 프로시저를 선택 및 `DeletePerson` 저장 프로시저를 클릭 하 고 **마침**합니다.

[![image20](the-entity-framework-and-aspnet-getting-started-part-7/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image5.png)

## <a name="mapping-the-stored-procedures"></a>저장된 프로시저 매핑

데이터 모델 디자이너에서 마우스 오른쪽 단추로 클릭는 `Student` 엔터티와 선택 **저장 프로시저 매핑**합니다.

[![image21](the-entity-framework-and-aspnet-getting-started-part-7/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image7.png)

**매핑 정보** Entity Framework는 삽입, 업데이트 및 이러한 종류의 엔터티를 삭제에 사용 해야 하는 저장된 프로시저를 지정할 수 있는 창이 나타납니다.

[![image22](the-entity-framework-and-aspnet-getting-started-part-7/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image9.png)

설정의 **삽입** 함수를 **InsertStudent**합니다. 창에는 엔터티 속성에 매핑되어 있어야 하며 각 저장된 프로시저 매개 변수 목록이 표시 됩니다. 이러한 두가 자동으로 매핑되어야 이름이 같기 때문에 있습니다. 라는 엔터티 속성이 없기 `FirstName`수동으로 선택 해야 하므로 `FirstMidName` 사용 가능한 엔터티 속성을 표시 하는 드롭다운 목록에서 합니다. (의 이름이 변경 때문에 이것이 `FirstName` 속성을 `FirstMidName` 첫 번째 자습서에서.)

[![image23](the-entity-framework-and-aspnet-getting-started-part-7/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image11.png)

동일한 **매핑 정보** 창, 맵은 `Update` 함수를 `UpdateStudent` 저장 프로시저 (지정 했는지 확인 `FirstMidName` 에 대 한 매개 변수 값으로 `FirstName`의 경우와 달리는 `Insert` 저장 프로시저) 및 `Delete` 함수를 `DeletePerson` 저장 프로시저입니다.

[![image01](the-entity-framework-and-aspnet-getting-started-part-7/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image13.png)

강사에 대 한 저장 프로시저 insert, update 및 delete 매핑할 동일한 절차에 따라는 `Instructor` 엔터티.

[![image02](the-entity-framework-and-aspnet-getting-started-part-7/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image15.png)

데이터 업데이트 하는 대신 읽을 하는 저장 프로시저를 사용 하는 **모델 브라우저** 엔터티에 저장된 프로시저를 매핑할 창 입력 반환 합니다. 데이터 모델 디자이너에서 디자인 화면 및 선택 마우스 오른쪽 단추로 클릭 **모델 브라우저**합니다. 열기는 **SchoolModel.Store** 노드를 연 후는 **Stored Procedures** 노드. 마우스 오른쪽 단추로 클릭 한 다음는 `GetCourses` 저장 프로시저 및 선택 **함수 가져오기 추가**합니다.

[![image24](the-entity-framework-and-aspnet-getting-started-part-7/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image17.png)

에 **함수 가져오기 추가** 대화 상자의 **반환 된 컬렉션의** 선택 **엔터티**, 선택한 후 `Course` 엔터티 형식으로 반환 합니다. 완료 되 면 클릭 **확인**합니다. 저장 하 고 닫습니다는 *.edmx* 파일입니다.

[![image25](the-entity-framework-and-aspnet-getting-started-part-7/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image19.png)

## <a name="using-insert-update-and-delete-stored-procedures"></a>Insert를 사용 하 여, Update 및 Delete 저장된 프로시저

저장된 프로시저를 삽입, 업데이트 및 데이터를 삭제 후에 사용 되는 Entity Framework에서 자동으로 데이터 모델에이 추가 하 고 적절 한 엔터티에 매핑됩니다. 이제 실행할 수 있습니다는 *StudentsAdd.aspx* 페이지, Entity Framework에서 사용 하 여 새 학생을 만들 때마다는 `InsertStudent` 저장 프로시저에 새 행을 추가 하는 `Student` 테이블입니다.

[![image03](the-entity-framework-and-aspnet-getting-started-part-7/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image21.png)

실행 된 *Students.aspx* 페이지와 새 학생 목록에 나타납니다.

[![image04](the-entity-framework-and-aspnet-getting-started-part-7/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image23.png)

Update 함수 작동 하는지 확인 하려면 이름을 변경 하 고 삭제 기능 작동 하는지 확인 하려면 학생을 삭제 합니다.

[![image05](the-entity-framework-and-aspnet-getting-started-part-7/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image25.png)

## <a name="using-select-stored-procedures"></a>Select 저장된 프로시저를 사용 하 여

Entity Framework가 자동으로 실행 되지 저장된 프로시저와 같은 `GetCourses`를 사용 하 여 사용할 수 없는 `EntityDataSource` 제어 합니다. 를 사용 하려면 해당 코드에서 호출 합니다.

열기는 *InstructorsCourses.aspx.cs* 파일입니다. `PopulateDropDownLists` 메서드 LINQ-엔터티 쿼리를 사용 하 여 목록을 반복 하 고 강사에 할당 되는 기능과 및 알림을 할당을 확인 수 있도록 모든 과정 엔터티를 검색 합니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample6.cs)]

이 다음 코드로 바꿉니다.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample7.cs)]

페이지 사용 하 여 이제는 `GetCourses` 모든 과정의 목록을 검색 하는 프로시저를 저장 합니다. 이전 처럼 작동 하는지 확인 하려면 페이지를 실행 합니다.

(저장된 프로시저에 의해 검색 되는 엔터티의 탐색 속성 하지 자동으로 채워질 수에 따라 이러한 엔터티와 관련 된 데이터 `ObjectContext` 기본 설정 합니다. 자세한 내용은 참조 [관련 개체 로드](https://msdn.microsoft.com/library/bb896272.aspx) MSDN 라이브러리에서.)

다음 자습서에서 프로그램 및 테스트 데이터 서식 및 유효성 검사 규칙을 쉽게 수행할 수 있도록 Dynamic Data 기능을 사용 하는 방법을 설명 합니다. 데이터 형식 문자열 등의 각 웹 페이지 규칙 및는 필드는 필수 여부를 지정 하지 않고 데이터 모델 메타 데이터에 이러한 규칙을 지정할 수 있습니다 및 모든 페이지에 자동으로 적용 합니다.

> [!div class="step-by-step"]
> [이전](the-entity-framework-and-aspnet-getting-started-part-6.md)
> [다음](the-entity-framework-and-aspnet-getting-started-part-8.md)
