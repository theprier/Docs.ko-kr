---
uid: overview
title: ASP.NET 개요 | Microsoft Docs
author: rick-anderson
description: 웹 사이트, 웹 응용 프로그램 및 Web API를 만들 수 있는 무료 프레임워크 ASP.NET을 소개합니다.
ms.assetid: 3a309468-f1ca-4e51-b9c3-536af79d7a8b
ms.author: riande
ms.date: 03/12/2010
ms.technology: aspnet
msc.legacyurl: ''
msc.type: content
ms.openlocfilehash: 5bdebcc226050afc2469840dc4a4dc97ec6b80b2
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41827154"
---
# <a name="aspnet-overview"></a>ASP.NET 개요

ASP.NET은 HTML, CSS 및 JavaScript를 사용하여 유용한 웹 사이트와 웹 응용 프로그램을 작성할 수 있는 무료 웹 프레임워크입니다. Web API를 만들고 웹 소켓 같은 실시간 기술도 사용할 수 있습니다.

[ASP.NET Core](https://docs.microsoft.com/aspnet/core/)는 ASP.NET의 대안입니다.  [ASP.NET 및 ASP.NET Core 중에서 선택](https://docs.microsoft.com/aspnet/core/choose-aspnet-framework)하는 방법을 알아보세요.

## <a name="get-started"></a>시작

[Visual Studio Community 2017](https://www.visualstudio.com/downloads/)는 Windows에서 사용할 수 있는 ASP.NET용 무료 IDE입니다.

## <a name="websites-and-web-applications"></a>웹 사이트 및 웹 응용 프로그램

 ASP.NET은 웹 응용 프로그램을 만들기 위한 세 가지 프레임워크 Web Forms, ASP.NET MVC 및 ASP.NET Web Pages를 제공합니다. 세 프레임워크 모두 안정적이고 완성된 기술이며, 어떤 것을 사용해도 멋진 웹 응용 프로그램을 만들 수 있습니다. 어떤 프레임워크를 선택하더라도 어디서나 ASP.NET의 장점과 기능을 모두 누릴 수 있습니다.

각 프레임워크는 서로 다른 개발 스타일을 대상으로 합니다. 어떤 프레임워크를 선택해야 하는지는 프로그래밍 자산(지식, 기술 및 개발 경험), 만들려는 응용 프로그램 종류, 익숙한 개발 방식에 따라 달라집니다.

아래는 각 프레임워크의 개요와 프레임워크 선택 요령입니다. 비디오를 선호하는 경우 [ASP.NET으로 웹 사이트 만들기](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/Making-Websites-with-ASPNET) 및 [웹 도구란?](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/what-is-web-tools)을 참조하세요.

|   | 다음 분야에 대한 경험이 있는 경우 | 개발 스타일 | 전문 지식 | 
|-----------|----------------------|-----------------------------------------------------|----------------|
| Web Forms | Win Forms, WPF, .NET | HTML 표시를 캡슐화하는 풍부한 컨트롤 라이브러리를 사용하여 신속하게 개발 | 중간 수준, 고급 RAD |
| MVC       | Ruby on Rails, .NET  | HTML 표시를 완벽하게 제어할 수 있고, 코드와 표시가 분리되고, 테스트를 쉽게 작성할 수 있습니다. 모바일 및 단일 페이지 응용 프로그램(SPA)에 적합합니다. | 중간 수준, 고급 |
| 웹 페이지  | 클래식 ASP, PHP     | HTML 표시와 코드가 같은 파일에 있습니다. | 최신, 중간 수준 |

### <a name="web-forms"></a>Web Forms

ASP.NET Web Forms를 사용하면 익숙한 끌어서 놓기, 이벤트 중심 모델을 사용하여 동적 웹 사이트를 빌드할 수 있습니다. 디자인 화면과 수백 개의 컨트롤 및 구성 요소를 통해 데이터 액세스를 지원하는 정교하고 강력한 UI 중심 사이트를 신속하게 빌드할 수 있습니다. 

[Web Forms에 대한 자세한 정보](web-forms/index.md)

### <a name="mvc"></a>MVC

즐겁고, 민첩한 개발을 위해 전체 제어 태그를 제공하여 명확한 영역 분리를 사용할 수 있는 동적 웹 사이트를 만들도록 강력한 패턴 기반의 방법인 ASP.NET MVC를 사용합니다. ASP.NET MVC에는 최신 웹 표준을 사용하는 정교한 응용 프로그램을 만들기 위한 TDD 친화적 개발을 지원하는 여러 기능이 포함되어 있습니다. 

[MVC에 대한 자세한 정보](mvc/index.md)

### <a name="aspnet-web-pages"></a>ASP.NET 웹 페이지

ASP.NET Web Pages 및 Razor 구문은 서버 코드를 HTML과 결합하여 동적 웹 콘텐츠를 만들 수 있는 빠르고 간단하며 사용하기 쉬운 방식을 제공합니다. 데이터베이스에 연결하고, 비디오를 추가하고, 소셜 네트워킹 사이트에 연결하고, 최신 웹 표준을 따르는 아름다운 사이트를 만들 수 있는 여러 기능을 포함하세요.

[Web Pages에 대한 자세한 정보](web-pages/index.md)

### <a name="notes-about-web-forms-mvc-and-web-pages"></a>Web Forms, MVC 및 Web Pages에 대한 참고 사항

세 ASP.NET 프레임워크는 모두 .NET Framework를 기반으로 하고 .NET 및 ASP.NET의 핵심 기능을 공유합니다. 예를 들어 세 프레임워크 모두 멤버 자격 기반의 로그인 보안 모델을 제공하며, 요청을 관리하고 세션을 처리하기 위한 시설과 그 밖의 핵심 ASP.NET 기능을 공유합니다.

뿐만 아니라 세 프레임워크가 완전히 독립적인 것은 아니기 때문에 한 프레임워크를 선택한다고 해서 나머지 두 프레임워크를 사용할 수 없는 것은 아닙니다. 여러 프레임워크가 동일한 웹 응용 프로그램에서 공존할 수 있으므로 응용 프로그램의 개별 구성 요소가 서로 다른 프레임워크를 사용하여 작성된 것을 어렵지 않게 볼 수 있습니다. 예를 들어 앱에서 고객 응대 부분은 MVC에서 개발하여 표시를 최적화하고, 데이터 및 관리 부분은 Web Forms로 개발하여 데이터 제어 및 간단한 데이터 액세스를 활용할 수 있습니다.

## <a name="web-apis"></a>Web API

ASP.NET Web API는 브라우저 및 모바일 장치를 비롯한 광범위한 클라이언트에 연결하는 HTTP 서비스를 쉽게 빌드할 수 있게 해 주는 프레임워크입니다. ASP.NET Web API는 .NET Framework에서 RESTful 응용 프로그램을 빌드하는 데 이상적인 플랫폼입니다.

[Web API에 대한 자세한 정보](web-api/index.md)

<!-- Put first under Web API TOC:  Watch video (9 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/services-and-aspnet -->

## <a name="real-time-technologies"></a>실시간 기술

ASP.NET SignalR은 실시간 웹 기능을 좀 더 쉽게 개발할 수 있도록 도와주는 새로운 ASP.NET 개발자용 라이브러리입니다. SignalR을 사용하면 서버와 클라이언트 간에 양방향 통신이 가능합니다. 클라이언트를 사용할 수 있게 되면 서버는 그 즉시 연결된 클라이언트로 콘텐츠를 푸시할 수 있습니다. SignalR은 웹 소켓을 지원하며, 이전 버전의 브라우저와 호환되는 다른 기술로 대체합니다. SignalR은 연결 관리(예: 이벤트 연결 및 연결 끊기), 연결 그룹화 및 권한 부여를 위한 API를 제공합니다.

[SignalR에 대한 자세한 정보](signalr/index.md)

<!-- Put first under SignalR TOC:  Watch video (6 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/signalr-and-the-real-time-web -->

## <a name="mobile-apps-and-sites"></a>모바일 앱 및 사이트 

ASP.NET은 Web API 백 엔드로 네이티브 모바일 앱을 활용할 수 있을 뿐 아니라 Twitter Bootstrap 같은 반응형 디자인 프레임워크를 사용하여 모바일 웹 사이트를 만들 수 있습니다. 네이티브 모바일 앱을 빌드하는 경우 데이터 액세스, 인증, 앱의 푸시 알림을 처리하는 JSON 기반 Web API를 손쉽게 만들 수 있습니다. 반응형 모바일 사이트를 빌드하는 경우 선호하는 CSS 프레임워크 또는 오픈 그리드 시스템을 사용해도 되고, jQuery Mobile 또는 Sencha 같은 강력한 모바일 시스템과 PhoneGap 같은 뛰어난 모바일 응용 프로그램을 선택해도 됩니다.

[모바일 앱 및 사이트 개발에 대한 자세한 정보](mobile/index.md)

<!-- Put first under mobile TOC:  Watch video (11 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/aspnet-and-mobile -->

## <a name="single-page-applications"></a>단일 페이지 응용 프로그램 

ASP.NET SPA(단일 페이지 응용 프로그램)는 HTML 5, CSS 3 및 JavaScript를 사용하여 중요한 클라이언트 쪽 상호 작용을 포함하는 응용 프로그램을 빌드할 수 있도록 도와줍니다. Visual Studio에는 knockout.js 및 ASP.NET Web API를 사용하여 단일 페이지 응용 프로그램을 구축할 수 있는 템플릿이 포함되어 있습니다. 기본 제공 SPA 템플릿 외에도 커뮤니티에서 만든 SPA 템플릿을 다운로드할 수 있습니다.

[단일 페이지 앱 개발에 대한 자세한 정보](single-page-application/index.md)

## <a name="webhooks"></a>웹후크

WebHook는 Web API와 SaaS 서비스를 연결하는 간단한 pub/sub 모델을 제공하는 가벼운 HTTP 패턴입니다. 서비스에서 이벤트가 발생하면 등록된 구독자에게 HTTP POST 요청의 형태로 알림이 전송됩니다. POST 요청에는 수신자가 적절하게 대처할 수 있도록 이벤트에 대한 정보를 포함되어 있습니다.

Dropbox, GitHub, Instagram, MailChimp, PayPal, Slack, Trello를 포함한 여러 서비스에 WebHook가 노출됩니다. 예를 들어 WebHook는 Dropbox에서 파일이 변경되었거나, GitHub에서 코드가 변경되었거나, PayPal에서 대금 결제가 시작되었거나, Trello에서 카드가 생성되었음을 나타낼 수 있습니다.

[WebHook에 대한 자세한 정보](webhooks/index.md)





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
