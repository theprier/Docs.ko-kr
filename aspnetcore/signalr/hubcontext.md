---
title: SignalR HubContext
author: rachelappel
description: 알림 허브를 외부에서 클라이언트를 보내기 위한 ASP.NET Core SignalR HubContext 서비스를 사용 하는 방법을 알아봅니다.
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 06/13/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: signalr/hubcontext
ms.openlocfilehash: 79b91a776a38a2e6810cc89ff0b8d15fe836ce66
ms.sourcegitcommit: 9a35906446af7ffd4ccfc18daec38874b5abbef7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35726081"
---
# <a name="send-messages-from-outside-a-hub"></a><span data-ttu-id="f2174-103">허브 외부의 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="f2174-103">Send messages from outside a hub</span></span>

<span data-ttu-id="f2174-104">으로 [Mikael Mengistu](https://twitter.com/MikaelM_12)</span><span class="sxs-lookup"><span data-stu-id="f2174-104">By [Mikael Mengistu](https://twitter.com/MikaelM_12)</span></span>

<span data-ttu-id="f2174-105">SignalR 허브는 SignalR 서버에 연결 된 클라이언트에 메시지를 보내기 위한 핵심 추상화입니다.</span><span class="sxs-lookup"><span data-stu-id="f2174-105">The SignalR hub is the core abstraction for sending messages to clients connected to the SignalR server.</span></span> <span data-ttu-id="f2174-106">사용 하 여 앱의 다른 위치에서 메시지를 보낼 수 이기도 `IHubContext` 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="f2174-106">It's also possible to send messages from other places in your app using the `IHubContext` service.</span></span> <span data-ttu-id="f2174-107">이 문서는 SignalR에 액세스 하는 방법에 설명 `IHubContext` 허브 외부에서 클라이언트에 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2174-107">This article explains how to access a SignalR `IHubContext` to send notifications to clients from outside a hub.</span></span>

<span data-ttu-id="f2174-108">[보거나 다운로드 샘플 코드](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/hubcontext/sample/) [(다운로드 하는 방법)](xref:tutorials/index#how-to-download-a-sample)</span><span class="sxs-lookup"><span data-stu-id="f2174-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/hubcontext/sample/) [(how to download)](xref:tutorials/index#how-to-download-a-sample)</span></span>

## <a name="get-an-instance-of-ihubcontext"></a><span data-ttu-id="f2174-109">인스턴스를 가져옵니다 `IHubContext`</span><span class="sxs-lookup"><span data-stu-id="f2174-109">Get an instance of `IHubContext`</span></span>

<span data-ttu-id="f2174-110">ASP.NET Core SignalR의 인스턴스를 액세스할 수 있습니다 `IHubContext` 종속성 주입을 통해.</span><span class="sxs-lookup"><span data-stu-id="f2174-110">In ASP.NET Core SignalR, you can access an instance of `IHubContext` via dependency injection.</span></span> <span data-ttu-id="f2174-111">인스턴스를 삽입할 수 `IHubContext` 는 컨트롤러, 미들웨어, 또는 기타 DI 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="f2174-111">You can inject an instance of `IHubContext` into a controller, middleware, or other DI service.</span></span> <span data-ttu-id="f2174-112">메시지를 보내는 클라이언트에 인스턴스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2174-112">Use the instance to send messages to clients.</span></span>

> [!NOTE]
> <span data-ttu-id="f2174-113">이와 달리 ASP.NET signalr에 대 한 액세스를 제공 하기 위해 GlobalHost를 사용 하는 `IHubContext`합니다.</span><span class="sxs-lookup"><span data-stu-id="f2174-113">This differs from ASP.NET SignalR which used GlobalHost to provide access to the `IHubContext`.</span></span> <span data-ttu-id="f2174-114">ASP.NET Core 전역이 단일 항목에 대 한 필요성을 제거 하는 종속성 주입 프레임 워크를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2174-114">ASP.NET Core has a dependency injection framework that removes the need for this global singleton.</span></span>

### <a name="inject-an-instance-of-ihubcontext-in-a-controller"></a><span data-ttu-id="f2174-115">인스턴스를 삽입할 `IHubContext` 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="f2174-115">Inject an instance of `IHubContext` in a controller</span></span>

<span data-ttu-id="f2174-116">인스턴스를 삽입할 수 `IHubContext` 생성자를 추가 하 여 컨트롤러에:</span><span class="sxs-lookup"><span data-stu-id="f2174-116">You can inject an instance of `IHubContext` into a controller by adding it to your constructor:</span></span>

[!code-csharp[IHubContext](hubcontext/sample/Controllers/HomeController.cs?range=12-19,57)]

<span data-ttu-id="f2174-117">인스턴스에 액세스할 수 있는 이제 `IHubContext`, 허브 자체에 있던 마치 허브 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2174-117">Now, with access to an instance of `IHubContext`, you can call hub methods as if you were in the hub itself.</span></span>

[!code-csharp[IHubContext](hubcontext/sample/Controllers/HomeController.cs?range=21-25)]

### <a name="get-an-instance-of-ihubcontext-in-middleware"></a><span data-ttu-id="f2174-118">인스턴스를 가져올 `IHubContext` 미들웨어에서</span><span class="sxs-lookup"><span data-stu-id="f2174-118">Get an instance of `IHubContext` in middleware</span></span>

<span data-ttu-id="f2174-119">액세스는 `IHubContext` 미들웨어 파이프라인 내에서 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2174-119">Access the `IHubContext` within the middleware pipeline like so:</span></span>

```csharp
app.Use(next => (context) =>
{
    var hubContext = (IHubContext<MyHub>)context
                        .RequestServices
                        .GetServices<IHubContext<MyHub>>();
    //...
});
```

> [!NOTE]
> <span data-ttu-id="f2174-120">외부에서 허브 메서드 호출 될 때는 `Hub` 클래스, 호출와 연결 된 호출자는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2174-120">When hub methods are called from outside of the `Hub` class, there's no caller associated with the invocation.</span></span> <span data-ttu-id="f2174-121">따라서이에 대 한 액세스는 `ConnectionId`, `Caller`, 및 `Others` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="f2174-121">Therefore, there's no access to the `ConnectionId`, `Caller`, and `Others` properties.</span></span>

## <a name="related-resources"></a><span data-ttu-id="f2174-122">관련 참고 자료</span><span class="sxs-lookup"><span data-stu-id="f2174-122">Related resources</span></span>

* [<span data-ttu-id="f2174-123">시작</span><span class="sxs-lookup"><span data-stu-id="f2174-123">Get started</span></span>](xref:signalr/get-started)
* [<span data-ttu-id="f2174-124">허브</span><span class="sxs-lookup"><span data-stu-id="f2174-124">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="f2174-125">Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="f2174-125">Publish to Azure</span></span>](xref:signalr/publish-to-azure-web-app)
