---
uid: mvc/overview/getting-started/introduction/adding-a-new-field
title: "새 필드 추가 | Microsoft Docs"
author: Rick-Anderson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/17/2013
ms.topic: article
ms.assetid: 4085de68-d243-4378-8a64-86236ea8d2da
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: 7427b4f7c6b7a00fe795053aac0f612471a163cd
ms.sourcegitcommit: 2b263e87217658caa42eedc4f9d2d21ef0ab5d59
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/12/2018
---
<a name="adding-a-new-field"></a><span data-ttu-id="99214-102">새 필드 추가</span><span class="sxs-lookup"><span data-stu-id="99214-102">Adding a New Field</span></span>
====================
<span data-ttu-id="99214-103">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="99214-103">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

[!INCLUDE[Tutorial Note](sample/code-location.md)]

<span data-ttu-id="99214-104">이 섹션에서는 변경 내용이 데이터베이스에 적용 되므로 일부 변경 내용이 모델 클래스 마이그레이션할 Entity Framework Code First 마이그레이션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-104">In this section you'll use Entity Framework Code First Migrations to migrate some changes to the model classes so the change is applied to the database.</span></span>

<span data-ttu-id="99214-105">기본적으로를 사용 하 여 Entity Framework Code First 자동으로 데이터베이스를 만들려면이 자습서의 앞부분에서 마찬가지로 코드 첫 번째 테이블에 추가 데이터베이스는 데이터베이스의 스키마에서 생성 된 모델 클래스 동기화 되어 있는지 여부를 추적 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-105">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="99214-106">동기화 하지 않을 경우 Entity Framework에서 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-106">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="99214-107">이렇게 하면 그렇지 않으면만 찾을 수 (모호한 오류)에 의해 런타임 시 개발 시 문제를 추적 하기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99214-107">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span>

## <a name="setting-up-code-first-migrations-for-model-changes"></a><span data-ttu-id="99214-108">Code First 마이그레이션을 모델 변경 내용에 대 한 설정</span><span class="sxs-lookup"><span data-stu-id="99214-108">Setting up Code First Migrations for Model Changes</span></span>

<span data-ttu-id="99214-109">솔루션 탐색기로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-109">Navigate to Solution Explorer.</span></span> <span data-ttu-id="99214-110">마우스 오른쪽 단추로 클릭는 *Movies.mdf* 파일을 선택 **삭제** 영화 데이터베이스를 제거 하려면.</span><span class="sxs-lookup"><span data-stu-id="99214-110">Right click on the *Movies.mdf* file and select **Delete** to remove the movies database.</span></span> <span data-ttu-id="99214-111">표시 되지 않으면는 *Movies.mdf* 파일, 클릭는 **모든 파일 표시** 빨간색 윤곽선에서 아래 표시 된 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="99214-111">If you don't see the *Movies.mdf* file, click on the **Show All Files** icon shown below in the red outline.</span></span>

![](adding-a-new-field/_static/image1.png)

<span data-ttu-id="99214-112">오류가 없는 되도록 응용 프로그램을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="99214-112">Build the application to make sure there are no errors.</span></span>

<span data-ttu-id="99214-113">**도구** 메뉴를 클릭 하 여 **NuGet 패키지 관리자** 차례로 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-113">From the **Tools** menu, click **NuGet Package Manager** and then **Package Manager Console**.</span></span>

![팩 매뉴얼 추가](adding-a-new-field/_static/image2.png)

<span data-ttu-id="99214-115">에 **패키지 관리자 콘솔** 창에는 `PM>` 입력 프롬프트</span><span class="sxs-lookup"><span data-stu-id="99214-115">In the **Package Manager Console** window at the `PM>` prompt enter</span></span>

<span data-ttu-id="99214-116">Enable-migrations-ContextTypeName MvcMovie.Models.MovieDBContext</span><span class="sxs-lookup"><span data-stu-id="99214-116">Enable-Migrations -ContextTypeName MvcMovie.Models.MovieDBContext</span></span>

![](adding-a-new-field/_static/image3.png)

<span data-ttu-id="99214-117">**Enable-migrations** 명령은 (위에 표시)을 만듭니다는 *Configuration.cs* 를 새로운 파일 *마이그레이션* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="99214-117">The **Enable-Migrations** command (shown above) creates a *Configuration.cs* file in a new *Migrations* folder.</span></span>

![](adding-a-new-field/_static/image4.png)

<span data-ttu-id="99214-118">Visual Studio가 열릴는 *Configuration.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="99214-118">Visual Studio opens the *Configuration.cs* file.</span></span> <span data-ttu-id="99214-119">대체는 `Seed` 에서 메서드는 *Configuration.cs* 를 다음 코드로 파일:</span><span class="sxs-lookup"><span data-stu-id="99214-119">Replace the `Seed` method in the *Configuration.cs* file with the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

<span data-ttu-id="99214-120">빨간색의 구불구불한 선이 아래에서 위로 마우스를 가져가고 `Movie` 클릭 `Show Potential Fixes` 클릭 하 고 **를 사용 하 여** **MvcMovie.Models;**</span><span class="sxs-lookup"><span data-stu-id="99214-120">Hover over the red squiggly line under `Movie` and click `Show Potential Fixes` and then click **using** **MvcMovie.Models;**</span></span>

![](adding-a-new-field/_static/image5.png)

<span data-ttu-id="99214-121">이렇게 하면 추가 되므로 다음 문을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="99214-121">Doing so adds the following using statement:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

> [!NOTE] 
> 
> <span data-ttu-id="99214-122">First 마이그레이션이 호출 코드의 `Seed` 모든 마이그레이션 후 메서드 (즉, 호출 **데이터베이스 업데이트** 패키지 관리자 콘솔에서),이 메서드는 이미 삽입 되었거나 경우 삽입 된 행을 업데이트 하 고 있습니다 아직 존재 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="99214-122">Code First Migrations calls the `Seed` method after every migration (that is, calling **update-database** in the Package Manager Console), and this method updates rows that have already been inserted, or inserts them if they don't exist yet.</span></span>
> 
> <span data-ttu-id="99214-123">[AddOrUpdate](https://msdn.microsoft.com/en-us/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 다음 코드에서 메서드는 "upsert" 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-123">The [AddOrUpdate](https://msdn.microsoft.com/en-us/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) method in the following code performs an "upsert" operation:</span></span>
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample3.cs)]
> 
> <span data-ttu-id="99214-124">때문에 [시드](https://msdn.microsoft.com/en-us/library/hh829453(v=vs.103).aspx) 모든 마이그레이션을 사용 하 여 메서드 실행, 때문에 추가 하려고 하는 행 이미 있는 데이터베이스를 만드는 첫 번째 마이그레이션 후에 데이터를 삽입할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="99214-124">Because the [Seed](https://msdn.microsoft.com/en-us/library/hh829453(v=vs.103).aspx) method runs with every migration, you can't just insert data, because the rows you are trying to add will already be there after the first migration that creates the database.</span></span> <span data-ttu-id="99214-125">"[upsert](http://en.wikipedia.org/wiki/Upsert)" 작업이 이미 존재 하는 행을 삽입 하려고 할 경우 수행 하는 오류를 방지할 수 있지만 응용 프로그램을 테스트 하는 동안 실행 한 데이터 변경 내용 보다 우선 합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-125">The "[upsert](http://en.wikipedia.org/wiki/Upsert)" operation prevents errors that would happen if you try to insert a row that already exists, but it overrides any changes to data that you may have made while testing the application.</span></span> <span data-ttu-id="99214-126">테스트 테이블의에서 데이터 일부 원하지 않을 수 있습니다이 위해서는: 경우에 따라 테스트 하는 동안 데이터를 변경 하면 원하는 변경 내용을 데이터베이스 업데이트 후 하 게 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-126">With test data in some tables you might not want that to happen: in some cases when you change data while testing you want your changes to remain after database updates.</span></span> <span data-ttu-id="99214-127">조건부 삽입 작업을 수행 하려는 경우: 존재 하지 않는 경우에 행을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-127">In that case you want to do a conditional insert operation: insert a row only if it doesn't already exist.</span></span>   
>   
> <span data-ttu-id="99214-128">에 전달 된 첫 번째 매개 변수는 [AddOrUpdate](https://msdn.microsoft.com/en-us/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 메서드 행 이미 존재 하는지 확인 하는 데 속성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-128">The first parameter passed to the [AddOrUpdate](https://msdn.microsoft.com/en-us/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) method specifies the property to use to check if a row already exists.</span></span> <span data-ttu-id="99214-129">제공 하는 테스트 동영상 데이터에는 `Title` 속성 각 타이틀 목록에는 고유 하므로이 용도로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99214-129">For the test movie data that you are providing, the `Title` property can be used for this purpose since each title in the list is unique:</span></span>
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample4.cs)]
> 
> <span data-ttu-id="99214-130">이 코드에서는 titiles는 고유한 것을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-130">This code assumes that titiles are unique.</span></span> <span data-ttu-id="99214-131">중복 된 제목에 수동으로 추가한 경우에 마이그레이션을 수행 하는 다음에 다음과 같은 예외를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99214-131">If you manually add a duplicate title, you'll get the following exception the next time you perform a migration.</span></span>   
>   
>  <span data-ttu-id="99214-132">*시퀀스에 요소가 둘 이상*</span><span class="sxs-lookup"><span data-stu-id="99214-132">*Sequence contains more than one element*</span></span>  
>   
> <span data-ttu-id="99214-133">에 대 한 자세한 내용은 [AddOrUpdate](https://msdn.microsoft.com/en-us/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) 메서드를 참조 [EF 4.3 AddOrUpdate 메서드로 주의](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)...</span><span class="sxs-lookup"><span data-stu-id="99214-133">For more information about the [AddOrUpdate](https://msdn.microsoft.com/en-us/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) method, see [Take care with EF 4.3 AddOrUpdate Method](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)..</span></span>


<span data-ttu-id="99214-134">**CTRL-SHIFT-B를 눌러 프로젝트를 빌드합니다.** (다음 단계 못합니다이 시점에서 작성 하지 않아도 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="99214-134">**Press CTRL-SHIFT-B to build the project.**(The following steps will fail if you don't build at this point.)</span></span>

<span data-ttu-id="99214-135">다음 단계를 만드는 것을 `DbMigration` 초기 마이그레이션에 대 한 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="99214-135">The next step is to create a `DbMigration` class for the initial migration.</span></span> <span data-ttu-id="99214-136">이 마이그레이션은 만듭니다 바로 이러한 이유로 하는 새 데이터베이스를 삭제 하면는 *movie.mdf* 파일을 이전 단계에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-136">This migration creates a new database, that's why you deleted the *movie.mdf* file in a previous step.</span></span>

<span data-ttu-id="99214-137">에 **패키지 관리자 콘솔** 창에서 명령을 입력 `add-migration Initial` 초기 마이그레이션 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-137">In the **Package Manager Console** window, enter the command `add-migration Initial` to create the initial migration.</span></span> <span data-ttu-id="99214-138">이름은 "초기"는 임의로 지정 하며 만든 마이그레이션 파일 이름을 지정 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="99214-138">The name "Initial" is arbitrary and is used to name the migration file created.</span></span>

![](adding-a-new-field/_static/image6.png)

<span data-ttu-id="99214-139">Code First 마이그레이션을에 다른 클래스 파일을 만듭니다는 *마이그레이션* 폴더 (이름의 *{날짜 스탬프}\_Initial.cs* ),이 클래스는 데이터베이스 스키마를 만드는 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-139">Code First Migrations creates another class file in the *Migrations* folder (with the name *{DateStamp}\_Initial.cs* ), and this class contains code that creates the database schema.</span></span> <span data-ttu-id="99214-140">마이그레이션 filename 미리 타임 스탬프가 순서 지정에 도움이 되도록 고정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="99214-140">The migration filename is pre-fixed with a timestamp to help with ordering.</span></span> <span data-ttu-id="99214-141">검사는 *{날짜 스탬프}\_Initial.cs* 파일을 만드는 지침이 포함 된 `Movies` 영화 DB에 대 한 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="99214-141">Examine the *{DateStamp}\_Initial.cs* file, it contains the instructions to create the `Movies` table for the Movie DB.</span></span> <span data-ttu-id="99214-142">이 아래 지침에 설명 된 데이터베이스를 업데이트 하는 경우 *{날짜 스탬프}\_Initial.cs* 파일은 실행 된 후 DB 스키마를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="99214-142">When you update the database in the instructions below, this *{DateStamp}\_Initial.cs* file will run and create the DB schema.</span></span> <span data-ttu-id="99214-143">그런 다음 **시드** DB 테스트 데이터로 채우는 메서드가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="99214-143">Then the **Seed** method will run to populate the DB with test data.</span></span>

<span data-ttu-id="99214-144">에 **패키지 관리자 콘솔**, 명령을 입력 `update-database` 데이터베이스를 만들고 실행 하는 `Seed` 메서드.</span><span class="sxs-lookup"><span data-stu-id="99214-144">In the **Package Manager Console**, enter the command `update-database` to create the database and run the `Seed` method.</span></span>

![](adding-a-new-field/_static/image7.png)

<span data-ttu-id="99214-145">테이블이 이미 존재 하며 만들 수를 나타내는 오류가 발생할 경우 때문일 것 데이터베이스 삭제 되 고 실행 하기 전에 응용 프로그램을 실행 `update-database`합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-145">If you get an error that indicates a table already exists and can't be created, it is probably because you ran the application after you deleted the database and before you executed `update-database`.</span></span> <span data-ttu-id="99214-146">이 경우 삭제 된 *Movies.mdf* 파일을 다시 시도 `update-database` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="99214-146">In that case, delete the *Movies.mdf* file again and retry the `update-database` command.</span></span> <span data-ttu-id="99214-147">오류가 여전히 발생 하면 migrations 폴더 및 내용을 삭제 한 다음이 페이지의 위쪽에 대 한 지침이 포함 된 시작 (삭제 되 고 *Movies.mdf* 파일 Enable-migrations를 진행 합니다).</span><span class="sxs-lookup"><span data-stu-id="99214-147">If you still get an error, delete the migrations folder and contents then start with the instructions at the top of this page (that is delete the *Movies.mdf* file then proceed to Enable-Migrations).</span></span> <span data-ttu-id="99214-148">함을 여전히 발생 하면 SQL Server 개체 탐색기를 열고 목록에서 데이터베이스를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-148">If you still get an eror, open SQL Server Object Explorer and remove the database from the list.</span></span>

<span data-ttu-id="99214-149">응용 프로그램을 실행 하 고 탐색 하 고 */Movies* URL입니다.</span><span class="sxs-lookup"><span data-stu-id="99214-149">Run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="99214-150">시드 데이터가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="99214-150">The seed data is displayed.</span></span>

![](adding-a-new-field/_static/image8.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="99214-151">영화 모델에 등급 속성 추가</span><span class="sxs-lookup"><span data-stu-id="99214-151">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="99214-152">추가 하 여 시작 `Rating` 속성을 기존 `Movie` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="99214-152">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="99214-153">열기는 *Models\Movie.cs* 파일을 추가 `Rating` 다음과 같은 속성:</span><span class="sxs-lookup"><span data-stu-id="99214-153">Open the *Models\Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

<span data-ttu-id="99214-154">전체 `Movie` 다음 코드 처럼 이제 보이는 클래스:</span><span class="sxs-lookup"><span data-stu-id="99214-154">The complete `Movie` class now looks like the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs?highlight=12)]

<span data-ttu-id="99214-155">(Ctrl + Shift + B) 응용 프로그램을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="99214-155">Build the application (Ctrl+Shift+B).</span></span>

<span data-ttu-id="99214-156">새 필드를 추가 했으므로 때문에 `Movie` 클래스도 업데이트 해야 바인딩 *허용 목록을* 하므로이 새로운 속성이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="99214-156">Because you've added a new field to the `Movie` class, you also need to update the binding *white list* so this new property will be included.</span></span> <span data-ttu-id="99214-157">업데이트는 `bind` 특성 `Create` 및 `Edit` 포함 하도록 동작 메서드는 `Rating` 속성:</span><span class="sxs-lookup"><span data-stu-id="99214-157">Update the `bind` attribute for `Create` and `Edit` action methods to include the `Rating` property:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs?highlight=1)]

<span data-ttu-id="99214-158">브라우저 보기에서 새 `Rating` 속성을 표시, 작성 및 편집하기 위해 보기 템플릿도 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-158">You also need to update the view templates in order to display, create and edit the new `Rating` property in the browser view.</span></span>

<span data-ttu-id="99214-159">열기는 *\Views\Movies\Index.cshtml* 파일을 추가 `<th>Rating</th>` 열 머리글 바로 뒤의 **가격** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="99214-159">Open the *\Views\Movies\Index.cshtml* file and add a `<th>Rating</th>` column heading just after the **Price** column.</span></span> <span data-ttu-id="99214-160">다음 추가 `<td>` 열을 렌더링 하는 서식 파일의 끝 부분에서 `@item.Rating` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="99214-160">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="99214-161">다음은 이러한 어떤 업데이트 된 *Index.cshtml* 보기 템플릿은 보입니다.</span><span class="sxs-lookup"><span data-stu-id="99214-161">Below is what the updated *Index.cshtml* view template looks like:</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample8.cshtml?highlight=31-33,52-54)]

<span data-ttu-id="99214-162">을 열고는 *\Views\Movies\Create.cshtml* 파일을 추가 `Rating` 다음 highlighed 태그로 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="99214-162">Next, open the *\Views\Movies\Create.cshtml* file and add the `Rating` field with the following highlighed markup.</span></span> <span data-ttu-id="99214-163">이 렌더링 하는 텍스트 상자가 새 동영상 만들어질 때에 대 한 등급을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99214-163">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample9.cshtml?highlight=9-15)]

<span data-ttu-id="99214-164">새 지원 하기 위해 응용 프로그램 코드를 지금 업데이트 한 `Rating` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="99214-164">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="99214-165">응용 프로그램을 실행 하 고 탐색 하 고 */Movies* URL입니다.</span><span class="sxs-lookup"><span data-stu-id="99214-165">Run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="99214-166">이 작업을 수행 하지만 표시 다음 오류 중 하나:</span><span class="sxs-lookup"><span data-stu-id="99214-166">When you do this, though, you'll see one of the following errors:</span></span>

![](adding-a-new-field/_static/image9.png)  
  
<span data-ttu-id="99214-167">'MovieDBContext' 컨텍스트를 백업 하는 모델 데이터베이스를 만든 후에 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="99214-167">The model backing the 'MovieDBContext' context has changed since the database was created.</span></span> <span data-ttu-id="99214-168">Code First 마이그레이션을 사용 하 여 (https://go.microsoft.com/fwlink/?LinkId=238269) 데이터베이스를 업데이트 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="99214-168">Consider using Code First Migrations to update the database (https://go.microsoft.com/fwlink/?LinkId=238269).</span></span>

![](adding-a-new-field/_static/image10.png)

<span data-ttu-id="99214-169">때문에이 오류를 표시 하는 업데이트 된 `Movie` 응용 프로그램에서 모델 클래스의 스키마와 다르면 이제는 `Movie` 기존 데이터베이스의 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="99214-169">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="99214-170">(데이터베이스 테이블에 `Rating` 열이 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="99214-170">(There's no `Rating` column in the database table.)</span></span>


<span data-ttu-id="99214-171">오류를 해결하는 몇 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99214-171">There are a few approaches to resolving the error:</span></span>

1. <span data-ttu-id="99214-172">Entity Framework에서 새 모델 클래스 스키마에 따라 데이터베이스를 자동으로 삭제하고 다시 만들도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-172">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="99214-173">이 방법은 테스트 데이터베이스에서 활발한 개발을 수행할 때 개발 주기의 초기 단계에서 매우 편리하며 신속하게 모델 및 데이터베이스 스키마를 함께 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99214-173">This approach is very convenient early in the development cycle when you are doing active development on a test database; it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="99214-174">데이터베이스의 기존 데이터 손실의 단점은 하지만입니다-하므로 있습니다 *하지 않는* 는 프로덕션 데이터베이스에서이 방법을 사용!</span><span class="sxs-lookup"><span data-stu-id="99214-174">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span> <span data-ttu-id="99214-175">응용 프로그램을 개발 하는 효율적인 방법으로 방식은를 자동으로 테스트 데이터로 데이터베이스를 시드하는 이니셜라이저를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-175">Using an initializer to automatically seed a database with test data is often a productive way to develope an application.</span></span> <span data-ttu-id="99214-176">Entity Framework 데이터베이스 이니셜라이저에 대 한 자세한 내용은 참조 하십시오. [ASP.NET MVC/엔터티 프레임 워크 자습서](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-176">For more information on Entity Framework database initializers, see [ASP.NET MVC/Entity Framework tutorial](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>
2. <span data-ttu-id="99214-177">모델 클래스와 일치하도록 기존 데이터베이스의 스키마를 명시적으로 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-177">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="99214-178">이 방법의 장점은 데이터를 유지한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="99214-178">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="99214-179">이러한 변경을 수동으로 수행하거나 데이터베이스 변경 스크립트를 만들어 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99214-179">You can make this change either manually or by creating a database change script.</span></span>
3. <span data-ttu-id="99214-180">Code First 마이그레이션을 사용하여 데이터베이스 스키마를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-180">Use Code First Migrations to update the database schema.</span></span>


<span data-ttu-id="99214-181">이 자습서의 경우 Code First 마이그레이션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-181">For this tutorial, we'll use Code First Migrations.</span></span>

<span data-ttu-id="99214-182">Seed 메서드를 업데이트 하는 새 열에 대 한 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-182">Update the Seed method so that it provides a value for the new column.</span></span> <span data-ttu-id="99214-183">Migrations\Configuration.cs 파일을 열고 각 영화 개체에 Rating 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-183">Open Migrations\Configuration.cs file and add a Rating field to each Movie object.</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample10.cs?highlight=6)]

<span data-ttu-id="99214-184">솔루션을 작성 한 다음 엽니다는 **패키지 관리자 콘솔** 창 하 고 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-184">Build the solution, and then open the **Package Manager Console** window and enter the following command:</span></span>

`add-migration Rating`

<span data-ttu-id="99214-185">`add-migration` 명령 마이그레이션 프레임 워크에 현재 영화 DB 스키마와 현재 영화 모델을 점검 하 여 DB 새 모델을 마이그레이션하는 데 필요한 코드를 만들 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-185">The `add-migration` command tells the migration framework to examine the current movie model with the current movie DB schema and create the necessary code to migrate the DB to the new model.</span></span> <span data-ttu-id="99214-186">이름을 *등급* 은 임의로 지정 하 고 마이그레이션 파일 이름을 지정 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="99214-186">The name *Rating* is arbitrary and is used to name the migration file.</span></span> <span data-ttu-id="99214-187">마이그레이션 단계에 대 한 의미 있는 이름을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="99214-187">It's helpful to use a meaningful name for the migration step.</span></span>

<span data-ttu-id="99214-188">Visual Studio 새 정의 하는 클래스 파일을 엽니다이 명령이 완료 되 면 `DbMigration` 파생 클래스를 및는 `Up` 메서드 새 열을 만드는 코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99214-188">When this command finishes, Visual Studio opens the class file that defines the new `DbMigration` derived class, and in the `Up` method you can see the code that creates the new column.</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample11.cs)]

<span data-ttu-id="99214-189">솔루션을 작성 한 다음 입력 된 `update-database` 명령에 **패키지 관리자 콘솔** 창.</span><span class="sxs-lookup"><span data-stu-id="99214-189">Build the solution, and then enter the `update-database` command in the **Package Manager Console** window.</span></span>

<span data-ttu-id="99214-190">다음 이미지는 출력에 표시는 **패키지 관리자 콘솔** 창 (날짜 스탬프 앞 *등급* 다릅니다.)</span><span class="sxs-lookup"><span data-stu-id="99214-190">The following image shows the output in the **Package Manager Console** window (The date stamp prepending *Rating* will be different.)</span></span>

![](adding-a-new-field/_static/image11.png)

<span data-ttu-id="99214-191">응용 프로그램을 다시 실행 하 고 /Movies URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-191">Re-run the application and navigate to the /Movies URL.</span></span> <span data-ttu-id="99214-192">새 등급 필드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99214-192">You can see the new Rating field.</span></span>

![](adding-a-new-field/_static/image12.png)

<span data-ttu-id="99214-193">클릭는 **새로 만들기** 새 동영상을 추가 하는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="99214-193">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="99214-194">참고에 대 한 등급을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99214-194">Note that you can add a rating.</span></span>

![7_CreateRioII](adding-a-new-field/_static/image13.png)

<span data-ttu-id="99214-196">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-196">Click **Create**.</span></span> <span data-ttu-id="99214-197">등급을 포함 하 여 새 동영상은 이제 나열 영화에서 표시:</span><span class="sxs-lookup"><span data-stu-id="99214-197">The new movie, including the rating, now shows up in the movies listing:</span></span>

![7_ourNewMovie_SM](adding-a-new-field/_static/image14.png)

<span data-ttu-id="99214-199">이제 프로젝트 마이그레이션을 사용 하는 새 필드를 추가 하거나 그렇지 않으면 스키마를 업데이트할 때 데이터베이스를 삭제할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="99214-199">Now that the project is using migrations, you won't need to drop the database when you add a new field or otherwise update the schema.</span></span> <span data-ttu-id="99214-200">다음 섹션에서 더 많은 스키마 변경을 알아보고 마이그레이션을 사용 하 여 데이터베이스를 업데이트 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="99214-200">In the next section, we'll make more schema changes and use migrations to update the database.</span></span>

<span data-ttu-id="99214-201">도 추가 해야는 `Rating` 필드 템플릿 보기 편집, 정보 및 삭제를 합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-201">You should also add the `Rating` field to the Edit, Details, and Delete view templates.</span></span>

<span data-ttu-id="99214-202">"update-database" 명령을 입력할 수는 **패키지 관리자 콘솔** 창을 다시 및 마이그레이션 코드가 없는 실행 스키마 모델 일치 하기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99214-202">You could enter the "update-database" command in the **Package Manager Console** window again and no migration code would run, because the schema matches the model.</span></span> <span data-ttu-id="99214-203">그러나 실행 됩니다 "데이터베이스 업데이트"를 실행 중인는 `Seed` 메서드를 다시, 초기값에 데이터를 변경한 경우 변경 내용이 손실 됩니다 때문에 `Seed` 메서드 upserts 데이터.</span><span class="sxs-lookup"><span data-stu-id="99214-203">However, running "update-database" will run the `Seed` method again, and if you changed any of the Seed data, the changes will be lost because the `Seed` method upserts data.</span></span> <span data-ttu-id="99214-204">에 대 한 자세한 내용은 `Seed` 인기 있는 Tom Dykstra에서 메서드 [ASP.NET MVC/엔터티 프레임 워크 자습서](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-204">You can read more about the `Seed` method in Tom Dykstra's popular [ASP.NET MVC/Entity Framework tutorial](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

<span data-ttu-id="99214-205">이 섹션에서는 모델 개체를 수정할 데이터베이스의 변경 내용과 동기화 된 상태로 유지 하는 방법을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-205">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="99214-206">또한 시나리오를 체험할 수 있도록 샘플 데이터로 새로 만든된 데이터베이스를 채우는 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="99214-206">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="99214-207">이 한 간단한 소개 Code First를 참조 하십시오. [ASP.NET MVC 응용 프로그램에 대 한 Entity Framework 데이터 모델을 만드는](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) 주체에 대 한 자세한 자습서에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="99214-207">This was just a quick introduction to Code First, see [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) for a more complete tutorial on the subject.</span></span> <span data-ttu-id="99214-208">다음으로, 다양 한 유효성 검사 논리 모델 클래스를 추가 적용 해야 할 몇 가지 비즈니스 규칙을 사용 하도록 설정 하는 방법에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="99214-208">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="99214-209">[이전](adding-search.md)
[다음](adding-validation.md)</span><span class="sxs-lookup"><span data-stu-id="99214-209">[Previous](adding-search.md)
[Next](adding-validation.md)</span></span>
