---
title: ASP.NET Core SignalR의 스트리밍 사용
author: tdykstra
description: ''
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 06/07/2018
uid: signalr/streaming
ms.openlocfilehash: 3ae9b83d60019eaa3196f35645bf9b4b03f6d8c6
ms.sourcegitcommit: 4bdf7703aed86ebd56b9b4bae9ad5700002af32d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2018
ms.locfileid: "49325642"
---
# <a name="use-streaming-in-aspnet-core-signalr"></a>ASP.NET Core SignalR의 스트리밍 사용

[브 레 넌 Conroy](https://github.com/BrennanConroy)

ASP.NET Core SignalR 서버 메서드의 스트리밍 반환 값을 지원합니다. 시간별 데이터 조각에 제공 하는 위치 하는 시나리오에 유용 합니다. 반환 값을 클라이언트에 스트리밍할 때 각 조각은 클라이언트에 즉시 전송 되기 모든 데이터를 사용할 수 있게 될 때까지 대기 하는 대신 사용할 수 있습니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/streaming/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="set-up-the-hub"></a>허브 설정

반환 될 때 자동으로 허브 메서드를 스트리밍 허브 메서드를 됩니다는 `ChannelReader<T>` 또는 `Task<ChannelReader<T>>`합니다. 다음은 스트리밍 데이터를 클라이언트의 기본 사항을 보여 주는 샘플입니다. 개체를 쓸 때마다는 `ChannelReader` 해당 개체는 클라이언트에 즉시 전송 됩니다. 끝에 `ChannelReader` 스트림이 클라이언트에 게 알리는 완료 됩니다.

> [!NOTE]
> 쓸 합니다 `ChannelReader` 백그라운드 스레드 및 반환에는 `ChannelReader` 최대한 빨리 합니다. 다른 허브 호출 될 때까지 차단 됩니다는 `ChannelReader` 반환 됩니다.

[!code-csharp[Streaming hub method](streaming/sample/Hubs/StreamHub.cs?range=10-34)]

## <a name="net-client"></a>.NET 클라이언트

합니다 `StreamAsChannelAsync` 메서드를 `HubConnection` 스트리밍 메서드를 호출 하는 데 사용 됩니다. 허브 메서드 이름 및 허브 메서드를 정의 하는 인수를 전달 `StreamAsChannelAsync`합니다. 제네릭 매개 변수를 `StreamAsChannelAsync<T>` 스트리밍 메서드에 의해 반환 된 개체의 형식을 지정 합니다. `ChannelReader<T>` stream 호출에서 반환 되 고 클라이언트에서 스트림을 나타냅니다. 반복에 일반적인 패턴은 데이터를 읽으려면 `WaitToReadAsync` 호출 `TryRead` 데이터를 사용할 수 있습니다. 루프는 스트림이 서버에 의해 닫힌 또는 취소 토큰을 전달할 때 끝납니다 `StreamAsChannelAsync` 취소 됩니다.

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

JavaScript 클라이언트를 사용 하 여 허브에서 스트리밍 메서드를 호출할 `connection.stream`합니다. `stream` 메서드는 두 인수를 허용 합니다.

* 허브 메서드의 이름입니다. 다음 예제에서는 허브 메서드 이름은 `Counter`합니다.
* 허브 메서드에 정의 된 인수입니다. 인수는 다음 예에서: 스트림 항목을 받으려면 및 스트림 항목 사이의 지연 시간 수의 개수입니다.

`connection.stream` 반환 합니다는 `IStreamResult` 포함 하는 한 `subscribe` 메서드. 전달는 `IStreamSubscriber` 를 `subscribe` 설정 합니다 `next`, `error`, 및 `complete` 에서 알림을 받는 콜백을 `stream` 호출 합니다.

[!code-javascript[Streaming javascript](streaming/sample/wwwroot/js/stream.js?range=19-36)]

클라이언트에서 스트림에 호출 합니다 `dispose` 메서드를 `ISubscription` 에서 반환 되는 `subscribe` 메서드.

## <a name="related-resources"></a>관련 참고 자료

* [허브](xref:signalr/hubs)
* [.NET 클라이언트](xref:signalr/dotnet-client)
* [JavaScript 클라이언트](xref:signalr/javascript-client)
* [Azure에 게시](xref:signalr/publish-to-azure-web-app)
