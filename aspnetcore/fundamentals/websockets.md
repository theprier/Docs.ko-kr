---
title: "ASP.NET Core에서 WebSocket 지원"
author: tdykstra
description: "ASP.NET Core에서 WebSocket을 시작하는 방법을 알아봅니다."
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
# <a name="introduction-to-websockets-in-aspnet-core"></a><span data-ttu-id="b3da0-103">ASP.NET Core에서 WebSocket 소개</span><span class="sxs-lookup"><span data-stu-id="b3da0-103">Introduction to WebSockets in ASP.NET Core</span></span>

<span data-ttu-id="b3da0-104">작성자: [Tom Dykstra](https://github.com/tdykstra) 및 [Andrew Stanton-Nurse](https://github.com/anurse)</span><span class="sxs-lookup"><span data-stu-id="b3da0-104">By [Tom Dykstra](https://github.com/tdykstra) and [Andrew Stanton-Nurse](https://github.com/anurse)</span></span>

<span data-ttu-id="b3da0-105">이 문서는 ASP.NET Core에서 WebSocket을 시작하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-105">This article explains how to get started with WebSockets in ASP.NET Core.</span></span> <span data-ttu-id="b3da0-106">[WebSocket](https://wikipedia.org/wiki/WebSocket)은 TCP 연결을 통한 영구 양방향 통신 채널을 사용하도록 설정하는 프로토콜이며</span><span class="sxs-lookup"><span data-stu-id="b3da0-106">[WebSocket](https://wikipedia.org/wiki/WebSocket) is a protocol that enables two-way persistent communication channels over TCP connections.</span></span> <span data-ttu-id="b3da0-107">채팅, 주식 종목, 게임, 웹 응용 프로그램의 실시간 기능을 사용하려는 곳 등 응용 프로그램에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-107">It's used for applications such as chat, stock tickers, games, anywhere you want real-time functionality in a web application.</span></span>

<span data-ttu-id="b3da0-108">[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="b3da0-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample)).</span></span> <span data-ttu-id="b3da0-109">자세한 내용은 [다음 단계](#next-steps) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3da0-109">See the [Next Steps](#next-steps) section for more information.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="b3da0-110">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="b3da0-110">Prerequisites</span></span>

* <span data-ttu-id="b3da0-111">ASP.NET Core 1.1(1.0에서 실행되지 않음)</span><span class="sxs-lookup"><span data-stu-id="b3da0-111">ASP.NET Core 1.1 (doesn't run on 1.0)</span></span>
* <span data-ttu-id="b3da0-112">ASP.NET Core를 실행하는 OS:</span><span class="sxs-lookup"><span data-stu-id="b3da0-112">Any OS that ASP.NET Core runs on:</span></span>
  
  * <span data-ttu-id="b3da0-113">Windows 7 / Windows Server 2008 이상</span><span class="sxs-lookup"><span data-stu-id="b3da0-113">Windows 7 / Windows Server 2008 and later</span></span>
  * <span data-ttu-id="b3da0-114">Linux</span><span class="sxs-lookup"><span data-stu-id="b3da0-114">Linux</span></span>
  * <span data-ttu-id="b3da0-115">macOS</span><span class="sxs-lookup"><span data-stu-id="b3da0-115">macOS</span></span>

* <span data-ttu-id="b3da0-116">**예외**: 앱이 IIS 또는 WebListener와 함께 Windows에서 실행되는 경우 다음을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-116">**Exception**: If your app runs on Windows with IIS, or with WebListener, you must use:</span></span>

  * <span data-ttu-id="b3da0-117">Windows 8 / Windows Server 2012 이상</span><span class="sxs-lookup"><span data-stu-id="b3da0-117">Windows 8 / Windows Server 2012 or later</span></span>
  * <span data-ttu-id="b3da0-118">IIS 8 / IIS 8 Express</span><span class="sxs-lookup"><span data-stu-id="b3da0-118">IIS 8 / IIS 8 Express</span></span>
  * <span data-ttu-id="b3da0-119">WebSocket은 IIS에서 활성화되어야 함</span><span class="sxs-lookup"><span data-stu-id="b3da0-119">WebSocket must be enabled in IIS</span></span>

* <span data-ttu-id="b3da0-120">지원되는 브라우저는 http://caniuse.com/#feat=websockets를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3da0-120">For supported browsers, see http://caniuse.com/#feat=websockets.</span></span>

## <a name="when-to-use-it"></a><span data-ttu-id="b3da0-121">용도</span><span class="sxs-lookup"><span data-stu-id="b3da0-121">When to use it</span></span>

<span data-ttu-id="b3da0-122">소켓 연결로 직접 작업해야 하는 경우 WebSocket을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-122">Use WebSockets when you need to work directly with a socket connection.</span></span> <span data-ttu-id="b3da0-123">예를 들어 실시간 게임에 최상의 가능한 성능이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-123">For example, you might need the best possible performance for a real-time game.</span></span>

<span data-ttu-id="b3da0-124">[ASP.NET SignalR](https://docs.microsoft.com/aspnet/signalr/overview/getting-started/introduction-to-signalr)은 실시간 기능에 대한 풍부한 응용 프로그램 모델을 제공하지만 ASP.NET Core가 아닌 ASP.NET에서만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-124">[ASP.NET SignalR](https://docs.microsoft.com/aspnet/signalr/overview/getting-started/introduction-to-signalr) provides a richer application model for real-time functionality, but it runs only on ASP.NET, not ASP.NET Core.</span></span> <span data-ttu-id="b3da0-125">SignalR의 핵심 버전은 해당 진행을 따르도록 개발 중이며 [SignalR Core용 GitHub 리포지토리](https://github.com/aspnet/SignalR)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3da0-125">A Core version of SignalR is under development; to follow its progress, see the [GitHub repository for SignalR Core](https://github.com/aspnet/SignalR).</span></span>

<span data-ttu-id="b3da0-126">SignalR Core를 기다리지 않으려는 경우 이제 WebSocket을 직접 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-126">If you don't want to wait for SignalR Core, you can use WebSockets directly now.</span></span> <span data-ttu-id="b3da0-127">하지만 다음과 같은 SignalR에서 제공하는 기능을 개발해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-127">But you might have to develop features that SignalR would provide, such as:</span></span>

* <span data-ttu-id="b3da0-128">대체 전송 방법에 대한 자동 대체를 사용하여 광범위한 브라우저 버전에 대한 지원</span><span class="sxs-lookup"><span data-stu-id="b3da0-128">Support for a broader range of browser versions by using automatic fallback to alternative transport methods.</span></span>
* <span data-ttu-id="b3da0-129">연결이 끊어지는 경우 자동 다시 연결</span><span class="sxs-lookup"><span data-stu-id="b3da0-129">Automatic reconnection when a connection drops.</span></span>
* <span data-ttu-id="b3da0-130">서버에서 메서드(또는 그 반대로)를 호출하는 클라이언트에 대한 지원</span><span class="sxs-lookup"><span data-stu-id="b3da0-130">Support for clients calling methods on the server or vice versa.</span></span>
* <span data-ttu-id="b3da0-131">여러 서버에 맞게 크기 조정에 대한 지원</span><span class="sxs-lookup"><span data-stu-id="b3da0-131">Support for scaling to multiple servers.</span></span>

## <a name="how-to-use-it"></a><span data-ttu-id="b3da0-132">사용 방법</span><span class="sxs-lookup"><span data-stu-id="b3da0-132">How to use it</span></span>

* <span data-ttu-id="b3da0-133">[Microsoft.AspNetCore.WebSockets](https://www.nuget.org/packages/Microsoft.AspNetCore.WebSockets/) 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-133">Install the [Microsoft.AspNetCore.WebSockets](https://www.nuget.org/packages/Microsoft.AspNetCore.WebSockets/) package.</span></span>
* <span data-ttu-id="b3da0-134">미들웨어를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-134">Configure the middleware.</span></span>
* <span data-ttu-id="b3da0-135">WebSocket 요청을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-135">Accept WebSocket requests.</span></span>
* <span data-ttu-id="b3da0-136">메시지를 보내고 받습니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-136">Send and receive messages.</span></span>

### <a name="configure-the-middleware"></a><span data-ttu-id="b3da0-137">미들웨어 구성</span><span class="sxs-lookup"><span data-stu-id="b3da0-137">Configure the middleware</span></span>

<span data-ttu-id="b3da0-138">`Startup` 클래스의 `Configure` 메서드에 WebSocket 미들웨어를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-138">Add the WebSockets middleware in the `Configure` method of the `Startup` class.</span></span>

[!code-csharp[](websockets/sample/Startup.cs?name=UseWebSockets)]

<span data-ttu-id="b3da0-139">다음 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-139">The following settings can be configured:</span></span>

* <span data-ttu-id="b3da0-140">`KeepAliveInterval` - 프록시 연결을 유지하도록 클라이언트에 "ping" 프레임을 보낼 빈도</span><span class="sxs-lookup"><span data-stu-id="b3da0-140">`KeepAliveInterval` - How frequently to send "ping" frames to the client, to ensure proxies keep the connection open.</span></span>
* <span data-ttu-id="b3da0-141">`ReceiveBufferSize` - 데이터를 수신하는 데 사용되는 버퍼의 크기</span><span class="sxs-lookup"><span data-stu-id="b3da0-141">`ReceiveBufferSize` - The size of the buffer used to receive data.</span></span> <span data-ttu-id="b3da0-142">고급 사용자만 자신의 데이터의 크기에 따라 성능 튜닝에 대해 이를 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-142">Only advanced users would need to change this, for performance tuning based on the size of their data.</span></span>

[!code-csharp[](websockets/sample/Startup.cs?name=UseWebSocketsOptions)]

### <a name="accept-websocket-requests"></a><span data-ttu-id="b3da0-143">WebSocket 요청 수락</span><span class="sxs-lookup"><span data-stu-id="b3da0-143">Accept WebSocket requests</span></span>

<span data-ttu-id="b3da0-144">요청 수명 주기의 뒷부분(예: `Configure` 메서드 또는 MVC 동작의 뒷부분)에서 WebSocket 요청인지 확인하고 WebSocket 요청을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-144">Somewhere later in the request life cycle (later in the `Configure` method or in an MVC action, for example) check if it's a WebSocket request and accept the WebSocket request.</span></span>

<span data-ttu-id="b3da0-145">이 예제는 `Configure` 메서드의 뒷부분에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-145">This example is from later in the `Configure` method.</span></span>

[!code-csharp[](websockets/sample/Startup.cs?name=AcceptWebSocket&highlight=7)]

<span data-ttu-id="b3da0-146">WebSocket 요청은 모든 URL에서 올 수도 있지만 이 샘플 코드는 `/ws`에 대한 요청만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-146">A WebSocket request could come in on any URL, but this sample code only accepts requests for `/ws`.</span></span>

### <a name="send-and-receive-messages"></a><span data-ttu-id="b3da0-147">메시지 보내기 및 받기</span><span class="sxs-lookup"><span data-stu-id="b3da0-147">Send and receive messages</span></span>

<span data-ttu-id="b3da0-148">`AcceptWebSocketAsync` 메서드는 WebSocket 연결에 대한 TCP 연결을 업그레이드하고 [WebSocket](https://docs.microsoft.com/dotnet/core/api/system.net.websockets.websocket) 개체를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-148">The `AcceptWebSocketAsync` method upgrades the TCP connection to a WebSocket connection and gives you a [WebSocket](https://docs.microsoft.com/dotnet/core/api/system.net.websockets.websocket) object.</span></span> <span data-ttu-id="b3da0-149">WebSocket 개체를 사용하여 메시지를 보내고 받습니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-149">Use the WebSocket object to send and receive messages.</span></span>

<span data-ttu-id="b3da0-150">WebSocket 요청을 수락하는 앞에 표시된 코드에서 `WebSocket` 개체를 `Echo` 메서드에 전달합니다. 여기서는 `Echo` 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-150">The code shown earlier that accepts the WebSocket request passes the `WebSocket` object to an `Echo` method; here's the `Echo` method.</span></span> <span data-ttu-id="b3da0-151">코드는 메시지를 수신하고 동일한 메시지를 즉시 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-151">The code receives a message and immediately sends back the same message.</span></span> <span data-ttu-id="b3da0-152">클라이언트가 연결을 닫을 때까지 작업을 수행하는 루프에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-152">It stays in a loop doing that until the client closes the connection.</span></span> 

[!code-csharp[](websockets/sample/Startup.cs?name=Echo)]

<span data-ttu-id="b3da0-153">이 루프를 시작하기 전에 WebSocket을 수락하면 미들웨어 파이프라인이 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-153">When you accept the WebSocket before beginning this loop, the middleware pipeline ends.</span></span>  <span data-ttu-id="b3da0-154">소켓을 닫을 때 파이프라인이 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-154">Upon closing the socket, the pipeline unwinds.</span></span> <span data-ttu-id="b3da0-155">즉, 예를 들어 MVC 작업을 적중할 때 수행하는 것과 마찬가지로 WebSocket을 수락하면 요청은 파이프라인에서 앞으로 이동을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-155">That is, the request stops moving forward in the pipeline when you accept a WebSocket, just as it would when you hit an MVC action, for example.</span></span>  <span data-ttu-id="b3da0-156">하지만 이 루프를 마치고 소켓을 닫으면 요청에서 파이프라인 백업을 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-156">But when you finish this loop and close the socket, the request proceeds back up the pipeline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3da0-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b3da0-157">Next steps</span></span>

<span data-ttu-id="b3da0-158">이 문서와 함께 제공되는 [샘플 응용 프로그램](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample)은 간단한 에코 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-158">The [sample application](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample) that accompanies this article is a simple echo application.</span></span> <span data-ttu-id="b3da0-159">WebSocket 연결을 설정하는 웹 페이지가 있으며 서버는 수신하는 모든 메시지를 클라이언트에 다시 전송하기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-159">It has a web page that makes WebSocket connections, and the server just resends back to the client any messages it receives.</span></span> <span data-ttu-id="b3da0-160">명령 프롬프트에서 실행하고(IIS Express로 Visual Studio에서 실행하도록 설정되지 않음) http://localhost:5000으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-160">Run it from a command prompt (it's not set up to run from Visual Studio with IIS Express) and navigate to http://localhost:5000.</span></span> <span data-ttu-id="b3da0-161">웹 페이지는 왼쪽 위에 연결 상태를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-161">The web page shows connection status at the upper left:</span></span>

![웹 페이지의 초기 상태](websockets/_static/start.png)

<span data-ttu-id="b3da0-163">**연결**을 선택하여 표시된 URL에 WebSocket 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-163">Select **Connect** to send a WebSocket request to the URL shown.</span></span>  <span data-ttu-id="b3da0-164">테스트 메시지를 입력하고 **보내기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-164">Enter a test message and select **Send**.</span></span> <span data-ttu-id="b3da0-165">완료한 후 **소켓 닫기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-165">When done, select **Close Socket**.</span></span> <span data-ttu-id="b3da0-166">**통신 로그** 섹션은 발생하는 대로 열기, 보내기 및 닫기 작업을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="b3da0-166">The **Communication Log** section reports each open, send, and close action as it happens.</span></span>

![웹 페이지의 초기 상태](websockets/_static/end.png)
