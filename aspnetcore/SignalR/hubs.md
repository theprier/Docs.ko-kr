---
title: ASP.NET Core SignalR 허브를 사용 합니다.
author: rachelappel
description: ASP.NET Core SignalR 허브를 사용 하는 방법을 알아봅니다.
manager: wpickett
ms.author: rachelap
ms.custom: mvc
ms.date: 03/30/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: signalr/hubs
ms.openlocfilehash: 73397ba6951f2752653575920bdf739439874366
ms.sourcegitcommit: 7d02ca5f5ddc2ca3eb0258fdd6996fbf538c129a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/03/2018
---
# <a name="use-hubs-in-signalr-for-aspnet-core"></a>ASP.NET Core에서 SignalR 허브를 사용 하 여

여 [Rachel Appel](https://twitter.com/rachelappel) 및 [Kevin Griffin](https://twitter.com/1kevgriff)

## <a name="what-is-a-signalr-hub"></a>SignalR 허브 이란

SignalR 허브 API를 사용 하면 서버에서 연결 된 클라이언트에서 메서드를 호출할 수 있습니다. 서버 코드에서 클라이언트에 의해 호출 되는 메서드를 정의 합니다. 클라이언트 코드는 서버에서 호출 하는 메서드를 정의 합니다. SignalR 하는 모든 실시간 클라이언트-서버 및 서버 클라이언트 통신을 가능 하 게 하는 백그라운드 처리 합니다.

## <a name="configure-signalr-hubs"></a>SignalR 허브를 구성 합니다.

SignalR 미들웨어를 호출 하 여 구성 된 일부 서비스 필요 `services.AddSignalR`합니다.

[!code-csharp[Configure service](hubs/sample/startup.cs?range=35)]

SignalR 기능에는 ASP.NET Core 응용 프로그램을 추가할 때 호출 하 여 SignalR 경로 설정 `app.UseSignalR` 에 `Startup.Configure` 메서드.

[!code-csharp[Configure routes to hubs](hubs/sample/startup.cs?range=55-58)]

## <a name="create-and-use-hubs"></a>만들기 및 허브를 사용 합니다.

상속 되는 클래스를 선언 하 여 허브를 만들 `Hub`, public 메서드를 추가 합니다. 클라이언트에서으로 정의 된 메서드를 호출할 수 `public`합니다.

[!code-csharp[Create and use hubs](hubs/sample/chathub.cs?range=10-13)]

반환 형식 및 C# 메서드에서 마찬가지로 배열 및 복합 형식을 포함 하 여 매개 변수를 지정할 수 있습니다. SignalR은 serialization 및 deserialization 복잡 한 개체 및 배열에 매개 변수 및 반환 값을 처리합니다.

## <a name="the-clients-object"></a>클라이언트 개체

각 인스턴스는 `Hub` 클래스 라는 속성이 `Clients` 서버와 클라이언트 간의 통신에 대 한 다음 멤버를 포함 하는:

| 속성 | 설명 |
| ------ | ----------- |
| `All` | 연결 된 모든 클라이언트에서 메서드를 호출합니다. |
| `Caller` | 클라이언트 허브 메서드를 호출한 메서드를 호출 합니다. |
| `Others` | 메서드를 호출한 클라이언트를 제외한 모든 연결 된 클라이언트에서 메서드를 호출 합니다. |

또한는 `Hub` 클래스에는 다음과 같은 메서드가 들어 있습니다.

| 메서드 | 설명 |
| ------ | ----------- |
| `AllExcept` | 지정된 된 연결을 제외한 모든 연결 된 클라이언트에서 메서드를 호출합니다. |
| `Client` | 특정 연결 된 클라이언트에 메서드를 호출합니다. |
| `Clients` | 특정 연결 된 클라이언트에서 메서드를 호출합니다. |
| `Group` | 지정된 된 그룹의 모든 연결에 메시지를 보냅니다.  |
| `GroupExcept` | 지정된 된 연결을 제외 하 고 지정된 된 그룹의 모든 연결에 메시지를 보냅니다. |
| `Groups` | 연결의 여러 그룹에 메시지를 보냅니다.  |
| `OthersInGroup` | 그룹 허브 메서드를 호출한 클라이언트 제외 하 고 연결에 메시지를 보냅니다.  |
| `User` | 특정 사용자와 관련 된 모든 연결에 메시지를 보냅니다. |
| `Users` | 지정된 된 사용자와 관련 된 모든 연결에 메시지를 보냅니다. |

위 표의 각 메서드나 속성 반환을 가진 개체는 `SendAsync` 메서드. `SendAsync` 메서드 이름 및 클라이언트 메서드를 호출할 매개 변수를 제공할 수 있습니다.

## <a name="send-messages-to-clients"></a>클라이언트에 메시지 보내기

특정 클라이언트에 대 한 호출을 하려면 속성을 사용 하 여는 `Clients` 개체입니다. 다음 예제에서는 다음에는 `SendMessageToCaller` 메서드 허브 메서드를 호출 하는 연결으로 메시지를 보내는 방법을 보여 줍니다. `SendMessageToGroups` 메서드에 저장 된 그룹에 메시지를 보냅니다는 `List` 라는 `groups`합니다.

[!code-csharp[Send messages](hubs/sample/chathub.cs?range=15-24)]

## <a name="handle-events-for-a-connection"></a>연결에 대 한 이벤트를 처리 합니다.

SignalR 허브 API를 제공는 `OnConnectedAsync` 및 `OnDisconnectedAsync` 가상 메서드 관리 하 고 연결을 추적 합니다. 재정의 `OnConnectedAsync` 가상 메서드는 클라이언트 그룹에 추가 하는 방법과 같은 허브에 연결할 때 동작을 수행할 수 있습니다.

[!code-csharp[Handle events](hubs/sample/chathub.cs?range=26-30)]

## <a name="handle-errors"></a>오류 처리

허브 메서드에서 throw 된 예외는 메서드를 호출한 클라이언트에 전송 됩니다. JavaScript 클라이언트는 `invoke` 메서드가 반환 되는 [JavaScript 프로 미스](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Using_promises)합니다. 사용 하 여 프라미스에 연결 된 클라이언트의 오류 처리기를 받을 때 `catch`, 호출 개이고는 javascript에 전달 된 `Error` 개체입니다.

[!code-javascript[Error](hubs/sample/chat.js?range=20)]
[!code-javascript[Error](hubs/sample/chat.js?range=16-18)]

## <a name="related-resources"></a>관련 참고 자료

[ASP.NET Core SignalR 소개](xref:signalr/introduction)