---
uid: visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
title: ASP.NET 및 웹 도구 Visual Studio 2013 릴리스 정보에 대 한 2013.2 | Microsoft Docs
author: microsoft
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/06/2014
ms.topic: article
ms.assetid: 7ef5f73c-ca60-43c1-bdb2-702800347e7e
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
msc.type: authoredcontent
ms.openlocfilehash: 0e7ad52662f7ceaa1f087d007d0b14b610f90bee
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2018
ms.locfileid: "28036026"
---
<a name="aspnet-and-web-tools-20132--for-visual-studio-2013-release-notes"></a>ASP.NET 및 Web Tools 2013.2 for Visual Studio 2013 릴리스 정보
====================
여 [Microsoft](https://github.com/microsoft)

## <a name="installation-notes"></a>설치 참고 사항

ASP.NET 및 Web Tools for Visual Studio 2013.2 주 설치 관리자에 번들로 제공 되 고의 일부로 다운로드할 수 있습니다 [Visual Studio 2013 업데이트 2](https://go.microsoft.com/fwlink/?LinkId=390521)합니다.

## <a name="documentation"></a>설명서

사용할 수 있는 자습서 및 Visual Studio 2013.2에 대 한 ASP.NET 및 Web Tools에 대 한 기타 정보는 [ASP.NET 웹 사이트](https://www.asp.net/)합니다.

## <a name="software-requirements"></a>소프트웨어 요구 사항

ASP.NET 및 Web Tools for Visual Studio 2013.2 Visual Studio 2013 필요 합니다.

## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-20132"></a>ASP.NET 및 Web Tools for Visual Studio 2013.2의 새로운 기능

다음 섹션에서는 릴리스에서 도입 된 기능을 설명 합니다.

- [ASP.NET 프로젝트 템플릿](#oneaspnet)
- [IIS Express에서 웹 응용 프로그램을 시작할 때 SSL을 지원 합니다.](#ssl)
- [Visual Studio 웹 편집기의 향상 된 기능](#vswebeditor)
- [브라우저 링크](#browserlink)
- [Visual Studio에서 Azure 앱 서비스 웹 앱에 대 한 지원](#waws)
- [새 웹 프로젝트를 만들 때 원격 Azure 리소스 만들기](#AzureResources)
- [향상 된 기능으로 웹 게시](#webpublish)
- [ASP.NET 스 캐 폴딩](#scaffolding)
- [NuGet 2.8.1](#nuget)
- [ASP.NET Web Forms](#webforms)
- [ASP.NET MVC 5.1.2](#mvc)
- [ASP.NET Web API 2.1.2](#webapi)
- [ASP.NET 웹 페이지 3.1.2](#webpages)
- [Entity Framework 6.1](#ef)
- [ASP.NET Identity 2.0.0](#identity)
- [Microsoft OWIN 구성 요소](#owin)
- [ASP.NET SignalR 2.0.2](#signalr)

<a id="oneaspnet"></a>
### <a name="one-aspnet-project-templates"></a>ASP.NET 프로젝트 템플릿

- 계정 확인 및 암호 재설정을 지원 하기 위해 ASP.NET 프로젝트 템플릿에 대 한 업데이트가 있습니다.
- ASP.NET Web API 템플릿을에 프레미스 조직 계정을 사용 하는 인증을 지원 하도록 업데이트 합니다.
- SPA 서식 파일에는 이제 MVC 및 서버 쪽 보기를 기반으로 하는 인증을 포함 됩니다. 서식 파일에는 인증 된 사용자만 액세스할 수 있는 WebAPI 컨트롤러를 있습니다.

<a id="ssl"></a>
### <a name="support-ssl-when-launching-web-applications-on-iis-express"></a>IIS Express에서 웹 응용 프로그램을 시작할 때 SSL을 지원 합니다.

탐색과 localhost에서 HTTPS를 디버깅 하는 경우 보안 경고를 방지 하려면 자체 서명 된 IIS를 신뢰 하도록 Internet Explorer 및 Chrome express SSL 인증서를 허용 하는 대화 상자를 추가 했습니다.

예를 들어 SSL을 사용 하도록 웹 프로젝트 속성을 설정할 수 있습니다. 속성 대화 상자를 표시 하려면 F4를 클릭 합니다. 변경 **SSL 사용** true로 합니다. SSL URL을 복사 합니다.

![SSL 사용 속성](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image1.png)

HTTPS를 사용 하도록 웹 프로젝트 속성 페이지 웹 탭 집합 기반 URL (SSL URL 됩니다 `https://localhost:44300/` SSL 웹 사이트를 이전에 만든 경우가 아니면.)

![프로젝트 URL (HTTPS)를 설정 합니다.](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image2.png)

Ctrl+F5를 눌러 응용 프로그램을 실행합니다. IIS Express에서 생성 하는 자체 서명 된 인증서를 신뢰 하도록 지시를 따릅니다.

![SSL 경고](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image3.png)

읽기는 **보안 경고** 대화 상자와 클릭 **예** 나타내는 localhost 인증서를 설치 하려는 경우.

![보안 경고](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image4.png)

사이트 IE 또는 크롬에 표시 될 브라우저에 인증서 경고 없이 합니다.

![경고 없이 HTTPS 페이지](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image5.png)

Firefox에서 경고를 표시 하므로 인증서 저장소를 사용 합니다.

<a id="vswebeditor"></a>
### <a name="visual-studio-web-editor-enhancements"></a>Visual Studio 웹 편집기의 향상 된 기능

- **새 JSON 프로젝트 항목 및 편집기**: JSON 프로젝트 항목 및 편집기 Visual Studio에 추가 했습니다. 현재 JSON 편집기 기능 색 지정, 구문 유효성 검사, 중괄호 완성, 개요, 도구 옵션 설정 등을 포함 합니다.

    ![JSON 편집기](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image6.png)

    IntelliSense에서 지 원하는 [JSON 스키마](http://json-schema.org/) v3 및 v4 합니다. 로컬 스키마 경로 편집 하려면 기존 스키마를 선택 합니다. 스키마 콤보 상자 또는 끌어서 놓기 프로젝트 JSON 파일에 대 한 상대 경로 가져올 수 있습니다.

    ![JSON Intellisense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image7.png)    ![JSON 스키마 편집기](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image8.png)
- **새 Sass (SCSS) 편집기**: 했습니다 Sass 프로젝트 항목 및 편집기 및 v s 2013 rtm에서 작은 추가 했습니다. Sass 편집기 기능 LESS 편집기에 버금가 및 색 지정, 변수 및 Mixin IntelliSense, 설명/주석 처리를 제거, 요약 정보, 서식 지정, 구문 유효성 검사, 개요, 정의 이동, 색 선택 도구 옵션 설정 하는 등 합니다.

    ![SCSS 스타일 시트를 새 항목 추가:](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image9.png)    ![스타일 시트 편집기](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image10.png)
- **HTML, Razor, CSS에서 덜 새 URL 선택기 및 Sass 문서:** VS 2013 Web Forms 페이지 밖에 없는 URL 선택기와 함께 제공 합니다. HTML, Razor, CSS, 적은 대 한 새 URL 선택기 및 Sass 편집기에 대 한 이해 하는 대화에 필요 없는, fluent 입력 선택은 '..' 컴퓨터의 목록과 필터 파일 적절 하 게 img 태그와 연결 합니다.

    ![이미지 태그에 대 한 URL 선택](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image11.png)    ![뷰에 대 한 URL 선택](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image12.png)    ![CSS에 대 한 URL 선택](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image13.png)
- **더 많은 기능을 추가 하 여 LESS 편집기에 대 한 업데이트**
- **Knockout Intellisense 업그레이드**: VS intelliSense에 대 한 비표준 KnockOut 구문을 추가 "ko vs 편집기 viewModel:" 구문입니다. 형식에서 주석을 사용 하 여 페이지에서 여러 보기 모델에 바인딩하는 사용할 수 있습니다.

    ![Knockout Intellisense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image14.png)

    또한 지원이 추가 되었습니다 중첩된 ViewModel IntelliSense에 대 한 깊이 중첩 된 ViewModel 개체에 드릴 수 있도록 합니다.

    `<div data-bind="text: foo.bar.baz.etc" />`

    표시 IntelilSense JavaScript 개체의 전체 IntelliSense입니다.

    ![Intellisense 보여 주는 전체 JavaScript 개체](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image15.png)
- **HTML, Razor, CSS에서 덜 새 URL 선택기 및 Sass 문서**: VS 2013 Web Forms 페이지 밖에 없는 URL 선택기와 함께 제공 합니다. HTML, Razor, CSS, 적은 대 한 새 URL 선택기 및 Sass 편집기에 대 한 이해 하는 대화에 필요 없는, fluent 입력 선택은 '..' 컴퓨터의 목록과 필터 파일 적절 하 게 img 태그와 연결 합니다.

    ![이미지 태그에 대 한 URL 선택](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image16.png)    ![뷰에 대 한 URL 선택](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image17.png)    ![CSS에 대 한 URL 선택](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image18.png)

<a id="browserlink"></a>
### <a name="browser-link"></a>브라우저 링크

- 브라우저 링크는 이제 HTTPS 연결을 지원 하 고 표시 하는 대시보드에 다른 연결과 함께으로 브라우저에서의 인증서를 신뢰 합니다.
- 정적 HTML 소스 매핑
- SPA 매핑 데이터에 대 한 지원
- 자동 업데이트, 데이터 매핑

<a id="waws"></a>
### <a name="support-for-azure-app-service-web-apps-in-visual-studio"></a>Visual Studio에서 Azure 앱 서비스 웹 앱에 대 한 지원

- **지원 Azure에 로그인 합니다.**
- **원격 디버깅 및 웹 앱에 대 한 원격 뷰**: 이제 지원 [Azure 앱 서비스의 웹 앱에 대 한 원격 디버깅](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio) 및 서버 탐색기에서 웹 응용 프로그램 콘텐츠 파일의 원격 보기.

<a id="AzureResources"></a>
### <a name="create-remote-azure-resources-when-creating-a-new-web-project"></a>새 웹 프로젝트를 만들 때 원격 Azure 리소스 만들기

추가 Azure ["원격 리소스 만들기"](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet) 새 웹 응용 프로그램 대화 상자에서 확인란을 선택 합니다. 를 선택 하 여 새 웹 응용 프로그램을 테스트 하 고 몇 가지 간단한 단계에서 게시 프로필을 만들기 위한 Azure 게시 사이트 설정의 환경을 통합 수 있습니다.

![Azure 리소스를 사용 하 여 새 프로젝트](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image19.png)![Azure에 게시](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image20.png)

<a id="webpublish"></a>
### <a name="web-publish-enhancements"></a>향상 된 기능으로 웹 게시

- 게시에 대 한 사용자 환경을 개선 합니다.

<a id="scaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET 스 캐 폴딩

- **열거형 지원:** 모델에 열거형을 사용 하는 경우 MVC Scaffolder 열거형에 대 한 드롭다운을 생성 합니다. 이 MVC의 Enum 도우미를 사용합니다.
- **지원 부트스트랩**: 부트스트랩 클래스를 사용 하도록 MVC 스 캐 폴딩의 EditorFor 서식 파일을 업데이트 합니다.
- **지원 패키지**: MVC 및 Web API 스 캐 폴더 및 웹 API의 MVC 5.1 패키지를 추가 합니다

다음 스크린샷에서 스 캐 폴딩 모델을 보여 줍니다.

- 코드 모델:

     ![코드 모델](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image21.png)
- 컴파일 모델 코드에서 마우스 선택 **추가**, **스 캐 폴드 된 새 항목**합니다.

     ![스 캐 폴드 새 항목 추가](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image22.png)
- 선택 **Entity Framework를 사용 하 여를 뷰와 m v c 5 컨트롤러**:

     ![뷰가 포함 된 새 m v c 5 컨트롤러 추가](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image23.png)
- **컨트롤러 추가** 모델을 사용 하 여:

    ![](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image24.png)
- 예를 들어 Views/WeekdayModels/Edit.cshtml 생성 된 코드를 확인 `@Html.EnumDropDownListFor`: ![EnumDropDownListFor 포함 된 보기](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image25.png)
- 생성 된 enum combobox 참조, 값은 null 일 수 있습니다, 빈 문자열 콤보 상자에 대 한 선택할 수 있습니다를 확인할 페이지를 실행 합니다. 예를 들어는 **만들기** 페이지 다음에 표시 합니다.

    ![빈 문자열을 허용 하는 콤보 상자](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image26.png)

<a id="nuget"></a>
### <a name="nuget-281"></a>NuGet 2.8.1

NuGet RTM는 2014 년 4 월에에서 출시 될 2.8.1. 릴리스 정보에서 눈에 띄는 지점은 없지만 확인 하십시오 여기는 [전체 릴리스 정보](http://docs.nuget.org/docs/release-notes/nuget-2.8) 이러한 변경 내용에 대 한 자세한 내용은 합니다.

- **Windows Phone 8.1 응용 프로그램을 대상**: NuGet 2.8.1 이제 Windows Phone 8.1 응용 프로그램의 대상 프레임 워크 모니커 '이 WindowsPhoneApp', 'WPA', 'WindowsPhoneApp81' 및 'WPA81'를 사용 하 여 대상 지정을 지원 합니다.
- **종속성에 대 한 패치 해상도**: 패키지 종속성을 확인할 때 NuGet가 지금까지 패키지의 종속성을 만족 하는 가장 낮은 주 및 부 패키지 버전을 선택 하는 전략을 구현 합니다. 그러나 주 및 부 버전을 달리 패치 버전 항상 해결 된 가장 높은 버전으로 합니다. 또한 악의적 동작 이지만 패키지 종속성이 설치를 위한 결정성이 부족 한 만들어집니다.
- **DependencyVersion 스위치**: 있지만 NuGet 2.8 변경는 *기본* 종속성 확인에 대 한 동작을 추가 종속성 확인 프로세스에서-DependencyVersion 스위치를 통해 보다 자세히 제어의 패키지 관리자 콘솔입니다. 스위치 가능한 가장 낮은 버전 (기본 동작), 가능한 최상 버전 또는 부 가장 높은 또는 패치 버전을 확인 하 고 종속성을 수 있습니다. 이 스위치는 powershell 명령에서 설치 패키지에 대 한 에서만 작동합니다.
- **DependencyVersion 특성**: 위에서 설명한-DependencyVersion 스위치, 뿐 아니라 NuGet에도 허용-DependencyVersion 전환 하는 경우 기본값은 무엇을 정의 하는 nuget.config 파일에서 새 특성을 설정 하는 기능 설치 패키지의 호출에 지정 되지 않았습니다. 이 값 NuGet 패키지 관리자 대화 상자 설치 패키지는 모든 작업에도 적용 됩니다. 이 값을 설정 하려면 아래 특성 nuget.config 파일을 추가 합니다.

    `<config> <add key="dependencyversion" value="Highest" /> </config>`
- **NuGet 작업와-whatif를 미리 볼**: 일부 NuGet 패키지 전체 종속성 그래프를 가질 수 있습니다 및 이와 같이 수는 설치 중에 도움이 될, 제거 또는 업데이트 작업을 먼저 실행 되는 작업을 볼 수 있습니다. 표준 PowerShell을 추가 하는 NuGet 2.8-경우에 어떻게 명령을 적용 하는 패키지의 전체 closure 시각화를 사용 하도록 설정 하기 위해 패키지 설치, 제거 패키지 및 업데이트 패키지 명령으로 전환 합니다.
- **패키지를 다운 그레이드**: 안정적인 마지막 버전으로 롤백할로 결정 한 새 기능을 검토 하려면 패키지의 시험판 버전을 설치 하는 경우가 종종 있습니다. NuGet 2.8 하기 전에이 시험판 패키지 및 해당 종속성을 제거한 다음 이전 버전을 설치의 여러 단계 프로세스입니다. 그러나 NuGet 2.8와 업데이트 패키지는 이제 롤백할 전체 패키지 클로저 (예: 패키지의 종속성 트리) 이전 버전으로.
- **개발 종속성**: NuGet 패키지-개발 프로세스를 최적화 하는 데 사용 되는 도구를 포함 하 여 다양 한 유형의 기능 전달할 수 있습니다. 이러한 구성 요소를 새 패키지를 개발에 도움이 될 수 있지만 간주 되지 않아야 이후이 경우 새 패키지의 종속성 게시 합니다. NuGet 2.8 패키지를.nuspec 파일은 developmentDependency로에서 자신을 식별할 수 있습니다. 설치 되 면이 메타 데이터도 패키지가 설치 된 프로젝트의 packages.config 파일에 추가 됩니다. Packages.config 파일은 나중에 분석 NuGet 종속성에 대 한 nuget.exe 팩 중 때 개발 종속성으로 표시 하는 이러한 종속성 제외 됩니다.
- **다양 한 플랫폼에 대 한 개별 packages.config 파일**: 여러 대상 플랫폼에 대 한 응용 프로그램을 개발할 때 일반적으로 각 해당 빌드 환경에 대 한 여러 프로젝트 파일입니다. 것도 다른 프로젝트 파일에서 다른 NuGet 패키지를 사용 하도록 패키지에 다양 한 플랫폼에 대 한 지원 수준이 다양 한 대로 합니다. 다른 플랫폼 관련 프로젝트 파일에 대 한 다른 packages.config 파일을 만들어이 시나리오에 대 한 향상 된 지원을 제공 하는 NuGet 2.8 합니다.
- **로컬 캐시에 대체**: 있지만 NuGet 패키지는 일반적으로 사용 된 원격 갤러리에서와 같은 [NuGet 갤러리](http://www.nuget.org) 는 네트워크 연결을 사용 하 여 다양 한 시나리오는 클라이언트가 연결 되지 않았습니다. 네트워크 연결 없이 NuGet 클라이언트에서 이러한 패키지는 로컬 캐시 NuGet의에서 클라이언트 컴퓨터에 이미 있던 경우에 패키지-설치할 수 없습니다. NuGet 2.8 패키지 관리자 콘솔에 대체 (fallback) 자동 캐시를 추가합니다.

    캐시 대체 기능에는 특정 명령 인수 필요 하지 않습니다. 또한 캐시 대체 현재 패키지 관리자 콘솔 에서만에서 작동 함-동작 패키지 관리자 대화 상자에서 현재 작동 하지 않습니다.
- **버그 수정**: 업데이트 패키지의 성능 향상 된 만든 주요 버그 수정 중 하나-명령을 다시 설치 합니다.

    이러한 기능과 앞에서 언급 한 성능 수정 외에이 버전의 NuGet 다른 많은 버그 수정 포함 되어 있습니다. 181 총 문제는 릴리스에서 해결 했습니다. 작업의 전체 목록에 대 한 항목에서에서 수정 된 NuGet 2.8 하십시오 보기는 [NuGet 문제 추적기](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all) 이 릴리스에 대 한 합니다.

<a id="webforms"></a>
### <a name="aspnet-web-forms"></a>ASP.NET Web Forms

- 이제 Web Forms 서식 파일에는 ASP.NET Identity에 대 한 계정 확인 및 암호 재설정을 수행 하는 방법을 보여 줍니다.
- 엔터티 데이터 소스 제어 및 Entity Framework 6에 대 한 동적 데이터 공급자입니다. 자세한 내용은 다음 MSDN 블로그를 참조 하십시오: [동적 데이터 공급자 및 Entity Framework 6에 대 한 EntityDataSource 컨트롤](https://blogs.msdn.com/b/webdev/archive/2014/01/30/announcing-preview-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx)합니다.

<a id="mvc"></a>
### <a name="aspnet-mvc-512"></a>ASP.NET MVC 5.1.2

- [라우팅 향상 된 기능 특성](../../../mvc/overview/releases/mvc51-release-notes.md#AttributeRouting)
- [부트스트랩 편집기 템플릿 지원](../../../mvc/overview/releases/mvc51-release-notes.md#Bootstrap)
- [뷰에서 열거형 지원](../../../mvc/overview/releases/mvc51-release-notes.md#Enum)
- [Unobstrusive 지원 MinLength / MaxLength 특성](../../../mvc/overview/releases/mvc51-release-notes.md#Unobtrusive)
- [비 가시적인 Ajax에서 'this'이 컨텍스트를 지 원하는](../../../mvc/overview/releases/mvc51-release-notes.md#thisContext)
- 다양 한 [버그 수정](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=MVC&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webapi"></a>
### <a name="aspnet-web-api-212"></a>ASP.NET Web API 2.1.2

- [전역 오류 처리](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#global-error)
- [라우팅의 향상 된 기능 특성](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#attribute-routing)
- [도움말 페이지 기능 향상](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#help-page)
- [IgnoreRoute 지원](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#ignoreroute)
- [BSON 미디어 유형 포맷터입니다.](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#bson)
- [비동기 필터에 대 한 지원 향상](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#async-filters)
- [쿼리는 클라이언트 라이브러리를 서식 지정에 대 한 구문](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#query-parsing)
- 다양 한 [버그 수정](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20API%7cWeb%20API%20OData&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webpages"></a>
### <a name="aspnet-web-pages-312"></a>ASP.NET 웹 페이지 3.1.2

- 다양 한 [버그 수정](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20Pages/Razor&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="ef"></a>
### <a name="entity-framework-61"></a>Entity Framework 6.1

Entity Framework 런타임 및 도구가 둘 다에 대해 6.1 버전으로 업데이트 되었습니다. Entity Framework (EF) 6.1 Entity Framework 6에 대 한 부분 업데이트는 버그 픽스와 새로운 기능을 포함 하 고 있습니다. 참조에 대 한 자세한 내용은 새로운 기능에 대 한 설명서에 대 한 링크를 포함 하 여 EF6.1 [Entity Framework 버전 기록이](https://msdn.microsoft.com/data/jj574253)합니다. 이 릴리스의 새로운 기능은 다음과 같습니다.

- **통합 tooling** 일관 된 새 EF 모델을 만들 수 있습니다. 이 기능은 ADO.NET 엔터티 데이터 모델 마법사에서 기존 데이터베이스 리버스 엔지니어링을 포함 하 여 만드는 Code First 모델을 지원 하도록 확장 합니다. 이러한 기능은 EF 파워 도구에서 베타 품질에서 이전에 사용할 수 없었습니다.
- **트랜잭션 커밋 실패의 처리** 제공 새 [System.Data.Entity.Infrastructure.CommitFailureHandler](https://msdn.microsoft.com/library/system.data.entity.infrastructure.commitfailurehandler(v=vs.113).aspx) 를 사용 하는 기능이 새로 도입 된 트랜잭션 작업을 가로챌 수 있습니다. **CommitFailureHandler** 트랜잭션을 커밋하는 동안 연결 오류 로부터 자동 복구를 허용 합니다.
- **IndexAttribute** 인덱스를 Code First 모델의 속성 (또는 속성)에 대 한 특성을 배치 하 여 지정할 수 있습니다. 먼저 코드는 데이터베이스에 해당 인덱스를 만들 다음 됩니다.
- **공용 매핑 API** EF 속성 및 형식에 매핑하는 방식을 데이터베이스의 열과 테이블에는 정보에 대 한 액세스를 제공 합니다. 이전 릴리스와에서이 API를 내부 합니다.
- **App/Web.config 파일을 통해 인터셉터를 구성 하는 기능**(응용 프로그램을 다시 컴파일하지 않고도 추가할 인터셉터 허용).
- **DatabaseLogger** 쉽게 파일에 모든 데이터베이스 작업을 기록 하는 새 인터셉터가 있습니다. 이전 기능 함께, 이렇게 하면 다시 컴파일할 필요 없이 배포 된 응용 프로그램에 대 한 데이터베이스 작업의 로깅을 쉽게 전환할 수 있습니다.
- **마이그레이션 모델 변경 내용 검색** 마이그레이션을 스 캐 폴드 보다 정확한; 변경 검색 프로세스의 성능을 크게 향상도 되도록 향상 되었습니다.
- **성능 향상** 초기화 하는 동안 감소 데이터베이스 작업을 포함 하 여 LINQ 쿼리에 null 같음 비교에 대 한 최적화 더 빠르게 생성 (모델 생성) 및에서 볼 더 많은 시나리오를 보다 효율적인 추적 된 엔터티에 대 한 여러 연결의 구체화 합니다.

<a id="identity"></a>
### <a name="aspnet-identity-200"></a>ASP.NET Identity 2.0.0

- **2 단계 인증**: ASP.NET Identity 이제 2 단계 인증을 지원 합니다. 2 단계 인증 추가 계층 암호가 손상 되는 경우에서 사용자 계정에 보안을 제공 합니다. 2 단계 코드에 대 한 무차별 암호 대입 공격에 대 한 보호 이기도합니다.
- **계정 잠금:** 사용자가 입력 되지 암호 또는 2 단계 코드 올바르게 사용자를 잠글 수 있는 방법을 제공 합니다. 잘못 된 시도 및 시간 범위 수는 사용자가 잠겨에 대해 구성할 수 있습니다. 개발자는 선택적으로 해제할 수 계정 잠금 특정 사용자 계정에 대 한 필요가 있을.
- **계정 확인:** ASP.NET Id 시스템은 이제 계정 확인을 지원 합니다. Where, 웹 사이트에서 새 사용자 계정을 등록 해야 하는 웹 사이트에 아무 것도 수행 하려면 먼저 사용자의 전자 메일 확인 대부분 오늘날의 웹 사이트에는 매우 일반적인 시나리오입니다. 전자 메일 확인 만들어지지 않도록 보 거 스 계정을 못하기 때문에 유용 합니다. 포럼 사이트, 금융, 전자 상거래, 또는 소셜 웹 사이트와 같은 웹 사이트의 사용자와의 통신 하는 방법으로 전자 메일을 사용 하는 경우 매우 유용 합니다.
- **암호 재설정:** 암호 재설정 사용자 암호를 잊은 경우 암호를 재설정할 수 기능입니다.
- **보안 스탬프 (로그 아웃 everywhere):** 사용자가 암호 또는 기타 보안을 변경할 때 보안 토큰의 경우 사용자에 대 한 다시 생성 하는 방법에서는 관련 정보 (예: Facebook, Google, 연결된 된 로그인을 제거 하는 등 Microsoft 계정 및 등)입니다. 이 이전 암호를 사용 하 여 생성 하는 모든 토큰 무효화 됩니다 되도록 필요 합니다. 샘플 프로젝트에 사용자의 암호를 변경 하는 경우 그런 다음 새 토큰을 사용자에 대해 생성 되 고 모든 이전 토큰이 무효화 됩니다. 어디에서 나 (다른 모든 브라우저의 경우)이 응용이 프로그램에 로그인 한 여기서 로그인 됩니다, 그리고이 기능에는 추가적인 보안 암호를 변경 하면 이후 응용 프로그램을 제공 합니다.
- **사용자 및 역할에 대 한 확장 될 수는 기본 키의 유형 확인**: ASP.NET Identity 1.0에서가 테이블 사용자 및 역할에 대 한 기본 키의 유형은 문자열입니다. 이러한 의미는 ASP.NET Identity 시스템 Entity Framework를 사용 하 여 SQL Server에서 유지 되는 경우 nvarchar를 사용 했습니다. 이 기본 구현은 스택 오버플로에 많은 논의 했습니다 들어오는 의견을 기반으로 하 고 있습니다. 사용자 및 역할 테이블의 기본 키 해야 하는지 지정할 수 있는 확장성 후크를 제공 했습니다. 이 확장성 후크는 저장 사용자 Id는 Guid 또는 정수는 응용 프로그램의 응용 프로그램을 마이그레이션하는 경우에 특히 유용 합니다.
- **사용자 및 역할의 IQueryable 지원**: UsersStore 및 RolesStore IQueryable에 대 한 지원 추가, 있습니다 사용자 및 역할의 목록을 쉽게 가져올 수 있습니다.
- **Usermanager가 통해 삭제 작업을 지원 합니다.**
- **사용자 이름에 대해 인덱싱을**: ASP.NET Identity Entity Framework 구현을 추가 했습니다 고유 인덱스를 사용자 이름에 새 IndexAttribute 6.1.0 EF에서 사용 하 여 합니다. 이렇게 하면 사용자는 항상 고유 하 고 있는 될 수 있습니다 중복 된 사용자 이름으로 경합 조건이 없는 했습니다.
- **향상 된 암호 유효성 검사기:** ASP.NET Identity 1.0에서 발송 된 암호 유효성 검사기가 매우 기본적인 암호 유효성 검사기를만 최소 길이 유효성을 검사 했습니다. 새 암호 유효성 검사기 암호의 복잡성을 더 많이 제어할 수 있게 해 주는 있습니다. 이 암호의 모든 설정을 설정한 경우에 않는 것이 좋습니다 사용자 계정에 대해 2 단계 인증을 사용할 수 있습니다. note 하십시오.
- **IdentityFactory 미들웨어 / CreatePerOwinContext**:

    - **사용자 관리자**: 프로그램의 인스턴스를 가져오는 UserManager OWIN 컨텍스트를 팩터리 구현을 사용할 수 있습니다. 이 패턴은 로그인 및 로그 아웃에 대 한 OWIN 컨텍스트를 AuthenticationManager를 가져오기 위한 사용한 비슷합니다. 이것이 응용 프로그램에 대 한 요청에 따라 UserManager의 인스턴스를 가져오는 권장된 방법입니다.
    - **DbContextFactory**: ASP.NET Identity Entity Framework를 사용 하 여 SQL Server에서 Id 시스템을 유지 합니다. Id 시스템이 작업을 수행 하기는 ApplicationDbContext에 대 한 참조를 있습니다. DbContextFactory 미들웨어 응용 프로그램에서 사용할 수 있는 요청당 ApplicationDbContext의 인스턴스를 반환 합니다.
- **ASP.NET Identity 샘플 NuGet 패키지**: 샘플 NuGet 패키지 쉽게 만들 수를 설치 하 고 ASP.NET Identity에 대 한 샘플을 실행 하 고 모범 사례를 준수 합니다. 샘플 ASP.NET MVC 응용 프로그램입니다. 프로덕션 환경에서이 배포 하기 전에 응용 프로그램에 맞게 코드를 수정 하십시오. 빈 ASP.NET 응용 프로그램에 샘플을 설치 해야 합니다. 패키지에 대 한 자세한 내용은 다음 블로그 게시물으로 이동: [발표 RTM의 ASP.NET Identity 2.0.0](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx)

<a id="owin"></a>
### <a name="microsoft-owin-components"></a>Microsoft OWIN 구성 요소

이 릴리스에서 수정 된 버그를 많이 있었습니다. 참조 하십시오는 [릴리스 정보는 2.1.0 릴리스](https://katanaproject.codeplex.com/releases/view/113281) 대 한 자세한 내용은 합니다.

<a id="signalr"></a>
### <a name="aspnet-signalr-202"></a>ASP.NET SignalR 2.0.2

이 릴리스에서 수정 된 버그를 많이 있었습니다. 참조 하십시오는 [릴리스 정보는 2.0.2 릴리스](https://github.com/SignalR/SignalR/releases/tag/2.0.2) 대 한 자세한 내용은 합니다.
