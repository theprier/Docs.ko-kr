---
title: ASP.NET Core의 Razor 페이지에 새 필드 추가
author: rick-anderson
description: Entity Framework Core를 사용하여 Razor 페이지에 새 필드를 추가하는 방법을 보여 줍니다.
ms.author: riande
ms.custom: mvc
ms.date: 12/5/2018
uid: tutorials/razor-pages/new-field
ms.openlocfilehash: f8661a48ddd6fc616c141435edc603117b4925fb
ms.sourcegitcommit: 036d4b03fd86ca5bb378198e29ecf2704257f7b2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57345895"
---
# <a name="add-a-new-field-to-a-razor-page-in-aspnet-core"></a><span data-ttu-id="1f722-103">ASP.NET Core의 Razor 페이지에 새 필드 추가</span><span class="sxs-lookup"><span data-stu-id="1f722-103">Add a new field to a Razor Page in ASP.NET Core</span></span>

<span data-ttu-id="1f722-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="1f722-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE[](~/includes/rp/download.md)]

<span data-ttu-id="1f722-105">[Entity Framework](/ef/core/get-started/aspnetcore/new-db) 단원에서 Code First 마이그레이션은 다음 작업에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-105">In this section [Entity Framework](/ef/core/get-started/aspnetcore/new-db) Code First Migrations is used to:</span></span>

* <span data-ttu-id="1f722-106">모델에 새 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-106">Add a new field to the model.</span></span>
* <span data-ttu-id="1f722-107">데이터베이스로 새 필드 스키마 변경 내용을 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-107">Migrate the new field schema change to the database.</span></span>

<span data-ttu-id="1f722-108">EF Code First를 사용하여 자동으로 데이터베이스를 만들 경우 Code First는</span><span class="sxs-lookup"><span data-stu-id="1f722-108">When using EF Code First to automatically create a database, Code First:</span></span>

* <span data-ttu-id="1f722-109">데이터베이스에 테이블을 추가하여 데이터베이스의 스키마가 생성된 모델 클래스와 동기화되어 있는지 여부를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-109">Adds a table to the database to track whether the schema of the database is in sync with the model classes it was generated from.</span></span>
* <span data-ttu-id="1f722-110">모델 클래스가 DB와 동기화되지 않으면 EF는 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-110">If the model classes aren't in sync with the DB, EF throws an exception.</span></span>

<span data-ttu-id="1f722-111">동기화된 스키마/모델의 자동 확인을 통해 일관성이 없는 데이터베이스/코드 문제를 쉽게 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-111">Automatic verification of schema/model in sync makes it easier to find inconsistent database/code issues.</span></span>

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="1f722-112">영화 모델에 등급 속성 추가</span><span class="sxs-lookup"><span data-stu-id="1f722-112">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="1f722-113">*Models/Movie.cs* 파일을 열고 `Rating` 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-113">Open the *Models/Movie.cs* file and add a `Rating` property:</span></span>

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie22/Models/MovieDateRating.cs?highlight=13&name=snippet)]

<span data-ttu-id="1f722-114">앱을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-114">Build the app.</span></span>

<span data-ttu-id="1f722-115">*Pages/Movies/Index.cshtml*를 편집하고 `Rating` 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-115">Edit *Pages/Movies/Index.cshtml*, and add a `Rating` field:</span></span>

[!code-cshtml[](razor-pages-start/sample/RazorPagesMovie22/Pages/Movies/IndexRating.cshtml.?highlight=40-42,61-63)]

<span data-ttu-id="1f722-116">다음 페이지를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-116">Update the following pages:</span></span>

* <span data-ttu-id="1f722-117">삭제 및 세부 정보 페이지에 `Rating` 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-117">Add the `Rating` field to the Delete and Details pages.</span></span>
* <span data-ttu-id="1f722-118">[Create.cshtml](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Pages/Movies/Create.cshtml)을 `Rating` 필드로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-118">Update [Create.cshtml](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Pages/Movies/Create.cshtml) with a `Rating` field.</span></span>
* <span data-ttu-id="1f722-119">편집 페이지에 `Rating` 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-119">Add the `Rating` field to the Edit Page.</span></span>

<span data-ttu-id="1f722-120">앱은 새 필드를 포함하도록 DB가 업데이트될 때까지 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-120">The app won't work until the DB is updated to include the new field.</span></span> <span data-ttu-id="1f722-121">지금 실행하면 앱은 `SqlException`을 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-121">If run now, the app throws a `SqlException`:</span></span>

`SqlException: Invalid column name 'Rating'.`

<span data-ttu-id="1f722-122">이 오류는 데이터베이스의 동영상 테이블의 스키마와 다른 업데이트된 동영상 모델 클래스로 인해 발생됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-122">This error is caused by the updated Movie model class being different than the schema of the Movie table of the database.</span></span> <span data-ttu-id="1f722-123">(데이터베이스 테이블에 `Rating` 열이 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="1f722-123">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="1f722-124">오류를 해결하는 몇 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-124">There are a few approaches to resolving the error:</span></span>

1. <span data-ttu-id="1f722-125">새 모델 클래스 스키마를 사용하여 Entity Framework를 자동으로 삭제하고 데이터베이스를 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-125">Have the Entity Framework automatically drop and re-create the database using the new model class schema.</span></span> <span data-ttu-id="1f722-126">이 방법은 개발 주기의 초기 단계에서 편리하며 신속하게 모델 및 데이터베이스 스키마를 함께 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-126">This approach is convenient early in the development cycle; it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="1f722-127">단점은 데이터베이스의 기존 데이터를 잃게 된다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-127">The downside is that you lose existing data in the database.</span></span> <span data-ttu-id="1f722-128">프로덕션 데이터베이스에서 이 방법을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="1f722-128">Don't use this approach on a production database!</span></span> <span data-ttu-id="1f722-129">테스트 데이터로 데이터베이스를 자동으로 시드하도록 스키마에서 DB를 삭제하고 이니셜라이저를 사용하는 것은 종종 앱을 개발하는 효율적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-129">Dropping the DB on schema changes and using an initializer to automatically seed the database with test data is often a productive way to develop an app.</span></span>

2. <span data-ttu-id="1f722-130">모델 클래스와 일치하도록 기존 데이터베이스의 스키마를 명시적으로 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-130">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="1f722-131">이 방법의 장점은 데이터를 유지한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-131">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="1f722-132">이러한 변경을 수동으로 수행하거나 데이터베이스 변경 스크립트를 만들어 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-132">You can make this change either manually or by creating a database change script.</span></span>

3. <span data-ttu-id="1f722-133">Code First 마이그레이션을 사용하여 데이터베이스 스키마를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-133">Use Code First Migrations to update the database schema.</span></span>

<span data-ttu-id="1f722-134">이 자습서의 경우 Code First 마이그레이션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-134">For this tutorial, use Code First Migrations.</span></span>

<span data-ttu-id="1f722-135">새 열에 대해 값을 제공하도록 `SeedData` 클래스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-135">Update the `SeedData` class so that it provides a value for the new column.</span></span> <span data-ttu-id="1f722-136">샘플 변경은 아래에 표시되지만 각 `new Movie` 블록에 대해 이 변경을 수행하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-136">A sample change is shown below, but you'll want to make this change for each `new Movie` block.</span></span>

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie22/Models/SeedDataRating.cs?name=snippet1&highlight=8)]

<span data-ttu-id="1f722-137">[완료된 SeedData.cs 파일](https://github.com/aspnet/Docs/blob/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Models/SeedDataRating.cs)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f722-137">See the [completed SeedData.cs file](https://github.com/aspnet/Docs/blob/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Models/SeedDataRating.cs).</span></span>

<span data-ttu-id="1f722-138">솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-138">Build the solution.</span></span>

<!-- VS -------------------------->
# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="1f722-139">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1f722-139">Visual Studio</span></span>](#tab/visual-studio)

<a name="pmc"></a>

### <a name="add-a-migration-for-the-rating-field"></a><span data-ttu-id="1f722-140">등급 필드에 대한 마이그레이션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-140">Add a migration for the rating field</span></span>

<span data-ttu-id="1f722-141">**도구** 메뉴에서 **NuGet 패키지 관리자 > 패키지 관리자 콘솔**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-141">From the **Tools** menu, select **NuGet Package Manager > Package Manager Console**.</span></span>
<span data-ttu-id="1f722-142">PMC에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-142">In the PMC, enter the following commands:</span></span>

```powershell
Add-Migration Rating
Update-Database
```

<span data-ttu-id="1f722-143">`Add-Migration` 명령은 프레임워크에 다음 작업을 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-143">The `Add-Migration` command tells the framework to:</span></span>

* <span data-ttu-id="1f722-144">`Movie` 모델을 `Movie` DB 스키마와 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-144">Compare the `Movie` model with the `Movie` DB schema.</span></span>
* <span data-ttu-id="1f722-145">DB 스키마를 새 모델로 마이그레이션하도록 코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-145">Create code to migrate the DB schema to the new model.</span></span>

<span data-ttu-id="1f722-146">"Rating" 이름은 임의로 지정되며 마이그레이션 파일의 이름을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-146">The name "Rating" is arbitrary and is used to name the migration file.</span></span> <span data-ttu-id="1f722-147">마이그레이션 파일에 의미 있는 이름을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-147">It's helpful to use a meaningful name for the migration file.</span></span>

<span data-ttu-id="1f722-148">`Update-Database` 명령은 스키마 변경 내용을 데이터베이스에 적용하기 위한 프레임워크를 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-148">The `Update-Database` command tells the framework to apply the schema changes to the database.</span></span>

<a name="ssox"></a>

<span data-ttu-id="1f722-149">DB의 모든 레코드를 삭제하는 경우 이니셜라이저에서 DB를 시드하고 `Rating` 필드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-149">If you delete all the records in the DB, the initializer will seed the DB and include the `Rating` field.</span></span> <span data-ttu-id="1f722-150">브라우저 또는 [SSOX](xref:tutorials/razor-pages/sql#ssox)(Sql Server 개체 탐색기)에서 삭제 링크를 사용하여 이를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-150">You can do this with the delete links in the browser or from [Sql Server Object Explorer](xref:tutorials/razor-pages/sql#ssox) (SSOX).</span></span>

<span data-ttu-id="1f722-151">다른 옵션은 데이터베이스를 삭제하고 마이그레이션을 사용하여 데이터베이스를 다시 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-151">Another option is to delete the database and use migrations to re-create the database.</span></span> <span data-ttu-id="1f722-152">SSOX에서 데이터베이스를 삭제하려면:</span><span class="sxs-lookup"><span data-stu-id="1f722-152">To delete the database in SSOX:</span></span>

* <span data-ttu-id="1f722-153">SSOX에서 데이터베이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-153">Select the database in SSOX.</span></span>
* <span data-ttu-id="1f722-154">데이터베이스를 마우스 오른쪽 단추로 클릭하고 *삭제*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-154">Right click on the database, and select *Delete*.</span></span>
* <span data-ttu-id="1f722-155">**기존 연결 닫기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-155">Check **Close existing connections**.</span></span>
* <span data-ttu-id="1f722-156">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-156">Select **OK**.</span></span>
* <span data-ttu-id="1f722-157">[PMC](xref:tutorials/razor-pages/new-field#pmc)에서 데이터베이스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-157">In the [PMC](xref:tutorials/razor-pages/new-field#pmc), update the database:</span></span>

  ```powershell
  Update-Database
  ```

<!-- Code -------------------------->
# <a name="visual-studio-code--visual-studio-for-mactabvisual-studio-codevisual-studio-mac"></a>[<span data-ttu-id="1f722-158">Visual Studio Code / Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="1f722-158">Visual Studio Code / Visual Studio for Mac</span></span>](#tab/visual-studio-code+visual-studio-mac)

<!-- copy/paste this tab to the next. Not worth an include  -->

<span data-ttu-id="1f722-159">다음 .NET Core CLI 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-159">Run the following .NET Core CLI commands:</span></span>

```console
dotnet ef migrations add Rating
dotnet ef database update
```

<span data-ttu-id="1f722-160">`ef migrations add` 명령은 프레임워크에 다음 작업을 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-160">The `ef migrations add` command tells the framework to:</span></span>

* <span data-ttu-id="1f722-161">`Movie` 모델을 `Movie` DB 스키마와 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-161">Compare the `Movie` model with the `Movie` DB schema.</span></span>
* <span data-ttu-id="1f722-162">DB 스키마를 새 모델로 마이그레이션하도록 코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-162">Create code to migrate the DB schema to the new model.</span></span>

<span data-ttu-id="1f722-163">"Rating" 이름은 임의로 지정되며 마이그레이션 파일의 이름을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-163">The name "Rating" is arbitrary and is used to name the migration file.</span></span> <span data-ttu-id="1f722-164">마이그레이션 파일에 의미 있는 이름을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-164">It's helpful to use a meaningful name for the migration file.</span></span>

<span data-ttu-id="1f722-165">`ef database update` 명령은 스키마 변경 내용을 데이터베이스에 적용하기 위한 프레임워크를 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-165">The `ef database update` command tells the framework to apply the schema changes to the database.</span></span>

<span data-ttu-id="1f722-166">DB의 모든 레코드를 삭제하는 경우 이니셜라이저에서 DB를 시드하고 `Rating` 필드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-166">If you delete all the records in the DB, the initializer will seed the DB and include the `Rating` field.</span></span> <span data-ttu-id="1f722-167">브라우저의 삭제 링크를 사용하거나 SQLite 도구를 사용하여 이를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-167">You can do this with the delete links in the browser or by using a SQLite tool.</span></span>

<span data-ttu-id="1f722-168">다른 옵션은 데이터베이스를 삭제하고 마이그레이션을 사용하여 데이터베이스를 다시 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-168">Another option is to delete the database and use migrations to re-create the database.</span></span> <span data-ttu-id="1f722-169">데이터베이스를 삭제하려면 데이터베이스 파일(*MvcMovie.db*)을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-169">To delete the database, delete the database file (*MvcMovie.db*).</span></span> <span data-ttu-id="1f722-170">그런 다음, `ef database update` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-170">Then run the `ef database update` command:</span></span> 

```console
dotnet ef database update
```

> [!NOTE]
> <span data-ttu-id="1f722-171">다양한 스키마 변경 작업은 EF Core SQLite 공급자에서 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-171">Many schema change operations are not supported by the EF Core SQLite provider.</span></span> <span data-ttu-id="1f722-172">예를 들어 열 추가는 지원되지만 열 제거는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-172">For example, adding a column is supported, but removing a column is not supported.</span></span> <span data-ttu-id="1f722-173">열을 제거하기 위해 마이그레이션을 추가하면 `ef migrations add` 명령은 성공하지만 `ef database update` 명령은 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-173">If you add a migration to remove a column, the `ef migrations add` command succeeds but the `ef database update` command fails.</span></span> <span data-ttu-id="1f722-174">수동으로 마이그레이션 코드를 작성하여 테이블 다시 빌드를 수행함으로써 코드를 몇 가지 제한 사항을 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-174">You can work around some of the limitations by manually writing migrations code to perform a table rebuild.</span></span> <span data-ttu-id="1f722-175">테이블 다시 빌드에는 기존 테이블 이름 바꾸기, 새 테이블 만들기, 새 테이블에 데이터 복사 및 이전 테이블 삭제가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-175">A table rebuild involves renaming the existing table, creating a new table, copying data to the new table, and dropping the old table.</span></span> <span data-ttu-id="1f722-176">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f722-176">For more information, see the following resources:</span></span>
> * [<span data-ttu-id="1f722-177">SQLite EF Core 데이터베이스 공급자 제한 사항</span><span class="sxs-lookup"><span data-stu-id="1f722-177">SQLite EF Core Database Provider Limitations</span></span>](/ef/core/providers/sqlite/limitations)
> * [<span data-ttu-id="1f722-178">마이그레이션 코드 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="1f722-178">Customize migration code</span></span>](/ef/core/managing-schemas/migrations/#customize-migration-code)
> * [<span data-ttu-id="1f722-179">데이터 시드</span><span class="sxs-lookup"><span data-stu-id="1f722-179">Data seeding</span></span>](/ef/core/modeling/data-seeding)

---  
<!-- End of VS tabs -->

<span data-ttu-id="1f722-180">앱을 실행하고 `Rating` 필드를 사용하여 동영상을 만들고/편집/표시할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-180">Run the app and verify you can create/edit/display movies with a `Rating` field.</span></span> <span data-ttu-id="1f722-181">데이터베이스가 시드되지 않은 경우 `SeedData.Initialize` 메서드에서 중단점을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1f722-181">If the database isn't seeded, set a break point in the `SeedData.Initialize` method.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1f722-182">추가 자료</span><span class="sxs-lookup"><span data-stu-id="1f722-182">Additional resources</span></span>

* [<span data-ttu-id="1f722-183">이 자습서의 YouTube 버전</span><span class="sxs-lookup"><span data-stu-id="1f722-183">YouTube version of this tutorial</span></span>](https://youtu.be/3i7uMxiGGR8)

> [!div class="step-by-step"]
> <span data-ttu-id="1f722-184">[이전: 검색 추가](xref:tutorials/razor-pages/search)
> [다음: 유효성 검사 추가](xref:tutorials/razor-pages/validation)</span><span class="sxs-lookup"><span data-stu-id="1f722-184">[Previous: Adding Search](xref:tutorials/razor-pages/search)
[Next: Adding Validation](xref:tutorials/razor-pages/validation)</span></span>
