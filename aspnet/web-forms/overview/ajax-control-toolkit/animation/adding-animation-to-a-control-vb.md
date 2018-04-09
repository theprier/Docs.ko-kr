---
uid: web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-vb
title: 애니메이션 컨트롤을 추가 (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 이 자습서에서는 방법...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: c120187e-963e-4439-bb85-32771bc7f1f4
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 3da98e478c45213875b3829e51351d03571a05b8
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="adding-animation-to-a-control-vb"></a>애니메이션은 컨트롤 (VB)에 추가
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1VB.pdf)

> ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 이 자습서에는 이러한 애니메이션을 설정 하는 방법을 보여 줍니다.


## <a name="overview"></a>개요

ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 이 자습서에는 이러한 애니메이션을 설정 하는 방법을 보여 줍니다.

## <a name="steps"></a>단계

첫 번째 단계는 일반적으로 포함는 `ScriptManager` 페이지에 있도록 ASP.NET AJAX 라이브러리를 로드 하 고 제어 도구 키트를 사용할 수 있습니다.

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample1.aspx)]

이 시나리오에서 애니메이션 다음과 같이 표시 된 텍스트의 패널에 적용 됩니다.

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample2.aspx)]

패널에 대 한 연결 된 CSS 클래스에는 배경 색 및 너비를 정의합니다.

[!code-css[Main](adding-animation-to-a-control-vb/samples/sample3.css)]

위쪽, 해야는 `AnimationExtender`합니다. 입력 한 후 프로그램 `ID` 는 일반적인 및 `runat="server"`, `TargetControlID` 특성 컨트롤에 패널 경우에서 애니메이션 효과를 설정 해야:

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample4.aspx)]

하지만 Visual Studio의 IntelliSense에서 현재 완전히 지원 XML 구문을 사용 하 여 전체 애니메이션 선언적으로 적용 됩니다. 루트 노드는 `<Animations>;` 이 노드 내에서 여러 이벤트 애니메이션의 현재 위치 take(s) 시기를 결정 하는 허용 됩니다.

- `OnClick` (마우스 클릭)
- `OnHoverOut` (마우스를 벗어날 때 컨트롤)
- `OnHoverOver` (중지를 컨트롤 위에 마우스를 가져가면는 `OnHoverOut` 애니메이션)
- `OnLoad` (때의 페이지 로드 된)
- `OnMouseOut` (마우스를 벗어날 때 컨트롤)
- `OnMouseOver` (컨트롤 위에 마우스를 가져가면 중지 하지는 `OnMouseOut` 애니메이션)

프레임 워크 자체 XML 요소로 표시 하나씩 애니메이션 집합이 함께 제공 됩니다. 선택 영역 다음과 같습니다.

- `<Color>` (색을 변경합니다.)
- `<FadeIn>` (페이딩)
- `<FadeOut>` (페이드 아웃)
- `<Property>` (컨트롤의 속성을 변경합니다.)
- `<Pulse>` (pulsating)
- `<Resize>` (크기 변경)
- `<Scale>` (비례적으로 크기를 변경)

이 예제에서는 패널은 페이드 아웃 합니다. 애니메이션 1.5 초 취해 (`Duration` 특성), 초당 프레임 (애니메이션 단계) 24 표시 (`Fps` attributs). 다음은 전체 태그를는 `AnimationExtender` 제어:

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample5.aspx)]

이 스크립트를 실행 하면 패널 표시 되 고 일 분 초에서 사라집니다.


[![패널은 옅은 색](adding-animation-to-a-control-vb/_static/image2.png)](adding-animation-to-a-control-vb/_static/image1.png)

패널은 페이딩 ([전체 크기 이미지를 보려면 클릭](adding-animation-to-a-control-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](dynamically-controlling-updatepanel-animations-cs.md)
> [다음](executing-several-animations-at-the-same-time-vb.md)
