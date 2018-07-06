---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
title: 클라이언트 코드 (VB)에서 DropShadow 속성 조작 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit에서 DropShadow 컨트롤 그림자를 사용 하 여 패널을 확장합니다. 이 extender의 속성 JavaScrip 클라이언트를 사용 하 여 변경할 수 있습니다...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: 11be4211-2fb9-4e15-b6d4-2aa623d81f3e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
msc.type: authoredcontent
ms.openlocfilehash: b9220eecca224c2b1e0f19c972c6c2a4dc9c7d35
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37841411"
---
<a name="manipulating-dropshadow-properties-from-client-code-vb"></a>클라이언트 코드 (VB)에서 DropShadow 속성 조작
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2VB.pdf)

> AJAX Control Toolkit에서 DropShadow 컨트롤 그림자를 사용 하 여 패널을 확장합니다. 이 extender의 속성 클라이언트 JavaScript 코드를 사용 하 여 변경할 수 있습니다.


## <a name="overview"></a>개요

AJAX Control Toolkit에서 DropShadow 컨트롤 그림자를 사용 하 여 패널을 확장합니다. 이 extender의 속성 클라이언트 JavaScript 코드를 사용 하 여 변경할 수 있습니다.

## <a name="steps"></a>단계

코드 몇 줄의 텍스트가 포함 된 패널을 사용 하 여 시작 합니다.

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample1.aspx)]

연결된 된 CSS 클래스는 훌륭한 배경 색을 패널을 제공합니다.

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample2.css)]

`DropShadowExtender` 그림자 효과 50%로 설정 하는 불투명도 사용 하 여 패널을 확장에 추가 됩니다.

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample3.aspx)]

그런 다음 ASP.NET AJAX `ScriptManager` 제어 하려면 컨트롤 도구 키트를 사용 하면:

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample4.aspx)]

그림자의 불투명도 설정 하는 것에 대 한 두 개의 JavaScript 링크를 포함 하는 다른 패널: 빼기 링크 그림자의 불투명도 감소, 더하기 링크를 늘립니다.

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample5.aspx)]

JavaScript 함수 `changeOpacity()` 먼저 찾아야 다음는 `DropShadowExtender` 페이지의 컨트롤입니다. ASP.NET AJAX 정의 `$find()` 정확 하 게 해당 작업에 대 한 메서드. 그런 다음, `get_Opacity()` 현재 불투명도 검색 하는 메서드를 `set_Opacity()` 메서드 설정 합니다. 다음 JavaScript 코드의 현재 불투명도 값을 배치 합니다 `<label>` 요소:

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample6.html)]


[![클라이언트 쪽에서 변경 되는 불투명도](manipulating-dropshadow-properties-from-client-code-vb/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-vb/_static/image1.png)

클라이언트 쪽에서 변경 되는 불투명도 ([클릭 하 여 큰 이미지 보기](manipulating-dropshadow-properties-from-client-code-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](adjusting-the-z-index-of-a-dropshadow-vb.md)
