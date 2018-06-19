---
uid: aspnet/overview/owin-and-katana/katana-samples
title: Katana 샘플 | Microsoft Docs
author: microsoft
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/17/2014
ms.topic: article
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: 815355c00c9c15cfefa5f98dc89da676743b0390
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
ms.locfileid: "28034492"
---
<a name="katana-samples"></a><span data-ttu-id="96b0d-102">Katana 샘플</span><span class="sxs-lookup"><span data-stu-id="96b0d-102">Katana Samples</span></span>
====================
<span data-ttu-id="96b0d-103">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="96b0d-103">by [Microsoft](https://github.com/microsoft)</span></span>

## <a name="katana-samples"></a><span data-ttu-id="96b0d-104">Katana 샘플</span><span class="sxs-lookup"><span data-stu-id="96b0d-104">Katana Samples</span></span>

<span data-ttu-id="96b0d-105">**ASP.NET 라우팅합니다 샘플** | [소스 코드](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/AspNetRoutes/ReadMe.txt)</span><span class="sxs-lookup"><span data-stu-id="96b0d-105">**ASP.NET Routes Sample** | [Source Code](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/AspNetRoutes/ReadMe.txt)</span></span>  
<span data-ttu-id="96b0d-106">일부 응용 프로그램 비 OWIN 구성 요소와 함께 Asp.Net 경로 테이블에는 OWIN 구성 요소를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="96b0d-106">In some applications you will want to hook up OWIN components in the Asp.Net route table side by side with non-OWIN components.</span></span> <span data-ttu-id="96b0d-107">이 샘플에서는 MapOwinPath 및 Microsoft.Owin.Host.SystemWeb 제공한 MapOwinRoute RouteCollection 확장 메서드를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="96b0d-107">This sample shows how to use the RouteCollection extension methods MapOwinPath and MapOwinRoute provided by Microsoft.Owin.Host.SystemWeb.</span></span>

<span data-ttu-id="96b0d-108">**샘플 파이프라인 분기** | [소스 코드](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/BranchingPipelines/ReadMe.txt)</span><span class="sxs-lookup"><span data-stu-id="96b0d-108">**Branching Pipelines Sample** | [Source Code](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/BranchingPipelines/ReadMe.txt)</span></span>  
<span data-ttu-id="96b0d-109">OWIN 요청 처리 파이프라인을 선형 될 필요가 없습니다, 다른 방법으로 요청을 처리 하는 분기 될 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="96b0d-109">OWIN request processing pipelines do not need to be linear, they can be branched to process requests in different ways.</span></span> <span data-ttu-id="96b0d-110">이 샘플에는 요청 경로 또는 헤더와 같은 다른 요청 데이터에 따라 분기 파이프라인을 생성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="96b0d-110">This sample shows how to construct a branching pipeline based on request paths or other request data such as headers.</span></span> <span data-ttu-id="96b0d-111">이러한 구성 요소는 Microsoft.Owin.Mapping nuget 패키지에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96b0d-111">These components are available in the Microsoft.Owin.Mapping nuget package.</span></span>

<span data-ttu-id="96b0d-112">**사용자 지정 서버 샘플** | [소스 코드](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/CustomServer/MyCustomServer/CustomServer.cs) </span><span class="sxs-lookup"><span data-stu-id="96b0d-112">**Custom Server Sample** | [Source Code](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/CustomServer/MyCustomServer/CustomServer.cs) </span></span>  
<span data-ttu-id="96b0d-113">자체 호스팅하는 경우 사용자 지정 OWIN 서버를 사용 하는 방법을 보여 줍니다. OWIN 합니다.</span><span class="sxs-lookup"><span data-stu-id="96b0d-113">Shows how to use a custom OWIN server when self-hosting OWIN.</span></span>

<span data-ttu-id="96b0d-114">**샘플에 포함 된** | [소스 코드](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/Embedded/ReadMe.txt)</span><span class="sxs-lookup"><span data-stu-id="96b0d-114">**Embedded Sample** | [Source Code](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/Embedded/ReadMe.txt)</span></span>  
<span data-ttu-id="96b0d-115">사용자가 소유한 프로세스 환경 일부 OWIN 서버에서 실행 될 수 있습니다 (&quot;자체 호스트&quot;).</span><span class="sxs-lookup"><span data-stu-id="96b0d-115">Some OWIN servers can be run inside of your own process (&quot;self-hosted&quot;).</span></span> <span data-ttu-id="96b0d-116">이 샘플에서는 Microsoft.Owin.Hosting nuget 패키지에서 제공 하는 도구를 사용 하 여 OWIN 응용 프로그램을 시작 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="96b0d-116">This sample shows how to start an OWIN application using the tools provided by the Microsoft.Owin.Hosting nuget package.</span></span>

<span data-ttu-id="96b0d-117">**HelloWorld 샘플** | [소스 코드](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/HelloWorld/ReadMe.txt)</span><span class="sxs-lookup"><span data-stu-id="96b0d-117">**HelloWorld Sample** | [Source Code](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/HelloWorld/ReadMe.txt)</span></span>  
<span data-ttu-id="96b0d-118">OWIN은 HTTP 서버 응용 프로그램 이식성을 통해 다양 한 서버 간에 API 추상화입니다.</span><span class="sxs-lookup"><span data-stu-id="96b0d-118">OWIN is a HTTP server API abstraction that enables application portability across various servers.</span></span> <span data-ttu-id="96b0d-119">이 샘플에서는 일부를 사용 하 여 Hello World 응용 프로그램을 작성 하는 방법을 보여 줍니다. **간단한 래퍼** ASP.NET 웹 서버에 같은 원시 OWIN 추상화 및 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="96b0d-119">This sample demonstrates how to write a Hello World application using some **simple wrappers** around the raw OWIN abstraction and run it on a web server like ASP.NET.</span></span>

<span data-ttu-id="96b0d-120">**Hello World 원시 OWIN 샘플** | [소스 코드](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/HelloWorldRawOwin/ReadMe.txt)</span><span class="sxs-lookup"><span data-stu-id="96b0d-120">**Hello World Raw OWIN Sample** | [Source Code](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/HelloWorldRawOwin/ReadMe.txt)</span></span>  
<span data-ttu-id="96b0d-121">이 샘플에 사용 하 여 Hello World 응용 프로그램을 작성 하는 방법을 보여 줍니다는 **원시** OWIN 추상화 및 Asp.Net과 같은 웹 서버에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="96b0d-121">This sample demonstrates how to write a Hello World application using the **raw** OWIN abstraction and run it on a web server like Asp.Net.</span></span>

<span data-ttu-id="96b0d-122">**SignalR 샘플** | [소스 코드](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/SignalR/Program.cs)</span><span class="sxs-lookup"><span data-stu-id="96b0d-122">**SignalR Sample** | [Source Code](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/SignalR/Program.cs)</span></span>  
<span data-ttu-id="96b0d-123">SignalR OWIN를 사용 하 여 자체 호스트 하는 방법을 보여 줍니다. / Katana 합니다.</span><span class="sxs-lookup"><span data-stu-id="96b0d-123">Shows how to self-host SignalR using OWIN / Katana.</span></span> <span data-ttu-id="96b0d-124">자체 호스팅을 SignalR에 대 한 자세한 내용은 참조 하십시오. [자습서: 자체 호스트 하는 SignalR](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="96b0d-124">For more info about self-hosting SignalR, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<span data-ttu-id="96b0d-125">**정적 샘플 파일** | [소스 코드](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/StaticFilesSample/Startup.cs) </span><span class="sxs-lookup"><span data-stu-id="96b0d-125">**Static Files Sample** | [Source Code](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/StaticFilesSample/Startup.cs) </span></span>  
<span data-ttu-id="96b0d-126">OWIN를 사용 하 여 정적 파일에 대 한 HTTP 요청을 지 원하는 방법을 보여 줍니다. / Katana 합니다.</span><span class="sxs-lookup"><span data-stu-id="96b0d-126">Shows how to support HTTP requests for static files using OWIN / Katana.</span></span>

<span data-ttu-id="96b0d-127">**Web API** | [소스 코드](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/WebApi/ReadMe.txt) </span><span class="sxs-lookup"><span data-stu-id="96b0d-127">**Web API** | [Source Code](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/WebApi/ReadMe.txt) </span></span>  
<span data-ttu-id="96b0d-128">이 예제에는 OWIN IIS에서 호스트 웹 API OWIN 파이프라인을 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="96b0d-128">This sample shows how to host OWIN in IIS and add Web API to the OWIN pipeline.</span></span>

<span data-ttu-id="96b0d-129">**웹 소켓 샘플** | [소스 코드](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/WebSocketSample/WebSocketServer/Startup.cs) </span><span class="sxs-lookup"><span data-stu-id="96b0d-129">**Web Socket Sample** | [Source Code](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/Katana/WebSocketSample/WebSocketServer/Startup.cs) </span></span>  
<span data-ttu-id="96b0d-130">사용 하 여 웹 소켓 OWIN에서 지 원하는 방법을 보여 줍니다는 [System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="96b0d-130">Shows how to support Web Sockets in OWIN by using the [System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) class.</span></span>
