---
title: SignalR에서 사용자 및 그룹 관리
author: tdykstra
description: ASP.NET Core SignalR 사용자 및 그룹 관리의 개요입니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 06/04/2018
uid: signalr/groups
ms.openlocfilehash: d54ab2a113345f98e26425a88cad165d67b8d456
ms.sourcegitcommit: 3ca527f27c88cfc9d04688db5499e372fbc2c775
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39095023"
---
# <a name="manage-users-and-groups-in-signalr"></a><span data-ttu-id="d531f-103">SignalR에서 사용자 및 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="d531f-103">Manage users and groups in SignalR</span></span>

<span data-ttu-id="d531f-104">[브 레 넌 Conroy](https://github.com/BrennanConroy)</span><span class="sxs-lookup"><span data-stu-id="d531f-104">By [Brennan Conroy](https://github.com/BrennanConroy)</span></span>

<span data-ttu-id="d531f-105">SignalR 메시지를 특정 사용자와 연결 된 모든 연결에 보낼 뿐만 아니라 명명 된 연결 그룹에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d531f-105">SignalR allows messages to be sent to all connections associated with a specific user, as well as to named groups of connections.</span></span>

<span data-ttu-id="d531f-106">[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/groups/sample/) [(다운로드 하는 방법)](xref:tutorials/index#how-to-download-a-sample)</span><span class="sxs-lookup"><span data-stu-id="d531f-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/groups/sample/) [(how to download)](xref:tutorials/index#how-to-download-a-sample)</span></span>

## <a name="users-in-signalr"></a><span data-ttu-id="d531f-107">SignalR에 대 한 사용자</span><span class="sxs-lookup"><span data-stu-id="d531f-107">Users in SignalR</span></span>

<span data-ttu-id="d531f-108">SignalR을 사용 하면 특정 사용자와 관련 된 모든 연결에 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d531f-108">SignalR allows you to send messages to all connections associated with a specific user.</span></span> <span data-ttu-id="d531f-109">SignalR 기본적으로 사용 합니다 `ClaimTypes.NameIdentifier` 에서 `ClaimsPrincipal` 사용자 식별자로 연결과 관련 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="d531f-109">By default, SignalR uses the `ClaimTypes.NameIdentifier` from the `ClaimsPrincipal` associated with the connection as the user identifier.</span></span> <span data-ttu-id="d531f-110">단일 사용자 SignalR 앱에 여러 연결이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d531f-110">A single user can have multiple connections to a SignalR app.</span></span> <span data-ttu-id="d531f-111">예를 들어 휴대폰 뿐만 아니라 데스크톱에 사용자를 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d531f-111">For example, a user could be connected on their desktop as well as their phone.</span></span> <span data-ttu-id="d531f-112">각 장치에 별도 SignalR 연결을 있지만 모두 동일한 사용자와 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="d531f-112">Each device has a separate SignalR connection, but they're all associated with the same user.</span></span> <span data-ttu-id="d531f-113">사용자에 게 메시지를 보내면 해당 사용자와 연결 된 연결의 모든 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="d531f-113">If a message is sent to the user, all of the connections associated with that user receive the message.</span></span> <span data-ttu-id="d531f-114">연결에 대 한 사용자 식별자에서 액세스할 수는 `Context.UserIdentifier` 허브의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d531f-114">The user identifier for a connection can be accessed by the `Context.UserIdentifier` property in your hub.</span></span>

<span data-ttu-id="d531f-115">사용자 식별자를 전달 하 여 특정 사용자에 게 메시지를 보내기는 `User` 다음 예제에서와 같이 허브 메서드에서 함수:</span><span class="sxs-lookup"><span data-stu-id="d531f-115">Send a message to a specific user by passing the user identifier to the `User` function in your hub method as shown in the following example:</span></span>

> [!NOTE]
> <span data-ttu-id="d531f-116">사용자 id는 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="d531f-116">The user identifier is case-sensitive.</span></span>

```csharp
public Task SendPrivateMessage(string user, string message)
{
    return Clients.User(user).SendAsync("ReceiveMessage", message);
}
```

<span data-ttu-id="d531f-117">사용자 id를 만들어 사용자 지정할 수 있습니다는 `IUserIdProvider`, 및에서 등록 `ConfigureServices`합니다.</span><span class="sxs-lookup"><span data-stu-id="d531f-117">The user identifier can be customized by creating an `IUserIdProvider`, and registering it in `ConfigureServices`.</span></span>

[!code-csharp[UserIdProvider](groups/sample/customuseridprovider.cs?range=4-10)]

[!code-csharp[Configure service](groups/sample/startup.cs?range=21-22,39-42)]

> [!NOTE]
> <span data-ttu-id="d531f-118">AddSignalR은 사용자 지정 SignalR 서비스를 등록 하기 전에 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d531f-118">AddSignalR must be called before registering your custom SignalR services.</span></span>

## <a name="groups-in-signalr"></a><span data-ttu-id="d531f-119">SignalR에서 그룹</span><span class="sxs-lookup"><span data-stu-id="d531f-119">Groups in SignalR</span></span>

<span data-ttu-id="d531f-120">그룹 이름과 관련 된 연결의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="d531f-120">A group is a collection of connections associated with a name.</span></span> <span data-ttu-id="d531f-121">그룹의 모든 연결에 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d531f-121">Messages can be sent to all connections in a group.</span></span> <span data-ttu-id="d531f-122">그룹은 그룹 응용 프로그램에 의해 관리 되기 때문에 하나 이상의 여러 연결이 보내기에 대 한 권장된 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d531f-122">Groups are the recommended way to send to a connection or multiple connections because the groups are managed by the application.</span></span> <span data-ttu-id="d531f-123">연결을 여러 그룹의 멤버일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d531f-123">A connection can be a member of multiple groups.</span></span> <span data-ttu-id="d531f-124">따라서 그룹 적합 한 채팅 응용 프로그램을 같은 그룹으로 각 룸을 나타낼 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d531f-124">This makes groups ideal for something like a chat application, where each room can be represented as a group.</span></span> <span data-ttu-id="d531f-125">연결 수에 추가 되거나를 통해 그룹에서 제거 합니다 `AddToGroupAsync` 고 `RemoveFromGroupAsync` 메서드.</span><span class="sxs-lookup"><span data-stu-id="d531f-125">Connections can be added to or removed from groups via the `AddToGroupAsync` and `RemoveFromGroupAsync` methods.</span></span>

[!code-csharp[Hub methods](groups/sample/hubs/chathub.cs?range=15-27)]

<span data-ttu-id="d531f-126">그룹 멤버 자격에는 연결을 다시 연결 될 때 유지 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d531f-126">Group membership isn't preserved when a connection reconnects.</span></span> <span data-ttu-id="d531f-127">연결을 다시 설정할 때 그룹을 다시 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d531f-127">The connection needs to rejoin the group when it's re-established.</span></span> <span data-ttu-id="d531f-128">이 정보를 여러 서버를 사용 하는 응용 프로그램에서 크기를 조정 하는 경우에 사용할 수 없기 때문에 그룹의 구성원을 계산 하는 것이 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="d531f-128">It's not possible to count the members of a group, since this information is not available if the application is scaled to multiple servers.</span></span>

> [!NOTE]
> <span data-ttu-id="d531f-129">그룹 이름은 대/소문자를 구분 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d531f-129">Group names are case-sensitive.</span></span>

## <a name="related-resources"></a><span data-ttu-id="d531f-130">관련 참고 자료</span><span class="sxs-lookup"><span data-stu-id="d531f-130">Related resources</span></span>

* [<span data-ttu-id="d531f-131">시작</span><span class="sxs-lookup"><span data-stu-id="d531f-131">Get started</span></span>](xref:tutorials/signalr)
* [<span data-ttu-id="d531f-132">허브</span><span class="sxs-lookup"><span data-stu-id="d531f-132">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="d531f-133">Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="d531f-133">Publish to Azure</span></span>](xref:signalr/publish-to-azure-web-app)
