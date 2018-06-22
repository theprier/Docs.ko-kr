---
title: SignalR의 사용자 및 그룹 관리
author: rachelappel
description: ASP.NET Core SignalR 사용자 및 그룹 관리의 개요입니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 06/04/2018
uid: signalr/groups
ms.openlocfilehash: f7d60a906fc238f79c76fd2a4ee693417a348825
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36272083"
---
# <a name="manage-users-and-groups-in-signalr"></a>SignalR의 사용자 및 그룹 관리

으로 [브 레 넌 Conroy](https://github.com/BrennanConroy)

SignalR 메시지를 특정 사용자와 관련 된 모든 연결에 보내도록 뿐만 아니라 명명 된 그룹의 연결을 허용 합니다.

[보거나 다운로드 샘플 코드](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/groups/sample/) [(다운로드 하는 방법)](xref:tutorials/index#how-to-download-a-sample)

## <a name="users-in-signalr"></a>SignalR의 사용자

SignalR을 사용 하면 특정 사용자와 관련 된 모든 연결에 메시지를 보낼 수 있습니다. SignalR 기본적으로 사용 하 여는 `ClaimTypes.NameIdentifier` 에서 `ClaimsPrincipal` 연결 된 사용자 식별자로 연결 합니다. 사용자 한 명이 SignalR 응용 프로그램에 여러 연결이 있을 수 있습니다. 예를 들어는 사용자는 전화 번호 뿐 아니라 데스크톱에 연결 될 수 없습니다. 각 장치에 별도 SignalR 연결에 있지만 동일한 사용자와 연결 된 모든입니다. 사용자에 게 메시지를 보내면 메시지를 수신할 모든 사용자와 관련 된 연결입니다.

사용자 식별자를 전달 하 여 특정 사용자에 게 메시지를 보낼는 `User` 다음 예제와 같이 허브 메서드의 작동 합니다.

> [!NOTE]
> 사용자 id는 대/소문자 구분 합니다.

```csharp
public Task SendPrivateMessage(string user, string message)
{
    return Clients.User(user).SendAsync("ReceiveMessage", message);
}
```

사용자의 id를 만들어 사용자 지정할 수는 `IUserIdProvider`, 및에서 등록 `ConfigureServices`합니다.

[!code-csharp[UserIdProvider](groups/sample/customuseridprovider.cs?range=4-10)]

[!code-csharp[Configure service](groups/sample/startup.cs?range=21-22,39-42)]

> [!NOTE]
> AddSignalR은 사용자 지정 SignalR 서비스에 등록 하기 전에 호출 되어야 합니다.

## <a name="groups-in-signalr"></a>SignalR의 그룹

그룹은 이름에 연결 된 연결의 컬렉션입니다. 그룹의 모든 연결에 메시지를 보낼 수 있습니다. 그룹은 그룹 응용 프로그램에 의해 관리 되므로 연결 또는 여러 연결에 전송 하는 것이 좋습니다. 연결을 여러 그룹의 구성원이 될 수 있습니다. 따라서 그룹 이상적인 다음과 같이 채팅 응용 프로그램에 대 한 각 방의 그룹으로 나타낼 수 있는 합니다. 연결에 추가 하거나을 통해 그룹에서 제거할 수는 `AddToGroupAsync` 및 `RemoveFromGroupAsync` 메서드.

[!code-csharp[Hub methods](groups/sample/hubs/chathub.cs?range=15-27)]

연결이 다시 연결 하는 경우 그룹 구성원 자격 유지 되지 않습니다. 연결 다시 설정 될 때 그룹을 다시 조인 해야 합니다. 이 정보를 여러 서버에 응용 프로그램의 크기가 조정 되는 경우에 사용할 수 없기 때문에 그룹의 구성원을 계산 하는 것이 불가능 합니다.

> [!NOTE]
> 그룹 이름은 대/소문자를 구분 하지 않습니다.

## <a name="related-resources"></a>관련 참고 자료

* [시작](xref:tutorials/signalr)
* [허브](xref:signalr/hubs)
* [Azure에 게시](xref:signalr/publish-to-azure-web-app)
