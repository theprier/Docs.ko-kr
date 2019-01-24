---
uid: signalr/overview/older-versions/scaleout-with-redis
title: Redis로 SignalR 규모 확장 (SignalR 1.x) | Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 6abecf80-8ffa-41ba-b0d9-1d9edbe7687b
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-redis
msc.type: authoredcontent
ms.openlocfilehash: 74294bd04d5649f2ec54e58adb744f5e30525162
ms.sourcegitcommit: ebf4e5a7ca301af8494edf64f85d4a8deb61d641
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54836417"
---
<a name="signalr-scaleout-with-redis-signalr-1x"></a><span data-ttu-id="dc540-102">Redis로 SignalR 규모 확장 (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="dc540-102">SignalR Scaleout with Redis (SignalR 1.x)</span></span>
====================
<span data-ttu-id="dc540-103">하 여 [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="dc540-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="dc540-104">이 자습서에서는 사용할지 [Redis](http://redis.io/) 에 메시지를 두 개의 별도 IIS 인스턴스에 배포 된 SignalR 응용 프로그램을 분산 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-104">In this tutorial, you will use [Redis](http://redis.io/) to distribute messages across a SignalR application that is deployed on two separate IIS instances.</span></span>

<span data-ttu-id="dc540-105">Redis는 메모리 내 키-값 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-105">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="dc540-106">또한 게시/구독 모델을 사용 하 여 메시징 시스템을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-106">It also supports a messaging system with a publish/subscribe model.</span></span> <span data-ttu-id="dc540-107">SignalR에서 Redis 백플레인에서 pub/sub 기능을 사용 하 여 다른 서버에 메시지를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-107">The SignalR Redis backplane uses the pub/sub feature to forward messages to other servers.</span></span>

![](scaleout-with-redis/_static/image1.png)

<span data-ttu-id="dc540-108">이 자습서에서는 세 명의 서버를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-108">For this tutorial, you will use three servers:</span></span>

- <span data-ttu-id="dc540-109">SignalR 응용 프로그램을 배포 하는 데 사용할 Windows를 실행 하는 두 서버.</span><span class="sxs-lookup"><span data-stu-id="dc540-109">Two servers running Windows, which you will use to deploy a SignalR application.</span></span>
- <span data-ttu-id="dc540-110">서버를 하나 사용 하 여 Redis를 실행 하는 Linux를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-110">One server running Linux, which you will use to run Redis.</span></span> <span data-ttu-id="dc540-111">이 자습서의 스크린샷에서, Ubuntu 12.04 TLS 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-111">For the screenshots in this tutorial, I used Ubuntu 12.04 TLS.</span></span>

<span data-ttu-id="dc540-112">사용 하는 세 명의 물리적 서버를 설정 하지 않은 경우에 Hyper-v에서 Vm을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-112">If you don't have three physical servers to use, you can create VMs on Hyper-V.</span></span> <span data-ttu-id="dc540-113">Azure에서 Vm을 만들어야 하는 방법도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-113">Another option is to create VMs on Azure.</span></span>

<span data-ttu-id="dc540-114">이 자습서에서는 공식 Redis 구현 하지만 이기도 한 [Redis의 Windows 포트](https://github.com/MSOpenTech/redis) MSOpenTech에서.</span><span class="sxs-lookup"><span data-stu-id="dc540-114">Although this tutorial uses the official Redis implementation, there is also a [Windows port of Redis](https://github.com/MSOpenTech/redis) from MSOpenTech.</span></span> <span data-ttu-id="dc540-115">설치 및 구성 서로 다르지만 고, 그렇지는 단계는 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-115">Setup and configuration are different, but otherwise the steps are the same.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="dc540-116">Redis로 SignalR 규모 확장에서 Redis 클러스터를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-116">SignalR scaleout with Redis does not support Redis clusters.</span></span>


## <a name="overview"></a><span data-ttu-id="dc540-117">개요</span><span class="sxs-lookup"><span data-stu-id="dc540-117">Overview</span></span>

<span data-ttu-id="dc540-118">자세한 자습서를 시작 하기 전에 수행할 작업의 간략 한 개요는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-118">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="dc540-119">Redis를 설치 하 고 Redis 서버를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-119">Install Redis and start the Redis server.</span></span>
2. <span data-ttu-id="dc540-120">응용 프로그램에 이러한 NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-120">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="dc540-121">Microsoft.AspNet.SignalR</span><span class="sxs-lookup"><span data-stu-id="dc540-121">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="dc540-122">Microsoft.AspNet.SignalR.Redis</span><span class="sxs-lookup"><span data-stu-id="dc540-122">Microsoft.AspNet.SignalR.Redis</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR.Redis)
3. <span data-ttu-id="dc540-123">SignalR 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-123">Create a SignalR application.</span></span>
4. <span data-ttu-id="dc540-124">Global.asax 백플레인에서 구성 하려면 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-124">Add the following code to Global.asax to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-redis/samples/sample1.cs)]

## <a name="ubuntu-on-hyper-v"></a><span data-ttu-id="dc540-125">Hyper-v에서 Ubuntu</span><span class="sxs-lookup"><span data-stu-id="dc540-125">Ubuntu on Hyper-V</span></span>

<span data-ttu-id="dc540-126">Windows Hyper-v를 사용 하 여 Windows Server에서 Ubuntu VM을 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-126">Using Windows Hyper-V, you can easily create an Ubuntu VM on Windows Server.</span></span>

<span data-ttu-id="dc540-127">Ubuntu에서 ISO를 다운로드 [ http://www.ubuntu.com ](http://www.ubuntu.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-127">Download the Ubuntu ISO from [http://www.ubuntu.com](http://www.ubuntu.com/).</span></span>

<span data-ttu-id="dc540-128">Hyper-v에서 새 VM을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-128">In Hyper-V, add a new VM.</span></span> <span data-ttu-id="dc540-129">에 **가상 하드 디스크 연결** 선택 단계 **가상 하드 디스크 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-129">In the **Connect Virtual Hard Disk** step, select **Create a virtual hard disk**.</span></span>

![](scaleout-with-redis/_static/image2.png)

<span data-ttu-id="dc540-130">에 **설치 옵션** 선택 단계 **이미지 파일 (.iso)**, 클릭 **찾아보기**, Ubuntu 설치 ISO 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-130">In the **Installation Options** step, select **Image file (.iso)**, click **Browse**, and browse to the Ubuntu installation ISO.</span></span>

![](scaleout-with-redis/_static/image3.png)

## <a name="install-redis"></a><span data-ttu-id="dc540-131">Redis를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-131">Install Redis</span></span>

<span data-ttu-id="dc540-132">단계에 따라 [ http://redis.io/download ](http://redis.io/download) 다운로드 및 Redis를 빌드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-132">Follow the steps at [http://redis.io/download](http://redis.io/download) to download and build Redis.</span></span>

[!code-console[Main](scaleout-with-redis/samples/sample2.cmd)]

<span data-ttu-id="dc540-133">Redis 이진이 빌드는 `src` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-133">This builds the Redis binaries in the `src` directory.</span></span>

<span data-ttu-id="dc540-134">기본적으로 Redis는 암호를 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-134">By default, Redis does not require a password.</span></span> <span data-ttu-id="dc540-135">암호를 설정 하려면 편집을 `redis.conf` 소스 코드의 루트 디렉터리에 있는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-135">To set a password, edit the `redis.conf` file, which is located in the root directory of the source code.</span></span> <span data-ttu-id="dc540-136">(편집 하기 전에 파일의 백업 복사본을 만듭니다.) 다음 지시문을 추가 `redis.conf`:</span><span class="sxs-lookup"><span data-stu-id="dc540-136">(Make a backup copy of the file before you edit it!) Add the following directive to `redis.conf`:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample3.ps1)]

<span data-ttu-id="dc540-137">이제 Redis 서버를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-137">Now start the Redis server:</span></span>

[!code-css[Main](scaleout-with-redis/samples/sample4.css)]

![](scaleout-with-redis/_static/image4.png)

<span data-ttu-id="dc540-138">열린 포트 6379를 Redis는 기본 포트에서 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-138">Open port 6379, which is the default port that Redis listens on.</span></span> <span data-ttu-id="dc540-139">(구성 파일에서 포트 번호를 변경할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="dc540-139">(You can change the port number in the configuration file.)</span></span>

## <a name="create-the-signalr-application"></a><span data-ttu-id="dc540-140">SignalR 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="dc540-140">Create the SignalR Application</span></span>

<span data-ttu-id="dc540-141">이러한 자습서 중 하나를 수행 하 여 SignalR 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-141">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="dc540-142">SignalR 시작</span><span class="sxs-lookup"><span data-stu-id="dc540-142">Getting Started with SignalR</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="dc540-143">SignalR 및 MVC 4 시작</span><span class="sxs-lookup"><span data-stu-id="dc540-143">Getting Started with SignalR and MVC 4</span></span>](tutorial-getting-started-with-signalr-and-mvc-4.md)

<span data-ttu-id="dc540-144">다음으로 Redis로 규모 확장을 지원 하기 위해 채팅 응용 프로그램을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-144">Next, we'll modify the chat application to support scaleout with Redis.</span></span> <span data-ttu-id="dc540-145">먼저 프로젝트에 SignalR.Redis NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-145">First, add the SignalR.Redis NuGet package to your project.</span></span> <span data-ttu-id="dc540-146">Visual Studio에서에서 합니다 **도구** 메뉴에서 **NuGet 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-146">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="dc540-147">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-147">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample5.ps1)]

<span data-ttu-id="dc540-148">다음으로 Global.asax 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-148">Next, open the Global.asax file.</span></span> <span data-ttu-id="dc540-149">다음 코드를 추가 합니다 **응용 프로그램\_시작** 메서드:</span><span class="sxs-lookup"><span data-stu-id="dc540-149">Add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample6.cs)]

- <span data-ttu-id="dc540-150">"server"는 Redis를 실행 하는 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-150">"server" is the name of the server that is running Redis.</span></span>
- <span data-ttu-id="dc540-151">*포트* 는 포트 번호</span><span class="sxs-lookup"><span data-stu-id="dc540-151">*port* is the port number</span></span>
- <span data-ttu-id="dc540-152">"password"는 redis.conf 파일에 정의 된 암호가입니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-152">"password" is the password that you defined in the redis.conf file.</span></span>
- <span data-ttu-id="dc540-153">"AppName"는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-153">"AppName" is any string.</span></span> <span data-ttu-id="dc540-154">SignalR이이 이름을 가진 Redis pub/sub 채널을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-154">SignalR creates a Redis pub/sub channel with this name.</span></span>

<span data-ttu-id="dc540-155">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="dc540-155">For example:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample7.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="dc540-156">배포 하 고 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="dc540-156">Deploy and Run the Application</span></span>

<span data-ttu-id="dc540-157">SignalR 응용 프로그램을 배포 하려면 Windows Server 인스턴스를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-157">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="dc540-158">IIS 역할을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-158">Add the IIS role.</span></span> <span data-ttu-id="dc540-159">WebSocket 프로토콜을 포함 하 여 "응용 프로그램 개발" 기능을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-159">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-redis/_static/image5.png)

<span data-ttu-id="dc540-160">관리 서비스 ("관리 도구" 아래)를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-160">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-redis/_static/image6.png)

<span data-ttu-id="dc540-161">**설치 웹 배포 3.0.**</span><span class="sxs-lookup"><span data-stu-id="dc540-161">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="dc540-162">IIS 관리자를 실행 하면, Microsoft 웹 플랫폼을 설치 하 라는 메시지가 나타납니다 것 또는 할 수 있습니다 [다운로드를 intstaller](https://go.microsoft.com/fwlink/?LinkId=255386)합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-162">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the intstaller](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="dc540-163">플랫폼 설치 관리자에서 웹 배포에 대 한 검색 하 고 웹 배포 3.0 설치</span><span class="sxs-lookup"><span data-stu-id="dc540-163">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-redis/_static/image7.png)

<span data-ttu-id="dc540-164">Web Management Service가 실행 중인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-164">Check that the Web Management Service is running.</span></span> <span data-ttu-id="dc540-165">그렇지 않은 경우 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-165">If not, start the service.</span></span> <span data-ttu-id="dc540-166">(웹 관리 서비스 Windows 서비스 목록에 보이지 않으면 확인 IIS 역할을 추가 했을 때 Management 서비스를 설치 합니다.)</span><span class="sxs-lookup"><span data-stu-id="dc540-166">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="dc540-167">기본적으로 웹 관리 서비스 8172 TCP 포트에서 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-167">By default, the Web Management Service listens on TCP port 8172.</span></span> <span data-ttu-id="dc540-168">Windows 방화벽에서 8172 포트의 TCP 트래픽을 허용 하는 새 인바운드 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-168">In Windows Firewall, create a new inbound rule to allow TCP traffic on port 8172.</span></span> <span data-ttu-id="dc540-169">자세한 내용은 [방화벽 규칙 구성](https://technet.microsoft.com/library/dd448559(WS.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-169">For more information, see [Configuring Firewall Rules](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span></span> <span data-ttu-id="dc540-170">(Azure에서 Vm을 호스트 하는 경우 이렇게 하려면 Azure portal에서 직접.</span><span class="sxs-lookup"><span data-stu-id="dc540-170">(If you are hosting the VMs on Azure, you can do this directly in the Azure portal.</span></span> <span data-ttu-id="dc540-171">참조 [Virtual Machine에 끝점을 설정 하는 방법](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)</span><span class="sxs-lookup"><span data-stu-id="dc540-171">See [How to Set Up Endpoints to a Virtual Machine](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)</span></span>

<span data-ttu-id="dc540-172">이제 서버에 개발 컴퓨터에서 Visual Studio 프로젝트를 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-172">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="dc540-173">솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-173">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="dc540-174">자세한 내용을 보려면 웹 배포에 대 한 설명서를 참조 하세요 [Visual Studio 및 ASP.NET 웹 배포 콘텐츠 맵](../../../whitepapers/aspnet-web-deployment-content-map.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-174">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="dc540-175">두 명의 서버 응용 프로그램을 배포 하는 경우에 별도 브라우저 창에서 각 인스턴스를 엽니다 하 고 다른에서 SignalR 메시지를 받을 각각 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-175">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="dc540-176">(물론 프로덕션 환경에서 두 서버는 sit 부하 분산 합니다.)</span><span class="sxs-lookup"><span data-stu-id="dc540-176">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-redis/_static/image8.png)

<span data-ttu-id="dc540-177">원하는 경우 사용할 수 있습니다, Redis로 전송 되는 메시지를 볼 수는 **redis cli** 클라이언트를 Redis를 사용 하 여 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc540-177">If you're curious to see the messages that are sent to Redis, you can use the **redis-cli** client, which installs with Redis.</span></span>

[!code-xml[Main](scaleout-with-redis/samples/sample8.xml)]

![](scaleout-with-redis/_static/image9.png)
