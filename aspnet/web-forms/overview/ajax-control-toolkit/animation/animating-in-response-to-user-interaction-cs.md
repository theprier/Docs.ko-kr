---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
title: 사용자 상호 작용 (C#)에 대 한 응답으로 애니메이션 효과 주는 | Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 애니메이션 별 있습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: ea26549d-fbbf-4973-a108-b14cd1d6de26
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-cs
msc.type: authoredcontent
ms.openlocfilehash: 9dea9daf3df76558eb19a524475cedd8e2085297
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37379821"
---
<a name="animating-in-response-to-user-interaction-c"></a>사용자 상호 작용 (C#)에 대 한 응답으로 애니메이션 적용
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6CS.pdf)

> ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 애니메이션은 자동으로 시작 하거나 트리거될 수 있습니다 사용자 상호 작용 하 여 예를 들어 마우스로 클릭 하 여.


## <a name="overview"></a>개요

ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 애니메이션은 자동으로 시작 하거나 트리거될 수 있습니다 사용자 상호 작용 하 여 예를 들어 마우스로 클릭 하 여.

## <a name="steps"></a>단계

첫째, 포함 된 `ScriptManager` 페이지 그런 다음 ASP.NET AJAX 라이브러리 로드 되 면 컨트롤 도구 키트를 사용 하 여:

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample1.aspx)]

그러면 다음과 같은 텍스트 패널에 애니메이션 적용 됩니다.

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample2.aspx)]

패널에 대 한 연결 된 CSS 클래스에 유용한 배경 색을 정의 하 고 패널 고정된 너비를 설정할 수도:

[!code-css[Main](animating-in-response-to-user-interaction-cs/samples/sample3.css)]

그런 다음 추가 `AnimationExtender` 페이지에서 제공 하는 `ID`, `TargetControlID` 특성과 필수 항목 이지만 `runat="server"`:

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample4.aspx)]

내 합니다 `<Animations>` 노드를 사용자 상호 작용을 통해 애니메이션을 시작 하는 방법은 5 가지가 있습니다 (누락 된 요소는 `<OnLoad>` 전체 페이지가 완전히 로드 되 면 실행 되는):

- `<OnClick>` (컨트롤의 마우스 클릭)
- `<OnHoverOut>` (마우스가 컨트롤)
- `<OnHoverOver>` (중지 컨트롤을 마우스로 `<OnHoverOut>` 애니메이션)
- `<OnMouseOut>` (마우스가 컨트롤)
- `<OnMouseOver>` (중지 컨트롤을 마우스로 `<OnMouseOut>` 애니메이션)

이 시나리오에서는 `<OnClick>` 사용 됩니다. 패널에서 사용자가 크기를 조정 하 고 동시에 페이드 아웃 합니다.

[!code-aspx[Main](animating-in-response-to-user-interaction-cs/samples/sample5.aspx)]


[![애니메이션을 시작 하는 마우스 클릭](animating-in-response-to-user-interaction-cs/_static/image2.png)](animating-in-response-to-user-interaction-cs/_static/image1.png)

마우스 클릭 애니메이션을 시작 ([클릭 하 여 큰 이미지 보기](animating-in-response-to-user-interaction-cs/_static/image3.png))

> [!div class="step-by-step"]
> [이전](picking-one-animation-out-of-a-list-cs.md)
> [다음](disabling-actions-during-animation-cs.md)
