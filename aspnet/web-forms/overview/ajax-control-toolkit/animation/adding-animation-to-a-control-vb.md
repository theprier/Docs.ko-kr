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
ms.locfileid: "30870637"
---
<a name="adding-animation-to-a-control-vb"></a><span data-ttu-id="2ce37-104">애니메이션은 컨트롤 (VB)에 추가</span><span class="sxs-lookup"><span data-stu-id="2ce37-104">Adding Animation to a Control (VB)</span></span>
====================
<span data-ttu-id="2ce37-105">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="2ce37-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="2ce37-106">[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="2ce37-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1VB.pdf)</span></span>

> <span data-ttu-id="2ce37-107">ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="2ce37-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="2ce37-108">이 자습서에는 이러한 애니메이션을 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2ce37-108">This tutorial shows how to set up such an animation.</span></span>


## <a name="overview"></a><span data-ttu-id="2ce37-109">개요</span><span class="sxs-lookup"><span data-stu-id="2ce37-109">Overview</span></span>

<span data-ttu-id="2ce37-110">ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="2ce37-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="2ce37-111">이 자습서에는 이러한 애니메이션을 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2ce37-111">This tutorial shows how to set up such an animation.</span></span>

## <a name="steps"></a><span data-ttu-id="2ce37-112">단계</span><span class="sxs-lookup"><span data-stu-id="2ce37-112">Steps</span></span>

<span data-ttu-id="2ce37-113">첫 번째 단계는 일반적으로 포함는 `ScriptManager` 페이지에 있도록 ASP.NET AJAX 라이브러리를 로드 하 고 제어 도구 키트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ce37-113">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample1.aspx)]

<span data-ttu-id="2ce37-114">이 시나리오에서 애니메이션 다음과 같이 표시 된 텍스트의 패널에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ce37-114">The animation in this scenario will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample2.aspx)]

<span data-ttu-id="2ce37-115">패널에 대 한 연결 된 CSS 클래스에는 배경 색 및 너비를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce37-115">The associated CSS class for the panel defines a background color and a width:</span></span>

[!code-css[Main](adding-animation-to-a-control-vb/samples/sample3.css)]

<span data-ttu-id="2ce37-116">위쪽, 해야는 `AnimationExtender`합니다.</span><span class="sxs-lookup"><span data-stu-id="2ce37-116">Next up, we need the `AnimationExtender`.</span></span> <span data-ttu-id="2ce37-117">입력 한 후 프로그램 `ID` 는 일반적인 및 `runat="server"`, `TargetControlID` 특성 컨트롤에 패널 경우에서 애니메이션 효과를 설정 해야:</span><span class="sxs-lookup"><span data-stu-id="2ce37-117">After providing an `ID` and the usual `runat="server"`, the `TargetControlID` attribute must be set to the control to animate in our case, the panel:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample4.aspx)]

<span data-ttu-id="2ce37-118">하지만 Visual Studio의 IntelliSense에서 현재 완전히 지원 XML 구문을 사용 하 여 전체 애니메이션 선언적으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ce37-118">The whole animation is applied declaratively, using an XML syntax, unfortunately currently not fully supported by Visual Studio's IntelliSense.</span></span> <span data-ttu-id="2ce37-119">루트 노드는 `<Animations>;` 이 노드 내에서 여러 이벤트 애니메이션의 현재 위치 take(s) 시기를 결정 하는 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ce37-119">The root node is `<Animations>;` within this node, several events are allowed which determine when the animation(s) take(s) place:</span></span>

- <span data-ttu-id="2ce37-120">`OnClick` (마우스 클릭)</span><span class="sxs-lookup"><span data-stu-id="2ce37-120">`OnClick` (mouse click)</span></span>
- <span data-ttu-id="2ce37-121">`OnHoverOut` (마우스를 벗어날 때 컨트롤)</span><span class="sxs-lookup"><span data-stu-id="2ce37-121">`OnHoverOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="2ce37-122">`OnHoverOver` (중지를 컨트롤 위에 마우스를 가져가면는 `OnHoverOut` 애니메이션)</span><span class="sxs-lookup"><span data-stu-id="2ce37-122">`OnHoverOver` (when the mouse hovers over a control, stopping the `OnHoverOut` animation)</span></span>
- <span data-ttu-id="2ce37-123">`OnLoad` (때의 페이지 로드 된)</span><span class="sxs-lookup"><span data-stu-id="2ce37-123">`OnLoad` (when the page has been loaded)</span></span>
- <span data-ttu-id="2ce37-124">`OnMouseOut` (마우스를 벗어날 때 컨트롤)</span><span class="sxs-lookup"><span data-stu-id="2ce37-124">`OnMouseOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="2ce37-125">`OnMouseOver` (컨트롤 위에 마우스를 가져가면 중지 하지는 `OnMouseOut` 애니메이션)</span><span class="sxs-lookup"><span data-stu-id="2ce37-125">`OnMouseOver` (when the mouse hovers over a control, not stopping the `OnMouseOut` animation)</span></span>

<span data-ttu-id="2ce37-126">프레임 워크 자체 XML 요소로 표시 하나씩 애니메이션 집합이 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ce37-126">The framework comes with a set of animations, each one represented by its own XML element.</span></span> <span data-ttu-id="2ce37-127">선택 영역 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2ce37-127">Here is a selection:</span></span>

- <span data-ttu-id="2ce37-128">`<Color>` (색을 변경합니다.)</span><span class="sxs-lookup"><span data-stu-id="2ce37-128">`<Color>` (changing a color)</span></span>
- <span data-ttu-id="2ce37-129">`<FadeIn>` (페이딩)</span><span class="sxs-lookup"><span data-stu-id="2ce37-129">`<FadeIn>` (fading in)</span></span>
- <span data-ttu-id="2ce37-130">`<FadeOut>` (페이드 아웃)</span><span class="sxs-lookup"><span data-stu-id="2ce37-130">`<FadeOut>` (fading out)</span></span>
- <span data-ttu-id="2ce37-131">`<Property>` (컨트롤의 속성을 변경합니다.)</span><span class="sxs-lookup"><span data-stu-id="2ce37-131">`<Property>` (changing a control's property)</span></span>
- <span data-ttu-id="2ce37-132">`<Pulse>` (pulsating)</span><span class="sxs-lookup"><span data-stu-id="2ce37-132">`<Pulse>` (pulsating)</span></span>
- <span data-ttu-id="2ce37-133">`<Resize>` (크기 변경)</span><span class="sxs-lookup"><span data-stu-id="2ce37-133">`<Resize>` (changing the size)</span></span>
- <span data-ttu-id="2ce37-134">`<Scale>` (비례적으로 크기를 변경)</span><span class="sxs-lookup"><span data-stu-id="2ce37-134">`<Scale>` (proportionally changing the size)</span></span>

<span data-ttu-id="2ce37-135">이 예제에서는 패널은 페이드 아웃 합니다. 애니메이션 1.5 초 취해 (`Duration` 특성), 초당 프레임 (애니메이션 단계) 24 표시 (`Fps` attributs).</span><span class="sxs-lookup"><span data-stu-id="2ce37-135">In this example, the panel shall fade out. The animation shall take 1.5 seconds (`Duration` attribute), displaying 24 frames (animation steps) per second (`Fps` attributs).</span></span> <span data-ttu-id="2ce37-136">다음은 전체 태그를는 `AnimationExtender` 제어:</span><span class="sxs-lookup"><span data-stu-id="2ce37-136">Here is the complete markup for the `AnimationExtender` control:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample5.aspx)]

<span data-ttu-id="2ce37-137">이 스크립트를 실행 하면 패널 표시 되 고 일 분 초에서 사라집니다.</span><span class="sxs-lookup"><span data-stu-id="2ce37-137">When you run this script, the panel is displayed and fades out in one and a half seconds.</span></span>


<span data-ttu-id="2ce37-138">[![패널은 옅은 색](adding-animation-to-a-control-vb/_static/image2.png)](adding-animation-to-a-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2ce37-138">[![The panel is fading out](adding-animation-to-a-control-vb/_static/image2.png)](adding-animation-to-a-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="2ce37-139">패널은 페이딩 ([전체 크기 이미지를 보려면 클릭](adding-animation-to-a-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="2ce37-139">The panel is fading out ([Click to view full-size image](adding-animation-to-a-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2ce37-140">[이전](dynamically-controlling-updatepanel-animations-cs.md)
> [다음](executing-several-animations-at-the-same-time-vb.md)</span><span class="sxs-lookup"><span data-stu-id="2ce37-140">[Previous](dynamically-controlling-updatepanel-animations-cs.md)
[Next](executing-several-animations-at-the-same-time-vb.md)</span></span>
