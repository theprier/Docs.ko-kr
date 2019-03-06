---
title: ASP.NET Core SignalR에서 스트리밍 사용
author: bradygaster
description: 서버 hub 메서드에서 스트림의 값을 반환 하 고.NET 및 JavaScript 클라이언트를 사용 하 여 스트림을 사용 하는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: bradyg
ms.custom: mvc
ms.date: 11/14/2018
uid: signalr/streaming
ms.openlocfilehash: fb7183f7189d62c181f69ffdb170e3da25612919
ms.sourcegitcommit: 036d4b03fd86ca5bb378198e29ecf2704257f7b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57345589"
---
# <a name="use-streaming-in-aspnet-core-signalr"></a>ASP.NET Core SignalR에서 스트리밍 사용

작성자: [Brennan Conroy](https://github.com/BrennanConroy)

ASP.NET Core SignalR은 서버 메서드의 스트리밍 반환 값을 지원합니다. 이 기능은 지속적으로 데이터 조각이 전달되는 시나리오에 유용합니다. 클라이언트에 반환 값을 스트리밍할 때 모든 조각이 사용 가능할 때까지 기다리는 대신 사용 가능한 즉시 각 조각을 클라이언트로 전송합니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/streaming/sample) ([다운로드 방법](xref:index#how-to-download-a-sample))

## <a name="set-up-the-hub"></a>허브 설정

::: moniker range=">= aspnetcore-3.0"

반환 될 때 자동으로 허브 메서드를 스트리밍 허브 메서드를 됩니다는 `ChannelReader<T>`, `IAsyncEnumerable<T>`를 `Task<ChannelReader<T>>`, 또는 `Task<IAsyncEnumerable<T>>`합니다.

::: moniker-end

::: moniker range="< aspnetcore-3.0"

`ChannelReader<T>` 또는 `Task<ChannelReader<T>>`를 반환하는 허브 메서드는 자동으로 스트리밍 허브 메서드로 간주됩니다.

::: moniker-end

::: moniker range=">= aspnetcore-3.0"

ASP.NET Core 3.0 이상에서는 허브 메서드를 스트리밍 반환할 수 있습니다 `IAsyncEnumerable<T>` 외에 `ChannelReader<T>`합니다. 반환 하는 가장 간단한 방법은 `IAsyncEnumerable<T>` 다음 샘플 에서처럼 허브 메서드를 비동기 반복기 메서드 만들기가 있습니다. 허브 비동기 반복기 메서드에 사용할 수는 `CancellationToken` 스트림에서 클라이언트 등록을 취소 하는 경우 트리거되는 매개 변수입니다. 쉽게 비동기 반복기 메서드 반환 하지 않는 등의 채널을 사용 하 여 일반적인 문제를 방지 합니다 `ChannelReader` 충분히 이른 메서드를 완료 하지 않고 종료 또는 `ChannelWriter`합니다.

[!INCLUDE[](~/includes/csharp-8-required.md)]

[!code-csharp[Streaming hub async iterator method](streaming/sample/Hubs/AsyncEnumerableHub.cs?name=snippet_AsyncIterator)]

::: moniker-end

다음 샘플에서는 스트리밍 채널을 사용 하 여 클라이언트에는 데이터의 기본 사항을 보여 줍니다. 개체가 `ChannelWriter`에 쓰여질 때마다 해당 개체는 클라이언트로 즉시 전송됩니다. 마지막으로 `ChannelWriter`가 완료되어 스트림이 닫혔음을 클라이언트에 알려줍니다.

> [!NOTE]
> * 백그라운드 스레드에서 `ChannelWriter`에 쓰고 최대한 빨리 `ChannelReader`를 반환하십시오. `ChannelReader`가 반환될 때까지 다른 허브 호출들은 차단됩니다.
> * 논리를 래핑하는 `try ... catch` 완료를 `Channel` 메서드 호출이 제대로 완료 하 고 catch 되도록 허브 외부 catch에 합니다.

::: moniker range="= aspnetcore-2.1"

[!code-csharp[Streaming hub method](streaming/sample/Hubs/StreamHub.aspnetcore21.cs?name=snippet1)]

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

[!code-csharp[Streaming hub method](streaming/sample/Hubs/StreamHub.cs?name=snippet1)]

ASP.NET Core 2.2 이상에서는 허브 메서드를 스트리밍 허용할 수는 `CancellationToken` 스트림에서 클라이언트 등록을 취소 하는 경우 트리거되는 매개 변수입니다. 이 토큰을 사용 하 여 서버 작업을 중지 및 스트림 종료 되기 전에 클라이언트 연결이 끊어지면 리소스를 해제 합니다.

::: moniker-end

## <a name="net-client"></a>.NET 클라이언트

스트리밍 메서드를 호출하기 위해 `HubConnection`의 `StreamAsChannelAsync` 메서드가 사용됩니다. 허브 메서드 이름과 허브 메서드에 정의된 인수를 `StreamAsChannelAsync`에 전달합니다. `StreamAsChannelAsync<T>`의 제네릭 매개 변수는 스트리밍 메서드에서 반환되는 개체의 형식을 지정합니다. 스트림 호출에서는 `ChannelReader<T>`가 반환되며 이는 클라이언트에서 스트림을 나타냅니다. 데이터를 읽기 위해서는 데이터가 사용 가능할 때 `WaitToReadAsync` 및 `TryRead` 호출을 반복하는 패턴이 일반적입니다. 서버에 의해 스트림이 닫히거나 `StreamAsChannelAsync`에 전달된 취소 토큰이 취소되면 루프가 끝납니다.

::: moniker range=">= aspnetcore-2.2"

```csharp
// Call "Cancel" on this CancellationTokenSource to send a cancellation message to
// the server, which will trigger the corresponding token in the hub method.
var cancellationTokenSource = new CancellationTokenSource();
var channel = await hubConnection.StreamAsChannelAsync<int>(
    "Counter", 10, 500, cancellationTokenSource.Token);

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

::: moniker-end

::: moniker range="= aspnetcore-2.1"

```csharp
var channel = await hubConnection
    .StreamAsChannelAsync<int>("Counter", 10, 500, CancellationToken.None);

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

::: moniker-end

## <a name="javascript-client"></a>JavaScript 클라이언트

JavaScript 클라이언트는 `connection.stream`을 사용하여 허브의 스트리밍 메서드를 호출합니다. 이 `stream` 메서드는 두 가지 인수를 전달받습니다.

* 허브 메서드의 이름. 다음 예제에서 허브 메서드 이름은 `Counter`입니다.
* 허브 메서드에 정의된 인수. 다음 예에서 인수는 수신할 스트림 항목의 갯수에 대한 카운트 및 스트림 항목 사이의 지연 시간입니다.

`connection.stream`은 `subscribe` 메서드가 포함된 `IStreamResult`를 반환합니다. `IStreamSubscriber`를 `subscribe`에 전달하고 `stream` 호출에서 알림을 받을 `next`, `error`및 `complete` 콜백을 설정합니다.

[!code-javascript[Streaming javascript](streaming/sample/wwwroot/js/stream.js?range=19-36)]

::: moniker range="= aspnetcore-2.1"

클라이언트에서 스트림을 끝내려면 `subscribe` 메서드에서 반환되는 `ISubscription`에서 `dispose` 메서드를 호출합니다.

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

클라이언트에서 스트림을 끝내려면 `subscribe` 메서드에서 반환되는 `ISubscription`에서 `dispose` 메서드를 호출합니다. 이 메서드는 호출을 `CancellationToken` (제공한 하나) 하는 경우에 허브 메서드의 매개 변수를 취소할 수 있습니다.

::: moniker-end

::: moniker range=">= aspnetcore-3.0"
## <a name="java-client"></a>Java 클라이언트
SignalR Java 클라이언트를 사용 하 여 `stream` 스트리밍 메서드를 호출 하는 방법입니다. 3 개 이상의 인수를 허용 합니다.

* 스트림 아이템의 예상된 형식 
* 허브 메서드의 이름.
* 허브 메서드에 정의된 인수. 

```java
hubConnection.stream(String.class, "ExampleStreamingHubMethod", "Arg1")
    .subscribe(
        (item) -> {/* Define your onNext handler here. */ },
        (error) -> {/* Define your onError handler here. */},
        () -> {/* Define your onCompleted handler here. */});
```
합니다 `stream` 메서드를 `HubConnection` 스트림 항목 형식의 관찰 가능 개체를 반환 합니다. Observable 형식 `subscribe` 메서드를 정의할 수는 프로그램 `onNext`를 `onError` 및 `onCompleted` 처리기입니다.

::: moniker-end

## <a name="related-resources"></a>관련 참고 자료

* [허브](xref:signalr/hubs)
* [.NET 클라이언트](xref:signalr/dotnet-client)
* [JavaScript 클라이언트](xref:signalr/javascript-client)
* [Azure에 게시](xref:signalr/publish-to-azure-web-app)
