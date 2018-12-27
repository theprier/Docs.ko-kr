---
uid: signalr/overview/older-versions/scaleout-in-signalr
title: SignalR의 규모 확장 소개 1.x | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 04/29/2013
ms.assetid: 3fd9f11c-799b-4001-bd60-1e70cfc61c19
msc.legacyurl: /signalr/overview/older-versions/scaleout-in-signalr
msc.type: authoredcontent
ms.openlocfilehash: fffa424ea4b62a54b9df48aaa409541ab5d1608f
ms.sourcegitcommit: 74e3be25ea37b5fc8b4b433b0b872547b4b99186
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2018
ms.locfileid: "53287600"
---
<a name="introduction-to-scaleout-in-signalr-1x"></a>SignalR의 규모 확장 소개 1.x
====================
하 여 [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

일반적으로 두 가지 웹 응용 프로그램의 크기를 조정 하: *강화* 하 고 *확장할*합니다.

- 대형 서버 (또는 더 큰 VM)를 사용 하 여 더 많은 RAM, Cpu 등을 사용 하 여 의미를 확장 합니다.
- 부하를 처리할 서버를 추가 하는 수단을 확장 합니다.

컴퓨터의 크기에 제한에 빠르게 도달 하는 확장 문제가 발생 합니다. 그 외에도 규모 확장 해야 합니다. 그러나를 규모 확장할 때 클라이언트가 서로 다른 서버 라우팅할 가져올 수 있습니다. 하나의 서버에 연결 된 클라이언트에서 다른 서버에서 보낸 메시지를 받지 못합니다.

![](scaleout-in-signalr/_static/image1.png)

한 가지 해결책은 라는 구성 요소를 사용 하 여 서버 간에 메시지를 전달 하는 *백플레인*합니다. 활성화 백 블 레인에를 사용 하 여 각 응용 프로그램 인스턴스가 메시지를 백플레인에 보냅니다 및 백플레인에서 다른 응용 프로그램 인스턴스에 전달 합니다. (전자를 백플레인으로 병렬 커넥터 그룹입니다. 비유 하자면를 SignalR 백플레인으로 연결 여러 서버입니다.)

![](scaleout-in-signalr/_static/image2.png)

SignalR에는 현재 세 가지 백플레인을 제공합니다.

- **Azure Service Bus**합니다. Service Bus는 메시징 인프라를 통해 느슨하게 결합 된 방식으로 메시지를 보내도록 구성 요소입니다.
- **Redis**합니다. Redis는 메모리 내 키-값 저장소입니다. Redis는 메시지를 보내기 위한 ("pub/sub") 게시/구독 패턴을 지원 합니다.
- **SQL Server**합니다. SQL Server 백플레인에서 SQL 테이블에 메시지를 씁니다. 백플레인에서 효율적인 메시징에 대 한 Service Broker를 사용합니다. 그러나 해당 Service Broker를 사용 하지 않는 경우에 작동 합니다.

Azure에서 응용 프로그램을 배포 하는 경우에 Azure Service Bus 백플레인으로 사용 하는 것이 좋습니다. 사용자 고유의 서버 팜에 배포 하는 경우 SQL Server 또는 Redis 백플레인 것이 좋습니다.

각 백플레인에 대 한 단계별 자습서를 포함 하는 다음 항목:

- [Azure Service Bus로 SignalR 규모 확장](scaleout-with-windows-azure-service-bus.md)
- [Redis로 SignalR 규모 확장](scaleout-with-redis.md)
- [SQL Server로 SignalR 규모 확장](scaleout-with-sql-server.md)

## <a name="implementation"></a>구현

Signalr에서 모든 메시지는 메시지 버스를 통해 전송 됩니다. 메시지 버스 구현 된 [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) 게시/구독 추상화를 제공 하는 인터페이스입니다. 기본 대체 하 여 작업의 백플레인 **IMessageBus** 해당 백플레인 위한 버스를 사용 하 여 합니다. Redis에 대 한 메시지 버스는 예를 들어 [RedisMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.redis.redismessagebus(v=vs.100).aspx)를 사용 하 여 Redis [pub/sub](http://redis.io/topics/pubsub) 메시지를 수신 하는 메커니즘.

각 서버 인스턴스에 백플레인에서 버스를 통해 연결할 수 있습니다. 메시지를 보낼 때 백 블 레인에 이동 하 고 백플레인에서 모든 서버에 보냅니다. 백플레인에서에서 메시지를 가져옵니다 하는 서버를 해당 로컬 캐시에서 메시지를 저장 합니다. 서버는 다음 로컬 캐시에서 클라이언트로 메시지를 배달합니다.

각 클라이언트 연결에 대 한 커서를 사용 하 여 클라이언트의 메시지 스트림을 읽는 진행을 추적 합니다. (커서 메시지 스트림의 위치를 나타냅니다.) 클라이언트 연결을 끊고 다시 연결을 하는 경우 클라이언트의 커서 값 뒤에 도착 한 메시지 버스를 요청 합니다. 연결을 사용 하는 경우 동일한 작업 수행 [긴 폴링](../getting-started/introduction-to-signalr.md#transports)합니다. 긴 폴링 요청에는 다음이 완료 되 면 클라이언트는 새 연결을 열고 하 고 커서 뒤 도착 하는 요청 합니다.

커서 메커니즘의 작동을 클라이언트에서 다른 서버에 라우팅되는 경우에 다시 연결 합니다. 백플레인에서 모든 서버를 인식 하 고 클라이언트가 연결 하는 서버는 중요 하지 않습니다.

## <a name="limitations"></a>제한 사항

백플레인으로 사용 하 여, 최대 메시지 처리량은 클라이언트와 직접 상담할 단일 서버 노드의 경우 보다 낮습니다. 백플레인에서 백플레인에서 병목 현상이 발생할 수 있으므로 모든 노드에 모든 메시지를 전달 하는 때문입니다. 이 제한은 문제가 있는지 여부를 응용 프로그램에 따라 달라 집니다. 예를 들어, 다음은 몇 가지 일반적인 SignalR 시나리오입니다.

- [서버 브로드캐스트](tutorial-server-broadcast-with-aspnet-signalr.md) (예: 주식 시세 표시기): 백플레인 서버 메시지가 전송 되는 속도 제어 하므로이 시나리오에 대 한 잘 작동 합니다.
- [클라이언트-](tutorial-getting-started-with-signalr.md) (채팅 예): 이 시나리오에서는 클라이언트의 수를 사용 하 여 메시지 수가 조정 하는 경우 백플레인에서 병목 지점이 될 수 있습니다. 즉, 메시지의 속도 증가 함에 따라 비례적으로 더 많은 클라이언트 조인 합니다.
- [고주파수](tutorial-high-frequency-realtime-with-signalr.md) (예: 실시간 게임): 이 시나리오를 백플레인으로 권장 되지 않습니다.

## <a name="enabling-tracing-for-signalr-scaleout"></a>SignalR 규모 확장에 대 한 추적을 사용 하도록 설정

백플레인에 대 한 추적을 사용 하려면 다음 섹션에서는 루트 아래에 있는 web.config 파일에 추가 **구성** 요소:

[!code-html[Main](scaleout-in-signalr/samples/sample1.html)]
