---
uid: web-pages/readme/beta3
title: "웹 매트릭스 및 ASP.NET 웹 페이지 (Razor) Beta 3 릴리스에 추가 정보 | Microsoft Docs"
author: rick-anderson
description: "웹 매트릭스 및 ASP.NET 웹 페이지 (Razor) Beta 3 릴리스에 추가 정보"
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/10/2011
ms.topic: article
ms.assetid: ffa3d5c9-91e5-4da3-b409-560b0c7fbbf0
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/readme/beta3
msc.type: content
ms.openlocfilehash: def2f4b3e54c8de539e10c1b526a1dababeca8fb
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="web-matrix-and-aspnet-web-pages-razor-beta-3-release-readme"></a>웹 매트릭스 및 ASP.NET 웹 페이지 (Razor) Beta 3 릴리스에 추가 정보
====================
> 웹 매트릭스 및 ASP.NET 웹 페이지 (Razor) Beta 3 릴리스에 추가 정보

2010 년 11 월 9

## <a name="contents"></a>목차

- [개요](#Overview)
- [설치](#Installation_Notes)
- [새 기능, 변경 및 Beta 3 릴리스에의 알려진 문제](#Known_Issues)

    - [WebMatrix 설치 문제](#Known_Issues_Installation)
    - [ASP.NET 웹 페이지 2](#Known_Issues_ASPNET)
    - [SQL Server Compact](#Known_Issues_SQL_Server_Compact)
    - [응용 프로그램 설치](#Known_Issues_Installing_Applications)
    - [응용 프로그램 게시](#Known_Issues_Publishing_Applications)
    - [기타 문제](#Known_Issues_Other_Issues)
- [자세한 내용은](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a>개요

> Microsoft WebMatrix 베타는 분에 설치 하는 무료 웹 개발 스택입니다. 데이터베이스와 프로그래밍 프레임 워크를 하나의 통합 된 환경을 만들려면 웹 서버를 통합 합니다. WebMatrix 베타를 사용 하 여 코드, 테스트 및 고유한 ASP.NET 또는 PHP 웹 사이트를 게시 하는 방법을 간소화할 수 있습니다 또는 DotNetNuke, Umbraco, WordPress 또는 Joomla와 같은 인기 있는 오픈 소스 응용 프로그램을 사용 하 여 새 웹 사이트를 시작 하려면 WebMatrix 베타를 사용할 수 있습니다. WebMatrix 베타 같은 강력한 웹 서버, 데이터베이스 엔진 및 매끄럽고 원활 하 게 개발에서 프로덕션으로 전환 하는 인터넷에서 웹 사이트를 실행 하는 프레임 워크 환경을 사용 합니다.


<a id="Installation_Notes"></a>

## <a name="installation"></a>설치

> 사용 하면 WebMatrix Beta 3를 설치 하려면 [Microsoft 웹 플랫폼 설치 관리자 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)합니다. 웹 플랫폼 설치 관리자를 설치한 후에 WebMatrix Beta 3을 설치 하려면 사용할 수 있습니다.
> 
> 을 설치 하는 동안 문제가 있는 경우 참조 [Microsoft 웹 플랫폼 설치 관리자 문제 해결](https://go.microsoft.com/fwlink/?LinkId=196212)합니다.


<a id="Installation_Notes0"></a>

## <a name="instructions-for-publishing-applications"></a>응용 프로그램을 게시 하기 위한 지침

> 참조 [응용 프로그램을 게시 하기 위한 단계별 지침](https://go.microsoft.com/fwlink/?LinkID=196149)


<a id="Known_Issues"></a>

## <a name="new-features-changes-andknown-issues"></a>새로운 기능을 변경, andKnown 문제

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-beta-3-installation"></a>WebMatrix 베타 3 설치

#### <a name="issue-webmatrix-beta-3-is-only-available-on-platforms-that-support-microsoft-net-framework-4"></a>문제: WebMatrix 베타 3은 Microsoft.NET Framework 4를 지 원하는 플랫폼에서 사용할 수만

> .NET Framework 버전 4는 WebMatrix 베타에 필요 합니다. 경우에 따라 WebMatrix 베타 설치 관리자는 있도록 지원 되는 구성 집합의 포함 되지 않은 플랫폼에 설치 하려고 합니다. 특히, WebMatrix 베타 설치를 시작 하기 Windows Vista SP1 업데이트 없이 수는 없지만.NET Framework 4 구성 요소 실패 하 고 설치를 차단 됩니다.
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


#### <a name="issue-cannot-install-webmatrix-beta-3-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a>문제: Microsoft Visual Studio 2008 Microsoft Visual Studio 2008 SP1 없이 설치 된 경우 WebMatrix Beta 3을 설치할 수 없습니다.

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

문서의이 섹션에서는 새로운 기능, 변경 및 Razor 구문이 있는 ASP.NET 웹 페이지의 Beta 3 릴리스에 알려진된 문제를 설명 합니다.

- [새로운 기능](#NewFeatures)
- [변경 내용](#Changes)
- [문제](#Issues)

<a id="NewFeatures"></a>

#### <a name="new-features-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a>Razor 구문이 있는 ASP.NET 웹 페이지에 대 한 베타 3의에서 새로운 기능

#### <a name="new-htmlraw-method-renders-unencoded-markup"></a>"Html.Raw" 메서드 인코딩되지 않은 태그를 렌더링 하는 새로운 기능:

> 새 `Html.Raw` 메서드를 사용 하면 인코딩된 출력을 렌더링 하는 대신 태그로 HTML 태그를 렌더링 합니다. (기본적으로 ASP.NET Razor 문자열을 인코딩합니다 렌더링 하기 전에.) 사용되는 구문은 다음과 같습니다.
> 
> `Html.Raw(value)`
> 
> 다음 예제에서는 `Html.Raw`을 사용하는 방법을 보여 줍니다.
> 
> [!code-cshtml[Main](beta3/samples/sample1.cshtml)]


<a id="Changes"></a>

#### <a name="changes-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a>Razor 구문이 있는 ASP.NET 웹 페이지에 대 한 베타 3의에서 변경 내용

#### <a name="change-hrefattribute-method-removed"></a>제거 하는 "HrefAttribute" 방법: 변경

> `HrefAttribute` 의 메서드는 `WebPage` 클래스가 제거 되었습니다. 이 도우미는 Url에 안전 하지 않은 문자를 인코딩하는 데 사용 되었습니다. ASP.NET Razor는 자동으로 문자열을 인코딩합니다 때문에 필요 하지 않습니다. (새로운 `Html.Raw` 메서드를 인코딩되지 않은 문자열을 렌더링 합니다.)


#### <a name="change-syntax-for-declarative-helper-helpers-changed"></a>변경 사항:에 대 한 구문을 선언적 "@helper" 도우미 변경

> Beta 3 릴리스에 ASP.NET 변경 방법을 사용 하 여 만든 도우미를 구문 분석 된 `@helper` 구문입니다. 기본적으로 `@helper` 구문 코드 블록으로 대신 코드를 포함할 수 있는 태그 블록으로 이제 구문 분석 됩니다. 따라서 도우미 내부에서 코드를 필요 하지 않습니다 `@{ }` 블록입니다. 도우미 안에 태그는 ASP.NET Razor 또는 HTML 요소에 명시적으로 포함 해야 반대로 `<text></text>` 태그입니다.
> 
> 예를 들어, 다음 `@helper` Beta 3 릴리스에에서 작동 하는 구문:
> 
> [!code-cshtml[Main](beta3/samples/sample2.cshtml)]
> 
> Beta 3 릴리스에이 도우미를 다음 예제와 같이 변경 해야 합니다.
> 
> [!code-cshtml[Main](beta3/samples/sample3.cshtml)]
> 
> 에 `@{ }` 도우미에서 초기 코드의 바깥쪽 문자가 더 이상 사용 합니다. 즉, 기본적으로는 도우미의 내용을 코드 블록으로 처리 됩니다. 열기와 시작 태그를 렌더링 하는 도우미 `<a>` 태그입니다. 일반 텍스트 또는 닫는 태그가 포함 되지 않은 태그 도우미 렌더링 해야 하는 경우 (예를 들어 `<meta>` 태그)에 콘텐츠를 렌더링할 수 있어야 합니다. `<text></text>` 태그입니다.


#### <a name="change-webpagecontexthttpcontext-removed"></a>Change: "WebPageContext.HttpContext" removed

> `WebPageContext.HttpContext` 속성은 제거 되었습니다. 대신 `HttpContext.Current`를 사용하세요. (의 `WebPageContext.HttpContext` 속성에이 항목을 단순히 래핑됩니다.)


#### <a name="change-facebook-helper-moved-to-new-package"></a>새 패키지를 이동 하는 변경 사항: "Facebook" 도우미

> `Facebook` 도우미로 이동 되었습니다는 *Facebook.Helper* 포함 된 라이브러리는 `Facebook` 도우미와 추가 기능입니다. 에 설치 해야이 라이브러리는 별도 패키지로 "패키지 관리자와 설치 도우미"에 설명 된 대로 자습서 [ASP.NET 페이지 시작](https://go.microsoft.com/fwlink/?LinkId=202889)합니다.


#### <a name="change-membership-role-and-security-types-moves-to-new-assembly"></a>새 어셈블리를 변경 사항: 멤버 자격, 역할 및 보안 형식 이동

> 다음 형식으로 이동 되기는 `WebMatrix.WebData` 어셈블리:
> 
> - `ExtendedMembershipProvider`
> - `SimpleMembershipProvider`
> - `SimpleRoleProvider`
> - `WebSecurity`


#### <a name="change-tagbuilder-class-moved-to-systemwebwebpagesdll-assembly"></a>변경 사항: "TagBuilder" 클래스 System.Web.WebPages.dll 어셈블리로 이동

> `TagBuilde` r 클래스 System.Web.WebPages.dll 어셈블리로 이동 되었습니다. 이전에이 ASP.NET MVC의 일부 였던 어셈블리에 있었습니다. 이러한 변경으로 ASP.NET MVC를 사용 하려면 설치할 필요가 없습니다는 `TagBuilder` 클래스입니다.
> 
> 그러나 클래스는 여전히는 `System.Web.Mvc` 네임 스페이스입니다. 사용 하려면는 `TagBuilder` 클래스 (예를 들어 사용자 지정 ASP.NET Razor 도우미)를 네임 스페이스를 참조 해야 합니다 (예를 들어 추가 하 여 `@using System.Web.Mvc` 코드에).


#### <a name="change-request-validation-syntax-changed-validation-class-removed"></a>변경 사항: 요청 유효성 검사 구문 변경 되었습니다. "확인" 클래스가 제거

> Beta 3 릴리스에 개별 필드 또는 필드 집합에 대 한 유효성 검사를 사용 하지 않도록 설정 하 여 호출할 수 있습니다는 `Validation.Exclude` 메서드를 유효성 검사에서 제외할 필드의 이름으로 전달 합니다. 새 구문 유효성 검사를 우회 하기 위한 Beta 3 릴리스에 제공 됩니다. `Validation` Beta 3에서 사용 되는 방법을 제거 되었습니다.
> 
> > [!NOTE]
> > 웹 사이트와 같은 오류를 보고 합니다 (예를 들어 페이지에 서식 있는 텍스트 편집기를 사용)에서 HTML 태그를 업로드를 시도할 경우 요청 유효성 검사를 해제 하지 않는 경우 *잠재적으로 위험한 Request.Form 값클라이언트에서검색되었습니다*사용자 입력이 허용 되지 않습니다. 사용자 입력을 하거나 하지 않는 잠재적으로 위험한 태그가 포함 스크립트를 다음과 같이 사용 하 여 확인을 요청 유효성 검사를 비활성화 하면 수동으로 확인 해야 합니다는 [Microsoft 바이러스 교차 사이트 스크립팅 라이브러리 V4.0](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651)합니다.
> 
> 
> 자동으로 요청 유효성 검사를 비활성화 하려면 호출 된 `Request.Unvalidated` 메서드, 필드 또는 대 한 요청 유효성 검사를 무시 하는 다른 post 개체의 이름을 전달 합니다. 이 메서드를 사용 하 여 모든 항목에 대 한 유효성 검사를 무시 하는 `Form`, `QueryString`, `Cookies`, 및 `ServerVariables` 컬렉션입니다. 다음 예제를 사용 하는 방법을 보여 줍니다는 `Unvalidated` 메서드:
> 
> [!code-csharp[Main](beta3/samples/sample4.cs)]


<a id="Issues"></a>

#### <a name="known-issues-for-aspnet-web-pages-with-razor-syntax"></a>Razor 구문이 있는 ASP.NET 웹 페이지에 대 한 알려진된 문제

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a>문제: 예기치 않은 동작이 멤버 자격에 대 한 사용자 지정 사용자 테이블을 사용 하는 경우

> 호출에서 ASP.NET Razor 웹 사이트에 대 한 멤버 자격 공급자를 초기화 하려면는 `WebSecurity.InitializeDatabaseConnection` 메서드. (시작 사이트 템플릿의 WebMatrix에서이 메서드에 대 한 호출을 포함 된  *\_AppStart.cshtml* 파일입니다.) 경우는 `autoCreateTables` 이 메서드의 매개 변수를 설정을 true로 (기본적으로 설정은 시작 사이트 템플릿의에서 true), 하며 메서드는 인식할 수 없는 테이블 이름 (두 번째 매개 변수)는 메서드에 전달 되 면 오류가 발생 하지 않습니다. 대신, 테이블이 자동으로 만들어집니다.
> 
> 멤버 자격에 대 한 사용자 지정 사용자 테이블을 사용 하지만 잘못 된 테이블을 이름을 전달 하려는 경우이 문제가 될 수는 `WebSecurity.InitializeDatabaseConnection` 메서드. 메서드가 발생 하지 않으므로 기본적으로 오류가 지정한 테이블이 없는 경우 및 대신 새 테이블을 만들기 때문에 응용 프로그램 작동 나타날 수 있습니다. 그러나 응용 프로그램 코드에 사용자 지정 사용자 테이블 (및 그 안에 필드에)를 사용 하는 예기치 않은 오류와 함께 결국 실패할 수 있습니다.
> 
> **해결 방법**  
> 이름에 전달 되는지 확인는 `InitializeDatabaseConnection` 사용자 프로필 테이블 멤버 자격 데이터베이스에 또는 다음 사항을 확인 메서드 일치는 `autoCreateTables` 매개 변수를 false로 설정 합니다.


#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a>문제: "하지 못했습니다 SQL Server의 사용자 인스턴스를 생성 하려면" 오류

> WebMatrix 웹 응용 프로그램을 SQL Server Express를 사용 하 여 Windows 7 또는 Windows Server 2008 r 2에서 IIS 7.5를 실행 중인 경우 SQL Server가 런타임 시 사용자의 로컬 응용 프로그램 경로 검색할 수 없습니다 되었음을 나타내는 오류가 표시 될 수 있습니다.
> 
> **해결 방법** (일반적으로 네트워크 서비스)에서 응용 프로그램을 실행 하는 Windows 계정에 대 한 응용 프로그램의 루트 폴더 및 하위 폴더에 대 한 읽기/쓰기 권한을 같은 있는지 확인 *앱\_데이터*. 더 자세한 정보는 기술 자료 문서에서 사용할 수 있는 [SQL Server Express 사용자 인스턴스 만들기 및 ASP.net 웹 응용 프로그램 프로젝트 문제](https://support.microsoft.com/kb/2002980)합니다.


#### <a name="issue-in-visual-studio-namespaces-for-custom-assemblies-dlls-are-not-imported-automatically"></a>문제: Visual Studio에서 사용자 지정 어셈블리 (Dll)에 대 한 네임 스페이스 가져오지 않은 자동으로

> Visual Studio에서 프로젝트에 사용자 지정 어셈블리를 사용 하는 경우에 디자인 타임에 이러한 어셈블리의 선언 된 네임 스페이스는 자동으로 가져오지 않습니다. 결과적으로, 사용자 지정 형식에 대 한 참조는 디자인 타임에 인식 되지 않을 수 있습니다 하 고 ("오류 표시선" 사용) Visual Studio에서 인식된 되지로 표시 됩니다. 이 문제는 Visual Studio;에서 디자인 타임에만 발생 응용 프로그램 자체는 제대로 실행 됩니다.
> 
> **해결 방법**  
> 포함 한 `using` 문 (`imports` Visual basic에서) 디자인 타임에 인식 되지 않는 엔터티를 참조 하는 합니다.


#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a>문제: Visual Studio IntelliSense 및 프로젝트 템플릿 ASP.NET MVC 버전 3에만 사용할 수 있는

> 설치 하는 ASP.NET 웹 페이지도 ´ â 도구 Visual Studio에 대 한 ASP.NET 웹 페이지 응용 프로그램에 대 한 IntelliSense 및 프로젝트 템플릿과 같은 합니다.
> 
> **해결 방법** 웹 플랫폼 설치 관리자를 통해 ASP.NET MVC 3 RC 설치 IntelliSense 및 프로젝트 템플릿을 Visual Studio에서 ASP.NET 웹 페이지 응용 프로그램을 사용 하려면 또는 [독립 실행형 설치 관리자](https://go.microsoft.com/fwlink/?LinkID=191797)합니다.


#### <a name="issue-lthelpergt-class-cannot-be-found-error"></a>문제: "&lt;도우미&gt; 클래스를 찾을 수 없습니다" 오류

> Beta 3로 업그레이드 한 후 오류가 표시 될 수 있습니다 하는 도우미 클래스 (예를 들어는 `Facebook` 클래스)를 찾을 수 없습니다. 베타 2부터 Beta 3의 진행을 명시적으로 설치 해야 하는 패키지에 대 한 읽기 권한만 이동 되었습니다. 이러한 패키지를 포함 하도록 기존 사이트는 업그레이드 되지 않습니다. 여기에 사이트 포함 됩니다는 *\My Documents\IISExpress* 또는 *\My Documents\My 웹사이트* 폴더입니다. 기본 사이트를 사용 하는 경우이 오류가 표시 됩니다는 특히 *내 사이트* (WebSite1)에 대 한 참조를 포함 하는 `Twitter` 도우미입니다.
> 
> **해결 방법**  
> 주석 처리를 실행 하는 사이트에 있는 모든 도우미에 대 한 호출에서  *\_Admin* 페이지를 선택한 패키지 또는 사용 하려는 하는 도우미를 포함 하는 패키지를 설치 합니다. 패키지를 설치한 후 도우미를 참조 하는 줄을 주석 처리 제거 합니다.


#### <a name="issue-deploying-beta-3-aspnet-razor-assemblies-to-the-bin-folder-might-not-work-on-hosting-sites"></a>문제: Bin 폴더를 베타 3 ASP.NET Razor 어셈블리 배포 작동 하지 않을 수 호스팅하는 사이트에서

> 호스팅 사이트에서 ASP.NET 웹 페이지 웹 사이트를 배포 하 고 사이트의 ASP.NET Razor Beta 3 어셈블리를 배포 하는 경우 *Bin* 폴더에서 다음을 포함 한 오류가 발생할 수 있습니다.
> 
> `Could not load type 'Microsoft.Web.Infrastructure.DynamicModuleHelper.DynamicModuleUtility' from assembly 'Microsoft.Web.Infrastructure, Version=1.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`
> 
> 이 호스팅 공급자가 서버의 전역 어셈블리 캐시 (GAC)에 ASP.NET 웹 페이지 베타 1 어셈블리를 설치 하는 경우에 발생할 수 있습니다. GAC의 어셈블리에 로컬로 설치 된 어셈블리에 대해 우선 순위를 가져오고는 *Bin* 폴더입니다.
> 
> **해결 방법** 공급자의 버전 간의 충돌로 인해 오류가 표시 되는 호스팅 공급자에 게 문의 어셈블리와 사용자입니다. 이 경우에 호스팅 공급자는 서버의 GAC에 어셈블리를 업데이트 하도록 요청 합니다.


#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a>문제: 프록시 서버를 통해 다른 외부 데이터 나 피드 읽기

> 프록시 서버 뒤에 있는 사이트를 실행 하는 서버가 있는 경우에 대 한 프록시 정보를 구성 해야 할 수도 있습니다는 *Web.config* 파일을 사이트 외부의에서 제공 되는 정보를 읽을 수 있습니다. 예를 들어, 사용 하는 경우는 `ReCaptcha` 도우미, 도우미 reCAPTCHA 서비스와 통신 하지만 프록시 서버에 의해 차단 될 수 있습니다. 마찬가지로, 패키지 관리자에서 사용 하는 피드 등 ASP.NET 웹 페이지에서 사용 되는 피드 프록시 구성이 필요할 수 있습니다.
> 
> 외부 서비스를 작업할 또는 피드 패키지 작업에서 문제가 있는 경우 응용 프로그램의 루트에는 다음과 같은 요소가 배치 *Web.config* 파일:
> 
> [!code-xml[Main](beta3/samples/sample5.xml)]
> 
> 프록시 서버를 구성 하는 방법에 대 한 자세한 내용은 참조 [ &lt;프록시&gt; 요소 (네트워크 설정)](https://msdn.microsoft.com/library/sa91de1e.aspx) MSDN 웹 사이트에 있습니다.


#### <a name="issue-microsoftwebinfrastructuredll-cannot-be-loaded-error"></a>문제: "Microsoft.Web.Infrastructure.dll를 로드할 수 없습니다." 오류

> 모든 적절 한 어셈블리를 제외 하 고 GAC에 설치 된 이전에 Razor 구문이 있는 ASP.NET 웹 페이지의 베타 1 버전을 설치 하 고 다음 베타 3 버전을 설치 하는 경우 *Microsoft.Web.Infrastructure.dll*합니다. 따라서 ASP.NET Razor 페이지를 실행 하면 오류가 표시 하 고 있음을 나타내는 *Microsoft.Web.Infrastructure.dll* 로드할 수 없습니다.
> 
> Beta 3 릴리스에 클린 컴퓨터에서 로드 한 경우에이 문제가 발생 하지 않습니다.
> 
> **해결 방법**  
> 제어판에서 ASP.NET 웹 페이지를 제거 합니다. Beta 3 릴리스에 다시 설치 합니다.


#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a>문제: Razor 구문이 있는 ASP.NET 웹 페이지를 사용 하지 않도록 설정.NET Framework 버전 4 제거 합니다.

> .NET Framework 버전 4 제거한 다음 다시 설치 하는 경우에 Razor 구문이 있는 ASP.NET 웹 페이지 비활성화 됩니다. 와 페이지는 *.cshtml* 확장 제대로 실행 되지 않습니다. 컴퓨터 루트에 있는 어셈블리를 등록 하는 ASP.NET 웹 페이지 *Web.config* 파일 및.NET Framework를 제거 합니다. 해당 파일을 제거 합니다. .NET Framework를 다시 설치 하는 구성 파일의 새 버전을 설치 하지만 ASP.NET 웹 페이지 어셈블리에 대 한 참조를 추가 하지 않습니다.
> 
> **해결 방법** .NET Framework를 다시 설치한 후 Razor 구문이 있는 ASP.NET 웹 페이지를 다시 설치 합니다. 이렇게 하면 다음 요소를 추가 *Web.config* 일반적으로 다음 위치에 있는 컴퓨터 루트에 파일:  
>   
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
>   
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](beta3/samples/sample6.xml)]


#### <a name="issue-applications-previously-deployed-with-aspnet-assemblies-in-the-bin-folder-experience-errors"></a>문제: Bin 폴더에서 ASP.NET 어셈블리와 함께 이전에 배포 된 응용 프로그램 오류가 발생 합니다.

> ASP.NET 웹 페이지 어셈블리 복사본을 배포 하는 동안 (예를 들어 *Microsoft.WebPages.dll*)에 *Bin* 서버에서 웹 사이트의 폴더입니다. (이 때문일 수 있습니다 자동으로 배포 하는 동안 개발자는 어셈블리를 명시적으로 복사 되므로 또는.) 그러나 Beta 3 릴리스에 설치 될 때 오류 발생, 예: 특정 형식을 찾을 수 없으므로 오류. 이 이유는 ASP.NET 웹 페이지 형식 수가 Beta 3 릴리스에 대 한 서로 다른 네임 스페이스로 이동 되었습니다.
> 
> **해결 방법**   
> 지우기는 *Bin* 배포 된 응용 프로그램의 폴더 새 어셈블리 폴더에 복사 (또는 응용 프로그램을 재배포) 한 다음 응용 프로그램 다시 시작 합니다.


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
> - 서버 컴퓨터에 대 한 제어 없는 경우 (예를 들어를 배포 하는 호스팅 웹 사이트에) 다음을 웹 사이트의 추가 *Web.config* 파일:
> 
> 
> [!code-xml[Main](beta3/samples/sample7.xml)]


#### <a name="issue-using-web-application-project-or-aspnet-mvc-and-aspnet-web-pages-in-the-same-application"></a>문제: ASP.NET MVC와 ASP.NET 웹 페이지 또는 웹 응용 프로그램 프로젝트를 사용 하 여 동일한 응용 프로그램

> ASP.NET 웹 페이지는 웹 응용 프로그램 프로젝트 또는 ASP.NET MVC 응용 프로그램에서 사용할 때 오류가 표시 될 수 있는 *WebPageHttpApplication* 찾을 수 없습니다.
> 
> **해결 방법**  
> 이 오류가 발생할 경우 응용 프로그램 파생 되는 기본 클래스를 변경 합니다. 에 *Global.asax* 파일에서 다음 줄을 변경 합니다.
> 
> [!code-csharp[Main](beta3/samples/sample8.cs)]
> 
> 다음과 같이 변경 하려면
> 
> [!code-csharp[Main](beta3/samples/sample9.cs)]
> 
> 도입 된 변경 이렇게 적용 하면 Razor 구문이 있는 ASP.NET 웹 페이지의 베타 1 릴리스 합니다.


#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a>문제: SQL Server Compact 설치 하지 않은 컴퓨터에 응용 프로그램 배포

> SQL Server Compact 데이터베이스를 포함 하는 응용 프로그램 컴퓨터에서 실행할 수 있는 SQL Server Compact 설치 되어 있지 않습니다. Microsoft WebMatrix Beta 3에서 자동으로 이러한 이진 파일을 복사 하 고 적절 한 수행 *Web.config* 변환 파일입니다.
> 
> **해결 방법** 하 이러한 파일을 복사 하 고 확인 해야 하는 경우는 *Web.config* 파일 변경 내용을 수동으로 다음을 수행 합니다.
> 
> 1. 데이터베이스 엔진 어셈블리를 복사는 *Bin* 대상 컴퓨터에 응용 프로그램의 폴더 (및 하위 폴더): 
> 
>     - Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* **to** *\Bin*
>     - Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\** **to** *\Bin\x86*
>     - Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\** **to** *\Bin\amd64*
> 2. 웹 사이트의 루트 폴더에 작성 하거나 열을 *Web.config* 파일입니다. (이 파일 형식이 WebMatrix 베타 3에서 클릭 하면 표시 되 **모든** 에 **파일 형식을 선택** 대화 상자.)
> 3. 다음 요소를 자식으로 추가  **&lt;구성&gt;**  요소 (에 포함 되지 않은  **&lt;system.web&gt;**  요소):
> 
> 
> [!code-xml[Main](beta3/samples/sample10.xml)]


#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a>문제: 데이터베이스 및 WebGrid 도우미 Visual Basic에서는 보통 신뢰에서 작동 하지 않음

> Visual Basic을 사용 하는 경우 (만드는 *.vbhtml* 파일), `Database` 및 `WebGrid` 도우미에는 보통 신뢰를 사용 하도록 설정 되어 있는 경우 작동 하지 것입니다.
> 
> **해결 방법**  
> 완전 신뢰를 사용 하도록 응용 프로그램을 일시적으로 설정 합니다.

<a id="Known_Issues_SQL_Server_Compact"></a>
### <a name="sql-server-compact"></a>SQL Server Compact

#### <a name="issue-encrypt-property-is-not-recognized"></a>문제: "Encrypt" 속성이 인식 되지 않습니다.

> SQL Server Compact 4.0 인식 하지 않으므로 `Encrypt` 의 속성은 `SqlCeConnection` 클래스입니다. 데이터베이스 파일을 암호화 하려면이 속성을 사용 하지 해야 합니다. `Encrypt` 속성 SQL Server Compact 3.5 릴리스에서 사용이 중단 되었으며 및 이전 버전과 호환성을 위해서만 유지 되었습니다. 
> 
> **해결 방법**  
> 사용 하 여는 `Encryption Mode` 의 속성은 `SqlCeConnection` SQL Server Compact 4.0 데이터베이스 파일을 암호화 하는 클래스입니다. 사용 하 여 암호화 된 SQL Server Compact 4.0 데이터베이스를 만드는 방법을 보여 주는 다음 예제는 `Encryption Mode` 속성:
>  
> [!code-csharp[Main](beta3/samples/sample11.cs)]
>  
> [!code-vb[Main](beta3/samples/sample12.vb)]
> 
> 기존 SQL Server Compact 4.0 데이터베이스의 암호화 모드를 변경 하려면 다음을 수행 합니다.
>  
> [!code-csharp[Main](beta3/samples/sample13.cs)]
>  
> [!code-vb[Main](beta3/samples/sample14.vb)]
> 
> 암호화 되지 않은 SQL Server Compact 4.0 데이터베이스를 암호화 하려면 다음을 수행 합니다.
>  
> [!code-csharp[Main](beta3/samples/sample15.cs)]
>  
> [!code-vb[Main](beta3/samples/sample16.vb)]


#### <a name="issue-microsoft-visual-c-2008-runtime-libraries-are-required"></a>문제: Microsoft Visual c + + 2008 런타임 라이브러리는 필요

> 네이티브 Dll의 SQL Server Compact 4.0의 Microsoft Visual c + + 2008 런타임 라이브러리 (x86, IA64, x64), 서비스 팩 1에 필요 합니다.
> 
> **해결 방법**  
> .NET Framework 3.5 s p 1을 설치 합니다. 이 Visual c + + 2008 런타임 라이브러리 s p 1도 설치 됩니다. 다음 위치에서 라이브러리를 다운로드할 수 있습니다.   
>   
> [Microsoft Visual c + + 2008 서비스 팩 1 재배포 가능 패키지 ATL 보안 업데이트](https://go.microsoft.com/fwlink/?LinkId=194827)
> 
> [!NOTE]
> 해당.NET Framework 2.0, 3.0, 설치 또는 4가 *하지* Visual c + + 2008 런타임 라이브러리 p 1을 설치 합니다.


#### <a name="issue-if-sql-server-compact-is-installed-prior-to-installing-net-framework-on-the-computer-its-provider-invariant-name-is-not-registered-in-the-net-framework-machineconfig-file"></a>문제: SQL Server Compact가 컴퓨터에.NET Framework를 설치 하기 전에 설치 된 경우 해당 공급자 고정 이름에에서 등록 되지 않은.NET Framework machine.config 파일

> SQL Server Compact.NET Framework가 SQL Server Compact는.NET framework가 필요 하기 때문에 설치 하지 않은 컴퓨터에 설치할 수 있습니다. .NET Framework 버전 3.5 아니고 4가 설치 되어 SQL Server Compact를 설치 하기 전에 SQL Server Compact 설치에 공급자 고정 이름을 등록 하지 않습니다는 *machine.config* 파일입니다. SQL Server Compact의 항목에 의존 하는 모든 응용 프로그램의 *machine.config* 파일 실패 합니다. 고정 이름이 등록 항목 *machine.config* 다음 예제에서는 것 같습니다.
> 
> [!code-xml[Main](beta3/samples/sample17.xml)]
> 
> **해결 방법**  
> SQL Server Compact 4.0 CTP1를 제거 합니다. 다운로드 하 고 다음 위치에서 전체 버전의.NET Framework를 설치 합니다.
> 
> [Microsoft.NET Framework 3.5 서비스 팩 1 (전체 패키지)](https://go.microsoft.com/fwlink/?LinkId=194828)  
> [Microsoft.NET Framework 4.0 릴리스 (전체 패키지)](https://www.microsoft.com/downloads/details.aspx?FamilyID=9cfb2d51-5ff4-4491-b0e5-b386f32c0992&amp;displaylang=en)
> 
> 다음 다시 설치 [SQL Server Compact 4.0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en)합니다.


<a id="Known_Issues_Installing_Applications"></a>

### <a name="installing-applications"></a>응용 프로그램 설치

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a>문제: 응용 프로그램을 설치는 시간이 오래 걸릴 수는 사용자의 내 문서 폴더를 네트워크 공유로 리디렉션되면

> **해결 방법**  
> 없음 응용 프로그램을 설치 하려면 시간이 오래 걸릴 수 있지만 제대로 설치 됩니다.


<a id="Known_Issues_Publishing_Applications"></a>

### <a name="publishing-applications"></a>응용 프로그램 게시

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


<a id="Known_Issues_Other_Issues"></a>

### <a name="other-issues"></a>기타 문제

#### <a name="issue-searchfilter-does-not-work-in-reports-for-group-by-issue-type"></a>문제: 검색/필터가 작동 하지 않음 보고서에서 Group By에 대 한: 문제 유형

> 텍스트를 입력 하는 경우 사이트에 대 한 보고서를 실행 하면는 *URL에 의해 필터* 상자 한 클릭 *검색*, 아무 일도 발생 합니다. 이 제어 하는 동안 작동 하지 않습니다. 때문에 이것이 *Group By* 상태 보고서의으로 설정 되어 *문제 유형*, 기본값입니다.
> 
> **해결 방법** 에 *Group By* 탭 리본 메뉴를 클릭 *URL* 해당 소스 URL으로 항목을 그룹화 합니다. 텍스트 상자 및 항목을 필터링 하려면이 단추는이 상태 동안 기능입니다.


#### <a name="issue-wcf-applications-fail-to-run-with-iis-express"></a>문제: WCF 응용 프로그램 IIS Express와 실행에 실패

> 탐색 하는 WCF 응용 프로그램에서 다음과 같은 오류가 발생 합니다.
> 
> *파일 또는 어셈블리를 로드할 수 없습니다 ' Microsoft.Web.Administration, 버전 = 7.0.0.0, Culture = neutral, PublicKeyToken = 31bf3856ad364e35' 또는 해당 종속성 중 하나. 지정한 파일을 찾을 수 없습니다.*
> 
> IIS Express 베타 릴리스 버전 기본적으로 WCF를 지원 하지 않으므로이 발생 합니다.
> 
> **해결 방법** 다음 해결 방법 중 하나를 사용 하 여 (해결 방법 2 필요한 Microsoft Windows Vista 이상):
> 
> 
> 1. 복사는 *Microsoft.Web.dll* 및 *Microsoft.Web.Administration.dll* 를 WebMatrix 설치 위치에서 어셈블리는 *bin* wcf 디렉터리 응용 프로그램입니다. 기본적으로 WebMatrix에서 설치는 *Microsoft WebMatrix* 시스템의 아래에 있는 하위 *Program Files* 폴더입니다.
> 2. Microsoft Windows Vista 이상에서는 만들의 어셈블리에는 기호화 된 링크는 *bin* 다음 명령을 사용 하 여 디렉터리입니다. (이 방법은 장점이 어셈블리의 복사본을 생성 하지 않습니다.)
> 
>     [!code-console[Main](beta3/samples/sample18.cmd)]
> 3. 두 명의 어셈블리가 GAC에 설치 합니다. 관리자 권한 프롬프트에서 다음 명령을 실행 합니다.
> 
>     [!code-console[Main](beta3/samples/sample19.cmd)]


#### <a name="issue-webmatrix-beta-3-is-unable-to-perform-certain-tasks-that-require-elevation"></a>문제: WebMatrix 베타 3 상승이 필요한 특정 작업을 수행할 수 없으면

> WebMatrix Beta 3가 다음과 같은 상황에서 추가 구성 요소를 설치 하는 등 상승이 필요한 특정 작업을 수행할 수 없습니다.
> 
> - Windows Vista 또는 Windows 7에서 관리자 권한이 없는 계정으로 로그인 및 사용자 계정 컨트롤 (UAC)을 사용할 수 없습니다.
> - Microsoft Windows XP 또는 Microsoft Windows Server 2003을 사용 하 고 있습니다.
> 
> **해결 방법**  
> 대부분의 작업 WebMatrix Beta 3에는 관리 권한이 필요 하지 않습니다. 않은에 대 한 다음이 단계를 수행 또는 관리자는 작업을 수행할 수 있습니다.
> 
> - Windows Vista 또는 Windows 7에서 UAC를 사용 하도록 설정 합니다.
> - Windows XP에서 Administrators 보안 그룹에 사용자를 추가 합니다.


#### <a name="issue-site-from-web-gallery-is-disabled"></a>문제: "사이트에서 웹 갤러리"을 사용할 수 없습니다.

> **웹 갤러리에서 사이트** 웹 플랫폼 설치 관리자 3.0이 설치 되지 않은 경우 옵션은 사용할 수 없습니다.
> 
> **해결 방법**  
> 설치는 [Microsoft 웹 플랫폼 설치 관리자 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)합니다.


#### <a name="issue-on-windows-server-2003-iis-express-does-not-start-for-a-non-administrative-user"></a>문제: Windows Server 2003에서 IIS Express 시작 되지 않으면 관리자가 아닌 사용자에 대 한

> Windows Server 2003에는 페이지를 시작 하거나 IIS Express를 시작 하는 경우 IIS Express 시작 되지 않습니다. 웹 페이지에 대 한 응용 프로그램 관리자가 아닌 사용자가 시작한 있는지 여부를 나타내는 오류가 표시 됩니다.
> 
> **해결 방법**  
> 관리자 권한으로 WebMatrix Beta 3를 시작 합니다. 자세한 내용은 다음 기술 자료 문서를 참조:  
>   
> [관리자가 아닌 사용자에 의해 시작 하는 응용 프로그램은 응용 프로그램이 Windows Vista, Windows Server 2003 또는 Windows XP에서 실행 되는 컴퓨터의 HTTP 트래픽을 수신할 수 없습니다.](https://support.microsoft.com/kb/939786)


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


#### <a name="issue-the-relationships-button-is-disabled"></a>문제: "관계" 단추는 사용할 수 없습니다.

> **관계** 단추는 **테이블** 탭에 **데이터베이스** SQL Server Compact 데이터베이스에 대 한 작업 영역을 사용할 수 없습니다.
> 
> **해결 방법**  
> 없음 SQL Server Compact에서 테이블 간의 관계 지원 하지 않습니다.


#### <a name="issue-parameterized-sql-queries-throw-exceptions"></a>문제: 매개 변수가 있는 SQL 쿼리 예외 throw

> SQL Server Compact 4.0에서는 데이터 형식 같은 지정 하지 않으면 `SqlDbType` 또는 `DbType` 매개 변수가 있는 쿼리 매개 변수에 대해 쿼리를 실행할 때 예외가 throw 됩니다.
> 
> **해결 방법**  
> 와 같은 데이터 형식 매개 변수에 대 한를 명시적으로 설정 `SqlDbType` 또는 `DbType`합니다. 이 BLOB 데이터 형식의 경우 중요 한 (`image` 및 `ntext`). 다음과 같은 코드를 사용 합니다.
> 
> [!code-sql[Main](beta3/samples/sample20.sql)]
>  
> [!code-vb[Main](beta3/samples/sample21.vb)]


<a id="More_Info"></a>

## <a name="for-more-information"></a>자세한 내용

WebMatrix Beta 3에 대 한 자세한 내용은 다음 웹 사이트를 참조 하십시오.

- [IIS.net](http://iis.net/)
- [ASP.NET](https://asp.net/webmatrix)
- [Microsoft.com/web](https://www.microsoft.com/web)

* * *

© 2010 Microsoft Corporation. All Rights Reserved. [사용 약관](https://msdn.microsoft.cos/cc300389.aspx)합니다.
