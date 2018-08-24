---
title: ASP.NET Core SignalR JavaScript 클라이언트
author: tdykstra
description: ASP.NET Core SignalR JavaScript 클라이언트의 개요입니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 08/14/2018
uid: signalr/javascript-client
ms.openlocfilehash: 639c30f1d145a3da5e4f5857f32c1b573c1bfce2
ms.sourcegitcommit: 2c158fcfd325cad97ead608a816e525fe3dcf757
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2018
ms.locfileid: "41829606"
---
# <a name="aspnet-core-signalr-javascript-client"></a>ASP.NET Core SignalR JavaScript 클라이언트

작성자: [Rachel Appel](http://twitter.com/rachelappel)

ASP.NET Core SignalR JavaScript 클라이언트 라이브러리를 사용 하면 서버 쪽 허브 코드를 호출할 수 있습니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/javascript-client/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="install-the-signalr-client-package"></a>SignalR 클라이언트 패키지를 설치 합니다.

SignalR JavaScript 클라이언트 라이브러리를 전달 되는 [npm](https://www.npmjs.com/) 패키지 있습니다. Visual Studio를 사용 하는 경우 실행할 `npm install` 에서 합니다 **패키지 관리자 콘솔** 루트 폴더에 있는 동안. Visual Studio Code에서 명령을 실행 합니다 **통합 터미널**합니다.

  ```console
  npm init -y
  npm install @aspnet/signalr
  ```

npm에서 패키지 콘텐츠를 설치 합니다 *node_modules\\ @aspnet\signalr\dist\browser* 폴더입니다. 라는 새 폴더를 만듭니다 *signalr* 아래의 합니다 *wwwroot\\lib* 폴더입니다. 복사 합니다 *signalr.js* 파일을 합니다 *wwwroot\lib\signalr* 폴더입니다.

## <a name="use-the-signalr-javascript-client"></a>SignalR JavaScript 클라이언트 사용

SignalR JavaScript 클라이언트에서 참조 된 `<script>` 요소입니다.

```html
<script src="~/lib/signalr/signalr.js"></script>
```

## <a name="connect-to-a-hub"></a>허브에 연결

다음 코드를 만들고 연결을 시작 합니다. 허브의 이름은 대/소문자 구분입니다.

[!code-javascript[Call hub methods](javascript-client/sample/wwwroot/js/chat.js?range=9-12,28)]

### <a name="cross-origin-connections"></a>크로스-원본 연결

일반적으로 브라우저는 요청된 된 페이지와 동일한 도메인에서 연결을 로드합니다. 그러나 다른 도메인에 연결할 때 필요한 경우가 있습니다.

악성 사이트에서 다른 사이트의 중요 한 데이터를 읽을 않으려면 [크로스-원본 연결](xref:security/cors) 기본적으로 비활성화 됩니다. 크로스-원본 요청을 허용 하려면에 있도록는 `Startup` 클래스입니다.

[!code-csharp[Cross-origin connections](javascript-client/sample/Startup.cs?highlight=29-35,56)]

## <a name="call-hub-methods-from-client"></a>클라이언트에서 허브 메서드를 호출 합니다.

JavaScript 클라이언트를 통해 허브에서 공용 메서드를 호출 합니다 [호출](/javascript/api/%40aspnet/signalr/hubconnection#invoke) 메서드는 [HubConnection](/javascript/api/%40aspnet/signalr/hubconnection)합니다. `invoke` 메서드는 두 인수를 허용 합니다.

* 허브 메서드의 이름입니다. 다음 예제에서는 메서드 허브 이름은 `SendMessage`합니다.
* 허브 메서드에 정의 된 모든 인수입니다. 다음 예제에서는 인수 이름은 `message`합니다.

  [!code-javascript[Call hub methods](javascript-client/sample/wwwroot/js/chat.js?range=24)]

## <a name="call-client-methods-from-hub"></a>허브에서 클라이언트 메서드를 호출

허브에서 메시지를 받으려면 사용 하는 메서드를 정의 합니다 [에](/javascript/api/%40aspnet/signalr/hubconnection#on) 메서드는 `HubConnection`합니다.

* JavaScript 클라이언트 메서드의 이름입니다. 다음 예제에서는 메서드 이름은 `ReceiveMessage`합니다.
* 허브 메서드에 전달 된 인수입니다. 다음 예제에서는 인수 값은 `message`합니다.

[!code-javascript[Receive calls from hub](javascript-client/sample/wwwroot/js/chat.js?range=14-19)]

위의 코드에서 `connection.on` 서버 쪽 코드를 사용 하 여 호출 될 때 실행 되는 [SendAsync](/dotnet/api/microsoft.aspnetcore.signalr.clientproxyextensions.sendasync) 메서드.

[!code-csharp[Call client-side](javascript-client/sample/hubs/chathub.cs?range=8-11)]

SignalR 클라이언트 호출할 메서드를 메서드 이름을 일치 시켜를 결정 하 고에 정의 된 인수 `SendAsync` 고 `connection.on`입니다.

> [!NOTE]
> 호출 하는 것이 좋습니다 합니다 [시작](/javascript/api/%40aspnet/signalr/hubconnection#start) 메서드는 `HubConnection` 후 `on`합니다. 이렇게 하면 모든 메시지를 수신 하기 전에 처리기 등록 됩니다.

## <a name="error-handling-and-logging"></a>오류 처리 및 로깅

체인을 `catch` 의 끝에 메서드를 `start` 클라이언트 쪽 오류를 처리 하는 방법입니다. 사용 하 여 `console.error` 브라우저의 콘솔에 출력 오류입니다.

[!code-javascript[Error handling](javascript-client/sample/wwwroot/js/chat.js?range=28)]

연결이 설정 되 면 로그로 거와 이벤트의 형식을 전달 하 여 클라이언트 쪽 로그 추적을 설정 합니다. 지정 된 로그 수준을 사용 하 여 이상 메시지가 기록 됩니다. 사용 가능한 로그 수준은 아래와 같습니다.

* `signalR.LogLevel.Error` &ndash; 오류 메시지입니다. 로그 `Error` 메시지만 해당 합니다.
* `signalR.LogLevel.Warning` &ndash; 잠재적 오류에 대 한 경고 메시지입니다. 로그 `Warning`, 및 `Error` 메시지입니다.
* `signalR.LogLevel.Information` &ndash; 오류 없이 상태 메시지입니다. 로그 `Information`하십시오 `Warning`, 및 `Error` 메시지입니다.
* `signalR.LogLevel.Trace` &ndash; 메시지를 추적 합니다. 허브와 클라이언트 간에 전송 되는 데이터를 포함 하 여 모든 기록 합니다.

사용 된 [configureLogging](/javascript/api/%40aspnet/signalr/hubconnectionbuilder#configurelogging) 메서드를 [HubConnectionBuilder](/javascript/api/%40aspnet/signalr/hubconnectionbuilder) 로그 수준을 구성 하려면. 메시지는 브라우저 콘솔에 기록 됩니다.

[!code-javascript[Logging levels](javascript-client/sample/wwwroot/js/chat.js?range=9-12)]

## <a name="related-resources"></a>관련 참고 자료

* [JavaScript API 참조](/javascript/api/)
* [허브](xref:signalr/hubs)
* [.NET 클라이언트](xref:signalr/dotnet-client)
* [Azure에 게시](xref:signalr/publish-to-azure-web-app)
* [ASP.NET Core에서 원본 간 요청 (CORS)를 사용 하도록 설정](xref:security/cors)
