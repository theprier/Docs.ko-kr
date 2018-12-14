---
title: ASP.NET Core에서 Razor 페이지 앱에 모델 추가
author: rick-anderson
description: Entity Framework Core(EF Core)를 사용하여 데이터베이스에서 영화를 관리하기 위한 클래스를 추가하는 방법을 알아봅니다.
ms.author: riande
monikerRange: '>= aspnetcore-2.2'
ms.date: 12/3/2018
uid: tutorials/razor-pages/model
ms.openlocfilehash: 91fee1db820493be671fecaee3cfb4c1b7df8bd3
ms.sourcegitcommit: 49faca2644590fc081d86db46ea5e29edfc28b7b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/09/2018
ms.locfileid: "53121365"
---
# <a name="add-a-model-to-a-razor-pages-app-in-aspnet-core"></a><span data-ttu-id="2e972-103">ASP.NET Core에서 Razor 페이지 앱에 모델 추가</span><span class="sxs-lookup"><span data-stu-id="2e972-103">Add a model to a Razor Pages app in ASP.NET Core</span></span>

<span data-ttu-id="2e972-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="2e972-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE[](~/includes/rp/download.md)]

<span data-ttu-id="2e972-105">이 섹션에서는 데이터베이스에서 동영상을 관리하기 위한 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-105">In this section, classes are added for managing movies in a database.</span></span> <span data-ttu-id="2e972-106">이러한 클래스를 EF Core([Entity Framework Core](/ef/core))와 함께 사용하여 데이터베이스 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-106">These classes are used with [Entity Framework Core](/ef/core) (EF Core) to work with a database.</span></span> <span data-ttu-id="2e972-107">EF Core는 데이터 액세스 코드를 간소화하는 ORM(개체-관계형 매핑) 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-107">EF Core is an object-relational mapping (ORM) framework that simplifies data access code.</span></span>

<span data-ttu-id="2e972-108">모델 클래스는 EF Core에 대한 종속성이 없으므로 POCO(Plain Old CLR Object) 클래스로 알려져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-108">The model classes are known as POCO classes (from "plain-old CLR objects") because they don't have any dependency on EF Core.</span></span> <span data-ttu-id="2e972-109">이 클래스는 데이터베이스에 저장되는 데이터의 속성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-109">They define the properties of the data that are stored in the database.</span></span>

<span data-ttu-id="2e972-110">샘플을 [보거나 다운로드합니다](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages-start/sample/).</span><span class="sxs-lookup"><span data-stu-id="2e972-110">[View or download](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/razor-pages-start/sample/) sample.</span></span>

## <a name="add-a-data-model"></a><span data-ttu-id="2e972-111">데이터 모델 추가</span><span class="sxs-lookup"><span data-stu-id="2e972-111">Add a data model</span></span>

<!-- VS -------------------------->

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="2e972-112">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2e972-112">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="2e972-113">**RazorPagesMovie** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 폴더**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-113">Right-click the **RazorPagesMovie** project > **Add** > **New Folder**.</span></span> <span data-ttu-id="2e972-114">폴더 이름을 *Models*로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-114">Name the folder *Models*.</span></span>

<span data-ttu-id="2e972-115">*Models* 폴더를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-115">Right click the *Models* folder.</span></span> <span data-ttu-id="2e972-116">**추가** > **클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-116">Select **Add** > **Class**.</span></span> <span data-ttu-id="2e972-117">클래스의 이름을 **동영상**으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-117">Name the class **Movie**.</span></span>

[!INCLUDE [model 1b](~/includes/RP/model1b.md)]

<!-- Code -------------------------->

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="2e972-118">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2e972-118">Visual Studio Code</span></span>](#tab/visual-studio-code)

* <span data-ttu-id="2e972-119">*Models* 폴더를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-119">Add a folder named *Models*.</span></span>
* <span data-ttu-id="2e972-120">*Models* 폴더에 *Movie.cs* 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-120">Add a class to the *Models* folder named *Movie.cs*.</span></span>

[!INCLUDE [model 1b](~/includes/RP/model1b.md)]

[!INCLUDE [model 2](~/includes/RP/model2.md)]

<!-- Mac -------------------------->
# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="2e972-121">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="2e972-121">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* <span data-ttu-id="2e972-122">솔루션 탐색기에서 **RazorPagesMovie** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 폴더**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-122">In Solution Explorer, right-click the **RazorPagesMovie** project, and then select **Add** > **New Folder**.</span></span> <span data-ttu-id="2e972-123">폴더 이름을 *Models*로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-123">Name the folder *Models*.</span></span>
* <span data-ttu-id="2e972-124">*Models* 폴더를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 파일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-124">Right-click the *Models* folder, and then select **Add** > **New File**.</span></span>
* <span data-ttu-id="2e972-125">**새 파일** 대화 상자에서:</span><span class="sxs-lookup"><span data-stu-id="2e972-125">In the **New File** dialog:</span></span>

  * <span data-ttu-id="2e972-126">왼쪽 창에서 **일반**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-126">Select **General** in the left pane.</span></span>
  * <span data-ttu-id="2e972-127">가운데 창에서 **빈 클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-127">Select **Empty Class** in the center pain.</span></span>
  * <span data-ttu-id="2e972-128">클래스 이름을 **Movie**로 지정하고 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-128">Name the class **Movie** and select **New**.</span></span>

[!INCLUDE [model 1b](~/includes/RP/model1b.md)]

[!INCLUDE [model 2](~/includes/RP/model2.md)]

<!-- End of VS tabs -->

---

<span data-ttu-id="2e972-129">프로젝트를 빌드하여 컴파일 오류가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-129">Build the project to verify there are no compilation errors.</span></span>

## <a name="scaffold-the-movie-model"></a><span data-ttu-id="2e972-130">동영상 모델 스캐폴드</span><span class="sxs-lookup"><span data-stu-id="2e972-130">Scaffold the movie model</span></span>

<span data-ttu-id="2e972-131">이 섹션에서는 동영상 모델을 스캐폴 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-131">In this section, the movie model is scaffolded.</span></span> <span data-ttu-id="2e972-132">즉, 스캐폴드 도구는 동영상 모델에서 CRUD(만들기, 읽기, 업데이트 및 삭제) 작업을 위한 페이지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-132">That is, the scaffolding tool produces pages for Create, Read, Update, and Delete (CRUD) operations for the movie model.</span></span>

<!-- VS -------------------------->

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="2e972-133">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2e972-133">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="2e972-134">*Pages/Movies* 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-134">Create a *Pages/Movies* folder:</span></span>

* <span data-ttu-id="2e972-135">*페이지* 폴더를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 폴더**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-135">Right click on the *Pages* folder > **Add** > **New Folder**.</span></span>
* <span data-ttu-id="2e972-136">폴더 이름을 *Movies*로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-136">Name the folder *Movies*</span></span>

<span data-ttu-id="2e972-137">*페이지/동영상* 폴더를 마우스 오른쪽 단추로 클릭하고 **추가** > **스캐폴드된 새 항목**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-137">Right click on the *Pages/Movies* folder > **Add** > **New Scaffolded Item**.</span></span>

![이전 지침의 이미지입니다.](model/_static/sca.png)

<span data-ttu-id="2e972-139">**스캐폴드 추가** 대화 상자에서 **Entity Framework(CRUD)를 사용한 Razor Pages** > **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-139">In the **Add Scaffold** dialog, select **Razor Pages using Entity Framework (CRUD)** > **Add**.</span></span>

![이전 지침의 이미지입니다.](model/_static/add_scaffold.png)

<span data-ttu-id="2e972-141">**Entity Framework(CRUD)를 사용하여 Razor Pages 추가** 대화 상자를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-141">Complete the **Add Razor Pages using Entity Framework (CRUD)** dialog:</span></span>

* <span data-ttu-id="2e972-142">**모델 클래스** 드롭다운에서 **동영상(RazorPagesMovie.Models)** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-142">In the **Model class** drop down, select **Movie (RazorPagesMovie.Models)**.</span></span>
* <span data-ttu-id="2e972-143">**데이터 컨텍스트 클래스** 행에서 **+** 기호를 선택하고 생성된 이름인 **RazorPagesMovie.Models.RazorPagesMovieContext**를 수용합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-143">In the **Data context class** row, select the **+** (plus) sign and accept the generated name **RazorPagesMovie.Models.RazorPagesMovieContext**.</span></span>
* <span data-ttu-id="2e972-144">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-144">Select **Add**.</span></span>

![이전 지침의 이미지입니다.](model/_static/arp.png)

<span data-ttu-id="2e972-146">*appsettings.json* 파일을 로컬 데이터베이스에 연결하는 데 사용된 연결 문자열로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-146">The *appsettings.json* file is updated with the connection string used to connect to a local database.</span></span>

<!-- Code -------------------------->

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="2e972-147">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2e972-147">Visual Studio Code</span></span>](#tab/visual-studio-code)

<!--  Until https://github.com/aspnet/Scaffolding/issues/582 is fixed windows needs backslash or the namespace is namespace RazorPagesMovie.Pages_Movies rather than namespace RazorPagesMovie.Pages.Movies
-->

* <span data-ttu-id="2e972-148">프로젝트 디렉터리(*Program.cs*, *Startup.cs* 및 *.csproj* 파일이 포함된 디렉터리)에서 명령 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-148">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>
* <span data-ttu-id="2e972-149">스캐폴딩 도구를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-149">Install the scaffolding tool:</span></span>

  ```console
   dotnet tool install --global dotnet-aspnet-codegenerator
   ```

* <span data-ttu-id="2e972-150">**Windows**: 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-150">**For Windows**: Run the following command:</span></span>

  ```console
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages\Movies --referenceScriptLibraries
  ```

* <span data-ttu-id="2e972-151">**macOS 및 Linux**: 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-151">**For macOS and Linux**: Run the following command:</span></span>

  ```console
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages/Movies --referenceScriptLibraries
  ```

[!INCLUDE [explains scaffold gen params](~/includes/RP/model4.md)]

<!-- Mac -------------------------->

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="2e972-152">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="2e972-152">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* <span data-ttu-id="2e972-153">프로젝트 디렉터리(*Program.cs*, *Startup.cs* 및 *.csproj* 파일이 포함된 디렉터리)에서 명령 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-153">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>
* <span data-ttu-id="2e972-154">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-154">Run the following command:</span></span>

  ```console
  dotnet aspnet-codegenerator razorpage -m Movie -dc RazorPagesMovieContext -udl -outDir Pages/Movies --referenceScriptLibraries
  ```

[!INCLUDE [explains scaffold gen params](~/includes/RP/model4.md)]

---

<span data-ttu-id="2e972-155">스캐폴드 프로세스는 다음 파일을 생성하고 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-155">The scaffold process creates and updates the following files:</span></span>

### <a name="files-created"></a><span data-ttu-id="2e972-156">생성된 파일</span><span class="sxs-lookup"><span data-stu-id="2e972-156">Files created</span></span>

* <span data-ttu-id="2e972-157">*페이지/동영상*: 만들기, 삭제, 세부 정보, 편집 및 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-157">*Pages/Movies*: Create, Delete, Details, Edit, and Index.</span></span>
* <span data-ttu-id="2e972-158">*Data/RazorPagesMovieContext.cs*</span><span class="sxs-lookup"><span data-stu-id="2e972-158">*Data/RazorPagesMovieContext.cs*</span></span>

### <a name="file-updated"></a><span data-ttu-id="2e972-159">파일 업데이트됨</span><span class="sxs-lookup"><span data-stu-id="2e972-159">File updated</span></span>

* <span data-ttu-id="2e972-160">*Startup.cs*</span><span class="sxs-lookup"><span data-stu-id="2e972-160">*Startup.cs*</span></span>

<span data-ttu-id="2e972-161">생성되고 업데이트된 파일은 다음 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-161">The created and updated files are explained in the next section.</span></span>

<a name="pmc"></a>

## <a name="initial-migration"></a><span data-ttu-id="2e972-162">초기 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="2e972-162">Initial migration</span></span>

<!-- VS -------------------------->

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="2e972-163">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2e972-163">Visual Studio</span></span>](#tab/visual-studio)

<!-- VS -------------------------->

<span data-ttu-id="2e972-164">이 섹션에서는 PMC(패키지 관리자 콘솔)를 사용하여 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-164">In this section, the Package Manager Console (PMC) is used to:</span></span>

* <span data-ttu-id="2e972-165">초기 마이그레이션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-165">Add an initial migration.</span></span>
* <span data-ttu-id="2e972-166">초기 마이그레이션을 사용하여 데이터베이스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-166">Update the database with the initial migration.</span></span>

<span data-ttu-id="2e972-167">**도구** 메뉴에서 **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-167">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span>

  ![PMC 메뉴](../first-mvc-app/adding-model/_static/pmc.png)

<span data-ttu-id="2e972-169">PMC에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-169">In the PMC, enter the following commands:</span></span>

```PMC
Add-Migration Initial
Update-Database
```

<!-- Code -------------------------->

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="2e972-170">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2e972-170">Visual Studio Code</span></span>](#tab/visual-studio-code)

<!-- Mac -------------------------->

[!INCLUDE [initial migration](~/includes/RP/model3.md)]

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="2e972-171">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="2e972-171">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

[!INCLUDE [initial migration](~/includes/RP/model3.md)]

---  
<!-- End of VS tabs -->

<span data-ttu-id="2e972-172">`ef migrations add InitialCreate` 명령은 초기 데이터베이스 스키마를 만드는 코드를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-172">The `ef migrations add InitialCreate` command generates code to create the initial database schema.</span></span> <span data-ttu-id="2e972-173">스키마는 `DbContext`에 지정된 모델을 기반으로 합니다(*Models/RazorPagesMovieContext.cs* 파일).</span><span class="sxs-lookup"><span data-stu-id="2e972-173">The schema is based on the model specified in the `DbContext` (In the *Models/RazorPagesMovieContext.cs* file).</span></span> <span data-ttu-id="2e972-174">`InitialCreate` 인수는 마이그레이션 이름을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-174">The `InitialCreate` argument is used to name the migrations.</span></span> <span data-ttu-id="2e972-175">모든 이름을 사용할 수 있지만 규칙에 따라 마이그레이션을 설명하는 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-175">Any name can be used, but by convention a name is selected that describes the migration.</span></span>

<span data-ttu-id="2e972-176">`ef database update` 명령은 *Migrations/\<time-stamp>_InitialCreate.cs* 파일에서 `Up` 메서드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-176">The `ef database update` command runs the `Up` method in the *Migrations/\<time-stamp>_InitialCreate.cs* file.</span></span> <span data-ttu-id="2e972-177">`Up` 메서드는 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-177">The `Up` method creates the database.</span></span>

<!-- VS -------------------------->

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="2e972-178">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2e972-178">Visual Studio</span></span>](#tab/visual-studio)

## <a name="examine-the-context-registered-with-dependency-injection"></a><span data-ttu-id="2e972-179">종속성 주입을 사용하여 등록된 컨텍스트 검사</span><span class="sxs-lookup"><span data-stu-id="2e972-179">Examine the context registered with dependency injection</span></span>

<span data-ttu-id="2e972-180">ASP.NET Core는 [종속성 주입](xref:fundamentals/dependency-injection)을 사용하여 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-180">ASP.NET Core is built with [dependency injection](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="2e972-181">서비스(예: EF Core DB 컨텍스트)는 응용 프로그램 시작 중에 종속성 주입에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-181">Services (such as the EF Core DB context) are registered with dependency injection during application startup.</span></span> <span data-ttu-id="2e972-182">이러한 서비스(예: Razor 페이지)가 필요한 구성 요소에는 생성자 매개 변수를 통해 이러한 서비스가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-182">Components that require these services (such as Razor Pages) are provided these services via constructor parameters.</span></span> <span data-ttu-id="2e972-183">DB 컨텍스트 인스턴스를 가져오는 생성자 코드는 자습서 뒷부분에 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-183">The constructor code that gets a DB context instance is shown later in the tutorial.</span></span>

<span data-ttu-id="2e972-184">스캐폴딩 도구는 자동으로 DB 컨텍스트를 생성하고 종속성 주입 컨테이너에 등록했습니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-184">The scaffolding tool automatically created a DB context and registered it with the dependency injection container.</span></span>

<span data-ttu-id="2e972-185">`Startup.ConfigureServices` 메서드를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-185">Examine the `Startup.ConfigureServices` method.</span></span> <span data-ttu-id="2e972-186">강조 표시된 줄은 스캐폴더에서 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-186">The highlighted line was added by the scaffolder:</span></span>

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie22/Startup.cs?name=snippet_ConfigureServices&highlight=15-18)]

<span data-ttu-id="2e972-187">`RazorPagesMovieContext`는 `Movie` 모델에 대한 EF Core 기능(만들기, 읽기, 업데이트, 삭제 등)을 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-187">The `RazorPagesMovieContext` coordinates EF Core functionality (Create, Read, Update, Delete, etc.) for the `Movie` model.</span></span> <span data-ttu-id="2e972-188">데이터 컨텍스트(`RazorPagesMovieContext`)는 [Microsoft.EntityFrameworkCore.DbContext](/dotnet/api/microsoft.entityframeworkcore.dbcontext)에서 파생됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-188">The data context (`RazorPagesMovieContext`) is derived from [Microsoft.EntityFrameworkCore.DbContext](/dotnet/api/microsoft.entityframeworkcore.dbcontext).</span></span> <span data-ttu-id="2e972-189">데이터 컨텍스트는 데이터 모델에 포함되는 엔터티를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-189">The data context specifies which entities are included in the data model.</span></span>

[!code-csharp[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Data/RazorPagesMovieContext.cs)]

<span data-ttu-id="2e972-190">이전 코드에서는 엔터티 세트에 대해 [DbSet/\<Movie>](/dotnet/api/microsoft.entityframeworkcore.dbset-1) 속성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-190">The preceding code creates a [DbSet/\<Movie>](/dotnet/api/microsoft.entityframeworkcore.dbset-1) property for the entity set.</span></span> <span data-ttu-id="2e972-191">Entity Framework 용어에서 엔터티 집합은 일반적으로 데이터베이스 테이블에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-191">In Entity Framework terminology, an entity set typically corresponds to a database table.</span></span> <span data-ttu-id="2e972-192">엔터티는 테이블의 행에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-192">An entity corresponds to a row in the table.</span></span>

<span data-ttu-id="2e972-193">[DbContextOptions](/dotnet/api/microsoft.entityframeworkcore.dbcontextoptions) 개체에서 메서드를 호출하여 연결 문자열의 이름을 컨텍스트에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-193">The name of the connection string is passed in to the context by calling a method on a [DbContextOptions](/dotnet/api/microsoft.entityframeworkcore.dbcontextoptions) object.</span></span> <span data-ttu-id="2e972-194">로컬 개발의 경우 [ASP.NET Core 구성 시스템](xref:fundamentals/configuration/index)은 *appsettings.json* 파일에서 연결 문자열을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-194">For local development, the [ASP.NET Core configuration system](xref:fundamentals/configuration/index) reads the connection string from the *appsettings.json* file.</span></span>
<!-- Code -------------------------->

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="2e972-195">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2e972-195">Visual Studio Code</span></span>](#tab/visual-studio-code)

<!-- Mac -------------------------->

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="2e972-196">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="2e972-196">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

<!-- End of VS tabs -->

---

<span data-ttu-id="2e972-197">`Add-Migration` 명령은 초기 데이터베이스 스키마를 만드는 코드를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-197">The `Add-Migration` command generates code to create the initial database schema.</span></span> <span data-ttu-id="2e972-198">스키마는 `RazorPagesMovieContext`에 지정된 모델을 기반으로 합니다(*Data/RazorPagesMovieContext.cs* 파일).</span><span class="sxs-lookup"><span data-stu-id="2e972-198">The schema is based on the model specified in the `RazorPagesMovieContext` (In the *Data/RazorPagesMovieContext.cs* file).</span></span> <span data-ttu-id="2e972-199">`Initial` 인수는 마이그레이션 이름을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-199">The `Initial` argument is used to name the migrations.</span></span> <span data-ttu-id="2e972-200">모든 이름을 사용할 수 있지만 규칙에 따라 마이그레이션을 설명하는 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-200">Any name can be used, but by convention a name that describes the migration is used.</span></span> <span data-ttu-id="2e972-201">자세한 내용은 [마이그레이션 소개](xref:data/ef-mvc/migrations#introduction-to-migrations)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2e972-201">See [Introduction to migrations](xref:data/ef-mvc/migrations#introduction-to-migrations) for more information.</span></span>

<span data-ttu-id="2e972-202">`Update-Database` 명령은 데이터베이스를 만드는 *Migrations/{time-stamp}_InitialCreate.cs* 파일에서 `Up` 메서드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-202">The `Update-Database` command runs the `Up` method in the *Migrations/{time-stamp}_InitialCreate.cs* file, which creates the database.</span></span>

<a name="test"></a>

### <a name="test-the-app"></a><span data-ttu-id="2e972-203">앱 테스트</span><span class="sxs-lookup"><span data-stu-id="2e972-203">Test the app</span></span>

* <span data-ttu-id="2e972-204">앱을 실행하고 브라우저에서 `/Movies`를 URL에 추가합니다(`http://localhost:port/movies`).</span><span class="sxs-lookup"><span data-stu-id="2e972-204">Run the app and append `/Movies` to the URL in the browser (`http://localhost:port/movies`).</span></span>

<span data-ttu-id="2e972-205">오류가 표시될 경우:</span><span class="sxs-lookup"><span data-stu-id="2e972-205">If you get the error:</span></span>

```console
SqlException: Cannot open database "RazorPagesMovieContext-GUID" requested by the login. The login failed.
Login failed for user 'User-name'.
```

<span data-ttu-id="2e972-206">[마이그레이션 단계](#pmc)를 누락했습니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-206">You missed the [migrations step](#pmc).</span></span>

* <span data-ttu-id="2e972-207">**만들기** 링크를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-207">Test the **Create** link.</span></span>

  ![페이지 만들기](model/_static/conan.png)
  
  > [!NOTE]
  > <span data-ttu-id="2e972-209">`Price` 필드에는 소수점을 입력하지 못할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-209">You may not be able to enter decimal commas in the `Price` field.</span></span> <span data-ttu-id="2e972-210">소수점으로 쉼표(",")를 사용하는 영어가 아닌 로캘 및 미국 영어가 아닌 날짜 형식에 대해 [jQuery 유효성 검사](https://jqueryvalidation.org/)를 지원하려면 앱을 글로벌화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-210">To support [jQuery validation](https://jqueryvalidation.org/) for non-English locales that use a comma (",") for a decimal point and for non US-English date formats, the app must be globalized.</span></span> <span data-ttu-id="2e972-211">세계화 지침은 [이 GitHub 문제](https://github.com/aspnet/Docs/issues/4076#issuecomment-326590420)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2e972-211">For globalization instructions, see [this GitHub issue](https://github.com/aspnet/Docs/issues/4076#issuecomment-326590420).</span></span>

* <span data-ttu-id="2e972-212">**편집**, **세부 정보** 및 **삭제** 링크를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-212">Test the **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="2e972-213">다음 자습서에서는 스캐폴딩을 통해 만들어진 파일을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2e972-213">The next tutorial explains the files created by scaffolding.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2e972-214">[이전: 시작](xref:tutorials/razor-pages/razor-pages-start)
> [다음: 스캐폴드된 Razor 페이지](xref:tutorials/razor-pages/page)</span><span class="sxs-lookup"><span data-stu-id="2e972-214">[Previous: Get Started](xref:tutorials/razor-pages/razor-pages-start)
[Next: Scaffolded Razor Pages](xref:tutorials/razor-pages/page)</span></span>
