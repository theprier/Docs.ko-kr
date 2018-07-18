---
title: ASP.NET Core SignalR에서 허브를 사용 합니다.
author: tdykstra
description: ASP.NET Core SignalR에서 허브를 사용 하는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 05/01/2018
uid: signalr/hubs
ms.openlocfilehash: be39666373e2b099054bb71f4a7fcf17aeb9a01c
ms.sourcegitcommit: 3ca527f27c88cfc9d04688db5499e372fbc2c775
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39095283"
---
# <a name="use-hubs-in-signalr-for-aspnet-core"></a>SignalR에서 허브를 사용 하 여 ASP.NET Core에 대 한

하 여 [Rachel Appel](https://twitter.com/rachelappel) 고 [Kevin Griffin](https://twitter.com/1kevgriff)

[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/hubs/sample/ ) [(다운로드 하는 방법)](xref:tutorials/index#how-to-download-a-sample)

## <a name="what-is-a-signalr-hub"></a>SignalR 허브 란

SignalR 허브 API를 사용 하면 서버에서 연결 된 클라이언트에서 메서드를 호출할 수 있습니다. 서버 코드를 클라이언트에서 호출 된 메서드를 정의 합니다. 클라이언트 코드를 서버에서 호출 된 메서드를 정의 합니다. SignalR은 클라이언트와 서버 간 및 서버와 클라이언트 간 실시간 통신을 가능 하 게 하는 백그라운드에서 모든 부분을 처리 합니다.

## <a name="configure-signalr-hubs"></a>SignalR 허브를 구성 합니다.

SignalR 미들웨어를 호출 하 여 구성 된 일부 서비스의 경우 필요한 `services.AddSignalR`합니다.

[!code-csharp[Configure service](hubs/sample/startup.cs?range=38)]

ASP.NET Core 앱에 SignalR 기능을 추가 하는 경우 호출 하 여 SignalR 경로 설정 `app.UseSignalR` 에 `Startup.Configure` 메서드.

[!code-csharp[Configure routes to hubs](hubs/sample/startup.cs?range=57-60)]

## <a name="create-and-use-hubs"></a>만들고 허브를 사용 합니다.

상속 되는 클래스를 선언 하 여 허브를 만들 `Hub`, public 메서드를 추가 합니다. 클라이언트도 정의 된 메서드를 호출할 수 `public`입니다.

[!code-csharp[Create and use hubs](hubs/sample/hubs/chathub.cs?range=8-37)]

반환 형식 및 C# 메서드에서 마찬가지로 복합 형식 및 배열 등 매개 변수를 지정할 수 있습니다. SignalR은 serialization 및 deserialization 복잡 한 개체 및 배열 매개 변수 및 반환 값을 처리합니다.

## <a name="the-clients-object"></a>클라이언트 개체

각 인스턴스는 `Hub` 클래스 라는 속성이 `Clients` 서버와 클라이언트 간의 통신에 대 한 다음 멤버를 포함 하는:

| 속성 | 설명 |
| ------ | ----------- |
| `All` | 연결 된 모든 클라이언트에서 메서드를 호출합니다. |
| `Caller` | 허브 메서드를 호출 하는 클라이언트의 메서드를 호출 합니다. |
| `Others` | 메서드를 호출한 클라이언트를 제외한 모든 연결 된 클라이언트에서 메서드를 호출 합니다. |


또한 `Hub.Clients` 다음 메서드를 포함 합니다.

| 메서드 | 설명 |
| ------ | ----------- |
| `AllExcept` | 지정 된 연결을 제외 하 고 연결 된 모든 클라이언트에서 메서드를 호출합니다. |
| `Client` | 특정 연결 된 클라이언트에서 메서드를 호출합니다. |
| `Clients` | 특정 연결 된 클라이언트에서 메서드를 호출합니다. |
| `Group` | 지정된 된 그룹의 모든 연결에 메서드를 호출합니다.  |
| `GroupExcept` | 지정된 된 연결을 제외 하 고 지정된 된 그룹의 모든 연결에 메서드를 호출합니다. |
| `Groups` | 연결의 여러 그룹에 메서드를 호출  |
| `OthersInGroup` | 허브 메서드를 호출 하는 클라이언트를 제외한 연결 그룹에 메서드를 호출  |
| `User` | 특정 사용자와 관련 된 모든 연결 하는 메서드를 호출 합니다. |
| `Users` | 지정된 된 사용자와 관련 된 모든 연결 하는 메서드를 호출 합니다. |

앞의 표에 각 메서드나 속성 개체를 반환을 `SendAsync` 메서드. `SendAsync` 메서드를 사용 하면 이름 및 클라이언트 메서드 호출의 매개 변수를 제공할 수 있습니다.

## <a name="send-messages-to-clients"></a>클라이언트에 메시지 보내기

특정 클라이언트에 대 한 호출을 하려면 속성을 사용 합니다 `Clients` 개체입니다. 다음 예제에서는 `SendMessageToCaller` 메서드 허브 메서드 호출 연결에 메시지를 보내는 방법을 보여 줍니다. 합니다 `SendMessageToGroups` 메서드에 저장 된 그룹에 메시지를 보냅니다는 `List` 라는 `groups`합니다.

[!code-csharp[Send messages](hubs/sample/hubs/chathub.cs?range=15-24)]

## <a name="handle-events-for-a-connection"></a>연결에 대 한 이벤트를 처리 합니다.

SignalR 허브 API를 제공 합니다 `OnConnectedAsync` 및 `OnDisconnectedAsync` 가상 메서드를 관리 하 고 연결을 추적 합니다. 재정의 `OnConnectedAsync` 가상 메서드는 클라이언트 그룹에 추가 하는 등 허브에 연결 시 작업을 수행 합니다.

[!code-csharp[Handle events](hubs/sample/hubs/chathub.cs?range=26-36)]

## <a name="handle-errors"></a>오류 처리

허브 메서드에서 throw 된 예외는 메서드를 호출한 클라이언트에 전송 됩니다. JavaScript 클라이언트에는 `invoke` 메서드가 반환 되는 [JavaScript 프라미스](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Using_promises)합니다. 프라미스를 통해 연결 된 클라이언트의 오류 처리기를 받을 때 `catch`, 호출 되 고 javascript 전달 `Error` 개체입니다.

[!code-javascript[Error](hubs/sample/wwwroot/js/chat.js?range=23)]

## <a name="related-resources"></a>관련 참고 자료

* [ASP.NET Core SignalR에 대 한 소개](xref:signalr/introduction)
* [JavaScript 클라이언트](xref:signalr/javascript-client)
* [Azure에 게시](xref:signalr/publish-to-azure-web-app)
