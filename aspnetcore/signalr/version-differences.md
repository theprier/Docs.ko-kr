---
title: SignalR과 ASP.NET Core SignalR의 차이점
author: tdykstra
description: SignalR과 ASP.NET Core SignalR의 차이점
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.date: 09/10/2018
uid: signalr/version-differences
ms.openlocfilehash: 8f07647959b6ef815eed599703bdb1bfb446572f
ms.sourcegitcommit: edb9d2d78c9a4d68b397e74ae2aff088b325a143
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51505754"
---
# <a name="differences-between-aspnet-signalr-and-aspnet-core-signalr"></a><span data-ttu-id="d1a58-103">ASP.NET SignalR과 ASP.NET Core SignalR의 차이점</span><span class="sxs-lookup"><span data-stu-id="d1a58-103">Differences between ASP.NET SignalR and ASP.NET Core SignalR</span></span>

<span data-ttu-id="d1a58-104">ASP.NET Core SignalR은 ASP.NET SignalR용 클라이언트 또는 서버와 호환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-104">ASP.NET Core SignalR isn't compatible with clients or servers for ASP.NET SignalR.</span></span> <span data-ttu-id="d1a58-105">이 문서에서는 ASP.NET Core SignalR에서 제거되거나 변경된 기능을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-105">This article details features which have been removed or changed in ASP.NET Core SignalR.</span></span>

## <a name="how-to-identify-the-signalr-version"></a><span data-ttu-id="d1a58-106">SignalR 버전 식별 방법</span><span class="sxs-lookup"><span data-stu-id="d1a58-106">How to identify the SignalR version</span></span>

|                      | <span data-ttu-id="d1a58-107">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="d1a58-107">ASP.NET SignalR</span></span> | <span data-ttu-id="d1a58-108">ASP.NET Core SignalR</span><span class="sxs-lookup"><span data-stu-id="d1a58-108">ASP.NET Core SignalR</span></span> |
| -------------------- | --------------- | -------------------- |
| <span data-ttu-id="d1a58-109">Server NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="d1a58-109">Server NuGet Package</span></span> | [<span data-ttu-id="d1a58-110">Microsoft.AspNet.SignalR</span><span class="sxs-lookup"><span data-stu-id="d1a58-110">Microsoft.AspNet.SignalR</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR/) | <span data-ttu-id="d1a58-111">[Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App/) (.NET Core)</span><span class="sxs-lookup"><span data-stu-id="d1a58-111">[Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App/) (.NET Core)</span></span><br><span data-ttu-id="d1a58-112">[Microsoft.AspNetCore.SignalR](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR/) (.NET Framework)</span><span class="sxs-lookup"><span data-stu-id="d1a58-112">[Microsoft.AspNetCore.SignalR](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR/) (.NET Framework)</span></span> |
| <span data-ttu-id="d1a58-113">클라이언트 NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="d1a58-113">Client NuGet Packages</span></span> | [<span data-ttu-id="d1a58-114">Microsoft.AspNet.SignalR.Client</span><span class="sxs-lookup"><span data-stu-id="d1a58-114">Microsoft.AspNet.SignalR.Client</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Client/)<br>[<span data-ttu-id="d1a58-115">Microsoft.AspNet.SignalR.JS</span><span class="sxs-lookup"><span data-stu-id="d1a58-115">Microsoft.AspNet.SignalR.JS</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.JS/) | [<span data-ttu-id="d1a58-116">Microsoft.AspNetCore.SignalR.Client</span><span class="sxs-lookup"><span data-stu-id="d1a58-116">Microsoft.AspNetCore.SignalR.Client</span></span>](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR.Client/) |
| <span data-ttu-id="d1a58-117">클라이언트 npm 패키지</span><span class="sxs-lookup"><span data-stu-id="d1a58-117">Client npm Package</span></span> | [<span data-ttu-id="d1a58-118">signalr</span><span class="sxs-lookup"><span data-stu-id="d1a58-118">signalr</span></span>](https://www.npmjs.com/package/signalr) | [@aspnet/signalr](https://www.npmjs.com/package/@aspnet/signalr) |
| <span data-ttu-id="d1a58-119">서버 앱 유형</span><span class="sxs-lookup"><span data-stu-id="d1a58-119">Server App Type</span></span> | <span data-ttu-id="d1a58-120">ASP.NET (System.Web) 또는 OWIN 자체 호스트</span><span class="sxs-lookup"><span data-stu-id="d1a58-120">ASP.NET (System.Web) or OWIN Self-Host</span></span> | <span data-ttu-id="d1a58-121">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="d1a58-121">ASP.NET Core</span></span> |
| <span data-ttu-id="d1a58-122">지원되는 서버 플랫폼</span><span class="sxs-lookup"><span data-stu-id="d1a58-122">Supported Server Platforms</span></span> | <span data-ttu-id="d1a58-123">.NET framework 4.5 이상</span><span class="sxs-lookup"><span data-stu-id="d1a58-123">.NET Framework 4.5 or later</span></span> | <span data-ttu-id="d1a58-124">.NET Framework 4.6.1 이상</span><span class="sxs-lookup"><span data-stu-id="d1a58-124">.NET Framework 4.6.1 or later</span></span><br><span data-ttu-id="d1a58-125">.NET core 2.1 이상</span><span class="sxs-lookup"><span data-stu-id="d1a58-125">.NET Core 2.1 or later</span></span> |

## <a name="feature-differences"></a><span data-ttu-id="d1a58-126">기능상의 차이점</span><span class="sxs-lookup"><span data-stu-id="d1a58-126">Feature differences</span></span>

### <a name="automatic-reconnects"></a><span data-ttu-id="d1a58-127">자동 다시 연결</span><span class="sxs-lookup"><span data-stu-id="d1a58-127">Automatic reconnects</span></span>

<span data-ttu-id="d1a58-128">ASP.NET Core SignalR은 자동 재연결을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-128">Automatic reconnects aren't supported in ASP.NET Core SignalR.</span></span> <span data-ttu-id="d1a58-129">클라이언트의 연결이 끊어진 경우 재연결하려면 사용자가 명시적으로 새로운 연결을 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-129">If the client is disconnected, the user must explicitly start a new connection if they want to reconnect.</span></span> <span data-ttu-id="d1a58-130">ASP.NET SignalR은 연결이 끊어지면 SignalR이 서버에 재연결하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-130">In ASP.NET SignalR, SignalR attempts to reconnect to the server if the connection is dropped.</span></span> 

### <a name="protocol-support"></a><span data-ttu-id="d1a58-131">프로토콜 지원</span><span class="sxs-lookup"><span data-stu-id="d1a58-131">Protocol support</span></span>

<span data-ttu-id="d1a58-132">ASP.NET Core SignalR은 JSON뿐만 아니라 [MessagePack](xref:signalr/messagepackhubprotocol) 기반의 새로운 이진 프로토콜을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-132">ASP.NET Core SignalR supports JSON, as well as a new binary protocol based on [MessagePack](xref:signalr/messagepackhubprotocol).</span></span> <span data-ttu-id="d1a58-133">또한 사용자 지정 프로토콜을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-133">Additionally, custom protocols can be created.</span></span>

### <a name="transports"></a><span data-ttu-id="d1a58-134">전송</span><span class="sxs-lookup"><span data-stu-id="d1a58-134">Transports</span></span>

<span data-ttu-id="d1a58-135">영원히 프레임 전송 ASP.NET Core SignalR에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-135">The Forever Frame transport is not supported in ASP.NET Core SignalR.</span></span>

## <a name="differences-on-the-server"></a><span data-ttu-id="d1a58-136">서버의 차이점</span><span class="sxs-lookup"><span data-stu-id="d1a58-136">Differences on the server</span></span>

<span data-ttu-id="d1a58-137">ASP.NET Core SignalR의 서버 쪽 라이브러리는 Razor 및 MVC 프로젝트를 위한 **ASP.NET Core 웹 응용 프로그램** 템플릿의 일부인 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app) 패키지에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-137">The ASP.NET Core SignalR server-side libraries are included in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) package that's part of the **ASP.NET Core Web Application** template for both Razor and MVC projects.</span></span>

<span data-ttu-id="d1a58-138">ASP.NET Core SignalR은 ASP.NET Core 미들웨어이므로 `Startup.ConfigureServices`에서 [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr)을 호출하여 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-138">ASP.NET Core SignalR is an ASP.NET Core middleware, so it must be configured by calling [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr) in `Startup.ConfigureServices`.</span></span>

```csharp
services.AddSignalR()
```

<span data-ttu-id="d1a58-139">라우팅을 구성하려면 `Startup.Configure` 메서드에서 [UseSignalR](/dotnet/api/microsoft.aspnetcore.builder.signalrappbuilderextensions.usesignalr) 메서드 호출 내부에서 허브에 경로를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-139">To configure routing, map routes to hubs inside the [UseSignalR](/dotnet/api/microsoft.aspnetcore.builder.signalrappbuilderextensions.usesignalr) method call in the `Startup.Configure` method.</span></span>

```csharp
app.UseSignalR(routes =>
{
    routes.MapHub<ChatHub>("/hub");
});
```

### <a name="sticky-sessions"></a><span data-ttu-id="d1a58-140">고정 세션</span><span class="sxs-lookup"><span data-stu-id="d1a58-140">Sticky sessions</span></span>

<span data-ttu-id="d1a58-141">ASP.NET SignalR에 대 한 확장 모델에는 클라이언트가 다시 연결 하 고 팜의 모든 서버에 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-141">The scaleout model for ASP.NET SignalR allows clients to reconnect and send messages to any server in the farm.</span></span> <span data-ttu-id="d1a58-142">ASP.NET Core SignalR의 연결 기간에 대 한 클라이언트는 동일한 서버를 사용 하 여 작용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-142">In ASP.NET Core SignalR, the client must interact with the same server for the duration of the connection.</span></span> <span data-ttu-id="d1a58-143">Redis를 사용 하 여 확장에는 고정 세션은 필요한 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-143">For scaleout using Redis, that means sticky sessions are required.</span></span> <span data-ttu-id="d1a58-144">확장 사용에 대 한 [Azure SignalR Service](/azure/azure-signalr/), 서비스가 클라이언트에 대 한 연결을 처리 하기 때문에 고정 세션이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-144">For scaleout using [Azure SignalR Service](/azure/azure-signalr/), sticky sessions are not required because the service handles connections to clients.</span></span> 

### <a name="single-hub-per-connection"></a><span data-ttu-id="d1a58-145">연결당 단일 허브</span><span class="sxs-lookup"><span data-stu-id="d1a58-145">Single hub per connection</span></span>

<span data-ttu-id="d1a58-146">ASP.NET Core SignalR에서는 연결 모델이 단순화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-146">In ASP.NET Core SignalR, the connection model has been simplified.</span></span> <span data-ttu-id="d1a58-147">단일 연결이 여러 허브에 대한 접근을 공유하기 위해 사용되기 보다는 단일 허브에 직접 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-147">Connections are made directly to a single hub, rather than a single connection being used to share access to multiple hubs.</span></span>

### <a name="streaming"></a><span data-ttu-id="d1a58-148">스트리밍</span><span class="sxs-lookup"><span data-stu-id="d1a58-148">Streaming</span></span>

<span data-ttu-id="d1a58-149">이제 ASP.NET Core SignalR은 허브에서 클라이언트로의 [스트리밍 데이터](xref:signalr/streaming)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-149">ASP.NET Core SignalR now supports [streaming data](xref:signalr/streaming) from the hub to the client.</span></span>

### <a name="state"></a><span data-ttu-id="d1a58-150">상태</span><span class="sxs-lookup"><span data-stu-id="d1a58-150">State</span></span>

<span data-ttu-id="d1a58-151">진행 메시지 관련 기능뿐만 아니라 클라이언트와 허브 간에 임의의 상태를 전달할 수 있는 기능(HubState라고도 함)이 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-151">The ability to pass arbitrary state between clients and the hub (often called HubState) has been removed, as well as support for progress messages.</span></span> <span data-ttu-id="d1a58-152">현재 허브 프록시에 해당하는 기능은 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-152">There is no counterpart of hub proxies at the moment.</span></span>

### <a name="globalhost"></a><span data-ttu-id="d1a58-153">GlobalHost</span><span class="sxs-lookup"><span data-stu-id="d1a58-153">GlobalHost</span></span>

<span data-ttu-id="d1a58-154">ASP.NET Core는 DI (종속성 주입) 프레임 워크에 기본 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-154">ASP.NET Core has dependency injection (DI) built into the framework.</span></span> <span data-ttu-id="d1a58-155">서비스에 액세스 하려면 DI를 사용할 수는 [HubContext](xref:signalr/hubcontext)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-155">Services can use DI to access the [HubContext](xref:signalr/hubcontext).</span></span> <span data-ttu-id="d1a58-156">합니다 `GlobalHost` 가져오려는 ASP.NET SignalR에서 사용 되는 개체는 `HubContext` ASP.NET Core SignalR에 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-156">The `GlobalHost` object that is used in ASP.NET SignalR to get a `HubContext` doesn't exist in ASP.NET Core SignalR.</span></span>

### <a name="hubpipeline"></a><span data-ttu-id="d1a58-157">HubPipeline</span><span class="sxs-lookup"><span data-stu-id="d1a58-157">HubPipeline</span></span>

<span data-ttu-id="d1a58-158">ASP.NET Core SignalR에 대 한 지원이 없는 `HubPipeline` 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-158">ASP.NET Core SignalR doesn't have support for `HubPipeline` modules.</span></span>

## <a name="differences-on-the-client"></a><span data-ttu-id="d1a58-159">클라이언트의 차이점</span><span class="sxs-lookup"><span data-stu-id="d1a58-159">Differences on the client</span></span>

### <a name="typescript"></a><span data-ttu-id="d1a58-160">TypeScript</span><span class="sxs-lookup"><span data-stu-id="d1a58-160">TypeScript</span></span>

<span data-ttu-id="d1a58-161">ASP.NET Core SignalR 클라이언트는 [TypeScript](https://www.typescriptlang.org/)로 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-161">The ASP.NET Core SignalR client is written in [TypeScript](https://www.typescriptlang.org/).</span></span> <span data-ttu-id="d1a58-162">[JavaScript 클라이언트](xref:signalr/javascript-client)를 사용할 때 JavaScript 또는 TypeScript로 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-162">You can write in JavaScript or TypeScript when using the [JavaScript client](xref:signalr/javascript-client).</span></span>

### <a name="the-javascript-client-is-hosted-at-npmhttpswwwnpmjscom"></a><span data-ttu-id="d1a58-163">JavaScript 클라이언트가 [npm](https://www.npmjs.com/)에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-163">The JavaScript client is hosted at [npm](https://www.npmjs.com/)</span></span>

<span data-ttu-id="d1a58-164">이전 버전에서는 Visual Studio의 NuGet 패키지를 통해서 JavaScript 클라이언트를 가져왔습니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-164">In previous versions, the JavaScript client was obtained through a NuGet package in Visual Studio.</span></span> <span data-ttu-id="d1a58-165">Core 버전에서는 [@aspnet/signalr](https://www.npmjs.com/package/@aspnet/signalr) npm 패키지에 JavaScript 라이브러리가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-165">For the Core versions, the [@aspnet/signalr](https://www.npmjs.com/package/@aspnet/signalr) npm package contains the JavaScript libraries.</span></span> <span data-ttu-id="d1a58-166">이 패키지는 **ASP.NET Core 웹 응용 프로그램** 템플릿에 포함되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-166">This package isn't included in the **ASP.NET Core Web Application** template.</span></span> <span data-ttu-id="d1a58-167">npm을 사용하여 `@aspnet/signalr` npm 패키지를 가져와서 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-167">Use npm to obtain and install the `@aspnet/signalr` npm package.</span></span>

```console
npm init -y
npm install @aspnet/signalr
```

### <a name="jquery"></a><span data-ttu-id="d1a58-168">jQuery</span><span class="sxs-lookup"><span data-stu-id="d1a58-168">jQuery</span></span>

<span data-ttu-id="d1a58-169">jQuery에 대한 종속성은 제거되었지만 프로젝트에서 여전히 jQuery를 사용할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-169">The dependency on jQuery has been removed, however projects can still use jQuery.</span></span>

### <a name="internet-explorer-support"></a><span data-ttu-id="d1a58-170">Internet Explorer 지원</span><span class="sxs-lookup"><span data-stu-id="d1a58-170">Internet Explorer support</span></span>

<span data-ttu-id="d1a58-171">ASP.NET Core SignalR (Microsoft Internet Explorer 8 자 이상에서 지원 되는 ASP.NET SignalR) Microsoft Internet Explorer 11 이상이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-171">ASP.NET Core SignalR requires Microsoft Internet Explorer 11 or later (ASP.NET SignalR supported Microsoft Internet Explorer 8 and later).</span></span>

### <a name="javascript-client-method-syntax"></a><span data-ttu-id="d1a58-172">JavaScript 클라이언트 메서드 구문</span><span class="sxs-lookup"><span data-stu-id="d1a58-172">JavaScript client method syntax</span></span>

<span data-ttu-id="d1a58-173">JavaScript 구문이 이전 버전의 SignalR과 달라졌습니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-173">The JavaScript syntax has changed from the previous version of SignalR.</span></span> <span data-ttu-id="d1a58-174">`$connection` 개체를 사용하는 대신 [HubConnectionBuilder](/javascript/api/%40aspnet/signalr/hubconnectionbuilder) API를 사용해서 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-174">Rather than using the `$connection` object, create a connection using the [HubConnectionBuilder](/javascript/api/%40aspnet/signalr/hubconnectionbuilder) API.</span></span>

```javascript
const connection = new signalR.HubConnectionBuilder()
    .withUrl("/hub")
    .build();
```

<span data-ttu-id="d1a58-175">[on](/javascript/api/@aspnet/signalr/HubConnection#on) 메서드를 사용해서 허브가 호출할 수 있는 클라이언트 메서드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-175">Use the [on](/javascript/api/@aspnet/signalr/HubConnection#on) method to specify client methods that the hub can call.</span></span>

```javascript
connection.on("ReceiveMessage", (user, message) => {
    const msg = message.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
    const encodedMsg = user + " says " + msg;
    log(encodedMsg);
});
```

<span data-ttu-id="d1a58-176">클라이언트 메서드를 생성한 다음, 허브 연결을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-176">After creating the client method, start the hub connection.</span></span> <span data-ttu-id="d1a58-177">오류를 기록하거나 처리하려면 [catch](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch) 메서드를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-177">Chain a [catch](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch) method to log or handle errors.</span></span>

```javascript
connection.start().catch(err => console.error(err.toString()));
```

### <a name="hub-proxies"></a><span data-ttu-id="d1a58-178">허브 프록시</span><span class="sxs-lookup"><span data-stu-id="d1a58-178">Hub proxies</span></span>

<span data-ttu-id="d1a58-179">더 이상 허브 프록시가 자동으로 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-179">Hub proxies are no longer automatically generated.</span></span> <span data-ttu-id="d1a58-180">대신 메서드 이름은 [invoke](/javascript/api/%40aspnet/signalr/hubconnection#invoke) API에 문자열로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-180">Instead, the method name is passed into the [invoke](/javascript/api/%40aspnet/signalr/hubconnection#invoke) API as a string.</span></span>

### <a name="net-and-other-clients"></a><span data-ttu-id="d1a58-181">.NET 및 기타 클라이언트</span><span class="sxs-lookup"><span data-stu-id="d1a58-181">.NET and other clients</span></span>

<span data-ttu-id="d1a58-182">`Microsoft.AspNetCore.SignalR.Client` NuGet 패키지에는 ASP.NET Core SignalR용 .NET 클라이언트 라이브러리가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-182">The `Microsoft.AspNetCore.SignalR.Client` NuGet package contains the .NET client libraries for ASP.NET Core SignalR.</span></span>

<span data-ttu-id="d1a58-183">[HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder)를 사용해서 허브에 대한 연결의 인스턴스를 생성하고 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-183">Use the [HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder) to create and build an instance of a connection to a hub.</span></span>

```csharp
connection = new HubConnectionBuilder()
    .WithUrl("url")
    .Build();
```

## <a name="scaleout-differences"></a><span data-ttu-id="d1a58-184">스케일 아웃 차이점</span><span class="sxs-lookup"><span data-stu-id="d1a58-184">Scaleout differences</span></span>

<span data-ttu-id="d1a58-185">ASP.NET SignalR은 SQL Server 및 Redis를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-185">ASP.NET SignalR supports SQL Server and Redis.</span></span> <span data-ttu-id="d1a58-186">ASP.NET Core SignalR은 Azure SignalR Service 및 Redis를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d1a58-186">ASP.NET Core SignalR supports Azure SignalR Service and Redis.</span></span>

### <a name="aspnet"></a><span data-ttu-id="d1a58-187">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d1a58-187">ASP.NET</span></span>

* [<span data-ttu-id="d1a58-188">Azure Service Bus를 이용한 SignalR 스케일 아웃</span><span class="sxs-lookup"><span data-stu-id="d1a58-188">SignalR scaleout with Azure Service Bus</span></span>](/aspnet/signalr/overview/performance/scaleout-with-windows-azure-service-bus)
* [<span data-ttu-id="d1a58-189">Redis를 이용한 SignalR 스케일 아웃</span><span class="sxs-lookup"><span data-stu-id="d1a58-189">SignalR scaleout with Redis</span></span>](/aspnet/signalr/overview/performance/scaleout-with-redis)
* [<span data-ttu-id="d1a58-190">SQL Server를 이용한 SignalR 스케일 아웃</span><span class="sxs-lookup"><span data-stu-id="d1a58-190">SignalR scaleout with SQL Server</span></span>](/aspnet/signalr/overview/performance/scaleout-with-sql-server)

### <a name="aspnet-core"></a><span data-ttu-id="d1a58-191">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="d1a58-191">ASP.NET Core</span></span>

* [<span data-ttu-id="d1a58-192">Azure SignalR Service</span><span class="sxs-lookup"><span data-stu-id="d1a58-192">Azure SignalR Service</span></span>](/azure/azure-signalr/)

## <a name="additional-resources"></a><span data-ttu-id="d1a58-193">추가 자료</span><span class="sxs-lookup"><span data-stu-id="d1a58-193">Additional resources</span></span>

* [<span data-ttu-id="d1a58-194">허브</span><span class="sxs-lookup"><span data-stu-id="d1a58-194">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="d1a58-195">JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="d1a58-195">JavaScript client</span></span>](xref:signalr/javascript-client)
* [<span data-ttu-id="d1a58-196">.NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="d1a58-196">.NET client</span></span>](xref:signalr/dotnet-client)
* [<span data-ttu-id="d1a58-197">지원되는 플랫폼</span><span class="sxs-lookup"><span data-stu-id="d1a58-197">Supported platforms</span></span>](xref:signalr/supported-platforms)
