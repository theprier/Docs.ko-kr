---
title: ASP.NET Core SignalR에서 스트리밍을 사용합니다
author: rachelappel
description: ''
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 06/07/2018
uid: signalr/streaming
ms.openlocfilehash: ae0e733dddfb48db07d77ea73f4673cf8f783b88
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36275852"
---
# <a name="use-streaming-in-aspnet-core-signalr"></a>ASP.NET Core SignalR에서 스트리밍을 사용합니다

으로 [브 레 넌 Conroy](https://github.com/BrennanConroy)

ASP.NET Core SignalR 서버 메서드의 스트리밍 반환 값을 지원 합니다. 데이터 조각에는 이때 시간이 지남에 따라 시나리오에 유용 합니다. 클라이언트에 스트림 되는 값을 반환 하는 경우 각 조각은 보내집니다 클라이언트에 있게 되는 즉시 모든 데이터를 사용할 수 있을 때 가지 기다리는 대신 사용할 수 있습니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/streaming/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="set-up-the-hub"></a>허브를 설정

반환 될 때 자동으로 스트리밍 허브 메서드를 됩니다 허브 메서드는 `ChannelReader<T>` 또는 `Task<ChannelReader<T>>`합니다. 다음은 스트리밍 데이터를 클라이언트의 기본 사항을 보여 주는 샘플입니다. 개체에 기록 되는 때마다는 `ChannelReader` 클라이언트에의 한 개체를 즉시 전송 됩니다. 마지막으로 `ChannelReader` 스트림이 닫혀 클라이언트에 게 알리는를 완료 합니다.

> [!NOTE]
> 에 쓰기는 `ChannelReader` 백그라운드 스레드 및 반환에는 `ChannelReader` 최대한 빨리 합니다. 다른 허브 호출 될 때까지 차단 되는 `ChannelReader` 반환 됩니다.

[!code-csharp[Streaming hub method](streaming/sample/hubs/streamhub.cs?range=10-34)]

## <a name="net-client"></a>.NET 클라이언트

`StreamAsChannelAsync` 메서드를 `HubConnection` 스트리밍 메서드를 호출 하는 데 사용 됩니다. 허브 메서드 이름 및 허브 메서드를 정의 된 인수를 전달 `StreamAsChannelAsync`합니다. 제네릭 매개 변수를 `StreamAsChannelAsync<T>` 스트리밍 메서드에 의해 반환 되는 개체의 유형을 지정 합니다. A `ChannelReader<T>` 스트림 호출에서 반환 되 고 클라이언트에서 스트림을 나타냅니다. 데이터를 읽을 수는 일반적인 패턴은 루프를 `WaitToReadAsync` 호출 `TryRead` 데이터를 사용할 수 있습니다. 스트림이 서버에 의해 닫힌 또는 취소 토큰을 전달 하는 경우 종료 됩니다 `StreamAsChannelAsync` 취소 됩니다.

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

## <a name="javascript-client"></a>JavaScript 클라이언트

JavaScript 클라이언트 허브에서 사용 하 여 스트리밍 메서드를 호출 `connection.stream`합니다. `stream` 메서드는 두 인수를 허용 합니다.

* 허브 메서드의 이름입니다. 다음 예에서는 허브 메서드 이름은 `Counter`합니다.
* 허브 메서드에 정의 된 인수입니다. 인수는 다음 예에서: 스트림 항목을 받으려면 및 스트림 항목 사이의 지연의 수에 대 한 수입니다.

`connection.stream` 반환 된 `IStreamResult` 포함 하는 `subscribe` 메서드. 전달는 `IStreamSubscriber` 를 `subscribe` 설정 하 고는 `next`, `error`, 및 `complete` 에서 알림을 받을 콜백을 `stream` 호출 합니다.

[!code-javascript[Streaming javascript](streaming/sample/wwwroot/js/stream.js?range=19-36)]

클라이언트 호출에서 스트림을 종료 하는 `dispose` 에서 메서드는 `ISubscription` 에서 반환 되는 `subscribe` 메서드.

## <a name="related-resources"></a>관련 참고 자료

* [허브](xref:signalr/hubs)
* [.NET 클라이언트](xref:signalr/dotnet-client)
* [JavaScript 클라이언트](xref:signalr/javascript-client)
* [Azure에 게시](xref:signalr/publish-to-azure-web-app)