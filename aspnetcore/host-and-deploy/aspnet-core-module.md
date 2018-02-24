---
title: "ASP.NET Core 모듈 구성 참조"
author: guardrex
description: "ASP.NET Core 응용 프로그램을 호스팅하기 위한 ASP.NET Core 모듈을 구성 하는 방법을 알아봅니다."
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 02/15/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/aspnet-core-module
ms.openlocfilehash: c01abed767a226eae68725c1c53d922eac2f705e
ms.sourcegitcommit: 49fb3b7669b504d35edad34db8285e56b958a9fc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/23/2018
---
# <a name="aspnet-core-module-configuration-reference"></a><span data-ttu-id="e0d5e-103">ASP.NET Core 모듈 구성 참조</span><span class="sxs-lookup"><span data-stu-id="e0d5e-103">ASP.NET Core Module configuration reference</span></span>

<span data-ttu-id="e0d5e-104">여 [Luke Latham](https://github.com/guardrex), [Rick Anderson](https://twitter.com/RickAndMSFT), 및 [Sourabh Shirhatti](https://twitter.com/sshirhatti)</span><span class="sxs-lookup"><span data-stu-id="e0d5e-104">By [Luke Latham](https://github.com/guardrex), [Rick Anderson](https://twitter.com/RickAndMSFT), and [Sourabh Shirhatti](https://twitter.com/sshirhatti)</span></span>

<span data-ttu-id="e0d5e-105">이 문서는 ASP.NET Core 응용 프로그램을 호스팅하기 위한 ASP.NET Core 모듈을 구성 하는 방법에 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-105">This document provides instructions on how to configure the ASP.NET Core Module for hosting ASP.NET Core apps.</span></span> <span data-ttu-id="e0d5e-106">ASP.NET Core 모듈 및 설치 지침에 대 한 소개를 참조 하십시오.는 [ASP.NET Core 모듈 개요](xref:fundamentals/servers/aspnet-core-module)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-106">For an introduction to the ASP.NET Core Module and installation instructions, see the [ASP.NET Core Module overview](xref:fundamentals/servers/aspnet-core-module).</span></span>

## <a name="configuration-with-webconfig"></a><span data-ttu-id="e0d5e-107">Web.config 구성</span><span class="sxs-lookup"><span data-stu-id="e0d5e-107">Configuration with web.config</span></span>

<span data-ttu-id="e0d5e-108">ASP.NET Core 모듈 구성 된는 `aspNetCore` 의 섹션은 `system.webServer` 노드 사이트의 *web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-108">The ASP.NET Core Module is configured with the `aspNetCore` section of the `system.webServer` node in the site's *web.config* file.</span></span>

<span data-ttu-id="e0d5e-109">다음 *web.config* 파일이 게시 되는 [프레임 워크 종속 배포](/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd) 사이트 요청을 처리 하도록 ASP.NET Core 모듈을 구성 하 고:</span><span class="sxs-lookup"><span data-stu-id="e0d5e-109">The following *web.config* file is published for a [framework-dependent deployment](/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd) and configures the ASP.NET Core Module to handle site requests:</span></span>

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

<span data-ttu-id="e0d5e-110">다음 *web.config* 에 대 한 게시는 [자체 포함된 배포](/dotnet/articles/core/deploying/#self-contained-deployments-scd):</span><span class="sxs-lookup"><span data-stu-id="e0d5e-110">The following *web.config* is published for a [self-contained deployment](/dotnet/articles/core/deploying/#self-contained-deployments-scd):</span></span>

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

<span data-ttu-id="e0d5e-111">응용 프로그램에 배포 되는 경우 [Azure 앱 서비스](https://azure.microsoft.com/services/app-service/), `stdoutLogFile` 경로가 설정 되었는지 `\\?\%home%\LogFiles\stdout`합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-111">When an app is deployed to [Azure App Service](https://azure.microsoft.com/services/app-service/), the `stdoutLogFile` path is set to `\\?\%home%\LogFiles\stdout`.</span></span> <span data-ttu-id="e0d5e-112">Stdout 로그를 저장 하는 경로 *LogFiles* 폴더에 위치를 자동으로 서비스에 의해 만들어진 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-112">The path saves stdout logs to the *LogFiles* folder, which is a location automatically created by the service.</span></span>

<span data-ttu-id="e0d5e-113">참조 [하위 응용 프로그램 구성](xref:host-and-deploy/iis/index#sub-application-configuration) 의 구성에 관련 된 중요 정보에 대 한 *web.config* 하위 앱의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-113">See [Sub-application configuration](xref:host-and-deploy/iis/index#sub-application-configuration) for an important note pertaining to the configuration of *web.config* files in sub-apps.</span></span>

### <a name="attributes-of-the-aspnetcore-element"></a><span data-ttu-id="e0d5e-114">AspNetCore 요소의 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-114">Attributes of the aspNetCore element</span></span>

| <span data-ttu-id="e0d5e-115">특성</span><span class="sxs-lookup"><span data-stu-id="e0d5e-115">Attribute</span></span> | <span data-ttu-id="e0d5e-116">설명</span><span class="sxs-lookup"><span data-stu-id="e0d5e-116">Description</span></span> | <span data-ttu-id="e0d5e-117">기본</span><span class="sxs-lookup"><span data-stu-id="e0d5e-117">Default</span></span> |
| --------- | ----------- | :-----: |
| `arguments` | <p><span data-ttu-id="e0d5e-118">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-118">Optional string attribute.</span></span></p><p><span data-ttu-id="e0d5e-119">에 지정 된 실행 파일에 대 한 인수 **processPath**합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-119">Arguments to the executable specified in **processPath**.</span></span></p>| |
| `disableStartUpErrorPage` | <span data-ttu-id="e0d5e-120">참 또는 거짓입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-120">true or false.</span></span></p><p><span data-ttu-id="e0d5e-121">True 이면는 **502.5-프로세스 오류** 페이지는 표시 되지 않으며 502 상태 코드 페이지에 구성 된는 *web.config* 우선적으로 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-121">If true, the **502.5 - Process Failure** page is suppressed, and the 502 status code page configured in the *web.config* takes precedence.</span></span></p> | `false` |
| `forwardWindowsAuthToken` | <span data-ttu-id="e0d5e-122">참 또는 거짓입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-122">true or false.</span></span></p><p><span data-ttu-id="e0d5e-123">True 이면 토큰 요청당 헤더로 ' MS ASPNETCORE WINAUTHTOKEN' % ASPNETCORE_PORT %에서 수신 하는 자식 프로세스에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-123">If true, the token is forwarded to the child process listening on %ASPNETCORE_PORT% as a header 'MS-ASPNETCORE-WINAUTHTOKEN' per request.</span></span> <span data-ttu-id="e0d5e-124">것은 해당 프로세스를 요청에 따라이 토큰에 CloseHandle 호출의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-124">It's the responsibility of that process to call CloseHandle on this token per request.</span></span></p> | `true` |
| `processPath` | <p><span data-ttu-id="e0d5e-125">필수 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-125">Required string attribute.</span></span></p><p><span data-ttu-id="e0d5e-126">HTTP 요청을 수신 하는 프로세스를 시작 하는 실행 파일 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-126">Path to the executable that launches a process listening for HTTP requests.</span></span> <span data-ttu-id="e0d5e-127">상대 경로 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-127">Relative paths are supported.</span></span> <span data-ttu-id="e0d5e-128">로 시작 하는 경로 경우 `.`, 경로 사이트 루트 기준 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-128">If the path begins with `.`, the path is considered to be relative to the site root.</span></span></p> | |
| `rapidFailsPerMinute` | <p><span data-ttu-id="e0d5e-129">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-129">Optional integer attribute.</span></span></p><p><span data-ttu-id="e0d5e-130">에 지정 된 프로세스의 수를 지정 **processPath** 분당 충돌을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-130">Specifies the number of times the process specified in **processPath** is allowed to crash per minute.</span></span> <span data-ttu-id="e0d5e-131">이 제한을 초과 하는 나머지 분에서 프로세스 시작 모듈을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-131">If this limit is exceeded, the module stops launching the process for the remainder of the minute.</span></span></p> | `10` |
| `requestTimeout` | <p><span data-ttu-id="e0d5e-132">선택적 timespan 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-132">Optional timespan attribute.</span></span></p><p><span data-ttu-id="e0d5e-133">ASP.NET Core 모듈 ASPNETCORE_PORT % %를 수신 하는 프로세스에서 응답에 대 한 대기 기간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-133">Specifies the duration for which the ASP.NET Core Module waits for a response from the process listening on %ASPNETCORE_PORT%.</span></span></p><p><span data-ttu-id="e0d5e-134">`requestTimeout` 지정 해야이 분 단위로, 그렇지 않으면 기본적으로 2 분입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-134">The `requestTimeout` must be specified in whole minutes only, otherwise it defaults to 2 minutes.</span></span></p> | `00:02:00` |
| `shutdownTimeLimit` | <p><span data-ttu-id="e0d5e-135">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-135">Optional integer attribute.</span></span></p><p><span data-ttu-id="e0d5e-136">기간 (초)를 정상적으로 종료 실행 파일에 대 한 모듈에서 대기 하는 경우는 *app_offline.htm* 파일이 검색 될 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-136">Duration in seconds that the module waits for the executable to gracefully shutdown when the *app_offline.htm* file is detected.</span></span></p> | `10` |
| `startupTimeLimit` | <p><span data-ttu-id="e0d5e-137">선택적 정수 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-137">Optional integer attribute.</span></span></p><p><span data-ttu-id="e0d5e-138">포트에서 수신 하는 프로세스가 시작 되는 파일에 대 한 모듈에서 대기 하는 시간 (초) 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-138">Duration in seconds that the module waits for the executable to start a process listening on the port.</span></span> <span data-ttu-id="e0d5e-139">이 시간 제한을 초과 하는 모듈에서 프로세스를 중단 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-139">If this time limit is exceeded, the module kills the process.</span></span> <span data-ttu-id="e0d5e-140">모듈에서 새 요청을 수신 하 고 앱이 시작 되지 않는 한 이후 들어오는 요청에서 프로세스를 다시 시작 하려고 계속 경우 프로세스를 다시 시작 하려고 **rapidFailsPerMinute** 지난에서 번 롤링 분입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-140">The module attempts to relaunch the process when it receives a new request and continues to attempt to restart the process on subsequent incoming requests unless the app fails to start **rapidFailsPerMinute** number of times in the last rolling minute.</span></span></p> | `120` |
| `stdoutLogEnabled` | <p><span data-ttu-id="e0d5e-141">선택적 부울 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-141">Optional Boolean attribute.</span></span></p><p><span data-ttu-id="e0d5e-142">True 이면 **stdout** 및 **stderr** 에 지정 된 프로세스에 대 한 **processPath** 는에 지정 된 파일로 리디렉션할 **가 stdoutLogFile**합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-142">If true, **stdout** and **stderr** for the process specified in **processPath** are redirected to the file specified in **stdoutLogFile**.</span></span></p> | `false` |
| `stdoutLogFile` | <p><span data-ttu-id="e0d5e-143">선택적 문자열 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-143">Optional string attribute.</span></span></p><p><span data-ttu-id="e0d5e-144">상대 또는 절대 파일 경로를 지정 **stdout** 및 **stderr** 에 지정 된 프로세스에서 **processPath** 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-144">Specifies the relative or absolute file path for which **stdout** and **stderr** from the process specified in **processPath** are logged.</span></span> <span data-ttu-id="e0d5e-145">상대 경로 사이트의 루트를 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-145">Relative paths are relative to the root of the site.</span></span> <span data-ttu-id="e0d5e-146">로 시작 하는 경로 `.` 은 절대 경로로 루트 및 다른 모든 경로 사이트에 상대적인 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-146">Any path starting with `.` are relative to the site root and all other paths are treated as absolute paths.</span></span> <span data-ttu-id="e0d5e-147">모든 폴더 경로에 제공 된 로그 파일을 만들 모듈에 대 한 순서에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-147">Any folders provided in the path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="e0d5e-148">밑줄 구분 기호, 타임 스탬프, 프로세스 ID 및 파일 확장명을 사용 하 여 (*.log*) 세그먼트의 마지막으로 추가 된 **가 stdoutLogFile** 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-148">Using underscore delimiters, a timestamp, process ID, and file extension (*.log*) are added to the last segment of the **stdoutLogFile** path.</span></span> <span data-ttu-id="e0d5e-149">경우 `.\logs\stdout` 제공 예제 stdout 로그로 저장 된 값으로 *stdout_20180205194132_1934.log* 에 *로그* 19시 41분: 32 1934의 프로세스 id는 2/5/2018에 저장할 경우 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-149">If `.\logs\stdout` is supplied as a value, an example stdout log is saved as *stdout_20180205194132_1934.log* in the *logs* folder when saved on 2/5/2018 at 19:41:32 with a process ID of 1934.</span></span></p> | `aspnetcore-stdout` |

### <a name="setting-environment-variables"></a><span data-ttu-id="e0d5e-150">환경 변수 설정</span><span class="sxs-lookup"><span data-stu-id="e0d5e-150">Setting environment variables</span></span>

<span data-ttu-id="e0d5e-151">프로세스에 대 한 환경 변수를 지정할 수 있습니다는 `processPath` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-151">Environment variables can be specified for the process in the `processPath` attribute.</span></span> <span data-ttu-id="e0d5e-152">지정 된 환경 변수는 `environmentVariable` 의 자식 요소는 `environmentVariables` 컬렉션 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-152">Specify an environment variable with the `environmentVariable` child element of an `environmentVariables` collection element.</span></span> <span data-ttu-id="e0d5e-153">이 섹션에 설정 된 환경 변수 보다 우선 적용 시스템 환경 변수.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-153">Environment variables set in this section take precedence over system environment variables.</span></span>

<span data-ttu-id="e0d5e-154">다음 예제에서는 두 개의 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-154">The following example sets two environment variables.</span></span> <span data-ttu-id="e0d5e-155">`ASPNETCORE_ENVIRONMENT` 앱의 환경을 구성 `Development`합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-155">`ASPNETCORE_ENVIRONMENT` configures the app's environment to `Development`.</span></span> <span data-ttu-id="e0d5e-156">개발자에 일시적으로이 값을 설정할 수 있습니다는 *web.config* 강제 파일은 [개발자 예외 페이지](xref:fundamentals/error-handling) 를 응용 프로그램 예외를 디버깅 하는 경우 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-156">A developer may temporarily set this value in the *web.config* file in order to force the [Developer Exception Page](xref:fundamentals/error-handling) to load when debugging an app exception.</span></span> <span data-ttu-id="e0d5e-157">`CONFIG_DIR` 한 예로, 사용자 정의 환경 변수 개발자 시작할 응용 프로그램의 구성 파일을 로드 하는 것에 대 한 경로를 구성할 때 값을 읽을 수 있는 코드를 기록 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-157">`CONFIG_DIR` is an example of a user-defined environment variable, where the developer has written code that reads the value on startup to form a path for loading the app's configuration file.</span></span>

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

> [!WARNING]
> <span data-ttu-id="e0d5e-158">에 설정는 `ASPNETCORE_ENVIRONMENT` envirnonment 변수를 `Development` 준비 하 고 테스트 인터넷과 같은 신뢰할 수 없는 네트워크에 액세스할 수 없는 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-158">Only set the `ASPNETCORE_ENVIRONMENT` envirnonment variable to `Development` on staging and testing servers that aren't accessible to untrusted networks, such as the Internet.</span></span>

## <a name="appofflinehtm"></a><span data-ttu-id="e0d5e-159">app_offline.htm</span><span class="sxs-lookup"><span data-stu-id="e0d5e-159">app_offline.htm</span></span>

<span data-ttu-id="e0d5e-160">이름 가진 파일이 있으면 *app_offline.htm* 응용 프로그램의 루트 디렉터리에서 검색 된 앱 및 들어오는 요청을 처리 하는 중지 ASP.NET Core 모듈 정상 종료 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-160">If a file with the name *app_offline.htm* is detected in the root directory of an app, the ASP.NET Core Module attempts to gracefully shutdown the app and stop processing incoming requests.</span></span> <span data-ttu-id="e0d5e-161">응용 프로그램에 정의 된 시간 (초)이 지나면 여전히 실행 중인 경우 `shutdownTimeLimit`, ASP.NET Core 모듈에서 실행 중인 프로세스를 중단 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-161">If the app is still running after the number of seconds defined in `shutdownTimeLimit`, the ASP.NET Core Module kills the running process.</span></span>

<span data-ttu-id="e0d5e-162">반면는 *app_offline.htm* 파일이 없으면 ASP.NET Core 모듈 요청에 응답의 내용을 다시 전송 하 여는 *app_offline.htm* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-162">While the *app_offline.htm* file is present, the ASP.NET Core Module responds to requests by sending back the contents of the *app_offline.htm* file.</span></span> <span data-ttu-id="e0d5e-163">경우는 *app_offline.htm* 다음 요청 응용 프로그램이 시작, 파일은 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-163">When the *app_offline.htm* file is removed, the next request starts the app.</span></span>

## <a name="start-up-error-page"></a><span data-ttu-id="e0d5e-164">시작 오류 페이지</span><span class="sxs-lookup"><span data-stu-id="e0d5e-164">Start-up error page</span></span>

<span data-ttu-id="e0d5e-165">ASP.NET Core 모듈을 백 엔드 프로세스 또는 백 엔드 프로세스 시작 하지만 구성된 된 포트에서 수신 하도록 실패를 시작할 수 없는 경우는 *502.5 프로세스 오류* 상태 코드 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-165">If the ASP.NET Core Module fails to launch the backend process or the backend process starts but fails to listen on the configured port, a *502.5 Process Failure* status code page appears.</span></span> <span data-ttu-id="e0d5e-166">이 페이지를 표시 하지 않는 하 여 기본 IIS 502 상태 코드 페이지로 되돌리려면 사용은 `disableStartUpErrorPage` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-166">To suppress this page and revert to the default IIS 502 status code page, use the `disableStartUpErrorPage` attribute.</span></span> <span data-ttu-id="e0d5e-167">사용자 정의 오류 메시지를 구성 하는 방법에 대 한 자세한 내용은 참조 하십시오. [HTTP 오류 `<httpErrors>` ](/iis/configuration/system.webServer/httpErrors/)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-167">For more information on configuring custom error messages, see [HTTP Errors `<httpErrors>`](/iis/configuration/system.webServer/httpErrors/).</span></span>

![502.5 프로세스 오류 상태 코드 페이지](aspnet-core-module/_static/ANCM-502_5.png)

## <a name="log-creation-and-redirection"></a><span data-ttu-id="e0d5e-169">로그 만들기 및 리디렉션</span><span class="sxs-lookup"><span data-stu-id="e0d5e-169">Log creation and redirection</span></span>

<span data-ttu-id="e0d5e-170">ASP.NET Core 모듈 리디렉션합니다 `stdout` 및 `stderr` 로그 디스크에 `stdoutLogEnabled` 및 `stdoutLogFile` 의 특성은 `aspNetCore` 요소 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-170">The ASP.NET Core Module redirects `stdout` and `stderr` logs to disk if the `stdoutLogEnabled` and `stdoutLogFile` attributes of the `aspNetCore` element are set.</span></span> <span data-ttu-id="e0d5e-171">에 있는 폴더는 `stdoutLogFile` 경로 로그 파일을 만들 모듈에 대 한 순서에 존재 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-171">Any folders in the `stdoutLogFile` path must exist in order for the module to create the log file.</span></span> <span data-ttu-id="e0d5e-172">타임 스탬프 및 파일 확장명은 로그 파일을 만들 때 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-172">A timestamp and file extension are added automatically when the log file is created.</span></span> <span data-ttu-id="e0d5e-173">프로세스 재활용/를 다시 시작이 발생 하지 않으면 로그가 회전 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-173">Logs aren't rotated, unless process recycling/restart occurs.</span></span> <span data-ttu-id="e0d5e-174">것은 로그 사용할 디스크 공간을 제한 하는 호스팅 서비스 공급자의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-174">It's the responsibility of the hoster to limit the disk space the logs consume.</span></span> <span data-ttu-id="e0d5e-175">사용 하는 `stdout` 로그 응용 프로그램 시작 문제 해결에 권장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-175">Using the `stdout` log is only recommended for troubleshooting app startup issues.</span></span> <span data-ttu-id="e0d5e-176">일반 응용 프로그램 로깅 목적 stdout 로그를 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-176">Don't use the stdout log for general app logging purposes.</span></span> <span data-ttu-id="e0d5e-177">ASP.NET Core 응용 프로그램의 일상적인 로깅에 대 한 로그 파일 크기를 제한 하 고 로그를 회전 하는 로깅 라이브러리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-177">For routine logging in an ASP.NET Core app, use a logging library that limits log file size and rotates logs.</span></span> <span data-ttu-id="e0d5e-178">자세한 내용은 참조 [제 3 자 로깅 공급자](xref:fundamentals/logging/index#third-party-logging-providers)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-178">For more information, see [third-party logging providers](xref:fundamentals/logging/index#third-party-logging-providers).</span></span>

<span data-ttu-id="e0d5e-179">타임 스탬프, 프로세스 ID 및 파일 확장명을 추가 하 여 로그 파일 이름이 구성 됩니다 (*.log*)의 마지막 세그먼트에는 `stdoutLogFile` 경로 (일반적으로 *stdout*) 밑줄로 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-179">The log file name is composed by appending the timestamp, process ID, and file extension (*.log*) to the last segment of the `stdoutLogFile` path (typically *stdout*) delimited by underscores.</span></span> <span data-ttu-id="e0d5e-180">경우는 `stdoutLogFile` 로 끝나는 경로 *stdout*, 19시 42분: 32에서 2/5/2018에서 만든 1934의 PID 사용 하 여 앱에 대 한 로그 파일 이름이 *stdout_20180205194132_1934.log*합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-180">If the `stdoutLogFile` path ends with *stdout*, a log for an app with a PID of 1934 created on 2/5/2018 at 19:42:32 has the file name *stdout_20180205194132_1934.log*.</span></span>

<span data-ttu-id="e0d5e-181">다음 샘플 `aspNetCore` 요소 구성 `stdout` Azure 앱 서비스에서 호스팅되는 앱에 대 한 로깅을 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-181">The following sample `aspNetCore` element configures `stdout` logging for an app hosted in Azure App Service.</span></span> <span data-ttu-id="e0d5e-182">로컬 경로 또는 네트워크 공유 경로 로컬 로깅 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-182">A local path or network share path is acceptable for local logging.</span></span> <span data-ttu-id="e0d5e-183">AppPool 사용자 id 제공 된 경로에 쓸 수 있는 권한이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-183">Confirm that the AppPool user identity has permission to write to the path provided.</span></span>

```xml
<aspNetCore processPath="dotnet"
    arguments=".\MyApp.dll"
    stdoutLogEnabled="true"
    stdoutLogFile="\\?\%home%\LogFiles\stdout">
</aspNetCore>
```

<span data-ttu-id="e0d5e-184">참조 [web.config 사용 하 여 구성을](#configuration-with-webconfig) 의 예는 `aspNetCore` 요소에는 *web.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-184">See [Configuration with web.config](#configuration-with-webconfig) for an example of the `aspNetCore` element in the *web.config* file.</span></span>

## <a name="aspnet-core-module-with-an-iis-shared-configuration"></a><span data-ttu-id="e0d5e-185">IIS 사용 하 여 ASP.NET Core 모듈 구성 공유</span><span class="sxs-lookup"><span data-stu-id="e0d5e-185">ASP.NET Core Module with an IIS Shared Configuration</span></span>

<span data-ttu-id="e0d5e-186">ASP.NET Core 모듈 설치 관리자의 권한으로 실행 되는 **시스템** 계정.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-186">The ASP.NET Core Module installer runs with the privileges of the **SYSTEM** account.</span></span> <span data-ttu-id="e0d5e-187">설치 관리자가 액세스 거부 오류가에서 모듈 설정을 구성 하는 동안 로컬 시스템 계정에서 IIS 공유 구성을 사용 하는 공유 경로 대 한 권한을 수정 하지 않습니다, 때문에 *applicationHost.config* 공유에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-187">Because the local system account doesn't have modify permission for the share path used by the IIS Shared Configuration, the installer hits an access denied error when attempting to configure the module settings in *applicationHost.config* on the share.</span></span> <span data-ttu-id="e0d5e-188">IIS 공유 구성을 사용 하는 경우 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-188">When using an IIS Shared Configuration, follow these steps:</span></span>

1. <span data-ttu-id="e0d5e-189">IIS 공유 구성을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-189">Disable the IIS Shared Configuration.</span></span>
1. <span data-ttu-id="e0d5e-190">설치 관리자를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-190">Run the installer.</span></span>
1. <span data-ttu-id="e0d5e-191">업데이트 된 내보내기 *applicationHost.config* 파일을 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-191">Export the updated *applicationHost.config* file to the share.</span></span>
1. <span data-ttu-id="e0d5e-192">IIS 공유 구성을 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-192">Re-enable the IIS Shared Configuration.</span></span>

## <a name="module-version-and-hosting-bundle-installer-logs"></a><span data-ttu-id="e0d5e-193">모듈의 버전 및 번들 설치 관리자 로그를 호스팅</span><span class="sxs-lookup"><span data-stu-id="e0d5e-193">Module version and hosting bundle installer logs</span></span>

<span data-ttu-id="e0d5e-194">확인 하려면 설치 된 ASP.NET Core 모듈 버전:</span><span class="sxs-lookup"><span data-stu-id="e0d5e-194">To determine the version of the installed ASP.NET Core Module:</span></span>

1. <span data-ttu-id="e0d5e-195">호스팅 시스템에서로 이동 *%windir%\System32\inetsrv*합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-195">On the hosting system, navigate to *%windir%\System32\inetsrv*.</span></span>
1. <span data-ttu-id="e0d5e-196">찾을 *aspnetcore.dll* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-196">Locate the *aspnetcore.dll* file.</span></span>
1. <span data-ttu-id="e0d5e-197">파일을 마우스 오른쪽 단추로 클릭 하 고 선택 **속성** 상황에 맞는 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-197">Right-click the file and select **Properties** from the contextual menu.</span></span>
1. <span data-ttu-id="e0d5e-198">선택 된 **세부 정보** 탭 합니다. **파일 버전** 및 **제품 버전** 모듈의 설치 된 버전을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-198">Select the **Details** tab. The **File version** and **Product version** represent the installed version of the module.</span></span>

<span data-ttu-id="e0d5e-199">모듈에 대 한 Windows 서버 호스팅 번들 설치 관리자 로그에서 발견 되 *c:\\사용자\\% UserName %\\AppData\\로컬\\Temp*합니다. 파일의 이름은 *dd_DotNetCoreWinSvrHosting__\<타임 스탬프 > _000_AspNetCoreModule_x64.log*합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-199">The Windows Server Hosting bundle installer logs for the module are found at *C:\\Users\\%UserName%\\AppData\\Local\\Temp*. The file is named *dd_DotNetCoreWinSvrHosting__\<timestamp>_000_AspNetCoreModule_x64.log*.</span></span>

## <a name="module-schema-and-configuration-file-locations"></a><span data-ttu-id="e0d5e-200">모듈, 스키마 및 구성 파일 위치</span><span class="sxs-lookup"><span data-stu-id="e0d5e-200">Module, schema, and configuration file locations</span></span>

### <a name="module"></a><span data-ttu-id="e0d5e-201">Module</span><span class="sxs-lookup"><span data-stu-id="e0d5e-201">Module</span></span>

<span data-ttu-id="e0d5e-202">**IIS (x86/amd64):**</span><span class="sxs-lookup"><span data-stu-id="e0d5e-202">**IIS (x86/amd64):**</span></span>

   * <span data-ttu-id="e0d5e-203">%windir%\System32\inetsrv\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="e0d5e-203">%windir%\System32\inetsrv\aspnetcore.dll</span></span>

   * <span data-ttu-id="e0d5e-204">%windir%\SysWOW64\inetsrv\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="e0d5e-204">%windir%\SysWOW64\inetsrv\aspnetcore.dll</span></span>

<span data-ttu-id="e0d5e-205">**IIS Express (x86/amd64):**</span><span class="sxs-lookup"><span data-stu-id="e0d5e-205">**IIS Express (x86/amd64):**</span></span>

   * <span data-ttu-id="e0d5e-206">%ProgramFiles%\IIS Express\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="e0d5e-206">%ProgramFiles%\IIS Express\aspnetcore.dll</span></span>

   * <span data-ttu-id="e0d5e-207">%ProgramFiles(x86)%\IIS Express\aspnetcore.dll</span><span class="sxs-lookup"><span data-stu-id="e0d5e-207">%ProgramFiles(x86)%\IIS Express\aspnetcore.dll</span></span>

### <a name="schema"></a><span data-ttu-id="e0d5e-208">스키마</span><span class="sxs-lookup"><span data-stu-id="e0d5e-208">Schema</span></span>

<span data-ttu-id="e0d5e-209">**IIS**</span><span class="sxs-lookup"><span data-stu-id="e0d5e-209">**IIS**</span></span>

   * <span data-ttu-id="e0d5e-210">%windir%\System32\inetsrv\config\schema\aspnetcore_schema.xml</span><span class="sxs-lookup"><span data-stu-id="e0d5e-210">%windir%\System32\inetsrv\config\schema\aspnetcore_schema.xml</span></span>

<span data-ttu-id="e0d5e-211">**IIS Express**</span><span class="sxs-lookup"><span data-stu-id="e0d5e-211">**IIS Express**</span></span>

   * <span data-ttu-id="e0d5e-212">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema.xml</span><span class="sxs-lookup"><span data-stu-id="e0d5e-212">%ProgramFiles%\IIS Express\config\schema\aspnetcore_schema.xml</span></span>

### <a name="configuration"></a><span data-ttu-id="e0d5e-213">구성</span><span class="sxs-lookup"><span data-stu-id="e0d5e-213">Configuration</span></span>

<span data-ttu-id="e0d5e-214">**IIS**</span><span class="sxs-lookup"><span data-stu-id="e0d5e-214">**IIS**</span></span>

   * <span data-ttu-id="e0d5e-215">%windir%\System32\inetsrv\config\applicationHost.config</span><span class="sxs-lookup"><span data-stu-id="e0d5e-215">%windir%\System32\inetsrv\config\applicationHost.config</span></span>

<span data-ttu-id="e0d5e-216">**IIS Express**</span><span class="sxs-lookup"><span data-stu-id="e0d5e-216">**IIS Express**</span></span>

   * <span data-ttu-id="e0d5e-217">.vs\config\applicationHost.config</span><span class="sxs-lookup"><span data-stu-id="e0d5e-217">.vs\config\applicationHost.config</span></span>

<span data-ttu-id="e0d5e-218">검색 하 여 파일을 찾을 수 *aspnetcore.dll* 에 *applicationHost.config* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-218">The files can be found by searching for *aspnetcore.dll* in the *applicationHost.config* file.</span></span> <span data-ttu-id="e0d5e-219">IIS express는 *applicationHost.config* 파일은 기본적으로 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-219">For IIS Express, the *applicationHost.config* file won't exist by default.</span></span> <span data-ttu-id="e0d5e-220">파일을 만들  *\<application_root >\\.vs\\config* 때 Visual Studio 솔루션에서 모든 웹 응용 프로그램 프로젝트를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0d5e-220">The file is created at *\<application_root>\\.vs\\config* when starting any web app project in the Visual Studio solution.</span></span>
