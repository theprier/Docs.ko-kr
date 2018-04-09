---
uid: web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
title: (Razor) 사이트 페이지는 ASP.NET 웹에 지도 표시 합니다. | Microsoft Docs
author: tfitzmac
description: 이 문서에서는 대화형 지도 매핑 Bing, Google, Ma 제공한 서비스를 기반으로 하는 ASP.NET 웹 페이지 (Razor) 웹 사이트의 페이지에 표시 하는 방법에 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2014
ms.topic: article
ms.assetid: b5c268dd-ca6a-4562-b94c-a220fcf01f58
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 608dab8760bad7b877ab6fd4f89b21e980f5b1db
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="displaying-maps-in-an-aspnet-web-pages-razor-site"></a>ASP.NET 웹 페이지 (Razor) 사이트에 지도 표시합니다.
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 대화형 지도 매핑 Bing, Google, 지도 보기, Yahoo에서 제공 되는 서비스를 기반으로 하는 ASP.NET 웹 페이지 (Razor) 웹 사이트의 페이지에 표시 하는 방법을 설명 합니다.
> 
> 학습 내용:
> 
> - 주소에 기반 하는 맵을 생성 하는 방법.
> - 위도 및 경도 좌표에 따라 맵을 생성 하는 방법.
> - Bing 지도와 사용할 키를 가져오고, Bing Maps 개발자 계정을 등록 하는 방법.
> 
> 다음은 문서에 도입 된 ASP.NET 기능입니다.
> 
> - `Maps` 도우미입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 2
> - WebMatrix 2
>   
> 
> 이 자습서는 WebMatrix 3 에서도 작동합니다.


웹 페이지를 표시할 수 있습니다 맵 페이지에서 사용 하 여 `Maps` 도우미입니다. 주소 또는 경도 및 위도 좌표 집합을 기반으로 하는 지도 생성할 수 있습니다. `Maps` 클래스 Bing, Google, 지도 보기, Yahoo 등 널리 사용 되 지도 엔진을 호출할 수 있습니다.

페이지에 매핑을 추가 하는 단계는 호출 지도 엔진에 관계 없이 동일 합니다. 지도 표시 하는 사용할 수 있는 메서드를 사용 하면 JavaScript 파일 참조를 추가 하 고의 메서드를 호출 하는 다음의 `Maps` 도우미입니다.

에 따라 지도 서비스를 선택 `Maps` 도우미 메서드를 사용 합니다. 이러한 항목 중 하나를 사용할 수 있습니다.

- `Maps.GetBingHtml`
- `Maps.GetGoogleHtml`
- `Maps.GetYahooHtml`
- `Maps.GetMapQuestHtml`

## <a name="installing-the-pieces-you-need"></a>필요한 구성 요소를 설치 합니다.

지도 표시 하려면이 정보가 필요 합니다.

- `Maps` 도우미입니다. 이 도우미 ASP.NET Web Helpers Library의 버전 2입니다. 라이브러리를 추가 하지 않은 경우 NuGet 패키지로 사이트에 설치할 수 있습니다. 자세한 내용은 참조 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372)합니다. (갤러리에서 검색 된 `microsoft-web-helpers` 패키지 합니다.)
- JQuery 라이브러리입니다. JQuery 라이브러리에 이미 포함 되어 WebMatrix 사이트 템플릿 중 일부의 *스크립트* 폴더입니다. 이러한 라이브러리가 최신 jQuery 라이브러리에서 직접 다운로드할 수 있습니다는 [jQuery.org](http://jQuery.org) 사이트입니다. 서식 파일을 사용 하 여 새 사이트를 만들 수 있습니다 (예를 들어는 **시작 사이트** 템플릿을) 현재 사이트에 해당 사이트에서 jQuery 파일을 복사 합니다.

마지막으로, Bing maps를 사용 하려는 경우 먼저 (무료) 계정 만들고 해야 키를 받습니다. 키를 가져오려면 다음이 단계를 따르십시오.

1. 계정을 만듭니다는 [Bing Maps 개발자 계정](https://www.microsoft.com/maps/developers/web.aspx)합니다. Microsoft 계정 (Windows Live ID)도 있어야 합니다.

    에 대 한 키를 사용 하도록 지정할 수 있습니다 **평가/테스트**합니다. 이동 컴퓨터에 IIS Express 및 WebMatrix를 사용 하 여 매핑 함수를 테스트 하는 경우는 **사이트** 작업 영역을 참고 하면 사이트의 URL (예를 들어 `http://localhost:50408`, 포트 번호는 다르지만 것). 이 사용 하 여 *localhost* 등록할 때 사이트와 주소입니다.
2. 을 계정에 등록 한 후 Bing Maps 계정 센터 이동 하 고 클릭 **만들기 또는 뷰 키**:

    ![mapping-2](displaying-maps-in-an-aspnet-web-pages-site/_static/image1.png)
3. Bing 만드는 키를 기록 합니다.

## <a name="creating-a-map-based-on-an-address-using-google"></a>주소 (사용 하 여 Google)에 따라 맵 만들기

다음 예제에는 주소에 기반 하는 구조를 렌더링 하는 페이지를 만드는 방법을 보여 줍니다. 이 예제에는 Google 맵을 사용 하는 방법을 보여 줍니다.

1. 라는 파일을 만들어 *MapAddress.cshtml* 사이트의 루트에 있습니다. 이 페이지는 지도를 전달 하는 주소에 따라 생성 됩니다.
2. 다음 코드를 파일에 복사 기존 내용을 덮어씁니다.

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    페이지의 다음 기능을 확인 합니다.

    - `<script>` 요소에는 `<head>` 요소입니다. 예제에서는 `<script>` 요소 참조는 *jquery 1.6.4.min.js* jQuery 라이브러리, 1.6.4 버전 (압축된) 축소 된 버전에 있는 파일입니다. 참조 가정는 *.js* 중인 파일의 *스크립트* 사이트의 폴더입니다. 

        > [!NOTE]
        > 다른 버전의 jQuery 라이브러리를 사용 하는 경우 단지를 가리키고 있는 해당 버전 올바르게 있어야 합니다.
    - 에 대 한 호출에서 `@Maps.GetGoogleHtml` 페이지의 본문에 있습니다. 주소를 매핑하려면 주소 문자열을 전달 해야 합니다. 비슷한 방법으로 다른 맵 엔진에 대 한 메서드는 작동 (`@Maps.GetYahooHtml`, `@Maps.GetMapQuestHtml`).
3. 페이지를 실행 하 고 주소를 입력 합니다. 사용자가 지정한 위치를 표시 하는 Google 맵에 따라 지도 페이지에 표시 됩니다.

     ![mapping-1](displaying-maps-in-an-aspnet-web-pages-site/_static/image2.png)

## <a name="creating-a-map-based-on-latitude-and-longitude-coordinates-using-bing"></a>위도 및 경도에 따라 맵 만들기 좌표를 (Bing 사용)

이 예제에는 좌표에 따라 지도 만드는 방법을 보여 줍니다. 이 예제에서는 Bing maps를 사용 하는 방법과 Bing 키를 포함 하는 방법을 보여 줍니다. (또한 Bing 키를 사용 하지 않고 다른 맵 엔진 사용 하 여 좌표에 따라 맵을 만들 수 있습니다.)

1. 라는 파일을 만들어 *MapCoordinates.cshtml* 사이트와의 다음 코드와 태그를 사용 하 여 기존 콘텐츠 바꾸기의 루트에서:

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample2.cshtml)]
2. 대체 `your-key-here` 앞에서 생성 하는 Bing 지도 키를 사용 합니다.
3. 실행 된 *MapCoordinates.cshtml* 페이지 위도 및 경도 좌표를 입력 한 다음 클릭는 **Map It!** 클릭합니다. (모든 좌표를 모르는 경우 다음을 시도 합니다. 이 Microsoft 레드먼드 본사에 있습니다.)

   - 위도: 47.6781005859375
   - Longitude: -122.158317565918

     지정한 좌표를 사용 하는 페이지가 표시 됩니다.

     ![mapping-3](displaying-maps-in-an-aspnet-web-pages-site/_static/image3.png)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 자료


[Microsoft.Maps API 참조](https://msdn.microsoft.com/library/gg427611.aspx)
