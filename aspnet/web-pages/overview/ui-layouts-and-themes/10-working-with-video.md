---
uid: web-pages/overview/ui-layouts-and-themes/10-working-with-video
title: 페이지 (Razor) 사이트를 ASP.NET 웹에서 비디오를 표시 합니다. | Microsoft Docs
author: Rick-Anderson
description: 이 장에서 ASP.NET 웹 페이지에서 Razor 구문 페이지를 사용 하 여 비디오를 표시 하는 방법에 설명 합니다.
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 332fb3da-e2a5-460d-bb90-dd911e1e2c95
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/10-working-with-video
msc.type: authoredcontent
ms.openlocfilehash: 8f4b7186ae5c7b7b384ebcb23f7c9ad65caeb0bd
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021042"
---
<a name="displaying-video-in-an-aspnet-web-pages-razor-site"></a>ASP.NET 웹 페이지 (Razor) 사이트에 비디오를 표시
====================
[Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 ASP.NET Web Pages (Razor) 웹 사이트에서 (미디어) 비디오 플레이어를 사용 하 여 사용자가 사이트에 저장 된 비디오를 볼 수 있도록 하는 방법에 설명 합니다. Razor 구문이 있는 ASP.NET 웹 페이지를 사용 하면 플래시 재생 (*.swf*)을 Media Player (*.wmv*), 및 Silverlight (*.xap*) 비디오.
> 
> 학습할 내용:
> 
> - 비디오 플레이어를 선택 하는 방법입니다.
> - 웹 페이지에 비디오를 추가 하는 방법입니다.
> - 비디오 플레이어 특성을 설정 하는 방법입니다.
> 
> 이 ASP.NET Razor 페이지는 문서에 도입 된 기능:
> 
> - `Video` 도우미입니다.
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


## <a name="introduction"></a>소개

사이트에 비디오를 표시 수 있습니다. 작업을 수행 하는 한 가지 방법은 YouTube 같이 텍스트가 풍부한 비디오에 이미 있는 사이트에 연결 하는 것입니다. 고유한 페이지에서 직접 해당이 사이트에서 비디오를 포함 하려는 경우 일반적으로 사이트에서 HTML 태그를 얻을 수 있으며 다음 페이지에 복사할 수 있습니다. 예를 들어, 다음 예와 YouTube를 포함 하는 방법 비디오:

[!code-html[Main](10-working-with-video/samples/sample1.html?highlight=10-14)]

(비디오 공유 공용 사이트)에 없는 고유한 웹 사이트에 있는 비디오를 재생 하려는 경우 다음과 같은 포함 된 태그를 사용 하 여 직접 연결할 수 없습니다. 사용 하 여 사이트에서 비디오를 재생할 수는 있지만 `Video` 페이지에서 직접 미디어 플레이어를 렌더링 하는 도우미입니다.

<a id="Choosing_a_Video_Player"></a>
## <a name="choosing-a-video-player"></a>비디오 플레이어를 선택합니다.

많은 비디오 파일, 형식 및 형식 마다 다른 플레이어 및 플레이어를 구성 하는 다른 방법을 일반적으로 필요 합니다. ASP.NET Razor 페이지에 사용 하 여 웹 페이지에서 비디오를 재생할 수 있습니다는 `Video` 도우미입니다. `Video` 도우미 자동으로 생성 하기 때문에 웹 페이지에 비디오를 포함 하는 과정을 간소화 합니다 `object` 및 `embed` 일반적으로 페이지에 비디오를 추가 하는 데 사용 되는 HTML 요소입니다.

`Video` 도우미는 다음 미디어 플레이어를 지원 합니다.

- Adobe Flash
- Windows MediaPlayer
- Microsoft Silverlight

### <a name="the-flash-player"></a>Flash Player

`Flash` 의 플레이어를 `Video` 도우미를 사용 하면 플래시 비디오 재생 (*.swf* 파일) 웹 페이지에 있습니다. 최소한 비디오 파일의 경로를 제공 해야 합니다. 경로만 지정 하면 플레이어는 Flash의 현재 버전으로 설정 된 기본값을 사용 합니다. 일반적인 기본 설정은 다음과 같습니다.

- 기본 너비와 높이 사용 하 여 비디오가 표시 되므로 않고 배경색입니다.
- 비디오는 페이지를 로드할 때 자동으로 재생 됩니다.
- 비디오에는 명시적으로 중지 될 때까지 계속 반복 합니다.
- 비디오는 특정 크기에 맞게 비디오 자르기 하는 것이 아니라 비디오를 모두 표시 하려면 크기가 조정 됩니다.
- 창에서 비디오를 재생합니다.

### <a name="the-mediaplayer-player"></a>MediaPlayer 플레이어

합니다 `MediaPlayer` 의 플레이어 합니다 `Video` 도우미를 사용 하면 Windows Media 비디오 재생 (*.wmv* 파일), Windows Media 오디오 (*.wma* 파일), 및 MP3 (*. mp3* 웹 페이지의 파일). 재생; 미디어 파일의 경로 포함 해야 합니다. 다른 모든 매개 변수는 선택적입니다. 경로만 지정 하면, 플레이어와 같은 MediaPlayer 현재 버전에서 설정한 기본 설정을 사용 합니다.

- 비디오의 기본 너비와 높이 사용 하 여 표시 됩니다.
- 비디오는 페이지를 로드할 때 자동으로 재생 됩니다.
- 한 번 재생 (해당 하지 않습니다 루프).
- 플레이어는 사용자 인터페이스에서 컨트롤의 전체 집합을 표시합니다.
- 창에서 비디오를 재생합니다.

### <a name="the-silverlight-player"></a>Silverlight 플레이어

합니다 `Silverlight` 플레이어의 합니다 `Video` 도우미를 사용 하면 Windows Media 비디오를 재생할 수 있습니다 (*.wmv* 파일), Windows Media 오디오 (*.wma* 파일), 및 MP3 (*. mp3* 파일)입니다. Silverlight 기반 응용 프로그램 패키지를 가리키도록 path 매개 변수를 설정 해야 합니다 (*.xap* 파일). 또한 width 및 height 매개 변수를 설정 해야 합니다. 다른 모든 매개 변수는 선택적 요소입니다. 를 사용 하면 Silverlight 플레이어 비디오에 대 한 필수 매개 변수를 설정한 경우 Silverlight 플레이어 배경 색을 사용 하지 않고 비디오를 표시 합니다.

> [!NOTE]
> Silverlight 아직 모르는 경우:를 *.xap* 파일은 압축 된 파일의 레이아웃 지침을 포함 하는 *.xaml* 파일, 어셈블리 및 선택적 리소스에서 관리 되는 코드입니다. 만들 수 있습니다는 *.xap* Silverlight 응용 프로그램 프로젝트와 Visual Studio에서 파일입니다.


합니다 `Silverlight` 비디오 플레이어 모두 플레이어를 제공 하는 설정 및에서 제공 되는 설정을 사용 합니다 *.xap* 파일입니다.

> [!TIP] 
> 
> <a id="SB_MimeTypes"></a>
> ### <a name="mime-types"></a>MIME 형식
> 
> 브라우저 파일을 다운로드 하는 경우 브라우저 파일 형식을 렌더링 되는 문서에 지정 된 MIME 형식과 일치 하는지 검사 합니다. MIME 유형 파일의 콘텐츠 유형 또는 미디어 형식이입니다. `Video` 도우미 다음 MIME 형식을 사용 합니다.
> 
> - `application/x-shockwave-flash`
> - `application/x-mplayer2`
> - `application/x-silverlight-2`


<a id="Playing_Flash"></a>
## <a name="playing-flash-swf-videos"></a>(.Swf) 플래시 비디오 재생

이 절차에서는 라는 플래시 비디오를 재생 하는 방법을 보여 줍니다 *sample.swf*합니다. 이 절차에서는 폴더로 했는지를 가정 *미디어* 사이트에는 *.swf* 파일은 해당 폴더에.

1. 에 설명 된 대로 웹 사이트에 ASP.NET Web Helpers Library를 추가 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372)추가 하지 않은 경우.
2. 웹 사이트에서 페이지를 추가 하 고 이름을 *FlashVideo.cshtml*합니다.
3. 페이지에 다음 태그를 추가 합니다. 

    [!code-cshtml[Main](10-working-with-video/samples/sample2.cshtml)]
4. 브라우저에서 페이지를 실행 합니다. (페이지에서 선택한 있는지 확인 합니다 **파일** 실행 하기 전에 작업 영역입니다.) 페이지가 표시 됩니다 및 비디오가 자동으로 재생 합니다. 

    ![[image]](10-working-with-video/_static/image1.jpg "ch08_video-1.jpg")

설정할 수 있습니다 합니다 `quality` 는 플래시 비디오에 대 한 매개 변수 `low`, `autolow`, `autohigh`를 `medium`를 `high`, 및 `best`:

[!code-cshtml[Main](10-working-with-video/samples/sample3.cshtml)]

플래시 비디오 재생 사용 하 여 특정 크기를 변경할 수 있습니다는 `scale` 매개 변수를 다음으로 설정할 수 있습니다.

- `showall`. 이렇게 하면 원래 가로 세로 비율을 유지 하면서 표시 전체 비디오. 그러나 각 면에 테두리가 있는 게 될 수 있습니다.
- `noorder`. 원래 가로 세로 비율을 유지 하면서 비디오 크기를 조정 하지만 잘릴 수 있습니다.
- `exactfit`. 이렇게 하면 전체 비디오가 표시 원래 가로 세로 비율을 유지 하지 않고 있지만 왜곡이 발생할 수 있습니다.

지정 하지 않으면는 `scale` 매개 변수를 전체 비디오를 볼 수 있습니다 및 자르기 없이 원래 가로 세로 비율이 유지 됩니다. 다음 예제에서는 사용 하는 방법의 `scale` 매개 변수:

[!code-cshtml[Main](10-working-with-video/samples/sample4.cshtml)]

Flash player 명명 된 설정 비디오 모드를 지원 `windowMode`합니다. 이 설정할 수 있습니다 `window`, `opaque`, 및 `transparent`합니다. 기본적으로 `windowMode` 로 설정 된 `window`, 웹 페이지에서 별도 창에서 비디오를 표시 하는 합니다. `opaque` 설정은 웹 페이지에 있는 비디오 뒤에 있는 모든 항목을 숨깁니다. `transparent` 설정을 통해 비디오를 통해 표시 하는 웹 페이지의 배경을 비디오의 모든 부분은 투명 한 것으로 가정 합니다.

<a id="Playing_MediaPlayer"></a>
## <a name="playing-mediaplayer-wmv-videos"></a>MediaPlayer 재생 (*.wmv*) 비디오

다음 절차에서는 명명 된 창 Media 비디오를 재생 하는 방법을 보여 줍니다 *sample.wmv* 에 *미디어* 폴더입니다.

1. 에 설명 된 대로 웹 사이트에 ASP.NET Web Helpers Library를 추가 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372), 아직 없는 경우.
2. 라는 새 페이지를 만듭니다 *MediaPlayerVideo.cshtml*합니다.
3. 페이지에 다음 태그를 추가 합니다. 

    [!code-cshtml[Main](10-working-with-video/samples/sample5.cshtml)]
4. 브라우저에서 페이지를 실행 합니다. 비디오를 로드 하 고 자동으로 재생 합니다. 

    ![[image]](10-working-with-video/_static/image2.jpg "ch08_video-2.jpg")

설정할 수 있습니다 `playCount` 에 비디오를 자동으로 재생 횟수를 나타내는 정수입니다.

[!code-cshtml[Main](10-working-with-video/samples/sample6.cshtml)]

`uiMode` 매개 변수를 사용 하면 컨트롤 사용자 인터페이스에 표시를 지정 합니다. 설정할 수 있습니다 `uiMode` 하 `invisible`를 `none`를 `mini`, 또는 `full`합니다. 지정 하지 않으면는 `uiMode` 매개 변수를 비디오 됩니다 검색 상태 창을 사용 하 여 표시 가로 막대형, 단추 및 비디오 창과 함께 볼륨 컨트롤을 제어 합니다. 이러한 컨트롤은 오디오 파일을 재생 하려면 플레이어를 사용 하는 경우에 표시 됩니다. 사용 하는 방법의 예로 `uiMode` 매개 변수:

[!code-cshtml[Main](10-working-with-video/samples/sample7.cshtml)]

기본적으로 오디오의 경우 비디오 재생 합니다. 설정 하 여 오디오 음소거 할 수 있습니다는 `mute` true 매개 변수:

[!code-cshtml[Main](10-working-with-video/samples/sample8.cshtml)]

MediaPlayer 비디오의 오디오 수준을 설정 하 여 제어할 수 있습니다는 `volume` 0과 100 사이의 값으로 매개 변수입니다. 기본값은 50입니다. 예를 들면 다음과 같습니다.

[!code-cshtml[Main](10-working-with-video/samples/sample9.cshtml)]

<a id="Playing_Silverlight"></a>
## <a name="playing-silverlight-videos"></a>Silverlight 비디오 재생

이 절차에서는 Silverlight에 포함 된 비디오를 재생 하는 방법을 보여 줍니다 *.xap* 이라는 폴더에는 페이지 *미디어*합니다.

1. 에 설명 된 대로 웹 사이트에 ASP.NET Web Helpers Library를 추가 [ASP.NET 웹 페이지 사이트에서 설치 도우미](https://go.microsoft.com/fwlink/?LinkId=252372), 아직 없는 경우.
2. 라는 새 페이지를 만듭니다 *SilverlightVideo.cshtml*합니다.
3. 페이지에 다음 태그를 추가 합니다. 

    [!code-cshtml[Main](10-working-with-video/samples/sample10.cshtml)]
4. 브라우저에서 페이지를 실행 합니다. 

    ![[image]](10-working-with-video/_static/image3.jpg "ch08_video-3.jpg")

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스


[Silverlight 개요](https://msdn.microsoft.com/library/bb404700(VS.95).aspx)

[플래시 개체와 EMBED 태그 특성](http://kb2.adobe.com/cps/127/tn_12701.html)

[Windows Media Player 11 SDK PARAM 태그](https://msdn.microsoft.com/library/aa392321(VS.85).aspx)
