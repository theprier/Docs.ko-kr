---
title: IIS에서 ASP.NET Core 문제 해결
author: guardrex
description: ASP.NET Core 응용 프로그램의 인터넷 정보 서비스 (IIS) 배포와 문제를 진단 하는 방법을 알아봅니다.
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 02/07/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/iis/troubleshoot
ms.openlocfilehash: e44892d2022ca1a176cee9d027e220e196c6572d
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="troubleshoot-aspnet-core-on-iis"></a>IIS에서 ASP.NET Core 문제 해결

[Luke Latham](https://github.com/guardrex)으로

이 문서에서는 설명 ASP.NET Core를 진단 하는 방법에 응용 프로그램 시작 문제를 호스트 하는 경우 [인터넷 정보 서비스 (IIS)](/iis)합니다. 이 문서의 정보는 Windows Server 및 Windows 바탕 화면에는 IIS에서 호스팅에 적용 됩니다.

Visual Studio에서 ASP.NET Core 프로젝트 기본값은 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) 디버깅 하는 동안 호스팅. A *502.5 프로세스 오류* 로컬로 troubleshooted 권장 하는이 항목의 사용 될 수 있습니다 디버깅 하는 경우 발생 하 합니다.

추가 문제 해결 항목:

[Azure App Service에서 ASP.NET Core 문제 해결](xref:host-and-deploy/azure-apps/troubleshoot)  
앱 서비스를 사용 하지는 않지만 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module) 및 호스트 응용 프로그램에는 IIS 응용 프로그램 서비스와 관련 된 지침에 대 한 전용된 항목을 참조 하십시오.

[오류 처리](xref:fundamentals/error-handling)  
로컬 시스템에서 개발 하는 동안 ASP.NET Core 응용 프로그램에서 오류를 처리 하는 방법을 알아봅니다.

[Visual Studio를 사용하여 디버깅하는 자세한 내용](/visualstudio/debugger/getting-started-with-the-debugger)  
이 항목에서는 Visual Studio 디버거 기능을 소개 합니다.

## <a name="app-startup-errors"></a>응용 프로그램 시작 오류

**502.5 프로세스 오류**  
작업자 프로세스가 실패합니다. 응용 프로그램을 시작 하지 않습니다.

ASP.NET Core 모듈 작업자 프로세스를 시작 하려고 시도 하지만 시작 하지 못한 합니다. 프로세스 시작 실패의 원인을 일반적으로 항목에서 확인할 수 있습니다는 [응용 프로그램 이벤트 로그](#application-event-log) 및 [ASP.NET Core 모듈 stdout 로그](#aspnet-core-module-stdout-log)합니다.

*502.5 프로세스 오류* 호스팅 또는 응용 프로그램 구성이 잘못 작업자 프로세스가 실패 하면 오류 페이지가 반환 됩니다.

![브라우저 창에 502.5 프로세스 오류 페이지를 표시 합니다.](troubleshoot/_static/process-failure-page.png)

**500 내부 서버 오류**  
응용 프로그램 시작 하지만 오류는 서버에서 요청을 수행할 수행할 수 없습니다.

시작 하는 동안 또는 응답을 만드는 동안 응용 프로그램의 코드 내에서이 오류가 발생 합니다. 응답 없는 콘텐츠를 포함할 수 또는 응답으로 나타날 수 있습니다는 *500 내부 서버 오류* 브라우저에서 합니다. 응용 프로그램 이벤트 로그는 일반적으로 응용 프로그램이 정상적으로 시작 상태입니다. 서버의 관점에서는 사실입니다. 응용 프로그램 시작 않았습니다 하지만 유효한 응답을 생성할 수 없습니다. [명령 프롬프트에서 앱 실행](#run-the-app-at-a-command-prompt) 서버의 또는 [ASP.NET Core 모듈 stdout 로그 사용](#aspnet-core-module-stdout-log) 문제를 해결 합니다.

**연결 다시 설정**

보낼 서버에 대 한 너무 늦을 때 헤더를 보낸 다음 오류가 발생 하는 경우는 **500 내부 서버 오류** 오류가 발생할 경우. 이 문제는 종종 복잡 한 개체에 대 한 응답을 직렬화 하는 동안 오류가 발생 하면 발생 합니다. 으로 이러한 종류의 오류 표시는 *연결 다시 설정* 클라이언트에 대 한 오류입니다. [응용 프로그램 로깅](xref:fundamentals/logging/index) 이러한 종류의 오류를 해결할 수 있습니다.

## <a name="default-startup-limits"></a>기본 시작 제한

ASP.NET Core 모듈 구성 된 기본 *startupTimeLimit* 120 초입니다. 기본값에 그대로 유지, 응용 프로그램 모듈 프로세스 오류를 기록 하기 전에 시작 하려면 최대 2 분 정도 걸릴 수 있습니다. 모듈 구성에 대 한 참조 [aspNetCore 요소의 특성](xref:host-and-deploy/aspnet-core-module#attributes-of-the-aspnetcore-element)합니다.

## <a name="troubleshoot-app-startup-errors"></a>응용 프로그램 시작 오류 문제 해결

### <a name="application-event-log"></a>응용 프로그램 이벤트 로그

응용 프로그램 이벤트 로그에 액세스 합니다.

1. 시작 메뉴를 열고, 검색할 **이벤트 뷰어**를 선택한 후는 **이벤트 뷰어** 응용 프로그램입니다.
1. **이벤트 뷰어**열고는 **Windows 로그** 노드.
1. 선택 **응용 프로그램** 를 응용 프로그램 이벤트 로그를 엽니다.
1. 실패 한 앱과 연결 된 오류에 대 한 검색입니다. 오류 값을 가질 *IIS AspNetCore 모듈* 또는 *IIS Express AspNetCore 모듈* 에 *소스* 열입니다.

### <a name="run-the-app-at-a-command-prompt"></a>명령 프롬프트에서 앱 실행

많은 시작 오류 응용 프로그램 이벤트 로그에서 유용한 정보를 생성 하지 않습니다. 호스팅 시스템에서 명령 프롬프트에서 앱을 실행 하 여 일부 오류 원인을 찾을 수 있습니다.

**프레임 워크 종속 배포**

하는 경우는 [프레임 워크 종속 배포](/dotnet/core/deploying/#framework-dependent-deployments-fdd):

1. 명령 프롬프트에서 배포 폴더로 이동 하 고 사용 하 여 응용 프로그램의 어셈블리를 실행 하 여 앱을 실행 *dotnet.exe*합니다. 다음 명령에서에 대 한 응용 프로그램의 어셈블리의 이름을 바꾸어야 \<assembly_name >: `dotnet .\<assembly_name>.dll`합니다.
1. 오류를 보여 주는 응용 프로그램에서 콘솔 출력은 콘솔 창에 기록 됩니다.
1. 응용 프로그램에 요청을 하는 경우는 오류가 발생 한 경우 호스트 및 Kestrel 수신 대기 포트에 요청을 수행 합니다. 요청을 수행 기본 호스트 및 게시를 사용 하 여 `http://localhost:5000/`합니다. 응용 프로그램 Kestrel 끝점 주소에서 정상적으로 응답을 하는 경우 문제가 관련 역방향 프록시 구성 및 응용 프로그램 내에서 될 가능성이 적기 가능성이 큽니다.

**자체 포함된 배포**

하는 경우는 [자체 포함된 배포](/dotnet/core/deploying/#self-contained-deployments-scd):

1. 명령 프롬프트에서 배포 폴더로 이동한 다음 응용 프로그램의 실행 파일을 실행 합니다. 다음 명령에서에 대 한 응용 프로그램의 어셈블리의 이름을 바꾸어야 \<assembly_name >: `<assembly_name>.exe`합니다.
1. 오류를 보여 주는 응용 프로그램에서 콘솔 출력은 콘솔 창에 기록 됩니다.
1. 응용 프로그램에 요청을 하는 경우는 오류가 발생 한 경우 호스트 및 Kestrel 수신 대기 포트에 요청을 수행 합니다. 요청을 수행 기본 호스트 및 게시를 사용 하 여 `http://localhost:5000/`합니다. 응용 프로그램 Kestrel 끝점 주소에서 정상적으로 응답을 하는 경우 문제가 관련 역방향 프록시 구성 및 응용 프로그램 내에서 될 가능성이 적기 가능성이 큽니다.

### <a name="aspnet-core-module-stdout-log"></a>ASP.NET Core 모듈 stdout 로그

사용 하도록 설정 하 고 stdout 로그를 확인 하십시오.

1. 호스팅 시스템에 표시 되는 사이트의 배포 폴더로 이동 합니다.
1. 경우는 *로그* 폴더 존재 하지, 폴더를 만듭니다. MSBuild를 사용 하도록 설정 하는 방법에 만드는 지침은 *로그* 폴더 배포에서 자동으로 참조는 [디렉터리 구조](xref:host-and-deploy/directory-structure) 항목입니다.
1. 편집 된 *web.config* 파일입니다. 설정 **stdoutLogEnabled** 를 `true` 변경 하 고는 **가 stdoutLogFile** 가리키도록 경로 *로그* 폴더 (예를 들어 `.\logs\stdout`). `stdout` 경로에 로그 파일 이름 접두사입니다. 로그를 만들 때 타임 스탬프, 프로세스 id 및 파일 확장명이 자동으로 추가 됩니다. 사용 하 여 `stdout` 일반적인 로그 파일의 이름은 파일 이름 접두사로 *stdout_20180205184032_5412.log*합니다. 
1. 업데이트 된 저장 *web.config* 파일입니다.
1. 응용 프로그램에 요청을 수행 합니다.
1. 탐색 하 고 *로그* 폴더입니다. 찾기 및 가장 최근의 stdout 로그를 엽니다.
1. 로그에서 오류를 조사 합니다.

**중요!** Stdout 문제 해결이 완료 될 때의 로깅이 사용 안 함

1. 편집 된 *web.config* 파일입니다.
1. 설정 **stdoutLogEnabled** 를 `false`합니다.
1. 파일을 저장합니다.

> [!WARNING]
> Stdout 로그를 사용 하지 않도록 설정 하지 않으면 응용 프로그램 또는 서버 오류가 발생할 수 있습니다. 로그 파일 크기 또는 생성되는 로그 파일 수에 대한 제한은 없습니다.
>
> ASP.NET Core 응용 프로그램의 일상적인 로깅에 대 한 로그 파일 크기를 제한 하 고 로그를 회전 하는 로깅 라이브러리를 사용 합니다. 자세한 내용은 참조 [제 3 자 로깅 공급자](xref:fundamentals/logging/index#third-party-logging-providers)합니다.

## <a name="enabling-the-developer-exception-page"></a>개발자 예외 페이지를 사용 하도록 설정

`ASPNETCORE_ENVIRONMENT` [web.config에 환경 변수를 추가할 수 있습니다](xref:host-and-deploy/aspnet-core-module#setting-environment-variables) 개발 환경에서 응용 프로그램을 실행 합니다. 으로 환경에서 응용 프로그램 시작에서 재정의 되지 않습니다 `UseEnvironment` 호스트 작성기 허용 환경 변수를 설정의 [개발자 예외 페이지](xref:fundamentals/error-handling) 표시할 때 앱이 실행 합니다.

```xml
<aspNetCore processPath="dotnet"
      arguments=".\MyApp.dll"
      stdoutLogEnabled="false"
      stdoutLogFile=".\logs\stdout">
  <environmentVariables>
    <environmentVariable name="ASPNETCORE_ENVIRONMENT" value="Development" />
  </environmentVariables>
</aspNetCore>
```

에 대 한 환경 변수를 설정 `ASPNETCORE_ENVIRONMENT` 준비 하 고 테스트 하는 인터넷에 노출 되지 않습니다는 서버에서 사용 하기 위해만 권장 됩니다. 환경 변수를 제거는 *web.config* 문제 해결 후 파일입니다. 환경 변수 설정에 대 한 내용은 *web.config*, 참조 [aspNetCore의 자식 요소 environmentVariables](xref:host-and-deploy/aspnet-core-module#setting-environment-variables)합니다.

## <a name="common-startup-errors"></a>일반적인 시작 오류 

참조는 [ASP.NET Core 오류 통칭](xref:host-and-deploy/azure-iis-errors-reference)합니다. 대부분의 응용 프로그램 시작을 방해 하는 일반적인 문제는 참조 항목에서 다룹니다.

## <a name="slow-or-hanging-app"></a>느린 되거나 응용 프로그램

앱 느리게 응답 하거나 요청에 응답 하지를 구하여 분석는 [덤프 파일](/visualstudio/debugger/using-dump-files)합니다. 다음 도구 중 하나를 사용 하 여 덤프 파일을 가져올 수 있습니다.

* [ProcDump](/sysinternals/downloads/procdump)
* [DebugDiag](https://www.microsoft.com/download/details.aspx?id=49924)
* WinDbg: [Windows 용 디버깅 도구를 다운로드](https://developer.microsoft.com/windows/hardware/download-windbg), [를 사용 하 여 WinDbg 디버깅](/windows-hardware/drivers/debugger/debugging-using-windbg)

## <a name="remote-debugging"></a>원격 디버깅

참조 [Visual Studio 2017에 원격 IIS 컴퓨터에 있는 원격 디버깅 ASP.NET Core](/visualstudio/debugger/remote-debugging-aspnet-on-a-remote-iis-computer) Visual Studio 설명서에 있습니다.

## <a name="application-insights"></a>응용 프로그램 정보

[Application Insights](/azure/application-insights/) 오류 로깅 및 보고 기능을 포함 하 여 IIS에서 호스트 되는 앱에서 원격 분석을 제공 합니다. Application Insights에서 응용 프로그램의 로깅 기능을 사용할 수 있게 하는 경우 응용 프로그램에서 시작 된 이후에 발생 하는 오류만 보고할 수 있습니다. 자세한 내용은 참조 [ASP.NET Core 용 Application Insights](/azure/application-insights/app-insights-asp-net-core)합니다.

## <a name="additional-troubleshooting-advice"></a>추가 문제 해결 도움말 제공

경우에 따라 작동 중인 응용 프로그램 중 하나가.NET Core SDK 앱 내에서 개발 컴퓨터 또는 패키지 버전에서 업그레이드 한 후에 즉시 실패 합니다. 경우에 따라 중요한 업그레이드를 수행할 때 일관되지 않은 패키지로 인해 응용 프로그램이 중단될 수 있습니다. 다음과 같은이 방법으로 이러한 문제를 대부분 해결할 수 있습니다:

1. 삭제 된 *bin* 및 *obj* 폴더입니다.
1. 패키지에서 캐시 지우기 *% UserProfile %\\.nuget\\패키지* 및 *% LocalAppData %\\Nuget\\v3 캐시*합니다.
1. 복원 하 고 프로젝트를 다시 빌드하십시오.
1. 서버에서 이전 배포 응용 프로그램을 다시 배포 하기 전에 완전히 삭제 되었는지 확인 합니다.

> [!TIP]
> 패키지 캐시의 선택을 취소 하는 편리한 방법을 실행 하는 것 `dotnet nuget locals all --clear` 명령 프롬프트에서 합니다.
> 
> 패키지 캐시를 지우기 수행할 수도 있습니다를 사용 하 여는 [nuget.exe](https://www.nuget.org/downloads) 도구 및 명령 실행 `nuget locals all -clear`합니다. *nuget.exe* Windows 데스크톱 운영 체제에 설치를 번들로 묶은 아니고에서 별도로 구입 해야는 [NuGet 웹 사이트](https://www.nuget.org/downloads)합니다.

## <a name="additional-resources"></a>추가 자료

* [ASP.NET Core의 오류 처리 소개](xref:fundamentals/error-handling)
* [ASP.NET Core를 사용하는 Azure App Service 및 IIS에 대한 일반적인 오류 참조](xref:host-and-deploy/azure-iis-errors-reference)
* [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module)
* [Azure App Service에서 ASP.NET Core 문제 해결](xref:host-and-deploy/azure-apps/troubleshoot)
