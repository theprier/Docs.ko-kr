---
uid: web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
title: "애니메이션 컨트롤 (C#)에 추가 | Microsoft Docs"
author: wenz
description: "ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 이 자습서에서는 방법..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 0f1fc1f5-9dbd-44e7-931e-387d42f0342b
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 7016ae3c92c665136579a8588818e6e4179a102a
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="adding-animation-to-a-control-c"></a><span data-ttu-id="6a169-104">애니메이션 컨트롤을 추가 (C#)</span><span class="sxs-lookup"><span data-stu-id="6a169-104">Adding Animation to a Control (C#)</span></span>
====================
<span data-ttu-id="6a169-105">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="6a169-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="6a169-106">[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="6a169-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1CS.pdf)</span></span>

> <span data-ttu-id="6a169-107">ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="6a169-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="6a169-108">이 자습서에는 이러한 애니메이션을 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6a169-108">This tutorial shows how to set up such an animation.</span></span>


## <a name="overview"></a><span data-ttu-id="6a169-109">개요</span><span class="sxs-lookup"><span data-stu-id="6a169-109">Overview</span></span>

<span data-ttu-id="6a169-110">ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="6a169-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="6a169-111">이 자습서에는 이러한 애니메이션을 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6a169-111">This tutorial shows how to set up such an animation.</span></span>

## <a name="steps"></a><span data-ttu-id="6a169-112">단계</span><span class="sxs-lookup"><span data-stu-id="6a169-112">Steps</span></span>

<span data-ttu-id="6a169-113">첫 번째 단계는 일반적으로 포함는 `ScriptManager` 페이지에 있도록 ASP.NET AJAX 라이브러리를 로드 하 고 제어 도구 키트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a169-113">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample1.aspx)]

<span data-ttu-id="6a169-114">이 시나리오에서 애니메이션 다음과 같이 표시 된 텍스트의 패널에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a169-114">The animation in this scenario will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample2.aspx)]

<span data-ttu-id="6a169-115">패널에 대 한 연결 된 CSS 클래스에는 배경 색 및 너비를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6a169-115">The associated CSS class for the panel defines a background color and a width:</span></span>

[!code-css[Main](adding-animation-to-a-control-cs/samples/sample3.css)]

<span data-ttu-id="6a169-116">위쪽, 해야는 `AnimationExtender`합니다.</span><span class="sxs-lookup"><span data-stu-id="6a169-116">Next up, we need the `AnimationExtender`.</span></span> <span data-ttu-id="6a169-117">입력 한 후 프로그램 `ID` 는 일반적인 및 `runat="server"`, `TargetControlID` 특성 컨트롤에 패널 경우에서 애니메이션 효과를 설정 해야:</span><span class="sxs-lookup"><span data-stu-id="6a169-117">After providing an `ID` and the usual `runat="server"`, the `TargetControlID` attribute must be set to the control to animate in our case, the panel:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample4.aspx)]

<span data-ttu-id="6a169-118">하지만 Visual Studio의 IntelliSense에서 현재 완전히 지원 XML 구문을 사용 하 여 전체 애니메이션 선언적으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a169-118">The whole animation is applied declaratively, using an XML syntax, unfortunately currently not fully supported by Visual Studio's IntelliSense.</span></span> <span data-ttu-id="6a169-119">루트 노드는 `<Animations>;` 이 노드 내에서 여러 이벤트 애니메이션의 현재 위치 take(s) 시기를 결정 하는 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a169-119">The root node is `<Animations>;` within this node, several events are allowed which determine when the animation(s) take(s) place:</span></span>

- <span data-ttu-id="6a169-120">`OnClick`(마우스 클릭)</span><span class="sxs-lookup"><span data-stu-id="6a169-120">`OnClick` (mouse click)</span></span>
- <span data-ttu-id="6a169-121">`OnHoverOut`(마우스를 벗어날 때 컨트롤)</span><span class="sxs-lookup"><span data-stu-id="6a169-121">`OnHoverOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="6a169-122">`OnHoverOver`(중지를 컨트롤 위에 마우스를 가져가면는 `OnHoverOut` 애니메이션)</span><span class="sxs-lookup"><span data-stu-id="6a169-122">`OnHoverOver` (when the mouse hovers over a control, stopping the `OnHoverOut` animation)</span></span>
- <span data-ttu-id="6a169-123">`OnLoad`(때의 페이지 로드 된)</span><span class="sxs-lookup"><span data-stu-id="6a169-123">`OnLoad` (when the page has been loaded)</span></span>
- <span data-ttu-id="6a169-124">`OnMouseOut`(마우스를 벗어날 때 컨트롤)</span><span class="sxs-lookup"><span data-stu-id="6a169-124">`OnMouseOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="6a169-125">`OnMouseOver`(컨트롤 위에 마우스를 가져가면 중지 하지는 `OnMouseOut` 애니메이션)</span><span class="sxs-lookup"><span data-stu-id="6a169-125">`OnMouseOver` (when the mouse hovers over a control, not stopping the `OnMouseOut` animation)</span></span>

<span data-ttu-id="6a169-126">프레임 워크 자체 XML 요소로 표시 하나씩 애니메이션 집합이 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a169-126">The framework comes with a set of animations, each one represented by its own XML element.</span></span> <span data-ttu-id="6a169-127">선택 영역 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6a169-127">Here is a selection:</span></span>

- <span data-ttu-id="6a169-128">`<Color>`(색을 변경합니다.)</span><span class="sxs-lookup"><span data-stu-id="6a169-128">`<Color>` (changing a color)</span></span>
- <span data-ttu-id="6a169-129">`<FadeIn>`(페이딩)</span><span class="sxs-lookup"><span data-stu-id="6a169-129">`<FadeIn>` (fading in)</span></span>
- <span data-ttu-id="6a169-130">`<FadeOut>`(페이드 아웃)</span><span class="sxs-lookup"><span data-stu-id="6a169-130">`<FadeOut>` (fading out)</span></span>
- <span data-ttu-id="6a169-131">`<Property>`(컨트롤의 속성을 변경합니다.)</span><span class="sxs-lookup"><span data-stu-id="6a169-131">`<Property>` (changing a control's property)</span></span>
- <span data-ttu-id="6a169-132">`<Pulse>`(pulsating)</span><span class="sxs-lookup"><span data-stu-id="6a169-132">`<Pulse>` (pulsating)</span></span>
- <span data-ttu-id="6a169-133">`<Resize>`(크기 변경)</span><span class="sxs-lookup"><span data-stu-id="6a169-133">`<Resize>` (changing the size)</span></span>
- <span data-ttu-id="6a169-134">`<Scale>`(비례적으로 크기를 변경)</span><span class="sxs-lookup"><span data-stu-id="6a169-134">`<Scale>` (proportionally changing the size)</span></span>

<span data-ttu-id="6a169-135">이 예제에서는 패널은 페이드 아웃 합니다. 애니메이션 1.5 초 취해 (`Duration` 특성), 초당 프레임 (애니메이션 단계) 24 표시 (`Fps` attributs).</span><span class="sxs-lookup"><span data-stu-id="6a169-135">In this example, the panel shall fade out. The animation shall take 1.5 seconds (`Duration` attribute), displaying 24 frames (animation steps) per second (`Fps` attributs).</span></span> <span data-ttu-id="6a169-136">다음은 전체 태그를는 `AnimationExtender` 제어:</span><span class="sxs-lookup"><span data-stu-id="6a169-136">Here is the complete markup for the `AnimationExtender` control:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample5.aspx)]

<span data-ttu-id="6a169-137">이 스크립트를 실행 하면 패널 표시 되 고 일 분 초에서 사라집니다.</span><span class="sxs-lookup"><span data-stu-id="6a169-137">When you run this script, the panel is displayed and fades out in one and a half seconds.</span></span>


<span data-ttu-id="6a169-138">[![패널은 옅은 색](adding-animation-to-a-control-cs/_static/image2.png)](adding-animation-to-a-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6a169-138">[![The panel is fading out](adding-animation-to-a-control-cs/_static/image2.png)](adding-animation-to-a-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="6a169-139">패널은 페이딩 ([전체 크기 이미지를 보려면 클릭](adding-animation-to-a-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="6a169-139">The panel is fading out ([Click to view full-size image](adding-animation-to-a-control-cs/_static/image3.png))</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="6a169-140">다음</span><span class="sxs-lookup"><span data-stu-id="6a169-140">Next</span></span>](executing-several-animations-at-the-same-time-cs.md)
