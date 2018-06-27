---
title: ASP.NET SignalR Core 구성
author: rachelappel
description: ASP.NET Core SignalR 응용 프로그램을 구성 하는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: rachelap
ms.custom: mvc
ms.date: 06/30/2018
uid: signalr/configuration
ms.openlocfilehash: 167b8828efd093d755aeb1c91e080dbd22b5d485
ms.sourcegitcommit: 356c8d394aaf384c834e9c90cabab43bfe36e063
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2018
ms.locfileid: "36961989"
---
# <a name="aspnet-core-signalr-configuration"></a><span data-ttu-id="b6725-103">ASP.NET SignalR Core 구성</span><span class="sxs-lookup"><span data-stu-id="b6725-103">ASP.NET Core SignalR configuration</span></span>

## <a name="jsonmessagepack-serialization-options"></a><span data-ttu-id="b6725-104">JSON/MessagePack 직렬화 옵션</span><span class="sxs-lookup"><span data-stu-id="b6725-104">JSON/MessagePack serialization options</span></span>

<span data-ttu-id="b6725-105">ASP.NET Core SignalR 메시지 인코딩에 대 한 두 프로토콜을 지원: [JSON](https://www.json.org/) 및 [MessagePack](https://msgpack.org/index.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-105">ASP.NET Core SignalR supports two protocols for encoding messages: [JSON](https://www.json.org/) and [MessagePack](https://msgpack.org/index.html).</span></span> <span data-ttu-id="b6725-106">각 프로토콜에 serialization 구성 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-106">Each protocol has serialization configuration options.</span></span>

<span data-ttu-id="b6725-107">JSON serialization을 사용 하 여 서버에 구성할 수는 [ `AddJsonProtocol` ](/dotnet/api/microsoft.extensions.dependencyinjection.jsonprotocoldependencyinjectionextensions.addjsonprotocol) 뒤에 추가할 수 있는 확장 메서드를 [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr) 에 프로그램 `Startup.ConfigureServices` 메서드.</span><span class="sxs-lookup"><span data-stu-id="b6725-107">JSON serialization can be configured on the server using the [`AddJsonProtocol`](/dotnet/api/microsoft.extensions.dependencyinjection.jsonprotocoldependencyinjectionextensions.addjsonprotocol) extension method, which can be added after [AddSignalR](/dotnet/api/microsoft.extensions.dependencyinjection.signalrdependencyinjectionextensions.addsignalr) in your `Startup.ConfigureServices` method.</span></span> <span data-ttu-id="b6725-108">`AddJsonProtocol` 메서드는 수신 하는 대리자는 `options` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-108">The `AddJsonProtocol` method takes a delegate that receives an `options` object.</span></span> <span data-ttu-id="b6725-109">[ `PayloadSerializerSettings` ](/dotnet/api/microsoft.aspnetcore.signalr.jsonhubprotocoloptions.payloadserializersettings) 해당 개체의 속성은 한 JSON.NET `JsonSerializerSettings` serialization의 인수를 구성 하 고 값을 반환 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-109">The [`PayloadSerializerSettings`](/dotnet/api/microsoft.aspnetcore.signalr.jsonhubprotocoloptions.payloadserializersettings) property on that object is a JSON.NET `JsonSerializerSettings` object that can be used to configure serialization of arguments and return values.</span></span> <span data-ttu-id="b6725-110">참조는 [JSON.NET 설명서](https://www.newtonsoft.com/json/help/html/Introduction.htm) 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-110">See the [JSON.NET Documentation](https://www.newtonsoft.com/json/help/html/Introduction.htm) for more details.</span></span>

<span data-ttu-id="b6725-111">예를 들어, "표시 방법이 PascalCase" 속성 이름은 기본 "camelCase" 이름 대신 사용 하는 serializer를 구성 하려면 다음 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-111">As an example, to configure the serializer to use "PascalCase" property names, instead of the default "camelCase" names, use the following code:</span></span>

```csharp
services.AddSignalR()
    .AddJsonHubProtocol(options => {
        options.PayloadSerializerSettings.ContractResolver = 
        new DefaultContractResolver();
    });
```

<span data-ttu-id="b6725-112">동일한.NET 클라이언트에서 `AddJsonHubProtocol` 에 확장 메서드가 있는 [HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder)합니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-112">In the .NET client, the same `AddJsonHubProtocol` extension method exists on [HubConnectionBuilder](/dotnet/api/microsoft.aspnetcore.signalr.client.hubconnectionbuilder).</span></span> <span data-ttu-id="b6725-113">`Microsoft.Extensions.DependencyInjection` 확장 메서드를 해결 하려면 네임 스페이스를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-113">The `Microsoft.Extensions.DependencyInjection` namespace must be imported to resolve the extension method:</span></span>

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
> <span data-ttu-id="b6725-114">이 이번에는 JSON serialization JavaScript 클라이언트에서 구성 하는 것이 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-114">It's not possible to configure JSON serialization in the JavaScript client at this time.</span></span>

### <a name="messagepack-serialization-options"></a><span data-ttu-id="b6725-115">MessagePack 직렬화 옵션</span><span class="sxs-lookup"><span data-stu-id="b6725-115">MessagePack serialization options</span></span>

<span data-ttu-id="b6725-116">대리자를 제공 하 여 MessagePack serialization을 구성할 수 있습니다는 [AddMessagePackProtocol](/dotnet/api/microsoft.extensions.dependencyinjection.msgpackprotocoldependencyinjectionextensions.addmessagepackprotocol) 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-116">MessagePack serialization can be configured by providing a delegate to the [AddMessagePackProtocol](/dotnet/api/microsoft.extensions.dependencyinjection.msgpackprotocoldependencyinjectionextensions.addmessagepackprotocol) call.</span></span> <span data-ttu-id="b6725-117">참조 [MessagePack SignalR에서](xref:signalr/messagepackhubprotocol) 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-117">See [MessagePack in SignalR](xref:signalr/messagepackhubprotocol) for more details.</span></span>

> [!NOTE]
> <span data-ttu-id="b6725-118">이 이번에는 JavaScript 클라이언트에서 MessagePack serialization을 구성 하는 것이 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-118">It's not possible to configure MessagePack serialization in the JavaScript client at this time.</span></span>

## <a name="configure-server-options"></a><span data-ttu-id="b6725-119">서버 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="b6725-119">Configure server options</span></span>

<span data-ttu-id="b6725-120">다음 표에서 SignalR 허브를 구성 하기 위한 옵션을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-120">The following table describes options for configuring SignalR hubs:</span></span>

| <span data-ttu-id="b6725-121">옵션</span><span class="sxs-lookup"><span data-stu-id="b6725-121">Option</span></span> | <span data-ttu-id="b6725-122">설명</span><span class="sxs-lookup"><span data-stu-id="b6725-122">Description</span></span> |
| ------ | ----------- |
| `HandshakeTimeout` | <span data-ttu-id="b6725-123">클라이언트는이 시간 간격 내에서 초기 핸드셰이크 메시지를 보내지 않습니다, 연결이 닫혀 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-123">If the client doesn't send an initial handshake message within this time interval, the connection is closed.</span></span> |
| `KeepAliveInterval` | <span data-ttu-id="b6725-124">이 간격 내에서 메시지를 전송 하는 작업 서버 하지 않은 경우 ping 메시지 연결을 유지 하려면 자동으로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-124">If the server hasn't sent a message within this interval, a ping message is sent automatically to keep the connection open.</span></span> |
| `SupportedProtocols` | <span data-ttu-id="b6725-125">이 허브에서 지 원하는 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-125">Protocols supported by this hub.</span></span> <span data-ttu-id="b6725-126">기본적으로 서버에 등록 하는 모든 프로토콜을 사용할 수 있지만 프로토콜 개별 허브에 대 한 특정 프로토콜을 사용 하지 않도록 설정 하려면이 목록에서 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-126">By default, all protocols registered on the server are allowed, but protocols can be removed from this list to disable specific protocols for individual hubs.</span></span> |
| `EnableDetailedErrors` | <span data-ttu-id="b6725-127">경우 `true`, 자세한 허브 메서드에서 예외가 throw 되 면 클라이언트에 예외 메시지가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-127">If `true`, detailed exception messages are returned to clients when an exception is thrown in a Hub method.</span></span> <span data-ttu-id="b6725-128">기본값은 `false`이러한 예외 메시지에는 중요 한 정보가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-128">The default is `false`, as these exception messages can contain sensitive information.</span></span> |

<span data-ttu-id="b6725-129">하는 옵션 대리자를 제공 하 여 모든 허브에 대 한 옵션을 구성할 수 있습니다는 `AddSignalR` 에서 호출 `Startup.ConfigureServices`합니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-129">Options can be configured for all hubs by providing an options delegate to the `AddSignalR` call in `Startup.ConfigureServices`.</span></span>

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

<span data-ttu-id="b6725-130">단일 허브에 대 한 옵션에 제공 된 전역 옵션 재정의 `AddSignalR` 를 사용 하 여 구성할 수 있습니다 및 [ `AddHubOptions<T>` ](/dotnet/api/microsoft.extensions.dependencyinjection.huboptionsdependencyinjectionextensions.addhuboptions):</span><span class="sxs-lookup"><span data-stu-id="b6725-130">Options for a single hub override the global options provided in `AddSignalR` and can be configured using [`AddHubOptions<T>`](/dotnet/api/microsoft.extensions.dependencyinjection.huboptionsdependencyinjectionextensions.addhuboptions):</span></span>

```csharp
services.AddSignalR().AddHubOptions<MyHub>(options =>
{
    options.EnableDetailedErrors = true;
}
```

<span data-ttu-id="b6725-131">사용 하 여 `HttpConnectionDispatcherOptions` 전송 및 메모리 버퍼 관리와 관련 된 고급 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-131">Use `HttpConnectionDispatcherOptions` to configure advanced settings related to transports and memory buffer management.</span></span> <span data-ttu-id="b6725-132">이러한 옵션은 대리자를 전달 하 여 구성 되어 [ `MapHub<T>` ](/dotnet/api/microsoft.aspnetcore.signalr.hubroutebuilder.maphub)합니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-132">These options are configured by passing a delegate to [`MapHub<T>`](/dotnet/api/microsoft.aspnetcore.signalr.hubroutebuilder.maphub).</span></span>

| <span data-ttu-id="b6725-133">옵션</span><span class="sxs-lookup"><span data-stu-id="b6725-133">Option</span></span> | <span data-ttu-id="b6725-134">설명</span><span class="sxs-lookup"><span data-stu-id="b6725-134">Description</span></span> |
| ------ | ----------- |
| `ApplicationMaxBufferSize` | <span data-ttu-id="b6725-135">클라이언트에서 받은 바이트의 최대 수 있는 서버 버퍼입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-135">The maximum number of bytes received from the client that the server buffers.</span></span> <span data-ttu-id="b6725-136">이 값을 늘리면 서버를 더 큰 메시지를 받을 수 있지만 메모리 사용에 부정적인 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-136">Increasing this value allows the server to receive larger messages, but can negatively impact memory consumption.</span></span> <span data-ttu-id="b6725-137">기본값은 32KB입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-137">The default value is 32KB.</span></span> |
| `AuthorizationData` | <span data-ttu-id="b6725-138">목록이 [ `IAuthorizeData` ](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizedata) 클라이언트가 허브에 연결할 권한이 있는지 확인 하는 데 사용 되는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-138">A list of [`IAuthorizeData`](/dotnet/api/microsoft.aspnetcore.authorization.iauthorizedata) objects used to determine if a client is authorized to connect to the hub.</span></span> <span data-ttu-id="b6725-139">기본적으로이 값으로 채워집니다에서 `Authorize` 허브 클래스에 적용 된 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-139">By default, this is populated with values from the `Authorize` attributes applied to the Hub class.</span></span> |
| `TransportMaxBufferSize` | <span data-ttu-id="b6725-140">응용 프로그램에서 보낸 바이트의 최대 수 있는 서버 버퍼입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-140">The maximum number of bytes sent by the app that the server buffers.</span></span> <span data-ttu-id="b6725-141">이 값을 늘리면 서버를 더 큰 메시지를 보낼 수 있지만 메모리 사용에 부정적인 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-141">Increasing this value allows the server to send larger messages, but can negatively impact memory consumption.</span></span> <span data-ttu-id="b6725-142">기본값은 32KB입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-142">The default value is 32KB.</span></span> |
| `Transports` | <span data-ttu-id="b6725-143">비트 마스크 `HttpTransportType` 전송을 제한할 수 있는 값 클라이언트가 연결 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-143">A bitmask of `HttpTransportType` values that can restrict the transports a client can use to connect.</span></span> <span data-ttu-id="b6725-144">모든 전송 기본적으로 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-144">All transports are enabled by default.</span></span> |
| `LongPolling` | <span data-ttu-id="b6725-145">긴 폴링 전송에만 추가 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-145">Additional options specific to the Long Polling transport.</span></span> |
| `WebSockets` | <span data-ttu-id="b6725-146">Websocket 전송에만 추가 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-146">Additional options specific to the WebSockets transport.</span></span> |

<span data-ttu-id="b6725-147">긴 폴링 전송을 사용 하 여 구성할 수 있는 추가 옵션에는 `LongPolling` 속성:</span><span class="sxs-lookup"><span data-stu-id="b6725-147">The Long Polling transport has additional options that can be configured using the `LongPolling` property:</span></span>

| <span data-ttu-id="b6725-148">옵션</span><span class="sxs-lookup"><span data-stu-id="b6725-148">Option</span></span> | <span data-ttu-id="b6725-149">설명</span><span class="sxs-lookup"><span data-stu-id="b6725-149">Description</span></span> |
| ------ | ----------- |
| `PollTimeout` | <span data-ttu-id="b6725-150">최대 기간 서버 단일 폴링 요청을 종료 하기 전에 클라이언트에 보낼 메시지를 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-150">The maximum amount of time the server waits for a message to send to the client before terminating a single poll request.</span></span> <span data-ttu-id="b6725-151">이 값을 줄이면 하면 클라이언트가 새 폴링 요청을 더 자주 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-151">Decreasing this value causes the client to issue new poll requests more frequently.</span></span> <span data-ttu-id="b6725-152">기본값은 90 초입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-152">The default value is 90 seconds.</span></span> |

<span data-ttu-id="b6725-153">WebSocket 전송 사용 하 여 구성할 수 있는 추가 옵션에는 `WebSockets` 속성:</span><span class="sxs-lookup"><span data-stu-id="b6725-153">The WebSocket transport has additional options that can be configured using the `WebSockets` property:</span></span>

| <span data-ttu-id="b6725-154">옵션</span><span class="sxs-lookup"><span data-stu-id="b6725-154">Option</span></span> | <span data-ttu-id="b6725-155">설명</span><span class="sxs-lookup"><span data-stu-id="b6725-155">Description</span></span> |
| ------ | ----------- |
| `CloseTimeout` | <span data-ttu-id="b6725-156">클라이언트가이 시간 간격 이내에 종결 되지 않으면 서버 닫힌 후에 연결이 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-156">After the server closes, if the client fails to close within this time interval, the connection is terminated.</span></span> |
| `SubProtocolSelector` | <span data-ttu-id="b6725-157">설정 하는 데 사용할 수 있는 대리자는 `Sec-WebSocket-Protocol` 헤더를 사용자 지정 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-157">A delegate that can be used to set the `Sec-WebSocket-Protocol` header to a custom value.</span></span> <span data-ttu-id="b6725-158">대리자는 값을 입력으로 클라이언트 요청을 받는 하 고 원하는 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-158">The delegate receives the values requested by the client as input and is expected to return the desired value.</span></span> |

## <a name="configure-client-options"></a><span data-ttu-id="b6725-159">클라이언트 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="b6725-159">Configure client options</span></span>

<span data-ttu-id="b6725-160">클라이언트 옵션에서 구성할 수 있습니다는 `HubConnectionBuilder` 유형 (.NET 및 JavaScript 클라이언트에서 사용 가능), 뿐만 `HubConnection` 자체입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-160">Client options can be configured on the `HubConnectionBuilder` type (available in both .NET and JavaScript clients), as well as on the `HubConnection` itself.</span></span>

### <a name="configure-logging"></a><span data-ttu-id="b6725-161">로깅 구성</span><span class="sxs-lookup"><span data-stu-id="b6725-161">Configure logging</span></span>

<span data-ttu-id="b6725-162">로깅을 사용 하 여.NET 클라이언트에서 구성 된 `ConfigureLogging` 메서드.</span><span class="sxs-lookup"><span data-stu-id="b6725-162">Logging is configured in the .NET Client using the `ConfigureLogging` method.</span></span> <span data-ttu-id="b6725-163">서버의 경우와 같은 방식으로 로깅 공급자 및 필터를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-163">Logging providers and filters can be registered in the same way as they are on the server.</span></span> <span data-ttu-id="b6725-164">참조는 [ASP.NET Core 로그인](xref:fundamentals/logging/index#how-to-add-providers) 자세한 정보에 대 한 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-164">See the [Logging in ASP.NET Core](xref:fundamentals/logging/index#how-to-add-providers) documentation for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="b6725-165">로깅 공급자를 등록 하려면 필요한 패키지를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-165">In order to register Logging providers, you must install the necessary packages.</span></span> <span data-ttu-id="b6725-166">참조는 [기본 제공 로깅 공급자](xref:fundamentals/logging/index#built-in-logging-providers) 전체 목록에 대 한 설명서의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-166">See the [Built-in logging providers](xref:fundamentals/logging/index#built-in-logging-providers) section of the docs for a full list.</span></span>

<span data-ttu-id="b6725-167">예를 들어 콘솔 로깅을 사용 하려면 설치는 `Microsoft.Extensions.Logging.Console` NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-167">For example, to enable Console logging, install the `Microsoft.Extensions.Logging.Console` NuGet package.</span></span> <span data-ttu-id="b6725-168">호출 된 `AddConsole` 확장 메서드:</span><span class="sxs-lookup"><span data-stu-id="b6725-168">Call the `AddConsole` extension method:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub")
    .ConfigureLogging(logging => {
        logging.SetMinimumLevel(LogLevel.Information);
        logging.AddConsole();
    })
    .Build();
```

<span data-ttu-id="b6725-169">JavaScript 클라이언트에서 비슷한 `configureLogging` 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-169">In the JavaScript client, a similar `configureLogging` method exists.</span></span> <span data-ttu-id="b6725-170">제공 된 `LogLevel` 최소 수준의 로그를 생성 하는 메시지를 나타내는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-170">Provide a `LogLevel` value indicating the minimum level of log messages to produce.</span></span> <span data-ttu-id="b6725-171">로그가는 브라우저 콘솔 창에 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-171">Logs are written to the browser console window.</span></span>

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub")
    .configureLogging(signalR.LogLevel.Information)
    .build();
```

> [!NOTE]
> <span data-ttu-id="b6725-172">완전히 로깅을 사용 하지 않으려면 지정 `signalR.LogLevel.None` 에 `configureLogging` 메서드.</span><span class="sxs-lookup"><span data-stu-id="b6725-172">To disable logging entirely, specify `signalR.LogLevel.None` in the `configureLogging` method.</span></span>

<span data-ttu-id="b6725-173">JavaScript 클라이언트에서 사용 가능한 로그 수준은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-173">Log levels available to the JavaScript client are listed below.</span></span> <span data-ttu-id="b6725-174">메시지의 로깅을 사용 하면 로그 수준은 다음이 값 중 하나를 설정 **이상** 해당 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-174">Setting the log level to one of these values enables logging of messages at **or above** that level.</span></span>

| <span data-ttu-id="b6725-175">수준</span><span class="sxs-lookup"><span data-stu-id="b6725-175">Level</span></span> | <span data-ttu-id="b6725-176">설명</span><span class="sxs-lookup"><span data-stu-id="b6725-176">Description</span></span> |
| ----- | ----------- |
| `None` | <span data-ttu-id="b6725-177">메시지가 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-177">No messages are logged.</span></span> |
| `Critical` | <span data-ttu-id="b6725-178">전체 응용 프로그램에서 오류를 나타내는 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-178">Messages that indicate a failure in the entire app.</span></span> |
| `Error` | <span data-ttu-id="b6725-179">현재 작업에서 오류를 나타내는 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-179">Messages that indicate a failure in the current operation.</span></span> |
| `Warning` | <span data-ttu-id="b6725-180">사소한 문제를 나타내는 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-180">Messages that indicate a non-fatal problem.</span></span> |
| `Information` | <span data-ttu-id="b6725-181">정보 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-181">Informational messages.</span></span> |
| `Debug` | <span data-ttu-id="b6725-182">진단 메시지를 디버깅할 때 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-182">Diagnostic messages useful for debugging.</span></span> |
| `Trace` | <span data-ttu-id="b6725-183">특정 문제를 진단 하기 위한 매우 자세한 진단 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-183">Very detailed diagnostic messages designed for diagnosing specific issues.</span></span> |

### <a name="configure-allowed-transports"></a><span data-ttu-id="b6725-184">허용 된 전송 구성</span><span class="sxs-lookup"><span data-stu-id="b6725-184">Configure allowed transports</span></span>

<span data-ttu-id="b6725-185">SignalR에서 사용 된 전송에서 구성할 수 있습니다는 `WithUrl` 호출 (`withUrl` JavaScript에서).</span><span class="sxs-lookup"><span data-stu-id="b6725-185">The transports used by SignalR can be configured in the `WithUrl` call (`withUrl` in JavaScript).</span></span> <span data-ttu-id="b6725-186">값의 비트 OR `HttpTransportType` 는 특정된 전송 모드를 사용 하도록 클라이언트를 제한 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-186">A bitwise-OR of the values of `HttpTransportType` can be used to restrict the client to only use the specified transports.</span></span> <span data-ttu-id="b6725-187">모든 전송 기본적으로 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-187">All transports are enabled by default.</span></span>

<span data-ttu-id="b6725-188">예를 들어 Server-Sent 이벤트 전송 하지 않으려면 하지만 Websocket 및 긴 폴링 연결 허용:</span><span class="sxs-lookup"><span data-stu-id="b6725-188">For example, to disable the Server-Sent Events transport, but allow WebSockets and Long Polling connections:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", HttpTransportType.WebSockets | HttpTransportType.LongPolling)
    .Build();
```

<span data-ttu-id="b6725-189">JavaScript 클라이언트에서 전송 설정 하 여 구성 된 `transport` 옵션 개체에 제공 된 필드 `withUrl`:</span><span class="sxs-lookup"><span data-stu-id="b6725-189">In the JavaScript client, transports are configured by setting the `transport` field on the options object provided to `withUrl`:</span></span>

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub", { transport: signalR.HttpTransportType.WebSockets | signalR.HttpTransportType.LongPolling })
    .build();
```

### <a name="configure-bearer-authentication"></a><span data-ttu-id="b6725-190">전달자 인증 구성</span><span class="sxs-lookup"><span data-stu-id="b6725-190">Configure bearer authentication</span></span>

<span data-ttu-id="b6725-191">SignalR 요청 함께 인증 데이터를 제공 하기 위해 사용 된 `AccessTokenProvider` 옵션 (`accessTokenFactory` JavaScript에서) 원하는 액세스 토큰을 반환 하는 함수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-191">To provide authentication data along with SignalR requests, use the `AccessTokenProvider` option (`accessTokenFactory` in JavaScript) to specify a function that returns the desired access token.</span></span> <span data-ttu-id="b6725-192">.NET 클라이언트에서이 액세스 토큰으로 전달 되어 HTTP "전달자 인증" 토큰 (사용 하는 `Authorization` 형식의 헤더 `Bearer`).</span><span class="sxs-lookup"><span data-stu-id="b6725-192">In the .NET Client, this access token is passed in as an HTTP "Bearer Authentication" token (Using the `Authorization` header with a type of `Bearer`).</span></span> <span data-ttu-id="b6725-193">JavaScript 클라이언트에서 액세스 토큰은 Bearer 토큰으로 사용 **제외 하 고** 브라우저 Api (특히, Server-Sent 이벤트 및 Websocket 요청 수)에 헤더를 적용 하는 기능을 제한 하는 몇 가지 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-193">In the JavaScript client, the access token is used as a Bearer token, **except** in a few cases where browser APIs restrict the ability to apply headers (specifically, in Server-Sent Events and WebSockets requests).</span></span> <span data-ttu-id="b6725-194">이러한 경우 액세스 토큰이 쿼리 문자열 값으로 제공 `access_token`합니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-194">In these cases, the access token is provided as a query string value `access_token`.</span></span>

<span data-ttu-id="b6725-195">.NET 클라이언트에는 `AccessTokenProvider` 의 옵션 대리자를 사용 하 여 옵션을 지정할 수 있습니다 `WithUrl`:</span><span class="sxs-lookup"><span data-stu-id="b6725-195">In the .NET client, the `AccessTokenProvider` option can be specified using the options delegate in `WithUrl`:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options => {
        options.AccessTokenProvider = async () => {
            // Get and return the access token.
        }
    })
    .Build();
```

<span data-ttu-id="b6725-196">JavaScript 클라이언트에서 액세스 토큰을 설정 하 여 구성 됩니다는 `accessTokenFactory` 필드에 있는 옵션 개체 `withUrl`:</span><span class="sxs-lookup"><span data-stu-id="b6725-196">In the JavaScript client, the access token is configured by setting the `accessTokenFactory` field on the options object in `withUrl`:</span></span>

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

### <a name="configure-timeout-and-keep-alive-options"></a><span data-ttu-id="b6725-197">시간 제한 및 연결 유지 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="b6725-197">Configure timeout and keep-alive options</span></span>

<span data-ttu-id="b6725-198">제한 시간 및 유지 동작을 구성 하기 위한 추가 옵션은 사용할 수는 `HubConnection` 개체 자체:</span><span class="sxs-lookup"><span data-stu-id="b6725-198">Additional options for configuring timeout and keep-alive behavior are available on the `HubConnection` object itself:</span></span>

| <span data-ttu-id="b6725-199">.NET 옵션</span><span class="sxs-lookup"><span data-stu-id="b6725-199">.NET Option</span></span> | <span data-ttu-id="b6725-200">JavaScript 옵션</span><span class="sxs-lookup"><span data-stu-id="b6725-200">JavaScript Option</span></span> | <span data-ttu-id="b6725-201">설명</span><span class="sxs-lookup"><span data-stu-id="b6725-201">Description</span></span> |
| ----------- | ----------------- | ----------- |
| `ServerTimeout` | `serverTimeoutInMilliseconds` | <span data-ttu-id="b6725-202">서버 작업에 대 한 제한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-202">Timeout for server activity.</span></span> <span data-ttu-id="b6725-203">클라이언트 서버가이 기간에 모든 메시지를 전송 하지 않은 경우 서버 연결 끊김 및 트리거 고려는 `Closed` 이벤트 (`onclose` JavaScript에서).</span><span class="sxs-lookup"><span data-stu-id="b6725-203">If the server hasn't sent any message in this interval, the client considers the server disconnected and trigger the `Closed` event (`onclose` in JavaScript).</span></span> |
| `HandshakeTimeout` | <span data-ttu-id="b6725-204">구성할 수 없습니다</span><span class="sxs-lookup"><span data-stu-id="b6725-204">Not configurable</span></span> | <span data-ttu-id="b6725-205">핸드셰이크 초기 서버에 대 한 제한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-205">Timeout for initial server handshake.</span></span> <span data-ttu-id="b6725-206">서버가이 간격의 핸드셰이크 응답을 전송 하지 않습니다, 클라이언트 취소 핸드셰이크 및 트리거는 `Closed` 이벤트 (`onclose` JavaScript에서).</span><span class="sxs-lookup"><span data-stu-id="b6725-206">If the server doesn't send a handshake response in this interval, the client cancels the handshake and trigger the `Closed` event (`onclose` in JavaScript).</span></span> |

<span data-ttu-id="b6725-207">.NET 클라이언트 시간 제한 값으로 지정 되 `TimeSpan` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-207">In the .NET Client, timeout values are specified as `TimeSpan` values.</span></span> <span data-ttu-id="b6725-208">JavaScript 클라이언트에서 제한 시간 값은 숫자로 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-208">In the JavaScript client, timeout values are specified as numbers.</span></span> <span data-ttu-id="b6725-209">수는 밀리초 단위의 시간 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-209">The numbers represent time values in milliseconds.</span></span>

### <a name="configure-additional-options"></a><span data-ttu-id="b6725-210">추가 옵션 구성</span><span class="sxs-lookup"><span data-stu-id="b6725-210">Configure additional options</span></span>

<span data-ttu-id="b6725-211">추가 옵션에서 구성할 수 있습니다는 `WithUrl` (`withUrl` JavaScript에서) 메서드를 `HubConnectionBuilder`:</span><span class="sxs-lookup"><span data-stu-id="b6725-211">Additional options can be configured in the `WithUrl` (`withUrl` in JavaScript) method on `HubConnectionBuilder`:</span></span>

| <span data-ttu-id="b6725-212">.NET 옵션</span><span class="sxs-lookup"><span data-stu-id="b6725-212">.NET Option</span></span> | <span data-ttu-id="b6725-213">JavaScript 옵션</span><span class="sxs-lookup"><span data-stu-id="b6725-213">JavaScript Option</span></span> | <span data-ttu-id="b6725-214">설명</span><span class="sxs-lookup"><span data-stu-id="b6725-214">Description</span></span> |
| ----------- | ----------------- | ----------- |
| `AccessTokenProvider` | `accessTokenFactory` | <span data-ttu-id="b6725-215">HTTP 요청에서 전달자 인증 토큰으로 제공 되는 문자열을 반환 하는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-215">A function returning a string that is provided as a Bearer authentication token in HTTP requests.</span></span> |
| `SkipNegotiation` | `skipNegotiation` | <span data-ttu-id="b6725-216">이 속성을 설정 `true` 협상 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-216">Set this to `true` to skip the negotiation step.</span></span> <span data-ttu-id="b6725-217">**Websocket 전송은 사용 가능한 유일한 전송 하는 경우에 지원**합니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-217">**Only supported when the WebSockets transport is the only enabled transport**.</span></span> <span data-ttu-id="b6725-218">이 설정은 Azure SignalR 서비스를 사용 하는 경우 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-218">This setting can't be enabled when using the Azure SignalR Service.</span></span> |
| `ClientCertificates` | <span data-ttu-id="b6725-219">구성 가능 \*</span><span class="sxs-lookup"><span data-stu-id="b6725-219">Not configurable \*</span></span> | <span data-ttu-id="b6725-220">요청을 인증에 보내도록 TLS 인증서의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-220">A collection of TLS certificates to send to authenticate requests.</span></span> |
| `Cookies` | <span data-ttu-id="b6725-221">구성 가능 \*</span><span class="sxs-lookup"><span data-stu-id="b6725-221">Not configurable \*</span></span> | <span data-ttu-id="b6725-222">모든 HTTP 요청에 보낼 HTTP 쿠키의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-222">A collection of HTTP cookies to send with every HTTP request.</span></span> |
| `Credentials` | <span data-ttu-id="b6725-223">구성 가능 \*</span><span class="sxs-lookup"><span data-stu-id="b6725-223">Not configurable \*</span></span> | <span data-ttu-id="b6725-224">모든 HTTP 요청과 함께 보내는 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-224">Credentials to send with every HTTP request.</span></span> |
| `CloseTimeout` | <span data-ttu-id="b6725-225">구성 가능 \*</span><span class="sxs-lookup"><span data-stu-id="b6725-225">Not configurable \*</span></span> | <span data-ttu-id="b6725-226">Websocket에만 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-226">WebSockets only.</span></span> <span data-ttu-id="b6725-227">최대 기간 클라이언트 닫기 요청을 승인 하는 데 서버에 대 한 닫힌 후 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-227">The maximum amount of time the client waits after closing for the server to acknowledge the close request.</span></span> <span data-ttu-id="b6725-228">서버가이 시간 안에 종료를 승인 하지 않습니다, 클라이언트 연결을 끊습니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-228">If the server doesn't acknowledge the close within this time, the client disconnects.</span></span> |
| `Headers` | <span data-ttu-id="b6725-229">구성 가능 \*</span><span class="sxs-lookup"><span data-stu-id="b6725-229">Not configurable \*</span></span> | <span data-ttu-id="b6725-230">모든 HTTP 요청에 보낼 추가 HTTP 헤더의 사전입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-230">A dictionary of additional HTTP headers to send with every HTTP request.</span></span> |
| `HttpMessageHandlerFactory` | <span data-ttu-id="b6725-231">구성 가능 \*</span><span class="sxs-lookup"><span data-stu-id="b6725-231">Not configurable \*</span></span> | <span data-ttu-id="b6725-232">구성 하거나 바꿀 사용할 수 있는 대리자는 `HttpMessageHandler` HTTP 요청을 보내는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-232">A delegate that can be used to configure or replace the `HttpMessageHandler` used to send HTTP requests.</span></span> <span data-ttu-id="b6725-233">WebSocket 연결에 대 한 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-233">Not used for WebSocket connections.</span></span> <span data-ttu-id="b6725-234">이 대리자는 null이 아닌 값을 반환 해야 하 고 기본 값을 매개 변수로 받을 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-234">This delegate must return a non-null value, and it receives the default value as a parameter.</span></span> <span data-ttu-id="b6725-235">해당 기본값에 대 한 설정을 수정 하 고, 반환 하거나 반환할 완전히 새로운 `HttpMessageHandler` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="b6725-235">Either modify settings on that default value and return it, or return a completely new `HttpMessageHandler` instance.</span></span> |
| `Proxy` | <span data-ttu-id="b6725-236">구성 가능 \*</span><span class="sxs-lookup"><span data-stu-id="b6725-236">Not configurable \*</span></span> | <span data-ttu-id="b6725-237">HTTP 요청을 보낼 때 사용 하는 HTTP 프록시입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-237">An HTTP proxy to use when sending HTTP requests.</span></span> |
| `UseDefaultCredentials` | <span data-ttu-id="b6725-238">구성 가능 \*</span><span class="sxs-lookup"><span data-stu-id="b6725-238">Not configurable \*</span></span> | <span data-ttu-id="b6725-239">이 부울 보낼 HTTP 및 Websocket 요청에 대 한 기본 자격 증명을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-239">Set this boolean to send the default credentials for HTTP and WebSockets requests.</span></span> <span data-ttu-id="b6725-240">이렇게 하면 Windows 인증을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-240">This enables the use of Windows authentication.</span></span> |
| `WebSocketConfiguration` | <span data-ttu-id="b6725-241">구성 가능 \*</span><span class="sxs-lookup"><span data-stu-id="b6725-241">Not configurable \*</span></span> | <span data-ttu-id="b6725-242">추가 WebSocket 옵션을 구성을 사용할 수 있는 대리자입니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-242">A delegate that can be used to configure additional WebSocket options.</span></span> <span data-ttu-id="b6725-243">인스턴스를 받아서 [ClientWebSocketOptions](/dotnet/api/system.net.websockets.clientwebsocketoptions) 옵션을 구성을 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-243">Receives an instance of [ClientWebSocketOptions](/dotnet/api/system.net.websockets.clientwebsocketoptions) that can be used to configure the options.</span></span> |

<span data-ttu-id="b6725-244">별표 (\*)로 표시 하는 옵션 브라우저 Api의에서 제한으로 인해 JavaScript 클라이언트에서 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b6725-244">Options marked with an asterisk (\*) aren't configurable in the JavaScript client, due to limitations in browser APIs.</span></span>

<span data-ttu-id="b6725-245">.NET 클라이언트에서 이러한 옵션을 수정할 수를 제공 하는 옵션 대리자가 `WithUrl`:</span><span class="sxs-lookup"><span data-stu-id="b6725-245">In the .NET Client, these options can be modified by the options delegate provided to `WithUrl`:</span></span>

```csharp
var connection = new HubConnectionBuilder()
    .WithUrl("https://example.com/myhub", options => {
        options.Headers["Foo"] = "Bar";
        options.Cookies.Add(new Cookie(/* ... */);
        options.ClientCertificates.Add(/* ... */);
    })
    .Build();
```

<span data-ttu-id="b6725-246">JavaScript 클라이언트에서 이러한 옵션에 제공 된 JavaScript 개체에 제공 될 수 있습니다 `withUrl`:</span><span class="sxs-lookup"><span data-stu-id="b6725-246">In the JavaScript Client, these options can be provided in a JavaScript object provided to `withUrl`:</span></span>

```javascript
let connection = new signalR.HubConnectionBuilder()
    .withUrl("/myhub", {
        skipNegotiation: true,
        transport: signalR.HttpTransportType.WebSockets
    });
    .build();
```

## <a name="additional-resources"></a><span data-ttu-id="b6725-247">추가 자료</span><span class="sxs-lookup"><span data-stu-id="b6725-247">Additional resources</span></span>

* <xref:tutorials/signalr>
* <xref:signalr/hubs>
* <xref:signalr/javascript-client>
* <xref:signalr/dotnet-client>
* <xref:signalr/messagepackhubprotocol>
* <xref:signalr/supported-platforms>
