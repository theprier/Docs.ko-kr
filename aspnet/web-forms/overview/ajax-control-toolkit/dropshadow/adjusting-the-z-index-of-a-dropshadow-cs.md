---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
title: DropShadow (C#)의 Z 인덱스를 조정 | Microsoft Docs
author: wenz
description: 들어의 DropShadow 컨트롤 그림자가 있는 패널을 확장합니다. 그러나이 그림자 insta에 대 한 다른 컨트롤과 경우에 따라 충돌 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 14133833-e518-4347-87b9-6b6f71f14a77
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
msc.type: authoredcontent
ms.openlocfilehash: 82add8427c8e574b213b67315e69bb4c28846095
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30868284"
---
<a name="adjusting-the-z-index-of-a-dropshadow-c"></a><span data-ttu-id="8b584-104">DropShadow (C#)의 Z 인덱스를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="8b584-104">Adjusting the Z-Index of a DropShadow (C#)</span></span>
====================
<span data-ttu-id="8b584-105">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="8b584-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="8b584-106">[코드를 다운로드](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="8b584-106">[Download Code](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1CS.pdf)</span></span>

> <span data-ttu-id="8b584-107">들어의 DropShadow 컨트롤 그림자가 있는 패널을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="8b584-107">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="8b584-108">그러나이 그림자 예를 들어 ASP.NET 메뉴 컨트롤이 다른 컨트롤과 경우에 따라 충돌 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b584-108">However this shadow sometimes conflicts with other controls, for instance the ASP.NET Menu control.</span></span> <span data-ttu-id="8b584-109">때 메뉴 항목을 팝업, 드롭 그림자 뒤에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b584-109">When a menu entry pops up, it appears behind the drop shadow.</span></span>


## <a name="overview"></a><span data-ttu-id="8b584-110">개요</span><span class="sxs-lookup"><span data-stu-id="8b584-110">Overview</span></span>

<span data-ttu-id="8b584-111">들어의 DropShadow 컨트롤 그림자가 있는 패널을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="8b584-111">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="8b584-112">그러나이 그림자 예를 들어 ASP.NET 메뉴 컨트롤이 다른 컨트롤과 경우에 따라 충돌 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b584-112">However this shadow sometimes conflicts with other controls, for instance the ASP.NET Menu control.</span></span> <span data-ttu-id="8b584-113">때 메뉴 항목을 팝업, 드롭 그림자 뒤에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b584-113">When a menu entry pops up, it appears behind the drop shadow.</span></span>

## <a name="steps"></a><span data-ttu-id="8b584-114">단계</span><span class="sxs-lookup"><span data-stu-id="8b584-114">Steps</span></span>

<span data-ttu-id="8b584-115">패널에 표시 되도록 효과 대 한 충분 한 텍스트에 포함 하도록 충분 한 텍스트가 포함 된 패널 자체를 코드 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b584-115">The code commences with the Panel itself, containing enough text so that the panel contains enough text for the effect to be visible:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample1.aspx)]

<span data-ttu-id="8b584-116">다른 패널 바로 앞에 삽입 된 `panelShadow` 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="8b584-116">Another panel is placed directly before the `panelShadow` panel.</span></span> <span data-ttu-id="8b584-117">메뉴 항목을 통해 표시 되도록 가로 방향으로 메뉴를 포함 (나 비슷한: 아래)는 `dropShadow` 패널):</span><span class="sxs-lookup"><span data-stu-id="8b584-117">It contains a menu with horizontal orientation so that menu entries appear over (or rather: under) the `dropShadow` panel):</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample2.aspx)]

<span data-ttu-id="8b584-118">그런 다음 `DropShadowExtender` 확장에 추가 되는 `panelShadow` 그림자 효과와 패널:</span><span class="sxs-lookup"><span data-stu-id="8b584-118">Then, the `DropShadowExtender` is added to extend the `panelShadow` panel with a drop shadow effect:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample3.aspx)]

<span data-ttu-id="8b584-119">마지막으로, ASP.NET AJAX `ScriptManager` 컨트롤을 사용 하면 제어 도구 키트에서 실행 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b584-119">Finally, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample4.aspx)]

<span data-ttu-id="8b584-120">이 스크립트를 실행할 때 메뉴 항목 패널 아래에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8b584-120">When you run this script, the menu entries appear underneath the panel.</span></span> <span data-ttu-id="8b584-121">그러나 메뉴는 CSS 클래스를 사용 하는 `panel` 만 있는 요소를 다른 패널 앞에 표시 하려면 다음 두 가지를 정의 하려면:</span><span class="sxs-lookup"><span data-stu-id="8b584-121">However the menu uses the CSS class `panel` where you just have to define two things to make elements appear in front of the other panel:</span></span>

- <span data-ttu-id="8b584-122">상대 위치 지정</span><span class="sxs-lookup"><span data-stu-id="8b584-122">Relative positioning</span></span>
- <span data-ttu-id="8b584-123">양수 z-인덱스</span><span class="sxs-lookup"><span data-stu-id="8b584-123">A positive z-index</span></span>

[!code-css[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample5.css)]

<span data-ttu-id="8b584-124">그런 다음 `DropShadowExtender` 컨트롤 메뉴 컨트롤에 더 이상 충돌 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8b584-124">Then, the `DropShadowExtender` control does not conflict any longer with the Menu control.</span></span>


<span data-ttu-id="8b584-125">[![이전: 메뉴 항목은 표시](adjusting-the-z-index-of-a-dropshadow-cs/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8b584-125">[![Before: The menu entry is not visible](adjusting-the-z-index-of-a-dropshadow-cs/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image1.png)</span></span>

<span data-ttu-id="8b584-126">이전: 메뉴 항목 보이지 않으면 ([전체 크기 이미지를 보려면 클릭](adjusting-the-z-index-of-a-dropshadow-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="8b584-126">Before: The menu entry is not visible ([Click to view full-size image](adjusting-the-z-index-of-a-dropshadow-cs/_static/image3.png))</span></span>


<span data-ttu-id="8b584-127">[![이후: 메뉴 항목 표시](adjusting-the-z-index-of-a-dropshadow-cs/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="8b584-127">[![After: The menu entry appears](adjusting-the-z-index-of-a-dropshadow-cs/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image4.png)</span></span>

<span data-ttu-id="8b584-128">이후: 메뉴 항목 표시 ([전체 크기 이미지를 보려면 클릭](adjusting-the-z-index-of-a-dropshadow-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="8b584-128">After: The menu entry appears ([Click to view full-size image](adjusting-the-z-index-of-a-dropshadow-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="8b584-129">다음</span><span class="sxs-lookup"><span data-stu-id="8b584-129">Next</span></span>](manipulating-dropshadow-properties-from-client-code-cs.md)
