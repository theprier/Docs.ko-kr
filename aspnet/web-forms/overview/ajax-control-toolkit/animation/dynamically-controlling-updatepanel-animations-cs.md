---
uid: web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-cs
title: UpdatePanel 애니메이션 (C#)을 동적으로 제어 | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 내용에는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 5138b8fe-98ff-4e73-a00b-e263fc3ff11d
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/dynamically-controlling-updatepanel-animations-cs
msc.type: authoredcontent
ms.openlocfilehash: 78401ee35027040dffea50c295c752dd182e75a1
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="dynamically-controlling-updatepanel-animations-c"></a><span data-ttu-id="1c47c-104">UpdatePanel 애니메이션 동적으로 제어 (C#)</span><span class="sxs-lookup"><span data-stu-id="1c47c-104">Dynamically Controlling UpdatePanel Animations (C#)</span></span>
====================
<span data-ttu-id="1c47c-105">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="1c47c-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="1c47c-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="1c47c-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation2.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation2CS.pdf)</span></span>

> <span data-ttu-id="1c47c-107">ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="1c47c-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="1c47c-108">특별 한 extender 존재 애니메이션 프레임 워크에 크게 의존 하는 UpdatePanel의 내용에 대해: UpdatePanelAnimation 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c47c-108">For the contents of an UpdatePanel, a special extender exists that relies heavily on the animation framework: UpdatePanelAnimation.</span></span> <span data-ttu-id="1c47c-109">UpdatePanel 트리거와 함께 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c47c-109">It can also work together with UpdatePanel triggers.</span></span>


## <a name="overview"></a><span data-ttu-id="1c47c-110">개요</span><span class="sxs-lookup"><span data-stu-id="1c47c-110">Overview</span></span>

<span data-ttu-id="1c47c-111">ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="1c47c-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="1c47c-112">내용에는 `UpdatePanel`, 애니메이션 프레임 워크에 크게 의존 하는 특별 한 extender 존재: `UpdatePanelAnimation`합니다.</span><span class="sxs-lookup"><span data-stu-id="1c47c-112">For the contents of an `UpdatePanel`, a special extender exists that relies heavily on the animation framework: `UpdatePanelAnimation`.</span></span> <span data-ttu-id="1c47c-113">와 함께 확대할 수 `UpdatePanel` 트리거.</span><span class="sxs-lookup"><span data-stu-id="1c47c-113">It can also work together with `UpdatePanel` triggers.</span></span>

## <a name="steps"></a><span data-ttu-id="1c47c-114">단계</span><span class="sxs-lookup"><span data-stu-id="1c47c-114">Steps</span></span>

<span data-ttu-id="1c47c-115">첫 번째 단계는 일반적으로 포함는 `ScriptManager` 페이지에 있도록 ASP.NET AJAX 라이브러리를 로드 하 고 제어 도구 키트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c47c-115">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample1.aspx)]

<span data-ttu-id="1c47c-116">이 시나리오에서 애니메이션의 현재 시간 표시를에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c47c-116">The animation in this scenario will be applied to a display of the current time.</span></span> <span data-ttu-id="1c47c-117">이 정보를 사용 하 여 레이블의에 쓸 수는 `Page_Load()` 메서드를 다음 인라인 코드를 사용 (편의상) 또는:</span><span class="sxs-lookup"><span data-stu-id="1c47c-117">This information can be written into a label using the `Page_Load()` method, or (for the sake of simplicity) the following inline code is used:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample2.aspx)]

<span data-ttu-id="1c47c-118">또한 시간을 업데이트할 트리거하는 단추를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1c47c-118">Also, a button to trigger updating the time is created:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample3.aspx)]

<span data-ttu-id="1c47c-119">이 코드는 다음에 배치 된 `<ContentTemplate>` 의 섹션은 `UpdatePanel` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="1c47c-119">This code is then put into the `<ContentTemplate>` section of an `UpdatePanel` element.</span></span> <span data-ttu-id="1c47c-120">패널의 `UpdateMode` 특성으로 설정 되어 있어야 `"Conditional"`이므로 트리거만 패널의 콘텐츠를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c47c-120">The panel's `UpdateMode` attribute must be set to `"Conditional"`, since only triggers may update the panel's contents.</span></span> <span data-ttu-id="1c47c-121">에 `<Triggers>` 의 섹션에서 `UpdatePanel`, 비동기 포스트백 트리거는 생성 되 고 변수에 연결는 `Click` 단추의 이벤트가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c47c-121">In the `<Triggers>` section of the `UpdatePanel`, an asynchronous postback trigger is created and tied to the `Click` event of the button.</span></span> <span data-ttu-id="1c47c-122">따라서 사용자가 단추를 클릭할 경우의 `UpdatePanel` 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="1c47c-122">Thus, if the user clicks on the button, the `UpdatePanel` is refreshed.</span></span> <span data-ttu-id="1c47c-123">다음은 대 한 태그는 `UpdatePanel` 제어:</span><span class="sxs-lookup"><span data-stu-id="1c47c-123">Here is the markup for the `UpdatePanel` control:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample4.aspx)]

<span data-ttu-id="1c47c-124">마지막으로 `UpdatePanelAnimationExtender` 구성 해야 합니다: 설정의 `TargetControlID` 패널의 ID에 특성을 extender 내에서 애니메이션을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c47c-124">Finally, the `UpdatePanelAnimationExtender` must be configured: Set the `TargetControlID` attribute to the ID of the panel, and define an animation within the extender.</span></span> <span data-ttu-id="1c47c-125">에서 페이딩 의미는 멋진 시각적에 중점을 둔 업데이트 시간을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1c47c-125">Fading in makes sense, which creates a nice visual emphasis on the updated time.</span></span> <span data-ttu-id="1c47c-126">Extender 태그 수 다음 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c47c-126">Your extender markup may then look like this:</span></span>


[!code-aspx[Main](dynamically-controlling-updatepanel-animations-cs/samples/sample5.aspx)]

<span data-ttu-id="1c47c-127">브라우저에서 파일을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c47c-127">Run the file in the browser.</span></span> <span data-ttu-id="1c47c-128">단추를 클릭할 때마다 현재 시간을 항상 1 초 동안 페이딩 패널에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c47c-128">Whenever you click on the button, the current time is shown in the panel, always fading in for the duration of one second.</span></span>


<span data-ttu-id="1c47c-129">[![현재 시간 페이딩 됩니다.](dynamically-controlling-updatepanel-animations-cs/_static/image2.png)](dynamically-controlling-updatepanel-animations-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1c47c-129">[![The current time is fading in](dynamically-controlling-updatepanel-animations-cs/_static/image2.png)](dynamically-controlling-updatepanel-animations-cs/_static/image1.png)</span></span>

<span data-ttu-id="1c47c-130">현재 시간 페이딩 됩니다 ([전체 크기 이미지를 보려면 클릭](dynamically-controlling-updatepanel-animations-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="1c47c-130">The current time is fading in ([Click to view full-size image](dynamically-controlling-updatepanel-animations-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1c47c-131">[이전](animating-an-updatepanel-control-cs.md)
> [다음](adding-animation-to-a-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="1c47c-131">[Previous](animating-an-updatepanel-control-cs.md)
[Next](adding-animation-to-a-control-vb.md)</span></span>
