---
title: "ASP.NET Core에서 Kestrel 웹 서버 구현"
author: tdykstra
description: "libuv 기반 ASP.NET Core에 대한 플랫폼 간 웹 서버인 Kestrel을 소개합니다."
manager: wpickett
ms.author: tdykstra
ms.custom: H1Hack27Feb2017
ms.date: 08/02/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/servers/kestrel
ms.openlocfilehash: bfe7644891296c7c3485c9a870d90951ba87e9e8
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="introduction-to-kestrel-web-server-implementation-in-aspnet-core"></a><span data-ttu-id="dd99d-103">ASP.NET Core에서 Kestrel 웹 서버 구현에 대한 소개</span><span class="sxs-lookup"><span data-stu-id="dd99d-103">Introduction to Kestrel web server implementation in ASP.NET Core</span></span>

<span data-ttu-id="dd99d-104">작성자: [Tom Dykstra](https://github.com/tdykstra), [Chris Ross](https://github.com/Tratcher) 및 [Stephen Halter](https://twitter.com/halter73)</span><span class="sxs-lookup"><span data-stu-id="dd99d-104">By [Tom Dykstra](https://github.com/tdykstra), [Chris Ross](https://github.com/Tratcher), and [Stephen Halter](https://twitter.com/halter73)</span></span>

<span data-ttu-id="dd99d-105">Kestrel은 플랫폼 간 비동기 I/O 라이브러리인 [libuv](https://github.com/libuv/libuv)를 기반으로 하는 [ASP.NET Core용 플랫폼 간 웹 서버](index.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-105">Kestrel is a cross-platform [web server for ASP.NET Core](index.md) based on [libuv](https://github.com/libuv/libuv), a cross-platform asynchronous I/O library.</span></span> <span data-ttu-id="dd99d-106">Kestrel은 기본적으로 ASP.NET Core 프로젝트 템플릿에 포함된 웹 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-106">Kestrel is the web server that's included by default in ASP.NET Core project templates.</span></span> 

<span data-ttu-id="dd99d-107">Kestrel은 다음과 같은 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-107">Kestrel supports the following features:</span></span>

  * <span data-ttu-id="dd99d-108">HTTPS</span><span class="sxs-lookup"><span data-stu-id="dd99d-108">HTTPS</span></span>
  * <span data-ttu-id="dd99d-109">[Websocket](https://github.com/aspnet/websockets)을 활성화하는 데 사용되는 불투명 업그레이드</span><span class="sxs-lookup"><span data-stu-id="dd99d-109">Opaque upgrade used to enable [WebSockets](https://github.com/aspnet/websockets)</span></span>
  * <span data-ttu-id="dd99d-110">Nginx 뒤의 고성능을 위한 Unix 소켓</span><span class="sxs-lookup"><span data-stu-id="dd99d-110">Unix sockets for high performance behind Nginx</span></span> 

<span data-ttu-id="dd99d-111">Kestrel은 .NET Core에서 지원하는 모든 플랫폼 및 버전에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-111">Kestrel is supported on all platforms and versions that .NET Core supports.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="dd99d-112">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="dd99d-112">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="dd99d-113">[2.x용 샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/sample2)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="dd99d-113">[View or download sample code for 2.x](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/sample2) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="dd99d-114">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="dd99d-114">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="dd99d-115">[1.x용 샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/sample1)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="dd99d-115">[View or download sample code for 1.x](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/sample1) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

---

## <a name="when-to-use-kestrel-with-a-reverse-proxy"></a><span data-ttu-id="dd99d-116">Kestrel을 역방향 프록시와 함께 사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="dd99d-116">When to use Kestrel with a reverse proxy</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="dd99d-117">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="dd99d-117">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="dd99d-118">Kestrel을 단독으로 사용하거나 IIS, Nginx 또는 Apache 같은 *역방향 프록시 서버*와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-118">You can use Kestrel by itself or with a *reverse proxy server*, such as IIS, Nginx, or Apache.</span></span> <span data-ttu-id="dd99d-119">역방향 프록시 서버는 인터넷에서 HTTP 요청을 수신하고 몇몇 사전 처리 후에 Kestrel에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-119">A reverse proxy server receives HTTP requests from the Internet and forwards them to Kestrel after some preliminary handling.</span></span>

![Kestrel은 역방향 프록시 서버 없이 직접 인터넷과 통신합니다.](kestrel/_static/kestrel-to-internet2.png)

![Kestrel은 IIS, Nginx 또는 Apache 같은 역방향 프록시 서버를 통해 간접적으로 인터넷과 통신합니다.](kestrel/_static/kestrel-to-internet.png)

<span data-ttu-id="dd99d-122">Kestrel이 내부 네트워크에만 노출되는 경우 역방향 프록시 서버를 사용하거나 사용하지 않는 구성을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-122">Either configuration &mdash; with or without a reverse proxy server &mdash; can also be used if Kestrel is exposed only to an internal network.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="dd99d-123">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="dd99d-123">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="dd99d-124">응용 프로그램이 내부 네트워크의 요청만 허용할 경우 Kestrel을 단독으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-124">If your application accepts requests only from an internal network, you can use Kestrel by itself.</span></span>

![Kestrel은 내부 네트워크와 직접 통신합니다.](kestrel/_static/kestrel-to-internal.png)

<span data-ttu-id="dd99d-126">응용 프로그램을 인터넷에 노출할 경우 IIS, Nginx 또는 Apache를 *역방향 프록시 서버*로 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-126">If you expose your application to the Internet, you must use IIS, Nginx, or Apache as a *reverse proxy server*.</span></span> <span data-ttu-id="dd99d-127">역방향 프록시 서버는 인터넷에서 HTTP 요청을 수신하고 몇몇 사전 처리 후에 Kestrel에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-127">A reverse proxy server receives HTTP requests from the Internet and forwards them to Kestrel after some preliminary handling.</span></span>

![Kestrel은 IIS, Nginx 또는 Apache 같은 역방향 프록시 서버를 통해 간접적으로 인터넷과 통신합니다.](kestrel/_static/kestrel-to-internet.png)

<span data-ttu-id="dd99d-129">역방향 프록시는 보안 이유로 인터넷에서 트래픽에 노출되는 에지 배포에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-129">A reverse proxy is required for edge deployments (exposed to traffic from the Internet) for security reasons.</span></span> <span data-ttu-id="dd99d-130">Kestrel 1.x 버전에는 공격에 대한 전체 방어 기능이 포함되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-130">The 1.x versions of Kestrel don't have a full complement of defenses against attacks.</span></span> <span data-ttu-id="dd99d-131">이 방어 기능에는 적절한 시간 제한, 크기 제한, 동시 연결 제한이 포함되지만 이것으로 제한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-131">This includes but isn't limited to appropriate timeouts, size limits, and concurrent connection limits.</span></span>

---

<span data-ttu-id="dd99d-132">역방향 프록시를 필요로 하는 시나리오는 동일한 IP 및 단일 서버에서 실행되는 포트를 공유하는 여러 응용 프로그램이 있는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-132">A scenario that requires a reverse proxy is when you have multiple applications that share the same IP and port running on a single server.</span></span> <span data-ttu-id="dd99d-133">Kestrel은 여러 프로세스 간에 동일한 IP 및 포트 공유를 지원하지 않으므로 Kestrel과 직접 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-133">That doesn't work with Kestrel directly because Kestrel doesn't support sharing the same IP and port between multiple processes.</span></span> <span data-ttu-id="dd99d-134">포트에서 수신 대기하도록 Kestrel을 구성할 때 호스트 헤더에 관계 없이 해당 포트에 대한 모든 트래픽을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-134">When you configure Kestrel to listen on a port, it handles all traffic for that port regardless of host header.</span></span> <span data-ttu-id="dd99d-135">포트를 공유할 수 있는 역방향 프록시는 고유 IP 및 포트에서 Kestrel에 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-135">A reverse proxy that can share ports must then forward to Kestrel on a unique IP and port.</span></span>

<span data-ttu-id="dd99d-136">역방향 프록시 서버가 필요하지 않은 경우에도 하나를 사용하는 것은 다른 이유로 적합한 선택일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-136">Even if a reverse proxy server isn't required, using one might be a good choice for other reasons:</span></span>

* <span data-ttu-id="dd99d-137">공개된 노출 영역을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-137">It can limit your exposed surface area.</span></span>
* <span data-ttu-id="dd99d-138">구성 및 방어의 선택적 추가 계층을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-138">It provides an optional additional layer of configuration and defense.</span></span>
* <span data-ttu-id="dd99d-139">기존 인프라와 잘 통합될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-139">It might integrate better with existing infrastructure.</span></span>
* <span data-ttu-id="dd99d-140">부하 분산 및 SSL 설정을 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-140">It simplifies load balancing and SSL set-up.</span></span> <span data-ttu-id="dd99d-141">역방향 프록시 서버에 SSL 인증서가 필요한 경우에만 해당 서버는 일반 HTTP를 사용하여 내부 네트워크의 응용 프로그램 서버와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-141">Only your reverse proxy server requires an SSL certificate, and that server can communicate with your application servers on the internal network using plain HTTP.</span></span>

## <a name="how-to-use-kestrel-in-aspnet-core-apps"></a><span data-ttu-id="dd99d-142">ASP.NET Core 앱에서 Kestrel을 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="dd99d-142">How to use Kestrel in ASP.NET Core apps</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="dd99d-143">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="dd99d-143">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="dd99d-144">[Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) 패키지는 [Microsoft.AspNetCore.All 메타패키지](xref:fundamentals/metapackage)에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-144">The [Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) package is included in the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage).</span></span>

<span data-ttu-id="dd99d-145">ASP.NET Core 프로젝트 템플릿은 기본적으로 Kestrel을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-145">ASP.NET Core project templates use Kestrel by default.</span></span> <span data-ttu-id="dd99d-146">*Program.cs*에서 템플릿 코드는 [UseKestrel](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions#Microsoft_AspNetCore_Hosting_WebHostBuilderKestrelExtensions_UseKestrel_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) 숨은 기능을 호출하는 `CreateDefaultBuilder`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-146">In *Program.cs*, the template code calls `CreateDefaultBuilder`, which calls [UseKestrel](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions#Microsoft_AspNetCore_Hosting_WebHostBuilderKestrelExtensions_UseKestrel_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) behind the scenes.</span></span>

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_DefaultBuilder&highlight=7)]

<span data-ttu-id="dd99d-147">Kestrel 옵션을 구성해야 하는 경우 다음 예제와 같이 *Program.cs*에서 `UseKestrel`을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-147">If you need to configure Kestrel options, call `UseKestrel` in *Program.cs* as shown in the following example:</span></span>

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_DefaultBuilder&highlight=9-16)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="dd99d-148">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="dd99d-148">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="dd99d-149">[Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) NuGet 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-149">Install the [Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) NuGet package.</span></span>

<span data-ttu-id="dd99d-150">다음 섹션과 같이 필요한 [Kestrel 옵션](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.server.kestrel.kestrelserveroptions)을 지정하여 `Main` 메서드에서 `WebHostBuilder`의 [UseKestrel](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions#Microsoft_AspNetCore_Hosting_WebHostBuilderKestrelExtensions_UseKestrel_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) 확장 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-150">Call the [UseKestrel](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions#Microsoft_AspNetCore_Hosting_WebHostBuilderKestrelExtensions_UseKestrel_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) extension method on `WebHostBuilder` in your `Main` method, specifying any [Kestrel options](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.server.kestrel.kestrelserveroptions) that you need, as shown in the next section.</span></span>

[!code-csharp[](kestrel/sample1/Program.cs?name=snippet_Main&highlight=13-19)]

---

### <a name="kestrel-options"></a><span data-ttu-id="dd99d-151">Kestrel 옵션</span><span class="sxs-lookup"><span data-stu-id="dd99d-151">Kestrel options</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="dd99d-152">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="dd99d-152">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="dd99d-153">Kestrel 웹 서버에는 인터넷 연결 배포에 특히 유용한 제약 조건 구성 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-153">The Kestrel web server has constraint configuration options that are especially useful in Internet-facing deployments.</span></span> <span data-ttu-id="dd99d-154">다음은 설정할 수 있는 몇 가지 제한입니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-154">Here are some of the limits you can set:</span></span>

- <span data-ttu-id="dd99d-155">최대 클라이언트 연결</span><span class="sxs-lookup"><span data-stu-id="dd99d-155">Maximum client connections</span></span>
- <span data-ttu-id="dd99d-156">최대 요청 본문 크기</span><span class="sxs-lookup"><span data-stu-id="dd99d-156">Maximum request body size</span></span>
- <span data-ttu-id="dd99d-157">최소 요청 본문 데이터 속도</span><span class="sxs-lookup"><span data-stu-id="dd99d-157">Minimum request body data rate</span></span>

<span data-ttu-id="dd99d-158">[KestrelServerOptions](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/KestrelServerOptions.cs) 클래스의 `Limits` 속성에서 이러한 제약 조건 및 그 외 항목을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-158">You set these constraints and others in the `Limits` property of the [KestrelServerOptions](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/KestrelServerOptions.cs) class.</span></span> <span data-ttu-id="dd99d-159">`Limits` 속성은 [KestrelServerLimits](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/KestrelServerLimits.cs) 클래스의 인스턴스를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-159">The `Limits` property holds an instance of the [KestrelServerLimits](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/KestrelServerLimits.cs) class.</span></span> 

<span data-ttu-id="dd99d-160">**최대 클라이언트 연결**</span><span class="sxs-lookup"><span data-stu-id="dd99d-160">**Maximum client connections**</span></span>

<span data-ttu-id="dd99d-161">다음 코드를 사용하여 전체 응용 프로그램에 대한 동시 개방 TCP 연결의 최대 수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-161">The maximum number of concurrent open TCP connections can be set for the entire application with the following code:</span></span>

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_Limits&highlight=3-4)]

<span data-ttu-id="dd99d-162">HTTP 또는 HTTPS에서 다른 프로토콜(예: WebSocket 요청에서)로 업그레이드된 연결에 대한 별도 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-162">There's a separate limit for connections that have been upgraded from HTTP or HTTPS to another protocol (for example, on a WebSockets request).</span></span> <span data-ttu-id="dd99d-163">연결이 업그레이드된 후 `MaxConcurrentConnections` 제한에 대해 계산되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-163">After a connection is upgraded, it isn't counted against the `MaxConcurrentConnections` limit.</span></span> 

<span data-ttu-id="dd99d-164">연결의 최대 수는 기본적으로 무제한(null)입니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-164">The maximum number of connections is unlimited (null) by default.</span></span>

<span data-ttu-id="dd99d-165">**최대 요청 본문 크기**</span><span class="sxs-lookup"><span data-stu-id="dd99d-165">**Maximum request body size**</span></span>

<span data-ttu-id="dd99d-166">기본 최대 요청 본문 크기는 약 28.6MB인 30,000,000바이트입니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-166">The default maximum request body size is 30,000,000 bytes, which is approximately 28.6MB.</span></span> 

<span data-ttu-id="dd99d-167">ASP.NET Core MVC 앱에서 한도를 재정의할 때는 작업 메서드에서 [RequestSizeLimit](https://github.com/aspnet/Mvc/blob/rel/2.0.0/src/Microsoft.AspNetCore.Mvc.Core/RequestSizeLimitAttribute.cs) 특성을 사용하는 방법이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-167">The recommended way to override the limit in an ASP.NET Core MVC app is to use the [RequestSizeLimit](https://github.com/aspnet/Mvc/blob/rel/2.0.0/src/Microsoft.AspNetCore.Mvc.Core/RequestSizeLimitAttribute.cs) attribute on an action method:</span></span>

```csharp
[RequestSizeLimit(100000000)]
public IActionResult MyActionMethod()
```

<span data-ttu-id="dd99d-168">다음 예제는 전체 응용 프로그램, 모든 요청에 대한 제약 조건을 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-168">Here's an example that shows how to configure the constraint for the entire application, every request:</span></span>

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_Limits&highlight=5)]

<span data-ttu-id="dd99d-169">미들웨어에서 특정 요청에 대한 설정을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-169">You can override the setting on a specific request in middleware:</span></span>

[!code-csharp[](kestrel/sample2/Startup.cs?name=snippet_Limits&highlight=3-4)]
 
<span data-ttu-id="dd99d-170">응용 프로그램에서 요청을 읽기 시작한 후 요청에 대한 제한을 구성하려고 하면 예외가 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-170">An exception is thrown if you try to configure the limit on a request after the application has started reading the request.</span></span> <span data-ttu-id="dd99d-171">`MaxRequestBodySize` 속성이 제한을 구성하기에 너무 늦은, 읽기 전용 상태인지를 알려주는 `IsReadOnly` 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-171">There's an `IsReadOnly` property that tells you if the `MaxRequestBodySize` property is in read-only state, meaning it's too late to configure the limit.</span></span>

<span data-ttu-id="dd99d-172">**최소 요청 본문 데이터 속도**</span><span class="sxs-lookup"><span data-stu-id="dd99d-172">**Minimum request body data rate**</span></span>

<span data-ttu-id="dd99d-173">Kestrel은 데이터가 지정된 속도(바이트/초)로 들어오는지 1초마다 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-173">Kestrel checks every second if data is coming in at the specified rate in bytes/second.</span></span> <span data-ttu-id="dd99d-174">속도가 최소 아래로 떨어지면 연결이 시간 초과됩니다. 유예 기간은 Kestrel에서 해당 전송 속도를 최소로 높이기 위해 클라이언트에 제공하는 총 시간입니다. 이 시간 동안 속도는 확인되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-174">If the rate drops below the minimum, the connection is timed out. The grace period is the amount of time that Kestrel gives the client to increase its send rate up to the minimum; the rate isn't checked during that time.</span></span> <span data-ttu-id="dd99d-175">유예 기간은 TCP 느린 시작으로 인해 느린 속도로 처음에 데이터를 보내는 연결 중단을 방지하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-175">The grace period helps avoid dropping connections that are initially sending data at a slow rate due to TCP slow-start.</span></span>

<span data-ttu-id="dd99d-176">기본 최소 속도는 5초의 유예 기간으로 240바이트/초입니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-176">The default minimum rate is 240 bytes/second, with a 5 second grace period.</span></span>

<span data-ttu-id="dd99d-177">최소 속도는 응답에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-177">A minimum rate also applies to the response.</span></span> <span data-ttu-id="dd99d-178">요청 제한 및 응답 제한을 설정하는 코드는 속성 및 인터페이스 이름에 `RequestBody` 또는 `Response`를 갖는 것을 제외하고 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-178">The code to set the request limit and the response limit is the same except for having `RequestBody` or `Response` in the property and interface names.</span></span> 

<span data-ttu-id="dd99d-179">*Program.cs*에서 최소 데이터 속도를 구성하는 방법을 보여 주는 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-179">Here's an example that shows how to configure the minimum data rates in *Program.cs*:</span></span>

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_Limits&highlight=6-9)]

<span data-ttu-id="dd99d-180">미들웨어에서 요청별 속도를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-180">You can configure the rates per request in middleware:</span></span>

[!code-csharp[](kestrel/sample2/Startup.cs?name=snippet_Limits&highlight=5-8)]

<span data-ttu-id="dd99d-181">다른 Kestrel 옵션에 대한 내용은 다음 클래스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd99d-181">For information about other Kestrel options, see the following classes:</span></span>

* [<span data-ttu-id="dd99d-182">KestrelServerOptions</span><span class="sxs-lookup"><span data-stu-id="dd99d-182">KestrelServerOptions</span></span>](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/KestrelServerOptions.cs)
* [<span data-ttu-id="dd99d-183">KestrelServerLimits</span><span class="sxs-lookup"><span data-stu-id="dd99d-183">KestrelServerLimits</span></span>](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/KestrelServerLimits.cs)
* [<span data-ttu-id="dd99d-184">ListenOptions</span><span class="sxs-lookup"><span data-stu-id="dd99d-184">ListenOptions</span></span>](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/ListenOptions.cs)

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="dd99d-185">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="dd99d-185">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="dd99d-186">Kestrel 옵션에 대한 정보는 [KestrelServerOptions 클래스](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.server.kestrel.kestrelserveroptions)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd99d-186">For information about Kestrel options, see [KestrelServerOptions class](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.server.kestrel.kestrelserveroptions).</span></span>

---

### <a name="endpoint-configuration"></a><span data-ttu-id="dd99d-187">엔드포인트 구성</span><span class="sxs-lookup"><span data-stu-id="dd99d-187">Endpoint configuration</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="dd99d-188">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="dd99d-188">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="dd99d-189">기본적으로 ASP.NET Core는 `http://localhost:5000`으로 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-189">By default ASP.NET Core binds to `http://localhost:5000`.</span></span> <span data-ttu-id="dd99d-190">`KestrelServerOptions`의 `Listen` 또는 `ListenUnixSocket` 메서드를 호출하여 수신 대기하도록 Kestrel에 대한 URL 접두사 및 포트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-190">You configure URL prefixes and ports for Kestrel to listen on by calling `Listen` or `ListenUnixSocket` methods on `KestrelServerOptions`.</span></span> <span data-ttu-id="dd99d-191">(`UseUrls`, `urls` 명령줄 인수 및 ASPNETCORE_URLS 환경 변수도 작동하지만 [이 문서의 뒷부분](#useurls-limitations)에 명시된 제한 사항이 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="dd99d-191">(`UseUrls`, the `urls` command-line argument, and the ASPNETCORE_URLS environment variable also work but have the limitations noted [later in this article](#useurls-limitations).)</span></span>

<span data-ttu-id="dd99d-192">**TCP 소켓에 바인딩**</span><span class="sxs-lookup"><span data-stu-id="dd99d-192">**Bind to a TCP socket**</span></span>

<span data-ttu-id="dd99d-193">`Listen` 메서드는 TCP 소켓에 바인딩하고 옵션 람다를 통해 SSL 인증서를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-193">The `Listen` method binds to a TCP socket, and an options lambda lets you configure an SSL certificate:</span></span>

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_DefaultBuilder&highlight=9-16)]

<span data-ttu-id="dd99d-194">[ListenOptions](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/ListenOptions.cs)를 사용하여 이 예에서 특정 엔드포인트에 대한 SSL을 구성하는 방법을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-194">Notice how this example configures SSL for a particular endpoint by using [ListenOptions](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/ListenOptions.cs).</span></span> <span data-ttu-id="dd99d-195">동일한 API를 사용하여 특정 엔드포인트에 대한 다른 Kestrel 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-195">You can use the same API to configure other Kestrel settings for particular endpoints.</span></span>

[!INCLUDE[How to make an SSL cert](../../includes/make-ssl-cert.md)]

<span data-ttu-id="dd99d-196">**Unix 소켓에 바인딩**</span><span class="sxs-lookup"><span data-stu-id="dd99d-196">**Bind to a Unix socket**</span></span>

<span data-ttu-id="dd99d-197">이 예제에 나와 있는 것처럼 Nginx를 사용하여 향상된 성능을 위해 Unix 소켓을 수신 대기할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-197">You can listen on a Unix socket for improved performance with Nginx, as shown in this example:</span></span>

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_UnixSocket)]

<span data-ttu-id="dd99d-198">**포트 0**</span><span class="sxs-lookup"><span data-stu-id="dd99d-198">**Port 0**</span></span>

<span data-ttu-id="dd99d-199">포트 번호 0을 지정하는 경우 Kestrel은 동적으로 사용 가능한 포트에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-199">If you specify port number 0, Kestrel dynamically binds to an available port.</span></span> <span data-ttu-id="dd99d-200">다음 예제에서는 Kestrel이 실제로 런타임에 바인딩한 포트를 확인하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-200">The following example shows how to determine which port Kestrel actually bound to at runtime:</span></span>

[!code-csharp[](kestrel/sample2/Startup.cs?name=snippet_Configure&highlight=3,13,16-17)]

<a id="useurls-limitations"></a>

<span data-ttu-id="dd99d-201">**UseUrls 제한 사항**</span><span class="sxs-lookup"><span data-stu-id="dd99d-201">**UseUrls limitations**</span></span>

<span data-ttu-id="dd99d-202">`UseUrls` 메서드를 호출하거나 `urls` 명령줄 인수 또는 ASPNETCORE_URLS 환경 변수를 사용하여 엔드포인트를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-202">You can configure endpoints by calling the `UseUrls` method or using the `urls` command-line argument or the ASPNETCORE_URLS environment variable.</span></span> <span data-ttu-id="dd99d-203">이러한 메서드는 코드를 Kestrel이 아닌 서버와 작동하도록 하려는 경우 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-203">These methods are useful if you want your code to work with servers other than Kestrel.</span></span> <span data-ttu-id="dd99d-204">그러나 이러한 제한 사항을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-204">However, be aware of these limitations:</span></span>

* <span data-ttu-id="dd99d-205">이러한 메서드로 SSL을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-205">You can't use SSL with these methods.</span></span>
* <span data-ttu-id="dd99d-206">`Listen` 메서드 및 `UseUrls` 모두를 사용하는 경우 `Listen` 엔드포인트는 `UseUrls` 엔드포인트를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-206">If you use both the `Listen` method and `UseUrls`, the `Listen` endpoints override the `UseUrls` endpoints.</span></span>

<span data-ttu-id="dd99d-207">**IIS에 대한 엔드포인트 구성**</span><span class="sxs-lookup"><span data-stu-id="dd99d-207">**Endpoint configuration for IIS**</span></span>

<span data-ttu-id="dd99d-208">IIS를 사용하는 경우 IIS에 대한 URL 바인딩은 `Listen` 또는 `UseUrls`를 호출하여 설정하는 모든 바인딩을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-208">If you use IIS, the URL bindings for IIS override any bindings that you set by calling either `Listen` or `UseUrls`.</span></span> <span data-ttu-id="dd99d-209">자세한 내용은 [ASP.NET Core 모듈 소개](aspnet-core-module.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd99d-209">For more information, see [Introduction to ASP.NET Core Module](aspnet-core-module.md).</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="dd99d-210">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="dd99d-210">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="dd99d-211">기본적으로 ASP.NET Core는 `http://localhost:5000`으로 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-211">By default ASP.NET Core binds to `http://localhost:5000`.</span></span> <span data-ttu-id="dd99d-212">`UseUrls` 확장 메서드, `urls` 명령줄 인수 또는 ASP.NET Core 구성 시스템을 사용하여 수신하도록 Kestrel에 대한 URL 접두사와 포트를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-212">You can configure URL prefixes and ports for Kestrel to listen on by using the `UseUrls` extension method, the `urls` command-line argument, or the ASP.NET Core configuration system.</span></span> <span data-ttu-id="dd99d-213">이러한 메서드에 대한 자세한 내용은 [호스팅](../../fundamentals/hosting.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd99d-213">For more information about these methods, see [Hosting](../../fundamentals/hosting.md).</span></span> <span data-ttu-id="dd99d-214">역방향 프록시로 IIS를 사용하는 경우 URL 바인딩이 작동하는 방법에 대한 자세한 내용은 [ASP.NET Core 모듈](aspnet-core-module.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd99d-214">For information about how URL binding works when you use IIS as a reverse proxy, see [ASP.NET Core Module](aspnet-core-module.md).</span></span> 

---

### <a name="url-prefixes"></a><span data-ttu-id="dd99d-215">URL 접두사</span><span class="sxs-lookup"><span data-stu-id="dd99d-215">URL prefixes</span></span>

<span data-ttu-id="dd99d-216">`UseUrls`를 호출하거나 `urls` 명령줄 인수 또는 ASPNETCORE_URLS 환경 변수를 사용하는 경우 URL 접두사는 다음 형식 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-216">If you call `UseUrls` or use the `urls` command-line argument or ASPNETCORE_URLS environment variable, the URL prefixes can be in any of the following formats.</span></span> 

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="dd99d-217">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="dd99d-217">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="dd99d-218">HTTP URL 접두사만 유효합니다. Kestrel은 `UseUrls`를 사용하여 URL 바인딩을 구성하는 경우 SSL을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-218">Only HTTP URL prefixes are valid; Kestrel doesn't support SSL when you configure URL bindings by using `UseUrls`.</span></span>

* <span data-ttu-id="dd99d-219">포트 번호가 있는 IPv4 주소</span><span class="sxs-lookup"><span data-stu-id="dd99d-219">IPv4 address with port number</span></span>

  ```
  http://65.55.39.10:80/
  ```

  <span data-ttu-id="dd99d-220">0.0.0.0은 모든 IPv4 주소에 바인딩하는 특별한 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-220">0.0.0.0 is a special case that binds to all IPv4 addresses.</span></span>


* <span data-ttu-id="dd99d-221">포트 번호가 있는 IPv6 주소</span><span class="sxs-lookup"><span data-stu-id="dd99d-221">IPv6 address with port number</span></span>

  ```
  http://[0:0:0:0:0:ffff:4137:270a]:80/ 
  ```

  <span data-ttu-id="dd99d-222">[:]는 IPv4 0.0.0.0에 해당하는 IPv6입니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-222">[::] is the IPv6 equivalent of IPv4 0.0.0.0.</span></span>


* <span data-ttu-id="dd99d-223">포트 번호가 있는 호스트 이름</span><span class="sxs-lookup"><span data-stu-id="dd99d-223">Host name with port number</span></span>

  ```
  http://contoso.com:80/
  http://*:80/
  ```

  <span data-ttu-id="dd99d-224">호스트 이름, \* 및 +는 특별하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-224">Host names, \*, and +, are not special.</span></span> <span data-ttu-id="dd99d-225">인식되는 IP 주소 또는 "localhost"가 아닌 모든 항목은 모든 IPv4 및 IPv6 IP에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-225">Anything that's not a recognized IP address or "localhost" will bind to all IPv4 and IPv6 IPs.</span></span> <span data-ttu-id="dd99d-226">서로 다른 호스트 이름을 같은 포트에서 서로 다른 ASP.NET Core 응용 프로그램에 바인딩해야 하는 경우 [HTTP.sys](httpsys.md) 또는 IIS, Nginx 또는 Apache와 같은 역방향 프록시 서버를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-226">If you need to bind different host names to different ASP.NET Core applications on the same port, use [HTTP.sys](httpsys.md) or a reverse proxy server such as IIS, Nginx, or Apache.</span></span>

* <span data-ttu-id="dd99d-227">포트 번호가 있는 "Localhost" 이름 또는 포트 번호가 있는 루프백 IP</span><span class="sxs-lookup"><span data-stu-id="dd99d-227">"Localhost" name with port number or loopback IP with port number</span></span>

  ```
  http://localhost:5000/
  http://127.0.0.1:5000/
  http://[::1]:5000/
  ```

  <span data-ttu-id="dd99d-228">`localhost`가 지정되면 Kestrel은 IPv4 및 IPv6 루프백 인터페이스 모두에 바인딩하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-228">When `localhost` is specified, Kestrel tries to bind to both IPv4 and IPv6 loopback interfaces.</span></span> <span data-ttu-id="dd99d-229">요청된 포트가 루프백 인터페이스 중 하나의 다른 서비스에서 사용 중인 경우 Kestrel은 시작에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-229">If the requested port is in use by another service on either loopback interface, Kestrel fails to start.</span></span> <span data-ttu-id="dd99d-230">루프백 인터페이스 중 하나를 다른 이유(일반적으로 IPv6이 지원되지 않으므로)로 사용할 수 없는 경우 Kestrel은 경고를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-230">If either loopback interface is unavailable for any other reason (most commonly because IPv6 isn't supported), Kestrel logs a warning.</span></span> 

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="dd99d-231">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="dd99d-231">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

* <span data-ttu-id="dd99d-232">포트 번호가 있는 IPv4 주소</span><span class="sxs-lookup"><span data-stu-id="dd99d-232">IPv4 address with port number</span></span>

  ```
  http://65.55.39.10:80/
  https://65.55.39.10:443/
  ```

  <span data-ttu-id="dd99d-233">0.0.0.0은 모든 IPv4 주소에 바인딩하는 특별한 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-233">0.0.0.0 is a special case that binds to all IPv4 addresses.</span></span>


* <span data-ttu-id="dd99d-234">포트 번호가 있는 IPv6 주소</span><span class="sxs-lookup"><span data-stu-id="dd99d-234">IPv6 address with port number</span></span>

  ```
  http://[0:0:0:0:0:ffff:4137:270a]:80/ 
  https://[0:0:0:0:0:ffff:4137:270a]:443/ 
  ```

  <span data-ttu-id="dd99d-235">[:]는 IPv4 0.0.0.0에 해당하는 IPv6입니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-235">[::] is the IPv6 equivalent of IPv4 0.0.0.0.</span></span>


* <span data-ttu-id="dd99d-236">포트 번호가 있는 호스트 이름</span><span class="sxs-lookup"><span data-stu-id="dd99d-236">Host name with port number</span></span>

  ```
  http://contoso.com:80/
  http://*:80/
  https://contoso.com:443/
  https://*:443/
  ```

  <span data-ttu-id="dd99d-237">호스트 이름, \* 및 +는 특별하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-237">Host names, \*, and + aren't special.</span></span> <span data-ttu-id="dd99d-238">인식되는 IP 주소 또는 "localhost"가 아닌 모든 항목은 모든 IPv4 및 IPv6 IP에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-238">Anything that isn't a recognized IP address or "localhost" binds to all IPv4 and IPv6 IPs.</span></span> <span data-ttu-id="dd99d-239">서로 다른 호스트 이름을 같은 포트에서 서로 다른 ASP.NET Core 응용 프로그램에 바인딩해야 하는 경우 [WebListener](weblistener.md) 또는 IIS, Nginx 또는 Apache와 같은 역방향 프록시 서버를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-239">If you need to bind different host names to different ASP.NET Core applications on the same port, use [WebListener](weblistener.md) or a reverse proxy server such as IIS, Nginx, or Apache.</span></span>

* <span data-ttu-id="dd99d-240">포트 번호가 있는 "Localhost" 이름 또는 포트 번호가 있는 루프백 IP</span><span class="sxs-lookup"><span data-stu-id="dd99d-240">"Localhost" name with port number or loopback IP with port number</span></span>

  ```
  http://localhost:5000/
  http://127.0.0.1:5000/
  http://[::1]:5000/
  ```

  <span data-ttu-id="dd99d-241">`localhost`가 지정되면 Kestrel은 IPv4 및 IPv6 루프백 인터페이스 모두에 바인딩하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-241">When `localhost` is specified, Kestrel tries to bind to both IPv4 and IPv6 loopback interfaces.</span></span> <span data-ttu-id="dd99d-242">요청된 포트가 루프백 인터페이스 중 하나의 다른 서비스에서 사용 중인 경우 Kestrel은 시작에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-242">If the requested port is in use by another service on either loopback interface, Kestrel fails to start.</span></span> <span data-ttu-id="dd99d-243">루프백 인터페이스 중 하나를 다른 이유(일반적으로 IPv6이 지원되지 않으므로)로 사용할 수 없는 경우 Kestrel은 경고를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-243">If either loopback interface is unavailable for any other reason (most commonly because IPv6 isn't supported), Kestrel logs a warning.</span></span> 

* <span data-ttu-id="dd99d-244">Unix 소켓</span><span class="sxs-lookup"><span data-stu-id="dd99d-244">Unix socket</span></span>

  ```
  http://unix:/run/dan-live.sock  
  ```

<span data-ttu-id="dd99d-245">**포트 0**</span><span class="sxs-lookup"><span data-stu-id="dd99d-245">**Port 0**</span></span>

<span data-ttu-id="dd99d-246">포트 번호 0을 지정하는 경우 Kestrel은 동적으로 사용 가능한 포트에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-246">If you specify port number 0, Kestrel dynamically binds to an available port.</span></span> <span data-ttu-id="dd99d-247">포트 0에 바인딩은 `localhost` 이름을 제외하고 모든 호스트 이름 또는 IP에 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-247">Binding to port 0 is allowed for any host name or IP except for `localhost` name.</span></span>

<span data-ttu-id="dd99d-248">다음 예제에서는 Kestrel이 실제로 런타임에 바인딩한 포트를 확인하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-248">The following example shows how to determine which port Kestrel actually bound to at runtime:</span></span>

[!code-csharp[](kestrel/sample1/Startup.cs?name=snippet_Configure)]

<span data-ttu-id="dd99d-249">**SSL에 대한 URL 접두사**</span><span class="sxs-lookup"><span data-stu-id="dd99d-249">**URL prefixes for SSL**</span></span>

<span data-ttu-id="dd99d-250">다음과 같이 `UseHttps` 확장 메서드를 호출하는 경우 `https:`로 URL 접두사를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-250">Be sure to include URL prefixes with `https:` if you call the `UseHttps` extension method, as shown below.</span></span>

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
> <span data-ttu-id="dd99d-251">HTTPS 및 HTTP는 동일한 포트에서 호스팅될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dd99d-251">HTTPS and HTTP cannot be hosted on the same port.</span></span>

[!INCLUDE[How to make an SSL cert](../../includes/make-ssl-cert.md)]

---
## <a name="next-steps"></a><span data-ttu-id="dd99d-252">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dd99d-252">Next steps</span></span>

<span data-ttu-id="dd99d-253">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dd99d-253">For more information, see the following resources:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="dd99d-254">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="dd99d-254">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

* [<span data-ttu-id="dd99d-255">2.x용 샘플 앱</span><span class="sxs-lookup"><span data-stu-id="dd99d-255">Sample app for 2.x</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/sample2)
* [<span data-ttu-id="dd99d-256">Kestrel 소스 코드</span><span class="sxs-lookup"><span data-stu-id="dd99d-256">Kestrel source code</span></span>](https://github.com/aspnet/KestrelHttpServer)

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="dd99d-257">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="dd99d-257">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

* [<span data-ttu-id="dd99d-258">1.x용 샘플 앱</span><span class="sxs-lookup"><span data-stu-id="dd99d-258">Sample app for 1.x</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/sample1)
* [<span data-ttu-id="dd99d-259">Kestrel 소스 코드</span><span class="sxs-lookup"><span data-stu-id="dd99d-259">Kestrel source code</span></span>](https://github.com/aspnet/KestrelHttpServer)

---
