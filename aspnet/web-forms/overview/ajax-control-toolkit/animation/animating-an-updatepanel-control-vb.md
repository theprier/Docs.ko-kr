---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
title: UpdatePanel 컨트롤 (VB) 애니메이션 | Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 내용에 대 한 프로그램...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 4c306a2c-92b6-4904-b70b-365b847334fe
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 5f14a3297c2f3ddd6b0817cc8e46ac23b3a06c0b
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37369718"
---
<a name="animating-an-updatepanel-control-vb"></a>UpdatePanel 컨트롤 (VB) 애니메이션
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1VB.pdf)

> ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. UpdatePanel의 내용에 대 한 특별 한 extender를 애니메이션 프레임 워크에 크게 의존 하는 존재: UpdatePanelAnimation 합니다. 이 자습서는 UpdatePanel에 대 한 이러한 애니메이션을 설정 하는 방법을 보여 줍니다.


## <a name="overview"></a>개요

ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 내용에 대 한는 `UpdatePanel`, 애니메이션 프레임 워크에 크게 의존 하는 특별 한 extender 존재: `UpdatePanelAnimation`합니다. 이 자습서에 대 한 이러한 애니메이션을 설정 하는 방법을 보여 줍니다는 `UpdatePanel`합니다.

## <a name="steps"></a>단계

첫 번째 단계는 일반적으로 포함 합니다 `ScriptManager` 페이지에서 ASP.NET AJAX library가 로드 하 고 컨트롤 도구 키트를 사용할 수 있도록 합니다.

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample1.aspx)]

ASP.NET에이 시나리오에서는 애니메이션을 적용할 `Wizard` 에 있는 웹 컨트롤을 `UpdatePanel`입니다. 세 가지 (임의) 단계는 포스트백을 트리거하려면 충분 한 옵션을 제공 합니다.

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample2.aspx)]

에 필요한 태그를 `UpdatePanelAnimationExtender` 컨트롤에 사용 되는 태그에 상당히 비슷합니다는 `AnimationExtender`합니다. `TargetControlID` 제공 하는 특성을 `ID` 의 `UpdatePanel` ;에 애니메이션 효과를 내는 `UpdatePanelAnimationExtender` 컨트롤을 `<Animations>` 요소 있는 애니메이션의 XML 태그를 포함 합니다. 그러나 한 가지 차이가: 이벤트 및 이벤트 처리기의 용량은 제한 비교 `AnimationExtender`합니다. 에 대 한 `UpdatePanels`, 두 개의 정도의 존재 합니다.

- `<OnUpdated>` UpdatePanel 업데이트 된 경우
- `<OnUpdating>` UpdatePanel 업데이트를 시작할 때

이 시나리오에서는 새 내용의 `UpdatePanel` 포스트백) (이후에 페이드 인 됩니다. 필요한 태그는 다음과 같습니다.

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample3.aspx)]

이제 UpdatePanel 내 포스트백이 발생할 때마다 패널의 새 내용이 페이드 원활 하 게 합니다.


[![다음 마법사 단계 옅은 색은](animating-an-updatepanel-control-vb/_static/image2.png)](animating-an-updatepanel-control-vb/_static/image1.png)

다음 마법사 단계 옅은 색은 ([클릭 하 여 큰 이미지 보기](animating-an-updatepanel-control-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](changing-an-animation-using-client-side-code-vb.md)
> [다음](dynamically-controlling-updatepanel-animations-vb.md)
