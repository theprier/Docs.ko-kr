---
title: ASP.NET SignalR JavaScript 코어 클라이언트
author: rachelappel
description: ASP.NET Core SignalR JavaScript 클라이언트 간략하게 설명 합니다.
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 04/06/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: signalr/javascript-client
ms.openlocfilehash: cca1a523bd536f4365e54c196f6c9024779d5d76
ms.sourcegitcommit: c79fd3592f444d58e17518914f8873d0a11219c0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="aspnet-core-signalr-javascript-client"></a>ASP.NET SignalR JavaScript 코어 클라이언트

작성자: [Rachel Appel](http://twitter.com/rachelappel)

[!INCLUDE [2.1 preview notice](~/includes/2.1.md)]

ASP.NET Core SignalR JavaScript 클라이언트 라이브러리를 사용 하면 서버 쪽 허브 코드를 호출할 수 있습니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/live/aspnetcore/signalr/javascript-client/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="install-the-signalr-client-package"></a>SignalR 클라이언트 패키지를 설치 합니다.

SignalR JavaScript 클라이언트 라이브러리로 배달 되는 [npm](https://www.npmjs.com/) 패키지 합니다. Visual Studio를 사용 하는 경우 실행 `npm install` 에서 **패키지 관리자 콘솔** 루트 폴더에 있는 동안 합니다. Visual Studio 코드에 대 한에서 명령을 실행 하는 **통합 터미널**합니다.

  ```console
   npm init -y
   npm install @aspnet/signalr
  ```

Npm 설치에서 패키지 콘텐츠는 *node_modules\\ @aspnet\signalr\dist\browser*  폴더입니다. 라는 새 폴더 만들기 *signalr* 아래는 *wwwroot\\lib* 폴더입니다. 복사는 *signalr.js* 파일을 여 *wwwroot\lib\signalr* 폴더입니다.

## <a name="use-the-signalr-javascript-client"></a>SignalR JavaScript 클라이언트 사용

참조에서 SignalR JavaScript 클라이언트는 `<script>` 요소입니다.

```html
<script src="~/lib/signalr/signalr.js"></script>
```

## <a name="connect-to-a-hub"></a>허브에 연결

다음 코드를 만들고 연결을 시작 합니다. 허브의 이름은 대/소문자 구분입니다.

[!code-javascript[Call hub methods](javascript-client/sample/wwwroot/js/chat.js?range=1-2,18)]

### <a name="cross-origin-connections"></a>크로스-원본 연결

일반적으로 브라우저는 요청된 된 페이지와 동일한 도메인에서 연결을 로드합니다. 그러나 다른 도메인에 대 한 연결 필요한 경우 경우가 있습니다.

악성 사이트를 다른 사이트에서 중요 한 데이터를 읽는 하지 않도록 하려면 [크로스-원본 연결](xref:security/cors) 기본적으로 비활성화 됩니다. 크로스-원본 요청을 허용 하려면에서 사용 하도록 설정할는 `Startup` 클래스입니다.

[!code-csharp[Cross-origin connections](javascript-client/sample/Startup.cs?highlight=29-34,55)]

## <a name="call-hub-methods-from-client"></a>클라이언트에서 허브 메서드를 호출 합니다.

JavaScript 클라이언트 공용 메서드를 호출 하 여 허브를 사용 하 여 `connection.invoke`합니다. `invoke` 메서드는 두 인수를 허용 합니다.

* 허브 메서드의 이름입니다. 다음 예에서는 허브 이름은 `SendMessage`합니다.
* 허브 메서드에 정의 된 인수입니다. 다음 예제에서는 인수 이름은 `message`합니다.

[!code-javascript[Call hub methods](javascript-client/sample/wwwroot/js/chat.js?range=14)]

## <a name="call-client-methods-from-hub"></a>허브에서 클라이언트를 메서드 호출

허브에서 메시지를 받으려면 사용 하 여 메서드를 정의 고 `connection.on` 메서드.

* JavaScript 클라이언트 메서드의 이름입니다. 다음 예제에서는 메서드 이름은 `ReceiveMessage`합니다.
* 허브 메서드에 전달 된 인수입니다. 인수 값이 다음 예에서 `message`합니다.

[!code-javascript[Receive calls from hub](javascript-client/sample/wwwroot/js/chat.js?range=4-9)]

위의 코드에서 `connection.on` 서버 쪽 코드를 사용 하 여 호출할 때 실행 되는 `SendAsync` 메서드.

[!code-javascript[Call client-side](javascript-client/sample/hubs/chathub.cs?range=8-11)]

SignalR 메서드 이름과 일치 하 여 호출 클라이언트 방법을 결정 하 고 인수에 정의 된 `SendAsync` 및 `connection.on`합니다.

> [!NOTE]
> 모범 사례로, 호출 `connection.start` 후 `connection.on` 모든 메시지를 수신 하기 전에 처리기를 등록 됩니다.

## <a name="error-handling-and-logging"></a>오류 처리 및 로깅

체인을 `catch` 끝날 때까지 메서드는 `connection.start` 클라이언트 오류를 처리 하는 메서드. 사용 하 여 `console.error` 브라우저의 콘솔에 출력 오류입니다.

[!code-javascript[Error handling](javascript-client/sample/wwwroot/js/chat.js?range=18)]

연결 되 면 로그로 거와 형식의 이벤트를 전달 하 여 클라이언트 쪽 로그 추적을 설정 합니다. 지정 된 로그 수준으로 및 더 높은 메시지가 기록 됩니다. 사용 가능한 로그는 다음과 같습니다.

* `signalR.LogLevel.Error` : 오류 메시지입니다. 로그 `Error` 만 메시지입니다.
* `signalR.LogLevel.Warning` : 잠재적 오류에 대 한 경고 메시지입니다. 로그 `Warning`, 및 `Error` 메시지입니다.
* `signalR.LogLevel.Information` : 오류 없이 상태 메시지입니다. 로그 `Information`, `Warning`, 및 `Error` 메시지입니다.
* `signalR.LogLevel.Trace` : 메시지를 추적 합니다. 허브와 클라이언트 간에 전송 되는 데이터를 포함 하 여 모든 기록 합니다.

로깅 시작 화면에 연결 된로 거를 전달 합니다. 브라우저 개발자 도구는 일반적으로 메시지를 표시 하는 콘솔을 포함 합니다.

[!code-javascript[Logging levels](javascript-client/sample/wwwroot/js/chat.js?range=1-2)]

## <a name="related-resources"></a>관련 참고 자료

* [ASP.NET Core SignalR 허브](xref:signalr/hubs)
* [ASP.NET Core에서 크로스-원본 요청 (CORS)를 사용 하도록 설정](xref:security/cors)