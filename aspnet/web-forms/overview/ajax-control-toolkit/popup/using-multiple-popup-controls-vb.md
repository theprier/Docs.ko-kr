---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
title: 여러 팝업 컨트롤 (VB)를 사용 하 여 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit의 PopupControl extender는 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수를 제공 합니다. M을 사용 하는 것도 가능...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: 4da43d77-f6c4-43a8-9124-f1e8e1c8f0a2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 5a2be36ecf17a95d53e5e912ba0a90113f70f2fb
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37807637"
---
<a name="using-multiple-popup-controls-vb"></a>여러 팝업 컨트롤 (VB)를 사용 하 여
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1VB.pdf)

> AJAX Control Toolkit의 PopupControl extender는 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수를 제공 합니다. 도 한 페이지에 둘 이상의 팝업 컨트롤을 사용 하는 것이 가능 합니다.


## <a name="overview"></a>개요

AJAX Control Toolkit의 PopupControl extender는 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수를 제공 합니다. 도 한 페이지에 둘 이상의 팝업 컨트롤을 사용 하는 것이 가능 합니다.

## <a name="steps"></a>단계

ASP.NET AJAX와 Control Toolkit의 기능을 활성화 하기 위해 합니다 `ScriptManager` 컨트롤 페이지의 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample1.aspx)]

다음으로, 팝업으로 사용 되는 패널을 추가 합니다. 패널에 현재 시나리오에는 `Calendar` 제어 합니다. 달력의 포스트백에서 발생 한 페이지 새로 고침을 피하기 위해 패널 내에서 것을 `UpdatePanel` 제어:

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample2.aspx)]

페이지에는 두 개의 텍스트 상자가 포함 되어 있습니다. 각 텍스트 상자에 텍스트 상자가 활성화 되 면 달력 팝업을 표시 합니다.

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample3.aspx)]

이제 각 사용 하 여 두 텍스트 상자를 확장 하는 `PopupControlExtender`합니다. `TargetControlID` 특성 extender에 연결 된 컨트롤의 ID를 제공 합니다. `PopupControlID` 특성 팝업 패널의 ID를 포함 합니다. 이 경우 모두 extender는 같은 패널을 표시 하지만 다른 패널도 가능 합니다.

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample4.aspx)]

이제 텍스트 필드 내에서 클릭할 때마다 일정 필드 아래에 표시에서 날짜를 선택할 수 있습니다. (텍스트 상자에 선택한 날짜를 다시 시작에서 다룰 다양 한 자습서입니다.)


[![텍스트 상자에 사용자가 클릭 하면 달력이 나타납니다.](using-multiple-popup-controls-vb/_static/image2.png)](using-multiple-popup-controls-vb/_static/image1.png)

텍스트 상자에 사용자가 클릭 하면 달력이 나타납니다 ([클릭 하 여 큰 이미지 보기](using-multiple-popup-controls-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
> [다음](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)
