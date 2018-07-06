---
uid: web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
title: 조건 (C#)에 따라 애니메이션 | Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 애니메이션 인지 하는 중...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: b7a28c0d-efb9-443a-80a4-1a5ee54671cd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
msc.type: authoredcontent
ms.openlocfilehash: cb08c330d6fbc86035a2f21ad382cc009411bcd6
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37808426"
---
<a name="animation-depending-on-a-condition-c"></a>조건 (C#)에 따라 애니메이션
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4CS.pdf)

> ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 여부 애니메이션 실행 되는 여부 일부 JavaScript 코드의 형태로 조건에도 달라질 수 있습니다.


## <a name="overview"></a>개요

ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 여부 애니메이션 실행 되는 여부 일부 JavaScript 코드의 형태로 조건에도 달라질 수 있습니다.

## <a name="steps"></a>단계

첫째, 포함 된 `ScriptManager` 페이지 그런 다음 ASP.NET AJAX 라이브러리 로드 되 면 컨트롤 도구 키트를 사용 하 여:

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample1.aspx)]

그러면 다음과 같은 텍스트 패널에 애니메이션 적용 됩니다.

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample2.aspx)]

패널에 대 한 연결 된 CSS 클래스에 유용한 배경 색을 정의 하 고 패널 고정된 너비를 설정할 수도:

[!code-css[Main](animation-depending-on-a-condition-cs/samples/sample3.css)]

그런 다음 추가 `AnimationExtender` 페이지에서 제공 하는 `ID`, `TargetControlID` 특성과 필수 항목 이지만 `runat="server":`

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample4.aspx)]

내 합니다 `<Animations>` 노드를 사용 하 여 `<OnLoad>` 페이지가 완전히 로드 되 면 애니메이션을 실행 합니다. 대신 일반 애니메이션 중 하나는 `<Condition>` 요소 고려해 야 합니다. 값으로 제공 하는 JavaScript 코드는 `ConditionScript` 특성은 런타임 시 실행 됩니다. True로 평가 될 경우 애니메이션 실행 되어이 고, 그렇지 없습니다. 다음 태그는 임의 시 사례의 50%에서 실행 되 고 각 두 애니메이션을 제공 합니다. 내에서 애니메이션 하나 수만 있으므로 `<OnLoad>`, 두 개의 `<Condition>` 애니메이션 사용 하 여 함께 조인 되는 `<Sequence>` 요소:

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample5.aspx)]

보다 작음 부호 (`<`)에 `ConditionScript` 이스케이프 ()을 설정 해야 합니다. 경우 하거나 애니메이션 실행이 없습니다,이 스크립트를 실행 하면 아니라 둘 중 하나 또는 둘 다 수행 합니다.


[![패널은 페이드아웃 크기 조정 없이 첫 번째 두 번째 애니메이션 실행 하지 않은 하므로](animation-depending-on-a-condition-cs/_static/image2.png)](animation-depending-on-a-condition-cs/_static/image1.png)

패널은 페이드아웃 크기 조정 없이 첫 번째 두 번째 애니메이션 실행 하지 않은 하도록 ([클릭 하 여 큰 이미지 보기](animation-depending-on-a-condition-cs/_static/image3.png))

> [!div class="step-by-step"]
> [이전](executing-several-animations-after-each-other-cs.md)
> [다음](picking-one-animation-out-of-a-list-cs.md)
