---
title: Nginx를 사용하여 Linux에서 ASP.NET Core 호스트
author: rick-anderson
description: Ubuntu 16.04에서 Nginx를 역방향 프록시로 설정하여 Kestrel에서 실행되는 ASP.NET Core 웹앱에 HTTP 트래픽을 전달하는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 05/22/2018
uid: host-and-deploy/linux-nginx
ms.openlocfilehash: aba9ed41ac3650d8c645d71fb772e2a8e4f32f02
ms.sourcegitcommit: c8e62aa766641aa55105f7db79cdf2b27a6e5977
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2018
ms.locfileid: "39254859"
---
# <a name="host-aspnet-core-on-linux-with-nginx"></a><span data-ttu-id="fa99d-103">Nginx를 사용하여 Linux에서 ASP.NET Core 호스트</span><span class="sxs-lookup"><span data-stu-id="fa99d-103">Host ASP.NET Core on Linux with Nginx</span></span>

<span data-ttu-id="fa99d-104">작성자: [Sourabh Shirhatti](https://twitter.com/sshirhatti)</span><span class="sxs-lookup"><span data-stu-id="fa99d-104">By [Sourabh Shirhatti](https://twitter.com/sshirhatti)</span></span>

<span data-ttu-id="fa99d-105">이 가이드에서는 Ubuntu 16.04 Server에서 프로덕션 준비 ASP.NET Core 환경을 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-105">This guide explains setting up a production-ready ASP.NET Core environment on an Ubuntu 16.04 server.</span></span> <span data-ttu-id="fa99d-106">이 지침은 최신 버전의 Ubuntu에서 작동할 수 있지만 최신 버전에서 테스트되지는 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-106">These instructions likely work with newer versions of Ubuntu, but the instructions haven't been tested with newer versions.</span></span>

> [!NOTE]
> <span data-ttu-id="fa99d-107">Ubuntu 14.04의 경우 Kestrel 프로세스를 모니터링하기 위한 솔루션으로 *supervisord*를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-107">For Ubuntu 14.04, *supervisord* is recommended as a solution for monitoring the Kestrel process.</span></span> <span data-ttu-id="fa99d-108">*systemd*는 Ubuntu 14.04에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-108">*systemd* isn't available on Ubuntu 14.04.</span></span> <span data-ttu-id="fa99d-109">Ubuntu 14.04 지침의 경우 [이 항목의 이전 버전](https://github.com/aspnet/Docs/blob/e9c1419175c4dd7e152df3746ba1df5935aaafd5/aspnetcore/publishing/linuxproduction.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fa99d-109">For Ubuntu 14.04 instructions, see the [previous version of this topic](https://github.com/aspnet/Docs/blob/e9c1419175c4dd7e152df3746ba1df5935aaafd5/aspnetcore/publishing/linuxproduction.md).</span></span>

<span data-ttu-id="fa99d-110">이 가이드의 내용:</span><span class="sxs-lookup"><span data-stu-id="fa99d-110">This guide:</span></span>

* <span data-ttu-id="fa99d-111">기존 ASP.NET Core 앱을 역방향 프록시 서버 뒤에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-111">Places an existing ASP.NET Core app behind a reverse proxy server.</span></span>
* <span data-ttu-id="fa99d-112">역방향 프록시 서버를 설정하여 Kestrel 웹 서버에 요청을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-112">Sets up the reverse proxy server to forward requests to the Kestrel web server.</span></span>
* <span data-ttu-id="fa99d-113">웹앱이 시작 시 디먼으로 실행되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-113">Ensures the web app runs on startup as a daemon.</span></span>
* <span data-ttu-id="fa99d-114">웹앱 다시 시작을 지원하도록 프로세스 관리 도구를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-114">Configures a process management tool to help restart the web app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa99d-115">전제 조건</span><span class="sxs-lookup"><span data-stu-id="fa99d-115">Prerequisites</span></span>

1. <span data-ttu-id="fa99d-116">sudo 권한을 가진 표준 사용자 계정으로 Ubuntu 16.04 Server에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-116">Access to an Ubuntu 16.04 server with a standard user account with sudo privilege.</span></span>
1. <span data-ttu-id="fa99d-117">서버에서 .NET Core 런타임을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-117">Install the .NET Core runtime on the server.</span></span>
   1. <span data-ttu-id="fa99d-118">[.NET Core 모든 다운로드 페이지](https://www.microsoft.com/net/download/all)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-118">Visit the [.NET Core All Downloads page](https://www.microsoft.com/net/download/all).</span></span>
   1. <span data-ttu-id="fa99d-119">**런타임** 아래의 목록에서 최신 미리 보기 상태가 아닌 런타임을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-119">Select the latest non-preview runtime from the list under **Runtime**.</span></span>
   1. <span data-ttu-id="fa99d-120">Ubuntu 버전의 서버와 일치하는 Ubuntu에 대한 지침을 선택하고 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-120">Select and follow the instructions for Ubuntu that match the Ubuntu version of the server.</span></span>
1. <span data-ttu-id="fa99d-121">기존 ASP.NET Core 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-121">An existing ASP.NET Core app.</span></span>

## <a name="publish-and-copy-over-the-app"></a><span data-ttu-id="fa99d-122">앱 게시 및 복사</span><span class="sxs-lookup"><span data-stu-id="fa99d-122">Publish and copy over the app</span></span>

<span data-ttu-id="fa99d-123">[프레임워크 종속 배포](/dotnet/core/deploying/#framework-dependent-deployments-fdd)인 경우 앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-123">Configure the app for a [framework-dependent deployment](/dotnet/core/deploying/#framework-dependent-deployments-fdd).</span></span>

<span data-ttu-id="fa99d-124">서버에서 실행할 수 있는 디렉터리(예: *bin/Release/&lt;target_framework_moniker&gt;/publish*)로 앱을 패키징하기 위해 개발 환경에서 [dotnet publish](/dotnet/core/tools/dotnet-publish)를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-124">Run [dotnet publish](/dotnet/core/tools/dotnet-publish) from the development environment to package an app into a directory (for example, *bin/Release/&lt;target_framework_moniker&gt;/publish*) that can run on the server:</span></span>

```console
dotnet publish --configuration Release
```

<span data-ttu-id="fa99d-125">.NET Core 런타임을 서버에서 유지 관리하지 않으려는 경우 앱은 [자체 포함된 배포](/dotnet/core/deploying/#self-contained-deployments-scd)로 게시될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-125">The app can also be published as a [self-contained deployment](/dotnet/core/deploying/#self-contained-deployments-scd) if you prefer not to maintain the .NET Core runtime on the server.</span></span>

<span data-ttu-id="fa99d-126">조직의 워크플로에 통합된 도구(예: SCP, SFTP)를 사용하여 ASP.NET Core 앱을 서버에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-126">Copy the ASP.NET Core app to the server using a tool that integrates into the organization's workflow (for example, SCP, SFTP).</span></span> <span data-ttu-id="fa99d-127">*var* 디렉터리(예: *var/aspnetcore/hellomvc*)에서 웹앱을 찾는 것이 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-127">It's common to locate web apps under the *var* directory (for example, *var/aspnetcore/hellomvc*).</span></span>

> [!NOTE]
> <span data-ttu-id="fa99d-128">프로덕션 배포 시나리오에서 지속적인 통합 워크플로는 앱을 게시하고 자산을 서버로 복사하는 워크플로를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-128">Under a production deployment scenario, a continuous integration workflow does the work of publishing the app and copying the assets to the server.</span></span>

<span data-ttu-id="fa99d-129">앱을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-129">Test the app:</span></span>

1. <span data-ttu-id="fa99d-130">명령줄에서 `dotnet <app_assembly>.dll` 앱을 실행하세요.</span><span class="sxs-lookup"><span data-stu-id="fa99d-130">From the command line, run the app: `dotnet <app_assembly>.dll`.</span></span>
1. <span data-ttu-id="fa99d-131">브라우저에서 `http://<serveraddress>:<port>`로 이동하여 앱이 Linux에서 로컬로 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-131">In a browser, navigate to `http://<serveraddress>:<port>` to verify the app works on Linux locally.</span></span>

## <a name="configure-a-reverse-proxy-server"></a><span data-ttu-id="fa99d-132">역방향 프록시 서버 구성</span><span class="sxs-lookup"><span data-stu-id="fa99d-132">Configure a reverse proxy server</span></span>

<span data-ttu-id="fa99d-133">역방향 프록시는 동적 웹앱을 지원하기 위한 일반적인 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-133">A reverse proxy is a common setup for serving dynamic web apps.</span></span> <span data-ttu-id="fa99d-134">역방향 프록시는 HTTP 요청을 종료하고 이 요청을 ASP.NET Core 앱에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-134">A reverse proxy terminates the HTTP request and forwards it to the ASP.NET Core app.</span></span>

::: moniker range=">= aspnetcore-2.0"

> [!NOTE]
> <span data-ttu-id="fa99d-135">&mdash;역방향 프록시 서버의 유무에 상관없이&mdash; ASP.NET Core 2.0 이상 앱에 대해 지원되는 유효한 호스팅 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-135">Either configuration&mdash;with or without a reverse proxy server&mdash;is a valid and supported hosting configuration for ASP.NET Core 2.0 or later apps.</span></span> <span data-ttu-id="fa99d-136">자세한 내용은 [Kestrel를 역방향 프록시와 함께 사용할 경우](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fa99d-136">For more information, see [When to use Kestrel with a reverse proxy](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy).</span></span>

::: moniker-end

### <a name="use-a-reverse-proxy-server"></a><span data-ttu-id="fa99d-137">역방향 프록시 서버를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-137">Use a reverse proxy server</span></span>

<span data-ttu-id="fa99d-138">Kestrel은 ASP.NET Core에서 동적 콘텐츠를 제공하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-138">Kestrel is great for serving dynamic content from ASP.NET Core.</span></span> <span data-ttu-id="fa99d-139">그러나 웹 지원 기능은 IIS, Apache 또는 Nginx와 같은 서버만큼 기능이 다양하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-139">However, the web serving capabilities aren't as feature rich as servers such as IIS, Apache, or Nginx.</span></span> <span data-ttu-id="fa99d-140">역방향 프록시 서버는 정적 콘텐츠 지원, 요청 캐시, 요청 압축 및 HTTP 서버에서 SSL 종료 같은 작업을 오프로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-140">A reverse proxy server can offload work such as serving static content, caching requests, compressing requests, and SSL termination from the HTTP server.</span></span> <span data-ttu-id="fa99d-141">역방향 프록시 서버는 전용 컴퓨터에 있거나 HTTP 서버와 함께 배포될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-141">A reverse proxy server may reside on a dedicated machine or may be deployed alongside an HTTP server.</span></span>

<span data-ttu-id="fa99d-142">이 가이드에서는 Nginx의 단일 인스턴스가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-142">For the purposes of this guide, a single instance of Nginx is used.</span></span> <span data-ttu-id="fa99d-143">이 인스턴스는 HTTP 서버와 함께 동일한 서버에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-143">It runs on the same server, alongside the HTTP server.</span></span> <span data-ttu-id="fa99d-144">요구 사항에 따라 다른 설정을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-144">Based on requirements, a different setup may be chosen.</span></span>

<span data-ttu-id="fa99d-145">요청이 역방향 프록시를 통해 전달되므로 [Microsoft.AspNetCore.HttpOverrides](https://www.nuget.org/packages/Microsoft.AspNetCore.HttpOverrides/) 패키지의 [전달된 헤더 미들웨어](xref:host-and-deploy/proxy-load-balancer)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-145">Because requests are forwarded by reverse proxy, use the [Forwarded Headers Middleware](xref:host-and-deploy/proxy-load-balancer) from the [Microsoft.AspNetCore.HttpOverrides](https://www.nuget.org/packages/Microsoft.AspNetCore.HttpOverrides/) package.</span></span> <span data-ttu-id="fa99d-146">이 미들웨어는 `X-Forwarded-Proto` 헤더를 사용하여 `Request.Scheme`을 업데이트하므로 리디렉션 URI 및 기타 보안 정책이 제대로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-146">The middleware updates the `Request.Scheme`, using the `X-Forwarded-Proto` header, so that redirect URIs and other security policies work correctly.</span></span>

<span data-ttu-id="fa99d-147">전달된 헤더 미들웨어를 호출한 후에 인증, 링크 생성, 리디렉션 및 지리적 위치 등 체계에 따라 달라지는 구성 요소를 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-147">Any component that depends on the scheme, such as authentication, link generation, redirects, and geolocation, must be placed after invoking the Forwarded Headers Middleware.</span></span> <span data-ttu-id="fa99d-148">일반 규칙으로 전달된 헤더 미들웨어는 진단 및 오류 처리 미들웨어를 제외한 다른 미들웨어 전에 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-148">As a general rule, Forwarded Headers Middleware should run before other middleware except diagnostics and error handling middleware.</span></span> <span data-ttu-id="fa99d-149">이 순서를 지정하면 전달된 헤더 정보에 따라 달라지는 미들웨어는 처리하기 위해 헤더 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-149">This ordering ensures that the middleware relying on forwarded headers information can consume the header values for processing.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="fa99d-150">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="fa99d-150">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="fa99d-151">[UseAuthentication](/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication) 또는 유사한 인증 체계 미들웨어를 호출하기 전에 `Startup.Configure`에서 [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-151">Invoke the [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) method in `Startup.Configure` before calling [UseAuthentication](/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication) or similar authentication scheme middleware.</span></span> <span data-ttu-id="fa99d-152">`X-Forwarded-For` 및 `X-Forwarded-Proto` 헤더를 전달하도록 미들웨어를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-152">Configure the middleware to forward the `X-Forwarded-For` and `X-Forwarded-Proto` headers:</span></span>

```csharp
app.UseForwardedHeaders(new ForwardedHeadersOptions
{
    ForwardedHeaders = ForwardedHeaders.XForwardedFor | ForwardedHeaders.XForwardedProto
});

app.UseAuthentication();
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="fa99d-153">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="fa99d-153">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="fa99d-154">[UseIdentity](/dotnet/api/microsoft.aspnetcore.builder.builderextensions.useidentity)와 [UseFacebookAuthentication](/dotnet/api/microsoft.aspnetcore.builder.facebookappbuilderextensions.usefacebookauthentication) 또는 유사한 인증 체계 미들웨어를 호출하기 전에 `Startup.Configure`에서 [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-154">Invoke the [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) method in `Startup.Configure` before calling [UseIdentity](/dotnet/api/microsoft.aspnetcore.builder.builderextensions.useidentity) and [UseFacebookAuthentication](/dotnet/api/microsoft.aspnetcore.builder.facebookappbuilderextensions.usefacebookauthentication) or similar authentication scheme middleware.</span></span> <span data-ttu-id="fa99d-155">`X-Forwarded-For` 및 `X-Forwarded-Proto` 헤더를 전달하도록 미들웨어를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-155">Configure the middleware to forward the `X-Forwarded-For` and `X-Forwarded-Proto` headers:</span></span>

```csharp
app.UseForwardedHeaders(new ForwardedHeadersOptions
{
    ForwardedHeaders = ForwardedHeaders.XForwardedFor | ForwardedHeaders.XForwardedProto
});

app.UseIdentity();
app.UseFacebookAuthentication(new FacebookOptions()
{
    AppId = Configuration["Authentication:Facebook:AppId"],
    AppSecret = Configuration["Authentication:Facebook:AppSecret"]
});
```

---

<span data-ttu-id="fa99d-156">미들웨어에 [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions)가 지정되지 않은 경우 전달할 기본 헤더는 `None`입니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-156">If no [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions) are specified to the middleware, the default headers to forward are `None`.</span></span>

<span data-ttu-id="fa99d-157">프록시 서버 및 부하 분산 장치 외에도 호스팅되는 앱에 추가 구성이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-157">Additional configuration might be required for apps hosted behind proxy servers and load balancers.</span></span> <span data-ttu-id="fa99d-158">자세한 내용은 [프록시 서버 및 부하 분산 장치를 사용하도록 ASP.NET Core 구성](xref:host-and-deploy/proxy-load-balancer)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fa99d-158">For more information, see [Configure ASP.NET Core to work with proxy servers and load balancers](xref:host-and-deploy/proxy-load-balancer).</span></span>

### <a name="install-nginx"></a><span data-ttu-id="fa99d-159">Nginx 설치</span><span class="sxs-lookup"><span data-stu-id="fa99d-159">Install Nginx</span></span>

<span data-ttu-id="fa99d-160">`apt-get`을 사용하여 Nginx를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-160">Use `apt-get` to install Nginx.</span></span> <span data-ttu-id="fa99d-161">설치 관리자는 시스템 시작 시 Nginx를 디먼으로 실행하는 *systemd* 시작 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-161">The installer creates a *systemd* init script that runs Nginx as daemon on system startup.</span></span> 

```bash
sudo -s
nginx=stable # use nginx=development for latest development version
add-apt-repository ppa:nginx/$nginx
apt-get update
apt-get install nginx
```

<span data-ttu-id="fa99d-162">Ubuntu PPA(개인 패키지 보관)는 지원자에서 유지 관리하고 [nginx.org](https://nginx.org/)에서 배포되지 않습니다. 자세한 내용은 [Nginx: 이진 릴리스: 공식 Debian/Ubuntu 패키지](https://www.nginx.com/resources/wiki/start/topics/tutorials/install/#official-debian-ubuntu-packages)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fa99d-162">The Ubuntu Personal Package Archive (PPA) is maintained by volunteers and isn't distributed by [nginx.org](https://nginx.org/). For more information, see [Nginx: Binary Releases: Official Debian/Ubuntu packages](https://www.nginx.com/resources/wiki/start/topics/tutorials/install/#official-debian-ubuntu-packages).</span></span>

> [!NOTE]
> <span data-ttu-id="fa99d-163">선택적 Nginx 모듈이 필요한 경우 소스에서 Nginx를 빌드해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-163">If optional Nginx modules are required, building Nginx from source might be required.</span></span>

<span data-ttu-id="fa99d-164">Nginx가 처음 설치되었으므로 다음을 실행하여 명시적으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-164">Since Nginx was installed for the first time, explicitly start it by running:</span></span>

```bash
sudo service nginx start
```

<span data-ttu-id="fa99d-165">브라우저에 Nginx에 대한 기본 방문 페이지가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-165">Verify a browser displays the default landing page for Nginx.</span></span> <span data-ttu-id="fa99d-166">방문 페이지는 `http://<server_IP_address>/index.nginx-debian.html`에 도달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-166">The landing page is reachable at `http://<server_IP_address>/index.nginx-debian.html`.</span></span>

### <a name="configure-nginx"></a><span data-ttu-id="fa99d-167">Nginx 구성</span><span class="sxs-lookup"><span data-stu-id="fa99d-167">Configure Nginx</span></span>

<span data-ttu-id="fa99d-168">Nginx를 역방향 프록시로 구성하여 요청을 ASP.NET Core 앱에 프로그램에 전달하려면 */etc/nginx/sites-available/default*를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-168">To configure Nginx as a reverse proxy to forward requests to your ASP.NET Core app, modify */etc/nginx/sites-available/default*.</span></span> <span data-ttu-id="fa99d-169">텍스트 편집기에서 해당 항목을 열고 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-169">Open it in a text editor, and replace the contents with the following:</span></span>

```nginx
server {
    listen        80;
    server_name   example.com *.example.com;
    location / {
        proxy_pass         http://localhost:5000;
        proxy_http_version 1.1;
        proxy_set_header   Upgrade $http_upgrade;
        proxy_set_header   Connection keep-alive;
        proxy_set_header   Host $host;
        proxy_cache_bypass $http_upgrade;
        proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header   X-Forwarded-Proto $scheme;
    }
}
```

<span data-ttu-id="fa99d-170">`server_name`이 일치하지 않으면 Nginx는 기본 서버를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-170">When no `server_name` matches, Nginx uses the default server.</span></span> <span data-ttu-id="fa99d-171">기본 서버가 정의되지 않은 경우 구성 파일의 첫 번째 서버는 기본 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-171">If no default server is defined, the first server in the configuration file is the default server.</span></span> <span data-ttu-id="fa99d-172">구성 파일에 있는 444 상태 코드를 반환하는 특정 기본 서버를 추가하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-172">As a best practice, add a specific default server which returns a status code of 444 in your configuration file.</span></span> <span data-ttu-id="fa99d-173">기본 서버 구성 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-173">A default server configuration example is:</span></span>

```nginx
server {
    listen   80 default_server;
    # listen [::]:80 default_server deferred;
    return   444;
}
```

<span data-ttu-id="fa99d-174">이전 구성 파일과 기본 서버를 사용하여 Nginx는 포트 80에서 호스트 헤더 `example.com` 또는 `*.example.com`가 포함된 공용 트래픽을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-174">With the preceding configuration file and default server, Nginx accepts public traffic on port 80 with host header `example.com` or `*.example.com`.</span></span> <span data-ttu-id="fa99d-175">이러한 호스트와 일치하지 않는 요청은 Kestrel로 전달되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-175">Requests not matching these hosts won't get forwarded to Kestrel.</span></span> <span data-ttu-id="fa99d-176">Nginx는 일치하는 요청을 `http://localhost:5000`의 Kestrel에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-176">Nginx forwards the matching requests to Kestrel at `http://localhost:5000`.</span></span> <span data-ttu-id="fa99d-177">자세한 내용은 [How nginx processes a request](https://nginx.org/docs/http/request_processing.html)(nginx가 요청을 처리하는 방법)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fa99d-177">See [How nginx processes a request](https://nginx.org/docs/http/request_processing.html) for more information.</span></span> <span data-ttu-id="fa99d-178">Kestrel의 IP/포트를 변경 하려면 [Kestrel: 끝점 구성](xref:fundamentals/servers/kestrel#endpoint-configuration)을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-178">To change Kestrel's IP/port, see [Kestrel: Endpoint configuration](xref:fundamentals/servers/kestrel#endpoint-configuration).</span></span>

> [!WARNING]
> <span data-ttu-id="fa99d-179">적절한 [server_name 지시문](https://nginx.org/docs/http/server_names.html)을 지정하지 않으면 앱이 보안 취약성에 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-179">Failure to specify a proper [server_name directive](https://nginx.org/docs/http/server_names.html) exposes your app to security vulnerabilities.</span></span> <span data-ttu-id="fa99d-180">전체 부모 도메인을 제어하는 경우 하위 도메인 와일드카드 바인딩(예: `*.example.com`)에는 이러한 보안 위험이 발생하지 않습니다(취약한 `*.com`과 반대임).</span><span class="sxs-lookup"><span data-stu-id="fa99d-180">Subdomain wildcard binding (for example, `*.example.com`) doesn't pose this security risk if you control the entire parent domain (as opposed to `*.com`, which is vulnerable).</span></span> <span data-ttu-id="fa99d-181">자세한 내용은 [rfc7230 섹션-5.4](https://tools.ietf.org/html/rfc7230#section-5.4)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fa99d-181">See [rfc7230 section-5.4](https://tools.ietf.org/html/rfc7230#section-5.4) for more information.</span></span>

<span data-ttu-id="fa99d-182">Nginx 구성이 설정되면 `sudo nginx -t`를 실행하여 구성 파일의 구문을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-182">Once the Nginx configuration is established, run `sudo nginx -t` to verify the syntax of the configuration files.</span></span> <span data-ttu-id="fa99d-183">구성 파일 테스트에 성공하면 `sudo nginx -s reload`를 실행하여 Nginx가 변경 내용을 선택하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-183">If the configuration file test is successful, force Nginx to pick up the changes by running `sudo nginx -s reload`.</span></span>

<span data-ttu-id="fa99d-184">앱을 서버에서 직접 실행하려면:</span><span class="sxs-lookup"><span data-stu-id="fa99d-184">To directly run the app on the server:</span></span>

1. <span data-ttu-id="fa99d-185">앱의 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-185">Navigate to the app's directory.</span></span>
1. <span data-ttu-id="fa99d-186">앱의 실행 파일인 `./<app_executable>`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-186">Run the app's executable: `./<app_executable>`.</span></span>

<span data-ttu-id="fa99d-187">사용 권한 오류가 발생하는 경우 사용 권한을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-187">If a permissions error occurs, change the permissions:</span></span>

```console
chmod u+x <app_executable>
```

<span data-ttu-id="fa99d-188">앱이 서버에서 실행되지만 인터넷을 통해 응답하지 않는 경우 서버의 방화벽을 확인하고 포트 80이 열려 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-188">If the app runs on the server but fails to respond over the Internet, check the server's firewall and confirm that port 80 is open.</span></span> <span data-ttu-id="fa99d-189">Ubuntu Azure VM을 사용하는 경우 인바운드 포트 80 트래픽을 사용하는 NSG(네트워크 보안 그룹) 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-189">If using an Azure Ubuntu VM, add a Network Security Group (NSG) rule that enables inbound port 80 traffic.</span></span> <span data-ttu-id="fa99d-190">인바운드 규칙을 사용할 때 아웃바운드 트래픽이 자동으로 부여되므로 아웃바운드 포트 80 규칙을 사용하도록 설정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-190">There's no need to enable an outbound port 80 rule, as the outbound traffic is automatically granted when the inbound rule is enabled.</span></span>

<span data-ttu-id="fa99d-191">앱 테스트를 완료한 후에 명령 프롬프트에서 `Ctrl+C`를 사용하여 앱을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-191">When done testing the app, shut the app down with `Ctrl+C` at the command prompt.</span></span>

## <a name="monitoring-the-app"></a><span data-ttu-id="fa99d-192">앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="fa99d-192">Monitoring the app</span></span>

<span data-ttu-id="fa99d-193">서버는 `http://<serveraddress>:80`에 대해 실행된 요청을 `http://127.0.0.1:5000`의 Kestrel에서 실행되는 ASP.NET Core 앱에 전달하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-193">The server is setup to forward requests made to `http://<serveraddress>:80` on to the ASP.NET Core app running on Kestrel at `http://127.0.0.1:5000`.</span></span> <span data-ttu-id="fa99d-194">그러나 Nginx는 Kestrel 프로세스를 관리하도록 설정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-194">However, Nginx isn't set up to manage the Kestrel process.</span></span> <span data-ttu-id="fa99d-195">*systemd*를 사용하여 기본 웹앱을 시작 및 모니터링하기 위한 서비스 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-195">*systemd* can be used to create a service file to start and monitor the underlying web app.</span></span> <span data-ttu-id="fa99d-196">*systemd*는 프로세스를 시작, 중지 및 관리하기 위한 다양하고 강력한 기능을 제공하는 init 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-196">*systemd* is an init system that provides many powerful features for starting, stopping, and managing processes.</span></span> 

### <a name="create-the-service-file"></a><span data-ttu-id="fa99d-197">서비스 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="fa99d-197">Create the service file</span></span>

<span data-ttu-id="fa99d-198">서비스 정의 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-198">Create the service definition file:</span></span>

```bash
sudo nano /etc/systemd/system/kestrel-hellomvc.service
```

<span data-ttu-id="fa99d-199">앱에 대한 예제 서비스 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-199">The following is an example service file for the app:</span></span>

```ini
[Unit]
Description=Example .NET Web API App running on Ubuntu

[Service]
WorkingDirectory=/var/aspnetcore/hellomvc
ExecStart=/usr/bin/dotnet /var/aspnetcore/hellomvc/hellomvc.dll
Restart=always
# Restart service after 10 seconds if the dotnet service crashes:
RestartSec=10
SyslogIdentifier=dotnet-example
User=www-data
Environment=ASPNETCORE_ENVIRONMENT=Production
Environment=DOTNET_PRINT_TELEMETRY_MESSAGE=false

[Install]
WantedBy=multi-user.target
```

<span data-ttu-id="fa99d-200">사용자 *www-data*가 구성에서 사용되지 않을 경우 여기서 정의된 사용자를 먼저 만들고 파일에 대한 적절한 소유권을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-200">If the user *www-data* isn't used by the configuration, the user defined here must be created first and given proper ownership for files.</span></span>

<span data-ttu-id="fa99d-201">Linux에는 대/소문자를 구분하는 파일 시스템이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-201">Linux has a case-sensitive file system.</span></span> <span data-ttu-id="fa99d-202">ASPNETCORE_ENVIRONMENT를 “프로덕션”으로 설정하면 *appsettings.production.json* 대신 구성 파일 *appsettings.Production.json*을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-202">Setting ASPNETCORE_ENVIRONMENT to "Production" results in searching for the configuration file *appsettings.Production.json*, not *appsettings.production.json*.</span></span>

> [!NOTE]
> <span data-ttu-id="fa99d-203">일부 값(예: SQL 연결 문자열)은 환경 변수를 읽기 위해 구성 공급자에 대해 이스케이프되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-203">Some values (for example, SQL connection strings) must be escaped for the configuration providers to read the environment variables.</span></span> <span data-ttu-id="fa99d-204">다음 명령을 사용하여 구성 파일에서 사용할 제대로 이스케이프된 값을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-204">Use the following command to generate a properly escaped value for use in the configuration file:</span></span>
>
> ```console
> systemd-escape "<value-to-escape>"
> ```

<span data-ttu-id="fa99d-205">파일을 저장하고 서비스를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-205">Save the file and enable the service.</span></span>

```bash
systemctl enable kestrel-hellomvc.service
```

<span data-ttu-id="fa99d-206">서비스를 시작하고 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-206">Start the service and verify that it's running.</span></span>

```
systemctl start kestrel-hellomvc.service
systemctl status kestrel-hellomvc.service

● kestrel-hellomvc.service - Example .NET Web API App running on Ubuntu
    Loaded: loaded (/etc/systemd/system/kestrel-hellomvc.service; enabled)
    Active: active (running) since Thu 2016-10-18 04:09:35 NZDT; 35s ago
Main PID: 9021 (dotnet)
    CGroup: /system.slice/kestrel-hellomvc.service
            └─9021 /usr/local/bin/dotnet /var/aspnetcore/hellomvc/hellomvc.dll
```

<span data-ttu-id="fa99d-207">역방향 프록시를 구성하고 systemd를 통해 Kestrel을 관리하면 웹앱이 완전히 구성되고 로컬 컴퓨터(`http://localhost`)의 브라우저에서 웹앱에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-207">With the reverse proxy configured and Kestrel managed through systemd, the web app is fully configured and can be accessed from a browser on the local machine at `http://localhost`.</span></span> <span data-ttu-id="fa99d-208">차단 중인 방화벽이 없다면 원격 컴퓨터에서 액세스할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-208">It's also accessible from a remote machine, barring any firewall that might be blocking.</span></span> <span data-ttu-id="fa99d-209">응답 헤더를 검사하는 `Server` 헤더는 Kestrel에서 지원하는 ASP.NET Core 앱을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-209">Inspecting the response headers, the `Server` header shows the ASP.NET Core app being served by Kestrel.</span></span>

```text
HTTP/1.1 200 OK
Date: Tue, 11 Oct 2016 16:22:23 GMT
Server: Kestrel
Keep-Alive: timeout=5, max=98
Connection: Keep-Alive
Transfer-Encoding: chunked
```

### <a name="viewing-logs"></a><span data-ttu-id="fa99d-210">로그 보기</span><span class="sxs-lookup"><span data-stu-id="fa99d-210">Viewing logs</span></span>

<span data-ttu-id="fa99d-211">Kestrel을 사용하는 웹앱은 `systemd`를 사용하여 관리되므로 모든 이벤트 및 프로세스가 중앙형 저널에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-211">Since the web app using Kestrel is managed using `systemd`, all events and processes are logged to a centralized journal.</span></span> <span data-ttu-id="fa99d-212">그러나 이 저널에는 `systemd`를 통해 관리하는 모든 서비스 및 프로세스에 대한 모든 항목이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-212">However, this journal includes all entries for all services and processes managed by `systemd`.</span></span> <span data-ttu-id="fa99d-213">`kestrel-hellomvc.service` 관련 항목을 보려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-213">To view the `kestrel-hellomvc.service`-specific items, use the following command:</span></span>

```bash
sudo journalctl -fu kestrel-hellomvc.service
```

<span data-ttu-id="fa99d-214">추가 필터링을 위해 `--since today`, `--until 1 hour ago` 같은 시간 옵션이나 이러한 옵션의 조합을 사용하여 반환되는 항목 수를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-214">For further filtering, time options such as `--since today`, `--until 1 hour ago` or a combination of these can reduce the amount of entries returned.</span></span>

```bash
sudo journalctl -fu kestrel-hellomvc.service --since "2016-10-18" --until "2016-10-18 04:00"
```

## <a name="data-protection"></a><span data-ttu-id="fa99d-215">데이터 보호</span><span class="sxs-lookup"><span data-stu-id="fa99d-215">Data protection</span></span>

<span data-ttu-id="fa99d-216">[ASP.NET Core 데이터 보호 스택](xref:security/data-protection/index)은 인증 미들웨어(예: 쿠키 미들웨어) 및 CSRF(교차 사이트 요청 위조) 보호를 비롯한 여러 ASP.NET Core [미들웨어](xref:fundamentals/middleware/index)에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-216">The [ASP.NET Core Data Protection stack](xref:security/data-protection/index) is used by several ASP.NET Core [middlewares](xref:fundamentals/middleware/index), including authentication middleware (for example, cookie middleware) and cross-site request forgery (CSRF) protections.</span></span> <span data-ttu-id="fa99d-217">사용자 코드에서 데이터 보호 API가 호출되지 않더라도 영구적 암호화 [키 저장소](xref:security/data-protection/implementation/key-management)를 만들도록 데이터 보호를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-217">Even if Data Protection APIs aren't called by user code, data protection should be configured to create a persistent cryptographic [key store](xref:security/data-protection/implementation/key-management).</span></span> <span data-ttu-id="fa99d-218">데이터 보호를 구성하지 않으면 키는 메모리에 보관되고 앱이 다시 시작되면 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-218">If data protection isn't configured, the keys are held in memory and discarded when the app restarts.</span></span>

<span data-ttu-id="fa99d-219">키 링이 메모리에 저장된 경우 앱을 다시 시작하면 다음과 같이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-219">If the key ring is stored in memory when the app restarts:</span></span>

* <span data-ttu-id="fa99d-220">모든 쿠키 기반 인증 토큰이 무효화됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-220">All cookie-based authentication tokens are invalidated.</span></span>
* <span data-ttu-id="fa99d-221">사용자는 다음 요청에서 다시 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-221">Users are required to sign in again on their next request.</span></span>
* <span data-ttu-id="fa99d-222">키 링으로 보호된 데이터의 암호를 더 이상 해독할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-222">Any data protected with the key ring can no longer be decrypted.</span></span> <span data-ttu-id="fa99d-223">여기에는 [CSRF 토큰](xref:security/anti-request-forgery#aspnet-core-antiforgery-configuration) 및 [ASP.NET Core MVC TempData 쿠키](xref:fundamentals/app-state#tempdata)가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-223">This may include [CSRF tokens](xref:security/anti-request-forgery#aspnet-core-antiforgery-configuration) and [ASP.NET Core MVC TempData cookies](xref:fundamentals/app-state#tempdata).</span></span>

<span data-ttu-id="fa99d-224">키 링을 유지하고 암호화하도록 데이터 보호를 구성하려면 다음을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="fa99d-224">To configure data protection to persist and encrypt the key ring, see:</span></span>

* <xref:security/data-protection/implementation/key-storage-providers>
* <xref:security/data-protection/implementation/key-encryption-at-rest>

## <a name="securing-the-app"></a><span data-ttu-id="fa99d-225">앱 보안</span><span class="sxs-lookup"><span data-stu-id="fa99d-225">Securing the app</span></span>

### <a name="enable-apparmor"></a><span data-ttu-id="fa99d-226">AppArmor 사용</span><span class="sxs-lookup"><span data-stu-id="fa99d-226">Enable AppArmor</span></span>

<span data-ttu-id="fa99d-227">LSM(Linux Security Modules)은 Linux 2.6 이후 Linux 커널에 포함된 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-227">Linux Security Modules (LSM) is a framework that's part of the Linux kernel since Linux 2.6.</span></span> <span data-ttu-id="fa99d-228">LSM은 보안 모듈의 다양한 구현을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-228">LSM supports different implementations of security modules.</span></span> <span data-ttu-id="fa99d-229">[AppArmor](https://wiki.ubuntu.com/AppArmor)는 프로그램을 제한된 리소스 집합으로 한정할 수 있는 필수 Access Control 시스템을 구현하는 LSM입니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-229">[AppArmor](https://wiki.ubuntu.com/AppArmor) is a LSM that implements a Mandatory Access Control system which allows confining the program to a limited set of resources.</span></span> <span data-ttu-id="fa99d-230">AppArmor가 사용하도록 설정되고 제대로 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-230">Ensure AppArmor is enabled and properly configured.</span></span>

### <a name="configuring-the-firewall"></a><span data-ttu-id="fa99d-231">방화벽 구성</span><span class="sxs-lookup"><span data-stu-id="fa99d-231">Configuring the firewall</span></span>

<span data-ttu-id="fa99d-232">사용되지 않는 모든 외부 포트를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-232">Close off all external ports that are not in use.</span></span> <span data-ttu-id="fa99d-233">복잡하지 않은 방화벽(ufw)은 방화벽을 구성하기 위한 명령줄 인터페이스를 제공하여 `iptables`에 대한 프런트 엔드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-233">Uncomplicated firewall (ufw) provides a front end for `iptables` by providing a command line interface for configuring the firewall.</span></span>

> [!WARNING]
> <span data-ttu-id="fa99d-234">방화벽이 올바르게 구성되지 않으면 전체 시스템에 대한 액세스가 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-234">A firewall will prevent access to the whole system if not configured correctly.</span></span> <span data-ttu-id="fa99d-235">올바른 SSH 포트를 지정하지 못하면 SSH를 사용하여 시스템에 연결하는 경우 실직적으로 시스템에 액세스할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-235">Failure to specify the correct SSH port will effectively lock you out of the system if you are using SSH to connect to it.</span></span> <span data-ttu-id="fa99d-236">기본 포트는 22입니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-236">The default port is 22.</span></span> <span data-ttu-id="fa99d-237">자세한 내용은 [ufw 소개](https://help.ubuntu.com/community/UFW) 및 [매뉴얼](http://manpages.ubuntu.com/manpages/bionic/man8/ufw.8.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fa99d-237">For more information, see the [introduction to ufw](https://help.ubuntu.com/community/UFW) and the [manual](http://manpages.ubuntu.com/manpages/bionic/man8/ufw.8.html).</span></span>

<span data-ttu-id="fa99d-238">`ufw`를 설치하고 필요한 모든 포트에서 트래픽을 허용하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-238">Install `ufw` and configure it to allow traffic on any ports needed.</span></span>

```bash
sudo apt-get install ufw

sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp

sudo ufw enable
```

### <a name="securing-nginx"></a><span data-ttu-id="fa99d-239">Nginx 보안</span><span class="sxs-lookup"><span data-stu-id="fa99d-239">Securing Nginx</span></span>

#### <a name="change-the-nginx-response-name"></a><span data-ttu-id="fa99d-240">Nginx 응답 이름 변경</span><span class="sxs-lookup"><span data-stu-id="fa99d-240">Change the Nginx response name</span></span>

<span data-ttu-id="fa99d-241">*src/http/ngx_http_header_filter_module.c*를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-241">Edit *src/http/ngx_http_header_filter_module.c*:</span></span>

```c
static char ngx_http_server_string[] = "Server: Web Server" CRLF;
static char ngx_http_server_full_string[] = "Server: Web Server" CRLF;
```

#### <a name="configure-options"></a><span data-ttu-id="fa99d-242">옵션 구성</span><span class="sxs-lookup"><span data-stu-id="fa99d-242">Configure options</span></span>

<span data-ttu-id="fa99d-243">추가 필수 모듈을 사용하여 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-243">Configure the server with additional required modules.</span></span> <span data-ttu-id="fa99d-244">[ModSecurity](https://www.modsecurity.org/)와 같은 웹앱 방화벽을 사용하여 앱을 강화해 보세요.</span><span class="sxs-lookup"><span data-stu-id="fa99d-244">Consider using a web app firewall, such as [ModSecurity](https://www.modsecurity.org/), to harden the app.</span></span>

#### <a name="configure-ssl"></a><span data-ttu-id="fa99d-245">SSL 구성</span><span class="sxs-lookup"><span data-stu-id="fa99d-245">Configure SSL</span></span>

* <span data-ttu-id="fa99d-246">신뢰할 수 있는 CA(인증 기관)에서 발급된 유효한 인증서를 지정하여 포트 `443`에서 HTTPS 트래픽을 수신 대기하도록 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-246">Configure the server to listen to HTTPS traffic on port `443` by specifying a valid certificate issued by a trusted Certificate Authority (CA).</span></span>

* <span data-ttu-id="fa99d-247">다음 */etc/nginx/nginx.conf* 파일에 설명된 일부 사례를 채택하여 보안을 강화합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-247">Harden the security by employing some of the practices depicted in the following */etc/nginx/nginx.conf* file.</span></span> <span data-ttu-id="fa99d-248">예를 들어 더 강력한 암호화를 선택하고 HTTP를 사용한 모든 트래픽을 HTTPS로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-248">Examples include choosing a stronger cipher and redirecting all traffic over HTTP to HTTPS.</span></span>

* <span data-ttu-id="fa99d-249">HSTS(`HTTP Strict-Transport-Security`) 헤더를 추가하면 클라이언트에서 만든 모든 후속 요청에 HTTPS만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-249">Adding an `HTTP Strict-Transport-Security` (HSTS) header ensures all subsequent requests made by the client are over HTTPS only.</span></span>

* <span data-ttu-id="fa99d-250">Strict-Transport-Security 헤더를 추가하지 않거나, 나중에 SSL을 사용하지 않도록 설정할 경우 적절한 `max-age`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-250">Don't add the Strict-Transport-Security header or chose an appropriate `max-age` if SSL will be disabled in the future.</span></span>

<span data-ttu-id="fa99d-251">*/etc/nginx/proxy.conf* 구성 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-251">Add the */etc/nginx/proxy.conf* configuration file:</span></span>

[!code-nginx[](linux-nginx/proxy.conf)]

<span data-ttu-id="fa99d-252">*/etc/nginx/nginx.conf* 구성 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-252">Edit the */etc/nginx/nginx.conf* configuration file.</span></span> <span data-ttu-id="fa99d-253">예제에서는 `http` 및 `server` 섹션이 하나의 구성 파일에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-253">The example contains both `http` and `server` sections in one configuration file.</span></span>

[!code-nginx[](linux-nginx/nginx.conf?highlight=2)]

#### <a name="secure-nginx-from-clickjacking"></a><span data-ttu-id="fa99d-254">클릭재킹(clickjacking)으로부터 Nginx 보호</span><span class="sxs-lookup"><span data-stu-id="fa99d-254">Secure Nginx from clickjacking</span></span>
<span data-ttu-id="fa99d-255">클릭재킹은 감염된 사용자의 클릭을 수집하는 악의적인 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-255">Clickjacking is a malicious technique to collect an infected user's clicks.</span></span> <span data-ttu-id="fa99d-256">클릭재킹은 희생자(방문자)를 속여서 감염된 사이트를 클릭하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-256">Clickjacking tricks the victim (visitor) into clicking on an infected site.</span></span> <span data-ttu-id="fa99d-257">X-FRAME-OPTIONS를 사용하여 사이트를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-257">Use X-FRAME-OPTIONS to secure the site.</span></span>

<span data-ttu-id="fa99d-258">*nginx.conf* 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-258">Edit the *nginx.conf* file:</span></span>

```bash
sudo nano /etc/nginx/nginx.conf
```

<span data-ttu-id="fa99d-259">줄 `add_header X-Frame-Options "SAMEORIGIN";`을 추가하고 파일을 저장한 다음 Nginx를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-259">Add the line `add_header X-Frame-Options "SAMEORIGIN";` and save the file, then restart Nginx.</span></span>

#### <a name="mime-type-sniffing"></a><span data-ttu-id="fa99d-260">MIME 형식 검색</span><span class="sxs-lookup"><span data-stu-id="fa99d-260">MIME-type sniffing</span></span>

<span data-ttu-id="fa99d-261">이 헤더는 응답 콘텐츠 형식을 재정의하지 않도록 브라우저에 지시하므로 대부분의 브라우저에서 선언된 콘텐츠 형식이 아닌 응답에 대한 MIME 검색을 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-261">This header prevents most browsers from MIME-sniffing a response away from the declared content type, as the header instructs the browser not to override the response content type.</span></span> <span data-ttu-id="fa99d-262">`nosniff` 옵션을 사용하면 서버에 콘텐츠가 “text/html”이라고 표시될 경우 브라우저는 콘텐츠를 “text/html”으로 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-262">With the `nosniff` option, if the server says the content is "text/html", the browser renders it as "text/html".</span></span>

<span data-ttu-id="fa99d-263">*nginx.conf* 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-263">Edit the *nginx.conf* file:</span></span>

```bash
sudo nano /etc/nginx/nginx.conf
```

<span data-ttu-id="fa99d-264">줄 `add_header X-Content-Type-Options "nosniff";`를 추가하고 파일을 저장한 다음 Nginx를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fa99d-264">Add the line `add_header X-Content-Type-Options "nosniff";` and save the file, then restart Nginx.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fa99d-265">추가 자료</span><span class="sxs-lookup"><span data-stu-id="fa99d-265">Additional resources</span></span>

* [<span data-ttu-id="fa99d-266">Nginx: 이진 릴리스: 공식 Debian/Ubuntu 패키지</span><span class="sxs-lookup"><span data-stu-id="fa99d-266">Nginx: Binary Releases: Official Debian/Ubuntu packages</span></span>](https://www.nginx.com/resources/wiki/start/topics/tutorials/install/#official-debian-ubuntu-packages)
* [<span data-ttu-id="fa99d-267">프록시 서버 및 부하 분산 장치를 사용하도록 ASP.NET Core 구성</span><span class="sxs-lookup"><span data-stu-id="fa99d-267">Configure ASP.NET Core to work with proxy servers and load balancers</span></span>](xref:host-and-deploy/proxy-load-balancer)
* [<span data-ttu-id="fa99d-268">NGINX: 전달된 헤더 사용</span><span class="sxs-lookup"><span data-stu-id="fa99d-268">NGINX: Using the Forwarded header</span></span>](https://www.nginx.com/resources/wiki/start/topics/examples/forwarded/)
