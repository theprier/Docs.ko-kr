---
title: ASP.NET Core에서 Kestrel 웹 서버 구현
author: tdykstra
description: libuv 기반 ASP.NET Core에 대한 플랫폼 간 웹 서버인 Kestrel에 대해 알아봅니다.
manager: wpickett
ms.author: tdykstra
ms.custom: mvc
ms.date: 04/26/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/servers/kestrel
ms.openlocfilehash: 1709d26f5dfe40d178da70c286d328982f2c39a0
ms.sourcegitcommit: 5130b3034165f5cf49d829fe7475a84aa33d2693
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="kestrel-web-server-implementation-in-aspnet-core"></a><span data-ttu-id="9cbf6-103">ASP.NET Core에서 Kestrel 웹 서버 구현</span><span class="sxs-lookup"><span data-stu-id="9cbf6-103">Kestrel web server implementation in ASP.NET Core</span></span>

<span data-ttu-id="9cbf6-104">작성자: [Tom Dykstra](https://github.com/tdykstra), [Chris Ross](https://github.com/Tratcher) 및 [Stephen Halter](https://twitter.com/halter73)</span><span class="sxs-lookup"><span data-stu-id="9cbf6-104">By [Tom Dykstra](https://github.com/tdykstra), [Chris Ross](https://github.com/Tratcher), and [Stephen Halter](https://twitter.com/halter73)</span></span>

<span data-ttu-id="9cbf6-105">Kestrel은 플랫폼 간 비동기 I/O 라이브러리인 [libuv](https://github.com/libuv/libuv)를 기반으로 하는 [ASP.NET Core용 플랫폼 간 웹 서버](xref:fundamentals/servers/index)입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-105">Kestrel is a cross-platform [web server for ASP.NET Core](xref:fundamentals/servers/index) based on [libuv](https://github.com/libuv/libuv), a cross-platform asynchronous I/O library.</span></span> <span data-ttu-id="9cbf6-106">Kestrel은 기본적으로 ASP.NET Core 프로젝트 템플릿에 포함된 웹 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-106">Kestrel is the web server that's included by default in ASP.NET Core project templates.</span></span>

<span data-ttu-id="9cbf6-107">Kestrel은 다음과 같은 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-107">Kestrel supports the following features:</span></span>

* <span data-ttu-id="9cbf6-108">HTTPS</span><span class="sxs-lookup"><span data-stu-id="9cbf6-108">HTTPS</span></span>
* <span data-ttu-id="9cbf6-109">[Websocket](https://github.com/aspnet/websockets)을 활성화하는 데 사용되는 불투명 업그레이드</span><span class="sxs-lookup"><span data-stu-id="9cbf6-109">Opaque upgrade used to enable [WebSockets](https://github.com/aspnet/websockets)</span></span>
* <span data-ttu-id="9cbf6-110">Nginx 뒤의 고성능을 위한 Unix 소켓</span><span class="sxs-lookup"><span data-stu-id="9cbf6-110">Unix sockets for high performance behind Nginx</span></span>

<span data-ttu-id="9cbf6-111">Kestrel은 .NET Core에서 지원하는 모든 플랫폼 및 버전에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-111">Kestrel is supported on all platforms and versions that .NET Core supports.</span></span>

<span data-ttu-id="9cbf6-112">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/samples)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="9cbf6-112">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="when-to-use-kestrel-with-a-reverse-proxy"></a><span data-ttu-id="9cbf6-113">Kestrel을 역방향 프록시와 함께 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="9cbf6-113">When to use Kestrel with a reverse proxy</span></span>

#### <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="9cbf6-114">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="9cbf6-114">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="9cbf6-115">Kestrel을 단독으로 사용하거나 IIS, Nginx 또는 Apache 같은 *역방향 프록시 서버*와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-115">You can use Kestrel by itself or with a *reverse proxy server*, such as IIS, Nginx, or Apache.</span></span> <span data-ttu-id="9cbf6-116">역방향 프록시 서버는 인터넷에서 HTTP 요청을 수신하고 몇몇 사전 처리 후에 Kestrel에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-116">A reverse proxy server receives HTTP requests from the Internet and forwards them to Kestrel after some preliminary handling.</span></span>

![Kestrel은 역방향 프록시 서버 없이 직접 인터넷과 통신합니다.](kestrel/_static/kestrel-to-internet2.png)

![Kestrel은 IIS, Nginx 또는 Apache 같은 역방향 프록시 서버를 통해 간접적으로 인터넷과 통신합니다.](kestrel/_static/kestrel-to-internet.png)

<span data-ttu-id="9cbf6-119">Kestrel이 내부 네트워크에만 노출되지 않는 한 역방향 프록시 서버와 함께 Kestrel를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-119">We recommend using Kestrel with a reverse proxy server unless Kestrel is only exposed to an internal network.</span></span>

#### <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="9cbf6-120">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="9cbf6-120">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="9cbf6-121">앱이 내부 네트워크에서만 요청을 수락하는 경우 Kestrel을 앱 서버로 직접 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-121">If an app accepts requests only from an internal network, Kestrel can be used directly as the app's server.</span></span>

![Kestrel은 내부 네트워크와 직접 통신합니다.](kestrel/_static/kestrel-to-internal.png)

<span data-ttu-id="9cbf6-123">앱을 인터넷에 노출할 경우 IIS, Nginx 또는 Apache를 *역방향 프록시 서버*로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-123">If you expose your app to the Internet, use IIS, Nginx, or Apache as a *reverse proxy server*.</span></span> <span data-ttu-id="9cbf6-124">역방향 프록시 서버는 인터넷에서 HTTP 요청을 수신하고 몇몇 사전 처리 후에 Kestrel에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-124">A reverse proxy server receives HTTP requests from the Internet and forwards them to Kestrel after some preliminary handling.</span></span>

![Kestrel은 IIS, Nginx 또는 Apache 같은 역방향 프록시 서버를 통해 간접적으로 인터넷과 통신합니다.](kestrel/_static/kestrel-to-internet.png)

<span data-ttu-id="9cbf6-126">역방향 프록시는 보안 이유로 인터넷에서 트래픽에 노출되는 에지 배포에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-126">A reverse proxy is required for edge deployments (exposed to traffic from the Internet) for security reasons.</span></span> <span data-ttu-id="9cbf6-127">Kestrel의 1.x 버전은 적절한 시간 제한, 크기 제한 및 동시 연결 제한 등의 공격에 대한 완벽한 방어 능력은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-127">The 1.x versions of Kestrel don't have a full complement of defenses against attacks, such as appropriate timeouts, size limits, and concurrent connection limits.</span></span>

* * *

<span data-ttu-id="9cbf6-128">역방향 프록시 시나리오는 동일한 IP 및 단일 서버에서 실행되는 포트를 공유하는 여러 앱이 있는 경우에 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-128">A reverse proxy scenario exists when there are multiple apps that share the same IP and port running on a single server.</span></span> <span data-ttu-id="9cbf6-129">Kestrel은 여러 프로세스 간에 동일한 IP 및 포트 공유를 지원하지 않으므로 이 시나리오를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-129">Kestrel doesn't support this scenario because Kestrel doesn't support sharing the same IP and port among multiple processes.</span></span> <span data-ttu-id="9cbf6-130">Kestrel이 포트에서 수신 대기하도록 구성된 경우 Kestrel은 요청의 호스트 헤더에 관계 없이 해당 포트에 대한 모든 트래픽을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-130">When Kestrel is configured to listen on a port, Kestrel handles all of the traffic for that port regardless of requests' host header.</span></span> <span data-ttu-id="9cbf6-131">포트를 공유할 수 있는 역방향 프록시는 고유 IP 및 포트에서 Kestrel에 요청을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-131">A reverse proxy that can share ports has the ability to forward requests to Kestrel on a unique IP and port.</span></span>

<span data-ttu-id="9cbf6-132">역방향 프록시 서버가 필요하지 않은 경우에도 역방향 프록시 서버를 사용하는 것은 적합한 선택일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-132">Even if a reverse proxy server isn't required, using a reverse proxy server might be a good choice:</span></span>

* <span data-ttu-id="9cbf6-133">호스트하는 앱의 공개된 공용 노출 영역을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-133">It can limit the exposed public surface area of the apps that it hosts.</span></span>
* <span data-ttu-id="9cbf6-134">구성 및 방어의 추가 계층을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-134">It provides an additional layer of configuration and defense.</span></span>
* <span data-ttu-id="9cbf6-135">기존 인프라와 잘 통합될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-135">It might integrate better with existing infrastructure.</span></span>
* <span data-ttu-id="9cbf6-136">부하 분산 및 SSL 구성을 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-136">It simplifies load balancing and SSL configuration.</span></span> <span data-ttu-id="9cbf6-137">역방향 프록시 서버에 SSL 인증서가 필요한 경우에만 해당 서버는 일반 HTTP를 사용하여 내부 네트워크에서 앱 서버와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-137">Only the reverse proxy server requires an SSL certificate, and that server can communicate with your app servers on the internal network using plain HTTP.</span></span>

> [!WARNING]
> <span data-ttu-id="9cbf6-138">호스트 필터링을 사용하도록 설정된 역방향 프록시를 사용하지 않는 경우 [호스트 필터링](#host-filtering)을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-138">If not using a reverse proxy with host filtering enabled, [host filtering](#host-filtering) must be enabled.</span></span>

## <a name="how-to-use-kestrel-in-aspnet-core-apps"></a><span data-ttu-id="9cbf6-139">ASP.NET Core 앱에서 Kestrel을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="9cbf6-139">How to use Kestrel in ASP.NET Core apps</span></span>

#### <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="9cbf6-140">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="9cbf6-140">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

<span data-ttu-id="9cbf6-141">[Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) 패키지는 [Microsoft.AspNetCore.All 메타패키지](xref:fundamentals/metapackage)에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-141">The [Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) package is included in the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage).</span></span>

<span data-ttu-id="9cbf6-142">ASP.NET Core 프로젝트 템플릿은 기본적으로 Kestrel을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-142">ASP.NET Core project templates use Kestrel by default.</span></span> <span data-ttu-id="9cbf6-143">*Program.cs*에서 템플릿 코드는 [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel) 숨은 기능을 호출하는 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-143">In *Program.cs*, the template code calls [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder), which calls [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel) behind the scenes.</span></span>

[!code-csharp[](kestrel/samples/2.x/Program.cs?name=snippet_DefaultBuilder&highlight=7)]

#### <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="9cbf6-144">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="9cbf6-144">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

<span data-ttu-id="9cbf6-145">[Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) NuGet 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-145">Install the [Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) NuGet package.</span></span>

<span data-ttu-id="9cbf6-146">다음 섹션과 같이 필요한 [Kestrel 옵션](/dotnet/api/microsoft.aspnetcore.server.kestrel.kestrelserveroptions?view=aspnetcore-1.1)을 지정하여 `Main` 메서드에서 [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder?view=aspnetcore-1.1)의 [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) 확장 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-146">Call the [UseKestrel](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions.usekestrel?view=aspnetcore-1.1) extension method on [WebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.webhostbuilder?view=aspnetcore-1.1) in the `Main` method, specifying any [Kestrel options](/dotnet/api/microsoft.aspnetcore.server.kestrel.kestrelserveroptions?view=aspnetcore-1.1) required, as shown in the next section.</span></span>

[!code-csharp[](kestrel/samples/1.x/Program.cs?name=snippet_Main&highlight=13-19)]

* * *

### <a name="kestrel-options"></a><span data-ttu-id="9cbf6-147">Kestrel 옵션</span><span class="sxs-lookup"><span data-stu-id="9cbf6-147">Kestrel options</span></span>

#### <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="9cbf6-148">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="9cbf6-148">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

<span data-ttu-id="9cbf6-149">Kestrel 웹 서버에는 인터넷 연결 배포에 특히 유용한 제약 조건 구성 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-149">The Kestrel web server has constraint configuration options that are especially useful in Internet-facing deployments.</span></span> <span data-ttu-id="9cbf6-150">사용자 지정될 수 있는 몇 가지 중요 한 제한입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-150">A few important limits that can be customized:</span></span>

* <span data-ttu-id="9cbf6-151">최대 클라이언트 연결</span><span class="sxs-lookup"><span data-stu-id="9cbf6-151">Maximum client connections</span></span>
* <span data-ttu-id="9cbf6-152">최대 요청 본문 크기</span><span class="sxs-lookup"><span data-stu-id="9cbf6-152">Maximum request body size</span></span>
* <span data-ttu-id="9cbf6-153">최소 요청 본문 데이터 속도</span><span class="sxs-lookup"><span data-stu-id="9cbf6-153">Minimum request body data rate</span></span>

<span data-ttu-id="9cbf6-154">[KestrelServerOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions) 클래스의 [한도](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.limits) 속성에서 이러한 제약 조건 및 기타 제약 조건을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-154">Set these and other constraints on the [Limits](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.limits) property of the [KestrelServerOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions) class.</span></span> <span data-ttu-id="9cbf6-155">`Limits` 속성은 [KestrelServerLimits](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits) 클래스의 인스턴스를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-155">The `Limits` property holds an instance of the [KestrelServerLimits](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits) class.</span></span>

<span data-ttu-id="9cbf6-156">**최대 클라이언트 연결**</span><span class="sxs-lookup"><span data-stu-id="9cbf6-156">**Maximum client connections**</span></span>

[<span data-ttu-id="9cbf6-157">MaxConcurrentConnections</span><span class="sxs-lookup"><span data-stu-id="9cbf6-157">MaxConcurrentConnections</span></span>](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.maxconcurrentconnections)  
[<span data-ttu-id="9cbf6-158">MaxConcurrentUpgradedConnections</span><span class="sxs-lookup"><span data-stu-id="9cbf6-158">MaxConcurrentUpgradedConnections</span></span>](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.maxconcurrentupgradedconnections)

<span data-ttu-id="9cbf6-159">다음 코드를 사용하여 전체 앱에 대한 동시 개방 TCP 연결의 최대 수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-159">The maximum number of concurrent open TCP connections can be set for the entire app with the following code:</span></span>

[!code-csharp[](kestrel/samples/2.x/Program.cs?name=snippet_Limits&highlight=3-4)]

<span data-ttu-id="9cbf6-160">HTTP 또는 HTTPS에서 다른 프로토콜(예: WebSocket 요청에서)로 업그레이드된 연결에 대한 별도 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-160">There's a separate limit for connections that have been upgraded from HTTP or HTTPS to another protocol (for example, on a WebSockets request).</span></span> <span data-ttu-id="9cbf6-161">연결이 업그레이드된 후 `MaxConcurrentConnections` 제한에 대해 계산되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-161">After a connection is upgraded, it isn't counted against the `MaxConcurrentConnections` limit.</span></span>

<span data-ttu-id="9cbf6-162">연결의 최대 수는 기본적으로 무제한(null)입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-162">The maximum number of connections is unlimited (null) by default.</span></span>

<span data-ttu-id="9cbf6-163">**최대 요청 본문 크기**</span><span class="sxs-lookup"><span data-stu-id="9cbf6-163">**Maximum request body size**</span></span>

[<span data-ttu-id="9cbf6-164">MaxRequestBodySize</span><span class="sxs-lookup"><span data-stu-id="9cbf6-164">MaxRequestBodySize</span></span>](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.maxrequestbodysize)

<span data-ttu-id="9cbf6-165">기본 최대 요청 본문 크기는 약 28.6MB인 30,000,000바이트입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-165">The default maximum request body size is 30,000,000 bytes, which is approximately 28.6 MB.</span></span>

<span data-ttu-id="9cbf6-166">ASP.NET Core MVC 앱에서 한도를 재정의할 때는 작업 메서드에서 [RequestSizeLimit](/dotnet/api/microsoft.aspnetcore.mvc.requestsizelimitattribute) 특성을 사용하는 방법이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-166">The recommended approach to override the limit in an ASP.NET Core MVC app is to use the [RequestSizeLimit](/dotnet/api/microsoft.aspnetcore.mvc.requestsizelimitattribute) attribute on an action method:</span></span>

```csharp
[RequestSizeLimit(100000000)]
public IActionResult MyActionMethod()
```

<span data-ttu-id="9cbf6-167">다음 예제는 모든 요청에서 앱에 대한 제약 조건을 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-167">Here's an example that shows how to configure the constraint for the app on every request:</span></span>

[!code-csharp[](kestrel/samples/2.x/Program.cs?name=snippet_Limits&highlight=5)]

<span data-ttu-id="9cbf6-168">미들웨어에서 특정 요청에 대한 설정을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-168">You can override the setting on a specific request in middleware:</span></span>

[!code-csharp[](kestrel/samples/2.x/Startup.cs?name=snippet_Limits&highlight=3-4)]

<span data-ttu-id="9cbf6-169">앱에서 요청을 읽기 시작한 후 요청에 대한 제한을 구성하려고 하면 예외가 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-169">An exception is thrown if you attempt to configure the limit on a request after the app has started to read the request.</span></span> <span data-ttu-id="9cbf6-170">`MaxRequestBodySize` 속성이 제한을 구성하기에 너무 늦은, 읽기 전용 상태인지를 알려주는 `IsReadOnly` 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-170">There's an `IsReadOnly` property that indicates if the `MaxRequestBodySize` property is in read-only state, meaning it's too late to configure the limit.</span></span>

<span data-ttu-id="9cbf6-171">**최소 요청 본문 데이터 속도**</span><span class="sxs-lookup"><span data-stu-id="9cbf6-171">**Minimum request body data rate**</span></span>

[<span data-ttu-id="9cbf6-172">MinRequestBodyDataRate</span><span class="sxs-lookup"><span data-stu-id="9cbf6-172">MinRequestBodyDataRate</span></span>](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.minrequestbodydatarate)  
[<span data-ttu-id="9cbf6-173">MinResponseDataRate</span><span class="sxs-lookup"><span data-stu-id="9cbf6-173">MinResponseDataRate</span></span>](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits.minresponsedatarate)

<span data-ttu-id="9cbf6-174">Kestrel은 데이터가 지정된 속도(바이트/초)로 도착하는지 1초마다 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-174">Kestrel checks every second if data is arriving at the specified rate in bytes/second.</span></span> <span data-ttu-id="9cbf6-175">속도가 최소 아래로 떨어지면 연결이 시간 초과됩니다. 유예 기간은 Kestrel에서 해당 전송 속도를 최소로 높이기 위해 클라이언트에 제공하는 총 시간입니다. 이 시간 동안 속도는 확인되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-175">If the rate drops below the minimum, the connection is timed out. The grace period is the amount of time that Kestrel gives the client to increase its send rate up to the minimum; the rate isn't checked during that time.</span></span> <span data-ttu-id="9cbf6-176">유예 기간은 TCP 느린 시작으로 인해 느린 속도로 처음에 데이터를 보내는 연결 중단을 방지하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-176">The grace period helps avoid dropping connections that are initially sending data at a slow rate due to TCP slow-start.</span></span>

<span data-ttu-id="9cbf6-177">기본 최소 속도는 5초의 유예 기간으로 240바이트/초입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-177">The default minimum rate is 240 bytes/second with a 5 second grace period.</span></span>

<span data-ttu-id="9cbf6-178">최소 속도는 응답에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-178">A minimum rate also applies to the response.</span></span> <span data-ttu-id="9cbf6-179">요청 제한 및 응답 제한을 설정하는 코드는 속성 및 인터페이스 이름에 `RequestBody` 또는 `Response`를 갖는 것을 제외하고 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-179">The code to set the request limit and the response limit is the same except for having `RequestBody` or `Response` in the property and interface names.</span></span>

<span data-ttu-id="9cbf6-180">*Program.cs*에서 최소 데이터 속도를 구성하는 방법을 보여 주는 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-180">Here's an example that shows how to configure the minimum data rates in *Program.cs*:</span></span>

[!code-csharp[](kestrel/samples/2.x/Program.cs?name=snippet_Limits&highlight=6-9)]

<span data-ttu-id="9cbf6-181">미들웨어에서 요청별 속도를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-181">You can configure the rates per request in middleware:</span></span>

[!code-csharp[](kestrel/samples/2.x/Startup.cs?name=snippet_Limits&highlight=5-8)]

<span data-ttu-id="9cbf6-182">다른 Kestrel 옵션 및 제한에 대한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-182">For information about other Kestrel options and limits, see:</span></span>

* [<span data-ttu-id="9cbf6-183">KestrelServerOptions</span><span class="sxs-lookup"><span data-stu-id="9cbf6-183">KestrelServerOptions</span></span>](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions)
* [<span data-ttu-id="9cbf6-184">KestrelServerLimits</span><span class="sxs-lookup"><span data-stu-id="9cbf6-184">KestrelServerLimits</span></span>](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserverlimits)
* [<span data-ttu-id="9cbf6-185">ListenOptions</span><span class="sxs-lookup"><span data-stu-id="9cbf6-185">ListenOptions</span></span>](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.listenoptions)

#### <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="9cbf6-186">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="9cbf6-186">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

<span data-ttu-id="9cbf6-187">Kestrel 옵션 및 제한에 대한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-187">For information about Kestrel options and limits, see:</span></span>

* [<span data-ttu-id="9cbf6-188">KestrelServerOptions class</span><span class="sxs-lookup"><span data-stu-id="9cbf6-188">KestrelServerOptions class</span></span>](/dotnet/api/microsoft.aspnetcore.server.kestrel.kestrelserveroptions?view=aspnetcore-1.1)
* [<span data-ttu-id="9cbf6-189">KestrelServerLimits</span><span class="sxs-lookup"><span data-stu-id="9cbf6-189">KestrelServerLimits</span></span>](/dotnet/api/microsoft.aspnetcore.server.kestrel.kestrelserverlimits?view=aspnetcore-1.1)

* * *

### <a name="endpoint-configuration"></a><span data-ttu-id="9cbf6-190">엔드포인트 구성</span><span class="sxs-lookup"><span data-stu-id="9cbf6-190">Endpoint configuration</span></span>

#### <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="9cbf6-191">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="9cbf6-191">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

::: moniker range="= aspnetcore-2.0"
<span data-ttu-id="9cbf6-192">기본적으로 ASP.NET Core는 `http://localhost:5000`으로 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-192">By default, ASP.NET Core binds to `http://localhost:5000`.</span></span> <span data-ttu-id="9cbf6-193">Kestrel에 대한 URL 접두사 및 포트를 구성하려면 [KestrelServerOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions)에 대한 [ListenUnixSocket](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listenunixsocket) 메서드 또는 [수신 대기](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listen)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-193">Call [Listen](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listen) or [ListenUnixSocket](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listenunixsocket) methods on [KestrelServerOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions) to configure URL prefixes and ports for Kestrel.</span></span> <span data-ttu-id="9cbf6-194">`UseUrls`, `--urls` 명령줄 인수 `urls` 호스트 구성 키 및 `ASPNETCORE_URLS` 환경 변수도 작동하지만 이 섹션의 뒷부분에 명시된 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-194">`UseUrls`, the `--urls` command-line argument, `urls` host configuration key, and the `ASPNETCORE_URLS` environment variable also work but have the limitations noted later in this section.</span></span>

<span data-ttu-id="9cbf6-195">`urls` 호스트 구성 키는 앱 구성이 아닌 호스트 구성에서 와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-195">The `urls` host configuration key must come from the host configuration, not the app configuration.</span></span> <span data-ttu-id="9cbf6-196">`urls` 키와 값을 *appsettings.json*에 추가하는 것은 구성 파일에서 구성을 읽을 때면 호스트가 완전히 초기화되기 때문에 호스트 구성에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-196">Adding a `urls` key and value to *appsettings.json* doesn't affect host configuration because the host is completely initialized by the time the configuration is read from the configuration file.</span></span> <span data-ttu-id="9cbf6-197">그러나 호스트를 구성하려면 호스트 작성기에서 [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration)을 통해 *appsettings.json*에서 `urls` 키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-197">However, a `urls` key in *appsettings.json* can be used with [UseConfiguration](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useconfiguration) on the host builder to configure the host:</span></span>

```csharp
var config = new ConfigurationBuilder()
    .SetBasePath(Directory.GetCurrentDirectory())
    .AddJsonFile("appSettings.json", optional: true, reloadOnChange: true)
    .Build();

var host = new WebHostBuilder()
    .UseKestrel()
    .UseConfiguration(config)
    .UseContentRoot(Directory.GetCurrentDirectory())
    .UseStartup<Startup>()
    .Build();
```
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
[!INCLUDE[](~/includes/2.1.md)]

<span data-ttu-id="9cbf6-199">기본적으로 ASP.NET Core는 다음으로 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-199">By default, ASP.NET Core binds to:</span></span>

* `http://localhost:5000`
* <span data-ttu-id="9cbf6-200">`https://localhost:5001` (로컬 개발 인증서가 제공되는 경우)</span><span class="sxs-lookup"><span data-stu-id="9cbf6-200">`https://localhost:5001` (when a local development certificate is present)</span></span>

<span data-ttu-id="9cbf6-201">개발 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-201">A development certificate is created:</span></span>

* <span data-ttu-id="9cbf6-202">[.NET Core SDK](/dotnet/core/sdk)가 설치되는 경우.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-202">When the [.NET Core SDK](/dotnet/core/sdk) is installed.</span></span>
* <span data-ttu-id="9cbf6-203">[dev-certs 도구](https://github.com/aspnet/DotNetTools/tree/dev/src/dotnet-dev-certs)가 인증서를 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-203">The [dev-certs tool](https://github.com/aspnet/DotNetTools/tree/dev/src/dotnet-dev-certs) is used to create a certificate.</span></span>

<span data-ttu-id="9cbf6-204">일부 브라우저에서 로컬 개발 인증서를 신뢰하도록 브라우저에 명시적 사용 권한을 부여할 것을 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-204">Some browsers require that you grant explicit permission to the browser to trust the local development certificate.</span></span>

<span data-ttu-id="9cbf6-205">ASP.NET Core 2.1 이상 프로젝트 템플릿은 기본적으로 HTTPS에서 실행할 앱을 구성하고 [HTTPS 리디렉션 및 HSTS 지원](xref:security/enforcing-ssl)을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-205">ASP.NET Core 2.1 and later project templates configure apps to run on HTTPS by default and include [HTTPS redirection and HSTS support](xref:security/enforcing-ssl).</span></span>

<span data-ttu-id="9cbf6-206">Kestrel에 대한 URL 접두사 및 포트를 구성하려면 [KestrelServerOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions)에 대한 [ListenUnixSocket](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listenunixsocket) 메서드 또는 [수신 대기](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listen)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-206">Call [Listen](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listen) or [ListenUnixSocket](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listenunixsocket) methods on [KestrelServerOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions) to configure URL prefixes and ports for Kestrel.</span></span>

<span data-ttu-id="9cbf6-207">`UseUrls`, `--urls` 명령줄 인수 `urls` 호스트 구성 키 및 `ASPNETCORE_URLS` 환경 변수도 작동하지만 이 섹션의 뒷부분에 명시된 제한 사항이 있습니다(HTTPS 엔드포인트 구성에 대해 기본 인증서를 사용할 수 있어야 합니다).</span><span class="sxs-lookup"><span data-stu-id="9cbf6-207">`UseUrls`, the `--urls` command-line argument, `urls` host configuration key, and the `ASPNETCORE_URLS` environment variable also work but have the limitations noted later in this section (a default certificate must be available for HTTPS endpoint configuration).</span></span>

<span data-ttu-id="9cbf6-208">ASP.NET Core 2.1 `KestrelServerOptions` 구성:</span><span class="sxs-lookup"><span data-stu-id="9cbf6-208">ASP.NET Core 2.1 `KestrelServerOptions` configuration:</span></span>

<span data-ttu-id="9cbf6-209">**ConfigureEndpointDefaults(Action<ListenOptions>)**</span><span class="sxs-lookup"><span data-stu-id="9cbf6-209">**ConfigureEndpointDefaults(Action<ListenOptions>)**</span></span>  
<span data-ttu-id="9cbf6-210">지정된 각 엔드포인트에 대해 실행할 구성 `Action`을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-210">Specifies a configuration `Action` to run for each specified endpoint.</span></span> <span data-ttu-id="9cbf6-211">`ConfigureEndpointDefaults`의 여러 차례 호출은 `Action`에 앞서 마지막으로 지정된 `Action`으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-211">Calling `ConfigureEndpointDefaults` multiple times replaces prior `Action`s with the last `Action` specified.</span></span>

<span data-ttu-id="9cbf6-212">**ConfigureHttpsDefaults(Action<HttpsConnectionAdapterOptions>)**</span><span class="sxs-lookup"><span data-stu-id="9cbf6-212">**ConfigureHttpsDefaults(Action<HttpsConnectionAdapterOptions>)**</span></span>  
<span data-ttu-id="9cbf6-213">각 HTTPS 엔드포인트에 대해 실행할 구성 `Action`을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-213">Specifies a configuration `Action` to run for each HTTPS endpoint.</span></span> <span data-ttu-id="9cbf6-214">`ConfigureHttpsDefaults`의 여러 차례 호출은 `Action`에 앞서 마지막으로 지정된 `Action`으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-214">Calling `ConfigureHttpsDefaults` multiple times replaces prior `Action`s with the last `Action` specified.</span></span>

<span data-ttu-id="9cbf6-215">**Configure(IConfiguration)**</span><span class="sxs-lookup"><span data-stu-id="9cbf6-215">**Configure(IConfiguration)**</span></span>  
<span data-ttu-id="9cbf6-216">입력으로 [IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration)을 받아들이는 Kestrel를 설정하기 위한 구성 로더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-216">Creates a configuration loader for setting up Kestrel that takes an [IConfiguration](/dotnet/api/microsoft.extensions.configuration.iconfiguration) as input.</span></span> <span data-ttu-id="9cbf6-217">구성은 Kestrel용 구성 섹션에 대해 범위를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-217">The configuration must be scoped to the configuration section for Kestrel.</span></span>

<span data-ttu-id="9cbf6-218">**ListenOptions.UseHttps**</span><span class="sxs-lookup"><span data-stu-id="9cbf6-218">**ListenOptions.UseHttps**</span></span>  
<span data-ttu-id="9cbf6-219">HTTPS를 사용하려면 Kestrel을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-219">Configure Kestrel to use HTTPS.</span></span>

<span data-ttu-id="9cbf6-220">`ListenOptions.UseHttps` 확장:</span><span class="sxs-lookup"><span data-stu-id="9cbf6-220">`ListenOptions.UseHttps` extensions:</span></span>

* <span data-ttu-id="9cbf6-221">`UseHttps` &ndash; 기본 인증서를 통해 HTTPS를 사용하려면 Kestrel 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-221">`UseHttps` &ndash; Configure Kestrel to use HTTPS with the default certificate.</span></span> <span data-ttu-id="9cbf6-222">기본 인증서가 구성되지 않은 경우 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-222">Throws an exception if no default certificate is configured.</span></span>
* `UseHttps(string fileName)`
* `UseHttps(string fileName, string password)`
* `UseHttps(string fileName, string password, Action<HttpsConnectionAdapterOptions> configureOptions)`
* `UseHttps(StoreName storeName, string subject)`
* `UseHttps(StoreName storeName, string subject, bool allowInvalid)`
* `UseHttps(StoreName storeName, string subject, bool allowInvalid, StoreLocation location)`
* `UseHttps(StoreName storeName, string subject, bool allowInvalid, StoreLocation location, Action<HttpsConnectionAdapterOptions> configureOptions)`
* `UseHttps(X509Certificate2 serverCertificate)`
* `UseHttps(X509Certificate2 serverCertificate, Action<HttpsConnectionAdapterOptions> configureOptions)`
* `UseHttps(Action<HttpsConnectionAdapterOptions> configureOptions)`

<span data-ttu-id="9cbf6-223">`ListenOptions.UseHttps` 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="9cbf6-223">`ListenOptions.UseHttps` parameters:</span></span>

* <span data-ttu-id="9cbf6-224">`filename`은 앱의 콘텐츠 파일을 포함하는 디렉터리와 관련된 인증서 파일의 경로 및 파일 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-224">`filename` is the path and file name of a certificate file, relative to the directory that contains the app's content files.</span></span>
* <span data-ttu-id="9cbf6-225">`password`은 X.509 인증서 데이터에 액세스하는 데 필요한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-225">`password` is the password required to access the X.509 certificate data.</span></span>
* <span data-ttu-id="9cbf6-226">`configureOptions`은 `HttpsConnectionAdapterOptions`를 구성하는 `Action`입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-226">`configureOptions` is an `Action` to configure the `HttpsConnectionAdapterOptions`.</span></span> <span data-ttu-id="9cbf6-227">`ListenOptions`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-227">Returns the `ListenOptions`.</span></span>
* <span data-ttu-id="9cbf6-228">`storeName`은 인증서를 로드할 수 있는 인증서 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-228">`storeName` is the certificate store from which to load the certificate.</span></span>
* <span data-ttu-id="9cbf6-229">`subject`은 인증서의 주체 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-229">`subject` is the subject name for the certificate.</span></span>
* <span data-ttu-id="9cbf6-230">`allowInvalid`은 자체 서명된 인증서와 같이 잘못된 인증서를 고려해야 할 경우를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-230">`allowInvalid` indicates if invalid certificates should be considered, such as self-signed certificates.</span></span>
* <span data-ttu-id="9cbf6-231">`location`은 인증서를 로드할 수 있는 저장소 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-231">`location` is the store location to load the certificate from.</span></span>
* <span data-ttu-id="9cbf6-232">`serverCertificate`은 X.509 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-232">`serverCertificate` is the X.509 certificate.</span></span>

<span data-ttu-id="9cbf6-233">프로덕션 내에 HTTPS가 명시적으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-233">In production, HTTPS must be explicitly configured.</span></span> <span data-ttu-id="9cbf6-234">최소한 기본 인증서를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-234">At a minimum, a default certificate must be provided.</span></span>

<span data-ttu-id="9cbf6-235">다음에 설명된 지원되는 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-235">Supported configurations described next:</span></span>

* <span data-ttu-id="9cbf6-236">구성 없음</span><span class="sxs-lookup"><span data-stu-id="9cbf6-236">No configuration</span></span>
* <span data-ttu-id="9cbf6-237">구성에서 기본 인증서를 바꿈</span><span class="sxs-lookup"><span data-stu-id="9cbf6-237">Replace the default certificate from configuration</span></span>
* <span data-ttu-id="9cbf6-238">코드에서 기본값 변경</span><span class="sxs-lookup"><span data-stu-id="9cbf6-238">Change the defaults in code</span></span>

<span data-ttu-id="9cbf6-239">*구성 없음*</span><span class="sxs-lookup"><span data-stu-id="9cbf6-239">*No configuration*</span></span>

<span data-ttu-id="9cbf6-240">Kestrel은 `http://localhost:5000` 및 `https://localhost:5001`에서 수신 대기합니다(기본 인증서가 사용 가능한 경우).</span><span class="sxs-lookup"><span data-stu-id="9cbf6-240">Kestrel listens on `http://localhost:5000` and `https://localhost:5001` (if a default cert is available).</span></span>

<span data-ttu-id="9cbf6-241">다음을 사용하여 URL을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-241">Specify URLs using the:</span></span>

* <span data-ttu-id="9cbf6-242">`ASPNETCORE_URLS` 환경 변수.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-242">`ASPNETCORE_URLS` environment variable.</span></span>
* <span data-ttu-id="9cbf6-243">`--urls` 명령줄 인수.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-243">`--urls` command-line argument.</span></span>
* <span data-ttu-id="9cbf6-244">`urls` 호스트 구성 키.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-244">`urls` host configuration key.</span></span>
* <span data-ttu-id="9cbf6-245">`UseUrls` 확장명 메서드.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-245">`UseUrls` extension method.</span></span>

<span data-ttu-id="9cbf6-246">자세한 내용은 [서버 URLs](xref:fundamentals/hosting#server-urls) 및 [구성 재정의](xref:fundamentals/hosting#overriding-configuration)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-246">For more information, see [Server URLs](xref:fundamentals/hosting#server-urls) and [Overriding configuration](xref:fundamentals/hosting#overriding-configuration).</span></span>

<span data-ttu-id="9cbf6-247">이러한 접근 방식을 사용하여 제공된 값은 하나 이상의 HTTP 및 HTTPS 엔드포인트(기본 인증서가 사용 가능한 경우의 HTTPS)일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-247">The value provided using these approaches can be one or more HTTP and HTTPS endpoints (HTTPS if a default cert is available).</span></span> <span data-ttu-id="9cbf6-248">값을 세미콜론으로 구분된 목록으로 구성합니다(예를 들어, `"Urls": "http://localhost:8000;http://localhost:8001"`).</span><span class="sxs-lookup"><span data-stu-id="9cbf6-248">Configure the value as a semicolon-separated list (for example, `"Urls": "http://localhost:8000;http://localhost:8001"`).</span></span>

<span data-ttu-id="9cbf6-249">*구성에서 기본 인증서를 바꿈*</span><span class="sxs-lookup"><span data-stu-id="9cbf6-249">*Replace the default certificate from configuration*</span></span>

<span data-ttu-id="9cbf6-250">[WebHost.CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)는 Kestrel 구성을 로드하려면 기본적으로 `serverOptions.Configure(context.Configuration.GetSection("Kestrel"))`을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-250">[WebHost.CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) calls `serverOptions.Configure(context.Configuration.GetSection("Kestrel"))` by default to load Kestrel configuration.</span></span> <span data-ttu-id="9cbf6-251">기본 HTTPS 앱 설정 구성 스키마는 Kestrel에 대해 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-251">A default HTTPS app settings configuration schema is available for Kestrel.</span></span> <span data-ttu-id="9cbf6-252">디스크 상의 파일에서 또는 인증서 저장소에서 사용할 인증서 및 URL을 포함하여 여러 엔드포인트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-252">Configure multiple endpoints, including the URLs and the certificates to use, either from a file on disk or from a certificate store.</span></span>

<span data-ttu-id="9cbf6-253">다음 *appsettings.json* 예제에서:</span><span class="sxs-lookup"><span data-stu-id="9cbf6-253">In the following *appsettings.json* example:</span></span>

* <span data-ttu-id="9cbf6-254">잘못된 인증서 사용을 허가하려면 **AllowInvalid**를 `true`으로 설정합니다(예를 들어, 자체 서명된 인증서).</span><span class="sxs-lookup"><span data-stu-id="9cbf6-254">Set **AllowInvalid** to `true` to permit the use of invalid certificates (for example, self-signed certificates).</span></span>
* <span data-ttu-id="9cbf6-255">인증서를 지정하지 않는 모든 HTTPS 엔드포인트(다음 예제에서 **HttpsDefaultCert**)는 **인증서** > **기본**에서 정의된 인증서 또는 개발 인증서로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-255">Any HTTPS endpoint that doesn't specify a certificate (**HttpsDefaultCert** in the example that follows) falls back to the cert defined under **Certificates** > **Default** or the development certificate.</span></span>

```json
{
"Kestrel": {
  "EndPoints": {
    "Http": {
      "Url": "http://localhost:5000"
    },

    "HttpsInlineCertFile": {
      "Url": "https://localhost:5001",
      "Certificate": {
        "Path": "<path to .pfx file>",
        "Password": "<certificate password>"
      }
    },

    "HttpsInlineCertStore": {
      "Url": "https://localhost:5002",
      "Certificate": {
        "Subject": "<subject; required>",
        "Store": "<certificate store; defaults to My>",
        "Location": "<location; defaults to CurrentUser>",
        "AllowInvalid": "<true or false; defaults to false>"
      }
    },

    "HttpsDefaultCert": {
      "Url": "https://localhost:5003"
    },

    "Https": {
      "Url": "https://*:5004",
      "Certificate": {
      "Path": "<path to .pfx file>",
      "Password": "<certificate password>"
      }
    }
    },
    "Certificates": {
      "Default": {
        "Path": "<path to .pfx file>",
        "Password": "<certificate password>"
      }
    }
  }
}
```

<span data-ttu-id="9cbf6-256">모든 인증서 노드에 대해 **경로** 및 **암호**를 사용하는 대신 인증서 저장소 필드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-256">An alternative to using **Path** and **Password** for any certificate node is to specify the certificate using certificate store fields.</span></span> <span data-ttu-id="9cbf6-257">예를 들어, **인증서** > **기본** 인증서는 다음과 같이 지정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-257">For example, the **Certificates** > **Default** certificate can be specified as:</span></span>

```json
"Default": {
  "Subject": "<subject; required>",
  "Store": "<cert store; defaults to My>",
  "Location": "<location; defaults to CurrentUser>",
  "AllowInvalid": "<true or false; defaults to false>"
}
```

<span data-ttu-id="9cbf6-258">스키마 참고 사항:</span><span class="sxs-lookup"><span data-stu-id="9cbf6-258">Schema notes:</span></span>

* <span data-ttu-id="9cbf6-259">엔드포인트 이름은 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-259">Endpoints names are case-insensitive.</span></span> <span data-ttu-id="9cbf6-260">예를 들어, `HTTPS` 및 `Https`는 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-260">For example, `HTTPS` and `Https` are valid.</span></span>
* <span data-ttu-id="9cbf6-261">`Url` 매개 변수는 각 엔드포인트에 대해 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-261">The `Url` parameter is required for each endpoint.</span></span> <span data-ttu-id="9cbf6-262">이 매개 변수에 대한 형식은 단일 값으로 제한된 경우를 제외하고 최상위 `Urls` 구성 매개 변수와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-262">The format for this parameter is the same as the top-level `Urls` configuration parameter except that it's limited to a single value.</span></span>
* <span data-ttu-id="9cbf6-263">이러한 엔드포인트는 추가하기보다는 최상위 `Urls` 구성에서 정의된 엔드포인트를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-263">These endpoints replace those defined in the top-level `Urls` configuration rather than adding to them.</span></span> <span data-ttu-id="9cbf6-264">`Listen`을 통해 코드에서 정의된 엔드포인트는 구성 섹션에서 정의된 엔드포인트로 누적됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-264">Endpoints defined in code via `Listen` are cumulative with the endpoints defined in the configuration section.</span></span>
* <span data-ttu-id="9cbf6-265">`Certificate` 섹션은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-265">The `Certificate` section is optional.</span></span> <span data-ttu-id="9cbf6-266">`Certificate` 섹션이 지정되지 않은 경우 이전 시나리오에서 정의된 기본값이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-266">If the `Certificate` section isn't specified, the defaults defined in earlier scenarios are used.</span></span> <span data-ttu-id="9cbf6-267">기본값이 사용 가능하지 않은 경우 서버는 예외를 throw하고 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-267">If no defaults are available, the server throws an exception and fails to start.</span></span>
* <span data-ttu-id="9cbf6-268">`Certificate` 섹션은 **경로**&ndash;**암호** 및 **주체**&ndash;**저장소** 인증서 모두를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-268">The `Certificate` section supports both **Path**&ndash;**Password** and **Subject**&ndash;**Store** certificates.</span></span>
* <span data-ttu-id="9cbf6-269">많은 엔드포인트가 포트 충돌을 일으키지 않는 한 이런 방식으로 정의될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-269">Any number of endpoints may be defined in this way so long as they don't cause port conflicts.</span></span>
* <span data-ttu-id="9cbf6-270">`serverOptions.Configure(context.Configuration.GetSection("Kestrel"))`은 구성된 엔드포인트의 설정을 보완하는 데 사용될 수 있는 `.Endpoint(string name, options => { })` 메서드를 통해 `KestrelConfigurationLoader`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-270">`serverOptions.Configure(context.Configuration.GetSection("Kestrel"))` returns a `KestrelConfigurationLoader` with an `.Endpoint(string name, options => { })` method that can be used to supplement a configured endpoint's settings:</span></span>

  ```csharp
  serverOptions.Configure(context.Configuration.GetSection("Kestrel"))
      .Endpoint("HTTPS", opt =>
      {
          opt.HttpsOptions.SslProtocols = SslProtocols.Tls12;
      });
  ```

  <span data-ttu-id="9cbf6-271">또한 `KestrelServerOptions.ConfigurationLoader`에 직접 액세스하여 `WebHost.CreatedDeafaultBuilder`에서 제공한 로더와 같이 기존 로더에서 반복을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-271">You can also directly access `KestrelServerOptions.ConfigurationLoader` to keep iterating on the existing loader, such as the one provided by `WebHost.CreatedDeafaultBuilder`.</span></span>

* <span data-ttu-id="9cbf6-272">각 엔드포인트에 대한 구성 섹션은 `Endpoint` 메서드의 옵션에서 사용 가능하므로 사용자 지정 설정을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-272">The configuration section for each endpoint is a available on the options in the `Endpoint` method so that custom settings may be read.</span></span>
* <span data-ttu-id="9cbf6-273">여러 구성은 다른 섹션을 통해 다시 `serverOptions.Configure(context.Configuration.GetSection("Kestrel"))`을 호출하여 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-273">Multiple configurations may be loaded by calling `serverOptions.Configure(context.Configuration.GetSection("Kestrel"))` again with another section.</span></span> <span data-ttu-id="9cbf6-274">`Load`은 이전 인스턴스에서 명시적으로 호출되지 않는 한 마지막 구성만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-274">Only the last configuration is used, unless `Load` is explicitly called on prior instances.</span></span> <span data-ttu-id="9cbf6-275">메타패키지는 `Load`을 호출하지 않으므로 기본 구성 섹션을 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-275">The metapackage doesn't call `Load` so that its default configuration section may be replaced.</span></span>
* <span data-ttu-id="9cbf6-276">`KestrelConfigurationLoader`은 `KestrelServerOptions`에서 `Endpoint` 오버로드로 `Listen` API 제품군을 미러링하므로 코드 및 구성 엔드포인트를 동일 장소에서 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-276">`KestrelConfigurationLoader` mirrors the `Listen` family of APIs from `KestrelServerOptions` as `Endpoint` overloads, so code and config endpoints may be configured in the same place.</span></span> <span data-ttu-id="9cbf6-277">이러한 오버로드는 이름을 사용하지 않고 구성에서 기본 설정만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-277">These overloads don't use names and only consume default settings from configuration.</span></span>

<span data-ttu-id="9cbf6-278">*코드에서 기본값 변경*</span><span class="sxs-lookup"><span data-stu-id="9cbf6-278">*Change the defaults in code*</span></span>

<span data-ttu-id="9cbf6-279">`ConfigureEndpointDefaults` 및 `ConfigureHttpsDefaults`는 이전 시나리오에서 지정된 기본 인증서 재정의를 포함한 `ListenOptions` 및 `HttpsConnectionAdapterOptions`에 대해 기본 설정을 변경하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-279">`ConfigureEndpointDefaults` and `ConfigureHttpsDefaults` can be used to change default settings for `ListenOptions` and `HttpsConnectionAdapterOptions`, including overriding the default certificate specified in the prior scenario.</span></span> <span data-ttu-id="9cbf6-280">`ConfigureEndpointDefaults` 및 `ConfigureHttpsDefaults`는 모든 엔드포인트가 구성되기 전에 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-280">`ConfigureEndpointDefaults` and `ConfigureHttpsDefaults` should be called before any endpoints are configured.</span></span>

```csharp
options.ConfigureEndpointDefaults(opt =>
{
    opt.NoDelay = true;
});

options.ConfigureHttpsDefaults(httpsOptions =>
{
    httpsOptions.SslProtocols = SslProtocols.Tls12;
});
```

<span data-ttu-id="9cbf6-281">*SNI에 대한 Kestrel 지원*</span><span class="sxs-lookup"><span data-stu-id="9cbf6-281">*Kestrel support for SNI*</span></span>

<span data-ttu-id="9cbf6-282">[서버 이름 표시(SNI)](https://tools.ietf.org/html/rfc6066#section-3)는 동일한 IP 주소 및 포트에서 여러 도메인을 호스트하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-282">[Server Name Indication (SNI)](https://tools.ietf.org/html/rfc6066#section-3) can be used to host multiple domains on the same IP address and port.</span></span> <span data-ttu-id="9cbf6-283">함수에 대한 SNI의 경우 클라이언트는 TLS 핸드셰이크 동안 보안 세션에 대한 호스트 이름을 서버로 보내므로 서버에서 올바른 인증서를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-283">For SNI to function, the client sends the host name for the secure session to the server during the TLS handshake so that the server can provide the correct certificate.</span></span> <span data-ttu-id="9cbf6-284">TLS 핸드셰이크 다음에 오는 보안 세션 동안 클라이언트는 서버와 암호화된 통신을 위해 제공된 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-284">The client uses the furnished certificate for encrypted communication with the server during the secure session that follows the TLS handshake.</span></span>

<span data-ttu-id="9cbf6-285">Kestrel은 `ServerCertificateSelector` 콜백을 통해 SNI를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-285">Kestrel supports SNI via the `ServerCertificateSelector` callback.</span></span> <span data-ttu-id="9cbf6-286">앱이 호스트 이름을 검사하고 적절한 인증서를 선택하도록 허용하려면 연결당 한 번씩 콜백이 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-286">The callback is invoked once per connection to allow the app to inspect the host name and select the appropriate certificate.</span></span>

<span data-ttu-id="9cbf6-287">SNI 지원은 대상 프레임워크 `netcoreapp2.1`에서 실행할 것을 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-287">SNI support requires running on target framework `netcoreapp2.1`.</span></span> <span data-ttu-id="9cbf6-288">`netcoreapp2.0` 및 `net461`에서 콜백이 호출되지만 `name` 은 항상 `null`입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-288">On `netcoreapp2.0` and `net461`, the callback is invoked but the `name` is always `null`.</span></span> <span data-ttu-id="9cbf6-289">클라이언트가 TLS 핸드셰이크에서 호스트 이름 매개 변수를 제공하지 않는 경우 `name`은 또한 `null`입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-289">The `name` is also `null` if the client doesn't provide the host name parameter in the TLS handshake.</span></span>

```csharp
WebHost.CreateDefaultBuilder()
    .UseKestrel((context, options) =>
    {
        options.ListenAnyIP(5005, listenOptions =>
        {
            listenOptions.UseHttps(httpsOptions =>
            {
                var localhostCert = CertificateLoader.LoadFromStoreCert(
                    "localhost", "My", StoreLocation.CurrentUser, 
                    allowInvalid: true);
                var exampleCert = CertificateLoader.LoadFromStoreCert(
                    "example.com", "My", StoreLocation.CurrentUser, 
                    allowInvalid: true);
                var subExampleCert = CertificateLoader.LoadFromStoreCert(
                    "sub.example.com", "My", StoreLocation.CurrentUser, 
                    allowInvalid: true);
                var certs = new Dictionary(StringComparer.OrdinalIgnoreCase);
                certs["localhost"] = localhostCert;
                certs["example.com"] = exampleCert;
                certs["sub.example.com"] = subExampleCert;

                httpsOptions.ServerCertificateSelector = (connectionContext, name) =>
                {
                    if (name != null && certs.TryGetValue(name, out var cert))
                    {
                        return cert;
                    }

                    return exampleCert;
                };
            });
        });
    });
```
::: moniker-end

<span data-ttu-id="9cbf6-290">**TCP 소켓에 바인딩**</span><span class="sxs-lookup"><span data-stu-id="9cbf6-290">**Bind to a TCP socket**</span></span>

<span data-ttu-id="9cbf6-291">[수신 대기](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listen) 메서드는 TCP 소켓에 바인딩하고 옵션 람다는 SSL 인증서 구성을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-291">The [Listen](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listen) method binds to a TCP socket, and an options lambda permits SSL certificate configuration:</span></span>

[!code-csharp[](kestrel/samples/2.x/Program.cs?name=snippet_DefaultBuilder&highlight=9-16)]

<span data-ttu-id="9cbf6-292">[ListenOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.listenoptions)를 사용하여 이 예에서 특정 엔드포인트에 대한 SSL을 구성하는 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-292">Notice how this example configures SSL for a particular endpoint by using [ListenOptions](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.listenoptions).</span></span> <span data-ttu-id="9cbf6-293">동일한 API를 사용하여 특정 엔드포인트에 대한 다른 Kestrel 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-293">Use the same API to configure other Kestrel settings for specific endpoints.</span></span>

[!INCLUDE [How to make an X.509 cert](~/includes/make-x509-cert.md)]

<span data-ttu-id="9cbf6-294">**Unix 소켓에 바인딩**</span><span class="sxs-lookup"><span data-stu-id="9cbf6-294">**Bind to a Unix socket**</span></span>

<span data-ttu-id="9cbf6-295">이 예제에 나와 있는 것처럼 Nginx를 사용하여 향상된 성능을 위해 [ListenUnixSocket](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listenunixsocket)을 통해 Unix 소켓을 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-295">Listen on a Unix socket with [ListenUnixSocket](/dotnet/api/microsoft.aspnetcore.server.kestrel.core.kestrelserveroptions.listenunixsocket) for improved performance with Nginx, as shown in this example:</span></span>

[!code-csharp[](kestrel/samples/2.x/Program.cs?name=snippet_UnixSocket)]

<span data-ttu-id="9cbf6-296">**포트 0**</span><span class="sxs-lookup"><span data-stu-id="9cbf6-296">**Port 0**</span></span>

<span data-ttu-id="9cbf6-297">포트 번호 `0`가 지정되는 경우 Kestrel은 동적으로 사용 가능한 포트에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-297">When the port number `0` is specified, Kestrel dynamically binds to an available port.</span></span> <span data-ttu-id="9cbf6-298">다음 예제에서는 Kestrel이 실제로 런타임에 바인딩한 포트를 확인하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-298">The following example shows how to determine which port Kestrel actually bound at runtime:</span></span>

[!code-csharp[](kestrel/samples/2.x/Startup.cs?name=snippet_Port0&highlight=3)]

<span data-ttu-id="9cbf6-299">앱이 실행되는 경우 콘솔 창 출력은 앱이 연결될 수 있는 동적 포트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-299">When the app is run, the console window output indicates the dynamic port where the app can be reached:</span></span>

```console
Now listening on: http://127.0.0.1:48508
```

<span data-ttu-id="9cbf6-300">**UseUrls, --urls 명령 줄 인수, urls 호스트 구성 키 및 ASPNETCORE_URLS 환경 변수 제한 사항**</span><span class="sxs-lookup"><span data-stu-id="9cbf6-300">**UseUrls, --urls command-line argument, urls host configuration key, and ASPNETCORE_URLS environment variable limitations**</span></span>

<span data-ttu-id="9cbf6-301">다음 방법으로 엔트포인트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-301">Configure endpoints with the following approaches:</span></span>

* [<span data-ttu-id="9cbf6-302">UseUrls</span><span class="sxs-lookup"><span data-stu-id="9cbf6-302">UseUrls</span></span>](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useurls)
* <span data-ttu-id="9cbf6-303">`--urls` 명령줄 인수</span><span class="sxs-lookup"><span data-stu-id="9cbf6-303">`--urls` command-line argument</span></span>
* <span data-ttu-id="9cbf6-304">`urls` 호스트 구성 키</span><span class="sxs-lookup"><span data-stu-id="9cbf6-304">`urls` host configuration key</span></span>
* <span data-ttu-id="9cbf6-305">`ASPNETCORE_URLS`환경 변수</span><span class="sxs-lookup"><span data-stu-id="9cbf6-305">`ASPNETCORE_URLS` environment variable</span></span>

<span data-ttu-id="9cbf6-306">이러한 메서드는 코드를 Kestrel이 아닌 서버와 작동하도록 하려는 경우 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-306">These methods are useful for making code work with servers other than Kestrel.</span></span> <span data-ttu-id="9cbf6-307">그러나 이러한 제한 사항을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-307">However, be aware of these limitations:</span></span>

* <span data-ttu-id="9cbf6-308">HTTPS 끝점 구성에서 기본 인증서를 제공하지 않는 한 이러한 방법으로는 SSL을 사용할 수 없습니다(예: 이 항목의 앞부분에 표시된 것처럼 `KestrelServerOptions` 구성 또는 구성 파일 사용).</span><span class="sxs-lookup"><span data-stu-id="9cbf6-308">SSL can't be used with these approaches unless a default certificate is provided in the HTTPS endpoint configuration (for example, using `KestrelServerOptions` configuration or a configuration file as shown earlier in this topic).</span></span>
* <span data-ttu-id="9cbf6-309">`Listen` 및 `UseUrls` 방식 모두를 동시에 사용할 경우 `Listen` 엔드포인트는 `UseUrls` 엔드포인트를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-309">When both the `Listen` and `UseUrls` approaches are used simultaneously, the `Listen` endpoints override the `UseUrls` endpoints.</span></span>

<span data-ttu-id="9cbf6-310">**IIS 엔드포인트 구성**</span><span class="sxs-lookup"><span data-stu-id="9cbf6-310">**IIS endpoint configuration**</span></span>

<span data-ttu-id="9cbf6-311">IIS를 사용하는 경우 IIS 재정의 바인딩에 대한 URL 바인딩은 `Listen` 또는 `UseUrls`에 의해 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-311">When using IIS, the URL bindings for IIS override bindings are set by either `Listen` or `UseUrls`.</span></span> <span data-ttu-id="9cbf6-312">자세한 내용은 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-312">For more information, see the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) topic.</span></span>

#### <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="9cbf6-313">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="9cbf6-313">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

<span data-ttu-id="9cbf6-314">기본적으로 ASP.NET Core는 `http://localhost:5000`으로 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-314">By default, ASP.NET Core binds to `http://localhost:5000`.</span></span> <span data-ttu-id="9cbf6-315">Kestrel 사용에 대한 URL 접두사 및 포트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-315">Configure URL prefixes and ports for Kestrel using:</span></span>

* <span data-ttu-id="9cbf6-316">[UseUrls](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useurls?view=aspnetcore-1.1) 확장 메서드</span><span class="sxs-lookup"><span data-stu-id="9cbf6-316">[UseUrls](/dotnet/api/microsoft.aspnetcore.hosting.hostingabstractionswebhostbuilderextensions.useurls?view=aspnetcore-1.1) extension method</span></span>
* <span data-ttu-id="9cbf6-317">`--urls` 명령줄 인수</span><span class="sxs-lookup"><span data-stu-id="9cbf6-317">`--urls` command-line argument</span></span>
* <span data-ttu-id="9cbf6-318">`urls` 호스트 구성 키</span><span class="sxs-lookup"><span data-stu-id="9cbf6-318">`urls` host configuration key</span></span>
* <span data-ttu-id="9cbf6-319">`ASPNETCORE_URLS` 환경 변수를 포함한 ASP.NET Core 구성 시스템</span><span class="sxs-lookup"><span data-stu-id="9cbf6-319">ASP.NET Core configuration system, including `ASPNETCORE_URLS` environment variable</span></span>

<span data-ttu-id="9cbf6-320">이러한 메서드에 대한 자세한 내용은 [호스팅](xref:fundamentals/hosting)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-320">For more information on these methods, see [Hosting](xref:fundamentals/hosting).</span></span>

<span data-ttu-id="9cbf6-321">**IIS 엔드포인트 구성**</span><span class="sxs-lookup"><span data-stu-id="9cbf6-321">**IIS endpoint configuration**</span></span>

<span data-ttu-id="9cbf6-322">IIS를 사용하는 경우 IIS 재정의 바인딩에 대한 URL 바인딩은 `UseUrls`에 의해 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-322">When using IIS, the URL bindings for IIS override bindings set by `UseUrls`.</span></span> <span data-ttu-id="9cbf6-323">자세한 내용은 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-323">For more information, see the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) topic.</span></span>

* * *

### <a name="url-prefixes"></a><span data-ttu-id="9cbf6-324">URL 접두사</span><span class="sxs-lookup"><span data-stu-id="9cbf6-324">URL prefixes</span></span>

<span data-ttu-id="9cbf6-325">`UseUrls`, `--urls` 명령줄 인수, `urls` 호스트 구성 키 또는 `ASPNETCORE_URLS` 환경 변수를 사용하는 경우 URL 접두사는 다음 형식 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-325">When using `UseUrls`, `--urls` command-line argument, `urls` host configuration key, or `ASPNETCORE_URLS` environment variable, the URL prefixes can be in any of the following formats.</span></span>

#### <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="9cbf6-326">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="9cbf6-326">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x/)

<span data-ttu-id="9cbf6-327">HTTP URL 접두사만 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-327">Only HTTP URL prefixes are valid.</span></span> <span data-ttu-id="9cbf6-328">Kestrel은 `UseUrls`을 사용하여 URL 바인딩을 구성하는 경우 SSL을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-328">Kestrel doesn't support SSL when configuring URL bindings using `UseUrls`.</span></span>

* <span data-ttu-id="9cbf6-329">포트 번호가 있는 IPv4 주소</span><span class="sxs-lookup"><span data-stu-id="9cbf6-329">IPv4 address with port number</span></span>

  ```
  http://65.55.39.10:80/
  ```

  <span data-ttu-id="9cbf6-330">`0.0.0.0`은 모든 IPv4 주소에 바인딩하는 특별한 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-330">`0.0.0.0` is a special case that binds to all IPv4 addresses.</span></span>


* <span data-ttu-id="9cbf6-331">포트 번호가 있는 IPv6 주소</span><span class="sxs-lookup"><span data-stu-id="9cbf6-331">IPv6 address with port number</span></span>

  ```
  http://[0:0:0:0:0:ffff:4137:270a]:80/
  ```

  <span data-ttu-id="9cbf6-332">`[::]`는 IPv4 `0.0.0.0`에 해당하는 IPv6입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-332">`[::]` is the IPv6 equivalent of IPv4 `0.0.0.0`.</span></span>


* <span data-ttu-id="9cbf6-333">포트 번호가 있는 호스트 이름</span><span class="sxs-lookup"><span data-stu-id="9cbf6-333">Host name with port number</span></span>

  ```
  http://contoso.com:80/
  http://*:80/
  ```

  <span data-ttu-id="9cbf6-334">호스트 이름, `*` 및 `+`는 특별하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-334">Host names, `*`, and `+`, aren't special.</span></span> <span data-ttu-id="9cbf6-335">유효한 IP 주소 또는 `localhost`로 인식하지 않는 모든 항목은 모든 IPv4 및 IPv6 IP에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-335">Anything not recognized as a valid IP address or `localhost` binds to all IPv4 and IPv6 IPs.</span></span> <span data-ttu-id="9cbf6-336">서로 다른 호스트 이름을 같은 포트에서 서로 다른 ASP.NET Core 앱에 바인딩하려면 IIS, Nginx 또는 Apache와 같은 역방향 프록시 서버 또는 [HTTP.sys](xref:fundamentals/servers/httpsys)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-336">To bind different host names to different ASP.NET Core apps on the same port, use [HTTP.sys](xref:fundamentals/servers/httpsys) or a reverse proxy server, such as IIS, Nginx, or Apache.</span></span>

  > [!WARNING]
  > <span data-ttu-id="9cbf6-337">호스트 필터링을 사용하도록 설정된 역방향 프록시를 사용하지 않는 경우 [호스트 필터링](#host-filtering)을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-337">If not using a reverse proxy with host filtering enabled, enable [host filtering](#host-filtering).</span></span>

* <span data-ttu-id="9cbf6-338">포트 번호가 있는 호스트 `localhost` 이름 또는 포트 번호가 있는 루프백 IP</span><span class="sxs-lookup"><span data-stu-id="9cbf6-338">Host `localhost` name with port number or loopback IP with port number</span></span>

  ```
  http://localhost:5000/
  http://127.0.0.1:5000/
  http://[::1]:5000/
  ```

  <span data-ttu-id="9cbf6-339">`localhost`가 지정되면 Kestrel은 IPv4 및 IPv6 루프백 인터페이스 모두에 바인딩하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-339">When `localhost` is specified, Kestrel attempts to bind to both IPv4 and IPv6 loopback interfaces.</span></span> <span data-ttu-id="9cbf6-340">요청된 포트가 루프백 인터페이스 중 하나의 다른 서비스에서 사용 중인 경우 Kestrel은 시작에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-340">If the requested port is in use by another service on either loopback interface, Kestrel fails to start.</span></span> <span data-ttu-id="9cbf6-341">루프백 인터페이스 중 하나를 다른 이유(일반적으로 IPv6이 지원되지 않으므로)로 사용할 수 없는 경우 Kestrel은 경고를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-341">If either loopback interface is unavailable for any other reason (most commonly because IPv6 isn't supported), Kestrel logs a warning.</span></span>

#### <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="9cbf6-342">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="9cbf6-342">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

* <span data-ttu-id="9cbf6-343">포트 번호가 있는 IPv4 주소</span><span class="sxs-lookup"><span data-stu-id="9cbf6-343">IPv4 address with port number</span></span>

  ```
  http://65.55.39.10:80/
  https://65.55.39.10:443/
  ```

  <span data-ttu-id="9cbf6-344">`0.0.0.0`은 모든 IPv4 주소에 바인딩하는 특별한 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-344">`0.0.0.0` is a special case that binds to all IPv4 addresses.</span></span>

* <span data-ttu-id="9cbf6-345">포트 번호가 있는 IPv6 주소</span><span class="sxs-lookup"><span data-stu-id="9cbf6-345">IPv6 address with port number</span></span>

  ```
  http://[0:0:0:0:0:ffff:4137:270a]:80/
  https://[0:0:0:0:0:ffff:4137:270a]:443/
  ```

  <span data-ttu-id="9cbf6-346">`[::]`는 IPv4 `0.0.0.0`에 해당하는 IPv6입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-346">`[::]` is the IPv6 equivalent of IPv4 `0.0.0.0`.</span></span>

* <span data-ttu-id="9cbf6-347">포트 번호가 있는 호스트 이름</span><span class="sxs-lookup"><span data-stu-id="9cbf6-347">Host name with port number</span></span>

  ```
  http://contoso.com:80/
  http://*:80/
  https://contoso.com:443/
  https://*:443/
  ```

  <span data-ttu-id="9cbf6-348">호스트 이름, `*` 및 `+`는 특별하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-348">Host names, `*`, and `+` aren't special.</span></span> <span data-ttu-id="9cbf6-349">인식된 IP 주소 또는 `localhost`가 아닌 모든 항목은 모든 IPv4 및 IPv6 IP에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-349">Anything that isn't a recognized IP address or `localhost` binds to all IPv4 and IPv6 IPs.</span></span> <span data-ttu-id="9cbf6-350">서로 다른 호스트 이름을 같은 포트에서 서로 다른 ASP.NET Core 앱에 바인딩하려면 IIS, Nginx 또는 Apache와 같은 역방향 프록시 서버 또는 [WebListener](xref:fundamentals/servers/weblistener)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-350">To bind different host names to different ASP.NET Core apps on the same port, use [WebListener](xref:fundamentals/servers/weblistener) or a reverse proxy server, such as IIS, Nginx, or Apache.</span></span>

* <span data-ttu-id="9cbf6-351">포트 번호가 있는 호스트 `localhost` 이름 또는 포트 번호가 있는 루프백 IP</span><span class="sxs-lookup"><span data-stu-id="9cbf6-351">Host `localhost` name with port number or loopback IP with port number</span></span>

  ```
  http://localhost:5000/
  http://127.0.0.1:5000/
  http://[::1]:5000/
  ```

  <span data-ttu-id="9cbf6-352">`localhost`가 지정되면 Kestrel은 IPv4 및 IPv6 루프백 인터페이스 모두에 바인딩하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-352">When `localhost` is specified, Kestrel attempts to bind to both IPv4 and IPv6 loopback interfaces.</span></span> <span data-ttu-id="9cbf6-353">요청된 포트가 루프백 인터페이스 중 하나의 다른 서비스에서 사용 중인 경우 Kestrel은 시작에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-353">If the requested port is in use by another service on either loopback interface, Kestrel fails to start.</span></span> <span data-ttu-id="9cbf6-354">루프백 인터페이스 중 하나를 다른 이유(일반적으로 IPv6이 지원되지 않으므로)로 사용할 수 없는 경우 Kestrel은 경고를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-354">If either loopback interface is unavailable for any other reason (most commonly because IPv6 isn't supported), Kestrel logs a warning.</span></span>

* <span data-ttu-id="9cbf6-355">Unix 소켓</span><span class="sxs-lookup"><span data-stu-id="9cbf6-355">Unix socket</span></span>

  ```
  http://unix:/run/dan-live.sock
  ```

<span data-ttu-id="9cbf6-356">**포트 0**</span><span class="sxs-lookup"><span data-stu-id="9cbf6-356">**Port 0**</span></span>

<span data-ttu-id="9cbf6-357">포트 번호 `0`가 지정되는 경우 Kestrel은 동적으로 사용 가능한 포트에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-357">When the port number is `0` is specified, Kestrel dynamically binds to an available port.</span></span> <span data-ttu-id="9cbf6-358">포트 `0`에 바인딩은 `localhost`를 제외하고 모든 호스트 이름 또는 IP에 대해 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-358">Binding to port `0` is allowed for any host name or IP except for `localhost`.</span></span>

<span data-ttu-id="9cbf6-359">앱이 실행되는 경우 콘솔 창 출력은 앱이 연결될 수 있는 동적 포트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-359">When the app is run, the console window output indicates the dynamic port where the app can be reached:</span></span>

```console
Now listening on: http://127.0.0.1:48508
```

<span data-ttu-id="9cbf6-360">**SSL에 대한 URL 접두사**</span><span class="sxs-lookup"><span data-stu-id="9cbf6-360">**URL prefixes for SSL**</span></span>

<span data-ttu-id="9cbf6-361">`UseHttps` 확장 메서드를 호출하는 경우 `https:`에 URL 접두사를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-361">If calling the `UseHttps` extension method, be sure to include URL prefixes with `https:`:</span></span>

```csharp
var host = new WebHostBuilder()
    .UseKestrel(options =>
    {
        options.UseHttps("testCert.pfx", "testPassword");
    })
   .UseUrls("http://localhost:5000", "https://localhost:5001")
   .UseContentRoot(Directory.GetCurrentDirectory())
   .UseStartup<Startup>()
   .Build();
```

> [!NOTE]
> <span data-ttu-id="9cbf6-362">HTTPS 및 HTTP는 동일한 포트에서 호스팅될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-362">HTTPS and HTTP can't be hosted on the same port.</span></span>

[!INCLUDE [How to make an X.509 cert](~/includes/make-x509-cert.md)]

* * *

## <a name="host-filtering"></a><span data-ttu-id="9cbf6-363">호스트 필터링</span><span class="sxs-lookup"><span data-stu-id="9cbf6-363">Host filtering</span></span>

<span data-ttu-id="9cbf6-364">Kestrel은 `http://example.com:5000`과 같은 접두사에 따라 구성을 지원하지만 일반적으로 호스트 이름을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-364">While Kestrel supports configuration based on prefixes such as `http://example.com:5000`, Kestrel largely ignores the host name.</span></span> <span data-ttu-id="9cbf6-365">호스트 `localhost`은 루프백 주소에 바인딩하는 데 사용된 특별한 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-365">Host `localhost` is a special case used for binding to loopback addresses.</span></span> <span data-ttu-id="9cbf6-366">명시적 IP 주소를 제외한 모든 호스트는 모든 공용 IP 주소에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-366">Any host other than an explicit IP address binds to all public IP addresses.</span></span> <span data-ttu-id="9cbf6-367">이 정보 중 어느 것도 요청 `Host` 헤더의 유효성을 검사하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-367">None of this information is used to validate request `Host` headers.</span></span>

<span data-ttu-id="9cbf6-368">두 가지 해결 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-368">There are two workarounds:</span></span>

* <span data-ttu-id="9cbf6-369">호스트 헤더 필터링을 사용한 역방향 프록시 뒤의 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-369">Host behind a reverse proxy with host header filtering.</span></span> <span data-ttu-id="9cbf6-370">ASP.NET Core 1.x에서 Kestrel에 대한 유일한 지원 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-370">This was the only supported scenario for Kestrel in ASP.NET Core 1.x.</span></span>
* <span data-ttu-id="9cbf6-371">미들웨어를 사용하여 `Host` 헤더로 요청을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-371">Use a middleware to filter requests by the `Host` header.</span></span> <span data-ttu-id="9cbf6-372">샘플 미들웨어는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-372">A sample middleware follows:</span></span>

```csharp
using Microsoft.AspNetCore.Http;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.Logging;
using Microsoft.Extensions.Primitives;
using Microsoft.Net.Http.Headers;
using System;
using System.Collections.Generic;
using System.Threading.Tasks;

// A normal middleware would provide an options type, config binding, extension methods, etc..
// This intentionally does all of the work inside of the middleware so it can be
// easily copy-pasted into docs and other projects.
public class HostFilteringMiddleware
{
    private readonly RequestDelegate _next;
    private readonly IList<string> _hosts;
    private readonly ILogger<HostFilteringMiddleware> _logger;

    public HostFilteringMiddleware(RequestDelegate next, IConfiguration config, ILogger<HostFilteringMiddleware> logger)
    {
        if (config == null)
        {
            throw new ArgumentNullException(nameof(config));
        }

        _next = next ?? throw new ArgumentNullException(nameof(next));
        _logger = logger ?? throw new ArgumentNullException(nameof(logger));

        // A semicolon separated list of host names without the port numbers.
        // IPv6 addresses must use the bounding brackets and be in their normalized form.
        _hosts = config["AllowedHosts"]?.Split(new[] { ';' }, StringSplitOptions.RemoveEmptyEntries);
        if (_hosts == null || _hosts.Count == 0)
        {
            throw new InvalidOperationException("No configuration entry found for AllowedHosts.");
        }
    }

    public Task Invoke(HttpContext context)
    {
        if (!ValidateHost(context))
        {
            context.Response.StatusCode = 400;
            _logger.LogDebug("Request rejected due to incorrect Host header.");
            return Task.CompletedTask;
        }

        return _next(context);
    }

    // This does not duplicate format validations that are expected to be performed by the host.
    private bool ValidateHost(HttpContext context)
    {
        StringSegment host = context.Request.Headers[HeaderNames.Host].ToString().Trim();

        if (StringSegment.IsNullOrEmpty(host))
        {
            // Http/1.0 does not require the Host header.
            // Http/1.1 requires the header but the value may be empty.
            return true;
        }

        // Drop the port

        var colonIndex = host.LastIndexOf(':');

        // IPv6 special case
        if (host.StartsWith("[", StringComparison.Ordinal))
        {
            var endBracketIndex = host.IndexOf(']');
            if (endBracketIndex < 0)
            {
                // Invalid format
                return false;
            }
            if (colonIndex < endBracketIndex)
            {
                // No port, just the IPv6 Host
                colonIndex = -1;
            }
        }

        if (colonIndex > 0)
        {
            host = host.Subsegment(0, colonIndex);
        }

        foreach (var allowedHost in _hosts)
        {
            if (StringSegment.Equals(allowedHost, host, StringComparison.OrdinalIgnoreCase))
            {
                return true;
            }

            // Sub-domain wildcards: *.example.com
            if (allowedHost.StartsWith("*.", StringComparison.Ordinal) && host.Length >= allowedHost.Length)
            {
                // .example.com
                var allowedRoot = new StringSegment(allowedHost, 1, allowedHost.Length - 1);

                var hostRoot = host.Subsegment(host.Length - allowedRoot.Length, allowedRoot.Length);
                if (hostRoot.Equals(allowedRoot, StringComparison.OrdinalIgnoreCase))
                {
                    return true;
                }
            }
        }

        return false;
    }
}
```

<span data-ttu-id="9cbf6-373">`Startup.Configure`에 위의 `HostFilteringMiddleware`을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-373">Register the preceding `HostFilteringMiddleware` in `Startup.Configure`.</span></span> <span data-ttu-id="9cbf6-374">[미들웨어 등록 순서](xref:fundamentals/middleware/index#ordering)가 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-374">Note that the [ordering of middleware registration](xref:fundamentals/middleware/index#ordering) is important.</span></span> <span data-ttu-id="9cbf6-375">등록은 진단 미들웨어 등록 후 즉시 이뤄져야 합니다(예: `app.UseExceptionHandler`).</span><span class="sxs-lookup"><span data-stu-id="9cbf6-375">Registration should occur immediately after Diagnostic Middleware registration (for example, `app.UseExceptionHandler`).</span></span>

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
        app.UseBrowserLink();
    }
    else
    {
        app.UseExceptionHandler("/Home/Error");
    }

    app.UseMiddleware<HostFilteringMiddleware>();

    app.UseMvcWithDefaultRoute();
}
```

<span data-ttu-id="9cbf6-376">위의 미들웨어는 *appsettings.\< EnvironmentName>.json*에서 `AllowedHosts` 키를 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-376">The preceding middleware expects an `AllowedHosts` key in *appsettings.\<EnvironmentName>.json*.</span></span> <span data-ttu-id="9cbf6-377">이 키의 값은 세미콜론으로 구분된 포트 번호 없는 호스트 이름 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-377">This key's value is a semicolon-delimited list of host names without the port numbers.</span></span> <span data-ttu-id="9cbf6-378">*appsettings.Production.json*에 `AllowedHosts` 키-값 쌍을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9cbf6-378">Include the `AllowedHosts` key-value pair in *appsettings.Production.json*:</span></span>

```json
{
  "AllowedHosts": "example.com"
}
```

<span data-ttu-id="9cbf6-379">*appsettings.Development.json* (로컬 호스트 구성 파일):</span><span class="sxs-lookup"><span data-stu-id="9cbf6-379">*appsettings.Development.json* (localhost configuration file):</span></span>

```json
{
  "AllowedHosts": "localhost"
}
```

## <a name="additional-resources"></a><span data-ttu-id="9cbf6-380">추가 자료</span><span class="sxs-lookup"><span data-stu-id="9cbf6-380">Additional resources</span></span>

* [<span data-ttu-id="9cbf6-381">HTTPS 적용</span><span class="sxs-lookup"><span data-stu-id="9cbf6-381">Enforce HTTPS</span></span>](xref:security/enforcing-ssl)
* [<span data-ttu-id="9cbf6-382">Kestrel 소스 코드</span><span class="sxs-lookup"><span data-stu-id="9cbf6-382">Kestrel source code</span></span>](https://github.com/aspnet/KestrelHttpServer)
