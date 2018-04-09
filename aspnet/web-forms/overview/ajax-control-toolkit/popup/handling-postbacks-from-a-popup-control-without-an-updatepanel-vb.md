---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
title: UpdatePanel (VB) 없이 Popup 컨트롤의 포스트백 처리 | Microsoft Docs
author: wenz
description: 에 들어 PopupControl extender 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수 있는 방법을 제공 합니다. 포스트백 su에서 발생 하면...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: a0b9186c-0912-4fff-916a-6d17e696a50b
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: c92083d4a57067c7b646721f21af059fc1e1e7d9
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-vb"></a>UpdatePanel (VB) 없이 Popup 컨트롤에서 포스트백을 처리합니다.
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3VB.pdf)

> 에 들어 PopupControl extender 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수 있는 방법을 제공 합니다. 이러한 패널에 포스트백이 발생할 때 여러 패널은 페이지에는 어떤 패널 클릭 했는지 확인 하려면 어렵습니다.


## <a name="overview"></a>개요

에 들어 PopupControl extender 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수 있는 방법을 제공 합니다. 이러한 패널에 포스트백이 발생할 때 여러 패널은 페이지에는 어떤 패널 클릭 했는지 확인 하려면 어렵습니다.

## <a name="steps"></a>단계

사용 하는 경우는 `PopupControl` 포스트백 있지만 필요 없이 `UpdatePanel` 페이지 컨트롤 Toolkit 클라이언트 요소에 포스트백을 실행 하는 팝업을 트리거 했습니다. 결정 하는 방법을 제공 하지 않습니다. 그러나 작은 트릭이이 시나리오에 대 한 해결 방법을 제공 합니다.

우선, 기본 설정 같습니다:이 두 가지 동일한 팝업 일정을 트리거하는 두 개의 텍스트 상자입니다. 두 개의 `PopupControlExtenders` 텍스트 상자 및 팝업 모읍니다.

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample1.aspx)]

기본 개념에는 숨겨진된 폼 필드를 추가 하는 것은 &lt; `form` &gt; 팝업을 시작 하 고 텍스트 상자에 포함 된 요소:

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample2.aspx)]

JavaScript 코드 두 텍스트 상자에 이벤트 처리기를 추가 하는 페이지가 로드 되 면: 숨겨진된 폼 필드에 기록 된 해당 이름 때마다 사용자가 텍스트 상자를 클릭 합니다.

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample3.html)]

서버 쪽 코드에 숨겨진된 필드의 값을 읽을 수 해야 합니다. 숨겨진된 양식 필드와 조작 하기 위한 간단한 되므로 허용 목록에서 숨겨진된 값을 검사할 방법은 필요 합니다. 올바른 입력란을 식별 한 후 달력에서 날짜 데이터베이스에 기록 됩니다.

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/samples/sample4.aspx)]


[![입력란에 사용자가 클릭 하면 달력이 나타납니다.](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image1.png)

입력란에 사용자가 클릭 하면 달력이 나타납니다 ([전체 크기 이미지를 보려면 클릭](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image3.png))


[![날짜를 클릭 하면 텍스트 상자에 전환](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image4.png)

날짜를 클릭 하면 텍스트 상자에 전환 ([전체 크기 이미지를 보려면 클릭](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb/_static/image6.png))

> [!div class="step-by-step"]
> [이전](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)
