---
uid: overview
title: ASP.NET 개요 | Microsoft Docs
author: rick-anderson
description: ASP.NET, 웹 사이트, 웹 응용 프로그램 및 web Api 만들기 위한 무료 프레임 워크에 소개 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/12/2010
ms.topic: article
ms.assetid: 3a309468-f1ca-4e51-b9c3-536af79d7a8b
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: ''
msc.type: content
ms.openlocfilehash: 0ba7814d4004b17e678eab9a2a41a6d6f34773e1
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2018
---
# <a name="aspnet-overview"></a>ASP.NET 개요

ASP.NET은 뛰어난 웹 사이트 및 HTML, CSS 및 JavaScript를 사용 하 여 웹 응용 프로그램을 구축 하기 위한 무료 웹 프레임 워크입니다. 웹 Api을 만들고 웹 소켓 같은 실시간 기술을 사용할 수도 있습니다.

[ASP.NET Core](https://docs.microsoft.com/aspnet/core/) ASP.NET 하지 않아도 됩니다.  참조는 [ASP.NET 및 ASP.NET Core 선택 하는 방법에 대 한 지침](https://docs.microsoft.com/aspnet/core/choose-aspnet-framework)합니다.

## <a name="get-started"></a>시작

[Visual Studio 커뮤니티 2017](https://www.visualstudio.com/downloads/), Windows에서 ASP.NET에 대 한 IDE를 해제 합니다.

## <a name="websites-and-web-applications"></a>웹 사이트 및 웹 응용 프로그램

 ASP.NET은 웹 응용 프로그램을 만들기 위한 세 가지 프레임 워크를 제공: Web Forms, ASP.NET MVC 및 ASP.NET 웹 페이지입니다. 모든 세 가지 프레임 워크 안정적이 고 발달 되며 그 중 하나에 있는 뛰어난 웹 응용 프로그램을 만들 수 있습니다. 선택 하면 어떤 프레임 워크에 관계 없이 모든 장점과 ASP.NET everywhere 기능 받아볼 수 있습니다.

각 프레임 워크에 다양 한 개발 스타일을 대상 으로합니다. 선택한 하나 익숙해지면 개발 접근 방식 및 응용 프로그램을 만드는의 유형, 프로그래밍 자산 (기술 자료, 기술 및 개발 환경)의 조합에 따라 달라 집니다.

다음은 각 프레임 워크가 및 선택 하는 방법에 대 한 몇 가지 아이디어의 개요입니다. 한 비디오 소개를 선호 하는 경우 참조 [asp.net 웹 사이트 만들기](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/Making-Websites-with-ASPNET) 및 [웹 도구 란?](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/what-is-web-tools)

|   | 환경에 있는 경우 | 개발 스타일 | 전문 지식 | 
|-----------|----------------------|-----------------------------------------------------|----------------|
| Web Forms | Win Forms, WPF, .NET | HTML 태그를 캡슐화 하는 컨트롤의 풍부한 라이브러리를 사용 하 여 신속 하 게 개발 | 표준은 중간 수준의 고급 RAD |
| MVC       | 레일에.NET에 ruby  | HTML 태그, 코드 및 태그, 분리 되 고 테스트를 작성 하기가 대 한 모든 권한을 합니다. 모바일 및 단일 페이지 응용 프로그램 (SPA)에 적합 합니다. | 표준은 중간 수준의 고급 |
| 웹 페이지  | 클래식 ASP, PHP     | HTML 태그와 같은 파일에 함께 코드 | 새, 중간 수준 |

### <a name="web-forms"></a>Web Forms

ASP.NET Web Forms 친숙 한 끌어서 놓기, 이벤트 기반 모델을 사용 하 여 동적 웹 사이트를 작성할 수 있습니다. 디자인 화면과 수백 개의 컨트롤 및 구성 요소를 통해 빠르게 정교 하 고 강력한 UI 기반의 사이트 데이터 액세스를 작성할 수 있습니다. 

[Web Forms에 대 한 자세한 정보](web-forms/index.md)

### <a name="mvc"></a>MVC

ASP.NET MVC 문제의 확실히 구분할 수 있도록 제공 하 고,는 태그를 완전히 제어할 기반의 방법을 제공에 대 한 동적 웹 사이트를 구축 하는 강력한 패턴 기반의 방법을 제공 합니다. ASP.NET MVC에는 최신 웹 표준을 사용 하는 복잡 한 응용 프로그램을 만들기 위한 개발을 신속 하 고 사용이 가능 하 게 수 있는 여러 기능이 포함 되어 있습니다. 

[MVC에 대 한 자세한 정보](mvc/index.md)

### <a name="aspnet-web-pages"></a>ASP.NET 웹 페이지

ASP.NET 웹 페이지 및 Razor 구문 html 동적 웹 콘텐츠를 만들려는 서버 코드를 결합 하는 빠르고 쉬우며 간편한 방법을 제공 합니다. 데이터베이스에 연결, 비디오를 추가 하 고, 소셜 네트워킹 사이트에 연결 하 고 많은 포함 최신 웹 표준을 준수 하는 보기 좋은 사이트를 만들 수 있는 더 많은 기능입니다.

[웹 페이지에 대 한 자세한 정보](web-pages/index.md)

### <a name="notes-about-web-forms-mvc-and-web-pages"></a>Web Forms, MVC 및 웹 페이지에 대 한 참고 사항

모든 세 가지 ASP.NET 프레임 워크는.NET Framework를 기반으로 하 고 ASP.NET 및.NET의 핵심 기능을 공유 합니다. 예를 들어 모든 세 가지 프레임 워크를 기반으로 멤버 자격, 로그인 보안 모델을 제공 하 고 세 가지 모두 핵심 기능 ASP.NET의 일부인 요청, 처리 세션을 관리 하기 위한 동일한 기능을 공유 합니다.

그리고 세 개의 프레임 워크가 완전히 독립적 하나를 선택 해도 다른를 사용 하 여 방해 하지 않는 합니다. 프레임 워크는 동일한 웹 응용 프로그램에서 공존할 수 있으므로 서로 다른 프레임 워크를 사용 하 여 작성 된 응용 프로그램의 개별 구성 요소를 볼 수는 일반적이 지 않습니다. 예를 들어 Web Forms 컨트롤 데이터 및 단순 데이터 액세스를 활용 하도록 데이터 액세스 및 관리 부분은 모두 개발 하는 동안에 태그를 최적화 하기 위해 mvc에서 응용 프로그램의 고객 관련 부분을 개발할 수 있습니다.

## <a name="web-apis"></a>Web API

ASP.NET Web API는 다양 한 브라우저 및 모바일 장치를 포함 한 클라이언트를 연결할 HTTP 서비스를 작성을 용이 하 게 하는 프레임 워크입니다. ASP.NET Web API는 .NET Framework에서 RESTful 응용 프로그램을 빌드하는 데 이상적인 플랫폼입니다.

[웹 API에 대 한 자세한 정보](web-api/index.md)

<!-- Put first under Web API TOC:  Watch video (9 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/services-and-aspnet -->

## <a name="real-time-technologies"></a>실시간 기술

ASP.NET SignalR은 ASP.NET 개발자를 위한 개발 실시간 웹 기능을 더 쉽게 하는 새 라이브러리. SignalR 서버와 클라이언트 간의 양방향 통신을 허용 합니다. 서버를 사용할 수 있게 되 면 즉시 연결 된 클라이언트에 콘텐츠 푸시할 수 있습니다. SignalR은 Websocket을 지원 및 이전 버전의 브라우저에 대 한 호환 다른 방법으로 대체 합니다. SignalR 연결 관리에 대 한 Api가 포함 됩니다 (예를 들어, 연결 및 연결 끊기 이벤트), 연결 그룹화 및 권한 부여 합니다.

[SignalR에 대 한 자세한 정보](signalr/index.md)

<!-- Put first under SignalR TOC:  Watch video (6 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/signalr-and-the-real-time-web -->

## <a name="mobile-apps-and-sites"></a>모바일 응용 프로그램 및 사이트 

ASP.NET 웹 API 백 엔드 뿐만 아니라 부트스트랩 Twitter와 같은 한 반응 형 디자인 프레임 워크를 사용 하 여 모바일 웹 사이트는 네이티브 모바일 앱을 활용할 수 있습니다. 기본 모바일 앱을 작성 하는 경우 핸들 데이터 액세스, 인증 및 응용 프로그램에서 푸시 알림을 JSON 기반 웹 API를 만드는 것이 쉽습니다. 반응 형 모바일 사이트를 작성 하는 경우 모든 CSS 프레임 워크 또는 jQuery Mobile 또는 Sencha 및 PhoneGap으로 뛰어난 모바일 응용 프로그램 같은 강력한 모바일 시스템을 선택 하거나 원하는 하면 열기 그리드 시스템을 사용할 수 있습니다.

[모바일 응용 프로그램 및 사이트 개발에 대 한 자세한 정보](mobile/index.md)

<!-- Put first under mobile TOC:  Watch video (11 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/aspnet-and-mobile -->

## <a name="single-page-applications"></a>단일 페이지 응용 프로그램 

ASP.NET 단일 페이지 응용 프로그램 (SPA)를 사용 하면 HTML 5, CSS 3 및 JavaScript를 사용 하 여 중요 한 클라이언트 쪽 상호 작용을 포함 하는 응용 프로그램을 빌드할 수 있습니다. Visual Studio knockout.js 및 ASP.NET Web API를 사용 하 여 단일 페이지 응용 프로그램을 구축 하기 위한 서식 파일을 포함 합니다. 기본 제공 SPA 템플릿 외에도 커뮤니티에서 만든 SPA 템플릿은 다운로드할 수 있습니다.

[단일 페이지 응용 프로그램 개발에 대 한 자세한 정보](single-page-application/index.md)

## <a name="webhooks"></a>웹후크

또한 Webhook 배선 함께 웹 Api 및 SaaS 서비스에 대 한 간단한 pub/sub 모델을 제공 하는 간단한 HTTP 패턴입니다. 서비스에는 이벤트가 발생 하면 등록 된 구독자에 HTTP POST 요청의 형태로 알림이 보내집니다. POST 요청의 수신자 문제에 대 한 가능 하 게 하는 이벤트에 대 한 정보를 포함 합니다.

또한 Webhook는 많은 수의 Dropbox, GitHub, Instagram, MailChimp, PayPal, 여유 시간, Trello, 및 등을 포함 하 여 서비스에 의해 노출 됩니다. 예를 들어 여 webhook을 사용할지 의미할 수 있습니다 Dropbox 등의 파일이 변경 또는 GitHub에서 코드 변경이 커밋 또는 지불 PayPal에서 시작 되었습니다 Trello에서 카드를 만들지 않았습니다.

[또한 Webhook에 대 한 자세한 정보](webhooks/index.md)





<!--
Create Deployment TOC based on https://www.asp.net/aspnet/overview/deployment
Copy deployment content map to MVC, WebForms, Web Pages, Web API sections.
Copy Web Deployment in Enterprise from WebForms to MVC
Move under ASP.NET Best practices
    What not to do in ASP.NET, and what to do instead https://review.docs.microsoft.cus/aspnet/aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
    Async and await https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/async-and-await
    Building Real World Cloud Apps with Azure https://review.docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
    Hands on Lab: Maintainable Azure Websites: Managing Change and Scale https://review.docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale

-->
