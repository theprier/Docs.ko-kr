---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
title: 사용자 상호 작용 (VB)에 대 한 응답에서 애니메이션이 | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 애니메이션 별 있습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: c8204c05-ec27-40fe-933d-88e4e727a482
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
msc.type: authoredcontent
ms.openlocfilehash: e12467bfeb88c2ab9d1cfb866506e9e8e7f9ae25
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30869441"
---
<a name="animating-in-response-to-user-interaction-vb"></a>사용자 상호 작용 (VB)에 대 한 응답으로 애니메이션 적용
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6VB.pdf)

> ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 애니메이션 자동으로 시작할 수 있습니다이 트리거될 수도 있고 사용자 인터페이스에 의해 예: 마우스로 클릭 하 여 합니다.


## <a name="overview"></a>개요

ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 애니메이션 자동으로 시작할 수 있습니다이 트리거될 수도 있고 사용자 인터페이스에 의해 예: 마우스로 클릭 하 여 합니다.

## <a name="steps"></a>단계

우선, 포함 된 `ScriptManager` 페이지; 그런 다음 ASP.NET AJAX 라이브러리 로드 되는 제어 도구 키트를 사용 하 여:

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample1.aspx)]

그러면 다음과 같은 텍스트의 패널에 애니메이션 적용 됩니다.

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample2.aspx)]

패널에 대 한 연결 된 CSS 클래스 좋은 배경색을 정의 하 고도 패널 고정된 폭을 설정 합니다.

[!code-css[Main](animating-in-response-to-user-interaction-vb/samples/sample3.css)]

그런 다음 추가 `AnimationExtender` 페이지에 제공 하는 `ID`, `TargetControlID` 특성과 반드시 `runat="server"`:

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample4.aspx)]

내에서 `<Animations>` 노드를 5 가지 방법으로 사용자 상호 작용을 통해 애니메이션을 시작 하려면 (누락 된 요소는 `<OnLoad>` 전체 페이지가 완전히 로드 되 면 실행 되는):

- `<OnClick>` (컨트롤에서 마우스 클릭)
- `<OnHoverOut>` (마우스 컨트롤을 리프)
- `<OnHoverOver>` (중지 하는 컨트롤을 마우스로 `<OnHoverOut>` 애니메이션)
- `<OnMouseOut>` (마우스가 컨트롤)
- `<OnMouseOver>` (중지 되지 컨트롤을 마우스로 `<OnMouseOut>` 애니메이션)

이 시나리오에서는 `<OnClick>` 사용 됩니다. 패널에 사용자가 크기를 조정 하 고 동시에 페이드 아웃 합니다.

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample5.aspx)]


[![마우스 클릭 컨트롤은 애니메이션 시작](animating-in-response-to-user-interaction-vb/_static/image2.png)](animating-in-response-to-user-interaction-vb/_static/image1.png)

마우스 클릭 컨트롤은 애니메이션 시작 ([전체 크기 이미지를 보려면 클릭](animating-in-response-to-user-interaction-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](picking-one-animation-out-of-a-list-vb.md)
> [다음](disabling-actions-during-animation-vb.md)
