---
title: SignalR에서 사용자 및 그룹 관리
author: tdykstra
description: ASP.NET Core SignalR의 사용자 및 그룹 관리에 대한 개요입니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 06/04/2018
uid: signalr/groups
ms.openlocfilehash: d3e580dfc42a36762358899892831c8b68f544b0
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50207162"
---
# <a name="manage-users-and-groups-in-signalr"></a><span data-ttu-id="7dc86-103">SignalR에서 사용자 및 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="7dc86-103">Manage users and groups in SignalR</span></span>

<span data-ttu-id="7dc86-104">작성자: [Brennan Conroy](https://github.com/BrennanConroy)</span><span class="sxs-lookup"><span data-stu-id="7dc86-104">By [Brennan Conroy](https://github.com/BrennanConroy)</span></span>

<span data-ttu-id="7dc86-105">SignalR을 사용하면 특정 사용자와 관련된 모든 연결뿐만 아니라 명명된 연결 그룹에 메시지를 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7dc86-105">SignalR allows messages to be sent to all connections associated with a specific user, as well as to named groups of connections.</span></span>

<span data-ttu-id="7dc86-106">[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/groups/sample/) [(다운로드 방법)](xref:index#how-to-download-a-sample)</span><span class="sxs-lookup"><span data-stu-id="7dc86-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/groups/sample/) [(how to download)](xref:index#how-to-download-a-sample)</span></span>

## <a name="users-in-signalr"></a><span data-ttu-id="7dc86-107">SignalR의 사용자</span><span class="sxs-lookup"><span data-stu-id="7dc86-107">Users in SignalR</span></span>

<span data-ttu-id="7dc86-108">SignalR을 사용하면 특정 사용자와 관련된 모든 연결에 메시지를 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7dc86-108">SignalR allows you to send messages to all connections associated with a specific user.</span></span> <span data-ttu-id="7dc86-109">SignalR은 기본적으로 연결과 관련된 `ClaimsPrincipal`의 `ClaimTypes.NameIdentifier`를 사용자 식별자로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7dc86-109">By default, SignalR uses the `ClaimTypes.NameIdentifier` from the `ClaimsPrincipal` associated with the connection as the user identifier.</span></span> <span data-ttu-id="7dc86-110">SignalR 앱에서 단일 사용자는 여러 개의 연결을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7dc86-110">A single user can have multiple connections to a SignalR app.</span></span> <span data-ttu-id="7dc86-111">예를 들어 사용자가 데스크톱은 물론 휴대폰에서도 연결했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7dc86-111">For example, a user could be connected on their desktop as well as their phone.</span></span> <span data-ttu-id="7dc86-112">각 장치마다 별도의 SignalR 연결을 갖지만, 이는 모두 동일한 사용자와 관련된 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="7dc86-112">Each device has a separate SignalR connection, but they're all associated with the same user.</span></span> <span data-ttu-id="7dc86-113">사용자에게 메시지가 전송되면 해당 사용자와 연관된 모든 연결에서 메시지를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="7dc86-113">If a message is sent to the user, all of the connections associated with that user receive the message.</span></span> <span data-ttu-id="7dc86-114">연결의 사용자 식별자는 허브의 `Context.UserIdentifier` 속성을 이용해서 접근할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7dc86-114">The user identifier for a connection can be accessed by the `Context.UserIdentifier` property in your hub.</span></span>

<span data-ttu-id="7dc86-115">다음 예제와 같이 허브 메서드에서 `User` 함수에 사용자 식별자를 전달해서 특정 사용자에게 메시지를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="7dc86-115">Send a message to a specific user by passing the user identifier to the `User` function in your hub method as shown in the following example:</span></span>

> [!NOTE]
> <span data-ttu-id="7dc86-116">사용자 식별자는 대소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="7dc86-116">The user identifier is case-sensitive.</span></span>

```csharp
public Task SendPrivateMessage(string user, string message)
{
    return Clients.User(user).SendAsync("ReceiveMessage", message);
}
```

<span data-ttu-id="7dc86-117">사용자 식별자는 `IUserIdProvider`를 생성한 다음, 이를 `ConfigureServices`에서 등록하여 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7dc86-117">The user identifier can be customized by creating an `IUserIdProvider`, and registering it in `ConfigureServices`.</span></span>

[!code-csharp[UserIdProvider](groups/sample/customuseridprovider.cs?range=4-10)]

[!code-csharp[Configure service](groups/sample/startup.cs?range=21-22,39-42)]

> [!NOTE]
> <span data-ttu-id="7dc86-118">사용자 지정 SignalR 서비스를 등록하기 전에 먼저 AddSignalR을 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7dc86-118">AddSignalR must be called before registering your custom SignalR services.</span></span>

## <a name="groups-in-signalr"></a><span data-ttu-id="7dc86-119">SignalR의 그룹</span><span class="sxs-lookup"><span data-stu-id="7dc86-119">Groups in SignalR</span></span>

<span data-ttu-id="7dc86-120">그룹은 이름이 연관된 연결들의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="7dc86-120">A group is a collection of connections associated with a name.</span></span> <span data-ttu-id="7dc86-121">그룹의 모든 연결에 메시지를 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7dc86-121">Messages can be sent to all connections in a group.</span></span> <span data-ttu-id="7dc86-122">그룹이 연결이나 다수의 연결에 전송하기에 적합한 방식인 이유는 그룹이 응용 프로그램에 의해 관리되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="7dc86-122">Groups are the recommended way to send to a connection or multiple connections because the groups are managed by the application.</span></span> <span data-ttu-id="7dc86-123">연결은 여러 그룹의 멤버일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7dc86-123">A connection can be a member of multiple groups.</span></span> <span data-ttu-id="7dc86-124">따라서 그룹은 각 방을 그룹으로 표현할 수 있는 채팅 같은 응용 프로그램에 이상적입니다.</span><span class="sxs-lookup"><span data-stu-id="7dc86-124">This makes groups ideal for something like a chat application, where each room can be represented as a group.</span></span> <span data-ttu-id="7dc86-125">`AddToGroupAsync` 및 `RemoveFromGroupAsync` 메서드를 통해서 연결을 그룹에 추가하거나 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7dc86-125">Connections can be added to or removed from groups via the `AddToGroupAsync` and `RemoveFromGroupAsync` methods.</span></span>

[!code-csharp[Hub methods](groups/sample/hubs/chathub.cs?range=15-27)]

<span data-ttu-id="7dc86-126">연결이 다시 연결되더라도 그룹의 멤버 자격은 유지되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7dc86-126">Group membership isn't preserved when a connection reconnects.</span></span> <span data-ttu-id="7dc86-127">연결이 다시 설정될 때 그룹에 다시 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7dc86-127">The connection needs to rejoin the group when it's re-established.</span></span> <span data-ttu-id="7dc86-128">응용 프로그램이 다수의 서버로 확장되는 경우 필요한 정보를 사용할 수 없기 때문에, 그룹의 구성원 수를 계산하는 것은 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="7dc86-128">It's not possible to count the members of a group, since this information is not available if the application is scaled to multiple servers.</span></span>

> [!NOTE]
> <span data-ttu-id="7dc86-129">그룹 이름은 대소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="7dc86-129">Group names are case-sensitive.</span></span>

## <a name="related-resources"></a><span data-ttu-id="7dc86-130">관련 자료</span><span class="sxs-lookup"><span data-stu-id="7dc86-130">Related resources</span></span>

* [<span data-ttu-id="7dc86-131">시작</span><span class="sxs-lookup"><span data-stu-id="7dc86-131">Get started</span></span>](xref:tutorials/signalr)
* [<span data-ttu-id="7dc86-132">허브</span><span class="sxs-lookup"><span data-stu-id="7dc86-132">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="7dc86-133">Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="7dc86-133">Publish to Azure</span></span>](xref:signalr/publish-to-azure-web-app)
