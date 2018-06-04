---
title: ASP.NET Core에서 SQL Server LocalDB 사용
author: rick-anderson
description: 간단한 ASP.NET Core MVC 앱에서 SQL Server LocalDB를 사용하는 방법에 대해 배웁니다.
manager: wpickett
ms.author: riande
ms.date: 03/07/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/first-mvc-app/working-with-sql
ms.openlocfilehash: b00d709f3009f63431becf24797269ad5988a20b
ms.sourcegitcommit: 43bd79667bbdc8a07bd39fb4cd6f7ad3e70212fb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34688376"
---
# <a name="work-with-sql-server-localdb-in-aspnet-core"></a><span data-ttu-id="c30ed-103">ASP.NET Core에서 SQL Server LocalDB 사용</span><span class="sxs-lookup"><span data-stu-id="c30ed-103">Work with SQL Server LocalDB in ASP.NET Core</span></span>

<span data-ttu-id="c30ed-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="c30ed-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="c30ed-105">`MvcMovieContext` 개체는 데이터베이스에 연결하고 데이터베이스 레코드에 `Movie` 개체를 매핑하는 작업을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c30ed-105">The `MvcMovieContext` object handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="c30ed-106">데이터베이스 컨텍스트는 *Startup.cs* 파일의 `ConfigureServices` 메서드에서 [종속성 주입](xref:fundamentals/dependency-injection) 컨테이너에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="c30ed-106">The database context is registered with the [Dependency Injection](xref:fundamentals/dependency-injection) container in the `ConfigureServices` method in the *Startup.cs* file:</span></span>

::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="c30ed-107">[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie21/Startup.cs?name=ConfigureServices&highlight=13-99)]</span><span class="sxs-lookup"><span data-stu-id="c30ed-107">[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie21/Startup.cs?name=ConfigureServices&highlight=13-99)]</span></span>
::: moniker-end
::: moniker range="<= aspnetcore-2.0"
<span data-ttu-id="c30ed-108">[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Startup.cs?name=ConfigureServices&highlight=6-7)]</span><span class="sxs-lookup"><span data-stu-id="c30ed-108">[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Startup.cs?name=ConfigureServices&highlight=6-7)]</span></span>
::: moniker-end

<span data-ttu-id="c30ed-109">ASP.NET Core [구성](xref:fundamentals/configuration/index) 시스템은 `ConnectionString`을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="c30ed-109">The ASP.NET Core [Configuration](xref:fundamentals/configuration/index) system reads the `ConnectionString`.</span></span> <span data-ttu-id="c30ed-110">로컬 개발의 경우 *appsettings.json* 파일에서 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c30ed-110">For local development, it gets the connection string from the *appsettings.json* file:</span></span>

[!code-json[](start-mvc/sample/MvcMovie/appsettings.json?highlight=2&range=8-10)]

<span data-ttu-id="c30ed-111">테스트 또는 프로덕션 서버에 앱을 배포할 때 환경 변수 또는 다른 방법을 사용하여 실제 SQL Server에 연결 문자열을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c30ed-111">When you deploy the app to a test or production server, you can use an environment variable or another approach to set the connection string to a real SQL Server.</span></span> <span data-ttu-id="c30ed-112">자세한 내용은 [구성](xref:fundamentals/configuration/index)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c30ed-112">See [Configuration](xref:fundamentals/configuration/index) for more information.</span></span>

## <a name="sql-server-express-localdb"></a><span data-ttu-id="c30ed-113">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="c30ed-113">SQL Server Express LocalDB</span></span>

<span data-ttu-id="c30ed-114">LocalDB는 프로그램 개발용으로 대상이 지정된 SQL Server Express 데이터베이스 엔진의 간단 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="c30ed-114">LocalDB is a lightweight version of the SQL Server Express Database Engine that's targeted for program development.</span></span> <span data-ttu-id="c30ed-115">LocalDB는 요청 시 시작하고 사용자 모드에서 실행되므로 복잡한 구성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c30ed-115">LocalDB starts on demand and runs in user mode, so there's no complex configuration.</span></span> <span data-ttu-id="c30ed-116">기본적으로 LocalDB 데이터베이스는 *C:/사용자/\<user\>* 디렉터리에 "\*.mdf" 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c30ed-116">By default, LocalDB database creates "\*.mdf" files in the *C:/Users/\<user\>* directory.</span></span>

* <span data-ttu-id="c30ed-117">**보기** 메뉴에서 SSOX(**SQL Server 개체 탐색기**)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c30ed-117">From the **View** menu, open **SQL Server Object Explorer** (SSOX).</span></span>

  ![보기 메뉴](working-with-sql/_static/ssox.png)

* <span data-ttu-id="c30ed-119">마우스 오른쪽 단추로 `Movie` 테이블 **> 디자이너 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c30ed-119">Right click on the `Movie` table **> View Designer**</span></span>

  ![동영상 테이블에서 열린 바로 가기 메뉴](working-with-sql/_static/design.png)

  ![디자이너에 열린 동영상 테이블](working-with-sql/_static/dv.png)

<span data-ttu-id="c30ed-122">`ID` 옆의 키 아이콘을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c30ed-122">Note the key icon next to `ID`.</span></span> <span data-ttu-id="c30ed-123">기본적으로 EF는 `ID`라는 속성을 기본 키로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c30ed-123">By default, EF will make a property named `ID` the primary key.</span></span>

* <span data-ttu-id="c30ed-124">마우스 오른쪽 단추로 `Movie` 테이블 **> 데이터 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c30ed-124">Right click on the `Movie` table **> View Data**</span></span>

  ![동영상 테이블에서 열린 바로 가기 메뉴](working-with-sql/_static/ssox2.png)

  ![테이블 데이터를 보여 주는 열린 동영상 테이블](working-with-sql/_static/vd22.png)

## <a name="seed-the-database"></a><span data-ttu-id="c30ed-127">데이터베이스 시드</span><span class="sxs-lookup"><span data-stu-id="c30ed-127">Seed the database</span></span>

<span data-ttu-id="c30ed-128">*Models* 폴더에 `SeedData`라는 새 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c30ed-128">Create a new class named `SeedData` in the *Models* folder.</span></span> <span data-ttu-id="c30ed-129">생성된 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c30ed-129">Replace the generated code with the following:</span></span>

[!code-csharp[](start-mvc/sample/MvcMovie/Models/SeedData.cs?name=snippet_1)]

<span data-ttu-id="c30ed-130">DB에 동영상이 있는 경우 시드 이니셜라이저가 반환되고 동영상이 추가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c30ed-130">If there are any movies in the DB, the seed initializer returns and no movies are added.</span></span>

```csharp
if (context.Movie.Any())
{
    return;   // DB has been seeded.
}
```

<a name="si"></a>
### <a name="add-the-seed-initializer"></a><span data-ttu-id="c30ed-131">시드 이니셜라이저 추가</span><span class="sxs-lookup"><span data-stu-id="c30ed-131">Add the seed initializer</span></span>

::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="c30ed-132">[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie21/Program.cs)]</span><span class="sxs-lookup"><span data-stu-id="c30ed-132">[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie21/Program.cs)]</span></span>
::: moniker-end
::: moniker range="<= aspnetcore-2.0"

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="c30ed-133">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="c30ed-133">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

<span data-ttu-id="c30ed-134">*Program.cs* 파일에서 `Main` 메서드에 시드 이니셜라이저를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c30ed-134">Add the seed initializer to the `Main` method in the *Program.cs* file:</span></span>

<span data-ttu-id="c30ed-135">[!code-csharp[](start-mvc/sample/MvcMovie/Program.cs?highlight=6,14-32)]</span><span class="sxs-lookup"><span data-stu-id="c30ed-135">[!code-csharp[](start-mvc/sample/MvcMovie/Program.cs?highlight=6,14-32)]</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="c30ed-136">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="c30ed-136">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

<span data-ttu-id="c30ed-137">*Startup.cs* 파일에서 `Configure` 메서드의 끝에 시드 이니셜라이저를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c30ed-137">Add the seed initializer to the end of the `Configure` method in the *Startup.cs* file.</span></span>

<span data-ttu-id="c30ed-138">[!code-csharp[](start-mvc/sample/MvcMovie/Startup.cs?highlight=9&name=snippet_seed)]</span><span class="sxs-lookup"><span data-stu-id="c30ed-138">[!code-csharp[](start-mvc/sample/MvcMovie/Startup.cs?highlight=9&name=snippet_seed)]</span></span>

---
::: moniker-end

<span data-ttu-id="c30ed-139">앱 테스트</span><span class="sxs-lookup"><span data-stu-id="c30ed-139">Test the app</span></span>

* <span data-ttu-id="c30ed-140">DB의 모든 레코드를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c30ed-140">Delete all the records in the DB.</span></span> <span data-ttu-id="c30ed-141">브라우저 또는 SSOX에서 삭제 링크를 사용하여 이를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c30ed-141">You can do this with the delete links in the browser or from SSOX.</span></span>
* <span data-ttu-id="c30ed-142">시드 메서드가 실행되도록 앱에서 초기화를 적용하도록 합니다(`Startup` 클래스에서 메서드 호출).</span><span class="sxs-lookup"><span data-stu-id="c30ed-142">Force the app to initialize (call the methods in the `Startup` class) so the seed method runs.</span></span> <span data-ttu-id="c30ed-143">초기화를 적용하려면 IIS Express를 중지하고 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c30ed-143">To force initialization, IIS Express must be stopped and restarted.</span></span> <span data-ttu-id="c30ed-144">다음 접근 방식 중 하나를 사용하여 이를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c30ed-144">You can do this with any of the following approaches:</span></span>

  * <span data-ttu-id="c30ed-145">알림 영역에서 IIS Express 시스템 트레이 아이콘을 마우스 오른쪽 단추로 클릭하고 **종료** 또는 **사이트 중지**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c30ed-145">Right click the IIS Express system tray icon in the notification area and tap **Exit** or **Stop Site**</span></span>

    ![IIS Express 시스템 트레이 아이콘](working-with-sql/_static/iisExIcon.png)

    ![바로 가기 메뉴](working-with-sql/_static/stopIIS.png)

    * <span data-ttu-id="c30ed-148">비디버그 모드에서 VS를 실행했던 경우 F5 키를 눌러 디버그 모드에서 실행되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c30ed-148">If you were running VS in non-debug mode, press F5 to run in debug mode</span></span>
    * <span data-ttu-id="c30ed-149">디버그 모드에서 VS를 실행했던 경우 디버거를 중지하고 F5 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c30ed-149">If you were running VS in debug mode, stop the debugger and press F5</span></span>

<span data-ttu-id="c30ed-150">앱에서 시드된 데이터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c30ed-150">The app shows the seeded data.</span></span>

![동영상 데이터를 표시하는 Microsoft Edge에서 열린 MVC 동영상 응용 프로그램](working-with-sql/_static/m55.png)

> [!div class="step-by-step"]
> <span data-ttu-id="c30ed-152">[이전](adding-model.md)
> [다음](controller-methods-views.md)</span><span class="sxs-lookup"><span data-stu-id="c30ed-152">[Previous](adding-model.md)
[Next](controller-methods-views.md)</span></span>  
