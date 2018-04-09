---
uid: web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
title: 조건 (C#)에 따라 애니메이션 | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 애니메이션 인지 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: b7a28c0d-efb9-443a-80a4-1a5ee54671cd
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
msc.type: authoredcontent
ms.openlocfilehash: b530239e76654bc68a8fa6ac900a20df1d5699b0
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="animation-depending-on-a-condition-c"></a><span data-ttu-id="b383c-104">조건 (C#)에 따라 애니메이션</span><span class="sxs-lookup"><span data-stu-id="b383c-104">Animation Depending On a Condition (C#)</span></span>
====================
<span data-ttu-id="b383c-105">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="b383c-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="b383c-106">[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="b383c-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4CS.pdf)</span></span>

> <span data-ttu-id="b383c-107">ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="b383c-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="b383c-108">애니메이션이 실행 여부 형태의 일부 JavaScript 코드에서 조건에도 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b383c-108">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="b383c-109">개요</span><span class="sxs-lookup"><span data-stu-id="b383c-109">Overview</span></span>

<span data-ttu-id="b383c-110">ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="b383c-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="b383c-111">애니메이션이 실행 여부 형태의 일부 JavaScript 코드에서 조건에도 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b383c-111">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="b383c-112">단계</span><span class="sxs-lookup"><span data-stu-id="b383c-112">Steps</span></span>

<span data-ttu-id="b383c-113">우선, 포함 된 `ScriptManager` 페이지; 그런 다음 ASP.NET AJAX 라이브러리 로드 되는 제어 도구 키트를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="b383c-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample1.aspx)]

<span data-ttu-id="b383c-114">그러면 다음과 같은 텍스트의 패널에 애니메이션 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b383c-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample2.aspx)]

<span data-ttu-id="b383c-115">패널에 대 한 연결 된 CSS 클래스 좋은 배경색을 정의 하 고도 패널 고정된 폭을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b383c-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animation-depending-on-a-condition-cs/samples/sample3.css)]

<span data-ttu-id="b383c-116">그런 다음 추가 `AnimationExtender` 페이지에 제공 하는 `ID`, `TargetControlID` 특성과 참가 `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="b383c-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample4.aspx)]

<span data-ttu-id="b383c-117">내에서 `<Animations>` 노드를 사용 하 여 `<OnLoad>` 페이지가 완전히 로드 되 면 애니메이션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b383c-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="b383c-118">대신 일반 애니메이션 중 하나는 `<Condition>` 요소에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b383c-118">Instead of one of the regular animations, the `<Condition>` element comes into play.</span></span> <span data-ttu-id="b383c-119">값으로 제공 하는 JavaScript 코드는 `ConditionScript` 특성은 런타임 시 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b383c-119">The JavaScript code provided as the value of the `ConditionScript` attribute is executed at runtime.</span></span> <span data-ttu-id="b383c-120">True로 평가 될 경우 애니메이션 실행 되어 그렇지 않으면 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b383c-120">If it evaluates to true, the animation is executed, otherwise not.</span></span> <span data-ttu-id="b383c-121">다음 태그는 각각의 임의 시 사례의 50%에서 실행 되는 두 개의 애니메이션이 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b383c-121">The following markup provides two animations, each of them being executed in 50% of cases upon random.</span></span> <span data-ttu-id="b383c-122">내에서 하나의 애니메이션 수만 있으므로 `<OnLoad>`, 두 `<Condition>` 애니메이션을 사용 하 여 함께 조인에서 `<Sequence>` 요소:</span><span class="sxs-lookup"><span data-stu-id="b383c-122">Since there may only be one animation within `<OnLoad>`, the two `<Condition>` animations are joined together using the `<Sequence>` element:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample5.aspx)]

<span data-ttu-id="b383c-123">보다 작음 부호 (`<`)에 `ConditionScript` 특성 (이스케이프) 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b383c-123">Note that the less than sign (`<`) in the `ConditionScript` attribute must be escaped ().</span></span> <span data-ttu-id="b383c-124">때 하거나 애니메이션 실행이 없습니다,이 스크립트를 실행 하거나 수행 하는 두 가지 중 하나 하거나 모두 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b383c-124">When you run this script, either no animation runs, or one of the two does, or both do.</span></span>


<span data-ttu-id="b383c-125">[![패널은 페이딩 크기를 조정 하지 않고 첫 번째는 두 번째 애니메이션 실행 하지 않은 하므로](animation-depending-on-a-condition-cs/_static/image2.png)](animation-depending-on-a-condition-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b383c-125">[![The panel is fading out without resizing, so the second animation runs, the first one didn't](animation-depending-on-a-condition-cs/_static/image2.png)](animation-depending-on-a-condition-cs/_static/image1.png)</span></span>

<span data-ttu-id="b383c-126">패널은 페이딩 크기를 조정 하지 않고 첫 번째는 두 번째 애니메이션 실행 하지 않은 하므로 ([전체 크기 이미지를 보려면 클릭](animation-depending-on-a-condition-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="b383c-126">The panel is fading out without resizing, so the second animation runs, the first one didn't ([Click to view full-size image](animation-depending-on-a-condition-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b383c-127">[이전](executing-several-animations-after-each-other-cs.md)
> [다음](picking-one-animation-out-of-a-list-cs.md)</span><span class="sxs-lookup"><span data-stu-id="b383c-127">[Previous](executing-several-animations-after-each-other-cs.md)
[Next](picking-one-animation-out-of-a-list-cs.md)</span></span>
