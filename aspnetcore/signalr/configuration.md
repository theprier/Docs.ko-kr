---
title: ASP.NET Core SignalR 구성
author: tdykstra
description: ASP.NET Core SignalR 앱을 구성 하는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 07/31/2018
uid: signalr/configuration
ms.openlocfilehash: 32c0ad94fba09fa099c2ab4a6b1d6d79a5542d7f
ms.sourcegitcommit: a25b572eaed21791230c85416f449f66a405ec19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2018
ms.locfileid: "39396064"
---
# <a name="aspnet-core-signalr-configuration"></a><span data-ttu-id="66746-103">ASP.NET Core SignalR 구성</span><span class="sxs-lookup"><span data-stu-id="66746-103">ASP.NET Core SignalR configuration</span></span>

## <a name="jsonmessagepack-serialization-options"></a><span data-ttu-id="66746-104">JSON/MessagePack 직렬화 옵션</span><span class="sxs-lookup"><span data-stu-id="66746-104">JSON/MessagePack serialization options</span></span>

<span data-ttu-id="66746-105">ASP.NET Core SignalR 메시지 인코딩에 대 한 두 가지 프로토콜을 지원 합니다. [JSON](https://www.json.org/) 하 고 [MessagePack](https://msgpack.org/index.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="66746-105">ASP.NET Core SignalR supports two protocols for encoding messages: [JSON](https://www.json.org/) and [MessagePack](https://msgpack.org/index.html).</span></span> <span data-ttu-id="66746-106">각 프로토콜에 serialization 구성 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66746-106">Each protocol has serialization configuration options.</span></span>

<span data-ttu-id="66746-107">JSON serialization을 사용 하 여 서버에 구성할 수 있습니다 합니다 [AddJsonProtocol](/dotnet/api/microsoft.extensions.dependencyinjection.jsonprotocoldependencyinjectionextensions.addjsonprotocol) 후 추가할 수 있는 확장 메서드 [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr) 에서 프로그램 `Startup.ConfigureServices` 메서드.</span><span class="sxs-lookup"><span data-stu-id="66746-107">JSON serialization can be configured on the server using the [AddJsonProtocol](/dotnet/api/microsoft.extensions.dependencyinjection.jsonprotocoldependencyinjectionextensions.addjsonprotocol) extension method, which can be added after [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr) in your `Startup.ConfigureServices` method.</span></span> <span data-ttu-id="66746-108">합니다 `AddJsonProtocol` 메서드는 수신 하는 대리자는 `options` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-108">The `AddJsonProtocol` method takes a delegate that receives an `options` object.</span></span> <span data-ttu-id="66746-109">합니다 [PayloadSerializerSettings](/dotnet/api/microsoft.aspnetcore.signalr.jsonhubprotocoloptions.payloadserializersettings) 해당 개체에 대해 속성이 한 JSON.NET `JsonSerializerSettings` serialization 인수를 구성 하 고 값을 반환 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66746-109">The [PayloadSerializerSettings](/dotnet/api/microsoft.aspnetcore.signalr.jsonhubprotocoloptions.payloadserializersettings) property on that object is a JSON.NET `JsonSerializerSettings` object that can be used to configure serialization of arguments and return values.</span></span> <span data-ttu-id="66746-110">참조 된 [JSON.NET 설명서](https://www.newtonsoft.com/json/help/html/Introduction.htm) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="66746-110">See the [JSON.NET Documentation](https://www.newtonsoft.com/json/help/html/Introduction.htm) for more details.</span></span>

<span data-ttu-id="66746-111">예를 들어 속성 이름 "PascalCase" 기본 "camelCase" 이름 대신 사용할 serializer를 구성 하려면 다음 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="66746-111">As an example, to configure the serializer to use "PascalCase" property names, instead of the default "camelCase" names, use the following code:</span></span>

```csharp
services.AddSignalR()
    .AddJsonHubProtocol(options => {
        options.PayloadSerializerSettings.ContractResolver = 
        new DefaultContractResolver();
    });
```

<span data-ttu-id="66746-112">.NET 클라이언트에서 동일한 `AddJsonHubProtocol` 에 있는 확장 메서드 [HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder)합니다.</span><span class="sxs-lookup"><span data-stu-id="66746-112">In the .NET client, the same `AddJsonHubProtocol` extension method exists on [HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder).</span></span> <span data-ttu-id="66746-113">`Microsoft.Extensions.DependencyInjection` 확장 메서드를 해결 하려면 네임 스페이스를 가져올 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66746-113">The `Microsoft.Extensions.DependencyInjection` namespace must be imported to resolve the extension method:</span></span>

```csharp
// At the top of the file:
using Microsoft.Extensions.DependencyInjection;

// When constructing your connection:
var connection = new HubConnectionBuilder()
.AddJsonHubProtocol(options => {
    options.PayloadSerializerSettings.ContractResolver = 
        new DefaultContractResolver();
});
```

> [!NOTE]
> <span data-ttu-id="66746-114">이 이번에 JavaScript 클라이언트에서 JSON serialization을 구성 하는 것이 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="66746-114">It's not possible to configure JSON serialization in the JavaScript client at this time.</span></span>

### <a name="messagepack-serialization-options"></a><span data-ttu-id="66746-115">MessagePack 직렬화 옵션</span><span class="sxs-lookup"><span data-stu-id="66746-115">MessagePack serialization options</span></span>

<span data-ttu-id="66746-116">MessagePack serialization에 대 한 대리자를 제공 하 여 구성할 수 있습니다 합니다 [AddMessagePackProtocol](/dotnet/api/microsoft.extensions.dependencyinjection.msgpackprotocoldependencyinjectionextensions.addmessagepackprotocol) 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="66746-116">MessagePack serialization can be configured by providing a delegate to the [AddMessagePackProtocol](/dotnet/api/microsoft.extensions.dependencyinjection.msgpackprotocoldependencyinjectionextensions.addmessagepackprotocol) call.</span></span> <span data-ttu-id="66746-117">참조 [SignalR에서 MessagePack](xref:signalr/messagepackhubprotocol) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="66746-117">See [MessagePack in SignalR](xref:signalr/messagepackhubprotocol) for more details.</span></span>

> [!NOTE]
> <span data-ttu-id="66746-118">이 이번에 JavaScript 클라이언트에서 MessagePack serialization을 구성 하는 것이 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="66746-118">It's not possible to configure MessagePack serialization in the JavaScript client at this time.</span></span>

## <a name="configure-server-options"></a><span data-ttu-id="66746-119">서버 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="66746-119">Configure server options</span></span>

<span data-ttu-id="66746-120">다음 표에서 SignalR 허브를 구성 하는 것에 대 한 옵션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="66746-120">The following table describes options for configuring SignalR hubs:</span></span>

| <span data-ttu-id="66746-121">옵션</span><span class="sxs-lookup"><span data-stu-id="66746-121">Option</span></span> | <span data-ttu-id="66746-122">기본값</span><span class="sxs-lookup"><span data-stu-id="66746-122">Default Value</span></span> | <span data-ttu-id="66746-123">설명</span><span class="sxs-lookup"><span data-stu-id="66746-123">Description</span></span> |
| ------ | ------------- | ----------- |
| `HandshakeTimeout` | <span data-ttu-id="66746-124">15초</span><span class="sxs-lookup"><span data-stu-id="66746-124">15 seconds</span></span> | <span data-ttu-id="66746-125">클라이언트는이 시간 간격 내에서 초기 핸드셰이크 메시지를 보내지 않습니다, 경우에 연결이 닫혀 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66746-125">If the client doesn't send an initial handshake message within this time interval, the connection is closed.</span></span> <span data-ttu-id="66746-126">이것이 핸드셰이크 시간 초과 오류는 심각한 네트워크 대기 시간으로 인해 발생 하는 경우에 수정 해야 하는 고급 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-126">This is an advanced setting that should only be modified if handshake timeout errors are occurring due to severe network latency.</span></span> <span data-ttu-id="66746-127">핸드셰이크 프로세스에서 구체적으로 말하면에 대 한 참조를 [SignalR 허브 프로토콜 사양](https://github.com/aspnet/SignalR/blob/master/specs/HubProtocol.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="66746-127">For more detail on the handshake process, see the [SignalR Hub Protocol Specification](https://github.com/aspnet/SignalR/blob/master/specs/HubProtocol.md).</span></span> |
| `KeepAliveInterval` | <span data-ttu-id="66746-128">15초</span><span class="sxs-lookup"><span data-stu-id="66746-128">15 seconds</span></span> | <span data-ttu-id="66746-129">서버는이 간격 내에서 메시지를 전송 되지 않은, ping 메시지는 연결을 열어 두려면 자동으로 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="66746-129">If the server hasn't sent a message within this interval, a ping message is sent automatically to keep the connection open.</span></span> |
| `SupportedProtocols` | <span data-ttu-id="66746-130">설치 된 모든 프로토콜</span><span class="sxs-lookup"><span data-stu-id="66746-130">All installed protocols</span></span> | <span data-ttu-id="66746-131">이 허브에 의해 지원 되는 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-131">Protocols supported by this hub.</span></span> <span data-ttu-id="66746-132">기본적으로 서버에 등록 하는 모든 프로토콜 수 있지만 개별 허브에 대 한 특정 프로토콜을 사용 하지 않도록 설정 하려면이 목록에서 프로토콜을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66746-132">By default, all protocols registered on the server are allowed, but protocols can be removed from this list to disable specific protocols for individual hubs.</span></span> |
| `EnableDetailedErrors` | `false` | <span data-ttu-id="66746-133">경우 `true`자세한, Hub 메서드에서 예외가 throw 될 때 예외 메시지가 클라이언트로 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66746-133">If `true`, detailed exception messages are returned to clients when an exception is thrown in a Hub method.</span></span> <span data-ttu-id="66746-134">기본값은 `false`처럼 이러한 예외 메시지는 중요 한 정보를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66746-134">The default is `false`, as these exception messages can contain sensitive information.</span></span> |

<span data-ttu-id="66746-135">하는 옵션 대리자를 제공 하 여 모든 허브에 대 한 옵션을 구성할 수 있습니다 합니다 `AddSignalR` 에서 호출 `Startup.ConfigureServices`합니다.</span><span class="sxs-lookup"><span data-stu-id="66746-135">Options can be configured for all hubs by providing an options delegate to the `AddSignalR` call in `Startup.ConfigureServices`.</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddSignalR(hubOptions =>
    {
        hubOptions.EnableDetailedErrors = true;
        hubOptions.KeepAliveInterval = TimeSpan.FromMinutes(1);
    })
}
```

<span data-ttu-id="66746-136">단일 허브에 대 한 옵션에서 제공 하는 전역 옵션을 재정의 `AddSignalR` 를 사용 하 여 구성할 수 있습니다 [AddHubOptions\<T >](/dotnet/api/microsoft.extensions.dependencyinjection.huboptionsdependencyinjectionextensions.addhuboptions):</span><span class="sxs-lookup"><span data-stu-id="66746-136">Options for a single hub override the global options provided in `AddSignalR` and can be configured using [AddHubOptions\<T>](/dotnet/api/microsoft.extensions.dependencyinjection.huboptionsdependencyinjectionextensions.addhuboptions):</span></span>

```csharp
services.AddSignalR().AddHubOptions<MyHub>(options =>
{
    options.EnableDetailedErrors = true;
}
```

<span data-ttu-id="66746-137">사용 하 여 `HttpConnectionDispatcherOptions` 전송 및 메모리 버퍼 관리와 관련 된 고급 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66746-137">Use `HttpConnectionDispatcherOptions` to configure advanced settings related to transports and memory buffer management.</span></span> <span data-ttu-id="66746-138">이러한 옵션에 대 한 대리자를 전달 하 여 구성 됩니다 [MapHub\<T >](/dotnet/api/microsoft.aspnetcore.signalr.hubroutebuilder.maphub)합니다.</span><span class="sxs-lookup"><span data-stu-id="66746-138">These options are configured by passing a delegate to [MapHub\<T>](/dotnet/api/microsoft.aspnetcore.signalr.hubroutebuilder.maphub).</span></span>

| <span data-ttu-id="66746-139">옵션</span><span class="sxs-lookup"><span data-stu-id="66746-139">Option</span></span> | <span data-ttu-id="66746-140">기본값</span><span class="sxs-lookup"><span data-stu-id="66746-140">Default Value</span></span> | <span data-ttu-id="66746-141">설명</span><span class="sxs-lookup"><span data-stu-id="66746-141">Description</span></span> |
| ------ | ------------- | ----------- |
| `ApplicationMaxBufferSize` | <span data-ttu-id="66746-142">32KB</span><span class="sxs-lookup"><span data-stu-id="66746-142">32 KB</span></span> | <span data-ttu-id="66746-143">클라이언트에서 받은 바이트의 최대 수는 서버 버퍼입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-143">The maximum number of bytes received from the client that the server buffers.</span></span> <span data-ttu-id="66746-144">이 값을 늘리면 서버에서 큰 메시지를 받을 수 있지만 메모리 사용에 부정적인 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66746-144">Increasing this value allows the server to receive larger messages, but can negatively impact memory consumption.</span></span> |
| `AuthorizationData` | <span data-ttu-id="66746-145">자동으로 수집 된 데이터는 `Authorize` 은 허브 클래스에 적용 되는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-145">Data automatically gathered from the `Authorize` attributes applied to the Hub class.</span></span> | <span data-ttu-id="66746-146">목록을 [IAuthorizeData](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizedata) 클라이언트가 허브에 연결할 권한이 있는지 확인 하는 데 사용 되는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-146">A list of [IAuthorizeData](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizedata) objects used to determine if a client is authorized to connect to the hub.</span></span> |
| `TransportMaxBufferSize` | <span data-ttu-id="66746-147">32KB</span><span class="sxs-lookup"><span data-stu-id="66746-147">32 KB</span></span> | <span data-ttu-id="66746-148">앱에서 전송 된 바이트의 최대 수는 서버 버퍼입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-148">The maximum number of bytes sent by the app that the server buffers.</span></span> <span data-ttu-id="66746-149">이 값을 늘리면 더 큰 메시지를 보낼 수 있지만 메모리 사용에 부정적인 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66746-149">Increasing this value allows the server to send larger messages, but can negatively impact memory consumption.</span></span> |
| `Transports` | <span data-ttu-id="66746-150">모든 전송은 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66746-150">All Transports are enabled.</span></span> | <span data-ttu-id="66746-151">비트 마스크 `HttpTransportType` 전송을 제한할 수 있는 값을 클라이언트는 연결할 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66746-151">A bitmask of `HttpTransportType` values that can restrict the transports a client can use to connect.</span></span> |
| `LongPolling` | <span data-ttu-id="66746-152">다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66746-152">See below.</span></span> | <span data-ttu-id="66746-153">긴 폴링 전송 관련 추가 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-153">Additional options specific to the Long Polling transport.</span></span> |
| `WebSockets` | <span data-ttu-id="66746-154">다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66746-154">See below.</span></span> | <span data-ttu-id="66746-155">Websocket 전송으로 특정 추가 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-155">Additional options specific to the WebSockets transport.</span></span> |

<span data-ttu-id="66746-156">긴 폴링 전송을 사용 하 여 구성할 수 있는 추가 옵션에는 `LongPolling` 속성:</span><span class="sxs-lookup"><span data-stu-id="66746-156">The Long Polling transport has additional options that can be configured using the `LongPolling` property:</span></span>

| <span data-ttu-id="66746-157">옵션</span><span class="sxs-lookup"><span data-stu-id="66746-157">Option</span></span> | <span data-ttu-id="66746-158">기본값</span><span class="sxs-lookup"><span data-stu-id="66746-158">Default Value</span></span> | <span data-ttu-id="66746-159">설명</span><span class="sxs-lookup"><span data-stu-id="66746-159">Description</span></span> |
| ------ | ------------- | ----------- |
| `PollTimeout` | <span data-ttu-id="66746-160">90 초</span><span class="sxs-lookup"><span data-stu-id="66746-160">90 seconds</span></span> | <span data-ttu-id="66746-161">최대 기간 서버 단일 폴링 요청을 종료 하기 전에 클라이언트에 보낼 메시지를 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="66746-161">The maximum amount of time the server waits for a message to send to the client before terminating a single poll request.</span></span> <span data-ttu-id="66746-162">이 값을 줄이면 하면 클라이언트가 새 폴링 요청을 더 자주 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="66746-162">Decreasing this value causes the client to issue new poll requests more frequently.</span></span> |

<span data-ttu-id="66746-163">WebSocket 전송 사용 하 여 구성할 수 있는 추가 옵션에는 `WebSockets` 속성:</span><span class="sxs-lookup"><span data-stu-id="66746-163">The WebSocket transport has additional options that can be configured using the `WebSockets` property:</span></span>

| <span data-ttu-id="66746-164">옵션</span><span class="sxs-lookup"><span data-stu-id="66746-164">Option</span></span> | <span data-ttu-id="66746-165">기본값</span><span class="sxs-lookup"><span data-stu-id="66746-165">Default Value</span></span> | <span data-ttu-id="66746-166">설명</span><span class="sxs-lookup"><span data-stu-id="66746-166">Description</span></span> |
| ------ | ------------- | ----------- |
| `CloseTimeout` | <span data-ttu-id="66746-167">5초</span><span class="sxs-lookup"><span data-stu-id="66746-167">5 seconds</span></span> | <span data-ttu-id="66746-168">서버를 닫으면이 시간 간격 내에서 닫기에 실패 하면 클라이언트에서 연결이 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66746-168">After the server closes, if the client fails to close within this time interval, the connection is terminated.</span></span> |
| `SubProtocolSelector` | `null` | <span data-ttu-id="66746-169">설정에 사용할 수 있는 대리자를 `Sec-WebSocket-Protocol` 헤더를 사용자 지정 값입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-169">A delegate that can be used to set the `Sec-WebSocket-Protocol` header to a custom value.</span></span> <span data-ttu-id="66746-170">대리자 값 입력으로 클라이언트에서 요청을 받는 및 원하는 값을 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66746-170">The delegate receives the values requested by the client as input and is expected to return the desired value.</span></span> |

## <a name="configure-client-options"></a><span data-ttu-id="66746-171">클라이언트 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="66746-171">Configure client options</span></span>

<span data-ttu-id="66746-172">클라이언트 옵션에서 구성할 수 있습니다 합니다 `HubConnectionBuilder` 형식 (.NET 및 JavaScript 클라이언트에서 사용 가능), 뿐만 `HubConnection` 자체입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-172">Client options can be configured on the `HubConnectionBuilder` type (available in both .NET and JavaScript clients), as well as on the `HubConnection` itself.</span></span>

### <a name="configure-logging"></a><span data-ttu-id="66746-173">로깅 구성</span><span class="sxs-lookup"><span data-stu-id="66746-173">Configure logging</span></span>

<span data-ttu-id="66746-174">로깅을 사용 하 여.NET 클라이언트에서 구성 됩니다는 `ConfigureLogging` 메서드.</span><span class="sxs-lookup"><span data-stu-id="66746-174">Logging is configured in the .NET Client using the `ConfigureLogging` method.</span></span> <span data-ttu-id="66746-175">서버의 경우와 동일한 방식으로 로깅 공급자 및 필터를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66746-175">Logging providers and filters can be registered in the same way as they are on the server.</span></span> <span data-ttu-id="66746-176">참조를 [ASP.NET Core 로그인](xref:fundamentals/logging/index#how-to-add-providers) 자세한 정보에 대 한 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-176">See the [Logging in ASP.NET Core](xref:fundamentals/logging/index#how-to-add-providers) documentation for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="66746-177">로깅 공급자를 등록 하기 위해 필요한 패키지를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66746-177">In order to register Logging providers, you must install the necessary packages.</span></span> <span data-ttu-id="66746-178">참조 된 [기본 제공 로깅 공급자](xref:fundamentals/logging/index#built-in-logging-providers) 전체 목록은 문서 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-178">See the [Built-in logging providers](xref:fundamentals/logging/index#built-in-logging-providers) section of the docs for a full list.</span></span>

<span data-ttu-id="66746-179">예를 들어 콘솔 로깅을 사용 하려면 설치 된 `Microsoft.Extensions.Logging.Console` NuGet 패키지.</span><span class="sxs-lookup"><span data-stu-id="66746-179">For example, to enable Console logging, install the `Microsoft.Extensions.Logging.Console` NuGet package.</span></span> <span data-ttu-id="66746-180">호출 된 `AddConsole` 확장 메서드:</span><span class="sxs-lookup"><span data-stu-id="66746-180">Call the `AddConsole` extension method:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub")
    .ConfigureLogging(logging => {
        logging.SetMinimumLevel(LogLevel.Information);
        logging.AddConsole();
    })
    .Build();
```

<span data-ttu-id="66746-181">JavaScript 클라이언트에서 유사한 `configureLogging` 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66746-181">In the JavaScript client, a similar `configureLogging` method exists.</span></span> <span data-ttu-id="66746-182">제공 된 `LogLevel` 최소 수준의 로그를 생성 하는 메시지를 나타내는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-182">Provide a `LogLevel` value indicating the minimum level of log messages to produce.</span></span> <span data-ttu-id="66746-183">로그는 브라우저 콘솔 창에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66746-183">Logs are written to the browser console window.</span></span>

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub")
    .configureLogging(signalR.LogLevel.Information)
    .build();
```

> [!NOTE]
> <span data-ttu-id="66746-184">전적으로 로깅을 사용 하지 않으려면 지정할 `signalR.LogLevel.None` 에 `configureLogging` 메서드.</span><span class="sxs-lookup"><span data-stu-id="66746-184">To disable logging entirely, specify `signalR.LogLevel.None` in the `configureLogging` method.</span></span>

<span data-ttu-id="66746-185">JavaScript 클라이언트에서 사용 가능한 로그 수준은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="66746-185">Log levels available to the JavaScript client are listed below.</span></span> <span data-ttu-id="66746-186">메시지 로깅을 설정 로그 수준은 다음이 값 중 하나를 설정 **이상** 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-186">Setting the log level to one of these values enables logging of messages at **or above** that level.</span></span>

| <span data-ttu-id="66746-187">수준</span><span class="sxs-lookup"><span data-stu-id="66746-187">Level</span></span> | <span data-ttu-id="66746-188">설명</span><span class="sxs-lookup"><span data-stu-id="66746-188">Description</span></span> |
| ----- | ----------- |
| `None` | <span data-ttu-id="66746-189">메시지가 기록 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="66746-189">No messages are logged.</span></span> |
| `Critical` | <span data-ttu-id="66746-190">전체 앱에서 오류를 나타내는 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-190">Messages that indicate a failure in the entire app.</span></span> |
| `Error` | <span data-ttu-id="66746-191">현재 작업에서 오류를 나타내는 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-191">Messages that indicate a failure in the current operation.</span></span> |
| `Warning` | <span data-ttu-id="66746-192">사소한 문제를 나타내는 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-192">Messages that indicate a non-fatal problem.</span></span> |
| `Information` | <span data-ttu-id="66746-193">정보 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-193">Informational messages.</span></span> |
| `Debug` | <span data-ttu-id="66746-194">진단 메시지를 디버깅할 때 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="66746-194">Diagnostic messages useful for debugging.</span></span> |
| `Trace` | <span data-ttu-id="66746-195">특정 문제를 진단 하기 위한 매우 자세한 진단 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-195">Very detailed diagnostic messages designed for diagnosing specific issues.</span></span> |

### <a name="configure-allowed-transports"></a><span data-ttu-id="66746-196">허용 된 전송 구성</span><span class="sxs-lookup"><span data-stu-id="66746-196">Configure allowed transports</span></span>

<span data-ttu-id="66746-197">SignalR에서 사용 된 전송에서 구성할 수 있습니다 합니다 `WithUrl` 호출 (`withUrl` JavaScript에서).</span><span class="sxs-lookup"><span data-stu-id="66746-197">The transports used by SignalR can be configured in the `WithUrl` call (`withUrl` in JavaScript).</span></span> <span data-ttu-id="66746-198">값의 비트 OR `HttpTransportType` 만 특정된 전송 모드를 사용 하도록 클라이언트를 제한 하려면 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66746-198">A bitwise-OR of the values of `HttpTransportType` can be used to restrict the client to only use the specified transports.</span></span> <span data-ttu-id="66746-199">모든 전송에서는 기본적으로 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66746-199">All transports are enabled by default.</span></span>

<span data-ttu-id="66746-200">예를 들어 Server-Sent 이벤트 전송 하지 않으려면 하지만 Websocket 및 Long Polling 연결 허용:</span><span class="sxs-lookup"><span data-stu-id="66746-200">For example, to disable the Server-Sent Events transport, but allow WebSockets and Long Polling connections:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", HttpTransportType.WebSockets | HttpTransportType.LongPolling)
    .Build();
```

<span data-ttu-id="66746-201">JavaScript 클라이언트에서 전송 설정 하 여 구성 합니다 `transport` 필드에 제공 되는 옵션 개체에 `withUrl`:</span><span class="sxs-lookup"><span data-stu-id="66746-201">In the JavaScript client, transports are configured by setting the `transport` field on the options object provided to `withUrl`:</span></span>

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub", { transport: signalR.HttpTransportType.WebSockets | signalR.HttpTransportType.LongPolling })
    .build();
```

### <a name="configure-bearer-authentication"></a><span data-ttu-id="66746-202">전달자 인증 구성</span><span class="sxs-lookup"><span data-stu-id="66746-202">Configure bearer authentication</span></span>

<span data-ttu-id="66746-203">SignalR 요청과 함께 인증 데이터를 제공 하려면 사용 합니다 `AccessTokenProvider` 옵션 (`accessTokenFactory` JavaScript에서) 원하는 액세스 토큰을 반환 하는 함수를 지정 하려면.</span><span class="sxs-lookup"><span data-stu-id="66746-203">To provide authentication data along with SignalR requests, use the `AccessTokenProvider` option (`accessTokenFactory` in JavaScript) to specify a function that returns the desired access token.</span></span> <span data-ttu-id="66746-204">.NET 클라이언트에서이 액세스 토큰으로 전달 되어 HTTP "전달자 인증" 토큰 (사용 하는 `Authorization` 형식의 헤더 `Bearer`).</span><span class="sxs-lookup"><span data-stu-id="66746-204">In the .NET Client, this access token is passed in as an HTTP "Bearer Authentication" token (Using the `Authorization` header with a type of `Bearer`).</span></span> <span data-ttu-id="66746-205">JavaScript 클라이언트에서 액세스 토큰을 전달자 토큰으로 사용 되는 **제외한** 경우 Api 브라우저 (특히 Server-Sent 이벤트 및 Websocket 요청)에 대 한 헤더를 적용 하는 기능을 제한 하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-205">In the JavaScript client, the access token is used as a Bearer token, **except** in a few cases where browser APIs restrict the ability to apply headers (specifically, in Server-Sent Events and WebSockets requests).</span></span> <span data-ttu-id="66746-206">이러한 경우 액세스 토큰은 쿼리 문자열 값으로 제공 됩니다 `access_token`합니다.</span><span class="sxs-lookup"><span data-stu-id="66746-206">In these cases, the access token is provided as a query string value `access_token`.</span></span>

<span data-ttu-id="66746-207">.NET 클라이언트에서를 `AccessTokenProvider` 의 옵션 대리자를 사용 하 여 옵션을 지정할 수 있습니다 `WithUrl`:</span><span class="sxs-lookup"><span data-stu-id="66746-207">In the .NET client, the `AccessTokenProvider` option can be specified using the options delegate in `WithUrl`:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options => {
        options.AccessTokenProvider = async () => {
            // Get and return the access token.
        }
    })
    .Build();
```

<span data-ttu-id="66746-208">JavaScript 클라이언트에서 액세스 토큰을 설정 하 여 구성 됩니다 합니다 `accessTokenFactory` 필드에서 옵션 개체에 `withUrl`:</span><span class="sxs-lookup"><span data-stu-id="66746-208">In the JavaScript client, the access token is configured by setting the `accessTokenFactory` field on the options object in `withUrl`:</span></span>

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub", {
        accessTokenFactory: () => {
            // Get and return the access token.
            // This function can return a JavaScript Promise if asynchronous
            // logic is required to retrieve the access token.
        }
    })
    .build();
```

### <a name="configure-timeout-and-keep-alive-options"></a><span data-ttu-id="66746-209">제한 시간 및 연결 유지 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="66746-209">Configure timeout and keep-alive options</span></span>

<span data-ttu-id="66746-210">제한 시간 및 유지 동작 구성에 대 한 추가 옵션에서 사용할 수는 `HubConnection` 개체 자체:</span><span class="sxs-lookup"><span data-stu-id="66746-210">Additional options for configuring timeout and keep-alive behavior are available on the `HubConnection` object itself:</span></span>

| <span data-ttu-id="66746-211">.NET 옵션</span><span class="sxs-lookup"><span data-stu-id="66746-211">.NET Option</span></span> | <span data-ttu-id="66746-212">JavaScript 옵션</span><span class="sxs-lookup"><span data-stu-id="66746-212">JavaScript Option</span></span> | <span data-ttu-id="66746-213">기본값</span><span class="sxs-lookup"><span data-stu-id="66746-213">Default Value</span></span> | <span data-ttu-id="66746-214">설명</span><span class="sxs-lookup"><span data-stu-id="66746-214">Description</span></span> |
| ----------- | ----------------- | ------------- | ----------- |
| `ServerTimeout` | `serverTimeoutInMilliseconds` | <span data-ttu-id="66746-215">30 초 (30000 밀리초)</span><span class="sxs-lookup"><span data-stu-id="66746-215">30 seconds (30,000 milliseconds)</span></span> | <span data-ttu-id="66746-216">서버 작업에 대 한 제한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-216">Timeout for server activity.</span></span> <span data-ttu-id="66746-217">클라이언트 연결이 끊어진 서버 및 트리거 고려 서버는이 간격에 메시지를 전송 되지 않은, 경우 합니다 `Closed` 이벤트 (`onclose` JavaScript에서).</span><span class="sxs-lookup"><span data-stu-id="66746-217">If the server hasn't sent a message in this interval, the client considers the server disconnected and triggers the `Closed` event (`onclose` in JavaScript).</span></span> |
| `HandshakeTimeout` | <span data-ttu-id="66746-218">구성할 수 없음</span><span class="sxs-lookup"><span data-stu-id="66746-218">Not configurable</span></span> | <span data-ttu-id="66746-219">15초</span><span class="sxs-lookup"><span data-stu-id="66746-219">15 seconds</span></span> | <span data-ttu-id="66746-220">초기 서버 핸드셰이크에 대 한 제한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-220">Timeout for initial server handshake.</span></span> <span data-ttu-id="66746-221">서버는이 간격의 핸드셰이크 응답을 보내지 않습니다, 클라이언트 취소 트리거와 핸드셰이크를 `Closed` 이벤트 (`onclose` JavaScript에서).</span><span class="sxs-lookup"><span data-stu-id="66746-221">If the server doesn't send a handshake response in this interval, the client cancels the handshake and triggers the `Closed` event (`onclose` in JavaScript).</span></span> <span data-ttu-id="66746-222">이것이 핸드셰이크 시간 초과 오류는 심각한 네트워크 대기 시간으로 인해 발생 하는 경우에 수정 해야 하는 고급 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-222">This is an advanced setting that should only be modified if handshake timeout errors are occurring due to severe network latency.</span></span> <span data-ttu-id="66746-223">핸드셰이크 프로세스에서 구체적으로 말하면에 대 한 참조를 [SignalR 허브 프로토콜 사양](https://github.com/aspnet/SignalR/blob/master/specs/HubProtocol.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="66746-223">For more detail on the Handshake process, see the [SignalR Hub Protocol Specification](https://github.com/aspnet/SignalR/blob/master/specs/HubProtocol.md).</span></span> |

<span data-ttu-id="66746-224">.NET 클라이언트에서 제한 시간 값으로 지정 됩니다 `TimeSpan` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-224">In the .NET Client, timeout values are specified as `TimeSpan` values.</span></span> <span data-ttu-id="66746-225">JavaScript 클라이언트에서 제한 시간 값은 지속 시간 (밀리초) 나타내는 숫자로 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66746-225">In the JavaScript client, timeout values are specified as a number indicating the duration in milliseconds.</span></span>

### <a name="configure-additional-options"></a><span data-ttu-id="66746-226">추가 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="66746-226">Configure additional options</span></span>

<span data-ttu-id="66746-227">추가 옵션에서 구성할 수 있습니다 합니다 `WithUrl` (`withUrl` javascript에서) 메서드를 `HubConnectionBuilder`:</span><span class="sxs-lookup"><span data-stu-id="66746-227">Additional options can be configured in the `WithUrl` (`withUrl` in JavaScript) method on `HubConnectionBuilder`:</span></span>

| <span data-ttu-id="66746-228">.NET 옵션</span><span class="sxs-lookup"><span data-stu-id="66746-228">.NET Option</span></span> | <span data-ttu-id="66746-229">JavaScript 옵션</span><span class="sxs-lookup"><span data-stu-id="66746-229">JavaScript Option</span></span> | <span data-ttu-id="66746-230">기본값</span><span class="sxs-lookup"><span data-stu-id="66746-230">Default Value</span></span> | <span data-ttu-id="66746-231">설명</span><span class="sxs-lookup"><span data-stu-id="66746-231">Description</span></span> |
| ----------- | ----------------- | ------------- | ----------- |
| `AccessTokenProvider` | `accessTokenFactory` | `null` | <span data-ttu-id="66746-232">HTTP 요청에서 전달자 인증 토큰으로 제공 되는 문자열을 반환 하는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-232">A function returning a string that is provided as a Bearer authentication token in HTTP requests.</span></span> |
| `SkipNegotiation` | `skipNegotiation` | `false` | <span data-ttu-id="66746-233">이 값을 설정 `true` 협상 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="66746-233">Set this to `true` to skip the negotiation step.</span></span> <span data-ttu-id="66746-234">**Websocket 전송이 사용된만 전송 하는 경우에 지원**합니다.</span><span class="sxs-lookup"><span data-stu-id="66746-234">**Only supported when the WebSockets transport is the only enabled transport**.</span></span> <span data-ttu-id="66746-235">Azure SignalR Service를 사용 하는 경우에이 설정을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="66746-235">This setting can't be enabled when using the Azure SignalR Service.</span></span> |
| `ClientCertificates` | <span data-ttu-id="66746-236">구성 가능 \*</span><span class="sxs-lookup"><span data-stu-id="66746-236">Not configurable \*</span></span> | <span data-ttu-id="66746-237">Empty</span><span class="sxs-lookup"><span data-stu-id="66746-237">Empty</span></span> | <span data-ttu-id="66746-238">요청을 인증 하는 보내도록 TLS 인증서의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-238">A collection of TLS certificates to send to authenticate requests.</span></span> |
| `Cookies` | <span data-ttu-id="66746-239">구성 가능 \*</span><span class="sxs-lookup"><span data-stu-id="66746-239">Not configurable \*</span></span> | <span data-ttu-id="66746-240">Empty</span><span class="sxs-lookup"><span data-stu-id="66746-240">Empty</span></span> | <span data-ttu-id="66746-241">모든 HTTP 요청과 함께 보낼 HTTP 쿠키의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-241">A collection of HTTP cookies to send with every HTTP request.</span></span> |
| `Credentials` | <span data-ttu-id="66746-242">구성 가능 \*</span><span class="sxs-lookup"><span data-stu-id="66746-242">Not configurable \*</span></span> | <span data-ttu-id="66746-243">Empty</span><span class="sxs-lookup"><span data-stu-id="66746-243">Empty</span></span> | <span data-ttu-id="66746-244">모든 HTTP 요청과 함께 보낼 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-244">Credentials to send with every HTTP request.</span></span> |
| `CloseTimeout` | <span data-ttu-id="66746-245">구성 가능 \*</span><span class="sxs-lookup"><span data-stu-id="66746-245">Not configurable \*</span></span> | <span data-ttu-id="66746-246">5초</span><span class="sxs-lookup"><span data-stu-id="66746-246">5 seconds</span></span> | <span data-ttu-id="66746-247">Websocket에만 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="66746-247">WebSockets only.</span></span> <span data-ttu-id="66746-248">최대 기간 클라이언트 닫기 요청을 승인 하기 위해 서버에 대해 닫는 태그 뒤 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="66746-248">The maximum amount of time the client waits after closing for the server to acknowledge the close request.</span></span> <span data-ttu-id="66746-249">서버는이 시간 내 닫기를 승인 하지 않습니다, 경우에 클라이언트 연결을 끊습니다.</span><span class="sxs-lookup"><span data-stu-id="66746-249">If the server doesn't acknowledge the close within this time, the client disconnects.</span></span> |
| `Headers` | <span data-ttu-id="66746-250">구성 가능 \*</span><span class="sxs-lookup"><span data-stu-id="66746-250">Not configurable \*</span></span> | <span data-ttu-id="66746-251">Empty</span><span class="sxs-lookup"><span data-stu-id="66746-251">Empty</span></span> | <span data-ttu-id="66746-252">모든 HTTP 요청과 함께 보낼 추가 HTTP 헤더의 사전입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-252">A dictionary of additional HTTP headers to send with every HTTP request.</span></span> |
| `HttpMessageHandlerFactory` | <span data-ttu-id="66746-253">구성 가능 \*</span><span class="sxs-lookup"><span data-stu-id="66746-253">Not configurable \*</span></span> | `null` | <span data-ttu-id="66746-254">구성 또는 교체를 사용할 수 있는 대리자를 `HttpMessageHandler` HTTP 요청을 보내는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="66746-254">A delegate that can be used to configure or replace the `HttpMessageHandler` used to send HTTP requests.</span></span> <span data-ttu-id="66746-255">WebSocket 연결에 대 한 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66746-255">Not used for WebSocket connections.</span></span> <span data-ttu-id="66746-256">이 대리자는 null이 아닌 값을 반환 해야 하 고 기본 값을 매개 변수로 수신.</span><span class="sxs-lookup"><span data-stu-id="66746-256">This delegate must return a non-null value, and it receives the default value as a parameter.</span></span> <span data-ttu-id="66746-257">기본값에서 설정을 수정 하 고 반환 하는 등 또는 완전히 새로운 반환 `HttpMessageHandler` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="66746-257">Either modify settings on that default value and return it, or return a completely new `HttpMessageHandler` instance.</span></span> |
| `Proxy` | <span data-ttu-id="66746-258">구성 가능 \*</span><span class="sxs-lookup"><span data-stu-id="66746-258">Not configurable \*</span></span> | `null` | <span data-ttu-id="66746-259">HTTP 요청을 보낼 때 사용할 HTTP 프록시입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-259">An HTTP proxy to use when sending HTTP requests.</span></span> |
| `UseDefaultCredentials` | <span data-ttu-id="66746-260">구성 가능 \*</span><span class="sxs-lookup"><span data-stu-id="66746-260">Not configurable \*</span></span> | `false` | <span data-ttu-id="66746-261">HTTP 및 WebSockets 요청에 대 한 기본 자격 증명을 보내려고이 부울 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="66746-261">Set this boolean to send the default credentials for HTTP and WebSockets requests.</span></span> <span data-ttu-id="66746-262">이 통해 Windows 인증을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="66746-262">This enables the use of Windows authentication.</span></span> |
| `WebSocketConfiguration` | <span data-ttu-id="66746-263">구성 가능 \*</span><span class="sxs-lookup"><span data-stu-id="66746-263">Not configurable \*</span></span> | `null` | <span data-ttu-id="66746-264">추가 WebSocket 옵션을 구성 하는 대리자입니다.</span><span class="sxs-lookup"><span data-stu-id="66746-264">A delegate that can be used to configure additional WebSocket options.</span></span> <span data-ttu-id="66746-265">인스턴스를 받아서 [ClientWebSocketOptions](/dotnet/api/system.net.websockets.clientwebsocketoptions) 옵션을 구성 하려면 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66746-265">Receives an instance of [ClientWebSocketOptions](/dotnet/api/system.net.websockets.clientwebsocketoptions) that can be used to configure the options.</span></span> |

<span data-ttu-id="66746-266">별표 (\*)로 표시 하는 옵션은 Api 브라우저의 제한으로 인해 JavaScript 클라이언트에서 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66746-266">Options marked with an asterisk (\*) aren't configurable in the JavaScript client, due to limitations in browser APIs.</span></span>

<span data-ttu-id="66746-267">.NET 클라이언트에서 이러한 옵션은 옵션 대리자를 제공 하 여 수정할 수 `WithUrl`:</span><span class="sxs-lookup"><span data-stu-id="66746-267">In the .NET Client, these options can be modified by the options delegate provided to `WithUrl`:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options => {
        options.Headers["Foo"] = "Bar";
        options.Cookies.Add(new Cookie(/* ... */);
        options.ClientCertificates.Add(/* ... */);
    })
    .Build();
```

<span data-ttu-id="66746-268">JavaScript 클라이언트에서 이러한 옵션을 제공 하는 JavaScript 개체에 제공할 수 있습니다 `withUrl`:</span><span class="sxs-lookup"><span data-stu-id="66746-268">In the JavaScript Client, these options can be provided in a JavaScript object provided to `withUrl`:</span></span>

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub", {
        skipNegotiation: true,
        transport: signalR.HttpTransportType.WebSockets
    });
    .build();
```

## <a name="additional-resources"></a><span data-ttu-id="66746-269">추가 자료</span><span class="sxs-lookup"><span data-stu-id="66746-269">Additional resources</span></span>

* <xref:tutorials/signalr>
* <xref:signalr/hubs>
* <xref:signalr/javascript-client>
* <xref:signalr/dotnet-client>
* <xref:signalr/messagepackhubprotocol>
* <xref:signalr/supported-platforms>
