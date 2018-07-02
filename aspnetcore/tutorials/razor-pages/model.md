---
title: ASP.NET Core에서 Razor 페이지 앱에 모델 추가
author: rick-anderson
description: Entity Framework Core(EF Core)를 사용하여 데이터베이스에서 영화를 관리하기 위한 클래스를 추가하는 방법을 알아봅니다.
ms.author: riande
ms.date: 05/30/2018
uid: tutorials/razor-pages/model
ms.openlocfilehash: 508cca07fa96c20e228d2c55c9fb101f7fc3cb02
ms.sourcegitcommit: 79b756ea03eae77a716f500ef88253ee9b1464d2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/22/2018
ms.locfileid: "36327554"
---
# <a name="add-a-model-to-a-razor-pages-app-in-aspnet-core"></a><span data-ttu-id="216fc-103">ASP.NET Core에서 Razor 페이지 앱에 모델 추가</span><span class="sxs-lookup"><span data-stu-id="216fc-103">Add a model to a Razor Pages app in ASP.NET Core</span></span>

::: moniker range=">= aspnetcore-2.1"

[!INCLUDE [model1](~/includes/RP/model1.md)]

## <a name="add-a-data-model"></a><span data-ttu-id="216fc-104">데이터 모델 추가</span><span class="sxs-lookup"><span data-stu-id="216fc-104">Add a data model</span></span>

<span data-ttu-id="216fc-105">솔루션 탐색기에서 **RazorPagesMovie** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 폴더**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-105">In Solution Explorer, right-click the **RazorPagesMovie** project > **Add** > **New Folder**.</span></span> <span data-ttu-id="216fc-106">폴더 이름을 *Models*로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-106">Name the folder *Models*.</span></span>

<span data-ttu-id="216fc-107">*Models* 폴더를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-107">Right click the *Models* folder.</span></span> <span data-ttu-id="216fc-108">**추가** > **클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-108">Select **Add** > **Class**.</span></span> <span data-ttu-id="216fc-109">클래스 이름을 **Movie**로 지정하고 다음 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-109">Name the class **Movie** and add the following properties:</span></span>

<span data-ttu-id="216fc-110">`Movie` 클래스의 콘텐츠를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-110">Replace the contents of the `Movie` class with the following code:</span></span>

<span data-ttu-id="216fc-111">[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie21/Models/Movie1.cs?name=snippet)]</span><span class="sxs-lookup"><span data-stu-id="216fc-111">[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie21/Models/Movie1.cs?name=snippet)]</span></span>

## <a name="scaffold-the-movie-model"></a><span data-ttu-id="216fc-112">동영상 모델 스캐폴드</span><span class="sxs-lookup"><span data-stu-id="216fc-112">Scaffold the movie model</span></span>

<span data-ttu-id="216fc-113">이 섹션에서는 동영상 모델을 스캐폴 합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-113">In this section, the movie model is scaffolded.</span></span> <span data-ttu-id="216fc-114">즉, 스캐폴드 도구는 동영상 모델에서 CRUD(만들기, 읽기, 업데이트 및 삭제) 작업을 위한 페이지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-114">That is, the scaffolding tool produces pages for Create, Read, Update, and Delete (CRUD) operations for the movie model.</span></span>

<span data-ttu-id="216fc-115">*Pages/Movies* 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-115">Create a *Pages/Movies* folder:</span></span>

* <span data-ttu-id="216fc-116">**솔루션 탐색기**에서 *Pages* 폴더 > **추가** > **새 폴더**를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-116">In **Solution Explorer**, right click on the *Pages* folder > **Add** > **New Folder**.</span></span>
* <span data-ttu-id="216fc-117">폴더 이름을 *Movies*로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-117">Name the folder *Movies*</span></span>

<span data-ttu-id="216fc-118">**솔루션 탐색기**에서 *Pages/Movies* 폴더 > **추가** > **새 스캐폴드된 항목**을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-118">In **Solution Explorer**, right click on the *Pages/Movies* folder > **Add** > **New Scaffolded Item**.</span></span>

![이전 지침의 이미지입니다.](model/_static/sca.png)

<span data-ttu-id="216fc-120">**스캐폴드 추가** 대화 상자에서 **Entity Framework(CRUD)를 사용한 Razor Pages** > **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-120">In the **Add Scaffold** dialog, select **Razor Pages using Entity Framework (CRUD)** > **ADD**.</span></span>

![이전 지침의 이미지입니다.](model/_static/add_scaffold.png)

<span data-ttu-id="216fc-122">**Entity Framework(CRUD)를 사용하여 Razor Pages 추가** 대화 상자를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-122">Complete the **Add Razor Pages using Entity Framework (CRUD)** dialog:</span></span>

* <span data-ttu-id="216fc-123">**모델 클래스** 드롭다운에서 **동영상(RazorPagesMovie.Models)** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-123">In the **Model class** drop down, select **Movie (RazorPagesMovie.Models)**.</span></span>
* <span data-ttu-id="216fc-124">**데이터 컨텍스트 클래스** 행에서 **+** 기호를 선택하고 생성된 이름인 **RazorPagesMovie.Models.RazorPagesMovieContext**를 수용합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-124">In the **Data context class** row, select the **+** (plus) sign and accept the generated name **RazorPagesMovie.Models.RazorPagesMovieContext**.</span></span>
* <span data-ttu-id="216fc-125">**데이터 컨텍스트 클래스** 드롭다운에서 **RazorPagesMovie.Models.RazorPagesMovieContext**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-125">In the **Data context class** drop down,  select **RazorPagesMovie.Models.RazorPagesMovieContext**</span></span>
* <span data-ttu-id="216fc-126">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-126">Select **Add**.</span></span>

![이전 지침의 이미지입니다.](model/_static/arp.png)

<a name="pmc"></a>
## <a name="perform-initial-migration"></a><span data-ttu-id="216fc-128">초기 마이그레이션 수행</span><span class="sxs-lookup"><span data-stu-id="216fc-128">Perform initial migration</span></span>

<span data-ttu-id="216fc-129">이 섹션에서는 PMC(패키지 관리자 콘솔)를 사용하여 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-129">In this section, you use the Package Manager Console (PMC) to:</span></span>

* <span data-ttu-id="216fc-130">초기 마이그레이션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-130">Add an initial migration.</span></span>
* <span data-ttu-id="216fc-131">초기 마이그레이션을 사용하여 데이터베이스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-131">Update the database with the initial migration.</span></span>

<span data-ttu-id="216fc-132">**도구** 메뉴에서 **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-132">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span>

  ![PMC 메뉴](../first-mvc-app/adding-model/_static/pmc.png)

<span data-ttu-id="216fc-134">PMC에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-134">In the PMC, enter the following commands:</span></span>

```PMC
Add-Migration Initial
Update-Database
```

<span data-ttu-id="216fc-135">또는 다음 .NET Core CLI 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-135">Alternatively, the following .NET Core CLI commands can be used:</span></span>

```console
dotnet ef migrations add Initial
dotnet ef database update
```

<span data-ttu-id="216fc-136">다음과 같은 경고 메시지를 무시합니다. 해당 문제를 다음 자습서에서 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-136">Ignore the following warning message, you fix that in the next tutorial:</span></span>

`Microsoft.EntityFrameworkCore.Model.Validation[30000]`

      *No type was specified for the decimal column 'Price' on entity type 'Movie'. This will cause values to be silently truncated if they do not fit in the default precision and scale. Explicitly specify the SQL server column type that can accommodate all the values using 'ForHasColumnType()'.*

<span data-ttu-id="216fc-137">`Add-Migration` 명령은 초기 데이터베이스 스키마를 만드는 코드를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-137">The `Add-Migration` command generates code to create the initial database schema.</span></span> <span data-ttu-id="216fc-138">스키마는 `RazorPagesMovieContext`에 지정된 모델을 기반으로 합니다(*Data/RazorPagesMovieContext.cs* 파일).</span><span class="sxs-lookup"><span data-stu-id="216fc-138">The schema is based on the model specified in the `RazorPagesMovieContext` (In the *Data/RazorPagesMovieContext.cs* file).</span></span> <span data-ttu-id="216fc-139">`Initial` 인수는 마이그레이션 이름을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-139">The `Initial` argument is used to name the migrations.</span></span> <span data-ttu-id="216fc-140">모든 이름을 사용할 수 있지만 일반적으로 마이그레이션을 설명하는 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-140">You can use any name, but by convention you choose a name that describes the migration.</span></span> <span data-ttu-id="216fc-141">자세한 내용은 [마이그레이션 소개](xref:data/ef-mvc/migrations#introduction-to-migrations)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="216fc-141">See [Introduction to migrations](xref:data/ef-mvc/migrations#introduction-to-migrations) for more information.</span></span>

<span data-ttu-id="216fc-142">`Update-Database` 명령은 데이터베이스를 만드는 *Migrations/{time-stamp}_InitialCreate.cs* 파일에서 `Up` 메서드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-142">The `Update-Database` command runs the `Up` method in the *Migrations/{time-stamp}_InitialCreate.cs* file, which creates the database.</span></span>

<span data-ttu-id="216fc-143">오류가 표시될 경우:</span><span class="sxs-lookup"><span data-stu-id="216fc-143">If you get the error:</span></span>

<span data-ttu-id="216fc-144">SqlException: 로그인에서 요청한 "RazorPagesMovieContext-GUID" 데이터베이스를 열 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-144">SqlException: Cannot open database "RazorPagesMovieContext-GUID" requested by the login.</span></span> <span data-ttu-id="216fc-145">로그인에 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-145">The login failed.</span></span>
<span data-ttu-id="216fc-146">'User-name' 사용자에 대한 로그인에 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-146">Login failed for user 'User-name'.</span></span>

<span data-ttu-id="216fc-147">[마이그레이션 단계](#pmc)를 누락했습니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-147">You missed the [migrations step](#pmc).</span></span>
::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!INCLUDE [model1](~/includes/RP/model1.md)]

## <a name="add-a-data-model"></a><span data-ttu-id="216fc-148">데이터 모델 추가</span><span class="sxs-lookup"><span data-stu-id="216fc-148">Add a data model</span></span>

<span data-ttu-id="216fc-149">솔루션 탐색기에서 **RazorPagesMovie** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 폴더**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-149">In Solution Explorer, right-click the **RazorPagesMovie** project > **Add** > **New Folder**.</span></span> <span data-ttu-id="216fc-150">폴더 이름을 *Models*로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-150">Name the folder *Models*.</span></span>

<span data-ttu-id="216fc-151">*Models* 폴더를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-151">Right click the *Models* folder.</span></span> <span data-ttu-id="216fc-152">**추가** > **클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-152">Select **Add** > **Class**.</span></span> <span data-ttu-id="216fc-153">클래스 이름을 **Movie**로 지정하고 다음 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-153">Name the class **Movie** and add the following properties:</span></span>

[!INCLUDE [model 2](~/includes/RP/model2.md)]

<a name="cs"></a>
### <a name="add-a-database-connection-string"></a><span data-ttu-id="216fc-154">데이터베이스 연결 문자열 추가</span><span class="sxs-lookup"><span data-stu-id="216fc-154">Add a database connection string</span></span>

<span data-ttu-id="216fc-155">*appsettings.json* 파일에 연결 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-155">Add a connection string to the *appsettings.json* file.</span></span>

<span data-ttu-id="216fc-156">[!code-json[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/appsettings.json?highlight=8-10)]</span><span class="sxs-lookup"><span data-stu-id="216fc-156">[!code-json[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/appsettings.json?highlight=8-10)]</span></span>

<a name="reg"></a>
###  <a name="register-the-database-context"></a><span data-ttu-id="216fc-157">데이터베이스 컨텍스트 등록</span><span class="sxs-lookup"><span data-stu-id="216fc-157">Register the database context</span></span>

<span data-ttu-id="216fc-158">[스타트업 클래스(*Startup.cs*)의 ConfigureServices 메서드](xref:fundamentals/startup#the-startup-class)에서 [종속성 주입](xref:fundamentals/dependency-injection) 컨테이너에 데이터베이스 컨텍스트를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-158">Register the database context with the [dependency injection](xref:fundamentals/dependency-injection) container in the [ConfigureServices method of the Startup class](xref:fundamentals/startup#the-startup-class) (*Startup.cs*):</span></span>

<span data-ttu-id="216fc-159">[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Startup.cs?name=snippet_ConfigureServices&highlight=3-5,7-9)]</span><span class="sxs-lookup"><span data-stu-id="216fc-159">[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Startup.cs?name=snippet_ConfigureServices&highlight=3-5,7-9)]</span></span>

<span data-ttu-id="216fc-160">프로젝트를 빌드하여 오류가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-160">Build the project to verify you don't have any errors.</span></span>

<a name="pmc"></a>
## <a name="add-scaffold-tooling-and-perform-initial-migration"></a><span data-ttu-id="216fc-161">스캐폴드 도구 추가 및 초기 마이그레이션 수행</span><span class="sxs-lookup"><span data-stu-id="216fc-161">Add scaffold tooling and perform initial migration</span></span>

<span data-ttu-id="216fc-162">이 섹션에서는 PMC(패키지 관리자 콘솔)를 사용하여 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-162">In this section, you use the Package Manager Console (PMC) to:</span></span>

* <span data-ttu-id="216fc-163">Visual Studio 웹 코드 생성 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-163">Add the Visual Studio web code generation package.</span></span> <span data-ttu-id="216fc-164">스캐폴딩 엔진을 실행하려면 이 패키지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-164">This package is required to run the scaffolding engine.</span></span>
* <span data-ttu-id="216fc-165">초기 마이그레이션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-165">Add an initial migration.</span></span>
* <span data-ttu-id="216fc-166">초기 마이그레이션을 사용하여 데이터베이스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-166">Update the database with the initial migration.</span></span>

<span data-ttu-id="216fc-167">**도구** 메뉴에서 **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-167">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span>

  ![PMC 메뉴](../first-mvc-app/adding-model/_static/pmc.png)

<span data-ttu-id="216fc-169">PMC에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-169">In the PMC, enter the following commands:</span></span>

```powershell
Install-Package Microsoft.VisualStudio.Web.CodeGeneration.Design -Version 2.0.3
Add-Migration Initial
Update-Database
```

<span data-ttu-id="216fc-170">또는 다음 .NET Core CLI 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-170">Alternatively, the following .NET Core CLI commands can be used:</span></span>

```console
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet ef migrations add Initial
dotnet ef database update
```

<span data-ttu-id="216fc-171">다음과 같은 메시지를 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-171">Ignore the following message:</span></span>

    `Microsoft.EntityFrameworkCore.Model.Validation[30000]`

      *No type was specified for the decimal column 'Price' on entity type 'Movie'. This will cause values to be silently truncated if they do not fit in the default precision and scale. Explicitly specify the SQL server column type that can accommodate all the values using 'ForHasColumnType()'*

<span data-ttu-id="216fc-172">다음 자습서에서 해당 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-172">You fix that in the next tutorial.</span></span>

<span data-ttu-id="216fc-173">`Install-Package` 명령은 스캐폴딩 엔진을 실행하는 데 필요한 도구를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-173">The `Install-Package` command installs the tooling required to run the scaffolding engine.</span></span>

<span data-ttu-id="216fc-174">`Add-Migration` 명령은 초기 데이터베이스 스키마를 만드는 코드를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-174">The `Add-Migration` command generates code to create the initial database schema.</span></span> <span data-ttu-id="216fc-175">스키마는 `DbContext`에 지정된 모델을 기반으로 합니다(*Models/MovieContext.cs* 파일에서).</span><span class="sxs-lookup"><span data-stu-id="216fc-175">The schema is based on the model specified in the `DbContext` (In the *Models/MovieContext.cs* file).</span></span> <span data-ttu-id="216fc-176">`Initial` 인수는 마이그레이션 이름을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-176">The `Initial` argument is used to name the migrations.</span></span> <span data-ttu-id="216fc-177">모든 이름을 사용할 수 있지만 일반적으로 마이그레이션을 설명하는 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-177">You can use any name, but by convention you choose a name that describes the migration.</span></span> <span data-ttu-id="216fc-178">자세한 내용은 [마이그레이션 소개](xref:data/ef-mvc/migrations#introduction-to-migrations)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="216fc-178">See [Introduction to migrations](xref:data/ef-mvc/migrations#introduction-to-migrations) for more information.</span></span>

<span data-ttu-id="216fc-179">`Update-Database` 명령은 데이터베이스를 만드는 *Migrations/{time-stamp}_InitialCreate.cs* 파일에서 `Up` 메서드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-179">The `Update-Database` command runs the `Up` method in the *Migrations/{time-stamp}_InitialCreate.cs* file, which creates the database.</span></span>

[!INCLUDE [model 4windows](~/includes/RP/model4Win.md)]

[!INCLUDE [model 4](~/includes/RP/model4tbl.md)]

::: moniker-end

<a name="test"></a>

### <a name="test-the-app"></a><span data-ttu-id="216fc-180">앱 테스트</span><span class="sxs-lookup"><span data-stu-id="216fc-180">Test the app</span></span>

* <span data-ttu-id="216fc-181">앱을 실행하고 브라우저에서 `/Movies`를 URL에 추가합니다(`http://localhost:port/movies`).</span><span class="sxs-lookup"><span data-stu-id="216fc-181">Run the app and append `/Movies` to the URL in the browser (`http://localhost:port/movies`).</span></span>
* <span data-ttu-id="216fc-182">**만들기** 링크를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-182">Test the **Create** link.</span></span>

  ![페이지 만들기](../../tutorials/razor-pages/model/_static/conan.png)

<a name="scaffold"></a>

* <span data-ttu-id="216fc-184">**편집**, **세부 정보** 및 **삭제** 링크를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-184">Test the **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="216fc-185">SQL 예외가 발생하는 경우 마이그레이션을 실행했는지와 데이터베이스를 업데이트했는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="216fc-185">If you get a SQL exception, verify you have run migrations and updated the database.</span></span>

<span data-ttu-id="216fc-186">다음 자습서에서는 스캐폴딩을 통해 만들어진 파일을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="216fc-186">The next tutorial explains the files created by scaffolding.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="216fc-187">[이전: 시작](xref:tutorials/razor-pages/razor-pages-start)
> [다음: 스캐폴드된 Razor 페이지](xref:tutorials/razor-pages/page)</span><span class="sxs-lookup"><span data-stu-id="216fc-187">[Previous: Get Started](xref:tutorials/razor-pages/razor-pages-start)
[Next: Scaffolded Razor Pages](xref:tutorials/razor-pages/page)</span></span>    
