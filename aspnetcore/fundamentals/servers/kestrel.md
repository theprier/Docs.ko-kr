---
title: "ASP.NET Core 웹 서버 구현이 kestrel"
author: tdykstra
description: "ASP.NET Core libuv 기반 Kestrel, 플랫폼 간 웹 서버를 소개 합니다."
ms.author: tdykstra
manager: wpickett
ms.date: 08/02/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/servers/kestrel
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3e2b28f15e47789ac89213e57396060ee356ee33
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
# <a name="introduction-to-kestrel-web-server-implementation-in-aspnet-core"></a><span data-ttu-id="1643f-103">ASP.NET Core 웹 서버 구현이 Kestrel 소개</span><span class="sxs-lookup"><span data-stu-id="1643f-103">Introduction to Kestrel web server implementation in ASP.NET Core</span></span>

<span data-ttu-id="1643f-104">여 [Tom Dykstra](https://github.com/tdykstra), [Chris Ross](https://github.com/Tratcher), 및 [Stephen Halter](https://twitter.com/halter73)</span><span class="sxs-lookup"><span data-stu-id="1643f-104">By [Tom Dykstra](https://github.com/tdykstra), [Chris Ross](https://github.com/Tratcher), and [Stephen Halter](https://twitter.com/halter73)</span></span>

<span data-ttu-id="1643f-105">Kestrel는 플랫폼 간 [ASP.NET Core 웹 서버로](index.md) 기반 [libuv](https://github.com/libuv/libuv), 비동기 I/O 플랫폼 간 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-105">Kestrel is a cross-platform [web server for ASP.NET Core](index.md) based on [libuv](https://github.com/libuv/libuv), a cross-platform asynchronous I/O library.</span></span> <span data-ttu-id="1643f-106">Kestrel은 ASP.NET Core 프로젝트 템플릿에서 기본적으로 포함 되는 웹 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-106">Kestrel is the web server that's included by default in ASP.NET Core project templates.</span></span> 

<span data-ttu-id="1643f-107">Kestrel은 다음과 같은 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-107">Kestrel supports the following features:</span></span>

  * <span data-ttu-id="1643f-108">HTTPS</span><span class="sxs-lookup"><span data-stu-id="1643f-108">HTTPS</span></span>
  * <span data-ttu-id="1643f-109">사용 하도록 설정 하는 데 사용 되는 불투명 업그레이드 [Websocket](https://github.com/aspnet/websockets)</span><span class="sxs-lookup"><span data-stu-id="1643f-109">Opaque upgrade used to enable [WebSockets](https://github.com/aspnet/websockets)</span></span>
  * <span data-ttu-id="1643f-110">고성능 Nginx 뒤에 대 한 Unix 소켓</span><span class="sxs-lookup"><span data-stu-id="1643f-110">Unix sockets for high performance behind Nginx</span></span> 

<span data-ttu-id="1643f-111">Kestrel 모든 플랫폼 및 버전을 지 원하는.NET Core에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-111">Kestrel is supported on all platforms and versions that .NET Core supports.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="1643f-112">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="1643f-112">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="1643f-113">[보기 또는 2.x에 대 한 샘플 코드를 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/sample2) ([다운로드 하는 방법을](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="1643f-113">[View or download sample code for 2.x](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/sample2) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="1643f-114">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="1643f-114">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="1643f-115">[보기 또는 1.x에 대 한 샘플 코드를 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/sample1) ([다운로드 하는 방법을](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="1643f-115">[View or download sample code for 1.x](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/sample1) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

---

## <a name="when-to-use-kestrel-with-a-reverse-proxy"></a><span data-ttu-id="1643f-116">Kestrel 역방향 프록시를 사용 하는 경우</span><span class="sxs-lookup"><span data-stu-id="1643f-116">When to use Kestrel with a reverse proxy</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="1643f-117">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="1643f-117">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="1643f-118">Kestrel을 단독으로 사용하거나 IIS, Nginx 또는 Apache 같은 *역방향 프록시 서버*와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-118">You can use Kestrel by itself or with a *reverse proxy server*, such as IIS, Nginx, or Apache.</span></span> <span data-ttu-id="1643f-119">역방향 프록시 서버는 인터넷에서 HTTP 요청을 수신하고 몇몇 사전 처리 후에 Kestrel에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-119">A reverse proxy server receives HTTP requests from the Internet and forwards them to Kestrel after some preliminary handling.</span></span>

![Kestrel은 역방향 프록시 서버 없이 직접 인터넷과 통신합니다.](kestrel/_static/kestrel-to-internet2.png)

![Kestrel은 IIS, Nginx 또는 Apache 같은 역방향 프록시 서버를 통해 간접적으로 인터넷과 통신합니다.](kestrel/_static/kestrel-to-internet.png)

<span data-ttu-id="1643f-122">Kestrel이 내부 네트워크에만 노출되는 경우 역방향 프록시 서버를 사용하거나 사용하지 않는 구성을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-122">Either configuration &mdash; with or without a reverse proxy server &mdash; can also be used if Kestrel is exposed only to an internal network.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="1643f-123">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="1643f-123">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="1643f-124">응용 프로그램이 내부 네트워크의 요청만 허용할 경우 Kestrel을 단독으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-124">If your application accepts requests only from an internal network, you can use Kestrel by itself.</span></span>

![Kestrel은 내부 네트워크와 직접 통신합니다.](kestrel/_static/kestrel-to-internal.png)

<span data-ttu-id="1643f-126">응용 프로그램을 인터넷에 노출할 경우 IIS, Nginx 또는 Apache를 *역방향 프록시 서버*로 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-126">If you expose your application to the Internet, you must use IIS, Nginx, or Apache as a *reverse proxy server*.</span></span> <span data-ttu-id="1643f-127">역방향 프록시 서버는 인터넷에서 HTTP 요청을 수신하고 몇몇 사전 처리 후에 Kestrel에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-127">A reverse proxy server receives HTTP requests from the Internet and forwards them to Kestrel after some preliminary handling.</span></span>

![Kestrel은 IIS, Nginx 또는 Apache 같은 역방향 프록시 서버를 통해 간접적으로 인터넷과 통신합니다.](kestrel/_static/kestrel-to-internet.png)

<span data-ttu-id="1643f-129">역방향 프록시는 보안상의 이유로 가장자리 배포 (인터넷에서 트래픽에 노출)에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-129">A reverse proxy is required for edge deployments (exposed to traffic from the Internet) for security reasons.</span></span> <span data-ttu-id="1643f-130">Kestrel 1.x 버전에는 공격에 대한 전체 방어 기능이 포함되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-130">The 1.x versions of Kestrel don't have a full complement of defenses against attacks.</span></span> <span data-ttu-id="1643f-131">여기에 포함 되지만 적절 한 제한 시간, 크기 제한 및 동시 연결 제한으로 제한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-131">This includes but isn't limited to appropriate timeouts, size limits, and concurrent connection limits.</span></span>

---

<span data-ttu-id="1643f-132">역방향 프록시를 필요로 하는 시나리오에는 동일한 IP 및 단일 서버에서 실행 되는 포트를 공유 하는 여러 응용 프로그램이 있는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-132">A scenario that requires a reverse proxy is when you have multiple applications that share the same IP and port running on a single server.</span></span> <span data-ttu-id="1643f-133">하지 않는 함께 작동 Kestrel 직접 Kestrel 동일한 IP 및 여러 프로세스 간에 포트 공유를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-133">That doesn't work with Kestrel directly because Kestrel doesn't support sharing the same IP and port between multiple processes.</span></span> <span data-ttu-id="1643f-134">포트에서 수신 하도록 Kestrel를 구성할 때 호스트 헤더에 관계 없이 해당 포트에 대 한 모든 트래픽을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-134">When you configure Kestrel to listen on a port, it handles all traffic for that port regardless of host header.</span></span> <span data-ttu-id="1643f-135">포트를 공유할 수 있는 역방향 프록시 해야 후 Kestrel에 고유 IP 및 포트에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-135">A reverse proxy that can share ports must then forward to Kestrel on a unique IP and port.</span></span>

<span data-ttu-id="1643f-136">역방향 프록시 서버는 필요 하지 않습니다, 경우에 하나를 사용 하 여 다른 이유로 좋은 적합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-136">Even if a reverse proxy server isn't required, using one might be a good choice for other reasons:</span></span>

* <span data-ttu-id="1643f-137">프로그램 노출 된 노출 영역을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-137">It can limit your exposed surface area.</span></span>
* <span data-ttu-id="1643f-138">선택적 추가 계층을 구성 및 철저 한 방어를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-138">It provides an optional additional layer of configuration and defense.</span></span>
* <span data-ttu-id="1643f-139">기존 인프라와 잘 통합 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-139">It might integrate better with existing infrastructure.</span></span>
* <span data-ttu-id="1643f-140">부하 분산 및 SSL 설정을 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-140">It simplifies load balancing and SSL set-up.</span></span> <span data-ttu-id="1643f-141">역방향 프록시 서버에만 필요한 SSL 인증서를 하 고 해당 서버가 일반 HTTP를 사용 하 여 내부 네트워크에 응용 프로그램 서버와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-141">Only your reverse proxy server requires an SSL certificate, and that server can communicate with your application servers on the internal network using plain HTTP.</span></span>

## <a name="how-to-use-kestrel-in-aspnet-core-apps"></a><span data-ttu-id="1643f-142">Kestrel ASP.NET Core 응용 프로그램에서 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1643f-142">How to use Kestrel in ASP.NET Core apps</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="1643f-143">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="1643f-143">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="1643f-144">[Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) 패키지에 포함 되어는 [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage)합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-144">The [Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) package is included in the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage).</span></span>

<span data-ttu-id="1643f-145">ASP.NET Core 프로젝트 템플릿은 기본적으로 Kestrel를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-145">ASP.NET Core project templates use Kestrel by default.</span></span> <span data-ttu-id="1643f-146">*Program.cs*, 템플릿 코드 호출 `CreateDefaultBuilder`, 되는 호출 [UseKestrel](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions#Microsoft_AspNetCore_Hosting_WebHostBuilderKestrelExtensions_UseKestrel_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) 내부적입니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-146">In *Program.cs*, the template code calls `CreateDefaultBuilder`, which calls [UseKestrel](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions#Microsoft_AspNetCore_Hosting_WebHostBuilderKestrelExtensions_UseKestrel_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) behind the scenes.</span></span>

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_DefaultBuilder&highlight=7)]

<span data-ttu-id="1643f-147">Kestrel 옵션을 구성 해야 할 경우 호출 `UseKestrel` 에 *Program.cs* 다음 예제와 같이:</span><span class="sxs-lookup"><span data-stu-id="1643f-147">If you need to configure Kestrel options, call `UseKestrel` in *Program.cs* as shown in the following example:</span></span>

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_DefaultBuilder&highlight=9-16)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="1643f-148">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="1643f-148">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="1643f-149">설치는 [Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-149">Install the [Microsoft.AspNetCore.Server.Kestrel](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.Kestrel/) NuGet package.</span></span>

<span data-ttu-id="1643f-150">호출 된 [UseKestrel](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions#Microsoft_AspNetCore_Hosting_WebHostBuilderKestrelExtensions_UseKestrel_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) 확장 메서드를 `WebHostBuilder` 에 프로그램 `Main` 메서드를 지정 하 [Kestrel 옵션](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.server.kestrel.kestrelserveroptions) 다음 섹션에 나와 있는 것 처럼 필요한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-150">Call the [UseKestrel](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.hosting.webhostbuilderkestrelextensions#Microsoft_AspNetCore_Hosting_WebHostBuilderKestrelExtensions_UseKestrel_Microsoft_AspNetCore_Hosting_IWebHostBuilder_) extension method on `WebHostBuilder` in your `Main` method, specifying any [Kestrel options](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.server.kestrel.kestrelserveroptions) that you need, as shown in the next section.</span></span>

[!code-csharp[](kestrel/sample1/Program.cs?name=snippet_Main&highlight=13-19)]

---

### <a name="kestrel-options"></a><span data-ttu-id="1643f-151">Kestrel 옵션</span><span class="sxs-lookup"><span data-stu-id="1643f-151">Kestrel options</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="1643f-152">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="1643f-152">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="1643f-153">Kestrel 웹 서버에는 인터넷 연결 배포에 특히 유용한 제약 조건 구성 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-153">The Kestrel web server has constraint configuration options that are especially useful in Internet-facing deployments.</span></span> <span data-ttu-id="1643f-154">다음은 몇 제한을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-154">Here are some of the limits you can set:</span></span>

- <span data-ttu-id="1643f-155">최대 클라이언트 연결</span><span class="sxs-lookup"><span data-stu-id="1643f-155">Maximum client connections</span></span>
- <span data-ttu-id="1643f-156">최대 요청 본문 크기</span><span class="sxs-lookup"><span data-stu-id="1643f-156">Maximum request body size</span></span>
- <span data-ttu-id="1643f-157">최소 요청 본문 데이터 속도</span><span class="sxs-lookup"><span data-stu-id="1643f-157">Minimum request body data rate</span></span>

<span data-ttu-id="1643f-158">이러한 제약 조건 및의 다른 설정의 `Limits` 의 속성은 [KestrelServerOptions](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/KestrelServerOptions.cs) 클래스.</span><span class="sxs-lookup"><span data-stu-id="1643f-158">You set these constraints and others in the `Limits` property of the [KestrelServerOptions](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/KestrelServerOptions.cs) class.</span></span> <span data-ttu-id="1643f-159">`Limits` 의 인스턴스를 보유 하는 속성은 [KestrelServerLimits](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/KestrelServerLimits.cs) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-159">The `Limits` property holds an instance of the [KestrelServerLimits](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/KestrelServerLimits.cs) class.</span></span> 

<span data-ttu-id="1643f-160">**최대 클라이언트 연결**</span><span class="sxs-lookup"><span data-stu-id="1643f-160">**Maximum client connections**</span></span>

<span data-ttu-id="1643f-161">다음 코드를 사용 하는 전체 응용 프로그램에 대 한 열려 있는 동시 TCP 연결의 최대 수를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-161">The maximum number of concurrent open TCP connections can be set for the entire application with the following code:</span></span>

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_Limits&highlight=3-4)]

<span data-ttu-id="1643f-162">다른 프로토콜 (예를 들어 Websocket 요청)에서 HTTP 또는 HTTPS에서 업그레이드 된 연결에 대 한 별도 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-162">There's a separate limit for connections that have been upgraded from HTTP or HTTPS to another protocol (for example, on a WebSockets request).</span></span> <span data-ttu-id="1643f-163">에 따라 계산 되지 않습니다 연결이 업그레이드 되는 `MaxConcurrentConnections` 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-163">After a connection is upgraded, it isn't counted against the `MaxConcurrentConnections` limit.</span></span> 

<span data-ttu-id="1643f-164">연결의 최대 수는 기본적으로 무제한 (null).</span><span class="sxs-lookup"><span data-stu-id="1643f-164">The maximum number of connections is unlimited (null) by default.</span></span>

<span data-ttu-id="1643f-165">**최대 요청 본문 크기**</span><span class="sxs-lookup"><span data-stu-id="1643f-165">**Maximum request body size**</span></span>

<span data-ttu-id="1643f-166">기본 최대 요청 본문 크기는 약 28.6 m B 인 30,000,000 바이트입니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-166">The default maximum request body size is 30,000,000 bytes, which is approximately 28.6MB.</span></span> 

<span data-ttu-id="1643f-167">사용 하는 ASP.NET Core MVC 응용 프로그램에 대 한도 무시 하는 권장된 방법은 [RequestSizeLimit](https://github.com/aspnet/Mvc/blob/rel/2.0.0/src/Microsoft.AspNetCore.Mvc.Core/RequestSizeLimitAttribute.cs) 작업 메서드에 특성:</span><span class="sxs-lookup"><span data-stu-id="1643f-167">The recommended way to override the limit in an ASP.NET Core MVC app is to use the [RequestSizeLimit](https://github.com/aspnet/Mvc/blob/rel/2.0.0/src/Microsoft.AspNetCore.Mvc.Core/RequestSizeLimitAttribute.cs) attribute on an action method:</span></span>

```csharp
[RequestSizeLimit(100000000)]
public IActionResult MyActionMethod()
```

<span data-ttu-id="1643f-168">전체 응용 프로그램을 모든 요청에 대 한 제약 조건을 구성 하는 방법을 보여 주는 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-168">Here's an example that shows how to configure the constraint for the entire application, every request:</span></span>

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_Limits&highlight=5)]

<span data-ttu-id="1643f-169">미들웨어의 특정 요청에 설정을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-169">You can override the setting on a specific request in middleware:</span></span>

[!code-csharp[](kestrel/sample2/Startup.cs?name=snippet_Limits&highlight=3-4)]
 
<span data-ttu-id="1643f-170">응용 프로그램 요청 읽기 시작 된 후 요청에 대 한 제한을 구성 하려고 하면 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-170">An exception is thrown if you try to configure the limit on a request after the application has started reading the request.</span></span> <span data-ttu-id="1643f-171">`IsReadOnly` 를 알려 주는 속성 경우는 `MaxRequestBodySize` 제한을 구성 하려면에 너무 늦었습니다 의미 속성은 읽기 전용 상태에서입니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-171">There's an `IsReadOnly` property that tells you if the `MaxRequestBodySize` property is in read-only state, meaning it's too late to configure the limit.</span></span>

<span data-ttu-id="1643f-172">**최소 요청 본문 데이터 속도**</span><span class="sxs-lookup"><span data-stu-id="1643f-172">**Minimum request body data rate**</span></span>

<span data-ttu-id="1643f-173">Kestrel은 데이터 제공 되는 경우는 지정 된 비율에 바이트 수/초 1 초 마다 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-173">Kestrel checks every second if data is coming in at the specified rate in bytes/second.</span></span> <span data-ttu-id="1643f-174">속도가 최소 아래로 떨어지면, 연결 시간이 초과 됩니다. 유예 기간은 Kestrel 최소;까지 해당 전송 속도 높이기 위해 클라이언트에 제공 하는 시간 이 시간 동안 속도 확인 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-174">If the rate drops below the minimum, the connection is timed out. The grace period is the amount of time that Kestrel gives the client to increase its send rate up to the minimum; the rate isn't checked during that time.</span></span> <span data-ttu-id="1643f-175">유예 기간에 TCP 느린 시작으로 인해 느린 속도로 데이터 보내는 처음 연결을 삭제 하지 않도록 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-175">The grace period helps avoid dropping connections that are initially sending data at a slow rate due to TCP slow-start.</span></span>

<span data-ttu-id="1643f-176">기본 최소 속도 240 바이트/초가 고 5 초의 유예 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-176">The default minimum rate is 240 bytes/second, with a 5 second grace period.</span></span>

<span data-ttu-id="1643f-177">최소 속도 응답에도 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-177">A minimum rate also applies to the response.</span></span> <span data-ttu-id="1643f-178">요청 제한 및 응답 용량 한도 설정 하는 코드는 것을 제외 하 고 동일 `RequestBody` 또는 `Response` 속성 및 인터페이스 이름에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-178">The code to set the request limit and the response limit is the same except for having `RequestBody` or `Response` in the property and interface names.</span></span> 

<span data-ttu-id="1643f-179">여기에 최소 데이터 속도 구성 하는 방법을 보여 주는 예제는 *Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="1643f-179">Here's an example that shows how to configure the minimum data rates in *Program.cs*:</span></span>

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_Limits&highlight=6-9)]

<span data-ttu-id="1643f-180">미들웨어에서 요청에 따라 속도 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-180">You can configure the rates per request in middleware:</span></span>

[!code-csharp[](kestrel/sample2/Startup.cs?name=snippet_Limits&highlight=5-8)]

<span data-ttu-id="1643f-181">다른 Kestrel 옵션에 대 한 내용은 다음 클래스를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="1643f-181">For information about other Kestrel options, see the following classes:</span></span>

* [<span data-ttu-id="1643f-182">KestrelServerOptions</span><span class="sxs-lookup"><span data-stu-id="1643f-182">KestrelServerOptions</span></span>](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/KestrelServerOptions.cs)
* [<span data-ttu-id="1643f-183">KestrelServerLimits</span><span class="sxs-lookup"><span data-stu-id="1643f-183">KestrelServerLimits</span></span>](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/KestrelServerLimits.cs)
* [<span data-ttu-id="1643f-184">ListenOptions</span><span class="sxs-lookup"><span data-stu-id="1643f-184">ListenOptions</span></span>](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/ListenOptions.cs)

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="1643f-185">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="1643f-185">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="1643f-186">Kestrel 옵션에 대 한 정보를 참조 하십시오. [KestrelServerOptions 클래스](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.server.kestrel.kestrelserveroptions)합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-186">For information about Kestrel options, see [KestrelServerOptions class](https://docs.microsoft.com/aspnet/core/api/microsoft.aspnetcore.server.kestrel.kestrelserveroptions).</span></span>

---

### <a name="endpoint-configuration"></a><span data-ttu-id="1643f-187">끝점 구성</span><span class="sxs-lookup"><span data-stu-id="1643f-187">Endpoint configuration</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="1643f-188">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="1643f-188">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="1643f-189">기본적으로 ASP.NET Core을 바인딩합니다 `http://localhost:5000`합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-189">By default ASP.NET Core binds to `http://localhost:5000`.</span></span> <span data-ttu-id="1643f-190">URL 접두사 및 호출 하 여에서 수신 하도록 Kestrel에 대 한 포트 구성 `Listen` 또는 `ListenUnixSocket` 에 대 한 메서드 `KestrelServerOptions`합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-190">You configure URL prefixes and ports for Kestrel to listen on by calling `Listen` or `ListenUnixSocket` methods on `KestrelServerOptions`.</span></span> <span data-ttu-id="1643f-191">(`UseUrls`, `urls` 명령줄 인수 및 ASPNETCORE_URLS 환경 변수 에서도 작동 하지만 제한이 명시 된 [이 문서의 뒷부분에 나오는](#useurls-limitations).)</span><span class="sxs-lookup"><span data-stu-id="1643f-191">(`UseUrls`, the `urls` command-line argument, and the ASPNETCORE_URLS environment variable also work but have the limitations noted [later in this article](#useurls-limitations).)</span></span>

<span data-ttu-id="1643f-192">**TCP 소켓에 바인딩**</span><span class="sxs-lookup"><span data-stu-id="1643f-192">**Bind to a TCP socket**</span></span>

<span data-ttu-id="1643f-193">`Listen` 메서드는 TCP 소켓을 바인딩하고 옵션 람다는 SSL 인증서를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-193">The `Listen` method binds to a TCP socket, and an options lambda lets you configure an SSL certificate:</span></span>

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_DefaultBuilder&highlight=9-16)]

<span data-ttu-id="1643f-194">어떻게이 예에서는 SSL을 특정 끝점에 대 한 사용 하 여 구성 확인 [ListenOptions](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/ListenOptions.cs)합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-194">Notice how this example configures SSL for a particular endpoint by using [ListenOptions](https://github.com/aspnet/KestrelHttpServer/blob/rel/2.0.0/src/Microsoft.AspNetCore.Server.Kestrel.Core/ListenOptions.cs).</span></span> <span data-ttu-id="1643f-195">특정 끝점에 대 한 다른 Kestrel 설정을 구성 하는 동일한 API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-195">You can use the same API to configure other Kestrel settings for particular endpoints.</span></span>

[!INCLUDE[How to make an SSL cert](../../includes/make-ssl-cert.md)]

<span data-ttu-id="1643f-196">**Unix 소켓에 바인딩**</span><span class="sxs-lookup"><span data-stu-id="1643f-196">**Bind to a Unix socket**</span></span>

<span data-ttu-id="1643f-197">이 예제에 나와 있는 것 처럼에 향상 된 성능을 얻으려면 Nginx, Unix 소켓에서 수신할 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="1643f-197">You can listen on a Unix socket for improved performance with Nginx, as shown in this example:</span></span>

[!code-csharp[](kestrel/sample2/Program.cs?name=snippet_UnixSocket)]

<span data-ttu-id="1643f-198">**포트 0**</span><span class="sxs-lookup"><span data-stu-id="1643f-198">**Port 0**</span></span>

<span data-ttu-id="1643f-199">포트 번호 0을 지정 하면 Kestrel는 동적으로 사용 가능한 포트를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-199">If you specify port number 0, Kestrel dynamically binds to an available port.</span></span> <span data-ttu-id="1643f-200">다음 예제에서는 Kestrel 실제로 런타임에 바인딩할 포트를 확인 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-200">The following example shows how to determine which port Kestrel actually bound to at runtime:</span></span>

[!code-csharp[](kestrel/sample2/Startup.cs?name=snippet_Configure&highlight=3,13,16-17)]

<a id="useurls-limitations"></a>

<span data-ttu-id="1643f-201">**UseUrls 제한 사항**</span><span class="sxs-lookup"><span data-stu-id="1643f-201">**UseUrls limitations**</span></span>

<span data-ttu-id="1643f-202">호출 하 여 끝점을 구성할 수 있습니다는 `UseUrls` 메서드 또는 사용 하는 `urls` ASPNETCORE_URLS 환경 변수나 명령줄 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-202">You can configure endpoints by calling the `UseUrls` method or using the `urls` command-line argument or the ASPNETCORE_URLS environment variable.</span></span> <span data-ttu-id="1643f-203">이러한 메서드는 코드 Kestrel 아닌 서버와 작동 하도록 하려는 경우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-203">These methods are useful if you want your code to work with servers other than Kestrel.</span></span> <span data-ttu-id="1643f-204">그러나 이러한 제한을 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-204">However, be aware of these limitations:</span></span>

* <span data-ttu-id="1643f-205">이러한 방법으로 SSL을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-205">You can't use SSL with these methods.</span></span>
* <span data-ttu-id="1643f-206">둘 다 사용 하는 경우는 `Listen` 메서드 및 `UseUrls`, `Listen` 끝점 재정의 `UseUrls` 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-206">If you use both the `Listen` method and `UseUrls`, the `Listen` endpoints override the `UseUrls` endpoints.</span></span>

<span data-ttu-id="1643f-207">**IIS에 대 한 끝점 구성**</span><span class="sxs-lookup"><span data-stu-id="1643f-207">**Endpoint configuration for IIS**</span></span>

<span data-ttu-id="1643f-208">IIS를 사용 하는 경우 IIS에 대 한 URL 바인딩을 재정의 중 하나를 호출 하 여 설정할 수 있는 모든 바인딩에 `Listen` 또는 `UseUrls`합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-208">If you use IIS, the URL bindings for IIS override any bindings that you set by calling either `Listen` or `UseUrls`.</span></span> <span data-ttu-id="1643f-209">자세한 내용은 참조 [ASP.NET Core 모듈 소개](aspnet-core-module.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-209">For more information, see [Introduction to ASP.NET Core Module](aspnet-core-module.md).</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="1643f-210">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="1643f-210">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="1643f-211">기본적으로 ASP.NET Core을 바인딩합니다 `http://localhost:5000`합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-211">By default ASP.NET Core binds to `http://localhost:5000`.</span></span> <span data-ttu-id="1643f-212">URL 접두사 및에서 사용 하 여 수신 하도록 Kestrel에 대 한 포트를 구성할 수는 `UseUrls` 확장 메서드는 `urls` 명령줄 인수 또는 ASP.NET Core 구성 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-212">You can configure URL prefixes and ports for Kestrel to listen on by using the `UseUrls` extension method, the `urls` command-line argument, or the ASP.NET Core configuration system.</span></span> <span data-ttu-id="1643f-213">이러한 메서드에 대 한 자세한 내용은 참조 [호스팅](../../fundamentals/hosting.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-213">For more information about these methods, see [Hosting](../../fundamentals/hosting.md).</span></span> <span data-ttu-id="1643f-214">역방향 프록시로 IIS를 사용 하는 경우 URL 바인딩을 작동 하는 방법에 대 한 자세한 내용은 참조 하십시오. [ASP.NET Core 모듈](aspnet-core-module.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-214">For information about how URL binding works when you use IIS as a reverse proxy, see [ASP.NET Core Module](aspnet-core-module.md).</span></span> 

---

### <a name="url-prefixes"></a><span data-ttu-id="1643f-215">URL 접두사</span><span class="sxs-lookup"><span data-stu-id="1643f-215">URL prefixes</span></span>

<span data-ttu-id="1643f-216">호출 하는 경우 `UseUrls` 하거나 사용 하 여는 `urls` 명령줄 인수나 ASPNETCORE_URLS 환경 변수 URL 접두사는 다음 형식 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-216">If you call `UseUrls` or use the `urls` command-line argument or ASPNETCORE_URLS environment variable, the URL prefixes can be in any of the following formats.</span></span> 

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="1643f-217">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="1643f-217">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="1643f-218">HTTP URL 접두사만 사용할 수 있습니다. Kestrel URL 바인딩을 사용 하 여 구성 하는 경우 SSL을 지원 하지 않습니다 `UseUrls`합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-218">Only HTTP URL prefixes are valid; Kestrel doesn't support SSL when you configure URL bindings by using `UseUrls`.</span></span>

* <span data-ttu-id="1643f-219">IPv4 주소와 포트 번호</span><span class="sxs-lookup"><span data-stu-id="1643f-219">IPv4 address with port number</span></span>

  ```
  http://65.55.39.10:80/
  ```

  <span data-ttu-id="1643f-220">0.0.0.0은 특별 한 경우로 모든 IPv4 주소를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-220">0.0.0.0 is a special case that binds to all IPv4 addresses.</span></span>


* <span data-ttu-id="1643f-221">포트 번호가 있는 IPv6 주소</span><span class="sxs-lookup"><span data-stu-id="1643f-221">IPv6 address with port number</span></span>

  ```
  http://[0:0:0:0:0:ffff:4137:270a]:80/ 
  ```

  <span data-ttu-id="1643f-222">[:]는 i p v 4에 해당 하는 IPv6 0.0.0.0입니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-222">[::] is the IPv6 equivalent of IPv4 0.0.0.0.</span></span>


* <span data-ttu-id="1643f-223">호스트 이름과 포트 번호</span><span class="sxs-lookup"><span data-stu-id="1643f-223">Host name with port number</span></span>

  ```
  http://contoso.com:80/
  http://*:80/
  ```

  <span data-ttu-id="1643f-224">호스트 이름, \*, 고 +, 특별 한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-224">Host names, \*, and +, are not special.</span></span> <span data-ttu-id="1643f-225">IP 주소 또는 "localhost"를 인식 하지 않은 모든 항목은 모든 IPv4 및 IPv6 Ip에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-225">Anything that's not a recognized IP address or "localhost" will bind to all IPv4 and IPv6 IPs.</span></span> <span data-ttu-id="1643f-226">서로 다른 호스트 이름을 같은 포트에서 서로 다른 ASP.NET Core 응용 프로그램에 바인딩할 필요 사용 [HTTP.sys](httpsys.md) 또는 IIS, Nginx, 또는 Apache 같은 역방향 프록시 서버.</span><span class="sxs-lookup"><span data-stu-id="1643f-226">If you need to bind different host names to different ASP.NET Core applications on the same port, use [HTTP.sys](httpsys.md) or a reverse proxy server such as IIS, Nginx, or Apache.</span></span>

* <span data-ttu-id="1643f-227">포트 번호 또는 루프백 ip 포트 번호로 "Localhost" 이름</span><span class="sxs-lookup"><span data-stu-id="1643f-227">"Localhost" name with port number or loopback IP with port number</span></span>

  ```
  http://localhost:5000/
  http://127.0.0.1:5000/
  http://[::1]:5000/
  ```

  <span data-ttu-id="1643f-228">때 `localhost` 를 지정, Kestrel IPv4 및 IPv6 모두 루프백 인터페이스에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-228">When `localhost` is specified, Kestrel tries to bind to both IPv4 and IPv6 loopback interfaces.</span></span> <span data-ttu-id="1643f-229">요청 된 포트는 루프백 인터페이스 중 하나에 다른 서비스에서 사용 중인 경우 Kestrel 시작 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-229">If the requested port is in use by another service on either loopback interface, Kestrel fails to start.</span></span> <span data-ttu-id="1643f-230">루프백 인터페이스 중 하나 사용할 수 없으면 다른 이유로 대부분 IPv6 지원 되지 않으므로 일반적으로, Kestrel 경고를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-230">If either loopback interface is unavailable for any other reason (most commonly because IPv6 isn't supported), Kestrel logs a warning.</span></span> 

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="1643f-231">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="1643f-231">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

* <span data-ttu-id="1643f-232">IPv4 주소와 포트 번호</span><span class="sxs-lookup"><span data-stu-id="1643f-232">IPv4 address with port number</span></span>

  ```
  http://65.55.39.10:80/
  https://65.55.39.10:443/
  ```

  <span data-ttu-id="1643f-233">0.0.0.0은 특별 한 경우로 모든 IPv4 주소를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-233">0.0.0.0 is a special case that binds to all IPv4 addresses.</span></span>


* <span data-ttu-id="1643f-234">포트 번호가 있는 IPv6 주소</span><span class="sxs-lookup"><span data-stu-id="1643f-234">IPv6 address with port number</span></span>

  ```
  http://[0:0:0:0:0:ffff:4137:270a]:80/ 
  https://[0:0:0:0:0:ffff:4137:270a]:443/ 
  ```

  <span data-ttu-id="1643f-235">[:]는 i p v 4에 해당 하는 IPv6 0.0.0.0입니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-235">[::] is the IPv6 equivalent of IPv4 0.0.0.0.</span></span>


* <span data-ttu-id="1643f-236">호스트 이름과 포트 번호</span><span class="sxs-lookup"><span data-stu-id="1643f-236">Host name with port number</span></span>

  ```
  http://contoso.com:80/
  http://*:80/
  https://contoso.com:443/
  https://*:443/
  ```

  <span data-ttu-id="1643f-237">호스트 이름, \*, 및 + 특별 한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-237">Host names, \*, and + aren't special.</span></span> <span data-ttu-id="1643f-238">이외의 모든 IP 주소 또는 "localhost"를 인식 된 모든 IPv4 및 IPv6 Ip에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-238">Anything that isn't a recognized IP address or "localhost" binds to all IPv4 and IPv6 IPs.</span></span> <span data-ttu-id="1643f-239">서로 다른 호스트 이름을 같은 포트에서 서로 다른 ASP.NET Core 응용 프로그램에 바인딩할 필요 사용 [WebListener](weblistener.md) 또는 IIS, Nginx, 또는 Apache 같은 역방향 프록시 서버.</span><span class="sxs-lookup"><span data-stu-id="1643f-239">If you need to bind different host names to different ASP.NET Core applications on the same port, use [WebListener](weblistener.md) or a reverse proxy server such as IIS, Nginx, or Apache.</span></span>

* <span data-ttu-id="1643f-240">포트 번호 또는 루프백 ip 포트 번호로 "Localhost" 이름</span><span class="sxs-lookup"><span data-stu-id="1643f-240">"Localhost" name with port number or loopback IP with port number</span></span>

  ```
  http://localhost:5000/
  http://127.0.0.1:5000/
  http://[::1]:5000/
  ```

  <span data-ttu-id="1643f-241">때 `localhost` 를 지정, Kestrel IPv4 및 IPv6 모두 루프백 인터페이스에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-241">When `localhost` is specified, Kestrel tries to bind to both IPv4 and IPv6 loopback interfaces.</span></span> <span data-ttu-id="1643f-242">요청 된 포트는 루프백 인터페이스 중 하나에 다른 서비스에서 사용 중인 경우 Kestrel 시작 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-242">If the requested port is in use by another service on either loopback interface, Kestrel fails to start.</span></span> <span data-ttu-id="1643f-243">루프백 인터페이스 중 하나 사용할 수 없으면 다른 이유로 대부분 IPv6 지원 되지 않으므로 일반적으로, Kestrel 경고를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-243">If either loopback interface is unavailable for any other reason (most commonly because IPv6 isn't supported), Kestrel logs a warning.</span></span> 

* <span data-ttu-id="1643f-244">Unix 소켓</span><span class="sxs-lookup"><span data-stu-id="1643f-244">Unix socket</span></span>

  ```
  http://unix:/run/dan-live.sock  
  ```

<span data-ttu-id="1643f-245">**포트 0**</span><span class="sxs-lookup"><span data-stu-id="1643f-245">**Port 0**</span></span>

<span data-ttu-id="1643f-246">포트 번호 0을 지정 하면 Kestrel는 동적으로 사용 가능한 포트를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-246">If you specify port number 0, Kestrel dynamically binds to an available port.</span></span> <span data-ttu-id="1643f-247">호스트 이름 또는 IP를 제외 하 고 사용할 수는 0 포트에 바인딩 `localhost` 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-247">Binding to port 0 is allowed for any host name or IP except for `localhost` name.</span></span>

<span data-ttu-id="1643f-248">다음 예제에서는 Kestrel 실제로 런타임에 바인딩할 포트를 확인 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-248">The following example shows how to determine which port Kestrel actually bound to at runtime:</span></span>

[!code-csharp[](kestrel/sample1/Startup.cs?name=snippet_Configure)]

<span data-ttu-id="1643f-249">**SSL에 대 한 URL 접두사**</span><span class="sxs-lookup"><span data-stu-id="1643f-249">**URL prefixes for SSL**</span></span>

<span data-ttu-id="1643f-250">URL 접두사를 포함 해야 `https:` 호출 하는 경우는 `UseHttps` 확장 메서드를 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-250">Be sure to include URL prefixes with `https:` if you call the `UseHttps` extension method, as shown below.</span></span>

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
> <span data-ttu-id="1643f-251">HTTPS 및 HTTP 같은 포트에서 호스팅할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1643f-251">HTTPS and HTTP cannot be hosted on the same port.</span></span>

[!INCLUDE[How to make an SSL cert](../../includes/make-ssl-cert.md)]

---
## <a name="next-steps"></a><span data-ttu-id="1643f-252">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1643f-252">Next steps</span></span>

<span data-ttu-id="1643f-253">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1643f-253">For more information, see the following resources:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="1643f-254">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="1643f-254">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

* [<span data-ttu-id="1643f-255">2.x에 대 한 샘플 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="1643f-255">Sample app for 2.x</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/sample2)
* [<span data-ttu-id="1643f-256">Kestrel 소스 코드</span><span class="sxs-lookup"><span data-stu-id="1643f-256">Kestrel source code</span></span>](https://github.com/aspnet/KestrelHttpServer)

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="1643f-257">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="1643f-257">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

* [<span data-ttu-id="1643f-258">1.x 용 예제 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="1643f-258">Sample app for 1.x</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/servers/kestrel/sample1)
* [<span data-ttu-id="1643f-259">Kestrel 소스 코드</span><span class="sxs-lookup"><span data-stu-id="1643f-259">Kestrel source code</span></span>](https://github.com/aspnet/KestrelHttpServer)

---
