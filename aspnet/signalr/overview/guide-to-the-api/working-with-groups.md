---
uid: signalr/overview/guide-to-the-api/working-with-groups
title: SignalR에서 그룹 사용 | Microsoft Docs
author: pfletcher
description: 이 항목에서는 허브 API를 사용 하 여 그룹 멤버 자격 정보를 유지 하는 방법을 설명 합니다.
ms.author: aspnetcontent
ms.date: 06/10/2014
ms.assetid: cd378ecd-3e9e-4236-b902-65916d85a048
msc.legacyurl: /signalr/overview/guide-to-the-api/working-with-groups
msc.type: authoredcontent
ms.openlocfilehash: c1df772c19bfa89c1d780d09d56c6bc4a79967c6
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37806195"
---
<a name="working-with-groups-in-signalr"></a>SignalR에서 그룹 작업
====================
하 여 [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)

> 이 항목에서는 사용자 그룹에 추가 하 여 그룹 멤버 자격 정보를 유지 하는 방법을 설명 합니다. 
> 
> ## <a name="software-versions-used-in-this-topic"></a>이 항목에서 사용 하는 소프트웨어 버전
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
> 이전 버전의 SignalR에 대 한 정보를 참조 하세요 [SignalR 이전 버전](../older-versions/index.md)합니다.
> 
> ## <a name="questions-and-comments"></a>질문이 나 의견이 있으면
> 
> 이 자습서를 연결 하는 방법 및 새로운 개선할 수 있습니다 페이지의 맨 아래에 의견에서에 의견을 남겨 주세요. 에 자습서로 직접 관련 되지 않은 질문이 있을 경우 게시할 수 하는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.


## <a name="overview"></a>개요

SignalR에서 그룹에 연결 된 클라이언트의 지정 된 하위 집합에 메시지 브로드캐스트 하는 방법을 제공합니다. 그룹의 클라이언트에서 모든 수 있고 클라이언트가 여러 그룹의 멤버일 수 있습니다. 명시적으로 그룹을 만들 필요가 없습니다. 실제로 그룹 Groups.Add에 대 한 호출에 해당 이름을 지정 하는 처음으로 자동으로 만들어집니다 및 마지막 연결에 대 한 멤버 자격에서 제거할 때 삭제 됩니다. 그룹을 사용 하 여 소개를 참조 하세요 [허브 클래스에서 그룹 멤버 자격을 관리 하는 방법을](hubs-api-guide-server.md#groupsfromhub) Hubs API-Server 가이드에서에서.

그룹 멤버 자격 목록 또는 그룹 목록을 가져오기 위한 API는 없습니다. SignalR 클라이언트와 pub/sub 모델을 기반으로 하는 그룹에 메시지를 전송 하 고 서버 그룹 또는 그룹 멤버 자격 목록을 유지 관리 하지 않습니다. 이렇게 하면 확장성을 최대화 하기 때문에 웹 팜에 노드를 추가할 때마다 SignalR 유지 관리 하는 모든 상태를 새 노드에 전파 합니다.

사용 하 여 그룹에 사용자를 추가 하 여 `Groups.Add` 메서드인 사용자 현재 연결 기간 동안 해당 그룹에 전달 하는 메시지를 수신 하지만 해당 그룹의 멤버 자격 사용자의 현재 연결 지속 되지 않습니다. 그룹과 그룹 멤버 자격에 대 한 정보를 영구적으로 유지 하려는 경우 database 또는 Azure table storage와 같은 리포지토리에서 데이터를 저장 해야 합니다. 그런 다음 사용자가 응용 프로그램에 연결 될 때마다 사용자가 속한 그룹 저장소에서 검색 하 수동으로 이러한 그룹에 해당 사용자를 추가 합니다.

임시 중단 후 다시 연결할 때 사용자 자동으로 다시 조인 이전에 할당 된 그룹입니다. 그룹에 자동으로 다시 참여 새 연결을 설정할 때가 아니라 다시 연결할 때 때만 적용 됩니다. 디지털 서명 된 토큰을 이전에 할당 된 그룹 목록을 포함 하는 클라이언트에서 전달 됩니다. 사용자 요청 된 그룹에 속하는지 여부를 확인 하려는 경우에 기본 동작을 재정의할 수 있습니다.

이 항목은 다음 섹션으로 구성되어 있습니다.

- [사용자 추가 및 제거](#add)
- [그룹의 멤버를 호출합니다.](#call)
- [그룹 멤버 자격 데이터베이스에 저장](#storedatabase)
- [Azure table storage에 저장 그룹 멤버 자격](#storeazuretable)
- [다시 연결 하는 경우 그룹 구성원 자격 확인](#verify)

<a id="add"></a>

## <a name="adding-and-removing-users"></a>사용자 추가 및 제거

호출을 추가 하거나 그룹에서 사용자를 제거 하려면 합니다 [추가](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) 하거나 [제거](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) 메서드 및 사용자의 연결 id 및 그룹의 이름을 매개 변수로 전달 합니다. 연결이 끝나면 그룹에서 사용자를 수동으로 제거 하 고 필요가 없습니다.

다음 예제는 `Groups.Add` 및 `Groups.Remove` 허브 메서드에서 사용 되는 메서드.

[!code-csharp[Main](working-with-groups/samples/sample1.cs?highlight=5,10)]

합니다 `Groups.Add` 고 `Groups.Remove` 메서드가 비동기적으로 실행 합니다.

그룹에 클라이언트를 추가 하 고 클라이언트에 그룹을 사용 하 여 메시지를 즉시 보내도록 하려면 Groups.Add 메서드를 먼저 완료 되도록 해야 합니다. 다음 코드 예제에는 작업을 수행 하는 방법을 보여 줍니다.

[!code-csharp[Main](working-with-groups/samples/sample2.cs?highlight=1,3)]

일반적으로 포함 하면 안 `await` 호출 하는 경우는 `Groups.Remove` 메서드 하므로 제거 하려고 하는 연결 id를 더 이상 사용할 수 없습니다. 이런 경우 `TaskCanceledException` 요청 시간이 초과 되 면 throw 됩니다. 경우 응용 프로그램 사용자 그룹에 메시지를 보내기 전에 그룹에서 제거 되어 있는지 확인 해야 합니다를 추가할 수 있습니다 `await` Groups.Remove를 하 고 다음 catch 하기 전에 `TaskCanceledException` throw 될 수 있는 예외입니다.

<a id="call"></a>

## <a name="calling-members-of-a-group"></a>그룹의 멤버를 호출합니다.

다음 예제와 같이 그룹의 구성원 또는 그룹의 멤버만 지정 된 모든 메시지를 보낼 수 있습니다.

- **모든** 지정된 된 그룹의 클라이언트를 연결 합니다. 

    [!code-css[Main](working-with-groups/samples/sample3.css)]
- 지정된 된 그룹의 클라이언트를 연결 된 모든 **지정 된 클라이언트를 제외 하 고**연결 ID로 식별 된, 

    [!code-csharp[Main](working-with-groups/samples/sample4.cs)]
- 지정된 된 그룹의 클라이언트를 연결 된 모든 **호출 클라이언트를 제외한**합니다. 

    [!code-css[Main](working-with-groups/samples/sample5.css)]

<a id="storedatabase"></a>

## <a name="storing-group-membership-in-a-database"></a>그룹 멤버 자격 데이터베이스에 저장

다음 예에서는 데이터베이스의 그룹 및 사용자 정보를 유지 하는 방법을 보여 줍니다. 모든 데이터 액세스 기술;를 사용할 수 있습니다. 그러나 다음 예제에서는 Entity Framework를 사용 하 여 모델을 정의 하는 방법을 보여 줍니다. 이러한 엔터티 모델은 데이터베이스 테이블 및 필드에 해당합니다. 데이터 구조에는 응용 프로그램의 요구 사항에 따라 크게 달라질 수 있습니다. 이 예제에서는 라는 클래스를 포함 `ConversationRoom` 스포츠 가든 등 다양 한 주제에 대 한 대화에 연결할 수 있는 응용 프로그램에 고유한 것입니다. 이 예제에는 연결에 대 한 클래스도 포함 됩니다. 연결 클래스를 사용 하는 그룹 멤버 자격을 추적 하기 위한 절대적으로 필요 하지 않습니다 하지만 사용자를 추적 하는 강력한 솔루션의 일부인 경우가 많습니다.

[!code-csharp[Main](working-with-groups/samples/sample6.cs)]

그런 다음 허브 데이터베이스에서 그룹 및 사용자 정보를 검색할 수 있으며 수동으로 사용자에 적절 한 그룹을 추가할 수 있습니다. 이 예제에서는 사용자 연결을 추적 하기 위한 코드를 포함 하지 않습니다. 이 예제에서는 합니다 `await` 하기 전에 키워드 적용 되지 않습니다 `Groups.Add` 되므로 그룹의 구성원에 게는 메시지가 즉시 전송 되지 않습니다. 적용 하려는 새 멤버를 추가한 후 즉시 그룹의 모든 멤버에 메시지를 보내려는 경우는 `await` 키워드는 비동기 작업이 완료 되도록 합니다.

[!code-csharp[Main](working-with-groups/samples/sample7.cs)]

<a id="storeazuretable"></a>

## <a name="storing-group-membership-in-azure-table-storage"></a>Azure table storage에 저장 그룹 멤버 자격

Azure 테이블 저장소를 사용 하 여 그룹 및 사용자 정보를 저장 하는 데이터베이스를 사용 하는 것과 비슷합니다. 다음 예제에서는 사용자 이름 및 그룹 이름을 저장 하는 테이블 엔터티를 보여 줍니다.

[!code-csharp[Main](working-with-groups/samples/sample8.cs)]

허브에 연결할 때 할당 된 그룹 검색 합니다.

[!code-csharp[Main](working-with-groups/samples/sample9.cs)]

<a id="verify"></a>

## <a name="verifying-group-membership-when-reconnecting"></a>다시 연결 하는 경우 그룹 구성원 자격 확인

기본적으로 SignalR에 자동으로 다시 할당 사용자 적절 한 그룹에서 연결을 삭제 하 고 연결 시간이 초과 되기 전에 다시 설정 하는 경우와 같은 임시 중단, 다시 연결 하는 경우. 다시 연결할 때 때 사용자의 그룹 정보 토큰을 전달 하 고 서버에서 해당 토큰을 확인 합니다. 사용자 그룹에 다시 참여에 대 한 확인 프로세스에 대 한 정보를 참조 하세요 [다시 연결 하는 경우 그룹에 다시 참여](../security/introduction-to-security.md#rejoingroup)합니다.

일반적으로 자동으로 그룹에 다시 연결에 다시 참여의 기본 동작을 사용 해야 합니다. 중요 한 데이터에 대 한 액세스를 제한 하는 것에 대 한 보안 메커니즘으로 SignalR 그룹을 사용 하는 것이 아닙니다. 그러나 응용 프로그램 다시 연결 하는 경우 사용자의 그룹 멤버 자격을 다시 확인 해야 합니다, 경우 기본 동작을 재정의할 수 있습니다. 기본 동작 변경 이므로 추가할 수 부담 데이터베이스에 사용자가 연결 하는 경우에 아니라 각 연결에 사용자의 그룹 멤버 자격을 가져와야 합니다.

그룹 멤버 자격을 확인 해야 하는 경우 다시 연결, 아래와 같이 할당 된 그룹의 목록을 반환 하는 새 허브 파이프라인 모듈을 만듭니다.

[!code-csharp[Main](working-with-groups/samples/sample10.cs)]

아래 강조 표시 된 대로 허브 파이프라인으로 모듈을 추가 합니다.

[!code-csharp[Main](working-with-groups/samples/sample11.cs?highlight=4)]
