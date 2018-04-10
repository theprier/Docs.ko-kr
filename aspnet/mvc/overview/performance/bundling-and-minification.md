---
uid: mvc/overview/performance/bundling-and-minification
title: 묶음 및 축소 | Microsoft Docs
author: Rick-Anderson
description: 묶음 및 축소는 다음 두 가지 기술 요청 부하 시간을 개선 하기 위해 ASP.NET 4.5에서 사용할 수 있습니다. 묶음 및 축소 reducin 여 로드 시간 개선 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/23/2012
ms.topic: article
ms.assetid: 5894dc13-5d45-4dad-8096-136499120f1d
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/performance/bundling-and-minification
msc.type: authoredcontent
ms.openlocfilehash: 001ebf89cda66a50cddcd7e4944f27b9396d4450
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2018
---
<a name="bundling-and-minification"></a>묶음 및 축소
====================
으로 [Rick Anderson](https://github.com/Rick-Anderson)

> 묶음 및 축소는 다음 두 가지 기술 요청 부하 시간을 개선 하기 위해 ASP.NET 4.5에서 사용할 수 있습니다. 묶음 및 축소 서버에 요청 수를 줄이면 및 (예: CSS 및 JavaScript.) 요청 된 자산의 크기 감소 하 여 로드 시간 개선


수를 제한 하는 대부분의 현재 주요 브라우저 [동시 연결](http://www.browserscope.org/?category=network) 당 6 개의 각 호스트 이름입니다. 즉, 처리 되는 6 개의 요청 하는 동안 호스트에는 자산에 대 한 추가 요청은 브라우저에서 대기 됩니다. 아래 그림에서는 IE F12 개발자 도구 네트워크 탭에서는 샘플 응용 프로그램의 정보 보기에 필요한 자산에 대 한 타이밍을 보여 줍니다.

![M B /](bundling-and-minification/_static/image1.png)

회색 막대는 6 개 연결 제한에서 대기 하는 브라우저에서 요청은 큐에 대기 시간을 표시 합니다. 노란색 막대는 첫 번째 바이트에는 요청 시간 즉, 요청을 보내고 서버에서 첫 번째 응답을 수신 하는 데 걸린 시간입니다. 파란색 막대는 서버에서 응답 데이터를 수신 하는 데 걸린 시간을 표시 합니다. 자세한 타이밍 정보를 얻으려면 자산에 대해 두 번 클릭 수 있습니다. 다음 이미지는 로드에 대 한 타이밍 정보를 표시 하는 예를 들어는 */Scripts/MyScripts/JavaScript6.js* 파일입니다.

![](bundling-and-minification/_static/image2.png)

위의 그림과 **시작** 동시 연결 수를 제한 하는 요청 브라우저 인해 큐에 지정 된 시간을 제공 하는 이벤트입니다. 이 경우 요청 46 밀리초 다른 요청을 완료를 기다리는 동안 대기한 날짜입니다.

## <a name="bundling"></a>번들

번들은 결합 하거나 단일 파일에 여러 파일을 번들로 쉽게 수 있도록 ASP.NET 4.5의 새로운 기능입니다. CSS, JavaScript 및 다른 번들을 만들 수 있습니다. 파일 수를 줄인 있고 더 적은 HTTP 요청에 첫 번째 페이지 로드 성능을 향상 시킬 수를 의미 합니다.

다음 이미지는 이전에 있지만이 이번에는 묶음 및 축소를 사용할 수를 표시 된 정보 보기의 동일한 타이밍 보기를 표시 합니다.

![](bundling-and-minification/_static/image3.png)

## <a name="minification"></a>축소

다양 한 스크립트 또는 불필요 한 공백 및 메모를 제거 하 고 한 문자를 변수 이름을 단축 같은 css 서로 다른 코드 최적화를 수행 하는 축소 합니다. 다음 JavaScript 함수를 살펴보세요.

[!code-javascript[Main](bundling-and-minification/samples/sample1.js)]

축소 후 함수가 다음과 감소 됩니다.

[!code-javascript[Main](bundling-and-minification/samples/sample2.js)]

주석 및 불필요 한 공백을 제거 하는 것 외에도 다음 매개 변수 및 변수 이름은 열의 이름을 (축약 됨) 다음과 같습니다.

| **원문 언어** | **이름이 변경** |
| --- | --- |
| imageTagAndImageID | n |
| imageContext | t |
| imageElement | i |

## <a name="impact-of-bundling-and-minification"></a>번들의 영향 및 축소

다음 표에서 모든 자산을 개별적으로 나열 하 고 샘플 프로그램에서 묶음 및 축소 (B/M)를 사용 하 여 간의 몇 가지 중요 한 차이점을 보여 줍니다.

|  | **M B/를 사용 하 여** | **M B/없이** | **Change** |
| --- | --- | --- | --- |
| **파일 요청** | 10 | 34 | 256% |
| **보낸 KB** | 3.26 | 11.92 | 266% |
| **받은 KB** | 388.51 | 530 | 36% |
| **로드 시간** | 510 MS | 780 MS | 53% |

보낸 바이트 브라우저 요청에 적용 되는 HTTP 헤더와 매우 자세한 정보는 번들 소프트웨어 크게 감소를 했습니다. 수신된 된 바이트 감소 크게있지 않습니다 때문에 가장 큰 파일 (*Scripts\jquery-ui-1.8.11.min.js* 및 *Scripts\jquery-1.7.1.min.js*) 이미 축소 됩니다. 참고: 샘플 프로그램 사용에 대해 타이밍은 [Fiddler](http://www.fiddler2.com/fiddler2/) 느린 네트워크를 시뮬레이션 하는 도구입니다. (에서 Fiddler에서 **규칙** 메뉴 선택 **성능** 다음 **모뎀 속도 시뮬레이션**.)

## <a name="debugging-bundled-and-minified-javascript"></a>번들로 제공 하 고 축소 JavaScript 디버깅

개발 환경에서 JavaScript를 디버깅 하는 것이 쉽습니다 (여기서는 [compilation 요소](https://msdn.microsoft.com/library/s10awwz0.aspx) 에 *Web.config* 파일으로 설정 되어 `debug="true"` ) JavaScript 파일은 하지 번들로 묶여 있으므로 또는 축소 합니다. JavaScript 파일은 번들로 제공 하 고 축소 릴리스 빌드를 디버그할 수 있습니다. 다음 방법을 사용 하 여 축소 된 번들에 포함 된 JavaScript 함수를 디버깅 IE F12 개발자 도구를 사용 하 여:

1. 선택 된 **스크립트** 탭을 선택한 다음는 **디버깅을 시작** 단추입니다.
2. 자산 단추를 사용 하 여 디버깅 하려면 JavaScript 함수를 포함 하는 번들을 선택 합니다.  
    ![](bundling-and-minification/_static/image4.png)
3. 선택 하 여 축소 된 JavaScript 형식을 **구성 단추** ![](bundling-and-minification/_static/image5.png), 다음을 선택 하 고 **형식 JavaScript**합니다.
4. 에 **검색 스크립트** t 입력된 상자에서 디버깅할 함수 이름을 선택 합니다. 다음 그림에 **AddAltToImg** 에 입력 된는 **검색 스크립트** t 입력된 상자.  
    ![](bundling-and-minification/_static/image6.png)

F12 개발자 도구를 사용 하 여 디버깅에 대 한 자세한 내용은 MSDN 문서를 참조 하십시오. [JavaScript 오류 디버그를 F12 개발자 도구를 사용 하 여](https://msdn.microsoft.com/library/ie/gg699336(v=vs.85).aspx)합니다.

## <a name="controlling-bundling-and-minification"></a>제어 묶음 및 축소

묶음 및 축소를 사용 하도록 설정 하거나에서 디버그 특성의 값을 설정 하 여 사용할 수는 [compilation 요소](https://msdn.microsoft.com/library/s10awwz0.aspx) 에 *Web.config* 파일입니다. 다음 xml에서 `debug` 가 있으므로 true로 설정 묶음 및 축소를 사용 하지 않도록 설정 합니다.

[!code-xml[Main](bundling-and-minification/samples/sample3.xml?highlight=2)]

묶음 및 축소를 사용 하려면 설정는 `debug` 값을 "false"입니다. 재정의할 수 있습니다는 *Web.config* 사용 하 여 설정 된 `EnableOptimizations` 속성에는 `BundleTable` 클래스. 다음 코드에서는 묶음 및 축소를 사용 하도록 설정 하 고의 모든 설정을 재정의 *Web.config* 파일입니다.

[!code-csharp[Main](bundling-and-minification/samples/sample4.cs?highlight=7)]

> [!NOTE]
> 하지 않는 한 `EnableOptimizations` 은 `true` 또는 디버그 특성에는 [compilation 요소](https://msdn.microsoft.com/library/s10awwz0.aspx) 에 *Web.config* 파일으로 설정 되어 `false`, 파일을 번들로 제공 되거나 축소 되지 것입니다. 또한.min 버전의 파일 사용 되지 않습니다, 그리고 전체 디버그 버전을 선택 됩니다. `EnableOptimizations` 디버그 특성이 재정의 [compilation 요소](https://msdn.microsoft.com/library/s10awwz0.aspx) 에 *Web.config* 파일


## <a name="using-bundling-and-minification-with-aspnet-web-forms-and-web-pages"></a>번들을 사용 하 여 및 ASP.NET Web Forms 및 웹 페이지 축소

- 웹 페이지에 대 한 블로그 항목을 참조 [웹 페이지 사이트에 추가 웹 최적화](https://blogs.msdn.com/b/rickandy/archive/2012/08/15/adding-web-optimization-to-a-web-pages-site.aspx)합니다.
- Web Forms, 블로그 항목을 참조 하십시오. [추가 묶음 및 축소를 Web Forms](https://blogs.msdn.com/b/rickandy/archive/2012/08/14/adding-bundling-and-minification-to-web-forms.aspx)합니다.

## <a name="using-bundling-and-minification-with-aspnet-mvc"></a>번들을 사용 하 여 및 ASP.NET MVC와 함께 축소

이 섹션의 번들을 검사 하는 프로젝트 및 축소는 ASP.NET MVC를 만듭니다. ASP.NET MVC 인터넷 이라는 새 프로젝트를 먼저 만듭니다 **MvcBM** 기본값을 변경 하지 않고 있습니다.

열기는 *앱\_Start\BundleConfig.cs* 파일 및 검사는 `RegisterBundles` 만들고, 등록, 번들을 구성 하는 데 사용 되는 메서드. 다음 코드의 일부를 보여 줍니다.는 `RegisterBundles` 메서드.

[!code-csharp[Main](bundling-and-minification/samples/sample5.cs)]

위의 코드 만듭니다 라는 새 JavaScript 번들 *~/bundles/jquery* 적절 한 포함 된 (디버그 되거나 축소 되지 않은 하. *vsdoc*) 파일에 *스크립트* 와일드 카드 문자열 "{버전} ~/Scripts/jquery-.js"와 일치 하는 폴더입니다. ASP.NET MVC 4, 즉 디버그 구성을 사용 하면 파일 *jquery 1.7.1.js* 번들에 추가 됩니다. 릴리스 구성에서 *jquery 1.7.1.min.js* 추가 됩니다. 번들 프레임 워크와 같은 몇 가지 일반적인 규칙을 따릅니다.

- "FileX.min.js"와 "FileX.js" 있을 때 릴리스에 대 한 ".min" 파일을 선택 합니다.
- 디버그에 대 한 비 ".min" 버전을 선택 합니다.
- 무시 하 고 "-vsdoc" IntelliSense에만 사용 되는 파일 (예: jquery-1.7.1-vsdoc.js) 합니다.

`{version}` 위에 표시 된 와일드 카드 일치 하는 데 자동으로 적절 한 버전의 jQuery의 jQuery 번들을 만들 프로그램 *스크립트* 폴더입니다. 이 예제에서는 와일드 카드를 사용 하 여 다음과 같은 이점이 있습니다.

- NuGet을 사용 하 여 위의 묶는 것 코드 또는 보기 페이지에서 jQuery 참조를 변경 하지 않고 새 jQuery 버전으로 업데이트할 수 있습니다.
- 자동으로 선택 릴리스에 대 한 ".min" 버전과 디버그 구성에 대 한 전체 버전 작성 합니다.

## <a name="using-a-cdn"></a>CDN을 사용 하 여

 다음 코드에서는 로컬 jQuery 번들을 CDN jQuery 번들 바꿉니다.

[!code-csharp[Main](bundling-and-minification/samples/sample6.cs)]

위의 코드에서 릴리스에서 모드 및 jQuery의 디버그 버전에 인출 되는 로컬로 디버그 모드에서 동안 CDN에서 jQuery는 요청 합니다. CDN을 사용할 경우 CDN 요청이 실패 하는 경우 대체 메커니즘이 있어야 합니다. JQuery 해야 CDN 실패 요청에 추가 레이아웃 파일에서는 스크립트의 끝에서 조각 내에 다음 태그 합니다.

[!code-cshtml[Main](bundling-and-minification/samples/sample7.cshtml?highlight=5-13)]

## <a name="creating-a-bundle"></a>번들 만들기

[번들](https://msdn.microsoft.com/library/system.web.optimization.bundle(v=VS.110).aspx) 클래스 `Include` 메서드 여기서 각 문자열은 리소스의 가상 경로 문자열의 배열을 사용 합니다. RegisterBundles 메서드에서 다음 코드는 *앱\_Start\BundleConfig.cs* 파일에 여러 개의 파일은 번들에 추가 표시:

[!code-csharp[Main](bundling-and-minification/samples/sample8.cs)]

[번들](https://msdn.microsoft.com/library/system.web.optimization.bundle(v=VS.110).aspx) 클래스 `IncludeDirectory` 메서드 검색 패턴과 일치 하는 디렉터리 (및 필요에 따라 모든 하위 디렉터리)의 모든 파일을 추가 하기 위해 제공 됩니다. [번들](https://msdn.microsoft.com/library/system.web.optimization.bundle(v=VS.110).aspx) 클래스 `IncludeDirectory` API는 다음과 같습니다.

[!code-csharp[Main](bundling-and-minification/samples/sample9.cs)]

번들 Render 메서드를 사용 하 여 뷰에서 참조 됩니다 ( `Styles.Render` CSS에 대 한 및 `Scripts.Render` JavaScript에 대 한). 다음 태그는 *Views\Shared\\_Layout.cshtml* 파일은 기본 ASP.NET 인터넷 프로젝트 뷰 CSS 및 JavaScript 번들을 참조 하는 방법을 보여 줍니다.

[!code-cshtml[Main](bundling-and-minification/samples/sample10.cshtml?highlight=5-6,11)]

Render 메서드 코드 한 줄에 여러 번들을 추가할 수 있도록 문자열의 배열을 사용을 확인 합니다. 일반적으로 자산을 참조 하는 데 필요한 HTML을 생성 하는 렌더링 방법을 사용 합니다. 사용할 수는 `Url` 자산을 참조 하는 데 필요한 태그 없이 자산에 대 한 URL을 생성 하는 메서드. 새 HTML5 사용 하려는 경우를 가정해 볼 [비동기](http://www.whatwg.org/specs/web-apps/current-work/#attr-script-async) 특성입니다. 다음 코드에서는 modernizr를 사용 하 여 참조 하는 방법을 보여 줍니다.는 `Url` 메서드.

[!code-cshtml[Main](bundling-and-minification/samples/sample11.cshtml?highlight=11)]

## <a name="using-the--wildcard-character-to-select-files"></a>사용 하는 "\*" 파일을 선택 하려면 와일드 카드 문자

에 지정 된 가상 경로 `Include` 메서드와 검색 패턴에 `IncludeDirectory` 메서드 하나를 사용할 수 "\*" 접두사 또는 접미사를 마지막 경로 세그먼트에 와일드 카드 문자입니다. 검색 문자열은 대/소문자 구분 합니다. `IncludeDirectory` 메서드에 하위 디렉터리를 검색 하는 옵션이 있습니다.

다음 JavaScript 파일이 프로젝트 있다고 가정 합니다.

- *Scripts\Common\AddAltToImg.js*
- *Scripts\Common\ToggleDiv.js*
- *Scripts\Common\ToggleImg.js*
- *Scripts\Common\Sub1\ToggleLinks.js*

![dir imag](bundling-and-minification/_static/image7.png)

다음 표에서 같이 와일드 카드를 사용 하는 번들에 추가 된 파일을 보여 줍니다.

| **Call** | **추가 된 파일 또는 예외 발생** |
| --- | --- |
| Include("~/Scripts/Common/\*.js") | *AddAltToImg.js, ToggleDiv.js, ToggleImg.js* |
| Include("~/Scripts/Common/T\*.js") | 잘못 된 패턴 예외입니다. 와일드 카드 문자는 접두사 또는 접미사에만 사용할 수 있습니다. |
| Include("~/Scripts/Common/\*og.\*") | 잘못 된 패턴 예외입니다. 하나의 와일드 카드 문자는 사용할 수 있습니다. |
| "Include("~/Scripts/Common/T\*") | *ToggleDiv.js, ToggleImg.js* |
| "Include("~/Scripts/Common/\*") | 잘못 된 패턴 예외입니다. 순수 와일드 카드 세그먼트가 잘못 되었습니다. |
| IncludeDirectory("~/Scripts/Common", "T\*") | *ToggleDiv.js, ToggleImg.js* |
| IncludeDirectory("~/Scripts/Common", "T\*",true) | *ToggleDiv.js, ToggleImg.js, ToggleLinks.js* |

각 파일 번들을 명시적으로 추가 하는 것이 일반적으로 좋습니다 통해 다음과 같은 이유로 파일의 와일드 카드 로드 합니다.

- 일반적으로 결과 원하지는 알파벳 순서로 로드 하기 와일드 카드 기본적으로 스크립트에 추가 합니다. 자주 CSS 및 JavaScript 파일 (-알파벳 이외의)은 특정 순서에 추가 해야 합니다. 사용자 지정을 추가 하 여이 위험을 줄일 수 있습니다 [IBundleOrderer](https://msdn.microsoft.com/library/system.web.optimization.ibundleorderer(VS.110).aspx) 구현 하지만 각 파일은 오류 발생 가능성을 명시적으로 추가 합니다. 예를 들어 나중에 폴더를 수정 해야 할 수 있는 새 자산을 추가할 수 있습니다 프로그램 [IBundleOrderer](https://msdn.microsoft.com/library/system.web.optimization.ibundleorderer(VS.110).aspx) 구현 합니다.
- 특정 파일 보기를 로드 하는 와일드 카드를 사용 하 여 디렉터리에 추가 된 해당 번들 참조 하는 모든 보기에 포함할 수 있습니다. 번들에 특정 스크립트 보기를 추가 하는 경우 뷰를 다른 뷰에 번들을 참조 하는 JavaScript 오류가 발생할 수 있습니다.
- CSS 파일에 다른 파일을 두 번 로드 하는 가져온 파일에서 발생 합니다. 예를 들어 다음 코드는 대부분 두 번 로드 jQuery UI 테마 CSS 파일의 번들을 만듭니다. 

    [!code-csharp[Main](bundling-and-minification/samples/sample12.cs)]

  와일드 카드 선택기 "\*.css" 폴더에서 각 CSS 파일에는 포함 하는 *Content\themes\base\jquery.ui.all.css* 파일입니다. *jquery.ui.all.css* 파일은 다른 CSS 파일을 가져옵니다.

## <a name="bundle-caching"></a>캐싱 번들

번들은 HTTP Expires 헤더 1 년에서 번들을 만들 때 설정 합니다. Fiddler 표시 IE에는 번들에 대 한 조건부 요청 수 없습니다. 이전에 본 페이지로 이동 하면 즉, 많은 경우의 번들에 대 한 IE에서 HTTP GET 요청이 없으면 및 서버에서 HTTP 304 응답 합니다. IE (각 번들에 대 한 HTTP 304 응답 발생 함)는 F5 키를 가진 각 번들에 대 한 조건부 요청을 적용할 수 있습니다. 사용 하 여 전체 새로 고침을 강제로 수 ^ F5 (각 번들에 대 한 HTTP 200 응답으로 인해 발생 합니다.)

다음 그림에서는 **캐싱** Fiddler 응답 창의 탭:

![fiddler 캐싱 이미지](bundling-and-minification/_static/image8.png)

요청   
`http://localhost/MvcBM_time/bundles/AllMyScripts?v=r0sLDicvP58AIXN_mc3QdyVvVj5euZNzdsa2N1PKvb81`  
 번들은 **AllMyScripts** 쿼리 문자열 쌍을 포함 하 고 **v r0sLDicvP58AIXN =\_mc3QdyVvVj5euZNzdsa2N1PKvb81**합니다. 쿼리 문자열 **v** 값 토큰 캐시에 사용 되는 고유 식별자입니다. ASP.NET 응용 프로그램 요청으로 번들 변경 되지 않습니다는 **AllMyScripts** 이 토큰을 사용 하 여 번들입니다. 번들에 모든 파일이 변경 되 면 ASP.NET 최적화 프레임 워크는 번들에 대 한 브라우저 요청 최신 번들을 받게 됩니다를 보장 하는 새 토큰을 생성 합니다.

IE9 F12 개발자 도구를 실행 하 고 이전에 로드 된 페이지를 탐색 하는 경우 IE 잘못 표시 각 번들 및 HTTP 304 반환 하는 서버에 대 한 조건부 GET 요청 합니다. IE9 조건부 요청에서 블로그 항목 여부를 확인 하는 문제에 이유를 읽을 수 [를 사용 하 여 Cdn 및 웹 사이트 성능 향상을 Expires](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx)합니다.

## <a name="less-coffeescript-scss-sass-bundling"></a>덜, CoffeeScript, SCSS, 번들 Sass 합니다.

묶음 및 축소 프레임 워크와 같은 중간 언어를 처리 하는 메커니즘을 제공 [SCSS](http://sass-lang.com/), [Sass](http://sass-lang.com/), [적은](http://www.dotlesscss.org/) 또는 [Coffeescript ](http://coffeescript.org/), 결과 번들에 축소와 같은 변환을 적용 하 고 있습니다. 예를 들어, 추가할 [.less](http://www.dotlesscss.org/) MVC 4 프로젝트에 파일:

1. 덜 콘텐츠에 대 한 폴더를 만듭니다. 다음 예제에서는 *Content\MyLess* 폴더입니다.
2. 추가 [.less](http://www.dotlesscss.org/) NuGet 패키지 **점이 없는** 프로젝트에 있습니다.  
    ![NuGet 점이 없는 설치](bundling-and-minification/_static/image9.png)
3. 구현 하는 클래스를 추가 [IBundleTransform](https://msdn.microsoft.com/library/system.web.optimization.ibundletransform(VS.110).aspx) 인터페이스입니다. .Less 변환에 대 한 프로젝트에 다음 코드를 추가 합니다.

    [!code-csharp[Main](bundling-and-minification/samples/sample13.cs)]
4. 덜 사용 하 여 파일의 번들을 만든는 `LessTransform` 및 [CssMinify](https://msdn.microsoft.com/library/system.web.optimization.cssminify(VS.110).aspx) 변환 합니다. 다음 코드를 추가 하는 `RegisterBundles` 에서 메서드는 *앱\_Start\BundleConfig.cs* 파일입니다.

    [!code-csharp[Main](bundling-and-minification/samples/sample14.cs)]
5. 덜 번들 참조 하는 모든 보기에 다음 코드를 추가 합니다.

    [!code-cshtml[Main](bundling-and-minification/samples/sample15.cshtml)]

## <a name="bundle-considerations"></a>번들 고려 사항

번들을 만들 때 따라야 하는 좋은 규칙 번들 이름에는 접두사로 "번들"를 포함 하는 것입니다. 이렇게 하면 가능한 [라우팅 충돌](https://forums.asp.net/post/5012037.aspx)합니다.

번들의 파일을 업데이트 한 후에 새 토큰 번들 쿼리 문자열 매개 변수 생성 되 고 전체 번들에는 클라이언트가 요청 번들을 포함 하는 페이지 다음에 다운로드 해야 합니다. 각 자산 개별적으로 나열 됩니다는 기존 태그에서 변경 된 파일만 다운로드할 지 합니다. 자산 자주 변경 되는 번들에 대 한 적절 한 후보를 아닐 수 있습니다.

묶음 및 축소는 주로 첫 번째 페이지 요청 부하 시간을 개선 합니다. 브라우저 캐시 자산 (JavaScript, CSS 및 이미지) 웹 페이지를 요청 되 면 페이지는 동일한 사이트 자산과 동일한 요청 하거나 묶음 및 축소 같은 페이지를 요청할 때 모든 성능 향상을 제공 하지 않습니다. 설정 하지 않으면는 사용자의 자산에서 올바르게 헤더 만료 묶음 및 축소를 사용 하지 않는, 브라우저 새로 고침 추론 됩니다 자산 부실 몇 일 후 약관을 표시할 브라우저 각 자산에 대 한 유효성 검사 요청을 해야 합니다. 이 경우 묶음 및 축소 첫 번째 페이지 요청 후 성능 향상을 제공합니다. 자세한 내용은 블로그를 참조 하십시오. [를 사용 하 여 Cdn 및 웹 사이트 성능 향상을 Expires](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx)합니다.

각 호스트 이름 당 동시 연결 수 6 개의 브라우저 제한을 사용 하 여 완화할 수 있습니다는 [CDN](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx)합니다. CDN은 서로 다른 호스트 이름 호스팅 사이트 보다 더 자산 CDN에서에서 요청에 호스팅 환경에는 6 개의 동시 연결 제한 수는 없습니다. 일반적인 패키지 캐싱 및 캐싱 장점 가장자리 CDN 제공할 수도 있습니다.

번들을 필요로 하는 페이지에서 분할 합니다. 예를 들어 기본 인터넷 응용 프로그램에 대 한 ASP.NET MVC 템플릿에서 만듭니다 jQuery 유효성 검사 번들 jQuery 별개입니다. 생성 되는 기본 보기에는 입력 하지 않고 있으며 값을 게시 하지 마십시오, 때문에 유효성 검사 번들을 포함 하지 않습니다.

`System.Web.Optimization` 네임 스페이스 System.Web.Optimization.DLL에서 구현 됩니다. 활용 WebGrease 라이브러리 (WebGrease.dll) 축소 기능을 차례로 Antlr3.Runtime.dll를 사용 하 여 합니다.

*Twitter 빠른 게시물 링크와 공유 하 고 사용 합니다. 내 Twitter 핸들은*: [@RickAndMSFT](http://twitter.com/RickAndMSFT)

## <a name="additional-resources"></a>추가 자료

- 비디오:[묶음 및 최적화](https://channel9.msdn.com/Events/aspConf/aspConf/Bundling-and-Optimizing) 여 [Howard Dierking](https://twitter.com/#!/howard_dierking)
- [웹 페이지 사이트에 웹 최적화 추가](https://blogs.msdn.com/b/rickandy/archive/2012/08/15/adding-web-optimization-to-a-web-pages-site.aspx)합니다.
- [추가 묶음 및 축소를 Web Forms](https://blogs.msdn.com/b/rickandy/archive/2012/08/14/adding-bundling-and-minification-to-web-forms.aspx)합니다.
- [번들의 성능에 미치는 영향 및 웹 검색에 축소](https://blogs.msdn.com/b/henrikn/archive/2012/06/17/performance-implications-of-bundling-and-minification-on-http.aspx) 여 [구재석 F Nielsen](http://en.wikipedia.org/wiki/Henrik_Frystyk_Nielsen) [@frystyk](https://twitter.com/frystyk)
- [Cdn을 사용 하 여 웹 사이트 성능 향상을 위해 만료 되 고](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx) Rick anderson [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)
- [최소화 RTT (왕복 시간)](https://developers.google.com/speed/docs/best-practices/rtt)

## <a name="contributors"></a>참가자

- Hao 둘러싼
- [Howard Dierking](https://twitter.com/#!/howard_dierking)
- Diana LaRose
