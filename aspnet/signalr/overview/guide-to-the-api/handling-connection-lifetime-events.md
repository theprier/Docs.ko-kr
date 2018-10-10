---
uid: signalr/overview/guide-to-the-api/handling-connection-lifetime-events
title: 이해 및 SignalR의 연결 수명 이벤트 처리 | Microsoft Docs
author: pfletcher
description: 이 문서에서는 Hubs API에서 노출 하는 이벤트를 사용 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 06/10/2014
ms.assetid: 03960de2-8d95-4444-9169-4426dcc64913
msc.legacyurl: /signalr/overview/guide-to-the-api/handling-connection-lifetime-events
msc.type: authoredcontent
ms.openlocfilehash: 1783a3ab292a5460d5cc1b7ad78073071d65d379
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "48911958"
---
<a name="understanding-and-handling-connection-lifetime-events-in-signalr"></a>이해 및 SignalR의 연결 수명 이벤트를 처리 합니다.
====================
하 여 [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)

> 이 문서는 SignalR 연결, 다시 연결 및 연결 끊기 이벤트를 처리할 수 있는 및 구성할 수 있는 시간 제한 및 keepalive 설정의 개요를 제공 합니다.
>
> 이 문서에서는 SignalR 및 연결 수명 이벤트에 대 한 지식이 이미 가정 합니다. SignalR 소개를 참조 하세요 [SignalR 소개](../getting-started/introduction-to-signalr.md)합니다. 연결 수명 이벤트의 목록에 대 한 다음 리소스를 참조 합니다.
>
> - [허브 클래스에서 연결 수명 이벤트를 처리 하는 방법](hubs-api-guide-server.md#connectionlifetime)
> - [JavaScript 클라이언트에서 연결 수명 이벤트를 처리 하는 방법](hubs-api-guide-javascript-client.md#connectionlifetime)
> - [.NET 클라이언트에서 연결 수명 이벤트를 처리 하는 방법](hubs-api-guide-net-client.md#connectionlifetime)
>
> ## <a name="software-versions-used-in-this-topic"></a>이 항목에서 사용 하는 소프트웨어 버전
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR 버전 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>이 항목의 이전 버전
>
> 이전 버전의 SignalR에 대 한 정보를 참조 하세요 [SignalR 이전 버전](../older-versions/index.md)합니다.
>
> ## <a name="questions-and-comments"></a>질문이 나 의견이 있으면
>
> 이 자습서를 연결 하는 방법 및 새로운 개선할 수 있습니다 페이지의 맨 아래에 의견에서에 의견을 남겨 주세요. 에 자습서로 직접 관련 되지 않은 질문이 있을 경우 게시할 수 하는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.


## <a name="overview"></a>개요

이 자료에는 다음과 같은 섹션이 포함되어 있습니다.

- [연결 수명 용어 및 시나리오](#terminology)

    - [SignalR 연결과 전송 연결을 실제 연결](#signalrvstransport)
    - [전송 연결 끊기를 기반으로 시나리오](#transportdisconnect)
    - [클라이언트 연결 끊기 시나리오](#clientdisconnect)
    - [서버 연결 끊김 시나리오](#serverdisconnect)
- [시간 제한 및 keepalive 설정](#timeoutkeepalive)

    - [ConnectionTimeout](#connectiontimeout)
    - [DisconnectTimeout](#disconnecttimeout)
    - [KeepAlive](#keepalive)
    - [제한 시간 및 keepalive 설정을 변경 하는 방법](#changetimeout)
- [연결 끊김에 대 한 사용자에 게 하는 방법](#notifydisconnect)
- [지속적으로 다시 연결 하는 방법](#continuousreconnect)
- [서버 코드에서 클라이언트를 분리 하는 방법](#disconnectclientfromserver)
- [연결 끊김 이유를 검색합니다.](#detectingreasonfordisconnection)

.NET 4.5 버전의 API는 API 참조 항목에 대 한 링크. .NET 4를 사용 하는 경우 참조 [항목에서는 API의.NET 4 버전](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)합니다.

<a id="terminology"></a>

## <a name="connection-lifetime-terminology-and-scenarios"></a>연결 수명 용어 및 시나리오

합니다 `OnReconnected` SignalR 허브에 이벤트 처리기 바로 뒤에 실행할 수 있습니다 `OnConnected` 하지만 하지 후 `OnDisconnected` 지정된 된 클라이언트에 대 한 합니다. 연결 끊김 없이 다시 연결을 할 수 있습니다 이유가 SignalR에서 사용 되는 단어 "연결" 하는 여러 가지가 있습니다.

<a id="signalrvstransport"></a>

### <a name="signalr-connections-transport-connections-and-physical-connections"></a>SignalR 연결과 전송 연결을 실제 연결

이 문서를 구분할 *SignalR 연결*, *연결 전송*, 및 *물리적 연결*:

- **SignalR 연결** 클라이언트와 서버 URL, SignalR API에 의해 유지 관리 하 고 고유 ID로 식별 연결 간의 논리적 관계를 가리킵니다. 이 관계에 대 한 데이터는 SignalR에서 유지 관리 하 고 전송 연결을 설정 하는 데 사용 됩니다. 클라이언트가 호출할 때 관계 끝 및 SignalR 데이터의 삭제를 `Stop` 메서드 또는 시간 제한에 도달 하면 SignalR 손실된 전송 연결을 다시 설정 하려고 하는 동안.
- **연결 전송** 클라이언트 및 네 개의 전송 Api 중 하나에 의해 유지 관리 서버 간의 논리적 관계를 가리킵니다: Websocket을 서버에서 전송 하는 이벤트를 영구적으로 프레임 또는 장기 폴링. SignalR 전송 API를 사용 하 여 전송 연결을 만들려고 하 고 전송 API 전송 연결을 만들려면 실제 네트워크 연결의 존재 여부에 따라 달라 집니다. 전송 연결 SignalR 종료 때나 전송 API 물리적 연결이 끊어진 지 감지할 때 종료 됩니다.
- **실제 연결** 가리킵니다 와이어, 실제 네트워크 링크-신호는 무선 라우터, 등-클라이언트 컴퓨터와 서버 컴퓨터 간의 통신을 원활 하 합니다. 실제 연결 전송 연결을 설정 하기 위해 있어야 하 고 SignalR 연결을 만드는 데는 전송 연결을 설정 해야 합니다. 그러나 실제 연결을 중단 하지 항상 즉시 전송 연결 또는 종료 SignalR 연결에이 항목의 뒷부분에 설명 하겠지만 합니다.

다음 다이어그램에서 SignalR 연결은 Hubs API 계층과 PersistentConnection API SignalR 표현, 전송 연결으로 전송 계층을 나타내고 실제 연결 서버 사이의 선으로 표시 됩니다. 및 클라이언트입니다.

![SignalR 아키텍처 다이어그램](handling-connection-lifetime-events/_static/image1.png)

호출 하는 경우는 `Start` SignalR 클라이언트에서 메서드를 서버에 실제 연결을 만드는 데 필요한 모든 정보를 사용 하 여 SignalR 클라이언트 코드를 제공 됩니다. SignalR 클라이언트 코드는 HTTP 요청을 확인 하 고 네 가지 전송 방법 중 하나를 사용 하는 실제 연결을 설정 하려면이 정보를 사용 합니다. 전송 연결에 실패 하면 서버가 실패 하는 경우, SignalR 연결 하지 사라집니다 즉시 때문에 여전히 동일한 SignalR URL에 새 전송 연결을 자동으로 다시 설정 하는 데 필요한 정보입니다. 이 시나리오에서는 사용자 응용 프로그램의 개입 없이 관련 된 및 새 전송 연결을 설정 하는 SignalR 클라이언트 코드, 경우에 시작 되는 않는 새 SignalR 연결 합니다. SignalR 연결의 연속성 사실을 반영 됩니다 하는 호출 하는 경우 생성 된 연결 ID를 `Start` 메서드를 변경 하지 않습니다.

`OnReconnected` 허브에 이벤트 처리기는 전송 연결 손실 된 후 자동으로 다시 설정 된 경우를 실행 합니다. `OnDisconnected` 이벤트 처리기가 SignalR 연결의 끝에 실행 합니다. 다음 방법 중 하나로 SignalR 연결을 종료할 수 있습니다.

- 클라이언트에서 호출 하는 경우는 `Stop` 메서드 중지 메시지는 서버에 전송 되 고 클라이언트와 서버 모두 SignalR 연결을 즉시 종료 합니다.
- 클라이언트와 서버 간의 연결이 끊어지면, 클라이언트는 다시 연결을 시도 후 다시 연결 하려면 클라이언트 서버 대기 합니다. 다시 연결 하려는 시도가 성공 하지 않으며 연결 끊기 시간 제한 기간이, 하는 경우 클라이언트와 서버는 SignalR 연결을 끊어야 합니다. 클라이언트에 다시 연결 시도 중지 하 고 표현 SignalR 연결의 서버를 삭제 합니다.
- 클라이언트를 호출 하지 않고 실행을 중지 하는 경우는 `Stop` 메서드를 다시 연결 하려면 클라이언트에 대 한 대기 서버 연결 끊기 시간 제한 기간 후 SignalR 연결을 종료 합니다.
- 경우 실행 서버 중지 클라이언트 하려고 다시 연결 (다시 전송 연결)을 만들려면 다음 연결 끊기 시간 제한 기간 후 SignalR 연결을 종료 합니다.

연결 문제가 없는지 시간과 사용자 응용 프로그램 호출 하 여 SignalR 연결 종료를 `Stop` 메서드, SignalR 연결 및 전송 연결에서 시작 및 종료 시간에 대 한 합니다. 다음 섹션에서는 다른 시나리오를 자세히 설명합니다.

<a id="transportdisconnect"></a>

### <a name="transport-disconnection-scenarios"></a>전송 연결 끊기를 기반으로 시나리오

실제 연결 속도가 느려질 수 있습니다 하거나 연결이 중단 있을 수 있습니다. 작업이 중단 되는 길이 같은 요인에 따라 전송 연결을 삭제할 수 있습니다. SignalR 다시 전송 연결을 설정 하려고 시도 합니다. 전송 연결 API 중단을 감지 하 고 전송 연결을 삭제 하는 경우에 따라 및 SignalR을 발견 즉시 연결이 손실 합니다. 다른 시나리오에서는 전송 연결 API 아니고 SignalR 바로 인식 연결 손실 되었습니다. SignalR 클라이언트 긴 폴링을 제외한 모든 전송에 대 한 호출 함수를 사용 *keepalive* 전송 API를 검색할 수 없는 경우 연결이 손실 되지 않도록 확인 합니다. 장기 폴링 연결에 대 한 정보를 참조 하세요 [제한 시간 및 keepalive 설정을](#timeoutkeepalive) 이 항목의에서 뒷부분에 있습니다.

연결을 활성 상태인 경우 주기적으로 서버 keepalive 패킷을 클라이언트로 보냅니다. 이 문서를 작성 하는 날짜를 기준으로 기본 빈도 10 초 마다는 합니다. 이러한 패킷을 수신 대기, 클라이언트 연결에 문제가 있는지 알 수 있습니다. 예상 하는 경우에 keepalive 패킷이 수신 되지 않으면, 짧은 시간 후 클라이언트는 있다고 가정 속도 저하 또는 중단 같은 연결 문제입니다. Keepalive는 여전히 수신 되지 않으면 더 긴 시간 후에 삭제 됨에 연결 하 고 다시 연결 시도 시작 하기 클라이언트 가정 합니다.

다음 다이어그램에서는 실제 연결을 사용 하 여 전송 API에 의해 즉시 인식 되지 않는 문제가 있는 경우 일반적인 시나리오에서 발생 하는 클라이언트 및 서버 이벤트를 보여 줍니다. 다이어그램은 다음과 같은 경우에 적용 됩니다.

- 전송은은 Websocket, 영원히 프레임 또는 서버에서 전송 하는 이벤트입니다.
- 다양 한 실제 네트워크 연결에서 중단 기간이 있습니다.
- SignalR 하 여 검색 keepalive 기능에 의존 하므로 전송 API를 중단 인식 되지 않습니다.

![전송 연결 끊기](handling-connection-lifetime-events/_static/image2.png)

클라이언트 모드를 다시 연결 되는 전송 연결 끊기 시간 제한 내에서 설정할 수 없습니다 하지만 서버 SignalR 연결을 종료 합니다. 허브의 서버에 실행 하는 경우 `OnDisconnected` 메서드 및 나중에 연결할 클라이언트를 관리 하는 경우 클라이언트에 보낼 연결 끊기 메시지 큐입니다. 연결 끊기 명령 및 호출을 받는 클라이언트에 다시, 하는 경우는 `Stop` 메서드. 이 시나리오에서는 `OnReconnected` 클라이언트에 다시 연결 될 때 실행 되지 않습니다 하 고 `OnDisconnected` 클라이언트가 호출할 때 실행 되지 않습니다 `Stop`합니다. 다음 다이어그램에서는이 시나리오를 보여 줍니다.

![전송 중단-서버 시간 제한](handling-connection-lifetime-events/_static/image3.png)

클라이언트에서 발생할 수 있는 SignalR 연결 수명 이벤트는 다음과 같습니다.

- `ConnectionSlow` 클라이언트는 이벤트입니다.

    Keepalive 시간 제한 기간에 비례하여 미리 설정 된 마지막 메시지 경과한 keepalive ping를 받을 때 발생 합니다. 기본 keepalive 경고 시간 2/3 keepalive 시간 제한의 경우 Keepalive 시간 제한이 20 초 이므로 약 13 초에 경고가 발생 합니다.

    기본적으로 서버 keepalive ping 10 초 마다 보내고 클라이언트 마다 2 초 (1/3 keepalive 시간 제한 값과 keepalive 시간 제한 경고 값 간의 차이)에 대 한 ping keepalive 확인 합니다.

    전송 API를 연결 끊기를 기반으로 인식 되 면 SignalR 수에 대해 숙지 연결을 끊는 데 keepalive 시간 경고 전달 되기 전에 합니다. 이런 경우는 `ConnectionSlow` 이벤트가 발생 하지는, 및 SignalR로 직접 이동 됩니다는 `Reconnecting` 이벤트입니다.
- `Reconnecting` 클라이언트는 이벤트입니다.

    (A) 전송이 API는 연결이 손실 또는 (b) keepalive 시간 이후 마지막 메시지 경과한 또는 keepalive ping 받은 검색할 때 발생 합니다. SignalR 클라이언트 코드를 다시 연결 시도 시작 합니다. 전송 연결이 손실 된 경우 일부 작업을 수행 하도록 응용 프로그램을 원하는 경우이 이벤트를 처리할 수 있습니다. 기본 keepalive 시간 제한 기간은 현재 20 초입니다.

    클라이언트 코드에 SignalR 모드를 다시 연결 되는 동안 허브 메서드를 호출 하려고 SignalR 명령을 보낼 하려고 합니다. 대부분의 경우 이러한 시도 실패 하지만 일부 상황에서 성공할 수 있습니다. 서버에서 전송 하는 이벤트, 영원히 프레임 및 긴 폴링 전송, SignalR 여러 개 있는 메시지를 보내는 클라이언트가 사용 하는 한 메시지를 수신 하는 데 사용 하는 두 개의 통신 채널을 사용 합니다. 수신에 사용 되는 채널 영구적으로 열린 것 이며 실제 연결 중단 된 경우 닫혀 있는 것입니다. 대 한 물리적 연결이 복원 되 면 서버에 클라이언트에서 메서드 호출 될 수 성공적으로 수신 채널 다시 설정 되기 전에 사용 가능한 유지를 보내는 데 사용할 채널입니다. SignalR 수신에 사용 되는 채널을 다시 엽니다 될 때까지 반환 값을 받을 수는 있습니다.
- `Reconnected` 클라이언트는 이벤트입니다.

    전송 연결을 다시 설정할 때 발생 합니다. `OnReconnected` 허브에서 이벤트 처리기를 실행 합니다.
- `Closed` 클라이언트 이벤트 (`disconnected` javascript에서 이벤트).

    SignalR 클라이언트 코드는 전송 연결 손실 된 후 다시 연결 하려고 하는 동안 연결 끊기 시간 제한 기간이 만료 되 면 발생 합니다. 기본 연결 끊기 시간 제한은 30 초입니다. (연결 때문에 종료 될 때에이 이벤트 발생을 `Stop` 메서드가 호출 됩니다.)

전송 API에 의해 검색 되지 않는 keepalive 시간 제한 경고 기간 보다 오랫동안 서버에서 ping keepalive 수신을 지체 하지 하는 전송 연결 중단 모든 연결 수명 이벤트가 발생 하지 않을 수 있습니다.

의도적으로 일부 네트워크 환경 유휴 연결을 닫고 keepalive 패킷의 다른 기능은 이러한 네트워크 알리는 SignalR 연결을 사용 하 여이 방지 하는 것입니다. 극단적인 경우 keepalive ping 기본 빈도 충분 하지 않이 닫힌된에 연결할 수 없게 합니다. 이 경우 더 자주 전송할 keepalive ping을 구성할 수 있습니다. 자세한 내용은 [제한 시간 및 keepalive 설정을](#timeoutkeepalive) 이 항목의에서 뒷부분에 있습니다.

> [!NOTE]
>
> **중요 한**: 여기에 설명 된 이벤트의 순서는 보장 되지 않습니다. SignalR에서는이 스키마에 따라 예측 가능한 방식으로 연결 수명 이벤트를 발생 시키는 모든 있지만 가지 다양 한 네트워크 이벤트 및 전송 Api와 같은 기본 통신 프레임 워크 처리 하는 다양 합니다. 예를 들어를 `Reconnected` 클라이언트는 다음 작업을 다시 연결 되 면 이벤트가 발생할 수 있습니다 또는 `OnConnected` 서버에서 처리기는 연결을 설정 하려는 시도가 성공적으로 수행 되지 경우에 실행할 수 있습니다. 이 항목에서는 일반적인 상황에서 정상적으로 생성 되는 영향만 설명 합니다.


<a id="clientdisconnect"></a>

### <a name="client-disconnection-scenarios"></a>클라이언트 연결 끊기 시나리오

브라우저 클라이언트에서 SignalR 연결을 관리 하는 SignalR 클라이언트 코드는 웹 페이지의 JavaScript 컨텍스트에서 실행 됩니다. 에 SignalR 연결 간에 이동 하면 종료 해야 하는 이유 페이지 간에 해당의 이유는 여러 연결이 있는 여러 연결 Id 사용 하 여 여러 브라우저 창이 나 탭에서 연결 하는 경우. 사용자는 브라우저 창이 나 탭을 닫습니다 또는 새 페이지로 이동 하거나 페이지를 새로 고칩니다, SignalR 연결 SignalR 클라이언트 코드 및 호출에 대 한 브라우저 이벤트를 처리 하기 때문에 즉시 종료 합니다 `Stop` 메서드. 이러한 시나리오에서 또는 응용 프로그램에서 호출 하는 경우 모든 클라이언트 플랫폼에는 `Stop` 메서드를를 `OnDisconnected` 서버에서 이벤트 처리기를 즉시 실행 및 클라이언트를 발생 시킵니다 합니다 `Closed` 이벤트 (이벤트의 이름은 `disconnected` 에서 JavaScript)입니다.

클라이언트 응용 프로그램 또는 컴퓨터에서 실행 되는 충돌 또는 (예를 들어,는 사용자가 닫을 때 랩톱)를 절전 모드로 전환 하는 경우 서버는 내용에 대 한 알려지지 않습니다. 서버가 알와 관련해 서 손실 클라이언트의 연결 중단 때문일 수 있습니다 및 클라이언트 다시 연결 하려고 할 수 있습니다. 따라서 서버가 대기 하는 클라이언트에 다시 연결을 제공할 수 있도록 이러한 시나리오에서는 및 `OnDisconnected` 연결 끊기 시간 제한 기간 (기본적으로 약 30 초)을 만료 될 때까지 실행 되지 않습니다. 다음 다이어그램에서는이 시나리오를 보여 줍니다.

![클라이언트 컴퓨터 오류입니다.](handling-connection-lifetime-events/_static/image4.png)

<a id="serverdisconnect"></a>

### <a name="server-disconnection-scenarios"></a>서버 연결 끊김 시나리오

서버를 오프 라인 상태가-다시 부팅, 실패 하면 응용 프로그램 도메인 재활용, 등-결과 연결이 끊기는 유사할 수 있습니다 또는 전송 API 및 SignalR 수 즉시 알 수는 서버는 사라지고 및 SignalR 시작 하지 않고 다시 연결 하려고 합니다. 발생 된 `ConnectionSlow` 이벤트입니다. 클라이언트 모드에서 다시 연결 되 고 서버를 복구 하거나 다시 시작 또는 새 서버를 온라인 연결 끊기 시간 제한 기간이 만료 되기 전에 클라이언트 복원 또는 새 서버에 다시 연결 됩니다. 클라이언트에서 SignalR 연결을 계속 하는 경우 및 `Reconnected` 이벤트가 발생 합니다. 첫 번째 서버의 `OnDisconnected` 실행 되지 않습니다 하 고 새 서버의 `OnReconnected` 있지만 실행 되 `OnConnected` 하기 전에 해당 서버에서 해당 클라이언트에 대 한 실행 되지 않은 합니다. (효과 클라이언트에 다시 연결 동일한 서버를 다시 부팅 하거나 응용 프로그램 도메인 재활용, 후 서버를 다시 시작할 때이 때문에 동일한에 이전 연결 작업의 메모리가 없습니다.) 다음 다이어그램은 즉시 전송 API가 연결 해제를 인식 하는 것으로 가정 하므로 `ConnectionSlow` 이벤트가 발생 하지 않습니다.

![서버 오류 및 다시 연결](handling-connection-lifetime-events/_static/image5.png)

서버를 사용할 수 없으면 연결 끊기 시간 제한 기간 내에 SignalR 연결 종료 됩니다. 이 시나리오에서는 합니다 `Closed` 이벤트 (`disconnected` JavaScript 클라이언트에서) 클라이언트에서 발생 하지만 `OnDisconnected` 서버에서 호출 되지 않습니다. 다음 다이어그램은 가정 SignalR keepalive 기능 감지 하므로 API 전송 연결 손실된의 인식 되지 않습니다 및 `ConnectionSlow` 이벤트가 발생 합니다.

![서버 오류 및 시간 제한](handling-connection-lifetime-events/_static/image6.png)

<a id="timeoutkeepalive"></a>

## <a name="timeout-and-keepalive-settings"></a>시간 제한 및 keepalive 설정

기본값 `ConnectionTimeout`, `DisconnectTimeout`, 및 `KeepAlive` 값 대부분의 시나리오에 적합 하지만 환경에 특별 한 요구 하는 경우에 변경할 수 있습니다. 예를 들어 네트워크 환경 닫히면 5 초 동안 유휴 상태인 연결 해야 keepalive 값을 줄입니다.

<a id="connectiontimeout"></a>

### <a name="connectiontimeout"></a>ConnectionTimeout

이 설정을 열고 닫고 새 연결을 열기 전에 응답을 기다리고는 전송 연결을 해제 하는 시간을 나타냅니다. 기본값은 110 초입니다.

이 설정은 적용만 경우 keepalive 기능이 해제 된 일반적으로 긴에만 적용 됩니다 폴링 전송 합니다. 다음 다이어그램은 long으로이 설정의 효과 보여 줍니다. 폴링 전송 연결입니다.

![긴 폴링 전송 연결입니다.](handling-connection-lifetime-events/_static/image7.png)

<a id="disconnecttimeout"></a>

### <a name="disconnecttimeout"></a>DisconnectTimeout

이 설정은 발생 하기 전에 전송 연결이 끊긴 후 대기할 시간을 나타냅니다는 `Disconnected` 이벤트입니다. 기본값은 30초입니다. 설정한 경우 `DisconnectTimeout`, `KeepAlive` 1/3로 자동 설정 됩니다는 `DisconnectTimeout` 값입니다.

<a id="keepalive"></a>

### <a name="keepalive"></a>KeepAlive

이 설정은 유휴 연결을 통해 keepalive 패킷 보내기 전에 대기할 시간을 나타냅니다. 기본값은 10 초입니다. 이 값에는의 1/3 개를 사용 해야 합니다.는 `DisconnectTimeout` 값입니다.

모두 설정 하려는 경우 `DisconnectTimeout` 하 고 `KeepAlive`설정 `KeepAlive` 후 `DisconnectTimeout`합니다. 그렇지 않은 경우에 `KeepAlive` 때 설정을 덮어쓰게 됩니다 `DisconnectTimeout` 자동으로 설정 `KeepAlive` 제한 시간 값의 1/3입니다.

Keepalive 기능을 사용 하지 않도록 설정 하려는 경우 설정 `KeepAlive` null로 합니다. Keepalive 기능이 자동으로 사용할 수 없게 됩니다 긴 폴링 전송 합니다.

<a id="changetimeout"></a>

### <a name="how-to-change-timeout-and-keepalive-settings"></a>제한 시간 및 keepalive 설정을 변경 하는 방법

설정 이러한 설정에 대 한 기본 값을 변경 하려면 `Application_Start` 에 사용자 *Global.asax* 파일을 다음 예와에서 같이 합니다. 샘플 코드에 표시 된 값의 기본 값과 동일 합니다.

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample1.cs)]

<a id="notifydisconnect"></a>

## <a name="how-to-notify-the-user-about-disconnections"></a>연결 끊김에 대 한 사용자에 게 하는 방법

일부 응용 프로그램에서 연결 문제가 있는 경우 사용자에 게 메시지를 표시 하는 것이 좋습니다. 방법에 대 한 몇 가지 옵션 및이 작업을 수행 하는 경우가 있습니다. 다음 코드 예제는 생성 된 프록시를 사용 하 여 JavaScript 클라이언트에 대 한 합니다.

- 처리는 `connectionSlow` 모드를 다시 연결로 이동 하기 전에 SignalR은 연결 문제를 인식 하는 즉시 메시지를 표시 하는 이벤트입니다.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample2.js)]
- 처리는 `reconnecting` SignalR 연결 끊김을 인식 및 모드를 다시 연결로 이동 하는 경우 메시지를 표시 하는 이벤트입니다.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample3.js)]
- 처리는 `disconnected` 다시 연결 하려고 할 때 메시지를 표시 하는 이벤트 시간이 초과 되었습니다. 이 시나리오에서는 서버를 사용 하 여 연결을 다시 다시 설정 하는 유일한 방법은를 호출 하 여 SignalR 연결을 다시 시작 되는 `Start` 새 연결 ID를 만드는 메서드 다음 코드 예제는 플래그를 사용 하 여 호출 하 여 SignalR 연결에 일반적인 최종 이후가 아님, 다시 연결 시간 초과 후에 알림을 발급 하는 되도록는 `Stop` 메서드.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample4.js)]

<a id="continuousreconnect"></a>

## <a name="how-to-continuously-reconnect"></a>지속적으로 다시 연결 하는 방법

일부 응용 프로그램에서 손실 된 후 다시 연결 시도 시간이 초과 되었습니다 자동으로 연결을 다시 설정 하는 것이 좋습니다. 이 위해 호출할 수 있습니다 합니다 `Start` 메서드에서 하 `Closed` 이벤트 처리기 (`disconnected` JavaScript 클라이언트에서 이벤트 처리기). 기간 호출 하기 전에 대기 하는 것이 좋습니다 `Start` 너무 이렇게 방지 하기 위해 자주 서버 또는 물리적으로 연결 되지 않는 경우 사용할 수 있습니다. 다음 코드 예제는 생성 된 프록시를 사용 하 여 JavaScript 클라이언트입니다.

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample5.js)]

모바일 클라이언트에서 알아야 할 잠재적 문제는 연속 재연결 시도 서버 또는 물리적 연결을 사용할 수 없는 경우 불필요 한 배터리가 발생할 수 있습니다.

<a id="disconnectclientfromserver"></a>

## <a name="how-to-disconnect-a-client-in-server-code"></a>서버 코드에서 클라이언트를 분리 하는 방법

SignalR 2 버전에 클라이언트 연결 끊기에 대 한 기본 제공 서버 API가 없습니다. 가지 [나중에이 기능을 추가 하는 것에 대 한 계획](https://github.com/SignalR/SignalR/issues/2101)합니다. 현재 SignalR 릴리스의 서버에서 클라이언트를 분리 하는 가장 간단한 방법은 클라이언트에서 연결 끊기 메서드를 구현 하는 서버에서 해당 메서드를 호출 합니다. 다음 코드 예제는 생성 된 프록시를 사용 하 여 JavaScript 클라이언트에 대 한 연결 끊기 메서드를 보여 줍니다.

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample6.js)]

> [!WARNING]
> 보안-클라이언트 연결 끊기에 대 한이 메서드가 아니고 제안 된 기본 제공 API를 처리할 클라이언트에 다시 연결할 수 없습니다 해킹된 코드를 제거할 수 있으므로 악성 코드를 실행 하는 클라이언트를 해킹된 하는 시나리오는 `stopClient` 메서드 또는 변경 수행 합니다. 상태 저장 서비스 거부 (DOS) 보호를 구현 하는 데 적합 한 곳 프런트 엔드 인프라 하지만 대신 프레임 워크 또는 서버 계층에 없는 경우


<a id="detectingreasonfordisconnection"></a>
## <a name="detecting-the-reason-for-a-disconnection"></a>연결 끊김 이유를 검색합니다.

서버에 오버 로드를 추가 하는 SignalR 2.1 `OnDisconnect` 시간 초과 보다는 의도적으로 연결이 나타내는 이벤트입니다. `StopCalled` 매개 변수는 클라이언트 연결을 명시적으로 닫힌 경우 true입니다. JavaScript에서 서버 오류를 초래한 클라이언트 연결을 끊을 경우 오류 정보를 전달할으로 클라이언트에 게 `$.connection.hub.lastError`합니다.

**C# 서버 코드: `stopCalled` 매개 변수**

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample7.cs?highlight=1,3)]

**JavaScript 클라이언트 코드가: 액세스 `lastError` 에 `disconnect` 이벤트입니다.**

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample8.js?highlight=2-3)]
