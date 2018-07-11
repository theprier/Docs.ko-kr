---
title: ASP.NET Core에서 WebSocket 지원
author: rick-anderson
description: ASP.NET Core에서 Websocket을 시작하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 06/28/2018
uid: fundamentals/websockets
ms.openlocfilehash: a9fe13ef7895ea3ab43257dbbaf4521f883c0804
ms.sourcegitcommit: 18339e3cb5a891a3ca36d8146fa83cf91c32e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37433989"
---
# <a name="websockets-support-in-aspnet-core"></a><span data-ttu-id="09891-103">ASP.NET Core에서 WebSocket 지원</span><span class="sxs-lookup"><span data-stu-id="09891-103">WebSockets support in ASP.NET Core</span></span>

<span data-ttu-id="09891-104">작성자: [Tom Dykstra](https://github.com/tdykstra) 및 [Andrew Stanton-Nurse](https://github.com/anurse)</span><span class="sxs-lookup"><span data-stu-id="09891-104">By [Tom Dykstra](https://github.com/tdykstra) and [Andrew Stanton-Nurse](https://github.com/anurse)</span></span>

<span data-ttu-id="09891-105">본문에서는 ASP.NET Core에서 Websocket을 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="09891-105">This article explains how to get started with WebSockets in ASP.NET Core.</span></span> <span data-ttu-id="09891-106">[WebSocket](https://wikipedia.org/wiki/WebSocket)([RFC 6455](https://tools.ietf.org/html/rfc6455))은 TCP 연결을 통해 지속적인 양방향 통신 채널을 사용할 수 있도록 해주는 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="09891-106">[WebSocket](https://wikipedia.org/wiki/WebSocket) ([RFC 6455](https://tools.ietf.org/html/rfc6455)) is a protocol that enables two-way persistent communication channels over TCP connections.</span></span> <span data-ttu-id="09891-107">채팅, 대시보드 및 게임 앱 등 신속한 실시간 통신을 활용하는 앱에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="09891-107">It's used in apps that benefit from fast, real-time communication, such as chat, dashboard, and game apps.</span></span>

<span data-ttu-id="09891-108">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample) ([다운로드 방법](xref:tutorials/index#how-to-download-a-sample)).</span><span class="sxs-lookup"><span data-stu-id="09891-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample)).</span></span> <span data-ttu-id="09891-109">자세한 내용은 [다음 단계](#next-steps) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09891-109">See the [Next steps](#next-steps) section for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09891-110">전제 조건</span><span class="sxs-lookup"><span data-stu-id="09891-110">Prerequisites</span></span>

* <span data-ttu-id="09891-111">ASP.NET Core 1.1 이상</span><span class="sxs-lookup"><span data-stu-id="09891-111">ASP.NET Core 1.1 or later</span></span>
* <span data-ttu-id="09891-112">ASP.NET Core를 지원하는 모든 OS:</span><span class="sxs-lookup"><span data-stu-id="09891-112">Any OS that supports ASP.NET Core:</span></span>
  
  * <span data-ttu-id="09891-113">Windows 7/Windows Server 2008 이상</span><span class="sxs-lookup"><span data-stu-id="09891-113">Windows 7 / Windows Server 2008 or later</span></span>
  * <span data-ttu-id="09891-114">Linux</span><span class="sxs-lookup"><span data-stu-id="09891-114">Linux</span></span>
  * <span data-ttu-id="09891-115">macOS</span><span class="sxs-lookup"><span data-stu-id="09891-115">macOS</span></span>
  
* <span data-ttu-id="09891-116">IIS가 있는 Windows에서 앱을 실행하는 경우:</span><span class="sxs-lookup"><span data-stu-id="09891-116">If the app runs on Windows with IIS:</span></span>

  * <span data-ttu-id="09891-117">Windows 8 / Windows Server 2012 이상</span><span class="sxs-lookup"><span data-stu-id="09891-117">Windows 8 / Windows Server 2012 or later</span></span>
  * <span data-ttu-id="09891-118">IIS 8 / IIS 8 Express</span><span class="sxs-lookup"><span data-stu-id="09891-118">IIS 8 / IIS 8 Express</span></span>
  * <span data-ttu-id="09891-119">WebSockets는 IIS에서 활성화되어야 합니다([IIS/IIS Express 지원](#iisiis-express-support) 섹션 참조).</span><span class="sxs-lookup"><span data-stu-id="09891-119">WebSockets must be enabled in IIS (See the [IIS/IIS Express support](#iisiis-express-support) section.)</span></span>
  
* <span data-ttu-id="09891-120">앱이 [HTTP.sys](xref:fundamentals/servers/httpsys)에서 실행되는 경우:</span><span class="sxs-lookup"><span data-stu-id="09891-120">If the app runs on [HTTP.sys](xref:fundamentals/servers/httpsys):</span></span>

  * <span data-ttu-id="09891-121">Windows 8 / Windows Server 2012 이상</span><span class="sxs-lookup"><span data-stu-id="09891-121">Windows 8 / Windows Server 2012 or later</span></span>

* <span data-ttu-id="09891-122">지원되는 브라우저는 https://caniuse.com/#feat=websockets를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09891-122">For supported browsers, see https://caniuse.com/#feat=websockets.</span></span>

## <a name="when-to-use-websockets"></a><span data-ttu-id="09891-123">WebSockets를 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="09891-123">When to use WebSockets</span></span>

<span data-ttu-id="09891-124">WebSockets를 사용하여 소켓 연결로 직접 작업하세요.</span><span class="sxs-lookup"><span data-stu-id="09891-124">Use WebSockets to work directly with a socket connection.</span></span> <span data-ttu-id="09891-125">예를 들어, 실시간 게임에서 가능한 최상의 성능을 얻으려면 WebSockets를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="09891-125">For example, use WebSockets for the best possible performance with a real-time game.</span></span>

<span data-ttu-id="09891-126">[ASP.NET Core SignalR](xref:signalr/introduction)은 앱에 실시간 웹 기능을 추가하는 것을 간소화하는 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="09891-126">[ASP.NET Core SignalR](xref:signalr/introduction) is a library that simplifies adding real-time web functionality to apps.</span></span> <span data-ttu-id="09891-127">가능하면 Websocket을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-127">It uses WebSockets whenever possible.</span></span>

## <a name="how-to-use-websockets"></a><span data-ttu-id="09891-128">WebSocket 사용 방법</span><span class="sxs-lookup"><span data-stu-id="09891-128">How to use WebSockets</span></span>

* <span data-ttu-id="09891-129">[Microsoft.AspNetCore.WebSockets](https://www.nuget.org/packages/Microsoft.AspNetCore.WebSockets/) 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-129">Install the [Microsoft.AspNetCore.WebSockets](https://www.nuget.org/packages/Microsoft.AspNetCore.WebSockets/) package.</span></span>
* <span data-ttu-id="09891-130">미들웨어를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-130">Configure the middleware.</span></span>
* <span data-ttu-id="09891-131">WebSocket 요청을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-131">Accept WebSocket requests.</span></span>
* <span data-ttu-id="09891-132">메시지를 전송 및 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-132">Send and receive messages.</span></span>

### <a name="configure-the-middleware"></a><span data-ttu-id="09891-133">미들웨어 구성하기</span><span class="sxs-lookup"><span data-stu-id="09891-133">Configure the middleware</span></span>

<span data-ttu-id="09891-134">`Startup` 클래스의 `Configure` 메서드에 WebSockets 미들웨어를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-134">Add the WebSockets middleware in the `Configure` method of the `Startup` class:</span></span>

[!code-csharp[](websockets/sample/Startup.cs?name=UseWebSockets)]

<span data-ttu-id="09891-135">이때 다음과 같은 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09891-135">The following settings can be configured:</span></span>

* <span data-ttu-id="09891-136">`KeepAliveInterval` - 프록시가 연결을 유지할 수 있도록 클라이언트로 "핑(ping)" 프레임을 전송하는 빈도입니다.</span><span class="sxs-lookup"><span data-stu-id="09891-136">`KeepAliveInterval` - How frequently to send "ping" frames to the client to ensure proxies keep the connection open.</span></span>
* <span data-ttu-id="09891-137">`ReceiveBufferSize` - 데이터 수신에 사용되는 버퍼의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="09891-137">`ReceiveBufferSize` - The size of the buffer used to receive data.</span></span> <span data-ttu-id="09891-138">고급 사용자는 데이터 크기에 따라 성능 튜닝이 필요할 경우 이 값을 변경해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09891-138">Advanced users may need to change this for performance tuning based on the size of the data.</span></span>

[!code-csharp[](websockets/sample/Startup.cs?name=UseWebSocketsOptions)]

### <a name="accept-websocket-requests"></a><span data-ttu-id="09891-139">WebSocket 요청 수락하기</span><span class="sxs-lookup"><span data-stu-id="09891-139">Accept WebSocket requests</span></span>

<span data-ttu-id="09891-140">요청 수명 주기의 뒷부분에서 (예를 들어, `Configure` 메서드나 MVC 액션의 뒷부분에서) WebSocket 요청 여부를 확인하고 WebSocket 요청을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-140">Somewhere later in the request life cycle (later in the `Configure` method or in an MVC action, for example) check if it's a WebSocket request and accept the WebSocket request.</span></span>

<span data-ttu-id="09891-141">다음 예제는 `Configure` 메서드의 뒷부분에서 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="09891-141">The following example is from later in the `Configure` method:</span></span>

[!code-csharp[](websockets/sample/Startup.cs?name=AcceptWebSocket&highlight=7)]

<span data-ttu-id="09891-142">WebSocket 요청은 모든 URL을 통해서 전달될 수 있지만, 이 예제 코드에서는 `/ws` 에 대한 요청만 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-142">A WebSocket request could come in on any URL, but this sample code only accepts requests for `/ws`.</span></span>

### <a name="send-and-receive-messages"></a><span data-ttu-id="09891-143">메시지 보내기 및 받기</span><span class="sxs-lookup"><span data-stu-id="09891-143">Send and receive messages</span></span>

<span data-ttu-id="09891-144">`AcceptWebSocketAsync` 메서드는 TCP 연결을 WebSocket 연결로 업그레이드하고 [WebSocket](/dotnet/core/api/system.net.websockets.websocket) 개체를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-144">The `AcceptWebSocketAsync` method upgrades the TCP connection to a WebSocket connection and provides a [WebSocket](/dotnet/core/api/system.net.websockets.websocket) object.</span></span> <span data-ttu-id="09891-145">`WebSocket` 개체를 사용하여 메시지를 보내고 받습니다.</span><span class="sxs-lookup"><span data-stu-id="09891-145">Use the `WebSocket` object to send and receive messages.</span></span>

<span data-ttu-id="09891-146">앞에서 살펴본 WebSocket 요청을 수락하는 코드는 `WebSocket` 개체를 `Echo` 메서드로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-146">The code shown earlier that accepts the WebSocket request passes the `WebSocket` object to an `Echo` method.</span></span> <span data-ttu-id="09891-147">코드는 메시지를 수신하고 동일한 메시지를 즉시 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="09891-147">The code receives a message and immediately sends back the same message.</span></span> <span data-ttu-id="09891-148">메시지는 클라이언트가 연결을 닫을 때까지 루프에서 보내고 받습니다.</span><span class="sxs-lookup"><span data-stu-id="09891-148">Messages are sent and received in a loop until the client closes the connection:</span></span>

[!code-csharp[](websockets/sample/Startup.cs?name=Echo)]

<span data-ttu-id="09891-149">루프가 시작되기 전에 WebSocket 연결을 수락하면 미들웨어 파이프라인이 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="09891-149">When accepting the WebSocket connection before beginning the loop, the middleware pipeline ends.</span></span> <span data-ttu-id="09891-150">그리고 소켓을 닫으면 파이프라인이 풀립니다.</span><span class="sxs-lookup"><span data-stu-id="09891-150">Upon closing the socket, the pipeline unwinds.</span></span> <span data-ttu-id="09891-151">즉, 요청은 WebSocket이 수락될 때 파이프라인에서 앞으로 이동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="09891-151">That is, the request stops moving forward in the pipeline when the WebSocket is accepted.</span></span> <span data-ttu-id="09891-152">루프가 완료되고 소켓이 닫히면 요청이 파이프라인 백업을 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-152">When the loop is finished and the socket is closed, the request proceeds back up the pipeline.</span></span>

## <a name="iisiis-express-support"></a><span data-ttu-id="09891-153">IIS/IIS Express 지원</span><span class="sxs-lookup"><span data-stu-id="09891-153">IIS/IIS Express support</span></span>

<span data-ttu-id="09891-154">IIS/IIS Express 8 이상이 있는 Windows Server 2012 이상 및 Windows 8 이상에서는 WebSocket 프로토콜을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-154">Windows Server 2012 or later and Windows 8 or later with IIS/IIS Express 8 or later has support for the WebSocket protocol.</span></span>

<span data-ttu-id="09891-155">Windows Server 2012 이상에서 WebSocket 프로토콜을 지원하려면:</span><span class="sxs-lookup"><span data-stu-id="09891-155">To enable support for the WebSocket protocol on Windows Server 2012 or later:</span></span>

1. <span data-ttu-id="09891-156">**관리** 메뉴 또는 **서버 관리자**의 링크를 통해 **역할 및 기능 추가** 마법사를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-156">Use the **Add Roles and Features** wizard from the **Manage** menu or the link in **Server Manager**.</span></span>
1. <span data-ttu-id="09891-157">**역할 기반 또는 기능 기반 설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-157">Select **Role-based or Feature-based Installation**.</span></span> <span data-ttu-id="09891-158">**새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-158">Select **Next**.</span></span>
1. <span data-ttu-id="09891-159">적절한 서버를 선택합니다(로컬 서버가 기본적으로 선택됨).</span><span class="sxs-lookup"><span data-stu-id="09891-159">Select the appropriate server (the local server is selected by default).</span></span> <span data-ttu-id="09891-160">**새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-160">Select **Next**.</span></span>
1. <span data-ttu-id="09891-161">**역할** 트리에서 **Web Server(IIS)** 를 확장하고 **Web Server**를 확장한 다음, **응용 프로그램 개발**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-161">Expand **Web Server (IIS)** in the **Roles** tree, expand **Web Server**, and then expand **Application Development**.</span></span>
1. <span data-ttu-id="09891-162">**WebSocket 프로토콜**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-162">Select **WebSocket Protocol**.</span></span> <span data-ttu-id="09891-163">**새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-163">Select **Next**.</span></span>
1. <span data-ttu-id="09891-164">추가 기능이 필요 없는 경우 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-164">If additional features aren't needed, select **Next**.</span></span>
1. <span data-ttu-id="09891-165">**설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-165">Select **Install**.</span></span>
1. <span data-ttu-id="09891-166">설치가 완료되면 **닫기**를 선택하여 마법사를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-166">When the installation completes, select **Close** to exit the wizard.</span></span>

<span data-ttu-id="09891-167">Windows 8 이상에서 WebSocket 프로토콜을 지원하려면:</span><span class="sxs-lookup"><span data-stu-id="09891-167">To enable support for the WebSocket protocol on Windows 8 or later:</span></span>

1. <span data-ttu-id="09891-168">**제어판** > **프로그램** > **프로그램 및 기능** > **Windows 기능 Windows 기능 사용/사용 안 함**(화면 왼쪽)으로 차례로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-168">Navigate to **Control Panel** > **Programs** > **Programs and Features** > **Turn Windows features on or off** (left side of the screen).</span></span>
1. <span data-ttu-id="09891-169">**인터넷 정보 서비스** > **World Wide Web 서비스** > **응용 프로그램 개발 기능** 노드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="09891-169">Open the following nodes: **Internet Information Services** > **World Wide Web Services** > **Application Development Features**.</span></span>
1. <span data-ttu-id="09891-170">**WebSocket 프로토콜** 기능을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-170">Select the **WebSocket Protocol** feature.</span></span> <span data-ttu-id="09891-171">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-171">Select **OK**.</span></span>

<span data-ttu-id="09891-172">**node.js에서 socket.io를 사용할 때 WebSocket 비활성화**</span><span class="sxs-lookup"><span data-stu-id="09891-172">**Disable WebSocket when using socket.io on node.js**</span></span>

<span data-ttu-id="09891-173">[Node.js](https://nodejs.org/)의 [socket.io](https://socket.io/)에서 WebSocket 지원을 사용하는 경우 *web.config* 또는 *applicationHost.config*의 `webSocket` 요소를 사용하여 기본 IIS WebSocket 모듈을 비활성화합니다. 이 단계를 수행하지 않으면 IIS WebSocket 모듈이 Node.js 및 앱이 아닌 WebSocket 통신을 처리하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-173">If using the WebSocket support in [socket.io](https://socket.io/) on [Node.js](https://nodejs.org/), disable the default IIS WebSocket module using the `webSocket` element in *web.config* or *applicationHost.config*. If this step isn't performed, the IIS WebSocket module attempts to handle the WebSocket communication rather than Node.js and the app.</span></span>

```xml
<system.webServer>
  <webSocket enabled="false" />
</system.webServer>
```

## <a name="next-steps"></a><span data-ttu-id="09891-174">다음 단계</span><span class="sxs-lookup"><span data-stu-id="09891-174">Next steps</span></span>

<span data-ttu-id="09891-175">이 아티클과 함께 제공되는 [샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample)은 에코 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="09891-175">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample) that accompanies this article is an echo app.</span></span> <span data-ttu-id="09891-176">WebSocket 연결을 생성하는 웹 페이지가 제공되며 서버는 수신한 메시지를 클라이언트로 재전송합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-176">It has a web page that makes WebSocket connections, and the server resends any messages it receives back to the client.</span></span> <span data-ttu-id="09891-177">명령 프롬프트에서 앱을 실행하고(IIS Express가 있는 Visual Studio에서 실행되도록 설정되지 않음) http://localhost:5000으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-177">Run the app from a command prompt (it's not set up to run from Visual Studio with IIS Express) and navigate to http://localhost:5000.</span></span> <span data-ttu-id="09891-178">웹 페이지 왼쪽 상단에 연결 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="09891-178">The web page shows the connection status in the upper left:</span></span>

![웹 페이지의 초기 상태](websockets/_static/start.png)

<span data-ttu-id="09891-180">**Connect** 를 선택해서 지정한 URL로 WebSocket 요청을 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-180">Select **Connect** to send a WebSocket request to the URL shown.</span></span> <span data-ttu-id="09891-181">그리고 테스트 메시지를 입력한 다음 **Send** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09891-181">Enter a test message and select **Send**.</span></span> <span data-ttu-id="09891-182">테스트를 모두 마쳤으면 **Close Socket** 을 선택하십시오.</span><span class="sxs-lookup"><span data-stu-id="09891-182">When done, select **Close Socket**.</span></span> <span data-ttu-id="09891-183">**Communication Log** 섹션에는 각각의 열기, 전송 및 닫기 동작이 발생한 순서대로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="09891-183">The **Communication Log** section reports each open, send, and close action as it happens.</span></span>

![웹 페이지의 초기 상태](websockets/_static/end.png)
