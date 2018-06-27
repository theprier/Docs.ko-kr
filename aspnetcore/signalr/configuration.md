---
title: ASP.NET SignalR Core 구성
author: rachelappel
description: ASP.NET Core SignalR 응용 프로그램을 구성 하는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 06/30/2018
uid: signalr/configuration
ms.openlocfilehash: 167b8828efd093d755aeb1c91e080dbd22b5d485
ms.sourcegitcommit: 356c8d394aaf384c834e9c90cabab43bfe36e063
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2018
ms.locfileid: "36961989"
---
# <a name="aspnet-core-signalr-configuration"></a>ASP.NET SignalR Core 구성

## <a name="jsonmessagepack-serialization-options"></a>JSON/MessagePack 직렬화 옵션

ASP.NET Core SignalR 메시지 인코딩에 대 한 두 프로토콜을 지원: [JSON](https://www.json.org/) 및 [MessagePack](https://msgpack.org/index.html)합니다. 각 프로토콜에 serialization 구성 옵션이 있습니다.

JSON serialization을 사용 하 여 서버에 구성할 수는 [ `AddJsonProtocol` ](/dotnet/api/microsoft.extensions.dependencyinjection.jsonprotocoldependencyinjectionextensions.addjsonprotocol) 뒤에 추가할 수 있는 확장 메서드를 [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr) 에 프로그램 `Startup.ConfigureServices` 메서드. `AddJsonProtocol` 메서드는 수신 하는 대리자는 `options` 개체입니다. [ `PayloadSerializerSettings` ](/dotnet/api/microsoft.aspnetcore.signalr.jsonhubprotocoloptions.payloadserializersettings) 해당 개체의 속성은 한 JSON.NET `JsonSerializerSettings` serialization의 인수를 구성 하 고 값을 반환 하는 데 사용할 수 있습니다. 참조는 [JSON.NET 설명서](https://www.newtonsoft.com/json/help/html/Introduction.htm) 내용을 확인 합니다.

예를 들어, "표시 방법이 PascalCase" 속성 이름은 기본 "camelCase" 이름 대신 사용 하는 serializer를 구성 하려면 다음 코드를 사용 합니다.

```csharp
services.AddSignalR()
    .AddJsonHubProtocol(options => {
        options.PayloadSerializerSettings.ContractResolver = 
        new DefaultContractResolver();
    });
```

동일한.NET 클라이언트에서 `AddJsonHubProtocol` 에 확장 메서드가 있는 [HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder)합니다. `Microsoft.Extensions.DependencyInjection` 확장 메서드를 해결 하려면 네임 스페이스를 가져와야 합니다.

```csharp
// At the top of the file:
using Microsoft.Extensions.DependencyInjection;

// When constructing your connection:
var connection = new HubConnectionBuilder()
.AddJsonHubProtocol(options => {
    options.PayloadSerializerSettings.ContractResolver = 
        new DefaultContractResolver();
});
```

> [!NOTE]
> 이 이번에는 JSON serialization JavaScript 클라이언트에서 구성 하는 것이 불가능 합니다.

### <a name="messagepack-serialization-options"></a>MessagePack 직렬화 옵션

대리자를 제공 하 여 MessagePack serialization을 구성할 수 있습니다는 [AddMessagePackProtocol](/dotnet/api/microsoft.extensions.dependencyinjection.msgpackprotocoldependencyinjectionextensions.addmessagepackprotocol) 호출 합니다. 참조 [MessagePack SignalR에서](xref:signalr/messagepackhubprotocol) 내용을 확인 합니다.

> [!NOTE]
> 이 이번에는 JavaScript 클라이언트에서 MessagePack serialization을 구성 하는 것이 불가능 합니다.

## <a name="configure-server-options"></a>서버 옵션 구성

다음 표에서 SignalR 허브를 구성 하기 위한 옵션을 설명 합니다.

| 옵션 | 설명 |
| ------ | ----------- |
| `HandshakeTimeout` | 클라이언트는이 시간 간격 내에서 초기 핸드셰이크 메시지를 보내지 않습니다, 연결이 닫혀 있습니다. |
| `KeepAliveInterval` | 이 간격 내에서 메시지를 전송 하는 작업 서버 하지 않은 경우 ping 메시지 연결을 유지 하려면 자동으로 전송 됩니다. |
| `SupportedProtocols` | 이 허브에서 지 원하는 프로토콜입니다. 기본적으로 서버에 등록 하는 모든 프로토콜을 사용할 수 있지만 프로토콜 개별 허브에 대 한 특정 프로토콜을 사용 하지 않도록 설정 하려면이 목록에서 제거할 수 있습니다. |
| `EnableDetailedErrors` | 경우 `true`, 자세한 허브 메서드에서 예외가 throw 되 면 클라이언트에 예외 메시지가 반환 됩니다. 기본값은 `false`이러한 예외 메시지에는 중요 한 정보가 포함 되어 있습니다. |

하는 옵션 대리자를 제공 하 여 모든 허브에 대 한 옵션을 구성할 수 있습니다는 `AddSignalR` 에서 호출 `Startup.ConfigureServices`합니다.

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddSignalR(hubOptions =>
    {
        hubOptions.EnableDetailedErrors = true;
        hubOptions.KeepAliveInterval = TimeSpan.FromMinutes(1);
    })
}
```

단일 허브에 대 한 옵션에 제공 된 전역 옵션 재정의 `AddSignalR` 를 사용 하 여 구성할 수 있습니다 및 [ `AddHubOptions<T>` ](/dotnet/api/microsoft.extensions.dependencyinjection.huboptionsdependencyinjectionextensions.addhuboptions):

```csharp
services.AddSignalR().AddHubOptions<MyHub>(options =>
{
    options.EnableDetailedErrors = true;
}
```

사용 하 여 `HttpConnectionDispatcherOptions` 전송 및 메모리 버퍼 관리와 관련 된 고급 설정을 구성할 수 있습니다. 이러한 옵션은 대리자를 전달 하 여 구성 되어 [ `MapHub<T>` ](/dotnet/api/microsoft.aspnetcore.signalr.hubroutebuilder.maphub)합니다.

| 옵션 | 설명 |
| ------ | ----------- |
| `ApplicationMaxBufferSize` | 클라이언트에서 받은 바이트의 최대 수 있는 서버 버퍼입니다. 이 값을 늘리면 서버를 더 큰 메시지를 받을 수 있지만 메모리 사용에 부정적인 영향을 줄 수 있습니다. 기본값은 32KB입니다. |
| `AuthorizationData` | 목록이 [ `IAuthorizeData` ](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizedata) 클라이언트가 허브에 연결할 권한이 있는지 확인 하는 데 사용 되는 개체입니다. 기본적으로이 값으로 채워집니다에서 `Authorize` 허브 클래스에 적용 된 특성입니다. |
| `TransportMaxBufferSize` | 응용 프로그램에서 보낸 바이트의 최대 수 있는 서버 버퍼입니다. 이 값을 늘리면 서버를 더 큰 메시지를 보낼 수 있지만 메모리 사용에 부정적인 영향을 줄 수 있습니다. 기본값은 32KB입니다. |
| `Transports` | 비트 마스크 `HttpTransportType` 전송을 제한할 수 있는 값 클라이언트가 연결 하는 데 사용할 수 있습니다. 모든 전송 기본적으로 활성화 됩니다. |
| `LongPolling` | 긴 폴링 전송에만 추가 옵션입니다. |
| `WebSockets` | Websocket 전송에만 추가 옵션입니다. |

긴 폴링 전송을 사용 하 여 구성할 수 있는 추가 옵션에는 `LongPolling` 속성:

| 옵션 | 설명 |
| ------ | ----------- |
| `PollTimeout` | 최대 기간 서버 단일 폴링 요청을 종료 하기 전에 클라이언트에 보낼 메시지를 기다립니다. 이 값을 줄이면 하면 클라이언트가 새 폴링 요청을 더 자주 실행 합니다. 기본값은 90 초입니다. |

WebSocket 전송 사용 하 여 구성할 수 있는 추가 옵션에는 `WebSockets` 속성:

| 옵션 | 설명 |
| ------ | ----------- |
| `CloseTimeout` | 클라이언트가이 시간 간격 이내에 종결 되지 않으면 서버 닫힌 후에 연결이 종료 됩니다. |
| `SubProtocolSelector` | 설정 하는 데 사용할 수 있는 대리자는 `Sec-WebSocket-Protocol` 헤더를 사용자 지정 값입니다. 대리자는 값을 입력으로 클라이언트 요청을 받는 하 고 원하는 값을 반환 합니다. |

## <a name="configure-client-options"></a>클라이언트 옵션 구성

클라이언트 옵션에서 구성할 수 있습니다는 `HubConnectionBuilder` 유형 (.NET 및 JavaScript 클라이언트에서 사용 가능), 뿐만 `HubConnection` 자체입니다.

### <a name="configure-logging"></a>로깅 구성

로깅을 사용 하 여.NET 클라이언트에서 구성 된 `ConfigureLogging` 메서드. 서버의 경우와 같은 방식으로 로깅 공급자 및 필터를 등록할 수 있습니다. 참조는 [ASP.NET Core 로그인](xref:fundamentals/logging/index#how-to-add-providers) 자세한 정보에 대 한 설명서입니다.

> [!NOTE]
> 로깅 공급자를 등록 하려면 필요한 패키지를 설치 해야 합니다. 참조는 [기본 제공 로깅 공급자](xref:fundamentals/logging/index#built-in-logging-providers) 전체 목록에 대 한 설명서의 섹션입니다.

예를 들어 콘솔 로깅을 사용 하려면 설치는 `Microsoft.Extensions.Logging.Console` NuGet 패키지 합니다. 호출 된 `AddConsole` 확장 메서드:

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub")
    .ConfigureLogging(logging => {
        logging.SetMinimumLevel(LogLevel.Information);
        logging.AddConsole();
    })
    .Build();
```

JavaScript 클라이언트에서 비슷한 `configureLogging` 메서드가 있습니다. 제공 된 `LogLevel` 최소 수준의 로그를 생성 하는 메시지를 나타내는 값입니다. 로그가는 브라우저 콘솔 창에 기록 합니다.

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub")
    .configureLogging(signalR.LogLevel.Information)
    .build();
```

> [!NOTE]
> 완전히 로깅을 사용 하지 않으려면 지정 `signalR.LogLevel.None` 에 `configureLogging` 메서드.

JavaScript 클라이언트에서 사용 가능한 로그 수준은 다음과 같습니다. 메시지의 로깅을 사용 하면 로그 수준은 다음이 값 중 하나를 설정 **이상** 해당 수준입니다.

| 수준 | 설명 |
| ----- | ----------- |
| `None` | 메시지가 기록 됩니다. |
| `Critical` | 전체 응용 프로그램에서 오류를 나타내는 메시지입니다. |
| `Error` | 현재 작업에서 오류를 나타내는 메시지입니다. |
| `Warning` | 사소한 문제를 나타내는 메시지입니다. |
| `Information` | 정보 메시지입니다. |
| `Debug` | 진단 메시지를 디버깅할 때 유용 합니다. |
| `Trace` | 특정 문제를 진단 하기 위한 매우 자세한 진단 메시지입니다. |

### <a name="configure-allowed-transports"></a>허용 된 전송 구성

SignalR에서 사용 된 전송에서 구성할 수 있습니다는 `WithUrl` 호출 (`withUrl` JavaScript에서). 값의 비트 OR `HttpTransportType` 는 특정된 전송 모드를 사용 하도록 클라이언트를 제한 하는 데 사용할 수 있습니다. 모든 전송 기본적으로 활성화 됩니다.

예를 들어 Server-Sent 이벤트 전송 하지 않으려면 하지만 Websocket 및 긴 폴링 연결 허용:

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", HttpTransportType.WebSockets | HttpTransportType.LongPolling)
    .Build();
```

JavaScript 클라이언트에서 전송 설정 하 여 구성 된 `transport` 옵션 개체에 제공 된 필드 `withUrl`:

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub", { transport: signalR.HttpTransportType.WebSockets | signalR.HttpTransportType.LongPolling })
    .build();
```

### <a name="configure-bearer-authentication"></a>전달자 인증 구성

SignalR 요청 함께 인증 데이터를 제공 하기 위해 사용 된 `AccessTokenProvider` 옵션 (`accessTokenFactory` JavaScript에서) 원하는 액세스 토큰을 반환 하는 함수를 지정 합니다. .NET 클라이언트에서이 액세스 토큰으로 전달 되어 HTTP "전달자 인증" 토큰 (사용 하는 `Authorization` 형식의 헤더 `Bearer`). JavaScript 클라이언트에서 액세스 토큰은 Bearer 토큰으로 사용 **제외 하 고** 브라우저 Api (특히, Server-Sent 이벤트 및 Websocket 요청 수)에 헤더를 적용 하는 기능을 제한 하는 몇 가지 경우에 합니다. 이러한 경우 액세스 토큰이 쿼리 문자열 값으로 제공 `access_token`합니다.

.NET 클라이언트에는 `AccessTokenProvider` 의 옵션 대리자를 사용 하 여 옵션을 지정할 수 있습니다 `WithUrl`:

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options => {
        options.AccessTokenProvider = async () => {
            // Get and return the access token.
        }
    })
    .Build();
```

JavaScript 클라이언트에서 액세스 토큰을 설정 하 여 구성 됩니다는 `accessTokenFactory` 필드에 있는 옵션 개체 `withUrl`:

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub", {
        accessTokenFactory: () => {
            // Get and return the access token.
            // This function can return a JavaScript Promise if asynchronous
            // logic is required to retrieve the access token.
        }
    })
    .build();
```

### <a name="configure-timeout-and-keep-alive-options"></a>시간 제한 및 연결 유지 옵션 구성

제한 시간 및 유지 동작을 구성 하기 위한 추가 옵션은 사용할 수는 `HubConnection` 개체 자체:

| .NET 옵션 | JavaScript 옵션 | 설명 |
| ----------- | ----------------- | ----------- |
| `ServerTimeout` | `serverTimeoutInMilliseconds` | 서버 작업에 대 한 제한 시간입니다. 클라이언트 서버가이 기간에 모든 메시지를 전송 하지 않은 경우 서버 연결 끊김 및 트리거 고려는 `Closed` 이벤트 (`onclose` JavaScript에서). |
| `HandshakeTimeout` | 구성할 수 없습니다 | 핸드셰이크 초기 서버에 대 한 제한 시간입니다. 서버가이 간격의 핸드셰이크 응답을 전송 하지 않습니다, 클라이언트 취소 핸드셰이크 및 트리거는 `Closed` 이벤트 (`onclose` JavaScript에서). |

.NET 클라이언트 시간 제한 값으로 지정 되 `TimeSpan` 값입니다. JavaScript 클라이언트에서 제한 시간 값은 숫자로 지정 됩니다. 수는 밀리초 단위의 시간 값을 나타냅니다.

### <a name="configure-additional-options"></a>추가 옵션 구성

추가 옵션에서 구성할 수 있습니다는 `WithUrl` (`withUrl` JavaScript에서) 메서드를 `HubConnectionBuilder`:

| .NET 옵션 | JavaScript 옵션 | 설명 |
| ----------- | ----------------- | ----------- |
| `AccessTokenProvider` | `accessTokenFactory` | HTTP 요청에서 전달자 인증 토큰으로 제공 되는 문자열을 반환 하는 함수입니다. |
| `SkipNegotiation` | `skipNegotiation` | 이 속성을 설정 `true` 협상 단계를 건너뜁니다. **Websocket 전송은 사용 가능한 유일한 전송 하는 경우에 지원**합니다. 이 설정은 Azure SignalR 서비스를 사용 하는 경우 사용할 수 없습니다. |
| `ClientCertificates` | 구성 가능 * | 요청을 인증에 보내도록 TLS 인증서의 컬렉션입니다. |
| `Cookies` | 구성 가능 * | 모든 HTTP 요청에 보낼 HTTP 쿠키의 컬렉션입니다. |
| `Credentials` | 구성 가능 * | 모든 HTTP 요청과 함께 보내는 자격 증명입니다. |
| `CloseTimeout` | 구성 가능 * | Websocket에만 해당 합니다. 최대 기간 클라이언트 닫기 요청을 승인 하는 데 서버에 대 한 닫힌 후 대기 합니다. 서버가이 시간 안에 종료를 승인 하지 않습니다, 클라이언트 연결을 끊습니다. |
| `Headers` | 구성 가능 * | 모든 HTTP 요청에 보낼 추가 HTTP 헤더의 사전입니다. |
| `HttpMessageHandlerFactory` | 구성 가능 * | 구성 하거나 바꿀 사용할 수 있는 대리자는 `HttpMessageHandler` HTTP 요청을 보내는 데 사용 합니다. WebSocket 연결에 대 한 사용 되지 않습니다. 이 대리자는 null이 아닌 값을 반환 해야 하 고 기본 값을 매개 변수로 받을 키를 누릅니다. 해당 기본값에 대 한 설정을 수정 하 고, 반환 하거나 반환할 완전히 새로운 `HttpMessageHandler` 인스턴스. |
| `Proxy` | 구성 가능 * | HTTP 요청을 보낼 때 사용 하는 HTTP 프록시입니다. |
| `UseDefaultCredentials` | 구성 가능 * | 이 부울 보낼 HTTP 및 Websocket 요청에 대 한 기본 자격 증명을 설정 합니다. 이렇게 하면 Windows 인증을 사용 합니다. |
| `WebSocketConfiguration` | 구성 가능 * | 추가 WebSocket 옵션을 구성을 사용할 수 있는 대리자입니다. 인스턴스를 받아서 [ClientWebSocketOptions](/dotnet/api/system.net.websockets.clientwebsocketoptions) 옵션을 구성을 사용할 수 있는 합니다. |

별표 (*)로 표시 하는 옵션 브라우저 Api의에서 제한으로 인해 JavaScript 클라이언트에서 구성할 수 없습니다.

.NET 클라이언트에서 이러한 옵션을 수정할 수를 제공 하는 옵션 대리자가 `WithUrl`:

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options => {
        options.Headers["Foo"] = "Bar";
        options.Cookies.Add(new Cookie(/* ... */);
        options.ClientCertificates.Add(/* ... */);
    })
    .Build();
```

JavaScript 클라이언트에서 이러한 옵션에 제공 된 JavaScript 개체에 제공 될 수 있습니다 `withUrl`:

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub", {
        skipNegotiation: true,
        transport: signalR.HttpTransportType.WebSockets
    });
    .build();
```

## <a name="additional-resources"></a>추가 자료

* <xref:tutorials/signalr>
* <xref:signalr/hubs>
* <xref:signalr/javascript-client>
* <xref:signalr/dotnet-client>
* <xref:signalr/messagepackhubprotocol>
* <xref:signalr/supported-platforms>
