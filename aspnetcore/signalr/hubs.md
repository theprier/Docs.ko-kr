---
title: ASP.NET Core SignalR에서 허브를 사용 합니다.
author: tdykstra
description: ASP.NET Core SignalR에서 허브를 사용 하는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 05/01/2018
uid: signalr/hubs
ms.openlocfilehash: e583676ab0eed45aeaf6391d8cdf8c1485aa914e
ms.sourcegitcommit: e7e1e531b80b3f4117ff119caadbebf4dcf5dcb7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2018
ms.locfileid: "44510339"
---
# <a name="use-hubs-in-signalr-for-aspnet-core"></a><span data-ttu-id="4ad94-103">SignalR에서 허브를 사용 하 여 ASP.NET Core에 대 한</span><span class="sxs-lookup"><span data-stu-id="4ad94-103">Use hubs in SignalR for ASP.NET Core</span></span>

<span data-ttu-id="4ad94-104">하 여 [Rachel Appel](https://twitter.com/rachelappel) 고 [Kevin Griffin](https://twitter.com/1kevgriff)</span><span class="sxs-lookup"><span data-stu-id="4ad94-104">By [Rachel Appel](https://twitter.com/rachelappel) and [Kevin Griffin](https://twitter.com/1kevgriff)</span></span>

<span data-ttu-id="4ad94-105">[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/hubs/sample/ ) [(다운로드 하는 방법)](xref:tutorials/index#how-to-download-a-sample)</span><span class="sxs-lookup"><span data-stu-id="4ad94-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/hubs/sample/ ) [(how to download)](xref:tutorials/index#how-to-download-a-sample)</span></span>

## <a name="what-is-a-signalr-hub"></a><span data-ttu-id="4ad94-106">SignalR 허브 란</span><span class="sxs-lookup"><span data-stu-id="4ad94-106">What is a SignalR hub</span></span>

<span data-ttu-id="4ad94-107">SignalR 허브 API를 사용 하면 서버에서 연결 된 클라이언트에서 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-107">The SignalR Hubs API enables you to call methods on connected clients from the server.</span></span> <span data-ttu-id="4ad94-108">서버 코드를 클라이언트에서 호출 된 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-108">In the server code, you define methods that are called by client.</span></span> <span data-ttu-id="4ad94-109">클라이언트 코드를 서버에서 호출 된 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-109">In the client code, you define methods that are called from the server.</span></span> <span data-ttu-id="4ad94-110">SignalR은 클라이언트와 서버 간 및 서버와 클라이언트 간 실시간 통신을 가능 하 게 하는 백그라운드에서 모든 부분을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-110">SignalR takes care of everything behind the scenes that makes real-time client-to-server and server-to-client communications possible.</span></span>

## <a name="configure-signalr-hubs"></a><span data-ttu-id="4ad94-111">SignalR 허브를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-111">Configure SignalR hubs</span></span>

<span data-ttu-id="4ad94-112">SignalR 미들웨어를 호출 하 여 구성 된 일부 서비스의 경우 필요한 `services.AddSignalR`합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-112">The SignalR middleware requires some services, which are configured by calling `services.AddSignalR`.</span></span>

[!code-csharp[Configure service](hubs/sample/startup.cs?range=38)]

<span data-ttu-id="4ad94-113">ASP.NET Core 앱에 SignalR 기능을 추가 하는 경우 호출 하 여 SignalR 경로 설정 `app.UseSignalR` 에 `Startup.Configure` 메서드.</span><span class="sxs-lookup"><span data-stu-id="4ad94-113">When adding SignalR functionality to an ASP.NET Core app, setup SignalR routes by calling `app.UseSignalR` in the `Startup.Configure` method.</span></span>

[!code-csharp[Configure routes to hubs](hubs/sample/startup.cs?range=57-60)]

## <a name="create-and-use-hubs"></a><span data-ttu-id="4ad94-114">만들고 허브를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-114">Create and use hubs</span></span>

<span data-ttu-id="4ad94-115">상속 되는 클래스를 선언 하 여 허브를 만들 `Hub`, public 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-115">Create a hub by declaring a class that inherits from `Hub`, and add public methods to it.</span></span> <span data-ttu-id="4ad94-116">클라이언트도 정의 된 메서드를 호출할 수 `public`입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-116">Clients can call methods that are defined as `public`.</span></span>

[!code-csharp[Create and use hubs](hubs/sample/hubs/chathub.cs?range=8-37)]

<span data-ttu-id="4ad94-117">반환 형식 및 C# 메서드에서 마찬가지로 복합 형식 및 배열 등 매개 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-117">You can specify a return type and parameters, including complex types and arrays, as you would in any C# method.</span></span> <span data-ttu-id="4ad94-118">SignalR은 serialization 및 deserialization 복잡 한 개체 및 배열 매개 변수 및 반환 값을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-118">SignalR handles the serialization and deserialization of complex objects and arrays in your parameters and return values.</span></span>

## <a name="the-context-object"></a><span data-ttu-id="4ad94-119">컨텍스트 개체</span><span class="sxs-lookup"><span data-stu-id="4ad94-119">The Context object</span></span>

<span data-ttu-id="4ad94-120">합니다 `Hub` 클래스에는 `Context` 연결에 대 한 정보를 사용 하 여 다음 속성을 포함 하는 속성:</span><span class="sxs-lookup"><span data-stu-id="4ad94-120">The `Hub` class has a `Context` property that contains the following properties with information about the connection:</span></span>

| <span data-ttu-id="4ad94-121">속성</span><span class="sxs-lookup"><span data-stu-id="4ad94-121">Property</span></span> | <span data-ttu-id="4ad94-122">설명</span><span class="sxs-lookup"><span data-stu-id="4ad94-122">Description</span></span> |
| ------ | ----------- |
| `ConnectionId` | <span data-ttu-id="4ad94-123">SignalR에서 할당 된 연결에 대 한 고유 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-123">Gets the unique ID for the connection, assigned by SignalR.</span></span> <span data-ttu-id="4ad94-124">각 연결에 대 한 연결 ID를 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-124">There is one connection ID for each connection.</span></span>|
| `UserIdentifier` | <span data-ttu-id="4ad94-125">가져옵니다 합니다 [사용자 식별자](xref:signalr/groups)합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-125">Gets the [user identifier](xref:signalr/groups).</span></span> <span data-ttu-id="4ad94-126">SignalR 기본적으로 사용 합니다 `ClaimTypes.NameIdentifier` 에서 `ClaimsPrincipal` 사용자 식별자로 연결과 관련 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-126">By default, SignalR uses the `ClaimTypes.NameIdentifier` from the `ClaimsPrincipal` associated with the connection as the user identifier.</span></span> |
| `User` | <span data-ttu-id="4ad94-127">가져옵니다는 `ClaimsPrincipal` 현재 사용자와 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-127">Gets the `ClaimsPrincipal` associated with the current user.</span></span> |
| `Items` | <span data-ttu-id="4ad94-128">이 연결의 범위 내에서 데이터를 공유할 수 있는 키/값 컬렉션을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-128">Gets a key/value collection that can be used to share data within the scope of this connection.</span></span> <span data-ttu-id="4ad94-129">이 컬렉션의 데이터를 저장할 수 있습니다 하 고 연결에 대 한 다양 한 허브 메서드 호출 간에 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-129">Data can be stored in this collection and it will persist for the connection across different hub method invocations.</span></span> |
| `Features` | <span data-ttu-id="4ad94-130">연결에서 사용할 수 있는 기능의 컬렉션을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-130">Gets the collection of features available on the connection.</span></span> <span data-ttu-id="4ad94-131">지금은 자세히 아직 문서화 되지 않습니다 있도록이 컬렉션은 대부분의 시나리오에서 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-131">For now, this collection isn't needed in most scenarios, so it isn't documented in detail yet.</span></span> |
| `ConnectionAborted` | <span data-ttu-id="4ad94-132">가져옵니다는 `CancellationToken` 연결이 중단 될 때를 알리는 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-132">Gets a `CancellationToken` that notifies when the connection is aborted.</span></span> |

<span data-ttu-id="4ad94-133">`Hub.Context` 또한 다음 메서드를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-133">`Hub.Context` also contains the following methods:</span></span>

| <span data-ttu-id="4ad94-134">메서드</span><span class="sxs-lookup"><span data-stu-id="4ad94-134">Method</span></span> | <span data-ttu-id="4ad94-135">설명</span><span class="sxs-lookup"><span data-stu-id="4ad94-135">Description</span></span> |
| ------ | ----------- |
| `GetHttpContext` | <span data-ttu-id="4ad94-136">반환 된 `HttpContext` 연결에 대해 또는 `null` 연결 HTTP 요청을 사용 하 여 연결 되지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="4ad94-136">Returns the `HttpContext` for the connection, or `null` if the connection is not associated with an HTTP request.</span></span> <span data-ttu-id="4ad94-137">HTTP 연결에 대 한 HTTP 헤더 및 쿼리 문자열과 같은 정보를 가져오려면이 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-137">For HTTP connections, you can use this method to get information such as HTTP headers and query strings.</span></span> |
| `Abort` | <span data-ttu-id="4ad94-138">연결을 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-138">Aborts the connection.</span></span> |

## <a name="the-clients-object"></a><span data-ttu-id="4ad94-139">클라이언트 개체</span><span class="sxs-lookup"><span data-stu-id="4ad94-139">The Clients object</span></span>

<span data-ttu-id="4ad94-140">합니다 `Hub` 클래스에는 `Clients` 서버와 클라이언트 간의 통신에 대 한 다음 속성을 포함 하는 속성:</span><span class="sxs-lookup"><span data-stu-id="4ad94-140">The `Hub` class has a `Clients` property that contains the following properties for communication between server and client:</span></span>

| <span data-ttu-id="4ad94-141">속성</span><span class="sxs-lookup"><span data-stu-id="4ad94-141">Property</span></span> | <span data-ttu-id="4ad94-142">설명</span><span class="sxs-lookup"><span data-stu-id="4ad94-142">Description</span></span> |
| ------ | ----------- |
| `All` | <span data-ttu-id="4ad94-143">연결 된 모든 클라이언트에서 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-143">Calls a method on all connected clients</span></span> |
| `Caller` | <span data-ttu-id="4ad94-144">허브 메서드를 호출 하는 클라이언트의 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-144">Calls a method on the client that invoked the hub method</span></span> |
| `Others` | <span data-ttu-id="4ad94-145">메서드를 호출한 클라이언트를 제외한 모든 연결 된 클라이언트에서 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-145">Calls a method on all connected clients except the client that invoked the method</span></span> |


<span data-ttu-id="4ad94-146">`Hub.Clients` 또한 다음 메서드를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-146">`Hub.Clients` also contains the following methods:</span></span>

| <span data-ttu-id="4ad94-147">메서드</span><span class="sxs-lookup"><span data-stu-id="4ad94-147">Method</span></span> | <span data-ttu-id="4ad94-148">설명</span><span class="sxs-lookup"><span data-stu-id="4ad94-148">Description</span></span> |
| ------ | ----------- |
| `AllExcept` | <span data-ttu-id="4ad94-149">지정 된 연결을 제외 하 고 연결 된 모든 클라이언트에서 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-149">Calls a method on all connected clients except for the specified connections</span></span> |
| `Client` | <span data-ttu-id="4ad94-150">특정 연결 된 클라이언트에서 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-150">Calls a method on a specific connected client</span></span> |
| `Clients` | <span data-ttu-id="4ad94-151">특정 연결 된 클라이언트에서 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-151">Calls a method on specific connected clients</span></span> |
| `Group` | <span data-ttu-id="4ad94-152">지정된 된 그룹의 모든 연결에 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-152">Calls a method to all connections in the specified group</span></span>  |
| `GroupExcept` | <span data-ttu-id="4ad94-153">지정된 된 연결을 제외 하 고 지정된 된 그룹의 모든 연결에 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-153">Calls a method to all connections in the specified group, except the specified connections</span></span> |
| `Groups` | <span data-ttu-id="4ad94-154">연결의 여러 그룹에 메서드를 호출</span><span class="sxs-lookup"><span data-stu-id="4ad94-154">Calls a method to multiple groups of connections</span></span>  |
| `OthersInGroup` | <span data-ttu-id="4ad94-155">허브 메서드를 호출 하는 클라이언트를 제외한 연결 그룹에 메서드를 호출</span><span class="sxs-lookup"><span data-stu-id="4ad94-155">Calls a method to a group of connections, excluding the client that invoked the hub method</span></span>  |
| `User` | <span data-ttu-id="4ad94-156">특정 사용자와 관련 된 모든 연결 하는 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-156">Calls a method to all connections associated with a specific user</span></span> |
| `Users` | <span data-ttu-id="4ad94-157">지정된 된 사용자와 관련 된 모든 연결 하는 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-157">Calls a method to all connections associated with the specified users</span></span> |

<span data-ttu-id="4ad94-158">앞의 표에 각 메서드나 속성 개체를 반환을 `SendAsync` 메서드.</span><span class="sxs-lookup"><span data-stu-id="4ad94-158">Each property or method in the preceding tables returns an object with a `SendAsync` method.</span></span> <span data-ttu-id="4ad94-159">`SendAsync` 메서드를 사용 하면 이름 및 클라이언트 메서드 호출의 매개 변수를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-159">The `SendAsync` method allows you to supply the name and parameters of the client method to call.</span></span>

## <a name="send-messages-to-clients"></a><span data-ttu-id="4ad94-160">클라이언트에 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="4ad94-160">Send messages to clients</span></span>

<span data-ttu-id="4ad94-161">특정 클라이언트에 대 한 호출을 하려면 속성을 사용 합니다 `Clients` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-161">To make calls to specific clients, use the properties of the `Clients` object.</span></span> <span data-ttu-id="4ad94-162">다음 예제에서는 `SendMessageToCaller` 메서드 허브 메서드 호출 연결에 메시지를 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-162">In the following example, the `SendMessageToCaller` method demonstrates sending a message to the connection that invoked the hub method.</span></span> <span data-ttu-id="4ad94-163">합니다 `SendMessageToGroups` 메서드에 저장 된 그룹에 메시지를 보냅니다는 `List` 라는 `groups`합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-163">The `SendMessageToGroups` method sends a message to the groups stored in a `List` named `groups`.</span></span>

[!code-csharp[Send messages](hubs/sample/hubs/chathub.cs?range=15-24)]

## <a name="handle-events-for-a-connection"></a><span data-ttu-id="4ad94-164">연결에 대 한 이벤트를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-164">Handle events for a connection</span></span>

<span data-ttu-id="4ad94-165">SignalR 허브 API를 제공 합니다 `OnConnectedAsync` 및 `OnDisconnectedAsync` 가상 메서드를 관리 하 고 연결을 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-165">The SignalR Hubs API provides the `OnConnectedAsync` and `OnDisconnectedAsync` virtual methods to manage and track connections.</span></span> <span data-ttu-id="4ad94-166">재정의 `OnConnectedAsync` 가상 메서드는 클라이언트 그룹에 추가 하는 등 허브에 연결 시 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-166">Override the `OnConnectedAsync` virtual method to perform actions when a client connects to the Hub, such as adding it to a group.</span></span>

[!code-csharp[Handle events](hubs/sample/hubs/chathub.cs?range=26-36)]

## <a name="handle-errors"></a><span data-ttu-id="4ad94-167">오류 처리</span><span class="sxs-lookup"><span data-stu-id="4ad94-167">Handle errors</span></span>

<span data-ttu-id="4ad94-168">허브 메서드에서 throw 된 예외는 메서드를 호출한 클라이언트에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-168">Exceptions thrown in your hub methods are sent to the client that invoked the method.</span></span> <span data-ttu-id="4ad94-169">JavaScript 클라이언트에는 `invoke` 메서드가 반환 되는 [JavaScript 프라미스](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Using_promises)합니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-169">On the JavaScript client, the `invoke` method returns a [JavaScript Promise](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Using_promises).</span></span> <span data-ttu-id="4ad94-170">프라미스를 통해 연결 된 클라이언트의 오류 처리기를 받을 때 `catch`, 호출 되 고 javascript 전달 `Error` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="4ad94-170">When the client receives an error with a handler attached to the promise using `catch`, it's invoked and passed as a JavaScript `Error` object.</span></span>

[!code-javascript[Error](hubs/sample/wwwroot/js/chat.js?range=23)]

## <a name="related-resources"></a><span data-ttu-id="4ad94-171">관련 참고 자료</span><span class="sxs-lookup"><span data-stu-id="4ad94-171">Related resources</span></span>

* [<span data-ttu-id="4ad94-172">ASP.NET Core SignalR에 대 한 소개</span><span class="sxs-lookup"><span data-stu-id="4ad94-172">Intro to ASP.NET Core SignalR</span></span>](xref:signalr/introduction)
* [<span data-ttu-id="4ad94-173">JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="4ad94-173">JavaScript client</span></span>](xref:signalr/javascript-client)
* [<span data-ttu-id="4ad94-174">Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="4ad94-174">Publish to Azure</span></span>](xref:signalr/publish-to-azure-web-app)
