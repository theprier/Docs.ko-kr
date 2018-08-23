---
uid: web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-cs
title: 축소 및 확장 (C#) JavaScript에서 패널 | Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit의 CollapsiblePanel 컨트롤 패널을 확장 하 고 해당 콘텐츠를 축소 하 고 확장 하는 기능을 사용 하 여 제공을 하는 중...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: de5500be-75e5-461a-8064-b70ae52ea6a4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-cs
msc.type: authoredcontent
ms.openlocfilehash: 325194fc1f980714ea2fc26cfaa13d86ae9d2f89
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41839145"
---
<a name="collapsing-and-expanding-a-panel-from-javascript-c"></a>확장 및 JavaScript (C#)에서 패널 축소
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1CS.pdf)

> ASP.NET AJAX Control Toolkit의 CollapsiblePanel 컨트롤 패널을 확장 하 고 해당 콘텐츠를 축소 하 고 다시 확장 하는 기능을 사용 하 여 제공 됩니다. 사용자 지정 JavaScript 코드에서 이러한 두 작업을 트리거할 수도 있습니다.


## <a name="overview"></a>개요

ASP.NET AJAX Control Toolkit의 CollapsiblePanel 컨트롤 패널을 확장 하 고 해당 콘텐츠를 축소 하 고 다시 확장 하는 기능을 사용 하 여 제공 됩니다. 사용자 지정 JavaScript 코드에서 이러한 두 작업을 트리거할 수도 있습니다.

## <a name="steps"></a>단계

먼저, 새 ASP.NET 페이지를 만들고 포함 된 `ScriptManager` 것 내 `<form>` 요소. 이 컨트롤 도구 키트에 필요한 ASP.NET AJAX 라이브러리를 로드 합니다.

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample1.aspx)]

그런 다음 확장/축소 효과 볼 수 있도록 일부 텍스트를 사용 하 여 패널을 만듭니다.

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample2.aspx)]

알 수 있듯이 패널에는 다음과 같습니다 (및 기본적으로 패널의 너비 및 배경색을 정의)는 CSS 클래스를 참조 합니다.

[!code-css[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample3.css)]

합니다 `CollapsiblePanelExtender` 컨트롤에 필요 합니다 `TargetControlID` 도구 키트에서 요청 시 확장 하거나 축소 패널을 알 수 있도록 특성:

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample4.aspx)]

아쉽게도 현재 extender 패널을 확장 또는 축소에 대 한 특정 API를 노출 하지 않습니다 하지만 문서화 되지 않은 몇 가지 방법을 수행 됩니다. 먼저, 패널의 콘텐츠를 확장 하거나 축소 하는 클라이언트 쪽 JavaScript 트리거할 다음 페이지로 세 개의 HTML 단추를 추가 합니다.

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample5.aspx)]

클라이언트 쪽 JavaScript 코드에서 (시작 `<script type="text/javascript">`), `$find()` 메서드를 사용 해야 합니다. 액세스를 `CollapsiblePanelExtender`입니다. `$find("cpe")` 에 대 한 참조를 반환 됩니다. 거기서부터 특정 메서드는 작업에 해결 됩니다.

메서드 (확장)를 열기 위한 패널 이라고 `_doOpen()`; 다음 구현 코드를 `doOpen()` 함수는 첫 번째 단추를 클릭할 때 호출:

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample6.js)]

패널을 축소 하거나 닫거나에 대 한는 `_doClose()` 메서드를 실행 해야 합니다. 따라서 사용자가 두 번째 단추를 클릭 하면 다음 JavaScript 코드 라고 합니다.

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample7.js)]

패널의 상태를 전환 하는 세 번째 단추:에서 축소 하 여 확장 하 고 그 반대의 경우도 마찬가지입니다. `CollapsiblePanelExtender` 노출 된 `toggle()` 정확히 일치 하는 메서드: 패널의 상태를 반대로 바꿉니다. 그러나도 또 다른 방법이 있습니다 (에서 내부적으로 사용 되는 `toggle()` 메서드): 합니다 `get_Collapsed()` 메서드의 `CollapsiblePanelExtender()` 패널 축소 되는지 여부를 알려줍니다. 이 함수의 반환 값에 따라 패널 인 확장 중 하나 (`_doOpen()` 메서드) 또는 축소 (`_doClose()`) 메서드.

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample8.js)]


[![패널의 상태를 변경 하는 세 번째 단추:에서 확장 및 다시 축소](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image1.png)

패널의 상태를 변경 하는 세 번째 단추:에서 축소 하 여 확장 하 고 백 ([클릭 하 여 큰 이미지 보기](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image3.png))

> [!div class="step-by-step"]
> [다음](collapsing-and-expanding-a-panel-from-javascript-vb.md)
