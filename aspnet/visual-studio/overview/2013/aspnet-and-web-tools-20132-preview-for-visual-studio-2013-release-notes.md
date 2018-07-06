---
uid: visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
title: ASP.NET 및 Web Tools 2013.2 for Visual Studio 2013 릴리스 정보 | Microsoft Docs
author: microsoft
description: ''
ms.author: aspnetcontent
ms.date: 03/06/2014
ms.assetid: 7ef5f73c-ca60-43c1-bdb2-702800347e7e
msc.legacyurl: /visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
msc.type: authoredcontent
ms.openlocfilehash: fb36d9f469265be60a7e40ed7e317d8da6560bf9
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37824499"
---
<a name="aspnet-and-web-tools-20132--for-visual-studio-2013-release-notes"></a>ASP.NET 및 Web Tools 2013.2 for Visual Studio 2013 릴리스 정보
====================
[Microsoft](https://github.com/microsoft)

## <a name="installation-notes"></a>설치 참고 사항

ASP.NET 및 Web Tools for Visual Studio 2013.2 기본 설치 관리자에서 번들로 제공 되 고의 일부로 다운로드할 수 있습니다 [Visual Studio 2013 업데이트 2](https://go.microsoft.com/fwlink/?LinkId=390521)합니다.

## <a name="documentation"></a>설명서

자습서 및 Visual Studio 2013.2에 대 한 ASP.NET 및 Web Tools에 대 한 다른 정보에서 사용할 수는 [ASP.NET 웹 사이트](https://www.asp.net/)합니다.

## <a name="software-requirements"></a>소프트웨어 요구 사항

ASP.NET 및 Web Tools for Visual Studio 2013.2 Visual Studio 2013이 필요 합니다.

## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-20132"></a>ASP.NET 및 Web Tools for Visual Studio 2013.2의 새로운 기능

다음 섹션에서는 릴리스에서 도입 된 기능을 설명 합니다.

- [ASP.NET 프로젝트 템플릿](#oneaspnet)
- [IIS Express에서 웹 응용 프로그램을 시작 하는 경우 SSL을 지원 합니다.](#ssl)
- [Visual Studio 웹 편집기 향상 기능](#vswebeditor)
- [브라우저 링크](#browserlink)
- [Visual Studio에서 Azure App Service Web Apps에 대 한 지원](#waws)
- [새 웹 프로젝트를 만들 때 원격 Azure 리소스 만들기](#AzureResources)
- [향상 된 기능으로 웹 게시](#webpublish)
- [ASP.NET 스 캐 폴딩](#scaffolding)
- [NuGet 2.8.1](#nuget)
- [ASP.NET Web Forms](#webforms)
- [ASP.NET MVC 5.1.2](#mvc)
- [ASP.NET Web API 2.1.2](#webapi)
- [ASP.NET Web Pages 3.1.2](#webpages)
- [Entity Framework 6.1](#ef)
- [ASP.NET Id 2.0.0](#identity)
- [Microsoft OWIN 구성 요소](#owin)
- [ASP.NET SignalR 2.0.2](#signalr)

<a id="oneaspnet"></a>
### <a name="one-aspnet-project-templates"></a>ASP.NET 프로젝트 템플릿

- 계정 확인 및 암호 재설정을 지원 하도록 ASP.NET 프로젝트 템플릿 업데이트 합니다.
- 온-프레미스 조직 계정을 사용 하 여 인증을 지원 하도록 ASP.NET Web API 템플릿을 업데이트 합니다.
- 이제 ASP.NET SPA 템플릿 MVC 및 서버 쪽 뷰를 기반으로 하는 인증을 포함 합니다. 템플릿을 인증 된 사용자만 액세스할 수 있는 WebAPI 컨트롤러를 있습니다.

<a id="ssl"></a>
### <a name="support-ssl-when-launching-web-applications-on-iis-express"></a>IIS Express에서 웹 응용 프로그램을 시작 하는 경우 SSL을 지원 합니다.

검색 및 로컬 호스트에서 HTTPS를 디버깅 하는 경우 보안 경고를 제거 하려면 Internet Explorer 및 Chrome 신뢰 자체 서명 된 IIS express SSL 인증서를 허용 하는 대화 상자를 추가 했습니다.

예를 들어, SSL을 사용 하도록 웹 프로젝트 속성을 설정할 수 있습니다. 속성 대화 상자를 표시 하려면 F4를 클릭 합니다. 변경 **SSL 설정** true로 합니다. SSL URL을 복사 합니다.

![SSL 사용 속성](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image1.png)

HTTPS를 사용 하도록 웹 프로젝트 속성 페이지 웹 탭 집합 기반 URL (SSL URL 됩니다 `https://localhost:44300/` SSL 웹 사이트를 이전에 만든 경우가 아니면.)

![프로젝트 URL (HTTPS)를 설정 합니다.](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image2.png)

Ctrl+F5를 눌러 응용 프로그램을 실행합니다. IIS Express에서 생성 하는 자체 서명 된 인증서를 신뢰 하도록 지침을 따릅니다.

![SSL 경고](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image3.png)

읽기를 **보안 경고** 대화 상자 및 클릭 **예** 나타내는 localhost 인증서를 설치 하려는 경우.

![보안 경고](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image4.png)

사이트 IE 또는 크롬에 표시 되는 브라우저에 인증서 경고 없이 합니다.

![경고 없이 HTTPS 페이지](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image5.png)

Firefox에서 경고를 표시 하므로 자체 인증서 저장소를 사용 합니다.

<a id="vswebeditor"></a>
### <a name="visual-studio-web-editor-enhancements"></a>Visual Studio 웹 편집기 향상 기능

- **새 JSON 프로젝트 항목 및 편집기**: JSON 프로젝트 항목 및 편집기를 Visual Studio에 추가 합니다. 현재 JSON 편집기 기능 색 지정, 구문 유효성 검사, 중괄호 완성, 개요, 도구 옵션 설정 등을 포함 합니다.

    ![JSON 편집기](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image6.png)

    IntelliSense에서 지 원하는 [JSON 스키마](http://json-schema.org/) v3 및 v4 합니다. 기존 스키마를 선택 하 여 로컬 스키마 경로 편집을 스키마 콤보 상자 또는 끌어서 놓기 프로젝트 JSON 파일의 상대 경로 가져올 수 있습니다.

    ![JSON Intellisense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image7.png)    ![JSON 스키마 편집기](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image8.png)
- **새 Sass (SCSS) 편집기**: VS2013 RTM에서 작은 추가 했 고 이제 Sass 프로젝트 항목 및 편집기입니다. LESS 편집기에서 비교할 기능과 색 지정, 변수, Mixin IntelliSense 달거나 주석, 요약 정보, 형식 지정, 구문 유효성 검사, 개요, 정의 이동, 색 선택 포함 sass 편집기 옵션 설정 하는 등 도구입니다.

    ![SCSS 스타일 시트를 새 항목을 추가 합니다.](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image9.png)    ![스타일 시트 편집기](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image10.png)
- **새 URL 선택 대화 상자에서 HTML, Razor, CSS, LESS 및 Sass 문서:** VS 2013 Web Forms 페이지 외부 없는 URL 선택 대화 상자를 사용 하 여 제공 합니다. 새 URL 선택기 HTML, Razor, css, LESS 및 Sass 편집기가 이해 하는 대화 무료, fluent 입력 선택 '..' 및 img 태그 및 링크에 대 한 필터 파일을 적절 하 게 나열 합니다.

    ![이미지 태그에 대 한 URL 선택](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image11.png)    ![보기에 대 한 URL 선택](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image12.png)    ![CSS에 대 한 URL 선택](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image13.png)
- **더 많은 기능을 추가 하 여 LESS 편집기에 대 한 업데이트**
- **Knockout Intellisense 업그레이드**: VS intelliSense에 대 한 비표준 KnockOut 구문을 추가 했습니다 "ko vs 편집기 viewModel:" 구문입니다. 형식에서 주석을 사용 하 여 페이지에서 여러 보기 모델에 바인딩할 사용할 수 있습니다.

    ![Knockout Intellisense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image14.png)

    중첩 된 ViewModel IntelliSense에 대 한 지원을 ViewModel에 깊게 중첩 된 개체에 드릴 수 있도록도 추가 했습니다.

    `<div data-bind="text: foo.bar.baz.etc" />`

    표시 IntelilSense JavaScript 개체의 전체 IntelliSense입니다.

    ![Intellisense 보여 주는 전체 JavaScript 개체](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image15.png)
- **새 URL 선택 대화 상자에서 HTML, Razor, CSS, LESS 및 Sass 문서**: VS 2013 Web Forms 페이지 외부 없는 URL 선택 대화 상자를 사용 하 여 제공 합니다. 새 URL 선택기 HTML, Razor, css, LESS 및 Sass 편집기가 이해 하는 대화 무료, fluent 입력 선택 '..' 및 img 태그 및 링크에 대 한 필터 파일을 적절 하 게 나열 합니다.

    ![이미지 태그에 대 한 URL 선택](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image16.png)    ![보기에 대 한 URL 선택](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image17.png)    ![CSS에 대 한 URL 선택](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image18.png)

<a id="browserlink"></a>
### <a name="browser-link"></a>브라우저 링크

- 이제 브라우저 링크는 HTTPS 연결을 지원 하 고 표시 하는 대시보드에서 다른 연결을 사용 하 여 브라우저에서 인증서를 신뢰할 수 있다면 합니다.
- 정적 HTML 소스 매핑
- SPA 매핑 데이터에 대 한 지원
- 매핑 데이터 자동 업데이트 합니다.

<a id="waws"></a>
### <a name="support-for-azure-app-service-web-apps-in-visual-studio"></a>Visual Studio에서 Azure App Service Web Apps에 대 한 지원

- **Azure 지원에 로그인 합니다.**
- **원격 디버깅 및 웹 앱에 대 한 원격 뷰**: 이제 지원 [Azure App Service에서 웹 앱에 대 한 원격 디버깅](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio) 및 서버 탐색기에서 웹 앱 콘텐츠 파일의 원격 보기.

<a id="AzureResources"></a>
### <a name="create-remote-azure-resources-when-creating-a-new-web-project"></a>새 웹 프로젝트를 만들 때 원격 Azure 리소스 만들기

Azure를 추가 했습니다 ["원격 리소스 만들기"](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet) 새 웹 응용 프로그램 대화 상자에서 확인란을 선택 합니다. 를 선택 하 여 새 웹 응용 프로그램 테스트 및 몇 가지 간단한 단계에서 게시 프로필 만들기에 대 한 Azure 게시 사이트 설정의 환경을 통합할 수 있습니다.

![Azure 리소스를 사용 하 여 새 프로젝트](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image19.png)![Azure에 게시](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image20.png)

<a id="webpublish"></a>
### <a name="web-publish-enhancements"></a>향상 된 기능으로 웹 게시

- 게시에 대 한 사용자 환경을 개선 합니다.

<a id="scaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET 스 캐 폴딩

- **열거형 지원:** 모델에 열거형을 사용 하는 경우 MVC 스 캐 폴더 열거형에 대 한 드롭다운을 생성 합니다. MVC에서 열거형 도우미를 사용합니다.
- **지원이 부트스트랩**: 부트스트랩 클래스를 사용 하도록 MVC 스 캐 폴딩의 EditorFor 서식 파일을 업데이트 합니다.
- **지원 패키지**: MVC 및 Web API 스 캐 폴더는 MVC 및 Web API에 대 한 5.1 패키지 추가

다음 스크린샷에서 스 캐 폴딩 모델을 보여 줍니다.

- 코드 모델:

     ![코드 모델](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image21.png)
- 컴파일 모델 코드를 마우스 오른쪽 단추로 **추가**하십시오 **새 스 캐 폴드 된 항목**합니다.

     ![새 스 캐 폴드 된 항목 추가](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image22.png)
- 선택할 **Entity Framework를 사용 하 여 뷰를 사용 하 여 MVC5 컨트롤러**:

     ![뷰를 사용 하 여 새 MVC5 컨트롤러 추가](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image23.png)
- **컨트롤러 추가** 모델을 사용 하 여:

    ![](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image24.png)
- 예를 들어 Views/WeekdayModels/Edit.cshtml 생성 된 코드를 확인 `@Html.EnumDropDownListFor`: ![EnumDropDownListFor 포함 된 보기](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image25.png)
- 값은 null 일 수 있습니다, 빈 문자열 콤보 상자에 선택할 수 있습니다 생성 열거형 콤보 상자 참조에서 페이지를 실행 합니다. 예를 들어 합니다 **만들기** 페이지 다음에 표시 됩니다.

    ![빈 문자열을 허용 하는 콤보 상자](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image26.png)

<a id="nuget"></a>
### <a name="nuget-281"></a>NuGet 2.8.1

NuGet 2.8.1 RTM은 2014 년 4 월 출시 됩니다. 다음 릴리스 정보에서 쟁점은 있지만 하십시오 합니다 [전체 릴리스 정보](http://docs.nuget.org/docs/release-notes/nuget-2.8) 이러한 변경에 대 한 자세한 내용은 합니다.

- **Windows Phone 8.1 응용 프로그램을 대상**: NuGet 2.8.1 이제 Windows Phone 8.1 응용 프로그램 '이 WindowsPhoneApp', 'WPA', 'WindowsPhoneApp81' 및 'WPA81' 대상 프레임 워크 모니커를 사용 하 여 대상으로 지원 합니다.
- **종속성에 대 한 패치 확인**: NuGet 패키지에서 종속성을 충족 하는 가장 낮은 주 및 부 패키지 버전을 선택 하는 전략을 지금까지 구현한 패키지 종속성을 해결 하는 경우. 그러나 주 및 부 버전을 달리 패치 버전을 항상 해결 된 가장 높은 버전으로 합니다. 좋은 의도로 동작 이지만 종속성을 사용 하 여 패키지를 설치 하는 것에 대 한 결정성이 부족을 만들었습니다.
- **DependencyVersion 스위치**: 하지만 NuGet 2.8 변경 합니다 *기본* 종속성 확인에 대 한 동작을 또한 추가 종속성 확인 프로세스에서-DependencyVersion 스위치를 통해 더 정밀 하 게 제어 합니다 패키지 관리자 콘솔입니다. 스위치를 통해 가능한 가장 낮은 버전 (기본 동작), 가능한 최상 버전을 가장 높은 부 또는 패치 버전에 대 한 종속성을 확인할 수 있습니다. 이 스위치는 powershell 명령에서 설치 패키지 에서만 작동합니다.
- **DependencyVersion 특성**:-DependencyVersion 스위치 위에서 자세히 설명 하는 것 외에도 NuGet에도 허용-DependencyVersion 전환 하는 경우 기본값은 무엇을 정의 하는 nuget.config 파일에서 새 특성을 설정 하는 데 필요한 권한 설치 패키지의 호출에서 지정 하지 않았습니다. 이 값이 모든 설치 패키지 작업에 대 한 NuGet 패키지 관리자 대화 상자도 적용 됩니다. 이 값을 설정 하려면 아래 특성 nuget.config 파일에 추가 합니다.

    `<config> <add key="dependencyversion" value="Highest" /> </config>`
- **-Whatif NuGet 사용 하 여 작업을 미리**: 일부 NuGet 패키지에는 전체 종속성 그래프 있을 수 있으며 따라서이 수를 설치 하는 동안 유용할 제거 또는 업데이트 작업을 먼저 발생 하는 결과 볼 수 있습니다. 표준 PowerShell을 추가 하는 NuGet 2.8-명령을 적용 되는 패키지의 완전 한 클로저 시각화를 활성화 하는 패키지 설치, 제거 패키지 및 패키지 업데이트 명령을 어떻게 전환 합니다.
- **패키지를 다운 그레이드**: 새로운 기능을 조사 하기 위해 패키지의 시험판 버전을 설치 하 고 마지막 안정적인 버전으로 롤백하려면 다음 결정 하는 것도 드물지 않습니다. NuGet 2.8 이전에이 시험판 패키지 및 해당 종속성을 제거 하 고 다음 이전 버전을 설치 하는 여러 단계의 프로세스가 이었습니다. 그러나 NuGet 2.8을 사용 하 여 업데이트 패키지를 이제 롤백됩니다 전체 패키지 클로저 (예: 패키지의 종속성 트리) 이전 버전으로 합니다.
- **개발 종속성**: 개발 프로세스를 최적화 하는 데 사용 되는 도구를 포함 하는 NuGet 패키지로-다양 한 기능을 제공할 수 있습니다. 이후이 경우 새 패키지의 종속성 게시 구성이 요소를 새 패키지를 개발 하는 데 도움이 될 수 있지만 이러한 고려 되어야 합니다. NuGet 2.8을 developmentDependency.nuspec 파일에 자신을 식별 하는 패키지를 수 있습니다. 설치 하는 경우에이 메타 데이터는 패키지가 설치 된 프로젝트의 packages.config 파일에 추가 됩니다. Packages.config 파일은 나중에 분석할 NuGet 종속성에 대 한 nuget.exe 팩 중 때 개발 종속성으로 표시 하는 이러한 종속성 제외 됩니다.
- **다양 한 플랫폼에 대 한 개별 packages.config 파일**: 여러 대상 플랫폼에 대 한 응용 프로그램을 개발할 때 각 해당 빌드 환경에 대해 다른 프로젝트 파일을 저장 하는 일반적인 합니다. 패키지에 다양 한 플랫폼에 대 한 지원 수준이 다양 한 대로도 여러 프로젝트 파일에서 다른 NuGet 패키지 사용에 일반적입니다. 다양 한 플랫폼 관련 프로젝트 파일에 대 한 다른 packages.config 파일을 만들어이 시나리오에 대 한 향상 된 지원을 제공 하는 NuGet 2.8 합니다.
- **로컬 캐시에 대체 (fallback)**: 하지만 NuGet 패키지는 일반적으로 사용 된 원격 갤러리에서와 같은 합니다 [NuGet 갤러리](http://www.nuget.org) 는 네트워크 연결을 사용 하 여, 다양 한 시나리오는 클라이언트가 연결 되지 않았습니다. 네트워크 연결 없이 NuGet 클라이언트에서 해당 패키지는 로컬 NuGet 캐시에서 클라이언트 컴퓨터에 이미 있던 경우에-패키지를 설치할 수 없습니다. 2.8 NuGet 패키지 관리자 콘솔에 대체 (fallback) 자동 캐시를 추가합니다.

    캐시 대체 (fallback) 기능에는 특정 명령 인수를 사용할 필요가 없습니다. 또한 대체 (fallback) 캐시는 현재 패키지 관리자 콘솔 에서만에서 작동-동작 패키지 관리자 대화 상자에서 현재 작동 하지 않습니다.
- **버그 수정**: 업데이트 패키지의 성능 향상 된 만든 주요 버그 수정 중-명령을 다시 설치 합니다.

    이 릴리스의 NuGet에는 이러한 기능 및 앞에서 언급 한 성능 문제를 해결 하는 것 외에도 다른 많은 버그 수정도 포함 됩니다. 릴리스에서 해결 181 총 문제가 있었습니다. 작업의 전체 목록은 항목에서에서 수정 된 NuGet 2.8 하세요 보기는 [NuGet 문제 추적기](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all) 이 릴리스에 대 한 합니다.

<a id="webforms"></a>
### <a name="aspnet-web-forms"></a>ASP.NET Web Forms

- Web Forms 템플릿에 이제 ASP.NET Id에 대 한 계정 확인 및 암호 재설정을 수행 하는 방법을 보여 줍니다.
- 엔터티 데이터 소스 제어 및 Entity Framework 6에 대 한 동적 데이터 공급자입니다. 자세한 내용은 MSDN 블로그를 참조 하세요. [동적 데이터 공급자 및 Entity Framework 6에 대 한 EntityDataSource 컨트롤](https://blogs.msdn.com/b/webdev/archive/2014/01/30/announcing-preview-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx)합니다.

<a id="mvc"></a>
### <a name="aspnet-mvc-512"></a>ASP.NET MVC 5.1.2

- [특성 라우팅 기능 향상](../../../mvc/overview/releases/mvc51-release-notes.md#AttributeRouting)
- [부트스트랩 편집기 템플릿 지원](../../../mvc/overview/releases/mvc51-release-notes.md#Bootstrap)
- [보기에서 열거형 지원](../../../mvc/overview/releases/mvc51-release-notes.md#Enum)
- [Unobstrusive 지원 MinLength / MaxLength 특성](../../../mvc/overview/releases/mvc51-release-notes.md#Unobtrusive)
- ['This'이 컨텍스트 눈에 띄지 않는 ajax 지원](../../../mvc/overview/releases/mvc51-release-notes.md#thisContext)
- 다양 한 [버그 수정](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=MVC&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webapi"></a>
### <a name="aspnet-web-api-212"></a>ASP.NET Web API 2.1.2

- [전역 오류 처리](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#global-error)
- [특성 라우팅 향상 된 기능](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#attribute-routing)
- [도움말 페이지 개선](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#help-page)
- [IgnoreRoute 지원](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#ignoreroute)
- [BSON 미디어 유형 포맷터입니다.](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#bson)
- [비동기 필터에 대 한 지원 향상](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#async-filters)
- [클라이언트 라이브러리를 서식 지정에 대 한 구문 분석 쿼리](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#query-parsing)
- 다양 한 [버그 수정](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20API%7cWeb%20API%20OData&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webpages"></a>
### <a name="aspnet-web-pages-312"></a>ASP.NET Web Pages 3.1.2

- 다양 한 [버그 수정](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20Pages/Razor&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="ef"></a>
### <a name="entity-framework-61"></a>Entity Framework 6.1

Entity Framework 런타임 및 도구에 대 한 버전 6.1로 업데이트 되었습니다. Entity Framework (EF) 6.1 Entity Framework 6에 대 한 부분 업데이트 되며 다양 한 버그 수정 및 새 기능이 포함 되어 있습니다. EF6.1, 새로운 기능에 대 한 설명서에 대 한 링크를 포함 하 여 대 한 자세한 내용은 참조 하세요 [Entity Framework 버전 기록이](https://msdn.microsoft.com/data/jj574253)합니다. 이 릴리스의 새로운 기능은 다음과 같습니다.

- **통합 도구** 새 EF 모델을 만드는 일관적인 방법을 제공 합니다. 이 기능을 기존 데이터베이스에서 리버스 엔지니어링을 포함 하 여 Code First 모델을 만드는 지원 하기 위해 ADO.NET 엔터티 데이터 모델 마법사를 확장 합니다. 이러한 기능은 이전에 베타 품질 EF Power Tools에서 사용할 수 있었습니다.
- **트랜잭션 커밋 오류 처리** 새 제공 [System.Data.Entity.Infrastructure.CommitFailureHandler](https://msdn.microsoft.com/library/system.data.entity.infrastructure.commitfailurehandler(v=vs.113).aspx) 수 있도록 하는 트랜잭션 작업 가로채기 위해 새로 도입 된 기능의 사용 합니다. 합니다 **CommitFailureHandler** 트랜잭션 커밋 시 연결 오류 로부터 자동 복구를 허용 합니다.
- **IndexAttribute** 인덱스 Code First 모델에 속성 (또는 속성)에 대 한 특성을 배치 하 여 지정할 수 있습니다. 먼저 코드 데이터베이스에서 해당 인덱스를 만들 다음 됩니다.
- **공용 매핑 API** EF가 속성 및 형식에 매핑되는 방법을 데이터베이스의 열과 테이블에 정보에 대 한 액세스를 제공 합니다. 이전 릴리스에서에서이 API를 내부.
- **App/Web.config 파일을 통해 인터셉터를 구성 하는 기능**(인터셉터는 응용 프로그램을 다시 컴파일하지 않고도 추가 가능).
- **DatabaseLogger** 쉽게 파일에 모든 데이터베이스 작업을 기록할 새 인터셉터가 있습니다. 이전 기능와 함께에서 따라서 다시 컴파일할 필요 없이 배포 된 응용 프로그램에 대 한 데이터베이스 작업의 로깅을 쉽게 전환할 수 있습니다.
- **마이그레이션 모델 변경 내용 검색** 스 캐 폴드 된 마이그레이션 보다 정확한; 변경 검색 프로세스의 성능을 크게 향상도 되도록 향상 되었습니다.
- **성능 향상** 초기화 하는 동안 감소 데이터베이스 작업을 포함 하 여 LINQ 쿼리에 null 같음 비교에 대 한 최적화 더 빠르게 생성 (모델 생성) 및에서 볼 더 많은 시나리오를 더 효율적 여러 연결을 사용 하 여 추적 된 엔터티의 구체화 합니다.

<a id="identity"></a>
### <a name="aspnet-identity-200"></a>ASP.NET Id 2.0.0

- **2 단계 인증**: ASP.NET Id는 이제 2 단계 인증을 지원 합니다. 2 단계 인증 암호가 손상 된 있는 경우에서 사용자 계정에 보안의 추가 계층을 제공 합니다. 2 단계 코드에 대 한 무차별 공격에 대 한 보호 이기도합니다.
- **계정 잠금:** 사용자가 입력 되지 암호 또는 2 단계 코드 올바르게 사용자를 잠글 수 있습니다. 잘못 된 시도 및 시간 범위 수가 사용자가 잠겨에 대해 구성할 수 있습니다. 개발자는 선택적으로 해제할 수 계정 잠금 특정 사용자 계정에 대 한 필요가 있을 합니다.
- **계정 확인:** ASP.NET Id 시스템은 이제 계정 확인을 지원 합니다. 여기서 웹 사이트에서 새 계정을 등록할 때 해야 웹 사이트에 아무 것도 수행 하기 전에 전자 메일을 확인 하려면 현재 대부분의 웹 사이트에서 매우 일반적인 시나리오입니다. 전자 메일 확인 가짜 계정이 생성 되지 않도록 하기 때문에 유용 합니다. 포럼 사이트, 뱅킹, 전자 상거래 또는 소셜 웹 사이트와 같은 웹 사이트의 사용자와 통신 하는 방법으로 전자 메일을 사용 하는 경우 매우 유용 합니다.
- **암호 재설정:** 암호 재설정은 기능 사용자 암호를 잊어버린 경우 암호를 재설정할 수 있습니다.
- **보안 스탬프 (로그 아웃 everywhere):** 사용자 암호 또는 기타 모든 보안 변경 될 때의 경우 사용자에 대 한 보안 토큰을 다시 생성 하는 방법에 대 한 지원 관련 정보 (예: Facebook, Google, 연관 된 로그인을 제거 하는 등 Microsoft 계정 및 등)입니다. 이 이전 암호를 사용 하 여 생성 된 모든 토큰은 무효화를 확인 해야 합니다. 샘플 프로젝트에서 사용자의 암호를 변경 하는 경우 사용자에 대 한 새 토큰 생성 되 고 모든 이전 토큰이 유효 하지 않습니다. 수 로그 아웃 됩니다 어디에서 든 (다른 모든 브라우저의 경우)이 응용이 프로그램에 로그인 한 위치,이 기능은 추가 계층을 보안 암호를 변경 하면 이후 응용 프로그램을 제공 합니다.
- **사용자 및 역할에 대 한 확장 가능 키의 형식을 만듭니다**: ASP.NET Identity 1.0에서가 테이블 사용자 및 역할에 대 한 기본 키의 유형은 문자열입니다. 이 즉, Entity Framework를 사용 하 여 SQL Server에 ASP.NET Id 시스템을 유지 된 경우, nvarchar를 사용 했습니다. Stack Overflow에서이 기본 구현은 많은 논의가 있었습니다 들어오는 피드백을 기반으로 합니다. 사용자 및 역할 테이블의 기본 키 해야 무엇을 지정할 수 있는 확장성 후크를 제공 했습니다. 이 확장성 후크는 저장 사용자 Id는 Guid 또는 정수 응용 프로그램 및 응용 프로그램을 마이그레이션하는 경우에 특히 유용 합니다.
- **사용자 및 역할의 IQueryable을 지 원하는**: IQueryable UsersStore RolesStore에 대 한 추가 지원 있습니다 사용자 및 역할 목록을 쉽게 가져올 수 있습니다.
- **Usermanager가 통해 삭제 작업 지원**
- **사용자 이름에 인덱싱**: ASP.NET Identity Entity Framework에서 구현을 추가 했습니다 고유 인덱스를 사용자 이름에 새 IndexAttribute 6.1.0 EF에서 사용 하 여 합니다. 이렇게 하면 사용자는 항상 고유 하 고 있는 될 수 있습니다 중복 된 사용자를 사용 하 여 경합 조건이 없는 했습니다.
- **향상 된 암호 유효성 검사기:** 된 ASP.NET Identity 1.0에서 제공 되는 암호 유효성 검사기가 최소 길이 유효성 검사만 된 하는 비교적 기본 암호 유효성 검사기입니다. 새 암호 유효성 검사기 암호의 복잡성을 통해 더 많은 제어를 제공 하는 경우 이 암호의 모든 설정에 설정한 경우에 않는 것이 좋습니다 사용자 계정에 대 한 2 단계 인증을 사용 하도록 설정 하면 note 하십시오.
- **IdentityFactory 미들웨어 / CreatePerOwinContext**:

    - **사용자 관리자**: OWIN 컨텍스트에서 UserManager 인스턴스에 가져오는 공장 구현을 사용할 수 있습니다. 이 패턴은 로그인 및 로그 아웃에 대 한 OWIN 컨텍스트를 AuthenticationManager를 가져오기 위한 사용 비슷합니다. 응용 프로그램에 대 한 요청에 따라 UserManager의 인스턴스를 가져오는 권장된 방법입니다.
    - **DbContextFactory**: ASP.NET Id Entity Framework를 사용 하 여 SQL Server에서 Id 시스템을 유지 합니다. 이렇게 하는 Id 시스템에는 ApplicationDbContext에 대 한 참조를 있습니다. DbContextFactory 미들웨어 응용 프로그램에서 사용할 수 있는 요청에 따라 ApplicationDbContext의 인스턴스를 반환 합니다.
- **ASP.NET Identity 샘플 NuGet 패키지**: 샘플 NuGet 패키지 있습니다 쉽게 설치 및 ASP.NET Id에 대 한 샘플을 실행 하 고 모범 사례를 따르세요. 다음은 샘플 ASP.NET MVC 응용 프로그램입니다. 프로덕션 환경에서이 배포 하기 전에 응용 프로그램에 맞게 코드를 수정 하세요. 빈 ASP.NET 응용 프로그램에서 샘플 설치 되어야 합니다. 패키지에 대 한 자세한 내용은 다음 블로그 게시물 참조: [발표 RTM의 ASP.NET Id 2.0.0](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx)

<a id="owin"></a>
### <a name="microsoft-owin-components"></a>Microsoft OWIN 구성 요소

이 릴리스에서 해결 된 버그 많은 있었습니다. 참조 하세요 합니다 [릴리스 정보는 2.1.0에 대 한 릴리스](https://katanaproject.codeplex.com/releases/view/113281) 좀 더 자세한 내용은 합니다.

<a id="signalr"></a>
### <a name="aspnet-signalr-202"></a>ASP.NET SignalR 2.0.2

이 릴리스에서 해결 된 버그 많은 있었습니다. 참조 하세요 합니다 [릴리스 정보는 2.0.2 이전 릴리스](https://github.com/SignalR/SignalR/releases/tag/2.0.2) 좀 더 자세한 내용은 합니다.
