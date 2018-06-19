---
uid: web-pages/overview/getting-started/13-adding-social-networking-to-your-web-site
title: 페이지 (Razor) 사이트를 ASP.NET 웹에 소셜 네트워킹 추가 | Microsoft Docs
author: tfitzmac
description: 이 사이트 소셜 네트워킹 서비스와 통합 하는 방법을 설명 합니다. 이 장에서 책갈피/링크 웹 사이트 사용자에 게 알릴지 방법을 배우게 됩니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/21/2014
ms.topic: article
ms.assetid: 03c342f9-b35c-4d7c-b9ed-cd9aaaffedb6
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/13-adding-social-networking-to-your-web-site
msc.type: authoredcontent
ms.openlocfilehash: 2d1f0074edf473c4be06adaa32598dd828a7552c
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30899345"
---
<a name="adding-social-networking-to-aspnet-web-pages-razor-sites"></a>소셜 네트워킹 ASP.NET 웹 페이지 (Razor) 사이트를 추가 합니다.
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서는 ASP.NET 웹 페이지 (Razor) 웹 사이트의 페이지에 Facebook, Twitter, Reddit, 및 Digg에 대 한 소셜 네트워킹 링크를 추가 하는 방법 및 Twitter 피드, Xbox 게이머 카드 및 Gravatar 이미지를 포함 하는 방법을 설명 합니다.
> 
> 학습 내용:
> 
> - 책갈피/링크 사이트 수 있게 하는 방법.
> - Twitter 피드를 추가 하는 방법입니다.
> - Facebook을 추가 하는 방법 **같은** 페이지에는 단추입니다.
> - Gravatar.com 이미지를 렌더링 하는 방법.
> - 사이트에는 Xbox 게이머 카드를 표시 하는 방법.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 2
> - ASP.NET 웹 도우미 라이브러리 (NuGet 패키지)
>   
> 
> 이 자습서는 또한 ASP.NET 웹 도우미 라이브러리를 사용 하는 파트를 제외 하 고 ASP.NET 웹 페이지 3으로 작동 합니다.


<a id="Linking_Your_Website"></a>
## <a name="linking-your-website-on-social-networking-sites"></a>소셜 네트워킹 사이트에서 웹 사이트를 연결합니다.

사람들이 마음에 사이트에, 종종 친구와 공유 하려고 합니다. 가능이 쉽게 사용자 Digg, Reddit, Facebook, Twitter, 또는 유사한 사이트에서 페이지를 공유 하기 위해 클릭할 수는 (아이콘)의 문자를 표시 하 여 합니다.

이러한 문자 모양을 표시 하려면 추가 `LinkSharecode` 페이지에는 도우미입니다. 페이지를 방문 하는 사용자는 개별 문자 모양을 클릭 수 있습니다. 해당 소셜 네트워킹 사이트에 계정이 있는 경우에 다음 해당 사이트에서 페이지에 대 한 링크를 게시할 수 있습니다.

![그림 1](13-adding-social-networking-to-your-web-site/_static/image1.jpg)

1. 에 설명 된 대로 웹 사이트에 ASP.NET Web Helpers Library를 추가 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372)합니다.-추가 하지 않은 경우는 *ListLinkShare.cshtml* 추가 다음 태그:

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample1.cshtml)]

    이 예제에서는 때는 `LinkShare` 페이지 제목, 도우미 실행 소셜 네트워킹 사이트 페이지 제목을 전달 매개 변수로 전달 됩니다. 그러나 원하는 모든 문자열을 전달할 수 있습니다. 이 예제는 또한 목록에 포함할 소셜 네트워킹 사이트를 지정 합니다. 사이트에 관련 된 소셜 네트워킹 사이트를 지정할 수 있습니다.
2. 실행 된 *ListLinkShare.cshtml* 브라우저에서 페이지입니다. (있는지 확인 페이지에서 선택한는 **파일** 실행 하기 전에 작업 영역입니다.)
3. 에 등록 하는 사이트 중 하나에 대 한 문자 모양을 클릭 합니다. 링크를 이동 페이지를 공유할 수 있는 선택한 소셜 네트워크 사이트에 링크 합니다. 예를 들어 Reddit 링크를 클릭 하면 하는 이동 하 여 `submit to reddit` Reddit 웹 사이트에서 페이지입니다.

     ![그림 2](13-adding-social-networking-to-your-web-site/_static/image2.jpg)

<a id="Adding_a_Twitter_Feed"></a>
## <a name="adding-a-twitter-feed"></a>추가 된 Twitter 피드

Twitter API의 현재 버전과 호환 되는 Twitter 도우미를 사용 하는 방법에 대 한 정보를 참조 하십시오. [Twitter 도우미](../ui-layouts-and-themes/twitter-helper.md)합니다. 이 예제에는 여러 페이지에서 코드를 쉽게 재사용할 수 있도록 고유한 도우미를 작성 하는 방법을 보여 줍니다.

<a id="Displaying_a_Facebook_Button"></a>
## <a name="displaying-a-facebook-quotlikequot-button"></a>표시는 Facebook &quot;같은&quot; 단추

경우에 따라 한 도우미에 의존 하지 않고 소셜 네트워킹 공급자에서 직접 코드 하에 가장 좋은 방법이입니다. 소셜 네트워크 공급자 도우미 업데이트 보다 더 빨리 해당 옵션을 업데이트 하는 경우 특히 유용 합니다.

Facebook 기능 (예: Like 단추)에 사이트를 추가 하려면 코드 조각에서 검색할 수 있습니다는 [developers.facebook.com](https://developers.facebook.com/) 사이트입니다. Facebook 사이트에서 사이트와 관련 된 코드 조각을 생성 하는 도구를 사용 합니다.

다음 강조 표시 된 코드에 developers.facebook.com 사이트의 단추와 같은 도구에서 검색 된 코드가입니다. 사용자 고유의 응용 프로그램 ID를 제공 해야 합니다.

[!code-html[Main](13-adding-social-networking-to-your-web-site/samples/sample2.html?highlight=7-14,16-17)]

<a id="Rendering_a_Gravatar_Image"></a>
## <a name="rendering-a-gravatar-image"></a>Gravatar 이미지 렌더링

A *Gravatar* (한 &quot;전체적으로 인식 된 아바타&quot;)는 아바타도 여러 웹 사이트에서 사용할 수 있는 이미지 &#8212; 수를 표시 하는 이미지, 합니다. 예를 들어 한 Gravatar 수 포럼 게시물 블로그 주석에서의 사용자 식별 등에입니다. (의 Gravatar 웹 사이트에서 사용자 고유의 Gravatar 등록할 수 있는 [ http://www.gravatar.com/ ](http://www.gravatar.com/).) 웹 사이트에 사용자의 이름 또는 전자 메일 주소 옆에 있는 이미지를 표시 하려는 경우 Gravatar 도우미를 사용할 수 있습니다.

이 예제에서는 사용자가 직접 나타내는 단일 Gravatar를 사용 하는 합니다. Gravatar를 사용 하 여 사이트에 등록할 때 해당 Gravatar 주소를 지정 하는 사용자에 게 알릴지 됩니다. (에 등록할 수 있게 하는 방법을 학습할 수 있는 [추가 보안 및 ASP.NET 웹 페이지 사이트 멤버 자격](https://go.microsoft.com/fwlink/?LinkId=202904).) 해당 사용자에 대 한 정보를 표시할 때마다 사용자의 이름을 표시 하는 Gravatar만 추가할 수 있습니다.

1. 에 설명 된 대로 웹 사이트에 ASP.NET Web Helpers Library를 추가 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372)아직 없는 경우, 합니다.
2. 라는 새 웹 페이지 생성 *Gravatar.cshtml*합니다.
3. 파일에 다음 태그를 추가 합니다. 

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample3.cshtml)]

    `Gravatar.GetHtml` 메서드 Gravatar 이미지를 페이지에 표시 합니다. 이미지의 크기를 변경 하려면 두 번째 매개 변수로 숫자를 포함할 수 있습니다. 기본 크기는 80입니다. 숫자 보다 작거나 80 확인 이미지 더 작은. 80 보다 큰 숫자 보다 큰 이미지를 확인합니다.
4. 에 `Gravatar.GetHtml` 메서드를 대체 `<Your Gravatar account here>` Gravatar 계정에 대해 사용 하는 전자 메일 주소를 사용 합니다. (Gravatar 계정에 없을 경우 사용할 수 있습니다는 사람의 전자 메일 주소.)
5. 브라우저에서 페이지를 실행 합니다. 지정한 전자 메일 주소에 대 한 두 개의 Gravatar 이미지가 페이지에 표시 됩니다. 두 번째 이미지는 첫 번째 보다 작습니다. 

    ![그림 4](13-adding-social-networking-to-your-web-site/_static/image3.jpg)

<a id="Displaying_an_Xbox_Gamer_Card"></a>
## <a name="displaying-an-xbox-gamer-card"></a>Xbox 게이머 카드 표시

사용자는 Microsoft Xbox 온라인 게임을 플레이할 각 사용자는 고유한 id입니다. 각 플레이어의 평판, 게이머 점수를 표시 하 고 최근에 게임을 재생는 게이머 카드의 형식에서에 대 한 통계 유지 됩니다. 게이머 Xbox 인 경우에 표시할 수 있습니다 프로그램 게이머 카드 사이트의 페이지를 사용 하 여는 `GamerCard` 도우미입니다.

1. 에 설명 된 대로 웹 사이트에 ASP.NET Web Helpers Library를 추가 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372)아직 없는 경우, 합니다.
2. 명명 된 새 페이지를 만들고 *XboxGamer.cshtml* 다음 태그를 추가 합니다.

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample4.cshtml)]

    사용 된 `GamerCard.GetHtml` 속성을 표시할 게이머 카드에 대 한 별칭을 지정 합니다.
3. 브라우저에서 페이지를 실행 합니다. 이 페이지에는 지정한 Xbox 게이머 카드를 표시 됩니다.

    ![그림 5](13-adding-social-networking-to-your-web-site/_static/image4.jpg)
