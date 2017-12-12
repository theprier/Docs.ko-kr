---
title: "EF 코어 8-마이그레이션-4 사용 하 여 razor 페이지"
author: rick-anderson
description: "이 자습서에서는 ASP.NET Core MVC 응용 프로그램에서 데이터 모델 변경 내용을 관리 하기 위한 EF 코어 마이그레이션 기능을 사용 하 여 시작 합니다."
keywords: "ASP.NET Core, Entity Framework Core, 마이그레이션"
ms.author: riande
manager: wpickett
ms.date: 10/15/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: data/ef-rp/migrations
ms.openlocfilehash: 8549fc522bcd05a5755a449cd6d4b655f00d998b
ms.sourcegitcommit: 6e46abd65973dea796d364a514de9ec2e3e1c1ed
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2017
---
# <a name="migrations---ef-core-with-razor-pages-tutorial-4-of-8"></a><span data-ttu-id="652c3-104">마이그레이션-EF 코어 Razor 페이지 자습서 (8 4)</span><span class="sxs-lookup"><span data-stu-id="652c3-104">Migrations - EF Core with Razor Pages tutorial (4 of 8)</span></span>

<span data-ttu-id="652c3-105">여 [Tom Dykstra](https://github.com/tdykstra), [Jon P Smith](https://twitter.com/thereformedprog), 및 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="652c3-105">By [Tom Dykstra](https://github.com/tdykstra), [Jon P Smith](https://twitter.com/thereformedprog), and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE[about the series](../../includes/RP-EF/intro.md)]

<span data-ttu-id="652c3-106">이 자습서에서는 데이터 모델 변경 내용을 관리 하기 위한 EF 핵심 마이그레이션 기능이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-106">In this tutorial, the EF Core migrations feature for managing data model changes is used.</span></span>

<span data-ttu-id="652c3-107">문제를 해결할 수 없는를 실행 하는 경우 다운로드는 [이 단계에 대 한 완성 된 앱](
https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part4-migrations)합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-107">If you run into problems you can't solve, download the [completed app for this stage](
https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part4-migrations).</span></span>

<span data-ttu-id="652c3-108">새 응용 프로그램 개발 된 데이터 변경 내용을 자주 모델링 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-108">When a new app is developed, the data model changes frequently.</span></span> <span data-ttu-id="652c3-109">될 때마다 모델 변경 내용을 모델이 가져옵니다 데이터베이스와 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-109">Each time the model changes, the model gets out of sync with the database.</span></span> <span data-ttu-id="652c3-110">이 자습서를 존재 하지 않는 경우 데이터베이스를 만들려면 Entity Framework를 구성 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-110">This tutorial started by configuring the Entity Framework to create the database if it doesn't exist.</span></span> <span data-ttu-id="652c3-111">데이터 모델이 변경 될 때마다:</span><span class="sxs-lookup"><span data-stu-id="652c3-111">Each time the data model changes:</span></span>

* <span data-ttu-id="652c3-112">DB 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-112">The DB is dropped.</span></span>
* <span data-ttu-id="652c3-113">EF는 모델과 일치 하는 새 브러시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-113">EF creates a new one that matches the model.</span></span>
* <span data-ttu-id="652c3-114">응용 프로그램 테스트 데이터로 DB을 시드합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-114">The app seeds the DB with test data.</span></span>

<span data-ttu-id="652c3-115">DB 데이터 모델을 통해 동기화를 유지 하려면이 방법을 프로덕션에 앱을 배포할 때까지 잘 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-115">This approach to keeping the DB in sync with the data model works well until you deploy the app to production.</span></span> <span data-ttu-id="652c3-116">앱이 프로덕션 환경에서 실행 중인 경우 유지 관리 하는 데이터를 저장 일반적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-116">When the app is running in production, it is usually storing data that needs to be maintained.</span></span> <span data-ttu-id="652c3-117">응용 프로그램 (예: 새 열 추가) 변경 될 때마다 DB 테스트를 시작할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-117">The app can't start with a test DB each time a change is made (such as adding a new column).</span></span> <span data-ttu-id="652c3-118">EF 코어 마이그레이션 기능 EF 새 DB 만드는 대신 DB 스키마를 업데이트 하는 코어를 사용 하 여이 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-118">The EF Core Migrations feature solves this problem by enabling EF Core to update the DB schema instead of creating a new DB.</span></span>

<span data-ttu-id="652c3-119">삭제 하 고는 데이터 모델이 변경 하는 경우에 DB를 다시 만들어, 대신 마이그레이션 스키마를 업데이트 한 기존 데이터를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-119">Rather than dropping and recreating the DB when the data model changes, migrations updates the schema and retains existing data.</span></span>

## <a name="entity-framework-core-nuget-packages-for-migrations"></a><span data-ttu-id="652c3-120">마이그레이션을 위한 Entity Framework Core NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="652c3-120">Entity Framework Core NuGet packages for migrations</span></span>

<span data-ttu-id="652c3-121">마이그레이션 작업을 하려면 사용 된 **패키지 관리자 콘솔** (PMC) 또는 명령줄 인터페이스 (CLI).</span><span class="sxs-lookup"><span data-stu-id="652c3-121">To work with migrations, use the **Package Manager Console** (PMC) or the command-line interface (CLI).</span></span> <span data-ttu-id="652c3-122">이 자습서에는 CLI 명령을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-122">These tutorials show how to use CLI commands.</span></span> <span data-ttu-id="652c3-123">PMC에 대 한 정보는 [이 자습서의 최종](#pmc)합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-123">Information about the PMC is at [the end of this tutorial](#pmc).</span></span>

<span data-ttu-id="652c3-124">제공 되는 CLI (명령줄 인터페이스)에 대 한 EF 핵심 도구 [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet)합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-124">The EF Core tools for the command-line interface (CLI) are provided in [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet).</span></span> <span data-ttu-id="652c3-125">이 패키지를 설치 하려면 추가 하는 `DotNetCliToolReference` 컬렉션에는 *.csproj* 표시 된 것 처럼 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-125">To install this package, add it to the `DotNetCliToolReference` collection in the *.csproj* file, as shown.</span></span> <span data-ttu-id="652c3-126">**참고:** 이 패키지를 편집 하 여 설치 해야는 *.csproj* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-126">**Note:** This package must be installed by editing the *.csproj* file.</span></span> <span data-ttu-id="652c3-127">`install-package` 이 패키지를 설치 명령이 나 패키지 관리자 GUI 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-127">The`install-package` command or the package manager GUI cannot be used to install this package.</span></span> <span data-ttu-id="652c3-128">편집 된 *.csproj* 파일에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 여 **솔루션 탐색기** 선택 하 고 **ContosoUniversity.csproj 편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-128">Edit the *.csproj* file by right-clicking the project name in **Solution Explorer** and selecting **Edit ContosoUniversity.csproj**.</span></span>

<span data-ttu-id="652c3-129">업데이트 된 다음 태그를 보여 줍니다 *.csproj* 강조 표시 EF 코어 CLI 도구 파일:</span><span class="sxs-lookup"><span data-stu-id="652c3-129">The following markup shows the updated *.csproj* file with the EF Core CLI tools highlighted:</span></span>

[!code-xml[](intro/samples/cu/ContosoUniversity.csproj?highlight=12)]
  
<span data-ttu-id="652c3-130">버전 번호를 앞의 예제 자습서 기록 될 때 최신 버전 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-130">The version numbers in the preceding example were current when the tutorial was written.</span></span> <span data-ttu-id="652c3-131">다른 패키지에는 EF 코어 CLI 도구에 대 한 동일한 버전을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-131">Use the same version for the EF Core CLI tools found in the other packages.</span></span>

## <a name="change-the-connection-string"></a><span data-ttu-id="652c3-132">연결 문자열 변경</span><span class="sxs-lookup"><span data-stu-id="652c3-132">Change the connection string</span></span>

<span data-ttu-id="652c3-133">에 *appsettings.json* 파일, DB 연결 문자열의 이름을 ContosoUniversity2로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-133">In the *appsettings.json* file, change the name of the DB in the connection string to ContosoUniversity2.</span></span>

[!code-json[Main](intro/samples/cu/appsettings2.json?range=1-4)]

<span data-ttu-id="652c3-134">연결 문자열에 DB 이름을 변경 하면 새 DB를 만들려면 첫 번째 마이그레이션이 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-134">Changing the DB name in the connection string causes the first migration to create a new DB.</span></span> <span data-ttu-id="652c3-135">해당 이름으로 존재 하지 않기 때문에 새 DB 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-135">A new DB is created because one with that name does not exist.</span></span> <span data-ttu-id="652c3-136">연결 문자열을 변경 마이그레이션을 시작 하기 위한 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-136">Changing the connection string isn't required for getting started with migrations.</span></span>

<span data-ttu-id="652c3-137">DB 이름 변경 하는 대신 DB을 삭제 하는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-137">An alternative to changing the DB name is deleting the DB.</span></span> <span data-ttu-id="652c3-138">사용 하 여 **SQL Server 개체 탐색기** (SSOX) 또는 `database drop` CLI 명령을:</span><span class="sxs-lookup"><span data-stu-id="652c3-138">Use **SQL Server Object Explorer** (SSOX) or the `database drop` CLI command:</span></span>

 ```console
 dotnet ef database drop
 ```

<span data-ttu-id="652c3-139">다음 섹션에는 CLI 명령을 실행 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-139">The following section explains how to run CLI commands.</span></span>

## <a name="create-an-initial-migration"></a><span data-ttu-id="652c3-140">초기 마이그레이션 만들기</span><span class="sxs-lookup"><span data-stu-id="652c3-140">Create an initial migration</span></span>

<span data-ttu-id="652c3-141">프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-141">Build the project.</span></span>

<span data-ttu-id="652c3-142">명령 창을 열고 프로젝트 폴더로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-142">Open a command window and navigate to the project folder.</span></span> <span data-ttu-id="652c3-143">프로젝트 폴더에 포함 된 *Startup.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-143">The project folder contains the *Startup.cs* file.</span></span>

<span data-ttu-id="652c3-144">명령 창에서 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-144">Enter the following in the command window:</span></span>

```console
dotnet ef migrations add InitialCreate
```

<span data-ttu-id="652c3-145">명령 창에는 다음과 유사한 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-145">The command window displays information similar to the following:</span></span>

```console
info: Microsoft.AspNetCore.DataProtection.KeyManagement.XmlKeyManager[0]
      User profile is available. Using 'C:\Users\username\AppData\Local\ASP.NET\DataProtection-Keys' as key repository and Windows DPAPI to encrypt keys at rest.
info: Microsoft.EntityFrameworkCore.Infrastructure[100403]
      Entity Framework Core 2.0.0-rtm-26452 initialized 'SchoolContext' using provider 'Microsoft.EntityFrameworkCore.SqlServer' with options: None
Done. To undo this action, use 'ef migrations remove'
```

<span data-ttu-id="652c3-146">메시지와 함께 마이그레이션이 실패할 경우 "*... 파일에 액세스할 수 없습니다 ContosoUniversity.dll 다른 프로세스에서 사용 되 고 있으므로 합니다.* "</span><span class="sxs-lookup"><span data-stu-id="652c3-146">If the migration fails with the message "*cannot access the file ... ContosoUniversity.dll because it is being used by another process.*"</span></span> <span data-ttu-id="652c3-147">표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-147">is displayed:</span></span>

* <span data-ttu-id="652c3-148">IIS Express를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-148">Stop IIS Express.</span></span>

   * <span data-ttu-id="652c3-149">종료 하 고 Visual Studio를 다시 시작 또는</span><span class="sxs-lookup"><span data-stu-id="652c3-149">Exit and restart Visual Studio, or</span></span>
   * <span data-ttu-id="652c3-150">Windows 시스템 트레이에서 아이콘을 IIS Express를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-150">Find the IIS Express icon in the Windows System Tray.</span></span>
   * <span data-ttu-id="652c3-151">IIS Express 아이콘을 마우스 오른쪽 단추로 누른 **ContosoUniversity > 사이트 중지**합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-151">Right-click the IIS Express icon, and then click **ContosoUniversity > Stop Site**.</span></span>

<span data-ttu-id="652c3-152">오류 메시지 "빌드 실패 했습니다." 하는 경우</span><span class="sxs-lookup"><span data-stu-id="652c3-152">If the error message "Build failed."</span></span> <span data-ttu-id="652c3-153">가 표시 된 명령을 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-153">is displayed, run the command again.</span></span> <span data-ttu-id="652c3-154">이 오류가 발생할 경우이 자습서의 맨 아래에 메모를 둡니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-154">If you get this error, leave a note at the bottom of this tutorial.</span></span>

### <a name="examine-the-up-and-down-methods"></a><span data-ttu-id="652c3-155">위쪽을 검토 하 고 아래쪽 메서드</span><span class="sxs-lookup"><span data-stu-id="652c3-155">Examine the Up and Down methods</span></span>

<span data-ttu-id="652c3-156">EF 코어 명령 `migrations add` DB에서 만드는 코드를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-156">The EF Core command `migrations add` generated code to create the DB from.</span></span> <span data-ttu-id="652c3-157">이 마이그레이션 코드에는 *마이그레이션\<타임 스탬프 > _InitialCreate.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-157">This migrations code is in the *Migrations\<timestamp>_InitialCreate.cs* file.</span></span> <span data-ttu-id="652c3-158">`Up` 의 메서드는 `InitialCreate` 클래스는 데이터 모델 엔터티 집합에 해당 하는 DB 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-158">The `Up` method of the `InitialCreate` class creates the DB tables that correspond to the data model entity sets.</span></span> <span data-ttu-id="652c3-159">`Down` 다음 예제와 같이, 메서드 삭제:</span><span class="sxs-lookup"><span data-stu-id="652c3-159">The `Down` method deletes them, as shown in the following example:</span></span>

[!code-csharp[Main](intro/samples/cu/Migrations/20171026010210_InitialCreate.cs?range=8-24,77-)]

<span data-ttu-id="652c3-160">마이그레이션 호출은 `Up` 마이그레이션에 대 한 데이터 모델 변경 내용을 구현 하려면 메서드.</span><span class="sxs-lookup"><span data-stu-id="652c3-160">Migrations calls the `Up` method to implement the data model changes for a migration.</span></span> <span data-ttu-id="652c3-161">Update, 마이그레이션 호출을 롤백해야 하는 명령을 입력할 때는 `Down` 메서드.</span><span class="sxs-lookup"><span data-stu-id="652c3-161">When you enter a command to roll back the update, migrations calls the `Down` method.</span></span>

<span data-ttu-id="652c3-162">위의 코드는 초기 마이그레이션에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-162">The preceding code is for the initial migration.</span></span> <span data-ttu-id="652c3-163">해당 코드를 만든 경우의 `migrations add InitialCreate` 명령이 실행 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-163">That code was created when the `migrations add InitialCreate` command was run.</span></span> <span data-ttu-id="652c3-164">마이그레이션 name 매개 변수 (이 예제에서 "InitialCreate")는 파일 이름에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-164">The migration name parameter ("InitialCreate" in the example) is used for the file name.</span></span> <span data-ttu-id="652c3-165">유효한 파일 이름을 마이그레이션 이름일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-165">The migration name can be any valid file name.</span></span> <span data-ttu-id="652c3-166">단어 또는 구를 마이그레이션에서 수행 되는 것을 요약 하는 선택 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-166">It's best to choose a word or phrase that summarizes what is being done in the migration.</span></span> <span data-ttu-id="652c3-167">예를 들어 department 테이블을 추가 하는 마이그레이션 파일명 "AddDepartmentTable."</span><span class="sxs-lookup"><span data-stu-id="652c3-167">For example, a migration that added a department table might be called "AddDepartmentTable."</span></span>

<span data-ttu-id="652c3-168">초기 마이그레이션 만들어지고 DB 종료 될 경우:</span><span class="sxs-lookup"><span data-stu-id="652c3-168">If the initial migration is created and the DB exits:</span></span>

* <span data-ttu-id="652c3-169">DB 만들기 코드가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-169">The DB creation code is generated.</span></span>
* <span data-ttu-id="652c3-170">DB 만들기 코드 DB에 이미 데이터 모델 일치 하기 때문에 실행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-170">The DB creation code doesn't need to run because the DB already matches the data model.</span></span> <span data-ttu-id="652c3-171">DB 만들기 코드를 실행 하는 경우에 DB에 이미 데이터 모델 일치 하기 때문에 변경 내용을 확인 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-171">If the The DB creation code is run, it doesn't make any changes because the DB already matches the data model.</span></span>

<span data-ttu-id="652c3-172">응용 프로그램을 새 환경에 배포 될 때 DB 만들려고 DB 생성 코드를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-172">When the app is deployed to a new environment, the DB creation code must be run to create the DB.</span></span>

<span data-ttu-id="652c3-173">이전에 DB에 대 한 새 이름을 사용 하도록 연결 문자열이 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-173">Previously the connection string was changed to use a new name for the DB.</span></span> <span data-ttu-id="652c3-174">지정 된 DB 존재 하지 않습니다 마이그레이션 DB를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-174">The specified DB doesn't exist, so migrations creates the DB.</span></span>

### <a name="examine-the-data-model-snapshot"></a><span data-ttu-id="652c3-175">데이터 모델 스냅숏을 검사합니다</span><span class="sxs-lookup"><span data-stu-id="652c3-175">Examine the data model snapshot</span></span>

<span data-ttu-id="652c3-176">마이그레이션 만듭니다는 *스냅숏* 에 현재 DB 스키마의 *Migrations/SchoolContextModelSnapshot.cs*:</span><span class="sxs-lookup"><span data-stu-id="652c3-176">Migrations creates a *snapshot* of the current DB schema in *Migrations/SchoolContextModelSnapshot.cs*:</span></span>

[!code-csharp[Main](intro/samples/cu/Migrations/SchoolContextModelSnapshot1.cs?name=snippet_Truncate)]

<span data-ttu-id="652c3-177">현재 DB 스키마 코드에 표시 되므로, EF 코어 마이그레이션 만들려는 DB 상호 작용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-177">Because the current DB schema is represented in code, EF Core doesn't have to interact with the DB to create migrations.</span></span> <span data-ttu-id="652c3-178">마이그레이션에 추가 하면 EF 코어 스냅숏 파일에 데이터 모델을 비교 하 여 변경 내용을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-178">When you add a migration, EF Core determines what changed by comparing the data model to the snapshot file.</span></span> <span data-ttu-id="652c3-179">DB 업데이트 해야 하는 경우에 EF 코어 DB 상호 작용 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-179">EF Core interacts with the DB only when it has to update the DB.</span></span>

<span data-ttu-id="652c3-180">스냅숏 파일을 만든 마이그레이션과 함께 동기화 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-180">The snapshot file must be in sync with the migrations that created it.</span></span> <span data-ttu-id="652c3-181">마이그레이션 라는 파일을 삭제 하 여 제거할 수 없습니다  *\<타임 스탬프 > _\<migrationname >.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-181">A migration can't be removed by deleting the file named *\<timestamp>_\<migrationname>.cs*.</span></span> <span data-ttu-id="652c3-182">해당 파일을 삭제 하는 경우 나머지 마이그레이션은 DB 스냅숏 파일과 함께 동기화 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-182">If that file is deleted, the remaining migrations are out of sync with the DB snapshot file.</span></span> <span data-ttu-id="652c3-183">사용 하 여 추가 하는 마지막 마이그레이션을 삭제 하려면는 [dotnet ef 마이그레이션 제거](https://docs.microsoft.com/ef/core/miscellaneous/cli/dotnet#dotnet-ef-migrations-remove) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-183">To delete the last migration added, use the [dotnet ef migrations remove](https://docs.microsoft.com/ef/core/miscellaneous/cli/dotnet#dotnet-ef-migrations-remove) command.</span></span>

## <a name="remove-ensurecreated"></a><span data-ttu-id="652c3-184">EnsureCreated 제거</span><span class="sxs-lookup"><span data-stu-id="652c3-184">Remove EnsureCreated</span></span>

<span data-ttu-id="652c3-185">초기 개발 작업에 `EnsureCreated` 명령이 사용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-185">For early development, the `EnsureCreated` command was used.</span></span> <span data-ttu-id="652c3-186">이 자습서에서는 마이그레이션은 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-186">In this tutorial, migrations is used.</span></span> <span data-ttu-id="652c3-187">`EnsureCreated`다음 limatitions에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-187">`EnsureCreated` has the following limatitions:</span></span>

* <span data-ttu-id="652c3-188">마이그레이션을 무시 하 고 DB 및 스키마를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-188">Bypasses migrations and creates the DB and schema.</span></span>
* <span data-ttu-id="652c3-189">마이그레이션 테이블을 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-189">Does not create a migrations table.</span></span>
* <span data-ttu-id="652c3-190">수 *하지* 마이그레이션과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-190">Can *not* be used with migrations.</span></span>
* <span data-ttu-id="652c3-191">위한 테스트, 신속한 프로토타입 DB을 삭제 하 고 다시 자주를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-191">Is designed for testing or rapid prototyping where the DB is dropped and re-created frequently.</span></span>

<span data-ttu-id="652c3-192">다음 줄을 제거 `DbInitializer`:</span><span class="sxs-lookup"><span data-stu-id="652c3-192">Remove the following line from `DbInitializer`:</span></span>

```csharp
context.Database.EnsureCreated();
```

## <a name="apply-the-migration-to-the-db-in-development"></a><span data-ttu-id="652c3-193">마이그레이션 개발에서 DB에 적용</span><span class="sxs-lookup"><span data-stu-id="652c3-193">Apply the migration to the DB in development</span></span>

<span data-ttu-id="652c3-194">명령 창에서 DB 및 테이블을 만들려면 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-194">In the command window, enter the following to create the DB and tables.</span></span>

```console
dotnet ef database update
```

<span data-ttu-id="652c3-195">참고: 경우는 `update` 명령은 "실패 한 빌드 합니다." 오류 반환:</span><span class="sxs-lookup"><span data-stu-id="652c3-195">Note: If the `update` command returns the error "Build failed.":</span></span>

* <span data-ttu-id="652c3-196">명령을 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-196">Run the command again.</span></span>
* <span data-ttu-id="652c3-197">다시 실패 하는 경우 Visual Studio를 종료 한 후 실행 된 `update` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-197">If it fails again, exit Visual Studio and then run the `update` command.</span></span>
* <span data-ttu-id="652c3-198">페이지의 맨 아래에 메시지를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-198">Leave a message at the bottom of the page.</span></span>

<span data-ttu-id="652c3-199">명령의 출력은는 `migrations add` 출력 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-199">The output from the command is similar to the `migrations add` command output.</span></span> <span data-ttu-id="652c3-200">이전 명령에서 DB를 설정 하는 SQL 명령에 대 한 로그 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-200">In the preceding command, logs for the SQL commands that set up the DB are displayed.</span></span> <span data-ttu-id="652c3-201">대부분의 로그는 다음 예제 출력에서 생략 됩니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-201">Most of the logs are omitted in the following sample output:</span></span>

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

<span data-ttu-id="652c3-202">로그 메시지의 세부 수준을 줄이려면에서 로그 수준을 변경할 수는 *appsettings 합니다. Development.json* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-202">To reduce the level of detail in log messages, can change the log levels in the *appsettings.Development.json* file.</span></span> <span data-ttu-id="652c3-203">자세한 내용은 참조 [로깅 소개](xref:fundamentals/logging/index)합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-203">For more information, see [Introduction to logging](xref:fundamentals/logging/index).</span></span>

<span data-ttu-id="652c3-204">사용 하 여 **SQL Server 개체 탐색기** DB를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-204">Use **SQL Server Object Explorer** to inspect the DB.</span></span> <span data-ttu-id="652c3-205">추가 확인 프로그램 `__EFMigrationsHistory` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-205">Notice the addition of an `__EFMigrationsHistory` table.</span></span> <span data-ttu-id="652c3-206">`__EFMigrationsHistory` DB에 적용 된 마이그레이션이 테이블의 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-206">The `__EFMigrationsHistory` table keeps track of which migrations have been applied to the DB.</span></span> <span data-ttu-id="652c3-207">데이터를 볼는 `__EFMigrationsHistory` 테이블을 첫 번째 마이그레이션에 한 행씩 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-207">View the data in the `__EFMigrationsHistory` table, it shows one row for the first migration.</span></span> <span data-ttu-id="652c3-208">마지막 로그 CLI 출력 앞의 예제에서이 행을 만들고 INSERT 문을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-208">The last log in the preceding CLI output example shows the INSERT statement that creates this row.</span></span>

<span data-ttu-id="652c3-209">응용 프로그램을 실행 하 고 작동 하는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-209">Run the app and verify that everything works.</span></span>

## <a name="appling-migrations-in-production"></a><span data-ttu-id="652c3-210">프로덕션 환경에서 적용 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="652c3-210">Appling migrations in production</span></span>

<span data-ttu-id="652c3-211">프로덕션 응용 프로그램 해야 하는 것이 좋습니다 **하지** 호출 [Database.Migrate](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.relationaldatabasefacadeextensions.migrate?view=efcore-2.0#Microsoft_EntityFrameworkCore_RelationalDatabaseFacadeExtensions_Migrate_Microsoft_EntityFrameworkCore_Infrastructure_DatabaseFacade_) 응용 프로그램 시작 시.</span><span class="sxs-lookup"><span data-stu-id="652c3-211">We recommend production apps should **not** call [Database.Migrate](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.relationaldatabasefacadeextensions.migrate?view=efcore-2.0#Microsoft_EntityFrameworkCore_RelationalDatabaseFacadeExtensions_Migrate_Microsoft_EntityFrameworkCore_Infrastructure_DatabaseFacade_) at application startup.</span></span> <span data-ttu-id="652c3-212">`Migrate`서버 팜의 응용 프로그램에서 호출할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-212">`Migrate` should not be called from an app in server farm.</span></span> <span data-ttu-id="652c3-213">예를 들어, 응용 프로그램 (앱의 여러 인스턴스가 실행 중인) 확장을 사용 하 여 배포 하는 클라우드 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-213">For example, if the app has been cloud deployed with scale-out (multiple instances of the app are running).</span></span>

<span data-ttu-id="652c3-214">데이터베이스 마이그레이션 제어 되는 방식에서 및 배포의 일부로 수행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-214">Database migration should be done as part of deployment, and in a controlled way.</span></span> <span data-ttu-id="652c3-215">프로덕션 데이터베이스 마이그레이션 방법 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-215">Production database migration approaches include:</span></span>

* <span data-ttu-id="652c3-216">마이그레이션을 사용 하 여 SQL 스크립트를 작성 및 배포에서 SQL 스크립트를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-216">Using migrations to create SQL scripts and using the SQL scripts in deployment.</span></span>
* <span data-ttu-id="652c3-217">실행 `dotnet ef database update` 제어 된 환경에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-217">Running `dotnet ef database update` from a controlled environment.</span></span>

<span data-ttu-id="652c3-218">사용 하 여 EF 코어는 `__MigrationsHistory` 테이블을 참조 하는 마이그레이션을 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-218">EF Core uses the `__MigrationsHistory` table to see if any migrations need to run.</span></span> <span data-ttu-id="652c3-219">DB 최신 상태 이면 마이그레이션 없음 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-219">If the DB is up to date, no migration is run.</span></span>

<a id="pmc"></a>
## <a name="command-line-interface-cli-vs-package-manager-console-pmc"></a><span data-ttu-id="652c3-220">CLI (명령줄 인터페이스) vs입니다. 패키지 관리자 콘솔 (PMC)</span><span class="sxs-lookup"><span data-stu-id="652c3-220">Command-line interface (CLI) vs. Package Manager Console (PMC)</span></span>

<span data-ttu-id="652c3-221">EF 코어 마이그레이션 관리 하기 위한 도구에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-221">The EF Core tooling for managing migrations is available from:</span></span>

* <span data-ttu-id="652c3-222">.NET core CLI 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-222">.NET Core CLI commands.</span></span>
* <span data-ttu-id="652c3-223">Visual Studio에서 PowerShell cmdlet **패키지 관리자 콘솔** (PMC) 창.</span><span class="sxs-lookup"><span data-stu-id="652c3-223">The PowerShell cmdlets in the Visual Studio **Package Manager Console** (PMC) window.</span></span>

<span data-ttu-id="652c3-224">PMC를 사용 하 여 선호 하는 개발자도,이 자습서에는 CLI를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-224">This tutorial shows how to use the CLI, some developers prefer using the PMC.</span></span>

<span data-ttu-id="652c3-225">PMC EF 코어 주석은에 [Microsoft.EntityFrameworkCore.Tools](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools) 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-225">The EF Core commands for the PMC are in the [Microsoft.EntityFrameworkCore.Tools](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools) package.</span></span> <span data-ttu-id="652c3-226">이 패키지에 포함 되어는 [Microsoft.AspNetCore.All](xref:fundamentals/metapackage) metapackage, 하므로 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-226">This package is included in the [Microsoft.AspNetCore.All](xref:fundamentals/metapackage) metapackage, so you don't have to install it.</span></span>

<span data-ttu-id="652c3-227">**중요:** 이 동일한 패키지를 편집 하 여 CLI를 설치 하는 것과는 *.csproj* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-227">**Important:** This is not the same package as the one you install for the CLI by editing the *.csproj* file.</span></span> <span data-ttu-id="652c3-228">이 개체의 이름이 끝나는 `Tools`, CLI 패키지 이름에는 달리 `Tools.DotNet`합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-228">The name of this one ends in `Tools`, unlike the CLI package name which ends in `Tools.DotNet`.</span></span>

<span data-ttu-id="652c3-229">CLI 명령에 대 한 자세한 내용은 참조 [.NET Core CLI](https://docs.microsoft.com/ef/core/miscellaneous/cli/dotnet)합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-229">For more information about the CLI commands, see [.NET Core CLI](https://docs.microsoft.com/ef/core/miscellaneous/cli/dotnet).</span></span>

<span data-ttu-id="652c3-230">PMC 명령에 대 한 자세한 내용은 참조 [패키지 관리자 콘솔 (Visual Studio)](https://docs.microsoft.com/ef/core/miscellaneous/cli/powershell)합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-230">For more information about the PMC commands, see [Package Manager Console (Visual Studio)](https://docs.microsoft.com/ef/core/miscellaneous/cli/powershell).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="652c3-231">문제 해결</span><span class="sxs-lookup"><span data-stu-id="652c3-231">Troubleshooting</span></span>

<span data-ttu-id="652c3-232">다운로드는 [이 단계에 대 한 완성 된 앱](
https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part4-migrations)합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-232">Download the [completed app for this stage](
https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part4-migrations).</span></span>

<span data-ttu-id="652c3-233">응용 프로그램에서는 다음과 같은 예외가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-233">The app generates the following exception:</span></span>

```text
`SqlException: Cannot open database "ContosoUniversity" requested by the login.
The login failed.
Login failed for user 'user name'.
```

<span data-ttu-id="652c3-234">솔루션: 실행`dotnet ef database update`</span><span class="sxs-lookup"><span data-stu-id="652c3-234">Solution: Run `dotnet ef database update`</span></span>

<span data-ttu-id="652c3-235">경우는 `update` 명령은 "실패 한 빌드 합니다." 오류 반환:</span><span class="sxs-lookup"><span data-stu-id="652c3-235">If the `update` command returns the error "Build failed.":</span></span>

* <span data-ttu-id="652c3-236">명령을 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-236">Run the command again.</span></span>
* <span data-ttu-id="652c3-237">페이지의 맨 아래에 메시지를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="652c3-237">Leave a message at the bottom of the page.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="652c3-238">[이전](xref:data/ef-rp/sort-filter-page)
[다음](xref:data/ef-rp/complex-data-model)</span><span class="sxs-lookup"><span data-stu-id="652c3-238">[Previous](xref:data/ef-rp/sort-filter-page)
[Next](xref:data/ef-rp/complex-data-model)</span></span>
