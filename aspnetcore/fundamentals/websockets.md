---
title: "ASP.NET Core에서 WebSocket 지원"
author: tdykstra
description: "ASP.NET Core에서 Websocket을 시작하는 방법을 알아봅니다."
manager: wpickett
ms.author: tdykstra
ms.date: 03/25/2017
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/websockets
ms.openlocfilehash: 306eca28b9f1f66e1ccaf185ccae87db8dea1b01
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="introduction-to-websockets-in-aspnet-core"></a><span data-ttu-id="93391-103">ASP.NET Core의 Websocket 살펴보기</span><span class="sxs-lookup"><span data-stu-id="93391-103">Introduction to WebSockets in ASP.NET Core</span></span>

<span data-ttu-id="93391-104">작성자: [Tom Dykstra](https://github.com/tdykstra) 및 [Andrew Stanton-Nurse](https://github.com/anurse)</span><span class="sxs-lookup"><span data-stu-id="93391-104">By [Tom Dykstra](https://github.com/tdykstra) and [Andrew Stanton-Nurse](https://github.com/anurse)</span></span>

<span data-ttu-id="93391-105">본문에서는 ASP.NET Core에서 Websocket을 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="93391-105">This article explains how to get started with WebSockets in ASP.NET Core.</span></span> <span data-ttu-id="93391-106">[WebSocket](https://wikipedia.org/wiki/WebSocket) 은 TCP 연결을 통해서 지속적인 양방향 통신 채널을 사용할 수 있도록 해주는 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="93391-106">[WebSocket](https://wikipedia.org/wiki/WebSocket) is a protocol that enables two-way persistent communication channels over TCP connections.</span></span> <span data-ttu-id="93391-107">채팅, 주식 전광판, 게임 등 웹 응용 프로그램 전반에서 실시간 기능이 필요한 모든 곳에 활용됩니다.</span><span class="sxs-lookup"><span data-stu-id="93391-107">It's used for applications such as chat, stock tickers, games, anywhere you want real-time functionality in a web application.</span></span>

<span data-ttu-id="93391-108">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample) ([다운로드 방법](xref:tutorials/index#how-to-download-a-sample)).</span><span class="sxs-lookup"><span data-stu-id="93391-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample)).</span></span> <span data-ttu-id="93391-109">예제 코드에 관한 보다 자세한 내용은 [다음 단계](#next-steps) 섹션을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="93391-109">See the [Next Steps](#next-steps) section for more information.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="93391-110">전제 조건</span><span class="sxs-lookup"><span data-stu-id="93391-110">Prerequisites</span></span>

* <span data-ttu-id="93391-111">ASP.NET Core 1.1 (1.0에서는 실행되지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="93391-111">ASP.NET Core 1.1 (doesn't run on 1.0)</span></span>
* <span data-ttu-id="93391-112">ASP.NET Core가 실행되는 모든 OS:</span><span class="sxs-lookup"><span data-stu-id="93391-112">Any OS that ASP.NET Core runs on:</span></span>
  
  * <span data-ttu-id="93391-113">Windows 7 / Windows Server 2008 이상</span><span class="sxs-lookup"><span data-stu-id="93391-113">Windows 7 / Windows Server 2008 and later</span></span>
  * <span data-ttu-id="93391-114">Linux</span><span class="sxs-lookup"><span data-stu-id="93391-114">Linux</span></span>
  * <span data-ttu-id="93391-115">macOS</span><span class="sxs-lookup"><span data-stu-id="93391-115">macOS</span></span>

* <span data-ttu-id="93391-116">**예외**: Windows에서 IIS 또는 WebListener를 통해서 앱을 실행한다면 다음을 만족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93391-116">**Exception**: If your app runs on Windows with IIS, or with WebListener, you must use:</span></span>

  * <span data-ttu-id="93391-117">Windows 8 / Windows Server 2012 이상</span><span class="sxs-lookup"><span data-stu-id="93391-117">Windows 8 / Windows Server 2012 or later</span></span>
  * <span data-ttu-id="93391-118">IIS 8 / IIS 8 Express</span><span class="sxs-lookup"><span data-stu-id="93391-118">IIS 8 / IIS 8 Express</span></span>
  * <span data-ttu-id="93391-119">IIS에서 WebSocket을 활성화시켜야 합니다</span><span class="sxs-lookup"><span data-stu-id="93391-119">WebSocket must be enabled in IIS</span></span>

* <span data-ttu-id="93391-120">지원 브라우저에 관한 정보는 http://caniuse.com/#feat=websockets을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="93391-120">For supported browsers, see http://caniuse.com/#feat=websockets.</span></span>

## <a name="when-to-use-it"></a><span data-ttu-id="93391-121">용도</span><span class="sxs-lookup"><span data-stu-id="93391-121">When to use it</span></span>

<span data-ttu-id="93391-122">소켓 연결을 통해서 직접 작업을 처리해야 할 때, Websocket을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93391-122">Use WebSockets when you need to work directly with a socket connection.</span></span> <span data-ttu-id="93391-123">예를 들어, 실시간 게임에서 최상의 성능이 필요할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93391-123">For example, you might need the best possible performance for a real-time game.</span></span>

<span data-ttu-id="93391-124">[ASP.NET SignalR](https://docs.microsoft.com/aspnet/signalr/overview/getting-started/introduction-to-signalr) 은 실시간 기능을 지원하는 보다 풍부한 응용 프로그램 모델을 제공하지만 ASP.NET에서만 실행되며 ASP.NET Core에서는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="93391-124">[ASP.NET SignalR](https://docs.microsoft.com/aspnet/signalr/overview/getting-started/introduction-to-signalr) provides a richer application model for real-time functionality, but it runs only on ASP.NET, not ASP.NET Core.</span></span> <span data-ttu-id="93391-125">SignalR의 Core 버전은 현재 개발중으로, 개발 진행 상황을 확인하려면 [SignalR Core의 GitHub 저장소](https://github.com/aspnet/SignalR) 를 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="93391-125">A Core version of SignalR is under development; to follow its progress, see the [GitHub repository for SignalR Core](https://github.com/aspnet/SignalR).</span></span>

<span data-ttu-id="93391-126">SignalR Core를 기다리고 싶지 않다면, 대신 지금 바로 WebSocket을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93391-126">If you don't want to wait for SignalR Core, you can use WebSockets directly now.</span></span> <span data-ttu-id="93391-127">그러나 SignalR이 제공하는 다음과 같은 기능들을 직접 개발해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93391-127">But you might have to develop features that SignalR would provide, such as:</span></span>

* <span data-ttu-id="93391-128">대체 전송 방식에 대한 자동 폴백을 통해서 보다 다양한 브라우저 버전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="93391-128">Support for a broader range of browser versions by using automatic fallback to alternative transport methods.</span></span>
* <span data-ttu-id="93391-129">연결이 끊어지면 자동으로 다시 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="93391-129">Automatic reconnection when a connection drops.</span></span>
* <span data-ttu-id="93391-130">서버의 메서드를 호출하는 클라이언트, 또는 반대로 클라이언트의 메서드를 호출하는 서버를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="93391-130">Support for clients calling methods on the server or vice versa.</span></span>
* <span data-ttu-id="93391-131">여러 서버에 대한 확장을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="93391-131">Support for scaling to multiple servers.</span></span>

## <a name="how-to-use-it"></a><span data-ttu-id="93391-132">사용 방법</span><span class="sxs-lookup"><span data-stu-id="93391-132">How to use it</span></span>

* <span data-ttu-id="93391-133">[Microsoft.AspNetCore.WebSockets](https://www.nuget.org/packages/Microsoft.AspNetCore.WebSockets/) 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="93391-133">Install the [Microsoft.AspNetCore.WebSockets](https://www.nuget.org/packages/Microsoft.AspNetCore.WebSockets/) package.</span></span>
* <span data-ttu-id="93391-134">미들웨어를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="93391-134">Configure the middleware.</span></span>
* <span data-ttu-id="93391-135">WebSocket 요청을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="93391-135">Accept WebSocket requests.</span></span>
* <span data-ttu-id="93391-136">메시지를 전송 및 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="93391-136">Send and receive messages.</span></span>

### <a name="configure-the-middleware"></a><span data-ttu-id="93391-137">미들웨어 구성하기</span><span class="sxs-lookup"><span data-stu-id="93391-137">Configure the middleware</span></span>

<span data-ttu-id="93391-138">`Startup` 클래스의 `Configure` 메서드에서 Websocket 미들웨어를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="93391-138">Add the WebSockets middleware in the `Configure` method of the `Startup` class.</span></span>

[!code-csharp[](websockets/sample/Startup.cs?name=UseWebSockets)]

<span data-ttu-id="93391-139">이때 다음과 같은 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93391-139">The following settings can be configured:</span></span>

* <span data-ttu-id="93391-140">`KeepAliveInterval` - 프록시가 클라이언트의 연결을 유지할 수 있도록 클라이언트로 "핑(ping)" 프레임을 전송하는 빈도입니다.</span><span class="sxs-lookup"><span data-stu-id="93391-140">`KeepAliveInterval` - How frequently to send "ping" frames to the client, to ensure proxies keep the connection open.</span></span>
* <span data-ttu-id="93391-141">`ReceiveBufferSize` - 데이터 수신에 사용되는 버퍼의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="93391-141">`ReceiveBufferSize` - The size of the buffer used to receive data.</span></span> <span data-ttu-id="93391-142">이 값은 데이터의 크기에 기반한 성능 튜닝이 필요할 경우, 고급 사용자만 변경하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="93391-142">Only advanced users would need to change this, for performance tuning based on the size of their data.</span></span>

[!code-csharp[](websockets/sample/Startup.cs?name=UseWebSocketsOptions)]

### <a name="accept-websocket-requests"></a><span data-ttu-id="93391-143">WebSocket 요청 수락하기</span><span class="sxs-lookup"><span data-stu-id="93391-143">Accept WebSocket requests</span></span>

<span data-ttu-id="93391-144">요청 수명 주기의 뒷부분에서 (예를 들어, `Configure` 메서드나 MVC 액션의 뒷부분에서) WebSocket 요청 여부를 확인하고 WebSocket 요청을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="93391-144">Somewhere later in the request life cycle (later in the `Configure` method or in an MVC action, for example) check if it's a WebSocket request and accept the WebSocket request.</span></span>

<span data-ttu-id="93391-145">다음은 `Configure` 메서드의 뒷부분에 나오는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="93391-145">This example is from later in the `Configure` method.</span></span>

[!code-csharp[](websockets/sample/Startup.cs?name=AcceptWebSocket&highlight=7)]

<span data-ttu-id="93391-146">WebSocket 요청은 모든 URL을 통해서 전달될 수 있지만, 이 예제 코드에서는 `/ws` 에 대한 요청만 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="93391-146">A WebSocket request could come in on any URL, but this sample code only accepts requests for `/ws`.</span></span>

### <a name="send-and-receive-messages"></a><span data-ttu-id="93391-147">메시지 보내기 및 받기</span><span class="sxs-lookup"><span data-stu-id="93391-147">Send and receive messages</span></span>

<span data-ttu-id="93391-148">`AcceptWebSocketAsync` 메서드는 WebSocket 연결에 대한 TCP 연결을 업그레이드하고 [WebSocket](https://docs.microsoft.com/dotnet/core/api/system.net.websockets.websocket) 개체를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="93391-148">The `AcceptWebSocketAsync` method upgrades the TCP connection to a WebSocket connection and gives you a [WebSocket](https://docs.microsoft.com/dotnet/core/api/system.net.websockets.websocket) object.</span></span> <span data-ttu-id="93391-149">WebSocket 개체를 사용하여 메시지를 보내고 받습니다.</span><span class="sxs-lookup"><span data-stu-id="93391-149">Use the WebSocket object to send and receive messages.</span></span>

<span data-ttu-id="93391-150">앞에서 살펴본 WebSocket 요청을 수락하는 코드는 `WebSocket` 개체를 `Echo` 메서드로 전달하는데, `Echo` 메서드의 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93391-150">The code shown earlier that accepts the WebSocket request passes the `WebSocket` object to an `Echo` method; here's the `Echo` method.</span></span> <span data-ttu-id="93391-151">코드는 메시지를 수신하고 동일한 메시지를 즉시 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="93391-151">The code receives a message and immediately sends back the same message.</span></span> <span data-ttu-id="93391-152">클라이언트가 연결을 닫을 때까지 작업을 수행하는 루프에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="93391-152">It stays in a loop doing that until the client closes the connection.</span></span> 

[!code-csharp[](websockets/sample/Startup.cs?name=Echo)]

<span data-ttu-id="93391-153">루프가 시작되기 전에 WebSocket을 수락하면 미들웨어 파이프라인이 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="93391-153">When you accept the WebSocket before beginning this loop, the middleware pipeline ends.</span></span>  <span data-ttu-id="93391-154">그리고 소켓을 닫으면 파이프라인이 풀립니다.</span><span class="sxs-lookup"><span data-stu-id="93391-154">Upon closing the socket, the pipeline unwinds.</span></span> <span data-ttu-id="93391-155">다시 말해서, 마치 MVC 액션을 실행할 때와 마찬가지로 WebSocket을 수락하면 요청이 파이프라인에서 더 이상 앞쪽으로 이동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93391-155">That is, the request stops moving forward in the pipeline when you accept a WebSocket, just as it would when you hit an MVC action, for example.</span></span>  <span data-ttu-id="93391-156">그러나 이 루프를 종료하고 소켓을 닫으면 파이프라인을 통해서 요청이 다시 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="93391-156">But when you finish this loop and close the socket, the request proceeds back up the pipeline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93391-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="93391-157">Next steps</span></span>

<span data-ttu-id="93391-158">본문과 함께 제공되는 [예제 응용 프로그램](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample) 은 간단한 에코 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="93391-158">The [sample application](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample) that accompanies this article is a simple echo application.</span></span> <span data-ttu-id="93391-159">WebSocket 연결을 생성하는 웹 페이지가 제공되며 서버는 수신한 메시지를 그대로 클라이언트로 재전송합니다.</span><span class="sxs-lookup"><span data-stu-id="93391-159">It has a web page that makes WebSocket connections, and the server just resends back to the client any messages it receives.</span></span> <span data-ttu-id="93391-160">명령 프롬프트에서 예제 응용 프로그램을 실행하고 (Visual Studio에서 IIS Express를 통해서 실행되도록 구성되지 않았습니다), 브라우저에서 http://localhost:5000으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="93391-160">Run it from a command prompt (it's not set up to run from Visual Studio with IIS Express) and navigate to http://localhost:5000.</span></span> <span data-ttu-id="93391-161">웹 페이지의 좌상단에는 현재 연결 상태가 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="93391-161">The web page shows connection status at the upper left:</span></span>

![웹 페이지의 초기 상태](websockets/_static/start.png)

<span data-ttu-id="93391-163">**Connect** 를 선택해서 지정한 URL로 WebSocket 요청을 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="93391-163">Select **Connect** to send a WebSocket request to the URL shown.</span></span>  <span data-ttu-id="93391-164">그리고 테스트 메시지를 입력한 다음 **Send** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93391-164">Enter a test message and select **Send**.</span></span> <span data-ttu-id="93391-165">테스트를 모두 마쳤으면 **Close Socket** 을 선택하십시오.</span><span class="sxs-lookup"><span data-stu-id="93391-165">When done, select **Close Socket**.</span></span> <span data-ttu-id="93391-166">**Communication Log** 섹션에는 각각의 열기, 전송 및 닫기 동작이 발생한 순서대로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="93391-166">The **Communication Log** section reports each open, send, and close action as it happens.</span></span>

![웹 페이지의 초기 상태](websockets/_static/end.png)
