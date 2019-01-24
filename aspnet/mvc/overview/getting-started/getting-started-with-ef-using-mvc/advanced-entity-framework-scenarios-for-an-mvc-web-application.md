---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application
title: '자습서: MVC 5 웹 앱에 대 한 고급 EF 시나리오에 대해 알아봅니다'
description: 이 자습서는 Entity Framework Code First를 사용 하는 ASP.NET 웹 응용 프로그램 개발의 기본 개념을 넘어 때 알아야 할 유용한 몇 가지 항목을 소개 합니다.
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: f35a9b0c-49ef-4cde-b06d-19d1543feb0b
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application
msc.type: authoredcontent
ms.openlocfilehash: ff480f7e8c2801fcb6a64c37d95e7e15467acde6
ms.sourcegitcommit: ebf4e5a7ca301af8494edf64f85d4a8deb61d641
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54837496"
---
# <a name="tutorial-learn-about-advanced-ef-scenarios-for-an-mvc-5-web-app"></a>자습서: MVC 5 웹 앱에 대 한 고급 EF 시나리오에 대해 알아봅니다

이전 자습서에서 계층당 하나의 테이블 상속을 구현 했습니다. 이 자습서는 Entity Framework Code First를 사용 하는 ASP.NET 웹 응용 프로그램 개발의 기본 개념을 넘어 때 알아야 할 유용한 몇 가지 항목을 소개 합니다. 첫 번째 몇 가지 섹션을 설정 하는 코드를 단계별로 안내 하는 단계별 지침이 및 링크 뒤에 자세한 내용을 관한 리소스에 대 한 간략 한 소개를 사용 하 여 여러 항목을 소개 이어지는 작업을 완료 하려면 Visual Studio를 사용 하 여 합니다.

대부분의 이러한 항목에 대해 이미 만든 페이지를 사용 하 여 작업할 수 있습니다. 원시 SQL 대량 업데이트 수행을 사용 하는 데이터베이스의 모든 과정의 학점 수를 업데이트 하는 새 페이지를 만듭니다.

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * 원시 SQL 쿼리를 수행 합니다.
> * 비 추적 쿼리를 수행 합니다.
> * 검사 SQL 데이터베이스에 전송 하는 쿼리

또한에 대해 알아봅니다.

> [!div class="checklist"]
> * 추상화 계층 만들기
> * 프록시 클래스
> * 자동 변경 내용 검색
> * 자동 유효성 검사
> * Entity Framework 파워 도구
> * Entity Framework 소스 코드

## <a name="prerequisite"></a>필수 조건

* [상속 구현](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="perform-raw-sql-queries"></a>원시 SQL 쿼리를 수행 합니다.

Entity Framework Code First API는 SQL 명령을 데이터베이스에 직접 전달할 수 있도록 하는 메서드를 포함 합니다. 다음과 같은 옵션을 선택할 수 있습니다.

- 사용 된 [DbSet.SqlQuery](https://msdn.microsoft.com/library/system.data.entity.dbset.sqlquery.aspx) 엔터티 형식을 반환 하는 쿼리에 대 한 메서드. 반환된 된 개체에서 예상 되는 형식 이어야 합니다는 `DbSet` 개체에 있으며 자동으로 추적할지 데이터베이스 컨텍스트에 의해 해제 하지 않으면 추적 합니다. (다음 섹션에 대 한 참조를 [AsNoTracking](https://msdn.microsoft.com/library/system.data.entity.dbextensions.asnotracking.aspx) 메서드.)
- 사용 된 [Database.SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery.aspx) 엔터티가 아닌 형식을 반환 하는 쿼리에 대 한 메서드. 이 메서드를 사용하여 엔터티 형식을 검색하더라도 반환된 데이터는 데이터베이스 컨텍스트에 의해 추적되지 않습니다.
- 사용 된 [Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456.aspx) 쿼리가 아닌 명령에 대 한 합니다.

Entity Framework를 사용할 때 장점 중 하나는 코드가 데이터를 저장하는 특정 메서드에 너무 얽매이지 않아도 된다는 점입니다. 이것은 사용자를 위한 SQL 쿼리와 명령이 생성되므로 가능하며 사용자는 코드를 직접 작성할 필요가 없습니다. 하지만 예외적인 시나리오 수동으로 만든 특정 SQL 쿼리를 실행 해야 할 때 되며 이러한 메서드 수 있도록 이러한 예외를 처리할 수 있습니다.

웹 애플리케이션에서 SQL 명령을 실행할 때 항상 그렇듯이 SQL 삽입 공격으로부터 사이트를 보호하기 위한 예방 조치를 취해야 합니다. 이를 수행하는 한 가지 방법은 매개 변수가 있는 쿼리를 사용하여 웹 페이지에서 제출한 문자열을 SQL 명령으로 해석할 수 없도록 하는 것입니다. 이 자습서에서는 사용자 입력을 쿼리에 통합할 때 매개 변수가 있는 쿼리를 사용합니다.

### <a name="calling-a-query-that-returns-entities"></a>엔터티를 반환 하는 쿼리 호출

합니다 [DbSet&lt;TEntity&gt; ](https://msdn.microsoft.com/library/gg696460.aspx) 형식의 엔터티를 반환 하는 쿼리를 실행 하는 데 사용할 수 있는 메서드를 제공 하는 클래스 `TEntity`합니다. 코드를 변경 하면 작동 방식을 보려면 합니다 `Details` 메서드는 `Department` 컨트롤러입니다.

*DepartmentController.cs*의 `Details` 메서드를 대체 합니다 `db.Departments.FindAsync` 메서드 호출을 `db.Departments.SqlQuery` 메서드 호출을 다음 강조 표시 된 코드에 표시 된 대로:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs?highlight=8-14)]

새 코드가 올바르게 작동하는지 확인하려면 **부서** 탭을 선택한 후 부서 중 하나에 대해 **세부 정보**를 선택합니다. 예상 대로 표시 하는 모든 데이터가 있는지 확인 합니다.

### <a name="calling-a-query-that-returns-other-types-of-objects"></a>다른 형식의 개체를 반환 하는 쿼리를 호출

이전에 등록 날짜별로 학생 수를 보여주는 [정보] 페이지의 학생 통계 표를 만들었습니다. 이 수행 하는 코드 *HomeController.cs* LINQ를 사용 하 여:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

LINQ를 사용 하는 것이 아니라 SQL에서 직접이 데이터를 검색 하는 코드를 작성 한다고 가정 합니다. 엔터티 개체 이외의 값을 반환 하는 쿼리를 실행 해야 할 즉 사용 해야 합니다 [Database.SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery(v=VS.103).aspx) 메서드.

*HomeController.cs*에서 LINQ 문을 대체 합니다 `About` 다음 강조 표시 된 코드에 표시 된 대로 SQL 문 사용 하 여 메서드:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs?highlight=3-18)]

정보 페이지를 실행 합니다. 이전과 동일한 데이터를 표시 하는지 확인 합니다.

### <a name="calling-an-update-query"></a>업데이트 쿼리 호출

Contoso University 관리자 대량 변경 내용이 모든 강좌에 대 한 학점 수를 변경 하는 등 데이터베이스에서 수행할 수 있으려면 가정 합니다. 대학에 과목이 많은 경우 엔터티로 모두 검색하여 개별적으로 변경하는 것은 비효율적입니다. 이 섹션의 모든 강좌에 대 한 학점 수를 변경 하는 비율을 지정 하려면 사용자를 사용 하도록 설정 하는 웹 페이지를 구현 하 고 SQL을 실행 하 여 변경 해야 `UPDATE` 문입니다. 

*CourseContoller.cs*에 추가 `UpdateCourseCredits` 메서드를 `HttpGet` 고 `HttpPost`:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

컨트롤러를 처리 하는 경우는 `HttpGet` 요청에 아무 것도 반환에 `ViewBag.RowsAffected` 변수와 뷰에 빈 텍스트 상자와 제출 단추가 표시 됩니다.

경우는 **업데이트** 단추를 클릭 합니다 `HttpPost` 메서드를 호출 및 `multiplier` 텍스트 상자에 입력 된 값에 합니다. 코드에는 다음 과정을 업데이트 하 고 보기에 영향을 받는 행 수를 반환 하는 SQL 실행을 `ViewBag.RowsAffected` 변수입니다. 뷰는 해당 변수에 값을 가져옵니다, 텍스트 상자 대신 업데이트 된 행의 수를 표시 하 고 제출 단추.

*CourseController.cs*, 중 하나를 마우스 오른쪽 단추로 클릭 합니다 `UpdateCourseCredits` 메서드 및 클릭 **뷰 추가**합니다. 합니다 **뷰 추가** 대화 상자가 나타납니다. 기본값은 그대로 두고 선택 **추가**합니다.

*Views\Course\UpdateCourseCredits.cshtml*, 템플릿 코드를 다음 코드로 바꿉니다.

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cshtml)]

**Courses(과정)** 탭을 선택하여 `UpdateCourseCredits` 메서드를 실행한 후 브라우저의 주소 표시줄에서 URL 끝에 "/UpdateCourseCredits"를 추가합니다(예: `http://localhost:50205/Course/UpdateCourseCredits`). 텍스트 상자에 숫자를 입력합니다.

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

**업데이트**를 클릭합니다. 영향을 받는 행 수가 표시 됩니다.

학점 수가 수정된 과정 목록을 보려면 **목록으로 돌아가기**를 클릭합니다.

원시 SQL 쿼리에 대 한 자세한 내용은 참조 하십시오 [원시 SQL 쿼리](https://msdn.microsoft.com/data/jj592907) MSDN에 있습니다.

## <a name="no-tracking-queries"></a>비 추적 쿼리

데이터베이스 컨텍스트가 테이블 행을 검색하고 해당 내용을 나타내는 엔터티 개체를 만드는 경우 기본적으로 메모리의 엔터티가 데이터베이스의 해당 내용과 동기화 상태인지 여부의 추적을 유지합니다. 메모리의 데이터는 캐시의 역할을 하고 엔터티를 업데이트할 때 사용됩니다. 컨텍스트 인스턴스는 일반적으로 수명이 짧으며(각 요청에 대해 새 것이 만들어지고 삭제됨) 엔터티를 읽는 컨텍스트는 일반적으로 해당 엔터티가 다시 사용되기 전에 삭제되므로 이 캐싱은 웹 애플리케이션에 종종 필요하지 않습니다.

사용 하 여 메모리에서 엔터티 개체의 추적을 해제할 수는 [AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx) 메서드. 이러한 작업을 수행할 수 있는 일반적인 시나리오는 다음을 포함합니다.

- 쿼리 추적을 해제 하면 성능을 향상 시킬 눈에 띄게 수 있는 데이터의 큰 볼륨을 검색 합니다.
- 업데이트 하기 위해 엔터티를 연결 하려고 하지만 이전 다른 목적을 위해 동일한 엔터티를 검색 합니다. 엔터티는 데이터베이스 컨텍스트에서 이미 추적 중이므로 변경하려는 엔터티를 연결할 수 없습니다. 이 상황을 처리 하는 한 가지 방법은 사용 하는 것은 `AsNoTracking` 이전 쿼리를 사용 하 여 옵션입니다.

사용 하는 방법을 보여 주는 예는 [AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx) 메서드를 참조 하십시오 [이 자습서의 이전 버전](../../older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application.md)합니다. 필요 하지 않습니다 자습서의이 버전 편집 메서드에서 모델 바인더를 만들 엔터티의 수정 된 플래그를 설정 하지 `AsNoTracking`합니다.

## <a name="examine-sql-sent-to-database"></a>데이터베이스에 전송 된 SQL 검사

때로는 데이터베이스로 전송된 실제 SQL 쿼리를 볼 수 있는 것이 도움이 됩니다. 이전 자습서에서 인터셉터 코드에서 작업을 수행 하는 방법을 살펴보았습니다. 이제 인터셉터 코드를 작성 하지 않고도 작업을 수행 하는 몇 가지 방법을 볼 수 있습니다. 이 사용 하려면 간단한 쿼리를 확인 하 고 이러한 즉시 로드, 필터링 및 정렬 옵션을 추가 하면를 어떻게 확인 하겠습니다 합니다.

*컨트롤러/CourseController*, 대체를 `Index` 메서드를 다음 코드로 즉시 로드를 일시적으로 중지 하려면:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

이제에 중단점을 설정 합니다 `return` 문 (해당 줄에 커서를 놓고 F9). 키를 눌러 **F5** 디버그 모드에서 프로젝트를 실행 하 고 과정 인덱스 페이지를 선택 합니다. 코드에서 중단점에 도달 하면 검사를 `sql` 변수입니다. SQL Server로 전송 되는 쿼리가 표시 됩니다. 단순 `Select` 문입니다.

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.json)]

쿼리를 확인 하려면 돋보기를 클릭 합니다 **텍스트 시각화 도우미**합니다.

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

이제 사용자가 특정 부서에 대 한 필터링 할 수 있도록 과정 인덱스 페이지에 드롭다운 목록의 추가 합니다. 과정 제목별로 정렬 하 고 지정에 대해 즉시 로드는 `Department` 탐색 속성입니다.

*CourseController.cs*을 대체 합니다 `Index` 메서드를 다음 코드로:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

중단점에서 복원 된 `return` 문.

드롭다운 목록에서 선택한 값을 받습니다. 메서드는 `SelectedDepartment` 매개 변수입니다. 선택한 내용이 없는 경우이 매개 변수가 null이 됩니다.

`SelectList` 드롭 다운 목록에 대 한 모든 부서를 포함 하는 컬렉션 뷰에 전달 됩니다. 매개 변수가 전달 된 `SelectList` 생성자 값 필드 이름, 텍스트 필드 이름 및 선택한 항목을 지정 합니다.

에 대 한는 `Get` 메서드를 `Course` 필터 식, 정렬 순서 및 즉시 로드에 대 한 리포지토리에 코드를 지정는 `Department` 탐색 속성입니다. 필터 식은 항상 반환 `true` 드롭 다운 목록에서 아무것도 선택 하는 경우 (즉, `SelectedDepartment` null).

*Views\Course\Index.cshtml*를 열기 전에 즉시 `table` 태그 드롭 다운 목록 및 전송 단추를 만들려면 다음 코드를 추가 합니다.

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

중단점을 사용 하 여 설정 여전히 과정 인덱스 페이지를 실행 합니다. 브라우저에서 페이지 표시 되도록 코드 중단점을 적중 하는 첫 번째 시간을 계속 진행 합니다. 드롭다운 목록에서 부서를 선택 하 고 클릭 **필터**합니다.

이 시간 드롭다운 목록에 대 한 부서 쿼리에 대 한 첫 번째 중단점이 됩니다. 건너뛰고 보기는 `query` 변수 다음에 코드 중단점에 도달 어떻게 표시 하기 위해는 `Course` 같습니다 쿼리 합니다. 다음과 유사한 출력이 표시 됩니다.

[!code-sql[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.sql)]

쿼리는 이제 표시를 `JOIN` 로드 하는 쿼리 `Department` 와 함께 데이터를 `Course` 데이터 및 포함 되어 있습니다를 `WHERE` 절.

제거 된 `var sql = courses.ToString()` 줄.

## <a name="create-an-abstraction-layer"></a>추상화 계층을 만들려면

대부분의 개발자는 리포지토리 및 작업 패턴 단위를 구현하기 위한 코드를 Entity Framework에서 작동하는 코드를 둘러싼 래퍼로 작성합니다. 이러한 패턴은 애플리케이션의 데이터 액세스 계층 및 비즈니스 논리 계층 간에 추상화 계층을 만드는 데 사용됩니다. 이러한 패턴을 구현하면 데이터 저장소의 변경 내용으로부터 애플리케이션을 격리할 수 있으며 자동화된 단위 테스트 또는 TDD(테스트 중심 개발)를 용이하게 수행할 수 있습니다. 그러나 이러한 패턴을 구현 하는 추가 코드를 작성 아닙니다 항상 여러 가지 이유로 EF를 사용 하는 응용 프로그램에 적합 합니다.

- EF 컨텍스트 클래스 자체에서 데이터 저장소별 코드로부터 사용자 코드를 격리합니다.
- EF 컨텍스트 클래스는 EF를 사용하여 수행하는 데이터베이스 업데이트에 대해 작업 단위 클래스로 사용될 수 있습니다.
- Entity Framework 6에서 도입 된 기능 쉽게 리포지토리 코드를 작성 하지 않고도 TDD를 구현 합니다.

리포지토리 및 작업 패턴 단위를 구현 하는 방법에 대 한 자세한 내용은 참조 하세요. [이 자습서 시리즈의 Entity Framework 5 버전](../../older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)합니다. Entity Framework 6에서 TDD를 구현 하는 방법에 대 한 자세한 내용은 다음 리소스를 참조 합니다.

- [사용 하는 방법을 EF6 모의 Dbset 쉽게](http://thedatafarm.com/data-access/how-ef6-enables-mocking-dbsets-more-easily/)
- [모의 프레임 워크를 사용 하 여 테스트](https://msdn.microsoft.com/data/dn314429)
- [사용자 고유의 test double을 사용 하 여 테스트](https://msdn.microsoft.com/data/dn314431)

<a id="proxies"></a>

## <a name="proxy-classes"></a>프록시 클래스

Entity Framework (예: 쿼리를 실행 하는 경우) 엔터티 인스턴스를 만들 때 종종 생성할 엔터티에 대 한 프록시로 작동 하는 동적으로 생성 된 파생된 형식 인스턴스로. 예를 들어, 다음 두 가지 디버거 이미지를 참조 하세요. 첫 번째 이미지에는 `student` 변수가 필요한 `Student` 엔터티를 인스턴스화한 후에 즉시를 입력 합니다. 두 번째 이미지에서는 EF 데이터베이스에서 학생 엔터티를 읽는 데 사용 된 프록시 클래스를 표시 됩니다.

![프록시 클래스 하기 전에](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

![프록시 클래스 뒤](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

이 프록시 클래스 속성에 액세스할 때 자동으로 작업을 수행 하는 것에 대 한 후크를 삽입할 엔터티의 일부 가상 속성을 재정의 합니다. 이 메커니즘에 사용 되는 하나의 함수는 지연 로드 합니다.

프록시를 사용 하이 여가 알아야 할 필요 대부분의는 없지만 예외 사항이 있습니다.

- 일부 시나리오에서는 Entity Framework 프록시 인스턴스를 만들지 못하도록는 것이 좋습니다. 예를 들어, 엔터티를 직렬화 하는 경우 일반적으로 원하는 poco 프록시 클래스에 없습니다. 에 표시 된 대로 serialization 문제를 방지 하는 한 가지 방법은 데이터 전송 개체 (Dto) 대신 엔터티 개체를 serialize 하는 것은 [Entity Framework를 사용 하 여 웹 API를 사용 하 여](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-1.md) 자습서입니다. 두 번째 방법은 [프록시 생성을 사용 하지 않도록 설정](https://msdn.microsoft.com/data/jj592886.aspx)합니다.
- 사용 하 여 엔터티 클래스를 인스턴스화하는 경우는 `new` 연산자를 얻지 못한 프록시 인스턴스를 합니다. 이 지연 로드 및 자동 변경 내용 추적 같은 기능을 얻지 것을 의미 합니다. 이 일반적으로 확인 합니다. 일반적으로 필요 하지 않습니다 지연 로드 하므로 데이터베이스에 없는 새 엔터티를 만들려는 엔터티를 명시적으로 표시 하는 경우 변경 내용 추적 일반적으로 필요 하지 않습니다 및 `Added`합니다. 그러나 지연 로딩 해야이 고 변경 내용 추적을 만들면 새 엔터티 인스턴스를 사용 하 여 프록시를 사용 하 여는 [Create](https://msdn.microsoft.com/library/gg679504.aspx) 메서드를 `DbSet` 클래스.
- 실제 엔터티 형식이 프록시 형식에서 가져오려는 좋습니다. 사용할 수는 [GetObjectType](https://msdn.microsoft.com/library/system.data.objects.objectcontext.getobjecttype.aspx) 메서드는 `ObjectContext` 프록시 형식 인스턴스의 실제 엔터티 형식을 가져올 클래스입니다.

자세한 내용은 [프록시를 사용 하 여 작업](https://msdn.microsoft.com/data/JJ592886.aspx) MSDN에서.

## <a name="automatic-change-detection"></a>자동 변경 내용 검색

Entity Framework는 엔터티의 현재 값을 원래 값과 비교하여 엔터티가 변경된 방법(즉, 데이터베이스에 전송해야 하는 업데이트)을 결정합니다. 원래 값은 엔터티가 쿼리 또는 연결될 때 저장됩니다. 자동 변경 내용 검색을 발생시키는 일부 메서드는 다음과 같습니다.

- `DbSet.Find`
- `DbSet.Local`
- `DbSet.Remove`
- `DbSet.Add`
- `DbSet.Attach`
- `DbContext.SaveChanges`
- `DbContext.GetValidationErrors`
- `DbContext.Entry`
- `DbChangeTracker.Entries`

많은 수의 엔터티를 추적 하는 경우 루프에서 여러 번 다음이 방법 중 하나 호출 하면 성능이 크게 향상 된 기능을 사용 하 여 변경 내용을 자동 검색을 일시적으로 해제 하 여 발생할 수 있습니다는 [AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled.aspx) 속성입니다. 자세한 내용은 [자동으로 검색 되는 변경 내용을](https://msdn.microsoft.com/data/jj556205) MSDN에서.

## <a name="automatic-validation"></a>자동 유효성 검사

호출 하는 경우는 `SaveChanges` 메서드를 기본적으로 Entity Framework의 유효성을 검사 모든 변경 된 엔터티의 모든 속성의 데이터를 데이터베이스를 업데이트 하기 전에 합니다. 많은 수의 엔터티를 업데이트 하 고 이미 확인 했으면 데이터에이 작업이 필요 하지 않습니다. 저장 하는 프로세스를 만들 수 있습니다 변경 내용을 시간이 덜 유효성 검사를 일시적으로 해제 하 여 합니다. 사용 하 여 수행할 수 있습니다 합니다 [ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled.aspx) 속성입니다. 자세한 내용은 [유효성 검사](https://msdn.microsoft.com/data/gg193959) MSDN에 있습니다.

## <a name="entity-framework-power-tools"></a>Entity Framework 파워 도구

[Entity Framework 파워 도구가](https://marketplace.visualstudio.com/items?itemName=ErikEJ.EntityFramework6PowerToolsCommunityEdition) 되는 Visual Studio 추가 기능으로 데이터 모델 다이어그램을 만드는 데 사용 된이 자습서에서 표시 합니다. 도구는 엔터티 클래스를 생성 하는 같은 테이블을 기반으로 기존 데이터베이스에서 Code First를 사용 하 여 데이터베이스를 사용할 수 있도록 하는 다른 함수를 수행할 수도 있습니다. 도구를 설치한 후에 몇 가지 추가 옵션이 상황에 맞는 메뉴에 나타납니다. 컨텍스트 클래스의 마우스 예를 들어 **솔루션 탐색기**를 표시 하 고 **Entity Framework** 옵션입니다. 이 다이어그램을 생성 하는 기능을 제공 합니다. Code First를 사용할 때 데이터 모델 다이어그램을 변경할 수 없지만 쉽게 이해할 수 있도록 항목을 이동할 수 있습니다.

![EF 다이어그램](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image15.png)

## <a name="entity-framework-source-code"></a>Entity Framework 소스 코드

Entity Framework 6에 대 한 소스 코드에서 제공 됩니다 [GitHub](https://github.com/aspnet/EntityFramework6)합니다. 버그를 제출할 수 있습니다 하 고 EF 소스 코드에 고유한 향상 된 기능에 기여할 수 있습니다.

소스 코드가 오픈 소스 이기는 하지만 Entity Framework는 Microsoft 제품으로 완전히 지원 됩니다. Microsoft Entity Framework 팀이 어떤 참가자를 수락할지 관리하고 각 릴리스의 품질을 보장하기 위해 모든 코드 변경 내용을 테스트합니다.

## <a name="acknowledgments"></a>감사의 글

- Tom Dykstra이이 자습서의 원래 버전을 작성 하 고, EF 5 업데이트 공동 작성, EF 6 업데이트를 작성 했습니다. Tom은 Microsoft 웹 플랫폼 및 도구 콘텐츠 팀에서 선임 프로그래밍 작가입니다.
- [Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [ @RickAndMSFT ](http://twitter.com/RickAndMSFT)) 대부분의 자습서 5 EF 및 MVC 4에 대 한 업데이트 작업이 고 EF 6 업데이트를 공동 저술 했습니다. Rick은 Microsoft Azure 및 MVC에 집중 프로그래밍 수석 테크니컬 합니다.
- [Rowan Miller](http://www.romiller.com) 코드 검토를 사용 하 여 지원 되는 Entity Framework 팀의 다른 멤버 및 EF 5 및 EF 6에 대 한 자습서를 업데이트 한다면 우리가 하는 동안 발생 하는 마이그레이션 사용 하 여 다양 한 문제를 디버그 합니다.

## <a name="troubleshoot-common-errors"></a>일반적인 오류 해결

### <a name="cannot-createshadow-copy"></a>복사본을 만드는 섀도 수 없습니다.

오류 메시지:

> 복사본을 만드는 섀도 수 없습니다. '&lt;filename&gt;' 파일이 이미 있는 경우.

솔루션

몇 초를 기다렸다가 페이지를 새로 고칩니다.

### <a name="update-database-not-recognized"></a>데이터베이스 업데이트 아닙니다.

오류 메시지 (에서 `Update-Database` PMC 명령을):

> ' Update-database ' 용어는 cmdlet, 함수, 스크립트 파일 또는 실행 프로그램의 이름으로 인식 되지 않습니다. 경로가 올바른지 확인한 다음 다시 시도하세요.

솔루션

Visual Studio를 끝냅니다. 프로젝트를 열어야 하 고 다시 시도 하세요.

### <a name="validation-failed"></a>유효성 검사 실패

오류 메시지 (에서 `Update-Database` PMC 명령을):

> 하나 이상의 엔터티에 대 한 유효성 검사가 실패 했습니다. 자세한 내용은 'EntityValidationErrors' 속성을 참조 하세요.

솔루션

이 문제의 원인 중 하나는 유효성 검사 오류는 경우는 `Seed` 메서드를 실행 합니다. 참조 [시드 및 디버깅 EF (Entity Framework) Db](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) 디버깅에 대 한 팁을 `Seed` 메서드.

### <a name="http-50019-error"></a>HTTP 500.19 오류

오류 메시지:

> HTTP 오류 500.19-내부 서버 오류 요청된 된 페이지는 페이지의 관련된 구성 데이터가 잘못 되어 액세스할 수 없습니다.

솔루션

이 오류가 발생 하는 방법 중 하나에서 복사본을 여러 개를 동일한 포트 번호를 사용 하 여 각 솔루션의 경우 일반적으로 Visual Studio의 모든 인스턴스를 종료 한 다음에 작업 중인 프로젝트를 다시 시작 하 여이 문제를 해결할 수 있습니다. 작동 하지 않는 경우 포트 번호를 변경해 보세요. 프로젝트 파일을 마우스 오른쪽 단추로 클릭 하 고 속성을 클릭 합니다. 선택 합니다 **웹** 탭 한 다음에 포트 번호를 변경 합니다 **프로젝트 Url** 입력란.

### <a name="error-locating-sql-server-instance"></a>SQL Server 인스턴스 찾기 오류

오류 메시지:

> SQL Server에 연결하는 중에 네트워크 관련 오류 또는 인스턴스별 오류가 발생했습니다. 서버를 찾을 수 없거나 액세스할 수 없습니다. 인스턴스 이름이 올바르고 SQL Server가 원격 연결을 허용하도록 구성되어 있는지 확인합니다. (공급자: SQL 네트워크 인터페이스, 오류: 26 - 지정된 서버/인스턴스 찾기 오류)

솔루션

연결 문자열을 확인합니다. 데이터베이스를 수동으로 삭제 하는 경우 생성 문자열에서 데이터베이스의 이름을 변경 합니다.

## <a name="get-the-code"></a>코드 가져오기

[완료 된 프로젝트 다운로드](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)

## <a name="additional-resources"></a>추가 자료

 Entity Framework를 사용 하 여 데이터를 사용 하는 방법에 대 한 자세한 내용은 참조는 [MSDN의 설명서 페이지를 EF](https://msdn.microsoft.com/data/ee712907) 및 [ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.

이 작성 한 후 웹 응용 프로그램을 배포 하는 방법에 대 한 자세한 내용은 참조 하세요. [ASP.NET 웹 배포-권장 리소스](../../../../whitepapers/aspnet-web-deployment-content-map.md) MSDN 라이브러리에서.

인증 및 권한 부여와 같은 MVC와 관련 된 기타 항목에 대 한 정보에 대 한 참조를 [ASP.NET MVC-권장 리소스](../recommended-resources-for-mvc.md)합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음을 수행했습니다.

> [!div class="checklist"]
> * 원시 SQL 쿼리를 수행합니다.
> * 비 추적 쿼리를 수행합니다.
> * 데이터베이스에 전송 하는 검사 SQL 쿼리

또한에 대해 알아보았습니다.

> [!div class="checklist"]
> * 추상화 계층 만들기
> * 프록시 클래스
> * 자동 변경 내용 검색
> * 자동 유효성 검사
> * Entity Framework 파워 도구
> * Entity Framework 소스 코드

이 자습서 시리즈를의 Entity Framework를 사용 하 여 ASP.NET MVC 응용 프로그램에서 완료 되었습니다. EF Database First에 대해 자세히 알아보려면 DB 첫 번째 자습서 시리즈를 참조 하세요.
> [!div class="nextstepaction"]
> [Entity Framework Database First](../database-first-development/setting-up-database.md)