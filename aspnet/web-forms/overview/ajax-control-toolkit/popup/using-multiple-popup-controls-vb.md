---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
title: 여러 개의 팝업 컨트롤이 (VB)를 사용 하 여 | Microsoft Docs
author: wenz
description: 에 들어 PopupControl extender 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수 있는 방법을 제공 합니다. M을 사용 하는 것도 가능 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 4da43d77-f6c4-43a8-9124-f1e8e1c8f0a2
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 7c57aab3ecf2c02a8488b5ea4e3e0ed33ac5e7fe
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="using-multiple-popup-controls-vb"></a><span data-ttu-id="e0e36-104">여러 개의 팝업 컨트롤이 (VB)를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e0e36-104">Using Multiple Popup Controls (VB)</span></span>
====================
<span data-ttu-id="e0e36-105">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="e0e36-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="e0e36-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="e0e36-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1VB.pdf)</span></span>

> <span data-ttu-id="e0e36-107">에 들어 PopupControl extender 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수 있는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e36-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="e0e36-108">도 한 페이지에 둘 이상의 popup 컨트롤을 사용 하는 것이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e36-108">It is also possible to use more than one popup control on one page.</span></span>


## <a name="overview"></a><span data-ttu-id="e0e36-109">개요</span><span class="sxs-lookup"><span data-stu-id="e0e36-109">Overview</span></span>

<span data-ttu-id="e0e36-110">에 들어 PopupControl extender 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수 있는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e36-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="e0e36-111">도 한 페이지에 둘 이상의 popup 컨트롤을 사용 하는 것이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e36-111">It is also possible to use more than one popup control on one page.</span></span>

## <a name="steps"></a><span data-ttu-id="e0e36-112">단계</span><span class="sxs-lookup"><span data-stu-id="e0e36-112">Steps</span></span>

<span data-ttu-id="e0e36-113">ASP.NET AJAX 및 제어 Toolkit의 기능을 활성화 하는 데는 `ScriptManager` 제어 페이지에서 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):</span><span class="sxs-lookup"><span data-stu-id="e0e36-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample1.aspx)]

<span data-ttu-id="e0e36-114">다음으로, 팝업으로 사용 되는 패널을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e36-114">Next, add a panel which serves as the popup.</span></span> <span data-ttu-id="e0e36-115">패널에 포함 된 현재 시나리오에는 `Calendar` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e36-115">In the current scenario, the panel contains a `Calendar` control.</span></span> <span data-ttu-id="e0e36-116">달력의 포스트백에서 발생 한 페이지 새로 고침을 방지 하기 위해 패널은 내에 배치 된 `UpdatePanel` 제어:</span><span class="sxs-lookup"><span data-stu-id="e0e36-116">In order to avoid the page refreshes caused by the Calendar's postbacks, the panel is put within an `UpdatePanel` control:</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample2.aspx)]

<span data-ttu-id="e0e36-117">또한이 페이지는 두 개의 텍스트 상자 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e36-117">The page also contains two text boxes.</span></span> <span data-ttu-id="e0e36-118">각 텍스트 상자에 텍스트 상자가 활성화 되 면 일정 팝업 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e36-118">For each text box, the calendar popup shall appear once the text box is activated.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample3.aspx)]

<span data-ttu-id="e0e36-119">이제 각와 두 개의 텍스트 상자를 확장 한 `PopupControlExtender`합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e36-119">Now extend each of the two text boxes with a `PopupControlExtender`.</span></span> <span data-ttu-id="e0e36-120">`TargetControlID` 특성은 extender에 연결 된 컨트롤의 ID를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e36-120">The `TargetControlID` attribute provides the ID of the control tied to the extender.</span></span> <span data-ttu-id="e0e36-121">`PopupControlID` 특성 팝업 패널의 ID를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e36-121">The `PopupControlID` attribute contains the ID of the popup panel.</span></span> <span data-ttu-id="e0e36-122">이 경우 두 extender 같은 패널 표시 되지만 다른 패널은도 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0e36-122">In this case, both extenders show the same panel, but different panels are possible, as well.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample4.aspx)]

<span data-ttu-id="e0e36-123">이제 텍스트 필드 내에서 클릭할 때마다 일정 필드 아래에 표시, 날짜를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0e36-123">Now whenever you click within a text field, a calendar appears below the field, allowing you to select a date.</span></span> <span data-ttu-id="e0e36-124">(텍스트 상자로 선택한 날짜를 다시 가져오는 다룰 예정 다른 자습서를 참조 합니다.)</span><span class="sxs-lookup"><span data-stu-id="e0e36-124">(Getting the selected date back into the text boxes will be covered in a different tutorial.)</span></span>


<span data-ttu-id="e0e36-125">[![입력란에 사용자가 클릭 하면 달력이 나타납니다.](using-multiple-popup-controls-vb/_static/image2.png)](using-multiple-popup-controls-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e0e36-125">[![The Calendar appears when the user clicks into the textbox](using-multiple-popup-controls-vb/_static/image2.png)](using-multiple-popup-controls-vb/_static/image1.png)</span></span>

<span data-ttu-id="e0e36-126">입력란에 사용자가 클릭 하면 달력이 나타납니다 ([전체 크기 이미지를 보려면 클릭](using-multiple-popup-controls-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="e0e36-126">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](using-multiple-popup-controls-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e0e36-127">[이전](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
> [다음](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)</span><span class="sxs-lookup"><span data-stu-id="e0e36-127">[Previous](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
[Next](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)</span></span>
