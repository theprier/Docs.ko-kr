---
uid: web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
title: 다른 컨트롤 (VB)에서 애니메이션 트리거 | Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 일반적으로 시작을...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 25ebaf1f-5a9f-423d-98c7-1d694e93664f
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
msc.type: authoredcontent
ms.openlocfilehash: b316b22bf355d7abb0909e43f0c2c38ea3e68f24
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37367812"
---
<a name="triggering-an-animation-in-another-control-vb"></a>다른 컨트롤 (VB)에서 애니메이션 트리거
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8VB.pdf)

> ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 일반적으로 동일한 컨트롤을 사용 하 여 사용자 상호 작용에 의해 트리거됩니다는 애니메이션을 시작. 하지만 이기도 다른 컨트롤이 컨트롤 및 애니메이션을 사용 하 여 상호 작용할 수 있습니다.


## <a name="overview"></a>개요

ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 일반적으로 동일한 컨트롤을 사용 하 여 사용자 상호 작용에 의해 트리거됩니다는 애니메이션을 시작. 하지만 이기도 다른 컨트롤이 컨트롤 및 애니메이션을 사용 하 여 상호 작용할 수 있습니다.

## <a name="steps"></a>단계

첫째, 포함 된 `ScriptManager` 페이지 그런 다음 ASP.NET AJAX 라이브러리 로드 되 면 컨트롤 도구 키트를 사용 하 여:

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample1.aspx)]

그러면 다음과 같은 텍스트 패널에 애니메이션 적용 됩니다.

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample2.aspx)]

패널에 대 한 연결 된 CSS 클래스에 유용한 배경 색을 정의 하 고 패널 고정된 너비를 설정할 수도:

[!code-css[Main](triggering-an-animation-in-another-control-vb/samples/sample3.css)]

패널에 애니메이션 적용을 시작 하기 위해 HTML 단추가 사용 됩니다. 사실은 `<input type="button" />` 들이 통해 좋아하는 `<asp:Button />` 사용자가 해당 단추를 클릭 하면 포스트백 않을 것 이므로 합니다.

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample4.aspx)]

그런 다음 추가 `AnimationExtender` 페이지에서 제공 하는 `ID`, `TargetControlID` 특성과 필수 항목 이지만 `runat="server"`. 설정 하는 것이 반드시 `TargetControlID` 단추 (애니메이션 트리거 요소)의 ID로 패널 (애니메이션 효과가 적용 되는 요소)의 ID에 없습니다

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample5.aspx)]

내는 `<Animations>` 노드를 일반적인 방법으로 위치 애니메이션 합니다. 단추가 아닌는 패널을 변경할 수 있도록, 하려면 설정 합니다 `AnimationTarget` 내에서 모든 애니메이션 요소에 대 한 특성 `AnimationExtender`합니다. 에 대 한 값 `AnimationTarget` 물론은 패널의 ID입니다. 이런 방식으로 애니메이션 트리거 단추와 패널을 사용 하 여 발생합니다. 다음은 `AnimationExtender` 이 시나리오에 대 한 태그:

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample6.aspx)]

특별 한 순서는 개별 애니메이션 note 합니다. 첫째, 단추 애니메이션 실행 되 면 비활성화를 가져옵니다. 있기 때문 없습니다 `AnimationTarget` 특성을 `<EnableAction>` 원래 컨트롤 요소를이 애니메이션을 적용할: 단추입니다. Parallelly 애니메이션 다음 두 단계를 수행 됩니다 (`<Parallel>` 요소). 둘 다 해당 `AnimationTarget` 특성으로 설정 `"Panel1"`, 따라서 패널에 단추가 아닌 애니메이션을 적용 합니다.


[![창 애니메이션을 시작 하는 단추 마우스 클릭](triggering-an-animation-in-another-control-vb/_static/image2.png)](triggering-an-animation-in-another-control-vb/_static/image1.png)

창 애니메이션을 시작 하는 단추 마우스 클릭 ([클릭 하 여 큰 이미지 보기](triggering-an-animation-in-another-control-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](disabling-actions-during-animation-vb.md)
> [다음](modifying-animations-from-the-server-side-vb.md)
