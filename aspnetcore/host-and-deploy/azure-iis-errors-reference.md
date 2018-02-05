---
title: "Azure 앱 서비스 및 ASP.NET 코어는 IIS에 대 한 일반적인 오류 참조"
author: guardrex
description: "Azure 앱 서비스 및 IIS에서 ASP.NET Core 응용 프로그램을 호스트 하는 경우에 일반적인 오류를 구분 합니다."
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 03/13/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/azure-iis-errors-reference
ms.openlocfilehash: 53b59045751153cd858e13769b5b42d5700e26d4
ms.sourcegitcommit: 7a87d66cf1d01febe6635c7306f2f679434901d1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="common-errors-reference-for-azure-app-service-and-iis-with-aspnet-core"></a>Azure 앱 서비스 및 ASP.NET 코어는 IIS에 대 한 일반적인 오류 참조

[Luke Latham](https://github.com/guardrex)으로

다음은 모든 오류를 나열한 목록이 아닙니다. 여기에 나열 되지 오류가 발생 하는 경우 [새 문제점](https://github.com/aspnet/Docs/issues/new) 오류를 재현 하는 방법을 자세히 설명 합니다.

다음과 같은 정보를 수집합니다.

* 브라우저 동작
* 응용 프로그램 이벤트 로그 항목
* ASP.NET Core 모듈 stdout 로그 항목

다음과 같은 일반적인 오류에 대 한 정보를 비교 합니다. 일치 하는 항목이 없는 경우 문제 해결 지시를 따릅니다.

## <a name="installer-unable-to-obtain-vc-redistributable"></a>설치 관리자에서 VC++ 재배포 가능 패키지를 가져올 수 없음

* **설치 관리자 예외:** 0x80072efd 또는 0x80072f76 - 지정되지 않은 오류

* **설치 관리자 로그 예외&#8224;:** 오류 0x80072efd 또는 0x80072f76: EXE 패키지를 실행하지 못했습니다.

  &#8224;로그는 C:\Users\\{USER}\AppData\Local\Temp\dd_DotNetCoreWinSvrHosting__{timestamp}.log에 있습니다.

문제 해결:

* 시스템에서 서버 호스팅 번들을 설치하지만 인터넷에 액세스할 수 없는 경우 이 예외는 설치 관리자에서 *Microsoft Visual C++ 2015 재배포 가능 패키지*를 얻을 수 없을 때 발생합니다. 프로그램 설치 관리자를 가져옵니다는 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=53840)합니다. 설치 관리자에 오류가 발생 하면 서버에서 프레임 워크 종속 배포 (FDD)를 호스트 하는 데 필요한.NET 핵심 런타임을 받지 못할 수 있습니다. FDD 호스팅, 하는 경우 프로그램에서 런타임이 설치 되어 있는지 확인 &amp; 기능입니다. 필요한 경우에서 런타임 설치 관리자를 가져올 [.NET 다운로드](https://www.microsoft.com/net/download/core)합니다. 런타임을 설치한 후 시스템을 다시 시작하거나 명령 프롬프트에서 **net stop was /y**에 이어 **net start w3svc**를 실행하여 IIS를 다시 시작합니다.

## <a name="os-upgrade-removed-the-32-bit-aspnet-core-module"></a>OS 업그레이드에서 32비트 ASP.NET Core 모듈이 제거됨

* **응용 프로그램 로그:** 모듈 DLL **C:\WINDOWS\system32\inetsrv\aspnetcore.dll**을(를) 로드하지 못했습니다. 데이터 오류입니다.

문제 해결:

* OS를 업그레이드하는 동안 **C:\Windows\SysWOW64\inetsrv** 디렉터리에 있는 비OS 파일은 보존되지 않습니다. ASP.NET Core 모듈은 이전에 설치 됩니다. 운영 체제 업그레이드와 모든 AppPool 다음은 운영 체제 업그레이드 한 후 32 비트 모드에서 실행 되 면이 문제가 발생 했습니다. OS를 업그레이드한 후에 ASP.NET Core 모듈을 복구합니다. [.NET Core Windows Server 호스팅 번들 설치](xref:host-and-deploy/iis/index#install-the-net-core-windows-server-hosting-bundle)를 참조하세요. 선택 **복구** 설치 관리자를 실행 한 경우.

## <a name="platform-conflicts-with-rid"></a>플랫폼이 RID와 충돌함

* **브라우저:** HTTP 오류 502.5 - 프로세스 오류

* **응용 프로그램 로그:** 응용 프로그램 ' MACHINE/WEBROOT/APPHOST / {어셈블리 (를) ' 실제 루트와 ' c:\{경로}\' commandline와 프로세스를 시작 하지 못했습니다 ' "c:\\{PATH} {어셈블리}. { exe | dll} "', 오류 코드 = ' 0x80004005: ff입니다.

* **ASP.NET Core 모듈 로그:** 처리 되지 않은 예외: System.BadImageFormatException: 로드할 수 없습니다 파일이 나 어셈블리 '{어셈블리}.dll'. 프로그램을 잘못된 형식으로 로드하려고 했습니다.

문제 해결:

* 앱이 Kestrel에서 로컬로 실행되는지 확인합니다. 프로세스 오류는 앱 내의 문제 때문일 수 있습니다. 자세한 내용은 참조 [문제 해결](xref:host-and-deploy/iis/troubleshoot)합니다.

* 확인 하는 `<PlatformTarget>` 에 *.csproj* 의 RID 충돌 하지 않습니다. 예를 들어, 지정 하지 않으면는 `<PlatformTarget>` 의 `x86` 의 RID를 사용 하 여 게시 및 `win10-x64`, 사용 하 여 *dotnet 게시-c 릴리스-r win10 x64* 하거나 설정 하는 `<RuntimeIdentifiers>` 에 *.csproj*  를 `win10-x64`합니다. 프로젝트는 경고 또는 오류 없이 게시되지만 시스템에서 위와 같이 로깅된 예외와 함께 실패합니다.

* 이 예외는 응용 프로그램을 업그레이드 하는 경우 Azure 응용 프로그램 배포에 대 한 발생 하 고 이전 배포에서 모든 파일을 수동으로 삭제 최신 어셈블리를 배포 하는 경우. 호환되지 않는 어셈블리가 오랫동안 남아 있으면 업그레이드된 응용 프로그램을 배포할 때 `System.BadImageFormatException` 예외가 발생할 수 있습니다.

## <a name="uri-endpoint-wrong-or-stopped-website"></a>URI 끝점이 잘못되었거나 중지된 웹 사이트

* **브라우저:** ERR_CONNECTION_REFUSED

* **응용 프로그램 로그:** 항목 없음

* **ASP.NET Core 모듈 로그:** 로그 파일이 만들어지지 않았습니다.

문제 해결:

* 사용 되는 앱에 대 한 올바른 URI 끝점을 확인 합니다. 바인딩을 확인 하십시오.

* IIS 웹 사이트에 없음을 확인는 *Stopped* 상태입니다.

## <a name="corewebengine-or-w3svc-server-features-disabled"></a>CoreWebEngine 또는 W3SVC 서버 기능이 사용되지 않음

* **OS 예외:** ASP.NET Core 모듈을 사용하려면 IIS 7.0 CoreWebEngine 및 W3SVC 기능이 설치되어 있어야 합니다.

문제 해결:

* 적절 한 역할 및 기능이 설정 되어 있는지 확인 합니다. [IIS 구성](xref:host-and-deploy/iis/index#iis-configuration)을 참조하세요.

## <a name="incorrect-website-physical-path-or-app-missing"></a>앱이 누락 또는 잘못 된 웹 사이트 실제 경로

* **브라우저:** 403 사용할 수 없음 - 액세스가 거부되었습니다.  **- 또는 -**  403.14 사용할 수 없음 - 웹 서버가 이 디렉터리의 내용을 표시하지 못하도록 구성되었습니다.

* **응용 프로그램 로그:** 항목 없음

* **ASP.NET Core 모듈 로그:** 로그 파일이 만들어지지 않았습니다.

문제 해결:

* IIS 웹 사이트 확인 **기본 설정** 및 실제 응용 프로그램 폴더가 있습니다. IIS 웹 사이트에 있는 폴더에 응용 프로그램 인지 확인 **실제 경로**합니다.

## <a name="incorrect-role-module-not-installed-or-incorrect-permissions"></a>잘못된 역할, 설치되지 않은 모듈 또는 잘못된 권한

* **브라우저:** 500.19 내부 서버 오류 - 요청된 페이지와 관련된 구성 데이터가 잘못되어 해당 페이지에 액세스할 수 없습니다.

* **응용 프로그램 로그:** 항목 없음

* **ASP.NET Core 모듈 로그:** 로그 파일이 만들어지지 않았습니다.

문제 해결:

* 적절 한 역할을 활성화 되어 있는지 확인 합니다. [IIS 구성](xref:host-and-deploy/iis/index#iis-configuration)을 참조하세요.

* **프로그램 &amp; 기능**을 확인하고 **Microsoft ASP.NET Core 모듈**이 설치되어 있는지 확인합니다. **Microsoft ASP.NET Core 모듈**이 설치된 프로그램 목록에 없으면 해당 모듈을 설치합니다. [.NET Core Windows Server 호스팅 번들 설치](xref:host-and-deploy/iis/index#install-the-net-core-windows-server-hosting-bundle)를 참조하세요.

* 다음 사항을 확인는 **응용 프로그램 풀** > **프로세스 모델** > **Identity** 로 설정 된 **ApplicationPoolIdentity** 또는 사용자 지정 id는 올바른 권한이 응용 프로그램의 배포 폴더에 액세스할 수 있습니다.

## <a name="incorrect-processpath-missing-path-variable-hosting-bundle-not-installed-systemiis-not-restarted-vc-redistributable-not-installed-or-dotnetexe-access-violation"></a>잘못된 processPath, 누락된 PATH 변수, 설치되지 않은 호스팅 번들, 다시 시작되지 않은 시스템/IIS, 설치되지 않은 VC++ 재배포 가능 패키지 또는 dotnet.exe 액세스 위반

* **브라우저:** HTTP 오류 502.5 - 프로세스 오류

* **응용 프로그램 로그:** 응용 프로그램 ' MACHINE/WEBROOT/APPHOST / {어셈블리 (를) ' 실제 루트와 ' c:\\{PATH}\' commandline와 프로세스를 시작 하지 못했습니다 ' ".\{ 어셈블리 (를).exe"', 오류 코드 = ' 0x80070002: 0.

* **ASP.NET Core 모듈 로그:** 로그 파일이 만들어졌지만 비어 있습니다.

문제 해결:

* 앱이 Kestrel에서 로컬로 실행되는지 확인합니다. 프로세스 오류는 앱 내의 문제 때문일 수 있습니다. 자세한 내용은 참조 [문제 해결](xref:host-and-deploy/iis/troubleshoot)합니다.

* 확인의 *processPath* 특성에 `<aspNetCore>` 요소에 *web.config* 이 있는지 확인 하려면 *dotnet* 프레임 워크 종속 배포 (FDD) 또는 *. \{어셈블리}.exe* 자체 포함된 배포 (SCD)에 대 한 합니다.

* FDD의 경우 *dotnet.exe*에서 PATH 설정을 통해 액세스하지 못할 수 있습니다. 시스템 PATH 설정에 *C:\Program Files\dotnet\*이 있는지 확인합니다.

* FDD의 경우 *dotnet.exe*에서 응용 프로그램 풀의 사용자 ID에 액세스하지 못할 수 있습니다. AppPool 사용자 ID에 *C:\Program Files\dotnet* 디렉터리에 대한 액세스 권한이 있는지 확인합니다. AppPool 사용자 id에 대해 구성 된 거부 규칙 확인는 *C:\Program Files\dotnet* 및 응용 프로그램 디렉터리입니다.

* FDD 배포 하 고 IIS를 다시 시작 하지 않고.NET Core를 설치 합니다. 서버를 다시 시작하거나 명령 프롬프트에서 **net stop was /y**에 이어 **net start w3svc**를 실행하여 IIS를 다시 시작합니다.

* .NET 핵심 런타임을 호스팅하는 시스템에 설치 하지 않고는 FDD는 배포 했을 수 있습니다. .NET 핵심 런타임을 설치 실패 하는 경우 실행는 **번들 설치 관리자.NET 핵심 Windows Server 호스팅** 시스템에 있습니다. [.NET Core Windows Server 호스팅 번들 설치](xref:host-and-deploy/iis/index#install-the-net-core-windows-server-hosting-bundle)를 참조하세요. 인터넷 연결 없이 시스템에.NET 핵심 런타임을 설치 하는 동안에서 런타임 가져올 [.NET 다운로드](https://www.microsoft.com/net/download/core) ASP.NET Core 모듈을 설치 하려면 호스팅 번들 설치 관리자를 실행 합니다. 설치를 완료하려면 시스템을 다시 시작하거나 명령 프롬프트에서 **net stop was /y**에 이어 **net start w3svc**를 실행하여 IIS를 다시 시작합니다.

* FDD 배포 및 *Microsoft Visual c + + 2015 재배포 가능 (x64)* 시스템에 설치 되어 있지 않습니다. 프로그램 설치 관리자를 가져옵니다는 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=53840)합니다.

## <a name="incorrect-arguments-of-aspnetcore-element"></a>\<aspNetCore\> 요소의 잘못된 인수

* **브라우저:** HTTP 오류 502.5 - 프로세스 오류

* **응용 프로그램 로그:** 응용 프로그램 ' MACHINE/WEBROOT/APPHOST / {어셈블리 (를) ' 실제 루트와 ' c:\\{PATH}\' commandline와 프로세스를 시작 하지 못했습니다 ' "dotnet".\{ (를) 어셈블리.dll ', 오류 코드 = ' 0x80004005: 80008081 합니다.

* **ASP.NET Core 모듈 로그:** 실행 하려면 응용 프로그램이 없습니다: ' 경로\{어셈블리}.dll '

문제 해결:

* 앱이 Kestrel에서 로컬로 실행되는지 확인합니다. 프로세스 오류는 앱 내의 문제 때문일 수 있습니다. 자세한 내용은 참조 [문제 해결](xref:host-and-deploy/iis/troubleshoot)합니다.

* 검사는 *인수* 특성에 `<aspNetCore>` 요소에 *web.config* 중 하나 인지 확인 하려면 (a) *.\{ (를) 어셈블리.dll* 프레임 워크 종속 배포 (FDD;)에 대 한 또는 (b)를 표시 하지, 빈 문자열 (*인수 = ""*), 또는 응용 프로그램의 인수 목록 (*인수 "arg1, arg2,..." =*) 자체 포함 배포 (SCD).

## <a name="missing-net-framework-version"></a>누락된 .NET Framework 버전

* **브라우저:** 502.3 잘못된 게이트웨이 - 요청을 라우팅하는 동안 연결 오류가 발생했습니다.

* **응용 프로그램 로그:** ErrorCode 응용 프로그램 = ' MACHINE/WEBROOT/APPHOST / {어셈블리 (를) ' 실제 루트와 ' c:\\{PATH}\' commandline와 프로세스를 시작 하지 못했습니다 ' "dotnet".\{ (를) 어셈블리.dll ', 오류 코드 = ' 0x80004005: 80008081 합니다.

* **ASP.NET Core 모듈 로그:** 메서드, 파일 또는 어셈블리 예외가 없습니다. 예외에 지정된 메서드, 파일 또는 어셈블리는 .NET Framework 메서드, 파일 또는 어셈블리입니다.

문제 해결:

* 시스템에서 누락된 .NET Framework 버전을 설치합니다.

* 프레임 워크 종속 배포 (FDD)에 대 한 올바른 런타임 시스템에 설치 되어 있는지 확인 합니다. 1.1에서 2.0, 호스팅 시스템에 배포 하는 프로젝트를 업그레이드 하는 경우이 예외로 인해 2.0 프레임 워크를 호스팅 시스템에서 있는지 확인 합니다.

## <a name="stopped-application-pool"></a>중지된 응용 프로그램 풀

* **브라우저:** 503 서비스를 사용할 수 없음

* **응용 프로그램 로그:** 항목 없음

* **ASP.NET Core 모듈 로그:** 로그 파일이 만들어지지 않았습니다.

문제 해결

* 응용 프로그램 풀에 없음을 확인는 *Stopped* 상태입니다.

## <a name="iis-integration-middleware-not-implemented"></a>IIS 통합 미들웨어가 구현되지 않음

* **브라우저:** HTTP 오류 502.5 - 프로세스 오류

* **응용 프로그램 로그:** 응용 프로그램 ' MACHINE/WEBROOT/APPHOST / {어셈블리 (를) ' 실제 루트와 ' c:\\{PATH}\' 명령줄을 사용 하 여 프로세스를 만든 ' "c:\\{PATH}\{어셈블리}. { exe | dll} "' 하지만 충돌 또는 응답 하지 않았습니다 또는 ErrorCode 지정한 포트 '{PORT}'에서 수신 하지 않은 '0x800705b4' =

* **ASP.NET Core 모듈 로그:**  로그 파일이 만들어졌고 정상 작동을 보여 줍니다.

문제 해결

* 앱이 Kestrel에서 로컬로 실행되는지 확인합니다. 프로세스 오류는 앱 내의 문제 때문일 수 있습니다. 자세한 내용은 참조 [문제 해결](xref:host-and-deploy/iis/troubleshoot)합니다.

* 하거나 확인 합니다.
  * IIS 통합 미들웨어가 referencedby 호출는 `UseIISIntegration` 메서드를 응용 프로그램의 `WebHostBuilder` (ASP.NET Core 1.x)
  * 앱 사용 하 여는 `CreateDefaultBuilder` 메서드 (ASP.NET Core 2.x).
  
  [ASP.NET Core에서의 호스팅](xref:fundamentals/hosting)에서 자세한 내용을 참조하세요.

## <a name="sub-application-includes-a-handlers-section"></a>하위 응용 프로그램에 \<handlers\> 섹션이 포함되어 있음

* **브라우저:** HTTP 오류 500.19 - 내부 서버 오류

* **응용 프로그램 로그:** 항목 없음

* **ASP.NET Core 모듈 로그:** 로그 파일이 만들어지고 루트 응용 프로그램에 대 한 정상 작동을 보여 줍니다. 로그 파일이 하위 앱에 대 한 생성 되지 않았습니다.

문제 해결

* 하위 앱의 *web.config* 파일에 `<handlers>` 섹션이 포함되어 있지 않은지 확인합니다.

## <a name="application-configuration-general-issue"></a>일반적인 응용 프로그램 구성 문제

* **브라우저:** HTTP 오류 502.5 - 프로세스 오류

* **응용 프로그램 로그:** 응용 프로그램 ' MACHINE/WEBROOT/APPHOST / {어셈블리 (를) ' 실제 루트와 ' c:\\{PATH}\' 명령줄을 사용 하 여 프로세스를 만든 ' "c:\\{PATH}\{어셈블리}. { exe | dll} "' 하지만 충돌 또는 응답 하지 않았습니다 또는 ErrorCode 지정한 포트 '{PORT}'에서 수신 하지 않은 '0x800705b4' =

* **ASP.NET Core 모듈 로그:** 로그 파일이 만들어졌지만 비어 있습니다.

문제 해결

* 이 일반 예외 프로세스 대부분 응용 프로그램 구성 문제로 인해 시작 되지 않았음을 나타냅니다. 참조 [디렉터리 구조](xref:host-and-deploy/directory-structure)응용 프로그램의 파일을 배포 하는 적절 한 폴더 및 응용 프로그램의 구성 파일이 있는지 확인 하 고 앱 및 환경에 대 한 올바른 설정을 포함 합니다. 자세한 내용은 참조 [문제 해결](xref:host-and-deploy/iis/troubleshoot)합니다.
