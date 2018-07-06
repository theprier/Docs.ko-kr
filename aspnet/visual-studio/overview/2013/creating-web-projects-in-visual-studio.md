---
uid: visual-studio/overview/2013/creating-web-projects-in-visual-studio
title: Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기 | Microsoft Docs
author: tdykstra
description: 이 항목에서는 Visual Studio 2013 업데이트 3 여기에서 ASP.NET 웹 프로젝트를 만들기 위한 옵션은 웹 개발 c에 대 한 새로운 기능 중 일부를 설명 하는 중...
ms.author: aspnetcontent
ms.date: 12/01/2014
ms.assetid: 61941e64-0c0d-4996-9270-cb8ccfd0cabc
msc.legacyurl: /visual-studio/overview/2013/creating-web-projects-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: b57492a51f65e7ca861a7c354ded6ab170a92488
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37814522"
---
<a name="creating-aspnet-web-projects-in-visual-studio-2013"></a>Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기
====================
[Tom Dykstra](https://github.com/tdykstra)

> 이 항목에서는 Visual Studio 2013 업데이트 3에서에서 ASP.NET 웹 프로젝트를 만드는 옵션을 설명 합니다.
> 
> 다음은 몇 가지 Visual Studio의 이전 버전에 비해 웹 개발을 위한 새로운 기능:
> 
> - 만들기 위한 간단한 UI를 제공 하는 프로젝트 [여러 ASP.NET 프레임 워크에 대 한 지원](#add) (Web Forms, MVC 및 Web API).
> - [ASP.NET Id](#indauth), 웹 호스팅 IIS 외에 소프트웨어를 사용 하 여 모든 ASP.NET 프레임 워크와에서 동일 하 게 작동 하는 새로운 ASP.NET 멤버 자격 시스템입니다.
> - 사용 [부트스트랩](#bootstrap) 응답성이 뛰어난 디자인 및 테마 기능을 제공 합니다.
> - 와 같은 MVC 용 으로만 제공 하는 데 사용 하는 Web Forms에 대 한 새로운 기능 [자동 테스트 프로젝트 만들기](#testproj) 와 [인트라넷 사이트 템플릿](#winauth)합니다.
> 
> Azure Cloud Services 또는 Azure Mobile Services에 대 한 웹 프로젝트를 만드는 방법에 대 한 자세한 내용은 [Azure Cloud Services 및 ASP.NET 시작](https://azure.microsoft.com/documentation/articles/cloud-services-dotnet-get-started/) 고 [Azure Mobile Services.NET을 사용 하 여 Leaderboard 앱 만들기 백 엔드](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)합니다.


<a id="prerequisites"></a>
## <a name="prerequisites"></a>전제 조건

이 문서에 적용 됩니다 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) 사용 하 여 [업데이트 3](https://go.microsoft.com/fwlink/?linkid=397827&amp;clcid=0x409) 설치 합니다.

<a id="wap"></a>
## <a name="web-application-projects-versus-web-site-projects"></a>웹 응용 프로그램 프로젝트와 웹 사이트 프로젝트 비교

ASP.NET을 사용 하면 두 종류의 웹 프로젝트 중 하나를 선택 합니다. *웹 응용 프로그램 프로젝트* 및 *웹 사이트 프로젝트*합니다. 새로운 개발에 웹 응용 프로그램 프로젝트 및이 문서에서는 웹 응용 프로그램 프로젝트에만 적용 됩니다. 자세한 내용은 [웹 응용 프로그램 프로젝트와 Visual Studio에서 웹 사이트 프로젝트 비교](https://msdn.microsoft.com/library/dd547590(v=vs.120).aspx) MSDN 사이트입니다.

<a id="overview"></a>
## <a name="overview-of-web-application-project-creation"></a>웹 응용 프로그램 프로젝트 만들기 개요

다음 단계를 웹 프로젝트를 만드는 방법을 보여 줍니다.

1. 클릭 **새 프로젝트** 에 **시작** 페이지 또는 합니다 **파일** 메뉴.
2. 에 **새 프로젝트** 대화 상자에서 클릭 **웹** 왼쪽된 창에서와 **ASP.NET 웹 응용 프로그램** 가운데 창에서.

    ![새 프로젝트 대화 상자](creating-web-projects-in-visual-studio/_static/image1.png)

    선택할 수 있습니다 **클라우드** 만들려면 왼쪽된 창에는 [Azure 클라우드 서비스](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy), [Azure 모바일 서비스](https://msdn.microsoft.com/library/windows/apps/dn629482.aspx), 또는 [Azure WebJob](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-webjobs)합니다. 이 항목에서는 이러한 서식 파일을 다루지 않습니다.
3. 오른쪽 창에서을 클릭 합니다 **프로젝트에 Application Insights 추가** 확인란 상태와 응용 프로그램에 대 한 사용 현황 모니터링 하려는 경우. 자세한 내용은 [웹 응용 프로그램의 성능 모니터링](https://azure.microsoft.com/documentation/articles/app-insights-web-monitor-performance/)합니다.
4. 프로젝트를 지정 **이름을**를 **위치**, 기타 옵션 및 클릭 **확인**합니다.

    합니다 **새 ASP.NET 프로젝트** 대화 상자가 나타납니다.

    ![새 프로젝트 대화 상자](creating-web-projects-in-visual-studio/_static/image2.png)
5. 템플릿을 클릭 합니다.

    ![템플릿 선택](creating-web-projects-in-visual-studio/_static/image3.png)
6. 서식 파일에 포함 되지 않습니다 추가 프레임 워크에 대 한 지원을 추가 하려는 경우에 적절 한 확인란을 클릭 합니다. (예제에서는에 추가할 수 있습니다/MVC 또는 Web API Web Forms 프로젝트에.)

    ![프레임 워크를 추가 합니다.](creating-web-projects-in-visual-studio/_static/image4.png)
7. <a id="testproj"></a>단위 테스트 프로젝트를 추가 하려면 클릭 **단위 테스트 추가**합니다.

    ![단위 테스트를 추가 합니다.](creating-web-projects-in-visual-studio/_static/image5.png)
8. 기본적으로 템플릿을 제공 하는 것 보다는 다른 인증 방법, 클릭 **인증 변경**합니다.

    ![인증 단추 구성](creating-web-projects-in-visual-studio/_static/image6.png)

    ![인증 대화 상자를 구성 합니다.](creating-web-projects-in-visual-studio/_static/image7.png)

<a id="azurenewproj"></a>
### <a name="create-a-web-app-or-virtual-machine-in-azure"></a>Azure에서 웹 앱 또는 가상 머신 만들기

Visual Studio는 웹 응용 프로그램 호스팅에 대 한 Azure 서비스를 사용할 수 있도록 하는 기능이 포함 되어 있습니다. 예를 들어, Visual Studio IDE에서 바로 다음을 수행할 수 있습니다.

- 웹 앱 또는 인터넷을 통해 응용 프로그램을 사용할 수 있도록 하는 가상 컴퓨터를 만들고 설정 합니다.
- 클라우드에서 실행 될 때 응용 프로그램에서 생성 된 로그를 봅니다.
- 디버그 모드에서 원격으로 실행할 응용 프로그램이 클라우드에서 실행 되는 동안.
- Viiew 및 SQL 데이터베이스와 같은 다른 Azure 서비스를 관리 합니다.

할 수 있습니다 [Azure 계정 만들기](https://www.windowsazure.com/pricing/free-trial/) 웹 앱과 같은 기본 서비스를 무료로 포함 하 고 MSDN 구독자 인 경우 다음을 할 수 있습니다 [혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/visual-studio-subscriptions/) 추가 azure 월간 크레딧을 제공 하는 서비스입니다. 

기본적으로는 **새 ASP.NET 프로젝트** 대화 상자를 사용 하면 웹 앱 또는 새 웹 프로젝트에 대 한 가상 컴퓨터를 만들 수 있습니다. 새 웹 앱 또는 가상 머신을 만드는 하지 않으려는 경우 선택을 취소 합니다 **클라우드에서 호스트** 확인란 합니다.

![원격 리소스 만들기](creating-web-projects-in-visual-studio/_static/image8.png)

확인 상자 캡션 될 수 있습니다 **클라우드에서 호스트** 또는 **원격 리소스 만들기**, 두 경우 모두 결과 동일 합니다. 확인란을 선택한 상태로 두면 기본적으로 웹 앱을 Azure App Service에서 만든 Visual Studio입니다. 로 변경 하려면 드롭다운 목록 상자를 사용할 수는 **가상 머신** 하려는 경우. Azure에 로그인 되어 있지는 Azure 자격 증명을 묻는 메시지가 나타납니다. 로그인 한 후 대화 상자를 사용 하면 Visual Studio가 프로젝트에 대해 만들 리소스를 구성 하려면 있습니다. 다음 그림에서는 웹 앱에 대 한 대화 상자를 표시합니다. 다른 옵션에는 가상 머신을 만들도록 선택한 경우 표시 됩니다.

![Azure 앱 설정 구성](creating-web-projects-in-visual-studio/_static/image9.png)

이 프로세스를 사용 하 여 Azure 리소스를 만드는 방법에 대 한 자세한 내용은 참조 하세요. [Azure 및 ASP.NET 시작](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet) 하 고 [Visual Studio를 사용 하 여 웹 사이트에 대 한 가상 머신을 만드는](https://azure.microsoft.com/documentation/articles/virtual-machines-dotnet-create-visual-studio-powershell/)합니다.

이 문서의 나머지 부분은 사용 가능한 템플릿 및 해당 옵션에 대 한 자세한 정보를 제공합니다. 문서에는 템플릿에 사용 하는 부트스트랩, 레이아웃 및 테마 프레임 워크도 소개 합니다.

<a id="vs2013"></a>
## <a name="visual-studio-2013-web-project-templates"></a>Visual Studio 2013 웹 프로젝트 템플릿

Visual Studio 웹 프로젝트를 만드는 템플릿을 사용 합니다. 프로젝트 템플릿으로 새 프로젝트에서 파일 및 폴더를 만들 수 있습니다, 그리고 NuGet 패키지를 설치 및 기본적인 응용 프로그램에 대 한 예제 코드를 제공 합니다. 최신 웹 표준을 구현 하 고 점프 하면 뿐만 아니라 ASP.NET 기술을 사용 하는 방법에 대 한 모범 사례 시작 사용자 고유의 응용 프로그램을 만드는 방법에 설명 하고자 하는 템플릿.

Visual Studio 2013 이상 버전의.NET framework 또는.NET 4.5를 대상으로 하는 프로젝트에 대 한 웹 프로젝트 템플릿에 대 한 다음 중 하나를 제공 합니다.

- [빈 템플릿](#empty)
- [웹 양식 서식 파일](#wf)
- [MVC 템플릿](#mvc)
- [Web API 템플릿](#webapi)
- [단일 페이지 응용 프로그램 템플릿](#spa)
- [Azure 모바일 서비스 템플릿](https://azure.microsoft.com/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)
- [Visual Studio 2012 템플릿](#vs2012)

제공 하는 Visual Studio 확장을 설치할 수도 있습니다는 [Facebook 템플릿](#facebook)합니다.

.NET 4를 대상으로 하는 프로젝트를 만드는 방법에 대 한 자세한 내용은 [Visual Studio 2012 템플릿](#vs2012) 이 항목의에서 뒷부분에 있습니다.

모바일 클라이언트에 대 한 ASP.NET 응용 프로그램을 만드는 방법에 대 한 자세한 내용은 [asp.net에서 모바일 지원](../../../mobile/index.md)합니다.

<a id="empty"></a>
### <a name="empty-template"></a>빈 템플릿

빈 템플릿에 제공 완전 최소 폴더와 같은 프로젝트 파일을 ASP.NET 웹 앱에 대 한 파일 (*.csproj* 또는. *vbproj*) 및 *Web.config* 파일입니다. 아래에 있는 확인란을 사용 하 여 Web Forms, MVC 및/또는 Web API에 대 한 지원을 추가할 수 있습니다 합니다 **폴더를 추가 하 고에 대 한 참조를 핵심:** 레이블.

빈 템플릿에 대해 없음 인증 옵션이 제공 됩니다. 샘플 응용 프로그램에 인증 기능이 구현 되었으면 하 고 빈 템플릿 샘플 응용 프로그램을 만들지 않습니다.

<a id="wf"></a>
### <a name="web-forms-template"></a>웹 양식 서식 파일

프레임 워크는 다양 한 UI 및 데이터는 웹 사이트를 구축 하는 신속 하 게 수 있는 다음 기능을 제공 하는 Web Forms 기능에 액세스 합니다.

- Visual Studio에서 WYSIWYG 디자이너입니다.
- HTML 및 속성 및 스타일을 설정 하 여 사용자 지정할 수 있는 렌더링 하는 서버 컨트롤입니다.
- 풍부한 데이터 액세스 및 데이터 표시에 대 한 제어 합니다.
- WPF와 같은 클라이언트 응용 프로그램을 프로그래밍 하는 같은 프로그래밍할 수 있는 이벤트를 노출 하는 이벤트 모델입니다.
- HTTP 요청 간에 상태 (데이터)의 자동 보존 합니다.

일반적으로 Web Forms 응용 프로그램을 만드는 ASP.NET MVC 프레임 워크를 사용 하 여 동일한 응용 프로그램을 만드는 것 보다 적은 프로그래밍 노력에 필요 합니다. 그러나 Web Forms 신속한 응용 프로그램 개발에 대해서만 아닙니다. 많은 복잡 한 상용 응용 프로그램 및 프레임 워크 Web Forms 기반으로 구축 됩니다.

Web Forms 페이지와 페이지의 컨트롤이 자동으로 브라우저에 보내지는 태그의 대부분을 생성, ASP.NET MVC에서 제공 하는 HTML에 대 한 세분화 된 제어 종류가 필요는 없습니다. 페이지 및 컨트롤을 구성 하기 위한 선언적 모델을 작성 해야 하지만 HTML 및 HTTP 동작의 일부 코드의 양을 최소화 합니다. 예를 들어 항상 수 없는 변경 내용을 컨트롤에 의해 생성 될 수 있습니다 정확 하 게 지정할 수 있습니다.

Web Forms framework가 제공 되지 않습니다 자체 ASP.NET MVC로 쉽게 패턴 기반 개발 사례와 같은 [테스트 기반 개발](http://en.wikipedia.org/wiki/Test-driven_development)하십시오 [중요 한 부분의 분리](http://en.wikipedia.org/wiki/Separation_of_concerns), [반전 컨트롤](http://en.wikipedia.org/wiki/Inversion_of_control), 및 [종속성 주입](http://en.wikipedia.org/wiki/Dependency_injection)합니다. 이런 방식으로 팩터링 한 코드를 작성 하려는 경우에 다음을 할 수 있습니다. ASP.NET MVC 프레임 워크 이므로 자동는 방금 없습니다. 합니다 [ASP.NET Web Forms MVP](http://webformsmvp.com/) 프로젝트 영역 분리 및 테스트 용이성 하면서도 Web Forms 전달할 빌드된 신속한 개발을 용이 하 게 하는 방법을 보여 줍니다. Microsoft SharePoint는 Web Forms MVP를 기반으로 합니다.

Web Forms 템플릿을 사용 하는 샘플 Web Forms 응용 프로그램을 만듭니다 [부트스트랩](#bootstrap) 에서 응답성이 뛰어난 디자인 및 테마 기능을 제공 합니다. 다음 그림은 홈 페이지를 보여 줍니다.

![Web Forms 템플릿 앱 홈 페이지](creating-web-projects-in-visual-studio/_static/image10.png)

Web Forms에 대 한 자세한 내용은 참조 하세요. [ASP.NET Web Forms](https://asp.net/web-forms)합니다. Web Forms 템플릿을을 수행 하는 방법에 대 한 내용은 [Visual Studio 2013을 사용 하 여 기본적인 Web Forms 응용 프로그램을 빌드하기](https://blogs.msdn.com/b/webdev/archive/2013/12/19/building-a-basic-web-forms-application-using-visual-studio-2013.aspx)합니다.

<a id="mvc"></a>
### <a name="mvc-template"></a>MVC 템플릿

ASP.NET MVC와 같은 패턴 기반 개발을 용이 하 게 설계 되었습니다 [테스트 기반 개발](http://en.wikipedia.org/wiki/Test-driven_development), [중요 한 부분의 분리](http://en.wikipedia.org/wiki/Separation_of_concerns)하십시오 [제어 반전](http://en.wikipedia.org/wiki/Inversion_of_control), 및 [종속성 주입](http://en.wikipedia.org/wiki/Dependency_injection)합니다. 프레임 워크는 프레젠테이션 계층에서 웹 응용 프로그램의 비즈니스 논리 레이어 구분을 권장 합니다. 응용 프로그램 모델 (M), (V), 뷰 및 컨트롤러 (C)로 나누어 ASP.NET MVC 대규모 응용 프로그램의 복잡성을 관리 하는 일을 쉽게 확인 합니다.

ASP.NET MVC를 사용 하 여 HTML 및 Web Forms에서 보다 HTTP 보다 직접적으로 작동 합니다. 예를 들어, Web Forms HTTP 요청 간에 상태를 자동으로 유지할 수 있습니다 하지만 MVC에서 명시적으로 코드를 해야 합니다. MVC 모델의 장점은 정확 하 게 응용 프로그램이 수행 하 고 웹 환경에서 작동 하는 방법을 통해 완전히 제어할 수 있도록 한다는 점입니다. 단점은 더 많은 코드를 작성 해야 한다는 점입니다.

MVC는 power 개발자의 프레임 워크 응용 프로그램 요구에 맞게 사용자 지정 하는 기능을 제공 하는 확장할 수 있도록 설계 되었습니다. 또한 ASP.NET MVC 소스 코드는 OSI 라이선스를 사용할 수 있습니다.

MVC 템플릿을 사용 하는 샘플 MVC 5 응용 프로그램을 만듭니다 [부트스트랩](#bootstrap) 에서 응답성이 뛰어난 디자인 및 테마 기능을 제공 합니다. 다음 그림은 홈 페이지를 보여 줍니다.

![MVC 샘플 응용 프로그램](creating-web-projects-in-visual-studio/_static/image11.png)

MVC에 대 한 자세한 내용은 참조 하세요. [ASP.NET MVC](https://asp.net/mvc)합니다. MVC 4 템플릿을 선택 하는 방법에 대 한 정보를 참조 하세요 [Visual Studio 2012 템플릿](#vs2012) 이 문서의 뒷부분에 나오는.

<a id="webapi"></a>
### <a name="web-api-template"></a>Web API 템플릿

Web API 템플릿에서 MVC를 기반으로 하는 API 도움말 페이지를 포함 하 여 Web API에 따라 샘플 웹 서비스를 만듭니다.

ASP.NET Web API는 브라우저 및 모바일 장치를 비롯한 광범위한 클라이언트에 연결하는 HTTP 서비스를 쉽게 빌드할 수 있게 해 주는 프레임워크입니다. ASP.NET Web API는.NET Framework에 RESTful 서비스를 빌드하기 위한 이상적인 플랫폼입니다.

Web API 템플릿에서 샘플 웹 서비스를 만듭니다. 다음 그림은 샘플 도움말 페이지를 보여 줍니다.

![Web API 도움말 페이지](creating-web-projects-in-visual-studio/_static/image12.png)

![API 가져오기에 대 한 web API 도움말 페이지](creating-web-projects-in-visual-studio/_static/image13.png)

Web API에 대 한 자세한 내용은 참조 하세요. [ASP.NET Web API](https://asp.net/web-api)합니다.

<a id="spa"></a>
### <a name="single-page-application-template"></a>단일 페이지 응용 프로그램 템플릿

단일 페이지 응용 프로그램 (SPA) 템플릿은 만듭니다 JavaScript, HTML 5를 사용 하는 샘플 응용 프로그램 및 [KnockoutJS](http://knockoutjs.com/) 클라이언트 및 서버에서 ASP.NET Web API에서 합니다.

SPA 템플릿에 대 한 인증 옵션은 [개별 사용자 계정](#indauth)합니다.

다음 그림에서는 SPA 템플릿을 작성 하는 샘플 응용 프로그램의 초기 상태를 보여 줍니다.

![SPA 샘플 응용 프로그램](creating-web-projects-in-visual-studio/_static/image14.png)

SPA 템플릿을 사용 하 여 응용 프로그램을 만드는 방법에 대 한 자세한 내용은 [Web API-외부 인증 서비스](../../../web-api/overview/security/external-authentication-services.md)합니다.

KnockoutJS 이외의 JavaScript 프레임 워크를 사용 하는 추가 SPA 템플릿 및 ASP.NET 단일 페이지 응용 프로그램에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 단일 페이지 응용 프로그램](../../../single-page-application/index.md)합니다.
- [VS2013 RC에 대 한 SPA 템플릿의 보안 기능을 이해](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx)
- [단일 페이지 응용 프로그램: ASP.NET 사용 하 여 최신이 고 응답성이 뛰어난 웹 앱 빌드](https://msdn.microsoft.com/magazine/dn463786.aspx)

<a id="facebook"></a>
### <a name="facebook-template"></a>Facebook 템플릿

설치할 수는 [Facebook 템플릿을 제공 하는 Visual Studio 확장](https://go.microsoft.com/fwlink/?LinkID=509965&amp;clcid=0x409)합니다. 이 템플릿은 Facebook 웹 사이트 내에서 실행 되도록 디자인 된 샘플 응용 프로그램을 만듭니다. ASP.NET MVC를 기반으로 하 고 실시간 업데이트 기능에 대 한 Web API를 사용 합니다.

Facebook 응용 프로그램 Facebook 사이트 내에서 실행 하 고 Facebook의 인증을 사용 하기 때문에 Facebook 템플릿 사용할 수 없는 인증 옵션은.

ASP.NET Facebook 응용 프로그램에 대 한 자세한 내용은 참조 하세요. [MVC Facebook API 업데이트](https://blogs.msdn.com/b/webdev/archive/2014/06/10/updating-the-mvc-facebook-api.aspx)합니다.

<a id="vs2012"></a>
### <a name="visual-studio-2012-templates"></a>Visual Studio 2012 템플릿

Visual Studio 2013 웹 프로젝트 만들기 대화 상자는 Visual Studio 2012에서 사용할 수 있었던 일부 서식 파일에 대 한 액세스를 제공 하지 않습니다. 이러한 템플릿 중 하나를 사용 하려는 경우에 Visual Studio 새 프로젝트 대화 상자의 왼쪽된 창에서 Visual Studio 2012 노드를 클릭 수 있습니다.

![Visual Studio 2012 템플릿](creating-web-projects-in-visual-studio/_static/image15.png)

합니다 **Visual Studio 2012** 지원 하지 않는 다음 웹 템플릿을 원하는 노드 수에 대 한 액세스 템플릿의 기본 목록에서 Visual Studio 2013 용:

- ASP.NET MVC 4 웹 응용 프로그램
- ASP.NET Dynamic Data 엔터티 웹 응용 프로그램
- ASP.NET AJAX 서버 컨트롤
- ASP.NET AJAX 서버 컨트롤 Extender
- ASP.NET 서버 컨트롤

<a id="bootstrap"></a>
## <a name="bootstrap-in-the-visual-studio-2013-web-project-templates"></a>Visual Studio 2013 웹 프로젝트 템플릿에서 부트스트랩

Visual Studio 2013 프로젝트 템플릿을 사용 하 여 [부트스트랩](http://getbootstrap.com/), Twitter에서 만든 레이아웃 및 테마 프레임 워크입니다. 부트스트랩 CSS3를 사용 하 여 레이아웃 다른 브라우저 창 크기를 동적으로 조정할 수는 반응 형 디자인을 제공 합니다. 예를 들어 넓은 브라우저 창에서 Web Forms 템플릿에서 만든 홈페이지 같습니다. 다음 그림에서는

![Web Forms 템플릿 앱 홈 페이지](creating-web-projects-in-visual-studio/_static/image16.png)

창 축소 만들고 가로로 정렬 된 열을 세로로 정렬으로 이동 합니다.

![부트스트랩 세로 열 정렬](creating-web-projects-in-visual-studio/_static/image17.png)

창을 좀 더 좁힌 상단 가로 메뉴 클릭 메뉴를 세로 방향된으로 확장할 수 있는 아이콘으로 바뀝니다.

![부트스트랩 메뉴 아이콘](creating-web-projects-in-visual-studio/_static/image18.png)

![부트스트랩 세로 메뉴](creating-web-projects-in-visual-studio/_static/image19.png)

또한 쉽게 응용 프로그램의 모양 및 느낌이 변경 내용을 적용 하려면 부트스트랩 테마 기능을 사용할 수 있습니다. 예를 들어 테마를 변경 하려면 다음 단계를 수행할 수 있습니다.

1. 브라우저에서로 이동 [ http://Bootswatch.com ](http://Bootswatch.com)테마를 선택한 후 클릭 **다운로드**합니다. (다운로드 *bootstrap.min.css* 기본적으로 CSS 코드를 검사 하려는 경우 가져오기 *bootstrap.css* 축소 된 버전 대신 합니다.)
2. 다운로드 된 CSS 파일의 내용을 복사 합니다.
3. Visual Studio에서 만드는 새 **스타일 시트** 라는 파일 *부트스트랩 theme.css* 에 *콘텐츠* 폴더 및 붙여넣기를 다운로드 한 CSS 코드를 합니다.
4. 오픈 *앱\_Start/Bundle.config* 변경 *bootstrap.css* 하 *부트스트랩 theme.css*합니다.

프로젝트를 다시 실행 하 고 응용 프로그램의 모습이 새롭게 바뀌었습니다. 다음 그림에서는 Amelia 테마의 효과 보여 줍니다.

![부트스트랩 Amelia 테마](creating-web-projects-in-visual-studio/_static/image20.png)

많은 부트스트랩 테마를 사용할 수는 무료 및 프리미엄 버전입니다. 부트스트랩도 다양 한 UI 구성 요소와 같은 [드롭다운](http://twitter.github.io/bootstrap/components.html#dropdowns)를 [그룹 단추](http://twitter.github.io/bootstrap/components.html#buttonGroups), 및 [아이콘](http://twitter.github.io/bootstrap/base-css.html#images)합니다. 부트스트랩에 대 한 자세한 내용은 참조 하세요. [부트스트랩 사이트](http://twitter.github.io/bootstrap/)합니다.

Visual Studio에서 Web Forms 디자이너를 사용 하는 경우 디자이너는 부트스트랩 테마 또는 반응 형 레이아웃 변경의 모든 작업이 정확 하 게 표시 되지 않습니다 있도록 CSS3을 지원 하지 않습니다 note 합니다. 그러나 브라우저를 사용 하 여 볼 때 Web Forms 페이지를 올바르게 표시 됩니다.

<a id="add"></a>
## <a name="adding-support-for-additional-frameworks"></a>추가 프레임 워크에 대 한 지원 추가

서식 파일을 선택 하면 템플릿에서 사용할 프레임 워크에 대 한 확인란은 자동으로 선택 됩니다. 예를 들어, 선택 하는 경우는 **Web Forms** 템플릿을 합니다 **Web Forms** 확인란을 선택 하 고 지울 수 없습니다.

![템플릿 선택](creating-web-projects-in-visual-studio/_static/image21.png)

![프레임 워크를 추가 합니다.](creating-web-projects-in-visual-studio/_static/image22.png)

프로젝트가 만들어질 때 프레임 워크에 대 한 지원을 추가 하기 위해 템플릿에 포함 되지 않은 프레임 워크에 대 한 확인란을 선택할 수 있습니다. 예를 들어, Web Forms를 사용 하도록 설정 하려면 *.aspx* MVC 템플릿을 선택한 경우 페이지를 선택 합니다 **Web Forms** 확인란 합니다. MVC를 Web Forms 템플릿을 사용 하는 경우 사용 하도록 설정 하려면 클릭 합니다 **MVC** 확인란 합니다. 추가 프레임 워크 런타임 뿐만 아니라 디자인 타임 지원할 수 있습니다. 예를 들어 MVC 지원 Web Forms 프로젝트에 추가 하는 경우에 컨트롤러와 뷰를 스 캐 폴드 하 수 있습니다.

Web Forms 및 MVC 프로젝트를 결합 하 고 사용 하는 경우 [친화적 Url](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx) Web Forms에 있을 수 있습니다 하지 라우팅 문제 URL이 하나 있는 대상이 여러 개 예상 합니다. 먼저 정의 된 경로 우선을 적용 됩니다. 예를 들어 있는 경우를 `Home` 컨트롤러와 *Home.aspx* 페이지를 `http://contoso.com/home` URL로 이동 됩니다 *Home.aspx* 호출 하는 경우는 `EnableFriendlyUrls` 를호출하기전에`MapRoute`에서 메서드 *RouteConfig.cs*에 동일한 URL에 대 한 기본 보기로 이동 또는 프로그램 `Home` 호출 하는 경우 컨트롤러 `MapRoute` 하기 전에 `EnableFriendlyUrls`.

프레임 워크를 추가 하는 경우에 샘플 응용 프로그램 기능을 추가 되지 않습니다. Web Forms 지원 되지 않습니다 MVC 템플릿을 선택한 경우 추가 하는 경우에 예를 들어 *Default.aspx* 홈 페이지 파일이 만들어집니다. 폴더, 파일 및 프레임 워크를 지 원하는 데 필요한 참조만 추가 됩니다. 따라서 프레임 워크를 추가 하면 템플릿에서 만든 샘플 응용 프로그램 코드에서 구현 되는 인증 옵션을 변경 되지 않습니다. 예를 들어, 빈 템플릿을 선택 하 고 추가 하는 경우 Web Forms 또는 MVC를 지원 합니다 **인증 구성** 단추가 비활성화 계속 됩니다.

다음 섹션에서는 각 확인란의 효과 간략하게 설명 합니다.

### <a name="add-web-forms-support"></a>Web Forms 지원 추가

빈 만듭니다 *앱\_데이터* 하 고 *모델* 폴더와 *Global.asax* 파일입니다. 이러한 이미 만들었으므로 빈 템플릿에 이외의 모든 템플릿에서 Web Forms 확인란을 선택 하는 다른 템플릿에 대 한 중요 하지 않습니다.

Web Forms 템플릿에 기본적으로 하지만 Web Forms 친화적 Url을 자동으로 사용할 수 없습니다 Web Forms 확인란을 선택 하 여 다른 템플릿에 대 한 지원 추가 하면 친화적 Url을 수 있습니다.

### <a name="add-mvc-support"></a>MVC 지원 추가

MVC, Razor, 및 웹 페이지 NuGet 패키지 설치를 만들고 빈 *앱\_데이터*합니다 *컨트롤러*를 *모델*, 및 *뷰*폴더를 만듭니다 *앱\_시작* 폴더가 *RouteConfig.cs* 파일을 만들고 *Global.asax* 파일입니다.

### <a name="add-web-api-support"></a>웹 API 지원 추가

WebApi 및 Newtonsoft.Json NuGet 패키지 설치를 만들고 빈 *앱\_데이터*합니다 *컨트롤러*, 및 *모델* 폴더를 만듭니다  *앱\_시작* 폴더가 *WebApiConfig.cs* 파일을 만들고 *Global.asax* 파일입니다.

<a id="auth"></a>
## <a name="authentication-methods"></a>인증 방법

Visual Studio 2013 Web Forms, MVC 및 Web API 템플릿에 대 한 몇 가지 인증 옵션을 제공합니다.

- [인증 안 함](#noauth)
- [개별 사용자 계정](#indauth) (ASP.NET 멤버 자격 이전의 ASP.NET Id)
- [조직 계정](#orgauth) (Windows Server Active Directory 또는 Azure Active Directory)
- [Windows 인증](#winauth) (인트라넷)

![인증 대화 상자를 구성 합니다.](creating-web-projects-in-visual-studio/_static/image23.png)

<a id="noauth"></a>

### <a name="no-authentication"></a>인증 안 함

선택 하는 경우 **인증 없음**이상 UI는 로그인 한 사용자를 나타내는 엔터티가 멤버 자격 데이터베이스에 멤버 자격 데이터베이스에 대 한 연결 문자열을 클래스, 샘플 응용 프로그램에 로그인 하기 위한 웹 페이지가 포함 됩니다.

<a id="indauth"></a>
### <a name="individual-user-accounts"></a>개별 사용자 계정

선택 하는 경우 **개별 사용자 계정**, 샘플 응용 프로그램 (이전의 ASP.NET 멤버 자격) ASP.NET Id를 사용 하도록 사용자 인증을 위해 구성 됩니다. ASP.NET Id 사용자를 Facebook, Google, Microsoft 계정 또는 Twitter 같은 소셜 공급자를 로그인 하 여 사이트에서 사용자 이름 및 암호를 만들어서 계정을 등록할 수 있습니다. ASP.NET Id에서 사용자 프로필에 대 한 기본 데이터 저장소는 프로덕션 사이트에 대 한 SQL Server 또는 Azure SQL Database로 배포할 수 있는 SQL Server LocalDB 데이터베이스입니다.

Visual Studio 2013에서 이러한 기능은 Visual Studio 2012와 동일 하지만 ASP.NET 멤버 자격 시스템의 기본 코드를 다시 작성 되었습니다. 새 코드 베이스의 장점은 다음과 같습니다.

- 새 멤버 자격 시스템 기반 [OWIN](http://owin.org/) ASP.NET 폼 인증 모듈을 대신 합니다. 즉, IIS에서 Web Forms 또는 MVC를 사용 하 든 웹 API 또는 SignalR 자체 호스팅 중인 동일한 인증 메커니즘을 사용할 수 있습니다.
- Entity Framework Code First에서 관리 하는 새 멤버 자격 데이터베이스 및 수정할 수 있는 엔터티 클래스에 의해 모든 테이블 표시 됩니다. 즉, 데이터베이스 스키마 및 프로필 관련 웹 UI 사용자 고유의 요구 사항에 맞게 쉽게 사용자 지정할 수 고 Code First 마이그레이션을 사용 하 여 업데이트를 쉽게 배포할 수 있습니다.

새 멤버 자격 시스템은 새 템플릿에 자동으로 구현 하 고 이상.NET 4.5를 대상으로 하는 모든 프로젝트에 수동으로 구현할 수 있습니다.

ASP.NET Id는 것이 좋습니다는 주로 외부 고객에 게는 인터넷 웹 사이트를 만드는 경우입니다. 조직에서는 Active Directory 또는 Office 365 및 있습니다 직원 및 비즈니스 파트너에 대 한 single sign-on 사용 하도록 설정 하는 프로젝트를 만들려고 할 경우는 **조직 계정** 옵션 보다 적합할 수 있습니다.

개별 사용자 계정 옵션에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [www.asp.net/identity](../../../identity/index.md). ASP.NET 웹 사이트에서 ASP.NET Id에 대 한 설명서입니다.
- [Facebook 및 Google OAuth2 및 OpenID Sign on을 사용 하 여 ASP.NET MVC 5 앱 만들기](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)합니다. 또한 사용자 프로필 데이터를 사용자 지정 하는 방법을 보여 줍니다.
- [웹 API-외부 인증 서비스](../../../web-api/overview/security/external-authentication-services.md)
- [Visual Studio 2013에서 ASP.NET 응용 프로그램에 외부 로그인 추가](https://blogs.msdn.com/b/webdev/archive/2013/06/27/adding-external-logins-to-your-asp-net-application-in-visual-studio-2013.aspx)

<a id="orgauth"></a>
### <a name="organizational-accounts"></a>조직 계정

선택 하는 경우 **조직 계정**, 샘플 응용 프로그램은 Azure Active Directory (Azure AD, Office 365를 포함 하는)에서 사용자 계정을 기반으로 하는 인증에 대 한 Windows Identity Foundation (WIF)을 사용 하도록 구성 수 또는 Windows Server Active Directory입니다. 자세한 내용은 [조직 계정 인증 옵션](#orgauthoptions) 이 항목의에서 뒷부분에 있습니다.

<a id="winauth"></a>
### <a name="windows-authentication"></a>Windows 인증

선택 하는 경우 **Windows 인증**, 샘플 응용 프로그램 인증에 대 한 Windows Authentication IIS 모듈을 사용 하도록 구성 됩니다. 응용 프로그램에는 Active directory 또는 Windows에 로그인 하지만 않습니다 포함 사용자 등록 하거나 로그인 UI는 로컬 컴퓨터 계정의 도메인 및 사용자 ID를 표시 됩니다. 이 옵션은 인트라넷 웹 사이트에 대 한 것입니다.

또는 선택 하 여 AD 인증을 사용 하는 인트라넷 사이트를 만들 수 있습니다 합니다 [온-프레미스 조직 계정으로 옵션](#orgauthonprem)합니다. 온-프레미스 옵션 Windows 인증 모듈 대신 Windows Identity Foundation (WIF)를 사용합니다. 온-프레미스 옵션을 설정 하기 위해 몇 가지 추가 단계가 필요 하지만 WIF Windows 인증 모듈을 사용 하 여 사용할 수 없는 기능을 사용 합니다. 예를 들어, WIF를 사용 하 여 디렉터리 데이터 쿼리 및 Active Directory에서에서 응용 프로그램 액세스를 구성할 수 있습니다.

<a id="orgauthoptions"></a>
## <a name="organizational-account-authentication-options"></a>조직 계정 인증 옵션

합니다 **인증 구성** 대화 Azure Active Directory (Azure AD, Office 365를 포함 하는) 또는 Windows Server Active Directory (AD) 계정 인증에 대 한 몇 가지 옵션을 제공 합니다.

- [클라우드-단일 조직](#orgauthsingle) (Azure AD 또는 Azure AD와 디렉터리 통합을 사용 하 여 AD)
- [클라우드-다중 조직](#orgauthmulti) (Azure AD 또는 Azure AD와 디렉터리 통합을 사용 하 여 AD)
- [온-프레미스](#orgauthonprem) (AD)

Azure AD 옵션 중 하나를 시도 하 긴 하지만 아직 계정이 없는 경우 [Azure AD 계정에 등록 하려면 여기를 클릭 하십시오.](https://go.microsoft.com/fwlink/?LinkId=309942)합니다.

> [!NOTE]
> Azure AD 옵션 중 하나를 선택 하면 프로젝트에 필요한 데이터베이스 및 Azure AD 테 넌 트에 대 한 전역 관리자 계정에 로그인 해야 합니다. 조직 계정에 대 한 이름 및 암호를 입력 (예를 들어 admin@contoso.onmicrosoft.com) Azure AD 테 넌 트에 대 한 관리 권한이 있는 합니다.
> 
> **Microsoft 계정 자격 증명을 입력 하지 마세요 (예를 들어 contoso@hotmail.com) 로그인 대화 상자에서.**


<a id="orgauthsingle"></a>
### <a name="cloud---single-organization-authentication"></a>클라우드-단일 조직 인증

![단일 조직 인증](creating-web-projects-in-visual-studio/_static/image24.png)

하나의 Azure AD에 정의 된 사용자 계정에 대 한 인증을 사용 하도록 설정 하려는 경우이 옵션을 선택 [테 넌 트](https://technet.microsoft.com/library/jj573650.aspx)합니다. 예를 들어 사이트 contoso.com 이며이 사용 가능 하 게 contoso.onmicrosoft.com 테 넌 트에 있는 Contoso 회사의 직원에 게 합니다. 사용자가 다른 테 넌 트 응용 프로그램에 액세스할 수 있도록 Azure AD를 구성할 수 없습니다.

#### <a name="domain"></a>도메인

예를 들어, 응용 프로그램을 설정 하려는 Azure AD 도메인 입력: `contoso.onmicrosoft.com`합니다. 있는 경우는 [사용자 지정 도메인](http://www.cloudidentity.com/blog/2013/04/14/adding-a-custom-domain-to-your-windows-azure-ad/)와 같은 `contoso.com` 대신 `contoso.onmicrosoft.com`, 여기를 입력할 수 있습니다.

#### <a name="access-level"></a>액세스 수준

응용 프로그램은 쿼리 또는 Graph API를 사용 하 여 디렉터리 정보 업데이트를 선택 해야 하는 경우 **Single Sign-on, 디렉터리 데이터 읽기** 하거나 **Single Sign-on, 읽기 및 디렉터리 데이터 쓰기**합니다. 그렇지 않으면 **Single Sign On**합니다. 자세한 내용은 [응용 프로그램 액세스 수준을](https://msdn.microsoft.com/library/windowsazure/b08d91fa-6a64-4deb-92f4-f5857add9ed8#BKMK_AccessLevels) 하 고 [쿼리 Azure AD Graph API를 사용 하 여](https://msdn.microsoft.com/library/windowsazure/dn151791.aspx)입니다.

#### <a name="application-id-uri"></a>응용 프로그램 ID URI

기본적으로 템플릿은 Azure AD 도메인에 프로젝트 이름을 추가 하 여를 응용 프로그램 ID URI를 만듭니다. 예를 들어 프로젝트 이름이 `Example` 도메인 이며 `contoso.onmicrosoft.com`, 응용 프로그램 ID URI가 `https://contoso.onmicrosoft.com/Example`합니다. 수동으로 응용 프로그램 ID URI를 지정 하려는 경우 확장 합니다 **기타 옵션** 섹션 및 텍스트 상자에 응용 프로그램 ID URI를 입력 합니다. 응용 프로그램 ID URI로 시작 해야 `https://`합니다.

기본적으로 Azure AD에서 이미 프로 비전 되는 응용 프로그램은 Visual Studio 프로젝트에 대해 사용 하는 것과 동일한 응용 프로그램 ID URI 프로젝트에 연결할 새 프로 비전 하는 대신 기존 응용 프로그램입니다. 이 경우 프로 비전 할 새 응용 프로그램을 원한다 면의 선택을 취소 합니다 **동일한 ID를 사용 하 여 이미 있는 경우 응용 프로그램 항목을 덮어쓸** 확인란 합니다.

경우는 **덮어쓰기** 확인란의 선택을 취소 하 고 Visual Studio에서 동일한 응용 프로그램 ID URI를 사용 하 여 기존 응용 프로그램을 찾습니다. 사용 하려는 URI에 숫자를 추가 하 여 새 URI를 만듭니다. 예를 들어 프로젝트 이름이 `Example`텍스트 상자를 비워 두면의 선택을 취소 합니다 **덮어쓰기** URI 사용 하 여 응용 프로그램에 이미 확인란 및 Azure AD 테 넌 트 `https://contoso.onmicrosoft.com/Example`합니다. 이 경우 새 응용 프로그램을 프로 비전 할 응용 프로그램 ID URI 등을 사용 하 여 `https://contoso.onmicrosoft.com/Example_20130619330903`입니다.

#### <a name="provisioning-the-application-in-azure-ad"></a>Azure AD에서 응용 프로그램을 프로 비전

Visual Studio을 Azure AD에서 응용 프로그램을 프로 비전 하거나 기존 응용 프로그램 프로젝트를 연결 하려면 도메인의 전역 관리자 자격 증명이 필요 합니다. 클릭 하면 **확인** 에 **인증 구성** 대화 상자에서 사용자 이름 및 지정한 도메인에 대 한 전역 관리자의 암호를 묻는 합니다. 클릭 하면 나중 **프로젝트 만들기** 에 **새 ASP.NET 프로젝트** 대화 상자에서 Visual Studio에서 Azure AD 응용 프로그램을 프로 비전 합니다. 이 프로세스의 일부로 Visual Studio에서는 클라이언트 암호 값을 만든 후 1 년 만료 되는 Web.config 파일에서 note 합니다.

사용 하는 응용 프로그램을 만드는 방법에 대 한 자세한 **클라우드-단일 조직** 인증의 경우 다음 리소스를 참조 하세요.

- [Azure 인증](../2012/windows-azure-authentication.md)
- [Azure AD를 사용 하 여 웹 응용 프로그램에 Sign-on 추가](https://msdn.microsoft.com/library/windowsazure/dn151790.aspx)
- [Azure Active Directory를 사용하여 ASP.NET 앱 개발](../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)
- [Azure AD 사용 하 여 ASP.NET Web API 보안 유지 및 Microsoft OWIN 구성 요소](https://msdn.microsoft.com/magazine/dn463788.aspx)

자습서를 아직 Visual Studio 2013에 대 한 업데이트 되지 않았습니다. 수동으로 작업을 수행할 수 있는 자습서 직접 일부 Visual Studio 2013에서 자동화 됩니다.

<a id="orgauthmulti"></a>
### <a name="cloud---multi-organization-authentication"></a>클라우드-다중 조직 인증

![여러 조직 인증](creating-web-projects-in-visual-studio/_static/image25.png)

여러 Azure AD에 정의 된 사용자 계정에 대 한 인증을 사용 하도록 설정 하려는 경우이 옵션을 선택 [테 넌 트](https://technet.microsoft.com/library/jj573650.aspx)합니다. 예를 들어 사이트 contoso.com 이며이 사용 가능 하 게 contoso.onmicrosoft.com 테 넌 트에는 Contoso 회사의 직원이 Fabrikam 회사의 직원 fabrikam.onmicrosoft.com 테 넌 트에서를 합니다.

입력 설정 및 응용 프로그램 프로 비전 단계는 비슷합니다 [단일 조직 인증](#orgauthsingle)합니다.

사용 하는 응용 프로그램을 만드는 방법에 대 한 자세한 **클라우드-다중 조직** 인증을 다음 리소스를 참조 하세요.

- [Azure Active Directory, ASP.NET 사용 하 여 쉽게 웹 앱 통합 &amp; Visual Studio](https://blogs.msdn.com/b/active_directory_team_blog/archive/2013/06/26/improved-windows-azure-active-directory-integration-with-asp-net-amp-visual-studio.aspx) Active Directory 팀 블로그.
- [Azure AD 사용 하 여 다중 테 넌 트 웹 응용 프로그램 개발](https://msdn.microsoft.com/library/windowsazure/dn151789.aspx) 자습서입니다. 이 자습서는 Visual Studio 2013 아직 업데이트 되지 않은 새로운 자습서가 만들도록 지시 하 수동으로 중 일부는 Visual Studio 2013에서 자동화 됩니다.
- [로그인 할 수 전에 고유한 여러 조직에서는 ASP.NET 앱을 사용 하 여 등록 해야](http://www.cloudidentity.com/blog/2013/10/26/you-have-to-sign-up-with-your-own-multiple-organizations-asp-net-app-before-you-can-sign-in/)합니다. 일반적인 문제 사람들이 해결 하는 방법을 설명 하는 Vittorio bertocci가 블로그 다중 조직 인증을 사용 하는 프로젝트를 만들 때 발생 합니다.

<a id="orgauthonprem"></a>
### <a name="on-premises-organizational-authentication"></a>온-프레미스 조직 인증

![온-프레미스 조직 인증](creating-web-projects-in-visual-studio/_static/image26.png)

Windows Server AD (Active Directory)에 정의 된 사용자 계정에 대 한 인증을 사용 하도록 설정 하 고 Azure AD를 사용 하지 않으려는 경우이 옵션을 선택 합니다. 인트라넷 사이트 또는 인터넷 사이트를 만들려면이 옵션을 사용할 수 있습니다. 인터넷 사이트의 경우 Active Directory Federation Services (ADFS) 사용 하 여 AD에 대 한 액세스를 제공 합니다. 자세한 내용은 [온-프레미스 조직 인증 옵션 (ADFS) 사용 하 여 ASP.NET을 사용 하 여 Visual Studio 2013에서](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)합니다.

인트라넷 사이트를 대신 선택할 수 있습니다 [Windows 인증](#winauth) 이 옵션 대신 합니다. Windows 인증 옵션에 대 한 메타 데이터 문서 URL을 제공할 필요가 없습니다. 그러나 Windows 인증 얻지 기능 디렉터리 데이터를 쿼리 또는 Active Directory에서 응용 프로그램 액세스를 제어 합니다.

#### <a name="on-premises-authority"></a>온-프레미스 기관

메타 데이터 문서를 가리키는 URL을 입력 합니다. 메타 데이터 문서는 기관의 좌표가 포함 합니다. 응용 프로그램 웹 로그온 흐름을 진행 하려면 이러한 좌표를 사용 합니다.

#### <a name="application-id-uri"></a>응용 프로그램 ID URI

AD는이 응용 프로그램을 식별 하거나 비워 두고 Visual studio에서 만들 수 하는 데 사용할 수 있는 고유한 URI를 제공 합니다.

<a id="nextsteps"></a>
## <a name="next-steps"></a>다음 단계

이 문서는 Visual Studio 2013에서 새 ASP.NET 웹 프로젝트를 만들기 위한 몇 가지 기본적인 도움말을 제공 했습니다. 웹 개발을 위한 Visual Studio에 대 한 사용에 대 한 자세한 내용은 참조 하세요. [ https://www.asp.net/visual-studio/ ](../../index.md)합니다.
