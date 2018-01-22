---
title: "ASP.NET Core에서 Razor 페이지 앱에 모델 추가"
author: rick-anderson
description: "ASP.NET Core에서 Razor 페이지 앱에 모델 추가"
ms.author: riande
manager: wpickett
ms.date: 07/27/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: aspnet-core
uid: tutorials/razor-pages/model
ms.openlocfilehash: 84e5ec27904b564fa6ee29843ceae0bb70754ea7
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="adding-a-model-to-a-razor-pages-app"></a><span data-ttu-id="b512b-103">Razor 페이지 앱에 모델 추가</span><span class="sxs-lookup"><span data-stu-id="b512b-103">Adding a model to a Razor Pages app</span></span>

[!INCLUDE[model1](../../includes/RP/model1.md)]

## <a name="add-a-data-model"></a><span data-ttu-id="b512b-104">데이터 모델 추가</span><span class="sxs-lookup"><span data-stu-id="b512b-104">Add a data model</span></span>

<span data-ttu-id="b512b-105">솔루션 탐색기에서 **RazorPagesMovie** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 폴더**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b512b-105">In Solution Explorer, right-click the **RazorPagesMovie** project > **Add** > **New Folder**.</span></span> <span data-ttu-id="b512b-106">폴더 이름을 *Models*로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b512b-106">Name the folder *Models*.</span></span>

<span data-ttu-id="b512b-107">*Models* 폴더를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b512b-107">Right click the *Models* folder.</span></span> <span data-ttu-id="b512b-108">**추가** > **클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b512b-108">Select **Add** > **Class**.</span></span> <span data-ttu-id="b512b-109">클래스 이름을 **Movie**로 지정하고 다음 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b512b-109">Name the class **Movie** and add the following properties:</span></span>

[!INCLUDE[model 2](../../includes/RP/model2.md)]

<a name="cs"></a>
### <a name="add-a-database-connection-string"></a><span data-ttu-id="b512b-110">데이터베이스 연결 문자열 추가</span><span class="sxs-lookup"><span data-stu-id="b512b-110">Add a database connection string</span></span>

<span data-ttu-id="b512b-111">*appsettings.json* 파일에 연결 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b512b-111">Add a connection string to the *appsettings.json* file.</span></span>

[!code-json[Main](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/appsettings.json?highlight=8-10)]

<a name="reg"></a>
###  <a name="register-the-database-context"></a><span data-ttu-id="b512b-112">데이터베이스 컨텍스트 등록</span><span class="sxs-lookup"><span data-stu-id="b512b-112">Register the database context</span></span>

<span data-ttu-id="b512b-113">*Startup.cs* 파일에서 [종속성 주입](xref:fundamentals/dependency-injection) 컨테이너에 데이터베이스 컨텍스트를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="b512b-113">Register the database context with the [dependency injection](xref:fundamentals/dependency-injection) container in the *Startup.cs* file.</span></span>

[!code-csharp[Main](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Startup.cs?name=snippet_ConfigureServices&highlight=3-5,7-9)]

<span data-ttu-id="b512b-114">프로젝트를 빌드하여 오류가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b512b-114">Build the project to verify you don't have any errors.</span></span>

<a name="pmc"></a>
## <a name="add-scaffold-tooling-and-perform-initial-migration"></a><span data-ttu-id="b512b-115">스캐폴드 도구 추가 및 초기 마이그레이션 수행</span><span class="sxs-lookup"><span data-stu-id="b512b-115">Add scaffold tooling and perform initial migration</span></span>

<span data-ttu-id="b512b-116">이 섹션에서는 PMC(패키지 관리자 콘솔)를 사용하여 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b512b-116">In this section, you use the Package Manager Console (PMC) to:</span></span>

* <span data-ttu-id="b512b-117">Visual Studio 웹 코드 생성 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b512b-117">Add the Visual Studio web code generation package.</span></span> <span data-ttu-id="b512b-118">스캐폴딩 엔진을 실행하려면 이 패키지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b512b-118">This package is required to run the scaffolding engine.</span></span>
* <span data-ttu-id="b512b-119">초기 마이그레이션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b512b-119">Add an initial migration.</span></span>
* <span data-ttu-id="b512b-120">초기 마이그레이션을 사용하여 데이터베이스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="b512b-120">Update the database with the initial migration.</span></span>

<span data-ttu-id="b512b-121">**도구** 메뉴에서 **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b512b-121">From the **Tools** menu, select **NuGet Package Manager** > **Package Manager Console**.</span></span>

  ![PMC 메뉴](../first-mvc-app/adding-model/_static/pmc.png)

<span data-ttu-id="b512b-123">PMC에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b512b-123">In the PMC, enter the following commands:</span></span>

```powershell
Install-Package Microsoft.VisualStudio.Web.CodeGeneration.Design
Add-Migration Initial
Update-Database
```

<span data-ttu-id="b512b-124">`Install-Package` 명령은 스캐폴딩 엔진을 실행하는 데 필요한 도구를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b512b-124">The `Install-Package` command installs the tooling required to run the scaffolding engine.</span></span>

<span data-ttu-id="b512b-125">`Add-Migration` 명령은 초기 데이터베이스 스키마를 만드는 코드를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="b512b-125">The `Add-Migration` command generates code to create the initial database schema.</span></span> <span data-ttu-id="b512b-126">스키마는 `DbContext`에 지정된 모델을 기반으로 합니다(*Models/MovieContext.cs* 파일에서).</span><span class="sxs-lookup"><span data-stu-id="b512b-126">The schema is based on the model specified in the `DbContext` (In the *Models/MovieContext.cs* file).</span></span> <span data-ttu-id="b512b-127">`Initial` 인수는 마이그레이션 이름을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b512b-127">The `Initial` argument is used to name the migrations.</span></span> <span data-ttu-id="b512b-128">모든 이름을 사용할 수 있지만 일반적으로 마이그레이션을 설명하는 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b512b-128">You can use any name, but by convention you choose a name that describes the migration.</span></span> <span data-ttu-id="b512b-129">자세한 내용은 [마이그레이션 소개](xref:data/ef-mvc/migrations#introduction-to-migrations)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b512b-129">See [Introduction to migrations](xref:data/ef-mvc/migrations#introduction-to-migrations) for more information.</span></span>

<span data-ttu-id="b512b-130">`Update-Database` 명령은 데이터베이스를 만드는 *Migrations/\<time-stamp>_InitialCreate.cs* 파일에서 `Up` 메서드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b512b-130">The `Update-Database` command runs the `Up` method in the *Migrations/\<time-stamp>_InitialCreate.cs* file, which creates the database.</span></span>

[!INCLUDE[model 4windows](../../includes/RP/model4Win.md)]

[!INCLUDE[model 4](../../includes/RP/model4tbl.md)]

<a name="test"></a>
### <a name="test-the-app"></a><span data-ttu-id="b512b-131">앱 테스트</span><span class="sxs-lookup"><span data-stu-id="b512b-131">Test the app</span></span>

* <span data-ttu-id="b512b-132">앱을 실행하고 브라우저에서 `/Movies`를 URL에 추가합니다(`http://localhost:port/movies`).</span><span class="sxs-lookup"><span data-stu-id="b512b-132">Run the app and append `/Movies` to the URL in the browser (`http://localhost:port/movies`).</span></span>
* <span data-ttu-id="b512b-133">**만들기** 링크를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b512b-133">Test the **Create** link.</span></span>

 ![페이지 만들기](../../tutorials/razor-pages/model/_static/conan.png)

<a name="scaffold"></a>

* <span data-ttu-id="b512b-135">**편집**, **세부 정보** 및 **삭제** 링크를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b512b-135">Test the **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="b512b-136">SQL 예외가 발생하는 경우 마이그레이션을 실행했는지와 데이터베이스를 업데이트했는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="b512b-136">If you get a SQL exception, verify you have run migrations and updated the database:</span></span>

<span data-ttu-id="b512b-137">다음 자습서에서는 스캐폴딩을 통해 만들어진 파일을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b512b-137">The next tutorial explains the files created by scaffolding.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="b512b-138">[이전: 시작](xref:tutorials/razor-pages/razor-pages-start)
[다음: 스캐폴드된 Razor 페이지](xref:tutorials/razor-pages/page)</span><span class="sxs-lookup"><span data-stu-id="b512b-138">[Previous: Getting Started](xref:tutorials/razor-pages/razor-pages-start)
[Next: Scaffolded Razor Pages](xref:tutorials/razor-pages/page)</span></span>    
