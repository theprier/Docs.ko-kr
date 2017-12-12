---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-cs
title: "클라이언트 코드 (C#)에서 DropShadow 속성 조작 | Microsoft Docs"
author: wenz
description: "DataList의 편집 인터페이스 사용자 지정"
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: c83ca3e6-c0bf-4158-a166-40c1ab0f33da
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 59f7d4610ce610ef4357510f0e861f107278b5da
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="manipulating-dropshadow-properties-from-client-code-c"></a>클라이언트 코드 (C#)에서 DropShadow 속성 조작
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2CS.pdf)

> 들어의 DropShadow 컨트롤 그림자가 있는 패널을 확장합니다. 클라이언트 JavaScript 코드를 사용 하 여이 extender의 속성을 변경할 수도 있습니다.


## <a name="overview"></a>개요

들어의 DropShadow 컨트롤 그림자가 있는 패널을 확장합니다. 클라이언트 JavaScript 코드를 사용 하 여이 extender의 속성을 변경할 수도 있습니다.

## <a name="steps"></a>단계

코드 몇 줄의 텍스트가 포함 된 패널으로 시작 됩니다.

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample1.aspx)]

연결 된 CSS 클래스 좋은 배경색 패널을 제공합니다.

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample2.css)]

`DropShadowExtender` 그림자 효과 불투명도 50%로 설정 된 패널을 확장에 추가 됩니다.

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample3.aspx)]

그런 다음 ASP.NET AJAX `ScriptManager` 컨트롤을 사용 하면 제어 도구 키트에서 실행 되도록 합니다.

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample4.aspx)]

그림자의 불투명도 설정 하기 위한 두 개의 JavaScript 링크를 포함 하는 다른 패널: 빼기 링크 그림자의 불투명도 감소, 더하기 링크 늘립니다.

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample5.aspx)]

JavaScript 함수 `changeOpacity()` 다음 먼저 찾아야는 `DropShadowExtender` 페이지에 있는 컨트롤입니다. ASP.NET AJAX 정의 `$find()` 정확 하 게 해당 작업에 대 한 메서드. 그런 다음 `get_Opacity()` 메서드 검색 현재 불투명도 `set_Opacity()` 설정 하는 메서드. 다음 JavaScript 코드에 현재 불투명 값을 놓입니다는 `<label>` 요소:

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample6.html)]


[![클라이언트 쪽에서 변경 되는 불투명도](manipulating-dropshadow-properties-from-client-code-cs/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-cs/_static/image1.png)

클라이언트 쪽에서 변경 되는 불투명도 ([전체 크기 이미지를 보려면 클릭](manipulating-dropshadow-properties-from-client-code-cs/_static/image3.png))

>[!div class="step-by-step"]
[이전](adjusting-the-z-index-of-a-dropshadow-cs.md)
[다음](adjusting-the-z-index-of-a-dropshadow-vb.md)
