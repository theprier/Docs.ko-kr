---
uid: web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-cs
title: 확장 및 축소 된 패널 JavaScript (C#)에서 | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트에서 CollapsiblePanel 컨트롤 패널을 확장 하 고 해당 콘텐츠를 축소 및 확장 하는 기능과 제공는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: de5500be-75e5-461a-8064-b70ae52ea6a4
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-cs
msc.type: authoredcontent
ms.openlocfilehash: 7baa3be7144946bde7d11afd9b1cb5f14ad9dede
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30875541"
---
<a name="collapsing-and-expanding-a-panel-from-javascript-c"></a>확장 및 JavaScript (C#)에서 패널 축소
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1CS.pdf)

> 패널을 확장 하 고 해당 콘텐츠를 축소 하 고 다시 확장 하는 기능과 제공 하는 ASP.NET AJAX 컨트롤 도구 키트에서 CollapsiblePanel 제어 합니다. 사용자 지정 JavaScript 코드에서 이러한 두 작업을 트리거할 수도 있습니다.


## <a name="overview"></a>개요

패널을 확장 하 고 해당 콘텐츠를 축소 하 고 다시 확장 하는 기능과 제공 하는 ASP.NET AJAX 컨트롤 도구 키트에서 CollapsiblePanel 제어 합니다. 사용자 지정 JavaScript 코드에서 이러한 두 작업을 트리거할 수도 있습니다.

## <a name="steps"></a>단계

새 ASP.NET 페이지를 만들고 포함 우선,는 `ScriptManager` 한 내 `<form>` 요소입니다. 컨트롤 도구 키트에서 필요한 ASP.NET AJAX 라이브러리를 로드 합니다.

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample1.aspx)]

그런 다음 확장/축소 효과 볼 수 있도록 일부 텍스트와 패널을 만듭니다.

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample2.aspx)]

볼 수 있듯이 패널은 같습니다. (및 기본적으로 배경색 및 패널의 너비를 정의)는 CSS 클래스를 참조 합니다.

[!code-css[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample3.css)]

`CollapsiblePanelExtender` 컨트롤을 사용 하려면는 `TargetControlID` 도구 키트 요청에 따라 확장 하거나 축소 패널을 알 수 있도록 특성:

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample4.aspx)]

그러나 현재 extender 축소 또는 패널을 확장에 대 한 특정 API를 노출 하지 않습니다 하지만 일부 문서화 되지 않은 메서드를 수행 합니다. 우선, 패널의 콘텐츠를 확장 하거나 축소 클라이언트 쪽 JavaScript 트리거되고 다음 페이지에 세 개의 HTML 단추를 추가 합니다.

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample5.aspx)]

클라이언트 쪽 JavaScript 코드에서 (시작 `<script type="text/javascript">`), `$find()` 메서드를 사용 해야 합니다. 액세스 하는 `CollapsiblePanelExtender`합니다. `$find("cpe")` 에 대 한 참조를 반환 합니다. 이 위치에서 관련 메서드는 작업에 해결 됩니다.

메서드가 패널 (확장)을 열기 위해 호출 됩니다 `_doOpen()`; 다음 구현 코드는 `doOpen()` 함수는 첫 번째 단추를 클릭할 때 호출 합니다.

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample6.js)]

패널을 축소 하거나 닫거나에 대 한는 `_doClose()` 메서드를 실행 해야 합니다. 따라서 사용자가 두 번째 단추를 클릭 하면 다음 JavaScript 코드 라고 합니다.

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample7.js)]

세 번째 단추 패널의 상태를 전환:에서 축소 하 여 확장 하 고, 그 반대의 합니다. `CollapsiblePanelExtender` 노출 된 `toggle()` 정확히 일치 하는 메서드: 패널의 상태를 반대로 바꿉니다. 그러나 또한 다른 방법이 (내부적으로 사용 되는 `toggle()` 메서드):는 `get_Collapsed()` 의 메서드는 `CollapsiblePanelExtender()` 패널 축소 되는지 여부를 보여 줍니다. 이 함수의 반환 값에 따라 패널은 하나 확장 한 다음 (`_doOpen()` 메서드) 또는 축소 된 (`_doClose()`) 방법:

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample8.js)]


[![패널의 상태를 변경 하는 세 번째 단추:에서 축소 하 여 코드 확장 되 고 뒤로](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image1.png)

패널의 상태를 변경 하는 세 번째 단추:에서 축소 하 여 코드 확장 되어 백 ([전체 크기 이미지를 보려면 클릭](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image3.png))

> [!div class="step-by-step"]
> [다음](collapsing-and-expanding-a-panel-from-javascript-vb.md)
