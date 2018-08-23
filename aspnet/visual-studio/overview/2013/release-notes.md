---
uid: visual-studio/overview/2013/release-notes
title: ASP.NET 및 Web Tools for Visual Studio 2013 릴리스 정보 | Microsoft Docs
author: microsoft
description: 이 문서에서는 Visual Studio 2013 용 ASP.NET 및 웹 도구 릴리스를 설명 합니다.
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: 44ab88b61a96235da27ff41d6b649bfd7fce3e38
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41837026"
---
<a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a>ASP.NET 및 Web Tools for Visual Studio 2013 릴리스 정보
====================
[Microsoft](https://github.com/microsoft)

> 이 문서에서는 Visual Studio 2013 용 ASP.NET 및 웹 도구 릴리스를 설명 합니다.


## <a name="contents"></a>목차

- [설치 참고 사항](#TOC1)
- [문서](#TOC2)
- [소프트웨어 요구 사항](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>ASP.NET 및 Web Tools for Visual Studio 2013의 새로운 기능

- [One ASP.NET](#TOC6)
- [새 웹 프로젝트 환경](#newproj)
- [ASP.NET 스 캐 폴딩](#scaffold)
- [브라우저 링크](#browser-link)
- [Visual Studio 웹 편집기 향상 기능](#web-editor)
- [Visual Studio에서 azure App Service 웹 앱 지원](#waws)
- [향상 된 기능으로 웹 게시](#publish)
- [NuGet 2.7](#nuget)
- [ASP.NET Web Forms](#TOC9)
- [ASP.NET MVC 5](#TOC10)
- [ASP.NET Web API 2](#TOC11)
- [ASP.NET SignalR](#TOC13)
- [ASP.NET Id](#TOC8)
- [Microsoft OWIN 구성 요소](#TOC7)
- [Entity Framework 6](#ef6)
- [ASP.NET Razor 3](#TOC14)
- [ASP.NET 앱 일시 중단](#TOC15)
- [알려진된 문제 및 주요 변경 내용](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a>설치 참고 사항

ASP.NET 및 Web Tools for Visual Studio 2013의 기본 설치 관리자를 번들로 제공 되 고 다운로드할 수 있습니다 [여기](https://www.asp.net/downloads)합니다.

<a id="TOC2"></a>
## <a name="documentation"></a>설명서

자습서 및 Visual Studio 2013 용 ASP.NET 및 Web Tools에 대 한 다른 정보에서 사용할 수는 [ASP.NET 웹 사이트](https://www.asp.net/)합니다.

<a id="TOC4"></a>
## <a name="software-requirements"></a>소프트웨어 요구 사항

ASP.NET 및 Web Tools Visual Studio 2013이 필요 합니다.

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>ASP.NET 및 Web Tools for Visual Studio 2013의 새로운 기능

다음 섹션에서는 릴리스에서 도입 된 기능을 설명 합니다.

<a id="TOC6"></a>
## <a name="one-aspnet"></a>One ASP.NET

Visual Studio 2013 릴리스를 쉽게 조합 하 고 싶지는 일치 수 있도록 ASP.NET 기술을 사용 하 여 환경을 통합 위한 단계로 이동 합니다. 예를 들어, 있습니다 수 MVC를 사용 하 여 프로젝트를 시작 및 쉽게 나중에 프로젝트를 Web Forms 페이지를 추가 또는 Web Forms 프로젝트에서 Web Api 스 캐 폴드 합니다. One ASP.NET은 쉽게를 ASP.NET에서 제공 하는 작업을 수행 하려면 개발자입니다. 원하는 어떤 기술에 관계 없이 One ASP.NET의 신뢰할 수 있는 기본 프레임 워크에서 작성 중인 자신 있게를 할 수 있습니다.

<a id="newproj"></a>
## <a name="new-web-project-experience"></a>새 웹 프로젝트 환경

Visual Studio 2013에서 새 웹 프로젝트를 만드는 환경을 향상 되었습니다. 에 **새 ASP.NET 웹 프로젝트** 대화 원하는, (Web Forms, MVC, Web API) 기술의 조합을 구성 하 고, 인증 옵션을 구성한 단위 테스트 프로젝트를 추가 하는 프로젝트 유형을 선택할 수 있습니다.

![새 ASP.NET 프로젝트](release-notes/_static/image1.png)

새 대화 상자를 사용 하면 다양 한 서식 파일에 대 한 기본 인증 옵션을 변경할 수 있습니다. 예를 들어, ASP.NET Web Forms 프로젝트를 만들 때 다음 옵션 중 하나로 선택할 수 있습니다.

- 인증 안 함
- 개별 사용자 계정 (ASP.NET 멤버 자격 또는 소셜 공급자 로그인)
- 조직 계정 (인터넷 응용 프로그램에서 Active Directory)
- Windows 인증 (인트라넷 응용 프로그램에서 Active Directory)

![인증 옵션](release-notes/_static/image2.png)

웹 프로젝트를 만들기 위한 새 프로세스에 대 한 자세한 내용은 참조 하세요. [Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기](creating-web-projects-in-visual-studio.md)합니다. 새 인증 옵션에 대 한 자세한 내용은 참조 하세요. [ASP.NET Id](#TOC8) 이 문서의 뒷부분에 나오는.

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a>ASP.NET 스 캐 폴딩

ASP.NET 스 캐 폴딩은 ASP.NET 웹 응용 프로그램에 대 한 코드 생성 프레임 워크. 쉽게 데이터 모델과 상호 작용 하는 프로젝트에 상용구 코드를 추가 합니다.

이전 버전의 Visual Studio에서 스 캐 폴딩 ASP.NET MVC 프로젝트에 있었습니다. Visual Studio 2013을 사용 하 여 Web Forms를 비롯 한 모든 ASP.NET 프로젝트에 대 한 스 캐 폴딩을 이제 사용할 수 있습니다. Visual Studio 2013 생성 페이지는 Web Forms 프로젝트에 대 한 현재 지원 하지 않습니다 하지만 프로젝트에 MVC 종속성을 추가 하 여 Web forms 스 캐 폴딩을 계속 사용할 수 있습니다. Web Forms에 대 한 페이지를 생성 하는 것에 대 한 지원이 향후 업데이트에서 추가 됩니다.

스 캐 폴딩을 사용 하는 경우 프로젝트의 종속성이 설치 되어 필요한 모든 것을 확인 합니다. 예를 들어, ASP.NET Web Forms 프로젝트를 시작 하 고 다음 스 캐 폴딩을 사용 하 여 Web API 컨트롤러를 추가할 경우 필요한 NuGet 패키지와 참조를 프로젝트에 자동으로 추가 됩니다.

MVC 스 캐 폴딩에 Web Forms 프로젝트를 추가 하려면 추가 된 **새 스 캐 폴드 된 항목** 선택한 **MVC 5 종속성** 대화 상자에서. 두 가지 옵션이 있습니다; MVC 스 캐 폴딩에 대 한 최소 및 전체. 최소를 선택 하면 프로젝트에 NuGet 패키지 및 ASP.NET MVC에 대 한 참조만 추가 됩니다. 전체 옵션을 선택 하는 경우 MVC 프로젝트에 필요한 콘텐츠 파일 뿐만 아니라 최소한의 종속성에 추가 합니다.

Entity Framework 6에서 새 비동기 기능을 사용 하는 비동기 컨트롤러 스 캐 폴딩에 대 한 지원.

자세한 내용 및 자습서를 참조 하세요 [ASP.NET 스 캐 폴딩 개요](aspnet-scaffolding-overview.md)합니다.

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a>브라우저 링크-브라우저 및 Visual Studio 간의 SignalR 채널

새 [브라우저 링크](using-browser-link.md) 를 통해 Visual Studio에 여러 브라우저를 연결 하 고 도구 모음에서 단추를 클릭 하 여 새로 고칠 수 있습니다. 모바일 에뮬레이터를 비롯 하 여 개발 사이트에 여러 브라우저를 연결할 수 있고 동시에 모든 모든 브라우저 새로 고침에 새로 고침을 클릭 합니다. 브라우저 링크에는 또한 개발자가 브라우저 링크 확장을 작성할 수 있도록 하기 위한 API를 노출 합니다.

![](release-notes/_static/image3.png)

브라우저 링크 API를 활용 하는 개발자를 사용 하 여 Visual Studio와 연결 된 모든 브라우저 간의 경계를 교차 하는 고급 시나리오를 만들 수 있습니다. Web Essentials는 Visual Studio 및 브라우저의 개발자 도구, 원격 제어 모바일 에뮬레이터 및 많은 간에 통합된 된 환경을 만들려면 API 활용 합니다.

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a>Visual Studio 웹 편집기 향상 기능

Visual Studio 2013 웹 응용 프로그램에 HTML 파일과 Razor 파일에 대 한 새 HTML 편집기를 포함합니다. 새 HTML 편집기는 HTML5를 기반으로 단일 통합된 스키마를 제공 합니다. 자동 중괄호 완성, jQuery UI 및 AngularJS IntelliSense 특성, 특성 IntelliSense 그룹화, ID 및 Intellisense, 클래스 이름 및 보다 나은 성능, 서식 지정을 비롯 한 다른 개선 사항 및 스마트 태그입니다.

다음 스크린 샷에서 HTML 편집기에서 IntelliSense 부트스트랩 특성을 사용 하는 방법을 보여 줍니다.

![HTML 편집기의 Intellisense](release-notes/_static/image4.png)

Visual Studio 2013에는 기본 제공 편집기 덜 모두 CoffeeScript와도 제공 됩니다. LESS 편집기 CSS 편집기에서 훌륭한 기능이 함께 있고 변수 및 mixin 특정 Intellisense에서 작은 모든 문서는 @import 체인입니다.

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a>Visual Studio에서 azure App Service 웹 앱 지원

Azure SDK for.NET 2.2를 사용 하 여 Visual Studio 2013에서 사용할 수 있습니다 **서버 탐색기** 원격 웹 앱의 직접 상호 작용 하도록 합니다. Azure 계정에 로그인 할 수 있습니다 새 웹 앱을 만들 되, 앱 구성, 실시간 로그 보기. SDK 2.2 즉시 제공 하는 것은 해제, Azure에서 원격으로 디버그 모드로 실행할 수 있습니다. 또한 대부분의 Azure App Service Web Apps에 대 한 새 기능이.NET 용 Azure SDK의 현재 릴리스를 설치할 때 Visual Studio 2012에서 작동 합니다.

자세한 내용은 다음 리소스를 참조하세요.

- [Azure App Service에서 ASP.NET 웹 앱 만들기](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [Visual Studio를 사용하여 Azure App Service의 웹앱 문제 해결](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a>향상 된 기능으로 웹 게시

Visual Studio 2013에는 새로운 기능과 향상 된 웹 게시 기능이 포함 됩니다. 그 중 일부는 다음과 같습니다.

- 쉽게 [Web.config 파일 암호화 자동화](https://go.microsoft.com/fwlink/?LinkId=325529)합니다. (이 링크 및 다음 두 지점 저녁에 10/17에까지 사용 하지 못할 수 있는 msdn 설명서입니다.)
- 쉽게 [는 응용 프로그램 오프 라인으로 배포 하는 동안 자동화](https://go.microsoft.com/fwlink/?LinkId=325530)합니다.
- 웹 배포를 구성 [파일 체크섬을 사용 하 여 마지막 변경 날짜 대신](https://go.microsoft.com/fwlink/?LinkId=325531) 서버로 파일을 복사할지를 결정 합니다.
- 파일 시스템 메서드를 게시 또는 FTP를 사용 하는 경우 뿐만 아니라 웹 배포에서 개별 선택한 파일 (Web.config 포함)를 신속 하 게 게시 합니다.

ASP.NET 웹 배포에 대 한 자세한 내용은 참조 하세요. [ASP.NET 사이트](https://go.microsoft.com/fwlink/?LinkId=322027)합니다.

<a id="nuget"></a>
## <a name="nuget-27"></a>NuGet 2.7

NuGet 2.7에 자세히 설명 하는 새로운 기능의 다양 한 집합을 포함 [NuGet 2.7 릴리스 정보](http://docs.nuget.org/docs/release-notes/nuget-2.7)합니다.

이 버전의 NuGet 패키지를 다운로드 하도록 NuGet의 패키지 복원 기능에 대 한 명시적인 동의 제공할 필요가 사라집니다. 동의 (및 NuGet의 기본 설정 대화 상자에서 관련된 확인란) NuGet을 설치 하 여 부여 됩니다. 이제 패키지 복원은 단순히 기본적으로 작동합니다.

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a>ASP.NET Web Forms

### <a name="one-aspnet"></a>One ASP.NET

Web Forms 프로젝트 템플릿은 새로운 One ASP.NET 환경을 원활 하 게 통합 합니다. Web Forms 프로젝트에 MVC 및 Web API를 지원 하 고 One ASP.NET 프로젝트 만들기 마법사를 사용 하 여 인증을 구성할 수 있습니다를 추가할 수 있습니다. 자세한 내용은 [Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기](creating-web-projects-in-visual-studio.md)합니다.

### <a name="aspnet-identity"></a>ASP.NET ID

Web Forms 프로젝트 템플릿에 새 ASP.NET Id 프레임 워크를 지원 합니다. 또한 템플릿을 이제 Web Forms 인트라넷 프로젝트의 생성을 지원합니다. 자세한 내용은 [인증 방법을](creating-web-projects-in-visual-studio.md#auth) 에 **Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기**합니다.

### <a name="bootstrap"></a>부트스트랩

Web Forms 템플릿을 사용 하 여 [부트스트랩](http://twitter.github.io/bootstrap/) 를 세련 되 고 응답성이 뛰어난 디자인을 쉽게 사용자 지정할 수 있도록 합니다. 자세한 내용은 [Visual Studio 2013 웹 프로젝트 템플릿에서 부트스트랩](creating-web-projects-in-visual-studio.md#bootstrap)합니다.

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a>ASP.NET MVC 5

### <a name="one-aspnet"></a>One ASP.NET

웹 MVC 프로젝트 템플릿을 새 One ASP.NET 환경을 원활 하 게 통합 합니다. MVC 프로젝트를 사용자 지정할 수 있으며 One ASP.NET 프로젝트 만들기 마법사를 사용 하 여 인증을 구성할 수 있습니다. ASP.NET MVC 5 소개 자습서에서 확인할 수 있습니다 [ASP.NET MVC 5 시작](../../../mvc/overview/getting-started/introduction/getting-started.md)합니다.

MVC 4 프로젝트에서 MVC 5 업그레이드에 대 한 자세한 내용은 [ASP.NET MVC 5 및 Web API 2에는 ASP.NET MVC 4 및 Web API 프로젝트를 업그레이드 하는 방법](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)합니다.

### <a name="aspnet-identity"></a>ASP.NET ID

MVC 프로젝트 템플릿 인증 및 id 관리에 대 한 ASP.NET Id를 사용 하도록 업데이트 되었습니다. Facebook 및 Google 인증 및 새 멤버 자격 API 자습서에서 확인할 수 있습니다 [Facebook 및 Google OAuth2 및 OpenID Sign on을 사용 하 여 ASP.NET MVC 5 앱 만들기](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 고 [인증을 사용 하 여 ASP.NET MVC 앱 만들기 및 SQL DB 및 Azure App Service에 배포](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)합니다.

### <a name="bootstrap"></a>부트스트랩

MVC 프로젝트 템플릿을 사용 하도록 업데이트 되었습니다 [부트스트랩](http://getbootstrap.com/) 를 세련 되 고 응답성이 뛰어난 디자인을 쉽게 사용자 지정할 수 있도록 합니다. 자세한 내용은 [Visual Studio 2013 웹 프로젝트 템플릿에서 부트스트랩](creating-web-projects-in-visual-studio.md#bootstrap)합니다.

### <a name="authentication-filters"></a>인증 필터

인증 필터는 ASP.NET MVC 파이프라인에서 권한 부여 필터 전에 실행 하 고 인증 논리 작업을 지정할 수 있는 ASP.NET MVC에서 필터의 새 종류 컨트롤러 별로 또는 모든 컨트롤러에 대 한 전역적으로 합니다. 인증 필터는 요청에 자격 증명을 처리 하 고 해당 보안 주체를 제공 합니다. 인증 필터 권한이 없는 요청에 대 한 응답에서 인증 질문을 추가할 수도 있습니다.

### <a name="filter-overrides"></a>필터 재정의

재정의 필터를 지정 하 여 지정 된 동작 메서드 또는 컨트롤러에 적용 하는 필터가 재정의할 수 있습니다. 재정의 필터에 지정된 된 범위 (작업 또는 컨트롤러)에 대 한 실행 되지 않아야 하는 필터 형식 집합을 지정 합니다. 이 통해 전역적으로 적용 되지만 다음의 특정 작업이 나 컨트롤러에 적용에서 특정 전역 필터를 제외 하는 필터를 구성할 수 있습니다.

### <a name="attribute-routing"></a>특성 라우팅

ASP.NET MVC는 이제 특성 라우팅, Tim McCall, 작성자에 의해 작성 글 덕분 [ http://attributerouting.net ](http://attributerouting.net)합니다. 특성 라우팅을 사용 하 여 작업 및 컨트롤러에 주석을 추가 하 여 경로 지정할 수 있습니다.

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a>ASP.NET Web API 2

### <a name="attribute-routing"></a>특성 라우팅

ASP.NET Web API는 이제 특성 라우팅, Tim McCall, 작성자에 의해 작성 글 덕분 [ http://attributerouting.net ](http://attributerouting.net)합니다. 특성 라우팅을 사용 하 여 작업 및 컨트롤러 다음과 같은 주석을 추가 하 여 Web API 경로 지정할 수 있습니다.

[!code-csharp[Main](release-notes/samples/sample1.cs)]

특성 라우팅을 제어할 수 자세한 Uri 통해 web API에에서 있습니다. 예를 들어, 단일 API 컨트롤러를 사용 하 여 리소스 계층을 쉽게 정의할 수 있습니다.

[!code-csharp[Main](release-notes/samples/sample2.cs)]

특성 라우팅도 선택적 매개 변수, 기본값 및 경로 제약 조건을 지정 하는 데 편리한 구문을 제공 합니다.

[!code-csharp[Main](release-notes/samples/sample3.cs)]

특성 라우팅에 대 한 자세한 내용은 참조 하세요. [Web API 2에서 특성 라우팅](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md)합니다.

### <a name="oauth-20"></a>OAuth 2.0

Web API 및 단일 페이지 응용 프로그램 프로젝트 템플릿에 이제 OAuth 2.0을 사용 하 여 인증을 지원 합니다. OAuth 2.0은 보호 된 리소스에 대 한 클라이언트 액세스 권한 부여를 위한 프레임 워크입니다. 다양 한 브라우저 및 모바일 장치를 포함 하 여 클라이언트에서 작동 합니다.

OAuth 2.0 지원은 새 보안 미들웨어는 권한 부여 서버 역할을 구현 및 Microsoft OWIN 구성 요소에서 제공 하는 전달자 인증에 대 한 기반으로 합니다. 또는 Azure Active Directory 또는 Windows Server 2012 r 2에서 ADFS와 같은 조직 권한 부여 서버를 사용 하 여 클라이언트에 권한을 수 있습니다.

### <a name="odata-improvements"></a>OData 개선 사항

**$Batch, 및 $value $select, $에 대 한 지원 확장**

ASP.NET Web API OData 이제에 완벽 하 게 지원 $select, $expand, 및 $value 합니다. 변경 집합 처리 및 일괄 처리 요청에 대 한 $batch를 이용할 수 있습니다.

$Select 및 $expand 옵션 OData 끝점에서 반환 되는 데이터의 모양을 변경할 수 있습니다. 자세한 내용은 [$select 소개 및 $expand에 Web API OData 지원](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md)합니다.

**향상 된 확장성**

OData 포맷터를 확장할 수 있는 됩니다. Atom 항목 메타 데이터 추가 명명 된 스트림 및 미디어 링크 항목을 지원 및 인스턴스 주석을 추가 링크 생성 되는 방식을 사용자 지정할 수 있습니다.

**형식이 없으므로 지원**

이제 엔터티 형식에 대 한 CLR 형식을 정의 하지 않고도 OData 서비스를 빌드할 수 있습니다. OData 컨트롤러 수 걸리거나의 인스턴스를 반환 하는 대신 **IEdmObject**는 직렬화/역직렬화는 OData 포맷터 됩니다.

**기존 모델을 다시 사용**

기존 엔터티 데이터 모델 (EDM)에 이미 있는 경우 이제 다시 사용할 수 있습니다을 직접 새로 작성 하는 대신 합니다. 예를 들어, Entity Framework를 사용 하는 경우 EF를 작성 하는 EDM을 사용할 수 있습니다.

### <a name="request-batching"></a>일괄 처리 요청

일괄 처리 요청은 네트워크 트래픽을 줄이고 덜 번잡 한 사용자 인터페이스를 매끄럽게 제공 하는 단일 HTTP POST 요청으로 여러 작업을 결합 합니다. ASP.NET Web API는 이제 일괄 처리 요청에 대 한 몇 가지 전략을 지원합니다.

- OData 서비스의 $batch 끝점을 사용 합니다.
- 단일 MIME 다중 파트 요청으로 여러 요청을 패키지 합니다.
- 사용자 지정 일괄 처리 형식을 사용 합니다.

일괄 처리 요청을 사용 하도록 설정 하려면 Web API 구성에 일괄 처리 처리기를 사용 하 여 경로 추가 하면:

[!code-csharp[Main](release-notes/samples/sample4.cs)]

제어할 수도 있습니다 있는지 여부를 요청 하거나 원하는 순서 대로 순차적으로 실행 합니다.

### <a name="portable-aspnet-web-api-client"></a>이식 가능한 ASP.NET 웹 API 클라이언트

이제 Windows 스토어 및 Windows Phone 8 응용 프로그램에 걸쳐 작동 하는 이식 가능한 클래스 라이브러리를 만드는 ASP.NET 웹 API 클라이언트를 사용할 수 있습니다. 또한 클라이언트와 서버 간에 공유할 수 있는 이식 가능한 포맷터를 만들 수 있습니다.

### <a name="improved-testability"></a>테스트 용이성 향상된

웹 API 2 사용 하면 쉽게 단위 테스트에 API 컨트롤러입니다. 방금 구성을 확인 하 고 요청 메시지를 사용 하 여 API 컨트롤러 인스턴스화하고 테스트 하려는 작업 메서드를 호출 합니다. 모의 쉽게 이기도 합니다 **UrlHelper** 링크 생성을 수행 하는 작업 메서드에 대 한 클래스입니다.

### <a name="ihttpactionresult"></a>IHttpActionResult

이제 Web API 작업 메서드의 결과 캡슐화 하는 IHttpActionResult를 구현할 수 있습니다. 웹 API 동작 메서드에서 반환 되는 IHttpActionResult 결과 응답 메시지를 생성 하기 위해 ASP.NET Web API 런타임에서 실행 됩니다. 단위를 간소화 하는 Web API 작업에서 반환할 수는 IHttpActionResult Web API 구현의 테스트 합니다. IHttpActionResult 구현의 숫자로 특정 상태 코드를 반환 하는 것에 대 한 결과 포함 하 여 기본적으로 제공 되는 편의 위해 콘텐츠 또는 콘텐츠 협상 응답을 포맷 합니다.

### <a name="httprequestcontext"></a>HttpRequestContext

새 **HttpRequestContext** 요청에 연결 되어 있지만 요청에서 즉시 사용할 수 없는 모든 상태를 추적 합니다. 예를 들어 사용할 수 있습니다 합니다 **HttpRequestContext** 경로 데이터를 클라이언트 인증서를 요청과 연결 된 보안 주체는 **UrlHelper** 및 가상 경로 루트입니다. 쉽게 만들 수 있습니다는 **HttpRequestContext** 단위에 대 한 테스트 목적으로 합니다.

요청에 대 한 보안 주체에 의존 하지 않고 요청을 사용 하 여 흐름용으로 때문 **Thread.CurrentPrincipal**, Web API 파이프라인에 있는 경우 주 서버 요청의 수명 동안 제공 됩니다.

### <a name="cors"></a>CORS

Brock Allen에서 또 다른 훌륭한 기여를 통해 ASP.NET 완벽 하 게 지원 요청 공유 CORS (Cross Origin).

브라우저의 보안 기능은 웹 페이지에서 다른 도메인으로 AJAX 요청을 전송하는 것을 막습니다. [CORS](http://www.w3.org/TR/cors/) 동일 원본 정책을 완화 하는 서버를 허용 하는 W3C 표준입니다. CORS를 사용하면 서버가 명시적으로 특정 교차 원본 요청만 허용하고, 다른 요청은 거부할 수 있습니다.

Web API 2에는 이제 자동 실행 전 요청 처리를 포함 하 여 CORS를 지원 합니다. 자세한 내용은 [ASP.NET Web API에서 크로스-원본 요청 사용](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md)합니다.

### <a name="authentication-filters"></a>인증 필터

인증 필터는 ASP.NET Web API 파이프라인의 권한 부여 필터 전에 실행 하 고 인증 논리 작업을 지정할 수 있는 ASP.NET Web API에서 필터의 새 종류 컨트롤러 별로 또는 모든 컨트롤러에 대 한 전역적으로 합니다. 인증 필터는 요청에 자격 증명을 처리 하 고 해당 보안 주체를 제공 합니다. 인증 필터 권한이 없는 요청에 대 한 응답에서 인증 질문을 추가할 수도 있습니다.

### <a name="filter-overrides"></a>필터 재정

재정의 필터를 지정 하 여 지정 된 동작 메서드 또는 컨트롤러에 적용 하는 필터가 재정의할 수 있습니다. 재정의 필터에 지정된 된 범위 (작업 또는 컨트롤러)에 대 한 실행 하지 않아야 하는 필터 형식 집합을 지정 합니다. 이 옵션을 사용 하면 전역 필터를 추가 하지만 일부는 특정 작업 또는 컨트롤러에서를 제외할 수 있습니다.

### <a name="owin-integration"></a>OWIN 통합

ASP.NET Web API 이제 완벽 하 게 지원 OWIN 하며 OWIN 수 있는 호스트에서 실행할 수 있습니다. 또한 포함 됩니다는 **HostAuthenticationFilter** OWIN 인증 시스템과 통합을 제공 합니다.

OWIN 통합을 사용 하 여 SignalR 같은 다른 OWIN 미들웨어와 함께 고유한 프로세스에서 Web API를 자체 호스트할 수 있습니다. 자세한 내용은 [여 ASP.NET Web API를 사용 하 여 OWIN](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)합니다.

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a>ASP.NET SignalR 2.0

다음 섹션에서는 SignalR 2.0의 기능을 설명 합니다.

- [OWIN 기반](#builtonowin)
- [MapHubs 및 MapConnection MapSignalR 됩니다.](#MapSignalR)
- [도메인 간 지원](#crossdomain)
- [iOS 및 Android MonoTouch 및 MonoDroid를 통해 지원](#mobile)
- [이식 가능한.NET 클라이언트](#portable)
- [자체 호스트 하는 새 패키지](#selfhost)
- [이전 버전과 호환 서버 지원](#backwardcompat)
- [.NET 4.0 용 서버 지원 제거](#remove40)
- [클라이언트 및 그룹 목록을 메시지 보내기](#messagelist)
- [특정 사용자에 게 메시지 보내기](#sendtouser)
- [더 나은 오류 처리 지원](#errorhandling)
- [쉽게 단위 테스트 허브](#unittesting)
- [JavaScript 오류 처리](#javascripterror)

SignalR 2.0으로 기존 1.x 프로젝트를 업그레이드 하는 방법의 예제를 참조 하세요 [업그레이드는 SignalR 1.x 프로젝트](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md)합니다.

<a id="builtonowin"></a>
### <a name="built-on-owin"></a>OWIN 기반

SignalR 2.0에서 완전히 빌드됩니다 [OWIN (.NET에 대 한 Open Web Interface)](http://owin.org/)합니다. 이 변경 웹 호스팅 및 자체 호스팅 SignalR 응용 프로그램을 훨씬 더 일관 된 SignalR에 대 한 설치 프로세스를 통해 하지만 다양 한 API 변경 내용 때도 필요 합니다.

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a>MapHubs 및 MapConnection MapSignalR 됩니다.

OWIN 표준 호환성을 위해 이러한 방법으로 바뀌었습니다 `MapSignalR`합니다. `MapSignalR` 매개 변수는 모든 허브 매핑될 하지 않고 호출 (으로 `MapHubs` 버전에서 1.x); 개별 매핑할 **PersistentConnection** 개체, 형식 매개 변수를 및로 연결에 대해 URL 확장이 연결 유형을 지정 합니다 첫 번째 인수입니다.

`MapSignalR` Owin 시작 클래스에서 호출 됩니다. Visual Studio 2013에는 Owin 시작 클래스에 대 한 새 템플릿을 포함 이 템플릿을 사용 하려면 다음을 수행 합니다.

1. 프로젝트를 마우스 오른쪽 단추로 클릭
2. 선택 **추가할**, **새 항목...**
3. 선택 **Owin Startup 클래스**합니다. 새 클래스 이름을 **Startup.cs**합니다.

에 **웹 응용 프로그램** 포함 하는 Owin 시작 클래스는 `MapSignalR` 메서드가 아래와 같이 다음 항목을 사용 하 여 Web.Config 파일의 응용 프로그램 설정 노드에서 Owin의 시작 프로세스에 추가 됩니다.

에 **응용 프로그램을 자체 호스팅**, Startup 클래스의 형식 매개 변수로 전달 되는 `WebApp.Start` 메서드.

**Hubs 및 SignalR에 대 한 연결 매핑 1.x (웹 응용 프로그램에서 전역 응용 프로그램 파일)에서:** 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

**허브 및 연결 (Owin Startup 클래스 파일)에서 SignalR 2.0에 매핑:** 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

에 **자체 호스트 된 응용 프로그램**, Startup 클래스에 대 한 형식 매개 변수로 전달 되는 `WebApp.Start` 메서드를 아래와 같이 합니다.

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a>도메인 간 지원

SignalR 1.x에서 도메인 간 요청 된 단일 EnableCrossDomain 플래그로 제어. 이 플래그는 JSONP 및 CORS 요청을 제어 합니다. 모든 CORS 지원 유연성을 높이기 위해 SignalR의 서버 구성 요소에서 제거 되었습니다 (JavaScript lients 여전히 CORS 일반적으로 사용 하는 브라우저에서 지 원하는 검색 되었을 때), 새 OWIN 미들웨어입니다. 이러한 시나리오를 지원 하기 위해 사용할 수 있게 되었습니다.

SignalR 2.0의 경우 JSONP는 클라이언트에서 (지 원하는 데 필요한 도메인 간 요청 이전 브라우저에서)를 설정 하 여 명시적으로 설정 해야 `EnableJSONP` 에 `HubConfiguration` 개체를 `true`다음과 같이 합니다. JSONP는 CORS 보다 안전 하지 않은 것 처럼 기본적으로 비활성화 됩니다.

SignalR 2.0에서 새 CORS 미들웨어를 추가 하려면 추가 합니다 `Microsoft.Owin.Cors` 라이브러리 프로젝트 및 호출 `UseCors` 아래 섹션에 나와 있는 것 처럼 SignalR 미들웨어 전에 합니다.

**Microsoft.Owin.Cors 프로젝트가 추가**:이 라이브러리를 설치 하려면 패키지 관리자 콘솔에서 다음 명령을 실행 합니다.

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

이 명령은 2.0.0 추가 패키지를 프로젝트의 버전입니다.

**UseCors를 호출합니다.**

다음 코드 조각에는 SignalR에서 도메인 간 연결을 구현 하는 방법을 보여 줍니다 1.x 및 2.0.

**SignalR에서 도메인 간 요청을 구현 (전역 응용 프로그램 파일)에서 1.x**

[!code-csharp[Main](release-notes/samples/sample9.cs)]

**도메인 간 요청 (C# 코드 파일)에서 SignalR 2.0 구현**

다음 코드는 SignalR 2.0 프로젝트에 JSONP 또는 CORS를 사용 하도록 설정 하는 방법에 설명 합니다. 이 코드 샘플에서는 `Map` 하 고 `RunSignalR` of `MapSignalR`CORS 미들웨어 CORS 지원 해야 하는 SignalR 요청에 대해서만 실행 되도록 (아니라에 지정 된 경로에서 모든 트래픽을 `MapSignalR`.) `Map` 특정 URL 접두사를 아니라 전체 응용 프로그램을 실행 해야 하는 다른 모든 미들웨어를 사용할 수도 있습니다.

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a>iOS 및 Android MonoTouch 및 MonoDroid를 통해 지원

IOS 및 Android 클라이언트에서 MonoTouch 및 MonoDroid 구성 요소를 사용 하 여에 대 한 지원이 추가 되었습니다 합니다 [Xamarin 라이브러리](https://xamarin.com/)합니다. 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [Xamarin 구성 요소를 사용 하 여](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln)입니다. 이러한 구성 요소에서 사용할 수 있습니다 합니다 [Xamarin 스토어](https://store.xamarin.com/) SignalR RTW 릴리스를 사용할 수 있습니다.

<a id="portable"></a> # # # 이식 가능한.NET 클라이언트

더 잘 Silverlight에서 WinRT 플랫폼 간 개발을 용이 하 게 하 고 다음 플랫폼을 지 원하는 단일 이식 가능한.NET 클라이언트를 사용 하 여 Windows Phone 클라이언트 대체 되었습니다.

- NET 4.5
- Silverlight 5
- WinRT (Windows 스토어 앱 용.NET)
- Windows Phone 8

<a id="selfhost"></a>

### <a name="new-self-host-package"></a>자체 호스트 하는 새 패키지

쉽게 SignalR 자체 호스팅 프로세스에서 호스트 되는 SignalR 응용 프로그램 또는 다른 응용 프로그램 대신 웹 서버에서 호스트 되는 것을 시작 하는 NuGet 패키지가 됩니다. SignalR을 사용 하 여 빌드한 자체 호스트 프로젝트를 업그레이드 하려면 1.x Microsoft.AspNet.SignalR.Owin 패키지를 제거 하 고 Microsoft.AspNet.SignalR.SelfHost 패키지를 추가 합니다. 시작를 자체 호스팅하는 패키지에 대 한 자세한 내용은 참조 하세요. [자습서: SignalR 자체 호스팅](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)합니다.

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a>이전 버전과 호환 서버 지원

이전 버전의 SignalR에 동일 하 게 필요한 서버 및 클라이언트에 사용 되는 SignalR 패키지의 버전입니다. 업데이트 하기가 굵은 클라이언트 응용 프로그램을 지원 하기 위해 SignalR 2.0 이전 클라이언트를 사용 하 여 최신 서버 버전을 사용 하 여 이제 지원 합니다. **참고: SignalR 2.0 최신 클라이언트를 사용 하 여 이전 버전을 사용 하 여 빌드된 서버를 지원 하지 않습니다.**

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a>.NET 4.0 용 서버 지원 제거

SignalR 2.0에는.NET 4.0을 사용 하 여 server 상호 운용성에 대 한 지원을 삭제 했습니다. .NET 4.5 SignalR 2.0 서버를 사용 하 여 사용 해야 합니다. SignalR 2.0에 대 한.NET 4.0 클라이언트 계속 됩니다.

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a>클라이언트 및 그룹 목록을 메시지 보내기

SignalR 2.0에서는 클라이언트 및 그룹 Id 목록을 사용 하 여 메시지를 보낼 가능성이 있습니다. 다음 코드 조각에는이 작업을 수행 하는 방법을 보여 줍니다.

**클라이언트 및 PersistentConnection를 사용 하 여 그룹의 목록을 메시지 보내기**

[!code-csharp[Main](release-notes/samples/sample11.cs)]

**클라이언트 및 허브를 사용 하 여 그룹의 목록을 메시지 보내기**

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a>특정 사용자에 게 메시지 보내기

이 기능을 사용 하면 사용자가 사용자 Id 란 지정할 수는 IRequest IUserIdProvider 새 인터페이스를 통해 기준:

**IUserIdProvider 인터페이스**

[!code-csharp[Main](release-notes/samples/sample13.cs)]

기본적으로 사용자 이름으로 사용자의 IPrincipal.Identity.Name를 사용 하는 구현은 수 됩니다.

허브에서 새 API 통해 이러한 사용자에 게 메시지를 보낼 수 있습니다.

**Clients.User API를 사용 하 여**

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a>더 나은 오류 처리 지원

사용자가 이제 throw 할 수 있습니다 **HubException** 모든 허브 호출에서. 생성자는 **HubException** 문자열 메시지와 개체 들 추가 오류 데이터입니다. SignalR 예외를 자동으로 serialize 하 고 거부/실패 허브 메서드 호출에 사용할 수는 클라이언트 전송 됩니다.

합니다 **자세한 허브 예외 표시** 설정을 관련이 없습니다 **HubException** 여부; 클라이언트로 다시 전송 되 고 항상 전송 됩니다.

**클라이언트는 HubException 보내기 설명 하는 서버 쪽 코드**

[!code-csharp[Main](release-notes/samples/sample15.cs)]

**서버에서 전송 하는 HubException에 응답을 보여 주는 JavaScript 클라이언트 코드**

[!code-html[Main](release-notes/samples/sample16.html)]

**서버에서 전송 하는 HubException에 응답을 보여 주는.NET 클라이언트 코드**

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a>쉽게 단위 테스트 허브

라는 인터페이스를 포함 하는 SignalR 2.0 `IHubCallerConnectionContext` 쉽게 모의 클라이언트 쪽 호출을 만들 수 있도록 하는 허브에서. 다음 코드 조각은이 인터페이스를 사용 하 여 인기 있는 테스트 도구를 사용 하 여 보여 줍니다 [xUnit.net](https://github.com/xunit/xunit) 하 고 [moq](https://code.google.com/p/moq/)합니다.

**SignalR을 사용한 단위 테스트 xUnit.net**

[!code-csharp[Main](release-notes/samples/sample18.cs)]

**Moq를 사용 하 여 SignalR을 테스트 하는 단위**

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a>JavaScript 오류 처리

모든 JavaScript 오류 처리 콜백을 SignalR 2.0에서는 원시 문자열 대신 JavaScript 오류 개체를 반환합니다. 이 SignalR을 오류 처리기를 더 많은 정보를 전달할 수 있습니다. 내부 예외를 가져올 수 있습니다는 `source` 오류의 속성입니다.

**Start.Fail 예외를 처리 하는 JavaScript 클라이언트 코드**

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a>ASP.NET ID

### <a name="new-aspnet-membership-system"></a>새 ASP.NET 멤버 자격 시스템

ASP.NET Id는 ASP.NET 응용 프로그램에 대 한 새 멤버 자격 시스템입니다. ASP.NET Id를 사용 하면 쉽게 응용 프로그램 데이터를 사용 하 여 사용자 고유의 프로필 데이터를 통합할 수 있습니다. ASP.NET Id를 사용 하면 응용 프로그램에서 사용자 프로필에 대 한 지 속성 모델을 선택할 수 있습니다. SQL Server 데이터베이스 또는 Azure Storage Tables와 같은 NoSQL 데이터 저장소를 포함 하는 다른 데이터 저장소에 데이터를 저장할 수 있습니다. 자세한 내용은 [개별 사용자 계정](creating-web-projects-in-visual-studio.md#indauth) 에 **Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기**합니다.

### <a name="claims-based-authentication"></a>클레임 기반 인증

이제 ASP.NET 사용자의 id를 신뢰할 수 있는 발급자의 클레임 집합으로 표시 됩니다는 클레임 기반 인증을 지원 합니다. 인증 된 사용자 이름 및 응용 프로그램 데이터베이스에서 유지 관리 하는 암호를 사용 하 여 또는 소셜 id 공급자를 사용 하 여 사용자가 될 수 있습니다 (예: Microsoft 계정, Facebook, Google, Twitter)를 Azure Active Directory를 통해 조직 계정을 사용 하 여 또는 또는 Active Directory Federation Services (ADFS)입니다.

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a>Azure Active Directory 및 Windows Server Active Directory와 통합

이제 인증을 위해 Azure Active Directory 또는 Windows Server Active Directory (AD)를 사용 하는 ASP.NET 프로젝트를 만들 수 있습니다. 자세한 내용은 [조직 계정](creating-web-projects-in-visual-studio.md#orgauth) 에 **Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기**합니다.

### <a name="owin-integration"></a>OWIN 통합

ASP.NET 인증은 이제 OWIN 미들웨어는 OWIN 기반 호스트에 사용할 수 있는 기반으로 합니다. OWIN에 대 한 자세한 내용은 다음을 참조 하세요 [Microsoft OWIN 구성 요소](#TOC7) 섹션입니다.

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a>Microsoft OWIN 구성 요소

[Open Web Interface for.NET](http://owin.org/) (OWIN).NET 웹 서버 및 웹 응용 프로그램 간의 추상화를 정의 합니다. OWIN 웹 응용 프로그램 호스트 중립적 만드는 서버에서 웹 응용 프로그램을 분리 합니다. 예를 들어 IIS에서 OWIN 기반 웹 응용 프로그램을 호스팅할 수도 있고 사용자 지정 프로세스에서 자체 호스트할 수 있습니다.

Microsoft OWIN 구성 요소 (Katana 프로젝트 라고도 함)에 도입 된 변경 내용을 새 서버와 호스트 구성 요소, 새로운 도우미 라이브러리 및 미들웨어 및 새 인증 미들웨어를 포함 합니다.

OWIN 및 Katana에 대 한 자세한 내용은 참조 하세요. [OWIN 및 Katana의 새로운 기능](../../../aspnet/overview/owin-and-katana/index.md)합니다.

**참고: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) 응용 프로그램 IIS 클래식 모드에서 실행할 수 없습니다; 통합 모드로 실행 해야 합니다.**

**참고: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) 완전 신뢰에서 응용 프로그램을 실행 해야 합니다.**

### <a name="new-servers-and-hosts"></a>새 서버 및 호스트

이 릴리스를 사용 하 여 새 구성 요소는 자체 호스트 시나리오를 사용 하도록 설정 하려면 추가 되었습니다. 이러한 구성 요소에는 다음 NuGet 패키지를 포함 합니다.

- **Microsoft.Owin.Host.HttpListener**. 사용 하는 OWIN 서버를 제공 **HttpListener** HTTP 요청을 수신 하 여 OWIN 파이프라인에 도달 하도록 지시 합니다.
- **Microsoft.Owin.Hosting** 자체 콘솔 응용 프로그램 또는 Windows 서비스와 같은 사용자 지정 프로세스에서 OWIN 파이프라인을 호스트 하려는 개발자를 위한 라이브러리를 제공 합니다.
- **OwinHost**합니다. 래핑하는 독립 실행형 실행 파일을 제공 `Microsoft.Owin.Hosting` 자체 사용자 지정 호스트 응용 프로그램을 작성 하지 않고도 OWIN 파이프라인을 호스트할 수 있습니다.

또한 합니다 `Microsoft.Owin.Host.SystemWeb` 패키지는 이제 힌트를 제공 하는 미들웨어를 사용 하면를 **SystemWeb** 특정 ASP.NET 파이프라인 단계에서 미들웨어를 호출 해야 함을 나타내는 서버. 이 기능은 인증 미들웨어를 ASP.NET 파이프라인 초기에 실행 해야 하는 데 특히 유용 합니다.

### <a name="helper-libraries-and-middleware"></a>도우미 라이브러리 및 미들웨어

OWIN 사양에서 함수 및 형식 정의 사용 하 여 OWIN 구성 요소를 작성할 수 있지만 새 `Microsoft.Owin` 패키지는 보다 친숙 한 추상화 집합을 제공 합니다. 몇 가지 이전 패키지를 결합 하는이 패키지 (예를 들어 `Owin.Extensions`, `Owin.Types`) 다른 OWIN 구성 요소에서 쉽게 사용할 수 있는 잘 구성 된 단일 개체 모델로 합니다. 사실 대부분의 Microsoft OWIN 구성 요소는 이제이 패키지를 사용 합니다.

> [!NOTE]
> [OWIN](http://www.owin.org) 응용 프로그램 IIS 클래식 모드에서 실행할 수 없습니다; 통합 모드로 실행 해야 합니다.

> [!NOTE]
> [OWIN](http://www.owin.org) 완전 신뢰에서 응용 프로그램을 실행 해야 합니다.

이 이번에는 실행 중인 OWIN 응용 프로그램의 유효성을 검사 하는 미들웨어와 오류를 조사 하는 데 오류 페이지 미들웨어를 포함 하는 Microsoft.Owin.Diagnostics 패키지도를 포함 됩니다.

### <a name="authentication-components"></a>인증 구성 요소

다음 인증 구성 요소가 사용할 수 있습니다.

- **Microsoft.Owin.Security.ActiveDirectory**. 온-프레미스 또는 클라우드 기반 디렉터리 서비스를 사용 하 여 인증을 사용 하도록 설정 합니다.
- **Microsoft.Owin.Security.Cookies** 쿠키를 사용 하 여 수 있도록 인증 합니다. 이 패키지 변수의 이름이 이전에 `Microsoft.Owin.Security.Forms`입니다.
- **Microsoft.Owin.Security.Facebook** Facebook의 OAuth 기반 서비스를 사용 하 여 수 있도록 인증 합니다.
- **Microsoft.Owin.Security.Google** Google의 OpenID 기반 서비스를 사용 하 여 수 있도록 인증 합니다.
- **Microsoft.Owin.Security.Jwt** JWT 토큰을 사용 하 여 수 있도록 인증 합니다.
- **Microsoft.Owin.Security.MicrosoftAccount** Microsoft 계정을 사용 하면 인증 합니다.
- **Microsoft.Owin.Security.OAuth**. 전달자 토큰을 인증 하기 위한 미들웨어 뿐만 아니라 OAuth 권한 부여 서버를 제공 합니다.
- **Microsoft.Owin.Security.Twitter** Twitter의 OAuth 기반 서비스를 사용 하 여 수 있도록 인증 합니다.

또한이 릴리스는 `Microsoft.Owin.Cors` 크로스-원본 HTTP 요청을 처리 하는 것에 대 한 미들웨어를 포함 하는 패키지입니다.

> [!NOTE]
> Visual Studio 2013의 최종 버전에서는 JWT를 서명 하는 것에 대 한 지원이 제거 되었습니다.

<a id="ef6"></a>
## <a name="entity-framework-6"></a>Entity Framework 6

새로운 기능 및 Entity Framework 6의 다른 부분이 변경의 목록을 참조 하세요 [Entity Framework 버전 기록이](https://msdn.com/data/jj574253)합니다.

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a>ASP.NET Razor 3

ASP.NET Razor 3에는 다음과 같은 새로운 기능이 포함 됩니다.

- 탭에서 편집할 수 있습니다. Preivously, 합니다 **문서 서식** 사용 하는 경우 명령, 자동 들여쓰기 및 자동 Visual Studio에서 서식이 제대로 작동 하지 않았습니다 합니다 **탭 유지** 옵션입니다. 이 변경은 서식 탭에 대 한 Razor 코드에 대 한 서식 지정 하는 Visual Studio를 수정 합니다.
- 링크를 생성 하는 경우 URL 다시 쓰기 규칙을 지원 합니다.
- 보안 투명 한 특성을 제거 합니다.
  > [!NOTE]
  > 이렇게는 주요 변경 내용, 고 Razor 3 호환 되지 않는 mvc 4 및 이전 버전에서는 동안 Razor 2 MVC5 또는 MVC5에 대해 컴파일된 어셈블리와 호환 되지 않습니다.

Visual Studio 2013 시험판 버전에서 수정 된 razor 3 문제를 찾을 수 있습니다 [여기](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0)합니다.

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a>ASP.NET 앱 일시 중단

ASP.NET 앱 일시 중단에는 사용자 환경 및 많은 수의 단일 컴퓨터에서 ASP.NET 사이트를 호스팅하기 위한 경제 모델 근본적으로 변경 하는.NET Framework 4.5.1에서에서 획기적인 기능입니다. 자세한 내용은 [.NET 웹 호스팅 ASP.NET 앱 일시 중단 – 응답 공유](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx)합니다.

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a>알려진된 문제 및 주요 변경 내용

이 섹션에서는 Visual Studio 2013 용 ASP.NET 및 Web Tools의 주요 변경 내용 및 알려진된 문제를 설명 합니다.

### <a name="nuget"></a>NuGet

- [SLN 파일을 사용 하는 경우 Mono에서 새 패키지 복원이 작동 하지 않습니다](https://nuget.codeplex.com/workitem/3596) –는 예정 된 nuget.exe 다운로드에서 수정 될 예정 및 [NuGet.CommandLine 패키지](http://www.nuget.org/packages/NuGet.CommandLine/) 업데이트 합니다.
- [Wix 프로젝트를 사용 하 여 새 패키지 복원이 작동 하지 않습니다](https://nuget.codeplex.com/workitem/3598) –는 예정 된 nuget.exe 다운로드에서 수정 될 예정 및 [NuGet.CommandLine 패키지](http://www.nuget.org/packages/NuGet.CommandLine/) 업데이트 합니다.
- [자동 패키지 복원 솔루션 폴더 아래의 프로젝트에 대 한 작동 하지 않습니다](https://nuget.codeplex.com/workitem/3625) – NuGet 2.8에서 수정 될 예정입니다.

### <a name="aspnet-web-api"></a>ASP.NET Web API

1. `ODataQueryOptions<T>.ApplyTo(IQueryable)` 반환 하지 않습니다 `IQueryable<T>` 에 대 한 지원을 추가 했습니다 하는 대로 항상 `$select` 고 `$expand`입니다.

    이전 샘플에 대 한 `ODataQueryOptions<T>` 반환 값에서 항상 캐스팅 `ApplyTo` 에 `IQueryable<T>`입니다. 이전에서는이 쿼리 옵션 때문에 이전 작업을 지원 하는지 (`$filter`, `$orderby`를 `$skip`, `$top`) 쿼리의 셰이프를 변경 하지 마십시오. 지원 했으므로 `$select` 하 고 `$expand` 의 반환 값 `ApplyTo` 됩니다 `IQueryable<T>` 항상 있습니다.

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    클라이언트에서 보내지 않으면 작업에서 이전 샘플 코드를 사용 하는 경우 계속 `$select` 고 `$expand`입니다. 그러나 지원 하려는 경우 `$select` 고 `$expand` 해당 코드를 변경 해야 합니다.

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. **일괄 처리 요청을 하는 동안 Request.Url 나 RequestContext.Url null 임**

    일괄 처리 시나리오에서는 **UrlHelper** 에서 액세스할 때 null **Request.Url** 하거나 **RequestContext.Url**합니다.

    이 문제는 현재 다음 추적: [BatchRequestContext.Url가 요청을 일괄 처리에 대해 null](http://aspnetwebstack.codeplex.com/workitem/1301)합니다.

    이 문제에 대 한 해결 방법은의 새 인스턴스를 만드는 것 **UrlHelper**다음 예제와 같이:

    **UrlHelper의 새 인스턴스 만들기**

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a>ASP.NET MVC

1. AntiForgerToken 유효성 검사를 수행 하는 보기가 있는 경우 MVC5 및 OrgAuth를 사용 하는 경우 나올 수 오류로 보기에 데이터를 게시 하는 경우:

    **오류**:

    *'/' 응용 프로그램에 서버 오류가 발생 했습니다.*

    <em>형식의 클레임은 '<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>'또는'<http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>'에 제공 된 ClaimsIdentity 제공 되지 않았습니다. 클레임 기반 인증을 사용 하 여 위조 방지 토큰 지원을 사용 하는 구성 된 클레임 공급자 제공 하는 이러한 클레임 생성 ClaimsIdentity 인스턴스 둘 다 확인 하세요. 구성 된 클레임 공급자 대신 다른 클레임 유형에 사용 하 여 고유 식별자로, AntiForgeryConfig.UniqueClaimTypeIdentifier 정적 속성을 설정 하 여 구성할 수 있습니다.</em>

    **해결 방법**:

    해결 하는 Global.asax의 다음 줄을 추가 합니다.

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    이 다음 릴리스에서 해결 될 예정입니다.
2. MVC4 앱 MVC5로 업그레이드 한 후 솔루션을 빌드하고 시작 합니다. 다음 오류가 표시 됩니다.

    [A] System.Web.WebPages.Razor.Configuration.HostSection [B]System.Web.WebPages.Razor.Configuration.HostSection 캐스팅할 수 없습니다. 시작 되는 형식 ' System.Web.WebPages.Razor, 버전 2.0.0.0, Culture = neutral, PublicKeyToken = 31bf3856ad364e35 =' 위치의 ' 기본값' 컨텍스트에 있는 ' C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\ v4.0\_2.0.0.0\_\_31bf3856ad364e35\System.Web.WebPages.Razor.dll'. 형식 B에서 시작 ' System.Web.WebPages.Razor, Version 3.0.0.0, Culture = neutral, PublicKeyToken = 31bf3856ad364e35 =' 위치의 ' 기본값' 컨텍스트에 있는 ' C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\ e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01\System.Web.WebPages.Razor.dll'.

    위의 오류를 해결 하려면 엽니다 *모든* 프로젝트에 다음을 수행 Web.config 파일 (Views 폴더의 항목 포함):

   1. "5.0.0.0"를 "System.Web.Mvc"의 "4.0.0.0" 버전의 모든 항목을 업데이트 합니다.
   2. "System.Web.Helpers"의 "2.0.0.0" 버전의 모든 항목을 업데이트 &quot;System.Web.WebPages&quot; 하 고 &quot;System.Web.WebPages.Razor&quot; "3.0.0.0"를

      예를 들어, 위의 변경 하면 어셈블리 바인딩을 다음과 같이 표시 됩니다.

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      MVC 4 프로젝트에서 MVC 5 업그레이드에 대 한 자세한 내용은 [ASP.NET MVC 5 및 Web API 2에는 ASP.NET MVC 4 및 Web API 프로젝트를 업그레이드 하는 방법](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)합니다.
3. JQuery 비간섭 유효성 검사를 사용 하 여 클라이언트 쪽 유효성 검사를 사용 하는 경우 유효성 검사 메시지를 올바르지 않을 경우에 따라 형식 사용 하 여 HTML input 요소에 대 한 = 'number'. 유효성 검사 오류에 대해 필요한 값 ("The Age 필드는 필수")가 표시 유효한 숫자가 필요 하다는 올바른 메시지 대신 잘못 된 숫자를 입력 하는 경우.

    이 문제는 만들기 및 편집 보기에는 정수 속성을 사용 하 여 모델에 대 한 스 캐 폴드 된 코드를 사용 하 여 흔히 발견 됩니다.

    이 문제를 해결 하려면 편집기 도우미를 변경 합니다.

    `@Html.EditorFor(person => person.Age)`

    대상:

    `@Html.TextBoxFor(person => person.Age)`
4. ASP.NET MVC 5 부분 신뢰를 더 이상 지원합니다. MVC 또는 WebAPI 바이너리에 연결 하는 프로젝트를 제거 해야 합니다 [SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) 특성 및 [AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) 특성입니다. 이러한 특성을 제거 하면 다음과 같은 컴파일러 오류가 제거 됩니다.

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > 참고로이의 부작용으로 사용할 수 없습니다 4.0 및 5.0 어셈블리 동일한 응용 프로그램. 5.0에이 모두 업데이트 해야 합니다.

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a>웹 사이트는 인트라넷 영역에서 호스트 되는 동안 Facebook 인증을 사용 하 여 SPA 템플릿 IE에서 불안정 해질 수 있습니다.

SPA 템플릿 외부 Facebook 로그인을 제공합니다. 템플릿을 사용 하 여 만든 프로젝트를 로컬로 실행 하는 경우 로그인 IE 크래시가 발생할 수 있습니다.

해결책:

1. 인터넷 영역의; 웹 사이트 호스트 또는

2. IE 이외의 브라우저에서 시나리오를 테스트 합니다.

### <a name="web-forms-scaffolding"></a>Web Forms 스 캐 폴딩

Web Forms 스 캐 폴딩 VS2013에서 제거 되 고 Visual Studio의 이후 업데이트에서 사용할 수 있습니다. 그러나 Web Forms 프로젝트에서 스 캐 폴딩 MVC 종속성 추가 하 고 mvc 스 캐 폴딩 생성 하 여 계속 사용할 수 있습니다. 프로젝트가는 Web Forms 및 MVC의 조합이 포함 됩니다.

MVC Web Forms 프로젝트에 추가할 새 스 캐 폴드 된 항목을 추가 하 고 선택 **MVC 5 종속성**합니다. 최소 또는 전체 스크립트와 같은 콘텐츠 파일을 모두 해야 하는지 여부에 따라 선택 합니다. 프로젝트에 뷰 및 컨트롤러를 만드는 mvc 스 캐 폴드 된 항목을 추가 합니다.

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC 및 Web API 스 캐 폴딩-HTTP 404 찾을 수 없음 오류

프로젝트에 스 캐 폴드 된 항목을 추가할 때 오류가 발견 되 면 가능 프로젝트 일관성 없는 상태로 남게 됩니다. 변경 내용 스 캐 폴딩 수 중 일부를 롤백할 수 있지만 설치 된 NuGet 패키지와 같은 다른 변경 내용을 다시 롤백할 수 됩니다. 라우팅 구성 변경 내용이 롤백되어도 경우 스 캐 폴드 항목으로 이동 하는 경우 사용자는 HTTP 404 오류를 받게 됩니다.

해결 방법:

- MVC에 대 한이 오류를 해결 하려면 새 스 캐 폴드 된 항목을 추가 하 고 MVC 5 종속성 선택 (최소 또는 전체). 이 프로세스에서 필요한 변경의 모든 프로젝트에 추가 합니다.
- 웹 API에 대 한이 오류를 수정 합니다.

  1. 프로젝트에 클래스를 추가 합니다.

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. 응용 프로그램에서 WebApiConfig.Register 구성\_Global.asax에서 다음과 같은 메서드를 시작 합니다.

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]
