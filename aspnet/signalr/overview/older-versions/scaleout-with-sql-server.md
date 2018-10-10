---
uid: signalr/overview/older-versions/scaleout-with-sql-server
title: SQL Server로 SignalR 규모 확장 (SignalR 1.x) | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 05/01/2013
ms.assetid: 1dca7967-8296-444a-9533-837eb284e78c
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: d68196aa8e4d0c60570a0e36ccc75a2a080d57bc
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "48912750"
---
<a name="signalr-scaleout-with-sql-server-signalr-1x"></a><span data-ttu-id="81e94-102">SQL Server로 SignalR 규모 확장 (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="81e94-102">SignalR Scaleout with SQL Server (SignalR 1.x)</span></span>
====================
<span data-ttu-id="81e94-103">하 여 [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="81e94-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

<span data-ttu-id="81e94-104">이 자습서에서는 SQL Server를 사용 하 여 메시지를 두 개의 별도 IIS 인스턴스에서 배포 되는 SignalR 응용 프로그램을 분산 하는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-104">In this tutorial, you will use SQL Server to distribute messages across a SignalR application that is deployed in two separate IIS instances.</span></span> <span data-ttu-id="81e94-105">단일 테스트 컴퓨터에서이 자습서를 실행할 수도 있지만 모든 결과 얻으려면 두 개 이상의 서버에 SignalR 응용 프로그램을 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-105">You can also run this tutorial on a single test machine, but to get the full effect, you need to deploy the SignalR application to two or more servers.</span></span> <span data-ttu-id="81e94-106">서버 중 하나에서 또는 별도 전용 서버에 SQL Server를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-106">You must also install SQL Server on one of the servers, or on a separate dedicated server.</span></span> <span data-ttu-id="81e94-107">Azure에서 Vm을 사용 하는 자습서를 실행 하는 방법도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-107">Another option is to run the tutorial using VMs on Azure.</span></span>

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a><span data-ttu-id="81e94-108">전제 조건</span><span class="sxs-lookup"><span data-stu-id="81e94-108">Prerequisites</span></span>

<span data-ttu-id="81e94-109">Microsoft SQL Server 2005 이상입니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-109">Microsoft SQL Server 2005 or later.</span></span> <span data-ttu-id="81e94-110">백플레인에서는 데스크톱 및 서버 모두 SQL Server 버전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-110">The backplane supports both desktop and server editions of SQL Server.</span></span> <span data-ttu-id="81e94-111">Azure SQL Database 또는 SQL Server Compact Edition을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-111">It does not support SQL Server Compact Edition or Azure SQL Database.</span></span> <span data-ttu-id="81e94-112">(응용 프로그램을 Azure에서 호스팅되는 경우 Service Bus 백플레인에서 대신 고려 합니다.)</span><span class="sxs-lookup"><span data-stu-id="81e94-112">(If your application is hosted on Azure, consider the Service Bus backplane instead.)</span></span>

## <a name="overview"></a><span data-ttu-id="81e94-113">개요</span><span class="sxs-lookup"><span data-stu-id="81e94-113">Overview</span></span>

<span data-ttu-id="81e94-114">자세한 자습서를 시작 하기 전에 수행할 작업의 간략 한 개요는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-114">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="81e94-115">새 빈 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-115">Create a new empty database.</span></span> <span data-ttu-id="81e94-116">백플레인에서이 데이터베이스에 필요한 테이블을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-116">The backplane will create the necessary tables in this database.</span></span>
2. <span data-ttu-id="81e94-117">응용 프로그램에 이러한 NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-117">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="81e94-118">Microsoft.AspNet.SignalR</span><span class="sxs-lookup"><span data-stu-id="81e94-118">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="81e94-119">Microsoft.AspNet.SignalR.SqlServer</span><span class="sxs-lookup"><span data-stu-id="81e94-119">Microsoft.AspNet.SignalR.SqlServer</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. <span data-ttu-id="81e94-120">SignalR 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-120">Create a SignalR application.</span></span>
4. <span data-ttu-id="81e94-121">Global.asax 백플레인에서 구성 하려면 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-121">Add the following code to Global.asax to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

## <a name="configure-the-database"></a><span data-ttu-id="81e94-122">데이터베이스 구성</span><span class="sxs-lookup"><span data-stu-id="81e94-122">Configure the Database</span></span>

<span data-ttu-id="81e94-123">응용 프로그램 Windows 인증 또는 SQL Server 인증을 사용 하는 데이터베이스에 액세스할 수 있는지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-123">Decide whether the application will use Windows authentication or SQL Server authentication to access the database.</span></span> <span data-ttu-id="81e94-124">그럼에도 불구 하 고 데이터베이스 사용자 로그인, 스키마를 만들고, 테이블을 만들 수 있는 권한이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-124">Regardless, make sure the database user has permissions to log in, create schemas, and create tables.</span></span>

<span data-ttu-id="81e94-125">백플레인으로 사용에 대 한 새 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-125">Create a new database for the backplane to use.</span></span> <span data-ttu-id="81e94-126">데이터베이스 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-126">You can give the database any name.</span></span> <span data-ttu-id="81e94-127">데이터베이스에서 모든 테이블을 만들 필요가 없습니다. 백플레인에서 필요한 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-127">You don't need to create any tables in the database; the backplane will create the necessary tables.</span></span>

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a><span data-ttu-id="81e94-128">Service Broker를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="81e94-128">Enable Service Broker</span></span>

<span data-ttu-id="81e94-129">백플레인에서 데이터베이스에 대 한 Service Broker를 활성화 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-129">It is recommended to enable Service Broker for the backplane database.</span></span> <span data-ttu-id="81e94-130">Service Broker는 메시징 및 백플레인에서 업데이트를 보다 효율적으로 받을 수 있는 SQL Server의 큐에 대 한 기본 지원을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-130">Service Broker provides native support for messaging and queuing in SQL Server, which lets the backplane receive updates more efficiently.</span></span> <span data-ttu-id="81e94-131">그러나 (백플레인에서 없이 이루어집니다 Service Broker.)</span><span class="sxs-lookup"><span data-stu-id="81e94-131">(However, the backplane also works without Service Broker.)</span></span>

<span data-ttu-id="81e94-132">Service Broker 사용 되는지 여부를 확인, 쿼리를 **은\_broker\_사용 하도록 설정** 열에는 **sys.databases** 카탈로그 뷰.</span><span class="sxs-lookup"><span data-stu-id="81e94-132">To check whether Service Broker is enabled, query the **is\_broker\_enabled** column in the **sys.databases** catalog view.</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

<span data-ttu-id="81e94-133">Service Broker를 사용 하도록 설정 하려면 다음 SQL 쿼리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-133">To enable Service Broker, use the following SQL query:</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> <span data-ttu-id="81e94-134">교착 상태가 발생 했는지를이 쿼리가 나타납니다 경우 DB에 연결 하는 응용 프로그램이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-134">If this query appears to deadlock, make sure there are no applications connected to the DB.</span></span>

<span data-ttu-id="81e94-135">추적을 설정한 경우 추적 Service Broker 사용 되는지 여부를 표시도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-135">If you have enabled tracing, the traces will also show whether Service Broker is enabled.</span></span>

## <a name="create-a-signalr-application"></a><span data-ttu-id="81e94-136">SignalR 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="81e94-136">Create a SignalR Application</span></span>

<span data-ttu-id="81e94-137">이러한 자습서 중 하나를 수행 하 여 SignalR 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-137">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="81e94-138">SignalR 시작</span><span class="sxs-lookup"><span data-stu-id="81e94-138">Getting Started with SignalR</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="81e94-139">SignalR 및 MVC 4 시작</span><span class="sxs-lookup"><span data-stu-id="81e94-139">Getting Started with SignalR and MVC 4</span></span>](tutorial-getting-started-with-signalr-and-mvc-4.md)

<span data-ttu-id="81e94-140">다음으로, SQL Server를 사용 하 여 확장을 지원 하기 위해 채팅 응용 프로그램을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-140">Next, we'll modify the chat application to support scaleout with SQL Server.</span></span> <span data-ttu-id="81e94-141">먼저 프로젝트에 SignalR.SqlServer NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-141">First, add the SignalR.SqlServer NuGet package to your project.</span></span> <span data-ttu-id="81e94-142">Visual Studio에서에서 합니다 **도구** 메뉴에서 **NuGet 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-142">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="81e94-143">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-143">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

<span data-ttu-id="81e94-144">다음으로 Global.asax 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-144">Next, open the Global.asax file.</span></span> <span data-ttu-id="81e94-145">다음 코드를 추가 합니다 **응용 프로그램\_시작** 메서드:</span><span class="sxs-lookup"><span data-stu-id="81e94-145">Add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="81e94-146">배포 하 고 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="81e94-146">Deploy and Run the Application</span></span>

<span data-ttu-id="81e94-147">SignalR 응용 프로그램을 배포 하려면 Windows Server 인스턴스를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-147">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="81e94-148">IIS 역할을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-148">Add the IIS role.</span></span> <span data-ttu-id="81e94-149">WebSocket 프로토콜을 포함 하 여 "응용 프로그램 개발" 기능을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-149">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-sql-server/_static/image4.png)

<span data-ttu-id="81e94-150">관리 서비스 ("관리 도구" 아래)를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-150">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-sql-server/_static/image5.png)

<span data-ttu-id="81e94-151">**설치 웹 배포 3.0.**</span><span class="sxs-lookup"><span data-stu-id="81e94-151">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="81e94-152">IIS 관리자를 실행 하면, Microsoft 웹 플랫폼을 설치 하 라는 메시지가 나타납니다 것 또는 할 수 있습니다 [다운로드를 intstaller](https://go.microsoft.com/fwlink/?LinkId=255386)합니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-152">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the intstaller](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="81e94-153">플랫폼 설치 관리자에서 웹 배포에 대 한 검색 하 고 웹 배포 3.0 설치</span><span class="sxs-lookup"><span data-stu-id="81e94-153">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-sql-server/_static/image6.png)

<span data-ttu-id="81e94-154">Web Management Service가 실행 중인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-154">Check that the Web Management Service is running.</span></span> <span data-ttu-id="81e94-155">그렇지 않은 경우 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-155">If not, start the service.</span></span> <span data-ttu-id="81e94-156">(웹 관리 서비스 Windows 서비스 목록에 보이지 않으면 확인 IIS 역할을 추가 했을 때 Management 서비스를 설치 합니다.)</span><span class="sxs-lookup"><span data-stu-id="81e94-156">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="81e94-157">마지막으로, tcp 8172 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-157">Finally, open port 8172 for TCP.</span></span> <span data-ttu-id="81e94-158">웹 배포 도구를 사용 하는 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-158">This is the port that the Web Deploy tool uses.</span></span>

<span data-ttu-id="81e94-159">이제 서버에 개발 컴퓨터에서 Visual Studio 프로젝트를 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-159">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="81e94-160">솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-160">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="81e94-161">자세한 내용을 보려면 웹 배포에 대 한 설명서를 참조 하세요 [Visual Studio 및 ASP.NET 웹 배포 콘텐츠 맵](../../../whitepapers/aspnet-web-deployment-content-map.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-161">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="81e94-162">두 명의 서버 응용 프로그램을 배포 하는 경우에 별도 브라우저 창에서 각 인스턴스를 엽니다 하 고 다른에서 SignalR 메시지를 받을 각각 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-162">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="81e94-163">(물론 프로덕션 환경에서 두 서버는 sit 부하 분산 합니다.)</span><span class="sxs-lookup"><span data-stu-id="81e94-163">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-sql-server/_static/image7.png)

<span data-ttu-id="81e94-164">응용 프로그램을 실행 한 후에 SignalR에 데이터베이스의 테이블을 만들었다고 자동으로 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-164">After you run the application, you can see that SignalR has automatically created tables in the database:</span></span>

![](scaleout-with-sql-server/_static/image8.png)

<span data-ttu-id="81e94-165">SignalR의 테이블을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-165">SignalR manages the tables.</span></span> <span data-ttu-id="81e94-166">응용 프로그램을 배포 하기만 없는 행을 삭제, 테이블을 수정 및 등입니다.</span><span class="sxs-lookup"><span data-stu-id="81e94-166">As long as your application is deployed, don't delete rows, modify the table, and so forth.</span></span>
