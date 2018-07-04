---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12
title: 'SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여를 사용 하 여 ASP.NET 웹 응용 프로그램을 배포 합니다: SQL Server-10 / 12로 마이그레이션 | Microsoft Docs'
author: tdykstra
description: 이 시리즈의 자습서에서는 배포 하는 방법을 보여 줍니다 (게시) ASP.NET 웹 응용 프로그램 프로젝트 Visual Stu를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/17/2011
ms.topic: article
ms.assetid: a89d6f32-b71b-4036-8ff7-5f8ac2a6eca8
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12
msc.type: authoredcontent
ms.openlocfilehash: 5c26baddfabeea8aee12619019c76c36b15a504e
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37392914"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-migrating-to-sql-server---10-of-12"></a><span data-ttu-id="55313-103">SQL Server Compact Visual Studio 또는 Visual Web Developer를 사용 하 여를 사용 하 여 ASP.NET 웹 응용 프로그램을 배포 합니다: SQL Server-10 / 12로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="55313-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Migrating to SQL Server - 10 of 12</span></span>
====================
<span data-ttu-id="55313-104">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="55313-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="55313-105">시작 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="55313-105">Download Starter Project</span></span>](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="55313-106">이 시리즈의 자습서에서는 배포 하는 방법을 보여 줍니다 (게시) ASP.NET 웹용 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 웹 응용 프로그램 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="55313-107">Visual Studio 2010 웹 게시 업데이트를 설치 하는 경우에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="55313-108">계열에 대 한 소개를 참조 하세요 [시리즈의 첫 번째 자습서](deployment-to-a-hosting-provider-introduction-1-of-12.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="55313-109">Visual Studio 2012 RC 출시 이후 도입 된 배포 기능을 보여 줍니다, 이외의 SQL Server Compact, SQL Server 버전을 배포 하는 방법을 보여 줍니다 및 Azure App Service Web Apps를 배포 하는 방법을 보여 줍니다 하는 자습서를 참조 하세요 [ASP.NET 웹 배포 Visual Studio를 사용 하 여](../../deployment/visual-studio-web-deployment/introduction.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Azure App Service Web Apps, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="55313-110">개요</span><span class="sxs-lookup"><span data-stu-id="55313-110">Overview</span></span>

<span data-ttu-id="55313-111">이 자습서에서는 SQL Server Compact에서 SQL Server로 마이그레이션하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="55313-111">This tutorial shows you how to migrate from SQL Server Compact to SQL Server.</span></span> <span data-ttu-id="55313-112">SQL Server Compact를 지원 하지 않는, 저장된 프로시저, 트리거, 뷰, 복제 등 SQL Server 기능을 활용 하는 작업을 수행 하는 것이 좋습니다 하는 이유 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-112">One reason you might want to do that is to take advantage of SQL Server features that SQL Server Compact does not support, such as stored procedures, triggers, views, or replication.</span></span> <span data-ttu-id="55313-113">SQL Server Compact 및 SQL Server 간의 차이점에 대 한 자세한 내용은 참조는 [SQL Server Compact 배포](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-113">For more information about the differences between SQL Server Compact and SQL Server, see the [Deploying SQL Server Compact](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) tutorial.</span></span>

### <a name="sql-server-express-versus-full-sql-server-for-development"></a><span data-ttu-id="55313-114">개발에 대 한 전체 SQL Server와 SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="55313-114">SQL Server Express versus full SQL Server for Development</span></span>

<span data-ttu-id="55313-115">SQL Server로 업그레이드 하기로 한 후에 개발 및 테스트 환경에서 SQL Server 또는 SQL Server Express를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-115">Once you've decided to upgrade to SQL Server, you might want to use SQL Server or SQL Server Express in your development and test environments.</span></span> <span data-ttu-id="55313-116">데이터베이스 엔진 기능 및 도구 지원에서 차이 외에도 공급자 구현 SQL Server Compact와 다른 버전의 SQL Server 간에 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-116">In addition to the differences in tool support and in database engine features, there are differences in provider implementations between SQL Server Compact and other versions of SQL Server.</span></span> <span data-ttu-id="55313-117">이러한 차이 다른 결과 생성 하는 동일한 코드를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-117">These differences can cause the same code to generate different results.</span></span> <span data-ttu-id="55313-118">따라서 개발 데이터베이스로 SQL Server Compact 유지 하려는 경우 철저히 테스트 해야 사이트 SQL Server 또는 SQL Server Express에서 프로덕션에 각 배포 하기 전에 테스트 환경에서.</span><span class="sxs-lookup"><span data-stu-id="55313-118">Therefore, if you decide to keep SQL Server Compact as your development database, you should thoroughly test your site in SQL Server or SQL Server Express in a test environment before each deployment to production.</span></span>

<span data-ttu-id="55313-119">SQL Server Compact는 달리 SQL Server Express는 기본적으로 동일한 데이터베이스 엔진 및 전체 SQL Server와 같은.NET 공급자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-119">Unlike SQL Server Compact, SQL Server Express is essentially the same database engine and uses the same .NET provider as full SQL Server.</span></span> <span data-ttu-id="55313-120">SQL Server express를 테스트 하는 경우 SQL Server를 사용 하 여 수로 동일한 결과 얻는 것 이라는 것을 확신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-120">When you test with SQL Server Express, you can be confident of getting the same results as you will with SQL Server.</span></span> <span data-ttu-id="55313-121">대부분의 동일한 데이터베이스 도구를 사용 하 여 SQL Server를 사용 하 여 사용할 수 있는 SQL Server express (되는 주목할 만한 예외 [SQL Server Profiler](https://msdn.microsoft.com/library/ms181091.aspx)), 저장된 프로시저, 뷰, 트리거, SQL Server의 다른 기능을 지원 하 고 및 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-121">You can use most of the same database tools with SQL Server Express that you can use with SQL Server (a notable exception being [SQL Server Profiler](https://msdn.microsoft.com/library/ms181091.aspx)), and it supports other features of SQL Server like stored procedures, views, triggers, and replication.</span></span> <span data-ttu-id="55313-122">하지만 (일반적으로 해야 프로덕션 웹 사이트에서는 전체 SQL Server를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-122">(You typically have to use full SQL Server in a production website, however.</span></span> <span data-ttu-id="55313-123">SQL Server Express는 공유 호스팅 환경에서 실행할 수 있지만를 위해 설계 되지 않았습니다 및 여러 호스팅 공급자에서 지원 하지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="55313-123">SQL Server Express can run in a shared hosting environment, but it was not designed for that, and many hosting providers do not support it.)</span></span>

<span data-ttu-id="55313-124">Visual Studio 2012를 사용 하는 경우 일반적으로 개발 환경에 대 한 SQL Server Express LocalDB를 선택할 Visual Studio를 사용 하 여 기본적으로 설치 된 기능 이므로.</span><span class="sxs-lookup"><span data-stu-id="55313-124">If you are using Visual Studio 2012, you typically choose SQL Server Express LocalDB for your development environment because that is what is installed by default with Visual Studio.</span></span> <span data-ttu-id="55313-125">그러나 LocalDB 테스트 환경에 대 한 SQL Server 또는 SQL Server Express를 사용 해야 하므로 IIS에서 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-125">However, LocalDB does not work in IIS, so for your test environment you have to use either SQL Server or SQL Server Express.</span></span>

### <a name="combining-databases-versus-keeping-them-separate"></a><span data-ttu-id="55313-126">데이터베이스를 별도 유지 및 결합</span><span class="sxs-lookup"><span data-stu-id="55313-126">Combining Databases versus Keeping Them Separate</span></span>

<span data-ttu-id="55313-127">Contoso University 응용 프로그램에 두 SQL Server Compact 데이터베이스: 멤버 자격 데이터베이스 (*aspnet.sdf*) 및 응용 프로그램 데이터베이스 (*School.sdf*).</span><span class="sxs-lookup"><span data-stu-id="55313-127">The Contoso University application has two SQL Server Compact databases: the membership database (*aspnet.sdf*) and the application database (*School.sdf*).</span></span> <span data-ttu-id="55313-128">를 마이그레이션하는 경우에 2 개의 개별 데이터베이스 또는 단일 데이터베이스에 이러한 데이터베이스를 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-128">When you migrate, you can migrate these databases to two separate databases or to a single database.</span></span> <span data-ttu-id="55313-129">응용 프로그램 데이터베이스 및 멤버 자격 데이터베이스 간의 데이터베이스 조인을 수행 하기 위해 결합 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="55313-129">You might want to combine them in order to facilitate database joins between your application database and your membership database.</span></span> <span data-ttu-id="55313-130">호스팅 계획 결합 하는 이유를 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-130">Your hosting plan might also provide a reason to combine them.</span></span> <span data-ttu-id="55313-131">예를 들어, 호스팅 공급자는 여러 데이터베이스에 대 한 추가 요금을 청구할 수 또는 둘 이상의 데이터베이스도 허용 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-131">For example, the hosting provider might charge more for multiple databases or might not even allow more than one database.</span></span> <span data-ttu-id="55313-132">Cytanium Lite 호스팅만 단일 SQL Server 데이터베이스를 허용 하는이 자습서에 사용 되는 계정에 사용 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-132">That's the case with the Cytanium Lite hosting account that's used for this tutorial, which allows only a single SQL Server database.</span></span>

<span data-ttu-id="55313-133">이 자습서에서는 이러한 방식으로 두 데이터베이스를 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-133">In this tutorial, you'll migrate your two databases this way:</span></span>

- <span data-ttu-id="55313-134">개발 환경에서 두 LocalDB 데이터베이스를 마이그레이션하십시오.</span><span class="sxs-lookup"><span data-stu-id="55313-134">Migrate to two LocalDB databases in the development environment.</span></span>
- <span data-ttu-id="55313-135">테스트 환경에서 두 SQL Server Express 데이터베이스를 마이그레이션하십시오.</span><span class="sxs-lookup"><span data-stu-id="55313-135">Migrate to two SQL Server Express databases in the test environment.</span></span>
- <span data-ttu-id="55313-136">결합 된 프로덕션 환경에서 완전 한 SQL Server 데이터베이스를 마이그레이션하십시오.</span><span class="sxs-lookup"><span data-stu-id="55313-136">Migrate to one combined full SQL Server database in the production environment.</span></span>

<span data-ttu-id="55313-137">미리 알림: 오류 메시지를 가져오거나 자습서를 진행할 때 작동 하지 않는 경우 확인 해야 합니다 [문제 해결 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-137">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="installing-sql-server-express"></a><span data-ttu-id="55313-138">SQL Server Express 설치</span><span class="sxs-lookup"><span data-stu-id="55313-138">Installing SQL Server Express</span></span>

<span data-ttu-id="55313-139">SQL Server Express는 Visual Studio 2010을 사용 하 여 기본적으로 자동으로 설치 됩니다 있지만 기본적으로 설치 되지 않은 Visual Studio 2012를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-139">SQL Server Express is automatically installed by default with Visual Studio 2010, but by default it is not installed with Visual Studio 2012.</span></span> <span data-ttu-id="55313-140">SQL Server 2012 Express를 설치 하려면 다음 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-140">To install SQL Server 2012 Express, click the following link</span></span>

- [<span data-ttu-id="55313-141">SQL Server Express 2012</span><span class="sxs-lookup"><span data-stu-id="55313-141">SQL Server Express 2012</span></span>](https://www.microsoft.com/download/details.aspx?id=29062)

<span data-ttu-id="55313-142">선택 *한국어/x64/SQLEXPR\_x64\_ENU.exe* 하거나 *한국어/x86/SQLEXPR\_x86\_ENU.exe*, 설치 마법사에서 기본값을 적용 하 고 설정.</span><span class="sxs-lookup"><span data-stu-id="55313-142">Choose *ENU/x64/SQLEXPR\_x64\_ENU.exe* or *ENU/x86/SQLEXPR\_x86\_ENU.exe*, and in the installation wizard accept the default settings.</span></span> <span data-ttu-id="55313-143">설치 옵션에 대 한 자세한 내용은 참조 하세요. [설치 마법사 (설치)에서 SQL Server 2012 설치](https://msdn.microsoft.com/library/ms143219.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-143">For more information about installation options, see [Install SQL Server 2012 from the Installation Wizard (Setup)](https://msdn.microsoft.com/library/ms143219.aspx).</span></span>

## <a name="creating-sql-server-express-databases-for-the-test-environment"></a><span data-ttu-id="55313-144">테스트 환경에 대 한 SQL Server Express 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="55313-144">Creating SQL Server Express Databases for the Test Environment</span></span>

<span data-ttu-id="55313-145">다음 단계는 ASP.NET 멤버 자격 및 School 데이터베이스를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-145">The next step is to create the ASP.NET membership and School databases.</span></span>

<span data-ttu-id="55313-146">**뷰** 메뉴 선택 **서버 탐색기** (**데이터베이스 탐색기** Visual Web developer에서)를 마우스 오른쪽 단추로 클릭 **데이터 연결**선택한 **새 SQL Server 데이터베이스 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-146">From the **View** menu select **Server Explorer** (**Database Explorer** in Visual Web Developer), and then right-click **Data Connections** and select **Create New SQL Server Database**.</span></span>

![Selecting_Create_New_SQL_Server_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image1.png)

<span data-ttu-id="55313-148">에 **새 SQL Server 데이터베이스 만들기** 대화 상자에 입력 합니다 ". \SQLExpress"에 **서버 이름** 상자 및 "aspnet 테스트"에서 **새 데이터베이스 이름** 상자를클릭**확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-148">In the **Create New SQL Server Database** dialog box, enter ".\SQLExpress" in the **Server name** box and "aspnet-Test" in the **New database name** box, then click **OK**.</span></span>

![Create_New_SQL_Server_Database_aspnet](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image2.png)

<span data-ttu-id="55313-150">"학교-Test" 라는 새 SQL Server Express School 데이터베이스를 만들려면 동일한 절차를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="55313-150">Follow the same procedure to create a new SQL Server Express School database named "School-Test".</span></span>

<span data-ttu-id="55313-151">(에 추가할 때는 "Test" 이러한 데이터베이스 이름은 나중에 개발 환경에 대 한 각 데이터베이스의 추가 인스턴스를 만들어야 하 고 데이터베이스의 두 집합을 구분할 수 해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="55313-151">(You're appending "Test" to these database names because later you'll create an additional instance of each database for the development environment, and you need to be able to differentiate the two sets of databases.)</span></span>

<span data-ttu-id="55313-152">**서버 탐색기** 이제 두 새 데이터베이스를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-152">**Server Explorer** now shows the two new databases.</span></span>

![New_databases_in_Server_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image3.png)

## <a name="creating-a-grant-script-for-the-new-databases"></a><span data-ttu-id="55313-154">새 데이터베이스에 대 한 권한 부여 스크립트 만들기</span><span class="sxs-lookup"><span data-stu-id="55313-154">Creating a Grant Script for the New Databases</span></span>

<span data-ttu-id="55313-155">응용 프로그램 개발 컴퓨터에 IIS에서 실행 하는 경우 응용 프로그램에 기본 응용 프로그램 풀 자격 증명을 사용 하 여 데이터베이스에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-155">When the application runs in IIS on your development computer, the application accesses the database by using the default application pool's credentials.</span></span> <span data-ttu-id="55313-156">그러나 기본적으로 응용 프로그램 풀 id 없는 데이터베이스를 열 수 있는 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-156">However, by default, the application pool identity does not have permission to open the databases.</span></span> <span data-ttu-id="55313-157">따라서 해당 권한을 부여 하는 스크립트를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-157">So you have to run a script to grant that permission.</span></span> <span data-ttu-id="55313-158">이 섹션에서는 실행 하는 IIS에서 실행 될 때 응용 프로그램에서 데이터베이스를 열 수 있도록 되도록 이상 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55313-158">In this section you create the script that you'll run later to make sure that the application can open the databases when it runs in IIS.</span></span>

<span data-ttu-id="55313-159">솔루션의 *SolutionFiles* 에서 만든 폴더를 [프로덕션 환경에 배포](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) 자습서에서는 명명 된 새 SQL 파일을 만듭니다 *Grant.sql*합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-159">In the solution's *SolutionFiles* folder that you created in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial, create a new SQL file named *Grant.sql*.</span></span> <span data-ttu-id="55313-160">파일에 다음 SQL 명령을 복사 하 고 저장 한 다음 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-160">Copy the following SQL commands into the file, and then save and close the file:</span></span>

[!code-sql[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample1.sql)]

> [!NOTE]
> <span data-ttu-id="55313-161">이 스크립트는이 자습서에서는 지정 된 SQL Server 2008 및 Windows 7에서 IIS 설정을 사용 하 여 작동 하도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-161">This script is designed to work with SQL Server 2008 and with the IIS settings in Windows 7 as they are specified in this tutorial.</span></span> <span data-ttu-id="55313-162">Windows, 또는 SQL Server의 다른 버전을 사용 하는 경우 또는 설정한 경우 IIS 컴퓨터에 다르게이 스크립트를 변경 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-162">If you're using a different version of SQL Server or of Windows, or if you set up IIS on your computer differently, changes to this script might be required.</span></span> <span data-ttu-id="55313-163">SQL Server 스크립트에 대 한 자세한 내용은 참조 하세요. [SQL Server Books Online](https://go.microsoft.com/fwlink/?LinkId=132511)합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-163">For more information about SQL Server scripts, see [SQL Server Books Online](https://go.microsoft.com/fwlink/?LinkId=132511).</span></span>


> [!NOTE] 
> 
> <span data-ttu-id="55313-164">**보안 참고** 이 스크립트는 db 제공\_프로덕션 환경에 맞게 해야는 런타임 시 데이터베이스를 액세스 하는 사용자에 게 소유자 권한.</span><span class="sxs-lookup"><span data-stu-id="55313-164">**Security Note** This script gives db\_owner permissions to the user that accesses the database at run time, which is what you'll have in the production environment.</span></span> <span data-ttu-id="55313-165">일부 시나리오에서는 전체 데이터베이스 스키마 배포에 대해서만 사용 권한을 업데이트 하 고 실행된 시간에 대 한 데이터 읽기 및 쓰기에 권한이 있는 다른 사용자 지정 된 사용자를 지정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-165">In some scenarios you might want to specify a user that has full database schema update permissions only for deployment, and specify for run time a different user that has permissions only to read and write data.</span></span> <span data-ttu-id="55313-166">자세한 내용은 **Code First 마이그레이션에 대 한 자동 Web.config 변경 내용 검토** 에 [IIS 테스트 환경으로 배포](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-166">For more information, see **Reviewing the Automatic Web.config Changes for Code First Migrations** in [Deploying to IIS as a Test Environment](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md).</span></span>


## <a name="configuring-database-deployment-for-the-test-environment"></a><span data-ttu-id="55313-167">테스트 환경에 대 한 데이터베이스 배포를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-167">Configuring Database Deployment for the Test Environment</span></span>

<span data-ttu-id="55313-168">다음으로, 각 데이터베이스에 대해 다음 태스크를 수행 합니다 하는 Visual Studio를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-168">Next, you'll configure Visual Studio so that it will do the following tasks for each database:</span></span>

- <span data-ttu-id="55313-169">대상 데이터베이스에서 원본 데이터베이스의 구조 (테이블, 열, 제약 조건 등)을 만드는 SQL 스크립트를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-169">Generate a SQL script that creates the source database's structure (tables, columns, constraints, etc.) in the destination database.</span></span>
- <span data-ttu-id="55313-170">대상 데이터베이스의 테이블에 원본 데이터베이스의 데이터를 삽입 하는 SQL 스크립트를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-170">Generate a SQL script that inserts the source database's data into the tables in the destination database.</span></span>
- <span data-ttu-id="55313-171">생성된 된 스크립트 및 대상 데이터베이스에서 만든 권한 부여 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-171">Run the generated scripts, and the Grant script that you created, in the destination database.</span></span>

<span data-ttu-id="55313-172">엽니다는 **프로젝트 속성** 창과 선택 합니다 **SQL 패키지 및 게시** 탭.</span><span class="sxs-lookup"><span data-stu-id="55313-172">Open the **Project Properties** window and select the **Package/Publish SQL** tab.</span></span>

<span data-ttu-id="55313-173">했는지 **활성 (릴리스)** 또는 **릴리스** 가 선택 합니다 **구성** 드롭 다운 목록.</span><span class="sxs-lookup"><span data-stu-id="55313-173">Make sure that **Active (Release)** or **Release** is selected in the **Configuration** drop-down list.</span></span>

<span data-ttu-id="55313-174">클릭 **이 페이지를 사용 하도록 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-174">Click **Enable this Page**.</span></span>

![Package_Publish_SQL_tab_Enable_This_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image4.png)

<span data-ttu-id="55313-176">합니다 **패키지 및 게시 SQL** 탭 일반적으로 레거시 배포 메서드를 지정 하기 때문에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-176">The **Package/Publish SQL** tab is normally disabled because it specifies a legacy deployment method.</span></span> <span data-ttu-id="55313-177">대부분의 시나리오에서 데이터베이스 배포를 구성 해야 합니다 **웹 게시** 마법사.</span><span class="sxs-lookup"><span data-stu-id="55313-177">For most scenarios, you should configure database deployment in the **Publish Web** wizard.</span></span> <span data-ttu-id="55313-178">SQL Server Compact에서 SQL Server 또는 SQL Server Express로 마이그레이션하는 특수가 방법이 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-178">Migrating from SQL Server Compact to SQL Server or SQL Server Express is a special case for which this method is a good choice.</span></span>

<span data-ttu-id="55313-179">클릭 **Web.config에서 가져오기**합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-179">Click **Import from Web.config**.</span></span>

![Selecting_Import_from_Web.config](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image5.png)

<span data-ttu-id="55313-181">Visual Studio에서 연결 문자열을 찾습니다 합니다 *Web.config* 파일인 멤버 자격 데이터베이스에 대 한 하나 및 School 데이터베이스를 찾아서 각 연결 문자열에 해당 하는 행을 추가 합니다 **데이터베이스 항목**  테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-181">Visual Studio looks for connection strings in the *Web.config* file, finds one for the membership database and one for the School database, and adds a row corresponding to each connection string in the **Database Entries** table.</span></span> <span data-ttu-id="55313-182">찾으면 연결 문자열은 기존 SQL Server Compact 데이터베이스의 경우 및 다음 단계 방법 및 위치를 구성 해야 합니다. 이러한 데이터베이스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-182">The connection strings it finds are for the existing SQL Server Compact databases, and your next step will be to configure how and where to deploy these databases.</span></span>

<span data-ttu-id="55313-183">에 데이터베이스 배포 설정을 입력 합니다 **데이터베이스 항목 세부 정보** 아래 섹션의 **데이터베이스 항목** 테이블.</span><span class="sxs-lookup"><span data-stu-id="55313-183">You enter database deployment settings in the **Database Entry Details** section below the **Database Entries** table.</span></span> <span data-ttu-id="55313-184">에 나와 있는 설정을 **데이터베이스 항목 세부 정보** 섹션의 행 중 관련이 **데이터베이스 항목** 다음 그림에 표시 된 대로 테이블을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-184">The settings shown in the **Database Entry Details** section pertain to whichever row in the **Database Entries** table is selected, as shown in the following illustration.</span></span>

![Database_Entry_Details_section_of_Package_Publish_SQL_tab](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image6.png)

### <a name="configuring-deployment-settings-for-the-membership-database"></a><span data-ttu-id="55313-186">멤버 자격 데이터베이스에 대 한 배포 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-186">Configuring Deployment Settings for the Membership Database</span></span>

<span data-ttu-id="55313-187">선택 합니다 **DefaultConnection 배포** 행에 **데이터베이스 항목** 멤버 자격 데이터베이스에 적용 되는 설정을 구성 하기 위해 테이블.</span><span class="sxs-lookup"><span data-stu-id="55313-187">Select the **DefaultConnection-Deployment** row in the **Database Entries** table in order to configure settings that apply to the membership database.</span></span>

<span data-ttu-id="55313-188">**대상 데이터베이스에 대 한 연결 문자열**를 새 SQL Server Express 멤버 자격 데이터베이스를 가리키는 연결 문자열을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-188">In **Connection string for destination database**, enter a connection string that points to the new SQL Server Express membership database.</span></span> <span data-ttu-id="55313-189">필요한 연결 문자열을 가져올 수 있습니다 **서버 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-189">You can get the connection string you need from **Server Explorer**.</span></span> <span data-ttu-id="55313-190">**서버 탐색기**, 확장 **데이터 연결** 선택한를 **aspnetTest** 데이터베이스에서 다음을 **속성** 창 복사는 **연결 문자열** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-190">In **Server Explorer**, expand **Data Connections** and select the **aspnetTest** database, then from the **Properties** window copy the **Connection String** value.</span></span>

![aspnet_connection_string_in_Server_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image7.png)

<span data-ttu-id="55313-192">여기에 재현 되어 동일한 연결 문자열:</span><span class="sxs-lookup"><span data-stu-id="55313-192">The same connection string is reproduced here:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample2.cmd)]

<span data-ttu-id="55313-193">복사 하 고이 연결 문자열을 붙여 넣습니다 **대상 데이터베이스에 대 한 연결 문자열** 에 **SQL 패키지 및 게시** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-193">Copy and paste this connection string into **Connection string for destination database** in the **Package/Publish SQL** tab.</span></span>

<span data-ttu-id="55313-194">했는지 **데이터 및/또는 기존 데이터베이스에서 스키마 가져오기** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-194">Make sure that **Pull data and/or schema from an existing database** is selected.</span></span> <span data-ttu-id="55313-195">이 인해 SQL 스크립트를 자동으로 생성 하 고 대상 데이터베이스에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-195">This is what causes SQL scripts to be automatically generated and run in the destination database.</span></span>

<span data-ttu-id="55313-196">합니다 **원본 데이터베이스에 대 한 연결 문자열** 값에서 추출 되는 *Web.config* 파일과 개발 SQL Server Compact 데이터베이스를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="55313-196">The **Connection string for the source database** value is extracted from the *Web.config* file and points to the development SQL Server Compact database.</span></span> <span data-ttu-id="55313-197">이 나중에 대상 데이터베이스에서에서 실행 될 스크립트를 생성 하는 데 사용할 원본 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-197">This is the source database that will be used to generate the scripts that will run later in the destination database.</span></span> <span data-ttu-id="55313-198">데이터베이스의 프로덕션 버전을 배포 하려면 "aspnet Dev.sdf" "aspnet Prod.sdf"를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-198">Since you want to deploy the production version of the database, change "aspnet-Dev.sdf" to "aspnet-Prod.sdf".</span></span>

<span data-ttu-id="55313-199">변경 **데이터베이스 스크립팅 옵션** 에서 **스키마만** 하 **스키마 및 데이터**데이터베이스 구조와 데이터 (사용자 계정 및 역할)을 복사 하려는 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-199">Change **Database scripting options** from **Schema Only** to **Schema and data**, since you want to copy your data (user accounts and roles) as well as the database structure.</span></span>

<span data-ttu-id="55313-200">이전에 만든 권한 부여 스크립트를 실행 하는 배포를 구성 하려면 추가 해야 합니다 **데이터베이스 스크립트** 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-200">To configure deployment to run the grant scripts that you created earlier, you have to add them to the **Database Scripts** section.</span></span> <span data-ttu-id="55313-201">클릭 **스크립트 추가**, 및를 **SQL 스크립트 추가** 대화 상자에서 권한 부여 스크립트를 저장할 폴더를 탐색 합니다 (이 솔루션 파일에 포함 된 폴더).</span><span class="sxs-lookup"><span data-stu-id="55313-201">Click **Add Script**, and in the **Add SQL Scripts** dialog box, navigate to the folder where you stored the grant script (this is the folder that contains your solution file).</span></span> <span data-ttu-id="55313-202">라는 파일을 선택 *Grant.sql*, 클릭 **오픈**합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-202">Select the file named *Grant.sql*, and click **Open**.</span></span>

<span data-ttu-id="55313-203">[![Select_File_dialog_box_grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image9.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="55313-203">[![Select_File_dialog_box_grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image9.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image8.png)</span></span>

<span data-ttu-id="55313-204">에 대 한 설정 합니다 **DefaultConnection 배포** 행 **데이터베이스 항목** 이제 다음 그림과 같이 표시:</span><span class="sxs-lookup"><span data-stu-id="55313-204">The settings for the **DefaultConnection-Deployment** row in **Database Entries** now look like the following illustration:</span></span>

![Database_Entry_Details_for_DefaultConnection_Test](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image10.png)

### <a name="configuring-deployment-settings-for-the-school-database"></a><span data-ttu-id="55313-206">School 데이터베이스에 대 한 배포 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-206">Configuring Deployment Settings for the School Database</span></span>

<span data-ttu-id="55313-207">다음으로, 선택는 **SchoolContext 배포** 행에 **데이터베이스 항목** School 데이터베이스에 대 한 배포 설정을 구성 하기 위해 테이블.</span><span class="sxs-lookup"><span data-stu-id="55313-207">Next, select the **SchoolContext-Deployment** row in the **Database Entries** table in order to configure deployment settings for the School database.</span></span>

<span data-ttu-id="55313-208">새 SQL Server Express 데이터베이스에 대 한 연결 문자열을 가져오려면 이전에 사용한 동일한 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-208">You can use the same method you used earlier to get the connection string for the new SQL Server Express database.</span></span> <span data-ttu-id="55313-209">이 연결 문자열을 복사 **대상 데이터베이스에 대 한 연결 문자열** 에 **SQL 패키지 및 게시** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-209">Copy this connection string into **Connection string for destination database** in the **Package/Publish SQL** tab.</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample3.cmd)]

<span data-ttu-id="55313-210">했는지 **데이터 및/또는 기존 데이터베이스에서 스키마 가져오기** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-210">Make sure that **Pull data and/or schema from an existing database** is selected.</span></span>

<span data-ttu-id="55313-211">합니다 **원본 데이터베이스에 대 한 연결 문자열** 값에서 추출 되는 *Web.config* 파일과 개발 SQL Server Compact 데이터베이스를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="55313-211">The **Connection string for the source database** value is extracted from the *Web.config* file and points to the development SQL Server Compact database.</span></span> <span data-ttu-id="55313-212">"학교 Dev.sdf" "학교 Prod.sdf" 배포 데이터베이스의 프로덕션 버전을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-212">Change "School-Dev.sdf" to "School-Prod.sdf" to deploy the production version of the database.</span></span> <span data-ttu-id="55313-213">(앱에서 학교 Prod.sdf 파일 만들어지지\_데이터 폴더를 앱에 테스트 환경에서 해당 파일을 복사할 수 있습니다\_ContosoUniversity 프로젝트 폴더를 나중에 데이터 폴더.)</span><span class="sxs-lookup"><span data-stu-id="55313-213">(You never created a School-Prod.sdf file in the App\_Data folder, so you'll copy that file from the test environment to the App\_Data folder in the ContosoUniversity project folder later.)</span></span>

<span data-ttu-id="55313-214">변경 **데이터베이스 스크립팅 옵션** 하 **스키마와 데이터**입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-214">Change **Database scripting options** to **Schema and data**.</span></span>

<span data-ttu-id="55313-215">읽기 권한을 부여 하 고 응용 프로그램 풀 id를 쓸 수 있는 권한이이 데이터베이스에 대 한 추가 스크립트를 실행 하려는 합니다 *Grant.sql* 멤버 자격 데이터베이스에 대해 수행한 것 처럼 스크립트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-215">You also want to run the script to grant read and write permission for this database to the application pool identity, so add the *Grant.sql* script file as you did for the membership database.</span></span>

<span data-ttu-id="55313-216">완료 되 면, 설정에 대 한 합니다 **SchoolContext 배포** 행 **데이터베이스 항목** 다음 그림과 같이 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-216">When you're done, the settings for the **SchoolContext-Deployment** row in **Database Entries** look like the following illustration:</span></span>

![Database_Entry_Details_for_SchoolContext_Test](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image11.png)

<span data-ttu-id="55313-218">변경 내용을 저장 합니다 **패키지 및 게시 SQL** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-218">Save the changes to the **Package/Publish SQL** tab.</span></span>

<span data-ttu-id="55313-219">복사를 *학교 Prod.sdf* 에서 파일을 *c:\inetpub\wwwroot\ContosoUniversity\App\_데이터* 폴더를 *앱\_데이터* 폴더에서 ContosoUniversity 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-219">Copy the *School-Prod.sdf* file from the *c:\inetpub\wwwroot\ContosoUniversity\App\_Data* folder to the *App\_Data* folder in the ContosoUniversity project.</span></span>

### <a name="specifying-transacted-mode-for-the-grant-script"></a><span data-ttu-id="55313-220">권한 부여 스크립트에 대 한 트랜잭션된 모드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-220">Specifying Transacted Mode for the Grant Script</span></span>

<span data-ttu-id="55313-221">배포 프로세스는 데이터베이스 스키마 및 데이터를 배포 하는 스크립트를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-221">The deployment process generates scripts that deploy the database schema and data.</span></span> <span data-ttu-id="55313-222">기본적으로 이러한 스크립트를 트랜잭션에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-222">By default, these scripts run in a transaction.</span></span> <span data-ttu-id="55313-223">그러나 기본적으로 (예: 권한 부여 스크립트) 사용자 지정 스크립트를 트랜잭션에서 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-223">However, custom scripts (like the grant scripts) by default do not run in a transaction.</span></span> <span data-ttu-id="55313-224">트랜잭션 모드를 혼합 하는 배포 프로세스를 배포 하는 동안 스크립트를 실행 하는 경우 시간 초과 오류를 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55313-224">If the deployment process mixes transaction modes, you might get a timeout error when the scripts run during deployment.</span></span> <span data-ttu-id="55313-225">이 섹션에서는 사용자 지정 스크립트를 트랜잭션에서 실행할 구성 하기 위해 프로젝트 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-225">In this section, you edit the project file in order to configure the custom scripts to run in a transaction.</span></span>

<span data-ttu-id="55313-226">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **ContosoUniversity** 프로젝트를 마우스 **프로젝트 언로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-226">In **Solution Explorer**, right-click the **ContosoUniversity** project and select **Unload Project**.</span></span>

![Unload_Project_in_Solution_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image12.png)

<span data-ttu-id="55313-228">그런 다음 프로젝트를 다시 마우스 오른쪽 단추로 클릭 하 고 선택 **ContosoUniversity.csproj 편집**합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-228">Then right-click the project again and select **Edit ContosoUniversity.csproj**.</span></span>

![Edit_Project_in_Solution_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image13.png)

<span data-ttu-id="55313-230">Visual Studio 편집기 프로젝트 파일의 XML 콘텐츠를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="55313-230">The Visual Studio editor shows you the XML content of the project file.</span></span> <span data-ttu-id="55313-231">몇 가지는 `PropertyGroup` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-231">Notice that there are several `PropertyGroup` elements.</span></span> <span data-ttu-id="55313-232">(이미지의 내용에는 `PropertyGroup` 요소가 생략 되었습니다.)</span><span class="sxs-lookup"><span data-stu-id="55313-232">(In the image, the contents of the `PropertyGroup` elements have been omitted.)</span></span>

![프로젝트 파일 편집기 창](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image15.png)

<span data-ttu-id="55313-234">아니요 있는 첫 번째 `Condition` 특성, 설정에 관계 없이 적용 되는 빌드 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-234">The first one, which has no `Condition` attribute, is for settings that apply regardless of build configuration.</span></span> <span data-ttu-id="55313-235">하나의 `PropertyGroup` 요소는 디버그 빌드 구성에만 적용 됩니다 (참고는 `Condition` 특성), 릴리스 빌드 구성에만 적용 됩니다 하나 및 하나 테스트 빌드 구성에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55313-235">One `PropertyGroup` element applies only to the Debug build configuration (note the `Condition` attribute), one applies only to the Release build configuration, and one applies only to the Test build configuration.</span></span> <span data-ttu-id="55313-236">내 합니다 `PropertyGroup` 릴리스 빌드 구성에 대 한 요소를 볼 수는 `PublishDatabaseSettings` 에 입력 한 설정을 포함 하는 요소는 **SQL 패키지 및 게시** 탭. `Object` 권한 부여 스크립트를 각각에 해당 하는 요소 ("Grant.sql"의 두 알림 인스턴스)를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-236">Within the `PropertyGroup` element for the Release build configuration, you'll see a `PublishDatabaseSettings` element that contains the settings you entered on the **Package/Publish SQL** tab. There is an `Object` element that corresponds to each of the grant scripts you specified (notice the two instances of "Grant.sql").</span></span> <span data-ttu-id="55313-237">기본적으로 `Transacted` 특성을 `Source` 각 권한 부여 스크립트에 대 한 요소가 `False`합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-237">By default, the `Transacted` attribute of the `Source` element for each grant script is `False`.</span></span>

![Transacted_false](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image16.png)

<span data-ttu-id="55313-239">값을 변경 합니다 `Transacted` 특성을 `Source` 요소를 `True`합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-239">Change the value of the `Transacted` attribute of the `Source` element to `True`.</span></span>

![Transacted_true](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image17.png)

<span data-ttu-id="55313-241">저장 하 고 프로젝트 파일을 닫고 다음에 프로젝트를 마우스 오른쪽 단추로 **솔루션 탐색기** 선택한 **프로젝트 다시 로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-241">Save and close the project file, and then right-click the project in **Solution Explorer** and select **Reload Project**.</span></span>

![Reload_project](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image18.png)

## <a name="setting-up-webconfig-transformations-for-the-connection-strings"></a><span data-ttu-id="55313-243">연결 문자열에 대 한 Web.Config 변환 설정</span><span class="sxs-lookup"><span data-stu-id="55313-243">Setting up Web.Config Transformations for the Connection Strings</span></span>

<span data-ttu-id="55313-244">입력 데이터베이스를 새 SQL Express에 대 한 연결 문자열을 **SQL 패키지 및 게시** 탭에서 사용 하는 웹 배포 배포 중 대상 데이터베이스를 업데이트 하는 중에 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-244">The connection strings for the new SQL Express databases that you entered on the **Package/Publish SQL** tab are used by Web Deploy only for updating the destination database during deployment.</span></span> <span data-ttu-id="55313-245">도 설정 해야 *Web.config* 변환 연결 문자열에 배포 되도록 *Web.config* 파일 새 SQL Server Express 데이터베이스를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="55313-245">You still have to set up *Web.config* transformations so that the connection strings in the deployed *Web.config* file point to the new SQL Server Express databases.</span></span> <span data-ttu-id="55313-246">(사용 하는 경우는 **패키지 및 게시 SQL** 탭 게시 프로필의 연결 문자열을 구성할 수 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="55313-246">(When you use the **Package/Publish SQL** tab, you can't configure connection strings in the publish profile.)</span></span>

<span data-ttu-id="55313-247">열기 *Web.Test.config* 바꾸고 합니다 `connectionStrings` 요소는 `connectionStrings` 다음 예제에서는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-247">Open *Web.Test.config* and replace the `connectionStrings` element with the `connectionStrings` element in the following example.</span></span> <span data-ttu-id="55313-248">(ConnectionStrings 요소는 다음과 같습니다 컨텍스트를 제공 하는 주변 코드가 아니라 복사할 수 있는지 확인 합니다.)</span><span class="sxs-lookup"><span data-stu-id="55313-248">(Make sure you only copy the connectionStrings element, not the surrounding code that is shown here to provide context.)</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample4.xml?highlight=2-11)]

<span data-ttu-id="55313-249">이 코드는 `connectionString` 및 `providerName` 각 특성 `add` 대체할 요소의 배포에서 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-249">This code causes the `connectionString` and `providerName` attributes of each `add` element to be replaced in the deployed *Web.config* file.</span></span> <span data-ttu-id="55313-250">이러한 연결 문자열에 입력 한 것과 동일 하지 않습니다.는 **패키지 및 게시 SQL** 탭 합니다. 설정 "MultipleActiveResultSets = True" Entity Framework 및 범용 공급자에 대 한 필요 하므로에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-250">These connection strings are not identical to the ones you entered in the **Package/Publish SQL** tab. The setting "MultipleActiveResultSets=True" has been added to them because it's required for the Entity Framework and the Universal Providers.</span></span>

## <a name="installing-sql-server-compact"></a><span data-ttu-id="55313-251">SQL Server Compact를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-251">Installing SQL Server Compact</span></span>

<span data-ttu-id="55313-252">SqlServerCompact NuGet 패키지는 Contoso University 응용 프로그램에 대 한 엔진 어셈블리를 SQL Server Compact 데이터베이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-252">The SqlServerCompact NuGet package provides the SQL Server Compact database engine assemblies for the Contoso University application.</span></span> <span data-ttu-id="55313-253">하지만 이제 없는 응용 프로그램 이지만 웹 배포를 SQL Server 데이터베이스에서 실행 하는 스크립트를 만들기 위해 SQL Server Compact 데이터베이스를 읽을 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-253">But now it is not the application but Web Deploy that must be able to read the SQL Server Compact databases, in order to create scripts to run in the SQL Server databases.</span></span> <span data-ttu-id="55313-254">을 사용 하려면 SQL Server Compact 데이터베이스를 읽기에 웹 배포 설치 SQL Server Compact 개발 컴퓨터의 다음 링크를 사용 하 여: [Microsoft SQL Server Compact 4.0](https://www.microsoft.com/downloads/details.aspx?FamilyID=15F7C9B3-A150-4AD2-823E-E4E0DCF85DF6)합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-254">To enable Web Deploy to read SQL Server Compact databases, install SQL Server Compact on the development computer by using the following link: [Microsoft SQL Server Compact 4.0](https://www.microsoft.com/downloads/details.aspx?FamilyID=15F7C9B3-A150-4AD2-823E-E4E0DCF85DF6).</span></span>

## <a name="deploying-to-the-test-environment"></a><span data-ttu-id="55313-255">테스트 환경에 배포</span><span class="sxs-lookup"><span data-stu-id="55313-255">Deploying to the Test Environment</span></span>

<span data-ttu-id="55313-256">테스트 환경에 게시 하기 위해 사용 하도록 구성 되어 있는 게시 프로필을 만들 필요가 합니다 **SQL 패키지 및 게시** 게시 프로필 데이터베이스 설정 하는 대신 게시 데이터베이스에 대 한 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-256">In order to publish to the Test environment, you have to create a publish profile that is configured to use the **Package/Publish SQL** tab for database publishing instead of the publish profile database settings.</span></span>

<span data-ttu-id="55313-257">먼저 기존 테스트 프로필을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-257">First, delete the existing Test profile.</span></span>

<span data-ttu-id="55313-258">**솔루션 탐색기**ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-258">In **Solution Explorer**, right-click the ContosoUniversity project, and click **Publish**.</span></span>

<span data-ttu-id="55313-259">선택 된 **프로필** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-259">Select the **Profile** tab.</span></span>

<span data-ttu-id="55313-260">클릭 **프로필을 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-260">Click **Manage Profiles**.</span></span>

<span data-ttu-id="55313-261">선택 **테스트**, 클릭 **제거**를 클릭 하 고 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-261">Select **Test**, click **Remove**, and then click **Close**.</span></span>

<span data-ttu-id="55313-262">닫기 합니다 **웹 게시** 마법사가 변경이 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-262">Close the **Publish Web** wizard to save this change.</span></span>

<span data-ttu-id="55313-263">다음으로, 새 테스트 프로필을 만들고 프로젝트를 게시 하는 데 사용할 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-263">Next, create a new Test profile and use it to publish the project.</span></span>

<span data-ttu-id="55313-264">**솔루션 탐색기**ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-264">In **Solution Explorer**, right-click the ContosoUniversity project, and click **Publish**.</span></span>

<span data-ttu-id="55313-265">선택 된 **프로필** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-265">Select the **Profile** tab.</span></span>

<span data-ttu-id="55313-266">선택 **&lt;새로 만들기... &gt;** 드롭다운 목록에서 목록에서 선택한 프로필 이름으로 "Test"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-266">Select **&lt;New...&gt;** from the drop-down list, and enter "Test" as the profile name.</span></span>

<span data-ttu-id="55313-267">에 **서비스 URL** 상자에 입력 합니다 *localhost*합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-267">In the **Service URL** box, enter *localhost*.</span></span>

<span data-ttu-id="55313-268">에 **사이트 및 응용 프로그램** 상자에 입력 합니다 *기본 웹 사이트/ContosoUniversity*합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-268">In the **Site/application** box, enter *Default Web Site/ContosoUniversity*.</span></span>

<span data-ttu-id="55313-269">에 **대상 URL** 상자에 입력 `http://localhost/ContosoUniversity/`합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-269">In the **Destination URL** box, enter `http://localhost/ContosoUniversity/`.</span></span>

<span data-ttu-id="55313-270">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-270">Click **Next**.</span></span>

<span data-ttu-id="55313-271">**설정을** 탭에서 경고는 합니다 **SQL 패키지 및 게시** 탭에 구성 된 새 데이터베이스 게시 개선 사항 사용을 클릭 하 여 덮어쓸 수 있는 기회를 제공 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-271">The **Settings** tab warns you that the **Package/Publish SQL** tab has been configured, and it gives you an opportunity to override them by clicking enable the new database publishing improvements.</span></span> <span data-ttu-id="55313-272">이 배포에 대 한 재정의 않으려는 합니다 **SQL 패키지 및 게시** 설정 탭에서 그러 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-272">For this deployment you don't want to override the **Package/Publish SQL** tab settings, so just click **Next**.</span></span>

![Publish_Web_wizard_Settings_tab_Migrate](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image19.png)

<span data-ttu-id="55313-274">메시지를 **미리 보기** 탭을 사용 함을 **데이터베이스가 선택 되지 않음 게시할**, 하지만 게시 프로필에서 데이터베이스 게시가 구성 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-274">A message on the **Preview** tab indicates that **No databases are selected to publish**, but this only means that database publishing is not configured in the publish profile.</span></span>

<span data-ttu-id="55313-275">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-275">Click **Publish**.</span></span>

![Publish_Web_wizard_Preview_tab_Migrate](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image20.png)

<span data-ttu-id="55313-277">Visual Studio 응용 프로그램을 배포 하 고 테스트 환경에서 사이트의 홈 페이지로 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="55313-277">Visual Studio deploys the application and opens the browser to the home page of the site in the test environment.</span></span> <span data-ttu-id="55313-278">앞서 살펴본 있는 동일한 데이터를 표시 하려면 강사 페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-278">Run the Instructors page to see that it displays the same data that you saw earlier.</span></span> <span data-ttu-id="55313-279">실행 합니다 **추가 학생** 페이지에서 새 학생을 추가 하 고 다음에 새 학생을 봅니다 합니다 **학생** 페이지.</span><span class="sxs-lookup"><span data-stu-id="55313-279">Run the **Add Students** page, add a new student, and then view the new student in the **Students** page.</span></span> <span data-ttu-id="55313-280">이 데이터베이스를 업데이트할 수 있습니다 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-280">This verifies that the you can update the database.</span></span> <span data-ttu-id="55313-281">선택 된 **업데이트 크레딧** 페이지 (로그인) 멤버 자격 데이터베이스가 배포 된 고에 액세스할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-281">Select the **Update Credits** page (you'll need to log in) to verify that the membership database was deployed and you have access to it.</span></span>

## <a name="creating-a-sql-server-database-for-the-production-environment"></a><span data-ttu-id="55313-282">프로덕션 환경에 대 한 SQL Server 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="55313-282">Creating a SQL Server Database for the Production Environment</span></span>

<span data-ttu-id="55313-283">테스트 환경에 배포한 했으므로 프로덕션 배포를 설정할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-283">Now that you've deployed to the test environment, you're ready to set up deployment to production.</span></span> <span data-ttu-id="55313-284">먼저, 데이터베이스에 배포를 만들어 테스트 환경에 대해 수행한 것 처럼.</span><span class="sxs-lookup"><span data-stu-id="55313-284">You begin as you did for the test environment, by creating a database to deploy to.</span></span> <span data-ttu-id="55313-285">개요에서 기억 하듯이, 두 개가 아닌 하나만 데이터베이스를 설정 하므로 Cytanium Lite 호스팅 계획에 단일 SQL Server 데이터베이스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-285">As you recall from the Overview, the Cytanium Lite hosting plan only allows a single SQL Server database, so you will set up only one database, not two.</span></span> <span data-ttu-id="55313-286">모든 테이블과 멤버 자격 및 학교 SQL Server Compact 데이터베이스에서 데이터를 프로덕션 환경에서 하나의 SQL Server 데이터베이스에 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55313-286">All of the tables and data from the membership and School SQL Server Compact databases will be deployed into one SQL Server database in production.</span></span>

<span data-ttu-id="55313-287">Cytanium 제어판으로 이동 [ http://panel.cytanium.com ](http://panel.cytanium.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-287">Go to the Cytanium control panel at [http://panel.cytanium.com](http://panel.cytanium.com).</span></span> <span data-ttu-id="55313-288">위로 마우스를 가져가면 **데이터베이스** 을 클릭 한 다음 **SQL Server 2008**합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-288">Hold the mouse over **Databases** and then click **SQL Server 2008**.</span></span>

<span data-ttu-id="55313-289">[![Selecting_Databases_in_Control_Panel](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image22.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="55313-289">[![Selecting_Databases_in_Control_Panel](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image22.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image21.png)</span></span>

<span data-ttu-id="55313-290">에 **SQL Server 2008** 페이지에서 클릭 **Create Database**합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-290">In the **SQL Server 2008** page, click **Create Database**.</span></span>

<span data-ttu-id="55313-291">[![Selecting_Create_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image24.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="55313-291">[![Selecting_Create_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image24.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image23.png)</span></span>

<span data-ttu-id="55313-292">School 데이터베이스 이름을 지정 하 고 클릭 **저장할**합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-292">Name the database "School" and click **Save**.</span></span> <span data-ttu-id="55313-293">(페이지 자동으로 추가 "contosou"를 접두사 효과적인 이름을 "contosouSchool" 되도록 합니다.)</span><span class="sxs-lookup"><span data-stu-id="55313-293">(The page automatically adds the prefix "contosou", so the effective name will be "contosouSchool".)</span></span>

<span data-ttu-id="55313-294">[![Naming_the_database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image26.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="55313-294">[![Naming_the_database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image26.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image25.png)</span></span>

<span data-ttu-id="55313-295">같은 페이지에서 클릭 **Create User**합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-295">On the same page, click **Create User**.</span></span> <span data-ttu-id="55313-296">Cytanium의 서버에 보다는 통합된 Windows 보안을 사용 하 여 데이터베이스를 열고 응용 프로그램 풀 id 수 있도록, 데이터베이스를 열 권한이 있는 사용자를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-296">On Cytanium's servers, rather than using integrated Windows security and letting the application pool identity open your database, you'll create a user that has authority to open your database.</span></span> <span data-ttu-id="55313-297">프로덕션에서 이동 하는 연결 문자열에 사용자의 자격 증명을 추가할 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-297">You'll add the user's credentials to the connection strings that go in the production *Web.config* file.</span></span> <span data-ttu-id="55313-298">이 단계에서는 해당 자격 증명을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-298">In this step you create those credentials.</span></span>

<span data-ttu-id="55313-299">[![Creating_a_database_user](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image28.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image27.png)</span><span class="sxs-lookup"><span data-stu-id="55313-299">[![Creating_a_database_user](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image28.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image27.png)</span></span>

<span data-ttu-id="55313-300">필수 필드를 입력 합니다 **SQL 사용자 속성** 페이지:</span><span class="sxs-lookup"><span data-stu-id="55313-300">Fill in the required fields in the **SQL User Properties** page:</span></span>

- <span data-ttu-id="55313-301">이름으로 "ContosoUniversityUser"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-301">Enter "ContosoUniversityUser" as the name.</span></span>
- <span data-ttu-id="55313-302">암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-302">Enter a password.</span></span>
- <span data-ttu-id="55313-303">선택 **contosouSchool** 를 기본 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-303">Select **contosouSchool** as the default database.</span></span>
- <span data-ttu-id="55313-304">선택 된 **contosouSchool** 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-304">Select the **contosouSchool** check box.</span></span>

<span data-ttu-id="55313-305">[![SQL_User_Properties_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image30.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image29.png)</span><span class="sxs-lookup"><span data-stu-id="55313-305">[![SQL_User_Properties_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image30.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image29.png)</span></span>

## <a name="configuring-database-deployment-for-the-production-environment"></a><span data-ttu-id="55313-306">프로덕션 환경에 대 한 데이터베이스 배포를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-306">Configuring Database Deployment for the Production Environment</span></span>

<span data-ttu-id="55313-307">데이터베이스 배포 설정을 설정할 준비가 되었습니다. 이제는 **SQL 패키지 및 게시** 이전 테스트 환경에 대해 수행한 것 처럼 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-307">Now you're ready to set up database deployment settings in the **Package/Publish SQL** tab, as you did earlier for the test environment.</span></span>

<span data-ttu-id="55313-308">열기는 **프로젝트 속성** 창에서를 **SQL 패키지 및 게시** 탭을 했는지 **활성 (릴리스)** 또는 **릴리스** 는 선택 합니다 **구성** 드롭 다운 목록.</span><span class="sxs-lookup"><span data-stu-id="55313-308">Open the **Project Properties** window, select the **Package/Publish SQL** tab, and make sure that **Active (Release)** or **Release** is selected in the **Configuration** drop-down list.</span></span>

<span data-ttu-id="55313-309">각 데이터베이스에 대 한 배포 설정을 구성한 경우 연결 문자열을 구성 하는 방법에 프로덕션 환경과 테스트 환경에 대 한 여러분의 주요 차이점은입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-309">When you configure deployment settings for each database, the key difference between what you do for production and test environments is in how you configure connection strings.</span></span> <span data-ttu-id="55313-310">다른 대상 데이터베이스 연결 문자열을 입력 한 테스트 환경에 대 한 하지만 프로덕션 환경에 대 한 대상 연결 문자열은 동일 데이터베이스 모두에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-310">For the test environment you entered different destination database connection strings, but for the production environment the destination connection string will be the same for both databases.</span></span> <span data-ttu-id="55313-311">두 데이터베이스를 배포 하는 프로덕션 환경에서 하나의 데이터베이스로 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-311">This is because you are deploying both databases to one database in production.</span></span>

### <a name="configuring-deployment-settings-for-the-membership-database"></a><span data-ttu-id="55313-312">멤버 자격 데이터베이스에 대 한 배포 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-312">Configuring Deployment Settings for the Membership Database</span></span>

<span data-ttu-id="55313-313">멤버 자격 데이터베이스에 적용 되는 설정을 구성 하려면 선택 합니다 **DefaultConnection 배포** 행에 **데이터베이스 항목** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-313">To configure settings that apply to the membership database, select the **DefaultConnection-Deployment** row in the **Database Entries** table.</span></span>

<span data-ttu-id="55313-314">**대상 데이터베이스에 대 한 연결 문자열**, 방금 만든 새 프로덕션 SQL Server 데이터베이스를 가리키는 연결 문자열을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-314">In **Connection string for destination database**, enter a connection string that points to the new production SQL Server database that you just created.</span></span> <span data-ttu-id="55313-315">환영 전자 메일에서 연결 문자열을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-315">You can get the connection string from your welcome email.</span></span> <span data-ttu-id="55313-316">다음 샘플 연결 문자열을 포함 하는 전자 메일의 관련 부분:</span><span class="sxs-lookup"><span data-stu-id="55313-316">The relevant part of the email contains the following sample connection string:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample5.cmd)]

<span data-ttu-id="55313-317">세 개의 변수를 대체 한 후 필요한 연결 문자열을이 예제와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-317">After you replace the three variables, the connection string you need looks like this example:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample6.cmd)]

<span data-ttu-id="55313-318">복사 하 고이 연결 문자열을 붙여 넣습니다 **대상 데이터베이스에 대 한 연결 문자열** 에 **SQL 패키지 및 게시** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-318">Copy and paste this connection string into **Connection string for destination database** in the **Package/Publish SQL** tab.</span></span>

<span data-ttu-id="55313-319">했는지 **데이터 및/또는 기존 데이터베이스에서 스키마 가져오기** 하 고 선택 계속 됩니다 **데이터베이스 스크립팅 옵션** 여전히 **스키마 및 데이터**입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-319">Make sure that **Pull data and/or schema from an existing database** is still selected, and that **Database scripting options** is still **Schema and Data**.</span></span>

<span data-ttu-id="55313-320">에 **데이터베이스 스크립트** 상자 Grant.sql 스크립트 옆의 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-320">In the **Database Scripts** box, clear the check box next to the Grant.sql script.</span></span>

![Disable_Grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image31.png)

### <a name="configuring-deployment-settings-for-the-school-database"></a><span data-ttu-id="55313-322">School 데이터베이스에 대 한 배포 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-322">Configuring Deployment Settings for the School Database</span></span>

<span data-ttu-id="55313-323">다음으로, 선택는 **SchoolContext 배포** 행을 **데이터베이스 항목** School 데이터베이스 설정을 구성 하기 위해 테이블.</span><span class="sxs-lookup"><span data-stu-id="55313-323">Next, select the **SchoolContext-Deployment** row in the **Database Entries** table in order to configure the School database settings.</span></span>

<span data-ttu-id="55313-324">동일한 연결 문자열을 복사 **대상 데이터베이스에 대 한 연결 문자열** 멤버 자격 데이터베이스에 대 한 해당 필드에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-324">Copy the same connection string into **Connection string for destination database** that you copied into that field for the membership database.</span></span>

<span data-ttu-id="55313-325">했는지 **데이터 및/또는 기존 데이터베이스에서 스키마 가져오기** 하 고 선택 계속 됩니다 **데이터베이스 스크립팅 옵션** 여전히 **스키마 및 데이터**입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-325">Make sure that **Pull data and/or schema from an existing database** is still selected, and that **Database scripting options** is still **Schema and Data**.</span></span>

<span data-ttu-id="55313-326">에 **데이터베이스 스크립트** 상자 Grant.sql 스크립트 옆의 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-326">In the **Database Scripts** box, clear the check box next to the Grant.sql script.</span></span>

<span data-ttu-id="55313-327">변경 내용을 저장 합니다 **패키지 및 게시 SQL** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-327">Save the changes to the **Package/Publish SQL** tab.</span></span>

## <a name="setting-up-webconfig-transforms-for-the-connection-strings-to-production-databases"></a><span data-ttu-id="55313-328">프로덕션 데이터베이스에 대 한 연결 문자열에 대 한 Web.Config 설정 변환</span><span class="sxs-lookup"><span data-stu-id="55313-328">Setting Up Web.Config Transforms for the Connection Strings to Production Databases</span></span>

<span data-ttu-id="55313-329">다음으로 설정 합니다 *Web.config* 변환을 연결 문자열에 배포 되도록 *Web.config* 새 프로덕션 데이터베이스를 가리키도록 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-329">Next, you'll set up *Web.config* transformations so that the connection strings in the deployed *Web.config* file to point to the new production database.</span></span> <span data-ttu-id="55313-330">에 입력 한 연결 문자열을 **SQL 패키지 및 게시** 탭을 사용 하 여 웹 배포에 대 한 응용 프로그램 추가 제외 하 고 사용 해야 하는 것 같습니다는 `MultipleResultSets` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-330">The connection string that you entered on the **Package/Publish SQL** tab for Web Deploy to use is the same as the one the application needs to use, except for the addition of the `MultipleResultSets` option.</span></span>

<span data-ttu-id="55313-331">열기 *Web.Production.config* 바꾸고 합니다 `connectionStrings` 요소를 `connectionStrings` 요소는 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-331">Open *Web.Production.config* and replace the `connectionStrings` element with a `connectionStrings` element that looks like the following example.</span></span> <span data-ttu-id="55313-332">(만 복사는 `connectionStrings` 요소, 컨텍스트를 표시 하도록 제공 되는 주변 태그가 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="55313-332">(Only copy the `connectionStrings` element, not the surrounding tags that are provided to show the context.)</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample7.xml?highlight=2-11)]

<span data-ttu-id="55313-333">경우에 따라 항상의 연결 문자열을 암호화 하도록 알려주는 통지를 표시 합니다 *Web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-333">You sometimes see advice that tells you to always encrypt connection strings in the *Web.config* file.</span></span> <span data-ttu-id="55313-334">이 여러분의 회사 네트워크에서 서버를 배포 하는 경우에 적절할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-334">This might be appropriate if you were deploying to servers on your own company's network.</span></span> <span data-ttu-id="55313-335">그러나 공유 호스팅 환경에 배포 하는 경우 호스팅 공급자의 보안 사례를 신뢰 하는 및 것은 불필요 하거나 연결 문자열을 암호화 하는 데 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-335">When you are deploying to a shared hosting environment, though, you're trusting the security practices of the hosting provider, and it's not necessary or practical to encrypt the connection strings.</span></span>

## <a name="deploying-to-the-production-environment"></a><span data-ttu-id="55313-336">프로덕션 환경에 배포</span><span class="sxs-lookup"><span data-stu-id="55313-336">Deploying to the Production Environment</span></span>

<span data-ttu-id="55313-337">이제 프로덕션 환경에 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-337">Now you're ready to deploy to production.</span></span> <span data-ttu-id="55313-338">웹 배포 프로젝트의 SQL Server Compact 데이터베이스를 읽어들일 *앱\_데이터* 폴더 하 고 다시 모든 테이블 및 프로덕션 SQL Server 데이터베이스의 데이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55313-338">Web Deploy will read the SQL Server Compact databases in your project's *App\_Data* folder and re-create all of their tables and data in the production SQL Server database.</span></span> <span data-ttu-id="55313-339">사용 하 여 게시 하려면 합니다 **웹 패키지 및 게시** 프로덕션에 대 한 새 게시 프로필을 만들 필요가 탭 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-339">In order to publish by using the **Package/Publish Web** tab settings, you have to create a new publish profile for production.</span></span>

<span data-ttu-id="55313-340">테스트 프로필을 앞서 수행한 것 처럼 기존 프로덕션 프로필을 먼저 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-340">First, delete the existing Production profile as you did the Test profile earlier.</span></span>

<span data-ttu-id="55313-341">**솔루션 탐색기**ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-341">In **Solution Explorer**, right-click the ContosoUniversity project, and click **Publish**.</span></span>

<span data-ttu-id="55313-342">선택 된 **프로필** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-342">Select the **Profile** tab.</span></span>

<span data-ttu-id="55313-343">클릭 **프로필을 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-343">Click **Manage Profiles**.</span></span>

<span data-ttu-id="55313-344">선택 **프로덕션**, 클릭 **제거**를 클릭 하 고 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-344">Select **Production**, click **Remove**, and then click **Close**.</span></span>

<span data-ttu-id="55313-345">닫기 합니다 **웹 게시** 마법사가 변경이 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-345">Close the **Publish Web** wizard to save this change.</span></span>

<span data-ttu-id="55313-346">다음으로, 새 프로덕션 프로필을 만들고 프로젝트를 게시 하는 데 사용할 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-346">Next, create a new Production profile and use it to publish the project.</span></span>

<span data-ttu-id="55313-347">**솔루션 탐색기**ContosoUniversity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-347">In **Solution Explorer**, right-click the ContosoUniversity project, and click **Publish**.</span></span>

<span data-ttu-id="55313-348">선택 된 **프로필** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-348">Select the **Profile** tab.</span></span>

<span data-ttu-id="55313-349">클릭 **가져오기**, 이전에 다운로드 한.publishsettings 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-349">Click **Import**, and select the .publishsettings file that you downloaded earlier.</span></span>

<span data-ttu-id="55313-350">에 **연결** 탭으로 변경 합니다 **대상 URL** 은이 예제에서는 임시 올바른 URL로 http://contosouniversity.com.vserver01.cytanium.com.</span><span class="sxs-lookup"><span data-stu-id="55313-350">On the **Connection** tab, change the **Destination URL** to the correct temporary URL, which in this example is http://contosouniversity.com.vserver01.cytanium.com.</span></span>

<span data-ttu-id="55313-351">프로덕션 프로필을 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="55313-351">Rename the profile to Production.</span></span> <span data-ttu-id="55313-352">(선택 된 **프로필** 탭을 클릭 **프로필 관리** 를 위해).</span><span class="sxs-lookup"><span data-stu-id="55313-352">(Select the **Profile** tab and click **Manage Profiles** to do that).</span></span>

<span data-ttu-id="55313-353">닫기 합니다 **웹 게시** 변경 내용을 저장 하는 마법사입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-353">Close the **Publish Web** wizard to save your changes.</span></span>

<span data-ttu-id="55313-354">데이터베이스를 프로덕션 환경에서 업데이트 되는 실제 응용 프로그램에서 수행한 두 가지 추가 단계가 이제 게시 하기 전에:</span><span class="sxs-lookup"><span data-stu-id="55313-354">In a real application in which the database was being updated in production, you would do two additional steps now before you publish:</span></span>

1. <span data-ttu-id="55313-355">업로드 *앱\_offline.htm*에 나와 있는 것 처럼 합니다 [프로덕션 환경에 배포](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-355">Upload *app\_offline.htm*, as shown in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial.</span></span>
2. <span data-ttu-id="55313-356">사용 합니다 **파일 관리자** 복사할 Cytanium 제어판의 기능을 *aspnet Prod.sdf* 및 *학교 Prod.sdf* 프로덕션 사이트에서 파일을 *앱\_데이터* ContosoUniversity 프로젝트의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-356">Use the **File Manager** feature of the Cytanium control panel to copy the *aspnet-Prod.sdf* and *School-Prod.sdf* files from the production site to the *App\_Data* folder of the ContosoUniversity project.</span></span> <span data-ttu-id="55313-357">이렇게 하면 새 SQL Server 데이터베이스에 배포 하는 데이터를 프로덕션 웹 사이트에서 수행 된 최신 업데이트에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-357">This ensures that the data you're deploying to the new SQL Server database includes the latest updates made by your production website.</span></span>

<span data-ttu-id="55313-358">에 **한 번 클릭으로 웹 게시** 도구 모음 있는지 확인 합니다 **프로덕션** 프로필을 선택한 다음 클릭 **게시**.</span><span class="sxs-lookup"><span data-stu-id="55313-358">In the **Web One Click Publish** toolbar, make sure that the **Production** profile is selected, and then click **Publish**.</span></span>

<span data-ttu-id="55313-359">업로드 한 경우 <em>앱\_offline.htm</em> 게시 하기 전에 사용 해야 합니다 <strong>파일 관리자</strong> Cytanium 제어판 삭제 유틸리티 <em>앱\_오프 라인.</em> htm 테스트 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-359">If you uploaded <em>app\_offline.htm</em> before publishing, you have to use the <strong>File Manager</strong> utility in the Cytanium control panel to delete <em>app\_offline.</em>htm before you test.</span></span> <span data-ttu-id="55313-360">동시에 삭제할 수도 합니다 <em>.sdf</em> 에서 파일을 <em>앱\_데이터</em> 폴더.</span><span class="sxs-lookup"><span data-stu-id="55313-360">You can also at the same time delete the <em>.sdf</em> files from the <em>App\_Data</em> folder.</span></span>

<span data-ttu-id="55313-361">이제 브라우저를 열고 하 수는 응용 프로그램 테스트 환경에 배포한 후 수행한 동일한 방식으로 테스트 공개 사이트의 URL로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-361">You can now open a browser and go to the URL of your public site to test the application the same way you did after deploying to the test environment.</span></span>

## <a name="switching-to-sql-server-express-localdb-in-development"></a><span data-ttu-id="55313-362">SQL Server Express LocalDB 개발에서로 전환</span><span class="sxs-lookup"><span data-stu-id="55313-362">Switching to SQL Server Express LocalDB in Development</span></span>

<span data-ttu-id="55313-363">개요에서 설명한 것 처럼 개발 테스트 및 프로덕션에서 사용 하는 동일한 데이터베이스 엔진을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-363">As was explained in the Overview, it's generally best to use the same database engine in development that you use in test and production.</span></span> <span data-ttu-id="55313-364">(개발에서 SQL Server Express를 사용 하는 이점은 데이터베이스를 동일 하 게 작동 개발, 테스트 및 프로덕션 환경에서 인지 해야 합니다.) 이 섹션에서 Visual Studio에서 응용 프로그램을 실행 하는 경우 SQL Server Express LocalDB를 사용 하도록 ContosoUniversity 프로젝트를 설정 하는 것이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55313-364">(Remember that the advantage to using SQL Server Express in development is that the database will work the same in your development, test, and production environments.) In this section you'll set up the ContosoUniversity project to use SQL Server Express LocalDB when you run the application from Visual Studio.</span></span>

<span data-ttu-id="55313-365">이 마이그레이션을 수행 하는 가장 간단한 방법은 되도록 두는 Code First 및 멤버 자격 시스템을 모두 새 개발 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55313-365">The simplest way to perform this migration is to let Code First and the membership system create both new development databases for you.</span></span> <span data-ttu-id="55313-366">이 메서드를 사용 하 여 마이그레이션하려면 세 단계가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-366">Using this method to migrate requires three steps:</span></span>

1. <span data-ttu-id="55313-367">새 SQL Express LocalDB 데이터베이스를 지정 하도록 연결 문자열을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-367">Change the connection strings to specify new SQL Express LocalDB databases.</span></span>
2. <span data-ttu-id="55313-368">관리자 사용자를 만들려면 웹 사이트 관리 도구를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-368">Run the Web Site Administration Tool to create an administrator user.</span></span> <span data-ttu-id="55313-369">이 멤버 자격 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55313-369">This creates the membership database.</span></span>
3. <span data-ttu-id="55313-370">Code First 마이그레이션을 update-database 명령은 사용 하 여 만들고 응용 프로그램 데이터베이스를 시드합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-370">Use the Code First Migrations update-database command to create and seed the application database.</span></span>

### <a name="updating-connection-strings-in-the-webconfig-file"></a><span data-ttu-id="55313-371">Web.config 파일에서 연결 문자열 업데이트</span><span class="sxs-lookup"><span data-stu-id="55313-371">Updating Connection Strings in the Web.config file</span></span>

<span data-ttu-id="55313-372">엽니다는 *Web.config* 바꾸고 파일을 `connectionStrings` 요소를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="55313-372">Open the *Web.config* file and replace the `connectionStrings` element with the following code:</span></span>

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample8.xml)]

### <a name="creating-the-membership-database"></a><span data-ttu-id="55313-373">멤버 자격 데이터베이스를 만드는 중</span><span class="sxs-lookup"><span data-stu-id="55313-373">Creating the Membership Database</span></span>

<span data-ttu-id="55313-374">**솔루션 탐색기**ContosoUniversity 프로젝트를 선택한 다음 클릭 **ASP.NET 구성** 에 **프로젝트** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="55313-374">In **Solution Explorer**, select the ContosoUniversity project, and then click **ASP.NET Configuration** in the **Project** menu.</span></span>

<span data-ttu-id="55313-375">보안 탭을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-375">Select the Security tab.</span></span>

<span data-ttu-id="55313-376">클릭 **만들거나 역할 관리**을 만든 다음는 **관리자** 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-376">Click **Create or Manage Roles**, and then create an **Administrator** role.</span></span>

<span data-ttu-id="55313-377">보안 탭으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="55313-377">Return to the Security tab.</span></span>

<span data-ttu-id="55313-378">클릭 **사용자 만들기**를 선택한 후 합니다 **관리자** 관리자 라는 사용자를 만들고 확인란</span><span class="sxs-lookup"><span data-stu-id="55313-378">Click **Create user**, and then select the **Administrator** check box and create a user named admin.</span></span>

<span data-ttu-id="55313-379">닫기 합니다 **웹 사이트 관리 도구**합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-379">Close the **Web Site Administration Tool**.</span></span>

### <a name="creating-the-school-database"></a><span data-ttu-id="55313-380">School 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="55313-380">Creating the School Database</span></span>

<span data-ttu-id="55313-381">패키지 관리자 콘솔 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="55313-381">Open the Package Manager Console window.</span></span>

<span data-ttu-id="55313-382">에 **기본 프로젝트** 드롭 다운 목록 ContosoUniversity.DAL 프로젝트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-382">In the **Default project** drop-down list, select the ContosoUniversity.DAL project.</span></span>

<span data-ttu-id="55313-383">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-383">Enter the following command:</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample9.ps1)]

<span data-ttu-id="55313-384">데이터베이스를 만드는 AddBirthDate 마이그레이션을 적용 하는 초기 마이그레이션을 적용 하는 code First 마이그레이션을 다음 Seed 메서드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-384">Code First Migrations applies the Initial migration that creates the database and then applies the AddBirthDate migration, then it runs the Seed method.</span></span>

<span data-ttu-id="55313-385">사이트 컨트롤 F5 키를 눌러 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-385">Run the site by pressing Control-F5.</span></span> <span data-ttu-id="55313-386">테스트 및 프로덕션 환경에 대해 수행한 것 처럼 실행 합니다 **추가 학생** 페이지에서 새 학생을 추가 하 고 다음에 새 학생을 봅니다 합니다 **학생** 페이지.</span><span class="sxs-lookup"><span data-stu-id="55313-386">As you did for the test and production environments, run the **Add Students** page, add a new student, and then view the new student in the **Students** page.</span></span> <span data-ttu-id="55313-387">School 데이터베이스 생성 및 초기화 된 그리고 읽기 및 쓰기 액세스 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-387">This verifies that the School database was created and initialized and that you have read and write access to it.</span></span>

<span data-ttu-id="55313-388">선택 된 **업데이트 크레딧** 페이지 및 멤버 자격 데이터베이스가 배포 된 고에 액세스할 수 있는지 확인 하려면 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-388">Select the **Update Credits** page and log in to verify that the membership database was deployed and that you have access to it.</span></span> <span data-ttu-id="55313-389">사용자 계정을 마이그레이션하지 않은 경우 관리자 계정을 만들고 다음을 선택 합니다 **업데이트 크레딧** 페이지 작동 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-389">If you did not migrate your user accounts, create an administrator account and then select the **Update Credits** page to verify that it works.</span></span>

## <a name="cleaning-up-sql-server-compact-files"></a><span data-ttu-id="55313-390">SQL Server Compact 파일 정리</span><span class="sxs-lookup"><span data-stu-id="55313-390">Cleaning Up SQL Server Compact Files</span></span>

<span data-ttu-id="55313-391">파일 및 SQL Server Compact를 지원 하기 위해 포함 된 NuGet 패키지가 더 이상 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-391">You no longer need files and NuGet packages that were included to support SQL Server Compact.</span></span> <span data-ttu-id="55313-392">원하는 경우 (이 단계가 필요 하지 않습니다), 불필요 한 파일 및 참조를 정리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-392">If you want (this step is not required), you can clean up unneeded files and references.</span></span>

<span data-ttu-id="55313-393">**솔루션 탐색기**, 삭제 합니다 *.sdf* 에서 파일을 *앱\_데이터* 폴더 및 *amd64* 및 *x86* 폴더를 *bin* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-393">In **Solution Explorer**, delete the *.sdf* files from the *App\_Data* folder and the *amd64* and *x86* folders from the *bin* folder.</span></span>

<span data-ttu-id="55313-394">**솔루션 탐색기**(없습니다 프로젝트 중 하나), 솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **솔루션용 NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-394">In **Solution Explorer**, right-click the solution (not one of the projects), and then click **Manage NuGet Packages for Solution**.</span></span>

<span data-ttu-id="55313-395">왼쪽된 창에는 **NuGet 패키지 관리** 대화 상자에서 **설치 된 패키지**합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-395">In the left pane of the **Manage NuGet Packages** dialog box, select **Installed packages**.</span></span>

<span data-ttu-id="55313-396">선택 된 **EntityFramework.SqlServerCompact** 패키징하고 클릭 **관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-396">Select the **EntityFramework.SqlServerCompact** package and click **Manage**.</span></span>

<span data-ttu-id="55313-397">에 **프로젝트 선택** 대화 상자에서 두 프로젝트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-397">In the **Select Projects** dialog box, both projects are selected.</span></span> <span data-ttu-id="55313-398">두 프로젝트에서 패키지를 제거 하려면 두 확인란의 선택을 취소 한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="55313-398">To uninstall the package in both projects, clear both check boxes, then click **OK**.</span></span>

<span data-ttu-id="55313-399">또한 종속성 패키지를 제거 하려는 경우 요청 하는 대화 상자에서 클릭 아니요.</span><span class="sxs-lookup"><span data-stu-id="55313-399">In the dialog box that asks if you want to uninstall the dependent packages also, click No.</span></span> <span data-ttu-id="55313-400">다음 중 하나를 유지 해야 하는 Entity Framework 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-400">One of these is the Entity Framework package that you have to keep.</span></span>

<span data-ttu-id="55313-401">제거 하려면 동일한 절차에 따라 합니다 **SqlServerCompact** 패키지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-401">Follow the same procedure to uninstall the **SqlServerCompact** package.</span></span> <span data-ttu-id="55313-402">(때문에이 순서 대로 패키지를 제거 해야 합니다는 **EntityFramework.SqlServerCompact** 패키지에 따라 달라 집니다 합니다 **SqlServerCompact** 패키지 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="55313-402">(The packages must be uninstalled in this order because the **EntityFramework.SqlServerCompact** package depends on the **SqlServerCompact** package.)</span></span>

<span data-ttu-id="55313-403">이제 성공적으로 마이그레이션한 SQL Server Express와 전체 SQL Server입니다.</span><span class="sxs-lookup"><span data-stu-id="55313-403">You have now successfully migrated to SQL Server Express and full SQL Server.</span></span> <span data-ttu-id="55313-404">다음 자습서를 다른 데이터베이스 변경 및 해야 SQL Server Express 및 SQL Server 전체 테스트 및 프로덕션 데이터베이스를 사용 하는 경우 데이터베이스 변경 내용을 배포 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="55313-404">In the next tutorial you'll make another database change, and you'll see how to deploy database changes when your test and production databases use SQL Server Express and full SQL Server.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="55313-405">[이전](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
> [다음](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="55313-405">[Previous](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
[Next](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)</span></span>
