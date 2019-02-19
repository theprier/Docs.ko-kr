---
uid: mvc/mvc5
title: ASP.NET MVC 5 | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 5 ASP.NET MVC 5는 체계적인 디자인 패턴 및 AS. 기능을 사용 하 여 확장성이 뛰어난 표준 기반 웹 응용 프로그램을 빌드하기 위한 프레임 워크...
ms.author: riande
ms.date: 10/11/2018
ms.assetid: f79fbf7f-59e5-4279-a832-c1a0294630f4
msc.legacyurl: /mvc/mvc5
msc.type: content
ms.openlocfilehash: 14fcf863a4ef5f6c9180cdf9e7b632ccdb1ebcb0
ms.sourcegitcommit: d75d8eb26c2cce19876c8d5b65ac8a4b21f625ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2019
ms.locfileid: "56410471"
---
<a name="aspnet-mvc-5"></a>ASP.NET MVC 5
====================
## <a name="whats-new-in-aspnet-mvc-5"></a>ASP.NET MVC 5의에서 새로운 기능

### <a name="one-aspnet"></a>One ASP.NET

웹 MVC 프로젝트 템플릿 One ASP.NET 환경을 원활 하 게 통합 합니다. MVC 프로젝트를 사용자 지정할 수 있으며 One ASP.NET 프로젝트 만들기 마법사를 사용 하 여 인증을 구성할 수 있습니다. ASP.NET MVC 5 소개 자습서에서 확인할 수 있습니다 [ASP.NET MVC 5 시작](overview/getting-started/introduction/getting-started.md)합니다.

MVC 4 프로젝트에서 MVC 5 업그레이드에 대 한 자세한 내용은 [ASP.NET MVC 5 및 Web API 2에는 ASP.NET MVC 4 및 Web API 프로젝트를 업그레이드 하는 방법](overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)합니다.

### <a name="aspnet-identity"></a>ASP.NET ID

MVC 프로젝트 템플릿 인증 및 id 관리에 대 한 ASP.NET Id를 사용 하도록 업데이트 되었습니다. Facebook 및 Google 인증 및 새 멤버 자격 API 자습서에서 확인할 수 있습니다 [Facebook 및 Google OAuth2 및 OpenID Sign on을 사용 하 여 ASP.NET MVC 5 앱 만들기](overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) 고 [사용 하 여 보안 ASP.NET MVC 앱 배포 멤버 자격, OAuth 및 SQL Database는 Windows Azure 웹 사이트를](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)입니다.

### <a name="bootstrap"></a>부트스트랩

MVC 프로젝트 템플릿을 사용 하도록 업데이트 되었습니다 [부트스트랩](http://getbootstrap.com/) 를 세련 되 고 응답성이 뛰어난 디자인을 쉽게 사용자 지정할 수 있도록 합니다. 자세한 내용은 [Visual Studio 웹 프로젝트 템플릿에서 부트스트랩](../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap)합니다.

### <a name="authentication-filters"></a>인증 필터

[인증 필터](http://www.dotnetcurry.com/showarticle.aspx?ID=957) 새로운 종류의 ASP.NET MVC 파이프라인에서 권한 부여 필터 전에 실행 하 고 인증 논리 작업을 지정할 수 있는 ASP.NET MVC의 필터는 컨트롤러 별로 또는 모든 컨트롤러에 대 한 전역적으로 합니다. 인증 필터는 요청에 자격 증명을 처리 하 고 해당 보안 주체를 제공 합니다. 인증 필터 권한이 없는 요청에 대 한 응답에서 인증 질문을 추가할 수도 있습니다. 참조 [ASP.NET MVC 5 인증 필터](http://www.dotnetcurry.com/showarticle.aspx?ID=957)하십시오 [ASP.NET MVC 5의에서 인증 필터](http://theshravan.net/blog/authentication-filters-in-asp-net-mvc-5/)합니다.

### <a name="filter-overrides"></a>필터 재정의

필터를 지정 하 여 지정 된 동작 메서드 또는 컨트롤러에 적용을 재정의할 수 있습니다는 [필터를 재정의](http://www.davidhayden.me/blog/filter-overrides-in-asp-net-mvc-5)합니다. 재정의 필터에 지정된 된 범위 (작업 또는 컨트롤러)에 대 한 실행 되지 않아야 하는 필터 형식 집합을 지정 합니다. 이 통해 전역적으로 적용 되지만 다음의 특정 작업이 나 컨트롤러에 적용에서 특정 전역 필터를 제외 하는 필터를 구성할 수 있습니다. 참조 [ASP.NET MVC 5 및 ASP.NET Web API 2의 기능은 새 필터 재정의](https://weblogs.asp.net/imranbaloch/archive/2013/09/25/new-filter-overrides-in-asp-net-mvc-5-and-asp-net-web-api-2.aspx)를 [ASP.NET MVC 5 필터 재정의 기능을 사용 하는 방법](http://hackwebwith.net/how-to-use-the-asp-net-mvc-5-filter-overrides-feature/), 및 [ASP.NET MVC 5의 필터 재정의](http://www.davidhayden.me/blog/filter-overrides-in-asp-net-mvc-5)

### <a name="attribute-routing"></a>특성 라우팅

ASP.NET MVC에서 지 원하는 [특성 라우팅은](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx), Tim McCall, 작성자에 의해 작성 글 덕분 [AttributeRouting](https://github.com/mccalltd/AttributeRouting)합니다. 특성 라우팅을 사용 하 여 작업 및 컨트롤러에 주석을 추가 하 여 경로 지정할 수 있습니다.

## <a name="new-web-project-experience"></a>새 웹 프로젝트 환경

Visual Studio에 Visual Studio 2013 부터는 새 웹 프로젝트를 만드는 환경을 향상 합니다. 에 **새 ASP.NET 웹 프로젝트** 대화 있습니다 원하는, 구성 (Web Forms, MVC, Web API) 기술의 조합을, 인증 옵션을 구성, Docker 지원 추가 및 단위 테스트 프로젝트 추가 프로젝트 형식을 선택할 수 있습니다.

![새 ASP.NET 프로젝트](mvc5/_static/new-aspnet-web-app-dialog.png)

대화 상자를 사용 하면 다양 한 서식 파일에 대 한 기본 인증 옵션을 변경할 수 있습니다. 예를 들어, ASP.NET Web Forms 프로젝트를 만들 때 다음 옵션 중 하나로 선택할 수 있습니다.

- 인증 안 함
- 개별 사용자 계정 (ASP.NET 멤버 자격 또는 소셜 공급자 로그인)
- 회사 또는 학교 계정 (인터넷 응용 프로그램에서 Active Directory)
- Windows 인증 (인트라넷 응용 프로그램에서 Active Directory)

![인증 옵션](mvc5/_static/change-authentication-dialog.png)

웹 프로젝트를 만드는 과정에 대 한 자세한 내용은 참조 하세요. [Visual Studio에서 ASP.NET 웹 프로젝트 만들기](../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md)합니다. 인증 옵션에 대 한 자세한 내용은 참조 하세요. [ASP.NET Id](../identity/overview/index.md)합니다.

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET 스 캐 폴딩

ASP.NET 스 캐 폴딩은 ASP.NET 웹 응용 프로그램에 대 한 코드 생성 프레임 워크. 쉽게 데이터 모델과 상호 작용 하는 프로젝트에 상용구 코드를 추가 합니다.

2013 이전 버전의 Visual Studio에서 스 캐 폴딩 ASP.NET MVC 프로젝트 개로 제한 되었습니다. Visual Studio 2013부터 Web Forms를 비롯 한 모든 ASP.NET 프로젝트에 대 한 스 캐 폴딩을 사용할 수 있습니다. Visual Studio 생성 페이지는 Web Forms 프로젝트에 대 한 현재 지원 하지 않습니다 하지만 프로젝트에 MVC 종속성을 추가 하 여 Web forms 스 캐 폴딩을 계속 사용할 수 있습니다. 이후 버전에서 Web Forms에 대 한 페이지를 생성 하는 것에 대 한 지원이 추가 됩니다.

스 캐 폴딩을 사용 하는 경우 모든 종속성이 프로젝트에 설치 되어 필요 합니다. 예를 들어, ASP.NET Web Forms 프로젝트를 시작 하 고 다음 스 캐 폴딩을 사용 하 여 Web API 컨트롤러를 추가할 경우 필요한 NuGet 패키지와 참조를 프로젝트에 자동으로 추가 됩니다.

MVC 스 캐 폴딩에 Web Forms 프로젝트를 추가 하려면 추가 된 **새 스 캐 폴드 된 항목** 선택한 **MVC 5 종속성** 대화 상자에서. 두 가지 옵션이 있습니다; MVC 스 캐 폴딩에 대 한 **최소 종속성** 하 고 **종속성 전체**합니다. 선택 하는 경우 **최소 종속성**, NuGet 패키지 및 ASP.NET MVC에 대 한 참조를 프로젝트에 추가 됩니다. 선택 하는 경우 **종속성 전체**, MVC 프로젝트에 필요한 콘텐츠 파일 뿐만 아니라 최소한의 종속성이 추가 됩니다.

![Visual Studio에서 스 캐 폴드 대화 상자 추가](overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/add-scaffold.png)

Entity Framework 6에서 비동기 기능을 사용 하는 비동기 컨트롤러 스 캐 폴딩에 대 한 지원.

자세한 내용 및 자습서를 참조 하세요 [ASP.NET 스 캐 폴딩 개요](../visual-studio/overview/2013/aspnet-scaffolding-overview.md)합니다.

### <a name="get-help-and-report-issues"></a>도움말 얻기 및 문제 보고

- [알려진된 문제 및 주요 변경 내용 목록](../visual-studio/overview/2013/release-notes.md#knownissues)
- 도움말 및 ASP.NET MVC 5에 설명 된 [포럼](https://forums.asp.net/1146.aspx)
- [ASP.NET MVC 5의 버그를 보고 합니다.](https://github.com/aspnet/AspNetWebStack/issues)
- [기능 요청](http://aspnet.uservoice.com/forums/41201-asp-net-mvc)

### <a name="upgrade-from-aspnet-mvc-4"></a>ASP.NET MVC 4에서에서 업그레이드

참조 [웹 API 프로젝트를 ASP.NET MVC 5 및 Web API 2 및 ASP.NET MVC 4를 업그레이드 하는 방법](overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md)
