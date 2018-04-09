---
title: ASP.NET Core SignalR 허브를 사용 합니다.
author: rachelappel
description: ASP.NET Core SignalR 허브를 사용 하는 방법을 알아봅니다.
manager: wpickett
ms.author: rachelap
ms.custom: mvc
ms.date: 03/30/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: signalr/hubs
ms.openlocfilehash: 73397ba6951f2752653575920bdf739439874366
ms.sourcegitcommit: 7d02ca5f5ddc2ca3eb0258fdd6996fbf538c129a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/03/2018
---
# <a name="use-hubs-in-signalr-for-aspnet-core"></a><span data-ttu-id="ec72d-103">ASP.NET Core에서 SignalR 허브를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="ec72d-103">Use hubs in SignalR for ASP.NET Core</span></span>

<span data-ttu-id="ec72d-104">여 [Rachel Appel](https://twitter.com/rachelappel) 및 [Kevin Griffin](https://twitter.com/1kevgriff)</span><span class="sxs-lookup"><span data-stu-id="ec72d-104">By [Rachel Appel](https://twitter.com/rachelappel) and [Kevin Griffin](https://twitter.com/1kevgriff)</span></span>

## <a name="what-is-a-signalr-hub"></a><span data-ttu-id="ec72d-105">SignalR 허브 이란</span><span class="sxs-lookup"><span data-stu-id="ec72d-105">What is a SignalR hub</span></span>

<span data-ttu-id="ec72d-106">SignalR 허브 API를 사용 하면 서버에서 연결 된 클라이언트에서 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-106">The SignalR Hubs API enables you to call methods on connected clients from the server.</span></span> <span data-ttu-id="ec72d-107">서버 코드에서 클라이언트에 의해 호출 되는 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-107">In the server code, you define methods that are called by client.</span></span> <span data-ttu-id="ec72d-108">클라이언트 코드는 서버에서 호출 하는 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-108">In the client code, you define methods that are called from the server.</span></span> <span data-ttu-id="ec72d-109">SignalR 하는 모든 실시간 클라이언트-서버 및 서버 클라이언트 통신을 가능 하 게 하는 백그라운드 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-109">SignalR takes care of everything behind the scenes that makes real-time client-to-server and server-to-client communications possible.</span></span>

## <a name="configure-signalr-hubs"></a><span data-ttu-id="ec72d-110">SignalR 허브를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-110">Configure SignalR hubs</span></span>

<span data-ttu-id="ec72d-111">SignalR 미들웨어를 호출 하 여 구성 된 일부 서비스 필요 `services.AddSignalR`합니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-111">The SignalR middleware requires some services, which are configured by calling `services.AddSignalR`.</span></span>

[!code-csharp[Configure service](hubs/sample/startup.cs?range=35)]

<span data-ttu-id="ec72d-112">SignalR 기능에는 ASP.NET Core 응용 프로그램을 추가할 때 호출 하 여 SignalR 경로 설정 `app.UseSignalR` 에 `Startup.Configure` 메서드.</span><span class="sxs-lookup"><span data-stu-id="ec72d-112">When adding SignalR functionality to an ASP.NET Core app, setup SignalR routes by calling `app.UseSignalR` in the `Startup.Configure` method.</span></span>

[!code-csharp[Configure routes to hubs](hubs/sample/startup.cs?range=55-58)]

## <a name="create-and-use-hubs"></a><span data-ttu-id="ec72d-113">만들기 및 허브를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-113">Create and use hubs</span></span>

<span data-ttu-id="ec72d-114">상속 되는 클래스를 선언 하 여 허브를 만들 `Hub`, public 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-114">Create a hub by declaring a class that inherits from `Hub`, and add public methods to it.</span></span> <span data-ttu-id="ec72d-115">클라이언트에서으로 정의 된 메서드를 호출할 수 `public`합니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-115">Clients can call methods that are defined as `public`.</span></span>

[!code-csharp[Create and use hubs](hubs/sample/chathub.cs?range=10-13)]

<span data-ttu-id="ec72d-116">반환 형식 및 C# 메서드에서 마찬가지로 배열 및 복합 형식을 포함 하 여 매개 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-116">You can specify a return type and parameters, including complex types and arrays, as you would in any C# method.</span></span> <span data-ttu-id="ec72d-117">SignalR은 serialization 및 deserialization 복잡 한 개체 및 배열에 매개 변수 및 반환 값을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-117">SignalR handles the serialization and deserialization of complex objects and arrays in your parameters and return values.</span></span>

## <a name="the-clients-object"></a><span data-ttu-id="ec72d-118">클라이언트 개체</span><span class="sxs-lookup"><span data-stu-id="ec72d-118">The Clients object</span></span>

<span data-ttu-id="ec72d-119">각 인스턴스는 `Hub` 클래스 라는 속성이 `Clients` 서버와 클라이언트 간의 통신에 대 한 다음 멤버를 포함 하는:</span><span class="sxs-lookup"><span data-stu-id="ec72d-119">Each instance of the `Hub` class has a property named `Clients` that contains the following members for communication between server and client:</span></span>

| <span data-ttu-id="ec72d-120">속성</span><span class="sxs-lookup"><span data-stu-id="ec72d-120">Property</span></span> | <span data-ttu-id="ec72d-121">설명</span><span class="sxs-lookup"><span data-stu-id="ec72d-121">Description</span></span> |
| ------ | ----------- |
| `All` | <span data-ttu-id="ec72d-122">연결 된 모든 클라이언트에서 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-122">Calls a method on all connected clients</span></span> |
| `Caller` | <span data-ttu-id="ec72d-123">클라이언트 허브 메서드를 호출한 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-123">Calls a method on the client that invoked the hub method</span></span> |
| `Others` | <span data-ttu-id="ec72d-124">메서드를 호출한 클라이언트를 제외한 모든 연결 된 클라이언트에서 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-124">Calls a method on all connected clients except the client that invoked the method</span></span> |

<span data-ttu-id="ec72d-125">또한는 `Hub` 클래스에는 다음과 같은 메서드가 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-125">Additionally, the `Hub` class contains the following methods:</span></span>

| <span data-ttu-id="ec72d-126">메서드</span><span class="sxs-lookup"><span data-stu-id="ec72d-126">Method</span></span> | <span data-ttu-id="ec72d-127">설명</span><span class="sxs-lookup"><span data-stu-id="ec72d-127">Description</span></span> |
| ------ | ----------- |
| `AllExcept` | <span data-ttu-id="ec72d-128">지정된 된 연결을 제외한 모든 연결 된 클라이언트에서 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-128">Calls a method on all connected clients except for the specified connections</span></span> |
| `Client` | <span data-ttu-id="ec72d-129">특정 연결 된 클라이언트에 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-129">Calls a method on a specific connected client</span></span> |
| `Clients` | <span data-ttu-id="ec72d-130">특정 연결 된 클라이언트에서 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-130">Calls a method on specific connected clients</span></span> |
| `Group` | <span data-ttu-id="ec72d-131">지정된 된 그룹의 모든 연결에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-131">Sends a message to all connections in the specified group</span></span>  |
| `GroupExcept` | <span data-ttu-id="ec72d-132">지정된 된 연결을 제외 하 고 지정된 된 그룹의 모든 연결에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-132">Sends a message to all connections in the specified group, except the specified connections</span></span> |
| `Groups` | <span data-ttu-id="ec72d-133">연결의 여러 그룹에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-133">Sends a message to multiple groups of connections</span></span>  |
| `OthersInGroup` | <span data-ttu-id="ec72d-134">그룹 허브 메서드를 호출한 클라이언트 제외 하 고 연결에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-134">Sends a message to a group of connections, excluding the client that invoked the hub method</span></span>  |
| `User` | <span data-ttu-id="ec72d-135">특정 사용자와 관련 된 모든 연결에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-135">Sends a message to all connections associated with a specific user</span></span> |
| `Users` | <span data-ttu-id="ec72d-136">지정된 된 사용자와 관련 된 모든 연결에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-136">Sends a message to all connections associated with the specified users</span></span> |

<span data-ttu-id="ec72d-137">위 표의 각 메서드나 속성 반환을 가진 개체는 `SendAsync` 메서드.</span><span class="sxs-lookup"><span data-stu-id="ec72d-137">Each property or method in the preceding tables returns an object with a `SendAsync` method.</span></span> <span data-ttu-id="ec72d-138">`SendAsync` 메서드 이름 및 클라이언트 메서드를 호출할 매개 변수를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-138">The `SendAsync` method allows you to supply the name and parameters of the client method to call.</span></span>

## <a name="send-messages-to-clients"></a><span data-ttu-id="ec72d-139">클라이언트에 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="ec72d-139">Send messages to clients</span></span>

<span data-ttu-id="ec72d-140">특정 클라이언트에 대 한 호출을 하려면 속성을 사용 하 여는 `Clients` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-140">To make calls to specific clients, use the properties of the `Clients` object.</span></span> <span data-ttu-id="ec72d-141">다음 예제에서는 다음에는 `SendMessageToCaller` 메서드 허브 메서드를 호출 하는 연결으로 메시지를 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-141">In the following In the following example, the `SendMessageToCaller` method demonstrates sending a message to the connection that invoked the hub method.</span></span> <span data-ttu-id="ec72d-142">`SendMessageToGroups` 메서드에 저장 된 그룹에 메시지를 보냅니다는 `List` 라는 `groups`합니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-142">The `SendMessageToGroups` method sends a message to the groups stored in a `List` named `groups`.</span></span>

[!code-csharp[Send messages](hubs/sample/chathub.cs?range=15-24)]

## <a name="handle-events-for-a-connection"></a><span data-ttu-id="ec72d-143">연결에 대 한 이벤트를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-143">Handle events for a connection</span></span>

<span data-ttu-id="ec72d-144">SignalR 허브 API를 제공는 `OnConnectedAsync` 및 `OnDisconnectedAsync` 가상 메서드 관리 하 고 연결을 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-144">The SignalR Hubs API provides the `OnConnectedAsync` and `OnDisconnectedAsync` virtual methods to manage and track connections.</span></span> <span data-ttu-id="ec72d-145">재정의 `OnConnectedAsync` 가상 메서드는 클라이언트 그룹에 추가 하는 방법과 같은 허브에 연결할 때 동작을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-145">Override the `OnConnectedAsync` virtual method to perform actions when a client connects to the Hub, such as adding it to a group.</span></span>

[!code-csharp[Handle events](hubs/sample/chathub.cs?range=26-30)]

## <a name="handle-errors"></a><span data-ttu-id="ec72d-146">오류 처리</span><span class="sxs-lookup"><span data-stu-id="ec72d-146">Handle errors</span></span>

<span data-ttu-id="ec72d-147">허브 메서드에서 throw 된 예외는 메서드를 호출한 클라이언트에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-147">Exceptions thrown in your hub methods are sent to the client that invoked the method.</span></span> <span data-ttu-id="ec72d-148">JavaScript 클라이언트는 `invoke` 메서드가 반환 되는 [JavaScript 프로 미스](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Using_promises)합니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-148">On the JavaScript client, the `invoke` method returns a [JavaScript Promise](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Using_promises).</span></span> <span data-ttu-id="ec72d-149">사용 하 여 프라미스에 연결 된 클라이언트의 오류 처리기를 받을 때 `catch`, 호출 개이고는 javascript에 전달 된 `Error` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="ec72d-149">When the client receives an error with a handler attached to the promise using `catch`, it's invoked and passed as a JavaScript `Error` object.</span></span>

[!code-javascript[Error](hubs/sample/chat.js?range=20)]
[!code-javascript[Error](hubs/sample/chat.js?range=16-18)]

## <a name="related-resources"></a><span data-ttu-id="ec72d-150">관련 참고 자료</span><span class="sxs-lookup"><span data-stu-id="ec72d-150">Related resources</span></span>

[<span data-ttu-id="ec72d-151">ASP.NET Core SignalR 소개</span><span class="sxs-lookup"><span data-stu-id="ec72d-151">Intro to ASP.NET Core SignalR</span></span>](xref:signalr/introduction)