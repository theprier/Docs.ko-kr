---
title: ASP.NET Core MVC 앱에 모델 추가
author: rick-anderson
description: 간단한 ASP.NET Core 앱에 모델을 추가합니다.
ms.author: riande
ms.date: 12/8/2017
uid: tutorials/first-mvc-app/adding-model
ms.openlocfilehash: 062a248ffdf8e30ed01a72e0a555c1c9a1ab1b6d
ms.sourcegitcommit: 42a8164b8aba21f322ffefacb92301bdfb4d3c2d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54341614"
---
# <a name="add-a-model-to-an-aspnet-core-mvc-app"></a><span data-ttu-id="978f3-103">ASP.NET Core MVC 앱에 모델 추가</span><span class="sxs-lookup"><span data-stu-id="978f3-103">Add a model to an ASP.NET Core MVC app</span></span>

<span data-ttu-id="978f3-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="978f3-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="978f3-105">이 섹션에서는 데이터베이스에서 동영상을 관리하기 위한 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-105">In this section, you add classes for managing movies in a database.</span></span> <span data-ttu-id="978f3-106">이러한 클래스는 **M**VC 앱의 "**M**odel" 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-106">These classes will be the "**M**odel" part of the **M**VC app.</span></span>

<span data-ttu-id="978f3-107">이러한 클래스를 EF Core([Entity Framework Core](/ef/core))와 함께 사용하여 데이터베이스 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-107">You use these classes with [Entity Framework Core](/ef/core) (EF Core) to work with a database.</span></span> <span data-ttu-id="978f3-108">EF Core는 작성해야 하는 데이터 액세스 코드를 간소화하는 ORM(개체-관계형 매핑) 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-108">EF Core is an object-relational mapping (ORM) framework that simplifies the data access code that you have to write.</span></span>

<span data-ttu-id="978f3-109">직접 만드는 모델 클래스는 EF Core에 대한 종속성이 없으므로 POCO(**P**lain **O**ld **C**LR **O**bject) 클래스로 알려져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-109">The model classes you create are known as POCO classes (from **P**lain **O**ld **C**LR **O**bjects) because they don't have any dependency on EF Core.</span></span> <span data-ttu-id="978f3-110">이 클래스는 데이터베이스에 저장되는 데이터의 속성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-110">They just define the properties of the data that will be stored in the database.</span></span>

<span data-ttu-id="978f3-111">이 자습서에서는 먼저 모델 클래스를 작성하면 EF Core가 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-111">In this tutorial, you write the model classes first, and EF Core creates the database.</span></span> <span data-ttu-id="978f3-112">이 문서에서 설명하지 않는 대체 방법은 기존 데이터베이스에서 모델 클래스를 생성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-112">An alternate approach not covered here is to generate model classes from an existing database.</span></span> <span data-ttu-id="978f3-113">이 방법에 대한 정보는 [ASP.NET Core - 기존 데이터베이스](/ef/core/get-started/aspnetcore/existing-db)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="978f3-113">For information about that approach, see [ASP.NET Core - Existing Database](/ef/core/get-started/aspnetcore/existing-db).</span></span>

## <a name="add-a-data-model-class"></a><span data-ttu-id="978f3-114">데이터 모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="978f3-114">Add a data model class</span></span>

<!-- VS -------------------------->
# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="978f3-115">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="978f3-115">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="978f3-116">*Models* 폴더> **추가** > **클래스**를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-116">Right-click the *Models* folder > **Add** > **Class**.</span></span> <span data-ttu-id="978f3-117">클래스의 이름을 **동영상**으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-117">Name the class **Movie**.</span></span>

[!INCLUDE [model 1b](~/includes/mvc-intro/model1b.md)]

<!-- Code -------------------------->
# <a name="visual-studio-code--visual-studio-for-mactabvisual-studio-codevisual-studio-mac"></a>[<span data-ttu-id="978f3-118">Visual Studio Code / Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="978f3-118">Visual Studio Code / Visual Studio for Mac</span></span>](#tab/visual-studio-code+visual-studio-mac)

* <span data-ttu-id="978f3-119">*Models* 폴더에 *Movie.cs* 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-119">Add a class to the *Models* folder named *Movie.cs*.</span></span>

[!INCLUDE [model 1b](~/includes/mvc-intro/model1b.md)]
[!INCLUDE [model 2](~/includes/mvc-intro/model2.md)]

---  
<!-- End of VS tabs -->

## <a name="scaffold-the-movie-model"></a><span data-ttu-id="978f3-120">동영상 모델 스캐폴드</span><span class="sxs-lookup"><span data-stu-id="978f3-120">Scaffold the movie model</span></span>

<span data-ttu-id="978f3-121">이 섹션에서는 동영상 모델을 스캐폴 합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-121">In this section, the movie model is scaffolded.</span></span> <span data-ttu-id="978f3-122">즉, 스캐폴드 도구는 동영상 모델에서 CRUD(만들기, 읽기, 업데이트 및 삭제) 작업을 위한 페이지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-122">That is, the scaffolding tool produces pages for Create, Read, Update, and Delete (CRUD) operations for the movie model.</span></span>

<!-- VS -------------------------->
# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="978f3-123">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="978f3-123">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="978f3-124">**솔루션 탐색기**에서 *Controllers* 폴더를 마우스 오른쪽 단추로 클릭하고 **> 추가 > 스캐폴드 항목 새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-124">In **Solution Explorer**, right-click the *Controllers* folder **> Add > New Scaffolded Item**.</span></span>

![위의 단계 보기](adding-model/_static/add_controller21.png)

<span data-ttu-id="978f3-126">**스캐폴드 추가** 대화 상자에서 **보기 포함 MVC 컨트롤러, Entity Framework > 추가 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-126">In the **Add Scaffold** dialog, select **MVC Controller with views, using Entity Framework > Add**.</span></span>

![스캐폴드 추가 대화 상자](adding-model/_static/add_scaffold21.png)

<span data-ttu-id="978f3-128">**컨트롤러 추가** 대화 상자를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-128">Complete the **Add Controller** dialog:</span></span>

* <span data-ttu-id="978f3-129">**모델 클래스:** *Movie(MvcMovie.Models)*</span><span class="sxs-lookup"><span data-stu-id="978f3-129">**Model class:** *Movie (MvcMovie.Models)*</span></span>
* <span data-ttu-id="978f3-130">**데이터 컨텍스트 클래스:** **+** 아이콘을 선택하고 기본값 **MvcMovie.Models.MvcMovieContext**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-130">**Data context class:** Select the **+** icon and add the default **MvcMovie.Models.MvcMovieContext**</span></span>

![데이터 컨텍스트 추가](adding-model/_static/dc.png)

* <span data-ttu-id="978f3-132">**보기:** 확인된 각 옵션의 기본값 선택 유지</span><span class="sxs-lookup"><span data-stu-id="978f3-132">**Views:** Keep the default of each option checked</span></span>
* <span data-ttu-id="978f3-133">**컨트롤러 이름:** 기본값 *MoviesController* 유지</span><span class="sxs-lookup"><span data-stu-id="978f3-133">**Controller name:** Keep the default *MoviesController*</span></span>
* <span data-ttu-id="978f3-134">**추가** 선택</span><span class="sxs-lookup"><span data-stu-id="978f3-134">Select **Add**</span></span>

![컨트롤러 추가 대화 상자](adding-model/_static/add_controller2.png)

<span data-ttu-id="978f3-136">Visual Studio에서 다음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-136">Visual Studio creates:</span></span>

* <span data-ttu-id="978f3-137">Entity Framework Core [데이터베이스 컨텍스트 클래스](xref:data/ef-mvc/intro#create-the-database-context)(*Data/MvcMovieContext.cs*)</span><span class="sxs-lookup"><span data-stu-id="978f3-137">An Entity Framework Core [database context class](xref:data/ef-mvc/intro#create-the-database-context) (*Data/MvcMovieContext.cs*)</span></span>
* <span data-ttu-id="978f3-138">동영상 컨트롤러(*Controllers/MoviesController.cs*)</span><span class="sxs-lookup"><span data-stu-id="978f3-138">A movies controller (*Controllers/MoviesController.cs*)</span></span>
* <span data-ttu-id="978f3-139">만들기, 삭제, 세부 정보, 편집 및 인덱스 페이지에 대한 Razor 뷰 파일(<em>Views/Movies/&ast;.cshtml</em>)</span><span class="sxs-lookup"><span data-stu-id="978f3-139">Razor view files for Create, Delete, Details, Edit, and Index pages (<em>Views/Movies/&ast;.cshtml</em>)</span></span>

<span data-ttu-id="978f3-140">[CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete)(만들기, 읽기, 업데이트 및 삭제) 작업 메서드와 뷰 및 데이터베이스 컨텍스트의 자동 생성을 *스캐폴딩*이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-140">The automatic creation of the database context and [CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete) (create, read, update, and delete) action methods and views is known as *scaffolding*.</span></span>

<!-- Code -------------------------->
# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="978f3-141">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="978f3-141">Visual Studio Code</span></span>](#tab/visual-studio-code)

<!--  Until https://github.com/aspnet/Scaffolding/issues/582 is fixed windows needs backslash or the namespace is namespace RazorPagesMovie.Pages_Movies rather than namespace RazorPagesMovie.Pages.Movies
-->

* <span data-ttu-id="978f3-142">프로젝트 디렉터리(*Program.cs*, *Startup.cs* 및 *.csproj* 파일이 포함된 디렉터리)에서 명령 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-142">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>
* <span data-ttu-id="978f3-143">스캐폴딩 도구를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-143">Install the scaffolding tool:</span></span>

  ```console
   dotnet tool install --global dotnet-aspnet-codegenerator
   ```

* <span data-ttu-id="978f3-144">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-144">Run the following command:</span></span>

  ```console
     dotnet aspnet-codegenerator controller -name MoviesController -m Movie -dc MvcMovieContext --relativeFolderPath Controllers --useDefaultLayout --referenceScriptLibraries
  ```

[!INCLUDE [explains scaffold generated params](~/includes/mvc-intro/model4.md)]

<!-- Mac -------------------------->

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="978f3-145">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="978f3-145">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* <span data-ttu-id="978f3-146">프로젝트 디렉터리(*Program.cs*, *Startup.cs* 및 *.csproj* 파일이 포함된 디렉터리)에서 명령 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-146">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>
* <span data-ttu-id="978f3-147">스캐폴딩 도구를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-147">Install the scaffolding tool:</span></span>

  ```console
   dotnet tool install --global dotnet-aspnet-codegenerator
   ```

* <span data-ttu-id="978f3-148">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-148">Run the following command:</span></span>

  ```console
     dotnet aspnet-codegenerator controller -name MoviesController -m Movie -dc MvcMovieContext --relativeFolderPath Controllers --useDefaultLayout --referenceScriptLibraries
  ```

[!INCLUDE [explains scaffold gen params](~/includes/RP/model4.md)]

---

<!-- End of VS tabs                  -->

<span data-ttu-id="978f3-149">응용 프로그램을 실행하고 **Mvc Movie** 링크를 클릭하면 다음과 유사한 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-149">If you run the app and click on the **Mvc Movie** link, you get an error similar to the following:</span></span>

``` error
An unhandled exception occurred while processing the request.

SqlException: Cannot open database "MvcMovieContext-<GUID removed>" requested by the login. The login failed.
Login failed for user 'Rick'.

System.Data.SqlClient.SqlInternalConnectionTds..ctor(DbConnectionPoolIdentity identity, SqlConnectionString
```

<span data-ttu-id="978f3-150">데이터베이스를 만들어야 하며 이를 수행하기 위해 EF Core [마이그레이션](xref:data/ef-mvc/migrations) 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-150">You need to create the database, and you use the EF Core [Migrations](xref:data/ef-mvc/migrations) feature to do that.</span></span> <span data-ttu-id="978f3-151">마이그레이션을 통해 데이터 모델과 일치하는 데이터베이스를 만들고 데이터 모델 변경 시 데이터베이스 스키마를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-151">Migrations lets you create a database that matches your data model and update the database schema when your data model changes.</span></span>

<a name="pmc"></a>

## <a name="initial-migration"></a><span data-ttu-id="978f3-152">초기 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="978f3-152">Initial migration</span></span>

<!-- VS -------------------------->

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="978f3-153">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="978f3-153">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="978f3-154">이 섹션에서는 PMC(패키지 관리자 콘솔)를 사용하여 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-154">In this section, the Package Manager Console (PMC) is used to:</span></span>

* <span data-ttu-id="978f3-155">초기 마이그레이션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-155">Add an initial migration.</span></span>
* <span data-ttu-id="978f3-156">초기 마이그레이션을 사용하여 데이터베이스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-156">Update the database with the initial migration.</span></span>

<span data-ttu-id="978f3-157">**도구** 메뉴에서 **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-157">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span>

  ![PMC 메뉴](~/tutorials/first-mvc-app/adding-model/_static/pmc.png)

<span data-ttu-id="978f3-159">PMC에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-159">In the PMC, enter the following commands:</span></span>

```PMC
Add-Migration Initial
Update-Database
```

<span data-ttu-id="978f3-160">`Add-Migration` 명령은 초기 데이터베이스 스키마를 만드는 코드를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-160">The `Add-Migration` command generates code to create the initial database schema.</span></span>
<!-- Code -------------------------->

# <a name="visual-studio-code--visual-studio-for-mactabvisual-studio-codevisual-studio-mac"></a>[<span data-ttu-id="978f3-161">Visual Studio Code / Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="978f3-161">Visual Studio Code / Visual Studio for Mac</span></span>](#tab/visual-studio-code+visual-studio-mac)

[!INCLUDE [initial migration](~/includes/RP/model3.md)]
<span data-ttu-id="978f3-162">`ef migrations add InitialCreate` 명령은 초기 데이터베이스 스키마를 만드는 코드를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-162">The `ef migrations add InitialCreate` command generates code to create the initial database schema.</span></span>

---  
<!-- End of VS tabs -->

<span data-ttu-id="978f3-163">이전 명령은 다음 경고를 생성합니다. "엔터티 형식 'Movie'에서 10진수 열 'Price'의 형식이 지정되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-163">The preceding commands generate the following warning: "No type was specified for the decimal column 'Price' on entity type 'Movie'.</span></span> <span data-ttu-id="978f3-164">그러면 값이 기본 전체 자릿수 및 소수 자릿수에 적합하지 않은 경우 자동으로 잘립니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-164">This will cause values to be silently truncated if they do not fit in the default precision and scale.</span></span> <span data-ttu-id="978f3-165">'HasColumnType()'를 사용하여 모든 값을 수용할 수 있는 SQL Server 열 형식을 명시적으로 지정합니다."</span><span class="sxs-lookup"><span data-stu-id="978f3-165">Explicitly specify the SQL server column type that can accommodate all the values using 'HasColumnType()'."</span></span>

<span data-ttu-id="978f3-166">해당 경고를 무시할 수 있지만 자습서의 뒷부분에서 수정될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-166">You can ignore that warning, it will be fixed in a later tutorial.</span></span>

<span data-ttu-id="978f3-167">스키마는 `DbContext`에 지정된 모델을 기반으로 합니다(*Models/MvcMovieContext.cs* 파일에서).</span><span class="sxs-lookup"><span data-stu-id="978f3-167">The schema is based on the model specified in the `DbContext` (In the *Models/MvcMovieContext.cs* file).</span></span> <span data-ttu-id="978f3-168">`InitialCreate` 인수는 마이그레이션 이름을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-168">The `InitialCreate` argument is used to name the migrations.</span></span> <span data-ttu-id="978f3-169">모든 이름을 사용할 수 있지만 규칙에 따라 마이그레이션을 설명하는 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-169">Any name can be used, but by convention a name is selected that describes the migration.</span></span>

<span data-ttu-id="978f3-170">`ef database update` 명령은 *Migrations/\<time-stamp>_InitialCreate.cs* 파일에서 `Up` 메서드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-170">The `ef database update` command runs the `Up` method in the *Migrations/\<time-stamp>_InitialCreate.cs* file.</span></span> <span data-ttu-id="978f3-171">`Up` 메서드는 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-171">The `Up` method creates the database.</span></span>

<!-- VS -------------------------->

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="978f3-172">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="978f3-172">Visual Studio</span></span>](#tab/visual-studio)

## <a name="examine-the-context-registered-with-dependency-injection"></a><span data-ttu-id="978f3-173">종속성 주입을 사용하여 등록된 컨텍스트 검사</span><span class="sxs-lookup"><span data-stu-id="978f3-173">Examine the context registered with dependency injection</span></span>

<span data-ttu-id="978f3-174">ASP.NET Core는 [종속성 주입](xref:fundamentals/dependency-injection)을 사용하여 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-174">ASP.NET Core is built with [dependency injection](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="978f3-175">서비스(예: EF Core DB 컨텍스트)는 애플리케이션 시작 중에 종속성 주입에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-175">Services (such as the EF Core DB context) are registered with dependency injection during application startup.</span></span> <span data-ttu-id="978f3-176">이러한 서비스(예: Razor 페이지)가 필요한 구성 요소에는 생성자 매개 변수를 통해 이러한 서비스가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-176">Components that require these services (such as Razor Pages) are provided these services via constructor parameters.</span></span> <span data-ttu-id="978f3-177">DB 컨텍스트 인스턴스를 가져오는 생성자 코드는 자습서 뒷부분에 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-177">The constructor code that gets a DB context instance is shown later in the tutorial.</span></span>

<span data-ttu-id="978f3-178">스캐폴딩 도구는 자동으로 DB 컨텍스트를 생성하고 종속성 주입 컨테이너에 등록했습니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-178">The scaffolding tool automatically created a DB context and registered it with the dependency injection container.</span></span>

<span data-ttu-id="978f3-179">`Startup.ConfigureServices` 메서드를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-179">Examine the `Startup.ConfigureServices` method.</span></span> <span data-ttu-id="978f3-180">강조 표시된 줄은 스캐폴더에서 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-180">The highlighted line was added by the scaffolder:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Startup.cs?name=snippet_ConfigureServices&highlight=15-18)]

<span data-ttu-id="978f3-181">`MvcMovieContext`는 `Movie` 모델에 대한 EF Core 기능(만들기, 읽기, 업데이트, 삭제 등)을 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-181">The `MvcMovieContext` coordinates EF Core functionality (Create, Read, Update, Delete, etc.) for the `Movie` model.</span></span> <span data-ttu-id="978f3-182">데이터 컨텍스트(`MvcMovieContext`)는 [Microsoft.EntityFrameworkCore.DbContext](/dotnet/api/microsoft.entityframeworkcore.dbcontext)에서 파생됩니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-182">The data context (`MvcMovieContext`) is derived from [Microsoft.EntityFrameworkCore.DbContext](/dotnet/api/microsoft.entityframeworkcore.dbcontext).</span></span> <span data-ttu-id="978f3-183">데이터 컨텍스트는 데이터 모델에 포함되는 엔터티를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-183">The data context specifies which entities are included in the data model:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Data/MvcMovieContext.cs)]

<span data-ttu-id="978f3-184">이전 코드에서는 엔터티 집합에 대한 [`DbSet<Movie>`](/dotnet/api/microsoft.entityframeworkcore.dbset-1) 속성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-184">The preceding code creates a [`DbSet<Movie>`](/dotnet/api/microsoft.entityframeworkcore.dbset-1) property for the entity set.</span></span> <span data-ttu-id="978f3-185">Entity Framework 용어에서 엔터티 집합은 일반적으로 데이터베이스 테이블에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-185">In Entity Framework terminology, an entity set typically corresponds to a database table.</span></span> <span data-ttu-id="978f3-186">엔터티는 테이블의 행에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-186">An entity corresponds to a row in the table.</span></span>

<span data-ttu-id="978f3-187">[DbContextOptions](/dotnet/api/microsoft.entityframeworkcore.dbcontextoptions) 개체에서 메서드를 호출하여 연결 문자열의 이름을 컨텍스트에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-187">The name of the connection string is passed in to the context by calling a method on a [DbContextOptions](/dotnet/api/microsoft.entityframeworkcore.dbcontextoptions) object.</span></span> <span data-ttu-id="978f3-188">로컬 개발의 경우 [ASP.NET Core 구성 시스템](xref:fundamentals/configuration/index)은 *appsettings.json* 파일에서 연결 문자열을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-188">For local development, the [ASP.NET Core configuration system](xref:fundamentals/configuration/index) reads the connection string from the *appsettings.json* file.</span></span>
<!-- Code -------------------------->

# <a name="visual-studio-code--visual-studio-for-mactabvisual-studio-codevisual-studio-mac"></a>[<span data-ttu-id="978f3-189">Visual Studio Code / Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="978f3-189">Visual Studio Code / Visual Studio for Mac</span></span>](#tab/visual-studio-code+visual-studio-mac)

<span data-ttu-id="978f3-190">ASP.NET Core는 [종속성 주입](xref:fundamentals/dependency-injection)을 사용하여 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-190">ASP.NET Core is built with [dependency injection](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="978f3-191">서비스(예: EF Core DB 컨텍스트)는 애플리케이션 시작 중에 종속성 주입에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-191">Services (such as the EF Core DB context) are registered with dependency injection during application startup.</span></span> <span data-ttu-id="978f3-192">이러한 서비스(예: Razor 페이지)가 필요한 구성 요소에는 생성자 매개 변수를 통해 이러한 서비스가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-192">Components that require these services (such as Razor Pages) are provided these services via constructor parameters.</span></span> <span data-ttu-id="978f3-193">DB 컨텍스트 인스턴스를 가져오는 생성자 코드는 자습서 뒷부분에 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-193">The constructor code that gets a DB context instance is shown later in the tutorial.</span></span>

<span data-ttu-id="978f3-194">DB 컨텍스트를 생성하고 종속성 주입 컨테이너에 등록했습니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-194">You created a DB context and registered it with the dependency injection container.</span></span>

---

<span data-ttu-id="978f3-195">스키마는 `MvcMovieContext`에 지정된 모델을 기반으로 합니다(*Data/MvcMovieContext.cs* 파일).</span><span class="sxs-lookup"><span data-stu-id="978f3-195">The schema is based on the model specified in the `MvcMovieContext` (In the *Data/MvcMovieContext.cs* file).</span></span> <span data-ttu-id="978f3-196">`Initial` 인수는 마이그레이션 이름을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-196">The `Initial` argument is used to name the migrations.</span></span> <span data-ttu-id="978f3-197">모든 이름을 사용할 수 있지만 규칙에 따라 마이그레이션을 설명하는 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-197">Any name can be used, but by convention a name that describes the migration is used.</span></span> <span data-ttu-id="978f3-198">자세한 내용은 [마이그레이션 소개](xref:data/ef-mvc/migrations#introduction-to-migrations)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="978f3-198">See [Introduction to migrations](xref:data/ef-mvc/migrations#introduction-to-migrations) for more information.</span></span>

<span data-ttu-id="978f3-199">`Update-Database` 명령은 데이터베이스를 만드는 *Migrations/{time-stamp}_InitialCreate.cs* 파일에서 `Up` 메서드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-199">The `Update-Database` command runs the `Up` method in the *Migrations/{time-stamp}_InitialCreate.cs* file, which creates the database.</span></span>

<a name="test"></a>

### <a name="test-the-app"></a><span data-ttu-id="978f3-200">앱 테스트</span><span class="sxs-lookup"><span data-stu-id="978f3-200">Test the app</span></span>

* <span data-ttu-id="978f3-201">앱을 실행하고 브라우저에서 `/Movies`를 URL에 추가합니다(`http://localhost:port/movies`).</span><span class="sxs-lookup"><span data-stu-id="978f3-201">Run the app and append `/Movies` to the URL in the browser (`http://localhost:port/movies`).</span></span>

<span data-ttu-id="978f3-202">다음과 비슷한 데이터베이스 예외가 발생하는 경우:</span><span class="sxs-lookup"><span data-stu-id="978f3-202">If you get a database exception similar to the following:</span></span>

```console
SqlException: Cannot open database "MvcMovieContext-GUID" requested by the login. The login failed.
Login failed for user 'User-name'.
```

<span data-ttu-id="978f3-203">[마이그레이션 단계](#pmc)를 누락했습니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-203">You missed the [migrations step](#pmc).</span></span>

* <span data-ttu-id="978f3-204">**만들기** 링크를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-204">Test the **Create** link.</span></span>

  > [!NOTE]
  > <span data-ttu-id="978f3-205">`Price` 필드에는 소수점을 입력하지 못할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-205">You may not be able to enter decimal commas in the `Price` field.</span></span> <span data-ttu-id="978f3-206">소수점으로 쉼표(",")를 사용하는 영어가 아닌 로캘 및 미국 영어가 아닌 날짜 형식에 대해 [jQuery 유효성 검사](https://jqueryvalidation.org/)를 지원하려면 앱을 글로벌화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-206">To support [jQuery validation](https://jqueryvalidation.org/) for non-English locales that use a comma (",") for a decimal point and for non US-English date formats, the app must be globalized.</span></span> <span data-ttu-id="978f3-207">세계화 지침은 [이 GitHub 문제](https://github.com/aspnet/Docs/issues/4076#issuecomment-326590420)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="978f3-207">For globalization instructions, see [this GitHub issue](https://github.com/aspnet/Docs/issues/4076#issuecomment-326590420).</span></span>

* <span data-ttu-id="978f3-208">**편집**, **세부 정보** 및 **삭제** 링크를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-208">Test the **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="978f3-209">`Startup` 클래스를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-209">Examine the `Startup` class:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Startup.cs?name=snippet_ConfigureServices&highlight=13-99)]

<span data-ttu-id="978f3-210">앞에서 강조 표시된 코드는 [종속성 주입](xref:fundamentals/dependency-injection) 컨테이너에 추가된 영화 데이터베이스 컨텍스트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-210">The preceding highlighted code shows the movie database context being added to the [Dependency Injection](xref:fundamentals/dependency-injection) container:</span></span>

* <span data-ttu-id="978f3-211">`services.AddDbContext<MvcMovieContext>(options =>`는 사용할 데이터베이스 및 연결 문자열을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-211">`services.AddDbContext<MvcMovieContext>(options =>` specifies the database to use and the connection string.</span></span>
* <span data-ttu-id="978f3-212">`=>`은 [람다 연산자](/dotnet/articles/csharp/language-reference/operators/lambda-operator)입니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-212">`=>` is a [lambda operator](/dotnet/articles/csharp/language-reference/operators/lambda-operator)</span></span>

<span data-ttu-id="978f3-213">*Controllers/MoviesController.cs* 파일을 열고 생성자를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-213">Open the *Controllers/MoviesController.cs* file and examine the constructor:</span></span>

<!-- l.. Make copy of Movies controller because we comment out the initial index method and update it later  -->

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Controllers/MC1.cs?name=snippet_1)]

<span data-ttu-id="978f3-214">생성자는 [종속성 주입](xref:fundamentals/dependency-injection)을 사용하여 컨트롤러에 데이터베이스 컨텍스트(`MvcMovieContext `)를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-214">The constructor uses [Dependency Injection](xref:fundamentals/dependency-injection) to inject the database context (`MvcMovieContext `) into the controller.</span></span> <span data-ttu-id="978f3-215">컨트롤러의 [CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete) 메서드 각각에서 데이터베이스 컨텍스트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-215">The database context is used in each of the [CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete) methods in the controller.</span></span>

<a name="strongly-typed-models-keyword-label"></a>
<a name="strongly-typed-models-and-the--keyword"></a>

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="978f3-216">강력한 형식의 모델 및 @model 키워드</span><span class="sxs-lookup"><span data-stu-id="978f3-216">Strongly typed models and the @model keyword</span></span>

<span data-ttu-id="978f3-217">이 자습서의 앞부분에서 언급했듯이 컨트롤러가 `ViewData` 사전을 사용하여 데이터 또는 개체를 뷰에 전달할 수 있는 방법이 표시되었습니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-217">Earlier in this tutorial, you saw how a controller can pass data or objects to a view using the `ViewData` dictionary.</span></span> <span data-ttu-id="978f3-218">`ViewData` 사전은 확인할 정보를 전달하는 편리한 런타임에 바인딩된 방법을 제공하는 동적 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-218">The `ViewData` dictionary is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="978f3-219">또한 MVC는 확인할 강력한 형식의 모델 개체를 전달하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-219">MVC also provides the ability to pass strongly typed model objects to a view.</span></span> <span data-ttu-id="978f3-220">이렇게 강력하게 형식화된 방법을 사용하면 코드를 검사하는 컴파일 시간을 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-220">This strongly typed approach enables better compile time checking of your code.</span></span> <span data-ttu-id="978f3-221">스캐폴딩 메커니즘은 메서드 및 뷰를 만든 경우 `MoviesController` 클래스 및 뷰에서 이 방법(즉, 강력한 형식의 모델 전달)을 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-221">The scaffolding mechanism used this approach (that is, passing a strongly typed model) with the `MoviesController` class and views when it created the methods and views.</span></span>

<span data-ttu-id="978f3-222">*Controllers/MoviesController.cs* 파일에서 생성된 `Details` 메서드를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-222">Examine the generated `Details` method in the *Controllers/MoviesController.cs* file:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Controllers/MC1.cs?name=snippet_details)]

<span data-ttu-id="978f3-223">`id` 매개 변수는 일반적으로 경로 데이터 변수로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-223">The `id` parameter is generally passed as route data.</span></span> <span data-ttu-id="978f3-224">예를 들어 `https://localhost:5001/movies/details/1`은 다음을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-224">For example `https://localhost:5001/movies/details/1` sets:</span></span>

* <span data-ttu-id="978f3-225">`movies` 컨트롤러에 대한 컨트롤러(첫 번째 URL 세그먼트)</span><span class="sxs-lookup"><span data-stu-id="978f3-225">The controller to the `movies` controller (the first URL segment).</span></span>
* <span data-ttu-id="978f3-226">`details`에 대한 작업(두 번째 URL 세그먼트)</span><span class="sxs-lookup"><span data-stu-id="978f3-226">The action to `details` (the second URL segment).</span></span>
* <span data-ttu-id="978f3-227">1에 대한 ID(마지막 URL 세그먼트)</span><span class="sxs-lookup"><span data-stu-id="978f3-227">The id to 1 (the last URL segment).</span></span>

<span data-ttu-id="978f3-228">다음과 같이 쿼리 문자열을 사용하여 `id`에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-228">You can also pass in the `id` with a query string as follows:</span></span>

`https://localhost:5001/movies/details?id=1`

<span data-ttu-id="978f3-229">ID 값이 제공되지 않는 경우에 `id` 매개 변수가 [nullable 형식](/dotnet/csharp/programming-guide/nullable-types/index)(`int?`)으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-229">The `id` parameter is defined as a [nullable type](/dotnet/csharp/programming-guide/nullable-types/index) (`int?`) in case an ID value isn't provided.</span></span>

<span data-ttu-id="978f3-230">[람다 식](/dotnet/articles/csharp/programming-guide/statements-expressions-operators/lambda-expressions)을 `FirstOrDefaultAsync`에 전달하여 경로 데이터 또는 쿼리 문자열 값과 일치하는 영화 엔터티를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-230">A [lambda expression](/dotnet/articles/csharp/programming-guide/statements-expressions-operators/lambda-expressions) is passed in to `FirstOrDefaultAsync` to select movie entities that match the route data or query string value.</span></span>

```csharp
var movie = await _context.Movie
    .FirstOrDefaultAsync(m => m.Id == id);
```

<span data-ttu-id="978f3-231">영화가 있으면 `Movie` 모델의 인스턴스를 `Details` 뷰에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-231">If a movie is found, an instance of the `Movie` model is passed to the `Details` view:</span></span>

```csharp
return View(movie);
   ```

<span data-ttu-id="978f3-232">*Views/Movies/Details.cshtml* 파일의 내용을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-232">Examine the contents of the *Views/Movies/Details.cshtml* file:</span></span>

[!code-html[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Views/Movies/DetailsOriginal.cshtml)]

<span data-ttu-id="978f3-233">뷰 파일 맨 위에 있는 `@model` 문을 포함하여 뷰에서 필요로 하는 개체의 유형을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-233">By including a `@model` statement at the top of the view file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="978f3-234">영화 컨트롤러를 만들 때 *Details.cshtml* 파일의 맨 위에 다음 `@model` 문이 자동으로 포함되었습니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-234">When you created the movie controller, the following `@model` statement was automatically included at the top of the *Details.cshtml* file:</span></span>

```HTML
@model MvcMovie.Models.Movie
   ```

<span data-ttu-id="978f3-235">이 `@model` 지시문을 사용하면 강력한 형식인 `Model` 개체를 사용하여 컨트롤러가 뷰에 전달된 영화에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-235">This `@model` directive allows you to access the movie that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="978f3-236">예를 들어 *Details.cshtml* 뷰에서 코드는 각 영화 필드를 강력한 형식의 `Model` 개체를 사용하여 `DisplayNameFor` 및 `DisplayFor` HTML 도우미에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-236">For example, in the *Details.cshtml* view, the code passes each movie field to the `DisplayNameFor` and `DisplayFor` HTML Helpers with the strongly typed `Model` object.</span></span> <span data-ttu-id="978f3-237">또한 `Create` 및 `Edit` 메서드 및 뷰는 `Movie` 모델 개체를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-237">The `Create` and `Edit` methods and views also pass a `Movie` model object.</span></span>

<span data-ttu-id="978f3-238">영화 컨트롤러에서 *Index.cshtml* 뷰 및 `Index` 메서드를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-238">Examine the *Index.cshtml* view and the `Index` method in the Movies controller.</span></span> <span data-ttu-id="978f3-239">코드가 `View` 메서드를 호출하는 경우 `List` 개체를 생성하는 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-239">Notice how the code creates a `List` object when it calls the `View` method.</span></span> <span data-ttu-id="978f3-240">이 코드는 `Index` 작업 메서드의 `Movies` 목록을 뷰에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-240">The code passes this `Movies` list from the `Index` action method to the view:</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Controllers/MC1.cs?name=snippet_index)]

<span data-ttu-id="978f3-241">영화 컨트롤러를 만들 때 스캐폴딩에서는 *Index.cshtml* 파일의 맨 위에 다음 `@model` 문을 자동으로 포함했습니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-241">When you created the movies controller, scaffolding automatically included the following `@model` statement at the top of the *Index.cshtml* file:</span></span>

<!-- Copy Index.cshtml to IndexOriginal.cshtml -->

[!code-html[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Views/Movies/IndexOriginal.cshtml?range=1)]

<span data-ttu-id="978f3-242">`@model` 지시문을 사용하면 강력한 형식인 `Model` 개체를 사용하여 컨트롤러가 뷰에 전달된 영화 목록에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-242">The `@model` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="978f3-243">예를 들어 *Index.cshtml* 뷰에서 코드는 강력한 형식의 `Model` 개체에 `foreach` 문을 포함한 영화를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-243">For example, in the *Index.cshtml* view, the code loops through the movies with a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-html[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Views/Movies/IndexOriginal.cshtml?highlight=1,31,34,37,40,43,46-48)]

<span data-ttu-id="978f3-244">`Model` 개체가 강력한 형식이기 때문에(`IEnumerable<Movie>` 개체처럼) 루프의 각 항목은 `Movie`으로 입력됩니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-244">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each item in the loop is typed as `Movie`.</span></span> <span data-ttu-id="978f3-245">즉, 여러 가지 이점 중에서 코드를 검사하는 컴파일 시간을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="978f3-245">Among other benefits, this means that you get compile time checking of the code:</span></span>

## <a name="additional-resources"></a><span data-ttu-id="978f3-246">추가 자료</span><span class="sxs-lookup"><span data-stu-id="978f3-246">Additional resources</span></span>

* [<span data-ttu-id="978f3-247">태그 도우미</span><span class="sxs-lookup"><span data-stu-id="978f3-247">Tag Helpers</span></span>](xref:mvc/views/tag-helpers/intro)
* [<span data-ttu-id="978f3-248">전역화 및 지역화</span><span class="sxs-lookup"><span data-stu-id="978f3-248">Globalization and localization</span></span>](xref:fundamentals/localization)

> [!div class="step-by-step"]
> <span data-ttu-id="978f3-249">[이전 뷰 추가](adding-view.md)
> [다음 SQL 사용](working-with-sql.md)</span><span class="sxs-lookup"><span data-stu-id="978f3-249">[Previous Adding a View](adding-view.md)
[Next Working with SQL](working-with-sql.md)</span></span>  
