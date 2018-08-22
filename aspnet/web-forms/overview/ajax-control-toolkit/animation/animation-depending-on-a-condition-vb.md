---
uid: web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-vb
title: 애니메이션 (VB) 조건에 따라 | Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 애니메이션 인지 하는 중...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1b87d8d6-b3f7-4126-b51c-d41442fbf947
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-vb
msc.type: authoredcontent
ms.openlocfilehash: be43b68ce77819cdcd09d8e875604db90e8a8d96
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830338"
---
<a name="animation-depending-on-a-condition-vb"></a><span data-ttu-id="acef5-104">애니메이션 (VB) 조건에 따라</span><span class="sxs-lookup"><span data-stu-id="acef5-104">Animation Depending On a Condition (VB)</span></span>
====================
<span data-ttu-id="acef5-105">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="acef5-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="acef5-106">[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="acef5-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4VB.pdf)</span></span>

> <span data-ttu-id="acef5-107">ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="acef5-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="acef5-108">여부 애니메이션 실행 되는 여부 일부 JavaScript 코드의 형태로 조건에도 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acef5-108">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="acef5-109">개요</span><span class="sxs-lookup"><span data-stu-id="acef5-109">Overview</span></span>

<span data-ttu-id="acef5-110">ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="acef5-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="acef5-111">여부 애니메이션 실행 되는 여부 일부 JavaScript 코드의 형태로 조건에도 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acef5-111">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="acef5-112">단계</span><span class="sxs-lookup"><span data-stu-id="acef5-112">Steps</span></span>

<span data-ttu-id="acef5-113">첫째, 포함 된 `ScriptManager` 페이지 그런 다음 ASP.NET AJAX 라이브러리 로드 되 면 컨트롤 도구 키트를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="acef5-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample1.aspx)]

<span data-ttu-id="acef5-114">그러면 다음과 같은 텍스트 패널에 애니메이션 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acef5-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample2.aspx)]

<span data-ttu-id="acef5-115">패널에 대 한 연결 된 CSS 클래스에 유용한 배경 색을 정의 하 고 패널 고정된 너비를 설정할 수도:</span><span class="sxs-lookup"><span data-stu-id="acef5-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animation-depending-on-a-condition-vb/samples/sample3.css)]

<span data-ttu-id="acef5-116">그런 다음 추가 `AnimationExtender` 페이지에서 제공 하는 `ID`, `TargetControlID` 특성과 필수 항목 이지만 `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="acef5-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample4.aspx)]

<span data-ttu-id="acef5-117">내 합니다 `<Animations>` 노드를 사용 하 여 `<OnLoad>` 페이지가 완전히 로드 되 면 애니메이션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="acef5-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="acef5-118">대신 일반 애니메이션 중 하나는 `<Condition>` 요소 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acef5-118">Instead of one of the regular animations, the `<Condition>` element comes into play.</span></span> <span data-ttu-id="acef5-119">값으로 제공 하는 JavaScript 코드는 `ConditionScript` 특성은 런타임 시 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acef5-119">The JavaScript code provided as the value of the `ConditionScript` attribute is executed at runtime.</span></span> <span data-ttu-id="acef5-120">True로 평가 될 경우 애니메이션 실행 되어이 고, 그렇지 없습니다.</span><span class="sxs-lookup"><span data-stu-id="acef5-120">If it evaluates to true, the animation is executed, otherwise not.</span></span> <span data-ttu-id="acef5-121">다음 태그는 임의 시 사례의 50%에서 실행 되 고 각 두 애니메이션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="acef5-121">The following markup provides two animations, each of them being executed in 50% of cases upon random.</span></span> <span data-ttu-id="acef5-122">내에서 애니메이션 하나 수만 있으므로 `<OnLoad>`, 두 개의 `<Condition>` 애니메이션 사용 하 여 함께 조인 되는 `<Sequence>` 요소:</span><span class="sxs-lookup"><span data-stu-id="acef5-122">Since there may only be one animation within `<OnLoad>`, the two `<Condition>` animations are joined together using the `<Sequence>` element:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-vb/samples/sample5.aspx)]

<span data-ttu-id="acef5-123">보다 작음 부호 (`<`)에 `ConditionScript` 이스케이프 ()을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acef5-123">Note that the less than sign (`<`) in the `ConditionScript` attribute must be escaped ().</span></span> <span data-ttu-id="acef5-124">경우 하거나 애니메이션 실행이 없습니다,이 스크립트를 실행 하면 아니라 둘 중 하나 또는 둘 다 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="acef5-124">When you run this script, either no animation runs, or one of the two does, or both do.</span></span>


<span data-ttu-id="acef5-125">[![패널은 페이드아웃 크기 조정 없이 첫 번째 두 번째 애니메이션 실행 하지 않은 하므로](animation-depending-on-a-condition-vb/_static/image2.png)](animation-depending-on-a-condition-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="acef5-125">[![The panel is fading out without resizing, so the second animation runs, the first one didn't](animation-depending-on-a-condition-vb/_static/image2.png)](animation-depending-on-a-condition-vb/_static/image1.png)</span></span>

<span data-ttu-id="acef5-126">패널은 페이드아웃 크기 조정 없이 첫 번째 두 번째 애니메이션 실행 하지 않은 하도록 ([클릭 하 여 큰 이미지 보기](animation-depending-on-a-condition-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="acef5-126">The panel is fading out without resizing, so the second animation runs, the first one didn't ([Click to view full-size image](animation-depending-on-a-condition-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="acef5-127">[이전](executing-several-animations-after-each-other-vb.md)
> [다음](picking-one-animation-out-of-a-list-vb.md)</span><span class="sxs-lookup"><span data-stu-id="acef5-127">[Previous](executing-several-animations-after-each-other-vb.md)
[Next](picking-one-animation-out-of-a-list-vb.md)</span></span>
