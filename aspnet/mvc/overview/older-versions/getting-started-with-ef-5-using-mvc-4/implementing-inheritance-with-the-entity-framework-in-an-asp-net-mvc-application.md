---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: (8 / 10) ASP.NET MVC 응용 프로그램에서 Entity Framework 사용한 상속 구현 | Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/30/2013
ms.topic: article
ms.assetid: a5c3feff-5335-4cdd-a97d-f7a8785c2494
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: ee088f841bdb68f4806b0b62be7d379b9eab9f8c
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30874007"
---
<a name="implementing-inheritance-with-the-entity-framework-in-an-aspnet-mvc-application-8-of-10"></a>(8 / 10) ASP.NET MVC 응용 프로그램에서 Entity Framework 사용한 상속 구현
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트를 다운로드 합니다.](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio 2012를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요. 시작 부분에서 자습서 시리즈를 시작할 수 있습니다 또는 [이 장의 대 한 시작 프로젝트 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 여기에서 시작 하 고 있습니다.
> 
> > [!NOTE] 
> > 
> > 해결할 수 없는 문제에 직면 하는 경우 [완료 장 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 문제를 재현 하려고 합니다. 일반적으로 코드 완성 된 코드를 비교 하 여 문제에 솔루션을 찾을 수 있습니다. 몇 가지 일반적인 오류 및 해결 하는 방법에 대 한 참조 [오류 및 해결 방법입니다.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)


이전 자습서에서 동시성 예외를 처리합니다. 이 자습서에서는 데이터 모델에서 상속을 구현하는 방법을 보여 줍니다.

개체 지향 프로그래밍에서 중복 코드를 제거할 상속을 사용할 수 있습니다. 이 자습서에서는 강사와 학생 모두에게 공통적인 속성(예: `LastName`)이 포함된 `Person` 기본 클래스에서 클래스가 파생되도록 `Instructor` 및 `Student` 클래스를 변경합니다. 웹 페이지를 추가하거나 변경하지는 않지만 일부 코드를 변경하고 이러한 변경 내용이 데이터베이스에 자동으로 반영됩니다.

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a>형식당 하나의 테이블 상속 및 계층 당 테이블

개체 지향 프로그래밍 관련된 클래스를 사용 하 여 쉽게 수행할 수 있도록 상속을 사용할 수 있습니다. 예를 들어는 `Instructor` 및 `Student` 에 있는 클래스는 `School` 데이터 모델을 중복 코드 줄어들고 결과적 몇 가지 속성을 공유 합니다.

![Student_and_Instructor_classes](https://asp.net/media/2578113/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_e7a32f99-8bc4-48ce-aeaf-216a18071a8b.png)

`Instructor` 및 `Student` 엔터티에서 공유하는 속성에 대해 중복 코드를 제거하려고 한다고 가정해 보겠습니다. 만들 수는 `Person` 확인 한 다음 기본 속성을 공유 하는 것만 포함 하는 클래스는 `Instructor` 및 `Student` 다음 그림에 나와 있는 것 처럼 해당 기본 클래스에서 상속 되는 엔터티:

![Student_and_Instructor_classes_deriving_from_Person_class](https://asp.net/media/2578119/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_deriving_from_Person_class_671d708c-cbb8-454a-a8f8-c2d99439acd9.png)

데이터베이스에 이 상속 구조를 여러 가지 방법으로 나타낼 수 있습니다. 있을 수 있습니다는 `Person` 학생과 단일 테이블에서 강사에 대 한 정보를 포함 하는 테이블입니다. 강사에만 적용할 수는 일부 열의 (`HireDate`), 학생에만 일부 (`EnrollmentDate`), 일부에 모두 (`LastName`, `FirstName`). 일반적으로, 한 *판별자* 는 형식을 각 행 표시 열을 나타냅니다. 예를 들어, 판별자 열은 강사에 대해 "Instructor"를, 학생에 대해 "Student"를 포함할 수 있습니다.

![Table-per-hierarchy_example](https://asp.net/media/2578125/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-hierarchy_example_244067cd-b451-4e9b-9595-793b9afca505.png)

이 패턴의 단일 데이터베이스 테이블에서 엔터티 상속 구조를 생성 하 라고 *테이블 계층당* TPH () 상속 합니다.

다른 방법은 데이터베이스를 상속 구조와 유사하게 만드는 것입니다. 예를 들어 이름 필드에만 있을 수 있습니다는 `Person` 테이블 있고 별도 `Instructor` 및 `Student` 날짜 필드가 있는 테이블입니다.

![Table-per-type_inheritance](https://asp.net/media/2578131/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-type_inheritance.png)

이 패턴의 각 엔터티 클래스에 대 한 데이터베이스 테이블을 만드는 *형식당 하나의 테이블* (TPT) 상속 합니다.

TPH 상속 패턴 일반적으로 더 나은 성능을 제공 TPT 상속 패턴 보다 Entity Framework에서 TPT 패턴 복잡 한 조인 쿼리에서 발생할 수 있기 때문입니다. 이 자습서에서는 TPH 상속을 구현하는 방법을 보여 줍니다. 다음 단계를 수행 하 여 수행 합니다.

- 만들기는 `Person` 클래스 및 변경 된 `Instructor` 및 `Student` 클래스에서 상속할 수 `Person`합니다.
- 데이터베이스 컨텍스트 클래스를 데이터베이스에 모델 매핑 코드를 추가 합니다.
- 변경 `InstructorID` 및 `StudentID` 참조를 프로젝트 전반에 걸쳐 `PersonID`합니다.

## <a name="creating-the-person-class"></a>사용자 클래스 만들기

 참고: 있습니다 할 수 없습니다 이러한 클래스를 사용 하는 컨트롤러를 업데이트할 때까지 아래 클래스를 만든 후 프로젝트를 컴파일합니다. 

에 *모델* 폴더를 만들 *Person.cs* 템플릿 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

*Instructor.cs*, 파생 된 `Instructor` 에서 클래스는 `Person` 클래스 및 키 / 이름 필드를 제거 합니다. 해당 코드는 다음 예제와 같이 나타납니다.

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

비슷한 변경 *Student.cs*합니다. `Student` 클래스는 다음 예제와 같습니다.

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="adding-the-person-entity-type-to-the-model"></a>Person 엔터티 형식을 모델에 추가

*SchoolContext.cs*, 추가 `DbSet` 속성에 대 한는 `Person` 엔터티 형식:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

계층당 하나의 테이블 상속을 구성하기 위해 Entity Framework에 필요한 모든 작업입니다. 하겠지만, 데이터베이스를 다시 생성 하는 경우는 `Person` 대신 테이블는 `Student` 및 `Instructor` 테이블입니다.

## <a name="changing-instructorid-and-studentid-to-personid"></a>InstructorID StudentID PersonID로 변경

*SchoolContext.cs*, 강사 과정 매핑 문에서 변경 `MapRightKey("InstructorID")` 를 `MapRightKey("PersonID")`:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=4)]

이러한 변경에는; 필요 하지 않습니다. 방금 다 대 다 조인 테이블에 InstructorID 열의 이름을 변경합니다. 이름으로 InstructorID 었으 면 응용 프로그램은 제대로 작동 여전히. 여기에 완성 된 *SchoolContext.cs*:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=15,24)]

변경 해야 다음 `InstructorID` 를 `PersonID` 및 `StudentID` 를 `PersonID` 프로젝트 전반에 걸쳐 ***제외 하 고*** 의 타임 스탬프 마이그레이션 파일에는 *마이그레이션* 폴더입니다. 그렇게 하려면 찾 및 열고 변경 해야 할 파일만 다음 열린된 파일에서 전역 변경 수행 수 있습니다. 유일한 파일은 *마이그레이션* 변경 해야 하는 폴더는 *Migrations\Configuration.cs 합니다.*

1. > [!IMPORTANT]
   > Visual Studio에서 열려 있는 모든 파일을 닫고 시작 합니다.
2. 클릭 **찾기 및 바꾸기 등의 모든 파일을 찾으려면** 에 **편집** 메뉴 및 포함 된 프로젝트의 모든 파일에 대 한 다음 검색 `InstructorID`합니다.  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. 각 파일을 열고는 **찾기 결과** 창 ***제외 하 고*** 는 &lt;타임 스탬프&gt;*\_.cs* 는 에서마이그레이션파일*마이그레이션* 폴더 각 파일에 대 한 줄을 두 번 클릭 합니다.  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)
4. 열기는 **파일에서 바꾸기** 대화 상자와 변경 **찾는 위치** 를 **열려 있는 모든 문서**합니다.
5. 사용 하 여는 **파일에서 바꾸기** 모든 변경 하려면 대화 `InstructorID` 를 `PersonID.`  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)
6. 포함 된 프로젝트의 모든 파일을 찾을 `StudentID`합니다.
7. 각 파일을 열고는 **찾기 결과** 창 ***제외 하 고*** 는 &lt;타임 스탬프&gt;*\_\*.cs* 마이그레이션 파일 에 *마이그레이션* 폴더 각 파일에 대 한 줄을 두 번 클릭 합니다.  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
8. 열기는 **파일에서 바꾸기** 대화 상자와 변경 **찾는 위치** 를 **열려 있는 모든 문서**합니다.
9. 사용 하 여는 **파일에서 바꾸기** 모든 변경 하려면 대화 `StudentID` 를 `PersonID`합니다.   
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)
10. 프로젝트를 빌드합니다.

(이 보이는 참고는 *단점은* 의 `classnameID` 패턴의 기본 키 이름을 지정 합니다. 기본 키 ID 클래스 이름에 접두사를 추가 하지 않고 명명 된 *없습니다* 이름 바꾸기을 수행 해야 이제.)

## <a name="create-and-update-a-migrations-file"></a>만들기 및 마이그레이션 파일 업데이트

패키지 관리자 콘솔 (PMC)에서 다음 명령을 입력 합니다.

`Add-Migration Inheritance`

실행 된 `Update-Database` 의 PMC 명령을 합니다. 기존 데이터 마이그레이션 처리 하는 방법을 모릅니다를 지정 했으므로 시점에서 명령이 실패 합니다. 다음과 같은 오류가 있습니다.

*ALTER TABLE 문을 FOREIGN KEY 제약 조건 충돌 "FK\_dbo입니다. 부서\_dbo입니다. 사람\_PersonID "입니다. 데이터베이스 "ContosoUniversity" 테이블 "dbo에에서 충돌이 발생 했습니다. 사용자 ", 열 'PersonID'입니다.*

열기 *마이그레이션\&lt; 타임 스탬프&gt;\_Inheritance.cs* 바꾸고는 `Up` 메서드를 다음 코드로:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=25,29-40)]

실행 된 `update-database` 명령을 다시 합니다.

> [!NOTE]
> 스키마 변경 하므로 및 데이터를 마이그레이션하는 경우 다른 오류를 가져오려는 것 같습니다. 마이그레이션 오류가 발생할 경우 해결할 수 없는, 연결 문자열을 변경 하 여이 자습서를 계속 하기는 *Web.config* 파일 또는 데이터베이스를 삭제 합니다. 가장 간단한 방법은 데이터베이스의 이름을 바꾸는 하는 *Web.config* 파일입니다. 예를 들어 데이터베이스 이름을 CU로 변경\_다음 예제와 같이 테스트 합니다.
> 
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.xml?highlight=1-2)]
> 
> 새 데이터베이스에서는 데이터가 없는 마이그레이션하려면 및 `update-database` 명령 작업이 오류 없이 완료 하는 것입니다. 데이터베이스를 삭제 하는 방법에 지침은 [Visual Studio 2012에서 데이터베이스를 삭제 하는 방법을](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)합니다. 이 자습서를 계속 하려면이 방법을 사용 하는 경우는 마이그레이션이 자동으로 실행 될 때 배포 된 사이트 동일한 오류가 대기줄 않으므로이 자습서의 끝에 배포 단계를 건너뜁니다. 마이그레이션 오류 문제를 해결 하려면 가장 적합 한 리소스는 StackOverflow.com 또는 Entity Framework 포럼 중 하나입니다.


## <a name="testing"></a>테스트

사이트를 실행 하 고 다양 한 페이지를 시도 하십시오. 모든 항목이 이전과 같이 작동합니다.

**서버 탐색기** 확장 **SchoolContext** 차례로 **테이블**, 했다는 보고는 **학생** 및 **강사**  으로 바꾼 테이블을 **사람** 테이블입니다. 확장 하 고는 **사람** 테이블을 모두 사용 하는 열 참조는 **학생** 및 **강사** 테이블입니다.

![Server_Explorer_showing_Person_table](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

Person 테이블을 마우스 오른쪽 단추로 클릭한 후 **테이블 데이터 표시**를 클릭하여 판별자 열을 표시합니다.

![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

다음 다이어그램에서는 새 School 데이터베이스의 구조를 보여 줍니다.

![School_database_diagram](https://asp.net/media/2578143/Windows-Live-Writer_58f5a93579b2_CC7B_School_database_diagram_6350a801-7199-413f-bbac-4a2009ed19d7.png)

## <a name="summary"></a>요약

에 대해 계층당 하나의 테이블 상속이 구현 이제는 `Person`, `Student`, 및 `Instructor` 클래스입니다. 이 및 다른 상속 구조에 대 한 자세한 내용은 참조 [상속 매핑 전략](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx) Morteza Manavi 블로그. 다음 자습서에서는 일부의 작업 패턴의 단위 및 저장소 구현 하기 위해 표시 됩니다.

다른 Entity Framework 리소스에 대 한 링크에서 확인할 수 있습니다는 [ASP.NET 데이터 액세스 콘텐츠 맵](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.

> [!div class="step-by-step"]
> [이전](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [다음](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)
