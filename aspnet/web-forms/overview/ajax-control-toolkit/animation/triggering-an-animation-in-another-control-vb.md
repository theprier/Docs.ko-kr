---
uid: web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
title: 다른 컨트롤 (VB) 애니메이션 트리거 | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 일반적으로 시작는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 25ebaf1f-5a9f-423d-98c7-1d694e93664f
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 262a17e7521a8ea16c81e8dfdc6d3b6614c18eea
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30878999"
---
<a name="triggering-an-animation-in-another-control-vb"></a>다른 컨트롤 (VB) 애니메이션 트리거
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8VB.pdf)

> ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 일반적으로 애니메이션 시작에 의해 트리거될 동일한 컨트롤과 상호 작용 합니다. 그러나 또한 다른 컨트롤을 한 개의 컨트롤 및 애니메이션와 상호 작용할 수 있습니다.


## <a name="overview"></a>개요

ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 일반적으로 애니메이션 시작에 의해 트리거될 동일한 컨트롤과 상호 작용 합니다. 그러나 또한 다른 컨트롤을 한 개의 컨트롤 및 애니메이션와 상호 작용할 수 있습니다.

## <a name="steps"></a>단계

우선, 포함 된 `ScriptManager` 페이지; 그런 다음 ASP.NET AJAX 라이브러리 로드 되는 제어 도구 키트를 사용 하 여:

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample1.aspx)]

그러면 다음과 같은 텍스트의 패널에 애니메이션 적용 됩니다.

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample2.aspx)]

패널에 대 한 연결 된 CSS 클래스 좋은 배경색을 정의 하 고도 패널 고정된 폭을 설정 합니다.

[!code-css[Main](triggering-an-animation-in-another-control-vb/samples/sample3.css)]

패널에 애니메이션 적용을 시작 하기 위해 HTML 단추가 사용 됩니다. `<input type="button" />` 들이 통해 좋아하는 `<asp:Button />` 사용자가 해당 단추를 클릭할 때 포스트백을 원치 않으므로 때문입니다.

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample4.aspx)]

그런 다음 추가 `AnimationExtender` 페이지에 제공 하는 `ID`, `TargetControlID` 특성과 반드시 `runat="server"`합니다. 설정 해야 `TargetControlID` 단추 (애니메이션 트리거 요소)의 ID로 패널 (애니메이션 효과가 적용 되는 요소)의 ID로 하지

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample5.aspx)]

내에서 `<Animations>` 노드를 일반적인 방법 대로 위치 애니메이션 합니다. 패널을 변경할 수를 단추가 아닌 설정의 `AnimationTarget` 특성 내에서 모든 애니메이션 요소에 대해 `AnimationExtender`합니다. 에 대 한 값 `AnimationTarget` 패널의 ID는 물론 합니다. 이런 방식으로 애니메이션 트리거 단추와 패널에서 발생 합니다. 다음은 `AnimationExtender` 이 시나리오에 대 한 태그:

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample6.aspx)]

Note 개별 애니메이션이 표시 되는 특별 한 순서입니다. 우선, 애니메이션 실행 되 면 단추 비활성화를 가져옵니다. 없기 때문 없는 `AnimationTarget` 특성에 `<EnableAction>` 요소가이 애니메이션 원본 컨트롤에 적용 되: 단추입니다. 애니메이션을 다음 두 단계는 수행 parallelly (`<Parallel>` 요소). 둘 다의 `AnimationTarget` 특성으로 설정 `"Panel1"`, 따라서 단추가 아니라 패널에 애니메이션을 적용 합니다.


[![패널 애니메이션을 시작 하는 마우스 단추 클릭](triggering-an-animation-in-another-control-vb/_static/image2.png)](triggering-an-animation-in-another-control-vb/_static/image1.png)

패널 애니메이션을 시작 하는 마우스 단추 클릭 ([전체 크기 이미지를 보려면 클릭](triggering-an-animation-in-another-control-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](disabling-actions-during-animation-vb.md)
> [다음](modifying-animations-from-the-server-side-vb.md)
