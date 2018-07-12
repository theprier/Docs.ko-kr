---
uid: signalr/overview/guide-to-the-api/working-with-groups
title: SignalR에서 그룹 사용 | Microsoft Docs
author: pfletcher
description: 이 항목에서는 허브 API를 사용 하 여 그룹 멤버 자격 정보를 유지 하는 방법을 설명 합니다.
ms.author: aspnetcontent
ms.date: 06/10/2014
ms.assetid: cd378ecd-3e9e-4236-b902-65916d85a048
msc.legacyurl: /signalr/overview/guide-to-the-api/working-with-groups
msc.type: authoredcontent
ms.openlocfilehash: ea396764bfba0a20347dc231acf40cb36adc1e37
ms.sourcegitcommit: 260abb706ed17f07a53288d8a0c3e69fc13e7468
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38966733"
---
<a name="working-with-groups-in-signalr"></a><span data-ttu-id="6d35c-103">SignalR에서 그룹 작업</span><span class="sxs-lookup"><span data-stu-id="6d35c-103">Working with Groups in SignalR</span></span>
====================
<span data-ttu-id="6d35c-104">하 여 [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="6d35c-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="6d35c-105">이 항목에서는 사용자 그룹에 추가 하 여 그룹 멤버 자격 정보를 유지 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-105">This topic describes how to add users to groups and persist group membership information.</span></span> 
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="6d35c-106">이 항목에서 사용 하는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="6d35c-106">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="6d35c-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="6d35c-107">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="6d35c-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="6d35c-108">.NET 4.5</span></span>
> - <span data-ttu-id="6d35c-109">SignalR 버전 2</span><span class="sxs-lookup"><span data-stu-id="6d35c-109">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="6d35c-110">이 항목의 이전 버전</span><span class="sxs-lookup"><span data-stu-id="6d35c-110">Previous versions of this topic</span></span>
> 
> <span data-ttu-id="6d35c-111">이전 버전의 SignalR에 대 한 정보를 참조 하세요 [SignalR 이전 버전](../older-versions/index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="6d35c-112">질문이 나 의견이 있으면</span><span class="sxs-lookup"><span data-stu-id="6d35c-112">Questions and comments</span></span>
> 
> <span data-ttu-id="6d35c-113">이 자습서를 연결 하는 방법 및 새로운 개선할 수 있습니다 페이지의 맨 아래에 의견에서에 의견을 남겨 주세요.</span><span class="sxs-lookup"><span data-stu-id="6d35c-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="6d35c-114">에 자습서로 직접 관련 되지 않은 질문이 있을 경우 게시할 수 하는 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


## <a name="overview"></a><span data-ttu-id="6d35c-115">개요</span><span class="sxs-lookup"><span data-stu-id="6d35c-115">Overview</span></span>

<span data-ttu-id="6d35c-116">SignalR에서 그룹에 연결 된 클라이언트의 지정 된 하위 집합에 메시지 브로드캐스트 하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-116">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="6d35c-117">그룹의 클라이언트에서 모든 수 있고 클라이언트가 여러 그룹의 멤버일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-117">A group can have any number of clients, and a client can be a member of any number of groups.</span></span> <span data-ttu-id="6d35c-118">명시적으로 그룹을 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-118">You don't have to explicitly create groups.</span></span> <span data-ttu-id="6d35c-119">실제로 그룹 Groups.Add에 대 한 호출에 해당 이름을 지정 하는 처음으로 자동으로 만들어집니다 및 마지막 연결에 대 한 멤버 자격에서 제거할 때 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-119">In effect, a group is automatically created the first time you specify its name in a call to Groups.Add, and it is deleted when you remove the last connection from membership in it.</span></span> <span data-ttu-id="6d35c-120">그룹을 사용 하 여 소개를 참조 하세요 [허브 클래스에서 그룹 멤버 자격을 관리 하는 방법을](hubs-api-guide-server.md#groupsfromhub) Hubs API-Server 가이드에서에서.</span><span class="sxs-lookup"><span data-stu-id="6d35c-120">For an introduction to using groups, see [How to manage group membership from the Hub class](hubs-api-guide-server.md#groupsfromhub) in the Hubs API - Server Guide.</span></span>

<span data-ttu-id="6d35c-121">그룹 멤버 자격 목록 또는 그룹 목록을 가져오기 위한 API는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-121">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="6d35c-122">SignalR 클라이언트와 pub/sub 모델을 기반으로 하는 그룹에 메시지를 전송 하 고 서버 그룹 또는 그룹 멤버 자격 목록을 유지 관리 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-122">SignalR sends messages to clients and groups based on a pub/sub model, and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="6d35c-123">이렇게 하면 확장성을 최대화 하기 때문에 웹 팜에 노드를 추가할 때마다 SignalR 유지 관리 하는 모든 상태를 새 노드에 전파 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-123">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<span data-ttu-id="6d35c-124">사용 하 여 그룹에 사용자를 추가 하 여 `Groups.Add` 메서드인 사용자 현재 연결 기간 동안 해당 그룹에 전달 하는 메시지를 수신 하지만 해당 그룹의 멤버 자격 사용자의 현재 연결 지속 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-124">When you add a user to a group using the `Groups.Add` method, the user receives messages directed to that group for the duration of the current connection, but the user's membership in that group is not persisted beyond the current connection.</span></span> <span data-ttu-id="6d35c-125">그룹과 그룹 멤버 자격에 대 한 정보를 영구적으로 유지 하려는 경우 database 또는 Azure table storage와 같은 리포지토리에서 데이터를 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-125">If you want to permanently retain information about groups and group membership, you must store that data in a repository such as a database or Azure table storage.</span></span> <span data-ttu-id="6d35c-126">그런 다음 사용자가 응용 프로그램에 연결 될 때마다 사용자가 속한 그룹 저장소에서 검색 하 수동으로 이러한 그룹에 해당 사용자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-126">Then, each time a user connects to your application, you retrieve from the repository which groups the user belongs to, and manually add that user to those groups.</span></span>

<span data-ttu-id="6d35c-127">임시 중단 후 다시 연결할 때 사용자 자동으로 다시 조인 이전에 할당 된 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-127">When reconnecting after a temporary disruption, the user automatically re-joins the previously-assigned groups.</span></span> <span data-ttu-id="6d35c-128">그룹에 자동으로 다시 참여 새 연결을 설정할 때가 아니라 다시 연결할 때 때만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-128">Automatically rejoining a group only applies when reconnecting, not when establishing a new connection.</span></span> <span data-ttu-id="6d35c-129">디지털 서명 된 토큰을 이전에 할당 된 그룹 목록을 포함 하는 클라이언트에서 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-129">A digitally-signed token is passed from the client that contains the list of previously-assigned groups.</span></span> <span data-ttu-id="6d35c-130">사용자 요청 된 그룹에 속하는지 여부를 확인 하려는 경우에 기본 동작을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-130">If you want to verify whether the user belongs to the requested groups, you can override the default behavior.</span></span>

<span data-ttu-id="6d35c-131">이 항목은 다음 섹션으로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-131">This topic includes the following sections:</span></span>

- [<span data-ttu-id="6d35c-132">사용자 추가 및 제거</span><span class="sxs-lookup"><span data-stu-id="6d35c-132">Adding and removing users</span></span>](#add)
- [<span data-ttu-id="6d35c-133">그룹의 멤버를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-133">Calling members of a group</span></span>](#call)
- [<span data-ttu-id="6d35c-134">그룹 멤버 자격 데이터베이스에 저장</span><span class="sxs-lookup"><span data-stu-id="6d35c-134">Storing group membership in a database</span></span>](#storedatabase)
- [<span data-ttu-id="6d35c-135">Azure table storage에 저장 그룹 멤버 자격</span><span class="sxs-lookup"><span data-stu-id="6d35c-135">Storing group membership in Azure table storage</span></span>](#storeazuretable)
- [<span data-ttu-id="6d35c-136">다시 연결 하는 경우 그룹 구성원 자격 확인</span><span class="sxs-lookup"><span data-stu-id="6d35c-136">Verifying group membership when reconnecting</span></span>](#verify)

<a id="add"></a>

## <a name="adding-and-removing-users"></a><span data-ttu-id="6d35c-137">사용자 추가 및 제거</span><span class="sxs-lookup"><span data-stu-id="6d35c-137">Adding and removing users</span></span>

<span data-ttu-id="6d35c-138">호출을 추가 하거나 그룹에서 사용자를 제거 하려면 합니다 [추가](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) 하거나 [제거](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) 메서드 및 사용자의 연결 id 및 그룹의 이름을 매개 변수로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-138">To add or remove users from a group, you call the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) or [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods, and pass in the user's connection id and group's name as parameters.</span></span> <span data-ttu-id="6d35c-139">연결이 끝나면 그룹에서 사용자를 수동으로 제거 하 고 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-139">You do not need to manually remove a user from a group when the connection ends.</span></span>

<span data-ttu-id="6d35c-140">다음 예제는 `Groups.Add` 및 `Groups.Remove` 허브 메서드에서 사용 되는 메서드.</span><span class="sxs-lookup"><span data-stu-id="6d35c-140">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample1.cs?highlight=5,10)]

<span data-ttu-id="6d35c-141">합니다 `Groups.Add` 고 `Groups.Remove` 메서드가 비동기적으로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-141">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span>

<span data-ttu-id="6d35c-142">그룹에 클라이언트를 추가 하 고 클라이언트에 그룹을 사용 하 여 메시지를 즉시 보내도록 하려면 Groups.Add 메서드를 먼저 완료 되도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-142">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the Groups.Add method finishes first.</span></span> <span data-ttu-id="6d35c-143">다음 코드 예제에는 작업을 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-143">The following code examples show how to do that.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample2.cs?highlight=1,3)]

<span data-ttu-id="6d35c-144">일반적으로 포함 하면 안 `await` 호출 하는 경우는 `Groups.Remove` 메서드 하므로 제거 하려고 하는 연결 id를 더 이상 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-144">In general, you should not include `await` when calling the `Groups.Remove` method because the connection id that you are trying to remove might no longer be available.</span></span> <span data-ttu-id="6d35c-145">이런 경우 `TaskCanceledException` 요청 시간이 초과 되 면 throw 됩니다. 경우 응용 프로그램 사용자 그룹에 메시지를 보내기 전에 그룹에서 제거 되어 있는지 확인 해야 합니다를 추가할 수 있습니다 `await` 하기 전에 `Groups.Remove`, 및 catch 한 다음는 `TaskCanceledException` throw 될 수 있는 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-145">In that case, `TaskCanceledException` is thrown after the request times out. If your application must ensure that the user has been removed from the group before sending a message to the group, you can add `await` before `Groups.Remove`, and then catch the `TaskCanceledException` exception that might be thrown.</span></span>

<a id="call"></a>

## <a name="calling-members-of-a-group"></a><span data-ttu-id="6d35c-146">그룹의 멤버를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-146">Calling members of a group</span></span>

<span data-ttu-id="6d35c-147">다음 예제와 같이 그룹의 구성원 또는 그룹의 멤버만 지정 된 모든 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-147">You can send messages to all of the members of a group or only specified members of the group, as shown in the following examples.</span></span>

- <span data-ttu-id="6d35c-148">**모든** 지정된 된 그룹의 클라이언트를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-148">**All** connected clients in a specified group.</span></span> 

    [!code-css[Main](working-with-groups/samples/sample3.css)]
- <span data-ttu-id="6d35c-149">지정된 된 그룹의 클라이언트를 연결 된 모든 **지정 된 클라이언트를 제외 하 고**연결 ID로 식별 된,</span><span class="sxs-lookup"><span data-stu-id="6d35c-149">All connected clients in a specified group **except the specified clients**, identified by connection ID.</span></span> 

    [!code-csharp[Main](working-with-groups/samples/sample4.cs)]
- <span data-ttu-id="6d35c-150">지정된 된 그룹의 클라이언트를 연결 된 모든 **호출 클라이언트를 제외한**합니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-150">All connected clients in a specified group **except the calling client**.</span></span> 

    [!code-css[Main](working-with-groups/samples/sample5.css)]

<a id="storedatabase"></a>

## <a name="storing-group-membership-in-a-database"></a><span data-ttu-id="6d35c-151">그룹 멤버 자격 데이터베이스에 저장</span><span class="sxs-lookup"><span data-stu-id="6d35c-151">Storing group membership in a database</span></span>

<span data-ttu-id="6d35c-152">다음 예에서는 데이터베이스의 그룹 및 사용자 정보를 유지 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-152">The following examples show how to retain group and user information in a database.</span></span> <span data-ttu-id="6d35c-153">모든 데이터 액세스 기술;를 사용할 수 있습니다. 그러나 다음 예제에서는 Entity Framework를 사용 하 여 모델을 정의 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-153">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="6d35c-154">이러한 엔터티 모델은 데이터베이스 테이블 및 필드에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-154">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="6d35c-155">데이터 구조에는 응용 프로그램의 요구 사항에 따라 크게 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-155">Your data structure could vary considerably depending on the requirements of your application.</span></span> <span data-ttu-id="6d35c-156">이 예제에서는 라는 클래스를 포함 `ConversationRoom` 스포츠 가든 등 다양 한 주제에 대 한 대화에 연결할 수 있는 응용 프로그램에 고유한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-156">This example includes a class named `ConversationRoom` which would be unique to an application that enables users to join conversations about different subjects, such as sports or gardening.</span></span> <span data-ttu-id="6d35c-157">이 예제에는 연결에 대 한 클래스도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-157">This example also includes a class for the connections.</span></span> <span data-ttu-id="6d35c-158">연결 클래스를 사용 하는 그룹 멤버 자격을 추적 하기 위한 절대적으로 필요 하지 않습니다 하지만 사용자를 추적 하는 강력한 솔루션의 일부인 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-158">The connection class is not absolutely required for tracking group membership but is frequently part of robust solution to tracking users.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample6.cs)]

<span data-ttu-id="6d35c-159">그런 다음 허브 데이터베이스에서 그룹 및 사용자 정보를 검색할 수 있으며 수동으로 사용자에 적절 한 그룹을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-159">Then, in the hub, you can retrieve the group and user information from the database and manually add the user to the appropriate groups.</span></span> <span data-ttu-id="6d35c-160">이 예제에서는 사용자 연결을 추적 하기 위한 코드를 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-160">The example does not include code for tracking the user connections.</span></span> <span data-ttu-id="6d35c-161">이 예제에서는 합니다 `await` 하기 전에 키워드 적용 되지 않습니다 `Groups.Add` 되므로 그룹의 구성원에 게는 메시지가 즉시 전송 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-161">In this example, the `await` keyword is not applied before `Groups.Add` because a message is not immediately sent to members of the group.</span></span> <span data-ttu-id="6d35c-162">적용 하려는 새 멤버를 추가한 후 즉시 그룹의 모든 멤버에 메시지를 보내려는 경우는 `await` 키워드는 비동기 작업이 완료 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-162">If you want to send a message to all members of the group immediately after adding the new member, you would want to apply the `await` keyword to make sure the asynchronous operation has completed.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample7.cs)]

<a id="storeazuretable"></a>

## <a name="storing-group-membership-in-azure-table-storage"></a><span data-ttu-id="6d35c-163">Azure table storage에 저장 그룹 멤버 자격</span><span class="sxs-lookup"><span data-stu-id="6d35c-163">Storing group membership in Azure table storage</span></span>

<span data-ttu-id="6d35c-164">Azure 테이블 저장소를 사용 하 여 그룹 및 사용자 정보를 저장 하는 데이터베이스를 사용 하는 것과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-164">Using Azure table storage to store group and user information is similar to using a database.</span></span> <span data-ttu-id="6d35c-165">다음 예제에서는 사용자 이름 및 그룹 이름을 저장 하는 테이블 엔터티를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-165">The following example shows a table entity that stores the user name and group name.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample8.cs)]

<span data-ttu-id="6d35c-166">허브에 연결할 때 할당 된 그룹 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-166">In the hub, you retrieve the assigned groups when the user connects.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample9.cs)]

<a id="verify"></a>

## <a name="verifying-group-membership-when-reconnecting"></a><span data-ttu-id="6d35c-167">다시 연결 하는 경우 그룹 구성원 자격 확인</span><span class="sxs-lookup"><span data-stu-id="6d35c-167">Verifying group membership when reconnecting</span></span>

<span data-ttu-id="6d35c-168">기본적으로 SignalR에 자동으로 다시 할당 사용자 적절 한 그룹에서 연결을 삭제 하 고 연결 시간이 초과 되기 전에 다시 설정 하는 경우와 같은 임시 중단, 다시 연결 하는 경우. 다시 연결할 때 때 사용자의 그룹 정보 토큰을 전달 하 고 서버에서 해당 토큰을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-168">By default, SignalR automatically re-assigns a user to the appropriate groups when reconnecting from a temporary disruption, such as when a connection is dropped and re-established before the connection times out. The user's group information is passed in a token when reconnecting, and that token is verified on the server.</span></span> <span data-ttu-id="6d35c-169">사용자 그룹에 다시 참여에 대 한 확인 프로세스에 대 한 정보를 참조 하세요 [다시 연결 하는 경우 그룹에 다시 참여](../security/introduction-to-security.md#rejoingroup)합니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-169">For information about the verification process for rejoining users to groups, see [Rejoining groups when reconnecting](../security/introduction-to-security.md#rejoingroup).</span></span>

<span data-ttu-id="6d35c-170">일반적으로 자동으로 그룹에 다시 연결에 다시 참여의 기본 동작을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-170">In general, you should use the default behavior of automatically rejoining groups on reconnect.</span></span> <span data-ttu-id="6d35c-171">중요 한 데이터에 대 한 액세스를 제한 하는 것에 대 한 보안 메커니즘으로 SignalR 그룹을 사용 하는 것이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-171">SignalR groups are not intended as a security mechanism for restricting access to sensitive data.</span></span> <span data-ttu-id="6d35c-172">그러나 응용 프로그램 다시 연결 하는 경우 사용자의 그룹 멤버 자격을 다시 확인 해야 합니다, 경우 기본 동작을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-172">However, if your application must double-check a user's group membership when reconnecting, you can override the default behavior.</span></span> <span data-ttu-id="6d35c-173">기본 동작 변경 이므로 추가할 수 부담 데이터베이스에 사용자가 연결 하는 경우에 아니라 각 연결에 사용자의 그룹 멤버 자격을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-173">Changing the default behavior can add a burden to your database because a user's group membership must be retrieved for each reconnection rather than just when the user connects.</span></span>

<span data-ttu-id="6d35c-174">그룹 멤버 자격을 확인 해야 하는 경우 다시 연결, 아래와 같이 할당 된 그룹의 목록을 반환 하는 새 허브 파이프라인 모듈을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-174">If you must verify group membership on reconnect, create a new hub pipeline module that returns a list of assigned groups, as shown below.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample10.cs)]

<span data-ttu-id="6d35c-175">아래 강조 표시 된 대로 허브 파이프라인으로 모듈을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d35c-175">Then, add that module to the hub pipeline, as highlighted below.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample11.cs?highlight=4)]
