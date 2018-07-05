---
uid: web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-cs
title: UpdatePanel 애니메이션 (C#)을 동적으로 제어 | Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 내용에 대 한 프로그램...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 5138b8fe-98ff-4e73-a00b-e263fc3ff11d
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-cs
msc.type: authoredcontent
ms.openlocfilehash: f7b363a23c05490522705648fabfe0e7d0856b55
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37400683"
---
<a name="dynamically-controlling-updatepanel-animations-c"></a>UpdatePanel 애니메이션을 동적으로 제어 (C#)
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2CS.pdf)

> ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. UpdatePanel의 내용에 대 한 특별 한 extender를 애니메이션 프레임 워크에 크게 의존 하는 존재: UpdatePanelAnimation 합니다. UpdatePanel 트리거와 함께 사용할 수 있습니다.


## <a name="overview"></a>개요

ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 내용에 대 한는 `UpdatePanel`, 애니메이션 프레임 워크에 크게 의존 하는 특별 한 extender 존재: `UpdatePanelAnimation`합니다. 함께 사용할 수도 있습니다 `UpdatePanel` 트리거.

## <a name="steps"></a>단계

첫 번째 단계는 일반적으로 포함 합니다 `ScriptManager` 페이지에서 ASP.NET AJAX library가 로드 하 고 컨트롤 도구 키트를 사용할 수 있도록 합니다.


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample1.aspx)]

이 시나리오에서는 애니메이션의 현재 디스플레이에 적용 됩니다. 이 정보를 사용 하 여 레이블에 쓸 수는 `Page_Load()` 메서드 또는 다음 인라인 코드를 사용 (간단히):


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample2.aspx)]

또한에 업데이트를 트리거하는 단추를 만듭니다.


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample3.aspx)]

이 코드는 다음을 배치 합니다 `<ContentTemplate>` 부분을 `UpdatePanel` 요소입니다. 패널의 `UpdateMode` 특성으로 설정 되어 있어야 `"Conditional"`가 트리거만 패널의 콘텐츠를 업데이트할 수 있습니다. 에 `<Triggers>` 의 섹션을 `UpdatePanel`, 비동기 포스트백 트리거를 만들고 연결를 `Click` 단추의 이벤트입니다. 따라서 사용자가 단추를 클릭할 경우의 `UpdatePanel` 새로 고쳐집니다. 여기에 대 한 태그는 `UpdatePanel` 제어 합니다.


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample4.aspx)]

마지막으로 `UpdatePanelAnimationExtender` 구성 해야 합니다: 설정의 `TargetControlID` 패널의 id 특성 및 extender에서 애니메이션을 정의 합니다. 페이딩 만드는 업데이트 된 시간에 유용한 시각적 강조를 의미 합니다. Extender 태그는 다음과 같은 다음 같을 수 있습니다.


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample5.aspx)]

브라우저에서 파일을 실행 합니다. 단추를 클릭할 때마다 현재 항상 1 초 동안 페이드 인 패널에 표시 됩니다.


[![현재는 페이드 인](dynamically-controlling-updatepanel-animations-cs/_static/image2.png)](dynamically-controlling-updatepanel-animations-cs/_static/image1.png)

현재 시간 페이딩 됩니다 ([클릭 하 여 큰 이미지 보기](dynamically-controlling-updatepanel-animations-cs/_static/image3.png))

> [!div class="step-by-step"]
> [이전](animating-an-updatepanel-control-cs.md)
> [다음](adding-animation-to-a-control-vb.md)
