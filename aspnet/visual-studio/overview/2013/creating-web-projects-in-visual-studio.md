---
uid: visual-studio/overview/2013/creating-web-projects-in-visual-studio
title: "Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기 | Microsoft Docs"
author: tdykstra
description: "이 항목에서는 Visual Studio 2013 업데이트 3 여기에서 ASP.NET 웹 프로젝트를 만들기 위한 옵션은 웹 개발 c에 대 한 새로운 기능 중 일부에 대해 설명..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/01/2014
ms.topic: article
ms.assetid: 61941e64-0c0d-4996-9270-cb8ccfd0cabc
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /visual-studio/overview/2013/creating-web-projects-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: 96960ef56b1206374458dbbba4befffaa83c1624
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="creating-aspnet-web-projects-in-visual-studio-2013"></a>Visual Studio 2013에서 ASP.NET 웹 프로젝트 만들기
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

> 이 항목에서는 Visual Studio 2013 업데이트 3에서 ASP.NET 웹 프로젝트를 만들기 위한 옵션 설명
> 
> 다음은 이전 버전의 Visual Studio에 비해 웹 개발에 대 한 새로운 기능 중 일부입니다.
> 
> - 간단한 UI를 만들기 위한 프로젝트 해당 제품 [여러 ASP.NET 프레임 워크에 대 한 지원](#add) (Web Forms, MVC 및 Web API).
> - [ASP.NET Identity](#indauth)를 웹 호스팅 IIS가 아닌 다른 소프트웨어와 모든 ASP.NET 프레임 워크와 작동에 동일 하 게 작동 하는 새로운 ASP.NET 멤버 자격 시스템.
> - 사용 [부트스트랩](#bootstrap) 반응 형 디자인 및 테마 설정 기능을 제공 합니다.
> - 와 같은 MVC에 대해서만 제공 하는 데 사용 하는 Web Forms에 대 한 새로운 기능 [자동 테스트 프로젝트 만들기](#testproj) 및 [인트라넷 사이트 템플릿](#winauth)합니다.
> 
> Azure 클라우드 서비스 또는 Azure 모바일 서비스에 대 한 웹 프로젝트를 만드는 방법에 대 한 정보를 참조 하십시오. [Azure 클라우드 서비스 및 ASP.NET 시작](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-dotnet-get-started/) 및 [Azure 모바일 서비스의 경우.NET을 사용 하 여 순위표 응용 프로그램 만들기 백 엔드](https://azure.microsoft.com/en-us/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)합니다.


<a id="prerequisites"></a>
## <a name="prerequisites"></a>필수 구성 요소

이 문서에 적용 됩니다. [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) 와 [업데이트 3](https://go.microsoft.com/fwlink/?linkid=397827&amp;clcid=0x409) 설치 합니다.

<a id="wap"></a>
## <a name="web-application-projects-versus-web-site-projects"></a>웹 응용 프로그램 프로젝트와 웹 사이트 프로젝트 비교

ASP.NET에서는 두 종류의 웹 프로젝트 간 선택할: *웹 응용 프로그램 프로젝트* 및 *웹 사이트 프로젝트*합니다. 새 개발을 위해 웹 응용 프로그램 프로젝트 것이 좋습니다 및 웹 응용 프로그램 프로젝트에만이 문서에 적용 됩니다. 자세한 내용은 참조 [웹 응용 프로그램 프로젝트와 Visual Studio에서 웹 사이트 프로젝트 비교](https://msdn.microsoft.com/en-us/library/dd547590(v=vs.120).aspx) MSDN 사이트입니다.

<a id="overview"></a>
## <a name="overview-of-web-application-project-creation"></a>웹 응용 프로그램 프로젝트 만들기 개요

다음 단계에는 웹 프로젝트를 만드는 방법을 보여 줍니다.

1. 클릭 **새 프로젝트** 에 **시작** 페이지 또는 **파일** 메뉴.
2. 에 **새 프로젝트** 대화 상자에서 클릭 **웹** 왼쪽된 창에서 및 **ASP.NET 웹 응용 프로그램** 가운데 창에서.

    ![새 프로젝트 대화 상자](creating-web-projects-in-visual-studio/_static/image1.png)

    선택할 수 있습니다 **클라우드** 를 만들려면 왼쪽된 창에서 한 [Azure 클라우드 서비스](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy), [Azure 모바일 서비스](https://msdn.microsoft.com/en-us/library/windows/apps/dn629482.aspx), 또는 [Azure WebJob](https://azure.microsoft.com/en-us/documentation/articles/web-sites-dotnet-deploy-webjobs)합니다. 이 항목에는 해당 템플릿을 처리 하지는 않습니다.
3. 오른쪽 창에서 클릭는 **프로젝트에 Application Insights 추가** 확인란 상태와 사용량 응용 프로그램에 대 한 모니터링을 선택 합니다. 자세한 내용은 참조 [웹 응용 프로그램의 성능을 모니터링](https://azure.microsoft.com/en-us/documentation/articles/app-insights-web-monitor-performance/)합니다.
4. 프로젝트를 지정 **이름**, **위치**, 기타 옵션 및 클릭 **확인**합니다.

    **새 ASP.NET 프로젝트** 대화 상자가 나타납니다.

    ![새 프로젝트 대화 상자](creating-web-projects-in-visual-studio/_static/image2.png)
5. 서식 파일을 클릭 합니다.

    ![서식 파일 선택](creating-web-projects-in-visual-studio/_static/image3.png)
6. 서식 파일에 없는 추가 프레임 워크에 대 한 지원을 추가 하려면 해당 확인란을 클릭 합니다. (표시 된 예에서를 추가할 수 있습니다 MVC 또는 Web API Web Forms 프로젝트입니다.)

    ![프레임 워크 추가](creating-web-projects-in-visual-studio/_static/image4.png)
7. <a id="testproj"></a>단위 테스트 프로젝트를 추가 하려면 클릭 **단위 테스트 추가**합니다.

    ![단위 테스트 추가](creating-web-projects-in-visual-studio/_static/image5.png)
8. 기본적으로 제공 하는 서식 파일 보다 다른 인증 방법을 클릭 **인증 변경**합니다.

    ![인증 단추 구성](creating-web-projects-in-visual-studio/_static/image6.png)

    ![인증 대화 상자를 구성 합니다.](creating-web-projects-in-visual-studio/_static/image7.png)

<a id="azurenewproj"></a>
### <a name="create-a-web-app-or-virtual-machine-in-azure"></a>Azure에 웹 응용 프로그램 또는 가상 컴퓨터 만들기

Visual Studio에는 쉽게 웹 응용 프로그램 호스팅에 대 한 Azure 서비스를 작업할 수 있도록 하는 기능이 포함 되어 있습니다. 예를 들어 Visual Studio IDE에서 바로 다음을 수행할 수 있습니다.

- 만들고 웹 앱 또는 인터넷을 통해 응용 프로그램을 사용할 수 있도록 하는 가상 컴퓨터를 관리 합니다.
- 클라우드에서 실행 되는 응용 프로그램에 의해 생성 된 로그를 봅니다.
- 디버그 모드에서 원격으로 실행할 응용 프로그램은 클라우드에서 실행 되는 동안.
- Viiew 및 SQL 데이터베이스와 같은 다른 Azure 서비스를 관리 합니다.

할 수 있습니다 [Azure 계정을 만들려면](https://www.windowsazure.com/en-us/pricing/free-trial/) 무료, 기본 서비스 등 웹 앱을 포함 하 고 MSDN 구독자 인 경우 다음을 할 수 있습니다 [혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/visual-studio-subscriptions/) 추가 Azure 방향으로 월간 크레딧을 제공 하는 서비스입니다. 

기본적으로는 **새 ASP.NET 프로젝트** 대화 상자를 사용 하면 웹 앱 또는 새 웹 프로젝트에 대 한 가상 컴퓨터를 만들 수 있습니다. 새 웹 응용 프로그램 또는 가상 컴퓨터를 만들려면 않으려면 선택을 취소는 **클라우드의 호스트에에서** 확인란 합니다.

![원격 리소스 만들기](creating-web-projects-in-visual-studio/_static/image8.png)

확인란 캡션 수 있습니다 **클라우드의 호스트에에서** 또는 **원격 리소스 만들기**, 두 경우 모두 효과 동일 합니다. 확인란을 선택한 두면 Visual Studio는 기본적으로 웹 응용 프로그램을 Azure 앱 서비스에서 만듭니다. 드롭다운 상자를 사용 하 여 변경 하는 **가상 컴퓨터** 하려는 경우. Azure에 로그인 되어 있지 되어 Azure 자격 증명을 묻는 메시지가 나타납니다. 에 로그인 한 후 대화 상자를 사용 하면 Visual Studio가 프로젝트에 대해 만들 리소스를 구성할 수 있습니다. 다음 그림은 웹 앱;에 대 한 대화 상자를 표시합니다. 가상 컴퓨터를 만들려면 선택 하면 다양 한 옵션 표시 합니다.

![Azure 앱 설정 구성](creating-web-projects-in-visual-studio/_static/image9.png)

Azure 리소스를 만들기 위한이 프로세스를 사용 하는 방법에 대 한 자세한 내용은 참조 [Azure 및 ASP.NET 시작](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet) 및 [Visual Studio와 함께 웹 사이트에 대 한 가상 컴퓨터를 만드는](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-dotnet-create-visual-studio-powershell/)합니다.

이 문서의 나머지 부분에서는 사용 가능한 템플릿 및 해당 옵션에 대 한 자세한 정보를 제공합니다. 또한 문서 서식 파일에 사용 되는 부트스트랩, 레이아웃 및 테마 프레임 워크를 제공 합니다.

<a id="vs2013"></a>
## <a name="visual-studio-2013-web-project-templates"></a>Visual Studio 2013 웹 프로젝트 템플릿

Visual Studio 웹 프로젝트를 만드는 템플릿을 사용 합니다. 프로젝트 템플릿을 새 프로젝트에서 파일 및 폴더를 만들 수 있습니다, 그리고 NuGet 패키지를 설치 및 기본적인 응용 프로그램에 대 한 예제 코드를 제공 합니다. 템플릿 최신 웹 표준을 구현 되며 점프를 사용 하면 뿐만 아니라 ASP.NET 기술을 사용 하는 방법에 대 한 유용한 시작 응용 프로그램을 만드는 방법에 설명 하기 위해 사용 됩니다.

Visual Studio 2013 이상 버전의.NET framework 또는.NET 4.5를 대상으로 하는 프로젝트에 대 한 웹 프로젝트 템플릿에 대 한 다음 중 하나를 제공 합니다.

- [빈 템플릿](#empty)
- [웹 양식 서식 파일](#wf)
- [MVC 템플릿](#mvc)
- [웹 API 서식 파일](#webapi)
- [단일 페이지 응용 프로그램 템플릿](#spa)
- [Azure 모바일 서비스 템플릿](https://azure.microsoft.com/en-us/documentation/articles/mobile-services-dotnet-backend-windows-store-dotnet-leaderboard/)
- [Visual Studio 2012 템플릿](#vs2012)

제공 하는 Visual Studio 확장을 설치할 수 있습니다는 [Facebook 템플릿](#facebook)합니다.

.NET 4를 대상으로 하는 프로젝트를 만드는 방법에 대 한 정보를 참조 하십시오. [Visual Studio 2012 템플릿](#vs2012) 이 항목의 뒷부분에 나오는 합니다.

모바일 클라이언트에 대 한 ASP.NET 응용 프로그램을 만드는 방법에 대 한 정보를 참조 하십시오. [asp.net에서 모바일 지원](../../../mobile/index.md)합니다.

<a id="empty"></a>
### <a name="empty-template"></a>빈 템플릿

빈 템플릿은 제공 완전 최소 폴더와 같은 프로젝트 파일에는 ASP.NET 웹 앱에 대 한 파일 (*.csproj* 또는. *vbproj*) 및 *Web.config* 파일입니다. 아래의 확인란을 사용 하 여 Web Forms, MVC 또는 Web API에 대 한 지원을 추가할 수는 **폴더 추가 및에 대 한 참조를 핵심:** 레이블.

빈 템플릿 없음 인증 옵션을 사용할 수 있습니다. 인증 기능 예제 응용 프로그램에서 구현 되 고 빈 템플릿에서 예제 응용 프로그램을 만들지 않습니다.

<a id="wf"></a>
### <a name="web-forms-template"></a>웹 양식 서식 파일

프레임 워크는 다양 한 UI 및 데이터를 웹 사이트를 구축 하는 신속 하 게 수 있는 다음과 같은 기능을 제공 하는 Web Forms 기능에 액세스 합니다.

- Visual Studio의 WYSIWYG 디자이너입니다.
- HTML과 속성 및 스타일을 설정 하 여 사용자 지정할 수 있는 렌더링 하는 서버 컨트롤입니다.
- 풍부한 다양 한 데이터 액세스 및 표시 되는 데이터에 대 한 제어 합니다.
- WPF와 같은 클라이언트 응용 프로그램 프로그래밍 것 처럼 프로그래밍할 수 있는 이벤트를 노출 하는 이벤트 모델입니다.
- HTTP 요청 간에 상태 (데이터)의 자동 보존 합니다.

일반적으로 Web Forms 응용 프로그램을 만드는 ASP.NET MVC 프레임 워크를 사용 하 여 동일한 응용 프로그램을 만드는 것 보다 적은 프로그래밍 노력이 필요 합니다. 그러나 Web Forms 신속한 응용 프로그램 개발에 대 한 않습니다. 많은 복잡 한 상업용 응용 프로그램 및 Web Forms 기반으로 구축 된 프레임 워크.

Web Forms 페이지 및 컨트롤 페이지에서 자동으로 브라우저로 전송 되는 태그의 대부분을 생성, ASP.NET MVC에서 제공 하는 HTML 보다 세분화 된 컨트롤의 종류가 필요는 없습니다. 페이지 및 컨트롤을 구성 하기 위한 선언적 모델을 작성 해야 하지만 HTML 및 HTTP 동작 일부를 숨기는 코드의 양을 최소화 합니다. 예를 들어 항상 수 없으면 어떤 태그 컨트롤에 의해 생성 될 수 있습니다 정확 하 게 지정할 수 있습니다.

Web Forms framework가 제공 되지 않습니다 자체 ASP.NET MVC 쉽게 패턴 기반의 개발 과정을와 같은 [테스트 기반 개발](http://en.wikipedia.org/wiki/Test-driven_development), [문제의 분리](http://en.wikipedia.org/wiki/Separation_of_concerns), [반전 컨트롤](http://en.wikipedia.org/wiki/Inversion_of_control), 및 [종속성 주입](http://en.wikipedia.org/wiki/Dependency_injection)합니다. 코드 팩터링 이런 방식으로 작성 하려는 경우에 다음을 할 수 있습니다. ASP.NET MVC 프레임 워크에서와 같이 자동는 방금 없습니다. [ASP.NET Web Forms MVP](http://webformsmvp.com/) 프로젝트 Web Forms 제공 하도록 구성 된 신속한 개발을 유지 하면서 고려 사항 및 테스트 용이성 분리를 용이 하 게 하는 방법을 보여 줍니다. Microsoft SharePoint Web Forms MVP에 작성 됩니다.

Web Forms 템플릿을 사용 하는 샘플 Web Forms 응용 프로그램을 만듭니다 [부트스트랩](#bootstrap) 반응 형 디자인 및 테마 설정 기능을 제공 하기. 다음 그림은 홈 페이지를 보여 줍니다.

![Web Forms 템플릿 응용 프로그램 홈 페이지](creating-web-projects-in-visual-studio/_static/image10.png)

Web Forms에 대 한 자세한 내용은 참조 [ASP.NET Web Forms](https://asp.net/web-forms)합니다. Web Forms 서식 파일은을 수행 하는 방법에 대 한 정보를 참조 하십시오. [Visual Studio 2013을 사용 하 여 기본 Web Forms 응용 프로그램을 구축](https://blogs.msdn.com/b/webdev/archive/2013/12/19/building-a-basic-web-forms-application-using-visual-studio-2013.aspx)합니다.

<a id="mvc"></a>
### <a name="mvc-template"></a>MVC 템플릿

ASP.NET MVC와 같은 개발 패턴 기반의 방법을 용이 하도록 설계 된 [테스트 기반 개발](http://en.wikipedia.org/wiki/Test-driven_development), [문제의 분리](http://en.wikipedia.org/wiki/Separation_of_concerns), [제어](http://en.wikipedia.org/wiki/Inversion_of_control), 및 [종속성 주입](http://en.wikipedia.org/wiki/Dependency_injection)합니다. 프레임 워크는 프레젠테이션 계층에서 웹 응용 프로그램의 비즈니스 논리 계층을 구분 하는 권장 합니다. 응용 프로그램 모델 (M), (V), 뷰 및 컨트롤러 (C)으로 나누어 ASP.NET MVC 대규모 응용 프로그램의 복잡성을 관리 하기 쉽게 수행할 수 있습니다.

ASP.NET MVC와 함께 HTML 및 Web Forms에 보다 HTTP 보다 직접적으로 작업 합니다. 예를 들면 Web Forms HTTP 요청 간에 상태를 자동으로 유지할 수 있지만을 MVC에서 하는 작업을 명시적으로 코딩할 필요 합니다. MVC 모델의 장점은 완벽 하 게 웹 환경에서 동작 하는 방식 및 응용 프로그램이 수행 하는 정확 하 게 제어를 수행할 수 있다는 점입니다. 단점은 더 많은 코드를 작성 해야 하는 것입니다.

MVC 전원 개발자가 응용 프로그램 요구에 맞게의 프레임 워크를 사용자 지정 하는 기능을 제공 하는 확장성을 설계 되었습니다. 또한 ASP.NET MVC 소스 코드는 OSI 라이선스에 따라 사용할 수 있습니다.

MVC 템플릿을 사용 하는 샘플 MVC 5 응용 프로그램을 만듭니다 [부트스트랩](#bootstrap) 반응 형 디자인 및 테마 설정 기능을 제공 하기. 다음 그림은 홈 페이지를 보여 줍니다.

![MVC 샘플 응용 프로그램](creating-web-projects-in-visual-studio/_static/image11.png)

MVC에 대 한 자세한 내용은 참조 [ASP.NET MVC](https://asp.net/mvc)합니다. MVC 4 서식 파일을 선택 하는 방법에 대 한 정보를 참조 하십시오. [Visual Studio 2012 템플릿](#vs2012) 이 문서의 뒷부분에 나오는 합니다.

<a id="webapi"></a>
### <a name="web-api-template"></a>웹 API 서식 파일

Web API 템플릿을 MVC를 기반으로 하는 API 도움말 페이지를 포함 하 여 웹 API에 따라 샘플 웹 서비스를 만듭니다.

ASP.NET Web API는 다양 한 브라우저 및 모바일 장치를 포함 한 클라이언트를 연결할 HTTP 서비스를 작성을 용이 하 게 하는 프레임 워크입니다. ASP.NET Web API는.NET Framework에서 RESTful 서비스를 구축 하기 위한 이상적인 플랫폼입니다.

Web API 템플릿을 샘플 웹 서비스를 만듭니다. 다음 그림은 샘플 도움말 페이지를 표시합니다.

![Web API 도움말 페이지](creating-web-projects-in-visual-studio/_static/image12.png)

![API 가져오기에 대 한 web API 도움말 페이지](creating-web-projects-in-visual-studio/_static/image13.png)

웹 API에 대 한 자세한 내용은 참조 [ASP.NET Web API](https://asp.net/web-api)합니다.

<a id="spa"></a>
### <a name="single-page-application-template"></a>단일 페이지 응용 프로그램 템플릿

단일 페이지 응용 프로그램 (SPA) 템플릿은 만듭니다 HTML 5, JavaScript를 사용 하는 예제 응용 프로그램 및 [KnockoutJS](http://knockoutjs.com/) 클라이언트 및 서버에서 ASP.NET 웹 API에 있습니다.

SPA 서식 파일에 대 한 유일한 인증 옵션은 [개별 사용자 계정](#indauth)합니다.

다음은 SPA 템플릿을 작성 하는 샘플 응용 프로그램의 초기 상태입니다.

![SPA 샘플 응용 프로그램](creating-web-projects-in-visual-studio/_static/image14.png)

SPA 템플릿을 사용 하 여 응용 프로그램을 만드는 방법에 대 한 정보를 참조 하십시오. [웹 API-외부 인증 서비스](../../../web-api/overview/security/external-authentication-services.md)합니다.

KnockoutJS 이외의 다른 JavaScript 프레임 워크를 사용 하는 추가 SPA 템플릿이 및 ASP.NET 단일 페이지 응용 프로그램에 대 한 자세한 내용은 다음 리소스를 참조 합니다.

- [ASP.NET 단일 페이지 응용 프로그램](../../../single-page-application/index.md)합니다.
- [VS2013 RC에 대 한 SPA 서식 파일의 보안 기능을 이해](https://blogs.msdn.com/b/webdev/archive/2013/09/20/understanding-security-features-in-spa-template.aspx)
- [단일 페이지 응용 프로그램: asp.net 현대적이 고 응답성이 뛰어난 웹 응용 프로그램 빌드](https://msdn.microsoft.com/en-us/magazine/dn463786.aspx)

<a id="facebook"></a>
### <a name="facebook-template"></a>Facebook 템플릿

설치할 수 있습니다는 [Facebook 템플릿 제공 하는 Visual Studio 확장](https://go.microsoft.com/fwlink/?LinkID=509965&amp;clcid=0x409)합니다. 이 템플릿은 Facebook 웹 사이트 내에서 실행 되도록 디자인 된 예제 응용 프로그램을 만듭니다. ASP.NET MVC를 기반으로 하 고 실시간 업데이트 기능에 대 한 웹 API를 사용 합니다.

Facebook 응용 프로그램에서 Facebook 사이트 내에서 실행 및 Facebook의 인증에 의존 하기 때문에 인증 옵션 없이 Facebook 템플릿 수 있습니다.

ASP.NET Facebook 응용 프로그램에 대 한 자세한 내용은 참조 [MVC Facebook API 업데이트](https://blogs.msdn.com/b/webdev/archive/2014/06/10/updating-the-mvc-facebook-api.aspx)합니다.

<a id="vs2012"></a>
### <a name="visual-studio-2012-templates"></a>Visual Studio 2012 템플릿

Visual Studio 2013 웹 프로젝트 만들기 대화 상자는 Visual Studio 2012에서 사용할 수 있었던 일부 서식 파일에 대 한 액세스를 제공 하지 않습니다. 이러한 템플릿 중 하나를 사용 하려는 경우 Visual Studio 새 프로젝트 대화 상자의 왼쪽된 창에서 Visual Studio 2012 노드를 클릭 수 있습니다.

![Visual Studio 2012 템플릿](creating-web-projects-in-visual-studio/_static/image15.png)

**Visual Studio 2012** 노드 액세스할 수 있습니다 지원 하지 않는 다음 웹 서식 파일을 선택 하려면 서식 파일의 기본 목록에서 Visual Studio 2013 용:

- ASP.NET MVC 4 웹 응용 프로그램
- ASP.NET Dynamic Data 엔터티 웹 응용 프로그램
- ASP.NET AJAX 서버 컨트롤
- ASP.NET AJAX 서버 컨트롤 Extender
- ASP.NET 서버 컨트롤

<a id="bootstrap"></a>
## <a name="bootstrap-in-the-visual-studio-2013-web-project-templates"></a>Visual Studio 2013 웹 프로젝트 템플릿에서 부트스트랩

Visual Studio 2013 프로젝트 템플릿을 사용 하 여 [부트스트랩](http://getbootstrap.com/), Twitter에서 만든 프레임 워크 레이아웃 및 테마 설정입니다. 다른 브라우저 창 크기에 맞게 레이아웃 동적으로 적용할 수는 반응 형 디자인을 제공 하기 위해 CSS3를 사용 하는 부트스트랩 합니다. 예를 들어 넓은 브라우저 창 홈 페이지 Web Forms 템플릿으로 만든 다음 그림과 같이 표시 됩니다.

![Web Forms 템플릿 응용 프로그램 홈 페이지](creating-web-projects-in-visual-studio/_static/image16.png)

2pt 창과 세로로 정렬으로 이동 가로로 정렬된 열을 확인 합니다.

![부트스트랩 세로 열 정렬](creating-web-projects-in-visual-studio/_static/image17.png)

창을 약간를 더 좁힌 가로 상단 메뉴 세로 방향의 메뉴를 확장 하기 위해 클릭할 수 있는 아이콘으로 바뀝니다.

![부트스트랩 메뉴 아이콘](creating-web-projects-in-visual-studio/_static/image18.png)

![부트스트랩 세로 메뉴](creating-web-projects-in-visual-studio/_static/image19.png)

또한 쉽게 응용 프로그램의 모양과 느낌에 변경 내용을 적용 하려면 부트스트랩의 테마 설정 기능을 사용할 수 있습니다. 예를 들어 테마를 변경 하려면 다음 단계를 수행할 수 있습니다.

1. 브라우저에서로 이동 [http://Bootswatch.com](http://Bootswatch.com)테마를 선택한 후 클릭 **다운로드**합니다. (그러면 다운로드 *bootstrap.min.css* 기본적으로 CSS 코드를 검사 하려는 경우 가져올 *bootstrap.css* 축소 된 버전 대신 합니다.)
2. 다운로드 된 CSS 파일의 내용을 복사 합니다.
3. Visual Studio에서 만드는 새 **스타일 시트** 라는 파일 *부트스트랩 theme.css* 에 *콘텐츠* 에 코드 폴더 및 다운로드 한 CSS 붙여넣기 합니다.
4. 열기 *앱\_Start/Bundle.config* 변경 *bootstrap.css* 를 *부트스트랩 theme.css*합니다.

프로젝트를 다시 실행 하 고 응용 프로그램은 새로운 디자인입니다. 다음 그림 Amelia 테마의 효과 보여 줍니다.

![부트스트랩 Amelia 테마](creating-web-projects-in-visual-studio/_static/image20.png)

부트스트랩 자유자재로 사용할 수 있는 무료 및 프리미엄 버전입니다. 부트스트랩 제공 다양 한 UI 구성 요소와 같은 [드롭다운](http://twitter.github.io/bootstrap/components.html#dropdowns), [그룹 단추](http://twitter.github.io/bootstrap/components.html#buttonGroups), 및 [아이콘](http://twitter.github.io/bootstrap/base-css.html#images)합니다. 부트스트랩에 대 한 자세한 내용은 참조 [부트스트랩 사이트](http://twitter.github.io/bootstrap/)합니다.

Visual Studio에서 Web Forms 디자이너를 사용 하는 경우 note 부트스트랩 테마 또는 반응 형 레이아웃 변경의 모든 작업이 정확 하 게 표시 하지 않는 디자이너가 CSS3를 지원 하지 않습니다. 그러나 브라우저를 사용 하 여 볼 때 Web Forms 페이지 제대로 표시 됩니다.

<a id="add"></a>
## <a name="adding-support-for-additional-frameworks"></a>추가 프레임 워크에 대 한 지원 추가

서식 파일을 선택 하면 템플릿에서 사용 framework(s)에 대 한 확인란이 자동으로 선택 됩니다. 예를 들어, 선택 하는 경우는 **Web Forms** 서식 파일은 **Web Forms** 확인란이 선택 되며 선택 취소할 수 없습니다.

![서식 파일 선택](creating-web-projects-in-visual-studio/_static/image21.png)

![프레임 워크 추가](creating-web-projects-in-visual-studio/_static/image22.png)

프로젝트를 만들 때 해당 프레임 워크에 대 한 지원을 추가 하기 위해 서식 파일에 포함 되지 않은 프레임 워크에 대 한 확인란을 선택할 수 있습니다. 예를 들어, Web Forms를 사용 하도록 설정 하려면 *.aspx* 페이지 MVC 템플릿을 선택한 경우에 선택 된 **Web Forms** 확인란 합니다. Web Forms 서식 파일을 사용할 때 MVC을 사용 하려면 또는 **MVC** 확인란 합니다. 프레임 워크를 추가 하는 것은 실행 시간 뿐 아니라 디자인 타임 지원 합니다. 예를 들어 Web Forms 프로젝트에 MVC 지원을 추가 하면 경우에 컨트롤러와 뷰를 스 캐 폴드 수 있습니다.

Web Forms 및 MVC 프로젝트의 결합을 사용 하도록 설정 하면 [친화적 Url](http://www.hanselman.com/blog/IntroducingASPNETFriendlyUrlsCleanerURLsEasierRoutingAndMobileViewsForASPNETWebForms.aspx) Web Forms에 있을 수 있습니다 하지 라우팅 문제 URL을 한 개에 대상이 여러 개 예상 합니다. 먼저 정의 하는 경로의 우선을 적용 됩니다. 예를 들어 한 `Home` 컨트롤러와 *Home.aspx* 페이지는 `http://contoso.com/home` URL로 이동 됩니다 *Home.aspx* 호출 하는 경우는 `EnableFriendlyUrls` 는 를호출하기전에`MapRoute`에서 메서드 *RouteConfig.cs*, 하거나 동일한 URL 됩니다에 대 한 기본 보기로 이동 하 여 프로그램 `Home` 호출 하는 경우 컨트롤러 `MapRoute` 하기 전에 `EnableFriendlyUrls`합니다.

프레임 워크를 추가 하는 모든 샘플 응용 프로그램의 기능을 추가 되지 않습니다. Web Forms 지원 MVC 템플릿에서 더 선택 했으면 추가 하는 경우에 예를 들어 *Default.aspx* 홈 페이지 파일이 만들어집니다. 폴더, 파일 및 프레임 워크를 지 원하는 데 필요한 참조가 추가 됩니다. 따라서 프레임 워크를 추가 하면 코드는 템플릿에서 생성 하는 예제 응용 프로그램에 의해 구현 되는 인증 옵션을 변경 되지 않습니다. 예를 들어 빈 템플릿을 선택 하 고 추가 하는 경우 MVC 또는 Web Forms 지원는 **인증 구성** 단추가 비활성화 계속 됩니다.

다음 섹션에서는 각 확인란의 효과 간략하게 기술 합니다.

### <a name="add-web-forms-support"></a>Web Forms 지원 추가

빈 만듭니다 *앱\_데이터* 및 *모델* 폴더 및 *Global.asax* 파일입니다. Web Forms 확인란을 선택 하면 차이가 없습니다. 다른 템플릿에 대해 하므로 이미 빈 서식 파일 이외의 모든 서식 파일에서 작성 됩니다.

Web Forms 서식 파일을 활성화 하 여 친화적 Url 기본적으로 Web Forms 친화적 Url을 자동으로 활성화 되지 Web Forms 확인란을 선택 하 여 다른 서식 파일을 지원 합니다. 추가 합니다.

### <a name="add-mvc-support"></a>MVC 지원 추가

MVC, Razor, 및 웹 페이지 NuGet 패키지 설치, 빈 만듭니다 *앱\_데이터*, *컨트롤러*, *모델*, 및 *뷰*폴더를 만듭니다 *앱\_시작* 폴더 *RouteConfig.cs* 파일을 만들고 *Global.asax* 파일입니다.

### <a name="add-web-api-support"></a>추가 웹 API 지원

WebApi 및 Newtonsoft.Json NuGet 패키지 설치, 빈 만듭니다 *앱\_데이터*, *컨트롤러*, 및 *모델* 폴더를 만듭니다  *응용 프로그램\_시작* 폴더 *WebApiConfig.cs* 파일을 만들고 *Global.asax* 파일입니다.

<a id="auth"></a>
## <a name="authentication-methods"></a>인증 방법

Visual Studio 2013에서는 Web Forms, MVC 및 Web API 템플릿에 대 한 몇 가지 인증 옵션을 제공합니다.

- [인증 안 함](#noauth)
- [개별 사용자 계정](#indauth) (이전 ASP.NET 멤버 자격에는 ASP.NET Identity)
- [조직 계정](#orgauth) (Windows Server Active Directory 또는 Azure Active Directory)
- [Windows 인증](#winauth) (인트라넷)

![인증 대화 상자를 구성 합니다.](creating-web-projects-in-visual-studio/_static/image23.png)

<a id="noauth"></a>

### <a name="no-authentication"></a>인증 안 함

선택 하는 경우 **인증 안 함**더 사용자가 로그인을 나타내는 UI 없는 엔터티는 멤버 자격 데이터베이스 및 멤버 자격 데이터베이스에 대 한 연결 문자열에 대 한을 클래스, 예제 응용 프로그램에 로그인 하기 위한 웹 페이지가 포함 됩니다.

<a id="indauth"></a>
### <a name="individual-user-accounts"></a>개별 사용자 계정

선택 하는 경우 **개별 사용자 계정**, 사용자 인증을 위한 예제 응용 프로그램을 ASP.NET Id (이전의 ASP.NET 멤버 자격)를 사용 하도록 구성 됩니다. ASP.NET Id 사용자를 Facebook, Google, Microsoft 계정 또는 Twitter와 같은 소셜 공급자를 사용 하 여 로그인 하거나 사이트에서 사용자 이름 및 암호를 만들거나 계정을 등록할 수 있습니다. ASP.NET Identity에서 사용자 프로필에 대 한 기본 데이터 저장소는 SQL Server LocalDB 데이터베이스를 프로덕션 사이트에 대 한 SQL Server 또는 Azure SQL 데이터베이스에 배포할 수 있습니다.

Visual Studio 2013의 이러한 기능은 Visual Studio 2012에서와 동일 하지만 ASP.NET 멤버 자격 시스템에 대 한 기본 코드는 다시 작성 되었습니다. 새 코드 베이스의 장점은 다음과 같습니다.

- 새 멤버 자격 시스템 기반 [OWIN](http://owin.org/) ASP.NET 폼 인증 모듈 대신 합니다. 즉, IIS에서 MVC 또는 Web Forms를 사용 하 든 웹 API 또는 SignalR를 자체 호스트 하 고 있는 동일한 인증 메커니즘을 사용할 수 있습니다.
- Entity Framework Code First에서 관리 하는 새 멤버 자격 데이터베이스 및 모든 테이블을 수정할 수 있는 엔터티 클래스로 표현 됩니다. 즉, 데이터베이스 스키마와 프로필 관련 웹 UI 자신의 요구에 맞게 쉽게 사용자 지정할 수 있으며 Code First 마이그레이션을 사용 하 여 업데이트를 쉽게 배포할 수 있습니다.

새 서식 파일에 새 멤버 자격 시스템을 자동으로 구현 하 고.NET 4.5를 대상으로 하는 프로젝트에 수동으로 구현 이상이 될 수 있습니다.

ASP.NET Id는 외부 고객에 주로 인터넷 웹 사이트를 만드는 경우 좋은 선택 합니다. 조직에서 Active Directory 또는 Office 365 및 있습니다 직원 및 비즈니스 파트너에 대 한 단일 로그온 수 있도록 하는 프로젝트를 만들려고 할 경우는 **조직 계정** 옵션에 더 적합할 수 있습니다.

개별 사용자 계정 옵션에 대 한 자세한 내용은 다음 리소스를 참조 합니다.

- [www.asp.net/identity](../../../identity/index.md)합니다. ASP.NET 웹 사이트에서 ASP.NET Identity에 대 한 설명서입니다.
- [Facebook, Google OAuth2 및 OpenID 로그온 ASP.NET MVC 5 앱을 만드는](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)합니다. 또한 사용자 프로필 데이터를 사용자 지정 하는 방법을 보여 줍니다.
- [웹 API-외부 인증 서비스](../../../web-api/overview/security/external-authentication-services.md)
- [Visual Studio 2013에서 ASP.NET 응용 프로그램에 외부 로그인을 추가합니다.](https://blogs.msdn.com/b/webdev/archive/2013/06/27/adding-external-logins-to-your-asp-net-application-in-visual-studio-2013.aspx)

<a id="orgauth"></a>
### <a name="organizational-accounts"></a>조직 계정

선택 하는 경우 **조직 계정**, 샘플 응용 프로그램에서 Azure Active Directory (Azure AD Office 365를 포함 하는) 사용자 계정 기반 인증에 대해 Windows Identity Foundation (WIF)를 사용 하도록 구성 됩니다 또는 Windows Server Active Directory 자세한 내용은 참조 [조직 계정 인증 옵션](#orgauthoptions) 이 항목의 뒷부분에 나오는 합니다.

<a id="winauth"></a>
### <a name="windows-authentication"></a>Windows 인증

선택 하는 경우 **Windows 인증**, 샘플 응용 프로그램 인증에 대 한 Windows 인증 IIS 모듈을 사용 하도록 구성 됩니다. 응용 프로그램 도메인 및 사용자 ID가 Windows에 로그인 하지만 않습니다 포함 사용자 등록 하거나 로그인 UI는 로컬 컴퓨터 계정 또는 Active directory의 표시 됩니다. 이 옵션은 인트라넷 웹 사이트에 대 한 것입니다.

또는 선택 하 여 AD 인증을 사용 하는 인트라넷 사이트를 만들 수는 [온-프레미스 조직 계정에서 옵션](#orgauthonprem)합니다. 온-프레미스 옵션 Windows 인증 모듈 대신 Windows Identity Foundation (WIF)를 사용합니다. 온-프레미스 옵션을 설정 하는 데 필요한 몇 가지 추가 단계가 있지만 WIF Windows 인증 모듈과 함께 사용할 수 없는 기능을 사용할 수 있습니다. 예를 들어 wif 디렉터리 데이터 쿼리 및 Active Directory에에서 응용 프로그램 액세스를 구성할 수 있습니다.

<a id="orgauthoptions"></a>
## <a name="organizational-account-authentication-options"></a>조직 계정 인증 옵션

**인증 구성** 이 대화 상자에서는 Azure Active Directory (Azure AD Office 365 포함) 또는 Windows Server Active Directory (AD) 계정 인증에 대 한 몇 가지 옵션:

- [클라우드-단일 조직](#orgauthsingle) (Azure AD 또는 Azure AD와 디렉터리 통합을 사용 하 여 AD)
- [클라우드-다중 조직](#orgauthmulti) (Azure AD 또는 Azure AD와 디렉터리 통합을 사용 하 여 AD)
- [온-프레미스](#orgauthonprem) (AD)

Azure AD 옵션 중 하나를 시도 하지만 계정이 아직 없는 경우 [Azure AD 계정에 등록 하려면 여기를 클릭 하십시오.](https://go.microsoft.com/fwlink/?LinkId=309942)합니다.

> [!NOTE]
> Azure AD 옵션 중 하나를 선택 하면 프로젝트에 필요한 데이터베이스 및 Azure AD 테 넌 트에 대 한 전역 관리자 계정에 로그인 해야 합니다. 조직 계정에 대 한 이름 및 암호를 입력 (예를 들어 admin@contoso.onmicrosoft.com) Azure AD 테 넌 트에 대 한 관리 권한이 있는 합니다.
> 
> **Microsoft 계정에 대 한 자격 증명을 입력 하지 마세요 (예를 들어 contoso@hotmail.com) 로그인 대화 상자에서.**


<a id="orgauthsingle"></a>
### <a name="cloud---single-organization-authentication"></a>클라우드-단일 조직에 인증

![단일 조직에 인증](creating-web-projects-in-visual-studio/_static/image24.png)

하나의 Azure AD에 정의 된 사용자 계정에 대 한 인증을 사용 하도록 설정 하려는 경우이 옵션을 선택 [테 넌 트](https://technet.microsoft.com/en-us/library/jj573650.aspx)합니다. 예를 들어 사이트는 contoso.com 및 해당 사용 가능 하 게 contoso.onmicrosoft.com 테 넌 트 내에 있는 Contoso 회사의 직원에 게 합니다. Azure AD 사용자가 다른 테 넌 트 응용 프로그램에 액세스를 허용 하도록 구성할 수 없습니다.

#### <a name="domain"></a>도메인

예를 들어, 응용 프로그램을 설정 하려면 Azure AD 도메인을 입력 하세요: `contoso.onmicrosoft.com`합니다. 있는 경우는 [사용자 지정 도메인](http://www.cloudidentity.com/blog/2013/04/14/adding-a-custom-domain-to-your-windows-azure-ad/)와 같은 `contoso.com` 대신 `contoso.onmicrosoft.com`, 여기에 입력 수 있습니다.

#### <a name="access-level"></a>액세스 수준

응용 프로그램 쿼리 또는 Graph API를 사용 하 여 디렉터리 정보 업데이트를 선택 하는 경우 **Single Sign-on, 디렉터리 데이터 읽기** 또는 **Single Sign On, 읽기 및 쓰기 디렉터리 데이터**합니다. 그렇지 않은 경우, 선택 **Single Sign On**합니다. 자세한 내용은 참조 [응용 프로그램 액세스 수준을](https://msdn.microsoft.com/en-us/library/windowsazure/b08d91fa-6a64-4deb-92f4-f5857add9ed8#BKMK_AccessLevels) 및 [쿼리 Azure AD Graph API를 사용 하 여](https://msdn.microsoft.com/en-US/library/windowsazure/dn151791.aspx)합니다.

#### <a name="application-id-uri"></a>응용 프로그램 ID URI

기본적으로 템플릿은 Azure AD 도메인에 프로젝트 이름을 추가 하 여 사용자에 대 한 응용 프로그램 ID URI를 만듭니다. 예를 들어 프로젝트 이름이 `Example` 도메인은 `contoso.onmicrosoft.com`, 응용 프로그램 ID URI가 `https://contoso.onmicrosoft.com/Example`합니다. 응용 프로그램 ID URI를 수동으로 지정 하려는 경우 확장 된 **기타 옵션** 섹션 및 텍스트 상자에 응용 프로그램 ID URI를 입력 합니다. 응용 프로그램 ID URI로 시작 해야 `https://`합니다.

기본적으로 이미 Azure AD에서 프로 비전 하는 응용 프로그램 프로젝트에 대 한 Visual Studio에서 사용 하는 것과 동일한 응용 프로그램 ID URI 있으면 프로젝트에 연결할 새 프로 비전 하는 대신 기존 응용 프로그램입니다. 이 경우 프로 비전 할 새 응용 프로그램 해제는 **이미 동일한 ID를 사용 하는 경우 응용 프로그램 항목 덮어쓰기** 확인란 합니다.

경우는 **덮어쓰기** 확인란의 선택을 취소 하 고 Visual Studio 같은 응용 프로그램 ID URI와 기존 응용 프로그램을 찾고, 사용 하려는 URI에 숫자를 추가 하 여 새 URI를 만듭니다. 예를 들어 프로젝트 이름이 `Example`, 팁 텍스트 상자에 아무, 선택을 취소 하면는 **덮어쓰기** 확인란 및 Azure AD 테 넌 트 URI와 응용 프로그램에 이미 `https://contoso.onmicrosoft.com/Example`합니다. 이 경우 새 응용 프로그램 프로 비전 할 ID URI와 같은 응용 프로그램으로 `https://contoso.onmicrosoft.com/Example_20130619330903`합니다.

#### <a name="provisioning-the-application-in-azure-ad"></a>Azure AD에서 응용 프로그램 프로 비전

Visual Studio을 Azure AD에서 응용 프로그램을 프로 비전 하거나 기존 응용 프로그램 프로젝트를 연결할 도메인의 전역 관리자 자격 증명이 필요 합니다. 클릭할 때 **확인** 에 **인증 구성** 대화 상자에서 사용자 이름 및 지정한 도메인에 대 한 전역 관리자의 암호에 대 한 메시지가 표시 됩니다. 나중에 클릭할 때 **프로젝트 만들기** 에 **새 ASP.NET 프로젝트** 대화 상자에서 Visual Studio에서 Azure AD 응용 프로그램을 프로 비전 합니다. 이 프로세스의 일부로 Visual Studio에서는 클라이언트 비밀 값 1 년을 만든 후에 만료 되는 Web.config 파일에서 note 합니다.

사용 하는 응용 프로그램을 만드는 방법에 대 한 내용은 **클라우드-단일 조직** 인증을 다음 리소스를 참조 합니다.

- [Azure 인증](../2012/windows-azure-authentication.md)
- [Azure AD를 사용 하 여 웹 응용 프로그램에 로그온 기능 추가](https://msdn.microsoft.com/library/windowsazure/dn151790.aspx)
- [Azure Active Directory와 ASP.NET 앱 개발](../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)
- [Azure AD와 ASP.NET 웹 API 보안 및 Microsoft OWIN 구성 요소](https://msdn.microsoft.com/en-us/magazine/dn463788.aspx)

자습서에서는 Visual Studio 2013;에 대 한 아직 업데이트 되지 않았습니다. Visual Studio 2013에서 수동으로 작업을 수행할 수 있는 자습서 직접 일부 자동화 합니다.

<a id="orgauthmulti"></a>
### <a name="cloud---multi-organization-authentication"></a>클라우드-다중 조직 인증

![여러 조직 인증](creating-web-projects-in-visual-studio/_static/image25.png)

여러 Azure AD에 정의 된 사용자 계정에 대 한 인증을 사용 하도록 설정 하려는 경우이 옵션을 선택 [테 넌 트](https://technet.microsoft.com/en-us/library/jj573650.aspx)합니다. 예를 들어 사이트는 contoso.com 및 그 사용 가능 하 게 contoso.onmicrosoft.com 테 넌 트, Contoso 회사의 직원이 Fabrikam 회사의 직원 fabrikam.onmicrosoft.com 테 넌 트에서 합니다.

입력 하는 설정 및 단계 프로 비전 응용 프로그램은 비슷합니다 [단일 조직 인증](#orgauthsingle)합니다.

사용 하는 응용 프로그램을 만드는 방법에 대 한 내용은 **클라우드-다중 조직** 인증을 다음 리소스를 참조 합니다.

- [ASP.NET, Azure Active Directory와의 손쉬운 웹 응용 프로그램 통합 &amp; Visual Studio](https://blogs.msdn.com/b/active_directory_team_blog/archive/2013/06/26/improved-windows-azure-active-directory-integration-with-asp-net-amp-visual-studio.aspx) Active Directory 팀 블로그.
- [Azure AD 사용한 다중 테 넌 트 웹 응용 프로그램 개발](https://msdn.microsoft.com/en-us/library/windowsazure/dn151789.aspx) 자습서입니다. 이 자습서는 Visual Studio 2013; 아직 업데이트 되지 않은 Visual Studio 2013에서 자동화 되어 일부 기능 자습서 지시 수동으로 작업을 수행할 수 있습니다.
- [로그인 하려면 사용자 고유의 여러 조직에서는 ASP.NET 응용 프로그램으로 등록 해야](http://www.cloudidentity.com/blog/2013/10/26/you-have-to-sign-up-with-your-own-multiple-organizations-asp-net-app-before-you-can-sign-in/)합니다. 블로그에 올린 Vittorio Bertocci 일반적인 문제 사람을 해결 하는 방법에 설명 하는 다중 조직 인증을 사용 하는 프로젝트를 만들 때 발생 합니다.

<a id="orgauthonprem"></a>
### <a name="on-premises-organizational-authentication"></a>온-프레미스 조직 인증

![온-프레미스 조직 인증](creating-web-projects-in-visual-studio/_static/image26.png)

Windows Server AD (Active Directory), 정의 된 사용자 계정에 대 한 인증을 사용 하도록 설정 하 고 Azure AD를 사용 하지 않으려는 경우이 옵션을 선택 합니다. 인트라넷 사이트 또는 인터넷 사이트를 만들려면이 옵션을 사용할 수 있습니다. 가 인터넷 사이트에 대 한 페더레이션 서비스 ADFS (Active Directory)를 사용 하 여 AD에 대 한 액세스를 제공 합니다. 자세한 내용은 참조 [온-프레미스 조직 인증 옵션 (ADFS)으로 ASP.NET을 사용 하 여 Visual Studio 2013에서](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)합니다.

인트라넷 사이트에 대 한 대안 선택할 수 있는 [Windows 인증](#winauth) 이 옵션 대신 합니다. Windows 인증 옵션에 대 한 메타 데이터 문서 URL을 제공할 필요가 없습니다. 그러나 Windows 인증 기능은 제공 되지 않습니다 있습니다는 Active Directory에 응용 프로그램 액세스를 제어 하거나 디렉터리 데이터를 쿼리 합니다.

#### <a name="on-premises-authority"></a>온-프레미스 기관

메타 데이터 문서를 가리키는 URL을 입력 합니다. 메타 데이터 문서 기관의 좌표가 포함 되어 있습니다. 응용 프로그램 웹 로그온 흐름을 진행 하는 데 이러한 좌표를 사용 합니다.

#### <a name="application-id-uri"></a>응용 프로그램 ID URI

AD는이 응용 프로그램을 식별 하거나 Visual Studio를 하나 만들 수 있도록 비워 하는 데 사용할 수 있는 고유 URI를 제공 합니다.

<a id="nextsteps"></a>
## <a name="next-steps"></a>다음 단계

이 문서는 Visual Studio 2013에서 새 ASP.NET 웹 프로젝트를 만들기 위한 몇 가지 기본적인 도움말을 제공 했습니다. Visual studio 웹 개발을 위한 사용 하는 방법에 대 한 자세한 내용은 참조 [https://www.asp.net/visual-studio/](../../index.md)합니다.
