---
uid: signalr/overview/getting-started/introduction-to-signalr
title: SignalR 소개 | Microsoft Docs
author: pfletcher
description: 이 문서에서는 설명 SignalR 이란, 일부 솔루션을 만들도록 설계 되었습니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: 0fab5e35-8c1f-43d4-8635-b8aba8766a71
ms.technology: dotnet-signalr
msc.legacyurl: /signalr/overview/getting-started/introduction-to-signalr
msc.type: authoredcontent
ms.openlocfilehash: 0798f149b25ab34dfc9b4233e74dc575ef0e7b4d
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37364121"
---
<a name="introduction-to-signalr"></a>SignalR 소개
====================
[Patrick Fletcher](https://github.com/pfletcher)

> 이 문서에서는 설명 SignalR 이란, 일부 솔루션을 만들도록 설계 되었습니다. 
> 
> ## <a name="questions-and-comments"></a>질문이 나 의견이 있으면
> 
> 이 자습서를 연결 하는 방법 및 새로운 개선할 수 있습니다 페이지의 맨 아래에 의견에서에 의견을 남겨 주세요. 에 자습서로 직접 관련 되지 않은 질문이 있을 경우 게시할 수 하는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr)합니다.


## <a name="what-is-signalr"></a>SignalR 이란?

ASP.NET SignalR은 ASP.NET 개발자를 위한 응용 프로그램에 실시간 웹 기능을 추가 하는 프로세스를 간소화 하는 라이브러리입니다. 실시간 웹 기능은 서버 코드 푸시를 사용할 수 있게 되 면 즉시 연결 된 클라이언트에 콘텐츠 대신 서버는 클라이언트가 새 데이터를 요청을 대기 하는 기능을 합니다.

SignalR은 ASP.NET 응용 프로그램에 모든 종류의 "실시간" 웹 기능을 추가 하려면 사용할 수 있습니다. 예를 들어 채팅 흔히 하는 동안 더 많은 작업을 수행할 수 있습니다. 페이지 구현 또는 사용자 든 지 새 데이터를 보려면 웹 페이지를 새로 고칩니다 [긴 폴링](http://en.wikipedia.org/wiki/Push_technology#Long_polling) 새 데이터를 검색 하려면 SignalR을 사용 하 여에 대 한 대상 인지 합니다. 예로 대시보드 및 진행 상황 업데이트 및 실시간 양식 (예: 동시 편집 문서의) 공동 작업 응용 프로그램 작업 응용 프로그램을 모니터링 합니다.

SignalR 있습니다 완전히 새로운 유형의 웹 응용 프로그램 서버에서 자주 업데이트 해야 하는 예를 들어, 실시간 게임입니다.

SignalR 서버 쪽.NET 코드에서 브라우저 (및 다른 클라이언트 플랫폼) 클라이언트에서 JavaScript 함수를 호출 하는 서버와 클라이언트 간 원격 프로시저 호출 (RPC)을 만들기 위한 간단한 API를 제공 합니다. 또한 SignalR 연결 관리에 대 한 API를 포함 (예를 들어, 연결 및 연결 끊기 이벤트) 및 연결을 그룹화 합니다.

![SignalR 사용 하 여 메서드를 호출합니다.](introduction-to-signalr/_static/image1.png)

SignalR 연결 관리를 자동으로 처리 하 고는 대화방 같은 각 항목 수 브로드캐스트 메시지 연결 된 모든 클라이언트를 동시에 있습니다. 또한 특정 클라이언트에 메시지를 보낼 수 있습니다. 클라이언트와 서버 간의 연결이 영구적 이므로, 각 통신에 대 한 연결이 다시 설정 하는 클래식 HTTP 연결을 달리 합니다.

SignalR은 클라이언트 코드를 사용 하 여 일반적인 요청-응답 모델 보다는 원격 프로시저 호출 (RPC)는 웹에서 현재 브라우저에서 서버 코드 호출할 수 있습니다 "서버 푸시" 기능을 지원 합니다.

SignalR 응용 프로그램의 Service Bus, SQL Server를 사용 하 여 클라이언트를 확장할 수 또는 [Redis](http://redis.io)합니다.

SignalR은 오픈 소스를 통해 액세스할 수 있습니다 [GitHub](https://github.com/signalr)합니다.

## <a name="signalr-and-websocket"></a>SignalR 및 WebSocket

SignalR 사용 가능한 경우 새 WebSocket 전송 사용 및 필요한 경우 이전 전송으로 대체 합니다. 하지만 물론 직접 WebSocket을 사용 하 여, 추가 기능을 구현 해야 합니다. 많은 이미 완료 된를 즉 SignalR을 사용 하 여 응용 프로그램을 작성할 수 있습니다. 가장 중요 한 점은이 이전 버전의 클라이언트에 대 한 별도 코드 경로 생성 하는 방법에 대 한 걱정 없이 WebSocket을 활용 하려면 응용 프로그램을 코딩할 수 있습니다 의미 합니다. SignalR도 보호 SignalR 계속 기본 전송에 대 한 변경을 지원 하도록 업데이트 되어야 WebSocket의 버전 간에 응용 프로그램을 일관 된 인터페이스를 제공 하므로 WebSocket에 대 한 업데이트에 걱정할 필요가 없도록 합니다.

확실히만 WebSocket을 사용 하는 솔루션을 만들 수 있습니다, 있지만 SignalR은 모든 다른 전송 및 WebSocket 구현에 업데이트에 대 한 응용 프로그램을 수정 하는 대체 (fallback)와 같은 사용자가 직접 작성 해야 하는 기능을 제공 합니다.

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a>전송 및 대체

SignalR은 클라이언트와 서버 간의 실시간 작업을 수행 하는 데 필요한 전송의 몇 가지 추상화입니다. SignalR 연결 HTTP로 시작 하 고 가능한 경우에 WebSocket 연결을 다음 승격 됩니다. 서버 메모리의 가장 효율적인 사용, 낮은 대기 시간, 고 (예: 완전 한 이중 클라이언트와 서버 간 통신), 기능이 가장 기본 뿐만 아니라 가장 엄격한 되므로 WebSocket는 SignalR에 대 한 이상적인 전송 요구 사항: WebSocket을 사용 하려면 Windows Server 2012 또는 Windows 8 및.NET Framework 4.5로 서버. 이러한 요구 사항을 충족 되지 않으면, SignalR 연결 되도록 다른 전송을 사용 하려고 합니다.

### <a name="html-5-transports"></a>HTML 5 전송

이러한 전송에 대 한 지원에 따라 달라 집니다 [HTML 5](http://en.wikipedia.org/wiki/HTML5)합니다. 클라이언트 브라우저는 html5 표준을 지원 하지 않으면, 이전 전송이 됩니다.

- **WebSocket** (하는 경우는 Websocket을 지원할 수 있는 서버 및 브라우저 표시). WebSocket은 클라이언트와 서버 간에 true 영구 양방향 연결을 설정 하는 유일한 전송 됩니다. 그러나, WebSocket에 요구 사항이 가장 엄격한; Microsoft Internet Explorer, Google Chrome 및 Mozilla Firefox의 최신 버전에만 완전히 지원 되 고 Opera 및 Safari와 같은 다른 브라우저에 부분적으로 구현만 합니다.
- **서버 전송 이벤트**EventSource (브라우저에서 지 원하는 경우 서버 전송 이벤트는 기본적으로 Internet Explorer를 제외한 모든 브라우저)로 알려진,

### <a name="comet-transports"></a>Comet 전송

다음 전송에 기반한 합니다 [Comet](http://en.wikipedia.org/wiki/Comet_(programming)) 브라우저 또는 다른 클라이언트 유지 관리 하는 장기 보관 HTTP 요청을 서버에 특히 클라이언트는 클라이언트에 데이터 푸시를 사용할 수 있는 웹 응용 프로그램 모델 요청 합니다.

- **프레임 영원히** (예: Internet Explorer에만 해당). 영원히 프레임 완료 되지 않은 서버에서 끝점에 요청을 수행 하는 숨겨진된 IFrame을 만듭니다. 서버는 다음 스크립트가 클라이언트에 서버에서 단방향 실시간 연결을 제공 하는 즉시 실행 하는 클라이언트에 지속적으로 전송 됩니다. 서버에 클라이언트에서 연결에서 클라이언트 연결을 서버에서 별도 연결을 사용 하 고 같은 표준 HTTP 요청을 전송 해야 하는 데이터의 각 부분에 대 한 새 연결을 만들어집니다.
- **긴 폴링 Ajax**합니다. 긴 폴링 영구 연결을 만들지는 않지만 대신이 시점에서 연결이 닫히고 서버 응답 하 고 새 연결을 즉시 요청 될 때까지 열린 상태로 유지 하는 요청을 사용 하 여 서버를 폴링합니다. 연결 다시 설정 하는 동안 약간의 대기 시간이 발생할 수 있습니다.

어떤 전송 되는 구성에서 지원 되는 자세한 내용은 [지원 되는 플랫폼](supported-platforms.md)합니다.

### <a name="transport-selection-process"></a>전송 선택 프로세스

다음 목록에는 SignalR 사용할 전송을 결정 하는 데 사용 하는 단계를 보여 줍니다.

1. 브라우저를 Internet Explorer 8 이하의 경우 긴 폴링 사용 됩니다.
2. JSONP 구성 된 경우 (즉, 합니다 `jsonp` 매개 변수는 설정 `true` 연결을 시작할 때), 되 긴 폴링.
3. (즉, SignalR 끝점에에서 없는 경우 호스팅 페이지와 동일한 도메인)는 도메인 간 연결이 설정 되는 경우 다음 WebSocket 사용한 다음 기준이 충족 될 경우:

   - 클라이언트에서 CORS (크로스-원본 자원 공유)을 지원 합니다. 클라이언트는 CORS를 지원 세부 정보를 참조 하세요 [caniuse.com에서 CORS](http://www.caniuse.com/CORS)합니다.
   - 클라이언트에서 WebSocket을 지원합니다.
   - 서버에서 WebSocket을 지원합니다.

     이러한 조건 중 하나라도 충족 되지 않는 경우 긴 폴링 사용 됩니다. 도메인 간 연결에 대 한 자세한 내용은 참조 하세요. [도메인 간 연결을 설정 하는 방법을](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)합니다.
4. JSONP 구성 되지 않은 경우 연결이 아닙니다. 도메인 간 WebSocket 클라이언트와 서버 모두에서 지 원하는 경우 사용 됩니다.
5. 클라이언트 또는 서버에는 WebSocket을 지원 하지 않으면, 사용 가능한 경우 이벤트를 전송 하는 서버 사용 됩니다.
6. 이벤트를 전송 하는 서버를 사용할 수 없는 경우 계속 프레임 시도 됩니다.
7. 프레임 계속 실패 하면 긴 폴링 사용 됩니다.

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a>전송 모니터링

응용 프로그램이 사용자 허브에서 로깅 및 브라우저에서 콘솔 창 열기를 사용 하 여 사용 중인 전송을 확인할 수 있습니다.

브라우저에서 허브의 이벤트에 대 한 로깅을 사용 하려면 다음 명령을 클라이언트 응용 프로그램에 추가 합니다.

`$.connection.hub.logging = true;`

- Internet Explorer에서 F12 키를 눌러 개발자 도구를 열고 콘솔 탭을 클릭 합니다.

    ![Microsoft Internet Explorer에서 콘솔](introduction-to-signalr/_static/image2.png)
- Chrome에서는 Ctrl + Shift + J를 눌러 콘솔을 엽니다.

    ![Google Chrome에서 콘솔](introduction-to-signalr/_static/image3.png)

콘솔 열기 및 로깅을 사용 하도록 설정, 사용 하 여 SignalR에서 사용 되는 전송 확인할 수 있습니다.

![Internet Explorer WebSocket 전송이 보여 주는 콘솔](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a>전송 지정

전송 협상 리소스 일정량의 시간과 클라이언트/서버를 사용 합니다. 클라이언트 기능에 알고 있는 경우 다음 전송 때 지정할 수 있습니다 클라이언트 연결을 시작 합니다. 다음 코드 조각은 클라이언트가 다른 프로토콜을 지원 하지 않은 것이 던 경우에 사용 되는 대로 Ajax 긴 폴링 전송을 사용 하 여 연결을 시작 하는 방법을 보여 줍니다.

`connection.start({ transport: 'longPolling' });`

시도 하도록 클라이언트를 순서 대로 특정 전송 하려는 경우 대체 (fallback) 순서를 지정할 수 있습니다. 다음 코드 조각은 동안 WebSocket을 실패 하는 긴 폴링으로 직접 이동 하는 방법을 보여 줍니다.

`connection.start({ transport: ['webSockets','longPolling'] });`

전송을 지정 하는 것에 대 한 문자열 상수는 다음과 같이 정의 됩니다.

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a>연결 및 허브

클라이언트와 서버 간의 통신을 위한 두 가지 모델을 포함 하는 SignalR API: 허브 및 영구 연결 합니다.

연결에는 간단한 단일 받는 사람, 그룹화 또는 브로드캐스트 메시지를 보낼 끝점을 나타냅니다. 개발자는 SignalR 노출 하는 하위 수준 통신 프로토콜에 대 한 액세스를 직접 (PersistentConnection 클래스에 의해.NET 코드에 표시 됨) 영구 연결 API 제공 합니다. 연결 통신 모델을 사용 하 여 Windows Communication Foundation 같은 연결 기반 Api를 사용한 적이 있는 개발자에 게 친숙 한 됩니다.

허브는 클라이언트 및 서버에서 서로 다른 메서드를 직접 호출할 수 있도록 연결 API를 기반으로 보다 높은 수준의 파이프라인. 클라이언트가 서버에서 로컬 메서드로 쉽게 이동 하 고 그 반대의 경우로 메서드를 호출 하도록 허용 매직에서 작업 하는 것 처럼 컴퓨터 경계를 넘어 디스패치 SignalR에서 처리 합니다. 허브 통신 모델을 사용 하 여 원격 호출.NET Remoting 등의 Api를 사용한 적이 있는 개발자에 게 친숙 한 됩니다. 또한 허브를 사용 하 여 모델 바인딩을 사용 하도록 설정 하는 메서드에 강력한 형식의 매개 변수를 전달할 수 있습니다.

### <a name="architecture-diagram"></a>아키텍처 다이어그램

다음 다이어그램은 허브, 영구 연결 및 전송에 사용 되는 기본 기술 간의 관계를 보여줍니다.

![Api, 전송 및 클라이언트를 보여 주는 SignalR 아키텍처 다이어그램](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a>허브의 작동 방식

클라이언트에서 메서드를 호출 하는 서버 쪽 코드, 이름 및 호출할 메서드의 매개 변수를 포함 하는 활성 전송에서 패킷을 전송 됩니다 (개체 메서드 매개 변수로 보내면 serialize 된 JSON을 사용 하 여). 클라이언트에는 다음 클라이언트 쪽 코드에 정의 된 메서드를 메서드 이름과 일치 합니다. 일치 하는 클라이언트 메서드는 deserialize 된 매개 변수 데이터를 사용 하 여 실행 됩니다.

메서드 호출 수와 같은 도구를 사용 하 여 모니터링할 [Fiddler.](http://fiddler2.com/) 다음 이미지에는 Fiddler의 로그 창에서 웹 브라우저 클라이언트에 SignalR 서버에서 전송 하는 메서드 호출을 보여 줍니다. 허브 호출에서 전송 되는 메서드 호출 `MoveShapeHub`를 호출할 메서드를 호출 하 고 `updateShape`입니다.

![SignalR 트래픽을 보여 주는 Fiddler 로그 보기](introduction-to-signalr/_static/image6.png)

이 예제에서는 허브 이름으로 식별 됩니다는 `H` 매개 변수; 메서드를 이름으로 식별 됩니다를 `M` 메서드에 전송 되는 데이터 및 매개 변수를 사용 하 여 식별 되는 `A` 매개 변수. 이 메시지를 생성 하는 응용 프로그램에서 만들어진 합니다 [고주파수](tutorial-high-frequency-realtime-with-signalr.md) 자습서입니다.

### <a name="choosing-a-communication-model"></a>통신 모델 선택

대부분의 응용 프로그램 허브 API를 사용 해야 합니다. 다음과 같은 경우에는 연결 API는 사용할 수 있습니다.

- 형식 지정 보낸 실제 메시지 요구 사항입니다.
- 개발자는 원격 호출 모델 보다는 메시징 및 디스패치 모델을 사용 하 여 작업을 선호 합니다.
- SignalR을 사용 하는 메시징 모델을 사용 하는 기존 응용 프로그램 이식 중인 합니다.
