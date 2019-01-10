---
title: ASP.NET Core 모듈
author: guardrex
description: ASP.NET Core 앱을 호스팅하기 위해 ASP.NET Core 모듈을 구성하는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 12/18/2018
uid: host-and-deploy/aspnet-core-module
ms.openlocfilehash: dee4fe7a498d211cb8ef6a3c49017c3cc8a56847
ms.sourcegitcommit: 816f39e852a8f453e8682081871a31bc66db153a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2018
ms.locfileid: "53637861"
---
# <a name="aspnet-core-module"></a><span data-ttu-id="f610e-103">ASP.NET Core 모듈</span><span class="sxs-lookup"><span data-stu-id="f610e-103">ASP.NET Core Module</span></span>

<span data-ttu-id="f610e-104">작성자: [Tom Dykstra](https://github.com/tdykstra), [Rick Strahl](https://github.com/RickStrahl), [Chris Ross](https://github.com/Tratcher), [Rick Anderson](https://twitter.com/RickAndMSFT), [Sourabh Shirhatti](https://twitter.com/sshirhatti), [Justin Kotalik](https://github.com/jkotalik) 및 [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="f610e-104">By [Tom Dykstra](https://github.com/tdykstra), [Rick Strahl](https://github.com/RickStrahl), [Chris Ross](https://github.com/Tratcher), [Rick Anderson](https://twitter.com/RickAndMSFT), [Sourabh Shirhatti](https://twitter.com/sshirhatti), [Justin Kotalik](https://github.com/jkotalik), and [Luke Latham](https://github.com/guardrex)</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="f610e-105">ASP.NET Core 모듈은 다음을 위해 IIS 파이프라인에 연결되는 네이티브 IIS 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-105">The ASP.NET Core Module is a native IIS module that plugs into the IIS pipeline to either:</span></span>

* <span data-ttu-id="f610e-106">IIS 작업자 프로세스(`w3wp.exe`) 내부에 ASP.NET Core 앱을 호스트하며 [In-Process 호스팅 모델](#in-process-hosting-model)이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-106">Host an ASP.NET Core app inside of the IIS worker process (`w3wp.exe`), called the [in-process hosting model](#in-process-hosting-model).</span></span>
* <span data-ttu-id="f610e-107">[Kestrel 서버](xref:fundamentals/servers/kestrel)를 실행하는 백 엔드 ASP.NET Core 앱으로 웹 요청을 전달하며 [Out-of-Process 호스팅 모델](#out-of-process-hosting-model)이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-107">Forward web requests to a backend ASP.NET Core app running the [Kestrel server](xref:fundamentals/servers/kestrel), called the [out-of-process hosting model](#out-of-process-hosting-model).</span></span>

<span data-ttu-id="f610e-108">지원되는 Windows 버전:</span><span class="sxs-lookup"><span data-stu-id="f610e-108">Supported Windows versions:</span></span>

* <span data-ttu-id="f610e-109">Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="f610e-109">Windows 7 or later</span></span>
* <span data-ttu-id="f610e-110">Windows Server 2008 R2 이상</span><span class="sxs-lookup"><span data-stu-id="f610e-110">Windows Server 2008 R2 or later</span></span>

<span data-ttu-id="f610e-111">In Process를 호스트하는 경우 모듈에서는 IIS HTTP Server(`IISHttpServer`)라는 IIS용 In Process 서버 구현을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-111">When hosting in-process, the module uses an in-process server implementation for IIS, called IIS HTTP Server (`IISHttpServer`).</span></span>

<span data-ttu-id="f610e-112">Out-of-Process로 호스트하는 경우 모듈은 Kestrel에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-112">When hosting out-of-process, the module only works with Kestrel.</span></span> <span data-ttu-id="f610e-113">모듈이 [HTTP.sys](xref:fundamentals/servers/httpsys)와 호환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-113">The module is incompatible with [HTTP.sys](xref:fundamentals/servers/httpsys).</span></span>

## <a name="hosting-models"></a><span data-ttu-id="f610e-114">호스팅 모델</span><span class="sxs-lookup"><span data-stu-id="f610e-114">Hosting models</span></span>

### <a name="in-process-hosting-model"></a><span data-ttu-id="f610e-115">In-Process 호스팅 모델</span><span class="sxs-lookup"><span data-stu-id="f610e-115">In-process hosting model</span></span>

<span data-ttu-id="f610e-116">In-Process 호스팅용 앱을 구성하려면 `<AspNetCoreHostingModel>` 속성을 `InProcess` 값의 앱 프로젝트 파일에 추가합니다(Out-of-Process 호스팅은 `OutOfProcess`로 설정됨).</span><span class="sxs-lookup"><span data-stu-id="f610e-116">To configure an app for in-process hosting, add the `<AspNetCoreHostingModel>` property to the app's project file with a value of `InProcess` (out-of-process hosting is set with `OutOfProcess`):</span></span>

```xml
<PropertyGroup>
  <AspNetCoreHostingModel>InProcess</AspNetCoreHostingModel>
</PropertyGroup>
```

<span data-ttu-id="f610e-117">파일에 `<AspNetCoreHostingModel>` 속성이 없으면 기본값은 `OutOfProcess`입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-117">If the `<AspNetCoreHostingModel>` property isn't present in the file, the default value is `OutOfProcess`.</span></span>

<span data-ttu-id="f610e-118">다음 특성은 In-Process로 호스팅할 때 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-118">The following characteristics apply when hosting in-process:</span></span>

* <span data-ttu-id="f610e-119">IIS HTTP 서버(`IISHttpServer`)는 [Kestrel](xref:fundamentals/servers/kestrel) 서버 대신 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-119">IIS HTTP Server (`IISHttpServer`) is used instead of [Kestrel](xref:fundamentals/servers/kestrel) server.</span></span>

* <span data-ttu-id="f610e-120">[requestTimeout 특성](#attributes-of-the-aspnetcore-element)이 In-Process 호스팅에 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-120">The [requestTimeout attribute](#attributes-of-the-aspnetcore-element) doesn't apply to in-process hosting.</span></span>

* <span data-ttu-id="f610e-121">앱 간의 앱 풀 공유는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-121">Sharing an app pool among apps isn't supported.</span></span> <span data-ttu-id="f610e-122">앱당 하나의 앱 풀을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-122">Use one app pool per app.</span></span>

* <span data-ttu-id="f610e-123">[웹 배포](/iis/publish/using-web-deploy/introduction-to-web-deploy)를 사용하거나 [app_offline.htm 파일을 배포에](xref:host-and-deploy/iis/index#locked-deployment-files) 수동으로 배치할 경우 열린 연결이 있으면 앱이 즉시 종료되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-123">When using [Web Deploy](/iis/publish/using-web-deploy/introduction-to-web-deploy) or manually placing an [app_offline.htm file in the deployment](xref:host-and-deploy/iis/index#locked-deployment-files), the app might not shut down immediately if there's an open connection.</span></span> <span data-ttu-id="f610e-124">예를 들어, WebSocket 연결은 앱 종료를 지연시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-124">For example, a websocket connection may delay app shut down.</span></span>

* <span data-ttu-id="f610e-125">앱 및 설치된 런타임(x64 또는 x86)의 아키텍처(비트)는 앱 풀의 아키텍처와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-125">The architecture (bitness) of the app and installed runtime (x64 or x86) must match the architecture of the app pool.</span></span>

* <span data-ttu-id="f610e-126">`WebHostBuilder`([CreateDefaultBuilder](xref:fundamentals/host/web-host#set-up-a-host)를 사용하지 않고)를 사용하여 앱 호스트를 수동으로 설정하며 앱이 Kestrel 서버에서 직접 실행되는 경우(자체 호스트됨) `UseIISIntegration`를 호출하기 전에 `UseKestrel`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-126">If setting up the app's host manually with `WebHostBuilder` (not using [CreateDefaultBuilder](xref:fundamentals/host/web-host#set-up-a-host)) and the app is ever run directly on the Kestrel server (self-hosted), call `UseKestrel` before calling `UseIISIntegration`.</span></span> <span data-ttu-id="f610e-127">이 순서가 바뀌면 호스트가 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-127">If the order is reversed, the host fails to start.</span></span>

* <span data-ttu-id="f610e-128">클라이언트의 연결 끊김이 검색되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-128">Client disconnects are detected.</span></span> <span data-ttu-id="f610e-129">클라이언트의 연결이 끊어지면 [HttpContext.RequestAborted](xref:Microsoft.AspNetCore.Http.HttpContext.RequestAborted*) 취소 토큰이 취소됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-129">The [HttpContext.RequestAborted](xref:Microsoft.AspNetCore.Http.HttpContext.RequestAborted*) cancellation token is cancelled when the client disconnects.</span></span>

* <span data-ttu-id="f610e-130"><xref:System.IO.Directory.GetCurrentDirectory*>는 앱 디렉터리가 아닌 IIS에 의해 시작된 프로세스의 작업자 디렉터리를 반환합니다(예: *w3wp.exe*에 대한 *C:\Windows\System32\inetsrv*).</span><span class="sxs-lookup"><span data-stu-id="f610e-130"><xref:System.IO.Directory.GetCurrentDirectory*> returns the worker directory of the process started by IIS rather than the app's directory (for example, *C:\Windows\System32\inetsrv* for *w3wp.exe*).</span></span>

  <span data-ttu-id="f610e-131">앱의 현재 디렉터리를 설정하는 샘플 코드는 [CurrentDirectoryHelpers 클래스](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/aspnet-core-module/samples_snapshot/2.x/CurrentDirectoryHelpers.cs)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f610e-131">For sample code that sets the app's current directory, see the [CurrentDirectoryHelpers class](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/aspnet-core-module/samples_snapshot/2.x/CurrentDirectoryHelpers.cs).</span></span> <span data-ttu-id="f610e-132">`SetCurrentDirectory` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-132">Call the `SetCurrentDirectory` method.</span></span> <span data-ttu-id="f610e-133"><xref:System.IO.Directory.GetCurrentDirectory*>에 대한 후속 호출은 앱의 디렉터리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-133">Subsequent calls to <xref:System.IO.Directory.GetCurrentDirectory*> provide the app's directory.</span></span>

### <a name="out-of-process-hosting-model"></a><span data-ttu-id="f610e-134">Out-of-Process 호스팅 모델</span><span class="sxs-lookup"><span data-stu-id="f610e-134">Out-of-process hosting model</span></span>

<span data-ttu-id="f610e-135">Out of Process 호스팅을 위한 앱을 구성하려면 프로젝트 파일에서 다음 방법 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-135">To configure an app for out-of-process hosting, use either of the following approaches in the project file:</span></span>

* <span data-ttu-id="f610e-136">`<AspNetCoreHostingModel>` 속성을 지정하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="f610e-136">Don't specify the `<AspNetCoreHostingModel>` property.</span></span> <span data-ttu-id="f610e-137">파일에 `<AspNetCoreHostingModel>` 속성이 없으면 기본값은 `OutOfProcess`입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-137">If the `<AspNetCoreHostingModel>` property isn't present in the file, the default value is `OutOfProcess`.</span></span>
* <span data-ttu-id="f610e-138">`<AspNetCoreHostingModel>` 속성 값을 `OutOfProcess`로 설정합니다(In Process 호스트팅은 `InProcess`로 설정됨).</span><span class="sxs-lookup"><span data-stu-id="f610e-138">Set the value of the `<AspNetCoreHostingModel>` property to `OutOfProcess` (in-process hosting is set with `InProcess`):</span></span>

```xml
<PropertyGroup>
  <AspNetCoreHostingModel>OutOfProcess</AspNetCoreHostingModel>
</PropertyGroup>
```

<span data-ttu-id="f610e-139">[Kestrel](xref:fundamentals/servers/kestrel) 서버는 IIS HTTP 서버(`IISHttpServer`) 대신 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-139">[Kestrel](xref:fundamentals/servers/kestrel) server is used instead of IIS HTTP Server (`IISHttpServer`).</span></span>

### <a name="hosting-model-changes"></a><span data-ttu-id="f610e-140">호스팅 모델 변경</span><span class="sxs-lookup"><span data-stu-id="f610e-140">Hosting model changes</span></span>

<span data-ttu-id="f610e-141">`hostingModel` 설정이 *web.config* 파일에서 변경되면([web.config로 구성](#configuration-with-webconfig) 섹션에 설명되어 있음) 모듈은 IIS에 대한 작업자 프로세스를 재순환합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-141">If the `hostingModel` setting is changed in the *web.config* file (explained in the [Configuration with web.config](#configuration-with-webconfig) section), the module recycles the worker process for IIS.</span></span>

<span data-ttu-id="f610e-142">IIS Express의 경우 모듈은 작업자 프로세스를 재순환하지 않고, 대신 현재 IIS Express 프로세스의 정상 종료를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-142">For IIS Express, the module doesn't recycle the worker process but instead triggers a graceful shutdown of the current IIS Express process.</span></span> <span data-ttu-id="f610e-143">앱에 대한 다음 요청은 새 IIS Express 프로세스를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-143">The next request to the app spawns a new IIS Express process.</span></span>

### <a name="process-name"></a><span data-ttu-id="f610e-144">프로세스 이름</span><span class="sxs-lookup"><span data-stu-id="f610e-144">Process name</span></span>

<span data-ttu-id="f610e-145">`Process.GetCurrentProcess().ProcessName`은 `w3wp`/`iisexpress`(In-Process) 또는 `dotnet`(Out-of-Process)을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-145">`Process.GetCurrentProcess().ProcessName` reports `w3wp`/`iisexpress` (in-process) or `dotnet` (out-of-process).</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="f610e-146">ASP.NET Core 모듈은 백 엔드 ASP.NET Core 앱으로 웹 요청을 전달하는 IIS 파이프라인에 연결되는 네이티브 IIS 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-146">The ASP.NET Core Module is a native IIS module that plugs into the IIS pipeline to forward web requests to backend ASP.NET Core apps.</span></span>

<span data-ttu-id="f610e-147">지원되는 Windows 버전:</span><span class="sxs-lookup"><span data-stu-id="f610e-147">Supported Windows versions:</span></span>

* <span data-ttu-id="f610e-148">Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="f610e-148">Windows 7 or later</span></span>
* <span data-ttu-id="f610e-149">Windows Server 2008 R2 이상</span><span class="sxs-lookup"><span data-stu-id="f610e-149">Windows Server 2008 R2 or later</span></span>

<span data-ttu-id="f610e-150">모듈은 Kestrel에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-150">The module only works with Kestrel.</span></span> <span data-ttu-id="f610e-151">모듈이 [HTTP.sys](xref:fundamentals/servers/httpsys)와 호환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-151">The module is incompatible with [HTTP.sys](xref:fundamentals/servers/httpsys).</span></span>

<span data-ttu-id="f610e-152">ASP.NET Core 앱은 IIS 작업자 프로세스와 별도의 프로세스에서 실행되므로 이 모듈은 프로세스 관리도 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-152">Because ASP.NET Core apps run in a process separate from the IIS worker process, the module also handles process management.</span></span> <span data-ttu-id="f610e-153">이 모듈은 첫 번째 요청이 들어올 때 ASP.NET Core 앱용 프로세스를 시작하고 충돌이 발생하면 앱을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-153">The module starts the process for the ASP.NET Core app when the first request arrives and restarts the app if it crashes.</span></span> <span data-ttu-id="f610e-154">이는 [Windows Process Activation Service(WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was)로 관리되는 IIS에서 In Process로 실행되는 ASP.NET 4.x 앱에서 볼 수 있는 동작과 기본적으로 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-154">This is essentially the same behavior as seen with ASP.NET 4.x apps that run in-process in IIS that are managed by the [Windows Process Activation Service (WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was).</span></span>

<span data-ttu-id="f610e-155">다음 다이어그램은 IIS, ASP.NET Core 모듈 및 앱 간의 관계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-155">The following diagram illustrates the relationship between IIS, the ASP.NET Core Module, and an app:</span></span>

![ASP.NET Core 모듈](aspnet-core-module/_static/ancm-outofprocess.png)

<span data-ttu-id="f610e-157">요청은 웹에서 커널 모드 HTTP.sys 드라이버로 도착합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-157">Requests arrive from the web to the kernel-mode HTTP.sys driver.</span></span> <span data-ttu-id="f610e-158">드라이버는 웹 사이트의 구성된 포트(일반적으로 80(HTTP) 또는 443(HTTPS))에서 IIS로 요청을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-158">The driver routes the requests to IIS on the website's configured port, usually 80 (HTTP) or 443 (HTTPS).</span></span> <span data-ttu-id="f610e-159">모듈은 포트 80 또는 443이 아닌 앱의 임의의 포트에서 Kestrel로 요청을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-159">The module forwards the requests to Kestrel on a random port for the app, which isn't port 80 or 443.</span></span>

<span data-ttu-id="f610e-160">모듈은 시작 시 환경 변수를 통해 포트를 지정하고 IIS 통합 미들웨어는 `http://localhost:{port}`에서 수신 대기하도록 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-160">The module specifies the port via an environment variable at startup, and the IIS Integration Middleware configures the server to listen on `http://localhost:{port}`.</span></span> <span data-ttu-id="f610e-161">추가 검사가 수행되고 모듈에서 시작되지 않은 요청은 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-161">Additional checks are performed, and requests that don't originate from the module are rejected.</span></span> <span data-ttu-id="f610e-162">모듈은 HTTPS 전달을 지원하지 않으므로 HTTPS를 통해 IIS에서 수신된 경우에도 HTTP를 통해 요청이 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-162">The module doesn't support HTTPS forwarding, so requests are forwarded over HTTP even if received by IIS over HTTPS.</span></span>

<span data-ttu-id="f610e-163">Kestrel이 모듈에서 요청을 선택한 후, 요청은 ASP.NET Core 미들웨어 파이프라인으로 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-163">After Kestrel picks up the request from the module, the request is pushed into the ASP.NET Core middleware pipeline.</span></span> <span data-ttu-id="f610e-164">미들웨어 파이프라인은 요청을 처리하고 앱의 논리에 `HttpContext` 인스턴스로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-164">The middleware pipeline handles the request and passes it on as an `HttpContext` instance to the app's logic.</span></span> <span data-ttu-id="f610e-165">IIS 통합에 의해 추가된 미들웨어는 체계, 원격 IP 및 경로 기준을 Kestrel에 요청을 전달하기 위한 계정으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-165">Middleware added by IIS Integration updates the scheme, remote IP, and pathbase to account for forwarding the request to Kestrel.</span></span> <span data-ttu-id="f610e-166">앱의 응답은 IIS로 다시 전달되고, 요청을 시작한 HTTP 클라이언트에 다시 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-166">The app's response is passed back to IIS, which pushes it back out to the HTTP client that initiated the request.</span></span>

::: moniker-end

<span data-ttu-id="f610e-167">Windows 인증 등의 많은 네이티브 모듈이 활성 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-167">Many native modules, such as Windows Authentication, remain active.</span></span> <span data-ttu-id="f610e-168">ASP.NET Core 모듈을 사용하여 활성화된 IIS 모듈에 대해 자세히 알아보려면 <xref:host-and-deploy/iis/modules>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f610e-168">To learn more about IIS modules active with the ASP.NET Core Module, see <xref:host-and-deploy/iis/modules>.</span></span>

<span data-ttu-id="f610e-169">ASP.NET Core 모듈은 다음 작업을 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-169">The ASP.NET Core Module can also:</span></span>

* <span data-ttu-id="f610e-170">작업자 프로세스의 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-170">Set environment variables for the worker process.</span></span>
* <span data-ttu-id="f610e-171">시작 문제를 해결하기 위해 stdout 출력을 파일 저장소에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-171">Log stdout output to file storage for troubleshooting startup issues.</span></span>
* <span data-ttu-id="f610e-172">Windows 인증 토큰을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-172">Forward Windows authentication tokens.</span></span>

## <a name="how-to-install-and-use-the-aspnet-core-module"></a><span data-ttu-id="f610e-173">ASP.NET Core 모듈을 설치하고 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="f610e-173">How to install and use the ASP.NET Core Module</span></span>

<span data-ttu-id="f610e-174">ASP.NET Core 모듈을 설치하고 사용하는 방법에 대한 지침은 <xref:host-and-deploy/iis/index>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f610e-174">For instructions on how to install and use the ASP.NET Core Module, see <xref:host-and-deploy/iis/index>.</span></span>

## <a name="configuration-with-webconfig"></a><span data-ttu-id="f610e-175">web.config를 사용한 구성</span><span class="sxs-lookup"><span data-stu-id="f610e-175">Configuration with web.config</span></span>

<span data-ttu-id="f610e-176">ASP.NET Core 모듈은 사이트의 *web.config* 파일에 있는 `system.webServer` 노드의 `aspNetCore` 섹션으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-176">The ASP.NET Core Module is configured with the `aspNetCore` section of the `system.webServer` node in the site's *web.config* file.</span></span>

<span data-ttu-id="f610e-177">다음 *web.config* 파일은 [프레임워크 종속 배포](/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd)를 위해 게시되고 사이트 요청을 처리하도록 ASP.NET Core 모듈을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-177">The following *web.config* file is published for a [framework-dependent deployment](/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd) and configures the ASP.NET Core Module to handle site requests:</span></span>

::: moniker range=">= aspnetcore-2.2"

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <location path="." inheritInChildApplications="false">
    <system.webServer>
      <handlers>
        <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModuleV2" resourceType="Unspecified" />
      </handlers>
      <aspNetCore processPath="dotnet" 
                  arguments=".\MyApp.dll" 
                  stdoutLogEnabled="false" 
                  stdoutLogFile=".\logs\stdout" 
                  hostingModel="InProcess" />
    </system.webServer>
  </location>
</configuration>
```

::: moniker-end

::: moniker range="< aspnetcore-2.2"

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModule" resourceType="Unspecified" />
    </handlers>
    <aspNetCore processPath="dotnet" 
                arguments=".\MyApp.dll" 
                stdoutLogEnabled="false" 
                stdoutLogFile=".\logs\stdout" />
  </system.webServer>
</configuration>
```

::: moniker-end

<span data-ttu-id="f610e-178">다음 *web.config*는 [자체 포함 배포](/dotnet/articles/core/deploying/#self-contained-deployments-scd)를 위해 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-178">The following *web.config* is published for a [self-contained deployment](/dotnet/articles/core/deploying/#self-contained-deployments-scd):</span></span>

::: moniker range=">= aspnetcore-2.2"

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <location path="." inheritInChildApplications="false">
    <system.webServer>
      <handlers>
        <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModuleV2" resourceType="Unspecified" />
      </handlers>
      <aspNetCore processPath=".\MyApp.exe" 
                  stdoutLogEnabled="false" 
                  stdoutLogFile=".\logs\stdout" 
                  hostingModel="InProcess" />
    </system.webServer>
  </location>
</configuration>
```

<span data-ttu-id="f610e-179"><xref:System.Configuration.SectionInformation.InheritInChildApplications*> 속성이 `false`로 설정되어 [\<location>](/iis/manage/managing-your-configuration-settings/understanding-iis-configuration-delegation#the-concept-of-location) 요소 내에서 지정된 설정이 하위 디렉터리에 있는 앱에 상속되지 않음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-179">The <xref:System.Configuration.SectionInformation.InheritInChildApplications*> property is set to `false` to indicate that the settings specified within the [\<location>](/iis/manage/managing-your-configuration-settings/understanding-iis-configuration-delegation#the-concept-of-location) element aren't inherited by apps that reside in a subdirectory of the app.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModule" resourceType="Unspecified" />
    </handlers>
    <aspNetCore processPath=".\MyApp.exe" 
                stdoutLogEnabled="false" 
                stdoutLogFile=".\logs\stdout" />
  </system.webServer>
</configuration>
```

::: moniker-end

<span data-ttu-id="f610e-180">앱이 [Azure App Service](https://azure.microsoft.com/services/app-service/)에 배포되면 `stdoutLogFile` 경로가 `\\?\%home%\LogFiles\stdout`로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-180">When an app is deployed to [Azure App Service](https://azure.microsoft.com/services/app-service/), the `stdoutLogFile` path is set to `\\?\%home%\LogFiles\stdout`.</span></span> <span data-ttu-id="f610e-181">이 경로는 서비스에서 자동으로 만들어진 위치인 *LogFiles* 폴더에 stdout 로그를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-181">The path saves stdout logs to the *LogFiles* folder, which is a location automatically created by the service.</span></span>

<span data-ttu-id="f610e-182">IIS 하위 애플리케이션 구성에 대한 자세한 내용은 <xref:host-and-deploy/iis/index#sub-applications>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f610e-182">For information on IIS sub-application configuration, see <xref:host-and-deploy/iis/index#sub-applications>.</span></span>

### <a name="attributes-of-the-aspnetcore-element"></a><span data-ttu-id="f610e-183">aspNetCore 요소의 특성</span><span class="sxs-lookup"><span data-stu-id="f610e-183">Attributes of the aspNetCore element</span></span>

::: moniker range=">= aspnetcore-2.2"

| <span data-ttu-id="f610e-184">특성</span><span class="sxs-lookup"><span data-stu-id="f610e-184">Attribute</span></span> | <span data-ttu-id="f610e-185">설명</span><span class="sxs-lookup"><span data-stu-id="f610e-185">Description</span></span> | <span data-ttu-id="f610e-186">기본</span><span class="sxs-lookup"><span data-stu-id="f610e-186">Default</span></span> |
| --------- | ----------- | :-----: |
| `arguments` | <p><span data-ttu-id="f610e-187">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-187">Optional string attribute.</span></span></p><p><span data-ttu-id="f610e-188">**processPath**에 지정된 실행 파일에 대한 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-188">Arguments to the executable specified in **processPath**.</span></span></p> | |
| `disableStartUpErrorPage` | <p><span data-ttu-id="f610e-189">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-189">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="f610e-190">true인 경우 **502.5 - 프로세스 실패** 페이지가 표시되지 않고 *web.config*에 구성된 502 상태 코드 페이지가 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-190">If true, the **502.5 - Process Failure** page is suppressed, and the 502 status code page configured in the *web.config* takes precedence.</span></span></p> | `false` |
| `forwardWindowsAuthToken` | <p><span data-ttu-id="f610e-191">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-191">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="f610e-192">true인 경우 토큰은 %ASPNETCORE_PORT%에서 수신 대기하는 자식 프로세스에 요청별 헤더 'MS-ASPNETCORE-WINAUTHTOKEN'으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-192">If true, the token is forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="f610e-193">이 프로세스는 요청별로 이 토큰에서 CloseHandle을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-193">It's the responsibility of that process to call CloseHandle on this token per request.</span></span></p> | `true` |
| `hostingModel` | <p><span data-ttu-id="f610e-194">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-194">Optional string attribute.</span></span></p><p><span data-ttu-id="f610e-195">호스팅 모델을 In-Process(`InProcess`) 또는 Out-of-Process(`OutOfProcess`)로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-195">Specifies the hosting model as in-process (`InProcess`) or out-of-process (`OutOfProcess`).</span></span></p> | `OutOfProcess` |
| `processesPerApplication` | <p><span data-ttu-id="f610e-196">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-196">Optional integer attribute.</span></span></p><p><span data-ttu-id="f610e-197">앱별로 스핀 업할 수 있는 **processPath** 설정에 지정된 프로세스의 인스턴스 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-197">Specifies the number of instances of the process specified in the **processPath** setting that can be spun up per app.</span></span></p><p><span data-ttu-id="f610e-198">&dagger;In-Process 호스팅의 경우 이 값은 `1`로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-198">&dagger;For in-process hosting, the value is limited to `1`.</span></span></p> | <span data-ttu-id="f610e-199">기본값: `1`</span><span class="sxs-lookup"><span data-stu-id="f610e-199">Default: `1`</span></span><br><span data-ttu-id="f610e-200">최소: `1`</span><span class="sxs-lookup"><span data-stu-id="f610e-200">Min: `1`</span></span><br><span data-ttu-id="f610e-201">최대: `100`&dagger;</span><span class="sxs-lookup"><span data-stu-id="f610e-201">Max: `100`&dagger;</span></span> |
| `processPath` | <p><span data-ttu-id="f610e-202">필수 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-202">Required string attribute.</span></span></p><p><span data-ttu-id="f610e-203">HTTP 요청을 수신 대기하는 프로세스를 시작하는 실행 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-203">Path to the executable that launches a process listening for HTTP requests.</span></span> <span data-ttu-id="f610e-204">상대 경로가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-204">Relative paths are supported.</span></span> <span data-ttu-id="f610e-205">경로가 `.`로 시작되면 경로는 사이트 루트의 상대 경로로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-205">If the path begins with `.`, the path is considered to be relative to the site root.</span></span></p> | |
| `rapidFailsPerMinute` | <p><span data-ttu-id="f610e-206">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-206">Optional integer attribute.</span></span></p><p><span data-ttu-id="f610e-207">**processPath**에 지정된 프로세스의 분당 크래시 허용 횟수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-207">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="f610e-208">이 제한을 초과하면 모듈은 남은 시간 동안 프로세스 시작을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-208">If this limit is exceeded, the module stops launching the process for the remainder of the minute.</span></span></p><p><span data-ttu-id="f610e-209">In-Process 호스팅에서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-209">Not supported with in-process hosting.</span></span></p> | <span data-ttu-id="f610e-210">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="f610e-210">Default: `10`</span></span><br><span data-ttu-id="f610e-211">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="f610e-211">Min: `0`</span></span><br><span data-ttu-id="f610e-212">최대: `100`</span><span class="sxs-lookup"><span data-stu-id="f610e-212">Max: `100`</span></span> |
| `requestTimeout` | <p><span data-ttu-id="f610e-213">선택적 시간 간격 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-213">Optional timespan attribute.</span></span></p><p><span data-ttu-id="f610e-214">ASP.NET Core 모듈이 %ASPNETCORE_PORT%에서 수신 대기하는 프로세스의 응답을 기다리는 기간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-214">Specifies the duration for which the ASP.NET Core Module waits for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="f610e-215">ASP.NET Core 2.1 이상 릴리스와 함께 제공되는 ASP.NET Core 모듈 버전에서는 `requestTimeout`이 전체 시간, 분, 초로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-215">In versions of the ASP.NET Core Module that shipped with the release of ASP.NET Core 2.1 or later, the `requestTimeout` is specified in hours, minutes, and seconds.</span></span></p><p><span data-ttu-id="f610e-216">In-Process 호스팅에는 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-216">Doesn't apply to in-process hosting.</span></span> <span data-ttu-id="f610e-217">In-Process 호스팅의 경우 모듈은 앱이 요청을 처리할 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-217">For in-process hosting, the module waits for the app to process the request.</span></span></p> | <span data-ttu-id="f610e-218">기본값: `00:02:00`</span><span class="sxs-lookup"><span data-stu-id="f610e-218">Default: `00:02:00`</span></span><br><span data-ttu-id="f610e-219">최소: `00:00:00`</span><span class="sxs-lookup"><span data-stu-id="f610e-219">Min: `00:00:00`</span></span><br><span data-ttu-id="f610e-220">최대: `360:00:00`</span><span class="sxs-lookup"><span data-stu-id="f610e-220">Max: `360:00:00`</span></span> |
| `shutdownTimeLimit` | <p><span data-ttu-id="f610e-221">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-221">Optional integer attribute.</span></span></p><p><span data-ttu-id="f610e-222">*app_offline.htm* 파일이 검색될 때 실행 파일이 정상적으로 종료될 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-222">Duration in seconds that the module waits for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p> | <span data-ttu-id="f610e-223">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="f610e-223">Default: `10`</span></span><br><span data-ttu-id="f610e-224">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="f610e-224">Min: `0`</span></span><br><span data-ttu-id="f610e-225">최대: `600`</span><span class="sxs-lookup"><span data-stu-id="f610e-225">Max: `600`</span></span> |
| `startupTimeLimit` | <p><span data-ttu-id="f610e-226">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-226">Optional integer attribute.</span></span></p><p><span data-ttu-id="f610e-227">실행 파일이 포트에서 수신 대기하는 프로세스를 시작할 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-227">Duration in seconds that the module waits for the executable to start a process listening on the port.</span></span> <span data-ttu-id="f610e-228">이 시간 제한을 초과하면 모듈이 프로세스를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-228">If this time limit is exceeded, the module kills the process.</span></span> <span data-ttu-id="f610e-229">모듈은 새 요청을 수신할 때 프로세스를 다시 시작하려고 하고, 마지막 롤링 기간(분)에 앱이 **rapidFailsPerMinute**번 시작에 실패한 경우가 아니면 이후 요청이 들어올 때 프로세스를 계속 다시 시작하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-229">The module attempts to relaunch the process when it receives a new request and continues to attempt to restart the process on subsequent incoming requests unless the app fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p><p><span data-ttu-id="f610e-230">값 0은 무한 시간 제한으로 간주되지 **않습니다**.</span><span class="sxs-lookup"><span data-stu-id="f610e-230">A value of 0 (zero) is **not** considered an infinite timeout.</span></span></p> | <span data-ttu-id="f610e-231">기본값: `120`</span><span class="sxs-lookup"><span data-stu-id="f610e-231">Default: `120`</span></span><br><span data-ttu-id="f610e-232">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="f610e-232">Min: `0`</span></span><br><span data-ttu-id="f610e-233">최대: `3600`</span><span class="sxs-lookup"><span data-stu-id="f610e-233">Max: `3600`</span></span> |
| `stdoutLogEnabled` | <p><span data-ttu-id="f610e-234">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-234">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="f610e-235">true인 경우 **processPath**에 지정된 프로세스에 대한 **stdout** 및 **stderr**이 **stdoutLogFile**에 지정된 파일로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-235">If true, **stdout** and **stderr** for the process specified in **processPath** are redirected to the file specified in **stdoutLogFile**.</span></span></p> | `false` |
| `stdoutLogFile` | <p><span data-ttu-id="f610e-236">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-236">Optional string attribute.</span></span></p><p><span data-ttu-id="f610e-237">**processPath**에 지정된 프로세스에서 **stdout** 및 **stderr**이 기록되는 상대 또는 절대 파일 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-237">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** are logged.</span></span> <span data-ttu-id="f610e-238">상대 경로는 사이트 루트에 상대적인 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-238">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="f610e-239">`.`로 시작하는 모든 경로는 사이트 루트에 상대적인 경로이고 다른 모든 경로는 절대 경로로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-239">Any path starting with `.` are relative to the site root and all other paths are treated as absolute paths.</span></span> <span data-ttu-id="f610e-240">모듈이 로그 파일을 만들려면 경로에 제공된 모든 폴더가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-240">Any folders provided in the path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="f610e-241">타임스탬프, 프로세스 ID 및 파일 확장명(*.log*)은 밑줄 구분 기호를 사용하여 **stdoutLogFile** 경로의 마지막 세그먼트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-241">Using underscore delimiters, a timestamp, process ID, and file extension (*.log*) are added to the last segment of the **stdoutLogFile** path.</span></span> <span data-ttu-id="f610e-242">`.\logs\stdout`이 값으로 제공되는 경우 예제 stdout 로그는 2018년 2월 5일 19시 41분 32초에 프로세스 ID 1934를 사용하여 저장될 경우 *logs* 폴더에 *stdout_20180205194132_1934.log*로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-242">If `.\logs\stdout` is supplied as a value, an example stdout log is saved as *stdout_20180205194132_1934.log* in the *logs* folder when saved on 2/5/2018 at 19:41:32 with a process ID of 1934.</span></span></p> | `aspnetcore-stdout` |

::: moniker-end

::: moniker range="= aspnetcore-2.1"

| <span data-ttu-id="f610e-243">특성</span><span class="sxs-lookup"><span data-stu-id="f610e-243">Attribute</span></span> | <span data-ttu-id="f610e-244">설명</span><span class="sxs-lookup"><span data-stu-id="f610e-244">Description</span></span> | <span data-ttu-id="f610e-245">기본</span><span class="sxs-lookup"><span data-stu-id="f610e-245">Default</span></span> |
| --------- | ----------- | :-----: |
| `arguments` | <p><span data-ttu-id="f610e-246">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-246">Optional string attribute.</span></span></p><p><span data-ttu-id="f610e-247">**processPath**에 지정된 실행 파일에 대한 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-247">Arguments to the executable specified in **processPath**.</span></span></p>| |
| `disableStartUpErrorPage` | <p><span data-ttu-id="f610e-248">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-248">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="f610e-249">true인 경우 **502.5 - 프로세스 실패** 페이지가 표시되지 않고 *web.config*에 구성된 502 상태 코드 페이지가 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-249">If true, the **502.5 - Process Failure** page is suppressed, and the 502 status code page configured in the *web.config* takes precedence.</span></span></p> | `false` |
| `forwardWindowsAuthToken` | <p><span data-ttu-id="f610e-250">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-250">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="f610e-251">true인 경우 토큰은 %ASPNETCORE_PORT%에서 수신 대기하는 자식 프로세스에 요청별 헤더 'MS-ASPNETCORE-WINAUTHTOKEN'으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-251">If true, the token is forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="f610e-252">이 프로세스는 요청별로 이 토큰에서 CloseHandle을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-252">It's the responsibility of that process to call CloseHandle on this token per request.</span></span></p> | `true` |
| `processesPerApplication` | <p><span data-ttu-id="f610e-253">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-253">Optional integer attribute.</span></span></p><p><span data-ttu-id="f610e-254">앱별로 스핀 업할 수 있는 **processPath** 설정에 지정된 프로세스의 인스턴스 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-254">Specifies the number of instances of the process specified in the **processPath** setting that can be spun up per app.</span></span></p> | <span data-ttu-id="f610e-255">기본값: `1`</span><span class="sxs-lookup"><span data-stu-id="f610e-255">Default: `1`</span></span><br><span data-ttu-id="f610e-256">최소: `1`</span><span class="sxs-lookup"><span data-stu-id="f610e-256">Min: `1`</span></span><br><span data-ttu-id="f610e-257">최대: `100`</span><span class="sxs-lookup"><span data-stu-id="f610e-257">Max: `100`</span></span> |
| `processPath` | <p><span data-ttu-id="f610e-258">필수 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-258">Required string attribute.</span></span></p><p><span data-ttu-id="f610e-259">HTTP 요청을 수신 대기하는 프로세스를 시작하는 실행 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-259">Path to the executable that launches a process listening for HTTP requests.</span></span> <span data-ttu-id="f610e-260">상대 경로가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-260">Relative paths are supported.</span></span> <span data-ttu-id="f610e-261">경로가 `.`로 시작되면 경로는 사이트 루트의 상대 경로로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-261">If the path begins with `.`, the path is considered to be relative to the site root.</span></span></p> | |
| `rapidFailsPerMinute` | <p><span data-ttu-id="f610e-262">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-262">Optional integer attribute.</span></span></p><p><span data-ttu-id="f610e-263">**processPath**에 지정된 프로세스의 분당 크래시 허용 횟수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-263">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="f610e-264">이 제한을 초과하면 모듈은 남은 시간 동안 프로세스 시작을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-264">If this limit is exceeded, the module stops launching the process for the remainder of the minute.</span></span></p> | <span data-ttu-id="f610e-265">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="f610e-265">Default: `10`</span></span><br><span data-ttu-id="f610e-266">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="f610e-266">Min: `0`</span></span><br><span data-ttu-id="f610e-267">최대: `100`</span><span class="sxs-lookup"><span data-stu-id="f610e-267">Max: `100`</span></span> |
| `requestTimeout` | <p><span data-ttu-id="f610e-268">선택적 시간 간격 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-268">Optional timespan attribute.</span></span></p><p><span data-ttu-id="f610e-269">ASP.NET Core 모듈이 %ASPNETCORE_PORT%에서 수신 대기하는 프로세스의 응답을 기다리는 기간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-269">Specifies the duration for which the ASP.NET Core Module waits for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="f610e-270">ASP.NET Core 2.1 이상 릴리스와 함께 제공되는 ASP.NET Core 모듈 버전에서는 `requestTimeout`이 전체 시간, 분, 초로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-270">In versions of the ASP.NET Core Module that shipped with the release of ASP.NET Core 2.1 or later, the `requestTimeout` is specified in hours, minutes, and seconds.</span></span></p> | <span data-ttu-id="f610e-271">기본값: `00:02:00`</span><span class="sxs-lookup"><span data-stu-id="f610e-271">Default: `00:02:00`</span></span><br><span data-ttu-id="f610e-272">최소: `00:00:00`</span><span class="sxs-lookup"><span data-stu-id="f610e-272">Min: `00:00:00`</span></span><br><span data-ttu-id="f610e-273">최대: `360:00:00`</span><span class="sxs-lookup"><span data-stu-id="f610e-273">Max: `360:00:00`</span></span> |
| `shutdownTimeLimit` | <p><span data-ttu-id="f610e-274">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-274">Optional integer attribute.</span></span></p><p><span data-ttu-id="f610e-275">*app_offline.htm* 파일이 검색될 때 실행 파일이 정상적으로 종료될 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-275">Duration in seconds that the module waits for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p> | <span data-ttu-id="f610e-276">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="f610e-276">Default: `10`</span></span><br><span data-ttu-id="f610e-277">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="f610e-277">Min: `0`</span></span><br><span data-ttu-id="f610e-278">최대: `600`</span><span class="sxs-lookup"><span data-stu-id="f610e-278">Max: `600`</span></span> |
| `startupTimeLimit` | <p><span data-ttu-id="f610e-279">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-279">Optional integer attribute.</span></span></p><p><span data-ttu-id="f610e-280">실행 파일이 포트에서 수신 대기하는 프로세스를 시작할 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-280">Duration in seconds that the module waits for the executable to start a process listening on the port.</span></span> <span data-ttu-id="f610e-281">이 시간 제한을 초과하면 모듈이 프로세스를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-281">If this time limit is exceeded, the module kills the process.</span></span> <span data-ttu-id="f610e-282">모듈은 새 요청을 수신할 때 프로세스를 다시 시작하려고 하고, 마지막 롤링 기간(분)에 앱이 **rapidFailsPerMinute**번 시작에 실패한 경우가 아니면 이후 요청이 들어올 때 프로세스를 계속 다시 시작하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-282">The module attempts to relaunch the process when it receives a new request and continues to attempt to restart the process on subsequent incoming requests unless the app fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p><p><span data-ttu-id="f610e-283">값 0은 무한 시간 제한으로 간주되지 **않습니다**.</span><span class="sxs-lookup"><span data-stu-id="f610e-283">A value of 0 (zero) is **not** considered an infinite timeout.</span></span></p> | <span data-ttu-id="f610e-284">기본값: `120`</span><span class="sxs-lookup"><span data-stu-id="f610e-284">Default: `120`</span></span><br><span data-ttu-id="f610e-285">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="f610e-285">Min: `0`</span></span><br><span data-ttu-id="f610e-286">최대: `3600`</span><span class="sxs-lookup"><span data-stu-id="f610e-286">Max: `3600`</span></span> |
| `stdoutLogEnabled` | <p><span data-ttu-id="f610e-287">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-287">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="f610e-288">true인 경우 **processPath**에 지정된 프로세스에 대한 **stdout** 및 **stderr**이 **stdoutLogFile**에 지정된 파일로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-288">If true, **stdout** and **stderr** for the process specified in **processPath** are redirected to the file specified in **stdoutLogFile**.</span></span></p> | `false` |
| `stdoutLogFile` | <p><span data-ttu-id="f610e-289">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-289">Optional string attribute.</span></span></p><p><span data-ttu-id="f610e-290">**processPath**에 지정된 프로세스에서 **stdout** 및 **stderr**이 기록되는 상대 또는 절대 파일 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-290">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** are logged.</span></span> <span data-ttu-id="f610e-291">상대 경로는 사이트 루트에 상대적인 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-291">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="f610e-292">`.`로 시작하는 모든 경로는 사이트 루트에 상대적인 경로이고 다른 모든 경로는 절대 경로로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-292">Any path starting with `.` are relative to the site root and all other paths are treated as absolute paths.</span></span> <span data-ttu-id="f610e-293">모듈이 로그 파일을 만들려면 경로에 제공된 모든 폴더가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-293">Any folders provided in the path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="f610e-294">타임스탬프, 프로세스 ID 및 파일 확장명(*.log*)은 밑줄 구분 기호를 사용하여 **stdoutLogFile** 경로의 마지막 세그먼트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-294">Using underscore delimiters, a timestamp, process ID, and file extension (*.log*) are added to the last segment of the **stdoutLogFile** path.</span></span> <span data-ttu-id="f610e-295">`.\logs\stdout`이 값으로 제공되는 경우 예제 stdout 로그는 2018년 2월 5일 19시 41분 32초에 프로세스 ID 1934를 사용하여 저장될 경우 *logs* 폴더에 *stdout_20180205194132_1934.log*로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-295">If `.\logs\stdout` is supplied as a value, an example stdout log is saved as *stdout_20180205194132_1934.log* in the *logs* folder when saved on 2/5/2018 at 19:41:32 with a process ID of 1934.</span></span></p> | `aspnetcore-stdout` |

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

| <span data-ttu-id="f610e-296">특성</span><span class="sxs-lookup"><span data-stu-id="f610e-296">Attribute</span></span> | <span data-ttu-id="f610e-297">설명</span><span class="sxs-lookup"><span data-stu-id="f610e-297">Description</span></span> | <span data-ttu-id="f610e-298">기본</span><span class="sxs-lookup"><span data-stu-id="f610e-298">Default</span></span> |
| --------- | ----------- | :-----: |
| `arguments` | <p><span data-ttu-id="f610e-299">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-299">Optional string attribute.</span></span></p><p><span data-ttu-id="f610e-300">**processPath**에 지정된 실행 파일에 대한 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-300">Arguments to the executable specified in **processPath**.</span></span></p>| |
| `disableStartUpErrorPage` | <p><span data-ttu-id="f610e-301">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-301">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="f610e-302">true인 경우 **502.5 - 프로세스 실패** 페이지가 표시되지 않고 *web.config*에 구성된 502 상태 코드 페이지가 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-302">If true, the **502.5 - Process Failure** page is suppressed, and the 502 status code page configured in the *web.config* takes precedence.</span></span></p> | `false` |
| `forwardWindowsAuthToken` | <p><span data-ttu-id="f610e-303">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-303">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="f610e-304">true인 경우 토큰은 %ASPNETCORE_PORT%에서 수신 대기하는 자식 프로세스에 요청별 헤더 'MS-ASPNETCORE-WINAUTHTOKEN'으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-304">If true, the token is forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="f610e-305">이 프로세스는 요청별로 이 토큰에서 CloseHandle을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-305">It's the responsibility of that process to call CloseHandle on this token per request.</span></span></p> | `true` |
| `processesPerApplication` | <p><span data-ttu-id="f610e-306">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-306">Optional integer attribute.</span></span></p><p><span data-ttu-id="f610e-307">앱별로 스핀 업할 수 있는 **processPath** 설정에 지정된 프로세스의 인스턴스 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-307">Specifies the number of instances of the process specified in the **processPath** setting that can be spun up per app.</span></span></p> | <span data-ttu-id="f610e-308">기본값: `1`</span><span class="sxs-lookup"><span data-stu-id="f610e-308">Default: `1`</span></span><br><span data-ttu-id="f610e-309">최소: `1`</span><span class="sxs-lookup"><span data-stu-id="f610e-309">Min: `1`</span></span><br><span data-ttu-id="f610e-310">최대: `100`</span><span class="sxs-lookup"><span data-stu-id="f610e-310">Max: `100`</span></span> |
| `processPath` | <p><span data-ttu-id="f610e-311">필수 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-311">Required string attribute.</span></span></p><p><span data-ttu-id="f610e-312">HTTP 요청을 수신 대기하는 프로세스를 시작하는 실행 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-312">Path to the executable that launches a process listening for HTTP requests.</span></span> <span data-ttu-id="f610e-313">상대 경로가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-313">Relative paths are supported.</span></span> <span data-ttu-id="f610e-314">경로가 `.`로 시작되면 경로는 사이트 루트의 상대 경로로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-314">If the path begins with `.`, the path is considered to be relative to the site root.</span></span></p> | |
| `rapidFailsPerMinute` | <p><span data-ttu-id="f610e-315">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-315">Optional integer attribute.</span></span></p><p><span data-ttu-id="f610e-316">**processPath**에 지정된 프로세스의 분당 크래시 허용 횟수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-316">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="f610e-317">이 제한을 초과하면 모듈은 남은 시간 동안 프로세스 시작을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-317">If this limit is exceeded, the module stops launching the process for the remainder of the minute.</span></span></p> | <span data-ttu-id="f610e-318">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="f610e-318">Default: `10`</span></span><br><span data-ttu-id="f610e-319">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="f610e-319">Min: `0`</span></span><br><span data-ttu-id="f610e-320">최대: `100`</span><span class="sxs-lookup"><span data-stu-id="f610e-320">Max: `100`</span></span> |
| `requestTimeout` | <p><span data-ttu-id="f610e-321">선택적 시간 간격 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-321">Optional timespan attribute.</span></span></p><p><span data-ttu-id="f610e-322">ASP.NET Core 모듈이 %ASPNETCORE_PORT%에서 수신 대기하는 프로세스의 응답을 기다리는 기간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-322">Specifies the duration for which the ASP.NET Core Module waits for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="f610e-323">ASP.NET Core 2.0 이하 릴리스와 함께 제공되는 ASP.NET Core 모듈 버전에서는 `requestTimeout`을 전체 시간(분)으로만 지정해야 합니다. 그렇지 않으면 기본적으로 2분으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-323">In versions of the ASP.NET Core Module that shipped with the release of ASP.NET Core 2.0 or earlier, the `requestTimeout` must be specified in whole minutes only, otherwise it defaults to 2 minutes.</span></span></p> | <span data-ttu-id="f610e-324">기본값: `00:02:00`</span><span class="sxs-lookup"><span data-stu-id="f610e-324">Default: `00:02:00`</span></span><br><span data-ttu-id="f610e-325">최소: `00:00:00`</span><span class="sxs-lookup"><span data-stu-id="f610e-325">Min: `00:00:00`</span></span><br><span data-ttu-id="f610e-326">최대: `360:00:00`</span><span class="sxs-lookup"><span data-stu-id="f610e-326">Max: `360:00:00`</span></span> |
| `shutdownTimeLimit` | <p><span data-ttu-id="f610e-327">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-327">Optional integer attribute.</span></span></p><p><span data-ttu-id="f610e-328">*app_offline.htm* 파일이 검색될 때 실행 파일이 정상적으로 종료될 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-328">Duration in seconds that the module waits for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p> | <span data-ttu-id="f610e-329">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="f610e-329">Default: `10`</span></span><br><span data-ttu-id="f610e-330">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="f610e-330">Min: `0`</span></span><br><span data-ttu-id="f610e-331">최대: `600`</span><span class="sxs-lookup"><span data-stu-id="f610e-331">Max: `600`</span></span> |
| `startupTimeLimit` | <p><span data-ttu-id="f610e-332">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-332">Optional integer attribute.</span></span></p><p><span data-ttu-id="f610e-333">실행 파일이 포트에서 수신 대기하는 프로세스를 시작할 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-333">Duration in seconds that the module waits for the executable to start a process listening on the port.</span></span> <span data-ttu-id="f610e-334">이 시간 제한을 초과하면 모듈이 프로세스를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-334">If this time limit is exceeded, the module kills the process.</span></span> <span data-ttu-id="f610e-335">모듈은 새 요청을 수신할 때 프로세스를 다시 시작하려고 하고, 마지막 롤링 기간(분)에 앱이 **rapidFailsPerMinute**번 시작에 실패한 경우가 아니면 이후 요청이 들어올 때 프로세스를 계속 다시 시작하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-335">The module attempts to relaunch the process when it receives a new request and continues to attempt to restart the process on subsequent incoming requests unless the app fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p> | <span data-ttu-id="f610e-336">기본값: `120`</span><span class="sxs-lookup"><span data-stu-id="f610e-336">Default: `120`</span></span><br><span data-ttu-id="f610e-337">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="f610e-337">Min: `0`</span></span><br><span data-ttu-id="f610e-338">최대: `3600`</span><span class="sxs-lookup"><span data-stu-id="f610e-338">Max: `3600`</span></span> |
| `stdoutLogEnabled` | <p><span data-ttu-id="f610e-339">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-339">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="f610e-340">true인 경우 **processPath**에 지정된 프로세스에 대한 **stdout** 및 **stderr**이 **stdoutLogFile**에 지정된 파일로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-340">If true, **stdout** and **stderr** for the process specified in **processPath** are redirected to the file specified in **stdoutLogFile**.</span></span></p> | `false` |
| `stdoutLogFile` | <p><span data-ttu-id="f610e-341">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-341">Optional string attribute.</span></span></p><p><span data-ttu-id="f610e-342">**processPath**에 지정된 프로세스에서 **stdout** 및 **stderr**이 기록되는 상대 또는 절대 파일 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-342">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** are logged.</span></span> <span data-ttu-id="f610e-343">상대 경로는 사이트 루트에 상대적인 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-343">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="f610e-344">`.`로 시작하는 모든 경로는 사이트 루트에 상대적인 경로이고 다른 모든 경로는 절대 경로로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-344">Any path starting with `.` are relative to the site root and all other paths are treated as absolute paths.</span></span> <span data-ttu-id="f610e-345">모듈이 로그 파일을 만들려면 경로에 제공된 모든 폴더가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-345">Any folders provided in the path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="f610e-346">타임스탬프, 프로세스 ID 및 파일 확장명(*.log*)은 밑줄 구분 기호를 사용하여 **stdoutLogFile** 경로의 마지막 세그먼트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-346">Using underscore delimiters, a timestamp, process ID, and file extension (*.log*) are added to the last segment of the **stdoutLogFile** path.</span></span> <span data-ttu-id="f610e-347">`.\logs\stdout`이 값으로 제공되는 경우 예제 stdout 로그는 2018년 2월 5일 19시 41분 32초에 프로세스 ID 1934를 사용하여 저장될 경우 *logs* 폴더에 *stdout_20180205194132_1934.log*로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-347">If `.\logs\stdout` is supplied as a value, an example stdout log is saved as *stdout_20180205194132_1934.log* in the *logs* folder when saved on 2/5/2018 at 19:41:32 with a process ID of 1934.</span></span></p> | `aspnetcore-stdout` |

::: moniker-end

### <a name="setting-environment-variables"></a><span data-ttu-id="f610e-348">환경 변수 설정</span><span class="sxs-lookup"><span data-stu-id="f610e-348">Setting environment variables</span></span>

<span data-ttu-id="f610e-349">`processPath` 특성에서 프로세스에 대한 환경 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-349">Environment variables can be specified for the process in the `processPath` attribute.</span></span> <span data-ttu-id="f610e-350">`environmentVariables` 컬렉션 요소의 `environmentVariable` 자식 요소를 사용하여 환경 변수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-350">Specify an environment variable with the `environmentVariable` child element of an `environmentVariables` collection element.</span></span> <span data-ttu-id="f610e-351">이 섹션에 설정된 환경 변수가 시스템 환경 변수보다 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-351">Environment variables set in this section take precedence over system environment variables.</span></span>

<span data-ttu-id="f610e-352">다음 예제에서는 두 개의 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-352">The following example sets two environment variables.</span></span> <span data-ttu-id="f610e-353">`ASPNETCORE_ENVIRONMENT`는 앱의 환경을 `Development`로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-353">`ASPNETCORE_ENVIRONMENT` configures the app's environment to `Development`.</span></span> <span data-ttu-id="f610e-354">앱 예외를 디버그할 때 [개발자 예외 페이지](xref:fundamentals/error-handling)를 강제로 로드하기 위해 개발자가 *web.config* 파일에서 이 값을 일시적으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-354">A developer may temporarily set this value in the *web.config* file in order to force the [Developer Exception Page](xref:fundamentals/error-handling) to load when debugging an app exception.</span></span> <span data-ttu-id="f610e-355">`CONFIG_DIR`은 개발자가 앱 구성 파일을 로드할 경로를 생성하기 위해 시작 시 값을 읽는 코드를 작성한 사용자 정의 환경 변수의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-355">`CONFIG_DIR` is an example of a user-defined environment variable, where the developer has written code that reads the value on startup to form a path for loading the app's configuration file.</span></span>

::: moniker range=">= aspnetcore-2.2"

```xml
<aspNetCore processPath="dotnet"
      arguments=".\MyApp.dll"
      stdoutLogEnabled="false"
      stdoutLogFile="\\?\%home%\LogFiles\stdout"
      hostingModel="InProcess">
  <environmentVariables>
    <environmentVariable name="ASPNETCORE_ENVIRONMENT" value="Development" />
    <environmentVariable name="CONFIG_DIR" value="f:\application_config" />
  </environmentVariables>
</aspNetCore>
```

::: moniker-end

::: moniker range="< aspnetcore-2.2"

```xml
<aspNetCore processPath="dotnet"
      arguments=".\MyApp.dll"
      stdoutLogEnabled="false"
      stdoutLogFile="\\?\%home%\LogFiles\stdout">
  <environmentVariables>
    <environmentVariable name="ASPNETCORE_ENVIRONMENT" value="Development" />
    <environmentVariable name="CONFIG_DIR" value="f:\application_config" />
  </environmentVariables>
</aspNetCore>
```

::: moniker-end

> [!WARNING]
> <span data-ttu-id="f610e-356">인터넷과 같은 신뢰할 수 없는 네트워크에 액세스할 수 없는 스테이징 및 테스트 서버에서는 `ASPNETCORE_ENVIRONMENT` 환경 변수를 `Development`로 설정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-356">Only set the `ASPNETCORE_ENVIRONMENT` environment variable to `Development` on staging and testing servers that aren't accessible to untrusted networks, such as the Internet.</span></span>

## <a name="appofflinehtm"></a><span data-ttu-id="f610e-357">app_offline.htm</span><span class="sxs-lookup"><span data-stu-id="f610e-357">app_offline.htm</span></span>

<span data-ttu-id="f610e-358">응용 프로그램의 루트 디렉터리에서 이름이 *app_offline.htm*인 파일이 검색되면 ASP.NET Core 모듈은 앱을 자동으로 종료하고 들어오는 요청 처리를 중지하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-358">If a file with the name *app_offline.htm* is detected in the root directory of an app, the ASP.NET Core Module attempts to gracefully shutdown the app and stop processing incoming requests.</span></span> <span data-ttu-id="f610e-359">`shutdownTimeLimit`에 정의된 시간(초) 후에도 앱이 계속 실행되면 ASP.NET Core 모듈은 실행 중인 프로세스를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-359">If the app is still running after the number of seconds defined in `shutdownTimeLimit`, the ASP.NET Core Module kills the running process.</span></span>

<span data-ttu-id="f610e-360">*app_offline.htm* 파일이 있는 동안 ASP.NET Core 모듈은 *app_offline.htm* 파일의 콘텐츠를 다시 보내 요청에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-360">While the *app_offline.htm* file is present, the ASP.NET Core Module responds to requests by sending back the contents of the *app_offline.htm* file.</span></span> <span data-ttu-id="f610e-361">*app_offline.htm* 파일이 제거되면 다음 요청이 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-361">When the *app_offline.htm* file is removed, the next request starts the app.</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="f610e-362">Out-of-Process 호스팅 모델을 사용할 때 열린 연결이 있으면 앱이 즉시 종료되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-362">When using the out-of-process hosting model, the app might not shut down immediately if there's an open connection.</span></span> <span data-ttu-id="f610e-363">예를 들어, WebSocket 연결은 앱 종료를 지연시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-363">For example, a websocket connection may delay app shut down.</span></span>

::: moniker-end

## <a name="start-up-error-page"></a><span data-ttu-id="f610e-364">시작 오류 페이지</span><span class="sxs-lookup"><span data-stu-id="f610e-364">Start-up error page</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="f610e-365">In process 및 out of process 호스팅은 모두 앱을 시작하지 못할 때 사용자 지정 오류 페이지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-365">Both in-process and out-of-process hosting produce custom error pages when they fail to start the app.</span></span>

<span data-ttu-id="f610e-366">ASP.NET Core 모듈이 in-process 또는 out-of-process 요청 처리기를 찾지 못하면 *500.0 - In-Process/Out-of-process 처리기 로드 실패* 상태 코드 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-366">If the ASP.NET Core Module fails to find either the in-process or out-of-process request handler, a *500.0 - In-Process/Out-Of-Process Handler Load Failure* status code page appears.</span></span>

<span data-ttu-id="f610e-367">in-process 호스팅의 경우 ASP.NET Core 모듈이 앱을 시작하지 못하면 *500.30 - 시작 실패* 상태 코드 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-367">For in-process hosting if the ASP.NET Core Module fails to start the app, a *500.30 - Start Failure* status code page appears.</span></span>

<span data-ttu-id="f610e-368">out-of-process 호스팅의 경우 ASP.NET Core 모듈이 백 엔드 프로세스를 시작하지 못하거나 백 엔드 프로세스가 시작되지만 구성된 포트에서 수신 대기하지 못하면 *502.5 - 프로세스 실패* 상태 코드 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-368">For out-of-process hosting if the ASP.NET Core Module fails to launch the backend process or the backend process starts but fails to listen on the configured port, a *502.5 - Process Failure* status code page appears.</span></span>

<span data-ttu-id="f610e-369">이 페이지를 표시하지 않고 기본 IIS 5xx 상태 코드 페이지로 되돌리려면 `disableStartUpErrorPage` 특성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-369">To suppress this page and revert to the default IIS 5xx status code page, use the `disableStartUpErrorPage` attribute.</span></span> <span data-ttu-id="f610e-370">사용자 지정 오류 메시지 구성에 대한 자세한 내용은 [HTTP 오류 \<httpErrors>](/iis/configuration/system.webServer/httpErrors/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f610e-370">For more information on configuring custom error messages, see [HTTP Errors \<httpErrors>](/iis/configuration/system.webServer/httpErrors/).</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="f610e-371">ASP.NET Core 모듈이 백 엔드 프로세스를 시작하지 못하거나 백 엔드 프로세스가 시작되지만 구성된 포트에서 수신 대기하지 못하면 *502.5 - 프로세스 실패* 상태 코드 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-371">If the ASP.NET Core Module fails to launch the backend process or the backend process starts but fails to listen on the configured port, a *502.5 - Process Failure* status code page appears.</span></span> <span data-ttu-id="f610e-372">이 페이지를 표시하지 않고 기본 IIS 502 상태 코드 페이지로 되돌리려면 `disableStartUpErrorPage` 특성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-372">To suppress this page and revert to the default IIS 502 status code page, use the `disableStartUpErrorPage` attribute.</span></span> <span data-ttu-id="f610e-373">사용자 지정 오류 메시지 구성에 대한 자세한 내용은 [HTTP 오류 \<httpErrors>](/iis/configuration/system.webServer/httpErrors/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f610e-373">For more information on configuring custom error messages, see [HTTP Errors \<httpErrors>](/iis/configuration/system.webServer/httpErrors/).</span></span>

![502.5 프로세스 실패 상태 코드 페이지](aspnet-core-module/_static/ANCM-502_5.png)

::: moniker-end

## <a name="log-creation-and-redirection"></a><span data-ttu-id="f610e-375">로그 만들기 및 리디렉션</span><span class="sxs-lookup"><span data-stu-id="f610e-375">Log creation and redirection</span></span>

<span data-ttu-id="f610e-376">ASP.NET Core 모듈은 `aspNetCore` 요소의 `stdoutLogEnabled` 및 `stdoutLogFile` 특성이 설정된 경우 stdout 및 stderr 콘솔 출력을 디스크로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-376">The ASP.NET Core Module redirects stdout and stderr console output to disk if the `stdoutLogEnabled` and `stdoutLogFile` attributes of the `aspNetCore` element are set.</span></span> <span data-ttu-id="f610e-377">모듈이 로그 파일을 만들려면 `stdoutLogFile` 경로의 모든 폴더가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-377">Any folders in the `stdoutLogFile` path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="f610e-378">앱 풀에는 로그가 기록될 위치에 쓰기 권한이 있어야 합니다(`IIS AppPool\<app_pool_name>`을 사용하여 쓰기 권한 제공).</span><span class="sxs-lookup"><span data-stu-id="f610e-378">The app pool must have write access to the location where the logs are written (use `IIS AppPool\<app_pool_name>` to provide write permission).</span></span>

<span data-ttu-id="f610e-379">프로세스 재생/다시 시작이 발생하지 않는 한 로그는 회전되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-379">Logs aren't rotated, unless process recycling/restart occurs.</span></span> <span data-ttu-id="f610e-380">로그에서 사용하는 디스크 공간을 제한하는 것은 호스터의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-380">It's the responsibility of the hoster to limit the disk space the logs consume.</span></span>

<span data-ttu-id="f610e-381">stdout 로그는 앱 시작 문제를 해결하는 경우에만 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-381">Using the stdout log is only recommended for troubleshooting app startup issues.</span></span> <span data-ttu-id="f610e-382">일반 앱 로깅을 위해 stdout 로그를 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="f610e-382">Don't use the stdout log for general app logging purposes.</span></span> <span data-ttu-id="f610e-383">ASP.NET Core 앱의 루틴 로깅에는 로그 파일 크기를 제한하고 로그를 회전하는 로깅 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-383">For routine logging in an ASP.NET Core app, use a logging library that limits log file size and rotates logs.</span></span> <span data-ttu-id="f610e-384">자세한 내용은 [타사 로깅 공급자](xref:fundamentals/logging/index#third-party-logging-providers)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f610e-384">For more information, see [third-party logging providers](xref:fundamentals/logging/index#third-party-logging-providers).</span></span>

<span data-ttu-id="f610e-385">로그 파일이 만들어질 때 타임스탬프 및 파일 확장명이 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-385">A timestamp and file extension are added automatically when the log file is created.</span></span> <span data-ttu-id="f610e-386">로그 파일 이름은 타임스탬프, 프로세스 ID 및 파일 확장명(*.log*)을 밑줄로 구분된 `stdoutLogFile` 경로의 마지막 세그먼트(일반적으로 *stdout*)에 추가하여 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-386">The log file name is composed by appending the timestamp, process ID, and file extension (*.log*) to the last segment of the `stdoutLogFile` path (typically *stdout*) delimited by underscores.</span></span> <span data-ttu-id="f610e-387">`stdoutLogFile` 경로가 *stdout*으로 끝나는 경우 2018년 2월 5일 19시 42분 32초에 만들어진 PID 1934를 사용하는 앱에 대한 로그의 파일 이름은 *stdout_20180205194132_1934.log*입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-387">If the `stdoutLogFile` path ends with *stdout*, a log for an app with a PID of 1934 created on 2/5/2018 at 19:42:32 has the file name *stdout_20180205194132_1934.log*.</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="f610e-388">`stdoutLogEnabled`가 false이면 앱 시작 시 발생하는 오류가 캡처되어 최대 30KB의 이벤트 로그로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-388">If `stdoutLogEnabled` is false, errors that occur on app startup are captured and emitted to the event log up to 30 KB.</span></span> <span data-ttu-id="f610e-389">시작 후에는 모든 추가 로그가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-389">After startup, all additional logs are discarded.</span></span>

::: moniker-end

<span data-ttu-id="f610e-390">다음 샘플 `aspNetCore` 요소는 Azure App Service에서 호스트되는 앱에 대한 stdout 로깅을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-390">The following sample `aspNetCore` element configures stdout logging for an app hosted in Azure App Service.</span></span> <span data-ttu-id="f610e-391">로컬 로깅에는 로컬 경로 또는 네트워크 공유 경로가 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-391">A local path or network share path is acceptable for local logging.</span></span> <span data-ttu-id="f610e-392">AppPool 사용자 ID에 제공된 경로에 쓸 수 있는 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-392">Confirm that the AppPool user identity has permission to write to the path provided.</span></span>

::: moniker range=">= aspnetcore-2.2"

```xml
<aspNetCore processPath="dotnet"
    arguments=".\MyApp.dll"
    stdoutLogEnabled="true"
    stdoutLogFile="\\?\%home%\LogFiles\stdout"
    hostingModel="InProcess">
</aspNetCore>
```

::: moniker-end

::: moniker range="< aspnetcore-2.2"

```xml
<aspNetCore processPath="dotnet"
    arguments=".\MyApp.dll"
    stdoutLogEnabled="true"
    stdoutLogFile="\\?\%home%\LogFiles\stdout">
</aspNetCore>
```

::: moniker-end

::: moniker range=">= aspnetcore-2.2"

## <a name="enhanced-diagnostic-logs"></a><span data-ttu-id="f610e-393">개선된 진단 로그</span><span class="sxs-lookup"><span data-stu-id="f610e-393">Enhanced diagnostic logs</span></span>

<span data-ttu-id="f610e-394">ASP.NET Core 모듈 제공은 개선된 진단 로그를 제공하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-394">The ASP.NET Core Module provides is configurable to provide enhanced diagnostics logs.</span></span> <span data-ttu-id="f610e-395">*web.config*의 `<aspNetCore>` 요소에 `<handlerSettings>` 요소를 추가합니다. `debugLevel`을 `TRACE`으로 설정하면 진단 정보의 충실도가 높아집니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-395">Add the `<handlerSettings>` element to the `<aspNetCore>` element in *web.config*. Setting the `debugLevel` to `TRACE` exposes a higher fidelity of diagnostic information:</span></span>

```xml
<aspNetCore processPath="dotnet"
    arguments=".\MyApp.dll"
    stdoutLogEnabled="false"
    stdoutLogFile="\\?\%home%\LogFiles\stdout"
    hostingModel="InProcess">
  <handlerSettings>
    <handlerSetting name="debugFile" value="aspnetcore-debug.log" />
    <handlerSetting name="debugLevel" value="FILE,TRACE" />
  </handlerSettings>
</aspNetCore>
```

<span data-ttu-id="f610e-396">디버그 수준 (`debugLevel`) 값은 수준과 위치를 모두 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-396">Debug level (`debugLevel`) values can include both the level and the location.</span></span>

<span data-ttu-id="f610e-397">수준(최소한에서 가장 자세한 정보까지 순서대로 ):</span><span class="sxs-lookup"><span data-stu-id="f610e-397">Levels (in order from least to most verbose):</span></span>

* <span data-ttu-id="f610e-398">오류</span><span class="sxs-lookup"><span data-stu-id="f610e-398">ERROR</span></span>
* <span data-ttu-id="f610e-399">경고</span><span class="sxs-lookup"><span data-stu-id="f610e-399">WARNING</span></span>
* <span data-ttu-id="f610e-400">정보</span><span class="sxs-lookup"><span data-stu-id="f610e-400">INFO</span></span>
* <span data-ttu-id="f610e-401">TRACE</span><span class="sxs-lookup"><span data-stu-id="f610e-401">TRACE</span></span>

<span data-ttu-id="f610e-402">위치(여러 위치가 허용됨):</span><span class="sxs-lookup"><span data-stu-id="f610e-402">Locations (multiple locations are permitted):</span></span>

* <span data-ttu-id="f610e-403">CONSOLE</span><span class="sxs-lookup"><span data-stu-id="f610e-403">CONSOLE</span></span>
* <span data-ttu-id="f610e-404">EVENTLOG</span><span class="sxs-lookup"><span data-stu-id="f610e-404">EVENTLOG</span></span>
* <span data-ttu-id="f610e-405">파일</span><span class="sxs-lookup"><span data-stu-id="f610e-405">FILE</span></span>

<span data-ttu-id="f610e-406">처리기 설정은 환경 변수를 통해서도 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-406">The handler settings can also be provided via environment variables:</span></span>

* <span data-ttu-id="f610e-407">`ASPNETCORE_MODULE_DEBUG_FILE` &ndash; 디버그 로그 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-407">`ASPNETCORE_MODULE_DEBUG_FILE` &ndash; Path to the debug log file.</span></span> <span data-ttu-id="f610e-408">(기본값: *aspnetcore-debug.log*)</span><span class="sxs-lookup"><span data-stu-id="f610e-408">(Default: *aspnetcore-debug.log*)</span></span>
* <span data-ttu-id="f610e-409">`ASPNETCORE_MODULE_DEBUG` &ndash; 디버그 수준 설정.</span><span class="sxs-lookup"><span data-stu-id="f610e-409">`ASPNETCORE_MODULE_DEBUG` &ndash; Debug level setting.</span></span>

> [!WARNING]
> <span data-ttu-id="f610e-410">배포에서 문제를 해결하는 데 필요한 시간보다 오래 디버그 로깅을 사용하도록 설정하지 **마세요**.</span><span class="sxs-lookup"><span data-stu-id="f610e-410">Do **not** leave debug logging enabled in the deployment for longer than required to troubleshoot an issue.</span></span> <span data-ttu-id="f610e-411">로그의 크기는 제한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-411">The size of the log isn't limited.</span></span> <span data-ttu-id="f610e-412">디버그 로그를 사용하도록 설정한 대로 두면 사용 가능한 디스크 공간이 소진되어 서버 또는 앱 서비스가 크래시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-412">Leaving the debug log enabled can exhaust the available disk space and crash the server or app service.</span></span>

::: moniker-end

<span data-ttu-id="f610e-413">*web.config* 파일에 있는 `aspNetCore` 요소의 예제에 대해서는 [web.config를 사용한 구성](#configuration-with-webconfig)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f610e-413">See [Configuration with web.config](#configuration-with-webconfig) for an example of the `aspNetCore` element in the *web.config* file.</span></span>

## <a name="proxy-configuration-uses-http-protocol-and-a-pairing-token"></a><span data-ttu-id="f610e-414">프록시 구성은 HTTP 프로토콜 및 페어링 토큰을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-414">Proxy configuration uses HTTP protocol and a pairing token</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="f610e-415">*호스팅에만 적용됩니다.*</span><span class="sxs-lookup"><span data-stu-id="f610e-415">*Only applies to out-of-process hosting.*</span></span>

::: moniker-end

<span data-ttu-id="f610e-416">ASP.NET Core 모듈과 Kestrel 사이에 만들어진 프록시는 HTTP 프로토콜을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-416">The proxy created between the ASP.NET Core Module and Kestrel uses the HTTP protocol.</span></span> <span data-ttu-id="f610e-417">HTTP 사용은 모듈과 Kestrel 간의 트래픽이 네트워크 인터페이스에서 분리된 루프백 주소에서 발생하는 성능 최적화입니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-417">Using HTTP is a performance optimization, where the traffic between the module and Kestrel takes place on a loopback address off of the network interface.</span></span> <span data-ttu-id="f610e-418">서버에서 분리된 위치에서 모듈과 Kestrel 간 트래픽 도청의 위험은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-418">There's no risk of eavesdropping the traffic between the module and Kestrel from a location off of the server.</span></span>

<span data-ttu-id="f610e-419">페어링 토큰은 Kestrel에서 받은 요청이 IIS에서 프록시되었으며 다른 원본에서 오지 않았다는 것을 보장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-419">A pairing token is used to guarantee that the requests received by Kestrel were proxied by IIS and didn't come from some other source.</span></span> <span data-ttu-id="f610e-420">페어링 토큰은 모듈에 의해 생성되며 환경 변수(`ASPNETCORE_TOKEN`)로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-420">The pairing token is created and set into an environment variable (`ASPNETCORE_TOKEN`) by the module.</span></span> <span data-ttu-id="f610e-421">페어링 토큰은 프록시된 모든 요청에서 헤더(`MS-ASPNETCORE-TOKEN`)로도 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-421">The pairing token is also set into a header (`MS-ASPNETCORE-TOKEN`) on every proxied request.</span></span> <span data-ttu-id="f610e-422">IIS 미들웨어는 수신하는 각 요청을 검사하여 페어링 토큰 헤더 값이 환경 변수 값과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-422">IIS Middleware checks each request it receives to confirm that the pairing token header value matches the environment variable value.</span></span> <span data-ttu-id="f610e-423">토큰 값이 일치하지 않는 경우 요청이 기록되고 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-423">If the token values are mismatched, the request is logged and rejected.</span></span> <span data-ttu-id="f610e-424">페어링 토큰 환경 변수와 모듈과 Kestrel 간의 트래픽은 서버에서 분리된 위치에서 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-424">The pairing token environment variable and the traffic between the module and Kestrel aren't accessible from a location off of the server.</span></span> <span data-ttu-id="f610e-425">페어링 토큰 값을 알지 못하면 공격자는 IIS 미들웨어에서 검사를 무시하는 요청을 전송할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-425">Without knowing the pairing token value, an attacker can't submit requests that bypass the check in the IIS Middleware.</span></span>

## <a name="aspnet-core-module-with-an-iis-shared-configuration"></a><span data-ttu-id="f610e-426">IIS 공유 구성이 포함된 ASP.NET Core 모듈</span><span class="sxs-lookup"><span data-stu-id="f610e-426">ASP.NET Core Module with an IIS Shared Configuration</span></span>

<span data-ttu-id="f610e-427">ASP.NET Core 모듈 설치 관리자는 **SYSTEM** 계정의 권한으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-427">The ASP.NET Core Module installer runs with the privileges of the **SYSTEM** account.</span></span> <span data-ttu-id="f610e-428">로컬 시스템 계정에는 IIS 공유 구성에서 사용하는 공유 경로에 대한 수정 권한이 없으므로 공유의 *applicationHost.config*에서 모듈 설정을 구성하려고 하면 설치 관리자에서 액세스 거부 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-428">Because the local system account doesn't have modify permission for the share path used by the IIS Shared Configuration, the installer hits an access denied error when attempting to configure the module settings in *applicationHost.config* on the share.</span></span> <span data-ttu-id="f610e-429">IIS 공유 구성을 사용할 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-429">When using an IIS Shared Configuration, follow these steps:</span></span>

1. <span data-ttu-id="f610e-430">IIS 공유 구성을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-430">Disable the IIS Shared Configuration.</span></span>
1. <span data-ttu-id="f610e-431">설치 관리자를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-431">Run the installer.</span></span>
1. <span data-ttu-id="f610e-432">업데이트된 *applicationHost.config* 파일을 공유로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-432">Export the updated *applicationHost.config* file to the share.</span></span>
1. <span data-ttu-id="f610e-433">IIS 공유 구성을 다시 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-433">Re-enable the IIS Shared Configuration.</span></span>

## <a name="module-version-and-hosting-bundle-installer-logs"></a><span data-ttu-id="f610e-434">모듈 버전 및 호스팅 번들 설치 관리자 로그</span><span class="sxs-lookup"><span data-stu-id="f610e-434">Module version and Hosting Bundle installer logs</span></span>

<span data-ttu-id="f610e-435">설치된 ASP.NET Core 모듈의 버전을 확인하려면:</span><span class="sxs-lookup"><span data-stu-id="f610e-435">To determine the version of the installed ASP.NET Core Module:</span></span>

1. <span data-ttu-id="f610e-436">호스팅 시스템에서 *%windir%\System32\inetsrv*로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-436">On the hosting system, navigate to *%windir%\System32\inetsrv*.</span></span>
1. <span data-ttu-id="f610e-437">*aspnetcore.dll* 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-437">Locate the *aspnetcore.dll* file.</span></span>
1. <span data-ttu-id="f610e-438">파일을 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-438">Right-click the file and select **Properties** from the contextual menu.</span></span>
1. <span data-ttu-id="f610e-439">**세부 정보** 탭을 선택합니다. **파일 버전** 및 **제품 버전**은 설치된 모듈 버전을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-439">Select the **Details** tab. The **File version** and **Product version** represent the installed version of the module.</span></span>

<span data-ttu-id="f610e-440">모듈에 대한 호스팅 번들 설치 관리자 로그는 *C:\\Users\\%UserName%\\AppData\\Local\\Temp*에 있습니다. 파일 이름은 *dd_DotNetCoreWinSvrHosting__\<timestamp>_000_AspNetCoreModule_x64.log*로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-440">The Hosting Bundle installer logs for the module are found at *C:\\Users\\%UserName%\\AppData\\Local\\Temp*. The file is named *dd_DotNetCoreWinSvrHosting__\<timestamp>_000_AspNetCoreModule_x64.log*.</span></span>

## <a name="module-schema-and-configuration-file-locations"></a><span data-ttu-id="f610e-441">모듈, 스키마 및 구성 파일 위치</span><span class="sxs-lookup"><span data-stu-id="f610e-441">Module, schema, and configuration file locations</span></span>

### <a name="module"></a><span data-ttu-id="f610e-442">Module</span><span class="sxs-lookup"><span data-stu-id="f610e-442">Module</span></span>

<span data-ttu-id="f610e-443">**IIS(x86/amd64):**</span><span class="sxs-lookup"><span data-stu-id="f610e-443">**IIS (x86/amd64):**</span></span>

   * <span data-ttu-id="f610e-444">%windir%\System32\inetsrv\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="f610e-444">%windir%\System32\inetsrv\aspnetcore.dll</span></span>

   * <span data-ttu-id="f610e-445">%windir%\SysWOW64\inetsrv\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="f610e-445">%windir%\SysWOW64\inetsrv\aspnetcore.dll</span></span>

::: moniker range=">= aspnetcore-2.2"

   * <span data-ttu-id="f610e-446">%ProgramFiles%\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll</span><span class="sxs-lookup"><span data-stu-id="f610e-446">%ProgramFiles%\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll</span></span>

   * <span data-ttu-id="f610e-447">%ProgramFiles(x86)%\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll</span><span class="sxs-lookup"><span data-stu-id="f610e-447">%ProgramFiles(x86)%\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll</span></span>

::: moniker-end

<span data-ttu-id="f610e-448">**IIS Express(x86/amd64):**</span><span class="sxs-lookup"><span data-stu-id="f610e-448">**IIS Express (x86/amd64):**</span></span>

   * <span data-ttu-id="f610e-449">%ProgramFiles%\IIS Express\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="f610e-449">%ProgramFiles%\IIS Express\aspnetcore.dll</span></span>

   * <span data-ttu-id="f610e-450">%ProgramFiles(x86)%\IIS Express\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="f610e-450">%ProgramFiles(x86)%\IIS Express\aspnetcore.dll</span></span>

::: moniker range=">= aspnetcore-2.2"

   * <span data-ttu-id="f610e-451">%ProgramFiles%\IIS Express\Asp.Net Core Module\V2\aspnetcorev2.dll</span><span class="sxs-lookup"><span data-stu-id="f610e-451">%ProgramFiles%\IIS Express\Asp.Net Core Module\V2\aspnetcorev2.dll</span></span>

   * <span data-ttu-id="f610e-452">%ProgramFiles(x86)%\IIS Express\Asp.Net Core Module\V2\aspnetcorev2.dll</span><span class="sxs-lookup"><span data-stu-id="f610e-452">%ProgramFiles(x86)%\IIS Express\Asp.Net Core Module\V2\aspnetcorev2.dll</span></span>

::: moniker-end

### <a name="schema"></a><span data-ttu-id="f610e-453">스키마</span><span class="sxs-lookup"><span data-stu-id="f610e-453">Schema</span></span>

<span data-ttu-id="f610e-454">**IIS**</span><span class="sxs-lookup"><span data-stu-id="f610e-454">**IIS**</span></span>

   * <span data-ttu-id="f610e-455">%windir%\System32\inetsrv\config\schema\aspnetcore_schema.xml</span><span class="sxs-lookup"><span data-stu-id="f610e-455">%windir%\System32\inetsrv\config\schema\aspnetcore_schema.xml</span></span>

::: moniker range=">= aspnetcore-2.2"

   * <span data-ttu-id="f610e-456">%windir%\System32\inetsrv\config\schema\aspnetcore_schema_v2.xml</span><span class="sxs-lookup"><span data-stu-id="f610e-456">%windir%\System32\inetsrv\config\schema\aspnetcore_schema_v2.xml</span></span>

::: moniker-end
<span data-ttu-id="f610e-457">**IIS Express**</span><span class="sxs-lookup"><span data-stu-id="f610e-457">**IIS Express**</span></span>

   * <span data-ttu-id="f610e-458">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema.xml</span><span class="sxs-lookup"><span data-stu-id="f610e-458">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema.xml</span></span>

::: moniker range=">= aspnetcore-2.2"

   * <span data-ttu-id="f610e-459">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema_v2.xml</span><span class="sxs-lookup"><span data-stu-id="f610e-459">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema_v2.xml</span></span>

::: moniker-end

### <a name="configuration"></a><span data-ttu-id="f610e-460">구성</span><span class="sxs-lookup"><span data-stu-id="f610e-460">Configuration</span></span>

<span data-ttu-id="f610e-461">**IIS**</span><span class="sxs-lookup"><span data-stu-id="f610e-461">**IIS**</span></span>

   * <span data-ttu-id="f610e-462">%windir%\System32\inetsrv\config\applicationHost.config</span><span class="sxs-lookup"><span data-stu-id="f610e-462">%windir%\System32\inetsrv\config\applicationHost.config</span></span>

<span data-ttu-id="f610e-463">**IIS Express**</span><span class="sxs-lookup"><span data-stu-id="f610e-463">**IIS Express**</span></span>

   * <span data-ttu-id="f610e-464">%ProgramFiles%\IIS Express\config\templates\PersonalWebServer\applicationHost.config</span><span class="sxs-lookup"><span data-stu-id="f610e-464">%ProgramFiles%\IIS Express\config\templates\PersonalWebServer\applicationHost.config</span></span>

<span data-ttu-id="f610e-465">*applicationHost.config* 파일에서 *aspnetcore*를 검색하여 파일을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f610e-465">The files can be found by searching for *aspnetcore* in the *applicationHost.config* file.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f610e-466">추가 자료</span><span class="sxs-lookup"><span data-stu-id="f610e-466">Additional resources</span></span>

* <xref:host-and-deploy/iis/index>
* [<span data-ttu-id="f610e-467">ASP.NET Core 모듈 GitHub 리포지토리(참조 소스)</span><span class="sxs-lookup"><span data-stu-id="f610e-467">ASP.NET Core Module GitHub repository (reference source)</span></span>](https://github.com/aspnet/AspNetCoreModule)
* <xref:host-and-deploy/iis/modules>