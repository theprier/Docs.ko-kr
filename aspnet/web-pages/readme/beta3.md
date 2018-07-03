---
uid: web-pages/readme/beta3
title: Webmatrix 및 ASP.NET 웹 페이지 (Razor) 베타 3 릴리스 정보 | Microsoft Docs
author: rick-anderson
description: Webmatrix 및 ASP.NET 웹 페이지 (Razor) 베타 3 릴리스 추가 정보
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/10/2011
ms.topic: article
ms.assetid: ffa3d5c9-91e5-4da3-b409-560b0c7fbbf0
ms.technology: dotnet-webpages
msc.legacyurl: /web-pages/readme/beta3
msc.type: content
ms.openlocfilehash: 5aa609bf31499485dc7a1298fa689f3a7cee4774
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37363535"
---
<a name="web-matrix-and-aspnet-web-pages-razor-beta-3-release-readme"></a>Webmatrix 및 ASP.NET 웹 페이지 (Razor) 베타 3 릴리스 추가 정보
====================
> Webmatrix 및 ASP.NET 웹 페이지 (Razor) 베타 3 릴리스 추가 정보

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

> Microsoft WebMatrix 베타는 몇 분 안에 설치 하는 무료 웹 개발 스택입니다. 데이터베이스 및 프로그래밍 프레임 워크를 단일 통합된 환경 만들기를 사용 하 여 웹 서버를 통합 합니다. WebMatrix 베타를 사용 하 여 코드, 테스트 및 고유한 ASP.NET 또는 PHP 웹 사이트를 게시 하는 방법을 간소화할 수 있습니다 또는 DotNetNuke, Umbraco, WordPress 또는 Joomla와 같은 인기 있는 오픈 소스 앱을 사용 하 여 새 웹 사이트를 시작 하려면 WebMatrix 베타를 사용할 수 있습니다. WebMatrix 베타 같은 강력한 웹 서버, 데이터베이스 엔진 및 원활 하 게 개발에서 프로덕션으로 전환 하면 인터넷에서 웹 사이트를 실행 되는 프레임 워크 환경을 사용 합니다.


<a id="Installation_Notes"></a>

## <a name="installation"></a>설치

> 사용할 WebMatrix 베타 3을 설치 하려면 [Microsoft 웹 플랫폼 설치 관리자 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)합니다. 웹 플랫폼 설치 관리자를 설치한 후에 WebMatrix 베타 3을 설치 하려면 사용할 수 있습니다.
> 
> 설치 중에 문제가 있는 경우 가리킵니다 [Microsoft 웹 플랫폼 설치 관리자를 사용 하 여 문제 해결](https://go.microsoft.com/fwlink/?LinkId=196212)합니다.


<a id="Installation_Notes0"></a>

## <a name="instructions-for-publishing-applications"></a>응용 프로그램을 게시 하기 위한 지침

> 참조 [응용 프로그램을 게시 하기 위한 단계별 지침](https://go.microsoft.com/fwlink/?LinkID=196149)


<a id="Known_Issues"></a>

## <a name="new-features-changes-andknown-issues"></a>새 기능을 변경 andKnown 문제

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-beta-3-installation"></a>WebMatrix 베타 3 설치

#### <a name="issue-webmatrix-beta-3-is-only-available-on-platforms-that-support-microsoft-net-framework-4"></a>문제: WebMatrix Beta 3은 Microsoft.NET Framework 4를 지 원하는 플랫폼에서 사용할 수 있습니다만

> .NET Framework 버전 4가 WebMatrix 베타 필요 합니다. 특정 경우에 지원 되는 구성 집합의 일부가 아닌 플랫폼에 설치 하려고 하면 WebMatrix 베타 설치 관리자 그러면 합니다. 특히 Windows Vista SP1 업데이트를 사용 하면 WebMatrix 베타 설치를 시작할 수 있지만.NET Framework 4 구성 요소 실패를 업데이트 하 고 설치를 차단 됩니다.
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


#### <a name="issue-cannot-install-webmatrix-beta-3-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a>문제: Microsoft Visual Studio 2008은 Microsoft Visual Studio 2008 SP1 없이 설치 된 경우 WebMatrix 베타 3을 설치할 수 없습니다.

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

문서의이 섹션에서는 새로운 기능, 변경 및 Razor 구문이 있는 ASP.NET 웹 페이지의 베타 3 릴리스를 사용 하 여 알려진된 문제에 설명합니다.

- [새로운 기능](#NewFeatures)
- [변경 내용](#Changes)
- [문제](#Issues)

<a id="NewFeatures"></a>

#### <a name="new-features-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a>Razor 구문이 있는 ASP.NET 웹 페이지에 대 한 베타 3의에서 새로운 기능

#### <a name="new-htmlraw-method-renders-unencoded-markup"></a>"Html.Raw" 메서드 인코딩되지 않은 태그를 렌더링 하는 새로운 기능:

> 새 `Html.Raw` 메서드를 사용 하면 인코딩된 출력을 렌더링 하는 대신 태그로 HTML 태그를 렌더링 합니다. (기본적으로 ASP.NET Razor 인코딩합니다 문자열을 렌더링 하기 전에.) 사용되는 구문은 다음과 같습니다.
> 
> `Html.Raw(value)`
> 
> 다음 예제에서는 `Html.Raw`을 사용하는 방법을 보여 줍니다.
> 
> [!code-cshtml[Main](beta3/samples/sample1.cshtml)]


<a id="Changes"></a>

#### <a name="changes-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a>Razor 구문이 있는 ASP.NET 웹 페이지의 Beta 3의에서 변경 내용

#### <a name="change-hrefattribute-method-removed"></a>변경 내용: "HrefAttribute" 메서드가 제거

> 합니다 `HrefAttribute` 메서드는 `WebPage` 클래스가 제거 되었습니다. 이 도우미는 Url에 안전 하지 않은 문자를 인코딩하는 데 사용 되었습니다. ASP.NET Razor 자동으로 인코딩되고, 문자열 때문에 필요 하지 않습니다. (새 `Html.Raw` 인코딩되지 않은 문자열을 렌더링 하는 방법입니다.)


#### <a name="change-syntax-for-declarative-helper-helpers-changed"></a>변경: 구문에 대 한 선언적 "@helper" 변경 하는 도우미

> Beta 3 릴리스에 ASP.NET 변경 하는 방법을 사용 하 여 만든 도우미를 구문 분석 된 `@helper` 구문입니다. 기본적으로 `@helper` 구문은 이제 코드를 포함할 수 있는 태그 블록으로 대신 코드 블록으로 구문 분석 합니다. 따라서 도우미 내부에서 코드 않아도 묶어야 `@{ }` 블록입니다. 태그 도우미 내부에서 ASP.NET Razor 또는 HTML 요소에 명시적으로 포함 되도록에 반대로, `<text></text>` 태그입니다.
> 
> 예를 들어, 다음 `@helper` 구문 Beta 3 릴리스에 작동 합니다.
> 
> [!code-cshtml[Main](beta3/samples/sample2.cshtml)]
> 
> Beta 3 릴리스에이 도우미를 다음과 같이 변경 해야 합니다.
> 
> [!code-cshtml[Main](beta3/samples/sample3.cshtml)]
> 
> 에 `@{ }` 도우미에서 초기 코드 주위 문자는 더 이상 사용 합니다. 즉, 기본적으로 도우미의 내용을 코드 블록으로 처리 됩니다. 시작 하 여는 태그를 렌더링 하는 도우미 `<a>` 태그입니다. 일반 텍스트 또는 닫는 태그를 포함 하지 않는 태그 도우미를 렌더링 해야 하는 경우 (예를 들어 `<meta>` 태그), 콘텐츠를 렌더링할에 있어야 합니다. `<text></text>` 태그입니다.


#### <a name="change-webpagecontexthttpcontext-removed"></a>변경 내용: "WebPageContext.HttpContext" 제거

> `WebPageContext.HttpContext` 속성이 제거 되었습니다. 대신 `HttpContext.Current`를 사용하세요. (의 `WebPageContext.HttpContext` 속성 래핑되어이.)


#### <a name="change-facebook-helper-moved-to-new-package"></a>새 패키지를 이동 하는 변경 내용: "Facebook" 도우미

> `Facebook` 도우미로 이동 되었습니다 합니다 *Facebook.Helper* 포함 하는 라이브러리는 `Facebook` 도우미와 추가 기능입니다. 에 설치 해야이 라이브러리는 별도 패키지로 "패키지 관리자 사용 하 여 설치 도우미"에 설명 된 대로 자습서 [Getting Started with ASP.NET 페이지](https://go.microsoft.com/fwlink/?LinkId=202889)합니다.


#### <a name="change-membership-role-and-security-types-moves-to-new-assembly"></a>새 어셈블리를 변경 합니다: 멤버 자격, 역할 및 보안 형식 이동

> 다음 형식에 이동 된는 `WebMatrix.WebData` 어셈블리:
> 
> - `ExtendedMembershipProvider`
> - `SimpleMembershipProvider`
> - `SimpleRoleProvider`
> - `WebSecurity`


#### <a name="change-tagbuilder-class-moved-to-systemwebwebpagesdll-assembly"></a>변경 내용: ""는 TagBuilder 클래스 System.Web.WebPages.dll 어셈블리로 이동

> `TagBuilde` r 클래스 System.Web.WebPages.dll 어셈블리로 이동 되었습니다. 이전에이 ASP.NET MVC의 일부 였던 어셈블리에 있었습니다. 따라서 사용 하기 위해 ASP.NET MVC를 설치할 필요가 없습니다를 `TagBuilder` 클래스입니다.
> 
> 그러나 클래스는 여전히는 `System.Web.Mvc` 네임 스페이스입니다. 사용 하기 위해 합니다 `TagBuilder` 클래스 (예를 들어, 사용자 지정 ASP.NET Razor 도우미)를 네임 스페이스를 참조 해야 합니다 (예를 들어, 추가 하 여 `@using System.Web.Mvc` 코드에).


#### <a name="change-request-validation-syntax-changed-validation-class-removed"></a>변경: 요청 유효성 검사 구문이 변경 되었습니다. "유효성 검사" 클래스 제거

> Beta 3 릴리스에 개별 필드 또는 필드의 집합에 대 한 유효성 검사를 사용 하지 않도록 설정 하려면 호출 하 여는 `Validation.Exclude` 메서드를 유효성 검사에서 제외할 필드의 이름을 전달 합니다. 새로운 구문 유효성 검사를 생략 하는 것에 대 한 Beta 3 릴리스에 제공 됩니다. `Validation` Beta 3에서 사용 하는 메서드가 제거 되었습니다.
> 
> > [!NOTE]
> > 웹 사이트와 같은 오류를 보고 사용자 (예를 들어, 서식 있는 텍스트 편집기를 사용 하 여 페이지)에서 HTML 태그를 업로드 하려고 하는 경우 요청 유효성 검사를 해제 하지 않는 경우 *클라이언트에서잠재적으로위험한Request.Form값이검색되었습니다*사용자 입력이 허용 되지 않습니다. 잠재적으로 위험한 태그를 포함 하거나 하지 같이 사용 하 여 스크립트 되도록 사용자 입력 요청 유효성 검사를 비활성화 하면 수동으로 확인 해야 합니다는 [Microsoft Anti-cross Site Scripting Library V4.0](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651)합니다.
> 
> 
> 자동 요청 유효성 검사를 해제 하려면 호출을 `Request.Unvalidated` 메서드, 필드 또는 다른 게시물 개체에 대 한 요청 유효성 검사를 무시 하려는 이름을 전달 합니다. 이 메서드를 사용 하 여 모든 항목에 대 한 유효성 검사를 무시 하는 `Form`, `QueryString`를 `Cookies`, 및 `ServerVariables` 컬렉션입니다. 다음 예제에 사용 하는 방법을 보여 줍니다는 `Unvalidated` 메서드:
> 
> [!code-csharp[Main](beta3/samples/sample4.cs)]


<a id="Issues"></a>

#### <a name="known-issues-for-aspnet-web-pages-with-razor-syntax"></a>Razor 구문이 있는 ASP.NET 웹 페이지에 대 한 알려진된 문제

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a>문제: 예기치 않은 동작이 멤버 자격에 대 한 사용자 테이블을 사용 하는 경우

> 호출 하는 ASP.NET Razor 웹 사이트에 대 한 멤버 자격 공급자를 초기화 하는 `WebSecurity.InitializeDatabaseConnection` 메서드. (시작 사이트 템플릿의 WebMatrix에서이 메서드에 대 한 호출을 포함 합니다  *\_AppStart.cshtml* 파일입니다.) 경우는 `autoCreateTables` 이 메서드의 매개 변수 설정을 true로 (기본적으로 설정은 시작 사이트 템플릿의 true), 하며 메서드는 인식할 수 없는 테이블 이름 (두 번째 매개 변수) 메서드에 전달 되 면 오류가 발생 하지 않습니다. 대신 테이블을 자동으로 만듭니다.
> 
> 이 멤버 자격에 대 한 사용자 테이블을 사용 하지만 잘못 된 테이블 이름을 전달 하려는 경우 문제가 될 수는 `WebSecurity.InitializeDatabaseConnection` 메서드. 메서드는 기본적으로 오류가 발생 하지 지정한 테이블 없으면 및 대신 새 테이블을 만들기 때문에 응용 프로그램 작동에 나타날 수 있습니다. 그러나 사용자 테이블 (및 해당 필드에)를 사용 하는 응용 프로그램 코드 예기치 않은 오류를 사용 하 여 최종적으로 실패할 수 있습니다.
> 
> **해결 방법**  
> 이름에 성공 했는지 확인 합니다 `InitializeDatabaseConnection` 사용자 프로필 멤버 자격 데이터베이스에서 테이블 또는 했는지 메서드 일치를 `autoCreateTables` 매개 변수를 false로.


#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a>문제: "못했습니다" SQL Server의 사용자 인스턴스 생성 오류

> WebMatrix 웹 응용 프로그램을 SQL Server Express를 사용 하 여 Windows 7 또는 Windows Server 2008 R2에서 IIS 7.5를 실행 중인 경우 SQL Server가 런타임 시 사용자의 로컬 응용 프로그램 경로 검색할 수 없습니다 나타내는 오류가 표시 될 수 있습니다.
> 
> **해결 방법** 응용 프로그램 (일반적으로 NETWORK SERVICE)에서 실행 되는 Windows 계정에 하위 폴더 및 응용 프로그램의 루트 폴더에 대 한 읽기/쓰기 권한을 같은 *앱\_데이터*. 자세한 내용은 기술 자료 문서에서 사용할 수 [SQL Server Express 사용자 인스턴스 및 ASP.net 웹 응용 프로그램 프로젝트를 사용 하 여 문제](https://support.microsoft.com/kb/2002980)합니다.


#### <a name="issue-in-visual-studio-namespaces-for-custom-assemblies-dlls-are-not-imported-automatically"></a>문제: Visual Studio에서 사용자 지정 어셈블리 (Dll)에 대 한 네임 스페이스는 자동 가져올 수 없습니다.

> Visual Studio에서 프로젝트의 사용자 지정 어셈블리를 사용 하는 경우에 디자인 타임에 해당 어셈블리에 선언 된 네임 스페이스는 자동으로 가져오지 않습니다. 결과적으로, 사용자 지정 형식에 대 한 참조 디자인 타임에 인식 하지 않으며 ("물결선" 사용)에서 인식할 수 없는 Visual Studio로 표시 됩니다. Visual Studio에서 디자인 타임에만이 문제가 발생 응용 프로그램 자체가 제대로 실행 됩니다.
> 
> **해결 방법**  
> 포함 된 `using` 문 (`imports` Visual Basic의) 디자인 타임에 인식 되지 않는 엔터티를 참조 하는 합니다.


#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a>문제: Visual Studio IntelliSense 및 프로젝트 템플릿이 ASP.NET MVC 3 버전 에서만 사용할 수 있습니다

> ASP.NET 웹 페이지를 설치 설치 하지 않습니다도 도구 Visual Studio에 대 한 예: ASP.NET Web Pages 응용 프로그램에 대 한 IntelliSense 및 프로젝트 템플릿.
> 
> **해결 방법** 웹 플랫폼 설치 관리자를 통해 ASP.NET MVC 3 RC 설치 Visual Studio에서 ASP.NET 웹 페이지 응용 프로그램에 대 한 IntelliSense 및 프로젝트 템플릿을 사용 하려면 또는 [독립 실행형 설치 관리자](https://go.microsoft.com/fwlink/?LinkID=191797)합니다.


#### <a name="issue-lthelpergt-class-cannot-be-found-error"></a>문제: "&lt;도우미&gt; 클래스를 찾을 수 없습니다" 오류

> Beta 3으로 업그레이드 한 후 오류가 표시 될 수 있습니다 하는 도우미 클래스 (예를 들어를 `Facebook` 클래스)를 찾을 수 없습니다. Beta 2에서 시작 하 고 베타 3에서 계속에 명시적으로 설치 해야 하는 패키지 도우미 이동 되었습니다. 이러한 패키지를 포함 하도록 기존 사이트는 업그레이드 되지 않습니다. 여기에 사이트를 *\My Documents\IISExpress* 또는 *\My Documents\My 웹 사이트* 폴더입니다. 기본 사이트를 사용 하는 경우이 오류가 표시 됩니다는 특히 *내 사이트* 에 대 한 참조를 포함 하는 (WebSite1)는 `Twitter` 도우미입니다.
> 
> **해결 방법**  
> 모든 도우미 사이트에서 실행에 대 한 호출을 주석 합니다  *\_관리자* 페이지 및 사용 하려는 도우미를 포함 하는 패키지를 설치 합니다. 패키지를 설치한 후 도우미 참조 하는 줄을 주석 처리 제거 합니다.


#### <a name="issue-deploying-beta-3-aspnet-razor-assemblies-to-the-bin-folder-might-not-work-on-hosting-sites"></a>문제: 베타 3 ASP.NET Razor 어셈블리를 Bin 폴더로 배포에서 작동할 수 없습니다 사이트 호스팅

> 호스팅 사이트에는 ASP.NET Web Pages 웹 사이트를 배포 하는 경우 및 사이트의 ASP.NET Razor 베타 3 어셈블리를 배포 하는 경우 *Bin* 폴더에 다음을 비롯 한 오류가 발생할 수 있습니다.
> 
> `Could not load type 'Microsoft.Web.Infrastructure.DynamicModuleHelper.DynamicModuleUtility' from assembly 'Microsoft.Web.Infrastructure, Version=1.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`
> 
> 이 호스팅 공급자가 서버의 전역 어셈블리 캐시 (GAC)에 ASP.NET 웹 페이지 베타 1 어셈블리를 설치 하는 경우 발생할 수 있습니다. GAC의 어셈블리 우선적으로 로컬에 설치 된 어셈블리를 *Bin* 폴더입니다.
> 
> **해결 방법** 오류가 표시 되는 공급자의 버전 간의 충돌로 인해 있는지 확인 하려면 호스팅 공급자에 게 문의 어셈블리 및 사용자. 그렇다면, 호스팅 공급자는 서버의 GAC에 어셈블리를 업데이트 하는 요청입니다.


#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a>문제: 프록시 서버를 통해 다른 외부 데이터 나 피드 읽기

> 에 대 한 프록시 정보를 구성 해야 사이트를 실행 하는 서버를 프록시 서버로 보호 하는 경우는 *Web.config* 외부 사이트에서 제공 되는 정보를 읽을 수 있도록 파일입니다. 예를 들어, 사용 하는 경우는 `ReCaptcha` 도우미 도우미 reCAPTCHA 서비스와 통신 하지만 프록시 서버에서 차단 될 수 있습니다. 마찬가지로, 패키지 관리자를 사용한 피드 등 ASP.NET 웹 페이지에서 사용 되는 피드 프록시 구성이 필요할 수 있습니다.
> 
> 패키지 피드를 사용 하거나 외부 서비스를 사용 하 여 작업에 문제가 있는 경우 다음 요소를 응용 프로그램의 루트에 배치 *Web.config* 파일:
> 
> [!code-xml[Main](beta3/samples/sample5.xml)]
> 
> 프록시 서버를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [ &lt;프록시&gt; 요소 (네트워크 설정)](https://msdn.microsoft.com/library/sa91de1e.aspx) MSDN 웹 사이트입니다.


#### <a name="issue-microsoftwebinfrastructuredll-cannot-be-loaded-error"></a>문제: "Microsoft.Web.Infrastructure.dll를 로드할 수 없습니다." 오류

> 이전에 Razor 구문이 있는 ASP.NET 웹 페이지의 베타 1 버전을 설치 하 고 다음 베타 3 버전을 설치 하는 경우 모든 적절 한 어셈블리 제외 하 고 GAC에 설치 됩니다 *Microsoft.Web.Infrastructure.dll*합니다. 따라서 ASP.NET Razor 페이지를 실행 하면 오류가 발생 함을 *Microsoft.Web.Infrastructure.dll* 로드할 수 없습니다.
> 
> 클린 컴퓨터에서 베타 3 릴리스를 로드 하는 경우에이 문제가 발생 하지 않습니다.
> 
> **해결 방법**  
> 제어판에서 ASP.NET 웹 페이지를 제거 합니다. 베타 3 릴리스를 다시 설치 합니다.


#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a>문제: Razor 구문이 있는 ASP.NET 웹 페이지를 사용 하지 않도록 설정.NET Framework 버전 4 제거 합니다.

> .NET Framework 버전 4 제거 하 고 다시 설치 하는 경우에 Razor 구문이 있는 ASP.NET 웹 페이지 비활성화 됩니다. 사용 하 여 페이지의 *.cshtml* 확장 제대로 실행 되지 않는 경우. 컴퓨터 루트에 있는 어셈블리를 등록 하는 ASP.NET 웹 페이지 *Web.config* 파일 및.NET Framework를 제거 합니다. 해당 파일을 제거 합니다. .NET Framework를 다시 설치 하면 구성 파일의 새 버전을 설치 하지만 ASP.NET 웹 페이지 어셈블리에 대 한 참조를 추가 하지 않습니다.
> 
> **해결 방법** .NET Framework를 다시 설치한 후 Razor 구문이 있는 ASP.NET 웹 페이지를 다시 설치 합니다. 다음 요소를 추가 합니다 *Web.config* 일반적으로 다음 위치에 있는 컴퓨터 루트에 있는 파일:  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> 
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](beta3/samples/sample6.xml)]


#### <a name="issue-applications-previously-deployed-with-aspnet-assemblies-in-the-bin-folder-experience-errors"></a>문제: Bin 폴더에 ASP.NET 어셈블리를 사용 하 여 이전에 배포 된 응용 프로그램 오류가 발생 합니다.

> ASP.NET 웹 페이지 어셈블리의 복사본을 배포 하는 동안 (예를 들어 *Microsoft.WebPages.dll*)에 *Bin* 서버의 웹 사이트의 폴더입니다. (이 때문일 수 있습니다 자동으로 배포 하는 동안 개발자는 어셈블리를 명시적으로 복사 되므로 또는.) 그러나 베타 3 릴리스를 설치할 때 오류 발생, 특정 형식을 찾을 수 있는 오류와 같은 합니다. ASP.NET Web Pages 형식의 숫자로 Beta 3 릴리스에 대 한 다른 네임 스페이스로 이동 된이 발생 합니다.
> 
> **해결 방법**   
> 선택을 취소는 *Bin* 배포 된 응용 프로그램의 새 어셈블리 폴더에 복사 (또는 응용 프로그램을 재배포) 한 다음 응용 프로그램 다시 시작 합니다.


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
> - 서버 컴퓨터에 대 한 제어 없는 경우 (예를 들어, 배포 하는 호스팅 웹 사이트), 웹 사이트의 다음 추가할 *Web.config* 파일:
> 
> 
> [!code-xml[Main](beta3/samples/sample7.xml)]


#### <a name="issue-using-web-application-project-or-aspnet-mvc-and-aspnet-web-pages-in-the-same-application"></a>문제: ASP.NET MVC 및 ASP.NET 웹 페이지 또는 웹 응용 프로그램 프로젝트를 사용 하 여 동일한 응용 프로그램

> ASP.NET 웹 페이지에서 웹 응용 프로그램 프로젝트 또는 ASP.NET MVC 응용 프로그램을 사용할 때 오류가 표시 될 수 있습니다 하 *WebPageHttpApplication* 찾을 수 없습니다.
> 
> **해결 방법**  
> 이 오류가 발생할 경우 응용 프로그램 파생 되는 기본 클래스를 변경 합니다. 에 *Global.asax* 파일에서 다음 줄을 변경 합니다.
> 
> [!code-csharp[Main](beta3/samples/sample8.cs)]
> 
> 다음과 같이 변경
> 
> [!code-csharp[Main](beta3/samples/sample9.cs)]
> 
> 도입 된 변경 적용 반대로이 Razor 구문이 있는 ASP.NET 웹 페이지의 베타 1 릴리스에 대 한 합니다.


#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a>문제: SQL Server Compact 설치 되지 않은 컴퓨터에 응용 프로그램 배포

> SQL Server Compact 데이터베이스를 포함 하는 응용 프로그램 SQL Server Compact는 설치 되지 않은 컴퓨터에서 실행할 수 있습니다. Microsoft WebMatrix Beta 3에서 자동으로 이러한 이진 파일을 복사 하 고 적절 한 수행 *Web.config* 파일 변환 합니다.
> 
> **해결 방법** 이러한 파일을 복사 하 고 확인 해야 할 경우 합니다 *Web.config* 파일 변경 내용을 수동으로 다음을 수행 합니다.
> 
> 1. 데이터베이스 엔진 어셈블리를 복사 합니다 *Bin* 대상 컴퓨터에서 응용 프로그램의 폴더 (및 하위 폴더). 
> 
>     - Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* **to** *\Bin*
>     - 복사본 *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\** **하** *\Bin\x86*
>     - 복사본 *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\** **하** *\Bin\amd64*
> 2. 웹 사이트의 루트 폴더를 만들거나 엽니다는 *Web.config* 파일입니다. (WebMatrix 베타 3을이 파일 형식은 클릭할 경우 사용할 수 있습니다 **모든** 에 **파일 형식을 선택** 대화 상자.)
> 3. 다음 요소 자식으로 추가 합니다 **&lt;구성&gt;** 요소 (에 포함 되지 않은 합니다 **&lt;system.web&gt;** 요소):
> 
> 
> [!code-xml[Main](beta3/samples/sample10.xml)]


#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a>문제: 데이터베이스 및 WebGrid 도우미 Visual Basic에서 보통 신뢰에서 작동 하지 않습니다.

> Visual Basic을 사용 하는 경우 (만드는 *.vbhtml* 파일), `Database` 고 `WebGrid` 도우미 응용 프로그램은 보통 신뢰를 사용 하도록 설정 된 경우 작동 하지 것입니다.
> 
> **해결 방법**  
> 완전 신뢰를 사용 하 여 응용 프로그램을 일시적으로 설정 합니다.

<a id="Known_Issues_SQL_Server_Compact"></a>
### <a name="sql-server-compact"></a>SQL Server Compact

#### <a name="issue-encrypt-property-is-not-recognized"></a>문제: "Encrypt" 속성이 인식 되지 않습니다.

> SQL Server Compact 4.0 인식 하지 못합니다 합니다 `Encrypt` 의 속성을 `SqlCeConnection` 클래스. 데이터베이스 파일을 암호화 하려면이 속성을 사용 하지 해야 합니다. `Encrypt` 속성 된 SQL Server Compact 3.5 릴리스에서 사용 되지 않으며 이전 버전과 호환성을 위해서만 유지 되었습니다. 
> 
> **해결 방법**  
> 사용 하 여 합니다 `Encryption Mode` 의 속성을 `SqlCeConnection` SQL Server Compact 4.0 데이터베이스 파일을 암호화 하는 클래스입니다. 다음 예제에 사용 하 여 암호화 된 SQL Server Compact 4.0 데이터베이스를 만드는 방법을 보여 줍니다는 `Encryption Mode` 속성:
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

> 네이티브 Dll의 SQL Server Compact 4.0에는 Microsoft Visual c + + 2008 런타임 라이브러리 ((x86, IA64 및 x64), 서비스 팩 1에 필요합니다.
> 
> **해결 방법**  
> .NET Framework 3.5 SP1을 설치 합니다. Visual c + + 2008 런타임 라이브러리 SP1도 설치 합니다. 다음 위치에서 라이브러리를 다운로드할 수 있습니다.   
>   
> [Microsoft Visual c + + 2008 서비스 팩 1 재배포 가능 패키지 ATL 보안 업데이트](https://go.microsoft.com/fwlink/?LinkId=194827)
> 
> [!NOTE]
> .NET Framework 2.0, 3.0, 설치 또는 4 *되지* Visual c + + 2008 런타임 라이브러리에 SP1을 설치 합니다.


#### <a name="issue-if-sql-server-compact-is-installed-prior-to-installing-net-framework-on-the-computer-its-provider-invariant-name-is-not-registered-in-the-net-framework-machineconfig-file"></a>문제: 컴퓨터의.NET Framework를 설치 하기 전에 SQL Server Compact를 설치 하는 경우 해당 공급자 고정 이름에에서 등록 되지 않은.NET Framework machine.config 파일

> SQL Server Compact.NET Framework가 SQL Server Compact는.NET framework가 필요 하기 때문에 설치 되지 않은 컴퓨터에 설치할 수 있습니다. SQL Server Compact를 설치 하기 전에.NET Framework 버전 3.5 또는 4를 모두 설치 되어 있으면 SQL Server Compact 설치에서 공급자 고정 이름을 등록 하지 않습니다 합니다 *machine.config* 파일입니다. SQL Server Compact 항목을 사용 하는 모든 응용 프로그램을 *machine.config* 파일 실패 합니다. 고정 이름이 등록 항목 *machine.config* 다음과 같습니다.
> 
> [!code-xml[Main](beta3/samples/sample17.xml)]
> 
> **해결 방법**  
> SQL Server Compact 4.0 CTP1을 제거 합니다. 다운로드 하 고 다음 위치에서.NET Framework의 전체 버전을 설치 합니다.
> 
> [Microsoft.NET Framework 3.5 서비스 팩 1 (전체 패키지)](https://go.microsoft.com/fwlink/?LinkId=194828)  
> [Microsoft.NET Framework 4.0 릴리스 (전체 패키지)](https://www.microsoft.com/downloads/details.aspx?FamilyID=9cfb2d51-5ff4-4491-b0e5-b386f32c0992&amp;displaylang=en)
> 
> 제거한 [SQL Server Compact 4.0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en)합니다.


<a id="Known_Issues_Installing_Applications"></a>

### <a name="installing-applications"></a>응용 프로그램 설치

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a>문제: 응용 프로그램을 설치할 수 시간이 오래 걸릴 경우 사용자의 내 문서 폴더는 네트워크 공유로 리디렉션됩니다.

> **해결 방법**  
> 없음 응용 프로그램을 설치 하는 데 소요 되지만 제대로 설치 됩니다.


<a id="Known_Issues_Publishing_Applications"></a>

### <a name="publishing-applications"></a>응용 프로그램 게시

#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a>문제: 사이트 "대상 URL" 필드는 http:// 또는 https://로 시작 하지 않는 경우 게시 한 후 작동 하지 않을 수 있습니다.

> 에 **게시 설정** 대화 상자에서 대상 URL로 시작 하지 않는 경우 `http://` 또는 `https://`, 사이트 배포 후 작동 하지 않을 수 있습니다.
> 
> **해결 방법**  
> 있는지 확인 하는 사이트에서 대상 URL을 게시 하기 전에 합니다 **게시 설정** 대화 상자 시작 `http://` 또는 `https://`합니다.


#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a>문제: MySQL 데이터베이스를 게시할 오류로 인해 실패 "데이터베이스를 게시 하지 못했습니다. 이 경우 발생할 수 있습니다 원격 데이터베이스에서 스크립트를 실행할 수 없습니다. "

> 이 오류는 다양 한 이유로 발생할 수 있습니다. 이 오류를 확인할 수 있습니다 하는 이유 중 하나 이며 경우 데이터베이스 스크립트 문자가 작은따옴표 (') u t F-8로 대상 MySQL 데이터베이스의 기본 문자 집합이 아닙니다.
> 
> **해결 방법**  
> U t F-8로 원격 MySQL 데이터베이스에 대 한 기본 문자를 설정 합니다.


<a id="Known_Issues_Other_Issues"></a>

### <a name="other-issues"></a>기타 문제

#### <a name="issue-searchfilter-does-not-work-in-reports-for-group-by-issue-type"></a>문제: 검색/필터에 작동 하지 않습니다 보고서의 Group By: 문제 유형

> 텍스트를 입력 하는 경우 사이트에 대 한 보고서를 실행할 때 합니다 *URL 필터링* 상자 하 고 클릭 *검색*, 아무 일도 발생 합니다. 이 제어 하는 동안 작동 하지 않습니다. 왜냐하면 합니다 *Group By* 보고서의 상태가로 설정 된 *문제 유형*, 기본값입니다.
> 
> **해결 방법** 에 *Group By* 탭 리본 메뉴를 클릭 *URL* 해당 소스 URL에서 항목을 그룹화 하 합니다. 단추 항목을 필터링 하 고 텍스트 상자는이 상태에서 작동 합니다.


#### <a name="issue-wcf-applications-fail-to-run-with-iis-express"></a>문제: WCF 응용 프로그램이 실행 되지 IIS express

> WCF 응용 프로그램으로 이동 다음과 같은 오류가 발생 합니다.
> 
> *파일 또는 어셈블리를 로드할 수 없습니다 ' Microsoft.Web.Administration, 버전 7.0.0.0, Culture = neutral, PublicKeyToken = 31bf3856ad364e35 =' 또는 해당 종속성 중 하나입니다. 지정한 파일을 찾을 수 없습니다.*
> 
> IIS Express 베타 릴리스 기본적으로 WCF를 지원 하지 않으므로이 발생 합니다.
> 
> **해결 방법** 다음 해결 방법 중 하나를 사용 하 여 (해결 방법 2 필요한 Microsoft Windows Vista 이상):
> 
> 
> 1. 복사 합니다 *Microsoft.Web.dll* 하 고 *Microsoft.Web.Administration.dll* WebMatrix 설치 위치에서 어셈블리를 *bin* wcf 디렉터리 응용 프로그램입니다. 기본적으로 WebMatrix에서 설치 합니다 *Microsoft WebMatrix* 시스템의 하위 폴더 *Program Files* 폴더입니다.
> 2. Microsoft Windows Vista 이상에서의 어셈블리에 symlink를 만듭니다는 *bin* 디렉터리에서 다음 명령을 사용 합니다. (이 방법은 이점이 어셈블리의 복사본이 만들어지지 않습니다.)
> 
>     [!code-console[Main](beta3/samples/sample18.cmd)]
> 3. 두 어셈블리를 GAC에 설치 합니다. 상승된 된 프롬프트에서 다음 명령을 실행 합니다.
> 
>     [!code-console[Main](beta3/samples/sample19.cmd)]


#### <a name="issue-webmatrix-beta-3-is-unable-to-perform-certain-tasks-that-require-elevation"></a>문제: WebMatrix 베타 3 상승이 필요한 특정 작업을 수행할 수 없는

> WebMatrix 베타 3가 다음과 같은 상황에서 추가 구성 요소를 설치 하는 등의 권한 상승 해야 하는 특정 작업을 수행할 수 없습니다.
> 
> - Windows Vista 또는 Windows 7에서 관리자 권한이 없는 계정으로 로그온 한 사용자 계정 컨트롤 (UAC)을 사용할 수 없습니다.
> - Microsoft Windows XP 또는 Microsoft Windows Server 2003을 사용 하는 있습니다.
> 
> **해결 방법**  
> WebMatrix Beta 3에서 대부분의 작업에는 관리 권한이 필요 하지 않습니다. 이러한 조작자에 대 한 다음이 단계를 수행 또는 관리자로 서 작업을 수행할 수 있습니다.
> 
> - Windows Vista 또는 Windows 7에서 UAC를 사용 하도록 설정 합니다.
> - Windows XP에서 Administrators 보안 그룹에 사용자를 추가 합니다.


#### <a name="issue-site-from-web-gallery-is-disabled"></a>문제: "웹 갤러리에서 사이트"을 사용할 수 없습니다.

> 합니다 **웹 갤러리에서 사이트** 웹 플랫폼 설치 관리자 3.0이 설치 되지 않은 경우 옵션은 사용할 수 없습니다.
> 
> **해결 방법**  
> 설치 합니다 [Microsoft 웹 플랫폼 설치 관리자 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)합니다.


#### <a name="issue-on-windows-server-2003-iis-express-does-not-start-for-a-non-administrative-user"></a>문제: Windows Server 2003에서 IIS Express 시작 되지 않으면 관리자가 아닌 사용자에 대 한

> Windows Server 2003에서 페이지를 시작 하거나 IIS Express를 시작 하는 경우 IIS Express 시작 되지 않습니다. 웹 페이지 응용 프로그램 관리자가 아닌 사용자가 시작한 있는지 여부를 나타내는 오류가 표시 됩니다.
> 
> **해결 방법**  
> 관리자 권한으로 WebMatrix 베타 3을 시작 합니다. 자세한 내용은 다음 기술 자료 문서를 참조 하세요.  
>   
> [관리자가 아닌 사용자가 시작 되는 응용 프로그램은 응용 프로그램이 Windows Vista, Windows Server 2003 또는 Windows XP에서 실행 되는 컴퓨터의 HTTP 트래픽을 수신할 수 없습니다.](https://support.microsoft.com/kb/939786)


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


#### <a name="issue-the-relationships-button-is-disabled"></a>문제: "관계" 단추는 사용할 수 없습니다.

> **관계** 단추를 **테이블** 탭에 **데이터베이스** SQL Server Compact 데이터베이스에 대 한 작업 영역을 사용할 수 없습니다.
> 
> **해결 방법**  
> 없음 SQL Server Compact 테이블 간의 관계를 지원 하지 않습니다.


#### <a name="issue-parameterized-sql-queries-throw-exceptions"></a>문제: 매개 변수가 있는 SQL 쿼리 예외 throw

> SQL Server Compact 4.0에서는 데이터 형식 같은 지정 하지 않으면 `SqlDbType` 또는 `DbType` 매개 변수가 있는 쿼리에서 매개 변수의 경우 쿼리를 실행할 때 예외가 throw 됩니다.
> 
> **해결 방법**  
> 와 같은 매개 변수의 데이터 형식을 명시적으로 설정할 `SqlDbType` 또는 `DbType`합니다. 이 BLOB 데이터 형식의 경우 중요 (`image` 고 `ntext`). 다음과 같은 코드를 사용 합니다.
> 
> [!code-sql[Main](beta3/samples/sample20.sql)]
> 
> [!code-vb[Main](beta3/samples/sample21.vb)]


<a id="More_Info"></a>

## <a name="for-more-information"></a>자세한 내용

WebMatrix 베타 3에 대 한 자세한 내용은 다음 웹 사이트를 참조 하세요.

- [IIS.net](http://iis.net/)
- [ASP.NET](https://asp.net/webmatrix)
- [Microsoft.com/web](https://www.microsoft.com/web)

* * *

© 2010 Microsoft Corporation. All Rights Reserved. [사용 약관](https://msdn.microsoft.cos/cc300389.aspx)합니다.
