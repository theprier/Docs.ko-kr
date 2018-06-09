---
uid: signalr/overview/performance/scaleout-with-windows-azure-service-bus
title: Azure 서비스 버스에 SignalR 확장 | Microsoft Docs
author: MikeWasson
description: 이 항목 Visual Studio 2013.NET 4.5 SignalR 버전에서는이 항목의이 항목에 대 한 SignalR 1.x 버전의 이전 버전 2 사용 하는 소프트웨어 버전 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: ce1305f9-30fd-49e3-bf38-d0a78dfb06c3
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/performance/scaleout-with-windows-azure-service-bus
msc.type: authoredcontent
ms.openlocfilehash: e6d9e4e6ba2040aa2c6e453aacf0ddca38c4a1a9
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2018
ms.locfileid: "32741542"
---
<a name="signalr-scaleout-with-azure-service-bus"></a><span data-ttu-id="b8f37-103">Azure 서비스 버스에 SignalR 확장</span><span class="sxs-lookup"><span data-stu-id="b8f37-103">SignalR Scaleout with Azure Service Bus</span></span>
====================
<span data-ttu-id="b8f37-104">여 [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="b8f37-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

<span data-ttu-id="b8f37-105">이 자습서에서는 서비스 버스 백플레인에서 사용 하 여 메시지를 각 역할 인스턴스에 배포 하는 Windows Azure 웹 역할에는 SignalR 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-105">In this tutorial, you will deploy a SignalR application to a Windows Azure Web Role, using the Service Bus backplane to distribute messages to each role instance.</span></span> <span data-ttu-id="b8f37-106">(서비스 버스 백플레인을 사용할 수도 있습니다 [웹 Azure 앱 서비스의 앱](https://docs.microsoft.com/azure/app-service-web/).)</span><span class="sxs-lookup"><span data-stu-id="b8f37-106">(You can also use the Service Bus backplane with [web apps in Azure App Service](https://docs.microsoft.com/azure/app-service-web/).)</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image1.png)

<span data-ttu-id="b8f37-107">필수 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="b8f37-107">Prerequisites:</span></span>

- <span data-ttu-id="b8f37-108">Windows Azure 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-108">A Windows Azure account.</span></span>
- <span data-ttu-id="b8f37-109">[Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-109">The [Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).</span></span>
- <span data-ttu-id="b8f37-110">Visual Studio 2012 또는 2013입니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-110">Visual Studio 2012 or 2013.</span></span>

<span data-ttu-id="b8f37-111">서비스 버스 백플레인에서 호환 이기도 [Service Bus for Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx), 버전 1.1.</span><span class="sxs-lookup"><span data-stu-id="b8f37-111">The service bus backplane is also compatible with [Service Bus for Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx), version 1.1.</span></span> <span data-ttu-id="b8f37-112">그러나 Service Bus for Windows Server의 버전 1.0과 호환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-112">However, it is not compatible with version 1.0 of Service Bus for Windows Server.</span></span>

## <a name="pricing"></a><span data-ttu-id="b8f37-113">가격</span><span class="sxs-lookup"><span data-stu-id="b8f37-113">Pricing</span></span>

<span data-ttu-id="b8f37-114">서비스 버스 백플레인에서 항목을 사용 하 여 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-114">The Service Bus backplane uses topics to send messages.</span></span> <span data-ttu-id="b8f37-115">최신 가격 정보에 대 한 참조 [서비스 버스](https://azure.microsoft.com/pricing/details/service-bus/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-115">For the latest pricing information, see [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).</span></span> <span data-ttu-id="b8f37-116">이 문서 작성 당시의 1 달러 매달 1000000 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-116">At the time of this writing, you can send 1,000,000 messages per month for less than $1.</span></span> <span data-ttu-id="b8f37-117">백플레인에서 각 SignalR 허브 메서드 호출에 대해 서비스 버스 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-117">The backplane sends a service bus message for each invocation of a SignalR hub method.</span></span> <span data-ttu-id="b8f37-118">연결, 연결 끊김, 그룹 및 기타 조인 또는 종료에 대 한 일부 제어 메시지도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-118">There are also some control messages for connections, disconnections, joining or leaving groups, and so forth.</span></span> <span data-ttu-id="b8f37-119">대부분의 응용 프로그램에서 대부분의 메시지 트래픽 허브 메서드 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-119">In most applications, the majority of the message traffic will be hub method invocations.</span></span>

## <a name="overview"></a><span data-ttu-id="b8f37-120">개요</span><span class="sxs-lookup"><span data-stu-id="b8f37-120">Overview</span></span>

<span data-ttu-id="b8f37-121">자세한 자습서에 들어가기 전에 수행할 작업의 간략 한 개요는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-121">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="b8f37-122">Windows Azure 포털을 사용 하 여 새 서비스 버스 네임 스페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-122">Use the Windows Azure portal to create a new Service Bus namespace.</span></span>
2. <span data-ttu-id="b8f37-123">응용 프로그램에 이러한 NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-123">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="b8f37-124">Microsoft.AspNet.SignalR</span><span class="sxs-lookup"><span data-stu-id="b8f37-124">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - <span data-ttu-id="b8f37-125">[Microsoft.AspNet.SignalR.ServiceBus3](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3) 또는 [Microsoft.AspNet.SignalR.ServiceBus](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus)</span><span class="sxs-lookup"><span data-stu-id="b8f37-125">[Microsoft.AspNet.SignalR.ServiceBus3](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3) or [Microsoft.AspNet.SignalR.ServiceBus](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus)</span></span>
3. <span data-ttu-id="b8f37-126">SignalR 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-126">Create a SignalR application.</span></span>
4. <span data-ttu-id="b8f37-127">백플레인에서 구성 하려면 Startup.cs에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-127">Add the following code to Startup.cs to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample1.cs)]

<span data-ttu-id="b8f37-128">이 코드에 대 한 기본 값으로 백플레인에서 구성 [TopicCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.servicebusscaleoutconfiguration.topiccount(v=vs.118).aspx) 및 [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-128">This code configures the backplane with the default values for [TopicCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.servicebusscaleoutconfiguration.topiccount(v=vs.118).aspx) and [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx).</span></span> <span data-ttu-id="b8f37-129">변경 된 이러한 값에 대 한 정보를 참조 하십시오. [SignalR 성능: 확장 메트릭](signalr-performance.md#scaleout_metrics)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-129">For information on changing these values, see [SignalR Performance: Scaleout Metrics](signalr-performance.md#scaleout_metrics).</span></span>

<span data-ttu-id="b8f37-130">각 응용 프로그램에 대 한 "앱 이름"에 대 한 다른 값을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-130">For each application, pick a different value for "YourAppName".</span></span> <span data-ttu-id="b8f37-131">여러 응용 프로그램에서 동일한 값을 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="b8f37-131">Do not use the same value across multiple applications.</span></span>

## <a name="create-the-azure-services"></a><span data-ttu-id="b8f37-132">Azure 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="b8f37-132">Create the Azure Services</span></span>

<span data-ttu-id="b8f37-133">에 설명 된 대로 클라우드 서비스를 만드는 [만들어 클라우드 서비스를 배포 하는 방법을](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-133">Create a Cloud Service, as described in [How to Create and Deploy a Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span></span> <span data-ttu-id="b8f37-134">섹션의 단계에 따라 "방법: 빠른 생성을 사용 하 여 클라우드 서비스 만들기"입니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-134">Follow the steps in the section "How to: Create a cloud service using Quick Create".</span></span> <span data-ttu-id="b8f37-135">이 자습서에 대 한 인증서를 업로드할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-135">For this tutorial, you do not need to upload a certificate.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image2.png)

<span data-ttu-id="b8f37-136">에 설명 된 대로 새 서비스 버스 네임 스페이스 만들기 [사용 하 여 서비스 버스 항목/구독 하는 방법을](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-136">Create a new Service Bus namespace, as described in [How to Use Service Bus Topics/Subscriptions](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions).</span></span> <span data-ttu-id="b8f37-137">"서비스 Namespace 만들기" 섹션의 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-137">Follow the steps in the section "Create a Service Namespace".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="b8f37-138">클라우드 서비스 및 서비스 버스 네임 스페이스에 대 한 동일한 지역을 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-138">Make sure to select the same region for the cloud service and the Service Bus namespace.</span></span>


## <a name="create-the-visual-studio-project"></a><span data-ttu-id="b8f37-139">Visual Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="b8f37-139">Create the Visual Studio Project</span></span>

<span data-ttu-id="b8f37-140">Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-140">Start Visual Studio.</span></span> <span data-ttu-id="b8f37-141">**파일** 메뉴를 클릭 하 여 **새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-141">From the **File** menu, click **New Project**.</span></span>

<span data-ttu-id="b8f37-142">에 **새 프로젝트** 대화 상자에서 **Visual C#** 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-142">In the **New Project** dialog box, expand **Visual C#**.</span></span> <span data-ttu-id="b8f37-143">아래 **설치 된 템플릿**선택, **클라우드** 선택한 후 **Windows Azure 클라우드 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-143">Under **Installed Templates**, select **Cloud** and then select **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="b8f37-144">기본.NET Framework 4.5를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-144">Keep the default .NET Framework 4.5.</span></span> <span data-ttu-id="b8f37-145">ChatService 응용 프로그램 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-145">Name the application ChatService and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image4.png)

<span data-ttu-id="b8f37-146">에 **새 Windows Azure 클라우드 서비스** 대화 상자에서 ASP.NET 웹 역할을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-146">In the **New Windows Azure Cloud Service** dialog, select ASP.NET Web Role.</span></span> <span data-ttu-id="b8f37-147">오른쪽 화살표 단추를 클릭 (**&gt;**) 솔루션에 역할을 추가 하려면.</span><span class="sxs-lookup"><span data-stu-id="b8f37-147">Click the right-arrow button (**&gt;**) to add the role to your solution.</span></span>

<span data-ttu-id="b8f37-148">따라서 새 역할 위로 마우스를 가져가고 연필 아이콘을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-148">Hover the mouse over the new role, so the pencil icon visible.</span></span> <span data-ttu-id="b8f37-149">역할의 이름을 바꾸려면이 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-149">Click this icon to rename the role.</span></span> <span data-ttu-id="b8f37-150">"SignalRChat" 역할 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-150">Name the role "SignalRChat" and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image5.png)

<span data-ttu-id="b8f37-151">에 **새 ASP.NET 프로젝트** 대화 상자에서 **MVC**, 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-151">In the **New ASP.NET Project** dialog, select **MVC**, and click OK.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image6.png)

<span data-ttu-id="b8f37-152">프로젝트 마법사에서 두 개의 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-152">The project wizard creates two projects:</span></span>

- <span data-ttu-id="b8f37-153">ChatService:이 프로젝트는 Windows Azure 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="b8f37-153">ChatService: This project is the Windows Azure application.</span></span> <span data-ttu-id="b8f37-154">Azure 역할 및 기타 구성 옵션을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-154">It defines the Azure roles and other configuration options.</span></span>
- <span data-ttu-id="b8f37-155">SignalRChat:이 프로젝트는 ASP.NET MVC 5 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="b8f37-155">SignalRChat: This project is your ASP.NET MVC 5 project.</span></span>

## <a name="create-the-signalr-chat-application"></a><span data-ttu-id="b8f37-156">SignalR 채팅 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="b8f37-156">Create the SignalR Chat Application</span></span>

<span data-ttu-id="b8f37-157">채팅 응용 프로그램을 만들려면이 자습서의 단계를 따라 [시작 SignalR 및 MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-157">To create the chat application, follow the steps in the tutorial [Getting Started with SignalR and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<span data-ttu-id="b8f37-158">NuGet을 사용 하 여 필요한 라이브러리를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-158">Use NuGet to install the required libraries.</span></span> <span data-ttu-id="b8f37-159">**도구** 메뉴 선택 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-159">From the **Tools** menu, select **Library Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="b8f37-160">에 **패키지 관리자 콘솔** 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-160">In the **Package Manager Console** window, enter the following commands:</span></span>

[!code-powershell[Main](scaleout-with-windows-azure-service-bus/samples/sample2.ps1)]

<span data-ttu-id="b8f37-161">사용 하 여 `-ProjectName` Windows Azure 프로젝트를 사용 하지 않고 ASP.NET MVC 프로젝트에 패키지를 설치 하는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-161">Use the `-ProjectName` option to install the packages to the ASP.NET MVC project, rather than the Windows Azure project.</span></span>

## <a name="configure-the-backplane"></a><span data-ttu-id="b8f37-162">백플레인에서 구성</span><span class="sxs-lookup"><span data-stu-id="b8f37-162">Configure the Backplane</span></span>

<span data-ttu-id="b8f37-163">응용 프로그램의 Startup.cs 파일에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-163">In your application's Startup.cs file, add the following code:</span></span>

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample3.cs)]

<span data-ttu-id="b8f37-164">이제 서비스 버스 연결 문자열을 가져올 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-164">Now you need to get your service bus connection string.</span></span> <span data-ttu-id="b8f37-165">Azure 포털에서 만든 서비스 버스 네임 스페이스를 선택 하 고 선택 키 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-165">In the Azure portal, select the service bus namespace that you created and click the Access Key icon.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image7.png)

<span data-ttu-id="b8f37-166">클립보드에 연결 문자열을 복사한 다음에 붙여 넣습니다는 *connectionString* 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-166">Copy the connection string to the clipboard, then paste it into the *connectionString* variable.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image8.png)

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample4.cs)]

## <a name="deploy-to-azure"></a><span data-ttu-id="b8f37-167">Azure에 배포</span><span class="sxs-lookup"><span data-stu-id="b8f37-167">Deploy to Azure</span></span>

<span data-ttu-id="b8f37-168">솔루션 탐색기에서 확장 된 **역할** ChatService 프로젝트 내의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-168">In Solution Explorer, expand the **Roles** folder inside the ChatService project.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image9.png)

<span data-ttu-id="b8f37-169">SignalRChat 역할을 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-169">Right-click the SignalRChat role and select **Properties**.</span></span> <span data-ttu-id="b8f37-170">선택 된 **구성** 탭 합니다. 아래 **인스턴스** 2를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-170">Select the **Configuration** tab. Under **Instances** select 2.</span></span> <span data-ttu-id="b8f37-171">VM 크기 설정할 수도 있습니다 **매우 작음으로**합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-171">You can also set the VM size to **Extra Small**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image10.png)

<span data-ttu-id="b8f37-172">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-172">Save the changes.</span></span>

<span data-ttu-id="b8f37-173">솔루션 탐색기에서 ChatService 프로젝트를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-173">In Solution Explorer, right-click the ChatService project.</span></span> <span data-ttu-id="b8f37-174">**게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-174">Select **Publish**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image11.png)

<span data-ttu-id="b8f37-175">프로그램 첫 번째 시간 Windows Azure에 게시 인 경우 자격 증명을 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-175">If this is your first time publishing to Windows Azure, you must download your credentials.</span></span> <span data-ttu-id="b8f37-176">에 **게시** 마법사 "자격 증명을 다운로드 하려면 로그인"을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-176">In the **Publish** wizard, click "Sign in to download credentials".</span></span> <span data-ttu-id="b8f37-177">이 라는 Windows Azure 포털에 로그인 하 여 게시 설정 파일 다운로드 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-177">This will prompt you to sign into the Windows Azure portal and download a publish settings file.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image12.png)

<span data-ttu-id="b8f37-178">클릭 **가져오기** 하 고 다운로드 한 게시 설정 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-178">Click **Import** and select the publish settings file that you downloaded.</span></span>

<span data-ttu-id="b8f37-179">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-179">Click **Next**.</span></span> <span data-ttu-id="b8f37-180">에 **게시 설정** 대화에서 **클라우드 서비스**를 앞에서 만든 클라우드 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-180">In the **Publish Settings** dialog, under **Cloud Service**, select the cloud service that you created earlier.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image13.png)

<span data-ttu-id="b8f37-181">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-181">Click **Publish**.</span></span> <span data-ttu-id="b8f37-182">응용 프로그램을 배포 하 고 Vm을 시작 하는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-182">It can take a few minutes to deploy the application and start the VMs.</span></span>

<span data-ttu-id="b8f37-183">이제 채팅 응용 프로그램을 실행 하면 역할 인스턴스에 서비스 버스 항목을 사용 하 여 Azure 서비스 버스를 통해 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-183">Now when you run the chat application, the role instances communicate through Azure Service Bus, using a Service Bus topic.</span></span> <span data-ttu-id="b8f37-184">한 항목은 여러 구독자를 허용 하는 메시지 큐입니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-184">A topic is a message queue that allows multiple subscribers.</span></span>

<span data-ttu-id="b8f37-185">백플레인에서 항목 및 구독에 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-185">The backplane automatically creates the topic and the subscriptions.</span></span> <span data-ttu-id="b8f37-186">구독 및 메시지 활동을 보려면 Azure 포털을 열고 서비스 버스 네임 스페이스 선택한 "항목"을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-186">To see the subscriptions and message activity, open the Azure portal, select the Service Bus namespace, and click on "Topics".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image14.png)

<span data-ttu-id="b8f37-187">대시보드에 표시 메시지 활동에 대 일 분 정도 걸릴 것으로 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-187">It make take a few minutes for the message activity to show up in the dashboard.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image15.png)

<span data-ttu-id="b8f37-188">SignalR 항목 수명을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-188">SignalR manages the topic lifetime.</span></span> <span data-ttu-id="b8f37-189">응용 프로그램을 배포한으로 수동으로 항목을 삭제 하거나 항목의 설정을 변경 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="b8f37-189">As long as your application is deployed, don't try to manually delete topics or change settings on the topic.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b8f37-190">문제 해결</span><span class="sxs-lookup"><span data-stu-id="b8f37-190">Troubleshooting</span></span>

<span data-ttu-id="b8f37-191">**System.InvalidOperationException "만 지원 되는 IsolationLevel 'IsolationLevel.Serializable'입니다."**</span><span class="sxs-lookup"><span data-stu-id="b8f37-191">**System.InvalidOperationException "The only supported IsolationLevel is 'IsolationLevel.Serializable'."**</span></span>

<span data-ttu-id="b8f37-192">이 오류는 작업에 대 한 트랜잭션 수준을 아닌 다른 값으로 설정 되어 있으면 `Serializable`합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-192">This error can occur if the transaction level for an operation is set to something other than `Serializable`.</span></span> <span data-ttu-id="b8f37-193">작업은 다른 트랜잭션 수준으로 수행 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8f37-193">Verify that no operations are being performed with other transaction levels.</span></span>
