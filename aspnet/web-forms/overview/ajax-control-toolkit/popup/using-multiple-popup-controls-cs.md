---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
title: 여러 팝업 컨트롤 (C#)를 사용 하 여 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit의 PopupControl extender는 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수를 제공 합니다. M을 사용 하는 것도 가능...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: 91511b0b-311d-481f-9e7c-73f07b813b79
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: 681ee1433130ef1cf6d1521497001215a1bfbb66
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37814742"
---
<a name="using-multiple-popup-controls-c"></a><span data-ttu-id="00a55-104">여러 팝업 컨트롤 (C#)를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="00a55-104">Using Multiple Popup Controls (C#)</span></span>
====================
<span data-ttu-id="00a55-105">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="00a55-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="00a55-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="00a55-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1CS.pdf)</span></span>

> <span data-ttu-id="00a55-107">AJAX Control Toolkit의 PopupControl extender는 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a55-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="00a55-108">도 한 페이지에 둘 이상의 팝업 컨트롤을 사용 하는 것이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a55-108">It is also possible to use more than one popup control on one page.</span></span>


## <a name="overview"></a><span data-ttu-id="00a55-109">개요</span><span class="sxs-lookup"><span data-stu-id="00a55-109">Overview</span></span>

<span data-ttu-id="00a55-110">AJAX Control Toolkit의 PopupControl extender는 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a55-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="00a55-111">도 한 페이지에 둘 이상의 팝업 컨트롤을 사용 하는 것이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a55-111">It is also possible to use more than one popup control on one page.</span></span>

## <a name="steps"></a><span data-ttu-id="00a55-112">단계</span><span class="sxs-lookup"><span data-stu-id="00a55-112">Steps</span></span>

<span data-ttu-id="00a55-113">ASP.NET AJAX와 Control Toolkit의 기능을 활성화 하기 위해 합니다 `ScriptManager` 컨트롤 페이지의 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):</span><span class="sxs-lookup"><span data-stu-id="00a55-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample1.aspx)]

<span data-ttu-id="00a55-114">다음으로, 팝업으로 사용 되는 패널을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a55-114">Next, add a panel which serves as the popup.</span></span> <span data-ttu-id="00a55-115">패널에 현재 시나리오에는 `Calendar` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a55-115">In the current scenario, the panel contains a `Calendar` control.</span></span> <span data-ttu-id="00a55-116">달력의 포스트백에서 발생 한 페이지 새로 고침을 피하기 위해 패널 내에서 것을 `UpdatePanel` 제어:</span><span class="sxs-lookup"><span data-stu-id="00a55-116">In order to avoid the page refreshes caused by the Calendar's postbacks, the panel is put within an `UpdatePanel` control:</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample2.aspx)]

<span data-ttu-id="00a55-117">페이지에는 두 개의 텍스트 상자가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a55-117">The page also contains two text boxes.</span></span> <span data-ttu-id="00a55-118">각 텍스트 상자에 텍스트 상자가 활성화 되 면 달력 팝업을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a55-118">For each text box, the calendar popup shall appear once the text box is activated.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample3.aspx)]

<span data-ttu-id="00a55-119">이제 각 사용 하 여 두 텍스트 상자를 확장 하는 `PopupControlExtender`합니다.</span><span class="sxs-lookup"><span data-stu-id="00a55-119">Now extend each of the two text boxes with a `PopupControlExtender`.</span></span> <span data-ttu-id="00a55-120">`TargetControlID` 특성 extender에 연결 된 컨트롤의 ID를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a55-120">The `TargetControlID` attribute provides the ID of the control tied to the extender.</span></span> <span data-ttu-id="00a55-121">`PopupControlID` 특성 팝업 패널의 ID를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a55-121">The `PopupControlID` attribute contains the ID of the popup panel.</span></span> <span data-ttu-id="00a55-122">이 경우 모두 extender는 같은 패널을 표시 하지만 다른 패널도 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a55-122">In this case, both extenders show the same panel, but different panels are possible, as well.</span></span>

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample4.aspx)]

<span data-ttu-id="00a55-123">이제 텍스트 필드 내에서 클릭할 때마다 일정 필드 아래에 표시에서 날짜를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a55-123">Now whenever you click within a text field, a calendar appears below the field, allowing you to select a date.</span></span> <span data-ttu-id="00a55-124">(텍스트 상자에 선택한 날짜를 다시 시작에서 다룰 다양 한 자습서입니다.)</span><span class="sxs-lookup"><span data-stu-id="00a55-124">(Getting the selected date back into the text boxes will be covered in a different tutorial.)</span></span>


<span data-ttu-id="00a55-125">[![텍스트 상자에 사용자가 클릭 하면 달력이 나타납니다.](using-multiple-popup-controls-cs/_static/image2.png)](using-multiple-popup-controls-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="00a55-125">[![The Calendar appears when the user clicks into the textbox](using-multiple-popup-controls-cs/_static/image2.png)](using-multiple-popup-controls-cs/_static/image1.png)</span></span>

<span data-ttu-id="00a55-126">텍스트 상자에 사용자가 클릭 하면 달력이 나타납니다 ([클릭 하 여 큰 이미지 보기](using-multiple-popup-controls-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="00a55-126">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](using-multiple-popup-controls-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="00a55-127">다음</span><span class="sxs-lookup"><span data-stu-id="00a55-127">Next</span></span>](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
