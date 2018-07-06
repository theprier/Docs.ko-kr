---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: (8 / 10) ASP.NET MVC 응용 프로그램에서 Entity Framework 사용한 상속 구현 | Microsoft Docs
author: tdykstra
description: Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다...
ms.author: aspnetcontent
ms.date: 07/30/2013
ms.assetid: a5c3feff-5335-4cdd-a97d-f7a8785c2494
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: b39fc609007d437dd0845f9087dd5a32272cebe9
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37821278"
---
<a name="implementing-inheritance-with-the-entity-framework-in-an-aspnet-mvc-application-8-of-10"></a>(8 / 10) ASP.NET MVC 응용 프로그램에서 Entity Framework 사용한 상속 구현
====================
[Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트 다운로드](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio 2012를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요. 시작 부분에서 자습서 시리즈를 시작할 수 있습니다 또는 [이 장이에 대 한 시작 프로젝트 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 여기에서 시작 하 고 있습니다.
> 
> > [!NOTE] 
> > 
> > 해결할 수 없는 문제가 발생 하는 경우 [완성 된 장 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 문제를 재현 하려고 합니다. 일반적으로 코드의 완성 된 코드를 비교 하 여 문제에 솔루션을 찾을 수 있습니다. 몇 가지 일반적인 오류 및 해결 하는 방법에 대 한 참조 [오류 및 해결 방법입니다.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)


이전 자습서에서 동시성 예외를 처리 합니다. 이 자습서에서는 데이터 모델에서 상속을 구현하는 방법을 보여 줍니다.

개체 지향 프로그래밍에서 중복 코드를 제거 하기 위해 상속을 사용할 수 있습니다. 이 자습서에서는 강사와 학생 모두에게 공통적인 속성(예: `LastName`)이 포함된 `Person` 기본 클래스에서 클래스가 파생되도록 `Instructor` 및 `Student` 클래스를 변경합니다. 웹 페이지를 추가하거나 변경하지는 않지만 일부 코드를 변경하고 이러한 변경 내용이 데이터베이스에 자동으로 반영됩니다.

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a>형식당 하나의 테이블 상속 및 계층 당 테이블

개체 지향 프로그래밍에서는 쉽게 관련된 클래스를 사용 하 여 상속을 사용할 수 있습니다. 예를 들어 합니다 `Instructor` 하 고 `Student` 의 클래스는 `School` 데이터 모델 중복 코드에서 발생 하는 몇 가지 속성을 공유:

![Student_and_Instructor_classes](https://asp.net/media/2578113/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_e7a32f99-8bc4-48ce-aeaf-216a18071a8b.png)

`Instructor` 및 `Student` 엔터티에서 공유하는 속성에 대해 중복 코드를 제거하려고 한다고 가정해 보겠습니다. 만들 수 있습니다는 `Person` 기본 공유 속성만 포함 하는 클래스를 확인 합니다 `Instructor` 및 `Student` 다음 그림에 나와 있는 것 처럼 해당 기본 클래스에서 상속 되는 엔터티:

![Student_and_Instructor_classes_deriving_from_Person_class](https://asp.net/media/2578119/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_deriving_from_Person_class_671d708c-cbb8-454a-a8f8-c2d99439acd9.png)

데이터베이스에 이 상속 구조를 여러 가지 방법으로 나타낼 수 있습니다. 바라는 `Person` 학생과 강사 단일 테이블에서에 대 한 정보를 포함 하는 테이블입니다. 강사에만 적용할 수의 일부 열 (`HireDate`), 학생 들 에게만 일부 (`EnrollmentDate`), 둘 다로 일부 (`LastName`, `FirstName`). 일반적으로 해야는 *판별자* 각 행 형식을 나타내도록 열을 나타냅니다. 예를 들어, 판별자 열은 강사에 대해 "Instructor"를, 학생에 대해 "Student"를 포함할 수 있습니다.

![Hierarchy_example 당 테이블](https://asp.net/media/2578125/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-hierarchy_example_244067cd-b451-4e9b-9595-793b9afca505.png)

단일 데이터베이스 테이블에서 엔터티 상속 구조를 생성 하는이 패턴 이라고 *계층당 하나의 테이블* TPH () 상속 합니다.

다른 방법은 데이터베이스를 상속 구조와 유사하게 만드는 것입니다. 예를 들어 이름 필드만 있을 수 있습니다는 `Person` 테이블 있고 별도 `Instructor` 및 `Student` 날짜 필드를 사용 하 여 테이블입니다.

![Table-per-type_inheritance](https://asp.net/media/2578131/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-type_inheritance.png)

이 패턴의 각 엔터티 클래스는 호출에 대 한 데이터베이스 테이블을 만드는 *형식당 하나의 테이블* (TPT) 상속 합니다.

TPH 상속 패턴 일반적으로 더 나은 성능을 낼 TPT 상속 패턴 보다 Entity Framework에서 TPT 패턴이 복잡 한 조인 쿼리에서 발생할 수 있기 때문입니다. 이 자습서에서는 TPH 상속을 구현하는 방법을 보여 줍니다. 다음 단계를 수행 하 여 할 수 있습니다.

- 만들기를 `Person` 클래스 및 변경 합니다 `Instructor` 하 고 `Student` 클래스에서 상속할 수 `Person`.
- 데이터베이스 컨텍스트 클래스를 데이터베이스에 모델 매핑 코드를 추가 합니다.
- 변경 `InstructorID` 하 고 `StudentID` 참조를 프로젝트 전체에 걸쳐 `PersonID`합니다.

## <a name="creating-the-person-class"></a>Person 클래스 만들기

 참고: 수 없게 이러한 클래스를 사용 하는 컨트롤러를 업데이트할 때까지 아래의 클래스를 만든 후 프로젝트를 컴파일합니다. 

에 *모델* 폴더를 만들기 *Person.cs* 템플릿 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

*Instructor.cs*를 파생 합니다 `Instructor` 에서 클래스를 `Person` 클래스 및 키 및 이름 필드를 제거 합니다. 해당 코드는 다음 예제와 같이 나타납니다.

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

비슷하게 변경할 *Student.cs*합니다. `Student` 클래스는 다음 예제와 같습니다.

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="adding-the-person-entity-type-to-the-model"></a>Person 엔터티 형식을 모델에 추가

*SchoolContext.cs*, 추가 `DbSet` 에 대 한 속성을 `Person` 엔터티 형식:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

계층당 하나의 테이블 상속을 구성하기 위해 Entity Framework에 필요한 모든 작업입니다. 더 알 수 있듯이, 데이터베이스를 다시 만든 경우는 `Person` 대신 테이블을 `Student` 및 `Instructor` 테이블입니다.

## <a name="changing-instructorid-and-studentid-to-personid"></a>InstructorID StudentID PersonID로 변경

*SchoolContext.cs*, 강사-강좌 매핑 문에서 변경 `MapRightKey("InstructorID")` 하려면 `MapRightKey("PersonID")`:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=4)]

이 변경에는; 필요 하지 않습니다. 방금 다 대 다 조인 테이블에 InstructorID 열의 이름을 변경합니다. InstructorID로 이름을 지정 하지, 응용 프로그램 여전히 올바르게 작동 합니다. 여기에 전체 *SchoolContext.cs*:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=15,24)]

변경 해야 하는 다음 `InstructorID` 에 `PersonID` 및 `StudentID` 에 `PersonID` 프로젝트 전반에 걸쳐 ***제외 하 고*** 의 타임 스탬프 마이그레이션 파일에는 *마이그레이션을* 폴더입니다. 이렇게 하려면 찾 및 변경 해야 할 파일만 연 다음 열린된 파일에 전역 변경을 수행 하겠습니다. 유일한 파일을 *마이그레이션을* 변경 해야 하는 폴더는 *migrations\ configuration.cs 합니다.*

1. > [!IMPORTANT]
   > Visual Studio에서 열려 있는 모든 파일을 닫아 시작 합니다.
2. 클릭 **찾기 및 바꾸기-모든 파일을 찾으려면** 에 **편집** 메뉴 및 포함 된 프로젝트의 모든 파일에 대 한 다음 검색 `InstructorID`합니다.  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. 각 파일을 엽니다는 **찾기 결과** 창 ***제외한*** 는 &lt;타임 스탬프&gt;*\_.cs* 합니다 에서마이그레이션파일*마이그레이션을* 폴더, 각 파일에 대 한 한 줄을 두 번 클릭 합니다.  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)
4. 열기를 **파일에서 바꾸기** 대화 상자 및 변경 **찾는 위치** 하 **모든 열린 문서**합니다.
5. 사용 된 **파일에서 바꾸기** 변경할 모든 대화 상자를 `InstructorID` 를 `PersonID.`  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)
6. 포함 된 프로젝트의 모든 파일을 찾을 `StudentID`합니다.
7. 각 파일을 엽니다는 **찾기 결과** 창이 ***제외한*** 는 &lt;타임 스탬프&gt;*\_\*.cs* 마이그레이션 파일 에 *마이그레이션을* 각 파일에 대 한 한 줄을 두 번 클릭 하 여 폴더입니다.  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
8. 열기를 **파일에서 바꾸기** 대화 상자 및 변경 **찾는 위치** 하 **모든 열린 문서**합니다.
9. 사용 하 여는 **파일에서 바꾸기** 모두를 변경 하려면 대화 상자 `StudentID` 에 `PersonID`입니다.   
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)
10. 프로젝트를 빌드합니다.

(이 보여 주는 참고를 *단점은* 의 `classnameID` 패턴 기본 키의 이름을 지정 합니다. 기본 키 ID 클래스 이름 접두사 없이 명명 된 경우 *없습니다* 이름을 변경 해야 하지만 이제.)

## <a name="create-and-update-a-migrations-file"></a>마이그레이션 파일 만들기 및 업데이트

관리자 콘솔 (PMC (패키지)을 다음 명령을 입력 합니다.

`Add-Migration Inheritance`

실행 된 `Update-Database` PMC에서 명령을 합니다. 명령은 기존 데이터 마이그레이션을 처리 하는 방법을 알지에 있기 때문이 시점에서 실패 합니다. 다음 오류가 있습니다.

*ALTER TABLE 문이 FOREIGN KEY 제약 조건 충돌 "FK\_dbo입니다. 부서\_dbo입니다. Person\_PersonID "입니다. 데이터베이스 "ContosoUniversity", "dbo 테이블에서에서 충돌이 발생 했습니다. 사용자 ", 열 'PersonID'입니다.*

오픈 *마이그레이션을\&lt; 타임 스탬프&gt;\_Inheritance.cs* 바꾸고는 `Up` 메서드를 다음 코드로:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=25,29-40)]

실행 된 `update-database` 명령을 다시 합니다.

> [!NOTE]
> 스키마 변경 하므로 및 데이터를 마이그레이션하는 경우 다른 오류가 것이 가능 합니다. 마이그레이션 오류가 발생할 경우 해결할 수 없는, 연결 문자열을 변경 하 여 자습서를 진행할 수 있습니다 합니다 *Web.config* 파일 또는 데이터베이스를 삭제 합니다. 가장 간단한 방법은 데이터베이스의 이름을 바꾸려면 합니다 *Web.config* 파일입니다. 예를 들어, CU로 데이터베이스 이름을 변경\_다음 예제에서와 같이 테스트 합니다.
> 
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.xml?highlight=1-2)]
> 
> 새 데이터베이스에 데이터가 없습니다. 마이그레이션할 및 `update-database` 명령은 오류 없이 완료 될 가능성이 훨씬 더 높습니다. 데이터베이스를 삭제 하는 방법에 지침은 [Visual Studio 2012에서 데이터베이스를 삭제 하는 방법](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)합니다. 이 자습서를 계속 하려면이 방법을 사용 하는 경우는 마이그레이션이 자동으로 실행 될 때 배포 된 사이트에서 동일한 오류를 얻게 되므로이 자습서의 끝에서 배포 단계를 건너뜁니다. 마이그레이션 오류 문제를 해결 하려는 경우 가장 좋은 리소스는 Entity Framework 포럼 또는 StackOverflow.com 중입니다.


## <a name="testing"></a>테스트

사이트를 실행 하 고 다양 한 페이지를 시도 하세요. 모든 항목이 이전과 같이 작동합니다.

**서버 탐색기** 확장 **SchoolContext** 차례로 **테이블**를 표시 하 고는 **학생** 및 **강사**  테이블 바뀌었습니다를 **Person** 테이블입니다. 확장 합니다 **Person** 테이블 표시 이어야 하는 데 사용 하는 열 모두에 **학생** 및 **강사** 테이블.

![Server_Explorer_showing_Person_table](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

Person 테이블을 마우스 오른쪽 단추로 클릭한 후 **테이블 데이터 표시**를 클릭하여 판별자 열을 표시합니다.

![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

다음 다이어그램에서는 새 School 데이터베이스의 구조를 보여 줍니다.

![School_database_diagram](https://asp.net/media/2578143/Windows-Live-Writer_58f5a93579b2_CC7B_School_database_diagram_6350a801-7199-413f-bbac-4a2009ed19d7.png)

## <a name="summary"></a>요약

이제 계층당 하나의 테이블 상속에 대해 구현에 `Person`, `Student`, 및 `Instructor` 클래스입니다. 이 및 다른 상속 구조에 대 한 자세한 내용은 참조 하세요. [상속 매핑 전략](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx) Morteza Manavi 블로그. 다음 자습서에서는 리포지토리 및 작업 패턴 단위를 구현 하는 몇 가지 방법을 볼 수 있습니다.

다른 Entity Framework 리소스에 대 한 링크에서 찾을 수 있습니다 합니다 [ASP.NET 데이터 액세스 콘텐츠 맵](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.

> [!div class="step-by-step"]
> [이전](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [다음](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)
