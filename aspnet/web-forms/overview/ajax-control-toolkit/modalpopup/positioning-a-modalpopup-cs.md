---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-cs
title: (C#) ModalPopup 위치 지정 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit의 ModalPopup 컨트롤 클라이언트 쪽 의미를 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 그러나 컨트롤을 제공 하지 않습니다는 중...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 1caac9d0-e21e-49d6-a8ff-e563a736d6ca
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-cs
msc.type: authoredcontent
ms.openlocfilehash: e767785f801b5110f0e9e915cd35c8a4425a9487
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41838272"
---
<a name="positioning-a-modalpopup-c"></a><span data-ttu-id="3784f-104">(C#) ModalPopup 위치 지정</span><span class="sxs-lookup"><span data-stu-id="3784f-104">Positioning a ModalPopup (C#)</span></span>
====================
<span data-ttu-id="3784f-105">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="3784f-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="3784f-106">[코드를 다운로드](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="3784f-106">[Download Code](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4CS.pdf)</span></span>

> <span data-ttu-id="3784f-107">AJAX Control Toolkit의 ModalPopup 컨트롤 클라이언트 쪽 의미를 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3784f-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="3784f-108">그러나 컨트롤은 팝업의 위치는 기본 제공 기능을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3784f-108">However the control does not offer a built-in functionality to position the popup.</span></span>


## <a name="overview"></a><span data-ttu-id="3784f-109">개요</span><span class="sxs-lookup"><span data-stu-id="3784f-109">Overview</span></span>

<span data-ttu-id="3784f-110">AJAX Control Toolkit의 ModalPopup 컨트롤 클라이언트 쪽 의미를 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3784f-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="3784f-111">그러나 컨트롤은 팝업의 위치는 기본 제공 기능을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3784f-111">However the control does not offer a built-in functionality to position the popup.</span></span>

## <a name="steps"></a><span data-ttu-id="3784f-112">단계</span><span class="sxs-lookup"><span data-stu-id="3784f-112">Steps</span></span>

<span data-ttu-id="3784f-113">ASP.NET AJAX와 Control Toolkit의 기능을 활성화 하기 위해는 `ScriptManager`합니다.</span><span class="sxs-lookup"><span data-stu-id="3784f-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager`.</span></span> <span data-ttu-id="3784f-114">컨트롤 페이지의 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소).</span><span class="sxs-lookup"><span data-stu-id="3784f-114">control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample1.aspx)]

<span data-ttu-id="3784f-115">다음으로 모달 팝업으로 사용 되는 패널을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3784f-115">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="3784f-116">단추는 팝업을 닫는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3784f-116">A button is used to close the popup:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample2.aspx)]

<span data-ttu-id="3784f-117">팝업이 표시 될 때마다 페이지에는 특정 위치에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3784f-117">Whenever the popup is shown, it shall be positioned at a certain place in the page.</span></span> <span data-ttu-id="3784f-118">이 태스크에 대 한 클라이언트 쪽 JavaScript 함수가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3784f-118">For this task, a client-side JavaScript function is created.</span></span> <span data-ttu-id="3784f-119">패널에 액세스 하려면 먼저 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="3784f-119">It first tries to access the panel.</span></span> <span data-ttu-id="3784f-120">성공 하면 패널의 위치는 CSS 및 JavaScript (에서 팝업의 위치는 변경)를 사용 하 여 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3784f-120">If it succeeds, the panel's position is set using CSS and JavaScript (change the position of the popup at will).</span></span> <span data-ttu-id="3784f-121">그러나 `ModalPopupExtender` 제어도 팝업 배치 하려고 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="3784f-121">However the `ModalPopupExtender` control also tries to position the popup.</span></span> <span data-ttu-id="3784f-122">따라서 JavaScript 코드를 반복적으로 팝업 0.1 초 마다 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="3784f-122">Therefore, the JavaScript code repeatedly positions the popup, every tenth of a second.</span></span>

[!code-html[Main](positioning-a-modalpopup-cs/samples/sample3.html)]

<span data-ttu-id="3784f-123">알 수 있듯이의 반환 값은 `setTimeout()` JavaScript 메서드는 전역 변수에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3784f-123">As you can see, the return value of the `setTimeout()` JavaScript method is saved in a global variable.</span></span> <span data-ttu-id="3784f-124">이렇게 하면 요청 시 팝업의 위치 지정 반복을 중지 하려면 사용 하는 `clearTimeout()` 메서드:</span><span class="sxs-lookup"><span data-stu-id="3784f-124">This allows to stop the repeated positioning of the popup on demand, using the `clearTimeout()` method:</span></span>

[!code-javascript[Main](positioning-a-modalpopup-cs/samples/sample4.js)]

<span data-ttu-id="3784f-125">이제 위해 남아 있는 모든 적절 한 때마다 이러한 함수를 호출 하는 브라우저를 확인 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3784f-125">Now all that is left to do is to make the browser call these functions whenever appropriate.</span></span> <span data-ttu-id="3784f-126">`movePanel()` 패널을 트리거하는 단추를 클릭할 때 JavaScript 함수를 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3784f-126">The `movePanel()` JavaScript function must be called when the button is clicked that triggers the panel:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample5.aspx)]

<span data-ttu-id="3784f-127">하며 `stopMoving()` 팝업이이 있습니다 닫힐 때 함수 고려해 야 트리거할 수는 `ModalPopupExtender` 제어:</span><span class="sxs-lookup"><span data-stu-id="3784f-127">And the `stopMoving()` function comes into play when the popup is closed this can be triggered in the `ModalPopupExtender` control:</span></span>

[!code-aspx[Main](positioning-a-modalpopup-cs/samples/sample6.aspx)]


<span data-ttu-id="3784f-128">[![지정 된 위치에서 모달 팝업 표시](positioning-a-modalpopup-cs/_static/image2.png)](positioning-a-modalpopup-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3784f-128">[![The modal popup appears at the designated position](positioning-a-modalpopup-cs/_static/image2.png)](positioning-a-modalpopup-cs/_static/image1.png)</span></span>

<span data-ttu-id="3784f-129">모달 팝업에 지정 된 위치에 있는 표시 되는 경우 ([클릭 하 여 큰 이미지 보기](positioning-a-modalpopup-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="3784f-129">The modal popup appears at the designated position ([Click to view full-size image](positioning-a-modalpopup-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3784f-130">[이전](handling-postbacks-from-a-modalpopup-cs.md)
> [다음](launching-a-modal-popup-window-from-server-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="3784f-130">[Previous](handling-postbacks-from-a-modalpopup-cs.md)
[Next](launching-a-modal-popup-window-from-server-code-vb.md)</span></span>
