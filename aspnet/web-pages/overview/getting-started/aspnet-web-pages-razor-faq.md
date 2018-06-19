---
uid: web-pages/overview/getting-started/aspnet-web-pages-razor-faq
title: ASP.NET 웹 페이지 (Razor) FAQ | Microsoft Docs
author: tfitzmac
description: 이 문서에서는 WebMatrix 및 ASP.NET 웹 페이지 (Razor)에 대 한 몇 가지 질문과 대답을 나열 합니다. 에 자습서 ASP.NET 웹 페이지 (오른쪽...를 사용 하는 소프트웨어 버전
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/07/2014
ms.topic: article
ms.assetid: b137bd04-25e1-47cb-9d96-ef2e179ecf1f
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/aspnet-web-pages-razor-faq
msc.type: authoredcontent
ms.openlocfilehash: 60cc4ca364923cb131d5e91cd7b6307b1e68644b
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
ms.locfileid: "28042461"
---
<a name="aspnet-web-pages-razor-faq"></a>ASP.NET 웹 페이지 (Razor) FAQ
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> > [!NOTE] 
> > WebMatrix 더 이상 권장 통합된 개발 환경에 대 한 ASP.NET 웹 페이지입니다. 사용 하 여 [Visual Studio](xref:aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio) 또는 [Visual Studio Code](https://code.visualstudio.com/)합니다.
>
> 이 문서에서는 WebMatrix 및 ASP.NET 웹 페이지 (Razor)에 대 한 몇 가지 질문과 대답을 나열 합니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 3
> - Visual Studio 2013
> - WebMatrix 3
>   
> 
> 이 자습서에서는 ASP.NET 웹 페이지 2, 2 WebMatrix 및 Visual Studio 2012 에서도 작동합니다.


- [ASP.NET 웹 페이지, ASP.NET Web Forms 및 ASP.NET MVC의 차이 무엇입니까?](#Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC)
- [WebMatrix 웹 페이지를 사용 하려면 필요 합니까?](#Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages)
- [웹 페이지의 페이지에서 ASP.NET Web Forms 컨트롤을 사용할 수 있습니까?](#Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page)
- [WebMatrix를 사용 하지 않고 ASP.NET 웹 페이지 사이트를 배포할 수 있습니까?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)
- [로그인을 지원 하기 위해 WebSecurity 도우미를 사용 해야 합니까?](#Do_I_have_to_use_the_WebSecurity_helper_to_support_logins)
- [ASP.NET 웹 페이지 HTML5 지원 합니까?](#Does_ASP.NET_Web_Pages_support_HTML5)
- [JavaScript 및 jQuery 웹 페이지를 사용할 수 있습니까?](#Can_I_use_JavaScript_and_jQuery_with_Web_Pages)
- [추가 리소스](#AdditionalResources)

오류 및 기타 문제에 대 한 질문에 대 한 참조는 [ASP.NET 웹 페이지 (Razor) 문제 해결 가이드](https://go.microsoft.com/fwlink/?LinkId=253001)합니다.

<a id="Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC"></a>
## <a name="whats-the-difference-between-aspnet-web-pages-aspnet-web-forms-and-aspnet-mvc"></a>ASP.NET 웹 페이지, ASP.NET Web Forms 및 ASP.NET MVC의 차이 무엇입니까?

세 개는 모두 동적 웹 응용 프로그램을 만들기 위한 ASP.NET 기술:

- ASP.NET 웹 페이지는 동적 (서버 쪽) 코드 및 데이터베이스 액세스 기능 간단 하 고 간단한 구문 및 HTML 페이지를 추가 하는 방법에 중점을 둡니다.
- ASP.NET Web Forms 페이지 개체 모델 및 기존 창 형식 컨트롤 (예: 단추, 목록)에 기반 합니다. Web Forms 클라이언트 기반 (Windows forms) 개발와 협력 하 여 사용자에 게 친숙 하는 이벤트 기반 모델을 사용 합니다.
- ASP.NET MVC는 ASP.NET에 대 한 모델-뷰-컨트롤러 패턴을 구현합니다. "문제의 분리" 강조 됩니다 (처리, 데이터 및 UI 레이어).

모든 세 가지 프레임 워크 완벽 하 게 지원 하 고 계속 ASP.NET 팀에서 개발 됩니다. 배경에 따라 사용 하는 프레임 워크 선택 되는 일반적으로 ASP.NET 경험 합니다.

특히 ASP.NET 웹 페이지를 쉽게 서버 처리 된 페이지를 추가 하는 HTML을 이미 알고 있는 사용자를 위해 설계 되었습니다. 학생, 취미, 프로그래밍을 처음 인 일반적 사용자에 대 한 것이 좋은 대안입니다. 비 ASP.NET 웹 기술 사용 경험을가지고 있는 개발자를 위한 적합 한 선택은 될 수도 있습니다.

<a id="Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages"></a>
## <a name="do-i-need-webmatrix-in-order-to-work-with-web-pages"></a>WebMatrix 웹 페이지를 사용 하려면 필요 합니까?

아니요. WebMatrix 더 이상 권장 통합된 개발 환경에 대 한 ASP.NET 웹 페이지입니다. 사용 하 여 [Visual Studio](program-asp-net-web-pages-in-visual-studio.md) 또는 [Visual Studio Code](https://code.visualstudio.com/)합니다.

Visual Studio 또는 Visual Studio 코드를 사용 하지 않음 경우 개별적으로 사용 하 여 구성 요소 제품을 설치할 수 있습니다 [Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)합니다. 다음 제품이 필요합니다.

- Microsoft .NET Framework 4.5
- ASP.NET MVC 5 (을 ASP.NET 웹 페이지 프레임 워크에도 설치)
- IIS Express (웹 서버)
- Microsoft SQL Server Compact 4.0 (데이터베이스)

텍스트 편집기를 사용 하 여 편집할 *.cshtml* (또는 *.vbhtml*) 페이지.

SQL Server Compact 데이터베이스를 관리 (*.sdf* 파일) 없이 도구는 다소 어렵습니다. 관리 하기 위한 visual Studio containds 도구 *.sdf* 데이터베이스. 또한 다양 한 SQL Server 관리 작업을 수행 하는 코드에서 SQL 명령을 실행할 수 있습니다.

테스트 하려면 *.cshtml* 통합된 개발 환경 (IDE)를 사용 하지 않고 페이지를 배포할 수 있습니다는 활성 서버에 있습니다. (참조 [WebMatrix를 사용 하지 않고 ASP.NET 웹 페이지 사이트를 배포할 수 있습니까?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix))

### <a name="running-iis-express-without-using-an-ide"></a>IIS Express를 실행 하는 IDE를 사용 하지 않고

웹 서버 컴퓨터에 IIS Express를 설치 하는 경우 페이지를 테스트 하는 사용할 수 있습니다. 명령줄에서 IIS Express를 실행 하 고 특정 포트 번호와 연결 수입니다. 요청 하는 경우 다음 해당 포트를 지정 *.cshtml* 브라우저의 파일입니다.

Windows에서 관리자 권한으로 명령 프롬프트를 열고를 바꾸려면 *C:\Program Files\IIS Express입니다.* (64 비트 시스템에 대 한 폴더를 사용 하 여 *C:\Program Files (x86) \IIS Express.)* 그런 다음 사이트에 실제 경로 사용 하 여 다음 명령을 입력 합니다.

`iisexpress.exe /port:35896 /path:C:\BasicWebSite`

다른 프로세스에서 이미 예약 되어 있지 않습니다 임의의 포트 번호를 사용할 수 있습니다. (1024 이상의 포트 번호는 일반적으로 무료입니다.) 에 대 한는 `path` 값, 웹 사이트 폴더의 경로 사용 하 여 여기서는 *.cshtml* 파일은 합니다.

IIS Express 페이지를 사용 하도록 설정 하려면이 명령을 실행 한 후 브라우저를 열고 하 수를 찾습니다는 *.cshtml* 파일입니다. 다음과 같은 URL을 사용 합니다.

`http://localhost:35896/default.cshtml`

에 대 한 도움말 IIS Express 명령줄 옵션을 입력 `iisexpress.exe /?` 명령줄에서.

<a id="Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page"></a>
## <a name="can-i-use-aspnet-web-forms-controls-on-a-web-pages-page"></a>웹 페이지의 페이지에서 ASP.NET Web Forms 컨트롤을 사용할 수 있습니까?

아니요. Web Forms 컨트롤 같은 [확인란](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox) 컨트롤의 [유효성 검사 컨트롤](https://msdn.microsoft.com/library/bwd43d0x), 및 [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview) 만 작동 하 여 Web Forms 페이지에서 (*.aspx* 파일). 이러한 컨트롤에는 Web Forms 페이지 프레임 워크가 필요합니다.

<a id="Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix"></a>
## <a name="can-i-deploy-an-aspnet-web-pages-site-without-using-webmatrix"></a>WebMatrix를 사용 하지 않고 ASP.NET 웹 페이지 사이트를 배포할 수 있습니까?

예. (일반적으로 사용 하 여 FTP) 서버에 웹 사이트 파일을 수동으로 복사할 수 있습니다. 수동 복사를 수행 하는 경우를 지 원하는 SQL Server Compact (데이터베이스) 파일을 복사할 수도 있습니다. 자세한 내용은 블로그 항목을 참조 [도구는 웹 페이지 배포 응용 프로그램](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317)합니다.

<a id="Do_I_have_to_use_the_WebSecurity_helper_to_support_logins"></a>
## <a name="do-i-have-to-use-the-websecurity-helper-to-support-logins"></a>로그인을 지원 하기 위해 WebSecurity 도우미를 사용 해야 합니까?

아니요. `SimpleMembership` 공급자 일부인 ASP.NET 웹 페이지의 옵션 중 하나입니다. (하는 ASP.NET Web Forms에서 사용 하는 데 사용 될 수 있습니다)의 일부인 보안 공급자를 사용할 수 있습니다. 예를 들어 사용할 수 있습니다 폼 인증 ASP.NET 웹 페이지에서 Web Forms에서와 마찬가지로. 폼 인증을 사용 하는 방법의 한 가지 예, Microsoft 지원 문서 참조 [How To Implement Forms-Based 인증을 사용 하 여 C#.NET에서 ASP.NET 응용 프로그램에](https://support.microsoft.com/kb/301240)합니다. 간단한 예제를 다운로드 하려면 [ASP.NET 버전의 "로그인 &amp; 암호](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm)합니다.

Windows 인증을 사용 하는 방법에 대 한 내용은 블로그 게시물을 참조 하십시오. [ASP.NET 웹 페이지에서 사용 하 여 Windows 인증](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298)합니다.

<a id="Does_ASP.NET_Web_Pages_support_HTML5"></a>
## <a name="does-aspnet-web-pages-support-html5"></a>ASP.NET 웹 페이지 HTML5 지원 합니까?

예. ASP.NET 웹 페이지를 만들 페이지 (*.cshtml* 또는 *.vbhtml* 페이지)는 기본적으로 페이지를 렌더링 하기 전에 서버에서 실행 되는 코드가 포함 된 HTML 페이지입니다. 사용자의 브라우저에서 HTML5 지원, HTML5 요소에 사용할 수 있습니다는 *.cshtml* 또는 *.vbhtml* 페이지.

<a id="Can_I_use_JavaScript_and_jQuery_with_Web_Pages"></a>
## <a name="can-i-use-javascript-and-jquery-with-web-pages"></a>JavaScript 및 jQuery 웹 페이지를 사용할 수 있습니까?

물론입니다! ASP.NET 웹 페이지를 만들 페이지 (*.cshtml* 또는 *.vbhtml* 페이지)에 서버 코드와 HTML 페이지만 됩니다. 따라서 JavaScript 또는 jQuery를 사용 하 여 일반 HTML 페이지에서 수행할 수 있는 모든 항목 또한에서 수행할 수 있습니다는 *.cshtml* 또는 *.vbhtml* 페이지.

**시작 사이트** WebMatrix에서 템플릿에 여러 가지 jQuery 라이브러리를 포함 합니다. 해당 서식 파일을 사용 하 여 사이트를 만들 경우는 *스크립트* jQuery 핵심 라이브러리를 포함 하는 폴더 (*jquery 1.6.2.js)* 및 jQuery 유효성 검사에 대 한 라이브러리 (*jquery.validate.js*등.).

다음은 jQuery ASP.NET 웹 페이지를 사용 하는 방법을 보여 주는 몇 가지 블로그 게시물입니다.

- [ASP.NET 웹 페이지에 WebMatrix를 사용 하 여 jQuery도 추가](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/) Rachel Appel 하 여
- [5 분: WebMatrix + jQuery UI + json + jQuery 템플릿](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/) Jonas Eriksson 하 여
- [WebMatrix 및 jQuery Forms](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms) Mike Brind 하 여

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>추가 리소스


[ASP.NET 웹 페이지(Razor) 문제 해결 가이드](https://go.microsoft.com/fwlink/?LinkId=253001)

[WebMatrix 및 ASP.NET 웹 페이지 포럼](https://forums.asp.net/1224.aspx/1?WebMatrix) ASP.NET 웹 사이트에서
