---
title: ASP.NET Core 모듈 구성 참조
author: guardrex
description: ASP.NET Core 앱을 호스팅하기 위해 ASP.NET Core 모듈을 구성하는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 09/21/2018
uid: host-and-deploy/aspnet-core-module
ms.openlocfilehash: ca86b1548c7c28a64fd391617b2e8290c1c264cf
ms.sourcegitcommit: 09affee3d234cb27ea6fe33bc113b79e68900d22
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51191362"
---
# <a name="aspnet-core-module-configuration-reference"></a><span data-ttu-id="fbe92-103">ASP.NET Core 모듈 구성 참조</span><span class="sxs-lookup"><span data-stu-id="fbe92-103">ASP.NET Core Module configuration reference</span></span>

<span data-ttu-id="fbe92-104">작성자: [Luke Latham](https://github.com/guardrex), [Rick Anderson](https://twitter.com/RickAndMSFT), [Sourabh Shirhatti](https://twitter.com/sshirhatti) 및 [Justin Kotalik](https://github.com/jkotalik)</span><span class="sxs-lookup"><span data-stu-id="fbe92-104">By [Luke Latham](https://github.com/guardrex), [Rick Anderson](https://twitter.com/RickAndMSFT), [Sourabh Shirhatti](https://twitter.com/sshirhatti), and [Justin Kotalik](https://github.com/jkotalik)</span></span>

<span data-ttu-id="fbe92-105">이 문서에서는 ASP.NET Core 앱을 호스트하기 위해 ASP.NET Core 모듈을 구성하는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-105">This document provides instructions on how to configure the ASP.NET Core Module for hosting ASP.NET Core apps.</span></span> <span data-ttu-id="fbe92-106">ASP.NET Core 모듈 및 설치 지침에 대한 개요는 [ASP.NET Core 모듈 개요](xref:fundamentals/servers/aspnet-core-module)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbe92-106">For an introduction to the ASP.NET Core Module and installation instructions, see the [ASP.NET Core Module overview](xref:fundamentals/servers/aspnet-core-module).</span></span>

::: moniker range=">= aspnetcore-2.2"

## <a name="hosting-model"></a><span data-ttu-id="fbe92-107">호스팅 모델</span><span class="sxs-lookup"><span data-stu-id="fbe92-107">Hosting model</span></span>

<span data-ttu-id="fbe92-108">.NET Core 2.2 이상에서 실행되는 앱의 경우, 모듈에서는 역방향 프록시(Out-of-Process) 호스팅과 비교할 때 더 나은 성능을 제공하기 위해 In-Process 호스팅 모델을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-108">For apps running on .NET Core 2.2 or later, the module supports an in-process hosting model for improved performance compared to reverse-proxy (out-of-process) hosting.</span></span> <span data-ttu-id="fbe92-109">자세한 내용은 <xref:fundamentals/servers/aspnet-core-module#aspnet-core-module-description>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbe92-109">For more information, see <xref:fundamentals/servers/aspnet-core-module#aspnet-core-module-description>.</span></span>

<span data-ttu-id="fbe92-110">In-Process 호스팅은 기존 앱에 대한 옵트인(opt in) 기능이지만 [dotnet new](/dotnet/core/tools/dotnet-new) 템플릿은 기본적으로 모든 IIS 및 IIS Express 시나리오에 대해 In-Process 호스팅 모델로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-110">In-procsess hosting is opt-in for existing apps, but [dotnet new](/dotnet/core/tools/dotnet-new) templates default to the in-process hosting model for all IIS and IIS Express scenarios.</span></span>

<span data-ttu-id="fbe92-111">In-Process 호스팅용 앱을 구성하려면 `inprocess`의 값을 사용하여 `<AspNetCoreHostingModel>` 속성을 앱의 프로젝트 파일(예: *MyApp.csproj*)에 추가합니다(Out-of-Process 호스팅은 `outofprocess`로 설정됨).</span><span class="sxs-lookup"><span data-stu-id="fbe92-111">To configure an app for in-process hosting, add the `<AspNetCoreHostingModel>` property to the app's project file (for example, *MyApp.csproj*) with a value of `inprocess` (out-of-process hosting is set with `outofprocess`):</span></span>

```xml
<PropertyGroup>
  <AspNetCoreHostingModel>inprocess</AspNetCoreHostingModel>
</PropertyGroup>
```

<span data-ttu-id="fbe92-112">다음 특성은 In-Process로 호스팅할 때 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-112">The following characteristics apply when hosting in-process:</span></span>

* <span data-ttu-id="fbe92-113">[Kestrel 서버](xref:fundamentals/servers/kestrel)가 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-113">The [Kestrel server](xref:fundamentals/servers/kestrel) isn't used.</span></span> <span data-ttu-id="fbe92-114">사용자 지정 <xref:Microsoft.AspNetCore.Hosting.Server.IServer> 구현인 `IISHttpServer`가 앱의 서버 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-114">A custom <xref:Microsoft.AspNetCore.Hosting.Server.IServer> implementation, `IISHttpServer` acts as the app's server.</span></span>

* <span data-ttu-id="fbe92-115">[requestTimeout 특성](#attributes-of-the-aspnetcore-element)이 In-Process 호스팅에 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-115">The [requestTimeout attribute](#attributes-of-the-aspnetcore-element) doesn't apply to in-process hosting.</span></span>

* <span data-ttu-id="fbe92-116">앱 간의 앱 풀 공유는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-116">Sharing an app pool among apps isn't supported.</span></span> <span data-ttu-id="fbe92-117">앱당 하나의 앱 풀을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-117">Use one app pool per app.</span></span>

* <span data-ttu-id="fbe92-118">[웹 배포](/iis/publish/using-web-deploy/introduction-to-web-deploy)를 사용하거나 [app_offline.htm 파일을 배포에](xref:host-and-deploy/iis/index#locked-deployment-files) 수동으로 배치할 경우 열린 연결이 있으면 앱이 즉시 종료되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-118">When using [Web Deploy](/iis/publish/using-web-deploy/introduction-to-web-deploy) or manually placing an [app_offline.htm file in the deployment](xref:host-and-deploy/iis/index#locked-deployment-files), the app might not shut down immediately if there's an open connection.</span></span> <span data-ttu-id="fbe92-119">예를 들어, WebSocket 연결은 앱 종료를 지연시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-119">For example, a websocket connection may delay app shut down.</span></span>

* <span data-ttu-id="fbe92-120">앱 및 설치된 런타임(x64 또는 x86)의 아키텍처(비트)는 앱 풀의 아키텍처와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-120">The architecture (bitness) of the app and installed runtime (x64 or x86) must match the architecture of the app pool.</span></span>

* <span data-ttu-id="fbe92-121">`WebHostBuilder`([CreateDefaultBuilder](xref:fundamentals/host/web-host#set-up-a-host)를 사용하지 않고)를 사용하여 앱 호스트를 수동으로 설정하며 앱이 Kestrel 서버에서 직접 실행되는 경우(자체 호스트됨) `UseIISIntegration`를 호출하기 전에 `UseKestrel`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-121">If setting up the app's host manually with `WebHostBuilder` (not using [CreateDefaultBuilder](xref:fundamentals/host/web-host#set-up-a-host)) and the app is ever run directly on the Kestrel server (self-hosted), call `UseKestrel` before calling `UseIISIntegration`.</span></span> <span data-ttu-id="fbe92-122">이 순서가 바뀌면 호스트가 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-122">If the order is reversed, the host fails to start.</span></span>

* <span data-ttu-id="fbe92-123">클라이언트의 연결 끊김이 검색되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-123">Client disconnects are detected.</span></span> <span data-ttu-id="fbe92-124">클라이언트의 연결이 끊어지면 [HttpContext.RequestAborted](xref:Microsoft.AspNetCore.Http.HttpContext.RequestAborted*) 취소 토큰이 취소됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-124">The [HttpContext.RequestAborted](xref:Microsoft.AspNetCore.Http.HttpContext.RequestAborted*) cancellation token is cancelled when the client disconnects.</span></span>

* <span data-ttu-id="fbe92-125">`Directory.GetCurrentDirectory()`는 애플리케이션 디렉터리가 아닌 IIS에 의해 시작된 프로세스의 작업자 디렉터리를 반환합니다(예: *w3wp.exe*에 대한 *C:\Windows\System32\inetsrv*).</span><span class="sxs-lookup"><span data-stu-id="fbe92-125">`Directory.GetCurrentDirectory()` returns the worker directory of the process started by IIS rather than the application directory (for example, *C:\Windows\System32\inetsrv* for *w3wp.exe*).</span></span>

### <a name="hosting-model-changes"></a><span data-ttu-id="fbe92-126">호스팅 모델 변경</span><span class="sxs-lookup"><span data-stu-id="fbe92-126">Hosting model changes</span></span>

<span data-ttu-id="fbe92-127">`hostingModel` 설정이 *web.config* 파일에서 변경되면([web.config로 구성](#configuration-with-webconfig) 섹션에 설명되어 있음) 모듈은 IIS에 대한 작업자 프로세스를 재순환합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-127">If the `hostingModel` setting is changed in the *web.config* file (explained in the [Configuration with web.config](#configuration-with-webconfig) section), the module recycles the worker process for IIS.</span></span>

<span data-ttu-id="fbe92-128">IIS Express의 경우 모듈은 작업자 프로세스를 재순환하지 않고, 대신 현재 IIS Express 프로세스의 정상 종료를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-128">For IIS Express, the module doesn't recycle the worker process but instead triggers a graceful shutdown of the current IIS Express process.</span></span> <span data-ttu-id="fbe92-129">앱에 대한 다음 요청은 새 IIS Express 프로세스를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-129">The next request to the app spawns a new IIS Express process.</span></span>

### <a name="process-name"></a><span data-ttu-id="fbe92-130">프로세스 이름</span><span class="sxs-lookup"><span data-stu-id="fbe92-130">Process name</span></span>

<span data-ttu-id="fbe92-131">`Process.GetCurrentProcess().ProcessName`은 `w3wp`/`iisexpress`(In-Process) 또는 `dotnet`(Out-of-Process)을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-131">`Process.GetCurrentProcess().ProcessName` reports `w3wp`/`iisexpress` (in-process) or `dotnet` (out-of-process).</span></span>

::: moniker-end

## <a name="configuration-with-webconfig"></a><span data-ttu-id="fbe92-132">web.config를 사용한 구성</span><span class="sxs-lookup"><span data-stu-id="fbe92-132">Configuration with web.config</span></span>

<span data-ttu-id="fbe92-133">ASP.NET Core 모듈은 사이트의 *web.config* 파일에 있는 `system.webServer` 노드의 `aspNetCore` 섹션으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-133">The ASP.NET Core Module is configured with the `aspNetCore` section of the `system.webServer` node in the site's *web.config* file.</span></span>

<span data-ttu-id="fbe92-134">다음 *web.config* 파일은 [프레임워크 종속 배포](/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd)를 위해 게시되고 사이트 요청을 처리하도록 ASP.NET Core 모듈을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-134">The following *web.config* file is published for a [framework-dependent deployment](/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd) and configures the ASP.NET Core Module to handle site requests:</span></span>

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
                  hostingModel="inprocess" />
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

<span data-ttu-id="fbe92-135">다음 *web.config*는 [자체 포함 배포](/dotnet/articles/core/deploying/#self-contained-deployments-scd)를 위해 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-135">The following *web.config* is published for a [self-contained deployment](/dotnet/articles/core/deploying/#self-contained-deployments-scd):</span></span>

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
                  hostingModel="inprocess" />
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
    <aspNetCore processPath=".\MyApp.exe" 
                stdoutLogEnabled="false" 
                stdoutLogFile=".\logs\stdout" />
  </system.webServer>
</configuration>
```

::: moniker-end

<span data-ttu-id="fbe92-136">앱이 [Azure App Service](https://azure.microsoft.com/services/app-service/)에 배포되면 `stdoutLogFile` 경로가 `\\?\%home%\LogFiles\stdout`로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-136">When an app is deployed to [Azure App Service](https://azure.microsoft.com/services/app-service/), the `stdoutLogFile` path is set to `\\?\%home%\LogFiles\stdout`.</span></span> <span data-ttu-id="fbe92-137">이 경로는 서비스에서 자동으로 만들어진 위치인 *LogFiles* 폴더에 stdout 로그를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-137">The path saves stdout logs to the *LogFiles* folder, which is a location automatically created by the service.</span></span>

<span data-ttu-id="fbe92-138">하위 앱에서 *web.config* 파일의 구성에 관한 중요 참고 사항은 [하위 응용 프로그램 구성](xref:host-and-deploy/iis/index#sub-application-configuration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbe92-138">See [Sub-application configuration](xref:host-and-deploy/iis/index#sub-application-configuration) for an important note pertaining to the configuration of *web.config* files in sub-apps.</span></span>

### <a name="attributes-of-the-aspnetcore-element"></a><span data-ttu-id="fbe92-139">aspNetCore 요소의 특성</span><span class="sxs-lookup"><span data-stu-id="fbe92-139">Attributes of the aspNetCore element</span></span>

::: moniker range=">= aspnetcore-2.2"

| <span data-ttu-id="fbe92-140">특성</span><span class="sxs-lookup"><span data-stu-id="fbe92-140">Attribute</span></span> | <span data-ttu-id="fbe92-141">설명</span><span class="sxs-lookup"><span data-stu-id="fbe92-141">Description</span></span> | <span data-ttu-id="fbe92-142">기본</span><span class="sxs-lookup"><span data-stu-id="fbe92-142">Default</span></span> |
| --------- | ----------- | :-----: |
| `arguments` | <p><span data-ttu-id="fbe92-143">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-143">Optional string attribute.</span></span></p><p><span data-ttu-id="fbe92-144">**processPath**에 지정된 실행 파일에 대한 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-144">Arguments to the executable specified in **processPath**.</span></span></p> | |
| `disableStartUpErrorPage` | <p><span data-ttu-id="fbe92-145">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-145">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="fbe92-146">true인 경우 **502.5 - 프로세스 실패** 페이지가 표시되지 않고 *web.config*에 구성된 502 상태 코드 페이지가 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-146">If true, the **502.5 - Process Failure** page is suppressed, and the 502 status code page configured in the *web.config* takes precedence.</span></span></p> | `false` |
| `forwardWindowsAuthToken` | <p><span data-ttu-id="fbe92-147">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-147">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="fbe92-148">true인 경우 토큰은 %ASPNETCORE_PORT%에서 수신 대기하는 자식 프로세스에 요청별 헤더 'MS-ASPNETCORE-WINAUTHTOKEN'으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-148">If true, the token is forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="fbe92-149">이 프로세스는 요청별로 이 토큰에서 CloseHandle을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-149">It's the responsibility of that process to call CloseHandle on this token per request.</span></span></p> | `true` |
| `hostingModel` | <p><span data-ttu-id="fbe92-150">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-150">Optional string attribute.</span></span></p><p><span data-ttu-id="fbe92-151">호스팅 모델을 In-Process(`inprocess`) 또는 Out-of-Process(`outofprocess`)로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-151">Specifies the hosting model as in-process (`inprocess`) or out-of-process (`outofprocess`).</span></span></p> | `outofprocess` |
| `processesPerApplication` | <p><span data-ttu-id="fbe92-152">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-152">Optional integer attribute.</span></span></p><p><span data-ttu-id="fbe92-153">앱별로 스핀 업할 수 있는 **processPath** 설정에 지정된 프로세스의 인스턴스 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-153">Specifies the number of instances of the process specified in the **processPath** setting that can be spun up per app.</span></span></p><p><span data-ttu-id="fbe92-154">&dagger;In-Process 호스팅의 경우 이 값은 `1`로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-154">&dagger;For in-process hosting, the value is limited to `1`.</span></span></p> | <span data-ttu-id="fbe92-155">기본값: `1`</span><span class="sxs-lookup"><span data-stu-id="fbe92-155">Default: `1`</span></span><br><span data-ttu-id="fbe92-156">최소: `1`</span><span class="sxs-lookup"><span data-stu-id="fbe92-156">Min: `1`</span></span><br><span data-ttu-id="fbe92-157">최대: `100`&dagger;</span><span class="sxs-lookup"><span data-stu-id="fbe92-157">Max: `100`&dagger;</span></span> |
| `processPath` | <p><span data-ttu-id="fbe92-158">필수 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-158">Required string attribute.</span></span></p><p><span data-ttu-id="fbe92-159">HTTP 요청을 수신 대기하는 프로세스를 시작하는 실행 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-159">Path to the executable that launches a process listening for HTTP requests.</span></span> <span data-ttu-id="fbe92-160">상대 경로가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-160">Relative paths are supported.</span></span> <span data-ttu-id="fbe92-161">경로가 `.`로 시작되면 경로는 사이트 루트의 상대 경로로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-161">If the path begins with `.`, the path is considered to be relative to the site root.</span></span></p> | |
| `rapidFailsPerMinute` | <p><span data-ttu-id="fbe92-162">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-162">Optional integer attribute.</span></span></p><p><span data-ttu-id="fbe92-163">**processPath**에 지정된 프로세스의 분당 크래시 허용 횟수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-163">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="fbe92-164">이 제한을 초과하면 모듈은 남은 시간 동안 프로세스 시작을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-164">If this limit is exceeded, the module stops launching the process for the remainder of the minute.</span></span></p><p><span data-ttu-id="fbe92-165">In-Process 호스팅에서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-165">Not supported with in-process hosting.</span></span></p> | <span data-ttu-id="fbe92-166">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="fbe92-166">Default: `10`</span></span><br><span data-ttu-id="fbe92-167">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="fbe92-167">Min: `0`</span></span><br><span data-ttu-id="fbe92-168">최대: `100`</span><span class="sxs-lookup"><span data-stu-id="fbe92-168">Max: `100`</span></span> |
| `requestTimeout` | <p><span data-ttu-id="fbe92-169">선택적 시간 간격 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-169">Optional timespan attribute.</span></span></p><p><span data-ttu-id="fbe92-170">ASP.NET Core 모듈이 %ASPNETCORE_PORT%에서 수신 대기하는 프로세스의 응답을 기다리는 기간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-170">Specifies the duration for which the ASP.NET Core Module waits for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="fbe92-171">ASP.NET Core 2.1 이상 릴리스와 함께 제공되는 ASP.NET Core 모듈 버전에서는 `requestTimeout`이 전체 시간, 분, 초로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-171">In versions of the ASP.NET Core Module that shipped with the release of ASP.NET Core 2.1 or later, the `requestTimeout` is specified in hours, minutes, and seconds.</span></span></p><p><span data-ttu-id="fbe92-172">In-Process 호스팅에는 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-172">Doesn't apply to in-process hosting.</span></span> <span data-ttu-id="fbe92-173">In-Process 호스팅의 경우 모듈은 앱이 요청을 처리할 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-173">For in-process hosting, the module waits for the app to process the request.</span></span></p> | <span data-ttu-id="fbe92-174">기본값: `00:02:00`</span><span class="sxs-lookup"><span data-stu-id="fbe92-174">Default: `00:02:00`</span></span><br><span data-ttu-id="fbe92-175">최소: `00:00:00`</span><span class="sxs-lookup"><span data-stu-id="fbe92-175">Min: `00:00:00`</span></span><br><span data-ttu-id="fbe92-176">최대: `360:00:00`</span><span class="sxs-lookup"><span data-stu-id="fbe92-176">Max: `360:00:00`</span></span> |
| `shutdownTimeLimit` | <p><span data-ttu-id="fbe92-177">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-177">Optional integer attribute.</span></span></p><p><span data-ttu-id="fbe92-178">*app_offline.htm* 파일이 검색될 때 실행 파일이 정상적으로 종료될 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-178">Duration in seconds that the module waits for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p> | <span data-ttu-id="fbe92-179">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="fbe92-179">Default: `10`</span></span><br><span data-ttu-id="fbe92-180">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="fbe92-180">Min: `0`</span></span><br><span data-ttu-id="fbe92-181">최대: `600`</span><span class="sxs-lookup"><span data-stu-id="fbe92-181">Max: `600`</span></span> |
| `startupTimeLimit` | <p><span data-ttu-id="fbe92-182">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-182">Optional integer attribute.</span></span></p><p><span data-ttu-id="fbe92-183">실행 파일이 포트에서 수신 대기하는 프로세스를 시작할 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-183">Duration in seconds that the module waits for the executable to start a process listening on the port.</span></span> <span data-ttu-id="fbe92-184">이 시간 제한을 초과하면 모듈이 프로세스를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-184">If this time limit is exceeded, the module kills the process.</span></span> <span data-ttu-id="fbe92-185">모듈은 새 요청을 수신할 때 프로세스를 다시 시작하려고 하고, 마지막 롤링 기간(분)에 앱이 **rapidFailsPerMinute**번 시작에 실패한 경우가 아니면 이후 요청이 들어올 때 프로세스를 계속 다시 시작하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-185">The module attempts to relaunch the process when it receives a new request and continues to attempt to restart the process on subsequent incoming requests unless the app fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p><p><span data-ttu-id="fbe92-186">값 0은 무한 시간 제한으로 간주되지 **않습니다**.</span><span class="sxs-lookup"><span data-stu-id="fbe92-186">A value of 0 (zero) is **not** considered an infinite timeout.</span></span></p> | <span data-ttu-id="fbe92-187">기본값: `120`</span><span class="sxs-lookup"><span data-stu-id="fbe92-187">Default: `120`</span></span><br><span data-ttu-id="fbe92-188">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="fbe92-188">Min: `0`</span></span><br><span data-ttu-id="fbe92-189">최대: `3600`</span><span class="sxs-lookup"><span data-stu-id="fbe92-189">Max: `3600`</span></span> |
| `stdoutLogEnabled` | <p><span data-ttu-id="fbe92-190">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-190">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="fbe92-191">true인 경우 **processPath**에 지정된 프로세스에 대한 **stdout** 및 **stderr**이 **stdoutLogFile**에 지정된 파일로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-191">If true, **stdout** and **stderr** for the process specified in **processPath** are redirected to the file specified in **stdoutLogFile**.</span></span></p> | `false` |
| `stdoutLogFile` | <p><span data-ttu-id="fbe92-192">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-192">Optional string attribute.</span></span></p><p><span data-ttu-id="fbe92-193">**processPath**에 지정된 프로세스에서 **stdout** 및 **stderr**이 기록되는 상대 또는 절대 파일 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-193">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** are logged.</span></span> <span data-ttu-id="fbe92-194">상대 경로는 사이트 루트에 상대적인 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-194">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="fbe92-195">`.`로 시작하는 모든 경로는 사이트 루트에 상대적인 경로이고 다른 모든 경로는 절대 경로로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-195">Any path starting with `.` are relative to the site root and all other paths are treated as absolute paths.</span></span> <span data-ttu-id="fbe92-196">모듈이 로그 파일을 만들려면 경로에 제공된 모든 폴더가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-196">Any folders provided in the path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="fbe92-197">타임스탬프, 프로세스 ID 및 파일 확장명(*.log*)은 밑줄 구분 기호를 사용하여 **stdoutLogFile** 경로의 마지막 세그먼트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-197">Using underscore delimiters, a timestamp, process ID, and file extension (*.log*) are added to the last segment of the **stdoutLogFile** path.</span></span> <span data-ttu-id="fbe92-198">`.\logs\stdout`이 값으로 제공되는 경우 예제 stdout 로그는 2018년 2월 5일 19시 41분 32초에 프로세스 ID 1934를 사용하여 저장될 경우 *logs* 폴더에 *stdout_20180205194132_1934.log*로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-198">If `.\logs\stdout` is supplied as a value, an example stdout log is saved as *stdout_20180205194132_1934.log* in the *logs* folder when saved on 2/5/2018 at 19:41:32 with a process ID of 1934.</span></span></p> | `aspnetcore-stdout` |

::: moniker-end

::: moniker range="= aspnetcore-2.1"

| <span data-ttu-id="fbe92-199">특성</span><span class="sxs-lookup"><span data-stu-id="fbe92-199">Attribute</span></span> | <span data-ttu-id="fbe92-200">설명</span><span class="sxs-lookup"><span data-stu-id="fbe92-200">Description</span></span> | <span data-ttu-id="fbe92-201">기본</span><span class="sxs-lookup"><span data-stu-id="fbe92-201">Default</span></span> |
| --------- | ----------- | :-----: |
| `arguments` | <p><span data-ttu-id="fbe92-202">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-202">Optional string attribute.</span></span></p><p><span data-ttu-id="fbe92-203">**processPath**에 지정된 실행 파일에 대한 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-203">Arguments to the executable specified in **processPath**.</span></span></p>| |
| `disableStartUpErrorPage` | <p><span data-ttu-id="fbe92-204">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-204">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="fbe92-205">true인 경우 **502.5 - 프로세스 실패** 페이지가 표시되지 않고 *web.config*에 구성된 502 상태 코드 페이지가 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-205">If true, the **502.5 - Process Failure** page is suppressed, and the 502 status code page configured in the *web.config* takes precedence.</span></span></p> | `false` |
| `forwardWindowsAuthToken` | <p><span data-ttu-id="fbe92-206">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-206">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="fbe92-207">true인 경우 토큰은 %ASPNETCORE_PORT%에서 수신 대기하는 자식 프로세스에 요청별 헤더 'MS-ASPNETCORE-WINAUTHTOKEN'으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-207">If true, the token is forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="fbe92-208">이 프로세스는 요청별로 이 토큰에서 CloseHandle을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-208">It's the responsibility of that process to call CloseHandle on this token per request.</span></span></p> | `true` |
| `processesPerApplication` | <p><span data-ttu-id="fbe92-209">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-209">Optional integer attribute.</span></span></p><p><span data-ttu-id="fbe92-210">앱별로 스핀 업할 수 있는 **processPath** 설정에 지정된 프로세스의 인스턴스 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-210">Specifies the number of instances of the process specified in the **processPath** setting that can be spun up per app.</span></span></p> | <span data-ttu-id="fbe92-211">기본값: `1`</span><span class="sxs-lookup"><span data-stu-id="fbe92-211">Default: `1`</span></span><br><span data-ttu-id="fbe92-212">최소: `1`</span><span class="sxs-lookup"><span data-stu-id="fbe92-212">Min: `1`</span></span><br><span data-ttu-id="fbe92-213">최대: `100`</span><span class="sxs-lookup"><span data-stu-id="fbe92-213">Max: `100`</span></span> |
| `processPath` | <p><span data-ttu-id="fbe92-214">필수 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-214">Required string attribute.</span></span></p><p><span data-ttu-id="fbe92-215">HTTP 요청을 수신 대기하는 프로세스를 시작하는 실행 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-215">Path to the executable that launches a process listening for HTTP requests.</span></span> <span data-ttu-id="fbe92-216">상대 경로가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-216">Relative paths are supported.</span></span> <span data-ttu-id="fbe92-217">경로가 `.`로 시작되면 경로는 사이트 루트의 상대 경로로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-217">If the path begins with `.`, the path is considered to be relative to the site root.</span></span></p> | |
| `rapidFailsPerMinute` | <p><span data-ttu-id="fbe92-218">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-218">Optional integer attribute.</span></span></p><p><span data-ttu-id="fbe92-219">**processPath**에 지정된 프로세스의 분당 크래시 허용 횟수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-219">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="fbe92-220">이 제한을 초과하면 모듈은 남은 시간 동안 프로세스 시작을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-220">If this limit is exceeded, the module stops launching the process for the remainder of the minute.</span></span></p> | <span data-ttu-id="fbe92-221">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="fbe92-221">Default: `10`</span></span><br><span data-ttu-id="fbe92-222">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="fbe92-222">Min: `0`</span></span><br><span data-ttu-id="fbe92-223">최대: `100`</span><span class="sxs-lookup"><span data-stu-id="fbe92-223">Max: `100`</span></span> |
| `requestTimeout` | <p><span data-ttu-id="fbe92-224">선택적 시간 간격 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-224">Optional timespan attribute.</span></span></p><p><span data-ttu-id="fbe92-225">ASP.NET Core 모듈이 %ASPNETCORE_PORT%에서 수신 대기하는 프로세스의 응답을 기다리는 기간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-225">Specifies the duration for which the ASP.NET Core Module waits for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="fbe92-226">ASP.NET Core 2.1 이상 릴리스와 함께 제공되는 ASP.NET Core 모듈 버전에서는 `requestTimeout`이 전체 시간, 분, 초로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-226">In versions of the ASP.NET Core Module that shipped with the release of ASP.NET Core 2.1 or later, the `requestTimeout` is specified in hours, minutes, and seconds.</span></span></p> | <span data-ttu-id="fbe92-227">기본값: `00:02:00`</span><span class="sxs-lookup"><span data-stu-id="fbe92-227">Default: `00:02:00`</span></span><br><span data-ttu-id="fbe92-228">최소: `00:00:00`</span><span class="sxs-lookup"><span data-stu-id="fbe92-228">Min: `00:00:00`</span></span><br><span data-ttu-id="fbe92-229">최대: `360:00:00`</span><span class="sxs-lookup"><span data-stu-id="fbe92-229">Max: `360:00:00`</span></span> |
| `shutdownTimeLimit` | <p><span data-ttu-id="fbe92-230">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-230">Optional integer attribute.</span></span></p><p><span data-ttu-id="fbe92-231">*app_offline.htm* 파일이 검색될 때 실행 파일이 정상적으로 종료될 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-231">Duration in seconds that the module waits for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p> | <span data-ttu-id="fbe92-232">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="fbe92-232">Default: `10`</span></span><br><span data-ttu-id="fbe92-233">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="fbe92-233">Min: `0`</span></span><br><span data-ttu-id="fbe92-234">최대: `600`</span><span class="sxs-lookup"><span data-stu-id="fbe92-234">Max: `600`</span></span> |
| `startupTimeLimit` | <p><span data-ttu-id="fbe92-235">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-235">Optional integer attribute.</span></span></p><p><span data-ttu-id="fbe92-236">실행 파일이 포트에서 수신 대기하는 프로세스를 시작할 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-236">Duration in seconds that the module waits for the executable to start a process listening on the port.</span></span> <span data-ttu-id="fbe92-237">이 시간 제한을 초과하면 모듈이 프로세스를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-237">If this time limit is exceeded, the module kills the process.</span></span> <span data-ttu-id="fbe92-238">모듈은 새 요청을 수신할 때 프로세스를 다시 시작하려고 하고, 마지막 롤링 기간(분)에 앱이 **rapidFailsPerMinute**번 시작에 실패한 경우가 아니면 이후 요청이 들어올 때 프로세스를 계속 다시 시작하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-238">The module attempts to relaunch the process when it receives a new request and continues to attempt to restart the process on subsequent incoming requests unless the app fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p><p><span data-ttu-id="fbe92-239">값 0은 무한 시간 제한으로 간주되지 **않습니다**.</span><span class="sxs-lookup"><span data-stu-id="fbe92-239">A value of 0 (zero) is **not** considered an infinite timeout.</span></span></p> | <span data-ttu-id="fbe92-240">기본값: `120`</span><span class="sxs-lookup"><span data-stu-id="fbe92-240">Default: `120`</span></span><br><span data-ttu-id="fbe92-241">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="fbe92-241">Min: `0`</span></span><br><span data-ttu-id="fbe92-242">최대: `3600`</span><span class="sxs-lookup"><span data-stu-id="fbe92-242">Max: `3600`</span></span> |
| `stdoutLogEnabled` | <p><span data-ttu-id="fbe92-243">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-243">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="fbe92-244">true인 경우 **processPath**에 지정된 프로세스에 대한 **stdout** 및 **stderr**이 **stdoutLogFile**에 지정된 파일로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-244">If true, **stdout** and **stderr** for the process specified in **processPath** are redirected to the file specified in **stdoutLogFile**.</span></span></p> | `false` |
| `stdoutLogFile` | <p><span data-ttu-id="fbe92-245">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-245">Optional string attribute.</span></span></p><p><span data-ttu-id="fbe92-246">**processPath**에 지정된 프로세스에서 **stdout** 및 **stderr**이 기록되는 상대 또는 절대 파일 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-246">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** are logged.</span></span> <span data-ttu-id="fbe92-247">상대 경로는 사이트 루트에 상대적인 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-247">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="fbe92-248">`.`로 시작하는 모든 경로는 사이트 루트에 상대적인 경로이고 다른 모든 경로는 절대 경로로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-248">Any path starting with `.` are relative to the site root and all other paths are treated as absolute paths.</span></span> <span data-ttu-id="fbe92-249">모듈이 로그 파일을 만들려면 경로에 제공된 모든 폴더가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-249">Any folders provided in the path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="fbe92-250">타임스탬프, 프로세스 ID 및 파일 확장명(*.log*)은 밑줄 구분 기호를 사용하여 **stdoutLogFile** 경로의 마지막 세그먼트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-250">Using underscore delimiters, a timestamp, process ID, and file extension (*.log*) are added to the last segment of the **stdoutLogFile** path.</span></span> <span data-ttu-id="fbe92-251">`.\logs\stdout`이 값으로 제공되는 경우 예제 stdout 로그는 2018년 2월 5일 19시 41분 32초에 프로세스 ID 1934를 사용하여 저장될 경우 *logs* 폴더에 *stdout_20180205194132_1934.log*로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-251">If `.\logs\stdout` is supplied as a value, an example stdout log is saved as *stdout_20180205194132_1934.log* in the *logs* folder when saved on 2/5/2018 at 19:41:32 with a process ID of 1934.</span></span></p> | `aspnetcore-stdout` |

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

| <span data-ttu-id="fbe92-252">특성</span><span class="sxs-lookup"><span data-stu-id="fbe92-252">Attribute</span></span> | <span data-ttu-id="fbe92-253">설명</span><span class="sxs-lookup"><span data-stu-id="fbe92-253">Description</span></span> | <span data-ttu-id="fbe92-254">기본</span><span class="sxs-lookup"><span data-stu-id="fbe92-254">Default</span></span> |
| --------- | ----------- | :-----: |
| `arguments` | <p><span data-ttu-id="fbe92-255">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-255">Optional string attribute.</span></span></p><p><span data-ttu-id="fbe92-256">**processPath**에 지정된 실행 파일에 대한 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-256">Arguments to the executable specified in **processPath**.</span></span></p>| |
| `disableStartUpErrorPage` | <p><span data-ttu-id="fbe92-257">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-257">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="fbe92-258">true인 경우 **502.5 - 프로세스 실패** 페이지가 표시되지 않고 *web.config*에 구성된 502 상태 코드 페이지가 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-258">If true, the **502.5 - Process Failure** page is suppressed, and the 502 status code page configured in the *web.config* takes precedence.</span></span></p> | `false` |
| `forwardWindowsAuthToken` | <p><span data-ttu-id="fbe92-259">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-259">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="fbe92-260">true인 경우 토큰은 %ASPNETCORE_PORT%에서 수신 대기하는 자식 프로세스에 요청별 헤더 'MS-ASPNETCORE-WINAUTHTOKEN'으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-260">If true, the token is forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="fbe92-261">이 프로세스는 요청별로 이 토큰에서 CloseHandle을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-261">It's the responsibility of that process to call CloseHandle on this token per request.</span></span></p> | `true` |
| `processesPerApplication` | <p><span data-ttu-id="fbe92-262">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-262">Optional integer attribute.</span></span></p><p><span data-ttu-id="fbe92-263">앱별로 스핀 업할 수 있는 **processPath** 설정에 지정된 프로세스의 인스턴스 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-263">Specifies the number of instances of the process specified in the **processPath** setting that can be spun up per app.</span></span></p> | <span data-ttu-id="fbe92-264">기본값: `1`</span><span class="sxs-lookup"><span data-stu-id="fbe92-264">Default: `1`</span></span><br><span data-ttu-id="fbe92-265">최소: `1`</span><span class="sxs-lookup"><span data-stu-id="fbe92-265">Min: `1`</span></span><br><span data-ttu-id="fbe92-266">최대: `100`</span><span class="sxs-lookup"><span data-stu-id="fbe92-266">Max: `100`</span></span> |
| `processPath` | <p><span data-ttu-id="fbe92-267">필수 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-267">Required string attribute.</span></span></p><p><span data-ttu-id="fbe92-268">HTTP 요청을 수신 대기하는 프로세스를 시작하는 실행 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-268">Path to the executable that launches a process listening for HTTP requests.</span></span> <span data-ttu-id="fbe92-269">상대 경로가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-269">Relative paths are supported.</span></span> <span data-ttu-id="fbe92-270">경로가 `.`로 시작되면 경로는 사이트 루트의 상대 경로로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-270">If the path begins with `.`, the path is considered to be relative to the site root.</span></span></p> | |
| `rapidFailsPerMinute` | <p><span data-ttu-id="fbe92-271">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-271">Optional integer attribute.</span></span></p><p><span data-ttu-id="fbe92-272">**processPath**에 지정된 프로세스의 분당 크래시 허용 횟수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-272">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="fbe92-273">이 제한을 초과하면 모듈은 남은 시간 동안 프로세스 시작을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-273">If this limit is exceeded, the module stops launching the process for the remainder of the minute.</span></span></p> | <span data-ttu-id="fbe92-274">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="fbe92-274">Default: `10`</span></span><br><span data-ttu-id="fbe92-275">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="fbe92-275">Min: `0`</span></span><br><span data-ttu-id="fbe92-276">최대: `100`</span><span class="sxs-lookup"><span data-stu-id="fbe92-276">Max: `100`</span></span> |
| `requestTimeout` | <p><span data-ttu-id="fbe92-277">선택적 시간 간격 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-277">Optional timespan attribute.</span></span></p><p><span data-ttu-id="fbe92-278">ASP.NET Core 모듈이 %ASPNETCORE_PORT%에서 수신 대기하는 프로세스의 응답을 기다리는 기간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-278">Specifies the duration for which the ASP.NET Core Module waits for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="fbe92-279">ASP.NET Core 2.0 이하 릴리스와 함께 제공되는 ASP.NET Core 모듈 버전에서는 `requestTimeout`을 전체 시간(분)으로만 지정해야 합니다. 그렇지 않으면 기본적으로 2분으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-279">In versions of the ASP.NET Core Module that shipped with the release of ASP.NET Core 2.0 or earlier, the `requestTimeout` must be specified in whole minutes only, otherwise it defaults to 2 minutes.</span></span></p> | <span data-ttu-id="fbe92-280">기본값: `00:02:00`</span><span class="sxs-lookup"><span data-stu-id="fbe92-280">Default: `00:02:00`</span></span><br><span data-ttu-id="fbe92-281">최소: `00:00:00`</span><span class="sxs-lookup"><span data-stu-id="fbe92-281">Min: `00:00:00`</span></span><br><span data-ttu-id="fbe92-282">최대: `360:00:00`</span><span class="sxs-lookup"><span data-stu-id="fbe92-282">Max: `360:00:00`</span></span> |
| `shutdownTimeLimit` | <p><span data-ttu-id="fbe92-283">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-283">Optional integer attribute.</span></span></p><p><span data-ttu-id="fbe92-284">*app_offline.htm* 파일이 검색될 때 실행 파일이 정상적으로 종료될 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-284">Duration in seconds that the module waits for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p> | <span data-ttu-id="fbe92-285">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="fbe92-285">Default: `10`</span></span><br><span data-ttu-id="fbe92-286">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="fbe92-286">Min: `0`</span></span><br><span data-ttu-id="fbe92-287">최대: `600`</span><span class="sxs-lookup"><span data-stu-id="fbe92-287">Max: `600`</span></span> |
| `startupTimeLimit` | <p><span data-ttu-id="fbe92-288">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-288">Optional integer attribute.</span></span></p><p><span data-ttu-id="fbe92-289">실행 파일이 포트에서 수신 대기하는 프로세스를 시작할 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-289">Duration in seconds that the module waits for the executable to start a process listening on the port.</span></span> <span data-ttu-id="fbe92-290">이 시간 제한을 초과하면 모듈이 프로세스를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-290">If this time limit is exceeded, the module kills the process.</span></span> <span data-ttu-id="fbe92-291">모듈은 새 요청을 수신할 때 프로세스를 다시 시작하려고 하고, 마지막 롤링 기간(분)에 앱이 **rapidFailsPerMinute**번 시작에 실패한 경우가 아니면 이후 요청이 들어올 때 프로세스를 계속 다시 시작하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-291">The module attempts to relaunch the process when it receives a new request and continues to attempt to restart the process on subsequent incoming requests unless the app fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p> | <span data-ttu-id="fbe92-292">기본값: `120`</span><span class="sxs-lookup"><span data-stu-id="fbe92-292">Default: `120`</span></span><br><span data-ttu-id="fbe92-293">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="fbe92-293">Min: `0`</span></span><br><span data-ttu-id="fbe92-294">최대: `3600`</span><span class="sxs-lookup"><span data-stu-id="fbe92-294">Max: `3600`</span></span> |
| `stdoutLogEnabled` | <p><span data-ttu-id="fbe92-295">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-295">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="fbe92-296">true인 경우 **processPath**에 지정된 프로세스에 대한 **stdout** 및 **stderr**이 **stdoutLogFile**에 지정된 파일로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-296">If true, **stdout** and **stderr** for the process specified in **processPath** are redirected to the file specified in **stdoutLogFile**.</span></span></p> | `false` |
| `stdoutLogFile` | <p><span data-ttu-id="fbe92-297">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-297">Optional string attribute.</span></span></p><p><span data-ttu-id="fbe92-298">**processPath**에 지정된 프로세스에서 **stdout** 및 **stderr**이 기록되는 상대 또는 절대 파일 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-298">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** are logged.</span></span> <span data-ttu-id="fbe92-299">상대 경로는 사이트 루트에 상대적인 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-299">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="fbe92-300">`.`로 시작하는 모든 경로는 사이트 루트에 상대적인 경로이고 다른 모든 경로는 절대 경로로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-300">Any path starting with `.` are relative to the site root and all other paths are treated as absolute paths.</span></span> <span data-ttu-id="fbe92-301">모듈이 로그 파일을 만들려면 경로에 제공된 모든 폴더가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-301">Any folders provided in the path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="fbe92-302">타임스탬프, 프로세스 ID 및 파일 확장명(*.log*)은 밑줄 구분 기호를 사용하여 **stdoutLogFile** 경로의 마지막 세그먼트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-302">Using underscore delimiters, a timestamp, process ID, and file extension (*.log*) are added to the last segment of the **stdoutLogFile** path.</span></span> <span data-ttu-id="fbe92-303">`.\logs\stdout`이 값으로 제공되는 경우 예제 stdout 로그는 2018년 2월 5일 19시 41분 32초에 프로세스 ID 1934를 사용하여 저장될 경우 *logs* 폴더에 *stdout_20180205194132_1934.log*로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-303">If `.\logs\stdout` is supplied as a value, an example stdout log is saved as *stdout_20180205194132_1934.log* in the *logs* folder when saved on 2/5/2018 at 19:41:32 with a process ID of 1934.</span></span></p> | `aspnetcore-stdout` |

::: moniker-end

### <a name="setting-environment-variables"></a><span data-ttu-id="fbe92-304">환경 변수 설정</span><span class="sxs-lookup"><span data-stu-id="fbe92-304">Setting environment variables</span></span>

<span data-ttu-id="fbe92-305">`processPath` 특성에서 프로세스에 대한 환경 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-305">Environment variables can be specified for the process in the `processPath` attribute.</span></span> <span data-ttu-id="fbe92-306">`environmentVariables` 컬렉션 요소의 `environmentVariable` 자식 요소를 사용하여 환경 변수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-306">Specify an environment variable with the `environmentVariable` child element of an `environmentVariables` collection element.</span></span> <span data-ttu-id="fbe92-307">이 섹션에 설정된 환경 변수가 시스템 환경 변수보다 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-307">Environment variables set in this section take precedence over system environment variables.</span></span>

<span data-ttu-id="fbe92-308">다음 예제에서는 두 개의 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-308">The following example sets two environment variables.</span></span> <span data-ttu-id="fbe92-309">`ASPNETCORE_ENVIRONMENT`는 앱의 환경을 `Development`로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-309">`ASPNETCORE_ENVIRONMENT` configures the app's environment to `Development`.</span></span> <span data-ttu-id="fbe92-310">앱 예외를 디버그할 때 [개발자 예외 페이지](xref:fundamentals/error-handling)를 강제로 로드하기 위해 개발자가 *web.config* 파일에서 이 값을 일시적으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-310">A developer may temporarily set this value in the *web.config* file in order to force the [Developer Exception Page](xref:fundamentals/error-handling) to load when debugging an app exception.</span></span> <span data-ttu-id="fbe92-311">`CONFIG_DIR`은 개발자가 앱 구성 파일을 로드할 경로를 생성하기 위해 시작 시 값을 읽는 코드를 작성한 사용자 정의 환경 변수의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-311">`CONFIG_DIR` is an example of a user-defined environment variable, where the developer has written code that reads the value on startup to form a path for loading the app's configuration file.</span></span>

::: moniker range=">= aspnetcore-2.2"

```xml
<aspNetCore processPath="dotnet"
      arguments=".\MyApp.dll"
      stdoutLogEnabled="false"
      stdoutLogFile="\\?\%home%\LogFiles\stdout"
      hostingModel="inprocess">
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
> <span data-ttu-id="fbe92-312">인터넷과 같은 신뢰할 수 없는 네트워크에 액세스할 수 없는 스테이징 및 테스트 서버에서는 `ASPNETCORE_ENVIRONMENT` 환경 변수를 `Development`로 설정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-312">Only set the `ASPNETCORE_ENVIRONMENT` environment variable to `Development` on staging and testing servers that aren't accessible to untrusted networks, such as the Internet.</span></span>

## <a name="appofflinehtm"></a><span data-ttu-id="fbe92-313">app_offline.htm</span><span class="sxs-lookup"><span data-stu-id="fbe92-313">app_offline.htm</span></span>

<span data-ttu-id="fbe92-314">응용 프로그램의 루트 디렉터리에서 이름이 *app_offline.htm*인 파일이 검색되면 ASP.NET Core 모듈은 앱을 자동으로 종료하고 들어오는 요청 처리를 중지하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-314">If a file with the name *app_offline.htm* is detected in the root directory of an app, the ASP.NET Core Module attempts to gracefully shutdown the app and stop processing incoming requests.</span></span> <span data-ttu-id="fbe92-315">`shutdownTimeLimit`에 정의된 시간(초) 후에도 앱이 계속 실행되면 ASP.NET Core 모듈은 실행 중인 프로세스를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-315">If the app is still running after the number of seconds defined in `shutdownTimeLimit`, the ASP.NET Core Module kills the running process.</span></span>

<span data-ttu-id="fbe92-316">*app_offline.htm* 파일이 있는 동안 ASP.NET Core 모듈은 *app_offline.htm* 파일의 콘텐츠를 다시 보내 요청에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-316">While the *app_offline.htm* file is present, the ASP.NET Core Module responds to requests by sending back the contents of the *app_offline.htm* file.</span></span> <span data-ttu-id="fbe92-317">*app_offline.htm* 파일이 제거되면 다음 요청이 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-317">When the *app_offline.htm* file is removed, the next request starts the app.</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="fbe92-318">Out-of-Process 호스팅 모델을 사용할 때 열린 연결이 있으면 앱이 즉시 종료되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-318">When using the out-of-process hosting model, the app might not shut down immediately if there's an open connection.</span></span> <span data-ttu-id="fbe92-319">예를 들어, WebSocket 연결은 앱 종료를 지연시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-319">For example, a websocket connection may delay app shut down.</span></span>

::: moniker-end

## <a name="start-up-error-page"></a><span data-ttu-id="fbe92-320">시작 오류 페이지</span><span class="sxs-lookup"><span data-stu-id="fbe92-320">Start-up error page</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="fbe92-321">In process 및 out of process 호스팅은 모두 앱을 시작하지 못할 때 사용자 지정 오류 페이지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-321">Both in-process and out-of-process hosting produce custom error pages when they fail to start the app.</span></span>

<span data-ttu-id="fbe92-322">ASP.NET Core 모듈이 in-process 또는 out-of-process 요청 처리기를 찾지 못하면 *500.0 - In-Process/Out-of-process 처리기 로드 실패* 상태 코드 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-322">If the ASP.NET Core Module fails to find either the in-process or out-of-process request handler, a *500.0 - In-Process/Out-Of-Process Handler Load Failure* status code page appears.</span></span>

<span data-ttu-id="fbe92-323">in-process 호스팅의 경우 ASP.NET Core 모듈이 앱을 시작하지 못하면 *500.30 - 시작 실패* 상태 코드 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-323">For in-process hosting if the ASP.NET Core Module fails to start the app, a *500.30 - Start Failure* status code page appears.</span></span>

<span data-ttu-id="fbe92-324">out-of-process 호스팅의 경우 ASP.NET Core 모듈이 백 엔드 프로세스를 시작하지 못하거나 백 엔드 프로세스가 시작되지만 구성된 포트에서 수신 대기하지 못하면 *502.5 - 프로세스 실패* 상태 코드 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-324">For out-of-process hosting if the ASP.NET Core Module fails to launch the backend process or the backend process starts but fails to listen on the configured port, a *502.5 - Process Failure* status code page appears.</span></span>

<span data-ttu-id="fbe92-325">이 페이지를 표시하지 않고 기본 IIS 5xx 상태 코드 페이지로 되돌리려면 `disableStartUpErrorPage` 특성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-325">To suppress this page and revert to the default IIS 5xx status code page, use the `disableStartUpErrorPage` attribute.</span></span> <span data-ttu-id="fbe92-326">사용자 지정 오류 메시지 구성에 대한 자세한 내용은 [HTTP 오류 &lt;httpErrors&gt;](/iis/configuration/system.webServer/httpErrors/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbe92-326">For more information on configuring custom error messages, see [HTTP Errors &lt;httpErrors&gt;](/iis/configuration/system.webServer/httpErrors/).</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="fbe92-327">ASP.NET Core 모듈이 백 엔드 프로세스를 시작하지 못하거나 백 엔드 프로세스가 시작되지만 구성된 포트에서 수신 대기하지 못하면 *502.5 - 프로세스 실패* 상태 코드 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-327">If the ASP.NET Core Module fails to launch the backend process or the backend process starts but fails to listen on the configured port, a *502.5 - Process Failure* status code page appears.</span></span> <span data-ttu-id="fbe92-328">이 페이지를 표시하지 않고 기본 IIS 502 상태 코드 페이지로 되돌리려면 `disableStartUpErrorPage` 특성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-328">To suppress this page and revert to the default IIS 502 status code page, use the `disableStartUpErrorPage` attribute.</span></span> <span data-ttu-id="fbe92-329">사용자 지정 오류 메시지 구성에 대한 자세한 내용은 [HTTP 오류 &lt;httpErrors&gt;](/iis/configuration/system.webServer/httpErrors/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbe92-329">For more information on configuring custom error messages, see [HTTP Errors &lt;httpErrors&gt;](/iis/configuration/system.webServer/httpErrors/).</span></span>

![502.5 프로세스 실패 상태 코드 페이지](aspnet-core-module/_static/ANCM-502_5.png)

::: moniker-end

## <a name="log-creation-and-redirection"></a><span data-ttu-id="fbe92-331">로그 만들기 및 리디렉션</span><span class="sxs-lookup"><span data-stu-id="fbe92-331">Log creation and redirection</span></span>

<span data-ttu-id="fbe92-332">ASP.NET Core 모듈은 `aspNetCore` 요소의 `stdoutLogEnabled` 및 `stdoutLogFile` 특성이 설정된 경우 stdout 및 stderr 콘솔 출력을 디스크로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-332">The ASP.NET Core Module redirects stdout and stderr console output to disk if the `stdoutLogEnabled` and `stdoutLogFile` attributes of the `aspNetCore` element are set.</span></span> <span data-ttu-id="fbe92-333">모듈이 로그 파일을 만들려면 `stdoutLogFile` 경로의 모든 폴더가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-333">Any folders in the `stdoutLogFile` path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="fbe92-334">앱 풀에는 로그가 기록될 위치에 쓰기 권한이 있어야 합니다(`IIS AppPool\<app_pool_name>`을 사용하여 쓰기 권한 제공).</span><span class="sxs-lookup"><span data-stu-id="fbe92-334">The app pool must have write access to the location where the logs are written (use `IIS AppPool\<app_pool_name>` to provide write permission).</span></span>

<span data-ttu-id="fbe92-335">프로세스 재생/다시 시작이 발생하지 않는 한 로그는 회전되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-335">Logs aren't rotated, unless process recycling/restart occurs.</span></span> <span data-ttu-id="fbe92-336">로그에서 사용하는 디스크 공간을 제한하는 것은 호스터의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-336">It's the responsibility of the hoster to limit the disk space the logs consume.</span></span>

<span data-ttu-id="fbe92-337">stdout 로그는 앱 시작 문제를 해결하는 경우에만 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-337">Using the stdout log is only recommended for troubleshooting app startup issues.</span></span> <span data-ttu-id="fbe92-338">일반 앱 로깅을 위해 stdout 로그를 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="fbe92-338">Don't use the stdout log for general app logging purposes.</span></span> <span data-ttu-id="fbe92-339">ASP.NET Core 앱의 루틴 로깅에는 로그 파일 크기를 제한하고 로그를 회전하는 로깅 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-339">For routine logging in an ASP.NET Core app, use a logging library that limits log file size and rotates logs.</span></span> <span data-ttu-id="fbe92-340">자세한 내용은 [타사 로깅 공급자](xref:fundamentals/logging/index#third-party-logging-providers)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbe92-340">For more information, see [third-party logging providers](xref:fundamentals/logging/index#third-party-logging-providers).</span></span>

<span data-ttu-id="fbe92-341">로그 파일이 만들어질 때 타임스탬프 및 파일 확장명이 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-341">A timestamp and file extension are added automatically when the log file is created.</span></span> <span data-ttu-id="fbe92-342">로그 파일 이름은 타임스탬프, 프로세스 ID 및 파일 확장명(*.log*)을 밑줄로 구분된 `stdoutLogFile` 경로의 마지막 세그먼트(일반적으로 *stdout*)에 추가하여 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-342">The log file name is composed by appending the timestamp, process ID, and file extension (*.log*) to the last segment of the `stdoutLogFile` path (typically *stdout*) delimited by underscores.</span></span> <span data-ttu-id="fbe92-343">`stdoutLogFile` 경로가 *stdout*으로 끝나는 경우 2018년 2월 5일 19시 42분 32초에 만들어진 PID 1934를 사용하는 앱에 대한 로그의 파일 이름은 *stdout_20180205194132_1934.log*입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-343">If the `stdoutLogFile` path ends with *stdout*, a log for an app with a PID of 1934 created on 2/5/2018 at 19:42:32 has the file name *stdout_20180205194132_1934.log*.</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="fbe92-344">`stdoutLogEnabled`가 false이면 앱 시작 시 발생하는 오류가 캡처되어 최대 30KB의 이벤트 로그로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-344">If `stdoutLogEnabled` is false, errors that occur on app startup are captured and emitted to the event log up to 30 KB.</span></span> <span data-ttu-id="fbe92-345">시작 후에는 모든 추가 로그가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-345">After startup, all additional logs are discarded.</span></span>

::: moniker-end

<span data-ttu-id="fbe92-346">다음 샘플 `aspNetCore` 요소는 Azure App Service에서 호스트되는 앱에 대한 stdout 로깅을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-346">The following sample `aspNetCore` element configures stdout logging for an app hosted in Azure App Service.</span></span> <span data-ttu-id="fbe92-347">로컬 로깅에는 로컬 경로 또는 네트워크 공유 경로가 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-347">A local path or network share path is acceptable for local logging.</span></span> <span data-ttu-id="fbe92-348">AppPool 사용자 ID에 제공된 경로에 쓸 수 있는 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-348">Confirm that the AppPool user identity has permission to write to the path provided.</span></span>

::: moniker range=">= aspnetcore-2.2"

```xml
<aspNetCore processPath="dotnet"
    arguments=".\MyApp.dll"
    stdoutLogEnabled="true"
    stdoutLogFile="\\?\%home%\LogFiles\stdout"
    hostingModel="inprocess">
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

## <a name="enhanced-diagnostic-logs"></a><span data-ttu-id="fbe92-349">개선된 진단 로그</span><span class="sxs-lookup"><span data-stu-id="fbe92-349">Enhanced diagnostic logs</span></span>

<span data-ttu-id="fbe92-350">ASP.NET Core 모듈 제공은 개선된 진단 로그를 제공하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-350">The ASP.NET Core Module provides is configurable to provide enhanced diagnostics logs.</span></span> <span data-ttu-id="fbe92-351">*web.config*의 `<aspNetCore>` 요소에 `<handlerSettings>` 요소를 추가합니다. `debugLevel`을 `TRACE`으로 설정하면 진단 정보의 충실도가 높아집니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-351">Add the `<handlerSettings>` element to the `<aspNetCore>` element in *web.config*. Setting the `debugLevel` to `TRACE` exposes a higher fidelity of diagnostic information:</span></span>

```xml
<aspNetCore processPath="dotnet"
    arguments=".\MyApp.dll"
    stdoutLogEnabled="false"
    stdoutLogFile="\\?\%home%\LogFiles\stdout"
    hostingModel="inprocess">
  <handlerSettings>
    <handlerSetting name="debugFile" value="aspnetcore-debug.log" />
    <handlerSetting name="debugLevel" value="FILE,TRACE" />
  </handlerSettings>
</aspNetCore>
```

<span data-ttu-id="fbe92-352">디버그 수준 (`debugLevel`) 값은 수준과 위치를 모두 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-352">Debug level (`debugLevel`) values can include both the level and the location.</span></span>

<span data-ttu-id="fbe92-353">수준(최소한에서 가장 자세한 정보까지 순서대로 ):</span><span class="sxs-lookup"><span data-stu-id="fbe92-353">Levels (in order from least to most verbose):</span></span>

* <span data-ttu-id="fbe92-354">오류</span><span class="sxs-lookup"><span data-stu-id="fbe92-354">ERROR</span></span>
* <span data-ttu-id="fbe92-355">경고</span><span class="sxs-lookup"><span data-stu-id="fbe92-355">WARNING</span></span>
* <span data-ttu-id="fbe92-356">정보</span><span class="sxs-lookup"><span data-stu-id="fbe92-356">INFO</span></span>
* <span data-ttu-id="fbe92-357">TRACE</span><span class="sxs-lookup"><span data-stu-id="fbe92-357">TRACE</span></span>

<span data-ttu-id="fbe92-358">위치(여러 위치가 허용됨):</span><span class="sxs-lookup"><span data-stu-id="fbe92-358">Locations (multiple locations are permitted):</span></span>

* <span data-ttu-id="fbe92-359">CONSOLE</span><span class="sxs-lookup"><span data-stu-id="fbe92-359">CONSOLE</span></span>
* <span data-ttu-id="fbe92-360">EVENTLOG</span><span class="sxs-lookup"><span data-stu-id="fbe92-360">EVENTLOG</span></span>
* <span data-ttu-id="fbe92-361">파일</span><span class="sxs-lookup"><span data-stu-id="fbe92-361">FILE</span></span>

<span data-ttu-id="fbe92-362">처리기 설정은 환경 변수를 통해서도 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-362">The handler settings can also be provided via environment variables:</span></span>

* <span data-ttu-id="fbe92-363">`ASPNETCORE_MODULE_DEBUG_FILE` &ndash; 디버그 로그 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-363">`ASPNETCORE_MODULE_DEBUG_FILE` &ndash; Path to the debug log file.</span></span> <span data-ttu-id="fbe92-364">(기본값: *aspnetcore-debug.log*)</span><span class="sxs-lookup"><span data-stu-id="fbe92-364">(Default: *aspnetcore-debug.log*)</span></span>
* <span data-ttu-id="fbe92-365">`ASPNETCORE_MODULE_DEBUG` &ndash; 디버그 수준 설정.</span><span class="sxs-lookup"><span data-stu-id="fbe92-365">`ASPNETCORE_MODULE_DEBUG` &ndash; Debug level setting.</span></span>

> [!WARNING]
> <span data-ttu-id="fbe92-366">배포에서 문제를 해결하는 데 필요한 시간보다 오래 디버그 로깅을 사용하도록 설정하지 **마세요**.</span><span class="sxs-lookup"><span data-stu-id="fbe92-366">Do **not** leave debug logging enabled in the deployment for longer than required to troubleshoot an issue.</span></span> <span data-ttu-id="fbe92-367">로그의 크기는 제한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-367">The size of the log isn't limited.</span></span> <span data-ttu-id="fbe92-368">디버그 로그를 사용하도록 설정한 대로 두면 사용 가능한 디스크 공간이 소진되어 서버 또는 앱 서비스가 크래시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-368">Leaving the debug log enabled can exhaust the available disk space and crash the server or app service.</span></span>

::: moniker-end

<span data-ttu-id="fbe92-369">*web.config* 파일에 있는 `aspNetCore` 요소의 예제에 대해서는 [web.config를 사용한 구성](#configuration-with-webconfig)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbe92-369">See [Configuration with web.config](#configuration-with-webconfig) for an example of the `aspNetCore` element in the *web.config* file.</span></span>

## <a name="proxy-configuration-uses-http-protocol-and-a-pairing-token"></a><span data-ttu-id="fbe92-370">프록시 구성은 HTTP 프로토콜 및 페어링 토큰을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-370">Proxy configuration uses HTTP protocol and a pairing token</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="fbe92-371">*호스팅에만 적용됩니다.*</span><span class="sxs-lookup"><span data-stu-id="fbe92-371">*Only applies to out-of-process hosting.*</span></span>

::: moniker-end

<span data-ttu-id="fbe92-372">ASP.NET Core 모듈과 Kestrel 사이에 만들어진 프록시는 HTTP 프로토콜을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-372">The proxy created between the ASP.NET Core Module and Kestrel uses the HTTP protocol.</span></span> <span data-ttu-id="fbe92-373">HTTP 사용은 모듈과 Kestrel 간의 트래픽이 네트워크 인터페이스에서 분리된 루프백 주소에서 발생하는 성능 최적화입니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-373">Using HTTP is a performance optimization, where the traffic between the module and Kestrel takes place on a loopback address off of the network interface.</span></span> <span data-ttu-id="fbe92-374">서버에서 분리된 위치에서 모듈과 Kestrel 간 트래픽 도청의 위험은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-374">There's no risk of eavesdropping the traffic between the module and Kestrel from a location off of the server.</span></span>

<span data-ttu-id="fbe92-375">페어링 토큰은 Kestrel에서 받은 요청이 IIS에서 프록시되었으며 다른 원본에서 오지 않았다는 것을 보장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-375">A pairing token is used to guarantee that the requests received by Kestrel were proxied by IIS and didn't come from some other source.</span></span> <span data-ttu-id="fbe92-376">페어링 토큰은 모듈에 의해 생성되며 환경 변수(`ASPNETCORE_TOKEN`)로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-376">The pairing token is created and set into an environment variable (`ASPNETCORE_TOKEN`) by the module.</span></span> <span data-ttu-id="fbe92-377">페어링 토큰은 프록시된 모든 요청에서 헤더(`MSAspNetCoreToken`)로도 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-377">The pairing token is also set into a header (`MSAspNetCoreToken`) on every proxied request.</span></span> <span data-ttu-id="fbe92-378">IIS 미들웨어는 수신하는 각 요청을 검사하여 페어링 토큰 헤더 값이 환경 변수 값과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-378">IIS Middleware checks each request it receives to confirm that the pairing token header value matches the environment variable value.</span></span> <span data-ttu-id="fbe92-379">토큰 값이 일치하지 않는 경우 요청이 기록되고 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-379">If the token values are mismatched, the request is logged and rejected.</span></span> <span data-ttu-id="fbe92-380">페어링 토큰 환경 변수와 모듈과 Kestrel 간의 트래픽은 서버에서 분리된 위치에서 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-380">The pairing token environment variable and the traffic between the module and Kestrel aren't accessible from a location off of the server.</span></span> <span data-ttu-id="fbe92-381">페어링 토큰 값을 알지 못하면 공격자는 IIS 미들웨어에서 검사를 무시하는 요청을 전송할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-381">Without knowing the pairing token value, an attacker can't submit requests that bypass the check in the IIS Middleware.</span></span>

## <a name="aspnet-core-module-with-an-iis-shared-configuration"></a><span data-ttu-id="fbe92-382">IIS 공유 구성이 포함된 ASP.NET Core 모듈</span><span class="sxs-lookup"><span data-stu-id="fbe92-382">ASP.NET Core Module with an IIS Shared Configuration</span></span>

<span data-ttu-id="fbe92-383">ASP.NET Core 모듈 설치 관리자는 **SYSTEM** 계정의 권한으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-383">The ASP.NET Core Module installer runs with the privileges of the **SYSTEM** account.</span></span> <span data-ttu-id="fbe92-384">로컬 시스템 계정에는 IIS 공유 구성에서 사용하는 공유 경로에 대한 수정 권한이 없으므로 공유의 *applicationHost.config*에서 모듈 설정을 구성하려고 하면 설치 관리자에서 액세스 거부 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-384">Because the local system account doesn't have modify permission for the share path used by the IIS Shared Configuration, the installer hits an access denied error when attempting to configure the module settings in *applicationHost.config* on the share.</span></span> <span data-ttu-id="fbe92-385">IIS 공유 구성을 사용할 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-385">When using an IIS Shared Configuration, follow these steps:</span></span>

1. <span data-ttu-id="fbe92-386">IIS 공유 구성을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-386">Disable the IIS Shared Configuration.</span></span>
1. <span data-ttu-id="fbe92-387">설치 관리자를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-387">Run the installer.</span></span>
1. <span data-ttu-id="fbe92-388">업데이트된 *applicationHost.config* 파일을 공유로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-388">Export the updated *applicationHost.config* file to the share.</span></span>
1. <span data-ttu-id="fbe92-389">IIS 공유 구성을 다시 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-389">Re-enable the IIS Shared Configuration.</span></span>

## <a name="module-version-and-hosting-bundle-installer-logs"></a><span data-ttu-id="fbe92-390">모듈 버전 및 호스팅 번들 설치 관리자 로그</span><span class="sxs-lookup"><span data-stu-id="fbe92-390">Module version and Hosting Bundle installer logs</span></span>

<span data-ttu-id="fbe92-391">설치된 ASP.NET Core 모듈의 버전을 확인하려면:</span><span class="sxs-lookup"><span data-stu-id="fbe92-391">To determine the version of the installed ASP.NET Core Module:</span></span>

1. <span data-ttu-id="fbe92-392">호스팅 시스템에서 *%windir%\System32\inetsrv*로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-392">On the hosting system, navigate to *%windir%\System32\inetsrv*.</span></span>
1. <span data-ttu-id="fbe92-393">*aspnetcore.dll* 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-393">Locate the *aspnetcore.dll* file.</span></span>
1. <span data-ttu-id="fbe92-394">파일을 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-394">Right-click the file and select **Properties** from the contextual menu.</span></span>
1. <span data-ttu-id="fbe92-395">**세부 정보** 탭을 선택합니다. **파일 버전** 및 **제품 버전**은 설치된 모듈 버전을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-395">Select the **Details** tab. The **File version** and **Product version** represent the installed version of the module.</span></span>

<span data-ttu-id="fbe92-396">모듈에 대한 호스팅 번들 설치 관리자 로그는 *C:\\Users\\%UserName%\\AppData\\Local\\Temp*에 있습니다. 파일 이름은 *dd_DotNetCoreWinSvrHosting__\<timestamp>_000_AspNetCoreModule_x64.log*로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-396">The Hosting Bundle installer logs for the module are found at *C:\\Users\\%UserName%\\AppData\\Local\\Temp*. The file is named *dd_DotNetCoreWinSvrHosting__\<timestamp>_000_AspNetCoreModule_x64.log*.</span></span>

## <a name="module-schema-and-configuration-file-locations"></a><span data-ttu-id="fbe92-397">모듈, 스키마 및 구성 파일 위치</span><span class="sxs-lookup"><span data-stu-id="fbe92-397">Module, schema, and configuration file locations</span></span>

### <a name="module"></a><span data-ttu-id="fbe92-398">Module</span><span class="sxs-lookup"><span data-stu-id="fbe92-398">Module</span></span>

<span data-ttu-id="fbe92-399">**IIS(x86/amd64):**</span><span class="sxs-lookup"><span data-stu-id="fbe92-399">**IIS (x86/amd64):**</span></span>

   * <span data-ttu-id="fbe92-400">%windir%\System32\inetsrv\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="fbe92-400">%windir%\System32\inetsrv\aspnetcore.dll</span></span>

   * <span data-ttu-id="fbe92-401">%windir%\SysWOW64\inetsrv\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="fbe92-401">%windir%\SysWOW64\inetsrv\aspnetcore.dll</span></span>

::: moniker range=">= aspnetcore-2.2"

   * <span data-ttu-id="fbe92-402">%ProgramFiles%\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll</span><span class="sxs-lookup"><span data-stu-id="fbe92-402">%ProgramFiles%\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll</span></span>

   * <span data-ttu-id="fbe92-403">%ProgramFiles(x86)%\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll</span><span class="sxs-lookup"><span data-stu-id="fbe92-403">%ProgramFiles(x86)%\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll</span></span>

::: moniker-end

<span data-ttu-id="fbe92-404">**IIS Express(x86/amd64):**</span><span class="sxs-lookup"><span data-stu-id="fbe92-404">**IIS Express (x86/amd64):**</span></span>

   * <span data-ttu-id="fbe92-405">%ProgramFiles%\IIS Express\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="fbe92-405">%ProgramFiles%\IIS Express\aspnetcore.dll</span></span>

   * <span data-ttu-id="fbe92-406">%ProgramFiles(x86)%\IIS Express\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="fbe92-406">%ProgramFiles(x86)%\IIS Express\aspnetcore.dll</span></span>

::: moniker range=">= aspnetcore-2.2"

   * <span data-ttu-id="fbe92-407">%ProgramFiles%\IIS Express\Asp.Net Core Module\V2\aspnetcorev2.dll</span><span class="sxs-lookup"><span data-stu-id="fbe92-407">%ProgramFiles%\IIS Express\Asp.Net Core Module\V2\aspnetcorev2.dll</span></span>

   * <span data-ttu-id="fbe92-408">%ProgramFiles(x86)%\IIS Express\Asp.Net Core Module\V2\aspnetcorev2.dll</span><span class="sxs-lookup"><span data-stu-id="fbe92-408">%ProgramFiles(x86)%\IIS Express\Asp.Net Core Module\V2\aspnetcorev2.dll</span></span>

::: moniker-end

### <a name="schema"></a><span data-ttu-id="fbe92-409">스키마</span><span class="sxs-lookup"><span data-stu-id="fbe92-409">Schema</span></span>

<span data-ttu-id="fbe92-410">**IIS**</span><span class="sxs-lookup"><span data-stu-id="fbe92-410">**IIS**</span></span>

   * <span data-ttu-id="fbe92-411">%windir%\System32\inetsrv\config\schema\aspnetcore_schema.xml</span><span class="sxs-lookup"><span data-stu-id="fbe92-411">%windir%\System32\inetsrv\config\schema\aspnetcore_schema.xml</span></span>

::: moniker range=">= aspnetcore-2.2"

   * <span data-ttu-id="fbe92-412">%windir%\System32\inetsrv\config\schema\aspnetcore_schema_v2.xml</span><span class="sxs-lookup"><span data-stu-id="fbe92-412">%windir%\System32\inetsrv\config\schema\aspnetcore_schema_v2.xml</span></span>

::: moniker-end
<span data-ttu-id="fbe92-413">**IIS Express**</span><span class="sxs-lookup"><span data-stu-id="fbe92-413">**IIS Express**</span></span>

   * <span data-ttu-id="fbe92-414">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema.xml</span><span class="sxs-lookup"><span data-stu-id="fbe92-414">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema.xml</span></span>

::: moniker range=">= aspnetcore-2.2"

   * <span data-ttu-id="fbe92-415">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema_v2.xml</span><span class="sxs-lookup"><span data-stu-id="fbe92-415">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema_v2.xml</span></span>

::: moniker-end

### <a name="configuration"></a><span data-ttu-id="fbe92-416">구성</span><span class="sxs-lookup"><span data-stu-id="fbe92-416">Configuration</span></span>

<span data-ttu-id="fbe92-417">**IIS**</span><span class="sxs-lookup"><span data-stu-id="fbe92-417">**IIS**</span></span>

   * <span data-ttu-id="fbe92-418">%windir%\System32\inetsrv\config\applicationHost.config</span><span class="sxs-lookup"><span data-stu-id="fbe92-418">%windir%\System32\inetsrv\config\applicationHost.config</span></span>

<span data-ttu-id="fbe92-419">**IIS Express**</span><span class="sxs-lookup"><span data-stu-id="fbe92-419">**IIS Express**</span></span>

   * <span data-ttu-id="fbe92-420">%ProgramFiles%\IIS Express\config\templates\PersonalWebServer\applicationHost.config</span><span class="sxs-lookup"><span data-stu-id="fbe92-420">%ProgramFiles%\IIS Express\config\templates\PersonalWebServer\applicationHost.config</span></span>

<span data-ttu-id="fbe92-421">*applicationHost.config* 파일에서 *aspnetcore*를 검색하여 파일을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbe92-421">The files can be found by searching for *aspnetcore* in the *applicationHost.config* file.</span></span>