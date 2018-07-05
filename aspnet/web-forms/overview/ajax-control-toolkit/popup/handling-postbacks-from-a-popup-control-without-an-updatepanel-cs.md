---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
title: UpdatePanel (C#) 하지 않고 팝업 컨트롤에서 포스트백 처리 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit의 PopupControl extender는 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수를 제공 합니다. Su에서 포스트백을 발생 하면...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 25444121-5a72-4dac-8e50-ad2b7ac667af
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: d74a44a277bdcb460dc20b78bad3e5ed68445b4a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37370985"
---
<a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-c"></a><span data-ttu-id="89da9-104">UpdatePanel (C#) 하지 않고 팝업 컨트롤에서 포스트백 처리</span><span class="sxs-lookup"><span data-stu-id="89da9-104">Handling Postbacks from A Popup Control Without an UpdatePanel (C#)</span></span>
====================
<span data-ttu-id="89da9-105">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="89da9-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="89da9-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="89da9-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3CS.pdf)</span></span>

> <span data-ttu-id="89da9-107">AJAX Control Toolkit의 PopupControl extender는 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="89da9-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="89da9-108">이러한 패널의 포스트백이 발생할 때 페이지에 여러 패널 패널 클릭 했는지 확인 하기 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="89da9-108">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>


## <a name="overview"></a><span data-ttu-id="89da9-109">개요</span><span class="sxs-lookup"><span data-stu-id="89da9-109">Overview</span></span>

<span data-ttu-id="89da9-110">AJAX Control Toolkit의 PopupControl extender는 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="89da9-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="89da9-111">이러한 패널의 포스트백이 발생할 때 페이지에 여러 패널 패널 클릭 했는지 확인 하기 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="89da9-111">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="steps"></a><span data-ttu-id="89da9-112">단계</span><span class="sxs-lookup"><span data-stu-id="89da9-112">Steps</span></span>

<span data-ttu-id="89da9-113">사용 하는 경우는 `PopupControl` 포스트백을 있지만 필요 없이 `UpdatePanel` 페이지의 컨트롤 도구 키트에서 포스트백을 발생 하는 팝업을 트리거 했습니다. 클라이언트 요소를 결정 하는 방법을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="89da9-113">When using a `PopupControl` with a postback, but without having an `UpdatePanel` on the page, the Control Toolkit does not offer a way to determine which client element has triggered the popup which in turn caused the postback.</span></span> <span data-ttu-id="89da9-114">그러나 작은 트릭이이 시나리오에 대 한 해결 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="89da9-114">However a small trick provides a workaround for this scenario.</span></span>

<span data-ttu-id="89da9-115">먼저, 기본 설정 같습니다.:는 모두 동일한 팝업 일정 트리거는 두 개의 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="89da9-115">First of all, here is the basic setup: two text boxes which both trigger the same popup, a calendar.</span></span> <span data-ttu-id="89da9-116">두 `PopupControlExtenders` 텍스트 상자 및 팝업을 결합 합니다.</span><span class="sxs-lookup"><span data-stu-id="89da9-116">Two `PopupControlExtenders` bring text boxes and popup together.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample1.aspx)]

<span data-ttu-id="89da9-117">기본 개념에는 숨겨진된 폼 필드를 추가 하는 것은 &lt; `form` &gt; 팝업을 시작 하는 입력란을 포함 하는 요소:</span><span class="sxs-lookup"><span data-stu-id="89da9-117">The basic idea is to add a hidden form field in the &lt;`form`&gt; element that holds the text box which launched the popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample2.aspx)]

<span data-ttu-id="89da9-118">JavaScript 코드 페이지가 로드 될 때 두 텍스트 상자에 이벤트 처리기를 추가 합니다: 이름과 숨겨진된 폼 필드에 기록 될 때마다 사용자가 텍스트 상자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="89da9-118">When the page is loaded, JavaScript code adds an event handler to both text boxes: Whenever the user clicks on a text box, its name is written into the hidden form field:</span></span>

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample3.html)]

<span data-ttu-id="89da9-119">서버 쪽 코드에서 숨겨진된 필드의 값을 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89da9-119">In the server-side code, the value of the hidden field must be read.</span></span> <span data-ttu-id="89da9-120">숨겨진된 양식 필드를 조작 하는 간단한 되므로 숨겨진된 값의 유효성을 검사 방법은 화이트 리스트 필요한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="89da9-120">Since hidden form fields are trivial to manipulate, a whitelist approach to validate the hidden value is required.</span></span> <span data-ttu-id="89da9-121">올바른 입력란을 식별 한 후 달력에서 날짜에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89da9-121">Once the correct text box has been identified, the date from the calendar is written into it.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample4.aspx)]


<span data-ttu-id="89da9-122">[![텍스트 상자에 사용자가 클릭 하면 달력이 나타납니다.](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="89da9-122">[![The Calendar appears when the user clicks into the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image1.png)</span></span>

<span data-ttu-id="89da9-123">텍스트 상자에 사용자가 클릭 하면 달력이 나타납니다 ([클릭 하 여 큰 이미지 보기](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="89da9-123">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image3.png))</span></span>


<span data-ttu-id="89da9-124">[![날짜를 클릭 하면 텍스트 상자에 전환](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="89da9-124">[![Clicking on a date puts it in the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image4.png)</span></span>

<span data-ttu-id="89da9-125">날짜를 클릭 하면 텍스트 상자에 배치 ([클릭 하 여 큰 이미지 보기](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="89da9-125">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="89da9-126">[이전](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
> [다음](using-multiple-popup-controls-vb.md)</span><span class="sxs-lookup"><span data-stu-id="89da9-126">[Previous](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
[Next](using-multiple-popup-controls-vb.md)</span></span>
