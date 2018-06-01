---
title: Nginx를 사용하여 Linux에서 ASP.NET Core 호스트
author: rick-anderson
description: Ubuntu 16.04에서 Nginx를 역방향 프록시로 설정하여 Kestrel에서 실행되는 ASP.NET Core 웹앱에 HTTP 트래픽을 전달하는 방법을 설명합니다.
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 03/13/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/linux-nginx
ms.openlocfilehash: d37aa25c712d715aa4134587a84e5923f9cb5b79
ms.sourcegitcommit: 50d40c83fa641d283c097f986dde5341ebe1b44c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/22/2018
ms.locfileid: "34452557"
---
# <a name="host-aspnet-core-on-linux-with-nginx"></a><span data-ttu-id="67cb6-103">Nginx를 사용하여 Linux에서 ASP.NET Core 호스트</span><span class="sxs-lookup"><span data-stu-id="67cb6-103">Host ASP.NET Core on Linux with Nginx</span></span>

<span data-ttu-id="67cb6-104">작성자: [Sourabh Shirhatti](https://twitter.com/sshirhatti)</span><span class="sxs-lookup"><span data-stu-id="67cb6-104">By [Sourabh Shirhatti](https://twitter.com/sshirhatti)</span></span>

<span data-ttu-id="67cb6-105">이 가이드에서는 Ubuntu 16.04 Server에서 프로덕션 준비 ASP.NET Core 환경을 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-105">This guide explains setting up a production-ready ASP.NET Core environment on an Ubuntu 16.04 Server.</span></span>

> [!NOTE]
> <span data-ttu-id="67cb6-106">Ubuntu 14.04의 경우 Kestrel 프로세스를 모니터링하기 위한 솔루션으로 *supervisord*를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-106">For Ubuntu 14.04, *supervisord* is recommended as a solution for monitoring the Kestrel process.</span></span> <span data-ttu-id="67cb6-107">*systemd*는 Ubuntu 14.04에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-107">*systemd* isn't available on Ubuntu 14.04.</span></span> <span data-ttu-id="67cb6-108">[이 문서의 이전 버전을 참조하세요](https://github.com/aspnet/Docs/blob/e9c1419175c4dd7e152df3746ba1df5935aaafd5/aspnetcore/publishing/linuxproduction.md).</span><span class="sxs-lookup"><span data-stu-id="67cb6-108">[See previous version of this document](https://github.com/aspnet/Docs/blob/e9c1419175c4dd7e152df3746ba1df5935aaafd5/aspnetcore/publishing/linuxproduction.md).</span></span>

<span data-ttu-id="67cb6-109">이 가이드의 내용:</span><span class="sxs-lookup"><span data-stu-id="67cb6-109">This guide:</span></span>

* <span data-ttu-id="67cb6-110">기존 ASP.NET Core 앱을 역방향 프록시 서버 뒤에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-110">Places an existing ASP.NET Core app behind a reverse proxy server.</span></span>
* <span data-ttu-id="67cb6-111">역방향 프록시 서버를 설정하여 Kestrel 웹 서버에 요청을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-111">Sets up the reverse proxy server to forward requests to the Kestrel web server.</span></span>
* <span data-ttu-id="67cb6-112">웹앱이 시작 시 디먼으로 실행되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-112">Ensures the web app runs on startup as a daemon.</span></span>
* <span data-ttu-id="67cb6-113">웹앱 다시 시작을 지원하도록 프로세스 관리 도구를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-113">Configures a process management tool to help restart the web app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67cb6-114">전제 조건</span><span class="sxs-lookup"><span data-stu-id="67cb6-114">Prerequisites</span></span>

1. <span data-ttu-id="67cb6-115">sudo 권한을 가진 표준 사용자 계정으로 Ubuntu 16.04 Server에 액세스</span><span class="sxs-lookup"><span data-stu-id="67cb6-115">Access to an Ubuntu 16.04 Server with a standard user account with sudo privilege</span></span>
1. <span data-ttu-id="67cb6-116">기존 ASP.NET Core 앱</span><span class="sxs-lookup"><span data-stu-id="67cb6-116">An existing ASP.NET Core app</span></span>

## <a name="copy-over-the-app"></a><span data-ttu-id="67cb6-117">앱을 통해 복사</span><span class="sxs-lookup"><span data-stu-id="67cb6-117">Copy over the app</span></span>

<span data-ttu-id="67cb6-118">개발 환경에서 [dotnet publish](/dotnet/core/tools/dotnet-publish)를 실행하여 앱을 서버에서 실행될 수 있는 자체 포함된 디렉터리로 패키지합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-118">Run [dotnet publish](/dotnet/core/tools/dotnet-publish) from the dev environment to package an app into a self-contained directory that can run on the server.</span></span>

<span data-ttu-id="67cb6-119">무엇이든 조직의 워크플로에 통합된 도구(예: SCP, FTP)를 사용하여 ASP.NET Core 앱을 서버에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-119">Copy the ASP.NET Core app to the server using whatever tool integrates into the organization's workflow (for example, SCP, FTP).</span></span> <span data-ttu-id="67cb6-120">다음과 같이 앱을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-120">Test the app, for example:</span></span>

* <span data-ttu-id="67cb6-121">명령줄에서 `dotnet <app_assembly>.dll`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-121">From the command line, run `dotnet <app_assembly>.dll`.</span></span>
* <span data-ttu-id="67cb6-122">브라우저에서 `http://<serveraddress>:<port>`로 이동하여 앱이 Linux에서 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-122">In a browser, navigate to `http://<serveraddress>:<port>` to verify the app works on Linux.</span></span> 
 
## <a name="configure-a-reverse-proxy-server"></a><span data-ttu-id="67cb6-123">역방향 프록시 서버 구성</span><span class="sxs-lookup"><span data-stu-id="67cb6-123">Configure a reverse proxy server</span></span>

<span data-ttu-id="67cb6-124">역방향 프록시는 동적 웹앱을 지원하기 위한 일반적인 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-124">A reverse proxy is a common setup for serving dynamic web apps.</span></span> <span data-ttu-id="67cb6-125">역방향 프록시는 HTTP 요청을 종료하고 이 요청을 ASP.NET Core 앱에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-125">A reverse proxy terminates the HTTP request and forwards it to the ASP.NET Core app.</span></span>

### <a name="why-use-a-reverse-proxy-server"></a><span data-ttu-id="67cb6-126">역방향 프록시 서버를 사용하는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="67cb6-126">Why use a reverse proxy server?</span></span>

<span data-ttu-id="67cb6-127">Kestrel은 ASP.NET Core에서 동적 콘텐츠를 제공하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-127">Kestrel is great for serving dynamic content from ASP.NET Core.</span></span> <span data-ttu-id="67cb6-128">그러나 웹 지원 기능은 IIS, Apache 또는 Nginx와 같은 서버만큼 기능이 다양하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-128">However, the web serving capabilities aren't as feature rich as servers such as IIS, Apache, or Nginx.</span></span> <span data-ttu-id="67cb6-129">역방향 프록시 서버는 정적 콘텐츠 지원, 요청 캐시, 요청 압축 및 HTTP 서버에서 SSL 종료 같은 작업을 오프로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-129">A reverse proxy server can offload work such as serving static content, caching requests, compressing requests, and SSL termination from the HTTP server.</span></span> <span data-ttu-id="67cb6-130">역방향 프록시 서버는 전용 컴퓨터에 있거나 HTTP 서버와 함께 배포될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-130">A reverse proxy server may reside on a dedicated machine or may be deployed alongside an HTTP server.</span></span>

<span data-ttu-id="67cb6-131">이 가이드에서는 Nginx의 단일 인스턴스가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-131">For the purposes of this guide, a single instance of Nginx is used.</span></span> <span data-ttu-id="67cb6-132">이 인스턴스는 HTTP 서버와 함께 동일한 서버에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-132">It runs on the same server, alongside the HTTP server.</span></span> <span data-ttu-id="67cb6-133">요구 사항에 따라 다른 설정을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-133">Based on requirements, a different setup may be chosen.</span></span>

<span data-ttu-id="67cb6-134">요청이 역방향 프록시를 통해 전달되므로 [Microsoft.AspNetCore.HttpOverrides](https://www.nuget.org/packages/Microsoft.AspNetCore.HttpOverrides/) 패키지의 전달된 헤더 미들웨어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-134">Because requests are forwarded by reverse proxy, use the Forwarded Headers Middleware from the [Microsoft.AspNetCore.HttpOverrides](https://www.nuget.org/packages/Microsoft.AspNetCore.HttpOverrides/) package.</span></span> <span data-ttu-id="67cb6-135">이 미들웨어는 `X-Forwarded-Proto` 헤더를 사용하여 `Request.Scheme`을 업데이트하므로 리디렉션 URI 및 기타 보안 정책이 제대로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-135">The middleware updates the `Request.Scheme`, using the `X-Forwarded-Proto` header, so that redirect URIs and other security policies work correctly.</span></span>

<span data-ttu-id="67cb6-136">인증 미들웨어 유형을 사용하는 경우에는 전달된 헤더 미들웨어를 먼저 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-136">When using any type of authentication middleware, the Forwarded Headers Middleware must run first.</span></span> <span data-ttu-id="67cb6-137">이렇게 순서를 지정하면 인증 미들웨어가 헤더 값을 사용하고 올바른 리디렉션 URI를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-137">This ordering ensures that the authentication middleware can consume the header values and generate correct redirect URIs.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="67cb6-138">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="67cb6-138">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="67cb6-139">[UseAuthentication](/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication) 또는 유사한 인증 체계 미들웨어를 호출하기 전에 `Startup.Configure`에서 [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-139">Invoke the [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) method in `Startup.Configure` before calling [UseAuthentication](/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication) or similar authentication scheme middleware.</span></span> <span data-ttu-id="67cb6-140">`X-Forwarded-For` 및 `X-Forwarded-Proto` 헤더를 전달하도록 미들웨어를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-140">Configure the middleware to forward the `X-Forwarded-For` and `X-Forwarded-Proto` headers:</span></span>

```csharp
app.UseForwardedHeaders(new ForwardedHeadersOptions
{
    ForwardedHeaders = ForwardedHeaders.XForwardedFor | ForwardedHeaders.XForwardedProto
});

app.UseAuthentication();
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="67cb6-141">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="67cb6-141">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="67cb6-142">[UseIdentity](/dotnet/api/microsoft.aspnetcore.builder.builderextensions.useidentity)와 [UseFacebookAuthentication](/dotnet/api/microsoft.aspnetcore.builder.facebookappbuilderextensions.usefacebookauthentication) 또는 유사한 인증 체계 미들웨어를 호출하기 전에 `Startup.Configure`에서 [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-142">Invoke the [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) method in `Startup.Configure` before calling [UseIdentity](/dotnet/api/microsoft.aspnetcore.builder.builderextensions.useidentity) and [UseFacebookAuthentication](/dotnet/api/microsoft.aspnetcore.builder.facebookappbuilderextensions.usefacebookauthentication) or similar authentication scheme middleware.</span></span> <span data-ttu-id="67cb6-143">`X-Forwarded-For` 및 `X-Forwarded-Proto` 헤더를 전달하도록 미들웨어를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-143">Configure the middleware to forward the `X-Forwarded-For` and `X-Forwarded-Proto` headers:</span></span>

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

<span data-ttu-id="67cb6-144">미들웨어에 [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions)가 지정되지 않은 경우 전달할 기본 헤더는 `None`입니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-144">If no [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions) are specified to the middleware, the default headers to forward are `None`.</span></span>

<span data-ttu-id="67cb6-145">프록시 서버 및 부하 분산 장치 외에도 호스팅되는 앱에 추가 구성이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-145">Additional configuration might be required for apps hosted behind proxy servers and load balancers.</span></span> <span data-ttu-id="67cb6-146">자세한 내용은 [프록시 서버 및 부하 분산 장치를 사용하도록 ASP.NET Core 구성](xref:host-and-deploy/proxy-load-balancer)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67cb6-146">For more information, see [Configure ASP.NET Core to work with proxy servers and load balancers](xref:host-and-deploy/proxy-load-balancer).</span></span>

### <a name="install-nginx"></a><span data-ttu-id="67cb6-147">Nginx 설치</span><span class="sxs-lookup"><span data-stu-id="67cb6-147">Install Nginx</span></span>

```bash
sudo apt-get install nginx
```

> [!NOTE]
> <span data-ttu-id="67cb6-148">선택적 Nginx 모듈이 설치될 경우 소스에서 Nginx를 빌드해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-148">If optional Nginx modules will be installed, building Nginx from source might be required.</span></span>

<span data-ttu-id="67cb6-149">`apt-get`을 사용하여 Nginx를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-149">Use `apt-get` to install Nginx.</span></span> <span data-ttu-id="67cb6-150">설치 관리자는 시스템 시작 시 Nginx를 디먼으로 실행하는 System V init 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-150">The installer creates a System V init script that runs Nginx as daemon on system startup.</span></span> <span data-ttu-id="67cb6-151">Nginx가 처음 설치되었으므로 다음을 실행하여 명시적으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-151">Since Nginx was installed for the first time, explicitly start it by running:</span></span>

```bash
sudo service nginx start
```

<span data-ttu-id="67cb6-152">브라우저에 Nginx에 대한 기본 방문 페이지가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-152">Verify a browser displays the default landing page for Nginx.</span></span>

### <a name="configure-nginx"></a><span data-ttu-id="67cb6-153">Nginx 구성</span><span class="sxs-lookup"><span data-stu-id="67cb6-153">Configure Nginx</span></span>

<span data-ttu-id="67cb6-154">Nginx를 역방향 프록시로 구성하여 요청을 ASP.NET Core 앱에 프로그램에 전달하려면 */etc/nginx/sites-available/default*를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-154">To configure Nginx as a reverse proxy to forward requests to your ASP.NET Core app, modify */etc/nginx/sites-available/default*.</span></span> <span data-ttu-id="67cb6-155">텍스트 편집기에서 해당 항목을 열고 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-155">Open it in a text editor, and replace the contents with the following:</span></span>

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

<span data-ttu-id="67cb6-156">`server_name`이 일치하지 않으면 Nginx는 기본 서버를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-156">When no `server_name` matches, Nginx uses the default server.</span></span> <span data-ttu-id="67cb6-157">기본 서버가 정의되지 않은 경우 구성 파일의 첫 번째 서버는 기본 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-157">If no default server is defined, the first server in the configuration file is the default server.</span></span> <span data-ttu-id="67cb6-158">구성 파일에 있는 444 상태 코드를 반환하는 특정 기본 서버를 추가하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-158">As a best practice, add a specific default server which returns a status code of 444 in your configuration file.</span></span> <span data-ttu-id="67cb6-159">기본 서버 구성 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-159">A default server configuration example is:</span></span>

```nginx
server {
    listen   80 default_server;
    # listen [::]:80 default_server deferred;
    return   444;
}
```

<span data-ttu-id="67cb6-160">이전 구성 파일과 기본 서버를 사용하여 Nginx는 포트 80에서 호스트 헤더 `example.com` 또는 `*.example.com`가 포함된 공용 트래픽을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-160">With the preceding configuration file and default server, Nginx accepts public traffic on port 80 with host header `example.com` or `*.example.com`.</span></span> <span data-ttu-id="67cb6-161">이러한 호스트와 일치하지 않는 요청은 Kestrel로 전달되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-161">Requests not matching these hosts won't get forwarded to Kestrel.</span></span> <span data-ttu-id="67cb6-162">Nginx는 일치하는 요청을 `http://localhost:5000`의 Kestrel에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-162">Nginx forwards the matching requests to Kestrel at `http://localhost:5000`.</span></span> <span data-ttu-id="67cb6-163">자세한 내용은 [How nginx processes a request](https://nginx.org/docs/http/request_processing.html)(nginx가 요청을 처리하는 방법)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67cb6-163">See [How nginx processes a request](https://nginx.org/docs/http/request_processing.html) for more information.</span></span>

> [!WARNING]
> <span data-ttu-id="67cb6-164">적절한 [server_name 지시문](https://nginx.org/docs/http/server_names.html)을 지정하지 않으면 앱이 보안 취약성에 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-164">Failure to specify a proper [server_name directive](https://nginx.org/docs/http/server_names.html) exposes your app to security vulnerabilities.</span></span> <span data-ttu-id="67cb6-165">전체 부모 도메인을 제어하는 경우 하위 도메인 와일드카드 바인딩(예: `*.example.com`)에는 이러한 보안 위험이 발생하지 않습니다(취약한 `*.com`과 반대임).</span><span class="sxs-lookup"><span data-stu-id="67cb6-165">Subdomain wildcard binding (for example, `*.example.com`) doesn't pose this security risk if you control the entire parent domain (as opposed to `*.com`, which is vulnerable).</span></span> <span data-ttu-id="67cb6-166">자세한 내용은 [rfc7230 섹션-5.4](https://tools.ietf.org/html/rfc7230#section-5.4)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="67cb6-166">See [rfc7230 section-5.4](https://tools.ietf.org/html/rfc7230#section-5.4) for more information.</span></span>

<span data-ttu-id="67cb6-167">Nginx 구성이 설정되면 `sudo nginx -t`를 실행하여 구성 파일의 구문을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-167">Once the Nginx configuration is established, run `sudo nginx -t` to verify the syntax of the configuration files.</span></span> <span data-ttu-id="67cb6-168">구성 파일 테스트에 성공하면 `sudo nginx -s reload`를 실행하여 Nginx가 변경 내용을 선택하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-168">If the configuration file test is successful, force Nginx to pick up the changes by running `sudo nginx -s reload`.</span></span>

## <a name="monitoring-the-app"></a><span data-ttu-id="67cb6-169">앱 모니터링</span><span class="sxs-lookup"><span data-stu-id="67cb6-169">Monitoring the app</span></span>

<span data-ttu-id="67cb6-170">서버는 `http://<serveraddress>:80`에 대해 실행된 요청을 `http://127.0.0.1:5000`의 Kestrel에서 실행되는 ASP.NET Core 앱에 전달하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-170">The server is setup to forward requests made to `http://<serveraddress>:80` on to the ASP.NET Core app running on Kestrel at `http://127.0.0.1:5000`.</span></span> <span data-ttu-id="67cb6-171">그러나 Nginx는 Kestrel 프로세스를 관리하도록 설정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-171">However, Nginx isn't set up to manage the Kestrel process.</span></span> <span data-ttu-id="67cb6-172">*systemd*를 사용하여 기본 웹앱을 시작 및 모니터링하기 위한 서비스 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-172">*systemd* can be used to create a service file to start and monitor the underlying web app.</span></span> <span data-ttu-id="67cb6-173">*systemd*는 프로세스를 시작, 중지 및 관리하기 위한 다양하고 강력한 기능을 제공하는 init 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-173">*systemd* is an init system that provides many powerful features for starting, stopping, and managing processes.</span></span> 

### <a name="create-the-service-file"></a><span data-ttu-id="67cb6-174">서비스 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="67cb6-174">Create the service file</span></span>

<span data-ttu-id="67cb6-175">서비스 정의 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-175">Create the service definition file:</span></span>

```bash
sudo nano /etc/systemd/system/kestrel-hellomvc.service
```

<span data-ttu-id="67cb6-176">앱에 대한 예제 서비스 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-176">The following is an example service file for the app:</span></span>

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

<span data-ttu-id="67cb6-177">사용자 *www-data*가 구성에서 사용되지 않을 경우 여기서 정의된 사용자를 먼저 만들고 파일에 대한 적절한 소유권을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-177">If the user *www-data* isn't used by the configuration, the user defined here must be created first and given proper ownership for files.</span></span>

<span data-ttu-id="67cb6-178">Linux에는 대/소문자를 구분하는 파일 시스템이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-178">Linux has a case-sensitive file system.</span></span> <span data-ttu-id="67cb6-179">ASPNETCORE_ENVIRONMENT를 “프로덕션”으로 설정하면 *appsettings.production.json* 대신 구성 파일 *appsettings.Production.json*을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-179">Setting ASPNETCORE_ENVIRONMENT to "Production" results in searching for the configuration file *appsettings.Production.json*, not *appsettings.production.json*.</span></span>

> [!NOTE]
> <span data-ttu-id="67cb6-180">일부 값(예: SQL 연결 문자열)은 환경 변수를 읽기 위해 구성 공급자에 대해 이스케이프되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-180">Some values (for example, SQL connection strings) must be escaped for the configuration providers to read the environment variables.</span></span> <span data-ttu-id="67cb6-181">다음 명령을 사용하여 구성 파일에서 사용할 제대로 이스케이프된 값을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-181">Use the following command to generate a properly escaped value for use in the configuration file:</span></span>
>
> ```console
> systemd-escape "<value-to-escape>"
> ```

<span data-ttu-id="67cb6-182">파일을 저장하고 서비스를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-182">Save the file and enable the service.</span></span>

```bash
systemctl enable kestrel-hellomvc.service
```

<span data-ttu-id="67cb6-183">서비스를 시작하고 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-183">Start the service and verify that it's running.</span></span>

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

<span data-ttu-id="67cb6-184">역방향 프록시를 구성하고 systemd를 통해 Kestrel을 관리하면 웹앱이 완전히 구성되고 로컬 컴퓨터(`http://localhost`)의 브라우저에서 웹앱에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-184">With the reverse proxy configured and Kestrel managed through systemd, the web app is fully configured and can be accessed from a browser on the local machine at `http://localhost`.</span></span> <span data-ttu-id="67cb6-185">차단 중인 방화벽이 없다면 원격 컴퓨터에서 액세스할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-185">It's also accessible from a remote machine, barring any firewall that might be blocking.</span></span> <span data-ttu-id="67cb6-186">응답 헤더를 검사하는 `Server` 헤더는 Kestrel에서 지원하는 ASP.NET Core 앱을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-186">Inspecting the response headers, the `Server` header shows the ASP.NET Core app being served by Kestrel.</span></span>

```text
HTTP/1.1 200 OK
Date: Tue, 11 Oct 2016 16:22:23 GMT
Server: Kestrel
Keep-Alive: timeout=5, max=98
Connection: Keep-Alive
Transfer-Encoding: chunked
```

### <a name="viewing-logs"></a><span data-ttu-id="67cb6-187">로그 보기</span><span class="sxs-lookup"><span data-stu-id="67cb6-187">Viewing logs</span></span>

<span data-ttu-id="67cb6-188">Kestrel을 사용하는 웹앱은 `systemd`를 사용하여 관리되므로 모든 이벤트 및 프로세스가 중앙형 저널에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-188">Since the web app using Kestrel is managed using `systemd`, all events and processes are logged to a centralized journal.</span></span> <span data-ttu-id="67cb6-189">그러나 이 저널에는 `systemd`를 통해 관리하는 모든 서비스 및 프로세스에 대한 모든 항목이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-189">However, this journal includes all entries for all services and processes managed by `systemd`.</span></span> <span data-ttu-id="67cb6-190">`kestrel-hellomvc.service` 관련 항목을 보려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-190">To view the `kestrel-hellomvc.service`-specific items, use the following command:</span></span>

```bash
sudo journalctl -fu kestrel-hellomvc.service
```

<span data-ttu-id="67cb6-191">추가 필터링을 위해 `--since today`, `--until 1 hour ago` 같은 시간 옵션이나 이러한 옵션의 조합을 사용하여 반환되는 항목 수를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-191">For further filtering, time options such as `--since today`, `--until 1 hour ago` or a combination of these can reduce the amount of entries returned.</span></span>

```bash
sudo journalctl -fu kestrel-hellomvc.service --since "2016-10-18" --until "2016-10-18 04:00"
```

## <a name="securing-the-app"></a><span data-ttu-id="67cb6-192">앱 보안</span><span class="sxs-lookup"><span data-stu-id="67cb6-192">Securing the app</span></span>

### <a name="enable-apparmor"></a><span data-ttu-id="67cb6-193">AppArmor 사용</span><span class="sxs-lookup"><span data-stu-id="67cb6-193">Enable AppArmor</span></span>

<span data-ttu-id="67cb6-194">LSM(Linux Security Modules)은 Linux 2.6 이후 Linux 커널에 포함된 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-194">Linux Security Modules (LSM) is a framework that's part of the Linux kernel since Linux 2.6.</span></span> <span data-ttu-id="67cb6-195">LSM은 보안 모듈의 다양한 구현을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-195">LSM supports different implementations of security modules.</span></span> <span data-ttu-id="67cb6-196">[AppArmor](https://wiki.ubuntu.com/AppArmor)는 프로그램을 제한된 리소스 집합으로 한정할 수 있는 필수 Access Control 시스템을 구현하는 LSM입니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-196">[AppArmor](https://wiki.ubuntu.com/AppArmor) is a LSM that implements a Mandatory Access Control system which allows confining the program to a limited set of resources.</span></span> <span data-ttu-id="67cb6-197">AppArmor가 사용하도록 설정되고 제대로 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-197">Ensure AppArmor is enabled and properly configured.</span></span>

### <a name="configuring-the-firewall"></a><span data-ttu-id="67cb6-198">방화벽 구성</span><span class="sxs-lookup"><span data-stu-id="67cb6-198">Configuring the firewall</span></span>

<span data-ttu-id="67cb6-199">사용되지 않는 모든 외부 포트를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-199">Close off all external ports that are not in use.</span></span> <span data-ttu-id="67cb6-200">복잡하지 않은 방화벽(ufw)은 방화벽을 구성하기 위한 명령줄 인터페이스를 제공하여 `iptables`에 대한 프런트 엔드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-200">Uncomplicated firewall (ufw) provides a front end for `iptables` by providing a command line interface for configuring the firewall.</span></span> <span data-ttu-id="67cb6-201">`ufw`가 필요한 모든 포트에서 트래픽을 허용하도록 구성되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-201">Verify that `ufw` is configured to allow traffic on any ports needed.</span></span>

```bash
sudo apt-get install ufw
sudo ufw enable

sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
```

### <a name="securing-nginx"></a><span data-ttu-id="67cb6-202">Nginx 보안</span><span class="sxs-lookup"><span data-stu-id="67cb6-202">Securing Nginx</span></span>

<span data-ttu-id="67cb6-203">Nginx의 기본 배포 시에는 SSL이 사용하도록 설정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-203">The default distribution of Nginx doesn't enable SSL.</span></span> <span data-ttu-id="67cb6-204">추가 보안 기능을 사용하도록 설정하려면 소스에서 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-204">To enable additional security features, build from source.</span></span>

#### <a name="download-the-source-and-install-the-build-dependencies"></a><span data-ttu-id="67cb6-205">소스 다운로드 및 빌드 종속성 설치</span><span class="sxs-lookup"><span data-stu-id="67cb6-205">Download the source and install the build dependencies</span></span>

```bash
# Install the build dependencies
sudo apt-get update
sudo apt-get install build-essential zlib1g-dev libpcre3-dev libssl-dev libxslt1-dev libxml2-dev libgd2-xpm-dev libgeoip-dev libgoogle-perftools-dev libperl-dev

# Download Nginx 1.10.0 or latest
wget http://www.nginx.org/download/nginx-1.10.0.tar.gz
tar zxf nginx-1.10.0.tar.gz
```

#### <a name="change-the-nginx-response-name"></a><span data-ttu-id="67cb6-206">Nginx 응답 이름 변경</span><span class="sxs-lookup"><span data-stu-id="67cb6-206">Change the Nginx response name</span></span>

<span data-ttu-id="67cb6-207">*src/http/ngx_http_header_filter_module.c*를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-207">Edit *src/http/ngx_http_header_filter_module.c*:</span></span>

```c
static char ngx_http_server_string[] = "Server: Web Server" CRLF;
static char ngx_http_server_full_string[] = "Server: Web Server" CRLF;
```

#### <a name="configure-the-options-and-build"></a><span data-ttu-id="67cb6-208">옵션 구성 및 빌드</span><span class="sxs-lookup"><span data-stu-id="67cb6-208">Configure the options and build</span></span>

<span data-ttu-id="67cb6-209">정규식의 경우 PCRE 라이브러리가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-209">The PCRE library is required for regular expressions.</span></span> <span data-ttu-id="67cb6-210">정규식은 ngx_http_rewrite_module에 대한 위치 지시문에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-210">Regular expressions are used in the location directive for the ngx_http_rewrite_module.</span></span> <span data-ttu-id="67cb6-211">http_ssl_module은 HTTPS 프로토콜 지원을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-211">The http_ssl_module adds HTTPS protocol support.</span></span>

<span data-ttu-id="67cb6-212">*ModSecurity* 같은 웹앱 방화벽을 사용하여 앱을 강화해 보세요.</span><span class="sxs-lookup"><span data-stu-id="67cb6-212">Consider using a web app firewall like *ModSecurity* to harden the app.</span></span>

```bash
./configure
--with-pcre=../pcre-8.38
--with-zlib=../zlib-1.2.8
--with-http_ssl_module
--with-stream
--with-mail=dynamic
```

#### <a name="configure-ssl"></a><span data-ttu-id="67cb6-213">SSL 구성</span><span class="sxs-lookup"><span data-stu-id="67cb6-213">Configure SSL</span></span>

* <span data-ttu-id="67cb6-214">신뢰할 수 있는 CA(인증 기관)에서 발급된 유효한 인증서를 지정하여 포트 `443`에서 HTTPS 트래픽을 수신 대기하도록 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-214">Configure the server to listen to HTTPS traffic on port `443` by specifying a valid certificate issued by a trusted Certificate Authority (CA).</span></span>

* <span data-ttu-id="67cb6-215">다음 */etc/nginx/nginx.conf* 파일에 설명된 일부 사례를 채택하여 보안을 강화합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-215">Harden the security by employing some of the practices depicted in the following */etc/nginx/nginx.conf* file.</span></span> <span data-ttu-id="67cb6-216">예를 들어 더 강력한 암호화를 선택하고 HTTP를 사용한 모든 트래픽을 HTTPS로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-216">Examples include choosing a stronger cipher and redirecting all traffic over HTTP to HTTPS.</span></span>

* <span data-ttu-id="67cb6-217">HSTS(`HTTP Strict-Transport-Security`) 헤더를 추가하면 클라이언트에서 만든 모든 후속 요청에 HTTPS만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-217">Adding an `HTTP Strict-Transport-Security` (HSTS) header ensures all subsequent requests made by the client are over HTTPS only.</span></span>

* <span data-ttu-id="67cb6-218">Strict-Transport-Security 헤더를 추가하지 않거나, 나중에 SSL을 사용하지 않도록 설정할 경우 적절한 `max-age`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-218">Don't add the Strict-Transport-Security header or chose an appropriate `max-age` if SSL will be disabled in the future.</span></span>

<span data-ttu-id="67cb6-219">*/etc/nginx/proxy.conf* 구성 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-219">Add the */etc/nginx/proxy.conf* configuration file:</span></span>

[!code-nginx[](linux-nginx/proxy.conf)]

<span data-ttu-id="67cb6-220">*/etc/nginx/nginx.conf* 구성 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-220">Edit the */etc/nginx/nginx.conf* configuration file.</span></span> <span data-ttu-id="67cb6-221">예제에서는 `http` 및 `server` 섹션이 하나의 구성 파일에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-221">The example contains both `http` and `server` sections in one configuration file.</span></span>

[!code-nginx[](linux-nginx/nginx.conf?highlight=2)]

#### <a name="secure-nginx-from-clickjacking"></a><span data-ttu-id="67cb6-222">클릭재킹(clickjacking)으로부터 Nginx 보호</span><span class="sxs-lookup"><span data-stu-id="67cb6-222">Secure Nginx from clickjacking</span></span>
<span data-ttu-id="67cb6-223">클릭재킹은 감염된 사용자의 클릭을 수집하는 악의적인 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-223">Clickjacking is a malicious technique to collect an infected user's clicks.</span></span> <span data-ttu-id="67cb6-224">클릭재킹은 희생자(방문자)를 속여서 감염된 사이트를 클릭하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-224">Clickjacking tricks the victim (visitor) into clicking on an infected site.</span></span> <span data-ttu-id="67cb6-225">X-FRAME-OPTIONS를 사용하여 사이트를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-225">Use X-FRAME-OPTIONS to secure the site.</span></span>

<span data-ttu-id="67cb6-226">*nginx.conf* 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-226">Edit the *nginx.conf* file:</span></span>

```bash
sudo nano /etc/nginx/nginx.conf
```

<span data-ttu-id="67cb6-227">줄 `add_header X-Frame-Options "SAMEORIGIN";`을 추가하고 파일을 저장한 다음 Nginx를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-227">Add the line `add_header X-Frame-Options "SAMEORIGIN";` and save the file, then restart Nginx.</span></span>

#### <a name="mime-type-sniffing"></a><span data-ttu-id="67cb6-228">MIME 형식 검색</span><span class="sxs-lookup"><span data-stu-id="67cb6-228">MIME-type sniffing</span></span>

<span data-ttu-id="67cb6-229">이 헤더는 응답 콘텐츠 형식을 재정의하지 않도록 브라우저에 지시하므로 대부분의 브라우저에서 선언된 콘텐츠 형식이 아닌 응답에 대한 MIME 검색을 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-229">This header prevents most browsers from MIME-sniffing a response away from the declared content type, as the header instructs the browser not to override the response content type.</span></span> <span data-ttu-id="67cb6-230">`nosniff` 옵션을 사용하면 서버에 콘텐츠가 “text/html”이라고 표시될 경우 브라우저는 콘텐츠를 “text/html”으로 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-230">With the `nosniff` option, if the server says the content is "text/html", the browser renders it as "text/html".</span></span>

<span data-ttu-id="67cb6-231">*nginx.conf* 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-231">Edit the *nginx.conf* file:</span></span>

```bash
sudo nano /etc/nginx/nginx.conf
```

<span data-ttu-id="67cb6-232">줄 `add_header X-Content-Type-Options "nosniff";`를 추가하고 파일을 저장한 다음 Nginx를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="67cb6-232">Add the line `add_header X-Content-Type-Options "nosniff";` and save the file, then restart Nginx.</span></span>
