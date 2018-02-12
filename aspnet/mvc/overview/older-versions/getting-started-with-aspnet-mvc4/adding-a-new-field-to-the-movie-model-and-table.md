---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
title: "영화 모델 및 테이블에 새 필드 추가 | Microsoft Docs"
author: Rick-Anderson
description: "참고:이 자습서의 업데이트 된 버전은 ASP.NET MVC 5 및 Visual Studio 2013을 사용 하는 있습니다. 것이 더 안전 하 고 진행할 데모를 단순..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/28/2012
ms.topic: article
ms.assetid: 9ef2c4f1-a305-4e0a-9fb8-bfbd9ef331d9
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
msc.type: authoredcontent
ms.openlocfilehash: 9965c8a755857a8e8cb8ecbc6c467a6c856aa83d
ms.sourcegitcommit: b83a5f731a9c02bdb1cc1e3f9a8bf273eb5b33e0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2018
---
<a name="adding-a-new-field-to-the-movie-model-and-table"></a><span data-ttu-id="4263f-104">영화 모델 및 테이블에 새 필드 추가</span><span class="sxs-lookup"><span data-stu-id="4263f-104">Adding a New Field to the Movie Model and Table</span></span>
====================
<span data-ttu-id="4263f-105">으로 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="4263f-105">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> > [!NOTE]
> > <span data-ttu-id="4263f-106">이 자습서의 업데이트 된 버전은 사용할 수 있는 [여기](../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 및 Visual Studio 2013을 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="4263f-107">더 안전 하 고 따라 하기 쉽고 이며 더 많은 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>


<span data-ttu-id="4263f-108">이 섹션에서는 변경 내용이 데이터베이스에 적용 되므로 일부 변경 내용이 모델 클래스 마이그레이션할 Entity Framework Code First 마이그레이션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-108">In this section you'll use Entity Framework Code First Migrations to migrate some changes to the model classes so the change is applied to the database.</span></span>

<span data-ttu-id="4263f-109">기본적으로를 사용 하 여 Entity Framework Code First 자동으로 데이터베이스를 만들려면이 자습서의 앞부분에서 마찬가지로 코드 첫 번째 테이블에 추가 데이터베이스는 데이터베이스의 스키마에서 생성 된 모델 클래스 동기화 되어 있는지 여부를 추적 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-109">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="4263f-110">동기화 하지 않을 경우 Entity Framework에서 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-110">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="4263f-111">이렇게 하면 그렇지 않으면만 찾을 수 (모호한 오류)에 의해 런타임 시 개발 시 문제를 추적 하기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-111">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span>

## <a name="setting-up-code-first-migrations-for-model-changes"></a><span data-ttu-id="4263f-112">Code First 마이그레이션을 모델 변경 내용에 대 한 설정</span><span class="sxs-lookup"><span data-stu-id="4263f-112">Setting up Code First Migrations for Model Changes</span></span>

<span data-ttu-id="4263f-113">Visual Studio 2012를 사용 하는 경우 두 번 클릭은 *Movies.mdf* 데이터베이스 도구를 열려면 솔루션 탐색기에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-113">If you are using Visual Studio 2012, double click the *Movies.mdf* file from Solution Explorer to open the database tool.</span></span> <span data-ttu-id="4263f-114">Visual Studio Express for Web이 표시 됩니다 데이터베이스 탐색기 Visual Studio 2012 서버 탐색기에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-114">Visual Studio Express for Web will show Database Explorer, Visual Studio 2012 will show Server Explorer.</span></span> <span data-ttu-id="4263f-115">Visual Studio 2010을 사용 하는 경우 SQL Server 개체 탐색기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-115">If you are using Visual Studio 2010, use SQL Server Object Explorer.</span></span>

<span data-ttu-id="4263f-116">데이터베이스 도구 (데이터베이스 탐색기, 서버 탐색기 또는 SQL Server 개체 탐색기)에서 마우스 오른쪽 단추로 클릭 `MovieDBContext` 선택 **삭제** 영화 데이터베이스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-116">In the database tool (Database Explorer, Server Explorer or SQL Server Object Explorer), right click on `MovieDBContext` and select **Delete** to drop the movies database.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image1.png)

<span data-ttu-id="4263f-117">솔루션 탐색기로 다시 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-117">Navigate back to Solution Explorer.</span></span> <span data-ttu-id="4263f-118">마우스 오른쪽 단추로 클릭는 *Movies.mdf* 파일을 선택 **삭제** 영화 데이터베이스를 제거 하려면.</span><span class="sxs-lookup"><span data-stu-id="4263f-118">Right click on the *Movies.mdf* file and select **Delete** to remove the movies database.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image2.png)

<span data-ttu-id="4263f-119">오류가 없는 되도록 응용 프로그램을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="4263f-119">Build the application to make sure there are no errors.</span></span>

<span data-ttu-id="4263f-120">**도구** 메뉴를 클릭 하 여 **라이브러리 패키지 관리자** 차례로 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-120">From the **Tools** menu, click **Library Package Manager** and then **Package Manager Console**.</span></span>

![팩 매뉴얼 추가](adding-a-new-field-to-the-movie-model-and-table/_static/image3.png)

<span data-ttu-id="4263f-122">에 **패키지 관리자 콘솔** 창에는 `PM>` 프롬프트 "Enable-migrations-ContextTypeName MvcMovie.Models.MovieDBContext"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-122">In the **Package Manager Console** window at the `PM>` prompt enter "Enable-Migrations -ContextTypeName MvcMovie.Models.MovieDBContext".</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image4.png)

<span data-ttu-id="4263f-123">**Enable-migrations** 명령은 (위에 표시)을 만듭니다는 *Configuration.cs* 를 새로운 파일 *마이그레이션* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-123">The **Enable-Migrations** command (shown above) creates a *Configuration.cs* file in a new *Migrations* folder.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image5.png)

<span data-ttu-id="4263f-124">Visual Studio가 열릴는 *Configuration.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-124">Visual Studio opens the *Configuration.cs* file.</span></span> <span data-ttu-id="4263f-125">대체는 `Seed` 에서 메서드는 *Configuration.cs* 를 다음 코드로 파일:</span><span class="sxs-lookup"><span data-stu-id="4263f-125">Replace the `Seed` method in the *Configuration.cs* file with the following code:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample1.cs)]

<span data-ttu-id="4263f-126">아래의 빨간색 물결선을 마우스 오른쪽 단추로 클릭 `Movie` 선택 **해결** 다음 **를 사용 하 여** **MvcMovie.Models;**</span><span class="sxs-lookup"><span data-stu-id="4263f-126">Right click on the red squiggly line under `Movie` and select **Resolve** then **using** **MvcMovie.Models;**</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image6.png)

<span data-ttu-id="4263f-127">이렇게 하면 추가 되므로 다음 문을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="4263f-127">Doing so adds the following using statement:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample2.cs)]

> [!NOTE] 
> 
> <span data-ttu-id="4263f-128">First 마이그레이션이 호출 코드의 `Seed` 모든 마이그레이션 후 메서드 (즉, 호출 **데이터베이스 업데이트** 패키지 관리자 콘솔에서),이 메서드는 이미 삽입 되었거나 경우 삽입 된 행을 업데이트 하 고 있습니다 아직 존재 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="4263f-128">Code First Migrations calls the `Seed` method after every migration (that is, calling **update-database** in the Package Manager Console), and this method updates rows that have already been inserted, or inserts them if they don't exist yet.</span></span>


<span data-ttu-id="4263f-129">**CTRL-SHIFT-B를 눌러 프로젝트를 빌드합니다.** (다음 단계는 경우 실패 합니다 프로그램이 시점에서 작성 하지 않아도 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="4263f-129">**Press CTRL-SHIFT-B to build the project.**(The following steps will fail if your don't build at this point.)</span></span>

<span data-ttu-id="4263f-130">다음 단계를 만드는 것을 `DbMigration` 초기 마이그레이션에 대 한 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-130">The next step is to create a `DbMigration` class for the initial migration.</span></span> <span data-ttu-id="4263f-131">이 마이그레이션에는 이유는 새 데이터베이스를 만듭니다 삭제 하는 *movie.mdf* 파일을 이전 단계에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-131">This migration to creates a new database, that's why you deleted the *movie.mdf* file in a previous step.</span></span>

<span data-ttu-id="4263f-132">에 **패키지 관리자 콘솔** 창에서 "추가 마이그레이션 초기" 명령을 입력 초기 마이그레이션 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-132">In the **Package Manager Console** window, enter the command "add-migration Initial" to create the initial migration.</span></span> <span data-ttu-id="4263f-133">이름은 "초기"는 임의로 지정 하며 만든 마이그레이션 파일 이름을 지정 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-133">The name "Initial" is arbitrary and is used to name the migration file created.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image7.png)

<span data-ttu-id="4263f-134">Code First 마이그레이션을에 다른 클래스 파일을 만듭니다는 *마이그레이션* 폴더 (이름의 *{날짜 스탬프}\_Initial.cs* ),이 클래스는 데이터베이스 스키마를 만드는 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-134">Code First Migrations creates another class file in the *Migrations* folder (with the name *{DateStamp}\_Initial.cs* ), and this class contains code that creates the database schema.</span></span> <span data-ttu-id="4263f-135">마이그레이션 filename 미리 타임 스탬프가 순서 지정에 도움이 되도록 고정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-135">The migration filename is pre-fixed with a timestamp to help with ordering.</span></span> <span data-ttu-id="4263f-136">검사는 *{날짜 스탬프}\_Initial.cs* 를 영화 DB에 대 한 동영상 테이블을 만드는 지침 포함 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-136">Examine the *{DateStamp}\_Initial.cs* file, it contains the instructions to create the Movies table for the Movie DB.</span></span> <span data-ttu-id="4263f-137">이 아래 지침에 설명 된 데이터베이스를 업데이트 하는 경우 *{날짜 스탬프}\_Initial.cs* 파일은 실행 된 후 DB 스키마를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-137">When you update the database in the instructions below, this *{DateStamp}\_Initial.cs* file will run and create the DB schema.</span></span> <span data-ttu-id="4263f-138">그런 다음 **시드** DB 테스트 데이터로 채우는 메서드가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-138">Then the **Seed** method will run to populate the DB with test data.</span></span>

<span data-ttu-id="4263f-139">에 **패키지 관리자 콘솔**, 명령 "업데이트-데이터베이스 입력" 데이터베이스를 만들고 실행 하는 **시드** 메서드.</span><span class="sxs-lookup"><span data-stu-id="4263f-139">In the **Package Manager Console**, enter the command "update-database" to create the database and run the **Seed** method.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image8.png)

<span data-ttu-id="4263f-140">테이블이 이미 존재 하며 만들 수를 나타내는 오류가 발생할 경우 때문일 것 데이터베이스 삭제 되 고 실행 하기 전에 응용 프로그램을 실행 `update-database`합니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-140">If you get an error that indicates a table already exists and can't be created, it is probably because you ran the application after you deleted the database and before you executed `update-database`.</span></span> <span data-ttu-id="4263f-141">이 경우 삭제 된 *Movies.mdf* 파일을 다시 시도 `update-database` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-141">In that case, delete the *Movies.mdf* file again and retry the `update-database` command.</span></span> <span data-ttu-id="4263f-142">오류가 여전히 발생 하면 migrations 폴더 및 내용을 삭제 한 다음이 페이지의 위쪽에 대 한 지침이 포함 된 시작 (삭제 되 고 *Movies.mdf* 파일 Enable-migrations를 진행 합니다).</span><span class="sxs-lookup"><span data-stu-id="4263f-142">If you still get an error, delete the migrations folder and contents then start with the instructions at the top of this page (that is delete the *Movies.mdf* file then proceed to Enable-Migrations).</span></span>

<span data-ttu-id="4263f-143">응용 프로그램을 실행 하 고 탐색 하 고 */Movies* URL입니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-143">Run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="4263f-144">시드 데이터가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-144">The seed data is displayed.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image9.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="4263f-145">영화 모델에 등급 속성 추가</span><span class="sxs-lookup"><span data-stu-id="4263f-145">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="4263f-146">추가 하 여 시작 `Rating` 속성을 기존 `Movie` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-146">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="4263f-147">열기는 *Models\Movie.cs* 파일을 추가 `Rating` 다음과 같은 속성:</span><span class="sxs-lookup"><span data-stu-id="4263f-147">Open the *Models\Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample3.cs)]

<span data-ttu-id="4263f-148">전체 `Movie` 다음 코드 처럼 이제 보이는 클래스:</span><span class="sxs-lookup"><span data-stu-id="4263f-148">The complete `Movie` class now looks like the following code:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample4.cs?highlight=8)]

<span data-ttu-id="4263f-149">사용 하 여 응용 프로그램 작성은 **빌드** &gt; **빌드 영화** 명령 또는 CTRL 시프트. 키를 눌러 메뉴</span><span class="sxs-lookup"><span data-stu-id="4263f-149">Build the application using the **Build** &gt;**Build Movie** menu command or by pressing CTRL-SHIFT-B.</span></span>

<span data-ttu-id="4263f-150">업데이트 한 했으므로 `Model` 클래스도 업데이트 해야는 *\Views\Movies\Index.cshtml* 및 *\Views\Movies\Create.cshtml* 새 표시하기위해템플릿을보려면`Rating`브라우저 보기에는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-150">Now that you've updated the `Model` class, you also need to update the *\Views\Movies\Index.cshtml* and *\Views\Movies\Create.cshtml* view templates in order to display the new `Rating` property in the browser view.</span></span>

<span data-ttu-id="4263f-151">열기는*\Views\Movies\Index.cshtml* 파일을 추가 `<th>Rating</th>` 열 머리글 바로 뒤의 **가격** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-151">Open the*\Views\Movies\Index.cshtml* file and add a `<th>Rating</th>` column heading just after the **Price** column.</span></span> <span data-ttu-id="4263f-152">다음 추가 `<td>` 열을 렌더링 하는 서식 파일의 끝 부분에서 `@item.Rating` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-152">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="4263f-153">다음은 이러한 어떤 업데이트 된 *Index.cshtml* 보기 템플릿은 보입니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-153">Below is what the updated *Index.cshtml* view template looks like:</span></span>

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample5.cshtml?highlight=26-28,46-48)]

<span data-ttu-id="4263f-154">을 열고는 *\Views\Movies\Create.cshtml* 파일을 폼의 끝 부분에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-154">Next, open the *\Views\Movies\Create.cshtml* file and add the following markup near the end of the form.</span></span> <span data-ttu-id="4263f-155">이 렌더링 하는 텍스트 상자가 새 동영상 만들어질 때에 대 한 등급을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-155">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample6.cshtml)]

<span data-ttu-id="4263f-156">새 지원 하기 위해 응용 프로그램 코드를 지금 업데이트 한 `Rating` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-156">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="4263f-157">이제 응용 프로그램을 실행 하 고 탐색 하 고 */Movies* URL입니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-157">Now run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="4263f-158">이 작업을 수행 하지만 표시 다음 오류 중 하나:</span><span class="sxs-lookup"><span data-stu-id="4263f-158">When you do this, though, you'll see one of the following errors:</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image10.png)

![](adding-a-new-field-to-the-movie-model-and-table/_static/image11.png)

<span data-ttu-id="4263f-159">때문에이 오류를 표시 하는 업데이트 된 `Movie` 응용 프로그램에서 모델 클래스의 스키마와 다르면 이제는 `Movie` 기존 데이터베이스의 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-159">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="4263f-160">(데이터베이스 테이블에 `Rating` 열이 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="4263f-160">(There's no `Rating` column in the database table.)</span></span>


<span data-ttu-id="4263f-161">오류를 해결하는 몇 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-161">There are a few approaches to resolving the error:</span></span>

1. <span data-ttu-id="4263f-162">Entity Framework에서 새 모델 클래스 스키마에 따라 데이터베이스를 자동으로 삭제하고 다시 만들도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-162">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="4263f-163">이 방법은 매우 편리 하 게 테스트 데이터베이스;에서 개발을 수행 하는 경우 신속 하 게 함께 모델 및 데이터베이스 스키마를 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-163">This approach is very convenient when doing active development on a test database; it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="4263f-164">데이터베이스의 기존 데이터 손실의 단점은 하지만입니다-하므로 있습니다 *하지 않는* 는 프로덕션 데이터베이스에서이 방법을 사용!</span><span class="sxs-lookup"><span data-stu-id="4263f-164">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span> <span data-ttu-id="4263f-165">응용 프로그램을 개발 하는 효율적인 방법으로 방식은를 자동으로 테스트 데이터로 데이터베이스를 시드하는 이니셜라이저를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-165">Using an initializer to automatically seed a database with test data is often a productive way to develope an application.</span></span> <span data-ttu-id="4263f-166">대 한 자세한 내용은 Entity Framework 데이터베이스 이니셜라이저를 Tom Dykstra 참조 [ASP.NET MVC/엔터티 프레임 워크 자습서](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-166">For more information on Entity Framework database initializers, see Tom Dykstra's [ASP.NET MVC/Entity Framework tutorial](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>
2. <span data-ttu-id="4263f-167">모델 클래스와 일치하도록 기존 데이터베이스의 스키마를 명시적으로 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-167">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="4263f-168">이 방법의 장점은 데이터를 유지한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-168">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="4263f-169">이러한 변경을 수동으로 수행하거나 데이터베이스 변경 스크립트를 만들어 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-169">You can make this change either manually or by creating a database change script.</span></span>
3. <span data-ttu-id="4263f-170">Code First 마이그레이션을 사용하여 데이터베이스 스키마를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-170">Use Code First Migrations to update the database schema.</span></span>


<span data-ttu-id="4263f-171">이 자습서의 경우 Code First 마이그레이션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-171">For this tutorial, we'll use Code First Migrations.</span></span>

<span data-ttu-id="4263f-172">Seed 메서드를 업데이트 하는 새 열에 대 한 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-172">Update the Seed method so that it provides a value for the new column.</span></span> <span data-ttu-id="4263f-173">Migrations\Configuration.cs 파일을 열고 각 영화 개체에 Rating 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-173">Open Migrations\Configuration.cs file and add a Rating field to each Movie object.</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample7.cs?highlight=6)]

<span data-ttu-id="4263f-174">솔루션을 작성 한 다음 엽니다는 **패키지 관리자 콘솔** 창 하 고 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-174">Build the solution, and then open the **Package Manager Console** window and enter the following command:</span></span>

`add-migration AddRatingMig`

<span data-ttu-id="4263f-175">`add-migration` 명령 마이그레이션 프레임 워크에 현재 영화 DB 스키마와 현재 영화 모델을 점검 하 여 DB 새 모델을 마이그레이션하는 데 필요한 코드를 만들 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-175">The `add-migration` command tells the migration framework to examine the current movie model with the current movie DB schema and create the necessary code to migrate the DB to the new model.</span></span> <span data-ttu-id="4263f-176">AddRatingMig 임의의 이며 마이그레이션 파일 이름을 지정 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-176">The AddRatingMig is arbitrary and is used to name the migration file.</span></span> <span data-ttu-id="4263f-177">마이그레이션 단계에 대 한 의미 있는 이름을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-177">It's helpful to use a meaningful name for the migration step.</span></span>

<span data-ttu-id="4263f-178">Visual Studio 새 정의 하는 클래스 파일을 엽니다이 명령이 완료 되 면 `DbMIgration` 파생 클래스를 및는 `Up` 메서드 새 열을 만드는 코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-178">When this command finishes, Visual Studio opens the class file that defines the new `DbMIgration` derived class, and in the `Up` method you can see the code that creates the new column.</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample8.cs)]

<span data-ttu-id="4263f-179">솔루션을 빌드한 다음에 "데이터베이스 업데이트" 명령을 입력 하 고 **패키지 관리자 콘솔** 창.</span><span class="sxs-lookup"><span data-stu-id="4263f-179">Build the solution, and then enter the "update-database" command in the **Package Manager Console** window.</span></span>

<span data-ttu-id="4263f-180">다음 이미지는 출력에 표시 된 **패키지 관리자 콘솔** 창 (AddRatingMig 앞에 추가 하는 날짜 스탬프를 것입니다.)</span><span class="sxs-lookup"><span data-stu-id="4263f-180">The following image shows the output in the **Package Manager Console** window (The date stamp prepending AddRatingMig will be different.)</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image12.png)

<span data-ttu-id="4263f-181">응용 프로그램을 다시 실행 하 고 /Movies URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-181">Re-run the application and navigate to the /Movies URL.</span></span> <span data-ttu-id="4263f-182">새 등급 필드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-182">You can see the new Rating field.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image13.png)

<span data-ttu-id="4263f-183">클릭는 **새로 만들기** 새 동영상을 추가 하는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-183">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="4263f-184">참고에 대 한 등급을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-184">Note that you can add a rating.</span></span>

![7_CreateRioII](adding-a-new-field-to-the-movie-model-and-table/_static/image14.png)

<span data-ttu-id="4263f-186">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-186">Click **Create**.</span></span> <span data-ttu-id="4263f-187">등급을 포함 하 여 새 동영상은 이제 나열 영화에서 표시:</span><span class="sxs-lookup"><span data-stu-id="4263f-187">The new movie, including the rating, now shows up in the movies listing:</span></span>

![7_ourNewMovie_SM](adding-a-new-field-to-the-movie-model-and-table/_static/image15.png)

<span data-ttu-id="4263f-189">도 추가 해야는 `Rating` 필드 편집, 세부 정보 및 SearchIndex 보기 템플릿.</span><span class="sxs-lookup"><span data-stu-id="4263f-189">You should also add the `Rating` field to the Edit, Details and SearchIndex view templates.</span></span>

<span data-ttu-id="4263f-190">"update-database" 명령을 입력할 수는 **패키지 관리자 콘솔** 창을 다시 하 고 변경 내용을 적용 될, 스키마 모델 일치 하기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-190">You could enter the "update-database" command in the **Package Manager Console** window again and no changes would be made, because the schema matches the model.</span></span>

<span data-ttu-id="4263f-191">이 섹션에서는 모델 개체를 수정할 데이터베이스의 변경 내용과 동기화 된 상태로 유지 하는 방법을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-191">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="4263f-192">또한 시나리오를 체험할 수 있도록 샘플 데이터로 새로 만든된 데이터베이스를 채우는 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-192">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="4263f-193">다음으로, 다양 한 유효성 검사 논리 모델 클래스를 추가 적용 해야 할 몇 가지 비즈니스 규칙을 사용 하도록 설정 하는 방법에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4263f-193">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="4263f-194">[이전](examining-the-edit-methods-and-edit-view.md)
[다음](adding-validation-to-the-model.md)</span><span class="sxs-lookup"><span data-stu-id="4263f-194">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-validation-to-the-model.md)</span></span>
