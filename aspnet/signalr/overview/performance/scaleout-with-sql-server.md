---
uid: signalr/overview/performance/scaleout-with-sql-server
title: SQL Server와 함께 SignalR 확장 | Microsoft Docs
author: MikeWasson
description: 이전 버전의에 대 한 내용은이 항목의 버전 2 이전 버전을 Visual Studio 2013.NET 4.5 SignalR이이 항목에서 사용 하는 소프트웨어 버전 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: 98358b6e-9139-4239-ba3a-2d7dd74dd664
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/performance/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: b3189c36fc076333c0c6007bd039b12e03d63bc8
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="signalr-scaleout-with-sql-server"></a><span data-ttu-id="15557-103">SQL Server와 함께 SignalR 확장</span><span class="sxs-lookup"><span data-stu-id="15557-103">SignalR Scaleout with SQL Server</span></span>
====================
<span data-ttu-id="15557-104">여 [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="15557-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="15557-105">이 항목에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="15557-105">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="15557-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="15557-106">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="15557-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="15557-107">.NET 4.5</span></span>
> - <span data-ttu-id="15557-108">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="15557-108">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="15557-109">이 항목의 이전 버전</span><span class="sxs-lookup"><span data-stu-id="15557-109">Previous versions of this topic</span></span>
> 
> <span data-ttu-id="15557-110">이전 버전의 SignalR에 대 한 정보를 참조 하십시오. [SignalR 이전 버전](../older-versions/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="15557-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="15557-111">질문이 나 의견이</span><span class="sxs-lookup"><span data-stu-id="15557-111">Questions and comments</span></span>
> 
> <span data-ttu-id="15557-112">이 자습서를 연결 하는 방법 및 페이지의 맨 아래에 주석에서 향상 될 수 있습니다 어떻게에 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="15557-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="15557-113">자습서를 직접 관련 되지 않는 질문 해야 하도록를 게시할 수 있습니다는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="15557-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


<span data-ttu-id="15557-114">이 자습서에서는 SQL Server를 사용 하 여 두 개의 별도 IIS 인스턴스에서 배포 되는 SignalR 응용 프로그램 간에 메시지를 분산 합니다.</span><span class="sxs-lookup"><span data-stu-id="15557-114">In this tutorial, you will use SQL Server to distribute messages across a SignalR application that is deployed in two separate IIS instances.</span></span> <span data-ttu-id="15557-115">단일 테스트 컴퓨터에서이 자습서를 실행할 수도 있지만 모든 결과 얻기 위해 둘 이상의 서버 SignalR 응용 프로그램 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15557-115">You can also run this tutorial on a single test machine, but to get the full effect, you need to deploy the SignalR application to two or more servers.</span></span> <span data-ttu-id="15557-116">서버 중 하나 또는 별도 전용된 서버에도 SQL Server를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15557-116">You must also install SQL Server on one of the servers, or on a separate dedicated server.</span></span> <span data-ttu-id="15557-117">두 번째 방법은 Azure에서 Vm을 사용 하는 자습서를 실행 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="15557-117">Another option is to run the tutorial using VMs on Azure.</span></span>

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a><span data-ttu-id="15557-118">전제 조건</span><span class="sxs-lookup"><span data-stu-id="15557-118">Prerequisites</span></span>

<span data-ttu-id="15557-119">Microsoft SQL Server 2005 이상입니다.</span><span class="sxs-lookup"><span data-stu-id="15557-119">Microsoft SQL Server 2005 or later.</span></span> <span data-ttu-id="15557-120">백플레인에서는 데스크톱 및 서버 모두 SQL Server 버전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="15557-120">The backplane supports both desktop and server editions of SQL Server.</span></span> <span data-ttu-id="15557-121">SQL Server Compact Edition 또는 Azure SQL 데이터베이스를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15557-121">It does not support SQL Server Compact Edition or Azure SQL Database.</span></span> <span data-ttu-id="15557-122">(응용 프로그램을 Azure에서 호스트 될 고려 서비스 버스 백플레인에서 대신 합니다.)</span><span class="sxs-lookup"><span data-stu-id="15557-122">(If your application is hosted on Azure, consider the Service Bus backplane instead.)</span></span>

## <a name="overview"></a><span data-ttu-id="15557-123">개요</span><span class="sxs-lookup"><span data-stu-id="15557-123">Overview</span></span>

<span data-ttu-id="15557-124">자세한 자습서에 들어가기 전에 수행할 작업의 간략 한 개요는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15557-124">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="15557-125">비어 있는 새 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15557-125">Create a new empty database.</span></span> <span data-ttu-id="15557-126">백플레인에서이 데이터베이스에 필요한 테이블 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="15557-126">The backplane will create the necessary tables in this database.</span></span>
2. <span data-ttu-id="15557-127">응용 프로그램에 이러한 NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="15557-127">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="15557-128">Microsoft.AspNet.SignalR</span><span class="sxs-lookup"><span data-stu-id="15557-128">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="15557-129">Microsoft.AspNet.SignalR.SqlServer</span><span class="sxs-lookup"><span data-stu-id="15557-129">Microsoft.AspNet.SignalR.SqlServer</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. <span data-ttu-id="15557-130">SignalR 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15557-130">Create a SignalR application.</span></span>
4. <span data-ttu-id="15557-131">백플레인에서 구성 하려면 Startup.cs에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="15557-131">Add the following code to Startup.cs to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

   <span data-ttu-id="15557-132">이 코드에 대 한 기본 값으로 백플레인에서 구성 [TableCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.sqlscaleoutconfiguration.tablecount(v=vs.118).aspx) 및 [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="15557-132">This code configures the backplane with the default values for [TableCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.sqlscaleoutconfiguration.tablecount(v=vs.118).aspx) and [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx).</span></span> <span data-ttu-id="15557-133">변경 된 이러한 값에 대 한 정보를 참조 하십시오. [SignalR 성능: 확장 메트릭](signalr-performance.md#scaleout_metrics)합니다.</span><span class="sxs-lookup"><span data-stu-id="15557-133">For information on changing these values, see [SignalR Performance: Scaleout Metrics](signalr-performance.md#scaleout_metrics).</span></span> 

## <a name="configure-the-database"></a><span data-ttu-id="15557-134">데이터베이스 구성</span><span class="sxs-lookup"><span data-stu-id="15557-134">Configure the Database</span></span>

<span data-ttu-id="15557-135">응용 프로그램 Windows 인증 또는 SQL Server 인증을 사용 하는 데이터베이스에 액세스할 수 있는지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15557-135">Decide whether the application will use Windows authentication or SQL Server authentication to access the database.</span></span> <span data-ttu-id="15557-136">그럼에도 불구 하 고 데이터베이스 사용자는 로그인 하 고 스키마를 만들 테이블을 만들 수 있는 권한이 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="15557-136">Regardless, make sure the database user has permissions to log in, create schemas, and create tables.</span></span>

<span data-ttu-id="15557-137">사용할 백플레인에서 대 한 새 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15557-137">Create a new database for the backplane to use.</span></span> <span data-ttu-id="15557-138">데이터베이스에 임의의 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15557-138">You can give the database any name.</span></span> <span data-ttu-id="15557-139">데이터베이스;에서 모든 테이블을 만들 필요가 없습니다. 백플레인에서 필요한 테이블 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="15557-139">You don't need to create any tables in the database; the backplane will create the necessary tables.</span></span>

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a><span data-ttu-id="15557-140">Service Broker를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="15557-140">Enable Service Broker</span></span>

<span data-ttu-id="15557-141">백플레인 데이터베이스에 대 한 Service Broker를 활성화 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="15557-141">It is recommended to enable Service Broker for the backplane database.</span></span> <span data-ttu-id="15557-142">Service Broker는 메시징 및 백플레인에서 업데이트를 보다 효율적으로 받을 수 있는 SQL Server의 큐에 대 한 기본 지원을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="15557-142">Service Broker provides native support for messaging and queuing in SQL Server, which lets the backplane receive updates more efficiently.</span></span> <span data-ttu-id="15557-143">그러나 (백플레인에서 에서도 사용할 수 없는 Service Broker.)</span><span class="sxs-lookup"><span data-stu-id="15557-143">(However, the backplane also works without Service Broker.)</span></span>

<span data-ttu-id="15557-144">Service Broker가 설정 여부를 확인 하려면 쿼리는 **은\_브로커\_활성화** 열에는 **sys.databases** 카탈로그 뷰.</span><span class="sxs-lookup"><span data-stu-id="15557-144">To check whether Service Broker is enabled, query the **is\_broker\_enabled** column in the **sys.databases** catalog view.</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

<span data-ttu-id="15557-145">Service Broker를 활성화 하려면 다음 SQL 쿼리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15557-145">To enable Service Broker, use the following SQL query:</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> <span data-ttu-id="15557-146">DB에 연결 하는 응용 프로그램이 없습니다 없으면이 쿼리 표시 하려면 교착 상태에 있는지 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="15557-146">If this query appears to deadlock, make sure there are no applications connected to the DB.</span></span>


<span data-ttu-id="15557-147">추적을 사용 하는 경우 추적 Service Broker 사용 되는지 여부를 표시도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15557-147">If you have enabled tracing, the traces will also show whether Service Broker is enabled.</span></span>

## <a name="create-a-signalr-application"></a><span data-ttu-id="15557-148">SignalR 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="15557-148">Create a SignalR Application</span></span>

<span data-ttu-id="15557-149">이러한 자습서 중 하나를 수행 하 여 SignalR 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15557-149">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="15557-150">SignalR 2.0 시작</span><span class="sxs-lookup"><span data-stu-id="15557-150">Getting Started with SignalR 2.0</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="15557-151">SignalR 2.0 및 MVC 5 시작</span><span class="sxs-lookup"><span data-stu-id="15557-151">Getting Started with SignalR 2.0 and MVC 5</span></span>](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

<span data-ttu-id="15557-152">다음으로, SQL Server와 함께 확장을 지원 하도록 채팅 응용 프로그램을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15557-152">Next, we'll modify the chat application to support scaleout with SQL Server.</span></span> <span data-ttu-id="15557-153">먼저 프로젝트에 SignalR.SqlServer NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="15557-153">First, add the SignalR.SqlServer NuGet package to your project.</span></span> <span data-ttu-id="15557-154">Visual Studio에서에서 **도구** 메뉴 선택 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="15557-154">In Visual Studio, from the **Tools** menu, select **Library Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="15557-155">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="15557-155">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

<span data-ttu-id="15557-156">다음으로 Startup.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="15557-156">Next, open the Startup.cs file.</span></span> <span data-ttu-id="15557-157">다음 코드를 추가 하는 **구성** 메서드:</span><span class="sxs-lookup"><span data-stu-id="15557-157">Add the following code to the **Configure** method:</span></span>

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="15557-158">배포 및 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="15557-158">Deploy and Run the Application</span></span>

<span data-ttu-id="15557-159">SignalR 응용 프로그램을 배포 하 여 Windows Server 인스턴스를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="15557-159">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="15557-160">IIS 역할을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="15557-160">Add the IIS role.</span></span> <span data-ttu-id="15557-161">WebSocket 프로토콜을 포함 하 여 "응용 프로그램 개발" 기능을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="15557-161">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-sql-server/_static/image4.png)

<span data-ttu-id="15557-162">관리 서비스 ("관리 도구" 아래에 나열)도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15557-162">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-sql-server/_static/image5.png)

<span data-ttu-id="15557-163">**설치 웹 배포 3.0.**</span><span class="sxs-lookup"><span data-stu-id="15557-163">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="15557-164">IIS 관리자를 실행 하면, Microsoft 웹 플랫폼 설치를 묻습니다 또는 할 수 있습니다 때 [는 intstaller 다운로드](https://go.microsoft.com/fwlink/?LinkId=255386)합니다.</span><span class="sxs-lookup"><span data-stu-id="15557-164">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the intstaller](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="15557-165">플랫폼 설치 관리자에서 웹 배포를 검색 하 고 웹 배포 3.0 설치</span><span class="sxs-lookup"><span data-stu-id="15557-165">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-sql-server/_static/image6.png)

<span data-ttu-id="15557-166">웹 관리 서비스에서 실행 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="15557-166">Check that the Web Management Service is running.</span></span> <span data-ttu-id="15557-167">그렇지 않은 경우 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="15557-167">If not, start the service.</span></span> <span data-ttu-id="15557-168">(웹 관리 서비스 보이지 않으면의 Windows 서비스 목록에 있는지 확인 IIS 역할을 추가 했을 때 관리 서비스를 설치 합니다.)</span><span class="sxs-lookup"><span data-stu-id="15557-168">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="15557-169">마지막으로, tcp 8172 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="15557-169">Finally, open port 8172 for TCP.</span></span> <span data-ttu-id="15557-170">웹 배포 도구를 사용 하는 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="15557-170">This is the port that the Web Deploy tool uses.</span></span>

<span data-ttu-id="15557-171">이제 서버에 개발 컴퓨터에서 Visual Studio 프로젝트를 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15557-171">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="15557-172">솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="15557-172">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="15557-173">웹 배포에 대 한 설명서 보다 자세한 참조 [Visual Studio 및 ASP.NET에 대 한 웹 배포 콘텐츠 맵](../../../whitepapers/aspnet-web-deployment-content-map.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="15557-173">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="15557-174">두 명의 서버에 응용 프로그램을 배포 하는 경우 각 인스턴스는 별도 브라우저 창에서 열고 하 고 다른에서 SignalR 메시지를 받을 구성 파일은 각각을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15557-174">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="15557-175">(물론, 프로덕션 환경에서 두 서버는 sit 부하 분산 장치 뒤.)</span><span class="sxs-lookup"><span data-stu-id="15557-175">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-sql-server/_static/image7.png)

<span data-ttu-id="15557-176">응용 프로그램을 실행 한 후에 SignalR에 데이터베이스에 테이블을 만들었다고 자동으로 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15557-176">After you run the application, you can see that SignalR has automatically created tables in the database:</span></span>

![](scaleout-with-sql-server/_static/image8.png)

<span data-ttu-id="15557-177">SignalR 테이블을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="15557-177">SignalR manages the tables.</span></span> <span data-ttu-id="15557-178">응용 프로그램을 배포한으로 하지 않는 행을 삭제을 테이블을 수정 하 고 등 합니다.</span><span class="sxs-lookup"><span data-stu-id="15557-178">As long as your application is deployed, don't delete rows, modify the table, and so forth.</span></span>
