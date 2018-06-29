---
title: SignalR 및 ASP.NET Core SignalR 간의 차이점
author: rachelappel
description: SignalR 및 ASP.NET Core SignalR 간의 차이점
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.date: 06/30/2018
uid: signalr/version-differences
ms.openlocfilehash: fd314d93333bd159aef4bb4863be50c646809cf0
ms.sourcegitcommit: 1faf2525902236428dae6a59e375519bafd5d6d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090070"
---
# <a name="differences-between-signalr-and-aspnet-core-signalr"></a>SignalR 및 ASP.NET Core SignalR 간의 차이점

ASP.NET Core SignalR 클라이언트 또는 ASP.NET SignalR 용 서버와 호환 되지 않습니다. 이 문서는 제거 되거나 ASP.NET Core SignalR에서 변경 된 기능을 자세히 설명 합니다.

## <a name="feature-differences"></a>기능 차이점

### <a name="automatic-reconnects"></a>자동 다시 연결

자동 다시 연결 이상 지원 되지 않습니다. 이전에 SignalR 연결 삭제 된 경우 서버에 다시 연결 하려고 했습니다. 이제, 클라이언트의 연결이 다시 연결 하는 경우 사용자 새 연결을 명시적으로 시작 해야 합니다.

### <a name="protocol-support"></a>프로토콜 지원

ASP.NET Core SignalR 기반으로 새로운 이진 프로토콜 뿐만 아니라 JSON 지원 [MessagePack](xref:signalr/messagepackhubprotocol)합니다. 또한 사용자 지정 프로토콜을 만들 수 있습니다.

## <a name="differences-on-the-server"></a>서버에서의 차이점

SignalR의 서버 쪽 라이브러리에 포함 된는 `Microsoft.AspNetCore.App` 패키지의 일부인는 **ASP.NET Core 웹 응용 프로그램** Razor와 MVC 프로젝트에 대 한 서식 파일입니다.

호출 하 여 구성 해야 하므로 SignalR은 ASP.NET Core 미들웨어, `AddSignalR` 에서 `Startup.ConfigureServices`합니다.

```csharp
services.AddSignalR();
```

라우팅을 구성 하려면 허브 내에 경로 매핑하는 `UseSignalR` 메서드 호출의 `Startup.Configure` 메서드.

```csharp
app.UseSignalR(routes =>
{
    routes.MapHub<ChatHub>("/hub");
});
```

### <a name="sticky-sessions-now-required"></a>이제 필요한 고정 세션

클라이언트는 어떻게 확장 이전 버전의 SignalR에 사용한 때문에 다시 연결 및 팜의 모든 서버에 메시지를 보낼 수 없습니다. 다시 연결을 지원 하지 않으므로 뿐만 아니라 확장 모델에 변경 내용으로 인해이 더 이상 지원 합니다. 이제 클라이언트가 서버에 연결 되 면 연결 기간에 대 한 동일한 서버와 상호 작용에 필요 합니다.

### <a name="single-hub-per-connection"></a>단일 허브 연결당

ASP.NET Core SignalR 연결 모델이 간소화 되었습니다. 연결은 여러 허브에 대 한 액세스를 공유 하는 데 사용 되는 단일 연결 하지 않고 단일 허브에 직접 만들어집니다.

### <a name="streaming"></a>스트리밍

SignalR에서 지 원하는 [스트리밍 데이터](xref:signalr/streaming) 클라이언트에 허브에서 동기화 합니다.

### <a name="state"></a>시스템 상태

진행 메시지에 대 한 지원 및 클라이언트와 허브 (HubState) 사이의 임의 상태를 전달 하는 기능, 없어졌습니다. 현재 허브 프록시 중 해당 하는 항목이 있습니다.

## <a name="differences-on-the-client"></a>클라이언트에서의 차이점

### <a name="typescript"></a>TypeScript

SignalR의 ASP.NET Core 버전으로 작성 된 [TypeScript](https://www.typescriptlang.org/)합니다. 사용 하는 경우 JavaScript 또는 TypeScript에서 작성할 수 있습니다는 [JavaScript 클라이언트](xref:signalr/javascript-client)합니다.

### <a name="the-javascript-client-is-hosted-at-npmhttpswwwnpmjscom"></a>JavaScript 클라이언트에 호스트 되어 [npm](https://www.npmjs.com/)

JavaScript 클라이언트는 이전 버전에서는 Visual Studio에서 NuGet 패키지를 통해 가져온 것입니다. 코어 버전에 대 한는 [ @aspnet/signalr npm 패키지](https://www.npmjs.com/package/@aspnet/signalr) JavaScript 라이브러리를 포함 합니다. 이 패키지에 포함 되어 있지는 **ASP.NET Core 웹 응용 프로그램** 템플릿. Npm을 사용 하 여 설치 하 고 `@aspnet/signalr` npm 패키지 합니다.

```console
npm init -y
npm install @aspnet/signalr
```

### <a name="jquery"></a>jQuery

JQuery에 대 한 종속성은 제거 되었습니다, 프로젝트에서 jQuery를 계속 사용할 수 있지만.

### <a name="javascript-client-method-syntax"></a>JavaScript 클라이언트 메서드 구문

JavaScript 구문 SignalR의 이전 버전에서 변경 되었습니다. 사용 하지 않고는 `$connection` 개체를 사용 하 여 연결을 만들기는 `HubConnectionBuilder` API입니다.

```javascript
const connection = new signalR.HubConnectionBuilder()
    .withUrl("/hub")
    .build();
```

사용 하 여 `connection.on` 허브를 호출할 수 있는 클라이언트 방법을 지정할 수 있습니다.

```javascript
connection.on("ReceiveMessage", (user, message) => {
    const msg = message.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
    const encodedMsg = user + " says " + msg;
    log(encodedMsg);
});
```

클라이언트 메서드를 만든 후 허브 연결을 시작 합니다. 체인을 `catch` 메서드를 로그 또는 오류를 처리 합니다.

```javascript
connection.start().catch(err => console.error(err.toString()));
```

### <a name="hub-proxies"></a>허브 프록시

허브 프록시 더 이상 자동으로 생성 됩니다. 메서드 이름에 전달 되는 대신,는 `invoke` 문자열로 API입니다.

### <a name="net-and-other-clients"></a>.NET 및 기타 클라이언트

`Microsoft.AspNetCore.SignalR.Client` ASP.NET Core SignalR 용.NET 클라이언트 라이브러리 NuGet 패키지에 포함 되어 있습니다.

사용 된 `HubConnectionBuilder` 을 작성 하는 허브에 대 한 연결의 인스턴스입니다.

```csharp
connection = new HubConnectionBuilder()
    .WithUrl("url")
    .Build();
```

## <a name="additional-resources"></a>추가 자료

* [허브](xref:signalr/hubs)
* [JavaScript 클라이언트](xref:signalr/javascript-client)
* [.NET 클라이언트](xref:signalr/dotnet-client)
* [지원되는 플랫폼](xref:signalr/supported-platforms)
