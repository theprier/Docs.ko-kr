---
uid: web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-cs
title: 축소 및 확장 (C#) JavaScript에서 패널 | Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit의 CollapsiblePanel 컨트롤 패널을 확장 하 고 해당 콘텐츠를 축소 하 고 확장 하는 기능을 사용 하 여 제공을 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: de5500be-75e5-461a-8064-b70ae52ea6a4
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-cs
msc.type: authoredcontent
ms.openlocfilehash: 85a9c6e6cc56cc563eefea6bc863950ba71149ba
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37402758"
---
<a name="collapsing-and-expanding-a-panel-from-javascript-c"></a><span data-ttu-id="d0f6c-103">확장 및 JavaScript (C#)에서 패널 축소</span><span class="sxs-lookup"><span data-stu-id="d0f6c-103">Collapsing and Expanding a Panel from JavaScript (C#)</span></span>
====================
<span data-ttu-id="d0f6c-104">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="d0f6c-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="d0f6c-105">[코드를 다운로드](http://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="d0f6c-105">[Download Code](http://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1CS.pdf)</span></span>

> <span data-ttu-id="d0f6c-106">ASP.NET AJAX Control Toolkit의 CollapsiblePanel 컨트롤 패널을 확장 하 고 해당 콘텐츠를 축소 하 고 다시 확장 하는 기능을 사용 하 여 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0f6c-106">The CollapsiblePanel control in the ASP.NET AJAX Control Toolkit extends a panel and provides it with the capability to collapse its contents and expand it again.</span></span> <span data-ttu-id="d0f6c-107">사용자 지정 JavaScript 코드에서 이러한 두 작업을 트리거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0f6c-107">These two actions can also be triggered from custom JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="d0f6c-108">개요</span><span class="sxs-lookup"><span data-stu-id="d0f6c-108">Overview</span></span>

<span data-ttu-id="d0f6c-109">ASP.NET AJAX Control Toolkit의 CollapsiblePanel 컨트롤 패널을 확장 하 고 해당 콘텐츠를 축소 하 고 다시 확장 하는 기능을 사용 하 여 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0f6c-109">The CollapsiblePanel control in the ASP.NET AJAX Control Toolkit extends a panel and provides it with the capability to collapse its contents and expand it again.</span></span> <span data-ttu-id="d0f6c-110">사용자 지정 JavaScript 코드에서 이러한 두 작업을 트리거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0f6c-110">These two actions can also be triggered from custom JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="d0f6c-111">단계</span><span class="sxs-lookup"><span data-stu-id="d0f6c-111">Steps</span></span>

<span data-ttu-id="d0f6c-112">먼저, 새 ASP.NET 페이지를 만들고 포함 된 `ScriptManager` 것 내 `<form>` 요소.</span><span class="sxs-lookup"><span data-stu-id="d0f6c-112">First of all, create a new ASP.NET page and include the `ScriptManager` within the one `<form>` element.</span></span> <span data-ttu-id="d0f6c-113">이 컨트롤 도구 키트에 필요한 ASP.NET AJAX 라이브러리를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0f6c-113">This loads the ASP.NET AJAX library which is required by the Control Toolkit:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample1.aspx)]

<span data-ttu-id="d0f6c-114">그런 다음 확장/축소 효과 볼 수 있도록 일부 텍스트를 사용 하 여 패널을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d0f6c-114">Then, create a panel with some text so that the collapse/expand effect can be seen:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample2.aspx)]

<span data-ttu-id="d0f6c-115">알 수 있듯이 패널에는 다음과 같습니다 (및 기본적으로 패널의 너비 및 배경색을 정의)는 CSS 클래스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0f6c-115">As you can see, the panel references a CSS class which is shown here (and basically defines a background color and the panel's width):</span></span>

[!code-css[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample3.css)]

<span data-ttu-id="d0f6c-116">합니다 `CollapsiblePanelExtender` 컨트롤에 필요 합니다 `TargetControlID` 도구 키트에서 요청 시 확장 하거나 축소 패널을 알 수 있도록 특성:</span><span class="sxs-lookup"><span data-stu-id="d0f6c-116">The `CollapsiblePanelExtender` control requires the `TargetControlID` attribute so that the toolkit knows which panel to collapse or expand upon request:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample4.aspx)]

<span data-ttu-id="d0f6c-117">아쉽게도 현재 extender 패널을 확장 또는 축소에 대 한 특정 API를 노출 하지 않습니다 하지만 문서화 되지 않은 몇 가지 방법을 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0f6c-117">Unfortunately, the extender currently does not expose a specific API for collapsing or expanding the panel, but some undocumented methods will do.</span></span> <span data-ttu-id="d0f6c-118">먼저, 패널의 콘텐츠를 확장 하거나 축소 하는 클라이언트 쪽 JavaScript 트리거할 다음 페이지로 세 개의 HTML 단추를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0f6c-118">First of all, add three HTML buttons to the page which will then trigger the client-side JavaScript to collapse or expand the panel's contents:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample5.aspx)]

<span data-ttu-id="d0f6c-119">클라이언트 쪽 JavaScript 코드에서 (시작 `<script type="text/javascript">`), `$find()` 메서드를 사용 해야 합니다. 액세스를 `CollapsiblePanelExtender`입니다.</span><span class="sxs-lookup"><span data-stu-id="d0f6c-119">In the client-side JavaScript code (started with `<script type="text/javascript">`), the `$find()` method needs to be used to access the `CollapsiblePanelExtender`.</span></span> <span data-ttu-id="d0f6c-120">`$find("cpe")` 에 대 한 참조를 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0f6c-120">`$find("cpe")` will return a reference to it.</span></span> <span data-ttu-id="d0f6c-121">거기서부터 특정 메서드는 작업에 해결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0f6c-121">From there on, specific methods will solve the task at hand.</span></span>

<span data-ttu-id="d0f6c-122">메서드 (확장)를 열기 위한 패널 이라고 `_doOpen()`; 다음 구현 코드를 `doOpen()` 함수는 첫 번째 단추를 클릭할 때 호출:</span><span class="sxs-lookup"><span data-stu-id="d0f6c-122">The method for opening (expanding) the panel is called `_doOpen()`; the following code implements the `doOpen()` function called when the first button is clicked:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample6.js)]

<span data-ttu-id="d0f6c-123">패널을 축소 하거나 닫거나에 대 한는 `_doClose()` 메서드를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0f6c-123">For closing, or collapsing the panel, the `_doClose()` method needs to be executed.</span></span> <span data-ttu-id="d0f6c-124">따라서 사용자가 두 번째 단추를 클릭 하면 다음 JavaScript 코드 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0f6c-124">So when the user clicks on the second button, the following JavaScript code is called:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample7.js)]

<span data-ttu-id="d0f6c-125">패널의 상태를 전환 하는 세 번째 단추:에서 축소 하 여 확장 하 고 그 반대의 경우도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="d0f6c-125">The third button toggles the state of the panel: from collapsed to expanded, and vice versa.</span></span> <span data-ttu-id="d0f6c-126">`CollapsiblePanelExtender` 노출 된 `toggle()` 정확히 일치 하는 메서드: 패널의 상태를 반대로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d0f6c-126">The `CollapsiblePanelExtender` exposes the `toggle()` method which does exactly that: reverses the state of the panel.</span></span> <span data-ttu-id="d0f6c-127">그러나도 또 다른 방법이 있습니다 (에서 내부적으로 사용 되는 `toggle()` 메서드): 합니다 `get_Collapsed()` 메서드의 `CollapsiblePanelExtender()` 패널 축소 되는지 여부를 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="d0f6c-127">However there is also another approach (which is internally used by the `toggle()` method): The `get_Collapsed()` method of the `CollapsiblePanelExtender()` tells us whether the panel is collapsed or not.</span></span> <span data-ttu-id="d0f6c-128">이 함수의 반환 값에 따라 패널 인 확장 중 하나 (`_doOpen()` 메서드) 또는 축소 (`_doClose()`) 메서드.</span><span class="sxs-lookup"><span data-stu-id="d0f6c-128">Depending on the return value of this function, the panel is then either expanded (`_doOpen()` method) or collapsed (`_doClose()`) method:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample8.js)]


<span data-ttu-id="d0f6c-129">[![패널의 상태를 변경 하는 세 번째 단추:에서 확장 및 다시 축소](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d0f6c-129">[![The third button changes the state of the panel: from collapsed to expanded and back](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image1.png)</span></span>

<span data-ttu-id="d0f6c-130">패널의 상태를 변경 하는 세 번째 단추:에서 축소 하 여 확장 하 고 백 ([클릭 하 여 큰 이미지 보기](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="d0f6c-130">The third button changes the state of the panel: from collapsed to expanded and back ([Click to view full-size image](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="d0f6c-131">다음</span><span class="sxs-lookup"><span data-stu-id="d0f6c-131">Next</span></span>](collapsing-and-expanding-a-panel-from-javascript-vb.md)
