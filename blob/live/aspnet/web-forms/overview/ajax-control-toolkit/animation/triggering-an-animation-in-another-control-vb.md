---
uid: web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
title: "다른 컨트롤 (VB) 애니메이션 트리거 | Microsoft Docs"
author: wenz
description: "ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 일반적으로 시작는 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 25ebaf1f-5a9f-423d-98c7-1d694e93664f
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
msc.type: authoredcontent
ms.openlocfilehash: ce1d29cbd06ef8a470780ff4c7bda8039575d59f
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="triggering-an-animation-in-another-control-vb"></a><span data-ttu-id="4e249-104">다른 컨트롤 (VB) 애니메이션 트리거</span><span class="sxs-lookup"><span data-stu-id="4e249-104">Triggering an Animation in another Control (VB)</span></span>
====================
<span data-ttu-id="4e249-105">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="4e249-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="4e249-106">[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="4e249-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8VB.pdf)</span></span>

> <span data-ttu-id="4e249-107">ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="4e249-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="4e249-108">일반적으로 애니메이션 시작에 의해 트리거될 동일한 컨트롤과 상호 작용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e249-108">Generally, launching an animation is triggered by user interaction with the same control.</span></span> <span data-ttu-id="4e249-109">그러나 또한 다른 컨트롤을 한 개의 컨트롤 및 애니메이션와 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e249-109">It is however also possible to interact with one control and then animation another control.</span></span>


## <a name="overview"></a><span data-ttu-id="4e249-110">개요</span><span class="sxs-lookup"><span data-stu-id="4e249-110">Overview</span></span>

<span data-ttu-id="4e249-111">ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="4e249-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="4e249-112">일반적으로 애니메이션 시작에 의해 트리거될 동일한 컨트롤과 상호 작용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e249-112">Generally, launching an animation is triggered by user interaction with the same control.</span></span> <span data-ttu-id="4e249-113">그러나 또한 다른 컨트롤을 한 개의 컨트롤 및 애니메이션와 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e249-113">It is however also possible to interact with one control and then animation another control.</span></span>

## <a name="steps"></a><span data-ttu-id="4e249-114">단계</span><span class="sxs-lookup"><span data-stu-id="4e249-114">Steps</span></span>

<span data-ttu-id="4e249-115">우선, 포함 된 `ScriptManager` 페이지; 그런 다음 ASP.NET AJAX 라이브러리 로드 되는 제어 도구 키트를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="4e249-115">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample1.aspx)]

<span data-ttu-id="4e249-116">그러면 다음과 같은 텍스트의 패널에 애니메이션 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e249-116">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample2.aspx)]

<span data-ttu-id="4e249-117">패널에 대 한 연결 된 CSS 클래스 좋은 배경색을 정의 하 고도 패널 고정된 폭을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e249-117">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](triggering-an-animation-in-another-control-vb/samples/sample3.css)]

<span data-ttu-id="4e249-118">패널에 애니메이션 적용을 시작 하기 위해 HTML 단추가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e249-118">In order to start animating the panel, an HTML button is used.</span></span> <span data-ttu-id="4e249-119">`<input type="button" />` 들이 통해 좋아하는 `<asp:Button />` 사용자가 해당 단추를 클릭할 때 포스트백을 원치 않으므로 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="4e249-119">Note that `<input type="button" />` is favoured over `<asp:Button />` since we do not want a postback when the user clicks on that button.</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample4.aspx)]

<span data-ttu-id="4e249-120">그런 다음 추가 `AnimationExtender` 페이지에 제공 하는 `ID`, `TargetControlID` 특성과 반드시 `runat="server"`합니다.</span><span class="sxs-lookup"><span data-stu-id="4e249-120">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`.</span></span> <span data-ttu-id="4e249-121">설정 해야 `TargetControlID` 단추 (애니메이션 트리거 요소)의 ID로 패널 (애니메이션 효과가 적용 되는 요소)의 ID로 하지</span><span class="sxs-lookup"><span data-stu-id="4e249-121">It is important to set `TargetControlID` to the ID of the button (the element triggering the animation), not to the ID of the panel (the element being animated)</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample5.aspx)]

<span data-ttu-id="4e249-122">내에서 `<Animations>` 노드를 일반적인 방법 대로 위치 애니메이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e249-122">Within the `<Animations>` node, place animations as usual.</span></span> <span data-ttu-id="4e249-123">패널을 변경할 수를 단추가 아닌 설정의 `AnimationTarget` 특성 내에서 모든 애니메이션 요소에 대해 `AnimationExtender`합니다.</span><span class="sxs-lookup"><span data-stu-id="4e249-123">In order to make them change the panel, not the button, set the `AnimationTarget` attribute for every animation element within `AnimationExtender`.</span></span> <span data-ttu-id="4e249-124">에 대 한 값 `AnimationTarget` 패널의 ID는 물론 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e249-124">The value for `AnimationTarget` is the ID of the panel, of course.</span></span> <span data-ttu-id="4e249-125">이런 방식으로 애니메이션 트리거 단추와 패널에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e249-125">That way, the animations happen with the panel, not with the triggering button.</span></span> <span data-ttu-id="4e249-126">다음은 `AnimationExtender` 이 시나리오에 대 한 태그:</span><span class="sxs-lookup"><span data-stu-id="4e249-126">Here is the `AnimationExtender` markup for this scenario:</span></span>

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample6.aspx)]

<span data-ttu-id="4e249-127">Note 개별 애니메이션이 표시 되는 특별 한 순서입니다.</span><span class="sxs-lookup"><span data-stu-id="4e249-127">Note the special order in which the individual animations appear.</span></span> <span data-ttu-id="4e249-128">우선, 애니메이션 실행 되 면 단추 비활성화를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4e249-128">First of all, the button gets deactivated once the animation runs.</span></span> <span data-ttu-id="4e249-129">없기 때문 없는 `AnimationTarget` 특성에 `<EnableAction>` 요소가이 애니메이션 원본 컨트롤에 적용 되: 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="4e249-129">Since there is no `AnimationTarget` attribute in the `<EnableAction>` element, this animation is applied to the originating control: the button.</span></span> <span data-ttu-id="4e249-130">애니메이션을 다음 두 단계는 수행 parallelly (`<Parallel>` 요소).</span><span class="sxs-lookup"><span data-stu-id="4e249-130">The next two animation steps shall be carried out parallelly (`<Parallel>` element).</span></span> <span data-ttu-id="4e249-131">둘 다의 `AnimationTarget` 특성으로 설정 `"Panel1"`, 따라서 단추가 아니라 패널에 애니메이션을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e249-131">Both have their `AnimationTarget` attributes set to `"Panel1"`, thus animating the panel, not the button.</span></span>


<span data-ttu-id="4e249-132">[![패널 애니메이션을 시작 하는 마우스 단추 클릭](triggering-an-animation-in-another-control-vb/_static/image2.png)](triggering-an-animation-in-another-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4e249-132">[![A mouse click on the button starts the panel animation](triggering-an-animation-in-another-control-vb/_static/image2.png)](triggering-an-animation-in-another-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="4e249-133">패널 애니메이션을 시작 하는 마우스 단추 클릭 ([전체 크기 이미지를 보려면 클릭](triggering-an-animation-in-another-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="4e249-133">A mouse click on the button starts the panel animation ([Click to view full-size image](triggering-an-animation-in-another-control-vb/_static/image3.png))</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="4e249-134">[이전](disabling-actions-during-animation-vb.md)
[다음](modifying-animations-from-the-server-side-vb.md)</span><span class="sxs-lookup"><span data-stu-id="4e249-134">[Previous](disabling-actions-during-animation-vb.md)
[Next](modifying-animations-from-the-server-side-vb.md)</span></span>
