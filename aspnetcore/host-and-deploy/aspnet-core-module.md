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
# <a name="aspnet-core-module-configuration-reference"></a>ASP.NET Core 모듈 구성 참조

여 [Luke Latham](https://github.com/guardrex), [Rick Anderson](https://twitter.com/RickAndMSFT), 및 [Sourabh Shirhatti](https://twitter.com/sshirhatti)

이 문서는 ASP.NET Core 응용 프로그램을 호스팅하기 위한 ASP.NET Core 모듈을 구성 하는 방법에 지침을 제공 합니다. ASP.NET Core 모듈 및 설치 지침에 대 한 소개를 참조 하십시오.는 [ASP.NET Core 모듈 개요](xref:fundamentals/servers/aspnet-core-module)합니다.

## <a name="configuration-with-webconfig"></a>Web.config 구성

ASP.NET Core 모듈 구성 된는 `aspNetCore` 의 섹션은 `system.webServer` 노드 사이트의 *web.config* 파일입니다.

다음 *web.config* 파일이 게시 되는 [프레임 워크 종속 배포](/dotnet/articles/core/deploying/#framework-dependent-deployments-fdd) 사이트 요청을 처리 하도록 ASP.NET Core 모듈을 구성 하 고:

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

다음 *web.config* 에 대 한 게시는 [자체 포함된 배포](/dotnet/articles/core/deploying/#self-contained-deployments-scd):

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

응용 프로그램에 배포 되는 경우 [Azure 앱 서비스](https://azure.microsoft.com/services/app-service/), `stdoutLogFile` 경로가 설정 되었는지 `\\?\%home%\LogFiles\stdout`합니다. Stdout 로그를 저장 하는 경로 *LogFiles* 폴더에 위치를 자동으로 서비스에 의해 만들어진 합니다.

참조 [하위 응용 프로그램 구성](xref:host-and-deploy/iis/index#sub-application-configuration) 의 구성에 관련 된 중요 정보에 대 한 *web.config* 하위 앱의 파일입니다.

### <a name="attributes-of-the-aspnetcore-element"></a>AspNetCore 요소의 특성입니다.

| 특성 | 설명 | 기본 |
| --------- | ----------- | :-----: |
| `arguments` | <p>선택적 문자열 특성입니다.</p><p>에 지정 된 실행 파일에 대 한 인수 **processPath**합니다.</p>| |
| `disableStartUpErrorPage` | 참 또는 거짓입니다.</p><p>True 이면는 **502.5-프로세스 오류** 페이지는 표시 되지 않으며 502 상태 코드 페이지에 구성 된는 *web.config* 우선적으로 적용 합니다.</p> | `false` |
| `forwardWindowsAuthToken` | 참 또는 거짓입니다.</p><p>True 이면 토큰 요청당 헤더로 ' MS ASPNETCORE WINAUTHTOKEN' % ASPNETCORE_PORT %에서 수신 하는 자식 프로세스에 전달 됩니다. 것은 해당 프로세스를 요청에 따라이 토큰에 CloseHandle 호출의 책임입니다.</p> | `true` |
| `processPath` | <p>필수 문자열 특성입니다.</p><p>HTTP 요청을 수신 하는 프로세스를 시작 하는 실행 파일 경로입니다. 상대 경로 지원 합니다. 로 시작 하는 경로 경우 `.`, 경로 사이트 루트 기준 것으로 간주 됩니다.</p> | |
| `rapidFailsPerMinute` | <p>선택적 정수 특성입니다.</p><p>에 지정 된 프로세스의 수를 지정 **processPath** 분당 충돌을 허용 합니다. 이 제한을 초과 하는 나머지 분에서 프로세스 시작 모듈을 중지 합니다.</p> | `10` |
| `requestTimeout` | <p>선택적 timespan 특성입니다.</p><p>ASP.NET Core 모듈 ASPNETCORE_PORT % %를 수신 하는 프로세스에서 응답에 대 한 대기 기간을 지정 합니다.</p><p>`requestTimeout` 지정 해야이 분 단위로, 그렇지 않으면 기본적으로 2 분입니다.</p> | `00:02:00` |
| `shutdownTimeLimit` | <p>선택적 정수 특성입니다.</p><p>기간 (초)를 정상적으로 종료 실행 파일에 대 한 모듈에서 대기 하는 경우는 *app_offline.htm* 파일이 검색 될 합니다.</p> | `10` |
| `startupTimeLimit` | <p>선택적 정수 특성입니다.</p><p>포트에서 수신 하는 프로세스가 시작 되는 파일에 대 한 모듈에서 대기 하는 시간 (초) 기간입니다. 이 시간 제한을 초과 하는 모듈에서 프로세스를 중단 합니다. 모듈에서 새 요청을 수신 하 고 앱이 시작 되지 않는 한 이후 들어오는 요청에서 프로세스를 다시 시작 하려고 계속 경우 프로세스를 다시 시작 하려고 **rapidFailsPerMinute** 지난에서 번 롤링 분입니다.</p> | `120` |
| `stdoutLogEnabled` | <p>선택적 부울 특성입니다.</p><p>True 이면 **stdout** 및 **stderr** 에 지정 된 프로세스에 대 한 **processPath** 는에 지정 된 파일로 리디렉션할 **가 stdoutLogFile**합니다.</p> | `false` |
| `stdoutLogFile` | <p>선택적 문자열 특성입니다.</p><p>상대 또는 절대 파일 경로를 지정 **stdout** 및 **stderr** 에 지정 된 프로세스에서 **processPath** 기록 됩니다. 상대 경로 사이트의 루트를 기준으로 합니다. 로 시작 하는 경로 `.` 은 절대 경로로 루트 및 다른 모든 경로 사이트에 상대적인 처리 합니다. 모든 폴더 경로에 제공 된 로그 파일을 만들 모듈에 대 한 순서에 있어야 합니다. 밑줄 구분 기호, 타임 스탬프, 프로세스 ID 및 파일 확장명을 사용 하 여 (*.log*) 세그먼트의 마지막으로 추가 된 **가 stdoutLogFile** 경로입니다. 경우 `.\logs\stdout` 제공 예제 stdout 로그로 저장 된 값으로 *stdout_20180205194132_1934.log* 에 *로그* 19시 41분: 32 1934의 프로세스 id는 2/5/2018에 저장할 경우 폴더입니다.</p> | `aspnetcore-stdout` |

### <a name="setting-environment-variables"></a>환경 변수 설정

프로세스에 대 한 환경 변수를 지정할 수 있습니다는 `processPath` 특성입니다. 지정 된 환경 변수는 `environmentVariable` 의 자식 요소는 `environmentVariables` 컬렉션 요소입니다. 이 섹션에 설정 된 환경 변수 보다 우선 적용 시스템 환경 변수.

다음 예제에서는 두 개의 환경 변수를 설정합니다. `ASPNETCORE_ENVIRONMENT` 앱의 환경을 구성 `Development`합니다. 개발자에 일시적으로이 값을 설정할 수 있습니다는 *web.config* 강제 파일은 [개발자 예외 페이지](xref:fundamentals/error-handling) 를 응용 프로그램 예외를 디버깅 하는 경우 로드 합니다. `CONFIG_DIR` 한 예로, 사용자 정의 환경 변수 개발자 시작할 응용 프로그램의 구성 파일을 로드 하는 것에 대 한 경로를 구성할 때 값을 읽을 수 있는 코드를 기록 했습니다.

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
> 에 설정는 `ASPNETCORE_ENVIRONMENT` envirnonment 변수를 `Development` 준비 하 고 테스트 인터넷과 같은 신뢰할 수 없는 네트워크에 액세스할 수 없는 서버에 있습니다.

## <a name="appofflinehtm"></a>app_offline.htm

이름 가진 파일이 있으면 *app_offline.htm* 응용 프로그램의 루트 디렉터리에서 검색 된 앱 및 들어오는 요청을 처리 하는 중지 ASP.NET Core 모듈 정상 종료 하려고 합니다. 응용 프로그램에 정의 된 시간 (초)이 지나면 여전히 실행 중인 경우 `shutdownTimeLimit`, ASP.NET Core 모듈에서 실행 중인 프로세스를 중단 합니다.

반면는 *app_offline.htm* 파일이 없으면 ASP.NET Core 모듈 요청에 응답의 내용을 다시 전송 하 여는 *app_offline.htm* 파일입니다. 경우는 *app_offline.htm* 다음 요청 응용 프로그램이 시작, 파일은 제거 됩니다.

## <a name="start-up-error-page"></a>시작 오류 페이지

ASP.NET Core 모듈을 백 엔드 프로세스 또는 백 엔드 프로세스 시작 하지만 구성된 된 포트에서 수신 하도록 실패를 시작할 수 없는 경우는 *502.5 프로세스 오류* 상태 코드 페이지가 나타납니다. 이 페이지를 표시 하지 않는 하 여 기본 IIS 502 상태 코드 페이지로 되돌리려면 사용은 `disableStartUpErrorPage` 특성입니다. 사용자 정의 오류 메시지를 구성 하는 방법에 대 한 자세한 내용은 참조 하십시오. [HTTP 오류 `<httpErrors>` ](/iis/configuration/system.webServer/httpErrors/)합니다.

![502.5 프로세스 오류 상태 코드 페이지](aspnet-core-module/_static/ANCM-502_5.png)

## <a name="log-creation-and-redirection"></a>로그 만들기 및 리디렉션

ASP.NET Core 모듈 리디렉션합니다 `stdout` 및 `stderr` 로그 디스크에 `stdoutLogEnabled` 및 `stdoutLogFile` 의 특성은 `aspNetCore` 요소 설정 됩니다. 에 있는 폴더는 `stdoutLogFile` 경로 로그 파일을 만들 모듈에 대 한 순서에 존재 해야 합니다. 타임 스탬프 및 파일 확장명은 로그 파일을 만들 때 자동으로 추가 됩니다. 프로세스 재활용/를 다시 시작이 발생 하지 않으면 로그가 회전 되지 않습니다. 것은 로그 사용할 디스크 공간을 제한 하는 호스팅 서비스 공급자의 책임입니다. 사용 하는 `stdout` 로그 응용 프로그램 시작 문제 해결에 권장 됩니다. 일반 응용 프로그램 로깅 목적 stdout 로그를 사용 하지 마십시오. ASP.NET Core 응용 프로그램의 일상적인 로깅에 대 한 로그 파일 크기를 제한 하 고 로그를 회전 하는 로깅 라이브러리를 사용 합니다. 자세한 내용은 참조 [제 3 자 로깅 공급자](xref:fundamentals/logging/index#third-party-logging-providers)합니다.

타임 스탬프, 프로세스 ID 및 파일 확장명을 추가 하 여 로그 파일 이름이 구성 됩니다 (*.log*)의 마지막 세그먼트에는 `stdoutLogFile` 경로 (일반적으로 *stdout*) 밑줄로 구분 합니다. 경우는 `stdoutLogFile` 로 끝나는 경로 *stdout*, 19시 42분: 32에서 2/5/2018에서 만든 1934의 PID 사용 하 여 앱에 대 한 로그 파일 이름이 *stdout_20180205194132_1934.log*합니다.

다음 샘플 `aspNetCore` 요소 구성 `stdout` Azure 앱 서비스에서 호스팅되는 앱에 대 한 로깅을 합니다. 로컬 경로 또는 네트워크 공유 경로 로컬 로깅 있습니다. AppPool 사용자 id 제공 된 경로에 쓸 수 있는 권한이 있는지 확인 합니다.

```xml
<aspNetCore processPath="dotnet"
    arguments=".\MyApp.dll"
    stdoutLogEnabled="true"
    stdoutLogFile="\\?\%home%\LogFiles\stdout">
</aspNetCore>
```

참조 [web.config 사용 하 여 구성을](#configuration-with-webconfig) 의 예는 `aspNetCore` 요소에는 *web.config* 파일입니다.

## <a name="aspnet-core-module-with-an-iis-shared-configuration"></a>IIS 사용 하 여 ASP.NET Core 모듈 구성 공유

ASP.NET Core 모듈 설치 관리자의 권한으로 실행 되는 **시스템** 계정. 설치 관리자가 액세스 거부 오류가에서 모듈 설정을 구성 하는 동안 로컬 시스템 계정에서 IIS 공유 구성을 사용 하는 공유 경로 대 한 권한을 수정 하지 않습니다, 때문에 *applicationHost.config* 공유에 있습니다. IIS 공유 구성을 사용 하는 경우 다음이 단계를 따르십시오.

1. IIS 공유 구성을 사용 하지 않도록 설정 합니다.
1. 설치 관리자를 실행합니다.
1. 업데이트 된 내보내기 *applicationHost.config* 파일을 공유 합니다.
1. IIS 공유 구성을 다시 설정 합니다.

## <a name="module-version-and-hosting-bundle-installer-logs"></a>모듈의 버전 및 번들 설치 관리자 로그를 호스팅

확인 하려면 설치 된 ASP.NET Core 모듈 버전:

1. 호스팅 시스템에서로 이동 *%windir%\System32\inetsrv*합니다.
1. 찾을 *aspnetcore.dll* 파일입니다.
1. 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 **속성** 상황에 맞는 메뉴에서 합니다.
1. 선택 된 **세부 정보** 탭 합니다. **파일 버전** 및 **제품 버전** 모듈의 설치 된 버전을 나타냅니다.

모듈에 대 한 Windows 서버 호스팅 번들 설치 관리자 로그에서 발견 되 *c:\\사용자\\% UserName %\\AppData\\로컬\\Temp*합니다. 파일의 이름은 *dd_DotNetCoreWinSvrHosting__\<타임 스탬프 > _000_AspNetCoreModule_x64.log*합니다.

## <a name="module-schema-and-configuration-file-locations"></a>모듈, 스키마 및 구성 파일 위치

### <a name="module"></a>Module

**IIS (x86/amd64):**

   * %windir%\System32\inetsrv\aspnetcore.dll

   * %windir%\SysWOW64\inetsrv\aspnetcore.dll

**IIS Express (x86/amd64):**

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

검색 하 여 파일을 찾을 수 *aspnetcore.dll* 에 *applicationHost.config* 파일입니다. IIS express는 *applicationHost.config* 파일은 기본적으로 존재 하지 않습니다. 파일을 만들  *\<application_root >\\.vs\\config* 때 Visual Studio 솔루션에서 모든 웹 응용 프로그램 프로젝트를 시작 합니다.
