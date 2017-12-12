---
uid: signalr/overview/performance/signalr-performance
title: "SignalR 성능 | Microsoft Docs"
author: pfletcher
description: "SignalR 성능"
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: 3751f5e7-59db-4be0-a290-50abc24e5c84
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/performance/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: dec2602e47fbcb838643a506a7e3feebda9d9c81
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="signalr-performance"></a><span data-ttu-id="a756f-103">SignalR 성능</span><span class="sxs-lookup"><span data-stu-id="a756f-103">SignalR Performance</span></span>
====================
<span data-ttu-id="a756f-104">으로 [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="a756f-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

> <span data-ttu-id="a756f-105">이 항목에 대 한 디자인 하 고 정확한 SignalR 응용 프로그램의 성능을 향상 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-105">This topic describes how to design for, measure, and improve performance in a SignalR application.</span></span>
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="a756f-106">이 항목에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="a756f-106">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="a756f-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="a756f-107">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="a756f-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="a756f-108">.NET 4.5</span></span>
> - <span data-ttu-id="a756f-109">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="a756f-109">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="a756f-110">이 항목의 이전 버전</span><span class="sxs-lookup"><span data-stu-id="a756f-110">Previous versions of this topic</span></span>
> 
> <span data-ttu-id="a756f-111">이전 버전의 SignalR에 대 한 정보를 참조 하십시오. [SignalR 이전 버전](../older-versions/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="a756f-112">질문이 나 의견이</span><span class="sxs-lookup"><span data-stu-id="a756f-112">Questions and comments</span></span>
> 
> <span data-ttu-id="a756f-113">이 자습서를 연결 하는 방법 및 페이지의 맨 아래에 주석에서 향상 될 수 있습니다 어떻게에 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="a756f-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="a756f-114">자습서를 직접 관련 되지 않는 질문 해야 하도록를 게시할 수 있습니다는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


<span data-ttu-id="a756f-115">SignalR 성능 및 확장성에 최근 프레젠테이션용 참조 [SignalR로 실시간 웹 크기 조정](https://channel9.msdn.com/Events/Build/2013/3-502)합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-115">For a recent presentation on SignalR performance and scaling, see [Scaling the Real-time Web with ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span></span>

<span data-ttu-id="a756f-116">이 항목에는 다음과 같은 단원이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="a756f-117">디자인 고려 사항</span><span class="sxs-lookup"><span data-stu-id="a756f-117">Design considerations</span></span>](#design)
- [<span data-ttu-id="a756f-118">SignalR 서버 성능을 튜닝</span><span class="sxs-lookup"><span data-stu-id="a756f-118">Tuning your SignalR server for performance</span></span>](#tuning)
- [<span data-ttu-id="a756f-119">성능 문제 해결</span><span class="sxs-lookup"><span data-stu-id="a756f-119">Troubleshooting performance issues</span></span>](#troubleshooting)
- [<span data-ttu-id="a756f-120">SignalR 성능 카운터를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="a756f-120">Using SignalR performance counters</span></span>](#perfcounters)
- [<span data-ttu-id="a756f-121">다른 성능 카운터를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="a756f-121">Using other performance counters</span></span>](#othercounters)
- [<span data-ttu-id="a756f-122">기타 리소스</span><span class="sxs-lookup"><span data-stu-id="a756f-122">Other resources</span></span>](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a><span data-ttu-id="a756f-123">디자인 고려 사항</span><span class="sxs-lookup"><span data-stu-id="a756f-123">Design considerations</span></span>

<span data-ttu-id="a756f-124">이 섹션에 성능 불필요 한 네트워크 트래픽이 생성 하 여 저하 되 고 있지은 되도록 SignalR 응용 프로그램을 디자인 하는 동안 구현할 수 있는 패턴에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-124">This section describes patterns that can be implemented during the design of a SignalR application, to ensure that performance is not being hindered by generating unnecessary network traffic.</span></span>

### <a name="throttling-message-frequency"></a><span data-ttu-id="a756f-125">메시지 빈도 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-125">Throttling message frequency</span></span>

<span data-ttu-id="a756f-126">높은 주파수 (예: 실시간 게임 응용 프로그램)에서 메시지를 전송 하는 응용 프로그램에도 대부분의 응용 프로그램을 두 번째로 많은 메시지를 보낼 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-126">Even in an application that sends out messages at a high frequency (such as a realtime gaming application), most applications don't need to send more than a few messages a second.</span></span> <span data-ttu-id="a756f-127">각 클라이언트에서 생성 되는 트래픽 용량을 줄이기 위해 메시지 루프를 구현할 수 있습니다 큐 및 보냅니다. 고정된 속도 보다 자주 더 이상 메시지가 있는지 (즉, 특정 메시지의 수로 전송 되지 않음 1 초 마다 해당 시간에 메시지가 있을 경우 전송 terval)입니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-127">To reduce the amount of traffic that each client generates, a message loop can be implemented that queues and sends out messages no more frequently than a fixed rate (that is, up to a certain number of messages will be sent every second, if there are messages in that time interval to be sent).</span></span> <span data-ttu-id="a756f-128">(클라이언트 및 서버)에서 특정 속도로 메시지를 제한 하는 샘플 응용 프로그램에 대 한 참조 [SignalR과 높은 주파수 실시간](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-128">For a sample application that throttles messages to a certain rate (from both client and server), see [High-Frequency Realtime with SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span></span>

### <a name="reducing-message-size"></a><span data-ttu-id="a756f-129">메시지 크기 감소</span><span class="sxs-lookup"><span data-stu-id="a756f-129">Reducing message size</span></span>

<span data-ttu-id="a756f-130">Serialize 된 개체의 크기를 줄여 SignalR 메시지의 크기를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-130">You can reduce the size of a SignalR message by reducing the size of your serialized objects.</span></span> <span data-ttu-id="a756f-131">서버 코드에서 전송 될 필요가 없는 속성을 포함 하는 개체를 보내는 경우 되지 않도록 해당 속성에서 사용 하 여 serialize 되는 `JsonIgnore` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-131">In server code, if you're sending an object that contains properties that don't need to be transmitted, prevent those properties from being serialized by using the `JsonIgnore` attribute.</span></span> <span data-ttu-id="a756f-132">속성의 이름은 메시지;에 저장 속성의 이름을 사용 하 여 단축할 수는 `JsonProperty` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-132">The names of properties are also stored in the message; the names of properties can be shortened using the `JsonProperty` attribute.</span></span> <span data-ttu-id="a756f-133">다음 코드 샘플을 클라이언트로 보낼 속성을 제외 하는 방법과 속성 이름을 단축 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-133">The following code sample demonstrates how to exclude a property from being sent to the client, and how to shorten property names:</span></span>

<span data-ttu-id="a756f-134">**데이터를 제외 하도록 클라이언트에 전송 되지 JsonIgnore 특성 및 메시지 크기를 줄이는 JsonProperty 특성을 보여 주는.NET 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="a756f-134">**.NET server code that demonstrates the JsonIgnore attribute to exclude data from being sent to the client, and the JsonProperty attribute to reduce message size**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

<span data-ttu-id="a756f-135">가독성을 유지 하기 위해 클라이언트 코드에서 관리의 용이성, 약식된 속성 이름은 이름일 수도 있습니다 사람이 친화적인에 매핑이 변경 메시지를 받은 후 / 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-135">In order to retain readability/ maintainability in the client code, the abbreviated property names can be remapped to human-friendly names after the message is received.</span></span> <span data-ttu-id="a756f-136">다음 코드 예제에서는 메시지 계약 (매핑)을 정의 하 여 긴 프로토콜로 약식된 이름을 다시 매핑의 한 가지 방법을 사용 하 고는 `reMap` 계약 최적화 된 메시지 클래스에 적용할 함수:</span><span class="sxs-lookup"><span data-stu-id="a756f-136">The following code sample demonstrates one possible way of remapping shortened names to longer ones, by defining a message contract (mapping), and using the `reMap` function to apply the contract to the optimized message class:</span></span>

<span data-ttu-id="a756f-137">**다시 매핑하는 클라이언트 쪽 JavaScript 코드를 이해 하기 쉬운 이름 속성 이름 단축**</span><span class="sxs-lookup"><span data-stu-id="a756f-137">**Client-side JavaScript code that remaps shortened property names to human-readable names**</span></span>

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

<span data-ttu-id="a756f-138">이름은 동일한 방법을 사용 하 여도 서버에 클라이언트에서 메시지에 단축 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-138">Names can be shortened in messages from the client to the server as well, using the same method.</span></span>

<span data-ttu-id="a756f-139">(즉, 메시지에 사용 된 메모리의 양)에 메모리 사용 공간 감소 메시지의 개체도 성능을 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-139">Reducing the memory footprint (that is, the amount of memory used for the message) of the message object can also improve performance.</span></span> <span data-ttu-id="a756f-140">예를 들어 경우의 전체 범위는 `int` 필요 하지 않은 한 `short` 또는 `byte` 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-140">For example, if the full range of an `int` is not needed, a `short` or `byte` can be used instead.</span></span>

<span data-ttu-id="a756f-141">메시지는 메시지의 크기를 줄이면 서버 메모리의 메시지 버스에 저장 되므로 서버 메모리 문제를 해결 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-141">Since messages are stored in the message bus in server memory, reducing the size of messages can also address server memory issues.</span></span>

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a><span data-ttu-id="a756f-142">SignalR 서버 성능을 튜닝</span><span class="sxs-lookup"><span data-stu-id="a756f-142">Tuning your SignalR server for performance</span></span>

<span data-ttu-id="a756f-143">다음 구성 설정은 SignalR 응용 프로그램에서 성능 향상을 위해 서버 조정할 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-143">The following configuration settings can be used to tune your server for better performance in a SignalR application.</span></span> <span data-ttu-id="a756f-144">ASP.NET 응용 프로그램의 성능을 향상 하는 방법에 대 한 일반적인 정보를 참조 하십시오. [ASP.NET 성능 향상](https://msdn.microsoft.com/en-us/library/ff647787.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-144">For general information on how to improve performance in an ASP.NET application, see [Improving ASP.NET Performance](https://msdn.microsoft.com/en-us/library/ff647787.aspx).</span></span>

<span data-ttu-id="a756f-145">**SignalR 구성 설정**</span><span class="sxs-lookup"><span data-stu-id="a756f-145">**SignalR configuration settings**</span></span>

- <span data-ttu-id="a756f-146">**DefaultMessageBufferSize**: 기본적으로 SignalR 허브 연결당 당 메모리에서 1000 메시지를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-146">**DefaultMessageBufferSize**: By default, SignalR retains 1000 messages in memory per hub per connection.</span></span> <span data-ttu-id="a756f-147">큰 메시지를 사용 하는 경우 이렇게이 값을 감소 시켜 용량을 줄일 수 있는 메모리 문제를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-147">If large messages are being used, this may create memory issues which can be alleviated by reducing this value.</span></span> <span data-ttu-id="a756f-148">이 설정을 설정할 수는 `Application_Start` 또는 ASP.NET 응용 프로그램에서 이벤트 처리기는 `Configuration` 자체 호스팅된 응용 프로그램에는 OWIN 시작 클래스의 메서드.</span><span class="sxs-lookup"><span data-stu-id="a756f-148">This setting can be set in the `Application_Start` event handler in an ASP.NET application, or in the `Configuration` method of an OWIN startup class in a self-hosted application.</span></span> <span data-ttu-id="a756f-149">다음 샘플에 사용 되는 서버 메모리의 양을 줄이기 위해 응용 프로그램의 메모리 사용 공간을 최소화 하기 위해이 값을 줄이는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-149">The following sample demonstrates how to reduce this value in order to reduce the memory footprint of your application in order to reduce the amount of server memory used:</span></span>

    <span data-ttu-id="a756f-150">**기본 메시지 버퍼 크기를 줄이면에 대 한 Startup.cs에서.NET 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="a756f-150">**.NET server code in Startup.cs for decreasing default message buffer size**</span></span>

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

<span data-ttu-id="a756f-151">**IIS 구성 설정**</span><span class="sxs-lookup"><span data-stu-id="a756f-151">**IIS configuration settings**</span></span>

- <span data-ttu-id="a756f-152">**응용 프로그램 당 최대 동시 요청**: 동시 IIS의 수를 늘리면 요청 늘어납니다 서버 리소스의 요청 처리에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-152">**Max concurrent requests per application**: Increasing the number of concurrent IIS requests will increase server resources available for serving requests.</span></span> <span data-ttu-id="a756f-153">기본값은 5000입니다. 이 설정의 늘리려면 다음 명령을 관리자 권한 명령 프롬프트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-153">The default value is 5000; to increase this setting, execute the following commands in an elevated command prompt:</span></span>

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- <span data-ttu-id="a756f-154">**ApplicationPool QueueLength**: Http.sys 응용 프로그램 풀에 대 한 큐 대기 하는 요청의 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-154">**ApplicationPool QueueLength**: This is the maximum number of requests that Http.sys queues for the application pool.</span></span> <span data-ttu-id="a756f-155">큐가 가득 찬 경우 새 요청에서 503 "서비스를 사용할 수 없음" 응답을 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-155">When the queue is full, new requests receive a 503 "Service Unavailable" response.</span></span> <span data-ttu-id="a756f-156">기본값은 1000입니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-156">The default value is 1000.</span></span>

    <span data-ttu-id="a756f-157">응용 프로그램을 호스팅하는 응용 프로그램 풀에서 작업자 프로세스에 대 한 큐 길이 줄이는 메모리 리소스를 확보 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-157">Shortening the queue length for the worker process in the application pool hosting your application will conserve memory resources.</span></span> <span data-ttu-id="a756f-158">자세한 내용은 참조 [관리, 조정, 및 응용 프로그램 풀 구성](https://technet.microsoft.com/en-us/library/cc745955.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-158">For more information, see [Managing, Tuning, and Configuring Application Pools](https://technet.microsoft.com/en-us/library/cc745955.aspx).</span></span>

<span data-ttu-id="a756f-159">**ASP.NET 구성 설정**</span><span class="sxs-lookup"><span data-stu-id="a756f-159">**ASP.NET configuration settings**</span></span>

<span data-ttu-id="a756f-160">이 섹션에서 설정할 수 있는 구성 설정에는 `aspnet.config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-160">This section includes configuration settings that can be set in the `aspnet.config` file.</span></span> <span data-ttu-id="a756f-161">이 파일은 플랫폼에 따라 다음 두 위치 중 하나에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-161">This file is found in one of two locations, depending on platform:</span></span>

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

<span data-ttu-id="a756f-162">SignalR 성능이 향상 될 수 있는 ASP.NET 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-162">ASP.NET settings that may improve SignalR performance include the following:</span></span>

- <span data-ttu-id="a756f-163">**CPU 당 최대 동시 요청**:이 설정을 성능 병목 현상을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-163">**Maximum concurrent requests per CPU**: Increasing this setting may alleviate performance bottlenecks.</span></span> <span data-ttu-id="a756f-164">이 설정을 늘릴,에 다음 구성 설정을 추가 `aspnet.config` 파일:</span><span class="sxs-lookup"><span data-stu-id="a756f-164">To increase this setting, add the following configuration setting to the `aspnet.config` file:</span></span>

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- <span data-ttu-id="a756f-165">**요청 큐 제한**: 총 연결 수 초과 하는 경우는 `maxConcurrentRequestsPerCPU` 설정, ASP.NET 요청 큐를 사용 하 여 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-165">**Request Queue Limit**: When the total number of connections exceeds the `maxConcurrentRequestsPerCPU` setting, ASP.NET will start throttling requests using a queue.</span></span> <span data-ttu-id="a756f-166">큐의 크기를 늘리려면 늘릴 수 있습니다는 `requestQueueLimit` 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-166">To increase the size of the queue, you can increase the `requestQueueLimit` setting.</span></span> <span data-ttu-id="a756f-167">이 수행 하려면에 다음 구성 설정을 추가 `processModel` 노드에서 `config/machine.config` (대신 `aspnet.config`):</span><span class="sxs-lookup"><span data-stu-id="a756f-167">To do this, add the following configuration setting to the `processModel` node in `config/machine.config` (rather than `aspnet.config`):</span></span>

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a><span data-ttu-id="a756f-168">성능 문제 해결</span><span class="sxs-lookup"><span data-stu-id="a756f-168">Troubleshooting performance issues</span></span>

<span data-ttu-id="a756f-169">이 섹션에서는 응용 프로그램에서 성능 병목 상태를 발견 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-169">This section describes ways to find performance bottlenecks in your application.</span></span>

### <a name="verifying-that-websocket-is-being-used"></a><span data-ttu-id="a756f-170">WebSocket이 사용 되 고 있는지 확인 하는 중</span><span class="sxs-lookup"><span data-stu-id="a756f-170">Verifying that WebSocket is being used</span></span>

<span data-ttu-id="a756f-171">SignalR를 사용할 수 있지만 다양 한 전송 방식 클라이언트와 서버 간의 통신에 대 한 WebSocket 뛰어난 성공을 제공 하 고 클라이언트와 서버에서 지 원하는 경우 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-171">While SignalR can use a variety of transports for communication between client and server, WebSocket offers a significant performance advantage, and should be used if the client and server support it.</span></span> <span data-ttu-id="a756f-172">클라이언트와 서버 WebSocket에 대 한 요구 사항을 충족 하는 경우를 확인 하려면 참조 [전송 및 대체](../getting-started/introduction-to-signalr.md#transports)합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-172">To determine if your client and server meet the requirements for WebSocket, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="a756f-173">어떤 전송을 응용 프로그램에서 사용량을 확인 하려면 브라우저 개발자 도구를 사용할 수 있으며 어떤 전송을 연결에 사용 되는지 확인 하려면 로그를 검사 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-173">To determine what transport is being used in your application, you can use the browser developer tools, and examine the logs to see what transport is being used for the connection.</span></span> <span data-ttu-id="a756f-174">Internet Explorer 및 Chrome 브라우저 개발 도구를 사용 하는 방법은 참조 하십시오. [전송 및 대체](../getting-started/introduction-to-signalr.md#transports)합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-174">For information on using the browser development tools in Internet Explorer and Chrome, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a><span data-ttu-id="a756f-175">SignalR 성능 카운터를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="a756f-175">Using SignalR performance counters</span></span>

<span data-ttu-id="a756f-176">이 섹션에서는 SignalR 성능 카운터를 사용 하는 방법 설명에 `Microsoft.AspNet.SignalR.Utils` 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-176">This section describes how to enable and use SignalR performance counters, found in the `Microsoft.AspNet.SignalR.Utils` package.</span></span>

### <a name="installing-signalrexe"></a><span data-ttu-id="a756f-177">Signalr.exe 설치</span><span class="sxs-lookup"><span data-stu-id="a756f-177">Installing signalr.exe</span></span>

<span data-ttu-id="a756f-178">성능 카운터 SignalR.exe 라는 유틸리티를 사용 하 여 서버에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-178">Performance counters can be added to the server using a utility called SignalR.exe.</span></span> <span data-ttu-id="a756f-179">이 유틸리티를 설치 하려면 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-179">To install this utility, follow these steps:</span></span>

1. <span data-ttu-id="a756f-180">Visual Studio 응용 프로그램에서 선택 **도구**, **라이브러리 패키지 관리자**, **솔루션에 대 한 NuGet 패키지 관리...**</span><span class="sxs-lookup"><span data-stu-id="a756f-180">In your Visual Studio application, select **Tools**, **Library Package Manager**, **Manage NuGet Packages for Solution...**</span></span>
2. <span data-ttu-id="a756f-181">검색할 **signalr.utils**, 설치를 선택 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-181">Search for **signalr.utils**, and select Install.</span></span>

    ![](signalr-performance/_static/image1.png)
3. <span data-ttu-id="a756f-182">패키지를 설치 하려면 사용권 계약에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-182">Accept the license agreement to install the package.</span></span>
4. <span data-ttu-id="a756f-183">SignalR.exe 되도록 설치 됩니다. `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-183">SignalR.exe will be installed to `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span></span>

### <a name="installing-performance-counters-with-signalrexe"></a><span data-ttu-id="a756f-184">SignalR.exe와 성능 카운터를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-184">Installing performance counters with SignalR.exe</span></span>

<span data-ttu-id="a756f-185">SignalR 성능 카운터를 설치 하려면 다음 매개 변수를 사용 하는 관리자 권한 명령 프롬프트에서 SignalR.exe를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-185">To install SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

<span data-ttu-id="a756f-186">SignalR 성능 카운터를 제거 하려면 다음 매개 변수를 사용 하는 관리자 권한 명령 프롬프트에서 SignalR.exe를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-186">To remove SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a><span data-ttu-id="a756f-187">SignalR 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="a756f-187">SignalR Performance counters</span></span>

<span data-ttu-id="a756f-188">유틸리티가 패키지는 다음 성능 카운터를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-188">The utilities package installs the following performance counters.</span></span> <span data-ttu-id="a756f-189">"Total" 카운터는 마지막 응용 프로그램 풀 또는 서버를 다시 시작한 이후 이벤트의 수를 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-189">The "Total" counters measure the number of events since the last application pool or server restart.</span></span>

<span data-ttu-id="a756f-190">**연결 메트릭**</span><span class="sxs-lookup"><span data-stu-id="a756f-190">**Connection metrics**</span></span>

<span data-ttu-id="a756f-191">다음과 같은 메트릭이 발생 하는 연결 수명 이벤트를 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-191">The following metrics measure the connection lifetime events that occur.</span></span> <span data-ttu-id="a756f-192">자세한 내용은 참조 [이해 하 고 연결 수명 이벤트를 처리](../guide-to-the-api/handling-connection-lifetime-events.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-192">For more information, see [Understanding and Handling Connection Lifetime Events](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

- <span data-ttu-id="a756f-193">**연결 된 연결**</span><span class="sxs-lookup"><span data-stu-id="a756f-193">**Connections Connected**</span></span>
- <span data-ttu-id="a756f-194">**다시 연결 하는 연결**</span><span class="sxs-lookup"><span data-stu-id="a756f-194">**Connections Reconnected**</span></span>
- <span data-ttu-id="a756f-195">**연결이 끊긴 연결**</span><span class="sxs-lookup"><span data-stu-id="a756f-195">**Connections Disconnected**</span></span>
- <span data-ttu-id="a756f-196">**현재 연결**</span><span class="sxs-lookup"><span data-stu-id="a756f-196">**Connections Current**</span></span>

<span data-ttu-id="a756f-197">**메시지 메트릭스**</span><span class="sxs-lookup"><span data-stu-id="a756f-197">**Message metrics**</span></span>

<span data-ttu-id="a756f-198">다음과 같은 메트릭이 SignalR에 의해 생성 된 메시지 트래픽을 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-198">The following metrics measure the message traffic generated by SignalR.</span></span>

- <span data-ttu-id="a756f-199">**총 받은 연결 메시지**</span><span class="sxs-lookup"><span data-stu-id="a756f-199">**Connection Messages Received Total**</span></span>
- <span data-ttu-id="a756f-200">**총 보낸 연결 메시지**</span><span class="sxs-lookup"><span data-stu-id="a756f-200">**Connection Messages Sent Total**</span></span>
- <span data-ttu-id="a756f-201">**연결에 수신 메시지/초**</span><span class="sxs-lookup"><span data-stu-id="a756f-201">**Connection Messages Received/Sec**</span></span>
- <span data-ttu-id="a756f-202">**전송 연결 Messages/Sec**</span><span class="sxs-lookup"><span data-stu-id="a756f-202">**Connection Messages Sent/Sec**</span></span>

<span data-ttu-id="a756f-203">**메시지 버스 메트릭**</span><span class="sxs-lookup"><span data-stu-id="a756f-203">**Message bus metrics**</span></span>

<span data-ttu-id="a756f-204">다음 메트릭을 모든 들어오는 / 나가는 SignalR 메시지 사항이 큐는 내부 SignalR 메시지 버스를 통해 트래픽을 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-204">The following metrics measure traffic through the internal SignalR message bus, the queue in which all incoming and outgoing SignalR messages are placed.</span></span> <span data-ttu-id="a756f-205">메시지는 **게시 됨** 전송 되거나 브로드캐스트 때.</span><span class="sxs-lookup"><span data-stu-id="a756f-205">A message is **Published** when it is sent or broadcast.</span></span> <span data-ttu-id="a756f-206">A **구독자** 이 컨텍스트에서 메시지 버스에서 구독;이 클라이언트와 서버 자체의 수와 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-206">A **Subscriber** in this context is a subscription on the message bus; this should equal the number of clients plus the server itself.</span></span> <span data-ttu-id="a756f-207">**할당 된 작업자** 활성 연결;에 데이터를 전송 하는 구성 요소는 **사용 중인 작업자** 는 보내는 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-207">An **Allocated Worker** is a component that sends data to active connections; a **Busy Worker** is one that is actively sending a message.</span></span>

- <span data-ttu-id="a756f-208">**메시지 버스 받은 총 메시지**</span><span class="sxs-lookup"><span data-stu-id="a756f-208">**Message Bus Messages Received Total**</span></span>
- <span data-ttu-id="a756f-209">**메시지 버스 메시지 Received/Sec**</span><span class="sxs-lookup"><span data-stu-id="a756f-209">**Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="a756f-210">**메시지 버스 메시지 게시 합계**</span><span class="sxs-lookup"><span data-stu-id="a756f-210">**Message Bus Messages Published Total**</span></span>
- <span data-ttu-id="a756f-211">**메시지 버스 Messages 게시/Sec**</span><span class="sxs-lookup"><span data-stu-id="a756f-211">**Message Bus Messages Published/Sec**</span></span>
- <span data-ttu-id="a756f-212">**메시지 버스 구독자 현재**</span><span class="sxs-lookup"><span data-stu-id="a756f-212">**Message Bus Subscribers Current**</span></span>
- <span data-ttu-id="a756f-213">**메시지 버스 구독자 합계**</span><span class="sxs-lookup"><span data-stu-id="a756f-213">**Message Bus Subscribers Total**</span></span>
- <span data-ttu-id="a756f-214">**메시지 버스 구독자/Sec**</span><span class="sxs-lookup"><span data-stu-id="a756f-214">**Message Bus Subscribers/Sec**</span></span>
- <span data-ttu-id="a756f-215">**메시지 버스 작업자를 할당 합니다.**</span><span class="sxs-lookup"><span data-stu-id="a756f-215">**Message Bus Allocated Workers**</span></span>
- <span data-ttu-id="a756f-216">**메시지 버스 근무 중인 노동자**</span><span class="sxs-lookup"><span data-stu-id="a756f-216">**Message Bus Busy Workers**</span></span>
- <span data-ttu-id="a756f-217">**메시지 버스 항목 현재**</span><span class="sxs-lookup"><span data-stu-id="a756f-217">**Message Bus Topics Current**</span></span>

<span data-ttu-id="a756f-218">**오차 메트릭**</span><span class="sxs-lookup"><span data-stu-id="a756f-218">**Error metrics**</span></span>

<span data-ttu-id="a756f-219">SignalR 메시지 트래픽에 의해 생성 된 오류를 측정 하는 다음 메트릭을 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-219">The following metrics measure errors generated by SignalR message traffic.</span></span> <span data-ttu-id="a756f-220">**허브 해상도** 허브 또는 허브 메서드를 확인할 수 없는 경우 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-220">**Hub Resolution** errors occur when a hub or hub method cannot be resolved.</span></span> <span data-ttu-id="a756f-221">**허브 호출** 오류는 허브 메서드를 호출 하는 동안 발생 한 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-221">**Hub Invocation** errors are exceptions thrown while invoking a hub method.</span></span> <span data-ttu-id="a756f-222">**전송** 오류는 연결 오류는 HTTP 요청 또는 응답 하는 동안 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-222">**Transport** errors are connection errors thrown during an HTTP request or response.</span></span>

- <span data-ttu-id="a756f-223">**모든 총 오류 수:**</span><span class="sxs-lookup"><span data-stu-id="a756f-223">**Errors: All Total**</span></span>
- <span data-ttu-id="a756f-224">**오류: All/Sec**</span><span class="sxs-lookup"><span data-stu-id="a756f-224">**Errors: All/Sec**</span></span>
- <span data-ttu-id="a756f-225">**허브 해상도 총 오류 수:**</span><span class="sxs-lookup"><span data-stu-id="a756f-225">**Errors: Hub Resolution Total**</span></span>
- <span data-ttu-id="a756f-226">**오류: 허브 해상도/초**</span><span class="sxs-lookup"><span data-stu-id="a756f-226">**Errors: Hub Resolution/Sec**</span></span>
- <span data-ttu-id="a756f-227">**허브 호출 총 오류 수:**</span><span class="sxs-lookup"><span data-stu-id="a756f-227">**Errors: Hub Invocation Total**</span></span>
- <span data-ttu-id="a756f-228">**오류: 허브 호출 수/초**</span><span class="sxs-lookup"><span data-stu-id="a756f-228">**Errors: Hub Invocation/Sec**</span></span>
- <span data-ttu-id="a756f-229">**전송 총 오류 수:**</span><span class="sxs-lookup"><span data-stu-id="a756f-229">**Errors: Transport Total**</span></span>
- <span data-ttu-id="a756f-230">**오류: 전송 수/초**</span><span class="sxs-lookup"><span data-stu-id="a756f-230">**Errors: Transport/Sec**</span></span>

<a id="scaleout_metrics"></a>

<span data-ttu-id="a756f-231">**확장 메트릭**</span><span class="sxs-lookup"><span data-stu-id="a756f-231">**Scaleout metrics**</span></span>

<span data-ttu-id="a756f-232">다음 메트릭을 트래픽과 확장 공급자에서 발생 한 오류를 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-232">The following metrics measure traffic and errors generated by the scaleout provider.</span></span> <span data-ttu-id="a756f-233">A **스트림** 이 컨텍스트에서이 확장 공급자에서 사용 하는 배율 단위에는이 SQL Server가 사용 하는 경우 테이블, 서비스 버스를 사용 하는 경우 항목 및 구독을 Redis 사용 되는 경우.</span><span class="sxs-lookup"><span data-stu-id="a756f-233">A **Stream** in this context is a scale unit used by the scaleout provider; this is a table if SQL Server is used, a Topic if Service Bus is used, and a Subscription if Redis is used.</span></span> <span data-ttu-id="a756f-234">각 스트림에 순서가 지정 된 읽기 및 쓰기 작업을 사용 하면 단일 스트림을 병목 상태가 발생할 수 배율, 되므로 해당 병목 현상을 줄일 수 있도록 스트림 수를 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-234">Each stream ensures ordered read and write operations; a single stream is a potential scale bottleneck, so the number of streams can be increased to help reduce that bottleneck.</span></span> <span data-ttu-id="a756f-235">여러 개의 스트림을 사용 되는 경우 SignalR 이러한 스트림에 지정된 된 연결에서 보낸 메시지 순서는 보장 하는 방식에서 (분할) 메시지를 자동으로 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-235">If multiple streams are used, SignalR will automatically distribute (shard) messages across these streams in a way that ensures messages sent from any given connection are in order.</span></span>

<span data-ttu-id="a756f-236">[MaxQueueLength](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) 설정은 SignalR에서 유지 관리 하는 확장 송신 큐의 길이 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-236">The [MaxQueueLength](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) setting controls the length of the scaleout send queue maintained by SignalR.</span></span> <span data-ttu-id="a756f-237">이 값 보다 큰로 설정 0 모든 메시지를 한 번에 하나씩에 보내도록 구성 된 메시징 백플레인으로 송신 큐에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-237">Setting it to a value greater than 0 will place all messages in a send queue to be sent one at a time to the configured messaging backplane.</span></span> <span data-ttu-id="a756f-238">큐 크기가 구성된 된 길이 넘으면, 이후에 보내기를 호출 즉시와 함께 실패 한 [InvalidOperationException](https://msdn.microsoft.com/en-us/library/system.invalidoperationexception(v=vs.118).aspx) 큐의 메시지 수가 설정 보다 작으면 될 때까지 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-238">If the size of the queue goes above the configured length, subsequent calls to send will fail immediately with an [InvalidOperationException](https://msdn.microsoft.com/en-us/library/system.invalidoperationexception(v=vs.118).aspx) until the number of messages in the queue is less than the setting again.</span></span> <span data-ttu-id="a756f-239">큐 나 때문에 구현 된 백플레인 일반적으로 자신의 큐 흐름 제어 위치에 기본적으로 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-239">Queueing is disabled by default because the implemented backplanes generally have their own queuing or flow-control in place.</span></span> <span data-ttu-id="a756f-240">SQL Server의 경우 한 번에 진행 하는 송신의 수를 제한 효과적으로 연결 풀링이 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-240">In the case of SQL Server, connection pooling effectively limits the number of sends going on at any one time.</span></span>

<span data-ttu-id="a756f-241">기본적으로 스트림을 하나만 SQL Server 및 Redis에 대 한 사용, 서비스 버스 5 개의 스트림을 사용 및 queueing 사용 하지 않으면 되지만 SQL 서버와 서비스 버스에서 구성을 통해 이러한 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-241">By default, only one stream is used for SQL Server and Redis, five streams are used for Service Bus, and queueing is disabled, but these settings can be changed through configuration on SQL Server and Service Bus:</span></span>

<span data-ttu-id="a756f-242">**SQL Server 백플레인에 대 한 테이블 수 및 큐 길이 구성 하기 위한.NET 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="a756f-242">**.NET Server Code for configuring table count and queue length for SQL Server backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

<span data-ttu-id="a756f-243">**서비스 버스 백플레인에 대 한 항목 수 및 큐 길이 구성 하기 위한.NET 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="a756f-243">**.NET Server Code for configuring topic count and queue length for Service Bus backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

<span data-ttu-id="a756f-244">A **버퍼링** 스트림이 faulted 상태로 전환; 스트림이 faulted 상태가 즉시 스트림에 오류가 더 이상 될 때까지 백플레인에 보낸 모든 메시지가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-244">A **Buffering** stream is one that has entered a faulted state; when the stream is in the faulted state, all messages sent to the backplane will fail immediately until the stream is no longer faulting.</span></span> <span data-ttu-id="a756f-245">**전송 큐 길이** 게시 되었지만 아직 보내지 않은 메시지 수입니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-245">The **Send Queue Length** is the number of messages that have been posted but not yet sent.</span></span>

- <span data-ttu-id="a756f-246">**확장 메시지 버스 메시지 Received/Sec**</span><span class="sxs-lookup"><span data-stu-id="a756f-246">**Scaleout Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="a756f-247">**확장 스트림 합계**</span><span class="sxs-lookup"><span data-stu-id="a756f-247">**Scaleout Streams Total**</span></span>
- <span data-ttu-id="a756f-248">**확장 스트림 열기**</span><span class="sxs-lookup"><span data-stu-id="a756f-248">**Scaleout Streams Open**</span></span>
- <span data-ttu-id="a756f-249">**확장 스트림 버퍼링**</span><span class="sxs-lookup"><span data-stu-id="a756f-249">**Scaleout Streams Buffering**</span></span>
- <span data-ttu-id="a756f-250">**확장 오류 합계**</span><span class="sxs-lookup"><span data-stu-id="a756f-250">**Scaleout Errors Total**</span></span>
- <span data-ttu-id="a756f-251">**초당 확장 오류**</span><span class="sxs-lookup"><span data-stu-id="a756f-251">**Scaleout Errors/Sec**</span></span>
- <span data-ttu-id="a756f-252">**확장 송신 큐 길이**</span><span class="sxs-lookup"><span data-stu-id="a756f-252">**Scaleout Send Queue Length**</span></span>

<span data-ttu-id="a756f-253">이러한 카운터를 측정 하는 기능에 대 한 자세한 내용은 참조 하십시오. [Azure 서비스 버스에 SignalR 확장](scaleout-with-windows-azure-service-bus.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-253">For more information on what these counters are measuring, see [SignalR Scaleout with Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span></span>

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a><span data-ttu-id="a756f-254">다른 성능 카운터를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="a756f-254">Using other performance counters</span></span>

<span data-ttu-id="a756f-255">다음 성능 카운터는 응용 프로그램의 성능 모니터링에 유용한 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-255">The following performance counters may also be useful in monitoring your application's performance.</span></span>

<span data-ttu-id="a756f-256">**메모리**</span><span class="sxs-lookup"><span data-stu-id="a756f-256">**Memory**</span></span>

- <span data-ttu-id="a756f-257">.NET CLR 메모리\\전체 힙 (w3wp)에서 바이트 수</span><span class="sxs-lookup"><span data-stu-id="a756f-257">.NET CLR Memory\\# bytes in all Heaps (for w3wp)</span></span>

<span data-ttu-id="a756f-258">**ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="a756f-258">**ASP.NET**</span></span>

- <span data-ttu-id="a756f-259">Asp. net\requests Current</span><span class="sxs-lookup"><span data-stu-id="a756f-259">ASP.NET\Requests Current</span></span>
- <span data-ttu-id="a756f-260">ASP.NET\Queued</span><span class="sxs-lookup"><span data-stu-id="a756f-260">ASP.NET\Queued</span></span>
- <span data-ttu-id="a756f-261">ASP.NET\Rejected</span><span class="sxs-lookup"><span data-stu-id="a756f-261">ASP.NET\Rejected</span></span>

<span data-ttu-id="a756f-262">**CPU**</span><span class="sxs-lookup"><span data-stu-id="a756f-262">**CPU**</span></span>

- <span data-ttu-id="a756f-263">프로세서 Information\Processor 시간</span><span class="sxs-lookup"><span data-stu-id="a756f-263">Processor Information\Processor Time</span></span>

<span data-ttu-id="a756f-264">**TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="a756f-264">**TCP/IP**</span></span>

- <span data-ttu-id="a756f-265">설정 된 TCPv6/연결</span><span class="sxs-lookup"><span data-stu-id="a756f-265">TCPv6/Connections Established</span></span>
- <span data-ttu-id="a756f-266">설정 된 TCPv4/연결</span><span class="sxs-lookup"><span data-stu-id="a756f-266">TCPv4/Connections Established</span></span>

<span data-ttu-id="a756f-267">**웹 서비스**</span><span class="sxs-lookup"><span data-stu-id="a756f-267">**Web Service**</span></span>

- <span data-ttu-id="a756f-268">웹 Connections</span><span class="sxs-lookup"><span data-stu-id="a756f-268">Web Service\Current Connections</span></span>
- <span data-ttu-id="a756f-269">웹 Service\Maximum 연결</span><span class="sxs-lookup"><span data-stu-id="a756f-269">Web Service\Maximum Connections</span></span>

<span data-ttu-id="a756f-270">**스레딩**</span><span class="sxs-lookup"><span data-stu-id="a756f-270">**Threading**</span></span>

- <span data-ttu-id="a756f-271">.NET CLR 잠금 및 스레드\\현재 논리 스레드</span><span class="sxs-lookup"><span data-stu-id="a756f-271">.NET CLR Locks And Threads\\# of current logical Threads</span></span>
- <span data-ttu-id="a756f-272">.NET CLR 잠금 및 스레드\\현재 실제 스레드</span><span class="sxs-lookup"><span data-stu-id="a756f-272">.NET CLR Locks And Threads\\# of current physical Threads</span></span>

<a id="otherresources"></a>

## <a name="other-resources"></a><span data-ttu-id="a756f-273">기타 리소스</span><span class="sxs-lookup"><span data-stu-id="a756f-273">Other Resources</span></span>

<span data-ttu-id="a756f-274">ASP.NET 성능 모니터링 및 튜닝에 대 한 자세한 내용은 다음 항목을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="a756f-274">For more information on ASP.NET performance monitoring and tuning, see the following topics:</span></span>

- <span data-ttu-id="a756f-275">[ASP.NET 성능 개요](https://msdn.microsoft.com/en-us/library/cc668225(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="a756f-275">[ASP.NET Performance Overview](https://msdn.microsoft.com/en-us/library/cc668225(v=vs.100).aspx)</span></span>
- [<span data-ttu-id="a756f-276">IIS 7.5, IIS 7.0 및 IIS 6.0에 ASP.NET 스레드 사용</span><span class="sxs-lookup"><span data-stu-id="a756f-276">ASP.NET Thread Usage on IIS 7.5, IIS 7.0, and IIS 6.0</span></span>](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [<span data-ttu-id="a756f-277">&lt;applicationPool&gt; 요소 (웹 설정)</span><span class="sxs-lookup"><span data-stu-id="a756f-277">&lt;applicationPool&gt; Element (Web Settings)</span></span>](https://msdn.microsoft.com/en-us/library/dd560842.aspx)
