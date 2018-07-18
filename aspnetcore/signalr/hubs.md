---
title: ASP.NET Core SignalR에서 허브를 사용 합니다.
author: tdykstra
description: ASP.NET Core SignalR에서 허브를 사용 하는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 05/01/2018
uid: signalr/hubs
ms.openlocfilehash: be39666373e2b099054bb71f4a7fcf17aeb9a01c
ms.sourcegitcommit: 3ca527f27c88cfc9d04688db5499e372fbc2c775
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39095283"
---
# <a name="use-hubs-in-signalr-for-aspnet-core"></a><span data-ttu-id="cf79d-103">SignalR에서 허브를 사용 하 여 ASP.NET Core에 대 한</span><span class="sxs-lookup"><span data-stu-id="cf79d-103">Use hubs in SignalR for ASP.NET Core</span></span>

<span data-ttu-id="cf79d-104">하 여 [Rachel Appel](https://twitter.com/rachelappel) 고 [Kevin Griffin](https://twitter.com/1kevgriff)</span><span class="sxs-lookup"><span data-stu-id="cf79d-104">By [Rachel Appel](https://twitter.com/rachelappel) and [Kevin Griffin](https://twitter.com/1kevgriff)</span></span>

<span data-ttu-id="cf79d-105">[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/hubs/sample/ ) [(다운로드 하는 방법)](xref:tutorials/index#how-to-download-a-sample)</span><span class="sxs-lookup"><span data-stu-id="cf79d-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/hubs/sample/ ) [(how to download)](xref:tutorials/index#how-to-download-a-sample)</span></span>

## <a name="what-is-a-signalr-hub"></a><span data-ttu-id="cf79d-106">SignalR 허브 란</span><span class="sxs-lookup"><span data-stu-id="cf79d-106">What is a SignalR hub</span></span>

<span data-ttu-id="cf79d-107">SignalR 허브 API를 사용 하면 서버에서 연결 된 클라이언트에서 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-107">The SignalR Hubs API enables you to call methods on connected clients from the server.</span></span> <span data-ttu-id="cf79d-108">서버 코드를 클라이언트에서 호출 된 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-108">In the server code, you define methods that are called by client.</span></span> <span data-ttu-id="cf79d-109">클라이언트 코드를 서버에서 호출 된 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-109">In the client code, you define methods that are called from the server.</span></span> <span data-ttu-id="cf79d-110">SignalR은 클라이언트와 서버 간 및 서버와 클라이언트 간 실시간 통신을 가능 하 게 하는 백그라운드에서 모든 부분을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-110">SignalR takes care of everything behind the scenes that makes real-time client-to-server and server-to-client communications possible.</span></span>

## <a name="configure-signalr-hubs"></a><span data-ttu-id="cf79d-111">SignalR 허브를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-111">Configure SignalR hubs</span></span>

<span data-ttu-id="cf79d-112">SignalR 미들웨어를 호출 하 여 구성 된 일부 서비스의 경우 필요한 `services.AddSignalR`합니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-112">The SignalR middleware requires some services, which are configured by calling `services.AddSignalR`.</span></span>

[!code-csharp[Configure service](hubs/sample/startup.cs?range=38)]

<span data-ttu-id="cf79d-113">ASP.NET Core 앱에 SignalR 기능을 추가 하는 경우 호출 하 여 SignalR 경로 설정 `app.UseSignalR` 에 `Startup.Configure` 메서드.</span><span class="sxs-lookup"><span data-stu-id="cf79d-113">When adding SignalR functionality to an ASP.NET Core app, setup SignalR routes by calling `app.UseSignalR` in the `Startup.Configure` method.</span></span>

[!code-csharp[Configure routes to hubs](hubs/sample/startup.cs?range=57-60)]

## <a name="create-and-use-hubs"></a><span data-ttu-id="cf79d-114">만들고 허브를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-114">Create and use hubs</span></span>

<span data-ttu-id="cf79d-115">상속 되는 클래스를 선언 하 여 허브를 만들 `Hub`, public 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-115">Create a hub by declaring a class that inherits from `Hub`, and add public methods to it.</span></span> <span data-ttu-id="cf79d-116">클라이언트도 정의 된 메서드를 호출할 수 `public`입니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-116">Clients can call methods that are defined as `public`.</span></span>

[!code-csharp[Create and use hubs](hubs/sample/hubs/chathub.cs?range=8-37)]

<span data-ttu-id="cf79d-117">반환 형식 및 C# 메서드에서 마찬가지로 복합 형식 및 배열 등 매개 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-117">You can specify a return type and parameters, including complex types and arrays, as you would in any C# method.</span></span> <span data-ttu-id="cf79d-118">SignalR은 serialization 및 deserialization 복잡 한 개체 및 배열 매개 변수 및 반환 값을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-118">SignalR handles the serialization and deserialization of complex objects and arrays in your parameters and return values.</span></span>

## <a name="the-clients-object"></a><span data-ttu-id="cf79d-119">클라이언트 개체</span><span class="sxs-lookup"><span data-stu-id="cf79d-119">The Clients object</span></span>

<span data-ttu-id="cf79d-120">각 인스턴스는 `Hub` 클래스 라는 속성이 `Clients` 서버와 클라이언트 간의 통신에 대 한 다음 멤버를 포함 하는:</span><span class="sxs-lookup"><span data-stu-id="cf79d-120">Each instance of the `Hub` class has a property named `Clients` that contains the following members for communication between server and client:</span></span>

| <span data-ttu-id="cf79d-121">속성</span><span class="sxs-lookup"><span data-stu-id="cf79d-121">Property</span></span> | <span data-ttu-id="cf79d-122">설명</span><span class="sxs-lookup"><span data-stu-id="cf79d-122">Description</span></span> |
| ------ | ----------- |
| `All` | <span data-ttu-id="cf79d-123">연결 된 모든 클라이언트에서 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-123">Calls a method on all connected clients</span></span> |
| `Caller` | <span data-ttu-id="cf79d-124">허브 메서드를 호출 하는 클라이언트의 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-124">Calls a method on the client that invoked the hub method</span></span> |
| `Others` | <span data-ttu-id="cf79d-125">메서드를 호출한 클라이언트를 제외한 모든 연결 된 클라이언트에서 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-125">Calls a method on all connected clients except the client that invoked the method</span></span> |


<span data-ttu-id="cf79d-126">또한 `Hub.Clients` 다음 메서드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-126">Additionally, `Hub.Clients` contains the following methods:</span></span>

| <span data-ttu-id="cf79d-127">메서드</span><span class="sxs-lookup"><span data-stu-id="cf79d-127">Method</span></span> | <span data-ttu-id="cf79d-128">설명</span><span class="sxs-lookup"><span data-stu-id="cf79d-128">Description</span></span> |
| ------ | ----------- |
| `AllExcept` | <span data-ttu-id="cf79d-129">지정 된 연결을 제외 하 고 연결 된 모든 클라이언트에서 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-129">Calls a method on all connected clients except for the specified connections</span></span> |
| `Client` | <span data-ttu-id="cf79d-130">특정 연결 된 클라이언트에서 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-130">Calls a method on a specific connected client</span></span> |
| `Clients` | <span data-ttu-id="cf79d-131">특정 연결 된 클라이언트에서 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-131">Calls a method on specific connected clients</span></span> |
| `Group` | <span data-ttu-id="cf79d-132">지정된 된 그룹의 모든 연결에 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-132">Calls a method to all connections in the specified group</span></span>  |
| `GroupExcept` | <span data-ttu-id="cf79d-133">지정된 된 연결을 제외 하 고 지정된 된 그룹의 모든 연결에 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-133">Calls a method to all connections in the specified group, except the specified connections</span></span> |
| `Groups` | <span data-ttu-id="cf79d-134">연결의 여러 그룹에 메서드를 호출</span><span class="sxs-lookup"><span data-stu-id="cf79d-134">Calls a method to multiple groups of connections</span></span>  |
| `OthersInGroup` | <span data-ttu-id="cf79d-135">허브 메서드를 호출 하는 클라이언트를 제외한 연결 그룹에 메서드를 호출</span><span class="sxs-lookup"><span data-stu-id="cf79d-135">Calls a method to a group of connections, excluding the client that invoked the hub method</span></span>  |
| `User` | <span data-ttu-id="cf79d-136">특정 사용자와 관련 된 모든 연결 하는 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-136">Calls a method to all connections associated with a specific user</span></span> |
| `Users` | <span data-ttu-id="cf79d-137">지정된 된 사용자와 관련 된 모든 연결 하는 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-137">Calls a method to all connections associated with the specified users</span></span> |

<span data-ttu-id="cf79d-138">앞의 표에 각 메서드나 속성 개체를 반환을 `SendAsync` 메서드.</span><span class="sxs-lookup"><span data-stu-id="cf79d-138">Each property or method in the preceding tables returns an object with a `SendAsync` method.</span></span> <span data-ttu-id="cf79d-139">`SendAsync` 메서드를 사용 하면 이름 및 클라이언트 메서드 호출의 매개 변수를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-139">The `SendAsync` method allows you to supply the name and parameters of the client method to call.</span></span>

## <a name="send-messages-to-clients"></a><span data-ttu-id="cf79d-140">클라이언트에 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="cf79d-140">Send messages to clients</span></span>

<span data-ttu-id="cf79d-141">특정 클라이언트에 대 한 호출을 하려면 속성을 사용 합니다 `Clients` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-141">To make calls to specific clients, use the properties of the `Clients` object.</span></span> <span data-ttu-id="cf79d-142">다음 예제에서는 `SendMessageToCaller` 메서드 허브 메서드 호출 연결에 메시지를 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-142">In the following example, the `SendMessageToCaller` method demonstrates sending a message to the connection that invoked the hub method.</span></span> <span data-ttu-id="cf79d-143">합니다 `SendMessageToGroups` 메서드에 저장 된 그룹에 메시지를 보냅니다는 `List` 라는 `groups`합니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-143">The `SendMessageToGroups` method sends a message to the groups stored in a `List` named `groups`.</span></span>

[!code-csharp[Send messages](hubs/sample/hubs/chathub.cs?range=15-24)]

## <a name="handle-events-for-a-connection"></a><span data-ttu-id="cf79d-144">연결에 대 한 이벤트를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-144">Handle events for a connection</span></span>

<span data-ttu-id="cf79d-145">SignalR 허브 API를 제공 합니다 `OnConnectedAsync` 및 `OnDisconnectedAsync` 가상 메서드를 관리 하 고 연결을 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-145">The SignalR Hubs API provides the `OnConnectedAsync` and `OnDisconnectedAsync` virtual methods to manage and track connections.</span></span> <span data-ttu-id="cf79d-146">재정의 `OnConnectedAsync` 가상 메서드는 클라이언트 그룹에 추가 하는 등 허브에 연결 시 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-146">Override the `OnConnectedAsync` virtual method to perform actions when a client connects to the Hub, such as adding it to a group.</span></span>

[!code-csharp[Handle events](hubs/sample/hubs/chathub.cs?range=26-36)]

## <a name="handle-errors"></a><span data-ttu-id="cf79d-147">오류 처리</span><span class="sxs-lookup"><span data-stu-id="cf79d-147">Handle errors</span></span>

<span data-ttu-id="cf79d-148">허브 메서드에서 throw 된 예외는 메서드를 호출한 클라이언트에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-148">Exceptions thrown in your hub methods are sent to the client that invoked the method.</span></span> <span data-ttu-id="cf79d-149">JavaScript 클라이언트에는 `invoke` 메서드가 반환 되는 [JavaScript 프라미스](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Using_promises)합니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-149">On the JavaScript client, the `invoke` method returns a [JavaScript Promise](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Using_promises).</span></span> <span data-ttu-id="cf79d-150">프라미스를 통해 연결 된 클라이언트의 오류 처리기를 받을 때 `catch`, 호출 되 고 javascript 전달 `Error` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="cf79d-150">When the client receives an error with a handler attached to the promise using `catch`, it's invoked and passed as a JavaScript `Error` object.</span></span>

[!code-javascript[Error](hubs/sample/wwwroot/js/chat.js?range=23)]

## <a name="related-resources"></a><span data-ttu-id="cf79d-151">관련 참고 자료</span><span class="sxs-lookup"><span data-stu-id="cf79d-151">Related resources</span></span>

* [<span data-ttu-id="cf79d-152">ASP.NET Core SignalR에 대 한 소개</span><span class="sxs-lookup"><span data-stu-id="cf79d-152">Intro to ASP.NET Core SignalR</span></span>](xref:signalr/introduction)
* [<span data-ttu-id="cf79d-153">JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="cf79d-153">JavaScript client</span></span>](xref:signalr/javascript-client)
* [<span data-ttu-id="cf79d-154">Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="cf79d-154">Publish to Azure</span></span>](xref:signalr/publish-to-azure-web-app)
