---
uid: signalr/overview/older-versions/handling-connection-lifetime-events
title: "SignalR에서 연결 수명 이벤트를 처리 하 고 이해 1.x | Microsoft Docs"
author: pfletcher
description: "이 문서에서는 허브 API에서 노출 하는 이벤트를 사용 하는 방법을 설명 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/05/2013
ms.topic: article
ms.assetid: e608e263-264d-448b-b0eb-6eeb77713b22
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/older-versions/handling-connection-lifetime-events
msc.type: authoredcontent
ms.openlocfilehash: db29c3382895ef4d7efc3a686fa558189c8788de
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="understanding-and-handling-connection-lifetime-events-in-signalr-1x"></a>SignalR에서 연결 수명 이벤트를 처리 하 고 이해 1.x
====================
여 [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)

> 이 문서는 SignalR 연결, 다시 연결 및 연결 끊기 이벤트를 처리할 수 있습니다 및 구성할 수 있는 제한 시간 및 keepalive 설정을 대 한 개요를 제공 합니다.
> 
> SignalR 연결과 수명 이벤트에 대 한 지식을 이미 있다고 가정 하는 문서입니다. SignalR에 대 한 소개를 참조 하십시오. [SignalR-개요-시작](index.md)합니다. 연결 수명 이벤트의 목록에 대 한 다음 리소스를 참조 합니다.
> 
> - [허브 클래스에서 연결 수명 이벤트를 처리 하는 방법](index.md)
> - [JavaScript 클라이언트에서 연결 수명 이벤트를 처리 하는 방법](index.md)
> - [.NET 클라이언트에서 연결 수명 이벤트를 처리 하는 방법](index.md)


## <a name="overview"></a>개요

이 자료에는 다음과 같은 섹션이 포함되어 있습니다.

- [연결 수명 용어 및 시나리오](#terminology)

    - [SignalR 연결과 전송 연결은 물리적 연결](#signalrvstransport)
    - [전송 연결 끊기 시나리오](#transportdisconnect)
    - [클라이언트의 연결을 끊는 시나리오](#clientdisconnect)
    - [서버 연결을 끊는 시나리오](#serverdisconnect)
- [제한 시간 및 keepalive 설정](#timeoutkeepalive)

    - [ConnectionTimeout](#connectiontimeout)
    - [Disconnecttimeout은](#disconnecttimeout)
    - [KeepAlive](#keepalive)
    - [제한 시간 및 keepalive 설정을 변경 하는 방법](#changetimeout)
- [연결 끊김에 대 한 사용자에 게 하는 방법](#notifydisconnect)
- [지속적으로 다시 연결 하는 방법](#continuousreconnect)
- [서버 코드에서 클라이언트 연결을 끊을 하는 방법](#disconnectclientfromserver)

API 참조 항목의 링크를.NET 4.5 버전의 API 되도록합니다. .NET 4를 사용 하 여 참조 [.NET 4 버전의 API 항목](https://msdn.microsoft.com/en-us/library/jj891075(v=vs.100).aspx)합니다.

<a id="terminology"></a>

## <a name="connection-lifetime-terminology-and-scenarios"></a>연결 수명 용어 및 시나리오

`OnReconnected` SignalR 허브의 이벤트 처리기 직후에 실행할 수 있습니다 `OnConnected` 후 하지 않지만 `OnDisconnected` 지정된 된 클라이언트에 대 한 합니다. 연결 해제 하지 않고 다시 연결이 있을 수 있습니다 원인은 SignalR에서 사용 되는 단어 "연결" 하는 여러 가지가 있습니다.

<a id="signalrvstransport"></a>

### <a name="signalr-connections-transport-connections-and-physical-connections"></a>SignalR 연결과 전송 연결은 물리적 연결

이 문서를 구분 합니다 *SignalR 연결*, *연결 전송*, 및 *실제 연결*:

- **SignalR 연결** 참조 하는 클라이언트와 서버 URL, SignalR API에 의해 유지 관리 하 고 고유 하 게 ID로 식별 연결 간의 논리적 관계 이 관계에 대 한 데이터 SignalR가 유지 관리 하 고 전송 연결을 설정 하는 데 사용 됩니다. 클라이언트가 호출할 때 관계 end와 SignalR 데이터의 삭제는 `Stop` 메서드 또는 시간 제한에 도달 하면 동안 SignalR 손실된 전송 연결을 다시 설정 하려고 합니다.
- **연결 전송** 참조 하는 클라이언트와 4 개의 전송 Api 중 하나에 의해 유지 관리 되는 서버 간의 논리적 관계를: Websocket, 서버에서 전송 이벤트 영원히 프레임에서 또는 긴 폴링 합니다. SignalR 전송 API를 사용 하 여 전송 연결을 만들려고 하 고 전송 API 전송 연결을 만들려면 실제 네트워크 연결이 있는지 여부에 따라 달라 집니다. 전송 연결이 종료 되 고 SignalR 종료 또는 전송 API에서 물리적 연결이 끊어진 임을 감지한 경우.
- **실제 연결** 가리킵니다 와이어, 실제 네트워크 링크-무선 신호를 라우터 등-는 클라이언트 컴퓨터와 서버 컴퓨터 간의 통신을 용이 하 게 합니다. 실제 연결 전송 연결을 설정 하기 위해 있어야 하 고 SignalR 연결을 설정 하기 위해 전송 연결을 설정 해야 합니다. 그러나 실제 연결을 중단 하지 않습니다 항상 즉시 종료는 전송 연결 또는 SignalR 연결이이 항목의 뒷부분에서 설명 하겠지만 합니다.

다음 다이어그램에 SignalR 연결 표시 되는 허브 API 및 API SignalR PersistentConnection 계층, 전송 연결에서 전송 계층을 나타내는 고 물리적으로 연결 하는 서버 간의 선으로 표시 됩니다. 및 클라이언트에서.

![SignalR 아키텍처 다이어그램](handling-connection-lifetime-events/_static/image1.png)

호출 하는 경우는 `Start` SignalR 클라이언트에서 메서드를 제공 하는 SignalR 클라이언트 코드는 서버에 물리적 연결을 설정 하는 데 필요한 모든 정보로 합니다. SignalR 클라이언트 코드가이 정보를 사용 하 여 HTTP 요청을 확인 하 고 네 가지 전송 방법 중 하나를 사용 하는 물리적 연결을 설정 합니다. 전송 연결에 실패 하면 서버가 실패 하는 경우 SignalR 연결 하지 않는 나타나지 즉시 때문에 여전히 동일한 SignalR URL에는 새 전송 연결을 자동으로 다시 설정 하는 데 필요한 정보입니다. 이 시나리오에서는 사용자 응용 프로그램의 개입 없이 포함 된 하 고 새 SignalR 연결 시작 되지 않으면 새 전송 연결을 설정 하는 SignalR 클라이언트 코드를 하는 경우. SignalR 연결 하는 팩트에 반영 됩니다 하는 호출 될 때 만들어지는 연결 ID는 `Start` 메서드를 변경 하지 않습니다.

`OnReconnected` 전송 연결이 손실 된 후 자동으로 다시 설정할 때 허브에 이벤트 처리기를 실행 합니다. `OnDisconnected` SignalR 연결의 끝에 이벤트 처리기를 실행 합니다. SignalR 연결에 다음과 같은 방법으로 종료할 수 있습니다.

- 클라이언트에서 호출 하는 경우는 `Stop` 메서드를 한 중지 메시지는 서버에 전송 되 고 클라이언트와 서버 모두 SignalR 연결 즉시 종료 합니다.
- 클라이언트와 서버 사이의 연결 손실 되 면 클라이언트에서 다시 연결 하려고 하 고 서버 다시 연결 하려면 클라이언트에 대 한 대기 합니다. 다시 연결 시도가 연결 끊기 시간 제한 기간이 종료 된 경우 클라이언트와 서버는 SignalR 연결을 끊어야 합니다. 클라이언트에 다시 연결 시도 중지 하 고 표현 SignalR 연결의 서버를 삭제 합니다.
- 클라이언트를 호출 하지 않고도 실행을 중지 한 경우는 `Stop` 메서드를 서버에 다시 연결 클라이언트에 대 한 대기 다음 연결 끊기 시간 제한 기간 후 SignalR 연결을 종료 합니다.
- 경우 실행을 서버 중지 클라이언트 하려고 다시 연결 (다시 작성 전송 연결) 한 다음 연결 끊기 시간 제한 기간 후 SignalR 연결을 종료 합니다.

연결 문제가 없는지를 호출 하 여 SignalR 연결을 종료 하는 사용자 응용 프로그램이 시점과 `Stop` 방법, SignalR 연결 및 전송 연결에서 시작 및 종료 같은 시간에 대 한 합니다. 다음 섹션에서는 다른 시나리오를 보다 자세히 설명 합니다.

<a id="transportdisconnect"></a>

### <a name="transport-disconnection-scenarios"></a>전송 연결 끊기 시나리오

실제 연결 속도가 느려질 수 있습니다 또는 연결에서 중단 있을 수 있습니다. 중단의 길이 같은 요인에 따라 전송 연결을 삭제할 수 있습니다. SignalR 다음 다시 전송 연결을 설정 하려고 합니다. 전송 연결 API 중단을 검색 하 고 전송 연결을 삭제 하는 경우에 따라 찾은 SignalR 즉시 연결이 끊어진입니다. 다른 시나리오에서는 전송 연결 API 아니고 SignalR는 인식 즉시 연결 손실 되었습니다. 긴 폴링을 제외한 모든 전송에 대 한 SignalR 클라이언트 사용 하는 함수 호출 *keepalive* 전송 API를 검색할 수 없는 경우 연결이 손실에 대 한 확인 합니다. 긴 폴링 연결에 대 한 정보를 참조 하십시오. [제한 시간 및 keepalive 설정을](#timeoutkeepalive) 이 항목의 뒷부분에 나오는 합니다.

연결이 활성 때 정기적으로 서버 keepalive 패킷을 클라이언트로 보냅니다. 이 문서 작성 될 날짜를 기준으로 기본 빈도 10 초 마다는 합니다. 이러한 패킷은 대 한 수신 대기 하 여 클라이언트 연결에 문제가 있는지 확인할 수 있습니다. 예상 keepalive 패킷이 수신 되지 않으면, 잠시 후 클라이언트 있는 것으로 가정 속도 저하가 또는 중단 같은 연결 문제가 있습니다. Keepalive는 여전히를 받지 않는 경우 더 긴 시간 이후에 삭제 됨에 연결 하 고 다시 연결을 시도 시작 하기 클라이언트 가정 합니다.

다음 다이어그램에서는 즉시 전송 API에 의해 인식 되지 않는 실제 연결에 문제가 없는 경우 일반적인 시나리오에서 발생 하는 클라이언트와 서버 이벤트를 보여 줍니다. 다음과 같은 경우에는 다이어그램에 적용 됩니다.

- 전송은은 WebSockets, 영원히 프레임 또는 서버에서 전송 하는 이벤트입니다.
- 다양 한 실제 네트워크 연결에서 중단 기간이 있습니다.
- 전송 API SignalR 검색할 keepalive 기능에 의존 하므로 중단, 인식 되지 않습니다.

![전송 연결 끊기](handling-connection-lifetime-events/_static/image2.png)

클라이언트 모드를 다시 연결 되는 전송 연결 끊기 시간 제한 내에서 설정할 수 없습니다 되지만 서버는 SignalR 연결을 종료 합니다. 서버 허브의 실행에 도달 하면 `OnDisconnected` 메서드 및 나중에 연결 하려면 클라이언트를 관리 하는 경우 클라이언트에 보낼 연결 끊기 메시지를 큐. 연결 끊기 명령 및 호출 받을 클라이언트 다음에 다시 연결 하는 경우는 `Stop` 메서드. 이 시나리오에서는 `OnReconnected` 클라이언트가 다시 연결 될 때 실행 되지 않습니다 및 `OnDisconnected` 클라이언트가 호출할 때 실행 되지 않습니다 `Stop`합니다. 다음 다이어그램은이 시나리오를 보여 줍니다.

![전송 작업 중단-서버 제한 시간](handling-connection-lifetime-events/_static/image3.png)

클라이언트에서 발생할 수 있는 SignalR 연결 수명 이벤트는 다음과 같습니다.

- `ConnectionSlow`클라이언트 이벤트입니다.

    마지막 메시지 이후 미리 설정 된 비율로 keepalive 제한 시간 경과 또는 keepalive ping을 받은 경우 발생 합니다. 기본 keepalive 시간 제한 경고 기간은 keepalive 시간 제한의 2/3입니다. Keepalive 시간 초과 20 초 이므로 약 13 초에는 경고가 발생 합니다.

    기본적으로 서버 ping keepalive 10 초 마다 보내고 2 초 간격 (1/keepalive 제한 시간 값과 시간 제한 경고 keepalive 값 간의 차이 3)에 대 한 keepalive ping에 대 한 클라이언트를 확인 합니다.

    API 전송에서 연결 해제를 인식 되 면 keepalive 시간 제한 경고 기간 전달 되기 전에 SignalR 연결 끊기를의 알림을 수 있습니다. 이 경우는 `ConnectionSlow` 이벤트 라우트된, 및 SignalR에 직접 할까요는 `Reconnecting` 이벤트입니다.
- `Reconnecting`클라이언트 이벤트입니다.

    연결이 끊어지면 또는 마지막 메시지 이후 (b) keepalive 제한 시간 경과 또는 않았는지 keepalive ping을 받았습니다 (a) 전송이 API 검색할 때 발생 합니다. SignalR 클라이언트 코드는 다시 연결을 시도 시작 합니다. 전송 연결이 손실 된 경우 일부 작업을 수행 하도록 응용 프로그램을 원하는 경우이 이벤트를 처리할 수 있습니다. 기본 keepalive 제한 시간이 현재 20 초입니다.

    클라이언트 코드에 SignalR 모드를 다시 연결 중인 동안에 허브 메서드를 호출 하려고 SignalR 명령을 보낼 하려고 합니다. 대부분의 경우 이러한 시도 실패 하지만 경우에 따라 성공할 수도 있습니다. 서버에서 전송 이벤트, 영원히 프레임 및 긴 폴링 전송, SignalR은 두 개의 통신 채널이 메시지를 보내는 클라이언트가 사용 하 고 다른 하나는 메시지를 받을 사용 하 여 사용 합니다. 수신에 사용 되는 채널은 영구적으로 열려 하나 있고 물리적 연결이 중단 된 경우 닫힌 것입니다. 물리적으로 연결을 복원 하는 경우 서버에 클라이언트에서 메서드 호출 될 수신 채널은 다시 설정 하기 전에 하므로 계속 사용할 수 있는, 보내는 데 사용 되는 채널입니다. SignalR 수신에 사용 되는 채널을 다시 여 될 때까지 반환 값을 받을 수는 있습니다.
- `Reconnected`클라이언트 이벤트입니다.

    전송 연결을 다시 설정할 때 발생 합니다. `OnReconnected` 허브에 이벤트 처리기를 실행 합니다.
- `Closed`클라이언트 이벤트 (`disconnected` JavaScript의 이벤트).

    SignalR 클라이언트 코드 전송 연결이 끊어진 후 다시 연결 하려고 하는 동안 연결 끊기 시간 제한 기간이 만료 되 면 발생 합니다. 기본 연결 끊기 시간 제한은 30 초입니다. (때문에 연결이 종료 될 때에이 이벤트는 발생 된 `Stop` 메서드를 호출 합니다.)

전송 API에 의해 검색 되지 않는 keepalive ping keepalive 시간 제한 경고 기간 보다 오랫동안 서버에서 수신이 중간 지체 하지 하는 전송 연결 중단 되지 않을 수 있습니다 모든 연결 수명 이벤트를 발생 합니다.

의도적으로 일부 네트워크 환경 유휴 연결을 닫고 keepalive 패킷 다른 기능은 이러한 네트워크 SignalR 연결 사용 중임을 알 수 있도록 함으로써이 방지 하는 것입니다. 극단적인 경우에는 기본 빈도의 keepalive ping 아닐 수 있습니다에 닫힌된 연결을 방지 하기에 충분 한. 이 경우 더 자주 보낼 keepalive ping을 구성할 수 있습니다. 자세한 내용은 참조 [제한 시간 및 keepalive 설정을](#timeoutkeepalive) 이 항목의 뒷부분에 나오는 합니다.

> [!NOTE] 
> 
> [!IMPORTANT]
> 여기에 설명 된 이벤트의 순서는 보장 되지 않습니다. SignalR에서는이 체계에 따라 예측 가능한 방식으로 연결 수명 이벤트를 발생 시키는 모든 하지만 다양 한 네트워크 이벤트 및 전송 Api와 같은 기본 통신 프레임 워크 처리 하는 여러 가지 방법입니다. 예를 들어는 `Reconnected` 클라이언트가 다시 연결 될 때 이벤트가 발생할 수 있습니다 또는 `OnConnected` 서버에서 처리기를 연결 하지 못한 경우 실행 될 수 있습니다. 이 항목에서는 특정 일반적인 상황에서 정상적으로 생성 되는 효과 설명 합니다.


<a id="clientdisconnect"></a>

### <a name="client-disconnection-scenarios"></a>클라이언트의 연결을 끊는 시나리오

브라우저 클라이언트에서 SignalR 연결을 관리 하는 SignalR 클라이언트 코드는 웹 페이지의 JavaScript 컨텍스트에서 실행 됩니다. 하는 SignalR 연결에 하나를 탐색할 때 종료 하는 이유 페이지 다른 디렉터리로 및 해당의 이유가 있는 여러 연결 Id와의 연결이 여러 여러 브라우저 창이 나 탭에서 연결 하는 경우. 사용자를 새 페이지로 이동 하거나 페이지를 새로 고칩니다 브라우저 창이 나 탭을 닫습니다, SignalR 연결 SignalR 클라이언트 코드와 호출을 위한 브라우저에 해당 이벤트를 처리 하기 때문에 즉시 종료는 `Stop` 메서드. 이러한 시나리오에서 또는 응용 프로그램 호출 하면 모든 클라이언트 플랫폼에는 `Stop` 메서드를는 `OnDisconnected` 서버에서 이벤트 처리기를 즉시 실행 하 고 클라이언트 시킵니다는 `Closed` 이벤트 (이벤트의 이름은 `disconnected` 에 JavaScript)입니다.

클라이언트 응용 프로그램 또는 컴퓨터에서 실행 되는 충돌 하거나 (예를 들어 사용자가 닫으면 랩톱) 대기 상태로 전환, 하는 경우 서버는 무슨 상황이 발생 하는 방법에 대 한 알림을 받습니다 되지 않습니다. 서버에서 검색 관련해 서 손실 클라이언트의 연결 중단 때문일 수 있습니다 및 클라이언트가 다시 연결 하려고 할 수 있습니다. 서버가 클라이언트에 다시 연결을 제공할 수 있도록 기다립니다. 이러한 시나리오에서 따라서 및 `OnDisconnected` 연결 끊기 시간 제한 기간 (기본적으로 약 30 초)을 만료 될 때까지 실행 되지 않습니다. 다음 다이어그램은이 시나리오를 보여 줍니다.

![클라이언트 컴퓨터 오류](handling-connection-lifetime-events/_static/image4.png)

<a id="serverdisconnect"></a>

### <a name="server-disconnection-scenarios"></a>서버 연결을 끊는 시나리오

서버가 되는 오프 라인-다시 부팅, 실패 하면 응용 프로그램 도메인 재활용,-등 결과 손실된 연결과 유사한 수 있습니다 또는 전송 API 및 SignalR 수 즉시 알 수는 서버는 사라지고 SignalR 시작 하지 않고 다시 연결 하려고 합니다. 발생 된 `ConnectionSlow` 이벤트입니다. 클라이언트 모드에서 다시 연결 되 고 서버를 복구 하거나 다시 시작 또는 새 서버를 온라인 상태로 만들 연결 끊기 시간 제한 기간이 만료 되기 전에 클라이언트 복원 또는 새 서버에 다시 연결 됩니다. SignalR 연결 클라이언트에서 계속 하는 경우와 `Reconnected` 이벤트가 발생 합니다. 첫 번째 서버에서 `OnDisconnected` 결코 실행 되지 않음을 새 서버 `OnReconnected` 있지만 실행 되 `OnConnected` 하기 전에 해당 서버에서 해당 클라이언트에 대해 실행 되지 않은 합니다. (효과 클라이언트에 다시 연결 동일한 서버를 다시 부팅 또는 응용 프로그램 도메인 재활용 서버 시작 시 때문에 동일한에 이전 연결 작업의 메모리가 없습니다.) 다음 다이어그램은 즉시 전송 API이 연결 해제를 인식 하는 것으로 가정 하므로 `ConnectionSlow` 이벤트가 발생 하지 않습니다.

![서버 오류 및 다시 연결](handling-connection-lifetime-events/_static/image5.png)

연결 끊기 시간 제한 내 서버를 사용할 수 있는 상태가 되지 않는, SignalR 연결 종료 됩니다. 이 시나리오는 `Closed` 이벤트 (`disconnected` JavaScript 클라이언트에서) 클라이언트에서 발생 합니다. 하지만 `OnDisconnected` 는 서버에서 호출 되지 않습니다. 다음 다이어그램은 API 전송 하므로 SignalR keepalive 기능으로 검색 되는 연결 끊김된의 인식 되지 않습니다 가정 및 `ConnectionSlow` 이벤트가 발생 합니다.

![서버 오류 및 시간 초과](handling-connection-lifetime-events/_static/image6.png)

<a id="timeoutkeepalive"></a>

## <a name="timeout-and-keepalive-settings"></a>제한 시간 및 keepalive 설정

기본 `ConnectionTimeout`, `DisconnectTimeout`, 및 `KeepAlive` 값 대부분의 시나리오에 적합 하지만 환경에 특별 한 요구 사항이 있으면 변경할 수 있습니다. 예를 들어 네트워크 환경에서 5 초 동안 유휴 상태인 연결을 닫은 경우에 keepalive 값이 감소 해야 합니다.

<a id="connectiontimeout"></a>

### <a name="connectiontimeout"></a>ConnectionTimeout

이 설정은 열기 및 닫기 새 연결을 열기 전에 응답을 받기 위해 대기 중인 전송 연결을 해제 하는 시간을 나타냅니다. 기본값은 110 초입니다.

이 설정은 경우 keepalive 기능이 해제 된 long에만 적용 일반적으로 적용 됩니다. 폴링 전송을 합니다. 다음 다이어그램은 long으로이 설정의 효과 보여 줍니다. 폴링 전송 연결입니다.

![긴 폴링 전송 연결입니다.](handling-connection-lifetime-events/_static/image7.png)

<a id="disconnecttimeout"></a>

### <a name="disconnecttimeout"></a>Disconnecttimeout은

이 설정은 발생 하기 전에 전송 연결이 끊긴 후 대기 하는 시간의 양을 나타냅니다는 `Disconnected` 이벤트입니다. 기본값은 30초입니다. 설정 하는 경우 `DisconnectTimeout`, `KeepAlive` 의 1/3로 자동 설정 됩니다는 `DisconnectTimeout` 값입니다.

<a id="keepalive"></a>

### <a name="keepalive"></a>KeepAlive

이 설정은 유휴 연결을 통해 keepalive 패킷을 보내기 까지의 대기 시간을 나타냅니다. 기본값은 10 초입니다. 이 값의 1/3 개 이상의 아니어야는 `DisconnectTimeout` 값입니다.

모두 설정 하려는 경우 `DisconnectTimeout` 및 `KeepAlive`설정, `KeepAlive` 후 `DisconnectTimeout`합니다. 그렇지 않으면 프로그램 `KeepAlive` 때 설정을 덮어쓰게 됩니다 `DisconnectTimeout` 를 자동으로 설정 `KeepAlive` 제한 시간 값의 1/3입니다.

Keepalive 기능을 사용 하지 않도록 설정 하려면 설정 `KeepAlive` null로 합니다. Keepalive 기능 long에 대 한 자동으로 사용 되지 않는지 폴링 전송을 합니다.

<a id="changetimeout"></a>

### <a name="how-to-change-timeout-and-keepalive-settings"></a>제한 시간 및 keepalive 설정을 변경 하는 방법

이러한 설정에 대 한 기본값을 변경 하려면에서 속성을 설정할 `Application_Start` 에 프로그램 *Global.asax* 다음 예제와 같이 파일입니다. 샘플 코드에 표시 된 값의 기본 값과 동일 합니다.

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample1.cs)]

<a id="notifydisconnect"></a>

## <a name="how-to-notify-the-user-about-disconnections"></a>연결 끊김에 대 한 사용자에 게 하는 방법

일부 응용 프로그램에서 연결 문제가 있을 때 사용자에 게 메시지를 표시 하는 것이 좋습니다. 방법에 대 한 몇 가지 옵션 및이 작업을 수행 하는 경우 해야 합니다. 생성 된 프록시를 사용 하는 JavaScript 클라이언트에 대 한 다음 코드 샘플은 됩니다.

- 처리는 `connectionSlow` SignalR은 모드를 다시 연결에 전달 되기 전에 연결 문제를 인식 하는 즉시 메시지를 표시 하는 이벤트입니다.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample2.js)]
- 처리는 `reconnecting` SignalR 연결 끊김을 인식 하며 모드를 다시 연결로 이동 하는 경우 메시지를 표시 하는 이벤트입니다.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample3.js)]
- 처리는 `disconnected` 다시 연결 하려고 할 때 메시지를 표시 하는 이벤트 시간이 초과 되었습니다. 이 시나리오에서는 다시 서버와의 연결이 다시 설정 하는 유일한 방법은를 호출 하 여 SignalR 연결을 다시 시작 되는 `Start` 메서드는 새 연결 ID를 생성 됩니다 다음 코드 예제는 플래그를 사용 하 여 호출 하 여 SignalR 연결에 정상적인 종료가 하지 후 다시 연결 제한 시간 후에 알림 발급 하 고 있는지 확인 하 고 `Stop` 메서드.

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample4.js)]

<a id="continuousreconnect"></a>

## <a name="how-to-continuously-reconnect"></a>지속적으로 다시 연결 하는 방법

일부 응용 프로그램에서 손실 된 후 다시 연결 시도 시간이 초과 되었습니다 자동으로 연결을 다시 설정 하는 것이 좋습니다. 이러한 파일을 호출 하면는 `Start` 메서드에서 프로그램 `Closed` 이벤트 처리기 (`disconnected` JavaScript 클라이언트에서 이벤트 처리기). 호출 하기 전에 시간 동안 대기 하는 것이 좋습니다 `Start` 너무 있으므로이 방지 하기 위해 자주 서버나 실제 연결 사용할 수 없는 경우. 다음 코드 샘플은 JavaScript 클라이언트는 생성 된 프록시를 사용 하 여입니다.

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample5.js)]

모바일 클라이언트에서 인식 하는 잠재적인 문제 연속 회 시도 서버 또는 물리적 연결을 사용할 수 없는 경우 불필요 한 배터리 소모 될 수 있다는 것입니다.

<a id="disconnectclientfromserver"></a>

## <a name="how-to-disconnect-a-client-in-server-code"></a>서버 코드에서 클라이언트 연결을 끊을 하는 방법

SignalR 1.1.1 버전에는 클라이언트 연결 끊기에 대 한 기본 제공 서버 API 없습니다. [나중에이 기능을 추가 하기 위한 계획](https://github.com/SignalR/SignalR/issues/2101)합니다. 현재 SignalR 릴리스에서 클라이언트가 서버에서 분리 하는 가장 간단한 방법은 클라이언트에서 disconnect 메서드를 구현 하 고 서버에서이 메서드를 호출 하는 합니다. 다음 코드 예제는 생성 된 프록시를 사용 하는 JavaScript 클라이언트에 대 한 disconnect 메서드를 보여줍니다.

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample6.js)]

> [!WARNING]
> 보안-클라이언트 연결 끊기에 대 한이 방법을 아니고 제안 된 기본 제공 된 API를 해결 하는 시나리오는 클라이언트가 다시 연결할 수 없습니다 또는 해킹된 코드를 제거할 수 있으므로 악성 코드를 실행 하는 해킹된 클라이언트에는 `stopClient` 메서드 또는 변경 역할입니다. 상태 저장 서비스 거부 (DOS) 보호를 구현 하는 데 적합 한 곳 형식이 아니라 프레임 워크 또는 서버 계층 프런트 엔드 인프라에 대신 합니다.
