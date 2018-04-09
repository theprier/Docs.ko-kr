---
uid: web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-cs
title: 데이터 바인딩 슬라이더 컨트롤 (C#) | Microsoft Docs
author: wenz
description: 슬라이더 컨트롤 들어에서 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다. 현재 positio 바인딩할 수는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: b7f77869-aa1d-4025-924f-622c57112db6
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 7644c991cd88868235511ba372be1f5b47c68fea
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="databinding-the-slider-control-c"></a><span data-ttu-id="1f41a-104">데이터 바인딩 슬라이더 컨트롤 (C#)</span><span class="sxs-lookup"><span data-stu-id="1f41a-104">Databinding the Slider Control (C#)</span></span>
====================
<span data-ttu-id="1f41a-105">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="1f41a-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="1f41a-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="1f41a-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0CS.pdf)</span></span>

> <span data-ttu-id="1f41a-107">슬라이더 컨트롤 들어에서 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f41a-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="1f41a-108">슬라이더의 현재 위치를 다른 ASP.NET 컨트롤 바인딩할 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1f41a-108">It is possible to bind the current position of the slider to another ASP.NET control.</span></span>


## <a name="overview"></a><span data-ttu-id="1f41a-109">개요</span><span class="sxs-lookup"><span data-stu-id="1f41a-109">Overview</span></span>

<span data-ttu-id="1f41a-110">슬라이더 컨트롤 들어에서 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f41a-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="1f41a-111">슬라이더의 현재 위치를 다른 ASP.NET 컨트롤 바인딩할 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1f41a-111">It is possible to bind the current position of the slider to another ASP.NET control.</span></span>

## <a name="steps"></a><span data-ttu-id="1f41a-112">단계</span><span class="sxs-lookup"><span data-stu-id="1f41a-112">Steps</span></span>

<span data-ttu-id="1f41a-113">ASP.NET AJAX 및 제어 Toolkit의 기능을 활성화 하는 데는 `ScriptManager` 제어 페이지에서 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):</span><span class="sxs-lookup"><span data-stu-id="1f41a-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample1.aspx)]

<span data-ttu-id="1f41a-114">다음으로, 두 개의 추가 `TextBox` 페이지 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="1f41a-114">Next, add two `TextBox` controls to the page.</span></span> <span data-ttu-id="1f41a-115">그래픽 슬라이더도 변환 됨 하나 길게 다른 하나는 슬라이더의 위치.</span><span class="sxs-lookup"><span data-stu-id="1f41a-115">One will be transformed into a graphical slider, and the other one will hold the position of the slider.</span></span>

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample2.aspx)]

<span data-ttu-id="1f41a-116">다음 단계는 이미 마지막 단계가입니다.</span><span class="sxs-lookup"><span data-stu-id="1f41a-116">The next step is already the final step.</span></span> <span data-ttu-id="1f41a-117">`SliderExtender` ASP.NET AJAX 컨트롤 도구 키트에서 첫 번째 텍스트 상자에서 슬라이더를 사용 하면 컨트롤과 슬라이더 위치가 변경 될 때 두 번째 텍스트 상자를 자동으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f41a-117">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit makes a slider out of the first text box and automatically updates the second text box when the slider position changes.</span></span> <span data-ttu-id="1f41a-118">작업을 위해서는 되려면는 `SliderExtender`의 `TargetControlID` 특성의 첫 번째 텍스트 상자; ID로 설정 해야 합니다는 `BoundControlID` 특성을 두 번째 텍스트 상자의 ID로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f41a-118">In order for that to work, The `SliderExtender`'s `TargetControlID` attribute must be set to the ID of the first text box; the `BoundControlID` attribute must be set to the ID of the second text box.</span></span>

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample3.aspx)]

<span data-ttu-id="1f41a-119">데이터 바인딩은 양방향에서 작동 브라우저에 보시: 슬라이더의 위치를 업데이트 하 고 텍스트 상자에 새 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f41a-119">As you can see in the browser, the data binding works in both directions: entering a new value in the text box updates the slider's position.</span></span> <span data-ttu-id="1f41a-120">읽기 전용 두 번째 텍스트 상자를 설정 하 여 사용자가 수동으로 거기에 값을 업데이트 하는 것이 어렵다는 텍스트 필드에 암호 보호를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f41a-120">If you make the second text box read only, you may add a weak protection to the text field so that it is harder for the user to manually update the value in there.</span></span>


<span data-ttu-id="1f41a-121">[![동기화 되어 슬라이더와 텍스트 상자](databinding-the-slider-control-cs/_static/image2.png)](databinding-the-slider-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1f41a-121">[![Slider and text box are in sync](databinding-the-slider-control-cs/_static/image2.png)](databinding-the-slider-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="1f41a-122">슬라이더와 텍스트 상자에 동기화 되었는지 ([전체 크기 이미지를 보려면 클릭](databinding-the-slider-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="1f41a-122">Slider and text box are in sync ([Click to view full-size image](databinding-the-slider-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1f41a-123">[이전](using-the-slider-control-with-auto-postback-cs.md)
> [다음](using-the-slider-control-with-auto-postback-vb.md)</span><span class="sxs-lookup"><span data-stu-id="1f41a-123">[Previous](using-the-slider-control-with-auto-postback-cs.md)
[Next](using-the-slider-control-with-auto-postback-vb.md)</span></span>
