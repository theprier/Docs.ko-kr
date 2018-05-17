---
title: ASP.NET Core의 웹 서버 구현
author: rick-anderson
description: ASP.NET Core의 웹 서버 Kestrel 및 HTTP.sys를 검색합니다. 서버를 선택하는 방법 및 역방향 프록시 서버를 사용하는 시기에 대해 알아봅니다.
manager: wpickett
ms.author: tdykstra
ms.custom: mvc
ms.date: 03/13/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/servers/index
ms.openlocfilehash: 38af9d0206d66ac7fd2dc13a5a8245e8f66df41e
ms.sourcegitcommit: a19261eb82b948af6e4a1664fcfb8dabb16150e3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2018
---
# <a name="web-server-implementations-in-aspnet-core"></a><span data-ttu-id="ed9b3-104">ASP.NET Core의 웹 서버 구현</span><span class="sxs-lookup"><span data-stu-id="ed9b3-104">Web server implementations in ASP.NET Core</span></span>

<span data-ttu-id="ed9b3-105">작성자: [Tom Dykstra](https://github.com/tdykstra), [Steve Smith](https://ardalis.com/), [Stephen Halter](https://twitter.com/halter73) 및 [Chris Ross](https://github.com/Tratcher)</span><span class="sxs-lookup"><span data-stu-id="ed9b3-105">By [Tom Dykstra](https://github.com/tdykstra), [Steve Smith](https://ardalis.com/), [Stephen Halter](https://twitter.com/halter73), and [Chris Ross](https://github.com/Tratcher)</span></span>

<span data-ttu-id="ed9b3-106">ASP.NET Core 앱은 In-process HTTP 서버 구현을 사용하여 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-106">An ASP.NET Core app runs with an in-process HTTP server implementation.</span></span> <span data-ttu-id="ed9b3-107">서버 구현은 HTTP 요청을 수신하고 [HttpContext](/dotnet/api/system.web.httpcontext)를 구성하는 [요청 기능](xref:fundamentals/request-features) 집합으로 앱에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-107">The server implementation listens for HTTP requests and surfaces them to the app as sets of [request features](xref:fundamentals/request-features) composed into an [HttpContext](/dotnet/api/system.web.httpcontext).</span></span>

<span data-ttu-id="ed9b3-108">ASP.NET Core는 다음 두 가지 서버 구현을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-108">ASP.NET Core ships two server implementations:</span></span>

* <span data-ttu-id="ed9b3-109">[Kestrel](xref:fundamentals/servers/kestrel)은 ASP.NET Core용 기본 플랫폼 간 HTTP 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-109">[Kestrel](xref:fundamentals/servers/kestrel) is the default, cross-platform HTTP server for ASP.NET Core.</span></span>
* <span data-ttu-id="ed9b3-110">[HTTP.sys](xref:fundamentals/servers/httpsys)는 [Http.Sys 커널 드라이버 및 HTTP 서버 API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx)를 기반으로 하는 Windows 전용 HTTP 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-110">[HTTP.sys](xref:fundamentals/servers/httpsys) is a Windows-only HTTP server based on the [HTTP.sys kernel driver and HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span></span> <span data-ttu-id="ed9b3-111">ASP.NET Core 1.x에서는 HTTP.sys를 [WebListener](xref:fundamentals/servers/weblistener)라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-111">(HTTP.sys is called [WebListener](xref:fundamentals/servers/weblistener) in ASP.NET Core 1.x.)</span></span>

## <a name="kestrel"></a><span data-ttu-id="ed9b3-112">Kestrel</span><span class="sxs-lookup"><span data-stu-id="ed9b3-112">Kestrel</span></span>

<span data-ttu-id="ed9b3-113">Kestrel은 ASP.NET Core 프로젝트 템플릿에 포함된 기본 웹 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-113">Kestrel is the default web server included in ASP.NET Core project templates.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="ed9b3-114">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="ed9b3-114">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="ed9b3-115">Kestrel을 단독으로 사용하거나 IIS, Nginx 또는 Apache 같은 *역방향 프록시 서버*와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-115">Kestrel can be used by itself or with a *reverse proxy server*, such as IIS, Nginx, or Apache.</span></span> <span data-ttu-id="ed9b3-116">역방향 프록시 서버는 인터넷에서 HTTP 요청을 수신하고 몇몇 사전 처리 후에 Kestrel에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-116">A reverse proxy server receives HTTP requests from the Internet and forwards them to Kestrel after some preliminary handling.</span></span>

![Kestrel은 역방향 프록시 서버 없이 직접 인터넷과 통신합니다.](kestrel/_static/kestrel-to-internet2.png)

![Kestrel은 IIS, Nginx 또는 Apache 같은 역방향 프록시 서버를 통해 간접적으로 인터넷과 통신합니다.](kestrel/_static/kestrel-to-internet.png)

<span data-ttu-id="ed9b3-119">Kestrel이 내부 네트워크에만 노출되는 경우 &mdash;역방향 프록시 서버를 사용하거나 사용하지 않는&mdash; 구성을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-119">Either configuration &mdash; with or without a reverse proxy server &mdash; can also be used if Kestrel is only exposed to an internal network.</span></span>

<span data-ttu-id="ed9b3-120">자세한 내용은 [Kestrel를 역방향 프록시와 함께 사용할 경우](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-120">For information, see [When to use Kestrel with a reverse proxy](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy).</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="ed9b3-121">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="ed9b3-121">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="ed9b3-122">앱이 내부 네트워크의 요청만을 수락하는 경우 Kestrel을 단독으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-122">If the app only accepts requests from an internal network, Kestrel can be used by itself.</span></span>

![Kestrel은 내부 네트워크와 직접 통신합니다.](kestrel/_static/kestrel-to-internal.png)

<span data-ttu-id="ed9b3-124">앱을 인터넷에 노출할 경우 Kestrel에서는 IIS, Nginx 또는 Apache를 *역방향 프록시 서버*로 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-124">If the app is exposed to the Internet, Kestrel must use IIS, Nginx, or Apache as a *reverse proxy server*.</span></span> <span data-ttu-id="ed9b3-125">역방향 프록시 서버는 인터넷에서 HTTP 요청을 수신하고, 다음 다이어그램에서 보여준 대로 몇 가지 사전 처리를 수행한 후에 Kestrel에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-125">A reverse proxy server receives HTTP requests from the Internet and forwards them to Kestrel after some preliminary handling, as shown in the following diagram:</span></span>

![Kestrel은 IIS, Nginx 또는 Apache 같은 역방향 프록시 서버를 통해 간접적으로 인터넷과 통신합니다.](kestrel/_static/kestrel-to-internet.png)

<span data-ttu-id="ed9b3-127">인터넷에서 트래픽에 노출되는 에지 배포에 역방향 프록시를 사용하는 가장 중요한 이유는 보안입니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-127">The most important reason for using a reverse proxy for edge deployments (exposed to traffic from the Internet) is security.</span></span> <span data-ttu-id="ed9b3-128">1.x 버전의 Kestrel에는 인터넷의 공격으로부터 보호하기 위한 중요한 보안 기능이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-128">The 1.x versions of Kestrel don't have important security features to defend against attacks from the Internet.</span></span> <span data-ttu-id="ed9b3-129">여기에는 적절한 시간 제한, 요청 크기 제한, 동시 연결 제한을 비롯한 다양한 기능이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-129">This includes, but isn't limited to, appropriate timeouts, request size limits, and concurrent connection limits.</span></span>

<span data-ttu-id="ed9b3-130">자세한 내용은 [Kestrel를 역방향 프록시와 함께 사용할 경우](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-130">For information, see [When to use Kestrel with a reverse proxy](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy).</span></span>

---

<span data-ttu-id="ed9b3-131">Kestrel 또는 [사용자 지정 서버 구현](#custom-servers)이 없으면 IIS, Nginx 또는 Apache를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-131">IIS, Nginx, and Apache can't be used without Kestrel or a [custom server implementation](#custom-servers).</span></span> <span data-ttu-id="ed9b3-132">ASP.NET Core는 플랫폼 간에 일관되게 동작하도록 자체 프로세스로 실행되도록 고안되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-132">ASP.NET Core was designed to run in its own process so that it can behave consistently across platforms.</span></span> <span data-ttu-id="ed9b3-133">IIS, Nginx 및 Apache에서는 고유한 시작 프로시저 및 환경을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-133">IIS, Nginx, and Apache dictate their own startup procedure and environment.</span></span> <span data-ttu-id="ed9b3-134">직접 이러한 서버 기술을 사용하려면 ASP.NET Core를 각 서버의 요구 사항에 맞게 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-134">To use these server technologies directly, ASP.NET Core would need to adapt to the requirements of each server.</span></span> <span data-ttu-id="ed9b3-135">ASP.NET Core는 Kestrel과 같은 웹 서버 구현을 사용하여 다른 서버 기술에서 호스팅될 경우 시작 프로세스 및 환경을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-135">Using a web server implementation, such as Kestrel, ASP.NET Core has control over the startup process and environment when hosted on different server technologies.</span></span>

### <a name="iis-with-kestrel"></a><span data-ttu-id="ed9b3-136">IIS 및 Kestrel</span><span class="sxs-lookup"><span data-stu-id="ed9b3-136">IIS with Kestrel</span></span>

<span data-ttu-id="ed9b3-137">[IIS](/iis/get-started/introduction-to-iis/introduction-to-iis-architecture) 또는 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)를 ASP.NET Core에 대한 역방향 프록시로 사용할 경우 ASP.NET Core 앱은 IIS 작업자 프로세스와 분리된 프로세스에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-137">When using [IIS](/iis/get-started/introduction-to-iis/introduction-to-iis-architecture) or [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) as a reverse proxy for ASP.NET Core, the ASP.NET Core app runs in a process separate from the IIS worker process.</span></span> <span data-ttu-id="ed9b3-138">IIS 프로세스에서 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)은 역방향 프록시 관계를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-138">In the IIS process, the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) coordinates the reverse proxy relationship.</span></span> <span data-ttu-id="ed9b3-139">ASP.NET Core 모듈의 기본 기능은 ASP.NET Core 앱을 시작하고, 작동 중단 시 앱을 다시 시작하고, 앱에 HTTP 트래픽을 전달하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-139">The primary functions of the ASP.NET Core Module are to start the ASP.NET Core app, restart the app when it crashes, and forward HTTP traffic to the app.</span></span> <span data-ttu-id="ed9b3-140">자세한 내용은 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-140">For more information, see [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module).</span></span> 

### <a name="nginx-with-kestrel"></a><span data-ttu-id="ed9b3-141">Nginx 및 Kestrel</span><span class="sxs-lookup"><span data-stu-id="ed9b3-141">Nginx with Kestrel</span></span>

<span data-ttu-id="ed9b3-142">Linux에서 Kestrel에 대한 역방향 프록시 서버로 Nginx를 사용하는 방법에 대한 자세한 내용은 [Nginx를 사용하여 Linux에서 호스트](xref:host-and-deploy/linux-nginx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-142">For information on how to use Nginx on Linux as a reverse proxy server for Kestrel, see [Host on Linux with Nginx](xref:host-and-deploy/linux-nginx).</span></span>

### <a name="apache-with-kestrel"></a><span data-ttu-id="ed9b3-143">Apache 및 Kestrel</span><span class="sxs-lookup"><span data-stu-id="ed9b3-143">Apache with Kestrel</span></span>

<span data-ttu-id="ed9b3-144">Linux에서 Apache에 대한 역방향 프록시 서버로 Nginx를 사용하는 방법에 대한 자세한 내용은 [Apache를 사용하여 Linux에서 호스트](xref:host-and-deploy/linux-apache)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-144">For information on how to use Apache on Linux as a reverse proxy server for Kestrel, see [Host on Linux with Apache](xref:host-and-deploy/linux-apache).</span></span>

## <a name="httpsys"></a><span data-ttu-id="ed9b3-145">HTTP.sys</span><span class="sxs-lookup"><span data-stu-id="ed9b3-145">HTTP.sys</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="ed9b3-146">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="ed9b3-146">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="ed9b3-147">Windows에서 ASP.NET Core 앱을 실행할 경우 Kestrel 대신 HTTP.sys를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-147">If ASP.NET Core apps are run on Windows, HTTP.sys is an alternative to Kestrel.</span></span> <span data-ttu-id="ed9b3-148">최상의 성능을 위해 일반적으로 Kestrel을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-148">Kestrel is generally recommended for best performance.</span></span> <span data-ttu-id="ed9b3-149">앱이 인터넷에 노출되고 필수 기능이 Kestrel이 아닌 HTTP.sys에서 지원되는 경우 시나리오에서 HTTP.sys를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-149">HTTP.sys can be used in scenarios where the app is exposed to the Internet and required features are supported by HTTP.sys but not Kestrel.</span></span> <span data-ttu-id="ed9b3-150">HTTP.sys 기능에 대한 자세한 내용은 [HTTP.sys](xref:fundamentals/servers/httpsys)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-150">For information on HTTP.sys features, see [HTTP.sys](xref:fundamentals/servers/httpsys).</span></span>

![HTTP.sys는 인터넷과 직접 통신합니다.](httpsys/_static/httpsys-to-internet.png)

<span data-ttu-id="ed9b3-152">HTTP.sys는 내부 네트워크에만 노출되는 앱에도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-152">HTTP.sys can also be used for apps that are only exposed to an internal network.</span></span> 

![HTTP.sys는 내부 네트워크와 직접 통신합니다.](httpsys/_static/httpsys-to-internal.png)

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="ed9b3-154">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="ed9b3-154">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="ed9b3-155">ASP.NET Core 1.x에서는 HTTP.sys의 이름이 [WebListener](xref:fundamentals/servers/weblistener)로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-155">HTTP.sys is named [WebListener](xref:fundamentals/servers/weblistener) in ASP.NET Core 1.x.</span></span> <span data-ttu-id="ed9b3-156">Windows에서 ASP.NET Core 앱을 실행하는 경우 IIS가 앱을 호스팅하는 데 사용할 수 없는 시나리오의 대안으로 WebListener를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-156">If ASP.NET Core apps are run on Windows, WebListener is an alternative for scenarios where IIS isn't available to host apps.</span></span>

![WebListener는 인터넷과 직접 통신합니다.](weblistener/_static/weblistener-to-internet.png)

<span data-ttu-id="ed9b3-158">필수 기능이 Kestrel이 아닌 WebListener에서 지원하는 경우 내부 네트워크에만 노출되는 앱에 Kestrel 대신 WebListener를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-158">WebListener can also be used in place of Kestrel for apps that are only exposed to an internal network, if required features are supported by WebListener but not Kestrel.</span></span> <span data-ttu-id="ed9b3-159">WebListener 기능에 대한 자세한 내용은 [WebListener](xref:fundamentals/servers/weblistener)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-159">For information on WebListener features, see [WebListener](xref:fundamentals/servers/weblistener).</span></span>

![WebListener는 내부 네트워크와 직접 통신합니다.](weblistener/_static/weblistener-to-internal.png)

---

## <a name="aspnet-core-server-infrastructure"></a><span data-ttu-id="ed9b3-161">ASP.NET Core 서버 인프라</span><span class="sxs-lookup"><span data-stu-id="ed9b3-161">ASP.NET Core server infrastructure</span></span>

<span data-ttu-id="ed9b3-162">`Startup.Configure` 메서드에서 사용할 수 있는 [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder)는 [IFeatureCollection](/dotnet/api/microsoft.aspnetcore.http.features.ifeaturecollection) 형식의 [ServerFeatures](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder.serverfeatures) 속성을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-162">The [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) available in the `Startup.Configure` method exposes the [ServerFeatures](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder.serverfeatures) property of type [IFeatureCollection](/dotnet/api/microsoft.aspnetcore.http.features.ifeaturecollection).</span></span> <span data-ttu-id="ed9b3-163">Kestrel 및 HTTP.sys(ASP.NET Core 1.x에서 WebListener)는 각각 단일 기능인 [IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature)만을 노출하지만 다른 서버 구현은 추가 기능을 노출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-163">Kestrel and HTTP.sys (WebListener in ASP.NET Core 1.x) only expose a single feature each, [IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature), but different server implementations may expose additional functionality.</span></span>

<span data-ttu-id="ed9b3-164">`IServerAddressesFeature`를 사용하여 런타임 시 서버 구현이 바인딩된 포트를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-164">`IServerAddressesFeature` can be used to find out which port the server implementation has bound at runtime.</span></span>

## <a name="custom-servers"></a><span data-ttu-id="ed9b3-165">사용자 지정 서버</span><span class="sxs-lookup"><span data-stu-id="ed9b3-165">Custom servers</span></span>

<span data-ttu-id="ed9b3-166">기본 제공 서버가 앱의 요구 사항을 충족하지 않으면 사용자 지정 서버 구현을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-166">If the built-in servers don't meet the app's requirements, a custom server implementation can be created.</span></span> <span data-ttu-id="ed9b3-167">[OWIN(Open Web Interface for .NET) 가이드](xref:fundamentals/owin)에서는 [Nowin](https://github.com/Bobris/Nowin) 기반 [IServer](/dotnet/api/microsoft.aspnetcore.hosting.server.iserver) 구현을 작성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-167">The [Open Web Interface for .NET (OWIN) guide](xref:fundamentals/owin) demonstrates how to write a [Nowin](https://github.com/Bobris/Nowin)-based [IServer](/dotnet/api/microsoft.aspnetcore.hosting.server.iserver) implementation.</span></span> <span data-ttu-id="ed9b3-168">앱이 사용하는 기능 인터페이스에는 구현이 필요합니다. 최소한 [IHttpRequestFeature](/dotnet/api/microsoft.aspnetcore.http.features.ihttprequestfeature) 및 [IHttpResponseFeature](/dotnet/api/microsoft.aspnetcore.http.features.ihttpresponsefeature)이 지원되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-168">Only the feature interfaces that the app uses require implementation, though at a minimum [IHttpRequestFeature](/dotnet/api/microsoft.aspnetcore.http.features.ihttprequestfeature) and [IHttpResponseFeature](/dotnet/api/microsoft.aspnetcore.http.features.ihttpresponsefeature) must be supported.</span></span>

## <a name="server-startup"></a><span data-ttu-id="ed9b3-169">서버 시작</span><span class="sxs-lookup"><span data-stu-id="ed9b3-169">Server startup</span></span>

<span data-ttu-id="ed9b3-170">[Visual Studio](https://www.visualstudio.com/vs/), [Mac용 Visual Studio](https://www.visualstudio.com/vs/mac/) 또는 [Visual Studio Code](https://code.visualstudio.com/)를 사용하는 경우 IDE(통합 개발 환경)에서 앱을 시작할 때 서버가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-170">When using [Visual Studio](https://www.visualstudio.com/vs/), [Visual Studio for Mac](https://www.visualstudio.com/vs/mac/), or [Visual Studio Code](https://code.visualstudio.com/), the server is launched when the app is started by the Integrated Development Environment (IDE).</span></span> <span data-ttu-id="ed9b3-171">Windows의 Visual Studio에서 실행 프로필을 사용하여 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)/[ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module) 또는 콘솔에서 앱 및 서버를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-171">In Visual Studio on Windows, launch profiles can be used to start the app and server with either [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)/[ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) or the console.</span></span> <span data-ttu-id="ed9b3-172">Visual Studio Code에서 [Omnisharp](https://github.com/OmniSharp/omnisharp-vscode)로 앱 및 서버를 시작합니다. 그러면 CoreCLR 디버거를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-172">In Visual Studio Code, the app and server are started by [Omnisharp](https://github.com/OmniSharp/omnisharp-vscode), which activates the CoreCLR debugger.</span></span> <span data-ttu-id="ed9b3-173">Mac용 Visual Studio를 사용하여 [Mono Soft-Mode 디버거](http://www.mono-project.com/docs/advanced/runtime/docs/soft-debugger/)로 앱 및 서버를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-173">Using Visual Studio for Mac, the app and server are started by the [Mono Soft-Mode Debugger](http://www.mono-project.com/docs/advanced/runtime/docs/soft-debugger/).</span></span>

<span data-ttu-id="ed9b3-174">프로젝트의 폴더에 있는 명령 프롬프트에서 앱을 시작할 때 [dotnet run](/dotnet/core/tools/dotnet-run)은 서버 및 앱을 시작합니다(Kestrel 및 HTTP.sys만 해당).</span><span class="sxs-lookup"><span data-stu-id="ed9b3-174">When launching an app from a command prompt in the project's folder, [dotnet run](/dotnet/core/tools/dotnet-run) launches the app and server (Kestrel and HTTP.sys only).</span></span> <span data-ttu-id="ed9b3-175">`Debug`(기본값) 또는 `Release`로 설정되어 있는 `-c|--configuration` 옵션으로 구성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-175">The configuration is specified by the `-c|--configuration` option, which is set to either `Debug` (default) or `Release`.</span></span> <span data-ttu-id="ed9b3-176">실행 프로필이 *launchSettings.json* 파일에 있는 경우 `--launch-profile <NAME>` 옵션을 사용하여 실행 프로필(예: `Development` 또는 `Production`)을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-176">If launch profiles are present in a *launchSettings.json* file, use the `--launch-profile <NAME>` option to set the launch profile (for example, `Development` or `Production`).</span></span> <span data-ttu-id="ed9b3-177">자세한 내용은 [dotnet run](/dotnet/core/tools/dotnet-run) 및 [.NET Core 배포 패키징](/dotnet/core/build/distribution-packaging) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed9b3-177">For more information, see the [dotnet run](/dotnet/core/tools/dotnet-run) and [.NET Core distribution packaging](/dotnet/core/build/distribution-packaging) topics.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ed9b3-178">추가 자료</span><span class="sxs-lookup"><span data-stu-id="ed9b3-178">Additional resources</span></span>

* [<span data-ttu-id="ed9b3-179">Kestrel</span><span class="sxs-lookup"><span data-stu-id="ed9b3-179">Kestrel</span></span>](xref:fundamentals/servers/kestrel)
* [<span data-ttu-id="ed9b3-180">Kestrel 및 IIS</span><span class="sxs-lookup"><span data-stu-id="ed9b3-180">Kestrel with IIS</span></span>](xref:fundamentals/servers/aspnet-core-module)
* [<span data-ttu-id="ed9b3-181">Nginx를 사용하여 Linux에서 호스트</span><span class="sxs-lookup"><span data-stu-id="ed9b3-181">Host on Linux with Nginx</span></span>](xref:host-and-deploy/linux-nginx)
* [<span data-ttu-id="ed9b3-182">Apache를 사용하여 Linux에서 호스트</span><span class="sxs-lookup"><span data-stu-id="ed9b3-182">Host on Linux with Apache</span></span>](xref:host-and-deploy/linux-apache)
* <span data-ttu-id="ed9b3-183">[HTTP.sys](xref:fundamentals/servers/httpsys)(ASP.NET Core 1.x의 경우 [WebListener](xref:fundamentals/servers/weblistener) 참조)</span><span class="sxs-lookup"><span data-stu-id="ed9b3-183">[HTTP.sys](xref:fundamentals/servers/httpsys) (for ASP.NET Core 1.x, see [WebListener](xref:fundamentals/servers/weblistener))</span></span>
