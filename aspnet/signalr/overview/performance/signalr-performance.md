---
uid: signalr/overview/performance/signalr-performance
title: SignalR 성능 | Microsoft Docs
author: bradygaster
description: SignalR 성능
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 3751f5e7-59db-4be0-a290-50abc24e5c84
msc.legacyurl: /signalr/overview/performance/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: 3326c2e600854fc7a4435d96c45b04a6188d3937
ms.sourcegitcommit: ebf4e5a7ca301af8494edf64f85d4a8deb61d641
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54836514"
---
<a name="signalr-performance"></a><span data-ttu-id="34758-103">SignalR 성능</span><span class="sxs-lookup"><span data-stu-id="34758-103">SignalR Performance</span></span>
====================
<span data-ttu-id="34758-104">[Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="34758-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="34758-105">이 항목에 대 한 디자인, 측정 및 SignalR 응용 프로그램의 성능을 향상 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-105">This topic describes how to design for, measure, and improve performance in a SignalR application.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="34758-106">이 항목에서 사용 하는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="34758-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="34758-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="34758-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="34758-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="34758-108">.NET 4.5</span></span>
> - <span data-ttu-id="34758-109">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="34758-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="34758-110">이 항목의 이전 버전</span><span class="sxs-lookup"><span data-stu-id="34758-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="34758-111">이전 버전의 SignalR에 대 한 정보를 참조 하세요 [SignalR 이전 버전](../older-versions/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="34758-112">질문이 나 의견이 있으면</span><span class="sxs-lookup"><span data-stu-id="34758-112">Questions and comments</span></span>
>
> <span data-ttu-id="34758-113">이 자습서를 연결 하는 방법 및 새로운 개선할 수 있습니다 페이지의 맨 아래에 의견에서에 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="34758-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="34758-114">에 자습서로 직접 관련 되지 않은 질문이 있을 경우 게시할 수 하는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


<span data-ttu-id="34758-115">SignalR 성능 및 크기 조정에서 최근 프레젠테이션을 참조 하세요 [ASP.NET SignalR을 사용 하 여 실시간 웹 크기 조정](https://channel9.msdn.com/Events/Build/2013/3-502)합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-115">For a recent presentation on SignalR performance and scaling, see [Scaling the Real-time Web with ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span></span>

<span data-ttu-id="34758-116">이 항목에는 다음과 같은 단원이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34758-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="34758-117">디자인 고려 사항</span><span class="sxs-lookup"><span data-stu-id="34758-117">Design considerations</span></span>](#design)
- [<span data-ttu-id="34758-118">SignalR 서버 성능 튜닝</span><span class="sxs-lookup"><span data-stu-id="34758-118">Tuning your SignalR server for performance</span></span>](#tuning)
- [<span data-ttu-id="34758-119">성능 문제 해결</span><span class="sxs-lookup"><span data-stu-id="34758-119">Troubleshooting performance issues</span></span>](#troubleshooting)
- [<span data-ttu-id="34758-120">SignalR 성능 카운터를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="34758-120">Using SignalR performance counters</span></span>](#perfcounters)
- [<span data-ttu-id="34758-121">다른 성능 카운터를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="34758-121">Using other performance counters</span></span>](#othercounters)
- [<span data-ttu-id="34758-122">기타 리소스</span><span class="sxs-lookup"><span data-stu-id="34758-122">Other resources</span></span>](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a><span data-ttu-id="34758-123">디자인 고려 사항</span><span class="sxs-lookup"><span data-stu-id="34758-123">Design considerations</span></span>

<span data-ttu-id="34758-124">이 섹션에서는 성능 불필요 한 네트워크 트래픽을 생성 하 여 하지 저하 되는 되도록 SignalR 응용 프로그램을 설계할 때 구현할 수 있는 패턴을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-124">This section describes patterns that can be implemented during the design of a SignalR application, to ensure that performance is not being hindered by generating unnecessary network traffic.</span></span>

### <a name="throttling-message-frequency"></a><span data-ttu-id="34758-125">메시지 빈도 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-125">Throttling message frequency</span></span>

<span data-ttu-id="34758-126">(예: 실시간 게임 응용 프로그램)는 높은 빈도로 메시지를 전송 하는 응용 프로그램에도 대부분의 응용 프로그램을 두 번째로 많은 메시지를 보낼 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="34758-126">Even in an application that sends out messages at a high frequency (such as a realtime gaming application), most applications don't need to send more than a few messages a second.</span></span> <span data-ttu-id="34758-127">각 클라이언트를 생성 하는 트래픽 용량을 줄이기 위해 메시지 루프를 구현할 수 있습니다 큐 및 보내는 아웃 보다 자주 고정된 요금 메시지는 (즉, 특정 개수의 메시지를 최대 보내집니다 매초에서 해당 시간에 메시지가 있는 경우 보낼 terval)입니다.</span><span class="sxs-lookup"><span data-stu-id="34758-127">To reduce the amount of traffic that each client generates, a message loop can be implemented that queues and sends out messages no more frequently than a fixed rate (that is, up to a certain number of messages will be sent every second, if there are messages in that time interval to be sent).</span></span> <span data-ttu-id="34758-128">(클라이언트 및 서버)에서 특정 속도로 메시지를 제한 하는 샘플 응용 프로그램을 참조 하세요 [SignalR 고주파수](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-128">For a sample application that throttles messages to a certain rate (from both client and server), see [High-Frequency Realtime with SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span></span>

### <a name="reducing-message-size"></a><span data-ttu-id="34758-129">메시지 크기를 줄임으로써</span><span class="sxs-lookup"><span data-stu-id="34758-129">Reducing message size</span></span>

<span data-ttu-id="34758-130">Serialize 된 개체의 크기를 줄임으로써 SignalR 메시지의 크기를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34758-130">You can reduce the size of a SignalR message by reducing the size of your serialized objects.</span></span> <span data-ttu-id="34758-131">서버 코드에서 전송할 필요가 없는 속성을 포함 하는 개체를 보내는 경우 방지 속성만 사용 하 여 serialize 되는 `JsonIgnore` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="34758-131">In server code, if you're sending an object that contains properties that don't need to be transmitted, prevent those properties from being serialized by using the `JsonIgnore` attribute.</span></span> <span data-ttu-id="34758-132">속성의 이름은 메시지에도 저장 됩니다. 속성의 이름을 사용 하 여 줄일 수 있습니다는 `JsonProperty` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="34758-132">The names of properties are also stored in the message; the names of properties can be shortened using the `JsonProperty` attribute.</span></span> <span data-ttu-id="34758-133">다음 코드 샘플에는 클라이언트에 전송 되는 속성을 제외 하는 방법 및 속성 이름을 단축 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="34758-133">The following code sample demonstrates how to exclude a property from being sent to the client, and how to shorten property names:</span></span>

<span data-ttu-id="34758-134">**클라이언트에 전송 중인 데이터를 제외할 JsonIgnore 특성 및 메시지 크기를 줄이기 위해 JsonProperty 특성을 보여 주는.NET 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="34758-134">**.NET server code that demonstrates the JsonIgnore attribute to exclude data from being sent to the client, and the JsonProperty attribute to reduce message size**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

<span data-ttu-id="34758-135">가독성을 유지 하기 위해 / 클라이언트 코드에서 유지 관리를 약식된 속성 이름을 사람이 읽기 편한 매핑된 이름 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-135">In order to retain readability/ maintainability in the client code, the abbreviated property names can be remapped to human-friendly names after the message is received.</span></span> <span data-ttu-id="34758-136">다음 코드 샘플을 보여 줍니다 (매핑), 메시지 계약을 정의 하 여 길이가 더 긴 약식된 이름 다시 매핑의 한 가지 방법을 사용 하는 `reMap` 계약 최적화 된 메시지 클래스에 적용할 함수입니다:</span><span class="sxs-lookup"><span data-stu-id="34758-136">The following code sample demonstrates one possible way of remapping shortened names to longer ones, by defining a message contract (mapping), and using the `reMap` function to apply the contract to the optimized message class:</span></span>

<span data-ttu-id="34758-137">**클라이언트 쪽 JavaScript 코드가 다시 매핑하는 알기 쉬운 이름으로 속성 이름 단축**</span><span class="sxs-lookup"><span data-stu-id="34758-137">**Client-side JavaScript code that remaps shortened property names to human-readable names**</span></span>

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

<span data-ttu-id="34758-138">이름이 같은 메서드를 사용 하 여도 서버에 클라이언트에서 메시지에 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34758-138">Names can be shortened in messages from the client to the server as well, using the same method.</span></span>

<span data-ttu-id="34758-139">메모리 사용 공간 (즉, 메시지에 사용 되는 메모리의 양)를 줄이고 메시지의 개체 성능을 향상할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34758-139">Reducing the memory footprint (that is, the amount of memory used for the message) of the message object can also improve performance.</span></span> <span data-ttu-id="34758-140">예를 들어 경우의 전체 범위는 `int` 필요 하지 않은 `short` 또는 `byte` 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34758-140">For example, if the full range of an `int` is not needed, a `short` or `byte` can be used instead.</span></span>

<span data-ttu-id="34758-141">메시지의 크기를 줄이면 서버 메모리에 메시지 버스에서 메시지 저장 되므로 서버 메모리 문제를 해결 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34758-141">Since messages are stored in the message bus in server memory, reducing the size of messages can also address server memory issues.</span></span>

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a><span data-ttu-id="34758-142">SignalR 서버 성능 튜닝</span><span class="sxs-lookup"><span data-stu-id="34758-142">Tuning your SignalR server for performance</span></span>

<span data-ttu-id="34758-143">SignalR 응용 프로그램에서 성능 향상을 위해 서버를 튜닝 하려면 다음 구성 설정은 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34758-143">The following configuration settings can be used to tune your server for better performance in a SignalR application.</span></span> <span data-ttu-id="34758-144">ASP.NET 응용 프로그램에서 성능 향상 방법에 대 한 일반 정보를 참조 하세요 [ASP.NET 성능 향상](https://msdn.microsoft.com/library/ff647787.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-144">For general information on how to improve performance in an ASP.NET application, see [Improving ASP.NET Performance](https://msdn.microsoft.com/library/ff647787.aspx).</span></span>

<span data-ttu-id="34758-145">**SignalR 구성 설정**</span><span class="sxs-lookup"><span data-stu-id="34758-145">**SignalR configuration settings**</span></span>

- <span data-ttu-id="34758-146">**DefaultMessageBufferSize**: 기본적으로 SignalR 허브 연결당 당 메모리에 1000 개의 메시지를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-146">**DefaultMessageBufferSize**: By default, SignalR retains 1000 messages in memory per hub per connection.</span></span> <span data-ttu-id="34758-147">큰 메시지를 사용 하는 경우이이 값을 줄여 완화할 수 있는 메모리 문제를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34758-147">If large messages are being used, this may create memory issues which can be alleviated by reducing this value.</span></span> <span data-ttu-id="34758-148">이 설정을 지정할 수 있습니다 합니다 `Application_Start` 또는 ASP.NET 응용 프로그램에서 이벤트 처리기는 `Configuration` 자체 호스팅된 응용 프로그램의 OWIN 시작 클래스의 메서드.</span><span class="sxs-lookup"><span data-stu-id="34758-148">This setting can be set in the `Application_Start` event handler in an ASP.NET application, or in the `Configuration` method of an OWIN startup class in a self-hosted application.</span></span> <span data-ttu-id="34758-149">다음 샘플을 사용 하는 서버 메모리의 양을 줄이기 위해 응용 프로그램의 메모리 공간을 줄이기 위해이 값을 줄이는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="34758-149">The following sample demonstrates how to reduce this value in order to reduce the memory footprint of your application in order to reduce the amount of server memory used:</span></span>

    <span data-ttu-id="34758-150">**기본 메시지 버퍼 크기를 줄이는 것에 대 한 Startup.cs에서.NET 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="34758-150">**.NET server code in Startup.cs for decreasing default message buffer size**</span></span>

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

<span data-ttu-id="34758-151">**IIS 구성 설정**</span><span class="sxs-lookup"><span data-stu-id="34758-151">**IIS configuration settings**</span></span>

- <span data-ttu-id="34758-152">**응용 프로그램 당 최대 동시 요청**: 동시 IIS의 수를 늘리면 요청 요청을 처리 하는 것에 대 한 사용 가능한 서버 리소스를 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-152">**Max concurrent requests per application**: Increasing the number of concurrent IIS requests will increase server resources available for serving requests.</span></span> <span data-ttu-id="34758-153">기본값은 5000입니다. 이 설정을 늘릴, 관리자 권한 명령 프롬프트에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-153">The default value is 5000; to increase this setting, execute the following commands in an elevated command prompt:</span></span>

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- <span data-ttu-id="34758-154">**ApplicationPool QueueLength**: 응용 프로그램 풀에 대 한 Http.sys 큐는 요청의 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="34758-154">**ApplicationPool QueueLength**: This is the maximum number of requests that Http.sys queues for the application pool.</span></span> <span data-ttu-id="34758-155">큐 가득 차면 새 요청 503 "서비스를 사용할 수 없음" 응답을 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-155">When the queue is full, new requests receive a 503 "Service Unavailable" response.</span></span> <span data-ttu-id="34758-156">기본값은 1000입니다.</span><span class="sxs-lookup"><span data-stu-id="34758-156">The default value is 1000.</span></span>

    <span data-ttu-id="34758-157">응용 프로그램을 호스팅하는 응용 프로그램 풀에서 작업자 프로세스에 대 한 큐 길이 줄이는 메모리 리소스가 절약 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34758-157">Shortening the queue length for the worker process in the application pool hosting your application will conserve memory resources.</span></span> <span data-ttu-id="34758-158">자세한 내용은 [관리, 튜닝, 및 응용 프로그램 풀 구성](https://technet.microsoft.com/library/cc745955.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-158">For more information, see [Managing, Tuning, and Configuring Application Pools](https://technet.microsoft.com/library/cc745955.aspx).</span></span>

<span data-ttu-id="34758-159">**ASP.NET 구성 설정**</span><span class="sxs-lookup"><span data-stu-id="34758-159">**ASP.NET configuration settings**</span></span>

<span data-ttu-id="34758-160">이 섹션에서는 구성 파일에서 설정할 수 있는 `aspnet.config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="34758-160">This section includes configuration settings that can be set in the `aspnet.config` file.</span></span> <span data-ttu-id="34758-161">이 파일은 플랫폼에 따라 두 위치 중 하나에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34758-161">This file is found in one of two locations, depending on platform:</span></span>

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

<span data-ttu-id="34758-162">SignalR 성능 향상 시킬 수 있는 ASP.NET 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="34758-162">ASP.NET settings that may improve SignalR performance include the following:</span></span>

- <span data-ttu-id="34758-163">**CPU 당 최대 동시 요청**: 이 설정을 성능 병목 현상을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34758-163">**Maximum concurrent requests per CPU**: Increasing this setting may alleviate performance bottlenecks.</span></span> <span data-ttu-id="34758-164">이 설정을 늘릴를 추가 하려면 다음 구성 설정을 `aspnet.config` 파일:</span><span class="sxs-lookup"><span data-stu-id="34758-164">To increase this setting, add the following configuration setting to the `aspnet.config` file:</span></span>

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- <span data-ttu-id="34758-165">**요청 큐 제한**: 총 연결 수를 초과 하는 경우는 `maxConcurrentRequestsPerCPU` 설정을 ASP.NET 요청 큐를 사용 하 여 제한을 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34758-165">**Request Queue Limit**: When the total number of connections exceeds the `maxConcurrentRequestsPerCPU` setting, ASP.NET will start throttling requests using a queue.</span></span> <span data-ttu-id="34758-166">큐의 크기를 늘리려면 늘릴 수 있습니다는 `requestQueueLimit` 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-166">To increase the size of the queue, you can increase the `requestQueueLimit` setting.</span></span> <span data-ttu-id="34758-167">이 작업을 수행 하려면 다음 구성 설정을 추가 합니다 `processModel` 에 노드 `config/machine.config` (대신 `aspnet.config`):</span><span class="sxs-lookup"><span data-stu-id="34758-167">To do this, add the following configuration setting to the `processModel` node in `config/machine.config` (rather than `aspnet.config`):</span></span>

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a><span data-ttu-id="34758-168">성능 문제 해결</span><span class="sxs-lookup"><span data-stu-id="34758-168">Troubleshooting performance issues</span></span>

<span data-ttu-id="34758-169">이 섹션에서는 응용 프로그램에서 성능 병목 지점을 찾는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-169">This section describes ways to find performance bottlenecks in your application.</span></span>

### <a name="verifying-that-websocket-is-being-used"></a><span data-ttu-id="34758-170">WebSocket 사용 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-170">Verifying that WebSocket is being used</span></span>

<span data-ttu-id="34758-171">SignalR 클라이언트와 서버 간의 통신에 대 한 다양 한 전송 방식 사용할 수 있습니다, WebSocket 상당한 성능 이점이 클라이언트 및 서버를 지 원하는 경우에 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-171">While SignalR can use a variety of transports for communication between client and server, WebSocket offers a significant performance advantage, and should be used if the client and server support it.</span></span> <span data-ttu-id="34758-172">클라이언트 및 서버에 WebSocket에 대 한 요구 사항을 충족 하는 경우를 확인 하려면 참조 [전송과 대체](../getting-started/introduction-to-signalr.md#transports)합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-172">To determine if your client and server meet the requirements for WebSocket, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="34758-173">전송 되는 응용 프로그램을 확인 하려면 브라우저 개발자 도구를 사용할 수 있으며 로그 전송 연결에 사용 되는 검사 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="34758-173">To determine what transport is being used in your application, you can use the browser developer tools, and examine the logs to see what transport is being used for the connection.</span></span> <span data-ttu-id="34758-174">Internet Explorer 및 Chrome 브라우저 개발 도구 사용에 대 한 자세한 내용은 [전송과 대체](../getting-started/introduction-to-signalr.md#transports)합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-174">For information on using the browser development tools in Internet Explorer and Chrome, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a><span data-ttu-id="34758-175">SignalR 성능 카운터를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="34758-175">Using SignalR performance counters</span></span>

<span data-ttu-id="34758-176">이 섹션에서는 사용 하 여 SignalR 성능 카운터를 사용 하는 방법을 설명에 `Microsoft.AspNet.SignalR.Utils` 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-176">This section describes how to enable and use SignalR performance counters, found in the `Microsoft.AspNet.SignalR.Utils` package.</span></span>

### <a name="installing-signalrexe"></a><span data-ttu-id="34758-177">Signalr.exe 설치</span><span class="sxs-lookup"><span data-stu-id="34758-177">Installing signalr.exe</span></span>

<span data-ttu-id="34758-178">성능 카운터 SignalR.exe 라는 유틸리티를 사용 하 여 서버에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34758-178">Performance counters can be added to the server using a utility called SignalR.exe.</span></span> <span data-ttu-id="34758-179">이 유틸리티를 설치 하려면 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-179">To install this utility, follow these steps:</span></span>

1. <span data-ttu-id="34758-180">Visual Studio에서 선택 **도구가** > **NuGet 패키지 관리자** > **솔루션용 NuGet 패키지 관리**</span><span class="sxs-lookup"><span data-stu-id="34758-180">In Visual Studio, select **Tools** > **NuGet Package Manager** > **Manage NuGet Packages for Solution**</span></span>
2. <span data-ttu-id="34758-181">검색할 **signalr.utils**, 설치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-181">Search for **signalr.utils**, and select Install.</span></span>

    ![](signalr-performance/_static/image1.png)
3. <span data-ttu-id="34758-182">패키지를 설치 하려면 사용권 계약에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-182">Accept the license agreement to install the package.</span></span>
4. <span data-ttu-id="34758-183">SignalR.exe 되도록 설치 됩니다. `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-183">SignalR.exe will be installed to `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span></span>

### <a name="installing-performance-counters-with-signalrexe"></a><span data-ttu-id="34758-184">SignalR.exe를 사용 하 여 성능 카운터를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-184">Installing performance counters with SignalR.exe</span></span>

<span data-ttu-id="34758-185">SignalR 성능 카운터를 설치 하려면 다음 매개 변수를 사용 하 여 관리자 권한 명령 프롬프트에서 SignalR.exe를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-185">To install SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

<span data-ttu-id="34758-186">SignalR 성능 카운터를 제거 하려면 다음 매개 변수를 사용 하 여 관리자 권한 명령 프롬프트에서 SignalR.exe를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-186">To remove SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a><span data-ttu-id="34758-187">SignalR 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="34758-187">SignalR Performance counters</span></span>

<span data-ttu-id="34758-188">유틸리티 패키지는 다음 성능 카운터를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-188">The utilities package installs the following performance counters.</span></span> <span data-ttu-id="34758-189">마지막 응용 프로그램 풀에 서버를 다시 시작한 이후 "전체" 카운터 이벤트 수를 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-189">The "Total" counters measure the number of events since the last application pool or server restart.</span></span>

<span data-ttu-id="34758-190">**연결 메트릭**</span><span class="sxs-lookup"><span data-stu-id="34758-190">**Connection metrics**</span></span>

<span data-ttu-id="34758-191">다음 메트릭을 측정 연결 수명 이벤트를 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-191">The following metrics measure the connection lifetime events that occur.</span></span> <span data-ttu-id="34758-192">자세한 내용은 [이해 하 고 연결 수명 이벤트 처리](../guide-to-the-api/handling-connection-lifetime-events.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-192">For more information, see [Understanding and Handling Connection Lifetime Events](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

- <span data-ttu-id="34758-193">**연결 된 연결**</span><span class="sxs-lookup"><span data-stu-id="34758-193">**Connections Connected**</span></span>
- <span data-ttu-id="34758-194">**다시 연결**</span><span class="sxs-lookup"><span data-stu-id="34758-194">**Connections Reconnected**</span></span>
- <span data-ttu-id="34758-195">**연결이 끊긴 연결**</span><span class="sxs-lookup"><span data-stu-id="34758-195">**Connections Disconnected**</span></span>
- <span data-ttu-id="34758-196">**현재 연결**</span><span class="sxs-lookup"><span data-stu-id="34758-196">**Connections Current**</span></span>

<span data-ttu-id="34758-197">**메시지 메트릭스**</span><span class="sxs-lookup"><span data-stu-id="34758-197">**Message metrics**</span></span>

<span data-ttu-id="34758-198">다음 메트릭은 SignalR에서 생성 되는 메시지 트래픽을 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-198">The following metrics measure the message traffic generated by SignalR.</span></span>

- <span data-ttu-id="34758-199">**총 받은 연결 메시지**</span><span class="sxs-lookup"><span data-stu-id="34758-199">**Connection Messages Received Total**</span></span>
- <span data-ttu-id="34758-200">**총 보낸 연결 메시지**</span><span class="sxs-lookup"><span data-stu-id="34758-200">**Connection Messages Sent Total**</span></span>
- <span data-ttu-id="34758-201">**연결에 수신 메시지/초**</span><span class="sxs-lookup"><span data-stu-id="34758-201">**Connection Messages Received/Sec**</span></span>
- <span data-ttu-id="34758-202">**연결 메시지 전송 수/초**</span><span class="sxs-lookup"><span data-stu-id="34758-202">**Connection Messages Sent/Sec**</span></span>

<span data-ttu-id="34758-203">**메시지 버스 메트릭**</span><span class="sxs-lookup"><span data-stu-id="34758-203">**Message bus metrics**</span></span>

<span data-ttu-id="34758-204">다음 메트릭은 내부 SignalR 메시지 버스에 배치 되는 모든 들어오고 나가는 SignalR 메시지 큐를 통해 트래픽을 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-204">The following metrics measure traffic through the internal SignalR message bus, the queue in which all incoming and outgoing SignalR messages are placed.</span></span> <span data-ttu-id="34758-205">메시지가 **게시** 전송 되거나 브로드캐스트 경우.</span><span class="sxs-lookup"><span data-stu-id="34758-205">A message is **Published** when it is sent or broadcast.</span></span> <span data-ttu-id="34758-206">A **구독자** 이 컨텍스트에서 메시지 버스에서 구독, 클라이언트 및 서버 자체의 수는 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-206">A **Subscriber** in this context is a subscription on the message bus; this should equal the number of clients plus the server itself.</span></span> <span data-ttu-id="34758-207">**할당 된 작업자** 활성 연결;에 데이터를 전송 하는 구성 요소를 **바쁜 작업자** 메시지를 보내는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="34758-207">An **Allocated Worker** is a component that sends data to active connections; a **Busy Worker** is one that is actively sending a message.</span></span>

- <span data-ttu-id="34758-208">**메시지 버스 받은 총 메시지 수**</span><span class="sxs-lookup"><span data-stu-id="34758-208">**Message Bus Messages Received Total**</span></span>
- <span data-ttu-id="34758-209">**메시지 버스 메시지 Received/Sec**</span><span class="sxs-lookup"><span data-stu-id="34758-209">**Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="34758-210">**메시지 버스 메시지 총 게시**</span><span class="sxs-lookup"><span data-stu-id="34758-210">**Message Bus Messages Published Total**</span></span>
- <span data-ttu-id="34758-211">**메시지 버스에 게시 된 초당 메시지**</span><span class="sxs-lookup"><span data-stu-id="34758-211">**Message Bus Messages Published/Sec**</span></span>
- <span data-ttu-id="34758-212">**메시지 버스 구독자 현재**</span><span class="sxs-lookup"><span data-stu-id="34758-212">**Message Bus Subscribers Current**</span></span>
- <span data-ttu-id="34758-213">**메시지 버스에 대 한 구독자 총 수**</span><span class="sxs-lookup"><span data-stu-id="34758-213">**Message Bus Subscribers Total**</span></span>
- <span data-ttu-id="34758-214">**메시지 버스 구독자/Sec**</span><span class="sxs-lookup"><span data-stu-id="34758-214">**Message Bus Subscribers/Sec**</span></span>
- <span data-ttu-id="34758-215">**메시지 버스 작업자 할당**</span><span class="sxs-lookup"><span data-stu-id="34758-215">**Message Bus Allocated Workers**</span></span>
- <span data-ttu-id="34758-216">**메시지 버스 작업 중인 작업자**</span><span class="sxs-lookup"><span data-stu-id="34758-216">**Message Bus Busy Workers**</span></span>
- <span data-ttu-id="34758-217">**메시지 버스 항목 현재**</span><span class="sxs-lookup"><span data-stu-id="34758-217">**Message Bus Topics Current**</span></span>

<span data-ttu-id="34758-218">**오차 메트릭**</span><span class="sxs-lookup"><span data-stu-id="34758-218">**Error metrics**</span></span>

<span data-ttu-id="34758-219">다음 메트릭은 SignalR 메시지 트래픽에 의해 생성 된 오류를 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-219">The following metrics measure errors generated by SignalR message traffic.</span></span> <span data-ttu-id="34758-220">**허브 확인** 허브 또는 허브 메서드를 확인할 수 없는 경우 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-220">**Hub Resolution** errors occur when a hub or hub method cannot be resolved.</span></span> <span data-ttu-id="34758-221">**허브 호출** 오류는 허브 메서드를 호출 하는 동안 throw 된 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="34758-221">**Hub Invocation** errors are exceptions thrown while invoking a hub method.</span></span> <span data-ttu-id="34758-222">**전송** 오류는 HTTP 요청 또는 응답 하는 동안 발생 하는 연결 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="34758-222">**Transport** errors are connection errors thrown during an HTTP request or response.</span></span>

- <span data-ttu-id="34758-223">**오류: 모든 합계**</span><span class="sxs-lookup"><span data-stu-id="34758-223">**Errors: All Total**</span></span>
- <span data-ttu-id="34758-224">**오류: All/Sec**</span><span class="sxs-lookup"><span data-stu-id="34758-224">**Errors: All/Sec**</span></span>
- <span data-ttu-id="34758-225">**오류: 허브 확인 합계**</span><span class="sxs-lookup"><span data-stu-id="34758-225">**Errors: Hub Resolution Total**</span></span>
- <span data-ttu-id="34758-226">**오류: 초당 허브 확인**</span><span class="sxs-lookup"><span data-stu-id="34758-226">**Errors: Hub Resolution/Sec**</span></span>
- <span data-ttu-id="34758-227">**오류: 허브 호출 합계**</span><span class="sxs-lookup"><span data-stu-id="34758-227">**Errors: Hub Invocation Total**</span></span>
- <span data-ttu-id="34758-228">**오류: 초당 허브 호출**</span><span class="sxs-lookup"><span data-stu-id="34758-228">**Errors: Hub Invocation/Sec**</span></span>
- <span data-ttu-id="34758-229">**오류: 전송 합계**</span><span class="sxs-lookup"><span data-stu-id="34758-229">**Errors: Transport Total**</span></span>
- <span data-ttu-id="34758-230">**오류: Transport/Sec**</span><span class="sxs-lookup"><span data-stu-id="34758-230">**Errors: Transport/Sec**</span></span>

<a id="scaleout_metrics"></a>

<span data-ttu-id="34758-231">**확장 메트릭**</span><span class="sxs-lookup"><span data-stu-id="34758-231">**Scaleout metrics**</span></span>

<span data-ttu-id="34758-232">다음 메트릭은 트래픽 및 확장 공급자에 의해 생성 된 오류를 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-232">The following metrics measure traffic and errors generated by the scaleout provider.</span></span> <span data-ttu-id="34758-233">A **Stream** 이 컨텍스트에서 확장 공급자에서 사용 하는 배율 단위는이 테이블은 SQL Server를 사용 하는 경우, Service Bus를 사용 하면 토픽 및 구독 Redis 사용 되는 경우.</span><span class="sxs-lookup"><span data-stu-id="34758-233">A **Stream** in this context is a scale unit used by the scaleout provider; this is a table if SQL Server is used, a Topic if Service Bus is used, and a Subscription if Redis is used.</span></span> <span data-ttu-id="34758-234">각 스트림 하면 정렬 된 읽기 및 쓰기 작업 단일 스트림을 잠재적 확장 병목 상태 이므로 해당 병목 상태를 줄일 수 있도록 스트림 수를 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34758-234">Each stream ensures ordered read and write operations; a single stream is a potential scale bottleneck, so the number of streams can be increased to help reduce that bottleneck.</span></span> <span data-ttu-id="34758-235">여러 개의 스트림을 사용 하는 경우 SignalR 순서에서 지정된 된 연결에서 보낸 메시지를 확인 하는 방식으로 이러한 스트림에서 (분할) 메시지를 자동으로 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34758-235">If multiple streams are used, SignalR will automatically distribute (shard) messages across these streams in a way that ensures messages sent from any given connection are in order.</span></span>

<span data-ttu-id="34758-236">합니다 [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) 컨트롤 SignalR에서 유지 관리 확장 송신 큐의 길이 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-236">The [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) setting controls the length of the scaleout send queue maintained by SignalR.</span></span> <span data-ttu-id="34758-237">설정 값으로 0 모든 메시지가 한 번에 하나씩로 보내도록 구성 된를 메시징 백플레인으로 송신 큐에 배치 하는 보다 큰 합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-237">Setting it to a value greater than 0 will place all messages in a send queue to be sent one at a time to the configured messaging backplane.</span></span> <span data-ttu-id="34758-238">큐의 크기 구성 된 길이 초과, 하는 경우는 보내도록 후속 호출은 즉시 실패를 [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) 설정 보다 낮은 큐의 메시지 수가 될 때까지 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-238">If the size of the queue goes above the configured length, subsequent calls to send will fail immediately with an [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) until the number of messages in the queue is less than the setting again.</span></span> <span data-ttu-id="34758-239">큐는 구현 된 백플레인 일반적으로 있는 고유한 큐 또는 흐름 제어 하기 때문에 기본적으로 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34758-239">Queueing is disabled by default because the implemented backplanes generally have their own queuing or flow-control in place.</span></span> <span data-ttu-id="34758-240">SQL Server의 경우 한 번에 진행 하는 전송 수를 제한 효과적으로 연결 풀링을 합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-240">In the case of SQL Server, connection pooling effectively limits the number of sends going on at any one time.</span></span>

<span data-ttu-id="34758-241">기본적으로 SQL Server 및 Redis에 대 한 스트림이 하나만 되 고 Service Bus에 대 한 5 개의 스트림이 사용 되는, 큐를 사용 하지 않도록 설정 하며 SQL Server 및 Service Bus에 대 한 구성을 통해 이러한 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34758-241">By default, only one stream is used for SQL Server and Redis, five streams are used for Service Bus, and queueing is disabled, but these settings can be changed through configuration on SQL Server and Service Bus:</span></span>

<span data-ttu-id="34758-242">**SQL Server 백플레인에 대 한 테이블 개수 및 큐 길이 구성 하는 것에 대 한.NET 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="34758-242">**.NET Server Code for configuring table count and queue length for SQL Server backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

<span data-ttu-id="34758-243">**Service Bus 백플레인에 대 한 항목 수 및 큐 길이 구성 하는 것에 대 한.NET 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="34758-243">**.NET Server Code for configuring topic count and queue length for Service Bus backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

<span data-ttu-id="34758-244">A **버퍼링** 스트림이 오류 상태가 된; 스트림이 오류 상태에 하는 경우를 백플레인에 보낸 모든 메시지 스트림을 더 이상 오류가 발생할 때까지 즉시 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-244">A **Buffering** stream is one that has entered a faulted state; when the stream is in the faulted state, all messages sent to the backplane will fail immediately until the stream is no longer faulting.</span></span> <span data-ttu-id="34758-245">합니다 **전송 큐 길이** 게시 되었지만 아직 보내지 않은 메시지 수입니다.</span><span class="sxs-lookup"><span data-stu-id="34758-245">The **Send Queue Length** is the number of messages that have been posted but not yet sent.</span></span>

- <span data-ttu-id="34758-246">**확장 메시지 버스 메시지 Received/Sec**</span><span class="sxs-lookup"><span data-stu-id="34758-246">**Scaleout Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="34758-247">**확장 스트림 합계**</span><span class="sxs-lookup"><span data-stu-id="34758-247">**Scaleout Streams Total**</span></span>
- <span data-ttu-id="34758-248">**Scaleout 스트림 열기**</span><span class="sxs-lookup"><span data-stu-id="34758-248">**Scaleout Streams Open**</span></span>
- <span data-ttu-id="34758-249">**Scaleout 스트림 버퍼링**</span><span class="sxs-lookup"><span data-stu-id="34758-249">**Scaleout Streams Buffering**</span></span>
- <span data-ttu-id="34758-250">**총 확장 오류 수**</span><span class="sxs-lookup"><span data-stu-id="34758-250">**Scaleout Errors Total**</span></span>
- <span data-ttu-id="34758-251">**초당 확장 오류**</span><span class="sxs-lookup"><span data-stu-id="34758-251">**Scaleout Errors/Sec**</span></span>
- <span data-ttu-id="34758-252">**Scaleout Send Queue Length**</span><span class="sxs-lookup"><span data-stu-id="34758-252">**Scaleout Send Queue Length**</span></span>

<span data-ttu-id="34758-253">이러한 카운터는 측정 되는 항목에 대 한 자세한 내용은 참조 하세요. [Azure Service Bus로 SignalR 규모 확장](scaleout-with-windows-azure-service-bus.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="34758-253">For more information on what these counters are measuring, see [SignalR Scaleout with Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span></span>

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a><span data-ttu-id="34758-254">다른 성능 카운터를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="34758-254">Using other performance counters</span></span>

<span data-ttu-id="34758-255">다음 성능 카운터는 응용 프로그램의 성능을 모니터링할 때 유용한 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34758-255">The following performance counters may also be useful in monitoring your application's performance.</span></span>

<span data-ttu-id="34758-256">**메모리**</span><span class="sxs-lookup"><span data-stu-id="34758-256">**Memory**</span></span>

- <span data-ttu-id="34758-257">.NET CLR Memory\\모든 힙 (w3wp)에서 바이트</span><span class="sxs-lookup"><span data-stu-id="34758-257">.NET CLR Memory\\# bytes in all Heaps (for w3wp)</span></span>

<span data-ttu-id="34758-258">**ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="34758-258">**ASP.NET**</span></span>

- <span data-ttu-id="34758-259">ASP.NET\Requests Current</span><span class="sxs-lookup"><span data-stu-id="34758-259">ASP.NET\Requests Current</span></span>
- <span data-ttu-id="34758-260">ASP.NET\Queued</span><span class="sxs-lookup"><span data-stu-id="34758-260">ASP.NET\Queued</span></span>
- <span data-ttu-id="34758-261">ASP.NET\Rejected</span><span class="sxs-lookup"><span data-stu-id="34758-261">ASP.NET\Rejected</span></span>

<span data-ttu-id="34758-262">**CPU**</span><span class="sxs-lookup"><span data-stu-id="34758-262">**CPU**</span></span>

- <span data-ttu-id="34758-263">프로세서 Information\Processor 시간</span><span class="sxs-lookup"><span data-stu-id="34758-263">Processor Information\Processor Time</span></span>

<span data-ttu-id="34758-264">**TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="34758-264">**TCP/IP**</span></span>

- <span data-ttu-id="34758-265">TCPv6/연결 설정</span><span class="sxs-lookup"><span data-stu-id="34758-265">TCPv6/Connections Established</span></span>
- <span data-ttu-id="34758-266">TCPv4/연결 설정</span><span class="sxs-lookup"><span data-stu-id="34758-266">TCPv4/Connections Established</span></span>

<span data-ttu-id="34758-267">**웹 서비스**</span><span class="sxs-lookup"><span data-stu-id="34758-267">**Web Service**</span></span>

- <span data-ttu-id="34758-268">웹 Connections</span><span class="sxs-lookup"><span data-stu-id="34758-268">Web Service\Current Connections</span></span>
- <span data-ttu-id="34758-269">웹 Service\Maximum 연결</span><span class="sxs-lookup"><span data-stu-id="34758-269">Web Service\Maximum Connections</span></span>

<span data-ttu-id="34758-270">**스레딩**</span><span class="sxs-lookup"><span data-stu-id="34758-270">**Threading**</span></span>

- <span data-ttu-id="34758-271">.NET CLR 잠금 및 스레드\\현재 논리 스레드</span><span class="sxs-lookup"><span data-stu-id="34758-271">.NET CLR Locks And Threads\\# of current logical Threads</span></span>
- <span data-ttu-id="34758-272">.NET CLR 잠금 및 스레드\\현재 실제 스레드</span><span class="sxs-lookup"><span data-stu-id="34758-272">.NET CLR Locks And Threads\\# of current physical Threads</span></span>

<a id="otherresources"></a>

## <a name="other-resources"></a><span data-ttu-id="34758-273">기타 리소스</span><span class="sxs-lookup"><span data-stu-id="34758-273">Other Resources</span></span>

<span data-ttu-id="34758-274">ASP.NET 성능 모니터링 및 튜닝에 대 한 자세한 내용은 다음 항목을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="34758-274">For more information on ASP.NET performance monitoring and tuning, see the following topics:</span></span>

- <span data-ttu-id="34758-275">[ASP.NET 성능 개요](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="34758-275">[ASP.NET Performance Overview](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span></span>
- [<span data-ttu-id="34758-276">IIS 7.5, IIS 7.0 및 IIS 6.0에서 ASP.NET 스레드 사용량</span><span class="sxs-lookup"><span data-stu-id="34758-276">ASP.NET Thread Usage on IIS 7.5, IIS 7.0, and IIS 6.0</span></span>](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [<span data-ttu-id="34758-277">&lt;applicationPool&gt; 요소 (웹 설정)</span><span class="sxs-lookup"><span data-stu-id="34758-277">&lt;applicationPool&gt; Element (Web Settings)</span></span>](https://msdn.microsoft.com/library/dd560842.aspx)
