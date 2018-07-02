---
title: ASP.NET Core MVC 및 EF Core - 마이그레이션 - 4/10
author: rick-anderson
description: 이 자습서에서는 ASP.NET Core MVC 응용 프로그램에서 데이터 모델 변경 관리를 위해 EF Core 마이그레이션 기능을 사용하는 것을 시작합니다.
ms.author: tdykstra
ms.date: 03/15/2018
uid: data/ef-mvc/migrations
ms.openlocfilehash: f710b33ac1a6017b0e3d7e8c3e528675a41424bb
ms.sourcegitcommit: c6ed2f00c7a08223d79090396b85793718b0dd69
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37092944"
---
# <a name="aspnet-core-mvc-with-ef-core---migrations---4-of-10"></a><span data-ttu-id="40769-103">ASP.NET Core MVC 및 EF Core - 마이그레이션 - 4/10</span><span class="sxs-lookup"><span data-stu-id="40769-103">ASP.NET Core MVC with EF Core - Migrations - 4 of 10</span></span>

[!INCLUDE [RP better than MVC](~/includes/RP-EF/rp-over-mvc-21.md)]

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="40769-104">작성자: [Tom Dykstra](https://github.com/tdykstra) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="40769-104">By [Tom Dykstra](https://github.com/tdykstra) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="40769-105">Contoso University 웹 응용 프로그램 예제는 Entity Framework Core 및 Visual Studio를 사용하여 ASP.NET Core MVC 웹 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="40769-105">The Contoso University sample web application demonstrates how to create ASP.NET Core MVC web applications using Entity Framework Core and Visual Studio.</span></span> <span data-ttu-id="40769-106">자습서 시리즈에 대한 정보는 [시리즈의 첫 번째 자습서](intro.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40769-106">For information about the tutorial series, see [the first tutorial in the series](intro.md).</span></span>

<span data-ttu-id="40769-107">이 자습서에서는 데이터 모델 변경을 관리하기 위해 EF Core 마이그레이션 기능을 사용하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="40769-107">In this tutorial, you start using the EF Core migrations feature for managing data model changes.</span></span> <span data-ttu-id="40769-108">이후의 자습서에서는 데이터 모델을 변경하면서 더 많은 마이그레이션을 추가하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40769-108">In later tutorials, you'll add more migrations as you change the data model.</span></span>

## <a name="introduction-to-migrations"></a><span data-ttu-id="40769-109">마이그레이션 소개</span><span class="sxs-lookup"><span data-stu-id="40769-109">Introduction to migrations</span></span>

<span data-ttu-id="40769-110">새 응용 프로그램을 개발하는 경우 데이터 모델은 자주 변경되며 모델이 변경될 때마다 데이터베이스와 동기화를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="40769-110">When you develop a new application, your data model changes frequently, and each time the model changes, it gets out of sync with the database.</span></span> <span data-ttu-id="40769-111">데이터베이스가 존재하지 않는 경우 Entity Framework를 구성하여 만들면서 이러한 자습서를 시작하였습니다.</span><span class="sxs-lookup"><span data-stu-id="40769-111">You started these tutorials by configuring the Entity Framework to create the database if it doesn't exist.</span></span> <span data-ttu-id="40769-112">그런 다음, 엔터티 클래스를 추가, 제거 또는 변경하거나 DbContext 클래스를 변경하면서 데이터 모델을 변경할 때마다 데이터베이스를 삭제할 수 있습니다. 또한 EF는 모델에 일치하는 새로운 항목을 만들고 테스트 데이터로 시드합니다.</span><span class="sxs-lookup"><span data-stu-id="40769-112">Then each time you change the data model -- add, remove, or change entity classes or change your DbContext class -- you can delete the database and EF creates a new one that matches the model, and seeds it with test data.</span></span>

<span data-ttu-id="40769-113">데이터베이스를 데이터 모델과 동기화된 상태로 유지하는 이 메서드는 응용 프로그램을 프로덕션 환경에 배포할 때까지 잘 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="40769-113">This method of keeping the database in sync with the data model works well until you deploy the application to production.</span></span> <span data-ttu-id="40769-114">응용 프로그램이 프로덕션 환경에서 실행 중인 경우, 일반적으로 새 열을 추가하는 것처럼 사용자가 변경할 때마다 유지하려는 데이터 및 손실하지 않으려는 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="40769-114">When the application is running in production it's usually storing data that you want to keep, and you don't want to lose everything each time you make a change such as adding a new column.</span></span> <span data-ttu-id="40769-115">EF Core 마이그레이션 기능은 EF가 새 데이터베이스를 만드는 대신 데이터베이스 스키마를 업데이트하도록 설정하여 이 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="40769-115">The EF Core Migrations feature solves this problem by enabling EF to update the database schema instead of creating  a new database.</span></span>

## <a name="entity-framework-core-nuget-packages-for-migrations"></a><span data-ttu-id="40769-116">마이그레이션을 위한 Entity Framework Core NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="40769-116">Entity Framework Core NuGet packages for migrations</span></span>

<span data-ttu-id="40769-117">마이그레이션을 수행하기 위해 **PMC(패키지 관리자 콘솔)** 또는 CLI(명령줄 인터페이스)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40769-117">To work with migrations, you can use the **Package Manager Console** (PMC) or the command-line interface (CLI).</span></span>  <span data-ttu-id="40769-118">이러한 자습서에는 CLI 명령을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="40769-118">These tutorials show how to use CLI commands.</span></span> <span data-ttu-id="40769-119">PMC에 대한 정보는 [이 자습서의 마지막](#pmc)에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40769-119">Information about the PMC is at [the end of this tutorial](#pmc).</span></span>

<span data-ttu-id="40769-120">CLI(명령줄 인터페이스)용 EF 도구는 [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet)에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="40769-120">The EF tools for the command-line interface (CLI) are provided in [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet).</span></span> <span data-ttu-id="40769-121">이 패키지를 설치하려면 표시된 것처럼 *.csproj* 파일의 `DotNetCliToolReference` 컬렉션에 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="40769-121">To install this package, add it to the `DotNetCliToolReference` collection in the *.csproj* file, as shown.</span></span> <span data-ttu-id="40769-122">**참고:** *.csproj* 파일을 편집하여 이 패키지를 설치해야 합니다. `install-package` 명령이나 패키지 관리자 GUI를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="40769-122">**Note:** You have to install this package by editing the *.csproj* file; you can't use the `install-package` command or the package manager GUI.</span></span> <span data-ttu-id="40769-123">**솔루션 탐색기**에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭하고 **ContosoUniversity.csproj 편집**을 선택하여 *.csproj* 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="40769-123">You can edit the *.csproj* file by right-clicking the project name in **Solution Explorer** and selecting **Edit ContosoUniversity.csproj**.</span></span>

[!code-xml[](intro/samples/cu/ContosoUniversity.csproj?range=12-15&highlight=2)]
  
<span data-ttu-id="40769-124">(이 예제의 버전 번호는 이 자습서가 작성된 당시의 버전 번호입니다.)</span><span class="sxs-lookup"><span data-stu-id="40769-124">(The version numbers in this example were current when the tutorial was written.)</span></span>

## <a name="change-the-connection-string"></a><span data-ttu-id="40769-125">연결 문자열 변경</span><span class="sxs-lookup"><span data-stu-id="40769-125">Change the connection string</span></span>

<span data-ttu-id="40769-126">*appsettings.json* 파일에서 연결 문자열에 있는 데이터베이스의 이름을 ContosoUniversity2 또는 사용 중인 컴퓨터에서 사용한 적 없는 다른 이름으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="40769-126">In the *appsettings.json* file, change the name of the database in the connection string to ContosoUniversity2 or some other name that you haven't used on the computer you're using.</span></span>

[!code-json[](intro/samples/cu/appsettings2.json?range=1-4)]

<span data-ttu-id="40769-127">이러한 변경은 첫 번째 마이그레이션이 새 데이터베이스를 만드는 프로젝트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="40769-127">This change sets up the project so that the first migration will create a new database.</span></span> <span data-ttu-id="40769-128">이는 마이그레이션을 시작하는 데 필수는 아니지만 나중에 이에 대한 이점을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40769-128">This isn't required to get started with migrations, but you'll see later why it's a good idea.</span></span>

> [!NOTE]
> <span data-ttu-id="40769-129">데이터베이스 이름을 변경하는 대신, 데이터베이스를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40769-129">As an alternative to changing the database name, you can delete the database.</span></span> <span data-ttu-id="40769-130">**SSOX(SQL Server 개체 탐색기)** 또는 `database drop` CLI 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="40769-130">Use **SQL Server Object Explorer** (SSOX) or the `database drop` CLI command:</span></span>
> ```console
> dotnet ef database drop
> ```
> <span data-ttu-id="40769-131">다음 섹션에서는 CLI 명령을 실행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="40769-131">The following section explains how to run CLI commands.</span></span>

## <a name="create-an-initial-migration"></a><span data-ttu-id="40769-132">초기 마이그레이션 만들기</span><span class="sxs-lookup"><span data-stu-id="40769-132">Create an initial migration</span></span>

<span data-ttu-id="40769-133">변경 내용을 저장하고 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="40769-133">Save your changes and build the project.</span></span> <span data-ttu-id="40769-134">그런 다음, 명령 창을 열고 프로젝트 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="40769-134">Then open a command window and navigate to the project folder.</span></span> <span data-ttu-id="40769-135">작업을 수행하는 빠른 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="40769-135">Here's a quick way to do that:</span></span>

* <span data-ttu-id="40769-136">**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 바로 가기 메뉴에서 **파일 탐색기에서 열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40769-136">In **Solution Explorer**, right-click the project and choose **Open in File Explorer** from the context menu.</span></span>

  ![파일 탐색기에서 열기 메뉴 항목](migrations/_static/open-in-file-explorer.png)

* <span data-ttu-id="40769-138">주소 표시줄에 “cmd”를 입력하고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="40769-138">Enter "cmd" in the address bar and press Enter.</span></span>

  ![열기 명령 창](migrations/_static/open-command-window.png)

<span data-ttu-id="40769-140">명령 창에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="40769-140">Enter the following command in the command window:</span></span>

```console
dotnet ef migrations add InitialCreate
```

<span data-ttu-id="40769-141">명령 창에 다음과 같은 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="40769-141">You see output like the following in the command window:</span></span>

```console
info: Microsoft.AspNetCore.DataProtection.KeyManagement.XmlKeyManager[0]
      User profile is available. Using 'C:\Users\username\AppData\Local\ASP.NET\DataProtection-Keys' as key repository and Windows DPAPI to encrypt keys at rest.
info: Microsoft.EntityFrameworkCore.Infrastructure[100403]
      Entity Framework Core 2.0.0-rtm-26452 initialized 'SchoolContext' using provider 'Microsoft.EntityFrameworkCore.SqlServer' with options: None
Done. To undo this action, use 'ef migrations remove'
```

> [!NOTE]
> <span data-ttu-id="40769-142">*No executable found matching command "dotnet-ef"(명령 “dotnet-ef”에 일치하는 실행 파일을 찾을 수 없음)* 오류 메시지가 표시되면 [이 블로그 게시물](http://thedatafarm.com/data-access/no-executable-found-matching-command-dotnet-ef/)을 참조하여 문제 해결에 도움을 받으세요.</span><span class="sxs-lookup"><span data-stu-id="40769-142">If you see an error message *No executable found matching command "dotnet-ef"*, see [this blog post](http://thedatafarm.com/data-access/no-executable-found-matching-command-dotnet-ef/) for help troubleshooting.</span></span>

<span data-ttu-id="40769-143">“*cannot access the file ... ContosoUniversity.dll because it is being used by another process.*(다른 프로세스에서 사용 중이므로 ContosoUniversity.dll 파일에 액세스할 수 없음.)” 오류 메시지가 표시되면 Windows 시스템 트레이에서 IIS Express 아이콘을 찾아 마우스 오른쪽 단추로 클릭한 다음, **ContosoUniversity > 사이트 중단**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40769-143">If you see an error message "*cannot access the file ... ContosoUniversity.dll because it is being used by another process.*", find the IIS Express icon in the Windows System Tray, and right-click it, then click **ContosoUniversity > Stop Site**.</span></span>

## <a name="examine-the-up-and-down-methods"></a><span data-ttu-id="40769-144">Up 및 Down 메서드 검사</span><span class="sxs-lookup"><span data-stu-id="40769-144">Examine the Up and Down methods</span></span>

<span data-ttu-id="40769-145">`migrations add` 명령을 실행하면 EF는 데이터베이스를 처음부터 만드는 코드를 생성했습니다.</span><span class="sxs-lookup"><span data-stu-id="40769-145">When you executed the `migrations add` command, EF generated the code that will create the database from scratch.</span></span> <span data-ttu-id="40769-146">이 코드는 *\<timestamp>_InitialCreate.cs*라는 파일의 *Migrations* 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40769-146">This code is in the *Migrations* folder, in the file named *\<timestamp>_InitialCreate.cs*.</span></span> <span data-ttu-id="40769-147">다음 예제와 같이 `InitialCreate` 클래스의 `Up` 메서드는 데이터 모델 엔터티 집합에 해당하는 데이터베이스 테이블을 만들고 `Down` 메서드는 이를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="40769-147">The `Up` method of the `InitialCreate` class creates the database tables that correspond to the data model entity sets, and the `Down` method deletes them, as shown in the following example.</span></span>

[!code-csharp[](intro/samples/cu/Migrations/20170215220724_InitialCreate.cs?range=92-118)]

<span data-ttu-id="40769-148">마이그레이션에서는 마이그레이션을 위한 데이터 모델 변경을 구현하기 위해 `Up` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="40769-148">Migrations calls the `Up` method to implement the data model changes for a migration.</span></span> <span data-ttu-id="40769-149">업데이트를 롤백하는 명령을 입력하면 마이그레이션에서 `Down` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="40769-149">When you enter a command to roll back the update, Migrations calls the `Down` method.</span></span>

<span data-ttu-id="40769-150">이 코드는 `migrations add InitialCreate` 명령을 입력했을 때 만들어진 초기 마이그레이션을 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="40769-150">This code is for the initial migration that was created when you entered the `migrations add InitialCreate` command.</span></span> <span data-ttu-id="40769-151">파일 이름에는 마이그레이션 이름 매개 변수(이 예제에서 “InitialCreate”)가 사용되며 사용자가 원하는 이름일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40769-151">The migration name parameter ("InitialCreate" in the example) is used for the file name and can be whatever you want.</span></span> <span data-ttu-id="40769-152">마이그레이션에서 수행 중인 작업을 요약한 단어 또는 구를 선택하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="40769-152">It's best to choose a word or phrase that summarizes what is being done in the migration.</span></span> <span data-ttu-id="40769-153">예를 들어 이후 마이그레이션의 이름을 “AddDepartmentTable”로 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40769-153">For example, you might name a later migration "AddDepartmentTable".</span></span>

<span data-ttu-id="40769-154">데이터베이스가 이미 존재할 때 초기 마이그레이션을 만든 경우 데이터베이스 만들기 코드가 생성되지만 데이터베이스는 이미 데이터 모델과 일치하기 때문에 실행할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="40769-154">If you created the initial migration when the database already exists, the database creation code is generated but it doesn't have to run because the database already matches the data model.</span></span> <span data-ttu-id="40769-155">데이터베이스가 아직 없는 다른 환경에 앱을 배포하는 경우 이 코드를 실행하여 데이터베이스를 만들기 때문에 먼저 테스트하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="40769-155">When you deploy the app to another environment where the database doesn't exist yet, this code will run to create your database, so it's a good idea to test it first.</span></span> <span data-ttu-id="40769-156">바로 이것이 앞서 연결 문자열의 데이터베이스 이름을 변경한 이유입니다. 따라서 해당 마이그레이션은 처음부터 새로운 데이터베이스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40769-156">That's why you changed the name of the database in the connection string earlier -- so that migrations can create a new one from scratch.</span></span>

## <a name="the-data-model-snapshot"></a><span data-ttu-id="40769-157">데이터 모델 스냅숏</span><span class="sxs-lookup"><span data-stu-id="40769-157">The data model snapshot</span></span>

<span data-ttu-id="40769-158">마이그레이션은 현재 데이터베이스 스키마의 *스냅숏*을 *Migrations/SchoolContextModelSnapshot.cs*에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="40769-158">Migrations creates a *snapshot* of the current database schema in *Migrations/SchoolContextModelSnapshot.cs*.</span></span> <span data-ttu-id="40769-159">마이그레이션을 추가하면 EF가 데이터 모델을 스냅숏 파일과 비교하여 변경 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="40769-159">When you add a migration, EF determines what changed by comparing the data model to the snapshot file.</span></span>

<span data-ttu-id="40769-160">마이그레이션을 삭제할 때는 [dotnet ef migrations remove](https://docs.microsoft.com/ef/core/miscellaneous/cli/dotnet#dotnet-ef-migrations-remove) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="40769-160">When deleting a migration, use the [dotnet ef migrations remove](https://docs.microsoft.com/ef/core/miscellaneous/cli/dotnet#dotnet-ef-migrations-remove) command.</span></span> <span data-ttu-id="40769-161">`dotnet ef migrations remove`는 마이그레이션을 삭제하고 스냅숏이 올바르게 다시 설정되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="40769-161">`dotnet ef migrations remove` deletes the migration and ensures the snapshot is correctly reset.</span></span>

<span data-ttu-id="40769-162">스냅숏 파일을 사용하는 방법에 대한 자세한 내용은 [팀 환경의 EF Core 마이그레이션](/ef/core/managing-schemas/migrations/teams)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40769-162">See [EF Core Migrations in Team Environments](/ef/core/managing-schemas/migrations/teams) for more information about how the snapshot file is used.</span></span>

## <a name="apply-the-migration-to-the-database"></a><span data-ttu-id="40769-163">새 마이그레이션을 데이터베이스에 적용</span><span class="sxs-lookup"><span data-stu-id="40769-163">Apply the migration to the database</span></span>

<span data-ttu-id="40769-164">명령 창에서 다음 명령을 입력하여 데이터베이스 및 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="40769-164">In the command window, enter the following command to create the database and tables in it.</span></span>

```console
dotnet ef database update
```

<span data-ttu-id="40769-165">명령의 출력은 데이터베이스를 설정하는 SQL 명령에 대한 로그가 표시되는 것 외에 `migrations add` 명령과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="40769-165">The output from the command is similar to the `migrations add` command, except that you see logs for the SQL commands that set up the database.</span></span> <span data-ttu-id="40769-166">대부분의 로그는 다음 예제 출력에서 생략됩니다.</span><span class="sxs-lookup"><span data-stu-id="40769-166">Most of the logs are omitted in the following sample output.</span></span> <span data-ttu-id="40769-167">로그 메시지의 세부 수준을 줄이는 것을 선호하는 경우 *appsettings.Development.json* 파일에서 로그 수준을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40769-167">If you prefer not to see this level of detail in log messages, you can change the log level in the *appsettings.Development.json* file.</span></span> <span data-ttu-id="40769-168">자세한 내용은 [로깅 소개](xref:fundamentals/logging/index)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40769-168">For more information, see [Introduction to logging](xref:fundamentals/logging/index).</span></span>

```text
info: Microsoft.AspNetCore.DataProtection.KeyManagement.XmlKeyManager[0]
      User profile is available. Using 'C:\Users\username\AppData\Local\ASP.NET\DataProtection-Keys' as key repository and Windows DPAPI to encrypt keys at rest.
info: Microsoft.EntityFrameworkCore.Infrastructure[100403]
      Entity Framework Core 2.0.0-rtm-26452 initialized 'SchoolContext' using provider 'Microsoft.EntityFrameworkCore.SqlServer' with options: None
info: Microsoft.EntityFrameworkCore.Database.Command[200101]
      Executed DbCommand (467ms) [Parameters=[], CommandType='Text', CommandTimeout='60']
      CREATE DATABASE [ContosoUniversity2];
info: Microsoft.EntityFrameworkCore.Database.Command[200101]
      Executed DbCommand (20ms) [Parameters=[], CommandType='Text', CommandTimeout='30']
      CREATE TABLE [__EFMigrationsHistory] (
          [MigrationId] nvarchar(150) NOT NULL,
          [ProductVersion] nvarchar(32) NOT NULL,
          CONSTRAINT [PK___EFMigrationsHistory] PRIMARY KEY ([MigrationId])
      );

<logs omitted for brevity>

info: Microsoft.EntityFrameworkCore.Database.Command[200101]
      Executed DbCommand (3ms) [Parameters=[], CommandType='Text', CommandTimeout='30']
      INSERT INTO [__EFMigrationsHistory] ([MigrationId], [ProductVersion])
      VALUES (N'20170816151242_InitialCreate', N'2.0.0-rtm-26452');
Done.
```

<span data-ttu-id="40769-169">**SQL Server 개체 탐색기**를 사용하여 첫 번째 자습서에서와 같이 데이터베이스를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="40769-169">Use **SQL Server Object Explorer** to inspect the database as you did in the first tutorial.</span></span>  <span data-ttu-id="40769-170">데이터베이스에 어떤 마이그레이션이 적용되는지를 추적하는 __EFMigrationsHistory 테이블이 추가된 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40769-170">You'll notice the addition of an __EFMigrationsHistory table that keeps track of which migrations have been applied to the database.</span></span> <span data-ttu-id="40769-171">해당 테이블의 데이터를 보면 첫 번째 마이그레이션에 대해 한 행이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="40769-171">View the data in that table and you'll see one row for the first migration.</span></span> <span data-ttu-id="40769-172">(앞의 CLI 출력 예제의 마지막 로그는 이 행을 만드는 INSERT 문을 보여 줍니다.)</span><span class="sxs-lookup"><span data-stu-id="40769-172">(The last log in the preceding CLI output example shows the INSERT statement that creates this row.)</span></span>

<span data-ttu-id="40769-173">응용 프로그램을 실행하여 모든 항목이 여전히 이전과 동일하게 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="40769-173">Run the application to verify that everything still works the same as before.</span></span>

![학생 인덱스 페이지](migrations/_static/students-index.png)

<a id="pmc"></a>
## <a name="command-line-interface-cli-vs-package-manager-console-pmc"></a><span data-ttu-id="40769-175">CLI(명령줄 인터페이스) 대 PMC(패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="40769-175">Command-line interface (CLI) vs. Package Manager Console (PMC)</span></span>

<span data-ttu-id="40769-176">마이그레이션 관리를 위한 EF 도구는 Visual Studio **PMC(패키지 관리자 콘솔)** 에서 PowerShell cmdlet 또는 .NET Core CLI 명령에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40769-176">The EF tooling for managing migrations is available from .NET Core CLI commands or from PowerShell cmdlets in the Visual Studio **Package Manager Console** (PMC) window.</span></span> <span data-ttu-id="40769-177">이 자습서에는 CLI를 사용하는 방법이 나와 있지만 원하는 경우에 PMC를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40769-177">This tutorial shows how to use the CLI, but you can use the PMC if you prefer.</span></span>

<span data-ttu-id="40769-178">PMC 명령을 위한 EF 명령은 [Microsoft.EntityFrameworkCore.Tools](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools) 패키지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40769-178">The EF commands for the PMC commands are in the [Microsoft.EntityFrameworkCore.Tools](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools) package.</span></span> <span data-ttu-id="40769-179">이 패키지는 이미 [Microsoft.AspNetCore.All](xref:fundamentals/metapackage) 메타패키지에 포함되어 있으므로 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="40769-179">This package is already included in the [Microsoft.AspNetCore.All](xref:fundamentals/metapackage) metapackage, so you don't have to install it.</span></span>

<span data-ttu-id="40769-180">**중요:** *.csproj* 파일을 편집하여 CLI에 대해 설치한 것과는 다른 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="40769-180">**Important:** This isn't the same package as the one you install for the CLI by editing the *.csproj* file.</span></span> <span data-ttu-id="40769-181">끝이 `Tools.DotNet`으로 끝나는 CLI 패키지 이름과 달리 이름이 `Tools`로 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="40769-181">The name of this one ends in `Tools`, unlike the CLI package name which ends in `Tools.DotNet`.</span></span>

<span data-ttu-id="40769-182">CLI 명령에 대한 자세한 내용은 [.NET Core CLI](https://docs.microsoft.com/ef/core/miscellaneous/cli/dotnet)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40769-182">For more information about the CLI commands, see [.NET Core CLI](https://docs.microsoft.com/ef/core/miscellaneous/cli/dotnet).</span></span>

<span data-ttu-id="40769-183">PMC 명령에 대한 자세한 내용은 [패키지 관리자 콘솔(Visual Studio)](https://docs.microsoft.com/ef/core/miscellaneous/cli/powershell)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40769-183">For more information about the PMC commands, see [Package Manager Console (Visual Studio)](https://docs.microsoft.com/ef/core/miscellaneous/cli/powershell).</span></span>

## <a name="summary"></a><span data-ttu-id="40769-184">요약</span><span class="sxs-lookup"><span data-stu-id="40769-184">Summary</span></span>

<span data-ttu-id="40769-185">이 자습서에서는 첫 번째 마이그레이션을 만들고 적용하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="40769-185">In this tutorial, you've seen how to create and apply your first migration.</span></span> <span data-ttu-id="40769-186">다음 자습서에서는 데이터 모델을 확장하여 더 많은 고급 항목을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="40769-186">In the next tutorial, you'll begin looking at more advanced topics by expanding the data model.</span></span> <span data-ttu-id="40769-187">방식에 따라 추가 마이그레이션을 만들고 적용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40769-187">Along the way you'll create and apply additional migrations.</span></span>
::: moniker-end

> [!div class="step-by-step"]
> <span data-ttu-id="40769-188">[이전](sort-filter-page.md)
> [다음](complex-data-model.md)</span><span class="sxs-lookup"><span data-stu-id="40769-188">[Previous](sort-filter-page.md)
[Next](complex-data-model.md)</span></span>
