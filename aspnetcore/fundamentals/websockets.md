---
title: "ASP.NET Core의 Websocket 지원"
author: tdykstra
description: "ASP.NET Core에서 Websocket을 시작하는 방법을 알아봅니다."
keywords: ASP.NET Core, WebSockets
ms.author: tdykstra
manager: wpickett
ms.date: 03/25/2017
ms.topic: article
ms.assetid: 0e0fedcd-a7b4-4479-8ae0-36eab0229d7e
ms.technology: aspnet
ms.prod: aspnet-core
uid: fundamentals/websockets
ms.openlocfilehash: 114d52d831668e5facd1142b5f9e5f68e7456f7e
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
# <a name="introduction-to-websockets-in-aspnet-core"></a>ASP.NET Core의 Websocket 살펴보기

작성자: [Tom Dykstra](https://github.com/tdykstra) 및 [Andrew Stanton-Nurse](https://github.com/anurse)

본문에서는 ASP.NET Core에서 Websocket을 사용하는 방법을 알아봅니다. [WebSocket](https://wikipedia.org/wiki/WebSocket)은 TCP 연결을 통해서 지속적인 양방향 통신 채널을 사용할 수 있도록 해주는 프로토콜입니다. 채팅, 주식 전광판, 게임 등 웹 응용 프로그램 전반에서 실시간 기능이 필요한 모든 곳에 활용됩니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample) ([다운로드 방법](xref:tutorials/index#how-to-download-a-sample)). 예제 코드에 관한 보다 자세한 내용은 [다음 단계](#next-steps) 섹션을 참고하시기 바랍니다.


## <a name="prerequisites"></a>전제 조건

* ASP.NET Core 1.1 (1.0에서는 동작하지 않습니다.)
* ASP.NET Core가 실행되는 모든 OS:
  
  * Windows 7 / Windows Server 2008 이상
  * Linux
  * MacOS

* **예외**: Windows에서 IIS 또는 WebListener를 통해서 응용 프로그램을 실행한다면 다음을 만족해야 합니다:

  * Windows 8 / Windows Server 2012 이상
  * IIS 8 / IIS 8 Express
  * IIS에서 WebSocket을 활성화시켜야 합니다.

* WebSocket 지원 브라우저에 관한 정보는 http://caniuse.com/#feat=websockets을 참고하시기 바랍니다.

## <a name="when-to-use-it"></a>용도

소켓 연결을 통해서 직접 작업을 처리해야 할 때, Websocket을 사용할 수 있습니다. 예를 들어, 실시간 게임에서 최상의 성능이 필요할 수도 있습니다.

[ASP.NET SignalR](https://docs.microsoft.com/aspnet/signalr/overview/getting-started/introduction-to-signalr)은 실시간 기능을 지원하는 보다 풍부한 응용 프로그램 모델을 제공하지만 ASP.NET에서만 실행되며 ASP.NET Core에서는 사용할 수 없습니다. SignalR의 Core 버전은 현재 개발중으로, 개발 진행 상황을 확인하려면 [SignalR Core의 GitHub 저장소](https://github.com/aspnet/SignalR)를 참고하시기 바랍니다.

SignalR Core를 기다리고 싶지 않다면, 대신 지금 바로 WebSocket을 사용할 수 있습니다. 그러나 SignalR이 제공하는 다음과 같은 기능들을 직접 개발해야 할 수도 있습니다:

* 대체 전송 방식에 대한 자동 폴백을 통해서 보다 다양한 브라우저 버전을 지원합니다.
* 연결이 끊어지면 자동으로 다시 연결합니다.
* 서버의 메서드를 호출하는 클라이언트, 또는 반대로 클라이언트의 메서드를 호출하는 서버를 지원합니다.
* 복수 서버에 대한 확장을 지원합니다.

## <a name="how-to-use-it"></a>사용 방법

* [Microsoft.AspNetCore.WebSockets](https://www.nuget.org/packages/Microsoft.AspNetCore.WebSockets/) 패키지를 설치합니다.
* 미들웨어를 구성합니다.
* WebSocket 요청을 수락합니다.
* 메시지를 전송 및 수신합니다.

### <a name="configure-the-middleware"></a>미들웨어 구성하기

`Startup` 클래스의 `Configure` 메서드에서 Websocket 미들웨어를 추가합니다.

[!code-csharp[](websockets/sample/Startup.cs?name=UseWebSockets)]

이때 다음과 같은 설정을 구성할 수 있습니다.

* `KeepAliveInterval` - 프록시가 클라이언트의 연결을 유지할 수 있도록 클라이언트로 "핑(ping)" 프레임을 전송하는 빈도입니다.
* `ReceiveBufferSize` - 데이터 수신에 사용되는 버퍼의 크기입니다. 이 값은 데이터의 크기에 기반한 성능 튜닝이 필요할 경우, 고급 사용자만 변경하는 것이 좋습니다.

[!code-csharp[](websockets/sample/Startup.cs?name=UseWebSocketsOptions)]

### <a name="accept-websocket-requests"></a>WebSocket 요청 수락하기

요청 수명 주기의 뒷부분에서 (예를 들어, `Configure` 메서드나 MVC 액션의 뒷부분에서) WebSocket 요청 여부를 확인하고 WebSocket 요청을 수락합니다.

다음 예제는 `Configure` 메서드의 뒷부분에 위치합니다.

[!code-csharp[](websockets/sample/Startup.cs?name=AcceptWebSocket&highlight=7)]

WebSocket 요청은 모든 URL을 통해서 전달될 수 있지만, 이 예제 코드에서는 `/ws`에 대한 요청만 수락합니다.

### <a name="send-and-receive-messages"></a>메시지 전송 및 수신하기

`AcceptWebSocketAsync` 메서드는 TCP 연결을 WebSocket 연결로 업그레이드하고 [WebSocket](https://docs.microsoft.com/dotnet/core/api/system.net.websockets.websocket) 개체를 반환합니다. 이 WebSocket 개체를 이용해서 메시지를 전송하거나 수신합니다.

앞에서 살펴본 WebSocket 요청을 수락하는 코드는 `WebSocket` 개체를 `Echo` 메서드로 전달하는데, `Echo` 메서드의 코드는 다음과 같습니다. 이 코드는 메시지를 수신하고 즉시 동일한 메시지를 다시 송신합니다. 그리고 클라이언트가 연결을 닫을 때까지 루프를 반복합니다.

[!code-csharp[](websockets/sample/Startup.cs?name=Echo)]

루프가 시작되기 전에 WebSocket을 수락하면 미들웨어 파이프라인이 종료됩니다. 그리고 소켓을 닫으면 파이프라인이 풀립니다. 다시 말해서, 마치 MVC 액션을 실행할 때와 마찬가지로 WebSocket을 수락하면 요청이 파이프라인에서 더 이상 앞쪽으로 이동하지 않습니다. 그러나 이 루프를 종료하고 소켓을 닫으면 파이프라인을 통해서 요청이 다시 처리됩니다.

## <a name="next-steps"></a>다음 단계

본문과 함께 제공되는 [예제 응용 프로그램](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample)은 간단한 에코 응용 프로그램입니다. WebSocket 연결을 생성하는 웹 페이지가 제공되며 서버는 수신한 메시지를 그대로 클라이언트로 재전송합니다. 명령 프롬프트에서 예제 응용 프로그램을 실행하고 (Visual Studio에서 IIS Express를 통해서 실행되도록 구성되지 않았습니다), 브라우저에서 http://localhost:5000으로 이동합니다. 웹 페이지의 좌상단에는 현재 연결 상태가 출력됩니다.

![웹 페이지의 초기 상태](websockets/_static/start.png)

**Connect**를 선택해서 지정한 URL로 WebSocket 요청을 전송합니다. 그리고 테스트 메시지를 입력한 다음 **Send**를 선택합니다. 테스트를 모두 마쳤으면 **Close Socket**을 선택하십시오. **Communication Log** 섹션에는 각각의 열기, 전송 및 닫기 동작이 발생한 순서대로 나타납니다.

![웹 페이지의 초기 상태](websockets/_static/end.png)
