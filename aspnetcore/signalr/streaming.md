---
title: ASP.NET Core SignalR에서 스트리밍 사용
author: tdykstra
description: ''
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 06/07/2018
uid: signalr/streaming
ms.openlocfilehash: 70f12999b7f4230147b9ea43f6f7730b0816c43a
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50206390"
---
# <a name="use-streaming-in-aspnet-core-signalr"></a><span data-ttu-id="e633c-102">ASP.NET Core SignalR에서 스트리밍 사용</span><span class="sxs-lookup"><span data-stu-id="e633c-102">Use streaming in ASP.NET Core SignalR</span></span>

<span data-ttu-id="e633c-103">작성자: [Brennan Conroy](https://github.com/BrennanConroy)</span><span class="sxs-lookup"><span data-stu-id="e633c-103">By [Brennan Conroy](https://github.com/BrennanConroy)</span></span>

<span data-ttu-id="e633c-104">ASP.NET Core SignalR은 서버 메서드의 스트리밍 반환 값을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e633c-104">ASP.NET Core SignalR supports streaming return values of server methods.</span></span> <span data-ttu-id="e633c-105">이 기능은 지속적으로 데이터 조각이 전달되는 시나리오에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="e633c-105">This is useful for scenarios where fragments of data will come in over time.</span></span> <span data-ttu-id="e633c-106">클라이언트에 반환 값을 스트리밍할 때 모든 조각이 사용 가능할 때까지 기다리는 대신 사용 가능한 즉시 각 조각을 클라이언트로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="e633c-106">When a return value is streamed to the client, each fragment is sent to the client as soon as it becomes available, rather than waiting for all the data to become available.</span></span>

<span data-ttu-id="e633c-107">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/streaming/sample) ([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="e633c-107">[View or download sample code](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/streaming/sample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="set-up-the-hub"></a><span data-ttu-id="e633c-108">허브 설정</span><span class="sxs-lookup"><span data-stu-id="e633c-108">Set up the hub</span></span>

<span data-ttu-id="e633c-109">`ChannelReader<T>` 또는 `Task<ChannelReader<T>>`를 반환하는 허브 메서드는 자동으로 스트리밍 허브 메서드로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="e633c-109">A hub method automatically becomes a streaming hub method when it returns a `ChannelReader<T>` or a `Task<ChannelReader<T>>`.</span></span> <span data-ttu-id="e633c-110">다음은 클라이언트로 데이터를 스트리밍하는 기본적인 방법을 보여주는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="e633c-110">Below is a sample that shows the basics of streaming data to the client.</span></span> <span data-ttu-id="e633c-111">개체가 `ChannelReader`에 쓰여질 때마다 해당 개체는 클라이언트로 즉시 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="e633c-111">Whenever an object is written to the `ChannelReader` that object is immediately sent to the client.</span></span> <span data-ttu-id="e633c-112">마지막으로 `ChannelReader`가 완료되어 스트림이 닫혔음을 클라이언트에 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="e633c-112">At the end, the `ChannelReader` is completed to tell the client the stream is closed.</span></span>

> [!NOTE]
> <span data-ttu-id="e633c-113">백그라운드 스레드에서 `ChannelReader`에 쓰고 최대한 빨리 `ChannelReader`를 반환하십시오.</span><span class="sxs-lookup"><span data-stu-id="e633c-113">Write to the `ChannelReader` on a background thread and return the `ChannelReader` as soon as possible.</span></span> <span data-ttu-id="e633c-114">`ChannelReader`가 반환될 때까지 다른 허브 호출들은 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="e633c-114">Other hub invocations will be blocked until a `ChannelReader` is returned.</span></span>

[!code-csharp[Streaming hub method](streaming/sample/Hubs/StreamHub.cs?range=10-34)]

## <a name="net-client"></a><span data-ttu-id="e633c-115">.NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="e633c-115">.NET client</span></span>

<span data-ttu-id="e633c-116">스트리밍 메서드를 호출하기 위해 `HubConnection`의 `StreamAsChannelAsync` 메서드가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e633c-116">The `StreamAsChannelAsync` method on `HubConnection` is used to invoke a streaming method.</span></span> <span data-ttu-id="e633c-117">허브 메서드 이름과 허브 메서드에 정의된 인수를 `StreamAsChannelAsync`에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="e633c-117">Pass the hub method name, and arguments defined in the hub method to `StreamAsChannelAsync`.</span></span> <span data-ttu-id="e633c-118">`StreamAsChannelAsync<T>`의 제네릭 매개 변수는 스트리밍 메서드에서 반환되는 개체의 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e633c-118">The generic parameter on `StreamAsChannelAsync<T>` specifies the type of objects returned by the streaming method.</span></span> <span data-ttu-id="e633c-119">스트림 호출에서는 `ChannelReader<T>`가 반환되며 이는 클라이언트에서 스트림을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e633c-119">A `ChannelReader<T>` is returned from the stream invocation, and represents the stream on the client.</span></span> <span data-ttu-id="e633c-120">데이터를 읽기 위해서는 데이터가 사용 가능할 때 `WaitToReadAsync` 및 `TryRead` 호출을 반복하는 패턴이 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="e633c-120">To read data, a common pattern is to loop over `WaitToReadAsync` and call `TryRead` when data is available.</span></span> <span data-ttu-id="e633c-121">서버에 의해 스트림이 닫히거나 `StreamAsChannelAsync`에 전달된 취소 토큰이 취소되면 루프가 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="e633c-121">The loop will end when the stream has been closed by the server, or the cancellation token passed to `StreamAsChannelAsync` is canceled.</span></span>

```csharp
var channel = await hubConnection.StreamAsChannelAsync<int>("Counter", 10, 500, CancellationToken.None);

// Wait asynchronously for data to become available
while (await channel.WaitToReadAsync())
{
    // Read all currently available data synchronously, before waiting for more data
    while (channel.TryRead(out var count))
    {
        Console.WriteLine($"{count}");
    }
}

Console.WriteLine("Streaming completed");
```

## <a name="javascript-client"></a><span data-ttu-id="e633c-122">JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="e633c-122">JavaScript client</span></span>

<span data-ttu-id="e633c-123">JavaScript 클라이언트는 `connection.stream`을 사용하여 허브의 스트리밍 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e633c-123">JavaScript clients call streaming methods on hubs by using `connection.stream`.</span></span> <span data-ttu-id="e633c-124">이 `stream` 메서드는 두 가지 인수를 전달받습니다.</span><span class="sxs-lookup"><span data-stu-id="e633c-124">The `stream` method accepts two arguments:</span></span>

* <span data-ttu-id="e633c-125">허브 메서드의 이름.</span><span class="sxs-lookup"><span data-stu-id="e633c-125">The name of the hub method.</span></span> <span data-ttu-id="e633c-126">다음 예제에서 허브 메서드 이름은 `Counter`입니다.</span><span class="sxs-lookup"><span data-stu-id="e633c-126">In the following example, the hub method name is `Counter`.</span></span>
* <span data-ttu-id="e633c-127">허브 메서드에 정의된 인수.</span><span class="sxs-lookup"><span data-stu-id="e633c-127">Arguments defined in the hub method.</span></span> <span data-ttu-id="e633c-128">다음 예에서 인수는 수신할 스트림 항목의 갯수에 대한 카운트 및 스트림 항목 사이의 지연 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e633c-128">In the following example, the arguments are: a count for the number of stream items to receive, and the delay between stream items.</span></span>

<span data-ttu-id="e633c-129">`connection.stream`은 `subscribe` 메서드가 포함된 `IStreamResult`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e633c-129">`connection.stream` returns an `IStreamResult` which contains a `subscribe` method.</span></span> <span data-ttu-id="e633c-130">`IStreamSubscriber`를 `subscribe`에 전달하고 `stream` 호출에서 알림을 받을 `next`, `error`및 `complete` 콜백을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e633c-130">Pass an `IStreamSubscriber` to `subscribe` and set the `next`, `error`, and `complete` callbacks to get notifications from the `stream` invocation.</span></span>

[!code-javascript[Streaming javascript](streaming/sample/wwwroot/js/stream.js?range=19-36)]

<span data-ttu-id="e633c-131">클라이언트에서 스트림을 끝내려면 `subscribe` 메서드에서 반환되는 `ISubscription`에서 `dispose` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e633c-131">To end the stream from the client, call the `dispose` method on the `ISubscription` that is returned from the `subscribe` method.</span></span>

## <a name="related-resources"></a><span data-ttu-id="e633c-132">관련 자료</span><span class="sxs-lookup"><span data-stu-id="e633c-132">Related resources</span></span>

* [<span data-ttu-id="e633c-133">허브</span><span class="sxs-lookup"><span data-stu-id="e633c-133">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="e633c-134">.NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="e633c-134">.NET client</span></span>](xref:signalr/dotnet-client)
* [<span data-ttu-id="e633c-135">JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="e633c-135">JavaScript client</span></span>](xref:signalr/javascript-client)
* [<span data-ttu-id="e633c-136">Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="e633c-136">Publish to Azure</span></span>](xref:signalr/publish-to-azure-web-app)
