---
uid: signalr/overview/older-versions/working-with-groups
title: "SignalR에서 그룹 작업 1.x | Microsoft Docs"
author: pfletcher
description: "이 항목에서는 허브 API 사용 하 여 그룹 멤버 자격 정보를 유지 하는 방법을 설명 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/21/2013
ms.topic: article
ms.assetid: 22929efd-68c9-4609-b76d-f8ba42fda01e
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/older-versions/working-with-groups
msc.type: authoredcontent
ms.openlocfilehash: 7bc0ff73ade72729cc5e1217b3fe704ac0d8cab8
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="working-with-groups-in-signalr-1x"></a><span data-ttu-id="608fb-103">SignalR에서 그룹 작업 1.x</span><span class="sxs-lookup"><span data-stu-id="608fb-103">Working with Groups in SignalR 1.x</span></span>
====================
<span data-ttu-id="608fb-104">여 [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="608fb-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="608fb-105">이 항목에서는 사용자 그룹에 추가 하 고 그룹 구성원 자격 정보를 유지 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-105">This topic describes how to add users to groups and persist group membership information.</span></span>


## <a name="overview"></a><span data-ttu-id="608fb-106">개요</span><span class="sxs-lookup"><span data-stu-id="608fb-106">Overview</span></span>

<span data-ttu-id="608fb-107">SignalR에서 그룹 연결 된 클라이언트의 지정 된 하위 집합에 메시지 브로드캐스트에 대 한 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-107">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="608fb-108">그룹의 클라이언트, 모든 수 있고 클라이언트가 여러 그룹의 멤버일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-108">A group can have any number of clients, and a client can be a member of any number of groups.</span></span> <span data-ttu-id="608fb-109">명시적으로 그룹을 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-109">You don't have to explicitly create groups.</span></span> <span data-ttu-id="608fb-110">실제로 그룹이 자동으로 Groups.Add에 대 한 호출에 해당 이름을 지정 하는 처음으로 만들어지고 것의 멤버 자격에서 마지막 연결을 제거할 때 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-110">In effect, a group is automatically created the first time you specify its name in a call to Groups.Add, and it is deleted when you remove the last connection from membership in it.</span></span> <span data-ttu-id="608fb-111">그룹을 사용 하는 방법을 알려면 [허브 클래스에서 그룹 구성원 자격을 관리 하는 방법](index.md) 허브 api-서버 가이드입니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-111">For an introduction to using groups, see [How to manage group membership from the Hub class](index.md) in the Hubs API - Server Guide.</span></span>

<span data-ttu-id="608fb-112">그룹 멤버 자격 목록 또는 그룹 목록을 가져오는 데 필요한 API는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-112">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="608fb-113">SignalR 클라이언트 및 pub/sub 모델을 기반으로 하는 그룹 메시지 보내고 서버 그룹 또는 그룹 멤버 자격 목록이 유지 관리 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-113">SignalR sends messages to clients and groups based on a pub/sub model, and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="608fb-114">이렇게 하면 확장성을 최대화 웹 팜에 노드를 추가할 때마다 SignalR 유지 하는 모든 상태 하기 때문에 새 노드를 전파할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-114">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<span data-ttu-id="608fb-115">사용 하 여 그룹에 사용자를 추가 하면는 `Groups.Add` 메서드를 사용자에 대 한 현재 연결 기간 동안 해당 그룹에 연결 하는 메시지를 수신 하지만 해당 그룹의 멤버 자격 사용자의 현재 연결 끝나면 지속 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-115">When you add a user to a group using the `Groups.Add` method, the user receives messages directed to that group for the duration of the current connection, but the user's membership in that group is not persisted beyond the current connection.</span></span> <span data-ttu-id="608fb-116">그룹과 그룹 멤버 자격에 대 한 정보를 영구적으로 유지 하려는 경우에 데이터베이스 또는 Azure 테이블 저장소와 같은 저장소에 해당 데이터를 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-116">If you want to permanently retain information about groups and group membership, you must store that data in a repository such as a database or Azure table storage.</span></span> <span data-ttu-id="608fb-117">그런 다음 사용자가 응용 프로그램에 연결 될 때마다 사용자가 속한 그룹 저장소에서 검색 했으며 해당 그룹에 해당 사용자를 수동으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-117">Then, each time a user connects to your application, you retrieve from the repository which groups the user belongs to, and manually add that user to those groups.</span></span>

<span data-ttu-id="608fb-118">임시 중단 후에 다시 연결할 때 사용자 자동으로 다시 조인 이전에 할당 된 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-118">When reconnecting after a temporary disruption, the user automatically re-joins the previously-assigned groups.</span></span> <span data-ttu-id="608fb-119">다시 연결 될 때, 새 연결을 설정할 때가 아니라 적용만 자동으로 그룹에 다시 참여 합니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-119">Automatically rejoining a group only applies when reconnecting, not when establishing a new connection.</span></span> <span data-ttu-id="608fb-120">디지털 서명 된 토큰은 이전에 할당 된 그룹의 목록을 포함 하는 클라이언트에서 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-120">A digitally-signed token is passed from the client that contains the list of previously-assigned groups.</span></span> <span data-ttu-id="608fb-121">사용자가 요청 된 그룹에 속하는지 여부를 확인 하려는 경우에 기본 동작을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-121">If you want to verify whether the user belongs to the requested groups, you can override the default behavior.</span></span>

<span data-ttu-id="608fb-122">이 항목은 다음 섹션으로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-122">This topic includes the following sections:</span></span>

- [<span data-ttu-id="608fb-123">사용자 추가 및 제거</span><span class="sxs-lookup"><span data-stu-id="608fb-123">Adding and removing users</span></span>](#add)
- [<span data-ttu-id="608fb-124">그룹의 멤버를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-124">Calling members of a group</span></span>](#call)
- [<span data-ttu-id="608fb-125">그룹 멤버 자격 데이터베이스에 저장</span><span class="sxs-lookup"><span data-stu-id="608fb-125">Storing group membership in a database</span></span>](#storedatabase)
- [<span data-ttu-id="608fb-126">Azure 테이블 저장소에 그룹 구성원 자격을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-126">Storing group membership in Azure table storage</span></span>](#storeazuretable)
- [<span data-ttu-id="608fb-127">다시 연결 될 때 그룹 구성원 자격 확인</span><span class="sxs-lookup"><span data-stu-id="608fb-127">Verifying group membership when reconnecting</span></span>](#verify)

<a id="add"></a>

## <a name="adding-and-removing-users"></a><span data-ttu-id="608fb-128">사용자 추가 및 제거</span><span class="sxs-lookup"><span data-stu-id="608fb-128">Adding and removing users</span></span>

<span data-ttu-id="608fb-129">호출을 추가 하거나 그룹에서 사용자를 제거 하려면는 [추가](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) 또는 [제거](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) 메서드 및 사용자의 연결 id와 그룹의 이름을 매개 변수로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-129">To add or remove users from a group, you call the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) or [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods, and pass in the user's connection id and group's name as parameters.</span></span> <span data-ttu-id="608fb-130">연결이 끝나면 그룹에서 사용자를 수동으로 제거 하 고 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-130">You do not need to manually remove a user from a group when the connection ends.</span></span>

<span data-ttu-id="608fb-131">다음 예제와 `Groups.Add` 및 `Groups.Remove` 허브 메서드에서 사용 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-131">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample1.cs?highlight=5,10)]

<span data-ttu-id="608fb-132">`Groups.Add` 및 `Groups.Remove` 메서드를 비동기적으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-132">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span>

<span data-ttu-id="608fb-133">그룹에 클라이언트를 추가 및 즉시 그룹을 사용 하 여 클라이언트에 메시지를 전송 하려는 경우 Groups.Add 메서드를 먼저 완료 되도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-133">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the Groups.Add method finishes first.</span></span> <span data-ttu-id="608fb-134">다음 코드 예제는.NET 4.5와.NET 4에서 작동 하는 코드를 사용 하 여 사용할 수 있는 코드를 사용 하 여는 작업을 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-134">The following code examples show how to do that, one by using code that works in .NET 4.5, and one by using code that works in .NET 4.</span></span>

#### <a name="asynchronous-net-45-example"></a><span data-ttu-id="608fb-135">비동기.NET 4.5 예제</span><span class="sxs-lookup"><span data-stu-id="608fb-135">Asynchronous .NET 4.5 Example</span></span>

[!code-csharp[Main](working-with-groups/samples/sample2.cs?highlight=1,3)]

#### <a name="asynchronous-net-4-example"></a><span data-ttu-id="608fb-136">비동기.NET 4 예제</span><span class="sxs-lookup"><span data-stu-id="608fb-136">Asynchronous .NET 4 Example</span></span>

[!code-csharp[Main](working-with-groups/samples/sample3.cs?highlight=3-4)]

<span data-ttu-id="608fb-137">일반적으로 포함 하면 안 `await` 를 호출할 때는 `Groups.Remove` 메서드는 제거 하려는 연결 id 더 이상 사용할 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-137">In general, you should not include `await` when calling the `Groups.Remove` method because the connection id that you are trying to remove might no longer be available.</span></span> <span data-ttu-id="608fb-138">이 경우 `TaskCanceledException` 요청이 시간 초과 후 throw 됩니다. 경우 응용 프로그램 사용자 그룹에 메시지를 보내기 전에 그룹에서 제거 되어 있는지 확인 해야를 추가할 수 있습니다 `await` Groups.Remove, 및 다음 catch 하기 전에 `TaskCanceledException` throw 될 수 있는 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-138">In that case, `TaskCanceledException` is thrown after the request times out. If your application must ensure that the user has been removed from the group before sending a message to the group, you can add `await` before Groups.Remove, and then catch the `TaskCanceledException` exception that might be thrown.</span></span>

<a id="call"></a>

## <a name="calling-members-of-a-group"></a><span data-ttu-id="608fb-139">그룹의 멤버를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-139">Calling members of a group</span></span>

<span data-ttu-id="608fb-140">다음 예제에 나와 있는 것 처럼 모든 그룹의 구성원 또는 그룹의 지정 된 멤버만에 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-140">You can send messages to all of the members of a group or only specified members of the group, as shown in the following examples.</span></span>

- <span data-ttu-id="608fb-141">**모든** 지정된 된 그룹의 클라이언트를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-141">**All** connected clients in a specified group.</span></span> 

    [!code-css[Main](working-with-groups/samples/sample4.css)]
- <span data-ttu-id="608fb-142">연결 된 모든 클라이언트에서 지정된 된 그룹의 **지정 된 클라이언트를 제외 하 고**로 식별 되 연결 id입니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-142">All connected clients in a specified group **except the specified clients**, identified by connection ID.</span></span> 

    [!code-csharp[Main](working-with-groups/samples/sample5.cs)]
- <span data-ttu-id="608fb-143">연결 된 모든 클라이언트에서 지정된 된 그룹의 **호출 클라이언트를 제외한**합니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-143">All connected clients in a specified group **except the calling client**.</span></span> 

    [!code-css[Main](working-with-groups/samples/sample6.css)]

<a id="storedatabase"></a>

## <a name="storing-group-membership-in-a-database"></a><span data-ttu-id="608fb-144">그룹 멤버 자격 데이터베이스에 저장</span><span class="sxs-lookup"><span data-stu-id="608fb-144">Storing group membership in a database</span></span>

<span data-ttu-id="608fb-145">다음 예에서는 데이터베이스에 그룹 및 사용자 정보를 저장 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-145">The following examples show how to retain group and user information in a database.</span></span> <span data-ttu-id="608fb-146">모든 데이터 액세스 기술; 사용할 수 있습니다. 그러나 다음 예제에서는 Entity Framework를 사용 하 여 모델을 정의 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-146">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="608fb-147">이러한 엔터티 모델 데이터베이스 테이블 및 필드에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-147">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="608fb-148">데이터 구조에 응용 프로그램의 요구 사항에 따라 크게 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-148">Your data structure could vary considerably depending on the requirements of your application.</span></span> <span data-ttu-id="608fb-149">이 예제에서는 라는 클래스를 포함 `ConversationRoom` 스포츠 또는 가든 같은 서로 다른 대상에 대 한 대화에 참여 하는 수 있도록 하는 응용 프로그램에 고유한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-149">This example includes a class named `ConversationRoom` which would be unique to an application that enables users to join conversations about different subjects, such as sports or gardening.</span></span> <span data-ttu-id="608fb-150">이 예제는 또한 연결에 대 한 클래스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-150">This example also includes a class for the connections.</span></span> <span data-ttu-id="608fb-151">연결 클래스는 그룹 멤버 자격을 추적 하기 위한 절대적으로 필요 하지 않지만 자주 사용자 추적을 강력한 솔루션의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-151">The connection class is not absolutely required for tracking group membership but is frequently part of robust solution to tracking users.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample7.cs)]

<span data-ttu-id="608fb-152">그런 다음 허브 데이터베이스에서 그룹 및 사용자 정보를 검색할 수 있으며 해당 그룹에 사용자를 수동으로 추가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-152">Then, in the hub, you can retrieve the group and user information from the database and manually add the user to the appropriate groups.</span></span> <span data-ttu-id="608fb-153">이 예제에서는 사용자 연결을 추적 하기 위한 코드를 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-153">The example does not include code for tracking the user connections.</span></span> <span data-ttu-id="608fb-154">이 예제에서는 `await` 하기 전에 키워드를 적용 하지 않으면 `Groups.Add` 메시지 그룹의 구성원에 즉시 전송 되지 되므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-154">In this example, the `await` keyword is not applied before `Groups.Add` because a message is not immediately sent to members of the group.</span></span> <span data-ttu-id="608fb-155">새 멤버를 추가한 후 즉시 그룹의 모든 구성원에 게 메시지를 보내려는 경우는 적용 하려는 `await` 키워드는 비동기 작업이 완료 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-155">If you want to send a message to all members of the group immediately after adding the new member, you would want to apply the `await` keyword to make sure the asynchronous operation has completed.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample8.cs)]

<a id="storeazuretable"></a>

## <a name="storing-group-membership-in-azure-table-storage"></a><span data-ttu-id="608fb-156">Azure 테이블 저장소에 그룹 구성원 자격을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-156">Storing group membership in Azure table storage</span></span>

<span data-ttu-id="608fb-157">Azure 테이블 저장소를 사용 하 여 그룹 및 사용자 정보를 저장 하는 데이터베이스를 사용 하는 것과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-157">Using Azure table storage to store group and user information is similar to using a database.</span></span> <span data-ttu-id="608fb-158">다음 예제에서는 사용자 이름 및 그룹 이름을 저장 하는 테이블 엔터티를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-158">The following example shows a table entity that stores the user name and group name.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample9.cs)]

<span data-ttu-id="608fb-159">허브에 연결할 때 할당 된 그룹을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-159">In the hub, you retrieve the assigned groups when the user connects.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample10.cs)]

<a id="verify"></a>

## <a name="verifying-group-membership-when-reconnecting"></a><span data-ttu-id="608fb-160">다시 연결 될 때 그룹 구성원 자격 확인</span><span class="sxs-lookup"><span data-stu-id="608fb-160">Verifying group membership when reconnecting</span></span>

<span data-ttu-id="608fb-161">기본적으로 SignalR 자동으로 다시 사용자의 적절 한 그룹 때 할당 한 연결을 삭제 하 고 연결 시간이 초과 되기 전에 다시 설정 하는 경우 등의 임시 중단에서 다시 연결 합니다. 를 다시 연결 될 때 사용자의 그룹 정보 토큰을 전달 하 고 서버에서 해당 토큰을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-161">By default, SignalR automatically re-assigns a user to the appropriate groups when reconnecting from a temporary disruption, such as when a connection is dropped and re-established before the connection times out. The user's group information is passed in a token when reconnecting, and that token is verified on the server.</span></span> <span data-ttu-id="608fb-162">사용자 그룹에 다시 가입에 대 한 확인 프로세스에 대 한 정보를 참조 하십시오. [다시 연결 될 때 그룹에 다시 가입](index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-162">For information about the verification process for rejoining users to groups, see [Rejoining groups when reconnecting](index.md).</span></span>

<span data-ttu-id="608fb-163">일반적으로 자동으로 다시 연결 그룹에 다시 가입의 기본 동작을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-163">In general, you should use the default behavior of automatically rejoining groups on reconnect.</span></span> <span data-ttu-id="608fb-164">SignalR 그룹에 중요 한 데이터에 대 한 액세스를 제한 하기 위해 보안 메커니즘으로 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-164">SignalR groups are not intended as a security mechanism for restricting access to sensitive data.</span></span> <span data-ttu-id="608fb-165">그러나 응용 프로그램 다시 연결 될 때 사용자의 그룹 구성원 자격을 다시 확인 해야, 하는 경우 기본 동작을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-165">However, if your application must double-check a user's group membership when reconnecting, you can override the default behavior.</span></span> <span data-ttu-id="608fb-166">기본 동작 변경 있으므로 추가할 수는 부담이 데이터베이스에는 사용자를 연결 하는 경우에 아닌 각 다시 연결에 대 한 사용자의 그룹 구성원 자격을 검색 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-166">Changing the default behavior can add a burden to your database because a user's group membership must be retrieved for each reconnection rather than just when the user connects.</span></span>

<span data-ttu-id="608fb-167">그룹 구성원 자격을 확인 해야 하는 경우에 다시 연결을 아래와 같이 할당 된 그룹의 목록을 반환 하는 새 허브 파이프라인 모듈을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-167">If you must verify group membership on reconnect, create a new hub pipeline module that returns a list of assigned groups, as shown below.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample11.cs)]

<span data-ttu-id="608fb-168">허브 파이프라인 아래 강조 표시 된 대로 해당 모듈을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="608fb-168">Then, add that module to the hub pipeline, as highlighted below.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample12.cs?highlight=10)]
