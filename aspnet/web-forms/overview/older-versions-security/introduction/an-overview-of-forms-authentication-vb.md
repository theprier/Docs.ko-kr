---
uid: web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-vb
title: 폼 인증 (VB)의 개요 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 낮 단순한 토론에서 구현을 제공 합니다. 특히, 폼 인증을 구현 살펴봅니다. 웹 응용 프로그램 w 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/14/2008
ms.topic: article
ms.assetid: 83267f7d-64d9-41ee-82cf-da91b1bf534d
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: 6482b10a470b50a1fc6f163ee2d59682e83f5a2b
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="an-overview-of-forms-authentication-vb"></a>폼 인증 (VB)의 개요
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/ASPNET_Security_Tutorial_02_VB.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/aspnet_tutorial02_FormsAuth_vb.pdf)

> 이 자습서에서는 낮 단순한 토론에서 구현을 제공 합니다. 특히, 폼 인증을 구현 살펴봅니다. 이 자습서의 생성을 시작 하는 웹 응용 프로그램 멤버 자격 및 역할에 간단한 폼 인증에서 이동 했습니다 후속 자습서를 기반으로 구축 계속 됩니다.
> 
> 이 항목에 자세한 내용은이 비디오를 참조 하십시오: [ASP.NET에서 사용 하 여 기본 폼 인증](# "using-basic-forms-authentication-in-aspnet")합니다.


## <a name="introduction"></a>소개

에 [이전 자습서](security-basics-and-asp-net-support-vb.md) ASP.NET에서 제공 되는 다양 한 인증, 권한 및 사용자 계정 옵션에 설명 했습니다. 이 자습서에서는 낮 단순한 토론에서 구현을 제공 합니다. 특히, 폼 인증을 구현 살펴봅니다. 이 자습서의 생성을 시작 하는 웹 응용 프로그램 멤버 자격 및 역할에 간단한 폼 인증에서 이동 했습니다 후속 자습서를 기반으로 구축 계속 됩니다.

이 자습서에서는 이전 자습서에서 시 작업 항목 폼 인증 워크플로에 대해 심층적으로 시작 합니다. 그런 다음, 데모 폼 인증의 개념을 통해 ASP.NET 웹 사이트를 만듭니다. 다음으로, 우리는 사이트를 구성 하 폼 인증을 사용 하 고, 간단한 로그인 페이지를 만들고, 여부를 확인, 코드에서 사용자가 인증,이 경우 사용자 이름을 변경 내용이 기록 하는 방법을 참조 합니다.

인증 워크플로에 웹 응용 프로그램에서 사용 하 고 로그인 / 로그 오프 페이지 만들기 사용자 계정을 지원 하 고 웹 페이지를 통해 사용자를 인증 하는 ASP.NET 응용 프로그램을 만드는 모든 중요 한 단계는 폼을 이해 합니다. 따라서-및 이러한 자습서를-서로 기반으로 작성 하므로 바랍니다 지난 프로젝트의 폼 인증 이미 러 웠 환경을 구성 하는 경우에 다음 단계로 넘어가기 전에 전체에서이 자습서를 통해 사용할 수 있습니다.

## <a name="understanding-the-forms-authentication-workflow"></a>폼 인증 워크플로 이해합니다.

ASP.NET 런타임, ASP.NET 페이지 또는 ASP.NET 웹 서비스 같은 ASP.NET 리소스에 대 한 요청을 처리할 때 요청 된 수의 이벤트 수명 주기 동안 발생 합니다. 요청이 인증 되 고 권한이 부여 된, 처리 되지 않은 예외 및 기타의 경우 발생 하는 이벤트 있을 때 발생 하는 스토리는 요청을 시작 하 고 매우 끝날 때 발생 하는 이벤트 있습니다. 이벤트의 전체 목록을 보려면, 참조는 [HttpApplication 개체의 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication_events.aspx)합니다.

*HTTP 모듈* 는 관리 되는 클래스는 요청 수명에 특정 이벤트에 해당 코드가 실행 됩니다. ASP.NET 원리를 자세히 파악할수록 필수 작업을 수행 하는 HTTP 모듈의 수와 함께 제공 합니다. 특히 관련 논의 하는 두 개의 기본 제공 HTTP 모듈은:

- **[FormsAuthenticationModule](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)**  -일반적으로 사용자의 쿠키 컬렉션에 포함 된 폼 인증 티켓을 검사 하 여 사용자를 인증 합니다. 폼 인증 티켓 없는 있는 경우 사용자가 익명입니다.
- **[UrlAuthorizationModule](https://msdn.microsoft.com/library/system.web.security.urlauthorizationmodule.aspx)**  -현재 사용자가 요청 된 URL에 액세스를 권한이 있는지 여부를 결정 합니다. 이 모듈 응용 프로그램의 구성 파일에 지정 된 권한 부여 규칙을 참고 하 여 권한을 결정 합니다. ASP.NET도 포함 되어는 [FileAuthorizationModule](https://msdn.microsoft.com/library/system.web.security.fileauthorizationmodule.aspx) 기관 요청한 파일 Acl을 참고 하 여 결정 하는 합니다.

FormsAuthenticationModule 실행 UrlAuthorizationModule (및 FileAuthorizationModule) 하기 전에 사용자를 인증 하려고 시도 합니다. 권한 부여 모듈은 요청을 종료 하 고이 반환 요청을 만드는 사용자는 요청 된 리소스에 액세스할 수 있는 권한이 없는, 경우는 [HTTP 401 권한이 없음](http://www.checkupdown.com/status/E401.html) 상태입니다. Windows 인증 시나리오에서 HTTP 401 상태는 브라우저에 반환 됩니다. 이 상태 코드에는 모달 대화 상자를 통해 자격 증명을 묻는 브라우저를 발생 합니다. 하지만 폼 인증을 사용 HTTP 401 권한이 없음 상태로 전송 되지 않습니다는 브라우저는 FormsAuthenticationModule이이 상태를 검색 하 고 대신 로그인 페이지에는 사용자를 리디렉션합니다 수정 하기 때문에 (통해는 [HTTP 302 리디렉션](http://www.checkupdown.com/status/E302.html) 상태).

로그인 페이지의 책임 경우 사용자의 자격 증명이 유효 하 고,이 경우 폼 인증 티켓을 만들고 사용자 페이지에 다시 리디렉션할 있습니다 하 려 했던 방문을 결정 하는 것입니다. 인증 티켓이 FormsAuthenticationModule 사용 하 여 사용자를 식별 하는 웹 사이트에 있는 페이지에 대 한 후속 요청에 포함 됩니다.


[![폼 인증 워크플로](an-overview-of-forms-authentication-vb/_static/image2.png)](an-overview-of-forms-authentication-vb/_static/image1.png)

**그림 01**: The Forms 인증 워크플로 ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image3.png))


### <a name="remembering-the-authentication-ticket-across-page-visits"></a>방문 페이지에서 인증 티켓을 기억

로그인 한 후 사이트를 찾아볼 때 사용자에 게 로그인 유지 되도록 각 요청에 대해 웹 서버에 다시 폼 인증 티켓을 전송 합니다. 이 사용자의 쿠키 컬렉션에 인증 티켓을 배치 하 여 일반적으로 수행 됩니다. [쿠키](http://en.wikipedia.org/wiki/HTTP_cookie) 은 사용자의 컴퓨터에 있으며 쿠키 만든 웹 사이트에 각 요청에서 HTTP 헤더에서 전송 되는 작은 텍스트 파일입니다. 따라서 폼 인증 티켓 생성 되 고 브라우저의 쿠키에 저장 된, 일단 각 후속 방문 해당 사이트에 사용자를 식별 하 여 요청과 함께 인증 티켓을 보냅니다.

> [!NOTE]
> 각 자습서에 사용 된 데모 웹 응용 프로그램 다운로드로 제공 됩니다. 이 다운로드 가능한 응용 프로그램은 Visual Web Developer 2008에 대 한.NET Framework 버전 3.5 대상으로 만들어졌습니다. 응용 프로그램,.NET 3.5에 대 한 대상 이후 해당 Web.config 파일에 추가, 3.5 관련 구성 요소가 포함 됩니다. 아직 다운로드 가능한 웹 응용 프로그램이 다음 컴퓨터에.NET 3.5를 설치 하는 경우에 간단히 3.5 관련 태그를 Web.config에서 제거 하지 않고 작동 하지 않습니다.


쿠키의 한 가지 측면은 날짜 및 시간을 브라우저 쿠키를 삭제 하는 만료 기한을입니다. 폼 인증 쿠키가 만료 되 면 사용자 인증 되 고 따라서 익명 될 더 이상 수 없습니다. 공용 터미널에서 사용자가 방문 하는 브라우저를 닫도록 때 만료 되도록 인증 티켓의 원하는 가능성 됩니다. 그러나 재택에서을 방문할 때 같은 사용자 수도 인증 티켓 보유 하지 않는 브라우저를 다시 시작할 주의 해야 할 사이트를 방문할 때마다 다시 로그인 합니다. 로그인 페이지에는 메일 주소 저장 확인란의 양식에서 사용자가이 결정 종종 이루어집니다. 3 단계에서에서 로그인 페이지에서 암호 저장 확인란을 구현 하는 방법을 살펴보겠습니다. 다음 자습서 인증 티켓 시간 제한 설정을 자세히 다룹니다.

> [!NOTE]
> 있기 웹 사이트에 로그온 하는 데 사용 하는 사용자 에이전트 쿠키를 지원 하지 않을 수 있습니다. 이 경우 ASP.NET cookieless 폼 인증 티켓을 사용할 수 있습니다. 이 모드에서는 인증 티켓의 URL로 인코딩됩니다. 쿠키 인증 티켓을 사용할 때와 만들고 다음 자습서에서 관리 되는 방법을 살펴보겠습니다.


### <a name="the-scope-of-forms-authentication"></a>폼 인증의 범위

관리 되는 FormsAuthenticationModule ASP.NET 런타임에 속하지 즉 코드. Microsoft의의 버전 7 이전 [인터넷 정보 서비스 (IIS)](https://www.iis.net/) 웹 서버 IIS의 HTTP 파이프라인 및 파이프라인 ASP.NET 런타임 간의 고유한 장벽 했습니다. 즉, IIS 6 및 이전 버전에서는 요청은 IIS에서 ASP.NET 런타임이에 위임 됩니다는 FormsAuthenticationModule만 실행 합니다. 기본적으로 IIS 정적 콘텐츠 자체-HTML 페이지 및 CSS 및 이미지 파일-요청 넘깁니다 때만 같은 ASP.NET 런타임에.aspx,.asmx 또는.ashx의 확장 된 페이지를 요청 하는 경우를 처리 합니다.

그러나 IIS 7 허용 통합된 IIS 및 ASP.NET 파이프라인 합니다. 몇 가지 구성 설정을 사용 하 여 IIS 7에 대 한 FormsAuthenticationModule 호출을 설정할 수 있습니다 *모든* 요청 합니다. 또한 IIS 7과 함께 모든 형식의 파일에 대 한 URL 권한 부여 규칙을 정의할 수 있습니다. 자세한 내용은 참조 [IIS6 사이의 변경 내용 및 IIS7 보안](https://www.iis.net/learn/get-started/whats-new-in-iis-7/changes-in-security-between-iis-60-and-iis-7-and-above), [웹 플랫폼 보안](https://www.iis.net/learn/get-started/whats-new-in-iis-7/iis7-and-above-security-improvements), 및 [이해 IIS7 URL 권한 부여](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/URL-Authorization/Understanding-IIS7-URL-Authorization)합니다.

말해서, IIS 7 이전 버전에서는, ASP.NET 런타임에 의해 처리 되는 리소스를 보호 하기 위해 폼 인증을만 사용할 수 있습니다. 마찬가지로, URL 권한 부여 규칙은 ASP.NET 런타임에 의해 처리 되는 리소스에만 적용 됩니다. 그러나 IIS 7 FormsAuthenticationModule 및 UrlAuthorizationModule 하므로 모든 요청에이 기능을 확장 되는 IIS의 HTTP 파이프라인에 통합할 수 있습니다.

## <a name="step-1-creating-an-aspnet-website-for-this-tutorial-series"></a>1 단계:이 자습서 시리즈에 대 한 ASP.NET 웹 사이트 만들기

Visual Studio 2008의 Microsoft의 무료 버전으로 생성 됩니다이 시리즈 작성할 ASP.NET 웹 사이트 많은 달성 하기 위해 [Visual Web Developer 2008](https://www.microsoft.com/express/vwd/)합니다. 구현 해 서 SqlMembershipProvider 사용자 저장소에는 [Microsoft SQL Server 2005 Express Edition](https://msdn.microsoft.com/sql/Aa336346.aspx) 데이터베이스입니다. Visual Studio 2005 또는 다른 버전의 Visual Studio 2008 또는 SQL Server를 사용 하는 경우 걱정 하지 마십시오-단계 거의 동일 하 게 됩니다 하 고 모든 특수 차이점 지적 합니다.

폼 인증을 구성 하 여 ASP.NET 웹 사이트 먼저 해야 합니다. 먼저 새 파일 시스템 기반 ASP.NET 웹 사이트를 만듭니다. 이를 위해 Visual Web Developer를 시작 하 파일 메뉴로 이동 하 고 새 웹 사이트 대화 상자를 표시 하는 새 웹 사이트를 선택 합니다. ASP.NET 웹 사이트 템플릿을 선택, 파일 시스템으로 위치 드롭 다운 목록 설정, 웹 사이트를 배치할 폴더를 선택 및 언어 VB.로 설정 새 웹 사이트를 응용 프로그램 Default.aspx ASP.NET 페이지와 이때\_데이터 폴더 및 Web.config 파일입니다.

> [!NOTE]
> Visual Studio 프로젝트 관리의 두 모드를 지원: 웹 사이트 프로젝트와 웹 응용 프로그램 프로젝트입니다. 웹 사이트 프로젝트는 웹 응용 프로그램 프로젝트를 Visual Studio.NET 2002/2003에서 프로젝트 아키텍처 모방-프로젝트 파일을 포함 하 고 /bin 폴더에 있는 단일 어셈블리로 프로젝트의 소스 코드를 컴파일할 때 반면 프로젝트 파일을 부족 합니다. Visual Studio 2005 처음만 지원 되는 웹 사이트 프로젝트, 서비스 팩 1; 웹 응용 프로그램 프로젝트 모델이 다시 발생 하지만 Visual Studio 2008 둘 다 프로젝트 모델을 제공 합니다. 그러나 Visual Web Developer 2005 및 2008 edition만 지원 웹 사이트 프로젝트. 웹 사이트 프로젝트 모델을 사용 하겠습니다. Express 이외의 버전을 사용 하는 경우를 사용 하려는 [웹 응용 프로그램 프로젝트 모델](https://msdn.microsoft.com/library/aa730880(vs.80).aspx) 대신 자유롭게 있을 수 있음을 약간 다 화면 및 비교 수행 해야 하는 단계에 표시 되는 내용 간에 수 있지만 이렇게는 표시 된 스크린 샷 및이 자습서에 제공 된 지침.


[![새 파일 시스템 기반 웹 사이트 만들기](an-overview-of-forms-authentication-vb/_static/image5.png)](an-overview-of-forms-authentication-vb/_static/image4.png)

**그림 02**: New File System-Based 웹 사이트 만들기 ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image6.png))


### <a name="adding-a-master-page"></a>마스터 페이지 추가

다음을 새 마스터 페이지 Site.master 명명 된 루트 디렉터리에 있는 사이트에 추가 합니다. [마스터 페이지](https://msdn.microsoft.com/library/wtxbf3hh.aspx) 페이지 개발자는 ASP.NET 페이지에 적용할 수 있는 사이트 수준 템플릿 정의를 사용 합니다. 마스터 페이지의 주요 장점은 사이트의 전반적인 모양을 정의할 수 있다는 단일 위치에 쉽게 업데이트 하거나 사이트의 레이아웃을 조정 하도록입니다.


[![마스터 페이지를 추가할 웹 사이트에 Site.master 라는](an-overview-of-forms-authentication-vb/_static/image8.png)](an-overview-of-forms-authentication-vb/_static/image7.png)

**그림 03**: 마스터 페이지 라는 Site.master 웹 사이트에 추가 ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image9.png))


마스터 페이지의 여기 사이트 전체 페이지 레이아웃을 정의 합니다. 디자인 뷰를 사용 하 고 필요한 모든 레이아웃 또는 웹 컨트롤을 추가 하거나 직접 소스 뷰에서 태그를 수동으로 추가할 수 있습니다. 내 마스터 페이지의 레이아웃에 사용 되는 레이아웃을 모방 하기 위해 구조 합니까 내 *[ASP.NET 2.0에서 데이터 작업을](../../data-access/index.md)* 자습서 시리즈 (그림 4 참조). 마스터 페이지를 사용 하 여 [스타일 시트](http://www.w3schools.com/css/default.asp) 위치 지정 (이 자습서의 관련된 다운로드에 포함)이 표시 된 Style.css 파일에 정의 된 CSS 설정 사용 하 여 스타일에 대 한 합니다. CSS 규칙을 정의 하는 동안 아래에 표시 된 태그에서 알 수 없습니다, 되도록 탐색 &lt;div&gt;의 왼쪽에 나타나고이 200 픽셀의 고정된 폭 있도록 절대 콘텐츠 위치로 지정 합니다.

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample1.aspx)]

마스터 페이지에는 정적 페이지 레이아웃 및 마스터 페이지를 사용 하는 ASP.NET 페이지에서 편집할 수 있는 영역을 모두 정의 합니다. 이러한 콘텐츠 편집 가능한 영역 콘텐츠 내에서 볼 수 있는 해당 ContentPlaceHolder 컨트롤에 의해 표시 됩니다 &lt;div&gt;합니다. 마스터 페이지 단일 ContentPlaceHolder (MainContent)을 갖지만 마스터 페이지의 여러 contentplaceholders의 있을 수 있습니다.

위에 입력 한 태그를 디자인 뷰로 전환 마스터 페이지의 레이아웃을 표시 됩니다. 이 마스터 페이지를 사용 하는 모든 ASP.NET 페이지 MainContent 영역에 대 한 태그를 지정 하는 기능과 함께이 균일 한 레이아웃을 갖습니다.


[![디자인 뷰를 통해 볼 때 마스터 페이지](an-overview-of-forms-authentication-vb/_static/image11.png)](an-overview-of-forms-authentication-vb/_static/image10.png)

**그림 04**: 마스터 페이지 때 볼 통해의 디자인 뷰 ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image12.png))


### <a name="creating-content-pages"></a>콘텐츠 페이지 만들기

이 시점에서 Default.aspx 페이지, 웹 사이트에 있는 있지만 방금 만든 마스터 페이지를 사용 하지 않습니다. 페이지 내용이 포함 되지 않은 경우 마스터 페이지를 사용 하는 웹 페이지의 선언적 태그를 조작할 수 있지만 아직 쉽습니다만 페이지를 삭제 하 고 다시 사용 하려면 마스터 페이지를 지정 하는 프로젝트에 추가 합니다. 따라서 프로젝트에서 Default.aspx를 삭제 하 여 시작 합니다.

그런 다음 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 Default.aspx 라는 새 Web Form을 추가 하려면 선택 합니다. 이 이번에 마스터 페이지 선택 확인란을 선택 하 고 목록에서 Site.master 마스터 페이지를 선택 합니다.


[![마스터 페이지를 선택 하도록 선택 하는 새 Default.aspx 페이지 추가](an-overview-of-forms-authentication-vb/_static/image14.png)](an-overview-of-forms-authentication-vb/_static/image13.png)

**그림 05**:는 새 Default.aspx 페이지 선택 마스터 페이지를 선택 하려면 추가 ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image15.png))


[![Site.master 마스터 페이지를 사용 하 여](an-overview-of-forms-authentication-vb/_static/image17.png)](an-overview-of-forms-authentication-vb/_static/image16.png)

**그림 06**: Site.master 마스터 페이지를 사용 하 여 ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image18.png))


> [!NOTE]
> 웹 응용 프로그램 프로젝트 모델을 사용 하는 경우 새 항목 추가 대화 상자에는 마스터 페이지 선택 확인란을 포함 되지 않습니다. 대신, 웹 콘텐츠 폼 형식의 항목을 추가 해야 합니다. 웹 콘텐츠 형식 옵션을 선택 하 고 추가 클릭 한 후 Visual Studio에는 동일한 Select는 마스터 표시 됩니다 대화 상자 그림 6에 나와 있습니다.


방금 새 Default.aspx 페이지의 선언적 태그를 포함 한 @Page 마스터에 대 한 경로 지정 하는 지시문 마스터 페이지의 MainContent ContentPlaceHolder에 대 한 파일 및 콘텐츠 컨트롤을 페이지.

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample2.aspx)]

지금은 Default.aspx를 비워 둡니다. 에서는 콘텐츠를 추가 하려면이 자습서의 뒷부분에 나오는를 반환 합니다.

> [!NOTE]
> 마스터 페이지 메뉴 또는 다른 탐색 인터페이스에 대 한 섹션을 포함합니다. 이후 자습서에서 이러한 인터페이스를 만듭니다.


## <a name="step-2-enabling-forms-authentication"></a>2 단계: 폼 인증을 사용 하도록 설정

ASP.NET 웹 사이트를 만든 폼 인증을 사용 하도록 설정 하는 다음 작업이입니다. 통해 응용 프로그램의 인증 구성이 지정 되어 있는 [ &lt;인증&gt; 요소](https://msdn.microsoft.com/library/532aee0e.aspx) Web.config에 있습니다. &lt;인증&gt; 요소는 응용 프로그램에서 사용 되는 인증 모델을 지정 하는 모드 라는 단일 특성을 포함 합니다. 이 특성은 다음 네 가지 값 중 하나일 수 있습니다.

- **Windows** -는 방문자에 인증 해야 하는 웹 서버의 응용 프로그램에서 Windows 인증을 사용 하는 경우 이전 자습서에 설명 된 대로 하 고 기본, 다이제스트 또는 Windows 통합을 통해 일반적으로 이렇게 인증입니다.
- **Forms**-웹 페이지의 양식을 통해 사용자가 인증 됩니다.
- **Passport**-사용자는 Microsoft의 Passport 네트워크를 사용 하 여 인증 됩니다.
- **None**-모든 방문자가 익명 인지, 인증 모델이 사용 됩니다.

기본적으로 ASP.NET 응용 프로그램 Windows 인증을 사용 합니다. 인증 유형을 폼 인증을 변경 하려면 다음을 수정 해야는 &lt;인증&gt; 요소의 모드 특성 폼에 적용 합니다.

프로젝트에 아직 없는 경우 Web.config 파일을 추가 하나 이제에서 마우스 오른쪽 단추로 클릭 솔루션 탐색기에서 프로젝트 이름을, 새 항목 추가 선택 합니다. 다음 웹 구성 파일을 추가 합니다.


[![프로젝트에 아직 없는 경우 Web.config를 지금 추가](an-overview-of-forms-authentication-vb/_static/image20.png)](an-overview-of-forms-authentication-vb/_static/image19.png)

**그림 07**: 경우 Your 프로젝트는 하지 아직 포함 Web.config, 추가 지금 ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image21.png))


찾은 다음으로 &lt;인증&gt; 요소 및 폼 인증을 사용 하도록 업데이트 합니다. 이 변경 후 Web.config 파일의 태그는 다음과 비슷하게 표시 됩니다.

[!code-xml[Main](an-overview-of-forms-authentication-vb/samples/sample3.xml)]

> [!NOTE]
> Web.config는 XML 파일에 대/소문자 구분이 중요 합니다. 6. 대문자로 양식 모드 특성을 설정 되었는지 확인 서로 다른 대/소문자, 폼 등을 사용 하는 경우 브라우저를 통해 사이트를 방문할 때 구성 오류를 받게 합니다.


&lt;인증&gt; 요소 포함 되기도 &lt;forms&gt; 폼 인증 관련 설정을 포함 하는 자식 요소입니다. 지금은 보겠습니다 사용 기본 폼 인증 설정 합니다. 살펴볼 것입니다는 &lt;forms&gt; 다음 자습서에서 더 자세하게에서 자식 요소입니다.

## <a name="step-3-building-the-login-page"></a>로그인 페이지를 구성 하는 3 단계:

폼 인증을 지원 하기 위해 웹 사이트에 로그인 페이지가 필요 합니다. 폼 인증 워크플로 섹션의 FormsAuthenticationModule 자동 리디렉션됩니다 이해에 설명 된 대로 로그인 페이지에 사용자에 맞지 않음을 페이지에 액세스 하려고 하면 볼 수 있는 권한이 있습니다. ASP.NET 웹 컨트롤 익명 사용자에 게 로그인 페이지에 대 한 링크를 표시할 수 있습니다. 이 로그인 페이지의 url 질문 일상적인?

기본적으로 폼 인증 시스템 Login.aspx 이름을 지정 하는 로그인 페이지를 요구 하 고 웹 응용 프로그램의 루트 디렉터리에 저장. 다른 로그인 페이지 URL을 사용 하려는 경우 Web.config를 사용 하 여 그렇게 할 수 있습니다. 이후 자습서에서이 작업을 수행 하는 방법을 살펴봅니다.

로그인 페이지에 세 개의 책임이 있습니다.

1. 자격 증명을 입력 방문자를 허용 하는 인터페이스를 제공 합니다.
2. 전송 된 자격 증명이 유효 하는 경우를 결정 합니다.
3. 폼 인증 티켓을 만들어 사용자를 로그인 합니다.

### <a name="creating-the-login-pages-user-interface"></a>로그인 페이지의 사용자 인터페이스 만들기

시작 하겠습니다 첫 번째 작업입니다. Login.aspx 이라는 사이트의 루트 디렉터리에 새 ASP.NET 페이지를 추가 하 고 Site.master 마스터 페이지와 연결 합니다.


[![새 ASP.NET 페이지 추가 Login.aspx 라는](an-overview-of-forms-authentication-vb/_static/image23.png)](an-overview-of-forms-authentication-vb/_static/image22.png)

**그림 08**: 새 ASP.NET 페이지 라는 Login.aspx 추가 ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image24.png))


두 텍스트 상자-사용자의 이름에 대 한 하나이 고, 자신의 암호-및에서는 양식을 제출 하는 단추에 대 한 일반 로그인 페이지 인터페이스 구성 됩니다. 웹 사이트에는 종종 암호 저장 하는 확인란을 선택 하는 경우 결과 인증 티켓을 계속 되 면 브라우저를 다시 시작할 포함 됩니다.

Login.aspx로 두 개의 텍스트 상자를 추가 하 고 해당 ID 속성 이름 및 암호를 각각 설정 합니다. 또한 암호로 암호의 텍스트 모드 속성을 설정 합니다. 다음으로 해당 ID 속성 RememberMe me. 사용자 이름 및 암호를 해당 텍스트 속성을로 설정 하는 CheckBox 컨트롤 추가 그런 다음, 로그인에 텍스트 속성을 설정할 LoginButton 라는 단추를 추가 합니다. 마지막으로 추가 Label 웹 컨트롤을 하 고 해당 ID 속성을 설정 하지 InvalidCredentialsMessage, Text 속성을 사용자 이름 또는 암호가 잘못 되었습니다. 다시 시도 하세요., 빨간색으로 해당 ForeColor 속성 및 해당 Visible 속성을 False로 합니다.

이 시점에서 화면이 그림 9에 스크린샷과 유사 표시 하 고 페이지의 선언적 구문 다음과 같이 해야 합니다.

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample4.aspx)]


[![로그인 페이지에서는 두 개의 텍스트 상자, CheckBox, 단추, 레이블](an-overview-of-forms-authentication-vb/_static/image26.png)](an-overview-of-forms-authentication-vb/_static/image25.png)

**그림 09**: The 로그인 페이지 포함 된 두 개의 텍스트 상자, CheckBox, 단추 및 레이블 ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image27.png))


마지막으로, LoginButton의 클릭에 대 한 이벤트 처리기를 만들고 이벤트입니다. 디자이너에서 단순히 Button 컨트롤을이 이벤트 처리기를 만들고 두 번 클릭 합니다.

### <a name="determining-if-the-supplied-credentials-are-valid"></a>설정 하면 제공 된 자격 증명이 유효 기간 확인

이제 작업 2 단추의 Click에서 구현 해야 이벤트 처리기-제공 된 자격 증명이 유효한 지 여부를 결정 합니다. 그러려면 제공 된 자격 증명이 알려진된 자격 증명과 일치 하는 경우 확인할 수 있습니다 수 있도록 사용자의 자격 증명을 모두 보유 하 고 있는 사용자 저장소에 있어야 합니다.

ASP.NET 2.0 이전 개발자가 자신의 사용자 저장소를 모두 구현 하 고 저장소에 대해 제공된 된 자격 증명의 유효성을 검사 하는 코드를 작성 하는 일을 담당 했습니다. 대부분의 개발자 명명 된 사용자 사용자 이름, 암호, 전자 메일, LastLoginDate, 등과 같은 열이 있는 테이블을 만드는 사용자 저장소에서 데이터베이스를 구현 합니다. 그런 다음이 테이블에서 사용자 계정 마다 하나의 레코드를 것입니다. 사용자의 제공 된 자격 증명을 확인 하는 일치 하는 사용자 이름에 대 한 데이터베이스를 쿼리 한 다음 데이터베이스에 암호가 제공 된 암호에 상응 하는 확인 포함 됩니다.

ASP.NET 2.0에서는 개발자가 하나를 사용 해야 멤버 자격 공급자의 사용자 저장소를 관리 하 합니다. 이 자습서 시리즈의 사용자 저장소에 대 한 SQL Server 데이터베이스를 사용 하 여 SqlMembershipProvider를 사용 합니다. SqlMembershipProvider를 사용 하는 경우 테이블, 뷰 및 공급자가 예상 하는 저장된 프로시저를 포함 하는 특정 데이터베이스 스키마를 구현 해야 합니다. 이 스키마를 구현 하는 방법을 검토 합니다는 *[SQL Server에서 멤버 자격 스키마 만들기](../membership/creating-the-membership-schema-in-sql-server-vb.md)* 자습서입니다. 위치에 멤버 자격 공급자를 사용자의 자격 증명 유효성을 검사 하는 작업은 호출으로는 [멤버 자격 클래스](https://msdn.microsoft.com/library/system.web.security.membership.aspx)의 [ValidateUser (*username*, *암호*) 메서드](https://msdn.microsoft.com/library/system.web.security.membership.validateuser.aspx)를 나타내는 부울 값을 반환 하는 여부의 유효성을 검사는 *사용자 이름* 및 *암호* 조합 합니다. 것을 확인으로 SqlMembershipProvider 사용자 저장소를 아직 구현 하지 않았습니다 멤버 자격 클래스 ValidateUser 메서드이 이번에 사용할 수 없습니다.

만드는 대신 많은 시간을 고유한 사용자 지정 사용자가 데이터베이스 테이블 (만드는 것이 사용 되지 않는 SqlMembershipProvider를 구현한 후) 보겠습니다 대신 하드 코딩 유효한 자격 증명을 로그인에 자체 페이지입니다. LoginButton의 클릭 이벤트 처리기를 다음 코드를 추가 합니다.

[!code-vb[Main](an-overview-of-forms-authentication-vb/samples/sample5.vb)]

볼 수 있듯이-Scott, Jisun, 및 Sam-세 유효한 사용자 계정이 있고 세 모두 동일한 암호 (password). 코드는 올바른 사용자 이름 및 암호 일치 찾고 사용자 이름 및 암호 배열을 반복 합니다. 사용자 이름 및 암호를 모두 유효한 경우 해야 사용자를 로그인 하 고 적절 한 페이지로 리디렉션됩니다. 자격 증명이 유효, InvalidCredentialsMessage 레이블 표시 했습니다.

유효한 자격 증명을 입력 하는 경우 적절 한 페이지로 리디렉션됩니다 다음 언급 했습니다. 그러나 적절 한 페이지 이란? 사용자를 보려면 허가 되지 않은 페이지를 방문는 FormsAuthenticationModule 자동으로 리디렉션되는 또 로그인 페이지에는 점에 유의 하세요. 이 과정에서 요청된 된 URL ReturnUrl 매개 변수를 통해 쿼리 문자열에 포함 됩니다. 즉, ProtectedPage.aspx를 방문 하 여 사용자가 고 그러려면 권한이 부여 되지 않은 경우는 FormsAuthenticationModule 리디렉션합니다 수 있습니다:

Login.aspx?ReturnUrl=ProtectedPage.aspx

성공적으로 로그인 시 사용자 ProtectedPage.aspx 돌아가기 리디렉션되어야 합니다. 또는 사용자가 자신의 volition 로그인 페이지를 방문 수 있습니다. 이 경우 사용자 로그인은 전송 되어야 합니다는 루트 폴더의 Default.aspx 페이지에.

### <a name="logging-in-the-user"></a>사용자 로그인

가정 하면 제공 된 자격 증명이 유효 하면 필요한 폼 인증 티켓을 만들 수 있으므로 사이트에 사용자를 로그인 합니다. [FormsAuthentication 클래스](https://msdn.microsoft.com/library/system.web.security.formsauthentication.aspx) 에 [System.Web.Security 네임 스페이스](https://msdn.microsoft.com/library/system.web.security.aspx) 인증 시스템 로깅 및 폼을 통해 사용자 로깅에 대 한 다양 한 메서드를 제공 합니다. FormsAuthentication 클래스에서 여러 가지가 있습니다 하지만 시점에 관심이 세 가지 합니다.

- [GetAuthCookie (*username*, *persistCookie*)](https://msdn.microsoft.com/library/system.web.security.formsauthentication.getauthcookie.aspx) -제공 된 이름에 대 한 폼 인증 티켓을 만들어 *username*합니다. 다음으로,이 메서드가 만들고 인증 티켓의 콘텐츠를 보유 하는 HttpCookie 개체를 반환 합니다. 경우 *persistCookie* 은 True, 영구 쿠키 생성 됩니다.
- [SetAuthCookie (*username*, *persistCookie*)](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx) -는 GetAuthCookie 호출 (*username*, *persistCookie*) 폼 인증 쿠키를 생성 하는 방법입니다. 이 메서드는 다음 (사용 되는, 그렇지 않으면 쿠키 기반 폼 인증 되 고,이 메서드는 쿠키 티켓 논리를 처리 하는 내부 클래스를 호출 한다고 가정) 쿠키 컬렉션에 GetAuthCookie에서 반환 된 쿠키를 추가 합니다.
- [RedirectFromLoginPage (*username*, *persistCookie*)](https://msdn.microsoft.com/library/system.web.security.formsauthentication.redirectfromloginpage.aspx) -이 메서드를 호출 SetAuthCookie (*username*, *persistCookie*), 한 다음 적절 한 페이지로 사용자를 리디렉션합니다.

GetAuthCookie 인증 티켓 쿠키 컬렉션에 쿠키를 쓰기 전에 수정 해야 할 때 유용 합니다. SetAuthCookie 쿠키 컬렉션에 추가 하 고 폼 인증 티켓 만들기를 이지만 적절 한 페이지로 사용자를 리디렉션할 하지 않으려는 경우에 유용 합니다. 로그인 페이지에 보관 하거나 일부 다른 페이지에 게 보낼 하려는 경우가 있을 것입니다.

사용자 로그인과 해당 페이지로 리디렉션됩니다 할 것 이므로 RedirectFromLoginPage 사용 합니다. 업데이트 LoginButton의 클릭 이벤트 처리기를 코드의 다음 행으로 두 주석 처리 된 TODO 줄을 바꿉니다.

FormsAuthentication.RedirectFromLoginPage(UserName.Text, RememberMe.Checked)

폼 인증 티켓에 대 한 사용자 이름 텍스트 상자의 텍스트 속성이 사용 폼 인증 티켓을 만들 때 *username* 매개 변수 및에 대 한 RememberMe 확인란의 선택된 상태는  *persistCookie* 매개 변수입니다.

로그인 페이지를 테스트 하려면 브라우저를 확인 하십시오. Nope의 사용자 이름 및 잘못 된 암호와 같은 잘못 된 자격 증명을 입력 하 여 시작 합니다. [로그인] 단추를 클릭 하면 포스트백이 발생 하 고 InvalidCredentialsMessage 레이블이 표시 됩니다.


[![InvalidCredentialsMessage 레이블이 표시 되는 경우 입력 잘못 된 자격 증명 됩니다.](an-overview-of-forms-authentication-vb/_static/image29.png)](an-overview-of-forms-authentication-vb/_static/image28.png)

**그림 10**: The InvalidCredentialsMessage 레이블이 표시 되는 경우 입력 자격 증명이 잘못 되었습니다 ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image30.png))


다음으로 유효한 자격 증명을 입력 하 고 [로그인] 단추를 클릭 합니다. 포스트백 폼 인증 티켓을 발생 하는 경우이 이번 만들어지고 Default.aspx로 다시 자동으로 리디렉션됩니다. 이 시점에서 로그인 웹 사이트는 현재 로그인을 나타내는 시각 신호 없습니다 있더라도 합니다. 또는 페이지를 방문 하는 사용자를 식별 하는 방법 뿐만 아니라 하지 프로그래밍 방식으로 사용자 있는지 여부를 결정 하는 방법과 4 단계에서에서 기록 됩니다.

5 단계에는 로깅을 웹 사이트에서 사용자를 제거 하는 기술을 있는지 검사 합니다.

### <a name="securing-the-login-page"></a>로그인 페이지에 보안 설정

사용자는 자신의 자격 증명을 입력 하 고 로그인 페이지 양식 제출, 자격 증명-암호를 포함 하 여-웹 서버에 인터넷을 통해 전송 됩니다 *일반 텍스트*합니다. 즉, 네트워크 트래픽을 검사 하는 모든 해커가 사용자 이름 및 암호를 볼 수 있습니다. 이 방지 하려면 사용 하 여 네트워크 트래픽을 암호화 하는 데 필수적인은 [레이어 SSL (Secure Socket)](http://en.wikipedia.org/wiki/Secure_Sockets_Layer)합니다. 이렇게 하면 자격 증명 (뿐만 아니라 전체 페이지의 HTML 태그) 웹 서버에서 수신 될 때까지 브라우저를 남깁니다 순간부터 암호화 됩니다.

중요 한 정보를 포함 하는 웹 사이트, 하지 않는 한 하기만 하면 됩니다 SSL을 사용 하도록 로그인 페이지에서와 다른 페이지에 일반 텍스트로 네트워크를 통해 그렇지 않은 경우 사용자의 암호가 전송 수입니다. 폼 인증 티켓 있으므로 기본적으로 모두 암호화 되어 디지털 서명 (변조를 방지) 보안에 대 한 걱정할 필요가 없습니다. 폼 인증 티켓 보안에 대 한 보다 철저 한 설명은 다음 자습서에 표시 됩니다.

> [!NOTE]
> 금융 및 의료 보험 많은 웹 사이트에서 SSL을 사용 하도록 구성 된 *모든* 인증 된 사용자 페이지에 액세스할 수 있습니다. 이러한 웹 사이트를 빌드하는 경우 폼 인증 티켓 보안 연결을 통해 전송할만 폼 인증 시스템을 구성할 수 있습니다. 다음 자습서에서는 다양 한 폼 인증 구성 옵션 살펴보도록 하겠습니다  *[폼 인증 구성 및 고급 항목](../membership/creating-the-membership-schema-in-sql-server-vb.md)*합니다.


## <a name="step-4-detecting-authenticated-visitors-and-determining-their-identity"></a>4 단계: 인증 된 방문자를 검색 하 고 해당 Id를 확인 합니다.

이 시점에서 폼 인증을 사용 하도록 설정 했으며 기본 로그인 페이지를 만든 하지만 아직 인증 또는 익명 사용자가 있는지 여부를 확인할 수 있습니다 어떻게 검사. 특정 시나리오에서는 서로 다른 데이터 또는 인증 또는 익명 사용자가 페이지를 방문 하는 여부에 따라 정보를 표시할 할 수 있습니다. 또한 종종 알아야 인증 된 사용자의 id입니다.

이러한 기법을 설명 하기 위해 기존 Default.aspx 페이지를 확장 해 보겠습니다. Default.aspx에서 하나의 명명 된 AuthenticatedMessagePanel 및 다른 명명 된 AnonymousMessagePanel 두 패널 컨트롤을 추가 합니다. 첫 번째 패널에서 WelcomeBackMessage 이라는 레이블 컨트롤을 추가 합니다. 두 번째 하이퍼링크 컨트롤을 추가, 로그인 및 해당 NavigateUrl 속성을 Text 속성을 설정 ~ / Login.aspx입니다. 이 시점에서 Default.aspx에 대 한 선언적 태그는 다음과 비슷하게 표시 됩니다.

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample6.aspx)]

짐작할 아마도 지금까지, 여기서 인증 된 방문자 및 익명 방문자에 게 AnonymousMessagePanel 방금 AuthenticatedMessagePanel만 표시 되려고 합니다. 이를 위해 사용자의 로그인은 여부에 따라 이러한 패널의 표시 되는 속성을 설정 해야 합니다.

[Request.IsAuthenticated 속성](https://msdn.microsoft.com/library/system.web.httprequest.isauthenticated.aspx) 요청이 인증 되었는지 여부를 나타내는 부울 값을 반환 합니다. 다음 코드 페이지에 입력\_이벤트 처리기 코드를 로드 합니다.

[!code-vb[Main](an-overview-of-forms-authentication-vb/samples/sample7.vb)]

이 코드가 브라우저를 통해 Default.aspx를 방문 합니다. 로그인 페이지에 대 한 링크 표시는 있다고 간주 되며 아직에 로그인 합니다 (그림 11 참조). 이 링크를 클릭 하 고 사이트에 로그인 합니다. 3 단계에서에서 설명한 것 처럼 자격 증명을 입력 한 후 돌아갑니다 Default.aspx에 있지만이 현재가 페이지에 표시는 진화! 메시지 (그림 12 참조).


[![방문 익명으로 링크 로그에 표시 되 면](an-overview-of-forms-authentication-vb/_static/image32.png)](an-overview-of-forms-authentication-vb/_static/image31.png)

**그림 11**: 때 방문 익명으로, 로그의 링크 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image33.png))


[![인증 된 사용자는 진화를 표시 됩니다! 메시지](an-overview-of-forms-authentication-vb/_static/image35.png)](an-overview-of-forms-authentication-vb/_static/image34.png)

**그림 12**: 인증 된 사용자는 진화 표시 됩니다. 메시지 ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image36.png))


통해 현재 로그온된 한 사용자의 id를 확인할 수 있습니다는 [HttpContext 개체](https://msdn.microsoft.com/library/system.web.httpcontext.aspx)의 [사용자 속성](https://msdn.microsoft.com/library/system.web.httpcontext.user.aspx)합니다. HttpContext 개체 현재 요청에 대 한 정보를 나타내며는 다른 규칙 으로부터 응답, 요청 및 세션 등과 같은 일반적인 ASP.NET 개체에 대 한 홈입니다. 사용자 속성의 현재 HTTP 요청 및 구현 보안 컨텍스트를 나타내는 [IPrincipal 인터페이스](https://msdn.microsoft.com/library/system.security.principal.iprincipal.aspx)합니다.

사용자 속성의 FormsAuthenticationModule로 설정 됩니다. 특히 면는 FormsAuthenticationModule가 들어오는 요청에서 폼 인증 티켓을 찾으면 새 GenericPrincipal 개체 만들어지고 사용자 속성에 할당 합니다.

(예: GenericPrincipal) 주 개체는 사용자의 id와 이들이 속하는 역할에 정보를 제공 합니다. IPrincipal 인터페이스는 두 명의 멤버를 정의합니다.

- [IsInRole (*roleName*)](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole.aspx) -보안 주체가 지정된 된 역할에 속하는지를 나타내는 부울 값을 반환 하는 메서드입니다.
- [Identity](https://msdn.microsoft.com/library/system.security.principal.iprincipal.identity.aspx) -구현 하는 개체를 반환 하는 속성은 [IIdentity 인터페이스](https://msdn.microsoft.com/library/system.security.principal.iidentity.aspx)합니다. IIdentity 인터페이스는 세 가지 속성을 정의: [AuthenticationType](https://msdn.microsoft.com/library/system.security.principal.iidentity.authenticationtype.aspx), [IsAuthenticated](https://msdn.microsoft.com/library/system.security.principal.iidentity.isauthenticated.aspx), 및 [이름](https://msdn.microsoft.com/library/system.security.principal.iidentity.name.aspx)합니다.

다음 코드를 사용 하 여 현재 방문자의 이름을 확인할 수 있습니다.

Dim currentUsersName As String = User.Identity.Name

사용 하 여 폼 인증을, 하는 경우는 [FormsIdentity 개체](https://msdn.microsoft.com/library/system.web.security.formsidentity.aspx) GenericPrincipal의 Identity 속성에 대해 생성 됩니다. 항상 FormsIdentity 클래스 IsAuthenticated 속성에 대해 문자열 폼의 AuthenticationType 속성 및 True를 반환합니다. Name 속성 폼 인증 티켓을 만들 때 지정한 사용자 이름을 반환 합니다. 이 세 가지 속성 외에도 FormsIdentity 포함을 통해 기본 인증 티켓에 대 한 액세스는 [속성 티켓](https://msdn.microsoft.com/library/system.web.security.formsidentity.ticket.aspx)합니다. 형식의 개체를 반환 하는 티켓 속성 [FormsAuthenticationTicket](https://msdn.microsoft.com/library/system.web.security.formsauthenticationticket.aspx), 만료, IsPersistent, IssueDate, 이름, 등 속성이 있는 합니다.

중요 한 부분은 여기는 *username* 는 FormsAuthentication.GetAuthCookie에 지정 된 매개 변수 (*사용자 이름*, *persistCookie*), FormsAuthentication.SetAuthCookie (*username*, *persistCookie*), 및 FormsAuthentication.RedirectFromLoginPage (*username*, *persistCookie*) 메서드는 동일한 값을 User.Identity.Name 반환 합니다. 또한 이러한 메서드에서 생성 인증 티켓을 User.Identity FormsIdentity 개체를 캐스팅 하 고 다음 Ticket 속성에 액세스 하 여 사용할 수 있습니다.

Dim ident As FormsIdentity = CType(User.Identity, FormsIdentity)

Dim authTicket As FormsAuthenticationTicket = ident.Ticket

Default.aspx에서 더 개인 설정 된 메시지를 제공 해 보겠습니다. 페이지가 업데이트\_WelcomeBackMessage 레이블의 Text 속성 문자열 시작 다시 할당 되도록 이벤트 처리기를 로드할 *username*!

WelcomeBackMessage.Text = "Welcome back, " &amp; User.Identity.Name &amp; "!"

그림 13 (Scott 사용자로 로그인) 하는 경우이 수정 작업의 결과 보여 줍니다.


[![환영 메시지는 사용자의 이름에 현재 로그온 한 포함 됩니다.](an-overview-of-forms-authentication-vb/_static/image38.png)](an-overview-of-forms-authentication-vb/_static/image37.png)

**그림 13**: 환영 메시지는 현재 로그온 한 사용자의 이름을 포함 ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image39.png))


### <a name="using-the-loginview-and-loginname-controls"></a>LoginView 및 LoginName 컨트롤을 사용 하 여

인증 및 익명 사용자에 게 다른 콘텐츠를 표시 하는 것은 일반적인 요구 사항은; 현재 로그온된 한 사용자의 이름을 표시 합니다. 따라서 ASP.NET를 한 줄의 코드를 작성할 필요 하지 않고 그림 13에 표시 되는 동일한 기능을 제공 하는 두 개의 웹 컨트롤에 포함 됩니다.

[LoginView 컨트롤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginview.aspx) 손쉽게 인증 및 익명 사용자에 게 다른 데이터를 표시할 수 있는 템플릿 기반 웹 컨트롤입니다. LoginView는 두 개의 미리 정의 된 템플릿이 포함 되어 있습니다.

- 이 서식 파일에 추가 된 모든 태그 AnonymousTemplate-은 익명 방문자에 게 표시 됩니다.
- LoggedInTemplate-이 서식 파일의이 태그는 인증 된 사용자 에게만 표시 됩니다.

이 사이트의 마스터 페이지, Site.master LoginView 컨트롤을 추가 해 보겠습니다. 방금 LoginView 컨트롤을 추가 하는 대신 하지만 새 ContentPlaceHolder 컨트롤과 추가해보겠습니다. 한 다음 새 해당 ContentPlaceHolder 내에서 LoginView 컨트롤. 이 결정에 대 한 설명 곧 표시 됩니다.

> [!NOTE]
> LoginView 컨트롤은 AnonymousTemplate 및 LoggedInTemplate 뿐만 아니라 역할 관련 서식 파일을 포함할 수 있습니다. 역할 관련 템플릿은 지정된 된 역할에 속하는 사용자에만 변경 내용을 표시 합니다. 이후 자습서에서 LoginView 컨트롤의 역할 기반 기능을 살펴보겠습니다.


마스터 페이지 탐색 내에 LoginContent 라는 ContentPlaceHolder를 추가 하 여 시작 &lt;div&gt; 요소입니다. 도구 상자에서 소스 뷰 결과 태그는 TODO 오른쪽 위에 배치 ContentPlaceHolder 컨트롤을 끌어 놓기만: 메뉴 여기 텍스트 이동 됩니다.

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample8.aspx)]

LoginView 컨트롤 LoginContent ContentPlaceHolder 내에서 다음을 추가 합니다. 마스터 페이지의 ContentPlaceHolder 컨트롤에 배치 하는 콘텐츠 것으로 간주 됩니다 *기본 페이지* ContentPlaceHolder는에 대 한 합니다. 즉,이 마스터 페이지를 사용 하는 ASP.NET 페이지에 대 한 각 ContentPlaceHolder 자신의 콘텐츠를 지정 하거나 마스터 페이지의 기본 콘텐츠를 사용할 수 있습니다.

로그인 탭의 도구 상자에는 LoginView 및 기타 로그인 관련 컨트롤이 있습니다.


[![도구 상자에서 LoginView 컨트롤](an-overview-of-forms-authentication-vb/_static/image41.png)](an-overview-of-forms-authentication-vb/_static/image40.png)

**그림 14**: 도구 상자에는 LoginView 컨트롤 ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image42.png))


다음으로, 두 개의 추가 &lt;br /&gt; 자 바로 뒤, LoginView 컨트롤 내에서 ContentPlaceHolder 요소입니다. 이 시점에서 탐색 &lt;div&gt; 요소의 태그는 다음과 같습니다.

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample9.aspx)]

LoginView의 템플릿 디자이너 또는 선언적 태그에서 정의할 수 있습니다. Visual Studio의 디자이너에서 구성 된 템플릿 드롭다운 목록에 나열 된 LoginView의 스마트 태그를 확장 합니다. Hello, 텍스트 모르는 AnonymousTemplate;에 입력 그런 다음, 하이퍼링크 컨트롤을 추가 하 고 로그에서 해당 텍스트와 NavigateUrl 속성을 설정 하 고 ~ / Login.aspx, 각각.

AnonymousTemplate를 구성한 후의 LoggedInTemplate로 전환 하 고 텍스트, "진화,"를 입력 합니다. 그런 다음 "시작 다시" 텍스트 직후 배치 하는 것은 LoggedInTemplate로 도구 상자에서 LoginName 컨트롤을 끕니다. [LoginName 컨트롤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginname.aspx), 의미 이름으로, 현재 로그인된 한 사용자의 이름을 표시 합니다. 내부적으로 LoginName 컨트롤 User.Identity.Name 속성을 단순히 출력

LoginView의 서식 파일에 추가 하는이 코드를 변경한 후 태그는 다음과 비슷하게 표시 됩니다.

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample10.aspx)]

Site.master 마스터 페이지에이 추가 된 웹 사이트의 각 페이지에는 사용자가 인증 되는지 여부에 따라 서로 다른 메시지를 표시 됩니다. 그림 15 Jisun 사용자가 브라우저를 통해 방문 Default.aspx 페이지를 보여줍니다. 진화 Jisun 메시지가 두 번 반복 됩니다: 콘텐츠 영역 (패널 컨트롤 및 프로그래밍 논리)를 통해 (방금 추가한 LoginView 컨트롤)를 통해 왼쪽의 마스터 페이지의 탐색 섹션에 두 번 및 Default.aspx의에서 한 번입니다.


[![LoginView 컨트롤 표시 시작 백 Jisun 합니다.](an-overview-of-forms-authentication-vb/_static/image44.png)](an-overview-of-forms-authentication-vb/_static/image43.png)

**그림 15**: LoginView 컨트롤 표시 시작 역방향으로 Jisun 합니다. ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image45.png))


마스터 페이지에는 LoginView 추가 함으로써 사이트에서 모든 페이지에 나타날 수 있습니다. 그러나 있을 수 있습니다 웹 페이지에이 메시지를 표시 하려고 하지 않습니다. 이러한 한 페이지 로그인 페이지 없으므로 없는 위치에서 로그인 페이지에 대 한 링크 같습니다. 마스터 페이지에서 ContentPlaceHolder의 LoginView 컨트롤을 배치 했습니다 이후 가격 콘텐츠 페이지에서이 기본 태그를 재정의할 수 있습니다. Login.aspx 열고 디자이너로 이동 합니다. 콘텐츠 컨트롤을 명시적으로 정의 하지 않은 우리 이후 LoginContent ContentPlaceHolder 마스터 페이지에 대 한 Login.aspx에 로그인 페이지에는 표시 마스터 페이지의 기본 태그이 ContentPlaceHolder이에 대 한 합니다. 볼 수 있습니다이 디자이너-를 통해 LoginContent ContentPlaceHolder 기본 태그 (LoginView 컨트롤)를 보여 줍니다.


[![로그인 페이지에 표시 된 기본 콘텐츠 LoginContent ContentPlaceHolder 마스터 페이지에 대 한](an-overview-of-forms-authentication-vb/_static/image47.png)](an-overview-of-forms-authentication-vb/_static/image46.png)

**그림 16**: 마스터 페이지의 LoginContent ContentPlaceHolder에 대 한 로그인 페이지는 기본 콘텐츠 ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image48.png))


LoginContent ContentPlaceHolder에 대 한 기본 태그를 무시 하려면 디자이너의 영역을 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 사용자 지정 콘텐츠 만들기 옵션을 선택 합니다. (Visual Studio 2008에서 ContentPlaceHolder를 사용 하 여 포함 된 경우 스마트 태그는 옵션을 선택 하면 동일한 옵션을 제공 합니다.) 이렇게 하면 새 페이지의 태그에 있고, 따라서 콘텐츠 컨트롤 추가를이 페이지에 대 한 사용자 지정 콘텐츠를 정의할 수 있습니다. 로그인 하십시오, 예: 여기에서 사용자 지정 메시지를 추가 하지만 보겠습니다 방금 비워 둘 수 있습니다.

> [!NOTE]
> 사용자 지정 콘텐츠를 만들면 Visual Studio 2005에서 빈 생성 콘텐츠 컨트롤은 ASP.NET 페이지에 있습니다. 그러나 Visual Studio 2008에서 사용자 지정 콘텐츠 만들기 마스터 페이지의 기본 콘텐츠를 복사 새로 만든된 콘텐츠 컨트롤에 합니다. Visual Studio 2008을 사용 하는 경우 다음, 새 콘텐츠 컨트롤 만들기 확인 한 후 마스터 페이지에서 복사한 내용을 취소 합니다.


그림 17이 같이 변경한 후 브라우저에서 열어 볼 때 Login.aspx 페이지를 보여줍니다. 모르는 또는 진화, Hello는 *username* 왼쪽된 탐색 창에서 메시지 &lt;div&gt; Default.aspx를 방문할 때 없기 때문입니다.


[![로그인 페이지 기본 LoginContent ContentPlaceHolder 태그를 숨깁니다.](an-overview-of-forms-authentication-vb/_static/image50.png)](an-overview-of-forms-authentication-vb/_static/image49.png)

**그림 17**: 로그인 페이지 기본 LoginContent ContentPlaceHolder의 태그를 숨깁니다 ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image51.png))


## <a name="step-5-logging-out"></a>5 단계: 로그 아웃

3 단계에서에서 보이는 것 처럼 로그인 페이지의 사용자는 사이트에 로그인 할 구성 하지만 아직 사용자를 로그 아웃 하는 방법을 참조 하십시오. 사용자를 기록 하기 위한 방법, 이외에 FormsAuthentication 클래스 제공는 [SignOut 메서드에](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx)합니다. SignOut 메서드는 단순히 함으로써 사이트에서 사용자로 로그온 폼 인증 티켓을 삭제 합니다.

로그 아웃 링크는 이러한 일반적인 기능을 제공 하는 ASP.NET 사용자를 로그 아웃 하도록 특별히 설계 된 컨트롤을 포함 합니다. [LoginStatus 제어](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginstatus.aspx) 로그인 LinkButton 또는 사용자의 인증 상태에 따라 로그 아웃 LinkButton을 표시 합니다. 로그 아웃 LinkButton 인증 된 사용자에 게 표시 되는 반면 익명 사용자에 대 한 로그인 LinkButton 렌더링 됩니다. 로그인 및 로그 아웃 링크 단추가 대 한 텍스트는 LoginStatus 통해 구성할 수 있습니다 LoginText 및 LogoutText 속성입니다.

로그인 LinkButton을 클릭 하면 로그인 페이지에 리디렉션이 실행 되어, 다시 게시 합니다. 로그 아웃 LinkButton를 클릭 하면 LoginStatus 컨트롤이 FormsAuthentication.SignOff 메서드를 호출 하 고 페이지에는 사용자를 리디렉션합니다. 로그인된 페이지 사용자 리디렉션됩니다 다음 세 값 중 하나를 지정할 수 있는 LogoutAction 속성에 따라 달라 집니다.

- 새로 고침-기본; 방금 방문 페이지에는 사용자를 리디렉션합니다. 방금 방문 페이지는 FormsAuthenticationModule가 자동으로 다음 익명 사용자가 허용 하지 않는 경우 사용자를 로그인 페이지로 리디렉션하십시오.

리디렉션 여기 수행 이유에 대 한 자세한 내용을 보려면 수 있습니다. 사용자가 동일한 페이지에 남아 야 할 이유 명시적 리디렉션에 대 한 필요성? 이유는 로그 오프 LinkButton을 클릭할 때 사용자 아직 되어 폼 인증 티켓은 쿠키 컬렉션에 있습니다. 따라서 포스트백 요청은 인증 된 요청. LoginStatus 컨트롤 SignOut 메서드를 호출 하지만 FormsAuthenticationModule 사용자를 인증 한 후 이러한 합니다. 따라서 명시적 리디렉션 하면는 브라우저에서 페이지를 다시 요청 합니다. 브라우저에서 페이지를 다시 요청 시점에서는 폼 인증 티켓을 제거한와 들어오는 요청 익명 이므로 합니다.

- 리디렉션-사용자가 LoginStatus의 LogoutPageUrl 속성으로 지정 된 URL로 리디렉션됩니다.
- RedirectToLoginPage-사용자가 로그인 페이지로 리디렉션됩니다.

마스터 페이지에 LoginStatus 컨트롤을 추가 하 고 서명 된 확인 하는 메시지가 표시 되는 페이지에 연결 하려면 리디렉션 옵션을 사용 하도록 구성 살펴보겠습니다. Logout.aspx 라는 루트 디렉터리의 페이지를 만들어 시작 합니다. 이 페이지 Site.master 마스터 페이지와 연결할 두는 것을 잊지 마십시오. 다음으로 아웃 기록 된 사용자에 게 설명 하는 페이지의 태그에는 메시지를 입력 합니다.

다음으로, Site.master 마스터 페이지에 반환 하 고 LoginContent ContentPlaceHolder의는 LoginView 아래 LoginStatus 컨트롤을 추가. ~/Logout.aspx로 리디렉션 LoginStatus 컨트롤의 LogoutAction 속성 및 해당 LogoutPageUrl 속성을 설정 합니다.

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample11.aspx)]

LoginView 컨트롤 외부에서 LoginStatus 이므로 익명 및 인증 된 사용자에 게 표시 됩니다 표시 되지만 확인 하기 때문는 LoginStatus 로그인 또는 로그 아웃 LinkButton을 올바르게 표시 됩니다. LoginStatus 컨트롤을 추가 하 여는 AnonymousTemplate의 하이퍼링크 로그에는 불필요 되므로 제거 합니다.

그림 18 Jisun 방문 Default.aspx를 보여 줍니다. 왼쪽된 열에 메시지가 표시 됩니다, 그리고 환영를 로그 아웃 링크와 Jisun 합니다. 로그 아웃 LinkButton 클릭 하면 포스트백, Jisun 시스템에서 서명 하 고 Logout.aspx 그녀는 리디렉션합니다. 그림 19에서 볼 수 있듯이 Jisun Logout.aspx에 도달할 때까지 그녀가 이미 로그 아웃 되었습니다 고 익명입니다. 따라서 왼쪽된 열에는 텍스트, 환영 이상 해지고 및 로그인 페이지 링크를 보여 줍니다.


[![Default.aspx의 진화를 로그 아웃 LinkButton 함께 Jisun를 보여 줍니다.](an-overview-of-forms-authentication-vb/_static/image53.png)](an-overview-of-forms-authentication-vb/_static/image52.png)

**그림 18**: Default.aspx 표시의 진화, 로그 아웃 LinkButton와 Jisun 함께 ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image54.png))


[![Logout.aspx 표시, 설정이 로그인 LinkButton 함께 모르는](an-overview-of-forms-authentication-vb/_static/image56.png)](an-overview-of-forms-authentication-vb/_static/image55.png)

**그림 19**: Logout.aspx 표시, 설정이 로그인 LinkButton 함께 모르는 ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image57.png))


> [!NOTE]
> 확인해 (예: 4 단계에서에서 Login.aspx에 대해 했던) 마스터 페이지의 LoginContent ContentPlaceHolder 숨기려면 Logout.aspx 페이지를 사용자 지정할 수 있습니다. LoginStatus 컨트롤에서 로그인 LinkButton 렌더링 때문에 (한 Hello, 아래에 모르는) 현재 URL ReturnUrl querystring 매개 변수를 전달 하는 로그인 페이지에 사용자를 보냅니다. 즉, 사용자가 로그 아웃 하는이 LoginStatus 로그인 LinkButton을 클릭 한 다음 로그인을 쉽게 사용자 혼동을 줄 수 있는 Logout.aspx로 다시 리디렉션할 수 됩니다.


## <a name="summary"></a>요약

이 자습서에서는 양식 인증 워크플로에 대 한 검사부터 시작 하 고 ASP.NET 응용 프로그램에서 폼 인증을 구현 하기 위해 다음 설정 합니다. 폼 인증 연결 된 값은 두 가지가 있는 FormsAuthenticationModule: 해당 폼 인증 티켓을 기반으로 사용자를 식별 하 고 권한이 없는 사용자가 로그인 페이지로 리디렉션합니다.

.NET Framework의 FormsAuthentication 클래스 만들기, 검사 및 폼 인증 티켓을 제거 하기 위한 메서드를 포함 합니다. Request.IsAuthenticated 속성 및 사용자 개체 요청이 인증 되는지 여부 및 사용자의 id에 대 한 정보를 확인 하기 위한 추가 프로그래밍 방식 지원을 제공 합니다. 여러 가지 일반적인 로그인 관련 작업을 수행 하기 위한 개발자가 빠르고 코드 해제 방법 제공 하는 LoginView, LoginStatus, 및 LoginName 웹 컨트롤도 있습니다. 이후 자습서 이러한 오류 코드 및 다른 로그인 관련 웹 컨트롤 더 자세히 검토할 것입니다.

이 자습서에는 폼 인증의 대략적인 개요를 제공합니다. 우리 또는 되지 않은 다양 한 구성 옵션을 확인, 어떻게 cookieless 폼 인증 티켓 작업 확인 ASP.NET 폼 인증 티켓의 콘텐츠를 보호 하는 방법을 탐색 합니다. 다음과 같은 작용이에서 이러한 항목 등에 [다음 자습서](forms-authentication-configuration-and-advanced-topics-vb.md)합니다.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [Iis 6 및 IIS7 보안 간의 변경 사항](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/Changes-between-IIS6-and-IIS7-Security)
- [로그인 ASP.NET 컨트롤](https://msdn.microsoft.com/library/d51ttbhx.aspx)
- [전문 ASP.NET 2.0 보안, 구성원 자격 및 역할 관리](http://www.wrox.com/WileyCDA/WroxTitle/productCd-0764596985.html) (ISBN: 978-0-7645-9698-8)
- [&lt;인증&gt; 요소](https://msdn.microsoft.com/library/532aee0e.aspx)
- [&lt;forms&gt; 요소에 대 한 &lt;인증&gt;](https://msdn.microsoft.com/library/1d3t3c61.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>이 자습서에 포함 된 항목에 대 한 비디오 교육

- [ASP.NET에서 기본 폼 인증 사용](../../../videos/authentication/using-basic-forms-authentication-in-aspnet.md)

### <a name="about-the-author"></a>작성자 정보

여러 ASP/ASP.NET 책의 작성자 및 4GuysFromRolla.com의 창립자 Scott Mitchell의 근무 기간이 Microsoft 웹 기술을 1998 이후입니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은  *[Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)*합니다. Scott에 도달할 수 [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) 또는에서 그의 블로그 통해 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Alicja Maziarz, John Suru 및 Teresa 머피의 포함 됩니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com)합니다.

> [!div class="step-by-step"]
> [이전](security-basics-and-asp-net-support-vb.md)
> [다음](forms-authentication-configuration-and-advanced-topics-vb.md)
