---
title: ASP.NET Core에서 EF Core를 사용한 Razor 페이지 - 마이그레이션 - 4/8
author: rick-anderson
description: 이 자습서에서는 ASP.NET Core MVC 앱에서 데이터 모델 변경 관리를 위해 EF Core 마이그레이션 기능을 사용하는 것을 시작합니다.
ms.author: riande
ms.date: 10/15/2017
uid: data/ef-rp/migrations
ms.openlocfilehash: d39e1aa40ff97d5b335f2bde6170242e89f6189a
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36272350"
---
# <a name="razor-pages-with-ef-core-in-aspnet-core---migrations---4-of-8"></a><span data-ttu-id="7a6f9-103">ASP.NET Core에서 EF Core를 사용한 Razor 페이지 - 마이그레이션 - 4/8</span><span class="sxs-lookup"><span data-stu-id="7a6f9-103">Razor Pages with EF Core in ASP.NET Core - Migrations - 4 of 8</span></span>

<span data-ttu-id="7a6f9-104">작성자: [Tom Dykstra](https://github.com/tdykstra), [Jon P Smith](https://twitter.com/thereformedprog) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="7a6f9-104">By [Tom Dykstra](https://github.com/tdykstra), [Jon P Smith](https://twitter.com/thereformedprog), and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [about the series](../../includes/RP-EF/intro.md)]

<span data-ttu-id="7a6f9-105">이 자습서에서는 데이터 모델 변경 관리를 위한 EF Core 마이그레이션 기능이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-105">In this tutorial, the EF Core migrations feature for managing data model changes is used.</span></span>

<span data-ttu-id="7a6f9-106">해결할 수 없는 문제가 발생한 경우 [이 단계에 완성된 앱](
https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part4-migrations)을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-106">If you run into problems you can't solve, download the [completed app for this stage](
https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part4-migrations).</span></span>

<span data-ttu-id="7a6f9-107">새 앱이 개발되면 데이터 모델이 자주 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-107">When a new app is developed, the data model changes frequently.</span></span> <span data-ttu-id="7a6f9-108">모델이 변경될 때마다 모델이 데이터베이스와 동기화 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-108">Each time the model changes, the model gets out of sync with the database.</span></span> <span data-ttu-id="7a6f9-109">이 자습서는 존재하지 않는 경우 데이터베이스를 만들도록 Entity Framework를 구성하여 시작되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-109">This tutorial started by configuring the Entity Framework to create the database if it doesn't exist.</span></span> <span data-ttu-id="7a6f9-110">데이터 모델이 변경될 때마다 다음이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-110">Each time the data model changes:</span></span>

* <span data-ttu-id="7a6f9-111">DB가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-111">The DB is dropped.</span></span>
* <span data-ttu-id="7a6f9-112">EF는 모델과 일치하는 새 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-112">EF creates a new one that matches the model.</span></span>
* <span data-ttu-id="7a6f9-113">앱은 테스트 데이터로 DB를 시드합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-113">The app seeds the DB with test data.</span></span>

<span data-ttu-id="7a6f9-114">DB를 데이터 모델과 동기화된 상태로 유지하는 이 접근 방식은 앱을 프로덕션 환경에 배포할 때까지 잘 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-114">This approach to keeping the DB in sync with the data model works well until you deploy the app to production.</span></span> <span data-ttu-id="7a6f9-115">앱이 프로덕션 환경에서 실행 중인 경우 일반적으로 유지 관리해야 하는 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-115">When the app is running in production, it's usually storing data that needs to be maintained.</span></span> <span data-ttu-id="7a6f9-116">앱은 변경(예: 새 열 추가)될 때마다 테스트 DB로 시작될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-116">The app can't start with a test DB each time a change is made (such as adding a new column).</span></span> <span data-ttu-id="7a6f9-117">EF Core 마이그레이션 기능은 EF Core에서 새 DB를 만드는 대신 DB 스키마를 업데이트하도록 하여 이 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-117">The EF Core Migrations feature solves this problem by enabling EF Core to update the DB schema instead of creating a new DB.</span></span>

<span data-ttu-id="7a6f9-118">데이터 모델이 변경될 때 DB를 삭제하고 다시 작성하는 대신 마이그레이션은 스키마를 업데이트하고 기존 데이터를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-118">Rather than dropping and recreating the DB when the data model changes, migrations updates the schema and retains existing data.</span></span>

## <a name="entity-framework-core-nuget-packages-for-migrations"></a><span data-ttu-id="7a6f9-119">마이그레이션을 위한 Entity Framework Core NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="7a6f9-119">Entity Framework Core NuGet packages for migrations</span></span>

<span data-ttu-id="7a6f9-120">마이그레이션 작업을 위해 **PMC(패키지 관리자 콘솔)** 또는 CLI(명령줄 인터페이스)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-120">To work with migrations, use the **Package Manager Console** (PMC) or the command-line interface (CLI).</span></span> <span data-ttu-id="7a6f9-121">이 자습서에는 CLI 명령을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-121">These tutorials show how to use CLI commands.</span></span> <span data-ttu-id="7a6f9-122">PMC에 대한 정보는 [이 자습서의 끝](#pmc)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-122">Information about the PMC is at [the end of this tutorial](#pmc).</span></span>

<span data-ttu-id="7a6f9-123">CLI(명령줄 인터페이스)용 EF Core 도구는 [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet)에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-123">The EF Core tools for the command-line interface (CLI) are provided in [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet).</span></span> <span data-ttu-id="7a6f9-124">이 패키지를 설치하려면 표시된 것처럼 *.csproj* 파일의 `DotNetCliToolReference` 컬렉션에 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-124">To install this package, add it to the `DotNetCliToolReference` collection in the *.csproj* file, as shown.</span></span> <span data-ttu-id="7a6f9-125">**참고:** *.csproj* 파일을 편집하여 이 패키지를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-125">**Note:** This package must be installed by editing the *.csproj* file.</span></span> <span data-ttu-id="7a6f9-126">이 패키지를 설치하는 데 `install-package` 명령이나 패키지 관리자 GUI를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-126">The`install-package` command or the package manager GUI cannot be used to install this package.</span></span> <span data-ttu-id="7a6f9-127">**솔루션 탐색기**에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭하고 **ContosoUniversity.csproj 편집**을 선택하여 *.csproj* 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-127">Edit the *.csproj* file by right-clicking the project name in **Solution Explorer** and selecting **Edit ContosoUniversity.csproj**.</span></span>

<span data-ttu-id="7a6f9-128">다음 표시는 EF Core CLI 도구가 강조 표시된 업데이트된 *.csproj* 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-128">The following markup shows the updated *.csproj* file with the EF Core CLI tools highlighted:</span></span>

[!code-xml[](intro/samples/cu/ContosoUniversity.csproj?highlight=12)]
  
<span data-ttu-id="7a6f9-129">이전 예제의 버전 번호는 이 자습서가 작성된 당시의 버전 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-129">The version numbers in the preceding example were current when the tutorial was written.</span></span> <span data-ttu-id="7a6f9-130">다른 패키지에 있는 EF Core CLI 도구에 대해 동일한 버전을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-130">Use the same version for the EF Core CLI tools found in the other packages.</span></span>

## <a name="change-the-connection-string"></a><span data-ttu-id="7a6f9-131">연결 문자열 변경</span><span class="sxs-lookup"><span data-stu-id="7a6f9-131">Change the connection string</span></span>

<span data-ttu-id="7a6f9-132">*appsettings.json* 파일에서 연결 문자열의 DB 이름을 ContosoUniversity2로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-132">In the *appsettings.json* file, change the name of the DB in the connection string to ContosoUniversity2.</span></span>

[!code-json[](intro/samples/cu/appsettings2.json?range=1-4)]

<span data-ttu-id="7a6f9-133">연결 문자열에서 DB 이름을 변경하면 첫 번째 마이그레이션으로 인해 새 DB가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-133">Changing the DB name in the connection string causes the first migration to create a new DB.</span></span> <span data-ttu-id="7a6f9-134">이름이 존재하지 않으므로 새 DB가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-134">A new DB is created because one with that name doesn't exist.</span></span> <span data-ttu-id="7a6f9-135">마이그레이션을 시작하기 위해 연결 문자열을 변경하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-135">Changing the connection string isn't required for getting started with migrations.</span></span>

<span data-ttu-id="7a6f9-136">DB 이름을 변경하는 다른 방법은 DB를 삭제하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-136">An alternative to changing the DB name is deleting the DB.</span></span> <span data-ttu-id="7a6f9-137">**SSOX(SQL Server 개체 탐색기)** 또는 `database drop` CLI 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-137">Use **SQL Server Object Explorer** (SSOX) or the `database drop` CLI command:</span></span>

 ```console
 dotnet ef database drop
 ```

<span data-ttu-id="7a6f9-138">다음 섹션에서는 CLI 명령을 실행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-138">The following section explains how to run CLI commands.</span></span>

## <a name="create-an-initial-migration"></a><span data-ttu-id="7a6f9-139">초기 마이그레이션 만들기</span><span class="sxs-lookup"><span data-stu-id="7a6f9-139">Create an initial migration</span></span>

<span data-ttu-id="7a6f9-140">프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-140">Build the project.</span></span>

<span data-ttu-id="7a6f9-141">명령 창을 열고 프로젝트 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-141">Open a command window and navigate to the project folder.</span></span> <span data-ttu-id="7a6f9-142">프로젝트 폴더에는 *Startup.cs* 파일이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-142">The project folder contains the *Startup.cs* file.</span></span>

<span data-ttu-id="7a6f9-143">명령 창에서 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-143">Enter the following in the command window:</span></span>

```console
dotnet ef migrations add InitialCreate
```

<span data-ttu-id="7a6f9-144">명령 창에는 다음과 유사한 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-144">The command window displays information similar to the following:</span></span>

```console
info: Microsoft.AspNetCore.DataProtection.KeyManagement.XmlKeyManager[0]
      User profile is available. Using 'C:\Users\username\AppData\Local\ASP.NET\DataProtection-Keys' as key repository and Windows DPAPI to encrypt keys at rest.
info: Microsoft.EntityFrameworkCore.Infrastructure[100403]
      Entity Framework Core 2.0.0-rtm-26452 initialized 'SchoolContext' using provider 'Microsoft.EntityFrameworkCore.SqlServer' with options: None
Done. To undo this action, use 'ef migrations remove'
```

<span data-ttu-id="7a6f9-145">"*ContosoUniversity.dll 파일은 다른 프로세스에서 사용하고 있으므로 액세스할 수 없습니다.*"라는 메시지가 표시되고</span><span class="sxs-lookup"><span data-stu-id="7a6f9-145">If the migration fails with the message "*cannot access the file ... ContosoUniversity.dll because it is being used by another process.*"</span></span> <span data-ttu-id="7a6f9-146">마이그레이션에 실패하는 경우:</span><span class="sxs-lookup"><span data-stu-id="7a6f9-146">is displayed:</span></span>

* <span data-ttu-id="7a6f9-147">IIS Express를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-147">Stop IIS Express.</span></span>

   * <span data-ttu-id="7a6f9-148">Visual Studio를 종료하고 다시 시작하거나</span><span class="sxs-lookup"><span data-stu-id="7a6f9-148">Exit and restart Visual Studio, or</span></span>
   * <span data-ttu-id="7a6f9-149">Windows 시스템 트레이에서 IIS Express 아이콘을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-149">Find the IIS Express icon in the Windows System Tray.</span></span>
   * <span data-ttu-id="7a6f9-150">IIS Express 아이콘을 마우스 오른쪽 단추로 클릭한 후 **ContosoUniversity > 사이트 중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-150">Right-click the IIS Express icon, and then click **ContosoUniversity > Stop Site**.</span></span>

<span data-ttu-id="7a6f9-151">오류 메시지 "빌드하지 못했습니다."가</span><span class="sxs-lookup"><span data-stu-id="7a6f9-151">If the error message "Build failed."</span></span> <span data-ttu-id="7a6f9-152">표시되는 경우 명령을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-152">is displayed, run the command again.</span></span> <span data-ttu-id="7a6f9-153">이 오류가 발생할 경우 이 자습서의 맨 아래에 메모를 남깁니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-153">If you get this error, leave a note at the bottom of this tutorial.</span></span>

### <a name="examine-the-up-and-down-methods"></a><span data-ttu-id="7a6f9-154">Up 및 Down 메서드 검사</span><span class="sxs-lookup"><span data-stu-id="7a6f9-154">Examine the Up and Down methods</span></span>

<span data-ttu-id="7a6f9-155">EF Core 명령 `migrations add`로 DB를 생성하는 코드를 생성했습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-155">The EF Core command `migrations add` generated code to create the DB from.</span></span> <span data-ttu-id="7a6f9-156">이 마이그레이션 코드는 *마이그레이션\<timestamp>_InitialCreate.cs* 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-156">This migrations code is in the *Migrations\<timestamp>_InitialCreate.cs* file.</span></span> <span data-ttu-id="7a6f9-157">`InitialCreate` 클래스dml `Up` 메서드는 데이터 모델 엔터티 집합에 해당하는 DB 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-157">The `Up` method of the `InitialCreate` class creates the DB tables that correspond to the data model entity sets.</span></span> <span data-ttu-id="7a6f9-158">`Down` 메서드는 다음 예제처럼 테이블을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-158">The `Down` method deletes them, as shown in the following example:</span></span>

[!code-csharp[](intro/samples/cu/Migrations/20171026010210_InitialCreate.cs?range=8-24,77-)]

<span data-ttu-id="7a6f9-159">마이그레이션에서는 마이그레이션을 위한 데이터 모델 변경을 구현하기 위해 `Up` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-159">Migrations calls the `Up` method to implement the data model changes for a migration.</span></span> <span data-ttu-id="7a6f9-160">업데이트를 롤백하는 명령을 입력하면 마이그레이션에서 `Down` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-160">When you enter a command to roll back the update, migrations calls the `Down` method.</span></span>

<span data-ttu-id="7a6f9-161">위의 코드는 초기 마이그레이션에 대한 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-161">The preceding code is for the initial migration.</span></span> <span data-ttu-id="7a6f9-162">이 코드는 `migrations add InitialCreate` 명령을 실행할 때 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-162">That code was created when the `migrations add InitialCreate` command was run.</span></span> <span data-ttu-id="7a6f9-163">파일 이름에는 마이그레이션 이름 매개 변수(이 예제에서 "InitialCreate")가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-163">The migration name parameter ("InitialCreate" in the example) is used for the file name.</span></span> <span data-ttu-id="7a6f9-164">마이그레이션 이름은 임의의 유효한 파일 이름이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-164">The migration name can be any valid file name.</span></span> <span data-ttu-id="7a6f9-165">마이그레이션에서 수행 중인 작업을 요약한 단어 또는 구를 선택하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-165">It's best to choose a word or phrase that summarizes what is being done in the migration.</span></span> <span data-ttu-id="7a6f9-166">예를 들어 부서 테이블을 추가한 마이그레이션은 "AddDepartmentTable"이라고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-166">For example, a migration that added a department table might be called "AddDepartmentTable."</span></span>

<span data-ttu-id="7a6f9-167">초기 마이그레이션이 생성되었고 DB가 존재하는 경우:</span><span class="sxs-lookup"><span data-stu-id="7a6f9-167">If the initial migration is created and the DB exists:</span></span>

* <span data-ttu-id="7a6f9-168">DB 만들기 코드가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-168">The DB creation code is generated.</span></span>
* <span data-ttu-id="7a6f9-169">DB는 데이터 모델과 이미 일치하므로 DB 만들기 코드를 실행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-169">The DB creation code doesn't need to run because the DB already matches the data model.</span></span> <span data-ttu-id="7a6f9-170">DB 만들기 코드가 실행되면 DB가 데이터 모델과 이미 일치하므로 아무것도 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-170">If the DB creation code is run, it doesn't make any changes because the DB already matches the data model.</span></span>

<span data-ttu-id="7a6f9-171">앱이 새 환경에 배포되면 DB 만들기 코드를 실행하여 DB를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-171">When the app is deployed to a new environment, the DB creation code must be run to create the DB.</span></span>

<span data-ttu-id="7a6f9-172">이전에는 DB에 새 이름을 사용하도록 연결 문자열을 변경했습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-172">Previously the connection string was changed to use a new name for the DB.</span></span> <span data-ttu-id="7a6f9-173">지정된 DB가 존재하지 않으므로 마이그레이션에서 DB를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-173">The specified DB doesn't exist, so migrations creates the DB.</span></span>

### <a name="the-data-model-snapshot"></a><span data-ttu-id="7a6f9-174">데이터 모델 스냅숏</span><span class="sxs-lookup"><span data-stu-id="7a6f9-174">The data model snapshot</span></span>

<span data-ttu-id="7a6f9-175">마이그레이션은 현재 데이터베이스 스키마의 *스냅숏*을 *Migrations/SchoolContextModelSnapshot.cs*에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-175">Migrations creates a *snapshot* of the current database schema in *Migrations/SchoolContextModelSnapshot.cs*.</span></span> <span data-ttu-id="7a6f9-176">마이그레이션을 추가하면 EF가 데이터 모델을 스냅숏 파일과 비교하여 변경 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-176">When you add a migration, EF determines what changed by comparing the data model to the snapshot file.</span></span>

<span data-ttu-id="7a6f9-177">마이그레이션을 삭제할 때는 [dotnet ef migrations remove](https://docs.microsoft.com/ef/core/miscellaneous/cli/dotnet#dotnet-ef-migrations-remove) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-177">When deleting a migration, use the [dotnet ef migrations remove](https://docs.microsoft.com/ef/core/miscellaneous/cli/dotnet#dotnet-ef-migrations-remove) command.</span></span> <span data-ttu-id="7a6f9-178">`dotnet ef migrations remove`는 마이그레이션을 삭제하고 스냅숏이 올바르게 다시 설정되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-178">`dotnet ef migrations remove` deletes the migration and ensures the snapshot is correctly reset.</span></span>

<span data-ttu-id="7a6f9-179">스냅숏 파일을 사용하는 방법에 대한 자세한 내용은 [팀 환경의 EF Core 마이그레이션](/ef/core/managing-schemas/migrations/teams)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-179">See [EF Core Migrations in Team Environments](/ef/core/managing-schemas/migrations/teams) for more information about how the snapshot file is used.</span></span>

## <a name="remove-ensurecreated"></a><span data-ttu-id="7a6f9-180">EnsureCreated 제거</span><span class="sxs-lookup"><span data-stu-id="7a6f9-180">Remove EnsureCreated</span></span>

<span data-ttu-id="7a6f9-181">초기 개발에는 `EnsureCreated` 명령이 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-181">For early development, the `EnsureCreated` command was used.</span></span> <span data-ttu-id="7a6f9-182">이 자습서에서는 마이그레이션이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-182">In this tutorial, migrations is used.</span></span> <span data-ttu-id="7a6f9-183">`EnsureCreated`에는 다음과 같은 제한 사항이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-183">`EnsureCreated` has the following limitations:</span></span>

* <span data-ttu-id="7a6f9-184">마이그레이션을 무시하고 DB 및 스키마를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-184">Bypasses migrations and creates the DB and schema.</span></span>
* <span data-ttu-id="7a6f9-185">마이그레이션 테이블을 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-185">Doesn't create a migrations table.</span></span>
* <span data-ttu-id="7a6f9-186">마이그레이션에 사용할 수 *없습니다*.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-186">Can *not* be used with migrations.</span></span>
* <span data-ttu-id="7a6f9-187">DB를 삭제하고 자주 다시 생성하는 테스트 또는 신속한 프로토타입 만들기를 위해 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-187">Is designed for testing or rapid prototyping where the DB is dropped and re-created frequently.</span></span>

<span data-ttu-id="7a6f9-188">`DbInitializer`에서 다음 줄을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-188">Remove the following line from `DbInitializer`:</span></span>

```csharp
context.Database.EnsureCreated();
```

## <a name="apply-the-migration-to-the-db-in-development"></a><span data-ttu-id="7a6f9-189">개발 중인 DB에 마이그레이션 적용</span><span class="sxs-lookup"><span data-stu-id="7a6f9-189">Apply the migration to the DB in development</span></span>

<span data-ttu-id="7a6f9-190">명령 창에서 다음을 입력하고 DB 및 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-190">In the command window, enter the following to create the DB and tables.</span></span>

```console
dotnet ef database update
```

<span data-ttu-id="7a6f9-191">참고: `update` 명령에서 "빌드하지 못했습니다."를 반환하는 경우:</span><span class="sxs-lookup"><span data-stu-id="7a6f9-191">Note: If the `update` command returns the error "Build failed.":</span></span>

* <span data-ttu-id="7a6f9-192">명령을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-192">Run the command again.</span></span>
* <span data-ttu-id="7a6f9-193">다시 실패하는 경우 Visual Studio를 종료한 후 `update` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-193">If it fails again, exit Visual Studio and then run the `update` command.</span></span>
* <span data-ttu-id="7a6f9-194">페이지의 맨 아래에 메시지를 남깁니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-194">Leave a message at the bottom of the page.</span></span>

<span data-ttu-id="7a6f9-195">명령의 출력은는 `migrations add` 명령 출력과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-195">The output from the command is similar to the `migrations add` command output.</span></span> <span data-ttu-id="7a6f9-196">이전 명령에서 DB를 설정하는 SQL 명령에 대한 로그가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-196">In the preceding command, logs for the SQL commands that set up the DB are displayed.</span></span> <span data-ttu-id="7a6f9-197">대부분의 로그는 다음 예제 출력에서 생략됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-197">Most of the logs are omitted in the following sample output:</span></span>

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

<span data-ttu-id="7a6f9-198">로그 메시지의 세부 수준을 줄이려면 *appsettings.Development.json* 파일에서 로그 수준을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-198">To reduce the level of detail in log messages, change the log levels in the *appsettings.Development.json* file.</span></span> <span data-ttu-id="7a6f9-199">자세한 내용은 [로깅 소개](xref:fundamentals/logging/index)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-199">For more information, see [Introduction to logging](xref:fundamentals/logging/index).</span></span>

<span data-ttu-id="7a6f9-200">**SQL Server 개체 탐색기**를 사용하여 DB를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-200">Use **SQL Server Object Explorer** to inspect the DB.</span></span> <span data-ttu-id="7a6f9-201">`__EFMigrationsHistory` 테이블이 추가된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-201">Notice the addition of an `__EFMigrationsHistory` table.</span></span> <span data-ttu-id="7a6f9-202">`__EFMigrationsHistory` 테이블은 DB에 적용된 마이그레이션을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-202">The `__EFMigrationsHistory` table keeps track of which migrations have been applied to the DB.</span></span> <span data-ttu-id="7a6f9-203">`__EFMigrationsHistory` 테이블의 데이터를 보면 첫 번째 마이그레이션에 대해 한 행이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-203">View the data in the `__EFMigrationsHistory` table, it shows one row for the first migration.</span></span> <span data-ttu-id="7a6f9-204">앞의 CLI 출력 예제의 마지막 로그는 이 행을 만드는 INSERT 문을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-204">The last log in the preceding CLI output example shows the INSERT statement that creates this row.</span></span>

<span data-ttu-id="7a6f9-205">앱을 실행하고 모든 항목이 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-205">Run the app and verify that everything works.</span></span>

## <a name="applying-migrations-in-production"></a><span data-ttu-id="7a6f9-206">프로덕션 환경에서 마이그레이션 적용</span><span class="sxs-lookup"><span data-stu-id="7a6f9-206">Applying migrations in production</span></span>

<span data-ttu-id="7a6f9-207">프로덕션 앱은 응용 프로그램 시작 시 [Database.Migrate](/dotnet/api/microsoft.entityframeworkcore.relationaldatabasefacadeextensions.migrate?view=efcore-2.0#Microsoft_EntityFrameworkCore_RelationalDatabaseFacadeExtensions_Migrate_Microsoft_EntityFrameworkCore_Infrastructure_DatabaseFacade_)를 호출하지 **않는 것이** 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-207">We recommend production apps should **not** call [Database.Migrate](/dotnet/api/microsoft.entityframeworkcore.relationaldatabasefacadeextensions.migrate?view=efcore-2.0#Microsoft_EntityFrameworkCore_RelationalDatabaseFacadeExtensions_Migrate_Microsoft_EntityFrameworkCore_Infrastructure_DatabaseFacade_) at application startup.</span></span> <span data-ttu-id="7a6f9-208">서버 팜의 앱에서 `Migrate`를 호출하면 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-208">`Migrate` shouldn't be called from an app in server farm.</span></span> <span data-ttu-id="7a6f9-209">예를 들어, 앱이 스케일 아웃으로 클라우드에 배포된 경우(앱의 여러 인스턴스가 실행 중임)</span><span class="sxs-lookup"><span data-stu-id="7a6f9-209">For example, if the app has been cloud deployed with scale-out (multiple instances of the app are running).</span></span>

<span data-ttu-id="7a6f9-210">데이터베이스 마이그레이션은 배포의 일부로 제어된 방식으로 수행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-210">Database migration should be done as part of deployment, and in a controlled way.</span></span> <span data-ttu-id="7a6f9-211">프로덕션 데이터베이스 마이그레이션 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-211">Production database migration approaches include:</span></span>

* <span data-ttu-id="7a6f9-212">마이그레이션을 사용하여 SQL 스크립트를 작성하고 배포 시 SQL 스크립트 사용</span><span class="sxs-lookup"><span data-stu-id="7a6f9-212">Using migrations to create SQL scripts and using the SQL scripts in deployment.</span></span>
* <span data-ttu-id="7a6f9-213">제어된 환경에서 `dotnet ef database update` 실행</span><span class="sxs-lookup"><span data-stu-id="7a6f9-213">Running `dotnet ef database update` from a controlled environment.</span></span>

<span data-ttu-id="7a6f9-214">EF Core는 `__MigrationsHistory` 테이블을 사용하여 마이그레이션을 실행해야 하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-214">EF Core uses the `__MigrationsHistory` table to see if any migrations need to run.</span></span> <span data-ttu-id="7a6f9-215">DB가 최신 상태이면 마이그레이션이 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-215">If the DB is up to date, no migration is run.</span></span>

<a id="pmc"></a>
## <a name="command-line-interface-cli-vs-package-manager-console-pmc"></a><span data-ttu-id="7a6f9-216">CLI(명령줄 인터페이스) 및 PMC(패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="7a6f9-216">Command-line interface (CLI) vs. Package Manager Console (PMC)</span></span>

<span data-ttu-id="7a6f9-217">마이그레이션 관리를 위한 EF Core 도구는 다음에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-217">The EF Core tooling for managing migrations is available from:</span></span>

* <span data-ttu-id="7a6f9-218">.NET Core CLI 명령</span><span class="sxs-lookup"><span data-stu-id="7a6f9-218">.NET Core CLI commands.</span></span>
* <span data-ttu-id="7a6f9-219">Visual Studio **PMC(패키지 관리자 콘솔)** 창에서 PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="7a6f9-219">The PowerShell cmdlets in the Visual Studio **Package Manager Console** (PMC) window.</span></span>

<span data-ttu-id="7a6f9-220">이 자습서에서는 CLI를 사용하는 방법을 보여 주며 일부 개발자는 PMC 사용을 선호합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-220">This tutorial shows how to use the CLI, some developers prefer using the PMC.</span></span>

<span data-ttu-id="7a6f9-221">PMC용 EF Core 명령은 [Microsoft.EntityFrameworkCore.Tools](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools) 패키지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-221">The EF Core commands for the PMC are in the [Microsoft.EntityFrameworkCore.Tools](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools) package.</span></span> <span data-ttu-id="7a6f9-222">이 패키지는 [Microsoft.AspNetCore.All](xref:fundamentals/metapackage) 메타패키지에 포함되므로 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-222">This package is included in the [Microsoft.AspNetCore.All](xref:fundamentals/metapackage) metapackage, so you don't have to install it.</span></span>

<span data-ttu-id="7a6f9-223">**중요:** *.csproj* 파일을 편집하여 CLI에 대해 설치한 것과 다른 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-223">**Important:** This isn't the same package as the one you install for the CLI by editing the *.csproj* file.</span></span> <span data-ttu-id="7a6f9-224">끝이 `Tools.DotNet`으로 끝나는 CLI 패키지 이름과 달리 이름이 `Tools`로 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-224">The name of this one ends in `Tools`, unlike the CLI package name which ends in `Tools.DotNet`.</span></span>

<span data-ttu-id="7a6f9-225">CLI 명령에 대한 자세한 내용은 [.NET Core CLI](https://docs.microsoft.com/ef/core/miscellaneous/cli/dotnet)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-225">For more information about the CLI commands, see [.NET Core CLI](https://docs.microsoft.com/ef/core/miscellaneous/cli/dotnet).</span></span>

<span data-ttu-id="7a6f9-226">PMC 명령에 대한 자세한 내용은 [패키지 관리자 콘솔(Visual Studio)](https://docs.microsoft.com/ef/core/miscellaneous/cli/powershell)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-226">For more information about the PMC commands, see [Package Manager Console (Visual Studio)](https://docs.microsoft.com/ef/core/miscellaneous/cli/powershell).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="7a6f9-227">문제 해결</span><span class="sxs-lookup"><span data-stu-id="7a6f9-227">Troubleshooting</span></span>

<span data-ttu-id="7a6f9-228">[이 단계에 대해 완성된 앱](
https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part4-migrations)을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-228">Download the [completed app for this stage](
https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part4-migrations).</span></span>

<span data-ttu-id="7a6f9-229">앱에서는 다음과 같은 예외가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-229">The app generates the following exception:</span></span>

```text
SqlException: Cannot open database "ContosoUniversity" requested by the login.
The login failed.
Login failed for user 'user name'.
```

<span data-ttu-id="7a6f9-230">해결 방법: `dotnet ef database update`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-230">Solution: Run `dotnet ef database update`</span></span>

<span data-ttu-id="7a6f9-231">`update` 명령에서 "빌드하지 못했습니다."를 반환하는 경우:</span><span class="sxs-lookup"><span data-stu-id="7a6f9-231">If the `update` command returns the error "Build failed.":</span></span>

* <span data-ttu-id="7a6f9-232">명령을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-232">Run the command again.</span></span>
* <span data-ttu-id="7a6f9-233">페이지의 맨 아래에 메시지를 남깁니다.</span><span class="sxs-lookup"><span data-stu-id="7a6f9-233">Leave a message at the bottom of the page.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7a6f9-234">[이전](xref:data/ef-rp/sort-filter-page)
> [다음](xref:data/ef-rp/complex-data-model)</span><span class="sxs-lookup"><span data-stu-id="7a6f9-234">[Previous](xref:data/ef-rp/sort-filter-page)
[Next](xref:data/ef-rp/complex-data-model)</span></span>
