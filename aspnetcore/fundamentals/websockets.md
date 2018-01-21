---
title: "ASP.NET Core에서 Websocket을 지원합니다."
author: tdykstra
description: "ASP.NET Core에서 Websocket을 시작 하는 방법을 알아봅니다."
ms.author: tdykstra
manager: wpickett
ms.date: 03/25/2017
ms.topic: article
ms.technology: aspnet
ms.prod: aspnet-core
uid: fundamentals/websockets
ms.openlocfilehash: 46c1f42b925a43df470d7491a1e259ab51ea5f50
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="introduction-to-websockets-in-aspnet-core"></a><span data-ttu-id="e9120-103">ASP.NET Core에서 Websocket 소개</span><span class="sxs-lookup"><span data-stu-id="e9120-103">Introduction to WebSockets in ASP.NET Core</span></span>

<span data-ttu-id="e9120-104">여 [Tom Dykstra](https://github.com/tdykstra) 및 [Andrew Stanton 간호사](https://github.com/anurse)</span><span class="sxs-lookup"><span data-stu-id="e9120-104">By [Tom Dykstra](https://github.com/tdykstra) and [Andrew Stanton-Nurse](https://github.com/anurse)</span></span>

<span data-ttu-id="e9120-105">이 문서에는 ASP.NET Core에서 Websocket을 시작 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-105">This article explains how to get started with WebSockets in ASP.NET Core.</span></span> <span data-ttu-id="e9120-106">[WebSocket](https://wikipedia.org/wiki/WebSocket)은 TCP 연결을 통한 영구 양방향 통신 채널을 사용하도록 설정하는 프로토콜이며</span><span class="sxs-lookup"><span data-stu-id="e9120-106">[WebSocket](https://wikipedia.org/wiki/WebSocket) is a protocol that enables two-way persistent communication channels over TCP connections.</span></span> <span data-ttu-id="e9120-107">웹 응용 프로그램에서 실시간 기능이 원하는 곳을 채팅, 주식 종목, 게임 등의 응용 프로그램에 대 한 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-107">It is used for applications such as chat, stock tickers, games, anywhere you want real-time functionality in a web application.</span></span>

<span data-ttu-id="e9120-108">[보거나 다운로드 샘플 코드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample) ([다운로드 하는 방법을](xref:tutorials/index#how-to-download-a-sample)).</span><span class="sxs-lookup"><span data-stu-id="e9120-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample)).</span></span> <span data-ttu-id="e9120-109">참조는 [다음 단계](#next-steps) 한 자세 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-109">See the [Next Steps](#next-steps) section for more information.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e9120-110">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="e9120-110">Prerequisites</span></span>

* <span data-ttu-id="e9120-111">ASP.NET Core 1.1 (1.0에 실행 되지 않습니다)</span><span class="sxs-lookup"><span data-stu-id="e9120-111">ASP.NET Core 1.1 (does not run on 1.0)</span></span>
* <span data-ttu-id="e9120-112">ASP.NET Core에서 실행 되는 모든 운영 체제:</span><span class="sxs-lookup"><span data-stu-id="e9120-112">Any OS that ASP.NET Core runs on:</span></span>
  
  * <span data-ttu-id="e9120-113">Windows 7 / Windows Server 2008 이상</span><span class="sxs-lookup"><span data-stu-id="e9120-113">Windows 7 / Windows Server 2008 and later</span></span>
  * <span data-ttu-id="e9120-114">Linux</span><span class="sxs-lookup"><span data-stu-id="e9120-114">Linux</span></span>
  * <span data-ttu-id="e9120-115">macOS</span><span class="sxs-lookup"><span data-stu-id="e9120-115">macOS</span></span>

* <span data-ttu-id="e9120-116">**예외**: iis에서 Windows에서 앱 실행 되거나 WebListener를 사용 해야 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="e9120-116">**Exception**: If your app runs on Windows with IIS, or with WebListener, you must use:</span></span>

  * <span data-ttu-id="e9120-117">Windows 8 / Windows Server 2012 이상</span><span class="sxs-lookup"><span data-stu-id="e9120-117">Windows 8 / Windows Server 2012 or later</span></span>
  * <span data-ttu-id="e9120-118">IIS 8 / IIS 8 Express</span><span class="sxs-lookup"><span data-stu-id="e9120-118">IIS 8 / IIS 8 Express</span></span>
  * <span data-ttu-id="e9120-119">IIS에서 WebSocket은 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-119">WebSocket must be enabled in IIS</span></span>

* <span data-ttu-id="e9120-120">지원 되는 브라우저 http://caniuse.com/#feat=websockets를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e9120-120">For supported browsers, see http://caniuse.com/#feat=websockets.</span></span>

## <a name="when-to-use-it"></a><span data-ttu-id="e9120-121">용도</span><span class="sxs-lookup"><span data-stu-id="e9120-121">When to use it</span></span>

<span data-ttu-id="e9120-122">소켓 연결으로 직접 작업 해야 할 때 Websocket을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-122">Use WebSockets when you need to work directly with a socket connection.</span></span> <span data-ttu-id="e9120-123">예를 들어 실시간 게임에 대 한 가능한 최상의 성능을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-123">For example, you might need the best possible performance for a real-time game.</span></span>

<span data-ttu-id="e9120-124">[ASP.NET SignalR](https://docs.microsoft.com/aspnet/signalr/overview/getting-started/introduction-to-signalr) 풍부 제공 하지만 실시간 기능에 대 한 응용 프로그램 모델 ASP.NET에서는 ASP.NET Core 하지 에서만 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-124">[ASP.NET SignalR](https://docs.microsoft.com/aspnet/signalr/overview/getting-started/introduction-to-signalr) provides a richer application model for real-time functionality, but it runs only on ASP.NET, not ASP.NET Core.</span></span> <span data-ttu-id="e9120-125">SignalR의 핵심 버전은 개발; 진행 상황을 수행 하려면 참조는 [SignalR Core 용 GitHub 리포지토리](https://github.com/aspnet/SignalR)합니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-125">A Core version of SignalR is under development; to follow its progress, see the [GitHub repository for SignalR Core](https://github.com/aspnet/SignalR).</span></span>

<span data-ttu-id="e9120-126">SignalR Core 기다려야 않으려면 이제 사용할 수 있습니다 Websocket 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-126">If you don't want to wait for SignalR Core, you can use WebSockets directly now.</span></span> <span data-ttu-id="e9120-127">하지만 SignalR 제공할와 같은 기능을 개발 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-127">But you might have to develop features that SignalR would provide, such as:</span></span>

* <span data-ttu-id="e9120-128">광범위 한 대체 전송 방법으로 자동 대체를 사용 하 여 브라우저 버전을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-128">Support for a broader range of browser versions by using automatic fallback to alternative transport methods.</span></span>
* <span data-ttu-id="e9120-129">자동 다시 연결은 연결을 삭제 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-129">Automatic reconnection when a connection drops.</span></span>
* <span data-ttu-id="e9120-130">서버에서 또는 그 반대로 메서드를 호출 하는 클라이언트에 대해 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-130">Support for clients calling methods on the server or vice versa.</span></span>
* <span data-ttu-id="e9120-131">여러 서버에 맞게 크기 조정 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-131">Support for scaling to multiple servers.</span></span>

## <a name="how-to-use-it"></a><span data-ttu-id="e9120-132">사용 방법</span><span class="sxs-lookup"><span data-stu-id="e9120-132">How to use it</span></span>

* <span data-ttu-id="e9120-133">설치는 [Microsoft.AspNetCore.WebSockets](https://www.nuget.org/packages/Microsoft.AspNetCore.WebSockets/) 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-133">Install the [Microsoft.AspNetCore.WebSockets](https://www.nuget.org/packages/Microsoft.AspNetCore.WebSockets/) package.</span></span>
* <span data-ttu-id="e9120-134">미들웨어를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-134">Configure the middleware.</span></span>
* <span data-ttu-id="e9120-135">WebSocket 요청을 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-135">Accept WebSocket requests.</span></span>
* <span data-ttu-id="e9120-136">메시지 보내기 및 받기.</span><span class="sxs-lookup"><span data-stu-id="e9120-136">Send and receive messages.</span></span>

### <a name="configure-the-middleware"></a><span data-ttu-id="e9120-137">미들웨어를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-137">Configure the middleware</span></span>

<span data-ttu-id="e9120-138">Websocket 미들웨어에서 추가 `Configure` 의 메서드는 `Startup` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-138">Add the WebSockets middleware in the `Configure` method of the `Startup` class.</span></span>

[!code-csharp[](websockets/sample/Startup.cs?name=UseWebSockets)]

<span data-ttu-id="e9120-139">다음 설정은 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-139">The following settings can be configured:</span></span>

* <span data-ttu-id="e9120-140">`KeepAliveInterval`-프록시 연결을 유지 하도록 클라이언트에 "ping" 프레임을 보낼 빈도를 사용 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-140">`KeepAliveInterval` - How frequently to send "ping" frames to the client, to ensure proxies keep the connection open.</span></span>
* <span data-ttu-id="e9120-141">`ReceiveBufferSize`-데이터를 수신 하는 데 사용 되는 버퍼의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-141">`ReceiveBufferSize` - The size of the buffer used to receive data.</span></span> <span data-ttu-id="e9120-142">고급 사용자만 자신의 데이터의 크기에 따라 성능 튜닝에이 변경할 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-142">Only advanced users would need to change this, for performance tuning based on the size of their data.</span></span>

[!code-csharp[](websockets/sample/Startup.cs?name=UseWebSocketsOptions)]

### <a name="accept-websocket-requests"></a><span data-ttu-id="e9120-143">WebSocket 요청을 수락</span><span class="sxs-lookup"><span data-stu-id="e9120-143">Accept WebSocket requests</span></span>

<span data-ttu-id="e9120-144">요청 라이프 사이클의 뒷부분에 있는 위치 (의 뒷부분에 나오는 `Configure` 메서드 또는 예를 들어 MVC 동작에서) WebSocket 요청 인지 확인 하 고 들어오는 WebSocket 요청을 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-144">Somewhere later in the request life cycle (later in the `Configure` method or in an MVC action, for example) check if it's a WebSocket request and accept the WebSocket request.</span></span>

<span data-ttu-id="e9120-145">이 예제는에서 나중에 `Configure` 메서드.</span><span class="sxs-lookup"><span data-stu-id="e9120-145">This example is from later in the `Configure` method.</span></span>

[!code-csharp[](websockets/sample/Startup.cs?name=AcceptWebSocket&highlight=7)]

<span data-ttu-id="e9120-146">WebSocket 요청에 모든 URL 일 수도 있지만이 샘플 코드에 대 한 요청은 허용 `/ws`합니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-146">A WebSocket request could come in on any URL, but this sample code only accepts requests for `/ws`.</span></span>

### <a name="send-and-receive-messages"></a><span data-ttu-id="e9120-147">메시지 보내기 및 받기</span><span class="sxs-lookup"><span data-stu-id="e9120-147">Send and receive messages</span></span>

<span data-ttu-id="e9120-148">`AcceptWebSocketAsync` 메서드는 WebSocket 연결에 TCP 연결을 업그레이드 하 고 제공 된 [WebSocket](https://docs.microsoft.com/dotnet/core/api/system.net.websockets.websocket) 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-148">The `AcceptWebSocketAsync` method upgrades the TCP connection to a WebSocket connection and gives you a [WebSocket](https://docs.microsoft.com/dotnet/core/api/system.net.websockets.websocket) object.</span></span> <span data-ttu-id="e9120-149">메시지를 받거나 보내기 위해 WebSocket 개체를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-149">Use the WebSocket object to send and receive messages.</span></span>

<span data-ttu-id="e9120-150">WebSocket 요청을 수락 하는 앞에 표시 된 코드에서 전달 된 `WebSocket` 개체를 `Echo` 방법으로, 여기는 `Echo` 메서드.</span><span class="sxs-lookup"><span data-stu-id="e9120-150">The code shown earlier that accepts the WebSocket request passes the `WebSocket` object to an `Echo` method; here's the `Echo` method.</span></span> <span data-ttu-id="e9120-151">코드는 메시지를 수신 하 고 동일한 메시지를 즉시 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-151">The code receives a message and immediately sends back the same message.</span></span> <span data-ttu-id="e9120-152">클라이언트가 연결을 닫을 때까지 작업을 수행 하는 루프에 보관 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-152">It stays in a loop doing that until the client closes the connection.</span></span> 

[!code-csharp[](websockets/sample/Startup.cs?name=Echo)]

<span data-ttu-id="e9120-153">WebSocket이이 루프를 시작 하기 전에 수락 하면 미들웨어 파이프라인 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-153">When you accept the WebSocket before beginning this loop, the middleware pipeline ends.</span></span>  <span data-ttu-id="e9120-154">소켓을 닫을 때 파이프라인을 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-154">Upon closing the socket, the pipeline unwinds.</span></span> <span data-ttu-id="e9120-155">즉,와 마찬가지로 WebSocket을 수락 하면 파이프라인에서 앞으로 이동 하 여 요청 중지 예를 들어 MVC 동작의 경우에 도달 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-155">That is, the request stops moving forward in the pipeline when you accept a WebSocket, just as it would when you hit an MVC action, for example.</span></span>  <span data-ttu-id="e9120-156">하지만 요청 파이프라인 백업 진행이 루프 끝나고 소켓을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-156">But when you finish this loop and close the socket, the request proceeds back up the pipeline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9120-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e9120-157">Next steps</span></span>

<span data-ttu-id="e9120-158">[샘플 응용 프로그램](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample) 이 함께 제공 되는 문서는 간단한 에코 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-158">The [sample application](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample) that accompanies this article is a simple echo application.</span></span> <span data-ttu-id="e9120-159">WebSocket 연결 하는 웹 페이지가 고 서버 항목만 다시 클라이언트에 수신 된 모든 메시지.</span><span class="sxs-lookup"><span data-stu-id="e9120-159">It has a web page that makes WebSocket connections, and the server just resends back to the client any messages it receives.</span></span> <span data-ttu-id="e9120-160">(해당 설정 있지 않은 IIS Express와 Visual Studio에서 실행) 하는 명령 프롬프트에서 실행 http://localhost:5000로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-160">Run it from a command prompt (it's not set up to run from Visual Studio with IIS Express) and navigate to http://localhost:5000.</span></span> <span data-ttu-id="e9120-161">웹 페이지 왼쪽 위에 연결 상태를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-161">The web page shows connection status at the upper left:</span></span>

![웹 페이지의 초기 상태](websockets/_static/start.png)

<span data-ttu-id="e9120-163">선택 **연결** WebSocket 요청에 표시 된 URL을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-163">Select **Connect** to send a WebSocket request to the URL shown.</span></span>  <span data-ttu-id="e9120-164">테스트 메시지를 입력 하 고 선택 **보낼**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-164">Enter a test message and select **Send**.</span></span> <span data-ttu-id="e9120-165">을 완료 한 후 선택 **닫기 소켓**합니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-165">When done, select **Close Socket**.</span></span> <span data-ttu-id="e9120-166">**통신 로그** 섹션 열려 전송할 때마다를 보고 하 고 발생 하는 것으로 닫기 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9120-166">The **Communication Log** section reports each open, send, and close action as it happens.</span></span>

![웹 페이지의 초기 상태](websockets/_static/end.png)
