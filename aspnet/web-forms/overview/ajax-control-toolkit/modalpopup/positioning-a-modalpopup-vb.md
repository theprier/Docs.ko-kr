---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-vb
title: 배치 ModalPopup (VB) | Microsoft Docs
author: wenz
description: 들어에서 ModalPopup 컨트롤을 클라이언트 쪽 방법을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 그러나 컨트롤을 제공 하지 않습니다는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 8a07210c-eb0e-485e-9ee8-82a101520e65
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-vb
msc.type: authoredcontent
ms.openlocfilehash: 2d20888674dfedee7a7af85efd8df118c8394c6c
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30874618"
---
<a name="positioning-a-modalpopup-vb"></a>ModalPopup (VB) 위치 지정
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4VB.pdf)

> 들어에서 ModalPopup 컨트롤을 클라이언트 쪽 방법을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 그러나 컨트롤의 팝업 위치를 기본 제공 기능을 제공 하지 않습니다.


## <a name="overview"></a>개요

들어에서 ModalPopup 컨트롤을 클라이언트 쪽 방법을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 그러나 컨트롤의 팝업 위치를 기본 제공 기능을 제공 하지 않습니다.

## <a name="steps"></a>단계

ASP.NET AJAX 및 제어 Toolkit의 기능을 활성화 하는 데는 `ScriptManager`합니다. 제어 페이지에서 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample1.aspx)]

다음으로 모달 팝업으로 사용 되는 패널을 추가 합니다. 단추는 팝업을 닫습니다 ï ´ ù.

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample2.aspx)]

팝업이 표시 될 때마다 페이지에서 특정 위치에 배치 해야 합니다. 이 작업에 대 한 클라이언트 쪽 JavaScript 함수가 생성 됩니다. 먼저 패널에 액세스 하려고 합니다. 성공 하면 패널의 위치는 CSS 및 JavaScript (팝업에서의 위치는 변경)를 사용 하 여 설정 됩니다. 그러나 `ModalPopupExtender` 컨트롤이 또한 팝업 배치 하려고 합니다. 따라서 JavaScript 코드를 반복 해 서 초의 1/10 마다 팝업을 배치합니다.

[!code-html[Main](positioning-a-modalpopup-vb/samples/sample3.html)]

볼 수 있듯이의 반환 값은 `setTimeout()` JavaScript 메서드는 전역 변수에 저장 됩니다. 따라서 필요에 따라 팝업의 반복 된 배치 중지를 사용 하는 `clearTimeout()` 메서드:

[!code-javascript[Main](positioning-a-modalpopup-vb/samples/sample4.js)]

이제을 마지막으로 하는 필요에 따라 이러한 함수를 호출 하는 브라우저를 확인 합니다. `movePanel()` 패널을 트리거하는 단추를 클릭할 때 JavaScript 함수를 호출 해야 합니다.

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample5.aspx)]

및 `stopMoving()` 팝업을 닫을 수이 있습니다 하는 경우에 발생 되는 함수에서 트리거할 수는 `ModalPopupExtender` 제어:

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample6.aspx)]


[![지정 된 위치에 모달 팝업 표시](positioning-a-modalpopup-vb/_static/image2.png)](positioning-a-modalpopup-vb/_static/image1.png)

지정 된 위치에 모달 팝업 표시 ([전체 크기 이미지를 보려면 클릭](positioning-a-modalpopup-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](handling-postbacks-from-a-modalpopup-vb.md)
