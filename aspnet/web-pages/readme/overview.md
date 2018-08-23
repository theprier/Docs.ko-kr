---
uid: web-pages/readme/overview
title: WebMatrix 추가 정보 | Microsoft Docs
author: rick-anderson
description: WebMatrix 및 ASP.NET 웹 페이지 (Razor) 1.0 릴리스 정보
ms.author: riande
ms.date: 01/06/2011
ms.assetid: 36c5beeb-45a7-48a0-9c30-f82cdf5c5f5f
msc.legacyurl: /web-pages/readme
msc.type: content
ms.openlocfilehash: aa852e7bbd93622154d59e0d0a13ffa680812df2
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41838303"
---
<a name="webmatrix-readme"></a>WebMatrix 추가 정보
====================
2011 년 1 월 13

## <a name="contents"></a>목차

> [!NOTE]
> 이 추가 정보는 WebMatrix의 1.0 릴리스에 적용 됩니다.


- [개요](#Overview)
- [설치](#Installation_Notes)
- [응용 프로그램을 게시 하는 방법](#InstructionsForPublishingApplications)
- [변경 내용 및 문제](#ChangesAndIssues)

    - [WebMatrix 1.0 설치](#Known_Issues_Installation)
    - [ASP.NET 웹 페이지 2](#Known_Issues_ASPNET)
    - [WebMatrix](#Known_Issues_WebMatrix)
    - [IIS Express](#Known_Issues_IISExpress)
    - [SQL Server Compact](#Known_Issues_SQLServerCompact)
    - [응용 프로그램 설치](#Known_Issues_Installing_Applications)
    - [응용 프로그램 게시](#Known_Issues_Publishing_Applications)
- [자세한 내용은](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a>개요

> Microsoft WebMatrix 1.0은 몇 분 안에 설치 하는 무료 웹 개발 스택입니다. 데이터베이스 및 프로그래밍 프레임 워크를 단일 통합된 환경 만들기를 사용 하 여 웹 서버를 통합 합니다. WebMatrix를 사용 하 여 코드, 테스트 및 고유한 ASP.NET 또는 PHP 웹 사이트를 게시 하는 방법을 간소화할 수 있습니다 또는 WebMatrix를 사용 하 여 DotNetNuke, Umbraco, WordPress 또는 Joomla와 같은 인기 있는 오픈 소스 앱을 사용 하 여 새 웹 사이트를 시작 합니다. WebMatrix에는 동일한 강력한 웹 서버, 데이터베이스 엔진 및 프레임 워크 환경을 원활 하 게 개발에서 프로덕션으로 전환 하면 인터넷에서 웹 사이트를 실행 되는 사용 합니다.


<a id="Installation_Notes"></a>

## <a name="installation"></a>설치

> WebMatrix 1.0을 설치 하려면 먼저 설치 해야 합니다 [Microsoft 웹 플랫폼 설치 관리자 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)합니다. 웹 플랫폼 설치 관리자를 설치한 후에 WebMatrix 설치에 사용할 수 있습니다.
> 
> 설치 중에 문제가 있는 경우 가리킵니다 [Microsoft 웹 플랫폼 설치 관리자를 사용 하 여 문제 해결](https://go.microsoft.com/fwlink/?LinkId=196212)합니다.


<a id="InstructionsForPublishingApplications"></a>
## <a name="how-to-publish-applications"></a>응용 프로그램을 게시 하는 방법

> 참조 [응용 프로그램을 게시 하기 위한 단계별 지침](https://go.microsoft.com/fwlink/?LinkID=196149)


<a id="ChangesAndIssues"></a>

## <a name="changes-and-issues"></a>변경 내용 및 문제

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-10-installation-issues"></a>WebMatrix 1.0 설치 문제

#### <a name="issue-webmatrix-10-is-available-only-on-platforms-that-support-microsoft-net-framework-4"></a>문제: WebMatrix 1.0은 Microsoft.NET Framework 4를 지 원하는 플랫폼 에서만 사용할 수 있습니다.

> .NET Framework 버전 4가 WebMatrix 필요 합니다. 특정 경우에 WebMatrix 1.0 설치 관리자는 사용해 볼 수 있도록 지원 되는 구성 집합의 일부가 아닌 플랫폼을 설치 합니다. 특히 Windows Vista SP1 업데이트를 사용 하면 WebMatrix의 설치를 시작 하면 되지만.NET Framework 4 구성 요소는 실패 하 고 설치를 차단 합니다.
> 
> **해결 방법**  
> 포함 하는 지원 되는 플랫폼에 설치 합니다.
> 
> - Windows 7
> - Windows Server 2008
> - Windows Server 2008 R2
> - Windows Vista SP1 이상
> - Windows XP SP3
> - Windows Server 2003 SP2


#### <a name="issue-cannot-install-webmatrix-10-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a>문제: Microsoft Visual Studio 2008은 Microsoft Visual Studio 2008 SP1 없이 설치 된 경우 WebMatrix 1.0을 설치할 수 없습니다.

> **해결 방법**  
> 설치할 [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) Microsoft 다운로드 센터에서.


#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a>문제: SQL Server Compact 4.0에 대 한 일부 어셈블리는 GAC에 설치 되지

> 64 비트 컴퓨터에서 SQL Server Compact 4.0을 설치 하 고 컴퓨터 프로필에만.NET Framework 3.5 SP1 클라이언트 설치에 SQL Server Compact 4.0 용 관리 되는 어셈블리를 전역 어셈블리 캐시 (GAC)에 배치 되지 않습니다. GAC에 설치 되지 않은 관리 되는 어셈블리는 다음과 같습니다.
> 
> - *System.Data.SqlServerCe.dll* (ADO.NET 공급자)
> - *System.Data.SqlServerCe.Entity.dll* (ADO.NET Entity Framework)
> 
> **해결 방법**  
> 제거할 SQL Server Compact 4.0입니다. 다운로드 하 고 다음 위치에서.NET Framework 3.5 SP1의 정식 버전을 설치 합니다.  
>   
> [Microsoft.NET Framework 3.5 서비스 팩 1 (전체 패키지)](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> SQL Server Compact 4.0를 다시 설치 합니다.


#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a>문제: SQL Server Compact는 명령줄을 사용 하 여 제거할 수 없습니다.

> SQL Server Compact 명령줄 옵션을 사용 하 여 제거는이 릴리스에서 작동 하지 않습니다.
> 
> **해결 방법**  
> 사용 하 여 *프로그램 및 기능* Microsoft SQL Server Compact 4.0을 제거 하려면 Windows 제어판에서.


<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a>ASP.NET 웹 페이지

문서의이 섹션에서는 새로운 기능, 변경 및 Razor 구문이 있는 ASP.NET 웹 페이지 1.0 릴리스를 사용 하 여 알려진된 문제에 설명합니다.

- [새로운 기능](#NewFeatures)
- [변경 내용](#Changes)
- [문제](#Issues)

#### <a id="NewFeatures"></a>  새로운 기능

#### <a name="new-configuration-setting-added-to-disable-the-package-manager"></a>패키지 관리자를 사용 하지 않도록 설정에 구성 설정을 추가 하는 새로운 기능:

> 새 `asp:AdminManagerEnabled` 키 수를 `<appSettings>` 요소에는 *web.config* 완전히 패키지 관리자를 사용 하지 않도록 설정할 수 있는 파일입니다. 이 요소에 대 한 기본값은 true, 즉에 포함 되지 않으면 합니다 *web.config* 파일, 패키지 관리자를 사용 하도록 설정 합니다. 패키지 관리자를 사용 하지 않으려면 다음 요소를 추가 합니다 *web.config* 웹 사이트의 루트에 있는 파일:
> 
> [!code-xml[Main](overview/samples/sample1.xml)]


#### <a id="Changes"></a>  Changes

#### <a name="change-webpagesadminfoldervirtualpath-key-renamed-to-aspadminfoldervirtualpath"></a>"Asp: AdminFolderVirtualPath" 이름이 "webPages:AdminFolderVirtualPath" 키를 변경 합니다.

> `webPages:AdminFolderVirtualPath` 에 추가할 수 있는 키를 *web.config* 사용 하려면 패키지 관리자의 위치를 지정 하는 파일 이름이 바뀐를 `asp:` 대신 네임 스페이스는 `webPages` 네임 스페이스입니다. 이 요소를 사용한 경우 구성 파일의 이름을 바꿀 해야 있습니다.


#### <a id="Issues"></a>  알려진된 문제

#### <a name="issue-passwords-for-membership-users-no-longer-recognized"></a>더 이상 인식 하는 멤버 자격 사용자에 대 한 암호 문제:

> 만들기 및 멤버 자격 (로그인) 암호를 저장 하기 위한 알고리즘 보다 안전한 것으로 변경 되었습니다. 결과적으로, ASP.NET Razor의 베타 버전에서 만든 멤버 (사용자)에 대 한 저장 된 암호를 인식할 수 없습니다. 
> 
> **해결 방법** 사이트에 아직 프로덕션에 배치 된 되지 경우 멤버 자격 데이터베이스에서 사용자 레코드를 제거 합니다. 프로그래밍 방식으로 데이터베이스 라이브 인 경우 멤버 자격 데이터베이스에서 기존 암호 다시 생성 합니다.


#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a>문제: 예기치 않은 동작이 멤버 자격에 대 한 사용자 테이블을 사용 하는 경우

> 호출 하는 ASP.NET Razor 웹 사이트에 대 한 멤버 자격 공급자를 초기화 하는 `WebSecurity.InitializeDatabaseConnection` 메서드. (시작 사이트 템플릿의 WebMatrix에서이 메서드에 대 한 호출을 포함 합니다  *\_AppStart.cshtml* 파일입니다.) 경우는 `autoCreateTables` 이 메서드의 매개 변수 설정을 true로 (기본적으로 설정은 시작 사이트 템플릿의 true), 하며 메서드는 인식할 수 없는 테이블 이름 (두 번째 매개 변수) 메서드에 전달 되 면 오류가 발생 하지 않습니다. 대신 테이블을 자동으로 만듭니다.
> 
> 이 멤버 자격에 대 한 사용자 테이블을 사용 하지만 잘못 된 테이블 이름을 전달 하려는 경우 문제가 될 수는 `WebSecurity.InitializeDatabaseConnection` 메서드. 메서드는 기본적으로 오류가 발생 하지 지정한 테이블 없으면 및 대신 새 테이블을 만들기 때문에 응용 프로그램 작동에 나타날 수 있습니다. 그러나 사용자 테이블 (및 해당 필드에)를 사용 하는 응용 프로그램 코드 예기치 않은 오류를 사용 하 여 최종적으로 실패할 수 있습니다.
> 
> **해결 방법**  
> 이름에 성공 했는지 확인 합니다 `InitializeDatabaseConnection` 사용자 프로필 멤버 자격 데이터베이스에서 테이블 또는 했는지 메서드 일치를 `autoCreateTables` 매개 변수를 false로.


#### <a name="issue-error-message-the-admin-module-requires-access-to-appdata"></a>문제: 오류 메시지 "~/App에 대 한 액세스 관리 모듈에 필요한\_데이터"

> 상황에 따라 사용자 만들기 또는 그렇지 않은 경우 ASP.NET 멤버 자격 시스템을 사용 하려고 하면 오류를 표시 하도록 페이지 *The 관리자 모듈 ~/App 액세스할 수 있어야\_데이터*입니다. IIS 또는 IIS Express에서 실행 되는 계정을 만들고 쓸 수 있는 권한이 없는 경우이 경고가 발생 합니다 *앱\_데이터* 웹 사이트 루트 폴더입니다. 
> 
> **해결 방법** 수동으로 만들기는 *App\_데이터* 웹 사이트에 대 한 폴더입니다. 응용 프로그램 (일반적으로 NETWORK SERVICE)에서 실행 되는 Windows 계정에 앱과 같은 하위 폴더 및 응용 프로그램의 루트 폴더에 대 한 읽기/쓰기 권한이 있는지를 확인 한 다음\_데이터입니다. 자세한 내용은 기술 자료 문서에서 사용할 수 [SQL Server Express 사용자 인스턴스 및 ASP.net 웹 응용 프로그램 프로젝트를 사용 하 여 문제](https://support.microsoft.com/kb/2002980)합니다.


#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a>문제: "못했습니다" SQL Server의 사용자 인스턴스 생성 오류

> WebMatrix 웹 응용 프로그램을 SQL Server Express를 사용 하 여 Windows 7 또는 Windows Server 2008 R2에서 IIS 7.5를 실행 중인 경우 SQL Server가 런타임 시 사용자의 로컬 응용 프로그램 경로 검색할 수 없습니다 나타내는 오류가 표시 될 수 있습니다.
> 
> **해결 방법** 응용 프로그램 (일반적으로 NETWORK SERVICE)에서 실행 되는 Windows 계정에 하위 폴더 및 응용 프로그램의 루트 폴더에 대 한 읽기/쓰기 권한을 같은 *앱\_데이터*. 자세한 내용은 기술 자료 문서에서 사용할 수 [SQL Server Express 사용자 인스턴스 및 ASP.net 웹 응용 프로그램 프로젝트를 사용 하 여 문제](https://support.microsoft.com/kb/2002980)합니다.


#### <a name="issue-files-that-contains-package-manager-resources-or-package-manager-passwords-are-servable-under-iis-60-and-earlier"></a>문제: 패키지 관리자 리소스 또는 패키지 관리자 암호를 포함 하는 파일은 IIS 6.0에서 제공 가능으로 및 이전 버전

> RC2 릴리스를 사용 하 여 빌드된 하는 ASP.NET Web Pages (Razor) 응용 프로그램을 배포 하는 경우 및 응용 프로그램을 포함 하는 경우는 *password.txt* 하거나 *packagesources.txt* 파일 */App\_ 데이터/관리자*, IIS 6.0 요청, 잠재적으로 패키지 관리자 인스턴스에 대 한 암호를 노출 하는 경우 파일을 제공 합니다. 
> 
> **해결 방법** 이름 바꾸기는 *password.txt* 하거나 *packagesources.txt* 파일을 *password.config* 또는 *packagesources.config*. IIS 6.0은 기본적으로 파일을 처리 하지 않는 경우는 *.config* 확장 합니다. (IIS 7에서는에 파일이 없는 합니다 *앱\_데이터* 폴더가 제공 되는 파일 이름을 바꿀 필요가 없습니다.)


#### <a name="issue-uninstalling-packages-installed-using-the-beta-3-release-does-not-completely-remove-package-components"></a>문제: 베타 3 릴리스를 사용 하 여 설치 된 패키지를 제거 하면 완전히 제거 하지 않습니다 패키지 구성 요소

> Beta 3 릴리스에에서 패키지 관리자를 사용 하 여 패키지를 설치 하 고 현재 버전을 사용 하 여 제거를 시도 하는 경우 패키지를 완전히 제거 되지 않습니다. 패키지 관리자를 사용 하 여 **제거** 단추 몇 가지 구성 요소를 제거 하지만 라이브러리 코드 패키지의 떠나고 업데이트 되지 않는 합니다 *package.config* 파일입니다.
> 
> **해결 방법**   
> 다음이 단계를 수행 합니다.  
> 1. 삭제 된 *앱\_Data\packages* 폴더입니다. 이 모든 패키지를 제거합니다.   
> 2. 삭제 된 *packages.config* 웹 사이트의 루트에 있는 파일입니다.


#### <a name="issue-in-visual-studio-invoking-the-web-based-package-manager-takes-the-application-offline"></a>문제: Visual Studio에서 웹 기반 패키지 관리자를 호출 합니다. 오프 라인 응용 프로그램

> Visual Studio (없습니다 WebMatrix)에서 작업 하는 하 고 사용 하는 경우는  *\_관리자* Visual Studio 패키지 관리자를 시작 하는 기능이 응용 프로그램을 오프 라인으로 전환 하 고 게시 합니다 *앱\_ offline.htm* 패키지 관리자를 사용 하는 기능을 방해 하는 웹 사이트 루트에 있습니다.
> 
> [!NOTE]
> 추가, 제거 또는에서 파일을 수정 하는 경우 동일한 동작이 수행는 가장 일반적으로 표시 되지만이 문제는 웹 기반 패키지 관리자 인터페이스를 사용 하는 경우에 *앱\_데이터* 폴더입니다.
> 
> **해결 방법**   
> Visual Studio에서 패키지를 사용 하려면 웹 기반 패키지 관리자 대신 NuGet 확장을 사용 합니다. 정보에 대 한 참조를 [NuGet 설명서](https://docs.microsoft.com/nuget/)합니다. 다른 파일을 사용 하 여 작업 하는 경우는 *앱\_데이터* 폴더에이 문제를 방지 하려면 다른 위치에서 파일을 유지 하는 것이 좋습니다. 그렇게 해도 효과가 없는 경우 삭제 합니다 *앱\_offline.htm* 파일을 수동으로 또는 자동으로 (기본적으로 30 초 후) 사이트를 다시 온라인 상태가 될 때까지 기다립니다.


#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a>문제: Visual Studio IntelliSense 및 프로젝트 템플릿이 ASP.NET MVC 3 버전 에서만 사용할 수 있습니다

> ASP.NET 웹 페이지를 설치 설치 하지 않습니다도 도구 Visual Studio에 대 한 예: ASP.NET Web Pages 응용 프로그램에 대 한 IntelliSense 및 프로젝트 템플릿.
> 
> **해결 방법** 웹 플랫폼 설치 관리자를 통해 ASP.NET MVC 3 RC 설치 Visual Studio에서 ASP.NET 웹 페이지 응용 프로그램에 대 한 IntelliSense 및 프로젝트 템플릿을 사용 하려면 또는 [독립 실행형 설치 관리자](https://go.microsoft.com/fwlink/?LinkID=191797)합니다.


#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a>문제: 프록시 서버를 통해 다른 외부 데이터 나 피드 읽기

> 에 대 한 프록시 정보를 구성 해야 사이트를 실행 하는 서버를 프록시 서버로 보호 하는 경우는 *web.config* 외부 사이트에서 제공 되는 정보를 읽을 수 있도록 파일입니다. 예를 들어, 사용 하는 경우는 `ReCaptcha` 도우미 도우미 reCAPTCHA 서비스와 통신 하지만 프록시 서버에서 차단 될 수 있습니다. 마찬가지로, 패키지 관리자를 사용한 피드 등 ASP.NET 웹 페이지에서 사용 되는 피드 프록시 구성이 필요할 수 있습니다.
> 
> 패키지 피드를 사용 하거나 외부 서비스를 사용 하 여 작업에 문제가 있는 경우 다음 요소를 응용 프로그램의 루트에 배치 *web.config* 파일:
> 
> [!code-xml[Main](overview/samples/sample2.xml)]
> 
> 프록시 서버를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [ &lt;프록시&gt; 요소 (네트워크 설정)](https://msdn.microsoft.com/library/sa91de1e.aspx) MSDN 웹 사이트입니다.


#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a>문제: Razor 구문이 있는 ASP.NET 웹 페이지를 사용 하지 않도록 설정.NET Framework 버전 4 제거 합니다.

> .NET Framework 버전 4 제거 하 고 다시 설치 하는 경우에 Razor 구문이 있는 ASP.NET 웹 페이지 비활성화 됩니다. 사용 하 여 페이지의 *.cshtml* 확장 제대로 실행 되지 않는 경우. 컴퓨터 루트에 있는 어셈블리를 등록 하는 ASP.NET 웹 페이지 *web.config* 파일 및.NET Framework를 제거 합니다. 해당 파일을 제거 합니다. .NET Framework를 다시 설치 하면 구성 파일의 새 버전을 설치 하지만 ASP.NET 웹 페이지 어셈블리에 대 한 참조를 추가 하지 않습니다.
> 
> **해결 방법** .NET Framework를 다시 설치한 후 Razor 구문이 있는 ASP.NET 웹 페이지를 다시 설치 합니다. 다음 요소를 추가 합니다 *web.config* 일반적으로 다음 위치에 있는 컴퓨터 루트에 있는 파일:  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](overview/samples/sample3.xml)]


#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a>문제: 확장명 없는 Url을 IIS 7 또는 IIS 7.5.cshtml/.vbhtml 파일 찾지 못한

> IIS 7 또는 IIS 7.5에서 다음과 같은 URL 사용 하 여 요청은 포함 된 페이지를 찾을 수 합니다 *.cshtml* 하거나 *.vbhtml* 확장:  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> URL 재작성 활성화 되어 있지 않으므로 기본적으로 IIS 7 또는 IIS 7.5 용 르면 문제가 발생 합니다. 문제일 수 있습니다 시나리오에는 IIS Express를 사용 하 여 로컬로 테스트할 때 문제가 표시 되지 않으면 있지만 호스팅 웹 사이트에 웹 사이트를 배포할 때 환경입니다.
> 
> **해결 방법**
> 
> - 서버 컴퓨터에 대 한 제어를 사용 하는 경우 서버 컴퓨터의 설치에 설명 된 업데이트가 [는 업데이트를 사용할 수 있도록 특정 Url을 요청 하는 IIS 7.0 또는 IIS 7.5 처리기를 처리 하는 마침표로 끝나지 않는](https://support.microsoft.com/kb/980368)합니다.
> - 서버 컴퓨터에 대 한 제어 없는 경우 (예를 들어, 배포 하는 호스팅 웹 사이트), 웹 사이트의 다음 추가할 *web.config* 파일: 
> 
>     [!code-xml[Main](overview/samples/sample4.xml)]


#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a>문제: SQL Server Compact 설치 되지 않은 컴퓨터에 응용 프로그램 배포

> SQL Server Compact 데이터베이스를 포함 하는 응용 프로그램 SQL Server Compact는 설치 되지 않은 컴퓨터에서 실행할 수 있습니다. Microsoft WebMatrix 1.0에서 자동으로 이러한 이진 파일을 복사 하 고 적절 한 수행 *web.config* 파일 변환 합니다.
> 
> **해결 방법** 이러한 파일을 복사 하 고 확인 해야 할 경우 합니다 *web.config* 파일 변경 내용을 수동으로 다음을 수행 합니다.
> 
> 1. 데이터베이스 엔진 어셈블리를 복사 합니다 *Bin* 대상 컴퓨터에서 응용 프로그램의 폴더 (및 하위 폴더).  
> 
>    - Copy *C:\Program Files\Microsoft SQL Server Edition\v4.0\Desktop\System.Data.SqlServerCe.dll*   
>        **to** *\Bin*
>    - 복사본 <em>C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\</em><strong><em>하</em></strong>\Bin\x86*
>    - 복사본 <em>C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\</em>* <strong>하</strong><em>\Bin\amd64</em>
> 
> 2. 웹 사이트의 루트 폴더를 만들거나 엽니다는 *web.config* 파일입니다. (WebMatrix 1.0에서이 파일 형식은 클릭할 경우 사용할 수 있습니다 **모든** 에 **파일 형식을 선택** 대화 상자.)
> 3. 다음 요소 자식으로 추가 합니다 `<configuration>` 요소 (에 포함 되지 않은 `<system.web>` 요소).
> 
>     [!code-xml[Main](overview/samples/sample5.xml)]


#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a>문제: Visual Basic에서 보통 신뢰 "Database" 및 "WebGrid" 도우미 작동 하지 않습니다.

> Visual Basic을 사용 하는 경우 (만드는 *.vbhtml* 파일), `Database` 고 `WebGrid` 도우미 응용 프로그램은 보통 신뢰를 사용 하도록 설정 된 경우 작동 하지 것입니다.
> 
> **해결 방법**  
> Visual Studio 2010을 사용 하는 경우에 서비스 팩 1 릴리스를 설치 하 여이 문제를 해결할 수 있습니다. Sp1의 최종 버전까지 베타 버전에서 SP1 다운로드할 수 있습니다 합니다 [Microsoft Visual Studio 2010 Service Pack 1 Beta](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en) Microsoft 다운로드 센터 페이지입니다.   
>   
> 이 방법은 실용적이 지 않거나 Visual Studio 2010을 사용 하지 않으면 하면 일시적으로 완전 신뢰를 사용 하 여 응용 프로그램을 설정 합니다.


#### <a name="issue-applicationpart-resources-are-externally-accessible"></a>문제: "ApplicationPart" 리소스는 외부에서 액세스할 수

> 어셈블리에서 파생 되는 개체를 포함 하는 경우는 `ApplicationPart` 어셈블리의 리소스에 의해 노출 되는 클래스는 `ResourceRouteHandler` 클래스입니다. 예를 들어 다음 URL을 가정해 봅니다.  
>   
> `~/r.ashx/System.Web.WebPages.Administration/Resources/AdminResources.resources`  
>   
> 이 요청에 리소스 문자열의 모든 다운로드 합니다 *System.Web.WebPages.Administration.dll* 어셈블리입니다. (도 정적 콘텐츠를 제공할 수 없습니다) 포함 된 리소스를 모두 다운로드 됩니다. 포함된 리소스에 중요 한 정보를 포함 하는 경우 보안 위험을 나타낼 수 있습니다이 합니다. 
> 
> **해결 방법**   
> 만드는 경우는 **ApplicationPart** 개체가 포함된 된 리소스가 연결 된 선택 되어 있는지 확인 합니다 **ApplicationPart** 개체의 어셈블리에 중요 한 정보가 포함 되지 않습니다.


<a id="Known_Issues_WebMatrix"></a>

### <a name="webmatrix"></a>WebMatrix

> [!NOTE]
> WebMatrix에 대 한 설치 문제에 대 한 정보를 참조 하세요 [WebMatrix 설치 문제](#Known_Issues_Installation) 이 문서의 앞부분에 설명 합니다.


문서의이 섹션에서는 WebMatrix 개발 환경에 대 한 알려진된 문제를 설명합니다.

#### <a name="issue-changes-in-the-username-or-password-of-a-database-connection-string-in-a-webconfig-file-are-not-reflected-in-the-databases-workspace"></a>문제: 사용자 이름 또는 web.config 파일에서 데이터베이스 연결 문자열의 암호 변경 내용은 데이터베이스 작업 영역에 반영 되지 않습니다.

> **해결 방법**  
> 
> 1. 에 *web.config* 파일, 연결 문자열에 데이터베이스 이름을 변경 (예를 들어를 "1" 추가).
> 2. 저장 된 *web.config* 파일입니다.
> 3. 클릭 **데이터베이스** 새로 고칩니다.
> 4. 연결 문자열에 데이터베이스 이름을 변경 합니다 *web.config* 에 파일을 다시 원래 데이터베이스 이름입니다.
> 5. 저장 된 *web.config* 파일입니다.
> 6. 클릭 **데이터베이스** 새로 고칩니다.


#### <a name="issue-folders-created-by-webmatrix-cannot-be-deleted"></a>문제: WebMatrix에서 생성 된 폴더를 삭제할 수 없습니다.

> WebMatrix 상승 된 권한을 사용 하 여 실행 중인 경우 (즉, WebMatrix를 사용 하 여 시작 하는 **관리자 권한으로 실행** Windows에서 옵션), Windows 탐색기를 사용 하 여 WebMatrix에서 생성 되는 폴더를 삭제할 수 없습니다.
> 
> **해결 방법**  
> 상승 된 권한을 사용 하 여 Windows 탐색기를 실행 합니다. 아래 단계를 수행합니다.  
> 
> 1. Windows, 클릭 **시작**합니다.
> 2. "Windows Explorer"를 입력 하 고 항목을 마우스 오른쪽 단추로 클릭 **Windows 탐색기**합니다.
> 3. 클릭 **관리자 권한으로 실행**합니다. 폴더를 삭제할 수 있습니다.


#### <a name="issue-webmatrix-10-is-unable-to-perform-certain-tasks-that-require-elevation"></a>문제: WebMatrix 1.0 권한 상승을 요구 하는 특정 작업을 수행할 수 없습니다

> WebMatrix 1.0가 다음과 같은 상황에서 추가 구성 요소를 설치 하는 등의 권한 상승 해야 하는 특정 작업을 수행할 수 없습니다.
> 
> - Windows Vista 또는 Windows 7에서 관리자 권한이 없는 계정으로 로그온 한 사용자 계정 컨트롤 (UAC)을 사용할 수 없습니다.
> - Microsoft Windows XP 또는 Microsoft Windows Server 2003을 사용 하는 있습니다.
> 
> **해결 방법**  
> WebMatrix 1.0에서 대부분의 작업에는 관리 권한이 필요 하지 않습니다. 이러한 조작자에 대 한 다음이 단계를 수행 또는 관리자로 서 작업을 수행할 수 있습니다.
> 
> - Windows Vista 또는 Windows 7에서 UAC를 사용 하도록 설정 합니다.
> - Windows XP에서 Administrators 보안 그룹에 사용자를 추가 합니다.


#### <a name="issue-site-from-web-gallery-is-disabled"></a>문제: "웹 갤러리에서 사이트"을 사용할 수 없습니다.

> 합니다 **웹 갤러리에서 사이트** 웹 플랫폼 설치 관리자 3.0이 설치 되지 않은 경우 옵션은 사용할 수 없습니다.
> 
> **해결 방법**  
> 설치 합니다 [Microsoft 웹 플랫폼 설치 관리자 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)합니다.


#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a>문제: Google Chrome 실행 옵션으로 지원 되지 않습니다.

> Google Chrome 브라우저에서 목록에 표시 되지 않습니다 **실행할** 에 **홈** 탭 합니다.
> 
> **해결 방법**  
> Google Chrome의 일부 버전에서는 등록 하지 자체 올바르게 Windows의 기본 프로그램 기능을 사용 합니다. 대 안으로, Google Chrome을 시작 합니다 *사용자 지정 및 Google Chrome 컨트롤* 메뉴에서 클릭 *옵션*를 클릭 하 고 *확인 Google Chrome 기본 브라우저*.


#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a>문제: "외래 키" 대화 상자를 허용 하지 않습니다는 기본 키를 입력 합니다.

> 합니다 **외래 키** 대화 상자 기본 키 테이블에서 기본 키 이름을 입력할 수를 허용 하지 않습니다.
> 
> **해결 방법**  
> 이 의도적입니다. 기본 키 테이블에서 기본 키의 이름을 입력할 필요가 없습니다.


#### <a name="issue-intellisense-is-not-available-in-webmatrix-for-razor-syntax-c-or-visual-basic"></a>문제: IntelliSense는 Razor 구문, C# 또는 Visual Basic WebMatrix에서 사용할 수 없습니다.

> HTML 및 CSS WebMatrix에서 IntelliSense가 지원 됩니다. 그러나 다른 언어에 대해 사용할 수 없는 경우 
> 
> **해결 방법**   
> 없음


#### <a name="issue-intellisense-for-html-and-css-suggests-elements-that-are-not-contextually-appropriate"></a>문제: HTML 및 CSS에 대 한 IntelliSense 제안 컨텍스트에 적절 하지 않은 요소

> WebMatrix의 태그에 대 한 IntelliSense 지원 사용 하 여 HTML 합니다 [XHTML 1.0 Transitional 스키마](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional) 하 고 CSS를 사용 하는 [CSS 2.1 스키마](http://www.w3.org/TR/CSS2/). IntelliSense를 이러한 특정 스키마를 기반으로 하기 때문에 특정 태그, 특성 또는 속성 수 제안 하는 현재 페이지 또는 스타일 정의에 적합 하지 않습니다. HTML에 대 한 잘못 된 XHTML (예: 태그가 닫혀 있지 않은 경우)로 해석 될 수 있는 콘텐츠에 예기치 않은 제안 발생할 수도 있습니다. 이 문제는 불완전 한 태그를 안에 삽입 지점이 있을 경우 더 두드러질 수 있습니다. 이 경우 IntelliSense 태그를 새 열을 제안 하거나 다른 잘못 된 제안 수 있습니다. 
> 
> **해결 방법**   
> HTML, 잘 구성 된, 완전 한 XHTML 페이지 내에서 작업 하는 것이 있는지 확인 합니다. CSS에 대 한 해결 방법이 없습니다.


#### <a name="issue-intellisense-is-not-invoked-while-you-type"></a>문제: 입력할 때 IntelliSense가 호출 되지 않는다

> 때때로 HTML 또는 CSS 편집기에서 입력 되는 IntelliSense 호출 되지 않을 수 있습니다. 특히,이 파일의 끝 또는 다른 요소 옆에 있는 직접 삽입 지점이 있을 경우 발생할 수 있습니다. 
> 
> **해결 방법**   
> 삽입 포인터 주위 공백 인지 삽입 지점이 되 고 있지 않음을 파일의 끝에 있는지 확인 합니다. 또한 Ctrl + 스페이스바를 눌러 IntelliSense를 수동으로 호출할 수 있습니다.


#### <a name="issue-no-ui-is-available-for-disabling-intellisense"></a>문제: UI 수 IntelliSense를 사용 하지 않도록 설정

> WebMatrix 1.0 IntelliSense를 사용 하지 않도록 설정 하는 것에 대 한 UI 또는 제스처를 제공 합니다. 
> 
> **해결 방법**   
> IntelliSense를 사용 하지 않도록 설정 하는 스위치를 포함 하는 다음 명령을 사용 하 여 WebMatrix를 시작 합니다.  
>   
> `WebMatrix.exe #ExecuteCommand# EditorIntelliSense off`


<a id="Known_Issues_IISExpress"></a>
### <a name="iis-express"></a>IIS Express

IIS Express는 다음 URL에서 사용할 수 있는 추가 정보 파일을 사용 하는 자체에 있습니다.

[https://go.microsoft.com/fwlink/?LinkID=207675&ampclcid = 0x409](https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409)

<a id="Known_Issues_SQLServerCompact"></a>

### <a name="sql-server-compact"></a>SQL Server Compact

SQL Server Compact에 다음 URL에서 사용할 수 있는 추가 정보 파일을 사용 하는 자체 있습니다.

[https://go.microsoft.com/fwlink/?LinkID=208545](https://go.microsoft.com/fwlink/?LinkID=208545&amp;clcid=0x409)

WebMatrix의 일부로 SQL Server Compact 설치와 관련 된 문제에 대 한 내용은 [WebMatrix 설치 문제](#Known_Issues_Installation) 이 문서의 앞부분에 설명 합니다.

### <a id="Known_Issues_Installing_Applications"></a>  응용 프로그램 설치

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a>문제: 응용 프로그램을 설치할 수 시간이 오래 걸릴 경우 사용자의 내 문서 폴더는 네트워크 공유로 리디렉션됩니다.

> **해결 방법**  
> 없음 응용 프로그램을 설치 하는 데 소요 되지만 제대로 설치 됩니다.


### <a id="Known_Issues_Publishing_Applications"></a>  응용 프로그램 게시

#### <a name="issue-required-permissions-cannot-be-acquired-error-when-publishing-a-sql-compact-database"></a>문제: "는 데 필요한 사용 권한을 가져올 수 없습니다" 오류 SQL Compact 데이터베이스를 게시 하는 경우

> WebMatrix에서는 보통 신뢰 수준 구성을 사용 하 여.NET Framework 버전 3.5 실행 하는 서버에 SQL Server Compact에 대 한 지원 이진 파일을 배포 완전히 지원 되지 않습니다.
> 
> **해결 방법**  
> 기본 해결 방법은 서버에서.NET Framework 4를 설치 하는 것입니다. 또는 다음을 수행 합니다.
> 
> 1. 다음 요소를 추가 합니다 `SecurityClasses` 단원의 *웹\_MediumTrust.config* 파일:
> 
>     [!code-html[Main](overview/samples/sample6.html)]
> 2. 만들 새 권한 집합는 *웹\_MediumTrust.config* 다음 필요한 권한이 있는 파일:
> 
>     [!code-html[Main](overview/samples/sample7.html)]
> 3. 다음 요소에 배치 하 여 SQL Server Compact로 설정 된 사용 권한을 적용 합니다 *웹\_MediumTrust.config* 파일:
> 
>     [!code-html[Main](overview/samples/sample8.html)]


#### <a name="issue-gallery-and-phpbb-web-applications-display-a-service-is-unavailable-error-after-publishing"></a>문제: 웹 응용 프로그램 갤러리 및 PhpBB "서비스를 사용할 수 없습니다." 오류를 게시 한 후 표시

> 상황에 따라 응용 프로그램을 게시 하면 "서비스를 사용할 수 없습니다." 오류가 발생 합니다.
> 
> **해결 방법**  
> WebMatrix에서 백슬래시를 추가 (\) 에서 서버 이름의 끝에는 **게시 설정** 창 및 응용 프로그램을 다시 게시 합니다.


#### <a name="issue-moodle-website-layout-and-links-are-broken-after-publishing"></a>문제: Moodle 웹 사이트 레이아웃 및 링크는 끊어진 게시 후

> Moodle은 응용 프로그램을 게시 한 후 응용 프로그램이 제대로 작동 하지 않습니다.
> 
> **해결 방법**  
> WebMatrix에서의 끝에 슬래시 (/)를 추가 합니다 **사이트 이름** 필드를 **게시 설정** 창 한 다음 응용 프로그램을 다시 게시 합니다.


#### <a name="issue-publishing-nopcommerce-fails-with-a-database-error"></a>문제: 데이터베이스 오류로 인해 실패할 nopCommerce 게시

> 게시 nopCommerce는 실패 하 고 같은 데이터베이스 오류를 보고 "를 nop 삽입\_로그 table이 실패 했습니다."
> 
> **해결 방법**  
> 
> 1. WebMatrix에서 클릭 **실행** nopCommerce 로컬로 시작 합니다.
> 2. 관리 페이지에 로그인 합니다.
> 3. 클릭 합니다 **시스템** 메뉴.
> 4. 클릭 합니다 **로그** 옵션입니다.
> 5. 클릭 합니다 **로그 지우기** 단추입니다.
> 6. NopCommerce를 다시 게시 합니다.


#### <a name="issue-silverstripe-cms-displays-a-http-500-php-fcgi-error-when-you-download-a-published-site"></a>문제: Silverstripe CMS 오류를 표시 "HTTP 500 PHP FCGI" 게시 된 사이트를 다운로드 하는 경우

> **해결 방법**  
> 클릭 한 후 **다운로드 사이트를 게시**, 건너뛰기 `silverstripe-cache/manifest_main` 에서 **게시 미리 보기**합니다. 이 파일 캐싱 목적으로 사용 되 고 각 컴퓨터에 따라 다릅니다.


#### <a name="issue-subtext-displays-server-error-in--application-when-you-download-a-published-site"></a>문제: Subtext 표시 "서버 오류 '/' 응용 프로그램 의" 게시 된 사이트를 다운로드 하는 경우

> **해결 방법**  
> 사이트를 엽니다 *web.config* 파일 및 SQL Server 관리자 자격 증명 ("sa" 자격 증명)를 사용 하 여 사용자 ID 및 데이터베이스 연결 문자열에 암호를 대체 합니다.
> 
> 또는 로그인 하는 사용자 계정에 부여 하려면 다음이 단계를 수행 `db_owner` 권한:
> 
> 1. 웹 플랫폼 설치 관리자를 사용 하 여 SQL Server Management Studio를 설치 합니다.
> 2. 로컬 SQL Server Express 인스턴스에 연결 (기본적으로 `.\SQLEXPRESS`).
> 3. 클릭 **데이터베이스** &gt; *[localSubtextDatabase]* &gt; **Security** &gt; **사용자** &gt; *[localSubtextUser*] (기본값은 `subtextuser`]를 마우스 오른쪽 단추로 클릭 하 고 **속성**합니다.
> 4. 선택 **db\_소유자** 역할 멤버 자격 섹션에서입니다.


#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a>문제: 사이트 "대상 URL" 필드는 http:// 또는 https:// 로 시작 하지 않는 경우 게시 한 후 작동 하지 않을 수 있습니다.

> 에 **게시 설정** 대화 상자에서 대상 URL로 시작 하지 않는 경우 `http://` 또는 `https://`, 사이트 배포 후 작동 하지 않을 수 있습니다.
> 
> **해결 방법**  
> 있는지 확인 하는 사이트에서 대상 URL을 게시 하기 전에 합니다 **게시 설정** 대화 상자 시작 `http://` 또는 `https://`합니다.


#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a>문제: MySQL 데이터베이스를 게시할 오류로 인해 실패 "데이터베이스를 게시 하지 못했습니다. 이 경우 발생할 수 있습니다 원격 데이터베이스에서 스크립트를 실행할 수 없습니다. "

> 이 오류는 다양 한 이유로 발생할 수 있습니다. 이 오류를 확인할 수 있습니다 하는 이유 중 하나 이며 경우 데이터베이스 스크립트 문자가 작은따옴표 (') u t F-8로 대상 MySQL 데이터베이스의 기본 문자 집합이 아닙니다.
> 
> **해결 방법**  
> U t F-8로 원격 MySQL 데이터베이스에 대 한 기본 문자를 설정 합니다.


#### <a name="issue-some-links-are-not-visible-in-dotnetnuke-after-publishing-or-downloading-the-site"></a>문제: 일부 링크에에서 표시 되지 않습니다 DotNetNuke 게시 하거나 사이트를 다운로드 한 후

> 게시 하거나 다운로드 DotNetNuke 사이트, 사이트에 표시할 새 링크의 캐시의 선택을 취소 해야 합니다.
> 
> **해결 방법**
> 
> 1. "Host"로 로그인 합니다.
> 2. 호스트 메뉴로 이동 하 고 선택 **호스트 설정**합니다.
> 3. 아래로 스크롤하여 **고급 설정**를 확장 하 고 **성능 설정을**합니다.
> 4. 클릭 합니다 **캐시 지우기** 페이지에 대 한 링크입니다.
> 5. 페이지 아래쪽으로 이동한 다음 응용 프로그램을 다시 시작 합니다.


#### <a name="issue-some-links-in-atomsite-are-broken-after-you-download-a-published-site"></a>문제: 게시 된 사이트를 다운로드 한 후 인 AtomSite의 일부 링크 중단 됩니다.

> **해결 방법**  
> *service.config* 파일인 *users.config* 파일 및 모든 *.xml* 파일을 대체 URL 문자열 (예를 들어, `http://myhost.com/atomsite`)을 로컬 (예를 들어 `http://localhost:1239`).


#### <a name="issue-mysql-based-applications-like-wordpress-fail-to-publish-and-report-a-database-error"></a>문제: WordPress와 같은 MySQL 기반 응용 프로그램을 게시 하 고 데이터베이스 오류를 보고 실패

> 기본적으로 WebMatrix에서 utf-8 문자 집합을 사용 하 여 MySQL을 설치합니다. 직접 MySQL을 설치 하 고 문자 집합을 u t F-8 없는 경우 (예를 들어 인 Latin1) 데이터베이스에 대 한 게시 프로세스가 실패할 수 있습니다.
> 
> **해결 방법**
> 
> 1. U t F-8로 MySQL의 문자 집합을 변경 합니다. (세부 정보를 참조 하세요 [서버 문자 집합 및 데이터 정렬](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html) MySQL 웹 사이트의.)
> 2. 응용 프로그램을 다시 설치 합니다.
> 3. 응용 프로그램을 다시 게시 합니다.


#### <a name="issue-download-published-site-fails-for-applications-that-have-browser-based-setup"></a>문제: "다운로드 사이트를 게시 하는 데 사용" 응용 프로그램을 브라우저 기반 설치에 대 한 실패

> 일부 응용 프로그램 (예: Kentico CMS) 데이터베이스 만들기 같은 설치 후 설치를 수행 하기 위해 브라우저에서 시작 해야 합니다. 다음과 같은 브라우저 기반 설치를 완료 하지 않고 응용 프로그램을 게시 하는 경우 원격 서버에서 같은 사이트를 다운로드 하려는 시도 실패 합니다.
> 
> **해결 방법**  
> 사이트를 게시 하기 전에 브라우저 기반 설치를 완료 합니다.


#### <a name="issue-download-published-site-fails-with-a-database-error-for-dotnetnuke-and-kooboo-cms"></a>문제: "다운로드 사이트를 게시 하는 데 사용" DotNetNuke 및 Kooboo CMS에 대 한 데이터베이스 오류와 함께 실패

> 서버에서 응용 프로그램을 다운로드 하려는 경우 및 관리자 자격 증명에서 데이터베이스 연결 문자열에는 **게시 설정** 대화 상자에서 게시 로그에 다음 오류가 표시 될 수 있습니다.
> 
> [!code-console[Main](overview/samples/sample9.cmd)]
> 
> **해결 방법**  
> 실제 환경인 경우 사이트를 다시 게시 (또는 게시) 데이터베이스에 대 한 비관리자 자격 증명을 사용 합니다.


<a id="More_Info"></a>

## <a name="for-more-information"></a>자세한 내용

WebMatrix 1.0에 대 한 자세한 내용은 다음 웹 사이트를 참조 하세요.

- [IIS.net](http://iis.net/)
- [ASP.NET](https://asp.net/webmatrix)
- [Microsoft.com/web](https://www.microsoft.com/web)

© 2011 Microsoft Corporation. All Rights Reserved. [사용 약관](https://msdn.microsoft.cos/cc300389.aspx)합니다.
