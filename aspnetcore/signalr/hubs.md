---
title: ASP.NET Core SignalR에서 허브 사용하기
author: tdykstra
description: ASP.NET Core SignalR에서 허브를 사용하는 방법을 알아봅니다.
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
# <a name="use-hubs-in-signalr-for-aspnet-core"></a>ASP.NET Core SignalR에서 허브 사용하기

작성자: [Rachel Appel](https://twitter.com/rachelappel) 및 [Kevin Griffin](https://twitter.com/1kevgriff)

[샘플 코드 보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/hubs/sample/ ) [(다운로드 방법)](xref:tutorials/index#how-to-download-a-sample)

## <a name="what-is-a-signalr-hub"></a>SignalR 허브 기능

SignalR 허브 API를 사용하면 서버에서 연결된 클라이언트의 메서드를 호출할 수 있습니다. 서버 코드는 클라이언트에 의해서 호출되는 메서드를 정의합니다. 클라이언트 코드는 서버에 의해서 호출되는 메서드를 정의합니다. SignalR은 클라이언트에서 서버로 그리고 서버에서 클라이언트로 실시간 통신을 가능하게 만들어주는 모든 작업을 내부적으로 처리합니다.

## <a name="configure-signalr-hubs"></a>SignalR 허브 구성하기

SignalR 미들웨어에는 `services.AddSignalR` 호출을 통해 구성되는 몇 가지 서비스가 필요합니다.

[!code-csharp[Configure service](hubs/sample/startup.cs?range=38)]

ASP.NET Core 앱에 SignalR 기능을 추가할 때, `Startup.Configure` 메서드에서 `app.UseSignalR`을 호출하여 SignalR 경로를 설정합니다.

[!code-csharp[Configure routes to hubs](hubs/sample/startup.cs?range=57-60)]

## <a name="create-and-use-hubs"></a>허브 생성 및 사용하기

`Hub`를 상속받는 클래스를 선언하여 허브를 생성하고, 이 허브에 public 메서드를 추가합니다. 클라이언트는 이렇게 `public`으로 정의된 메서드를 호출할 수 있습니다.

[!code-csharp[Create and use hubs](hubs/sample/hubs/chathub.cs?range=8-37)]

일반적인 C# 메서드와 마찬가지로 복합 형식 및 배열 등을 사용해서 반환 형식과 매개 변수를 지정할 수 있습니다. SignalR은 매개 변수 및 반환 값에 사용되는 복합 개체 및 배열의 직렬화와 역직렬화를 처리합니다.

## <a name="the-context-object"></a>Context 개체

`Hub` 클래스에는 연결 정보와 함께 다음 속성들을 포함하고 있는 `Context` 속성이 존재합니다.

| 속성 | 설명 |
| ------ | ----------- |
| `ConnectionId` | SignalR에 의해 할당된 연결의 고유 ID를 가져옵니다. 각 연결마다 하나의 연결 ID가 존재합니다.|
| `UserIdentifier` | 가져옵니다 합니다 [사용자 식별자](xref:signalr/groups)를 가져옵니다. SignalR은 기본적으로 연결과 관련된 `ClaimTypes.NameIdentifier` 의 `ClaimsPrincipal` 을 가져옵니다. |
| `User` | 현재 사용자와 관련된 `ClaimsPrincipal` 현재 사용자와 연결 합니다. |
| `Items` | 연결의 범위 내에서 데이터 공유를 위해 사용할 수 있는 키/값 컬렉션을 가져옵니다. 이 컬렉션에 데이터를 저장할 수 있으며 저장된 데이터는 연결에 대한 다른 허브 메서드들의 호출 간에 유지됩니다. |
| `Features` | 연결에서 사용할 수 있는 기능들의 컬렉션을 가져옵니다. 이 컬렉션은 대부분의 시나리오에서 사용되지 않기 때문에, 지금은 아직 자세히 문서화되지 않았습니다. |
| `ConnectionAborted` | 연결이 중단될 때 이를 알려주는 `CancellationToken` 을 가져옵니다. |

`Hub.Context`는 다음 메서드도 포함하고 있습니다.

| 메서드 | 설명 |
| ------ | ----------- |
| `GetHttpContext` | 연결에 대한 `HttpContext`를 반환하거나, 연결이 HTTP 요청과 연관되지 않은 경우 `null`을 반환합니다. HTTP 연결에서 HTTP 헤더 및 쿼리 문자열 같은 정보를 가져오기 위해 이 메서드를 사용할 수 있습니다. |
| `Abort` | 연결을 중단합니다. |

## <a name="the-clients-object"></a>Clients 개체

`Hub` 클래스에는 서버와 클라이언트 간의 통신을 위한 다음 속성들을 포함하고 있는 `Clients` 속성이 존재합니다.

| 속성 | 설명 |
| ------ | ----------- |
| `All` | 연결된 모든 클라이언트에서 메서드를 호출합니다. |
| `Caller` | 해당 허브 메서드를 호출한 클라이언트에서 메서드를 호출합니다. |
| `Others` | 메서드를 호출한 클라이언트를 제외한 모든 연결된 클라이언트에서 메서드를 호출합니다. |


`Hub.Clients`는 다음 메서드도 포함하고 있습니다.

| 메서드 | 설명 |
| ------ | ----------- |
| `AllExcept` | 지정된 연결을 제외한 모든 연결된 클라이언트에서 메서드를 호출합니다. |
| `Client` | 연결된 특정 클라이언트에서 메서드를 호출합니다. |
| `Clients` | 연결된 특정 클라이언트들에서 메서드를 호출합니다. |
| `Group` | 지정된 그룹의 모든 연결에서 메서드를 호출합니다.  |
| `GroupExcept` | 지정된 연결을 제외한, 지정된 그룹의 모든 연결에서 메서드를 호출합니다. |
| `Groups` | 여러 그룹의 연결에서 메서드를 호출합니다.  |
| `OthersInGroup` | 허브 메서드를 호출한 클라이언트를 제외하고 연결 그룹에서 메서드를 호출합니다.  |
| `User` | 특정 사용자와 관련된 모든 연결에서 메서드를 호출합니다. |
| `Users` | 지정한 사용자들과 관련된 모든 연결에서 메서드를 호출합니다. |

앞의 표에 설명된 각 속성 및 메서드는 `SendAsync` 메서드를 통해서 개체를 반환합니다. `SendAsync` 메서드를 사용해서 호출할 클라이언트 메서드의 이름 및 매개 변수를 제공할 수 있습니다.

## <a name="send-messages-to-clients"></a>클라이언트에 메시지 전송하기

특정 클라이언트를 대상으로 호출하려면 `Clients` 개체의 속성을 사용합니다. 다음 예제에서 `SendMessageToCaller` 메서드는 허브 메서드를 호출한 연결에 메시지를 전송하는 방법을 보여줍니다. `SendMessageToGroups` 메서드는 `groups`라는 이름의 `List`에 저장된 그룹에 메시지를 전송합니다.

[!code-csharp[Send messages](hubs/sample/hubs/chathub.cs?range=15-24)]

## <a name="strongly-typed-hubs"></a>강력한 형식의 허브

`SendAsync` 방식의 단점은 호출된 클라이언트 메서드를 지정하기 위해 매직 문자열에 의존한다는 것입니다. 이로 인해 메서드 이름의 철자가 잘못되거나 클라이언트에서 누락된 경우 런타임 오류가 발생합니다.

`SendAsync` 방식의 대안은 <xref:Microsoft.AspNetCore.SignalR.Hub`1>를 이용한 강력한 형식의 `Hub`를 사용하는 것입니다. 다음 예제에서 `ChatHub` 클라이언트 메서드들은 `IChatClient`라는 인터페이스로 추출됩니다.  

[!code-csharp[Interface for IChatClient](hubs/sample/hubs/ichatclient.cs?name=snippet_IChatClient)]

이 인터페이스를 사용해서 기존의 `ChatHub` 예제를 리팩터링할 수 있습니다.

[!code-csharp[Strongly typed ChatHub](hubs/sample/hubs/StronglyTypedChatHub.cs?range=8-18,36)]

`Hub<IChatClient>`를 사용하면 클라이언트 메서드를 컴파일 시점에 검사할 수 있습니다. 이렇게 하면 `Hub<T>` 인터페이스에 정의된 메서드만 접근할 수 있기 때문에 마법 문자열 사용으로 인한 문제를 방지할 수 있습니다.

강력한 형식의 `Hub<T>`를 사용하면 `SendAsync`를 사용할 수 없습니다.

## <a name="handle-events-for-a-connection"></a>연결에 관한 이벤트 처리하기

SignalR 허브 API는 연결을 관리하고 추적하기 위한 `OnConnectedAsync` 및 `OnDisconnectedAsync` 가상 메서드를 제공합니다. 클라이언트가 허브에 연결할 때, 클라이언트를 그룹에 추가하는 등과 같은 작업을 수행하려면 `OnConnectedAsync` 가상 메서드를 재정의합니다.

[!code-csharp[Handle events](hubs/sample/hubs/chathub.cs?range=26-36)]

## <a name="handle-errors"></a>오류 처리

허브 메서드에서 발생(throw)된 예외는 메서드를 호출한 클라이언트로 전송됩니다. JavaScript 클라이언트에서 `invoke` 메서드는 [JavaScript Promise](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Using_promises)를 반환합니다. 클라이언트가 `catch`를 통해서 Promise에 첨부된 처리기로 오류를 수신하면, 오류가 JavaScript `Error` 개체로 전달되어 호출됩니다.

[!code-javascript[Error](hubs/sample/wwwroot/js/chat.js?range=23)]

## <a name="related-resources"></a>관련 자료

* [ASP.NET Core SignalR 소개](xref:signalr/introduction)
* [JavaScript 클라이언트](xref:signalr/javascript-client)
* [Azure에 게시하기](xref:signalr/publish-to-azure-web-app)
