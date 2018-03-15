---
title: "Nginx를 사용하여 Linux에서 ASP.NET Core 호스트"
author: rick-anderson
description: "Ubuntu 16.04 Kestrel에서 실행 되는 ASP.NET Core 웹 앱에 대 한 HTTP 트래픽을 전달 하도록에 역방향 프록시로 Nginx를 설정 하는 방법을 설명 합니다."
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 03/13/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/linux-nginx
ms.openlocfilehash: a1de177fcd41c925a85e5aab9a0d236249b7da0b
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="host-aspnet-core-on-linux-with-nginx"></a><span data-ttu-id="80674-103">Nginx를 사용하여 Linux에서 ASP.NET Core 호스트</span><span class="sxs-lookup"><span data-stu-id="80674-103">Host ASP.NET Core on Linux with Nginx</span></span>

<span data-ttu-id="80674-104">작성자: [Sourabh Shirhatti](https://twitter.com/sshirhatti)</span><span class="sxs-lookup"><span data-stu-id="80674-104">By [Sourabh Shirhatti](https://twitter.com/sshirhatti)</span></span>

<span data-ttu-id="80674-105">이 가이드에서는 Ubuntu 16.04 Server에서 프로덕션 준비 ASP.NET Core 환경을 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-105">This guide explains setting up a production-ready ASP.NET Core environment on an Ubuntu 16.04 Server.</span></span>

> [!NOTE]
> <span data-ttu-id="80674-106">Ubuntu 14.04에 대 한 *supervisord* Kestrel 프로세스를 모니터링 하기 위한 솔루션으로 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="80674-106">For Ubuntu 14.04, *supervisord* is recommended as a solution for monitoring the Kestrel process.</span></span> <span data-ttu-id="80674-107">*systemd* Ubuntu 14.04에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="80674-107">*systemd* isn't available on Ubuntu 14.04.</span></span> <span data-ttu-id="80674-108">[이 문서의 이전 버전 참조](https://github.com/aspnet/Docs/blob/e9c1419175c4dd7e152df3746ba1df5935aaafd5/aspnetcore/publishing/linuxproduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-108">[See previous version of this document](https://github.com/aspnet/Docs/blob/e9c1419175c4dd7e152df3746ba1df5935aaafd5/aspnetcore/publishing/linuxproduction.md).</span></span>

<span data-ttu-id="80674-109">이 가이드의 내용:</span><span class="sxs-lookup"><span data-stu-id="80674-109">This guide:</span></span>

* <span data-ttu-id="80674-110">역방향 프록시 서버로 보호 하는 기존 ASP.NET Core 응용 프로그램을 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-110">Places an existing ASP.NET Core app behind a reverse proxy server.</span></span>
* <span data-ttu-id="80674-111">Kestrel 웹 서버에 요청 전달 하는 역방향 프록시 서버를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-111">Sets up the reverse proxy server to forward requests to the Kestrel web server.</span></span>
* <span data-ttu-id="80674-112">디먼 시작 시에 실행 하는 웹 응용 프로그램을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-112">Ensures the web app runs on startup as a daemon.</span></span>
* <span data-ttu-id="80674-113">웹 앱을 다시 시작 하려면 프로세스 관리 도구를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-113">Configures a process management tool to help restart the web app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80674-114">전제 조건</span><span class="sxs-lookup"><span data-stu-id="80674-114">Prerequisites</span></span>

1. <span data-ttu-id="80674-115">sudo 권한을 가진 표준 사용자 계정으로 Ubuntu 16.04 Server에 액세스</span><span class="sxs-lookup"><span data-stu-id="80674-115">Access to an Ubuntu 16.04 Server with a standard user account with sudo privilege</span></span>
1. <span data-ttu-id="80674-116">기존 ASP.NET Core 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="80674-116">An existing ASP.NET Core app</span></span>

## <a name="copy-over-the-app"></a><span data-ttu-id="80674-117">응용 프로그램을 통해 복사</span><span class="sxs-lookup"><span data-stu-id="80674-117">Copy over the app</span></span>

<span data-ttu-id="80674-118">실행 [dotnet 게시](/dotnet/core/tools/dotnet-publish) 서버에서 실행할 수 있는 자체 포함 된 디렉터리에 응용 프로그램을 패키징할 개발 환경에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-118">Run [dotnet publish](/dotnet/core/tools/dotnet-publish) from the dev environment to package an app into a self-contained directory that can run on the server.</span></span>

<span data-ttu-id="80674-119">ASP.NET Core 응용 프로그램 (예: SCP, FTP) 조직의 워크플로로 통합 하는 어떤 도구를 사용 하 여 서버에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-119">Copy the ASP.NET Core app to the server using whatever tool integrates into the organization's workflow (for example, SCP, FTP).</span></span> <span data-ttu-id="80674-120">다음과 같이 앱을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-120">Test the app, for example:</span></span>

* <span data-ttu-id="80674-121">명령줄에서 실행 `dotnet <app_assembly>.dll`합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-121">From the command line, run `dotnet <app_assembly>.dll`.</span></span>
* <span data-ttu-id="80674-122">브라우저에서 `http://<serveraddress>:<port>`로 이동하여 앱이 Linux에서 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-122">In a browser, navigate to `http://<serveraddress>:<port>` to verify the app works on Linux.</span></span> 
 
## <a name="configure-a-reverse-proxy-server"></a><span data-ttu-id="80674-123">역방향 프록시 서버 구성</span><span class="sxs-lookup"><span data-stu-id="80674-123">Configure a reverse proxy server</span></span>

<span data-ttu-id="80674-124">역방향 프록시는 동적 웹 앱을 처리 하기 위한 일반적인 설치.</span><span class="sxs-lookup"><span data-stu-id="80674-124">A reverse proxy is a common setup for serving dynamic web apps.</span></span> <span data-ttu-id="80674-125">역방향 프록시는 HTTP 요청을 종료 하 고 ASP.NET Core 응용 프로그램에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-125">A reverse proxy terminates the HTTP request and forwards it to the ASP.NET Core app.</span></span>

### <a name="why-use-a-reverse-proxy-server"></a><span data-ttu-id="80674-126">역방향 프록시 서버를 사용하는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="80674-126">Why use a reverse proxy server?</span></span>

<span data-ttu-id="80674-127">Kestrel은 ASP.NET Core에서 동적 콘텐츠를 처리 하기 위한 훌륭한입니다.</span><span class="sxs-lookup"><span data-stu-id="80674-127">Kestrel is great for serving dynamic content from ASP.NET Core.</span></span> <span data-ttu-id="80674-128">그러나 웹 서비스 기능으로 IIS, Apache 또는 Nginx 등의 서버 기능 풍부한으로 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="80674-128">However, the web serving capabilities aren't as feature rich as servers such as IIS, Apache, or Nginx.</span></span> <span data-ttu-id="80674-129">역방향 프록시 서버는 정적 콘텐츠를 처리, 요청을 캐시 하 고, 요청, 및 HTTP 서버에서 SSL 종료를 압축 하는 등의 작업을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80674-129">A reverse proxy server can offload work such as serving static content, caching requests, compressing requests, and SSL termination from the HTTP server.</span></span> <span data-ttu-id="80674-130">역방향 프록시 서버는 전용 컴퓨터에 있거나 HTTP 서버와 함께 배포될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80674-130">A reverse proxy server may reside on a dedicated machine or may be deployed alongside an HTTP server.</span></span>

<span data-ttu-id="80674-131">이 가이드에서는 Nginx의 단일 인스턴스가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="80674-131">For the purposes of this guide, a single instance of Nginx is used.</span></span> <span data-ttu-id="80674-132">이 인스턴스는 HTTP 서버와 함께 동일한 서버에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="80674-132">It runs on the same server, alongside the HTTP server.</span></span> <span data-ttu-id="80674-133">요구 사항에 따라 다른 설치 프로그램을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80674-133">Based on requirements, a different setup may be chosen.</span></span>

<span data-ttu-id="80674-134">전달 헤더 미들웨어를 사용 하 여 요청 역방향 프록시를 전달 하기 때문에 [Microsoft.AspNetCore.HttpOverrides](https://www.nuget.org/packages/Microsoft.AspNetCore.HttpOverrides/) 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-134">Because requests are forwarded by reverse proxy, use the Forwarded Headers Middleware from the [Microsoft.AspNetCore.HttpOverrides](https://www.nuget.org/packages/Microsoft.AspNetCore.HttpOverrides/) package.</span></span> <span data-ttu-id="80674-135">미들웨어 업데이트는 `Request.Scheme`를 사용 하 여는 `X-Forwarded-Proto` 헤더로, 해당 리디렉션 Uri 및 기타 보안 정책을 올바르게 작동 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-135">The middleware updates the `Request.Scheme`, using the `X-Forwarded-Proto` header, so that redirect URIs and other security policies work correctly.</span></span>

<span data-ttu-id="80674-136">모든 종류의 인증 미들웨어를 사용 하 여 전달 헤더 미들웨어 첫 번째 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-136">When using any type of authentication middleware, the Forwarded Headers Middleware must run first.</span></span> <span data-ttu-id="80674-137">이 순서 지정 하면 인증 미들웨어 헤더 값을 사용 하 고 올바른 리디렉션 Uri를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80674-137">This ordering ensures that the authentication middleware can consume the header values and generate correct redirect URIs.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="80674-138">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="80674-138">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="80674-139">호출 된 [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) 에서 메서드 `Startup.Configure` 호출 하기 전에 [UseAuthentication](/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication) 또는 유사한 인증 체계 미들웨어:</span><span class="sxs-lookup"><span data-stu-id="80674-139">Invoke the [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) method in `Startup.Configure` before calling [UseAuthentication](/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication) or similar authentication scheme middleware:</span></span>

```csharp
app.UseForwardedHeaders(new ForwardedHeadersOptions
{
    ForwardedHeaders = ForwardedHeaders.XForwardedFor | ForwardedHeaders.XForwardedProto
});

app.UseAuthentication();
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="80674-140">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="80674-140">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="80674-141">호출 된 [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) 에서 메서드 `Startup.Configure` 호출 하기 전에 [UseIdentity](/dotnet/api/microsoft.aspnetcore.builder.builderextensions.useidentity) 및 [UseFacebookAuthentication](/dotnet/api/microsoft.aspnetcore.builder.facebookappbuilderextensions.usefacebookauthentication) 또는 유사한 인증 체계 미들웨어:</span><span class="sxs-lookup"><span data-stu-id="80674-141">Invoke the [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) method in `Startup.Configure` before calling [UseIdentity](/dotnet/api/microsoft.aspnetcore.builder.builderextensions.useidentity) and [UseFacebookAuthentication](/dotnet/api/microsoft.aspnetcore.builder.facebookappbuilderextensions.usefacebookauthentication) or similar authentication scheme middleware:</span></span>

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

<span data-ttu-id="80674-142">없는 경우 [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions) 전달 하도록 기본 헤더는 미들웨어를 지정 된 `None`합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-142">If no [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions) are specified to the middleware, the default headers to forward are `None`.</span></span>

### <a name="install-nginx"></a><span data-ttu-id="80674-143">Nginx 설치</span><span class="sxs-lookup"><span data-stu-id="80674-143">Install Nginx</span></span>

```bash
sudo apt-get install nginx
```

> [!NOTE]
> <span data-ttu-id="80674-144">선택적 Nginx 모듈 설치 되는 경우에 원본에서 Nginx 구축 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80674-144">If optional Nginx modules will be installed, building Nginx from source might be required.</span></span>

<span data-ttu-id="80674-145">`apt-get`을 사용하여 Nginx를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-145">Use `apt-get` to install Nginx.</span></span> <span data-ttu-id="80674-146">설치 관리자는 시스템 시작 시 Nginx를 디먼으로 실행하는 System V init 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="80674-146">The installer creates a System V init script that runs Nginx as daemon on system startup.</span></span> <span data-ttu-id="80674-147">Nginx가 처음 설치되었으므로 다음을 실행하여 명시적으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-147">Since Nginx was installed for the first time, explicitly start it by running:</span></span>

```bash
sudo service nginx start
```

<span data-ttu-id="80674-148">브라우저에 Nginx에 대한 기본 방문 페이지가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-148">Verify a browser displays the default landing page for Nginx.</span></span>

### <a name="configure-nginx"></a><span data-ttu-id="80674-149">Nginx 구성</span><span class="sxs-lookup"><span data-stu-id="80674-149">Configure Nginx</span></span>

<span data-ttu-id="80674-150">요청을 전달 ASP.NET Core 응용 프로그램에 역방향 프록시로 Nginx을 구성 하려면 수정 */etc/nginx/sites-available/default*합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-150">To configure Nginx as a reverse proxy to forward requests to your ASP.NET Core app, modify */etc/nginx/sites-available/default*.</span></span> <span data-ttu-id="80674-151">텍스트 편집기에서 해당 항목을 열고 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="80674-151">Open it in a text editor, and replace the contents with the following:</span></span>

```nginx
server {
    listen        80;
    server_name   example.com *.example.com;
    location / {
        proxy_pass         http://localhost:5000;
        proxy_http_version 1.1;
        proxy_set_header   Upgrade $http_upgrade;
        proxy_set_header   Connection keep-alive;
        proxy_set_header   Host $http_host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

<span data-ttu-id="80674-152">No `server_name` 일치 Nginx 기본 서버를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-152">When no `server_name` matches, Nginx uses the default server.</span></span> <span data-ttu-id="80674-153">기본 서버 정의 된 경우 구성 파일에서 첫 번째 서버는 기본 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="80674-153">If no default server is defined, the first server in the configuration file is the default server.</span></span> <span data-ttu-id="80674-154">모범 사례로, 구성 파일에 444의 상태 코드를 반환 하는 특정 기본 서버를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-154">As a best practice, add a specific default server which returns a status code of 444 in your configuration file.</span></span> <span data-ttu-id="80674-155">다음은 기본 서버 구성 예가입니다.</span><span class="sxs-lookup"><span data-stu-id="80674-155">A default server configuration example is:</span></span>

```nginx
server {
    listen   80 default_server;
    # listen [::]:80 default_server deferred;
    return   444;
}
```

<span data-ttu-id="80674-156">위의 구성 파일 및 기본 서버와 Nginx 허용 호스트 헤더를 사용 하 여 포트 80에서 공용 트래픽을 `example.com` 또는 `*.example.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-156">With the preceding configuration file and default server, Nginx accepts public traffic on port 80 with host header `example.com` or `*.example.com`.</span></span> <span data-ttu-id="80674-157">이러한 호스트와 일치 하지 않는 요청 Kestrel에 경고가 전달 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="80674-157">Requests not matching these hosts won't get forwarded to Kestrel.</span></span> <span data-ttu-id="80674-158">일치 하는 요청에 Kestrel을 전달 하는 Nginx `http://localhost:5000`합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-158">Nginx forwards the matching requests to Kestrel at `http://localhost:5000`.</span></span> <span data-ttu-id="80674-159">참조 [nginx 요청을 처리 하는 방법을](https://nginx.org/docs/http/request_processing.html) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-159">See [How nginx processes a request](https://nginx.org/docs/http/request_processing.html) for more information.</span></span>

> [!WARNING]
> <span data-ttu-id="80674-160">적절 한 입력 하지 않으면 [server_name 지시문](https://nginx.org/docs/http/server_names.html) 보안 취약성이 있는 응용 프로그램을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-160">Failure to specify a proper [server_name directive](https://nginx.org/docs/http/server_names.html) exposes your app to security vulnerabilities.</span></span> <span data-ttu-id="80674-161">와일드 카드 바인딩 하위 도메인 (예를 들어 `*.example.com`) 전체 부모 도메인을 제어 하는 경우이 보안 위험을 노출 하지 않습니다 (반대인 `*.com`, 취약 한 변수인).</span><span class="sxs-lookup"><span data-stu-id="80674-161">Subdomain wildcard binding (for example, `*.example.com`) doesn't pose this security risk if you control the entire parent domain (as opposed to `*.com`, which is vulnerable).</span></span> <span data-ttu-id="80674-162">참조 [rfc7230 섹션 5.4](https://tools.ietf.org/html/rfc7230#section-5.4) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-162">See [rfc7230 section-5.4](https://tools.ietf.org/html/rfc7230#section-5.4) for more information.</span></span>

<span data-ttu-id="80674-163">Nginx 구성, 설정 되 면 실행 `sudo nginx -t` 구성 파일의 구문을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-163">Once the Nginx configuration is established, run `sudo nginx -t` to verify the syntax of the configuration files.</span></span> <span data-ttu-id="80674-164">구성 파일 테스트에 성공한 경우 강제로 실행 하 여 변경 내용을 적용 하려면 Nginx `sudo nginx -s reload`합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-164">If the configuration file test is successful, force Nginx to pick up the changes by running `sudo nginx -s reload`.</span></span>

## <a name="monitoring-the-app"></a><span data-ttu-id="80674-165">응용 프로그램 모니터링</span><span class="sxs-lookup"><span data-stu-id="80674-165">Monitoring the app</span></span>

<span data-ttu-id="80674-166">서버에 대 한 요청을 전달 하도록 설치가 `http://<serveraddress>:80` 에 Kestrel에서 실행 중인 ASP.NET Core 응용 프로그램에 로그온 `http://127.0.0.1:5000`합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-166">The server is setup to forward requests made to `http://<serveraddress>:80` on to the ASP.NET Core app running on Kestrel at `http://127.0.0.1:5000`.</span></span> <span data-ttu-id="80674-167">그러나 Nginx Kestrel 프로세스를 관리할 수를 설정 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="80674-167">However, Nginx isn't set up to manage the Kestrel process.</span></span> <span data-ttu-id="80674-168">*systemd* 시작 하 고 기본 웹 응용 프로그램 모니터링 서비스 파일을 만드는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80674-168">*systemd* can be used to create a service file to start and monitor the underlying web app.</span></span> <span data-ttu-id="80674-169">*systemd*는 프로세스를 시작, 중지 및 관리하기 위한 다양하고 강력한 기능을 제공하는 init 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="80674-169">*systemd* is an init system that provides many powerful features for starting, stopping, and managing processes.</span></span> 

### <a name="create-the-service-file"></a><span data-ttu-id="80674-170">서비스 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="80674-170">Create the service file</span></span>

<span data-ttu-id="80674-171">서비스 정의 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="80674-171">Create the service definition file:</span></span>

```bash
sudo nano /etc/systemd/system/kestrel-hellomvc.service
```

<span data-ttu-id="80674-172">다음은 응용 프로그램에 대 한 서비스 파일의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="80674-172">The following is an example service file for the app:</span></span>

```ini
[Unit]
Description=Example .NET Web API App running on Ubuntu

[Service]
WorkingDirectory=/var/aspnetcore/hellomvc
ExecStart=/usr/bin/dotnet /var/aspnetcore/hellomvc/hellomvc.dll
Restart=always
RestartSec=10  # Restart service after 10 seconds if dotnet service crashes
SyslogIdentifier=dotnet-example
User=www-data
Environment=ASPNETCORE_ENVIRONMENT=Production
Environment=DOTNET_PRINT_TELEMETRY_MESSAGE=false

[Install]
WantedBy=multi-user.target
```

<span data-ttu-id="80674-173">**참고:** 경우 사용자 *www 데이터* 사용 되지 않는 구성, 여기에 정의 된 사용자를 만든 다음 먼저 파일에 대 한 적절 한 소유권을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-173">**Note:** If the user *www-data* isn't used by the configuration, the user defined here must be created first and given proper ownership for files.</span></span>
<span data-ttu-id="80674-174">**참고:** Linux는 대/소문자 구분 파일 시스템이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80674-174">**Note:** Linux has a case-sensitive file system.</span></span> <span data-ttu-id="80674-175">구성 파일에 대 한 검색에 "Production"을로 ASPNETCORE_ENVIRONMENT 설정 *appsettings 합니다. Production.json*이 아니라 *appsettings.production.json*합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-175">Setting ASPNETCORE_ENVIRONMENT to "Production" results in searching for the configuration file *appsettings.Production.json*, not *appsettings.production.json*.</span></span>

<span data-ttu-id="80674-176">파일을 저장하고 서비스를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-176">Save the file and enable the service.</span></span>

```bash
systemctl enable kestrel-hellomvc.service
```

<span data-ttu-id="80674-177">서비스를 시작 하 고 실행 중인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-177">Start the service and verify that it's running.</span></span>

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

<span data-ttu-id="80674-178">된 역방향 프록시 구성 및 Kestrel systemd 통해 관리 되는 웹 응용 프로그램이 완전히 구성 된 하 고 브라우저에서 로컬 컴퓨터에서 액세스할 수 `http://localhost`합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-178">With the reverse proxy configured and Kestrel managed through systemd, the web app is fully configured and can be accessed from a browser on the local machine at `http://localhost`.</span></span> <span data-ttu-id="80674-179">막을 수 있는 모든 방화벽을 제한 하 여 원격 컴퓨터에서 액세스할 수 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-179">It's also accessible from a remote machine, barring any firewall that might be blocking.</span></span> <span data-ttu-id="80674-180">응답 헤더를 검사 하 여 `Server` 헤더 Kestrel에서 제공 하는 ASP.NET Core 응용 프로그램을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-180">Inspecting the response headers, the `Server` header shows the ASP.NET Core app being served by Kestrel.</span></span>

```text
HTTP/1.1 200 OK
Date: Tue, 11 Oct 2016 16:22:23 GMT
Server: Kestrel
Keep-Alive: timeout=5, max=98
Connection: Keep-Alive
Transfer-Encoding: chunked
```

### <a name="viewing-logs"></a><span data-ttu-id="80674-181">로그 보기</span><span class="sxs-lookup"><span data-stu-id="80674-181">Viewing logs</span></span>

<span data-ttu-id="80674-182">웹 앱 이후 Kestrel를 사용 하 여 관리를 사용 하 여 `systemd`, 모든 이벤트 및 프로세스 중앙 집중식된 저널에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80674-182">Since the web app using Kestrel is managed using `systemd`, all events and processes are logged to a centralized journal.</span></span> <span data-ttu-id="80674-183">그러나 이 저널에는 `systemd`를 통해 관리하는 모든 서비스 및 프로세스에 대한 모든 항목이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="80674-183">However, this journal includes all entries for all services and processes managed by `systemd`.</span></span> <span data-ttu-id="80674-184">`kestrel-hellomvc.service` 관련 항목을 보려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-184">To view the `kestrel-hellomvc.service`-specific items, use the following command:</span></span>

```bash
sudo journalctl -fu kestrel-hellomvc.service
```

<span data-ttu-id="80674-185">추가 필터링을 위해 `--since today`, `--until 1 hour ago` 같은 시간 옵션이나 이러한 옵션의 조합을 사용하여 반환되는 항목 수를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="80674-185">For further filtering, time options such as `--since today`, `--until 1 hour ago` or a combination of these can reduce the amount of entries returned.</span></span>

```bash
sudo journalctl -fu kestrel-hellomvc.service --since "2016-10-18" --until "2016-10-18 04:00"
```

## <a name="securing-the-app"></a><span data-ttu-id="80674-186">응용 프로그램 보안 설정</span><span class="sxs-lookup"><span data-stu-id="80674-186">Securing the app</span></span>

### <a name="enable-apparmor"></a><span data-ttu-id="80674-187">AppArmor 사용</span><span class="sxs-lookup"><span data-stu-id="80674-187">Enable AppArmor</span></span>

<span data-ttu-id="80674-188">Linux 보안 모듈 (LSM)는 Linux 2.6 이후 Linux 커널의 일부인 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="80674-188">Linux Security Modules (LSM) is a framework that's part of the Linux kernel since Linux 2.6.</span></span> <span data-ttu-id="80674-189">LSM은 보안 모듈의 다양한 구현을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-189">LSM supports different implementations of security modules.</span></span> <span data-ttu-id="80674-190">[AppArmor](https://wiki.ubuntu.com/AppArmor)는 프로그램을 제한된 리소스 집합으로 한정할 수 있는 필수 Access Control 시스템을 구현하는 LSM입니다.</span><span class="sxs-lookup"><span data-stu-id="80674-190">[AppArmor](https://wiki.ubuntu.com/AppArmor) is a LSM that implements a Mandatory Access Control system which allows confining the program to a limited set of resources.</span></span> <span data-ttu-id="80674-191">AppArmor가 사용하도록 설정되고 제대로 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-191">Ensure AppArmor is enabled and properly configured.</span></span>

### <a name="configuring-the-firewall"></a><span data-ttu-id="80674-192">방화벽 구성</span><span class="sxs-lookup"><span data-stu-id="80674-192">Configuring the firewall</span></span>

<span data-ttu-id="80674-193">사용되지 않는 모든 외부 포트를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="80674-193">Close off all external ports that are not in use.</span></span> <span data-ttu-id="80674-194">복잡하지 않은 방화벽(ufw)은 방화벽을 구성하기 위한 명령줄 인터페이스를 제공하여 `iptables`에 대한 프런트 엔드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-194">Uncomplicated firewall (ufw) provides a front end for `iptables` by providing a command line interface for configuring the firewall.</span></span> <span data-ttu-id="80674-195">확인 `ufw` 필요한 모든 포트에서 트래픽을 허용 하도록 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80674-195">Verify that `ufw` is configured to allow traffic on any ports needed.</span></span>

```bash
sudo apt-get install ufw
sudo ufw enable

sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
```

### <a name="securing-nginx"></a><span data-ttu-id="80674-196">Nginx 보안</span><span class="sxs-lookup"><span data-stu-id="80674-196">Securing Nginx</span></span>

<span data-ttu-id="80674-197">Nginx의 기본 배포 시에는 SSL이 사용하도록 설정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="80674-197">The default distribution of Nginx doesn't enable SSL.</span></span> <span data-ttu-id="80674-198">추가 보안 기능을 사용하도록 설정하려면 소스에서 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-198">To enable additional security features, build from source.</span></span>

#### <a name="download-the-source-and-install-the-build-dependencies"></a><span data-ttu-id="80674-199">소스 다운로드 및 빌드 종속성 설치</span><span class="sxs-lookup"><span data-stu-id="80674-199">Download the source and install the build dependencies</span></span>

```bash
# Install the build dependencies
sudo apt-get update
sudo apt-get install build-essential zlib1g-dev libpcre3-dev libssl-dev libxslt1-dev libxml2-dev libgd2-xpm-dev libgeoip-dev libgoogle-perftools-dev libperl-dev

# Download Nginx 1.10.0 or latest
wget http://www.nginx.org/download/nginx-1.10.0.tar.gz
tar zxf nginx-1.10.0.tar.gz
```

#### <a name="change-the-nginx-response-name"></a><span data-ttu-id="80674-200">Nginx 응답 이름 변경</span><span class="sxs-lookup"><span data-stu-id="80674-200">Change the Nginx response name</span></span>

<span data-ttu-id="80674-201">*src/http/ngx_http_header_filter_module.c*를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-201">Edit *src/http/ngx_http_header_filter_module.c*:</span></span>

```c
static char ngx_http_server_string[] = "Server: Web Server" CRLF;
static char ngx_http_server_full_string[] = "Server: Web Server" CRLF;
```

#### <a name="configure-the-options-and-build"></a><span data-ttu-id="80674-202">옵션 구성 및 빌드</span><span class="sxs-lookup"><span data-stu-id="80674-202">Configure the options and build</span></span>

<span data-ttu-id="80674-203">정규식의 경우 PCRE 라이브러리가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-203">The PCRE library is required for regular expressions.</span></span> <span data-ttu-id="80674-204">정규식은 ngx_http_rewrite_module에 대한 위치 지시문에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="80674-204">Regular expressions are used in the location directive for the ngx_http_rewrite_module.</span></span> <span data-ttu-id="80674-205">http_ssl_module은 HTTPS 프로토콜 지원을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-205">The http_ssl_module adds HTTPS protocol support.</span></span>

<span data-ttu-id="80674-206">와 같은 웹 응용 프로그램 방화벽을 사용 하는 것이 좋습니다. *ModSecurity* 강화 응용 프로그램 보안을 강화 합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-206">Consider using a web app firewall like *ModSecurity* to harden the app.</span></span>

```bash
./configure
--with-pcre=../pcre-8.38
--with-zlib=../zlib-1.2.8
--with-http_ssl_module
--with-stream
--with-mail=dynamic
```

#### <a name="configure-ssl"></a><span data-ttu-id="80674-207">SSL 구성</span><span class="sxs-lookup"><span data-stu-id="80674-207">Configure SSL</span></span>

* <span data-ttu-id="80674-208">HTTPS 트래픽에 포트에서 수신 하도록 서버 구성 `443` 신뢰할 수 있는 인증 기관 (CA)에서 발급 한 올바른 인증서를 지정 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-208">Configure the server to listen to HTTPS traffic on port `443` by specifying a valid certificate issued by a trusted Certificate Authority (CA).</span></span>

* <span data-ttu-id="80674-209">다음에서에 사용 된 사례 중 일부를 사용 하 여 보안을 강화 */etc/nginx/nginx.conf* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="80674-209">Harden the security by employing some of the practices depicted in the following */etc/nginx/nginx.conf* file.</span></span> <span data-ttu-id="80674-210">예를 들어 더 강력한 암호화를 선택하고 HTTP를 사용한 모든 트래픽을 HTTPS로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-210">Examples include choosing a stronger cipher and redirecting all traffic over HTTP to HTTPS.</span></span>

* <span data-ttu-id="80674-211">HSTS(`HTTP Strict-Transport-Security`) 헤더를 추가하면 클라이언트에서 만든 모든 후속 요청에 HTTPS만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="80674-211">Adding an `HTTP Strict-Transport-Security` (HSTS) header ensures all subsequent requests made by the client are over HTTPS only.</span></span>

* <span data-ttu-id="80674-212">적절 한 선택한 또는 Strict-전송-보안 헤더를 추가 하지 `max-age` 경우 SSL을 나중에 사용할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="80674-212">Don't add the Strict-Transport-Security header or chose an appropriate `max-age` if SSL will be disabled in the future.</span></span>

<span data-ttu-id="80674-213">*/etc/nginx/proxy.conf* 구성 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-213">Add the */etc/nginx/proxy.conf* configuration file:</span></span>

[!code-nginx[](linux-nginx/proxy.conf)]

<span data-ttu-id="80674-214">*/etc/nginx/nginx.conf* 구성 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-214">Edit the */etc/nginx/nginx.conf* configuration file.</span></span> <span data-ttu-id="80674-215">예제에서는 `http` 및 `server` 섹션이 하나의 구성 파일에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="80674-215">The example contains both `http` and `server` sections in one configuration file.</span></span>

[!code-nginx[](linux-nginx/nginx.conf?highlight=2)]

#### <a name="secure-nginx-from-clickjacking"></a><span data-ttu-id="80674-216">클릭재킹(clickjacking)으로부터 Nginx 보호</span><span class="sxs-lookup"><span data-stu-id="80674-216">Secure Nginx from clickjacking</span></span>
<span data-ttu-id="80674-217">클릭재킹은 감염된 사용자의 클릭을 수집하는 악의적인 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="80674-217">Clickjacking is a malicious technique to collect an infected user's clicks.</span></span> <span data-ttu-id="80674-218">클릭재킹은 희생자(방문자)를 속여서 감염된 사이트를 클릭하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-218">Clickjacking tricks the victim (visitor) into clicking on an infected site.</span></span> <span data-ttu-id="80674-219">X-프레임-옵션을 사용 사이트를 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-219">Use X-FRAME-OPTIONS to secure the site.</span></span>

<span data-ttu-id="80674-220">*nginx.conf* 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-220">Edit the *nginx.conf* file:</span></span>

```bash
sudo nano /etc/nginx/nginx.conf
```

<span data-ttu-id="80674-221">줄 `add_header X-Frame-Options "SAMEORIGIN";`을 추가하고 파일을 저장한 다음 Nginx를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-221">Add the line `add_header X-Frame-Options "SAMEORIGIN";` and save the file, then restart Nginx.</span></span>

#### <a name="mime-type-sniffing"></a><span data-ttu-id="80674-222">MIME 형식 검색</span><span class="sxs-lookup"><span data-stu-id="80674-222">MIME-type sniffing</span></span>

<span data-ttu-id="80674-223">이 헤더는 응답 콘텐츠 형식을 재정의하지 않도록 브라우저에 지시하므로 대부분의 브라우저에서 선언된 콘텐츠 형식이 아닌 응답에 대한 MIME 검색을 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-223">This header prevents most browsers from MIME-sniffing a response away from the declared content type, as the header instructs the browser not to override the response content type.</span></span> <span data-ttu-id="80674-224">`nosniff` 옵션을 사용하면 서버에 콘텐츠가 “text/html”이라고 표시될 경우 브라우저는 콘텐츠를 “text/html”으로 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-224">With the `nosniff` option, if the server says the content is "text/html", the browser renders it as "text/html".</span></span>

<span data-ttu-id="80674-225">*nginx.conf* 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-225">Edit the *nginx.conf* file:</span></span>

```bash
sudo nano /etc/nginx/nginx.conf
```

<span data-ttu-id="80674-226">줄 `add_header X-Content-Type-Options "nosniff";`를 추가하고 파일을 저장한 다음 Nginx를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="80674-226">Add the line `add_header X-Content-Type-Options "nosniff";` and save the file, then restart Nginx.</span></span>
