---
title: ASP.NET Core SignalR에서 허브 사용하기
author: tdykstra
description: ASP.NET Core SignalR에서 허브를 사용하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 09/12/2018
uid: signalr/hubs
ms.openlocfilehash: 27aedc5b2f2060d961070fbd1ff5304eaa3956d1
ms.sourcegitcommit: fc7eb4243188950ae1f1b52669edc007e9d0798d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2018
ms.locfileid: "51225358"
---
# <a name="use-hubs-in-signalr-for-aspnet-core"></a><span data-ttu-id="e3026-103">ASP.NET Core SignalR에서 허브 사용하기</span><span class="sxs-lookup"><span data-stu-id="e3026-103">Use hubs in SignalR for ASP.NET Core</span></span>

<span data-ttu-id="e3026-104">작성자: [Rachel Appel](https://twitter.com/rachelappel) 및 [Kevin Griffin](https://twitter.com/1kevgriff)</span><span class="sxs-lookup"><span data-stu-id="e3026-104">By [Rachel Appel](https://twitter.com/rachelappel) and [Kevin Griffin](https://twitter.com/1kevgriff)</span></span>

<span data-ttu-id="e3026-105">[샘플 코드 보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/hubs/sample/ ) [(다운로드 방법)](xref:index#how-to-download-a-sample)</span><span class="sxs-lookup"><span data-stu-id="e3026-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/hubs/sample/ ) [(how to download)](xref:index#how-to-download-a-sample)</span></span>

## <a name="what-is-a-signalr-hub"></a><span data-ttu-id="e3026-106">SignalR 허브 기능</span><span class="sxs-lookup"><span data-stu-id="e3026-106">What is a SignalR hub</span></span>

<span data-ttu-id="e3026-107">SignalR 허브 API를 사용하면 서버에서 연결된 클라이언트의 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-107">The SignalR Hubs API enables you to call methods on connected clients from the server.</span></span> <span data-ttu-id="e3026-108">서버 코드는 클라이언트에 의해서 호출되는 메서드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-108">In the server code, you define methods that are called by client.</span></span> <span data-ttu-id="e3026-109">클라이언트 코드는 서버에 의해서 호출되는 메서드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-109">In the client code, you define methods that are called from the server.</span></span> <span data-ttu-id="e3026-110">SignalR은 클라이언트에서 서버로 그리고 서버에서 클라이언트로 실시간 통신을 가능하게 만들어주는 모든 작업을 내부적으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-110">SignalR takes care of everything behind the scenes that makes real-time client-to-server and server-to-client communications possible.</span></span>

## <a name="configure-signalr-hubs"></a><span data-ttu-id="e3026-111">SignalR 허브 구성하기</span><span class="sxs-lookup"><span data-stu-id="e3026-111">Configure SignalR hubs</span></span>

<span data-ttu-id="e3026-112">SignalR 미들웨어에는 `services.AddSignalR` 호출을 통해 구성되는 몇 가지 서비스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-112">The SignalR middleware requires some services, which are configured by calling `services.AddSignalR`.</span></span>

[!code-csharp[Configure service](hubs/sample/startup.cs?range=38)]

<span data-ttu-id="e3026-113">ASP.NET Core 앱에 SignalR 기능을 추가할 때, `Startup.Configure` 메서드에서 `app.UseSignalR`을 호출하여 SignalR 경로를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-113">When adding SignalR functionality to an ASP.NET Core app, setup SignalR routes by calling `app.UseSignalR` in the `Startup.Configure` method.</span></span>

[!code-csharp[Configure routes to hubs](hubs/sample/startup.cs?range=57-60)]

## <a name="create-and-use-hubs"></a><span data-ttu-id="e3026-114">허브 생성 및 사용하기</span><span class="sxs-lookup"><span data-stu-id="e3026-114">Create and use hubs</span></span>

<span data-ttu-id="e3026-115">`Hub`를 상속받는 클래스를 선언하여 허브를 생성하고, 이 허브에 public 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-115">Create a hub by declaring a class that inherits from `Hub`, and add public methods to it.</span></span> <span data-ttu-id="e3026-116">클라이언트는 이렇게 `public`으로 정의된 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-116">Clients can call methods that are defined as `public`.</span></span>

[!code-csharp[Create and use hubs](hubs/sample/hubs/chathub.cs?range=8-37)]

<span data-ttu-id="e3026-117">일반적인 C# 메서드와 마찬가지로 복합 형식 및 배열 등을 사용해서 반환 형식과 매개 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-117">You can specify a return type and parameters, including complex types and arrays, as you would in any C# method.</span></span> <span data-ttu-id="e3026-118">SignalR은 매개 변수 및 반환 값에 사용되는 복합 개체 및 배열의 직렬화와 역직렬화를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-118">SignalR handles the serialization and deserialization of complex objects and arrays in your parameters and return values.</span></span>

> [!NOTE]
> <span data-ttu-id="e3026-119">일시적인 hubs 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-119">Hubs are transient:</span></span>
> * <span data-ttu-id="e3026-120">허브 클래스의 속성에서 상태를 저장 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="e3026-120">Don't store state in a property on the hub class.</span></span> <span data-ttu-id="e3026-121">허브 메서드 호출 마다 새 허브 인스턴스에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-121">Every hub method call is executed on a new hub instance.</span></span>  
> * <span data-ttu-id="e3026-122">사용 하 여 `await` 활성 상태로 유지 하는 허브에 의존 하는 비동기 메서드를 호출할 때.</span><span class="sxs-lookup"><span data-stu-id="e3026-122">Use `await` when calling asynchronous methods that depend on the hub staying alive.</span></span> <span data-ttu-id="e3026-123">예를 들어,와 같은 메서드 `Clients.All.SendAsync(...)` 없이 호출 되는 경우 실패할 수 있습니다 `await` 허브 메서드를 완료 하기 전에 `SendAsync` 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-123">For example, a method such as `Clients.All.SendAsync(...)` can fail if it's called without `await` and the hub method completes before `SendAsync` finishes.</span></span>

## <a name="the-context-object"></a><span data-ttu-id="e3026-124">Context 개체</span><span class="sxs-lookup"><span data-stu-id="e3026-124">The Context object</span></span>

<span data-ttu-id="e3026-125">`Hub` 클래스에는 연결 정보와 함께 다음 속성들을 포함하고 있는 `Context` 속성이 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-125">The `Hub` class has a `Context` property that contains the following properties with information about the connection:</span></span>

| <span data-ttu-id="e3026-126">속성</span><span class="sxs-lookup"><span data-stu-id="e3026-126">Property</span></span> | <span data-ttu-id="e3026-127">설명</span><span class="sxs-lookup"><span data-stu-id="e3026-127">Description</span></span> |
| ------ | ----------- |
| `ConnectionId` | <span data-ttu-id="e3026-128">SignalR에 의해 할당된 연결의 고유 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-128">Gets the unique ID for the connection, assigned by SignalR.</span></span> <span data-ttu-id="e3026-129">각 연결마다 하나의 연결 ID가 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-129">There is one connection ID for each connection.</span></span>|
| `UserIdentifier` | <span data-ttu-id="e3026-130">가져옵니다 합니다 [사용자 식별자](xref:signalr/groups)를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-130">Gets the [user identifier](xref:signalr/groups).</span></span> <span data-ttu-id="e3026-131">SignalR은 기본적으로 연결과 관련된 `ClaimTypes.NameIdentifier` 의 `ClaimsPrincipal` 을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-131">By default, SignalR uses the `ClaimTypes.NameIdentifier` from the `ClaimsPrincipal` associated with the connection as the user identifier.</span></span> |
| `User` | <span data-ttu-id="e3026-132">현재 사용자와 관련된 `ClaimsPrincipal` 현재 사용자와 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-132">Gets the `ClaimsPrincipal` associated with the current user.</span></span> |
| `Items` | <span data-ttu-id="e3026-133">연결의 범위 내에서 데이터 공유를 위해 사용할 수 있는 키/값 컬렉션을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-133">Gets a key/value collection that can be used to share data within the scope of this connection.</span></span> <span data-ttu-id="e3026-134">이 컬렉션에 데이터를 저장할 수 있으며 저장된 데이터는 연결에 대한 다른 허브 메서드들의 호출 간에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-134">Data can be stored in this collection and it will persist for the connection across different hub method invocations.</span></span> |
| `Features` | <span data-ttu-id="e3026-135">연결에서 사용할 수 있는 기능들의 컬렉션을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-135">Gets the collection of features available on the connection.</span></span> <span data-ttu-id="e3026-136">이 컬렉션은 대부분의 시나리오에서 사용되지 않기 때문에, 지금은 아직 자세히 문서화되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-136">For now, this collection isn't needed in most scenarios, so it isn't documented in detail yet.</span></span> |
| `ConnectionAborted` | <span data-ttu-id="e3026-137">연결이 중단될 때 이를 알려주는 `CancellationToken` 을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-137">Gets a `CancellationToken` that notifies when the connection is aborted.</span></span> |

<span data-ttu-id="e3026-138">`Hub.Context`는 다음 메서드도 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-138">`Hub.Context` also contains the following methods:</span></span>

| <span data-ttu-id="e3026-139">메서드</span><span class="sxs-lookup"><span data-stu-id="e3026-139">Method</span></span> | <span data-ttu-id="e3026-140">설명</span><span class="sxs-lookup"><span data-stu-id="e3026-140">Description</span></span> |
| ------ | ----------- |
| `GetHttpContext` | <span data-ttu-id="e3026-141">연결에 대한 `HttpContext`를 반환하거나, 연결이 HTTP 요청과 연관되지 않은 경우 `null`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-141">Returns the `HttpContext` for the connection, or `null` if the connection is not associated with an HTTP request.</span></span> <span data-ttu-id="e3026-142">HTTP 연결에서 HTTP 헤더 및 쿼리 문자열 같은 정보를 가져오기 위해 이 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-142">For HTTP connections, you can use this method to get information such as HTTP headers and query strings.</span></span> |
| `Abort` | <span data-ttu-id="e3026-143">연결을 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-143">Aborts the connection.</span></span> |

## <a name="the-clients-object"></a><span data-ttu-id="e3026-144">Clients 개체</span><span class="sxs-lookup"><span data-stu-id="e3026-144">The Clients object</span></span>

<span data-ttu-id="e3026-145">`Hub` 클래스에는 서버와 클라이언트 간의 통신을 위한 다음 속성들을 포함하고 있는 `Clients` 속성이 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-145">The `Hub` class has a `Clients` property that contains the following properties for communication between server and client:</span></span>

| <span data-ttu-id="e3026-146">속성</span><span class="sxs-lookup"><span data-stu-id="e3026-146">Property</span></span> | <span data-ttu-id="e3026-147">설명</span><span class="sxs-lookup"><span data-stu-id="e3026-147">Description</span></span> |
| ------ | ----------- |
| `All` | <span data-ttu-id="e3026-148">연결된 모든 클라이언트에서 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-148">Calls a method on all connected clients</span></span> |
| `Caller` | <span data-ttu-id="e3026-149">해당 허브 메서드를 호출한 클라이언트에서 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-149">Calls a method on the client that invoked the hub method</span></span> |
| `Others` | <span data-ttu-id="e3026-150">메서드를 호출한 클라이언트를 제외한 모든 연결된 클라이언트에서 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-150">Calls a method on all connected clients except the client that invoked the method</span></span> |


<span data-ttu-id="e3026-151">`Hub.Clients`는 다음 메서드도 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-151">`Hub.Clients` also contains the following methods:</span></span>

| <span data-ttu-id="e3026-152">메서드</span><span class="sxs-lookup"><span data-stu-id="e3026-152">Method</span></span> | <span data-ttu-id="e3026-153">설명</span><span class="sxs-lookup"><span data-stu-id="e3026-153">Description</span></span> |
| ------ | ----------- |
| `AllExcept` | <span data-ttu-id="e3026-154">지정된 연결을 제외한 모든 연결된 클라이언트에서 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-154">Calls a method on all connected clients except for the specified connections</span></span> |
| `Client` | <span data-ttu-id="e3026-155">연결된 특정 클라이언트에서 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-155">Calls a method on a specific connected client</span></span> |
| `Clients` | <span data-ttu-id="e3026-156">연결된 특정 클라이언트들에서 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-156">Calls a method on specific connected clients</span></span> |
| `Group` | <span data-ttu-id="e3026-157">지정된 그룹의 모든 연결에서 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-157">Calls a method to all connections in the specified group</span></span>  |
| `GroupExcept` | <span data-ttu-id="e3026-158">지정된 연결을 제외한, 지정된 그룹의 모든 연결에서 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-158">Calls a method to all connections in the specified group, except the specified connections</span></span> |
| `Groups` | <span data-ttu-id="e3026-159">여러 그룹의 연결에서 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-159">Calls a method to multiple groups of connections</span></span>  |
| `OthersInGroup` | <span data-ttu-id="e3026-160">허브 메서드를 호출한 클라이언트를 제외하고 연결 그룹에서 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-160">Calls a method to a group of connections, excluding the client that invoked the hub method</span></span>  |
| `User` | <span data-ttu-id="e3026-161">특정 사용자와 관련된 모든 연결에서 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-161">Calls a method to all connections associated with a specific user</span></span> |
| `Users` | <span data-ttu-id="e3026-162">지정한 사용자들과 관련된 모든 연결에서 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-162">Calls a method to all connections associated with the specified users</span></span> |

<span data-ttu-id="e3026-163">앞의 표에 설명된 각 속성 및 메서드는 `SendAsync` 메서드를 통해서 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-163">Each property or method in the preceding tables returns an object with a `SendAsync` method.</span></span> <span data-ttu-id="e3026-164">`SendAsync` 메서드를 사용해서 호출할 클라이언트 메서드의 이름 및 매개 변수를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-164">The `SendAsync` method allows you to supply the name and parameters of the client method to call.</span></span>

## <a name="send-messages-to-clients"></a><span data-ttu-id="e3026-165">클라이언트에 메시지 전송하기</span><span class="sxs-lookup"><span data-stu-id="e3026-165">Send messages to clients</span></span>

<span data-ttu-id="e3026-166">특정 클라이언트를 대상으로 호출하려면 `Clients` 개체의 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-166">To make calls to specific clients, use the properties of the `Clients` object.</span></span> <span data-ttu-id="e3026-167">다음 예제에서 `SendMessageToCaller` 메서드는 허브 메서드를 호출한 연결에 메시지를 전송하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-167">In the following example, the `SendMessageToCaller` method demonstrates sending a message to the connection that invoked the hub method.</span></span> <span data-ttu-id="e3026-168">`SendMessageToGroups` 메서드는 `groups`라는 이름의 `List`에 저장된 그룹에 메시지를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-168">The `SendMessageToGroups` method sends a message to the groups stored in a `List` named `groups`.</span></span>

[!code-csharp[Send messages](hubs/sample/hubs/chathub.cs?range=15-24)]

## <a name="strongly-typed-hubs"></a><span data-ttu-id="e3026-169">강력한 형식의 허브</span><span class="sxs-lookup"><span data-stu-id="e3026-169">Strongly typed hubs</span></span>

<span data-ttu-id="e3026-170">`SendAsync` 방식의 단점은 호출된 클라이언트 메서드를 지정하기 위해 매직 문자열에 의존한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-170">A drawback of using `SendAsync` is that it relies on a magic string to specify the client method to be called.</span></span> <span data-ttu-id="e3026-171">이로 인해 메서드 이름의 철자가 잘못되거나 클라이언트에서 누락된 경우 런타임 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-171">This leaves code open to runtime errors if the method name is misspelled or missing from the client.</span></span>

<span data-ttu-id="e3026-172">`SendAsync` 방식의 대안은 <xref:Microsoft.AspNetCore.SignalR.Hub`1>를 이용한 강력한 형식의 `Hub`를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-172">An alternative to using `SendAsync` is to strongly type the `Hub` with <xref:Microsoft.AspNetCore.SignalR.Hub`1>.</span></span> <span data-ttu-id="e3026-173">다음 예제에서 `ChatHub` 클라이언트 메서드들은 `IChatClient`라는 인터페이스로 추출됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-173">In the following example, the `ChatHub` client methods have been extracted out into an interface called `IChatClient`.</span></span>  

[!code-csharp[Interface for IChatClient](hubs/sample/hubs/ichatclient.cs?name=snippet_IChatClient)]

<span data-ttu-id="e3026-174">이 인터페이스를 사용해서 기존의 `ChatHub` 예제를 리팩터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-174">This interface can be used to refactor the preceding `ChatHub` example.</span></span>

[!code-csharp[Strongly typed ChatHub](hubs/sample/hubs/StronglyTypedChatHub.cs?range=8-18,36)]

<span data-ttu-id="e3026-175">`Hub<IChatClient>`를 사용하면 클라이언트 메서드를 컴파일 시점에 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-175">Using `Hub<IChatClient>` enables compile-time checking of the client methods.</span></span> <span data-ttu-id="e3026-176">이렇게 하면 `Hub<T>` 인터페이스에 정의된 메서드만 접근할 수 있기 때문에 마법 문자열 사용으로 인한 문제를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-176">This prevents issues caused by using magic strings, since `Hub<T>` can only provide access to the methods defined in the interface.</span></span>

<span data-ttu-id="e3026-177">강력한 형식의 `Hub<T>`를 사용하면 `SendAsync`를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-177">Using a strongly typed `Hub<T>` disables the ability to use `SendAsync`.</span></span>

## <a name="handle-events-for-a-connection"></a><span data-ttu-id="e3026-178">연결에 관한 이벤트 처리하기</span><span class="sxs-lookup"><span data-stu-id="e3026-178">Handle events for a connection</span></span>

<span data-ttu-id="e3026-179">SignalR 허브 API는 연결을 관리하고 추적하기 위한 `OnConnectedAsync` 및 `OnDisconnectedAsync` 가상 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-179">The SignalR Hubs API provides the `OnConnectedAsync` and `OnDisconnectedAsync` virtual methods to manage and track connections.</span></span> <span data-ttu-id="e3026-180">클라이언트가 허브에 연결할 때, 클라이언트를 그룹에 추가하는 등과 같은 작업을 수행하려면 `OnConnectedAsync` 가상 메서드를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-180">Override the `OnConnectedAsync` virtual method to perform actions when a client connects to the Hub, such as adding it to a group.</span></span>

[!code-csharp[Handle events](hubs/sample/hubs/chathub.cs?range=26-36)]

## <a name="handle-errors"></a><span data-ttu-id="e3026-181">오류 처리</span><span class="sxs-lookup"><span data-stu-id="e3026-181">Handle errors</span></span>

<span data-ttu-id="e3026-182">허브 메서드에서 발생(throw)된 예외는 메서드를 호출한 클라이언트로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-182">Exceptions thrown in your hub methods are sent to the client that invoked the method.</span></span> <span data-ttu-id="e3026-183">JavaScript 클라이언트에서 `invoke` 메서드는 [JavaScript Promise](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Using_promises)를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-183">On the JavaScript client, the `invoke` method returns a [JavaScript Promise](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Using_promises).</span></span> <span data-ttu-id="e3026-184">클라이언트가 `catch`를 통해서 Promise에 첨부된 처리기로 오류를 수신하면, 오류가 JavaScript `Error` 개체로 전달되어 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3026-184">When the client receives an error with a handler attached to the promise using `catch`, it's invoked and passed as a JavaScript `Error` object.</span></span>

[!code-javascript[Error](hubs/sample/wwwroot/js/chat.js?range=23)]

## <a name="related-resources"></a><span data-ttu-id="e3026-185">관련 자료</span><span class="sxs-lookup"><span data-stu-id="e3026-185">Related resources</span></span>

* [<span data-ttu-id="e3026-186">ASP.NET Core SignalR 소개</span><span class="sxs-lookup"><span data-stu-id="e3026-186">Intro to ASP.NET Core SignalR</span></span>](xref:signalr/introduction)
* [<span data-ttu-id="e3026-187">JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="e3026-187">JavaScript client</span></span>](xref:signalr/javascript-client)
* [<span data-ttu-id="e3026-188">Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="e3026-188">Publish to Azure</span></span>](xref:signalr/publish-to-azure-web-app)
