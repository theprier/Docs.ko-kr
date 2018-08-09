---
title: ASP.NET Core SignalR 구성
author: tdykstra
description: ASP.NET Core SignalR 앱을 구성 하는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 07/31/2018
uid: signalr/configuration
ms.openlocfilehash: eac1202828edbcd295d7e52aa424cd625ee70e34
ms.sourcegitcommit: 29dfe436f54a27fbb4f6494bc639d16c75001fab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2018
ms.locfileid: "39722466"
---
# <a name="aspnet-core-signalr-configuration"></a>ASP.NET Core SignalR 구성

## <a name="jsonmessagepack-serialization-options"></a>JSON/MessagePack 직렬화 옵션

ASP.NET Core SignalR 메시지 인코딩에 대 한 두 가지 프로토콜을 지원 합니다. [JSON](https://www.json.org/) 하 고 [MessagePack](https://msgpack.org/index.html)합니다. 각 프로토콜에 serialization 구성 옵션이 있습니다.

JSON serialization을 사용 하 여 서버에 구성할 수 있습니다 합니다 [AddJsonProtocol](/dotnet/api/microsoft.extensions.dependencyinjection.jsonprotocoldependencyinjectionextensions.addjsonprotocol) 후 추가할 수 있는 확장 메서드 [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr) 에서 프로그램 `Startup.ConfigureServices` 메서드. 합니다 `AddJsonProtocol` 메서드는 수신 하는 대리자는 `options` 개체입니다. 합니다 [PayloadSerializerSettings](/dotnet/api/microsoft.aspnetcore.signalr.jsonhubprotocoloptions.payloadserializersettings) 해당 개체에 대해 속성이 한 JSON.NET `JsonSerializerSettings` serialization 인수를 구성 하 고 값을 반환 하는 데 사용할 수 있습니다. 참조 된 [JSON.NET 설명서](https://www.newtonsoft.com/json/help/html/Introduction.htm) 대 한 자세한 내용은 합니다.

예를 들어 속성 이름 "PascalCase" 기본 "camelCase" 이름 대신 사용할 serializer를 구성 하려면 다음 코드를 사용 합니다.

```csharp
services.AddSignalR()
    .AddJsonHubProtocol(options => {
        options.PayloadSerializerSettings.ContractResolver = 
        new DefaultContractResolver();
    });
```

.NET 클라이언트에서 동일한 `AddJsonHubProtocol` 에 있는 확장 메서드 [HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder)합니다. `Microsoft.Extensions.DependencyInjection` 확장 메서드를 해결 하려면 네임 스페이스를 가져올 수 있어야 합니다.

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
> 이 이번에 JavaScript 클라이언트에서 JSON serialization을 구성 하는 것이 불가능 합니다.

### <a name="messagepack-serialization-options"></a>MessagePack 직렬화 옵션

MessagePack serialization에 대 한 대리자를 제공 하 여 구성할 수 있습니다 합니다 [AddMessagePackProtocol](/dotnet/api/microsoft.extensions.dependencyinjection.msgpackprotocoldependencyinjectionextensions.addmessagepackprotocol) 호출 합니다. 참조 [SignalR에서 MessagePack](xref:signalr/messagepackhubprotocol) 대 한 자세한 내용은 합니다.

> [!NOTE]
> 이 이번에 JavaScript 클라이언트에서 MessagePack serialization을 구성 하는 것이 불가능 합니다.

## <a name="configure-server-options"></a>서버 옵션 구성

다음 표에서 SignalR 허브를 구성 하는 것에 대 한 옵션을 보여 줍니다.

| 옵션 | 기본값 | 설명 |
| ------ | ------------- | ----------- |
| `HandshakeTimeout` | 15초 | 클라이언트는이 시간 간격 내에서 초기 핸드셰이크 메시지를 보내지 않습니다, 경우에 연결이 닫혀 있습니다. 이것이 핸드셰이크 시간 초과 오류는 심각한 네트워크 대기 시간으로 인해 발생 하는 경우에 수정 해야 하는 고급 설정입니다. 핸드셰이크 프로세스에서 구체적으로 말하면에 대 한 참조를 [SignalR 허브 프로토콜 사양](https://github.com/aspnet/SignalR/blob/master/specs/HubProtocol.md)합니다. |
| `KeepAliveInterval` | 15초 | 서버는이 간격 내에서 메시지를 전송 되지 않은, ping 메시지는 연결을 열어 두려면 자동으로 보내집니다. |
| `SupportedProtocols` | 설치 된 모든 프로토콜 | 이 허브에 의해 지원 되는 프로토콜입니다. 기본적으로 서버에 등록 하는 모든 프로토콜 수 있지만 개별 허브에 대 한 특정 프로토콜을 사용 하지 않도록 설정 하려면이 목록에서 프로토콜을 제거할 수 있습니다. |
| `EnableDetailedErrors` | `false` | 경우 `true`자세한, Hub 메서드에서 예외가 throw 될 때 예외 메시지가 클라이언트로 반환 됩니다. 기본값은 `false`처럼 이러한 예외 메시지는 중요 한 정보를 포함할 수 있습니다. |

하는 옵션 대리자를 제공 하 여 모든 허브에 대 한 옵션을 구성할 수 있습니다 합니다 `AddSignalR` 에서 호출 `Startup.ConfigureServices`합니다.

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

단일 허브에 대 한 옵션에서 제공 하는 전역 옵션을 재정의 `AddSignalR` 를 사용 하 여 구성할 수 있습니다 [AddHubOptions\<T >](/dotnet/api/microsoft.extensions.dependencyinjection.huboptionsdependencyinjectionextensions.addhuboptions):

```csharp
services.AddSignalR().AddHubOptions<MyHub>(options =>
{
    options.EnableDetailedErrors = true;
}
```

사용 하 여 `HttpConnectionDispatcherOptions` 전송 및 메모리 버퍼 관리와 관련 된 고급 설정을 구성할 수 있습니다. 이러한 옵션에 대 한 대리자를 전달 하 여 구성 됩니다 [MapHub\<T >](/dotnet/api/microsoft.aspnetcore.signalr.hubroutebuilder.maphub)합니다.

| 옵션 | 기본값 | 설명 |
| ------ | ------------- | ----------- |
| `ApplicationMaxBufferSize` | 32KB | 클라이언트에서 받은 바이트의 최대 수는 서버 버퍼입니다. 이 값을 늘리면 서버에서 큰 메시지를 받을 수 있지만 메모리 사용에 부정적인 영향을 줄 수 있습니다. |
| `AuthorizationData` | 자동으로 수집 된 데이터는 `Authorize` 은 허브 클래스에 적용 되는 특성입니다. | 목록을 [IAuthorizeData](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizedata) 클라이언트가 허브에 연결할 권한이 있는지 확인 하는 데 사용 되는 개체입니다. |
| `TransportMaxBufferSize` | 32KB | 앱에서 전송 된 바이트의 최대 수는 서버 버퍼입니다. 이 값을 늘리면 더 큰 메시지를 보낼 수 있지만 메모리 사용에 부정적인 영향을 줄 수 있습니다. |
| `Transports` | 모든 전송은 사용할 수 있습니다. | 비트 마스크 `HttpTransportType` 전송을 제한할 수 있는 값을 클라이언트는 연결할 사용할 수 있습니다. |
| `LongPolling` | 다음을 참조하세요. | 긴 폴링 전송 관련 추가 옵션입니다. |
| `WebSockets` | 다음을 참조하세요. | Websocket 전송으로 특정 추가 옵션입니다. |

긴 폴링 전송을 사용 하 여 구성할 수 있는 추가 옵션에는 `LongPolling` 속성:

| 옵션 | 기본값 | 설명 |
| ------ | ------------- | ----------- |
| `PollTimeout` | 90 초 | 최대 기간 서버 단일 폴링 요청을 종료 하기 전에 클라이언트에 보낼 메시지를 기다립니다. 이 값을 줄이면 하면 클라이언트가 새 폴링 요청을 더 자주 실행 합니다. |

WebSocket 전송 사용 하 여 구성할 수 있는 추가 옵션에는 `WebSockets` 속성:

| 옵션 | 기본값 | 설명 |
| ------ | ------------- | ----------- |
| `CloseTimeout` | 5초 | 서버를 닫으면이 시간 간격 내에서 닫기에 실패 하면 클라이언트에서 연결이 종료 됩니다. |
| `SubProtocolSelector` | `null` | 설정에 사용할 수 있는 대리자를 `Sec-WebSocket-Protocol` 헤더를 사용자 지정 값입니다. 대리자 값 입력으로 클라이언트에서 요청을 받는 및 원하는 값을 반환 해야 합니다. |

## <a name="configure-client-options"></a>클라이언트 옵션 구성

클라이언트 옵션에서 구성할 수 있습니다 합니다 `HubConnectionBuilder` 형식 (.NET 및 JavaScript 클라이언트에서 사용 가능), 뿐만 `HubConnection` 자체입니다.

### <a name="configure-logging"></a>로깅 구성

로깅을 사용 하 여.NET 클라이언트에서 구성 됩니다는 `ConfigureLogging` 메서드. 서버의 경우와 동일한 방식으로 로깅 공급자 및 필터를 등록할 수 있습니다. 참조를 [ASP.NET Core 로그인](xref:fundamentals/logging/index#how-to-add-providers) 자세한 정보에 대 한 설명서입니다.

> [!NOTE]
> 로깅 공급자를 등록 하기 위해 필요한 패키지를 설치 해야 합니다. 참조 된 [기본 제공 로깅 공급자](xref:fundamentals/logging/index#built-in-logging-providers) 전체 목록은 문서 섹션입니다.

예를 들어 콘솔 로깅을 사용 하려면 설치 된 `Microsoft.Extensions.Logging.Console` NuGet 패키지. 호출 된 `AddConsole` 확장 메서드:

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub")
    .ConfigureLogging(logging => {
        logging.SetMinimumLevel(LogLevel.Information);
        logging.AddConsole();
    })
    .Build();
```

JavaScript 클라이언트에서 유사한 `configureLogging` 메서드가 있습니다. 제공 된 `LogLevel` 최소 수준의 로그를 생성 하는 메시지를 나타내는 값입니다. 로그는 브라우저 콘솔 창에 기록 됩니다.

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub")
    .configureLogging(signalR.LogLevel.Information)
    .build();
```

> [!NOTE]
> 전적으로 로깅을 사용 하지 않으려면 지정할 `signalR.LogLevel.None` 에 `configureLogging` 메서드.

JavaScript 클라이언트에서 사용 가능한 로그 수준은 다음과 같습니다. 메시지 로깅을 설정 로그 수준은 다음이 값 중 하나를 설정 **이상** 수준입니다.

| 수준 | 설명 |
| ----- | ----------- |
| `None` | 메시지가 기록 되지 않았습니다. |
| `Critical` | 전체 앱에서 오류를 나타내는 메시지입니다. |
| `Error` | 현재 작업에서 오류를 나타내는 메시지입니다. |
| `Warning` | 사소한 문제를 나타내는 메시지입니다. |
| `Information` | 정보 메시지입니다. |
| `Debug` | 진단 메시지를 디버깅할 때 유용 합니다. |
| `Trace` | 특정 문제를 진단 하기 위한 매우 자세한 진단 메시지입니다. |

### <a name="configure-allowed-transports"></a>허용 된 전송 구성

SignalR에서 사용 된 전송에서 구성할 수 있습니다 합니다 `WithUrl` 호출 (`withUrl` JavaScript에서). 값의 비트 OR `HttpTransportType` 만 특정된 전송 모드를 사용 하도록 클라이언트를 제한 하려면 사용할 수 있습니다. 모든 전송에서는 기본적으로 활성화 됩니다.

예를 들어 Server-Sent 이벤트 전송 하지 않으려면 하지만 Websocket 및 Long Polling 연결 허용:

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", HttpTransportType.WebSockets | HttpTransportType.LongPolling)
    .Build();
```

JavaScript 클라이언트에서 전송 설정 하 여 구성 합니다 `transport` 필드에 제공 되는 옵션 개체에 `withUrl`:

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub", { transport: signalR.HttpTransportType.WebSockets | signalR.HttpTransportType.LongPolling })
    .build();
```

### <a name="configure-bearer-authentication"></a>전달자 인증 구성

SignalR 요청과 함께 인증 데이터를 제공 하려면 사용 합니다 `AccessTokenProvider` 옵션 (`accessTokenFactory` JavaScript에서) 원하는 액세스 토큰을 반환 하는 함수를 지정 하려면. .NET 클라이언트에서이 액세스 토큰으로 전달 되어 HTTP "전달자 인증" 토큰 (사용 하는 `Authorization` 형식의 헤더 `Bearer`). JavaScript 클라이언트에서 액세스 토큰을 전달자 토큰으로 사용 되는 **제외한** 경우 Api 브라우저 (특히 Server-Sent 이벤트 및 Websocket 요청)에 대 한 헤더를 적용 하는 기능을 제한 하는 위치입니다. 이러한 경우 액세스 토큰은 쿼리 문자열 값으로 제공 됩니다 `access_token`합니다.

.NET 클라이언트에서를 `AccessTokenProvider` 의 옵션 대리자를 사용 하 여 옵션을 지정할 수 있습니다 `WithUrl`:

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options => {
        options.AccessTokenProvider = async () => {
            // Get and return the access token.
        }
    })
    .Build();
```

JavaScript 클라이언트에서 액세스 토큰을 설정 하 여 구성 됩니다 합니다 `accessTokenFactory` 필드에서 옵션 개체에 `withUrl`:

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

### <a name="configure-timeout-and-keep-alive-options"></a>제한 시간 및 연결 유지 옵션 구성

제한 시간 및 유지 동작 구성에 대 한 추가 옵션에서 사용할 수는 `HubConnection` 개체 자체:

| .NET 옵션 | JavaScript 옵션 | 기본값 | 설명 |
| ----------- | ----------------- | ------------- | ----------- |
| `ServerTimeout` | `serverTimeoutInMilliseconds` | 30 초 (30000 밀리초) | 서버 작업에 대 한 제한 시간입니다. 클라이언트 연결이 끊어진 서버 및 트리거 고려 서버는이 간격에 메시지를 전송 되지 않은, 경우 합니다 `Closed` 이벤트 (`onclose` JavaScript에서). |
| `HandshakeTimeout` | 구성할 수 없음 | 15초 | 초기 서버 핸드셰이크에 대 한 제한 시간입니다. 서버는이 간격의 핸드셰이크 응답을 보내지 않습니다, 클라이언트 취소 트리거와 핸드셰이크를 `Closed` 이벤트 (`onclose` JavaScript에서). 이것이 핸드셰이크 시간 초과 오류는 심각한 네트워크 대기 시간으로 인해 발생 하는 경우에 수정 해야 하는 고급 설정입니다. 핸드셰이크 프로세스에서 구체적으로 말하면에 대 한 참조를 [SignalR 허브 프로토콜 사양](https://github.com/aspnet/SignalR/blob/master/specs/HubProtocol.md)합니다. |

.NET 클라이언트에서 제한 시간 값으로 지정 됩니다 `TimeSpan` 값입니다. JavaScript 클라이언트에서 제한 시간 값은 지속 시간 (밀리초) 나타내는 숫자로 지정 됩니다.

### <a name="configure-additional-options"></a>추가 옵션 구성

추가 옵션에서 구성할 수 있습니다 합니다 `WithUrl` (`withUrl` javascript에서) 메서드를 `HubConnectionBuilder`:

| .NET 옵션 | JavaScript 옵션 | 기본값 | 설명 |
| ----------- | ----------------- | ------------- | ----------- |
| `AccessTokenProvider` | `accessTokenFactory` | `null` | HTTP 요청에서 전달자 인증 토큰으로 제공 되는 문자열을 반환 하는 함수입니다. |
| `SkipNegotiation` | `skipNegotiation` | `false` | 이 값을 설정 `true` 협상 단계를 건너뜁니다. **Websocket 전송이 사용된만 전송 하는 경우에 지원**합니다. Azure SignalR Service를 사용 하는 경우에이 설정을 사용할 수 없습니다. |
| `ClientCertificates` | 구성 가능 * | Empty | 요청을 인증 하는 보내도록 TLS 인증서의 컬렉션입니다. |
| `Cookies` | 구성 가능 * | Empty | 모든 HTTP 요청과 함께 보낼 HTTP 쿠키의 컬렉션입니다. |
| `Credentials` | 구성 가능 * | Empty | 모든 HTTP 요청과 함께 보낼 자격 증명입니다. |
| `CloseTimeout` | 구성 가능 * | 5초 | Websocket에만 해당 합니다. 최대 기간 클라이언트 닫기 요청을 승인 하기 위해 서버에 대해 닫는 태그 뒤 대기 합니다. 서버는이 시간 내 닫기를 승인 하지 않습니다, 경우에 클라이언트 연결을 끊습니다. |
| `Headers` | 구성 가능 * | Empty | 모든 HTTP 요청과 함께 보낼 추가 HTTP 헤더의 사전입니다. |
| `HttpMessageHandlerFactory` | 구성 가능 * | `null` | 구성 또는 교체를 사용할 수 있는 대리자를 `HttpMessageHandler` HTTP 요청을 보내는 데 사용 합니다. WebSocket 연결에 대 한 사용 되지 않습니다. 이 대리자는 null이 아닌 값을 반환 해야 하 고 기본 값을 매개 변수로 수신. 기본값에서 설정을 수정 하 고 반환 하는 등 또는 새 반환 `HttpMessageHandler` 인스턴스. **그렇지 않은 경우 처리기를 교체 해야 제공된 된 처리기에서 유지 하려는 설정을 복사, 구성된 옵션 (예: 쿠키 및 헤더) 새 처리기에 적용 되지 않습니다.** |
| `Proxy` | 구성 가능 * | `null` | HTTP 요청을 보낼 때 사용할 HTTP 프록시입니다. |
| `UseDefaultCredentials` | 구성 가능 * | `false` | HTTP 및 WebSockets 요청에 대 한 기본 자격 증명을 보내려고이 부울 값을 설정 합니다. 이 통해 Windows 인증을 사용 합니다. |
| `WebSocketConfiguration` | 구성 가능 * | `null` | 추가 WebSocket 옵션을 구성 하는 대리자입니다. 인스턴스를 받아서 [ClientWebSocketOptions](/dotnet/api/system.net.websockets.clientwebsocketoptions) 옵션을 구성 하려면 사용할 수 있습니다. |

별표 (*)로 표시 하는 옵션은 Api 브라우저의 제한으로 인해 JavaScript 클라이언트에서 구성할 수 있습니다.

.NET 클라이언트에서 이러한 옵션은 옵션 대리자를 제공 하 여 수정할 수 `WithUrl`:

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options => {
        options.Headers["Foo"] = "Bar";
        options.Cookies.Add(new Cookie(/* ... */);
        options.ClientCertificates.Add(/* ... */);
    })
    .Build();
```

JavaScript 클라이언트에서 이러한 옵션을 제공 하는 JavaScript 개체에 제공할 수 있습니다 `withUrl`:

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
