---
uid: signalr/overview/testing-and-debugging/troubleshooting
title: SignalR 문제 해결 | Microsoft Docs
author: pfletcher
description: 이 문서는 SignalR 응용 프로그램을 개발 하는 일반적인 문제를 설명 합니다.
ms.author: riande
ms.date: 06/10/2014
ms.assetid: 4b559e6c-4fb0-4a04-9812-45cf08ae5779
msc.legacyurl: /signalr/overview/testing-and-debugging/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: 9ef69ece2558260f0409e9388751f77ac84a06f1
ms.sourcegitcommit: c12ebdab65853f27fbb418204646baf6ce69515e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/21/2018
ms.locfileid: "46523079"
---
<a name="signalr-troubleshooting"></a><span data-ttu-id="1f835-103">SignalR 문제 해결</span><span class="sxs-lookup"><span data-stu-id="1f835-103">SignalR Troubleshooting</span></span>
====================
<span data-ttu-id="1f835-104">[Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="1f835-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

> <span data-ttu-id="1f835-105">이 문서는 SignalR 사용 하 여 일반적인 문제를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-105">This document describes common troubleshooting issues with SignalR.</span></span>
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="1f835-106">이 항목에서 사용 하는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="1f835-106">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="1f835-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="1f835-107">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="1f835-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="1f835-108">.NET 4.5</span></span>
> - <span data-ttu-id="1f835-109">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="1f835-109">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="1f835-110">이 항목의 이전 버전</span><span class="sxs-lookup"><span data-stu-id="1f835-110">Previous versions of this topic</span></span>
> 
> <span data-ttu-id="1f835-111">이전 버전의 SignalR에 대 한 정보를 참조 하세요 [SignalR 이전 버전](../older-versions/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="1f835-112">질문이 나 의견이 있으면</span><span class="sxs-lookup"><span data-stu-id="1f835-112">Questions and comments</span></span>
> 
> <span data-ttu-id="1f835-113">이 자습서를 연결 하는 방법 및 새로운 개선할 수 있습니다 페이지의 맨 아래에 의견에서에 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="1f835-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="1f835-114">에 자습서로 직접 관련 되지 않은 질문이 있을 경우 게시할 수 하는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


<span data-ttu-id="1f835-115">이 문서에는 다음과 같은 섹션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-115">This document contains the following sections.</span></span>

- [<span data-ttu-id="1f835-116">메서드를 호출 하는 클라이언트와 서버 간에 자동으로 실패</span><span class="sxs-lookup"><span data-stu-id="1f835-116">Calling methods between the client and server silently fails</span></span>](#connection)
- [<span data-ttu-id="1f835-117">IIS websocket ping/핑퐁 비활성 클라이언트 검색을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-117">Configuring IIS websockets to ping/pong to detect a dead client</span></span>](#pong)
- [<span data-ttu-id="1f835-118">다른 연결 문제</span><span class="sxs-lookup"><span data-stu-id="1f835-118">Other connection issues</span></span>](#other)
- [<span data-ttu-id="1f835-119">컴파일 및 서버 쪽 오류</span><span class="sxs-lookup"><span data-stu-id="1f835-119">Compilation and server-side errors</span></span>](#server)
- [<span data-ttu-id="1f835-120">Visual Studio 문제</span><span class="sxs-lookup"><span data-stu-id="1f835-120">Visual Studio issues</span></span>](#vs)
- [<span data-ttu-id="1f835-121">인터넷 정보 서비스 문제</span><span class="sxs-lookup"><span data-stu-id="1f835-121">Internet Information Services issues</span></span>](#iis)
- [<span data-ttu-id="1f835-122">Microsoft Azure 문제</span><span class="sxs-lookup"><span data-stu-id="1f835-122">Microsoft Azure issues</span></span>](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a><span data-ttu-id="1f835-123">메서드를 호출 하는 클라이언트와 서버 간에 자동으로 실패</span><span class="sxs-lookup"><span data-stu-id="1f835-123">Calling methods between the client and server silently fails</span></span>

<span data-ttu-id="1f835-124">이 섹션에서는 의미 있는 오류 메시지 없이 실패 하는 클라이언트와 서버 간의 메서드 호출에 대 한 가능한 원인을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-124">This section describes possible causes for a method call between client and server to fail without a meaningful error message.</span></span> <span data-ttu-id="1f835-125">SignalR 응용 프로그램을 서버에 클라이언트 구현; 하는 방법에 대 한 정보가 없습니다. 클라이언트 메서드를 호출 하는 서버를 클라이언트에는 메서드 이름과 매개 변수 데이터를 보내고 메서드는 서버를 지정 하는 형식으로 존재 하는 경우에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-125">In a SignalR application, the server has no information about the methods that the client implements; when the server invokes a client method, the method name and parameter data are sent to the client, and the method is executed only if it exists in the format that the server specified.</span></span> <span data-ttu-id="1f835-126">아무런 결과가 일치 하는 메서드가 없는 클라이언트에서 발견 된 경우 서버에서 오류 메시지가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-126">If no matching method is found on the client, nothing happens, and no error message is raised on the server.</span></span>

<span data-ttu-id="1f835-127">클라이언트 메서드를 호출 하지를 자세히 조사 하려면 어떤 호출을 표시 하도록 허브의 start 메서드는 서버에서 들어오는 호출 하기 전에 로깅을 켤 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-127">To further investigate client methods not getting called, you can turn on logging before the calling the start method on the hub to see what calls are coming from the server.</span></span> <span data-ttu-id="1f835-128">JavaScript 응용 프로그램에서 로깅을 사용 하려면 [클라이언트 쪽 로깅 (JavaScript 클라이언트 버전)를 사용 하도록 설정 하는 방법을](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-128">To enable logging in a JavaScript application, see [How to enable client-side logging (JavaScript client version)](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging).</span></span> <span data-ttu-id="1f835-129">.NET 클라이언트 응용 프로그램에서 로깅을 사용 하려면 [(.NET 클라이언트 버전) 클라이언트 쪽 로깅을 사용 하도록 설정 하는 방법을](../guide-to-the-api/hubs-api-guide-net-client.md#logging)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-129">To enable logging in a .NET client application, see [How to enable client-side logging (.NET Client version)](../guide-to-the-api/hubs-api-guide-net-client.md#logging).</span></span>

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a><span data-ttu-id="1f835-130">철자가 잘못 된 메서드, 잘못 된 메서드 시그니처 또는 잘못 된 허브 이름</span><span class="sxs-lookup"><span data-stu-id="1f835-130">Misspelled method, incorrect method signature, or incorrect hub name</span></span>

<span data-ttu-id="1f835-131">이름 또는 호출 메서드의 시그니처에 정확히 일치 하지 않는 클라이언트에서 적절 한 메서드를 호출 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-131">If the name or signature of a called method does not exactly match an appropriate method on the client, the call will fail.</span></span> <span data-ttu-id="1f835-132">메서드 이름을 호출 하 여 클라이언트에 대 한 메서드의 이름과 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-132">Verify that the method name called by the server matches the name of the method on the client.</span></span> <span data-ttu-id="1f835-133">또한 SignalR 카멜식 대 메서드를 사용 하 여 허브 프록시를 만들고 JavaScript에서 적절 한 경우 이므로 메서드를 호출할 `SendMessage` 서버에서 호출 됩니다 `sendMessage` 클라이언트 프록시에 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-133">Also, SignalR creates the hub proxy using camel-cased methods, as is appropriate in JavaScript, so a method called `SendMessage` on the server would be called `sendMessage` in the client proxy.</span></span> <span data-ttu-id="1f835-134">사용 하는 경우는 `HubName` 서버 쪽 코드에서 특성에 사용 되는 이름 클라이언트에 허브를 만드는 데 이름과 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-134">If you use the `HubName` attribute in your server-side code, verify that the name used matches the name used to create the hub on the client.</span></span> <span data-ttu-id="1f835-135">사용 하지 않는 경우는 `HubName` 특성, 카멜식 대/소문자, ChatHub 대신 chatHub 같은 JavaScript 클라이언트에서 허브의 이름 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-135">If you do not use the `HubName` attribute, verify that the name of the hub in a JavaScript client is camel-cased, such as chatHub instead of ChatHub.</span></span>

### <a name="duplicate-method-name-on-client"></a><span data-ttu-id="1f835-136">클라이언트에서 메서드 이름이 중복 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-136">Duplicate method name on client</span></span>

<span data-ttu-id="1f835-137">없는 중복 된 메서드를 대/소문자만 다른 클라이언트에서 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-137">Verify that you do not have a duplicate method on the client that differs only by case.</span></span> <span data-ttu-id="1f835-138">클라이언트 응용 프로그램 라는 메서드가 있으면 `sendMessage`, 메서드 호출도 없다는 확인 `SendMessage` 도 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-138">If your client application has a method called `sendMessage`, verify that there isn't also a method called `SendMessage` as well.</span></span>

### <a name="missing-json-parser-on-the-client"></a><span data-ttu-id="1f835-139">클라이언트에서 누락 된 JSON 파서</span><span class="sxs-lookup"><span data-stu-id="1f835-139">Missing JSON parser on the client</span></span>

<span data-ttu-id="1f835-140">SignalR을 서버와 클라이언트 간의 호출을 serialize 하는 데 사용할 JSON 파서를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-140">SignalR requires a JSON parser to be present to serialize calls between the server and the client.</span></span> <span data-ttu-id="1f835-141">클라이언트는 기본 제공 JSON 파서 (예: Internet Explorer 7)가 없는 경우에 응용 프로그램에서 하나를 포함 하는 것이 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-141">If your client doesn't have a built-in JSON parser (such as Internet Explorer 7), you'll need to include one in your application.</span></span> <span data-ttu-id="1f835-142">JSON 파서를 다운로드할 수 있습니다 [여기](http://nuget.org/packages/json2)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-142">You can download the JSON parser [here](http://nuget.org/packages/json2).</span></span>

### <a name="mixing-hub-and-persistentconnection-syntax"></a><span data-ttu-id="1f835-143">허브 및 PersistentConnection 구문을 함께 사용</span><span class="sxs-lookup"><span data-stu-id="1f835-143">Mixing Hub and PersistentConnection syntax</span></span>

<span data-ttu-id="1f835-144">두 통신 모델을 사용 하 여 SignalR: 허브 및 PersistentConnections 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-144">SignalR uses two communication models: Hubs and PersistentConnections.</span></span> <span data-ttu-id="1f835-145">이러한 두 통신 모델을 호출 하기 위한 구문은 클라이언트 코드에서 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-145">The syntax for calling these two communication models is different in the client code.</span></span> <span data-ttu-id="1f835-146">서버 코드에서 허브를 추가한 경우에 적절 한 허브 구문을 사용 하는 모든 클라이언트 코드를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-146">If you have added a hub in your server code, verify that all of your client code uses the proper hub syntax.</span></span>

<span data-ttu-id="1f835-147">**JavaScript 클라이언트를 만드는 코드를 한 PersistentConnection JavaScript 클라이언트에서**</span><span class="sxs-lookup"><span data-stu-id="1f835-147">**JavaScript client code that creates a PersistentConnection in a JavaScript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

<span data-ttu-id="1f835-148">**Javascript 클라이언트에 허브 프록시를 만드는 JavaScript 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="1f835-148">**JavaScript client code that creates a Hub Proxy in a Javascript client**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

<span data-ttu-id="1f835-149">**C# 서버 코드 경로 PersistentConnection 매핑되는**</span><span class="sxs-lookup"><span data-stu-id="1f835-149">**C# server code that maps a route to a PersistentConnection**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

<span data-ttu-id="1f835-150">**C# 서버 코드 여러 응용 프로그램이 있는 경우 허브에 또는 여러 허브에 대 한 경로 매핑하는**</span><span class="sxs-lookup"><span data-stu-id="1f835-150">**C# server code that maps a route to a Hub, or to mulitple hubs if you have multiple applications**</span></span>

[!code-css[Main](troubleshooting/samples/sample4.css)]

### <a name="connection-started-before-subscriptions-are-added"></a><span data-ttu-id="1f835-151">구독 추가 되기 전에 시작 된 연결</span><span class="sxs-lookup"><span data-stu-id="1f835-151">Connection started before subscriptions are added</span></span>

<span data-ttu-id="1f835-152">허브의 연결 서버에서 호출할 수 있는 메서드는 프록시에 추가 되기 전에 시작 된 경우 메시지 수신 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-152">If the Hub's connection is started before methods that can be called from the server are added to the proxy, messages will not be received.</span></span> <span data-ttu-id="1f835-153">다음 JavaScript 코드 허브를 제대로 시작 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-153">The following JavaScript code will not start the hub properly:</span></span>

<span data-ttu-id="1f835-154">**허브 메시지가 수신 되도록 허용 하지 않는 잘못 된 JavaScript 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="1f835-154">**Incorrect JavaScript client code that will not allow Hubs messages to be received**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

<span data-ttu-id="1f835-155">대신, 시작을 호출 하기 전에 메서드 구독을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-155">Instead, add the method subscriptions before calling Start:</span></span>

<span data-ttu-id="1f835-156">**올바르게 허브에 구독을 추가 하는 JavaScript 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="1f835-156">**JavaScript client code that correctly adds subscriptions to a hub**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a><span data-ttu-id="1f835-157">허브 프록시에 누락 된 메서드 이름</span><span class="sxs-lookup"><span data-stu-id="1f835-157">Missing method name on the hub proxy</span></span>

<span data-ttu-id="1f835-158">클라이언트에서 서버에 정의 된 메서드가에 구독 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-158">Verify that the method defined on the server is subscribed to on the client.</span></span> <span data-ttu-id="1f835-159">서버 메서드를 정의 하는 경우에 여전히 클라이언트 프록시에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-159">Even though the server defines the method, it must still be added to the client proxy.</span></span> <span data-ttu-id="1f835-160">메서드는 다음과 같은 방법으로 클라이언트 프록시를 추가할 수 있습니다 (메서드가 추가 되는 참고를 `client` 허브 아닌 직접 허브 소속):</span><span class="sxs-lookup"><span data-stu-id="1f835-160">Methods can be added to the client proxy in the following ways (Note that the method is added to the `client` member of the hub, not the hub directly):</span></span>

<span data-ttu-id="1f835-161">**허브 프록시에 메서드를 추가 하는 JavaScript 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="1f835-161">**JavaScript client code that adds methods to a hub proxy**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a><span data-ttu-id="1f835-162">허브 또는 허브 메서드를 Public로 선언 되지 않았습니다</span><span class="sxs-lookup"><span data-stu-id="1f835-162">Hub or hub methods not declared as Public</span></span>

<span data-ttu-id="1f835-163">클라이언트에서 표시 하려면 허브 구현 및 메서드를 선언 해야 합니다 `public`합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-163">To be visible on the client, the hub implementation and methods must be declared as `public`.</span></span>

### <a name="accessing-hub-from-a-different-application"></a><span data-ttu-id="1f835-164">다른 응용 프로그램에서 허브에 액세스 하기</span><span class="sxs-lookup"><span data-stu-id="1f835-164">Accessing hub from a different application</span></span>

<span data-ttu-id="1f835-165">SignalR 허브 SignalR 클라이언트를 구현 하는 응용 프로그램을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-165">SignalR Hubs can only be accessed through applications that implement SignalR clients.</span></span> <span data-ttu-id="1f835-166">SignalR 다른 통신 라이브러리 (예: SOAP 또는 WCF 웹 서비스)를 사용 하 여 상호 작용할 수 없습니다. 대상 플랫폼에 사용할 수 있는 SignalR 클라이언트가 없는 경우 서버의 끝점을 직접 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-166">SignalR cannot interoperate with other communication libraries (like SOAP or WCF web services.) If there is no SignalR client available for your target platform, you cannot access the server's endpoint directly.</span></span>

### <a name="manually-serializing-data"></a><span data-ttu-id="1f835-167">수동으로 데이터를 직렬화합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-167">Manually serializing data</span></span>

<span data-ttu-id="1f835-168">SignalR은 자동으로 JSON을 사용 메서드를 serialize 할 매개 변수-여기의 하지 않아도 사용자가 직접 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-168">SignalR will automatically use JSON to serialize your method parameters- there's no need to do it yourself.</span></span>

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a><span data-ttu-id="1f835-169">OnDisconnected 함수에는 클라이언트에서 실행 되지 원격 허브 메서드</span><span class="sxs-lookup"><span data-stu-id="1f835-169">Remote Hub method not executed on client in OnDisconnected function</span></span>

<span data-ttu-id="1f835-170">이 동작은 설계 시 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-170">This behavior is by design.</span></span> <span data-ttu-id="1f835-171">때 `OnDisconnected` 는 호출 허브 이미 입력는 `Disconnected` 상태를 허용 하지 않는 추가 허브 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-171">When `OnDisconnected` is called, the hub has already entered the `Disconnected` state, which does not allow further hub methods to be called.</span></span>

<span data-ttu-id="1f835-172">**C# 서버 코드 올바르게 OnDisconnected 이벤트에 코드를 실행 하는**</span><span class="sxs-lookup"><span data-stu-id="1f835-172">**C# server code that correctly executes code in the OnDisconnected event**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="ondisconnect-not-firing-at-consistent-times"></a><span data-ttu-id="1f835-173">OnDisconnect 일관 된 시간에 실행 되지 않음</span><span class="sxs-lookup"><span data-stu-id="1f835-173">OnDisconnect not firing at consistent times</span></span>

<span data-ttu-id="1f835-174">이 동작은 설계 시 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-174">This behavior is by design.</span></span> <span data-ttu-id="1f835-175">사용자 활성 SignalR 연결을 사용 하 여 페이지 외부로 이동할 때 SignalR 클라이언트는 클라이언트 연결이 중지 되는 서버에 알리기 위해 시도 하는 최상의 노력을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-175">When a user attempts to navigate away from a page with an active SignalR connection, the SignalR client will then make a best-effort attempt to notify the server that the client connection will be stopped.</span></span> <span data-ttu-id="1f835-176">SignalR 클라이언트의 최상의 노력을 다 하는 경우 서버에 도달 하도록 시도가 실패 하면, 서버는 구성 가능한 후 연결을 삭제 `DisconnectTimeout` 이때 나중의 `OnDisconnected` 이벤트가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-176">If the SignalR client's best-effort attempt fails to reach the server, the server will dispose of the connection after a configurable `DisconnectTimeout` later, at which time the `OnDisconnected` event will fire.</span></span> <span data-ttu-id="1f835-177">SignalR 클라이언트의 최상의 시도가 성공한 경우에 `OnDisconnected` 이벤트는 즉시 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-177">If the SignalR client's best-effort attempt is successful, the `OnDisconnected` event will fire immediately.</span></span>

<span data-ttu-id="1f835-178">설정에 대 한 정보에 대 한 합니다 `DisconnectTimeout` 설정을 참조 하세요 [연결 수명 이벤트를 처리: DisconnectTimeout](../guide-to-the-api/handling-connection-lifetime-events.md#disconnecttimeout)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-178">For information on setting the `DisconnectTimeout` setting, see [Handling connection lifetime events: DisconnectTimeout](../guide-to-the-api/handling-connection-lifetime-events.md#disconnecttimeout).</span></span>

### <a name="connection-limit-reached"></a><span data-ttu-id="1f835-179">연결 제한에 도달 함</span><span class="sxs-lookup"><span data-stu-id="1f835-179">Connection limit reached</span></span>

<span data-ttu-id="1f835-180">Windows 7 같은 클라이언트 운영 체제에서 전체 버전의 IIS 사용 하는 경우에 10 연결 제한이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-180">When using the full version of IIS on a client operating system like Windows 7, a 10-connection limit is imposed.</span></span> <span data-ttu-id="1f835-181">클라이언트 OS를 사용 하는 경우 대신 IIS Express 사용이 제한을 피할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-181">When using a client OS, use IIS Express instead to avoid this limit.</span></span>

### <a name="cross-domain-connection-not-set-up-properly"></a><span data-ttu-id="1f835-182">도메인 간 연결을 제대로 설정 되지 않았습니다</span><span class="sxs-lookup"><span data-stu-id="1f835-182">Cross-domain connection not set up properly</span></span>

<span data-ttu-id="1f835-183">하는 경우 도메인 간 연결을 (를 SignalR URL이 호스팅 페이지와 동일한 도메인에 연결) 올바르게 설정 하지 않으면 오류 메시지 없이 연결이 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-183">If a cross-domain connection (a connection for which the SignalR URL is not in the same domain as the hosting page) is not set up correctly, the connection may fail without an error message.</span></span> <span data-ttu-id="1f835-184">도메인 간 통신을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 [도메인 간 연결을 설정 하는 방법을](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-184">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span>

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a><span data-ttu-id="1f835-185">.NET 클라이언트에서 작동 하지 않는 NTLM (Active Directory)를 사용 하 여 연결</span><span class="sxs-lookup"><span data-stu-id="1f835-185">Connection using NTLM (Active Directory) not working in .NET client</span></span>

<span data-ttu-id="1f835-186">도메인 보안을 사용 하는.NET 클라이언트 응용 프로그램에서 연결을 연결이 제대로 구성 되지 않은 경우 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-186">A connection in a .NET client application that uses Domain security may fail if the connection is not configured properly.</span></span> <span data-ttu-id="1f835-187">도메인 환경에서 SignalR을 사용 하려면 필수 연결 속성을 다음과 같이 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-187">To use SignalR in a domain environment, set the requisite connection property as follows:</span></span>

<span data-ttu-id="1f835-188">**C# 클라이언트 코드는 연결 자격 증명 구현**</span><span class="sxs-lookup"><span data-stu-id="1f835-188">**C# client code that implements connection credentials**</span></span>

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="pong"></a>

## <a name="configuring-iis-websockets-to-pingpong-to-detect-a-dead-client"></a><span data-ttu-id="1f835-189">IIS websocket ping/핑퐁 비활성 클라이언트 검색을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-189">Configuring IIS websockets to ping/pong to detect a dead client</span></span>

<span data-ttu-id="1f835-190">SignalR 서버 클라이언트 인지 배달 못 한 편지 및 즉 연결 실패에 대 한 기본 websocket에서 알림을 사용 하는 경우 알지는 `OnClose` 콜백 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-190">SignalR servers don't know if the client is dead or not and they rely on notification from the underlying websocket for connection failures, that is, the `OnClose` callback.</span></span> <span data-ttu-id="1f835-191">이 문제를 해결 하려면 ping/핑퐁 하기 위해 IIS websockets를 구성 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-191">One solution to this problem is to configure IIS websockets to do the ping/pong for you.</span></span> <span data-ttu-id="1f835-192">이렇게 하면 예기치 않게 중단 연결이 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-192">This ensures that your connection will close if it breaks unexpectedly.</span></span> <span data-ttu-id="1f835-193">자세한 내용은 참조 [이 stackoverflow 게시물](http://stackoverflow.com/questions/19502755/websocket-clients-state-not-changing-on-network-loss)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-193">For more information see [this stackoverflow post](http://stackoverflow.com/questions/19502755/websocket-clients-state-not-changing-on-network-loss).</span></span>

<a id="other"></a>

## <a name="other-connection-issues"></a><span data-ttu-id="1f835-194">다른 연결 문제</span><span class="sxs-lookup"><span data-stu-id="1f835-194">Other connection issues</span></span>

<span data-ttu-id="1f835-195">이 섹션에서는 원인 및 솔루션 특정 증상에 연결 하는 동안 발생 하는 오류 메시지를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-195">This section describes the causes and solutions for specific symptoms or error messages that occur during a connection.</span></span>

### <a name="start-must-be-called-before-data-can-be-sent-error"></a><span data-ttu-id="1f835-196">"시작 해야 데이터를 보내기 전에 호출 됨" 오류</span><span class="sxs-lookup"><span data-stu-id="1f835-196">"Start must be called before data can be sent" error</span></span>

<span data-ttu-id="1f835-197">이 오류는 일반적으로 연결을 시작 하기 전에 코드 SignalR 개체를 참조 하는 경우에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-197">This error is commonly seen if code references SignalR objects before the connection is started.</span></span> <span data-ttu-id="1f835-198">등 처리기에 대 한 연결이 메서드를 호출 하는 서버에 정의 된 추가 되어야 함을 연결 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-198">The wireup for handlers and the like that will call methods defined on the server must be added after the connection completes.</span></span> <span data-ttu-id="1f835-199">호출 `Start` 비동기 이므로 완료 하는 코드를 호출 하기 전에 실행 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-199">Note that the call to `Start` is asynchronous, so code after the call may be executed before it completes.</span></span> <span data-ttu-id="1f835-200">연결이 완전히 시작 된 후 처리기를 추가 하려면 start 메서드에 매개 변수로 전달 되는 콜백 함수에 배치 하는 가장 좋은 방법은:</span><span class="sxs-lookup"><span data-stu-id="1f835-200">The best way to add handlers after a connection starts completely is to put them into a callback function that is passed as a parameter to the start method:</span></span>

<span data-ttu-id="1f835-201">**올바르게 SignalR 개체를 참조 하는 이벤트 처리기를 추가 하는 JavaScript 클라이언트 코드**</span><span class="sxs-lookup"><span data-stu-id="1f835-201">**JavaScript client code that correctly adds event handlers that reference SignalR objects**</span></span>

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

<span data-ttu-id="1f835-202">이 오류 SignalR 개체는 여전히 참조 되는 동안 연결을 중지 하는 경우에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-202">This error will also be seen if a connection stops while SignalR objects are still being referenced.</span></span>

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a><span data-ttu-id="1f835-203">"301 영구적으로 이동 됨" 또는 "302 임시로 이동 됨" 오류</span><span class="sxs-lookup"><span data-stu-id="1f835-203">"301 Moved Permanently" or "302 Moved Temporarily" error</span></span>

<span data-ttu-id="1f835-204">이 오류는 프로젝트는 자동으로 만들어진 프록시를 방해 하는 SignalR 라는 폴더를 포함 하는 경우 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-204">This error may be seen if the project contains a folder called SignalR, which will interfere with the automatically-created proxy.</span></span> <span data-ttu-id="1f835-205">이 오류를 방지 하려면 라는 폴더를 사용 하지 않는 `SignalR` 응용 프로그램 또는 해제 자동 프록시 생성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-205">To avoid this error, do not use a folder called `SignalR` in your application, or turn automatic proxy generation off.</span></span> <span data-ttu-id="1f835-206">참조 [생성 된 프록시 및 용도를](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-206">See [The Generated Proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy) for more details.</span></span>

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a><span data-ttu-id="1f835-207">.NET 또는 Silverlight 클라이언트에서 "403 사용할 수 없음" 오류</span><span class="sxs-lookup"><span data-stu-id="1f835-207">"403 Forbidden" error in .NET or Silverlight client</span></span>

<span data-ttu-id="1f835-208">이 오류는 도메인 간 통신 해제 되어 없는 제대로 도메인 간 환경에서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-208">This error may occur in cross-domain environments where cross-domain communication is not properly enabled.</span></span> <span data-ttu-id="1f835-209">도메인 간 통신을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 [도메인 간 연결을 설정 하는 방법을](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-209">For information on how to enable cross-domain communication, see [How to establish a cross-domain connection](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain).</span></span> <span data-ttu-id="1f835-210">Silverlight 클라이언트에서 도메인 간 연결을 설정 참조 [Silverlight 클라이언트에서 도메인 간 연결](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-210">To establish a cross-domain connection in a Silverlight client, see [Cross-domain connections from Silverlight clients](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain).</span></span>

### <a name="404-not-found-error"></a><span data-ttu-id="1f835-211">"404 찾을 수 없음" 오류</span><span class="sxs-lookup"><span data-stu-id="1f835-211">"404 Not Found" error</span></span>

<span data-ttu-id="1f835-212">이 문제에 대 한 여러 원인이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-212">There are several causes for this issue.</span></span> <span data-ttu-id="1f835-213">다음을 모두 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-213">Verify all of the following:</span></span>

- <span data-ttu-id="1f835-214">**허브 프록시 주소 참조 형식이 올바르지 않습니다:** 생성 된 허브 프록시 주소에 대 한 참조의 형식이 올바르게 지정 되지 않았습니다 하는 경우이 오류는 일반적으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-214">**Hub proxy address reference not formatted correctly:** This error is commonly seen if the reference to the generated hub proxy address is not formatted correctly.</span></span> <span data-ttu-id="1f835-215">허브 주소에 대 한 참조가 제대로 만들어지기를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-215">Verify that the reference to the hub address is made properly.</span></span> <span data-ttu-id="1f835-216">참조 [동적으로 생성 된 프록시를 참조 하는 방법을](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-216">See [How to reference the dynamically generated proxy](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) for details.</span></span>
- <span data-ttu-id="1f835-217">**허브 경로 추가 하기 전에 응용 프로그램에 경로 추가 합니다.** 응용 프로그램에서 다른 경로 사용 하는 경우 추가 하는 첫 번째 경로에 대 한 호출 인지 확인 `MapSignalR`합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-217">**Adding routes to application before adding the hub route:** If your application uses other routes, verify that the first route added is the call to `MapSignalR`.</span></span>
- <span data-ttu-id="1f835-218">**확장명 없는 Url에 대 한 업데이트 없이 7.5 또는 IIS 7을 사용 하 여:** 를 사용 하 여 IIS 7 또는 7.5를 업데이트 해야 확장명 없는 Url에 대 한 서버에서 허브 정의에 대 한 액세스를 제공할 수 있도록 `/signalr/hubs`입니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-218">**Using IIS 7 or 7.5 without the update for extensionless URLs:** Using IIS 7 or 7.5 requires an update for extensionless URLs so that the server can provide access to the hub definitions at `/signalr/hubs`.</span></span> <span data-ttu-id="1f835-219">업데이트를 확인할 수 있습니다 [여기](https://support.microsoft.com/kb/980368)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-219">The update can be found [here](https://support.microsoft.com/kb/980368).</span></span>
- <span data-ttu-id="1f835-220">**IIS 캐시 만료 또는 손상:** 캐시 콘텐츠 만료 없는지를 확인 하려면 캐시를 지우는 PowerShell 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-220">**IIS cache out of date or corrupt:** To verify that the cache contents are not out of date, enter the following command in a PowerShell window to clear the cache:</span></span>

    [!code-powershell[Main](troubleshooting/samples/sample11.ps1)]

### <a name="500-internal-server-error"></a><span data-ttu-id="1f835-221">"500 내부 서버 오류"</span><span class="sxs-lookup"><span data-stu-id="1f835-221">"500 Internal Server Error"</span></span>

<span data-ttu-id="1f835-222">다양 한 원인 포함 될 수 있는 매우 일반적인 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-222">This is a very generic error that could have a wide variety of causes.</span></span> <span data-ttu-id="1f835-223">오류의 세부 정보 서버의 이벤트 로그에 표시 해야 하거나 서버 디버깅을 통해 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-223">The details of the error should appear in the server's event log, or can be found through debugging the server.</span></span> <span data-ttu-id="1f835-224">서버에서 자세한 오류를 켜면 더 자세한 오류 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-224">More detailed error information may be obtained by turning on detailed errors on the server.</span></span> <span data-ttu-id="1f835-225">자세한 내용은 [허브 클래스에서 오류를 처리 하는 방법을](../guide-to-the-api/hubs-api-guide-server.md#handleErrors)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-225">For more information, see [How to handle errors in the Hub class](../guide-to-the-api/hubs-api-guide-server.md#handleErrors).</span></span>

<span data-ttu-id="1f835-226">이 오류는 일반적으로 방화벽 또는 프록시를 제대로 구성 되지 않았습니다, 다시 작성 요청 헤더를 유발 하는 경우에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-226">This error is also commonly seen if a firewall or proxy is not configured properly, causing the request headers to be rewritten.</span></span> <span data-ttu-id="1f835-227">솔루션 포트 80에서 방화벽 또는 프록시 활성화 되어 있는지 확인 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-227">The solution is to make sure that port 80 is enabled on the firewall or proxy.</span></span>

### <a name="unexpected-response-code-500"></a><span data-ttu-id="1f835-228">"예기치 않은 응답 코드: 500"</span><span class="sxs-lookup"><span data-stu-id="1f835-228">"Unexpected response code: 500"</span></span>

<span data-ttu-id="1f835-229">응용 프로그램에 사용 되는.NET framework의 버전 Web.Config에 지정 된 버전과 일치 하지 않으면이 오류가 발생할 수 있습니다. 솔루션은.NET 4.5 응용 프로그램 설정 및 Web.Config 파일에서 사용 되 고 있는지 확인 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-229">This error may occur if the version of .NET framework used in the application does not match the version specified in Web.Config. The solution is to verify that .NET 4.5 is used in both the application settings and the Web.Config file.</span></span>

### <a name="typeerror-lthubtypegt-is-undefined-error"></a><span data-ttu-id="1f835-230">"TypeError: &lt;hubType&gt; 정의 되지 않았습니다" 오류</span><span class="sxs-lookup"><span data-stu-id="1f835-230">"TypeError: &lt;hubType&gt; is undefined" error</span></span>

<span data-ttu-id="1f835-231">이 오류가 발생 하는 경우에 대 한 호출 `MapSignalR` 제대로 수행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-231">This error will result if the call to `MapSignalR` is not made properly.</span></span> <span data-ttu-id="1f835-232">참조 [SignalR 미들웨어를 등록 하 여 SignalR 옵션을 구성 하는 방법을](../guide-to-the-api/hubs-api-guide-server.md#route) 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-232">See [How to register SignalR Middleware and configure SignalR options](../guide-to-the-api/hubs-api-guide-server.md#route) for more information.</span></span>

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a><span data-ttu-id="1f835-233">JsonSerializationException은 사용자 코드에서 처리 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-233">JsonSerializationException was unhandled by user code</span></span>

<span data-ttu-id="1f835-234">메서드에 전송 하는 매개 변수를 직렬화 형식 (예: 파일 핸들, 데이터베이스 연결) 들어 있지 않은지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-234">Verify that the parameters you send to your methods do not include non-serializable types (like file handles or database connections).</span></span> <span data-ttu-id="1f835-235">사용 하 여 (또는 보안에 대 한 serialization 위해), 클라이언트에 전송 하지 않으려는 서버 쪽 개체의 멤버를 사용 하는 경우는 `JSONIgnore` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-235">If you need to use members on a server-side object that you don't want to be sent to the client (either for security or for reasons of serialization), use the `JSONIgnore` attribute.</span></span>

### <a name="protocol-error-unknown-transport-error"></a><span data-ttu-id="1f835-236">"프로토콜 오류: 알 수 없는 전송" 오류</span><span class="sxs-lookup"><span data-stu-id="1f835-236">"Protocol error: Unknown transport" error</span></span>

<span data-ttu-id="1f835-237">이 오류는 클라이언트에 SignalR 사용 되는 전송을 지원 하지 않는 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-237">This error may occur if the client does not support the transports that SignalR uses.</span></span> <span data-ttu-id="1f835-238">참조 [전송과 대체](../getting-started/introduction-to-signalr.md#transports) 정보는 브라우저 사용 하 여 SignalR에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-238">See [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports) for information on which browsers can be used with SignalR.</span></span>

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a><span data-ttu-id="1f835-239">"JavaScript 허브 프록시 생성 비활성화 되었습니다."</span><span class="sxs-lookup"><span data-stu-id="1f835-239">"JavaScript Hub proxy generation has been disabled."</span></span>

<span data-ttu-id="1f835-240">이 오류가 발생 하는 경우 `DisableJavaScriptProxies` 에서 동적으로 생성 된 프록시에 대 한 참조를 포함 하는 동안 설정 된 `signalr/hubs`합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-240">This error will occur if `DisableJavaScriptProxies` is set while also including a reference to the dynamically generated proxy at `signalr/hubs`.</span></span> <span data-ttu-id="1f835-241">프록시를 수동으로 만드는 방법에 대 한 자세한 내용은 참조 하세요. [생성 된 프록시 및 용도를](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)입니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-241">For more information on creating the proxy manually, see [The generated proxy and what it does for you](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy).</span></span>

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a><span data-ttu-id="1f835-242">"연결 ID가 잘못 된 형식의" 또는 "사용자 id는 활성 SignalR 연결을 사용 하는 동안 변경할 수 없습니다." 오류</span><span class="sxs-lookup"><span data-stu-id="1f835-242">"The connection ID is in the incorrect format" or "The user identity cannot change during an active SignalR connection" error</span></span>

<span data-ttu-id="1f835-243">클라이언트 로그 아웃 됩니다. 연결을 중지 하기 전에 인증을 사용 중인 경우이 오류가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-243">This error may be seen if authentication is being used, and the client is logged out before the connection is stopped.</span></span> <span data-ttu-id="1f835-244">솔루션은 클라이언트에는 로그 아웃 하기 전에 SignalR 연결을 중지 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-244">The solution is to stop the SignalR connection before logging the client out.</span></span>

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a><span data-ttu-id="1f835-245">"오류를 확인할 수 없는: SignalR: jQuery 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-245">"Uncaught Error: SignalR: jQuery not found.</span></span> <span data-ttu-id="1f835-246">JQuery SignalR.js 파일 전에 참조를 확인 하세요"오류</span><span class="sxs-lookup"><span data-stu-id="1f835-246">Please ensure jQuery is referenced before the SignalR.js file" error</span></span>

<span data-ttu-id="1f835-247">SignalR JavaScript 클라이언트를 실행 하는 jQuery 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-247">The SignalR JavaScript client requires jQuery to run.</span></span> <span data-ttu-id="1f835-248">JQuery에 대 한 참조에 사용 되는 경로가 올바른지 및 SignalR에 대 한 참조 하기 전에 jQuery에 대 한 참조는 정확한 지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-248">Verify that your reference to jQuery is correct, that the path used is valid, and that the reference to jQuery is before the reference to SignalR.</span></span>

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a><span data-ttu-id="1f835-249">"TypeError를 확인할 수 없는: 속성을 읽을 수 없습니다. '&lt;속성&gt;' 정의 되지 않은의" 오류</span><span class="sxs-lookup"><span data-stu-id="1f835-249">"Uncaught TypeError: Cannot read property '&lt;property&gt;' of undefined" error</span></span>

<span data-ttu-id="1f835-250">jQuery 또는 적절히 참조 허브 프록시를가지고 있지 않은 경우이 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-250">This error results from not having jQuery or the hubs proxy referenced properly.</span></span> <span data-ttu-id="1f835-251">JQuery와 허브 프록시에 대 한 참조에 사용 된 경로가 유효 하며 허브 프록시에 대 한 참조 하기 전에 jQuery에 대 한 참조는 정확한 지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-251">Verify that your reference to jQuery and the hubs proxy is correct, that the path used is valid, and that the reference to jQuery is before the reference to the hubs proxy.</span></span> <span data-ttu-id="1f835-252">허브 프록시에 대 한 기본 참조는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-252">The default reference to the hubs proxy should look like the following:</span></span>

<span data-ttu-id="1f835-253">**허브 프록시를 올바르게 참조 하는 HTML 클라이언트 쪽 코드**</span><span class="sxs-lookup"><span data-stu-id="1f835-253">**HTML client-side code that correctly references the Hubs proxy**</span></span>

[!code-html[Main](troubleshooting/samples/sample12.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a><span data-ttu-id="1f835-254">"RuntimeBinderException 처리 되지 않았습니다. 사용자 코드에서" 오류</span><span class="sxs-lookup"><span data-stu-id="1f835-254">"RuntimeBinderException was unhandled by user code" error</span></span>

<span data-ttu-id="1f835-255">이 오류가 발생할 때의 잘못 된 오버 로드를 `Hub.On` 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-255">This error may occur when the incorrect overload of `Hub.On` is used.</span></span> <span data-ttu-id="1f835-256">메서드 반환 값이 있으면 반환 형식이 제네릭 형식 매개 변수로 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-256">If the method has a return value, the return type must be specified as a generic type parameter:</span></span>

<span data-ttu-id="1f835-257">**생성 된 프록시) (없이 클라이언트에 정의 된 메서드**</span><span class="sxs-lookup"><span data-stu-id="1f835-257">**Method defined on the client (without generated proxy)**</span></span>

[!code-html[Main](troubleshooting/samples/sample13.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a><span data-ttu-id="1f835-258">연결 ID 일치 하지 않습니다. 또는 페이지 로드 간의 연결을 중단 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-258">Connection ID is inconsistent or connection breaks between page loads</span></span>

<span data-ttu-id="1f835-259">이 동작은 설계 시 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-259">This behavior is by design.</span></span> <span data-ttu-id="1f835-260">Page 개체에 호스트 되는 허브 개체 이므로 허브 페이지를 새로 고칠 때 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-260">Since the hub object is hosted in the page object, the hub is destroyed when the page refreshes.</span></span> <span data-ttu-id="1f835-261">응용 프로그램을 다중 페이지는 페이지 로드 간에 일치 될 수 있도록 사용자 및 연결 Id 간의 연결을 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-261">A multi-page application needs to maintain the association between users and connection IDs so that they will be consistent between page loads.</span></span> <span data-ttu-id="1f835-262">서버 중 하나에서 연결 Id를 저장할 수 있습니다는 `ConcurrentDictionary` 개체나 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-262">The connection IDs can be stored on the server in either a `ConcurrentDictionary` object or a database.</span></span>

### <a name="value-cannot-be-null-error"></a><span data-ttu-id="1f835-263">"값은 null 일 수 없습니다" 오류</span><span class="sxs-lookup"><span data-stu-id="1f835-263">"Value cannot be null" error</span></span>

<span data-ttu-id="1f835-264">선택적 매개 변수를 사용 하 여 서버 쪽 메서드는 현재 지원 되지 않습니다. 선택적 매개 변수를 생략 하면 메서드가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-264">Server-side methods with optional parameters are not currently supported; if the optional parameter is omitted, the method will fail.</span></span> <span data-ttu-id="1f835-265">자세한 내용은 [선택적 매개 변수](https://github.com/SignalR/SignalR/issues/324)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-265">For more information, see [Optional Parameters](https://github.com/SignalR/SignalR/issues/324).</span></span>

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a><span data-ttu-id="1f835-266">"Firefox 서버에 연결할 수 없습니다 &lt;주소&gt;" Firebug에 오류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-266">"Firefox can't establish a connection to the server at &lt;address&gt;" error in Firebug</span></span>

<span data-ttu-id="1f835-267">이 오류 메시지가 표시 될 수 있습니다 Firebug에서 협상 WebSocket 전송이 실패 하 고 다른 전송 대신 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-267">This error message can be seen in Firebug if negotiation of the WebSocket transport fails and another transport is used instead.</span></span> <span data-ttu-id="1f835-268">이 동작은 설계 시 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-268">This behavior is by design.</span></span>

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a><span data-ttu-id="1f835-269">.NET 클라이언트 응용 프로그램에서 "원격 인증서 유효성 검사 절차에 따라 잘못 되었습니다." 오류</span><span class="sxs-lookup"><span data-stu-id="1f835-269">"The remote certificate is invalid according to the validation procedure" error in .NET client application</span></span>

<span data-ttu-id="1f835-270">서버에 필요한 경우 사용자 지정 클라이언트 인증서를 추가 하 여 x509certificate 연결 요청을 시작 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-270">If your server requires custom client certificates, then you can add an x509certificate to the connection before the request is made.</span></span> <span data-ttu-id="1f835-271">인증서를 사용 하 여 연결 추가 `Connection.AddClientCertificate`합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-271">Add the certificate to the connection using `Connection.AddClientCertificate`.</span></span>

### <a name="connection-drops-after-authentication-times-out"></a><span data-ttu-id="1f835-272">인증 시간 초과 후 연결 삭제</span><span class="sxs-lookup"><span data-stu-id="1f835-272">Connection drops after authentication times out</span></span>

<span data-ttu-id="1f835-273">이 동작은 설계 시 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-273">This behavior is by design.</span></span> <span data-ttu-id="1f835-274">연결이 활성; 인증 자격 증명을 수정할 수 없습니다. 자격 증명을 새로 고치려면 연결을 중지 했다가 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-274">Authentication credentials cannot be modified while a connection is active; to refresh credentials, the connection must be stopped and restarted.</span></span>

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a><span data-ttu-id="1f835-275">JQuery Mobile을 사용 하는 경우에 두 번 OnConnected 호출</span><span class="sxs-lookup"><span data-stu-id="1f835-275">OnConnected gets called twice when using jQuery Mobile</span></span>

<span data-ttu-id="1f835-276">jQuery Mobile `initializePage` 함수 강제로 다시 실행할 각 페이지의 스크립트는 두 번째 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-276">jQuery Mobile's `initializePage` function forces the scripts in each page to be re-executed, thus creating a second connection.</span></span> <span data-ttu-id="1f835-277">이 문제에 대 한 솔루션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-277">Solutions for this issue include:</span></span>

- <span data-ttu-id="1f835-278">JQuery Mobile 전에 JavaScript 파일에 대 한 참조를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-278">Include the reference to jQuery Mobile before your JavaScript file.</span></span>
- <span data-ttu-id="1f835-279">사용 하지 않도록 설정 합니다 `initializePage` 함수를 설정 하 여 `$.mobile.autoInitializePage = false`입니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-279">Disable the `initializePage` function by setting `$.mobile.autoInitializePage = false`.</span></span>
- <span data-ttu-id="1f835-280">연결을 시작 하기 전에 초기화를 완료 하려면 페이지를 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-280">Wait for the page to finish initializing before starting the connection.</span></span>

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a><span data-ttu-id="1f835-281">이벤트를 전송 하는 서버를 사용 하 여 Silverlight 응용 프로그램의 메시지 지연</span><span class="sxs-lookup"><span data-stu-id="1f835-281">Messages are delayed in Silverlight applications using Server Sent Events</span></span>

<span data-ttu-id="1f835-282">Silverlight에서 이벤트를 보낸 서버를 사용 하는 경우 메시지가 지연 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-282">Messages are delayed when using server sent events on Silverlight.</span></span> <span data-ttu-id="1f835-283">긴 폴링을 대신 사용 하도록 연결을 시작 하는 경우 다음을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-283">To force long polling to be used instead, use the following when starting the connection:</span></span>

[!code-css[Main](troubleshooting/samples/sample14.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a><span data-ttu-id="1f835-284">프로토콜 프레임 영원히 "권한 거부"를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="1f835-284">"Permission Denied" using Forever Frame protocol</span></span>

<span data-ttu-id="1f835-285">이 설명 된 알려진된 문제 [여기](https://github.com/SignalR/SignalR/issues/1963)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-285">This is a known issue, described [here](https://github.com/SignalR/SignalR/issues/1963).</span></span> <span data-ttu-id="1f835-286">최신 JQuery 라이브러리를 사용 하 여 이러한 현상이 나타날 수 있습니다. JQuery 1.8.2 응용 프로그램을 다운 그레이드 하려면이 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-286">This symptom may be seen using the latest JQuery library; the workaround is to downgrade your application to JQuery 1.8.2.</span></span>

### <a name="invalidoperationexception-not-a-valid-web-socket-request"></a><span data-ttu-id="1f835-287">"InvalidOperationException: 유효한 웹 소켓 요청 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-287">"InvalidOperationException: Not a valid web socket request.</span></span>

<span data-ttu-id="1f835-288">WebSocket 프로토콜을 사용 하지만 네트워크 프록시 요청 헤더를 수정 하는 경우이 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-288">This error may occur if the WebSocket protocol is used, but the network proxy is modifying the request headers.</span></span> <span data-ttu-id="1f835-289">솔루션 포트 80에서 WebSocket을 허용 하도록 프록시를 구성 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-289">The solution is to configure the proxy to allow WebSocket on port 80.</span></span>

### <a name="exception-ltmethod-namegt-method-could-not-be-resolved-when-client-calls-method-on-server"></a><span data-ttu-id="1f835-290">"예외: &lt;메서드 이름&gt; 메서드를 확인할 수 없는" 클라이언트가 서버에서 메서드를 호출 하는 경우</span><span class="sxs-lookup"><span data-stu-id="1f835-290">"Exception: &lt;method name&gt; method could not be resolved" when client calls method on server</span></span>

<span data-ttu-id="1f835-291">이 오류는 배열과 같이 JSON 페이로드를에서 검색 될 수 없는 데이터 형식을 사용 하 여 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-291">This error can result from using data types that cannot be discovered in a JSON payload, such as Array.</span></span> <span data-ttu-id="1f835-292">IList와 같은 JSON에서 검색할 수 있는 데이터 형식을 사용 하도록이 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-292">The workaround is to use a data type that is discoverable by JSON, such as IList.</span></span> <span data-ttu-id="1f835-293">자세한 내용은 [배열 매개 변수를 사용 하 여 허브 메서드를 호출할 수 없습니다.NET 클라이언트](https://github.com/SignalR/SignalR/issues/2672)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-293">For more information, see [.NET Client unable to call hub methods with array parameters](https://github.com/SignalR/SignalR/issues/2672).</span></span>

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a><span data-ttu-id="1f835-294">컴파일 및 서버 쪽 오류</span><span class="sxs-lookup"><span data-stu-id="1f835-294">Compilation and server-side errors</span></span>

 <span data-ttu-id="1f835-295">다음 섹션에서는 컴파일러 및 서버 쪽 런타임 오류를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-295">The following section contains possible solutions to compiler and server-side runtime errors.</span></span> 

### <a name="reference-to-hub-instance-is-null"></a><span data-ttu-id="1f835-296">허브 인스턴스에 대 한 참조는 null</span><span class="sxs-lookup"><span data-stu-id="1f835-296">Reference to Hub instance is null</span></span>

<span data-ttu-id="1f835-297">각 연결에 대 한 허브 인스턴스에 만들어지므로 만들 수 없습니다 허브 인스턴스의 코드에서 직접.</span><span class="sxs-lookup"><span data-stu-id="1f835-297">Since a hub instance is created for each connection, you can't create an instance of a hub in your code yourself.</span></span> <span data-ttu-id="1f835-298">허브 자체 외부에서 허브 메서드를 호출 하려면 참조 [클라이언트 메서드를 호출 하 여 허브 클래스 외부에서 그룹을 관리 하는 방법을](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) 허브 컨텍스트에 대 한 참조를 가져오는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-298">To call methods on a hub from outside the hub itself, see [How to call client methods and manage groups from outside the Hub class](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub) for how to obtain a reference to the hub context.</span></span>

### <a name="httpcontextcurrentsession-is-null"></a><span data-ttu-id="1f835-299">HTTPContext.Current.Session null입니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-299">HTTPContext.Current.Session is null</span></span>

<span data-ttu-id="1f835-300">이 동작은 설계 시 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-300">This behavior is by design.</span></span> <span data-ttu-id="1f835-301">SignalR 이중 메시징 중단 세션 상태를 사용 하도록 설정 하므로 ASP.NET 세션 상태를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-301">SignalR does not support the ASP.NET session state, since enabling the session state would break duplex messaging.</span></span>

### <a name="no-suitable-method-to-override"></a><span data-ttu-id="1f835-302">재정의 하는 적절 한 방법</span><span class="sxs-lookup"><span data-stu-id="1f835-302">No suitable method to override</span></span>

<span data-ttu-id="1f835-303">이전 문서 또는 블로그에서 코드를 사용 하는 경우이 오류가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-303">You may see this error if you are using code from older documentation or blogs.</span></span> <span data-ttu-id="1f835-304">변경 되었거나 더 이상 사용 되지 않는 메서드 이름을 참조 하지 않는 확인 (같은 `OnConnectedAsync`).</span><span class="sxs-lookup"><span data-stu-id="1f835-304">Verify that you are not referencing names of methods that have been changed or deprecated (like `OnConnectedAsync`).</span></span>

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a><span data-ttu-id="1f835-305">HostContextExtensions.WebSocketServerUrl null입니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-305">HostContextExtensions.WebSocketServerUrl is null</span></span>

<span data-ttu-id="1f835-306">이 동작은 설계 시 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-306">This behavior is by design.</span></span> <span data-ttu-id="1f835-307">이 멤버는 사용 되지 않으며 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-307">This member is deprecated and should not be used.</span></span>

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a><span data-ttu-id="1f835-308">"'Signalr.hubs' 경로 경로 컬렉션에 이미 됨" 오류 발생</span><span class="sxs-lookup"><span data-stu-id="1f835-308">"A route named 'signalr.hubs' is already in the route collection" error</span></span>

<span data-ttu-id="1f835-309">이 오류가 표시 됩니다 경우 `MapSignalR` 응용 프로그램에서 두 번 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-309">This error will be seen if `MapSignalR` is called twice by your application.</span></span> <span data-ttu-id="1f835-310">일부 예제 응용 프로그램 호출 `MapSignalR` 직접 시작 클래스에 게 호출 래퍼 클래스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-310">Some example applications call `MapSignalR` directly in the Startup class; others make the call in a wrapper class.</span></span> <span data-ttu-id="1f835-311">응용 프로그램 둘 다 수행 하지 않습니다 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-311">Ensure that your application does not do both.</span></span>

### <a name="websocket-is-not-used"></a><span data-ttu-id="1f835-312">WebSocket이 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-312">WebSocket is not used</span></span>

<span data-ttu-id="1f835-313">서버 및 클라이언트 WebSocket에 대 한 요구 사항을 충족 하는지 확인 한 경우 (에 나열 된는 [지원 되는 플랫폼](../getting-started/supported-platforms.md) 문서), 서버에서 WebSocket을 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-313">If you have verified that your server and clients meet the requirements for WebSocket (listed in the [Supported Platforms](../getting-started/supported-platforms.md) document), you will need to enable WebSocket on your server.</span></span> <span data-ttu-id="1f835-314">이 작업을 수행 하는 것에 대 한 지침을 찾을 수 있습니다 [여기](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-314">Instructions for doing this can be found [here](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support).</span></span>

### <a name="connection-is-undefined"></a><span data-ttu-id="1f835-315">$.connection 정의 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-315">$.connection is undefined</span></span>

<span data-ttu-id="1f835-316">이 오류는 페이지에 스크립트를 제대로 로드 되지 않은 또는 허브 프록시에 연결할 수 없습니다 또는 올바르게 액세스 하는 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-316">This error indicates that either the scripts on a page are not being loaded properly, or the hub proxy is not reachable or is being accessed incorrectly.</span></span> <span data-ttu-id="1f835-317">페이지에 스크립트 참조를 프로젝트에 로드 된 스크립트에 해당 하 고 서버가 실행 중인 경우 /signalr/hubs 브라우저에서 액세스할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-317">Verify that the script references on your page correspond to the scripts loaded in your project, and that /signalr/hubs can be accessed in a browser when the server is running.</span></span>

### <a name="one-or-more-types-required-to-compile-a-dynamic-expression-cannot-be-found"></a><span data-ttu-id="1f835-318">동적 식을 컴파일하는 데 필요한 하나 이상의 형식은 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-318">One or more types required to compile a dynamic expression cannot be found</span></span>

<span data-ttu-id="1f835-319">이 오류는 `Microsoft.CSharp` 라이브러리를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-319">This error indicates that the `Microsoft.CSharp` library is missing.</span></span> <span data-ttu-id="1f835-320">에 추가 합니다 **어셈블리-&gt;Framework** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-320">Add it in the **Assemblies-&gt;Framework** tab.</span></span>

### <a name="caller-state-cannot-be-accessed-from-clientscaller-in-visual-basic-or-in-a-strongly-typed-hub-conversion-from-type-taskof-object-to-type-string-is-not-valid-error"></a><span data-ttu-id="1f835-321">호출자가 상태 Clients.Caller Visual Basic 또는 강력한 형식의 허브;에서 액세스할 수 없습니다. "'String' 형식으로 형식 'Task (Of Object)'로의 변환이 잘못 되었습니다." 오류</span><span class="sxs-lookup"><span data-stu-id="1f835-321">Caller state cannot be accessed from Clients.Caller in Visual Basic or in a strongly typed hub; "Conversion from type 'Task(Of Object)' to type 'String' is not valid" error</span></span>

<span data-ttu-id="1f835-322">Visual basic에서 또는 강력한 형식의 허브의 호출자 상태에 액세스 하려면 사용 합니다 `Clients.CallerState` 속성 (SignalR 2.1에 도입 됨) 대신 `Clients.Caller`합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-322">To access caller state in Visual Basic or in a strongly typed hub, use the `Clients.CallerState` property (introduced in SignalR 2.1) instead of `Clients.Caller`.</span></span>

<a id="vs"></a>

## <a name="visual-studio-issues"></a><span data-ttu-id="1f835-323">Visual Studio 문제</span><span class="sxs-lookup"><span data-stu-id="1f835-323">Visual Studio issues</span></span>

<span data-ttu-id="1f835-324">이 섹션에서는 Visual Studio에서 발생 하는 문제를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-324">This section describes issues encountered in Visual Studio.</span></span>

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a><span data-ttu-id="1f835-325">솔루션 탐색기에서 스크립트 문서 노드가 표시 되지 않으면</span><span class="sxs-lookup"><span data-stu-id="1f835-325">Script Documents node does not appear in Solution Explorer</span></span>

<span data-ttu-id="1f835-326">이 자습서의 일부 디버깅 하는 동안 솔루션 탐색기에서 "스크립트 문서" 노드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-326">Some of our tutorials direct you to the "Script Documents" node in Solution Explorer while debugging.</span></span> <span data-ttu-id="1f835-327">이 노드는 JavaScript 디버거에서 생성 되 고 브라우저 클라이언트에서 Internet Explorer;를 디버깅 하는 동안에 표시 됩니다. Chrome 또는 Firefox에서 사용 하는 경우에 노드가 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-327">This node is produced by the JavaScript debugger, and will only appear while debugging browser clients in Internet Explorer; the node will not appear if Chrome or Firefox are used.</span></span> <span data-ttu-id="1f835-328">JavaScript 디버거도 실행 되지 않습니다 Silverlight 디버거와 같은 다른 클라이언트 디버거를 실행 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="1f835-328">The JavaScript debugger will also not run if another client debugger is running, such as the Silverlight debugger.</span></span>

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a><span data-ttu-id="1f835-329">또는 이전 버전 Visual Studio 2008의 SignalR 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-329">SignalR does not work on Visual Studio 2008 or earlier</span></span>

<span data-ttu-id="1f835-330">이 동작은 설계 시 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-330">This behavior is by design.</span></span> <span data-ttu-id="1f835-331">SignalR에는.NET Framework 4 이상, Visual Studio 2010 이상에서 SignalR 응용 프로그램을 개발 하는 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-331">SignalR requires .NET Framework 4 or later; this requires that SignalR applications be developed in Visual Studio 2010 or later.</span></span> <span data-ttu-id="1f835-332">SignalR의 서버 구성 요소가.NET Framework 4.5를 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-332">The server component of SignalR requires .NET Framework 4.5.</span></span>

<a id="iis"></a>

## <a name="iis-issues"></a><span data-ttu-id="1f835-333">IIS 문제</span><span class="sxs-lookup"><span data-stu-id="1f835-333">IIS issues</span></span>

<span data-ttu-id="1f835-334">이 섹션에서는 인터넷 정보 서비스를 사용 하 여 문제를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-334">This section contains issues with Internet Information Services.</span></span>

### <a name="signalr-works-on-visual-studio-development-server-but-not-in-iis"></a><span data-ttu-id="1f835-335">SignalR은 IIS 아니라 Visual Studio 개발 서버에서 작동</span><span class="sxs-lookup"><span data-stu-id="1f835-335">SignalR works on Visual Studio development server, but not in IIS</span></span>

<span data-ttu-id="1f835-336">SignalR IIS 7.0 및 7.5에서 지원 됩니다 있지만 대 한 지원이 확장명 없는 Url을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-336">SignalR is supported on IIS 7.0 and 7.5, but support for extensionless URLs must be added.</span></span> <span data-ttu-id="1f835-337">확장명 없는 Url에 대 한 지원 추가 참조 하세요. [https://support.microsoft.com/kb/980368](https://support.microsoft.com/kb/980368)</span><span class="sxs-lookup"><span data-stu-id="1f835-337">To add support for extensionless URLs, see [https://support.microsoft.com/kb/980368](https://support.microsoft.com/kb/980368)</span></span>

<span data-ttu-id="1f835-338">SignalR ASP.NET (ASP.NET은 IIS에서 기본적으로 설치 되지) 서버에 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-338">SignalR requires ASP.NET to be installed on the server (ASP.NET is not installed on IIS by default).</span></span> <span data-ttu-id="1f835-339">ASP.NET을 설치 하려면 [ASP.NET 다운로드](https://www.asp.net/downloads)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-339">To install ASP.NET, see [ASP.NET Downloads](https://www.asp.net/downloads).</span></span>

<a id="azure"></a>

## <a name="microsoft-azure-issues"></a><span data-ttu-id="1f835-340">Microsoft Azure 문제</span><span class="sxs-lookup"><span data-stu-id="1f835-340">Microsoft Azure issues</span></span>

<span data-ttu-id="1f835-341">이 섹션에서는 Microsoft Azure를 사용 하 여 문제를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-341">This section contains issues with Microsoft Azure.</span></span>

### <a name="fileloadexception-when-hosting-signalr-in-an-azure-worker-role"></a><span data-ttu-id="1f835-342">FileLoadException Azure 작업자 역할에서 SignalR을 호스팅하는 경우</span><span class="sxs-lookup"><span data-stu-id="1f835-342">FileLoadException when hosting SignalR in an Azure Worker Role</span></span>

<span data-ttu-id="1f835-343">예외가 발생할 Azure 작업자 역할에서 SignalR 호스팅 "파일이 나 어셈블리를 로드할 수 없습니다 ' Microsoft.Owin, 버전 2.0.0.0 ="입니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-343">Hosting SignalR in an Azure Worker Role might result in the exception "Could not load file or assembly 'Microsoft.Owin, Version=2.0.0.0".</span></span> <span data-ttu-id="1f835-344">이 NuGet 사용 하 여 알려진된 문제 Azure 작업자 역할 프로젝트에 바인딩 리디렉션은 자동으로 추가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-344">This is a known issue with NuGet; Binding redirects are not added automatically in Azure Worker Role projects.</span></span> <span data-ttu-id="1f835-345">이 해결 하려면 바인딩 리디렉션을 수동으로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-345">To fix this, you can add the binding redirects manually.</span></span> <span data-ttu-id="1f835-346">다음 줄을 추가 하 여 `app.config` 작업자 역할 프로젝트에 대 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-346">Add the following lines to the `app.config` file for your Worker Role project.</span></span>

[!code-xml[Main](troubleshooting/samples/sample15.xml)]

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a><span data-ttu-id="1f835-347">토픽 이름 변경 후 Azure 백플레인에서 통해 메시지가 수신 되지 않은</span><span class="sxs-lookup"><span data-stu-id="1f835-347">Messages are not received through the Azure backplane after altering topic names</span></span>

<span data-ttu-id="1f835-348">Azure 백플레인에서에서 사용 하는 항목을 내부적으로 유지 됩니다. 이러한는 사용자를 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1f835-348">The topics used by the Azure backplane are maintained internally; they are not intended to be user-configurable.</span></span>
