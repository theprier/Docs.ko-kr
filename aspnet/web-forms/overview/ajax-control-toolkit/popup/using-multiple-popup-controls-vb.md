---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
title: 여러 팝업 컨트롤 (VB)를 사용 하 여 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit의 PopupControl extender는 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수를 제공 합니다. M을 사용 하는 것도 가능...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4da43d77-f6c4-43a8-9124-f1e8e1c8f0a2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 81b0dbd794d31bc3c55bff4ba8110c590b88b509
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41828208"
---
<a name="using-multiple-popup-controls-vb"></a><span data-ttu-id="397d3-104">여러 팝업 컨트롤 (VB)를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="397d3-104">Using Multiple Popup Controls (VB)</span></span>
====================
<span data-ttu-id="397d3-105">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="397d3-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="397d3-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="397d3-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1VB.pdf)</span></span>

> <span data-ttu-id="397d3-107">AJAX Control Toolkit의 PopupControl extender는 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="397d3-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="397d3-108">도 한 페이지에 둘 이상의 팝업 컨트롤을 사용 하는 것이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="397d3-108">It is also possible to use more than one popup control on one page.</span></span>


## <a name="overview"></a><span data-ttu-id="397d3-109">개요</span><span class="sxs-lookup"><span data-stu-id="397d3-109">Overview</span></span>

<span data-ttu-id="397d3-110">AJAX Control Toolkit의 PopupControl extender는 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="397d3-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="397d3-111">도 한 페이지에 둘 이상의 팝업 컨트롤을 사용 하는 것이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="397d3-111">It is also possible to use more than one popup control on one page.</span></span>

## <a name="steps"></a><span data-ttu-id="397d3-112">단계</span><span class="sxs-lookup"><span data-stu-id="397d3-112">Steps</span></span>

<span data-ttu-id="397d3-113">ASP.NET AJAX와 Control Toolkit의 기능을 활성화 하기 위해 합니다 `ScriptManager` 컨트롤 페이지의 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):</span><span class="sxs-lookup"><span data-stu-id="397d3-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample1.aspx)]

<span data-ttu-id="397d3-114">다음으로, 팝업으로 사용 되는 패널을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="397d3-114">Next, add a panel which serves as the popup.</span></span> <span data-ttu-id="397d3-115">패널에 현재 시나리오에는 `Calendar` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="397d3-115">In the current scenario, the panel contains a `Calendar` control.</span></span> <span data-ttu-id="397d3-116">달력의 포스트백에서 발생 한 페이지 새로 고침을 피하기 위해 패널 내에서 것을 `UpdatePanel` 제어:</span><span class="sxs-lookup"><span data-stu-id="397d3-116">In order to avoid the page refreshes caused by the Calendar's postbacks, the panel is put within an `UpdatePanel` control:</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample2.aspx)]

<span data-ttu-id="397d3-117">페이지에는 두 개의 텍스트 상자가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="397d3-117">The page also contains two text boxes.</span></span> <span data-ttu-id="397d3-118">각 텍스트 상자에 텍스트 상자가 활성화 되 면 달력 팝업을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="397d3-118">For each text box, the calendar popup shall appear once the text box is activated.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample3.aspx)]

<span data-ttu-id="397d3-119">이제 각 사용 하 여 두 텍스트 상자를 확장 하는 `PopupControlExtender`합니다.</span><span class="sxs-lookup"><span data-stu-id="397d3-119">Now extend each of the two text boxes with a `PopupControlExtender`.</span></span> <span data-ttu-id="397d3-120">`TargetControlID` 특성 extender에 연결 된 컨트롤의 ID를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="397d3-120">The `TargetControlID` attribute provides the ID of the control tied to the extender.</span></span> <span data-ttu-id="397d3-121">`PopupControlID` 특성 팝업 패널의 ID를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="397d3-121">The `PopupControlID` attribute contains the ID of the popup panel.</span></span> <span data-ttu-id="397d3-122">이 경우 모두 extender는 같은 패널을 표시 하지만 다른 패널도 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="397d3-122">In this case, both extenders show the same panel, but different panels are possible, as well.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample4.aspx)]

<span data-ttu-id="397d3-123">이제 텍스트 필드 내에서 클릭할 때마다 일정 필드 아래에 표시에서 날짜를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="397d3-123">Now whenever you click within a text field, a calendar appears below the field, allowing you to select a date.</span></span> <span data-ttu-id="397d3-124">(텍스트 상자에 선택한 날짜를 다시 시작에서 다룰 다양 한 자습서입니다.)</span><span class="sxs-lookup"><span data-stu-id="397d3-124">(Getting the selected date back into the text boxes will be covered in a different tutorial.)</span></span>


<span data-ttu-id="397d3-125">[![텍스트 상자에 사용자가 클릭 하면 달력이 나타납니다.](using-multiple-popup-controls-vb/_static/image2.png)](using-multiple-popup-controls-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="397d3-125">[![The Calendar appears when the user clicks into the textbox](using-multiple-popup-controls-vb/_static/image2.png)](using-multiple-popup-controls-vb/_static/image1.png)</span></span>

<span data-ttu-id="397d3-126">텍스트 상자에 사용자가 클릭 하면 달력이 나타납니다 ([클릭 하 여 큰 이미지 보기](using-multiple-popup-controls-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="397d3-126">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](using-multiple-popup-controls-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="397d3-127">[이전](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
> [다음](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)</span><span class="sxs-lookup"><span data-stu-id="397d3-127">[Previous](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
[Next](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)</span></span>
