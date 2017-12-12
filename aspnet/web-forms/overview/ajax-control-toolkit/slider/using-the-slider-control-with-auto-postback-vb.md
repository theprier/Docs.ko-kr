---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
title: "슬라이더 컨트롤을 사용 하 여 자동 다시 게시 (VB)으로 | Microsoft Docs"
author: wenz
description: "슬라이더 컨트롤 들어에서 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다. 슬라이더 autopost 확인 수는 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 41d1abba-97a5-4a45-9b44-d05624c19777
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
msc.type: authoredcontent
ms.openlocfilehash: fedd3ff947c6f5d5d4d00791087e9fd825fdf9d3
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="using-the-slider-control-with-auto-postback-vb"></a>슬라이더 컨트롤을 사용 하 여 자동 다시 게시 (VB)으로
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1VB.pdf)

> 슬라이더 컨트롤 들어에서 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다. 해당 값이 변경 슬라이더 autopostback를 한 번 확인 수는.


## <a name="overview"></a>개요

슬라이더 컨트롤 들어에서 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다. 해당 값이 변경 슬라이더 autopostback를 한 번 확인 수는.

## <a name="steps"></a>단계

슬라이더를 변경 시 자동으로 다시 게시 하기 위해 두 텍스트 상자에 특성을 추가 해야 `AutoPostBack="true"`: 자체 슬라이더 될 텍스트 상자 및 슬라이더의 위치를 보유 하는 텍스트 상자가 있습니다. 필수 태그에는 다음과 같습니다.

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample1.aspx)]

`SliderExtender` ASP.NET AJAX 컨트롤 도구 키트에서 컨트롤의 두 텍스트 상자에 슬라이더 기능을 할당 합니다.

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample2.aspx)]

추가 레이블 요소 나중에 다시 게시의 사용자에 게에 사용 됩니다.

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample3.aspx)]

마지막으로 `ScriptManager` ASP.NET AJAX의 컨트롤에서 작동 하도록 제어 도구 키트에 대 한 필요한 JavaScript 로드:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample4.aspx)]

슬라이더를 다시; 게시 이제 서버 쪽에서이 이벤트 발생 및 대상이 될 수 있습니다.:

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample5.aspx)]


[![포스트백을 트리거합니다 슬라이더를 이동](using-the-slider-control-with-auto-postback-vb/_static/image2.png)](using-the-slider-control-with-auto-postback-vb/_static/image1.png)

포스트백 트리거합니다 슬라이더를 이동 ([전체 크기 이미지를 보려면 클릭](using-the-slider-control-with-auto-postback-vb/_static/image3.png))


[![이러한 변경의 날짜 레이블이 작성 된 이후에,](using-the-slider-control-with-auto-postback-vb/_static/image5.png)](using-the-slider-control-with-auto-postback-vb/_static/image4.png)

이러한 변경의 날짜 레이블을 작성 된 이후에 ([전체 크기 이미지를 보려면 클릭](using-the-slider-control-with-auto-postback-vb/_static/image6.png))

>[!div class="step-by-step"]
[이전](databinding-the-slider-control-cs.md)
[다음](databinding-the-slider-control-vb.md)
