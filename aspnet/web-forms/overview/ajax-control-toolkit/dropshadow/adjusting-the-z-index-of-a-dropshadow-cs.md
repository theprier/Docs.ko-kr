---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
title: (C#) DropShadow의 Z-인덱스 조정 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit에서 DropShadow 컨트롤 그림자를 사용 하 여 패널을 확장합니다. 그러나이 섀도 경우에 따라 설치에 대 한 다른 컨트롤을 사용 하 여 충돌 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 14133833-e518-4347-87b9-6b6f71f14a77
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
msc.type: authoredcontent
ms.openlocfilehash: 22732bc44a56819a2ec73346dc32659d027eaee0
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37369572"
---
<a name="adjusting-the-z-index-of-a-dropshadow-c"></a><span data-ttu-id="b88ff-104">(C#) DropShadow의 Z-인덱스 조정</span><span class="sxs-lookup"><span data-stu-id="b88ff-104">Adjusting the Z-Index of a DropShadow (C#)</span></span>
====================
<span data-ttu-id="b88ff-105">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="b88ff-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="b88ff-106">[코드를 다운로드](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="b88ff-106">[Download Code](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1CS.pdf)</span></span>

> <span data-ttu-id="b88ff-107">AJAX Control Toolkit에서 DropShadow 컨트롤 그림자를 사용 하 여 패널을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="b88ff-107">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="b88ff-108">그러나이 섀도 ASP.NET Menu 컨트롤 예를 들어 다른 컨트롤과 경우에 따라 충돌 합니다.</span><span class="sxs-lookup"><span data-stu-id="b88ff-108">However this shadow sometimes conflicts with other controls, for instance the ASP.NET Menu control.</span></span> <span data-ttu-id="b88ff-109">때 메뉴 항목 팝업 뒤에 그림자 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b88ff-109">When a menu entry pops up, it appears behind the drop shadow.</span></span>


## <a name="overview"></a><span data-ttu-id="b88ff-110">개요</span><span class="sxs-lookup"><span data-stu-id="b88ff-110">Overview</span></span>

<span data-ttu-id="b88ff-111">AJAX Control Toolkit에서 DropShadow 컨트롤 그림자를 사용 하 여 패널을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="b88ff-111">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="b88ff-112">그러나이 섀도 ASP.NET Menu 컨트롤 예를 들어 다른 컨트롤과 경우에 따라 충돌 합니다.</span><span class="sxs-lookup"><span data-stu-id="b88ff-112">However this shadow sometimes conflicts with other controls, for instance the ASP.NET Menu control.</span></span> <span data-ttu-id="b88ff-113">때 메뉴 항목 팝업 뒤에 그림자 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b88ff-113">When a menu entry pops up, it appears behind the drop shadow.</span></span>

## <a name="steps"></a><span data-ttu-id="b88ff-114">단계</span><span class="sxs-lookup"><span data-stu-id="b88ff-114">Steps</span></span>

<span data-ttu-id="b88ff-115">코드 표시 되도록 효과 대 한 충분 한 텍스트를 포함 하는 패널 수 있도록 충분 한 텍스트가 포함 된 패널 자체를 사용 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b88ff-115">The code commences with the Panel itself, containing enough text so that the panel contains enough text for the effect to be visible:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample1.aspx)]

<span data-ttu-id="b88ff-116">다른 패널 바로 앞에 삽입 된 `panelShadow` 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="b88ff-116">Another panel is placed directly before the `panelShadow` panel.</span></span> <span data-ttu-id="b88ff-117">메뉴 항목 위에 나타나도록 가로 방향으로 메뉴가 포함 (또는 대신: 아래)를 `dropShadow` 패널):</span><span class="sxs-lookup"><span data-stu-id="b88ff-117">It contains a menu with horizontal orientation so that menu entries appear over (or rather: under) the `dropShadow` panel):</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample2.aspx)]

<span data-ttu-id="b88ff-118">그런 다음, `DropShadowExtender` 확장에 추가 되는 `panelShadow` 그림자 효과 사용 하 여 패널:</span><span class="sxs-lookup"><span data-stu-id="b88ff-118">Then, the `DropShadowExtender` is added to extend the `panelShadow` panel with a drop shadow effect:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample3.aspx)]

<span data-ttu-id="b88ff-119">마지막으로 ASP.NET AJAX `ScriptManager` 제어 하려면 컨트롤 도구 키트를 사용 하면:</span><span class="sxs-lookup"><span data-stu-id="b88ff-119">Finally, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample4.aspx)]

<span data-ttu-id="b88ff-120">이 스크립트를 실행 하면 메뉴 항목 패널 아래에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b88ff-120">When you run this script, the menu entries appear underneath the panel.</span></span> <span data-ttu-id="b88ff-121">하지만 메뉴는 CSS 클래스를 사용 `panel` 만 있는 두 가지 다른 패널 앞에 표시 되는 요소를 정의 하려면:</span><span class="sxs-lookup"><span data-stu-id="b88ff-121">However the menu uses the CSS class `panel` where you just have to define two things to make elements appear in front of the other panel:</span></span>

- <span data-ttu-id="b88ff-122">상대 위치</span><span class="sxs-lookup"><span data-stu-id="b88ff-122">Relative positioning</span></span>
- <span data-ttu-id="b88ff-123">양의 z-인덱스</span><span class="sxs-lookup"><span data-stu-id="b88ff-123">A positive z-index</span></span>

[!code-css[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample5.css)]

<span data-ttu-id="b88ff-124">그런 다음, `DropShadowExtender` 컨트롤 메뉴 컨트롤을 사용 하 여 더 이상 충돌 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b88ff-124">Then, the `DropShadowExtender` control does not conflict any longer with the Menu control.</span></span>


<span data-ttu-id="b88ff-125">[![이전: 메뉴 항목은 표시](adjusting-the-z-index-of-a-dropshadow-cs/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b88ff-125">[![Before: The menu entry is not visible](adjusting-the-z-index-of-a-dropshadow-cs/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image1.png)</span></span>

<span data-ttu-id="b88ff-126">이전: 메뉴 항목 표시 되지 않습니다 ([클릭 하 여 큰 이미지 보기](adjusting-the-z-index-of-a-dropshadow-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="b88ff-126">Before: The menu entry is not visible ([Click to view full-size image](adjusting-the-z-index-of-a-dropshadow-cs/_static/image3.png))</span></span>


<span data-ttu-id="b88ff-127">[![메뉴 항목을 표시 하는 이후:](adjusting-the-z-index-of-a-dropshadow-cs/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="b88ff-127">[![After: The menu entry appears](adjusting-the-z-index-of-a-dropshadow-cs/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image4.png)</span></span>

<span data-ttu-id="b88ff-128">이후: 메뉴 항목 표시 ([클릭 하 여 큰 이미지 보기](adjusting-the-z-index-of-a-dropshadow-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="b88ff-128">After: The menu entry appears ([Click to view full-size image](adjusting-the-z-index-of-a-dropshadow-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="b88ff-129">다음</span><span class="sxs-lookup"><span data-stu-id="b88ff-129">Next</span></span>](manipulating-dropshadow-properties-from-client-code-cs.md)
