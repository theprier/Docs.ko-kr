---
uid: signalr/overview/deployment/using-signalr-with-azure-web-sites
title: SignalR을 사용 하 여 Azure App Service에서 Web Apps를 사용 하 여 | Microsoft Docs
author: pfletcher
description: 이 문서에서는 Microsoft Azure에서 실행 되는 SignalR 응용 프로그램을 구성 하는 방법을 설명 합니다. 소프트웨어 버전은 Visual Studio 2013 또는 Vis. 자습서에서 사용...
ms.author: riande
ms.date: 07/01/2015
ms.assetid: 2a7517a0-b88c-4162-ade3-9bf6ca7062fd
msc.legacyurl: /signalr/overview/deployment/using-signalr-with-azure-web-sites
msc.type: authoredcontent
ms.openlocfilehash: da69e1aba1b56d69ad8e710cddd2b492168f1255
ms.sourcegitcommit: 74e3be25ea37b5fc8b4b433b0b872547b4b99186
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2018
ms.locfileid: "53287769"
---
<a name="using-signalr-with-web-apps-in-azure-app-service"></a><span data-ttu-id="ba88f-104">Azure App Service에서 Web Apps에 SignalR 사용</span><span class="sxs-lookup"><span data-stu-id="ba88f-104">Using SignalR with Web Apps in Azure App Service</span></span>
====================
<span data-ttu-id="ba88f-105">[Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="ba88f-105">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="ba88f-106">이 문서에서는 Microsoft Azure에서 실행 되는 SignalR 응용 프로그램을 구성 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba88f-106">This document describes how to configure a SignalR application that runs on Microsoft Azure.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="ba88f-107">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="ba88f-107">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="ba88f-108">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) 또는 Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="ba88f-108">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) or Visual Studio 2012</span></span>
> - <span data-ttu-id="ba88f-109">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="ba88f-109">.NET 4.5</span></span>
> - <span data-ttu-id="ba88f-110">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="ba88f-110">SignalR version 2</span></span>
> - <span data-ttu-id="ba88f-111">Visual Studio 2013 또는 2012 용 azure SDK 2.3</span><span class="sxs-lookup"><span data-stu-id="ba88f-111">Azure SDK 2.3 for Visual Studio 2013 or 2012</span></span>
>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="ba88f-112">질문이 나 의견이 있으면</span><span class="sxs-lookup"><span data-stu-id="ba88f-112">Questions and comments</span></span>
>
> <span data-ttu-id="ba88f-113">이 자습서를 연결 하는 방법 및 새로운 개선할 수 있습니다 페이지의 맨 아래에 의견에서에 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="ba88f-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="ba88f-114">에 자습서로 직접 관련 되지 않은 질문이 있을 경우 게시할 수 하는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR), [StackOverflow.com](http://stackoverflow.com/), 또는 [Microsoft Azure 포럼](https://social.msdn.microsoft.com/Forums/windowsazure/home?category=windowsazureplatform).</span><span class="sxs-lookup"><span data-stu-id="ba88f-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR), [StackOverflow.com](http://stackoverflow.com/), or the [Microsoft Azure forums](https://social.msdn.microsoft.com/Forums/windowsazure/home?category=windowsazureplatform).</span></span>


## <a name="table-of-contents"></a><span data-ttu-id="ba88f-115">목차</span><span class="sxs-lookup"><span data-stu-id="ba88f-115">Table of Contents</span></span>

- [<span data-ttu-id="ba88f-116">소개</span><span class="sxs-lookup"><span data-stu-id="ba88f-116">Introduction</span></span>](#introduction)
- [<span data-ttu-id="ba88f-117">SignalR 웹 앱을 Azure App Service에 배포</span><span class="sxs-lookup"><span data-stu-id="ba88f-117">Deploying a SignalR Web App to Azure App Service</span></span>](#deploying)
- [<span data-ttu-id="ba88f-118">Azure App Service에서 Websocket을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="ba88f-118">Enabling WebSockets on Azure App Service</span></span>](#websocket)
- [<span data-ttu-id="ba88f-119">Azure Redis 캐시 백플레인으로 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="ba88f-119">Using the Azure Redis Cache Backplane</span></span>](#backplane)
- [<span data-ttu-id="ba88f-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ba88f-120">Next Steps</span></span>](#nextsteps)

<a id="introduction"></a>
## <a name="introduction"></a><span data-ttu-id="ba88f-121">소개</span><span class="sxs-lookup"><span data-stu-id="ba88f-121">Introduction</span></span>

<span data-ttu-id="ba88f-122">ASP.NET SignalR 새로운 수준의 서버와 웹 또는.NET 클라이언트 간의 상호 작용을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba88f-122">ASP.NET SignalR can be used to bring a new level of interactivity between servers and web or .NET clients.</span></span> <span data-ttu-id="ba88f-123">Azure에서 호스트 하는 경우 SignalR 응용 프로그램 수 활용 항상 사용 가능한 확장성을 제공 클라우드에서 실행 하는 고성능 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="ba88f-123">When hosted in Azure, SignalR applications can take advantage of the highly available, scalable, and performant environment that running in the cloud provides.</span></span>

<a id="deploying"></a>
## <a name="deploying-a-signalr-web-app-to-azure-app-service"></a><span data-ttu-id="ba88f-124">SignalR 웹 앱을 Azure App Service에 배포</span><span class="sxs-lookup"><span data-stu-id="ba88f-124">Deploying a SignalR Web App to Azure App Service</span></span>

<span data-ttu-id="ba88f-125">SignalR은 온-프레미스 서버에 배포와 Azure에 응용 프로그램을 배포 하는 데 특정 복잡 한 문제를 추가 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ba88f-125">SignalR doesn't add any particular complications to deploying an application to Azure versus deploying to an on-premises server.</span></span> <span data-ttu-id="ba88f-126">SignalR을 사용 하는 응용 프로그램 구성 또는 기타 설정을 변경 하지 않고 Azure에서 호스팅할 수 있습니다 (그러나 Websocket 지원에 대 한 참조 [Azure App Service에서 사용 하도록 설정 하면 Websocket](#websocket) 아래.) 이 자습서에서 만든 응용 프로그램 배포 하는 [초보자를 위한 자습서](../getting-started/tutorial-getting-started-with-signalr.md) azure.</span><span class="sxs-lookup"><span data-stu-id="ba88f-126">An application that uses SignalR can be hosted in Azure without any changes in configuration or other settings (though for WebSockets support, see [Enabling WebSockets on Azure App Service](#websocket) below.) For this tutorial, you'll deploy the application created in the [Getting Started Tutorial](../getting-started/tutorial-getting-started-with-signalr.md) to Azure.</span></span>

<span data-ttu-id="ba88f-127">**필수 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="ba88f-127">**Prerequisites**</span></span>

- <span data-ttu-id="ba88f-128">Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="ba88f-128">Visual Studio 2013.</span></span> <span data-ttu-id="ba88f-129">Visual Studio가 없는 Visual Studio 2013 Express for Web의 Azure SDK 설치에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba88f-129">If you don't have Visual Studio, Visual Studio 2013 Express for Web is included in the install of the Azure SDK.</span></span>
- <span data-ttu-id="ba88f-130">[Visual Studio 2013 용 azure SDK 2.3](https://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409) 나 [Visual Studio 2012 용 Azure SDK 2.3](https://go.microsoft.com/fwlink/p/?linkid=323511)합니다.</span><span class="sxs-lookup"><span data-stu-id="ba88f-130">[Azure SDK 2.3 for Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409) or [Azure SDK 2.3 for Visual Studio 2012](https://go.microsoft.com/fwlink/p/?linkid=323511).</span></span>
- <span data-ttu-id="ba88f-131">이 자습서를 완료 하려면 Azure 구독을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba88f-131">To complete this tutorial, you will need an Azure subscription.</span></span> <span data-ttu-id="ba88f-132">할 수 있습니다 [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), 또는 [평가판 구독을 신청](https://azure.microsoft.com/pricing/free-trial/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ba88f-132">You can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), or [sign up for a trial subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span>

### <a name="deploying-a-signalr-web-app-to-azure"></a><span data-ttu-id="ba88f-133">Azure SignalR 웹 앱 배포</span><span class="sxs-lookup"><span data-stu-id="ba88f-133">Deploying a SignalR web app to Azure</span></span>

1. <span data-ttu-id="ba88f-134">완료 합니다 [초보자를 위한 자습서](../getting-started/tutorial-getting-started-with-signalr.md), 또는에서 완료 된 프로젝트를 다운로드 [코드 갤러리](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)합니다.</span><span class="sxs-lookup"><span data-stu-id="ba88f-134">Complete the [Getting Started Tutorial](../getting-started/tutorial-getting-started-with-signalr.md), or download the finished project from [Code Gallery](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9).</span></span>
2. <span data-ttu-id="ba88f-135">Visual Studio에서 선택 **빌드**하십시오 **SignalR 채팅 게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba88f-135">In Visual Studio, select **Build**, **Publish SignalR Chat**.</span></span>
3. <span data-ttu-id="ba88f-136">"웹 게시" 대화 상자에서 "Windows Azure 웹 사이트"를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba88f-136">In the "Publish Web" dialog, select "Windows Azure Web Sites".</span></span>

    ![Azure 웹 사이트를 선택 합니다.](using-signalr-with-azure-web-sites/_static/image1.png)
4. <span data-ttu-id="ba88f-138">Microsoft 계정에 로그인 하지 않은 경우 클릭 **로그인 하는 중...**  "기존 웹 사이트 선택" 대화 상자에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba88f-138">If you aren't signed in to your Microsoft account, click **Sign In...** in the "Select Existing Web Site" dialog, and sign in.</span></span>

    ![기존 웹 사이트를 선택 합니다.](using-signalr-with-azure-web-sites/_static/image2.png)    ![Azure에 로그인](using-signalr-with-azure-web-sites/_static/image3.png)
5. <span data-ttu-id="ba88f-141">"기존 웹 사이트 선택" 대화 상자에서 클릭 **새로 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba88f-141">In the "Select Existing Web Site" dialog, click **New**.</span></span>

    ![새 웹 사이트](using-signalr-with-azure-web-sites/_static/image4.png)
6. <span data-ttu-id="ba88f-143">"Windows Azure에서 사이트 만들기" 대화 상자에서 고유한 앱 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba88f-143">In the "Create site on Windows Azure" dialog, enter a unique app name.</span></span> <span data-ttu-id="ba88f-144">지역 드롭다운 목록에서 가장 가까운 지역을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba88f-144">Select the region closest to you in the Region dropdown.</span></span> <span data-ttu-id="ba88f-145">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ba88f-145">Click **Create**.</span></span>

    ![Azure에서 사이트 만들기](using-signalr-with-azure-web-sites/_static/image5.png)
7. <span data-ttu-id="ba88f-147">"웹 게시" 대화 상자에서 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba88f-147">In the "Publish Web" dialog, click **Publish**.</span></span>

    ![사이트 게시](using-signalr-with-azure-web-sites/_static/image6.png)
8. <span data-ttu-id="ba88f-149">앱 게시 완료 되 면 Azure App Service Web Apps에서 호스팅되는 SignalR 채팅 응용 프로그램을 브라우저에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ba88f-149">When the app has completed publishing, the SignalR Chat application hosted in Azure App Service Web Apps will open in a browser.</span></span>

    ![브라우저에서 열고 사이트](using-signalr-with-azure-web-sites/_static/image7.png)

<a id="websocket"></a>
### <a name="enabling-websockets-on-azure-app-service-web-apps"></a><span data-ttu-id="ba88f-151">Azure App Service Web Apps에서 Websocket을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="ba88f-151">Enabling WebSockets on Azure App Service Web Apps</span></span>

<span data-ttu-id="ba88f-152">Websocket를 SignalR 응용 프로그램에 사용할 웹 앱에서 명시적으로 설정 해야 합니다. 그렇지 않으면 다른 프로토콜 사용 됩니다 (참조 [전송과 대체](../getting-started/introduction-to-signalr.md#transports) 세부 정보에 대 한).</span><span class="sxs-lookup"><span data-stu-id="ba88f-152">WebSockets needs to be explicitly enabled in your web app to be used in a SignalR application; otherwise, other protocols will be used (See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for details).</span></span>

<span data-ttu-id="ba88f-153">Azure App Service Web Apps에서 Websocket을 사용 하려면 웹 앱의 구성 섹션에서 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba88f-153">In order to use WebSockets on Azure App Service Web Apps, enable it in the configuration section of the web app.</span></span> <span data-ttu-id="ba88f-154">이렇게 하려면 웹 앱을 엽니다는 [Azure 관리 포털](https://manage.windowsazure.com/), 선택한 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba88f-154">To do this, open your web app in the [Azure Management Portal](https://manage.windowsazure.com/), and select Configure.</span></span>

![구성 탭](using-signalr-with-azure-web-sites/_static/image8.png)

<span data-ttu-id="ba88f-156">구성 페이지의 맨 위에 있는 웹 앱에.NET 4.5 사용 됨을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba88f-156">At the top of the configuration page, ensure that .NET 4.5 is used for your web app.</span></span>

![.NET framework 4.5 버전 설정](using-signalr-with-azure-web-sites/_static/image9.png)

<span data-ttu-id="ba88f-158">구성 페이지에 **Websocket** 설정 선택 **에서**합니다.</span><span class="sxs-lookup"><span data-stu-id="ba88f-158">On the configuration page, in the **WebSockets** setting, select **On**.</span></span>

![Websocket 설정: 켜기](using-signalr-with-azure-web-sites/_static/image10.png)

<span data-ttu-id="ba88f-160">구성 페이지의 맨 아래에서 선택 **저장할** 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba88f-160">At the bottom of the Configuration page, select **Save** to save your changes.</span></span>

![설정 저장](using-signalr-with-azure-web-sites/_static/image11.png)

<a id="backplane"></a>
## <a name="using-the-azure-redis-cache-backplane"></a><span data-ttu-id="ba88f-162">Azure Redis 캐시 백플레인으로 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="ba88f-162">Using the Azure Redis Cache Backplane</span></span>

<span data-ttu-id="ba88f-163">여러 인스턴스를 사용 하 여 웹 앱에 대 한 및 해당 인스턴스의 사용자 (, 예를 들어 하나의 인스턴스만 생성 하는 채팅 메시지 연결할 수 있도록 다른 인스턴스에 연결 된 사용자) 간에 상호 작용 해야 하는 경우, [Azure Redis Cache 백플레인에서](../performance/scaleout-with-redis.md) 응용 프로그램에서 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba88f-163">If you use multiple instances for your web app, and the users of those instances need to interact with one another (so that, for instance, chat messages created in one instance can reach the users connected to other instances), the [Azure Redis Cache backplane](../performance/scaleout-with-redis.md) must be implemented in your application.</span></span>

<a id="nextsteps"></a>
## <a name="next-steps"></a><span data-ttu-id="ba88f-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ba88f-164">Next Steps</span></span>

<span data-ttu-id="ba88f-165">Azure App Service에서 웹 앱에 대 한 자세한 내용은 참조 하세요. [Web Apps 개요](https://azure.microsoft.com/documentation/articles/app-service-web-overview/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ba88f-165">For more information on Web Apps in Azure App Service, see [Web Apps overview](https://azure.microsoft.com/documentation/articles/app-service-web-overview/).</span></span>
