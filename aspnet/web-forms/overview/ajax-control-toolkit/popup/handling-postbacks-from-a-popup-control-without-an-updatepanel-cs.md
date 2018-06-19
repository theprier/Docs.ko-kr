---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
title: UpdatePanel (C#) 없이 Popup 컨트롤의 포스트백 처리 | Microsoft Docs
author: wenz
description: 에 들어 PopupControl extender 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수 있는 방법을 제공 합니다. 포스트백 su에서 발생 하면...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 25444121-5a72-4dac-8e50-ad2b7ac667af
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: 59ffa05945289de6e01e2c21dd5a0f82ca1fa374
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30879545"
---
<a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-c"></a><span data-ttu-id="ac740-104">UpdatePanel (C#) 없이 Popup 컨트롤에서 포스트백을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="ac740-104">Handling Postbacks from A Popup Control Without an UpdatePanel (C#)</span></span>
====================
<span data-ttu-id="ac740-105">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="ac740-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ac740-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="ac740-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3CS.pdf)</span></span>

> <span data-ttu-id="ac740-107">에 들어 PopupControl extender 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수 있는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac740-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="ac740-108">이러한 패널에 포스트백이 발생할 때 여러 패널은 페이지에는 어떤 패널 클릭 했는지 확인 하려면 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="ac740-108">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>


## <a name="overview"></a><span data-ttu-id="ac740-109">개요</span><span class="sxs-lookup"><span data-stu-id="ac740-109">Overview</span></span>

<span data-ttu-id="ac740-110">에 들어 PopupControl extender 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수 있는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac740-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="ac740-111">이러한 패널에 포스트백이 발생할 때 여러 패널은 페이지에는 어떤 패널 클릭 했는지 확인 하려면 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="ac740-111">When a postback occurs in such a panel and there are several panels on the page it is hard to determine which panel has been clicked.</span></span>

## <a name="steps"></a><span data-ttu-id="ac740-112">단계</span><span class="sxs-lookup"><span data-stu-id="ac740-112">Steps</span></span>

<span data-ttu-id="ac740-113">사용 하는 경우는 `PopupControl` 포스트백 있지만 필요 없이 `UpdatePanel` 페이지 컨트롤 Toolkit 클라이언트 요소에 포스트백을 실행 하는 팝업을 트리거 했습니다. 결정 하는 방법을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ac740-113">When using a `PopupControl` with a postback, but without having an `UpdatePanel` on the page, the Control Toolkit does not offer a way to determine which client element has triggered the popup which in turn caused the postback.</span></span> <span data-ttu-id="ac740-114">그러나 작은 트릭이이 시나리오에 대 한 해결 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac740-114">However a small trick provides a workaround for this scenario.</span></span>

<span data-ttu-id="ac740-115">우선, 기본 설정 같습니다:이 두 가지 동일한 팝업 일정을 트리거하는 두 개의 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="ac740-115">First of all, here is the basic setup: two text boxes which both trigger the same popup, a calendar.</span></span> <span data-ttu-id="ac740-116">두 개의 `PopupControlExtenders` 텍스트 상자 및 팝업 모읍니다.</span><span class="sxs-lookup"><span data-stu-id="ac740-116">Two `PopupControlExtenders` bring text boxes and popup together.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample1.aspx)]

<span data-ttu-id="ac740-117">기본 개념에는 숨겨진된 폼 필드를 추가 하는 것은 &lt; `form` &gt; 팝업을 시작 하 고 텍스트 상자에 포함 된 요소:</span><span class="sxs-lookup"><span data-stu-id="ac740-117">The basic idea is to add a hidden form field in the &lt;`form`&gt; element that holds the text box which launched the popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample2.aspx)]

<span data-ttu-id="ac740-118">JavaScript 코드 두 텍스트 상자에 이벤트 처리기를 추가 하는 페이지가 로드 되 면: 숨겨진된 폼 필드에 기록 된 해당 이름 때마다 사용자가 텍스트 상자를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac740-118">When the page is loaded, JavaScript code adds an event handler to both text boxes: Whenever the user clicks on a text box, its name is written into the hidden form field:</span></span>

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample3.html)]

<span data-ttu-id="ac740-119">서버 쪽 코드에 숨겨진된 필드의 값을 읽을 수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac740-119">In the server-side code, the value of the hidden field must be read.</span></span> <span data-ttu-id="ac740-120">숨겨진된 양식 필드와 조작 하기 위한 간단한 되므로 허용 목록에서 숨겨진된 값을 검사할 방법은 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac740-120">Since hidden form fields are trivial to manipulate, a whitelist approach to validate the hidden value is required.</span></span> <span data-ttu-id="ac740-121">올바른 입력란을 식별 한 후 달력에서 날짜 데이터베이스에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac740-121">Once the correct text box has been identified, the date from the calendar is written into it.</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample4.aspx)]


<span data-ttu-id="ac740-122">[![입력란에 사용자가 클릭 하면 달력이 나타납니다.](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ac740-122">[![The Calendar appears when the user clicks into the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image1.png)</span></span>

<span data-ttu-id="ac740-123">입력란에 사용자가 클릭 하면 달력이 나타납니다 ([전체 크기 이미지를 보려면 클릭](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="ac740-123">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image3.png))</span></span>


<span data-ttu-id="ac740-124">[![날짜를 클릭 하면 텍스트 상자에 전환](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="ac740-124">[![Clicking on a date puts it in the textbox](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image4.png)</span></span>

<span data-ttu-id="ac740-125">날짜를 클릭 하면 텍스트 상자에 전환 ([전체 크기 이미지를 보려면 클릭](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="ac740-125">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ac740-126">[이전](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
> [다음](using-multiple-popup-controls-vb.md)</span><span class="sxs-lookup"><span data-stu-id="ac740-126">[Previous](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
[Next](using-multiple-popup-controls-vb.md)</span></span>
