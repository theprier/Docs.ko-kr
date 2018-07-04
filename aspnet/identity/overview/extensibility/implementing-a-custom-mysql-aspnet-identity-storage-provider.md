---
uid: identity/overview/extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider
title: 사용자 지정 MySQL ASP.NET Id 저장소 공급자 구현 | Microsoft Docs
author: raquelsa
description: ASP.NET Id는 사용자 고유의 저장소 공급자를 만들고 응용은 작업이 다시 실행 하지 않고 응용 프로그램에 연결할 수 있는 확장 가능한 시스템...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/22/2015
ms.topic: article
ms.assetid: 248f5fe7-39ba-40ea-ab1e-71a69b0bd649
ms.technology: ''
msc.legacyurl: /identity/overview/extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider
msc.type: authoredcontent
ms.openlocfilehash: 44c21b749377c5df445a20deee3f1b689c7c84c0
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37381129"
---
<a name="implementing-a-custom-mysql-aspnet-identity-storage-provider"></a><span data-ttu-id="a6e69-103">사용자 지정 MySQL ASP.NET Id 저장소 공급자 구현</span><span class="sxs-lookup"><span data-stu-id="a6e69-103">Implementing a Custom MySQL ASP.NET Identity Storage Provider</span></span>
====================
<span data-ttu-id="a6e69-104">하 여 [Raquel Soares De Almeida](https://github.com/raquelsa)하십시오 [Suhas Joshi](https://github.com/suhasj), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="a6e69-104">by [Raquel Soares De Almeida](https://github.com/raquelsa), [Suhas Joshi](https://github.com/suhasj), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="a6e69-105">ASP.NET Id는 확장 가능한 시스템 사용자 고유의 저장소 공급자를 만들고 응용 프로그램을 다시 사용 하지 않고 응용 프로그램에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-105">ASP.NET Identity is an extensible system which enables you to create your own storage provider and plug it into your application without re-working the application.</span></span> <span data-ttu-id="a6e69-106">이 항목에서는 ASP.NET Id에 대 한 MySQL 저장소 공급자를 만드는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-106">This topic describes how to create a MySQL storage provider for ASP.NET Identity.</span></span> <span data-ttu-id="a6e69-107">사용자 지정 저장소 공급자를 만드는 개요를 참조 하세요 [개요의 사용자 지정 저장소 공급자 ASP.NET Id에 대 한](overview-of-custom-storage-providers-for-aspnet-identity.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-107">For an overview of creating custom storage providers, see [Overview of Custom Storage Providers for ASP.NET Identity](overview-of-custom-storage-providers-for-aspnet-identity.md).</span></span>
> 
> <span data-ttu-id="a6e69-108">이 자습서를 완료 하려면 Visual Studio 2013 업데이트 2를 사용 하 여 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-108">To complete this tutorial, you must have Visual Studio 2013 with Update 2.</span></span>
> 
> <span data-ttu-id="a6e69-109">이 자습서는:</span><span class="sxs-lookup"><span data-stu-id="a6e69-109">This tutorial will:</span></span>
> 
> - <span data-ttu-id="a6e69-110">Azure에서 MySQL 데이터베이스 인스턴스를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-110">Show how to create a MySQL database instance on Azure.</span></span>
> - <span data-ttu-id="a6e69-111">MySQL 클라이언트 도구 (MySQL Workbench)를 사용 하 여 테이블을 만들고 Azure에서 원격 데이터베이스를 관리 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-111">Show how to use a MySQL client tool (MySQL Workbench) to create tables and manage your remote database on Azure.</span></span>
> - <span data-ttu-id="a6e69-112">ASP.NET Id 저장소 구현을 기본 MVC 응용 프로그램 프로젝트에서 사용자 지정 구현으로 대체 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-112">Show how to replace the default ASP.NET Identity storage implementation with our custom implementation on a MVC application project.</span></span>
> 
> <span data-ttu-id="a6e69-113">이 자습서가 원래 Raquel Soares De Almeida 및 Rick Anderson으로 작성 됩니다 ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) ).</span><span class="sxs-lookup"><span data-stu-id="a6e69-113">This tutorial was originally written by Raquel Soares De Almeida and Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ).</span></span> <span data-ttu-id="a6e69-114">샘플 프로젝트는 Suhas Joshi에서 Identity 2.0에 대 한 업데이트 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-114">The sample project was updated for Identity 2.0 by Suhas Joshi.</span></span> <span data-ttu-id="a6e69-115">항목은 Tom FitzMacken에서 Identity 2.0에 대 한 업데이트 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-115">The topic was updated for Identity 2.0 by Tom FitzMacken.</span></span>


## <a name="download-completed-project"></a><span data-ttu-id="a6e69-116">다운로드가 완료 된 프로젝트</span><span class="sxs-lookup"><span data-stu-id="a6e69-116">Download completed project</span></span>

<span data-ttu-id="a6e69-117">이 자습서의 끝 MVC 응용 프로그램 프로젝트를 Azure에서 호스트 되는 MySQL 데이터베이스를 사용 하는 ASP.NET id로 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-117">At the end of this tutorial, you will have an MVC application project with ASP.NET Identity working with a MySQL database hosted on Azure.</span></span>

<span data-ttu-id="a6e69-118">완료 된 MySQL 저장소 공급자를 다운로드할 수 있습니다 [AspNet.Identity.MySQL (CodePlex)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-118">You can download the completed MySQL storage provider at [AspNet.Identity.MySQL (CodePlex)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/).</span></span>

## <a name="the-steps-you-will-perform"></a><span data-ttu-id="a6e69-119">수행 하는 단계</span><span class="sxs-lookup"><span data-stu-id="a6e69-119">The steps you will perform</span></span>

<span data-ttu-id="a6e69-120">이 자습서에서는 다음을 수행 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-120">In this tutorial you will:</span></span>

1. <span data-ttu-id="a6e69-121">Azure에서 MySQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="a6e69-121">Create a MySQL database on Azure</span></span>
2. <span data-ttu-id="a6e69-122">MySQL에 ASP.NET Id 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="a6e69-122">Create the ASP.NET Identity tables in MySQL</span></span>
3. <span data-ttu-id="a6e69-123">MVC 응용 프로그램을 만들고 MySQL 공급자를 사용 하도록 구성</span><span class="sxs-lookup"><span data-stu-id="a6e69-123">Create an MVC application and configure it to use the MySQL provider</span></span>
4. <span data-ttu-id="a6e69-124">앱 실행</span><span class="sxs-lookup"><span data-stu-id="a6e69-124">Run the app</span></span>

<span data-ttu-id="a6e69-125">이 항목에서는 ASP.NET Id 및 고객 저장소 공급자를 구현 하는 경우 해야 결정의 아키텍처를 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-125">This topic does not cover the architecture of ASP.NET Identity and the decisions you must make when implementing a customer storage provider.</span></span> <span data-ttu-id="a6e69-126">해당 정보를 참조 하세요 [개요의 사용자 지정 저장소 공급자 ASP.NET Id에 대 한](overview-of-custom-storage-providers-for-aspnet-identity.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-126">For that information, see [Overview of Custom Storage Providers for ASP.NET Identity](overview-of-custom-storage-providers-for-aspnet-identity.md).</span></span>

## <a name="review-mysql-storage-provider-classes"></a><span data-ttu-id="a6e69-127">MySQL 저장소 공급자 클래스를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-127">Review MySQL storage provider classes</span></span>

<span data-ttu-id="a6e69-128">MySQL 저장소 공급자를 만드는 단계에 들어가기 전에 살펴보겠습니다 저장소 공급자를 구성 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-128">Before jumping into the steps to create the MySQL storage provider, let's look at the classes that make up the storage provider.</span></span> <span data-ttu-id="a6e69-129">데이터베이스 작업을 관리 하는 클래스 및 사용자 및 역할 관리 응용 프로그램에서 호출 되는 클래스 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-129">You will need classes that manage the database operations and classes that are called from the application to manage users and roles.</span></span>

### <a name="storage-classes"></a><span data-ttu-id="a6e69-130">저장소 클래스</span><span class="sxs-lookup"><span data-stu-id="a6e69-130">Storage classes</span></span>

- <span data-ttu-id="a6e69-131">[IdentityUser](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/IdentityUser.cs) -사용자에 대 한 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-131">[IdentityUser](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/IdentityUser.cs) - contains properties for the user.</span></span>
- <span data-ttu-id="a6e69-132">[UserStore](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserStore.cs) -추가, 업데이트 또는 사용자 검색에 대 한 작업을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-132">[UserStore](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserStore.cs) - contains operations for adding, updating or retrieving users.</span></span>
- <span data-ttu-id="a6e69-133">[IdentityRole](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/IdentityRole.cs) -역할에 대 한 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-133">[IdentityRole](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/IdentityRole.cs) - contains properties for roles.</span></span>
- <span data-ttu-id="a6e69-134">[RoleStore](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/RoleStore.cs) -추가, 삭제, 업데이트 및 역할을 검색 하는 작업이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-134">[RoleStore](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/RoleStore.cs) - contains operations for adding, deleting, updating and retrieving roles.</span></span>

### <a name="data-access-layer-classes"></a><span data-ttu-id="a6e69-135">데이터 액세스 계층 클래스</span><span class="sxs-lookup"><span data-stu-id="a6e69-135">Data access layer classes</span></span>

<span data-ttu-id="a6e69-136">예를 들어 데이터 액세스 계층 클래스는 테이블; 작업에 대 한 SQL 문을 포함 그러나 코드에서 Entity Framework 또는 NHibernate 같은 개체-관계형 매핑 (ORM)를 사용 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-136">For this example, the data access layer classes contain SQL statements for working with the tables; however, in your code you might want to use object-relational mapping (ORM) such as Entity Framework or NHibernate.</span></span> <span data-ttu-id="a6e69-137">특히, 응용 프로그램 지연 로드 및 개체 캐싱을 포함 하는 ORM 없이 성능 저하를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-137">In particular, your application may experience poor performance without an ORM that includes lazy loading and object caching.</span></span> <span data-ttu-id="a6e69-138">자세한 내용은 참조 하세요. [Entity Framework 없이 ASP.NET Identity 2.0?](https://aspnetidentity.codeplex.com/discussions/561828)</span><span class="sxs-lookup"><span data-stu-id="a6e69-138">For more information, see [ASP.NET Identity 2.0 without Entity Framework?](https://aspnetidentity.codeplex.com/discussions/561828)</span></span>

- <span data-ttu-id="a6e69-139">[MySQLDatabase](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) -MySQL 데이터베이스 연결 및 데이터베이스 작업을 수행 하기 위한 메서드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-139">[MySQLDatabase](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) - contains the MySQL database connection and methods for performing database operations.</span></span> <span data-ttu-id="a6e69-140">UserStore 및 RoleStore이이 클래스의 인스턴스를 사용 하 여 인스턴스화됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-140">UserStore and RoleStore are both instantiated with an instance of this class.</span></span>
- <span data-ttu-id="a6e69-141">[RoleTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/RoleTable.cs) -역할을 저장 하는 테이블에 대 한 데이터베이스 작업을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-141">[RoleTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/RoleTable.cs) - contains database operations for the table that stores roles.</span></span>
- <span data-ttu-id="a6e69-142">[UserClaimsTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) -사용자 클레임을 저장 하는 테이블에 대 한 데이터베이스 작업을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-142">[UserClaimsTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) - contains database operations for the table that stores user claims.</span></span>
- <span data-ttu-id="a6e69-143">[UserLoginsTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) -사용자 로그인 정보를 저장 하는 테이블에 대 한 데이터베이스 작업을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-143">[UserLoginsTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) - contains database operations for the table that stores user login information.</span></span>
- <span data-ttu-id="a6e69-144">[UserRoleTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) -역할에 할당 된 사용자를 저장 하는 테이블에 대 한 데이터베이스 작업을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-144">[UserRoleTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) - contains database operations for the table that stores which users are assigned to which roles.</span></span>
- <span data-ttu-id="a6e69-145">[UserTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserTable.cs) -사용자를 저장 하는 테이블에 대 한 데이터베이스 작업을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-145">[UserTable](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/UserTable.cs) - contains database operations for the table that stores users.</span></span>

## <a name="create-a-mysql-database-instance-on-azure"></a><span data-ttu-id="a6e69-146">Azure에서 MySQL 데이터베이스 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="a6e69-146">Create a MySQL database instance on Azure</span></span>

1. <span data-ttu-id="a6e69-147">[Azure Portal](https://manage.windowsazure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-147">Log in to the [Azure Portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="a6e69-148">클릭 **+ 새로 만들기** 한 다음 선택한 페이지의 맨 아래에서 **스토어**합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-148">Click **+NEW** at the bottom of the page, and then select **STORE**.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.png)
3. <span data-ttu-id="a6e69-149">에 **선택 및 추가 기능** 마법사 **ClearDB MySQL 데이터베이스** 대화의 오른쪽 맨 아래에 있는 다음 화살표를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-149">In the **Choose and Add-on** wizard, select **ClearDB MySQL Database** and click on the next arrow at the bottom right of the dialog.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.png)
4. <span data-ttu-id="a6e69-150">기본값을 유지 **무료** 계획 하 고 변경 합니다 **이름** 하 **IdentityMySQLDatabase**합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-150">Keep the default **Free** plan and change the **Name** to **IdentityMySQLDatabase**.</span></span> <span data-ttu-id="a6e69-151">가장 가까운 지역을 선택 하 고 화살표를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-151">Select the region nearest you and then click the next arrow.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.png)
5. <span data-ttu-id="a6e69-152">데이터베이스 만들기를 완료 하려면 확인 표시를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-152">Click the checkmark to complete the database creation.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image4.png)
6. <span data-ttu-id="a6e69-153">데이터베이스를 만든 후에서 관리할 수 있습니다 합니다 **추가 기능** 관리 포털에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-153">After your database has been created, you can manage it from the **ADD-ONS** tab in the management portal.</span></span>   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image5.png)
7. <span data-ttu-id="a6e69-154">클릭 하 여 데이터베이스 연결 정보를 가져올 수 있습니다 **연결 정보** 페이지의 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-154">You can get the database connection information by clicking on **CONNECTION INFO** at the bottom of the page.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image6.png)
8. <span data-ttu-id="a6e69-155">복사 단추를 클릭 하 여 연결 문자열을 복사 하 고 나중에 MVC 응용 프로그램에서 사용할 수 있도록 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-155">Copy the connection string by clicking on the copy button and save it so you can use later in your MVC application.</span></span>   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image7.png)

## <a name="create-the-aspnet-identity-tables-in-a-mysql-database"></a><span data-ttu-id="a6e69-156">MySQL 데이터베이스에 ASP.NET Id 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="a6e69-156">Create the ASP.NET Identity tables in a MySQL database</span></span>

### <a name="install-mysql-workbench-tool-to-connect-and-manage-mysql-database"></a><span data-ttu-id="a6e69-157">MySQL Workbench 연결 하 여 MySQL 데이터베이스를 관리 하는 도구를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-157">Install MySQL Workbench tool to connect and manage MySQL database</span></span>

1. <span data-ttu-id="a6e69-158">설치 합니다 **MySQL Workbench** 에서 도구는 [MySQL 다운로드 페이지](http://dev.mysql.com/downloads/windows/installer/)</span><span class="sxs-lookup"><span data-stu-id="a6e69-158">Install the **MySQL Workbench** tool from the [MySQL downloads page](http://dev.mysql.com/downloads/windows/installer/)</span></span>
2. <span data-ttu-id="a6e69-159">앱을 시작 하 고 클릭에 추가 합니다 **MySQLConnections +** 단추를 새 연결을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-159">Launch the app and add click on the **MySQLConnections +** button to add a new connection.</span></span> <span data-ttu-id="a6e69-160">이 자습서의 앞부분에서 만든 Azure MySQL 데이터베이스에서 복사한 연결 문자열 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-160">Use the connection string data you copied from the Azure MySQL database you created earlier in this tutorial.</span></span>
3. <span data-ttu-id="a6e69-161">연결을 만든 후 새 엽니다 **쿼리** 탭,에서 명령을 붙여 [MySQLIdentity.sql](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql) 쿼리로 데이터베이스 테이블을 만들기 위해 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-161">After establishing the connection, open a new **Query** tab; paste the commands from [MySQLIdentity.sql](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql) into the query and execute it in order to create the database tables.</span></span>
4. <span data-ttu-id="a6e69-162">이제 ASP.NET Id 필요한 모든 테이블 아래와 같이 Azure에서 호스트 되는 MySQL 데이터베이스에 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-162">You now have all the ASP.NET Identity necessary tables created on a MySQL database hosted on Azure as shown below.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.jpg)

## <a name="create-an-mvc-application-project-from-template-and-configure-it-to-use-mysql-provider"></a><span data-ttu-id="a6e69-163">템플릿에서 MVC 응용 프로그램 프로젝트를 만들고 MySQL 공급자를 사용 하도록 구성</span><span class="sxs-lookup"><span data-stu-id="a6e69-163">Create an MVC application project from template and configure it to use MySQL provider</span></span>

<span data-ttu-id="a6e69-164">필요한 경우 설치할 [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) 하거나 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) 업데이트 2를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-164">If needed, install either [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) with Update 2.</span></span>

### <a name="download-the-aspnetidentitymysql-project-from-codeplex"></a><span data-ttu-id="a6e69-165">CodePlex의 ASP.NET.Identity.MySQL 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-165">Download the ASP.NET.Identity.MySQL project from CodePlex</span></span>

1. <span data-ttu-id="a6e69-166">리포지토리 URL로 이동 [AspNet.Identity.MySQL (CodePlex)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-166">Browse to the repository URL at [AspNet.Identity.MySQL (CodePlex)](https://aspnet.codeplex.com/SourceControl/latest#Samples/Identity/AspNet.Identity.MySQL/).</span></span>
2. <span data-ttu-id="a6e69-167">소스 코드를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-167">Download the source code.</span></span>
3. <span data-ttu-id="a6e69-168">로컬 폴더에.zip 파일을 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-168">Extract the .zip file into a local folder.</span></span>
4. <span data-ttu-id="a6e69-169">AspNet.Identity.MySQL 솔루션을 열고 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="a6e69-169">Open the AspNet.Identity.MySQL solution and build it.</span></span>

### <a name="create-a-new-mvc-application-project-from-template"></a><span data-ttu-id="a6e69-170">템플릿에서 새 MVC 응용 프로그램 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="a6e69-170">Create a new MVC application project from template</span></span>

1. <span data-ttu-id="a6e69-171">마우스 오른쪽 단추로 클릭 합니다 **AspNet.Identity.MySQL** 솔루션 및 **추가**, **새 프로젝트**</span><span class="sxs-lookup"><span data-stu-id="a6e69-171">Right click the **AspNet.Identity.MySQL** solution and **Add**, **New Project**</span></span>
2. <span data-ttu-id="a6e69-172">에 **새 프로젝트 추가** 대화 상자 선택 **Visual C#** 왼쪽에서 다음 **웹** 선택한 후 **ASP.NET 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-172">In the **Add New Project** Dialog select **Visual C#** on the left, then **Web** and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="a6e69-173">프로젝트 이름을 **IdentityMySQLDemo**; 확인을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-173">Name your project **IdentityMySQLDemo**; and then click OK.</span></span>  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.jpg)
3. <span data-ttu-id="a6e69-174">에 **새 ASP.NET 프로젝트** 대화 상자에서 기본 옵션을 사용 하 여 MVC 템플릿을 선택 (포함 하는 **개별 사용자 계정** 인증 방법으로)를 클릭 하 고 **확인** .![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.jpg)</span><span class="sxs-lookup"><span data-stu-id="a6e69-174">In the **New ASP.NET Project** dialog, select the MVC template with the default options (that includes **Individual User Accounts** as authentication method) and click **OK**.![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.jpg)</span></span>
4. <span data-ttu-id="a6e69-175">솔루션 탐색기에서 IdentityMySQLDemo 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-175">In Solution Explorer, right-click your IdentityMySQLDemo project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="a6e69-176">검색 텍스트 상자 대화 상자에서 입력 **Identity.EntityFramework**합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-176">In the search text box dialog, type **Identity.EntityFramework**.</span></span> <span data-ttu-id="a6e69-177">결과 목록에서이 패키지를 선택 하 고 클릭 **제거**합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-177">Select this package in the list of results and click **Uninstall**.</span></span> <span data-ttu-id="a6e69-178">EntityFramework 종속성 패키지를 제거 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-178">You will be prompted to uninstall the dependency package EntityFramework.</span></span> <span data-ttu-id="a6e69-179">예를 클릭이 응용 프로그램에서이 패키지는 더 이상.</span><span class="sxs-lookup"><span data-stu-id="a6e69-179">Click on Yes as we will no longer this package on this application.</span></span>
5. <span data-ttu-id="a6e69-180">IdentityMySQLDemo 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음를 선택 합니다 **추가**하십시오 **참조, 솔루션, 프로젝트** AspNet.Identity.MySQL 프로젝트를 선택 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-180">Right click the IdentityMySQLDemo project, select **Add**, **Reference, Solution, Projects;** select the AspNet.Identity.MySQL project and click **OK**.</span></span>
6. <span data-ttu-id="a6e69-181">IdentityMySQLDemo 프로젝트에 대 한 모든 참조를 대체</span><span class="sxs-lookup"><span data-stu-id="a6e69-181">In the IdentityMySQLDemo project, replace all references to</span></span>  
    `using Microsoft.AspNet.Identity.EntityFramework;`  
   <span data-ttu-id="a6e69-182">다음 문자열로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="a6e69-182">with</span></span>  
     `using AspNet.Identity.MySQL;`
7. <span data-ttu-id="a6e69-183">IdentityModels.cs를 설정 **ApplicationDbContext** 에서 파생 시키는 **MySqlDatabase** 연결 이름이 단일 매개 변수를 사용 하는 생성자를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-183">In IdentityModels.cs, set **ApplicationDbContext** to derive from **MySqlDatabase** and include a contructor that take a single parameter with the connection name.</span></span>  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample1.cs)]
8. <span data-ttu-id="a6e69-184">IdentityConfig.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-184">Open the IdentityConfig.cs file.</span></span> <span data-ttu-id="a6e69-185">에 **ApplicationUserManager.Create** 메서드를 다음 코드를 사용 하 여 UserManager 인스턴스화 바꾸기:</span><span class="sxs-lookup"><span data-stu-id="a6e69-185">In the **ApplicationUserManager.Create** method, replace instantiating UserManager with the following code:</span></span>  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample2.cs)]
9. <span data-ttu-id="a6e69-186">Web.config 파일을 열고이 항목의 이전 단계에서 만든 MySQL 데이터베이스 연결 문자열을 사용 하 여 강조 표시 된 값 대체를 사용 하 여 DefaultConnection 문자열을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-186">Open the web.config file and replace the DefaultConnection string with this entry replacing the highlighted values with the connection string of the MySQL database you created on previous steps:</span></span>  

    [!code-xml[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample3.xml?highlight=2)]

## <a name="run-the-app-and-connect-to-the-mysql-db"></a><span data-ttu-id="a6e69-187">앱을 실행 하 고 MySQL DB에 연결</span><span class="sxs-lookup"><span data-stu-id="a6e69-187">Run the app and connect to the MySQL DB</span></span>

1. <span data-ttu-id="a6e69-188">마우스 오른쪽 단추로 클릭 합니다 **IdentityMySQLDemo** 프로젝트를 마우스 **시작 프로젝트로 설정**</span><span class="sxs-lookup"><span data-stu-id="a6e69-188">Right click the **IdentityMySQLDemo** project and select **Set as Startup Project**</span></span>
2. <span data-ttu-id="a6e69-189">키를 눌러 **ctrl+f5** 를 빌드하고 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-189">Press **Ctrl + F5** to build and run the app.</span></span>
3. <span data-ttu-id="a6e69-190">클릭할 **등록** 페이지 위쪽의 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-190">Click on **Register** tab on the top of the page.</span></span>
4. <span data-ttu-id="a6e69-191">새 사용자 이름 및 암호를 입력 하 고 클릭 **등록**합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-191">Enter a new user name and password and then click on **Register**.</span></span>  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image8.png)
5. <span data-ttu-id="a6e69-192">이제 새 사용자 등록 되 고 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-192">The new user is now registered and logged in.</span></span>  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image9.png)
6. <span data-ttu-id="a6e69-193">MySQL Workbench 도구로 다시 이동 하 고 검사 합니다 **IdentityMySQLDatabase** 테이블의 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-193">Go back to the MySQL Workbench tool and inspect the **IdentityMySQLDatabase** table's contents.</span></span> <span data-ttu-id="a6e69-194">새 사용자를 등록 하는 대로 항목에 대 한 사용자 테이블을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-194">Inspect the users table for the entries as you register new users.</span></span>  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image10.png)

## <a name="next-steps"></a><span data-ttu-id="a6e69-195">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a6e69-195">Next Steps</span></span>

<span data-ttu-id="a6e69-196">이 앱에 다른 인증 방법을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 참조 [Facebook 및 Google OAuth2 및 OpenID Sign on을 사용 하 여 ASP.NET MVC 5 앱 만들기](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-196">For more information on how to enable other authentication methods on this app, refer to [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>

<span data-ttu-id="a6e69-197">OAuth를 사용 하 여 DB를 통합 하 고 앱에 대 한 사용자 액세스를 제한 하려면 역할을 설정 하는 방법에 알아보려면 참조 [멤버 자격, OAuth 및 SQL Database를 사용 하 여 보안 ASP.NET MVC 5 앱을 Azure에 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다.</span><span class="sxs-lookup"><span data-stu-id="a6e69-197">To learn how to integrate your DB with OAuth and to set up roles to limit users access to your app, see [Deploy a Secure ASP.NET MVC 5 app with Membership, OAuth, and SQL Database to Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span>
