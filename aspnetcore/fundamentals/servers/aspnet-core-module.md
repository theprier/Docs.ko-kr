---
title: ASP.NET Core 모듈
author: guardrex
description: ASP.NET Core 모듈이 Kestrel 웹 서버에서 IIS 또는 IIS Express를 사용하도록 허용하는 방법을 알아봅니다.
ms.author: tdykstra
ms.custom: mvc
ms.date: 11/30/2018
uid: fundamentals/servers/aspnet-core-module
ms.openlocfilehash: d3f3a42dd7aebc425905b865376a584bcf0e5153
ms.sourcegitcommit: 9bb58d7c8dad4bbd03419bcc183d027667fefa20
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/04/2018
ms.locfileid: "52861461"
---
# <a name="aspnet-core-module"></a><span data-ttu-id="ae666-103">ASP.NET Core 모듈</span><span class="sxs-lookup"><span data-stu-id="ae666-103">ASP.NET Core Module</span></span>

<span data-ttu-id="ae666-104">작성자: [Tom Dykstra](https://github.com/tdykstra), [Rick Strahl](https://github.com/RickStrahl) 및 [Chris Ross](https://github.com/Tratcher)</span><span class="sxs-lookup"><span data-stu-id="ae666-104">By [Tom Dykstra](https://github.com/tdykstra), [Rick Strahl](https://github.com/RickStrahl), and [Chris Ross](https://github.com/Tratcher)</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="ae666-105">ASP.NET Core 모듈을 사용하면 ASP.NET Core 앱을 IIS 작업자 프로세스에서(*In-Process*) 또는 역방향 프록시 구성의 IIS 뒤에서(*Out-of-Process*) 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-105">The ASP.NET Core Module allows ASP.NET Core apps to run in an IIS worker process (*in-process*) or behind IIS in a reverse proxy configuration (*out-of-process*).</span></span> <span data-ttu-id="ae666-106">IIS는 고급 웹앱 보안 및 관리 효율성 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-106">IIS provides advanced web app security and manageability features.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="ae666-107">ASP.NET Core 모듈은 역방향 프록시 구성에서 ASP.NET Core 앱을 IIS 뒤에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-107">The ASP.NET Core Module allows ASP.NET Core apps to run behind IIS in a reverse proxy configuration.</span></span> <span data-ttu-id="ae666-108">IIS는 고급 웹앱 보안 및 관리 효율성 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-108">IIS provides advanced web app security and manageability features.</span></span>

::: moniker-end

<span data-ttu-id="ae666-109">지원되는 Windows 버전:</span><span class="sxs-lookup"><span data-stu-id="ae666-109">Supported Windows versions:</span></span>

* <span data-ttu-id="ae666-110">Windows 7 이상</span><span class="sxs-lookup"><span data-stu-id="ae666-110">Windows 7 or later</span></span>
* <span data-ttu-id="ae666-111">Windows Server 2008 R2 이상</span><span class="sxs-lookup"><span data-stu-id="ae666-111">Windows Server 2008 R2 or later</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="ae666-112">In Process를 호스트하는 경우 모듈에서는 IIS In Process 서버 구현, IIS HTTP Server(`IISHttpServer`)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-112">When hosting in-process, the module uses an IIS in-process server implementation, IIS HTTP Server (`IISHttpServer`).</span></span>

<span data-ttu-id="ae666-113">Out-of-Process로 호스트하는 경우 모듈은 Kestrel에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-113">When hosting out-of-process, the module only works with Kestrel.</span></span> <span data-ttu-id="ae666-114">이 모듈은 [HTTP.sys](xref:fundamentals/servers/httpsys)(이전 명칭 [WebListener](xref:fundamentals/servers/weblistener))와 호환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-114">The module is incompatible with [HTTP.sys](xref:fundamentals/servers/httpsys) (formerly called [WebListener](xref:fundamentals/servers/weblistener)).</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="ae666-115">모듈은 Kestrel에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-115">The module only works with Kestrel.</span></span> <span data-ttu-id="ae666-116">이 모듈은 [HTTP.sys](xref:fundamentals/servers/httpsys)(이전 명칭 [WebListener](xref:fundamentals/servers/weblistener))와 호환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-116">The module is incompatible with [HTTP.sys](xref:fundamentals/servers/httpsys) (formerly called [WebListener](xref:fundamentals/servers/weblistener)).</span></span>

::: moniker-end

## <a name="aspnet-core-module-description"></a><span data-ttu-id="ae666-117">ASP.NET Core 모듈 설명</span><span class="sxs-lookup"><span data-stu-id="ae666-117">ASP.NET Core Module description</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="ae666-118">ASP.NET Core 모듈은 다음을 위해 IIS 파이프라인에 연결되는 네이티브 IIS 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-118">The ASP.NET Core Module is a native IIS module that plugs into the IIS pipeline to either:</span></span>

* <span data-ttu-id="ae666-119">IIS 작업자 프로세스(`w3wp.exe`) 내부에 ASP.NET Core 앱을 호스트하며 [In-Process 호스팅 모델](#in-process-hosting-model)이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-119">Host an ASP.NET Core app inside of the IIS worker process (`w3wp.exe`), called the [in-process hosting model](#in-process-hosting-model).</span></span>

* <span data-ttu-id="ae666-120">[Kestrel 서버](xref:fundamentals/servers/kestrel)를 실행하는 백 엔드 ASP.NET Core 앱으로 웹 요청을 전달하며 [Out-of-Process 호스팅 모델](#out-of-process-hosting-model)이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-120">Forward web requests to a backend ASP.NET Core app running the [Kestrel server](xref:fundamentals/servers/kestrel), called the [out-of-process hosting model](#out-of-process-hosting-model).</span></span>

### <a name="in-process-hosting-model"></a><span data-ttu-id="ae666-121">In-Process 호스팅 모델</span><span class="sxs-lookup"><span data-stu-id="ae666-121">In-process hosting model</span></span>

<span data-ttu-id="ae666-122">In-Process 호스팅을 사용하면 ASP.NET Core 앱은 IIS 작업자 프로세스와 동일한 프로세스에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-122">Using in-process hosting, an ASP.NET Core app runs in the same process as its IIS worker process.</span></span> <span data-ttu-id="ae666-123">이 경우 Out-of-Process 호스팅 모델을 사용할 때 나타나는 루프백 어댑터로 인한 프록시 요청 성능 저하 문제가 해결됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-123">This removes the performance penalty of proxying requests over the loopback adapter when using the out-of-process hosting model.</span></span> <span data-ttu-id="ae666-124">IIS는 [Windows Process Activation Service(WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was)를 사용하여 프로세스 관리를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-124">IIS handles process management with the [Windows Process Activation Service (WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was).</span></span>

<span data-ttu-id="ae666-125">ASP.NET Core 모듈:</span><span class="sxs-lookup"><span data-stu-id="ae666-125">The ASP.NET Core Module:</span></span>

* <span data-ttu-id="ae666-126">앱 초기화를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-126">Performs app initialization.</span></span>
  * <span data-ttu-id="ae666-127">[CoreCLR](/dotnet/standard/glossary#coreclr)을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-127">Loads the [CoreCLR](/dotnet/standard/glossary#coreclr).</span></span>
  * <span data-ttu-id="ae666-128">`Program.Main`.</span><span class="sxs-lookup"><span data-stu-id="ae666-128">Calls `Program.Main`.</span></span>
* <span data-ttu-id="ae666-129">IIS 네이티브 요청의 수명을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-129">Handles the lifetime of the IIS native request.</span></span>

<span data-ttu-id="ae666-130">다음 다이어그램은 IIS, ASP.NET Core 모듈 및 In-Process에 호스트된 앱 간의 관계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-130">The following diagram illustrates the relationship between IIS, the ASP.NET Core Module, and an app hosted in-process:</span></span>

![ASP.NET Core 모듈](aspnet-core-module/_static/ancm-inprocess.png)

<span data-ttu-id="ae666-132">요청은 웹에서 커널 모드 HTTP.sys 드라이버로 도착합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-132">A request arrives from the web to the kernel-mode HTTP.sys driver.</span></span> <span data-ttu-id="ae666-133">드라이버는 웹 사이트의 구성된 포트[일반적으로 80(HTTP) 또는 443(HTTPS)]에서 IIS로 네이티브 요청을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-133">The driver routes the native request to IIS on the website's configured port, usually 80 (HTTP) or 443 (HTTPS).</span></span> <span data-ttu-id="ae666-134">모듈에서는 기본 요청을 수신하고 IIS HTTP Server(`IISHttpServer`)에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-134">The module receives the native request and passes it to IIS HTTP Server (`IISHttpServer`).</span></span> <span data-ttu-id="ae666-135">IIS HTTP Server는 기본 요청을 관리 요청으로 변환하는 IIS In-process 서버 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-135">IIS HTTP Server is an IIS in-process server implementation that converts the request from native to managed.</span></span>

<span data-ttu-id="ae666-136">IIS HTTP Server가 요청을 처리하면 해당 요청이 ASP.NET Core 미들웨어 파이프라인에 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-136">After the IIS HTTP Server processes the request, the request is pushed into the ASP.NET Core middleware pipeline.</span></span> <span data-ttu-id="ae666-137">미들웨어 파이프라인은 요청을 처리하고 앱의 논리에 `HttpContext` 인스턴스로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-137">The middleware pipeline handles the request and passes it on as an `HttpContext` instance to the app's logic.</span></span> <span data-ttu-id="ae666-138">앱의 응답은 IIS로 다시 전달되고, 요청을 시작한 클라이언트에 다시 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-138">The app's response is passed back to IIS, which pushes it back out to the client that initiated the request.</span></span>

### <a name="out-of-process-hosting-model"></a><span data-ttu-id="ae666-139">Out-of-Process 호스팅 모델</span><span class="sxs-lookup"><span data-stu-id="ae666-139">Out-of-process hosting model</span></span>

<span data-ttu-id="ae666-140">ASP.NET Core 앱은 IIS 작업자 프로세스와 별도의 프로세스에서 실행되므로 이 모듈은 프로세스 관리를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-140">Because ASP.NET Core apps run in a process separate from the IIS worker process, the module handles process management.</span></span> <span data-ttu-id="ae666-141">이 모듈은 첫 번째 요청이 들어올 때 ASP.NET Core 앱용 프로세스를 시작하고 종료되거나 충돌이 발생하면 앱을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-141">The module starts the process for the ASP.NET Core app when the first request arrives and restarts the app if it shuts down or crashes.</span></span> <span data-ttu-id="ae666-142">이는 [Windows Process Activation Service(WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was)로 관리되는 In-Process로 실행되는 앱에서 볼 수 있는 동작과 기본적으로 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-142">This is essentially the same behavior as seen with apps that run in-process that are managed by the [Windows Process Activation Service (WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was).</span></span>

<span data-ttu-id="ae666-143">다음 다이어그램은 IIS, ASP.NET Core 모듈 및 Out-of-Process에 호스트된 앱 간의 관계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-143">The following diagram illustrates the relationship between IIS, the ASP.NET Core Module, and an app hosted out-of-process:</span></span>

![ASP.NET Core 모듈](aspnet-core-module/_static/ancm-outofprocess.png)

<span data-ttu-id="ae666-145">요청은 웹에서 커널 모드 HTTP.sys 드라이버로 도착합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-145">Requests arrive from the web to the kernel-mode HTTP.sys driver.</span></span> <span data-ttu-id="ae666-146">드라이버는 웹 사이트의 구성된 포트(일반적으로 80(HTTP) 또는 443(HTTPS))에서 IIS로 요청을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-146">The driver routes the requests to IIS on the website's configured port, usually 80 (HTTP) or 443 (HTTPS).</span></span> <span data-ttu-id="ae666-147">모듈은 포트 80/443이 아닌 앱의 임의의 포트에서 Kestrel로 요청을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-147">The module forwards the requests to Kestrel on a random port for the app, which isn't port 80/443.</span></span>

<span data-ttu-id="ae666-148">모듈은 시작 시 환경 변수를 통해 포트를 지정하고 IIS 통합 미들웨어는 `http://localhost:{port}`에서 수신 대기하도록 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-148">The module specifies the port via an environment variable at startup, and the IIS Integration Middleware configures the server to listen on `http://localhost:{port}`.</span></span> <span data-ttu-id="ae666-149">추가 검사가 수행되고 모듈에서 시작되지 않은 요청은 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-149">Additional checks are performed, and requests that don't originate from the module are rejected.</span></span> <span data-ttu-id="ae666-150">모듈은 HTTPS 전달을 지원하지 않으므로 HTTPS를 통해 IIS에서 수신된 경우에도 HTTP를 통해 요청이 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-150">The module doesn't support HTTPS forwarding, so requests are forwarded over HTTP even if received by IIS over HTTPS.</span></span>

<span data-ttu-id="ae666-151">Kestrel이 모듈에서 요청을 선택한 후, 요청은 ASP.NET Core 미들웨어 파이프라인으로 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-151">After Kestrel picks up the request from the module, the request is pushed into the ASP.NET Core middleware pipeline.</span></span> <span data-ttu-id="ae666-152">미들웨어 파이프라인은 요청을 처리하고 앱의 논리에 `HttpContext` 인스턴스로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-152">The middleware pipeline handles the request and passes it on as an `HttpContext` instance to the app's logic.</span></span> <span data-ttu-id="ae666-153">IIS 통합에 의해 추가된 미들웨어는 체계, 원격 IP 및 경로 기준을 Kestrel에 요청을 전달하기 위한 계정으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-153">Middleware added by IIS Integration updates the scheme, remote IP, and pathbase to account for forwarding the request to Kestrel.</span></span> <span data-ttu-id="ae666-154">앱의 응답은 IIS로 다시 전달되고, 요청을 시작한 HTTP 클라이언트에 다시 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-154">The app's response is passed back to IIS, which pushes it back out to the HTTP client that initiated the request.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="ae666-155">ASP.NET Core 모듈은 백 엔드 ASP.NET Core 앱으로 웹 요청을 전달하는 IIS 파이프라인에 연결되는 네이티브 IIS 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-155">The ASP.NET Core Module is a native IIS module that plugs into the IIS pipeline to forward web requests to backend ASP.NET Core apps.</span></span>

<span data-ttu-id="ae666-156">ASP.NET Core 앱은 IIS 작업자 프로세스와 별도의 프로세스에서 실행되므로 이 모듈은 프로세스 관리도 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-156">Because ASP.NET Core apps run in a process separate from the IIS worker process, the module also handles process management.</span></span> <span data-ttu-id="ae666-157">이 모듈은 첫 번째 요청이 들어올 때 ASP.NET Core 앱용 프로세스를 시작하고 충돌이 발생하면 앱을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-157">The module starts the process for the ASP.NET Core app when the first request arrives and restarts the app if it crashes.</span></span> <span data-ttu-id="ae666-158">이는 [Windows Process Activation Service(WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was)로 관리되는 IIS에서 In Process로 실행되는 ASP.NET 4.x 앱에서 볼 수 있는 동작과 기본적으로 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-158">This is essentially the same behavior as seen with ASP.NET 4.x apps that run in-process in IIS that are managed by the [Windows Process Activation Service (WAS)](/iis/manage/provisioning-and-managing-iis/features-of-the-windows-process-activation-service-was).</span></span>

<span data-ttu-id="ae666-159">다음 다이어그램은 IIS, ASP.NET Core 모듈 및 앱 간의 관계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-159">The following diagram illustrates the relationship between IIS, the ASP.NET Core Module, and an app:</span></span>

![ASP.NET Core 모듈](aspnet-core-module/_static/ancm-outofprocess.png)

<span data-ttu-id="ae666-161">요청은 웹에서 커널 모드 HTTP.sys 드라이버로 도착합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-161">Requests arrive from the web to the kernel-mode HTTP.sys driver.</span></span> <span data-ttu-id="ae666-162">드라이버는 웹 사이트의 구성된 포트(일반적으로 80(HTTP) 또는 443(HTTPS))에서 IIS로 요청을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-162">The driver routes the requests to IIS on the website's configured port, usually 80 (HTTP) or 443 (HTTPS).</span></span> <span data-ttu-id="ae666-163">모듈은 포트 80/443이 아닌 앱의 임의의 포트에서 Kestrel로 요청을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-163">The module forwards the requests to Kestrel on a random port for the app, which isn't port 80/443.</span></span>

<span data-ttu-id="ae666-164">모듈은 시작 시 환경 변수를 통해 포트를 지정하고 IIS 통합 미들웨어는 `http://localhost:{port}`에서 수신 대기하도록 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-164">The module specifies the port via an environment variable at startup, and the IIS Integration Middleware configures the server to listen on `http://localhost:{port}`.</span></span> <span data-ttu-id="ae666-165">추가 검사가 수행되고 모듈에서 시작되지 않은 요청은 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-165">Additional checks are performed, and requests that don't originate from the module are rejected.</span></span> <span data-ttu-id="ae666-166">모듈은 HTTPS 전달을 지원하지 않으므로 HTTPS를 통해 IIS에서 수신된 경우에도 HTTP를 통해 요청이 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-166">The module doesn't support HTTPS forwarding, so requests are forwarded over HTTP even if received by IIS over HTTPS.</span></span>

<span data-ttu-id="ae666-167">Kestrel이 모듈에서 요청을 선택한 후, 요청은 ASP.NET Core 미들웨어 파이프라인으로 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-167">After Kestrel picks up the request from the module, the request is pushed into the ASP.NET Core middleware pipeline.</span></span> <span data-ttu-id="ae666-168">미들웨어 파이프라인은 요청을 처리하고 앱의 논리에 `HttpContext` 인스턴스로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-168">The middleware pipeline handles the request and passes it on as an `HttpContext` instance to the app's logic.</span></span> <span data-ttu-id="ae666-169">IIS 통합에 의해 추가된 미들웨어는 체계, 원격 IP 및 경로 기준을 Kestrel에 요청을 전달하기 위한 계정으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-169">Middleware added by IIS Integration updates the scheme, remote IP, and pathbase to account for forwarding the request to Kestrel.</span></span> <span data-ttu-id="ae666-170">앱의 응답은 IIS로 다시 전달되고, 요청을 시작한 HTTP 클라이언트에 다시 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-170">The app's response is passed back to IIS, which pushes it back out to the HTTP client that initiated the request.</span></span>

::: moniker-end

<span data-ttu-id="ae666-171">Windows 인증 등의 많은 네이티브 모듈이 활성 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-171">Many native modules, such as Windows Authentication, remain active.</span></span> <span data-ttu-id="ae666-172">모듈을 사용하여 활성화된 IIS 모듈에 대해 자세히 알아보려면 <xref:host-and-deploy/iis/modules>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae666-172">To learn more about IIS modules active with the module, see <xref:host-and-deploy/iis/modules>.</span></span>

<span data-ttu-id="ae666-173">ASP.NET Core 모듈에는 몇 가지 기타 함수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-173">The ASP.NET Core Module has a few other functions.</span></span> <span data-ttu-id="ae666-174">모듈은 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-174">The module can:</span></span>

* <span data-ttu-id="ae666-175">작업자 프로세스의 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-175">Set environment variables for the worker process.</span></span>
* <span data-ttu-id="ae666-176">시작 문제를 해결하기 위해 stdout 출력을 파일 저장소에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-176">Log stdout output to file storage for troubleshooting startup issues.</span></span>
* <span data-ttu-id="ae666-177">Windows 인증 토큰을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="ae666-177">Forward Windows authentication tokens.</span></span>

## <a name="how-to-install-and-use-the-aspnet-core-module"></a><span data-ttu-id="ae666-178">ASP.NET Core 모듈을 설치하고 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="ae666-178">How to install and use the ASP.NET Core Module</span></span>

<span data-ttu-id="ae666-179">ASP.NET Core 모듈을 설치하고 사용하는 방법에 대한 자세한 지침은 <xref:host-and-deploy/iis/index>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae666-179">For detailed instructions on how to install and use the ASP.NET Core Module, see <xref:host-and-deploy/iis/index>.</span></span> <span data-ttu-id="ae666-180">모듈 구성에 대한 내용은 <xref:host-and-deploy/aspnet-core-module>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae666-180">For information on configuring the module, see the <xref:host-and-deploy/aspnet-core-module>.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ae666-181">추가 자료</span><span class="sxs-lookup"><span data-stu-id="ae666-181">Additional resources</span></span>

* <xref:host-and-deploy/iis/index>
* <xref:host-and-deploy/aspnet-core-module>
* [<span data-ttu-id="ae666-182">ASP.NET Core 모듈 GitHub 리포지토리(소스 코드)</span><span class="sxs-lookup"><span data-stu-id="ae666-182">ASP.NET Core Module GitHub repository (source code)</span></span>](https://github.com/aspnet/AspNetCoreModule)
* <xref:host-and-deploy/iis/modules>
