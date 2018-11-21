---
title: ASP.NET Core 모듈 구성 참조
author: guardrex
description: ASP.NET Core 앱을 호스팅하기 위해 ASP.NET Core 모듈을 구성하는 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 11/12/2018
uid: host-and-deploy/aspnet-core-module
ms.openlocfilehash: 32fbf2b19da2d088847279f447f9a72cedcf8085
ms.sourcegitcommit: 408921a932448f66cb46fd53c307a864f5323fe5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/12/2018
ms.locfileid: "51570180"
---
# <a name="aspnet-core-module-configuration-reference"></a><span data-ttu-id="66a79-103">ASP.NET Core 모듈 구성 참조</span><span class="sxs-lookup"><span data-stu-id="66a79-103">ASP.NET Core Module configuration reference</span></span>

<span data-ttu-id="66a79-104">작성자: [Luke Latham](https://github.com/guardrex), [Rick Anderson](https://twitter.com/RickAndMSFT), [Sourabh Shirhatti](https://twitter.com/sshirhatti) 및 [Justin Kotalik](https://github.com/jkotalik)</span><span class="sxs-lookup"><span data-stu-id="66a79-104">By [Luke Latham](https://github.com/guardrex), [Rick Anderson](https://twitter.com/RickAndMSFT), [Sourabh Shirhatti](https://twitter.com/sshirhatti), and [Justin Kotalik](https://github.com/jkotalik)</span></span>

<span data-ttu-id="66a79-105">이 문서에서는 ASP.NET Core 앱을 호스트하기 위해 ASP.NET Core 모듈을 구성하는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-105">This document provides instructions on how to configure the ASP.NET Core Module for hosting ASP.NET Core apps.</span></span> <span data-ttu-id="66a79-106">ASP.NET Core 모듈 및 설치 지침에 대한 개요는 [ASP.NET Core 모듈 개요](xref:fundamentals/servers/aspnet-core-module)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66a79-106">For an introduction to the ASP.NET Core Module and installation instructions, see the [ASP.NET Core Module overview](xref:fundamentals/servers/aspnet-core-module).</span></span>

::: moniker range=">= aspnetcore-2.2"

## <a name="hosting-model"></a><span data-ttu-id="66a79-107">호스팅 모델</span><span class="sxs-lookup"><span data-stu-id="66a79-107">Hosting model</span></span>

<span data-ttu-id="66a79-108">.NET Core 2.2 이상에서 실행되는 앱의 경우, 모듈에서는 역방향 프록시(Out-of-Process) 호스팅과 비교할 때 더 나은 성능을 제공하기 위해 In-Process 호스팅 모델을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-108">For apps running on .NET Core 2.2 or later, the module supports an in-process hosting model for improved performance compared to reverse-proxy (out-of-process) hosting.</span></span> <span data-ttu-id="66a79-109">자세한 내용은 <xref:fundamentals/servers/aspnet-core-module#aspnet-core-module-description>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66a79-109">For more information, see <xref:fundamentals/servers/aspnet-core-module#aspnet-core-module-description>.</span></span>

<span data-ttu-id="66a79-110">In-Process 호스팅은 기존 앱에 대한 옵트인(opt in) 기능이지만 [dotnet new](/dotnet/core/tools/dotnet-new) 템플릿은 기본적으로 모든 IIS 및 IIS Express 시나리오에 대해 In-Process 호스팅 모델로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-110">In-procsess hosting is opt-in for existing apps, but [dotnet new](/dotnet/core/tools/dotnet-new) templates default to the in-process hosting model for all IIS and IIS Express scenarios.</span></span>

<span data-ttu-id="66a79-111">In-Process 호스팅용 앱을 구성하려면 `inprocess`의 값을 사용하여 `<AspNetCoreHostingModel>` 속성을 앱의 프로젝트 파일(예: *MyApp.csproj*)에 추가합니다(Out-of-Process 호스팅은 `outofprocess`로 설정됨).</span><span class="sxs-lookup"><span data-stu-id="66a79-111">To configure an app for in-process hosting, add the `<AspNetCoreHostingModel>` property to the app's project file (for example, *MyApp.csproj*) with a value of `inprocess` (out-of-process hosting is set with `outofprocess`):</span></span>

```xml
<PropertyGroup>
  <AspNetCoreHostingModel>inprocess</AspNetCoreHostingModel>
</PropertyGroup>
```

<span data-ttu-id="66a79-112">다음 특성은 In-Process로 호스팅할 때 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-112">The following characteristics apply when hosting in-process:</span></span>

* <span data-ttu-id="66a79-113">[Kestrel 서버](xref:fundamentals/servers/kestrel)가 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-113">The [Kestrel server](xref:fundamentals/servers/kestrel) isn't used.</span></span> <span data-ttu-id="66a79-114">사용자 지정 <xref:Microsoft.AspNetCore.Hosting.Server.IServer> 구현인 `IISHttpServer`가 앱의 서버 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-114">A custom <xref:Microsoft.AspNetCore.Hosting.Server.IServer> implementation, `IISHttpServer` acts as the app's server.</span></span>

* <span data-ttu-id="66a79-115">[requestTimeout 특성](#attributes-of-the-aspnetcore-element)이 In-Process 호스팅에 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-115">The [requestTimeout attribute](#attributes-of-the-aspnetcore-element) doesn't apply to in-process hosting.</span></span>

* <span data-ttu-id="66a79-116">앱 간의 앱 풀 공유는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-116">Sharing an app pool among apps isn't supported.</span></span> <span data-ttu-id="66a79-117">앱당 하나의 앱 풀을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-117">Use one app pool per app.</span></span>

* <span data-ttu-id="66a79-118">[웹 배포](/iis/publish/using-web-deploy/introduction-to-web-deploy)를 사용하거나 [app_offline.htm 파일을 배포에](xref:host-and-deploy/iis/index#locked-deployment-files) 수동으로 배치할 경우 열린 연결이 있으면 앱이 즉시 종료되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-118">When using [Web Deploy](/iis/publish/using-web-deploy/introduction-to-web-deploy) or manually placing an [app_offline.htm file in the deployment](xref:host-and-deploy/iis/index#locked-deployment-files), the app might not shut down immediately if there's an open connection.</span></span> <span data-ttu-id="66a79-119">예를 들어, WebSocket 연결은 앱 종료를 지연시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-119">For example, a websocket connection may delay app shut down.</span></span>

* <span data-ttu-id="66a79-120">앱 및 설치된 런타임(x64 또는 x86)의 아키텍처(비트)는 앱 풀의 아키텍처와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-120">The architecture (bitness) of the app and installed runtime (x64 or x86) must match the architecture of the app pool.</span></span>

* <span data-ttu-id="66a79-121">`WebHostBuilder`([CreateDefaultBuilder](xref:fundamentals/host/web-host#set-up-a-host)를 사용하지 않고)를 사용하여 앱 호스트를 수동으로 설정하며 앱이 Kestrel 서버에서 직접 실행되는 경우(자체 호스트됨) `UseIISIntegration`를 호출하기 전에 `UseKestrel`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-121">If setting up the app's host manually with `WebHostBuilder` (not using [CreateDefaultBuilder](xref:fundamentals/host/web-host#set-up-a-host)) and the app is ever run directly on the Kestrel server (self-hosted), call `UseKestrel` before calling `UseIISIntegration`.</span></span> <span data-ttu-id="66a79-122">이 순서가 바뀌면 호스트가 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-122">If the order is reversed, the host fails to start.</span></span>

* <span data-ttu-id="66a79-123">클라이언트의 연결 끊김이 검색되었습니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-123">Client disconnects are detected.</span></span> <span data-ttu-id="66a79-124">클라이언트의 연결이 끊어지면 [HttpContext.RequestAborted](xref:Microsoft.AspNetCore.Http.HttpContext.RequestAborted*) 취소 토큰이 취소됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-124">The [HttpContext.RequestAborted](xref:Microsoft.AspNetCore.Http.HttpContext.RequestAborted*) cancellation token is cancelled when the client disconnects.</span></span>

* <span data-ttu-id="66a79-125">`Directory.GetCurrentDirectory()`는 애플리케이션 디렉터리가 아닌 IIS에 의해 시작된 프로세스의 작업자 디렉터리를 반환합니다(예: *w3wp.exe*에 대한 *C:\Windows\System32\inetsrv*).</span><span class="sxs-lookup"><span data-stu-id="66a79-125">`Directory.GetCurrentDirectory()` returns the worker directory of the process started by IIS rather than the application directory (for example, *C:\Windows\System32\inetsrv* for *w3wp.exe*).</span></span>

### <a name="hosting-model-changes"></a><span data-ttu-id="66a79-126">호스팅 모델 변경</span><span class="sxs-lookup"><span data-stu-id="66a79-126">Hosting model changes</span></span>

<span data-ttu-id="66a79-127">`hostingModel` 설정이 *web.config* 파일에서 변경되면([web.config로 구성](#configuration-with-webconfig) 섹션에 설명되어 있음) 모듈은 IIS에 대한 작업자 프로세스를 재순환합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-127">If the `hostingModel` setting is changed in the *web.config* file (explained in the [Configuration with web.config](#configuration-with-webconfig) section), the module recycles the worker process for IIS.</span></span>

<span data-ttu-id="66a79-128">IIS Express의 경우 모듈은 작업자 프로세스를 재순환하지 않고, 대신 현재 IIS Express 프로세스의 정상 종료를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-128">For IIS Express, the module doesn't recycle the worker process but instead triggers a graceful shutdown of the current IIS Express process.</span></span> <span data-ttu-id="66a79-129">앱에 대한 다음 요청은 새 IIS Express 프로세스를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-129">The next request to the app spawns a new IIS Express process.</span></span>

### <a name="process-name"></a><span data-ttu-id="66a79-130">프로세스 이름</span><span class="sxs-lookup"><span data-stu-id="66a79-130">Process name</span></span>

<span data-ttu-id="66a79-131">`Process.GetCurrentProcess().ProcessName`은 `w3wp`/`iisexpress`(In-Process) 또는 `dotnet`(Out-of-Process)을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-131">`Process.GetCurrentProcess().ProcessName` reports `w3wp`/`iisexpress` (in-process) or `dotnet` (out-of-process).</span></span>

::: moniker-end

## <a name="configuration-with-webconfig"></a><span data-ttu-id="66a79-132">web.config를 사용한 구성</span><span class="sxs-lookup"><span data-stu-id="66a79-132">Configuration with web.config</span></span>

<span data-ttu-id="66a79-133">ASP.NET Core 모듈은 사이트의 *web.config* 파일에 있는 `system.webServer` 노드의 `aspNetCore` 섹션으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-133">The ASP.NET Core Module is configured with the `aspNetCore` section of the `system.webServer` node in the site's *web.config* file.</span></span>

<span data-ttu-id="66a79-134">다음 *web.config* 파일은 [프레임워크 종속 배포](/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd)를 위해 게시되고 사이트 요청을 처리하도록 ASP.NET Core 모듈을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-134">The following *web.config* file is published for a [framework-dependent deployment](/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd) and configures the ASP.NET Core Module to handle site requests:</span></span>

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

<span data-ttu-id="66a79-135">다음 *web.config*는 [자체 포함 배포](/dotnet/articles/core/deploying/#self-contained-deployments-scd)를 위해 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-135">The following *web.config* is published for a [self-contained deployment](/dotnet/articles/core/deploying/#self-contained-deployments-scd):</span></span>

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

<span data-ttu-id="66a79-136"><xref:System.Configuration.SectionInformation.InheritInChildApplications*> 속성이 `false`로 설정되어 [\<location>](/iis/manage/managing-your-configuration-settings/understanding-iis-configuration-delegation#the-concept-of-location) 요소 내에서 지정된 설정이 하위 디렉터리에 있는 앱에 상속되지 않음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-136">The <xref:System.Configuration.SectionInformation.InheritInChildApplications*> property is set to `false` to indicate that the settings specified within the [\<location>](/iis/manage/managing-your-configuration-settings/understanding-iis-configuration-delegation#the-concept-of-location) element aren't inherited by apps that reside in a subdirectory of the app.</span></span>

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

<span data-ttu-id="66a79-137">앱이 [Azure App Service](https://azure.microsoft.com/services/app-service/)에 배포되면 `stdoutLogFile` 경로가 `\\?\%home%\LogFiles\stdout`로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-137">When an app is deployed to [Azure App Service](https://azure.microsoft.com/services/app-service/), the `stdoutLogFile` path is set to `\\?\%home%\LogFiles\stdout`.</span></span> <span data-ttu-id="66a79-138">이 경로는 서비스에서 자동으로 만들어진 위치인 *LogFiles* 폴더에 stdout 로그를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-138">The path saves stdout logs to the *LogFiles* folder, which is a location automatically created by the service.</span></span>

<span data-ttu-id="66a79-139">하위 앱에서 *web.config* 파일의 구성에 관한 중요 참고 사항은 [하위 응용 프로그램 구성](xref:host-and-deploy/iis/index#sub-application-configuration)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66a79-139">See [Sub-application configuration](xref:host-and-deploy/iis/index#sub-application-configuration) for an important note pertaining to the configuration of *web.config* files in sub-apps.</span></span>

### <a name="attributes-of-the-aspnetcore-element"></a><span data-ttu-id="66a79-140">aspNetCore 요소의 특성</span><span class="sxs-lookup"><span data-stu-id="66a79-140">Attributes of the aspNetCore element</span></span>

::: moniker range=">= aspnetcore-2.2"

| <span data-ttu-id="66a79-141">특성</span><span class="sxs-lookup"><span data-stu-id="66a79-141">Attribute</span></span> | <span data-ttu-id="66a79-142">설명</span><span class="sxs-lookup"><span data-stu-id="66a79-142">Description</span></span> | <span data-ttu-id="66a79-143">기본</span><span class="sxs-lookup"><span data-stu-id="66a79-143">Default</span></span> |
| --------- | ----------- | :-----: |
| `arguments` | <p><span data-ttu-id="66a79-144">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-144">Optional string attribute.</span></span></p><p><span data-ttu-id="66a79-145">**processPath**에 지정된 실행 파일에 대한 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-145">Arguments to the executable specified in **processPath**.</span></span></p> | |
| `disableStartUpErrorPage` | <p><span data-ttu-id="66a79-146">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-146">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="66a79-147">true인 경우 **502.5 - 프로세스 실패** 페이지가 표시되지 않고 *web.config*에 구성된 502 상태 코드 페이지가 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-147">If true, the **502.5 - Process Failure** page is suppressed, and the 502 status code page configured in the *web.config* takes precedence.</span></span></p> | `false` |
| `forwardWindowsAuthToken` | <p><span data-ttu-id="66a79-148">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-148">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="66a79-149">true인 경우 토큰은 %ASPNETCORE_PORT%에서 수신 대기하는 자식 프로세스에 요청별 헤더 'MS-ASPNETCORE-WINAUTHTOKEN'으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-149">If true, the token is forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="66a79-150">이 프로세스는 요청별로 이 토큰에서 CloseHandle을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-150">It's the responsibility of that process to call CloseHandle on this token per request.</span></span></p> | `true` |
| `hostingModel` | <p><span data-ttu-id="66a79-151">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-151">Optional string attribute.</span></span></p><p><span data-ttu-id="66a79-152">호스팅 모델을 In-Process(`inprocess`) 또는 Out-of-Process(`outofprocess`)로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-152">Specifies the hosting model as in-process (`inprocess`) or out-of-process (`outofprocess`).</span></span></p> | `outofprocess` |
| `processesPerApplication` | <p><span data-ttu-id="66a79-153">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-153">Optional integer attribute.</span></span></p><p><span data-ttu-id="66a79-154">앱별로 스핀 업할 수 있는 **processPath** 설정에 지정된 프로세스의 인스턴스 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-154">Specifies the number of instances of the process specified in the **processPath** setting that can be spun up per app.</span></span></p><p><span data-ttu-id="66a79-155">&dagger;In-Process 호스팅의 경우 이 값은 `1`로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-155">&dagger;For in-process hosting, the value is limited to `1`.</span></span></p> | <span data-ttu-id="66a79-156">기본값: `1`</span><span class="sxs-lookup"><span data-stu-id="66a79-156">Default: `1`</span></span><br><span data-ttu-id="66a79-157">최소: `1`</span><span class="sxs-lookup"><span data-stu-id="66a79-157">Min: `1`</span></span><br><span data-ttu-id="66a79-158">최대: `100`&dagger;</span><span class="sxs-lookup"><span data-stu-id="66a79-158">Max: `100`&dagger;</span></span> |
| `processPath` | <p><span data-ttu-id="66a79-159">필수 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-159">Required string attribute.</span></span></p><p><span data-ttu-id="66a79-160">HTTP 요청을 수신 대기하는 프로세스를 시작하는 실행 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-160">Path to the executable that launches a process listening for HTTP requests.</span></span> <span data-ttu-id="66a79-161">상대 경로가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-161">Relative paths are supported.</span></span> <span data-ttu-id="66a79-162">경로가 `.`로 시작되면 경로는 사이트 루트의 상대 경로로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-162">If the path begins with `.`, the path is considered to be relative to the site root.</span></span></p> | |
| `rapidFailsPerMinute` | <p><span data-ttu-id="66a79-163">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-163">Optional integer attribute.</span></span></p><p><span data-ttu-id="66a79-164">**processPath**에 지정된 프로세스의 분당 크래시 허용 횟수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-164">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="66a79-165">이 제한을 초과하면 모듈은 남은 시간 동안 프로세스 시작을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-165">If this limit is exceeded, the module stops launching the process for the remainder of the minute.</span></span></p><p><span data-ttu-id="66a79-166">In-Process 호스팅에서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-166">Not supported with in-process hosting.</span></span></p> | <span data-ttu-id="66a79-167">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="66a79-167">Default: `10`</span></span><br><span data-ttu-id="66a79-168">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="66a79-168">Min: `0`</span></span><br><span data-ttu-id="66a79-169">최대: `100`</span><span class="sxs-lookup"><span data-stu-id="66a79-169">Max: `100`</span></span> |
| `requestTimeout` | <p><span data-ttu-id="66a79-170">선택적 시간 간격 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-170">Optional timespan attribute.</span></span></p><p><span data-ttu-id="66a79-171">ASP.NET Core 모듈이 %ASPNETCORE_PORT%에서 수신 대기하는 프로세스의 응답을 기다리는 기간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-171">Specifies the duration for which the ASP.NET Core Module waits for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="66a79-172">ASP.NET Core 2.1 이상 릴리스와 함께 제공되는 ASP.NET Core 모듈 버전에서는 `requestTimeout`이 전체 시간, 분, 초로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-172">In versions of the ASP.NET Core Module that shipped with the release of ASP.NET Core 2.1 or later, the `requestTimeout` is specified in hours, minutes, and seconds.</span></span></p><p><span data-ttu-id="66a79-173">In-Process 호스팅에는 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-173">Doesn't apply to in-process hosting.</span></span> <span data-ttu-id="66a79-174">In-Process 호스팅의 경우 모듈은 앱이 요청을 처리할 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-174">For in-process hosting, the module waits for the app to process the request.</span></span></p> | <span data-ttu-id="66a79-175">기본값: `00:02:00`</span><span class="sxs-lookup"><span data-stu-id="66a79-175">Default: `00:02:00`</span></span><br><span data-ttu-id="66a79-176">최소: `00:00:00`</span><span class="sxs-lookup"><span data-stu-id="66a79-176">Min: `00:00:00`</span></span><br><span data-ttu-id="66a79-177">최대: `360:00:00`</span><span class="sxs-lookup"><span data-stu-id="66a79-177">Max: `360:00:00`</span></span> |
| `shutdownTimeLimit` | <p><span data-ttu-id="66a79-178">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-178">Optional integer attribute.</span></span></p><p><span data-ttu-id="66a79-179">*app_offline.htm* 파일이 검색될 때 실행 파일이 정상적으로 종료될 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-179">Duration in seconds that the module waits for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p> | <span data-ttu-id="66a79-180">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="66a79-180">Default: `10`</span></span><br><span data-ttu-id="66a79-181">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="66a79-181">Min: `0`</span></span><br><span data-ttu-id="66a79-182">최대: `600`</span><span class="sxs-lookup"><span data-stu-id="66a79-182">Max: `600`</span></span> |
| `startupTimeLimit` | <p><span data-ttu-id="66a79-183">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-183">Optional integer attribute.</span></span></p><p><span data-ttu-id="66a79-184">실행 파일이 포트에서 수신 대기하는 프로세스를 시작할 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-184">Duration in seconds that the module waits for the executable to start a process listening on the port.</span></span> <span data-ttu-id="66a79-185">이 시간 제한을 초과하면 모듈이 프로세스를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-185">If this time limit is exceeded, the module kills the process.</span></span> <span data-ttu-id="66a79-186">모듈은 새 요청을 수신할 때 프로세스를 다시 시작하려고 하고, 마지막 롤링 기간(분)에 앱이 **rapidFailsPerMinute**번 시작에 실패한 경우가 아니면 이후 요청이 들어올 때 프로세스를 계속 다시 시작하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-186">The module attempts to relaunch the process when it receives a new request and continues to attempt to restart the process on subsequent incoming requests unless the app fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p><p><span data-ttu-id="66a79-187">값 0은 무한 시간 제한으로 간주되지 **않습니다**.</span><span class="sxs-lookup"><span data-stu-id="66a79-187">A value of 0 (zero) is **not** considered an infinite timeout.</span></span></p> | <span data-ttu-id="66a79-188">기본값: `120`</span><span class="sxs-lookup"><span data-stu-id="66a79-188">Default: `120`</span></span><br><span data-ttu-id="66a79-189">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="66a79-189">Min: `0`</span></span><br><span data-ttu-id="66a79-190">최대: `3600`</span><span class="sxs-lookup"><span data-stu-id="66a79-190">Max: `3600`</span></span> |
| `stdoutLogEnabled` | <p><span data-ttu-id="66a79-191">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-191">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="66a79-192">true인 경우 **processPath**에 지정된 프로세스에 대한 **stdout** 및 **stderr**이 **stdoutLogFile**에 지정된 파일로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-192">If true, **stdout** and **stderr** for the process specified in **processPath** are redirected to the file specified in **stdoutLogFile**.</span></span></p> | `false` |
| `stdoutLogFile` | <p><span data-ttu-id="66a79-193">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-193">Optional string attribute.</span></span></p><p><span data-ttu-id="66a79-194">**processPath**에 지정된 프로세스에서 **stdout** 및 **stderr**이 기록되는 상대 또는 절대 파일 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-194">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** are logged.</span></span> <span data-ttu-id="66a79-195">상대 경로는 사이트 루트에 상대적인 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-195">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="66a79-196">`.`로 시작하는 모든 경로는 사이트 루트에 상대적인 경로이고 다른 모든 경로는 절대 경로로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-196">Any path starting with `.` are relative to the site root and all other paths are treated as absolute paths.</span></span> <span data-ttu-id="66a79-197">모듈이 로그 파일을 만들려면 경로에 제공된 모든 폴더가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-197">Any folders provided in the path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="66a79-198">타임스탬프, 프로세스 ID 및 파일 확장명(*.log*)은 밑줄 구분 기호를 사용하여 **stdoutLogFile** 경로의 마지막 세그먼트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-198">Using underscore delimiters, a timestamp, process ID, and file extension (*.log*) are added to the last segment of the **stdoutLogFile** path.</span></span> <span data-ttu-id="66a79-199">`.\logs\stdout`이 값으로 제공되는 경우 예제 stdout 로그는 2018년 2월 5일 19시 41분 32초에 프로세스 ID 1934를 사용하여 저장될 경우 *logs* 폴더에 *stdout_20180205194132_1934.log*로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-199">If `.\logs\stdout` is supplied as a value, an example stdout log is saved as *stdout_20180205194132_1934.log* in the *logs* folder when saved on 2/5/2018 at 19:41:32 with a process ID of 1934.</span></span></p> | `aspnetcore-stdout` |

::: moniker-end

::: moniker range="= aspnetcore-2.1"

| <span data-ttu-id="66a79-200">특성</span><span class="sxs-lookup"><span data-stu-id="66a79-200">Attribute</span></span> | <span data-ttu-id="66a79-201">설명</span><span class="sxs-lookup"><span data-stu-id="66a79-201">Description</span></span> | <span data-ttu-id="66a79-202">기본</span><span class="sxs-lookup"><span data-stu-id="66a79-202">Default</span></span> |
| --------- | ----------- | :-----: |
| `arguments` | <p><span data-ttu-id="66a79-203">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-203">Optional string attribute.</span></span></p><p><span data-ttu-id="66a79-204">**processPath**에 지정된 실행 파일에 대한 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-204">Arguments to the executable specified in **processPath**.</span></span></p>| |
| `disableStartUpErrorPage` | <p><span data-ttu-id="66a79-205">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-205">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="66a79-206">true인 경우 **502.5 - 프로세스 실패** 페이지가 표시되지 않고 *web.config*에 구성된 502 상태 코드 페이지가 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-206">If true, the **502.5 - Process Failure** page is suppressed, and the 502 status code page configured in the *web.config* takes precedence.</span></span></p> | `false` |
| `forwardWindowsAuthToken` | <p><span data-ttu-id="66a79-207">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-207">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="66a79-208">true인 경우 토큰은 %ASPNETCORE_PORT%에서 수신 대기하는 자식 프로세스에 요청별 헤더 'MS-ASPNETCORE-WINAUTHTOKEN'으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-208">If true, the token is forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="66a79-209">이 프로세스는 요청별로 이 토큰에서 CloseHandle을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-209">It's the responsibility of that process to call CloseHandle on this token per request.</span></span></p> | `true` |
| `processesPerApplication` | <p><span data-ttu-id="66a79-210">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-210">Optional integer attribute.</span></span></p><p><span data-ttu-id="66a79-211">앱별로 스핀 업할 수 있는 **processPath** 설정에 지정된 프로세스의 인스턴스 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-211">Specifies the number of instances of the process specified in the **processPath** setting that can be spun up per app.</span></span></p> | <span data-ttu-id="66a79-212">기본값: `1`</span><span class="sxs-lookup"><span data-stu-id="66a79-212">Default: `1`</span></span><br><span data-ttu-id="66a79-213">최소: `1`</span><span class="sxs-lookup"><span data-stu-id="66a79-213">Min: `1`</span></span><br><span data-ttu-id="66a79-214">최대: `100`</span><span class="sxs-lookup"><span data-stu-id="66a79-214">Max: `100`</span></span> |
| `processPath` | <p><span data-ttu-id="66a79-215">필수 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-215">Required string attribute.</span></span></p><p><span data-ttu-id="66a79-216">HTTP 요청을 수신 대기하는 프로세스를 시작하는 실행 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-216">Path to the executable that launches a process listening for HTTP requests.</span></span> <span data-ttu-id="66a79-217">상대 경로가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-217">Relative paths are supported.</span></span> <span data-ttu-id="66a79-218">경로가 `.`로 시작되면 경로는 사이트 루트의 상대 경로로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-218">If the path begins with `.`, the path is considered to be relative to the site root.</span></span></p> | |
| `rapidFailsPerMinute` | <p><span data-ttu-id="66a79-219">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-219">Optional integer attribute.</span></span></p><p><span data-ttu-id="66a79-220">**processPath**에 지정된 프로세스의 분당 크래시 허용 횟수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-220">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="66a79-221">이 제한을 초과하면 모듈은 남은 시간 동안 프로세스 시작을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-221">If this limit is exceeded, the module stops launching the process for the remainder of the minute.</span></span></p> | <span data-ttu-id="66a79-222">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="66a79-222">Default: `10`</span></span><br><span data-ttu-id="66a79-223">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="66a79-223">Min: `0`</span></span><br><span data-ttu-id="66a79-224">최대: `100`</span><span class="sxs-lookup"><span data-stu-id="66a79-224">Max: `100`</span></span> |
| `requestTimeout` | <p><span data-ttu-id="66a79-225">선택적 시간 간격 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-225">Optional timespan attribute.</span></span></p><p><span data-ttu-id="66a79-226">ASP.NET Core 모듈이 %ASPNETCORE_PORT%에서 수신 대기하는 프로세스의 응답을 기다리는 기간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-226">Specifies the duration for which the ASP.NET Core Module waits for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="66a79-227">ASP.NET Core 2.1 이상 릴리스와 함께 제공되는 ASP.NET Core 모듈 버전에서는 `requestTimeout`이 전체 시간, 분, 초로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-227">In versions of the ASP.NET Core Module that shipped with the release of ASP.NET Core 2.1 or later, the `requestTimeout` is specified in hours, minutes, and seconds.</span></span></p> | <span data-ttu-id="66a79-228">기본값: `00:02:00`</span><span class="sxs-lookup"><span data-stu-id="66a79-228">Default: `00:02:00`</span></span><br><span data-ttu-id="66a79-229">최소: `00:00:00`</span><span class="sxs-lookup"><span data-stu-id="66a79-229">Min: `00:00:00`</span></span><br><span data-ttu-id="66a79-230">최대: `360:00:00`</span><span class="sxs-lookup"><span data-stu-id="66a79-230">Max: `360:00:00`</span></span> |
| `shutdownTimeLimit` | <p><span data-ttu-id="66a79-231">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-231">Optional integer attribute.</span></span></p><p><span data-ttu-id="66a79-232">*app_offline.htm* 파일이 검색될 때 실행 파일이 정상적으로 종료될 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-232">Duration in seconds that the module waits for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p> | <span data-ttu-id="66a79-233">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="66a79-233">Default: `10`</span></span><br><span data-ttu-id="66a79-234">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="66a79-234">Min: `0`</span></span><br><span data-ttu-id="66a79-235">최대: `600`</span><span class="sxs-lookup"><span data-stu-id="66a79-235">Max: `600`</span></span> |
| `startupTimeLimit` | <p><span data-ttu-id="66a79-236">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-236">Optional integer attribute.</span></span></p><p><span data-ttu-id="66a79-237">실행 파일이 포트에서 수신 대기하는 프로세스를 시작할 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-237">Duration in seconds that the module waits for the executable to start a process listening on the port.</span></span> <span data-ttu-id="66a79-238">이 시간 제한을 초과하면 모듈이 프로세스를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-238">If this time limit is exceeded, the module kills the process.</span></span> <span data-ttu-id="66a79-239">모듈은 새 요청을 수신할 때 프로세스를 다시 시작하려고 하고, 마지막 롤링 기간(분)에 앱이 **rapidFailsPerMinute**번 시작에 실패한 경우가 아니면 이후 요청이 들어올 때 프로세스를 계속 다시 시작하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-239">The module attempts to relaunch the process when it receives a new request and continues to attempt to restart the process on subsequent incoming requests unless the app fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p><p><span data-ttu-id="66a79-240">값 0은 무한 시간 제한으로 간주되지 **않습니다**.</span><span class="sxs-lookup"><span data-stu-id="66a79-240">A value of 0 (zero) is **not** considered an infinite timeout.</span></span></p> | <span data-ttu-id="66a79-241">기본값: `120`</span><span class="sxs-lookup"><span data-stu-id="66a79-241">Default: `120`</span></span><br><span data-ttu-id="66a79-242">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="66a79-242">Min: `0`</span></span><br><span data-ttu-id="66a79-243">최대: `3600`</span><span class="sxs-lookup"><span data-stu-id="66a79-243">Max: `3600`</span></span> |
| `stdoutLogEnabled` | <p><span data-ttu-id="66a79-244">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-244">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="66a79-245">true인 경우 **processPath**에 지정된 프로세스에 대한 **stdout** 및 **stderr**이 **stdoutLogFile**에 지정된 파일로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-245">If true, **stdout** and **stderr** for the process specified in **processPath** are redirected to the file specified in **stdoutLogFile**.</span></span></p> | `false` |
| `stdoutLogFile` | <p><span data-ttu-id="66a79-246">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-246">Optional string attribute.</span></span></p><p><span data-ttu-id="66a79-247">**processPath**에 지정된 프로세스에서 **stdout** 및 **stderr**이 기록되는 상대 또는 절대 파일 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-247">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** are logged.</span></span> <span data-ttu-id="66a79-248">상대 경로는 사이트 루트에 상대적인 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-248">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="66a79-249">`.`로 시작하는 모든 경로는 사이트 루트에 상대적인 경로이고 다른 모든 경로는 절대 경로로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-249">Any path starting with `.` are relative to the site root and all other paths are treated as absolute paths.</span></span> <span data-ttu-id="66a79-250">모듈이 로그 파일을 만들려면 경로에 제공된 모든 폴더가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-250">Any folders provided in the path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="66a79-251">타임스탬프, 프로세스 ID 및 파일 확장명(*.log*)은 밑줄 구분 기호를 사용하여 **stdoutLogFile** 경로의 마지막 세그먼트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-251">Using underscore delimiters, a timestamp, process ID, and file extension (*.log*) are added to the last segment of the **stdoutLogFile** path.</span></span> <span data-ttu-id="66a79-252">`.\logs\stdout`이 값으로 제공되는 경우 예제 stdout 로그는 2018년 2월 5일 19시 41분 32초에 프로세스 ID 1934를 사용하여 저장될 경우 *logs* 폴더에 *stdout_20180205194132_1934.log*로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-252">If `.\logs\stdout` is supplied as a value, an example stdout log is saved as *stdout_20180205194132_1934.log* in the *logs* folder when saved on 2/5/2018 at 19:41:32 with a process ID of 1934.</span></span></p> | `aspnetcore-stdout` |

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

| <span data-ttu-id="66a79-253">특성</span><span class="sxs-lookup"><span data-stu-id="66a79-253">Attribute</span></span> | <span data-ttu-id="66a79-254">설명</span><span class="sxs-lookup"><span data-stu-id="66a79-254">Description</span></span> | <span data-ttu-id="66a79-255">기본</span><span class="sxs-lookup"><span data-stu-id="66a79-255">Default</span></span> |
| --------- | ----------- | :-----: |
| `arguments` | <p><span data-ttu-id="66a79-256">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-256">Optional string attribute.</span></span></p><p><span data-ttu-id="66a79-257">**processPath**에 지정된 실행 파일에 대한 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-257">Arguments to the executable specified in **processPath**.</span></span></p>| |
| `disableStartUpErrorPage` | <p><span data-ttu-id="66a79-258">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-258">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="66a79-259">true인 경우 **502.5 - 프로세스 실패** 페이지가 표시되지 않고 *web.config*에 구성된 502 상태 코드 페이지가 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-259">If true, the **502.5 - Process Failure** page is suppressed, and the 502 status code page configured in the *web.config* takes precedence.</span></span></p> | `false` |
| `forwardWindowsAuthToken` | <p><span data-ttu-id="66a79-260">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-260">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="66a79-261">true인 경우 토큰은 %ASPNETCORE_PORT%에서 수신 대기하는 자식 프로세스에 요청별 헤더 'MS-ASPNETCORE-WINAUTHTOKEN'으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-261">If true, the token is forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="66a79-262">이 프로세스는 요청별로 이 토큰에서 CloseHandle을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-262">It's the responsibility of that process to call CloseHandle on this token per request.</span></span></p> | `true` |
| `processesPerApplication` | <p><span data-ttu-id="66a79-263">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-263">Optional integer attribute.</span></span></p><p><span data-ttu-id="66a79-264">앱별로 스핀 업할 수 있는 **processPath** 설정에 지정된 프로세스의 인스턴스 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-264">Specifies the number of instances of the process specified in the **processPath** setting that can be spun up per app.</span></span></p> | <span data-ttu-id="66a79-265">기본값: `1`</span><span class="sxs-lookup"><span data-stu-id="66a79-265">Default: `1`</span></span><br><span data-ttu-id="66a79-266">최소: `1`</span><span class="sxs-lookup"><span data-stu-id="66a79-266">Min: `1`</span></span><br><span data-ttu-id="66a79-267">최대: `100`</span><span class="sxs-lookup"><span data-stu-id="66a79-267">Max: `100`</span></span> |
| `processPath` | <p><span data-ttu-id="66a79-268">필수 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-268">Required string attribute.</span></span></p><p><span data-ttu-id="66a79-269">HTTP 요청을 수신 대기하는 프로세스를 시작하는 실행 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-269">Path to the executable that launches a process listening for HTTP requests.</span></span> <span data-ttu-id="66a79-270">상대 경로가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-270">Relative paths are supported.</span></span> <span data-ttu-id="66a79-271">경로가 `.`로 시작되면 경로는 사이트 루트의 상대 경로로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-271">If the path begins with `.`, the path is considered to be relative to the site root.</span></span></p> | |
| `rapidFailsPerMinute` | <p><span data-ttu-id="66a79-272">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-272">Optional integer attribute.</span></span></p><p><span data-ttu-id="66a79-273">**processPath**에 지정된 프로세스의 분당 크래시 허용 횟수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-273">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="66a79-274">이 제한을 초과하면 모듈은 남은 시간 동안 프로세스 시작을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-274">If this limit is exceeded, the module stops launching the process for the remainder of the minute.</span></span></p> | <span data-ttu-id="66a79-275">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="66a79-275">Default: `10`</span></span><br><span data-ttu-id="66a79-276">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="66a79-276">Min: `0`</span></span><br><span data-ttu-id="66a79-277">최대: `100`</span><span class="sxs-lookup"><span data-stu-id="66a79-277">Max: `100`</span></span> |
| `requestTimeout` | <p><span data-ttu-id="66a79-278">선택적 시간 간격 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-278">Optional timespan attribute.</span></span></p><p><span data-ttu-id="66a79-279">ASP.NET Core 모듈이 %ASPNETCORE_PORT%에서 수신 대기하는 프로세스의 응답을 기다리는 기간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-279">Specifies the duration for which the ASP.NET Core Module waits for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="66a79-280">ASP.NET Core 2.0 이하 릴리스와 함께 제공되는 ASP.NET Core 모듈 버전에서는 `requestTimeout`을 전체 시간(분)으로만 지정해야 합니다. 그렇지 않으면 기본적으로 2분으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-280">In versions of the ASP.NET Core Module that shipped with the release of ASP.NET Core 2.0 or earlier, the `requestTimeout` must be specified in whole minutes only, otherwise it defaults to 2 minutes.</span></span></p> | <span data-ttu-id="66a79-281">기본값: `00:02:00`</span><span class="sxs-lookup"><span data-stu-id="66a79-281">Default: `00:02:00`</span></span><br><span data-ttu-id="66a79-282">최소: `00:00:00`</span><span class="sxs-lookup"><span data-stu-id="66a79-282">Min: `00:00:00`</span></span><br><span data-ttu-id="66a79-283">최대: `360:00:00`</span><span class="sxs-lookup"><span data-stu-id="66a79-283">Max: `360:00:00`</span></span> |
| `shutdownTimeLimit` | <p><span data-ttu-id="66a79-284">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-284">Optional integer attribute.</span></span></p><p><span data-ttu-id="66a79-285">*app_offline.htm* 파일이 검색될 때 실행 파일이 정상적으로 종료될 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-285">Duration in seconds that the module waits for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p> | <span data-ttu-id="66a79-286">기본값: `10`</span><span class="sxs-lookup"><span data-stu-id="66a79-286">Default: `10`</span></span><br><span data-ttu-id="66a79-287">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="66a79-287">Min: `0`</span></span><br><span data-ttu-id="66a79-288">최대: `600`</span><span class="sxs-lookup"><span data-stu-id="66a79-288">Max: `600`</span></span> |
| `startupTimeLimit` | <p><span data-ttu-id="66a79-289">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-289">Optional integer attribute.</span></span></p><p><span data-ttu-id="66a79-290">실행 파일이 포트에서 수신 대기하는 프로세스를 시작할 때까지 모듈이 기다리는 기간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-290">Duration in seconds that the module waits for the executable to start a process listening on the port.</span></span> <span data-ttu-id="66a79-291">이 시간 제한을 초과하면 모듈이 프로세스를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-291">If this time limit is exceeded, the module kills the process.</span></span> <span data-ttu-id="66a79-292">모듈은 새 요청을 수신할 때 프로세스를 다시 시작하려고 하고, 마지막 롤링 기간(분)에 앱이 **rapidFailsPerMinute**번 시작에 실패한 경우가 아니면 이후 요청이 들어올 때 프로세스를 계속 다시 시작하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-292">The module attempts to relaunch the process when it receives a new request and continues to attempt to restart the process on subsequent incoming requests unless the app fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p> | <span data-ttu-id="66a79-293">기본값: `120`</span><span class="sxs-lookup"><span data-stu-id="66a79-293">Default: `120`</span></span><br><span data-ttu-id="66a79-294">최소: `0`</span><span class="sxs-lookup"><span data-stu-id="66a79-294">Min: `0`</span></span><br><span data-ttu-id="66a79-295">최대: `3600`</span><span class="sxs-lookup"><span data-stu-id="66a79-295">Max: `3600`</span></span> |
| `stdoutLogEnabled` | <p><span data-ttu-id="66a79-296">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-296">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="66a79-297">true인 경우 **processPath**에 지정된 프로세스에 대한 **stdout** 및 **stderr**이 **stdoutLogFile**에 지정된 파일로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-297">If true, **stdout** and **stderr** for the process specified in **processPath** are redirected to the file specified in **stdoutLogFile**.</span></span></p> | `false` |
| `stdoutLogFile` | <p><span data-ttu-id="66a79-298">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-298">Optional string attribute.</span></span></p><p><span data-ttu-id="66a79-299">**processPath**에 지정된 프로세스에서 **stdout** 및 **stderr**이 기록되는 상대 또는 절대 파일 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-299">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** are logged.</span></span> <span data-ttu-id="66a79-300">상대 경로는 사이트 루트에 상대적인 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-300">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="66a79-301">`.`로 시작하는 모든 경로는 사이트 루트에 상대적인 경로이고 다른 모든 경로는 절대 경로로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-301">Any path starting with `.` are relative to the site root and all other paths are treated as absolute paths.</span></span> <span data-ttu-id="66a79-302">모듈이 로그 파일을 만들려면 경로에 제공된 모든 폴더가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-302">Any folders provided in the path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="66a79-303">타임스탬프, 프로세스 ID 및 파일 확장명(*.log*)은 밑줄 구분 기호를 사용하여 **stdoutLogFile** 경로의 마지막 세그먼트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-303">Using underscore delimiters, a timestamp, process ID, and file extension (*.log*) are added to the last segment of the **stdoutLogFile** path.</span></span> <span data-ttu-id="66a79-304">`.\logs\stdout`이 값으로 제공되는 경우 예제 stdout 로그는 2018년 2월 5일 19시 41분 32초에 프로세스 ID 1934를 사용하여 저장될 경우 *logs* 폴더에 *stdout_20180205194132_1934.log*로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-304">If `.\logs\stdout` is supplied as a value, an example stdout log is saved as *stdout_20180205194132_1934.log* in the *logs* folder when saved on 2/5/2018 at 19:41:32 with a process ID of 1934.</span></span></p> | `aspnetcore-stdout` |

::: moniker-end

### <a name="setting-environment-variables"></a><span data-ttu-id="66a79-305">환경 변수 설정</span><span class="sxs-lookup"><span data-stu-id="66a79-305">Setting environment variables</span></span>

<span data-ttu-id="66a79-306">`processPath` 특성에서 프로세스에 대한 환경 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-306">Environment variables can be specified for the process in the `processPath` attribute.</span></span> <span data-ttu-id="66a79-307">`environmentVariables` 컬렉션 요소의 `environmentVariable` 자식 요소를 사용하여 환경 변수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-307">Specify an environment variable with the `environmentVariable` child element of an `environmentVariables` collection element.</span></span> <span data-ttu-id="66a79-308">이 섹션에 설정된 환경 변수가 시스템 환경 변수보다 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-308">Environment variables set in this section take precedence over system environment variables.</span></span>

<span data-ttu-id="66a79-309">다음 예제에서는 두 개의 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-309">The following example sets two environment variables.</span></span> <span data-ttu-id="66a79-310">`ASPNETCORE_ENVIRONMENT`는 앱의 환경을 `Development`로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-310">`ASPNETCORE_ENVIRONMENT` configures the app's environment to `Development`.</span></span> <span data-ttu-id="66a79-311">앱 예외를 디버그할 때 [개발자 예외 페이지](xref:fundamentals/error-handling)를 강제로 로드하기 위해 개발자가 *web.config* 파일에서 이 값을 일시적으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-311">A developer may temporarily set this value in the *web.config* file in order to force the [Developer Exception Page](xref:fundamentals/error-handling) to load when debugging an app exception.</span></span> <span data-ttu-id="66a79-312">`CONFIG_DIR`은 개발자가 앱 구성 파일을 로드할 경로를 생성하기 위해 시작 시 값을 읽는 코드를 작성한 사용자 정의 환경 변수의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-312">`CONFIG_DIR` is an example of a user-defined environment variable, where the developer has written code that reads the value on startup to form a path for loading the app's configuration file.</span></span>

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
> <span data-ttu-id="66a79-313">인터넷과 같은 신뢰할 수 없는 네트워크에 액세스할 수 없는 스테이징 및 테스트 서버에서는 `ASPNETCORE_ENVIRONMENT` 환경 변수를 `Development`로 설정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-313">Only set the `ASPNETCORE_ENVIRONMENT` environment variable to `Development` on staging and testing servers that aren't accessible to untrusted networks, such as the Internet.</span></span>

## <a name="appofflinehtm"></a><span data-ttu-id="66a79-314">app_offline.htm</span><span class="sxs-lookup"><span data-stu-id="66a79-314">app_offline.htm</span></span>

<span data-ttu-id="66a79-315">응용 프로그램의 루트 디렉터리에서 이름이 *app_offline.htm*인 파일이 검색되면 ASP.NET Core 모듈은 앱을 자동으로 종료하고 들어오는 요청 처리를 중지하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-315">If a file with the name *app_offline.htm* is detected in the root directory of an app, the ASP.NET Core Module attempts to gracefully shutdown the app and stop processing incoming requests.</span></span> <span data-ttu-id="66a79-316">`shutdownTimeLimit`에 정의된 시간(초) 후에도 앱이 계속 실행되면 ASP.NET Core 모듈은 실행 중인 프로세스를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-316">If the app is still running after the number of seconds defined in `shutdownTimeLimit`, the ASP.NET Core Module kills the running process.</span></span>

<span data-ttu-id="66a79-317">*app_offline.htm* 파일이 있는 동안 ASP.NET Core 모듈은 *app_offline.htm* 파일의 콘텐츠를 다시 보내 요청에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-317">While the *app_offline.htm* file is present, the ASP.NET Core Module responds to requests by sending back the contents of the *app_offline.htm* file.</span></span> <span data-ttu-id="66a79-318">*app_offline.htm* 파일이 제거되면 다음 요청이 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-318">When the *app_offline.htm* file is removed, the next request starts the app.</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="66a79-319">Out-of-Process 호스팅 모델을 사용할 때 열린 연결이 있으면 앱이 즉시 종료되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-319">When using the out-of-process hosting model, the app might not shut down immediately if there's an open connection.</span></span> <span data-ttu-id="66a79-320">예를 들어, WebSocket 연결은 앱 종료를 지연시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-320">For example, a websocket connection may delay app shut down.</span></span>

::: moniker-end

## <a name="start-up-error-page"></a><span data-ttu-id="66a79-321">시작 오류 페이지</span><span class="sxs-lookup"><span data-stu-id="66a79-321">Start-up error page</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="66a79-322">In process 및 out of process 호스팅은 모두 앱을 시작하지 못할 때 사용자 지정 오류 페이지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-322">Both in-process and out-of-process hosting produce custom error pages when they fail to start the app.</span></span>

<span data-ttu-id="66a79-323">ASP.NET Core 모듈이 in-process 또는 out-of-process 요청 처리기를 찾지 못하면 *500.0 - In-Process/Out-of-process 처리기 로드 실패* 상태 코드 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-323">If the ASP.NET Core Module fails to find either the in-process or out-of-process request handler, a *500.0 - In-Process/Out-Of-Process Handler Load Failure* status code page appears.</span></span>

<span data-ttu-id="66a79-324">in-process 호스팅의 경우 ASP.NET Core 모듈이 앱을 시작하지 못하면 *500.30 - 시작 실패* 상태 코드 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-324">For in-process hosting if the ASP.NET Core Module fails to start the app, a *500.30 - Start Failure* status code page appears.</span></span>

<span data-ttu-id="66a79-325">out-of-process 호스팅의 경우 ASP.NET Core 모듈이 백 엔드 프로세스를 시작하지 못하거나 백 엔드 프로세스가 시작되지만 구성된 포트에서 수신 대기하지 못하면 *502.5 - 프로세스 실패* 상태 코드 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-325">For out-of-process hosting if the ASP.NET Core Module fails to launch the backend process or the backend process starts but fails to listen on the configured port, a *502.5 - Process Failure* status code page appears.</span></span>

<span data-ttu-id="66a79-326">이 페이지를 표시하지 않고 기본 IIS 5xx 상태 코드 페이지로 되돌리려면 `disableStartUpErrorPage` 특성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-326">To suppress this page and revert to the default IIS 5xx status code page, use the `disableStartUpErrorPage` attribute.</span></span> <span data-ttu-id="66a79-327">사용자 지정 오류 메시지 구성에 대한 자세한 내용은 [HTTP 오류 \<httpErrors>](/iis/configuration/system.webServer/httpErrors/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66a79-327">For more information on configuring custom error messages, see [HTTP Errors \<httpErrors>](/iis/configuration/system.webServer/httpErrors/).</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.2"

<span data-ttu-id="66a79-328">ASP.NET Core 모듈이 백 엔드 프로세스를 시작하지 못하거나 백 엔드 프로세스가 시작되지만 구성된 포트에서 수신 대기하지 못하면 *502.5 - 프로세스 실패* 상태 코드 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-328">If the ASP.NET Core Module fails to launch the backend process or the backend process starts but fails to listen on the configured port, a *502.5 - Process Failure* status code page appears.</span></span> <span data-ttu-id="66a79-329">이 페이지를 표시하지 않고 기본 IIS 502 상태 코드 페이지로 되돌리려면 `disableStartUpErrorPage` 특성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-329">To suppress this page and revert to the default IIS 502 status code page, use the `disableStartUpErrorPage` attribute.</span></span> <span data-ttu-id="66a79-330">사용자 지정 오류 메시지 구성에 대한 자세한 내용은 [HTTP 오류 \<httpErrors>](/iis/configuration/system.webServer/httpErrors/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66a79-330">For more information on configuring custom error messages, see [HTTP Errors \<httpErrors>](/iis/configuration/system.webServer/httpErrors/).</span></span>

![502.5 프로세스 실패 상태 코드 페이지](aspnet-core-module/_static/ANCM-502_5.png)

::: moniker-end

## <a name="log-creation-and-redirection"></a><span data-ttu-id="66a79-332">로그 만들기 및 리디렉션</span><span class="sxs-lookup"><span data-stu-id="66a79-332">Log creation and redirection</span></span>

<span data-ttu-id="66a79-333">ASP.NET Core 모듈은 `aspNetCore` 요소의 `stdoutLogEnabled` 및 `stdoutLogFile` 특성이 설정된 경우 stdout 및 stderr 콘솔 출력을 디스크로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-333">The ASP.NET Core Module redirects stdout and stderr console output to disk if the `stdoutLogEnabled` and `stdoutLogFile` attributes of the `aspNetCore` element are set.</span></span> <span data-ttu-id="66a79-334">모듈이 로그 파일을 만들려면 `stdoutLogFile` 경로의 모든 폴더가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-334">Any folders in the `stdoutLogFile` path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="66a79-335">앱 풀에는 로그가 기록될 위치에 쓰기 권한이 있어야 합니다(`IIS AppPool\<app_pool_name>`을 사용하여 쓰기 권한 제공).</span><span class="sxs-lookup"><span data-stu-id="66a79-335">The app pool must have write access to the location where the logs are written (use `IIS AppPool\<app_pool_name>` to provide write permission).</span></span>

<span data-ttu-id="66a79-336">프로세스 재생/다시 시작이 발생하지 않는 한 로그는 회전되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-336">Logs aren't rotated, unless process recycling/restart occurs.</span></span> <span data-ttu-id="66a79-337">로그에서 사용하는 디스크 공간을 제한하는 것은 호스터의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-337">It's the responsibility of the hoster to limit the disk space the logs consume.</span></span>

<span data-ttu-id="66a79-338">stdout 로그는 앱 시작 문제를 해결하는 경우에만 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-338">Using the stdout log is only recommended for troubleshooting app startup issues.</span></span> <span data-ttu-id="66a79-339">일반 앱 로깅을 위해 stdout 로그를 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="66a79-339">Don't use the stdout log for general app logging purposes.</span></span> <span data-ttu-id="66a79-340">ASP.NET Core 앱의 루틴 로깅에는 로그 파일 크기를 제한하고 로그를 회전하는 로깅 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-340">For routine logging in an ASP.NET Core app, use a logging library that limits log file size and rotates logs.</span></span> <span data-ttu-id="66a79-341">자세한 내용은 [타사 로깅 공급자](xref:fundamentals/logging/index#third-party-logging-providers)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66a79-341">For more information, see [third-party logging providers](xref:fundamentals/logging/index#third-party-logging-providers).</span></span>

<span data-ttu-id="66a79-342">로그 파일이 만들어질 때 타임스탬프 및 파일 확장명이 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-342">A timestamp and file extension are added automatically when the log file is created.</span></span> <span data-ttu-id="66a79-343">로그 파일 이름은 타임스탬프, 프로세스 ID 및 파일 확장명(*.log*)을 밑줄로 구분된 `stdoutLogFile` 경로의 마지막 세그먼트(일반적으로 *stdout*)에 추가하여 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-343">The log file name is composed by appending the timestamp, process ID, and file extension (*.log*) to the last segment of the `stdoutLogFile` path (typically *stdout*) delimited by underscores.</span></span> <span data-ttu-id="66a79-344">`stdoutLogFile` 경로가 *stdout*으로 끝나는 경우 2018년 2월 5일 19시 42분 32초에 만들어진 PID 1934를 사용하는 앱에 대한 로그의 파일 이름은 *stdout_20180205194132_1934.log*입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-344">If the `stdoutLogFile` path ends with *stdout*, a log for an app with a PID of 1934 created on 2/5/2018 at 19:42:32 has the file name *stdout_20180205194132_1934.log*.</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="66a79-345">`stdoutLogEnabled`가 false이면 앱 시작 시 발생하는 오류가 캡처되어 최대 30KB의 이벤트 로그로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-345">If `stdoutLogEnabled` is false, errors that occur on app startup are captured and emitted to the event log up to 30 KB.</span></span> <span data-ttu-id="66a79-346">시작 후에는 모든 추가 로그가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-346">After startup, all additional logs are discarded.</span></span>

::: moniker-end

<span data-ttu-id="66a79-347">다음 샘플 `aspNetCore` 요소는 Azure App Service에서 호스트되는 앱에 대한 stdout 로깅을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-347">The following sample `aspNetCore` element configures stdout logging for an app hosted in Azure App Service.</span></span> <span data-ttu-id="66a79-348">로컬 로깅에는 로컬 경로 또는 네트워크 공유 경로가 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-348">A local path or network share path is acceptable for local logging.</span></span> <span data-ttu-id="66a79-349">AppPool 사용자 ID에 제공된 경로에 쓸 수 있는 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-349">Confirm that the AppPool user identity has permission to write to the path provided.</span></span>

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

## <a name="enhanced-diagnostic-logs"></a><span data-ttu-id="66a79-350">개선된 진단 로그</span><span class="sxs-lookup"><span data-stu-id="66a79-350">Enhanced diagnostic logs</span></span>

<span data-ttu-id="66a79-351">ASP.NET Core 모듈 제공은 개선된 진단 로그를 제공하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-351">The ASP.NET Core Module provides is configurable to provide enhanced diagnostics logs.</span></span> <span data-ttu-id="66a79-352">*web.config*의 `<aspNetCore>` 요소에 `<handlerSettings>` 요소를 추가합니다. `debugLevel`을 `TRACE`으로 설정하면 진단 정보의 충실도가 높아집니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-352">Add the `<handlerSettings>` element to the `<aspNetCore>` element in *web.config*. Setting the `debugLevel` to `TRACE` exposes a higher fidelity of diagnostic information:</span></span>

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

<span data-ttu-id="66a79-353">디버그 수준 (`debugLevel`) 값은 수준과 위치를 모두 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-353">Debug level (`debugLevel`) values can include both the level and the location.</span></span>

<span data-ttu-id="66a79-354">수준(최소한에서 가장 자세한 정보까지 순서대로 ):</span><span class="sxs-lookup"><span data-stu-id="66a79-354">Levels (in order from least to most verbose):</span></span>

* <span data-ttu-id="66a79-355">오류</span><span class="sxs-lookup"><span data-stu-id="66a79-355">ERROR</span></span>
* <span data-ttu-id="66a79-356">경고</span><span class="sxs-lookup"><span data-stu-id="66a79-356">WARNING</span></span>
* <span data-ttu-id="66a79-357">정보</span><span class="sxs-lookup"><span data-stu-id="66a79-357">INFO</span></span>
* <span data-ttu-id="66a79-358">TRACE</span><span class="sxs-lookup"><span data-stu-id="66a79-358">TRACE</span></span>

<span data-ttu-id="66a79-359">위치(여러 위치가 허용됨):</span><span class="sxs-lookup"><span data-stu-id="66a79-359">Locations (multiple locations are permitted):</span></span>

* <span data-ttu-id="66a79-360">CONSOLE</span><span class="sxs-lookup"><span data-stu-id="66a79-360">CONSOLE</span></span>
* <span data-ttu-id="66a79-361">EVENTLOG</span><span class="sxs-lookup"><span data-stu-id="66a79-361">EVENTLOG</span></span>
* <span data-ttu-id="66a79-362">파일</span><span class="sxs-lookup"><span data-stu-id="66a79-362">FILE</span></span>

<span data-ttu-id="66a79-363">처리기 설정은 환경 변수를 통해서도 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-363">The handler settings can also be provided via environment variables:</span></span>

* <span data-ttu-id="66a79-364">`ASPNETCORE_MODULE_DEBUG_FILE` &ndash; 디버그 로그 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-364">`ASPNETCORE_MODULE_DEBUG_FILE` &ndash; Path to the debug log file.</span></span> <span data-ttu-id="66a79-365">(기본값: *aspnetcore-debug.log*)</span><span class="sxs-lookup"><span data-stu-id="66a79-365">(Default: *aspnetcore-debug.log*)</span></span>
* <span data-ttu-id="66a79-366">`ASPNETCORE_MODULE_DEBUG` &ndash; 디버그 수준 설정.</span><span class="sxs-lookup"><span data-stu-id="66a79-366">`ASPNETCORE_MODULE_DEBUG` &ndash; Debug level setting.</span></span>

> [!WARNING]
> <span data-ttu-id="66a79-367">배포에서 문제를 해결하는 데 필요한 시간보다 오래 디버그 로깅을 사용하도록 설정하지 **마세요**.</span><span class="sxs-lookup"><span data-stu-id="66a79-367">Do **not** leave debug logging enabled in the deployment for longer than required to troubleshoot an issue.</span></span> <span data-ttu-id="66a79-368">로그의 크기는 제한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-368">The size of the log isn't limited.</span></span> <span data-ttu-id="66a79-369">디버그 로그를 사용하도록 설정한 대로 두면 사용 가능한 디스크 공간이 소진되어 서버 또는 앱 서비스가 크래시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-369">Leaving the debug log enabled can exhaust the available disk space and crash the server or app service.</span></span>

::: moniker-end

<span data-ttu-id="66a79-370">*web.config* 파일에 있는 `aspNetCore` 요소의 예제에 대해서는 [web.config를 사용한 구성](#configuration-with-webconfig)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66a79-370">See [Configuration with web.config](#configuration-with-webconfig) for an example of the `aspNetCore` element in the *web.config* file.</span></span>

## <a name="proxy-configuration-uses-http-protocol-and-a-pairing-token"></a><span data-ttu-id="66a79-371">프록시 구성은 HTTP 프로토콜 및 페어링 토큰을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-371">Proxy configuration uses HTTP protocol and a pairing token</span></span>

::: moniker range=">= aspnetcore-2.2"

<span data-ttu-id="66a79-372">*호스팅에만 적용됩니다.*</span><span class="sxs-lookup"><span data-stu-id="66a79-372">*Only applies to out-of-process hosting.*</span></span>

::: moniker-end

<span data-ttu-id="66a79-373">ASP.NET Core 모듈과 Kestrel 사이에 만들어진 프록시는 HTTP 프로토콜을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-373">The proxy created between the ASP.NET Core Module and Kestrel uses the HTTP protocol.</span></span> <span data-ttu-id="66a79-374">HTTP 사용은 모듈과 Kestrel 간의 트래픽이 네트워크 인터페이스에서 분리된 루프백 주소에서 발생하는 성능 최적화입니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-374">Using HTTP is a performance optimization, where the traffic between the module and Kestrel takes place on a loopback address off of the network interface.</span></span> <span data-ttu-id="66a79-375">서버에서 분리된 위치에서 모듈과 Kestrel 간 트래픽 도청의 위험은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-375">There's no risk of eavesdropping the traffic between the module and Kestrel from a location off of the server.</span></span>

<span data-ttu-id="66a79-376">페어링 토큰은 Kestrel에서 받은 요청이 IIS에서 프록시되었으며 다른 원본에서 오지 않았다는 것을 보장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-376">A pairing token is used to guarantee that the requests received by Kestrel were proxied by IIS and didn't come from some other source.</span></span> <span data-ttu-id="66a79-377">페어링 토큰은 모듈에 의해 생성되며 환경 변수(`ASPNETCORE_TOKEN`)로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-377">The pairing token is created and set into an environment variable (`ASPNETCORE_TOKEN`) by the module.</span></span> <span data-ttu-id="66a79-378">페어링 토큰은 프록시된 모든 요청에서 헤더(`MSAspNetCoreToken`)로도 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-378">The pairing token is also set into a header (`MSAspNetCoreToken`) on every proxied request.</span></span> <span data-ttu-id="66a79-379">IIS 미들웨어는 수신하는 각 요청을 검사하여 페어링 토큰 헤더 값이 환경 변수 값과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-379">IIS Middleware checks each request it receives to confirm that the pairing token header value matches the environment variable value.</span></span> <span data-ttu-id="66a79-380">토큰 값이 일치하지 않는 경우 요청이 기록되고 거부됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-380">If the token values are mismatched, the request is logged and rejected.</span></span> <span data-ttu-id="66a79-381">페어링 토큰 환경 변수와 모듈과 Kestrel 간의 트래픽은 서버에서 분리된 위치에서 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-381">The pairing token environment variable and the traffic between the module and Kestrel aren't accessible from a location off of the server.</span></span> <span data-ttu-id="66a79-382">페어링 토큰 값을 알지 못하면 공격자는 IIS 미들웨어에서 검사를 무시하는 요청을 전송할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-382">Without knowing the pairing token value, an attacker can't submit requests that bypass the check in the IIS Middleware.</span></span>

## <a name="aspnet-core-module-with-an-iis-shared-configuration"></a><span data-ttu-id="66a79-383">IIS 공유 구성이 포함된 ASP.NET Core 모듈</span><span class="sxs-lookup"><span data-stu-id="66a79-383">ASP.NET Core Module with an IIS Shared Configuration</span></span>

<span data-ttu-id="66a79-384">ASP.NET Core 모듈 설치 관리자는 **SYSTEM** 계정의 권한으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-384">The ASP.NET Core Module installer runs with the privileges of the **SYSTEM** account.</span></span> <span data-ttu-id="66a79-385">로컬 시스템 계정에는 IIS 공유 구성에서 사용하는 공유 경로에 대한 수정 권한이 없으므로 공유의 *applicationHost.config*에서 모듈 설정을 구성하려고 하면 설치 관리자에서 액세스 거부 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-385">Because the local system account doesn't have modify permission for the share path used by the IIS Shared Configuration, the installer hits an access denied error when attempting to configure the module settings in *applicationHost.config* on the share.</span></span> <span data-ttu-id="66a79-386">IIS 공유 구성을 사용할 경우 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-386">When using an IIS Shared Configuration, follow these steps:</span></span>

1. <span data-ttu-id="66a79-387">IIS 공유 구성을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-387">Disable the IIS Shared Configuration.</span></span>
1. <span data-ttu-id="66a79-388">설치 관리자를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-388">Run the installer.</span></span>
1. <span data-ttu-id="66a79-389">업데이트된 *applicationHost.config* 파일을 공유로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-389">Export the updated *applicationHost.config* file to the share.</span></span>
1. <span data-ttu-id="66a79-390">IIS 공유 구성을 다시 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-390">Re-enable the IIS Shared Configuration.</span></span>

## <a name="module-version-and-hosting-bundle-installer-logs"></a><span data-ttu-id="66a79-391">모듈 버전 및 호스팅 번들 설치 관리자 로그</span><span class="sxs-lookup"><span data-stu-id="66a79-391">Module version and Hosting Bundle installer logs</span></span>

<span data-ttu-id="66a79-392">설치된 ASP.NET Core 모듈의 버전을 확인하려면:</span><span class="sxs-lookup"><span data-stu-id="66a79-392">To determine the version of the installed ASP.NET Core Module:</span></span>

1. <span data-ttu-id="66a79-393">호스팅 시스템에서 *%windir%\System32\inetsrv*로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-393">On the hosting system, navigate to *%windir%\System32\inetsrv*.</span></span>
1. <span data-ttu-id="66a79-394">*aspnetcore.dll* 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-394">Locate the *aspnetcore.dll* file.</span></span>
1. <span data-ttu-id="66a79-395">파일을 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-395">Right-click the file and select **Properties** from the contextual menu.</span></span>
1. <span data-ttu-id="66a79-396">**세부 정보** 탭을 선택합니다. **파일 버전** 및 **제품 버전**은 설치된 모듈 버전을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-396">Select the **Details** tab. The **File version** and **Product version** represent the installed version of the module.</span></span>

<span data-ttu-id="66a79-397">모듈에 대한 호스팅 번들 설치 관리자 로그는 *C:\\Users\\%UserName%\\AppData\\Local\\Temp*에 있습니다. 파일 이름은 *dd_DotNetCoreWinSvrHosting__\<timestamp>_000_AspNetCoreModule_x64.log*로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-397">The Hosting Bundle installer logs for the module are found at *C:\\Users\\%UserName%\\AppData\\Local\\Temp*. The file is named *dd_DotNetCoreWinSvrHosting__\<timestamp>_000_AspNetCoreModule_x64.log*.</span></span>

## <a name="module-schema-and-configuration-file-locations"></a><span data-ttu-id="66a79-398">모듈, 스키마 및 구성 파일 위치</span><span class="sxs-lookup"><span data-stu-id="66a79-398">Module, schema, and configuration file locations</span></span>

### <a name="module"></a><span data-ttu-id="66a79-399">Module</span><span class="sxs-lookup"><span data-stu-id="66a79-399">Module</span></span>

<span data-ttu-id="66a79-400">**IIS(x86/amd64):**</span><span class="sxs-lookup"><span data-stu-id="66a79-400">**IIS (x86/amd64):**</span></span>

   * <span data-ttu-id="66a79-401">%windir%\System32\inetsrv\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="66a79-401">%windir%\System32\inetsrv\aspnetcore.dll</span></span>

   * <span data-ttu-id="66a79-402">%windir%\SysWOW64\inetsrv\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="66a79-402">%windir%\SysWOW64\inetsrv\aspnetcore.dll</span></span>

::: moniker range=">= aspnetcore-2.2"

   * <span data-ttu-id="66a79-403">%ProgramFiles%\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll</span><span class="sxs-lookup"><span data-stu-id="66a79-403">%ProgramFiles%\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll</span></span>

   * <span data-ttu-id="66a79-404">%ProgramFiles(x86)%\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll</span><span class="sxs-lookup"><span data-stu-id="66a79-404">%ProgramFiles(x86)%\IIS\Asp.Net Core Module\V2\aspnetcorev2.dll</span></span>

::: moniker-end

<span data-ttu-id="66a79-405">**IIS Express(x86/amd64):**</span><span class="sxs-lookup"><span data-stu-id="66a79-405">**IIS Express (x86/amd64):**</span></span>

   * <span data-ttu-id="66a79-406">%ProgramFiles%\IIS Express\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="66a79-406">%ProgramFiles%\IIS Express\aspnetcore.dll</span></span>

   * <span data-ttu-id="66a79-407">%ProgramFiles(x86)%\IIS Express\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="66a79-407">%ProgramFiles(x86)%\IIS Express\aspnetcore.dll</span></span>

::: moniker range=">= aspnetcore-2.2"

   * <span data-ttu-id="66a79-408">%ProgramFiles%\IIS Express\Asp.Net Core Module\V2\aspnetcorev2.dll</span><span class="sxs-lookup"><span data-stu-id="66a79-408">%ProgramFiles%\IIS Express\Asp.Net Core Module\V2\aspnetcorev2.dll</span></span>

   * <span data-ttu-id="66a79-409">%ProgramFiles(x86)%\IIS Express\Asp.Net Core Module\V2\aspnetcorev2.dll</span><span class="sxs-lookup"><span data-stu-id="66a79-409">%ProgramFiles(x86)%\IIS Express\Asp.Net Core Module\V2\aspnetcorev2.dll</span></span>

::: moniker-end

### <a name="schema"></a><span data-ttu-id="66a79-410">스키마</span><span class="sxs-lookup"><span data-stu-id="66a79-410">Schema</span></span>

<span data-ttu-id="66a79-411">**IIS**</span><span class="sxs-lookup"><span data-stu-id="66a79-411">**IIS**</span></span>

   * <span data-ttu-id="66a79-412">%windir%\System32\inetsrv\config\schema\aspnetcore_schema.xml</span><span class="sxs-lookup"><span data-stu-id="66a79-412">%windir%\System32\inetsrv\config\schema\aspnetcore_schema.xml</span></span>

::: moniker range=">= aspnetcore-2.2"

   * <span data-ttu-id="66a79-413">%windir%\System32\inetsrv\config\schema\aspnetcore_schema_v2.xml</span><span class="sxs-lookup"><span data-stu-id="66a79-413">%windir%\System32\inetsrv\config\schema\aspnetcore_schema_v2.xml</span></span>

::: moniker-end
<span data-ttu-id="66a79-414">**IIS Express**</span><span class="sxs-lookup"><span data-stu-id="66a79-414">**IIS Express**</span></span>

   * <span data-ttu-id="66a79-415">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema.xml</span><span class="sxs-lookup"><span data-stu-id="66a79-415">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema.xml</span></span>

::: moniker range=">= aspnetcore-2.2"

   * <span data-ttu-id="66a79-416">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema_v2.xml</span><span class="sxs-lookup"><span data-stu-id="66a79-416">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema_v2.xml</span></span>

::: moniker-end

### <a name="configuration"></a><span data-ttu-id="66a79-417">구성</span><span class="sxs-lookup"><span data-stu-id="66a79-417">Configuration</span></span>

<span data-ttu-id="66a79-418">**IIS**</span><span class="sxs-lookup"><span data-stu-id="66a79-418">**IIS**</span></span>

   * <span data-ttu-id="66a79-419">%windir%\System32\inetsrv\config\applicationHost.config</span><span class="sxs-lookup"><span data-stu-id="66a79-419">%windir%\System32\inetsrv\config\applicationHost.config</span></span>

<span data-ttu-id="66a79-420">**IIS Express**</span><span class="sxs-lookup"><span data-stu-id="66a79-420">**IIS Express**</span></span>

   * <span data-ttu-id="66a79-421">%ProgramFiles%\IIS Express\config\templates\PersonalWebServer\applicationHost.config</span><span class="sxs-lookup"><span data-stu-id="66a79-421">%ProgramFiles%\IIS Express\config\templates\PersonalWebServer\applicationHost.config</span></span>

<span data-ttu-id="66a79-422">*applicationHost.config* 파일에서 *aspnetcore*를 검색하여 파일을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66a79-422">The files can be found by searching for *aspnetcore* in the *applicationHost.config* file.</span></span>
