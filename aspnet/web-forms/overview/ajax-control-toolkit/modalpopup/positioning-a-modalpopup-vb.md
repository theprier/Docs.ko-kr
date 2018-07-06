---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-vb
title: (VB) ModalPopup 위치 지정 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit의 ModalPopup 컨트롤 클라이언트 쪽 의미를 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 그러나 컨트롤을 제공 하지 않습니다는 중...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: 8a07210c-eb0e-485e-9ee8-82a101520e65
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-vb
msc.type: authoredcontent
ms.openlocfilehash: e36d22b5c2f503ed849f373153e263bdd9546452
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37821763"
---
<a name="positioning-a-modalpopup-vb"></a>(VB) ModalPopup 위치 지정
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4VB.pdf)

> AJAX Control Toolkit의 ModalPopup 컨트롤 클라이언트 쪽 의미를 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 그러나 컨트롤은 팝업의 위치는 기본 제공 기능을 제공 하지 않습니다.


## <a name="overview"></a>개요

AJAX Control Toolkit의 ModalPopup 컨트롤 클라이언트 쪽 의미를 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 그러나 컨트롤은 팝업의 위치는 기본 제공 기능을 제공 하지 않습니다.

## <a name="steps"></a>단계

ASP.NET AJAX와 Control Toolkit의 기능을 활성화 하기 위해는 `ScriptManager`합니다. 컨트롤 페이지의 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소).

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample1.aspx)]

다음으로 모달 팝업으로 사용 되는 패널을 추가 합니다. 단추는 팝업을 닫는 데 사용 됩니다.

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample2.aspx)]

팝업이 표시 될 때마다 페이지에는 특정 위치에 배치 됩니다. 이 태스크에 대 한 클라이언트 쪽 JavaScript 함수가 만들어집니다. 패널에 액세스 하려면 먼저 시도 합니다. 성공 하면 패널의 위치는 CSS 및 JavaScript (에서 팝업의 위치는 변경)를 사용 하 여 설정 됩니다. 그러나 `ModalPopupExtender` 제어도 팝업 배치 하려고 시도 합니다. 따라서 JavaScript 코드를 반복적으로 팝업 0.1 초 마다 배치합니다.

[!code-html[Main](positioning-a-modalpopup-vb/samples/sample3.html)]

알 수 있듯이의 반환 값은 `setTimeout()` JavaScript 메서드는 전역 변수에 저장 됩니다. 이렇게 하면 요청 시 팝업의 위치 지정 반복을 중지 하려면 사용 하는 `clearTimeout()` 메서드:

[!code-javascript[Main](positioning-a-modalpopup-vb/samples/sample4.js)]

이제 위해 남아 있는 모든 적절 한 때마다 이러한 함수를 호출 하는 브라우저를 확인 하는 것입니다. `movePanel()` 패널을 트리거하는 단추를 클릭할 때 JavaScript 함수를 호출 해야 합니다.

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample5.aspx)]

하며 `stopMoving()` 팝업이이 있습니다 닫힐 때 함수 고려해 야 트리거할 수는 `ModalPopupExtender` 제어:

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample6.aspx)]


[![지정 된 위치에서 모달 팝업 표시](positioning-a-modalpopup-vb/_static/image2.png)](positioning-a-modalpopup-vb/_static/image1.png)

모달 팝업에 지정 된 위치에 있는 표시 되는 경우 ([클릭 하 여 큰 이미지 보기](positioning-a-modalpopup-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](handling-postbacks-from-a-modalpopup-vb.md)
