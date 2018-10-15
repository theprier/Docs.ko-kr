---
title: SignalR에서 MessagePack Hub 프로토콜을 사용 하 여 ASP.NET Core에 대 한
author: tdykstra
description: ASP.NET Core signalr MessagePack Hub 프로토콜을 추가 합니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 06/04/2018
uid: signalr/messagepackhubprotocol
ms.openlocfilehash: 0874afc5493eca5d43dfde30bb28aedc1f193744
ms.sourcegitcommit: 4bdf7703aed86ebd56b9b4bae9ad5700002af32d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2018
ms.locfileid: "49325583"
---
# <a name="use-messagepack-hub-protocol-in-signalr-for-aspnet-core"></a>SignalR에서 MessagePack Hub 프로토콜을 사용 하 여 ASP.NET Core에 대 한

[브 레 넌 Conroy](https://github.com/BrennanConroy)

이 문서에 설명 된 항목을 알고 있다고 가정 [시작](xref:tutorials/signalr)합니다.

## <a name="what-is-messagepack"></a>MessagePack 란?

[MessagePack](https://msgpack.org/index.html) 은 빠르고 compact는 이진 serialization 형식입니다. 에 비해 크기가 작은 메시지를 만들기 때문에 성능 및 대역폭은 중요 한 경우에 유용 [JSON](https://www.json.org/)합니다. 이진 형식 이므로 바이트 MessagePack 파서를 통과 하지 않는 한 네트워크 추적 및 로그를 조사 하는 경우 메시지를 읽을 수 없습니다. SignalR은 MessagePack 형식에 대 한 기본 제공 지원 하 고 사용 하 여 클라이언트와 서버에 대 한 Api를 제공 합니다.

## <a name="configure-messagepack-on-the-server"></a>MessagePack 서버의 구성

서버에서 MessagePack Hub 프로토콜을 사용 하려면 설치 된 `Microsoft.AspNetCore.SignalR.Protocols.MessagePack` 앱의 패키지입니다. Startup.cs 파일에 추가 `AddMessagePackProtocol` 에 `AddSignalR` 서버의 MessagePack 지원을 사용 하도록 호출 합니다.

> [!NOTE]
> JSON은 기본적으로 사용 됩니다. MessagePack 추가 JSON 및 MessagePack 클라이언트용 지원할 수 있습니다.

```csharp
services.AddSignalR()
    .AddMessagePackProtocol();
```

MessagePack 데이터에는 서식을 지정 하는 방법을 사용자 지정 하려면 `AddMessagePackProtocol` 옵션을 구성 하는 것에 대 한 대리자를 사용 합니다. 해당 대리자에서는 `FormatterResolvers` MessagePack serialization 옵션을 구성 하려면 속성을 사용할 수 있습니다. 해결 프로그램은 어떻게 작동 하는지에 대 한 자세한 내용은 MessagePack 라이브러리를 방문 [MessagePack CSharp](https://github.com/neuecc/MessagePack-CSharp)합니다. 특성을 처리 하는 방법을 정의로 직렬화 할 개체에 사용할 수 있습니다.

```csharp
services.AddSignalR()
    .AddMessagePackProtocol(options =>
    {
        options.FormatterResolvers = new List<MessagePack.IFormatterResolver>()
        {
            MessagePack.Resolvers.StandardResolver.Instance
        };
    });
```

## <a name="configure-messagepack-on-the-client"></a>클라이언트에서 MessagePack 구성

> [!NOTE]
> 지원 되는 클라이언트에 대 한 JSON이 기본적으로 사용 됩니다. 클라이언트에서는 단일 프로토콜을 지원할 수 있습니다. 프로토콜 구성 MessagePack 지원 바뀝니다 모든 이전에 추가 합니다.

### <a name="net-client"></a>.NET 클라이언트

MessagePack.NET 클라이언트에서를 설치 합니다 `Microsoft.AspNetCore.SignalR.Protocols.MessagePack` 패키지 및 호출 `AddMessagePackProtocol` 에서 `HubConnectionBuilder`합니다.

```csharp
var hubConnection = new HubConnectionBuilder()
                        .WithUrl("/chatHub")
                        .AddMessagePackProtocol()
                        .Build();
```

> [!NOTE]
> 이 `AddMessagePackProtocol` 서버와 마찬가지로 옵션을 구성 하는 데는 대리자를 호출 합니다.

### <a name="javascript-client"></a>JavaScript 클라이언트

Javascript 클라이언트에 대 한 지원은 MessagePack가 제공 된 `@aspnet/signalr-protocol-msgpack` NPM 패키지 합니다.

```console
npm install @aspnet/signalr-protocol-msgpack
```

Npm 패키지를 설치한 후 모듈을 사용 하거나 수 있습니다 JavaScript 모듈 로더를 통해 직접 참조 하 여 브라우저에 가져온 합니다 *node_modules\\@aspnet\signalr-protocol-msgpack\dist\browser\signalr-protocol-msgpack.js* 파일입니다. 브라우저에서을 `msgpack5` 라이브러리 참조 되어야 합니다. 사용 된 `<script>` 대 한 참조를 만듭니다. 라이브러리에서 찾을 수 있습니다 *node_modules\msgpack5\dist\msgpack5.js*합니다.

> [!NOTE]
> 사용 하는 경우는 `<script>` 요소 순서는 중요 합니다. 하는 경우 *signalr-프로토콜-msgpack.js* 하기 전에 참조 *msgpack5.js*, MessagePack를 사용 하 여 연결 하려고 할 때 오류가 발생 합니다. *signalr.js* 전에 필요 *signalr-프로토콜-msgpack.js*합니다.

```html
<script src="~/lib/signalr/signalr.js"></script>
<script src="~/lib/msgpack5/msgpack5.js"></script>
<script src="~/lib/signalr/signalr-protocol-msgpack.js"></script>
```

추가 `.withHubProtocol(new signalR.protocols.msgpack.MessagePackHubProtocol())` 에 `HubConnectionBuilder` 서버에 연결할 때 MessagePack 프로토콜을 사용 하도록 클라이언트를 구성 합니다.

```javascript
const connection = new signalR.HubConnectionBuilder()
    .withUrl("/chatHub")
    .withHubProtocol(new signalR.protocols.msgpack.MessagePackHubProtocol())
    .build();
```

> [!NOTE]
> 이때 JavaScript 클라이언트에서 MessagePack 프로토콜에 대 한 아무런 구성 옵션이 있습니다.

## <a name="related-resources"></a>관련 참고 자료

* [시작](xref:tutorials/signalr)
* [.NET 클라이언트](xref:signalr/dotnet-client)
* [JavaScript 클라이언트](xref:signalr/javascript-client)
