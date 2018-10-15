---
title: SignalR 및 ASP.NET Core SignalR의 차이점
author: tdykstra
description: SignalR 및 ASP.NET Core SignalR의 차이점
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.date: 09/10/2018
uid: signalr/version-differences
ms.openlocfilehash: ea2de2606a99de70fa645c0c42303525fea0a44e
ms.sourcegitcommit: 4bdf7703aed86ebd56b9b4bae9ad5700002af32d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2018
ms.locfileid: "49325538"
---
# <a name="differences-between-aspnet-signalr-and-aspnet-core-signalr"></a><span data-ttu-id="25daf-103">ASP.NET SignalR 및 ASP.NET Core SignalR의 차이점</span><span class="sxs-lookup"><span data-stu-id="25daf-103">Differences between ASP.NET SignalR and ASP.NET Core SignalR</span></span>

<span data-ttu-id="25daf-104">ASP.NET Core SignalR 클라이언트 또는 ASP.NET SignalR에 대 한 서버와 호환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="25daf-104">ASP.NET Core SignalR isn't compatible with clients or servers for ASP.NET SignalR.</span></span> <span data-ttu-id="25daf-105">이 문서에서는 ASP.NET Core SignalR에서 변경 되거나 제거 된 기능을 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="25daf-105">This article details features which have been removed or changed in ASP.NET Core SignalR.</span></span>

## <a name="how-to-identify-the-signalr-version"></a><span data-ttu-id="25daf-106">SignalR 버전을 식별 하는 방법</span><span class="sxs-lookup"><span data-stu-id="25daf-106">How to identify the SignalR version</span></span>

|                      | <span data-ttu-id="25daf-107">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="25daf-107">ASP.NET SignalR</span></span> | <span data-ttu-id="25daf-108">ASP.NET Core SignalR</span><span class="sxs-lookup"><span data-stu-id="25daf-108">ASP.NET Core SignalR</span></span> |
| -------------------- | --------------- | -------------------- |
| <span data-ttu-id="25daf-109">Server NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="25daf-109">Server NuGet Package</span></span> | [<span data-ttu-id="25daf-110">Microsoft.AspNet.SignalR</span><span class="sxs-lookup"><span data-stu-id="25daf-110">Microsoft.AspNet.SignalR</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR/) | <span data-ttu-id="25daf-111">[Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App/) (.NET Core)</span><span class="sxs-lookup"><span data-stu-id="25daf-111">[Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App/) (.NET Core)</span></span><br><span data-ttu-id="25daf-112">[Microsoft.AspNetCore.SignalR](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR/) (.NET Framework)</span><span class="sxs-lookup"><span data-stu-id="25daf-112">[Microsoft.AspNetCore.SignalR](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR/) (.NET Framework)</span></span> |
| <span data-ttu-id="25daf-113">클라이언트 NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="25daf-113">Client NuGet Packages</span></span> | [<span data-ttu-id="25daf-114">Microsoft.AspNet.SignalR.Client</span><span class="sxs-lookup"><span data-stu-id="25daf-114">Microsoft.AspNet.SignalR.Client</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Client/)<br>[<span data-ttu-id="25daf-115">Microsoft.AspNet.SignalR.JS</span><span class="sxs-lookup"><span data-stu-id="25daf-115">Microsoft.AspNet.SignalR.JS</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.JS/) | [<span data-ttu-id="25daf-116">Microsoft.AspNetCore.SignalR.Client</span><span class="sxs-lookup"><span data-stu-id="25daf-116">Microsoft.AspNetCore.SignalR.Client</span></span>](https://www.nuget.org/packages/Microsoft.AspNetCore.SignalR.Client/) |
| <span data-ttu-id="25daf-117">클라이언트 npm 패키지</span><span class="sxs-lookup"><span data-stu-id="25daf-117">Client npm Package</span></span> | [<span data-ttu-id="25daf-118">signalr</span><span class="sxs-lookup"><span data-stu-id="25daf-118">signalr</span></span>](https://www.npmjs.com/package/signalr) | [@aspnet/signalr](https://www.npmjs.com/package/@aspnet/signalr) |
| <span data-ttu-id="25daf-119">서버 앱 유형</span><span class="sxs-lookup"><span data-stu-id="25daf-119">Server App Type</span></span> | <span data-ttu-id="25daf-120">ASP.NET (System.Web) 또는 OWIN 자체 호스트</span><span class="sxs-lookup"><span data-stu-id="25daf-120">ASP.NET (System.Web) or OWIN Self-Host</span></span> | <span data-ttu-id="25daf-121">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="25daf-121">ASP.NET Core</span></span> |
| <span data-ttu-id="25daf-122">지원 되는 서버 플랫폼</span><span class="sxs-lookup"><span data-stu-id="25daf-122">Supported Server Platforms</span></span> | <span data-ttu-id="25daf-123">.NET framework 4.5 이상</span><span class="sxs-lookup"><span data-stu-id="25daf-123">.NET Framework 4.5 or later</span></span> | <span data-ttu-id="25daf-124">.NET Framework 4.6.1 이상</span><span class="sxs-lookup"><span data-stu-id="25daf-124">.NET Framework 4.6.1 or later</span></span><br><span data-ttu-id="25daf-125">.NET core 2.1 이상</span><span class="sxs-lookup"><span data-stu-id="25daf-125">.NET Core 2.1 or later</span></span> |

## <a name="feature-differences"></a><span data-ttu-id="25daf-126">기능 차이점</span><span class="sxs-lookup"><span data-stu-id="25daf-126">Feature differences</span></span>

### <a name="automatic-reconnects"></a><span data-ttu-id="25daf-127">자동 다시 연결</span><span class="sxs-lookup"><span data-stu-id="25daf-127">Automatic reconnects</span></span>

<span data-ttu-id="25daf-128">자동 다시 연결 ASP.NET Core SignalR에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="25daf-128">Automatic reconnects aren't supported in ASP.NET Core SignalR.</span></span> <span data-ttu-id="25daf-129">클라이언트 연결이 끊어진 경우 다시 연결 하려는 경우 사용자는 새 연결을 시작 명시적으로 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25daf-129">If the client is disconnected, the user must explicitly start a new connection if they want to reconnect.</span></span> <span data-ttu-id="25daf-130">ASP.NET SignalR, SignalR 연결 삭제 되 면 서버에 다시 연결 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="25daf-130">In ASP.NET SignalR, SignalR attempts to reconnect to the server if the connection is dropped.</span></span> 

### <a name="protocol-support"></a><span data-ttu-id="25daf-131">프로토콜 지원</span><span class="sxs-lookup"><span data-stu-id="25daf-131">Protocol support</span></span>

<span data-ttu-id="25daf-132">ASP.NET Core SignalR 기반 새 이진 프로토콜 뿐만 아니라 JSON 지원 [MessagePack](xref:signalr/messagepackhubprotocol)합니다.</span><span class="sxs-lookup"><span data-stu-id="25daf-132">ASP.NET Core SignalR supports JSON, as well as a new binary protocol based on [MessagePack](xref:signalr/messagepackhubprotocol).</span></span> <span data-ttu-id="25daf-133">또한 사용자 지정 프로토콜을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25daf-133">Additionally, custom protocols can be created.</span></span>

## <a name="differences-on-the-server"></a><span data-ttu-id="25daf-134">서버에서 차이점</span><span class="sxs-lookup"><span data-stu-id="25daf-134">Differences on the server</span></span>

<span data-ttu-id="25daf-135">ASP.NET Core SignalR의 서버 쪽 라이브러리에 포함 된 합니다 [Microsoft.AspNetCore.App 메타 패키지](xref:fundamentals/metapackage-app) 패키지의 일부인 합니다 **ASP.NET Core 웹 응용 프로그램** Razor 및 MVC에 대 한 템플릿 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="25daf-135">The ASP.NET Core SignalR server-side libraries are included in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app) package that's part of the **ASP.NET Core Web Application** template for both Razor and MVC projects.</span></span>

<span data-ttu-id="25daf-136">ASP.NET Core SignalR은 ASP.NET Core 미들웨어를 호출 하 여 구성 해야 하므로 [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr) 에서 `Startup.ConfigureServices`합니다.</span><span class="sxs-lookup"><span data-stu-id="25daf-136">ASP.NET Core SignalR is an ASP.NET Core middleware, so it must be configured by calling [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr) in `Startup.ConfigureServices`.</span></span>

```csharp
services.AddSignalR()
```

<span data-ttu-id="25daf-137">에 라우팅을 구성 하려면 경로 내에서 허브에 매핑하는 [UseSignalR](/dotnet/api/microsoft.aspnetcore.builder.signalrappbuilderextensions.usesignalr) 메서드 호출을 `Startup.Configure` 메서드.</span><span class="sxs-lookup"><span data-stu-id="25daf-137">To configure routing, map routes to hubs inside the [UseSignalR](/dotnet/api/microsoft.aspnetcore.builder.signalrappbuilderextensions.usesignalr) method call in the `Startup.Configure` method.</span></span>

```csharp
app.UseSignalR(routes =>
{
    routes.MapHub<ChatHub>("/hub");
});
```

### <a name="sticky-sessions-now-required"></a><span data-ttu-id="25daf-138">이제 필요한 고정 세션</span><span class="sxs-lookup"><span data-stu-id="25daf-138">Sticky sessions now required</span></span>

<span data-ttu-id="25daf-139">ASP.NET SignalR에서 스케일 아웃 작동 하는 방법으로 인해 클라이언트가 다시 연결을 팜의 모든 서버에 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25daf-139">Because of how scale-out worked in ASP.NET SignalR, clients could reconnect and send messages to any server in the farm.</span></span> <span data-ttu-id="25daf-140">다시 연결을 지원 하지 않는 뿐만 아니라 확장 모델을 변경으로 인해이 더 이상 지원 되지.</span><span class="sxs-lookup"><span data-stu-id="25daf-140">Due to changes to the scale-out model, as well as not supporting reconnects, this is no longer supported.</span></span> <span data-ttu-id="25daf-141">클라이언트가 서버에 연결 되 면 연결 기간에 대 한 동일한 서버 상호 작용 해야 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="25daf-141">Once the client connects to the server, it must interact with the same server for the duration of the connection.</span></span>

### <a name="single-hub-per-connection"></a><span data-ttu-id="25daf-142">단일 허브 연결당</span><span class="sxs-lookup"><span data-stu-id="25daf-142">Single hub per connection</span></span>

<span data-ttu-id="25daf-143">ASP.NET Core SignalR의 연결 모델이 간소화 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="25daf-143">In ASP.NET Core SignalR, the connection model has been simplified.</span></span> <span data-ttu-id="25daf-144">여러 허브에 대 한 액세스를 공유 하는 데 사용 되는 단일 연결 하지 않고 단일 허브에 직접 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25daf-144">Connections are made directly to a single hub, rather than a single connection being used to share access to multiple hubs.</span></span>

### <a name="streaming"></a><span data-ttu-id="25daf-145">스트리밍</span><span class="sxs-lookup"><span data-stu-id="25daf-145">Streaming</span></span>

<span data-ttu-id="25daf-146">ASP.NET Core SignalR 지원 [스트리밍 데이터](xref:signalr/streaming) 클라이언트에 허브에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="25daf-146">ASP.NET Core SignalR now supports [streaming data](xref:signalr/streaming) from the hub to the client.</span></span>

### <a name="state"></a><span data-ttu-id="25daf-147">시스템 상태</span><span class="sxs-lookup"><span data-stu-id="25daf-147">State</span></span>

<span data-ttu-id="25daf-148">진행 메시지에 대 한 지원 뿐만 아니라 클라이언트 허브 (HubState 라고도 함) 사이의 임의 상태를 전달 하는 기능, 없어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="25daf-148">The ability to pass arbitrary state between clients and the hub (often called HubState) has been removed, as well as support for progress messages.</span></span> <span data-ttu-id="25daf-149">지금은 허브 프록시 문자가 없는 경우</span><span class="sxs-lookup"><span data-stu-id="25daf-149">There is no counterpart of hub proxies at the moment.</span></span>

## <a name="differences-on-the-client"></a><span data-ttu-id="25daf-150">클라이언트의 차이점</span><span class="sxs-lookup"><span data-stu-id="25daf-150">Differences on the client</span></span>

### <a name="typescript"></a><span data-ttu-id="25daf-151">TypeScript</span><span class="sxs-lookup"><span data-stu-id="25daf-151">TypeScript</span></span>

<span data-ttu-id="25daf-152">ASP.NET Core SignalR 클라이언트 쓰여질 [TypeScript](https://www.typescriptlang.org/)합니다.</span><span class="sxs-lookup"><span data-stu-id="25daf-152">The ASP.NET Core SignalR client is written in [TypeScript](https://www.typescriptlang.org/).</span></span> <span data-ttu-id="25daf-153">사용 하는 경우 JavaScript 또는 TypeScript에서 작성할 수는 [JavaScript 클라이언트](xref:signalr/javascript-client)합니다.</span><span class="sxs-lookup"><span data-stu-id="25daf-153">You can write in JavaScript or TypeScript when using the [JavaScript client](xref:signalr/javascript-client).</span></span>

### <a name="the-javascript-client-is-hosted-at-npmhttpswwwnpmjscom"></a><span data-ttu-id="25daf-154">JavaScript 클라이언트에서 호스팅되는 [npm](https://www.npmjs.com/)</span><span class="sxs-lookup"><span data-stu-id="25daf-154">The JavaScript client is hosted at [npm](https://www.npmjs.com/)</span></span>

<span data-ttu-id="25daf-155">이전 버전에서는 Visual Studio의 NuGet 패키지를 통해 JavaScript 클라이언트가 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="25daf-155">In previous versions, the JavaScript client was obtained through a NuGet package in Visual Studio.</span></span> <span data-ttu-id="25daf-156">Core 버전에 대 한 합니다 [ @aspnet/signalr ](https://www.npmjs.com/package/@aspnet/signalr) npm 패키지는 JavaScript 라이브러리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="25daf-156">For the Core versions, the [@aspnet/signalr](https://www.npmjs.com/package/@aspnet/signalr) npm package contains the JavaScript libraries.</span></span> <span data-ttu-id="25daf-157">이 패키지에 포함 되지 합니다 **ASP.NET Core 웹 응용 프로그램** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="25daf-157">This package isn't included in the **ASP.NET Core Web Application** template.</span></span> <span data-ttu-id="25daf-158">Npm을 사용 하 여 설치 하는 `@aspnet/signalr` npm 패키지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25daf-158">Use npm to obtain and install the `@aspnet/signalr` npm package.</span></span>

```console
npm init -y
npm install @aspnet/signalr
```

### <a name="jquery"></a><span data-ttu-id="25daf-159">jQuery</span><span class="sxs-lookup"><span data-stu-id="25daf-159">jQuery</span></span>

<span data-ttu-id="25daf-160">JQuery에 대 한 종속성이 제거 되었습니다, 프로젝트에는 jQuery 계속 사용할 수 있지만.</span><span class="sxs-lookup"><span data-stu-id="25daf-160">The dependency on jQuery has been removed, however projects can still use jQuery.</span></span>

### <a name="javascript-client-method-syntax"></a><span data-ttu-id="25daf-161">JavaScript 클라이언트 메서드 구문</span><span class="sxs-lookup"><span data-stu-id="25daf-161">JavaScript client method syntax</span></span>

<span data-ttu-id="25daf-162">이전 버전의 SignalR에서 JavaScript 구문이 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="25daf-162">The JavaScript syntax has changed from the previous version of SignalR.</span></span> <span data-ttu-id="25daf-163">사용 하지 않고는 `$connection` 개체를 사용 하 여 연결 합니다 [HubConnectionBuilder](/javascript/api/%40aspnet/signalr/hubconnectionbuilder) API.</span><span class="sxs-lookup"><span data-stu-id="25daf-163">Rather than using the `$connection` object, create a connection using the [HubConnectionBuilder](/javascript/api/%40aspnet/signalr/hubconnectionbuilder) API.</span></span>

```javascript
const connection = new signalR.HubConnectionBuilder()
    .withUrl("/hub")
    .build();
```

<span data-ttu-id="25daf-164">사용 된 [에서](/javascript/api/@aspnet/signalr/HubConnection#on) 허브를 호출할 수 있는 클라이언트 메서드를 지정 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="25daf-164">Use the [on](/javascript/api/@aspnet/signalr/HubConnection#on) method to specify client methods that the hub can call.</span></span>

```javascript
connection.on("ReceiveMessage", (user, message) => {
    const msg = message.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
    const encodedMsg = user + " says " + msg;
    log(encodedMsg);
});
```

<span data-ttu-id="25daf-165">클라이언트 메서드를 만든 후 허브 연결을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="25daf-165">After creating the client method, start the hub connection.</span></span> <span data-ttu-id="25daf-166">체인을 [catch](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch) 메서드를 기록 하거나 오류를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="25daf-166">Chain a [catch](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch) method to log or handle errors.</span></span>

```javascript
connection.start().catch(err => console.error(err.toString()));
```

### <a name="hub-proxies"></a><span data-ttu-id="25daf-167">허브 프록시</span><span class="sxs-lookup"><span data-stu-id="25daf-167">Hub proxies</span></span>

<span data-ttu-id="25daf-168">허브 프록시 더 이상 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25daf-168">Hub proxies are no longer automatically generated.</span></span> <span data-ttu-id="25daf-169">메서드 이름에 전달 되는 대신 합니다 [호출할](/javascript/api/%40aspnet/signalr/hubconnection#invoke) 문자열로 API.</span><span class="sxs-lookup"><span data-stu-id="25daf-169">Instead, the method name is passed into the [invoke](/javascript/api/%40aspnet/signalr/hubconnection#invoke) API as a string.</span></span>

### <a name="net-and-other-clients"></a><span data-ttu-id="25daf-170">.NET 및 기타 클라이언트</span><span class="sxs-lookup"><span data-stu-id="25daf-170">.NET and other clients</span></span>

<span data-ttu-id="25daf-171">`Microsoft.AspNetCore.SignalR.Client` NuGet 패키지는 ASP.NET Core SignalR에 대 한.NET 클라이언트 라이브러리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="25daf-171">The `Microsoft.AspNetCore.SignalR.Client` NuGet package contains the .NET client libraries for ASP.NET Core SignalR.</span></span>

<span data-ttu-id="25daf-172">사용 된 [HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder) 을 작성 하는 허브에 대 한 연결의 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="25daf-172">Use the [HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder) to create and build an instance of a connection to a hub.</span></span>

```csharp
connection = new HubConnectionBuilder()
    .WithUrl("url")
    .Build();
```

## <a name="scaleout-differences"></a><span data-ttu-id="25daf-173">확장 차이점</span><span class="sxs-lookup"><span data-stu-id="25daf-173">Scaleout differences</span></span>

<span data-ttu-id="25daf-174">ASP.NET SignalR에는 SQL Server 및 Redis를 모두 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="25daf-174">ASP.NET SignalR supports both SQL Server and Redis.</span></span> <span data-ttu-id="25daf-175">ASP.NET Core SignalR에는 Azure SignalR Service 및 Redis를 모두 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="25daf-175">ASP.NET Core SignalR supports both Azure SignalR Service and Redis.</span></span>

### <a name="aspnet"></a><span data-ttu-id="25daf-176">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="25daf-176">ASP.NET</span></span>

* [<span data-ttu-id="25daf-177">Azure Service Bus로 SignalR 규모 확장</span><span class="sxs-lookup"><span data-stu-id="25daf-177">SignalR scaleout with Azure Service Bus</span></span>](/aspnet/signalr/overview/performance/scaleout-with-windows-azure-service-bus)
* [<span data-ttu-id="25daf-178">Redis로 SignalR 규모 확장</span><span class="sxs-lookup"><span data-stu-id="25daf-178">SignalR scaleout with Redis</span></span>](/aspnet/signalr/overview/performance/scaleout-with-redis)
* [<span data-ttu-id="25daf-179">SQL Server로 SignalR 규모 확장</span><span class="sxs-lookup"><span data-stu-id="25daf-179">SignalR scaleout with SQL Server</span></span>](/aspnet/signalr/overview/performance/scaleout-with-sql-server)

### <a name="aspnet-core"></a><span data-ttu-id="25daf-180">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="25daf-180">ASP.NET Core</span></span>

* [<span data-ttu-id="25daf-181">Azure SignalR Service</span><span class="sxs-lookup"><span data-stu-id="25daf-181">Azure SignalR Service</span></span>](/azure/azure-signalr/)

## <a name="additional-resources"></a><span data-ttu-id="25daf-182">추가 자료</span><span class="sxs-lookup"><span data-stu-id="25daf-182">Additional resources</span></span>

* [<span data-ttu-id="25daf-183">허브</span><span class="sxs-lookup"><span data-stu-id="25daf-183">Hubs</span></span>](xref:signalr/hubs)
* [<span data-ttu-id="25daf-184">JavaScript 클라이언트</span><span class="sxs-lookup"><span data-stu-id="25daf-184">JavaScript client</span></span>](xref:signalr/javascript-client)
* [<span data-ttu-id="25daf-185">.NET 클라이언트</span><span class="sxs-lookup"><span data-stu-id="25daf-185">.NET client</span></span>](xref:signalr/dotnet-client)
* [<span data-ttu-id="25daf-186">지원되는 플랫폼</span><span class="sxs-lookup"><span data-stu-id="25daf-186">Supported platforms</span></span>](xref:signalr/supported-platforms)
