---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: "ASP.NET MVC 5 (11/12) 응용 프로그램에서 Entity Framework 6 사용 하 여 상속 구현 | Microsoft Docs"
author: tdykstra
description: "Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 6 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/07/2014
ms.topic: article
ms.assetid: 08834147-77ec-454a-bb7a-d931d2a40dab
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: e6ee3f9c055a15b13c27f94675006b9a7e804f1b
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="implementing-inheritance-with-the-entity-framework-6-in-an-aspnet-mvc-5-application-11-of-12"></a>ASP.NET MVC 5 (11/12) 응용 프로그램에서 Entity Framework 6 사용 하 여 상속 구현
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트를 다운로드](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8) 또는 [PDF 다운로드](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)

> Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 6 Code First 및 Visual Studio 2013을 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대 한 정보를 참조 하십시오. [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.


이전 자습서에서 동시성 예외를 처리합니다. 이 자습서에서는 데이터 모델에서 상속을 구현 하는 방법을 보여줍니다.

개체 지향 프로그래밍에서 사용할 수 있습니다 [상속](http://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming)) 용이 하 게 [코드 재사용](http://en.wikipedia.org/wiki/Code_reuse)합니다. 이 자습서에서는 변경 된 `Instructor` 및 `Student` 에서 파생 되도록 클래스는 `Person` 기본 클래스와 같은 속성이 포함 된 `LastName` 강사 및 학생 데이터 모두에 공통적인 합니다. 추가 하거나 모든 웹 페이지를 변경 하지 않습니다 되지만 일부 코드를 변경 합니다 및 이러한 변경 내용을 데이터베이스에 자동으로 반영 됩니다.

## <a name="options-for-mapping-inheritance-to-database-tables"></a>데이터베이스 테이블에 상속 매핑에 대 한 옵션

`Instructor` 및 `Student` 에 있는 클래스는 `School` 데이터 모델에는 동일한 여러 속성이 있습니다.

![Student_and_Instructor_classes](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

공유 하는 속성에 대 한 중복 코드를 제거 하려는 경우 다음과 같이 `Instructor` 및 `Student` 엔터티. 또는 이름 강사 또는 학생 반환 되었는지 여부를 고려 하지 않고 이름에 서식을 지정할 수 있는 서비스를 작성 하려는 합니다. 만들 수는 `Person` 확인 한 다음 기본 속성을 공유 하는 것만 포함 하는 클래스는 `Instructor` 및 `Student` 다음 그림에 나와 있는 것 처럼 해당 기본 클래스에서 상속 되는 엔터티:

![Student_and_Instructor_classes_deriving_from_Person_class](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

여러 가지 방법으로 데이터베이스에이 상속 구조를 나타낼 수 있습니다. 있을 수 있습니다는 `Person` 학생과 단일 테이블에서 강사에 대 한 정보를 포함 하는 테이블입니다. 강사에만 적용할 수는 일부 열의 (`HireDate`), 학생에만 일부 (`EnrollmentDate`), 일부에 모두 (`LastName`, `FirstName`). 일반적으로, 한 *판별자* 는 형식을 각 행 표시 열을 나타냅니다. 예를 들어 판별자 열 학생용 강사 및 "학생"에 대 한 "강사"를 할 수 있습니다.

![Hierarchy_example 당 테이블](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

이 패턴의 단일 데이터베이스 테이블에서 엔터티 상속 구조를 생성 하 라고 *테이블 계층당* TPH () 상속 합니다.

대신 좀 더 상속 구조 처럼 보이도록 하는 데이터베이스입니다. 예를 들어 이름 필드에만 있을 수 있습니다는 `Person` 테이블 있고 별도 `Instructor` 및 `Student` 날짜 필드가 있는 테이블입니다.

![Type_inheritance 당 테이블](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

이 패턴의 각 엔터티 클래스에 대 한 데이터베이스 테이블을 만드는 *형식당 하나의 테이블* (TPT) 상속 합니다.

또 다른 옵션을 개별 테이블에 모든 추상이 아닌 형식을 매핑하는 것입니다. 상속 된 속성을 포함 하는 클래스의 모든 속성을 해당 테이블의 열에 매핑합니다. 이 패턴에는 테이블 구체적 클래스 (TPC) 상속을 라고 합니다. 에 대 한 TPC 상속을 구현 하는 경우는 `Person`, `Student`, 및 `Instructor` 앞에서 표시 된 것 처럼 클래스는 `Student` 및 `Instructor` 전과 상속 구현 후 테이블과 같습니다.

TPC 및 TPH 상속 패턴 일반적으로 더 나은 성능을 제공 TPT 상속 패턴 보다 Entity Framework에서 복잡 한 조인 쿼리에서 TPT 패턴 발생할 수 있기 때문입니다.

이 자습서에서는 TPH 상속 구현 하는 방법을 설명 합니다. TPH는 Entity Framework에서 기본 상속 패턴 만들기만 하면 이므로 `Person` 클래스, 변경의 `Instructor` 및 `Student` 클래스에서 상속할 수 `Person`에 새 클래스 추가 `DbContext`를 만들고는 마이그레이션입니다. (다른 상속 패턴을 구현 하는 방법에 대 한 정보를 참조 하십시오. [형식당 하나의 테이블 (TPT) 상속 매핑](https://msdn.microsoft.com/en-us/data/jj591617#2.5) 및 [테이블 구체적 클래스 (TPC) 상속 매핑](https://msdn.microsoft.com/en-us/data/jj591617#2.6) MSDN에서 Entity Framework 설명서입니다.)

## <a name="create-the-person-class"></a>Person 클래스 만들기

에 *모델* 폴더를 만들 *Person.cs* 템플릿 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

## <a name="make-student-and-instructor-classes-inherit-from-person"></a>사용자 로부터 상속 학생과 강사 클래스

*Instructor.cs*, 파생 된 `Instructor` 에서 클래스는 `Person` 클래스 및 키 / 이름 필드를 제거 합니다. 코드는 다음 예제와 같습니다.

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

비슷한 변경 *Student.cs*합니다. `Student` 클래스는 다음 예제와 같습니다.

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="add-the-person-entity-type-to-the-model"></a>Person 엔터티 형식을 모델에 추가

*SchoolContext.cs*, 추가 `DbSet` 속성에 대 한는 `Person` 엔터티 형식:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

Entity Framework 계층당 하나의 테이블 상속을 구성 하는 데 필요한 것입니다. 데이터베이스 업데이트 될 때, 볼 수 있듯이 한 `Person` 대신 테이블는 `Student` 및 `Instructor` 테이블입니다.

## <a name="create-and-update-a-migrations-file"></a>만들기 및 마이그레이션 파일 업데이트

패키지 관리자 콘솔 (PMC)에서 다음 명령을 입력 합니다.

`Add-Migration Inheritance`

실행 된 `Update-Database` 의 PMC 명령을 합니다. 기존 데이터 마이그레이션 처리 하는 방법을 모릅니다를 지정 했으므로 시점에서 명령이 실패 합니다. 다음과 같은 오류 메시지가 가져오려면

> *개체를 삭제할 수 없습니다 ' dbo입니다. 강사 ' FOREIGN KEY 제약 조건에 의해 참조 되므로 합니다.*


열기 *마이그레이션\&lt; 타임 스탬프&gt;\_Inheritance.cs* 바꾸고는 `Up` 메서드를 다음 코드로:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

이 코드는 다음과 같은 데이터베이스 작업 업데이트를 처리할 수 있습니다:

- Foreign key 제약 조건 및 학생 테이블 인덱스를 제거 합니다.
- 사람으로 강사 테이블 이름을 바꾸고 학생 데이터를 저장 하는 데 필요한 변경:

    - 학생용 nullable EnrollmentDate를 추가합니다.
    - 학생 또는 강사에 대 한 행이 있는지 여부를 나타내기 위해 판별자 열을 추가 합니다.
    - 학생 행 고용 날짜 되지 않았으므로 HireDate null을 허용 하면 있습니다.
    - 학생을 가리키는 외래 키를 업데이트 하는 임시 필드를 추가 합니다. 학생 Person 테이블에 복사 하는 경우 새 기본 키 값을 볼 수 있습니다.
- Person 테이블에 학생 테이블에서 데이터를 복사 합니다. 이렇게 하면 새 기본 키 값도 할당에 대해 학습 합니다.
- 학생을 가리키는 외래 키 값을 수정 합니다.
- Foreign key 제약 조건 및 인덱스를 이제으로 지정 하기 Person 테이블을 다시 만듭니다.

(기본 키 유형으로 정수 대신 GUID를 사용 했다면, 학생 기본 키 값을 변경할 필요가 없게 및 이러한 단계 중 일부 수 누락 되었습니다.)

실행 된 `update-database` 명령을 다시 합니다.

(프로덕션 시스템에는 해당을 변경 하면 다운 메서드 이전 데이터베이스 버전으로 돌아가려면를 사용 해야 하는 경우. 이 자습서에 대 한 사용 하지 않을 다운 메서드.)

> [!NOTE]
> 스키마 변경 하므로 및 데이터를 마이그레이션하는 경우 다른 오류를 가져오려는 것 같습니다. 마이그레이션 오류가 발생할 경우 해결할 수 없는, 연결 문자열을 변경 하 여이 자습서를 계속 하기는 *Web.config* 파일 또는 데이터베이스를 삭제 하 여 합니다. 가장 간단한 방법은 데이터베이스의 이름을 바꾸는 하는 *Web.config* 파일입니다. 예를 들어 다음 예제와 같이 ContosoUniversity2에 데이터베이스 이름을 변경:
> 
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.xml?highlight=2)]
> 
> 새 데이터베이스에서는 데이터가 없는 마이그레이션하려면 및 `update-database` 명령 작업이 오류 없이 완료 하는 것입니다. 데이터베이스를 삭제 하는 방법에 지침은 [Visual Studio 2012에서 데이터베이스를 삭제 하는 방법을](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)합니다. 이 자습서를 계속 하려면이 방법을 사용 하는 경우이 자습서의 끝에 배포 단계를 건너뛸 또는 새 사이트 및 데이터베이스에 배포 합니다. 한 된 배포 경우에 이미 동일한 사이트에 대 한 업데이트를 배포 하는 경우에 EF 마이그레이션이 자동으로 실행 때 동일한 오류가 발생에 발생 합니다. 마이그레이션 오류 문제를 해결 하려면 가장 적합 한 리소스는 StackOverflow.com 또는 Entity Framework 포럼 중 하나입니다.


## <a name="testing"></a>테스트

사이트를 실행 하 고 다양 한 페이지를 시도 하십시오. 모든 항목이 작동 하기 전과 동일 합니다.

**서버 탐색기** 확장 **데이터 Connections\SchoolContext** 차례로 **테이블**, 했다는 보고는 **학생** 및 **강사** 으로 바꾼 테이블을 **사람** 테이블입니다. 확장 하 고는 **사람** 테이블을 모두 사용 하는 열 참조는 **학생** 및 **강사** 테이블입니다.

![Server_Explorer_showing_Person_table](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

Person 테이블을 마우스 오른쪽 단추로 누른 **테이블 데이터 표시** 판별자 열을 표시 합니다.

![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

다음 다이어그램에서는 새 School 데이터베이스의 구조를 보여 줍니다.

![School_database_diagram](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

## <a name="deploy-to-azure"></a>Azure에 배포

이 섹션에 필요한 선택적 완료 **Azure에 앱을 배포** 섹션 [파트 3, 정렬, 필터링 및 페이징을](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md) 이 자습서 시리즈의 합니다. 마이그레이션 오류 로컬 프로젝트의 데이터베이스를 삭제 하 여 확인을 설치한 경우이 단계는; 또는 새 사이트 및 데이터베이스를 만들고 새 환경에 배포 합니다.

1. Visual Studio에서 프로젝트를 마우스 오른쪽 단추로 클릭 **솔루션 탐색기** 선택 **게시** 상황에 맞는 메뉴입니다.  
  
    ![프로젝트 상황에 맞는 메뉴에서 게시](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)
2. **게시**를 클릭합니다.  
  
    ![게시](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)  
  
 웹 응용 프로그램 기본 브라우저에서 열립니다.
3. 확인할 응용 프로그램을 테스트 작동 합니다.

    처음으로 페이지를 실행 하면 데이터베이스에 액세스, Entity Framework를 실행 하는 마이그레이션의 모든 `Up` 메서드 현재 데이터 모델을 최신 상태로 데이터베이스를 가져오는 데 필요 합니다.

## <a name="summary"></a>요약

에 대 한 계층당 하나의 테이블 상속을 구현한는 `Person`, `Student`, 및 `Instructor` 클래스입니다. 이 및 다른 상속 구조에 대 한 자세한 내용은 참조 [TPT 상속 패턴](https://msdn.microsoft.com/en-us/data/jj618293) 및 [TPH 상속 패턴](https://msdn.microsoft.com/en-us/data/jj618292) msdn 합니다. 다음 자습서에서는 다양 한 고급 비교적 Entity Framework 시나리오를 처리 하는 방법을 볼 수 있습니다.

다른 Entity Framework 리소스에 대 한 링크에서 확인할 수 있습니다는 [ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.

>[!div class="step-by-step"]
[이전](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[다음](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
