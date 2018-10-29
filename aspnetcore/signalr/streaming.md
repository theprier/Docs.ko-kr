---
title: ASP.NET Core SignalR의 스트리밍 사용
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
# <a name="use-streaming-in-aspnet-core-signalr"></a><span data-ttu-id="9cdb3-102">ASP.NET Core SignalR의 스트리밍 사용</span><span class="sxs-lookup"><span data-stu-id="9cdb3-102">Use streaming in ASP.NET Core SignalR</span></span>

<span data-ttu-id="9cdb3-103">작성자: [Brennan Conroy](https://github.com/BrennanConroy)</span><span class="sxs-lookup"><span data-stu-id="9cdb3-103">By [Brennan Conroy](https://github.com/BrennanConroy)</span></span>

<span data-ttu-id="9cdb3-104">ASP.NET Core SignalR 서버 메서드의 스트리밍 반환 값을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9cdb3-104">ASP.NET Core SignalR supports streaming return values of server methods.</span></span> <span data-ttu-id="9cdb3-105">시간별 데이터 조각에 제공 하는 위치 하는 시나리오에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cdb3-105">This is useful for scenarios where fragments of data will come in over time.</span></span> <span data-ttu-id="9cdb3-106">반환 값을 클라이언트에 스트리밍할 때 각 조각은 클라이언트에 즉시 전송 되기 모든 데이터를 사용할 수 있게 될 때까지 대기 하는 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cdb3-106">When a return value is streamed to the client, each fragment is sent to the client as soon as it becomes available, rather than waiting for all the data to become available.</span></span>

<span data-ttu-id="9cdb3-107">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/streaming/sample) ([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="9cdb3-107">[View or download sample code](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/streaming/sample) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="set-up-the-hub"></a><span data-ttu-id="9cdb3-108">허브 설정</span><span class="sxs-lookup"><span data-stu-id="9cdb3-108">Set up the hub</span></span>

<span data-ttu-id="9cdb3-109">반환 될 때 자동으로 허브 메서드를 스트리밍 허브 메서드를 됩니다는 `ChannelReader<T>` 또는 `Task<ChannelReader<T>>`합니다.</span><span class="sxs-lookup"><span data-stu-id="9cdb3-109">A hub method automatically becomes a streaming hub method when it returns a `ChannelReader<T>` or a `Task<ChannelReader<T>>`.</span></span> <span data-ttu-id="9cdb3-110">다음은 스트리밍 데이터를 클라이언트의 기본 사항을 보여 주는 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="9cdb3-110">Below is a sample that shows the basics of streaming data to the client.</span></span> <span data-ttu-id="9cdb3-111">개체를 쓸 때마다는 `ChannelReader` 해당 개체는 클라이언트에 즉시 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cdb3-111">Whenever an object is written to the `ChannelReader` that object is immediately sent to the client.</span></span> <span data-ttu-id="9cdb3-112">끝에 `ChannelReader` 스트림이 클라이언트에 게 알리는 완료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cdb3-112">At the end, the `ChannelReader` is completed to tell the client the stream is closed.</span></span>

> [!NOTE]
> <span data-ttu-id="9cdb3-113">쓸 합니다 `ChannelReader` 백그라운드 스레드 및 반환에는 `ChannelReader` 최대한 빨리 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cdb3-113">Write to the `ChannelReader` on a background thread and return the `ChannelReader` as soon as possible.</span></span> <span data-ttu-id="9cdb3-114">다른 허브 호출 될 때까지 차단 됩니다는 `ChannelReader` 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cdb3-114">Other hub invocations will be blocked until a `ChannelReader` is returned.</span></span>

[!code-csharp[Streaming hub method](streaming/sample/Hubs/StreamHub.cs?range=10-34)]

## <a name="net-client"></a><span data-ttu-id="9cdb3-115">.NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="9cdb3-115">.NET client</span></span>

<span data-ttu-id="9cdb3-116">합니다 `StreamAsChannelAsync` 메서드를 `HubConnection` 스트리밍 메서드를 호출 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cdb3-116">The `StreamAsChannelAsync` method on `HubConnection` is used to invoke a streaming method.</span></span> <span data-ttu-id="9cdb3-117">허브 메서드 이름 및 허브 메서드를 정의 하는 인수를 전달 `StreamAsChannelAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="9cdb3-117">Pass the hub method name, and arguments defined in the hub method to `StreamAsChannelAsync`.</span></span> <span data-ttu-id="9cdb3-118">제네릭 매개 변수를 `StreamAsChannelAsync<T>` 스트리밍 메서드에 의해 반환 된 개체의 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cdb3-118">The generic parameter on `StreamAsChannelAsync<T>` specifies the type of objects returned by the streaming method.</span></span> <span data-ttu-id="9cdb3-119">`ChannelReader<T>` stream 호출에서 반환 되 고 클라이언트에서 스트림을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9cdb3-119">A `ChannelReader<T>` is returned from the stream invocation, and represents the stream on the client.</span></span> <span data-ttu-id="9cdb3-120">반복에 일반적인 패턴은 데이터를 읽으려면 `WaitToReadAsync` 호출 `TryRead` 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cdb3-120">To read data, a common pattern is to loop over `WaitToReadAsync` and call `TryRead` when data is available.</span></span> <span data-ttu-id="9cdb3-121">루프는 스트림이 서버에 의해 닫힌 또는 취소 토큰을 전달할 때 끝납니다 `StreamAsChannelAsync` 취소 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cdb3-121">The loop will end when the stream has been closed by the server, or the cancellation token passed to `StreamAsChannelAsync` is canceled.</span></span>

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

## <a name="javascript-client"></a><span data-ttu-id="9cdb3-122">JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="9cdb3-122">JavaScript client</span></span>

<span data-ttu-id="9cdb3-123">JavaScript 클라이언트를 사용 하 여 허브에서 스트리밍 메서드를 호출할 `connection.stream`합니다.</span><span class="sxs-lookup"><span data-stu-id="9cdb3-123">JavaScript clients call streaming methods on hubs by using `connection.stream`.</span></span> <span data-ttu-id="9cdb3-124">이 `stream` 메서드는 두 가지 인수를 전달 받습니다.</span><span class="sxs-lookup"><span data-stu-id="9cdb3-124">The `stream` method accepts two arguments:</span></span>

* <span data-ttu-id="9cdb3-125">허브 메서드의 이름.</span><span class="sxs-lookup"><span data-stu-id="9cdb3-125">The name of the hub method.</span></span> <span data-ttu-id="9cdb3-126">다음 예제에서는 허브 메서드 이름은 `Counter`합니다.</span><span class="sxs-lookup"><span data-stu-id="9cdb3-126">In the following example, the hub method name is `Counter`.</span></span>
* <span data-ttu-id="9cdb3-127">허브 메서드에 정의 된 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="9cdb3-127">Arguments defined in the hub method.</span></span> <span data-ttu-id="9cdb3-128">인수는 다음 예에서: 스트림 항목을 받으려면 및 스트림 항목 사이의 지연 시간 수의 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="9cdb3-128">In the following example, the arguments are: a count for the number of stream items to receive, and the delay between stream items.</span></span>

<span data-ttu-id="9cdb3-129">`connection.stream` 반환 합니다는 `IStreamResult` 포함 하는 한 `subscribe` 메서드.</span><span class="sxs-lookup"><span data-stu-id="9cdb3-129">`connection.stream` returns an `IStreamResult` which contains a `subscribe` method.</span></span> <span data-ttu-id="9cdb3-130">전달는 `IStreamSubscriber` 를 `subscribe` 설정 합니다 `next`, `error`, 및 `complete` 에서 알림을 받는 콜백을 `stream` 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cdb3-130">Pass an `IStreamSubscriber` to `subscribe` and set the `next`, `error`, and `complete` callbacks to get notifications from the `stream` invocation.</span></span>

[!code-javascript[Streaming javascript](streaming/sample/wwwroot/js/stream.js?range=19-36)]

<span data-ttu-id="9cdb3-131">클라이언트에서 스트림에 호출 합니다 `dispose` 메서드를 `ISubscription` 에서 반환 되는 `subscribe` 메서드.</span><span class="sxs-lookup"><span data-stu-id="9cdb3-131">To end the stream from the client, call the `dispose` method on the `ISubscription` that is returned from the `subscribe` method.</span></span>

## <a name="related-resources"></a><span data-ttu-id="9cdb3-132">관련 자료</span><span class="sxs-lookup"><span data-stu-id="9cdb3-132">Related resources</span></span>

* [<span data-ttu-id="9cdb3-133">허브</span><span class="sxs-lookup"><span data-stu-id="9cdb3-133">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="9cdb3-134">.NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="9cdb3-134">.NET client</span></span>](xref:signalr/dotnet-client)
* [<span data-ttu-id="9cdb3-135">JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="9cdb3-135">JavaScript client</span></span>](xref:signalr/javascript-client)
* [<span data-ttu-id="9cdb3-136">Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="9cdb3-136">Publish to Azure</span></span>](xref:signalr/publish-to-azure-web-app)
