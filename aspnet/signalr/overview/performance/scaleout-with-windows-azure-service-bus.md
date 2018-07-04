---
uid: signalr/overview/performance/scaleout-with-windows-azure-service-bus
title: Azure Service Bus로 SignalR 규모 확장 | Microsoft Docs
author: MikeWasson
description: 소프트웨어 버전 2 이전 버전을이 항목에서는이 항목의 SignalR 1.x 버전의이 항목에서는 Visual Studio 2013.NET 4.5 SignalR 버전에서 사용 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: ce1305f9-30fd-49e3-bf38-d0a78dfb06c3
ms.technology: dotnet-signalr
msc.legacyurl: /signalr/overview/performance/scaleout-with-windows-azure-service-bus
msc.type: authoredcontent
ms.openlocfilehash: a9e5d59c1b9120a32fabe55b4864d861040bcd67
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37369152"
---
<a name="signalr-scaleout-with-azure-service-bus"></a><span data-ttu-id="ed44c-103">Azure Service Bus로 SignalR 규모 확장</span><span class="sxs-lookup"><span data-stu-id="ed44c-103">SignalR Scaleout with Azure Service Bus</span></span>
====================
<span data-ttu-id="ed44c-104">하 여 [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="ed44c-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

<span data-ttu-id="ed44c-105">이 자습서에서는 Service Bus 백플레인에서 사용 하 여 각 역할 인스턴스에 메시지를 분산 하는 Windows Azure 웹 역할에는 SignalR 응용 프로그램 배포.</span><span class="sxs-lookup"><span data-stu-id="ed44c-105">In this tutorial, you will deploy a SignalR application to a Windows Azure Web Role, using the Service Bus backplane to distribute messages to each role instance.</span></span> <span data-ttu-id="ed44c-106">(사용 하 여 Service Bus 백플레인에서 이용할 수 있습니다 [Azure App Service의 웹 앱](https://docs.microsoft.com/azure/app-service-web/).)</span><span class="sxs-lookup"><span data-stu-id="ed44c-106">(You can also use the Service Bus backplane with [web apps in Azure App Service](https://docs.microsoft.com/azure/app-service-web/).)</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image1.png)

<span data-ttu-id="ed44c-107">필수 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="ed44c-107">Prerequisites:</span></span>

- <span data-ttu-id="ed44c-108">Windows Azure 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-108">A Windows Azure account.</span></span>
- <span data-ttu-id="ed44c-109">합니다 [Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-109">The [Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).</span></span>
- <span data-ttu-id="ed44c-110">Visual Studio 2012 또는 2013입니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-110">Visual Studio 2012 or 2013.</span></span>

<span data-ttu-id="ed44c-111">Service bus 백플레인에서 호환 이기도 [Windows Server 용 Service Bus](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx), 버전 1.1입니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-111">The service bus backplane is also compatible with [Service Bus for Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx), version 1.1.</span></span> <span data-ttu-id="ed44c-112">그러나 Service Bus for Windows Server의 버전 1.0과 호환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-112">However, it is not compatible with version 1.0 of Service Bus for Windows Server.</span></span>

## <a name="pricing"></a><span data-ttu-id="ed44c-113">가격</span><span class="sxs-lookup"><span data-stu-id="ed44c-113">Pricing</span></span>

<span data-ttu-id="ed44c-114">Service Bus 백플레인에서 메시지를 보낼 항목을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-114">The Service Bus backplane uses topics to send messages.</span></span> <span data-ttu-id="ed44c-115">최신 가격 정보 참조 [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-115">For the latest pricing information, see [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).</span></span> <span data-ttu-id="ed44c-116">이 문서 작성 당시 1 달러 미만 매월 1,000,000 개의 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-116">At the time of this writing, you can send 1,000,000 messages per month for less than $1.</span></span> <span data-ttu-id="ed44c-117">백플레인에서는 SignalR 허브 메서드에 대 한 각 호출에 대 한 service bus 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-117">The backplane sends a service bus message for each invocation of a SignalR hub method.</span></span> <span data-ttu-id="ed44c-118">일부 제어 메시지 등에 대 한 연결, 연결 끊김, 조인 또는 그대로 유지 되어 그룹도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-118">There are also some control messages for connections, disconnections, joining or leaving groups, and so forth.</span></span> <span data-ttu-id="ed44c-119">대부분의 응용 프로그램에서 대부분의 메시지 트래픽 허브 메서드 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-119">In most applications, the majority of the message traffic will be hub method invocations.</span></span>

## <a name="overview"></a><span data-ttu-id="ed44c-120">개요</span><span class="sxs-lookup"><span data-stu-id="ed44c-120">Overview</span></span>

<span data-ttu-id="ed44c-121">자세한 자습서를 시작 하기 전에 수행할 작업의 간략 한 개요는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-121">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="ed44c-122">새 Service Bus 네임 스페이스를 만들려면 Windows Azure 포털을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-122">Use the Windows Azure portal to create a new Service Bus namespace.</span></span>
2. <span data-ttu-id="ed44c-123">응용 프로그램에 이러한 NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-123">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="ed44c-124">Microsoft.AspNet.SignalR</span><span class="sxs-lookup"><span data-stu-id="ed44c-124">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - <span data-ttu-id="ed44c-125">[Microsoft.AspNet.SignalR.ServiceBus3](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3) 또는 [Microsoft.AspNet.SignalR.ServiceBus](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus)</span><span class="sxs-lookup"><span data-stu-id="ed44c-125">[Microsoft.AspNet.SignalR.ServiceBus3](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3) or [Microsoft.AspNet.SignalR.ServiceBus](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus)</span></span>
3. <span data-ttu-id="ed44c-126">SignalR 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-126">Create a SignalR application.</span></span>
4. <span data-ttu-id="ed44c-127">Startup.cs 백플레인에서 구성 하려면 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-127">Add the following code to Startup.cs to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample1.cs)]

<span data-ttu-id="ed44c-128">이 코드에 대 한 기본값을 사용 하 여 백플레인에서 구성 [TopicCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.servicebusscaleoutconfiguration.topiccount(v=vs.118).aspx) 하 고 [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-128">This code configures the backplane with the default values for [TopicCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.servicebusscaleoutconfiguration.topiccount(v=vs.118).aspx) and [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx).</span></span> <span data-ttu-id="ed44c-129">이러한 값을 변경에 대 한 내용은 참조 하세요 [SignalR 성능: 확장 메트릭](signalr-performance.md#scaleout_metrics)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-129">For information on changing these values, see [SignalR Performance: Scaleout Metrics](signalr-performance.md#scaleout_metrics).</span></span>

<span data-ttu-id="ed44c-130">각 응용 프로그램에 대 한 "응용 프로그램 이름"에 대 한 다른 값을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-130">For each application, pick a different value for "YourAppName".</span></span> <span data-ttu-id="ed44c-131">여러 응용 프로그램에서 동일한 값을 사용 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="ed44c-131">Do not use the same value across multiple applications.</span></span>

## <a name="create-the-azure-services"></a><span data-ttu-id="ed44c-132">Azure 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="ed44c-132">Create the Azure Services</span></span>

<span data-ttu-id="ed44c-133">에 설명 된 대로 클라우드 서비스를 만듭니다 [클라우드 서비스 만들기 및 배포 하는 방법을](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-133">Create a Cloud Service, as described in [How to Create and Deploy a Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span></span> <span data-ttu-id="ed44c-134">섹션의 단계에 따라 "방법: 빠른 생성을 사용 하 여 클라우드 서비스 만들기"입니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-134">Follow the steps in the section "How to: Create a cloud service using Quick Create".</span></span> <span data-ttu-id="ed44c-135">이 자습서에서는 인증서를 업로드할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-135">For this tutorial, you do not need to upload a certificate.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image2.png)

<span data-ttu-id="ed44c-136">에 설명 된 대로 새 Service Bus 네임 스페이스를 만듭니다 [방법을 사용 하 여 Service Bus 토픽/구독에](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions)입니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-136">Create a new Service Bus namespace, as described in [How to Use Service Bus Topics/Subscriptions](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions).</span></span> <span data-ttu-id="ed44c-137">"서비스 Namespace 만들기" 섹션의 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-137">Follow the steps in the section "Create a Service Namespace".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="ed44c-138">클라우드 서비스 및 Service Bus 네임 스페이스에 대 한 동일한 지역을 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-138">Make sure to select the same region for the cloud service and the Service Bus namespace.</span></span>


## <a name="create-the-visual-studio-project"></a><span data-ttu-id="ed44c-139">Visual Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="ed44c-139">Create the Visual Studio Project</span></span>

<span data-ttu-id="ed44c-140">Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-140">Start Visual Studio.</span></span> <span data-ttu-id="ed44c-141">**파일** 메뉴에서 클릭 **새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-141">From the **File** menu, click **New Project**.</span></span>

<span data-ttu-id="ed44c-142">에 **새 프로젝트** 대화 상자에서 **Visual C#** 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-142">In the **New Project** dialog box, expand **Visual C#**.</span></span> <span data-ttu-id="ed44c-143">아래 **설치 된 템플릿**를 선택 **클라우드** 선택한 후 **Windows Azure 클라우드 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-143">Under **Installed Templates**, select **Cloud** and then select **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="ed44c-144">기본.NET Framework 4.5를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-144">Keep the default .NET Framework 4.5.</span></span> <span data-ttu-id="ed44c-145">ChatService 응용 프로그램 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-145">Name the application ChatService and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image4.png)

<span data-ttu-id="ed44c-146">에 **새 Windows Azure 클라우드 서비스** 대화 상자에서 ASP.NET 웹 역할을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-146">In the **New Windows Azure Cloud Service** dialog, select ASP.NET Web Role.</span></span> <span data-ttu-id="ed44c-147">오른쪽 화살표 단추를 클릭 (**&gt;**) 솔루션에 역할을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-147">Click the right-arrow button (**&gt;**) to add the role to your solution.</span></span>

<span data-ttu-id="ed44c-148">따라서 새 역할 위로 마우스를 이동 연필 아이콘을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-148">Hover the mouse over the new role, so the pencil icon visible.</span></span> <span data-ttu-id="ed44c-149">역할 이름을 바꾸려면이 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-149">Click this icon to rename the role.</span></span> <span data-ttu-id="ed44c-150">"SignalRChat" 역할 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-150">Name the role "SignalRChat" and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image5.png)

<span data-ttu-id="ed44c-151">에 **새 ASP.NET 프로젝트** 대화 상자에서 **MVC**, 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-151">In the **New ASP.NET Project** dialog, select **MVC**, and click OK.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image6.png)

<span data-ttu-id="ed44c-152">프로젝트 마법사에서 두 개의 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-152">The project wizard creates two projects:</span></span>

- <span data-ttu-id="ed44c-153">ChatService:이 프로젝트는 Windows Azure 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="ed44c-153">ChatService: This project is the Windows Azure application.</span></span> <span data-ttu-id="ed44c-154">Azure 역할 및 기타 구성 옵션을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-154">It defines the Azure roles and other configuration options.</span></span>
- <span data-ttu-id="ed44c-155">SignalRChat:이 프로젝트는 ASP.NET MVC 5 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="ed44c-155">SignalRChat: This project is your ASP.NET MVC 5 project.</span></span>

## <a name="create-the-signalr-chat-application"></a><span data-ttu-id="ed44c-156">SignalR 채팅 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="ed44c-156">Create the SignalR Chat Application</span></span>

<span data-ttu-id="ed44c-157">채팅 응용 프로그램을 만들려면이 자습서의 단계를 따라 [SignalR 및 MVC 5 시작](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-157">To create the chat application, follow the steps in the tutorial [Getting Started with SignalR and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<span data-ttu-id="ed44c-158">필요한 라이브러리를 설치 하려면 NuGet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-158">Use NuGet to install the required libraries.</span></span> <span data-ttu-id="ed44c-159">**도구** 메뉴에서 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-159">From the **Tools** menu, select **Library Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="ed44c-160">에 **패키지 관리자 콘솔** 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-160">In the **Package Manager Console** window, enter the following commands:</span></span>

[!code-powershell[Main](scaleout-with-windows-azure-service-bus/samples/sample2.ps1)]

<span data-ttu-id="ed44c-161">사용 된 `-ProjectName` Windows Azure 프로젝트 보다는 ASP.NET MVC 프로젝트에 패키지를 설치 하는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-161">Use the `-ProjectName` option to install the packages to the ASP.NET MVC project, rather than the Windows Azure project.</span></span>

## <a name="configure-the-backplane"></a><span data-ttu-id="ed44c-162">백플레인에서 구성</span><span class="sxs-lookup"><span data-stu-id="ed44c-162">Configure the Backplane</span></span>

<span data-ttu-id="ed44c-163">응용 프로그램의 Startup.cs 파일에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-163">In your application's Startup.cs file, add the following code:</span></span>

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample3.cs)]

<span data-ttu-id="ed44c-164">이제 service bus 연결 문자열 가져오기 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-164">Now you need to get your service bus connection string.</span></span> <span data-ttu-id="ed44c-165">Azure portal에서 만든 service bus 네임 스페이스를 선택 하 고 액세스 키 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-165">In the Azure portal, select the service bus namespace that you created and click the Access Key icon.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image7.png)

<span data-ttu-id="ed44c-166">연결 문자열을 클립보드에 복사한 다음 붙여 넣습니다 합니다 *connectionString* 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-166">Copy the connection string to the clipboard, then paste it into the *connectionString* variable.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image8.png)

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample4.cs)]

## <a name="deploy-to-azure"></a><span data-ttu-id="ed44c-167">Azure에 배포</span><span class="sxs-lookup"><span data-stu-id="ed44c-167">Deploy to Azure</span></span>

<span data-ttu-id="ed44c-168">솔루션 탐색기에서 확장을 **역할** ChatService 프로젝트 내부 폴더.</span><span class="sxs-lookup"><span data-stu-id="ed44c-168">In Solution Explorer, expand the **Roles** folder inside the ChatService project.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image9.png)

<span data-ttu-id="ed44c-169">SignalRChat 역할을 마우스 오른쪽 단추로 클릭 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-169">Right-click the SignalRChat role and select **Properties**.</span></span> <span data-ttu-id="ed44c-170">선택 된 **구성** 탭 합니다. 아래 **인스턴스** 2를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-170">Select the **Configuration** tab. Under **Instances** select 2.</span></span> <span data-ttu-id="ed44c-171">VM 크기 설정할 수도 있습니다 **작음**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-171">You can also set the VM size to **Extra Small**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image10.png)

<span data-ttu-id="ed44c-172">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-172">Save the changes.</span></span>

<span data-ttu-id="ed44c-173">솔루션 탐색기에서 ChatService 프로젝트를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-173">In Solution Explorer, right-click the ChatService project.</span></span> <span data-ttu-id="ed44c-174">**게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-174">Select **Publish**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image11.png)

<span data-ttu-id="ed44c-175">Windows Azure에 첫 번째 시간 게시 인 경우 자격 증명을 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-175">If this is your first time publishing to Windows Azure, you must download your credentials.</span></span> <span data-ttu-id="ed44c-176">에 **게시** 마법사 "자격 증명을 다운로드 하려면 로그인"을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-176">In the **Publish** wizard, click "Sign in to download credentials".</span></span> <span data-ttu-id="ed44c-177">Windows Azure 포털에 로그인 하 고 게시 설정 파일을 다운로드 하 라는 메시지가 나타납니다이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-177">This will prompt you to sign into the Windows Azure portal and download a publish settings file.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image12.png)

<span data-ttu-id="ed44c-178">클릭 **가져오기** 다운로드 한 게시 설정 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-178">Click **Import** and select the publish settings file that you downloaded.</span></span>

<span data-ttu-id="ed44c-179">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-179">Click **Next**.</span></span> <span data-ttu-id="ed44c-180">에 **게시 설정** 대화 상자 아래에 있는 **클라우드 서비스**, 앞에서 만든 클라우드 서비스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-180">In the **Publish Settings** dialog, under **Cloud Service**, select the cloud service that you created earlier.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image13.png)

<span data-ttu-id="ed44c-181">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-181">Click **Publish**.</span></span> <span data-ttu-id="ed44c-182">응용 프로그램을 배포 하 고 Vm을 시작 하려면 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-182">It can take a few minutes to deploy the application and start the VMs.</span></span>

<span data-ttu-id="ed44c-183">지금 채팅 응용 프로그램을 실행 하는 경우 역할 인스턴스가 Service Bus 토픽을 사용 하 여 Azure Service Bus를 통해 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-183">Now when you run the chat application, the role instances communicate through Azure Service Bus, using a Service Bus topic.</span></span> <span data-ttu-id="ed44c-184">항목은 여러 구독자를 허용 하는 메시지 큐입니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-184">A topic is a message queue that allows multiple subscribers.</span></span>

<span data-ttu-id="ed44c-185">백플레인에서 항목 및 구독에 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-185">The backplane automatically creates the topic and the subscriptions.</span></span> <span data-ttu-id="ed44c-186">구독 및 메시지 작업을 보려면 Azure portal을 열고 Service Bus 네임 스페이스를 선택한 "항목"을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-186">To see the subscriptions and message activity, open the Azure portal, select the Service Bus namespace, and click on "Topics".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image14.png)

<span data-ttu-id="ed44c-187">메시지 작업 대시보드에 표시 되는 데 몇 분 정도 걸릴 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-187">It make take a few minutes for the message activity to show up in the dashboard.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image15.png)

<span data-ttu-id="ed44c-188">SignalR 항목 수명을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-188">SignalR manages the topic lifetime.</span></span> <span data-ttu-id="ed44c-189">응용 프로그램 배포는 수동으로 항목을 삭제 하거나 해당 항목에 대 한 설정을 변경 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="ed44c-189">As long as your application is deployed, don't try to manually delete topics or change settings on the topic.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ed44c-190">문제 해결</span><span class="sxs-lookup"><span data-stu-id="ed44c-190">Troubleshooting</span></span>

<span data-ttu-id="ed44c-191">**System.InvalidOperationException "만 지원 되는 IsolationLevel is 'IsolationLevel.Serializable'."**</span><span class="sxs-lookup"><span data-stu-id="ed44c-191">**System.InvalidOperationException "The only supported IsolationLevel is 'IsolationLevel.Serializable'."**</span></span>

<span data-ttu-id="ed44c-192">이 오류는 작업에 대 한 트랜잭션 수준을 이외의 값으로 설정 된 경우 `Serializable`합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-192">This error can occur if the transaction level for an operation is set to something other than `Serializable`.</span></span> <span data-ttu-id="ed44c-193">작업이 없는 다른 트랜잭션 수준을 사용 하 여 수행 되는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed44c-193">Verify that no operations are being performed with other transaction levels.</span></span>
