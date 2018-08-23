---
uid: signalr/overview/older-versions/persistent-connection-authorization
title: SignalR 영구 연결 프로그램용 인증과 권한 부여 (SignalR 1.x) | Microsoft Docs
author: pfletcher
description: 이 항목에서는 영구 연결에 권한 부여를 적용 하는 방법을 설명 합니다. 보안 SignalR 응용 프로그램을 통합 하는 방법에 대 한 일반 정보에 대 한 중...
ms.author: riande
ms.date: 10/21/2013
ms.assetid: c34bc627-41af-4c21-a817-e97a19a7f252
msc.legacyurl: /signalr/overview/older-versions/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: 6c13a63630948a8b6bd1f6e3a6e752b9695256bf
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41839167"
---
<a name="authentication-and-authorization-for-signalr-persistent-connections-signalr-1x"></a>SignalR 영구 연결 프로그램용 인증과 권한 부여 (SignalR 1.x)
====================
하 여 [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)

> 이 항목에서는 영구 연결에 권한 부여를 적용 하는 방법을 설명 합니다. SignalR 응용 프로그램에 보안을 통합 하는 방법에 대 한 일반적인 정보를 참조 하세요 [보안 소개](index.md)합니다.


## <a name="enforce-authorization"></a>권한 부여를 적용 합니다.

사용 하는 경우 권한 부여 규칙을 적용 하는 [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) 재정의 해야 합니다는 `AuthorizeRequest` 메서드. 사용할 수 없습니다는 `Authorize` 영구 연결을 사용 하 여 특성입니다. `AuthorizeRequest` 사용자 요청된 작업을 수행할 권한이 있는지 확인 하는 모든 요청 전에 SignalR 프레임 워크에서 호출 됩니다. `AuthorizeRequest` 응용 프로그램의 표준 인증 메커니즘을 통해 사용자를 인증 하는 대신; 메서드가 클라이언트에서 호출 되지 않습니다.

아래 예제에서는 인증 된 사용자에 대 한 요청을 제한 하는 방법을 보여 줍니다.

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

AuthorizeRequest 메서드;에서 모든 사용자 지정된 권한 부여 논리를 추가할 수 있습니다. 와 같은 사용자 특정 역할에 속하는지 여부를 확인 합니다.
