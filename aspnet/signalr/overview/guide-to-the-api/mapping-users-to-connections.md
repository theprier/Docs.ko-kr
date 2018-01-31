---
uid: signalr/overview/guide-to-the-api/mapping-users-to-connections
title: "SignalR 사용자 연결에 매핑하면 | Microsoft Docs"
author: tfitzmac
description: "이 항목에는 사용자 및 해당 연결에 대 한 정보를 저장 하는 방법을 보여 줍니다. Patrick Fletcher이 도움말이 항목을 작성 하는 데 도움이 되었습니다. 이 항목에서 사용 되는 소프트웨어 버전 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/30/2014
ms.topic: article
ms.assetid: f80c08b1-3f1f-432c-980c-c7b6edeb31b1
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/guide-to-the-api/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: c4f95a3b65c57dd7cb7c5c7f1ee09daa17fa9616
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="mapping-signalr-users-to-connections"></a>SignalR 사용자 연결에 매핑
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 항목에는 사용자 및 해당 연결에 대 한 정보를 저장 하는 방법을 보여 줍니다.
> 
> Patrick Fletcher이 도움말이 항목을 작성 하는 데 도움이 되었습니다.
> 
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


## <a name="introduction"></a>소개

허브에 연결 되는 각 클라이언트 고유 연결 id를 전달 합니다. 이 값을 검색할 수 있습니다는 `Context.ConnectionId` 허브 컨텍스트 속성입니다. 응용 프로그램을 사용자 연결 id에 매핑한 매핑이 유지 하는 경우에 다음 중 하나를 사용할 수 있습니다.

- [사용자 ID 공급자 (SignalR 2)](#IUserIdProvider)
- [메모리 내 저장소](#inmemory), 사전 등
- [각 사용자에 대 한 SignalR 그룹](#groups)
- [세션에서 외부 저장소](#database)데이터베이스 테이블 또는 Azure 테이블 저장소와 같은

각각의이 구현은이 항목에 표시 됩니다. 사용 된 `OnConnected`, `OnDisconnected`, 및 `OnReconnected` 의 메서드는 `Hub` 사용자 연결 상태를 추적 하는 클래스입니다.

가장 좋은 방법은 응용 프로그램에 따라 달라 집니다.

- 응용 프로그램을 호스팅하는 웹 서버의 수입니다.
- 현재 연결 된 사용자 목록을 가져와서 해야 하는지 여부입니다.
- 응용 프로그램 또는 서버를 다시 시작 하는 경우에 그룹 및 사용자 정보를 유지 해야 하는지 여부입니다.
- 외부 서버를 호출 하 여 대기 시간 문제 인지 여부입니다.

다음 표에서 이러한 고려 사항에 대해 작동 하는 방식을 보여 줍니다.

|  | 둘 이상의 서버 | 현재 연결 된 사용자 목록을 가져옵니다. | 다시 시작한 다음 정보를 유지 합니다. | 최적의 성능 |
| --- | --- | --- | --- | --- |
| 사용자 Id 공급자 | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| 메모리 내 |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| 단일 사용자 그룹 | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| 영구 외부 | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a>IUserID 공급자

사용자 대상을 지정 하는 사용자 Id는이 기능을 통해 IUserIdProvider 새 인터페이스를 통해 IRequest에 기반 합니다.

**The IUserIdProvider**

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

기본적으로 있을 것을 사용자의 사용 하는 구현 `IPrincipal.Identity.Name` 사용자 이름으로 합니다. 이 변경 하려면 등록의 구현 `IUserIdProvider` 전역 호스트 응용 프로그램 시작 시와:

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

허브에 내 수는 다음 API 통해 이러한 사용자에 메시지를 보낼:

**특정 사용자에 게 메시지 보내기**

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a>메모리 내 저장소

다음 예제는 메모리에 저장 된 사전에 연결 및 사용자 정보를 유지 하는 방법을 보여 줍니다. 사전을 사용 하 여 한 `HashSet` 연결 id를 저장할 수 있습니다. 언제 든 지 사용자 SignalR 응용 프로그램에 둘 이상의 연결이 있을 수 있습니다. 예를 들어 사용자가 여러 장치 또는 둘 이상의 브라우저 탭을 통해 연결 된 둘 이상의 연결 id는 것입니다.

응용 프로그램이 종료 되 면 모든 정보가 손실 되 있지만 다시 채워집니다 사용자가 연결을 다시 설정 하는 것입니다. 환경의 각 서버 연결의 별도 컬렉션을 갖기 때문에 둘 이상의 웹 서버를 포함 하는 경우에 메모리 내 저장소 작동 하지 않습니다.

첫 번째 예에서는 연결에 대 한 사용자 매핑을 관리 하는 클래스를 보여 줍니다. HashSet에 대 한 키를 사용자의 이름이 됩니다.

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

다음 예에서는 허브에서 연결 매핑 클래스를 사용 하는 방법을 보여 줍니다. 클래스의 인스턴스는 변수 이름에 저장 된 `_connections`합니다.

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a>단일 사용자 그룹

각 사용자에 대 한 그룹을 만들고에 해당 사용자만 액세스 하려는 경우 해당 그룹에는 메시지를 보낼 수 있습니다. 각 그룹의 이름은 사용자의 이름입니다. 사용자에 게 둘 이상의 연결을 경우 각 연결 id는 사용자의 그룹에 추가 됩니다.

하지 수동으로 제거 해야 사용자 그룹에서 사용자 연결을 끊을 때. 이 작업은 SignalR 프레임 워크에서 자동으로 수행 됩니다.

다음 예제에서는 단일 사용자 그룹을 구현 하는 방법을 보여 줍니다.

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a>세션에서 외부 저장소

이 항목에서는 연결 정보를 저장 하기 위한 데이터베이스 또는 Azure 테이블 저장소를 사용 하는 방법을 보여 줍니다. 이 방법은 각 웹 서버는 동일한 데이터 저장소와 상호 작용할 수 때문에 웹 서버가 여러 개 있는 경우에 작동 합니다. 웹 서버 또는 응용 프로그램 다시 시작 하는 작업을 중지 하는 경우는 `OnDisconnected` 메서드가 호출 되지 않습니다. 따라서 것이 데이터 저장소에 더 이상 사용할 수 있는 연결 id에 대 한 레코드 해야 합니다. 이러한 분리 된 레코드를 정리 하려면 응용 프로그램에 관련 된 시간 범위 외부에서 생성 된 모든 연결을 무효화 하는 것이 좋습니다. 이 섹션의 예에서는 연결을 만들 때 추적에 대 한 값이 포함 되지만 백그라운드 작업으로 작업을 수행 하는 것이 좋습니다 때문에 오래 된 레코드를 정리 하는 표시 되지 않습니다.

### <a name="database"></a>데이터베이스

다음 예에서는 데이터베이스에 연결 및 사용자 정보를 저장 하는 방법을 보여 줍니다. 모든 데이터 액세스 기술; 사용할 수 있습니다. 그러나 다음 예제에서는 Entity Framework를 사용 하 여 모델을 정의 하는 방법을 보여 줍니다. 이러한 엔터티 모델 데이터베이스 테이블 및 필드에 해당합니다. 데이터 구조에 응용 프로그램의 요구 사항에 따라 크게 다를 수 있습니다.

첫 번째 예에는 많은 연결 엔터티와 연결할 수 있는 사용자 엔터티를 정의 하는 방법을 보여 줍니다.

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

그런 다음 허브에서 아래에 표시 된 코드와 함께 각 연결의 상태를 추적할 수 있습니다.

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a>Azure 테이블 저장소

다음 Azure 테이블 저장소 예제 데이터베이스 예제와 비슷합니다. Azure 테이블 저장소 서비스를 시작 해야 하는 정보를 모두 포함 되지 않습니다. 자세한 내용은 참조 [.NET에서 테이블 저장소를 사용 하는 방법을](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)합니다.

다음 예제에서는 연결 정보를 저장 하기 위한 테이블 엔터티를 보여 줍니다. 사용자 이름으로 데이터를 분할 하 고 사용자는 언제 든 지 여러 개의 연결이 있을 수 있으므로 각 엔터티에 연결 id로 식별 합니다.

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

허브에서 각 사용자의 연결 상태를 추적할 수 있습니다.

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]
