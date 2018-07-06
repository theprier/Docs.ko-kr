---
uid: web-pages/overview/getting-started/aspnet-web-pages-razor-faq
title: ASP.NET 웹 페이지 (Razor) FAQ | Microsoft Docs
author: tfitzmac
description: 이 문서에서는 ASP.NET Web Pages (Razor) 및 WebMatrix에 대 한 몇 가지 질문과 대답을 나열합니다. 소프트웨어 버전을 사용 하는 자습서 ASP.NET 웹 페이지에서 (R...
ms.author: aspnetcontent
ms.date: 02/07/2014
ms.assetid: b137bd04-25e1-47cb-9d96-ef2e179ecf1f
msc.legacyurl: /web-pages/overview/getting-started/aspnet-web-pages-razor-faq
msc.type: authoredcontent
ms.openlocfilehash: 1f97056c952757ea2d009eaca57d904791e80ca3
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37814238"
---
<a name="aspnet-web-pages-razor-faq"></a>ASP.NET 웹 페이지 (Razor) FAQ
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> > [!NOTE] 
> > WebMatrix는 더 이상 권장 통합된 개발 환경으로 ASP.NET 웹 페이지에 대 한 합니다. 사용 하 여 [Visual Studio](xref:aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio) 하거나 [Visual Studio Code](https://code.visualstudio.com/)합니다.
>
> 이 문서에서는 ASP.NET Web Pages (Razor) 및 WebMatrix에 대 한 몇 가지 질문과 대답을 나열합니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET Web Pages (Razor) 3
> - Visual Studio 2013
> - WebMatrix 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2, WebMatrix 2 및 Visual Studio 2012 에서도 작동합니다.


- [ASP.NET 웹 페이지, ASP.NET Web Forms 및 ASP.NET MVC의 차이 무엇입니까?](#Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC)
- [WebMatrix 웹 페이지를 사용 하기 위해 필요 합니까?](#Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages)
- [ASP.NET Web Forms 페이지의 컨트롤을 웹 페이지를 사용할 수 있나요?](#Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page)
- [WebMatrix를 사용 하지 않고 ASP.NET 웹 페이지 사이트를 배포할 수 있습니까?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)
- [로그인을 지원 하기 위해 WebSecurity 도우미를 사용 해야 합니까?](#Do_I_have_to_use_the_WebSecurity_helper_to_support_logins)
- [ASP.NET 웹 페이지에 HTML5 지원 하나요?](#Does_ASP.NET_Web_Pages_support_HTML5)
- [JavaScript 및 jQuery 웹 페이지를 사용 하 여 사용할 수 있나요?](#Can_I_use_JavaScript_and_jQuery_with_Web_Pages)
- [추가 리소스](#AdditionalResources)

오류 및 기타 문제에 대 한 질문에 대 한 참조를 [ASP.NET Web Pages (Razor) 문제 해결 가이드](https://go.microsoft.com/fwlink/?LinkId=253001)합니다.

<a id="Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC"></a>
## <a name="whats-the-difference-between-aspnet-web-pages-aspnet-web-forms-and-aspnet-mvc"></a>ASP.NET 웹 페이지, ASP.NET Web Forms 및 ASP.NET MVC의 차이 무엇입니까?

세 가지 모두 동적 웹 응용 프로그램을 만들기 위한 ASP.NET 기술을 같습니다.

- ASP.NET 웹 페이지에 HTML 페이지 및 기능 간단 하 고 간단한 구문 동적 (서버 쪽) 코드 및 데이터베이스 액세스 추가에 중점을 둡니다.
- ASP.NET Web Forms는 페이지 개체 모델 및 기존 창 형식 컨트롤 (예: 단추, 목록)을 기반으로 합니다. Web Forms (Windows forms) 클라이언트 기반 개발 작업을 했었다면 모든 사람에 게 익숙한 이벤트 기반 모델을 사용 합니다.
- ASP.NET MVC는 ASP.NET에 대 한 모델-뷰-컨트롤러 패턴을 구현 합니다. 중요 한 점은 "문제의 분리"에 (처리, 데이터 및 UI 레이어).

모든 세 가지 프레임 워크는 완전히 지원 되며 계속 ASP.NET 팀에서 개발 됩니다. 배경에 따라 사용 하는 프레임 워크의 선택 되는 일반적으로 ASP.NET을 사용 하 여 발생 합니다.

특히 ASP.NET 웹 페이지를 쉽게 서버 처리 해당 페이지를 추가 하는 HTML을 이미 알고 있는 사람들을 위해 설계 되었습니다. 학생, 취미 개발자, 처음으로 프로그래밍 인 일반적 사용자에 대 한 적합 한 것입니다. 비 ASP.NET 웹 기술 사용 하 여 경험이 있는 개발자를 위한 좋은 선택 일 수도 있습니다.

<a id="Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages"></a>
## <a name="do-i-need-webmatrix-in-order-to-work-with-web-pages"></a>WebMatrix 웹 페이지를 사용 하기 위해 필요 합니까?

아니요. WebMatrix는 더 이상 권장 통합된 개발 환경으로 ASP.NET 웹 페이지에 대 한 합니다. 사용 하 여 [Visual Studio](program-asp-net-web-pages-in-visual-studio.md) 하거나 [Visual Studio Code](https://code.visualstudio.com/)합니다.

Visual Studio 또는 Visual Studio Code를 사용 하지 않으려는 경우에 개별적으로 사용 하 여 구성 요소 제품을 설치할 수 있습니다 [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)합니다. 다음 제품이 필요합니다.

- Microsoft .NET Framework 4.5
- ASP.NET MVC 5 (설치 하는 ASP.NET Web Pages 프레임 워크에도)
- IIS Express (웹 서버)
- Microsoft SQL Server Compact 4.0 (데이터베이스)

텍스트 편집기를 사용 하 여 편집할 *.cshtml* (또는 *.vbhtml*) 페이지.

SQL Server Compact 데이터베이스 관리 (*.sdf* 파일) 없이 도구는 다소 어렵습니다. 관리에 대 한 visual studio containds *.sdf* 데이터베이스입니다. 또한 다양 한 SQL Server 관리 작업을 수행 하는 코드에서 SQL 명령을 실행할 수 있습니다.

테스트할 *.cshtml* 통합된 개발 환경 (IDE)를 사용 하지 않고 페이지를 배포할 수 있습니다 라이브 서버. (참조 [WebMatrix를 사용 하지 않고는 ASP.NET Web Pages 사이트를 배포할 수 있습니까?](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix))

### <a name="running-iis-express-without-using-an-ide"></a>IIS Express를 실행 하는 IDE를 사용 하지 않고

웹 서버 컴퓨터에서 IIS Express를 설치 하는 경우 페이지를 테스트 하는 사용할 수 있습니다. 명령줄에서 IIS Express를 실행 하 고 특정 포트 번호를 사용 하 여 연결할 수 있습니다. 요청 하는 경우 다음 포트를 지정 *.cshtml* 브라우저에서 파일입니다.

Windows에서 관리자 권한으로 명령 프롬프트를 열고 및 변경 *C:\Program Files\IIS Express입니다.* (64 비트 시스템에 대 한 폴더를 사용 하 여 *C:\Program Files (x86) \IIS Express.)* 다음 사이트의 실제 경로 사용 하 여 다음 명령을 입력:

`iisexpress.exe /port:35896 /path:C:\BasicWebSite`

다른 프로세스에 의해 이미 예약 되지 않는 어떤 포트 번호도 사용할 수 있습니다. (1024 위의 포트 번호는 일반적으로 무료입니다.) 에 대 한 합니다 `path` 값, 웹 사이트 폴더의 경로 사용 하 여 위치를 *.cshtml* 파일이 합니다.

이 명령은 IIS Express 페이지를 사용 하도록 설정 하려면를 실행 한 후에 브라우저를 열고 고를 찾아볼 수 있습니다는 *.cshtml* 파일입니다. 다음과 같은 URL을 사용 합니다.

`http://localhost:35896/default.cshtml`

IIS Express 명령줄 옵션을 사용 하 여 도움말에 대 한 입력 `iisexpress.exe /?` 명령줄에서.

<a id="Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page"></a>
## <a name="can-i-use-aspnet-web-forms-controls-on-a-web-pages-page"></a>ASP.NET Web Forms 페이지의 컨트롤을 웹 페이지를 사용할 수 있나요?

아니요. Web Forms 컨트롤 같은 합니다 [확인란을 선택](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox) 컨트롤을 [유효성 검사 컨트롤](https://msdn.microsoft.com/library/bwd43d0x), 및 [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview) Web Forms 페이지에만 작동을 제어 (*.aspx* 파일). 이러한 컨트롤에는 Web Forms 페이지 프레임 워크가 필요합니다.

<a id="Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix"></a>
## <a name="can-i-deploy-an-aspnet-web-pages-site-without-using-webmatrix"></a>WebMatrix를 사용 하지 않고 ASP.NET 웹 페이지 사이트를 배포할 수 있습니까?

예. (일반적으로 사용 하 여 FTP) 서버에 웹 사이트 파일을 수동으로 복사할 수 있습니다. 수동 복사를 수행 하는 경우에 또한 SQL Server Compact (데이터베이스) 지 원하는 파일을 복사 해야 합니다. 자세한 내용은 블로그 항목을 참조 하세요 [웹 페이지 배포 응용 프로그램 도구 없이](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317)합니다.

<a id="Do_I_have_to_use_the_WebSecurity_helper_to_support_logins"></a>
## <a name="do-i-have-to-use-the-websecurity-helper-to-support-logins"></a>로그인을 지원 하기 위해 WebSecurity 도우미를 사용 해야 합니까?

아니요. `SimpleMembership` ASP.NET 웹 페이지에 포함 된 공급자 옵션 중 하나입니다. (하는 ASP.NET Web Forms에서 사용 하는 데 사용 될 수 있습니다)의 일부인 보안 공급자를 사용할 수 있습니다. 예를 들어 사용할 수 있습니다 폼 인증 ASP.NET 웹 페이지에서 Web Forms에서와 마찬가지로. 폼 인증을 사용 하는 방법의 예로, Microsoft 지원 문서 참조 [를 사용 하 여 C#.NET에서 ASP.NET 응용 프로그램에서 How To Implement Forms-Based 인증](https://support.microsoft.com/kb/301240)합니다. 간단한 예제를 다운로드 하려면 [ASP.NET 버전의 "로그인 &amp; 암호](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm)합니다.

Windows 인증을 사용 하는 방법에 대 한 자세한 내용은 블로그 게시물을 참조 하세요 [를 사용 하 여 Windows 인증 ASP.NET 웹 페이지에서](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298)합니다.

<a id="Does_ASP.NET_Web_Pages_support_HTML5"></a>
## <a name="does-aspnet-web-pages-support-html5"></a>ASP.NET 웹 페이지에 HTML5 지원 하나요?

예. ASP.NET 웹 페이지를 사용 하 여 만든 페이지 (*.cshtml* 하거나 *.vbhtml* 페이지)는 기본적으로 페이지를 렌더링 하기 전에 서버에서 실행 되는 코드를 포함 하는 HTML 페이지입니다. 사용자의 브라우저에서 HTML5를 지 원하는으로에서 HTML5 요소를 사용할 수 있습니다는 *.cshtml* 하거나 *.vbhtml* 페이지입니다.

<a id="Can_I_use_JavaScript_and_jQuery_with_Web_Pages"></a>
## <a name="can-i-use-javascript-and-jquery-with-web-pages"></a>JavaScript 및 jQuery 웹 페이지를 사용 하 여 사용할 수 있나요?

물론입니다! ASP.NET 웹 페이지를 사용 하 여 만든 페이지 (*.cshtml* 또는 *.vbhtml* 페이지)에서 서버 코드를 사용 하 여 HTML 페이지 뿐입니다. 따라서 모든 JavaScript 또는 jQuery를 사용 하 여 일반 HTML 페이지에서 수행할 수 있습니다 에서도 수행할 수는 *.cshtml* 하거나 *.vbhtml* 페이지입니다.

합니다 **시작 사이트** WebMatrix에서 템플릿에 jQuery 라이브러리의 수입니다. 해당 템플릿을 사용 하 여 사이트를 만든 경우 합니다 *스크립트* 폴더에는 jQuery core 라이브러리가 포함 되어 (*jquery 1.6.2.js)* 및 jQuery 유효성 검사에 대 한 라이브러리 (*jquery.validate.js*등.).

ASP.NET 웹 페이지를 사용 하 여 jQuery를 사용 하는 방법을 보여 주는 몇 가지 블로그 게시물 보기는 다음과 같습니다.

- [JQuery의 유용한 기능을 ASP.NET 웹 페이지 추가 WebMatrix를 사용 하 여](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/) 여 Rachel Appel
- [5 분: WebMatrix의 jQuery UI + json + jQuery 템플릿](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/) Jonas Eriksson 여
- [WebMatrix 및 jQuery Forms](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms) Mike Brind 여

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>추가 리소스


[ASP.NET 웹 페이지(Razor) 문제 해결 가이드](https://go.microsoft.com/fwlink/?LinkId=253001)

[WebMatrix 및 ASP.NET Web Pages 포럼](https://forums.asp.net/1224.aspx/1?WebMatrix) ASP.NET 웹 사이트
