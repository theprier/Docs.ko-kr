---
uid: mvc/overview/performance/bundling-and-minification
title: 묶음 및 축소 | Microsoft Docs
author: Rick-Anderson
description: 묶음 및 축소는 두 가지 기술을 요청 로드 시간을 개선 하기 위해 ASP.NET 4.5에서 사용할 수 있습니다. 묶음 및 축소 reducin 여 로드 시간을 개선 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/23/2012
ms.topic: article
ms.assetid: 5894dc13-5d45-4dad-8096-136499120f1d
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/performance/bundling-and-minification
msc.type: authoredcontent
ms.openlocfilehash: 4f21184f0917cd957e9e1719c63769e1a027961c
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37384783"
---
<a name="bundling-and-minification"></a>묶음 및 축소
====================
[Rick Anderson](https://github.com/Rick-Anderson)

> 묶음 및 축소는 두 가지 기술을 요청 로드 시간을 개선 하기 위해 ASP.NET 4.5에서 사용할 수 있습니다. 묶음 및 축소 서버 요청의 수를 줄이고 요청 된 자산 (예: CSS 및 JavaScript)의 크기를 줄이면 하 여 로드 시간 개선


대부분의 현재 주요 브라우저의 수를 제한 [동시 연결](http://www.browserscope.org/?category=network) 당 6 개의 각 호스트 이름입니다. 즉, 처리 되는 6 개의 요청 하는 동안 호스트에서 자산에 대 한 추가 요청은 브라우저에서 대기 됩니다. 아래 이미지에서 IE F12 개발자 도구 네트워크 탭에서는 샘플 응용 프로그램 정보 보기에 필요한 자산에 대 한 타이밍을 보여 줍니다.

![B/M](bundling-and-minification/_static/image1.png)

회색 막대 6 연결 제한을 대기 하는 브라우저에서 요청은 큐에 대기 시간을 표시 합니다. 노란색 막대는 첫 번째 바이트 까지의 요청 시간, 요청을 보내고 서버에서 첫 번째 응답을 수신 하는 데 걸리는 시간입니다. 파란색 막대 서버에서 응답 데이터를 수신 하는 데 걸리는 시간을 표시 합니다. 자세한 타이밍 정보를 가져오려면 자산에 두 번 클릭 수 있습니다. 예를 들어, 다음 이미지는 로드에 대 한 타이밍 정보를 표시 합니다 */Scripts/MyScripts/JavaScript6.js* 파일입니다.

![](bundling-and-minification/_static/image2.png)

위의 그림과 합니다 **시작** 브라우저 때문에 요청이 대기한 시간을 제공 하는 동시 연결 수를 제한 하는 이벤트입니다. 이 경우 요청 다른 요청이 완료 되기를 기다리는 46 밀리초 동안 대기한 날짜입니다.

## <a name="bundling"></a>번들

번들을 쉽게 결합 하 여 단일 파일에 여러 파일을 번들에 ASP.NET 4.5의 새로운 기능입니다. CSS, JavaScript 및 기타 번들을 만들 수 있습니다. 파일 수가 적으면 하 고 더 적은 수의 HTTP 요청에 첫 번째 페이지 로드 성능을 향상 시킬 수 있습니다 의미 합니다.

다음 이미지는 이전에 하지만이 이번 묶음 및 축소 설정에 표시 된 정보 보기의 동일한 타이밍 보기를 보여줍니다.

![](bundling-and-minification/_static/image3.png)

## <a name="minification"></a>축소

축소는 다양 한 스크립트 또는 불필요 한 공백 및 메모를 제거 하 고 변수 이름의 문자 하나를 줄여 같은 css 다른 코드 최적화를 수행 합니다. 다음 JavaScript 함수를 고려해 야 합니다.

[!code-javascript[Main](bundling-and-minification/samples/sample1.js)]

축소 후 함수는 다음과 감소 됩니다.

[!code-javascript[Main](bundling-and-minification/samples/sample2.js)]

주석 및 불필요 한 공백을 제거 하는 것 외에도 다음 매개 변수 및 변수 이름을 바뀌었습니다 (단축) 다음과 같이 합니다.

| **원문 언어** | **이름이** |
| --- | --- |
| imageTagAndImageID | n |
| imageContext | t |
| imageElement | i |

## <a name="impact-of-bundling-and-minification"></a>번들의 영향 및 축소

다음 표에서 모든 자산을 개별적으로 나열 하 고 샘플 프로그램의 묶음 및 축소 (B/M)를 사용 하 여 간의 몇 가지 중요 한 차이점을 보여 줍니다.

|  | **B/M을 사용 하 여** | **B/M 없이** | **변경** |
| --- | --- | --- | --- |
| **파일 요청** | 10 | 34 | 256% |
| **전송 (kb)** | 3.26 | 11.92 | 266% |
| **수신 (kb)** | 388.51 | 530 | 36% |
| **로드 시간** | 510 MS | 780 MS | 53% |

보낸 바이트 수에는 브라우저 요청에 적용 되는 HTTP 헤더를 사용 하 여 매우 자세한 정보는 번들 상당히 감소를 했습니다. 수신된 바이트 수를 줄이는으로 크지 않습니다. 때문에 가장 큰 파일 (*Scripts\jquery-ui-1.8.11.min.js* 하 고 *Scripts\jquery-1.7.1.min.js*) 이미 축소 됩니다. 참고: 사용 하는 샘플 프로그램에 타이밍 합니다 [Fiddler](http://www.fiddler2.com/fiddler2/) 느린 네트워크를 시뮬레이션 하는 도구입니다. (의 Fiddler에서 **규칙** 메뉴에서 **성능** 한 다음 **모뎀 속도 시뮬레이션**.)

## <a name="debugging-bundled-and-minified-javascript"></a>번들 및 축소 JavaScript 디버깅

개발 환경에서 JavaScript를 디버깅 하는 것이 쉽습니다 (여기서는 [compilation 요소](https://msdn.microsoft.com/library/s10awwz0.aspx) 에 *Web.config* 파일을 설정 `debug="true"` ) JavaScript 파일에 포함 되지는 않습니다 때문에 또는 축소 합니다. 또한 JavaScript 파일은 번들 및 축소는 릴리스 빌드를 디버그할 수 있습니다. IE F12 개발자 도구를 사용 하는 다음 방법을 사용 하 여 축소 된 번들에 포함 하는 JavaScript 함수 디버깅할:

1. 선택 합니다 **스크립트** 탭을 선택한 다음는 **디버깅을 시작할** 단추입니다.
2. 자산 단추를 사용 하 여 디버그 하려는 JavaScript 함수를 포함 하는 번들을 선택 합니다.  
    ![](bundling-and-minification/_static/image4.png)
3. 선택 하 여 축소 된 JavaScript 형식을 **구성 단추** ![](bundling-and-minification/_static/image5.png)를 선택한 다음 **형식을 JavaScript**합니다.
4. 에 **검색 스크립트** t 입력된 상자에서 디버깅할 함수 이름을 선택 합니다. 다음 그림과에서 **AddAltToImg** 에 입력 된 합니다 **검색 스크립트** t 입력란입니다.  
    ![](bundling-and-minification/_static/image6.png)

F12 개발자 도구를 사용 하 여 디버깅 하는 방법은 MSDN 문서를 참조 하세요 [JavaScript 오류 디버그 F12 개발자 도구를 사용 하 여](https://msdn.microsoft.com/library/ie/gg699336(v=vs.85).aspx)입니다.

## <a name="controlling-bundling-and-minification"></a>제어 묶음 및 축소

묶음 및 축소를 사용 하도록 설정 하거나 디버그 특성의 값을 설정 하 여 사용할 수는 [compilation 요소](https://msdn.microsoft.com/library/s10awwz0.aspx) 에 *Web.config* 파일입니다. 다음 xml에서 `debug` 는를 true로 설정 묶음 및 축소를 사용 하지 않도록 설정 합니다.

[!code-xml[Main](bundling-and-minification/samples/sample3.xml?highlight=2)]

묶음 및 축소를 사용 하도록 설정 하려면 설정의 `debug` 값을 "false"입니다. 재정의할 수 있습니다를 *Web.config* 사용 하 여 설정 합니다 `EnableOptimizations` 속성에는 `BundleTable` 클래스. 다음 코드는 묶음 및 축소를 사용 하도록 설정 하 고의 모든 설정을 재정의 합니다 *Web.config* 파일입니다.

[!code-csharp[Main](bundling-and-minification/samples/sample4.cs?highlight=7)]

> [!NOTE]
> 경우가 아니면 `EnableOptimizations` 은 `true` 또는 디버그 특성에는 [compilation 요소](https://msdn.microsoft.com/library/s10awwz0.aspx) 에 *Web.config* 파일을 설정 `false`, 파일을 번들로 제공 되거나 축소 되지 것입니다. 또한.min 버전의 파일 사용 되지 않습니다, 그리고 전체 디버그 버전이 선택 됩니다. `EnableOptimizations` 디버그 특성을 재정의 합니다 [compilation 요소](https://msdn.microsoft.com/library/s10awwz0.aspx) 에 *Web.config* 파일


## <a name="using-bundling-and-minification-with-aspnet-web-forms-and-web-pages"></a>묶음을 사용 하 여 및 ASP.NET Web Forms 및 웹 페이지를 사용 하 여 축소

- 웹 페이지, 블로그 항목을 참조 하세요 [웹 페이지 사이트에 추가 웹 최적화](https://blogs.msdn.com/b/rickandy/archive/2012/08/15/adding-web-optimization-to-a-web-pages-site.aspx)합니다.
- Web Forms에 대 한 블로그 항목을 참조 하세요 [추가 묶음 및 축소 Web forms](https://blogs.msdn.com/b/rickandy/archive/2012/08/14/adding-bundling-and-minification-to-web-forms.aspx)합니다.

## <a name="using-bundling-and-minification-with-aspnet-mvc"></a>묶음을 사용 하 여 ASP.NET MVC를 사용 하 여 축소 하 고

이 섹션의 묶음을 검사 하는 프로젝트 및 축소는 ASP.NET MVC에서는 만들어집니다. 먼저, 명명 된 새 ASP.NET MVC 인터넷 프로젝트를 만듭니다 **MvcBM** 기본값을 변경 하지 않고 있습니다.

엽니다는 *앱\_Start\BundleConfig.cs* 파일을 검사 합니다 `RegisterBundles` 만들기, 등록 및 번들을 구성 하는 데 사용 되는 메서드. 다음 코드의 일부를 보여 줍니다.는 `RegisterBundles` 메서드.

[!code-csharp[Main](bundling-and-minification/samples/sample5.cs)]

위의 코드는 라는 새 JavaScript 번들을 만듭니다 *~/bundles/jquery* 포함 하는 모든 적절 한 (아닌 축소 되거나 디버그는. *vsdoc*)에서 파일을 *스크립트* 와일드 카드 문자열 "~/Scripts/jquery-{version}.js"와 일치 하는 폴더입니다. ASP.NET MVC 4, 즉 디버그 구성의 경우 파일을 사용 하 여 *jquery 1.7.1.js* 번들에 추가 됩니다. 릴리스 구성에서는 *jquery 1.7.1.min.js* 추가 됩니다. 번들 프레임 워크와 같은 몇 가지 일반적인 규칙을 따릅니다.

- "FileX.min.js" 및 "FileX.js" 있으면 릴리스에 대 한 ".min" 파일을 선택 합니다.
- 디버그에 대 한 비 ".min" 버전을 선택합니다.
- 무시 하 고 "-vsdoc" IntelliSense만 사용 되는 파일 (예: jquery-1.7.1-vsdoc.js) 합니다.

합니다 `{version}` 자동으로 적절 한 버전에 jQuery의 jQuery 번들을 만드는 데 사용 됩니다 와일드 카드 위에 표시 된 일치 하 *스크립트* 폴더입니다. 이 예제에서는 와일드 카드를 사용 하 여 다음과 같은 이점이 제공:

- NuGet를 사용 하 여 이전 번들 코드 또는 보기 페이지에 jQuery 참조를 변경 하지 않고 최신 jQuery 버전으로 업데이트할 수 있습니다.
- 자동으로 선택 디버그 구성에 대 한 정식 버전 및 릴리스 ".min" 버전을 빌드합니다.

## <a name="using-a-cdn"></a>CDN을 사용 하 여

 다음 코드는 로컬 jQuery 번들을 CDN의 jQuery 번들 바꿉니다.

[!code-csharp[Main](bundling-and-minification/samples/sample6.cs)]

위의 코드에서 릴리스에서 모드 및 jQuery의 디버그 버전에 인출 되는 로컬에서 디버그 모드에서 동안 CDN에서 jQuery는 요청 합니다. CDN을 사용 하는 경우 CDN 요청이 실패 하는 경우 대체 메커니즘을 있어야 합니다. 다음 태그는 jQuery는 CDN 실패 요청에 추가 레이아웃 파일에서는 스크립트의 끝에서 조각을입니다.

[!code-cshtml[Main](bundling-and-minification/samples/sample7.cshtml?highlight=5-13)]

## <a name="creating-a-bundle"></a>번들 만들기

합니다 [번들](https://msdn.microsoft.com/library/system.web.optimization.bundle(v=VS.110).aspx) 클래스 `Include` 메서드는 여기서 각 문자열은 리소스의 가상 경로 문자열의 배열을 사용 합니다. RegisterBundles 메서드에서 다음 코드를 *앱\_Start\BundleConfig.cs* 파일 번들을 추가할 여러 파일을 보여 줍니다.

[!code-csharp[Main](bundling-and-minification/samples/sample8.cs)]

합니다 [번들](https://msdn.microsoft.com/library/system.web.optimization.bundle(v=VS.110).aspx) 클래스 `IncludeDirectory` 검색 패턴과 일치 하는 디렉터리 (및 필요에 따라 모든 하위 디렉터리)에 있는 모든 파일을 추가할 메서드가 제공 됩니다. 합니다 [번들](https://msdn.microsoft.com/library/system.web.optimization.bundle(v=VS.110).aspx) 클래스 `IncludeDirectory` API는 다음과 같습니다.

[!code-csharp[Main](bundling-and-minification/samples/sample9.cs)]

번들은 렌더링 메서드를 사용 하는 뷰에서 참조 하는 ( `Styles.Render` css 및 `Scripts.Render` JavaScript 용). 다음 태그를 *Views\Shared\\_Layout.cshtml* 파일은 기본 ASP.NET 인터넷 프로젝트 보기 CSS 및 JavaScript 번들을 참조 하는 방법을 보여 줍니다.

[!code-cshtml[Main](bundling-and-minification/samples/sample10.cshtml?highlight=5-6,11)]

코드 한 줄에 여러 번들을 추가할 수 있도록 렌더링 메서드는 문자열 배열을 확인 합니다. 일반적으로 자산을 참조 하는 데 필요한 HTML을 만들기는 렌더링 메서드를 사용 합니다. 사용할 수는 `Url` 자산을 참조 하는 데 필요한 태그 없이 자산에 URL을 생성 하는 방법입니다. 새 HTML5를 사용 하려고 한다고 가정해 보겠습니다 [비동기](http://www.whatwg.org/specs/web-apps/current-work/#attr-script-async) 특성입니다. 다음 코드는 modernizr를 사용 하 여 참조 하는 방법을 보여 줍니다는 `Url` 메서드.

[!code-cshtml[Main](bundling-and-minification/samples/sample11.cshtml?highlight=11)]

## <a name="using-the--wildcard-character-to-select-files"></a>사용 하 여 "\*" 파일을 선택 하려면 와일드 카드 문자

에 지정 된 가상 경로 `Include` 메서드와 검색 패턴에 `IncludeDirectory` 메서드가 하나를 수락할 수 "\*" 접두사 또는 접미사를 마지막 경로 세그먼트에 와일드 카드 문자. 검색 문자열은 대/소문자 구분입니다. `IncludeDirectory` 메서드는 하위 디렉터리를 검색 합니다.

다음 JavaScript 파일을 사용 하 여 프로젝트를 고려 합니다.

- *Scripts\Common\AddAltToImg.js*
- *Scripts\Common\ToggleDiv.js*
- *Scripts\Common\ToggleImg.js*
- *Scripts\Common\Sub1\ToggleLinks.js*

![dir 이미지](bundling-and-minification/_static/image7.png)

다음 표에서 같이 와일드 카드를 사용 하 여 번들에 추가 된 파일을 보여 줍니다.

| **Call** | **추가 된 파일 또는 예외 발생** |
| --- | --- |
| Include("~/Scripts/Common/\*.js") | *AddAltToImg.js, ToggleDiv.js, ToggleImg.js* |
| Include("~/Scripts/Common/T\*.js") | 잘못 된 패턴 예외입니다. 와일드 카드 문자 접두사 또는 접미사에만 허용 됩니다. |
| Include("~/Scripts/Common/\*og.\*") | 잘못 된 패턴 예외입니다. 와일드 카드 문자를 하나씩만 허용 됩니다. |
| "Include("~/Scripts/Common/T\*") | *ToggleDiv.js, ToggleImg.js* |
| "Include("~/Scripts/Common/\*") | 잘못 된 패턴 예외입니다. 순수 와일드 카드 세그먼트가 잘못 되었습니다. |
| IncludeDirectory("~/Scripts/Common", "T\*") | *ToggleDiv.js, ToggleImg.js* |
| IncludeDirectory("~/Scripts/Common", "T\*",true) | *ToggleDiv.js, ToggleImg.js, ToggleLinks.js* |

명시적으로 각 파일에 번들을 추가 하는 것이 일반적으로 기본 와일드 카드 다음과 같은 이유로 파일 로드를 통해:

- 일반적으로 결과 원하지는 사전순으로 로드 하기에 와일드 카드 기본적으로 스크립트를 추가 합니다. 자주 CSS 및 JavaScript 파일 (영문자가 아닌) 특정 순서에 추가 해야 합니다. 사용자 지정을 추가 하 여이 위험을 완화할 수 있습니다 [IBundleOrderer](https://msdn.microsoft.com/library/system.web.optimization.ibundleorderer(VS.110).aspx) 구현이 아니라 각 파일은 오류 발생 가능성을 명시적으로 추가 합니다. 예를 들어 나중에 폴더를 수정 해야 할 수도 있습니다는 새 자산을 추가할 수 있습니다 하 [IBundleOrderer](https://msdn.microsoft.com/library/system.web.optimization.ibundleorderer(VS.110).aspx) 구현 합니다.
- 해당 번들을 참조 하는 모든 보기에서 로드 하는 와일드 카드를 사용 하 여 디렉터리에 추가 하는 보기 특정 파일을 포함할 수 있습니다. 보기 특정 스크립트 번들에 추가 되 면 번들을 참조 하는 다른 보기에 JavaScript 오류가 발생할 수 있습니다.
- 다른 파일을 가져올 CSS 파일 두 번 로드 하는 가져온된 파일에서 발생 합니다. 예를 들어, 다음 코드는 대부분의 jQuery UI 테마 CSS 파일이 두 번 로드를 사용 하 여 번들을 만듭니다. 

    [!code-csharp[Main](bundling-and-minification/samples/sample12.cs)]

  와일드 카드 선택기 "\*.css" 폴더에 각 CSS 파일에는 포함 하 여 합니다 *Content\themes\base\jquery.ui.all.css* 파일. 합니다 *jquery.ui.all.css* 파일 다른 CSS 파일을 가져옵니다.

## <a name="bundle-caching"></a>캐싱 번들

번들에서 번들을 만들 때 HTTP 만료 헤더 1 년 설정 합니다. Fiddler 표시 IE 번들에 대 한 조건부 요청 해도 이전에 본 페이지로 이동 하는 경우 즉, 가지 번들에 대 한 IE에서 HTTP GET 요청이 없습니다 및 서버에서 304 HTTP 응답이 없습니다. IE (따라서 각 번들에 대 한 HTTP 304 응답) F5 키를 사용 하 여 각 번들에 대 한 조건부 요청을 할 수 있습니다. 사용 하 여 전체 새로 고침을 할 수 있습니다 ^ F5 (따라서 각 번들에 대 한 HTTP 200 응답 합니다.)

다음 이미지는 **캐싱** Fiddler 응답 창의 탭:

![fiddler 캐싱 이미지](bundling-and-minification/_static/image8.png)

요청   
`http://localhost/MvcBM_time/bundles/AllMyScripts?v=r0sLDicvP58AIXN_mc3QdyVvVj5euZNzdsa2N1PKvb81`  
 번들입니다 **AllMyScripts** 쿼리 문자열 쌍을 포함 하 고 **v = r0sLDicvP58AIXN\_mc3QdyVvVj5euZNzdsa2N1PKvb81**합니다. 쿼리 문자열 **v** 값 토큰 캐싱에 사용 되는 고유 식별자입니다. ASP.NET 응용 프로그램 요청으로 번들 변경 되지 합니다 **AllMyScripts** 번들이 토큰을 사용 합니다. 번들의 모든 파일이 변경 되 면 ASP.NET 최적화 프레임 워크에는 번들에 대 한 브라우저 요청 최신 번들을 얻게 되며 보장 하는 새 토큰을 생성 됩니다.

IE9 F12 개발자 도구를 실행 하 고 이전에 로드 된 페이지로 이동 하는 경우 IE 잘못 표시 각 번들 및 HTTP 304를 반환 하는 서버에 대 한 조건부 GET 요청 합니다. IE9 조건부 요청 블로그 항목에서 수행 된 경우를 결정 하는 문제를가 하는 이유를 확인할 수 있습니다 [를 사용 하 여 Cdn 및 웹 사이트 성능 향상에 Expires](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx)합니다.

## <a name="less-coffeescript-scss-sass-bundling"></a>LESS, SCSS, CoffeeScript 묶음 Sass 합니다.

묶음 및 축소 프레임 워크와 같은 중간 언어를 처리 하는 메커니즘을 제공 [SCSS](http://sass-lang.com/)를 [Sass](http://sass-lang.com/)하십시오 [적은](http://www.dotlesscss.org/) 또는 [Coffeescript ](http://coffeescript.org/), 축소와 같은 변환 결과 번들에 적용 합니다. 예를 들어 추가할 [.less](http://www.dotlesscss.org/) MVC 4 프로젝트에 파일:

1. 작은 콘텐츠에 대 한 폴더를 만듭니다. 다음 예제에서는 합니다 *Content\MyLess* 폴더입니다.
2. 추가 된 [.less](http://www.dotlesscss.org/) NuGet 패키지 **점이** 프로젝트입니다.  
    ![NuGet 점 설치](bundling-and-minification/_static/image9.png)
3. 구현 하는 클래스를 추가 합니다 [IBundleTransform](https://msdn.microsoft.com/library/system.web.optimization.ibundletransform(VS.110).aspx) 인터페이스입니다. .Less 변환에 대 한 프로젝트에 다음 코드를 추가 합니다.

    [!code-csharp[Main](bundling-and-minification/samples/sample13.cs)]
4. 사용 하 여 LESS 파일의 번들을 만들지 합니다 `LessTransform` 하며 [CssMinify](https://msdn.microsoft.com/library/system.web.optimization.cssminify(VS.110).aspx) 변환 합니다. 다음 코드를 추가 합니다 `RegisterBundles` 의 메서드를 *앱\_Start\BundleConfig.cs* 파일입니다.

    [!code-csharp[Main](bundling-and-minification/samples/sample14.cs)]
5. 작은 번들을 참조 하는 모든 보기에 다음 코드를 추가 합니다.

    [!code-cshtml[Main](bundling-and-minification/samples/sample15.cshtml)]

## <a name="bundle-considerations"></a>번들 고려 사항

번들을 만들 때 수행 하는 좋은 규칙 번들 이름 접두사로 "번들"를 포함 하는 것입니다. 이렇게 하면 가능한 [라우팅 충돌](https://forums.asp.net/post/5012037.aspx)합니다.

번들의 파일을 업데이트 한 후에 새 토큰을 번들 쿼리 문자열 매개 변수에 대해 생성 되 고 전체 번들 클라이언트가 요청 하는 번들을 포함 하는 페이지 다음에 다운로드 해야 합니다. 기존 태그를 각 자산 개별적으로 나열 됩니다에서 변경 된 파일만 다운로드 됩니다. 자주 변경 되는 자산 묶음에 대 한 적절 한 후보를 수 있습니다.

묶음 및 축소 주로 첫 번째 페이지 요청 로드 시간을 개선 합니다. 브라우저 캐시 된 자산 (예: JavaScript, CSS 및 이미지) 웹 페이지를 요청한 후 동일한 페이지 사이트 동일한 자산을 요청 하거나 묶음 및 축소 같은 페이지를 요청 하는 경우 성능 향상을 제공 하지 않습니다. 설정 하지 않으면는 expires 헤더 자산에서 올바르게 및 묶음 및 축소를 사용 하지 않는, 브라우저 새로 고침 추론 표시 자산 부실 며칠 후 브라우저 각 자산에 대 한 유효성 검사 요청을 해야 합니다. 이 경우 묶음 및 축소 첫 번째 페이지 요청 후 성능이 향상을 제공합니다. 자세한 내용은 블로그를 참조 하십시오. [를 사용 하 여 Cdn 및 웹 사이트 성능 향상에 Expires](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx)합니다.

브라우저에 대 한 제한인 각 호스트 이름 당 6 개의 동시 연결을 사용 하 여 완화할 수 있습니다는 [CDN](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx)합니다. CDN은가 다른 호스트 이름을 호스팅 사이트 보다 때문에 CDN에서 자산이 요청 호스팅 환경에는 6 개의 동시 연결 제한에 대해 계산 되지 않습니다. CDN에는 일반적인 패키지 캐싱 및에 지 캐싱 이점을 제공할 수도 있습니다.

번들을 필요로 하는 페이지 분할 되어야 합니다. 예를 들어, 기본 인터넷 응용 프로그램에 대 한 ASP.NET MVC 템플릿을 번들을 만듭니다 jQuery 유효성 검사 jQuery에서 분리 합니다. 만든 기본 보기 입력 하지 않고 있으며 값을 게시 하지 말고, 때문에 유효성 검사 번들을 포함 하지 않습니다.

`System.Web.Optimization` 네임 스페이스 System.Web.Optimization.DLL에서 구현 됩니다. 활용 WebGrease 라이브러리 (WebGrease.dll) 축소 기능을 차례로 Antlr3.Runtime.dll를 사용 합니다.

*빠른 게시 하 고 링크를 공유 Twitter를 사용 합니다. 내 Twitter 핸들은*: [@RickAndMSFT](http://twitter.com/RickAndMSFT)

## <a name="additional-resources"></a>추가 리소스

- 비디오:[묶음 및 최적화](https://channel9.msdn.com/Events/aspConf/aspConf/Bundling-and-Optimizing) 여 [Howard Dierking](https://twitter.com/#!/howard_dierking)
- [Web Pages 사이트에 웹 최적화 추가](https://blogs.msdn.com/b/rickandy/archive/2012/08/15/adding-web-optimization-to-a-web-pages-site.aspx)합니다.
- [추가 묶음 및 축소 Web forms](https://blogs.msdn.com/b/rickandy/archive/2012/08/14/adding-bundling-and-minification-to-web-forms.aspx)합니다.
- [번들의 성능에 미치는 영향 및 웹 검색에 축소](https://blogs.msdn.com/b/henrikn/archive/2012/06/17/performance-implications-of-bundling-and-minification-on-http.aspx) 여 [Henrik F Nielsen](http://en.wikipedia.org/wiki/Henrik_Frystyk_Nielsen) [@frystyk](https://twitter.com/frystyk)
- [Cdn을 사용 하 여 웹 사이트 성능 향상을 위해 만료](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx) Rick anderson [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)
- [RTT (왕복 시간)를 최소화 합니다.](https://developers.google.com/speed/docs/best-practices/rtt)

## <a name="contributors"></a>참가자

- Hao 둘러싼
- [Howard Dierking](https://twitter.com/#!/howard_dierking)
- Diana LaRose
