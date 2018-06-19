---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
title: 'SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: SQL Server 데이터베이스 업데이트-11/12 배포 | Microsoft Docs'
author: tdykstra
description: 이 일련의 자습서 배포 하는 방법을 보여 줍니다. (게시) ASP.NET Visual Stu를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/17/2011
ms.topic: article
ms.assetid: 5e2bb092-cb22-4511-ad0a-22ae12dd99b3
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
msc.type: authoredcontent
ms.openlocfilehash: d8cc072c631900937f31c8f2637869b53d46cf54
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30887332"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-sql-server-database-update---11-of-12"></a><span data-ttu-id="e687c-103">SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: SQL Server 데이터베이스 업데이트-12 11를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Deploying a SQL Server Database Update - 11 of 12</span></span>
====================
<span data-ttu-id="e687c-104">으로 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="e687c-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="e687c-105">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="e687c-105">Download Starter Project</span></span>](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="e687c-106">이 일련의 자습서 배포 하는 방법을 보여 줍니다. (게시)는 ASP.NET 웹에 대 한 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="e687c-107">웹 게시 업데이트를 설치 하는 경우에 Visual Studio 2010을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="e687c-108">계열에 대 한 소개를 참조 하십시오. [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="e687c-109">Visual Studio 2012 RC 릴리스 이후 도입 된 배포 기능 보여주며 이외의 SQL Server Compact, SQL Server 버전을 배포 하는 방법을 보여 줍니다. Windows Azure 웹 사이트를 배포 하는 방법을 보여 줍니다 하는 자습서를 참조 하십시오. [ASP.NET 웹 배포 Visual Studio를 사용 하 여](../../deployment/visual-studio-web-deployment/introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Windows Azure Web Sites, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="e687c-110">개요</span><span class="sxs-lookup"><span data-stu-id="e687c-110">Overview</span></span>

<span data-ttu-id="e687c-111">이 자습서에서는 전체 SQL Server 데이터베이스를 데이터베이스 업데이트를 배포 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-111">This tutorial shows you how to deploy a database update to a full SQL Server database.</span></span> <span data-ttu-id="e687c-112">프로세스는 거의 동일 수행한 작업에서 SQL Server Compact에 대 한 데이터베이스를 업데이트 하는 모든 작업을 수행 하는 Code First 마이그레이션을, 때문에 [데이터베이스 업데이트를 배포](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-112">Because Code First Migrations does all the work of updating the database, the process is almost identical to what you did for SQL Server Compact in the [Deploying a Database Update](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md) tutorial.</span></span>

<span data-ttu-id="e687c-113">미리 알림: 오류 메시지가 자습서를 진행할 때 작동 하지 않는 경우 반드시 확인는 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-113">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="adding-a-new-column-to-a-table"></a><span data-ttu-id="e687c-114">테이블에 새 열 추가</span><span class="sxs-lookup"><span data-stu-id="e687c-114">Adding a New Column to a Table</span></span>

<span data-ttu-id="e687c-115">자습서의이 섹션의 변경 하는 데이터베이스와 다음 테스트 및 프로덕션 환경에 배포 하기 위해에서 Visual Studio에서 테스트, 해당 코드 변경 내용을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-115">In this section of the tutorial you'll make a database change and corresponding code changes, then test them in Visual Studio in preparation for deploying them to the test and production environments.</span></span> <span data-ttu-id="e687c-116">변경 내용을 추가 해야는 `OfficeHours` 열을는 `Instructor` 엔터티 및 새로운 정보를 표시는 **강사** 웹 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-116">The change involves adding an `OfficeHours` column to the `Instructor` entity and displaying the new information in the **Instructors** web page.</span></span>

<span data-ttu-id="e687c-117">ContosoUniversity.DAL 프로젝트를 열고 *Instructor.cs* 은 다음 속성을 추가 하 고는 `HireDate` 및 `Courses` 속성:</span><span class="sxs-lookup"><span data-stu-id="e687c-117">In the ContosoUniversity.DAL project, open *Instructor.cs* and add the following property between the `HireDate` and `Courses` properties:</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample1.cs)]

<span data-ttu-id="e687c-118">테스트 데이터로 새 열을 시드합니다 이니셜라이저 클래스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-118">Update the initializer class so that it seeds the new column with test data.</span></span> <span data-ttu-id="e687c-119">열기 *Migrations\Configuration.cs* 및 시작 하는 코드 블록을 바꾸기 `var instructors = new List<Instructor>` 새 열을 포함 하는 다음 코드 블록:</span><span class="sxs-lookup"><span data-stu-id="e687c-119">Open *Migrations\Configuration.cs* and replace the code block that begins `var instructors = new List<Instructor>` with the following code block which includes the new column:</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample2.cs)]

<span data-ttu-id="e687c-120">ContosoUniversity 프로젝트를 열고 *Instructors.aspx* 닫기 바로 전에 업무 시간에 대 한 새 서식 파일 필드를 추가 하 고 `</Columns>` 첫 번째 범위에서 태그 `GridView` 제어:</span><span class="sxs-lookup"><span data-stu-id="e687c-120">In the ContosoUniversity project, open *Instructors.aspx* and add a new template field for office hours just before the closing `</Columns>` tag in the first `GridView` control:</span></span>

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample3.aspx)]

<span data-ttu-id="e687c-121">솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-121">Build the solution.</span></span>

<span data-ttu-id="e687c-122">열기는 **패키지 관리자 콘솔** 창과로 선택 ContosoUniversity.DAL는 **기본 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-122">Open the **Package Manager Console** window, and select ContosoUniversity.DAL as the **Default project**.</span></span>

<span data-ttu-id="e687c-123">다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-123">Enter the following commands:</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample4.ps1)]

<span data-ttu-id="e687c-124">응용 프로그램을 실행 하 고 선택 된 **강사** 페이지.</span><span class="sxs-lookup"><span data-stu-id="e687c-124">Run the application and select the **Instructors** page.</span></span> <span data-ttu-id="e687c-125">페이지 약간 Entity Framework는 데이터베이스를 만들고 다시 테스트 데이터로 초기값을 설정 하기 때문에 로드 하는 데 평소 보다 오래 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-125">The page takes a little longer than usual to load, because the Entity Framework re-creates the database and seeds it with test data.</span></span>

<span data-ttu-id="e687c-126">[![Instructors_page_with_office_hours](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e687c-126">[![Instructors_page_with_office_hours](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image1.png)</span></span>

## <a name="deploying-the-database-update-to-the-test-environment"></a><span data-ttu-id="e687c-127">테스트 환경에 데이터베이스 업데이트 배포</span><span class="sxs-lookup"><span data-stu-id="e687c-127">Deploying the Database Update to the Test Environment</span></span>

<span data-ttu-id="e687c-128">Code First 마이그레이션을 사용 하는 경우 SQL Server로 데이터베이스 변경 내용을 배포 하기 위한 메서드는 SQL Server Compact의 경우와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-128">When you use Code First Migrations, the method for deploying a database change to SQL Server is the same as for SQL Server Compact.</span></span> <span data-ttu-id="e687c-129">그러나 변경 하 고 테스트 해야 SQL Server Compact에서 SQL Server로 마이그레이션하려면 여전히 설정 되어 있으므로 게시 프로필.</span><span class="sxs-lookup"><span data-stu-id="e687c-129">However, you have to change the Test publish profile because it is still set up to migrate from SQL Server Compact to SQL Server.</span></span>

<span data-ttu-id="e687c-130">이전 자습서에서 만든 연결 문자열 변환을 제거 하는 첫 번째 단계가입니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-130">The first step is to remove the connection string transformations that you created in the previous tutorial.</span></span> <span data-ttu-id="e687c-131">이러한 더 이상 되므로 세 키워드가 필요 게시 프로필에 연결 문자열 변환을 지정 합니다을 구성 하기 전에 수행한 것 처럼는 **SQL 패키지 및 게시** SQL Server로의 마이그레이션 위한 탭.</span><span class="sxs-lookup"><span data-stu-id="e687c-131">These are no longer needed because you'll specify connection string transformations in the publish profile, as you did before you configured the **Package/Publish SQL** tab for migration to SQL Server.</span></span>

<span data-ttu-id="e687c-132">열기는 *Web.Test.config* 파일을 제거는 `connectionStrings` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-132">Open the *Web.Test.config* file and remove the `connectionStrings` element.</span></span> <span data-ttu-id="e687c-133">유일한 나머지 변환을 *Web.Test.config* 에 대 한 파일은는 `Environment` 값에 `appSettings` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-133">The only remaining transformation in the *Web.Test.config* file is for the `Environment` value in the `appSettings` element.</span></span>

<span data-ttu-id="e687c-134">이제 테스트 환경에 게시 프로필 및 게시를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-134">Now you can update the publish profile and publish to the test environment.</span></span>

<span data-ttu-id="e687c-135">열기는 **웹 게시** 마법사, 그리고 후는 **프로필** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-135">Open the **Publish Web** wizard, and then switch to the **Profile** tab.</span></span>

<span data-ttu-id="e687c-136">선택 된 **테스트** 게시 프로필.</span><span class="sxs-lookup"><span data-stu-id="e687c-136">Select the **Test** publish profile.</span></span>

<span data-ttu-id="e687c-137">선택 된 **설정을** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-137">Select the **Settings** tab.</span></span>

<span data-ttu-id="e687c-138">클릭 **새 데이터베이스에서 향상 된 게시 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-138">Click **enable the new database publishing improvements**.</span></span>

<span data-ttu-id="e687c-139">에 대 한 연결 문자열 상자에서 **SchoolContext**에서 사용한 동일한 값을 입력에서 *Web.Test.config* 이전 자습서에서 변환 파일:</span><span class="sxs-lookup"><span data-stu-id="e687c-139">In the connection string box for **SchoolContext**, enter the same value that you used in the *Web.Test.config* transformation file in the previous tutorial:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample5.cmd)]

<span data-ttu-id="e687c-140">선택 **실행 Code First 마이그레이션을 (응용 프로그램 시작 시 실행)** 합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-140">Select **Execute Code First Migrations (runs on application start)**.</span></span> <span data-ttu-id="e687c-141">(프로그램 버전의 Visual Studio에서 확인란을 레이블이 지정 될 수 있습니다 **Code First 마이그레이션을 적용**.)</span><span class="sxs-lookup"><span data-stu-id="e687c-141">(In your version of Visual Studio, the check box might be labeled **Apply Code First Migrations**.)</span></span>

<span data-ttu-id="e687c-142">에 대 한 연결 문자열 상자에서 **DefaultConnection**에서 사용한 동일한 값을 입력에서 *Web.Test.config* 이전 자습서에서 변환 파일:</span><span class="sxs-lookup"><span data-stu-id="e687c-142">In the connection string box for **DefaultConnection**, enter the same value that you used in the *Web.Test.config* transformation file in the previous tutorial:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample6.cmd)]

<span data-ttu-id="e687c-143">둡니다 **데이터베이스 업데이트** 의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-143">Leave **Update database** cleared.</span></span>

<span data-ttu-id="e687c-144">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-144">Click **Publish**.</span></span>

<span data-ttu-id="e687c-145">Visual Studio에서 코드 변경 내용을 테스트 환경에 배포 하 고 브라우저 Contoso 대학 홈 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-145">Visual Studio deploys the code changes to the test environment and opens the browser to the Contoso University home page.</span></span>

<span data-ttu-id="e687c-146">강사 페이지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-146">Select the Instructors page.</span></span>

<span data-ttu-id="e687c-147">이 페이지를 실행 하는 응용 프로그램 데이터베이스에 액세스 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-147">When the application runs this page, it tries to access the database.</span></span> <span data-ttu-id="e687c-148">Code First 마이그레이션을 확인 하는 데이터베이스 현재 상태는 최신 마이그레이션 적용 되지 않은 아직 찾습니다 합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-148">Code First Migrations checks if the database is current, and finds that the latest migration has not been applied yet.</span></span> <span data-ttu-id="e687c-149">Code First 마이그레이션을 최신 마이그레이션 적용의 경우 실행는 `Seed` 메서드를 다음 페이지는 정상적으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-149">Code First Migrations applies the latest migration, runs the `Seed` method, and then the page runs normally.</span></span> <span data-ttu-id="e687c-150">시드 된 데이터로 새 근무 시간 열을 참조 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="e687c-150">You see the new Office Hours column with the seeded data.</span></span>

<span data-ttu-id="e687c-151">[![Instructors_page_with_OfficeHours_Test](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="e687c-151">[![Instructors_page_with_OfficeHours_Test](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image3.png)</span></span>

## <a name="deploying-the-database-update-to-the-production-environment"></a><span data-ttu-id="e687c-152">데이터베이스 업데이트는 프로덕션 환경에 배포</span><span class="sxs-lookup"><span data-stu-id="e687c-152">Deploying the Database Update to the Production Environment</span></span>

<span data-ttu-id="e687c-153">또한 프로덕션 환경에 대 한 게시 프로필을 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-153">You have to change the publish profile for the production environment also.</span></span> <span data-ttu-id="e687c-154">이 경우 기존 프로필을 제거 하 고 업데이트 된.publishsettings 파일을 가져와서 새로 만들 합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-154">In this case you'll remove the existing profile and create a new one by importing an updated .publishsettings file.</span></span> <span data-ttu-id="e687c-155">업데이트 된 파일에는 Cytanium에서 SQL Server 데이터베이스에 대 한 연결 문자열이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-155">The updated file will include the connection string for the SQL Server database at Cytanium.</span></span>

<span data-ttu-id="e687c-156">연결 문자열 변환 테스트 환경에 배포 하는 경우 본 것 처럼 더 이상 필요는 *Web.Production.config* 변환 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-156">As you saw when you deployed to the test environment, you no longer need connection string transforms in the *Web.Production.config* transformation file.</span></span> <span data-ttu-id="e687c-157">파일을 제거 하는 열려는 `connectionStrings` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-157">Open that file and remove the `connectionStrings` element.</span></span> <span data-ttu-id="e687c-158">나머지 변형은 대 한는 `Environment` 값에 `appSettings` 요소 및 `location` Elmah 오류 보고서에 대 한 액세스를 제한 하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-158">The remaining transformations are for the `Environment` value in the `appSettings` element and the `location` element that restricts access to Elmah error reports.</span></span>

<span data-ttu-id="e687c-159">프로덕션에 대 한 새 게시 프로필을 만들기 전에 업데이트 된.publishsettings 파일에서 이전에 수행한 동일한 방식으로 다운로드는 [프로덕션 환경에 배포](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-159">Before you create a new publish profile for production, download an updated .publishsettings file the same way you did earlier in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial.</span></span> <span data-ttu-id="e687c-160">(Cytanium 제어판 **웹사이트**, 클릭 하 고는 **contosouniversity.com** 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-160">(In the Cytanium control panel, click **Web Sites**, and then click the **contosouniversity.com** website.</span></span> <span data-ttu-id="e687c-161">선택 된 **웹 게시** 탭을 클릭 한 다음 **이 웹 사이트에 대 한 게시 프로필 다운로드**.) 이렇게 하는 이유는.publishsettings 파일에서 데이터베이스 연결 문자열을 선택할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-161">Select the **Web Publishing** tab, and then click **Download Publishing Profile for this web site**.) The reason you are doing this is to pick up the database connection string in the .publishsettings file.</span></span> <span data-ttu-id="e687c-162">연결 문자열을 여전히를 사용한 SQL Server Compact 및 Cytanium에서 SQL Server 데이터베이스 아직 만들지 않았다면 때문에 파일을 다운로드 처음으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-162">The connection string wasn't available the first time you downloaded the file, because you were still using SQL Server Compact and hadn't created the SQL Server database at Cytanium yet.</span></span>

<span data-ttu-id="e687c-163">이제 프로덕션 환경에 게시 프로필 및 게시를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-163">Now you can update the publish profile and publish to the production environment.</span></span>

<span data-ttu-id="e687c-164">열기는 **웹 게시** 마법사, 그리고 후는 **프로필** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-164">Open the **Publish Web** wizard, and then switch to the **Profile** tab.</span></span>

<span data-ttu-id="e687c-165">클릭 **프로필 관리**, 한 다음 프로덕션 프로필을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-165">Click **Manage Profiles**, and then delete the Production profile.</span></span>

<span data-ttu-id="e687c-166">닫기는 **웹 게시** 이 변경 내용을 저장 하는 마법사입니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-166">Close the **Publish Web** wizard to save this change.</span></span>

<span data-ttu-id="e687c-167">열기는 **웹 게시** 마법사를 다시 클릭 하 고 **가져오기**합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-167">Open the **Publish Web** wizard again, and then click **Import**.</span></span>

<span data-ttu-id="e687c-168">에 **연결** 탭으로 변경 **대상 URL** 임시 URL을 사용 하는 경우 적절 한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-168">On the **Connection** tab, change **Destination URL** to the appropriate value if you are using a temporary URL.</span></span>

<span data-ttu-id="e687c-169">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-169">Click **Next**.</span></span>

<span data-ttu-id="e687c-170">에 **설정** 탭을 클릭 **새 데이터베이스에서 향상 된 게시 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-170">On the **Settings** tab, click **enable the new database publishing improvements**.</span></span>

<span data-ttu-id="e687c-171">에 대 한 연결 문자열 드롭 다운 목록에서 **SchoolContext**를 Cytanium 연결 문자열을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-171">In the connection string drop-down list for **SchoolContext**, select the Cytanium connection string.</span></span>

![Selecting_Cytanium_connection_string](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image5.png)

<span data-ttu-id="e687c-173">선택 **실행 Code First 마이그레이션 (응용 프로그램 시작 시 실행)** 합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-173">Select **Execute Code First migrations (runs on application start)**.</span></span>

<span data-ttu-id="e687c-174">에 대 한 연결 문자열 드롭 다운 목록에서 **DefaultConnection**를 Cytanium 연결 문자열을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-174">In the connection string drop-down list for **DefaultConnection**, select the Cytanium connection string.</span></span>

<span data-ttu-id="e687c-175">선택 된 **프로필** 탭을 클릭 **프로필 관리**, "Production"를 "contosouniversity.com-웹 배포"에서 프로필의 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-175">Select the **Profile** tab, click **Manage Profiles**, and rename the profile from "contosouniversity.com - Web Deploy" to "Production".</span></span>

<span data-ttu-id="e687c-176">게시 프로필의 변경 내용을 저장 다음 다시 여십시오.</span><span class="sxs-lookup"><span data-stu-id="e687c-176">Close the publish profile to save the change, then open it again.</span></span>

<span data-ttu-id="e687c-177">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-177">Click **Publish**.</span></span> <span data-ttu-id="e687c-178">(실제 프로덕션 웹 사이트에 대 한 복사 *앱\_offline.htm* 프로덕션 및 put를 게시 하기 전에 해당 프로젝트 폴더에서 다음 제거 배포가 완료 되 면.)</span><span class="sxs-lookup"><span data-stu-id="e687c-178">(For a real production website, you would copy *app\_offline.htm* to production and put it in your project folder before publishing, then remove it when deployment is complete.)</span></span>

<span data-ttu-id="e687c-179">Visual Studio에서 코드 변경 내용을 테스트 환경에 배포 하 고 브라우저 Contoso 대학 홈 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-179">Visual Studio deploys the code changes to the test environment and opens the browser to the Contoso University home page.</span></span>

<span data-ttu-id="e687c-180">강사 페이지를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-180">Select the Instructors page.</span></span>

<span data-ttu-id="e687c-181">Code First 마이그레이션을 테스트 환경에서 동일한 방식으로 데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-181">Code First Migrations updates the database the same way it did in the Test environment.</span></span> <span data-ttu-id="e687c-182">시드 된 데이터로 새 근무 시간 열을 참조 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="e687c-182">You see the new Office Hours column with the seeded data.</span></span>

![Instructors_page_with_OfficeHours_Prod](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image6.png)

<span data-ttu-id="e687c-184">이제 성공적으로 배포한 데이터베이스 변경 내용을 포함 하는 응용 프로그램 업데이트는 SQL Server 데이터베이스를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-184">You have now successfully deployed an application update that included a database change, using a SQL Server database.</span></span>

## <a name="more-information"></a><span data-ttu-id="e687c-185">추가 정보</span><span class="sxs-lookup"><span data-stu-id="e687c-185">More Information</span></span>

<span data-ttu-id="e687c-186">이 일련의 제 3 자 호스팅 공급자에 ASP.NET 웹 응용 프로그램 배포에 대 한 자습서를 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-186">This completes this series of tutorials on deploying an ASP.NET web application to a third-party hosting provider.</span></span> <span data-ttu-id="e687c-187">이 자습서에 포함 된 항목 중 하나에 대 한 자세한 내용은 참조는 [ASP.NET 배포 콘텐츠 맵](https://msdn.microsoft.com/library/bb386521(v=vs.110).aspx) MSDN 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-187">For more information about any of the topics covered in these tutorials, see the [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521(v=vs.110).aspx) on the MSDN web site.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="e687c-188">감사의 글</span><span class="sxs-lookup"><span data-stu-id="e687c-188">Acknowledgements</span></span>

<span data-ttu-id="e687c-189">이 자습서 시리즈의 내용에 중요 한 기여를 수행한 다음 사람에 게 감사 하 고 싶습니다.</span><span class="sxs-lookup"><span data-stu-id="e687c-189">I would like to thank the following people who made significant contributions to the content of this tutorial series:</span></span>

- [<span data-ttu-id="e687c-190">Alberto Poblacion, MVP &amp; MCT, 스페인</span><span class="sxs-lookup"><span data-stu-id="e687c-190">Alberto Poblacion, MVP &amp; MCT, Spain</span></span>](https://mvp.support.microsoft.com/profile/Alberto)
- <span data-ttu-id="e687c-191">Jarod 퍼거슨, 데이터 플랫폼 개발 MVP United States</span><span class="sxs-lookup"><span data-stu-id="e687c-191">Jarod Ferguson, Data Platform Development MVP, United States</span></span>
- <span data-ttu-id="e687c-192">Harsh Mittal, Microsoft</span><span class="sxs-lookup"><span data-stu-id="e687c-192">Harsh Mittal, Microsoft</span></span>
- [<span data-ttu-id="e687c-193">Kristina Olson, Microsoft</span><span class="sxs-lookup"><span data-stu-id="e687c-193">Kristina Olson, Microsoft</span></span>](https://blogs.iis.net/krolson/default.aspx)
- [<span data-ttu-id="e687c-194">Mike Pope, Microsoft</span><span class="sxs-lookup"><span data-stu-id="e687c-194">Mike Pope, Microsoft</span></span>](http://www.mikepope.com/blog/DisplayBlog.aspx)
- <span data-ttu-id="e687c-195">Mohit Srivastava, Microsoft</span><span class="sxs-lookup"><span data-stu-id="e687c-195">Mohit Srivastava, Microsoft</span></span>
- [<span data-ttu-id="e687c-196">Raffaele Rialdi 이탈리아</span><span class="sxs-lookup"><span data-stu-id="e687c-196">Raffaele Rialdi, Italy</span></span>](http://www.iamraf.net/)
- [<span data-ttu-id="e687c-197">Rick Anderson, Microsoft</span><span class="sxs-lookup"><span data-stu-id="e687c-197">Rick Anderson, Microsoft</span></span>](https://blogs.msdn.com/b/rickandy/)
- <span data-ttu-id="e687c-198">[Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [ @sayedihashimi ](http://twitter.com/sayedihashimi))</span><span class="sxs-lookup"><span data-stu-id="e687c-198">[Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))</span></span>
- <span data-ttu-id="e687c-199">[Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [ @shanselman ](http://twitter.com/shanselman))</span><span class="sxs-lookup"><span data-stu-id="e687c-199">[Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))</span></span>
- <span data-ttu-id="e687c-200">[Scott 헌터, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [ @coolcsh ](http://twitter.com/coolcsh))</span><span class="sxs-lookup"><span data-stu-id="e687c-200">[Scott Hunter, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))</span></span>
- [<span data-ttu-id="e687c-201">Srđan Božović, 세르비아</span><span class="sxs-lookup"><span data-stu-id="e687c-201">Srđan Božović, Serbia</span></span>](http://msforge.net/blogs/zmajcek/)
- <span data-ttu-id="e687c-202">[Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [ @vishalrjoshi ](http://twitter.com/vishalrjoshi))</span><span class="sxs-lookup"><span data-stu-id="e687c-202">[Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e687c-203">[이전](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
> [다음](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="e687c-203">[Previous](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
[Next](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)</span></span>
