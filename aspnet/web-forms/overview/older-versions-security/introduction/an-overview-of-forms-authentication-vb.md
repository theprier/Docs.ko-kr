---
uid: web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-vb
title: 폼 인증 (VB)의 개요 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 기능을 단순한 토론에서 구현 됩니다. 특히, 폼 인증을 구현 살펴봅니다. 웹 응용 프로그램 w...
ms.author: aspnetcontent
ms.date: 01/14/2008
ms.assetid: 83267f7d-64d9-41ee-82cf-da91b1bf534d
msc.legacyurl: /web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: 757cdebc436a4cb799f92374744ee9cb69eb0e0b
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37809461"
---
<a name="an-overview-of-forms-authentication-vb"></a>폼 인증 (VB) 개요
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/ASPNET_Security_Tutorial_02_VB.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/aspnet_tutorial02_FormsAuth_vb.pdf)

> 이 자습서에서는 기능을 단순한 토론에서 구현 됩니다. 특히, 폼 인증을 구현 살펴봅니다. 이 자습서에서 생성 하는 것이 먼저 웹 응용 프로그램 멤버 자격 및 역할에 간단한 폼 인증에서 이동 후속 자습서를 기반으로 구축 계속 됩니다.
> 
> 이 항목에 대 한 자세한 내용은이 비디오를 참조 하세요. [ASP.NET에서 사용 하 여 기본 폼 인증](# "using-basic-forms-authentication-in-aspnet")합니다.


## <a name="introduction"></a>소개

에 [이전 자습서](security-basics-and-asp-net-support-vb.md) ASP.NET에서 제공 되는 다양 한 인증, 권한 및 사용자 계정 옵션을 설명 했습니다. 이 자습서에서는 기능을 단순한 토론에서 구현 됩니다. 특히, 폼 인증을 구현 살펴봅니다. 이 자습서에서 생성 하는 것이 먼저 웹 응용 프로그램 멤버 자격 및 역할에 간단한 폼 인증에서 이동 후속 자습서를 기반으로 구축 계속 됩니다.

이 자습서에서는 이전 자습서에서 시 작업 항목 폼 인증 워크플로 자세히 살펴보기 시작 됩니다. 그런 다음, 폼 인증의 개념을 데모를 통해 ASP.NET 웹 사이트를 만듭니다. 다음으로 폼 인증을 사용 하 여 간단한 로그인 페이지를 만들고 여부를 확인, 코드에서 사용자가 인증, 그렇다면 사용자는 로그인 하는 방법은 사이트를 구성 됩니다.

폼 인증 워크플로 웹 응용 프로그램에서 사용 하도록 설정 하 고 로그인 및 로그 오프 페이지 만들기는 ASP.NET 응용 프로그램 사용자 계정만 지원 하 고 웹 페이지를 통해 사용자를 인증 하는 모든 중요 한 단계를 이해 합니다. 이 인해 이러한 자습서-서로 작성할 수 있으므로 바랍니다 지난 프로젝트의 폼 인증이 이미 환경을 구성 하는 경우에 다음 단계로 넘어가기 전에 전체에서이 자습서를 진행 하 고 있습니다.

## <a name="understanding-the-forms-authentication-workflow"></a>Forms 인증 워크플로 이해합니다.

ASP.NET 런타임은 ASP.NET 리소스의 경우는 ASP.NET 페이지 또는 ASP.NET 웹 서비스와 같은 요청을 처리할 때 요청에 해당 수명 주기 동안 이벤트 수가 발생 시킵니다. 요청이 인증 되 고 권한이 부여는 처리 되지 않은 예외 등의 경우 발생 하는 이벤트 발생 된 요청을 시작 하 고 매우 끝날 때 발생 하는 이벤트 가지가 있습니다. 이벤트의 전체 목록을 참조에 [HttpApplication 개체의 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication_events.aspx)합니다.

*HTTP 모듈* 는 요청 수명 주기에서 특정 이벤트에 대 한 응답에서 해당 코드가 실행 되는 관리 되는 클래스입니다. ASP.NET 여러 백그라운드에서 필수 작업을 수행 하는 HTTP 모듈이 함께 제공 됩니다. 특히 논의 관련 된 두 개의 기본 제공 HTTP 모듈 다음과 같습니다.

- **[FormsAuthenticationModule](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)**  -일반적으로 사용자의 쿠키 컬렉션에 포함 된 폼 인증 티켓을 검사 하 여 사용자를 인증 합니다. 없는 폼 인증 티켓이 있는 경우 사용자가 익명입니다.
- **[UrlAuthorizationModule](https://msdn.microsoft.com/library/system.web.security.urlauthorizationmodule.aspx)**  -현재 사용자는 요청 된 URL에 액세스할 권한이 있는지 여부를 결정 합니다. 이 모듈 응용 프로그램의 구성 파일에 지정 된 권한 부여 규칙을 참조 하 여 권한을 결정 합니다. ASP.NET도 포함 되어는 [FileAuthorizationModule](https://msdn.microsoft.com/library/system.web.security.fileauthorizationmodule.aspx) 기관 요청한 파일 Acl을 참조 하 여 결정 하는 합니다.

Formsauthenticationmodule은 실행 하는 UrlAuthorizationModule (및 FileAuthorizationModule) 전에 사용자를 인증 하려고 합니다. 권한 부여 모듈은 요청을 종료 하 고이 반환 요청을 만드는 사용자는 요청 된 리소스에 액세스할 수 있는 권한이 없습니다, 하는 경우는 [HTTP 401 권한이 없음](http://www.checkupdown.com/status/E401.html) 상태입니다. Windows 인증 시나리오에서 HTTP 401 상태는 브라우저에 반환 됩니다. 이 상태 코드에는 브라우저를 모달 대화 상자를 통해 자격 증명을 묻는 프롬프트를 발생 시킵니다. 그러나 폼 인증을 사용 하 여 HTTP 401 권한이 없음 상태로 전송 되지 않습니다 브라우저 formsauthenticationmodule은이 상태를 검색 하 고 대신에 로그인 페이지로 사용자를 리디렉션할 수정 하기 때문에 (통해는 [HTTP 302 리디렉션](http://www.checkupdown.com/status/E302.html) 상태).

로그인 페이지의 역할은 확인 하는 경우 사용자의 자격 증명이 유효한 경우 폼 인증 티켓을 만들고 페이지로 사용자를 리디렉션하는 하 려 했던 방문입니다. 인증 티켓 formsauthenticationmodule은 사용자를 식별 하는 웹 사이트에 있는 페이지에 대 한 후속 요청에 포함 됩니다.


[![Forms 인증 워크플로](an-overview-of-forms-authentication-vb/_static/image2.png)](an-overview-of-forms-authentication-vb/_static/image1.png)

**그림 01**: The Forms 인증 워크플로 ([큰 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image3.png))


### <a name="remembering-the-authentication-ticket-across-page-visits"></a>방문 페이지에서 인증 티켓을 기억

로그인 한 후 사이트를 검색할 때 사용자에 게 로그인 유지 되도록 각 요청에 대해 웹 서버에 다시 폼 인증 티켓이 전송 합니다. 이 일반적으로 사용자의 쿠키 컬렉션에서 인증 티켓을 배치 하 여 수행 됩니다. [쿠키](http://en.wikipedia.org/wiki/HTTP_cookie) 은 사용자의 컴퓨터에 상주 하 고 쿠키를 생성 하는 웹 사이트에 각 요청에서 HTTP 헤더에 전송 되는 작은 텍스트 파일입니다. 따라서 폼 인증 티켓이 생성 되었으며 브라우저의 쿠키에 저장 되 면 해당 사이트를 방문할 때마다 후속 있으므로 사용자를 식별 하는 요청과 함께 인증 티켓을 보냅니다.

> [!NOTE]
> 각 자습서에 사용 되는 데모 웹 응용 프로그램 다운로드로 제공 됩니다. 이 다운로드 가능한 응용 프로그램은.NET Framework 버전 3.5 대상으로 하는 Visual Web Developer 2008을 사용 하 여 생성 되었습니다. .NET 3.5에 대 한 응용 프로그램을 대상으로 하므로 해당 Web.config 파일 추가, 3.5 관련 구성 요소를 포함 합니다. 결론부터 말하자면, 다운로드할 수 있는 웹 응용 프로그램이 다음 컴퓨터에.NET 3.5를 설치 하려면 아직 Web.config에서 첫 번째 3.5 관련 태그를 제거 하지 않고 작동 하지 않습니다.


쿠키의 측면 중 하나는 해당 만료 날짜와 브라우저는 쿠키를 삭제 하는 시간입니다. 폼 인증 쿠키가 만료 되 면 사용자 인증 및 익명를 따라서 될 더 이상 수 없습니다. 공용 터미널에서 사용자가 방문 하는 경우 브라우저를 닫을 때 만료는 인증 티켓 하고자 하는 것이 경우가 있습니다. 그러나 집에서 방문 하는 경우 동일한 사용자 수도 없는 있도록 브라우저 다시 시작 후 저장 하려면 인증 티켓을 사이트를 방문할 때마다 다시 로그인 합니다. 이 의사 결정의 로그인 페이지에서 암호 저장 확인란의 형태로 사용자가 자주 이루어집니다. 3 단계에서에서 로그인 페이지에서 암호 저장 확인란을 구현 하는 방법을 살펴보겠습니다. 다음 자습서를 인증 티켓 시간 제한 설정을 자세히 다룹니다.

> [!NOTE]
> 웹 사이트에 로그온 하는 데 사용자 에이전트 쿠키를 지원 하지 않을 수 있습니다 것 같습니다. 이러한 경우 ASP.NET 쿠키 없는 폼 인증 티켓을 사용할 수 있습니다. 이 모드에서는 인증 티켓을 URL로 인코딩됩니다. 쿠키 없는 인증 티켓을 사용할 때와 만들어지고 다음 자습서에서 관리 되는 방법을 살펴보겠습니다.


### <a name="the-scope-of-forms-authentication"></a>폼 인증의 범위

Formsauthenticationmodule은 관리 되는 ASP.NET 런타임의 일부 코드입니다. Microsoft의 버전 7 이전의 [인터넷 정보 서비스 (IIS)](https://www.iis.net/) 웹 서버에 IIS의 HTTP 파이프라인 및 ASP.NET 런타임의 파이프라인 간에 고유한 장벽 했습니다. 즉, IIS 6 및 이전 버전에서는 IIS에서 ASP.NET 런타임에서 요청을 위임 FormsAuthenticationModule만 실행 합니다. 기본적으로 IIS 자체와 같은 정적 콘텐츠에 HTML 페이지 및 CSS 및 이미지 파일-요청 넘깁니다 때만 ASP.NET 런타임에서.aspx,.asmx 또는.ashx의 확장을 사용 하 여 페이지를 요청 하는 경우를 처리 합니다.

그러나 IIS 7 허용 통합된 IIS 및 ASP.NET에 대 한 파이프라인 합니다. 몇 가지 구성 설정을 사용 하 여 IIS 7에 대 한 formsauthenticationmodule은 호출을 설정할 수 있습니다 *모든* 요청 합니다. 또한 IIS 7을 사용 하 여 모든 형식의 파일에 대 한 URL 권한 부여 규칙을 정의할 수 있습니다. 자세한 내용은 [IIS7 보안과 변경 간에 IIS6](https://www.iis.net/learn/get-started/whats-new-in-iis-7/changes-in-security-between-iis-60-and-iis-7-and-above), [Your 웹 플랫폼 보안](https://www.iis.net/learn/get-started/whats-new-in-iis-7/iis7-and-above-security-improvements), 및 [이해 IIS7 URL 권한 부여](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/URL-Authorization/Understanding-IIS7-URL-Authorization)합니다.

결론부터 말하자면, IIS 7 이전 버전에서는, ASP.NET 런타임에 의해 처리 되는 리소스를 보호 하기 위해 폼 인증을만 사용할 수 있습니다. 마찬가지로, URL 권한 부여 규칙은 ASP.NET 런타임에 의해 처리 되는 리소스에만 적용 됩니다. 이지만 IIS 7을 사용 하 여 UrlAuthorizationModule 고 formsauthenticationmodule은 모든 요청에이 기능을 확장 함으로써 IIS의 HTTP 파이프라인에 통합할 수 있습니다.

## <a name="step-1-creating-an-aspnet-website-for-this-tutorial-series"></a>1 단계:이 자습서 시리즈에 대 한 ASP.NET 웹 사이트 만들기

많은 도달 하기 위해 ASP.NET 웹 사이트는이 시리즈 전체 작성할 Visual Studio 2008의 Microsoft의 무료 버전을 사용 하 여 생성 됩니다 [Visual Web Developer 2008](https://www.microsoft.com/express/vwd/)합니다. SqlMembershipProvider 사용자 저장소에서 구현 된 [Microsoft SQL Server 2005 Express Edition](https://msdn.microsoft.com/sql/Aa336346.aspx) 데이터베이스입니다. Visual Studio 2005 또는 Visual Studio 2008 또는 SQL Server의 다른 버전을 사용 하는 경우 걱정 하지 마세요-단계를 거의 동일 하 고 trivial이 아닌 모든 차이점을 지적 합니다.

인증 서비스를 구성할 수 있습니다, 전에 먼저 ASP.NET 웹 사이트를 해야 합니다. 새 파일 시스템 기반 ASP.NET 웹 사이트를 만들어 시작 합니다. 이렇게 하려면 Visual Web Developer를 시작 하 파일 메뉴로 이동 하 고 새 웹 사이트 대화 상자를 표시 하는 새 웹 사이트를 선택. ASP.NET 웹 사이트 템플릿을 선택, 파일 시스템 위치 드롭 다운 목록 설정, 웹 사이트를 배치할 폴더를 선택 및 VB.에 언어를 설정 합니다. Default.aspx ASP.NET 페이지, 앱을 사용 하 여이 새 웹 사이트를 만듭니다\_데이터 폴더 및 Web.config 파일입니다.

> [!NOTE]
> Visual Studio는 프로젝트 관리의 두 가지 모드를 지원 합니다: 웹 사이트 프로젝트와 웹 응용 프로그램 프로젝트입니다. 웹 사이트 프로젝트는 프로젝트 아키텍처에 Visual Studio.NET 2002/2003을 모방 하는 웹 응용 프로그램 프로젝트-프로젝트 파일을 포함 하 고 /bin 폴더에 배치 되는 단일 어셈블리를 프로젝트의 소스 코드를 컴파일할 때 반면 프로젝트 파일을 부족 합니다. Visual Studio 2005 처음에 지원 되는 웹 사이트 프로젝트에 있지만 서비스 팩 1을 사용 하 여 웹 응용 프로그램 프로젝트 모델을 다시 도입 되었습니다. Visual Studio 2008 프로젝트 모델을 모두 제공합니다. 그러나 Visual Web Developer 2005 및 2008 edition만 지원 웹 사이트 프로젝트입니다. 웹 사이트 프로젝트 모델로 사용 하겠습니다. Express 이외의 버전을 사용 하는 사용 하려면 합니다 [웹 응용 프로그램 프로젝트 모델](https://msdn.microsoft.com/library/aa730880(vs.80).aspx) 대신 자유롭게 있을 수 있다는 일부 불일치 화면 및 수행 해야 하는 단계에 표시 되는 내용 간에 수 있지만 이렇게 합니다 이 자습서에 제공 된 지침을 표시 하는 스크린 샷


[![새 파일 시스템 기반 웹 사이트 만들기](an-overview-of-forms-authentication-vb/_static/image5.png)](an-overview-of-forms-authentication-vb/_static/image4.png)

**그림 02**: New File System-Based 웹 사이트 만들기 ([큰 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image6.png))


### <a name="adding-a-master-page"></a>마스터 페이지 추가

다음으로 사이트 Site.master 명명 된 루트 디렉터리에 새 마스터 페이지를 추가 합니다. [마스터 페이지](https://msdn.microsoft.com/library/wtxbf3hh.aspx) ASP.NET 페이지에 적용할 수 있는 사이트 전체 템플릿을 정의 하는 페이지 개발자를 사용 하도록 설정 합니다. 마스터 페이지의 주요 장점은 사이트의 전체적인 모양을 정의할 수 있습니다 단일 위치에 있으므로 간편 하 게 업데이트 하거나 사이트의 레이아웃을 조정입니다.


[![마스터 페이지 추가 웹 사이트에 Site.master 라는](an-overview-of-forms-authentication-vb/_static/image8.png)](an-overview-of-forms-authentication-vb/_static/image7.png)

**그림 03**: 웹 사이트에 마스터 페이지 라는 Site.master 추가 ([큰 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image9.png))


마스터 페이지에서 사이트 전체 페이지 레이아웃 여기를 정의 합니다. 디자인 뷰를 사용할 수 있으며 필요한 모든 레이아웃 또는 웹 컨트롤을 추가 하거나 수동으로 소스 뷰에서 태그를 수동으로 추가할 수 있습니다. 마스터 페이지의 레이아웃에 사용 되는 레이아웃을 모방을 구조적 합니까 내 *[ASP.NET 2.0에서 데이터로 작업할](../../data-access/index.md)* 자습서 시리즈 (그림 4 참조). 마스터 페이지를 사용 하 여 [cascading style sheet](http://www.w3schools.com/css/default.asp) 위치 (이 자습서의 관련된 다운로드에 포함 됨)는 Style.css 파일에 정의 된 CSS 설정 사용 하 여 스타일에 대 한 합니다. 아래에 표시 된 태그에서 알 수 없습니다, 하는 동안 CSS 규칙을 정의 하는 탐색 &lt;div&gt;의 콘텐츠는 왼쪽에 표시 되 고 고정 너비가 200 픽셀이 있도록 절대적으로 배치 됩니다.

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample1.aspx)]

마스터 페이지에는 정적 페이지 레이아웃 및 마스터 페이지를 사용 하는 ASP.NET 페이지에서 편집할 수 있는 지역을 정의 합니다. 이러한 콘텐츠 편집 가능한 영역 콘텐츠 내에서 볼 수 있는 ContentPlaceHolder 컨트롤로 표시 됩니다 &lt;div&gt;합니다. 마스터 페이지는 단일 ContentPlaceHolder (MainContent) 갖지만 마스터 페이지의 여러 ContentPlaceHolders 있을 수 있습니다.

위에 입력 한 태그를 사용 하 여 마스터 페이지의 레이아웃을 표시 디자인 뷰로 전환 합니다. 이 마스터 페이지를 사용 하는 모든 ASP.NET 페이지 MainContent 영역에 대 한 태그를 지정 하는 기능을 사용 하 여이 균일 한 레이아웃을 갖게 됩니다.


[![마스터 페이지, 디자인 뷰를 통해 볼 때](an-overview-of-forms-authentication-vb/_static/image11.png)](an-overview-of-forms-authentication-vb/_static/image10.png)

**그림 04**:의 마스터 페이지 때 볼 통해 디자인 뷰 ([큰 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image12.png))


### <a name="creating-content-pages"></a>콘텐츠 페이지 만들기

이 시점에서 Default.aspx 페이지는 웹 사이트에 있지만 방금 만든 마스터 페이지를 사용 하지 않습니다. 페이지 내용이 없는 경우 마스터 페이지를 사용 하 여 웹 페이지의 선언적 태그를 조작할 수 있지만 아직 쉽습니다만 페이지를 삭제 하 고 다시 지정 마스터 페이지를 사용 하 여 프로젝트에 추가 합니다. 따라서 프로젝트에서 Default.aspx를 삭제 하 여 시작 합니다.

다음으로, 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 Default.aspx 라는 새 Web Form을 추가 하려면 선택 합니다. 이 이번에 마스터 페이지 선택 확인란을 선택 하 고 목록에서 Site.master 마스터 페이지를 선택 합니다.


[![마스터 페이지를 선택 하는 새 Default.aspx 페이지 추가](an-overview-of-forms-authentication-vb/_static/image14.png)](an-overview-of-forms-authentication-vb/_static/image13.png)

**그림 05**:를 새 Default.aspx 페이지 선택 마스터 페이지를 선택 하려면 추가 ([큰 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image15.png))


[![Site.master 마스터 페이지를 사용 합니다.](an-overview-of-forms-authentication-vb/_static/image17.png)](an-overview-of-forms-authentication-vb/_static/image16.png)

**그림 06**: Site.master 마스터 페이지를 사용 하 여 ([큰 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image18.png))


> [!NOTE]
> 웹 응용 프로그램 프로젝트 모델을 사용 하는 경우 새 항목 추가 대화 상자에는 마스터 페이지 선택 확인란을 포함 되지 않습니다. 대신, 웹 콘텐츠 폼 형식의 항목을 추가 해야 합니다. Visual Studio에서 동일한 Select 마스터를 표시 하는 데 웹 콘텐츠 폼 옵션을 선택 하 고 추가 클릭 한 후 그림 6 에서처럼 대화 상자가 있습니다.


새 Default.aspx 페이지의 선언적 태그만 포함을 @Page 마스터에 대 한 경로 지정 하는 지시문 MainContent ContentPlaceHolder 마스터 페이지의 파일 및 콘텐츠 컨트롤을 페이지입니다.

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample2.aspx)]

지금은 Default.aspx를 비워 둡니다. 에서는 콘텐츠를 추가 하려면이 자습서의 뒷부분에 나오는를 반환 합니다.

> [!NOTE]
> 마스터 페이지 메뉴 또는 다른 탐색 인터페이스에 대 한 섹션을 포함 합니다. 이후 자습서에서 이러한 인터페이스를 만들겠습니다.


## <a name="step-2-enabling-forms-authentication"></a>2 단계: 폼 인증을 사용 하도록 설정

ASP.NET 웹 사이트를 만든 다음이 작업은 폼 인증을 사용 하도록 설정입니다. 응용 프로그램의 인증 구성을 통해 지정 되는 [ &lt;인증&gt; 요소](https://msdn.microsoft.com/library/532aee0e.aspx) Web.config에서. 합니다 &lt;인증&gt; 요소 응용 프로그램에서 사용 되는 인증 모델을 지정 하는 모드 라는 단일 특성을 포함 합니다. 이 특성은 다음 네 가지 값 중 하나일 수 있습니다.

- **Windows** -응용 프로그램이 Windows 인증을 사용 하는 경우 이전 자습서에서 설명한 대로 방문자를 인증 해야 하는 웹 서버의 이며 일반적으로 이렇게 Basic, Digest 또는 Windows 통합 인증 합니다.
- **Forms**-사용자는 웹 페이지 상의 폼을 통해 인증 됩니다.
- **Passport**-사용자는 Microsoft Passport Network를 사용 하 여 인증 됩니다.
- **None**-없음 인증 모델을 사용 하는 모든 방문자 익명입니다.

기본적으로 ASP.NET 응용 프로그램 Windows 인증을 사용 합니다. 인증 유형을 폼 인증을 변경 하려면 다음을 수정 해야 합니다 &lt;인증&gt; forms 요소의 모드 특성입니다.

프로젝트에 아직 없는 경우 Web.config 파일을 하나의 이제에서 마우스 오른쪽 단추로 클릭 솔루션 탐색기에서 프로젝트 이름을 새 항목 추가 선택 하 고 웹 구성 파일을 추가 하는 다음을 추가 합니다.


[![프로젝트는 Web.config를 아직 포함 되지 않은, 경우 지금 추가](an-overview-of-forms-authentication-vb/_static/image20.png)](an-overview-of-forms-authentication-vb/_static/image19.png)

**그림 07**: 경우 Your 프로젝트 않습니다 하지 아직 포함 Web.config, 추가 지금 ([큰 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image21.png))


다음으로 &lt;인증&gt; 요소 및 폼 인증을 사용 하도록 업데이트 합니다. 이렇게이 변경한 후 Web.config 파일의 태그는 다음과 비슷하게 표시 됩니다.

[!code-xml[Main](an-overview-of-forms-authentication-vb/samples/sample3.xml)]

> [!NOTE]
> Web.config XML 파일 이므로 대/소문자는 중요 합니다. 6. 대문자를 사용 하 여 양식 모드 특성을 설정 되었는지 확인 대/소문자, 폼 등을 사용 하는 경우 받게 구성 오류가 브라우저를 통해 사이트를 방문할 때.


&lt;인증&gt; 요소를 선택적으로 포함할 수는 &lt;forms&gt; forms 인증 관련 설정이 포함 된 자식 요소입니다. 지금은 기본 폼 인증 설정 뿐 사용해 보겠습니다. 살펴봅니다 합니다 &lt;forms&gt; 다음 자습서에서 자세히 자식 요소입니다.

## <a name="step-3-building-the-login-page"></a>로그인 페이지를 구성 하는 3 단계:

폼 인증을 지원 하기 위해 웹 사이트에는 로그인 페이지를 해야 합니다. Formsauthenticationmodule은 인증 워크플로 Forms 섹션을 자동으로 리디렉션됩니다 이해에 설명 된 대로 로그인 페이지로 사용자 없는 페이지에 액세스 하려고 할 경우를 볼 권한이 있습니다. 익명 사용자에 게 로그인 페이지에 대 한 링크를 표시 하는 ASP.NET 웹 컨트롤이 있습니다. 이 위반한 로그인 페이지의 URL은 무엇입니까?

기본적으로 폼 인증 시스템 Login.aspx 이라는 이름으로 로그인 페이지를 예상 하 고 웹 응용 프로그램의 루트 디렉터리에 배치 합니다. 다른 로그인 페이지 URL을 사용 하려는 경우 Web.config를 사용 하 여 이렇게 수 있습니다. 이후 자습서에서이 작업을 수행 하는 방법을 살펴보겠습니다.

로그인 페이지에는 세 가지 책임에 있습니다.

1. 방문자에 게 자격 증명을 허용 하는 인터페이스를 제공 합니다.
2. 제출 된 자격 증명이 유효 하는 경우를 결정 합니다.
3. 폼 인증 티켓을 만들어 사용자를 로그인 합니다.

### <a name="creating-the-login-pages-user-interface"></a>로그인 페이지의 사용자 인터페이스 만들기

이제 첫 번째 작업을 사용 하 여 시작 하세요. Login.aspx 라는 사이트의 루트 디렉터리에 새 ASP.NET 페이지를 추가 하 고 Site.master 마스터 페이지를 사용 하 여 연결 합니다.


[![새 ASP.NET 페이지를 추가 Login.aspx 라는](an-overview-of-forms-authentication-vb/_static/image23.png)](an-overview-of-forms-authentication-vb/_static/image22.png)

**그림 08**: 새 ASP.NET 페이지 라는 Login.aspx 추가 ([큰 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image24.png))


일반 로그인 페이지 인터페이스를 두 개의 텍스트 상자-사용자의 이름에 대해 하나씩,-자신의 암호 및 폼을 전송 하는 단추에 대 한 이루어져 있습니다. 웹 사이트에 암호 저장 확인란을 선택 하는 경우 결과 인증 티켓을 브라우저를 다시 시작 간에 유지 되는 경우가 많습니다 포함 됩니다.

Login.aspx로 두 개의 텍스트 상자를 추가 하 고 해당 ID 속성 이름 및 암호를 각각 설정 합니다. 또한 암호로 암호의 하려면 TextMode 속성을 설정 합니다. 다음으로 RememberMe me. 이름 및 암호를 해당 텍스트 속성을 해당 ID 속성을 설정 하 여 CheckBox 컨트롤을 추가 그런 다음, 로그인 텍스트 속성을 설정할 LoginButton 라는 단추를 추가 합니다. 및 마지막으로, Label 웹 컨트롤을 추가 및 ID 속성 설정에 InvalidCredentialsMessage, 해당 텍스트 속성을 사용자 이름 또는 암호가 잘못 되었습니다. 다시 시도 하세요., 빨강으로 해당 ForeColor 속성 및 해당 Visible 속성을 False로 합니다.

이 시점에서 화면 그림 9에서 스크린샷과 비슷하게 표시 됩니다 하 고 페이지의 선언적 구문을 다음과 같아야 합니다.

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample4.aspx)]


[![로그인 페이지에 두 개의 텍스트 상자, 확인란, 단추 및 레이블이 포함](an-overview-of-forms-authentication-vb/_static/image26.png)](an-overview-of-forms-authentication-vb/_static/image25.png)

**그림 09**:의 로그인 페이지에 두 개의 텍스트 상자, 확인란, 단추 및 레이블이 ([큰 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image27.png))


마지막으로, LoginButton의 클릭 이벤트 처리기를 만들 이벤트입니다. 디자이너에서이 이벤트 처리기를 만드는 단추 컨트롤 두 번 클릭 하기만 하면 됩니다.

### <a name="determining-if-the-supplied-credentials-are-valid"></a>제공 된 자격 증명이 올바른 경우 확인

이제 단추 클릭에서 작업 2를 구현 해야 이벤트 처리기-제공 된 자격 증명이 유효한 지 여부를 결정 합니다. 설정 하려면 제공된 된 자격 증명 알려진된 자격 증명을 사용 하 여 일치 하는 경우 확인 수 있도록 모든 사용자의 자격 증명을 보유 하는 사용자 저장소에 있어야 합니다.

ASP.NET 2.0 이전 개발자 모두 자신의 사용자 저장소를 구현 하 고 저장소에 대해 제공된 된 자격 증명의 유효성을 검사 하는 코드를 작성 하는 일을 담당 했습니다. 대부분의 개발자 명명 된 사용자 사용자 이름, 암호, 전자 메일, LastLoginDate, 등과 같은 열이 있는 테이블을 만드는 사용자 저장소를 데이터베이스에서 구현할 수 있습니다. 그런 다음이 테이블에서 사용자 계정 마다 하나의 레코드를 해야 합니다. 일치 하는 사용자 이름에 대 한 데이터베이스를 쿼리하고 다음 데이터베이스에 암호를 제공 된 암호에 해당 하는 보장에 사용자의 제공 된 자격 증명을 확인 하는 작업이 포함 됩니다.

ASP.NET 2.0에서는 개발자가 하나를 사용 해야 멤버 자격 공급자의 사용자 저장소를 관리 하 합니다. 이 자습서 시리즈의 사용자 저장소에 대 한 SQL Server 데이터베이스를 사용 하 여 SqlMembershipProvider를 사용 합니다. SqlMembershipProvider를 사용 하는 경우 테이블, 뷰 및 공급자가 예상 하는 저장된 프로시저를 포함 하는 특정 데이터베이스 스키마를 구현 해야 합니다. 이 스키마를 구현 하는 방법을 살펴보겠습니다 합니다 *[SQL Server에서 멤버 자격 스키마 만들기](../membership/creating-the-membership-schema-in-sql-server-vb.md)* 자습서입니다. 되어에서 멤버 자격 공급자를 사용 하 여 사용자의 자격 증명 유효성 검사 간단 하 게 호출 합니다 [멤버 자격 클래스](https://msdn.microsoft.com/library/system.web.security.membership.aspx)의 [ValidateUser (*username*, *암호*) 메서드](https://msdn.microsoft.com/library/system.web.security.membership.validateuser.aspx)를 나타내는 부울 값을 반환 하는 여부를의 유효성을 검사 합니다 *사용자 이름* 및 *암호* 조합 합니다. SqlMembershipProvider의 사용자 저장소에 아직 구현 하지 않았기 하는 대로 표시 지금은 구성원 클래스의 ValidateUser 메서드를 사용할 수 없습니다.

하는 시간이 고유한 사용자 지정 사용자가 데이터베이스 테이블 (이 사용 되지 않는 SqlMembershipProvider를 구현한 것)를 빌드 해 보겠습니다 대신 하드 코딩 하지 않고 유효한 자격 증명을 로그인에 자체 페이지입니다. LoginButton의 클릭 이벤트 처리기에 다음 코드를 추가 합니다.

[!code-vb[Main](an-overview-of-forms-authentication-vb/samples/sample5.vb)]

알 수 있듯이-Scott, Jisun, 및 Sam-세 가지 유효한 사용자 계정이 있고 세 가지 모두 동일한 암호 (password). 코드를 올바른 사용자 이름 및 암호 일치를 찾고 사용자 이름 및 암호 배열을 반복 합니다. 사용자 이름 및 암호 유효 사용자를 로그인 하 여 해당 페이지로 리디렉션하도록 해야 합니다. 자격 증명이 잘못 된 경우 InvalidCredentialsMessage 레이블이 표시 됩니다.

사용자가 유효한 자격 증명을 입력 하는 경우 해당 페이지로 리디렉션됩니다 다음 언급 했습니다. 하지만 적절 한 페이지에서 새로운 기능? 사용자가 보려는 허가 되지 않은 페이지를 방문 하면 formsauthenticationmodule은 자동으로 리디렉션되어 로그인 페이지에 회수 합니다. 이 과정에서 요청된 된 URL ReturnUrl 매개 변수를 통해 쿼리 문자열에 포함 됩니다. 즉, ProtectedPage.aspx를 방문 하 여 사용자가 수행할 수 있는 권한이 없습니다 되었습니다 경우 FormsAuthenticationModule 리디렉션하 하도록 합니다.

Login.aspx?ReturnUrl=ProtectedPage.aspx

성공적으로 로그인 할 때 사용자 ProtectedPage.aspx로 리디렉션되어야 합니다. 또는 사용자가 자신의 volition의 로그인 페이지를 방문 수 있습니다. 이 경우 사용자를 로그인 한 후 이러한 보내야 루트 폴더의 Default.aspx 페이지.

### <a name="logging-in-the-user"></a>사용자 로그인

제공 된 자격 증명이 유효 가정 하므로 사이트에 사용자를 로그인 폼 인증 티켓을 만드는 해야 합니다. 합니다 [FormsAuthentication 클래스](https://msdn.microsoft.com/library/system.web.security.formsauthentication.aspx) 에 [System.Web.Security 네임 스페이스](https://msdn.microsoft.com/library/system.web.security.aspx) 인증 시스템 로깅 및 폼을 통해 사용자 로깅에 대 한 다양 한 메서드를 제공 합니다. FormsAuthentication 클래스에서 여러 가지가 있습니다 하지만 관심이 시점에 세 가지 합니다.

- [GetAuthCookie (*사용자 이름*를 *persistCookie*)](https://msdn.microsoft.com/library/system.web.security.formsauthentication.getauthcookie.aspx) -제공 된 이름에 대 한 폼 인증 티켓을 만들어 *username*합니다. 다음으로,이 메서드를 만들어 인증 티켓의 내용이 들어 있는 HttpCookie 개체를 반환 합니다. 하는 경우 *persistCookie* 가 True 인 영구 쿠키 만들어집니다.
- [SetAuthCookie (*사용자 이름*를 *persistCookie*)](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx) -는 GetAuthCookie 호출 (*username*를 *persistCookie*) 폼 인증 쿠키를 생성 하는 메서드. 이 메서드는 다음 GetAuthCookie (forms 쿠키 기반 인증을 사용 하지 않으면,이 메서드를 호출 하는 쿠키 티켓 논리를 처리 하는 내부 클래스 라고 가정) 쿠키 컬렉션에 반환한 쿠키를 추가 합니다.
- [RedirectFromLoginPage (*사용자 이름*를 *persistCookie*)](https://msdn.microsoft.com/library/system.web.security.formsauthentication.redirectfromloginpage.aspx) -SetAuthCookie 호출 (*username*, *persistCookie*), 다음 적절 한 페이지로 사용자를 리디렉션합니다.

GetAuthCookie 인증 티켓 쿠키 컬렉션에 쿠키를 작성 하기 전에 수정 해야 할 때 유용 합니다. SetAuthCookie 폼 인증 티켓을 만들기 및 쿠키 컬렉션에 추가 하려고 하지만 해당 페이지에 사용자를 리디렉션할 하지 않으려는 경우에 유용 합니다. 로그인 페이지에 보관 하거나 일부 다른 페이지로 보낼 하려는 경우가 있을 것입니다.

사용자를 로그인 하 고 해당 페이지로 리디렉션하도록 하고자 하므로 RedirectFromLoginPage를 사용해 보겠습니다. 업데이트 LoginButton의 클릭 이벤트 처리기를 두 주석 처리 된 TODO 줄을 다음 줄의 코드로 대체 합니다.

FormsAuthentication.RedirectFromLoginPage(UserName.Text, RememberMe.Checked)

폼 인증 티켓에 대 한 사용자 이름 텍스트 상자의 Text 속성을 사용 했습니다 폼 인증 티켓을 만들 때 *사용자 이름* 매개 변수 및 RememberMe 확인란의 선택된 상태를  *persistCookie* 매개 변수입니다.

로그인 페이지를 테스트 하려면 브라우저에서 참조 하세요. Nope의 사용자 이름 및 잘못 된 암호와 같은 잘못 된 자격 증명을 입력 하 여 시작 합니다. 로그인 단추를 클릭 하면 포스트백을 발생 하 고 InvalidCredentialsMessage 레이블이 표시 됩니다.


[![InvalidCredentialsMessage 레이블이 표시 되는 경우 입력 잘못 된 자격 증명 되었습니다.](an-overview-of-forms-authentication-vb/_static/image29.png)](an-overview-of-forms-authentication-vb/_static/image28.png)

**그림 10**: The InvalidCredentialsMessage 레이블이 표시 되는 경우 입력 잘못 된 자격 증명 되었습니다 ([큰 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image30.png))


다음으로, 유효한 자격 증명을 입력 하 고 [로그인] 단추를 클릭 합니다. 포스트백 폼 인증 티켓을 발생 하는 경우이 이번 만들어지고 Default.aspx로 다시 자동으로 리디렉션됩니다. 이 시점에 로그인 한 웹 사이트에 현재 로그인을 나타내기 위해 시각 신호 없음 있기는 합니다. 또는 페이지를 방문 하는 사용자를 식별 하는 방법 뿐만 아니라 하지 프로그래밍 방식으로 사용자 여부를 결정 하는 방법을 살펴보겠습니다 4 단계에서에서 기록 됩니다.

5 단계는 사용자 웹 사이트에서 로그 아웃 로깅에 대 한 기술 검사 합니다.

### <a name="securing-the-login-page"></a>로그인 페이지를 보호합니다.

-자신의 암호를 포함 하 여-자격 증명을 웹 서버에 인터넷을 통해 전송 됩니다 때 사용자가 자격 증명을 입력 하 고 로그인 페이지 양식 제출 합니다 *일반 텍스트*합니다. 즉, 사용자 이름 및 암호를 네트워크 트래픽을 검사 하는 모든 해커가 볼 수 있습니다. 이 방지 하려면 반드시 사용 하 여 네트워크 트래픽을 암호화할 [보안 소켓 레이어 (SSL)](http://en.wikipedia.org/wiki/Secure_Sockets_Layer)합니다. 이렇게 하면 자격 증명 (뿐만 아니라 전체 페이지의 HTML 태그) 웹 서버에서 수신 될 때까지 브라우저를 떠날 순간부터 암호화 됩니다.

중요 한 정보를 포함 하는 웹 사이트, 하지 않는 한 하기만 하면 됩니다 SSL을 사용 하도록 로그인 페이지에 다른 페이지에 일반 텍스트로 네트워크를 통해 그렇지 않은 경우 사용자의 암호를 보낼 수 있습니다. 폼 인증 티켓 기본적으로 모두 암호화 되어 (변조를 방지) 디지털 서명 되므로 보안에 대해 걱정할 필요가 없습니다. 폼 인증 티켓 보안 더 상세히 논의 다음 자습서에 표시 됩니다.

> [!NOTE]
> 많은 금융 및 의료 웹 사이트에서 SSL을 사용 하도록 구성 된 *모든* 페이지에 액세스할 수 있는 사용자를 인증 합니다. 이러한 웹 사이트를 구축 하는 경우 폼 인증 티켓은 보안 연결을 통해 전송 되도록 forms 인증 시스템을 구성할 수 있습니다. 다음 자습서에서는 다양 한 폼 인증 구성 옵션에 살펴보겠습니다  *[폼 인증 구성 및 고급 항목](../membership/creating-the-membership-schema-in-sql-server-vb.md)* 합니다.


## <a name="step-4-detecting-authenticated-visitors-and-determining-their-identity"></a>4 단계: 인증 된 방문자를 검색 하 고 해당 Id를 확인 합니다.

이 시점에서 폼 인증을 사용 하도록 설정 하 고 기본적인 로그인 페이지를 만들 수 있지만 인증 또는 익명 사용자 인지 여부를 확인할 수 있습니다 하는 방법을 검사할 아직 있습니다. 특정 시나리오에서 다른 데이터 또는 인증 또는 익명 사용자 페이지를 방문 하는 여부에 따라 정보를 표시 하려고 수 있습니다. 또한 종종 해야 인증된 된 사용자의 id를 알아야 합니다.

이러한 기법을 설명 하기 위해 기존 Default.aspx 페이지를 확장 해 보겠습니다. Default.aspx에서 하나의 명명 된 AuthenticatedMessagePanel 및 다른 명명 된 AnonymousMessagePanel 두 개의 패널 컨트롤을 추가 합니다. 첫 번째 패널에서 WelcomeBackMessage 이라는 레이블 컨트롤을 추가 합니다. 두 번째 하이퍼링크 컨트롤을 추가, 로그인 및 해당 NavigateUrl 속성을 Text 속성을 설정 합니다. ~ / Login.aspx입니다. 이 시점에서 Default.aspx에 대 한 선언적 태그는 다음과 비슷하게 표시 됩니다.

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample6.aspx)]

짐작할 아마도 지금쯤, 여기서 인증 된 방문자를 익명 방문자에 게 AnonymousMessagePanel 방금 AuthenticatedMessagePanel만 표시 됩니다. 이렇게 하려면 사용자의 로그인 여부 여부에 따라 이러한 패널의 표시 속성을 설정 해야 합니다.

합니다 [Request.IsAuthenticated 속성](https://msdn.microsoft.com/library/system.web.httprequest.isauthenticated.aspx) 요청이 인증 되었는지 여부를 나타내는 부울 값을 반환 합니다. 페이지에 다음 코드를 입력\_이벤트 처리기 코드를 로드 합니다.

[!code-vb[Main](an-overview-of-forms-authentication-vb/samples/sample7.vb)]

이 코드를 사용 하 여 브라우저를 통해 Default.aspx를 방문 합니다. 로그인 페이지에 대 한 링크 표시는 가정 하 고 있으 니 아직 로그인 (그림 11 참조). 이 링크를 클릭 하 고 사이트에 로그인 합니다. 3 단계에서에서 살펴본 것 처럼 자격 증명을 입력 한 후 사용자에 게 반환할 Default.aspx를 하지만이 시간은 페이지를 다시 시작을 보여 줍니다. (그림 12 참조)의 메시지입니다.


[![방문 익명으로 링크의 로그를 표시할 때](an-overview-of-forms-authentication-vb/_static/image32.png)](an-overview-of-forms-authentication-vb/_static/image31.png)

**그림 11**: 때 방문 익명, 링크의 로그 표시 됩니다 ([큰 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image33.png))


[![인증 된 사용자 다시 시작을 표시 됩니다. 메시지](an-overview-of-forms-authentication-vb/_static/image35.png)](an-overview-of-forms-authentication-vb/_static/image34.png)

**그림 12**: 인증 된 사용자는 다시 시작을 표시 됩니다. 메시지 ([클릭 하 여 큰 이미지 보기](an-overview-of-forms-authentication-vb/_static/image36.png))


통해 현재 로그온된 한 사용자의 신원을 확인할 수 있습니다 합니다 [HttpContext 개체](https://msdn.microsoft.com/library/system.web.httpcontext.aspx)의 [사용자 속성](https://msdn.microsoft.com/library/system.web.httpcontext.user.aspx)합니다. HttpContext 개체는 현재 요청에 대 한 정보를 나타내는 이며 특히 응답, 요청 및 세션 등과 같은 공통 ASP.NET 개체에 대 한 홈입니다. 사용자 속성의 현재 HTTP 요청 및 구현 보안 컨텍스트를 나타내는 합니다 [IPrincipal 인터페이스](https://msdn.microsoft.com/library/system.security.principal.iprincipal.aspx)합니다.

사용자 속성 FormsAuthenticationModule로 설정 됩니다. 특히 formsauthenticationmodule은 들어오는 요청의 폼 인증 티켓을 찾으면 새 GenericPrincipal 개체를 만들고 사용자 속성에 할당 합니다.

보안 주체 개체 (예: GenericPrincipal)는 사용자의 id에 속하는 역할 정보를 제공 합니다. IPrincipal 인터페이스는 두 명의 멤버를 정의합니다.

- [IsInRole (*roleName*)](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole.aspx) -보안 주체가 지정된 된 역할에 속할 경우를 나타내는 부울 값을 반환 하는 메서드입니다.
- [Identity](https://msdn.microsoft.com/library/system.security.principal.iprincipal.identity.aspx) -구현 하는 개체를 반환 하는 속성을 [IIdentity 인터페이스](https://msdn.microsoft.com/library/system.security.principal.iidentity.aspx)합니다. IIdentity 인터페이스를 사용 하는 세 가지 속성을 정의 합니다. [AuthenticationType](https://msdn.microsoft.com/library/system.security.principal.iidentity.authenticationtype.aspx), [IsAuthenticated](https://msdn.microsoft.com/library/system.security.principal.iidentity.isauthenticated.aspx), 및 [이름](https://msdn.microsoft.com/library/system.security.principal.iidentity.name.aspx)합니다.

다음 코드를 사용 하 여 현재 방문자의 이름을 확인할 수 있습니다.

As String currentUsersName dim User.Identity.Name =

사용 하 여 폼 인증을, 하는 경우는 [FormsIdentity 개체](https://msdn.microsoft.com/library/system.web.security.formsidentity.aspx) GenericPrincipal의 Identity 속성에 대해 생성 됩니다. FormsIdentity 클래스는 항상 해당 IsAuthenticated 속성에 대 한 문자열 폼의 AuthenticationType 속성에 True를 반환합니다. Name 속성에는 폼 인증 티켓을 만들 때 지정한 사용자 이름을 반환 합니다. 이러한 세 가지 속성 외에도 FormsIdentity 포함을 통해 기본 인증 티켓에 대 한 액세스를 해당 [속성을 티켓](https://msdn.microsoft.com/library/system.web.security.formsidentity.ticket.aspx). Ticket 속성 형식의 개체를 반환 합니다. [FormsAuthenticationTicket](https://msdn.microsoft.com/library/system.web.security.formsauthenticationticket.aspx), 만료, IsPersistent, IssueDate, 이름 등 속성이 있는 합니다.

중요 한 부분은 여기는 합니다 *사용자 이름* 는 FormsAuthentication.GetAuthCookie에 지정 된 매개 변수 (*username*, *persistCookie*), FormsAuthentication.SetAuthCookie (*사용자 이름*, *persistCookie*), 및 FormsAuthentication.RedirectFromLoginPage (*username*합니다 *persistCookie*) 메서드 User.Identity.Name 반환한 동일한 값입니다. 또한 이러한 메서드에서 생성 된 인증 티켓은 User.Identity FormsIdentity 개체를 캐스팅 하 고 다음 Ticket 속성에 액세스 하 여 제공 됩니다.

Ident으로 FormsIdentity dim CType (User.Identity, FormsIdentity) =

Dim authTicket As FormsAuthenticationTicket = ident.Ticket

Default.aspx에서 보다 개별화 된 메시지를 제공 하겠습니다. 페이지를 업데이트할\_WelcomeBackMessage 레이블의 텍스트 속성 문자열 시작 다시 할당 되도록 이벤트 처리기를 로드 *username*!

WelcomeBackMessage.Text = "Welcome back, " &amp; User.Identity.Name &amp; "!"

그림 13 (Scott 사용자로 로그인) 하는 경우이 수정 작업의 결과 보여 줍니다.


[![환영 메시지는 사용자의 이름에 현재 로그온 한 포함](an-overview-of-forms-authentication-vb/_static/image38.png)](an-overview-of-forms-authentication-vb/_static/image37.png)

**그림 13**: 시작 메시지를 포함 하는 현재 로그온 한 사용자의 이름 ([큰 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image39.png))


### <a name="using-the-loginview-and-loginname-controls"></a>LoginView 및 LoginName 컨트롤을 사용 하 여

인증 및 익명 사용자에 게 다른 콘텐츠를 표시 하는 것은 일반적인 요구 사항; 따라서를 현재 로그온된 한 사용자의 이름을 표시 합니다. 따라서 ASP.NET 코드 한 줄도 작성할 필요가 없이 그림 13에 표시 되는 동일한 기능을 제공 하는 두 개의 웹 컨트롤에 포함 됩니다.

합니다 [LoginView 컨트롤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginview.aspx) 를 쉽게 인증 및 익명 사용자에 게 다양 한 데이터를 표시할 수 있도록 하는 템플릿 기반 웹 컨트롤입니다. LoginView 두 개의 미리 정의 된 템플릿이 포함 되어 있습니다.

- AnonymousTemplate-이 템플릿에 추가할 태그는 익명 방문자에 게 표시 됩니다.
- LoggedInTemplate-인증 된 사용자만이 템플릿의 태그가 나와 있습니다.

사이트의 마스터 페이지, Site.master LoginView 컨트롤을 추가 해 보겠습니다. 방금 LoginView 컨트롤을 추가 하는 대신 하지만 모두 새 ContentPlaceHolder 컨트롤을 추가 해 보겠습니다 및 그런 다음 해당 새 ContentPlaceHolder 내 LoginView 컨트롤을 배치 합니다. 이 의사 결정에 대 한 근거를 곧 명백한 될 것입니다.

> [!NOTE]
> AnonymousTemplate 및 LoggedInTemplate 외에 LoginView 컨트롤에는 역할 관련 템플릿을 포함할 수 있습니다. 지정된 된 역할에 속하는 사용자에만 태그를 표시 하는 역할 관련 템플릿. 이후 자습서에서 LoginView 컨트롤의 역할 기반 기능을 검토해 보겠습니다.


탐색 내에서 마스터 페이지에 LoginContent 라는 ContentPlaceHolder를 추가 하 여 시작 &lt;div&gt; 요소입니다. 도구 상자에서 원본 뷰를 배치 된 TODO 바로 위에 결과 태그는 각각의 ContentPlaceHolder 컨트롤로 드래그 하기만 해도: 메뉴 여기 텍스트 이동 됩니다.

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample8.aspx)]

다음으로, LoginContent ContentPlaceHolder 내의 LoginView 컨트롤을 추가 합니다. 마스터 페이지의 ContentPlaceHolder 컨트롤로 배치 하는 콘텐츠를 사용 하는 것으로 간주 *콘텐츠를 기본* 의 ContentPlaceHolder에 대 한 합니다. 즉,이 마스터 페이지를 사용 하는 ASP.NET 페이지에 대 한 각 ContentPlaceHolder 자신의 콘텐츠를 지정 하거나 마스터 페이지의 기본 콘텐츠를 사용할 수 있습니다.

LoginView 및 다른 로그인 관련 컨트롤을 도구 상자 로그인 탭에 있습니다.


[![도구 상자에서 LoginView 컨트롤](an-overview-of-forms-authentication-vb/_static/image41.png)](an-overview-of-forms-authentication-vb/_static/image40.png)

**그림 14**: 도구 상자에는 LoginView 컨트롤 ([큰 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image42.png))


다음으로 두 개의 추가 &lt;b r /&gt; LoginView 컨트롤 직후 하지만 ContentPlaceHolder 안에서 요소입니다. 이 시점에서 탐색 &lt;div&gt; 요소의 태그는 다음과 같습니다.

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample9.aspx)]

LoginView의 템플릿 디자이너 또는 선언적 태그에서 정의할 수 있습니다. Visual Studio의 디자이너에서 구성 된 템플릿 드롭다운 목록에서 나열 하는 LoginView의 스마트 태그를 확장 합니다. AnonymousTemplate;에 낯선 Hello, 텍스트 입력 다음으로, 하이퍼링크 컨트롤을 추가 하 고 로그에 텍스트 및 NavigateUrl 속성을 설정 하 고 ~ / Login.aspx, 각각.

AnonymousTemplate를 구성한 후의 LoggedInTemplate 전환한 텍스트, "다시 시작,"를 입력 합니다. 그런 다음 "시작 다시" 텍스트 직후 배치를 LoggedInTemplate에 도구 상자에서 LoginName 컨트롤을 끕니다. 합니다 [LoginName 컨트롤과](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginname.aspx)의미 이름으로, 현재 로그인된 한 사용자의 이름을 표시 합니다. 내부적으로 LoginName 컨트롤과 출력 User.Identity.Name 속성

LoginView의 템플릿에 대 한 이러한 추가 마치면 태그는 다음과 비슷하게 표시 됩니다.

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample10.aspx)]

이 또한 Site.master 마스터 페이지를 사용 하 여 웹 사이트의 각 페이지에는 사용자가 인증 되는지 여부에 따라 다른 메시지가 표시 됩니다. 그림 15에서는 브라우저를 통해 사용자 Jisun 방문한 경우 Default.aspx 페이지를 보여 줍니다. 다시 시작, Jisun 메시지가 두 번 반복 됩니다. (방금 추가한 LoginView 컨트롤)를 통해 왼쪽의 마스터 페이지의 탐색 섹션에서 한 번 및 Default.aspx의에서 한 번 콘텐츠 패널 컨트롤 및 프로그래밍 논리) (통해 영역.


[![LoginView 컨트롤 시작 표시 백 Jisun 합니다.](an-overview-of-forms-authentication-vb/_static/image44.png)](an-overview-of-forms-authentication-vb/_static/image43.png)

**그림 15**: Jisun 다시 The LoginView 컨트롤 표시 시작 합니다. ([클릭 하 여 큰 이미지 보기](an-overview-of-forms-authentication-vb/_static/image45.png))


LoginView 마스터 페이지를 추가 했으므로 사이트에서 모든 페이지에 나타날 수 있습니다. 그러나 있을 수 있습니다 웹 페이지는이 메시지를 표시 하려고 하지 않습니다. 이러한 한 페이지의 로그인 페이지 이므로 알려 있는 것 같습니다. 로그인 페이지에 대 한 링크입니다. 때문에 마스터 페이지에 ContentPlaceHolder LoginView 컨트롤을 배치 했습니다 보면 콘텐츠 페이지에서이 기본 태그를 재정의할 수 있습니다. Login.aspx 열고 디자이너로 이동 합니다. 콘텐츠 컨트롤을 명시적으로 정의 하지 않은 것 이므로 LoginContent ContentPlaceHolder를 마스터 페이지에서에 대 한 Login.aspx에서 로그인 페이지에는 표시 마스터 페이지의 기본 태그이 ContentPlaceHolder이에 대 한 합니다. 볼 수 있습니다이 디자이너를 통해 LoginContent ContentPlaceHolder 기본 태그 (LoginView 컨트롤)를 보여 줍니다.


[![로그인 페이지의 기본 콘텐츠가 표시 LoginContent ContentPlaceHolder 마스터 페이지에 대 한](an-overview-of-forms-authentication-vb/_static/image47.png)](an-overview-of-forms-authentication-vb/_static/image46.png)

**그림 16**: 마스터 페이지의 LoginContent ContentPlaceHolder에 대 한 로그인 페이지는 기본 콘텐츠 ([큰 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image48.png))


LoginContent ContentPlaceHolder에 대 한 기본 태그가 재정의 하려면 디자이너의 영역을 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 사용자 지정 콘텐츠 만들기 옵션을 선택 합니다. (Visual Studio 2008의 ContentPlaceHolder를 사용 하 여 포함 된 경우 스마트 태그를 선택 하면 동일한 옵션을 제공 합니다.) 이 추가 페이지의 태그 하 여 새 콘텐츠 컨트롤을이 페이지에 대 한 사용자 지정 콘텐츠를 정의할 수 있습니다. 여기에서 사용자 지정 메시지에서는 하세요 로그와 같은 추가 하지만 보겠습니다만 비워 둘 수 있습니다.

> [!NOTE]
> Visual Studio 2005에서 빈을 만들고 사용자 지정 콘텐츠 만들기 컨트롤은 ASP.NET 페이지의 콘텐츠입니다. 그러나 Visual Studio 2008에서는 사용자 지정 콘텐츠 만들기 복사 마스터 페이지의 기본 콘텐츠 새로 만든된 콘텐츠 컨트롤입니다. Visual Studio 2008을 사용 하는 경우 이렇게 하면 새 콘텐츠 컨트롤 만들기 확인 한 후 마스터 페이지에서 복사 된 내용을 취소 합니다.


그림 17에는 이렇게 변경한 후 브라우저에서 방문할 때 Login.aspx 페이지를 보여 줍니다. Hello, 전혀 모르는 사람 또는 다시 시작 있다는 점에 주의 *사용자 이름* 왼쪽된 탐색 창에서 메시지 &lt;div&gt; Default.aspx를 방문할 때 그대로입니다.


[![로그인 페이지 기본 LoginContent ContentPlaceHolder 태그를 숨깁니다.](an-overview-of-forms-authentication-vb/_static/image50.png)](an-overview-of-forms-authentication-vb/_static/image49.png)

**그림 17**: 로그인 페이지 기본 LoginContent ContentPlaceHolder의 태그를 숨깁니다 ([큰 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image51.png))


## <a name="step-5-logging-out"></a>5 단계: 로그 아웃

3 단계에서에서 사이트에 사용자를 로그인 하는 로그인 페이지를 빌드할 살펴보았습니다 있지만 사용자를 로그 아웃 하는 방법은 아직 있습니다. 사용자를 로그인 하기 위한 방법 이외에 FormsAuthentication 클래스도 제공 된 [SignOut 메서드](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx)합니다. 로그 아웃 메서드는 단순히 함으로써 사이트에서 사용자를 로그인 폼 인증 티켓을 제거 합니다.

로그 아웃 링크는 이러한 일반적인 기능을 제공 하는 ASP.NET 사용자를 로그 아웃 하도록 특별히 설계 된 컨트롤을 포함 합니다. 합니다 [LoginStatus 컨트롤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginstatus.aspx) 로그인 LinkButton 또는 사용자의 인증 상태에 따라 로그 아웃 LinkButton을 표시 합니다. 로그 아웃 LinkButton 인증 된 사용자에 게 표시 되는 반면 익명 사용자에 대 한 로그인 LinkButton 렌더링 됩니다. LoginStatus의 로그인 및 로그 아웃 Linkbutton 텍스트를 구성할 수 있습니다 LoginText 및 LogoutText 속성입니다.

로그인 페이지 리디렉션이 실행 되어, 포스트백을 발생 시키는 로그인 LinkButton을 클릭 합니다. 로그 아웃 LinkButton 클릭 FormsAuthentication.SignOff 메서드를 호출 하는 LoginStatus 컨트롤 시키고 페이지로 사용자를 리디렉션합니다. 로그인된 페이지 사용자 해제 리디렉션됩니다 LogoutAction 속성을 다음 세 값 중 하나에 할당할 수에 따라 달라 집니다.

- 새로 고침-기본값이 며 사용자를 방문 페이지로 리디렉션합니다. FormsAuthenticationModule은 자동으로 다음 방금 방문 페이지 익명 사용자를 허용 하지 않는 경우 사용자를 로그인 페이지로 리디렉션하십시오.

여기 리디렉션이 수행 되는 이유에 대해 관심이 있을 수 있습니다. 사용자가 같은 페이지에 유지 하려는 경우 이유 명시적 리디렉션 필요? 로그 오프 LinkButton 클릭 하면 사용자 계속에 폼 인증 티켓을 해당 쿠키 컬렉션 이므로 이유. 결과적으로 포스트백 요청이 인증 된 요청이입니다. 로그 아웃 메서드를 호출 하는 LoginStatus 컨트롤 이지만 formsauthenticationmodule은 사용자가 인증 후에 발생 하는 합니다. 따라서는 명시적 리디렉션 브라우저 페이지를 다시 요청 하면 됩니다. 브라우저 페이지를 다시 요청 시간, 폼 인증 티켓을 제거 되 고 따라서 들어오는 요청은 익명입니다.

- 리디렉션-사용자는 LoginStatus LogoutPageUrl 속성에서 지정한 URL로 리디렉션됩니다.
- RedirectToLoginPage-사용자가 로그인 페이지로 리디렉션됩니다.

마스터 페이지 LoginStatus 컨트롤을 추가 하 고 서명 된 확인 메시지를 표시 하는 페이지에 사용자를 보낼 리디렉션 옵션을 사용 하도록 구성 해 보겠습니다. Logout.aspx 라는 루트 디렉터리에 페이지를 만들어 시작 합니다. 이 페이지 Site.master 마스터 페이지와 연결할 두는 것을 잊지 마세요. 다음으로, out 기록 된 사용자에 게 설명 하는 페이지의 태그에는 메시지를 입력 합니다.

다음으로, Site.master 마스터 페이지로 돌아가서을 LoginContent ContentPlaceHolder LoginView 아래 LoginStatus 컨트롤을 추가 합니다. ~/Logout.aspx로 리디렉션 LoginStatus 컨트롤의 LogoutAction 속성 및 해당 LogoutPageUrl 속성을 설정 합니다.

[!code-aspx[Main](an-overview-of-forms-authentication-vb/samples/sample11.aspx)]

LoginStatus LoginView 컨트롤 외부 이므로 익명 및 인증 된 사용자에 게 표시 됩니다 됐 네요 확인 LoginStatus 로그인 또는 로그 아웃 LinkButton을 올바르게 표시 됩니다. LoginStatus 컨트롤을 추가 하 여는 AnonymousTemplate의 로그에서 하이퍼링크는 불필요 하므로를 제거 합니다.

그림 18 Jisun 방문 하면 Default.aspx를 보여 줍니다. 왼쪽된 열에 메시지가 표시 됩니다, 그리고 로그 아웃 하는 링크와 함께 Jisun 다시 시작 합니다. 로그 아웃 LinkButton 클릭 하면 포스트백을 발생 시키는, 시스템에서 Jisun 서명 하 고 Logout.aspx 만듭니다 리디렉션합니다. 그림 19와 같이 Jisun Logout.aspx 도달 시간을 기준으로 자신이 이미 로그 아웃 되었습니다 이므로 익명입니다. 따라서 왼쪽된 열 텍스트 시작을 이상 해지고 및 로그인 페이지에 링크를 보여 줍니다.


[![Default.aspx는 Jisun 로그 아웃 LinkButton 함께 다시 시작을 보여 줍니다.](an-overview-of-forms-authentication-vb/_static/image53.png)](an-overview-of-forms-authentication-vb/_static/image52.png)

**그림 18**: Default.aspx 표시 진화, 로그 아웃 LinkButton과 Jisun 함께 ([큰 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image54.png))


[![Logout.aspx 표시 시작 로그인 LinkButton 함께 stranger](an-overview-of-forms-authentication-vb/_static/image56.png)](an-overview-of-forms-authentication-vb/_static/image55.png)

**그림 19**: Logout.aspx 표시 시작 로그인 LinkButton 함께 당신 ([큰 이미지를 보려면 클릭](an-overview-of-forms-authentication-vb/_static/image57.png))


> [!NOTE]
> 것이 좋습니다 (예: Login.aspx 4 단계에서에서 수행한) 마스터 페이지의 LoginContent ContentPlaceHolder를 숨기려면 Logout.aspx 페이지 사용자 지정 합니다. 로그인 LinkButton LoginStatus 컨트롤에서 렌더링 때문에 (Hello, 아래에 있는 한 stranger) 현재 URL ReturnUrl 쿼리 문자열 매개 변수 전달 로그인 페이지로 사용자를 보냅니다. 간단히 말해가 로그 아웃 한 사용자가 로그인 한 다음이 LoginStatus 로그인 LinkButton을 클릭 하 고 하는 경우 리디렉션됩니다 쉽게 사용자 혼동을 줄 수 있는 Logout.aspx 돌아갑니다.


## <a name="summary"></a>요약

이 자습서에서는 forms 인증 워크플로에 대 한 검사를 사용 하 여 시작 켜 졌다가 다음 ASP.NET 응용 프로그램에서 폼 인증을 구현 하는 데 있습니다. 폼 인증의 두 가지 책임이 있는 FormsAuthenticationModule로 전원이: 해당 폼 인증 티켓을 기반으로 사용자를 식별 하 고 권한이 없는 사용자가 로그인 페이지로 리디렉션.

.NET Framework의 FormsAuthentication 클래스 만들기, 검사 및 폼 인증 티켓을 제거 하기 위한 메서드를 포함 합니다. Request.IsAuthenticated 속성 및 사용자 개체는 사용자의 id에 대 한 정보와 요청이 인증 되는지 여부를 결정 하는 것에 대 한 추가 프로그래밍 방식 지원을 제공 합니다. 많은 일반적인 로그인 관련 작업을 수행 하는 것에 대 한 개발자가 신속 하 고 코드 없는 방식으로 제공 하는 LoginView, LoginStatus, LoginName 웹 컨트롤을도 있습니다. 이후 자습서 및 다른 로그인 관련 웹 컨트롤을 더 자세히 검토할 것입니다.

이 자습서에는 폼 인증의 대략적인 개요를 제공 합니다. 에서는 또는 되지 않은 다양 한 구성 옵션을 검토, 어떻게 쿠키 없는 폼 인증 티켓 작업 확인 ASP.NET 폼 인증 티켓의 콘텐츠를 보호 하는 방법을 탐색 합니다. 이러한 항목과에서 자세히 설명 합니다 [다음 자습서](forms-authentication-configuration-and-advanced-topics-vb.md)합니다.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [IIS6 사이의 IIS7 보안 변경 내용](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/Changes-between-IIS6-and-IIS7-Security)
- [ASP.NET 로그인 컨트롤](https://msdn.microsoft.com/library/d51ttbhx.aspx)
- [Professional ASP.NET 2.0 보안, 멤버 자격 및 역할 관리](http://www.wrox.com/WileyCDA/WroxTitle/productCd-0764596985.html) (ISBN: 978-0-7645-9698-8)
- [합니다 &lt;인증&gt; 요소](https://msdn.microsoft.com/library/532aee0e.aspx)
- [합니다 &lt;forms&gt; 요소에 대 한 &lt;인증&gt;](https://msdn.microsoft.com/library/1d3t3c61.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>이 자습서에 포함 된 항목의 비디오 교육

- [ASP.NET에서 기본 폼 인증 사용](../../../videos/authentication/using-basic-forms-authentication-in-aspnet.md)

### <a name="about-the-author"></a>저자 소개

Scott Mitchell, 여러 ASP/ASP.NET 책의 저자 이자 4GuysFromRolla.com의 설립자 이며 1998 Microsoft 웹 기술을 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는  *[Sams 설명 직접 ASP.NET 2.0 24 시간 동안의](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 합니다. Scott에 도달할 수 있습니다 [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) 통하거나 저자의 블로그 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Alicja Maziarz, John Suru 및 Teresa Murphy 포함 됩니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com)합니다.

> [!div class="step-by-step"]
> [이전](security-basics-and-asp-net-support-vb.md)
> [다음](forms-authentication-configuration-and-advanced-topics-vb.md)
