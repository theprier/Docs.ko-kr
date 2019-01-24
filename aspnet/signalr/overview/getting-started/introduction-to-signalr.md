---
uid: signalr/overview/getting-started/introduction-to-signalr
title: SignalR 소개 | Microsoft Docs
author: bradygaster
description: 이 문서에서는 설명 SignalR 이란, 일부 솔루션을 만들도록 설계 되었습니다.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 0fab5e35-8c1f-43d4-8635-b8aba8766a71
msc.legacyurl: /signalr/overview/getting-started/introduction-to-signalr
msc.type: authoredcontent
ms.openlocfilehash: 7b9dae3e5d79319a9fefee41f4525a59f950746a
ms.sourcegitcommit: ebf4e5a7ca301af8494edf64f85d4a8deb61d641
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54837769"
---
<a name="introduction-to-signalr"></a><span data-ttu-id="bea1e-103">SignalR 소개</span><span class="sxs-lookup"><span data-stu-id="bea1e-103">Introduction to SignalR</span></span>
====================

<span data-ttu-id="bea1e-104">[Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="bea1e-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]


> <span data-ttu-id="bea1e-105">이 문서에서는 설명 SignalR 이란, 일부 솔루션을 만들도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-105">This article describes what SignalR is, and some of the solutions it was designed to create.</span></span> 
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="bea1e-106">질문이 나 의견이 있으면</span><span class="sxs-lookup"><span data-stu-id="bea1e-106">Questions and comments</span></span>
> 
> <span data-ttu-id="bea1e-107">이 자습서를 연결 하는 방법 및 새로운 개선할 수 있습니다 페이지의 맨 아래에 의견에서에 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="bea1e-107">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="bea1e-108">에 자습서로 직접 관련 되지 않은 질문이 있을 경우 게시할 수 하는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr)합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-108">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr).</span></span>

## <a name="what-is-signalr"></a><span data-ttu-id="bea1e-109">SignalR이란?</span><span class="sxs-lookup"><span data-stu-id="bea1e-109">What is SignalR?</span></span>

<span data-ttu-id="bea1e-110">ASP.NET SignalR은 ASP.NET 개발자를 위한 응용 프로그램에 실시간 웹 기능을 추가 하는 프로세스를 간소화 하는 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-110">ASP.NET SignalR is a library for ASP.NET developers that simplifies the process of adding real-time web functionality to applications.</span></span> <span data-ttu-id="bea1e-111">실시간 웹 기능은 서버 코드 푸시를 사용할 수 있게 되 면 즉시 연결 된 클라이언트에 콘텐츠 대신 서버는 클라이언트가 새 데이터를 요청을 대기 하는 기능을 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-111">Real-time web functionality is the ability to have server code push content to connected clients instantly as it becomes available, rather than having the server wait for a client to request new data.</span></span>

<span data-ttu-id="bea1e-112">SignalR은 ASP.NET 응용 프로그램에 모든 종류의 "실시간" 웹 기능을 추가 하려면 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-112">SignalR can be used to add any sort of "real-time" web functionality to your ASP.NET application.</span></span> <span data-ttu-id="bea1e-113">예를 들어 채팅 흔히 하는 동안 더 많은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-113">While chat is often used as an example, you can do a whole lot more.</span></span> <span data-ttu-id="bea1e-114">페이지 구현 또는 사용자 든 지 새 데이터를 보려면 웹 페이지를 새로 고칩니다 [긴 폴링](http://en.wikipedia.org/wiki/Push_technology#Long_polling) 새 데이터를 검색 하려면 SignalR을 사용 하 여에 대 한 대상 인지 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-114">Any time a user refreshes a web page to see new data, or the page implements [long polling](http://en.wikipedia.org/wiki/Push_technology#Long_polling) to retrieve new data, it is a candidate for using SignalR.</span></span> <span data-ttu-id="bea1e-115">예로 대시보드 및 진행 상황 업데이트 및 실시간 양식 (예: 동시 편집 문서의) 공동 작업 응용 프로그램 작업 응용 프로그램을 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-115">Examples include dashboards and monitoring applications, collaborative applications (such as simultaneous editing of documents), job progress updates, and real-time forms.</span></span>

<span data-ttu-id="bea1e-116">SignalR 있습니다 완전히 새로운 유형의 웹 응용 프로그램 서버에서 자주 업데이트 해야 하는 예를 들어, 실시간 게임입니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-116">SignalR also enables completely new types of web applications that require high frequency updates from the server, for example, real-time gaming.</span></span>

<span data-ttu-id="bea1e-117">SignalR 서버 쪽.NET 코드에서 브라우저 (및 다른 클라이언트 플랫폼) 클라이언트에서 JavaScript 함수를 호출 하는 서버와 클라이언트 간 원격 프로시저 호출 (RPC)을 만들기 위한 간단한 API를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-117">SignalR provides a simple API for creating server-to-client remote procedure calls (RPC) that call JavaScript functions in client browsers (and other client platforms) from server-side .NET code.</span></span> <span data-ttu-id="bea1e-118">또한 SignalR 연결 관리에 대 한 API를 포함 (예를 들어, 연결 및 연결 끊기 이벤트) 및 연결을 그룹화 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-118">SignalR also includes API for connection management (for instance, connect and disconnect events), and grouping connections.</span></span>

![SignalR 사용 하 여 메서드를 호출합니다.](introduction-to-signalr/_static/image1.png)

<span data-ttu-id="bea1e-120">SignalR 연결 관리를 자동으로 처리 하 고는 대화방 같은 각 항목 수 브로드캐스트 메시지 연결 된 모든 클라이언트를 동시에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-120">SignalR handles connection management automatically, and lets you broadcast messages to all connected clients simultaneously, like a chat room.</span></span> <span data-ttu-id="bea1e-121">또한 특정 클라이언트에 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-121">You can also send messages to specific clients.</span></span> <span data-ttu-id="bea1e-122">클라이언트와 서버 간의 연결이 영구적 이므로, 각 통신에 대 한 연결이 다시 설정 하는 클래식 HTTP 연결을 달리 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-122">The connection between the client and server is persistent, unlike a classic HTTP connection, which is re-established for each communication.</span></span>

<span data-ttu-id="bea1e-123">SignalR은 클라이언트 코드를 사용 하 여 일반적인 요청-응답 모델 보다는 원격 프로시저 호출 (RPC)는 웹에서 현재 브라우저에서 서버 코드 호출할 수 있습니다 "서버 푸시" 기능을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-123">SignalR supports "server push" functionality, in which server code can call out to client code in the browser using Remote Procedure Calls (RPC), rather than the request-response model common on the web today.</span></span>

<span data-ttu-id="bea1e-124">SignalR 응용 프로그램의 Service Bus, SQL Server를 사용 하 여 클라이언트를 확장할 수 또는 [Redis](http://redis.io)합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-124">SignalR applications can scale out to thousands of clients using Service Bus, SQL Server or [Redis](http://redis.io).</span></span>

<span data-ttu-id="bea1e-125">SignalR은 오픈 소스를 통해 액세스할 수 있습니다 [GitHub](https://github.com/signalr)합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-125">SignalR is open-source, accessible through [GitHub](https://github.com/signalr).</span></span>

## <a name="signalr-and-websocket"></a><span data-ttu-id="bea1e-126">SignalR 및 WebSocket</span><span class="sxs-lookup"><span data-stu-id="bea1e-126">SignalR and WebSocket</span></span>

<span data-ttu-id="bea1e-127">SignalR 사용 가능한 경우 새 WebSocket 전송 사용 및 필요한 경우 이전 전송으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-127">SignalR uses the new WebSocket transport where available and falls back to older transports where necessary.</span></span> <span data-ttu-id="bea1e-128">하지만 물론 직접 WebSocket을 사용 하 여, 많은 구현 해야 하는 추가 기능을 이미 수행 즉 SignalR을 사용 하 여 앱을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-128">While you could certainly write your app using WebSocket directly, using SignalR means that a lot of the extra functionality you would need to implement is already done for you.</span></span> <span data-ttu-id="bea1e-129">가장 중요 한 점은이 이전 버전의 클라이언트에 대 한 별도 코드 경로 생성 하는 방법에 대 한 걱정 없이 WebSocket을 활용 하려면 앱을 코딩할 수 있습니다 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-129">Most importantly, this means that you can code your app to take advantage of WebSocket without having to worry about creating a separate code path for older clients.</span></span> <span data-ttu-id="bea1e-130">SignalR도 보호 SignalR 기본 전송에 대 한 변경을 지원 하도록 업데이트 됩니다 WebSocket의 버전 간에 응용 프로그램을 일관 된 인터페이스를 제공 하므로 WebSocket에 대 한 업데이트에 걱정할 필요가 없도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-130">SignalR also shields you from having to worry about updates to WebSocket, since SignalR is updated to support changes in the underlying transport, providing your application a consistent interface across versions of WebSocket.</span></span>

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a><span data-ttu-id="bea1e-131">전송 및 대체</span><span class="sxs-lookup"><span data-stu-id="bea1e-131">Transports and fallbacks</span></span>

<span data-ttu-id="bea1e-132">SignalR은 클라이언트와 서버 간의 실시간 작업을 수행 하는 데 필요한 전송의 몇 가지 추상화입니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-132">SignalR is an abstraction over some of the transports that are required to do real-time work between client and server.</span></span> <span data-ttu-id="bea1e-133">SignalR 연결 HTTP로 시작 하 고 가능한 경우에 WebSocket 연결을 다음 승격 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-133">A SignalR connection starts as HTTP, and is then promoted to a WebSocket connection if it is available.</span></span> <span data-ttu-id="bea1e-134">서버 메모리의 가장 효율적인 사용, 낮은 대기 시간, 고 (예: 완전 한 이중 클라이언트와 서버 간 통신), 기능이 가장 기본 뿐만 아니라 가장 엄격한 되므로 WebSocket는 SignalR에 대 한 이상적인 전송 요구 사항: WebSocket을 사용 하려면 Windows Server 2012 또는 Windows 8 및.NET Framework 4.5로 서버.</span><span class="sxs-lookup"><span data-stu-id="bea1e-134">WebSocket is the ideal transport for SignalR, since it makes the most efficient use of server memory, has the lowest latency, and has the most underlying features (such as full duplex communication between client and server), but it also has the most stringent requirements: WebSocket requires the server to be using Windows Server 2012 or Windows 8, and .NET Framework 4.5.</span></span> <span data-ttu-id="bea1e-135">이러한 요구 사항을 충족 되지 않으면, SignalR 연결 되도록 다른 전송을 사용 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-135">If these requirements are not met, SignalR will attempt to use other transports to make its connections.</span></span>

### <a name="html-5-transports"></a><span data-ttu-id="bea1e-136">HTML 5 전송</span><span class="sxs-lookup"><span data-stu-id="bea1e-136">HTML 5 transports</span></span>

<span data-ttu-id="bea1e-137">이러한 전송에 대 한 지원에 따라 달라 집니다 [HTML 5](http://en.wikipedia.org/wiki/HTML5)합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-137">These transports depend on support for [HTML 5](http://en.wikipedia.org/wiki/HTML5).</span></span> <span data-ttu-id="bea1e-138">클라이언트 브라우저는 html5 표준을 지원 하지 않으면, 이전 전송이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-138">If the client browser does not support the HTML 5 standard, older transports will be used.</span></span>

- <span data-ttu-id="bea1e-139">**WebSocket** (하는 경우는 Websocket을 지원할 수 있는 서버 및 브라우저 표시).</span><span class="sxs-lookup"><span data-stu-id="bea1e-139">**WebSocket** (if the both the server and browser indicate they can support Websocket).</span></span> <span data-ttu-id="bea1e-140">WebSocket은 클라이언트와 서버 간에 true 영구 양방향 연결을 설정 하는 유일한 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-140">WebSocket is the only transport that establishes a true persistent, two-way connection between client and server.</span></span> <span data-ttu-id="bea1e-141">그러나, WebSocket에 요구 사항이 가장 엄격한; Microsoft Internet Explorer, Google Chrome 및 Mozilla Firefox의 최신 버전에만 완전히 지원 되 고 Opera 및 Safari와 같은 다른 브라우저에 부분적으로 구현만 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-141">However, WebSocket also has the most stringent requirements; it is fully supported only in the latest versions of Microsoft Internet Explorer, Google Chrome, and Mozilla Firefox, and only has a partial implementation in other browsers such as Opera and Safari.</span></span>
- <span data-ttu-id="bea1e-142">**서버 전송 이벤트**EventSource (브라우저에서 지 원하는 경우 서버 전송 이벤트는 기본적으로 Internet Explorer를 제외한 모든 브라우저)로 알려진,</span><span class="sxs-lookup"><span data-stu-id="bea1e-142">**Server Sent Events**, also known as EventSource (if the browser supports Server Sent Events, which is basically all browsers except Internet Explorer.)</span></span>

### <a name="comet-transports"></a><span data-ttu-id="bea1e-143">Comet 전송</span><span class="sxs-lookup"><span data-stu-id="bea1e-143">Comet transports</span></span>

<span data-ttu-id="bea1e-144">다음 전송에 기반한 합니다 [Comet](http://en.wikipedia.org/wiki/Comet_(programming)) 브라우저 또는 다른 클라이언트 유지 관리 하는 장기 보관 HTTP 요청을 서버에 특히 클라이언트는 클라이언트에 데이터 푸시를 사용할 수 있는 웹 응용 프로그램 모델 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-144">The following transports are based on the [Comet](http://en.wikipedia.org/wiki/Comet_(programming)) web application model, in which a browser or other client maintains a long-held HTTP request, which the server can use to push data to the client without the client specifically requesting it.</span></span>

- <span data-ttu-id="bea1e-145">**프레임 영원히** (예: Internet Explorer에만 해당).</span><span class="sxs-lookup"><span data-stu-id="bea1e-145">**Forever Frame** (for Internet Explorer only).</span></span> <span data-ttu-id="bea1e-146">영원히 프레임 완료 되지 않은 서버에서 끝점에 요청을 수행 하는 숨겨진된 IFrame을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-146">Forever Frame creates a hidden IFrame which makes a request to an endpoint on the server that does not complete.</span></span> <span data-ttu-id="bea1e-147">서버는 다음 스크립트가 클라이언트에 서버에서 단방향 실시간 연결을 제공 하는 즉시 실행 하는 클라이언트에 지속적으로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-147">The server then continually sends script to the client which is immediately executed, providing a one-way realtime connection from server to client.</span></span> <span data-ttu-id="bea1e-148">서버에 클라이언트에서 연결에서 클라이언트 연결을 서버에서 별도 연결을 사용 하 고 같은 표준 HTTP 요청을 전송 해야 하는 데이터의 각 부분에 대 한 새 연결을 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-148">The connection from client to server uses a separate connection from the server to client connection, and like a standard HTTP request, a new connection is created for each piece of data that needs to be sent.</span></span>
- <span data-ttu-id="bea1e-149">**긴 폴링 Ajax**합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-149">**Ajax long polling**.</span></span> <span data-ttu-id="bea1e-150">긴 폴링 영구 연결을 만들지는 않지만 대신이 시점에서 연결이 닫히고 서버 응답 하 고 새 연결을 즉시 요청 될 때까지 열린 상태로 유지 하는 요청을 사용 하 여 서버를 폴링합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-150">Long polling does not create a persistent connection, but instead polls the server with a request that stays open until the server responds, at which point the connection closes, and a new connection is requested immediately.</span></span> <span data-ttu-id="bea1e-151">연결 다시 설정 하는 동안 약간의 대기 시간이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-151">This may introduce some latency while the connection resets.</span></span>

<span data-ttu-id="bea1e-152">어떤 전송 되는 구성에서 지원 되는 자세한 내용은 [지원 되는 플랫폼](supported-platforms.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-152">For more information on what transports are supported under which configurations, see [Supported Platforms](supported-platforms.md).</span></span>

### <a name="transport-selection-process"></a><span data-ttu-id="bea1e-153">전송 선택 프로세스</span><span class="sxs-lookup"><span data-stu-id="bea1e-153">Transport selection process</span></span>

<span data-ttu-id="bea1e-154">다음 목록에는 SignalR 사용할 전송을 결정 하는 데 사용 하는 단계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-154">The following list shows the steps that SignalR uses to decide which transport to use.</span></span>

1. <span data-ttu-id="bea1e-155">브라우저를 Internet Explorer 8 이하의 경우 긴 폴링 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-155">If the browser is Internet Explorer 8 or earlier, Long Polling is used.</span></span>
2. <span data-ttu-id="bea1e-156">JSONP 구성 된 경우 (즉, 합니다 `jsonp` 매개 변수는 설정 `true` 연결을 시작할 때), 되 긴 폴링.</span><span class="sxs-lookup"><span data-stu-id="bea1e-156">If JSONP is configured (that is, the `jsonp` parameter is set to `true` when the connection is started), Long Polling is used.</span></span>
3. <span data-ttu-id="bea1e-157">(즉, SignalR 끝점에에서 없는 경우 호스팅 페이지와 동일한 도메인)는 도메인 간 연결이 설정 되는 경우 다음 WebSocket 사용한 다음 기준이 충족 될 경우:</span><span class="sxs-lookup"><span data-stu-id="bea1e-157">If a cross-domain connection is being made (that is, if the SignalR endpoint is not in the same domain as the hosting page), then WebSocket will be used if the following criteria are met:</span></span>

   - <span data-ttu-id="bea1e-158">클라이언트에서 CORS (크로스-원본 자원 공유)을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-158">The client supports CORS (Cross-Origin Resource Sharing).</span></span> <span data-ttu-id="bea1e-159">클라이언트는 CORS를 지원 세부 정보를 참조 하세요 [caniuse.com에서 CORS](http://www.caniuse.com/CORS)합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-159">For details on which clients support CORS, see [CORS at caniuse.com](http://www.caniuse.com/CORS).</span></span>
   - <span data-ttu-id="bea1e-160">클라이언트에서 WebSocket을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-160">The client supports WebSocket</span></span>
   - <span data-ttu-id="bea1e-161">서버에서 WebSocket을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-161">The server supports WebSocket</span></span>

     <span data-ttu-id="bea1e-162">이러한 조건 중 하나라도 충족 되지 않는 경우 긴 폴링 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-162">If any of these criteria are not met, Long Polling will be used.</span></span> <span data-ttu-id="bea1e-163">도메인 간 연결에 대 한 자세한 내용은 참조 하세요. [도메인 간 연결을 설정 하는 방법을](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-163">For more information on cross-domain connections, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>
4. <span data-ttu-id="bea1e-164">JSONP 구성 되지 않은 경우 연결이 아닙니다. 도메인 간 WebSocket 클라이언트와 서버 모두에서 지 원하는 경우 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-164">If JSONP is not configured and the connection is not cross-domain, WebSocket will be used if both the client and server support it.</span></span>
5. <span data-ttu-id="bea1e-165">클라이언트 또는 서버에는 WebSocket을 지원 하지 않으면, 사용 가능한 경우 이벤트를 전송 하는 서버 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-165">If either the client or server do not support WebSocket, Server Sent Events is used if it is available.</span></span>
6. <span data-ttu-id="bea1e-166">이벤트를 전송 하는 서버를 사용할 수 없는 경우 계속 프레임 시도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-166">If Server Sent Events is not available, Forever Frame is attempted.</span></span>
7. <span data-ttu-id="bea1e-167">프레임 계속 실패 하면 긴 폴링 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-167">If Forever Frame fails, Long Polling is used.</span></span>

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a><span data-ttu-id="bea1e-168">전송 모니터링</span><span class="sxs-lookup"><span data-stu-id="bea1e-168">Monitoring transports</span></span>

<span data-ttu-id="bea1e-169">응용 프로그램이 사용자 허브에서 로깅 및 브라우저에서 콘솔 창 열기를 사용 하 여 사용 중인 전송을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-169">You can determine what transport your application is using by enabling logging on your hub, and opening the console window in your browser.</span></span>

<span data-ttu-id="bea1e-170">브라우저에서 허브의 이벤트에 대 한 로깅을 사용 하려면 다음 명령을 클라이언트 응용 프로그램에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-170">To enable logging for your hub's events in a browser, add the following command to your client application:</span></span>

`$.connection.hub.logging = true;`

- <span data-ttu-id="bea1e-171">Internet Explorer에서 F12 키를 눌러 개발자 도구를 열고 콘솔 탭을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-171">In Internet Explorer, open the developer tools by pressing F12, and click the Console tab.</span></span>

    ![Microsoft Internet Explorer에서 콘솔](introduction-to-signalr/_static/image2.png)
- <span data-ttu-id="bea1e-173">Chrome에서는 Ctrl + Shift + J를 눌러 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-173">In Chrome, open the console by pressing Ctrl+Shift+J.</span></span>

    ![Google Chrome에서 콘솔](introduction-to-signalr/_static/image3.png)

<span data-ttu-id="bea1e-175">콘솔 열기 및 로깅을 사용 하도록 설정, 사용 하 여 SignalR에서 사용 되는 전송 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-175">With the console open and logging enabled, you'll be able to see which transport is being used by SignalR.</span></span>

![Internet Explorer WebSocket 전송이 보여 주는 콘솔](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a><span data-ttu-id="bea1e-177">전송 지정</span><span class="sxs-lookup"><span data-stu-id="bea1e-177">Specifying a transport</span></span>

<span data-ttu-id="bea1e-178">전송 협상 리소스 일정량의 시간과 클라이언트/서버를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-178">Negotiating a transport takes a certain amount of time and client/server resources.</span></span> <span data-ttu-id="bea1e-179">클라이언트 기능에 알고 있는 경우 다음 전송 때 지정할 수 있습니다 클라이언트 연결을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-179">If the client capabilities are known, then a transport can be specified when the client connection is started.</span></span> <span data-ttu-id="bea1e-180">다음 코드 조각은 클라이언트가 다른 프로토콜을 지원 하지 않은 것이 던 경우에 사용 되는 대로 Ajax 긴 폴링 전송을 사용 하 여 연결을 시작 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-180">The following code snippet demonstrates starting a connection using the Ajax Long Polling transport, as would be used if it was known that the client did not support any other protocol:</span></span>

`connection.start({ transport: 'longPolling' });`

<span data-ttu-id="bea1e-181">시도 하도록 클라이언트를 순서 대로 특정 전송 하려는 경우 대체 (fallback) 순서를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-181">You can specify a fallback order if you want a client to try specific transports in order.</span></span> <span data-ttu-id="bea1e-182">다음 코드 조각은 동안 WebSocket을 실패 하는 긴 폴링으로 직접 이동 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-182">The following code snippet demonstrates trying WebSocket, and failing that, going directly to Long Polling.</span></span>

`connection.start({ transport: ['webSockets','longPolling'] });`

<span data-ttu-id="bea1e-183">전송을 지정 하는 것에 대 한 문자열 상수는 다음과 같이 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-183">The string constants for specifying transports are defined as follows:</span></span>

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a><span data-ttu-id="bea1e-184">연결 및 허브</span><span class="sxs-lookup"><span data-stu-id="bea1e-184">Connections and Hubs</span></span>

<span data-ttu-id="bea1e-185">SignalR API는 클라이언트와 서버 간의 통신을 위한 두 가지 모델을 포함 되어 있습니다. 영구 연결 및 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-185">The SignalR API contains two models for communicating between clients and servers: Persistent Connections and Hubs.</span></span>

<span data-ttu-id="bea1e-186">연결에는 간단한 단일 받는 사람, 그룹화 또는 브로드캐스트 메시지를 보낼 끝점을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-186">A Connection represents a simple endpoint for sending single-recipient, grouped, or broadcast messages.</span></span> <span data-ttu-id="bea1e-187">개발자는 SignalR 노출 하는 하위 수준 통신 프로토콜에 대 한 액세스를 직접 (PersistentConnection 클래스에 의해.NET 코드에 표시 됨) 영구 연결 API 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-187">The Persistent Connection API (represented in .NET code by the PersistentConnection class) gives the developer direct access to the low-level communication protocol that SignalR exposes.</span></span> <span data-ttu-id="bea1e-188">연결 통신 모델을 사용 하 여 Windows Communication Foundation 같은 연결 기반 Api를 사용한 적이 있는 개발자에 게 친숙 한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-188">Using the Connections communication model will be familiar to developers who have used connection-based APIs such as Windows Communication Foundation.</span></span>

<span data-ttu-id="bea1e-189">허브는 클라이언트 및 서버에서 서로 다른 메서드를 직접 호출할 수 있도록 연결 API를 기반으로 보다 높은 수준의 파이프라인.</span><span class="sxs-lookup"><span data-stu-id="bea1e-189">A Hub is a more high-level pipeline built upon the Connection API that allows your client and server to call methods on each other directly.</span></span> <span data-ttu-id="bea1e-190">클라이언트가 서버에서 로컬 메서드로 쉽게 이동 하 고 그 반대의 경우로 메서드를 호출 하도록 허용 매직에서 작업 하는 것 처럼 컴퓨터 경계를 넘어 디스패치 SignalR에서 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-190">SignalR handles the dispatching across machine boundaries as if by magic, allowing clients to call methods on the server as easily as local methods, and vice versa.</span></span> <span data-ttu-id="bea1e-191">허브 통신 모델을 사용 하 여 원격 호출.NET Remoting 등의 Api를 사용한 적이 있는 개발자에 게 친숙 한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-191">Using the Hubs communication model will be familiar to developers who have used remote invocation APIs such as .NET Remoting.</span></span> <span data-ttu-id="bea1e-192">또한 허브를 사용 하 여 모델 바인딩을 사용 하도록 설정 하는 메서드에 강력한 형식의 매개 변수를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-192">Using a Hub also allows you to pass strongly typed parameters to methods, enabling model binding.</span></span>

### <a name="architecture-diagram"></a><span data-ttu-id="bea1e-193">아키텍처 다이어그램</span><span class="sxs-lookup"><span data-stu-id="bea1e-193">Architecture diagram</span></span>

<span data-ttu-id="bea1e-194">다음 다이어그램은 허브, 영구 연결 및 전송에 사용 되는 기본 기술 간의 관계를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-194">The following diagram shows the relationship between Hubs, Persistent Connections, and the underlying technologies used for transports.</span></span>

![Api, 전송 및 클라이언트를 보여 주는 SignalR 아키텍처 다이어그램](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a><span data-ttu-id="bea1e-196">허브의 작동 방식</span><span class="sxs-lookup"><span data-stu-id="bea1e-196">How Hubs work</span></span>

<span data-ttu-id="bea1e-197">클라이언트에서 메서드를 호출 하는 서버 쪽 코드, 이름 및 호출할 메서드의 매개 변수를 포함 하는 활성 전송에서 패킷을 전송 됩니다 (개체 메서드 매개 변수로 보내면 serialize 된 JSON을 사용 하 여).</span><span class="sxs-lookup"><span data-stu-id="bea1e-197">When server-side code calls a method on the client, a packet is sent across the active transport that contains the name and parameters of the method to be called (when an object is sent as a method parameter, it is serialized using JSON).</span></span> <span data-ttu-id="bea1e-198">클라이언트에는 다음 클라이언트 쪽 코드에 정의 된 메서드를 메서드 이름과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-198">The client then matches the method name to methods defined in client-side code.</span></span> <span data-ttu-id="bea1e-199">일치 하는 클라이언트 메서드는 deserialize 된 매개 변수 데이터를 사용 하 여 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-199">If there is a match, the client method will be executed using the deserialized parameter data.</span></span>

<span data-ttu-id="bea1e-200">메서드 호출 수와 같은 도구를 사용 하 여 모니터링할 [Fiddler.](http://fiddler2.com/)</span><span class="sxs-lookup"><span data-stu-id="bea1e-200">The method call can be monitored using tools like [Fiddler.](http://fiddler2.com/)</span></span> <span data-ttu-id="bea1e-201">다음 이미지에는 Fiddler의 로그 창에서 웹 브라우저 클라이언트에 SignalR 서버에서 전송 하는 메서드 호출을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-201">The following image shows a method call sent from a SignalR server to a web browser client in the Logs pane of Fiddler.</span></span> <span data-ttu-id="bea1e-202">허브 호출에서 전송 되는 메서드 호출 `MoveShapeHub`를 호출할 메서드를 호출 하 고 `updateShape`입니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-202">The method call is being sent from a hub called `MoveShapeHub`, and the method being invoked is called `updateShape`.</span></span>

![SignalR 트래픽을 보여 주는 Fiddler 로그 보기](introduction-to-signalr/_static/image6.png)

<span data-ttu-id="bea1e-204">이 예제에서는 허브 이름으로 식별 됩니다는 `H` 매개 변수; 메서드를 이름으로 식별 됩니다를 `M` 메서드에 전송 되는 데이터 및 매개 변수를 사용 하 여 식별 되는 `A` 매개 변수.</span><span class="sxs-lookup"><span data-stu-id="bea1e-204">In this example, the hub name is identified with the `H` parameter; the method name is identified with the `M` parameter, and the data being sent to the method is identified with the `A` parameter.</span></span> <span data-ttu-id="bea1e-205">이 메시지를 생성 하는 응용 프로그램에서 만들어진 합니다 [고주파수](tutorial-high-frequency-realtime-with-signalr.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-205">The application that generated this message is created in the [High-Frequency Realtime](tutorial-high-frequency-realtime-with-signalr.md) tutorial.</span></span>

### <a name="choosing-a-communication-model"></a><span data-ttu-id="bea1e-206">통신 모델 선택</span><span class="sxs-lookup"><span data-stu-id="bea1e-206">Choosing a communication model</span></span>

<span data-ttu-id="bea1e-207">대부분의 응용 프로그램 허브 API를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-207">Most applications should use the Hubs API.</span></span> <span data-ttu-id="bea1e-208">다음과 같은 경우에는 연결 API는 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-208">The Connections API could be used in the following circumstances:</span></span>

- <span data-ttu-id="bea1e-209">형식 지정 보낸 실제 메시지 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-209">The format of the actual message sent needs to be specified.</span></span>
- <span data-ttu-id="bea1e-210">개발자는 원격 호출 모델 보다는 메시징 및 디스패치 모델을 사용 하 여 작업을 선호 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-210">The developer prefers to work with a messaging and dispatching model rather than a remote invocation model.</span></span>
- <span data-ttu-id="bea1e-211">SignalR을 사용 하는 메시징 모델을 사용 하는 기존 응용 프로그램 이식 중인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bea1e-211">An existing application that uses a messaging model is being ported to use SignalR.</span></span>
