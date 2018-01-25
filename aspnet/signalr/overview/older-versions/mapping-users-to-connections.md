---
uid: signalr/overview/older-versions/mapping-users-to-connections
title: "SignalR 사용자의 SignalR 연결으로 매핑 1.x | Microsoft Docs"
author: pfletcher
description: "이 항목에는 사용자 및 해당 연결에 대 한 정보를 저장 하는 방법을 보여 줍니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/17/2013
ms.topic: article
ms.assetid: ebbc93a8-e6c4-4122-8e0d-3aa42293c747
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/older-versions/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: 896bf4142ce090e39ed5697ff053cd56728318ed
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="mapping-signalr-users-to-connections-in-signalr-1x"></a><span data-ttu-id="5feca-103">SignalR 사용자의 SignalR 연결으로 매핑 1.x</span><span class="sxs-lookup"><span data-stu-id="5feca-103">Mapping SignalR Users to Connections in SignalR 1.x</span></span>
====================
<span data-ttu-id="5feca-104">여 [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="5feca-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="5feca-105">이 항목에는 사용자 및 해당 연결에 대 한 정보를 저장 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-105">This topic shows how to retain information about users and their connections.</span></span>


## <a name="introduction"></a><span data-ttu-id="5feca-106">소개</span><span class="sxs-lookup"><span data-stu-id="5feca-106">Introduction</span></span>

<span data-ttu-id="5feca-107">허브에 연결 되는 각 클라이언트 고유 연결 id를 전달 합니다. 이 값을 검색할 수 있습니다는 `Context.ConnectionId` 허브 컨텍스트 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-107">Each client connecting to a hub passes a unique connection id. You can retrieve this value in the `Context.ConnectionId` property of the hub context.</span></span> <span data-ttu-id="5feca-108">응용 프로그램을 사용자 연결 id에 매핑한 매핑이 유지 하는 경우에 다음 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-108">If your application needs to map a user to the connection id and persist that mapping, you can use one of the following:</span></span>

- <span data-ttu-id="5feca-109">[메모리 내 저장소](#inmemory), 사전 등</span><span class="sxs-lookup"><span data-stu-id="5feca-109">[In-memory storage](#inmemory), such as a dictionary</span></span>
- [<span data-ttu-id="5feca-110">각 사용자에 대 한 SignalR 그룹</span><span class="sxs-lookup"><span data-stu-id="5feca-110">SignalR group for each user</span></span>](#groups)
- <span data-ttu-id="5feca-111">[세션에서 외부 저장소](#database)데이터베이스 테이블 또는 Azure 테이블 저장소와 같은</span><span class="sxs-lookup"><span data-stu-id="5feca-111">[Permanent, external storage](#database), such as a database table or Azure table storage</span></span>

<span data-ttu-id="5feca-112">각각의이 구현은이 항목에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-112">Each of these implementations is shown in this topic.</span></span> <span data-ttu-id="5feca-113">사용 된 `OnConnected`, `OnDisconnected`, 및 `OnReconnected` 의 메서드는 `Hub` 사용자 연결 상태를 추적 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-113">You use the `OnConnected`, `OnDisconnected`, and `OnReconnected` methods of the `Hub` class to track the user connection status.</span></span>

<span data-ttu-id="5feca-114">가장 좋은 방법은 응용 프로그램에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-114">The best approach for your application depends on:</span></span>

- <span data-ttu-id="5feca-115">응용 프로그램을 호스팅하는 웹 서버의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-115">The number of web servers hosting your application.</span></span>
- <span data-ttu-id="5feca-116">현재 연결 된 사용자 목록을 가져와서 해야 하는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-116">Whether you need to get a list of the currently connected users.</span></span>
- <span data-ttu-id="5feca-117">응용 프로그램 또는 서버를 다시 시작 하는 경우에 그룹 및 사용자 정보를 유지 해야 하는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-117">Whether you need to persist group and user information when the application or server restarts.</span></span>
- <span data-ttu-id="5feca-118">외부 서버를 호출 하 여 대기 시간 문제 인지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-118">Whether the latency of calling an external server is an issue.</span></span>

<span data-ttu-id="5feca-119">다음 표에서 이러한 고려 사항에 대해 작동 하는 방식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-119">The following table shows which approach works for these considerations.</span></span>

|  | <span data-ttu-id="5feca-120">둘 이상의 서버</span><span class="sxs-lookup"><span data-stu-id="5feca-120">More than one server</span></span> | <span data-ttu-id="5feca-121">현재 연결 된 사용자 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-121">Get list of currently connected users</span></span> | <span data-ttu-id="5feca-122">다시 시작한 다음 정보를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-122">Persist information after restarts</span></span> | <span data-ttu-id="5feca-123">최적의 성능</span><span class="sxs-lookup"><span data-stu-id="5feca-123">Optimal performance</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="5feca-124">메모리 내</span><span class="sxs-lookup"><span data-stu-id="5feca-124">In-memory</span></span> |  | ![](mapping-users-to-connections/_static/image1.png) |  | ![](mapping-users-to-connections/_static/image2.png) |
| <span data-ttu-id="5feca-125">단일 사용자 그룹</span><span class="sxs-lookup"><span data-stu-id="5feca-125">Single-user groups</span></span> | ![](mapping-users-to-connections/_static/image3.png) |  |  | ![](mapping-users-to-connections/_static/image4.png) |
| <span data-ttu-id="5feca-126">영구 외부</span><span class="sxs-lookup"><span data-stu-id="5feca-126">Permanent, external</span></span> | ![](mapping-users-to-connections/_static/image5.png) | ![](mapping-users-to-connections/_static/image6.png) | ![](mapping-users-to-connections/_static/image7.png) |  |

<a id="inmemory"></a>

## <a name="in-memory-storage"></a><span data-ttu-id="5feca-127">메모리 내 저장소</span><span class="sxs-lookup"><span data-stu-id="5feca-127">In-memory storage</span></span>

<span data-ttu-id="5feca-128">다음 예제는 메모리에 저장 된 사전에 연결 및 사용자 정보를 유지 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-128">The following examples show how to retain connection and user information in a dictionary that is stored in memory.</span></span> <span data-ttu-id="5feca-129">사전을 사용 하 여 한 `HashSet` 연결 id를 저장할 수 있습니다. 언제 든 지 사용자 SignalR 응용 프로그램에 둘 이상의 연결이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-129">The dictionary uses a `HashSet` to store the connection id. At any time a user could have more than one connection to the SignalR application.</span></span> <span data-ttu-id="5feca-130">예를 들어 사용자가 여러 장치 또는 둘 이상의 브라우저 탭을 통해 연결 된 둘 이상의 연결 id는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-130">For example, a user who is connected through multiple devices or more than one browser tab would have more than one connection id.</span></span>

<span data-ttu-id="5feca-131">응용 프로그램이 종료 되 면 모든 정보가 손실 되 있지만 다시 채워집니다 사용자가 연결을 다시 설정 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-131">If the application shuts down, all of the information is lost, but it will be re-populated as the users re-establish their connections.</span></span> <span data-ttu-id="5feca-132">환경의 각 서버 연결의 별도 컬렉션을 갖기 때문에 둘 이상의 웹 서버를 포함 하는 경우에 메모리 내 저장소 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-132">In-memory storage does not work if your environment includes more than one web server because each server would have a separate collection of connections.</span></span>

<span data-ttu-id="5feca-133">첫 번째 예에서는 연결에 대 한 사용자 매핑을 관리 하는 클래스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-133">The first example shows a class that manages the mapping of users to connections.</span></span> <span data-ttu-id="5feca-134">HashSet에 대 한 키를 사용자의 이름이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-134">The key for the HashSet will be the user's name.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

<span data-ttu-id="5feca-135">다음 예에서는 허브에서 연결 매핑 클래스를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-135">The next example shows how to use the connection mapping class from a hub.</span></span> <span data-ttu-id="5feca-136">클래스의 인스턴스는 변수 이름에 저장 된 `_connections`합니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-136">The instance of the class is stored in a variable name `_connections`.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a><span data-ttu-id="5feca-137">단일 사용자 그룹</span><span class="sxs-lookup"><span data-stu-id="5feca-137">Single-user groups</span></span>

<span data-ttu-id="5feca-138">각 사용자에 대 한 그룹을 만들고에 해당 사용자만 액세스 하려는 경우 해당 그룹에는 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-138">You can create a group for each user, and then send a message to that group when you want to reach only that user.</span></span> <span data-ttu-id="5feca-139">각 그룹의 이름은 사용자의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-139">The name of each group is the name of the user.</span></span> <span data-ttu-id="5feca-140">사용자에 게 둘 이상의 연결을 경우 각 연결 id는 사용자의 그룹에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-140">If a user has more than one connection, each connection id is added to the user's group.</span></span>

<span data-ttu-id="5feca-141">하지 수동으로 제거 해야 사용자 그룹에서 사용자 연결을 끊을 때.</span><span class="sxs-lookup"><span data-stu-id="5feca-141">You should not manually remove the user from the group when the user disconnects.</span></span> <span data-ttu-id="5feca-142">이 작업은 SignalR 프레임 워크에서 자동으로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-142">This action is automatically performed by the SignalR framework.</span></span>

<span data-ttu-id="5feca-143">다음 예제에서는 단일 사용자 그룹을 구현 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-143">The following example shows how to implement single-user groups.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a><span data-ttu-id="5feca-144">세션에서 외부 저장소</span><span class="sxs-lookup"><span data-stu-id="5feca-144">Permanent, external storage</span></span>

<span data-ttu-id="5feca-145">이 항목에서는 연결 정보를 저장 하기 위한 데이터베이스 또는 Azure 테이블 저장소를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-145">This topic shows how to use either a database or Azure table storage for storing connection information.</span></span> <span data-ttu-id="5feca-146">이 방법은 각 웹 서버는 동일한 데이터 저장소와 상호 작용할 수 때문에 웹 서버가 여러 개 있는 경우에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-146">This approach works when you have multiple web servers because each web server can interact with the same data repository.</span></span> <span data-ttu-id="5feca-147">웹 서버 또는 응용 프로그램 다시 시작 하는 작업을 중지 하는 경우는 `OnDisconnected` 메서드가 호출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-147">If your web servers stop working or the application restarts, the `OnDisconnected` method is not called.</span></span> <span data-ttu-id="5feca-148">따라서 것이 데이터 저장소에 더 이상 사용할 수 있는 연결 id에 대 한 레코드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-148">Therefore, it is possible that your data repository will have records for connection ids that are no longer valid.</span></span> <span data-ttu-id="5feca-149">이러한 분리 된 레코드를 정리 하려면 응용 프로그램에 관련 된 시간 범위 외부에서 생성 된 모든 연결을 무효화 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-149">To clean up these orphaned records, you may wish to invalidate any connection that was created outside of a timeframe that is relevant to your application.</span></span> <span data-ttu-id="5feca-150">이 섹션의 예에서는 연결을 만들 때 추적에 대 한 값이 포함 되지만 백그라운드 작업으로 작업을 수행 하는 것이 좋습니다 때문에 오래 된 레코드를 정리 하는 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-150">The examples in this section include a value for tracking when the connection was created, but do not show how to clean up old records because you may want to do that as background process.</span></span>

### <a name="database"></a><span data-ttu-id="5feca-151">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="5feca-151">Database</span></span>

<span data-ttu-id="5feca-152">다음 예에서는 데이터베이스에 연결 및 사용자 정보를 저장 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-152">The following examples show how to retain connection and user information in a database.</span></span> <span data-ttu-id="5feca-153">모든 데이터 액세스 기술; 사용할 수 있습니다. 그러나 다음 예제에서는 Entity Framework를 사용 하 여 모델을 정의 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-153">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="5feca-154">이러한 엔터티 모델 데이터베이스 테이블 및 필드에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-154">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="5feca-155">데이터 구조에 응용 프로그램의 요구 사항에 따라 크게 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-155">Your data structure could vary considerably depending on the requirements of your application.</span></span>

<span data-ttu-id="5feca-156">첫 번째 예에는 많은 연결 엔터티와 연결할 수 있는 사용자 엔터티를 정의 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-156">The first example shows how to define a user entity that can be associated with many connection entities.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

<span data-ttu-id="5feca-157">그런 다음 허브에서 아래에 표시 된 코드와 함께 각 연결의 상태를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-157">Then, from the hub, you can track the state of each connection with the code shown below.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

### <a name="azure-table-storage"></a><span data-ttu-id="5feca-158">Azure 테이블 저장소</span><span class="sxs-lookup"><span data-stu-id="5feca-158">Azure table storage</span></span>

<span data-ttu-id="5feca-159">다음 Azure 테이블 저장소 예제 데이터베이스 예제와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-159">The following Azure table storage example is similar to the database example.</span></span> <span data-ttu-id="5feca-160">Azure 테이블 저장소 서비스를 시작 해야 하는 정보를 모두 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-160">It does not include all of the information that you would need to get started with Azure Table Storage Service.</span></span> <span data-ttu-id="5feca-161">자세한 내용은 참조 [.NET에서 테이블 저장소를 사용 하는 방법을](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)합니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-161">For information, see [How to use Table storage from .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span></span>

<span data-ttu-id="5feca-162">다음 예제에서는 연결 정보를 저장 하기 위한 테이블 엔터티를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-162">The following example shows a table entity for storing connection information.</span></span> <span data-ttu-id="5feca-163">사용자 이름으로 데이터를 분할 하 고 사용자는 언제 든 지 여러 개의 연결이 있을 수 있으므로 각 엔터티에 연결 id로 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-163">It partitions the data by user name, and identifies each entity by the connection id, so a user can have multiple connections at any time.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<span data-ttu-id="5feca-164">허브에서 각 사용자의 연결 상태를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5feca-164">In the hub, you track the status of each user's connection.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]
