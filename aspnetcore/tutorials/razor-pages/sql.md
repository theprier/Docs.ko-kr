---
title: SQL Server LocalDB 및 ASP.NET Core 사용
author: rick-anderson
description: SQL Server LocalDB 및 ASP.NET Core 사용을 설명합니다.
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 08/07/2017
uid: tutorials/razor-pages/sql
ms.openlocfilehash: 255faf12064aa424d51fb6faa801884c474bd288
ms.sourcegitcommit: a09820f91e71a7d98b7347bf93210abb9e995e22
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2018
ms.locfileid: "37889485"
---
# <a name="work-with-sql-server-localdb-and-aspnet-core"></a><span data-ttu-id="3ab32-103">SQL Server LocalDB 및 ASP.NET Core 사용</span><span class="sxs-lookup"><span data-stu-id="3ab32-103">Work with SQL Server LocalDB and ASP.NET Core</span></span>

<span data-ttu-id="3ab32-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Joe Audette](https://twitter.com/joeaudette)</span><span class="sxs-lookup"><span data-stu-id="3ab32-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Joe Audette](https://twitter.com/joeaudette)</span></span> 

<span data-ttu-id="3ab32-105">`MovieContext` 개체는 데이터베이스에 연결하고 데이터베이스 레코드에 `Movie` 개체를 매핑하는 작업을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-105">The `MovieContext` object handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="3ab32-106">데이터베이스 컨텍스트는 *Startup.cs* 파일의 `ConfigureServices` 메서드에서 [종속성 주입](xref:fundamentals/dependency-injection) 컨테이너에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-106">The database context is registered with the [Dependency Injection](xref:fundamentals/dependency-injection) container in the `ConfigureServices` method in the *Startup.cs* file:</span></span>

::: moniker range="= aspnetcore-2.0"
[!code-csharp[](razor-pages-start/sample/RazorPagesMovie/Startup.cs?name=snippet_ConfigureServices&highlight=7-8)]

::: moniker-end

::: moniker range=">= aspnetcore-2.1"
[!code-csharp[](razor-pages-start/sample/RazorPagesMovie21/Startup.cs?name=snippet_ConfigureServices&highlight=12-13)]

<span data-ttu-id="3ab32-107">`ConfigureServices`에서 사용되는 메서드에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ab32-107">For more information on the methods used in `ConfigureServices`, see:</span></span>

* <span data-ttu-id="3ab32-108">`CookiePolicyOptions`에 대한 [EU GDPR(일반 데이터 보호 규정) 지원](xref:security/gdpr)</span><span class="sxs-lookup"><span data-stu-id="3ab32-108">[EU General Data Protection Regulation (GDPR) support in ASP.NET Core](xref:security/gdpr) for `CookiePolicyOptions`.</span></span>
* [<span data-ttu-id="3ab32-109">SetCompatibilityVersion</span><span class="sxs-lookup"><span data-stu-id="3ab32-109">SetCompatibilityVersion</span></span>](xref:fundamentals/startup#setcompatibilityversion-for-aspnet-core-mvc)

::: moniker-end

<span data-ttu-id="3ab32-110">ASP.NET Core [구성](xref:fundamentals/configuration/index) 시스템은 `ConnectionString`을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-110">The ASP.NET Core [Configuration](xref:fundamentals/configuration/index) system reads the `ConnectionString`.</span></span> <span data-ttu-id="3ab32-111">로컬 개발의 경우 *appsettings.json* 파일에서 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-111">For local development, it gets the connection string from the *appsettings.json* file.</span></span> <span data-ttu-id="3ab32-112">데이터베이스의 이름 값(`Database={Database name}`)은 생성된 코드에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-112">The name value for the database (`Database={Database name}`) will be different for your generated code.</span></span> <span data-ttu-id="3ab32-113">이름 값은 임의적입니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-113">The name value is arbitrary.</span></span>

[!code-json[](razor-pages-start/sample/RazorPagesMovie/appsettings.json?highlight=2&range=8-10)]

<span data-ttu-id="3ab32-114">테스트 또는 프로덕션 서버에 앱을 배포할 때 환경 변수 또는 다른 방법을 사용하여 실제 SQL Server에 연결 문자열을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-114">When you deploy the app to a test or production server, you can use an environment variable or another approach to set the connection string to a real SQL Server.</span></span> <span data-ttu-id="3ab32-115">자세한 내용은 [구성](xref:fundamentals/configuration/index)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3ab32-115">See [Configuration](xref:fundamentals/configuration/index) for more information.</span></span>

## <a name="sql-server-express-localdb"></a><span data-ttu-id="3ab32-116">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="3ab32-116">SQL Server Express LocalDB</span></span>

<span data-ttu-id="3ab32-117">LocalDB는 프로그램 개발용으로 대상이 지정된 SQL Server Express 데이터베이스 엔진의 간단 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-117">LocalDB is a lightweight version of the SQL Server Express Database Engine that's targeted for program development.</span></span> <span data-ttu-id="3ab32-118">LocalDB는 요청 시 시작하고 사용자 모드에서 실행되므로 복잡한 구성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-118">LocalDB starts on demand and runs in user mode, so there's no complex configuration.</span></span> <span data-ttu-id="3ab32-119">기본적으로 LocalDB 데이터베이스는 *C:/사용자/\<user\>* 디렉터리에 "\*.mdf" 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-119">By default, LocalDB database creates "\*.mdf" files in the *C:/Users/\<user\>* directory.</span></span>

<a name="ssox"></a>
* <span data-ttu-id="3ab32-120">**보기** 메뉴에서 SSOX(**SQL Server 개체 탐색기**)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-120">From the **View** menu, open **SQL Server Object Explorer** (SSOX).</span></span>

  ![보기 메뉴](sql/_static/ssox.png)

* <span data-ttu-id="3ab32-122">`Movie` 테이블을 마우스 오른쪽 단추로 클릭하고 **디자이너 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-122">Right click on the `Movie` table and select **View Designer**:</span></span>

  ![동영상 테이블에서 열린 바로 가기 메뉴](sql/_static/design.png)

  ![디자이너에 열린 동영상 테이블](sql/_static/dv.png)

<span data-ttu-id="3ab32-125">`ID` 옆의 키 아이콘을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-125">Note the key icon next to `ID`.</span></span> <span data-ttu-id="3ab32-126">기본적으로 EF는 기본 키에 대해 `ID`라는 속성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-126">By default, EF creates a property named `ID` for the primary key.</span></span>

* <span data-ttu-id="3ab32-127">`Movie` 테이블을 마우스 오른쪽 단추로 클릭하고 **데이터 보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-127">Right click on the `Movie` table and select **View Data**:</span></span>

  ![테이블 데이터를 보여 주는 열린 동영상 테이블](sql/_static/vd22.png)

## <a name="seed-the-database"></a><span data-ttu-id="3ab32-129">데이터베이스 시드</span><span class="sxs-lookup"><span data-stu-id="3ab32-129">Seed the database</span></span>

<span data-ttu-id="3ab32-130">*Models* 폴더에 `SeedData`라는 새 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-130">Create a new class named `SeedData` in the *Models* folder.</span></span> <span data-ttu-id="3ab32-131">생성된 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-131">Replace the generated code with the following:</span></span>

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie/Models/SeedData.cs?name=snippet_1)]

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie21/Models/SeedData.cs?name=snippet_1)]

::: moniker-end

<span data-ttu-id="3ab32-132">DB에 동영상이 있는 경우 시드 이니셜라이저가 반환되고 동영상이 추가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-132">If there are any movies in the DB, the seed initializer returns and no movies are added.</span></span>

```csharp
if (context.Movie.Any())
{
    return;   // DB has been seeded.
}
```
<a name="si"></a>
### <a name="add-the-seed-initializer"></a><span data-ttu-id="3ab32-133">시드 이니셜라이저 추가</span><span class="sxs-lookup"><span data-stu-id="3ab32-133">Add the seed initializer</span></span>

<span data-ttu-id="3ab32-134">*Program.cs*에서 다음을 수행하는 `Main` 메서드를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-134">In *Program.cs*, modify the `Main` method to do the following:</span></span>

* <span data-ttu-id="3ab32-135">종속성 주입 컨테이너에서 DB 컨텍스트 인스턴스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-135">Get a DB context instance from the dependency injection container.</span></span>
* <span data-ttu-id="3ab32-136">컨텍스트를 전달하는 시드 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-136">Call the seed method, passing to it the context.</span></span>
* <span data-ttu-id="3ab32-137">시드 메서드가 완료되면 컨텍스트를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-137">Dispose the context when the seed method completes.</span></span>

<span data-ttu-id="3ab32-138">다음 코드는 업데이트된 *Program.cs* 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-138">The following code shows the updated *Program.cs* file.</span></span>

::: moniker range="= aspnetcore-2.0"

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie/Program.cs)]

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie21/Program.cs)]

::: moniker-end

<span data-ttu-id="3ab32-139">프로덕션 앱은 `Database.Migrate`를 호출하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-139">A production app would not call `Database.Migrate`.</span></span> <span data-ttu-id="3ab32-140">`Update-Database`가 실행되지 않는 경우 다음 예외를 방지하기 위해 위의 코드에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-140">It's added to the preceding code to prevent the following exception when `Update-Database` has not been run:</span></span>

<span data-ttu-id="3ab32-141">SqlException: 로그인에서 요청한 "RazorPagesMovieContext-21" 데이터베이스를 열 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-141">SqlException: Cannot open database "RazorPagesMovieContext-21" requested by the login.</span></span> <span data-ttu-id="3ab32-142">로그인에 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-142">The login failed.</span></span>
<span data-ttu-id="3ab32-143">'user name' 사용자에 대한 로그인에 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-143">Login failed for user 'user name'.</span></span>

### <a name="test-the-app"></a><span data-ttu-id="3ab32-144">앱 테스트</span><span class="sxs-lookup"><span data-stu-id="3ab32-144">Test the app</span></span>

* <span data-ttu-id="3ab32-145">DB의 모든 레코드를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-145">Delete all the records in the DB.</span></span> <span data-ttu-id="3ab32-146">브라우저 또는 [SSOX](xref:tutorials/razor-pages/new-field#ssox)에서 삭제 링크를 사용하여 이를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-146">You can do this with the delete links in the browser or from [SSOX](xref:tutorials/razor-pages/new-field#ssox)</span></span>
* <span data-ttu-id="3ab32-147">시드 메서드가 실행되도록 앱에서 초기화를 적용하도록 합니다(`Startup` 클래스에서 메서드 호출).</span><span class="sxs-lookup"><span data-stu-id="3ab32-147">Force the app to initialize (call the methods in the `Startup` class) so the seed method runs.</span></span> <span data-ttu-id="3ab32-148">초기화를 적용하려면 IIS Express를 중지하고 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-148">To force initialization, IIS Express must be stopped and restarted.</span></span> <span data-ttu-id="3ab32-149">다음 접근 방식 중 하나를 사용하여 이를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-149">You can do this with any of the following approaches:</span></span>

  * <span data-ttu-id="3ab32-150">알림 영역에서 IIS Express 시스템 트레이 아이콘을 마우스 오른쪽 단추로 클릭하고 **종료** 또는 **사이트 중지**를 탭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-150">Right click the IIS Express system tray icon in the notification area and tap **Exit** or **Stop Site**:</span></span>

    ![IIS Express 시스템 트레이 아이콘](../first-mvc-app/working-with-sql/_static/iisExIcon.png)

    ![바로 가기 메뉴](sql/_static/stopIIS.png)

    * <span data-ttu-id="3ab32-153">비디버그 모드에서 VS를 실행했던 경우 F5 키를 눌러 디버그 모드에서 실행되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-153">If you were running VS in non-debug mode, press F5 to run in debug mode.</span></span>
    * <span data-ttu-id="3ab32-154">디버그 모드에서 VS를 실행했던 경우 디버거를 중지하고 F5 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-154">If you were running VS in debug mode, stop the debugger and press F5.</span></span>
   
<span data-ttu-id="3ab32-155">앱에서 시드된 데이터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-155">The app shows the seeded data:</span></span>

![동영상 데이터를 표시하는 크롬에서 열린 동영상 응용 프로그램](sql/_static/m55.png)

<span data-ttu-id="3ab32-157">다음 자습서는 데이터의 표현을 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="3ab32-157">The next tutorial will clean up the presentation of the data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3ab32-158">[이전: 스캐폴드된 Razor 페이지](xref:tutorials/razor-pages/page)
> [다음: 페이지 업데이트](xref:tutorials/razor-pages/da1)</span><span class="sxs-lookup"><span data-stu-id="3ab32-158">[Previous: Scaffolded Razor Pages](xref:tutorials/razor-pages/page)
[Next: Updating the pages](xref:tutorials/razor-pages/da1)</span></span>
