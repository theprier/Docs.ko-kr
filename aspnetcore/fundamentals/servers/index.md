---
title: ASP.NET Core의 웹 서버 구현
author: guardrex
description: ASP.NET Core의 웹 서버 Kestrel 및 HTTP.sys를 검색합니다. 서버를 선택하는 방법 및 역방향 프록시 서버를 사용하는 시기에 대해 알아봅니다.
ms.author: tdykstra
ms.custom: mvc
ms.date: 12/01/2018
uid: fundamentals/servers/index
ms.openlocfilehash: 965d69dd071ec71d283284d58e6e1a6e78604f90
ms.sourcegitcommit: 9bb58d7c8dad4bbd03419bcc183d027667fefa20
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/04/2018
ms.locfileid: "52861358"
---
# <a name="web-server-implementations-in-aspnet-core"></a><span data-ttu-id="a7a72-104">ASP.NET Core의 웹 서버 구현</span><span class="sxs-lookup"><span data-stu-id="a7a72-104">Web server implementations in ASP.NET Core</span></span>

<span data-ttu-id="a7a72-105">작성자: [Tom Dykstra](https://github.com/tdykstra), [Steve Smith](https://ardalis.com/), [Stephen Halter](https://twitter.com/halter73) 및 [Chris Ross](https://github.com/Tratcher)</span><span class="sxs-lookup"><span data-stu-id="a7a72-105">By [Tom Dykstra](https://github.com/tdykstra), [Steve Smith](https://ardalis.com/), [Stephen Halter](https://twitter.com/halter73), and [Chris Ross](https://github.com/Tratcher)</span></span>

<span data-ttu-id="a7a72-106">ASP.NET Core 앱은 In-process HTTP 서버 구현을 사용하여 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-106">An ASP.NET Core app runs with an in-process HTTP server implementation.</span></span> <span data-ttu-id="a7a72-107">서버 구현은 HTTP 요청을 수신하고 <xref:Microsoft.AspNetCore.Http.HttpContext>에 구성된 [요청 기능](xref:fundamentals/request-features)의 집합으로 앱에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-107">The server implementation listens for HTTP requests and surfaces them to the app as sets of [request features](xref:fundamentals/request-features) composed into an <xref:Microsoft.AspNetCore.Http.HttpContext>.</span></span>

::: moniker range=">= aspnetcore-2.2"

# <a name="windowstabwindows"></a>[<span data-ttu-id="a7a72-108">Windows</span><span class="sxs-lookup"><span data-stu-id="a7a72-108">Windows</span></span>](#tab/windows)

<span data-ttu-id="a7a72-109">ASP.NET Core는 다음과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-109">ASP.NET Core ships with the following:</span></span>

* <span data-ttu-id="a7a72-110">[Kestrel](xref:fundamentals/servers/kestrel) 서버는 기본 플랫폼 간 HTTP 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-110">[Kestrel server](xref:fundamentals/servers/kestrel) is the default, cross-platform HTTP server.</span></span>
* <span data-ttu-id="a7a72-111">IIS HTTP Server(`IISHttpServer`)는 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)과 함께 사용되는 [IIS In-process 서버](xref:fundamentals/servers/aspnet-core-module#in-process-hosting-model)입니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-111">IIS HTTP Server (`IISHttpServer`) is an [IIS in-process server](xref:fundamentals/servers/aspnet-core-module#in-process-hosting-model) implementation used with the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module).</span></span>
* <span data-ttu-id="a7a72-112">[HTTP.sys 서버](xref:fundamentals/servers/httpsys)는 [Http.Sys 커널 드라이버 및 HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx)를 기반으로 하는 Windows 전용 HTTP 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-112">[HTTP.sys server](xref:fundamentals/servers/httpsys) is a Windows-only HTTP server based on the [HTTP.sys kernel driver and HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span></span> <span data-ttu-id="a7a72-113">ASP.NET Core 1.x에서는 HTTP.sys를 [WebListener](xref:fundamentals/servers/weblistener)라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-113">HTTP.sys is called [WebListener](xref:fundamentals/servers/weblistener) in ASP.NET Core 1.x.</span></span>

# <a name="macostabmacos"></a>[<span data-ttu-id="a7a72-114">macOS</span><span class="sxs-lookup"><span data-stu-id="a7a72-114">macOS</span></span>](#tab/macos)

<span data-ttu-id="a7a72-115">ASP.NET Core는 기본 플랫폼 간 HTTP 서버인 [Kestrel 서버](xref:fundamentals/servers/kestrel)와 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-115">ASP.NET Core ships with [Kestrel server](xref:fundamentals/servers/kestrel), which is the default, cross-platform HTTP server.</span></span>

# <a name="linuxtablinux"></a>[<span data-ttu-id="a7a72-116">Linux</span><span class="sxs-lookup"><span data-stu-id="a7a72-116">Linux</span></span>](#tab/linux)

<span data-ttu-id="a7a72-117">ASP.NET Core는 기본 플랫폼 간 HTTP 서버인 [Kestrel 서버](xref:fundamentals/servers/kestrel)와 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-117">ASP.NET Core ships with [Kestrel server](xref:fundamentals/servers/kestrel), which is the default, cross-platform HTTP server.</span></span>

---

::: moniker-end

::: moniker range="< aspnetcore-2.2"

# <a name="windowstabwindows"></a>[<span data-ttu-id="a7a72-118">Windows</span><span class="sxs-lookup"><span data-stu-id="a7a72-118">Windows</span></span>](#tab/windows)

<span data-ttu-id="a7a72-119">ASP.NET Core는 다음과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-119">ASP.NET Core ships with the following:</span></span>

* <span data-ttu-id="a7a72-120">[Kestrel](xref:fundamentals/servers/kestrel) 서버는 기본 플랫폼 간 HTTP 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-120">[Kestrel server](xref:fundamentals/servers/kestrel) is the default, cross-platform HTTP server.</span></span>
* <span data-ttu-id="a7a72-121">[HTTP.sys 서버](xref:fundamentals/servers/httpsys)는 [Http.Sys 커널 드라이버 및 HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx)를 기반으로 하는 Windows 전용 HTTP 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-121">[HTTP.sys server](xref:fundamentals/servers/httpsys) is a Windows-only HTTP server based on the [HTTP.sys kernel driver and HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span></span> <span data-ttu-id="a7a72-122">ASP.NET Core 1.x에서는 HTTP.sys를 [WebListener](xref:fundamentals/servers/weblistener)라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-122">HTTP.sys is called [WebListener](xref:fundamentals/servers/weblistener) in ASP.NET Core 1.x.</span></span>

# <a name="macostabmacos"></a>[<span data-ttu-id="a7a72-123">macOS</span><span class="sxs-lookup"><span data-stu-id="a7a72-123">macOS</span></span>](#tab/macos)

<span data-ttu-id="a7a72-124">ASP.NET Core는 기본 플랫폼 간 HTTP 서버인 [Kestrel 서버](xref:fundamentals/servers/kestrel)와 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-124">ASP.NET Core ships with [Kestrel server](xref:fundamentals/servers/kestrel), which is the default, cross-platform HTTP server.</span></span>

# <a name="linuxtablinux"></a>[<span data-ttu-id="a7a72-125">Linux</span><span class="sxs-lookup"><span data-stu-id="a7a72-125">Linux</span></span>](#tab/linux)

<span data-ttu-id="a7a72-126">ASP.NET Core는 기본 플랫폼 간 HTTP 서버인 [Kestrel 서버](xref:fundamentals/servers/kestrel)와 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-126">ASP.NET Core ships with [Kestrel server](xref:fundamentals/servers/kestrel), which is the default, cross-platform HTTP server.</span></span>

---

::: moniker-end

## <a name="kestrel"></a><span data-ttu-id="a7a72-127">Kestrel</span><span class="sxs-lookup"><span data-stu-id="a7a72-127">Kestrel</span></span>

<span data-ttu-id="a7a72-128">Kestrel은 ASP.NET Core 프로젝트 템플릿에 포함된 기본 웹 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-128">Kestrel is the default web server included in ASP.NET Core project templates.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="a7a72-129">Kestrel은 다음과 같이 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-129">Kestrel can be used:</span></span>

* <span data-ttu-id="a7a72-130">인터넷을 포함한 네트워크로부터 직접 요청을 처리하는 에지 서버로서 단독으로 사용</span><span class="sxs-lookup"><span data-stu-id="a7a72-130">By itself as an edge server processing requests directly from a network, including the Internet.</span></span>
* <span data-ttu-id="a7a72-131">[IIS(인터넷 정보 서비스)](https://www.iis.net/), [Nginx](http://nginx.org) 또는 [Apache](https://httpd.apache.org/)와 같은 *역방향 프록시 서버*와 함께 사용</span><span class="sxs-lookup"><span data-stu-id="a7a72-131">With a *reverse proxy server*, such as [Internet Information Services (IIS)](https://www.iis.net/), [Nginx](http://nginx.org), or [Apache](https://httpd.apache.org/).</span></span> <span data-ttu-id="a7a72-132">역방향 프록시 서버는 인터넷에서 HTTP 요청을 받아서 Kestrel에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-132">A reverse proxy server receives HTTP requests from the Internet and forwards them to Kestrel.</span></span>

![Kestrel은 역방향 프록시 서버 없이 직접 인터넷과 통신합니다.](kestrel/_static/kestrel-to-internet2.png)

![Kestrel은 IIS, Nginx 또는 Apache 같은 역방향 프록시 서버를 통해 간접적으로 인터넷과 통신합니다.](kestrel/_static/kestrel-to-internet.png)

<span data-ttu-id="a7a72-135">&mdash;역방향 프록시 서버의 유무에 상관없이&mdash; ASP.NET Core 2.0 이상 앱에 대해 지원되는 유효한 호스팅 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-135">Either configuration&mdash;with or without a reverse proxy server&mdash;is a valid and supported hosting configuration for ASP.NET Core 2.0 or later apps.</span></span> <span data-ttu-id="a7a72-136">자세한 내용은 [Kestrel를 역방향 프록시와 함께 사용할 경우](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7a72-136">For more information, see [When to use Kestrel with a reverse proxy](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy).</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="a7a72-137">앱이 내부 네트워크의 요청만을 수락하는 경우 Kestrel을 단독으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-137">If the app only accepts requests from an internal network, Kestrel can be used by itself.</span></span>

![Kestrel은 내부 네트워크와 직접 통신합니다.](kestrel/_static/kestrel-to-internal.png)

<span data-ttu-id="a7a72-139">앱이 인터넷에 노출된 경우, Kestrel은 [IIS(인터넷 정보 서비스)](https://www.iis.net/), [Nginx](http://nginx.org) 또는 [Apache](https://httpd.apache.org/)와 같은 *역방향 프록시 서버*를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-139">If the app is exposed to the Internet, Kestrel must use a *reverse proxy server*, such as [Internet Information Services (IIS)](https://www.iis.net/), [Nginx](http://nginx.org), or [Apache](https://httpd.apache.org/).</span></span> <span data-ttu-id="a7a72-140">역방향 프록시 서버는 인터넷에서 HTTP 요청을 받아서 Kestrel에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-140">A reverse proxy server receives HTTP requests from the Internet and forwards them to Kestrel.</span></span>

![Kestrel은 IIS, Nginx 또는 Apache 같은 역방향 프록시 서버를 통해 간접적으로 인터넷과 통신합니다.](kestrel/_static/kestrel-to-internet.png)

<span data-ttu-id="a7a72-142">인터넷에 직접 노출되는 공용 에지 서버 배포에 역방향 프록시를 사용하는 가장 중요한 이유는 보안입니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-142">The most important reason for using a reverse proxy for public-facing edge server deployments that are exposed directly the Internet is security.</span></span> <span data-ttu-id="a7a72-143">1.x 버전의 Kestrel에는 인터넷의 공격으로부터 보호하기 위한 중요한 보안 기능이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-143">The 1.x versions of Kestrel don't include important security features to defend against attacks from the Internet.</span></span> <span data-ttu-id="a7a72-144">여기에는 적절한 시간 제한, 요청 크기 제한, 동시 연결 제한을 비롯한 다양한 기능이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-144">This includes, but isn't limited to, appropriate timeouts, request size limits, and concurrent connection limits.</span></span>

<span data-ttu-id="a7a72-145">자세한 내용은 [Kestrel를 역방향 프록시와 함께 사용할 경우](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7a72-145">For more information, see [When to use Kestrel with a reverse proxy](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy).</span></span>

::: moniker-end

### <a name="iis-with-kestrel"></a><span data-ttu-id="a7a72-146">IIS 및 Kestrel</span><span class="sxs-lookup"><span data-stu-id="a7a72-146">IIS with Kestrel</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="a7a72-147">[IIS](/iis/get-started/introduction-to-iis/introduction-to-iis-architecture) 또는 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)를 사용할 때 ASP.NET Core 앱은 IIS 작업자 프로세스(*in-process* 호스팅 모델)와 동일한 프로세스에서 실행되거나 IIS 작업자 프로세스(*out-of-process* 호스팅 모델)와는 별개로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-147">When using [IIS](/iis/get-started/introduction-to-iis/introduction-to-iis-architecture) or [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview), the ASP.NET Core app either runs in the same process as the IIS worker process (the *in-process* hosting model) or in a process separate from the IIS worker process (the *out-of-process* hosting model).</span></span>

<span data-ttu-id="a7a72-148">[ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)은 in-process IIS HTTP Server 또는 out-of-process Kestrel 서버 간의 네이티브 IIS 요청을 처리하는 네이티브 IIS 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-148">The [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) is a native IIS module that handles native IIS requests between either the in-process IIS HTTP Server or the out-of-process Kestrel server.</span></span> <span data-ttu-id="a7a72-149">자세한 내용은 <xref:fundamentals/servers/aspnet-core-module>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7a72-149">For more information, see <xref:fundamentals/servers/aspnet-core-module>.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="a7a72-150">[IIS](/iis/get-started/introduction-to-iis/introduction-to-iis-architecture) 또는 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)를 ASP.NET Core에 대한 역방향 프록시로 사용할 경우 ASP.NET Core 앱은 IIS 작업자 프로세스와 분리된 프로세스에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-150">When using [IIS](/iis/get-started/introduction-to-iis/introduction-to-iis-architecture) or [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) as a reverse proxy for ASP.NET Core, the ASP.NET Core app runs in a process separate from the IIS worker process.</span></span> <span data-ttu-id="a7a72-151">IIS 프로세스에서 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)은 역방향 프록시 관계를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-151">In the IIS process, the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) coordinates the reverse proxy relationship.</span></span> <span data-ttu-id="a7a72-152">ASP.NET Core 모듈의 기본 기능은 앱을 시작하고, 크래시 발생 시 앱을 다시 시작하고, 앱으로 HTTP 트래픽을 전달하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-152">The primary functions of the ASP.NET Core Module are to start the app, restart the app when it crashes, and forward HTTP traffic to the app.</span></span> <span data-ttu-id="a7a72-153">자세한 내용은 <xref:fundamentals/servers/aspnet-core-module>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7a72-153">For more information, see <xref:fundamentals/servers/aspnet-core-module>.</span></span>

::: moniker-end

### <a name="nginx-with-kestrel"></a><span data-ttu-id="a7a72-154">Nginx 및 Kestrel</span><span class="sxs-lookup"><span data-stu-id="a7a72-154">Nginx with Kestrel</span></span>

<span data-ttu-id="a7a72-155">Linux에서 Kestrel에 대한 역방향 프록시 서버로 Nginx를 사용하는 방법은 <xref:host-and-deploy/linux-nginx>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7a72-155">For information on how to use Nginx on Linux as a reverse proxy server for Kestrel, see <xref:host-and-deploy/linux-nginx>.</span></span>

### <a name="apache-with-kestrel"></a><span data-ttu-id="a7a72-156">Apache 및 Kestrel</span><span class="sxs-lookup"><span data-stu-id="a7a72-156">Apache with Kestrel</span></span>

<span data-ttu-id="a7a72-157">Linux에서 Kestrel에 대한 역방향 프록시 서버로 Apache를 사용하는 방법은 <xref:host-and-deploy/linux-apache>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7a72-157">For information on how to use Apache on Linux as a reverse proxy server for Kestrel, see <xref:host-and-deploy/linux-apache>.</span></span>

## <a name="httpsys"></a><span data-ttu-id="a7a72-158">HTTP.sys</span><span class="sxs-lookup"><span data-stu-id="a7a72-158">HTTP.sys</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="a7a72-159">Windows에서 ASP.NET Core 앱을 실행할 경우 Kestrel 대신 HTTP.sys를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-159">If ASP.NET Core apps are run on Windows, HTTP.sys is an alternative to Kestrel.</span></span> <span data-ttu-id="a7a72-160">최상의 성능을 위해 일반적으로 Kestrel을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-160">Kestrel is generally recommended for best performance.</span></span> <span data-ttu-id="a7a72-161">앱이 인터넷에 노출되고 필수 기능이 Kestrel이 아닌 HTTP.sys에서 지원되는 경우 시나리오에서 HTTP.sys를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-161">HTTP.sys can be used in scenarios where the app is exposed to the Internet and required capabilities are supported by HTTP.sys but not Kestrel.</span></span> <span data-ttu-id="a7a72-162">자세한 내용은 <xref:fundamentals/servers/httpsys>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7a72-162">For more information, see <xref:fundamentals/servers/httpsys>.</span></span>

![HTTP.sys는 인터넷과 직접 통신합니다.](httpsys/_static/httpsys-to-internet.png)

<span data-ttu-id="a7a72-164">HTTP.sys는 내부 네트워크에만 노출되는 앱에도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-164">HTTP.sys can also be used for apps that are only exposed to an internal network.</span></span>

![HTTP.sys는 내부 네트워크와 직접 통신합니다.](httpsys/_static/httpsys-to-internal.png)

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="a7a72-166">ASP.NET Core 1.x에서는 HTTP.sys의 이름이 [WebListener](xref:fundamentals/servers/weblistener)로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-166">HTTP.sys is named [WebListener](xref:fundamentals/servers/weblistener) in ASP.NET Core 1.x.</span></span> <span data-ttu-id="a7a72-167">Windows에서 ASP.NET Core 앱을 실행하는 경우 IIS가 앱을 호스팅하는 데 사용할 수 없는 시나리오의 대안으로 WebListener를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-167">If ASP.NET Core apps are run on Windows, WebListener is an alternative for scenarios where IIS isn't available to host apps.</span></span>

![WebListener는 인터넷과 직접 통신합니다.](weblistener/_static/weblistener-to-internet.png)

<span data-ttu-id="a7a72-169">필수 기능이 Kestrel이 아닌 WebListener에서 지원하는 경우 내부 네트워크에만 노출되는 앱에 Kestrel 대신 WebListener를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-169">WebListener can also be used in place of Kestrel for apps that are only exposed to an internal network, if required capabilities are supported by WebListener but not Kestrel.</span></span> <span data-ttu-id="a7a72-170">WebListener에 대한 자세한 내용은 [WebListener](xref:fundamentals/servers/weblistener)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7a72-170">For information on WebListener, see [WebListener](xref:fundamentals/servers/weblistener).</span></span>

![WebListener는 내부 네트워크와 직접 통신합니다.](weblistener/_static/weblistener-to-internal.png)

::: moniker-end

## <a name="aspnet-core-server-infrastructure"></a><span data-ttu-id="a7a72-172">ASP.NET Core 서버 인프라</span><span class="sxs-lookup"><span data-stu-id="a7a72-172">ASP.NET Core server infrastructure</span></span>

<span data-ttu-id="a7a72-173">`Startup.Configure` 메서드에서 사용할 수 있는 [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder)는 [IFeatureCollection](/dotnet/api/microsoft.aspnetcore.http.features.ifeaturecollection) 형식의 [ServerFeatures](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder.serverfeatures) 속성을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-173">The [IApplicationBuilder](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder) available in the `Startup.Configure` method exposes the [ServerFeatures](/dotnet/api/microsoft.aspnetcore.builder.iapplicationbuilder.serverfeatures) property of type [IFeatureCollection](/dotnet/api/microsoft.aspnetcore.http.features.ifeaturecollection).</span></span> <span data-ttu-id="a7a72-174">Kestrel 및 HTTP.sys(ASP.NET Core 1.x에서 WebListener)는 각각 단일 기능인 [IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature)만을 노출하지만 다른 서버 구현은 추가 기능을 노출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-174">Kestrel and HTTP.sys (WebListener in ASP.NET Core 1.x) only expose a single feature each, [IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature), but different server implementations may expose additional functionality.</span></span>

<span data-ttu-id="a7a72-175">`IServerAddressesFeature`를 사용하여 런타임 시 서버 구현이 바인딩된 포트를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-175">`IServerAddressesFeature` can be used to find out which port the server implementation has bound at runtime.</span></span>

## <a name="custom-servers"></a><span data-ttu-id="a7a72-176">사용자 지정 서버</span><span class="sxs-lookup"><span data-stu-id="a7a72-176">Custom servers</span></span>

<span data-ttu-id="a7a72-177">기본 제공 서버가 앱의 요구 사항을 충족하지 않으면 사용자 지정 서버 구현을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-177">If the built-in servers don't meet the app's requirements, a custom server implementation can be created.</span></span> <span data-ttu-id="a7a72-178">[OWIN(Open Web Interface for .NET) 가이드](xref:fundamentals/owin)에서는 [Nowin](https://github.com/Bobris/Nowin) 기반 [IServer](/dotnet/api/microsoft.aspnetcore.hosting.server.iserver) 구현을 작성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-178">The [Open Web Interface for .NET (OWIN) guide](xref:fundamentals/owin) demonstrates how to write a [Nowin](https://github.com/Bobris/Nowin)-based [IServer](/dotnet/api/microsoft.aspnetcore.hosting.server.iserver) implementation.</span></span> <span data-ttu-id="a7a72-179">앱이 사용하는 기능 인터페이스에는 구현이 필요합니다. 최소한 [IHttpRequestFeature](/dotnet/api/microsoft.aspnetcore.http.features.ihttprequestfeature) 및 [IHttpResponseFeature](/dotnet/api/microsoft.aspnetcore.http.features.ihttpresponsefeature)이 지원되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-179">Only the feature interfaces that the app uses require implementation, though at a minimum [IHttpRequestFeature](/dotnet/api/microsoft.aspnetcore.http.features.ihttprequestfeature) and [IHttpResponseFeature](/dotnet/api/microsoft.aspnetcore.http.features.ihttpresponsefeature) must be supported.</span></span>

## <a name="server-startup"></a><span data-ttu-id="a7a72-180">서버 시작</span><span class="sxs-lookup"><span data-stu-id="a7a72-180">Server startup</span></span>

<span data-ttu-id="a7a72-181">[Visual Studio](https://www.visualstudio.com/vs/), [Mac용 Visual Studio](https://www.visualstudio.com/vs/mac/) 또는 [Visual Studio Code](https://code.visualstudio.com/)를 사용하는 경우 IDE(통합 개발 환경)에서 앱을 시작할 때 서버가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-181">When using [Visual Studio](https://www.visualstudio.com/vs/), [Visual Studio for Mac](https://www.visualstudio.com/vs/mac/), or [Visual Studio Code](https://code.visualstudio.com/), the server is launched when the app is started by the Integrated Development Environment (IDE).</span></span> <span data-ttu-id="a7a72-182">Windows의 Visual Studio에서 실행 프로필을 사용하여 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)/[ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module) 또는 콘솔에서 앱 및 서버를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-182">In Visual Studio on Windows, launch profiles can be used to start the app and server with either [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)/[ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) or the console.</span></span> <span data-ttu-id="a7a72-183">Visual Studio Code에서 [Omnisharp](https://github.com/OmniSharp/omnisharp-vscode)로 앱 및 서버를 시작합니다. 그러면 CoreCLR 디버거를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-183">In Visual Studio Code, the app and server are started by [Omnisharp](https://github.com/OmniSharp/omnisharp-vscode), which activates the CoreCLR debugger.</span></span> <span data-ttu-id="a7a72-184">Mac용 Visual Studio를 사용하여 [Mono Soft-Mode 디버거](http://www.mono-project.com/docs/advanced/runtime/docs/soft-debugger/)로 앱 및 서버를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-184">Using Visual Studio for Mac, the app and server are started by the [Mono Soft-Mode Debugger](http://www.mono-project.com/docs/advanced/runtime/docs/soft-debugger/).</span></span>

<span data-ttu-id="a7a72-185">프로젝트의 폴더에 있는 명령 프롬프트에서 앱을 시작할 때 [dotnet run](/dotnet/core/tools/dotnet-run)은 서버 및 앱을 시작합니다(Kestrel 및 HTTP.sys만 해당).</span><span class="sxs-lookup"><span data-stu-id="a7a72-185">When launching an app from a command prompt in the project's folder, [dotnet run](/dotnet/core/tools/dotnet-run) launches the app and server (Kestrel and HTTP.sys only).</span></span> <span data-ttu-id="a7a72-186">`Debug`(기본값) 또는 `Release`로 설정되어 있는 `-c|--configuration` 옵션으로 구성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-186">The configuration is specified by the `-c|--configuration` option, which is set to either `Debug` (default) or `Release`.</span></span> <span data-ttu-id="a7a72-187">실행 프로필이 *launchSettings.json* 파일에 있는 경우 `--launch-profile <NAME>` 옵션을 사용하여 실행 프로필(예: `Development` 또는 `Production`)을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-187">If launch profiles are present in a *launchSettings.json* file, use the `--launch-profile <NAME>` option to set the launch profile (for example, `Development` or `Production`).</span></span> <span data-ttu-id="a7a72-188">자세한 내용은 [dotnet run](/dotnet/core/tools/dotnet-run) 및 [.NET Core 배포 패키징](/dotnet/core/build/distribution-packaging) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7a72-188">For more information, see the [dotnet run](/dotnet/core/tools/dotnet-run) and [.NET Core distribution packaging](/dotnet/core/build/distribution-packaging) topics.</span></span>

## <a name="http2-support"></a><span data-ttu-id="a7a72-189">HTTP/2 지원</span><span class="sxs-lookup"><span data-stu-id="a7a72-189">HTTP/2 support</span></span>

<span data-ttu-id="a7a72-190">[HTTP/2](https://httpwg.org/specs/rfc7540.html)는 다음과 같은 배포 시나리오에서 ASP.NET Core를 통해 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-190">[HTTP/2](https://httpwg.org/specs/rfc7540.html) is supported with ASP.NET Core in the following deployment scenarios:</span></span>

::: moniker range=">= aspnetcore-2.2"

* [<span data-ttu-id="a7a72-191">Kestrel</span><span class="sxs-lookup"><span data-stu-id="a7a72-191">Kestrel</span></span>](xref:fundamentals/servers/kestrel#http2-support)
  * <span data-ttu-id="a7a72-192">운영 체제</span><span class="sxs-lookup"><span data-stu-id="a7a72-192">Operating system</span></span>
    * <span data-ttu-id="a7a72-193">Windows Server 2016/Windows 10 이상&dagger;</span><span class="sxs-lookup"><span data-stu-id="a7a72-193">Windows Server 2016/Windows 10 or later&dagger;</span></span>
    * <span data-ttu-id="a7a72-194">Linux 및 OpenSSL 1.0.2 이상(예: Ubuntu 16.04 이상)</span><span class="sxs-lookup"><span data-stu-id="a7a72-194">Linux with OpenSSL 1.0.2 or later (for example, Ubuntu 16.04 or later)</span></span>
    * <span data-ttu-id="a7a72-195">이후 릴리스에서는 macOS에서 HTTP/2가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-195">HTTP/2 will be supported on macOS in a future release.</span></span>
  * <span data-ttu-id="a7a72-196">대상 프레임워크: .NET Core 2.2 이상</span><span class="sxs-lookup"><span data-stu-id="a7a72-196">Target framework: .NET Core 2.2 or later</span></span>
* [<span data-ttu-id="a7a72-197">HTTP.sys</span><span class="sxs-lookup"><span data-stu-id="a7a72-197">HTTP.sys</span></span>](xref:fundamentals/servers/httpsys#http2-support)
  * <span data-ttu-id="a7a72-198">Windows Server 2016/Windows 10 이상</span><span class="sxs-lookup"><span data-stu-id="a7a72-198">Windows Server 2016/Windows 10 or later</span></span>
  * <span data-ttu-id="a7a72-199">대상 프레임워크: HTTP.sys 배포에는 적용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-199">Target framework: Not applicable to HTTP.sys deployments.</span></span>
* [<span data-ttu-id="a7a72-200">IIS(In-Process)</span><span class="sxs-lookup"><span data-stu-id="a7a72-200">IIS (in-process)</span></span>](xref:host-and-deploy/iis/index#http2-support)
  * <span data-ttu-id="a7a72-201">Windows Server 2016/Windows 10 이상, IIS 10 이상</span><span class="sxs-lookup"><span data-stu-id="a7a72-201">Windows Server 2016/Windows 10 or later; IIS 10 or later</span></span>
  * <span data-ttu-id="a7a72-202">대상 프레임워크: .NET Core 2.2 이상</span><span class="sxs-lookup"><span data-stu-id="a7a72-202">Target framework: .NET Core 2.2 or later</span></span>
* [<span data-ttu-id="a7a72-203">IIS(Out-of-process)</span><span class="sxs-lookup"><span data-stu-id="a7a72-203">IIS (out-of-process)</span></span>](xref:host-and-deploy/iis/index#http2-support)
  * <span data-ttu-id="a7a72-204">Windows Server 2016/Windows 10 이상, IIS 10 이상</span><span class="sxs-lookup"><span data-stu-id="a7a72-204">Windows Server 2016/Windows 10 or later; IIS 10 or later</span></span>
  * <span data-ttu-id="a7a72-205">공용 에지 서버 연결은 HTTP/2를 사용하지만 Kestrel에 대한 역방향 프록시 연결은 HTTP/1.1을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-205">Public-facing edge server connections use HTTP/2, but the reverse proxy connection to Kestrel uses HTTP/1.1.</span></span>
  * <span data-ttu-id="a7a72-206">대상 프레임워크: IIS Out-of-process 배포에는 적용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-206">Target framework: Not applicable to IIS out-of-process deployments.</span></span>

<span data-ttu-id="a7a72-207">&dagger;Kestrel은 Windows Server 2012 R2와 Windows 8.1에서의 HTTP/2 지원을 제한했습니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-207">&dagger;Kestrel has limited support for HTTP/2 on Windows Server 2012 R2 and Windows 8.1.</span></span> <span data-ttu-id="a7a72-208">이러한 운영 체제에서 사용할 수 있는 지원 가능 TLS 암호 그룹 목록이 제한되므로 지원이 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-208">Support is limited because the list of supported TLS cipher suites available on these operating systems is limited.</span></span> <span data-ttu-id="a7a72-209">TLS 연결을 보호하는 데 ECDSA(타원 곡선 디지털 서명 알고리즘)를 사용하여 생성된 인증서가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-209">A certificate generated using an Elliptic Curve Digital Signature Algorithm (ECDSA) may be required to secure TLS connections.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

* [<span data-ttu-id="a7a72-210">HTTP.sys</span><span class="sxs-lookup"><span data-stu-id="a7a72-210">HTTP.sys</span></span>](xref:fundamentals/servers/httpsys#http2-support)
  * <span data-ttu-id="a7a72-211">Windows Server 2016/Windows 10 이상</span><span class="sxs-lookup"><span data-stu-id="a7a72-211">Windows Server 2016/Windows 10 or later</span></span>
  * <span data-ttu-id="a7a72-212">대상 프레임워크: HTTP.sys 배포에는 적용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-212">Target framework: Not applicable to HTTP.sys deployments.</span></span>
* [<span data-ttu-id="a7a72-213">IIS(Out-of-process)</span><span class="sxs-lookup"><span data-stu-id="a7a72-213">IIS (out-of-process)</span></span>](xref:host-and-deploy/iis/index#http2-support)
  * <span data-ttu-id="a7a72-214">Windows Server 2016/Windows 10 이상, IIS 10 이상</span><span class="sxs-lookup"><span data-stu-id="a7a72-214">Windows Server 2016/Windows 10 or later; IIS 10 or later</span></span>
  * <span data-ttu-id="a7a72-215">공용 에지 서버 연결은 HTTP/2를 사용하지만 Kestrel에 대한 역방향 프록시 연결은 HTTP/1.1을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-215">Public-facing edge server connections use HTTP/2, but the reverse proxy connection to Kestrel uses HTTP/1.1.</span></span>
  * <span data-ttu-id="a7a72-216">대상 프레임워크: IIS Out-of-process 배포에는 적용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-216">Target framework: Not applicable to IIS out-of-process deployments.</span></span>

::: moniker-end

<span data-ttu-id="a7a72-217">HTTP/2 연결은 [ALPN(Application-Layer Protocol Negotiation)](https://tools.ietf.org/html/rfc7301#section-3) 및 TLS 1.2 이상을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a7a72-217">An HTTP/2 connection must use [Application-Layer Protocol Negotiation (ALPN)](https://tools.ietf.org/html/rfc7301#section-3) and TLS 1.2 or later.</span></span> <span data-ttu-id="a7a72-218">자세한 정보는 서버 배포 시나리오와 관련된 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a7a72-218">For more information, see the topics that pertain to your server deployment scenarios.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a7a72-219">추가 자료</span><span class="sxs-lookup"><span data-stu-id="a7a72-219">Additional resources</span></span>

* <xref:fundamentals/servers/kestrel>
* <xref:fundamentals/servers/aspnet-core-module>
* <xref:host-and-deploy/iis/index>
* <xref:host-and-deploy/azure-apps/index>
* <xref:host-and-deploy/linux-nginx>
* <xref:host-and-deploy/linux-apache>
* <span data-ttu-id="a7a72-220"><xref:fundamentals/servers/httpsys>(ASP.NET Core 1.x에 대해서는 <xref:fundamentals/servers/weblistener> 참조)</span><span class="sxs-lookup"><span data-stu-id="a7a72-220"><xref:fundamentals/servers/httpsys> (for ASP.NET Core 1.x, see <xref:fundamentals/servers/weblistener>)</span></span>
