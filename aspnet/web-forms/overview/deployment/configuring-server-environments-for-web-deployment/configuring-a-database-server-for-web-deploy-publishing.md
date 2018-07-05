---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing
title: 배포 게시용 웹에 대 한 데이터베이스 서버 구성 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 웹 배포 및 게시를 지원 하도록 SQL Server 2008 R2 데이터베이스 서버를 구성 하는 방법을 설명 합니다. 이 항목에 설명 된 작업은 공동...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: e7c447f9-eddf-4bbe-9f18-3326d965d093
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing
msc.type: authoredcontent
ms.openlocfilehash: 5563b737e3fd200070951f8d281ed8015137ae35
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37384461"
---
<a name="configuring-a-database-server-for-web-deploy-publishing"></a><span data-ttu-id="36d59-104">웹 배포 게시용 데이터베이스 서버 구성</span><span class="sxs-lookup"><span data-stu-id="36d59-104">Configuring a Database Server for Web Deploy Publishing</span></span>
====================
<span data-ttu-id="36d59-105">[Jason lee 공저](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="36d59-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="36d59-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="36d59-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="36d59-107">이 항목에서는 웹 배포 및 게시를 지원 하도록 SQL Server 2008 R2 데이터베이스 서버를 구성 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-107">This topic describes how to configure a SQL Server 2008 R2 database server to support web deployment and publishing.</span></span>
> 
> <span data-ttu-id="36d59-108">이 항목에 설명 된 작업은 모든 배포 시나리오에 공통적으로 적용&#x2014;웹 서버는 IIS 웹 배포 도구 (웹 배포) 원격 에이전트 서비스, 웹 배포 처리기 또는 오프 라인 배포를 사용 하도록 구성 된 여부와 상관 또는 응용 프로그램은 단일 웹 서버 또는 서버 팜의에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-108">The tasks described in this topic are common to every deployment scenario&#x2014;it doesn't matter whether your web servers are configured to use the IIS Web Deployment Tool (Web Deploy) Remote Agent Service, the Web Deploy Handler, or offline deployment or your application is running on a single web server or a server farm.</span></span> <span data-ttu-id="36d59-109">데이터베이스를 배포 하는 방법은 보안 요구 사항 및 기타 고려 사항에 따라 변경 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-109">The way you deploy the database may change according to security requirements and other considerations.</span></span> <span data-ttu-id="36d59-110">예를 들어, 샘플 데이터 없이 데이터베이스를 배포할 수 있습니다 및 사용자 역할 매핑을 배포 또는 배포 후 수동으로 구성 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-110">For example, you might deploy the database with or without sample data, and you might deploy user role mappings or configure them manually after deployment.</span></span> <span data-ttu-id="36d59-111">그러나 데이터베이스 서버를 구성 하는 방법은 동일 하 게 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-111">However, the way you configure the database server remains the same.</span></span>


<span data-ttu-id="36d59-112">웹 배포를 지원 하도록 데이터베이스 서버를 구성 하는 데 추가 제품 또는 도구를 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-112">You don't have to install any additional products or tools to configuring a database server to support web deployment.</span></span> <span data-ttu-id="36d59-113">데이터베이스 서버 및 웹 서버를 서로 다른 컴퓨터에서 실행을 만든다고 가정 하면:</span><span class="sxs-lookup"><span data-stu-id="36d59-113">Assuming that your database server and your web server run on different machines, you simply need to:</span></span>

- <span data-ttu-id="36d59-114">SQL Server TCP/IP를 사용 하 여 통신을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-114">Permit SQL Server to communicate using TCP/IP.</span></span>
- <span data-ttu-id="36d59-115">방화벽을 통해 SQL Server 트래픽을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-115">Allow SQL Server traffic through any firewalls.</span></span>
- <span data-ttu-id="36d59-116">웹 서버 컴퓨터 계정을 SQL Server 로그인을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-116">Give the web server machine account a SQL Server login.</span></span>
- <span data-ttu-id="36d59-117">필요한 데이터베이스 역할에 컴퓨터 계정 로그인을 매핑하십시오.</span><span class="sxs-lookup"><span data-stu-id="36d59-117">Map the machine account login to any required database roles.</span></span>
- <span data-ttu-id="36d59-118">배포는 SQL Server 로그인 및 데이터베이스 작성자 권한이 실행 계정에 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-118">Give the account that will run the deployment a SQL Server login and database creator permissions.</span></span>
- <span data-ttu-id="36d59-119">반복 배포를 지원 하려면 배포 계정 로그인을 매핑하는 **db\_소유자** 데이터베이스 역할.</span><span class="sxs-lookup"><span data-stu-id="36d59-119">To support repeat deployments, map the deployment account login to the **db\_owner** database role.</span></span>

<span data-ttu-id="36d59-120">이 항목에서는 이러한 각 절차를 수행 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-120">This topic will show you how to perform each of these procedures.</span></span> <span data-ttu-id="36d59-121">작업은이 항목의 연습에서는 Windows Server 2008 R2를 실행 하는 SQL Server 2008 R2의 기본 인스턴스를 사용 하 여 시작 하 고 있음을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-121">The tasks and walkthroughs in this topic assume that you're starting with a default instance of SQL Server 2008 R2 running on Windows Server 2008 R2.</span></span> <span data-ttu-id="36d59-122">계속 하기 전에 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-122">Before you continue, ensure that:</span></span>

- <span data-ttu-id="36d59-123">Windows Server 2008 R2 서비스 팩 1 및 모든 사용 가능한 업데이트가 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-123">Windows Server 2008 R2 Service Pack 1 and all available updates are installed.</span></span>
- <span data-ttu-id="36d59-124">서버가는 도메인에 가입 된입니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-124">The server is domain-joined.</span></span>
- <span data-ttu-id="36d59-125">서버에 고정 IP가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-125">The server has a static IP address.</span></span>
- <span data-ttu-id="36d59-126">SQL Server 2008 R2 서비스 팩 1 및 모든 사용 가능한 업데이트가 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-126">SQL Server 2008 R2 Service Pack 1 and all available updates are installed.</span></span>

<span data-ttu-id="36d59-127">SQL Server 인스턴스는만 포함 해야 합니다 **데이터베이스 엔진 서비스** 역할을 모든 SQL Server 설치에 자동으로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-127">The SQL Server instance only needs to include the **Database Engine Services** role, which is included automatically in any SQL Server installation.</span></span> <span data-ttu-id="36d59-128">단, 구성 및 유지 관리 편의성을 위해 권장 하는 합니다 **관리 도구-기본** 하 고 **관리 도구-전체** 서버 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-128">However, for ease of configuration and maintenance, we recommend that you include the **Management Tools – Basic** and **Management Tools – Complete** server roles.</span></span>

> [!NOTE]
> <span data-ttu-id="36d59-129">참조 컴퓨터를 도메인에 가입 하는 방법은 [도메인 및 로그온에 컴퓨터 가입](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-129">For more information on joining computers to a domain, see [Joining Computers to the Domain and Logging On](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx).</span></span> <span data-ttu-id="36d59-130">고정 IP 주소를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [정적 IP 주소를 구성](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-130">For more information on configuring static IP addresses, see [Configure a Static IP Address](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).</span></span> <span data-ttu-id="36d59-131">SQL Server 설치에 대 한 자세한 내용은 참조 하세요. [SQL Server 2008 R2 설치](https://technet.microsoft.com/library/bb500395.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-131">For more information on installing SQL Server, see [Installing SQL Server 2008 R2](https://technet.microsoft.com/library/bb500395.aspx).</span></span>


## <a name="enable-remote-access-to-sql-server"></a><span data-ttu-id="36d59-132">SQL Server에 대 한 원격 액세스를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="36d59-132">Enable Remote Access to SQL Server</span></span>

<span data-ttu-id="36d59-133">SQL Server TCP/IP를 사용 하 여 원격 컴퓨터와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-133">SQL Server uses TCP/IP to communicate with remote computers.</span></span> <span data-ttu-id="36d59-134">데이터베이스 서버 및 웹 서버는 서로 다른 컴퓨터에 있는 경우에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-134">If your database server and your web server are on different machines, you need to:</span></span>

- <span data-ttu-id="36d59-135">SQL Server TCP/IP를 통한 통신을 허용 하도록 네트워킹 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-135">Configure SQL Server networking settings to allow communication over TCP/IP.</span></span>
- <span data-ttu-id="36d59-136">TCP 트래픽을 허용 (및 사용자 데이터 그램 프로토콜 (UDP)의 경우 일부 트래픽)에 SQL Server 인스턴스를 사용 하는 포트에서 모든 하드웨어 또는 소프트웨어 방화벽을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-136">Configure any hardware or software firewalls to allow TCP traffic (and in some cases User Datagram Protocol (UDP) traffic) on the ports that the SQL Server instance uses.</span></span>

<span data-ttu-id="36d59-137">TCP/IP를 통해 통신 하는 SQL Server를 사용 하도록 설정 하려면 SQL Server 인스턴스에 대 한 네트워크 구성을 변경 하려면 SQL Server 구성 관리자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-137">To enable SQL Server to communicate over TCP/IP, use SQL Server Configuration Manager to change the network configuration for your SQL Server instance.</span></span>

<span data-ttu-id="36d59-138">**TCP/IP를 사용 하 여 통신 하도록 SQL Server를 사용 하도록 설정 하려면**</span><span class="sxs-lookup"><span data-stu-id="36d59-138">**To enable SQL Server to communicate using TCP/IP**</span></span>

1. <span data-ttu-id="36d59-139">에 **시작** 메뉴에서 **프로그램도**, 클릭 **Microsoft SQL Server 2008 R2**, 클릭 **구성 도구**, 클릭 하 고 **SQL Server 구성 관리자**합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-139">On the **Start** menu, point to **All Programs**, click **Microsoft SQL Server 2008 R2**, click **Configuration Tools**, and then click **SQL Server Configuration Manager**.</span></span>
2. <span data-ttu-id="36d59-140">트리 뷰 창에서 확장 **SQL Server 네트워크 구성**를 클릭 하 고 **MSSQLSERVER 용 프로토콜**합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-140">In the tree view pane, expand **SQL Server Network Configuration**, and then click **Protocols for MSSQLSERVER**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="36d59-141">SQL Server의 여러 인스턴스를 설치한 경우 표시 됩니다는 <strong>에 대 한 프로토콜</strong><em>[인스턴스 이름]</em> 각 인스턴스에 대 한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-141">If you have installed multiple instances of SQL Server, you'll see a <strong>Protocols for</strong><em>[instance name]</em> item for each instance.</span></span> <span data-ttu-id="36d59-142">인스턴스에 의해 단위로 네트워크 설정을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-142">You need to configure network settings on an instance-by-instance basis.</span></span>
3. <span data-ttu-id="36d59-143">세부 정보 창에서 마우스 오른쪽 단추로 클릭 합니다 **TCP/IP** 행을 클릭 하 고 **사용**합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-143">In the details pane, right-click the **TCP/IP** row, and then click **Enable**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image1.png)
4. <span data-ttu-id="36d59-144">에 **경고** 대화 상자, 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-144">In the **Warning** dialog box, click **OK**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image2.png)
5. <span data-ttu-id="36d59-145">새로운 네트워크 구성을 적용 하려면 MSSQLSERVER 서비스를 다시 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-145">You need to restart the MSSQLSERVER service before your new network configuration will take effect.</span></span> <span data-ttu-id="36d59-146">서비스 콘솔에서 또는 SQL Server Management Studio에서 명령 프롬프트에서 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-146">You can do that at a command prompt, from the Services console, or from SQL Server Management Studio.</span></span> <span data-ttu-id="36d59-147">이 절차에서는 SQL Server Management Studio를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-147">In this procedure, you'll use SQL Server Management Studio.</span></span>
6. <span data-ttu-id="36d59-148">SQL Server 구성 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-148">Close SQL Server Configuration Manager.</span></span>
7. <span data-ttu-id="36d59-149">에 **시작** 메뉴에서 **모든 프로그램**, 클릭 **Microsoft SQL Server 2008 R2**를 클릭 하 고 **SQL Server Management Studio**합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-149">On the **Start** menu, point to **All Programs**, click **Microsoft SQL Server 2008 R2**, and then click **SQL Server Management Studio**.</span></span>
8. <span data-ttu-id="36d59-150">에 **서버에 연결** 대화 상자의 합니다 **서버 이름** 상자, 데이터베이스 서버의 이름을 입력 한 다음 클릭 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-150">In the **Connect to Server** dialog box, in the **Server name** box, type the name of the database server, and then click **Connect**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image3.png)
9. <span data-ttu-id="36d59-151">에 **개체 탐색기** 창 상위 서버 노드를 마우스 오른쪽 단추로 클릭 (예를 들어 **TESTDB1**)를 클릭 하 고 **다시 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-151">In the **Object Explorer** pane, right-click the parent server node (for example, **TESTDB1**), and then click **Restart**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image4.png)
10. <span data-ttu-id="36d59-152">에 **Microsoft SQL Server Management Studio** 대화 상자, 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-152">In the **Microsoft SQL Server Management Studio** dialog box, click **Yes**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image5.png)
11. <span data-ttu-id="36d59-153">서비스 다시 시작 하는 경우 SQL Server Management Studio를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-153">When the service has restarted, close SQL Server Management Studio.</span></span>

<span data-ttu-id="36d59-154">방화벽을 통해 SQL Server 트래픽을 허용 하려면 먼저 SQL Server 인스턴스를 사용 하 여 포트를 알고 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-154">To allow SQL Server traffic through a firewall, you first need to know which ports your SQL Server instance is using.</span></span> <span data-ttu-id="36d59-155">이 SQL Server 인스턴스를 생성 하 고 구성 하는 방법에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-155">This will depend on how the SQL Server instance was created and configured:</span></span>

- <span data-ttu-id="36d59-156">A *기본 인스턴스* SQL server에 대 한 수신 (및 응답할) TCP 포트 1433에 대 한 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-156">A *default instance* of SQL Server listens for (and responds to) requests on TCP port 1433.</span></span>
- <span data-ttu-id="36d59-157">A *명명 된 인스턴스* SQL server에 대 한 수신 (및 응답할) 동적으로 할당 된 TCP 포트에서 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-157">A *named instance* of SQL Server listens for (and responds to) requests on a dynamically assigned TCP port.</span></span>
- <span data-ttu-id="36d59-158">SQL Server Browser 서비스를 사용 하는 경우 클라이언트는 UDP 포트 1434 특정 SQL Server 인스턴스에 대해 사용 하는 TCP 포트를 확인 하려면 서비스를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-158">If the SQL Server Browser service is enabled, clients can query the service on UDP port 1434 to find out which TCP port to use for a particular SQL Server instance.</span></span> <span data-ttu-id="36d59-159">그러나이 서비스는 종종 보안상의 이유로 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-159">However, this service is often disabled for security reasons.</span></span>

<span data-ttu-id="36d59-160">SQL Server의 기본 인스턴스를 사용 하는 가정 트래픽을 허용 하도록 방화벽을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-160">Assuming that you're using a default instance of SQL Server, you need to configure your firewall to allow traffic.</span></span>

| <span data-ttu-id="36d59-161">방향</span><span class="sxs-lookup"><span data-stu-id="36d59-161">Direction</span></span> | <span data-ttu-id="36d59-162">포트에서</span><span class="sxs-lookup"><span data-stu-id="36d59-162">From Port</span></span> | <span data-ttu-id="36d59-163">포트</span><span class="sxs-lookup"><span data-stu-id="36d59-163">To Port</span></span> | <span data-ttu-id="36d59-164">포트 유형</span><span class="sxs-lookup"><span data-stu-id="36d59-164">Port Type</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="36d59-165">인바운드</span><span class="sxs-lookup"><span data-stu-id="36d59-165">Inbound</span></span> | <span data-ttu-id="36d59-166">임의의 값</span><span class="sxs-lookup"><span data-stu-id="36d59-166">Any</span></span> | <span data-ttu-id="36d59-167">1433</span><span class="sxs-lookup"><span data-stu-id="36d59-167">1433</span></span> | <span data-ttu-id="36d59-168">TCP</span><span class="sxs-lookup"><span data-stu-id="36d59-168">TCP</span></span> |
| <span data-ttu-id="36d59-169">아웃 바운드</span><span class="sxs-lookup"><span data-stu-id="36d59-169">Outbound</span></span> | <span data-ttu-id="36d59-170">1433</span><span class="sxs-lookup"><span data-stu-id="36d59-170">1433</span></span> | <span data-ttu-id="36d59-171">임의의 값</span><span class="sxs-lookup"><span data-stu-id="36d59-171">Any</span></span> | <span data-ttu-id="36d59-172">TCP</span><span class="sxs-lookup"><span data-stu-id="36d59-172">TCP</span></span> |
  

> [!NOTE]
> <span data-ttu-id="36d59-173">기술적으로 클라이언트 컴퓨터를 임의로 할당 된 TCP 포트 1024-5000을 사용 하 여 SQL Server와 통신 하 고 방화벽 규칙을 적절 하 게 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-173">Technically, a client computer will use a randomly assigned TCP port between 1024 and 5000 to communicate with SQL Server, and you can restrict your firewall rules accordingly.</span></span> <span data-ttu-id="36d59-174">SQL Server 포트 및 방화벽에 대 한 자세한 내용은 참조 하세요. [to SQL 방화벽을 통해 통신 해야 하는 TCP/IP 포트 번호](https://go.microsoft.com/?linkid=9805125) 및 [방법: 특정 TCP 포트 (SQL Server 구성에서 수신 하도록 서버 구성 관리자)](https://msdn.microsoft.com/library/ms177440.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-174">For more information on SQL Server ports and firewalls, see [TCP/IP port numbers required to communicate to SQL over a firewall](https://go.microsoft.com/?linkid=9805125) and [How to: Configure a Server to Listen on a Specific TCP Port (SQL Server Configuration Manager)](https://msdn.microsoft.com/library/ms177440.aspx).</span></span>


<span data-ttu-id="36d59-175">대부분의 Windows Server 환경에서 데이터베이스 서버에서 Windows 방화벽을 구성 해야 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-175">In most Windows Server environments, you'll likely have to configure Windows Firewall on the database server.</span></span> <span data-ttu-id="36d59-176">기본적으로 Windows 방화벽 규칙을 구체적으로 금지 하지 않는 한 모든 아웃 바운드 트래픽을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-176">By default, Windows Firewall allows all outbound traffic unless a rule specifically prohibits it.</span></span> <span data-ttu-id="36d59-177">데이터베이스에 연결할 웹 서버를 사용 하려면 SQL Server 인스턴스를 사용 하는 포트 번호에 TCP 트래픽을 허용 하는 인바운드 규칙을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-177">To enable your web server to reach your database, you need to configure an inbound rule that allows TCP traffic on the port number that the SQL Server instance uses.</span></span> <span data-ttu-id="36d59-178">SQL Server의 기본 인스턴스를 사용 하는 경우에이 규칙을 구성 하려면 다음 절차를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-178">If you're using a default instance of SQL Server, you can use the next procedure to configure this rule.</span></span>

<span data-ttu-id="36d59-179">**기본 SQL Server 인스턴스를 사용 하 여 통신을 허용 하도록 Windows 방화벽을 구성 하려면**</span><span class="sxs-lookup"><span data-stu-id="36d59-179">**To configure Windows Firewall to allow communication with a default SQL Server instance**</span></span>

1. <span data-ttu-id="36d59-180">데이터베이스 서버의는 **시작** 메뉴에서 **관리 도구**를 클릭 하 고 **고급 보안이 포함 된 Windows 방화벽**합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-180">On the database server, on the **Start** menu, point to **Administrative Tools**, and then click **Windows Firewall with Advanced Security**.</span></span>
2. <span data-ttu-id="36d59-181">트리 뷰 창에서 클릭 **인바운드 규칙**합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-181">In the tree view pane, click **Inbound Rules**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image6.png)
3. <span data-ttu-id="36d59-182">에 **동작** 창 아래에 있는 **인바운드 규칙**, 클릭 **새 규칙**합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-182">In the **Actions** pane, under **Inbound Rules**, click **New Rule**.</span></span>
4. <span data-ttu-id="36d59-183">새 인바운드 규칙 마법사에서에 **규칙 유형** 페이지에서 **포트**를 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-183">In the New Inbound Rule Wizard, on the **Rule Type** page, select **Port**, and then click **Next**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image7.png)
5. <span data-ttu-id="36d59-184">에 **프로토콜 및 포트** 페이지에서 **TCP** 을 선택 하면 및를 **특정 로컬 포트** 상자에 입력 **1433**를 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-184">On the **Protocol and Ports** page, ensure that **TCP** is selected, and in the **Specific local ports** box, type **1433**, and then click **Next**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image8.png)
6. <span data-ttu-id="36d59-185">에 **동작** 페이지에서 **연결을 허용** 선택 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-185">On the **Action** page, leave **Allow the connection** selected and click **Next**.</span></span>
7. <span data-ttu-id="36d59-186">에 **프로필** 페이지에서 **도메인** 지우기 옵션을 선택 합니다 **개인** 및 **공용** 확인란을 선택한 다음 클릭  **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-186">On the **Profile** page, leave **Domain** selected, clear the **Private** and **Public** check boxes, and then click **Next**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image9.png)
8. <span data-ttu-id="36d59-187">에 **이름** 페이지에서 규칙 이름을 적절 하 게 설명 (예를 들어 **SQL Server 기본 인스턴스에 대 한 네트워크 액세스**)를 클릭 하 고 **마침**.</span><span class="sxs-lookup"><span data-stu-id="36d59-187">On the **Name** page, give the rule a suitably descriptive name (for example, **SQL Server default instance – network access**), and then click **Finish**.</span></span>

<span data-ttu-id="36d59-188">내용은 비표준 또는 동적 포트를 통해 SQL Server와 통신 해야 하는 경우에 특히 SQL Server에 대 한 Windows 방화벽을 구성 하는 방법은 [방법: 데이터베이스 엔진 액세스에 대 한 Windows 방화벽 구성](https://technet.microsoft.com/library/ms175043.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-188">For more information on configuring Windows Firewall for SQL Server, particularly if you need to communicate with SQL Server over non-standard or dynamic ports, see [How to: Configure a Windows Firewall for Database Engine Access](https://technet.microsoft.com/library/ms175043.aspx).</span></span>

## <a name="configure-logins-and-database-permissions"></a><span data-ttu-id="36d59-189">로그인을 구성 및 데이터베이스 권한</span><span class="sxs-lookup"><span data-stu-id="36d59-189">Configure Logins and Database Permissions</span></span>

<span data-ttu-id="36d59-190">인터넷 정보 서비스 (IIS) 웹 응용 프로그램을 배포할 때는 응용 프로그램 풀의 id를 사용 하 여 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-190">When you deploy a web application to Internet Information Services (IIS), the application runs using the identity of the application pool.</span></span> <span data-ttu-id="36d59-191">도메인 환경에서 응용 프로그램 풀 id에는 실행 네트워크 리소스에 액세스 하는 서버의 컴퓨터 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-191">In a domain environment, application pool identities use the machine account of the server on which they run to access network resources.</span></span> <span data-ttu-id="36d59-192">컴퓨터 계정 형태가 <em>[도메인 이름]</em><strong>\</s o n ><em>[컴퓨터 이름]</em><strong>$</strong>&#x2014;예를 들어, <strong>FABRIKAM\TESTWEB1$</strong>합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-192">Machine accounts take the form <em>[domain name]</em><strong>\</strong><em>[machine name]</em><strong>$</strong>&#x2014;for example, <strong>FABRIKAM\TESTWEB1$</strong>.</span></span> <span data-ttu-id="36d59-193">네트워크를 통해 데이터베이스에 액세스 하려면 웹 응용 프로그램에 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-193">To allow your web application to access a database across the network, you need to:</span></span>

- <span data-ttu-id="36d59-194">SQL Server 인스턴스를 웹 서버 컴퓨터 계정에 대 한 로그인을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-194">Add a login for the web server machine account to the SQL Server instance.</span></span>
- <span data-ttu-id="36d59-195">필요한 데이터베이스 역할에 컴퓨터 계정 로그인에 매핑합니다 (일반적으로 **db\_datareader** 하 고 **db\_datawriter**).</span><span class="sxs-lookup"><span data-stu-id="36d59-195">Map the machine account login to any required database roles (typically **db\_datareader** and **db\_datawriter**).</span></span>

<span data-ttu-id="36d59-196">웹 응용 프로그램은 단일 서버가 아닌 서버 팜에 실행 하는 경우에 서버 팜의 모든 웹 서버에 대해이 절차를 반복 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-196">If your web application is running on a server farm, rather than a single server, you'll need to repeat these procedures for every web server in the server farm.</span></span>

> [!NOTE]
> <span data-ttu-id="36d59-197">응용 프로그램 풀 id 및 네트워크 리소스에 액세스에 대 한 자세한 내용은 참조 하세요. [응용 프로그램 풀 Id](https://go.microsoft.com/?linkid=9805123)합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-197">For more information on application pool identities and accessing network resources, see [Application Pool Identities](https://go.microsoft.com/?linkid=9805123).</span></span>


<span data-ttu-id="36d59-198">다양 한 방법으로 이러한 작업을 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-198">You can approach these tasks in various ways.</span></span> <span data-ttu-id="36d59-199">로그인을 만들려면 다음 하거나 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-199">To create the login, you can either:</span></span>

- <span data-ttu-id="36d59-200">TRANSACT-SQL 또는 SQL Server Management Studio를 사용 하 여 데이터베이스 서버의 로그인을 수동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-200">Create the login manually on the database server, using Transact-SQL or SQL Server Management Studio.</span></span>
- <span data-ttu-id="36d59-201">Visual Studio에서 SQL Server 2008 서버 프로젝트를 사용 하 여 만들고 로그인을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-201">Use a SQL Server 2008 Server Project in Visual Studio to create and deploy the login.</span></span>

<span data-ttu-id="36d59-202">SQL Server 로그인 이므로 데이터베이스 수준 개체를 보다는 서버 수준 개체를 배포 하려는 데이터베이스에 종속 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-202">A SQL Server login is a server-level object, rather than a database-level object, so it's not dependent on the database you want to deploy.</span></span> <span data-ttu-id="36d59-203">이와 같이 언제 든 지 로그인을 만들 수 있습니다 및 가장 쉬운 방법은 데이터베이스를 배포 하기 전에 데이터베이스 서버의 로그인을 수동으로 만들 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-203">As such, you can create the login at any point, and the easiest approach is often to create the login manually on the database server before you start deploying databases.</span></span> <span data-ttu-id="36d59-204">SQL Server Management Studio에서 로그인을 만들려면 다음 절차를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-204">You can use the next procedure to create a login in SQL Server Management Studio.</span></span>

<span data-ttu-id="36d59-205">**웹 서버 컴퓨터 계정에 대 한 SQL Server 로그인을 만들려면**</span><span class="sxs-lookup"><span data-stu-id="36d59-205">**To create a SQL Server login for the web server machine account**</span></span>

1. <span data-ttu-id="36d59-206">데이터베이스 서버의는 **시작** 메뉴에서 **모든 프로그램**, 클릭 **Microsoft SQL Server 2008 R2**를 클릭 하 고 **SQL Server Management Studio** .</span><span class="sxs-lookup"><span data-stu-id="36d59-206">On the database server, on the **Start** menu, point to **All Programs**, click **Microsoft SQL Server 2008 R2**, and then click **SQL Server Management Studio**.</span></span>
2. <span data-ttu-id="36d59-207">에 **서버에 연결** 대화 상자의 합니다 **서버 이름** 상자, 데이터베이스 서버의 이름을 입력 한 다음 클릭 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-207">In the **Connect to Server** dialog box, in the **Server name** box, type the name of the database server, and then click **Connect**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image10.png)
3. <span data-ttu-id="36d59-208">에 **개체 탐색기** 창 마우스 오른쪽 단추로 클릭 **보안**를 가리킨 **새로 만들기**, 클릭 하 고 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-208">In the **Object Explorer** pane, right-click **Security**, point to **New**, and then click **Login**.</span></span>
4. <span data-ttu-id="36d59-209">에 **로그인 – 새로 만들기** 대화 상자의 합니다 **로그인 이름** 상자에 웹 서버 컴퓨터 계정의 이름을 입력 (예를 들어 **FABRIKAM\TESTWEB1$**).</span><span class="sxs-lookup"><span data-stu-id="36d59-209">In the **Login – New** dialog box, in the **Login name** box, type the name of your web server machine account (for example, **FABRIKAM\TESTWEB1$**).</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image11.png)
5. <span data-ttu-id="36d59-210">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-210">Click **OK**.</span></span>

<span data-ttu-id="36d59-211">이 시점에서 데이터베이스 서버는 웹 배포 게시를 위해 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-211">At this point, your database server is ready for Web Deploy publishing.</span></span> <span data-ttu-id="36d59-212">그러나 배포 하는 모든 솔루션에 필요한 데이터베이스 역할에 컴퓨터 계정 로그인을 매핑할 때까지 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-212">However, any solutions you deploy won't work until you map the machine account login to the required database roles.</span></span> <span data-ttu-id="36d59-213">생각 보다 많이 필요한 데이터베이스 역할에 로그인 매핑, 것 없습니다 후 될 때까지 지도 역할 배포한 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-213">Mapping the login to database roles requires a lot more thought, as you can't map roles until after you've deployed the database.</span></span> <span data-ttu-id="36d59-214">컴퓨터 계정 로그인에 필요한 데이터베이스 역할을 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-214">To map the machine account login to the required database roles, you can either:</span></span>

- <span data-ttu-id="36d59-215">처음으로 데이터베이스를 배포한 후 로그인에 데이터베이스 역할을 수동으로 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-215">Assign the database roles to the login manually, after you've deployed the database for the first time.</span></span>
- <span data-ttu-id="36d59-216">배포 후 스크립트를 사용 하 여 로그인에 데이터베이스 역할을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-216">Use a post-deployment script to assign the database roles to the login.</span></span>

<span data-ttu-id="36d59-217">로그인 및 데이터베이스 역할 매핑을 만들기를 자동화 하는 방법은 참조 하세요 [배포 데이터베이스 역할 멤버 자격 테스트 환경에](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-217">For more information on automating the creation of logins and database role mappings, see [Deploying Database Role Memberships to Test Environments](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md).</span></span> <span data-ttu-id="36d59-218">또는 필요한 데이터베이스 역할에 컴퓨터 계정 로그인을 수동으로 매핑할 다음 절차를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-218">Alternatively, you can use the next procedure to map the machine account login to the required database roles manually.</span></span> <span data-ttu-id="36d59-219">될 때까지이 절차를 수행할 수 없다는 기억 *후* 데이터베이스를 배포 했습니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-219">Remember that you can't perform this procedure until *after* you've deployed the database.</span></span>

<span data-ttu-id="36d59-220">**데이터베이스 역할은 웹 서버 컴퓨터 계정 로그인에 매핑할**</span><span class="sxs-lookup"><span data-stu-id="36d59-220">**To map database roles to the web server machine account login**</span></span>

1. <span data-ttu-id="36d59-221">이전 처럼 SQL Server Management Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-221">Open SQL Server Management Studio as before.</span></span>
2. <span data-ttu-id="36d59-222">에 **개체 탐색기** 창 확장를 **보안** 노드를 확장 합니다 **로그인** 노드를 컴퓨터 계정 로그인을 두 번 클릭 하 고 (예를 들어  **FABRIKAM\TESTWEB1$**).</span><span class="sxs-lookup"><span data-stu-id="36d59-222">In the **Object Explorer** pane, expand the **Security** node, expand the **Logins** node, and then double-click the machine account login (for example, **FABRIKAM\TESTWEB1$**).</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image12.png)
3. <span data-ttu-id="36d59-223">에 **로그인 속성** 대화 상자, 클릭 **사용자 매핑**합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-223">In the **Login Properties** dialog box, click **User Mapping**.</span></span>
4. <span data-ttu-id="36d59-224">에 **이 로그인으로 매핑된 사용자** 테이블에서 데이터베이스의 이름을 선택 (예를 들어 **ContactManager**).</span><span class="sxs-lookup"><span data-stu-id="36d59-224">In the **Users mapped to this login** table, select the name of your database (for example, **ContactManager**).</span></span>
5. <span data-ttu-id="36d59-225">에 **데이터베이스 역할 멤버 자격:** *[데이터베이스 이름]* 목록에서 필요한 권한을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-225">In the **Database role membership for:** *[database name]* list, select the permissions required.</span></span> <span data-ttu-id="36d59-226">Contact Manager 샘플 솔루션의 경우 선택 해야 합니다 **db\_datareader** 및 **db\_datawriter** 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-226">In the case of the Contact Manager sample solution, you must select the **db\_datareader** and **db\_datawriter** roles.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image13.png)
6. <span data-ttu-id="36d59-227">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-227">Click **OK**.</span></span>

<span data-ttu-id="36d59-228">데이터베이스 역할을 수동으로 매핑 테스트 환경에 더욱 적합 한 경우가 것 스테이징 또는 프로덕션 환경에 자동화 된 또는 한 번 클릭 배포를 위해 그다지 바람직하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-228">While manually mapping database roles is often more than adequate for test environments, it's less desirable for automated or one-click deployments to staging or production environments.</span></span> <span data-ttu-id="36d59-229">이러한 종류의 배포 후 스크립트를 사용 하 여 태스크의 자동화에 대 한 자세한 정보를 찾을 수 있습니다 [배포 데이터베이스 역할 멤버 자격 테스트 환경에](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-229">You can find more information on automating this kind of task using post-deployment scripts in [Deploying Database Role Memberships to Test Environments](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md).</span></span>

> [!NOTE]
> <span data-ttu-id="36d59-230">서버 프로젝트와 데이터베이스 프로젝트에 대 한 자세한 내용은 참조 하세요. [Visual Studio 2010 SQL Server 데이터베이스 프로젝트](https://msdn.microsoft.com/library/ff678491.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-230">For more information on server projects and database projects, see [Visual Studio 2010 SQL Server Database Projects](https://msdn.microsoft.com/library/ff678491.aspx).</span></span>


## <a name="configure-permissions-for-the-deployment-account"></a><span data-ttu-id="36d59-231">배포 계정에 대 한 사용 권한 구성</span><span class="sxs-lookup"><span data-stu-id="36d59-231">Configure Permissions for the Deployment Account</span></span>

<span data-ttu-id="36d59-232">배포를 실행 하려면 사용 하는 계정이 SQL 서버 관리자가 아닌 경우에이 계정에 대 한 로그인을 만드는 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-232">If the account that you'll use to run the deployment is not a SQL Server administrator, you'll also need to create a login for this account.</span></span> <span data-ttu-id="36d59-233">데이터베이스를 만들기 위해 계정은의 구성원 이어야 합니다는 **dbcreator** 서버 역할 이거나 해당 권한을 가져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-233">In order to create the database, the account must be a member of the **dbcreator** server role or have equivalent permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="36d59-234">웹 배포 또는 VSDBCMD를 사용 하 여 데이터베이스를 배포 하는 경우 (SQL Server 인스턴스 혼합된 모드 인증을 지원 하도록 구성 됨) 하는 경우 Windows 자격 증명 또는 SQL Server 자격 증명을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-234">When you use Web Deploy or VSDBCMD to deploy a database, you can use Windows credentials or SQL Server credentials (if your SQL Server instance is configured to support mixed mode authentication).</span></span> <span data-ttu-id="36d59-235">다음 절차는 Windows 자격 증명을 사용 하려고 하지만에서 배포를 구성한 경우 연결 문자열에 SQL Server 사용자 이름 및 암호를 지정 하면 중지 하는 항목이 없는 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-235">The next procedure assumes that you want to use Windows credentials, but there's nothing stopping you from specifying a SQL Server user name and password in your connection string when you configure the deployment.</span></span>


<span data-ttu-id="36d59-236">**배포 계정에 대 한 사용 권한을 설정 하려면**</span><span class="sxs-lookup"><span data-stu-id="36d59-236">**To set up permissions for the deployment account**</span></span>

1. <span data-ttu-id="36d59-237">이전 처럼 SQL Server Management Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-237">Open SQL Server Management Studio as before.</span></span>
2. <span data-ttu-id="36d59-238">에 **개체 탐색기** 창 마우스 오른쪽 단추로 클릭 **보안**를 가리킨 **새로 만들기**, 클릭 하 고 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-238">In the **Object Explorer** pane, right-click **Security**, point to **New**, and then click **Login**.</span></span>
3. <span data-ttu-id="36d59-239">에 **로그인 – 새로 만들기** 대화 상자의 합니다 **로그인 이름** 상자 배포 계정의 이름을 입력 합니다 (예를 들어 **FABRIKAM\matt**).</span><span class="sxs-lookup"><span data-stu-id="36d59-239">In the **Login – New** dialog box, in the **Login name** box, type the name of your deployment account (for example, **FABRIKAM\matt**).</span></span>
4. <span data-ttu-id="36d59-240">에 **페이지 선택** 창 클릭 **서버 역할**입니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-240">In the **Select a page** pane, click **Server Roles**.</span></span>
5. <span data-ttu-id="36d59-241">선택 **dbcreator**를 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-241">Select **dbcreator**, and then click **OK**.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image14.png)

<span data-ttu-id="36d59-242">후속 배포를 지원 하려면 해야 배포 계정을 추가 하는 **db\_소유자** 처음 배포 된 후 데이터베이스의 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-242">To support subsequent deployments, you'll also need to add the deploying account to the **db\_owner** role on the database after the first deployment.</span></span> <span data-ttu-id="36d59-243">후속 배포에는 기존 데이터베이스의 스키마를 수정 하지 않고 있습니다 새 데이터베이스를 만들기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-243">This is because on subsequent deployments you're modifying the schema of an existing database, rather than creating a new database.</span></span> <span data-ttu-id="36d59-244">이전 섹션에서 설명한 대로, 여러 가지 이유로 데이터베이스를 만든 때까지 사용자는 데이터베이스 역할에 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-244">As described in the previous section, you can't add a user to a database role until you've created the database, for obvious reasons.</span></span>

<span data-ttu-id="36d59-245">**Db 배포 계정 로그인에 매핑할\_소유자 데이터베이스 역할**</span><span class="sxs-lookup"><span data-stu-id="36d59-245">**To map the deployment account login to the db\_owner database role**</span></span>

1. <span data-ttu-id="36d59-246">이전 처럼 SQL Server Management Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-246">Open SQL Server Management Studio as before.</span></span>
2. <span data-ttu-id="36d59-247">에 **개체 탐색기** 창 확장를 **보안** 노드를 확장 합니다 **로그인** 노드를 컴퓨터 계정 로그인을 두 번 클릭 하 고 (예를 들어,  **FABRIKAM\matt**).</span><span class="sxs-lookup"><span data-stu-id="36d59-247">In the **Object Explorer** window, expand the **Security** node, expand the **Logins** node, and then double-click the machine account login (for example, **FABRIKAM\matt**).</span></span>
3. <span data-ttu-id="36d59-248">에 **로그인 속성** 대화 상자, 클릭 **사용자 매핑**합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-248">In the **Login Properties** dialog box, click **User Mapping**.</span></span>
4. <span data-ttu-id="36d59-249">에 **이 로그인으로 매핑된 사용자** 테이블에서 데이터베이스의 이름을 선택 (예를 들어 **ContactManager**).</span><span class="sxs-lookup"><span data-stu-id="36d59-249">In the **Users mapped to this login** table, select the name of your database (for example, **ContactManager**).</span></span>
5. <span data-ttu-id="36d59-250">에 **데이터베이스 역할 멤버 자격:** *[데이터베이스 이름]* 목록에서를 **db\_소유자** 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-250">In the **Database role membership for:** *[database name]* list, select the **db\_owner** role.</span></span>

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image15.png)
6. <span data-ttu-id="36d59-251">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-251">Click **OK**.</span></span>

## <a name="conclusion"></a><span data-ttu-id="36d59-252">결론</span><span class="sxs-lookup"><span data-stu-id="36d59-252">Conclusion</span></span>

<span data-ttu-id="36d59-253">이제 데이터베이스 서버에 원격 데이터베이스 배포를 허용 하는 데 원격 IIS 웹 서버가 데이터베이스에 액세스할 수 있도록 준비 됩니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-253">Your database server should now be ready to accept remote database deployments and to allow remote IIS web servers to access your databases.</span></span> <span data-ttu-id="36d59-254">배포 하 고 데이터베이스를 사용 하려고 하기 전에 이러한 요점을 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-254">Before you attempt to deploy and use databases, you may want to check these key points:</span></span>

- <span data-ttu-id="36d59-255">SQL Server 원격 TCP/IP 연결을 허용 하도록 구성 했습니까?</span><span class="sxs-lookup"><span data-stu-id="36d59-255">Have you configured SQL Server to accept remote TCP/IP connections?</span></span>
- <span data-ttu-id="36d59-256">SQL Server 트래픽을 허용 하도록 방화벽을 구성 했습니까?</span><span class="sxs-lookup"><span data-stu-id="36d59-256">Have you configured any firewalls to permit SQL Server traffic?</span></span>
- <span data-ttu-id="36d59-257">SQL Server를 액세스 하는 모든 웹 서버에 대 한 컴퓨터 계정 로그인을 작성 했습니까?</span><span class="sxs-lookup"><span data-stu-id="36d59-257">Have you created a machine account login for every web server that will access SQL Server?</span></span>
- <span data-ttu-id="36d59-258">데이터베이스 배포 스크립트를 만들 사용자 역할 매핑을 포함 또는 처음으로 데이터베이스를 배포한 후 수동으로 이러한 만들어야 하나요?</span><span class="sxs-lookup"><span data-stu-id="36d59-258">Does your database deployment include a script to create user role mappings, or do you need to create these manually after you deploy the database for the first time?</span></span>
- <span data-ttu-id="36d59-259">가 배포 계정에 대 한 로그인을 만들고 추가 하는 **dbcreator** 서버 역할?</span><span class="sxs-lookup"><span data-stu-id="36d59-259">Have you created a login for the deployment account and added it to the **dbcreator** server role?</span></span>

## <a name="further-reading"></a><span data-ttu-id="36d59-260">추가 정보</span><span class="sxs-lookup"><span data-stu-id="36d59-260">Further Reading</span></span>

<span data-ttu-id="36d59-261">데이터베이스 프로젝트를 배포 하는 방법에 대 한 지침을 참조 하세요 [데이터베이스 프로젝트 배포](../web-deployment-in-the-enterprise/deploying-database-projects.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-261">For guidance on deploying database projects, see [Deploying Database Projects](../web-deployment-in-the-enterprise/deploying-database-projects.md).</span></span> <span data-ttu-id="36d59-262">배포 후 스크립트를 실행 하 여 데이터베이스 역할 멤버 자격을 만들기에 대 한 지침을 참조 하세요 [배포 데이터베이스 역할 멤버 자격 테스트 환경에](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-262">For guidance on creating database role memberships by running a post-deployment script, see [Deploying Database Role Memberships to Test Environments](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md).</span></span> <span data-ttu-id="36d59-263">멤버 자격 데이터베이스에서 발생할 수 있는 고유한 배포 과제를 충족 하는 방법에 대 한 지침을 참조 하세요 [엔터프라이즈 환경에 멤버 자격 데이터베이스 배포](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="36d59-263">For guidance on how to meet the unique deployment challenges that membership databases pose, see [Deploying Membership Databases to Enterprise Environments](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="36d59-264">[이전](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
> [다음](creating-a-server-farm-with-the-web-farm-framework.md)</span><span class="sxs-lookup"><span data-stu-id="36d59-264">[Previous](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
[Next](creating-a-server-farm-with-the-web-farm-framework.md)</span></span>
