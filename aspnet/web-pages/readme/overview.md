---
uid: web-pages/readme/overview
title: WebMatrix 추가 정보 | Microsoft Docs
author: rick-anderson
description: WebMatrix 및 ASP.NET 웹 페이지 (Razor) 1.0 릴리스 추가 정보
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/06/2011
ms.topic: article
ms.assetid: 36c5beeb-45a7-48a0-9c30-f82cdf5c5f5f
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/readme
msc.type: content
ms.openlocfilehash: c65ee58b8c13b0b4acb6e7c9b631c8235e791506
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
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

> Microsoft WebMatrix 1.0은 분에 설치 하는 무료 웹 개발 스택입니다. 데이터베이스와 프로그래밍 프레임 워크를 하나의 통합 된 환경을 만들려면 웹 서버를 통합 합니다. WebMatrix를 사용 하 여 코드, 테스트 및 고유한 ASP.NET 또는 PHP 웹 사이트를 게시 하는 방법을 간소화할 수 있습니다 또는 DotNetNuke, Umbraco, WordPress 또는 Joomla와 같은 인기 있는 오픈 소스 응용 프로그램을 사용 하 여 새 웹 사이트를 시작 하려면 WebMatrix를 사용할 수 있습니다. WebMatrix에는 같은 강력한 웹 서버, 데이터베이스 엔진 및 매끄럽고 원활 하 게 개발에서 프로덕션으로 전환 하는 인터넷에서 웹 사이트를 실행 하는 프레임 워크 환경을 사용 합니다.


<a id="Installation_Notes"></a>

## <a name="installation"></a>설치

> WebMatrix 1.0을 설치 하려면 먼저 설치 해야는 [Microsoft 웹 플랫폼 설치 관리자 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)합니다. 웹 플랫폼 설치 관리자를 설치한 후에 WebMatrix를 설치할 사용할 수 있습니다.
> 
> 을 설치 하는 동안 문제가 있는 경우 참조 [Microsoft 웹 플랫폼 설치 관리자 문제 해결](https://go.microsoft.com/fwlink/?LinkId=196212)합니다.


<a id="InstructionsForPublishingApplications"></a>
## <a name="how-to-publish-applications"></a>응용 프로그램을 게시 하는 방법

> 참조 [응용 프로그램을 게시 하기 위한 단계별 지침](https://go.microsoft.com/fwlink/?LinkID=196149)


<a id="ChangesAndIssues"></a>

## <a name="changes-and-issues"></a>변경 내용 및 문제

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-10-installation-issues"></a>WebMatrix 1.0 설치 문제

#### <a name="issue-webmatrix-10-is-available-only-on-platforms-that-support-microsoft-net-framework-4"></a>문제: 1.0 WebMatrix는 Microsoft.NET Framework 4를 지 원하는 플랫폼 에서만 사용할 수

> .NET Framework 버전 4는 WebMatrix에 필요 합니다. 경우에 따라 WebMatrix 1.0 설치 관리자는 있도록 지원 되는 구성 집합의 포함 되지 않은 플랫폼에 설치 하려고 합니다. 특히, Windows Vista SP1 업데이트 없이 하면 WebMatrix 설치 하기 하지만.NET Framework 4 구성 요소 실패 하 고 설치를 차단 됩니다.
> 
> **해결 방법**  
> 포함 된 지원 되는 플랫폼에 설치 합니다.
> 
> - Windows 7
> - Windows Server 2008
> - Windows Server 2008 R2
> - Windows Vista SP1 이상
> - Windows XP SP3
> - Windows Server 2003 SP2


#### <a name="issue-cannot-install-webmatrix-10-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a>문제: Microsoft Visual Studio 2008 Microsoft Visual Studio 2008 SP1 없이 설치 된 경우 WebMatrix 1.0을 설치할 수 없습니다.

> **해결 방법**  
> 설치 [Microsoft Visual Studio 2008 s p 1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) Microsoft 다운로드 센터에서.


#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a>문제: SQL Server Compact 4.0에 대 한 일부 어셈블리는 GAC에 설치 되지 않은

> SQL Server Compact 4.0에 대 한 관리 되는 어셈블리를 전역 어셈블리 캐시 (GAC)에 배치 되지 64 비트 컴퓨터에서 SQL Server Compact 4.0을 설치 하 고 컴퓨터에만.NET Framework 3.5 SP1 Client Profile 설치 합니다. GAC에 설치 되지 않은 관리 되는 어셈블리에는
> 
> - *System.Data.SqlServerCe.dll* (ADO.NET 공급자)
> - *System.Data.SqlServerCe.Entity.dll* (ADO.NET Entity Framework)
> 
> **해결 방법**  
> 제거할 SQL Server Compact 4.0입니다. 다운로드 하 고 다음 위치에서.NET Framework 3.5 s p 1의 정식 버전을 설치 합니다.  
>   
> [Microsoft.NET Framework 3.5 서비스 팩 1 (전체 패키지)](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> SQL Server Compact 4.0를 다시 설치 합니다.


#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a>문제: SQL Server Compact는 명령줄을 사용 하 여 제거할 수 없습니다.

> SQL Server Compact 명령줄 옵션을 사용 하 여 제거가 릴리스에서 작동 하지 않습니다.
> 
> **해결 방법**  
> 사용 하 여 *프로그램 및 기능* Microsoft SQL Server Compact 4.0을 제거 하려면 Windows 제어판에서.


<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a>ASP.NET 웹 페이지

문서의이 섹션에서는 새로운 기능, 변경 및 Razor 구문이 있는 ASP.NET 웹 페이지 1.0 릴리스에서 알려진된 문제를 설명 합니다.

- [새로운 기능](#NewFeatures)
- [변경 내용](#Changes)
- [문제](#Issues)

#### <a id="NewFeatures"></a>  새로운 기능

#### <a name="new-configuration-setting-added-to-disable-the-package-manager"></a>패키지 관리자를 사용 하지 않도록 설정에 구성 설정을 추가 하는 새로운 기능:

> 새 `asp:AdminManagerEnabled` 키에 사용할 수 있는는 `<appSettings>` 요소에는 *web.config* 파일 완전히 패키지 관리자를 사용 하지 않도록 설정할 수 있습니다. 이 요소에 대 한 기본값은 true, 즉에 포함 되지 않은 경우는 *web.config* 패키지 관리자, 파일을 사용 합니다. 패키지 관리자를 사용 하지 않으려면 다음 요소를 추가할는 *web.config* 웹 사이트의 루트에 파일:
> 
> [!code-xml[Main](overview/samples/sample1.xml)]


#### <a id="Changes"></a>  Changes

#### <a name="change-webpagesadminfoldervirtualpath-key-renamed-to-aspadminfoldervirtualpath"></a>변경 사항: "webPages:AdminFolderVirtualPath" 키 "asp: AdminFolderVirtualPath"로 변경

> `webPages:AdminFolderVirtualPath` 에 추가할 수 있는 키의 *web.config* 사용할 패키지 관리자의 위치를 지정 하는 파일의 이름이 변경는 `asp:` 대신 네임 스페이스는 `webPages` 네임 스페이스입니다. 이 요소를 사용한 경우 구성 파일에서 이름을 바꿀 해야 있습니다.


#### <a id="Issues"></a>  알려진된 문제

#### <a name="issue-passwords-for-membership-users-no-longer-recognized"></a>더 이상 인식 하지 멤버 자격 사용자에 대 한 암호 문제:

> 보안을 만들고 구성원 (로그인) 암호를 저장 하기 위한 알고리즘 변경 되었습니다. 결과적으로, ASP.NET Razor의 베타 버전에서 만든 멤버 (사용자)에 대 한 저장 된 암호는 인식 되지 않습니다. 
> 
> **해결 방법** 사이트 프로덕션에 아직 삽입 되지에 멤버 자격 데이터베이스에서 사용자 레코드를 제거 합니다. 라이브 데이터베이스의 경우에 프로그래밍 방식으로 멤버 자격 데이터베이스에 기존 암호 다시 생성 합니다.


#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a>문제: 예기치 않은 동작이 멤버 자격에 대 한 사용자 지정 사용자 테이블을 사용 하는 경우

> 호출에서 ASP.NET Razor 웹 사이트에 대 한 멤버 자격 공급자를 초기화 하려면는 `WebSecurity.InitializeDatabaseConnection` 메서드. (시작 사이트 템플릿의 WebMatrix에서이 메서드에 대 한 호출을 포함 된  *\_AppStart.cshtml* 파일입니다.) 경우는 `autoCreateTables` 이 메서드의 매개 변수를 설정을 true로 (기본적으로 설정은 시작 사이트 템플릿의에서 true), 하며 메서드는 인식할 수 없는 테이블 이름 (두 번째 매개 변수)는 메서드에 전달 되 면 오류가 발생 하지 않습니다. 대신, 테이블이 자동으로 만들어집니다.
> 
> 멤버 자격에 대 한 사용자 지정 사용자 테이블을 사용 하지만 잘못 된 테이블을 이름을 전달 하려는 경우이 문제가 될 수는 `WebSecurity.InitializeDatabaseConnection` 메서드. 메서드가 발생 하지 않으므로 기본적으로 오류가 지정한 테이블이 없는 경우 및 대신 새 테이블을 만들기 때문에 응용 프로그램 작동 나타날 수 있습니다. 그러나 응용 프로그램 코드에 사용자 지정 사용자 테이블 (및 그 안에 필드에)를 사용 하는 예기치 않은 오류와 함께 결국 실패할 수 있습니다.
> 
> **해결 방법**  
> 이름에 전달 되는지 확인는 `InitializeDatabaseConnection` 사용자 프로필 테이블 멤버 자격 데이터베이스에 또는 다음 사항을 확인 메서드 일치는 `autoCreateTables` 매개 변수를 false로 설정 합니다.


#### <a name="issue-error-message-the-admin-module-requires-access-to-appdata"></a>문제: 오류 메시지 "Admin 모듈 ~/App에 액세스 해야\_데이터"

> 상황에 따라 사용자 만들기 또는 그렇지 않은 경우 ASP.NET 멤버 자격 시스템을 사용 하려고 하면이 오류를 표시 하려면 페이지 *관리 모듈 ~/App에 액세스 해야\_데이터*합니다. IIS 또는 IIS Express에서 실행 중인 계정에 만들고에 쓸 수 있는 권한이 없는 경우이 *앱\_데이터* 웹 사이트 루트 아래의 폴더입니다. 
> 
> **해결 방법** 수동으로 만들는 *앱\_데이터* 웹 사이트에 대 한 폴더입니다. 다음 응용 프로그램 (일반적으로 네트워크 서비스)에서 실행 하는 Windows 계정에 응용 프로그램의 루트 폴더에 대 한 및 앱과 같은 하위 폴더에 대 한 읽기/쓰기 권한이 있는지를 확인\_데이터입니다. 더 자세한 정보는 기술 자료 문서에서 사용할 수 있는 [SQL Server Express 사용자 인스턴스 만들기 및 ASP.net 웹 응용 프로그램 프로젝트 문제](https://support.microsoft.com/kb/2002980)합니다.


#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a>문제: "하지 못했습니다 SQL Server의 사용자 인스턴스를 생성 하려면" 오류

> WebMatrix 웹 응용 프로그램을 SQL Server Express를 사용 하 여 Windows 7 또는 Windows Server 2008 r 2에서 IIS 7.5를 실행 중인 경우 SQL Server가 런타임 시 사용자의 로컬 응용 프로그램 경로 검색할 수 없습니다 되었음을 나타내는 오류가 표시 될 수 있습니다.
> 
> **해결 방법** (일반적으로 네트워크 서비스)에서 응용 프로그램을 실행 하는 Windows 계정에 대 한 응용 프로그램의 루트 폴더 및 하위 폴더에 대 한 읽기/쓰기 권한을 같은 있는지 확인 *앱\_데이터*. 더 자세한 정보는 기술 자료 문서에서 사용할 수 있는 [SQL Server Express 사용자 인스턴스 만들기 및 ASP.net 웹 응용 프로그램 프로젝트 문제](https://support.microsoft.com/kb/2002980)합니다.


#### <a name="issue-files-that-contains-package-manager-resources-or-package-manager-passwords-are-servable-under-iis-60-and-earlier"></a>문제: 파일 리소스 패키지 관리자 또는 패키지 관리자 암호를 포함 하는 IIS 6.0에서 servable 및 이전 버전

> RC2 릴리스를 사용 하 여 만든 ASP.NET 웹 페이지 (Razor) 응용 프로그램을 배포 하 고 응용 프로그램이 포함 되어 있는 경우는 *password.txt* 또는 *packagesources.txt* 파일 */App\_ 데이터/admin*, IIS 6.0 요청 패키지 관리자 인스턴스에 대 한 암호를 잠재적으로 노출 하는 경우이 파일을 제공 합니다. 
> 
> **해결 방법** 이름 바꾸기는 *password.txt* 또는 *packagesources.txt* 파일을 *password.config* 또는 *packagesources.config*. IIS 6.0은 기본적으로는 파일을 제공 하지 않습니다는 *.config* 확장 합니다. (IIS 7에서는에 파일이 *앱\_데이터* 폴더가 처리 되는 파일 이름을 바꿀 필요가 없습니다.)


#### <a name="issue-uninstalling-packages-installed-using-the-beta-3-release-does-not-completely-remove-package-components"></a>문제: Beta 3 릴리스에 사용 하 여 설치 된 패키지 제거 완전히 제거 하지 않습니다 패키지 구성 요소

> Beta 3 릴리스에 패키지 관리자를 사용 하 여 패키지를 설치 하 고 현재 버전을 사용 하 여이 삭제 하려고 하는 경우 패키지가 완전히 제거 되지 않았습니다. 패키지 관리자를 사용 하 여 **제거** 단추 일부 구성 요소를 제거 하지만 패키지의 라이브러리 코드를 유지 하며 업데이트 하지 않습니다는 *package.config* 파일입니다.
> 
> **해결 방법**   
> 이러한 단계를 수행 합니다.  
> 1. 삭제 된 *앱\_Data\packages* 폴더입니다. 모든 패키지를 제거합니다.   
> 2. 삭제 된 *packages.config* 웹 사이트의 루트에 파일입니다.


#### <a name="issue-in-visual-studio-invoking-the-web-based-package-manager-takes-the-application-offline"></a>문제: Visual Studio에서 웹 기반 패키지 관리자를 호출 하는 응용 프로그램 오프 라인

> Visual Studio (하지 WebMatrix)에서 작업 하 고 사용 하는 경우는  *\_admin* , Visual Studio 패키지 관리자를 시작 하는 기능이 응용 프로그램 오프 라인으로 전환 하 고 게시는 *앱\_ offline.htm* 패키지 관리자를 사용 하는 기능을 방해 하 여 웹 사이트 루트입니다.
> 
> [!NOTE]
> 동일한 동작이 수행 추가, 제거 또는에서 모든 파일을 수정 하는 경우 웹 기반 패키지 관리자 인터페이스를 사용 하는 경우에 가장 일반적으로이 문제를 볼 것, 있지만 *앱\_데이터* 폴더입니다.
> 
> **해결 방법**   
> Visual Studio에서 패키지를 사용 하려면 웹 기반 패키지 관리자 대신 NuGet 확장을 사용 합니다. 자세한 내용은 참조는 [NuGet 설명서](https://docs.microsoft.com/nuget/)합니다. 다른 파일로 작업 하는 경우는 *앱\_데이터* 폴더에서이 문제를 방지 하려면 다른 위치로 파일을 유지 하는 것이 좋습니다. 합니다. 삭제 방법이 적절 하지 않은 경우는 *앱\_offline.htm* 파일을 수동으로 또는 자동으로 (기본적으로 30 초 후) 사이트를 다시 온라인 상태가 될 때까지 기다립니다.


#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a>문제: Visual Studio IntelliSense 및 프로젝트 템플릿 ASP.NET MVC 버전 3에만 사용할 수 있는

> 설치 하는 ASP.NET 웹 페이지도 ´ â 도구 Visual Studio에 대 한 ASP.NET 웹 페이지 응용 프로그램에 대 한 IntelliSense 및 프로젝트 템플릿과 같은 합니다.
> 
> **해결 방법** 웹 플랫폼 설치 관리자를 통해 ASP.NET MVC 3 RC 설치 IntelliSense 및 프로젝트 템플릿을 Visual Studio에서 ASP.NET 웹 페이지 응용 프로그램을 사용 하려면 또는 [독립 실행형 설치 관리자](https://go.microsoft.com/fwlink/?LinkID=191797)합니다.


#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a>문제: 프록시 서버를 통해 다른 외부 데이터 나 피드 읽기

> 프록시 서버 뒤에 있는 사이트를 실행 하는 서버가 있는 경우에 대 한 프록시 정보를 구성 해야 할 수도 있습니다는 *web.config* 파일을 사이트 외부의에서 제공 되는 정보를 읽을 수 있습니다. 예를 들어, 사용 하는 경우는 `ReCaptcha` 도우미, 도우미 reCAPTCHA 서비스와 통신 하지만 프록시 서버에 의해 차단 될 수 있습니다. 마찬가지로, 패키지 관리자에서 사용 하는 피드 등 ASP.NET 웹 페이지에서 사용 되는 피드 프록시 구성이 필요할 수 있습니다.
> 
> 외부 서비스를 작업할 또는 피드 패키지 작업에서 문제가 있는 경우 응용 프로그램의 루트에는 다음과 같은 요소가 배치 *web.config* 파일:
> 
> [!code-xml[Main](overview/samples/sample2.xml)]
> 
> 프록시 서버를 구성 하는 방법에 대 한 자세한 내용은 참조 [ &lt;프록시&gt; 요소 (네트워크 설정)](https://msdn.microsoft.com/library/sa91de1e.aspx) MSDN 웹 사이트에 있습니다.


#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a>문제: Razor 구문이 있는 ASP.NET 웹 페이지를 사용 하지 않도록 설정.NET Framework 버전 4 제거 합니다.

> .NET Framework 버전 4 제거한 다음 다시 설치 하는 경우에 Razor 구문이 있는 ASP.NET 웹 페이지 비활성화 됩니다. 와 페이지는 *.cshtml* 확장 제대로 실행 되지 않습니다. 컴퓨터 루트에 있는 어셈블리를 등록 하는 ASP.NET 웹 페이지 *web.config* 파일 및.NET Framework를 제거 합니다. 해당 파일을 제거 합니다. .NET Framework를 다시 설치 하는 구성 파일의 새 버전을 설치 하지만 ASP.NET 웹 페이지 어셈블리에 대 한 참조를 추가 하지 않습니다.
> 
> **해결 방법** .NET Framework를 다시 설치한 후 Razor 구문이 있는 ASP.NET 웹 페이지를 다시 설치 합니다. 이렇게 하면 다음 요소를 추가 *web.config* 일반적으로 다음 위치에 있는 컴퓨터 루트에 파일:  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](overview/samples/sample3.xml)]


#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a>문제: 확장명 없는 Url 찾지 못하면 IIS 7.5 또는 IIS 7에서.cshtml/.vbhtml 파일

> IIS 7 또는 IIS 7.5에서 다음과 같은 URL로 요청은 페이지를 찾을 수는 *.cshtml* 또는 *.vbhtml* 확장:  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> URL 다시 쓰기 해제 되어 기본적으로 IIS 7.5 또는 IIS 7에 대 한 문제가 발생 합니다. 문제일 수 상황은 IIS Express를 사용 하 여 로컬로 테스트할 때 문제가 표시 되지 않으면 하지만 웹 사이트 호스팅 웹 사이트에 배포 하는 경우 발생 합니다.
> 
> **해결 방법**
> 
> - 에 설명 된 업데이트 설치 서버 컴퓨터에서 서버 컴퓨터에 대 한 제어를 있으면 [업데이트를 사용 하면 특정 Url 요청을 처리 하는 IIS 7.0 또는 IIS 7.5 처리기 마침표로 끝나지 않는 ´ ï ´](https://support.microsoft.com/kb/980368)합니다.
> - 서버 컴퓨터에 대 한 제어 없는 경우 (예를 들어를 배포 하는 호스팅 웹 사이트에) 다음을 웹 사이트의 추가 *web.config* 파일: 
> 
>     [!code-xml[Main](overview/samples/sample4.xml)]


#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a>문제: SQL Server Compact 설치 하지 않은 컴퓨터에 응용 프로그램 배포

> SQL Server Compact 데이터베이스를 포함 하는 응용 프로그램 컴퓨터에서 실행할 수 있는 SQL Server Compact 설치 되어 있지 않습니다. Microsoft WebMatrix 1.0에서 자동으로 이러한 이진 파일을 복사 하 고 적절 한 수행 *web.config* 변환 파일입니다.
> 
> **해결 방법** 하 이러한 파일을 복사 하 고 확인 해야 하는 경우는 *web.config* 파일 변경 내용을 수동으로 다음을 수행 합니다.
> 
> 1. 데이터베이스 엔진 어셈블리를 복사는 *Bin* 대상 컴퓨터에 응용 프로그램의 폴더 (및 하위 폴더):  
> 
>    - Copy *C:\Program Files\Microsoft SQL Server Edition\v4.0\Desktop\System.Data.SqlServerCe.dll*   
>        **to** *\Bin*
>    - Copy <em>C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\</em><strong><em>to</em></strong>\Bin\x86*
>    - Copy <em>C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\</em>* <strong>to</strong><em>\Bin\amd64</em>
> 
> 2. 웹 사이트의 루트 폴더에 작성 하거나 열을 *web.config* 파일입니다. (이 파일 형식은 WebMatrix 1.0에서 클릭 하면 사용할 수는 **모든** 에 **파일 형식을 선택** 대화 상자.)
> 3. 다음 요소를 자식으로 추가 된 `<configuration>` 요소 (에 포함 되지 않은 `<system.web>` 요소):
> 
>     [!code-xml[Main](overview/samples/sample5.xml)]


#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a>문제: "Database" 및 "WebGrid" 도우미 Visual Basic에서는 보통 신뢰에서 작동 하지 않음

> Visual Basic을 사용 하는 경우 (만드는 *.vbhtml* 파일), `Database` 및 `WebGrid` 도우미에는 보통 신뢰를 사용 하도록 설정 되어 있는 경우 작동 하지 것입니다.
> 
> **해결 방법**  
> Visual Studio 2010을 사용 하는 경우에 서비스 팩 1 릴리스를 설치 하 여이 문제를 해결할 수 있습니다. SP1 릴리스의 최종 버전 있을 때까지에서 s p 1의 베타 버전을 다운로드할 수 있습니다는 [Microsoft Visual Studio 2010 서비스 팩 1 베타](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en) Microsoft 다운로드 센터 페이지입니다.   
>   
> 이 방법은 실용적이 지 않거나 Visual Studio 2010을 사용 하지 않으면 하면 일시적으로 완전 신뢰를 사용 하도록 응용 프로그램을 설정 합니다.


#### <a name="issue-applicationpart-resources-are-externally-accessible"></a>문제: "ApplicationPart" 리소스는 외부에서 액세스할 수

> 어셈블리에서 파생 되는 개체를 포함 하는 경우는 `ApplicationPart` 클래스, 어셈블리의 리소스에 의해 노출 되는 `ResourceRouteHandler` 클래스입니다. 예를 들어 다음 URL을 가정해 봅니다.  
>   
> `~/r.ashx/System.Web.WebPages.Administration/Resources/AdminResources.resources`  
>   
> 이 요청에 리소스 문자열의 모든 다운로드는 *System.Web.WebPages.Administration.dll* 어셈블리입니다. (붙지 않은으로 정적 콘텐츠가 담긴 서비스할 수 없도록 되어) 포함 된 리소스를 모두 다운로드 됩니다. 포함 된 리소스에 중요 한 정보가 포함 되어 보안 위험을 초래할 수 있습니다이 합니다. 
> 
> **해결 방법**   
> 만드는 경우는 **ApplicationPart** 개체 포함된 하는 리소스와 연결 된 선택 되어 있는지 확인 합니다 **ApplicationPart** 어셈블리 개체의 중요 한 정보가 포함 되지 않습니다.


<a id="Known_Issues_WebMatrix"></a>

### <a name="webmatrix"></a>WebMatrix

> [!NOTE]
> WebMatrix에 대 한 설치 문제에 대 한 정보를 참조 하십시오. [WebMatrix 설치 문제](#Known_Issues_Installation) 이 문서의 앞부분에 설명 합니다.


문서의이 섹션에서는 WebMatrix 개발 환경에 대 한 알려진된 문제를 설명 합니다.

#### <a name="issue-changes-in-the-username-or-password-of-a-database-connection-string-in-a-webconfig-file-are-not-reflected-in-the-databases-workspace"></a>문제: 데이터베이스 작업 영역에 사용자 이름 또는 web.config 파일에서 데이터베이스 연결 문자열의 암호 변경 내용이 반영 되지 않습니다.

> **해결 방법**  
> 
> 1. 에 *web.config* 파일에서 연결 문자열에 데이터베이스 이름 변경 (예를 들어를 "1" 추가).
> 2. 저장 된 *web.config* 파일입니다.
> 3. 클릭 **데이터베이스** 새로 고칩니다.
> 4. 연결 문자열에 데이터베이스 이름을 변경 하는 *web.config* 다시 원래 데이터베이스 이름으로 파일입니다.
> 5. 저장 된 *web.config* 파일입니다.
> 6. 클릭 **데이터베이스** 새로 고칩니다.


#### <a name="issue-folders-created-by-webmatrix-cannot-be-deleted"></a>문제: WebMatrix에서 만든 폴더를 삭제할 수 없습니다.

> WebMatrix는 관리자 권한으로 실행 되는 경우 (즉, WebMatrix를 사용 하 여 시작 하는 **관리자 권한으로 실행** Windows 옵션), Windows 탐색기를 사용 하 여 WebMatrix가 만든 폴더를 삭제할 수 없습니다.
> 
> **해결 방법**  
> 승격 된 권한을 사용 하 여 Windows 탐색기를 실행 합니다. 아래 단계를 수행합니다.  
> 
> 1. Windows에서 **시작**합니다.
> 2. "Windows 탐색기"를 입력 하 고에 대 한 항목을 마우스 오른쪽 단추로 클릭 **Windows 탐색기**합니다.
> 3. 클릭 **관리자 권한으로 실행**합니다. 폴더를 삭제할 수 있습니다.


#### <a name="issue-webmatrix-10-is-unable-to-perform-certain-tasks-that-require-elevation"></a>문제: 1.0 WebMatrix는 권한 상승이 필요는 특정 작업을 수행할 수 없습니다.

> WebMatrix 1.0가 다음과 같은 상황에서 추가 구성 요소를 설치 하는 등 상승이 필요한 특정 작업을 수행할 수 없습니다.
> 
> - Windows Vista 또는 Windows 7에서 관리자 권한이 없는 계정으로 로그인 및 사용자 계정 컨트롤 (UAC)을 사용할 수 없습니다.
> - Microsoft Windows XP 또는 Microsoft Windows Server 2003을 사용 하 고 있습니다.
> 
> **해결 방법**  
> WebMatrix 1.0에서 대부분의 작업 관리 권한이 필요 하지 않습니다. 않은에 대 한 다음이 단계를 수행 또는 관리자는 작업을 수행할 수 있습니다.
> 
> - Windows Vista 또는 Windows 7에서 UAC를 사용 하도록 설정 합니다.
> - Windows XP에서 Administrators 보안 그룹에 사용자를 추가 합니다.


#### <a name="issue-site-from-web-gallery-is-disabled"></a>문제: "사이트에서 웹 갤러리"을 사용할 수 없습니다.

> **웹 갤러리에서 사이트** 웹 플랫폼 설치 관리자 3.0이 설치 되지 않은 경우 옵션은 사용할 수 없습니다.
> 
> **해결 방법**  
> 설치는 [Microsoft 웹 플랫폼 설치 관리자 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)합니다.


#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a>문제: Google Chrome 실행 옵션으로 지원 되지 않습니다.

> Google Chrome 브라우저에서 목록에 표시 되지 않습니다 **실행** 에 **홈** 탭 합니다.
> 
> **해결 방법**  
> Google Chrome의 일부 버전에서는 등록 하지 않습니다 스스로 제대로 Windows의 기본 프로그램 기능. 이 문제를 해결 Google Chrome 시작을 클릭는 *사용자 지정 및 Google Chrome 제어* 메뉴에서 클릭 *옵션*, 클릭 하 고 *확인 Google Chrome 내 기본 브라우저*합니다.


#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a>문제: "외래 키" 대화 상자 허용 하지 않습니다는 기본 키를 입력 합니다.

> **외래 키** 대화 상자에서 기본 키 테이블의 기본 키 이름을 입력 하 수 없습니다.
> 
> **해결 방법**  
> 이 의도적입니다. 기본 키 테이블에서 기본 키의 이름을 입력 하 고 필요가 없습니다.


#### <a name="issue-intellisense-is-not-available-in-webmatrix-for-razor-syntax-c-or-visual-basic"></a>문제: IntelliSense를 Razor 구문, C# 또는 Visual Basic 용 WebMatrix에서 사용할 수 없습니다.

> HTML 및 CSS에 대 한 WebMatrix에서 IntelliSense가 지원 됩니다. 그러나, 다른 언어에 대 한 가능 하지 않습니다. 
> 
> **해결 방법**   
> 없음


#### <a name="issue-intellisense-for-html-and-css-suggests-elements-that-are-not-contextually-appropriate"></a>문제: HTML 및 CSS에 대 한 IntelliSense 제안 컨텍스트에 적절 하지 않은 요소

> WebMatrix에서 태그에 대 한 IntelliSense를 사용 하 여 HTML 지원는 [XHTML 1.0 변환 스키마](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional) CSS를 사용 하 고는 [CSS 2.1 스키마](http://www.w3.org/TR/CSS2/)합니다. IntelliSense는 이러한 특정 스키마를 기반으로, 특정 태그, 특성 또는 속성 수 수 제안 현재 페이지 또는 스타일 정의에 적합 하지 않습니다. HTML, 잘못 된 형식의 XHTML (예: 태그가 닫혀 있지 않은 경우)로 해석 될 수 있는 내용에 예기치 않은 제안에도 발생할 수 있습니다. 이 문제는 불완전 한 태그; 안에 삽입 지점이 있으면 따라 더 두드러질 수 있습니다. 이 경우 IntelliSense 새 태그를 열어 제안 또는 다른 잘못 된 제안을 제공 될 수 있습니다. 
> 
> **해결 방법**   
> HTML, 잘 구성 된, 전체 XHTML 페이지 내에서 작업 하는 것이 있는지 확인 합니다. CSS에 대 한 해결 방법이 없습니다.


#### <a name="issue-intellisense-is-not-invoked-while-you-type"></a>문제: 입력 하는 동안 IntelliSense가 호출 되지 않았습니다.

> 때로는 HTML 또는 CSS 편집기에 입력 되 고 IntelliSense는 호출 하지 수도 있습니다. 특히, 다른 요소 옆에 있는 직접 또는 파일의 끝에 삽입 포인터를 때 발생할 수 있습니다. 
> 
> **해결 방법**   
> 커서 주위에 공백을 인지 하며 삽입 지점 파일의 끝에 아닌지 확인 합니다. 또한 Ctrl + 스페이스바를 눌러 IntelliSense를 수동으로 호출할 수 있습니다.


#### <a name="issue-no-ui-is-available-for-disabling-intellisense"></a>문제: UI ´ ü ± IntelliSense를 사용 하지 않도록 설정

> WebMatrix 1.0 IntelliSense를 사용 하지 않도록 설정 하는 것에 대 한 UI 또는 제스처를 제공 합니다. 
> 
> **해결 방법**   
> IntelliSense를 사용 하지 않도록 설정 하는 스위치를 포함 하는 다음 명령을 사용 하 여 WebMatrix를 시작 합니다.  
>   
> `WebMatrix.exe #ExecuteCommand# EditorIntelliSense off`


<a id="Known_Issues_IISExpress"></a>
### <a name="iis-express"></a>IIS Express

IIS Express에 다음 URL에서 사용할 수 있는 추가 정보 파일을 사용 하는 자체 있습니다.

[https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409)

<a id="Known_Issues_SQLServerCompact"></a>

### <a name="sql-server-compact"></a>SQL Server Compact

SQL Server Compact는 다음 URL에서 사용할 수 있는 추가 정보 파일을 사용 하는 자체에 있습니다.

[https://go.microsoft.com/fwlink/?LinkID=208545](https://go.microsoft.com/fwlink/?LinkID=208545&amp;clcid=0x409)

WebMatrix의 일부로 SQL Server Compact 설치와 관련 된 문제에 대 한 정보를 참조 하십시오. [WebMatrix 설치 문제](#Known_Issues_Installation) 이 문서의 앞부분에 설명 합니다.

### <a id="Known_Issues_Installing_Applications"></a>  응용 프로그램 설치

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a>문제: 응용 프로그램을 설치는 시간이 오래 걸릴 수는 사용자의 내 문서 폴더를 네트워크 공유로 리디렉션되면

> **해결 방법**  
> 없음 응용 프로그램을 설치 하려면 시간이 오래 걸릴 수 있지만 제대로 설치 됩니다.


### <a id="Known_Issues_Publishing_Applications"></a>  응용 프로그램 게시

#### <a name="issue-required-permissions-cannot-be-acquired-error-when-publishing-a-sql-compact-database"></a>문제: "는 데 필요한 권한을 얻을 수 없습니다" 오류 SQL Compact 데이터베이스를 게시 하는 경우

> WebMatrix는 보통 신뢰 구성을 사용 하 여.NET Framework 버전 3.5 실행 중인 서버에 SQL Server Compact에 대 한 지원 이진 파일을 배포 완벽 하 게 지원 하지 않습니다.
> 
> **해결 방법**  
> 기본적인된 해결 방법은 서버에서.NET Framework 4를 설치 하는 것입니다. 또는 다음을 수행 합니다.
> 
> 1. 다음 요소를 추가 하는 `SecurityClasses` 섹션 *웹\_MediumTrust.config* 파일:
> 
>     [!code-html[Main](overview/samples/sample6.html)]
> 2. 새 권한 집합을 만들기는 *웹\_MediumTrust.config* 다음 필수 권한 가진 파일:
> 
>     [!code-html[Main](overview/samples/sample7.html)]
> 3. 다음 요소를 삽입 하 여 SQL Server Compact로 설정 하는 권한이 적용 된 *웹\_MediumTrust.config* 파일:
> 
>     [!code-html[Main](overview/samples/sample8.html)]


#### <a name="issue-gallery-and-phpbb-web-applications-display-a-service-is-unavailable-error-after-publishing"></a>문제: 웹 응용 프로그램 갤러리 및 PhpBB "서비스를 사용할 수 없습니다." 오류를 게시 한 후 표시

> 상황에 따라 응용 프로그램을 게시 하면 "서비스를 사용할 수 없습니다." 오류가 발생 합니다.
> 
> **해결 방법**  
> WebMatrix에서 백슬래시를 추가 (\) 에서 서버 이름의 끝에는 **게시 설정** 창 다음 응용 프로그램을 다시 게시 합니다.


#### <a name="issue-moodle-website-layout-and-links-are-broken-after-publishing"></a>문제: Moodle 웹 사이트의 레이아웃과 링크는 예측할 수 게시 한 후

> Moodle 응용 프로그램을 게시 한 후 응용 프로그램이 제대로 작동 하지 않습니다.
> 
> **해결 방법**  
> WebMatrix에서 슬래시 (/)의 끝에 추가 **사이트 이름** 필드에 **게시 설정** 창 다음 응용 프로그램을 다시 게시 합니다.


#### <a name="issue-publishing-nopcommerce-fails-with-a-database-error"></a>문제: nopCommerce 게시 데이터베이스 오류와 함께 실패 함

> 게시 nopCommerce는 실패 하 고 같은 데이터베이스 오류를 보고 "는 nop 삽입할\_로그 table이 실패 했습니다."
> 
> **해결 방법**  
> 
> 1. WebMatrix에서 클릭 **실행** 를 로컬로 nopCommerce를 시작 합니다.
> 2. 관리 페이지에 로그인 합니다.
> 3. 클릭는 **시스템** 메뉴.
> 4. 클릭는 **로그** 옵션입니다.
> 5. 클릭는 **로그 지우기** 단추입니다.
> 6. NopCommerce를 다시 게시 합니다.


#### <a name="issue-silverstripe-cms-displays-a-http-500-php-fcgi-error-when-you-download-a-published-site"></a>문제: Silverstripe CMS 표시는 "HTTP 500 PHP FCGI 오류" 게시 된 사이트를 다운로드 하는 경우

> **해결 방법**  
> 클릭 한 후 **다운로드 사이트 게시**, 건너뛸 `silverstripe-cache/manifest_main` 에 **제작 미리 보기**합니다. 이 파일에는 캐싱 목적으로 사용 되며 각 컴퓨터에 특정 합니다.


#### <a name="issue-subtext-displays-server-error-in--application-when-you-download-a-published-site"></a>문제: Subtext 표시 "서버 오류 '/' 응용 프로그램 에서" 게시 된 사이트를 다운로드 하는 경우

> **해결 방법**  
> 사이트의을 열고 *web.config* 파일 및 사용자 ID 및 데이터베이스 연결 문자열에 암호 ("sa" 자격 증명)의 SQL Server 관리자 자격으로 바꿔야 합니다.
> 
> 로그인 하는 사용자 계정에 부여 하려면 다음이 단계를 수행 또는 `db_owner` 사용 권한:
> 
> 1. 웹 플랫폼 설치 관리자를 사용 하 여 SQL Server Management Studio를 설치 합니다.
> 2. 로컬 SQL Server Express 인스턴스에 연결 (기본적으로 `.\SQLEXPRESS`).
> 3. 클릭 **데이터베이스** &gt; *[localSubtextDatabase]* &gt; **보안** &gt; **사용자** &gt; *[localSubtextUser*] (기본값은 `subtextuser`]를 클릭 **속성**합니다.
> 4. 선택 **db\_소유자** 역할 멤버 자격 섹션에 있습니다.


#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a>문제: 사이트 "대상 URL" 필드는 http:// 또는 https://로 시작 하지 않는 경우 게시 한 후 작동 하지 않을 수 있습니다.

> 에 **게시 설정을** 대화 상자에서 대상 URL로 시작 하지 않으면 `http://` 또는 `https://`, 사이트 배포 후 작동 하지 않을 수 있습니다.
> 
> **해결 방법**  
> 있는지 확인 하는 사이트에서 대상 URL을 게시 하기 전에 **게시 설정** 로 대화 상자 시작 `http://` 또는 `https://`합니다.


#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a>문제: MySQL 데이터베이스를 게시 실패 및 오류 발생 "데이터베이스를 게시 하지 못했습니다. 이러한 상황은 원격 데이터베이스가 스크립트를 실행할 수 없습니다. "

> 오류에 대 한 다양 한 이유로 발생할 수 있습니다. 이 오류를 볼 수는 한 가지 이유가 경우에 작은따옴표 문자 (')를 포함 하는 데이터베이스 스크립트 대상 MySQL 데이터베이스의 기본 문자 집합을 u t F-8 않습니다.
> 
> **해결 방법**  
> 기본 문자 집합 원격 MySQL 데이터베이스에 u t F-8로 설정 합니다.


#### <a name="issue-some-links-are-not-visible-in-dotnetnuke-after-publishing-or-downloading-the-site"></a>문제: 일부 링크에에서 표시 되지 않는 DotNetNuke 게시 하거나 사이트를 다운로드 한 후

> 게시 하거나 DotNetNuke 사이트를 다운로드 하는 경우 사이트에 표시할 새 링크의 캐시를 지우려면 할 수 있습니다.
> 
> **해결 방법**
> 
> 1. "호스트"로 로그인 합니다.
> 2. 호스트 메뉴로 이동 하 고 선택 **호스트 설정**합니다.
> 3. 아래로 스크롤하여 **고급 설정**를 확장 하 고 **성능 설정**합니다.
> 4. 클릭는 **캐시 지우기** 페이지에 대 한 링크입니다.
> 5. 페이지의 아래쪽으로 이동한 다음 응용 프로그램을 다시 시작 합니다.


#### <a name="issue-some-links-in-atomsite-are-broken-after-you-download-a-published-site"></a>문제: AtomSite의 일부 링크는 예측할 수는 게시 된 사이트를 다운로드 한 후

> **해결 방법**  
> 에 *service.config* 파일인 *users.config* 파일 및 모든 *.xml* URL 문자열을 대체 하는 파일 (예를 들어 `http://myhost.com/atomsite`)을 로컬 (예를 들어 `http://localhost:1239`).


#### <a name="issue-mysql-based-applications-like-wordpress-fail-to-publish-and-report-a-database-error"></a>문제: WordPress 처럼 MySQL 기반 응용 프로그램을 게시 하 고 데이터베이스 오류를 보고 실패

> 기본적으로 WebMatrix u t F-8 문자 집합으로 MySQL을 설치합니다. 직접 MySQL을 설치를 사용할 수 없으면 u t F-8 문자 집합 (예를 들어이 라틴어 1), 데이터베이스에 대 한 게시 프로세스가 실패할 수 있습니다.
> 
> **해결 방법**
> 
> 1. 문자 집합을 u t F-8로 MySQL에 대 한를 변경 합니다. (세부 정보를 참조 하십시오. [서버 문자 집합 및 데이터 정렬](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html) MySQL 웹사이트에서.)
> 2. 응용 프로그램을 다시 설치 합니다.
> 3. 응용 프로그램을 다시 게시 합니다.


#### <a name="issue-download-published-site-fails-for-applications-that-have-browser-based-setup"></a>문제: "다운로드 사이트를 게시 하는 데 사용" 응용 프로그램 브라우저 기반 설치에 실패 함

> 일부 응용 프로그램 (예를 들어 Kentico CMS) 데이터베이스 만들기 같은 설치 후 설치를 수행 하기 위해 브라우저에서 시작 해야 합니다. 브라우저 기반 설치를 완료 하지 않고 이와 같은 응용 프로그램을 게시 하는 경우 원격 서버에서 같은 사이트를 다운로드 하는 실패 합니다.
> 
> **해결 방법**  
> 사이트를 게시 하기 전에 브라우저 기반 설치를 완료 합니다.


#### <a name="issue-download-published-site-fails-with-a-database-error-for-dotnetnuke-and-kooboo-cms"></a>문제: "다운로드 사이트를 게시 하는 데 사용" DotNetNuke 및 Kooboo CMS에 대 한 데이터베이스 오류와 함께 실패 함

> 서버에서 응용 프로그램을 다운로드 하려고 하 고 관리자 자격 증명에서 데이터베이스 연결 문자열에 있는 경우는 **게시 설정** 대화 상자에서 게시 로그에서 다음 오류가 표시 될 수 있습니다.
> 
> [!code-console[Main](overview/samples/sample9.cmd)]
> 
> **해결 방법**  
> 실제 환경인 경우 사이트를 다시 게시 (또는 게시 된) 데이터베이스에 대 한 관리자가 아닌 자격 증명을 사용 합니다.


<a id="More_Info"></a>

## <a name="for-more-information"></a>자세한 내용

WebMatrix 1.0에 대 한 자세한 내용은 다음 웹 사이트를 참조 하십시오.

- [IIS.net](http://iis.net/)
- [ASP.NET](https://asp.net/webmatrix)
- [Microsoft.com/web](https://www.microsoft.com/web)

© 2011 Microsoft Corporation. All Rights Reserved. [사용 약관](https://msdn.microsoft.cos/cc300389.aspx)합니다.
