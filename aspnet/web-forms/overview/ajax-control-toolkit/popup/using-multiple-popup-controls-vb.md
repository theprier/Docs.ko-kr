---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
title: "여러 개의 팝업 컨트롤이 (VB)를 사용 하 여 | Microsoft Docs"
author: wenz
description: "에 들어 PopupControl extender 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수 있는 방법을 제공 합니다. M을 사용 하는 것도 가능 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 4da43d77-f6c4-43a8-9124-f1e8e1c8f0a2
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 32e170ebd78a6f849004e789f53c03d9cd40be01
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="using-multiple-popup-controls-vb"></a>여러 개의 팝업 컨트롤이 (VB)를 사용 하 여
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1VB.pdf)

> 에 들어 PopupControl extender 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수 있는 방법을 제공 합니다. 도 한 페이지에 둘 이상의 popup 컨트롤을 사용 하는 것이 가능 합니다.


## <a name="overview"></a>개요

에 들어 PopupControl extender 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수 있는 방법을 제공 합니다. 도 한 페이지에 둘 이상의 popup 컨트롤을 사용 하는 것이 가능 합니다.

## <a name="steps"></a>단계

ASP.NET AJAX 및 제어 Toolkit의 기능을 활성화 하는 데는 `ScriptManager` 제어 페이지에서 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample1.aspx)]

다음으로, 팝업으로 사용 되는 패널을 추가 합니다. 패널에 포함 된 현재 시나리오에는 `Calendar` 제어 합니다. 달력의 포스트백에서 발생 한 페이지 새로 고침을 방지 하기 위해 패널은 내에 배치 된 `UpdatePanel` 제어:

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample2.aspx)]

또한이 페이지는 두 개의 텍스트 상자 포함 합니다. 각 텍스트 상자에 텍스트 상자가 활성화 되 면 일정 팝업 표시 합니다.

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample3.aspx)]

이제 각와 두 개의 텍스트 상자를 확장 한 `PopupControlExtender`합니다. `TargetControlID` 특성은 extender에 연결 된 컨트롤의 ID를 제공 합니다. `PopupControlID` 특성 팝업 패널의 ID를 포함 합니다. 이 경우 두 extender 같은 패널 표시 되지만 다른 패널은도 가능 합니다.

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample4.aspx)]

이제 텍스트 필드 내에서 클릭할 때마다 일정 필드 아래에 표시, 날짜를 선택할 수 있습니다. (텍스트 상자로 선택한 날짜를 다시 가져오는 다룰 예정 다른 자습서를 참조 합니다.)


[![입력란에 사용자가 클릭 하면 달력이 나타납니다.](using-multiple-popup-controls-vb/_static/image2.png)](using-multiple-popup-controls-vb/_static/image1.png)

입력란에 사용자가 클릭 하면 달력이 나타납니다 ([전체 크기 이미지를 보려면 클릭](using-multiple-popup-controls-vb/_static/image3.png))

>[!div class="step-by-step"]
[이전](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
[다음](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)
