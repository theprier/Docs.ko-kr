---
uid: signalr/overview/performance/scaleout-in-signalr
title: "SignalR에서 확장 소개 | Microsoft Docs"
author: MikeWasson
description: "이전 버전의에 대 한 내용은이 항목의 버전 2 이전 버전을 Visual Studio 2013.NET 4.5 SignalR이이 항목에서 사용 하는 소프트웨어 버전 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: 7e781fc1-1c1f-45a8-bc1d-338e96dbe9c9
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/performance/scaleout-in-signalr
msc.type: authoredcontent
ms.openlocfilehash: 4f1ad959c45281cdd831c37c2e3ca428f3fae9a0
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="introduction-to-scaleout-in-signalr"></a>SignalR에서 확장 소개
====================
여 [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)

> ## <a name="software-versions-used-in-this-topic"></a>이 항목에서 사용 되는 소프트웨어 버전
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - .NET 4.5
> - SignalR 버전 2
>   
> 
> 
> ## <a name="previous-versions-of-this-topic"></a>이 항목의 이전 버전
> 
> 이전 버전의 SignalR에 대 한 정보를 참조 하십시오. [SignalR 이전 버전](../older-versions/index.md)합니다.
> 
> ## <a name="questions-and-comments"></a>질문이 나 의견이
> 
> 이 자습서를 연결 하는 방법 및 페이지의 맨 아래에 주석에서 향상 될 수 있습니다 어떻게에 의견을 남겨 주세요. 자습서를 직접 관련 되지 않는 질문 해야 하도록를 게시할 수 있습니다는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.


일반적으로 두 가지 웹 응용 프로그램의 크기를 조정 하려면: *수직* 및 *확장할*합니다.

- 대형 서버 (또는 더 큰 VM)를 사용 하 여 더 많은 RAM, Cpu, 등으로 평균 수직 확장 합니다.
- 부하를 처리할 서버를 추가 하는 수단을 확장 합니다.

컴퓨터의 크기에 제한이 신속 하 게 도달 하면는 수직 확장 문제가 발생 합니다. 이 외 수평 확장 해야 합니다. 그러나 확장 시, 클라이언트가 서로 다른 서버 라우팅할 얻을 수 있습니다. 하나의 서버에 연결 된 클라이언트에서 다른 서버에서 보낸 메시지를 받지 못합니다.

![](scaleout-in-signalr/_static/image1.png)

한 가지 해결 방법은 라는 구성 요소를 사용 하 여 서버 간에 메시지를 전달 하는 *백플레인*합니다. 사용 하도록 설정 하는 백플레인에 각 응용 프로그램 인스턴스에 메시지를 백플레인에 보내고 백플레인에서 다른 응용 프로그램 인스턴스에 전달 합니다. (전기 부문에서 백플레인에 병렬 커넥터의 그룹입니다. 비유, SignalR 백플레인 연결 여러 서버 합니다.)

![](scaleout-in-signalr/_static/image2.png)

SignalR 현재 세 가지 백플레인을 제공합니다.

- **Azure 서비스 버스**합니다. 서비스 버스에 구성 요소가 느슨하게 결합 된 방식으로 메시지를 보낼 수 있도록 하는 메시징 인프라입니다.
- **Redis**합니다. Redis는 메모리에 키-값 저장소입니다. Redis는 메시지를 보내기 위한 게시/구독 ("pub/sub") 패턴을 지원 합니다.
- **SQL Server**합니다. SQL Server 백플레인에서 SQL 테이블에 메시지를 씁니다. 백플레인에서 효율적인 메시징에 대 한 Service Broker를 사용 합니다. 그러나 해당 Service Broker를 사용 하지 않는 경우에 작동 합니다.

사용 하 여 Redis 백플레인으로 사용 하 여 Azure에서 응용 프로그램을 배포 하는 경우 고려 [Azure Redis Cache](https://azure.microsoft.com/en-us/services/cache/)합니다. 사용자 고유의 서버 팜에 배포 하는 경우 SQL Server 또는 Redis 백플레인 것이 좋습니다.

다음 항목에서는 각 백플레인에 대 한 단계별 자습서 포함 되어 있습니다.

- [Azure 서비스 버스에 SignalR 확장](scaleout-with-windows-azure-service-bus.md)
- [Redis와 함께 SignalR 확장](scaleout-with-redis.md)
- [SQL Server와 함께 SignalR 확장](scaleout-with-sql-server.md)

## <a name="implementation"></a>구현

SignalR에 모든 메시지는 메시지 버스를 통해 전송 됩니다. 메시지 버스 구현 하는 [IMessageBus](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) 인터페이스에는 게시/구독 추상화를 제공 합니다. 기본 대체 하 여 작업의 백플레인 **IMessageBus** 는 버스 해당 백플레인에서 위한 것입니다. 예를 들어 Redis 용 메시지 버스는 [RedisMessageBus](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.redis.redismessagebus(v=vs.100).aspx), Redis를 사용 하 여 [pub/sub](http://redis.io/topics/pubsub) 메시지를 송수신 하는 메커니즘입니다.

버스를 통해 백플레인에서에 각 서버 인스턴스에 연결합니다. 메시지를 보낼 때를 백플레인에 이동 하 고 백플레인에서 모든 서버에 보냅니다. 서버에서 메시지 백플레인에서 받으면 메시지 로컬 캐시에 배치 합니다. 서버는 다음 로컬 캐시에서 클라이언트에 메시지를 배달 합니다.

각 클라이언트 연결에 대 한 커서를 사용 하는 클라이언트의 진행 상황 메시지 스트림을 읽는 추적 합니다. (커서 메시지 스트림 내의 위치를 나타냅니다.) 클라이언트 연결을 끊고 다시 연결을 하는 경우 클라이언트의 커서 값 뒤에 도착 하는 모든 메시지 버스를 요청 합니다. 동일한 상황이 연결을 사용 하는 경우 [긴 폴링](../getting-started/introduction-to-signalr.md#transports)합니다. 긴 폴링 요청 완료 되 면 클라이언트는 새 연결을 열고 하 고 커서 뒤 도착 하는 요청 합니다.

커서 메커니즘의 작동 클라이언트에 다른 서버에 전달 되는 경우에 다시 연결 합니다. 백플레인에서 모든 서버를 인식 하며 클라이언트가 연결 하는 서버는 문제가 되지 않습니다.

## <a name="limitations"></a>제한 사항

백플레인에 사용 하 여 최대 메시지 처리량은 단일 서버 노드를 직접 클라이언트와 통신 하는 경우 보다 낮습니다. 백플레인에서 백플레인에서 병목 지점이 될 수 있도록 모든 노드에 모든 메시지를 전달 하는 때문입니다. 이 제한 사항은 문제가 있는지 여부를 응용 프로그램에 따라 달라 집니다. 예를 들어 다음은 몇 가지 일반적인 SignalR 시나리오입니다.

- [서버 브로드캐스트](../getting-started/tutorial-server-broadcast-with-signalr.md) (예: 주식 시세): 백플레인 서버 메시지를 보내는 속도 제어 하기 때문에이 시나리오에 대 한 잘 작동 합니다.
- [클라이언트-](../getting-started/tutorial-getting-started-with-signalr.md) (예: 채트):이 시나리오에서는 클라이언트의 수와 크기와 메시지 수가 조정 백플레인에서 병목 지점이 될 수 있습니다; 그리고 즉, 증가 하는 메시지의 속도 비율에 따라 더 많은 클라이언트에 조인 합니다.
- [높은 주파수 실시간](../getting-started/tutorial-high-frequency-realtime-with-signalr.md) (예: 실시간 게임): 백플레인에이 시나리오에 적합 하지 않습니다.

## <a name="enabling-tracing-for-signalr-scaleout"></a>SignalR 확장에 대 한 추적을 사용합니다.

백플레인에 대 한 추적을 사용 하려면 다음 섹션에서는 루트 아래에 있는 web.config 파일에 추가 **구성** 요소:

[!code-html[Main](scaleout-in-signalr/samples/sample1.html)]
