---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
title: "DropShadow (C#)의 Z 인덱스를 조정 | Microsoft Docs"
author: wenz
description: "들어의 DropShadow 컨트롤 그림자가 있는 패널을 확장합니다. 그러나이 그림자 insta에 대 한 다른 컨트롤과 경우에 따라 충돌 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 14133833-e518-4347-87b9-6b6f71f14a77
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
msc.type: authoredcontent
ms.openlocfilehash: 161f02daa5dd1f0e21853c1b7c1a65c1a9aa5d03
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="adjusting-the-z-index-of-a-dropshadow-c"></a>DropShadow (C#)의 Z 인덱스를 조정합니다.
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1CS.pdf)

> 들어의 DropShadow 컨트롤 그림자가 있는 패널을 확장합니다. 그러나이 그림자 예를 들어 ASP.NET 메뉴 컨트롤이 다른 컨트롤과 경우에 따라 충돌 합니다. 때 메뉴 항목을 팝업, 드롭 그림자 뒤에 표시 됩니다.


## <a name="overview"></a>개요

들어의 DropShadow 컨트롤 그림자가 있는 패널을 확장합니다. 그러나이 그림자 예를 들어 ASP.NET 메뉴 컨트롤이 다른 컨트롤과 경우에 따라 충돌 합니다. 때 메뉴 항목을 팝업, 드롭 그림자 뒤에 표시 됩니다.

## <a name="steps"></a>단계

패널에 표시 되도록 효과 대 한 충분 한 텍스트에 포함 하도록 충분 한 텍스트가 포함 된 패널 자체를 코드 시작 됩니다.

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample1.aspx)]

다른 패널 바로 앞에 삽입 된 `panelShadow` 패널입니다. 메뉴 항목을 통해 표시 되도록 가로 방향으로 메뉴를 포함 (나 비슷한: 아래)는 `dropShadow` 패널):

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample2.aspx)]

그런 다음 `DropShadowExtender` 확장에 추가 되는 `panelShadow` 그림자 효과와 패널:

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample3.aspx)]

마지막으로, ASP.NET AJAX `ScriptManager` 컨트롤을 사용 하면 제어 도구 키트에서 실행 되도록 합니다.

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample4.aspx)]

이 스크립트를 실행할 때 메뉴 항목 패널 아래에 나타납니다. 그러나 메뉴는 CSS 클래스를 사용 하는 `panel` 만 있는 요소를 다른 패널 앞에 표시 하려면 다음 두 가지를 정의 하려면:

- 상대 위치 지정
- 양수 z-인덱스

[!code-css[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample5.css)]

그런 다음 `DropShadowExtender` 컨트롤 메뉴 컨트롤에 더 이상 충돌 하지 않습니다.


[![이전: 메뉴 항목은 표시](adjusting-the-z-index-of-a-dropshadow-cs/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image1.png)

이전: 메뉴 항목 보이지 않으면 ([전체 크기 이미지를 보려면 클릭](adjusting-the-z-index-of-a-dropshadow-cs/_static/image3.png))


[![이후: 메뉴 항목 표시](adjusting-the-z-index-of-a-dropshadow-cs/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image4.png)

이후: 메뉴 항목 표시 ([전체 크기 이미지를 보려면 클릭](adjusting-the-z-index-of-a-dropshadow-cs/_static/image6.png))

>[!div class="step-by-step"]
[다음](manipulating-dropshadow-properties-from-client-code-cs.md)
