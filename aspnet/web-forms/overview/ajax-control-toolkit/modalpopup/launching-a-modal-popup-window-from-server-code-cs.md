---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-cs
title: 서버 코드 (C#)에서 모달 팝업 창을 시작 | Microsoft Docs
author: wenz
description: 들어에서 ModalPopup 컨트롤을 클라이언트 쪽 방법을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 그러나 일부 시나리오에서는 t 해야...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 2f67d8ef-73ca-447d-a0cc-6e3168431e6a
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 04bb056ee29065a472a70d480568b897a789ae59
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="launching-a-modal-popup-window-from-server-code-c"></a><span data-ttu-id="449e2-104">서버 코드 (C#)에서 모달 팝업 창을 시작</span><span class="sxs-lookup"><span data-stu-id="449e2-104">Launching a Modal Popup Window from Server Code (C#)</span></span>
====================
<span data-ttu-id="449e2-105">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="449e2-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="449e2-106">[코드를 다운로드](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="449e2-106">[Download Code](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1CS.pdf)</span></span>

> <span data-ttu-id="449e2-107">들어에서 ModalPopup 컨트롤을 클라이언트 쪽 방법을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="449e2-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="449e2-108">그러나 일부 시나리오 모달 팝업을 여는 서버 쪽에서 트리거되는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="449e2-108">However some scenarios require that the opening of the modal popup is triggered on the server-side.</span></span>


## <a name="overview"></a><span data-ttu-id="449e2-109">개요</span><span class="sxs-lookup"><span data-stu-id="449e2-109">Overview</span></span>

<span data-ttu-id="449e2-110">들어에서 ModalPopup 컨트롤을 클라이언트 쪽 방법을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="449e2-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="449e2-111">그러나 일부 시나리오 모달 팝업을 여는 서버 쪽에서 트리거되는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="449e2-111">However some scenarios require that the opening of the modal popup is triggered on the server-side.</span></span>

## <a name="steps"></a><span data-ttu-id="449e2-112">단계</span><span class="sxs-lookup"><span data-stu-id="449e2-112">Steps</span></span>

<span data-ttu-id="449e2-113">우선, ASP.NET Button 웹 컨트롤 ModalPopup 컨트롤의 작동 방식을 설명 하기 위해 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="449e2-113">First of all, an ASP.NET Button web control is required to demonstrate how the ModalPopup control works.</span></span> <span data-ttu-id="449e2-114">내에서 이러한 단추 추가 &lt;양식&gt; 새 페이지에는 요소:</span><span class="sxs-lookup"><span data-stu-id="449e2-114">Add such a button within the &lt;form&gt; element on a new page:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample1.aspx)]

<span data-ttu-id="449e2-115">그런 다음 태그를 만들려는 팝업 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="449e2-115">Then, you need the markup for the popup you want to create.</span></span> <span data-ttu-id="449e2-116">로 정의 된 `<asp:Panel>` 제어 하 고 단추 컨트롤이 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="449e2-116">Define it as an `<asp:Panel>` control and make sure that it includes a Button control.</span></span> <span data-ttu-id="449e2-117">ModalPopup 컨트롤은 단추를 만들려면 이러한 닫기 팝업; 기능을 제공 합니다. 그렇지 않으면 쉽게 두면 사라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="449e2-117">The ModalPopup control offers the functionality to make such a button close the popup; otherwise there is no easy way to let it vanish.</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample2.aspx)]

<span data-ttu-id="449e2-118">다음 페이지에는 ASP.NET AJAX 도구 키트에서 ModalPopup 제어를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="449e2-118">Next add the ModalPopup control from the ASP.NET AJAX Toolkit to the page.</span></span> <span data-ttu-id="449e2-119">컨트롤을 로드 하는 단추, 사라지는 하므로 단추 및 실제 팝업의 ID에 대 한 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="449e2-119">Set properties for the button which loads the control, the button which makes it disappear, and the ID of the actual popup.</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample3.aspx)]

<span data-ttu-id="449e2-120">ASP.NET AJAX;에 따라 모든 웹 페이지와 마찬가지로 스크립트 관리자는 다른 대상 브라우저에 대 한 필요한 JavaScript 라이브러리를 로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="449e2-120">As with all web pages based on ASP.NET AJAX; the Script Manager is required to load the necessary JavaScript libraries for the different target browsers:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample4.aspx)]

<span data-ttu-id="449e2-121">브라우저에서 예제를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="449e2-121">Run the example in the browser.</span></span> <span data-ttu-id="449e2-122">단추를 클릭 하면 모달 팝업이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="449e2-122">When you click on the button, the modal popup appears.</span></span> <span data-ttu-id="449e2-123">서버 쪽 코드를 사용 하 여 동일한 효과 최대화 하기 위해 새 단추가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="449e2-123">In order to achieve the same effect using server-side code, a new button is required:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample5.aspx)]

<span data-ttu-id="449e2-124">단추 클릭에서 포스트백을 생성 하 여 실행 볼 수 있듯이 `ServerButton_Click()` 서버에서 메서드.</span><span class="sxs-lookup"><span data-stu-id="449e2-124">As you can see, a click on the button generates a postback and executes the `ServerButton_Click()` method on the server.</span></span> <span data-ttu-id="449e2-125">이 메서드는 JavaScript 함수가 호출 `launchModal()` 실행 정확 하 게, JavaScript 함수 실행 됩니다 페이지가 로드 되 면:</span><span class="sxs-lookup"><span data-stu-id="449e2-125">In this method, a JavaScript function called `launchModal()` is executed to be exact, the JavaScript function will be executed once the page has been loaded:</span></span>

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample6.aspx)]

<span data-ttu-id="449e2-126">작업 `launchModal()` 는 ModalPopup 표시 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="449e2-126">The job of `launchModal()` is to display the ModalPopup.</span></span> <span data-ttu-id="449e2-127">`launchModal()` 함수는 전체 HTML 페이지 로드 되 면 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="449e2-127">The `launchModal()` function is executed once the complete HTML page has been loaded.</span></span> <span data-ttu-id="449e2-128">그러나 그 시점에 ASP.NET AJAX 프레임 워크 로드 되지 않았습니다 완전히 아직 있습니다.</span><span class="sxs-lookup"><span data-stu-id="449e2-128">At that moment, however, the ASP.NET AJAX framework has not been fully loaded yet.</span></span> <span data-ttu-id="449e2-129">따라서는 `launchModal()` 함수 방금 ModalPopup 컨트롤 나중에 표시 해야 하는 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="449e2-129">Therefore, the `launchModal()` function just sets a variable that the ModalPopup control must be shown later on:</span></span>

[!code-html[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample7.html)]

<span data-ttu-id="449e2-130">`pageLoad()` JavaScript 함수는 ASP.NET AJAX 완전히 로드 되 면 실행 되는 특수 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="449e2-130">The `pageLoad()` JavaScript function is a special function that gets executed once ASP.NET AJAX has been fully loaded.</span></span> <span data-ttu-id="449e2-131">따라서 ModalPopup 컨트롤 이지만 경우에만 표시 하려면이 함수에 코드를 추가 했습니다 `launchModal()` 가 호출 하기 전에:</span><span class="sxs-lookup"><span data-stu-id="449e2-131">Therefore we add code to this function to show the ModalPopup control, but only if `launchModal()` has been called before:</span></span>

[!code-javascript[Main](launching-a-modal-popup-window-from-server-code-cs/samples/sample8.js)]

<span data-ttu-id="449e2-132">`$find()` 함수 페이지에서 명명된 된 요소를 찾고 및 서버 쪽 ID를 매개 변수로 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="449e2-132">The `$find()` function is looking for a named element on the page and expects the server-side ID as a parameter.</span></span> <span data-ttu-id="449e2-133">따라서 `$find("mpe")` ModalPopup 컨트롤의 클라이언트 표시를 반환 합니다; 해당 `show()` 메서드를 사용 하는 팝업 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="449e2-133">Therefore, `$find("mpe")` returns the client representation of the ModalPopup control; its `show()` method lets the popup appear.</span></span>


<span data-ttu-id="449e2-134">[![모달 팝업이 표시 되는 경우 단추 중 하나를 클릭](launching-a-modal-popup-window-from-server-code-cs/_static/image2.png)](launching-a-modal-popup-window-from-server-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="449e2-134">[![The modal popup appears when either of the buttons is clicked](launching-a-modal-popup-window-from-server-code-cs/_static/image2.png)](launching-a-modal-popup-window-from-server-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="449e2-135">모달 팝업이 표시 되는 경우 단추 중 하나를 클릭 ([전체 크기 이미지를 보려면 클릭](launching-a-modal-popup-window-from-server-code-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="449e2-135">The modal popup appears when either of the buttons is clicked ([Click to view full-size image](launching-a-modal-popup-window-from-server-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="449e2-136">다음</span><span class="sxs-lookup"><span data-stu-id="449e2-136">Next</span></span>](using-modalpopup-with-a-repeater-control-cs.md)
