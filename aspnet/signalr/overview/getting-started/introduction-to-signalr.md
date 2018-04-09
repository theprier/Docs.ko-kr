---
uid: signalr/overview/getting-started/introduction-to-signalr
title: SignalR 소개 | Microsoft Docs
author: pfletcher
description: 이 문서에서는 SignalR, 정의 및 만들기 하도록 설계 된 솔루션 중 일부를 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: 0fab5e35-8c1f-43d4-8635-b8aba8766a71
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/getting-started/introduction-to-signalr
msc.type: authoredcontent
ms.openlocfilehash: 0ceca3edc26d35b1155946e60863a84da0bbe592
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="introduction-to-signalr"></a>SignalR 소개
====================
으로 [Patrick Fletcher](https://github.com/pfletcher)

> 이 문서에서는 SignalR, 정의 및 만들기 하도록 설계 된 솔루션 중 일부를 설명 합니다. 
> 
> ## <a name="questions-and-comments"></a>질문이 나 의견이
> 
> 이 자습서를 연결 하는 방법 및 페이지의 맨 아래에 주석에서 향상 될 수 있습니다 어떻게에 의견을 남겨 주세요. 자습서를 직접 관련 되지 않는 질문 해야 하도록를 게시할 수 있습니다는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr)합니다.


## <a name="what-is-signalr"></a>SignalR 란?

ASP.NET SignalR은 ASP.NET 개발자를 위한 간단 하 게 응용 프로그램에 실시간 웹 기능을 추가 하는 라이브러리입니다. 실시간 웹 기능은 서버 새 데이터를 요청 하는 클라이언트에 대 한 대기 하는 것이 아니라 서버 코드 푸시를 사용할 수 있게 되 면 즉시 연결 된 클라이언트에 콘텐츠를 가질 수 있습니다.

SignalR은 ASP.NET 응용 프로그램에 모든 종류의 "실시간" 웹 기능을 추가 데 사용할 수 있습니다. 채팅은 일반적으로 예를 사용 하는 동안 더 많은 작업을 수행할 수 있습니다. 사용자는 언제 든 지 새 데이터를 보려면 웹 페이지를 새로 고칩니다. 또는 페이지를 구현 [긴 폴링](http://en.wikipedia.org/wiki/Push_technology#Long_polling) 새 데이터를 검색 하려면 SignalR을 사용 하기 위한 대상 인지 합니다. 예로 대시보드 및 진행 상황 업데이트 및 실시간 양식 (예: 동시 편집 문서), 공동 작업 응용 프로그램 작업 응용 프로그램을 모니터링 합니다.

SignalR 해줍니다 완전히 새로운 유형의 웹 응용 프로그램 서버에서 자주 발생 하는 업데이트를 필요로 하는 예를 들어 실시간 게임.

SignalR 서버 쪽.NET 코드에서 브라우저 (및 다른 클라이언트 플랫폼) 클라이언트에서 JavaScript 함수를 호출 하는 서버 클라이언트 원격 프로시저 호출 (RPC)을 만들기 위한 단순 API를 제공 합니다. SignalR API도 포함 되어 연결 관리를 위해 (예를 들어, 연결 및 연결 끊기 이벤트), 연결 그룹화 하 고 있습니다.

![SignalR 사용 하 여 메서드를 호출합니다.](introduction-to-signalr/_static/image1.png)

SignalR 연결 관리를 자동으로 처리 하 고는 대화방 같은 각 항목 수 브로드캐스트 메시지 연결 된 모든 클라이언트에 동시에 있습니다. 특정 클라이언트에 메시지를 보낼 수도 있습니다. 클라이언트와 서버 간의 연결 각 통신을 위해 다시 설정 하는 기본 HTTP 연결을 달리 지속 됩니다.

SignalR을 사용 하 여 일반적인 요청-응답 모델 보다는 원격 프로시저 호출 (RPC)는 웹에서 현재 브라우저에서 클라이언트 코드에 서버 코드 호출할 수 있습니다 "서버 푸시" 기능을 지원 합니다.

SignalR 응용 프로그램의 서비스 버스, SQL Server를 사용 하 여 클라이언트를 확장할 수 있습니다 또는 [Redis](http://redis.io)합니다.

SignalR은 오픈 소스를 통해 액세스할 수 있는 [GitHub](https://github.com/signalr)합니다.

## <a name="signalr-and-websocket"></a>SignalR 및 WebSocket

SignalR를 사용할 수 있는 새 WebSocket 전송 사용 하 고 필요한 경우 이전 전송 하도록 대체 합니다. 대부분 응용 프로그램을 작성할 수는 있지만 직접 WebSocket을 사용 하 여, SignalR을 사용 하 여 구현 해야 하는 추가 기능을 많이 이미 있다는 것을 의미 있는 수행 되었습니다. 가장 중요 한 점은 즉, 이전 버전의 클라이언트에 대 한 별도 코드 경로 만드는 방법에 대해 신경 쓰지 않고 WebSocket을 활용 하도록 응용 프로그램을 코딩할 수 있습니다. SignalR도 보호 있습니다 SignalR WebSocket의 버전 간에 응용 프로그램을 일관 된 인터페이스를 제공 하는 기본 전송에 대 한 변경을 지원 하도록 업데이트 되어야 계속 됩니다 있으므로 WebSocket에 대 한 업데이트에 대해서는 걱정 하지 않아도 됩니다.

확실히만 WebSocket을 사용 하는 솔루션을 만들 수 있습니다, SignalR 같은 다른 전송 및 업데이트에 대 한 WebSocket 구현에 응용 프로그램을 수정 하는 대체 (fallback)를 직접 작성 해야 하는 기능을 모두 제공 합니다.

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a>전송 및 대체

SignalR은 클라이언트와 서버 간의 실시간 작업을 수행 하는 데 필요한 전송 중 일부를 통해 추상화입니다. SignalR 연결 HTTP로 시작 하 고 가능한 경우에 WebSocket 연결 후 승격 됩니다. 서버 메모리의 가장 효율적인 사용, 대기 시간이 가장이 있으며 (예: 양방향 클라이언트와 서버 간 통신)는 가장 기본 기능이 있을 뿐만 아니라 있습니다 가장 엄격한 이후 WebSocket는 SignalR에 대 한 이상적인 전송 요구 사항: WebSocket 서버를 사용 하 여 Windows Server 2012 또는 Windows 8 및.NET Framework 4.5를 필요 합니다. 이러한 요구 사항을 충족 되지 않는 경우에 SignalR 다른 전송의 연결을 사용 하도록 시도 합니다.

### <a name="html-5-transports"></a>HTML 5 전송

이러한 전송에 대 한 지원에 따라 달라 집니다 [HTML 5](http://en.wikipedia.org/wiki/HTML5)합니다. 클라이언트 브라우저에서 HTML 5 표준을 지원 하지 않는 경우 이전 전송 사용 됩니다.

- **WebSocket** (하는 경우는 Websocket 지원할 수 있는 서버와 브라우저 표시). WebSocket은 클라이언트와 서버 간에 true 영구 양방향 연결을 설정 하는 유일한 transport입니다. 그러나 WebSocket도 사항이 가장 엄격한; Microsoft Internet Explorer 및 Google Chrome, Mozilla Firefox 최신 버전에만 완전히 지원 됩니다 하 고에 Opera 및 Safari와 같은 다른 브라우저의 부분적으로 구현 합니다.
- **서버 이벤트 전송**EventSource (브라우저에서 지 원하는 경우 서버 전송 이벤트는 기본적으로 Internet Explorer를 제외한 모든 브라우저) 라고도 합니다

### <a name="comet-transports"></a>Comet 전송

에서는 다음과 같은 전송을 기반으로 [Comet](http://en.wikipedia.org/wiki/Comet_(programming)) 브라우저 또는 다른 클라이언트 유지 하는 서버 특히 클라이언트는 클라이언트에 데이터를 푸시를 사용할 수는 장기 보관 HTTP 요청을 웹 응용 프로그램 모델 요청 합니다.

- **Forever Frame** (예: Internet Explorer에만 해당). 영원히 프레임에 완료 되지 않으면 서버의 끝점에 요청 하는 숨겨진된 IFrame을 만듭니다. 서버는 다음 스크립트는 단방향 실시간 서버에서 클라이언트 연결을 제공 하는 즉시 실행 되는 클라이언트에 지속적으로 보냅니다. 클라이언트 연결을 서버에서 별도 연결을 사용 하는 서버에 클라이언트에서 연결 하 고 같은 표준 HTTP 요청을 전송 해야 하는 데이터의 각 조각에 대 한 새 연결 만들어집니다.
- **Ajax 긴 폴링과**합니다. 긴 폴링 영구 연결을 만들지 않습니다 있지만 대신 이때 연결이 닫힙니다, 서버 응답 하 고 새 연결을 즉시 요청 될 때까지 열린 상태를 유지 하는 요청을 사용 하 여 서버를 폴링합니다. 연결 다시 설정 하는 동안 약간의 대기 시간이 발생할 수 있습니다.

어떤 전송 하는 구성이에서 지원 되는에 대 한 자세한 내용은 참조 하십시오. [지원 되는 플랫폼](supported-platforms.md)합니다.

### <a name="transport-selection-process"></a>전송 선택 프로세스

다음과 같은 사용할 전송을 결정 SignalR을 사용 하는 단계를 보여 줍니다.

1. 브라우저는 Internet Explorer 8 또는 이전 버전, 긴 폴링을 사용 됩니다.
2. JSONP 구성 된 경우 (즉,는 `jsonp` 로 설정 된 `true` 연결이 시작 될 때), 긴 폴링을 사용 됩니다.
3. 도메인 간 연결 되 고 (즉, SignalR 끝점에에서 없는 경우 호스팅 페이지와 같은 도메인)를 만들어지면 다음 WebSocket 사용 됩니다는 다음 조건을 충족 될 경우:

   - 클라이언트에서 CORS (크로스-원본 자원 공유)을 지원 합니다. 클라이언트에 CORS는 지원 세부 정보를 참조 하십시오. [caniuse.com에 CORS](http://www.caniuse.com/CORS)합니다.
   - 클라이언트에서 WebSocket을 지원합니다.
   - 서버에서 WebSocket을 지원합니다.

     이러한 조건 중 하나라도 충족 되지 않는 긴 폴링을 사용 됩니다. 도메인 간 연결에 대 한 자세한 내용은 참조 하십시오. [도메인 간 연결을 설정 하는 방법을](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)합니다.
4. JSONP 구성 되지 않은 경우 연결이 도메인 간 클라이언트와 서버 모두에서 지 원하는 경우 WebSocket 사용 됩니다.
5. 클라이언트 또는 서버에는 WebSocket을 지원 하지 않는, 사용 가능한 경우 서버 전송 이벤트 사용 됩니다.
6. 이벤트를 전송 하는 서버를 사용할 수 없는 프레임 계속 시도 됩니다.
7. 프레임 계속 실패 하면 긴 폴링을 사용 됩니다.

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a>전송 모니터링

응용 프로그램은 브라우저에서 콘솔 창 열기 및 허브에 대 한 로깅을 사용 하 여 사용 하 여 어떤 전송을 확인할 수 있습니다.

브라우저에서 허브의 이벤트에 대 한 로깅을 사용 하려면 클라이언트 응용 프로그램에 다음 명령을 추가 합니다.

`$.connection.hub.logging = true;`

- Internet Explorer에서 F12 키를 눌러 개발자 도구를 열고 콘솔 탭을 클릭 합니다.

    ![Microsoft Internet Explorer에서 콘솔](introduction-to-signalr/_static/image2.png)
- Chrome에서는 Ctrl + Shift + J를 눌러 콘솔을 엽니다.

    ![Google Chrome의 콘솔](introduction-to-signalr/_static/image3.png)

콘솔 열기 및 로깅을 사용 하도록 설정 된 전송 SignalR에서 사용 되는지 확인 수 있습니다.

![Internet Explorer WebSocket 전송 보여 주는 콘솔](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a>전송 지정

전송 협상는 시간과 클라이언트/서버는 상당히 리소스. 클라이언트 기능 알고 있는 경우 다음 전송 지정할 수 있습니다 클라이언트 연결을 시작할 때. 다음 코드 조각 클라이언트가 다른 프로토콜을 지원 하지 않은 알려지기 하는 경우에 사용 되는 Ajax 긴 폴링 전송을 사용 하 여 연결을 시작 하는 방법을 보여 줍니다.

`connection.start({ transport: 'longPolling' });`

시도 하도록 클라이언트를 순서 대로 특정 전송 하려는 경우 대체 순서를 지정할 수 있습니다. 다음 코드 조각 중 WebSocket 스레드가 없으면, 긴 폴링를 직접 시작를 보여 줍니다.

`connection.start({ transport: ['webSockets','longPolling'] });`

전송 지정 하기 위한 문자열 상수는 다음과 같이 정의 됩니다.

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a>연결 및 허브

클라이언트와 서버 간의 통신을 위해 두 개의 모델을 포함 하는 SignalR API: 허브 및 영구 연결 합니다.

연결에 대 한 단일-받는 사람, 그룹화 또는 브로드캐스트 메시지 보내기를 간단한 끝점을 나타냅니다. (PersistentConnection 클래스에 의해.NET 코드에 표시 됨) 하는 영구 연결 API 개발자 직접 SignalR을 노출 하는 하위 수준 통신 프로토콜에 대 한 액세스를 사용 합니다. 연결 통신 모델을 사용 하 여 Windows Communication Foundation 같은 연결 기반 Api을 사용한 개발자에 게 익숙한 됩니다.

허브는 기반으로 클라이언트와 서버가 서로에서 메서드를 직접 호출할 수 있도록 연결 API는 더 높은 수준의 파이프라인입니다. 서버에서 로컬 메서드로 쉽게 그 반대의으로 메서드를 호출 하는 클라이언트 수, 매직 하 여 마치 컴퓨터 경계 간 디스패치 SignalR에서 처리 합니다. 허브 통신 모델을 사용 하 여.NET Remoting와 같은 Api 원격 호출을 사용한 개발자에 게 익숙한 됩니다. 또한 허브를 사용 하 여 모델 바인딩을 사용 하도록 설정 하는 메서드에 강력한 형식의 매개 변수를 전달할 수 있습니다.

### <a name="architecture-diagram"></a>아키텍처 다이어그램

다음 다이어그램은 전송에 사용 되는 기본 기술, 허브 및 영구 연결 사이의 관계를 보여 줍니다.

![Api, 전송 및 클라이언트를 보여 주는 SignalR 아키텍처 다이어그램](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a>허브의 작동 방식

클라이언트에서 메서드를 호출 하는 서버 쪽 코드, 이름 및 메서드를 호출할 수의 매개 변수를 포함 하는 활성 전송에서 패킷을 전송 됩니다 (개체 메서드 매개 변수로 보내면 serialize 된 JSON을 사용 하 여). 클라이언트에는 다음 클라이언트 측 코드에 정의 된 메서드를 메서드 이름과 일치 합니다. 일치 하는 클라이언트 메서드는 deserialize 된 매개 변수 데이터를 사용 하 여 실행 됩니다.

와 같은 도구를 사용 하 여 메서드 호출을 모니터링할 수 있습니다 [Fiddler 합니다.](http://fiddler2.com/) 다음 이미지에서는 Fiddler의 로그 창에서 웹 브라우저 클라이언트에는 SignalR 서버에서 전송 하는 메서드 호출을 보여 줍니다. 허브 호출에서 전송 되는 메서드 호출 `MoveShapeHub`, 호출 되는 메서드가 호출 되 고 `updateShape`합니다.

![SignalR 트래픽 보여 주는 Fiddler 로그의 보기](introduction-to-signalr/_static/image6.png)

이 예에서는 허브 이름으로 식별 됩니다는 `H` 매개 변수; 메서드 이름으로 식별 되는 `M` 매개 변수를 메서드에 전송 중인 데이터와 식별 되는 `A` 매개 변수입니다. 이 메시지를 발생 시킨 응용 프로그램을 만듭니다는 [고주파 실시간](tutorial-high-frequency-realtime-with-signalr.md) 자습서입니다.

### <a name="choosing-a-communication-model"></a>통신 모델 선택

대부분의 응용 프로그램 허브 API를 사용 해야 합니다. 다음과 같은 경우에는 연결 API는 사용할 수 있습니다.

- 지정 보낸 실제 메시지 해야의 형식입니다.
- 원격 호출 모델 보다는 메시징 및 디스패치 모델을 사용 하려면 개발자가 선호 합니다.
- SignalR을 사용 하는 메시징 모델을 사용 하는 기존 응용 프로그램 이식 되는 합니다.
