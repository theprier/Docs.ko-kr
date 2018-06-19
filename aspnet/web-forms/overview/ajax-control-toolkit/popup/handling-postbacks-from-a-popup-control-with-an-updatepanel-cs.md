---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-cs
title: UpdatePanel (C#)와 Popup 컨트롤의 포스트백 처리 | Microsoft Docs
author: wenz
description: 에 들어 PopupControl extender 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수 있는 방법을 제공 합니다. 특별 한 주의 만들어야 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 1f68f59d-9c1e-4cf3-b304-c13ae6b7203e
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-with-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: abedb5247f710b02752651a7bfb011ab63d32844
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30879636"
---
<a name="handling-postbacks-from-a-popup-control-with-an-updatepanel-c"></a><span data-ttu-id="2c41a-104">UpdatePanel (C#)와 Popup 컨트롤에서 포스트백을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="2c41a-104">Handling Postbacks from A Popup Control With an UpdatePanel (C#)</span></span>
====================
<span data-ttu-id="2c41a-105">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="2c41a-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="2c41a-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="2c41a-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl2.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol2CS.pdf)</span></span>

> <span data-ttu-id="2c41a-107">에 들어 PopupControl extender 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수 있는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c41a-107">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="2c41a-108">특별 한 주의 이러한 팝업 내의 포스트백이 발생할 때 수행할에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c41a-108">Special care has to be taken when a postback occurs within such a popup.</span></span>


## <a name="overview"></a><span data-ttu-id="2c41a-109">개요</span><span class="sxs-lookup"><span data-stu-id="2c41a-109">Overview</span></span>

<span data-ttu-id="2c41a-110">에 들어 PopupControl extender 쉽게 다른 컨트롤이 활성화 될 때 팝업을 트리거할 수 있는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c41a-110">The PopupControl extender in the AJAX Control Toolkit offers an easy way to trigger a popup when any other control is activated.</span></span> <span data-ttu-id="2c41a-111">특별 한 주의 이러한 팝업 내의 포스트백이 발생할 때 수행할에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c41a-111">Special care has to be taken when a postback occurs within such a popup.</span></span>

## <a name="steps"></a><span data-ttu-id="2c41a-112">단계</span><span class="sxs-lookup"><span data-stu-id="2c41a-112">Steps</span></span>

<span data-ttu-id="2c41a-113">사용 하는 경우는 `PopupControl` 포스트백에서는 `UpdatePanel` 포스트백 페이지 새로 고침 하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c41a-113">When using a `PopupControl` with a postback, an `UpdatePanel` can prevent the page refresh caused by the postback.</span></span> <span data-ttu-id="2c41a-114">다음 태그 몇 가지 중요 한 요소를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="2c41a-114">The following markup defines a couple of important elements:</span></span>

- <span data-ttu-id="2c41a-115">A `ScriptManager` ASP.NET AJAX 컨트롤 도구 키트 작동 되도록</span><span class="sxs-lookup"><span data-stu-id="2c41a-115">A `ScriptManager` control so that the ASP.NET AJAX Control Toolkit works</span></span>
- <span data-ttu-id="2c41a-116">두 개의 `TextBox` 팝업 트리거되고 둘 다 컨트롤</span><span class="sxs-lookup"><span data-stu-id="2c41a-116">Two `TextBox` controls which will both trigger a popup</span></span>
- <span data-ttu-id="2c41a-117">A `Panel` 팝업 기호로 사용할 컨트롤</span><span class="sxs-lookup"><span data-stu-id="2c41a-117">A `Panel` control that will serve as the popup</span></span>
- <span data-ttu-id="2c41a-118">패널 내에서 한 `Calendar` 컨트롤 내에 포함 되는 `UpdatePanel` 컨트롤</span><span class="sxs-lookup"><span data-stu-id="2c41a-118">Within the panel, a `Calendar` control is embedded within an `UpdatePanel` control</span></span>
- <span data-ttu-id="2c41a-119">두 개의 `PopupControlExtender` 패널에서 텍스트 상자에 할당 하는 컨트롤</span><span class="sxs-lookup"><span data-stu-id="2c41a-119">Two `PopupControlExtender` controls that assign the panel to the text boxes</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/samples/sample1.aspx)]

<span data-ttu-id="2c41a-120">`OnSelectionChanged` 특성에는 `Calendar` 컨트롤 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c41a-120">Note that the `OnSelectionChanged` attribute of the `Calendar` control is set.</span></span> <span data-ttu-id="2c41a-121">포스트백이 발생할 때 사용자가 달력에서 날짜를 선택 하도록 하 고 서버 쪽 메서드 `c1_SelectionChanged()` 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c41a-121">So when the user selects a date within the calendar, a postback occurs and the server-side method `c1_SelectionChanged()` is executed.</span></span> <span data-ttu-id="2c41a-122">이 메서드 내에 현재 날짜를 검색 하 고 텍스트 상자에 다시 기록 수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c41a-122">Within that method, the current date must be retrieved and written back to the textbox.</span></span>

<span data-ttu-id="2c41a-123">에 대 한 구문은 다음과 같습니다: 우선, 프록시 개체에 대 한는 `PopupControlExtender` 페이지 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c41a-123">The syntax for that is as follows: First of all, a proxy object for the `PopupControlExtender` on the page must be generated.</span></span> <span data-ttu-id="2c41a-124">ASP.NET AJAX 컨트롤 도구 키트는 제공 된 `GetProxyForCurrentPopup()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="2c41a-124">The ASP.NET AJAX Control Toolkit offers the `GetProxyForCurrentPopup()` method.</span></span> <span data-ttu-id="2c41a-125">이 메서드가 반환 개체가 지 원하는 `Commit()` 다시 팝업 (컨트롤이 아님 메서드 호출을 트리거한!)를 발생 시킨 컨트롤에 값을 전송 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="2c41a-125">The object this method returns supports the `Commit()` method which sends a value back to the control that triggered the popup (not the control that triggered the method call!).</span></span> <span data-ttu-id="2c41a-126">다음 코드에서는 선택된 된 날짜에 대 한 인수로 `Commit()` 메서드, 텍스트 상자에 선택된 된 날짜를 다시 작성 하기 위해 코드:</span><span class="sxs-lookup"><span data-stu-id="2c41a-126">The following code provides the selected date as the argument for the `Commit()` method, causing the code to write the selected date back to the text box:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/samples/sample2.aspx)]

<span data-ttu-id="2c41a-127">이제 클릭할 때마다 달력 날짜 관련된 텍스트 상자에 선택 된 날짜가 나타납니다 날짜 선택 컨트롤을 만드는 현재 있습니다 많은 웹 사이트에서.</span><span class="sxs-lookup"><span data-stu-id="2c41a-127">Now whenever you click on a calendar date, the selected date appears in the associated text box, creating a date picker control that can currently be found on many websites.</span></span>


<span data-ttu-id="2c41a-128">[![입력란에 사용자가 클릭 하면 달력이 나타납니다.](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2c41a-128">[![The Calendar appears when the user clicks into the textbox](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image1.png)</span></span>

<span data-ttu-id="2c41a-129">입력란에 사용자가 클릭 하면 달력이 나타납니다 ([전체 크기 이미지를 보려면 클릭](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="2c41a-129">The Calendar appears when the user clicks into the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image3.png))</span></span>


<span data-ttu-id="2c41a-130">[![날짜를 클릭 하면 텍스트 상자에 전환](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="2c41a-130">[![Clicking on a date puts it in the textbox](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image4.png)</span></span>

<span data-ttu-id="2c41a-131">날짜를 클릭 하면 텍스트 상자에 전환 ([전체 크기 이미지를 보려면 클릭](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="2c41a-131">Clicking on a date puts it in the textbox ([Click to view full-size image](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2c41a-132">[이전](using-multiple-popup-controls-cs.md)
> [다음](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)</span><span class="sxs-lookup"><span data-stu-id="2c41a-132">[Previous](using-multiple-popup-controls-cs.md)
[Next](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)</span></span>
