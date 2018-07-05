---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
title: Entity Framework 시나리오는 MVC 웹 응용 프로그램 (10 / 10)에 대 한 고급 | Microsoft Docs
author: tdykstra
description: Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/30/2013
ms.topic: article
ms.assetid: 64906a1d-f734-41cf-9615-ee95f8740996
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application
msc.type: authoredcontent
ms.openlocfilehash: e4e0a754163ad6b44ca02678fe6a0407e71ec3e6
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37398199"
---
<a name="advanced-entity-framework-scenarios-for-an-mvc-web-application-10-of-10"></a>MVC 웹 응용 프로그램 (10 / 10)에 대 한 고급 Entity Framework 시나리오
====================
[Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트 다운로드](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 5 Code First 및 Visual Studio 2012를 사용 하 여 ASP.NET MVC 4 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요. 시작 부분에서 자습서 시리즈를 시작할 수 있습니다 또는 [이 장이에 대 한 시작 프로젝트 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 여기에서 시작 하 고 있습니다.
> 
> > [!NOTE] 
> > 
> > 해결할 수 없는 문제가 발생 하는 경우 [완성 된 장 다운로드](building-the-ef5-mvc4-chapter-downloads.md) 문제를 재현 하려고 합니다. 일반적으로 코드의 완성 된 코드를 비교 하 여 문제에 솔루션을 찾을 수 있습니다. 몇 가지 일반적인 오류 및 해결 하는 방법에 대 한 참조 [오류 및 해결 방법입니다.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)


이전 자습서에서 리포지토리 및 작업 패턴 단위를 구현 합니다. 이 자습서에서는 다음 내용을 다룹니다.

- 원시 SQL 쿼리를 수행 합니다.
- 비 추적 쿼리를 수행 합니다.
- 쿼리를 검사 하는 데이터베이스로 전송 합니다.
- 프록시 클래스를 사용합니다.
- 변경의 자동 검색을 사용 하지 않도록 설정 합니다.
- 변경 저장할 때 유효성 검사를 사용 하지 않도록 설정 합니다.
- [오류 및 해결](#errors)

대부분의 이러한 항목에 대해 이미 만든 페이지를 사용 하 여 작업할 수 있습니다. 원시 SQL 대량 업데이트 수행을 사용 하는 데이터베이스의 모든 과정의 학점 수를 업데이트 하는 새 페이지를 만듭니다.

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

및 부서 편집 페이지에 새 유효성 검사 논리를 추가할 비 추적 쿼리를 사용 하려면:

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image2.png)

## <a name="performing-raw-sql-queries"></a>원시 SQL 쿼리 수행

Entity Framework Code First API는 SQL 명령을 데이터베이스에 직접 전달할 수 있도록 하는 메서드를 포함 합니다. 다음과 같은 옵션을 선택할 수 있습니다.

- 엔터티 형식을 반환하는 쿼리에 `DbSet.SqlQuery` 메서드를 사용합니다. 반환된 된 개체에서 예상 되는 형식 이어야 합니다는 `DbSet` 개체에 있으며 자동으로 추적할지 데이터베이스 컨텍스트에 의해 해제 하지 않으면 추적 합니다. (다음 섹션에 대 한 참조를 `AsNoTracking` 메서드.)
- 사용 된 `Database.SqlQuery` 엔터티가 아닌 형식을 반환 하는 쿼리에 대 한 메서드. 이 메서드를 사용하여 엔터티 형식을 검색하더라도 반환된 데이터는 데이터베이스 컨텍스트에 의해 추적되지 않습니다.
- 사용 된 [Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456(v=vs.103).aspx) 쿼리가 아닌 명령에 대 한 합니다.

Entity Framework를 사용할 때 장점 중 하나는 코드가 데이터를 저장하는 특정 메서드에 너무 얽매이지 않아도 된다는 점입니다. 이것은 사용자를 위한 SQL 쿼리와 명령이 생성되므로 가능하며 사용자는 코드를 직접 작성할 필요가 없습니다. 하지만 예외적인 시나리오 수동으로 만든 특정 SQL 쿼리를 실행 해야 할 때 되며 이러한 메서드 수 있도록 이러한 예외를 처리할 수 있습니다.

웹 응용 프로그램에서 SQL 명령을 실행할 때 항상 그렇듯이 SQL 삽입 공격으로부터 사이트를 보호하기 위한 예방 조치를 취해야 합니다. 이를 수행하는 한 가지 방법은 매개 변수가 있는 쿼리를 사용하여 웹 페이지에서 제출한 문자열을 SQL 명령으로 해석할 수 없도록 하는 것입니다. 이 자습서에서는 사용자 입력을 쿼리에 통합할 때 매개 변수가 있는 쿼리를 사용합니다.

### <a name="calling-a-query-that-returns-entities"></a>엔터티를 반환 하는 쿼리 호출

만든다고 합니다 `GenericRepository` 클래스 추가 필터링 및 추가 메서드를 사용 하 여 파생된 클래스를 만든다고 하지 않고도 유연 하 게 정렬를 제공 합니다. SQL 쿼리를 허용 하는 메서드를 추가 하는 것을 달성 하기 위해 하나의 방법입니다. 와 같은 컨트롤러에서 원하는 모든 종류의 필터링 또는 정렬 지정할 수 있습니다는 `Where` 는 조인이 나 하위에 의존 하는 절. 이 섹션에서는 이러한 메서드를 구현 하는 방법을 배웁니다.

만들기는 `GetWithRawSql` 메서드에 다음 코드를 추가 하 여 *GenericRepository.cs*:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs)]

*CourseController.cs*에서 새 메서드를 호출 합니다 `Details` 메서드를 다음 예제에서와 같이:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

사용한 수 있습니다이 경우에 `GetByID` 있지만 메서드를 사용 하는 `GetWithRawSql` 확인 하는 메서드를 `GetWithRawSQL` 메서드 작동 합니다.

Select 쿼리가 작동을 확인 하려면 세부 정보 페이지를 실행 (선택 합니다 **코스** 탭 차례로 **세부 정보** 하나의 강좌에 대 한).

![Course_Details_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image3.png)

### <a name="calling-a-query-that-returns-other-types-of-objects"></a>다른 형식의 개체를 반환 하는 쿼리를 호출

이전에 등록 날짜별로 학생 수를 보여주는 [정보] 페이지의 학생 통계 표를 만들었습니다. 이 수행 하는 코드 *HomeController.cs* LINQ를 사용 하 여:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs)]

LINQ를 사용 하는 것이 아니라 SQL에서 직접이 데이터를 검색 하는 코드를 작성 한다고 가정 합니다. 엔터티 개체 이외의 값을 반환 하는 쿼리를 실행 해야 할 즉 사용 해야 합니다 `Database.SqlQuery` 메서드.

*HomeController.cs*에서 LINQ 문을 대체 합니다 `About` 메서드를 다음 코드로:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

정보 페이지를 실행 합니다. 이전과 동일한 데이터가 표시됩니다.

![About_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image4.png)

### <a name="calling-an-update-query"></a>업데이트 쿼리 호출

Contoso University 관리자 대량 변경 내용이 모든 강좌에 대 한 학점 수를 변경 하는 등 데이터베이스에서 수행할 수 있으려면 가정 합니다. 대학에 과목이 많은 경우 엔터티로 모두 검색하여 개별적으로 변경하는 것은 비효율적입니다. 이 섹션의 모든 강좌에 대 한 학점 수를 변경 하는 비율을 지정 하려면 사용자를 허용 하는 웹 페이지를 구현 하 고 SQL을 실행 하 여 변경 해야 `UPDATE` 문입니다. 그러면 웹 페이지가 다음 그림과 같이 표시됩니다.

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image5.png)

이전 자습서를 사용 하는 제네릭 리포지토리 읽기 및 업데이트 `Course` 엔터티는 `Course` 컨트롤러입니다. 이 대량 업데이트 작업에 대 한 일반 저장소에 없는 새 리포지토리 메서드를 만들 해야 합니다. 이렇게 하려면 전용 만들게 `CourseRepository` 에서 파생 된 클래스는 `GenericRepository` 클래스입니다.

에 *DAL* 폴더를 만들기 *CourseRepository.cs* 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cs)]

*UnitOfWork.cs*를 변경 합니다 `Course` 에서 저장소 유형 `GenericRepository<Course>` 를 `CourseRepository:`

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.cs)]

*CourseContoller.cs*에 추가 `UpdateCourseCredits` 메서드:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

이 메서드는 둘 다 `HttpGet` 고 `HttpPost`입니다. 경우는 `HttpGet` `UpdateCourseCredits` 메서드를 실행 합니다 `multiplier` 변수는 null이 됩니다 하 고 앞의 그림에 표시 된 대로 보기는 빈 텍스트 상자와 제출 단추에 표시 됩니다.

경우는 **업데이트** 단추를 클릭 하며 `HttpPost` 메서드를 실행 `multiplier` 텍스트 상자에 입력 된 값을 갖습니다. 저장소 호출 `UpdateCourseCredits` 영향을 받는 행을 수를 반환 하는 메서드 및 해당 값에 저장 되는 `ViewBag` 개체입니다. 보기에 영향을 받는 행 수를 수신 하는 경우는 `ViewBag` 개체를 텍스트 상자 대신 해당 숫자를 표시 하 고 다음 그림에 나와 있는 것 처럼 전송 단추를 합니다.

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image6.png)

보기 만들기를 *Views\Course* 업데이트 과정 학점이 페이지에 대 한 폴더:

![Add_View_dialog_box_for_Update_Course_Credits](https://asp.net/media/2578203/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Add_View_dialog_box_for_Update_Course_Credits.png)

*Views\Course\UpdateCourseCredits.cshtml*, 템플릿 코드를 다음 코드로 바꿉니다.

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

**Courses(과정)** 탭을 선택하여 `UpdateCourseCredits` 메서드를 실행한 후 브라우저의 주소 표시줄에서 URL 끝에 "/UpdateCourseCredits"를 추가합니다(예: `http://localhost:50205/Course/UpdateCourseCredits`). 텍스트 상자에 숫자를 입력합니다.

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image7.png)

**업데이트**를 클릭합니다. 영향을 받은 행 수가 표시됩니다.

![Update_Course_Credits_rows_affected_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image8.png)

학점 수가 수정된 과정 목록을 보려면 **목록으로 돌아가기**를 클릭합니다.

![Courses_Index_page_showing_revised_credits](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image9.png)

원시 SQL 쿼리에 대 한 자세한 내용은 참조 하십시오 [원시 SQL 쿼리](https://blogs.msdn.com/b/adonet/archive/2011/02/04/using-dbcontext-in-ef-feature-ctp5-part-10-raw-sql-queries.aspx) Entity Framework 팀 블로그.

## <a name="no-tracking-queries"></a>비 추적 쿼리

데이터베이스 컨텍스트 데이터베이스 행을 검색 하 고 해당 내용을 나타내는 엔터티 개체를 만드는 기본적으로이 여부를 추적 메모리의 엔터티가 데이터베이스의 한 것으로 동기화 됩니다. 메모리의 데이터는 캐시의 역할을 하고 엔터티를 업데이트할 때 사용됩니다. 컨텍스트 인스턴스는 일반적으로 수명이 짧으며(각 요청에 대해 새 것이 만들어지고 삭제됨) 엔터티를 읽는 컨텍스트는 일반적으로 해당 엔터티가 다시 사용되기 전에 삭제되므로 이 캐싱은 웹 응용 프로그램에 종종 필요하지 않습니다.

컨텍스트를 사용 하 여 쿼리에 대 한 엔터티 개체를 추적 하는지 여부를 지정할 수 있습니다는 `AsNoTracking` 메서드. 이러한 작업을 수행할 수 있는 일반적인 시나리오는 다음을 포함합니다.

- 쿼리 추적을 해제 하면 성능을 향상 시킬 눈에 띄게 수 있는 데이터의 큰 볼륨을 검색 합니다.
- 업데이트 하기 위해 엔터티를 연결 하려고 하지만 이전 다른 목적을 위해 동일한 엔터티를 검색 합니다. 엔터티는 데이터베이스 컨텍스트에서 이미 추적 중이므로 변경하려는 엔터티를 연결할 수 없습니다. 이를 방지 하는 한 가지 방법은 사용 하는 것은 `AsNoTracking` 이전 쿼리를 사용 하 여 옵션입니다.

이 섹션에서는 이러한 시나리오의 두 번째를 보여 주는 비즈니스 논리를 구현 합니다. 특히, 강사 둘 이상의 부서의 관리자 일 수 없음을 알리는 비즈니스 규칙을 적용할 수 있습니다.

*DepartmentController.cs*에서 호출할 수 있는 새 메서드를 추가 합니다 `Edit` 및 `Create` 없는 두 부서 동일한 관리자가 있는지 확인 하는 방법.

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.cs)]

코드를 추가 합니다 `try` 블록을 `HttpPost` `Edit` 유효성 검사 오류가 없는 경우이 새 메서드를 호출 하는 방법입니다. `try` 블록은 이제 다음과 같이 표시 됩니다.

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample11.cs?highlight=9-12)]

부서 편집 페이지를 실행 하 고 다른 부서 관리자가 이미 있는 강사는 부서 관리자 변경 하 려 합니다. 예상 되는 오류 메시지가 있습니다.

![Department_Edit_page_with_duplicate_administrator_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

이제 부서 편집 페이지를 다시 및 시간 변경 내용에이 실행 합니다 **예산** 크기입니다. 클릭 하면 **저장**, 오류 페이지를 참조 하세요.

![Department_Edit_page_with_object_state_manager_error_message](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image11.png)

예외 오류 메시지는 "`An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key.`" 인해 다음과 같은 순서의 이벤트가 발생 합니다.

- 합니다 `Edit` 메서드 호출을 `ValidateOneAdministratorAssignmentPerInstructor` Kim 손 해당 관리자로 있는 모든 부서를 검색 하는 메서드. 이 경우 영어 부서를 읽을 수 됩니다. 편집 중인 부서 이기 때문에 오류가 보고 됩니다. 그러나이 읽기 작업의 결과로 데이터베이스에서 읽은 영어 부서 엔터티는 이제 추적 중인 데이터베이스 컨텍스트에 의해 합니다.
- 합니다 `Edit` 메서드를 설정 하려고 합니다.는 `Modified` 영어 플래그 부서 엔터티, MVC 모델 바인더에서 만들어지지만 컨텍스트가 영어 부서 엔터티를 이미 추적 하기 때문에 실패 합니다.

이 문제를 해결 하려면에서 유효성 검사 쿼리를 통해 검색 하는 메모리 내 부서 엔터티를 추적 컨텍스트를 유지 하는 것입니다. 이 엔터티를 업데이트 하지 때문에이 수행 하거나 메모리에 캐시 되 고 여기에서 이익이 되는 방식으로 다시 읽는 없는 단점이 있습니다.

*DepartmentController.cs*를 `ValidateOneAdministratorAssignmentPerInstructor` 메서드를 다음에 표시 된 대로 추적 안 함 지정:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample12.cs?highlight=4)]

편집 하려는 시도 반복 합니다 **예산** 부서 양입니다. 이 이번에는 작업이 완료 되 면 하 고 사이트에는 수정 된 예산 값을 표시 하 고 부서 인덱스 페이지로 예상 대로 반환 합니다.

## <a name="examining-queries-sent-to-the-database"></a>데이터베이스에 전송 하는 쿼리를 검사 합니다.

때로는 데이터베이스로 전송된 실제 SQL 쿼리를 볼 수 있는 것이 도움이 됩니다. 이렇게 하려면 디버거에서 쿼리 변수를 검사 하거나 쿼리의 호출 수를 `ToString` 메서드. 이 사용 하려면 간단한 쿼리를 확인 하 고 이러한 즉시 로드, 필터링 및 정렬 옵션을 추가 하면를 어떻게 확인 하겠습니다 합니다.

*컨트롤러/CourseController*을 대체 합니다 `Index` 메서드를 다음 코드로:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample13.cs?highlight=3)]

이제에서 중단점을 설정 *GenericRepository.cs* 에 `return query.ToList();` 및 `return orderBy(query).ToList();` 문을 `Get` 메서드. 디버그 모드에서 프로젝트를 실행 하 고 과정 인덱스 페이지를 선택 합니다. 코드에서 중단점에 도달 하면 검사를 `query` 변수입니다. SQL Server로 전송 되는 쿼리가 표시 됩니다. 단순 `Select` 문:

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample14.json)]

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

쿼리는 너무 길어서 Visual Studio에서 디버깅 창에 표시할 수 있습니다. 전체 쿼리를 확인 하려면 변수 값을 복사한 텍스트 편집기에 붙여 넣습니다.

![Copy_value_of_variable_in_debug_mode](https://asp.net/media/2578239/Windows-Live-Writer_Advanced-Entity-Framework-Scenarios-for-_CEF8_Copy_value_of_variable_in_debug_mode_0902a2b1-b799-47a6-9b4b-f266c79d83c1.png)

이제 사용자가 특정 부서에 대 한 필터링 할 수 있도록 과정 인덱스 페이지에 드롭다운 목록의 추가 합니다. 과정 제목별로 정렬 하 고 지정에 대해 즉시 로드는 `Department` 탐색 속성입니다. *CourseController.cs*을 대체 합니다 `Index` 메서드를 다음 코드로:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample15.cs)]

드롭다운 목록에서 선택한 값을 받습니다. 메서드는 `SelectedDepartment` 매개 변수입니다. 선택한 내용이 없는 경우이 매개 변수가 null이 됩니다.

`SelectList` 드롭 다운 목록에 대 한 모든 부서를 포함 하는 컬렉션 뷰에 전달 됩니다. 매개 변수가 전달 된 `SelectList` 생성자 값 필드 이름, 텍스트 필드 이름 및 선택한 항목을 지정 합니다.

에 대 한는 `Get` 메서드를 `Course` 필터 식, 정렬 순서 및 즉시 로드에 대 한 리포지토리에 코드를 지정는 `Department` 탐색 속성입니다. 필터 식은 항상 반환 `true` 드롭 다운 목록에서 아무것도 선택 하는 경우 (즉, `SelectedDepartment` null).

*Views\Course\Index.cshtml*를 열기 전에 즉시 `table` 태그 드롭 다운 목록 및 전송 단추를 만들려면 다음 코드를 추가 합니다.

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample16.cshtml)]

여전히 설정 된 중단점과 `GenericRepository` 과정 인덱스 페이지를 실행 하는 클래스입니다. 브라우저에서 페이지 표시 되도록 코드에 중단점을 적중는 처음 두 번을 계속 진행 합니다. 드롭다운 목록에서 부서를 선택 하 고 클릭 **필터**:

![Course_Index_page_with_department_selected](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

이 시간 드롭다운 목록에 대 한 부서 쿼리에 대 한 첫 번째 중단점이 됩니다. 건너뛰고 보기는 `query` 변수 다음에 코드 중단점에 도달 어떻게 표시 하기 위해는 `Course` 같습니다 쿼리 합니다. 다음과 유사한 출력이 표시 됩니다.

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample17.json)]

쿼리는 이제 표시를 `JOIN` 로드 하는 쿼리 `Department` 와 함께 데이터를 `Course` 데이터 및 포함 되어 있습니다를 `WHERE` 절.

<a id="proxyclasses"></a>

## <a name="working-with-proxy-classes"></a>프록시 클래스를 사용 하 여 작업

Entity Framework (예: 쿼리를 실행 하는 경우) 엔터티 인스턴스를 만들 때 종종 생성할 엔터티에 대 한 프록시로 작동 하는 동적으로 생성 된 파생된 형식 인스턴스로. 이 프록시 속성에 액세스할 때 자동으로 작업을 수행 하는 것에 대 한 후크를 삽입할 엔터티의 일부 가상 속성을 재정의 합니다. 예를 들어,이 메커니즘은 관계의 지연 로드를 지원 하기 위해 사용 됩니다.

프록시를 사용 하이 여가 알아야 할 필요 대부분의는 없지만 예외 사항이 있습니다.

- 일부 시나리오에서는 Entity Framework 프록시 인스턴스를 만들지 못하도록는 것이 좋습니다. 예를 들어 프록시가 아닌 인스턴스를 직렬화 하는 작업 프록시 인스턴스를 직렬화 하는 작업 보다 더 효율적일 수 있습니다.
- 사용 하 여 엔터티 클래스를 인스턴스화하는 경우는 `new` 연산자를 얻지 못한 프록시 인스턴스를 합니다. 이 지연 로드 및 자동 변경 내용 추적 같은 기능을 얻지 것을 의미 합니다. 이 일반적으로 확인 합니다. 일반적으로 필요 하지 않습니다 지연 로드 하므로 데이터베이스에 없는 새 엔터티를 만들려는 엔터티를 명시적으로 표시 하는 경우 변경 내용 추적 일반적으로 필요 하지 않습니다 및 `Added`합니다. 그러나 지연 로딩 해야이 고 변경 내용 추적을 만들면 새 엔터티 인스턴스를 사용 하 여 프록시를 사용 하 여 합니다 `Create` 메서드는 `DbSet` 클래스입니다.
- 실제 엔터티 형식이 프록시 형식에서 가져오려는 좋습니다. 사용할 수는 `GetObjectType` 메서드는 `ObjectContext` 프록시 형식 인스턴스의 실제 엔터티 형식을 가져올 클래스입니다.

자세한 내용은 [프록시를 사용 하 여 작업](https://blogs.msdn.com/b/adonet/archive/2011/02/02/using-dbcontext-in-ef-feature-ctp5-part-8-working-with-proxies.aspx) Entity Framework 팀 블로그.

## <a name="disabling-automatic-detection-of-changes"></a>변경의 자동 검색을 사용 하지 않도록 설정

Entity Framework는 엔터티의 현재 값을 원래 값과 비교하여 엔터티가 변경된 방법(즉, 데이터베이스에 전송해야 하는 업데이트)을 결정합니다. 원래 값은 엔터티가 쿼리 또는 연결 되었을 때 저장 됩니다. 자동 변경 내용 검색을 발생시키는 일부 메서드는 다음과 같습니다.

- `DbSet.Find`
- `DbSet.Local`
- `DbSet.Remove`
- `DbSet.Add`
- `DbSet.Attach`
- `DbContext.SaveChanges`
- `DbContext.GetValidationErrors`
- `DbContext.Entry`
- `DbChangeTracker.Entries`

많은 수의 엔터티를 추적 하는 경우 루프에서 여러 번 다음이 방법 중 하나 호출 하면 성능이 크게 향상 된 기능을 사용 하 여 변경 내용을 자동 검색을 일시적으로 해제 하 여 발생할 수 있습니다는 [AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled(VS.103).aspx) 속성입니다. 자세한 내용은 [자동으로 검색 되는 변경 내용을](https://blogs.msdn.com/b/adonet/archive/2011/02/06/using-dbcontext-in-ef-feature-ctp5-part-12-automatically-detecting-changes.aspx)합니다.

## <a name="disabling-validation-when-saving-changes"></a>저장할 때 유효성 검사를 사용 하지 않도록 설정 변경

호출 하는 경우는 `SaveChanges` 메서드를 기본적으로 Entity Framework의 유효성을 검사 모든 변경 된 엔터티의 모든 속성의 데이터를 데이터베이스를 업데이트 하기 전에 합니다. 많은 수의 엔터티를 업데이트 하 고 이미 확인 했으면 데이터에이 작업이 필요 하지 않습니다. 저장 하는 프로세스를 만들 수 있습니다 변경 내용을 시간이 덜 유효성 검사를 일시적으로 해제 하 여 합니다. 사용 하 여 수행할 수 있습니다 합니다 [ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled(VS.103).aspx) 속성입니다. 자세한 내용은 [유효성 검사](https://blogs.msdn.com/b/adonet/archive/2010/12/15/ef-feature-ctp5-validation.aspx)합니다.

## <a name="summary"></a>요약

이 자습서 시리즈를의 Entity Framework를 사용 하 여 ASP.NET MVC 응용 프로그램에서 완료 되었습니다. 다른 Entity Framework 리소스에 대 한 링크에서 찾을 수 있습니다 합니다 [ASP.NET 데이터 액세스 콘텐츠 맵](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.

이 작성 한 후 웹 응용 프로그램을 배포 하는 방법에 대 한 자세한 내용은 참조 하세요. [ASP.NET 배포 콘텐츠 맵](https://msdn.microsoft.com/library/bb386521.aspx) MSDN 라이브러리에서.

인증 및 권한 부여와 같은 MVC와 관련 된 기타 항목에 대 한 정보에 대 한 참조를 [MVC 권장 리소스](../../getting-started/recommended-resources-for-mvc.md)합니다.

<a id="acknowledgments"></a>

## <a name="acknowledgments"></a>감사의 글

- Tom Dykstra 작성이 자습서의 원래 버전 이며 Microsoft 웹 플랫폼 및 도구 콘텐츠 팀에서 선임 프로그래밍 작가입니다.
- [Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [ @RickAndMSFT ](http://twitter.com/RickAndMSFT)) 공동이 자습서를 작성 하 고 대부분의 EF 5 및 MVC 4에 대 한 업데이트 작업을 하지 못했습니다. Rick은 Microsoft Azure 및 MVC에 집중 프로그래밍 수석 테크니컬 합니다.
- [Rowan Miller](http://www.romiller.com) 코드 검토를 사용 하 여 지원 되는 Entity Framework 팀의 다른 멤버 및 EF 5에 대 한 자습서를 업데이트 한다면 우리가 하는 동안 발생 하는 마이그레이션 사용 하 여 다양 한 문제를 디버그 합니다.

## <a name="vb"></a>VB

자습서, 처음에 생성 하는 경우 완료 된 다운로드 프로젝트의 C# 및 VB 버전을 제공 했습니다. 이 업데이트를 사용 하 여 쉽게 시리즈 있지만 시간 제한 및 다른 우선 순위는 VB 용 그렇게 하지 않은 것으로 인해 어디서 나 시작 하려면 각 장의 C# 다운로드 가능한 프로젝트를 제공 하 고 이러한 자습서를 사용 하 여 VB 프로젝트를 작성 하 고 다른 사용자와 공유 해 주시기를 기꺼이 했습니다.

<a id="errors"></a>

## <a name="errors-and-workarounds"></a>오류 및 해결 방법

### <a name="cannot-createshadow-copy"></a>복사본을 만드는 섀도 수 없습니다.

오류 메시지:

*없습니다 만들어 섀도 복사본 'DotNetOpenAuth.OpenId' 파일이 이미 있는 경우.*

해결책:

몇 초를 기다렸다가 페이지를 새로 고칩니다.

### <a name="update-database-not-recognized"></a>데이터베이스 업데이트 아닙니다.

오류 메시지:

*' Update-database ' 용어는 cmdlet, 함수, 스크립트 파일 또는 실행 프로그램의 이름으로 인식 되지 않습니다. 이름의 철자를 확인 하거나 경로 포함 하는 경우 경로가 올바른지 확인 하 고 다시 시도 합니다.* (에서 합니다 *`Update-Database`* PMC에서 명령을 합니다.)

해결책:

Visual Studio를 끝냅니다. 프로젝트를 열어야 하 고 다시 시도 하세요.

### <a name="validation-failed"></a>유효성 검사 실패

오류 메시지:

*하나 이상의 엔터티에 대 한 유효성 검사가 실패 했습니다. 자세한 내용은 'EntityValidationErrors' 속성을 참조 하세요.* (에서 합니다 *`Update-Database`* PMC에서 명령을 합니다.)

해결책:

이 문제의 원인 중 하나는 유효성 검사 오류는 경우는 `Seed` 메서드를 실행 합니다. 참조 [시드 및 디버깅 EF (Entity Framework) Db](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) 디버깅에 대 한 팁을 `Seed` 메서드.

### <a name="http-50019-error"></a>HTTP 500.19 오류

오류 메시지:

*HTTP 오류 500.19-내부 서버 오류 요청된 된 페이지는 페이지의 관련된 구성 데이터가 잘못 되어 액세스할 수 없습니다.*

해결책:

이 오류가 발생 하는 방법 중 하나에서 복사본을 여러 개를 동일한 포트 번호를 사용 하 여 각 솔루션의 경우 일반적으로 Visual Studio의 모든 인스턴스를 종료 한 다음 프로젝트에 작업을 다시 시작 하 여이 문제를 해결할 수 있습니다. 작동 하지 않는 경우 포트 번호를 변경해 보세요. 프로젝트 파일을 마우스 오른쪽 단추로 클릭 하 고 속성을 클릭 합니다. 선택 합니다 **웹** 탭 한 다음에 포트 번호를 변경 합니다 **프로젝트 Url** 입력란.

### <a name="error-locating-sql-server-instance"></a>SQL Server 인스턴스 찾기 오류

오류 메시지:

*SQL Server에 연결을 설정 하는 동안 네트워크 관련 또는 인스턴스 관련 오류가 발생 했습니다. 서버를 찾을 수 없거나 액세스할 수 없습니다. 인스턴스 이름이 올바르고 SQL Server 원격 연결을 허용 하도록 구성 되어 있는지 확인 합니다. (공급자: SQL 네트워크 인터페이스, 오류: 26-서버/인스턴스 지정 된 찾기 오류)*

해결책:

연결 문자열을 확인 합니다. 데이터베이스를 수동으로 삭제 하는 경우 생성 문자열에서 데이터베이스의 이름을 변경 합니다.

> [!div class="step-by-step"]
> [이전](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)
> [다음](building-the-ef5-mvc4-chapter-downloads.md)
