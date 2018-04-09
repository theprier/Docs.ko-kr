---
uid: web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
title: 데이터 바인딩 슬라이더 컨트롤 (VB) | Microsoft Docs
author: wenz
description: 슬라이더 컨트롤 들어에서 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다. 현재 positio 바인딩할 수는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 4f3ba53f-d166-422d-b29c-403348057836
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 3ecd8598cd7fdcbbb4812e501bb30fa1f563a054
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="databinding-the-slider-control-vb"></a>데이터 바인딩 (VB) 슬라이더 컨트롤
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0VB.pdf)

> 슬라이더 컨트롤 들어에서 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다. 슬라이더의 현재 위치를 다른 ASP.NET 컨트롤 바인딩할 것 같습니다.


## <a name="overview"></a>개요

슬라이더 컨트롤 들어에서 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다. 슬라이더의 현재 위치를 다른 ASP.NET 컨트롤 바인딩할 것 같습니다.

## <a name="steps"></a>단계

ASP.NET AJAX 및 제어 Toolkit의 기능을 활성화 하는 데는 `ScriptManager` 제어 페이지에서 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample1.aspx)]

다음으로, 두 개의 추가 `TextBox` 페이지 컨트롤입니다. 그래픽 슬라이더도 변환 됨 하나 길게 다른 하나는 슬라이더의 위치.

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample2.aspx)]

다음 단계는 이미 마지막 단계가입니다. `SliderExtender` ASP.NET AJAX 컨트롤 도구 키트에서 첫 번째 텍스트 상자에서 슬라이더를 사용 하면 컨트롤과 슬라이더 위치가 변경 될 때 두 번째 텍스트 상자를 자동으로 업데이트 합니다. 작업을 위해서는 되려면는 `SliderExtender`의 `TargetControlID` 특성의 첫 번째 텍스트 상자; ID로 설정 해야 합니다는 `BoundControlID` 특성을 두 번째 텍스트 상자의 ID로 설정 해야 합니다.

[!code-aspx[Main](databinding-the-slider-control-vb/samples/sample3.aspx)]

데이터 바인딩은 양방향에서 작동 브라우저에 보시: 슬라이더의 위치를 업데이트 하 고 텍스트 상자에 새 값을 입력 합니다. 읽기 전용 두 번째 텍스트 상자를 설정 하 여 사용자가 수동으로 거기에 값을 업데이트 하는 것이 어렵다는 텍스트 필드에 암호 보호를 추가할 수 있습니다.


[![동기화 되어 슬라이더와 텍스트 상자](databinding-the-slider-control-vb/_static/image2.png)](databinding-the-slider-control-vb/_static/image1.png)

슬라이더와 텍스트 상자에 동기화 되었는지 ([전체 크기 이미지를 보려면 클릭](databinding-the-slider-control-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](using-the-slider-control-with-auto-postback-vb.md)
