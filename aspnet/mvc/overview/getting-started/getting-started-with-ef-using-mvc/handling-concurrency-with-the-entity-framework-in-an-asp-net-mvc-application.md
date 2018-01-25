---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
title: "ASP.NET MVC 5 (10 / 12) 응용 프로그램에서 Entity Framework 6 사용 하 여 동시성 처리 | Microsoft Docs"
author: tdykstra
description: "Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 6 Code First 및 Visual Studio를 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/08/2014
ms.topic: article
ms.assetid: be0c098a-1fb2-457e-b815-ddca601afc65
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9df5b9c7e955b784bca7a4195b7c9cf3d2bca7a7
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="handling-concurrency-with-the-entity-framework-6-in-an-aspnet-mvc-5-application-10-of-12"></a>ASP.NET MVC 5 (10 / 12) 응용 프로그램에서 Entity Framework 6 사용 하 여 동시성 처리
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[완료 된 프로젝트를 다운로드](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8) 또는 [PDF 다운로드](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)

> Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 6 Code First 및 Visual Studio 2013을 사용 하 여 ASP.NET MVC 5 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대 한 정보를 참조 하십시오. [시리즈의 첫 번째 자습서](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.


이전 자습서에서는 데이터를 업데이트 하는 방법을 알아보았습니다. 이 자습서에는 여러 사용자가 동시에 같은 엔터티를 업데이트 하는 경우 충돌을 처리 하는 방법을 보여 줍니다.

작동 하는 웹 페이지를 변경 합니다는 `Department` 엔터티는 동시성 오류를 처리 하도록 합니다. 다음 그림은 동시성 충돌이 발생 한 경우 표시 되는 일부 메시지를 포함 하는 인덱스 및 Delete 페이지를 보여 줍니다.

![Department_Index_page_before_edits](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="concurrency-conflicts"></a>동시성 충돌

한 명의 사용자를 편집 하기 위해 엔터티 데이터를 표시 하 고 첫 번째 사용자의 변경 내용을 데이터베이스에 기록 되기 전에 다른 사용자는 동일한 엔터티의 데이터를 업데이트 하는 다음 동시성 충돌이 발생 합니다. 이러한 충돌 감지를 사용 하지 않을 경우 다른 사용자의 변경 내용을 덮어씁니다 마지막 누구 든 지 데이터베이스를 업데이트 합니다. 많은 응용 프로그램에서이 위험을 감수할: 적은 수의 사용자, 또는 몇 가지 업데이트 하거나 동시성에 대 한 프로그래밍의 비용의 이점 보다 클 수 일부 변경 내용이 덮어쓰면 실제로 중요 하지 않은 합니다. 이 경우 동시성 충돌을 처리 하도록 응용 프로그램을 구성할 필요가 없습니다.

### <a name="pessimistic-concurrency-locking"></a>비관적 동시성 (잠금)

응용 프로그램에서 동시성 시나리오에서 실수로 인 한 데이터 손실을 방지할 필요가 경우 작업을 수행 하는 한 가지 방법은 데이터베이스 잠금을 사용 하는 합니다. 이 라고 *비관적 동시성*합니다. 예를 들어 데이터베이스에서 행을 읽기 전에 요청에 대 한 잠금을 읽기 전용 이거나 업데이트 액세스 합니다. 업데이트 권한이 대 한 행을 잠그는 다른 사용자가 허용 되는 경우 행에 대해 잠글 읽기 전용 또는 변경 중인 데이터의 복사본을 가져오기 때문에 대 한 액세스를 업데이트 합니다. 읽기 전용 액세스에 대 한 행을 잠그는 경우 다른 사용자도 잠글 수 있지만 업데이트에 대 한 읽기 전용 액세스 합니다.

잠금 관리에 단점이 있습니다. 프로그램으로 복잡할 수 있습니다. 중요 한 데이터베이스 관리 리소스 있어야 하며 응용 프로그램의 사용자의 수로 성능 문제가 생길 수 증가 합니다. 이러한 이유로 모든 데이터베이스 관리 시스템 비관적 동시성을 지원 합니다. Entity Framework,에 대 한 기본 제공 지원이 제공 하 고이 자습서에서는 구현 하는 방법을 표시 되지 않습니다.

### <a name="optimistic-concurrency"></a>낙관적 동시성

비관적 동시성을 대신 사용 하는 *낙관적 동시성*합니다. 낙관적 동시성 현상이 동시성 충돌을 허용 하 고 그럴 경우 적절 하 게 반응 의미 합니다. 이한일은 변경 부서 편집 페이지를 실행 하는 예를 들어는 **예산** $0.00으로 $350,000.00에서 영어 부서에 대 한 금액입니다.

![Changing_English_dept_budget_to_100000](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

John 클릭 하기 전에 **저장**, Jane의 동일한 페이지 및 변경 내용 실행 되는 **시작 날짜** 2013 년 8 월 8 일에 필드를 2007 년 9 월 1입니다.

![Changing_English_dept_start_date_to_1999](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

John 클릭 **저장** 클릭 한 다음 jane은 인덱스 페이지에는 브라우저는 반환 될 때 그의 변경에 게 표시 하 고 첫 번째 **저장**합니다. 다음은 동시성 충돌을 처리 하는 방법을 따라 결정 됩니다. 일부 옵션은 다음과 같습니다.

- 한 사용자가 수정 되는 속성을 추적 하 고 데이터베이스의 해당 열만 업데이트할 수 있습니다. 예제 시나리오에서 데이터가 손실 될, 서로 다른 속성 두 사용자가 업데이트 되었기 때문에 합니다. 다음에 영어 부서 이동, John의와 Jane의 변경 내용을 볼 수 있습니다-2013 년 8 월 8 일의 시작 날짜와 예산 0 달러입니다.

    이 메서드를 업데이트 하는 데이터가 손실 될 수 있는 충돌 수를 줄일 수 있지만 경쟁 변경 되 면 동일한 엔터티의 속성에 데이터 손실을 방지할 수 없습니다. Entity Framework이 방식이으로 작동 하는지 여부를 업데이트 코드를 구현 하는 방법에 따라 달라 집니다. 것은 엔터티에 대 한 기존 속성 값 뿐만 아니라 새 값의 추적을 유지 하기 위해 많은 양의 상태를 유지 해야 하므로 웹 응용 프로그램에서는 실용적 없는 경우가 많습니다. 많은 양의 상태를 유지 관리 성능이 떨어질 수 있습니다 응용 프로그램 서버 리소스를 필요로 하거나 (예를 들어 숨겨진된 필드)에 웹 페이지 자체에 포함 해야 하기 때문에 이나 쿠키입니다.
- John의 내용으로 덮어쓰게 Jane의 변경 하도록 할 수 있습니다. 다음에 영어 부서 이동, 2013 년 8 월 8 일을 볼 수 있습니다 및 복원 된 $350,000.00 값입니다. 이 라고는 *클라이언트 우선* 또는 *최신으로* 시나리오입니다. (클라이언트에서 모든 값 보다 우선 데이터 저장소에 포함 된 내용입니다.) 동시성 처리에 대 한 코딩이 이렇게 하지 않으면이 섹션의 소개 부분에서 언급 했 듯이이 자동으로 수행 됩니다.
- 데이터베이스에서 업데이트 되 고에서 Jane의 변경을 방지할 수 있습니다. 일반적으로 오류 메시지가 표시, 그녀는 데이터의 현재 상태를 표시 하는 그녀는 여전히 있도록가 그녀의 변경 내용을 다시 적용할 수 있습니다. 이 라고는 *저장소 Wins* 시나리오입니다. (데이터 저장소 값 보다 우선 적용 클라이언트에서 전송한 값.) 이 자습서에서는 저장소 Wins 시나리오를 구현 합니다. 이 메서드는 변경 하는 상황과 경고가 표시 되 고 사용자가 없어도 덮어씀을 확인 합니다.

### <a name="detecting-concurrency-conflicts"></a>동시성 충돌 확인

처리 하 여 충돌을 해결할 수 [OptimisticConcurrencyException](https://msdn.microsoft.com/library/system.data.optimisticconcurrencyexception.aspx) Entity Framework throw 하는 예외입니다. 이러한 예외를 throw 하는 시기를 확인 하기 위해 Entity Framework에서 충돌을 검색할 수 있어야 합니다. 따라서 구성 해야 데이터베이스와 데이터 모델 적절 하 게 합니다. 충돌 감지를 사용 하기 위한 몇 가지 옵션은 다음과 같습니다.

- 데이터베이스 테이블에 행이 변경 된 시기를 결정 하는 데 사용할 수 있는 추적 열을 포함 합니다. Entity Framework의 해당 열을 포함 하도록 구성할 수 있습니다는 `Where` sql 절 `Update` 또는 `Delete` 명령입니다.

    추적 열의 데이터 형식이 일반적으로 [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)합니다. [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) 값은 행이 업데이트 될 때마다가 증가 하는 일련 번호입니다. 에 `Update` 또는 `Delete` 명령을 `Where` 절 추적 열 (원래 행 버전)의 원래 값이 포함 됩니다. 업데이트 되는 행의 값을 다른 사용자에 의해 변경 된 경우는 `rowversion` 열이 원래 값과 다른 하므로 `Update` 또는 `Delete` 문 때문에 업데이트할 행을 찾을 수 없습니다는 `Where` 절. 경우 Entity Framework의 행이 없는 하 여 업데이트를 찾습니다는 `Update` 또는 `Delete` 명령 (즉 때 영향을 받는 행 수는 0), 동시성 충돌 하는 해석 합니다.
- Entity Framework에서 테이블의 모든 열의 원래 값을 포함 하도록 구성 된 `Where` 절 `Update` 및 `Delete` 명령 합니다.

    첫 번째 옵션 행 주체를 읽어 먼저 이후에 변경 된 행에 아무 것도 경우와 같이 `Where` 절 반환 하지 않습니다는 행을 업데이트 하려면 Entity Framework를 동시성 충돌로 해석 합니다. 많은 열이 있는 데이터베이스 테이블에 대 한이 방법을 사용 하면 매우 큰 `Where` 절, 많은 양의 상태를 유지 관리 하는 필요할 수 있습니다. 앞에서 설명한 것 처럼 많은 양의 상태를 유지 관리 응용 프로그램 성능 영향을 줄 수 있습니다. 따라서이 방법은 일반적으로 권장 되지 않으며,이 자습서에 사용 하는 방법은 아닙니다.

    추가 하 여 동시성을 추적 하려는 엔터티의 모든 아닌 기본 키 속성을 표시 해야 하는 동시성이 접근 방식을 구현 않으려면는 [ConcurrencyCheck](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.concurrencycheckattribute.aspx) 특성을 해당 합니다. Entity Framework는 SQL의 모든 열을 포함 하도록 변경 하는 `WHERE` 절 `UPDATE` 문.

이 자습서의 나머지 부분에서는 추가 [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) 속성을 추적는 `Department` 엔터티를 컨트롤러와 뷰를 만들고 모든 항목이 올바르게 작동 하는지 확인 하려면 테스트 합니다.

## <a name="add-an-optimistic-concurrency-property-to-the-department-entity"></a>낙관적 동시성 속성 부서 엔터티에 추가

*Models\Department.cs*, 라는 추적 속성을 추가 `RowVersion`:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=20-22)]

[타임 스탬프](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx) 특성에이 열은 포함 되어야 함을 지정는 `Where` 절 `Update` 및 `Delete` 명령을 데이터베이스에 전송 합니다. 이 특성 이라고 [타임 스탬프](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx) 이전 버전의 SQL Server는 SQL을 사용 하기 때문에 [타임 스탬프](https://msdn.microsoft.com/library/ms182776(v=SQL.90).aspx) SQL 전에 데이터 형식 [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) 대체 했습니다. .Net 유형을 [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) 는 바이트 배열입니다.

Fluent API를 사용 하는 것을 선호 하는 경우 사용할 수 있습니다는 [IsConcurrencyToken](https://msdn.microsoft.com/library/gg679501(v=VS.103).aspx) 메서드를 다음 예제와 같이 추적 속성을 지정 합니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

속성을 추가 하 여 다른 마이그레이션을 수행 해야 하므로 데이터베이스 모델을 변경 했습니다. 패키지 관리자 콘솔 (PMC)에서 다음 명령을 입력 합니다.

[!code-console[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cmd)]

## <a name="modify-the-department-controller"></a>부서 컨트롤러를 수정

*Controllers\DepartmentController.cs*, 추가 `using` 문:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

에 *DepartmentController.cs* 파일에서 "LastName"의 모든 4 개의 항목을 "FullName"로 변경 하 부서 관리자 드롭 다운 목록을 강의의 전체 이름이 아니라 마지막 이름만 포함 됩니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=1)]

에 대 한 기존 코드는 `HttpPost` `Edit` 메서드를 다음 코드로:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

경우는 `FindAsync` 메서드가 null을 반환, 부서에서 다른 사용자가 삭제 되었습니다. 표시 된 코드는 department 엔터티를 편집 페이지를 하 고 오류 메시지가 다시 표시 될 수 있도록 게시 된 양식 값을 사용 합니다. 대신 부서 필드를 다시 표시 하지 않고 오류 메시지를 표시 하는 경우 department 엔터티를 다시 만들 필요가 있습니다.

뷰 저장 원래 `RowVersion` 숨겨진된 필드와 메서드에서 값에서 받는 `rowVersion` 매개 변수입니다. 호출 하기 전에 `SaveChanges`, 원래를 설치 해야 `RowVersion` 속성 값에는 `OriginalValues` 엔터티에 대 한 컬렉션입니다. Entity Framework는 SQL을 생성할 때 다음 `UPDATE` 명령, 명령 포함 됩니다는 `WHERE` 원래 있는 행을 검색 하는 절 `RowVersion` 값입니다.

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

마지막으로 코드가 설정는 `RowVersion` 의 값은 `Department` 데이터베이스에서 검색 한 개체를 새 값입니다. 이 새로운 `RowVersion` 페이지 다시 표시 됩니다, 편집 및 다음의 사용자 클릭을 시간 값 숨겨진된 필드에 저장 됩니다 **저장**만 편집 페이지를 다시 표시 됩니다 찾아낼 수 때문에 발생 하는 동시성 오류.

*Views\Department\Edit.cshtml*를 저장 하는 숨겨진된 필드를 추가 하는 `RowVersion` 속성 값을 바로 다음에 대 한 숨겨진된 필드는 `DepartmentID` 속성:

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=18)]

## <a name="testing-optimistic-concurrency-handling"></a>낙관적 동시성 처리를 테스트합니다.

사이트를 실행 하 고 클릭 **부서**:

![Department_Index_page_before_edits](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

마우스 오른쪽 단추로 클릭는 **편집** 영어 부서 및 선택에 대 한 하이퍼링크 **새 탭에서 열기** 클릭는 **편집** 영어 부서에 대 한 하이퍼링크입니다. 두 개의 탭과 동일한 정보를 표시합니다.

![Department_Edit_page_before_changes](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

첫 번째 브라우저 탭에서 필드를 변경 하 고 클릭 **저장**합니다.

![Department_Edit_page_1_after_change](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

브라우저는 변경 된 값은 인덱스 페이지를 보여 줍니다.

![Departments_Index_page_after_first_budget_edit](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

두 번째 브라우저 탭에서 필드를 변경 하 고 클릭 **저장**합니다.

![Department_Edit_page_2_after_change](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

클릭 **저장** 두 번째 브라우저 탭에 있습니다. 오류 메시지가 나타납니다.

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

클릭 **저장** 다시 합니다. 두 번째 브라우저 탭에 입력 한 값은 첫 번째 브라우저에서 변경 되는 데이터의 원래 값과 함께 저장 됩니다. 인덱스 페이지가 표시 되 면 저장된 된 값을 참조 합니다.

![Department_Index_page_with_change_from_second_browser](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image11.png)

## <a name="updating-the-delete-page"></a>업데이트 페이지 삭제

Delete 페이지에 대 한 Entity Framework는 다른 부서에서 비슷한 방식으로 편집 사용자에 의해 발생 한 동시성 충돌을 검색 합니다. 경우는 `HttpGet` `Delete` 확인 뷰를 표시 하는 메서드, 보기 포함 원래 `RowVersion` 숨겨진된 필드의 값입니다. 값은 사용할 수 있는 다음의 `HttpPost` `Delete` 메서드를 사용자가 삭제 확인 될 때 호출 됩니다. Entity Framework는 SQL을 생성할 때 `DELETE` 명령을 포함 한 `WHERE` 원래 절 `RowVersion` 값입니다. 0 개의 행에 명령 결과가 (행이 삭제 확인 페이지에 표시 된 후 변경 의미), 영향을 받는 경우 동시성 예외가 throw 되 고 `HttpGet Delete` 로 설정 하는 오류 플래그가 메서드는 `true` 다시 표시 하려면는 오류 메시지와 함께 확인 페이지입니다. 행이 없는 경우에서 다른 오류 메시지가 표시 되는 행 다른 사용자가 삭제 되었으므로 때문에 영향을 받은 수 이기도 합니다.

*DepartmentController.cs*, 대체 된 `HttpGet` `Delete` 메서드를 다음 코드로:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

메서드는 동시성 오류가 발생 한 후 페이지는 다시 표시 되 고 있는지 여부를 나타내는 선택적 매개 변수를 허용 합니다. 이 플래그는 경우 `true`를 사용 하 여 보기에 오류 메시지가 전송 되는 `ViewBag` 속성입니다.

코드는 `HttpPost` `Delete` 메서드 (라는 `DeleteConfirmed`)를 다음 코드로:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

대체 했습니까 스 캐 폴드 코드에서이 메서드는 레코드 ID만 수락 됨:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

이 매개 변수를 변경한 후는 `Department` 모델 바인더를 통해 만든 엔터티 인스턴스. 그러면에 액세스할 수는 `RowVersion` 레코드 키 외에 속성 값입니다.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

작업 메서드 이름을 변경한 `DeleteConfirmed` 를 `Delete`합니다. 명명 된 스 캐 폴드 코드는 `HttpPost` `Delete` 메서드 `DeleteConfirmed` 제공 하는 `HttpPost` 메서드는 고유의 시그니처가 있습니다. (CLR 오버 로드 된 메서드를 다른 메서드에 매개 변수가 필요 합니다.) 이제는 서명 되는 고유 수는 MVC 규칙 집중 하에 동일한 이름을 사용 하 여는 `HttpPost` 및 `HttpGet` 메서드를 삭제 합니다.

동시성 오류 들어갈 코드 삭제 확인 페이지를 다시 표시 하 고 것을 나타내는 플래그를 동시성 오류 메시지를 표시할지를 제공 합니다.

*Views\Department\Delete.cshtml*를 스 캐 폴드 코드는 오류 메시지 필드와 DepartmentID 및 RowVersion 속성에 대 한 숨겨진된 필드를 추가 하는 다음 코드로 바꿉니다. 변경 내용은 강조 표시 됩니다.

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

두 번째 탭에서 클릭 **삭제**합니다.

![Department_Delete_confirmation_page_before_concurrency_error](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)

동시성 오류 메시지가 표시 되며 부서 값은 현재 데이터베이스와 새로 고쳐집니다.

![Department_Delete_confirmation_page_with_concurrency_error](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)

클릭 하면 **삭제** 부서 삭제 했을 보여 주는 인덱스 페이지로 이동 하는 하는 다시 합니다.

## <a name="summary"></a>요약

동시성 충돌 처리 소개를 완료 합니다. 다양 한 동시성 시나리오를 처리 하는 다른 방법에 대 한 정보를 참조 하십시오. [낙관적 동시성 패턴](https://msdn.microsoft.com/data/jj592904) 및 [속성 값을 가진 작업](https://msdn.microsoft.com/data/jj592677) msdn 합니다. 다음 자습서에 대 한 계층당 하나의 테이블 상속을 구현 하는 방법을 보여 줍니다는 `Instructor` 및 `Student` 엔터티.

다른 Entity Framework 리소스에 대 한 링크에서 확인할 수 있습니다는 [ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)합니다.

>[!div class="step-by-step"]
[이전](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application.md)
[다음](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
