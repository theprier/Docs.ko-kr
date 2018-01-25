---
uid: mvc/overview/getting-started/database-first-development/setting-up-database
title: "Entity Framework 6 Database First MVC 5를 사용 하 여 시작 | Microsoft Docs"
author: tfitzmac
description: "MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 seri 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/01/2014
ms.topic: article
ms.assetid: 095abad4-3bfe-4f06-b092-ae6a735b7e49
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/database-first-development/setting-up-database
msc.type: authoredcontent
ms.openlocfilehash: cb979333131cc6ac87fd640bf7c96931054a1814
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="getting-started-with-entity-framework-6-database-first-using-mvc-5"></a><span data-ttu-id="8d3e6-104">Entity Framework 6 Database First MVC 5를 사용 하 여 시작 하기</span><span class="sxs-lookup"><span data-stu-id="8d3e6-104">Getting Started with Entity Framework 6 Database First using MVC 5</span></span>
====================
<span data-ttu-id="8d3e6-105">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="8d3e6-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="8d3e6-106">MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-106">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="8d3e6-107">이 자습서 시리즈 자동으로 표시, 편집를 만들 수 있도록 하는 코드를 생성 하 고 데이터베이스 테이블에 있는 데이터를 삭제 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-107">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="8d3e6-108">생성 된 코드는 데이터베이스 테이블의 열에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-108">The generated code corresponds to the columns in the database table.</span></span> <span data-ttu-id="8d3e6-109">시리즈의 마지막 부분에서 사이트와 데이터베이스 Azure에 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-109">In the last part of the series, you will deploy the site and database to Azure.</span></span>
> 
> <span data-ttu-id="8d3e6-110">시리즈의이 부분 데이터베이스를 만들고 데이터로 채우는에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-110">This part of the series focuses on creating a database and populating it with data.</span></span>
> 
> <span data-ttu-id="8d3e6-111">이 시리즈 기여 Tom Dykstra 및 Rick Anderson에서 작성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-111">This series was written with contributions from Tom Dykstra and Rick Anderson.</span></span> <span data-ttu-id="8d3e6-112">설명 섹션에는 사용자의 의견에로 기반 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-112">It was improved based on feedback from users in the comments section.</span></span>


## <a name="introduction"></a><span data-ttu-id="8d3e6-113">소개</span><span class="sxs-lookup"><span data-stu-id="8d3e6-113">Introduction</span></span>

<span data-ttu-id="8d3e6-114">이 항목에 기존 데이터베이스 및 신속 하 게 데이터와 상호 작용할 수 있도록 하는 웹 응용 프로그램을 만들 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-114">This topic shows how to start with an existing database and quickly create a web application that enables users to interact with the data.</span></span> <span data-ttu-id="8d3e6-115">Entity Framework 6 및 MVC 5는 사용 하 여 웹 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-115">It uses the Entity Framework 6 and MVC 5 to build the web application.</span></span> <span data-ttu-id="8d3e6-116">스 캐 폴딩 ASP.NET 기능을 사용 하면 자동으로 표시, 업데이트, 만들기 및 데이터 삭제에 대 한 코드를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-116">The ASP.NET Scaffolding feature enables you to automatically generate code for displaying, updating, creating and deleting data.</span></span> <span data-ttu-id="8d3e6-117">Visual Studio 내에서 게시 도구를 사용 하 여 쉽게 배포할 수 있습니다는 사이트 및 데이터베이스를 Azure입니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-117">Using the publishing tools within Visual Studio, you can easily deploy the site and database to Azure.</span></span>

<span data-ttu-id="8d3e6-118">이 항목에서는 데이터베이스 및 해당 데이터베이스의 필드를 기반으로 하는 웹 응용 프로그램에 대 한 코드를 생성 하려면 상황입니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-118">This topic addresses the situation where you have a database and want to generate code for a web application based on the fields of that database.</span></span> <span data-ttu-id="8d3e6-119">이 방법은 첫 번째 데이터베이스 개발을 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-119">This approach is called Database First development.</span></span> <span data-ttu-id="8d3e6-120">기존 데이터베이스 아직 없는 경우 데이터 클래스를 정의 하 고 클래스 속성에서 생성 하는 데이터베이스를 포함 하는 Code First 개발을 호출 하는 방법 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-120">If you do not already have an existing database, you can instead use an approach called Code First development which involves defining data classes and generating the database from the class properties.</span></span>

<span data-ttu-id="8d3e6-121">Code First 개발의 기본 예제를 보려면 [Getting Started with ASP.NET MVC 5](../introduction/getting-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-121">For an introductory example of Code First development, see [Getting Started with ASP.NET MVC 5](../introduction/getting-started.md).</span></span> <span data-ttu-id="8d3e6-122">고급 예제를 보려면 [ASP.NET MVC 4 응용 프로그램에 대 한 Entity Framework 데이터 모델을 만드는](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-122">For a more advanced example, see [Creating an Entity Framework Data Model for an ASP.NET MVC 4 App](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

<span data-ttu-id="8d3e6-123">사용 하려면 Entity Framework 방식을 선택에 대 한 지침을 참조 하십시오. [Entity Framework 개발 방법](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-123">For guidance on selecting which Entity Framework approach to use, see [Entity Framework Development Approaches](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d3e6-124">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="8d3e6-124">Prerequisites</span></span>

<span data-ttu-id="8d3e6-125">Visual Studio 2013 또는 Visual Studio Express 2013 for Web</span><span class="sxs-lookup"><span data-stu-id="8d3e6-125">Visual Studio 2013 or Visual Studio Express 2013 for Web</span></span>

## <a name="set-up-the-database"></a><span data-ttu-id="8d3e6-126">데이터베이스 설정</span><span class="sxs-lookup"><span data-stu-id="8d3e6-126">Set up the database</span></span>

<span data-ttu-id="8d3e6-127">환경을 모방 하기 위해는의 기존 데이터베이스를 먼저 데이터베이스 미리 채워진 데이터를 만들고 데이터베이스에 연결 하는 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-127">To mimic the environment of having an existing database, you will first create a database with some pre-filled data, and then create your web application that connects to the database.</span></span>

<span data-ttu-id="8d3e6-128">이 자습서는 Visual Studio 2013 또는 Visual Studio Express 2013과 함께 LocalDB를 사용 하 여 웹에 대 한 개발 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-128">This tutorial was developed using LocalDB with either Visual Studio 2013 or Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="8d3e6-129">LocalDB, 대신 기존 데이터베이스 서버를 사용할 수 있지만 프로그램 버전의 Visual Studio 및 데이터베이스 유형에 따라 데이터 도구는 Visual Studio의 모든 지원 되지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-129">You can use an existing database server instead of LocalDB, but depending on your version of Visual Studio and your type of database, all of the data tools in Visual Studio might not be supported.</span></span> <span data-ttu-id="8d3e6-130">도구를 데이터베이스에 대해 사용할 수 없는 경우 데이터베이스에 대 한 일부 관리 도구 모음 내에서 데이터베이스 관련 단계를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-130">If the tools are not available for your database, you may need to perform some of the database-specific steps within the management suite for your database.</span></span>

<span data-ttu-id="8d3e6-131">Visual Studio 버전에 데이터베이스 도구에 문제가 있는 경우 최신 버전의 데이터베이스 도구를 설치 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-131">If you have a problem with the database tools in your version of Visual Studio, make sure you have installed the latest version of the database tools.</span></span> <span data-ttu-id="8d3e6-132">업데이트 또는 데이터베이스 도구를 설치 하는 방법에 대 한 정보를 참조 하십시오. [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/hh297027)합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-132">For information about updating or installing the database tools, see [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/hh297027).</span></span>

<span data-ttu-id="8d3e6-133">Visual Studio를 시작 하 고 만듭니다는 **SQL Server 데이터베이스 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-133">Launch Visual Studio and create a **SQL Server Database Project**.</span></span> <span data-ttu-id="8d3e6-134">프로젝트 이름을 **ContosoUniversityData**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-134">Name the project **ContosoUniversityData**.</span></span>

![데이터베이스 프로젝트 만들기](setting-up-database/_static/image1.png)

<span data-ttu-id="8d3e6-136">이제 빈 데이터베이스 프로젝트가 준비 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-136">You now have an empty database project.</span></span> <span data-ttu-id="8d3e6-137">프로젝트에 대 한 대상 플랫폼으로 Azure SQL 데이터베이스를 설정 해야 하므로이 데이터베이스를 Azure이이 자습서의 뒷부분에 나오는 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-137">You will deploy this database to Azure later in this tutorial, so you'll need to set Azure SQL Database as the target platform for the project.</span></span> <span data-ttu-id="8d3e6-138">대상 플랫폼을 설정 배포 하지 않는 실제로 데이터베이스입니다. 데이터베이스 프로젝트는 데이터베이스 디자인 대상 플랫폼와 호환 되는지 확인만 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-138">Setting the target platform does not actually deploy the database; it only means that the database project will verify that the database design is compatible with the target platform.</span></span> <span data-ttu-id="8d3e6-139">대상 플랫폼을 설정 하려면 엽니다는 **속성** 선택한 프로젝트에 대 한 **Microsoft Azure SQL 데이터베이스** 대상 플랫폼에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-139">To set the target platform, open the **Properties** for the project and select **Microsoft Azure SQL Database** for the target platform.</span></span>

![집합 대상 플랫폼](setting-up-database/_static/image2.png)

<span data-ttu-id="8d3e6-141">테이블을 정의 하는 SQL 스크립트를 추가 하 여이 자습서에 필요한 테이블을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-141">You can create the tables needed for this tutorial by adding SQL scripts that define the tables.</span></span> <span data-ttu-id="8d3e6-142">프로젝트를 마우스 오른쪽 단추로 클릭 하 고 새 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-142">Right-click your project and add a new item.</span></span>

![새 항목 추가](setting-up-database/_static/image3.png)

<span data-ttu-id="8d3e6-144">학생 라는 새 테이블을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-144">Add a new table named Student.</span></span>

![학생 테이블 추가](setting-up-database/_static/image4.png)

<span data-ttu-id="8d3e6-146">테이블 파일에서 T-SQL 명령을 테이블을 만들려면 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-146">In the table file, replace the T-SQL command with the following code to create the table.</span></span>

[!code-sql[Main](setting-up-database/samples/sample1.sql)]

<span data-ttu-id="8d3e6-147">확인 코드와 디자인 창을 자동으로 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-147">Notice that the design window automatically synchronizes with the code.</span></span> <span data-ttu-id="8d3e6-148">코드 또는 디자이너를 사용 하 여 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-148">You can work with either the code or designer.</span></span>

![코드와 디자인 표시](setting-up-database/_static/image5.png)

<span data-ttu-id="8d3e6-150">다른 테이블을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-150">Add another table.</span></span> <span data-ttu-id="8d3e6-151">이 시간 과정 이름을 지정 하 고 다음 T-SQL 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-151">This time name it Course and use the following T-SQL command.</span></span>

[!code-sql[Main](setting-up-database/samples/sample2.sql)]

<span data-ttu-id="8d3e6-152">등록 라는 테이블을 만들려면 한 번 더 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-152">And, repeat one more time to create a table named Enrollment.</span></span>

[!code-sql[Main](setting-up-database/samples/sample3.sql)]

<span data-ttu-id="8d3e6-153">데이터베이스는 데이터베이스를 배포한 후 실행 되는 스크립트를 통해 데이터로 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-153">You can populate your database with data through a script that is run after the database is deployed.</span></span> <span data-ttu-id="8d3e6-154">배포 후 스크립트를 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-154">Add a Post-Deployment Script to the project.</span></span> <span data-ttu-id="8d3e6-155">기본 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-155">You can use the default name.</span></span>

![배포 후 스크립트를 추가 합니다.](setting-up-database/_static/image6.png)

<span data-ttu-id="8d3e6-157">다음 T-SQL 코드 배포 후 스크립트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-157">Add the following T-SQL code to the post-deployment script.</span></span> <span data-ttu-id="8d3e6-158">이 스크립트에 추가 하기만 하면 데이터는 데이터베이스 일치 하는 레코드가 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-158">This script simply adds data to the database when no matching record is found.</span></span> <span data-ttu-id="8d3e6-159">덮어쓰기 하거나 데이터베이스에 입력 데이터를 삭제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-159">It does not overwrite or delete any data you may have entered into the database.</span></span>

[!code-sql[Main](setting-up-database/samples/sample4.sql)]

<span data-ttu-id="8d3e6-160">데이터베이스 프로젝트를 배포할 때마다 배포 후 스크립트를 실행 하는 것이 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-160">It is important to note that the post-deployment script is run every time you deploy your database project.</span></span> <span data-ttu-id="8d3e6-161">따라서이 스크립트를 작성할 때 요구 사항을 신중 하 게 고려 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-161">Therefore, you need to carefully consider your requirements when writing this script.</span></span> <span data-ttu-id="8d3e6-162">경우에 따라 프로젝트 배포 될 때마다 알려진된 데이터 집합에서 다시 시작 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-162">In some cases, you may wish to start over from a known set of data every time the project is deployed.</span></span> <span data-ttu-id="8d3e6-163">다른 경우에는 기존 데이터에 어떤 방식으로 변경 하기 위해 하지 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-163">In other cases, you may not want to alter the existing data in any way.</span></span> <span data-ttu-id="8d3e6-164">요구 사항에 따라, 배포 후 스크립트 또는 스크립트에 포함 하는 데 필요한가 필요한 지 여부를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-164">Based on your requirements, you can decide whether you need a post-deployment script or what you need to include in the script.</span></span> <span data-ttu-id="8d3e6-165">배포 후 스크립트를 사용 하 여 데이터베이스를 채우기에 대 한 자세한 내용은 참조 [SQL Server 데이터베이스 프로젝트의 데이터를 포함 하 여](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-165">For more information about populating your database with a post-deployment script, see [Including Data in a SQL Server Database Project](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx).</span></span>

<span data-ttu-id="8d3e6-166">이제 4 SQL 스크립트 파일 하지만 실제 테이블이 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-166">You now have 4 SQL script files but no actual tables.</span></span> <span data-ttu-id="8d3e6-167">Localdb에 데이터베이스 프로젝트를 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-167">You are ready to deploy your database project to localdb.</span></span> <span data-ttu-id="8d3e6-168">Visual Studio에서 데이터베이스 프로젝트 빌드 및 배포를 시작 단추 (또는 f5 키)를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-168">In Visual Studio, click the Start button (or F5) to build and deploy your database project.</span></span> <span data-ttu-id="8d3e6-169">빌드 및 배포에 성공 했는지 확인 하려면 출력 탭을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-169">Check the Output tab to verify that the build and deployment succeeded.</span></span>

![출력 표시](setting-up-database/_static/image7.png)

<span data-ttu-id="8d3e6-171">새 데이터베이스가 만들어졌는지 확인 하려면 열고 **SQL Server 개체 탐색기** 올바른 로컬 데이터베이스 서버에 프로젝트의 이름을 찾습니다 (이 경우 **(localdb) \ProjectsV12**).</span><span class="sxs-lookup"><span data-stu-id="8d3e6-171">To see that the new database has been created, open **SQL Server Object Explorer** and look for the name of the project in the correct local database server (in this case **(localdb)\ProjectsV12**).</span></span>

![새 데이터베이스를 표시 합니다.](setting-up-database/_static/image8.png)

<span data-ttu-id="8d3e6-173">테이블 데이터가 할당 되는 확인 하려면 테이블을 마우스 오른쪽 단추로 클릭 하 고 선택 **데이터 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-173">To see that the tables are populated with data, right-click a table, and select **View Data**.</span></span>

![테이블 데이터 표시](setting-up-database/_static/image9.png)

<span data-ttu-id="8d3e6-175">테이블 데이터의 편집 가능한 뷰에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-175">An editable view of the table data is displayed.</span></span>

![테이블 데이터 결과 표시 합니다.](setting-up-database/_static/image10.png)

<span data-ttu-id="8d3e6-177">이제 데이터베이스 설정 되며 데이터로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-177">Your database is now set up and populated with data.</span></span> <span data-ttu-id="8d3e6-178">다음 자습서는 데이터베이스에 대 한 웹 응용 프로그램에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="8d3e6-178">In the next tutorial, you will create a web application for the database.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="8d3e6-179">다음</span><span class="sxs-lookup"><span data-stu-id="8d3e6-179">Next</span></span>](creating-the-web-application.md)
