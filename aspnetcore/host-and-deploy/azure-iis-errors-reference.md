---
title: ASP.NET Core를 사용하는 Azure App Service 및 IIS에 대한 일반적인 오류 참조
author: guardrex
description: Azure App Service 및 IIS에서 ASP.NET Core 앱을 호스트할 때 일반적인 오류를 구분합니다.
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 03/13/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/azure-iis-errors-reference
ms.openlocfilehash: 995890a5e6b0cc1d9cebc21486917a7a39587076
ms.sourcegitcommit: a66f38071e13685bbe59d48d22aa141ac702b432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/17/2018
ms.locfileid: "34233341"
---
# <a name="common-errors-reference-for-azure-app-service-and-iis-with-aspnet-core"></a>ASP.NET Core를 사용하는 Azure App Service 및 IIS에 대한 일반적인 오류 참조

[Luke Latham](https://github.com/guardrex)으로

다음은 모든 오류를 나열한 목록이 아닙니다. 여기에 나열되지 않은 오류가 발생하면 오류를 재현하기 위한 자세한 지침이 포함된 [새 문제를 엽니다](https://github.com/aspnet/Docs/issues/new).

다음과 같은 정보를 수집합니다.

* 브라우저 동작
* 응용 프로그램 이벤트 로그 항목
* ASP.NET Core 모듈 stdout 로그 항목

정보를 다음 일반 오류와 비교합니다. 일치하는 항목이 발견되면 문제 해결 권장 사항을 따릅니다.

[!INCLUDE [Azure App Service Preview Notice](../includes/azure-apps-preview-notice.md)]

## <a name="installer-unable-to-obtain-vc-redistributable"></a>설치 관리자에서 VC++ 재배포 가능 패키지를 가져올 수 없음

* **설치 관리자 예외:** 0x80072efd 또는 0x80072f76 - 지정되지 않은 오류

* **설치 관리자 로그 예외&#8224;:** 오류 0x80072efd 또는 0x80072f76: EXE 패키지를 실행하지 못했습니다.

  &#8224;로그는 C:\Users\\{USER}\AppData\Local\Temp\dd_DotNetCoreWinSvrHosting__{timestamp}.log에 있습니다.

문제 해결:

* 시스템에서 호스팅 번들을 설치하는 동안 인터넷에 액세스할 수 없는 경우 이 예외는 설치 관리자에서 ‘Microsoft Visual C++ 2015 재배포 가능 패키지’를 다운로드할 수 없을 때 발생합니다. [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=53840)에서 설치 관리자를 다운로드합니다. 설치 관리자에 오류가 발생하면 서버가 FDD(프레임워크 종속 배포)를 호스트하는 데 필요한 .NET Core 런타임을 받지 못할 수 있습니다. FDD를 호스트하려면 프로그램 및 기능에서 런타임이 설치되어 있는지 확인합니다. 필요한 경우 [.NET 모든 다운로드](https://www.microsoft.com/net/download/all)에서 런타임 설치 관리자를 다운로드합니다. 런타임을 설치한 후 시스템을 다시 시작하거나 명령 프롬프트에서 **net stop was /y**에 이어 **net start w3svc**를 실행하여 IIS를 다시 시작합니다.

## <a name="os-upgrade-removed-the-32-bit-aspnet-core-module"></a>OS 업그레이드에서 32비트 ASP.NET Core 모듈이 제거됨

* **응용 프로그램 로그:** 모듈 DLL **C:\WINDOWS\system32\inetsrv\aspnetcore.dll**을(를) 로드하지 못했습니다. 데이터 오류입니다.

문제 해결:

* OS를 업그레이드하는 동안 **C:\Windows\SysWOW64\inetsrv** 디렉터리에 있는 비OS 파일은 보존되지 않습니다. OS를 업그레이드하기 전에 ASP.NET Core 모듈을 설치한 다음, OS를 업그레이드한 후에 32비트 모드에서 AppPool을 실행하면 이 문제가 발생합니다. OS를 업그레이드한 후에 ASP.NET Core 모듈을 복구합니다. [.NET Core 호스팅 번들 설치](xref:host-and-deploy/iis/index#install-the-net-core-hosting-bundle)를 참조하세요. 설치 관리자가 실행될 때 **복구**를 선택합니다.

## <a name="platform-conflicts-with-rid"></a>플랫폼이 RID와 충돌함

* **브라우저:** HTTP 오류 502.5 - 프로세스 오류

* **응용 프로그램 로그:** 실제 루트 'C:\{PATH}\'가 있는 응용 프로그램 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}'에서 '"C:\\{PATH}{assembly}.{exe|dll}" ' 명령줄로 프로세스를 시작하지 못했습니다. 오류 코드 = '0x80004005 : ff.

* **ASP.NET Core 모듈 로그:** 처리되지 않은 예외: System.BadImageFormatException: 파일이나 어셈블리 '{assembly}.dll'을 로드할 수 없습니다. 프로그램을 잘못된 형식으로 로드하려고 했습니다.

문제 해결:

* 앱이 Kestrel에서 로컬로 실행되는지 확인합니다. 프로세스 오류는 앱 내의 문제 때문일 수 있습니다. 자세한 내용은 [문제 해결](xref:host-and-deploy/iis/troubleshoot)을 참조하세요.

* *.csproj*의 `<PlatformTarget>`이 RID와 충돌하지 않는지 확인합니다. 예를 들어 *dotnet publish -c Release -r win10-x64*를 사용하거나 *.csproj*의 `<RuntimeIdentifiers>`를 `win10-x64`로 설정하여 `x86`인 `<PlatformTarget>`을 지정하지 않고 `win10-x64`인 RID를 사용하여 게시하지 않습니다. 프로젝트는 경고 또는 오류 없이 게시되지만 시스템에서 위와 같이 로깅된 예외와 함께 실패합니다.

* Azure 앱 배포에서 앱을 업그레이드하고 새 어셈블리를 배포할 때 이 예외가 발생하면 이전 배포에서 모든 파일을 수동으로 삭제합니다. 호환되지 않는 어셈블리가 오랫동안 남아 있으면 업그레이드된 응용 프로그램을 배포할 때 `System.BadImageFormatException` 예외가 발생할 수 있습니다.

## <a name="uri-endpoint-wrong-or-stopped-website"></a>URI 끝점이 잘못되었거나 중지된 웹 사이트

* **브라우저:** ERR_CONNECTION_REFUSED

* **응용 프로그램 로그:** 항목 없음

* **ASP.NET Core 모듈 로그:** 로그 파일이 만들어지지 않았습니다.

문제 해결:

* 앱에 올바른 URI 끝점을 사용하고 있는지 확인합니다. 바인딩을 확인합니다.

* IIS 웹 사이트가 ‘중지됨’ 상태가 아닌지 확인합니다.

## <a name="corewebengine-or-w3svc-server-features-disabled"></a>CoreWebEngine 또는 W3SVC 서버 기능이 사용되지 않음

* **OS 예외:** ASP.NET Core 모듈을 사용하려면 IIS 7.0 CoreWebEngine 및 W3SVC 기능이 설치되어 있어야 합니다.

문제 해결:

* 적절한 역할 및 기능이 사용 가능한지 확인합니다. [IIS 구성](xref:host-and-deploy/iis/index#iis-configuration)을 참조하세요.

## <a name="incorrect-website-physical-path-or-app-missing"></a>잘못된 웹 사이트 실제 경로 또는 누락된 앱

* **브라우저:** 403 사용할 수 없음 - 액세스가 거부되었습니다. **- 또는 -** 403.14 사용할 수 없음 - 웹 서버가 이 디렉터리의 내용을 표시하지 못하도록 구성되었습니다.

* **응용 프로그램 로그:** 항목 없음

* **ASP.NET Core 모듈 로그:** 로그 파일이 만들어지지 않았습니다.

문제 해결:

* IIS 웹 사이트 **기본 설정**과 실제 앱 폴더를 확인합니다. 앱이 IIS 웹 사이트 **실제 경로**의 폴더에 있는지 확인합니다.

## <a name="incorrect-role-module-not-installed-or-incorrect-permissions"></a>잘못된 역할, 설치되지 않은 모듈 또는 잘못된 권한

* **브라우저:** 500.19 내부 서버 오류 - 요청된 페이지와 관련된 구성 데이터가 잘못되어 해당 페이지에 액세스할 수 없습니다.

* **응용 프로그램 로그:** 항목 없음

* **ASP.NET Core 모듈 로그:** 로그 파일이 만들어지지 않았습니다.

문제 해결:

* 적절한 역할을 사용할 수 있는지 확인합니다. [IIS 구성](xref:host-and-deploy/iis/index#iis-configuration)을 참조하세요.

* **프로그램 &amp; 기능**을 확인하고 **Microsoft ASP.NET Core 모듈**이 설치되어 있는지 확인합니다. **Microsoft ASP.NET Core 모듈**이 설치된 프로그램 목록에 없으면 해당 모듈을 설치합니다. [.NET Core 호스팅 번들 설치](xref:host-and-deploy/iis/index#install-the-net-core-hosting-bundle)를 참조하세요.

* **응용 프로그램 풀** > **프로세스 모델** > **ID**가 **ApplicationPoolIdentity**로 설정되어 있는지 또는 사용자 지정 ID에 앱의 배포 폴더에 액세스할 수 있는 올바른 권한이 있는지 확인합니다.

## <a name="incorrect-processpath-missing-path-variable-hosting-bundle-not-installed-systemiis-not-restarted-vc-redistributable-not-installed-or-dotnetexe-access-violation"></a>잘못된 processPath, 누락된 PATH 변수, 설치되지 않은 호스팅 번들, 다시 시작되지 않은 시스템/IIS, 설치되지 않은 VC++ 재배포 가능 패키지 또는 dotnet.exe 액세스 위반

* **브라우저:** HTTP 오류 502.5 - 프로세스 오류

* **응용 프로그램 로그:** 실제 루트 'C:\\{PATH}\'가 있는 응용 프로그램 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}'에서 '".\{assembly}.exe" ' 명령줄로 프로세스를 시작하지 못했습니다. 오류 코드 = '0x80070002 : 0.

* **ASP.NET Core 모듈 로그:** 로그 파일이 만들어졌지만 비어 있습니다.

문제 해결:

* 앱이 Kestrel에서 로컬로 실행되는지 확인합니다. 프로세스 오류는 앱 내의 문제 때문일 수 있습니다. 자세한 내용은 [문제 해결](xref:host-and-deploy/iis/troubleshoot)을 참조하세요.

* *web.config*의 `<aspNetCore>` 요소에서 *processPath* 특성을 확인하여 FDD(프레임워크 종속 배포)에 대한 *dotnet*인지 또는 SCD(자체 포함 배포)에 대한 *.\{assembly}.exe*인지 확인합니다.

* FDD의 경우 *dotnet.exe*에서 PATH 설정을 통해 액세스하지 못할 수 있습니다. 시스템 PATH 설정에 *C:\Program Files\dotnet\*이 있는지 확인합니다.

* FDD의 경우 *dotnet.exe*에서 응용 프로그램 풀의 사용자 ID에 액세스하지 못할 수 있습니다. AppPool 사용자 ID에 *C:\Program Files\dotnet* 디렉터리에 대한 액세스 권한이 있는지 확인합니다. *C:\Program Files\dotnet* 및 앱 디렉터리에 AppPool 사용자 ID에 대해 구성된 거부 규칙이 없는지 확인합니다.

* IIS를 다시 시작하지 않은 상태로 FDD를 배포하고 .NET Core를 설치했을 수 있습니다. 서버를 다시 시작하거나 명령 프롬프트에서 **net stop was /y**에 이어 **net start w3svc**를 실행하여 IIS를 다시 시작합니다.

* 호스팅 시스템에 .NET Core 런타임을 설치하지 않고 FDD를 배포했을 수 있습니다. .NET Core 런타임이 설치되어 있지 않으면 시스템에서 **.NET Core 호스팅 번들 설치 관리자**를 실행합니다. [.NET Core 호스팅 번들 설치](xref:host-and-deploy/iis/index#install-the-net-core-hosting-bundle)를 참조하세요. 인터넷에 연결되지 않은 시스템에 .NET Core 런타임을 설치하려는 경우 [.NET 모든 다운로드](https://www.microsoft.com/net/download/all)에서 런타임을 다운로드한 다음, 호스팅 번들 설치 관리자를 실행하여 ASP.NET Core 모듈을 설치합니다. 설치를 완료하려면 시스템을 다시 시작하거나 명령 프롬프트에서 **net stop was /y**에 이어 **net start w3svc**를 실행하여 IIS를 다시 시작합니다.

* FDD를 배포했을 수 있지만 ‘Microsoft Visual C++ 2015 재배포 가능 패키지(x64)’가 시스템에 설치되어 있지 않습니다. [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=53840)에서 설치 관리자를 다운로드합니다.

## <a name="incorrect-arguments-of-aspnetcore-element"></a>\<aspNetCore\> 요소의 잘못된 인수

* **브라우저:** HTTP 오류 502.5 - 프로세스 오류

* **응용 프로그램 로그:** 실제 루트 'C:\\{PATH}\'가 있는 응용 프로그램 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}'에서 '"dotnet" .\{assembly}.dll' 명령줄로 프로세스를 시작하지 못했습니다. 오류 코드 = '0x80004005 : 80008081.

* **ASP.NET Core 모듈 로그:** 실행할 응용 프로그램이 없습니다. 'PATH\{assembly}.dll'

문제 해결:

* 앱이 Kestrel에서 로컬로 실행되는지 확인합니다. 프로세스 오류는 앱 내의 문제 때문일 수 있습니다. 자세한 내용은 [문제 해결](xref:host-and-deploy/iis/troubleshoot)을 참조하세요.

* *web.config*의 `<aspNetCore>` 요소에서 *arguments* 특성을 검사하여 (a) FDD(프레임워크 종속 배포)에 대한 *.\{assembly}.dll*인지, 또는 (b) 없는 경우 빈 문자열(*arguments=""*)이거나 SCD(자체 포함 배포)에 대한 앱의 인수(*arguments="arg1, arg2, ..."*) 목록인지 확인합니다.

## <a name="missing-net-framework-version"></a>누락된 .NET Framework 버전

* **브라우저:** 502.3 잘못된 게이트웨이 - 요청을 라우팅하는 동안 연결 오류가 발생했습니다.

* **응용 프로그램 로그:** 오류 코드 = 실제 루트 'C:\\{PATH}\'가 있는 응용 프로그램 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}'에서 '"dotnet" .\{assembly}.dll' 명령줄로 프로세스를 시작하지 못했습니다. 오류 코드 = '0x80004005 : 80008081.

* **ASP.NET Core 모듈 로그:** 메서드, 파일 또는 어셈블리 예외가 없습니다. 예외에 지정된 메서드, 파일 또는 어셈블리는 .NET Framework 메서드, 파일 또는 어셈블리입니다.

문제 해결:

* 시스템에서 누락된 .NET Framework 버전을 설치합니다.

* FDD(프레임워크 종속 배포)의 경우 시스템에 올바른 런타임이 설치되어 있는지 확인합니다. 프로젝트가 1.1에서 2.0으로 업그레이드되고 호스팅 시스템에 배포된 다음, 이 예외가 발생하면 2.0 프레임워크가 호스팅 시스템에 있는지 확인합니다.

## <a name="stopped-application-pool"></a>중지된 응용 프로그램 풀

* **브라우저:** 503 서비스를 사용할 수 없음

* **응용 프로그램 로그:** 항목 없음

* **ASP.NET Core 모듈 로그:** 로그 파일이 만들어지지 않았습니다.

문제 해결

* 응용 프로그램 풀이 ‘중지됨’ 상태가 아닌지 확인합니다.

## <a name="iis-integration-middleware-not-implemented"></a>IIS 통합 미들웨어가 구현되지 않음

* **브라우저:** HTTP 오류 502.5 - 프로세스 오류

* **응용 프로그램 로그:** 실제 루트 'C:\\{PATH}\'이(가) 있는 응용 프로그램 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}'에서 '"C:\\{PATH}\{assembly}.{exe|dll}" ' 명령줄로 프로세스를 만들었지만 지정된 포트 '{PORT}'에서 크래시하거나 응답하지 않거나 수신 대기하지 않습니다. 오류 코드 = '0x800705b4'

* **ASP.NET Core 모듈 로그:** 로그 파일이 만들어졌고 정상 작동을 보여 줍니다.

문제 해결

* 앱이 Kestrel에서 로컬로 실행되는지 확인합니다. 프로세스 오류는 앱 내의 문제 때문일 수 있습니다. 자세한 내용은 [문제 해결](xref:host-and-deploy/iis/troubleshoot)을 참조하세요.

* 다음 중 하나를 확인합니다.
  * IIS 통합 미들웨어를 참조하려면 앱의 `WebHostBuilder`에서 `UseIISIntegration` 메서드를 호출합니다(ASP.NET Core 1.x).
  * 앱에서 `CreateDefaultBuilder` 메서드를 사용합니다(ASP.NET Core 2.x).
  
  자세한 내용은 [ASP.NET Core의 호스트](xref:fundamentals/host/index)를 참조하세요.

## <a name="sub-application-includes-a-handlers-section"></a>하위 응용 프로그램에 \<handlers\> 섹션이 포함되어 있음

* **브라우저:** HTTP 오류 500.19 - 내부 서버 오류

* **응용 프로그램 로그:** 항목 없음

* **ASP.NET Core 모듈 로그:** 로그 파일이 만들어졌고 루트 앱에 대해 정상 작동을 보여줍니다. 하위 앱에 대한 로그 파일이 만들어지지 않았습니다.

문제 해결

* 하위 앱의 *web.config* 파일에 `<handlers>` 섹션이 포함되어 있지 않은지 확인합니다.

## <a name="stdout-log-path-incorrect"></a>stdout 로그 경로가 올바르지 않음

* **브라우저:** 앱이 정상적으로 응답합니다.

* **응용 프로그램 로그:** 경고: stdoutLogFile \\?\C:\_apps\app_folder\bin\Release\netcoreapp2.0\win10-x64\publish\logs\path_doesnt_exist\stdout_8748_201831835937.log를 만들 수 없습니다. 오류 코드 = -2147024893.

* **ASP.NET Core 모듈 로그:** 로그 파일이 만들어지지 않았습니다.

문제 해결

* *web.config*의 `<aspNetCore>` 요소에 지정된 `stdoutLogFile` 경로가 없습니다. 자세한 내용은 ASP.NET Core 모듈 구성 참조 항목의 [로그 만들기 및 리디렉션](xref:host-and-deploy/aspnet-core-module#log-creation-and-redirection) 섹션을 참조하세요.

## <a name="application-configuration-general-issue"></a>일반적인 응용 프로그램 구성 문제

* **브라우저:** HTTP 오류 502.5 - 프로세스 오류

* **응용 프로그램 로그:** 실제 루트 'C:\\{PATH}\'이(가) 있는 응용 프로그램 'MACHINE/WEBROOT/APPHOST/{ASSEMBLY}'에서 '"C:\\{PATH}\{assembly}.{exe|dll}" ' 명령줄로 프로세스를 만들었지만 지정된 포트 '{PORT}'에서 크래시하거나 응답하지 않거나 수신 대기하지 않습니다. 오류 코드 = '0x800705b4'

* **ASP.NET Core 모듈 로그:** 로그 파일이 만들어졌지만 비어 있습니다.

문제 해결

* 이 일반 예외는 앱 구성 문제로 인해 프로세스가 시작되지 못했음을 나타냅니다. [디렉터리 구조](xref:host-and-deploy/directory-structure)를 참조하여 앱의 배포된 파일과 폴더가 적절하고, 앱의 구성 파일이 있고, 앱과 환경에 대한 올바른 설정을 포함하고 있는지 확인합니다. 자세한 내용은 [문제 해결](xref:host-and-deploy/iis/troubleshoot)을 참조하세요.
