---
uid: web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-vb
title: UpdatePanel 애니메이션 (VB)을 동적으로 제어 | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 내용에는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: bea66072-59b6-42b4-98fa-211812f5925f
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-vb
msc.type: authoredcontent
ms.openlocfilehash: ff2853b4457a83a7367b4d1072d21929c40a3ed2
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30871547"
---
<a name="dynamically-controlling-updatepanel-animations-vb"></a>UpdatePanel 애니메이션 (VB)을 동적으로 제어
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2VB.pdf)

> ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 특별 한 extender 존재 애니메이션 프레임 워크에 크게 의존 하는 UpdatePanel의 내용에 대해: UpdatePanelAnimation 합니다. UpdatePanel 트리거와 함께 사용할 수도 있습니다.


## <a name="overview"></a>개요

ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 내용에는 `UpdatePanel`, 애니메이션 프레임 워크에 크게 의존 하는 특별 한 extender 존재: `UpdatePanelAnimation`합니다. 와 함께 확대할 수 `UpdatePanel` 트리거.

## <a name="steps"></a>단계

첫 번째 단계는 일반적으로 포함는 `ScriptManager` 페이지에 있도록 ASP.NET AJAX 라이브러리를 로드 하 고 제어 도구 키트를 사용할 수 있습니다.


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample1.aspx)]

이 시나리오에서 애니메이션의 현재 시간 표시를에 적용 됩니다. 이 정보를 사용 하 여 레이블의에 쓸 수는 `Page_Load()` 메서드를 다음 인라인 코드를 사용 (편의상) 또는:


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample2.aspx)]

또한 시간을 업데이트할 트리거하는 단추를 만듭니다.


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample3.aspx)]

이 코드는 다음에 배치 된 `<ContentTemplate>` 의 섹션은 `UpdatePanel` 요소입니다. 패널의 `UpdateMode` 특성으로 설정 되어 있어야 `"Conditional"`이므로 트리거만 패널의 콘텐츠를 업데이트할 수 있습니다. 에 `<Triggers>` 의 섹션에서 `UpdatePanel`, 비동기 포스트백 트리거는 생성 되 고 변수에 연결는 `Click` 단추의 이벤트가 합니다. 따라서 사용자가 단추를 클릭할 경우의 `UpdatePanel` 새로 고쳐집니다. 다음은 대 한 태그는 `UpdatePanel` 제어:


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample4.aspx)]

마지막으로 `UpdatePanelAnimationExtender` 구성 해야 합니다: 설정의 `TargetControlID` 패널의 ID에 특성을 extender 내에서 애니메이션을 정의 합니다. 에서 페이딩 의미는 멋진 시각적에 중점을 둔 업데이트 시간을 만듭니다. Extender 태그 수 다음 다음과 같이 표시 됩니다.


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-vb/samples/sample5.aspx)]

브라우저에서 파일을 실행 합니다. 단추를 클릭할 때마다 현재 시간을 항상 1 초 동안 페이딩 패널에서 표시 됩니다.


[![현재 시간 페이딩 됩니다.](dynamically-controlling-updatepanel-animations-vb/_static/image2.png)](dynamically-controlling-updatepanel-animations-vb/_static/image1.png)

현재 시간 페이딩 됩니다 ([전체 크기 이미지를 보려면 클릭](dynamically-controlling-updatepanel-animations-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](animating-an-updatepanel-control-vb.md)
