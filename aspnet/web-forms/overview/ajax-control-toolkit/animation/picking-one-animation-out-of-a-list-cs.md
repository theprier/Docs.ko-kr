---
uid: web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-cs
title: 목록 (C#)에서 애니메이션 하나 선택 | Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 프레임 워크도 허용 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 06a776fe-7c73-4ca7-8e02-5260a86edc03
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-cs
msc.type: authoredcontent
ms.openlocfilehash: 4b0193f47697e072605ed8c01a37fbfa128eb0e0
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37380748"
---
<a name="picking-one-animation-out-of-a-list-c"></a>목록 (C#)에서 애니메이션 하나 선택
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5CS.pdf)

> ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 또한 프레임 워크에는 일부 JavaScript 코드의 평가 따라 애니메이션을 목록에서 애니메이션 하나 선택 하는 프로그래머가 수 있습니다.


## <a name="overview"></a>개요

ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 또한 프레임 워크에는 일부 JavaScript 코드의 평가 따라 애니메이션을 목록에서 애니메이션 하나 선택 하는 프로그래머가 수 있습니다.

## <a name="steps"></a>단계

첫째, 포함 된 `ScriptManager` 페이지 그런 다음 ASP.NET AJAX 라이브러리 로드 되 면 컨트롤 도구 키트를 사용 하 여:

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample1.aspx)]

그러면 다음과 같은 텍스트 패널에 애니메이션 적용 됩니다.

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample2.aspx)]

패널에 대 한 연결 된 CSS 클래스에 유용한 배경 색을 정의 하 고 패널 고정된 너비를 설정할 수도:

[!code-css[Main](picking-one-animation-out-of-a-list-cs/samples/sample3.css)]

그런 다음 추가 `AnimationExtender` 페이지에서 제공 하는 `ID`, `TargetControlID` 특성과 필수 항목 이지만 `runat="server":`

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample4.aspx)]

내 합니다 `<Animations>` 노드를 사용 하 여 `<OnLoad>` 페이지가 완전히 로드 되 면 애니메이션을 실행 합니다. 대신 일반 애니메이션 중 하나는 `<Case>` 요소 고려해 야 합니다. SelectScript 특성 값이 계산 됩니다. 반환 값은 숫자 여야 합니다. 내에서 하위 애니메이션 중 하나는이 수에 따라 &lt;사례&gt; 실행 됩니다. 예를 들어 SelectScript 2로 계산 되 면 컨트롤 도구 키트 내에서 세 번째 애니메이션 실행 &lt;사례&gt; (0부터 계산).

다음 태그는 세 가지 하위 애니메이션 정의: 너비를 크기 조정, 높이, 크기 조정 및 옅은 색입니다. JavaScript 코드 (`Math.floor(3 * Math.random())`) 다음 세 가지 애니메이션 중 실행 되는 0과 2 사이의 숫자를 선택 합니다.

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample5.aspx)]


[![가능한 세 가지 애니메이션 중 하나: 패널 더 광범위 한 가져옵니다.](picking-one-animation-out-of-a-list-cs/_static/image2.png)](picking-one-animation-out-of-a-list-cs/_static/image1.png)

가능한 세 가지 애니메이션 중 하나: 광범위 한 패널을 가져옵니다 ([클릭 하 여 큰 이미지 보기](picking-one-animation-out-of-a-list-cs/_static/image3.png))

> [!div class="step-by-step"]
> [이전](animation-depending-on-a-condition-cs.md)
> [다음](animating-in-response-to-user-interaction-cs.md)
