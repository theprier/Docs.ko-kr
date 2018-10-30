---
title: SignalR 및 ASP.NET Core SignalR의 차이점
author: tdykstra
description: SignalR 및 ASP.NET Core SignalR의 차이점
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.date: 09/10/2018
uid: signalr/version-differences
ms.openlocfilehash: 3cec37719b743b3c805ada77249f526278e44599
ms.sourcegitcommit: 2ef32676c16f76282f7c23154d13affce8c8bf35
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/30/2018
ms.locfileid: "50234607"
---
# <a name="differences-between-aspnet-signalr-and-aspnet-core-signalr"></a>ASP.NET SignalR 및 ASP.NET Core SignalR의 차이점

ASP.NET Core SignalR 클라이언트 또는 ASP.NET SignalR에 대 한 서버와 호환 되지 않습니다. 이 문서에서는 ASP.NET Core SignalR에서 변경 되거나 제거 된 기능을 자세히 설명 합니다.

## <a name="how-to-identify-the-signalr-version"></a>SignalR 버전을 식별 하는 방법

|                      | ASP.NET SignalR | ASP.NET Core SignalR |
| -------------------- | --------------- | -------------------- |
| Server NuGet 패키지 | [Microsoft.AspNet.SignalR](https://www.nuget.org/packages/Microsoft.AspNet.SignalR/) | [Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App/) (.NET Core)<br>[Microsoft.AspNetCore.SignalR](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR/) (.NET Framework) |
| 클라이언트 NuGet 패키지 | [Microsoft.AspNet.SignalR.Client](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Client/)<br>[Microsoft.AspNet.SignalR.JS](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.JS/) | [Microsoft.AspNetCore.SignalR.Client](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR.Client/) |
| 클라이언트 npm 패키지 | [signalr](https://www.npmjs.com/package/signalr) | [@aspnet/signalr](https://www.npmjs.com/package/@aspnet/signalr) |
| 서버 앱 유형 | ASP.NET (System.Web) 또는 OWIN 자체 호스트 | ASP.NET Core |
| 지원 되는 서버 플랫폼 | .NET framework 4.5 이상 | .NET Framework 4.6.1 이상<br>.NET core 2.1 이상 |

## <a name="feature-differences"></a>기능 차이점

### <a name="automatic-reconnects"></a>자동 다시 연결

자동 다시 연결 ASP.NET Core SignalR에서 지원 되지 않습니다. 클라이언트 연결이 끊어진 경우 다시 연결 하려는 경우 사용자는 새 연결을 시작 명시적으로 해야 합니다. ASP.NET SignalR, SignalR 연결 삭제 되 면 서버에 다시 연결 하려고 합니다. 

### <a name="protocol-support"></a>프로토콜 지원

ASP.NET Core SignalR 기반 새 이진 프로토콜 뿐만 아니라 JSON 지원 [MessagePack](xref:signalr/messagepackhubprotocol)합니다. 또한 사용자 지정 프로토콜을 만들 수 있습니다.

## <a name="differences-on-the-server"></a>서버에서 차이점

ASP.NET Core SignalR의 서버 쪽 라이브러리에 포함 된 합니다 [Microsoft.AspNetCore.App 메타 패키지](xref:fundamentals/metapackage-app) 패키지의 일부인 합니다 **ASP.NET Core 웹 응용 프로그램** Razor 및 MVC에 대 한 템플릿 프로젝트입니다.

ASP.NET Core SignalR은 ASP.NET Core 미들웨어를 호출 하 여 구성 해야 하므로 [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr) 에서 `Startup.ConfigureServices`합니다.

```csharp
services.AddSignalR()
```

에 라우팅을 구성 하려면 경로 내에서 허브에 매핑하는 [UseSignalR](/dotnet/api/microsoft.aspnetcore.builder.signalrappbuilderextensions.usesignalr) 메서드 호출을 `Startup.Configure` 메서드.

```csharp
app.UseSignalR(routes =>
{
    routes.MapHub<ChatHub>("/hub");
});
```

### <a name="sticky-sessions"></a>고정 세션

ASP.NET SignalR에 대 한 확장 모델에는 클라이언트가 다시 연결 하 고 팜의 모든 서버에 메시지를 보낼 수 있습니다. ASP.NET Core SignalR의 연결 기간에 대 한 클라이언트는 동일한 서버를 사용 하 여 작용 해야 합니다. Redis를 사용 하 여 확장에는 고정 세션은 필요한 의미 합니다. 확장 사용에 대 한 [Azure SignalR Service](/azure/azure-signalr/), 서비스가 클라이언트에 대 한 연결을 처리 하기 때문에 고정 세션이 필요 하지 않습니다. 

### <a name="single-hub-per-connection"></a>단일 허브 연결당

ASP.NET Core SignalR의 연결 모델이 간소화 되었습니다. 여러 허브에 대 한 액세스를 공유 하는 데 사용 되는 단일 연결 하지 않고 단일 허브에 직접 연결 됩니다.

### <a name="streaming"></a>스트리밍

ASP.NET Core SignalR 지원 [스트리밍 데이터](xref:signalr/streaming) 클라이언트에 허브에서 합니다.

### <a name="state"></a>시스템 상태

진행 메시지에 대 한 지원 뿐만 아니라 클라이언트 허브 (HubState 라고도 함) 사이의 임의 상태를 전달 하는 기능, 없어졌습니다. 지금은 허브 프록시 문자가 없는 경우

## <a name="differences-on-the-client"></a>클라이언트의 차이점

### <a name="typescript"></a>TypeScript

ASP.NET Core SignalR 클라이언트 쓰여질 [TypeScript](https://www.typescriptlang.org/)합니다. 사용 하는 경우 JavaScript 또는 TypeScript에서 작성할 수는 [JavaScript 클라이언트](xref:signalr/javascript-client)합니다.

### <a name="the-javascript-client-is-hosted-at-npmhttpswwwnpmjscom"></a>JavaScript 클라이언트에서 호스팅되는 [npm](https://www.npmjs.com/)

이전 버전에서는 Visual Studio의 NuGet 패키지를 통해 JavaScript 클라이언트가 받았습니다. Core 버전에 대 한 합니다 [ @aspnet/signalr ](https://www.npmjs.com/package/@aspnet/signalr) npm 패키지는 JavaScript 라이브러리를 포함 합니다. 이 패키지에 포함 되지 합니다 **ASP.NET Core 웹 응용 프로그램** 템플릿. Npm을 사용 하 여 설치 하는 `@aspnet/signalr` npm 패키지 있습니다.

```console
npm init -y
npm install @aspnet/signalr
```

### <a name="jquery"></a>jQuery

JQuery에 대 한 종속성이 제거 되었습니다, 프로젝트에는 jQuery 계속 사용할 수 있지만.

### <a name="javascript-client-method-syntax"></a>JavaScript 클라이언트 메서드 구문

이전 버전의 SignalR에서 JavaScript 구문이 변경 되었습니다. 사용 하지 않고는 `$connection` 개체를 사용 하 여 연결 합니다 [HubConnectionBuilder](/javascript/api/%40aspnet/signalr/hubconnectionbuilder) API.

```javascript
const connection = new signalR.HubConnectionBuilder()
    .withUrl("/hub")
    .build();
```

사용 된 [에서](/javascript/api/@aspnet/signalr/HubConnection#on) 허브를 호출할 수 있는 클라이언트 메서드를 지정 하는 방법입니다.

```javascript
connection.on("ReceiveMessage", (user, message) => {
    const msg = message.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
    const encodedMsg = user + " says " + msg;
    log(encodedMsg);
});
```

클라이언트 메서드를 만든 후 허브 연결을 시작 합니다. 체인을 [catch](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch) 메서드를 기록 하거나 오류를 처리 합니다.

```javascript
connection.start().catch(err => console.error(err.toString()));
```

### <a name="hub-proxies"></a>허브 프록시

허브 프록시 더 이상 자동으로 생성 됩니다. 메서드 이름에 전달 되는 대신 합니다 [호출할](/javascript/api/%40aspnet/signalr/hubconnection#invoke) 문자열로 API.

### <a name="net-and-other-clients"></a>.NET 및 기타 클라이언트

`Microsoft.AspNetCore.SignalR.Client` NuGet 패키지는 ASP.NET Core SignalR에 대 한.NET 클라이언트 라이브러리를 포함 합니다.

사용 된 [HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder) 을 작성 하는 허브에 대 한 연결의 인스턴스.

```csharp
connection = new HubConnectionBuilder()
    .WithUrl("url")
    .Build();
```

## <a name="scaleout-differences"></a>확장 차이점

ASP.NET SignalR SQL Server 및 Redis를 지원합니다. ASP.NET Core SignalR Azure SignalR Service 및 Redis를 지원합니다.

### <a name="aspnet"></a>ASP.NET

* [Azure Service Bus로 SignalR 규모 확장](/aspnet/signalr/overview/performance/scaleout-with-windows-azure-service-bus)
* [Redis로 SignalR 규모 확장](/aspnet/signalr/overview/performance/scaleout-with-redis)
* [SQL Server로 SignalR 규모 확장](/aspnet/signalr/overview/performance/scaleout-with-sql-server)

### <a name="aspnet-core"></a>ASP.NET Core

* [Azure SignalR Service](/azure/azure-signalr/)

## <a name="additional-resources"></a>추가 자료

* [허브](xref:signalr/hubs)
* [JavaScript 클라이언트](xref:signalr/javascript-client)
* [.NET 클라이언트](xref:signalr/dotnet-client)
* [지원되는 플랫폼](xref:signalr/supported-platforms)
