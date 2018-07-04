---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-vb
title: UpdatePanel (VB)를 사용 하 여 팝업 컨트롤에서 포스트백 처리 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit의 PopupControl extender는 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수를 제공 합니다. 특별 한 주의 수행 해야 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: ec9db57c-9f68-402a-bf4c-0d63d5f6908e
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-vb
msc.type: authoredcontent
ms.openlocfilehash: cf17025219fbf24e749c172f2ddb47ec20980cdc
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37395905"
---
<a name="handling-postbacks-from-a-popup-control-with-an-updatepanel-vb"></a><span data-ttu-id="71d28-104">UpdatePanel (VB)를 사용 하 여 팝업 컨트롤에서 포스트백 처리</span><span class="sxs-lookup"><span data-stu-id="71d28-104">Handling Postbacks from A Popup Control With an UpdatePanel (VB)</span></span>
====================
<span data-ttu-id="71d28-105">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="71d28-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="71d28-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="71d28-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2VB.pdf)</span></span>

> <span data-ttu-id="71d28-107">AJAX Control Toolkit의 PopupControl extender는 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="71d28-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="71d28-108">특별 한 주의 이러한 팝업에 포스트백이 발생할 때 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71d28-108">Special care has to be taken when a postback occurs within such a popup.</span></span>


## <a name="overview"></a><span data-ttu-id="71d28-109">개요</span><span class="sxs-lookup"><span data-stu-id="71d28-109">Overview</span></span>

<span data-ttu-id="71d28-110">AJAX Control Toolkit의 PopupControl extender는 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="71d28-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="71d28-111">특별 한 주의 이러한 팝업에 포스트백이 발생할 때 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71d28-111">Special care has to be taken when a postback occurs within such a popup.</span></span>

## <a name="steps"></a><span data-ttu-id="71d28-112">단계</span><span class="sxs-lookup"><span data-stu-id="71d28-112">Steps</span></span>

<span data-ttu-id="71d28-113">사용 하는 경우는 `PopupControl` 포스트백을 사용 하 여는 `UpdatePanel` 포스트백 페이지 새로 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71d28-113">When using a `PopupControl` with a postback, an `UpdatePanel` can prevent the page refresh caused by the postback.</span></span> <span data-ttu-id="71d28-114">다음 태그는 몇 가지 중요 한 요소를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="71d28-114">The following markup defines a couple of important elements:</span></span>

- <span data-ttu-id="71d28-115">`ScriptManager` ASP.NET AJAX Control Toolkit 작동할 수 있도록 제어</span><span class="sxs-lookup"><span data-stu-id="71d28-115">A `ScriptManager` control so that the ASP.NET AJAX Control Toolkit works</span></span>
- <span data-ttu-id="71d28-116">두 `TextBox` 팝업 모두 트리거할 컨트롤</span><span class="sxs-lookup"><span data-stu-id="71d28-116">Two `TextBox` controls which will both trigger a popup</span></span>
- <span data-ttu-id="71d28-117">`Panel` 팝업 사용할 컨트롤</span><span class="sxs-lookup"><span data-stu-id="71d28-117">A `Panel` control that will serve as the popup</span></span>
- <span data-ttu-id="71d28-118">패널 내에서 한 `Calendar` 컨트롤 내에 포함 되는 `UpdatePanel` 컨트롤</span><span class="sxs-lookup"><span data-stu-id="71d28-118">Within the panel, a `Calendar` control is embedded within an `UpdatePanel` control</span></span>
- <span data-ttu-id="71d28-119">두 `PopupControlExtender` 패널의 텍스트 상자에 할당 하는 컨트롤</span><span class="sxs-lookup"><span data-stu-id="71d28-119">Two `PopupControlExtender` controls that assign the panel to the text boxes</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/samples/sample1.aspx)]

<span data-ttu-id="71d28-120">`OnSelectionChanged` 특성을 `Calendar` 컨트롤 설정.</span><span class="sxs-lookup"><span data-stu-id="71d28-120">Note that the `OnSelectionChanged` attribute of the `Calendar` control is set.</span></span> <span data-ttu-id="71d28-121">포스트백이 발생할 때 사용자가 달력의 날짜를 선택 하도록 하 고 서버 측 메서드 `c1_SelectionChanged()` 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="71d28-121">So when the user selects a date within the calendar, a postback occurs and the server-side method `c1_SelectionChanged()` is executed.</span></span> <span data-ttu-id="71d28-122">이 메서드 내에 현재 날짜를 검색 하 고 텍스트 상자에 다시 쓸 수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71d28-122">Within that method, the current date must be retrieved and written back to the textbox.</span></span>

<span data-ttu-id="71d28-123">에 대 한 구문은 다음과 같습니다: 먼저 모든 프록시에 대 한 개체는 `PopupControlExtender` 페이지에서 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71d28-123">The syntax for that is as follows: First of all, a proxy object for the `PopupControlExtender` on the page must be generated.</span></span> <span data-ttu-id="71d28-124">ASP.NET AJAX Control Toolkit에서 제공 된 `GetProxyForCurrentPopup()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="71d28-124">The ASP.NET AJAX Control Toolkit offers the `GetProxyForCurrentPopup()` method.</span></span> <span data-ttu-id="71d28-125">이 메서드는 반환 된 개체에서 지원 합니다 `Commit()` 메서드 (컨트롤 아니라 메서드 호출을 트리거한!) 팝업을 트리거한 컨트롤에 다시 값을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="71d28-125">The object this method returns supports the `Commit()` method which sends a value back to the control that triggered the popup (not the control that triggered the method call!).</span></span> <span data-ttu-id="71d28-126">다음 코드에서는 선택된 된 날짜에 대 한 인수로 `Commit()` 메서드를 텍스트 상자에 선택한 날짜를 다시 작성 하는 코드를 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="71d28-126">The following code provides the selected date as the argument for the `Commit()` method, causing the code to write the selected date back to the text box:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/samples/sample2.aspx)]

<span data-ttu-id="71d28-127">이제 클릭할 때마다 달력 날짜를 관련된 텍스트 상자에 표시할 선택한 날짜는 날짜 선택 컨트롤 만들기 현재 있습니다 많은 웹 사이트에서.</span><span class="sxs-lookup"><span data-stu-id="71d28-127">Now whenever you click on a calendar date, the selected date appears in the associated text box, creating a date picker control that can currently be found on many websites.</span></span>


<span data-ttu-id="71d28-128">[![텍스트 상자에 사용자가 클릭 하면 달력이 나타납니다.](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="71d28-128">[![The Calendar appears when the user clicks into the textbox](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image1.png)</span></span>

<span data-ttu-id="71d28-129">텍스트 상자에 사용자가 클릭 하면 달력이 나타납니다 ([클릭 하 여 큰 이미지 보기](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="71d28-129">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image3.png))</span></span>


<span data-ttu-id="71d28-130">[![날짜를 클릭 하면 텍스트 상자에 전환](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="71d28-130">[![Clicking on a date puts it in the textbox](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image4.png)</span></span>

<span data-ttu-id="71d28-131">날짜를 클릭 하면 텍스트 상자에 배치 ([클릭 하 여 큰 이미지 보기](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="71d28-131">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="71d28-132">[이전](using-multiple-popup-controls-vb.md)
> [다음](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb.md)</span><span class="sxs-lookup"><span data-stu-id="71d28-132">[Previous](using-multiple-popup-controls-vb.md)
[Next](handling-postbacks-from-a-popup-control-without-an-updatepanel-vb.md)</span></span>
