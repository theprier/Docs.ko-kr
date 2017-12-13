---
uid: signalr/overview/performance/scaleout-with-redis
title: "Redis와 함께 SignalR 확장 | Microsoft Docs"
author: MikeWasson
description: "이전 버전의에 대 한 내용은이 항목의 버전 2 이전 버전을 Visual Studio 2013.NET 4.5 SignalR이이 항목에서 사용 하는 소프트웨어 버전 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: 6ecd08c1-e364-4cd7-ad4c-806521911585
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/performance/scaleout-with-redis
msc.type: authoredcontent
ms.openlocfilehash: 965c32a4e2f2c9c4bd457d0c13ae99c1378c22c9
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="signalr-scaleout-with-redis"></a><span data-ttu-id="983d0-103">Redis와 함께 SignalR 확장</span><span class="sxs-lookup"><span data-stu-id="983d0-103">SignalR Scaleout with Redis</span></span>
====================
<span data-ttu-id="983d0-104">여 [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="983d0-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="983d0-105">이 항목에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="983d0-105">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="983d0-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="983d0-106">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="983d0-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="983d0-107">.NET 4.5</span></span>
> - <span data-ttu-id="983d0-108">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="983d0-108">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="983d0-109">이 항목의 이전 버전</span><span class="sxs-lookup"><span data-stu-id="983d0-109">Previous versions of this topic</span></span>
> 
> <span data-ttu-id="983d0-110">이전 버전의 SignalR에 대 한 정보를 참조 하십시오. [SignalR 이전 버전](../older-versions/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="983d0-111">질문이 나 의견이</span><span class="sxs-lookup"><span data-stu-id="983d0-111">Questions and comments</span></span>
> 
> <span data-ttu-id="983d0-112">이 자습서를 연결 하는 방법 및 페이지의 맨 아래에 주석에서 향상 될 수 있습니다 어떻게에 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="983d0-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="983d0-113">자습서를 직접 관련 되지 않는 질문 해야 하도록를 게시할 수 있습니다는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


<span data-ttu-id="983d0-114">이 자습서를 사용 하 여 [Redis](http://redis.io/) 두 개의 별도 IIS 인스턴스에 배포 하는 SignalR 응용 프로그램 간에 메시지를 분산 합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-114">In this tutorial, you will use [Redis](http://redis.io/) to distribute messages across a SignalR application that is deployed on two separate IIS instances.</span></span>

<span data-ttu-id="983d0-115">Redis는 메모리에 키-값 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-115">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="983d0-116">또한 게시/구독 모델을 사용 하는 메시징 시스템을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-116">It also supports a messaging system with a publish/subscribe model.</span></span> <span data-ttu-id="983d0-117">SignalR Redis 백플레인에서 다른 서버로 메시지를 전달 하는 pub/sub 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-117">The SignalR Redis backplane uses the pub/sub feature to forward messages to other servers.</span></span>

![](scaleout-with-redis/_static/image1.png)

<span data-ttu-id="983d0-118">이 자습서에서는 세 명의 서버를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-118">For this tutorial, you will use three servers:</span></span>

- <span data-ttu-id="983d0-119">SignalR 응용 프로그램을 배포 하는 데 사용할 수 있는 Windows를 실행 하는 두 개의 서버</span><span class="sxs-lookup"><span data-stu-id="983d0-119">Two servers running Windows, which you will use to deploy a SignalR application.</span></span>
- <span data-ttu-id="983d0-120">서버를 하나 사용 하는 Redis를 실행 하는 Linux를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-120">One server running Linux, which you will use to run Redis.</span></span> <span data-ttu-id="983d0-121">이 자습서에서 스크린 샷에 대 한 Ubuntu 12.04 TLS를 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-121">For the screenshots in this tutorial, I used Ubuntu 12.04 TLS.</span></span>

<span data-ttu-id="983d0-122">사용 하는 세 명의 물리적 서버를 설정 하지 않은 경우에 Hyper-v에서 Vm을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-122">If you don't have three physical servers to use, you can create VMs on Hyper-V.</span></span> <span data-ttu-id="983d0-123">두 번째 방법은 Azure에서 Vm을 만들려고 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-123">Another option is to create VMs on Azure.</span></span>

<span data-ttu-id="983d0-124">이 자습서에서는 공식 Redis 구현 하지만 이기도 한 [Windows Redis 포트](https://github.com/MSOpenTech/redis) MSOpenTech에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-124">Although this tutorial uses the official Redis implementation, there is also a [Windows port of Redis](https://github.com/MSOpenTech/redis) from MSOpenTech.</span></span> <span data-ttu-id="983d0-125">설치 및 구성 하는 다르지만 그렇지 않은 경우 단계는 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-125">Setup and configuration are different, but otherwise the steps are the same.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="983d0-126">SignalR 확장 Redis와 함께 Redis 클러스터를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-126">SignalR scaleout with Redis does not support Redis clusters.</span></span>


## <a name="overview"></a><span data-ttu-id="983d0-127">개요</span><span class="sxs-lookup"><span data-stu-id="983d0-127">Overview</span></span>

<span data-ttu-id="983d0-128">자세한 자습서에 들어가기 전에 수행할 작업의 간략 한 개요는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-128">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="983d0-129">Redis를 설치 하 고 Redis 서버를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-129">Install Redis and start the Redis server.</span></span>
2. <span data-ttu-id="983d0-130">응용 프로그램에 이러한 NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-130">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="983d0-131">Microsoft.AspNet.SignalR</span><span class="sxs-lookup"><span data-stu-id="983d0-131">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="983d0-132">Microsoft.AspNet.SignalR.Redis</span><span class="sxs-lookup"><span data-stu-id="983d0-132">Microsoft.AspNet.SignalR.Redis</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR.Redis)
3. <span data-ttu-id="983d0-133">SignalR 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-133">Create a SignalR application.</span></span>
4. <span data-ttu-id="983d0-134">백플레인에서 구성 하려면 Startup.cs에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-134">Add the following code to Startup.cs to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-redis/samples/sample1.cs)]

## <a name="ubuntu-on-hyper-v"></a><span data-ttu-id="983d0-135">Hyper-v의 Ubuntu</span><span class="sxs-lookup"><span data-stu-id="983d0-135">Ubuntu on Hyper-V</span></span>

<span data-ttu-id="983d0-136">Windows Hyper-v를 사용 하 여 Windows Server에서 Ubuntu VM을 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-136">Using Windows Hyper-V, you can easily create an Ubuntu VM on Windows Server.</span></span>

<span data-ttu-id="983d0-137">Ubuntu ISO를 다운로드 [http://www.ubuntu.com](http://www.ubuntu.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-137">Download the Ubuntu ISO from [http://www.ubuntu.com](http://www.ubuntu.com/).</span></span>

<span data-ttu-id="983d0-138">Hyper-v, 새 VM을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-138">In Hyper-V, add a new VM.</span></span> <span data-ttu-id="983d0-139">에 **가상 하드 디스크 연결** 단계에서는 **가상 하드 디스크 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-139">In the **Connect Virtual Hard Disk** step, select **Create a virtual hard disk**.</span></span>

![](scaleout-with-redis/_static/image2.png)

<span data-ttu-id="983d0-140">에 **설치 옵션** 단계에서는 **이미지 파일 (.iso)**, 클릭 **찾아보기**, Ubuntu 설치 ISO 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-140">In the **Installation Options** step, select **Image file (.iso)**, click **Browse**, and browse to the Ubuntu installation ISO.</span></span>

![](scaleout-with-redis/_static/image3.png)

## <a name="install-redis"></a><span data-ttu-id="983d0-141">Redis를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-141">Install Redis</span></span>

<span data-ttu-id="983d0-142">단계에 따라 [http://redis.io/download](http://redis.io/download) 다운로드 하 고 Redis를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-142">Follow the steps at [http://redis.io/download](http://redis.io/download) to download and build Redis.</span></span>

[!code-console[Main](scaleout-with-redis/samples/sample2.cmd)]

<span data-ttu-id="983d0-143">Redis 이진 파일에서 빌드이 고 `src` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-143">This builds the Redis binaries in the `src` directory.</span></span>

<span data-ttu-id="983d0-144">기본적으로 Redis에 암호가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-144">By default, Redis does not require a password.</span></span> <span data-ttu-id="983d0-145">암호를 설정 하려면 편집는 `redis.conf` 소스 코드의 루트 디렉터리에 있는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-145">To set a password, edit the `redis.conf` file, which is located in the root directory of the source code.</span></span> <span data-ttu-id="983d0-146">(편집 하기 전에 파일의 백업 복사본을 만듭니다.) 다음 지시문을 추가 `redis.conf`:</span><span class="sxs-lookup"><span data-stu-id="983d0-146">(Make a backup copy of the file before you edit it!) Add the following directive to `redis.conf`:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample3.ps1)]

<span data-ttu-id="983d0-147">Redis 서버를 지금 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-147">Now start the Redis server:</span></span>

[!code-css[Main](scaleout-with-redis/samples/sample4.css)]

![](scaleout-with-redis/_static/image4.png)

<span data-ttu-id="983d0-148">열린 포트 6379, Redis는 기본 포트에서 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-148">Open port 6379, which is the default port that Redis listens on.</span></span> <span data-ttu-id="983d0-149">(구성 파일에서 포트 번호를 변경할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="983d0-149">(You can change the port number in the configuration file.)</span></span>

## <a name="create-the-signalr-application"></a><span data-ttu-id="983d0-150">SignalR 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="983d0-150">Create the SignalR Application</span></span>

<span data-ttu-id="983d0-151">이러한 자습서 중 하나를 수행 하 여 SignalR 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-151">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="983d0-152">SignalR 2.0 시작</span><span class="sxs-lookup"><span data-stu-id="983d0-152">Getting Started with SignalR 2.0</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="983d0-153">SignalR 2.0 및 MVC 5 시작</span><span class="sxs-lookup"><span data-stu-id="983d0-153">Getting Started with SignalR 2.0 and MVC 5</span></span>](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

<span data-ttu-id="983d0-154">다음으로, Redis와 함께 확장을 지원 하도록 채팅 응용 프로그램을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-154">Next, we'll modify the chat application to support scaleout with Redis.</span></span> <span data-ttu-id="983d0-155">먼저 프로젝트에 SignalR.Redis NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-155">First, add the SignalR.Redis NuGet package to your project.</span></span> <span data-ttu-id="983d0-156">Visual Studio에서에서 **도구** 메뉴 선택 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-156">In Visual Studio, from the **Tools** menu, select **Library Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="983d0-157">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-157">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample5.ps1)]

<span data-ttu-id="983d0-158">다음으로 Startup.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-158">Next, open the Startup.cs file.</span></span> <span data-ttu-id="983d0-159">다음 코드를 추가 하는 **구성** 메서드:</span><span class="sxs-lookup"><span data-stu-id="983d0-159">Add the following code to the **Configuration** method:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample6.cs)]

- <span data-ttu-id="983d0-160">"서버"는 Redis를 실행 하는 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-160">"server" is the name of the server that is running Redis.</span></span>
- <span data-ttu-id="983d0-161">*포트* 는 포트 번호</span><span class="sxs-lookup"><span data-stu-id="983d0-161">*port* is the port number</span></span>
- <span data-ttu-id="983d0-162">"p"는 redis.conf 파일에 정의 된 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-162">"password" is the password that you defined in the redis.conf file.</span></span>
- <span data-ttu-id="983d0-163">"응용 프로그램 이름"은 모든 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-163">"AppName" is any string.</span></span> <span data-ttu-id="983d0-164">SignalR이이 이름을 가진 Redis pub/sub 채널을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-164">SignalR creates a Redis pub/sub channel with this name.</span></span>

<span data-ttu-id="983d0-165">예:</span><span class="sxs-lookup"><span data-stu-id="983d0-165">For example:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample7.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="983d0-166">배포 및 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="983d0-166">Deploy and Run the Application</span></span>

<span data-ttu-id="983d0-167">SignalR 응용 프로그램을 배포 하 여 Windows Server 인스턴스를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-167">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="983d0-168">IIS 역할을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-168">Add the IIS role.</span></span> <span data-ttu-id="983d0-169">WebSocket 프로토콜을 포함 하 여 "응용 프로그램 개발" 기능을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-169">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-redis/_static/image5.png)

<span data-ttu-id="983d0-170">관리 서비스 ("관리 도구" 아래에 나열)도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-170">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-redis/_static/image6.png)

<span data-ttu-id="983d0-171">**설치 웹 배포 3.0.**</span><span class="sxs-lookup"><span data-stu-id="983d0-171">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="983d0-172">IIS 관리자를 실행 하면, Microsoft 웹 플랫폼 설치를 묻습니다 또는 할 수 있습니다 때 [는 intstaller 다운로드](https://go.microsoft.com/fwlink/?LinkId=255386)합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-172">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the intstaller](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="983d0-173">플랫폼 설치 관리자에서 웹 배포를 검색 하 고 웹 배포 3.0 설치</span><span class="sxs-lookup"><span data-stu-id="983d0-173">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-redis/_static/image7.png)

<span data-ttu-id="983d0-174">웹 관리 서비스에서 실행 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-174">Check that the Web Management Service is running.</span></span> <span data-ttu-id="983d0-175">그렇지 않은 경우 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-175">If not, start the service.</span></span> <span data-ttu-id="983d0-176">(웹 관리 서비스 보이지 않으면의 Windows 서비스 목록에 있는지 확인 IIS 역할을 추가 했을 때 관리 서비스를 설치 합니다.)</span><span class="sxs-lookup"><span data-stu-id="983d0-176">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="983d0-177">웹 관리 서비스는 기본적으로 TCP 8172 포트에서 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-177">By default, the Web Management Service listens on TCP port 8172.</span></span> <span data-ttu-id="983d0-178">Windows 방화벽에서 TCP 8172 포트 트래픽을 허용 하는 새 인바운드 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-178">In Windows Firewall, create a new inbound rule to allow TCP traffic on port 8172.</span></span> <span data-ttu-id="983d0-179">자세한 내용은 참조 [방화벽 규칙 구성](https://technet.microsoft.com/en-us/library/dd448559(WS.10).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-179">For more information, see [Configuring Firewall Rules](https://technet.microsoft.com/en-us/library/dd448559(WS.10).aspx).</span></span> <span data-ttu-id="983d0-180">(Azure에서 Vm을 호스팅하는 경우 이렇게 하려면 Azure 포털에서 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-180">(If you are hosting the VMs on Azure, you can do this directly in the Azure portal.</span></span> <span data-ttu-id="983d0-181">참조 [가상 컴퓨터에 끝점을 설정 하는 방법을](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-set-up-endpoints/).)</span><span class="sxs-lookup"><span data-stu-id="983d0-181">See [How to Set Up Endpoints to a Virtual Machine](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-set-up-endpoints/).)</span></span>

<span data-ttu-id="983d0-182">이제 서버에 개발 컴퓨터에서 Visual Studio 프로젝트를 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-182">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="983d0-183">솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-183">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="983d0-184">웹 배포에 대 한 설명서 보다 자세한 참조 [Visual Studio 및 ASP.NET에 대 한 웹 배포 콘텐츠 맵](../../../whitepapers/aspnet-web-deployment-content-map.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-184">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="983d0-185">두 명의 서버에 응용 프로그램을 배포 하는 경우 각 인스턴스는 별도 브라우저 창에서 열고 하 고 다른에서 SignalR 메시지를 받을 구성 파일은 각각을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-185">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="983d0-186">(물론, 프로덕션 환경에서 두 서버는 sit 부하 분산 장치 뒤.)</span><span class="sxs-lookup"><span data-stu-id="983d0-186">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-redis/_static/image8.png)

<span data-ttu-id="983d0-187">내용은로 보내지는 Redis를 사용할 수 있습니다 메시지를 볼 수는 **redis cli** Redis와 함께 설치 된 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="983d0-187">If you're curious to see the messages that are sent to Redis, you can use the **redis-cli** client, which installs with Redis.</span></span>

[!code-xml[Main](scaleout-with-redis/samples/sample8.xml)]

![](scaleout-with-redis/_static/image9.png)
