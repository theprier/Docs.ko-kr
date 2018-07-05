---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: ASP.NET 및 Visual Studio 2012 용 웹 도구 2013.1 릴리스 정보 | Microsoft Docs
author: microsoft
description: 이 문서에서는 Visual Studio 2012 용 ASP.NET 및 웹 도구 2013.1 릴리스를 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/13/2013
ms.topic: article
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
ms.technology: ''
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 85cd45c25e0f2ad3c8d6d6de73a1a493533e7f7b
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37374262"
---
<a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>ASP.NET 및 Visual Studio 2012 용 웹 도구 2013.1 릴리스 정보
====================
[Microsoft](https://github.com/microsoft)

> 이 문서에서는 Visual Studio 2012 용 ASP.NET 및 웹 도구 2013.1 릴리스를 설명 합니다.


## <a name="contents"></a>목차

- [설치 참고 사항](#install)
- [소프트웨어 요구 사항](#requirements)
- ASP.NET 및 Visual Studio 2012 용 웹 도구 2013.1의 새로운 기능

    - [부트스트랩](#bootstrap)
    - [템플릿](#templates)

        - [ASP.NET MVC 5 템플릿에서](#mvc5template)
        - [ASP.NET Web API 2 템플릿](#apitemplate)
        - [항목 템플릿](#itemtemplate)
    - [Entity Framework 6](#ef6)
    - [ASP.NET 스 캐 폴딩](#scaffold)
    - [Razor 편집기](#razor)
    - [NuGet 2.7](#nuget)
- 알려진된 문제 및 주요 변경 내용

    - [ASP.NET 스 캐 폴딩](#issuescaffolding)

        - [MVC 및 Web API 스 캐 폴딩-HTTP 404 찾을 수 없음 오류](#404issue)
        - [Visual Studio Express 2012 for Web 스 캐 폴드 된 항목을 추가한 후 작동이 중지 됩니다.](#expressissue)
    - [ASP.NET Razor 3](#issuerazor)

        - [서버 오류가 발생 하는 브라우저 또는 f5 키를 사용 하 여 cshtml 파일 보기](#browseissue)
        - [Url 재작성 및 Tilde(~)](#rewriteissue)
    - [템플릿](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a>설치 참고 사항

[설치](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET 및 웹 도구 2013.1 Visual Studio 2012 용입니다.

<a id="requirements"></a>
## <a name="software-requirements"></a>소프트웨어 요구 사항

Visual Studio 2012 또는 Visual Studio Express 2012 for Web 있어야 합니다.

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>ASP.NET 및 Visual Studio 2012 용 웹 도구 2013.1의 새로운 기능

<a id="bootstrap"></a>
### <a name="bootstrap"></a>부트스트랩

보기에 대 한 태그를 사용 하 여 MVC 5 컨트롤러와 뷰 스 캐 폴드 하는 경우 [부트스트랩](http://getbootstrap.com/)합니다.

<a id="templates"></a>
### <a name="templates"></a>템플릿

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a>ASP.NET MVC 5 템플릿에서

새 MVC 5 템플릿을 추가 했습니다. 최신 MVC 5 NuGet 패키지 참조 및 스 캐 폴딩 컨트롤러 및 뷰를 추가 하는 데 사용할 수 있습니다.

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a>ASP.NET Web API 2 템플릿

새 Web API 2 템플릿을 추가 했습니다. 최신 웹 API 2 NuGet 패키지 참조 및 스 캐 폴딩 컨트롤러 및 뷰를 추가 하는 데 사용할 수 있습니다.

<a id="itemtemplate"></a>
#### <a name="item-templates"></a>항목 템플릿

MVC 5 뷰, 웹 페이지 (Razor 3) 및 Web API 2 컨트롤러에 대 한 새 항목 템플릿을 추가 했습니다. 새 항목을 추가 하는 동안 프로젝트에 관련 된 NuGet 패키지를 설치 합니다.

<a id="ef6"></a>
### <a name="entity-framework-6"></a>Entity Framework 6

Entity Framework를 사용 하 여 MVC 또는 Web API 컨트롤러를 스 캐 폴딩 하면 Framework 6을 사용 했습니다. Entity Framework에 대 한 자세한 내용은 참조는 [Entity Framework 버전 기록이](https://msdn.com/data/jj574253)합니다.

또한 다운로드 하 고 Visual Studio 2012에 대 한 Entity Framework 6 도구를 설치할 수 있습니다. 참조 된 [Entity Framework 가져오기](https://msdn.com/data/ee712906#tooling)합니다.

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET 스 캐 폴딩

ASP.NET 스 캐 폴딩은 ASP.NET 웹 응용 프로그램에 대 한 코드 생성 프레임 워크. 쉽게 데이터 모델과 상호 작용 하는 프로젝트에 상용구 코드를 추가 합니다.

이전 버전의 Visual Studio에서 스 캐 폴딩 ASP.NET MVC 프로젝트에 있었습니다. 이 업데이트를 Web Forms를 비롯 한 모든 ASP.NET 프로젝트에 대 한 스 캐 폴딩을 이제 사용할 수 있습니다. 이 업데이트를 Web Forms 프로젝트에 대 한 생성 페이지를 지원 하지 않습니다 하지만 프로젝트에 MVC 종속성을 추가 하 여 Web forms 스 캐 폴딩을 계속 사용할 수 있습니다. Web Forms에 대 한 페이지를 생성 하는 것에 대 한 지원이 향후 업데이트에서 추가 됩니다.

스 캐 폴딩을 사용 하는 경우 프로젝트의 종속성이 설치 되어 필요한 모든 것을 확인 합니다. 예를 들어, ASP.NET Web Forms 프로젝트를 시작 하 고 다음 스 캐 폴딩을 사용 하 여 Web API 컨트롤러를 추가할 경우 필요한 NuGet 패키지와 참조를 프로젝트에 자동으로 추가 됩니다.

MVC 스 캐 폴딩에 Web Forms 프로젝트를 추가 하려면 추가 된 **새 스 캐 폴드 된 항목** 선택한 **MVC 5 종속성** 대화 상자에서. 두 가지 옵션이 있습니다; MVC 스 캐 폴딩에 대 한 최소 및 전체. 최소를 선택 하면 프로젝트에 NuGet 패키지 및 ASP.NET MVC에 대 한 참조만 추가 됩니다. 전체 옵션을 선택 하는 경우 MVC 프로젝트에 필요한 콘텐츠 파일 뿐만 아니라 최소한의 종속성에 추가 합니다.

Entity Framework 6에서 새 비동기 기능을 사용 하는 비동기 컨트롤러 스 캐 폴딩에 대 한 지원.

자세한 내용 및 자습서를 참조 하세요 [ASP.NET 스 캐 폴딩 개요](../2013/aspnet-scaffolding-overview.md)합니다. 이러한 자습서에는 Visual Studio 2013을 사용 하 여 스 캐 폴딩을 보여 줍니다. 하지만 ASP.NET 및 Visual Studio 2012 용 웹 도구 2013.1에 적용 됩니다.

<a id="razor"></a>
### <a name="razor-editor"></a>Razor 편집기

이 업데이트를 사용 하 여 Visual Studio 2012는 이제 Razor 3 도구/편집 합니다.

<a id="nuget"></a>
### <a name="nuget-27"></a>NuGet 2.7

NuGet 2.7에 자세히 설명 하는 새로운 기능의 다양 한 집합을 포함 [NuGet 2.7 릴리스 정보](http://docs.nuget.org/docs/release-notes/nuget-2.7)합니다.

이 버전의 NuGet이 누락 된 패키지를 복원 하려면 NuGet을 명시적으로 허용 하는 사용자에 대 한 필요성을 제거 합니다. NuGet 2.7의 경우 사용자를 암시적으로 설치 하는 경우 자동으로 누락 된 패키지를 복원에 동의 합니다. 사용자는 Visual Studio에서 NuGet 설정을 통해 패키지 복원에서 명시적으로 선택할 수 있습니다. 이 변경은 패키지 복원의 작동 원리를 간소화 합니다.

## <a name="known-issues-and-breaking-changes"></a>알려진된 문제 및 주요 변경 내용

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET 스 캐 폴딩

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC 및 Web API 스 캐 폴딩-HTTP 404 찾을 수 없음 오류

프로젝트에 스 캐 폴드 된 항목을 추가할 때 오류가 발생 하면 경우 프로젝트가 일관성 없는 상태로 남게 됩니다. 변경 내용 스 캐 폴딩 수 중 일부를 롤백할 수 있지만 설치 된 NuGet 패키지와 같은 다른 변경 내용을 다시 롤백할 수 됩니다. 라우팅 구성 변경 내용이 롤백되어도 경우 스 캐 폴드 항목으로 이동 하는 경우 사용자는 HTTP 404 오류를 받게 됩니다.

MVC에 대 한이 오류를 해결 하려면 새 스 캐 폴드 된 항목을 추가 하 고 MVC 5 종속성 선택 (최소 또는 전체). 이 프로세스에서 필요한 변경의 모든 프로젝트에 추가 합니다.

웹 API에 대 한이 오류를 수정 합니다.

1. 프로젝트에 다음 WebApiConfig 클래스를 추가 합니다.

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. 응용 프로그램에서 WebApiConfig.Register 구성\_Global.asax에서 다음과 같은 메서드를 시작 합니다.

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a>Visual Studio Express 2012 for Web 스 캐 폴드 된 항목을 추가한 후 작동이 중지 됩니다.

Visual Studio Express 2012 for Web (예: Web API 2 컨트롤러 작업을 사용 하 여 Entity Framework를 사용 하 여) Entity Framework와 함께 스 캐 폴드 된 항목을 추가한 후 작동을 멈출 경우는 어셈블리의 네이티브 이미지를 로드 하지 못했습니다 Visual Studio Express System.Web.Extensions에 따라 달라 집니다.

이 문제를 해결 하려면 Visual Studio Express System.Web.Extensions MSIL 이미지와 함께 작동 하도록을 구성 합니다.

1. 관리자 모드에서 명령 프롬프트를 엽니다.
2. %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE 또는 (64 비트 Windows)에 대 한 %Programfiles(x86)% %\Microsoft Visual Studio 11.0\Common7\IDE로 이동 합니다.
3. VWDExpress.exe.config 텍스트 편집기에서 엽니다.
4. 아래에 다음 줄을 추가 합니다 &lt;configuration&gt;/&lt;런타임&gt; 요소:  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. 다시 Visual Studio Express 2012 for Web.

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a>ASP.NET Razor 3

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-withbrowse-withorf5causes-a-server-error"></a>Cshtml 파일 withBrowse WithorF5causes 서버 오류 보기

-없다는 오류가 표시는 Visual Studio 2012 (또는 Visual Studio 2013에서 만든 Visual Studio 2012는 MVC 5 프로젝트에서 열기)에서 MVC 5 프로젝트 만들기를 cshtml 파일을 사용 하 여 찾아보기 또는 f5 키를 사용 하 여 보려고 **에서 서버 오류 '/' 응용 프로그램**합니다. 서버를 탐색 하려고 합니다. `http://localhost:XXXX/Views/../XXXX.cshtml`

이 문제를 해결 하려면 변경 된 **시작 작업** 하기 위해 프로젝트에서 설정 **특정 페이지**합니다. 페이지에 대 한 값을 제공할 필요가 없습니다.

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

이렇게 변경한 후 f5 키를 선택 하면 이동할 응용 프로그램의 루트 (`http://localhost:XXXX`). 이 동작은 다릅니다 Visual Studio 2013에서 MVC 5 프로젝트에 대 한 동작으로 위치를 **현재 페이지** 설정 페이지 열기를 시작 합니다.

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a>Url 재작성 및 Tilde(~)

ASP.NET Razor 3 또는 ASP.NET MVC 5로 업그레이드 한 후 tilde(~) 표기법을 사용할 수 없습니다 올바르게 URL 재작성을 사용 하는 경우. URL 다시 쓰기에 영향을 줍니다 tilde(~) 표기법에서 HTML 요소와 같은 &lt;A /&gt;, &lt;스크립트 /&gt;, &lt;링크 /&gt;, 물결표 루트 디렉터리에 더 이상 매핑됩니다 결과적으로 합니다.

예를 들어에 대 한 요청을 다시 작성할 때 **asp.net/content** 하 **asp.net**, href 특성에 &lt;a "~/content/" = /&gt; 확인 **/content/ 콘텐츠 /** of **/** 합니다. 이 변경 하지 않으려면 설정할 수 있습니다 합니다 **IIS\_WasUrlRewritten** 각 웹 페이지 또는 false로 상황에 맞는 **응용 프로그램\_BeginRequest** Global.asax의 합니다.

<a id="templateissue"></a>
### <a name="templates"></a>템플릿

만들 때 ASP.NET MVC 프로젝트 Windows 8.1 또는 Windows Server 2012 R2, Visual Studio에서 Visual Studio 2012를 사용 하 여 구성 봚 [url] asp.net 4.5가 실패 했습니다. "를 나타내는 오류 메시지가 표시 됩니다.

![구성 오류](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

해당 릴리스의 Windows에서 설치 될 때 Visual Studio 2012에 ASP.NET 4.5 기능을 활성화 하지 때문에이 오류가 표시 됩니다. ASP.NET 4.5를 사용 하도록 설정 하려면에 설명 된 단계를 수행 [설정할 Windows 기능 사용 /](https://windows.microsoft.com/windows-8/turn-windows-features-on-off)합니다.

![Windows 기능 설정](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

또는 명령줄을 통해 ASP.NET 4.5를 사용할 수 있습니다.

1. 관리자 모드에서 명령 프롬프트를 엽니다.
2. ASP.NET 4.5를 사용 하도록 설정 하려면 다음 명령을 실행 합니다.  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
