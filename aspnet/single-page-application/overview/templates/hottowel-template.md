---
uid: single-page-application/overview/templates/hottowel-template
title: Hot Towel 템플릿 | Microsoft Docs
author: madskristensen
description: HotTowel 템플릿
ms.author: riande
ms.date: 02/09/2013
ms.assetid: 75af2e17-6ed3-4d24-8ea1-bc340027c318
msc.legacyurl: /single-page-application/overview/templates/hottowel-template
msc.type: authoredcontent
ms.openlocfilehash: b80b5940b5733a0ae2af3491ccdfa05b84b50343
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41823837"
---
<a name="hot-towel-template"></a>Hot Towel 템플릿
====================
[제작: Mads Kristensen](https://github.com/madskristensen)

> John Papa에서 작성 되었습니다. Hot Towel MVC 템플릿
> 
> 다운로드할 버전을 선택 합니다.
> 
> [Visual Studio 2012 용 hot Towel MVC 템플릿](https://visualstudiogallery.msdn.microsoft.com/1f68fbe8-b4e9-4968-9fd3-ddc7cbc52dca)
> 
> [Visual Studio 2013 용 hot Towel MVC 템플릿](https://visualstudiogallery.msdn.microsoft.com/1eb8780d-d522-4dcf-bf56-56f0eab305c2)
> 
> 
> 핫 수건: 없으면 SPA 이동할 않으려고 하기 때문에!


SPA를 작성 하 고 싶지만 시작 위치를 결정할 수 없습니다. 핫 수건을 사용 하 고 (초)에서 수 있고 SPA를 토대로 하는 데 필요한 모든 도구!

핫 수건 단일 페이지 응용 프로그램 (SPA) ASP.NET 사용 하 여 구축 하기 위한 좋은 시작점이 만듭니다. 즉시 있습니다 제공 모듈형 구조 코드, 뷰 탐색, 데이터 바인딩, 다양 한 데이터 관리 및 간단 하지만 세련 된 스타일을 지정 합니다. 핫 수건은 앱을 연결 하지에 집중할 수 있도록 SPA를 작성 하는 데 필요한 모든 것을 제공 합니다.

> SPA를 빌드하는 방법을 자세히 알아봅니다 [John Papa의 비디오, 자습서 및 Pluralsight 과정](http://johnpapa.net/spa?vsix)합니다.


## <a name="application-structure"></a>응용 프로그램 구조

핫 수건 SPA 응용 프로그램을 정의 하는 JavaScript 및 HTML 파일을 포함 하는 앱 폴더를 제공 합니다.

앱 폴더:

- durandal
- 서비스
- viewmodel
- 뷰

앱 폴더 모듈의 컬렉션을 포함 합니다. 이러한 모듈 기능을 캡슐화 및 다른 모듈에 종속성을 선언 합니다. Views 폴더에는 HTML 응용 프로그램을 포함 하 고 viewmodels 폴더 보기 (일반적인 MVVM 패턴)에 대 한 프레젠테이션 논리를 포함 합니다. Services 폴더에는 응용 프로그램 예: HTTP 데이터 검색 또는 로컬 저장소 상호 작용 해야 할 수 있는 모든 공통 서비스를 보유할 수 있도록 적합 합니다. 하기가 여러 viewmodel에 대 한 일반적인 다시 서비스 모듈의 코드를 사용 합니다.

## <a name="aspnet-mvc-server-side-application-structure"></a>Asp.net 서버 쪽 응용 프로그램 구조

핫 수건 친숙 하 고 강력한 ASP.NET MVC 구조를 기반합니다.

- 앱\_시작
- 콘텐츠
- 컨트롤러
- 모델
- 스크립트
- 보기

## <a name="featured-libraries"></a>주요 라이브러리

- ASP.NET MVC
- ASP.NET Web API
- ASP.NET 웹 최적화-묶음 및 축소
- [Breeze.js](http://Breezejs.com) -다양 한 데이터 관리
- [Durandal.js](http://Durandaljs.com) -탐색 및 보기 구성
- [Knockout.js](http://Knockoutjs.com) -데이터 바인딩
- [Require.js](http://requirejs.org) -AMD 및 최적화를 사용 하 여 모듈화
- [Toastr.js](http://jpapa.me/c7toastr) -팝업 메시지
- [Twitter Bootstrap](http://twitter.github.com/bootstrap/) -강력한 CSS 스타일 지정

## <a name="installing-via-the-visual-studio-2012-hot-towel-spa-template"></a>Visual Studio 2012 핫 수건 SPA 템플릿을 통해 설치

Visual Studio 2012 템플릿으로 핫 수건을 설치할 수 있습니다. 클릭 하기만 `File`  |  `New Project` 선택한 `ASP.NET MVC 4 Web Application`합니다. 선택 된 ' 핫 수건 단일 페이지 응용 프로그램 "템플릿과 실행!

## <a name="installing-via-the-nuget-package"></a>NuGet 패키지를 통해 설치

핫 수건 기존 빈 ASP.NET MVC 프로젝트를 확대 하는 NuGet 패키지를 이기도 합니다. Nuget을 사용 하 여 설치 하 고 실행!

[!code-powershell[Main](hottowel-template/samples/sample1.ps1)]

## <a name="how-do-i-build-on-hot-towel"></a>핫 수건에서 빌드하려면 어떻게 할까요?

코드를 추가 하기만 하면!

1. 사용자 고유의 서버 쪽 코드를 가급적 Entity Framework와 WebAPI (실제로 Breeze.js를 사용 하 여 우수한 성능을 나타내는) 추가
2. 뷰를 추가 합니다 `App/views` 폴더
3. Viewmodel에 추가 된 `App/viewmodels` 폴더
4. 새 보기에 HTML 및 Knockout 데이터 바인딩 추가
5. 탐색 경로 업데이트 합니다. `shell.js`

## <a name="walkthrough-of-the-htmljavascript"></a>HTML/JavaScript의 연습

### <a name="viewshottowelindexcshtml"></a>Views/HotTowel/index.cshtml

index.cshtml에는 시작 경로 및 MVC 응용 프로그램에 대 한 보기입니다. 모든 표준 메타 태그, css 링크 및 예상한 JavaScript 참조를 포함 합니다. 본문은 단일 포함 `<div>` 즉, 모든 콘텐츠 (보기)을 배치할 요청 된 경우. 합니다 `@Scripts.Render` Require.js를 사용 하 여에 포함 된 응용 프로그램의 코드에 대 한 진입점을 실행 하는 `main.js` 파일입니다. 시작 화면 앱을 로드 하는 동안 시작 화면을 만드는 방법을 보여 주기 위해 제공 됩니다.

[!code-cshtml[Main](hottowel-template/samples/sample2.cshtml)]

### <a name="appmainjs"></a>App/main.js

`main.js` 파일에 앱이 로드 되는 즉시 실행 될 코드를 포함 합니다. 탐색 경로 정의 뷰, 시작 설정 및 모든 설치/부트스트래핑 응용 프로그램의 데이터를 초기화 하는 등을 수행 하려는입니다.

`main.js` 파일은 다양 한 시작 응용 프로그램 시작 하는 데 durandal의 모듈을 정의 합니다. 정의 문을 함수에 대해 사용할 수 있도록 모듈 종속성을 확인할 수 있습니다. 먼저 디버깅 메시지가 사용 됩니다, 콘솔 창에 수행 하는 응용 프로그램 이벤트에 대 한 메시지를 보내는. App.start 코드를 응용 프로그램을 시작 하기 위해 durandal 프레임 워크를 알려 줍니다. 규칙은 durandal 알고 모든 보기 및 viewmodels 각각 동일한 명명 된 폴더에 포함 된 되도록 설정 됩니다. 마지막으로 `app.setRoot` 로드를 시작 합니다 `shell` 사용 하 여 미리 정의 된 `entrance` 애니메이션 합니다.

[!code-javascript[Main](hottowel-template/samples/sample3.js)]

## <a name="views"></a>보기

보기에서 발견 되는 `App/views` 폴더입니다.

### <a name="shellhtml"></a>shell.html

`shell.html` HTML에 대 한 마스터 레이아웃을 포함 합니다. 다른 보기의 모든 구성 됩니다 위치에 있는 프로그램 `shell` 보기. 핫 수건 제공을 `shell` 이러한 세 가지 영역을 사용 하 여: 머리글, 콘텐츠 영역 및 바닥글을 합니다. 사용 하 여 로드 되는 이러한 각 지역 내용을 요청 하는 경우 다른 보기를 형성 합니다.

`compose` 머리글 및 바닥글에 대 한 바인딩을 하드 코드 되지를 가리키도록 핫 수건에는 `nav` 및 `footer` 뷰, 각각. 섹션에 대 한 작성 바인딩을 `#content` 바인딩되는 `router` 모듈의 활성 항목입니다. 즉, 클릭 하면 해당 뷰이므로 탐색 링크는이 영역에 로드 됩니다.

[!code-html[Main](hottowel-template/samples/sample4.html)]

### <a name="navhtml"></a>nav.html

`nav.html` SPA에 대 한 탐색 링크를 포함 합니다. 메뉴 구조를 배치할 수 있는, 예를 들어입니다. (Knockout을 사용 하 여) 바인딩된 데이터 인 경우가 많습니다 합니다 `router` 모듈에 정의 된 탐색을 표시 하는 `shell.js`합니다. Knockout 찾습니다 데이터 바인딩 특성 및이를 바인딩합니다 합니다 `shell` viewmodel 탐색 경로 표시 하 고 (Twitter Bootstrap을 사용 하 여) progressbar를 표시할 경우를 `router` 모듈은 하나의 뷰에서 다른 (참조로 이동 하는 중 `router.isNavigating`).

[!code-html[Main](hottowel-template/samples/sample5.html)]

### <a name="homehtml-and-detailshtml"></a>home.html 및 details.html

이러한 뷰는 사용자 지정 보기에 대 한 HTML을 포함합니다. 경우는 `home` 링크를 `nav` 보기의 메뉴를 클릭 하면 합니다 `home` 보기의 콘텐츠 영역에 배치 됩니다는 `shell` 보기. 이러한 뷰를 확대 또는 고유한 사용자 지정 보기를 사용 하 여 대체 수 있습니다.

### <a name="footerhtml"></a>footer.html

`footer.html` 아래쪽의 바닥글에 표시 되는 HTML이 포함 된 `shell` 보기.

## <a name="viewmodels"></a>ViewModels

Viewmodel에서 발견 되는 `App/viewmodels` 폴더입니다.

### <a name="shelljs"></a>shell.js

`shell` viewmodel에 바인딩되어 있는 함수 및 속성이 포함 된 `shell` 보기. 메뉴 탐색 바인딩이 있는 인 경우가 많습니다 (참조는 `router.mapNav` 논리).

[!code-javascript[Main](hottowel-template/samples/sample6.js)]

### <a name="homejs-and-detailsjs"></a>home.js 및 details.js

이러한 viewmodel 속성 및 함수에 바인딩되는 포함 된 `home` 보기. 또한 보기의 경우 프레젠테이션 논리를 포함 하 고 데이터 및 뷰 간의 연결 됩니다.

[!code-javascript[Main](hottowel-template/samples/sample7.js)]

## <a name="services"></a>서비스

서비스 앱/서비스 폴더에 있습니다. 이상적으로 시작 하 고 원격 데이터를 게시 해야 하는 dataservice 모듈과 같은 향후 서비스를 배치할 수 있습니다.

### <a name="loggerjs"></a>logger.js

핫 수건 제공을 `logger` 서비스 폴더에서는 모듈입니다. `logger` 모듈 로깅 메시지를 콘솔 및 알림 팝업에서 사용자에 게 적합 합니다.
