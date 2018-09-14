---
title: ASP.NET Core SignalR에서 허브를 사용 합니다.
author: tdykstra
description: ASP.NET Core SignalR에서 허브를 사용 하는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 09/12/2018
uid: signalr/hubs
ms.openlocfilehash: 17e3ee23967bc1097a3121b3e3e5b58cebe3887d
ms.sourcegitcommit: a742b55e4b8276a48b8b4394784554fecd883c84
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45538364"
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

## <a name="the-context-object"></a>컨텍스트 개체

합니다 `Hub` 클래스에는 `Context` 연결에 대 한 정보를 사용 하 여 다음 속성을 포함 하는 속성:

| 속성 | 설명 |
| ------ | ----------- |
| `ConnectionId` | SignalR에서 할당 된 연결에 대 한 고유 ID를 가져옵니다. 각 연결에 대 한 연결 ID를 하나 있습니다.|
| `UserIdentifier` | 가져옵니다 합니다 [사용자 식별자](xref:signalr/groups)합니다. SignalR 기본적으로 사용 합니다 `ClaimTypes.NameIdentifier` 에서 `ClaimsPrincipal` 사용자 식별자로 연결과 관련 된 합니다. |
| `User` | 가져옵니다는 `ClaimsPrincipal` 현재 사용자와 연결 합니다. |
| `Items` | 이 연결의 범위 내에서 데이터를 공유할 수 있는 키/값 컬렉션을 가져옵니다. 이 컬렉션의 데이터를 저장할 수 있습니다 하 고 연결에 대 한 다양 한 허브 메서드 호출 간에 유지 됩니다. |
| `Features` | 연결에서 사용할 수 있는 기능의 컬렉션을 가져옵니다. 지금은 자세히 아직 문서화 되지 않습니다 있도록이 컬렉션은 대부분의 시나리오에서 필요 하지 않습니다. |
| `ConnectionAborted` | 가져옵니다는 `CancellationToken` 연결이 중단 될 때를 알리는 합니다. |

`Hub.Context` 또한 다음 메서드를 포함 되어 있습니다.

| 메서드 | 설명 |
| ------ | ----------- |
| `GetHttpContext` | 반환 된 `HttpContext` 연결에 대해 또는 `null` 연결 HTTP 요청을 사용 하 여 연결 되지 않은 경우. HTTP 연결에 대 한 HTTP 헤더 및 쿼리 문자열과 같은 정보를 가져오려면이 메서드를 사용할 수 있습니다. |
| `Abort` | 연결을 중단합니다. |

## <a name="the-clients-object"></a>클라이언트 개체

합니다 `Hub` 클래스에는 `Clients` 서버와 클라이언트 간의 통신에 대 한 다음 속성을 포함 하는 속성:

| 속성 | 설명 |
| ------ | ----------- |
| `All` | 연결 된 모든 클라이언트에서 메서드를 호출합니다. |
| `Caller` | 허브 메서드를 호출 하는 클라이언트의 메서드를 호출 합니다. |
| `Others` | 메서드를 호출한 클라이언트를 제외한 모든 연결 된 클라이언트에서 메서드를 호출 합니다. |


`Hub.Clients` 또한 다음 메서드를 포함 되어 있습니다.

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

## <a name="strongly-typed-hubs"></a>강력한 형식의 허브

사용 하 여의 단점은 `SendAsync` 클라이언트 메서드 호출 수를 지정 하는 매직 문자열에는 사용 됩니다. 이 코드 open 메서드 이름의 철자가 잘못 되어 경우 런타임 오류 또는 클라이언트에서 누락 된 경우.

사용 하는 대신 `SendAsync` 강력 하 게 입력 하는 것은 `Hub` 사용 하 여 <xref:Microsoft.AspNetCore.SignalR.Hub`1>입니다. 다음 예제에서는 `ChatHub` 클라이언트 메서드 호출 하는 인터페이스에 확장 추출 된 `IChatClient`합니다.  

[!code-csharp[Interface for IChatClient](hubs/sample/hubs/ichatclient.cs?name=snippet_IChatClient)]

이 인터페이스는 위의 리팩터링 데 사용할 수 있습니다 `ChatHub` 예제입니다.

[!code-csharp[Strongly typed ChatHub](hubs/sample/hubs/StronglyTypedChatHub.cs?range=8-18,36)]

사용 하 여 `Hub<IChatClient>` 클라이언트 메서드의 컴파일 타임 검사를 사용 하도록 설정 합니다. 이후 매직 문자열을 사용 하 여 발생 하는 문제를 방지 하는이 `Hub<T>` 인터페이스에 메서드를 정의에 액세스할 수 있습니다.

사용 하 여 강력한 형식의 `Hub<T>` 사용 하는 기능을 사용 하지 않도록 설정 `SendAsync`합니다.

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
