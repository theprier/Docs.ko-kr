---
uid: identity/overview/getting-started/aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider
title: ": ASP.NET Identity EntityFramework MySQL 공급자 (C#)와 함께 MySQL 저장소를 사용 하 여 | Microsoft Docs"
author: maumar
description: "이 자습서에서는 MySQL 견실한와 EntityFramework (SQL 클라이언트 공급자)으로 ASP.NET Identity에 대 한 기본 데이터 저장소 메커니즘을 바꾸는 방법을 보여 줍니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/10/2013
ms.topic: article
ms.assetid: 15253312-a92c-43ba-908e-b5dacd3d08b8
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /identity/overview/getting-started/aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider
msc.type: authoredcontent
ms.openlocfilehash: ac254abcb756d048d159a9b67967a581f35ac871
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider-c"></a><span data-ttu-id="22b74-103">: ASP.NET Identity EntityFramework MySQL 공급자 (C#) MySQL 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="22b74-103">ASP.NET Identity: Using MySQL Storage with an EntityFramework MySQL Provider (C#)</span></span>
====================
<span data-ttu-id="22b74-104">여 [Maurycy Markowski](https://github.com/maumar), [Raquel Soares De Almeida](https://github.com/raquelsa), [Robert McMurray](https://github.com/rmcmurray)</span><span class="sxs-lookup"><span data-stu-id="22b74-104">by [Maurycy Markowski](https://github.com/maumar), [Raquel Soares De Almeida](https://github.com/raquelsa), [Robert McMurray](https://github.com/rmcmurray)</span></span>

> <span data-ttu-id="22b74-105">이 자습서에 대 한 기본 데이터 저장소 메커니즘을 대체 하는 방법을 보여 줍니다. [ **ASP.NET Identity** ](introduction-to-aspnet-identity.md) EntityFramework (SQL 클라이언트 공급자)는 MySQL 공급자와 함께 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-105">This tutorial shows you how to replace the default data storage mechanism for [**ASP.NET Identity**](introduction-to-aspnet-identity.md) with EntityFramework (SQL client provider) with a MySQL provider.</span></span>


<span data-ttu-id="22b74-106">이 자습서는 다음 항목 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-106">The following topics will be covered in this tutorial:</span></span>

- <span data-ttu-id="22b74-107">Azure에서 MySQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="22b74-107">Creating a MySQL database on Azure</span></span>
- <span data-ttu-id="22b74-108">Visual Studio 2013 MVC 템플릿을 사용 하 여 MVC 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="22b74-108">Creating an MVC application using Visual Studio 2013 MVC template</span></span>
- <span data-ttu-id="22b74-109">EntityFramework MySQL 데이터베이스 공급자와 작동 하도록 구성</span><span class="sxs-lookup"><span data-stu-id="22b74-109">Configuring EntityFramework to work with a MySQL database provider</span></span>
- <span data-ttu-id="22b74-110">결과 확인 하려면 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="22b74-110">Running the application to verify the results</span></span>

<span data-ttu-id="22b74-111">이 자습서를 마치면 나면 MVC 응용 프로그램을 ASP.NET Identity 저장 Azure에서 호스팅하는 MySQL 데이터베이스를 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-111">At the end of this tutorial, you will have an MVC application with the ASP.NET Identity store that is using a MySQL database that is hosted in Azure.</span></span>

## <a name="creating-a-mysql-database-instance-on-azure"></a><span data-ttu-id="22b74-112">Azure에서 MySQL 데이터베이스 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="22b74-112">Creating a MySQL database instance on Azure</span></span>

1. <span data-ttu-id="22b74-113">에 로그인 하 고 [Azure 포털](https://go.microsoft.com/fwlink/?linkid=529715&amp;clcid=0x409)합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-113">Log in to the [Azure Portal](https://go.microsoft.com/fwlink/?linkid=529715&amp;clcid=0x409).</span></span>
2. <span data-ttu-id="22b74-114">클릭 **새로** 페이지 및 다음 선택의 맨 아래에 **저장소**:</span><span class="sxs-lookup"><span data-stu-id="22b74-114">Click **NEW** at the bottom of the page, and then select **STORE**:</span></span>  
  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image2.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image1.png)
3. <span data-ttu-id="22b74-115">에 **선택 및 추가 기능** 선택 마법사 **ClearDB MySQL 데이터베이스**, 클릭 하 고는 **다음** 프레임의 아래쪽 화살표:</span><span class="sxs-lookup"><span data-stu-id="22b74-115">In the **Choose and Add-on** wizard, select **ClearDB MySQL Database**, and then click the **Next** arrow at the bottom of the frame:</span></span>  
  
 <span data-ttu-id="22b74-116">[확장 하려면 다음 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-116">[Click the following image to expand it.</span></span> <span data-ttu-id="22b74-117">]</span><span class="sxs-lookup"><span data-stu-id="22b74-117">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image4.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image3.png)
4. <span data-ttu-id="22b74-118">기본값을 유지 **무료** 변경, 계획 된 **이름** 를 **IdentityMySQLDatabase**영역을 가장 가까운 항목을 선택한 다음 클릭는 **다음** 프레임의 아래쪽 화살표:</span><span class="sxs-lookup"><span data-stu-id="22b74-118">Keep the default **Free** plan, change the **NAME** to **IdentityMySQLDatabase**, select the region that is nearest to you, and then click the **Next** arrow at the bottom of the frame:</span></span>  
  
 <span data-ttu-id="22b74-119">[확장 하려면 다음 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-119">[Click the following image to expand it.</span></span> <span data-ttu-id="22b74-120">]</span><span class="sxs-lookup"><span data-stu-id="22b74-120">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image6.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image5.png)
5. <span data-ttu-id="22b74-121">클릭는 **구매** 데이터베이스 만들기를 완료 하려면 확인 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-121">Click the **PURCHASE** checkmark to complete the database creation.</span></span>  
  
 <span data-ttu-id="22b74-122">[확장 하려면 다음 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-122">[Click the following image to expand it.</span></span> <span data-ttu-id="22b74-123">]</span><span class="sxs-lookup"><span data-stu-id="22b74-123">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image8.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image7.png)
6. <span data-ttu-id="22b74-124">데이터베이스를 만든 후에서 관리할 수 있습니다는 **추가 기능** 관리 포털에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-124">After your database has been created, you can manage it from the **ADD-ONS** tab in the management portal.</span></span> <span data-ttu-id="22b74-125">데이터베이스에 대 한 연결 정보를 검색 하려면 클릭 **연결 정보입니다.** 페이지의 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-125">To retrieve the connection information for your database, click **CONNECTION INFO** at the bottom of the page:</span></span>  
  
 <span data-ttu-id="22b74-126">[확장 하려면 다음 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-126">[Click the following image to expand it.</span></span> <span data-ttu-id="22b74-127">]</span><span class="sxs-lookup"><span data-stu-id="22b74-127">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image10.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image9.png)
7. <span data-ttu-id="22b74-128">[복사] 단추를 클릭 하 여 연결 문자열을 복사는 **CONNECTIONSTRING** 필드 및 저장; MVC 응용 프로그램에 대 한이 자습서의 뒷부분에서이 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-128">Copy the connection string by clicking on the copy button by the **CONNECTIONSTRING** field and save it; you will use this information later in this tutorial for your MVC application:</span></span>  
  
 <span data-ttu-id="22b74-129">[확장 하려면 다음 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-129">[Click the following image to expand it.</span></span> <span data-ttu-id="22b74-130">]</span><span class="sxs-lookup"><span data-stu-id="22b74-130">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image12.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image11.png)

## <a name="creating-an-mvc-application-project"></a><span data-ttu-id="22b74-131">MVC 응용 프로그램 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="22b74-131">Creating an MVC application project</span></span>

<span data-ttu-id="22b74-132">자습서의이 섹션의 단계를 완료 하려면 먼저 할 설치 [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) 또는 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-132">To complete the steps in this section of the tutorial, you will first need to install [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="22b74-133">Visual Studio를 설치한 후 새 MVC 응용 프로그램 프로젝트를 만들려면 다음 단계를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-133">Once Visual Studio has been installed, use the following steps to create a new MVC application project:</span></span>

1. <span data-ttu-id="22b74-134">Visual Studio 2013을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-134">Open Visual Studio 2103.</span></span>
2. <span data-ttu-id="22b74-135">클릭 **새 프로젝트** 에서 **시작** 페이지 또는 있습니다 클릭할 수는 **파일** 메뉴 차례로 **새 프로젝트**:</span><span class="sxs-lookup"><span data-stu-id="22b74-135">Click **New Project** from the **Start** page, or you can click the **File** menu and then **New Project**:</span></span>  
  
 <span data-ttu-id="22b74-136">[확장 하려면 다음 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-136">[Click the following image to expand it.</span></span> <span data-ttu-id="22b74-137">]</span><span class="sxs-lookup"><span data-stu-id="22b74-137">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image2.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image1.jpg)
3. <span data-ttu-id="22b74-138">경우는 **새 프로젝트** 대화 상자가 표시 됩니다, 확장 **Visual C#** 템플릿 목록에서 클릭 **웹**를 선택 하 고 **ASP.NET 웹 응용 프로그램**.</span><span class="sxs-lookup"><span data-stu-id="22b74-138">When the **New Project** dialog box is displayed, expand **Visual C#** in the list of templates, then click **Web**, and select **ASP.NET Web Application**.</span></span> <span data-ttu-id="22b74-139">프로젝트 이름을 **IdentityMySQLDemo** 클릭 하 고 **확인**:</span><span class="sxs-lookup"><span data-stu-id="22b74-139">Name your project **IdentityMySQLDemo** and then click **OK**:</span></span>  
  
 <span data-ttu-id="22b74-140">[확장 하려면 다음 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-140">[Click the following image to expand it.</span></span> <span data-ttu-id="22b74-141">]</span><span class="sxs-lookup"><span data-stu-id="22b74-141">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image14.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image13.png)
4. <span data-ttu-id="22b74-142">에 **새 ASP.NET 프로젝트** 대화 상자에서는 **MVC** templatewith 기본 옵션; 이렇게 설정이 하면 구성 **개별 사용자 계정** 인증 방법으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-142">In the **New ASP.NET Project** dialog, select the **MVC** templatewith the default options; this will configure **Individual User Accounts** as the authentication method.</span></span> <span data-ttu-id="22b74-143">클릭 **확인**:</span><span class="sxs-lookup"><span data-stu-id="22b74-143">Click **OK**:</span></span>  
  
 <span data-ttu-id="22b74-144">[확장 하려면 다음 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-144">[Click the following image to expand it.</span></span> <span data-ttu-id="22b74-145">]</span><span class="sxs-lookup"><span data-stu-id="22b74-145">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image16.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image15.png)

## <a name="configure-entityframework-to-work-with-a-mysql-database"></a><span data-ttu-id="22b74-146">MySQL 데이터베이스를 작성 하려면 EntityFramework 구성</span><span class="sxs-lookup"><span data-stu-id="22b74-146">Configure EntityFramework to work with a MySQL database</span></span>

### <a name="update-the-entity-framework-assembly-for-your-project"></a><span data-ttu-id="22b74-147">프로젝트에 대 한 Entity Framework 어셈블리를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-147">Update the Entity Framework assembly for your project</span></span>

<span data-ttu-id="22b74-148">Visual Studio 2013 서식 파일에서 만든 MVC 응용 프로그램에 대 한 참조를 포함 된 [EntityFramework 6.0.0](http://www.nuget.org/packages/EntityFramework) 있어야 하지만 패키지 하 고, 업데이트를 해당 릴리스 이후 해당 어셈블리에 포함 된 중요 한 되었습니다 성능 향상입니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-148">The MVC application that was created from the Visual Studio 2013 template contains a reference to the [EntityFramework 6.0.0](http://www.nuget.org/packages/EntityFramework) package, but there have been updates to to that assembly since its release which contain significant performance improvements.</span></span> <span data-ttu-id="22b74-149">응용 프로그램에서 이러한 최신 업데이트를 사용 하려면 다음 단계를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-149">In order to use these latest updates in your application, use the following steps.</span></span>

1. <span data-ttu-id="22b74-150">Visual Studio 2013에서 MVC 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-150">Open your MVC project in Visual Studio 2013.</span></span>
2. <span data-ttu-id="22b74-151">클릭 **도구**, 클릭 **라이브러리 패키지 관리자**, 클릭 하 고 **패키지 관리자 콘솔**:</span><span class="sxs-lookup"><span data-stu-id="22b74-151">Click **TOOLS**, then click **Library Package Manager**, and then click **Package Manager Console**:</span></span>  
  
 <span data-ttu-id="22b74-152">[확장 하려면 다음 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-152">[Click the following image to expand it.</span></span> <span data-ttu-id="22b74-153">]</span><span class="sxs-lookup"><span data-stu-id="22b74-153">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image18.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image17.png)
3. <span data-ttu-id="22b74-154">**패키지 관리자 콘솔** Visual Studio의 아래쪽 섹션에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-154">The **Package Manager Console** will appear in the bottom section of Visual Studio.</span></span> <span data-ttu-id="22b74-155">형식 &quot; **업데이트 패키지 EntityFramework** &quot; Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-155">Type &quot;**Update-Package EntityFramework**&quot; and press Enter:</span></span>  
  
 <span data-ttu-id="22b74-156">[확장 하려면 다음 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-156">[Click the following image to expand it.</span></span> <span data-ttu-id="22b74-157">]</span><span class="sxs-lookup"><span data-stu-id="22b74-157">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image20.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image19.png)

### <a name="install-the-mysql-provider-for-entityframework"></a><span data-ttu-id="22b74-158">EntityFramework에 대 한 MySQL 공급자를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-158">Install the MySQL provider for EntityFramework</span></span>

<span data-ttu-id="22b74-159">MySQL 데이터베이스에 연결 하는 EntityFramework MySQL 공급자를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-159">In order for EntityFramework to connect to MySQL database, you need to install a MySQL provider.</span></span> <span data-ttu-id="22b74-160">이 위해 열고는 **패키지 관리자 콘솔** 유형과 &quot; **Install-package MySql.Data.Entity 사전**&quot;, 한 다음 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-160">To do so, open the **Package Manager Console** and type &quot;**Install-Package MySql.Data.Entity -Pre**&quot;, and then press Enter.</span></span>

> [!NOTE]
> <span data-ttu-id="22b74-161">어셈블리의 시험판 버전 이며 따라서 버그를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-161">This is a pre-release version of the assembly, and as such it may contain bugs.</span></span> <span data-ttu-id="22b74-162">하지 프로덕션 환경에서 시험판 버전의 공급자를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-162">You should not use a pre-release version of the provider in production.</span></span>


<span data-ttu-id="22b74-163">[다음 그림을 확장 하려면 클릭 합니다.]</span><span class="sxs-lookup"><span data-stu-id="22b74-163">[Click the following image to expand it.]</span></span>  
  
[![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image22.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image21.png)

### <a name="making-project-configuration-changes-to-the-webconfig-file-for-your-application"></a><span data-ttu-id="22b74-164">프로젝트 구성을 변경 응용 프로그램에 대 한 Web.config 파일</span><span class="sxs-lookup"><span data-stu-id="22b74-164">Making project configuration changes to the Web.config file for your application</span></span>

<span data-ttu-id="22b74-165">방금 설치한 MySQL 공급자를 사용 하려면 Entity Framework를 구성 하는이 섹션에서는 MySQL 공급자 팩터리를 등록 하 고 Azure에서 연결 문자열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-165">In this section you will configure the Entity Framework to use the MySQL provider that you just installed, register the MySQL provider factory, and add your connection string from Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="22b74-166">다음 예에서는 MySql.Data.dll에 대 한 특정 어셈블리 버전을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-166">The following examples contain a specific assembly version for MySql.Data.dll.</span></span> <span data-ttu-id="22b74-167">어셈블리 버전 변경 되는 경우에 올바른 버전으로 적절 한 구성 설정을 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-167">If the assembly version changes, you will need to modify the appropriate configuration settings with the correct version.</span></span>


1. <span data-ttu-id="22b74-168">Visual Studio 2013에서 프로젝트에 대 한 Web.config 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-168">Open the Web.config file for your project in Visual Studio 2013.</span></span>
2. <span data-ttu-id="22b74-169">Entity Framework에 대 한 기본 데이터베이스 공급자 및 팩터리를 정의 하는 다음 구성 설정을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-169">Locate the following configuration settings, which define the default database provider and factory for the Entity Framework:</span></span>

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample1.xml)]
3. <span data-ttu-id="22b74-170">이러한 구성 설정을 MySQL 공급자를 사용 하려면 Entity Framework 구성에서 다음을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-170">Replace those configuration settings with the following, which will configure the Entity Framework to use the MySQL provider:</span></span> 

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample2.xml)]
4. <span data-ttu-id="22b74-171">찾을 &lt;connectionStrings&gt; 섹션 및 Azure에서 호스팅하는 MySQL 데이터베이스에 대 한 연결 문자열을 정의 합니다를 다음 코드로 바꿉니다 (providerName 값에서 변경도 원본):</span><span class="sxs-lookup"><span data-stu-id="22b74-171">Locate the &lt;connectionStrings&gt; section and replace it with the following code, which will define the connection string for your MySQL database that is hosted on Azure (note that providerName value has also been changed from the original):</span></span>

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample3.xml?highlight=3-4)]

### <a name="adding-custom-migrationhistory-context"></a><span data-ttu-id="22b74-172">사용자 지정 MigrationHistory 컨텍스트 추가</span><span class="sxs-lookup"><span data-stu-id="22b74-172">Adding custom MigrationHistory context</span></span>

<span data-ttu-id="22b74-173">사용 하 여 entity Framework Code First는 **MigrationHistory** 테이블 모델 변경 내용을 추적 하 고 데이터베이스 스키마 및 개념 스키마 간의 일관성을 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-173">Entity Framework Code First uses a **MigrationHistory** table to keep track of model changes and to ensure the consistency between the database schema and conceptual schema.</span></span> <span data-ttu-id="22b74-174">그러나이 테이블 작동 하지 않습니다 MySQL 용 기본적으로 기본 키가 너무 커서.</span><span class="sxs-lookup"><span data-stu-id="22b74-174">However, this table does not work for MySQL by default because the primary key is too large.</span></span> <span data-ttu-id="22b74-175">이 문제를 해결 하려면 해당 테이블에 대 한 키 크기를 축소 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-175">To remedy this situation, you will need to shrink the key size for that table.</span></span> <span data-ttu-id="22b74-176">이렇게 하려면 다음 단계를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-176">To do so, use the following steps:</span></span>

1. <span data-ttu-id="22b74-177">이 테이블에 대 한 스키마 정보에서 캡처되는 **HistoryContext**, 모든 다른 수정할 수 있는 **DbContext**합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-177">The schema information for this table is captured in a **HistoryContext**, which can be modified as any other **DbContext**.</span></span> <span data-ttu-id="22b74-178">이렇게 하려면 라는 새 클래스 파일 추가 **MySqlHistoryContext.cs** 을 프로젝트에 해당 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-178">To do so, add a new class file named **MySqlHistoryContext.cs** to the project, and replace its contents with the following code:</span></span>

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample4.cs)]
2. <span data-ttu-id="22b74-179">그런 다음 수정 된 사용 하려면 Entity Framework를 구성 해야 합니다 **HistoryContext**, 기본 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-179">Next you will need to configure Entity Framework to use the modified **HistoryContext**, rather than default one.</span></span> <span data-ttu-id="22b74-180">코드 기반 구성 기능을 활용 하 여이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-180">This can be done by leveraging code-based configuration features.</span></span> <span data-ttu-id="22b74-181">이렇게 하려면 라는 새 클래스 파일 추가 **MySqlConfiguration.cs** 프로젝트 및 그 내용을 바꾸기:</span><span class="sxs-lookup"><span data-stu-id="22b74-181">To do so, add new class file named **MySqlConfiguration.cs** to your project and replace its contents with:</span></span>

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample5.cs)]

### <a name="creating-a-custom-entityframework-initializer-for-applicationdbcontext"></a><span data-ttu-id="22b74-182">ApplicationDbContext에 대 한 사용자 지정 EntityFramework 이니셜라이저 만들기</span><span class="sxs-lookup"><span data-stu-id="22b74-182">Creating a custom EntityFramework initializer for ApplicationDbContext</span></span>

<span data-ttu-id="22b74-183">데이터베이스에 연결 하기 위해 모델 이니셜라이저를 사용 해야이 자습서에서는 추천 목록에 MySQL 공급자 Entity Framework 마이그레이션의 현재 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-183">The MySQL provider that is featured in this tutorial does not currently support Entity Framework migrations, so you will need to use model initializers in order to connect to the database.</span></span> <span data-ttu-id="22b74-184">이 자습서에서는 Azure에서 MySQL 인스턴스를 사용 하는, 때문에 사용자 지정 Entity Framework 이니셜라이저 만들 해야 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-184">Because this tutorial is using a MySQL instance on Azure, you will need need to create a custom Entity Framework initializer.</span></span>

> [!NOTE]
> <span data-ttu-id="22b74-185">Azure 또는 온-프레미스에서 호스트 된 데이터베이스를 사용 하는 경우에 SQL Server 인스턴스에 연결 하는 경우에이 단계가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-185">This step is not required if you are connecting to a SQL Server instance on Azure or if you are using a database that is hosted on premises.</span></span>


<span data-ttu-id="22b74-186">MySQL에 대 한 사용자 지정 Entity Framework 이니셜라이저를 만들려면 다음 단계를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-186">To create a custom Entity Framework initializer for MySQL, use the following steps:</span></span>

1. <span data-ttu-id="22b74-187">라는 새 클래스 파일 추가 **MySqlInitializer.cs** 프로젝트 및 바꾸기를 다음 코드를 사용 하 여 콘텐츠:</span><span class="sxs-lookup"><span data-stu-id="22b74-187">Add a new class file named **MySqlInitializer.cs** to the project, and replace it's contents with the following code:</span></span> 

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample6.cs?highlight=23)]
2. <span data-ttu-id="22b74-188">열기는 **IdentityModels.cs** 파일에 있는 프로젝트에 대해는 **모델** 디렉터리의 내용을 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-188">Open the **IdentityModels.cs** file for your project, which is located in the **Models** directory, and replace it's contents with the following:</span></span> 

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample7.cs)]

## <a name="running-the-application-and-verifying-the-database"></a><span data-ttu-id="22b74-189">응용 프로그램을 실행 하 고 데이터베이스를 확인 하는 중</span><span class="sxs-lookup"><span data-stu-id="22b74-189">Running the application and verifying the database</span></span>

<span data-ttu-id="22b74-190">이전 섹션의 단계를 완료 후 데이터베이스를 테스트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-190">Once you have completed the steps in the preceding sections, you should test your database.</span></span> <span data-ttu-id="22b74-191">이렇게 하려면 다음 단계를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-191">To do so, use the following steps:</span></span>

1. <span data-ttu-id="22b74-192">키를 눌러 **Ctrl + f 5를 눌러** 작성 하 고 웹 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-192">Press **Ctrl + F5** to build and run the web application.</span></span>
2. <span data-ttu-id="22b74-193">클릭는 **등록** 페이지 위쪽의 탭:</span><span class="sxs-lookup"><span data-stu-id="22b74-193">Click the **Register** tab on the top of the page:</span></span>  
  
 <span data-ttu-id="22b74-194">[확장 하려면 다음 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-194">[Click the following image to expand it.</span></span> <span data-ttu-id="22b74-195">]</span><span class="sxs-lookup"><span data-stu-id="22b74-195">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image4.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image3.jpg)
3. <span data-ttu-id="22b74-196">새 사용자 이름 및 암호를 입력 한 다음 클릭 **등록**:</span><span class="sxs-lookup"><span data-stu-id="22b74-196">Enter a new user name and password, and then click **Register**:</span></span>  
  
 <span data-ttu-id="22b74-197">[확장 하려면 다음 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-197">[Click the following image to expand it.</span></span> <span data-ttu-id="22b74-198">]</span><span class="sxs-lookup"><span data-stu-id="22b74-198">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image24.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image23.png)
4. <span data-ttu-id="22b74-199">이 시점에서 ASP.NET Identity 테이블은에서 MySQL 데이터베이스 만들어지고 사용자가 등록 하 고 응용 프로그램에 로그인:</span><span class="sxs-lookup"><span data-stu-id="22b74-199">At this point the ASP.NET Identity tables are created on the MySQL Database, and the user is registered and logged into the application:</span></span>  
  
 <span data-ttu-id="22b74-200">[확장 하려면 다음 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-200">[Click the following image to expand it.</span></span> <span data-ttu-id="22b74-201">]</span><span class="sxs-lookup"><span data-stu-id="22b74-201">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image6.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image5.jpg)

### <a name="installing-mysql-workbench-tool-to-verify-the-data"></a><span data-ttu-id="22b74-202">데이터를 확인 하려면 MySQL 워크 벤치 도구 설치</span><span class="sxs-lookup"><span data-stu-id="22b74-202">Installing MySQL Workbench tool to verify the data</span></span>

1. <span data-ttu-id="22b74-203">설치는 **MySQL 워크 벤치** 에서 도구는 [MySQL 다운로드 페이지](http://dev.mysql.com/downloads/windows/installer/)</span><span class="sxs-lookup"><span data-stu-id="22b74-203">Install the **MySQL Workbench** tool from the [MySQL downloads page](http://dev.mysql.com/downloads/windows/installer/)</span></span>
2. <span data-ttu-id="22b74-204">설치 마법사에서: **기능 선택** 탭에서 **MySQL 워크 벤치** 아래 **응용 프로그램** 섹션.</span><span class="sxs-lookup"><span data-stu-id="22b74-204">In the installation wizard: **Feature Selection** tab, select **MySQL Workbench** under **applications** section.</span></span>
3. <span data-ttu-id="22b74-205">응용 프로그램을 실행 하 고이 자습서의 말아달라 때 만든 Azure의 MySQL 데이터베이스의 연결 문자열 데이터를 사용 하 여 새 연결을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-205">Launch the app and add a new connection using the connection string data from the Azure MySQL database you created at the begging of this tutorial.</span></span>
4. <span data-ttu-id="22b74-206">연결을 만든 후 검사는 **ASP.NET Identity** 에 생성 된 테이블은 **IdentityMySQLDatabase 합니다.**</span><span class="sxs-lookup"><span data-stu-id="22b74-206">After establishing the connection, inspect the **ASP.NET Identity** tables created on the **IdentityMySQLDatabase.**</span></span>
5. <span data-ttu-id="22b74-207">모든 ASP.NET Identity 필요한 아래 이미지에 표시 된 대로 테이블을 만들 수 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-207">You will see that all ASP.NET Identity required tables are created as shown in the image below:</span></span>  
  
 <span data-ttu-id="22b74-208">[확장 하려면 다음 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-208">[Click the following image to expand it.</span></span> <span data-ttu-id="22b74-209">]</span><span class="sxs-lookup"><span data-stu-id="22b74-209">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image8.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image7.jpg)
6. <span data-ttu-id="22b74-210">검사는 **aspnetusers** 테이블 예를 들어 새 사용자를 등록할 때 항목을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-210">Inspect the **aspnetusers** table for instance to check for the entries as you register new users.</span></span>  
  
 <span data-ttu-id="22b74-211">[확장 하려면 다음 이미지를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b74-211">[Click the following image to expand it.</span></span> <span data-ttu-id="22b74-212">]</span><span class="sxs-lookup"><span data-stu-id="22b74-212">]</span></span>  
    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image26.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image25.png)
