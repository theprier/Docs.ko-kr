---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
title: ASP.NET MVC 5 (10 / 12) 응용 프로그램에서 Entity Framework 6 사용 하 여 동시성 처리 | Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 6 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/08/2014
ms.topic: article
ms.assetid: be0c098a-1fb2-457e-b815-ddca601afc65
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: b92aded80ad6b435a2409a137bb96fe4d0a726f4
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30875658"
---
<a name="handling-concurrency-with-the-entity-framework-6-in-an-aspnet-mvc-5-application-10-of-12"></a>ASP.NET MVC 5 (10 / 12) 응용 프로그램에서 Entity Framework 6 사용 하 여 동시성 처리
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트를 다운로드](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8) 또는 [PDF 다운로드](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)

> Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 6 Code First 및 Visual Studio 2013을 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조하세요.


이전 자습서에서는 데이터를 업데이트 하는 방법을 알아보았습니다. 이 자습서에는 여러 사용자가 동시에 같은 엔터티를 업데이트하는 경우 충돌을 처리하는 방법을 보여 줍니다.

작동 하는 웹 페이지를 변경 합니다는 `Department` 엔터티는 동시성 오류를 처리 하도록 합니다. 다음 그림은 동시성 충돌이 발생 한 경우 표시 되는 일부 메시지를 포함 하는 인덱스 및 Delete 페이지를 보여 줍니다.

![Department_Index_page_before_edits](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="concurrency-conflicts"></a>동시성 충돌

한 명의 사용자가 편집하기 위해 엔터티의 데이터를 표시한 다음, 다른 사용자가 첫 번째 사용자의 변경 내용이 데이터베이스에 기록되기 전에 동일한 엔터티의 데이터를 업데이트하는 경우 동시성 충돌이 발생합니다. 이러한 충돌의 감지를 활성화하지 않는 경우 누구든지 데이터베이스를 마지막으로 업데이트하면 다른 사용자의 변경 내용을 덮어씁니다. 많은 응용 프로그램에서 이 위험은 허용 가능합니다. 적은 수의 사용자 또는 적은 업데이트가 있거나 일부 변경 내용이 덮어쓰여지는지 여부가 실제로 중요하지 않은 경우 동시성에 대한 프로그래밍의 비용은 이점보다 클 수 있습니다. 이 경우 동시성 충돌을 처리하도록 응용 프로그램을 구성할 필요가 없습니다.

### <a name="pessimistic-concurrency-locking"></a>비관적 동시성 (잠금)

응용 프로그램에서 동시성 시나리오에서 실수로 인한 데이터 손실을 방지할 필요가 있는 경우 해당 작업을 수행하는 한 가지 방법은 데이터베이스 잠금을 사용하는 것입니다. 이 라고 *비관적 동시성*합니다. 예를 들어 데이터베이스에서 행을 읽기 전에 읽기 전용 또는 업데이트 액세스에 대한 잠금을 요청합니다. 업데이트 액세스에 대한 행을 잠그는 경우 변경 중인 데이터의 복사본을 가져오기 때문에 다른 사용자는 읽기 전용 또는 업데이트 액세스에 대한 행을 잠그도록 허용되지 않습니다. 읽기 전용 액세스에 대한 행을 잠그는 경우 다른 사용자도 읽기 전용에 대해 잠글 수 있지만 업데이트에 대해서는 잠글 수 없습니다.

잠금 관리에는 단점이 있습니다. 프로그램을 설정하는 데 복잡할 수 있습니다. 상당한 데이터베이스 관리 리소스가 필요하며 응용 프로그램의 사용자 수가 증가할 수록 성능 문제가 발생할 수 있습니다. 이러한 이유로 모든 데이터베이스 관리 시스템은 비관적 동시성을 지원하지 않습니다. Entity Framework,에 대 한 기본 제공 지원이 제공 하 고이 자습서에서는 구현 하는 방법을 표시 되지 않습니다.

### <a name="optimistic-concurrency"></a>낙관적 동시성

비관적 동시성을 대신 사용 하는 *낙관적 동시성*합니다. 낙관적 동시성은 동시성 충돌 발생을 허용한 다음, 그럴 경우 적절하게 반응하는 것을 의미합니다. 이한일은 변경 부서 편집 페이지를 실행 하는 예를 들어는 **예산** $0.00으로 $350,000.00에서 영어 부서에 대 한 금액입니다.

![Changing_English_dept_budget_to_100000](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

John 클릭 하기 전에 **저장**, Jane의 동일한 페이지 및 변경 내용 실행 되는 **시작 날짜** 2013 년 8 월 8 일에 필드를 2007 년 9 월 1입니다.

![Changing_English_dept_start_date_to_1999](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

John 클릭 **저장** 클릭 한 다음 jane은 인덱스 페이지에는 브라우저는 반환 될 때 그의 변경에 게 표시 하 고 첫 번째 **저장**합니다. 다음 작업은 동시성 충돌을 처리하는 방법에 따라 결정됩니다. 몇 가지 옵션에는 다음이 포함됩니다.

- 사용자가 수정한 속성의 추적을 유지하고 데이터베이스에서 해당하는 열만 업데이트할 수 있습니다. 예제 시나리오에서 서로 다른 속성이 두 사용자에 의해 업데이트되었기 때문에 데이터가 손실되지 않습니다. 다음에 영어 부서 이동, John의와 Jane의 변경 내용을 볼 수 있습니다-2013 년 8 월 8 일의 시작 날짜와 예산 0 달러입니다.

    이 업데이트의 메서드는 데이터 손실이 발생할 수 있는 충돌 수를 줄일 수 있지만 경쟁하는 변경 내용이 동일한 엔터티의 속성에 만들어지는 경우 데이터 손실을 방지할 수 없습니다. Entity Framework가 이 방식으로 작동하는지 여부는 업데이트 코드를 구현하는 방법에 따라 달라집니다. 엔터티에 대한 모든 기존 속성 값 뿐만 아니라 새 값의 추적을 유지하기 위해 많은 양의 상태를 유지 관리해야 하므로 웹 응용 프로그램에서는 종종 실용적이지 않습니다. 서버 리소스가 필요하거나 웹 페이지 자체(예: 숨겨진 필드에) 또는 쿠키에 포함되어야 하기 때문에 많은 양의 상태를 유지 관리하는 것은 응용 프로그램 성능에 영향을 줄 수 있습니다.
- John의 내용으로 덮어쓰게 Jane의 변경 하도록 할 수 있습니다. 다음에 영어 부서 이동, 2013 년 8 월 8 일을 볼 수 있습니다 및 복원 된 $350,000.00 값입니다. 이를 *클라이언트 우선* 또는 *최종 우선* 시나리오라고 합니다. (클라이언트의 모든 값은 데이터 저장소에 포함된 값에 우선합니다.) 이 섹션의 소개에서 언급했듯이 동시성 처리에 대해 아무런 코딩을 수행하지 않는 경우 이는 자동으로 발생합니다.
- 데이터베이스에서 업데이트 되 고에서 Jane의 변경을 방지할 수 있습니다. 일반적으로 오류 메시지가 표시, 그녀는 데이터의 현재 상태를 표시 하는 그녀는 여전히 있도록가 그녀의 변경 내용을 다시 적용할 수 있습니다. 이를 *저장소 우선* 시나리오라고 합니다. (데이터 저장소 값은 클라이언트에서 전송한 값에 우선합니다.) 이 자습서에서는 저장소 우선 시나리오를 구현합니다. 이 메서드는 상황에 대한 경고를 받는 사용자 없이 변경 내용을 덮어쓰지 않도록 합니다.

### <a name="detecting-concurrency-conflicts"></a>동시성 충돌 확인

처리 하 여 충돌을 해결할 수 [OptimisticConcurrencyException](https://msdn.microsoft.com/library/system.data.optimisticconcurrencyexception.aspx) Entity Framework throw 하는 예외입니다. 이러한 예외를 throw하는 시기를 확인하기 위해 Entity Framework에서 충돌을 검색할 수 있어야 합니다. 따라서 데이터베이스와 데이터 모델을 적절하게 구성해야 합니다. 충돌 검색을 활성화하기 위한 몇 가지 옵션은 다음과 같습니다.

- 데이터베이스 테이블에서 행이 변경된 시기를 확인하는 데 사용될 수 있는 추적 열을 포함합니다. Entity Framework의 해당 열을 포함 하도록 구성할 수 있습니다는 `Where` sql 절 `Update` 또는 `Delete` 명령입니다.

    추적 열의 데이터 형식이 일반적으로 [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)합니다. [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) 값은 행이 업데이트 될 때마다가 증가 하는 일련 번호입니다. 에 `Update` 또는 `Delete` 명령을 `Where` 절 추적 열 (원래 행 버전)의 원래 값이 포함 됩니다. 업데이트 되는 행의 값을 다른 사용자에 의해 변경 된 경우는 `rowversion` 열이 원래 값과 다른 하므로 `Update` 또는 `Delete` 문 때문에 업데이트할 행을 찾을 수 없습니다는 `Where` 절. 경우 Entity Framework의 행이 없는 하 여 업데이트를 찾습니다는 `Update` 또는 `Delete` 명령 (즉 때 영향을 받는 행 수는 0), 동시성 충돌 하는 해석 합니다.
- Entity Framework에서 테이블의 모든 열의 원래 값을 포함 하도록 구성 된 `Where` 절 `Update` 및 `Delete` 명령 합니다.

    첫 번째 옵션 행 주체를 읽어 먼저 이후에 변경 된 행에 아무 것도 경우와 같이 `Where` 절 반환 하지 않습니다는 행을 업데이트 하려면 Entity Framework를 동시성 충돌로 해석 합니다. 많은 열이 있는 데이터베이스 테이블에 대 한이 방법을 사용 하면 매우 큰 `Where` 절, 많은 양의 상태를 유지 관리 하는 필요할 수 있습니다. 앞에서 설명한 것처럼 많은 양의 상태를 유지 관리하는 것은 응용 프로그램 성능에 영향을 미칠 수 있습니다. 따라서 이 방법은 일반적으로 권장되지 않으며 이 자습서에서 사용되는 방법이 아닙니다.

    추가 하 여 동시성을 추적 하려는 엔터티의 모든 아닌 기본 키 속성을 표시 해야 하는 동시성이 접근 방식을 구현 않으려면는 [ConcurrencyCheck](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.concurrencycheckattribute.aspx) 특성을 해당 합니다. Entity Framework는 SQL의 모든 열을 포함 하도록 변경 하는 `WHERE` 절 `UPDATE` 문.

이 자습서의 나머지 부분에서는 추가 [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) 속성을 추적는 `Department` 엔터티를 컨트롤러와 뷰를 만들고 모든 항목이 올바르게 작동 하는지 확인 하려면 테스트 합니다.

## <a name="add-an-optimistic-concurrency-property-to-the-department-entity"></a>낙관적 동시성 속성 부서 엔터티에 추가

*Models\Department.cs*, 라는 추적 속성을 추가 `RowVersion`:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=20-22)]

[타임 스탬프](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx) 특성에이 열은 포함 되어야 함을 지정는 `Where` 절 `Update` 및 `Delete` 명령을 데이터베이스에 전송 합니다. 이 특성 이라고 [타임 스탬프](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx) 이전 버전의 SQL Server는 SQL을 사용 하기 때문에 [타임 스탬프](https://msdn.microsoft.com/library/ms182776(v=SQL.90).aspx) SQL 전에 데이터 형식 [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) 대체 했습니다. .Net 유형을 [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) 는 바이트 배열입니다.

Fluent API를 사용 하는 것을 선호 하는 경우 사용할 수 있습니다는 [IsConcurrencyToken](https://msdn.microsoft.com/library/gg679501(v=VS.103).aspx) 메서드를 다음 예제와 같이 추적 속성을 지정 합니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

속성을 추가하여 데이터베이스 모델을 변경했으므로 다른 마이그레이션을 수행해야 합니다. PMC(패키지 관리자 콘솔)에서 다음 명령을 입력합니다.

[!code-console[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cmd)]

## <a name="modify-the-department-controller"></a>부서 컨트롤러를 수정

*Controllers\DepartmentController.cs*, 추가 `using` 문:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

에 *DepartmentController.cs* 파일에서 "LastName"의 모든 4 개의 항목을 "FullName"로 변경 하 부서 관리자 드롭 다운 목록을 강의의 전체 이름이 아니라 마지막 이름만 포함 됩니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=1)]

에 대 한 기존 코드는 `HttpPost` `Edit` 메서드를 다음 코드로:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

`FindAsync` 메서드가 Null을 반환하는 경우 부서가 다른 사용자에 의해 삭제되었습니다. 표시 된 코드는 department 엔터티를 편집 페이지를 하 고 오류 메시지가 다시 표시 될 수 있도록 게시 된 양식 값을 사용 합니다. 대신 부서 필드를 다시 표시하지 않고 오류 메시지만을 표시하는 경우 부서 엔터티를 다시 만들 필요가 없습니다.

뷰 저장 원래 `RowVersion` 숨겨진된 필드와 메서드에서 값에서 받는 `rowVersion` 매개 변수입니다. `SaveChanges`를 호출하기 전에 엔터티에 대한 `OriginalValues` 컬렉션에 해당 원래 `RowVersion` 속성 값을 넣어야 합니다. Entity Framework는 SQL을 생성할 때 다음 `UPDATE` 명령, 명령 포함 됩니다는 `WHERE` 원래 있는 행을 검색 하는 절 `RowVersion` 값입니다.

행의 영향을 받는 경우는 `UPDATE` 명령 (행이 없는 원래 `RowVersion` 값), Entity Framework에서는 `DbUpdateConcurrencyException` 예외 및의 코드는 `catch` 블록 가져옵니다 영향을 받는 `Department` 예외에서 엔터티 개체입니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

이 개체에서 사용자가 입력 한 새 값에 해당 `Entity` 속성을 호출 하 여 데이터베이스에서 읽은 값을 가져올 수는 `GetDatabaseValues` 메서드.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

`GetDatabaseValues` 메서드 다른 사용자가 데이터베이스에서 행 삭제 하는 경우 null을 반환 합니다; 그렇지 않은 경우에 반환된 된 개체를 캐스팅 해야는 `Department` 에 액세스 하기 위해 클래스는 `Department` 속성입니다. (삭제 이미 확인 되었으므로 `databaseEntry` 부서 후 삭제 된 경우에 null이 될 것 `FindAsync` 실행 하기 전에 `SaveChanges` 실행 합니다.)

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

다음으로, 코드 편집 페이지에서 사용자 입력에서 다른 데이터베이스 값이 포함 된 각 열에 대 한 사용자 지정 오류 메시지를 추가 합니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

긴 오류 메시지에 발생 하는 결과 수행할 작업 항목에 대 한 설명 합니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

마지막으로 코드가 설정는 `RowVersion` 의 값은 `Department` 데이터베이스에서 검색 한 개체를 새 값입니다. 이 새로운 `RowVersion` 값은 편집 페이지가 다시 표시되고, 다음 번에 사용자가 **저장**을 클릭할 때 숨겨진 필드에 저장되고, 편집 페이지의 다시 표시로 인해 발생하는 동시성 오류만 catch됩니다.

*Views\Department\Edit.cshtml*를 저장 하는 숨겨진된 필드를 추가 하는 `RowVersion` 속성 값을 바로 다음에 대 한 숨겨진된 필드는 `DepartmentID` 속성:

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=18)]

## <a name="testing-optimistic-concurrency-handling"></a>낙관적 동시성 처리를 테스트합니다.

사이트를 실행 하 고 클릭 **부서**:

![Department_Index_page_before_edits](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

마우스 오른쪽 단추로 클릭는 **편집** 영어 부서 및 선택에 대 한 하이퍼링크 **새 탭에서 열기** 클릭는 **편집** 영어 부서에 대 한 하이퍼링크입니다. 두 개의 탭과 동일한 정보를 표시합니다.

![Department_Edit_page_before_changes](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

첫 번째 브라우저 탭의 필드를 변경하고 **저장**을 클릭합니다.

![Department_Edit_page_1_after_change](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

브라우저에 변경된 값과 인덱스 페이지가 표시됩니다.

![Departments_Index_page_after_first_budget_edit](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

두 번째 브라우저 탭에서 필드를 변경 하 고 클릭 **저장**합니다.

![Department_Edit_page_2_after_change](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

클릭 **저장** 두 번째 브라우저 탭에 있습니다. 오류 메시지가 표시됩니다.

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

**저장**을 다시 클릭합니다. 두 번째 브라우저 탭에 입력 한 값은 첫 번째 브라우저에서 변경 되는 데이터의 원래 값과 함께 저장 됩니다. 인덱스 페이지가 나타날 때 저장된 값이 표시됩니다.

![Department_Index_page_with_change_from_second_browser](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image11.png)

## <a name="updating-the-delete-page"></a>업데이트 페이지 삭제

삭제 페이지의 경우 Entity Framework는 비슷한 방식으로 부서를 편집하는 사용자에 의해 발생한 동시성 충돌을 감지합니다. 경우는 `HttpGet` `Delete` 확인 뷰를 표시 하는 메서드, 보기 포함 원래 `RowVersion` 숨겨진된 필드의 값입니다. 값은 사용할 수 있는 다음의 `HttpPost` `Delete` 메서드를 사용자가 삭제 확인 될 때 호출 됩니다. Entity Framework는 SQL을 생성할 때 `DELETE` 명령을 포함 한 `WHERE` 원래 절 `RowVersion` 값입니다. 0 개의 행에 명령 결과가 (행이 삭제 확인 페이지에 표시 된 후 변경 의미), 영향을 받는 경우 동시성 예외가 throw 되 고 `HttpGet Delete` 로 설정 하는 오류 플래그가 메서드는 `true` 다시 표시 하려면는 오류 메시지와 함께 확인 페이지입니다. 행이 없는 경우에서 다른 오류 메시지가 표시 되는 행 다른 사용자가 삭제 되었으므로 때문에 영향을 받은 수 이기도 합니다.

*DepartmentController.cs*, 대체 된 `HttpGet` `Delete` 메서드를 다음 코드로:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

메서드는 동시성 오류가 발생한 후 페이지가 다시 표시되고 있는지 여부를 나타내는 선택적 매개 변수를 허용합니다. 이 플래그는 경우 `true`를 사용 하 여 보기에 오류 메시지가 전송 되는 `ViewBag` 속성입니다.

코드는 `HttpPost` `Delete` 메서드 (라는 `DeleteConfirmed`)를 다음 코드로:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

방금 바꾼 스캐폴드된 코드에서 이 메서드는 레코드 ID만 허용했습니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

이 매개 변수를 변경한 후는 `Department` 모델 바인더를 통해 만든 엔터티 인스턴스. 그러면에 액세스할 수는 `RowVersion` 레코드 키 외에 속성 값입니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

또한 `DeleteConfirmed`에서 `Delete`로 작업 메서드 이름을 변경했습니다. 명명 된 스 캐 폴드 코드는 `HttpPost` `Delete` 메서드 `DeleteConfirmed` 제공 하는 `HttpPost` 메서드는 고유의 시그니처가 있습니다. (CLR 오버 로드 된 메서드를 다른 메서드에 매개 변수가 필요 합니다.) 이제는 서명 되는 고유 수는 MVC 규칙 집중 하에 동일한 이름을 사용 하 여는 `HttpPost` 및 `HttpGet` 메서드를 삭제 합니다.

동시성 오류가 catch되는 경우 코드는 삭제 확인 페이지를 다시 표시하고 동시성 오류 메시지를 표시해야 함을 나타내는 플래그를 제공합니다.

*Views\Department\Delete.cshtml*를 스 캐 폴드 코드는 오류 메시지 필드와 DepartmentID 및 RowVersion 속성에 대 한 숨겨진된 필드를 추가 하는 다음 코드로 바꿉니다. 변경 내용은 강조 표시되어 있습니다.

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml?highlight=9-10,21,52-54)]

이 코드 사이 오류 메시지가 추가 `h2` 및 `h3` 머리글:

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

대체 `LastName` 와 `FullName` 에 `Administrator` 필드:

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

마지막으로, 숨겨진된 필드에 대 한 추가 `DepartmentID` 및 `RowVersion` 후 속성은 `Html.BeginForm` 문:

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cshtml)]

부서 인덱스 페이지를 실행 합니다. 마우스 오른쪽 단추로 클릭는 **삭제** 영어 부서 및 선택에 대 한 하이퍼링크 **새 탭에서 열기** 첫 번째 탭에서을 클릭는 **편집** 영어 부서에 대 한 하이퍼링크입니다.

첫 번째 창에서 값 중 하나를 변경 하 고 클릭 **저장** :

![Department_Edit_page_after_change_before_delete](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image12.png)

인덱스 페이지에 변경 내용을 확인합니다.

![Departments_Index_page_after_budget_edit_before_delete](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)

두 번째 탭에서 **삭제**를 클릭합니다.

![Department_Delete_confirmation_page_before_concurrency_error](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)

동시성 오류 메시지가 표시되며 부서 값은 데이터베이스의 현재 값으로 새로 고쳐집니다.

![Department_Delete_confirmation_page_with_concurrency_error](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)

**삭제**를 다시 클릭하면 부서가 삭제되었음을 보여 주는 인덱스 페이지로 리디렉션됩니다.

## <a name="summary"></a>요약

동시성 충돌 처리에 대한 소개를 완료합니다. 다양 한 동시성 시나리오를 처리 하는 다른 방법에 대 한 정보를 참조 하십시오. [낙관적 동시성 패턴](https://msdn.microsoft.com/data/jj592904) 및 [속성 값을 가진 작업](https://msdn.microsoft.com/data/jj592677) msdn 합니다. 다음 자습서에 대 한 계층당 하나의 테이블 상속을 구현 하는 방법을 보여 줍니다는 `Instructor` 및 `Student` 엔터티.

다른 Entity Framework 리소스에 대 한 링크에서 확인할 수 있습니다는 [ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.

> [!div class="step-by-step"]
> [이전](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [다음](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
