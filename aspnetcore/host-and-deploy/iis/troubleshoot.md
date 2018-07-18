---
title: IIS에서 ASP.NET Core 문제 해결
author: guardrex
description: ASP.NET Core 앱의 IIS(인터넷 정보 서비스) 배포에 대한 문제 진단 방법을 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 02/07/2018
uid: host-and-deploy/iis/troubleshoot
ms.openlocfilehash: cbbdee6849768004476d94c58be4a0e7cc2d6f9e
ms.sourcegitcommit: 661d30492d5ef7bbca4f7e709f40d8f3309d2dac
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2018
ms.locfileid: "37938474"
---
# <a name="troubleshoot-aspnet-core-on-iis"></a>IIS에서 ASP.NET Core 문제 해결

[Luke Latham](https://github.com/guardrex)으로

이 문서에서는 [IIS(인터넷 정보 서비스)](/iis)를 통해 호스트할 경우 ASP.NET Core 앱 시작 문제를 진단하는 방법에 대한 지침을 제공합니다. 이 문서의 정보는 Windows Server 및 Windows 데스크톱의 IIS에서 호스트하는 경우에 적용됩니다.

Visual Studio에서 ASP.NET Core 프로젝트는 기본적으로 디버그 중에 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) 호스팅으로 설정됩니다. 로컬에서 디버그할 때 발생하는 *502.5 프로세스 실패*는 이 항목의 권장 사항을 사용하여 해결할 수 있습니다.

추가 문제 해결 항목:

[Azure App Service에서 ASP.NET Core 문제 해결](xref:host-and-deploy/azure-apps/troubleshoot)  
App Service는 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)과 IIS를 사용하여 앱을 호스트하지만 App Service 관련 지침은 전용 항목을 참조하세요.

[오류 처리](xref:fundamentals/error-handling)  
로컬 시스템에서 개발하는 동안 ASP.NET Core 앱에서 오류를 처리하는 방법을 알아봅니다.

[Visual Studio를 사용하여 디버깅하는 자세한 내용](/visualstudio/debugger/getting-started-with-the-debugger)  
이 항목에서는 Visual Studio 디버거의 기능을 소개합니다.

[Debugging with Visual Studio Code](https://code.visualstudio.com/docs/editor/debugging)(Visual Studio Code를 사용한 디버깅)  
Visual Studio Code에 기본 제공되는 디버깅 지원에 대해 알아봅니다.

## <a name="app-startup-errors"></a>앱 시작 오류

**502.5 프로세스 실패**  
작업자 프로세스가 실패합니다. 앱이 시작되지 않습니다.

ASP.NET Core 모듈이 작업자 프로세스를 시작하려고 하지만 시작할 수 없습니다. 프로세스 시작 실패의 원인은 일반적으로 [응용 프로그램 이벤트 로그](#application-event-log) 및 [ASP.NET Core 모듈 stdout 로그](#aspnet-core-module-stdout-log)의 항목에서 확인할 수 있습니다.

호스팅 또는 앱의 잘못된 구성으로 인해 작업자 프로세스가 실패하면 ‘502.5 프로세스 실패’ 오류 페이지가 반환됩니다.

![502.5 프로세스 실패 페이지를 보여주는 브라우저 창](troubleshoot/_static/process-failure-page.png)

**500 내부 서버 오류**  
앱이 시작되지만 오류로 인해 서버에서 요청을 처리할 수 없습니다.

이 오류는 시작하는 동안 또는 응답을 만드는 동안 앱 코드 내에서 발생합니다. 응답에 콘텐츠가 없거나 응답이 브라우저에 ‘500 내부 서버 오류’로 표시될 수 있습니다. 응용 프로그램 이벤트 로그는 일반적으로 앱이 정상적으로 시작되었음을 나타냅니다. 서버의 관점에서 보면 맞습니다. 앱이 시작되었지만 유효한 응답을 생성할 수 없습니다. 서버의 [명령 프롬프트에서 앱을 실행](#run-the-app-at-a-command-prompt)하거나 [ASP.NET Core 모듈 stdout 로그를 사용](#aspnet-core-module-stdout-log)하여 문제를 해결합니다.

**연결 다시 설정**

헤더가 전송된 후 오류가 발생할 경우, 오류가 발생할 때 서버에서 **500 내부 서버 오류**를 전송하는 것은 너무 늦은 것입니다. 응답에 대한 복잡한 개체의 serialization 중에 오류가 발생할 때 이 문제가 종종 발생합니다. 이 유형의 오류는 클라이언트에서 ‘연결 다시 설정’ 오류로 나타납니다. [응용 프로그램 로깅](xref:fundamentals/logging/index)은 이러한 유형의 오류를 해결하는 데 도움이 될 수 있습니다.

## <a name="default-startup-limits"></a>기본 시작 제한

ASP.NET Core 모듈은 기본 *startupTimeLimit*이 120초로 구성됩니다. 기본값으로 남아 있으면 앱에서 모듈이 프로세스 실패를 기록하기 전에 시작하는 데 최대 2분이 걸릴 수 있습니다. 모듈 구성에 대한 자세한 내용은 [aspNetCore 요소의 특성](xref:host-and-deploy/aspnet-core-module#attributes-of-the-aspnetcore-element)을 참조하세요.

## <a name="troubleshoot-app-startup-errors"></a>앱 시작 오류 해결

### <a name="application-event-log"></a>응용 프로그램 이벤트 로그

응용 프로그램 이벤트 로그에 액세스합니다.

1. [시작] 메뉴를 열고 **이벤트 뷰어**를 검색한 다음, **이벤트 뷰어** 앱을 선택합니다.
1. **이벤트 뷰어**에서 **Windows 로그** 노드를 엽니다.
1. **응용 프로그램**을 선택하여 응용 프로그램 이벤트 로그를 엽니다.
1. 실패한 앱과 연결된 오류를 검색합니다. 오류는 ‘소스’ 열에서 ‘IIS AspNetCore 모듈’ 또는 ‘IIS Express AspNetCore 모듈’의 값을 포함합니다.

### <a name="run-the-app-at-a-command-prompt"></a>명령 프롬프트에서 앱 실행

응용 프로그램 이벤트 로그에서 대부분의 시작 오류는 유용한 정보를 생성하지 않습니다. 호스팅 시스템의 명령 프롬프트에서 앱을 실행하여 일부 오류의 원인을 찾을 수 있습니다.

**프레임워크 종속 배포**

앱이 [프레임워크 종속 배포](/dotnet/core/deploying/#framework-dependent-deployments-fdd)인 경우:

1. 명령 프롬프트에서 배포 폴더로 이동하고 *dotnet.exe*로 앱의 어셈블리를 실행하여 앱을 실행합니다. `dotnet .\<assembly_name>.dll` 명령에서 \<assembly_name>을 앱 어셈블리의 이름으로 대체합니다.
1. 오류를 표시하는 앱의 콘솔 출력이 콘솔 창에 기록됩니다.
1. 앱에 대한 요청을 실행할 때 오류가 발생하는 경우에는 Kestrel이 수신 대기하는 호스트 및 포트에 대한 요청을 실행합니다. 기본 호스트 및 게시를 사용하여 `http://localhost:5000/`에 대한 요청을 실행합니다. 앱이 Kestrel 끝점 주소에서 정상적으로 응답하는 경우, 문제는 역방향 프록시 구성과 관련이 있으며 앱 내에서 관련되었을 가능성은 작습니다.

**자체 포함 배포**

앱이 [자체 포함 배포](/dotnet/core/deploying/#self-contained-deployments-scd)인 경우:

1. 명령 프롬프트에서 배포 폴더로 이동하고 앱의 실행 파일을 실행합니다. `<assembly_name>.exe` 명령에서 \<assembly_name>을 앱 어셈블리의 이름으로 대체합니다.
1. 오류를 표시하는 앱의 콘솔 출력이 콘솔 창에 기록됩니다.
1. 앱에 대한 요청을 실행할 때 오류가 발생하는 경우에는 Kestrel이 수신 대기하는 호스트 및 포트에 대한 요청을 실행합니다. 기본 호스트 및 게시를 사용하여 `http://localhost:5000/`에 대한 요청을 실행합니다. 앱이 Kestrel 끝점 주소에서 정상적으로 응답하는 경우, 문제는 역방향 프록시 구성과 관련이 있으며 앱 내에서 관련되었을 가능성은 작습니다.

### <a name="aspnet-core-module-stdout-log"></a>ASP.NET Core 모듈 stdout 로그

stdout 로그를 사용하고 보려면:

1. 호스팅 시스템에서 사이트의 배포 폴더로 이동합니다.
1. *logs* 폴더가 없으면 폴더를 만듭니다. MSBuild를 사용하여 배포에서 *logs* 폴더를 자동으로 만드는 방법에 대한 지침은 [디렉터리 구조](xref:host-and-deploy/directory-structure) 항목을 참조하세요.
1. *web.config* 파일을 편집합니다. **stdoutLogEnabled**를 `true`로 설정하고 **stdoutLogFile** 경로가 *logs* 폴더를 가리키도록 변경합니다(예: `.\logs\stdout`). 경로의 `stdout`은 로그 파일 이름 접두사입니다. 로그가 만들어질 때 타임스탬프, 프로세스 ID 및 파일 확장명이 자동으로 추가됩니다. `stdout`을 파일 이름 접두사로 사용하여 일반적인 로그 파일의 이름은 *stdout_20180205184032_5412.log*로 지정됩니다. 
1. 업데이트된 *web.config* 파일을 저장합니다.
1. 앱에 대한 요청을 실행합니다.
1. *logs* 폴더로 이동합니다. 가장 최근의 stdout 로그를 찾아서 엽니다.
1. 오류에 대한 로그를 검토합니다.

**중요!** 문제 해결이 완료되면 stdout 로깅을 사용하지 않도록 설정합니다.

1. *web.config* 파일을 편집합니다.
1. **stdoutLogEnabled**를 `false`로 설정합니다.
1. 파일을 저장합니다.

> [!WARNING]
> stdout 로그를 사용하지 않도록 설정하지 않으면 앱 또는 서버 오류가 발생할 수 있습니다. 로그 파일 크기 또는 생성되는 로그 파일 수에 대한 제한은 없습니다.
>
> ASP.NET Core 앱의 루틴 로깅에는 로그 파일 크기를 제한하고 로그를 회전하는 로깅 라이브러리를 사용합니다. 자세한 내용은 [타사 로깅 공급자](xref:fundamentals/logging/index#third-party-logging-providers)를 참조하세요.

## <a name="enabling-the-developer-exception-page"></a>개발자 예외 페이지 사용

`ASPNETCORE_ENVIRONMENT` [환경 변수를 web.config에 추가](xref:host-and-deploy/aspnet-core-module#setting-environment-variables)하여 개발 환경에서 앱을 실행할 수 있습니다. 앱 시작 시 호스트 작성기의 `UseEnvironment`에 의해 환경이 재정의되지 않는 한, 환경 변수를 설정하면 앱이 실행될 때 [개발자 예외 페이지](xref:fundamentals/error-handling)가 표시될 수 있습니다.

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

`ASPNETCORE_ENVIRONMENT`에 대한 환경 변수 설정은 인터넷에 노출되지 않은 스테이징 및 테스트 서버에서만 사용하는 것이 좋습니다. 문제를 해결한 후 *web.config* 파일에서 환경 변수를 제거합니다. *web.config*에서 환경 변수를 설정하는 방법에 대한 자세한 내용은[aspNetCore의 environmentVariables 자식 요소](xref:host-and-deploy/aspnet-core-module#setting-environment-variables)를 참조하세요.

## <a name="common-startup-errors"></a>일반 시작 오류 

[ASP.NET Core 일반 오류 참조](xref:host-and-deploy/azure-iis-errors-reference)를 참조하세요. 앱 시작을 차단하는 대부분의 일반적인 문제는 참조 항목에서 다룹니다.

## <a name="slow-or-hanging-app"></a>앱이 느리거나 중단됨

요청 시 앱이 느리게 응답하거나 중단되면 [덤프 파일](/visualstudio/debugger/using-dump-files)을 가져와서 분석합니다. 덤프 파일은 다음 도구를 사용하여 가져올 수 있습니다.

* [ProcDump](/sysinternals/downloads/procdump)
* [DebugDiag](https://www.microsoft.com/download/details.aspx?id=49924)
* WinDbg: [Windows용 디버깅 도구 다운로드](https://developer.microsoft.com/windows/hardware/download-windbg), [WinDbg를 사용하여 디버그](/windows-hardware/drivers/debugger/debugging-using-windbg)

## <a name="remote-debugging"></a>원격 디버깅

Visual Studio 설명서에서 [Visual Studio 2017의 원격 IIS 컴퓨터에서 ASP.NET Core 원격 디버그](/visualstudio/debugger/remote-debugging-aspnet-on-a-remote-iis-computer)를 참조하세요.

## <a name="application-insights"></a>응용 프로그램 정보

[Application Insights](/azure/application-insights/)에서는 오류 로깅 및 보고 기능을 포함하여 IIS를 통해 호스트된 앱의 원격 분석을 제공합니다. Application Insights는 앱의 로깅 기능을 사용할 수 있게 될 때 응용 프로그램이 시작된 후 발생하는 오류만 보고할 수 있습니다. 자세한 내용은 [ASP.NET Core용 Application Insights](/azure/application-insights/app-insights-asp-net-core)를 참조하세요.

## <a name="additional-troubleshooting-advice"></a>추가 문제 해결 권장 사항

개발 컴퓨터의 .NET Core SDK 또는 앱 내의 패키지 버전을 업그레이드한 후에 즉시 작동 중인 앱에서 오류가 발생하는 경우가 있습니다. 경우에 따라 중요한 업그레이드를 수행할 때 일관되지 않은 패키지로 인해 응용 프로그램이 중단될 수 있습니다. 이러한 대부분의 문제는 다음 지침에 따라 수정할 수 있습니다.

1. *bin* 및 *obj* 폴더를 삭제합니다.
1. *%UserProfile%\\.nuget\\packages* 및 *%LocalAppData%\\Nuget\\v3-cache*에 있는 패키지 캐시를 지웁니다.
1. 프로젝트를 복원하고 다시 빌드합니다.
1. 서버의 이전 배포가 앱을 다시 배포하기 전에 완전히 삭제되었는지 확인합니다.

> [!TIP]
> 명령 프롬프트에서 `dotnet nuget locals all --clear`를 실행하면 간편하게 패키지 캐시를 지울 수 있습니다.
> 
> [nuget.exe](https://www.nuget.org/downloads) 도구를 사용하고 명령 `nuget locals all -clear`를 실행하여 패키지 캐시를 지울 수도 있습니다. *nuget.exe*는 Windows 데스크톱 운영 체제와 함께 제공되는 설치가 아니므로 [NuGet 웹 사이트](https://www.nuget.org/downloads)에서 별도로 다운로드해야 합니다.

## <a name="additional-resources"></a>추가 자료

* [ASP.NET Core의 오류 처리 소개](xref:fundamentals/error-handling)
* [ASP.NET Core를 사용하는 Azure App Service 및 IIS에 대한 일반적인 오류 참조](xref:host-and-deploy/azure-iis-errors-reference)
* [ASP.NET Core 모듈 구성 참조](xref:host-and-deploy/aspnet-core-module)
* [Azure App Service에서 ASP.NET Core 문제 해결](xref:host-and-deploy/azure-apps/troubleshoot)
