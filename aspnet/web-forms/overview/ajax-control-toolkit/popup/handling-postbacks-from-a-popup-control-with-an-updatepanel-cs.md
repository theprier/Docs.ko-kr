---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-cs
title: UpdatePanel (C#)를 사용 하 여 팝업 컨트롤에서 포스트백 처리 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit의 PopupControl extender는 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수를 제공 합니다. 특별 한 주의 수행 해야 하는 중...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1f68f59d-9c1e-4cf3-b304-c13ae6b7203e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: 0f886ba0f3e79bc6d5daf193eaedfd627bc9b937
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831543"
---
<a name="handling-postbacks-from-a-popup-control-with-an-updatepanel-c"></a>UpdatePanel (C#)를 사용 하 여 팝업 컨트롤에서 포스트백 처리
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2CS.pdf)

> AJAX Control Toolkit의 PopupControl extender는 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수를 제공 합니다. 특별 한 주의 이러한 팝업에 포스트백이 발생할 때 주의 해야 합니다.


## <a name="overview"></a>개요

AJAX Control Toolkit의 PopupControl extender는 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수를 제공 합니다. 특별 한 주의 이러한 팝업에 포스트백이 발생할 때 주의 해야 합니다.

## <a name="steps"></a>단계

사용 하는 경우는 `PopupControl` 포스트백을 사용 하 여는 `UpdatePanel` 포스트백 페이지 새로 방지할 수 있습니다. 다음 태그는 몇 가지 중요 한 요소를 정의합니다.

- `ScriptManager` ASP.NET AJAX Control Toolkit 작동할 수 있도록 제어
- 두 `TextBox` 팝업 모두 트리거할 컨트롤
- `Panel` 팝업 사용할 컨트롤
- 패널 내에서 한 `Calendar` 컨트롤 내에 포함 되는 `UpdatePanel` 컨트롤
- 두 `PopupControlExtender` 패널의 텍스트 상자에 할당 하는 컨트롤

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/samples/sample1.aspx)]

`OnSelectionChanged` 특성을 `Calendar` 컨트롤 설정. 포스트백이 발생할 때 사용자가 달력의 날짜를 선택 하도록 하 고 서버 측 메서드 `c1_SelectionChanged()` 실행 됩니다. 이 메서드 내에 현재 날짜를 검색 하 고 텍스트 상자에 다시 쓸 수 해야 합니다.

에 대 한 구문은 다음과 같습니다: 먼저 모든 프록시에 대 한 개체는 `PopupControlExtender` 페이지에서 생성 해야 합니다. ASP.NET AJAX Control Toolkit에서 제공 된 `GetProxyForCurrentPopup()` 메서드. 이 메서드는 반환 된 개체에서 지원 합니다 `Commit()` 메서드 (컨트롤 아니라 메서드 호출을 트리거한!) 팝업을 트리거한 컨트롤에 다시 값을 보냅니다. 다음 코드에서는 선택된 된 날짜에 대 한 인수로 `Commit()` 메서드를 텍스트 상자에 선택한 날짜를 다시 작성 하는 코드를 발생 합니다.

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/samples/sample2.aspx)]

이제 클릭할 때마다 달력 날짜를 관련된 텍스트 상자에 표시할 선택한 날짜는 날짜 선택 컨트롤 만들기 현재 있습니다 많은 웹 사이트에서.


[![텍스트 상자에 사용자가 클릭 하면 달력이 나타납니다.](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image1.png)

텍스트 상자에 사용자가 클릭 하면 달력이 나타납니다 ([클릭 하 여 큰 이미지 보기](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image3.png))


[![날짜를 클릭 하면 텍스트 상자에 전환](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image4.png)

날짜를 클릭 하면 텍스트 상자에 배치 ([클릭 하 여 큰 이미지 보기](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image6.png))

> [!div class="step-by-step"]
> [이전](using-multiple-popup-controls-cs.md)
> [다음](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
