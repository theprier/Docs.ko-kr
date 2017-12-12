---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: "ASP.NET 및 Visual Studio 2012 용 2013.1 웹 도구 릴리스 정보 | Microsoft Docs"
author: microsoft
description: "이 문서에서는 Visual Studio 2012 용 ASP.NET 및 웹 도구 2013.1의 릴리스를 설명 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/13/2013
ms.topic: article
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 1e4ee8eb4901305bf6a8c9c5b949dc4ee10290e5
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>ASP.NET 및 Visual Studio 2012 용 웹 도구 2013.1에 대 한 릴리스 정보
====================
여 [Microsoft](https://github.com/microsoft)

> 이 문서에서는 Visual Studio 2012 용 ASP.NET 및 웹 도구 2013.1의 릴리스를 설명 합니다.


## <a name="contents"></a>목차

- [설치 참고 사항](#install)
- [소프트웨어 요구 사항](#requirements)
- ASP.NET 및 Web Tools 2013.1 for Visual Studio 2012의 새로운 기능

    - [부트스트랩](#bootstrap)
    - [템플릿](#templates)

        - [ASP.NET MVC 5 서식 파일](#mvc5template)
        - [ASP.NET Web API 2 템플릿](#apitemplate)
        - [항목 템플릿](#itemtemplate)
    - [Entity Framework 6](#ef6)
    - [ASP.NET 스 캐 폴딩](#scaffold)
    - [Razor 편집기](#razor)
    - [NuGet 2.7](#nuget)
- 알려진된 문제 및 주요 변경 내용

    - [ASP.NET 스 캐 폴딩](#issuescaffolding)

        - [MVC 및 Web API 스 캐 폴딩-HTTP 404 찾을 수 없음 오류](#404issue)
        - [스 캐 폴드 된 항목을 추가한 후 작업을 중지 하는 visual Studio Express 2012 for Web](#expressissue)
    - [ASP.NET Razor 3](#issuerazor)

        - [서버 오류 발생 시키는 cshtml 파일 브라우저 또는 f5 키 보기](#browseissue)
        - [Url 재작성 및 Tilde(~)](#rewriteissue)
    - [템플릿](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a>설치 참고 사항

[설치](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET 및 웹 도구 2013.1 Visual Studio 2012 용입니다.

<a id="requirements"></a>
## <a name="software-requirements"></a>소프트웨어 요구 사항

Visual Studio 2012 또는 Visual Studio Express 2012 for Web 있어야 합니다.

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>ASP.NET 및 Web Tools 2013.1 for Visual Studio 2012의 새로운 기능

<a id="bootstrap"></a>
### <a name="bootstrap"></a>부트스트랩

보기에 대 한 태그를 사용 하 여 MVC 5 컨트롤러와 뷰 스 캐 폴드 할 때 [부트스트랩](http://getbootstrap.com/)합니다.

<a id="templates"></a>
### <a name="templates"></a>템플릿

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a>ASP.NET MVC 5 서식 파일

새 MVC 5 템플릿을 추가 했습니다. 최신 MVC 5 NuGet 패키지를 참조 하 고 컨트롤러와 뷰를 추가 하려면 스 캐 폴딩을 사용할 수 있습니다.

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a>ASP.NET Web API 2 템플릿

새 Web API 2 서식 파일을 추가 했습니다. 최신 웹 API 2 NuGet 패키지를 참조 하 고 스 캐 폴딩 컨트롤러와 뷰를 추가 하려면 사용할 수 있습니다.

<a id="itemtemplate"></a>
#### <a name="item-templates"></a>항목 템플릿

MVC 5 뷰, 웹 페이지 (Razor 3), 및 Web API 2 컨트롤러에 대 한 새 항목 템플릿 추가 했습니다. 새 항목을 추가 하는 동안 관련된 NuGet 패키지는 프로젝트에 설치할 합니다.

<a id="ef6"></a>
### <a name="entity-framework-6"></a>Entity Framework 6

Entity Framework를 사용 하 여 MVC 또는 Web API 컨트롤러를 스 캐 폴드 할 때 프레임 워크 6 사용 합니다. Entity Framework에 대 한 자세한 내용은 참조는 [Entity Framework 버전 기록이](https://msdn.com/data/jj574253)합니다.

또한 다운로드 하 고 Visual Studio 2012에 대 한 Entity Framework 6 도구를 설치할 수 있습니다. 참조는 [Entity Framework 가져오기](https://msdn.com/data/ee712906#tooling)합니다.

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET 스 캐 폴딩

ASP.NET 스 캐 폴딩 ASP.NET 웹 응용 프로그램에 대 한 코드 생성 프레임 워크입니다. 쉽게 데이터 모델과 상호 작용 하는 프로젝트에 상용구 코드를 추가 합니다.

이전 버전의 Visual Studio를 스 캐 폴딩 ASP.NET MVC 프로젝트에 있었습니다. 이 업데이트를 Web Forms를 포함 하 여 모든 ASP.NET 프로젝트에 대 한 스 캐 폴딩 이제 사용할 수 있습니다. 이 업데이트는 Web Forms 프로젝트에 대 한 생성 페이지를 지원 하지 않습니다 되지만 프로젝트에 MVC 종속성을 추가 하 여 스 캐 폴딩 Web Forms를 계속 사용할 수 있습니다. Web forms 페이지를 생성 하는 것에 대 한 지원이 향후 업데이트에서 추가 됩니다.

스 캐 폴딩을 사용할 때 필요한 모든 프로젝트에 종속성이 설치 되어을 확인 합니다. 예를 들어, ASP.NET Web Forms 프로젝트와 함께 시작 하 고 다음 스 캐 폴딩을 사용 하 여 웹 API 컨트롤러를 추가 하려면 필요한 NuGet 패키지와 참조를 프로젝트에 자동으로 추가 됩니다.

MVC 스 캐 폴딩 Web Forms 프로젝트를 추가 하려면 추가 **스 캐 폴드 된 새 항목** 선택 **MVC 5 종속성** 대화 상자 창에서. MVC; 스 캐 폴딩에 대 한 다음과 같은 최소이 고 전체. 최소을 선택 하면 NuGet 패키지와 ASP.NET MVC에 대 한 참조가 프로젝트에 추가 됩니다. 전체 옵션을 선택 하는 경우 MVC 프로젝트에 필요한 콘텐츠 파일 뿐만 아니라 최소한의 종속성 추가 됩니다.

비동기 컨트롤러를 스 캐 폴딩에 대 한 지원 Entity Framework 6의 새로운 비동기 기능을 사용 합니다.

자세한 내용과 자습서에 대 한 참조 [ASP.NET 스 캐 폴딩 개요](../2013/aspnet-scaffolding-overview.md)합니다. 이 자습서는 Visual Studio 2013과 함께 스 캐 폴딩 나타나지만 ASP.NET 및 Visual Studio 2012 용 웹 도구 2013.1 적용할 수도 있습니다.

<a id="razor"></a>
### <a name="razor-editor"></a>Razor 편집기

이 업데이트를 Visual Studio 2012 Razor 3 도구/편집 이제 지원합니다.

<a id="nuget"></a>
### <a name="nuget-27"></a>NuGet 2.7

NuGet 2.7에 자세히 설명 하는 새로운 기능의 풍부한 포함 [NuGet 2.7 릴리스 정보](http://docs.nuget.org/docs/release-notes/nuget-2.7)합니다.

이 버전의 NuGet이 누락 된 패키지를 복원 하려면 NuGet을 명시적으로 허용 하려면 사용자에 대 한 필요성을 제거 합니다. NuGet 2.7을 설치할 때 사용자가 암시적으로 자동으로 누락 된 패키지를 복원 하는 데 동의 합니다. 패키지 복원 Visual Studio에서 NuGet 설정을 통해 사용자가 명시적으로 않을 수 있습니다. 이러한 변경 패키지 복원 작동 하는 방법을 간소화 합니다.

## <a name="known-issues-and-breaking-changes"></a>알려진된 문제 및 주요 변경 내용

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET 스 캐 폴딩

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC 및 Web API 스 캐 폴딩-HTTP 404 찾을 수 없음 오류

프로젝트에 스 캐 폴드 된 항목을 추가할 때 오류가 발생 하면 있기 프로젝트 일관성 없는 상태로 유지 됩니다. 스 캐 폴딩 수 변경 중 일부는 롤백할 수 있지만 설치 된 NuGet 패키지와 같은 다른 변경 내용을 다시 롤백되며 되지 않습니다. 라우팅 구성 변경 내용이 롤백되어도 경우 스 캐 폴드 항목으로 이동 하는 경우 사용자가 HTTP 404 오류를 받습니다.

MVC에 대 한이 오류를 해결 하려면 새 스 캐 폴드 항목을 추가 하 고 MVC 5 종속성 선택 (최소 또는 전체). 이 프로세스의 모든 필요한 변경 사항을 프로젝트에 추가 합니다.

웹 API에 대 한이 오류를 해결 하려면:

1. 프로젝트에 다음과 같은 경우 WebApiConfig 클래스를 추가 합니다.

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. 응용 프로그램에서 WebApiConfig.Register 구성\_Global.asax에 다음과 같이 메서드를 시작 합니다.

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a>스 캐 폴드 된 항목을 추가한 후 작업을 중지 하는 visual Studio Express 2012 for Web

(예: Web API 2 컨트롤러와 동작을 Entity Framework를 사용 하 여) Entity Framework와 함께 스 캐 폴드 항목을 추가한 후에 작동을 중지 하는 Visual Studio Express 2012 for Web,이 경우 Visual Studio Express 되지 못한 어셈블리의 네이티브 이미지를 로드 합니다. System.Web.Extensions에 의존 합니다.

이 문제를 해결 하려면 Visual Studio Express System.Web.Extensions의 MSIL 이미지와 함께 작동 하도록을 구성 합니다.

1. 관리자 모드에서 명령 프롬프트를 엽니다.
2. %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE 또는 (64 비트 Windows) 용 %ProgramFiles(x86) %\Microsoft Visual Studio 11.0\Common7\IDE 이동 합니다.
3. VWDExpress.exe.config 텍스트 편집기에서 엽니다.
4. 아래에 다음 줄 추가 &lt;구성&gt;/&lt;런타임&gt; 요소:  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. 다시 Visual Studio Express 2012 for Web입니다.

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a>ASP.NET Razor 3

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-withbrowse-withorf5causes-a-server-error"></a>서버 오류 cshtml 파일 withBrowse WithorF5causes 보기

Visual Studio 2012 (또는 Visual Studio 2012 MVC 5 만든 프로젝트를 Visual Studio 2013에서에서 열기)에서 MVC 5 프로젝트를 만들 cshtml 파일 브라우저 또는 f5 키를 사용 하 여 보려고 하는 경우 오류 메시지가 결과로-받습니다 **에서 서버 오류 '/' 응용 프로그램**합니다. 서버를 탐색 하려고 합니다.`http://localhost:XXXX/Views/../XXXX.cshtml`

이 문제를 해결 하려면 변경 된 **시작 작업** 프로젝트에서 설정 **특정 페이지**합니다. 페이지에 대 한 값을 제공할 필요가 없습니다.

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

응용 프로그램의 루트에이 변경 후 f5 키를 선택 하면 탐색 (`http://localhost:XXXX`). 이 동작은 Visual Studio 2013에서 MVC 5 프로젝트에 대 한 동작와 동일 하 게 되지 않습니다 여기서는 **현재 페이지** 설정 페이지 열기를 시작 합니다.

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a>Url 재작성 및 Tilde(~)

ASP.NET Razor 3 또는 ASP.NET MVC 5로 업그레이드 한 후 tilde(~) 표기법 없습니다 더 이상 제대로 작동 URL 다시 작성을 사용 하는 경우. URL 다시 쓰기에 영향을 줍니다 tilde(~) 표기법에서 HTML 요소와 같은 &lt;A /&gt;, &lt;스크립트 /&gt;, &lt;링크 /&gt;, 결과적으로 물결표 더 이상 매핑되는 루트 디렉터리입니다.

예를 들어에 대 한 요청을 다시 작성할 때 **asp.net/content** 를 **asp.net**에 href 특성이 &lt;A href = "~/content/" /&gt; 확인 **/content/ 콘텐츠 /** 대신  **/** 합니다. 이 변경은 표시 하지 않으려면 설정할 수 있습니다는 **IIS\_WasUrlRewritten** 각 웹 페이지 또는 false로 컨텍스트 **응용 프로그램\_BeginRequest** Global.asax에 있습니다.

<a id="templateissue"></a>
### <a name="templates"></a>템플릿

만들 때 ASP.NET MVC 프로젝트 Windows 8.1 또는 Windows Server 2012 R2, Visual Studio에서 Visual Studio 2012를 사용한 "구성 웹 [url] asp.net 4.5 실패 했습니다."를 설명 하는 오류 메시지가 표시 됩니다.

![구성 오류](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

해당 버전의 Windows에 설치 된 경우 Visual Studio 2012 ASP.NET 4.5 기능을 사용 하지 않는 때문에이 오류가 표시 됩니다. ASP.NET 4.5를 사용 하도록 설정 하려면에 설명 된 단계를 수행 [Windows 기능 설정 또는 해제](https://windows.microsoft.com/en-us/windows-8/turn-windows-features-on-off)합니다.

![Windows 기능 설정](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

또는 명령줄을 통해 ASP.NET 4.5를 활성화할 수 있습니다.

1. 관리자 모드에서 명령 프롬프트를 엽니다.
2. ASP.NET 4.5를 사용 하도록 설정 하려면 다음 명령을 실행 합니다.  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
