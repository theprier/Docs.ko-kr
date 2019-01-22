---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: '템플릿: ASP.NET MVC 5 앱에서 EF 사용 하 여 상속을 구현 합니다.'
description: 이 자습서에서는 데이터 모델에서 상속을 구현하는 방법을 보여 줍니다.
author: tdykstra
ms.author: riande
ms.date: 01/21/2019
ms.topic: tutorial
ms.assetid: 08834147-77ec-454a-bb7a-d931d2a40dab
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: df8715e4416ce3ccdf1d9e380addcded553d85f8
ms.sourcegitcommit: 728f4e47be91e1c87bb7c0041734191b5f5c6da3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/22/2019
ms.locfileid: "54444287"
---
# <a name="template-implement-inheritance-with-ef-in-an-aspnet-mvc-5-app"></a>템플릿: ASP.NET MVC 5 앱에서 EF 사용 하 여 상속을 구현 합니다.

이전 자습서에서 동시성 예외를 처리 합니다. 이 자습서에서는 데이터 모델에서 상속을 구현하는 방법을 보여 줍니다.

개체 지향 프로그래밍에서 사용할 수 있습니다 [상속](http://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming)) 용이 하 게 [코드 재사용](http://en.wikipedia.org/wiki/Code_reuse)합니다. 이 자습서에서는 강사와 학생 모두에게 공통적인 속성(예: `LastName`)이 포함된 `Person` 기본 클래스에서 클래스가 파생되도록 `Instructor` 및 `Student` 클래스를 변경합니다. 웹 페이지를 추가하거나 변경하지는 않지만 일부 코드를 변경하고 이러한 변경 내용이 데이터베이스에 자동으로 반영됩니다.

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * 데이터베이스에 상속 매핑 방법
> * Person 클래스 만들기
> * 업데이트 Instructor 및 Student
> * 모델에 사용자 추가
> * 만들고 마이그레이션 업데이트
> * 구현을 테스트합니다
> * Azure에 배포

## <a name="prerequisites"></a>전제 조건

* [상속 구현](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="map-inheritance-to-database"></a>데이터베이스에 상속 매핑

`Instructor` 및 `Student` 의 클래스는 `School` 데이터 모델은 일부의 속성이 동일 합니다.

![Student_and_Instructor_classes](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

`Instructor` 및 `Student` 엔터티에서 공유하는 속성에 대해 중복 코드를 제거하려고 한다고 가정해 보겠습니다. 또는 강사 또는 학생의 이름인지 여부를 신경쓰지 않고 이름의 형식을 지정할 수 있는 서비스를 작성하려고 합니다. 만들 수 있습니다는 `Person` 기본 공유 속성만 포함 하는 클래스를 확인 합니다 `Instructor` 및 `Student` 다음 그림에 나와 있는 것 처럼 해당 기본 클래스에서 상속 되는 엔터티:

![Student_and_Instructor_classes_deriving_from_Person_class](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

데이터베이스에 이 상속 구조를 여러 가지 방법으로 나타낼 수 있습니다. 바라는 `Person` 학생과 강사 단일 테이블에서에 대 한 정보를 포함 하는 테이블입니다. 강사에만 적용할 수의 일부 열 (`HireDate`), 학생 들 에게만 일부 (`EnrollmentDate`), 둘 다로 일부 (`LastName`, `FirstName`). 일반적으로 해야는 *판별자* 각 행 형식을 나타내도록 열을 나타냅니다. 예를 들어, 판별자 열은 강사에 대해 "Instructor"를, 학생에 대해 "Student"를 포함할 수 있습니다.

![Hierarchy_example 당 테이블](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

단일 데이터베이스 테이블에서 엔터티 상속 구조를 생성 하는이 패턴 이라고 *계층당 하나의 테이블* TPH () 상속 합니다.

다른 방법은 데이터베이스를 상속 구조와 유사하게 만드는 것입니다. 예를 들어 이름 필드만 있을 수 있습니다는 `Person` 테이블 있고 별도 `Instructor` 및 `Student` 날짜 필드를 사용 하 여 테이블입니다.

![Table-per-type_inheritance](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

이 패턴의 각 엔터티 클래스는 호출에 대 한 데이터베이스 테이블을 만드는 *형식당 하나의 테이블* (TPT) 상속 합니다.

또 다른 옵션은 모든 비추상 형식을 개별 테이블에 매핑하는 것입니다. 상속된 속성을 포함한 모든 클래스 속성을 해당 테이블의 열에 매핑합니다. 이 패턴을 TPC(구체적 클래스당 하나의 테이블) 상속이라고 합니다. 에 대 한 TPC 상속을 구현 하는 경우는 `Person`, `Student`, 및 `Instructor` 이전에 표시 된 것 처럼 클래스는 `Student` 및 `Instructor` 이전과 다르지 상속을 구현한 후 테이블 다르지 보입니다.

TPC 및 TPH 상속 패턴 일반적으로 더 나은 성능을 제공 TPT 상속 패턴 보다 Entity Framework에서 TPT 패턴이 복잡 한 조인 쿼리에서 발생할 수 있기 때문입니다.

이 자습서에서는 TPH 상속을 구현하는 방법을 보여 줍니다. 만들기 위해 해야 할 모든 이므로 TPH는 Entity Framework에서 기본 상속 패턴을 `Person` 클래스를 변경 합니다 `Instructor` 및 `Student` 클래스에서 상속할 수 `Person`, 새 클래스를 추가 합니다를 `DbContext`, 만들고를 마이그레이션입니다. (다른 상속 패턴을 구현 하는 방법에 대 한 자세한 내용은 [(TPT) 형식당 하나의 테이블 상속 매핑](https://msdn.microsoft.com/data/jj591617#2.5) 하 고 [구체적 형식당 테이블 클래스 (TPC) 상속 매핑](https://msdn.microsoft.com/data/jj591617#2.6) msdn Entity Framework 설명서입니다.)

## <a name="create-the-person-class"></a>Person 클래스 만들기

에 *모델* 폴더를 만들기 *Person.cs* 템플릿 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

## <a name="update-instructor-and-student"></a>업데이트 Instructor 및 Student

이제 업데이트를 *Instructor.cs* 하 고 *Sudent.cs* 값에서 상속 하는 *Person.sc*.

*Instructor.cs*를 파생 합니다 `Instructor` 에서 클래스를 `Person` 클래스 및 키 및 이름 필드를 제거 합니다. 해당 코드는 다음 예제와 같이 나타납니다.

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

비슷하게 변경할 *Student.cs*합니다. `Student` 클래스는 다음 예제와 같습니다.

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="add-person-to-the-model"></a>모델에 사용자 추가

*SchoolContext.cs*, 추가 `DbSet` 에 대 한 속성을 `Person` 엔터티 형식:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

계층당 하나의 테이블 상속을 구성하기 위해 Entity Framework에 필요한 모든 작업입니다. 더 알 수 있듯이, 데이터베이스가 업데이트 되는 경우는 `Person` 대신 테이블을 `Student` 및 `Instructor` 테이블입니다.

## <a name="create-and-update-migrations"></a>만들고 마이그레이션 업데이트

관리자 콘솔 (PMC (패키지)을 다음 명령을 입력 합니다.

`Add-Migration Inheritance`

실행 된 `Update-Database` PMC에서 명령을 합니다. 명령은 기존 데이터 마이그레이션을 처리 하는 방법을 알지에 있기 때문이 시점에서 실패 합니다. 다음과 같은 오류 메시지가 표시:

> *개체를 삭제할 수 없습니다 ' dbo입니다. 강사 ' FOREIGN KEY 제약 조건에 의해 참조 되므로 합니다.*


오픈 *마이그레이션을\&lt; 타임 스탬프&gt;\_Inheritance.cs* 바꾸고는 `Up` 메서드를 다음 코드로:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

이 코드는 다음과 같은 데이터베이스 업데이트 작업을 처리합니다.

- Student 테이블을 가리키는 외래 키 제약 조건 및 인덱스를 제거합니다.
- Instructor 테이블 이름을 Person으로 바꾸고 Student 데이터를 저장하기 위해 필요한 변경을 수행합니다.

    - 학생에 대한 Nullable EnrollmentDate를 추가합니다.
    - 행이 학생용인지, 강사용인지 나타내는 판별자 열을 추가합니다.
    - 학생 행은 고용 날짜를 포함하지 않으므로 HireDate를 Nullable로 설정합니다.
    - 학생을 가리키는 외래 키를 업데이트하는 데 사용할 임시 필드를 추가합니다. 학생에 게 Person 테이블로 복사할 때 새 기본 키 값 하 게 합니다.
- Student 테이블에서 Person 테이블로 데이터를 복사합니다. 그러면 학생에게 새 기본 키 값이 할당됩니다.
- 학생을 가리키는 외래 키 값을 수정합니다.
- 이제 Person 테이블을 가리키도록 외래 키 제약 조건 및 인덱스를 다시 만듭니다.

(기본 키 형식으로 정수 대신 GUID를 사용한 경우, 학생 기본 키 값을 변경할 필요가 없으며 이 단계 중 일부가 생략되었을 수 있습니다.)

실행 된 `update-database` 명령을 다시 합니다.

(프로덕션 시스템에는 변경한 해당 하위 메서드 이전 데이터베이스 버전으로 돌아가려면 사용 해야 하는 경우. 이 자습서에 사용 하지 않습니다 하위 메서드.)

> [!NOTE]
> 스키마 변경 하므로 및 데이터를 마이그레이션하는 경우 다른 오류가 것이 가능 합니다. 마이그레이션 오류가 발생할 경우 해결할 수 없는, 연결 문자열을 변경 하 여 자습서를 진행할 수 있습니다 합니다 *Web.config* 파일 또는 데이터베이스 삭제 합니다. 가장 간단한 방법은 데이터베이스의 이름을 바꾸려면 합니다 *Web.config* 파일입니다. 다음 예와에서 같이 예를 들어, 데이터베이스 이름을 ContosoUniversity2로 변경 합니다.
>
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.xml?highlight=2)]
>
> 새 데이터베이스에 데이터가 없습니다. 마이그레이션할 및 `update-database` 명령은 오류 없이 완료 될 가능성이 훨씬 더 높습니다. 데이터베이스를 삭제 하는 방법에 지침은 [Visual Studio 2012에서 데이터베이스를 삭제 하는 방법](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)합니다. 이 자습서를 계속 하려면이 방법을 사용 하는 경우이 자습서의 끝에서 배포 단계를 건너뛸 또는 새 사이트 및 데이터베이스를 배포 합니다. 있습니다 했으므로 된 배포에 이미 동일한 사이트에 대 한 업데이트를 배포 하는 경우 자동 마이그레이션을 실행 하는 경우 EF가 동일한 오류가 받습니다. 마이그레이션 오류 문제를 해결 하려는 경우 가장 좋은 리소스는 Entity Framework 포럼 또는 StackOverflow.com 중입니다.

## <a name="test-the-implementation"></a>구현을 테스트합니다

사이트를 실행 하 고 다양 한 페이지를 시도 하세요. 모든 항목이 이전과 같이 작동합니다.

**서버 탐색기** 확장 **데이터 Connections\SchoolContext** 차례로 **테이블**를 표시 하 고는 **학생** 및 **강사** 테이블 바뀌었습니다를 **Person** 테이블입니다. 확장 합니다 **Person** 테이블 표시 이어야 하는 데 사용 하는 열 모두에 **학생** 및 **강사** 테이블.

Person 테이블을 마우스 오른쪽 단추로 클릭한 후 **테이블 데이터 표시**를 클릭하여 판별자 열을 표시합니다.

다음 다이어그램에서는 새 School 데이터베이스의 구조를 보여 줍니다.

![School_database_diagram](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

## <a name="deploy-to-azure"></a>Azure에 배포

이 섹션에서는 선택적 완료 해야 **Azure에 앱을 배포** 단원의 [3 부에 정렬, 필터링 및 페이징](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md) 이 자습서 시리즈의 합니다. 로컬 프로젝트에서 데이터베이스를 삭제 하 여 해결 하는 마이그레이션 오류를 설치한 경우이 단계 건너뛰기 또는 새 사이트 및 데이터베이스를 만들고 새 환경에 배포 합니다.

1. Visual studio에서에서 프로젝트를 마우스 오른쪽 단추로 **솔루션 탐색기** 선택한 **게시** 상황에 맞는 메뉴입니다.

2. **게시**를 클릭합니다.

    웹 앱이 기본 브라우저에서 열립니다.

3. 확인을 위해 응용 프로그램을 테스트 작동 합니다.

    실행 하는 페이지는 처음에는 데이터베이스에 액세스, Entity Framework를 실행 하 여 마이그레이션의 모든 `Up` 데이터베이스를 현재 데이터 모델을 사용 하 여 최신 상태로 만드는 데 필요한 메서드.

## <a name="get-the-code"></a>코드 가져오기

[완료 된 프로젝트 다운로드](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)

## <a name="additional-resources"></a>추가 자료

다른 Entity Framework 리소스에 대 한 링크에서 찾을 수 있습니다 합니다 [ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.

이 및 다른 상속 구조에 대 한 자세한 내용은 참조 하세요. [TPT 상속 패턴](https://msdn.microsoft.com/data/jj618293) 하 고 [TPH 상속 패턴](https://msdn.microsoft.com/data/jj618292) MSDN에서. 다음 자습서에서는 다양한 고급 Entity Framework 시나리오를 처리하는 방법을 살펴봅니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * 데이터베이스에 상속을 매핑할 학습
> * Person 클래스를 생성합니다.
> * 업데이트 된 강사 및 학생
> * 모델에 추가 된 사용자
> * 만들고 마이그레이션 업데이트
> * 구현 테스트
> * Azure에 배포

Entity Framework Code First를 사용 하는 ASP.NET 웹 응용 프로그램 개발의 기본 개념을 넘어 때 알아야 할 유용한 항목에 대해 자세히 알아보려면 다음 문서로 이동 합니다.
> [!div class="nextstepaction"]
> [고급 Entity Framework 시나리오](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)