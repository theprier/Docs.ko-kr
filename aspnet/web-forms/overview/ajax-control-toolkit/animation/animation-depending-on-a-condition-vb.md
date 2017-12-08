---
uid: web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-vb
title: "애니메이션 (VB) 조건에 따라 | Microsoft Docs"
author: wenz
description: "ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 애니메이션 인지 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 1b87d8d6-b3f7-4126-b51c-d41442fbf947
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-vb
msc.type: authoredcontent
ms.openlocfilehash: cc8600f33f9c27e1045f5083a126b9d2d1e90303
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="animation-depending-on-a-condition-vb"></a>(VB) 조건에 따라 애니메이션
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4VB.pdf)

> ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 애니메이션이 실행 여부 형태의 일부 JavaScript 코드에서 조건에도 달라질 수 있습니다.


## <a name="overview"></a>개요

ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 애니메이션이 실행 여부 형태의 일부 JavaScript 코드에서 조건에도 달라질 수 있습니다.

## <a name="steps"></a>단계

우선, 포함 된 `ScriptManager` 페이지; 그런 다음 ASP.NET AJAX 라이브러리 로드 되는 제어 도구 키트를 사용 하 여:

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample1.aspx)]

그러면 다음과 같은 텍스트의 패널에 애니메이션 적용 됩니다.

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample2.aspx)]

패널에 대 한 연결 된 CSS 클래스 좋은 배경색을 정의 하 고도 패널 고정된 폭을 설정 합니다.

[!code-css[Main](animation-depending-on-a-condition-vb/samples/sample3.css)]

그런 다음 추가 `AnimationExtender` 페이지에 제공 하는 `ID`, `TargetControlID` 특성과 참가`runat="server":`

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample4.aspx)]

내에서 `<Animations>` 노드를 사용 하 여 `<OnLoad>` 페이지가 완전히 로드 되 면 애니메이션을 실행 합니다. 대신 일반 애니메이션 중 하나는 `<Condition>` 요소에 발생 합니다. 값으로 제공 하는 JavaScript 코드는 `ConditionScript` 특성은 런타임 시 실행 됩니다. True로 평가 될 경우 애니메이션 실행 되어 그렇지 않으면 없습니다. 다음 태그는 각각의 임의 시 사례의 50%에서 실행 되는 두 개의 애니메이션이 제공 합니다. 내에서 하나의 애니메이션 수만 있으므로 `<OnLoad>`, 두 `<Condition>` 애니메이션을 사용 하 여 함께 조인에서 `<Sequence>` 요소:

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample5.aspx)]

보다 작음 부호 (`<`)에 `ConditionScript` 특성 (이스케이프) 이어야 합니다. 때 하거나 애니메이션 실행이 없습니다,이 스크립트를 실행 하거나 수행 하는 두 가지 중 하나 하거나 모두 않습니다.


[![패널은 페이딩 크기를 조정 하지 않고 첫 번째는 두 번째 애니메이션 실행 하지 않은 하므로](animation-depending-on-a-condition-vb/_static/image2.png)](animation-depending-on-a-condition-vb/_static/image1.png)

패널은 페이딩 크기를 조정 하지 않고 첫 번째는 두 번째 애니메이션 실행 하지 않은 하므로 ([전체 크기 이미지를 보려면 클릭](animation-depending-on-a-condition-vb/_static/image3.png))

>[!div class="step-by-step"]
[이전](executing-several-animations-after-each-other-vb.md)
[다음](picking-one-animation-out-of-a-list-vb.md)
