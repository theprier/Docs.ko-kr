---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-cs
title: UpdatePanel (C#)와 Popup 컨트롤의 포스트백 처리 | Microsoft Docs
author: wenz
description: 에 들어 PopupControl extender 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수 있는 방법을 제공 합니다. 특별 한 주의 만들어야 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 1f68f59d-9c1e-4cf3-b304-c13ae6b7203e
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: abedb5247f710b02752651a7bfb011ab63d32844
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="handling-postbacks-from-a-popup-control-with-an-updatepanel-c"></a>UpdatePanel (C#)와 Popup 컨트롤에서 포스트백을 처리합니다.
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2CS.pdf)

> 에 들어 PopupControl extender 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수 있는 방법을 제공 합니다. 특별 한 주의 이러한 팝업 내의 포스트백이 발생할 때 수행할에 있습니다.


## <a name="overview"></a>개요

에 들어 PopupControl extender 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수 있는 방법을 제공 합니다. 특별 한 주의 이러한 팝업 내의 포스트백이 발생할 때 수행할에 있습니다.

## <a name="steps"></a>단계

사용 하는 경우는 `PopupControl` 포스트백에서는 `UpdatePanel` 포스트백 페이지 새로 고침 하지 못할 수 있습니다. 다음 태그 몇 가지 중요 한 요소를 정의합니다.

- A `ScriptManager` ASP.NET AJAX 컨트롤 도구 키트 작동 되도록
- 두 개의 `TextBox` 팝업 트리거되고 둘 다 컨트롤
- A `Panel` 팝업 기호로 사용할 컨트롤
- 패널 내에서 한 `Calendar` 컨트롤 내에 포함 되는 `UpdatePanel` 컨트롤
- 두 개의 `PopupControlExtender` 패널에서 텍스트 상자에 할당 하는 컨트롤

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/samples/sample1.aspx)]

`OnSelectionChanged` 특성에는 `Calendar` 컨트롤 설정 합니다. 포스트백이 발생할 때 사용자가 달력에서 날짜를 선택 하도록 하 고 서버 쪽 메서드 `c1_SelectionChanged()` 실행 됩니다. 이 메서드 내에 현재 날짜를 검색 하 고 텍스트 상자에 다시 기록 수 해야 합니다.

에 대 한 구문은 다음과 같습니다: 우선, 프록시 개체에 대 한는 `PopupControlExtender` 페이지 생성 해야 합니다. ASP.NET AJAX 컨트롤 도구 키트는 제공 된 `GetProxyForCurrentPopup()` 메서드. 이 메서드가 반환 개체가 지 원하는 `Commit()` 다시 팝업 (컨트롤이 아님 메서드 호출을 트리거한!)를 발생 시킨 컨트롤에 값을 전송 하는 메서드. 다음 코드에서는 선택된 된 날짜에 대 한 인수로 `Commit()` 메서드, 텍스트 상자에 선택된 된 날짜를 다시 작성 하기 위해 코드:

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/samples/sample2.aspx)]

이제 클릭할 때마다 달력 날짜 관련된 텍스트 상자에 선택 된 날짜가 나타납니다 날짜 선택 컨트롤을 만드는 현재 있습니다 많은 웹 사이트에서.


[![입력란에 사용자가 클릭 하면 달력이 나타납니다.](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image1.png)

입력란에 사용자가 클릭 하면 달력이 나타납니다 ([전체 크기 이미지를 보려면 클릭](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image3.png))


[![날짜를 클릭 하면 텍스트 상자에 전환](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image4.png)

날짜를 클릭 하면 텍스트 상자에 전환 ([전체 크기 이미지를 보려면 클릭](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image6.png))

> [!div class="step-by-step"]
> [이전](using-multiple-popup-controls-cs.md)
> [다음](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
