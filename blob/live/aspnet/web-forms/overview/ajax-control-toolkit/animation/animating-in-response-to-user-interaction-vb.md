---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
title: "사용자 상호 작용 (VB)에 대 한 응답에서 애니메이션이 | Microsoft Docs"
author: wenz
description: "ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 애니메이션 별 있습니다..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: c8204c05-ec27-40fe-933d-88e4e727a482
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
msc.type: authoredcontent
ms.openlocfilehash: 3219e9d126b3225bfc78d08fb3ac7ef4cc3dca75
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="animating-in-response-to-user-interaction-vb"></a><span data-ttu-id="f8e5e-104">사용자 상호 작용 (VB)에 대 한 응답으로 애니메이션 적용</span><span class="sxs-lookup"><span data-stu-id="f8e5e-104">Animating in Response To User Interaction (VB)</span></span>
====================
<span data-ttu-id="f8e5e-105">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="f8e5e-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f8e5e-106">[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="f8e5e-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6VB.pdf)</span></span>

> <span data-ttu-id="f8e5e-107">ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="f8e5e-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="f8e5e-108">애니메이션 자동으로 시작할 수 있습니다이 트리거될 수도 있고 사용자 인터페이스에 의해 예: 마우스로 클릭 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8e5e-108">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>


## <a name="overview"></a><span data-ttu-id="f8e5e-109">개요</span><span class="sxs-lookup"><span data-stu-id="f8e5e-109">Overview</span></span>

<span data-ttu-id="f8e5e-110">ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="f8e5e-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="f8e5e-111">애니메이션 자동으로 시작할 수 있습니다이 트리거될 수도 있고 사용자 인터페이스에 의해 예: 마우스로 클릭 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8e5e-111">The animations can start automatically or may be triggered by user interaction, e.g. by clicking with the mouse.</span></span>

## <a name="steps"></a><span data-ttu-id="f8e5e-112">단계</span><span class="sxs-lookup"><span data-stu-id="f8e5e-112">Steps</span></span>

<span data-ttu-id="f8e5e-113">우선, 포함 된 `ScriptManager` 페이지; 그런 다음 ASP.NET AJAX 라이브러리 로드 되는 제어 도구 키트를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="f8e5e-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample1.aspx)]

<span data-ttu-id="f8e5e-114">그러면 다음과 같은 텍스트의 패널에 애니메이션 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8e5e-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample2.aspx)]

<span data-ttu-id="f8e5e-115">패널에 대 한 연결 된 CSS 클래스 좋은 배경색을 정의 하 고도 패널 고정된 폭을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8e5e-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animating-in-response-to-user-interaction-vb/samples/sample3.css)]

<span data-ttu-id="f8e5e-116">그런 다음 추가 `AnimationExtender` 페이지에 제공 하는 `ID`, `TargetControlID` 특성과 반드시 `runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="f8e5e-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample4.aspx)]

<span data-ttu-id="f8e5e-117">내에서 `<Animations>` 노드를 5 가지 방법으로 사용자 상호 작용을 통해 애니메이션을 시작 하려면 (누락 된 요소는 `<OnLoad>` 전체 페이지가 완전히 로드 되 면 실행 되는):</span><span class="sxs-lookup"><span data-stu-id="f8e5e-117">Within the `<Animations>` node, there are five ways to start the animation via user interaction (the missing element is `<OnLoad>` which is executed once the whole page has been fully loaded):</span></span>

- <span data-ttu-id="f8e5e-118">`<OnClick>`(컨트롤에서 마우스 클릭)</span><span class="sxs-lookup"><span data-stu-id="f8e5e-118">`<OnClick>` (mouse click on the control)</span></span>
- <span data-ttu-id="f8e5e-119">`<OnHoverOut>`(마우스 컨트롤을 리프)</span><span class="sxs-lookup"><span data-stu-id="f8e5e-119">`<OnHoverOut>` (mouse leaves the control)</span></span>
- <span data-ttu-id="f8e5e-120">`<OnHoverOver>`(중지 하는 컨트롤을 마우스로 `<OnHoverOut>` 애니메이션)</span><span class="sxs-lookup"><span data-stu-id="f8e5e-120">`<OnHoverOver>` (mouse hovers over a control, stopping the `<OnHoverOut>` animation)</span></span>
- <span data-ttu-id="f8e5e-121">`<OnMouseOut>`(마우스가 컨트롤)</span><span class="sxs-lookup"><span data-stu-id="f8e5e-121">`<OnMouseOut>` (mouse leaves a control)</span></span>
- <span data-ttu-id="f8e5e-122">`<OnMouseOver>`(중지 되지 컨트롤을 마우스로 `<OnMouseOut>` 애니메이션)</span><span class="sxs-lookup"><span data-stu-id="f8e5e-122">`<OnMouseOver>` (mouse hovers over a control, not stopping the `<OnMouseOut>` animation)</span></span>

<span data-ttu-id="f8e5e-123">이 시나리오에서는 `<OnClick>` 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8e5e-123">In this scenario, `<OnClick>` is used.</span></span> <span data-ttu-id="f8e5e-124">패널에 사용자가 크기를 조정 하 고 동시에 페이드 아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8e5e-124">When the user clicks on the panel, it is resized and fades out at the same time.</span></span>

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample5.aspx)]


<span data-ttu-id="f8e5e-125">[![마우스 클릭 컨트롤은 애니메이션 시작](animating-in-response-to-user-interaction-vb/_static/image2.png)](animating-in-response-to-user-interaction-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f8e5e-125">[![A mouse click starts the animation](animating-in-response-to-user-interaction-vb/_static/image2.png)](animating-in-response-to-user-interaction-vb/_static/image1.png)</span></span>

<span data-ttu-id="f8e5e-126">마우스 클릭 컨트롤은 애니메이션 시작 ([전체 크기 이미지를 보려면 클릭](animating-in-response-to-user-interaction-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="f8e5e-126">A mouse click starts the animation ([Click to view full-size image](animating-in-response-to-user-interaction-vb/_static/image3.png))</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="f8e5e-127">[이전](picking-one-animation-out-of-a-list-vb.md)
[다음](disabling-actions-during-animation-vb.md)</span><span class="sxs-lookup"><span data-stu-id="f8e5e-127">[Previous](picking-one-animation-out-of-a-list-vb.md)
[Next](disabling-actions-during-animation-vb.md)</span></span>
