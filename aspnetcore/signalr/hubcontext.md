---
title: SignalR HubContext
author: tdykstra
description: 알림 허브를 외부 클라이언트에서 보내기를 ASP.NET Core SignalR HubContext 서비스를 사용 하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 06/13/2018
uid: signalr/hubcontext
ms.openlocfilehash: 2d7d37b655bf7dbb71b321919314bbb8bef8db17
ms.sourcegitcommit: 57eccdea7d89a62989272f71aad655465f1c600a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2018
ms.locfileid: "44339981"
---
# <a name="send-messages-from-outside-a-hub"></a><span data-ttu-id="74405-103">허브를 외부에서 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="74405-103">Send messages from outside a hub</span></span>

<span data-ttu-id="74405-104">[Mikael Mengistu](https://twitter.com/MikaelM_12)</span><span class="sxs-lookup"><span data-stu-id="74405-104">By [Mikael Mengistu](https://twitter.com/MikaelM_12)</span></span>

<span data-ttu-id="74405-105">SignalR 허브는 SignalR 서버에 연결 하는 클라이언트에 메시지를 보내기 위한 핵심 추상화입니다.</span><span class="sxs-lookup"><span data-stu-id="74405-105">The SignalR hub is the core abstraction for sending messages to clients connected to the SignalR server.</span></span> <span data-ttu-id="74405-106">사용 하 여 앱의 다른 위치에서 메시지를 보낼 수 이기도 합니다 `IHubContext` 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="74405-106">It's also possible to send messages from other places in your app using the `IHubContext` service.</span></span> <span data-ttu-id="74405-107">이 문서는 SignalR에 액세스 하는 방법에 설명 `IHubContext` 허브 외부의 클라이언트에 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74405-107">This article explains how to access a SignalR `IHubContext` to send notifications to clients from outside a hub.</span></span>

<span data-ttu-id="74405-108">[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/hubcontext/sample/) [(다운로드 하는 방법)](xref:tutorials/index#how-to-download-a-sample)</span><span class="sxs-lookup"><span data-stu-id="74405-108">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/hubcontext/sample/) [(how to download)](xref:tutorials/index#how-to-download-a-sample)</span></span>

## <a name="get-an-instance-of-ihubcontext"></a><span data-ttu-id="74405-109">인스턴스 `IHubContext`</span><span class="sxs-lookup"><span data-stu-id="74405-109">Get an instance of `IHubContext`</span></span>

<span data-ttu-id="74405-110">ASP.NET Core SignalR의 인스턴스에 액세스할 수 있습니다 `IHubContext` 종속성 주입을 통해.</span><span class="sxs-lookup"><span data-stu-id="74405-110">In ASP.NET Core SignalR, you can access an instance of `IHubContext` via dependency injection.</span></span> <span data-ttu-id="74405-111">인스턴스를 삽입할 수 있습니다 `IHubContext` 컨트롤러, 미들웨어 또는 다른 DI 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="74405-111">You can inject an instance of `IHubContext` into a controller, middleware, or other DI service.</span></span> <span data-ttu-id="74405-112">클라이언트에 메시지를 보내는 인스턴스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="74405-112">Use the instance to send messages to clients.</span></span>

> [!NOTE]
> <span data-ttu-id="74405-113">ASP.NET에서이 반해 GlobalHost에 대 한 액세스를 제공 하는 데는 SignalR 4.x는 `IHubContext`합니다.</span><span class="sxs-lookup"><span data-stu-id="74405-113">This differs from ASP.NET 4.x SignalR which used GlobalHost to provide access to the `IHubContext`.</span></span> <span data-ttu-id="74405-114">ASP.NET Core는 전역이 단일 항목에 대 한 필요성을 제거 하는 종속성 주입 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="74405-114">ASP.NET Core has a dependency injection framework that removes the need for this global singleton.</span></span>

### <a name="inject-an-instance-of-ihubcontext-in-a-controller"></a><span data-ttu-id="74405-115">인스턴스를 주입 `IHubContext` 컨트롤러에서</span><span class="sxs-lookup"><span data-stu-id="74405-115">Inject an instance of `IHubContext` in a controller</span></span>

<span data-ttu-id="74405-116">인스턴스를 삽입할 수 있습니다 `IHubContext` 생성자에 추가 하 여 컨트롤러:</span><span class="sxs-lookup"><span data-stu-id="74405-116">You can inject an instance of `IHubContext` into a controller by adding it to your constructor:</span></span>

[!code-csharp[IHubContext](hubcontext/sample/Controllers/HomeController.cs?range=12-19,57)]

<span data-ttu-id="74405-117">인스턴스에 대 한 액세스를 사용 하 여 이제 `IHubContext`, 자체 허브에 것 처럼 허브 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74405-117">Now, with access to an instance of `IHubContext`, you can call hub methods as if you were in the hub itself.</span></span>

[!code-csharp[IHubContext](hubcontext/sample/Controllers/HomeController.cs?range=21-25)]

### <a name="get-an-instance-of-ihubcontext-in-middleware"></a><span data-ttu-id="74405-118">인스턴스를 가져올 `IHubContext` 미들웨어에서</span><span class="sxs-lookup"><span data-stu-id="74405-118">Get an instance of `IHubContext` in middleware</span></span>

<span data-ttu-id="74405-119">액세스는 `IHubContext` 미들웨어 파이프라인 내에서 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="74405-119">Access the `IHubContext` within the middleware pipeline like so:</span></span>

```csharp
app.Use(next => async (context) =>
{
    var hubContext = context.RequestServices
                            .GetRequiredService<IHubContext<MyHub>>();
    //...
});
```

> [!NOTE]
> <span data-ttu-id="74405-120">외부에서 허브 메서드 호출 될 때를 `Hub` 클래스는 호출을 통해 연결 하는 호출자에 게 없습니다.</span><span class="sxs-lookup"><span data-stu-id="74405-120">When hub methods are called from outside of the `Hub` class, there's no caller associated with the invocation.</span></span> <span data-ttu-id="74405-121">따라서이에 대 한 액세스는 `ConnectionId`, `Caller`, 및 `Others` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="74405-121">Therefore, there's no access to the `ConnectionId`, `Caller`, and `Others` properties.</span></span>

## <a name="related-resources"></a><span data-ttu-id="74405-122">관련 참고 자료</span><span class="sxs-lookup"><span data-stu-id="74405-122">Related resources</span></span>

* [<span data-ttu-id="74405-123">시작</span><span class="sxs-lookup"><span data-stu-id="74405-123">Get started</span></span>](xref:tutorials/signalr)
* [<span data-ttu-id="74405-124">허브</span><span class="sxs-lookup"><span data-stu-id="74405-124">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="74405-125">Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="74405-125">Publish to Azure</span></span>](xref:signalr/publish-to-azure-web-app)
