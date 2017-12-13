---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
title: "애니메이션 UpdatePanel 컨트롤 (VB) | Microsoft Docs"
author: wenz
description: "ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 내용에는 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 4c306a2c-92b6-4904-b70b-365b847334fe
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 0d1056fc798e22254e94e5cad54436576a297f7d
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="animating-an-updatepanel-control-vb"></a><span data-ttu-id="dc764-104">UpdatePanel 컨트롤 (VB) 애니메이션 적용</span><span class="sxs-lookup"><span data-stu-id="dc764-104">Animating an UpdatePanel Control (VB)</span></span>
====================
<span data-ttu-id="dc764-105">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="dc764-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="dc764-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="dc764-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1VB.pdf)</span></span>

> <span data-ttu-id="dc764-107">ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="dc764-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="dc764-108">특별 한 extender 존재 애니메이션 프레임 워크에 크게 의존 하는 UpdatePanel의 내용에 대해: UpdatePanelAnimation 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc764-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="dc764-109">이 자습서는 UpdatePanel에 대 한 이러한 애니메이션을 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dc764-109">This tutorial shows how to set up such an animation for an UpdatePanel.</span></span>


## <a name="overview"></a><span data-ttu-id="dc764-110">개요</span><span class="sxs-lookup"><span data-stu-id="dc764-110">Overview</span></span>

<span data-ttu-id="dc764-111">ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="dc764-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="dc764-112">내용에는 `UpdatePanel`, 애니메이션 프레임 워크에 크게 의존 하는 특별 한 extender 존재: `UpdatePanelAnimation`합니다.</span><span class="sxs-lookup"><span data-stu-id="dc764-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="dc764-113">에 대 한 애니메이션을 설정 하는 방법을 보여 주는이 자습서는 `UpdatePanel`합니다.</span><span class="sxs-lookup"><span data-stu-id="dc764-113">This tutorial shows how to set up such an animation for an `UpdatePanel`.</span></span>

## <a name="steps"></a><span data-ttu-id="dc764-114">단계</span><span class="sxs-lookup"><span data-stu-id="dc764-114">Steps</span></span>

<span data-ttu-id="dc764-115">첫 번째 단계는 일반적으로 포함는 `ScriptManager` 페이지에 있도록 ASP.NET AJAX 라이브러리를 로드 하 고 제어 도구 키트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc764-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample1.aspx)]

<span data-ttu-id="dc764-116">이 시나리오에서 애니메이션을 적용할 ASP.NET `Wizard` 웹 컨트롤에 있는 프로그램 `UpdatePanel`합니다.</span><span class="sxs-lookup"><span data-stu-id="dc764-116">The animation in this scenario will be applied to an ASP.NET `Wizard` web control residing in an `UpdatePanel`.</span></span> <span data-ttu-id="dc764-117">포스트백을 트리거할 충분 한 옵션을 제공 하는 임의의 3 단계:</span><span class="sxs-lookup"><span data-stu-id="dc764-117">Three (arbitrary) steps provide enough options to trigger postbacks:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample2.aspx)]

<span data-ttu-id="dc764-118">에 필요한 태그는 `UpdatePanelAnimationExtender` 컨트롤에 사용 되는 태그를 매우 비슷합니다는 `AnimationExtender`합니다.</span><span class="sxs-lookup"><span data-stu-id="dc764-118">The markup necessary for the `UpdatePanelAnimationExtender` control is quite similar to the markup used for the `AnimationExtender`.</span></span> <span data-ttu-id="dc764-119">에 `TargetControlID` 제공 특성은 `ID` 의 `UpdatePanel` ; 애니메이션 효과를 줄 내에서 `UpdatePanelAnimationExtender` 컨트롤은 `<Animations>` 요소 애니메이션에 대 한 XML 태그를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc764-119">In the `TargetControlID` attribute we provide the `ID` of the `UpdatePanel` to animate; within the `UpdatePanelAnimationExtender` control, the `<Animations>` element holds XML markup for the animation(s).</span></span> <span data-ttu-id="dc764-120">그러나 한 가지 차이가: 이벤트 및 이벤트 처리기의 용량은 제한 비해 `AnimationExtender`합니다.</span><span class="sxs-lookup"><span data-stu-id="dc764-120">However there is one difference: The amount of events and event handlers is limited in comparison to `AnimationExtender`.</span></span> <span data-ttu-id="dc764-121">에 대 한 `UpdatePanels`두 개의 그중에서 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc764-121">For `UpdatePanels`, only two of them exist:</span></span>

- <span data-ttu-id="dc764-122">`<OnUpdated>`UpdatePanel이 업데이트 된 경우</span><span class="sxs-lookup"><span data-stu-id="dc764-122">`<OnUpdated>` when the UpdatePanel has been updated</span></span>
- <span data-ttu-id="dc764-123">`<OnUpdating>`UpdatePanel을 업데이트를 시작할 때</span><span class="sxs-lookup"><span data-stu-id="dc764-123">`<OnUpdating>` when the UpdatePanel starts updating</span></span>

<span data-ttu-id="dc764-124">이 시나리오에서는의 새 내용은 `UpdatePanel` (이후 포스트백)은 페이드 인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc764-124">In this scenario, the new content of the `UpdatePanel` (after the postback) shall fade in.</span></span> <span data-ttu-id="dc764-125">다음은 해당 하는 데 필요한 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="dc764-125">This is the necessary markup for that:</span></span>

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample3.aspx)]

<span data-ttu-id="dc764-126">이제 UpdatePanel 내 포스트백이 발생할 때마다 패널의 새 내용이 페이드 인 원활 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc764-126">Now whenever a postback occurs within the UpdatePanel, the new contents of the panel fade in smoothly.</span></span>


<span data-ttu-id="dc764-127">[![다음 마법사 단계 페이딩는](animating-an-updatepanel-control-vb/_static/image2.png)](animating-an-updatepanel-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="dc764-127">[![The next wizard step is fading in](animating-an-updatepanel-control-vb/_static/image2.png)](animating-an-updatepanel-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="dc764-128">다음 마법사 단계 페이딩 됩니다 ([전체 크기 이미지를 보려면 클릭](animating-an-updatepanel-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="dc764-128">The next wizard step is fading in ([Click to view full-size image](animating-an-updatepanel-control-vb/_static/image3.png))</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="dc764-129">[이전](changing-an-animation-using-client-side-code-vb.md)
[다음](dynamically-controlling-updatepanel-animations-vb.md)</span><span class="sxs-lookup"><span data-stu-id="dc764-129">[Previous](changing-an-animation-using-client-side-code-vb.md)
[Next](dynamically-controlling-updatepanel-animations-vb.md)</span></span>
