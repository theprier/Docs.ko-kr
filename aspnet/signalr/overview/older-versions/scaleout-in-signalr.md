---
uid: signalr/overview/older-versions/scaleout-in-signalr
title: SignalR에서 확장 소개 1.x | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/29/2013
ms.topic: article
ms.assetid: 3fd9f11c-799b-4001-bd60-1e70cfc61c19
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/older-versions/scaleout-in-signalr
msc.type: authoredcontent
ms.openlocfilehash: ee3384046bf8a0f363aa6801d7a46f68b2bf125a
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
ms.locfileid: "28043748"
---
<a name="introduction-to-scaleout-in-signalr-1x"></a><span data-ttu-id="753df-102">SignalR에서 확장 소개 1.x</span><span class="sxs-lookup"><span data-stu-id="753df-102">Introduction to Scaleout in SignalR 1.x</span></span>
====================
<span data-ttu-id="753df-103">여 [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="753df-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

<span data-ttu-id="753df-104">일반적으로 두 가지 웹 응용 프로그램의 크기를 조정 하려면: *수직* 및 *확장할*합니다.</span><span class="sxs-lookup"><span data-stu-id="753df-104">In general, there are two ways to scale a web application: *scale up* and *scale out*.</span></span>

- <span data-ttu-id="753df-105">대형 서버 (또는 더 큰 VM)를 사용 하 여 더 많은 RAM, Cpu, 등으로 평균 수직 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="753df-105">Scale up means using a larger server (or a larger VM) with more RAM, CPUs, etc.</span></span>
- <span data-ttu-id="753df-106">부하를 처리할 서버를 추가 하는 수단을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="753df-106">Scale out means adding more servers to handle the load.</span></span>

<span data-ttu-id="753df-107">컴퓨터의 크기에 제한이 신속 하 게 도달 하면는 수직 확장 문제가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="753df-107">The problem with scaling up is that you quickly hit a limit on the size of the machine.</span></span> <span data-ttu-id="753df-108">이 외 수평 확장 해야 합니다. 그러나 확장 시, 클라이언트가 서로 다른 서버 라우팅할 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="753df-108">Beyond that, you need to scale out. However, when you scale out, clients can get routed to different servers.</span></span> <span data-ttu-id="753df-109">하나의 서버에 연결 된 클라이언트에서 다른 서버에서 보낸 메시지를 받지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="753df-109">A client that is connected to one server will not receive messages sent from another server.</span></span>

![](scaleout-in-signalr/_static/image1.png)

<span data-ttu-id="753df-110">한 가지 해결 방법은 라는 구성 요소를 사용 하 여 서버 간에 메시지를 전달 하는 *백플레인*합니다.</span><span class="sxs-lookup"><span data-stu-id="753df-110">One solution is to forward messages between servers, using a component called a *backplane*.</span></span> <span data-ttu-id="753df-111">사용 하도록 설정 하는 백플레인에 각 응용 프로그램 인스턴스에 메시지를 백플레인에 보내고 백플레인에서 다른 응용 프로그램 인스턴스에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="753df-111">With a backplane enabled, each application instance sends messages to the backplane, and the backplane forwards them to the other application instances.</span></span> <span data-ttu-id="753df-112">(전기 부문에서 백플레인에 병렬 커넥터의 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="753df-112">(In electronics, a backplane is a group of parallel connectors.</span></span> <span data-ttu-id="753df-113">비유, SignalR 백플레인 연결 여러 서버 합니다.)</span><span class="sxs-lookup"><span data-stu-id="753df-113">By analogy, a SignalR backplane connects multiple servers.)</span></span>

![](scaleout-in-signalr/_static/image2.png)

<span data-ttu-id="753df-114">SignalR 현재 세 가지 백플레인을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="753df-114">SignalR currently provides three backplanes:</span></span>

- <span data-ttu-id="753df-115">**Azure 서비스 버스**합니다.</span><span class="sxs-lookup"><span data-stu-id="753df-115">**Azure Service Bus**.</span></span> <span data-ttu-id="753df-116">서비스 버스에 구성 요소가 느슨하게 결합 된 방식으로 메시지를 보낼 수 있도록 하는 메시징 인프라입니다.</span><span class="sxs-lookup"><span data-stu-id="753df-116">Service Bus is a messaging infrastructure that allows components to send messages in a loosely coupled way.</span></span>
- <span data-ttu-id="753df-117">**Redis**합니다.</span><span class="sxs-lookup"><span data-stu-id="753df-117">**Redis**.</span></span> <span data-ttu-id="753df-118">Redis는 메모리에 키-값 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="753df-118">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="753df-119">Redis는 메시지를 보내기 위한 게시/구독 ("pub/sub") 패턴을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="753df-119">Redis supports a publish/subscribe ("pub/sub") pattern for sending messages.</span></span>
- <span data-ttu-id="753df-120">**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="753df-120">**SQL Server**.</span></span> <span data-ttu-id="753df-121">SQL Server 백플레인에서 SQL 테이블에 메시지를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="753df-121">The SQL Server backplane writes messages to SQL tables.</span></span> <span data-ttu-id="753df-122">백플레인에서 효율적인 메시징에 대 한 Service Broker를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="753df-122">The backplane uses Service Broker for efficient messaging.</span></span> <span data-ttu-id="753df-123">그러나 해당 Service Broker를 사용 하지 않는 경우에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="753df-123">However, it also works if Service Broker is not enabled.</span></span>

<span data-ttu-id="753df-124">Azure에서 응용 프로그램을 배포 하는 경우에 Azure 서비스 버스 백플레인으로 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="753df-124">If you deploy your application on Azure, consider using the Azure Service Bus backplane.</span></span> <span data-ttu-id="753df-125">사용자 고유의 서버 팜에 배포 하는 경우 SQL Server 또는 Redis 백플레인 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="753df-125">If you are deploying to your own server farm, consider the SQL Server or Redis backplanes.</span></span>

<span data-ttu-id="753df-126">다음 항목에서는 각 백플레인에 대 한 단계별 자습서 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="753df-126">The following topics contain step-by-step tutorials for each backplane:</span></span>

- [<span data-ttu-id="753df-127">Azure Service Bus로 SignalR 규모 확장</span><span class="sxs-lookup"><span data-stu-id="753df-127">SignalR Scaleout with Azure Service Bus</span></span>](scaleout-with-windows-azure-service-bus.md)
- [<span data-ttu-id="753df-128">Redis로 SignalR 규모 확장</span><span class="sxs-lookup"><span data-stu-id="753df-128">SignalR Scaleout with Redis</span></span>](scaleout-with-redis.md)
- [<span data-ttu-id="753df-129">SQL Server로 SignalR 규모 확장</span><span class="sxs-lookup"><span data-stu-id="753df-129">SignalR Scaleout with SQL Server</span></span>](scaleout-with-sql-server.md)

## <a name="implementation"></a><span data-ttu-id="753df-130">구현</span><span class="sxs-lookup"><span data-stu-id="753df-130">Implementation</span></span>

<span data-ttu-id="753df-131">SignalR에 모든 메시지는 메시지 버스를 통해 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="753df-131">In SignalR, every message is sent through a message bus.</span></span> <span data-ttu-id="753df-132">메시지 버스 구현 하는 [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) 인터페이스에는 게시/구독 추상화를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="753df-132">A message bus implements the [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) interface, which provides a publish/subscribe abstraction.</span></span> <span data-ttu-id="753df-133">기본 대체 하 여 작업의 백플레인 **IMessageBus** 는 버스 해당 백플레인에서 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="753df-133">The backplanes work by replacing the default **IMessageBus** with a bus designed for that backplane.</span></span> <span data-ttu-id="753df-134">예를 들어 Redis 용 메시지 버스는 [RedisMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.redis.redismessagebus(v=vs.100).aspx), Redis를 사용 하 여 [pub/sub](http://redis.io/topics/pubsub) 메시지를 송수신 하는 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="753df-134">For example, the message bus for Redis is [RedisMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.redis.redismessagebus(v=vs.100).aspx), and it uses the Redis [pub/sub](http://redis.io/topics/pubsub) mechanism to send and receive messages.</span></span>

<span data-ttu-id="753df-135">버스를 통해 백플레인에서에 각 서버 인스턴스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="753df-135">Each server instance connects to the backplane through the bus.</span></span> <span data-ttu-id="753df-136">메시지를 보낼 때를 백플레인에 이동 하 고 백플레인에서 모든 서버에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="753df-136">When a message is sent, it goes to the backplane, and the backplane sends it to every server.</span></span> <span data-ttu-id="753df-137">서버에서 메시지 백플레인에서 받으면 메시지 로컬 캐시에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="753df-137">When a server gets a message from the backplane, it puts the message in its local cache.</span></span> <span data-ttu-id="753df-138">서버는 다음 로컬 캐시에서 클라이언트에 메시지를 배달 합니다.</span><span class="sxs-lookup"><span data-stu-id="753df-138">The server then delivers messages to clients from its local cache.</span></span>

<span data-ttu-id="753df-139">각 클라이언트 연결에 대 한 커서를 사용 하는 클라이언트의 진행 상황 메시지 스트림을 읽는 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="753df-139">For each client connection, the client's progress in reading the message stream is tracked using a cursor.</span></span> <span data-ttu-id="753df-140">(커서 메시지 스트림 내의 위치를 나타냅니다.) 클라이언트 연결을 끊고 다시 연결을 하는 경우 클라이언트의 커서 값 뒤에 도착 하는 모든 메시지 버스를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="753df-140">(A cursor represents a position in the message stream.) If a client disconnects and then reconnects, it asks the bus for any messages that arrived after the client's cursor value.</span></span> <span data-ttu-id="753df-141">동일한 상황이 연결을 사용 하는 경우 [긴 폴링](../getting-started/introduction-to-signalr.md#transports)합니다.</span><span class="sxs-lookup"><span data-stu-id="753df-141">The same thing happens when a connection uses [long polling](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="753df-142">긴 폴링 요청 완료 되 면 클라이언트는 새 연결을 열고 하 고 커서 뒤 도착 하는 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="753df-142">After a long poll request completes, the client opens a new connection and asks for messages that arrived after the cursor.</span></span>

<span data-ttu-id="753df-143">커서 메커니즘의 작동 클라이언트에 다른 서버에 전달 되는 경우에 다시 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="753df-143">The cursor mechanism works even if a client is routed to a different server on reconnect.</span></span> <span data-ttu-id="753df-144">백플레인에서 모든 서버를 인식 하며 클라이언트가 연결 하는 서버는 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="753df-144">The backplane is aware of all the servers, and it doesn't matter which server a client connects to.</span></span>

## <a name="limitations"></a><span data-ttu-id="753df-145">제한 사항</span><span class="sxs-lookup"><span data-stu-id="753df-145">Limitations</span></span>

<span data-ttu-id="753df-146">백플레인에 사용 하 여 최대 메시지 처리량은 단일 서버 노드를 직접 클라이언트와 통신 하는 경우 보다 낮습니다.</span><span class="sxs-lookup"><span data-stu-id="753df-146">Using a backplane, the maximum message throughput is lower than it is when clients talk directly to a single server node.</span></span> <span data-ttu-id="753df-147">백플레인에서 백플레인에서 병목 지점이 될 수 있도록 모든 노드에 모든 메시지를 전달 하는 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="753df-147">That's because the backplane forwards every message to every node, so the backplane can become a bottleneck.</span></span> <span data-ttu-id="753df-148">이 제한 사항은 문제가 있는지 여부를 응용 프로그램에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="753df-148">Whether this limitation is a problem depends on the application.</span></span> <span data-ttu-id="753df-149">예를 들어 다음은 몇 가지 일반적인 SignalR 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="753df-149">For example, here are some typical SignalR scenarios:</span></span>

- <span data-ttu-id="753df-150">[서버 브로드캐스트](tutorial-server-broadcast-with-aspnet-signalr.md) (예: 주식 시세): 백플레인 서버 메시지를 보내는 속도 제어 하기 때문에이 시나리오에 대 한 잘 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="753df-150">[Server broadcast](tutorial-server-broadcast-with-aspnet-signalr.md) (e.g., stock ticker): Backplanes work well for this scenario, because the server controls the rate at which messages are sent.</span></span>
- <span data-ttu-id="753df-151">[클라이언트-](tutorial-getting-started-with-signalr.md) (예: 채트):이 시나리오에서는 클라이언트의 수와 크기와 메시지 수가 조정 백플레인에서 병목 지점이 될 수 있습니다; 그리고 즉, 증가 하는 메시지의 속도 비율에 따라 더 많은 클라이언트에 조인 합니다.</span><span class="sxs-lookup"><span data-stu-id="753df-151">[Client-to-client](tutorial-getting-started-with-signalr.md) (e.g., chat): In this scenario, the backplane might be a bottleneck if the number of messages scales with the number of clients; that is, if the rate of messages grows proportionally as more clients join.</span></span>
- <span data-ttu-id="753df-152">[높은 주파수 실시간](tutorial-high-frequency-realtime-with-signalr.md) (예: 실시간 게임): 백플레인에이 시나리오에 적합 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="753df-152">[High-frequency realtime](tutorial-high-frequency-realtime-with-signalr.md) (e.g., real-time games): A backplane is not recommended for this scenario.</span></span>

## <a name="enabling-tracing-for-signalr-scaleout"></a><span data-ttu-id="753df-153">SignalR 확장에 대 한 추적을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="753df-153">Enabling Tracing For SignalR Scaleout</span></span>

<span data-ttu-id="753df-154">백플레인에 대 한 추적을 사용 하려면 다음 섹션에서는 루트 아래에 있는 web.config 파일에 추가 **구성** 요소:</span><span class="sxs-lookup"><span data-stu-id="753df-154">To enable tracing for the backplanes, add the following sections to the web.config file, under the root **configuration** element:</span></span>

[!code-html[Main](scaleout-in-signalr/samples/sample1.html)]
