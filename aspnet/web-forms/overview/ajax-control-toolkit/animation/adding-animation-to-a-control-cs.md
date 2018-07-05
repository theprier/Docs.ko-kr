---
uid: web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
title: 애니메이션 컨트롤을 추가 (C#) | Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 이 자습서에서는 방법...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 0f1fc1f5-9dbd-44e7-931e-387d42f0342b
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 80c982e041af2d0b9ee789665613ced0311dfcc9
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37396574"
---
<a name="adding-animation-to-a-control-c"></a>컨트롤 (C#)에 애니메이션 추가
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1CS.pdf)

> ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 이 자습서에서는 이러한 애니메이션을 설정 하는 방법을 보여 줍니다.


## <a name="overview"></a>개요

ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 이 자습서에서는 이러한 애니메이션을 설정 하는 방법을 보여 줍니다.

## <a name="steps"></a>단계

첫 번째 단계는 일반적으로 포함 합니다 `ScriptManager` 페이지에서 ASP.NET AJAX library가 로드 하 고 컨트롤 도구 키트를 사용할 수 있도록 합니다.

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample1.aspx)]

이 시나리오에서는 애니메이션 패널 다음과 같이 표시 됩니다는 텍스트에 적용 됩니다.

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample2.aspx)]

패널에 대 한 연결 된 CSS 클래스에는 배경 색과 너비를 정의합니다.

[!code-css[Main](adding-animation-to-a-control-cs/samples/sample3.css)]

필요한 up, 다음은 `AnimationExtender`합니다. 입력 한 후는 `ID` 및 일반적인 `runat="server"`, `TargetControlID` 특성 컨트롤에 여기서는 패널에서 애니메이션 효과를 설정 해야 합니다.

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample4.aspx)]

하지만 완전히 현재 Visual Studio의 IntelliSense에서 지원 하는 XML 구문을 사용 하 여 전체 애니메이션을 선언적으로 적용 됩니다. 루트 노드는 `<Animations>;` 이 노드 내에서 여러 이벤트는 사용할 수 있는 애니메이션의 현재 위치를 take(s) 하는 경우를 결정 합니다.

- `OnClick` (마우스 클릭)
- `OnHoverOut` (경우 마우스가 컨트롤)
- `OnHoverOver` (컨트롤 위로 마우스를 가져가면 중지는 `OnHoverOut` 애니메이션)
- `OnLoad` (때 페이지 로드 된)
- `OnMouseOut` (경우 마우스가 컨트롤)
- `OnMouseOver` (컨트롤 위로 마우스를 가져가면 중지 하지 않습니다는 `OnMouseOut` 애니메이션)

프레임 워크를 각각 자체 XML 요소로 표시 애니메이션 집합이 함께 제공 됩니다. 선택 영역은 다음과 같습니다.

- `<Color>` (색을 변경합니다.)
- `<FadeIn>` (페이드)
- `<FadeOut>` (페이드)
- `<Property>` (컨트롤의 속성을 변경합니다.)
- `<Pulse>` (pulsating)
- `<Resize>` (크기 변경)
- `<Scale>` (비례적으로 크기 변경)

이 예제에서는 패널은 페이드 아웃을 적용 합니다. 애니메이션 1.5 시간 (초)을 사용 해야 (`Duration` 특성), 초 당 24 프레임 (애니메이션 단계)을 표시 (`Fps` attributs). 전체 태그를 다음과 같습니다는 `AnimationExtender` 제어 합니다.

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample5.aspx)]

이 스크립트를 실행 하면 패널이 표시 되 고 1.5 명의 초에 페이드 아웃 합니다.


[![패널은 페이드아웃](adding-animation-to-a-control-cs/_static/image2.png)](adding-animation-to-a-control-cs/_static/image1.png)

패널은 페이드아웃 ([클릭 하 여 큰 이미지 보기](adding-animation-to-a-control-cs/_static/image3.png))

> [!div class="step-by-step"]
> [다음](executing-several-animations-at-the-same-time-cs.md)
