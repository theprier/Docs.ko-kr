---
uid: signalr/overview/older-versions/mapping-users-to-connections
title: SignalR 사용자를 SignalR 연결 매핑 1.x | Microsoft Docs
author: pfletcher
description: 이 항목에서는 사용자 및 해당 연결에 대 한 정보를 유지 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 10/17/2013
ms.assetid: ebbc93a8-e6c4-4122-8e0d-3aa42293c747
msc.legacyurl: /signalr/overview/older-versions/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: ba7bbea25cd35f8ba23901c5f8db08404c91bd52
ms.sourcegitcommit: 74e3be25ea37b5fc8b4b433b0b872547b4b99186
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2018
ms.locfileid: "53287490"
---
<a name="mapping-signalr-users-to-connections-in-signalr-1x"></a>SignalR 사용자를 SignalR 연결 매핑 1.x
====================
하 여 [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 항목에서는 사용자 및 해당 연결에 대 한 정보를 유지 하는 방법을 보여 줍니다.


## <a name="introduction"></a>소개

허브에 연결 하는 각 클라이언트에 고유 연결 id를 전달 합니다. 이 값을 검색할 수 있습니다는 `Context.ConnectionId` 허브 컨텍스트의 속성입니다. 응용 프로그램을 사용자 연결 id를 매핑하고 해당 매핑을 유지 하는 경우 다음 중 하나를 사용할 수 있습니다.

- [메모리 내 저장소](#inmemory), 사전 등
- [각 사용자에 대 한 SignalR 그룹](#groups)
- [외부 영구 저장소](#database), 데이터베이스 테이블 또는 Azure table storage와 같은

이러한 구현은 각각이 항목에 표시 됩니다. 사용할 합니다 `OnConnected`, `OnDisconnected`, 및 `OnReconnected` 의 메서드는 `Hub` 사용자 연결 상태를 추적 하는 클래스입니다.

가장 좋은 방법은 응용 프로그램에 따라 달라 집니다.

- 응용 프로그램을 호스팅하는 웹 서버의 수입니다.
- 현재 연결 된 사용자의 목록을 가져오려면 해야 하는지 여부입니다.
- 응용 프로그램 또는 서버 다시 시작 하는 경우 그룹 및 사용자 정보를 유지 해야 하는지 여부입니다.
- 외부 서버를 호출 하는 대기 시간 문제 인지 여부입니다.

다음 표에서 이러한 고려 사항에 대 한 작동 하는 방법을 보여 줍니다.

|  | 둘 이상의 서버 | 현재 연결 된 사용자의 목록을 가져옵니다. | 다시 시작한 후 정보를 유지 합니다. | 최적의 성능 |
| --- | --- | --- | --- | --- |
| 메모리 내 |  | ![](mapping-users-to-connections/_static/image1.png) |  | ![](mapping-users-to-connections/_static/image2.png) |
| 단일 사용자 그룹 | ![](mapping-users-to-connections/_static/image3.png) |  |  | ![](mapping-users-to-connections/_static/image4.png) |
| 외부 영구 | ![](mapping-users-to-connections/_static/image5.png) | ![](mapping-users-to-connections/_static/image6.png) | ![](mapping-users-to-connections/_static/image7.png) |  |

<a id="inmemory"></a>

## <a name="in-memory-storage"></a>메모리 내 저장소

다음 예제에서는 메모리에 저장 되어 있는 사전에 연결 및 사용자 정보를 유지 하는 방법을 보여 줍니다. 사전을 사용 하는 `HashSet` 연결 id를 저장 합니다. 사용자는 언제 든 지 SignalR 응용 프로그램에 둘 이상의 연결을 가질 수 없습니다. 예를 들어, 여러 장치 또는 둘 이상의 브라우저 탭을 통해 연결 된 사용자는 둘 이상의 연결 id를 것입니다.

응용 프로그램을 종료 하는 경우 모든 정보가 손실 되지만 다시 채워지고 사용자가 연결을 다시 설정 합니다. 환경의 각 서버에 별도 컬렉션을 연결 해야 합니다. 때문에 둘 이상의 웹 서버를 포함 하는 경우에 메모리 내 저장소 작동 하지 않습니다.

첫 번째 예제에서는 연결에 대 한 사용자 매핑을 관리 하는 클래스를 보여 줍니다. HashSet에 대 한 키를 사용자의 이름이 됩니다.

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

다음 예제에는 허브에서 연결 매핑을 클래스를 사용 하는 방법을 보여 줍니다. 클래스의 인스턴스 변수 이름에 저장 된 `_connections`합니다.

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a>단일 사용자 그룹

각 사용자에 대 한 그룹을 만들고 해당 사용자만 도달 하려고 할 때 해당 그룹에 메시지를 보낼 수 있습니다. 각 그룹의 이름은 사용자의 이름입니다. 사용자가 여러 개 연결 하는 경우 각 연결 id는 사용자의 그룹에 추가 됩니다.

해야 수동으로 제거 하면 사용자 그룹에서 사용자 연결을 끊을 때. 이 작업은 SignalR 프레임 워크에서 자동으로 수행 됩니다.

다음 예제에서는 단일 사용자 그룹을 구현 하는 방법을 보여 줍니다.

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a>외부 영구 저장소

이 항목에서는 데이터베이스 또는 Azure 테이블 저장소를 사용 하 여 연결 정보를 저장 하는 방법을 보여 줍니다. 이 방법은 각 웹 서버는 동일한 데이터 저장소와 상호 작용할 수 있으므로 웹 서버가 여러 개 있는 경우에 작동 합니다. 웹 서버 작업 또는 응용 프로그램이 다시 시작, 중지는 `OnDisconnected` 메서드가 호출 되지 않습니다. 따라서 데이터 리포지토리에 유효 하지 않은 연결 id에 대 한 레코드 되어 가능한 것입니다. 이러한 분리 된 레코드를 정리 하려면 응용 프로그램에 관련 된 시간 범위 외부에서 만든 모든 연결을 무효화 하는 것이 좋습니다. 이 섹션의 예제에서는 생성 된 연결 하는 경우 추적에 대 한 값을 포함 하지만 백그라운드 프로세스로 작업을 수행 하는 것이 좋습니다 때문에 오래 된 레코드를 정리 하는 방법을 표시 하지 않습니다.

### <a name="database"></a>데이터베이스

다음 예에서는 데이터베이스에 연결 및 사용자 정보를 유지 하는 방법을 보여 줍니다. 모든 데이터 액세스 기술;를 사용할 수 있습니다. 그러나 다음 예제에서는 Entity Framework를 사용 하 여 모델을 정의 하는 방법을 보여 줍니다. 이러한 엔터티 모델은 데이터베이스 테이블 및 필드에 해당합니다. 데이터 구조에는 응용 프로그램의 요구 사항에 따라 크게 달라질 수 있습니다.

첫 번째 예제에는 여러 연결 엔터티를 사용 하 여 연결할 수 있는 사용자 엔터티를 정의 하는 방법을 보여 줍니다.

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

그런 다음 허브에서 아래 표시 된 코드를 사용 하 여 각 연결의 상태를 추적할 수 있습니다.

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

### <a name="azure-table-storage"></a>Azure 테이블 저장소

다음 Azure table storage 예제 데이터베이스 예제와 비슷합니다. Azure Table Storage 서비스를 사용 하 여 시작 해야 하는 정보를 모두 포함 되지 않습니다. 정보를 참조 하세요 [.NET에서 Table storage를 사용 하는 방법을](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)합니다.

다음 예제에서는 연결 정보를 저장 하는 것에 대 한 테이블 엔터티를 보여 줍니다. 사용자 이름으로 데이터를 분할 하 고 사용자는 언제 든 지 여러 연결을 가질 수 있도록 연결 id를 기준으로 각 엔터티를 식별 합니다.

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

허브의 각 사용자의 연결의 상태를 추적할 수 있습니다.

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]
