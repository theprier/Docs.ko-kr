---
title: SignalR에서 MessagePack 허브 프로토콜을 사용 하 여 ASP.NET Core에 대 한
author: rachelappel
description: ASP.NET Core signalr 허브 MessagePack 프로토콜을 추가 합니다.
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 06/04/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: signalr/messagepackhubprotocol
ms.openlocfilehash: b6c33c4da47a19d67bffbaf84f54d59013edadbe
ms.sourcegitcommit: 63fb07fb3f71b32daf2c9466e132f2e7cc617163
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/10/2018
ms.locfileid: "35252485"
---
# <a name="use-messagepack-hub-protocol-in-signalr-for-aspnet-core"></a>SignalR에서 MessagePack 허브 프로토콜을 사용 하 여 ASP.NET Core에 대 한

으로 [브 레 넌 Conroy](https://github.com/BrennanConroy)

이 문서에서는 독자가 가정에서 다루는 항목에 잘 알고 [시작](xref:signalr/get-started)합니다.

## <a name="what-is-messagepack"></a>MessagePack 란?

[MessagePack](https://msgpack.org/index.html) 이진 serialization 형식 신속 하 고 압축입니다. 경우에 비해 더 작은 메시지를 만들기 때문에 성능 및 대역폭은 문제가 [JSON](https://www.json.org/)합니다. 이진 형식 이므로 확인할 때 네트워크 추적 및 로그 바이트 MessagePack 파서 통과 하지 않는 한 메시지를 읽을 수 없습니다. SignalR은 MessagePack 형식에 대 한 기본적으로 지원 하 고 사용 하 여 클라이언트와 서버에 대 한 Api를 제공 합니다.

## <a name="configure-messagepack-on-the-server"></a>서버에서 MessagePack 구성

서버에서 MessagePack 허브 프로토콜을 사용 하도록 설정 하려면 설치는 `Microsoft.AspNetCore.SignalR.Protocols.MessagePack` 앱의 패키지입니다. Startup.cs 파일에서 추가 `AddMessagePackProtocol` 에 `AddSignalR` 서버의 MessagePack 지원을 사용 하도록 호출 합니다.

> [!NOTE]
> JSON은 기본적으로 사용 됩니다. MessagePack를 추가 하는 JSON 및 MessagePack 클라이언트에 대 한 지원을 수 있습니다.

```csharp
services.AddSignalR()
    .AddMessagePackProtocol();
```

MessagePack 여 데이터에는 서식 지정 방법을 사용자 지정 하려면 `AddMessagePackProtocol` 옵션을 구성 하기 위한 대리자를 사용 합니다. 해당 대리자에는 `FormatterResolvers` MessagePack 직렬화 옵션을 구성 하려면 속성을 사용할 수 있습니다. 해결 프로그램의 작동 방식에 대 한 자세한 내용은 MessagePack 라이브러리 방문 [MessagePack CSharp](https://github.com/neuecc/MessagePack-CSharp)합니다. 특성을 처리 하는 방법을 정의 하는 serialize 할 개체에 사용할 수 있습니다.

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

## <a name="configure-messagepack-on-the-client"></a>클라이언트에서 MessagePack을 구성 합니다.

### <a name="net-client"></a>.NET 클라이언트

.NET 클라이언트에서 MessagePack를 사용 하도록 설정 하려면 설치는 `Microsoft.AspNetCore.SignalR.Protocols.MessagePack` 패키지 및 호출 `AddMessagePackProtocol` 에 `HubConnectionBuilder`합니다.

```csharp
var hubConnection = new HubConnectionBuilder()
                        .WithUrl("/chatHub")
                        .AddMessagePackProtocol()
                        .Build();
```

> [!NOTE]
> 이 `AddMessagePackProtocol` 호출 서버와 마찬가지로 옵션을 구성 하기 위한 대리자를 사용 합니다.

### <a name="javascript-client"></a>JavaScript 클라이언트

Javascript 클라이언트에 대 한 MessagePack 지원에서 제공 되는 `@aspnet/signalr-protocol-msgpack` NPM 패키지 합니다.

```console
npm install @aspnet/signalr-protocol-msgpack
```

Npm 패키지를 설치한 후 모듈 JavaScript 모듈 로더를 통해 직접 사용 하거나 수 참조 하 여 브라우저에 가져올는 *node_modules\\ @aspnet\signalr-protocol-msgpack\dist\browser\signalr-protocol-msgpack.js*  파일입니다. 브라우저에서는 `msgpack5` 라이브러리 참조 해야 합니다. 사용 하 여 한 `<script>` 태그에 대 한 참조를 만듭니다. 라이브러리에서 찾을 수 있습니다 *node_modules\msgpack5\dist\msgpack5.js*합니다.

> [!NOTE]
> 사용 하는 경우는 `<script>` 요소 순서는 중요 합니다. 경우 *signalr-프로토콜-msgpack.js* 하기 전에 참조 *msgpack5.js*, MessagePack를 사용 하 여 연결 하려고 할 때 오류가 발생 합니다. *signalr.js* 가 필요 하기 전에 *signalr-프로토콜-msgpack.js*합니다.

```html
<script src="~/lib/signalr/signalr.js"></script>
<script src="~/lib/msgpack5/msgpack5.js"></script>
<script src="~/lib/signalr/signalr-protocol-msgpack.js"></script>
```

추가 `.withHubProtocol(new signalR.protocols.msgpack.MessagePackHubProtocol())` 에 `HubConnectionBuilder` 는 서버에 연결할 때 MessagePack 프로토콜을 사용 하도록 클라이언트를 구성 합니다.

```javascript
const connection = new signalR.HubConnectionBuilder()
    .withUrl("/chatHub")
    .withHubProtocol(new signalR.protocols.msgpack.MessagePackHubProtocol())
    .build();
```

> [!NOTE]
> 이때 JavaScript 클라이언트에서 MessagePack 프로토콜에 대 한 아무런 구성 옵션이 있습니다.

## <a name="related-resources"></a>관련 참고 자료

* [시작](xref:signalr/get-started)
* [.NET 클라이언트](xref:signalr/dotnet-client)
* [JavaScript 클라이언트](xref:signalr/javascript-client)
