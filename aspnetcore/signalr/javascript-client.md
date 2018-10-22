---
title: ASP.NET Core SignalR JavaScript 클라이언트
author: tdykstra
description: ASP.NET Core SignalR JavaScript 클라이언트의 개요입니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 08/14/2018
uid: signalr/javascript-client
ms.openlocfilehash: 10958c414aa4a285c8a2810bb99e278f719c5b7f
ms.sourcegitcommit: 8bf4dff3069e62972c1b0839a93fb444e502afe7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/20/2018
ms.locfileid: "46483051"
---
# <a name="aspnet-core-signalr-javascript-client"></a>ASP.NET Core SignalR JavaScript 클라이언트

작성자: [Rachel Appel](http://twitter.com/rachelappel)

ASP.NET Core SignalR JavaScript 클라이언트 라이브러리를 사용하면 서버 쪽 허브 코드를 호출할 수 있습니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/javascript-client/sample) ([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="install-the-signalr-client-package"></a>SignalR 클라이언트 패키지를 설치하기

SignalR JavaScript 클라이언트 라이브러리는 [npm](https://www.npmjs.com/) 패키지로 배포됩니다. Visual Studio를 사용하고 있다면 **패키지 관리자 콘솔**에서 루트 폴더에 위치해 있는 동안 `npm install`을 실행합니다. Visual Studio Code에서는 **통합 터미널**에서 명령을 실행합니다.

  ```console
  npm init -y
  npm install @aspnet/signalr
  ```

그러면 npm이 *node_modules\\@aspnet\signalr\dist\browser* 폴더에 패키지 콘텐츠를 설치합니다. *wwwroot\\lib* 폴더 하위에 *signalr*이라는 새 폴더를 만듭니다. *signalr.js* 파일을 *wwwroot\lib\signalr* 폴더로 복사합니다.

## <a name="use-the-signalr-javascript-client"></a>SignalR JavaScript 클라이언트 사용하기

`<script>` 요소를 이용해서 SignalR JavaScript 클라이언트를 참조합니다.

```html
<script src="~/lib/signalr/signalr.js"></script>
```

## <a name="connect-to-a-hub"></a>허브에 연결하기

다음 코드는 연결을 만들고 시작합니다. 허브의 이름은 대소문자를 구분하지 않습니다.

[!code-javascript[Call hub methods](javascript-client/sample/wwwroot/js/chat.js?range=9-12,28)]

### <a name="cross-origin-connections"></a>원본 간 연결

일반적으로 브라우저는 요청된 페이지와 동일한 도메인에서 연결을 로드합니다. 그러나 다른 도메인에 연결해야 하는 경우도 있습니다.

악의적인 사이트가 다른 사이트의 민감한 데이터를 읽지 못하게 막기 위해서, 기본적으로 [원본 간 연결](xref:security/cors)은 비활성화되어 있습니다. 원본 간 요청을 허용하려면 `Startup` 클래스에서 이를 활성화시키십시오.

[!code-csharp[Cross-origin connections](javascript-client/sample/Startup.cs?highlight=29-35,56)]

## <a name="call-hub-methods-from-client"></a>클라이언트에서 허브 메서드 호출하기

JavaScript 클라이언트는 [HubConnection](/javascript/api/%40aspnet/signalr/hubconnection)의 [invoke](/javascript/api/%40aspnet/signalr/hubconnection#invoke) 메서드를 통해서 허브의 public 메서드를 호출합니다. 이 `invoke` 메서드는 두 가지 인수를 전달 받습니다.

* 허브 메서드의 이름. 다음 예제에서 허브 메서드의 이름은 `SendMessage`입니다.
* 허브 메서드에 정의된 모든 인수. 다음 예제에서 인수의 이름은 `message`입니다.

  [!code-javascript[Call hub methods](javascript-client/sample/wwwroot/js/chat.js?range=24)]

## <a name="call-client-methods-from-hub"></a>허브에서 클라이언트 메서드 호출하기

허브에서 메시지를 수신하려면 `HubConnection`의 [on](/javascript/api/%40aspnet/signalr/hubconnection#on) 메서드를 이용해서 메서드를 정의합니다.

* JavaScript 클라이언트 메서드의 이름. 다음 예제에서 메서드 이름은 `ReceiveMessage`입니다.
* 허브에서 메서드로 전달될 인수. 다음 예제에서 인수의 이름은 `message`입니다.

[!code-javascript[Receive calls from hub](javascript-client/sample/wwwroot/js/chat.js?range=14-19)]

위의 `connection.on` 내부의 코드는 서버 쪽 코드에서 [SendAsync](/dotnet/api/microsoft.aspnetcore.signalr.clientproxyextensions.sendasync) 메서드를 사용하여 이 코드를 호출할 때 실행됩니다.

[!code-csharp[Call client-side](javascript-client/sample/hubs/chathub.cs?range=8-11)]

SignalR은 `SendAsync`와 `connection.on`에 정의된 메서드 이름과 인수들이 일치하는지를 검사해서 어떤 클라이언트 메서드를 호출할지 결정합니다.

> [!NOTE]
> 권장되는 방식은 `on` 메서드를 호출한 뒤에 `HubConnection`의 [start](/javascript/api/%40aspnet/signalr/hubconnection#start) 메서드를 호출하는 것입니다. 이렇게 하면 모든 메시지를 수신하기 전에 처리기가 먼저 등록됩니다.

## <a name="error-handling-and-logging"></a>오류 처리 및 로깅

클라이언트 쪽 오류를 처리하려면 `start` 메서드의 끝에 `catch` 메서드를 연결합니다. 브라우저의 콘솔에 오류를 출력하려면 `console.error`를 사용합니다.

[!code-javascript[Error handling](javascript-client/sample/wwwroot/js/chat.js?range=28)]

연결이 만들어지면 로거와 기록할 이벤트 유형을 전달하여 클라이언트 쪽 로그 추적을 설정합니다. 지정한 로그 수준 이상의 메시지가 기록됩니다. 사용 가능한 로그 수준은 다음과 같습니다.

* `signalR.LogLevel.Error` &ndash; 오류 메시지. `Error` 메시지만 기록합니다.
* `signalR.LogLevel.Warning` &ndash; 잠재적 오류에 대한 경고 메시지. `Warning` 및 `Error` 메시지를 기록합니다.
* `signalR.LogLevel.Information` &ndash; 오류가 아닌 상태 메시지. `Information`, `Warning`, 및 `Error` 메시지를 기록합니다.
* `signalR.LogLevel.Trace` &ndash; 추적 메시지. 허브와 클라이언트 간에 전송되는 데이터를 포함한 모든 것을 기록합니다.

로그 수준을 구성하려면 [HubConnectionBuilder](/javascript/api/%40aspnet/signalr/hubconnectionbuilder)의 [configureLogging](/javascript/api/%40aspnet/signalr/hubconnectionbuilder#configurelogging) 메서드를 사용합니다. 메시지는 브라우저 콘솔에 기록됩니다.

[!code-javascript[Logging levels](javascript-client/sample/wwwroot/js/chat.js?range=9-12)]

## <a name="additional-resources"></a>추가 자료

* [JavaScript API 참조](/javascript/api/?view=signalr-js-latest)
* [허브](xref:signalr/hubs)
* [.NET 클라이언트](xref:signalr/dotnet-client)
* [Azure에 게시하기](xref:signalr/publish-to-azure-web-app)
* [ASP.NET Core에서 원본 간 요청(CORS)을 사용하도록 설정하기](xref:security/cors)
