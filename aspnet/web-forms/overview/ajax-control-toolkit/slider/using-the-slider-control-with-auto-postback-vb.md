---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
title: 슬라이더 컨트롤을 사용 하 여 자동 다시 게시 (VB)으로 | Microsoft Docs
author: wenz
description: 슬라이더 컨트롤 들어에서 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다. 슬라이더 autopost 확인 수는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 41d1abba-97a5-4a45-9b44-d05624c19777
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-vb
msc.type: authoredcontent
ms.openlocfilehash: edb8fa13716c3c0beb7cf86dd3843caaec939483
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30879274"
---
<a name="using-the-slider-control-with-auto-postback-vb"></a><span data-ttu-id="6d905-104">슬라이더 컨트롤을 사용 하 여 자동 다시 게시 (VB)으로</span><span class="sxs-lookup"><span data-stu-id="6d905-104">Using the Slider Control With Auto-Postback (VB)</span></span>
====================
<span data-ttu-id="6d905-105">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="6d905-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="6d905-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="6d905-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1VB.pdf)</span></span>

> <span data-ttu-id="6d905-107">슬라이더 컨트롤 들어에서 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d905-107">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="6d905-108">해당 값이 변경 슬라이더 autopostback를 한 번 확인 수는.</span><span class="sxs-lookup"><span data-stu-id="6d905-108">It is possible to make the slider autopostback once its value changes.</span></span>


## <a name="overview"></a><span data-ttu-id="6d905-109">개요</span><span class="sxs-lookup"><span data-stu-id="6d905-109">Overview</span></span>

<span data-ttu-id="6d905-110">슬라이더 컨트롤 들어에서 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d905-110">The Slider control in the AJAX Control Toolkit provides a graphical slider that can be controlled using the mouse.</span></span> <span data-ttu-id="6d905-111">해당 값이 변경 슬라이더 autopostback를 한 번 확인 수는.</span><span class="sxs-lookup"><span data-stu-id="6d905-111">It is possible to make the slider autopostback once its value changes.</span></span>

## <a name="steps"></a><span data-ttu-id="6d905-112">단계</span><span class="sxs-lookup"><span data-stu-id="6d905-112">Steps</span></span>

<span data-ttu-id="6d905-113">슬라이더를 변경 시 자동으로 다시 게시 하기 위해 두 텍스트 상자에 특성을 추가 해야 `AutoPostBack="true"`: 자체 슬라이더 될 텍스트 상자 및 슬라이더의 위치를 보유 하는 텍스트 상자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d905-113">In order to make the slider automatically postback upon a change, both text boxes need the attribute `AutoPostBack="true"`: The text box that will become the slider itself, and the text box that holds the slider's position.</span></span> <span data-ttu-id="6d905-114">필수 태그에는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6d905-114">Here is the required markup for that:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample1.aspx)]

<span data-ttu-id="6d905-115">`SliderExtender` ASP.NET AJAX 컨트롤 도구 키트에서 컨트롤의 두 텍스트 상자에 슬라이더 기능을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d905-115">The `SliderExtender` control from the ASP.NET AJAX Control Toolkit assigns the slider functionality to the two text boxes:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample2.aspx)]

<span data-ttu-id="6d905-116">추가 레이블 요소 나중에 다시 게시의 사용자에 게에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d905-116">An additional label element will later be used to inform the user of a postback:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample3.aspx)]

<span data-ttu-id="6d905-117">마지막으로 `ScriptManager` ASP.NET AJAX의 컨트롤에서 작동 하도록 제어 도구 키트에 대 한 필요한 JavaScript 로드:</span><span class="sxs-lookup"><span data-stu-id="6d905-117">Finally, the `ScriptManager` control of ASP.NET AJAX loads the required JavaScript for the Control Toolkit to work:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample4.aspx)]

<span data-ttu-id="6d905-118">슬라이더를 다시; 게시 이제 서버 쪽에서이 이벤트 발생 및 대상이 될 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="6d905-118">Now the slider is posting back; on the server-side, this event may be caught and acted upon:</span></span>

[!code-aspx[Main](using-the-slider-control-with-auto-postback-vb/samples/sample5.aspx)]


<span data-ttu-id="6d905-119">[![포스트백을 트리거합니다 슬라이더를 이동](using-the-slider-control-with-auto-postback-vb/_static/image2.png)](using-the-slider-control-with-auto-postback-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6d905-119">[![Moving the slider triggers a postback](using-the-slider-control-with-auto-postback-vb/_static/image2.png)](using-the-slider-control-with-auto-postback-vb/_static/image1.png)</span></span>

<span data-ttu-id="6d905-120">포스트백 트리거합니다 슬라이더를 이동 ([전체 크기 이미지를 보려면 클릭](using-the-slider-control-with-auto-postback-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="6d905-120">Moving the slider triggers a postback ([Click to view full-size image](using-the-slider-control-with-auto-postback-vb/_static/image3.png))</span></span>


<span data-ttu-id="6d905-121">[![이러한 변경의 날짜 레이블이 작성 된 이후에,](using-the-slider-control-with-auto-postback-vb/_static/image5.png)](using-the-slider-control-with-auto-postback-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="6d905-121">[![Afterwards, the date of this change is written in the label](using-the-slider-control-with-auto-postback-vb/_static/image5.png)](using-the-slider-control-with-auto-postback-vb/_static/image4.png)</span></span>

<span data-ttu-id="6d905-122">이러한 변경의 날짜 레이블을 작성 된 이후에 ([전체 크기 이미지를 보려면 클릭](using-the-slider-control-with-auto-postback-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="6d905-122">Afterwards, the date of this change is written in the label ([Click to view full-size image](using-the-slider-control-with-auto-postback-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6d905-123">[이전](databinding-the-slider-control-cs.md)
> [다음](databinding-the-slider-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="6d905-123">[Previous](databinding-the-slider-control-cs.md)
[Next](databinding-the-slider-control-vb.md)</span></span>
