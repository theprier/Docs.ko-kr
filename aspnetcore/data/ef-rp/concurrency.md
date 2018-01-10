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
ms.openlocfilehash: 841c638b2cacaab7970f2b173fee488972957b63
ms.sourcegitcommit: 2d23ea501e0213bbacf65298acf1c8bd17209540
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
<span data-ttu-id="29317-104">en-미국 /</span><span class="sxs-lookup"><span data-stu-id="29317-104">en-us/</span></span>

# <a name="handling-concurrency-conflicts---ef-core-with-razor-pages-8-of-8"></a><span data-ttu-id="29317-105">동시성 충돌-EF 코어 Razor 페이지 (8의 8)에 처리</span><span class="sxs-lookup"><span data-stu-id="29317-105">Handling concurrency conflicts - EF Core with Razor Pages (8 of 8)</span></span>

<span data-ttu-id="29317-106">여 [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra), 및 [Jon P Smith](https://twitter.com/thereformedprog)</span><span class="sxs-lookup"><span data-stu-id="29317-106">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra), and  [Jon P Smith](https://twitter.com/thereformedprog)</span></span>

[!INCLUDE[about the series](../../includes/RP-EF/intro.md)]

<span data-ttu-id="29317-107">이 자습서에는 여러 사용자가 동시에 (동시에) 엔터티를 업데이트 하는 경우 충돌을 처리 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="29317-107">This tutorial shows how to handle conflicts when multiple users update an entity concurrently (at the same time).</span></span> <span data-ttu-id="29317-108">문제를 해결할 수 없는를 실행 하는 경우 다운로드는 [이 단계에 대 한 완성 된 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part8)합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-108">If you run into problems you can't solve, download the [completed app for this stage](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part8).</span></span>

## <a name="concurrency-conflicts"></a><span data-ttu-id="29317-109">동시성 충돌</span><span class="sxs-lookup"><span data-stu-id="29317-109">Concurrency conflicts</span></span>

<span data-ttu-id="29317-110">동시성 충돌이 발생 한 경우:</span><span class="sxs-lookup"><span data-stu-id="29317-110">A concurrency conflict occurs when:</span></span>

* <span data-ttu-id="29317-111">사용자는 엔터티에 대 한 편집 페이지를 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-111">A user navigates to the edit page for an entity.</span></span>
* <span data-ttu-id="29317-112">다른 사용자는 db 첫 번째 사용자의 변경 내용을 기록 하기 전에 동일한 엔터티를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-112">Another user updates the same entity before the first user's change is written to the DB.</span></span>

<span data-ttu-id="29317-113">동시성 검색을 사용 하지 않는 경우 동시 업데이트 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-113">If concurrency detection is not enabled, when concurrent updates occur:</span></span>

* <span data-ttu-id="29317-114">마지막 업데이트 우선 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-114">The last update wins.</span></span> <span data-ttu-id="29317-115">즉, 마지막 값 업데이트 DB에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29317-115">That is, the last update values are saved to the DB.</span></span>
* <span data-ttu-id="29317-116">현재 업데이트 중 첫 번째 작업은 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29317-116">The first of the current updates are lost.</span></span>

### <a name="optimistic-concurrency"></a><span data-ttu-id="29317-117">낙관적 동시성</span><span class="sxs-lookup"><span data-stu-id="29317-117">Optimistic concurrency</span></span>

<span data-ttu-id="29317-118">업데이트를 동시성 충돌을 허용 하는 낙관적 동시성 및 반응 적절 하 게 때 않습니다.</span><span class="sxs-lookup"><span data-stu-id="29317-118">Optimistic concurrency allows concurrency conflicts to happen, and then reacts appropriately when they do.</span></span> <span data-ttu-id="29317-119">예를 들어, Jane 부서 편집 페이지를 방문 하 고 $0.00 달러 350,000.00에서 영어 부서에 대 한 할당으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-119">For example, Jane visits the Department edit page and changes the budget for the English department from $350,000.00 to $0.00.</span></span>

![예산 0으로 변경](concurrency/_static/change-budget.png)

<span data-ttu-id="29317-121">Jane은 클릭 하기 전에 **저장**, John 동일한 페이지를 방문 하 고 2007 년 9 월 1에서에서 2013 년 9 월 1 일 시작 날짜 필드를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-121">Before Jane clicks **Save**, John visits the same page and changes the Start Date field from 9/1/2007 to 9/1/2013.</span></span>

![2013을 시작 날짜를 변경합니다.](concurrency/_static/change-date.png)

<span data-ttu-id="29317-123">Jane은 클릭 **저장** 첫 번째 및 브라우저 인덱스 페이지를 표시할 때 변경 자신에 게 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-123">Jane clicks **Save** first and sees her change when the browser displays the Index page.</span></span>

![예산 0으로 변경 합니다.](concurrency/_static/budget-zero.png)

<span data-ttu-id="29317-125">John 클릭 **저장** $350,000.00의 예산에 여전히 표시 하는 편집 페이지가에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29317-125">John clicks **Save** on an Edit page that still shows a budget of $350,000.00.</span></span> <span data-ttu-id="29317-126">다음은 동시성 충돌을 처리 하는 방법을 따라 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29317-126">What happens next is determined by how you handle concurrency conflicts.</span></span>

<span data-ttu-id="29317-127">낙관적 동시성에는 다음과 같은 옵션이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29317-127">Optimistic concurrency includes the following options:</span></span>

* <span data-ttu-id="29317-128">한 사용자가 수정 되는 속성을 추적 하 고 데이터베이스에서 해당 열만 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29317-128">You can keep track of which property a user has modified and update only the corresponding columns in the DB.</span></span>

 <span data-ttu-id="29317-129">이 시나리오에서는 데이터가 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29317-129">In the scenario, no data would be lost.</span></span> <span data-ttu-id="29317-130">서로 다른 속성 두 사용자가 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="29317-130">Different properties were updated by the two users.</span></span> <span data-ttu-id="29317-131">다음에 영어 부서 이동 Jane의와 John의 변경 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29317-131">The next time someone browses the English department, they'll see both Jane's and John's changes.</span></span> <span data-ttu-id="29317-132">이 메서드를 업데이트 하는 충돌 데이터가 손실 될 수 있는 횟수를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29317-132">This method of updating can reduce the number of conflicts that could result in data loss.</span></span> <span data-ttu-id="29317-133">이 방법은: * 같은 속성 경쟁 변경 되 면 데이터 손실을 방지할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="29317-133">This approach: * Can't avoid data loss if competing changes are made to the same property.</span></span>
        <span data-ttu-id="29317-134">*는 일반적으로 불가능 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="29317-134">* Is generally not practical in a web app.</span></span> <span data-ttu-id="29317-135">모든 인출 된 값과 새 값의 추적을 유지 하기 위해 중요 한 상태를 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-135">It requires maintaining significant state in order to keep track of all fetched values and new values.</span></span> <span data-ttu-id="29317-136">많은 양의 상태를 유지 관리 응용 프로그램 성능이 떨어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29317-136">Maintaining large amounts of state can affect app performance.</span></span>
        <span data-ttu-id="29317-137">* 엔터티에 대해 동시성 검색에 비해 앱 복잡성이 증가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29317-137">* Can increase app complexity compared to concurrency detection on an entity.</span></span>

* <span data-ttu-id="29317-138">Jane의 내용으로 덮어쓰게 이한일의 변경 하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29317-138">You can let John's change overwrite Jane's change.</span></span>

 <span data-ttu-id="29317-139">다음에 영어 부서 이동, 2013 년 9 월 1 일을 볼 수 있습니다 및 인출 된 $350,000.00 값입니다.</span><span class="sxs-lookup"><span data-stu-id="29317-139">The next time someone browses the English department, they'll see 9/1/2013 and the fetched $350,000.00 value.</span></span> <span data-ttu-id="29317-140">이 방법은 라고는 *클라이언트 우선* 또는 *최신으로* 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="29317-140">This approach is called a *Client Wins* or *Last in Wins* scenario.</span></span> <span data-ttu-id="29317-141">(클라이언트에서 모든 값 보다 우선 데이터 저장소에 포함 된 내용입니다.) 동시성 처리에 대 한 코딩이 이렇게 하지 않으면 자동으로 이루어짐 클라이언트 우선 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-141">(All values from the client take precedence over what's in the data store.) If you don't do any coding for concurrency handling, Client Wins happens automatically.</span></span>

* <span data-ttu-id="29317-142">데이터베이스에서 업데이트할 이한일의 변경을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29317-142">You can prevent John's change from being updated in the DB.</span></span> <span data-ttu-id="29317-143">응용 프로그램은 일반적으로: * 오류 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-143">Typically, the app would: * Display an error message.</span></span>
        <span data-ttu-id="29317-144">* 데이터의 현재 상태를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-144">* Show the current state of the data.</span></span>
        <span data-ttu-id="29317-145">* 사용자 변경 내용을 다시 적용 하도록 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-145">* Allow the user to reapply the changes.</span></span>

 <span data-ttu-id="29317-146">이 라고는 *저장소 Wins* 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="29317-146">This is called a *Store Wins* scenario.</span></span> <span data-ttu-id="29317-147">(데이터 저장소 값 보다 우선 적용 클라이언트에서 전송한 값.) 이 자습서에서는 저장소 Wins 시나리오를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-147">(The data-store values take precedence over the values submitted by the client.) You implement the Store Wins scenario in this tutorial.</span></span> <span data-ttu-id="29317-148">이 메서드를 사용 하면 변경 내용이 없습니다에 경고가 표시 되 고 사용자가 없어도 덮어쓰도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-148">This method ensures that no changes are overwritten without a user being alerted.</span></span>

## <a name="handling-concurrency"></a><span data-ttu-id="29317-149">동시성 처리</span><span class="sxs-lookup"><span data-stu-id="29317-149">Handling concurrency</span></span> 

<span data-ttu-id="29317-150">속성으로 구성 된 경우는 [동시성 토큰](https://docs.microsoft.com/en-us/ef/core/modeling/concurrency):</span><span class="sxs-lookup"><span data-stu-id="29317-150">When a property is configured as a [concurrency token](https://docs.microsoft.com/en-us/ef/core/modeling/concurrency):</span></span>

* <span data-ttu-id="29317-151">EF 코어가 인출 된 후 수정 되지 않은 속성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-151">EF Core verifies that property has not been modified after it was fetched.</span></span> <span data-ttu-id="29317-152">확인이 수행 때 [SaveChanges](https://docs.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.dbcontext.savechanges?view=efcore-2.0#Microsoft_EntityFrameworkCore_DbContext_SaveChanges) 또는 [SaveChangesAsync](https://docs.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.dbcontext.savechangesasync?view=efcore-2.0#Microsoft_EntityFrameworkCore_DbContext_SaveChangesAsync_System_Threading_CancellationToken_) 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29317-152">The check occurs when [SaveChanges](https://docs.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.dbcontext.savechanges?view=efcore-2.0#Microsoft_EntityFrameworkCore_DbContext_SaveChanges) or [SaveChangesAsync](https://docs.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.dbcontext.savechangesasync?view=efcore-2.0#Microsoft_EntityFrameworkCore_DbContext_SaveChangesAsync_System_Threading_CancellationToken_) is called.</span></span>
* <span data-ttu-id="29317-153">이 인출 된 후 속성을 변경한 경우 한 [DbUpdateConcurrencyException](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.dbupdateconcurrencyexception?view=efcore-2.0) throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29317-153">If the property has been changed after it was fetched, a [DbUpdateConcurrencyException](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.dbupdateconcurrencyexception?view=efcore-2.0) is thrown.</span></span> 

<span data-ttu-id="29317-154">DB 및 데이터 모델 throw 지원 하도록 구성 해야 `DbUpdateConcurrencyException`합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-154">The DB and data model must be configured to support throwing `DbUpdateConcurrencyException`.</span></span>

### <a name="detecting-concurrency-conflicts-on-a-property"></a><span data-ttu-id="29317-155">속성에 대 한 동시성 충돌 검색</span><span class="sxs-lookup"><span data-stu-id="29317-155">Detecting concurrency conflicts on a property</span></span>

<span data-ttu-id="29317-156">사용 속성 수준에서 동시성 충돌을 검색할 수는 [ConcurrencyCheck](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.dataannotations.concurrencycheckattribute?view=netcore-2.0) 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="29317-156">Concurrency conflicts can be detected at the property level with the [ConcurrencyCheck](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.dataannotations.concurrencycheckattribute?view=netcore-2.0) attribute.</span></span> <span data-ttu-id="29317-157">특성은 모델에 여러 속성에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29317-157">The attribute can be applied to multiple properties on the model.</span></span> <span data-ttu-id="29317-158">자세한 내용은 참조 [데이터 주석 ConcurrencyCheck](https://docs.microsoft.com/en-us/ef/core/modeling/concurrency#data-annotations)합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-158">For more information, see [Data Annotations-ConcurrencyCheck](https://docs.microsoft.com/en-us/ef/core/modeling/concurrency#data-annotations).</span></span>

<span data-ttu-id="29317-159">`[ConcurrencyCheck]` 특성이이 자습서에서 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="29317-159">The `[ConcurrencyCheck]` attribute is not used in this tutorial.</span></span>

### <a name="detecting-concurrency-conflicts-on-a-row"></a><span data-ttu-id="29317-160">행에 대해 동시성 충돌 확인</span><span class="sxs-lookup"><span data-stu-id="29317-160">Detecting concurrency conflicts on a row</span></span>

<span data-ttu-id="29317-161">동시성 충돌을 검색 하는 [rowversion](https://docs.microsoft.com/sql/t-sql/data-types/rowversion-transact-sql) 는 모델에 추가 된 열을 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-161">To detect concurrency conflicts, a [rowversion](https://docs.microsoft.com/sql/t-sql/data-types/rowversion-transact-sql) tracking column is added to the model.</span></span>  <span data-ttu-id="29317-162">`rowversion` :</span><span class="sxs-lookup"><span data-stu-id="29317-162">`rowversion` :</span></span>

* <span data-ttu-id="29317-163">특정 SQL Server입니다.</span><span class="sxs-lookup"><span data-stu-id="29317-163">Is SQL Server specific.</span></span> <span data-ttu-id="29317-164">다른 데이터베이스 유사한 기능을 제공 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29317-164">Other databases may not provide a similar feature.</span></span>
* <span data-ttu-id="29317-165">DB에서 인출 된 이후로 변경 되지 않은 엔터티를 확인 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29317-165">Is used to determine that an entity has not been changed since it was fetched from the DB.</span></span> 

<span data-ttu-id="29317-166">DB 생성 순차적 `rowversion` 가 증가 될 때마다 행 개수 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29317-166">The DB generates a sequential `rowversion` number that's incremented each time the row is updated.</span></span> <span data-ttu-id="29317-167">에 `Update` 또는 `Delete` 명령에는 `Where` 절 인출 된 값이 포함 됩니다 `rowversion`합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-167">In an `Update` or `Delete` command, the `Where` clause includes the fetched value of `rowversion`.</span></span> <span data-ttu-id="29317-168">행이 업데이트 될 경우 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="29317-168">If the row being updated has changed:</span></span>

 * <span data-ttu-id="29317-169">`rowversion`인출 된 값을 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="29317-169">`rowversion` doesn't match the fetched value.</span></span>
 * <span data-ttu-id="29317-170">`Update` 또는 `Delete` 명령 때문에 행을 찾지 못한는 `Where` 절 포함 하 여 인출 된 `rowversion`합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-170">The `Update` or `Delete` commands don't find a row because the `Where` clause includes the fetched `rowversion`.</span></span>
 * <span data-ttu-id="29317-171">A `DbUpdateConcurrencyException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29317-171">A `DbUpdateConcurrencyException` is thrown.</span></span>

<span data-ttu-id="29317-172">EF 코어, 행이 없는으로 업데이트 한 후에 `Update` 또는 `Delete` 명령, 동시성 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29317-172">In EF Core, when no rows have been updated by an `Update` or `Delete` command, a concurrency exception is thrown.</span></span>

### <a name="add-a-tracking-property-to-the-department-entity"></a><span data-ttu-id="29317-173">추적 속성 부서 엔터티에 추가</span><span class="sxs-lookup"><span data-stu-id="29317-173">Add a tracking property to the Department entity</span></span>

<span data-ttu-id="29317-174">*Models/Department.cs*, RowVersion 라는 추적 속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-174">In *Models/Department.cs*, add a tracking property named RowVersion:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Department.cs?name=snippet_Final&highlight=26,27)]

<span data-ttu-id="29317-175">[타임 스탬프](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.timestampattribute) 특성 지정이 열에 포함 되어 있는지는 `Where` 절 `Update` 및 `Delete` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="29317-175">The [Timestamp](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.timestampattribute) attribute specifies that this column is included in the `Where` clause of `Update` and `Delete` commands.</span></span> <span data-ttu-id="29317-176">이 특성 이라고 `Timestamp` 이전 버전의 SQL Server는 SQL을 사용 하기 때문에 `timestamp` SQL 전에 데이터 형식 `rowversion` 형식 대체 했습니다.</span><span class="sxs-lookup"><span data-stu-id="29317-176">The attribute is called `Timestamp` because previous versions of SQL Server used a SQL `timestamp` data type before the SQL `rowversion` type replaced it.</span></span>

<span data-ttu-id="29317-177">Fluent API 추적 속성을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29317-177">The fluent API can also specify the tracking property:</span></span>

```csharp
modelBuilder.Entity<Department>()
  .Property<byte[]>("RowVersion")
  .IsRowVersion();
```

<span data-ttu-id="29317-178">다음 코드에서는 부서 이름 업데이트 될 때 EF 코어에서 생성 된 T-SQL의 일부를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="29317-178">The following code shows a portion of the T-SQL generated by EF Core when the Department name is updated:</span></span>

[!code-sql[](intro/samples/sql.txt?highlight=2-3)]

<span data-ttu-id="29317-179">위의 코드에서 보여 주는 강조 표시 됩니다는 `WHERE` 절이 포함 된 `RowVersion`합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-179">The preceding highlighted code shows the `WHERE` clause containing `RowVersion`.</span></span> <span data-ttu-id="29317-180">경우 DB `RowVersion` 와 같지 않습니다는 `RowVersion` 매개 변수 (`@p2`), 아무 행도 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29317-180">If the DB `RowVersion` doesn't equal the `RowVersion` parameter (`@p2`), no rows are updated.</span></span>

<span data-ttu-id="29317-181">다음 강조 표시 된 코드에는 정확히 한 개의 행이 업데이트를 확인 하는 T-SQL 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="29317-181">The following highlighted code shows the T-SQL that verifies exactly one row was updated:</span></span>

[!code-sql[](intro/samples/sql.txt?highlight=4-6)]

<span data-ttu-id="29317-182">[@@ROWCOUNT ](https://docs.microsoft.com/en-us/sql/t-sql/functions/rowcount-transact-sql) 마지막 문의 영향을 받는 행 수를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-182">[@@ROWCOUNT](https://docs.microsoft.com/en-us/sql/t-sql/functions/rowcount-transact-sql) returns the number of rows affected by the last statement.</span></span> <span data-ttu-id="29317-183">아무에서 행이 업데이트 되, EF 코어를 throw 한 `DbUpdateConcurrencyException`합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-183">In no rows are updated, EF Core throws a `DbUpdateConcurrencyException`.</span></span>

<span data-ttu-id="29317-184">Visual Studio의 출력 창에 T-SQL EF 코어 생성을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29317-184">You can see the T-SQL EF Core generates in the output window of Visual Studio.</span></span>

### <a name="update-the-db"></a><span data-ttu-id="29317-185">DB 업데이트</span><span class="sxs-lookup"><span data-stu-id="29317-185">Update the DB</span></span>

<span data-ttu-id="29317-186">추가 `RowVersion` 속성이 변경 되는 마이그레이션 마이그레이션해야 하는 DB 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="29317-186">Adding the `RowVersion` property changes the DB model, which requires a migration.</span></span>

<span data-ttu-id="29317-187">프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-187">Build the project.</span></span> <span data-ttu-id="29317-188">명령 창에서 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-188">Enter the following in a command window:</span></span>

```console
dotnet ef migrations add RowVersion
dotnet ef database update
```

<span data-ttu-id="29317-189">이전 명령:</span><span class="sxs-lookup"><span data-stu-id="29317-189">The preceding commands:</span></span>

* <span data-ttu-id="29317-190">추가 *마이그레이션 / {시간 stamp}_RowVersion.cs* 마이그레이션 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="29317-190">Adds the *Migrations/{time stamp}_RowVersion.cs* migration file.</span></span>
* <span data-ttu-id="29317-191">업데이트는 *Migrations/SchoolContextModelSnapshot.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="29317-191">Updates the *Migrations/SchoolContextModelSnapshot.cs* file.</span></span> <span data-ttu-id="29317-192">다음 강조 표시 된 코드를 추가 하는 업데이트는 `BuildModel` 메서드:</span><span class="sxs-lookup"><span data-stu-id="29317-192">The update adds the following highlighted code to the `BuildModel` method:</span></span>

[!code-csharp[Main](intro/samples/cu/Migrations/SchoolContextModelSnapshot2.cs?name=snippet&highlight=14-16)]

* <span data-ttu-id="29317-193">마이그레이션 DB 업데이트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-193">Runs migrations to update the DB.</span></span>

<a name="scaffold"></a>
## <a name="scaffold-the-departments-model"></a><span data-ttu-id="29317-194">스 캐 폴드 부서 모델</span><span class="sxs-lookup"><span data-stu-id="29317-194">Scaffold the Departments model</span></span>

* <span data-ttu-id="29317-195">Visual Studio를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-195">Exit Visual Studio.</span></span>
* <span data-ttu-id="29317-196">프로젝트 디렉터리(*Program.cs*, *Startup.cs* 및 *.csproj* 파일이 포함된 디렉터리)에서 명령 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="29317-196">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>
* <span data-ttu-id="29317-197">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-197">Run the following command:</span></span>

 ```console
dotnet aspnet-codegenerator razorpage -m Department -dc SchoolContext -udl -outDir Pages\Departments --referenceScriptLibraries
 ```

<span data-ttu-id="29317-198">위의 명령은 스 캐 폴드 된 `Department` 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="29317-198">The preceding command scaffolds the `Department` model.</span></span> <span data-ttu-id="29317-199">Visual Studio에서 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="29317-199">Open the project in Visual Studio.</span></span>

<span data-ttu-id="29317-200">프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-200">Build the project.</span></span> <span data-ttu-id="29317-201">빌드에서는 다음과 같은 오류를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-201">The build generates errors like the following:</span></span>

`1>Pages/Departments/Index.cshtml.cs(26,37,26,43): error CS1061: 'SchoolContext' does not
 contain a definition for 'Department' and no extension method 'Department' accepting a first
 argument of type 'SchoolContext' could be found (are you missing a using directive or
 an assembly reference?)`

 <span data-ttu-id="29317-202">전역으로 변경 `_context.Department` 를 `_context.Departments` (즉, "s"에 추가 `Department`).</span><span class="sxs-lookup"><span data-stu-id="29317-202">Globally change `_context.Department` to `_context.Departments` (that is, add an "s" to `Department`).</span></span> <span data-ttu-id="29317-203">7 번 발견 되 고 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29317-203">7 occurrences are found and updated.</span></span>

### <a name="update-the-departments-index-page"></a><span data-ttu-id="29317-204">부서 인덱스 페이지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-204">Update the Departments Index page</span></span>

<span data-ttu-id="29317-205">만든 스 캐 폴딩 엔진은 `RowVersion` 인덱스 페이지 이지만 해당 필드에 대 한 열을 표시 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-205">The scaffolding engine created a `RowVersion` column for the Index page, but that field shouldn't be displayed.</span></span> <span data-ttu-id="29317-206">이 자습서의 마지막 바이트는 `RowVersion` 동시성 이해 하기 위해 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29317-206">In this tutorial, the last byte of the `RowVersion` is displayed to help understand concurrency.</span></span> <span data-ttu-id="29317-207">마지막 바이트는 고유 하 게 보장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="29317-207">The last byte is not guaranteed to be unique.</span></span> <span data-ttu-id="29317-208">실제 앱 없게 표시 `RowVersion` 또는의 마지막 바이트 `RowVersion`합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-208">A real app wouldn't display `RowVersion` or the last byte of `RowVersion`.</span></span>

<span data-ttu-id="29317-209">인덱스 페이지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-209">Update the Index page:</span></span>

* <span data-ttu-id="29317-210">인덱스를 부서 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="29317-210">Replace Index with Departments.</span></span>
* <span data-ttu-id="29317-211">포함 하는 태그 대체 `RowVersion` 의 마지막 바이트와 `RowVersion`합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-211">Replace the markup containing `RowVersion` with the last byte of `RowVersion`.</span></span>
* <span data-ttu-id="29317-212">FullName FirstMidName 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-212">Replace FirstMidName with FullName.</span></span>

<span data-ttu-id="29317-213">다음 태그 업데이트 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="29317-213">The following markup shows the updated page:</span></span>

[!code-html[](intro/samples/cu/Pages/Departments/Index.cshtml?highlight=5,8,29,47,50)]

### <a name="update-the-edit-page-model"></a><span data-ttu-id="29317-214">편집 페이지 모델 업데이트</span><span class="sxs-lookup"><span data-stu-id="29317-214">Update the Edit page model</span></span>

<span data-ttu-id="29317-215">업데이트 *pages\departments\edit.cshtml.cs* 를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="29317-215">Update *pages\departments\edit.cshtml.cs* with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Departments/Edit.cshtml.cs?name=snippet)]

<span data-ttu-id="29317-216">동시성 문제를 감지 하는 [OriginalValue](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.changetracking.propertyentry.originalvalue?view=efcore-2.0#Microsoft_EntityFrameworkCore_ChangeTracking_PropertyEntry_OriginalValue) 으로 업데이트는 `rowVersion` 값이 인출 된 엔터티에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-216">To detect a concurrency issue, the [OriginalValue](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.changetracking.propertyentry.originalvalue?view=efcore-2.0#Microsoft_EntityFrameworkCore_ChangeTracking_PropertyEntry_OriginalValue) is updated with the `rowVersion` value from the entity it was fetched.</span></span> <span data-ttu-id="29317-217">EF 코어 원본이 포함 된 WHERE 절과 함께 SQL UPDATE 명령과 생성 `RowVersion` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="29317-217">EF Core generates a SQL UPDATE command with a WHERE clause containing the original `RowVersion` value.</span></span> <span data-ttu-id="29317-218">UPDATE 명령 영향을 받는 행이 없는 경우 (행이 없는 원래 `RowVersion` 값), 즉 `DbUpdateConcurrencyException` 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29317-218">If no rows are affected by the UPDATE command (no rows have the original `RowVersion` value), a `DbUpdateConcurrencyException` exception is thrown.</span></span>

[!code-csharp[](intro/samples/cu/Pages/Departments/Edit.cshtml.cs?name=snippet_rv&highlight=24-)]

<span data-ttu-id="29317-219">위의 코드에서 `Department.RowVersion` 엔터티를 인출할 때 값입니다.</span><span class="sxs-lookup"><span data-stu-id="29317-219">In the preceding code, `Department.RowVersion` is the value when the entity was fetched.</span></span> <span data-ttu-id="29317-220">`OriginalValue`DB에 값이 때 `FirstOrDefaultAsync` 이 메서드의 호출 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="29317-220">`OriginalValue` is the value in the DB when `FirstOrDefaultAsync` was called in this method.</span></span>

<span data-ttu-id="29317-221">다음 코드는 클라이언트 값 (이 메서드에 게시 된 값) 및 DB 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="29317-221">The following code gets the client values (the values posted to this method) and the DB values:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Departments/Edit.cshtml.cs?name=snippet_try&highlight=9,18)]

<span data-ttu-id="29317-222">DB가 있는 각 열에 게시 된 작업에서 다른 값에 대 한 사용자 지정 오류 메시지를 추가 하는 다음 코드 `OnPostAsync`:</span><span class="sxs-lookup"><span data-stu-id="29317-222">The follwing code adds a custom error message for each column that has DB values different from what was posted to `OnPostAsync`:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Departments/Edit.cshtml.cs?name=snippet_err)]

<span data-ttu-id="29317-223">다음 코드 집합을 강조 표시는 `RowVersion` DB에서 검색 된 값을 새 값입니다.</span><span class="sxs-lookup"><span data-stu-id="29317-223">The following highlighted code sets the `RowVersion` value to the new value retrieved from the DB.</span></span> <span data-ttu-id="29317-224">다음에 사용자가 클릭 **저장**, 이후 편집 페이지의 마지막 디스플레이 찾아낼 수는 발생 하는 동시성 오류만 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-224">The next time the user clicks **Save**, only concurrency errors that happen since the last display of the Edit page will be caught.</span></span>

[!code-csharp[](intro/samples/cu/Pages/Departments/Edit.cshtml.cs?name=snippet_try&highlight=23)]

<span data-ttu-id="29317-225">`ModelState.Remove` 때문에 문이 필요 않습니다 `ModelState` 이전에 `RowVersion` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="29317-225">The `ModelState.Remove` statement is required because `ModelState` has the old `RowVersion` value.</span></span> <span data-ttu-id="29317-226">Razor 페이지에는 `ModelState` 필드 우선 모델 속성 값은 둘 다 있는 경우에 대 한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="29317-226">In the Razor Page, the `ModelState` value for a field takes precedence over the model property values when both are present.</span></span>

## <a name="update-the-edit-page"></a><span data-ttu-id="29317-227">업데이트 편집 페이지</span><span class="sxs-lookup"><span data-stu-id="29317-227">Update the Edit page</span></span>

<span data-ttu-id="29317-228">업데이트 *Pages/Departments/Edit.cshtml* 다음 태그로:</span><span class="sxs-lookup"><span data-stu-id="29317-228">Update *Pages/Departments/Edit.cshtml* with the following markup:</span></span>

[!code-html[](intro/samples/cu/Pages/Departments/Edit.cshtml?highlight=1,14,16-17,37-39)]

<span data-ttu-id="29317-229">위의 태그:</span><span class="sxs-lookup"><span data-stu-id="29317-229">The preceding markup:</span></span>

* <span data-ttu-id="29317-230">업데이트는 `page` 지시어를 `@page` 를 `@page "{id:int}"`합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-230">Updates the `page` directive from `@page` to `@page "{id:int}"`.</span></span>
* <span data-ttu-id="29317-231">숨겨진된 행 버전을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-231">Adds a hidden row version.</span></span> <span data-ttu-id="29317-232">`RowVersion`다시 게시 값을 연결 하므로 추가 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-232">`RowVersion` must be added so post back binds the value.</span></span>
* <span data-ttu-id="29317-233">마지막 바이트 표시 `RowVersion` 디버깅 목적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-233">Displays the last byte of `RowVersion` for debugging purposes.</span></span>
* <span data-ttu-id="29317-234">대체 `ViewData` 강력한 형식의와 `InstructorNameSL`합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-234">Replaces `ViewData` with the strongly-typed `InstructorNameSL`.</span></span>

## <a name="test-concurrency-conflicts-with-the-edit-page"></a><span data-ttu-id="29317-235">동시성 충돌 편집 페이지를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-235">Test concurrency conflicts with the Edit page</span></span>

<span data-ttu-id="29317-236">영어 부서에 있는 편집의 두 브라우저 인스턴스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="29317-236">Open two browsers instances of Edit on the English department:</span></span>

* <span data-ttu-id="29317-237">응용 프로그램을 실행 하 고 부서를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-237">Run the app and select Departments.</span></span>
* <span data-ttu-id="29317-238">마우스 오른쪽 단추로 클릭는 **편집** 영어 부서 및 선택에 대 한 하이퍼링크 **새 탭에서 열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-238">Right-click the **Edit** hyperlink for the English department and select **Open in new tab**.</span></span>
* <span data-ttu-id="29317-239">첫 번째 탭을 클릭는 **편집** 영어 부서에 대 한 하이퍼링크입니다.</span><span class="sxs-lookup"><span data-stu-id="29317-239">In the first tab, click the **Edit** hyperlink for the English department.</span></span>

<span data-ttu-id="29317-240">두 개의 브라우저 탭 동일한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-240">The two browser tabs display the same information.</span></span>

<span data-ttu-id="29317-241">첫 번째 브라우저 탭에서 이름을 변경 하 고 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-241">Change the name in the first browser tab and click **Save**.</span></span>

![부서 편집 페이지 1 변경 후](concurrency/_static/edit-after-change-1.png)

<span data-ttu-id="29317-243">브라우저에서는 변경 된 값과 업데이트 된 rowVersion 표시기 인 인덱스 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="29317-243">The browser shows the Index page with the changed value and updated rowVersion indicator.</span></span> <span data-ttu-id="29317-244">업데이트 된 rowVersion 표시기 참고 기타 탭에 두 번째 포스트백에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29317-244">Note the updated rowVersion indicator, it is displayed on the second postback in the other tab.</span></span>

<span data-ttu-id="29317-245">두 번째 브라우저 탭에서 다른 필드를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-245">Change a different field in the second browser tab.</span></span>

![부서 편집 변경 후 2 페이지](concurrency/_static/edit-after-change-2.png)

<span data-ttu-id="29317-247">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-247">Click **Save**.</span></span> <span data-ttu-id="29317-248">DB 값과 일치 하지 않는 모든 필드에 대 한 오류 메시지 표시:</span><span class="sxs-lookup"><span data-stu-id="29317-248">You see error messages for all fields that don't match the DB values:</span></span>

![부서 편집 페이지 오류 메시지](concurrency/_static/edit-error.png)

<span data-ttu-id="29317-250">이 브라우저 창 Name 필드를 변경 하 려 하지 않았던 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-250">This browser window did not intend to change the Name field.</span></span> <span data-ttu-id="29317-251">복사 하 고 현재 값 (언어)의 이름 필드에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="29317-251">Copy and paste the current value (Languages) into the Name field.</span></span> <span data-ttu-id="29317-252">탭 합니다. 클라이언트 쪽 유효성 검사 오류 메시지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-252">Tab out. Client-side validation removes the error message.</span></span>

![부서 편집 페이지 오류 메시지](concurrency/_static/cv.png)

<span data-ttu-id="29317-254">클릭 **저장** 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-254">Click **Save** again.</span></span> <span data-ttu-id="29317-255">두 번째 브라우저 탭에 입력 한 값이 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29317-255">The value you entered in the second browser tab is saved.</span></span> <span data-ttu-id="29317-256">인덱스 페이지에 저장된 된 값을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-256">You see the saved values in the Index page.</span></span>

## <a name="update-the-delete-page"></a><span data-ttu-id="29317-257">업데이트 페이지 삭제</span><span class="sxs-lookup"><span data-stu-id="29317-257">Update the Delete page</span></span>

<span data-ttu-id="29317-258">다음 코드로 Delete 페이지 모델을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-258">Update the Delete page model with the following code:</span></span>

[!code-csharp[](intro/samples/cu/Pages/Departments/Delete.cshtml.cs)]

<span data-ttu-id="29317-259">페이지 삭제 된 엔터티가 인출 된 후 변경 될 때 동시성 충돌을 감지 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-259">The Delete page detects concurrency conflicts when the entity has changed after it was fetched.</span></span> <span data-ttu-id="29317-260">`Department.RowVersion`엔터티를 인출할 때 행 버전이입니다.</span><span class="sxs-lookup"><span data-stu-id="29317-260">`Department.RowVersion` is the row version when the entity was fetched.</span></span> <span data-ttu-id="29317-261">WHERE 절을 포함 EF 핵심 SQL DELETE 명령과 만들면 `RowVersion`합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-261">When EF Core creates the SQL DELETE command, it includes a WHERE clause with `RowVersion`.</span></span> <span data-ttu-id="29317-262">SQL DELETE 명령 결과가 0 인 행에 영향을 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-262">If the SQL DELETE command results in zero rows affected:</span></span>

* <span data-ttu-id="29317-263">`RowVersion` SQL DELETE 명령을 일치 하지 않습니다 `RowVersion` DB에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29317-263">The `RowVersion` in the SQL DELETE command doesn't match `RowVersion` in the DB.</span></span>
* <span data-ttu-id="29317-264">DbUpdateConcurrencyException 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29317-264">A DbUpdateConcurrencyException exception is thrown.</span></span>
* <span data-ttu-id="29317-265">`OnGetAsync`사용 하 여 호출 된 `concurrencyError`합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-265">`OnGetAsync` is called with the `concurrencyError`.</span></span>

### <a name="update-the-delete-page"></a><span data-ttu-id="29317-266">업데이트 페이지 삭제</span><span class="sxs-lookup"><span data-stu-id="29317-266">Update the Delete page</span></span>

<span data-ttu-id="29317-267">업데이트 *Pages/Departments/Delete.cshtml* 를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="29317-267">Update *Pages/Departments/Delete.cshtml* with the following code:</span></span>

[!code-html[](intro/samples/cu/Pages/Departments/Delete.cshtml?highlight=1,10,36,51)]


<span data-ttu-id="29317-268">위의 태그에서는 다음과 같이 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-268">The preceding markup makes the following changes:</span></span>

* <span data-ttu-id="29317-269">업데이트는 `page` 지시어를 `@page` 를 `@page "{id:int}"`합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-269">Updates the `page` directive from `@page` to `@page "{id:int}"`.</span></span>
* <span data-ttu-id="29317-270">오류 메시지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-270">Adds an error message.</span></span>
* <span data-ttu-id="29317-271">FullName FirstMidName 바꿉니다는 **관리자** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="29317-271">Replaces FirstMidName with FullName in the **Administrator** field.</span></span>
* <span data-ttu-id="29317-272">변경 내용을 `RowVersion` 마지막 바이트를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-272">Changes `RowVersion` to display the last byte.</span></span>
* <span data-ttu-id="29317-273">숨겨진된 행 버전을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-273">Adds a hidden row version.</span></span> <span data-ttu-id="29317-274">`RowVersion`다시 게시 값을 연결 하므로 추가 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-274">`RowVersion` must be added so post back binds the value.</span></span>

### <a name="test-concurrency-conflicts-with-the-delete-page"></a><span data-ttu-id="29317-275">Delete 페이지와 테스트 동시성 충돌</span><span class="sxs-lookup"><span data-stu-id="29317-275">Test concurrency conflicts with the Delete page</span></span>

<span data-ttu-id="29317-276">테스트 부서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29317-276">Create a test department.</span></span>

<span data-ttu-id="29317-277">테스트 부서에 Delete의 두 브라우저 인스턴스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="29317-277">Open two browsers instances of Delete on the test department:</span></span>

* <span data-ttu-id="29317-278">응용 프로그램을 실행 하 고 부서를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-278">Run the app and select Departments.</span></span>
* <span data-ttu-id="29317-279">마우스 오른쪽 단추로 클릭는 **삭제** 테스트 부서 및 선택에 대 한 하이퍼링크 **새 탭에서 열기**합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-279">Right-click the **Delete** hyperlink for the test department and select **Open in new tab**.</span></span>
* <span data-ttu-id="29317-280">클릭는 **편집** 테스트 부서에 대 한 하이퍼링크입니다.</span><span class="sxs-lookup"><span data-stu-id="29317-280">Click the **Edit** hyperlink for the test department.</span></span>

<span data-ttu-id="29317-281">두 개의 브라우저 탭 동일한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-281">The two browser tabs display the same information.</span></span>

<span data-ttu-id="29317-282">첫 번째 브라우저 탭에서 할당을 변경 하 고 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="29317-282">Change the budget in the first browser tab and click **Save**.</span></span>

<span data-ttu-id="29317-283">브라우저에서는 변경 된 값과 업데이트 된 rowVersion 표시기 인 인덱스 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="29317-283">The browser shows the Index page with the changed value and updated rowVersion indicator.</span></span> <span data-ttu-id="29317-284">업데이트 된 rowVersion 표시기 참고 기타 탭에 두 번째 포스트백에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29317-284">Note the updated rowVersion indicator, it is displayed on the second postback in the other tab.</span></span>

<span data-ttu-id="29317-285">두 번째 탭에서 테스트 부서를 삭제 합니다. 동시성 오류는 DB의 현재 값으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29317-285">Delete the test department from the second tab. A concurrency error is display with the current values from the DB.</span></span> <span data-ttu-id="29317-286">클릭 하면 **삭제** 되지 않는 한 엔터티를 삭제 `RowVersion` updated.department가 삭제 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="29317-286">Clicking **Delete** deletes the entity, unless `RowVersion` has been updated.department has been deleted.</span></span>

<span data-ttu-id="29317-287">참조 [상속](xref:data/ef-mvc/inheritance) 데이터 모델을 상속 하는 방법에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29317-287">See [Inheritance](xref:data/ef-mvc/inheritance) on how to inherit a data model.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="29317-288">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="29317-288">Additional resources</span></span>

* [<span data-ttu-id="29317-289">EF 코어의 동시성 토큰</span><span class="sxs-lookup"><span data-stu-id="29317-289">Concurrency Tokens in EF Core</span></span>](https://docs.microsoft.com/en-us/ef/core/modeling/concurrency)
* [<span data-ttu-id="29317-290">EF 코어에서 동시성 처리</span><span class="sxs-lookup"><span data-stu-id="29317-290">Handling concurrency in EF Core</span></span>](https://docs.microsoft.com/en-us/ef/core/saving/concurrency)

>[!div class="step-by-step"]
[<span data-ttu-id="29317-291">이전</span><span class="sxs-lookup"><span data-stu-id="29317-291">Previous</span></span>](xref:data/ef-rp/update-related-data)
