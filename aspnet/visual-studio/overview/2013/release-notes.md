---
uid: visual-studio/overview/2013/release-notes
title: ASP.NET 및 Web Tools for Visual Studio 2013 릴리스 정보 | Microsoft Docs
author: microsoft
description: 이 문서에서는 Visual Studio 2013 용 ASP.NET 및 웹 도구 릴리스를 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/17/2013
ms.topic: article
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: e9ddd96f186564834ff6bb2c30cf0ed5444cbf1b
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a>ASP.NET 및 Web Tools for Visual Studio 2013 릴리스 정보
====================
by [Microsoft](https://github.com/microsoft)

> 이 문서에서는 Visual Studio 2013 용 ASP.NET 및 웹 도구 릴리스를 설명 합니다.


## <a name="contents"></a>목차

- [설치 참고 사항](#TOC1)
- [문서](#TOC2)
- [소프트웨어 요구 사항](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>ASP.NET 및 Web Tools for Visual Studio 2013의 새로운 기능

- [One ASP.NET](#TOC6)
- [새 웹 프로젝트 경험](#newproj)
- [ASP.NET 스 캐 폴딩](#scaffold)
- [브라우저 링크](#browser-link)
- [Visual Studio 웹 편집기의 향상 된 기능](#web-editor)
- [Visual Studio에서 azure 앱 서비스 웹 앱 지원](#waws)
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

ASP.NET 및 Web Tools for Visual Studio 2013 주요 설치 관리자에 제공 되어 있으며 다운로드할 수 있습니다 [여기](https://www.asp.net/downloads)합니다.

<a id="TOC2"></a>
## <a name="documentation"></a>설명서

사용할 수 있는 자습서 및 Visual Studio 2013 용 ASP.NET 및 Web Tools에 대 한 기타 정보는 [ASP.NET 웹 사이트](https://www.asp.net/)합니다.

<a id="TOC4"></a>
## <a name="software-requirements"></a>소프트웨어 요구 사항

ASP.NET 및 Web Tools는 Visual Studio 2013 필요 합니다.

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a>ASP.NET 및 Web Tools for Visual Studio 2013의 새로운 기능

다음 섹션에서는 릴리스에서 도입 된 기능을 설명 합니다.

<a id="TOC6"></a>
## <a name="one-aspnet"></a>One ASP.NET

Visual Studio 2013의 릴리스로 쉽게을 혼합 하 고 사용자가 원하는 일치 수 있도록 ASP.NET 기술을 사용 경험을 통합 하기 위한 단계를 이동 합니다. 예를 들어 수 MVC를 사용 하 여 프로젝트를 시작할와 쉽게 나중에 프로젝트를 Web Forms 페이지를 추가 또는 Web Api Web Forms 프로젝트에 스 캐 폴드 합니다. One ASP.NET 모두 쉽게을 ASP.NET에서 선호 하는 작업을 수행 하려면 개발자는 됩니다. 선택한 기술은에 관계 없이 하나의 ASP.NET의 신뢰할 수 있는 기본 프레임 워크에서 작성할 수 있도록 한다는 확신을 가질 수 있습니다.

<a id="newproj"></a>
## <a name="new-web-project-experience"></a>새 웹 프로젝트 경험

Visual Studio 2013에서 새 웹 프로젝트를 만드는 환경과 향상 된 했습니다. 에 **새 ASP.NET 웹 프로젝트** 대화 원하는, 어떠한 조합의 기술 (Web Forms, MVC, Web API)를 구성 하 고, 인증 옵션을 구성 단위 테스트 프로젝트를 추가 프로젝트 유형을 선택할 수 있습니다.

![새 ASP.NET 프로젝트](release-notes/_static/image1.png)

새 대화 상자를 사용 하는 템플릿 중 대부분에 대 한 기본 인증 옵션을 변경할 수 있습니다. 예를 들어, ASP.NET Web Forms 프로젝트를 만들 때 다음 옵션 중 선택할 수 있습니다.

- 인증 안 함
- 개별 사용자 계정 (ASP.NET 멤버 자격 또는 소셜 공급자 로그에서)
- 조직 계정 (인터넷 응용 프로그램에 Active Directory)
- Windows 인증 (인트라넷 응용 프로그램에서 Active Directory)

![인증 옵션](release-notes/_static/image2.png)

웹 프로젝트를 만들기 위한 새 프로세스에 대 한 자세한 내용은 참조 [Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기](creating-web-projects-in-visual-studio.md)합니다. 새 인증 옵션에 대 한 자세한 내용은 참조 [ASP.NET Identity](#TOC8) 이 문서의 뒷부분에 나오는 합니다.

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a>ASP.NET 스 캐 폴딩

ASP.NET 스 캐 폴딩 ASP.NET 웹 응용 프로그램에 대 한 코드 생성 프레임 워크입니다. 쉽게 데이터 모델과 상호 작용 하는 프로젝트에 상용구 코드를 추가 합니다.

이전 버전의 Visual Studio를 스 캐 폴딩 ASP.NET MVC 프로젝트에 있었습니다. Visual Studio 2013, Web Forms를 포함 하 여 모든 ASP.NET 프로젝트에 대 한 스 캐 폴딩을 지금 사용할 수 있습니다. Visual Studio 2013 생성 페이지 Web Forms 프로젝트에 대 한 현재 지원 하지 않는 있지만 프로젝트에 MVC 종속성을 추가 하 여 스 캐 폴딩 Web Forms를 계속 사용할 수 있습니다. Web forms 페이지를 생성 하는 것에 대 한 지원이 향후 업데이트에서 추가 됩니다.

스 캐 폴딩을 사용할 때 필요한 모든 프로젝트에 종속성이 설치 되어을 확인 합니다. 예를 들어, ASP.NET Web Forms 프로젝트와 함께 시작 하 고 다음 스 캐 폴딩을 사용 하 여 웹 API 컨트롤러를 추가 하려면 필요한 NuGet 패키지와 참조를 프로젝트에 자동으로 추가 됩니다.

MVC 스 캐 폴딩 Web Forms 프로젝트를 추가 하려면 추가 **스 캐 폴드 된 새 항목** 선택 **MVC 5 종속성** 대화 상자 창에서. MVC; 스 캐 폴딩에 대 한 다음과 같은 최소이 고 전체. 최소을 선택 하면 NuGet 패키지와 ASP.NET MVC에 대 한 참조가 프로젝트에 추가 됩니다. 전체 옵션을 선택 하는 경우 MVC 프로젝트에 필요한 콘텐츠 파일 뿐만 아니라 최소한의 종속성 추가 됩니다.

비동기 컨트롤러를 스 캐 폴딩에 대 한 지원 Entity Framework 6의 새로운 비동기 기능을 사용 합니다.

자세한 내용과 자습서에 대 한 참조 [ASP.NET 스 캐 폴딩 개요](aspnet-scaffolding-overview.md)합니다.

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a>브라우저 링크-브라우저와 Visual Studio 간의 SignalR 채널

새 [브라우저 링크](using-browser-link.md) 를 통해 Visual Studio에 여러 브라우저를 연결 하 고 도구 모음에서 단추를 클릭 하 여 모든 고쳐지므로 새로 고칠 수 있습니다. 모바일 에뮬레이터를 비롯 하 여 개발 사이트에 여러 브라우저를 연결할 수 있고 동시에 모두 있는 모든 브라우저 새로 고침에 새로 고침을 클릭 합니다. 브라우저 링크는 또한 개발자 브라우저 링크 확장을 작성할 수 있도록 API를 노출 합니다.

![](release-notes/_static/image3.png)

브라우저 링크 API를 활용 하는 개발자를 활성화 하 여 Visual Studio와 연결 된 모든 브라우저 간의 경계를 교차 하는 고급 시나리오를 만들 수 수 있습니다. 웹 Essentials에서는 Visual Studio 및 브라우저의 개발자 도구, 모바일 에뮬레이터 및 더 많은 제어 원격 간에 통합된 된 환경을 만들려면 API 활용 합니다.

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a>Visual Studio 웹 편집기의 향상 된 기능

Visual Studio 2013 웹 응용 프로그램에서는 Razor 파일 및 HTML 파일에 대 한 새 HTML 편집기를 포함합니다. 새 HTML 편집기 HTML5에 따라 단일 통합된 스키마를 제공 합니다. 자동 중괄호 완성, jQuery UI 및 AngularJS 특성 IntelliSense, IntelliSense 그룹화, ID, Intellisense, 클래스 이름 및 기타 개선 기능 보다 나은 성능, 서식 지정을 포함 하 여 특성 및 스마트 태그입니다.

다음 스크린 샷에서 HTML 편집기에서 IntelliSense 부트스트랩 특성을 사용 하는 방법을 보여 줍니다.

![HTML 편집기의 Intellisense](release-notes/_static/image4.png)

Visual Studio 2013 모두 CoffeeScript 서 기본 제공 편집기에도 제공 됩니다. LESS 편집기에서는 CSS 편집기에서 훌륭한 기능이 함께 제공 되었으며 변수와 mixin에 대 한 특정 Intellisense의 덜 모든 문서 전체에서 @import 체인입니다.

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a>Visual Studio에서 azure 앱 서비스 웹 앱 지원

Azure SDK for.NET 2.2와 Visual Studio 2013에서 사용할 수 있습니다 **서버 탐색기** 원격 웹 앱과 직접 상호 작용할 수 있습니다. Azure 계정에 로그인 새 웹 응용 프로그램을 만들, 앱 구성 등 실시간 로그를 볼 수 있습니다. 기능은 이후 SDK 2.2 릴리스, Azure에서 원격으로 디버그 모드로 실행할 수 있습니다. Azure 앱 서비스 웹 앱에 대 한 새로운 기능 대부분.NET 용 Azure SDK의 현재 버전을 설치 하면 Visual Studio 2012에서 에서도 작동 합니다.

자세한 내용은 다음 리소스를 참조하세요.

- [Azure 앱 서비스에서 ASP.NET 웹 앱 만들기](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [Visual Studio를 사용 하 여 Azure 앱 서비스의 웹 응용 프로그램 문제 해결](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a>향상 된 기능으로 웹 게시

Visual Studio 2013에는 새로운 기능과 향상 된 웹 게시 기능이 포함 됩니다. 그 중 일부는 다음과 같습니다.

- 쉽게 [Web.config 파일 암호화 자동화](https://go.microsoft.com/fwlink/?LinkId=325529)합니다. (이 링크 및 다음 두 지점 저녁에 10/17에까지 제공 되지 않을 수 있는 msdn 설명서를 합니다.)
- 쉽게 [응용 프로그램 오프 라인으로 배포 하는 동안 수행 자동화](https://go.microsoft.com/fwlink/?LinkId=325530)합니다.
- 웹 배포를 구성 [파일 체크섬을 사용 하 여 마지막 변경 날짜 대신](https://go.microsoft.com/fwlink/?LinkId=325531) 서버에 있는 파일을 복사할 결정 합니다.
- 메서드를 게시 하는 파일 시스템 또는 FTP를 사용 하는 경우 뿐만 아니라 웹 배포와 개별 선택한 파일 (Web.config 포함)를 신속 하 게 게시 합니다.

ASP.NET 웹 배포에 대 한 자세한 내용은 참조 [ASP.NET 사이트](https://go.microsoft.com/fwlink/?LinkId=322027)합니다.

<a id="nuget"></a>
## <a name="nuget-27"></a>NuGet 2.7

NuGet 2.7에 자세히 설명 하는 새로운 기능의 풍부한 포함 [NuGet 2.7 릴리스 정보](http://docs.nuget.org/docs/release-notes/nuget-2.7)합니다.

또한이 버전의 NuGet 패키지를 다운로드 하려면 NuGet의 패키지 복원 기능에 대 한 명시적 동의 제공 하는 것을 제거 합니다. 동의 (및 연결 된 확인란 NuGet의 기본 설정 대화 상자) NuGet을 설치 하 여 부여 됩니다. 이제 패키지를 복원 하기만 하면 기본적으로 작동합니다.

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a>ASP.NET Web Forms

### <a name="one-aspnet"></a>One ASP.NET

Web Forms 프로젝트 템플릿 새 One ASP.NET 환경과 완벽 하 게 통합 합니다. MVC 및 Web API Web Forms 프로젝트를 지원 하 고 하나의 ASP.NET 프로젝트 만들기 마법사를 사용 하 여 인증을 구성할 수 있습니다를 추가할 수 있습니다. 자세한 내용은 참조 [Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기](creating-web-projects-in-visual-studio.md)합니다.

### <a name="aspnet-identity"></a>ASP.NET ID

Web Forms 프로젝트 템플릿은 새로운 ASP.NET Identity 프레임 워크를 지원합니다. 또한 서식 파일에는 이제 Web Forms 인트라넷 프로젝트를 만드는 지원합니다. 자세한 내용은 참조 [인증 방법을](creating-web-projects-in-visual-studio.md#auth) 에 **Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기**합니다.

### <a name="bootstrap"></a>부트스트랩

Web Forms 템플릿을 사용 하 여 [부트스트랩](http://twitter.github.io/bootstrap/) 는 매끄러운 및 응답성이 뛰어난 디자인을 쉽게 사용자 지정할 수 있도록 합니다. 자세한 내용은 참조 [Visual Studio 2013 웹 프로젝트 템플릿에서 부트스트랩](creating-web-projects-in-visual-studio.md#bootstrap)합니다.

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a>ASP.NET MVC 5

### <a name="one-aspnet"></a>One ASP.NET

웹 MVC 프로젝트 템플릿을 새 One ASP.NET 환경과 완벽 하 게 통합 합니다. MVC 프로젝트를 사용자 지정 하 고 하나의 ASP.NET 프로젝트 만들기 마법사를 사용 하 여 인증을 구성할 수 있습니다. ASP.NET MVC 5에 있는 소개 자습서에서 찾을 수 있습니다 [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md)합니다.

MVC 5로 MVC 4 프로젝트 업그레이드에 대 한 자세한 내용은 참조 하십시오. [ASP.NET MVC 4 및 Web API 프로젝트를 ASP.NET MVC 5 및 Web API 2로 업그레이드 하는 방법을](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)합니다.

### <a name="aspnet-identity"></a>ASP.NET ID

MVC 프로젝트 템플릿 인증 및 id 관리에 대 한 ASP.NET Id를 사용 하도록 업데이트 되었습니다. Facebook 및 Google 인증 및 새로운 구성원 API 자습서에서 찾을 수 있습니다 [Facebook, Google OAuth2 및 OpenID 로그온 ASP.NET MVC 5 응용 프로그램을 만들](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 및 [auth ASP.NET MVC 응용 프로그램 만들기 및 SQL DB Azure 앱 서비스를 배포 하 고](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)합니다.

### <a name="bootstrap"></a>부트스트랩

MVC 프로젝트 템플릿을 사용 하도록 업데이트 되었습니다 [부트스트랩](http://getbootstrap.com/) 는 매끄러운 및 응답성이 뛰어난 디자인을 쉽게 사용자 지정할 수 있도록 합니다. 자세한 내용은 참조 [Visual Studio 2013 웹 프로젝트 템플릿에서 부트스트랩](creating-web-projects-in-visual-studio.md#bootstrap)합니다.

### <a name="authentication-filters"></a>인증 필터

인증 필터는 새로운 종류의 필터를 실행 하는 ASP.NET MVC 파이프라인에서 권한 부여 필터 전에 인증 논리 당-작업을 지정할 수 있도록 ASP.NET MVC에서 컨트롤러 당 또는 모든 컨트롤러에 대 한 전역적으로 합니다. 인증 필터 요청에 자격 증명을 처리 하 고 해당 보안 주체를 제공 합니다. 인증 필터 권한이 없는 요청에 부응 인증 챌린지에 추가할 수도 있습니다.

### <a name="filter-overrides"></a>필터 재정

이제 재정의 필터를 지정 하 여 지정 된 동작 메서드 또는 컨트롤러에 적용 하는 필터를 재정의할 수 있습니다. 재정의 필터에 지정된 된 범위 (작업이 나 컨트롤러)에 대 한 실행 하지 않아야 하는 필터 형식 집합을 지정 합니다. 이 통해 전체적으로 적용 되지만 다음의 특정 작업이 나 컨트롤러에 적용 하 여 특정 전역 필터를 제외 하는 필터를 구성할 수 있습니다.

### <a name="attribute-routing"></a>특성 라우팅

ASP.NET MVC의 작성자, Tim McCall 여 기여 덕분에 특성 라우팅을 지원 [ http://attributerouting.net ](http://attributerouting.net)합니다. 특성 라우팅을 사용 하 여 작업 및 컨트롤러를 주석을 달아 프로그램 경로 지정할 수 있습니다.

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a>ASP.NET Web API 2

### <a name="attribute-routing"></a>특성 라우팅

ASP.NET Web API는 이제 Tim McCall, 작성자에 의해 기여 덕분에 특성 라우팅을 지원 [ http://attributerouting.net ](http://attributerouting.net)합니다. 특성 라우팅을 사용 하 여 다음과 같은 컨트롤러를 주석을 달아 웹 API 경로 지정할 수 있습니다.

[!code-csharp[Main](release-notes/samples/sample1.cs)]

특성 라우팅을 제어할 수 더 많은 Uri 통해 웹 API에에서 있습니다. 예를 들어 단일 API 컨트롤러를 사용 하 여 리소스 계층 구조를 쉽게 정의할 수 있습니다.

[!code-csharp[Main](release-notes/samples/sample2.cs)]

특성 라우팅을 선택적 매개 변수, 기본값 및 경로 제약 조건을 지정 하기 위한 편리한 구문을 제공 합니다.

[!code-csharp[Main](release-notes/samples/sample3.cs)]

특성 라우팅에 대 한 자세한 내용은 참조 [특성 Web API 2에서의 라우팅](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md)합니다.

### <a name="oauth-20"></a>OAuth 2.0

이제 Web API 및 단일 페이지 응용 프로그램 프로젝트 템플릿이 OAuth 2.0을 사용 하는 인증을 지원 합니다. OAuth 2.0은 보호 된 리소스에 대 한 클라이언트 액세스 권한 부여를 위한 프레임 워크. 브라우저 및 모바일 장치를 포함 하 여 클라이언트의 다양 한 작동 합니다.

OAuth 2.0에 대 한 지원 구현 하는 권한 부여 서버 역할 및 Microsoft OWIN 구성 요소에서 제공 하는 전달자 인증에 대 한 새 보안 미들웨어를 기반으로 합니다. 또는 Azure Active Directory 또는 Windows Server 2012 r 2에서 ad FS와 같은 조직 권한 부여 서버를 사용 하 여 클라이언트에 권한을 부여할 수 있습니다.

### <a name="odata-improvements"></a>OData 개선 사항

**$Batch, 및 $value $select, $에 대 한 지원 확장**

이제 완전히 지원 ASP.NET Web API OData $select에 대 한, $expand, 및 $value 합니다. 또한 일괄 처리 및 변경 집합이 처리 요청에 대 한 $batch를 사용할 수 있습니다.

$Select 및 $expand 옵션 OData 끝점에서 반환 되는 데이터의 모양을 변경할 수 있습니다. 자세한 내용은 참조 [$select 소개 및 $expand에 Web API OData 지원](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md)합니다.

**향상 된 확장성**

이제 OData 포맷터를 확장할 수 있습니다. Atom 항목 메타 데이터를 추가할 명명 된 스트림 및 미디어 링크 항목을 지원 및 인스턴스 주석을 추가 링크가 생성 되는 방법을 사용자 지정할 수 있습니다.

**형식 없는 지원**

이제 엔터티 형식에 대 한 CLR 형식을 정의할 필요 없이 OData 서비스를 작성할 수 있습니다. OData 컨트롤러 수 걸리거나의 인스턴스를 반환 하는 대신, **IEdmObject**되는 OData 포맷터 직렬화/역직렬화 합니다.

**기존 모델을 다시 사용**

기존 엔터티 데이터 모델 (EDM)를 이미 있는 경우 이제 다시 사용할 수 있습니다 것을 직접 새로 작성 하는 대신 합니다. 예를 들어, Entity Framework를 사용 하는 경우에 EF 빌드 수에 대 한 EDM를 사용할 수 있습니다.

### <a name="request-batching"></a>일괄 처리 요청

일괄 처리 요청 네트워크 트래픽을 줄일 수 다 스러운 사용자 인터페이스 보다 매끄럽게, 제공 하는 단일 HTTP POST 요청을 여러 작업을 결합 합니다. ASP.NET Web API는 이제 일괄 처리 요청에 대 한 몇 가지 전략을 지원합니다.

- OData 서비스의 $batch 끝점을 사용 합니다.
- 여러 개의 요청을 단일 MIME 다중 파트 요청으로 패키지 합니다.
- 일괄 처리 사용자 지정 형식을 사용 합니다.

일괄 처리 요청을 사용 하려면 Web API 구성을 일괄 처리 처리기가 포함 된 경로 추가 합니다.

[!code-csharp[Main](release-notes/samples/sample4.cs)]

제어할 수도 있는지 여부를 요청 또는 순차적으로 또는 순서에 관계 없이 실행 합니다.

### <a name="portable-aspnet-web-api-client"></a>휴대용 ASP.NET 웹 API 클라이언트

이제 Windows 스토어 및 Windows Phone 8 응용 프로그램에 걸쳐 작동 하는 이식 가능한 클래스 라이브러리를 만드는 ASP.NET 웹 API 클라이언트를 사용할 수 있습니다. 클라이언트와 서버 간에 공유할 수 있는 휴대용 포맷터를 만들 수 있습니다.

### <a name="improved-testability"></a>테스트 용이성 향상된

API 2에서는 웹 API 컨트롤러를 테스트 하는 것이 훨씬 쉽게 단위 수입니다. 방금 요청 메시지와 구성을 API 컨트롤러 인스턴스화하고 테스트 하려는 작업 메서드를 호출 합니다. 모의로 쉽게는 **UrlHelper** 링크 생성을 수행 하는 작업 방법에 대 한 클래스입니다.

### <a name="ihttpactionresult"></a>IHttpActionResult

이제 Web API 동작 메서드의 결과 캡슐화 하는 IHttpActionResult 구현할 수 있습니다. 웹 API 동작 메서드에서 반환 되는 IHttpActionResult 결과 응답 메시지를 만들기 위해 ASP.NET Web API 런타임에 의해 실행 됩니다. IHttpActionResult 단위를 간소화 하기 위해 웹 API 작업에서 반환 될 수의 웹 API 구현을 테스트 합니다. 많은 IHttpActionResult 구현 관련 상태 코드를 반환 하는 것에 대 한 결과 포함 하 여 기본적으로 제공 되는 편의 위해 콘텐츠 또는 콘텐츠 협상 응답을 포맷 합니다.

### <a name="httprequestcontext"></a>HttpRequestContext

새 **HttpRequestContext** 요청에 연결 하지 않으면이 요청에서 바로 사용할 수 있는 모든 상태를 추적 합니다. 예를 들어, 사용할 수는 **HttpRequestContext** 경로 데이터를 클라이언트 인증서를 요청에 연결 된 보안 주체 가져오는 **UrlHelper** 및 가상 경로 루트입니다. 쉽게 만들 수 있습니다는 **HttpRequestContext** 단위에 대 한 테스트 목적으로 합니다.

요청에 대 한 보안 주체에 의존 하지 않고 요청으로 흐를 때문에 **Thread.CurrentPrincipal**, Web API 파이프라인 되는 동안 주 서버 요청의 수명 주기 동안 출시 되었습니다.

### <a name="cors"></a>CORS

Brock Allen에서 또 다른 훌륭한 기여를 통해 ASP.NET 완벽 하 게 지원 요청 공유 CORS (Cross Origin).

브라우저의 보안 기능은 웹 페이지에서 다른 도메인으로 AJAX 요청을 전송하는 것을 막습니다. [CORS](http://www.w3.org/TR/cors/) 은 W3C 표준 동일 원본 정책을 완화 하도록 서버입니다. CORS를 사용하면 서버가 명시적으로 특정 교차 원본 요청만 허용하고, 다른 요청은 거부할 수 있습니다.

Web API 2에는 이제 자동으로 실행 전 요청 처리를 포함 하 여 CORS를 지원 합니다. 자세한 내용은 참조 [ASP.NET Web API에서 크로스-원본 요청을 사용 하도록 설정](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md)합니다.

### <a name="authentication-filters"></a>인증 필터

인증 필터는 새로운 종류의 필터에 ASP.NET Web API 파이프라인의 권한 부여 필터 전에 실행 하 고 인증 논리 당-작업을 지정할 수 있도록 하는 ASP.NET Web API 컨트롤러 당 또는 모든 컨트롤러에 대 한 전역적으로 합니다. 인증 필터 요청에 자격 증명을 처리 하 고 해당 보안 주체를 제공 합니다. 인증 필터 권한이 없는 요청에 부응 인증 챌린지에 추가할 수도 있습니다.

### <a name="filter-overrides"></a>필터 재정

이제 재정의 필터를 지정 하 여 지정 된 동작 메서드 또는 컨트롤러에 적용 하는 필터를 재정의할 수 있습니다. 재정의 필터에 지정된 된 범위 (작업이 나 컨트롤러)에 대 한 실행 하지 않아야 하는 필터 형식 집합을 지정 합니다. 이 옵션을 사용 하면 전역 필터를 추가 하지만 특정 작업이 나 컨트롤러에서 일부를 제외할 수 있습니다.

### <a name="owin-integration"></a>OWIN 통합

ASP.NET Web API 이제 완벽 하 게 지원 OWIN 하며 모든 OWIN 가능 호스트에서 실행할 수 있습니다. 또한 포함 됩니다는 **HostAuthenticationFilter** OWIN 인증 시스템과 통합을 제공 하는 합니다.

OWIN 통합 SignalR 등 다른 OWIN 미들웨어와 함께 사용자가 소유한 프로세스에 Web API를 자체 호스트할 수 있습니다. 자세한 내용은 참조 [Self-Host ASP.NET Web API를 사용 하 여 OWIN](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)합니다.

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a>ASP.NET SignalR 2.0

다음 섹션에서는 SignalR 2.0의 기능을 설명 합니다.

- [OWIN 기반](#builtonowin)
- [MapHubs 및 MapConnection MapSignalR 됩니다.](#MapSignalR)
- [도메인 간 지원](#crossdomain)
- [iOS 및 Android MonoTouch 및 MonoDroid를 통해 지원](#mobile)
- [이식 가능한.NET 클라이언트](#portable)
- [자체 호스트 하는 새 패키지](#selfhost)
- [이전 버전과 호환성 서버 지원](#backwardcompat)
- [.NET 4.0에 대 한 서버 지원을 제거](#remove40)
- [클라이언트 및 그룹의 목록으로 메시지 보내기](#messagelist)
- [특정 사용자에 게 메시지 보내기](#sendtouser)
- [더 나은 오류 처리 지원](#errorhandling)
- [보다 쉽게 단위 테스트 허브의](#unittesting)
- [JavaScript 오류 처리](#javascripterror)

SignalR 2.0으로 기존 1.x 프로젝트를 업그레이드 하는 방법의 예제를 보려면 [업그레이드 하는 SignalR 프로젝트 1.x](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md)합니다.

<a id="builtonowin"></a>
### <a name="built-on-owin"></a>OWIN 기반

SignalR 2.0에 완전히 빌드될 [OWIN (.NET에 대 한 Open Web Interface)](http://owin.org/)합니다. 이러한 변경 하면 설치 프로세스를 SignalR에 대 한 훨씬 더 웹 호스팅 및 자체 호스트 된 SignalR 응용 프로그램 간에 일관 하지만 다양 한 API 변경 때도 필요 합니다.

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a>MapHubs 및 MapConnection MapSignalR 됩니다.

OWIN 표준 호환성을 위해 이러한 메서드로 변경 되었습니다 `MapSignalR`합니다. `MapSignalR` 매개 변수는 모든 허브 매핑됩니다 없이 호출 (으로 `MapHubs` 버전에서 1.x); 개별 매핑할 **PersistentConnection** 개체, 형식 매개 변수 및으로 연결에 대 한 URL 확장명 연결 유형을 지정는 첫 번째 인수입니다.

`MapSignalR` 메서드 Owin 시작 클래스에서 호출 됩니다. Owin 시작 클래스;에 대 한 새 서식 파일을 포함 하는 visual Studio 2013 이 서식 파일을 사용 하려면 다음을 수행 합니다.

1. 프로젝트를 마우스 오른쪽 단추로 클릭
2. 선택 **추가**, **새 항목...**
3. 선택 **Owin 시작 클래스**합니다. 클래스의 새 이름을 **Startup.cs**합니다.

에 **웹 응용 프로그램을** 는 Owin 시작 클래스를 포함 하는 `MapSignalR` 메서드가 아래와 같이 다음 항목을 사용 하 여 Web.Config 파일의 응용 프로그램 설정 노드에 Owin의 시작 프로세스에 추가 됩니다.

에 **자체 응용 프로그램을 호스트**, 시작 클래스의 형식 매개 변수로 전달 되는 `WebApp.Start` 메서드.

**SignalR 연결 및 허브 매핑 1.x (웹 응용 프로그램의 전역 응용 프로그램 파일)에서:** 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

**Owin 시작 클래스 파일) (에서 SignalR 2.0의 연결 및 허브 매핑:** 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

에 **자체 응용 프로그램을 호스트**, 시작 클래스에 대 한 형식 매개 변수로 전달 되는 `WebApp.Start` 메서드를 다음과 같이 합니다.

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a>도메인 간 지원

SignalR에서 도메인 간 요청 1.x 된 단일 EnableCrossDomain 플래그에 의해 제어 됩니다. 이 플래그는 모두 JSONP 및 CORS 요청을 제어합니다. 모든 CORS 지원 유연성을 높이기 위해 SignalR의 서버 구성 요소에서 제거 되었습니다 (JavaScript lients 여전히 CORS 일반적으로 브라우저 지원 하는지 검색 하는 경우)을 사용할 새 OWIN 미들웨어가 제공 되기 이러한 시나리오를 지원 하도록 하 고 있습니다.

SignalR 2.0의 경우 JSONP에 필요 클라이언트 (이전 브라우저에서 도메인 간 요청을 지 원하는)을 설정 하 여 명시적으로 설정 해야 합니다 `EnableJSONP` 에 `HubConfiguration` 개체를 `true`다음과 같이 합니다. JSONP는 CORS 보다 덜 안전 이므로 기본적으로 비활성화 됩니다.

SignalR 2.0을 새 CORS 미들웨어를 추가 하려면 추가 `Microsoft.Owin.Cors` 라이브러리를 프로젝트 및 호출 `UseCors` SignalR 미들웨어, 아래 섹션에 나와 있는 것 처럼 하기 전에.

**Microsoft.Owin.Cors 프로젝트에 추가**:이 라이브러리를 설치 하려면 패키지 관리자 콘솔에서 다음 명령을 실행 합니다.

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

이 명령은 2.0.0을 추가 합니다 프로젝트에 패키지의 버전입니다.

**UseCors 호출**

다음 코드 조각에는 SignalR에서 도메인 간 연결을 구현 하는 방법을 보여 1.x 및 2.0.

**SignalR에서 도메인 간 요청을 구현 1.x (에서 전역 응용 프로그램 파일)**

[!code-csharp[Main](release-notes/samples/sample9.cs)]

**(C# 코드 파일)에서 SignalR 2.0에서 도메인 간 요청을 구현합니다.**

다음 코드는 SignalR 2.0 프로젝트에서 JSONP 또는 CORS를 사용 하도록 설정 하는 방법을 보여 줍니다. 이 코드 샘플에서는 `Map` 및 `RunSignalR` 대신 `MapSignalR`CORS 미들웨어 CORS 지원 해야 하는 SignalR 요청에 대해서만 실행 되도록 하는, (아니라에 지정 된 경로에 모든 트래픽에 대해 `MapSignalR`.) `Map` 특정 URL 접두사에 대 한 아니라 전체 응용 프로그램을 실행 하는 다른 모든 미들웨어에 대 한 사용할 수도 있습니다.

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a>iOS 및 Android MonoTouch 및 MonoDroid를 통해 지원

IOS 및 Android 클라이언트에서 MonoTouch 및 MonoDroid 구성 요소를 사용 하 여에 대 한 지원이 추가 되었습니다는 [Xamarin 라이브러리](https://xamarin.com/)합니다. 사용 하는 방법에 대 한 자세한 내용은 참조 하십시오. [Xamarin 구성 요소를 사용 하 여](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln)합니다. 이러한 구성 요소에서 사용할 수 있습니다는 [Xamarin 스토어](https://store.xamarin.com/) SignalR RTW 릴리스를 사용할 수 있습니다.

<a id="portable"></a> # # # 이식 가능한.NET 클라이언트

보다 잘 Silverlight, WinRT 플랫폼 간 개발을 용이 하 게 하 고 Windows Phone 클라이언트는 단일 이식 가능한.NET 클라이언트를 지 원하는 플랫폼은 다음과 같은 대체 되었습니다.

- NET 4.5
- Silverlight 5
- WinRT (Windows 스토어 앱 용.NET)
- Windows Phone 8

<a id="selfhost"></a>

### <a name="new-self-host-package"></a>자체 호스트 하는 새 패키지

SignalR 자가 호스트 (SignalR 응용 프로그램 프로세스에서 호스트 되는 다른 응용 프로그램을 대신 또는 웹 서버에 호스트 중인)를 시작 하기 쉽게 수행할 수 있도록 NuGet 패키지가 됩니다. SignalR을 사용 하 여 작성 하는 자체 호스트 프로젝트를 업그레이드 하려면 1.x Microsoft.AspNet.SignalR.Owin 패키지를 제거 하 고 Microsoft.AspNet.SignalR.SelfHost 패키지를 추가 합니다. 시작 자가 호스트 패키지에 대 한 자세한 내용은 참조 하십시오. [자습서: 자체 호스트 하는 SignalR](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)합니다.

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a>이전 버전과 호환성 서버 지원

이전 버전의 SignalR에 동일 해야 하는 서버 및 클라이언트에서 사용 되는 SignalR 패키지의 버전입니다. 업데이트 하기 어려운는 굵게 클라이언트 응용 프로그램을 지원 하기 위해 SignalR 2.0 이전 클라이언트를 최신 서버 버전을 사용 하 여 이제 지원 합니다. **참고: SignalR 2.0 최신 클라이언트를 사용 하 여 이전 버전으로 작성 하는 서버를 지원 하지 않습니다.**

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a>.NET 4.0에 대 한 서버 지원을 제거

SignalR 2.0 미만으로 떨어졌습니다.NET 4.0이 있는 서버 상호 운용성에 대 한 지원. .NET 4.5 SignalR 2.0 서버와 함께 사용 되어야 합니다. SignalR 2.0에 대 한.NET 4.0 클라이언트는 여전히 합니다.

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a>클라이언트 및 그룹의 목록으로 메시지 보내기

SignalR 2.0에서는 클라이언트와 그룹 Id 목록을 사용 하 여 메시지를 보낼 수는. 다음 코드 조각에서는이 작업을 수행 하는 방법을 보여 줍니다.

**클라이언트 및 PersistentConnection를 사용 하 여 그룹의 목록으로 메시지 보내기**

[!code-csharp[Main](release-notes/samples/sample11.cs)]

**클라이언트와 허브를 사용 하 여 그룹의 목록으로 메시지 보내기**

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a>특정 사용자에 게 메시지 보내기

사용자 대상을 지정 하는 사용자 Id는이 기능을 통해 IUserIdProvider 새 인터페이스를 통해 IRequest에 따라:

**IUserIdProvider 인터페이스**

[!code-csharp[Main](release-notes/samples/sample13.cs)]

기본적으로에 사용자의 IPrincipal.Identity.Name 사용자 이름으로 사용 하는 구현이 생깁니다.

허브에서 새 API 통해 이러한 사용자에 게 메시지를 보낼 수 있습니다.

**Clients.User API를 사용 하 여**

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a>더 나은 오류 처리 지원

사용자가 throw 할 수 이제 **HubException** 모든 허브 호출에서. 생성자는 **HubException** 문자열 메시지와 개체 표시 되려면 추가 오류 데이터입니다. SignalR 예외를 자동 serialize 하 고 클라이언트에 보냅니다 거부/실패 허브 메서드 호출에 사용할 수는 됩니다.

**자세한 허브 예외 표시** 설정은 관련이 없습니다 **HubException** 는 없습니다; 다시 클라이언트에 전송 되 고 항상 전송 됩니다.

**서버 쪽 코드는 HubException 클라이언트에 게 보내는 시연**

[!code-csharp[Main](release-notes/samples/sample15.cs)]

**JavaScript 클라이언트 코드가 서버에서 보낸 HubException에 응답을 시연**

[!code-html[Main](release-notes/samples/sample16.html)]

**서버에서 보낸 HubException에 응답을 보여 주는.NET 클라이언트 코드**

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a>보다 쉽게 단위 테스트 허브의

SignalR 2.0 이라는 인터페이스에 `IHubCallerConnectionContext` 모의 클라이언트 쪽 호출을 만드는 쉽게 허브에서. 다음 코드 조각 인기 있는 테스트 장비와이 인터페이스를 사용 하 여 보여 줍니다. [xUnit.net](https://github.com/xunit/xunit) 및 [moq](https://code.google.com/p/moq/)합니다.

**SignalR를 사용한 단위 테스트 xUnit.net**

[!code-csharp[Main](release-notes/samples/sample18.cs)]

**SignalR를 사용한 단위 테스트 moq**

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a>JavaScript 오류 처리

SignalR 2.0 모든 JavaScript 오류 처리 콜백을 원시 문자열 대신 JavaScript 오류 개체를 반환 합니다. 따라서 오류 처리기에 다양 한 정보를 이동 하는 SignalR 수 있습니다. 내부 예외를 가져올 수 있습니다는 `source` 오류 속성입니다.

**Start.Fail 예외를 처리 하는 JavaScript 클라이언트 코드**

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a>ASP.NET ID

### <a name="new-aspnet-membership-system"></a>새 ASP.NET 멤버 자격 시스템

ASP.NET Id는 ASP.NET 응용 프로그램에 대 한 새 멤버 자격 시스템입니다. ASP.NET Id를 사용 하면 쉽게 응용 프로그램 데이터와 사용자 고유의 프로필 데이터를 통합할 수 있습니다. ASP.NET Id를 사용 하면 응용 프로그램의 사용자 프로필에 대 한 지 속성 모델을 선택할 수 있습니다. SQL Server 데이터베이스 또는 Azure 저장소 테이블 같은 NoSQL 데이터 저장소를 포함 하 여 다른 데이터 저장소에 데이터를 저장할 수 있습니다. 자세한 내용은 참조 [개별 사용자 계정](creating-web-projects-in-visual-studio.md#indauth) 에 **Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기**합니다.

### <a name="claims-based-authentication"></a>클레임 기반 인증

이제 ASP.NET 클레임 기반 인증 일 경우 사용자의 id은 신뢰할 수 있는 발급자 클레임 집합으로 표시 되는 위치를 지원 합니다. 인증 된 사용자 이름 및 응용 프로그램 데이터베이스에서 유지 관리 하는 암호를 사용 하 여 또는 소셜 id 공급자를 사용 하 여 사용자가 될 수 있습니다 (예: Microsoft 계정, Facebook, Google, Twitter), 또는 Azure Active Directory를 통해 조직 계정을 사용 하 여 또는 Active Directory Federation Services (ad FS)입니다.

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a>Azure Active Directory 및 Windows Server Active Directory와의 통합

이제 인증을 위해 Azure Active Directory 또는 Windows Server AD (Active Directory)를 사용 하는 ASP.NET 프로젝트를 만들 수 있습니다. 자세한 내용은 참조 [조직 계정](creating-web-projects-in-visual-studio.md#orgauth) 에 **Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기**합니다.

### <a name="owin-integration"></a>OWIN 통합

ASP.NET 인증은 이제 모든 OWIN 기반 호스트에서 사용할 수 있는 OWIN 미들웨어 기반으로 합니다. OWIN에 대 한 자세한 내용은 다음을 참조 하십시오. [Microsoft OWIN 구성 요소](#TOC7) 섹션.

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a>Microsoft OWIN 구성 요소

[.NET 용 웹 인터페이스를 열고](http://owin.org/) (OWIN).NET 웹 서버와 웹 응용 프로그램 간의 추상화를 정의 합니다. OWIN 웹 응용 프로그램 호스트를 알 수 없는 하는 서버에서 웹 응용 프로그램을 분리 합니다. 예를 들어 IIS에서 OWIN 기반 웹 응용 프로그램을 호스팅할 수도 있고 사용자 지정 프로세스에서 자체 호스트할 수 있습니다.

Microsoft OWIN 구성 요소 (Katana 프로젝트 라고도 함)에 도입 된 변경 내용을 새 서버와 호스트 구성 요소, 새로운 도우미 라이브러리 및 미들웨어 및 새로운 인증 미들웨어 포함 됩니다.

OWIN 및 Katana에 대 한 자세한 내용은 참조 [OWIN 및 Katana 새로운](../../../aspnet/overview/owin-and-katana/index.md)합니다.

**참고: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) 응용 프로그램 IIS 클래식 모드에서 실행할 수 없습니다; 통합된 모드에서 실행 해야 합니다.**

**참고: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) 완전 신뢰에서 응용 프로그램을 실행 합니다.**

### <a name="new-servers-and-hosts"></a>새 서버와 호스트

이 릴리스에서 새 구성 요소는 자체 호스트 시나리오를 사용 하도록 설정에 추가 되었습니다. 이러한 구성 요소는 다음과 같은 NuGet 패키지를 같습니다.

- **Microsoft.Owin.Host.HttpListener**. 사용 하는 OWIN 서버 제공 **HttpListener** 하 OWIN 파이프라인에 지시 하 고 HTTP 요청을 수신 합니다.
- **Microsoft.Owin.Hosting** 자체 콘솔 응용 프로그램 또는 Windows 서비스와 같은 사용자 지정 프로세스에서 OWIN 파이프라인을 호스트 하려는 개발자가 있는 라이브러리를 제공 합니다.
- **OwinHost**합니다. 래핑하는 독립 실행형 실행 파일을 제공 `Microsoft.Owin.Hosting` 자체 사용자 지정 호스트 응용 프로그램을 작성 하지 않고도 OWIN 파이프라인을 호스팅할 수 있습니다.

또한는 `Microsoft.Owin.Host.SystemWeb` 패키지 수 있게 되었습니다. 힌트를 제공 하는 미들웨어는 **SystemWeb** 특정 ASP.NET 파이프라인 단계 동안 미들웨어를 호출 해야 함을 나타내는 서버입니다. 이 기능은 인증 미들웨어 초기 ASP.NET 파이프라인에에서 실행 되어야 하는 데 특히 유용 합니다.

### <a name="helper-libraries-and-middleware"></a>도우미 라이브러리 및 미들웨어

OWIN 사양에서 함수 및 유형 정의 사용 하는 OWIN 구성 요소를 작성할 수 있지만 새 `Microsoft.Owin` 패키지 보다 사용자 친화적인 집합의 추상화를 제공 합니다. 이 패키지는 여러 이전 패키지 결합 (예: `Owin.Extensions`, `Owin.Types`) 사용할 수 있는 다음 쉽게 다른 OWIN 구성 요소에서 단일, 잘 구성 된 개체 모델을 합니다. 실제로 대부분의 Microsoft OWIN 구성 요소는 이제이 패키지를 사용 합니다.

> [!NOTE]
> [OWIN](http://www.owin.org) 응용 프로그램 IIS 클래식 모드에서 실행할 수 없습니다; 통합된 모드에서 실행 해야 합니다.

> [!NOTE]
> [OWIN](http://www.owin.org) 완전 신뢰에서 응용 프로그램을 실행 합니다.

이 릴리스에서 실행 중인 OWIN 응용 프로그램 유효성을 검사 하는 미들웨어와 오류를 조사 하는 데 오류 페이지 미들웨어를 포함 하는 Microsoft.Owin.Diagnostics 패키지용을 포함 됩니다.

### <a name="authentication-components"></a>인증 구성 요소

다음 인증 구성 요소가 사용할 수 있습니다.

- **Microsoft.Owin.Security.ActiveDirectory**. 온-프레미스 또는 클라우드 기반 디렉터리 서비스를 사용 하 여 인증을 사용 하도록 설정 합니다.
- **Microsoft.Owin.Security.Cookies** 쿠키를 사용 하 여 사용 하면 인증 합니다. 이 패키지 변수의 이름이 이전에 `Microsoft.Owin.Security.Forms`합니다.
- **Microsoft.Owin.Security.Facebook** Facebook의 OAuth 기반 서비스를 사용 하 여 사용 하면 인증 합니다.
- **Microsoft.Owin.Security.Google** Google의 OpenID 기반 서비스를 사용 하 여 사용 하면 인증 합니다.
- **Microsoft.Owin.Security.Jwt** JWT 토큰을 사용 하 여 사용 하면 인증 합니다.
- **Microsoft.Owin.Security.MicrosoftAccount** Microsoft 계정을 사용 하 여 사용 하면 인증 합니다.
- **Microsoft.Owin.Security.OAuth**. 전달자 토큰을 인증 하기 위한에서는 OAuth 권한 부여 서버는 물론 미들웨어를 제공 합니다.
- **Microsoft.Owin.Security.Twitter** Twitter의 OAuth 기반 서비스를 사용 하 여 사용 하면 인증 합니다.

또한이 릴리스는는 `Microsoft.Owin.Cors` 크로스-원본 HTTP 요청 처리에 대 한 미들웨어를 포함 하는 패키지입니다.

> [!NOTE]
> Visual Studio 2013의 최종 버전에서 JWT를 서명 하는 것에 대 한 지원이 제거 되었습니다.

<a id="ef6"></a>
## <a name="entity-framework-6"></a>Entity Framework 6

새로운 기능 및 Entity Framework 6의 다른 변경의 목록이 참조 [Entity Framework 버전 기록이](https://msdn.com/data/jj574253)합니다.

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a>ASP.NET Razor 3

ASP.NET Razor 3에는 다음과 같은 새로운 기능이 포함 됩니다.

- 탭에서 편집할 수 있습니다. Preivously,는 **문서 서식** 사용 하는 경우 명령, 자동 들여쓰기 및 서식을 Visual Studio에서 자동 올바르게 작동 하지 않았습니다 고 **탭 유지** 옵션입니다. 이 변경에는 Visual Studio 서식 탭에 대 한 Razor 코드에 대 한 서식을 해결 합니다.
- 링크를 생성 하는 경우 URL 재작성 규칙에 대 한 지원 합니다.
- 보안 투명 특성으로 제거 합니다.
  > [!NOTE]
  > 이 주요 변경 내용, 고 Razor 3 호환 되지 않는 mvc 4 및 이전 버전에서는 동안 Razor 2 m v c 5 또는 m v c 5에 대해 컴파일된 어셈블리와 호환 되지 않습니다.

시험판 버전에서 Visual Studio 2013에서 해결 된 razor 3 문제 있습니다 [여기](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0)합니다.

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a>ASP.NET 앱 일시 중단

ASP.NET 앱 일시 중단에는 사용자 환경 및 많은 수의 단일 컴퓨터에 ASP.NET 사이트를 호스팅하기 위한 경제 모델 근본적으로 변경 하는.NET Framework 4.5.1의에서 게임 변경 기능입니다. 자세한 내용은 참조 [ASP.NET 앱 일시 중단 – 응답 공유.NET 웹 호스팅](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx)합니다.

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a>알려진된 문제 및 주요 변경 내용

이 섹션에서는 Visual Studio 2013 용 ASP.NET 및 Web Tools의 주요 변경 내용 및 알려진된 문제를 설명 합니다.

### <a name="nuget"></a>NuGet

- [SLN 파일을 사용 하는 경우 새 패키지를 복원 모노에서 작동 하지 않습니다](https://nuget.codeplex.com/workitem/3596) – 예정 된 nuget.exe 다운로드에 수정 될 예정 및 [NuGet.CommandLine 패키지](http://www.nuget.org/packages/NuGet.CommandLine/) 업데이트 합니다.
- [새 패키지를 복원 Wix 프로젝트와 함께 작동 하지 않는](https://nuget.codeplex.com/workitem/3598) – 예정 된 nuget.exe 다운로드에 수정 될 예정 및 [NuGet.CommandLine 패키지](http://www.nuget.org/packages/NuGet.CommandLine/) 업데이트 합니다.
- [프로젝트는 솔루션 폴더에 대 한 자동 패키지 복원 작동 하지 않는](https://nuget.codeplex.com/workitem/3625) – NuGet 2.8에서 수정 됩니다.

### <a name="aspnet-web-api"></a>ASP.NET Web API

1. `ODataQueryOptions<T>.ApplyTo(IQueryable)` 반환 하지 `IQueryable<T>` 에 대 한 지원을 추가 하는 대로 항상 `$select` 및 `$expand`합니다.

    에 대 한 이전 샘플 `ODataQueryOptions<T>` 항상 캐스팅할의 반환 값에서 `ApplyTo` 를 `IQueryable<T>`합니다. 이전에서는이 되는 쿼리 옵션 때문에 이전 작업을 지원 하는지 (`$filter`, `$orderby`, `$skip`, `$top`) 쿼리의 셰이프를 변경 하지 마십시오. 지원 했으므로 `$select` 및 `$expand` 반환 값을 `ApplyTo` 됩니다 `IQueryable<T>` 항상 합니다.

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    클라이언트를 보내지 않는 경우 작업에서 이전 예제 코드를 사용 하는 경우 계속 `$select` 및 `$expand`합니다. 그러나 지원 하려는 경우 `$select` 및 `$expand` 이 코드를 변경 해야 합니다.

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. **일괄 처리를 요청 하는 동안 Request.Url 나 RequestContext.Url null 임**

    일괄 처리 시나리오에서 **UrlHelper** 에서 액세스할 때 null **Request.Url** 또는 **RequestContext.Url**합니다.

    현재이 문제는 여기에 추적: [BatchRequestContext.Url은 요청을 일괄 처리에 대해 null](http://aspnetwebstack.codeplex.com/workitem/1301)합니다.

    새 인스턴스를 만드는 것이 문제에 대 한 해결 **UrlHelper**다음 예제와 같이,:

    **UrlHelper의 새 인스턴스 만들기**

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a>ASP.NET MVC

1. 를 사용할 때는 m v c 5 OrgAuth, AntiForgerToken 유효성 검사를 수행 하는 보기가 있는 경우 보기에 데이터를 게시 하면 다음 오류를 발견할 수 있습니다.

    **오류**:

    *'/' 응용 프로그램에서 서버 오류입니다.*

    <em>형식의 클레임이 '<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>'또는'<http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>'에 제공 된 ClaimsIdentity 표시 되지 않았습니다. 위조 방지 토큰 지원 클레임 기반 인증을 사용 하도록 설정 하려면 구성 된 클레임 공급자 생성 ClaimsIdentity 인스턴스에서 이러한 클레임의 둘 다 제공할가 있는지 확인 하십시오. 구성 된 클레임 공급자 대신 다른 클레임 유형에 사용 하 여 고유 식별자로, AntiForgeryConfig.UniqueClaimTypeIdentifier 정적 속성을 설정 하 여 구성할 수 있습니다.</em>

    **해결 방법**:

    해결 하는 Global.asax에 다음 줄을 추가 합니다.

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    그러면 다음 릴리스에 대 한 수정 됩니다.
2. Mvc 4 응용 m v c 5로 업그레이드 한 후 솔루션을 빌드하고 응용 프로그램을 시작 합니다. 다음과 같은 오류가 나타납니다.

    [A] System.Web.WebPages.Razor.Configuration.HostSection [B]System.Web.WebPages.Razor.Configuration.HostSection으로 캐스팅할 수 없습니다. Type A originates from 'System.Web.WebPages.Razor, Version=2.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35\System.Web.WebPages.Razor.dll'. B 형식 발생 ' System.Web.WebPages.Razor, Version 3.0.0.0, Culture = neutral, PublicKeyToken = = 31bf3856ad364e35' 컨텍스트의 'Default' 위치에 ' C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\ e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01\System.Web.WebPages.Razor.dll'.

    위의 오류를 해결 하려면 열고 *모든* 프로젝트 및 다음을 수행에 Web.config 파일 (Views 폴더에 있는 구성을 포함):

   1. 버전 "4.0.0.0"의 "System.Web.Mvc"를 "5.0.0.0"의 모든 항목을 업데이트 합니다.
   2. "System.Web.Helpers"의 "2.0.0.0" 버전의 항목을 모두 업데이트 &quot;System.Web.WebPages&quot; 및 &quot;System.Web.WebPages.Razor&quot; "3.0.0.0"를

      예를 들어 위의 변경을 수행한 후 어셈블리 바인딩 다음과 같이 표시 됩니다.

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      MVC 5로 MVC 4 프로젝트 업그레이드에 대 한 자세한 내용은 참조 하십시오. [ASP.NET MVC 4 및 Web API 프로젝트를 ASP.NET MVC 5 및 Web API 2로 업그레이드 하는 방법을](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)합니다.
3. 유효성 검사 비 가시적인 jQuery 함께 클라이언트 쪽 유효성 검사를 사용 하면 유효성 검사 메시지 올바르지 않을 경우에 따라 형식과 HTML input 요소에 대 한 = 'number'. 유효성 검사 오류에 대해 필요한 값 ("The이 지 필드는 필수")가 표시 유효한 숫자가 필수임 올바른 메시지 대신 잘못 된 숫자 입력 된 경우.

    이 문제는 일반적으로 만들기 및 편집 보기에는 정수 속성을 사용 하 여 모델에 대 한 스 캐 폴드 코드로 발견 됩니다.

    이 문제를 해결 하려면 편집기 도우미를 변경 합니다.

    `@Html.EditorFor(person => person.Age)`

    대상:

    `@Html.TextBoxFor(person => person.Age)`
4. ASP.NET MVC 5 부분 신뢰를 더 이상 지원합니다. MVC 또는 WebAPI 바이너리에 연결 하는 프로젝트를 제거 해야는 [SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) 특성 및 [AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) 특성입니다. 이러한 특성을 제거 하면 다음과 같은 컴파일러 오류 제거 됩니다.

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > 단,이 사용자의 부작용으로 사용할 수 없습니다 4.0 및 5.0 어셈블리 같은 응용 프로그램. 5.0에이 모두 업데이트 해야 합니다.

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a>웹 사이트는 인트라넷 영역에서 호스트 하면서 Facebook 인증 인 SPA 템플릿을 IE에서 불안정 해질 수 있습니다.

SPA 템플릿은 Facebook 사용 하 여 외부 로그를 제공합니다. 템플릿을 사용 하 여 만든 프로젝트는 로컬로 실행 되는 경우 IE 작동이 중단 됩니다. 로그인에 발생할 수 있습니다.

해결책:

1. 인터넷 영역;에서 웹 사이트를 호스팅하거나 또는

2. IE 이외의 브라우저에서 시나리오를 테스트 합니다.

### <a name="web-forms-scaffolding"></a>Web Forms 스 캐 폴딩

Web Forms 스 캐 폴딩 VS2013에서 제거 되었습니다 및 Visual Studio에 대 한 향후 업데이트에서 사용할 수 있습니다. 그러나 Web Forms 프로젝트 내에서 스 캐 폴딩 MVC 종속성을 추가 하 고 스 캐 폴딩 MVC에 대해 생성 하 여 계속 사용할 수 있습니다. 프로젝트는 Web Forms 및 MVC의 조합을 포함 됩니다.

MVC Web Forms 프로젝트를 추가 하려면 새 스 캐 폴드 항목을 추가 하 고 선택 **MVC 5 종속성**합니다. 최소 또는 스크립트와 같은 콘텐츠 파일의 모든 해야 하는지 여부에 따라 전체 선택 합니다. Mvc 프로젝트의 뷰 및 컨트롤러를 생성 하는 스 캐 폴드 된 항목을 추가 합니다.

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC 및 Web API 스 캐 폴딩-HTTP 404 찾을 수 없음 오류

프로젝트에 스 캐 폴드 된 항목을 추가할 때 오류가 발생 있기 프로젝트 일관성 없는 상태로 유지 됩니다. 스 캐 폴딩 수 변경 중 일부는 롤백할 수 있지만 설치 된 NuGet 패키지와 같은 다른 변경 내용을 다시 롤백되며 되지 않습니다. 라우팅 구성 변경 내용이 롤백되어도 경우 스 캐 폴드 항목으로 이동 하는 경우 사용자가 HTTP 404 오류를 받습니다.

해결 방법:

- MVC에 대 한이 오류를 해결 하려면 새 스 캐 폴드 항목을 추가 하 고 MVC 5 종속성 선택 (최소 또는 전체). 이 프로세스의 모든 필요한 변경 사항을 프로젝트에 추가 합니다.
- 웹 API에 대 한이 오류를 해결 하려면:

  1. 프로젝트에 경우 WebApiConfig 클래스를 추가 합니다.

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. 응용 프로그램에서 WebApiConfig.Register 구성\_Global.asax에 다음과 같이 메서드를 시작 합니다.

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]
