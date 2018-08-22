---
uid: web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
title: 페이지 (Razor) 사이트를 ASP.NET 웹에 맵 표시 | Microsoft Docs
author: tfitzmac
description: 이 문서에서는 Bing, Google, Ma 제공한 서비스 매핑을 기반으로 하는 ASP.NET Web Pages (Razor) 웹 사이트의 페이지에서 대화형 지도 표시 하는 방법을 설명 하는 중...
ms.author: riande
ms.date: 02/20/2014
ms.assetid: b5c268dd-ca6a-4562-b94c-a220fcf01f58
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 0b0879047bc71057884ebef98a598eed8c28cddf
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829698"
---
<a name="displaying-maps-in-an-aspnet-web-pages-razor-site"></a>ASP.NET 웹 페이지 (Razor) 사이트에 맵 표시
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에는 Bing, Google, 지도 보기, Yahoo를 제공 하는 서비스 매핑을 기반으로 하는 ASP.NET Web Pages (Razor) 웹 사이트의 페이지에서 대화형 지도 표시 하는 방법을 설명 합니다.
> 
> 학습할 내용:
> 
> - 주소에 기반 하는 맵을 생성 하는 방법입니다.
> - 위도 및 경도 좌표를 기준으로 지도 생성 하는 방법입니다.
> - Bing 맵 개발자 계정을 등록 하 고 Bing Maps를 사용 하는 키를 가져오는 방법입니다.
> 
> 문서에 도입 된 ASP.NET 기능은 다음과 같습니다.
> 
> - `Maps` 도우미입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET Web Pages (Razor) 2
> - WebMatrix 2
>   
> 
> 이 자습서 에서도 WebMatrix 3를 사용 하 여 작동합니다.


웹 페이지에서 표시할 수 있습니다 맵 페이지에서 사용 하 여 `Maps` 도우미입니다. 주소 또는 경도 및 위도 좌표 집합을 기반으로 하는 지도 생성할 수 있습니다. `Maps` 클래스 Bing, Google, 지도 보기, Yahoo 등 널리 사용 되 지도 엔진을 호출할 수 있습니다.

페이지에 매핑을 추가 하는 단계는 호출 지도 엔진에 관계 없이 동일 합니다. 지도 표시할 사용 가능한 메서드는 JavaScript 파일 참조를 추가 하면 및의 메서드를 호출 하는 다음을 `Maps` 도우미입니다.

에 따라 맵 서비스를 선택 하면 `Maps` 도우미 메서드를 사용 합니다. 이러한 템플릿 중 하나를 사용할 수 있습니다.

- `Maps.GetBingHtml`
- `Maps.GetGoogleHtml`
- `Maps.GetYahooHtml`
- `Maps.GetMapQuestHtml`

## <a name="installing-the-pieces-you-need"></a>필요한 구성 요소를 설치 합니다.

지도 표시 하려면 이러한 정보가 필요 합니다.

- `Maps` 도우미입니다. 이 도우미 ASP.NET Web Helpers Library 버전 2입니다. 라이브러리를 추가 하지 않은 경우 NuGet 패키지로 사이트에서 설치할 수 있습니다. 자세한 내용은 참조 하세요 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372)합니다. (갤러리에서 검색 된 `microsoft-web-helpers` 패키지 있습니다.)
- JQuery 라이브러리입니다. JQuery 라이브러리에 이미 들어 WebMatrix 사이트 템플릿의 여러 자신의 *스크립트* 폴더입니다. 이러한 라이브러리가 없는 경우에서 직접 최신 jQuery 라이브러리를 다운로드할 수 있습니다 합니다 [jQuery.org](http://jQuery.org) 사이트입니다. 템플릿을 사용 하 여 새 사이트를 만들 수 있습니다 (예를 들어를 **시작 사이트** 템플릿) 한 다음 현재 사이트로 해당 사이트에서 jQuery 파일을 복사 합니다.

마지막으로, Bing maps를 사용 하려는 경우 먼저 (무료) 계정 만들고 해야 키를 받으세요. 키를 가져오려면 다음이 단계를 수행 합니다.

1. 에 계정을 만들고 합니다 [Bing Maps 개발자 계정](https://www.microsoft.com/maps/developers/web.aspx)합니다. Microsoft 계정 (Windows Live ID)도 있어야 합니다.

    에 대 한 키를 사용 하도록 지정할 수 있습니다 **평가/테스트**합니다. WebMatrix 및 IIS Express를 사용 하 여 사용자 고유의 컴퓨터 매핑 함수를 테스트 하는 경우 이동 합니다 **사이트** 작업 영역 및 참고 사이트의 URL (예를 들어 `http://localhost:50408`이지만 포트 번호는 다른 것). 사용할 수 있습니다 *localhost* 등록할 때 사이트와 주소입니다.
2. 계정에 등록 한 후 Bing Maps 계정 센터로 이동 하 고 클릭 **키 만들기 또는 보기**:

    ![매핑-2](displaying-maps-in-an-aspnet-web-pages-site/_static/image1.png)
3. Bing에서 만든 키를 기록 합니다.

## <a name="creating-a-map-based-on-an-address-using-google"></a>주소 (사용 하 여 Google)에 따라 맵 만들기

다음 예제는 주소를 기반으로 지도 렌더링 하는 페이지를 만드는 방법을 보여 줍니다. 이 예제에는 Google Maps를 사용 하는 방법을 보여 줍니다.

1. 이라는 파일을 만듭니다 *MapAddress.cshtml* 사이트의 루트에 있습니다. 이 페이지를 전달 하는 주소에 기반 하는 맵을 생성 됩니다.
2. 기존 콘텐츠를 덮어씁니다를 파일에 다음 코드를 복사 합니다.

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    페이지의 다음 기능을 확인 합니다.

    - 합니다 `<script>` 요소에는 `<head>` 요소입니다. 예에서는 `<script>` 요소 참조를 *jquery 1.6.4.min.js* 파일을 버전 1.6.4 jQuery 라이브러리의 (압축된) 축소 된 버전입니다. 참조는 가정 합니다 *.js* 파일은 합니다 *스크립트* 사이트의 폴더입니다. 

        > [!NOTE]
        > 다른 버전의 jQuery 라이브러리를 사용 하는 경우 방금 가리키고 있는지 확인 하는 해당 버전을 올바르게.
    - 에 대 한 호출을 `@Maps.GetGoogleHtml` 페이지의 본문에 있습니다. 주소에 매핑하려면 주소 문자열을 전달 해야 합니다. 다른 맵 엔진에 대 한 메서드는 유사한 방식으로 작동 (`@Maps.GetYahooHtml`, `@Maps.GetMapQuestHtml`).
3. 페이지를 실행 하 고 주소를 입력 합니다. 페이지에 지정 된 위치를 보여 주는 Google 맵을 기반으로 지도 표시 됩니다.

     ![매핑-1](displaying-maps-in-an-aspnet-web-pages-site/_static/image2.png)

## <a name="creating-a-map-based-on-latitude-and-longitude-coordinates-using-bing"></a>(Bing 사용) 조정 위도 및 경도에 따라 맵 만들기

이 예제에는 좌표를 기준으로 지도 만드는 방법을 보여 줍니다. 이 예제에서는 Bing maps를 사용 하는 방법 및 Bing 키를 포함 하는 방법을 보여 줍니다. (또한 Bing 키를 사용 하지 않고 다른 맵 엔진을 사용 하 여 좌표에 따라 맵을 만들 수 있습니다.)

1. 이라는 파일을 만듭니다 *MapCoordinates.cshtml* 바꾸기 다음 코드와 태그를 사용 하 여 기존 콘텐츠를 확인 하 고 사이트의 루트에:

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample2.cshtml)]
2. 대체 `your-key-here` 이전에 생성 하는 Bing 지도 키를 사용 하 여 합니다.
3. 실행 합니다 *MapCoordinates.cshtml* 페이지, 위도 및 경도 좌표를 입력 한 다음 클릭는 **Map It!** 클릭합니다. (모든 좌표를 모르는 경우 다음을 시도 합니다. 이것이 Microsoft 레드먼드 캠퍼스에서 한 위치입니다.)

   - 위도: 47.6781005859375
   - 경도:-122.158317565918

     페이지가 지정 된 좌표를 사용 하 여 표시 됩니다.

     ![매핑-3](displaying-maps-in-an-aspnet-web-pages-site/_static/image3.png)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스


[Microsoft.Maps API 참조](https://msdn.microsoft.com/library/gg427611.aspx)
