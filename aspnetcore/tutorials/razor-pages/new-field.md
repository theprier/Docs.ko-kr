---
title: "Razor 페이지에 새 필드 추가"
author: rick-anderson
description: "Entity Framework Core를 사용하여 Razor 페이지에 새 필드를 추가하는 방법을 보여 줍니다."
manager: wpickett
ms.author: riande
ms.date: 08/07/2017
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/razor-pages/new-field
ms.openlocfilehash: 36412e9d1f3143f0d1999d0e754e6627f0984ad5
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="adding-a-new-field-to-a-razor-page"></a><span data-ttu-id="d2b23-103">Razor 페이지에 새 필드 추가</span><span class="sxs-lookup"><span data-stu-id="d2b23-103">Adding a new field to a Razor Page</span></span>

<span data-ttu-id="d2b23-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="d2b23-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="d2b23-105">이 섹션에서는 [Entity Framework](https://docs.microsoft.com/ef/core/get-started/aspnetcore/new-db) Code First 마이그레이션을 사용하여 모델에 새 필드를 추가하고 해당 변경 내용을 데이터베이스로 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-105">In this section you'll use [Entity Framework](https://docs.microsoft.com/ef/core/get-started/aspnetcore/new-db) Code First Migrations to add a new field to the model and migrate that change to the database.</span></span>

<span data-ttu-id="d2b23-106">EF Code First를 사용하여 자동으로 데이터베이스를 만들 때 Code First는 데이터베이스에 테이블을 추가하여 데이터베이스의 스키마가 생성된 모델 클래스와 동기화되어 있는지 여부를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-106">When you use EF Code First to automatically create a database, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="d2b23-107">동기화되어 있지 않은 경우 EF에서 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-107">If they aren't in sync, EF throws an exception.</span></span> <span data-ttu-id="d2b23-108">이렇게 하면 더 쉽게 일관성이 없는 데이터베이스/코드 문제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-108">This makes it easier to find inconsistent database/code issues.</span></span>

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="d2b23-109">동영상 모델에 등급 속성 추가</span><span class="sxs-lookup"><span data-stu-id="d2b23-109">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="d2b23-110">*Models/Movie.cs* 파일을 열고 `Rating` 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-110">Open the *Models/Movie.cs* file and add a `Rating` property:</span></span>

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Models/MovieDateRating.cs?highlight=11&range=7-18)]

<span data-ttu-id="d2b23-111">앱을 빌드합니다(Ctrl+Shift+B).</span><span class="sxs-lookup"><span data-stu-id="d2b23-111">Build the app (Ctrl+Shift+B).</span></span>

<span data-ttu-id="d2b23-112">*Pages/Movies/Index.cshtml*를 편집하고 `Rating` 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-112">Edit *Pages/Movies/Index.cshtml*, and add a `Rating` field:</span></span>

[!code-cshtml[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Index.cshtml?highlight=40-42,61-63)]

<span data-ttu-id="d2b23-113">삭제 및 세부 정보 페이지에 `Rating` 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-113">Add the `Rating` field to the Delete and Details pages.</span></span>

<span data-ttu-id="d2b23-114">*Create.cshtml*을 `Rating` 필드로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-114">Update *Create.cshtml* with a `Rating` field.</span></span> <span data-ttu-id="d2b23-115">이전 `<div>` 요소를 복사/붙여넣기하고 intelliSense에서 필드를 업데이트하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-115">You can copy/paste the previous `<div>` element and let intelliSense help you update the fields.</span></span> <span data-ttu-id="d2b23-116">IntelliSense는 [태그 도우미](xref:mvc/views/tag-helpers/intro)와 함께 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-116">IntelliSense works with [Tag Helpers](xref:mvc/views/tag-helpers/intro).</span></span>

![개발자가 보기의 두 번째 레이블 요소에서 asp-for의 특성 값에 대해 문자 R을 입력했습니다.](new-field/_static/cr.png)

<span data-ttu-id="d2b23-120">다음 코드는 `Rating` 필드와 함께 *Create.cshtml*을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-120">The following code shows *Create.cshtml* with a `Rating` field:</span></span>

[!code-cshtml[Main](razor-pages-start/sample/RazorPagesMovie/Pages/Movies/Create.cshtml?highlight=36-40)]

<span data-ttu-id="d2b23-121">편집 페이지에 `Rating` 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-121">Add the `Rating` field to the Edit Page.</span></span>

<span data-ttu-id="d2b23-122">앱은 새 필드를 포함하도록 DB가 업데이트될 때까지 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-122">The app won't work until the DB is updated to include the new field.</span></span> <span data-ttu-id="d2b23-123">지금 실행하면 앱은 `SqlException`을 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-123">If run now, the app throws a `SqlException`:</span></span>

```
SqlException: Invalid column name 'Rating'.
```

<span data-ttu-id="d2b23-124">이 오류는 데이터베이스의 동영상 테이블의 스키마와 다른 업데이트된 동영상 모델 클래스로 인해 발생됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-124">This error is caused by the updated Movie model class being different than the schema of the Movie table of the database.</span></span> <span data-ttu-id="d2b23-125">(데이터베이스 테이블에 `Rating` 열이 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="d2b23-125">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="d2b23-126">오류를 해결하는 몇 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-126">There are a few approaches to resolving the error:</span></span>

1. <span data-ttu-id="d2b23-127">Entity Framework에서 새 모델 클래스 스키마를 사용하여 데이터베이스를 자동으로 삭제하고 다시 만들도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-127">Have the Entity Framework automatically drop and re-create the database using  the new model class schema.</span></span> <span data-ttu-id="d2b23-128">이 방법은 개발 주기의 초기 단계에서 편리하며 신속하게 모델 및 데이터베이스 스키마를 함께 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-128">This approach is convenient early in the development cycle; it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="d2b23-129">단점은 데이터베이스의 기존 데이터를 잃게 된다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-129">The downside is that you lose existing data in the database.</span></span> <span data-ttu-id="d2b23-130">프로덕션 데이터베이스에서 이러한 방법을 사용하지 않으려 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-130">You don't want to use this approach on a production database!</span></span> <span data-ttu-id="d2b23-131">테스트 데이터로 데이터베이스를 자동으로 시드하도록 스키마에서 DB를 삭제하고 이니셜라이저를 사용하는 것은 종종 앱을 개발하는 효율적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-131">Dropping the DB on schema changes and using an initializer to automatically seed the database with test data is often a productive way to develop an app.</span></span>

2. <span data-ttu-id="d2b23-132">모델 클래스와 일치하도록 기존 데이터베이스의 스키마를 명시적으로 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-132">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="d2b23-133">이 방법의 장점은 데이터를 유지한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-133">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="d2b23-134">이러한 변경을 수동으로 수행하거나 데이터베이스 변경 스크립트를 만들어 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-134">You can make this change either manually or by creating a database change script.</span></span>

3. <span data-ttu-id="d2b23-135">Code First 마이그레이션을 사용하여 데이터베이스 스키마를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-135">Use Code First Migrations to update the database schema.</span></span>

<span data-ttu-id="d2b23-136">이 자습서의 경우 Code First 마이그레이션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-136">For this tutorial, use Code First Migrations.</span></span>

<span data-ttu-id="d2b23-137">새 열에 대해 값을 제공하도록 `SeedData` 클래스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-137">Update the `SeedData` class so that it provides a value for the new column.</span></span> <span data-ttu-id="d2b23-138">샘플 변경은 아래에 표시되지만 각 `new Movie` 블록에 대해 이 변경을 수행하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-138">A sample change is shown below, but you'll want to make this change for each `new Movie` block.</span></span>

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Models/SeedDataRating.cs?name=snippet1&highlight=8)]

<span data-ttu-id="d2b23-139">[완료된 SeedData.cs 파일](https://github.com/aspnet/Docs/blob/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Models/SeedDataRating.cs)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2b23-139">See the [completed SeedData.cs file](https://github.com/aspnet/Docs/blob/master/aspnetcore/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Models/SeedDataRating.cs).</span></span>

<span data-ttu-id="d2b23-140">솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-140">Build the solution.</span></span>

<a name="pmc"></a> <span data-ttu-id="d2b23-141">**도구** 메뉴에서 **NuGet 패키지 관리자 > 패키지 관리자 콘솔**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-141">From the **Tools** menu, select **NuGet Package Manager > Package Manager Console**.</span></span>
<span data-ttu-id="d2b23-142">PMC에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-142">In the PMC, enter the following commands:</span></span>

```powershell
Add-Migration Rating
Update-Database
```

<span data-ttu-id="d2b23-143">`Add-Migration` 명령은 프레임워크에 다음 작업을 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-143">The `Add-Migration` command tells the framework to:</span></span>

* <span data-ttu-id="d2b23-144">`Movie` 모델을 `Movie` DB 스키마와 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-144">Compare the `Movie` model with the `Movie` DB schema.</span></span>
* <span data-ttu-id="d2b23-145">DB 스키마를 새 모델로 마이그레이션하도록 코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-145">Create code to migrate the DB schema to the new model.</span></span>

<span data-ttu-id="d2b23-146">"Rating" 이름은 임의로 지정되며 마이그레이션 파일의 이름을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-146">The name "Rating" is arbitrary and is used to name the migration file.</span></span> <span data-ttu-id="d2b23-147">마이그레이션 파일에 의미 있는 이름을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-147">It's helpful to use a meaningful name for the migration file.</span></span>

<a name="ssox"></a> <span data-ttu-id="d2b23-148">DB의 모든 레코드를 삭제하는 경우 이니셜라이저에서 DB를 시드하고 `Rating` 필드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-148">If you delete all the records in the DB, the initializer will seed the DB and include the `Rating` field.</span></span> <span data-ttu-id="d2b23-149">브라우저 또는 [SSOX](xref:tutorials/razor-pages/sql#ssox)(Sql Server 개체 탐색기)에서 삭제 링크를 사용하여 이를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-149">You can do this with the delete links in the browser or from [Sql Server Object Explorer](xref:tutorials/razor-pages/sql#ssox) (SSOX).</span></span> <span data-ttu-id="d2b23-150">SSOX에서 데이터베이스를 삭제하려면:</span><span class="sxs-lookup"><span data-stu-id="d2b23-150">To delete the database from SSOX:</span></span>

* <span data-ttu-id="d2b23-151">SSOX에서 데이터베이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-151">Select the database in SSOX.</span></span>
* <span data-ttu-id="d2b23-152">데이터베이스를 마우스 오른쪽 단추로 클릭하고 *삭제*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-152">Right click on the database, and select *Delete*.</span></span>
* <span data-ttu-id="d2b23-153">**기존 연결 닫기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-153">Check **Close existing connections**.</span></span>
* <span data-ttu-id="d2b23-154">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-154">Select **OK**.</span></span>
* <span data-ttu-id="d2b23-155">[PMC](xref:tutorials/razor-pages/new-field#pmc)에서 데이터베이스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-155">In the [PMC](xref:tutorials/razor-pages/new-field#pmc), update the database:</span></span>

  ```powershell
  Update-Database
  ```

<span data-ttu-id="d2b23-156">앱을 실행하고 `Rating` 필드를 사용하여 동영상을 만들고/편집/표시할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-156">Run the app and verify you can create/edit/display movies with a `Rating` field.</span></span> <span data-ttu-id="d2b23-157">데이터베이스가 시드되지 않은 경우 IIS Express를 중지한 다음 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b23-157">If the database isn't seeded, stop IIS Express, and then run the app.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="d2b23-158">[이전: 검색 추가](xref:tutorials/razor-pages/search)
[다음: 유효성 검사 추가](xref:tutorials/razor-pages/validation)</span><span class="sxs-lookup"><span data-stu-id="d2b23-158">[Previous: Adding Search](xref:tutorials/razor-pages/search)
[Next: Adding Validation](xref:tutorials/razor-pages/validation)</span></span>
