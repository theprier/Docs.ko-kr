---
uid: single-page-application/overview/templates/hottowel-template
title: "핫 수건 템플릿 | Microsoft Docs"
author: madskristensen
description: "HotTowel 서식 파일"
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/09/2013
ms.topic: article
ms.assetid: 75af2e17-6ed3-4d24-8ea1-bc340027c318
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /single-page-application/overview/templates/hottowel-template
msc.type: authoredcontent
ms.openlocfilehash: bfc6e2c884c422f44e8be5f4f29554ae86f7ecb6
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="hot-towel-template"></a>핫 수건 서식 파일
====================
여 [Kristensen Mads](https://github.com/madskristensen)

> John 예가 핫 수건 MVC 템플릿 작성
> 
> 버전을 다운로드 하려면를 선택 합니다.
> 
> [Visual Studio 2012에 대 한 핫 수건 MVC 템플릿](https://visualstudiogallery.msdn.microsoft.com/1f68fbe8-b4e9-4968-9fd3-ddc7cbc52dca)
> 
> [Visual Studio 2013에 대 한 핫 수건 MVC 템플릿](https://visualstudiogallery.msdn.microsoft.com/1eb8780d-d522-4dcf-bf56-56f0eab305c2)


> 핫 수건: 하나가 없어서 SPA로 이동 하려고 하므로!


SPA를 작성 하려고 하지만 시작 위치를 결정할 수 없습니다. 핫 수건을 사용 하 여 및 초에서 해야 합니다.에 빌드하는 데 필요한 모든 도구와 한 SPA!

핫 수건은 단일 페이지 응용 프로그램 (SPA) ASP.NET으로 작성 하기 위한 좋은 출발점을 만듭니다. 즉시 있습니다 제공 모듈형 구조 코드, 보기 탐색, 데이터 바인딩, 다양 한 데이터 관리 및 스타일을 간단 하지만 유용 합니다. 핫 수건 배관 하지 앱에 집중할 수는 SPA를 만드는 데 필요한 모든를 제공 합니다.

> SPA를 구축 하는 방법에 대 한 자세한 정보 [John 예의 비디오, 자습서 및 Pluralsight 교육 과정](http://johnpapa.net/spa?vsix)합니다.


## <a name="application-structure"></a>응용 프로그램 구조

핫 수건 SPA 응용 프로그램을 정의 하는 JavaScript 및 HTML 파일을 포함 하는 응용 프로그램 폴더를 제공 합니다.

응용 프로그램 폴더에 저장 합니다.

- durandal
- 서비스
- viewmodel
- 뷰

응용 프로그램 폴더는 모듈의 컬렉션을 포함합니다. 이러한 모듈의 기능을 캡슐화 하 고 다른 모듈에 대해 종속성을 선언 합니다. Views 폴더에는 응용 프로그램에 대 한 HTML 포함 되 고 viewmodel 폴더 뷰 (공통 MVVM 패턴)에 대 한 프레젠테이션 논리를 포함 합니다. 서비스 폴더는 응용 프로그램 예: HTTP 데이터 검색 또는 로컬 저장소의 상호 작용 해야 하는 모든 공통 서비스 보유할 수 있도록 이상적입니다. 것에 대 한 여러 viewmodel 서비스 모듈에서 코드 다시 사용 합니다.

## <a name="aspnet-mvc-server-side-application-structure"></a>ASP.NET MVC 서버 쪽 응용 프로그램 구조

핫 수건 친숙 하 고 강력한 ASP.NET MVC 구조 기반으로 합니다.

- 응용 프로그램\_시작
- 콘텐츠
- 컨트롤러
- 모델
- 스크립트
- 보기

## <a name="featured-libraries"></a>추천된 라이브러리

- ASP.NET MVC
- ASP.NET Web API
- ASP.NET 웹 최적화-묶음 및 축소
- [Breeze.js](http://Breezejs.com) -다양 한 데이터 관리
- [Durandal.js](http://Durandaljs.com) -탐색 및 보기 구성
- [Knockout.js](http://Knockoutjs.com) -데이터 바인딩
- [Require.js](http://requirejs.org) -모듈화 AMD 및 최적화
- [Toastr.js](http://jpapa.me/c7toastr) -팝업 메시지
- [부트스트랩 twitter](http://twitter.github.com/bootstrap/) -강력한 CSS 스타일 지정

## <a name="installing-via-the-visual-studio-2012-hot-towel-spa-template"></a>Visual Studio 2012 핫 수건 SPA 서식 파일을 통해 설치

Visual Studio 2012 템플릿으로 핫 수건을 설치할 수 있습니다. 클릭 하기만 `File`  |  `New Project` 선택 `ASP.NET MVC 4 Web Application`합니다. 다음을 선택 된 ' 핫 수건 단일 페이지 응용 프로그램 "템플릿과 실행!

## <a name="installing-via-the-nuget-package"></a>NuGet 패키지를 통해 설치

핫 수건 기존 빈 ASP.NET MVC 프로젝트를 확대 하는 NuGet 패키지 이기도 합니다. Nuget을 사용 하 여 설치 하 고 실행!

[!code-powershell[Main](hottowel-template/samples/sample1.ps1)]

## <a name="how-do-i-build-on-hot-towel"></a>핫 수건 토대로 방법

단순히 코드 추가 시작!

1. 가급적 Entity Framework와 WebAPI (Breeze.js와 줄)에 사용자 고유의 서버 쪽 코드 추가
2. 뷰를 추가 `App/views` 폴더
3. Viewmodel에 추가 `App/viewmodels` 폴더
4. 새 보기에 HTML 및 Knockout 데이터 바인딩 추가
5. 탐색 경로 업데이트 합니다.`shell.js`

## <a name="walkthrough-of-the-htmljavascript"></a>HTML/JavaScript의 연습

### <a name="viewshottowelindexcshtml"></a>Views/HotTowel/index.cshtml

index.cshtml는 시작 경로 및 MVC 응용 프로그램에 대 한 보기입니다. 모든 표준 메타 태그, css 링크 및 예상 되는 JavaScript 참조를 포함 합니다. 포함 하는 하나의 본문 `<div>` 즉, 모든 콘텐츠 (views) 배치 될 위치 요청 되는 경우. `@Scripts.Render` Require.js를 사용 하 여에 포함 되어 있는 응용 프로그램의 코드에 대 한 진입점을 실행 하는 `main.js` 파일입니다. 시작 화면을 응용 프로그램에서 로드 되는 동안 시작 화면을 만드는 방법을 보여 주기 위해 제공 됩니다.

[!code-cshtml[Main](hottowel-template/samples/sample2.cshtml)]

### <a name="appmainjs"></a>App/main.js

`main.js` 파일에 코드가 사용자 응용 프로그램이 로드 되는 즉시 실행 됩니다. 탐색 경로 정의 뷰, 시작 및 모든 설치/부트스트래핑 응용 프로그램의 데이터를 priming 등을 수행 하려면 원하는입니다.

`main.js` 시작 응용 프로그램 준비 수 있도록 durandal의 모듈의 여러 파일을 정의 합니다. 정의 문의 함수에 대해 사용할 수 있도록 모듈 종속성을 해결 합니다. 먼저는 디버깅 메시지를 사용할 수을 수행 하 고 콘솔 창에 있는 이벤트에 대 한 메시지를 보낼입니다. App.start 코드 응용 프로그램을 시작 하기 위해 durandal 프레임 워크를 알려 줍니다. 규칙은 durandal 모든 보기를 알고 있으며 각각와 같은 명명 된 폴더에 포함 된 viewmodel 되도록 설정 됩니다. 마지막으로 `app.setRoot` 로드를 시작 하기 전에 `shell` 사용 하 여 미리 정의 된 `entrance` 애니메이션 합니다.

[!code-javascript[Main](hottowel-template/samples/sample3.js)]

## <a name="views"></a>보기

보기에서 발견 되는 `App/views` 폴더입니다.

### <a name="shellhtml"></a>shell.html

`shell.html` HTML에 대 한 마스터 레이아웃을 포함 합니다. 다른 보기의 모든 작성 되는 곳 쪽에 프로그램 `shell` 보기. 핫 수건 제공는 `shell` 이러한 3 개의 영역으로: 헤더, 콘텐츠 영역 및 바닥글입니다. 이러한 각 지역와 함께 로드 됩니다 내용을 요청 될 때 다른 보기를 형성 합니다.

`compose` 머리글 및 바닥글에 대 한 바인딩을 하드 코드 되지를 가리키도록 핫 수건에는 `nav` 및 `footer` 각각 봅니다. 섹션에 대 한 작성 바인딩을 `#content` 바인딩되는 `router` 모듈의 활성 항목. 즉,를 클릭할 때 해당 보기가 탐색 링크를이 영역에 로드 됩니다.

[!code-html[Main](hottowel-template/samples/sample4.html)]

### <a name="navhtml"></a>nav.html

`nav.html` 는 SPA에 대 한 탐색 링크를 포함 합니다. 메뉴 구조 배치할 수 있는 위치, 예를 들어입니다. 자주이 통해 데이터 바인딩된 (Knockout 사용)는 `router` 모듈에 정의 된 탐색을 표시 하는 `shell.js`합니다. 데이터 바인딩 특성 및이를 바인딩합니다 knockout 찾습니다는 `shell` viewmodel 탐색 경로 표시 하 고 progressbar (Twitter 부트스트랩 사용)을 표시 하기 경우는 `router` 하나의 뷰에서 다른 (참조 탐색 중에 모듈은 `router.isNavigating`).

[!code-html[Main](hottowel-template/samples/sample5.html)]

### <a name="homehtml-and-detailshtml"></a>home.html 및 details.html

이러한 뷰는 사용자 지정 보기에 대 한 HTML을 포함합니다. 때는 `home` 연결에 `nav` 보기의 메뉴를 클릭 하면는 `home` 보기의 콘텐츠 영역에 표시 됩니다는 `shell` 보기. 이러한 뷰를 확장 또는 사용자 지정 보기 아래 템플릿으로 바뀝니다 수 있습니다.

### <a name="footerhtml"></a>footer.html

`footer.html` 바닥글의 맨 아래에 표시 되는 HTML이 포함 되어는 `shell` 보기.

## <a name="viewmodels"></a>Viewmodel

Viewmodel에서 발견 되는 `App/viewmodels` 폴더입니다.

### <a name="shelljs"></a>shell.js

`shell` viewmodel 포함 속성 및 함수에 바인딩되는 `shell` 보기. 메뉴 탐색 바인딩을 발견 되 이름인 경우가 많습니다 (참조는 `router.mapNav` 논리).

[!code-javascript[Main](hottowel-template/samples/sample6.js)]

### <a name="homejs-and-detailsjs"></a>home.js 및 details.js

이러한 viewmodel 포함 속성 및 함수에 바인딩되는 `home` 보기. 또한 보기에 대 한 프레젠테이션 논리를 포함 하 고 데이터와 뷰 간에 작업은 합니다.

[!code-javascript[Main](hottowel-template/samples/sample7.js)]

## <a name="services"></a>서비스

서비스 응용 프로그램/서비스 폴더에 있습니다. 이상적으로 가져오고 원격 데이터를 게시 하는 일을 담당 하는 dataservice 모듈과 같은 향후 서비스를 배치할 수 있습니다.

### <a name="loggerjs"></a>logger.js

핫 수건 제공는 `logger` 서비스 폴더에는 모듈입니다. `logger` 모듈 로깅 메시지를 콘솔 및 알림 팝업에서 사용자에 게 이상적입니다.
