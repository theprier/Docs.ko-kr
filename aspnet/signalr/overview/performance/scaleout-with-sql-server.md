---
uid: signalr/overview/performance/scaleout-with-sql-server
title: SQL Server로 SignalR 규모 확장 | Microsoft Docs
author: MikeWasson
description: 이전 버전의에 대 한 내용은이 항목의 버전 2 이전 버전을이 항목에서는 Visual Studio 2013.NET 4.5 SignalR에서 사용 하는 소프트웨어 버전...
ms.author: riande
ms.date: 06/10/2014
ms.assetid: 98358b6e-9139-4239-ba3a-2d7dd74dd664
msc.legacyurl: /signalr/overview/performance/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: 73b16ecf141732f0adc362dc5167073491cc2dea
ms.sourcegitcommit: 74e3be25ea37b5fc8b4b433b0b872547b4b99186
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2018
ms.locfileid: "53287015"
---
<a name="signalr-scaleout-with-sql-server"></a><span data-ttu-id="28170-103">SQL Server로 SignalR 규모 확장</span><span class="sxs-lookup"><span data-stu-id="28170-103">SignalR Scaleout with SQL Server</span></span>
====================
<span data-ttu-id="28170-104">하 여 [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="28170-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="28170-105">이 항목에서 사용 하는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="28170-105">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="28170-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="28170-106">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="28170-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="28170-107">.NET 4.5</span></span>
> - <span data-ttu-id="28170-108">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="28170-108">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="28170-109">이 항목의 이전 버전</span><span class="sxs-lookup"><span data-stu-id="28170-109">Previous versions of this topic</span></span>
>
> <span data-ttu-id="28170-110">이전 버전의 SignalR에 대 한 정보를 참조 하세요 [SignalR 이전 버전](../older-versions/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="28170-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="28170-111">질문이 나 의견이 있으면</span><span class="sxs-lookup"><span data-stu-id="28170-111">Questions and comments</span></span>
>
> <span data-ttu-id="28170-112">이 자습서를 연결 하는 방법 및 새로운 개선할 수 있습니다 페이지의 맨 아래에 의견에서에 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="28170-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="28170-113">에 자습서로 직접 관련 되지 않은 질문이 있을 경우 게시할 수 하는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="28170-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


<span data-ttu-id="28170-114">이 자습서에서는 SQL Server를 사용 하 여 메시지를 두 개의 별도 IIS 인스턴스에서 배포 되는 SignalR 응용 프로그램을 분산 하는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28170-114">In this tutorial, you will use SQL Server to distribute messages across a SignalR application that is deployed in two separate IIS instances.</span></span> <span data-ttu-id="28170-115">단일 테스트 컴퓨터에서이 자습서를 실행할 수도 있지만 모든 결과 얻으려면 두 개 이상의 서버에 SignalR 응용 프로그램을 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28170-115">You can also run this tutorial on a single test machine, but to get the full effect, you need to deploy the SignalR application to two or more servers.</span></span> <span data-ttu-id="28170-116">서버 중 하나에서 또는 별도 전용 서버에 SQL Server를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28170-116">You must also install SQL Server on one of the servers, or on a separate dedicated server.</span></span> <span data-ttu-id="28170-117">Azure에서 Vm을 사용 하는 자습서를 실행 하는 방법도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28170-117">Another option is to run the tutorial using VMs on Azure.</span></span>

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a><span data-ttu-id="28170-118">전제 조건</span><span class="sxs-lookup"><span data-stu-id="28170-118">Prerequisites</span></span>

<span data-ttu-id="28170-119">Microsoft SQL Server 2005 이상입니다.</span><span class="sxs-lookup"><span data-stu-id="28170-119">Microsoft SQL Server 2005 or later.</span></span> <span data-ttu-id="28170-120">백플레인에서는 데스크톱 및 서버 모두 SQL Server 버전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="28170-120">The backplane supports both desktop and server editions of SQL Server.</span></span> <span data-ttu-id="28170-121">Azure SQL Database 또는 SQL Server Compact Edition을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="28170-121">It does not support SQL Server Compact Edition or Azure SQL Database.</span></span> <span data-ttu-id="28170-122">(응용 프로그램을 Azure에서 호스팅되는 경우 Service Bus 백플레인에서 대신 고려 합니다.)</span><span class="sxs-lookup"><span data-stu-id="28170-122">(If your application is hosted on Azure, consider the Service Bus backplane instead.)</span></span>

## <a name="overview"></a><span data-ttu-id="28170-123">개요</span><span class="sxs-lookup"><span data-stu-id="28170-123">Overview</span></span>

<span data-ttu-id="28170-124">자세한 자습서를 시작 하기 전에 수행할 작업의 간략 한 개요는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="28170-124">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="28170-125">새 빈 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28170-125">Create a new empty database.</span></span> <span data-ttu-id="28170-126">백플레인에서이 데이터베이스에 필요한 테이블을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="28170-126">The backplane will create the necessary tables in this database.</span></span>
2. <span data-ttu-id="28170-127">응용 프로그램에 이러한 NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="28170-127">Add these NuGet packages to your application:</span></span>

    - [<span data-ttu-id="28170-128">Microsoft.AspNet.SignalR</span><span class="sxs-lookup"><span data-stu-id="28170-128">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="28170-129">Microsoft.AspNet.SignalR.SqlServer</span><span class="sxs-lookup"><span data-stu-id="28170-129">Microsoft.AspNet.SignalR.SqlServer</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. <span data-ttu-id="28170-130">SignalR 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28170-130">Create a SignalR application.</span></span>
4. <span data-ttu-id="28170-131">Startup.cs 백플레인에서 구성 하려면 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="28170-131">Add the following code to Startup.cs to configure the backplane:</span></span>

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

   <span data-ttu-id="28170-132">이 코드에 대 한 기본값을 사용 하 여 백플레인에서 구성 [TableCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.sqlscaleoutconfiguration.tablecount(v=vs.118).aspx) 하 고 [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="28170-132">This code configures the backplane with the default values for [TableCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.sqlscaleoutconfiguration.tablecount(v=vs.118).aspx) and [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx).</span></span> <span data-ttu-id="28170-133">이러한 값을 변경에 대 한 정보를 참조 하세요. [SignalR 성능: 확장 메트릭을](signalr-performance.md#scaleout_metrics)합니다.</span><span class="sxs-lookup"><span data-stu-id="28170-133">For information on changing these values, see [SignalR Performance: Scaleout Metrics](signalr-performance.md#scaleout_metrics).</span></span>

## <a name="configure-the-database"></a><span data-ttu-id="28170-134">데이터베이스 구성</span><span class="sxs-lookup"><span data-stu-id="28170-134">Configure the Database</span></span>

<span data-ttu-id="28170-135">응용 프로그램 Windows 인증 또는 SQL Server 인증을 사용 하는 데이터베이스에 액세스할 수 있는지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="28170-135">Decide whether the application will use Windows authentication or SQL Server authentication to access the database.</span></span> <span data-ttu-id="28170-136">그럼에도 불구 하 고 데이터베이스 사용자 로그인, 스키마를 만들고, 테이블을 만들 수 있는 권한이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="28170-136">Regardless, make sure the database user has permissions to log in, create schemas, and create tables.</span></span>

<span data-ttu-id="28170-137">백플레인으로 사용에 대 한 새 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28170-137">Create a new database for the backplane to use.</span></span> <span data-ttu-id="28170-138">데이터베이스 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28170-138">You can give the database any name.</span></span> <span data-ttu-id="28170-139">데이터베이스에서 모든 테이블을 만들 필요가 없습니다. 백플레인에서 필요한 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28170-139">You don't need to create any tables in the database; the backplane will create the necessary tables.</span></span>

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a><span data-ttu-id="28170-140">Service Broker를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="28170-140">Enable Service Broker</span></span>

<span data-ttu-id="28170-141">백플레인에서 데이터베이스에 대 한 Service Broker를 활성화 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="28170-141">It is recommended to enable Service Broker for the backplane database.</span></span> <span data-ttu-id="28170-142">Service Broker는 메시징 및 백플레인에서 업데이트를 보다 효율적으로 받을 수 있는 SQL Server의 큐에 대 한 기본 지원을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="28170-142">Service Broker provides native support for messaging and queuing in SQL Server, which lets the backplane receive updates more efficiently.</span></span> <span data-ttu-id="28170-143">그러나 (백플레인에서 없이 이루어집니다 Service Broker.)</span><span class="sxs-lookup"><span data-stu-id="28170-143">(However, the backplane also works without Service Broker.)</span></span>

<span data-ttu-id="28170-144">Service Broker 사용 되는지 여부를 확인, 쿼리를 **은\_broker\_사용 하도록 설정** 열에는 **sys.databases** 카탈로그 뷰.</span><span class="sxs-lookup"><span data-stu-id="28170-144">To check whether Service Broker is enabled, query the **is\_broker\_enabled** column in the **sys.databases** catalog view.</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

<span data-ttu-id="28170-145">Service Broker를 사용 하도록 설정 하려면 다음 SQL 쿼리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="28170-145">To enable Service Broker, use the following SQL query:</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> <span data-ttu-id="28170-146">교착 상태가 발생 했는지를이 쿼리가 나타납니다 경우 DB에 연결 하는 응용 프로그램이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="28170-146">If this query appears to deadlock, make sure there are no applications connected to the DB.</span></span>


<span data-ttu-id="28170-147">추적을 설정한 경우 추적 Service Broker 사용 되는지 여부를 표시도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28170-147">If you have enabled tracing, the traces will also show whether Service Broker is enabled.</span></span>

## <a name="create-a-signalr-application"></a><span data-ttu-id="28170-148">SignalR 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="28170-148">Create a SignalR Application</span></span>

<span data-ttu-id="28170-149">이러한 자습서 중 하나를 수행 하 여 SignalR 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28170-149">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="28170-150">SignalR 2.0 시작</span><span class="sxs-lookup"><span data-stu-id="28170-150">Getting Started with SignalR 2.0</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="28170-151">SignalR 2.0 및 MVC 5 시작</span><span class="sxs-lookup"><span data-stu-id="28170-151">Getting Started with SignalR 2.0 and MVC 5</span></span>](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

<span data-ttu-id="28170-152">다음으로, SQL Server를 사용 하 여 확장을 지원 하기 위해 채팅 응용 프로그램을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="28170-152">Next, we'll modify the chat application to support scaleout with SQL Server.</span></span> <span data-ttu-id="28170-153">먼저 프로젝트에 SignalR.SqlServer NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="28170-153">First, add the SignalR.SqlServer NuGet package to your project.</span></span> <span data-ttu-id="28170-154">Visual Studio에서에서 합니다 **도구** 메뉴에서 **NuGet 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="28170-154">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="28170-155">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="28170-155">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

<span data-ttu-id="28170-156">다음으로, Startup.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="28170-156">Next, open the Startup.cs file.</span></span> <span data-ttu-id="28170-157">다음 코드를 추가 합니다 **구성** 메서드:</span><span class="sxs-lookup"><span data-stu-id="28170-157">Add the following code to the **Configure** method:</span></span>

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="28170-158">배포 하 고 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="28170-158">Deploy and Run the Application</span></span>

<span data-ttu-id="28170-159">SignalR 응용 프로그램을 배포 하려면 Windows Server 인스턴스를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="28170-159">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="28170-160">IIS 역할을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="28170-160">Add the IIS role.</span></span> <span data-ttu-id="28170-161">WebSocket 프로토콜을 포함 하 여 "응용 프로그램 개발" 기능을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="28170-161">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-sql-server/_static/image4.png)

<span data-ttu-id="28170-162">관리 서비스 ("관리 도구" 아래)를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="28170-162">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-sql-server/_static/image5.png)

<span data-ttu-id="28170-163">**설치 웹 배포 3.0.**</span><span class="sxs-lookup"><span data-stu-id="28170-163">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="28170-164">IIS 관리자를 실행 하면, Microsoft 웹 플랫폼을 설치 하 라는 메시지가 나타납니다 것 또는 할 수 있습니다 [다운로드를 intstaller](https://go.microsoft.com/fwlink/?LinkId=255386)합니다.</span><span class="sxs-lookup"><span data-stu-id="28170-164">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the intstaller](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="28170-165">플랫폼 설치 관리자에서 웹 배포에 대 한 검색 하 고 웹 배포 3.0 설치</span><span class="sxs-lookup"><span data-stu-id="28170-165">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-sql-server/_static/image6.png)

<span data-ttu-id="28170-166">Web Management Service가 실행 중인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="28170-166">Check that the Web Management Service is running.</span></span> <span data-ttu-id="28170-167">그렇지 않은 경우 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="28170-167">If not, start the service.</span></span> <span data-ttu-id="28170-168">(웹 관리 서비스 Windows 서비스 목록에 보이지 않으면 확인 IIS 역할을 추가 했을 때 Management 서비스를 설치 합니다.)</span><span class="sxs-lookup"><span data-stu-id="28170-168">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="28170-169">마지막으로, tcp 8172 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="28170-169">Finally, open port 8172 for TCP.</span></span> <span data-ttu-id="28170-170">웹 배포 도구를 사용 하는 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="28170-170">This is the port that the Web Deploy tool uses.</span></span>

<span data-ttu-id="28170-171">이제 서버에 개발 컴퓨터에서 Visual Studio 프로젝트를 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="28170-171">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="28170-172">솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="28170-172">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="28170-173">자세한 내용을 보려면 웹 배포에 대 한 설명서를 참조 하세요 [Visual Studio 및 ASP.NET 웹 배포 콘텐츠 맵](../../../whitepapers/aspnet-web-deployment-content-map.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="28170-173">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="28170-174">두 명의 서버 응용 프로그램을 배포 하는 경우에 별도 브라우저 창에서 각 인스턴스를 엽니다 하 고 다른에서 SignalR 메시지를 받을 각각 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28170-174">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="28170-175">(물론 프로덕션 환경에서 두 서버는 sit 부하 분산 합니다.)</span><span class="sxs-lookup"><span data-stu-id="28170-175">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-sql-server/_static/image7.png)

<span data-ttu-id="28170-176">응용 프로그램을 실행 한 후에 SignalR에 데이터베이스의 테이블을 만들었다고 자동으로 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28170-176">After you run the application, you can see that SignalR has automatically created tables in the database:</span></span>

![](scaleout-with-sql-server/_static/image8.png)

<span data-ttu-id="28170-177">SignalR의 테이블을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="28170-177">SignalR manages the tables.</span></span> <span data-ttu-id="28170-178">응용 프로그램을 배포 하기만 없는 행을 삭제, 테이블을 수정 및 등입니다.</span><span class="sxs-lookup"><span data-stu-id="28170-178">As long as your application is deployed, don't delete rows, modify the table, and so forth.</span></span>
