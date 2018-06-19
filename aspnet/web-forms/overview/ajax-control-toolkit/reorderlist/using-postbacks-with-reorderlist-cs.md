---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-cs
title: 포스트백을 사용 하 여 ReorderList (C#)와 | Microsoft Docs
author: wenz
description: 끌어 놓기를 통해 사용자가 다시 정렬할 수 있는 목록을 제공 하는 들어에서 ReorderList 컨트롤입니다. 목록 순서를 변경할 때마다 po...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 70d5d106-b547-442c-a7fd-3492b3e3d646
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-cs
msc.type: authoredcontent
ms.openlocfilehash: ed01c30c0721c8f1cd8ccb3fea0735ea8fa4f0a1
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30871729"
---
<a name="using-postbacks-with-reorderlist-c"></a><span data-ttu-id="28efa-104">포스트백 ReorderList (C#) 사용</span><span class="sxs-lookup"><span data-stu-id="28efa-104">Using Postbacks with ReorderList (C#)</span></span>
====================
<span data-ttu-id="28efa-105">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="28efa-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="28efa-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="28efa-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4CS.pdf)</span></span>

> <span data-ttu-id="28efa-107">끌어 놓기를 통해 사용자가 다시 정렬할 수 있는 목록을 제공 하는 들어에서 ReorderList 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="28efa-107">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="28efa-108">목록 순서를 변경할 때마다이 포스트백은 변경의 서버를 알립니다.</span><span class="sxs-lookup"><span data-stu-id="28efa-108">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>


## <a name="overview"></a><span data-ttu-id="28efa-109">개요</span><span class="sxs-lookup"><span data-stu-id="28efa-109">Overview</span></span>

<span data-ttu-id="28efa-110">`ReorderList` 들어에서 컨트롤 끌어 놓기를 통해 사용자가 다시 정렬할 수 있는 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="28efa-110">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="28efa-111">목록 순서를 변경할 때마다이 포스트백은 변경의 서버를 알립니다.</span><span class="sxs-lookup"><span data-stu-id="28efa-111">Whenever the list is reordered, a postback shall inform the server of the change.</span></span>

## <a name="steps"></a><span data-ttu-id="28efa-112">단계</span><span class="sxs-lookup"><span data-stu-id="28efa-112">Steps</span></span>

<span data-ttu-id="28efa-113">에 대 한 여러 가능한 데이터 소스는 `ReorderList` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="28efa-113">There are several possible data sources for the `ReorderList` control.</span></span> <span data-ttu-id="28efa-114">하나 사용 하는 `XmlDataSource` 제어:</span><span class="sxs-lookup"><span data-stu-id="28efa-114">One is to use an `XmlDataSource` control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample1.aspx)]

<span data-ttu-id="28efa-115">이 XML을 바인딩하는 데는 `ReorderList` 제어를 사용 하도록 설정한 포스트백을 다음과 같은 특성을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28efa-115">In order to bind this XML to a `ReorderList` control and enable postbacks, the following attributes must be set:</span></span>

- <span data-ttu-id="28efa-116">`DataSourceID`: 데이터 원본 ID</span><span class="sxs-lookup"><span data-stu-id="28efa-116">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="28efa-117">`SortOrderField`정렬 기준: 속성</span><span class="sxs-lookup"><span data-stu-id="28efa-117">`SortOrderField`: The property to sort by</span></span>
- <span data-ttu-id="28efa-118">`AllowReorder`: 사용자는 목록 요소를 다시 정렬할 수 있도록 여부</span><span class="sxs-lookup"><span data-stu-id="28efa-118">`AllowReorder`: Whether to allow the user to reorder the list elements</span></span>
- <span data-ttu-id="28efa-119">`PostBackOnReorder`: 목록 다시 정렬 될 때마다 다시 게시를 만들려면 여부</span><span class="sxs-lookup"><span data-stu-id="28efa-119">`PostBackOnReorder`: Whether to create a postback whenever the list is rearranged</span></span>

<span data-ttu-id="28efa-120">컨트롤에 대 한 적절 한 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="28efa-120">Here is the appropriate markup for the control:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample2.aspx)]

<span data-ttu-id="28efa-121">내에서 `ReorderList` 컨트롤, 데이터 원본의 특정 데이터를 사용 하 여 바인딩할 수 있습니다는 `Eval()` 메서드:</span><span class="sxs-lookup"><span data-stu-id="28efa-121">Within the `ReorderList` control, specific data from the data source may be bound using the `Eval()` method:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample3.aspx)]

<span data-ttu-id="28efa-122">페이지에서 임의의 위치에서 마지막 다시 정렬 발생 했을 때 레이블을 정보가 보관 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28efa-122">At an arbitrary position on the page, a label will hold the information when the last reordering occurred:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample4.aspx)]

<span data-ttu-id="28efa-123">이 레이블은 포스트백을 처리 하는 서버 쪽 코드의 텍스트도 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="28efa-123">This label is filled with text in the server-side code, handling the postback:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample5.aspx)]

<span data-ttu-id="28efa-124">마지막으로, ASP.NET AJAX 및 제어 Toolkit의 기능을 활성화 하는 데는 `ScriptManager` 페이지에 컨트롤을 배치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28efa-124">Finally, in order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put on the page:</span></span>

[!code-aspx[Main](using-postbacks-with-reorderlist-cs/samples/sample6.aspx)]


<span data-ttu-id="28efa-125">[![포스트백을 트리거합니다 각 순서 변경](using-postbacks-with-reorderlist-cs/_static/image2.png)](using-postbacks-with-reorderlist-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="28efa-125">[![Each reordering triggers a postback](using-postbacks-with-reorderlist-cs/_static/image2.png)](using-postbacks-with-reorderlist-cs/_static/image1.png)</span></span>

<span data-ttu-id="28efa-126">포스트백 트리거합니다 각 순서 변경 ([전체 크기 이미지를 보려면 클릭](using-postbacks-with-reorderlist-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="28efa-126">Each reordering triggers a postback ([Click to view full-size image](using-postbacks-with-reorderlist-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="28efa-127">다음</span><span class="sxs-lookup"><span data-stu-id="28efa-127">Next</span></span>](drag-and-drop-via-reorderlist-cs.md)
