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
# <a name="aspnet-core-module-configuration-reference"></a>ASP.NET Core 모듈 구성 참조

작성자: [Luke Latham](https://github.com/guardrex), [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Sourabh Shirhatti](https://twitter.com/sshirhatti)

이 문서에서는 ASP.NET Core 앱을 호스트하기 위해 ASP.NET Core 모듈을 구성하는 방법에 대한 지침을 제공합니다. ASP.NET Core 모듈 및 설치 지침에 대한 개요는 [ASP.NET Core 모듈 개요](xref:fundamentals/servers/aspnet-core-module)를 참조하세요.

::: moniker range=">= aspnetcore-2.2"

## <a name="hosting-model"></a>호스팅 모델

.NET Core 2.2 이상에서 실행되는 앱의 경우, 모듈에서는 역방향 프록시(Out-of-Process) 호스팅과 비교할 때 더 나은 성능을 제공하기 위해 In-Process 호스팅 모델을 지원합니다. 자세한 내용은 <xref:fundamentals/servers/aspnet-core-module#aspnet-core-module-description>을 참조하세요.

In-Process 호스팅은 기존 앱에 대한 옵트인(opt in) 기능이지만 [dotnet new](/dotnet/core/tools/dotnet-new) 템플릿은 기본적으로 모든 IIS 및 IIS Express 시나리오에 대해 In-Process 호스팅 모델로 설정됩니다.

In-Process 호스팅용 앱을 구성하려면 `<AspNetCoreModuleHostingModel>` 속성을 `inprocess` 값의 앱 프로젝트 파일에 추가합니다(Out-of-Process 호스팅은 `outofprocess`로 설정됨).

```xml
<PropertyGroup>
  <AspNetCoreModuleHostingModel>inprocess</AspNetCoreModuleHostingModel>
</PropertyGroup>
```

다음 특성은 In-Process로 호스팅할 때 적용됩니다.

* [Kestrel 서버](xref:fundamentals/servers/kestrel)가 사용되지 않습니다. 사용자 지정 <xref:Microsoft.AspNetCore.Hosting.Server.IServer> 구현인 `IISHttpServer`가 앱의 서버 역할을 합니다.

* [requestTimeout 특성](#attributes-of-the-aspnetcore-element)이 In-Process 호스팅에 적용되지 않습니다.

* 앱 간의 앱 풀 공유는 지원되지 않습니다. 앱당 하나의 앱 풀을 사용합니다.

* [웹 배포](/iis/publish/using-web-deploy/introduction-to-web-deploy)를 사용하거나 [app_offline.htm 파일을 배포에](xref:host-and-deploy/iis/index#locked-deployment-files) 수동으로 배치할 경우 열린 연결이 있으면 앱이 즉시 종료되지 않을 수 있습니다. 예를 들어, WebSocket 연결은 앱 종료를 지연시킬 수 있습니다.

* 앱 및 설치된 런타임(x64 또는 x86)의 아키텍처(비트)는 앱 풀의 아키텍처와 일치해야 합니다.

* `WebHostBuilder`([CreateDefaultBuilder](xref:fundamentals/host/web-host#set-up-a-host)를 사용하지 않고)를 사용하여 앱 호스트를 수동으로 설정하며 앱이 Kestrel 서버에서 직접 실행되는 경우(자체 호스트됨) `UseIISIntegration`를 호출하기 전에 `UseKestrel`를 호출합니다. 이 순서가 바뀌면 호스트가 시작되지 않습니다.

### <a name="hosting-model-changes"></a>호스팅 모델 변경

`hostingModel` 설정이 *web.config* 파일에서 변경되면([web.config로 구성](#configuration-with-webconfig) 섹션에 설명되어 있음) 모듈은 IIS에 대한 작업자 프로세스를 재순환합니다.

IIS Express의 경우 모듈은 작업자 프로세스를 재순환하지 않고, 대신 현재 IIS Express 프로세스의 정상 종료를 트리거합니다. 앱에 대한 다음 요청은 새 IIS Express 프로세스를 생성합니다.

### <a name="process-name"></a>프로세스 이름

`Process.GetCurrentProcess().ProcessName`은 `w3wp`(In-Process) 또는 `dotnet`(Out-of-Process)을 보고합니다.

::: moniker-end

## <a name="configuration-with-webconfig"></a>web.config를 사용한 구성

ASP.NET Core 모듈은 사이트의 *web.config* 파일에 있는 `system.webServer` 노드의 `aspNetCore` 섹션으로 구성됩니다.

다음 *web.config* 파일은 [프레임워크 종속 배포](/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd)를 위해 게시되고 사이트 요청을 처리하도록 ASP.NET Core 모듈을 구성합니다.

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

다음 *web.config*는 [자체 포함 배포](/dotnet/articles/core/deploying/#self-contained-deployments-scd)를 위해 게시됩니다.

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

앱이 [Azure App Service](https://azure.microsoft.com/services/app-service/)에 배포되면 `stdoutLogFile` 경로가 `\\?\%home%\LogFiles\stdout`로 설정됩니다. 이 경로는 서비스에서 자동으로 만들어진 위치인 *LogFiles* 폴더에 stdout 로그를 저장합니다.

하위 앱에서 *web.config* 파일의 구성에 관한 중요 참고 사항은 [하위 응용 프로그램 구성](xref:host-and-deploy/iis/index#sub-application-configuration)을 참조하세요.

### <a name="attributes-of-the-aspnetcore-element"></a>aspNetCore 요소의 특성

::: moniker range=">= aspnetcore-2.2"

| 특성 | 설명 | 기본 |
| --------- | ----------- | :-----: |
| `arguments` | <p>선택적 문자열 특성입니다.</p><p>**processPath**에 지정된 실행 파일에 대한 인수입니다.</p>| |
| `disableStartUpErrorPage` | <p>선택적 부울 특성입니다.</p><p>true인 경우 **502.5 - 프로세스 실패** 페이지가 표시되지 않고 *web.config*에 구성된 502 상태 코드 페이지가 우선 적용됩니다.</p> | `false` |
| `forwardWindowsAuthToken` | <p>선택적 부울 특성입니다.</p><p>true인 경우 토큰은 %ASPNETCORE_PORT%에서 수신 대기하는 자식 프로세스에 요청별 헤더 'MS-ASPNETCORE-WINAUTHTOKEN'으로 전달됩니다. 이 프로세스는 요청별로 이 토큰에서 CloseHandle을 호출합니다.</p> | `true` |
| `hostingModel` | <p>선택적 문자열 특성입니다.</p><p>호스팅 모델을 In-Process(`inprocess`) 또는 Out-of-Process(`outofprocess`)로 지정합니다.</p> | `outofprocess` |
| `processesPerApplication` | <p>선택적 정수 특성입니다.</p><p>앱별로 스핀 업할 수 있는 **processPath** 설정에 지정된 프로세스의 인스턴스 수를 지정합니다.</p><p>&dagger;In-Process 호스팅의 경우 이 값은 `1`로 제한됩니다.</p> | 기본값: `1`<br>최소: `1`<br>최대: `100`&dagger; |
| `processPath` | <p>필수 문자열 특성입니다.</p><p>HTTP 요청을 수신 대기하는 프로세스를 시작하는 실행 파일의 경로입니다. 상대 경로가 지원됩니다. 경로가 `.`로 시작되면 경로는 사이트 루트의 상대 경로로 간주됩니다.</p> | |
| `rapidFailsPerMinute` | <p>선택적 정수 특성입니다.</p><p>**processPath**에 지정된 프로세스의 분당 크래시 허용 횟수를 지정합니다. 이 제한을 초과하면 모듈은 남은 시간 동안 프로세스 시작을 중지합니다.</p><p>In-Process 호스팅에서는 지원되지 않습니다.</p> | 기본값: `10`<br>최소: `0`<br>최대: `100` |
| `requestTimeout` | <p>선택적 시간 간격 특성입니다.</p><p>ASP.NET Core 모듈이 %ASPNETCORE_PORT%에서 수신 대기하는 프로세스의 응답을 기다리는 기간을 지정합니다.</p><p>ASP.NET Core 2.1 이상 릴리스와 함께 제공되는 ASP.NET Core 모듈 버전에서는 `requestTimeout`이 전체 시간, 분, 초로 지정됩니다.</p><p>In-Process 호스팅에는 적용되지 않습니다. In-Process 호스팅의 경우 모듈은 앱이 요청을 처리할 때까지 기다립니다.</p> | 기본값: `00:02:00`<br>최소: `00:00:00`<br>최대: `360:00:00` |
| `shutdownTimeLimit` | <p>선택적 정수 특성입니다.</p><p>*app_offline.htm* 파일이 검색될 때 실행 파일이 정상적으로 종료될 때까지 모듈이 기다리는 기간(초)입니다.</p> | 기본값: `10`<br>최소: `0`<br>최대: `600` |
| `startupTimeLimit` | <p>선택적 정수 특성입니다.</p><p>실행 파일이 포트에서 수신 대기하는 프로세스를 시작할 때까지 모듈이 기다리는 기간(초)입니다. 이 시간 제한을 초과하면 모듈이 프로세스를 종료합니다. 모듈은 새 요청을 수신할 때 프로세스를 다시 시작하려고 하고, 마지막 롤링 기간(분)에 앱이 **rapidFailsPerMinute**번 시작에 실패한 경우가 아니면 이후 요청이 들어올 때 프로세스를 계속 다시 시작하려고 합니다.</p><p>값 0은 무한 시간 제한으로 간주되지 **않습니다**.</p> | 기본값: `120`<br>최소: `0`<br>최대: `3600` |
| `stdoutLogEnabled` | <p>선택적 부울 특성입니다.</p><p>true인 경우 **processPath**에 지정된 프로세스에 대한 **stdout** 및 **stderr**이 **stdoutLogFile**에 지정된 파일로 리디렉션됩니다.</p> | `false` |
| `stdoutLogFile` | <p>선택적 문자열 특성입니다.</p><p>**processPath**에 지정된 프로세스에서 **stdout** 및 **stderr**이 기록되는 상대 또는 절대 파일 경로를 지정합니다. 상대 경로는 사이트 루트에 상대적인 경로입니다. `.`로 시작하는 모든 경로는 사이트 루트에 상대적인 경로이고 다른 모든 경로는 절대 경로로 처리됩니다. 모듈이 로그 파일을 만들려면 경로에 제공된 모든 폴더가 있어야 합니다. 타임스탬프, 프로세스 ID 및 파일 확장명(*.log*)은 밑줄 구분 기호를 사용하여 **stdoutLogFile** 경로의 마지막 세그먼트에 추가됩니다. `.\logs\stdout`이 값으로 제공되는 경우 예제 stdout 로그는 2018년 2월 5일 19시 41분 32초에 프로세스 ID 1934를 사용하여 저장될 경우 *logs* 폴더에 *stdout_20180205194132_1934.log*로 저장됩니다.</p> | `aspnetcore-stdout` |

::: moniker-end

::: moniker range="= aspnetcore-2.1"

| 특성 | 설명 | 기본 |
| --------- | ----------- | :-----: |
| `arguments` | <p>선택적 문자열 특성입니다.</p><p>**processPath**에 지정된 실행 파일에 대한 인수입니다.</p>| |
| `disableStartUpErrorPage` | <p>선택적 부울 특성입니다.</p><p>true인 경우 **502.5 - 프로세스 실패** 페이지가 표시되지 않고 *web.config*에 구성된 502 상태 코드 페이지가 우선 적용됩니다.</p> | `false` |
| `forwardWindowsAuthToken` | <p>선택적 부울 특성입니다.</p><p>true인 경우 토큰은 %ASPNETCORE_PORT%에서 수신 대기하는 자식 프로세스에 요청별 헤더 'MS-ASPNETCORE-WINAUTHTOKEN'으로 전달됩니다. 이 프로세스는 요청별로 이 토큰에서 CloseHandle을 호출합니다.</p> | `true` |
| `processesPerApplication` | <p>선택적 정수 특성입니다.</p><p>앱별로 스핀 업할 수 있는 **processPath** 설정에 지정된 프로세스의 인스턴스 수를 지정합니다.</p> | 기본값: `1`<br>최소: `1`<br>최대: `100` |
| `processPath` | <p>필수 문자열 특성입니다.</p><p>HTTP 요청을 수신 대기하는 프로세스를 시작하는 실행 파일의 경로입니다. 상대 경로가 지원됩니다. 경로가 `.`로 시작되면 경로는 사이트 루트의 상대 경로로 간주됩니다.</p> | |
| `rapidFailsPerMinute` | <p>선택적 정수 특성입니다.</p><p>**processPath**에 지정된 프로세스의 분당 크래시 허용 횟수를 지정합니다. 이 제한을 초과하면 모듈은 남은 시간 동안 프로세스 시작을 중지합니다.</p> | 기본값: `10`<br>최소: `0`<br>최대: `100` |
| `requestTimeout` | <p>선택적 시간 간격 특성입니다.</p><p>ASP.NET Core 모듈이 %ASPNETCORE_PORT%에서 수신 대기하는 프로세스의 응답을 기다리는 기간을 지정합니다.</p><p>ASP.NET Core 2.1 이상 릴리스와 함께 제공되는 ASP.NET Core 모듈 버전에서는 `requestTimeout`이 전체 시간, 분, 초로 지정됩니다.</p> | 기본값: `00:02:00`<br>최소: `00:00:00`<br>최대: `360:00:00` |
| `shutdownTimeLimit` | <p>선택적 정수 특성입니다.</p><p>*app_offline.htm* 파일이 검색될 때 실행 파일이 정상적으로 종료될 때까지 모듈이 기다리는 기간(초)입니다.</p> | 기본값: `10`<br>최소: `0`<br>최대: `600` |
| `startupTimeLimit` | <p>선택적 정수 특성입니다.</p><p>실행 파일이 포트에서 수신 대기하는 프로세스를 시작할 때까지 모듈이 기다리는 기간(초)입니다. 이 시간 제한을 초과하면 모듈이 프로세스를 종료합니다. 모듈은 새 요청을 수신할 때 프로세스를 다시 시작하려고 하고, 마지막 롤링 기간(분)에 앱이 **rapidFailsPerMinute**번 시작에 실패한 경우가 아니면 이후 요청이 들어올 때 프로세스를 계속 다시 시작하려고 합니다.</p><p>값 0은 무한 시간 제한으로 간주되지 **않습니다**.</p> | 기본값: `120`<br>최소: `0`<br>최대: `3600` |
| `stdoutLogEnabled` | <p>선택적 부울 특성입니다.</p><p>true인 경우 **processPath**에 지정된 프로세스에 대한 **stdout** 및 **stderr**이 **stdoutLogFile**에 지정된 파일로 리디렉션됩니다.</p> | `false` |
| `stdoutLogFile` | <p>선택적 문자열 특성입니다.</p><p>**processPath**에 지정된 프로세스에서 **stdout** 및 **stderr**이 기록되는 상대 또는 절대 파일 경로를 지정합니다. 상대 경로는 사이트 루트에 상대적인 경로입니다. `.`로 시작하는 모든 경로는 사이트 루트에 상대적인 경로이고 다른 모든 경로는 절대 경로로 처리됩니다. 모듈이 로그 파일을 만들려면 경로에 제공된 모든 폴더가 있어야 합니다. 타임스탬프, 프로세스 ID 및 파일 확장명(*.log*)은 밑줄 구분 기호를 사용하여 **stdoutLogFile** 경로의 마지막 세그먼트에 추가됩니다. `.\logs\stdout`이 값으로 제공되는 경우 예제 stdout 로그는 2018년 2월 5일 19시 41분 32초에 프로세스 ID 1934를 사용하여 저장될 경우 *logs* 폴더에 *stdout_20180205194132_1934.log*로 저장됩니다.</p> | `aspnetcore-stdout` |

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

| 특성 | 설명 | 기본 |
| --------- | ----------- | :-----: |
| `arguments` | <p>선택적 문자열 특성입니다.</p><p>**processPath**에 지정된 실행 파일에 대한 인수입니다.</p>| |
| `disableStartUpErrorPage` | <p>선택적 부울 특성입니다.</p><p>true인 경우 **502.5 - 프로세스 실패** 페이지가 표시되지 않고 *web.config*에 구성된 502 상태 코드 페이지가 우선 적용됩니다.</p> | `false` |
| `forwardWindowsAuthToken` | <p>선택적 부울 특성입니다.</p><p>true인 경우 토큰은 %ASPNETCORE_PORT%에서 수신 대기하는 자식 프로세스에 요청별 헤더 'MS-ASPNETCORE-WINAUTHTOKEN'으로 전달됩니다. 이 프로세스는 요청별로 이 토큰에서 CloseHandle을 호출합니다.</p> | `true` |
| `processesPerApplication` | <p>선택적 정수 특성입니다.</p><p>앱별로 스핀 업할 수 있는 **processPath** 설정에 지정된 프로세스의 인스턴스 수를 지정합니다.</p> | 기본값: `1`<br>최소: `1`<br>최대: `100` |
| `processPath` | <p>필수 문자열 특성입니다.</p><p>HTTP 요청을 수신 대기하는 프로세스를 시작하는 실행 파일의 경로입니다. 상대 경로가 지원됩니다. 경로가 `.`로 시작되면 경로는 사이트 루트의 상대 경로로 간주됩니다.</p> | |
| `rapidFailsPerMinute` | <p>선택적 정수 특성입니다.</p><p>**processPath**에 지정된 프로세스의 분당 크래시 허용 횟수를 지정합니다. 이 제한을 초과하면 모듈은 남은 시간 동안 프로세스 시작을 중지합니다.</p> | 기본값: `10`<br>최소: `0`<br>최대: `100` |
| `requestTimeout` | <p>선택적 시간 간격 특성입니다.</p><p>ASP.NET Core 모듈이 %ASPNETCORE_PORT%에서 수신 대기하는 프로세스의 응답을 기다리는 기간을 지정합니다.</p><p>ASP.NET Core 2.0 이하 릴리스와 함께 제공되는 ASP.NET Core 모듈 버전에서는 `requestTimeout`을 전체 시간(분)으로만 지정해야 합니다. 그렇지 않으면 기본적으로 2분으로 설정됩니다.</p> | 기본값: `00:02:00`<br>최소: `00:00:00`<br>최대: `360:00:00` |
| `shutdownTimeLimit` | <p>선택적 정수 특성입니다.</p><p>*app_offline.htm* 파일이 검색될 때 실행 파일이 정상적으로 종료될 때까지 모듈이 기다리는 기간(초)입니다.</p> | 기본값: `10`<br>최소: `0`<br>최대: `600` |
| `startupTimeLimit` | <p>선택적 정수 특성입니다.</p><p>실행 파일이 포트에서 수신 대기하는 프로세스를 시작할 때까지 모듈이 기다리는 기간(초)입니다. 이 시간 제한을 초과하면 모듈이 프로세스를 종료합니다. 모듈은 새 요청을 수신할 때 프로세스를 다시 시작하려고 하고, 마지막 롤링 기간(분)에 앱이 **rapidFailsPerMinute**번 시작에 실패한 경우가 아니면 이후 요청이 들어올 때 프로세스를 계속 다시 시작하려고 합니다.</p> | 기본값: `120`<br>최소: `0`<br>최대: `3600` |
| `stdoutLogEnabled` | <p>선택적 부울 특성입니다.</p><p>true인 경우 **processPath**에 지정된 프로세스에 대한 **stdout** 및 **stderr**이 **stdoutLogFile**에 지정된 파일로 리디렉션됩니다.</p> | `false` |
| `stdoutLogFile` | <p>선택적 문자열 특성입니다.</p><p>**processPath**에 지정된 프로세스에서 **stdout** 및 **stderr**이 기록되는 상대 또는 절대 파일 경로를 지정합니다. 상대 경로는 사이트 루트에 상대적인 경로입니다. `.`로 시작하는 모든 경로는 사이트 루트에 상대적인 경로이고 다른 모든 경로는 절대 경로로 처리됩니다. 모듈이 로그 파일을 만들려면 경로에 제공된 모든 폴더가 있어야 합니다. 타임스탬프, 프로세스 ID 및 파일 확장명(*.log*)은 밑줄 구분 기호를 사용하여 **stdoutLogFile** 경로의 마지막 세그먼트에 추가됩니다. `.\logs\stdout`이 값으로 제공되는 경우 예제 stdout 로그는 2018년 2월 5일 19시 41분 32초에 프로세스 ID 1934를 사용하여 저장될 경우 *logs* 폴더에 *stdout_20180205194132_1934.log*로 저장됩니다.</p> | `aspnetcore-stdout` |

::: moniker-end

### <a name="setting-environment-variables"></a>환경 변수 설정

`processPath` 특성에서 프로세스에 대한 환경 변수를 지정할 수 있습니다. `environmentVariables` 컬렉션 요소의 `environmentVariable` 자식 요소를 사용하여 환경 변수를 지정합니다. 이 섹션에 설정된 환경 변수가 시스템 환경 변수보다 우선 적용됩니다.

다음 예제에서는 두 개의 환경 변수를 설정합니다. `ASPNETCORE_ENVIRONMENT`는 앱의 환경을 `Development`로 구성합니다. 앱 예외를 디버그할 때 [개발자 예외 페이지](xref:fundamentals/error-handling)를 강제로 로드하기 위해 개발자가 *web.config* 파일에서 이 값을 일시적으로 설정할 수 있습니다. `CONFIG_DIR`은 개발자가 앱 구성 파일을 로드할 경로를 생성하기 위해 시작 시 값을 읽는 코드를 작성한 사용자 정의 환경 변수의 예입니다.

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
> 인터넷과 같은 신뢰할 수 없는 네트워크에 액세스할 수 없는 스테이징 및 테스트 서버에서는 `ASPNETCORE_ENVIRONMENT` 환경 변수를 `Development`로 설정하면 됩니다.

## <a name="appofflinehtm"></a>app_offline.htm

응용 프로그램의 루트 디렉터리에서 이름이 *app_offline.htm*인 파일이 검색되면 ASP.NET Core 모듈은 앱을 자동으로 종료하고 들어오는 요청 처리를 중지하려고 합니다. `shutdownTimeLimit`에 정의된 시간(초) 후에도 앱이 계속 실행되면 ASP.NET Core 모듈은 실행 중인 프로세스를 종료합니다.

*app_offline.htm* 파일이 있는 동안 ASP.NET Core 모듈은 *app_offline.htm* 파일의 콘텐츠를 다시 보내 요청에 응답합니다. *app_offline.htm* 파일이 제거되면 다음 요청이 앱을 시작합니다.

::: moniker range=">= aspnetcore-2.2"

Out-of-Process 호스팅 모델을 사용할 때 열린 연결이 있으면 앱이 즉시 종료되지 않을 수 있습니다. 예를 들어, WebSocket 연결은 앱 종료를 지연시킬 수 있습니다.

::: moniker-end

## <a name="start-up-error-page"></a>시작 오류 페이지

::: moniker range=">= aspnetcore-2.2"

*호스팅에만 적용됩니다.*

::: moniker-end

ASP.NET Core 모듈이 백 엔드 프로세스를 시작하지 못하거나 백 엔드 프로세스가 시작되지만 구성된 포트에서 수신 대기하지 못하면 ‘502.5 프로세스 실패’ 상태 코드 페이지가 나타납니다. 이 페이지를 표시하지 않고 기본 IIS 502 상태 코드 페이지로 되돌리려면 `disableStartUpErrorPage` 특성을 사용합니다. 사용자 지정 오류 메시지 구성에 대한 자세한 내용은 [HTTP 오류`<httpErrors>`](/iis/configuration/system.webServer/httpErrors/)를 참조하세요.

![502.5 프로세스 실패 상태 코드 페이지](aspnet-core-module/_static/ANCM-502_5.png)

## <a name="log-creation-and-redirection"></a>로그 만들기 및 리디렉션

ASP.NET Core 모듈은 `aspNetCore` 요소의 `stdoutLogEnabled` 및 `stdoutLogFile` 특성이 설정된 경우 stdout 및 stderr 콘솔 출력을 디스크로 리디렉션합니다. 모듈이 로그 파일을 만들려면 `stdoutLogFile` 경로의 모든 폴더가 있어야 합니다. 앱 풀에는 로그가 기록될 위치에 쓰기 권한이 있어야 합니다(`IIS AppPool\<app_pool_name>`을 사용하여 쓰기 권한 제공).

프로세스 재생/다시 시작이 발생하지 않는 한 로그는 회전되지 않습니다. 로그에서 사용하는 디스크 공간을 제한하는 것은 호스터의 책임입니다.

stdout 로그는 앱 시작 문제를 해결하는 경우에만 사용하는 것이 좋습니다. 일반 앱 로깅을 위해 stdout 로그를 사용하지 마세요. ASP.NET Core 앱의 루틴 로깅에는 로그 파일 크기를 제한하고 로그를 회전하는 로깅 라이브러리를 사용합니다. 자세한 내용은 [타사 로깅 공급자](xref:fundamentals/logging/index#third-party-logging-providers)를 참조하세요.

로그 파일이 만들어질 때 타임스탬프 및 파일 확장명이 자동으로 추가됩니다. 로그 파일 이름은 타임스탬프, 프로세스 ID 및 파일 확장명(*.log*)을 밑줄로 구분된 `stdoutLogFile` 경로의 마지막 세그먼트(일반적으로 *stdout*)에 추가하여 작성됩니다. `stdoutLogFile` 경로가 *stdout*으로 끝나는 경우 2018년 2월 5일 19시 42분 32초에 만들어진 PID 1934를 사용하는 앱에 대한 로그의 파일 이름은 *stdout_20180205194132_1934.log*입니다.

다음 샘플 `aspNetCore` 요소는 Azure App Service에서 호스트되는 앱에 대한 stdout 로깅을 구성합니다. 로컬 로깅에는 로컬 경로 또는 네트워크 공유 경로가 허용됩니다. AppPool 사용자 ID에 제공된 경로에 쓸 수 있는 권한이 있는지 확인합니다.

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

*web.config* 파일에 있는 `aspNetCore` 요소의 예제에 대해서는 [web.config를 사용한 구성](#configuration-with-webconfig)을 참조하세요.

## <a name="proxy-configuration-uses-http-protocol-and-a-pairing-token"></a>프록시 구성은 HTTP 프로토콜 및 페어링 토큰을 사용합니다.

::: moniker range=">= aspnetcore-2.2"

*호스팅에만 적용됩니다.*

::: moniker-end

ASP.NET Core 모듈과 Kestrel 사이에 만들어진 프록시는 HTTP 프로토콜을 사용합니다. HTTP 사용은 모듈과 Kestrel 간의 트래픽이 네트워크 인터페이스에서 분리된 루프백 주소에서 발생하는 성능 최적화입니다. 서버에서 분리된 위치에서 모듈과 Kestrel 간 트래픽 도청의 위험은 없습니다.

페어링 토큰은 Kestrel에서 받은 요청이 IIS에서 프록시되었으며 다른 원본에서 오지 않았다는 것을 보장하는 데 사용됩니다. 페어링 토큰은 모듈에 의해 생성되며 환경 변수(`ASPNETCORE_TOKEN`)로 설정됩니다. 페어링 토큰은 프록시된 모든 요청에서 헤더(`MSAspNetCoreToken`)로도 설정됩니다. IIS 미들웨어는 수신하는 각 요청을 검사하여 페어링 토큰 헤더 값이 환경 변수 값과 일치하는지 확인합니다. 토큰 값이 일치하지 않는 경우 요청이 기록되고 거부됩니다. 페어링 토큰 환경 변수와 모듈과 Kestrel 간의 트래픽은 서버에서 분리된 위치에서 액세스할 수 없습니다. 페어링 토큰 값을 알지 못하면 공격자는 IIS 미들웨어에서 검사를 무시하는 요청을 전송할 수 없습니다.

## <a name="aspnet-core-module-with-an-iis-shared-configuration"></a>IIS 공유 구성이 포함된 ASP.NET Core 모듈

ASP.NET Core 모듈 설치 관리자는 **SYSTEM** 계정의 권한으로 실행됩니다. 로컬 시스템 계정에는 IIS 공유 구성에서 사용하는 공유 경로에 대한 수정 권한이 없으므로 공유의 *applicationHost.config*에서 모듈 설정을 구성하려고 하면 설치 관리자에서 액세스 거부 오류가 발생합니다. IIS 공유 구성을 사용할 경우 다음 단계를 수행합니다.

1. IIS 공유 구성을 사용하지 않도록 설정합니다.
1. 설치 관리자를 실행합니다.
1. 업데이트된 *applicationHost.config* 파일을 공유로 내보냅니다.
1. IIS 공유 구성을 다시 사용하도록 설정합니다.

## <a name="module-version-and-hosting-bundle-installer-logs"></a>모듈 버전 및 호스팅 번들 설치 관리자 로그

설치된 ASP.NET Core 모듈의 버전을 확인하려면:

1. 호스팅 시스템에서 *%windir%\System32\inetsrv*로 이동합니다.
1. *aspnetcore.dll* 파일을 찾습니다.
1. 파일을 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **속성**을 선택합니다.
1. **세부 정보** 탭을 선택합니다. **파일 버전** 및 **제품 버전**은 설치된 모듈 버전을 나타냅니다.

모듈에 대한 호스팅 번들 설치 관리자 로그는 *C:\\Users\\%UserName%\\AppData\\Local\\Temp*에 있습니다. 파일 이름은 *dd_DotNetCoreWinSvrHosting__\<timestamp>_000_AspNetCoreModule_x64.log*로 지정됩니다.

## <a name="module-schema-and-configuration-file-locations"></a>모듈, 스키마 및 구성 파일 위치

### <a name="module"></a>Module

**IIS(x86/amd64):**

   * %windir%\System32\inetsrv\aspnetcore.dll

   * %windir%\SysWOW64\inetsrv\aspnetcore.dll

**IIS Express(x86/amd64):**

   * %ProgramFiles%\IIS Express\aspnetcore.dll

   * %ProgramFiles(x86)%\IIS Express\aspnetcore.dll

### <a name="schema"></a>스키마

**IIS**

   * %windir%\System32\inetsrv\config\schema\aspnetcore_schema.xml

**IIS Express**

   * %ProgramFiles%\IIS Express\config\schema\aspnetcore_schema.xml

### <a name="configuration"></a>구성

**IIS**

   * %windir%\System32\inetsrv\config\applicationHost.config

**IIS Express**

   * .vs\config\applicationHost.config

*applicationHost.config* 파일에서 *aspnetcore.dll*을 검색하여 파일을 찾을 수 있습니다. IIS Express의 경우 기본적으로 *applicationHost.config* 파일이 없습니다. Visual Studio 솔루션에서 웹앱 프로젝트를 시작할 때 *\<application_root>\\.vs\\config*에 파일이 만들어집니다.
