---
title: SignalR의 사용자 및 그룹 관리
author: rachelappel
description: ASP.NET Core SignalR 사용자 및 그룹 관리의 개요입니다.
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 06/04/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: signalr/groups
ms.openlocfilehash: 2a2f129863cf7d5cdfa3c0e5b2d901af52144671
ms.sourcegitcommit: 7e87671fea9a5f36ca516616fe3b40b537f428d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35358452"
---
# <a name="manage-users-and-groups-in-signalr"></a><span data-ttu-id="f5933-103">SignalR의 사용자 및 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="f5933-103">Manage users and groups in SignalR</span></span>

<span data-ttu-id="f5933-104">으로 [브 레 넌 Conroy](https://github.com/BrennanConroy)</span><span class="sxs-lookup"><span data-stu-id="f5933-104">By [Brennan Conroy](https://github.com/BrennanConroy)</span></span>

<span data-ttu-id="f5933-105">SignalR 메시지를 특정 사용자와 관련 된 모든 연결에 보내도록 뿐만 아니라 명명 된 그룹의 연결을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5933-105">SignalR allows messages to be sent to all connections associated with a specific user, as well as to named groups of connections.</span></span>

<span data-ttu-id="f5933-106">[보거나 다운로드 샘플 코드](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/groups/sample/) [(다운로드 하는 방법)](xref:tutorials/index#how-to-download-a-sample)</span><span class="sxs-lookup"><span data-stu-id="f5933-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/groups/sample/) [(how to download)](xref:tutorials/index#how-to-download-a-sample)</span></span>

## <a name="users-in-signalr"></a><span data-ttu-id="f5933-107">SignalR의 사용자</span><span class="sxs-lookup"><span data-stu-id="f5933-107">Users in SignalR</span></span>

<span data-ttu-id="f5933-108">SignalR을 사용 하면 특정 사용자와 관련 된 모든 연결에 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5933-108">SignalR allows you to send messages to all connections associated with a specific user.</span></span> <span data-ttu-id="f5933-109">SignalR 기본적으로 사용 하 여는 `ClaimTypes.NameIdentifier` 에서 `ClaimsPrincipal` 연결 된 사용자 식별자로 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5933-109">By default SignalR uses the `ClaimTypes.NameIdentifier` from the `ClaimsPrincipal` associated with the connection as the user identifier.</span></span> <span data-ttu-id="f5933-110">사용자 한 명이 SignalR 응용 프로그램에 여러 연결이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5933-110">A single user can have multiple connections to a SignalR application.</span></span> <span data-ttu-id="f5933-111">예를 들어는 사용자는 전화 번호 뿐 아니라 데스크톱에 연결 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f5933-111">For example, a user could be connected on their desktop as well as their phone.</span></span> <span data-ttu-id="f5933-112">각 장치에 별도 SignalR 연결에 있지만 동일한 사용자와 연결 된 모든입니다.</span><span class="sxs-lookup"><span data-stu-id="f5933-112">Each device has a separate SignalR connection, but they are all associated with the same user.</span></span> <span data-ttu-id="f5933-113">사용자에 게 메시지를 보내면 메시지를 수신할 모든 사용자와 관련 된 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="f5933-113">If a message is sent to the user, all of the connections associated with that user will receive the message.</span></span>

<span data-ttu-id="f5933-114">사용자 식별자를 전달 하 여 특정 사용자에 게 메시지를 보낼는 `User` 다음 예제와 같이 허브 메서드의 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5933-114">Send a message to a specific user by passing the user identifier to the `User` function in your hub method as shown in the following example:</span></span>

> [!NOTE]
> <span data-ttu-id="f5933-115">사용자 id는 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5933-115">The user identifier is case-sensitive.</span></span>

```csharp
public Task SendPrivateMessage(string user, string message)
{
    return Clients.User(user).SendAsync("ReceiveMessage", message);
}
```

<span data-ttu-id="f5933-116">사용자의 id를 만들어 사용자 지정할 수는 `IUserIdProvider`, 및에서 등록 `ConfigureServices`합니다.</span><span class="sxs-lookup"><span data-stu-id="f5933-116">The user identifier can be customized by creating an `IUserIdProvider`, and registering it in `ConfigureServices`.</span></span>

[!code-csharp[UserIdProvider](groups/sample/customuseridprovider.cs?range=4-10)]

[!code-csharp[Configure service](groups/sample/startup.cs?range=21-22,39-42)]

> [!NOTE]
> <span data-ttu-id="f5933-117">AddSignalR은 사용자 지정 SignalR 서비스에 등록 하기 전에 호출 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5933-117">AddSignalR must be called before registering your custom SignalR services.</span></span>

## <a name="groups-in-signalr"></a><span data-ttu-id="f5933-118">SignalR의 그룹</span><span class="sxs-lookup"><span data-stu-id="f5933-118">Groups in SignalR</span></span>

<span data-ttu-id="f5933-119">그룹은 이름에 연결 된 연결의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="f5933-119">A group is a collection of connections associated with a name.</span></span> <span data-ttu-id="f5933-120">그룹의 모든 연결에 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5933-120">Messages can be sent to all connections in a group.</span></span> <span data-ttu-id="f5933-121">그룹은 그룹 응용 프로그램에 의해 관리 되므로 연결 또는 여러 연결에 전송 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f5933-121">Groups are the recommended way to send to a connection or multiple connections because the groups are managed by the application.</span></span> <span data-ttu-id="f5933-122">연결을 여러 그룹의 구성원이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5933-122">A connection can be a member of multiple groups.</span></span> <span data-ttu-id="f5933-123">따라서 그룹 이상적인 다음과 같이 채팅 응용 프로그램에 대 한 각 방의 그룹으로 나타낼 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5933-123">This makes groups ideal for something like a chat application, where each room can be represented as a group.</span></span> <span data-ttu-id="f5933-124">연결에 추가 하거나을 통해 그룹에서 제거할 수는 `AddToGroupAsync` 및 `RemoveFromGroupAsync` 메서드.</span><span class="sxs-lookup"><span data-stu-id="f5933-124">Connections can be added to or removed from groups via the `AddToGroupAsync` and `RemoveFromGroupAsync` methods.</span></span>

[!code-csharp[Hub methods](groups/sample/hubs/chathub.cs?range=15-27)]

<span data-ttu-id="f5933-125">연결이 다시 연결 하는 경우 그룹 구성원 자격 유지 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f5933-125">Group membership isn't preserved when a connection reconnects.</span></span> <span data-ttu-id="f5933-126">연결 다시 설정 될 때 그룹을 다시 조인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5933-126">The connection needs to rejoin the group when it's re-established.</span></span> <span data-ttu-id="f5933-127">이 정보를 여러 서버에 응용 프로그램의 크기가 조정 되는 경우에 사용할 수 없기 때문에 그룹의 구성원을 계산 하는 것이 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5933-127">It's not possible to count the members of a group, since this information is not available if the application is scaled to multiple servers.</span></span>

> [!NOTE]
> <span data-ttu-id="f5933-128">그룹 이름은 대/소문자를 구분 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f5933-128">Group names are case-sensitive.</span></span>

## <a name="related-resources"></a><span data-ttu-id="f5933-129">관련 참고 자료</span><span class="sxs-lookup"><span data-stu-id="f5933-129">Related resources</span></span>

* [<span data-ttu-id="f5933-130">시작</span><span class="sxs-lookup"><span data-stu-id="f5933-130">Get started</span></span>](xref:signalr/get-started)
* [<span data-ttu-id="f5933-131">허브</span><span class="sxs-lookup"><span data-stu-id="f5933-131">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="f5933-132">Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="f5933-132">Publish to Azure</span></span>](xref:signalr/publish-to-azure-web-app)
