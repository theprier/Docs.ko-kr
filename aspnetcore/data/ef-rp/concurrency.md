---
title: "EF 코어 8-동시성-8 사용 하 여 razor 페이지"
author: rick-anderson
description: "이 자습서에는 여러 사용자가 동시에 같은 엔터티를 업데이트 하는 경우 충돌을 처리 하는 방법을 보여 줍니다."
keywords: "ASP.NET Core, Entity Framework Core 동시성"
ms.author: riande
manager: wpickett
ms.date: 11/15/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: data/ef-rp/concurrency
ms.openlocfilehash: 0c49376fd1b602fe03ef2a152d19b58513ae2710
ms.sourcegitcommit: 05e798c9bac7b9e9983599afb227ef393905d023
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
en-미국 /

# <a name="handling-concurrency-conflicts---ef-core-with-razor-pages-8-of-8"></a>동시성 충돌-EF 코어 Razor 페이지 (8의 8)에 처리

여 [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra), 및 [Jon P Smith](https://twitter.com/thereformedprog)

[!INCLUDE[about the series](../../includes/RP-EF/intro.md)]

이 자습서에는 여러 사용자가 동시에 (동시에) 엔터티를 업데이트 하는 경우 충돌을 처리 하는 방법을 보여 줍니다. 문제를 해결할 수 없는를 실행 하는 경우 다운로드는 [이 단계에 대 한 완성 된 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part8)합니다.

## <a name="concurrency-conflicts"></a>동시성 충돌

동시성 충돌이 발생 한 경우:

* 사용자는 엔터티에 대 한 편집 페이지를 탐색합니다.
* 다른 사용자는 db 첫 번째 사용자의 변경 내용을 기록 하기 전에 동일한 엔터티를 업데이트 합니다.

동시성 검색을 사용 하지 않는 경우 동시 업데이트 발생 합니다.

* 마지막 업데이트 우선 합니다. 즉, 마지막 값 업데이트 DB에 저장 됩니다.
* 현재 업데이트 중 첫 번째 작업은 손실 됩니다.

### <a name="optimistic-concurrency"></a>낙관적 동시성

업데이트를 동시성 충돌을 허용 하는 낙관적 동시성 및 반응 적절 하 게 때 않습니다. 예를 들어, Jane 부서 편집 페이지를 방문 하 고 $0.00 달러 350,000.00에서 영어 부서에 대 한 할당으로 변경 합니다.

![예산 0으로 변경](concurrency/_static/change-budget.png)

Jane은 클릭 하기 전에 **저장**, John 동일한 페이지를 방문 하 고 2007 년 9 월 1에서에서 2013 년 9 월 1 일 시작 날짜 필드를 변경 합니다.

![2013을 시작 날짜를 변경합니다.](concurrency/_static/change-date.png)

Jane은 클릭 **저장** 첫 번째 및 브라우저 인덱스 페이지를 표시할 때 변경 자신에 게 표시 합니다.

![예산 0으로 변경 합니다.](concurrency/_static/budget-zero.png)

John 클릭 **저장** $350,000.00의 예산에 여전히 표시 하는 편집 페이지가에 있습니다. 다음은 동시성 충돌을 처리 하는 방법을 따라 결정 됩니다.

낙관적 동시성에는 다음과 같은 옵션이 포함 됩니다.

* 한 사용자가 수정 되는 속성을 추적 하 고 데이터베이스에서 해당 열만 업데이트할 수 있습니다.

 이 시나리오에서는 데이터가 손실 됩니다. 서로 다른 속성 두 사용자가 업데이트 되었습니다. 다음에 영어 부서 이동 Jane의와 John의 변경 내용을 볼 수 있습니다. 이 메서드를 업데이트 하는 충돌 데이터가 손실 될 수 있는 횟수를 줄일 수 있습니다. 이 방법은: * 같은 속성 경쟁 변경 되 면 데이터 손실을 방지할 수 없습니다.
        *는 일반적으로 불가능 웹 앱입니다. 모든 인출 된 값과 새 값의 추적을 유지 하기 위해 중요 한 상태를 유지 해야 합니다. 많은 양의 상태를 유지 관리 응용 프로그램 성능이 떨어질 수 있습니다.
        * 엔터티에 대해 동시성 검색에 비해 앱 복잡성이 증가 수 있습니다.

* Jane의 내용으로 덮어쓰게 이한일의 변경 하도록 할 수 있습니다.

 다음에 영어 부서 이동, 2013 년 9 월 1 일을 볼 수 있습니다 및 인출 된 $350,000.00 값입니다. 이 방법은 라고는 *클라이언트 우선* 또는 *최신으로* 시나리오입니다. (클라이언트에서 모든 값 보다 우선 데이터 저장소에 포함 된 내용입니다.) 동시성 처리에 대 한 코딩이 이렇게 하지 않으면 자동으로 이루어짐 클라이언트 우선 합니다.

* 데이터베이스에서 업데이트할 이한일의 변경을 방지할 수 있습니다. 응용 프로그램은 일반적으로: * 오류 메시지를 표시 합니다.
        * 데이터의 현재 상태를 표시 합니다.
        * 사용자 변경 내용을 다시 적용 하도록 허용 합니다.

 이 라고는 *저장소 Wins* 시나리오입니다. (데이터 저장소 값 보다 우선 적용 클라이언트에서 전송한 값.) 이 자습서에서는 저장소 Wins 시나리오를 구현 합니다. 이 메서드를 사용 하면 변경 내용이 없습니다에 경고가 표시 되 고 사용자가 없어도 덮어쓰도록 합니다.

## <a name="handling-concurrency"></a>동시성 처리 

속성으로 구성 된 경우는 [동시성 토큰](https://docs.microsoft.com/en-us/ef/core/modeling/concurrency):

* EF 코어가 인출 된 후 수정 되지 않은 속성을 확인 합니다. 확인이 수행 때 [SaveChanges](https://docs.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.dbcontext.savechanges?view=efcore-2.0#Microsoft_EntityFrameworkCore_DbContext_SaveChanges) 또는 [SaveChangesAsync](https://docs.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.dbcontext.savechangesasync?view=efcore-2.0#Microsoft_EntityFrameworkCore_DbContext_SaveChangesAsync_System_Threading_CancellationToken_) 호출 됩니다.
* 이 인출 된 후 속성을 변경한 경우 한 [DbUpdateConcurrencyException](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.dbupdateconcurrencyexception?view=efcore-2.0) throw 됩니다. 

DB 및 데이터 모델 throw 지원 하도록 구성 해야 `DbUpdateConcurrencyException`합니다.

### <a name="detecting-concurrency-conflicts-on-a-property"></a>속성에 대 한 동시성 충돌 검색

사용 속성 수준에서 동시성 충돌을 검색할 수는 [ConcurrencyCheck](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.dataannotations.concurrencycheckattribute?view=netcore-2.0) 특성입니다. 특성은 모델에 여러 속성에 적용할 수 있습니다. 자세한 내용은 참조 [데이터 주석 ConcurrencyCheck](https://docs.microsoft.com/en-us/ef/core/modeling/concurrency#data-annotations)합니다.

`[ConcurrencyCheck]` 특성이이 자습서에서 사용 되지 않습니다.

### <a name="detecting-concurrency-conflicts-on-a-row"></a>행에 대해 동시성 충돌 확인

동시성 충돌을 검색 하는 [rowversion](https://docs.microsoft.com/sql/t-sql/data-types/rowversion-transact-sql) 는 모델에 추가 된 열을 추적 합니다.  `rowversion` :

* 특정 SQL Server입니다. 다른 데이터베이스 유사한 기능을 제공 하지 않을 수 있습니다.
* DB에서 인출 된 이후로 변경 되지 않은 엔터티를 확인 하는 데 사용 됩니다. 

DB 생성 순차적 `rowversion` 가 증가 될 때마다 행 개수 업데이트 됩니다. 에 `Update` 또는 `Delete` 명령에는 `Where` 절 인출 된 값이 포함 됩니다 `rowversion`합니다. 행이 업데이트 될 경우 변경 되었습니다.

 * `rowversion`인출 된 값을 일치 하지 않습니다.
 * `Update` 또는 `Delete` 명령 때문에 행을 찾지 못한는 `Where` 절 포함 하 여 인출 된 `rowversion`합니다.
 * A `DbUpdateConcurrencyException` throw 됩니다.

EF 코어, 행이 없는으로 업데이트 한 후에 `Update` 또는 `Delete` 명령, 동시성 예외가 throw 됩니다.

### <a name="add-a-tracking-property-to-the-department-entity"></a>추적 속성 부서 엔터티에 추가

*Models/Department.cs*, RowVersion 라는 추적 속성을 추가 합니다.

[!code-csharp[Main](intro/samples/cu/Models/Department.cs?name=snippet_Final&highlight=26,27)]

[타임 스탬프](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.timestampattribute) 특성 지정이 열에 포함 되어 있는지는 `Where` 절 `Update` 및 `Delete` 명령입니다. 이 특성 이라고 `Timestamp` 이전 버전의 SQL Server는 SQL을 사용 하기 때문에 `timestamp` SQL 전에 데이터 형식 `rowversion` 형식 대체 했습니다.

Fluent API 추적 속성을 지정할 수도 있습니다.

```csharp
modelBuilder.Entity<Department>()
  .Property<byte[]>("RowVersion")
  .IsRowVersion();
```

다음 코드에서는 부서 이름 업데이트 될 때 EF 코어에서 생성 된 T-SQL의 일부를 보여 줍니다.

[!code-sql[](intro/samples/sql.txt?highlight=2-3)]

위의 코드에서 보여 주는 강조 표시 됩니다는 `WHERE` 절이 포함 된 `RowVersion`합니다. 경우 DB `RowVersion` 와 같지 않습니다는 `RowVersion` 매개 변수 (`@p2`), 아무 행도 업데이트 됩니다.

다음 강조 표시 된 코드에는 정확히 한 개의 행이 업데이트를 확인 하는 T-SQL 보여 줍니다.

[!code-sql[](intro/samples/sql.txt?highlight=4-6)]

[@@ROWCOUNT ](https://docs.microsoft.com/en-us/sql/t-sql/functions/rowcount-transact-sql) 마지막 문의 영향을 받는 행 수를 반환 합니다. 아무에서 행이 업데이트 되, EF 코어를 throw 한 `DbUpdateConcurrencyException`합니다.

Visual Studio의 출력 창에 T-SQL EF 코어 생성을 확인할 수 있습니다.

### <a name="update-the-db"></a>DB 업데이트

추가 `RowVersion` 속성이 변경 되는 마이그레이션 마이그레이션해야 하는 DB 모델입니다.

프로젝트를 빌드합니다. 명령 창에서 다음을 입력 합니다.

```console
dotnet ef migrations add RowVersion
dotnet ef database update
```

이전 명령:

* 추가 *마이그레이션 / {시간 stamp}_RowVersion.cs* 마이그레이션 파일입니다.
* 업데이트는 *Migrations/SchoolContextModelSnapshot.cs* 파일입니다. 다음 강조 표시 된 코드를 추가 하는 업데이트는 `BuildModel` 메서드:

[!code-csharp[Main](intro/samples/cu/Migrations/SchoolContextModelSnapshot2.cs?name=snippet&highlight=14-16)]

* 마이그레이션 DB 업데이트를 실행 합니다.

<a name="scaffold"></a>
## <a name="scaffold-the-departments-model"></a>스 캐 폴드 부서 모델

* Visual Studio를 종료 합니다.
* 프로젝트 디렉터리(*Program.cs*, *Startup.cs* 및 *.csproj* 파일이 포함된 디렉터리)에서 명령 창을 엽니다.
* 다음 명령을 실행합니다.

 ```console
dotnet aspnet-codegenerator razorpage -m Department -dc SchoolContext -udl -outDir Pages\Departments --referenceScriptLibraries
 ```

위의 명령은 스 캐 폴드 된 `Department` 모델입니다. Visual Studio에서 프로젝트를 엽니다.

프로젝트를 빌드합니다. 빌드에서는 다음과 같은 오류를 생성합니다.

`1>Pages/Departments/Index.cshtml.cs(26,37,26,43): error CS1061: 'SchoolContext' does not
 contain a definition for 'Department' and no extension method 'Department' accepting a first
 argument of type 'SchoolContext' could be found (are you missing a using directive or
 an assembly reference?)`

 전역으로 변경 `_context.Department` 를 `_context.Departments` (즉, "s"에 추가 `Department`). 7 번 발견 되 고 업데이트 됩니다.

### <a name="update-the-departments-index-page"></a>부서 인덱스 페이지를 업데이트 합니다.

만든 스 캐 폴딩 엔진은 `RowVersion` 인덱스 페이지 이지만 해당 필드에 대 한 열을 표시 하지 않아야 합니다. 이 자습서의 마지막 바이트는 `RowVersion` 동시성 이해 하기 위해 표시 됩니다. 마지막 바이트는 고유 하 게 보장 되지 않습니다. 실제 앱 없게 표시 `RowVersion` 또는의 마지막 바이트 `RowVersion`합니다.

인덱스 페이지를 업데이트 합니다.

* 인덱스를 부서 바꿉니다.
* 포함 하는 태그 대체 `RowVersion` 의 마지막 바이트와 `RowVersion`합니다.
* FullName FirstMidName 대체 합니다.

다음 태그 업데이트 페이지를 보여 줍니다.

[!code-html[](intro/samples/cu/Pages/Departments/Index.cshtml?highlight=5,8,29,47,50)]

### <a name="update-the-edit-page-model"></a>편집 페이지 모델 업데이트

업데이트 *pages\departments\edit.cshtml.cs* 를 다음 코드로:

[!code-csharp[](intro/samples/cu/Pages/Departments/Edit.cshtml.cs?name=snippet)]

동시성 문제를 감지 하는 [OriginalValue](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.changetracking.propertyentry.originalvalue?view=efcore-2.0#Microsoft_EntityFrameworkCore_ChangeTracking_PropertyEntry_OriginalValue) 으로 업데이트는 `rowVersion` 엔터티에서 값이 인출 되었습니다. EF 코어 원본이 포함 된 WHERE 절과 함께 SQL UPDATE 명령과 생성 `RowVersion` 값입니다. UPDATE 명령 영향을 받는 행이 없는 경우 (행이 없는 원래 `RowVersion` 값), 즉 `DbUpdateConcurrencyException` 예외가 throw 됩니다.

[!code-csharp[](intro/samples/cu/Pages/Departments/Edit.cshtml.cs?name=snippet_rv&highlight=24-)]

위의 코드에서 `Department.RowVersion` 엔터티를 인출할 때 값입니다. `OriginalValue`DB에 값이 때 `FirstOrDefaultAsync` 이 메서드의 호출 되었습니다.

다음 코드는 클라이언트 값 (이 메서드에 게시 된 값) 및 DB 값을 가져옵니다.

[!code-csharp[](intro/samples/cu/Pages/Departments/Edit.cshtml.cs?name=snippet_try&highlight=9,18)]

DB가 있는 각 열에 게시 된 작업에서 다른 값에 대 한 사용자 지정 오류 메시지를 추가 하는 다음 코드 `OnPostAsync`:

[!code-csharp[](intro/samples/cu/Pages/Departments/Edit.cshtml.cs?name=snippet_err)]

다음 코드 집합을 강조 표시는 `RowVersion` DB에서 검색 된 값을 새 값입니다. 다음에 사용자가 클릭 **저장**, 이후 편집 페이지의 마지막 디스플레이 찾아낼 수는 발생 하는 동시성 오류만 합니다.

[!code-csharp[](intro/samples/cu/Pages/Departments/Edit.cshtml.cs?name=snippet_try&highlight=23)]

`ModelState.Remove` 때문에 문이 필요 않습니다 `ModelState` 이전에 `RowVersion` 값입니다. Razor 페이지에는 `ModelState` 필드 우선 모델 속성 값은 둘 다 있는 경우에 대 한 값입니다.

## <a name="update-the-edit-page"></a>업데이트 편집 페이지

업데이트 *Pages/Departments/Edit.cshtml* 다음 태그로:

[!code-html[](intro/samples/cu/Pages/Departments/Edit.cshtml?highlight=1,14,16-17,37-39)]

위의 태그:

* 업데이트는 `page` 지시어를 `@page` 를 `@page "{id:int}"`합니다.
* 숨겨진된 행 버전을 추가합니다. `RowVersion`다시 게시 값을 연결 하므로 추가 되어야 합니다.
* 마지막 바이트 표시 `RowVersion` 디버깅 목적으로 합니다.
* 대체 `ViewData` 강력한 형식의와 `InstructorNameSL`합니다.

## <a name="test-concurrency-conflicts-with-the-edit-page"></a>동시성 충돌 편집 페이지를 테스트 합니다.

영어 부서에 있는 편집의 두 브라우저 인스턴스를 엽니다.

* 응용 프로그램을 실행 하 고 부서를 선택 합니다.
* 마우스 오른쪽 단추로 클릭는 **편집** 영어 부서 및 선택에 대 한 하이퍼링크 **새 탭에서 열기**합니다.
* 첫 번째 탭을 클릭는 **편집** 영어 부서에 대 한 하이퍼링크입니다.

두 개의 브라우저 탭 동일한 정보를 표시 합니다.

첫 번째 브라우저 탭에서 이름을 변경 하 고 클릭 **저장**합니다.

![부서 편집 페이지 1 변경 후](concurrency/_static/edit-after-change-1.png)

브라우저에서는 변경 된 값과 업데이트 된 rowVersion 표시기 인 인덱스 페이지를 보여 줍니다. 업데이트 된 rowVersion 표시기 참고 기타 탭에 두 번째 포스트백에 표시 됩니다.

두 번째 브라우저 탭에서 다른 필드를 변경 합니다.

![부서 편집 변경 후 2 페이지](concurrency/_static/edit-after-change-2.png)

**저장**을 클릭합니다. DB 값과 일치 하지 않는 모든 필드에 대 한 오류 메시지 표시:

![부서 편집 페이지 오류 메시지](concurrency/_static/edit-error.png)

이 브라우저 창 Name 필드를 변경 하 려 하지 않았던 합니다. 복사 하 고 현재 값 (언어)의 이름 필드에 붙여넣습니다. 탭 합니다. 클라이언트 쪽 유효성 검사 오류 메시지를 제거합니다.

![부서 편집 페이지 오류 메시지](concurrency/_static/cv.png)

클릭 **저장** 다시 합니다. 두 번째 브라우저 탭에 입력 한 값이 저장 됩니다. 인덱스 페이지에 저장된 된 값을 표시 합니다.

## <a name="update-the-delete-page"></a>업데이트 페이지 삭제

다음 코드로 Delete 페이지 모델을 업데이트 합니다.

[!code-csharp[](intro/samples/cu/Pages/Departments/Delete.cshtml.cs)]

페이지 삭제 된 엔터티가 인출 된 후 변경 될 때 동시성 충돌을 감지 합니다. `Department.RowVersion`엔터티를 인출할 때 행 버전이입니다. WHERE 절을 포함 EF 핵심 SQL DELETE 명령과 만들면 `RowVersion`합니다. SQL DELETE 명령 결과가 0 인 행에 영향을 합니다.

* `RowVersion` SQL DELETE 명령을 일치 하지 않습니다 `RowVersion` DB에 있습니다.
* DbUpdateConcurrencyException 예외가 throw 됩니다.
* `OnGetAsync`사용 하 여 호출 된 `concurrencyError`합니다.

### <a name="update-the-delete-page"></a>업데이트 페이지 삭제

업데이트 *Pages/Departments/Delete.cshtml* 를 다음 코드로:

[!code-html[](intro/samples/cu/Pages/Departments/Delete.cshtml?highlight=1,10,36,51)]


위의 태그에서는 다음과 같이 변경 합니다.

* 업데이트는 `page` 지시어를 `@page` 를 `@page "{id:int}"`합니다.
* 오류 메시지를 추가 합니다.
* FullName FirstMidName 바꿉니다는 **관리자** 필드입니다.
* 변경 내용을 `RowVersion` 마지막 바이트를 표시 합니다.
* 숨겨진된 행 버전을 추가합니다. `RowVersion`다시 게시 값을 연결 하므로 추가 되어야 합니다.

### <a name="test-concurrency-conflicts-with-the-delete-page"></a>Delete 페이지와 테스트 동시성 충돌

테스트 부서를 만듭니다.

테스트 부서에 Delete의 두 브라우저 인스턴스를 엽니다.

* 응용 프로그램을 실행 하 고 부서를 선택 합니다.
* 마우스 오른쪽 단추로 클릭는 **삭제** 테스트 부서 및 선택에 대 한 하이퍼링크 **새 탭에서 열기**합니다.
* 클릭는 **편집** 테스트 부서에 대 한 하이퍼링크입니다.

두 개의 브라우저 탭 동일한 정보를 표시 합니다.

첫 번째 브라우저 탭에서 할당을 변경 하 고 클릭 **저장**합니다.

브라우저에서는 변경 된 값과 업데이트 된 rowVersion 표시기 인 인덱스 페이지를 보여 줍니다. 업데이트 된 rowVersion 표시기 참고 기타 탭에 두 번째 포스트백에 표시 됩니다.

두 번째 탭에서 테스트 부서를 삭제 합니다. 동시성 오류는 DB의 현재 값으로 표시 됩니다. 클릭 하면 **삭제** 되지 않는 한 엔터티를 삭제 `RowVersion` updated.department가 삭제 되었습니다.

참조 [상속](xref:data/ef-mvc/inheritance) 데이터 모델에서 상속 하는 방법에 대 한 합니다.

### <a name="additional-resources"></a>추가 리소스

* [EF 코어의 동시성 토큰](https://docs.microsoft.com/en-us/ef/core/modeling/concurrency)
* [EF 코어에서 동시성 처리](https://docs.microsoft.com/en-us/ef/core/saving/concurrency)

>[!div class="step-by-step"]
[이전](xref:data/ef-rp/update-related-data)
