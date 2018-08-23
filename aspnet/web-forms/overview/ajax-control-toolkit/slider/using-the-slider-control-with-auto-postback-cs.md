---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
title: 슬라이더 컨트롤을 사용 하 여 포스트백 (C#) | Microsoft Docs
author: wenz
description: AJAX Control Toolkit의 슬라이더 컨트롤에 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다. 슬라이더 autopost를 확인 하는 것이 불가능 하는 중...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4d85e9fb-91e6-41f2-9c13-754549b19c27
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
msc.type: authoredcontent
ms.openlocfilehash: 4f776d609099c398b4937710487ba51a5efb1876
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41838225"
---
<a name="using-the-slider-control-with-auto-postback-c"></a><span data-ttu-id="b639e-104">슬라이더 컨트롤을 사용 하 여 포스트백 (C#)</span><span class="sxs-lookup"><span data-stu-id="b639e-104">Using the Slider Control With Auto-Postback (C#)</span></span>
====================
<span data-ttu-id="b639e-105">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="b639e-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="b639e-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="b639e-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)</span></span>

> <span data-ttu-id="b639e-107">AJAX Control Toolkit의 슬라이더 컨트롤에 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b639e-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="b639e-108">슬라이더 autopostback을 해당 값이 변경 되 면 확인 하는 것이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="b639e-108">It is possible to make the slider autopostback once its value changes.</span></span>


## <a name="overview"></a><span data-ttu-id="b639e-109">개요</span><span class="sxs-lookup"><span data-stu-id="b639e-109">Overview</span></span>

<span data-ttu-id="b639e-110">AJAX Control Toolkit의 슬라이더 컨트롤에 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b639e-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="b639e-111">슬라이더 autopostback을 해당 값이 변경 되 면 확인 하는 것이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="b639e-111">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="steps"></a><span data-ttu-id="b639e-112">단계</span><span class="sxs-lookup"><span data-stu-id="b639e-112">Steps</span></span>

<span data-ttu-id="b639e-113">슬라이더를 변경 하면 자동으로 다시 게시 하려면 두 텍스트 상자에 특성을 추가 해야 `AutoPostBack="true"`: 자체 슬라이더에 텍스트 상자 및 슬라이더의 위치를 보유 하는 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="b639e-113">In order to make the slider automatically postback upon a change, both text boxes need the attribute `AutoPostBack="true"`: The text box that will become the slider itself, and the text box that holds the slider's position.</span></span> <span data-ttu-id="b639e-114">에 대 한 필수 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b639e-114">Here is the required markup for that:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample1.aspx)]

<span data-ttu-id="b639e-115">`SliderExtender` ASP.NET AJAX Control Toolkit에서 컨트롤의 두 텍스트 상자에 슬라이더 기능을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b639e-115">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit assigns the slider functionality to the two text boxes:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample2.aspx)]

<span data-ttu-id="b639e-116">추가 레이블 요소 포스트백의 사용자에 게 알려 나중에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b639e-116">An additional label element will later be used to inform the user of a postback:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample3.aspx)]

<span data-ttu-id="b639e-117">마지막으로 `ScriptManager` ASP.NET AJAX의 컨트롤 컨트롤 도구 키트 작동 하려면 필요한 JavaScript를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b639e-117">Finally, the `ScriptManager` control of ASP.NET AJAX loads the required JavaScript for the Control Toolkit to work:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample4.aspx)]

<span data-ttu-id="b639e-118">이제 슬라이더는 포스트백; 서버 쪽에서이 이벤트 수 발견 되 고 취해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b639e-118">Now the slider is posting back; on the server-side, this event may be caught and acted upon:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample5.aspx)]


<span data-ttu-id="b639e-119">[![포스트백을 트리거하는 슬라이더를 이동 합니다.](using-the-slider-control-with-auto-postback-cs/_static/image2.png)](using-the-slider-control-with-auto-postback-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b639e-119">[![Moving the slider triggers a postback](using-the-slider-control-with-auto-postback-cs/_static/image2.png)](using-the-slider-control-with-auto-postback-cs/_static/image1.png)</span></span>

<span data-ttu-id="b639e-120">포스트백을 트리거하는 슬라이더를 이동 ([클릭 하 여 큰 이미지 보기](using-the-slider-control-with-auto-postback-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="b639e-120">Moving the slider triggers a postback ([Click to view full-size image](using-the-slider-control-with-auto-postback-cs/_static/image3.png))</span></span>


<span data-ttu-id="b639e-121">[![레이블을이 변경의 날짜 이후에 작성 된](using-the-slider-control-with-auto-postback-cs/_static/image5.png)](using-the-slider-control-with-auto-postback-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="b639e-121">[![Afterwards, the date of this change is written in the label](using-the-slider-control-with-auto-postback-cs/_static/image5.png)](using-the-slider-control-with-auto-postback-cs/_static/image4.png)</span></span>

<span data-ttu-id="b639e-122">그런 다음이 변경의 날짜 레이블을 작성 됩니다 ([클릭 하 여 큰 이미지 보기](using-the-slider-control-with-auto-postback-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="b639e-122">Afterwards, the date of this change is written in the label ([Click to view full-size image](using-the-slider-control-with-auto-postback-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="b639e-123">다음</span><span class="sxs-lookup"><span data-stu-id="b639e-123">Next</span></span>](databinding-the-slider-control-cs.md)
