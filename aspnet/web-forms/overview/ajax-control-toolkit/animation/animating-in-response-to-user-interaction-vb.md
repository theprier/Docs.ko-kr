---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
title: 사용자 상호 작용 (VB)에 대 한 응답으로 애니메이션 효과 주는 | Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 애니메이션 별 있습니다...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: c8204c05-ec27-40fe-933d-88e4e727a482
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
msc.type: authoredcontent
ms.openlocfilehash: 4b774a058e715e4a98e767daf92886f24e627822
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37815527"
---
<a name="animating-in-response-to-user-interaction-vb"></a><span data-ttu-id="a24ac-104">사용자 상호 작용 (VB)에 대 한 응답으로 애니메이션 적용</span><span class="sxs-lookup"><span data-stu-id="a24ac-104">Animating in Response To User Interaction (VB)</span></span>
====================
<span data-ttu-id="a24ac-105">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="a24ac-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a24ac-106">[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="a24ac-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6VB.pdf)</span></span>

> <span data-ttu-id="a24ac-107">ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a24ac-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="a24ac-108">애니메이션은 자동으로 시작 하거나 트리거될 수 있습니다 사용자 상호 작용 하 여 예를 들어 마우스로 클릭 하 여.</span><span class="sxs-lookup"><span data-stu-id="a24ac-108">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>


## <a name="overview"></a><span data-ttu-id="a24ac-109">개요</span><span class="sxs-lookup"><span data-stu-id="a24ac-109">Overview</span></span>

<span data-ttu-id="a24ac-110">ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a24ac-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="a24ac-111">애니메이션은 자동으로 시작 하거나 트리거될 수 있습니다 사용자 상호 작용 하 여 예를 들어 마우스로 클릭 하 여.</span><span class="sxs-lookup"><span data-stu-id="a24ac-111">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="steps"></a><span data-ttu-id="a24ac-112">단계</span><span class="sxs-lookup"><span data-stu-id="a24ac-112">Steps</span></span>

<span data-ttu-id="a24ac-113">첫째, 포함 된 `ScriptManager` 페이지 그런 다음 ASP.NET AJAX 라이브러리 로드 되 면 컨트롤 도구 키트를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="a24ac-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample1.aspx)]

<span data-ttu-id="a24ac-114">그러면 다음과 같은 텍스트 패널에 애니메이션 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a24ac-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample2.aspx)]

<span data-ttu-id="a24ac-115">패널에 대 한 연결 된 CSS 클래스에 유용한 배경 색을 정의 하 고 패널 고정된 너비를 설정할 수도:</span><span class="sxs-lookup"><span data-stu-id="a24ac-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animating-in-response-to-user-interaction-vb/samples/sample3.css)]

<span data-ttu-id="a24ac-116">그런 다음 추가 `AnimationExtender` 페이지에서 제공 하는 `ID`, `TargetControlID` 특성과 필수 항목 이지만 `runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="a24ac-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample4.aspx)]

<span data-ttu-id="a24ac-117">내 합니다 `<Animations>` 노드를 사용자 상호 작용을 통해 애니메이션을 시작 하는 방법은 5 가지가 있습니다 (누락 된 요소는 `<OnLoad>` 전체 페이지가 완전히 로드 되 면 실행 되는):</span><span class="sxs-lookup"><span data-stu-id="a24ac-117">Within the `<Animations>` node, there are five ways to start the animation via user interaction (the missing element is `<OnLoad>` which is executed once the whole page has been fully loaded):</span></span>

- <span data-ttu-id="a24ac-118">`<OnClick>` (컨트롤의 마우스 클릭)</span><span class="sxs-lookup"><span data-stu-id="a24ac-118">`<OnClick>` (mouse click on the control)</span></span>
- <span data-ttu-id="a24ac-119">`<OnHoverOut>` (마우스가 컨트롤)</span><span class="sxs-lookup"><span data-stu-id="a24ac-119">`<OnHoverOut>` (mouse leaves the control)</span></span>
- <span data-ttu-id="a24ac-120">`<OnHoverOver>` (중지 컨트롤을 마우스로 `<OnHoverOut>` 애니메이션)</span><span class="sxs-lookup"><span data-stu-id="a24ac-120">`<OnHoverOver>` (mouse hovers over a control, stopping the `<OnHoverOut>` animation)</span></span>
- <span data-ttu-id="a24ac-121">`<OnMouseOut>` (마우스가 컨트롤)</span><span class="sxs-lookup"><span data-stu-id="a24ac-121">`<OnMouseOut>` (mouse leaves a control)</span></span>
- <span data-ttu-id="a24ac-122">`<OnMouseOver>` (중지 컨트롤을 마우스로 `<OnMouseOut>` 애니메이션)</span><span class="sxs-lookup"><span data-stu-id="a24ac-122">`<OnMouseOver>` (mouse hovers over a control, not stopping the `<OnMouseOut>` animation)</span></span>

<span data-ttu-id="a24ac-123">이 시나리오에서는 `<OnClick>` 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a24ac-123">In this scenario, `<OnClick>` is used.</span></span> <span data-ttu-id="a24ac-124">패널에서 사용자가 크기를 조정 하 고 동시에 페이드 아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="a24ac-124">When the user clicks on the panel, it is resized and fades out at the same time.</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample5.aspx)]


<span data-ttu-id="a24ac-125">[![애니메이션을 시작 하는 마우스 클릭](animating-in-response-to-user-interaction-vb/_static/image2.png)](animating-in-response-to-user-interaction-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a24ac-125">[![A mouse click starts the animation](animating-in-response-to-user-interaction-vb/_static/image2.png)](animating-in-response-to-user-interaction-vb/_static/image1.png)</span></span>

<span data-ttu-id="a24ac-126">마우스 클릭 애니메이션을 시작 ([클릭 하 여 큰 이미지 보기](animating-in-response-to-user-interaction-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="a24ac-126">A mouse click starts the animation ([Click to view full-size image](animating-in-response-to-user-interaction-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a24ac-127">[이전](picking-one-animation-out-of-a-list-vb.md)
> [다음](disabling-actions-during-animation-vb.md)</span><span class="sxs-lookup"><span data-stu-id="a24ac-127">[Previous](picking-one-animation-out-of-a-list-vb.md)
[Next](disabling-actions-during-animation-vb.md)</span></span>
