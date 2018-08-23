---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
title: 리포지토리 및 작업 패턴 단위 (9 / 10) ASP.NET MVC 응용 프로그램 구현 | Microsoft Docs
author: tdykstra
description: Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 44761193-04ba-4990-9f90-145d3c10a716
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 20f82744582faddaffdc5b4785bf208ecf0955a7
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41828781"
---
<a name="implementing-the-repository-and-unit-of-work-patterns-in-an-aspnet-mvc-application-9-of-10"></a>(9 / 10) ASP.NET MVC 응용 프로그램에서 리포지토리 및 작업 패턴 단위 구현
====================
[Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트 다운로드](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio 2012를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요. 시작 부분에서 자습서 시리즈를 시작할 수 있습니다 또는 [이 장이에 대 한 시작 프로젝트 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 여기에서 시작 하 고 있습니다.
> 
> > [!NOTE] 
> > 
> > 해결할 수 없는 문제가 발생 하는 경우 [완성 된 장 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 문제를 재현 하려고 합니다. 일반적으로 코드의 완성 된 코드를 비교 하 여 문제에 솔루션을 찾을 수 있습니다. 몇 가지 일반적인 오류 및 해결 하는 방법에 대 한 참조 [오류 및 해결 방법입니다.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)


이전 자습서에서 중복 코드를 줄이기 위해 상속 사용 합니다 `Student` 고 `Instructor` 엔터티 클래스입니다. 이 자습서에서 CRUD 작업에 대 한 리포지토리 및 작업 패턴 단위를 사용 하는 몇 가지 방법을 볼 수 있습니다. 이전 자습서와 같이 변경 방식과 코드 페이지를 사용 하 여 이미 생성 하지 않고 새 페이지를 만들 수 있습니다.

## <a name="the-repository-and-unit-of-work-patterns"></a>리포지토리 및 작업 패턴 단위

리포지토리 및 작업 패턴 단위는 데이터 액세스 계층 및 응용 프로그램의 비즈니스 논리 계층 간에 추상화 계층을 만들기 위해 제공 됩니다. 이러한 패턴을 구현하면 데이터 저장소의 변경 내용으로부터 응용 프로그램을 격리할 수 있으며 자동화된 단위 테스트 또는 TDD(테스트 중심 개발)를 용이하게 수행할 수 있습니다.

이 자습서에서는 각 엔터티 형식에 대 한 리포지토리 클래스를 구현할 수 있습니다. 에 대 한는 `Student` 리포지토리 인터페이스 및 리포지토리 클래스를 만들어야 하는 엔터티 형식입니다. 저장소 컨트롤러에서를 인스턴스화할 때 컨트롤러 리포지토리 인터페이스를 구현 하는 개체에 대 한 참조를 받아들일 수 있도록 인터페이스를 사용 합니다. 컨트롤러는 웹 서버에서 실행 되 면 Entity Framework와 함께 작동 하는 리포지토리를 받습니다. 컨트롤러 단위 테스트 클래스에서 실행 되는 메모리 내 컬렉션과 같은 테스트를 쉽게 조작할 수 있는 방식으로 저장 된 데이터를 사용 하 여 작동 하는 리포지토리를 받습니다.

나중에 자습서에서는 사용 하 여 여러 리포지토리 및 작업 클래스에 대 한 단위를 `Course` 및 `Department` 엔터티 형식에 `Course` 컨트롤러입니다. 작업 클래스의 단위 모두에서 공유 하는 단일 데이터베이스 컨텍스트 클래스를 만들어 여러 리포지토리의 작업을 조정 합니다. 자동화 된 단위 테스트를 수행할 수 하려는 경우 만들고 이러한 클래스에 대 한 인터페이스를 사용 하 여에 수행한 동일한 방식으로 `Student` 리포지토리. 그러나이 자습서를 간단히 유지 하기 만들고 인터페이스 없이 이러한 클래스를 사용 합니다.

다음 그림에서는 컨트롤러와 비교 하지 리포지토리 또는 작업 단위 패턴을 전혀 사용 하는 컨텍스트 클래스 간의 관계를 개념화 하는 방법을 보여 줍니다.

![Repository_pattern_diagram](https://asp.net/media/2578149/Windows-Live-Writer_8c4963ba1fa3_CE3B_Repository_pattern_diagram_1df790d3-bdf2-4c11-9098-946ddd9cd884.png)

이 자습서 시리즈에서 단위 테스트를 만들고 없습니다. 리포지토리 패턴을 사용 하는 MVC 응용 프로그램을 사용 하 여 TDD 소개를 참조 하세요 [연습: ASP.NET MVC와 함께 TDD를 사용 하 여](https://msdn.microsoft.com/library/ff847525.aspx)입니다. 리포지토리 패턴에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [리포지토리 패턴](https://msdn.microsoft.com/library/ff649690.aspx) MSDN에 있습니다.
- [Entity Framework 4.0을 사용 하 여 리포지토리 및 작업 단위 패턴을 사용 하 여](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx) Entity Framework 팀 블로그.
- [Agile Entity Framework 4 리포지토리](http://thedatafarm.com/blog/data-access/agile-entity-framework-4-repository-part-1-model-and-poco-classes/) Julie Lerman의 블로그 게시물 시리즈입니다.
- [빌드 보기 HTML5/jQuery 응용 프로그램을에서 계정을](https://weblogs.asp.net/dwahlin/archive/2011/08/15/building-the-account-at-a-glance-html5-jquery-application.aspx) Dan Wahlin의 블로그입니다.

> [!NOTE]
> 리포지토리 및 작업 패턴 단위를 구현 하는 방법은 여러 가지가 있습니다. 작업 클래스의 단위 없이 리포지토리 클래스를 사용할 수 있습니다. 모든 엔터티 형식 또는 각 형식에 대 한 하나에 대 한 단일 리포지토리를 구현할 수 있습니다. 각 형식에 대 한 하나를 구현 하는 경우에 별도 클래스, 제네릭 기본 클래스 및 파생된 클래스 또는 추상 기본 클래스 및 파생된 클래스를 사용할 수 있습니다. 리포지토리에서 비즈니스 논리를 포함할 수도 있고 데이터 액세스 논리를 제한할 수 있습니다. 사용 하 여 데이터베이스 컨텍스트 클래스에 추상 계층을 빌드할 수도 있습니다 [IDbSet](https://msdn.microsoft.com/library/gg679233(v=vs.103).aspx) 대신 있습니다 인터페이스 [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) 엔터티 집합에는 형식입니다. 이 자습서에 나와 있는 추상화 계층을 구현 하는 방법에는 되지 모든 시나리오 및 환경에 대 한 권장 사항을 고려해 야 하는 한 가지 옵션입니다.


## <a name="creating-the-student-repository-class"></a>학생 리포지토리 클래스 만들기

에 *DAL* 폴더를 라는 클래스 파일을 만듭니다 *IStudentRepository.cs* 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample1.cs)]

이 코드는 일반적인 CRUD 메서드를 두 개의 읽기 메서드를 포함 하 여 집합을 선언 합니다.-모든 반환 하는 `Student` 엔터티 및 단일 찾습니다는 `Student` 엔터티 id

에 *DAL* 폴더를 라는 클래스 파일을 만듭니다 *StudentRepository.cs* 파일입니다. 기존 코드를 구현 하는 다음 코드로 대체 합니다 `IStudentRepository` 인터페이스:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample2.cs)]

데이터베이스 컨텍스트 클래스 변수에 정의 됩니다 하며 생성자 호출 개체 컨텍스트 인스턴스를 전달 합니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample3.cs)]

리포지토리에 새 컨텍스트를 인스턴스화할 수 있지만 다음 하나의 컨트롤러에서 여러 리포지토리를 사용 하는 경우 각 결국에 별도 컨텍스트를 사용 하 여 합니다. 나중에 사용 하 여에서 여러 리포지토리를 `Course` 컨트롤러에서 어떻게 작업 클래스의 단위는 모든 리포지토리는 사용 하도록 동일한 컨텍스트 표시 됩니다.

저장소 구현 [IDisposable](https://msdn.microsoft.com/library/system.idisposable.aspx) 하 고 컨트롤러에서 앞서 살펴본를 해당 CRUD 메서드 호출 데이터베이스 컨텍스트 앞서 본 것과 동일한 방식에서으로 데이터베이스 컨텍스트를 삭제 합니다.

## <a name="change-the-student-controller-to-use-the-repository"></a>저장소를 사용 하는 학생 컨트롤러를 변경 합니다.

*StudentController.cs*, 클래스의 현재 코드를 다음 코드로 바꿉니다. 변경 내용은 강조 표시되어 있습니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=13-18,44,75,77,102-103,120,137-138,159,172-174,186)]

컨트롤러에는 이제 구현 하는 개체에 대 한 클래스 변수를 선언 합니다 `IStudentRepository` 컨텍스트 클래스가 아니라 인터페이스:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample5.cs)]

기본 (매개 변수가 없는) 생성자는 새 컨텍스트 인스턴스를 만들고 선택적 생성자를 호출자 컨텍스트 인스턴스를 전달할 수 있습니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample6.cs)]

(사용 중 이었다 면 *종속성 주입*, DI를 DI 소프트웨어 올바른 리포지토리 개체 제공 되는 항상 확인 하므로 기본 생성자는 필요 하지 않습니다. 또는.)

CRUD 메서드에서 저장소 컨텍스트 대신 라고 합니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample7.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample8.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample9.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample10.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample11.cs)]

및 `Dispose` 메서드는 이제 컨텍스트 대신 리포지토리를 삭제 합니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample12.cs)]

사이트를 실행 하 고 클릭 합니다 **학생** 탭 합니다.

![Students_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image1.png)

페이지를 찾아 리포지토리를 사용 하는 코드를 변경 하 고 다른 학생 페이지도 동일 하 게 작동 하기 전 처럼 동일한 방식으로 작동 합니다. 그러나 방식으로 중요 한 차이점이 있습니다.는 `Index` 컨트롤러의 메서드는 필터링 및 정렬 합니다. 다음 코드를 포함 하는이 메서드의 원래 버전:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample13.cs?highlight=1)]

업데이트 된 `Index` 메서드에 다음 코드를 포함 합니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=1)]

강조 표시 된 코드에만 변경 되었습니다.

코드의 원래 버전에서 `students` 으로 입력 된는 `IQueryable` 개체입니다. 와 같은 메서드를 사용 하 여 컬렉션으로 변환 하지 않으면 쿼리는 데이터베이스에 전송 되지 않습니다 `ToList`, 인덱스 보기 학생 모델에 액세스 될 때까지 발생 하지 않습니다. 합니다 `Where` 위의 원본 코드에서 메서드를 `WHERE` 데이터베이스로 전송 되는 SQL 쿼리 절. 그러면 즉, 데이터베이스에서 선택한 엔터티만 반환 되도록 합니다. 그러나 변경의 결과로 `context.Students` 하 `studentRepository.GetStudents()`, `students` 문이이 변수는 `IEnumerable` 데이터베이스에 속한 모든 학생을 포함 하는 컬렉션입니다. 적용 하는 최종 결과 `Where` 메서드는 동일 하지만 데이터베이스가 아니라에 웹 서버의 메모리에는 작업을 수행 하는 이제 합니다. 많은 양의 데이터를 반환 하는 쿼리에 대 한이 비효율적일 수 있습니다.

> [!TIP]
> 
> **IQueryable vs입니다. IEnumerable**
> 
> 구현한 후 저장소 다음과 같이에서 내용을 입력 해야 하는 경우에 합니다 **검색** 상자 SQL 서버로 보내진 쿼리의 검색 조건을 포함 하지 않으므로 모든 학생 행을 반환 합니다.
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image2.png)
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample15.sql)]
> 
> 저장소 검색 조건에 대 한 알 필요 없이 쿼리를 실행 하기 때문에이 쿼리는 모든 학생 데이터를 반환 합니다. 정렬, 검색 조건을 적용 하 고 메모리에서 수행 됩니다 (이 경우 3 개의 행 표시) 하는 페이징에 대 한 데이터의 하위 집합을 선택 과정 뒷부분에 나오는 경우를 `ToPagedList` 메서드를 호출 합니다 `IEnumerable` 컬렉션입니다.
> 
> (저장소를 구현 하기) 전에 코드의 이전 버전에서는 쿼리를 보내지 될 때까지 데이터베이스에는 검색 조건을 적용 한 후 때 `ToPagedList` 라고 하는 `IQueryable` 개체입니다.
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image3.png)
> 
> ToPagedList에서 호출 되는 경우는 `IQueryable` 개체를 SQL Server 전송 되는 쿼리, 검색 문자열을 지정 하 고 결과적으로 검색 조건을 충족 하는 행만 반환 되 고 필터링을 하지 않고 메모리에서 수행 해야 합니다.
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample16.sql)]
> 
> (다음 자습서에는 SQL Server로 전송 하는 쿼리를 검사 하는 방법을 설명 합니다.)


다음 섹션에는 데이터베이스에서이 작업을 수행 해야는 지정할 수 있도록 하는 리포지토리 메서드를 구현 하는 방법을 보여 줍니다.

이제 컨트롤러 및 Entity Framework 데이터베이스 컨텍스트 간에 추상화 계층을 만들었습니다. 이 응용 프로그램을 사용 하 여 테스트 자동화 된 단위를 수행 하려는 경우 구현 하는 단위 테스트 프로젝트에는 대체 리포지토리 클래스를 만들 수 있습니다 `IStudentRepository` *합니다.* 데이터 읽기 및 쓰기에 컨텍스트를 호출 하지 않고이 모의 리포지토리 클래스는 컨트롤러 함수를 테스트 하기 위해 메모리 내 컬렉션을 조작할 수 있습니다.

## <a name="implement-a-generic-repository-and-a-unit-of-work-class"></a>제네릭 리포지토리 및 작업 클래스의 단위를 구현 합니다.

중복 코드를 많이 발생할 수 있습니다 각 엔터티 형식에 대 한 리포지토리 클래스 만들기 및 부분적으로 업데이트 될 수 있습니다. 예를 들어, 두 가지 엔터티 형식이 동일한 트랜잭션의 일부로 업데이트 해야 합니다. 별도 데이터베이스 컨텍스트 인스턴스를 사용 하는 각 경우 성공할 수 하나 및 다른 실패할 수 있습니다. 중복 코드를 최소화 하는 한 가지 방법은 제네릭 리포지토리 및 확인 방법 중 하나를 사용 하는 작업 클래스의 단위를 사용 하는 모든 리포지토리는 동일한 데이터베이스 컨텍스트를 사용 하 여 (및 따라서 모든 업데이트를 조정할) 됩니다.

자습서의이 섹션에서는 만듭니다는 `GenericRepository` 클래스 및 `UnitOfWork` 클래스를 사용 하는 `Course` 둘 다에 액세스 하기 위해 컨트롤러는 `Department` 및 `Course` 엔터티 집합. 앞에서 설명한 대로 단순하게 유지 하기 위해이 자습서의이 부분에서 이러한 클래스에 인터페이스를 만드는 되지 않습니다. TDD를 용이 하 게 사용 하려는 경우 사용자는 일반적으로 구현는 인터페이스를 사용 하 여 수행한 동일한 방식으로 `Student` 리포지토리.

### <a name="create-a-generic-repository"></a>제네릭 리포지토리 만들기

에 *DAL* 폴더를 만들기 *GenericRepository.cs* 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample17.cs)]

엔터티 집합에 대 한 저장소 인스턴스화되는 한 데이터베이스 컨텍스트에 대 한 클래스 변수 선언 됩니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample18.cs)]

생성자는 데이터베이스 컨텍스트 인스턴스를 받아들이고 엔터티 집합 변수를 초기화 합니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample19.cs)]

`Get` 메서드 호출 코드에서 결과 정렬 하는 열과 필터 조건을 지정을 허용 하도록 람다 식을 사용 하 고 문자열 매개 변수를 호출자에 게 즉시 로드에 대 한 탐색 속성의 쉼표로 구분 된 목록을 제공 합니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample20.cs)]

코드 `Expression<Func<TEntity, bool>> filter` 호출자를 기반으로 하는 람다 식을 제공할는 의미는 `TEntity` 형식 및이 식은 부울 값을 반환 합니다. 예를 들어 저장소에 대해 인스턴스화된 합니다 `Student` 엔터티 형식에 호출 메서드에 있는 코드를 지정할 수 있습니다 `student => student.LastName == "Smith` &quot; 에 대 한는 `filter` 매개 변수입니다.

코드 `Func<IQueryable<TEntity>, IOrderedQueryable<TEntity>> orderBy` 또한 호출자는 람다 식을 제공 합니다. 이지만 경우 식에 대 한 입력을 `IQueryable` 개체에 대 한는 `TEntity` 형식입니다. 식의 정렬된 된 버전을 반환 합니다 `IQueryable` 개체입니다. 예를 들어 저장소에 대해 인스턴스화된 합니다 `Student` 엔터티 형식에 호출 메서드에 있는 코드를 지정할 수 있습니다 `q => q.OrderBy(s => s.LastName)` 에 대 한는 `orderBy` 매개 변수입니다.

코드를 `Get` 메서드를 만듭니다는 `IQueryable` 를 있으면 필터 식을 적용 하는 개체:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample21.cs)]

그런 다음 쉼표로 구분 된 목록을 구문 분석 한 후 즉시 로드 식을 적용 됩니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample22.cs)]

마지막으로 적용 됩니다는 `orderBy` 식이 있는 경우 결과 반환 합니다. 그렇지 않은 경우 순서가 지정 되지 않은 쿼리의 결과 반환 하기:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample23.cs)]

호출 하는 경우는 `Get` 메서드를 필터링 및 정렬을 수행할 수 있습니다는 `IEnumerable` 이러한 함수에 대 한 매개 변수를 제공 하는 대신 메서드에 의해 반환 된 컬렉션입니다. 있지만 정렬 및 필터링 작업은 다음 웹 서버의 메모리에 합니다. 이러한 매개 변수를 사용 하 여 웹 서버 대신 데이터베이스에서 작업 했는지 확인 합니다. 대안은 특정 엔터티 형식에 대 한 파생된 클래스를 만들고 추가 특수 `Get` 메서드를 같은 `GetStudentsInNameOrder` 또는 `GetStudentsByName`합니다. 그러나 복잡 한 응용 프로그램에서는이 발생할 수 있습니다 많은 수의 파생 된 클래스 및 유지 하기 위해 더 많은 작업을 수 있는 특수 메서드를 이러한.

코드를 `GetByID`, `Insert`, 및 `Update` 메서드는 제네릭이 아닌 저장소에서 살펴본 내용과 비슷합니다. (에 선행 로딩 매개 변수를 제공 하지 않습니다는 `GetByID` 시그니처를 사용 하 여 즉시 로드를 수행할 수 없으므로 `Find` 메서드.)

두 오버 로드에 제공 되는 `Delete` 메서드:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample24.cs)]

삭제할 엔터티 ID만 전달이 사용 중 및 엔터티 인스턴스를 사용 하는 하나입니다. 볼 수 있듯이 합니다 [동시성 처리](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) 동시성 처리가 필요에 대 한 자습서는 `Delete` 메서드는 엔터티 인스턴스를 사용 하는 추적 속성의 원래 값을 포함 합니다.

이 제네릭 리포지토리는 일반적인 CRUD 요구 사항을 처리 합니다. 특정 엔터티 형식에 더 복잡 한 필터링 또는 정렬과, 같은 특별 한 요구 사항에 해당 형식에 대 한 추가 메서드는 파생된 된 클래스를 만들 수 있습니다.

## <a name="creating-the-unit-of-work-class"></a>작업 클래스의 단위 만들기

작업 클래스의 단위는 한 가지 목적은: 되도록 하는 여러 리포지토리를 사용 하는 경우, 단일 데이터베이스 컨텍스트를 공유 합니다. 하나의 작업 단위로 완료 되 면 이런 방식으로 호출할 수 있습니다는 `SaveChanges` 컨텍스트의 인스턴스에서 해당 메서드는 관련 된 모든 변경 내용이 조정 됩니다을 보장할 수. 클래스 요구 되는 모든는 `Save` 메서드 및 각 리포지토리에 대 한 속성입니다. 각 저장소 속성에는 동일한 데이터베이스 컨텍스트 인스턴스를 사용 하 여 다른 저장소 인스턴스로 인스턴스화된 리포지토리 인스턴스를 반환 합니다.

에 *DAL* 폴더를 라는 클래스 파일을 만듭니다 *UnitOfWork.cs* 템플릿 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample25.cs)]

코드는 데이터베이스 컨텍스트 및 각 리포지토리에 대 한 클래스 변수를 만듭니다. 에 대 한는 `context` 변수에 새 컨텍스트를 인스턴스화됩니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample26.cs)]

각 리포지토리 속성 리포지토리에 이미 있는지 여부를 확인 합니다. 그렇지 않은 경우 컨텍스트 인스턴스를 전달 하는 리포지토리를 인스턴스화합니다. 결과적으로, 모든 리포지토리는 동일한 컨텍스트 인스턴스를 공유합니다.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample27.cs)]

합니다 `Save` 메서드 호출 `SaveChanges` 데이터베이스 컨텍스트에 따라 합니다.

클래스 변수에 데이터베이스 컨텍스트를 인스턴스화하는 모든 클래스와 마찬가지로 합니다 `UnitOfWork` 구현 클래스 `IDisposable` 및 컨텍스트를 삭제 합니다.

### <a name="changing-the-course-controller-to-use-the-unitofwork-class-and-repositories"></a>UnitOfWork 클래스 및 리포지토리를 사용 하는 과정 컨트롤러를 변경 합니다.

현재에 코드를 바꿉니다 *CourseController.cs* 다음 코드를 사용 하 여:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample28.cs?highlight=15,20,22,31,54-55,70,85-86,101-102,122-124,130)]

이 코드에 대 한 클래스 변수를 추가 하 여 `UnitOfWork` 클래스입니다. (여기에 변수를 초기화 하지 않습니다. 인터페이스를 여기서 사용 된 경우;에 대해 수행한 것 처럼 두 명의 생성자 패턴을 구현 하는 대신는 `Student` 리포지토리.)

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample29.cs)]

클래스의 나머지 부분에서는 데이터베이스 컨텍스트에 대 한 모든 참조는 적절 한 리포지토리를 참조 하 여 대체를 사용 하 여 `UnitOfWork` 리포지토리에 액세스 하는 속성입니다. 합니다 `Dispose` 메서드를 삭제 합니다 `UnitOfWork` 인스턴스.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample30.cs)]

사이트를 실행 하 고 클릭 합니다 **코스** 탭 합니다.

![Courses_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image4.png)

페이지를 찾아 다른 강좌 페이지도 동일 하 게 작동 하 고 변경 내용을 이전과 동일 하 게 작동 합니다.

## <a name="summary"></a>요약

리포지토리 및 작업 패턴 단위를 모두 구현 했습니다. 제네릭 리포지토리 메서드 매개 변수로 람다 식을 사용 했습니다. 사용 하 여 이러한 식을 사용 하는 방법에 대 한 자세한 내용은 `IQueryable` 개체를 참조 하십시오 [IQueryable(T) 인터페이스 (System.Linq)](https://msdn.microsoft.com/library/bb351562.aspx) MSDN 라이브러리에서. 다음에서 자습서 일부를 처리 하는 방법을 알아봅니다 고급 시나리오를 사용 합니다.

다른 Entity Framework 리소스에 대 한 링크에서 찾을 수 있습니다 합니다 [ASP.NET 데이터 액세스 콘텐츠 맵](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.

> [!div class="step-by-step"]
> [이전](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [다음](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
