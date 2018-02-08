---
title: "ASP.NET Core에서 WebSocket 지원"
author: tdykstra
description: "ASP.NET Core에서 WebSocket을 시작하는 방법을 알아봅니다."
manager: wpickett
ms.author: tdykstra
ms.date: 03/25/2017
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/websockets
ms.openlocfilehash: 306eca28b9f1f66e1ccaf185ccae87db8dea1b01
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="introduction-to-websockets-in-aspnet-core"></a>ASP.NET Core에서 WebSocket 소개

작성자: [Tom Dykstra](https://github.com/tdykstra) 및 [Andrew Stanton-Nurse](https://github.com/anurse)

이 문서는 ASP.NET Core에서 WebSocket을 시작하는 방법을 설명합니다. [WebSocket](https://wikipedia.org/wiki/WebSocket)은 TCP 연결을 통한 영구 양방향 통신 채널을 사용하도록 설정하는 프로토콜이며 채팅, 주식 종목, 게임, 웹 응용 프로그램의 실시간 기능을 사용하려는 곳 등 응용 프로그램에 사용됩니다.

[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample)) 자세한 내용은 [다음 단계](#next-steps) 섹션을 참조하세요.


## <a name="prerequisites"></a>필수 구성 요소

* ASP.NET Core 1.1(1.0에서 실행되지 않음)
* ASP.NET Core를 실행하는 OS:
  
  * Windows 7 / Windows Server 2008 이상
  * Linux
  * macOS

* **예외**: 앱이 IIS 또는 WebListener와 함께 Windows에서 실행되는 경우 다음을 사용해야 합니다.

  * Windows 8 / Windows Server 2012 이상
  * IIS 8 / IIS 8 Express
  * WebSocket은 IIS에서 활성화되어야 함

* 지원되는 브라우저는 http://caniuse.com/#feat=websockets를 참조하세요.

## <a name="when-to-use-it"></a>용도

소켓 연결로 직접 작업해야 하는 경우 WebSocket을 사용합니다. 예를 들어 실시간 게임에 최상의 가능한 성능이 필요할 수 있습니다.

[ASP.NET SignalR](https://docs.microsoft.com/aspnet/signalr/overview/getting-started/introduction-to-signalr)은 실시간 기능에 대한 풍부한 응용 프로그램 모델을 제공하지만 ASP.NET Core가 아닌 ASP.NET에서만 실행됩니다. SignalR의 핵심 버전은 해당 진행을 따르도록 개발 중이며 [SignalR Core용 GitHub 리포지토리](https://github.com/aspnet/SignalR)를 참조하세요.

SignalR Core를 기다리지 않으려는 경우 이제 WebSocket을 직접 사용할 수 있습니다. 하지만 다음과 같은 SignalR에서 제공하는 기능을 개발해야 할 수 있습니다.

* 대체 전송 방법에 대한 자동 대체를 사용하여 광범위한 브라우저 버전에 대한 지원
* 연결이 끊어지는 경우 자동 다시 연결
* 서버에서 메서드(또는 그 반대로)를 호출하는 클라이언트에 대한 지원
* 여러 서버에 맞게 크기 조정에 대한 지원

## <a name="how-to-use-it"></a>사용 방법

* [Microsoft.AspNetCore.WebSockets](https://www.nuget.org/packages/Microsoft.AspNetCore.WebSockets/) 패키지를 설치합니다.
* 미들웨어를 구성합니다.
* WebSocket 요청을 수락합니다.
* 메시지를 보내고 받습니다.

### <a name="configure-the-middleware"></a>미들웨어 구성

`Startup` 클래스의 `Configure` 메서드에 WebSocket 미들웨어를 추가합니다.

[!code-csharp[](websockets/sample/Startup.cs?name=UseWebSockets)]

다음 설정을 구성할 수 있습니다.

* `KeepAliveInterval` - 프록시 연결을 유지하도록 클라이언트에 "ping" 프레임을 보낼 빈도
* `ReceiveBufferSize` - 데이터를 수신하는 데 사용되는 버퍼의 크기 고급 사용자만 자신의 데이터의 크기에 따라 성능 튜닝에 대해 이를 변경해야 합니다.

[!code-csharp[](websockets/sample/Startup.cs?name=UseWebSocketsOptions)]

### <a name="accept-websocket-requests"></a>WebSocket 요청 수락

요청 수명 주기의 뒷부분(예: `Configure` 메서드 또는 MVC 동작의 뒷부분)에서 WebSocket 요청인지 확인하고 WebSocket 요청을 수락합니다.

이 예제는 `Configure` 메서드의 뒷부분에 포함되어 있습니다.

[!code-csharp[](websockets/sample/Startup.cs?name=AcceptWebSocket&highlight=7)]

WebSocket 요청은 모든 URL에서 올 수도 있지만 이 샘플 코드는 `/ws`에 대한 요청만 허용합니다.

### <a name="send-and-receive-messages"></a>메시지 보내기 및 받기

`AcceptWebSocketAsync` 메서드는 WebSocket 연결에 대한 TCP 연결을 업그레이드하고 [WebSocket](https://docs.microsoft.com/dotnet/core/api/system.net.websockets.websocket) 개체를 제공합니다. WebSocket 개체를 사용하여 메시지를 보내고 받습니다.

WebSocket 요청을 수락하는 앞에 표시된 코드에서 `WebSocket` 개체를 `Echo` 메서드에 전달합니다. 여기서는 `Echo` 메서드입니다. 코드는 메시지를 수신하고 동일한 메시지를 즉시 보냅니다. 클라이언트가 연결을 닫을 때까지 작업을 수행하는 루프에 유지됩니다. 

[!code-csharp[](websockets/sample/Startup.cs?name=Echo)]

이 루프를 시작하기 전에 WebSocket을 수락하면 미들웨어 파이프라인이 종료됩니다.  소켓을 닫을 때 파이프라인이 해제됩니다. 즉, 예를 들어 MVC 작업을 적중할 때 수행하는 것과 마찬가지로 WebSocket을 수락하면 요청은 파이프라인에서 앞으로 이동을 중지합니다.  하지만 이 루프를 마치고 소켓을 닫으면 요청에서 파이프라인 백업을 진행합니다.

## <a name="next-steps"></a>다음 단계

이 문서와 함께 제공되는 [샘플 응용 프로그램](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/websockets/sample)은 간단한 에코 응용 프로그램입니다. WebSocket 연결을 설정하는 웹 페이지가 있으며 서버는 수신하는 모든 메시지를 클라이언트에 다시 전송하기만 합니다. 명령 프롬프트에서 실행하고(IIS Express로 Visual Studio에서 실행하도록 설정되지 않음) http://localhost:5000으로 이동합니다. 웹 페이지는 왼쪽 위에 연결 상태를 보여 줍니다.

![웹 페이지의 초기 상태](websockets/_static/start.png)

**연결**을 선택하여 표시된 URL에 WebSocket 요청을 보냅니다.  테스트 메시지를 입력하고 **보내기**를 선택합니다. 완료한 후 **소켓 닫기**를 선택합니다. **통신 로그** 섹션은 발생하는 대로 열기, 보내기 및 닫기 작업을 보고합니다.

![웹 페이지의 초기 상태](websockets/_static/end.png)
