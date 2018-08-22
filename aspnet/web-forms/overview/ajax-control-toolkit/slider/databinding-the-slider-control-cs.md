---
uid: web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-cs
title: 데이터 바인딩 슬라이더 컨트롤 (C#) | Microsoft Docs
author: wenz
description: AJAX Control Toolkit의 슬라이더 컨트롤에 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다. 현재 positio 바인딩하는 것이 불가능 하는 중...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b7f77869-aa1d-4025-924f-622c57112db6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 951a7484f0dbb14ee7f1e1d62c9666e5cc49e7c1
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41823793"
---
<a name="databinding-the-slider-control-c"></a><span data-ttu-id="88dcd-104">데이터 바인딩 슬라이더 컨트롤 (C#)</span><span class="sxs-lookup"><span data-stu-id="88dcd-104">Databinding the Slider Control (C#)</span></span>
====================
<span data-ttu-id="88dcd-105">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="88dcd-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="88dcd-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="88dcd-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0CS.pdf)</span></span>

> <span data-ttu-id="88dcd-107">AJAX Control Toolkit의 슬라이더 컨트롤에 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="88dcd-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="88dcd-108">다른 ASP.NET 컨트롤에 슬라이더의 현재 위치를 바인딩하는 것이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="88dcd-108">It is possible to bind the current position of the slider to another ASP.NET control.</span></span>


## <a name="overview"></a><span data-ttu-id="88dcd-109">개요</span><span class="sxs-lookup"><span data-stu-id="88dcd-109">Overview</span></span>

<span data-ttu-id="88dcd-110">AJAX Control Toolkit의 슬라이더 컨트롤에 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="88dcd-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="88dcd-111">다른 ASP.NET 컨트롤에 슬라이더의 현재 위치를 바인딩하는 것이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="88dcd-111">It is possible to bind the current position of the slider to another ASP.NET control.</span></span>

## <a name="steps"></a><span data-ttu-id="88dcd-112">단계</span><span class="sxs-lookup"><span data-stu-id="88dcd-112">Steps</span></span>

<span data-ttu-id="88dcd-113">ASP.NET AJAX와 Control Toolkit의 기능을 활성화 하기 위해 합니다 `ScriptManager` 컨트롤 페이지의 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):</span><span class="sxs-lookup"><span data-stu-id="88dcd-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample1.aspx)]

<span data-ttu-id="88dcd-114">다음으로 두 개의 추가 `TextBox` 페이지로 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="88dcd-114">Next, add two `TextBox` controls to the page.</span></span> <span data-ttu-id="88dcd-115">하나는 그래픽 슬라이더도 변환 됩니다 및 다른 슬라이더의 위치에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88dcd-115">One will be transformed into a graphical slider, and the other one will hold the position of the slider.</span></span>

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample2.aspx)]

<span data-ttu-id="88dcd-116">다음 단계는 이미 마지막 단계가입니다.</span><span class="sxs-lookup"><span data-stu-id="88dcd-116">The next step is already the final step.</span></span> <span data-ttu-id="88dcd-117">`SliderExtender` ASP.NET AJAX Control Toolkit에서 첫 번째 텍스트 상자에서 슬라이더를 사용 하면 컨트롤과 슬라이더 위치를 변경 하는 경우 두 번째 텍스트 상자를 자동으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="88dcd-117">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit makes a slider out of the first text box and automatically updates the second text box when the slider position changes.</span></span> <span data-ttu-id="88dcd-118">작업을 위해서는 순서로 합니다 `SliderExtender`의 `TargetControlID` 첫 번째 텍스트 상자의 id 특성을 설정 해야 합니다는 `BoundControlID` 특성의 두 번째 텍스트 상자 ID로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="88dcd-118">In order for that to work, The `SliderExtender`'s `TargetControlID` attribute must be set to the ID of the first text box; the `BoundControlID` attribute must be set to the ID of the second text box.</span></span>

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample3.aspx)]

<span data-ttu-id="88dcd-119">양방향에서 데이터 바인딩이 작동 브라우저에서 보듯이: 슬라이더의 위치를 업데이트 하 고 텍스트 상자에 새 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="88dcd-119">As you can see in the browser, the data binding works in both directions: entering a new value in the text box updates the slider's position.</span></span> <span data-ttu-id="88dcd-120">읽기 전용 두 번째 텍스트 상자를 설정 하면 여기에 값을 수동으로 업데이트 하려면 사용자에 대 한 어렵습니다 있도록 텍스트 필드에 약한 보호를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88dcd-120">If you make the second text box read only, you may add a weak protection to the text field so that it is harder for the user to manually update the value in there.</span></span>


<span data-ttu-id="88dcd-121">[![슬라이더 및 텍스트 상자에 동기화 됩니다.](databinding-the-slider-control-cs/_static/image2.png)](databinding-the-slider-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="88dcd-121">[![Slider and text box are in sync](databinding-the-slider-control-cs/_static/image2.png)](databinding-the-slider-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="88dcd-122">슬라이더 및 텍스트 상자에 동기화 됩니다 ([클릭 하 여 큰 이미지 보기](databinding-the-slider-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="88dcd-122">Slider and text box are in sync ([Click to view full-size image](databinding-the-slider-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="88dcd-123">[이전](using-the-slider-control-with-auto-postback-cs.md)
> [다음](using-the-slider-control-with-auto-postback-vb.md)</span><span class="sxs-lookup"><span data-stu-id="88dcd-123">[Previous](using-the-slider-control-with-auto-postback-cs.md)
[Next](using-the-slider-control-with-auto-postback-vb.md)</span></span>
