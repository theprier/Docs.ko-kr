---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-vb
title: (VB) DropShadow의 Z-인덱스 조정 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit에서 DropShadow 컨트롤 그림자를 사용 하 여 패널을 확장합니다. 그러나이 섀도 경우에 따라 설치에 대 한 다른 컨트롤을 사용 하 여 충돌 하는 중...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ecb004b5-82c0-44fb-bcaf-233fffac6195
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-vb
msc.type: authoredcontent
ms.openlocfilehash: a900a074e1507965e7d60e8de4202de57dc6180e
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829690"
---
<a name="adjusting-the-z-index-of-a-dropshadow-vb"></a>(VB) DropShadow의 Z-인덱스 조정
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1VB.pdf)

> AJAX Control Toolkit에서 DropShadow 컨트롤 그림자를 사용 하 여 패널을 확장합니다. 그러나이 섀도 ASP.NET Menu 컨트롤 예를 들어 다른 컨트롤과 경우에 따라 충돌 합니다. 때 메뉴 항목 팝업 뒤에 그림자 표시 됩니다.


## <a name="overview"></a>개요

AJAX Control Toolkit에서 DropShadow 컨트롤 그림자를 사용 하 여 패널을 확장합니다. 그러나이 섀도 ASP.NET Menu 컨트롤 예를 들어 다른 컨트롤과 경우에 따라 충돌 합니다. 때 메뉴 항목 팝업 뒤에 그림자 표시 됩니다.

## <a name="steps"></a>단계

코드 표시 되도록 효과 대 한 충분 한 텍스트를 포함 하는 패널 수 있도록 충분 한 텍스트가 포함 된 패널 자체를 사용 하 여 시작 합니다.

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample1.aspx)]

다른 패널 바로 앞에 삽입 된 `panelShadow` 패널입니다. 메뉴 항목 위에 나타나도록 가로 방향으로 메뉴가 포함 (또는 대신: 아래)를 `dropShadow` 패널):

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample2.aspx)]

그런 다음, `DropShadowExtender` 확장에 추가 되는 `panelShadow` 그림자 효과 사용 하 여 패널:

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample3.aspx)]

마지막으로 ASP.NET AJAX `ScriptManager` 제어 하려면 컨트롤 도구 키트를 사용 하면:

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample4.aspx)]

이 스크립트를 실행 하면 메뉴 항목 패널 아래에 나타납니다. 하지만 메뉴는 CSS 클래스를 사용 `panel` 만 있는 두 가지 다른 패널 앞에 표시 되는 요소를 정의 하려면:

- 상대 위치
- 양의 z-인덱스

[!code-css[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample5.css)]

그런 다음, `DropShadowExtender` 컨트롤 메뉴 컨트롤을 사용 하 여 더 이상 충돌 하지 않습니다.


[![이전: 메뉴 항목은 표시](adjusting-the-z-index-of-a-dropshadow-vb/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image1.png)

이전: 메뉴 항목 표시 되지 않습니다 ([클릭 하 여 큰 이미지 보기](adjusting-the-z-index-of-a-dropshadow-vb/_static/image3.png))


[![메뉴 항목을 표시 하는 이후:](adjusting-the-z-index-of-a-dropshadow-vb/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image4.png)

이후: 메뉴 항목 표시 ([클릭 하 여 큰 이미지 보기](adjusting-the-z-index-of-a-dropshadow-vb/_static/image6.png))

> [!div class="step-by-step"]
> [이전](manipulating-dropshadow-properties-from-client-code-cs.md)
> [다음](manipulating-dropshadow-properties-from-client-code-vb.md)
