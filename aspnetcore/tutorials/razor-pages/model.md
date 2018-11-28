---
title: ASP.NET Core에서 Razor 페이지 앱에 모델 추가
author: rick-anderson
description: Entity Framework Core(EF Core)를 사용하여 데이터베이스에서 영화를 관리하기 위한 클래스를 추가하는 방법을 알아봅니다.
ms.author: riande
ms.date: 05/30/2018
uid: tutorials/razor-pages/model
ms.openlocfilehash: c4b23f75da298e4ee804f649219c2ce466b6d6ea
ms.sourcegitcommit: 710fc5fcac258cc8415976dc66bdb355b3e061d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52299445"
---
# <a name="add-a-model-to-a-razor-pages-app-in-aspnet-core"></a><span data-ttu-id="f0864-103">ASP.NET Core에서 Razor 페이지 앱에 모델 추가</span><span class="sxs-lookup"><span data-stu-id="f0864-103">Add a model to a Razor Pages app in ASP.NET Core</span></span>

::: moniker range=">= aspnetcore-2.1"

[!INCLUDE [model1](~/includes/RP/model1.md)]

## <a name="add-a-data-model"></a><span data-ttu-id="f0864-104">데이터 모델 추가</span><span class="sxs-lookup"><span data-stu-id="f0864-104">Add a data model</span></span>

<span data-ttu-id="f0864-105">솔루션 탐색기에서 **RazorPagesMovie** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 폴더**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-105">In Solution Explorer, right-click the **RazorPagesMovie** project > **Add** > **New Folder**.</span></span> <span data-ttu-id="f0864-106">폴더 이름을 *Models*로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-106">Name the folder *Models*.</span></span>

<span data-ttu-id="f0864-107">*Models* 폴더를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-107">Right click the *Models* folder.</span></span> <span data-ttu-id="f0864-108">**추가** > **클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-108">Select **Add** > **Class**.</span></span> <span data-ttu-id="f0864-109">**Movie**라고 클래스의 이름을 지정하고 `Movie` 클래스의 콘텐츠를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-109">Name the class **Movie** and replace the contents of the `Movie` class with the following code:</span></span>

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie21/Models/Movie1.cs?name=snippet)]

## <a name="scaffold-the-movie-model"></a><span data-ttu-id="f0864-110">동영상 모델 스캐폴드</span><span class="sxs-lookup"><span data-stu-id="f0864-110">Scaffold the movie model</span></span>

<span data-ttu-id="f0864-111">이 섹션에서는 동영상 모델을 스캐폴 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-111">In this section, the movie model is scaffolded.</span></span> <span data-ttu-id="f0864-112">즉, 스캐폴드 도구는 동영상 모델에서 CRUD(만들기, 읽기, 업데이트 및 삭제) 작업을 위한 페이지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-112">That is, the scaffolding tool produces pages for Create, Read, Update, and Delete (CRUD) operations for the movie model.</span></span>

<span data-ttu-id="f0864-113">*Pages/Movies* 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-113">Create a *Pages/Movies* folder:</span></span>

* <span data-ttu-id="f0864-114">**솔루션 탐색기**에서 *Pages* 폴더 > **추가** > **새 폴더**를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-114">In **Solution Explorer**, right click on the *Pages* folder > **Add** > **New Folder**.</span></span>
* <span data-ttu-id="f0864-115">폴더 이름을 *Movies*로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-115">Name the folder *Movies*</span></span>

<span data-ttu-id="f0864-116">**솔루션 탐색기**에서 *Pages/Movies* 폴더 > **추가** > **새 스캐폴드된 항목**을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-116">In **Solution Explorer**, right click on the *Pages/Movies* folder > **Add** > **New Scaffolded Item**.</span></span>

![이전 지침의 이미지입니다.](model/_static/sca.png)

<span data-ttu-id="f0864-118">**스캐폴드 추가** 대화 상자에서 **Entity Framework(CRUD)를 사용한 Razor Pages** > **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-118">In the **Add Scaffold** dialog, select **Razor Pages using Entity Framework (CRUD)** > **Add**.</span></span>

![이전 지침의 이미지입니다.](model/_static/add_scaffold.png)

<span data-ttu-id="f0864-120">**Entity Framework(CRUD)를 사용하여 Razor Pages 추가** 대화 상자를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-120">Complete the **Add Razor Pages using Entity Framework (CRUD)** dialog:</span></span>

* <span data-ttu-id="f0864-121">**모델 클래스** 드롭다운에서 **동영상(RazorPagesMovie.Models)** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-121">In the **Model class** drop down, select **Movie (RazorPagesMovie.Models)**.</span></span>
* <span data-ttu-id="f0864-122">**데이터 컨텍스트 클래스** 행에서 **+** 기호를 선택하고 생성된 이름인 **RazorPagesMovie.Models.RazorPagesMovieContext**를 수용합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-122">In the **Data context class** row, select the **+** (plus) sign and accept the generated name **RazorPagesMovie.Models.RazorPagesMovieContext**.</span></span>
* <span data-ttu-id="f0864-123">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-123">Select **Add**.</span></span>

![이전 지침의 이미지입니다.](model/_static/arp.png)

<span data-ttu-id="f0864-125">스캐폴드 프로세스는 다음 파일을 생성하고 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-125">The scaffold process creates and updates the following files:</span></span>

### <a name="files-created"></a><span data-ttu-id="f0864-126">생성된 파일</span><span class="sxs-lookup"><span data-stu-id="f0864-126">Files created</span></span>

* <span data-ttu-id="f0864-127">*Pages/Movies*: 만들기, 삭제, 세부 정보, 편집, 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-127">*Pages/Movies*: Create, Delete, Details, Edit, Index.</span></span> <span data-ttu-id="f0864-128">이러한 페이지는 다음 자습서에서 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-128">These pages are detailed in the next tutorial.</span></span>
* <span data-ttu-id="f0864-129">*Data/RazorPagesMovieContext.cs*</span><span class="sxs-lookup"><span data-stu-id="f0864-129">*Data/RazorPagesMovieContext.cs*</span></span>

### <a name="file-updated"></a><span data-ttu-id="f0864-130">파일 업데이트됨</span><span class="sxs-lookup"><span data-stu-id="f0864-130">File updated</span></span>

* <span data-ttu-id="f0864-131">*Startup.cs*: 이 파일의 변경 내용은 다음 섹션에서 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-131">*Startup.cs*: Changes to this file are detailed in the next section.</span></span>
* <span data-ttu-id="f0864-132">*appsettings.json*: 로컬 데이터베이스에 연결하는 데 사용된 연결 문자열이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-132">*appsettings.json*: The connection string used to connect to a local database is added.</span></span>

## <a name="examine-the-context-registered-with-dependency-injection"></a><span data-ttu-id="f0864-133">종속성 주입을 사용하여 등록된 컨텍스트 검사</span><span class="sxs-lookup"><span data-stu-id="f0864-133">Examine the context registered with dependency injection</span></span>

<span data-ttu-id="f0864-134">ASP.NET Core는 [종속성 주입](xref:fundamentals/dependency-injection)을 사용하여 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-134">ASP.NET Core is built with [dependency injection](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="f0864-135">서비스(예: EF Core DB 컨텍스트)는 응용 프로그램 시작 중에 종속성 주입에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-135">Services (such as the EF Core DB context) are registered with dependency injection during application startup.</span></span> <span data-ttu-id="f0864-136">이러한 서비스(예: Razor 페이지)가 필요한 구성 요소에는 생성자 매개 변수를 통해 이러한 서비스가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-136">Components that require these services (such as Razor Pages) are provided these services via constructor parameters.</span></span> <span data-ttu-id="f0864-137">DB 컨텍스트 인스턴스를 가져오는 생성자 코드는 자습서 뒷부분에 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-137">The constructor code that gets a DB context instance is shown later in the tutorial.</span></span>

<span data-ttu-id="f0864-138">스캐폴딩 도구는 자동으로 DB 컨텍스트를 생성하고 종속성 주입 컨테이너에 등록했습니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-138">The scaffolding tool automatically created a DB context and registered it with the dependency injection container.</span></span>

<span data-ttu-id="f0864-139">`Startup.ConfigureServices` 메서드를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-139">Examine the `Startup.ConfigureServices` method.</span></span> <span data-ttu-id="f0864-140">강조 표시된 줄은 스캐폴더에서 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-140">The highlighted line was added by the scaffolder:</span></span>

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie21/Startup.cs?name=snippet_ConfigureServices&highlight=12-13)]

<span data-ttu-id="f0864-141">특정 데이터 모델에 맞게 EF Core 기능을 조정하는 주 클래스는 DB 컨텍스트 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-141">The main class that coordinates EF Core functionality for a given data model is the DB context class.</span></span> <span data-ttu-id="f0864-142">데이터 컨텍스트는 [Microsoft.EntityFrameworkCore.DbContext](/dotnet/api/microsoft.entityframeworkcore.dbcontext)에서 파생됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-142">The data context is derived from [Microsoft.EntityFrameworkCore.DbContext](/dotnet/api/microsoft.entityframeworkcore.dbcontext).</span></span> <span data-ttu-id="f0864-143">데이터 컨텍스트는 데이터 모델에 포함되는 엔터티를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-143">The data context specifies which entities are included in the data model.</span></span> <span data-ttu-id="f0864-144">이 프로젝트에서 클래스 이름은 `RazorPagesMovieContext`로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-144">In this project, the class is named `RazorPagesMovieContext`.</span></span>

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie21/Data/RazorPagesMovieContext.cs)]

<span data-ttu-id="f0864-145">이전 코드에서는 엔터티 집합에 대해 [DbSet\<Movie>](/dotnet/api/microsoft.entityframeworkcore.dbset-1) 속성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-145">The preceding code creates a [DbSet\<Movie>](/dotnet/api/microsoft.entityframeworkcore.dbset-1) property for the entity set.</span></span> <span data-ttu-id="f0864-146">Entity Framework 용어에서 엔터티 집합은 일반적으로 데이터베이스 테이블에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-146">In Entity Framework terminology, an entity set typically corresponds to a database table.</span></span> <span data-ttu-id="f0864-147">엔터티는 테이블의 행에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-147">An entity corresponds to a row in the table.</span></span>

<span data-ttu-id="f0864-148">[DbContextOptions](/dotnet/api/microsoft.entityframeworkcore.dbcontextoptions) 개체에서 메서드를 호출하여 연결 문자열의 이름을 컨텍스트에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-148">The name of the connection string is passed in to the context by calling a method on a [DbContextOptions](/dotnet/api/microsoft.entityframeworkcore.dbcontextoptions) object.</span></span> <span data-ttu-id="f0864-149">로컬 개발의 경우 [ASP.NET Core 구성 시스템](xref:fundamentals/configuration/index)은 *appsettings.json* 파일에서 연결 문자열을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-149">For local development, the [ASP.NET Core configuration system](xref:fundamentals/configuration/index) reads the connection string from the *appsettings.json* file.</span></span>

<a name="pmc"></a>
## <a name="perform-initial-migration"></a><span data-ttu-id="f0864-150">초기 마이그레이션 수행</span><span class="sxs-lookup"><span data-stu-id="f0864-150">Perform initial migration</span></span>

<span data-ttu-id="f0864-151">이 섹션에서는 PMC(패키지 관리자 콘솔)를 사용하여 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-151">In this section, you use the Package Manager Console (PMC) to:</span></span>

* <span data-ttu-id="f0864-152">초기 마이그레이션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-152">Add an initial migration.</span></span>
* <span data-ttu-id="f0864-153">초기 마이그레이션을 사용하여 데이터베이스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-153">Update the database with the initial migration.</span></span>

<span data-ttu-id="f0864-154">**도구** 메뉴에서 **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-154">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span>

  ![PMC 메뉴](../first-mvc-app/adding-model/_static/pmc.png)

<span data-ttu-id="f0864-156">PMC에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-156">In the PMC, enter the following commands:</span></span>

```PMC
Add-Migration Initial
Update-Database
```

<span data-ttu-id="f0864-157">또는 프로젝트 폴더에서 다음 .NET Core CLI 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-157">Alternatively, the following .NET Core CLI commands can be used from the project folder:</span></span>

```console
dotnet ef migrations add Initial
dotnet ef database update
```

<span data-ttu-id="f0864-158">다음과 같은 경고 메시지를 무시합니다. 해당 문제를 나중에 자습서에서 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-158">Ignore the following warning message, which you fix in a later tutorial:</span></span>

```console
Microsoft.EntityFrameworkCore.Model.Validation[30000]
      No type was specified for the decimal column 'Price' on entity type 'Movie'. This will cause values to be silently truncated if they do not fit in the default precision and scale. Explicitly specify the SQL server column type that can accommodate all the values using 'ForHasColumnType()'.
```

<span data-ttu-id="f0864-159">`Add-Migration` 명령은 초기 데이터베이스 스키마를 만드는 코드를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-159">The `Add-Migration` command generates code to create the initial database schema.</span></span> <span data-ttu-id="f0864-160">스키마는 `RazorPagesMovieContext`에 지정된 모델을 기반으로 합니다(*Data/RazorPagesMovieContext.cs* 파일).</span><span class="sxs-lookup"><span data-stu-id="f0864-160">The schema is based on the model specified in the `RazorPagesMovieContext` (In the *Data/RazorPagesMovieContext.cs* file).</span></span> <span data-ttu-id="f0864-161">`Initial` 인수는 마이그레이션 이름을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-161">The `Initial` argument is used to name the migrations.</span></span> <span data-ttu-id="f0864-162">모든 이름을 사용할 수 있지만 일반적으로 마이그레이션을 설명하는 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-162">You can use any name, but by convention you choose a name that describes the migration.</span></span> <span data-ttu-id="f0864-163">자세한 내용은 [마이그레이션 소개](xref:data/ef-mvc/migrations#introduction-to-migrations)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0864-163">See [Introduction to migrations](xref:data/ef-mvc/migrations#introduction-to-migrations) for more information.</span></span>

<span data-ttu-id="f0864-164">`Update-Database` 명령은 데이터베이스를 만드는 *Migrations/{time-stamp}_InitialCreate.cs* 파일에서 `Up` 메서드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-164">The `Update-Database` command runs the `Up` method in the *Migrations/{time-stamp}_InitialCreate.cs* file, which creates the database.</span></span>

<span data-ttu-id="f0864-165">오류가 표시될 경우:</span><span class="sxs-lookup"><span data-stu-id="f0864-165">If you get the error:</span></span>

```console
SqlException: Cannot open database "RazorPagesMovieContext-GUID" requested by the login. The login failed.
Login failed for user 'User-name'.
```

<span data-ttu-id="f0864-166">[마이그레이션 단계](#pmc)를 누락했습니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-166">You missed the [migrations step](#pmc).</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!INCLUDE [model1](~/includes/RP/model1.md)]

## <a name="add-a-data-model"></a><span data-ttu-id="f0864-167">데이터 모델 추가</span><span class="sxs-lookup"><span data-stu-id="f0864-167">Add a data model</span></span>

<span data-ttu-id="f0864-168">솔루션 탐색기에서 **RazorPagesMovie** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 폴더**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-168">In Solution Explorer, right-click the **RazorPagesMovie** project > **Add** > **New Folder**.</span></span> <span data-ttu-id="f0864-169">폴더 이름을 *Models*로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-169">Name the folder *Models*.</span></span>

<span data-ttu-id="f0864-170">*Models* 폴더를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-170">Right click the *Models* folder.</span></span> <span data-ttu-id="f0864-171">**추가** > **클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-171">Select **Add** > **Class**.</span></span> <span data-ttu-id="f0864-172">클래스 이름을 **Movie**로 지정하고 다음 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-172">Name the class **Movie** and add the following properties:</span></span>

[!INCLUDE [model 2](~/includes/RP/model2.md)]

<a name="cs"></a>
### <a name="add-a-database-connection-string"></a><span data-ttu-id="f0864-173">데이터베이스 연결 문자열 추가</span><span class="sxs-lookup"><span data-stu-id="f0864-173">Add a database connection string</span></span>

<span data-ttu-id="f0864-174">*appsettings.json* 파일에 연결 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-174">Add a connection string to the *appsettings.json* file.</span></span>

[!code-json[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/appsettings.json?highlight=8-10)]

<a name="reg"></a>
###  <a name="register-the-database-context"></a><span data-ttu-id="f0864-175">데이터베이스 컨텍스트 등록</span><span class="sxs-lookup"><span data-stu-id="f0864-175">Register the database context</span></span>

<span data-ttu-id="f0864-176">[스타트업 클래스(*Startup.cs*)의 ConfigureServices 메서드](xref:fundamentals/startup#the-startup-class)에서 [종속성 주입](xref:fundamentals/dependency-injection) 컨테이너에 데이터베이스 컨텍스트를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-176">Register the database context with the [dependency injection](xref:fundamentals/dependency-injection) container in the [ConfigureServices method of the Startup class](xref:fundamentals/startup#the-startup-class) (*Startup.cs*):</span></span>

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Startup.cs?name=snippet_ConfigureServices&highlight=3-5,7-9)]

<span data-ttu-id="f0864-177">프로젝트를 빌드하여 오류가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-177">Build the project to verify you don't have any errors.</span></span>

<a name="pmc"></a>
## <a name="add-scaffold-tooling-and-perform-initial-migration"></a><span data-ttu-id="f0864-178">스캐폴드 도구 추가 및 초기 마이그레이션 수행</span><span class="sxs-lookup"><span data-stu-id="f0864-178">Add scaffold tooling and perform initial migration</span></span>

<span data-ttu-id="f0864-179">이 섹션에서는 PMC(패키지 관리자 콘솔)를 사용하여 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-179">In this section, you use the Package Manager Console (PMC) to:</span></span>

* <span data-ttu-id="f0864-180">Visual Studio 웹 코드 생성 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-180">Add the Visual Studio web code generation package.</span></span> <span data-ttu-id="f0864-181">스캐폴딩 엔진을 실행하려면 이 패키지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-181">This package is required to run the scaffolding engine.</span></span>
* <span data-ttu-id="f0864-182">초기 마이그레이션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-182">Add an initial migration.</span></span>
* <span data-ttu-id="f0864-183">초기 마이그레이션을 사용하여 데이터베이스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-183">Update the database with the initial migration.</span></span>

<span data-ttu-id="f0864-184">**도구** 메뉴에서 **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-184">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span>

  ![PMC 메뉴](../first-mvc-app/adding-model/_static/pmc.png)

<span data-ttu-id="f0864-186">PMC에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-186">In the PMC, enter the following commands:</span></span>

```powershell
Install-Package Microsoft.VisualStudio.Web.CodeGeneration.Design -Version 2.0.3
Add-Migration Initial
Update-Database
```

<span data-ttu-id="f0864-187">또는 다음 .NET Core CLI 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-187">Alternatively, the following .NET Core CLI commands can be used:</span></span>

```console
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet ef migrations add Initial
dotnet ef database update
```

<span data-ttu-id="f0864-188">다음과 같은 메시지를 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-188">Ignore the following message:</span></span>

```console
Microsoft.EntityFrameworkCore.Model.Validation[30000]
      No type was specified for the decimal column 'Price' on entity type 'Movie'. This will cause values to be silently truncated if they do not fit in the default precision and scale. Explicitly specify the SQL server column type that can accommodate all the values using 'ForHasColumnType()'
```

<span data-ttu-id="f0864-189">다음 자습서에서 해당 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-189">You fix that in the next tutorial.</span></span>

<span data-ttu-id="f0864-190">`Install-Package` 명령은 스캐폴딩 엔진을 실행하는 데 필요한 도구를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-190">The `Install-Package` command installs the tooling required to run the scaffolding engine.</span></span>

<span data-ttu-id="f0864-191">`Add-Migration` 명령은 초기 데이터베이스 스키마를 만드는 코드를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-191">The `Add-Migration` command generates code to create the initial database schema.</span></span> <span data-ttu-id="f0864-192">스키마는 `DbContext`에 지정된 모델을 기반으로 합니다(*Models/MovieContext.cs* 파일에서).</span><span class="sxs-lookup"><span data-stu-id="f0864-192">The schema is based on the model specified in the `DbContext` (In the *Models/MovieContext.cs* file).</span></span> <span data-ttu-id="f0864-193">`Initial` 인수는 마이그레이션 이름을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-193">The `Initial` argument is used to name the migrations.</span></span> <span data-ttu-id="f0864-194">모든 이름을 사용할 수 있지만 일반적으로 마이그레이션을 설명하는 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-194">You can use any name, but by convention you choose a name that describes the migration.</span></span> <span data-ttu-id="f0864-195">자세한 내용은 [마이그레이션 소개](xref:data/ef-mvc/migrations#introduction-to-migrations)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0864-195">See [Introduction to migrations](xref:data/ef-mvc/migrations#introduction-to-migrations) for more information.</span></span>

<span data-ttu-id="f0864-196">`Update-Database` 명령은 데이터베이스를 만드는 *Migrations/{time-stamp}_InitialCreate.cs* 파일에서 `Up` 메서드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-196">The `Update-Database` command runs the `Up` method in the *Migrations/{time-stamp}_InitialCreate.cs* file, which creates the database.</span></span>

[!INCLUDE [model 4windows](~/includes/RP/model4Win.md)]

[!INCLUDE [model 4](~/includes/RP/model4tbl.md)]

::: moniker-end

<a name="test"></a>

### <a name="test-the-app"></a><span data-ttu-id="f0864-197">앱 테스트</span><span class="sxs-lookup"><span data-stu-id="f0864-197">Test the app</span></span>

* <span data-ttu-id="f0864-198">앱을 실행하고 브라우저에서 `/Movies`를 URL에 추가합니다(`http://localhost:port/movies`).</span><span class="sxs-lookup"><span data-stu-id="f0864-198">Run the app and append `/Movies` to the URL in the browser (`http://localhost:port/movies`).</span></span>
* <span data-ttu-id="f0864-199">**만들기** 링크를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-199">Test the **Create** link.</span></span>

  ![페이지 만들기](../../tutorials/razor-pages/model/_static/conan.png)

<a name="scaffold"></a>

* <span data-ttu-id="f0864-201">**편집**, **세부 정보** 및 **삭제** 링크를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-201">Test the **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="f0864-202">SQL 예외가 발생하는 경우 마이그레이션을 실행했는지와 데이터베이스를 업데이트했는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="f0864-202">If you get a SQL exception, verify you have run migrations and updated the database.</span></span>

<span data-ttu-id="f0864-203">다음 자습서에서는 스캐폴딩을 통해 만들어진 파일을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f0864-203">The next tutorial explains the files created by scaffolding.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f0864-204">[이전: 시작](xref:tutorials/razor-pages/razor-pages-start)
> [다음: 스캐폴드된 Razor 페이지](xref:tutorials/razor-pages/page)</span><span class="sxs-lookup"><span data-stu-id="f0864-204">[Previous: Get Started](xref:tutorials/razor-pages/razor-pages-start)
[Next: Scaffolded Razor Pages](xref:tutorials/razor-pages/page)</span></span>
