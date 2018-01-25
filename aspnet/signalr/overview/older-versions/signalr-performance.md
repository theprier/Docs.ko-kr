---
uid: signalr/overview/older-versions/signalr-performance
title: "SignalR 성능 (SignalR 1.x) | Microsoft Docs"
author: pfletcher
description: "SignalR 성능"
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/03/2013
ms.topic: article
ms.assetid: 9594d644-66b6-4223-acdd-23e29a6e4c46
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/older-versions/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: bad742af28d6c36bb1b66207c2ba09d140332449
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="signalr-performance-signalr-1x"></a><span data-ttu-id="e1866-103">SignalR 성능 (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="e1866-103">SignalR Performance (SignalR 1.x)</span></span>
====================
<span data-ttu-id="e1866-104">으로 [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="e1866-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

> <span data-ttu-id="e1866-105">이 항목에 대 한 디자인 하 고 정확한 SignalR 응용 프로그램의 성능을 향상 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-105">This topic describes how to design for, measure, and improve performance in a SignalR application.</span></span>


<span data-ttu-id="e1866-106">SignalR 성능 및 확장성에 최근 프레젠테이션용 참조 [SignalR로 실시간 웹 크기 조정](https://channel9.msdn.com/Events/Build/2013/3-502)합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-106">For a recent presentation on SignalR performance and scaling, see [Scaling the Real-time Web with ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span></span>

<span data-ttu-id="e1866-107">이 항목에는 다음과 같은 단원이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-107">This topic contains the following sections:</span></span>

- [<span data-ttu-id="e1866-108">디자인 고려 사항</span><span class="sxs-lookup"><span data-stu-id="e1866-108">Design considerations</span></span>](#design)
- [<span data-ttu-id="e1866-109">SignalR 서버 성능을 튜닝</span><span class="sxs-lookup"><span data-stu-id="e1866-109">Tuning your SignalR server for performance</span></span>](#tuning)
- [<span data-ttu-id="e1866-110">성능 문제 해결</span><span class="sxs-lookup"><span data-stu-id="e1866-110">Troubleshooting performance issues</span></span>](#troubleshooting)
- [<span data-ttu-id="e1866-111">SignalR 성능 카운터를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e1866-111">Using SignalR performance counters</span></span>](#perfcounters)
- [<span data-ttu-id="e1866-112">다른 성능 카운터를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e1866-112">Using other performance counters</span></span>](#othercounters)
- [<span data-ttu-id="e1866-113">기타 리소스</span><span class="sxs-lookup"><span data-stu-id="e1866-113">Other resources</span></span>](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a><span data-ttu-id="e1866-114">디자인 고려 사항</span><span class="sxs-lookup"><span data-stu-id="e1866-114">Design considerations</span></span>

<span data-ttu-id="e1866-115">이 섹션에 성능 불필요 한 네트워크 트래픽이 생성 하 여 저하 되 고 있지은 되도록 SignalR 응용 프로그램을 디자인 하는 동안 구현할 수 있는 패턴에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-115">This section describes patterns that can be implemented during the design of a SignalR application, to ensure that performance is not being hindered by generating unnecessary network traffic.</span></span>

### <a name="throttling-message-frequency"></a><span data-ttu-id="e1866-116">메시지 빈도 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-116">Throttling message frequency</span></span>

<span data-ttu-id="e1866-117">높은 주파수 (예: 실시간 게임 응용 프로그램)에서 메시지를 전송 하는 응용 프로그램에도 대부분의 응용 프로그램을 두 번째로 많은 메시지를 보낼 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-117">Even in an application that sends out messages at a high frequency (such as a realtime gaming application), most applications don't need to send more than a few messages a second.</span></span> <span data-ttu-id="e1866-118">각 클라이언트에서 생성 되는 트래픽 용량을 줄이기 위해 메시지 루프를 구현할 수 있습니다 큐 및 보냅니다. 고정된 속도 보다 자주 더 이상 메시지가 있는지 (즉, 특정 메시지의 수로 전송 되지 않음 1 초 마다 해당 시간에 메시지가 있을 경우 전송 terval)입니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-118">To reduce the amount of traffic that each client generates, a message loop can be implemented that queues and sends out messages no more frequently than a fixed rate (that is, up to a certain number of messages will be sent every second, if there are messages in that time interval to be sent).</span></span> <span data-ttu-id="e1866-119">(클라이언트 및 서버)에서 특정 속도로 메시지를 제한 하는 샘플 응용 프로그램에 대 한 참조 [SignalR과 높은 주파수 실시간](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-119">For a sample application that throttles messages to a certain rate (from both client and server), see [High-Frequency Realtime with SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span></span>

### <a name="reducing-message-size"></a><span data-ttu-id="e1866-120">메시지 크기 감소</span><span class="sxs-lookup"><span data-stu-id="e1866-120">Reducing message size</span></span>

<span data-ttu-id="e1866-121">Serialize 된 개체의 크기를 줄여 SignalR 메시지의 크기를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-121">You can reduce the size of a SignalR message by reducing the size of your serialized objects.</span></span> <span data-ttu-id="e1866-122">서버 코드에서 전송 될 필요가 없는 속성을 포함 하는 개체를 보내는 경우 되지 않도록 해당 속성에서 사용 하 여 serialize 되는 `JsonIgnore` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-122">In server code, if you're sending an object that contains properties that don't need to be transmitted, prevent those properties from being serialized by using the `JsonIgnore` attribute.</span></span> <span data-ttu-id="e1866-123">속성의 이름은 메시지;에 저장 속성의 이름을 사용 하 여 단축할 수는 `JsonProperty` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-123">The names of properties are also stored in the message; the names of properties can be shortened using the `JsonProperty` attribute.</span></span> <span data-ttu-id="e1866-124">다음 코드 샘플을 클라이언트로 보낼 속성을 제외 하는 방법과 속성 이름을 단축 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-124">The following code sample demonstrates how to exclude a property from being sent to the client, and how to shorten property names:</span></span>

<span data-ttu-id="e1866-125">**데이터를 제외 하도록 클라이언트에 전송 되지 JsonIgnore 특성 및 메시지 크기를 줄이는 JsonProperty 특성을 보여 주는.NET 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="e1866-125">**.NET server code that demonstrates the JsonIgnore attribute to exclude data from being sent to the client, and the JsonProperty attribute to reduce message size**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

<span data-ttu-id="e1866-126">가독성을 유지 하기 위해 클라이언트 코드에서 관리의 용이성, 약식된 속성 이름은 이름일 수도 있습니다 사람이 친화적인에 매핑이 변경 메시지를 받은 후 / 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-126">In order to retain readability/ maintainability in the client code, the abbreviated property names can be remapped to human-friendly names after the message is received.</span></span> <span data-ttu-id="e1866-127">다음 코드 예제에서는 메시지 계약 (매핑)을 정의 하 여 긴 프로토콜로 약식된 이름을 다시 매핑의 한 가지 방법을 사용 하 고는 `reMap` 계약 최적화 된 메시지 클래스에 적용할 함수:</span><span class="sxs-lookup"><span data-stu-id="e1866-127">The following code sample demonstrates one possible way of remapping shortened names to longer ones, by defining a message contract (mapping), and using the `reMap` function to apply the contract to the optimized message class:</span></span>

<span data-ttu-id="e1866-128">**다시 매핑하는 클라이언트 쪽 JavaScript 코드를 이해 하기 쉬운 이름 속성 이름 단축**</span><span class="sxs-lookup"><span data-stu-id="e1866-128">**Client-side JavaScript code that remaps shortened property names to human-readable names**</span></span>

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

<span data-ttu-id="e1866-129">이름은 동일한 방법을 사용 하 여도 서버에 클라이언트에서 메시지에 단축 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-129">Names can be shortened in messages from the client to the server as well, using the same method.</span></span>

<span data-ttu-id="e1866-130">(즉, 메시지에 사용 된 메모리의 양)에 메모리 사용 공간 감소 메시지의 개체도 성능을 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-130">Reducing the memory footprint (that is, the amount of memory used for the message) of the message object can also improve performance.</span></span> <span data-ttu-id="e1866-131">예를 들어 경우의 전체 범위는 `int` 필요 하지 않은 한 `short` 또는 `byte` 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-131">For example, if the full range of an `int` is not needed, a `short` or `byte` can be used instead.</span></span>

<span data-ttu-id="e1866-132">메시지는 메시지의 크기를 줄이면 서버 메모리의 메시지 버스에 저장 되므로 서버 메모리 문제를 해결 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-132">Since messages are stored in the message bus in server memory, reducing the size of messages can also address server memory issues.</span></span>

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a><span data-ttu-id="e1866-133">SignalR 서버 성능을 튜닝</span><span class="sxs-lookup"><span data-stu-id="e1866-133">Tuning your SignalR server for performance</span></span>

<span data-ttu-id="e1866-134">다음 구성 설정은 SignalR 응용 프로그램에서 성능 향상을 위해 서버 조정할 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-134">The following configuration settings can be used to tune your server for better performance in a SignalR application.</span></span> <span data-ttu-id="e1866-135">ASP.NET 응용 프로그램의 성능을 향상 하는 방법에 대 한 일반적인 정보를 참조 하십시오. [ASP.NET 성능 향상](https://msdn.microsoft.com/library/ff647787.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-135">For general information on how to improve performance in an ASP.NET application, see [Improving ASP.NET Performance](https://msdn.microsoft.com/library/ff647787.aspx).</span></span>

<span data-ttu-id="e1866-136">**SignalR 구성 설정**</span><span class="sxs-lookup"><span data-stu-id="e1866-136">**SignalR configuration settings**</span></span>

- <span data-ttu-id="e1866-137">**DefaultMessageBufferSize**: 기본적으로 SignalR 허브 연결당 당 메모리에서 1000 메시지를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-137">**DefaultMessageBufferSize**: By default, SignalR retains 1000 messages in memory per hub per connection.</span></span> <span data-ttu-id="e1866-138">큰 메시지를 사용 하는 경우 이렇게이 값을 감소 시켜 용량을 줄일 수 있는 메모리 문제를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-138">If large messages are being used, this may create memory issues which can be alleviated by reducing this value.</span></span> <span data-ttu-id="e1866-139">이 설정을 설정할 수는 `Application_Start` 또는 ASP.NET 응용 프로그램에서 이벤트 처리기는 `Configuration` 자체 호스팅된 응용 프로그램에는 OWIN 시작 클래스의 메서드.</span><span class="sxs-lookup"><span data-stu-id="e1866-139">This setting can be set in the `Application_Start` event handler in an ASP.NET application, or in the `Configuration` method of an OWIN startup class in a self-hosted application.</span></span> <span data-ttu-id="e1866-140">다음 샘플에 사용 되는 서버 메모리의 양을 줄이기 위해 응용 프로그램의 메모리 사용 공간을 최소화 하기 위해이 값을 줄이는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-140">The following sample demonstrates how to reduce this value in order to reduce the memory footprint of your application in order to reduce the amount of server memory used:</span></span>

    <span data-ttu-id="e1866-141">**기본 메시지 버퍼 크기를 줄이면에 대 한 Global.asax에.NET 서버 코드**</span><span class="sxs-lookup"><span data-stu-id="e1866-141">**.NET server code in Global.asax for decreasing default message buffer size**</span></span>

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

<span data-ttu-id="e1866-142">**IIS 구성 설정**</span><span class="sxs-lookup"><span data-stu-id="e1866-142">**IIS configuration settings**</span></span>

- <span data-ttu-id="e1866-143">**응용 프로그램 당 최대 동시 요청**: 동시 IIS의 수를 늘리면 요청 늘어납니다 서버 리소스의 요청 처리에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-143">**Max concurrent requests per application**: Increasing the number of concurrent IIS requests will increase server resources available for serving requests.</span></span> <span data-ttu-id="e1866-144">기본값은 5000입니다. 이 설정의 늘리려면 다음 명령을 관리자 권한 명령 프롬프트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-144">The default value is 5000; to increase this setting, execute the following commands in an elevated command prompt:</span></span>

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]

<span data-ttu-id="e1866-145">**ASP.NET 구성 설정**</span><span class="sxs-lookup"><span data-stu-id="e1866-145">**ASP.NET configuration settings**</span></span>

<span data-ttu-id="e1866-146">이 섹션에서 설정할 수 있는 구성 설정에는 `aspnet.config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-146">This section includes configuration settings that can be set in the `aspnet.config` file.</span></span> <span data-ttu-id="e1866-147">이 파일은 플랫폼에 따라 다음 두 위치 중 하나에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-147">This file is found in one of two locations, depending on platform:</span></span>

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

<span data-ttu-id="e1866-148">SignalR 성능이 향상 될 수 있는 ASP.NET 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-148">ASP.NET settings that may improve SignalR performance include the following:</span></span>

- <span data-ttu-id="e1866-149">**CPU 당 최대 동시 요청**:이 설정을 성능 병목 현상을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-149">**Maximum concurrent requests per CPU**: Increasing this setting may alleviate performance bottlenecks.</span></span> <span data-ttu-id="e1866-150">이 설정을 늘릴,에 다음 구성 설정을 추가 `aspnet.config` 파일:</span><span class="sxs-lookup"><span data-stu-id="e1866-150">To increase this setting, add the following configuration setting to the `aspnet.config` file:</span></span>

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- <span data-ttu-id="e1866-151">**요청 큐 제한**: 총 연결 수 초과 하는 경우는 `maxConcurrentRequestsPerCPU` 설정, ASP.NET 요청 큐를 사용 하 여 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-151">**Request Queue Limit**: When the total number of connections exceeds the `maxConcurrentRequestsPerCPU` setting, ASP.NET will start throttling requests using a queue.</span></span> <span data-ttu-id="e1866-152">큐의 크기를 늘리려면 늘릴 수 있습니다는 `requestQueueLimit` 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-152">To increase the size of the queue, you can increase the `requestQueueLimit` setting.</span></span> <span data-ttu-id="e1866-153">이 수행 하려면에 다음 구성 설정을 추가 `processModel` 노드에서 `config/machine.config` (대신 `aspnet.config`):</span><span class="sxs-lookup"><span data-stu-id="e1866-153">To do this, add the following configuration setting to the `processModel` node in `config/machine.config` (rather than `aspnet.config`):</span></span>

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a><span data-ttu-id="e1866-154">성능 문제 해결</span><span class="sxs-lookup"><span data-stu-id="e1866-154">Troubleshooting performance issues</span></span>

<span data-ttu-id="e1866-155">이 섹션에서는 응용 프로그램에서 성능 병목 상태를 발견 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-155">This section describes ways to find performance bottlenecks in your application.</span></span>

### <a name="verifying-that-websocket-is-being-used"></a><span data-ttu-id="e1866-156">WebSocket이 사용 되 고 있는지 확인 하는 중</span><span class="sxs-lookup"><span data-stu-id="e1866-156">Verifying that WebSocket is being used</span></span>

<span data-ttu-id="e1866-157">SignalR를 사용할 수 있지만 다양 한 전송 방식 클라이언트와 서버 간의 통신에 대 한 WebSocket 뛰어난 성공을 제공 하 고 클라이언트와 서버에서 지 원하는 경우 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-157">While SignalR can use a variety of transports for communication between client and server, WebSocket offers a significant performance advantage, and should be used if the client and server support it.</span></span> <span data-ttu-id="e1866-158">클라이언트와 서버 WebSocket에 대 한 요구 사항을 충족 하는 경우를 확인 하려면 참조 [전송 및 대체](../getting-started/introduction-to-signalr.md#transports)합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-158">To determine if your client and server meet the requirements for WebSocket, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="e1866-159">어떤 전송을 응용 프로그램에서 사용량을 확인 하려면 브라우저 개발자 도구를 사용할 수 있으며 어떤 전송을 연결에 사용 되는지 확인 하려면 로그를 검사 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-159">To determine what transport is being used in your application, you can use the browser developer tools, and examine the logs to see what transport is being used for the connection.</span></span> <span data-ttu-id="e1866-160">Internet Explorer 및 Chrome 브라우저 개발 도구를 사용 하는 방법은 참조 하십시오. [전송 및 대체](../getting-started/introduction-to-signalr.md#transports)합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-160">For information on using the browser development tools in Internet Explorer and Chrome, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a><span data-ttu-id="e1866-161">SignalR 성능 카운터를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e1866-161">Using SignalR performance counters</span></span>

<span data-ttu-id="e1866-162">이 섹션에서는 SignalR 성능 카운터를 사용 하는 방법 설명에 `Microsoft.AspNet.SignalR.Utils` 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-162">This section describes how to enable and use SignalR performance counters, found in the `Microsoft.AspNet.SignalR.Utils` package.</span></span>

### <a name="installing-signalrexe"></a><span data-ttu-id="e1866-163">Signalr.exe 설치</span><span class="sxs-lookup"><span data-stu-id="e1866-163">Installing signalr.exe</span></span>

<span data-ttu-id="e1866-164">성능 카운터 SignalR.exe 라는 유틸리티를 사용 하 여 서버에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-164">Peformance counters can be added to the server using a utility called SignalR.exe.</span></span> <span data-ttu-id="e1866-165">이 유틸리티를 설치 하려면 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-165">To install this utility, follow these steps:</span></span>

1. <span data-ttu-id="e1866-166">Visual Studio 응용 프로그램에서 선택 **도구**, **라이브러리 패키지 관리자**, **솔루션에 대 한 NuGet 패키지 관리...**</span><span class="sxs-lookup"><span data-stu-id="e1866-166">In your Visual Studio application, select **Tools**, **Library Package Manager**, **Manage NuGet Packages for Solution...**</span></span>
2. <span data-ttu-id="e1866-167">검색할 **signalr.utils**, 설치를 선택 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-167">Search for **signalr.utils**, and select Install.</span></span>

    ![](signalr-performance/_static/image1.png)
3. <span data-ttu-id="e1866-168">패키지를 설치 하려면 사용권 계약에 동의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-168">Accept the license agreement to install the package.</span></span>
4. <span data-ttu-id="e1866-169">SignalR.exe 되도록 설치 됩니다. `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-169">SignalR.exe will be installed to `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span></span>

### <a name="installing-performance-counters-with-signalrexe"></a><span data-ttu-id="e1866-170">SignalR.exe와 성능 카운터를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-170">Installing performance counters with SignalR.exe</span></span>

<span data-ttu-id="e1866-171">SignalR 성능 카운터를 설치 하려면 다음 매개 변수를 사용 하는 관리자 권한 명령 프롬프트에서 SignalR.exe를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-171">To install SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

<span data-ttu-id="e1866-172">SignalR 성능 카운터를 제거 하려면 다음 매개 변수를 사용 하는 관리자 권한 명령 프롬프트에서 SignalR.exe를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-172">To remove SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a><span data-ttu-id="e1866-173">SignalR 성능 카운터</span><span class="sxs-lookup"><span data-stu-id="e1866-173">SignalR Performance counters</span></span>

<span data-ttu-id="e1866-174">유틸리티도 패키지는 다음 성능 카운터를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-174">The utilites package installs the following performance counters.</span></span> <span data-ttu-id="e1866-175">"Total" 카운터는 마지막 응용 프로그램 풀 또는 서버를 다시 시작한 이후 이벤트의 수를 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-175">The "Total" counters measure the number of events since the last application pool or server restart.</span></span>

<span data-ttu-id="e1866-176">**연결 메트릭**</span><span class="sxs-lookup"><span data-stu-id="e1866-176">**Connection metrics**</span></span>

<span data-ttu-id="e1866-177">다음과 같은 메트릭이 발생 하는 연결 수명 이벤트를 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-177">The following metrics measure the connection lifetime events that occur.</span></span> <span data-ttu-id="e1866-178">자세한 내용은 참조 [이해 하 고 연결 수명 이벤트를 처리](../guide-to-the-api/handling-connection-lifetime-events.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-178">For more information, see [Understanding and Handling Connection Lifetime Events](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

- <span data-ttu-id="e1866-179">**연결 된 연결**</span><span class="sxs-lookup"><span data-stu-id="e1866-179">**Connections Connected**</span></span>
- <span data-ttu-id="e1866-180">**다시 연결 하는 연결**</span><span class="sxs-lookup"><span data-stu-id="e1866-180">**Connections Reconnected**</span></span>
- <span data-ttu-id="e1866-181">**연결 Disonnected**</span><span class="sxs-lookup"><span data-stu-id="e1866-181">**Connections Disonnected**</span></span>
- <span data-ttu-id="e1866-182">**현재 연결**</span><span class="sxs-lookup"><span data-stu-id="e1866-182">**Connections Current**</span></span>

<span data-ttu-id="e1866-183">**메시지 메트릭스**</span><span class="sxs-lookup"><span data-stu-id="e1866-183">**Message metrics**</span></span>

<span data-ttu-id="e1866-184">다음과 같은 메트릭이 SignalR에 의해 생성 된 메시지 트래픽을 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-184">The following metrics measure the message traffic generated by SignalR.</span></span>

- <span data-ttu-id="e1866-185">**총 받은 연결 메시지**</span><span class="sxs-lookup"><span data-stu-id="e1866-185">**Connection Messages Received Total**</span></span>
- <span data-ttu-id="e1866-186">**총 보낸 연결 메시지**</span><span class="sxs-lookup"><span data-stu-id="e1866-186">**Connection Messages Sent Total**</span></span>
- <span data-ttu-id="e1866-187">**연결에 수신 메시지/초**</span><span class="sxs-lookup"><span data-stu-id="e1866-187">**Connection Messages Received/Sec**</span></span>
- <span data-ttu-id="e1866-188">**전송 연결 Messages/Sec**</span><span class="sxs-lookup"><span data-stu-id="e1866-188">**Connection Messages Sent/Sec**</span></span>

<span data-ttu-id="e1866-189">**메시지 버스 메트릭**</span><span class="sxs-lookup"><span data-stu-id="e1866-189">**Message bus metrics**</span></span>

<span data-ttu-id="e1866-190">다음 메트릭을 모든 들어오는 / 나가는 SignalR 메시지 사항이 큐는 내부 SignalR 메시지 버스를 통해 트래픽을 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-190">The following metrics measure traffic through the internal SignalR message bus, the queue in which all incoming and outgoing SignalR messages are placed.</span></span> <span data-ttu-id="e1866-191">메시지는 **게시 됨** 전송 되거나 브로드캐스트 때.</span><span class="sxs-lookup"><span data-stu-id="e1866-191">A message is **Published** when it is sent or broadcast.</span></span> <span data-ttu-id="e1866-192">A **구독자** 이 컨텍스트에서 메시지 버스에서 구독;이 클라이언트와 서버 자체의 수와 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-192">A **Subscriber** in this context is a subscription on the message bus; this should equal the number of clients plus the server itself.</span></span> <span data-ttu-id="e1866-193">**할당 된 작업자** 활성 연결;에 데이터를 전송 하는 구성 요소는 **사용 중인 작업자** 는 보내는 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-193">An **Allocated Worker** is a component that sends data to active connections; a **Busy Worker** is one that is actively sending a message.</span></span>

- <span data-ttu-id="e1866-194">**메시지 버스 받은 총 메시지**</span><span class="sxs-lookup"><span data-stu-id="e1866-194">**Message Bus Messages Received Total**</span></span>
- <span data-ttu-id="e1866-195">**메시지 버스 메시지 Received/Sec**</span><span class="sxs-lookup"><span data-stu-id="e1866-195">**Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="e1866-196">**메시지 버스 메시지 게시 합계**</span><span class="sxs-lookup"><span data-stu-id="e1866-196">**Message Bus Messages Published Total**</span></span>
- <span data-ttu-id="e1866-197">**메시지 버스 Messages 게시/Sec**</span><span class="sxs-lookup"><span data-stu-id="e1866-197">**Message Bus Messages Published/Sec**</span></span>
- <span data-ttu-id="e1866-198">**메시지 버스 구독자 현재**</span><span class="sxs-lookup"><span data-stu-id="e1866-198">**Message Bus Subscribers Current**</span></span>
- <span data-ttu-id="e1866-199">**메시지 버스 구독자 합계**</span><span class="sxs-lookup"><span data-stu-id="e1866-199">**Message Bus Subscribers Total**</span></span>
- <span data-ttu-id="e1866-200">**메시지 버스 구독자/Sec**</span><span class="sxs-lookup"><span data-stu-id="e1866-200">**Message Bus Subscribers/Sec**</span></span>
- <span data-ttu-id="e1866-201">**메시지 버스 작업자를 할당 합니다.**</span><span class="sxs-lookup"><span data-stu-id="e1866-201">**Message Bus Allocated Workers**</span></span>
- <span data-ttu-id="e1866-202">**메시지 버스 근무 중인 노동자**</span><span class="sxs-lookup"><span data-stu-id="e1866-202">**Message Bus Busy Workers**</span></span>
- <span data-ttu-id="e1866-203">**메시지 버스 항목 현재**</span><span class="sxs-lookup"><span data-stu-id="e1866-203">**Message Bus Topics Current**</span></span>

<span data-ttu-id="e1866-204">**오차 메트릭**</span><span class="sxs-lookup"><span data-stu-id="e1866-204">**Error metrics**</span></span>

<span data-ttu-id="e1866-205">SignalR 메시지 트래픽에 의해 생성 된 오류를 측정 하는 다음 메트릭을 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-205">The following metrics measure errors generated by SignalR message traffic.</span></span> <span data-ttu-id="e1866-206">**허브 해상도** 허브 또는 허브 메서드를 확인할 수 없는 경우 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-206">**Hub Resolution** errors occur when a hub or hub method cannot be resolved.</span></span> <span data-ttu-id="e1866-207">**허브 호출** 오류는 허브 메서드를 호출 하는 동안 발생 한 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-207">**Hub Invocation** errors are exceptions thrown while invoking a hub method.</span></span> <span data-ttu-id="e1866-208">**전송** 오류는 연결 오류는 HTTP 요청 또는 응답 하는 동안 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-208">**Transport** errors are connection errors thrown during an HTTP request or response.</span></span>

- <span data-ttu-id="e1866-209">**모든 총 오류 수:**</span><span class="sxs-lookup"><span data-stu-id="e1866-209">**Errors: All Total**</span></span>
- <span data-ttu-id="e1866-210">**오류: All/Sec**</span><span class="sxs-lookup"><span data-stu-id="e1866-210">**Errors: All/Sec**</span></span>
- <span data-ttu-id="e1866-211">**허브 해상도 총 오류 수:**</span><span class="sxs-lookup"><span data-stu-id="e1866-211">**Errors: Hub Resolution Total**</span></span>
- <span data-ttu-id="e1866-212">**오류: 허브 해상도/초**</span><span class="sxs-lookup"><span data-stu-id="e1866-212">**Errors: Hub Resolution/Sec**</span></span>
- <span data-ttu-id="e1866-213">**허브 호출 총 오류 수:**</span><span class="sxs-lookup"><span data-stu-id="e1866-213">**Errors: Hub Invocation Total**</span></span>
- <span data-ttu-id="e1866-214">**오류: 허브 호출 수/초**</span><span class="sxs-lookup"><span data-stu-id="e1866-214">**Errors: Hub Invocation/Sec**</span></span>
- <span data-ttu-id="e1866-215">**전송 총 오류 수:**</span><span class="sxs-lookup"><span data-stu-id="e1866-215">**Errors: Transport Total**</span></span>
- <span data-ttu-id="e1866-216">**오류: 전송 수/초**</span><span class="sxs-lookup"><span data-stu-id="e1866-216">**Errors: Transport/Sec**</span></span>

<span data-ttu-id="e1866-217">**확장 메트릭**</span><span class="sxs-lookup"><span data-stu-id="e1866-217">**Scaleout metrics**</span></span>

<span data-ttu-id="e1866-218">다음 메트릭을 트래픽과 확장 공급자에서 발생 한 오류를 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-218">The following metrics measure traffic and errors generated by the scaleout provider.</span></span> <span data-ttu-id="e1866-219">A **스트림** 이 컨텍스트에서이 확장 공급자에서 사용 하는 배율 단위에는이 SQL Server가 사용 하는 경우 테이블, 서비스 버스를 사용 하는 경우 항목 및 구독을 Redis 사용 되는 경우.</span><span class="sxs-lookup"><span data-stu-id="e1866-219">A **Stream** in this context is a scale unit used by the scaleout provider; this is a table if SQL Server is used, a Topic if Service Bus is used, and a Subscription if Redis is used.</span></span> <span data-ttu-id="e1866-220">기본적으로 스트림을 하나만 사용 되지만이 SQL Server와 서비스 버스에서 구성을 통해 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-220">By default, only one stream is used, but this can be increased through configuration on SQL Server and Service Bus.</span></span> <span data-ttu-id="e1866-221">A **버퍼링** 스트림이 faulted 상태로 전환; 스트림이 faulted 상태가 즉시 스트림에 오류가 더 이상 될 때까지 백플레인에 보낸 모든 메시지가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-221">A **Buffering** stream is one that has entered a faulted state; when the stream is in the faulted state, all messages sent to the backplane will fail immediately until the stream is no longer faulting.</span></span> <span data-ttu-id="e1866-222">**전송 큐 길이** 게시 되었지만 아직 보내지 않은 메시지 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-222">The **Send Queue Length** is the number of messages that have been posted but not yet sent.</span></span>

- <span data-ttu-id="e1866-223">**확장 메시지 버스 메시지 Received/Sec**</span><span class="sxs-lookup"><span data-stu-id="e1866-223">**Scaleout Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="e1866-224">**확장 스트림 합계**</span><span class="sxs-lookup"><span data-stu-id="e1866-224">**Scaleout Streams Total**</span></span>
- <span data-ttu-id="e1866-225">**확장 스트림 열기**</span><span class="sxs-lookup"><span data-stu-id="e1866-225">**Scaleout Streams Open**</span></span>
- <span data-ttu-id="e1866-226">**확장 스트림 버퍼링**</span><span class="sxs-lookup"><span data-stu-id="e1866-226">**Scaleout Streams Buffering**</span></span>
- <span data-ttu-id="e1866-227">**확장 오류 합계**</span><span class="sxs-lookup"><span data-stu-id="e1866-227">**Scaleout Errors Total**</span></span>
- <span data-ttu-id="e1866-228">**초당 확장 오류**</span><span class="sxs-lookup"><span data-stu-id="e1866-228">**Scaleout Errors/Sec**</span></span>
- <span data-ttu-id="e1866-229">**확장 송신 큐 길이**</span><span class="sxs-lookup"><span data-stu-id="e1866-229">**Scaleout Send Queue Length**</span></span>

<span data-ttu-id="e1866-230">이러한 카운터를 측정 하는 기능에 대 한 자세한 내용은 참조 하십시오. [Azure 서비스 버스에 SignalR 확장](scaleout-with-windows-azure-service-bus.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-230">For more information on what these counters are measuring, see [SignalR Scaleout with Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span></span>

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a><span data-ttu-id="e1866-231">다른 성능 카운터를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e1866-231">Using other performance counters</span></span>

<span data-ttu-id="e1866-232">다음 성능 카운터는 응용 프로그램의 성능 모니터링에 유용한 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-232">The following performance counters may also be useful in monitoring your application's performance.</span></span>

<span data-ttu-id="e1866-233">**Memory**</span><span class="sxs-lookup"><span data-stu-id="e1866-233">**Memory**</span></span>

- <span data-ttu-id="e1866-234">전체 힙 (w3wp)의.NET CLR 메모리 # 바이트</span><span class="sxs-lookup"><span data-stu-id="e1866-234">.NET CLR Memory# bytes in all Heaps (for w3wp)</span></span>

<span data-ttu-id="e1866-235">**ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="e1866-235">**ASP.NET**</span></span>

- <span data-ttu-id="e1866-236">ASP.NET\Requests Current</span><span class="sxs-lookup"><span data-stu-id="e1866-236">ASP.NET\Requests Current</span></span>
- <span data-ttu-id="e1866-237">ASP.NET\Queued</span><span class="sxs-lookup"><span data-stu-id="e1866-237">ASP.NET\Queued</span></span>
- <span data-ttu-id="e1866-238">ASP.NET\Rejected</span><span class="sxs-lookup"><span data-stu-id="e1866-238">ASP.NET\Rejected</span></span>

<span data-ttu-id="e1866-239">**CPU**</span><span class="sxs-lookup"><span data-stu-id="e1866-239">**CPU**</span></span>

- <span data-ttu-id="e1866-240">Processor Information\Processor Time</span><span class="sxs-lookup"><span data-stu-id="e1866-240">Processor Information\Processor Time</span></span>

<span data-ttu-id="e1866-241">**TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="e1866-241">**TCP/IP**</span></span>

- <span data-ttu-id="e1866-242">설정 된 TCPv6/연결</span><span class="sxs-lookup"><span data-stu-id="e1866-242">TCPv6/Connections Established</span></span>
- <span data-ttu-id="e1866-243">설정 된 TCPv4/연결</span><span class="sxs-lookup"><span data-stu-id="e1866-243">TCPv4/Connections Established</span></span>

<span data-ttu-id="e1866-244">**웹 서비스**</span><span class="sxs-lookup"><span data-stu-id="e1866-244">**Web Service**</span></span>

- <span data-ttu-id="e1866-245">웹 Connections</span><span class="sxs-lookup"><span data-stu-id="e1866-245">Web Service\Current Connections</span></span>
- <span data-ttu-id="e1866-246">웹 Service\Maximum 연결</span><span class="sxs-lookup"><span data-stu-id="e1866-246">Web Service\Maximum Connections</span></span>

<span data-ttu-id="e1866-247">**스레딩**</span><span class="sxs-lookup"><span data-stu-id="e1866-247">**Threading**</span></span>

- <span data-ttu-id="e1866-248">.NET CLR LocksAndThreads\# 현재 논리 스레드</span><span class="sxs-lookup"><span data-stu-id="e1866-248">.NET CLR LocksAndThreads\# of current logical Threads</span></span>
- <span data-ttu-id="e1866-249">.NET CLR LocksAnd 스레드\# 현재 실제 스레드</span><span class="sxs-lookup"><span data-stu-id="e1866-249">.NET CLR LocksAnd Threads\# of current physical Threads</span></span>

<a id="otherresources"></a>

## <a name="other-resources"></a><span data-ttu-id="e1866-250">기타 리소스</span><span class="sxs-lookup"><span data-stu-id="e1866-250">Other Resources</span></span>

<span data-ttu-id="e1866-251">ASP.NET 성능 모니터링 및 튜닝에 대 한 자세한 내용은 다음 항목을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1866-251">For more information on ASP.NET performance monitoring and tuning, see the following topics:</span></span>

- <span data-ttu-id="e1866-252">[ASP.NET 성능 개요](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="e1866-252">[ASP.NET Performance Overview](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span></span>
- [<span data-ttu-id="e1866-253">IIS 7.5, IIS 7.0 및 IIS 6.0에 ASP.NET 스레드 사용</span><span class="sxs-lookup"><span data-stu-id="e1866-253">ASP.NET Thread Usage on IIS 7.5, IIS 7.0, and IIS 6.0</span></span>](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [<span data-ttu-id="e1866-254">&lt;applicationPool&gt; 요소 (웹 설정)</span><span class="sxs-lookup"><span data-stu-id="e1866-254">&lt;applicationPool&gt; Element (Web Settings)</span></span>](https://msdn.microsoft.com/library/dd560842.aspx)
