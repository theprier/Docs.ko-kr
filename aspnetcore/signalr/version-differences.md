---
title: SignalR 및 ASP.NET Core SignalR 간의 차이점
author: rachelappel
description: SignalR 및 ASP.NET Core SignalR 간의 차이점
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.date: 06/30/2018
uid: signalr/version-differences
ms.openlocfilehash: fd314d93333bd159aef4bb4863be50c646809cf0
ms.sourcegitcommit: 1faf2525902236428dae6a59e375519bafd5d6d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090070"
---
# <a name="differences-between-signalr-and-aspnet-core-signalr"></a><span data-ttu-id="f97d9-103">SignalR 및 ASP.NET Core SignalR 간의 차이점</span><span class="sxs-lookup"><span data-stu-id="f97d9-103">Differences between SignalR and ASP.NET Core SignalR</span></span>

<span data-ttu-id="f97d9-104">ASP.NET Core SignalR 클라이언트 또는 ASP.NET SignalR 용 서버와 호환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-104">ASP.NET Core SignalR is not compatible with clients or servers for ASP.NET SignalR.</span></span> <span data-ttu-id="f97d9-105">이 문서는 제거 되거나 ASP.NET Core SignalR에서 변경 된 기능을 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-105">This article details the features which have been removed or changed in the ASP.NET Core SignalR.</span></span>

## <a name="feature-differences"></a><span data-ttu-id="f97d9-106">기능 차이점</span><span class="sxs-lookup"><span data-stu-id="f97d9-106">Feature differences</span></span>

### <a name="automatic-reconnects"></a><span data-ttu-id="f97d9-107">자동 다시 연결</span><span class="sxs-lookup"><span data-stu-id="f97d9-107">Automatic reconnects</span></span>

<span data-ttu-id="f97d9-108">자동 다시 연결 이상 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-108">Automatic reconnects are no longer supported.</span></span> <span data-ttu-id="f97d9-109">이전에 SignalR 연결 삭제 된 경우 서버에 다시 연결 하려고 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-109">Previously, SignalR tried to reconnect to the server if the connection was dropped.</span></span> <span data-ttu-id="f97d9-110">이제, 클라이언트의 연결이 다시 연결 하는 경우 사용자 새 연결을 명시적으로 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-110">Now, if the client is disconnected the user must explicitly start a new connection if they want to reconnect.</span></span>

### <a name="protocol-support"></a><span data-ttu-id="f97d9-111">프로토콜 지원</span><span class="sxs-lookup"><span data-stu-id="f97d9-111">Protocol support</span></span>

<span data-ttu-id="f97d9-112">ASP.NET Core SignalR 기반으로 새로운 이진 프로토콜 뿐만 아니라 JSON 지원 [MessagePack](xref:signalr/messagepackhubprotocol)합니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-112">ASP.NET Core SignalR supports JSON, as well as a new binary protocol based on [MessagePack](xref:signalr/messagepackhubprotocol).</span></span> <span data-ttu-id="f97d9-113">또한 사용자 지정 프로토콜을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-113">Additionally, custom protocols can be created.</span></span>

## <a name="differences-on-the-server"></a><span data-ttu-id="f97d9-114">서버에서의 차이점</span><span class="sxs-lookup"><span data-stu-id="f97d9-114">Differences on the server</span></span>

<span data-ttu-id="f97d9-115">SignalR의 서버 쪽 라이브러리에 포함 된는 `Microsoft.AspNetCore.App` 패키지의 일부인는 **ASP.NET Core 웹 응용 프로그램** Razor와 MVC 프로젝트에 대 한 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-115">The SignalR server-side libraries are included in the `Microsoft.AspNetCore.App` package that is part of the **ASP.NET Core Web Application** template for both Razor and MVC projects.</span></span>

<span data-ttu-id="f97d9-116">호출 하 여 구성 해야 하므로 SignalR은 ASP.NET Core 미들웨어, `AddSignalR` 에서 `Startup.ConfigureServices`합니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-116">SignalR is an ASP.NET Core middleware, so it must be configured by calling `AddSignalR` in `Startup.ConfigureServices`.</span></span>

```csharp
services.AddSignalR();
```

<span data-ttu-id="f97d9-117">라우팅을 구성 하려면 허브 내에 경로 매핑하는 `UseSignalR` 메서드 호출의 `Startup.Configure` 메서드.</span><span class="sxs-lookup"><span data-stu-id="f97d9-117">To configure routing, map routes to hubs inside the `UseSignalR` method call in the `Startup.Configure` method.</span></span>

```csharp
app.UseSignalR(routes =>
{
    routes.MapHub<ChatHub>("/hub");
});
```

### <a name="sticky-sessions-now-required"></a><span data-ttu-id="f97d9-118">이제 필요한 고정 세션</span><span class="sxs-lookup"><span data-stu-id="f97d9-118">Sticky sessions now required</span></span>

<span data-ttu-id="f97d9-119">클라이언트는 어떻게 확장 이전 버전의 SignalR에 사용한 때문에 다시 연결 및 팜의 모든 서버에 메시지를 보낼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-119">Because of how scale-out worked in the previous versions of SignalR, clients could reconnect and send messages to any server in the farm.</span></span> <span data-ttu-id="f97d9-120">다시 연결을 지원 하지 않으므로 뿐만 아니라 확장 모델에 변경 내용으로 인해이 더 이상 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-120">Due to changes to the scale-out model, as well as not supporting reconnects, this is no longer supported.</span></span> <span data-ttu-id="f97d9-121">이제 클라이언트가 서버에 연결 되 면 연결 기간에 대 한 동일한 서버와 상호 작용에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-121">Now, once the client connects to the server it needs to interact with the same server for the duration of the connection.</span></span>

### <a name="single-hub-per-connection"></a><span data-ttu-id="f97d9-122">단일 허브 연결당</span><span class="sxs-lookup"><span data-stu-id="f97d9-122">Single hub per connection</span></span>

<span data-ttu-id="f97d9-123">ASP.NET Core SignalR 연결 모델이 간소화 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-123">In ASP.NET Core SignalR, the connection model has been simplified.</span></span> <span data-ttu-id="f97d9-124">연결은 여러 허브에 대 한 액세스를 공유 하는 데 사용 되는 단일 연결 하지 않고 단일 허브에 직접 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-124">Connections are made directly to a single hub, rather than a single connection being used to share access to multiple hubs.</span></span>

### <a name="streaming"></a><span data-ttu-id="f97d9-125">스트리밍</span><span class="sxs-lookup"><span data-stu-id="f97d9-125">Streaming</span></span>

<span data-ttu-id="f97d9-126">SignalR에서 지 원하는 [스트리밍 데이터](xref:signalr/streaming) 클라이언트에 허브에서 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-126">SignalR now supports [streaming data](xref:signalr/streaming) from the hub to the client.</span></span>

### <a name="state"></a><span data-ttu-id="f97d9-127">시스템 상태</span><span class="sxs-lookup"><span data-stu-id="f97d9-127">State</span></span>

<span data-ttu-id="f97d9-128">진행 메시지에 대 한 지원 및 클라이언트와 허브 (HubState) 사이의 임의 상태를 전달 하는 기능, 없어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-128">The ability to pass arbitrary state between clients and the hub (often called HubState) has been removed, as well as support for progress messages.</span></span> <span data-ttu-id="f97d9-129">현재 허브 프록시 중 해당 하는 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-129">There is no counterpart of hub proxies at the moment.</span></span>

## <a name="differences-on-the-client"></a><span data-ttu-id="f97d9-130">클라이언트에서의 차이점</span><span class="sxs-lookup"><span data-stu-id="f97d9-130">Differences on the client</span></span>

### <a name="typescript"></a><span data-ttu-id="f97d9-131">TypeScript</span><span class="sxs-lookup"><span data-stu-id="f97d9-131">TypeScript</span></span>

<span data-ttu-id="f97d9-132">SignalR의 ASP.NET Core 버전으로 작성 된 [TypeScript](https://www.typescriptlang.org/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-132">The ASP.NET Core version of SignalR is written in [TypeScript](https://www.typescriptlang.org/).</span></span> <span data-ttu-id="f97d9-133">사용 하는 경우 JavaScript 또는 TypeScript에서 작성할 수 있습니다는 [JavaScript 클라이언트](xref:signalr/javascript-client)합니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-133">You can write in JavaScript or TypeScript when using the [JavaScript client](xref:signalr/javascript-client).</span></span>

### <a name="the-javascript-client-is-hosted-at-npmhttpswwwnpmjscom"></a><span data-ttu-id="f97d9-134">JavaScript 클라이언트에 호스트 되어 [npm](https://www.npmjs.com/)</span><span class="sxs-lookup"><span data-stu-id="f97d9-134">The JavaScript client is hosted at [npm](https://www.npmjs.com/)</span></span>

<span data-ttu-id="f97d9-135">JavaScript 클라이언트는 이전 버전에서는 Visual Studio에서 NuGet 패키지를 통해 가져온 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-135">In previous versions, the JavaScript client was obtained through a NuGet package in Visual Studio.</span></span> <span data-ttu-id="f97d9-136">코어 버전에 대 한는 [ @aspnet/signalr npm 패키지](https://www.npmjs.com/package/@aspnet/signalr) JavaScript 라이브러리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-136">For the Core versions, the [@aspnet/signalr npm package](https://www.npmjs.com/package/@aspnet/signalr) contains the JavaScript libraries.</span></span> <span data-ttu-id="f97d9-137">이 패키지에 포함 되어 있지는 **ASP.NET Core 웹 응용 프로그램** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="f97d9-137">This package isn't included in the **ASP.NET Core Web Application** template.</span></span> <span data-ttu-id="f97d9-138">Npm을 사용 하 여 설치 하 고 `@aspnet/signalr` npm 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-138">Use npm to obtain and install the `@aspnet/signalr` npm package.</span></span>

```console
npm init -y
npm install @aspnet/signalr
```

### <a name="jquery"></a><span data-ttu-id="f97d9-139">jQuery</span><span class="sxs-lookup"><span data-stu-id="f97d9-139">jQuery</span></span>

<span data-ttu-id="f97d9-140">JQuery에 대 한 종속성은 제거 되었습니다, 프로젝트에서 jQuery를 계속 사용할 수 있지만.</span><span class="sxs-lookup"><span data-stu-id="f97d9-140">The dependency on jQuery has been removed, however projects can still use jQuery.</span></span>

### <a name="javascript-client-method-syntax"></a><span data-ttu-id="f97d9-141">JavaScript 클라이언트 메서드 구문</span><span class="sxs-lookup"><span data-stu-id="f97d9-141">JavaScript client method syntax</span></span>

<span data-ttu-id="f97d9-142">JavaScript 구문 SignalR의 이전 버전에서 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-142">The JavaScript syntax has changed from the previous version of SignalR.</span></span> <span data-ttu-id="f97d9-143">사용 하지 않고는 `$connection` 개체를 사용 하 여 연결을 만들기는 `HubConnectionBuilder` API입니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-143">Rather than using the `$connection` object, create a connection using the `HubConnectionBuilder` API.</span></span>

```javascript
const connection = new signalR.HubConnectionBuilder()
    .withUrl("/hub")
    .build();
```

<span data-ttu-id="f97d9-144">사용 하 여 `connection.on` 허브를 호출할 수 있는 클라이언트 방법을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-144">Use `connection.on` to specify client methods that the hub can call.</span></span>

```javascript
connection.on("ReceiveMessage", (user, message) => {
    const msg = message.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
    const encodedMsg = user + " says " + msg;
    log(encodedMsg);
});
```

<span data-ttu-id="f97d9-145">클라이언트 메서드를 만든 후 허브 연결을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-145">After creating the client method, start the hub connection.</span></span> <span data-ttu-id="f97d9-146">체인을 `catch` 메서드를 로그 또는 오류를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-146">Chain a `catch` method to log or handle errors.</span></span>

```javascript
connection.start().catch(err => console.error(err.toString()));
```

### <a name="hub-proxies"></a><span data-ttu-id="f97d9-147">허브 프록시</span><span class="sxs-lookup"><span data-stu-id="f97d9-147">Hub proxies</span></span>

<span data-ttu-id="f97d9-148">허브 프록시 더 이상 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-148">Hub proxies are no longer automatically generated.</span></span> <span data-ttu-id="f97d9-149">메서드 이름에 전달 되는 대신,는 `invoke` 문자열로 API입니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-149">Instead, the method name is passed into the `invoke` API as a string.</span></span>

### <a name="net-and-other-clients"></a><span data-ttu-id="f97d9-150">.NET 및 기타 클라이언트</span><span class="sxs-lookup"><span data-stu-id="f97d9-150">.NET and other clients</span></span>

<span data-ttu-id="f97d9-151">`Microsoft.AspNetCore.SignalR.Client` ASP.NET Core SignalR 용.NET 클라이언트 라이브러리 NuGet 패키지에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-151">The `Microsoft.AspNetCore.SignalR.Client` NuGet package contains the .NET client libraries for ASP.NET Core SignalR.</span></span>

<span data-ttu-id="f97d9-152">사용 된 `HubConnectionBuilder` 을 작성 하는 허브에 대 한 연결의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="f97d9-152">Use the `HubConnectionBuilder` to create and build an instance of a connection to a hub.</span></span>

```csharp
connection = new HubConnectionBuilder()
    .WithUrl("url")
    .Build();
```

## <a name="additional-resources"></a><span data-ttu-id="f97d9-153">추가 자료</span><span class="sxs-lookup"><span data-stu-id="f97d9-153">Additional resources</span></span>

* [<span data-ttu-id="f97d9-154">허브</span><span class="sxs-lookup"><span data-stu-id="f97d9-154">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="f97d9-155">JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="f97d9-155">JavaScript client</span></span>](xref:signalr/javascript-client)
* [<span data-ttu-id="f97d9-156">.NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="f97d9-156">.NET client</span></span>](xref:signalr/dotnet-client)
* [<span data-ttu-id="f97d9-157">지원되는 플랫폼</span><span class="sxs-lookup"><span data-stu-id="f97d9-157">Supported platforms</span></span>](xref:signalr/supported-platforms)
