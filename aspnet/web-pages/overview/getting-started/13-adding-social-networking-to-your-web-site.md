---
uid: web-pages/overview/getting-started/13-adding-social-networking-to-your-web-site
title: 페이지 (Razor) 사이트를 ASP.NET 웹에 소셜 네트워킹 추가 | Microsoft Docs
author: tfitzmac
description: 이 소셜 네트워킹 서비스를 사용 하 여 사이트를 통합 하는 방법을 설명 합니다. 이 장에서 웹 사이트에 대 한 책갈피/링크 수 있게 하는 방법을 배웁니다...
ms.author: aspnetcontent
ms.date: 02/21/2014
ms.assetid: 03c342f9-b35c-4d7c-b9ed-cd9aaaffedb6
msc.legacyurl: /web-pages/overview/getting-started/13-adding-social-networking-to-your-web-site
msc.type: authoredcontent
ms.openlocfilehash: e50a35d9770da247d18bbe1b3660b7bd5d46d8e9
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37822446"
---
<a name="adding-social-networking-to-aspnet-web-pages-razor-sites"></a>소셜 네트워킹 ASP.NET 웹 페이지 (Razor) 사이트 추가
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서는 ASP.NET Web Pages (Razor) 웹 사이트의 페이지에 Facebook, Twitter, Reddit, 및 Digg에 대 한 소셜 네트워킹 링크를 추가 하는 방법 및 Twitter 피드, Xbox 게이머 카드 및 Gravatar 이미지를 포함 하는 방법을 설명 합니다.
> 
> 학습할 내용:
> 
> - 책갈피/링크 사이트 사용자에 게는 한 방법입니다.
> - Twitter 피드를 추가 하는 방법입니다.
> - Facebook을 추가 하는 방법 **같은** 페이지에는 단추입니다.
> - Gravatar.com 이미지를 렌더링 하는 방법입니다.
> - 사이트에는 Xbox 게이머 카드를 표시 하는 방법.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET Web Pages (Razor) 2
> - ASP.NET 웹 도우미 라이브러리 (NuGet 패키지)
>   
> 
> 이 자습서는 또한 ASP.NET 웹 도우미 라이브러리를 사용 하는 일부 제외 하 고 ASP.NET 웹 페이지 3을 사용 하 여 작동 합니다.


<a id="Linking_Your_Website"></a>
## <a name="linking-your-website-on-social-networking-sites"></a>소셜 네트워킹 사이트에서 웹 사이트를 연결합니다.

사용자와 같은 사이트에서 어떤 일을 하는 경우 종종 친구 들과 공유 하려고 합니다. 가능이 쉬운 사용자가 클릭 하 여 Digg, Reddit, Facebook, Twitter 또는 유사한 사이트에서 페이지를 공유할 수 있는 문자 (아이콘)를 표시 하 여 합니다.

이러한 문자 모양을 표시 하려면 추가 `LinkSharecode` 페이지로 도우미입니다. 페이지를 방문 하는 사용자는 개별 문자 모양을 클릭 수 있습니다. 해당 소셜 네트워킹 사이트에 계정이 있으면 다음 해당 사이트의 페이지에 대 한 링크를 게시할 수 있습니다.

![그림 1](13-adding-social-networking-to-your-web-site/_static/image1.jpg)

1. 에 설명 된 대로 웹 사이트에 ASP.NET Web Helpers Library를 추가 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372)하십시오.-추가 하지 않은 경우 라는 페이지를 만듭니다 *ListLinkShare.cshtml* 추가 다음 태그:

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample1.cshtml)]

    이 예제의 경우는 `LinkShare` 도우미 실행 페이지 제목을 소셜 네트워킹 사이트 페이지 제목을 전달 매개 변수로 전달 됩니다. 그러나 원하는 모든 문자열에 전달할 수 있습니다. 이 예제는 또한 목록에 포함 하는 소셜 네트워킹 사이트를 지정 합니다. 사이트에 관련 된 소셜 네트워킹 사이트를 지정할 수 있습니다.
2. 실행 합니다 *ListLinkShare.cshtml* 브라우저에서 페이지입니다. (페이지에서 선택한 있는지 확인 합니다 **파일** 실행 하기 전에 작업 영역입니다.)
3. 에 등록 되셨습니다는 사이트 중 하나에 대 한 문자 모양을 클릭 합니다. 링크는 페이지를 공유할 수 있는 선택한 소셜 네트워크 사이트에 링크 합니다. 예를 들어, Reddit 링크를 클릭 하면 이동 하면는 `submit to reddit` Reddit 웹 사이트의 페이지입니다.

     ![그림 2](13-adding-social-networking-to-your-web-site/_static/image2.jpg)

<a id="Adding_a_Twitter_Feed"></a>
## <a name="adding-a-twitter-feed"></a>피드는 Twitter 추가

Twitter API의 현재 버전과 호환 되는 Twitter 도우미를 사용 하는 방법에 대 한 내용은 [Twitter 도우미](../ui-layouts-and-themes/twitter-helper.md)합니다. 이 예제에서는 여러 페이지에서 코드를 쉽게 다시 사용할 수 있도록 고유한 도우미를 작성 하는 방법을 보여 줍니다.

<a id="Displaying_a_Facebook_Button"></a>
## <a name="displaying-a-facebook-quotlikequot-button"></a>Facebook 표시 &quot;같은&quot; 단추

경우에 따라 것이 가장 좋은 도우미에 의존 하는 것이 아니라 소셜 네트워킹 공급자에서 직접 코드를 가져올 수 있습니다. 소셜 네트워크 공급자 도우미는 업데이트 보다 더 빨리 해당 옵션을 업데이트 하는 경우 특히 그렇습니다.

Facebook 기능 (예: Like 단추)에 사이트를 추가 하려면 코드 조각에서 검색할 수 있습니다 합니다 [developers.facebook.com](https://developers.facebook.com/) 사이트입니다. Facebook 사이트에서 사이트와 관련 된 코드를 생성 하는 도구를 사용 합니다.

다음 강조 표시 된 코드는 developers.facebook.com 사이트 단추와 같은 도구에서 검색 된 코드가입니다. 사용자 고유의 앱 ID를 제공 해야 합니다.

[!code-html[Main](13-adding-social-networking-to-your-web-site/samples/sample2.html?highlight=7-14,16-17)]

<a id="Rendering_a_Gravatar_Image"></a>
## <a name="rendering-a-gravatar-image"></a>Gravatar 이미지 렌더링

*Gravatar* (을 &quot;전역적으로 인식된 아바타&quot;)은 여러 웹 사이트에서 아바타로 사용할 수 있는 이미지 &#8212; 수를 표시 하는 이미지, 합니다. 예를 들어, 한 Gravatar 블로그 주석에서 포럼 게시물에서는 사용자를 식별 하 고 등 수 있습니다. (사용자 고유의 Gravatar Gravatar 웹 사이트에서 등록할 수 있습니다 [ http://www.gravatar.com/ ](http://www.gravatar.com/).) 웹 사이트에 사용자의 이름 또는 이메일 주소 옆에 있는 이미지를 표시 하려는 경우 Gravatar 도우미를 사용할 수 있습니다.

이 예제에서는 직접 나타내는 단일 Gravatar 사용 하는 합니다. Gravatar를 사용 하는 또 다른 방법은 사이트에 등록할 때 해당 Gravatar 주소를 지정 하는 사용자에 게 됩니다. (에 등록할 수 있게 하는 방법을 알아볼 수 있습니다 [추가 보안 및 ASP.NET 웹 페이지 사이트 멤버 자격](https://go.microsoft.com/fwlink/?LinkId=202904).) 해당 사용자에 대 한 정보를 표시할 때마다 사용자의 이름을 표시 하는 위치는 Gravatar만 추가할 수 있습니다.

1. 에 설명 된 대로 웹 사이트에 ASP.NET Web Helpers Library를 추가 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372), 아직 없는 경우.
2. 라는 새 웹 페이지를 만듭니다 *Gravatar.cshtml*합니다.
3. 파일에 다음 태그를 추가 합니다. 

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample3.cshtml)]

    `Gravatar.GetHtml` 메서드는 페이지의 Gravatar 이미지를 표시 합니다. 이미지의 크기를 변경 하려면 두 번째 매개 변수로 숫자를 포함할 수 있습니다. 기본 크기는 80입니다. 숫자 보다 작거나 80 확인 이미지 작은 합니다. 80 보다 큰 숫자 보다 큰 이미지를 확인합니다.
4. 에 `Gravatar.GetHtml` 메서드를 대체 `<Your Gravatar account here>` Gravatar 계정에 사용 하는 전자 메일 주소를 사용 하 여 합니다. (Gravatar 계정이 없으면 사용할 수는 사용자의 이메일 주소입니다.)
5. 브라우저에서 페이지를 실행 합니다. 페이지는 지정한 전자 메일 주소에 대 한 두 가지 Gravatar 이미지를 표시 합니다. 두 번째 이미지는 첫 번째 보다 작습니다. 

    ![그림 4](13-adding-social-networking-to-your-web-site/_static/image3.jpg)

<a id="Displaying_an_Xbox_Gamer_Card"></a>
## <a name="displaying-an-xbox-gamer-card"></a>Xbox 게이머 카드를 표시합니다.

사용자는 Microsoft Xbox 온라인 게임을 재생 하는 경우 각 사용자 고유 ID가 있습니다. 통계는 평판, 게이머 점수를 보여 줍니다. 최근에 게임을 재생 하며 게이머 카드의 형태로 각 플레이어에 대해 유지 됩니다. Xbox 게이머 인 경우에 표시할 수 있습니다 게이머 카드 사이트에서에서 페이지를 사용 하 여는 `GamerCard` 도우미입니다.

1. 에 설명 된 대로 웹 사이트에 ASP.NET Web Helpers Library를 추가 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372), 아직 없는 경우.
2. 라는 새 페이지를 만듭니다 *XboxGamer.cshtml* 다음 태그를 추가 합니다.

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample4.cshtml)]

    사용 된 `GamerCard.GetHtml` 표시할 게이머 카드에 대 한 별칭을 지정 하는 속성입니다.
3. 브라우저에서 페이지를 실행 합니다. 페이지는 지정한 Xbox 게이머 카드를 표시 합니다.

    ![그림 5](13-adding-social-networking-to-your-web-site/_static/image4.jpg)
