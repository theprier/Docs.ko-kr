---
title: ASP.NET Core 모듈 구성 참조
author: guardrex
description: ASP.NET Core 앱을 호스팅하기 위해 ASP.NET Core 모듈을 구성하는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 09/21/2018
uid: host-and-deploy/aspnet-core-module
ms.openlocfilehash: 0ae19b26bc86c9da7a61f3117aaae1844115593a
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "48913283"
---
# <a name="aspnet-core-module-configuration-reference"></a><span data-ttu-id="bf182-103">ASP.NET Core 모듈 구성 참조</span><span class="sxs-lookup"><span data-stu-id="bf182-103">ASP.NET Core Module configuration reference</span></span>

<span data-ttu-id="bf182-104">작성자: [Luke Latham](https://github.com/guardrex), [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Sourabh Shirhatti](https://twitter.com/sshirhatti)</span><span class="sxs-lookup"><span data-stu-id="bf182-104">By [Luke Latham](https://github.com/guardrex), [Rick Anderson](https://twitter.com/RickAndMSFT), and [Sourabh Shirhatti](https://twitter.com/sshirhatti)</span></span>

<span data-ttu-id="bf182-105">이 문서에서는 ASP.NET Core 앱을 호스트하기 위해 ASP.NET Core 모듈을 구성하는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-105">This document provides instructions on how to configure the ASP.NET Core Module for hosting ASP.NET Core apps.</span></span> <span data-ttu-id="bf182-106">ASP.NET Core 모듈 및 설치 지침에 대한 개요는 [ASP.NET Core 모듈 개요](xref:fundamentals/servers/aspnet-core-module)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf182-106">For an introduction to the ASP.NET Core Module and installation instructions, see the [ASP.NET Core Module overview](xref:fundamentals/servers/aspnet-core-module).</span></span>

::: moniker range=">= aspnetcore-2.2"

## <a name="hosting-model"></a><span data-ttu-id="bf182-107">호스팅 모델</span><span class="sxs-lookup"><span data-stu-id="bf182-107">Hosting model</span></span>

<span data-ttu-id="bf182-108">.NET Core 2.2 이상에서 실행되는 앱의 경우, 모듈에서는 역방향 프록시(Out-of-Process) 호스팅과 비교할 때 더 나은 성능을 제공하기 위해 In-Process 호스팅 모델을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-108">For apps running on .NET Core 2.2 or later, the module supports an in-process hosting model for improved performance compared to reverse-proxy (out-of-process) hosting.</span></span> <span data-ttu-id="bf182-109">자세한 내용은 <xref:fundamentals/servers/aspnet-core-module#aspnet-core-module-description>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf182-109">For more information, see <xref:fundamentals/servers/aspnet-core-module#aspnet-core-module-description>.</span></span>

<span data-ttu-id="bf182-110">In-Process 호스팅은 기존 앱에 대한 옵트인(opt in) 기능이지만 [dotnet new](/dotnet/core/tools/dotnet-new) 템플릿은 기본적으로 모든 IIS 및 IIS Express 시나리오에 대해 In-Process 호스팅 모델로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-110">In-procsess hosting is opt-in for existing apps, but [dotnet new](/dotnet/core/tools/dotnet-new) templates default to the in-process hosting model for all IIS and IIS Express scenarios.</span></span>

<span data-ttu-id="bf182-111">In-Process 호스팅용 앱을 구성하려면 `<AspNetCoreModuleHostingModel>` 속성을 `inprocess` 값의 앱 프로젝트 파일에 추가합니다(Out-of-Process 호스팅은 `outofprocess`로 설정됨).</span><span class="sxs-lookup"><span data-stu-id="bf182-111">To configure an app for in-process hosting, add the `<AspNetCoreModuleHostingModel>` property to the app's project file with a value of `inprocess` (out-of-process hosting is set with `outofprocess`):</span></span>

```xml
<PropertyGroup>
  <AspNetCoreModuleHostingModel>inprocess</AspNetCoreModuleHostingModel>
</PropertyGroup>
```

<span data-ttu-id="bf182-112">다음 특성은 In-Process로 호스팅할 때 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-112">The following characteristics apply when hosting in-process:</span></span>

* <span data-ttu-id="bf182-113">[Kestrel 서버](xref:fundamentals/servers/kestrel)가 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-113">The [Kestrel server](xref:fundamentals/servers/kestrel) isn't used.</span></span> <span data-ttu-id="bf182-114">사용자 지정 <xref:Microsoft.AspNetCore.Hosting.Server.IServer> 구현인 `IISHttpServer`가 앱의 서버 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-114">A custom <xref:Microsoft.AspNetCore.Hosting.Server.IServer> implementation, `IISHttpServer` acts as the app's server.</span></span>

* <span data-ttu-id="bf182-115">[requestTimeout 특성](#attributes-of-the-aspnetcore-element)이 In-Process 호스팅에 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-115">The [requestTimeout attribute](#attributes-of-the-aspnetcore-element) doesn't apply to in-process hosting.</span></span>

* <span data-ttu-id="bf182-116">앱 간의 앱 풀 공유는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-116">Sharing an app pool among apps isn't supported.</span></span> <span data-ttu-id="bf182-117">앱당 하나의 앱 풀을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-117">Use one app pool per app.</span></span>

* <span data-ttu-id="bf182-118">[웹 배포](/iis/publish/using-web-deploy/introduction-to-web-deploy)를 사용하거나 [app_offline.htm 파일을 배포에](xref:host-and-deploy/iis/index#locked-deployment-files) 수동으로 배치할 경우 열린 연결이 있으면 앱이 즉시 종료되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-118">When using [Web Deploy](/iis/publish/using-web-deploy/introduction-to-web-deploy) or manually placing an [app_offline.htm file in the deployment](xref:host-and-deploy/iis/index#locked-deployment-files), the app might not shut down immediately if there's an open connection.</span></span> <span data-ttu-id="bf182-119">예를 들어, WebSocket 연결은 앱 종료를 지연시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-119">For example, a websocket connection may delay app shut down.</span></span>

* <span data-ttu-id="bf182-120">앱 및 설치된 런타임(x64 또는 x86)의 아키텍처(비트)는 앱 풀의 아키텍처와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-120">The architecture (bitness) of the app and installed runtime (x64 or x86) must match the architecture of the app pool.</span></span>

* <span data-ttu-id="bf182-121">`WebHostBuilder`([CreateDefaultBuilder](xref:fundamentals/host/web-host#set-up-a-host)를 사용하지 않고)를 사용하여 앱 호스트를 수동으로 설정하며 앱이 Kestrel 서버에서 직접 실행되는 경우(자체 호스트됨) `UseIISIntegration`를 호출하기 전에 `UseKestrel`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-121">If setting up the app's host manually with `WebHostBuilder` (not using [CreateDefaultBuilder](xref:fundamentals/host/web-host#set-up-a-host)) and the app is ever run directly on the Kestrel server (self-hosted), call `UseKestrel` before calling `UseIISIntegration`.</span></span> <span data-ttu-id="bf182-122">이 순서가 바뀌면 호스트가 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-122">If the order is reversed, the host fails to start.</span></span>

### <a name="hosting-model-changes"></a><span data-ttu-id="bf182-123">호스팅 모델 변경</span><span class="sxs-lookup"><span data-stu-id="bf182-123">Hosting model changes</span></span>

<span data-ttu-id="bf182-124">`hostingModel` 설정이 *web.config* 파일에서 변경되면([web.config로 구성](#configuration-with-webconfig) 섹션에 설명되어 있음) 모듈은 IIS에 대한 작업자 프로세스를 재순환합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-124">If the `hostingModel` setting is changed in the *web.config* file (explained in the [Configuration with web.config](#configuration-with-webconfig) section), the module recycles the worker process for IIS.</span></span>

<span data-ttu-id="bf182-125">IIS Express의 경우 모듈은 작업자 프로세스를 재순환하지 않고, 대신 현재 IIS Express 프로세스의 정상 종료를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-125">For IIS Express, the module doesn't recycle the worker process but instead triggers a graceful shutdown of the current IIS Express process.</span></span> <span data-ttu-id="bf182-126">앱에 대한 다음 요청은 새 IIS Express 프로세스를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-126">The next request to the app spawns a new IIS Express process.</span></span>

### <a name="process-name"></a><span data-ttu-id="bf182-127">프로세스 이름</span><span class="sxs-lookup"><span data-stu-id="bf182-127">Process name</span></span>

<span data-ttu-id="bf182-128">`Process.GetCurrentProcess().ProcessName`은 `w3wp`(In-Process) 또는 `dotnet`(Out-of-Process)을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-128">`Process.GetCurrentProcess().ProcessName` reports either `w3wp` (in-process) or `dotnet` (out-of-process).</span></span>

::: moniker-end

## <a name="configuration-with-webconfig"></a><span data-ttu-id="bf182-129">web.config를 사용한 구성</span><span class="sxs-lookup"><span data-stu-id="bf182-129">Configuration with web.config</span></span>

<span data-ttu-id="bf182-130">ASP.NET Core 모듈은 사이트의 *web.config* 파일에 있는 `system.webServer` 노드의 `aspNetCore` 섹션으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-130">The ASP.NET Core Module is configured with the `aspNetCore` section of the `system.webServer` node in the site's *web.config* file.</span></span>

<span data-ttu-id="bf182-131">다음 *web.config* 파일은 [프레임워크 종속 배포](/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd)를 위해 게시되고 사이트 요청을 처리하도록 ASP.NET Core 모듈을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-131">The following *web.config* file is published for a [framework-dependent deployment](/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd) and configures the ASP.NET Core Module to handle site requests:</span></span>

::: moniker range=">= aspnetcore-2.2"

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
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

<span data-ttu-id="bf182-132">다음 *web.config*는 [자체 포함 배포](/dotnet/articles/core/deploying/#self-contained-deployments-scd)를 위해 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-132">The following *web.config* is published for a [self-contained deployment](/dotnet/articles/core/deploying/#self-contained-deployments-scd):</span></span>

::: moniker range=">= aspnetcore-2.2"

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModuleV2" resourceType="Unspecified" />
    </handlers>
    <aspNetCore processPath=".\MyApp.exe" 
                stdoutLogEnabled="false" 
                stdoutLogFile=".\logs\stdout" 
                hostingModel="inprocess" />
  </system.webServer>
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

<span data-ttu-id="bf182-133">앱이 [Azure App Service](https://azure.microsoft.com/services/app-service/)에 배포되면 `stdoutLogFile` 경로가 `\\?\%home%\LogFiles\stdout`로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-133">When an app is deployed to [Azure App Service](https://azure.microsoft.com/services/app-service/), the `stdoutLogFile` path is set to `\\?\%home%\LogFiles\stdout`.</span></span> <span data-ttu-id="bf182-134">이 경로는 서비스에서 자동으로 만들어진 위치인 *LogFiles* 폴더에 stdout 로그를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-134">The path saves stdout logs to the *LogFiles* folder, which is a location automatically created by the service.</span></span>

<span data-ttu-id="bf182-135">하위 앱에서 *web.config* 파일의 구성에 관한 중요 참고 사항은 [하위 응용 프로그램 구성](xref:host-and-deploy/iis/index#sub-application-configuration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf182-135">See [Sub-application configuration](xref:host-and-deploy/iis/index#sub-application-configuration) for an important note pertaining to the configuration of *web.config* files in sub-apps.</span></span>

### <a name="attributes-of-the-aspnetcore-element"></a><span data-ttu-id="bf182-136">aspNetCore 요소의 특성</span><span class="sxs-lookup"><span data-stu-id="bf182-136">Attributes of the aspNetCore element</span></span>

::: moniker range=">= aspnetcore-2.2"

| <span data-ttu-id="bf182-137">특성</span><span class="sxs-lookup"><span data-stu-id="bf182-137">Attribute</span></span> | <span data-ttu-id="bf182-138">설명</span><span class="sxs-lookup"><span data-stu-id="bf182-138">Description</span></span> | <span data-ttu-id="bf182-139">기본</span><span class="sxs-lookup"><span data-stu-id="bf182-139">Default</span></span> |
| --------- | ----------- | :-----: |
| `arguments` | <p><span data-ttu-id="bf182-140">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-140">Optional string attribute.</span></span></p><p><span data-ttu-id="bf182-141">**processPath**에 지정된 실행 파일에 대한 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-141">Arguments to the executable specified in **processPath**.</span></span></p>| |
| `disableStartUpErrorPage` | <p><span data-ttu-id="bf182-142">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-142">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="bf182-143">true인 경우 **502.5 - 프로세스 실패** 페이지가 표시되지 않고 *web.config*에 구성된 502 상태 코드 페이지가 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-143">If true, the **502.5 - Process Failure** page is suppressed, and the 502 status code page configured in the *web.config* takes precedence.</span></span></p> | `false` |
| `forwardWindowsAuthToken` | <p><span data-ttu-id="bf182-144">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-144">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="bf182-145">true인 경우 토큰은 %ASPNETCORE_PORT%에서 수신 대기하는 자식 프로세스에 요청별 헤더 'MS-ASPNETCORE-WINAUTHTOKEN'으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-145">If true, the token is forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="bf182-146">이 프로세스는 요청별로 이 토큰에서 CloseHandle을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-146">It's the responsibility of that process to call CloseHandle on this token per request.</span></span></p> | `true` |
| `hostingModel` | <p><span data-ttu-id="bf182-147">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-147">Optional string attribute.</span></span></p><p><span data-ttu-id="bf182-148">호스팅 모델을 In-Process(`inprocess`) 또는 Out-of-Process(`outofprocess`)로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-148">Specifies the hosting model as in-process (`inprocess`) or out-of-process (`outofprocess`).</span></span></p> | `outofprocess` |
| `processesPerApplication` | <p><span data-ttu-id="bf182-149">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-149">Optional integer attribute.</span></span></p><p><span data-ttu-id="bf182-150">앱별로 스핀 업할 수 있는 **processPath** 설정에 지정된 프로세스의 인스턴스 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-150">Specifies the number of instances of the process specified in the **processPath** setting that can be spun up per app.</span></span></p><p><span data-ttu-id="bf182-151">&dagger;In-Process 호스팅의 경우 이 값은 `1`로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-151">&dagger;For in-process hosting, the value is limited to `1`.</span></span></p> | <span data-ttu-id="bf182-152">기본값: `1`</span><span class="sxs-lookup"><span data-stu-id="bf182-152">Default: `1`</span></span><br><span data-ttu-id="bf182-153">최소: `1`</span><span class="sxs-lookup"><span data-stu-id="bf182-153">Min: `1`</span></span><br><span data-ttu-id="bf182-154">최대: `100`&dagger;</span><span class="sxs-lookup"><span data-stu-id="bf182-154">Max: `100`&dagger;</span></span> |
| `processPath` | <p><span data-ttu-id="bf182-155">필수 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-155">Required string attribute.</span></span></p><p><span data-ttu-id="bf182-156">HTTP 요청을 수신 대기하는 프로세스를 시작하는 실행 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-156">Path to the executable that launches a process listening for HTTP requests.</span></span> <span data-ttu-id="bf182-157">상대 경로가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-157">Relative paths are supported.</span></span> <span data-ttu-id="bf182-158">경로가 `.`로 시작되면 경로는 사이트 루트의 상대 경로로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-158">If the path begins with `.`, the path is considered to be relative to the site root.</span></span></p> | |
| `rapidFailsPerMinute` | <p><span data-ttu-id="bf182-159">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-159">Optional integer attribute.</span></span></p><p><span data-ttu-id="bf182-160">**processPath**에 지정된 프로세스의 분당 크래시 허용 횟수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-160">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="bf182-161">이 제한을 초과하면 모듈은 남은 시간 동안 프로세스 시작을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-161">If this limit is exceeded, the module stops launching the process for the remainder of the minute.</span></span></p><p><span data-ttu-id="bf182-162">In-Process 호스팅에서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-162">Not supported with in-process hosting.</span></span></p> | <span data-ttu-id="bf182-163">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="bf182-163">Default: `10`</span></span><br><span data-ttu-id="bf182-164">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="bf182-164">Min: `0`</span></span><br><span data-ttu-id="bf182-165">최대: `100`</span><span class="sxs-lookup"><span data-stu-id="bf182-165">Max: `100`</span></span> |
| `requestTimeout` | <p><span data-ttu-id="bf182-166">선택적 시간 간격 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-166">Optional timespan attribute.</span></span></p><p><span data-ttu-id="bf182-167">ASP.NET Core 모듈이 %ASPNETCORE_PORT%에서 수신 대기하는 프로세스의 응답을 기다리는 기간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-167">Specifies the duration for which the ASP.NET Core Module waits for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="bf182-168">ASP.NET Core 2.1 이상 릴리스와 함께 제공되는 ASP.NET Core 모듈 버전에서는 `requestTimeout`이 전체 시간, 분, 초로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-168">In versions of the ASP.NET Core Module that shipped with the release of ASP.NET Core 2.1 or later, the `requestTimeout` is specified in hours, minutes, and seconds.</span></span></p><p><span data-ttu-id="bf182-169">In-Process 호스팅에는 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-169">Doesn't apply to in-process hosting.</span></span> <span data-ttu-id="bf182-170">In-Process 호스팅의 경우 모듈은 앱이 요청을 처리할 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-170">For in-process hosting, the module waits for the app to process the request.</span></span></p> | <span data-ttu-id="bf182-171">기본값: `00:02:00`</span><span class="sxs-lookup"><span data-stu-id="bf182-171">Default: `00:02:00`</span></span><br><span data-ttu-id="bf182-172">최소: `00:00:00`</span><span class="sxs-lookup"><span data-stu-id="bf182-172">Min: `00:00:00`</span></span><br><span data-ttu-id="bf182-173">최대: `360:00:00`</span><span class="sxs-lookup"><span data-stu-id="bf182-173">Max: `360:00:00`</span></span> |
| `shutdownTimeLimit` | <p><span data-ttu-id="bf182-174">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-174">Optional integer attribute.</span></span></p><p><span data-ttu-id="bf182-175">*app_offline.htm* 파일이 검색될 때 실행 파일이 정상적으로 종료될 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-175">Duration in seconds that the module waits for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p> | <span data-ttu-id="bf182-176">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="bf182-176">Default: `10`</span></span><br><span data-ttu-id="bf182-177">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="bf182-177">Min: `0`</span></span><br><span data-ttu-id="bf182-178">최대: `600`</span><span class="sxs-lookup"><span data-stu-id="bf182-178">Max: `600`</span></span> |
| `startupTimeLimit` | <p><span data-ttu-id="bf182-179">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-179">Optional integer attribute.</span></span></p><p><span data-ttu-id="bf182-180">실행 파일이 포트에서 수신 대기하는 프로세스를 시작할 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-180">Duration in seconds that the module waits for the executable to start a process listening on the port.</span></span> <span data-ttu-id="bf182-181">이 시간 제한을 초과하면 모듈이 프로세스를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-181">If this time limit is exceeded, the module kills the process.</span></span> <span data-ttu-id="bf182-182">모듈은 새 요청을 수신할 때 프로세스를 다시 시작하려고 하고, 마지막 롤링 기간(분)에 앱이 **rapidFailsPerMinute**번 시작에 실패한 경우가 아니면 이후 요청이 들어올 때 프로세스를 계속 다시 시작하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-182">The module attempts to relaunch the process when it receives a new request and continues to attempt to restart the process on subsequent incoming requests unless the app fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p><p><span data-ttu-id="bf182-183">값 0은 무한 시간 제한으로 간주되지 **않습니다**.</span><span class="sxs-lookup"><span data-stu-id="bf182-183">A value of 0 (zero) is **not** considered an infinite timeout.</span></span></p> | <span data-ttu-id="bf182-184">기본값: `120`</span><span class="sxs-lookup"><span data-stu-id="bf182-184">Default: `120`</span></span><br><span data-ttu-id="bf182-185">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="bf182-185">Min: `0`</span></span><br><span data-ttu-id="bf182-186">최대: `3600`</span><span class="sxs-lookup"><span data-stu-id="bf182-186">Max: `3600`</span></span> |
| `stdoutLogEnabled` | <p><span data-ttu-id="bf182-187">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-187">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="bf182-188">true인 경우 **processPath**에 지정된 프로세스에 대한 **stdout** 및 **stderr**이 **stdoutLogFile**에 지정된 파일로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-188">If true, **stdout** and **stderr** for the process specified in **processPath** are redirected to the file specified in **stdoutLogFile**.</span></span></p> | `false` |
| `stdoutLogFile` | <p><span data-ttu-id="bf182-189">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-189">Optional string attribute.</span></span></p><p><span data-ttu-id="bf182-190">**processPath**에 지정된 프로세스에서 **stdout** 및 **stderr**이 기록되는 상대 또는 절대 파일 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-190">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** are logged.</span></span> <span data-ttu-id="bf182-191">상대 경로는 사이트 루트에 상대적인 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-191">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="bf182-192">`.`로 시작하는 모든 경로는 사이트 루트에 상대적인 경로이고 다른 모든 경로는 절대 경로로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-192">Any path starting with `.` are relative to the site root and all other paths are treated as absolute paths.</span></span> <span data-ttu-id="bf182-193">모듈이 로그 파일을 만들려면 경로에 제공된 모든 폴더가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-193">Any folders provided in the path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="bf182-194">타임스탬프, 프로세스 ID 및 파일 확장명(*.log*)은 밑줄 구분 기호를 사용하여 **stdoutLogFile** 경로의 마지막 세그먼트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-194">Using underscore delimiters, a timestamp, process ID, and file extension (*.log*) are added to the last segment of the **stdoutLogFile** path.</span></span> <span data-ttu-id="bf182-195">`.\logs\stdout`이 값으로 제공되는 경우 예제 stdout 로그는 2018년 2월 5일 19시 41분 32초에 프로세스 ID 1934를 사용하여 저장될 경우 *logs* 폴더에 *stdout_20180205194132_1934.log*로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-195">If `.\logs\stdout` is supplied as a value, an example stdout log is saved as *stdout_20180205194132_1934.log* in the *logs* folder when saved on 2/5/2018 at 19:41:32 with a process ID of 1934.</span></span></p> | `aspnetcore-stdout` |

::: moniker-end

::: moniker range="= aspnetcore-2.1"

| <span data-ttu-id="bf182-196">특성</span><span class="sxs-lookup"><span data-stu-id="bf182-196">Attribute</span></span> | <span data-ttu-id="bf182-197">설명</span><span class="sxs-lookup"><span data-stu-id="bf182-197">Description</span></span> | <span data-ttu-id="bf182-198">기본</span><span class="sxs-lookup"><span data-stu-id="bf182-198">Default</span></span> |
| --------- | ----------- | :-----: |
| `arguments` | <p><span data-ttu-id="bf182-199">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-199">Optional string attribute.</span></span></p><p><span data-ttu-id="bf182-200">**processPath**에 지정된 실행 파일에 대한 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-200">Arguments to the executable specified in **processPath**.</span></span></p>| |
| `disableStartUpErrorPage` | <p><span data-ttu-id="bf182-201">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-201">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="bf182-202">true인 경우 **502.5 - 프로세스 실패** 페이지가 표시되지 않고 *web.config*에 구성된 502 상태 코드 페이지가 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-202">If true, the **502.5 - Process Failure** page is suppressed, and the 502 status code page configured in the *web.config* takes precedence.</span></span></p> | `false` |
| `forwardWindowsAuthToken` | <p><span data-ttu-id="bf182-203">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-203">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="bf182-204">true인 경우 토큰은 %ASPNETCORE_PORT%에서 수신 대기하는 자식 프로세스에 요청별 헤더 'MS-ASPNETCORE-WINAUTHTOKEN'으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-204">If true, the token is forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="bf182-205">이 프로세스는 요청별로 이 토큰에서 CloseHandle을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-205">It's the responsibility of that process to call CloseHandle on this token per request.</span></span></p> | `true` |
| `processesPerApplication` | <p><span data-ttu-id="bf182-206">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-206">Optional integer attribute.</span></span></p><p><span data-ttu-id="bf182-207">앱별로 스핀 업할 수 있는 **processPath** 설정에 지정된 프로세스의 인스턴스 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-207">Specifies the number of instances of the process specified in the **processPath** setting that can be spun up per app.</span></span></p> | <span data-ttu-id="bf182-208">기본값: `1`</span><span class="sxs-lookup"><span data-stu-id="bf182-208">Default: `1`</span></span><br><span data-ttu-id="bf182-209">최소: `1`</span><span class="sxs-lookup"><span data-stu-id="bf182-209">Min: `1`</span></span><br><span data-ttu-id="bf182-210">최대: `100`</span><span class="sxs-lookup"><span data-stu-id="bf182-210">Max: `100`</span></span> |
| `processPath` | <p><span data-ttu-id="bf182-211">필수 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-211">Required string attribute.</span></span></p><p><span data-ttu-id="bf182-212">HTTP 요청을 수신 대기하는 프로세스를 시작하는 실행 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-212">Path to the executable that launches a process listening for HTTP requests.</span></span> <span data-ttu-id="bf182-213">상대 경로가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-213">Relative paths are supported.</span></span> <span data-ttu-id="bf182-214">경로가 `.`로 시작되면 경로는 사이트 루트의 상대 경로로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-214">If the path begins with `.`, the path is considered to be relative to the site root.</span></span></p> | |
| `rapidFailsPerMinute` | <p><span data-ttu-id="bf182-215">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-215">Optional integer attribute.</span></span></p><p><span data-ttu-id="bf182-216">**processPath**에 지정된 프로세스의 분당 크래시 허용 횟수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-216">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="bf182-217">이 제한을 초과하면 모듈은 남은 시간 동안 프로세스 시작을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-217">If this limit is exceeded, the module stops launching the process for the remainder of the minute.</span></span></p> | <span data-ttu-id="bf182-218">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="bf182-218">Default: `10`</span></span><br><span data-ttu-id="bf182-219">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="bf182-219">Min: `0`</span></span><br><span data-ttu-id="bf182-220">최대: `100`</span><span class="sxs-lookup"><span data-stu-id="bf182-220">Max: `100`</span></span> |
| `requestTimeout` | <p><span data-ttu-id="bf182-221">선택적 시간 간격 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-221">Optional timespan attribute.</span></span></p><p><span data-ttu-id="bf182-222">ASP.NET Core 모듈이 %ASPNETCORE_PORT%에서 수신 대기하는 프로세스의 응답을 기다리는 기간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-222">Specifies the duration for which the ASP.NET Core Module waits for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="bf182-223">ASP.NET Core 2.1 이상 릴리스와 함께 제공되는 ASP.NET Core 모듈 버전에서는 `requestTimeout`이 전체 시간, 분, 초로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-223">In versions of the ASP.NET Core Module that shipped with the release of ASP.NET Core 2.1 or later, the `requestTimeout` is specified in hours, minutes, and seconds.</span></span></p> | <span data-ttu-id="bf182-224">기본값: `00:02:00`</span><span class="sxs-lookup"><span data-stu-id="bf182-224">Default: `00:02:00`</span></span><br><span data-ttu-id="bf182-225">최소: `00:00:00`</span><span class="sxs-lookup"><span data-stu-id="bf182-225">Min: `00:00:00`</span></span><br><span data-ttu-id="bf182-226">최대: `360:00:00`</span><span class="sxs-lookup"><span data-stu-id="bf182-226">Max: `360:00:00`</span></span> |
| `shutdownTimeLimit` | <p><span data-ttu-id="bf182-227">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-227">Optional integer attribute.</span></span></p><p><span data-ttu-id="bf182-228">*app_offline.htm* 파일이 검색될 때 실행 파일이 정상적으로 종료될 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-228">Duration in seconds that the module waits for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p> | <span data-ttu-id="bf182-229">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="bf182-229">Default: `10`</span></span><br><span data-ttu-id="bf182-230">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="bf182-230">Min: `0`</span></span><br><span data-ttu-id="bf182-231">최대: `600`</span><span class="sxs-lookup"><span data-stu-id="bf182-231">Max: `600`</span></span> |
| `startupTimeLimit` | <p><span data-ttu-id="bf182-232">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-232">Optional integer attribute.</span></span></p><p><span data-ttu-id="bf182-233">실행 파일이 포트에서 수신 대기하는 프로세스를 시작할 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-233">Duration in seconds that the module waits for the executable to start a process listening on the port.</span></span> <span data-ttu-id="bf182-234">이 시간 제한을 초과하면 모듈이 프로세스를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-234">If this time limit is exceeded, the module kills the process.</span></span> <span data-ttu-id="bf182-235">모듈은 새 요청을 수신할 때 프로세스를 다시 시작하려고 하고, 마지막 롤링 기간(분)에 앱이 **rapidFailsPerMinute**번 시작에 실패한 경우가 아니면 이후 요청이 들어올 때 프로세스를 계속 다시 시작하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-235">The module attempts to relaunch the process when it receives a new request and continues to attempt to restart the process on subsequent incoming requests unless the app fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p><p><span data-ttu-id="bf182-236">값 0은 무한 시간 제한으로 간주되지 **않습니다**.</span><span class="sxs-lookup"><span data-stu-id="bf182-236">A value of 0 (zero) is **not** considered an infinite timeout.</span></span></p> | <span data-ttu-id="bf182-237">기본값: `120`</span><span class="sxs-lookup"><span data-stu-id="bf182-237">Default: `120`</span></span><br><span data-ttu-id="bf182-238">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="bf182-238">Min: `0`</span></span><br><span data-ttu-id="bf182-239">최대: `3600`</span><span class="sxs-lookup"><span data-stu-id="bf182-239">Max: `3600`</span></span> |
| `stdoutLogEnabled` | <p><span data-ttu-id="bf182-240">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-240">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="bf182-241">true인 경우 **processPath**에 지정된 프로세스에 대한 **stdout** 및 **stderr**이 **stdoutLogFile**에 지정된 파일로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-241">If true, **stdout** and **stderr** for the process specified in **processPath** are redirected to the file specified in **stdoutLogFile**.</span></span></p> | `false` |
| `stdoutLogFile` | <p><span data-ttu-id="bf182-242">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-242">Optional string attribute.</span></span></p><p><span data-ttu-id="bf182-243">**processPath**에 지정된 프로세스에서 **stdout** 및 **stderr**이 기록되는 상대 또는 절대 파일 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-243">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** are logged.</span></span> <span data-ttu-id="bf182-244">상대 경로는 사이트 루트에 상대적인 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-244">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="bf182-245">`.`로 시작하는 모든 경로는 사이트 루트에 상대적인 경로이고 다른 모든 경로는 절대 경로로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-245">Any path starting with `.` are relative to the site root and all other paths are treated as absolute paths.</span></span> <span data-ttu-id="bf182-246">모듈이 로그 파일을 만들려면 경로에 제공된 모든 폴더가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-246">Any folders provided in the path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="bf182-247">타임스탬프, 프로세스 ID 및 파일 확장명(*.log*)은 밑줄 구분 기호를 사용하여 **stdoutLogFile** 경로의 마지막 세그먼트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-247">Using underscore delimiters, a timestamp, process ID, and file extension (*.log*) are added to the last segment of the **stdoutLogFile** path.</span></span> <span data-ttu-id="bf182-248">`.\logs\stdout`이 값으로 제공되는 경우 예제 stdout 로그는 2018년 2월 5일 19시 41분 32초에 프로세스 ID 1934를 사용하여 저장될 경우 *logs* 폴더에 *stdout_20180205194132_1934.log*로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-248">If `.\logs\stdout` is supplied as a value, an example stdout log is saved as *stdout_20180205194132_1934.log* in the *logs* folder when saved on 2/5/2018 at 19:41:32 with a process ID of 1934.</span></span></p> | `aspnetcore-stdout` |

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

| <span data-ttu-id="bf182-249">특성</span><span class="sxs-lookup"><span data-stu-id="bf182-249">Attribute</span></span> | <span data-ttu-id="bf182-250">설명</span><span class="sxs-lookup"><span data-stu-id="bf182-250">Description</span></span> | <span data-ttu-id="bf182-251">기본</span><span class="sxs-lookup"><span data-stu-id="bf182-251">Default</span></span> |
| --------- | ----------- | :-----: |
| `arguments` | <p><span data-ttu-id="bf182-252">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-252">Optional string attribute.</span></span></p><p><span data-ttu-id="bf182-253">**processPath**에 지정된 실행 파일에 대한 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-253">Arguments to the executable specified in **processPath**.</span></span></p>| |
| `disableStartUpErrorPage` | <p><span data-ttu-id="bf182-254">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-254">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="bf182-255">true인 경우 **502.5 - 프로세스 실패** 페이지가 표시되지 않고 *web.config*에 구성된 502 상태 코드 페이지가 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-255">If true, the **502.5 - Process Failure** page is suppressed, and the 502 status code page configured in the *web.config* takes precedence.</span></span></p> | `false` |
| `forwardWindowsAuthToken` | <p><span data-ttu-id="bf182-256">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-256">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="bf182-257">true인 경우 토큰은 %ASPNETCORE_PORT%에서 수신 대기하는 자식 프로세스에 요청별 헤더 'MS-ASPNETCORE-WINAUTHTOKEN'으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-257">If true, the token is forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="bf182-258">이 프로세스는 요청별로 이 토큰에서 CloseHandle을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-258">It's the responsibility of that process to call CloseHandle on this token per request.</span></span></p> | `true` |
| `processesPerApplication` | <p><span data-ttu-id="bf182-259">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-259">Optional integer attribute.</span></span></p><p><span data-ttu-id="bf182-260">앱별로 스핀 업할 수 있는 **processPath** 설정에 지정된 프로세스의 인스턴스 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-260">Specifies the number of instances of the process specified in the **processPath** setting that can be spun up per app.</span></span></p> | <span data-ttu-id="bf182-261">기본값: `1`</span><span class="sxs-lookup"><span data-stu-id="bf182-261">Default: `1`</span></span><br><span data-ttu-id="bf182-262">최소: `1`</span><span class="sxs-lookup"><span data-stu-id="bf182-262">Min: `1`</span></span><br><span data-ttu-id="bf182-263">최대: `100`</span><span class="sxs-lookup"><span data-stu-id="bf182-263">Max: `100`</span></span> |
| `processPath` | <p><span data-ttu-id="bf182-264">필수 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-264">Required string attribute.</span></span></p><p><span data-ttu-id="bf182-265">HTTP 요청을 수신 대기하는 프로세스를 시작하는 실행 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-265">Path to the executable that launches a process listening for HTTP requests.</span></span> <span data-ttu-id="bf182-266">상대 경로가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-266">Relative paths are supported.</span></span> <span data-ttu-id="bf182-267">경로가 `.`로 시작되면 경로는 사이트 루트의 상대 경로로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-267">If the path begins with `.`, the path is considered to be relative to the site root.</span></span></p> | |
| `rapidFailsPerMinute` | <p><span data-ttu-id="bf182-268">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-268">Optional integer attribute.</span></span></p><p><span data-ttu-id="bf182-269">**processPath**에 지정된 프로세스의 분당 크래시 허용 횟수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-269">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="bf182-270">이 제한을 초과하면 모듈은 남은 시간 동안 프로세스 시작을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-270">If this limit is exceeded, the module stops launching the process for the remainder of the minute.</span></span></p> | <span data-ttu-id="bf182-271">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="bf182-271">Default: `10`</span></span><br><span data-ttu-id="bf182-272">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="bf182-272">Min: `0`</span></span><br><span data-ttu-id="bf182-273">최대: `100`</span><span class="sxs-lookup"><span data-stu-id="bf182-273">Max: `100`</span></span> |
| `requestTimeout` | <p><span data-ttu-id="bf182-274">선택적 시간 간격 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-274">Optional timespan attribute.</span></span></p><p><span data-ttu-id="bf182-275">ASP.NET Core 모듈이 %ASPNETCORE_PORT%에서 수신 대기하는 프로세스의 응답을 기다리는 기간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-275">Specifies the duration for which the ASP.NET Core Module waits for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="bf182-276">ASP.NET Core 2.0 이하 릴리스와 함께 제공되는 ASP.NET Core 모듈 버전에서는 `requestTimeout`을 전체 시간(분)으로만 지정해야 합니다. 그렇지 않으면 기본적으로 2분으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-276">In versions of the ASP.NET Core Module that shipped with the release of ASP.NET Core 2.0 or earlier, the `requestTimeout` must be specified in whole minutes only, otherwise it defaults to 2 minutes.</span></span></p> | <span data-ttu-id="bf182-277">기본값: `00:02:00`</span><span class="sxs-lookup"><span data-stu-id="bf182-277">Default: `00:02:00`</span></span><br><span data-ttu-id="bf182-278">최소: `00:00:00`</span><span class="sxs-lookup"><span data-stu-id="bf182-278">Min: `00:00:00`</span></span><br><span data-ttu-id="bf182-279">최대: `360:00:00`</span><span class="sxs-lookup"><span data-stu-id="bf182-279">Max: `360:00:00`</span></span> |
| `shutdownTimeLimit` | <p><span data-ttu-id="bf182-280">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-280">Optional integer attribute.</span></span></p><p><span data-ttu-id="bf182-281">*app_offline.htm* 파일이 검색될 때 실행 파일이 정상적으로 종료될 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-281">Duration in seconds that the module waits for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p> | <span data-ttu-id="bf182-282">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="bf182-282">Default: `10`</span></span><br><span data-ttu-id="bf182-283">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="bf182-283">Min: `0`</span></span><br><span data-ttu-id="bf182-284">최대: `600`</span><span class="sxs-lookup"><span data-stu-id="bf182-284">Max: `600`</span></span> |
| `startupTimeLimit` | <p><span data-ttu-id="bf182-285">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-285">Optional integer attribute.</span></span></p><p><span data-ttu-id="bf182-286">실행 파일이 포트에서 수신 대기하는 프로세스를 시작할 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-286">Duration in seconds that the module waits for the executable to start a process listening on the port.</span></span> <span data-ttu-id="bf182-287">이 시간 제한을 초과하면 모듈이 프로세스를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-287">If this time limit is exceeded, the module kills the process.</span></span> <span data-ttu-id="bf182-288">모듈은 새 요청을 수신할 때 프로세스를 다시 시작하려고 하고, 마지막 롤링 기간(분)에 앱이 **rapidFailsPerMinute**번 시작에 실패한 경우가 아니면 이후 요청이 들어올 때 프로세스를 계속 다시 시작하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-288">The module attempts to relaunch the process when it receives a new request and continues to attempt to restart the process on subsequent incoming requests unless the app fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p> | <span data-ttu-id="bf182-289">기본값: `120`</span><span class="sxs-lookup"><span data-stu-id="bf182-289">Default: `120`</span></span><br><span data-ttu-id="bf182-290">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="bf182-290">Min: `0`</span></span><br><span data-ttu-id="bf182-291">최대: `3600`</span><span class="sxs-lookup"><span data-stu-id="bf182-291">Max: `3600`</span></span> |
| `stdoutLogEnabled` | <p><span data-ttu-id="bf182-292">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-292">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="bf182-293">true인 경우 **processPath**에 지정된 프로세스에 대한 **stdout** 및 **stderr**이 **stdoutLogFile**에 지정된 파일로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-293">If true, **stdout** and **stderr** for the process specified in **processPath** are redirected to the file specified in **stdoutLogFile**.</span></span></p> | `false` |
| `stdoutLogFile` | <p><span data-ttu-id="bf182-294">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-294">Optional string attribute.</span></span></p><p><span data-ttu-id="bf182-295">**processPath**에 지정된 프로세스에서 **stdout** 및 **stderr**이 기록되는 상대 또는 절대 파일 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-295">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** are logged.</span></span> <span data-ttu-id="bf182-296">상대 경로는 사이트 루트에 상대적인 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-296">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="bf182-297">`.`로 시작하는 모든 경로는 사이트 루트에 상대적인 경로이고 다른 모든 경로는 절대 경로로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-297">Any path starting with `.` are relative to the site root and all other paths are treated as absolute paths.</span></span> <span data-ttu-id="bf182-298">모듈이 로그 파일을 만들려면 경로에 제공된 모든 폴더가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-298">Any folders provided in the path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="bf182-299">타임스탬프, 프로세스 ID 및 파일 확장명(*.log*)은 밑줄 구분 기호를 사용하여 **stdoutLogFile** 경로의 마지막 세그먼트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-299">Using underscore delimiters, a timestamp, process ID, and file extension (*.log*) are added to the last segment of the **stdoutLogFile** path.</span></span> <span data-ttu-id="bf182-300">`.\logs\stdout`이 값으로 제공되는 경우 예제 stdout 로그는 2018년 2월 5일 19시 41분 32초에 프로세스 ID 1934를 사용하여 저장될 경우 *logs* 폴더에 *stdout_20180205194132_1934.log*로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-300">If `.\logs\stdout` is supplied as a value, an example stdout log is saved as *stdout_20180205194132_1934.log* in the *logs* folder when saved on 2/5/2018 at 19:41:32 with a process ID of 1934.</span></span></p> | `aspnetcore-stdout` |

::: moniker-end

### <a name="setting-environment-variables"></a><span data-ttu-id="bf182-301">환경 변수 설정</span><span class="sxs-lookup"><span data-stu-id="bf182-301">Setting environment variables</span></span>

<span data-ttu-id="bf182-302">`processPath` 특성에서 프로세스에 대한 환경 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-302">Environment variables can be specified for the process in the `processPath` attribute.</span></span> <span data-ttu-id="bf182-303">`environmentVariables` 컬렉션 요소의 `environmentVariable` 자식 요소를 사용하여 환경 변수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-303">Specify an environment variable with the `environmentVariable` child element of an `environmentVariables` collection element.</span></span> <span data-ttu-id="bf182-304">이 섹션에 설정된 환경 변수가 시스템 환경 변수보다 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-304">Environment variables set in this section take precedence over system environment variables.</span></span>

<span data-ttu-id="bf182-305">다음 예제에서는 두 개의 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-305">The following example sets two environment variables.</span></span> <span data-ttu-id="bf182-306">`ASPNETCORE_ENVIRONMENT`는 앱의 환경을 `Development`로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-306">`ASPNETCORE_ENVIRONMENT` configures the app's environment to `Development`.</span></span> <span data-ttu-id="bf182-307">앱 예외를 디버그할 때 [개발자 예외 페이지](xref:fundamentals/error-handling)를 강제로 로드하기 위해 개발자가 *web.config* 파일에서 이 값을 일시적으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-307">A developer may temporarily set this value in the *web.config* file in order to force the [Developer Exception Page](xref:fundamentals/error-handling) to load when debugging an app exception.</span></span> <span data-ttu-id="bf182-308">`CONFIG_DIR`은 개발자가 앱 구성 파일을 로드할 경로를 생성하기 위해 시작 시 값을 읽는 코드를 작성한 사용자 정의 환경 변수의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-308">`CONFIG_DIR` is an example of a user-defined environment variable, where the developer has written code that reads the value on startup to form a path for loading the app's configuration file.</span></span>

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
> <span data-ttu-id="bf182-309">인터넷과 같은 신뢰할 수 없는 네트워크에 액세스할 수 없는 스테이징 및 테스트 서버에서는 `ASPNETCORE_ENVIRONMENT` 환경 변수를 `Development`로 설정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-309">Only set the `ASPNETCORE_ENVIRONMENT` environment variable to `Development` on staging and testing servers that aren't accessible to untrusted networks, such as the Internet.</span></span>

## <a name="appofflinehtm"></a><span data-ttu-id="bf182-310">app_offline.htm</span><span class="sxs-lookup"><span data-stu-id="bf182-310">app_offline.htm</span></span>

<span data-ttu-id="bf182-311">응용 프로그램의 루트 디렉터리에서 이름이 *app_offline.htm*인 파일이 검색되면 ASP.NET Core 모듈은 앱을 자동으로 종료하고 들어오는 요청 처리를 중지하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-311">If a file with the name *app_offline.htm* is detected in the root directory of an app, the ASP.NET Core Module attempts to gracefully shutdown the app and stop processing incoming requests.</span></span> <span data-ttu-id="bf182-312">`shutdownTimeLimit`에 정의된 시간(초) 후에도 앱이 계속 실행되면 ASP.NET Core 모듈은 실행 중인 프로세스를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-312">If the app is still running after the number of seconds defined in `shutdownTimeLimit`, the ASP.NET Core Module kills the running process.</span></span>

<span data-ttu-id="bf182-313">*app_offline.htm* 파일이 있는 동안 ASP.NET Core 모듈은 *app_offline.htm* 파일의 콘텐츠를 다시 보내 요청에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-313">While the *app_offline.htm* file is present, the ASP.NET Core Module responds to requests by sending back the contents of the *app_offline.htm* file.</span></span> <span data-ttu-id="bf182-314">*app_offline.htm* 파일이 제거되면 다음 요청이 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-314">When the *app_offline.htm* file is removed, the next request starts the app.</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="bf182-315">Out-of-Process 호스팅 모델을 사용할 때 열린 연결이 있으면 앱이 즉시 종료되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-315">When using the out-of-process hosting model, the app might not shut down immediately if there's an open connection.</span></span> <span data-ttu-id="bf182-316">예를 들어, WebSocket 연결은 앱 종료를 지연시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-316">For example, a websocket connection may delay app shut down.</span></span>

::: moniker-end

## <a name="start-up-error-page"></a><span data-ttu-id="bf182-317">시작 오류 페이지</span><span class="sxs-lookup"><span data-stu-id="bf182-317">Start-up error page</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="bf182-318">*호스팅에만 적용됩니다.*</span><span class="sxs-lookup"><span data-stu-id="bf182-318">*Only applies to out-of-process hosting.*</span></span>

::: moniker-end

<span data-ttu-id="bf182-319">ASP.NET Core 모듈이 백 엔드 프로세스를 시작하지 못하거나 백 엔드 프로세스가 시작되지만 구성된 포트에서 수신 대기하지 못하면 ‘502.5 프로세스 실패’ 상태 코드 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-319">If the ASP.NET Core Module fails to launch the backend process or the backend process starts but fails to listen on the configured port, a *502.5 Process Failure* status code page appears.</span></span> <span data-ttu-id="bf182-320">이 페이지를 표시하지 않고 기본 IIS 502 상태 코드 페이지로 되돌리려면 `disableStartUpErrorPage` 특성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-320">To suppress this page and revert to the default IIS 502 status code page, use the `disableStartUpErrorPage` attribute.</span></span> <span data-ttu-id="bf182-321">사용자 지정 오류 메시지 구성에 대한 자세한 내용은 [HTTP 오류`<httpErrors>`](/iis/configuration/system.webServer/httpErrors/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf182-321">For more information on configuring custom error messages, see [HTTP Errors `<httpErrors>`](/iis/configuration/system.webServer/httpErrors/).</span></span>

![502.5 프로세스 실패 상태 코드 페이지](aspnet-core-module/_static/ANCM-502_5.png)

## <a name="log-creation-and-redirection"></a><span data-ttu-id="bf182-323">로그 만들기 및 리디렉션</span><span class="sxs-lookup"><span data-stu-id="bf182-323">Log creation and redirection</span></span>

<span data-ttu-id="bf182-324">ASP.NET Core 모듈은 `aspNetCore` 요소의 `stdoutLogEnabled` 및 `stdoutLogFile` 특성이 설정된 경우 stdout 및 stderr 콘솔 출력을 디스크로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-324">The ASP.NET Core Module redirects stdout and stderr console output to disk if the `stdoutLogEnabled` and `stdoutLogFile` attributes of the `aspNetCore` element are set.</span></span> <span data-ttu-id="bf182-325">모듈이 로그 파일을 만들려면 `stdoutLogFile` 경로의 모든 폴더가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-325">Any folders in the `stdoutLogFile` path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="bf182-326">앱 풀에는 로그가 기록될 위치에 쓰기 권한이 있어야 합니다(`IIS AppPool\<app_pool_name>`을 사용하여 쓰기 권한 제공).</span><span class="sxs-lookup"><span data-stu-id="bf182-326">The app pool must have write access to the location where the logs are written (use `IIS AppPool\<app_pool_name>` to provide write permission).</span></span>

<span data-ttu-id="bf182-327">프로세스 재생/다시 시작이 발생하지 않는 한 로그는 회전되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-327">Logs aren't rotated, unless process recycling/restart occurs.</span></span> <span data-ttu-id="bf182-328">로그에서 사용하는 디스크 공간을 제한하는 것은 호스터의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-328">It's the responsibility of the hoster to limit the disk space the logs consume.</span></span>

<span data-ttu-id="bf182-329">stdout 로그는 앱 시작 문제를 해결하는 경우에만 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-329">Using the stdout log is only recommended for troubleshooting app startup issues.</span></span> <span data-ttu-id="bf182-330">일반 앱 로깅을 위해 stdout 로그를 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="bf182-330">Don't use the stdout log for general app logging purposes.</span></span> <span data-ttu-id="bf182-331">ASP.NET Core 앱의 루틴 로깅에는 로그 파일 크기를 제한하고 로그를 회전하는 로깅 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-331">For routine logging in an ASP.NET Core app, use a logging library that limits log file size and rotates logs.</span></span> <span data-ttu-id="bf182-332">자세한 내용은 [타사 로깅 공급자](xref:fundamentals/logging/index#third-party-logging-providers)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf182-332">For more information, see [third-party logging providers](xref:fundamentals/logging/index#third-party-logging-providers).</span></span>

<span data-ttu-id="bf182-333">로그 파일이 만들어질 때 타임스탬프 및 파일 확장명이 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-333">A timestamp and file extension are added automatically when the log file is created.</span></span> <span data-ttu-id="bf182-334">로그 파일 이름은 타임스탬프, 프로세스 ID 및 파일 확장명(*.log*)을 밑줄로 구분된 `stdoutLogFile` 경로의 마지막 세그먼트(일반적으로 *stdout*)에 추가하여 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-334">The log file name is composed by appending the timestamp, process ID, and file extension (*.log*) to the last segment of the `stdoutLogFile` path (typically *stdout*) delimited by underscores.</span></span> <span data-ttu-id="bf182-335">`stdoutLogFile` 경로가 *stdout*으로 끝나는 경우 2018년 2월 5일 19시 42분 32초에 만들어진 PID 1934를 사용하는 앱에 대한 로그의 파일 이름은 *stdout_20180205194132_1934.log*입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-335">If the `stdoutLogFile` path ends with *stdout*, a log for an app with a PID of 1934 created on 2/5/2018 at 19:42:32 has the file name *stdout_20180205194132_1934.log*.</span></span>

<span data-ttu-id="bf182-336">다음 샘플 `aspNetCore` 요소는 Azure App Service에서 호스트되는 앱에 대한 stdout 로깅을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-336">The following sample `aspNetCore` element configures stdout logging for an app hosted in Azure App Service.</span></span> <span data-ttu-id="bf182-337">로컬 로깅에는 로컬 경로 또는 네트워크 공유 경로가 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-337">A local path or network share path is acceptable for local logging.</span></span> <span data-ttu-id="bf182-338">AppPool 사용자 ID에 제공된 경로에 쓸 수 있는 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-338">Confirm that the AppPool user identity has permission to write to the path provided.</span></span>

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

<span data-ttu-id="bf182-339">*web.config* 파일에 있는 `aspNetCore` 요소의 예제에 대해서는 [web.config를 사용한 구성](#configuration-with-webconfig)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf182-339">See [Configuration with web.config](#configuration-with-webconfig) for an example of the `aspNetCore` element in the *web.config* file.</span></span>

## <a name="proxy-configuration-uses-http-protocol-and-a-pairing-token"></a><span data-ttu-id="bf182-340">프록시 구성은 HTTP 프로토콜 및 페어링 토큰을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-340">Proxy configuration uses HTTP protocol and a pairing token</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="bf182-341">*호스팅에만 적용됩니다.*</span><span class="sxs-lookup"><span data-stu-id="bf182-341">*Only applies to out-of-process hosting.*</span></span>

::: moniker-end

<span data-ttu-id="bf182-342">ASP.NET Core 모듈과 Kestrel 사이에 만들어진 프록시는 HTTP 프로토콜을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-342">The proxy created between the ASP.NET Core Module and Kestrel uses the HTTP protocol.</span></span> <span data-ttu-id="bf182-343">HTTP 사용은 모듈과 Kestrel 간의 트래픽이 네트워크 인터페이스에서 분리된 루프백 주소에서 발생하는 성능 최적화입니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-343">Using HTTP is a performance optimization, where the traffic between the module and Kestrel takes place on a loopback address off of the network interface.</span></span> <span data-ttu-id="bf182-344">서버에서 분리된 위치에서 모듈과 Kestrel 간 트래픽 도청의 위험은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-344">There's no risk of eavesdropping the traffic between the module and Kestrel from a location off of the server.</span></span>

<span data-ttu-id="bf182-345">페어링 토큰은 Kestrel에서 받은 요청이 IIS에서 프록시되었으며 다른 원본에서 오지 않았다는 것을 보장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-345">A pairing token is used to guarantee that the requests received by Kestrel were proxied by IIS and didn't come from some other source.</span></span> <span data-ttu-id="bf182-346">페어링 토큰은 모듈에 의해 생성되며 환경 변수(`ASPNETCORE_TOKEN`)로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-346">The pairing token is created and set into an environment variable (`ASPNETCORE_TOKEN`) by the module.</span></span> <span data-ttu-id="bf182-347">페어링 토큰은 프록시된 모든 요청에서 헤더(`MSAspNetCoreToken`)로도 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-347">The pairing token is also set into a header (`MSAspNetCoreToken`) on every proxied request.</span></span> <span data-ttu-id="bf182-348">IIS 미들웨어는 수신하는 각 요청을 검사하여 페어링 토큰 헤더 값이 환경 변수 값과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-348">IIS Middleware checks each request it receives to confirm that the pairing token header value matches the environment variable value.</span></span> <span data-ttu-id="bf182-349">토큰 값이 일치하지 않는 경우 요청이 기록되고 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-349">If the token values are mismatched, the request is logged and rejected.</span></span> <span data-ttu-id="bf182-350">페어링 토큰 환경 변수와 모듈과 Kestrel 간의 트래픽은 서버에서 분리된 위치에서 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-350">The pairing token environment variable and the traffic between the module and Kestrel aren't accessible from a location off of the server.</span></span> <span data-ttu-id="bf182-351">페어링 토큰 값을 알지 못하면 공격자는 IIS 미들웨어에서 검사를 무시하는 요청을 전송할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-351">Without knowing the pairing token value, an attacker can't submit requests that bypass the check in the IIS Middleware.</span></span>

## <a name="aspnet-core-module-with-an-iis-shared-configuration"></a><span data-ttu-id="bf182-352">IIS 공유 구성이 포함된 ASP.NET Core 모듈</span><span class="sxs-lookup"><span data-stu-id="bf182-352">ASP.NET Core Module with an IIS Shared Configuration</span></span>

<span data-ttu-id="bf182-353">ASP.NET Core 모듈 설치 관리자는 **SYSTEM** 계정의 권한으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-353">The ASP.NET Core Module installer runs with the privileges of the **SYSTEM** account.</span></span> <span data-ttu-id="bf182-354">로컬 시스템 계정에는 IIS 공유 구성에서 사용하는 공유 경로에 대한 수정 권한이 없으므로 공유의 *applicationHost.config*에서 모듈 설정을 구성하려고 하면 설치 관리자에서 액세스 거부 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-354">Because the local system account doesn't have modify permission for the share path used by the IIS Shared Configuration, the installer hits an access denied error when attempting to configure the module settings in *applicationHost.config* on the share.</span></span> <span data-ttu-id="bf182-355">IIS 공유 구성을 사용할 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-355">When using an IIS Shared Configuration, follow these steps:</span></span>

1. <span data-ttu-id="bf182-356">IIS 공유 구성을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-356">Disable the IIS Shared Configuration.</span></span>
1. <span data-ttu-id="bf182-357">설치 관리자를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-357">Run the installer.</span></span>
1. <span data-ttu-id="bf182-358">업데이트된 *applicationHost.config* 파일을 공유로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-358">Export the updated *applicationHost.config* file to the share.</span></span>
1. <span data-ttu-id="bf182-359">IIS 공유 구성을 다시 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-359">Re-enable the IIS Shared Configuration.</span></span>

## <a name="module-version-and-hosting-bundle-installer-logs"></a><span data-ttu-id="bf182-360">모듈 버전 및 호스팅 번들 설치 관리자 로그</span><span class="sxs-lookup"><span data-stu-id="bf182-360">Module version and Hosting Bundle installer logs</span></span>

<span data-ttu-id="bf182-361">설치된 ASP.NET Core 모듈의 버전을 확인하려면:</span><span class="sxs-lookup"><span data-stu-id="bf182-361">To determine the version of the installed ASP.NET Core Module:</span></span>

1. <span data-ttu-id="bf182-362">호스팅 시스템에서 *%windir%\System32\inetsrv*로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-362">On the hosting system, navigate to *%windir%\System32\inetsrv*.</span></span>
1. <span data-ttu-id="bf182-363">*aspnetcore.dll* 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-363">Locate the *aspnetcore.dll* file.</span></span>
1. <span data-ttu-id="bf182-364">파일을 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-364">Right-click the file and select **Properties** from the contextual menu.</span></span>
1. <span data-ttu-id="bf182-365">**세부 정보** 탭을 선택합니다. **파일 버전** 및 **제품 버전**은 설치된 모듈 버전을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-365">Select the **Details** tab. The **File version** and **Product version** represent the installed version of the module.</span></span>

<span data-ttu-id="bf182-366">모듈에 대한 호스팅 번들 설치 관리자 로그는 *C:\\Users\\%UserName%\\AppData\\Local\\Temp*에 있습니다. 파일 이름은 *dd_DotNetCoreWinSvrHosting__\<timestamp>_000_AspNetCoreModule_x64.log*로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-366">The Hosting Bundle installer logs for the module are found at *C:\\Users\\%UserName%\\AppData\\Local\\Temp*. The file is named *dd_DotNetCoreWinSvrHosting__\<timestamp>_000_AspNetCoreModule_x64.log*.</span></span>

## <a name="module-schema-and-configuration-file-locations"></a><span data-ttu-id="bf182-367">모듈, 스키마 및 구성 파일 위치</span><span class="sxs-lookup"><span data-stu-id="bf182-367">Module, schema, and configuration file locations</span></span>

### <a name="module"></a><span data-ttu-id="bf182-368">Module</span><span class="sxs-lookup"><span data-stu-id="bf182-368">Module</span></span>

<span data-ttu-id="bf182-369">**IIS(x86/amd64):**</span><span class="sxs-lookup"><span data-stu-id="bf182-369">**IIS (x86/amd64):**</span></span>

   * <span data-ttu-id="bf182-370">%windir%\System32\inetsrv\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="bf182-370">%windir%\System32\inetsrv\aspnetcore.dll</span></span>

   * <span data-ttu-id="bf182-371">%windir%\SysWOW64\inetsrv\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="bf182-371">%windir%\SysWOW64\inetsrv\aspnetcore.dll</span></span>

<span data-ttu-id="bf182-372">**IIS Express(x86/amd64):**</span><span class="sxs-lookup"><span data-stu-id="bf182-372">**IIS Express (x86/amd64):**</span></span>

   * <span data-ttu-id="bf182-373">%ProgramFiles%\IIS Express\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="bf182-373">%ProgramFiles%\IIS Express\aspnetcore.dll</span></span>

   * <span data-ttu-id="bf182-374">%ProgramFiles(x86)%\IIS Express\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="bf182-374">%ProgramFiles(x86)%\IIS Express\aspnetcore.dll</span></span>

### <a name="schema"></a><span data-ttu-id="bf182-375">스키마</span><span class="sxs-lookup"><span data-stu-id="bf182-375">Schema</span></span>

<span data-ttu-id="bf182-376">**IIS**</span><span class="sxs-lookup"><span data-stu-id="bf182-376">**IIS**</span></span>

   * <span data-ttu-id="bf182-377">%windir%\System32\inetsrv\config\schema\aspnetcore_schema.xml</span><span class="sxs-lookup"><span data-stu-id="bf182-377">%windir%\System32\inetsrv\config\schema\aspnetcore_schema.xml</span></span>

<span data-ttu-id="bf182-378">**IIS Express**</span><span class="sxs-lookup"><span data-stu-id="bf182-378">**IIS Express**</span></span>

   * <span data-ttu-id="bf182-379">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema.xml</span><span class="sxs-lookup"><span data-stu-id="bf182-379">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema.xml</span></span>

### <a name="configuration"></a><span data-ttu-id="bf182-380">구성</span><span class="sxs-lookup"><span data-stu-id="bf182-380">Configuration</span></span>

<span data-ttu-id="bf182-381">**IIS**</span><span class="sxs-lookup"><span data-stu-id="bf182-381">**IIS**</span></span>

   * <span data-ttu-id="bf182-382">%windir%\System32\inetsrv\config\applicationHost.config</span><span class="sxs-lookup"><span data-stu-id="bf182-382">%windir%\System32\inetsrv\config\applicationHost.config</span></span>

<span data-ttu-id="bf182-383">**IIS Express**</span><span class="sxs-lookup"><span data-stu-id="bf182-383">**IIS Express**</span></span>

   * <span data-ttu-id="bf182-384">.vs\config\applicationHost.config</span><span class="sxs-lookup"><span data-stu-id="bf182-384">.vs\config\applicationHost.config</span></span>

<span data-ttu-id="bf182-385">*applicationHost.config* 파일에서 *aspnetcore.dll*을 검색하여 파일을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-385">The files can be found by searching for *aspnetcore.dll* in the *applicationHost.config* file.</span></span> <span data-ttu-id="bf182-386">IIS Express의 경우 기본적으로 *applicationHost.config* 파일이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-386">For IIS Express, the *applicationHost.config* file won't exist by default.</span></span> <span data-ttu-id="bf182-387">Visual Studio 솔루션에서 웹앱 프로젝트를 시작할 때 *\<application_root>\\.vs\\config*에 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="bf182-387">The file is created at *\<application_root>\\.vs\\config* when starting any web app project in the Visual Studio solution.</span></span>
