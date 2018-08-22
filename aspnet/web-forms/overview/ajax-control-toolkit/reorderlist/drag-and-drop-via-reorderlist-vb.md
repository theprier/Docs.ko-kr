---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-vb
title: 끌어서 놓기 (VB) ReorderList를 통해 | Microsoft Docs
author: wenz
description: /data-access/tutorials/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 848e6bcf-4c3f-4d14-974d-e45b9444ab79
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 12c5aa60aa6bb71c99e267a1a71b40ed718df8cf
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829439"
---
<a name="drag-and-drop-via-reorderlist-vb"></a><span data-ttu-id="4dafe-103">끌어서 놓기 (VB) ReorderList 통해</span><span class="sxs-lookup"><span data-stu-id="4dafe-103">Drag and Drop via ReorderList (VB)</span></span>
====================
<span data-ttu-id="4dafe-104">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="4dafe-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="4dafe-105">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="4dafe-105">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5VB.pdf)</span></span>

> <span data-ttu-id="4dafe-106">ReorderList 컨트롤이 AJAX Control Toolkit에서 끌어서 놓기를 통해 사용자에 의해 다시 정렬할 수 있는 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dafe-106">The ReorderList control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="4dafe-107">현재 순서 목록에는 서버에서 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dafe-107">The current order of the list shall be persisted on the server.</span></span>


## <a name="overview"></a><span data-ttu-id="4dafe-108">개요</span><span class="sxs-lookup"><span data-stu-id="4dafe-108">Overview</span></span>

<span data-ttu-id="4dafe-109">`ReorderList` AJAX Control Toolkit 컨트롤 끌어서 놓기를 통해 사용자에 의해 다시 정렬할 수 있는 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dafe-109">The `ReorderList` control in the AJAX Control Toolkit provides a list that can be reordered by the user via drag and drop.</span></span> <span data-ttu-id="4dafe-110">현재 순서 목록에는 서버에서 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dafe-110">The current order of the list shall be persisted on the server.</span></span>

## <a name="steps"></a><span data-ttu-id="4dafe-111">단계</span><span class="sxs-lookup"><span data-stu-id="4dafe-111">Steps</span></span>

<span data-ttu-id="4dafe-112">`ReorderList` 컨트롤 목록에는 데이터베이스에서 바인딩 데이터를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dafe-112">The `ReorderList` control supports binding data from a database to the list.</span></span> <span data-ttu-id="4dafe-113">무엇 보다도, 데이터 저장소 목록 요소 순서 변경 내용 쓰기도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4dafe-113">Best of all, it also supports writing changes to the order of the list element back to the data store.</span></span>

<span data-ttu-id="4dafe-114">이 샘플에서는 데이터 저장소로 Microsoft SQL Server 2005 Express Edition을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dafe-114">This sample uses Microsoft SQL Server 2005 Express Edition as the data store.</span></span> <span data-ttu-id="4dafe-115">Express edition을 포함 하는 Visual Studio 설치에서 선택적 (및 사용 가능한) 부분은 데이터베이스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dafe-115">The database is an optional (and free) part of a Visual Studio installation, including express edition.</span></span> <span data-ttu-id="4dafe-116">아래에서 개별 다운로드로 제공 됩니다 [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)합니다.</span><span class="sxs-lookup"><span data-stu-id="4dafe-116">It is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="4dafe-117">이 샘플에서는 SQL Server 2005 Express Edition 인스턴스 라고 가정 `SQLEXPRESS` 웹 서버와 동일한 컴퓨터에 상주 하 고 기본 설정 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dafe-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="4dafe-118">설정이 다른 경우에 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dafe-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="4dafe-119">데이터베이스를 설정 하는 가장 쉬운 방법은 Microsoft SQL Server Management Studio Express를 사용 하는 것 ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span><span class="sxs-lookup"><span data-stu-id="4dafe-119">The easiest way to set up the database is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ).</span></span> <span data-ttu-id="4dafe-120">서버에 연결을 두 번 클릭 `Databases` 새 데이터베이스를 만듭니다 (마우스 오른쪽 단추로 `New Database`) 이라는 `Tutorials`합니다.</span><span class="sxs-lookup"><span data-stu-id="4dafe-120">Connect to the server, double-click on `Databases` and create a new database (right-click and choose `New Database`) called `Tutorials`.</span></span>

<span data-ttu-id="4dafe-121">이 데이터베이스에서 라는 새 테이블을 만듭니다 `AJAX` 다음 4 개의 열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dafe-121">In this database, create a new table called `AJAX` with the following four columns:</span></span>

- <span data-ttu-id="4dafe-122">`id` (기본 키, 정수 id를 NULL이 아님)</span><span class="sxs-lookup"><span data-stu-id="4dafe-122">`id` (primary key, integer, identity, not NULL)</span></span>
- <span data-ttu-id="4dafe-123">`char` (char(1), NULL)</span><span class="sxs-lookup"><span data-stu-id="4dafe-123">`char` (char(1), NULL)</span></span>
- <span data-ttu-id="4dafe-124">`description` (varchar(50), NULL)</span><span class="sxs-lookup"><span data-stu-id="4dafe-124">`description` (varchar(50), NULL)</span></span>
- <span data-ttu-id="4dafe-125">`position` (int, NULL)</span><span class="sxs-lookup"><span data-stu-id="4dafe-125">`position` (int, NULL)</span></span>


<span data-ttu-id="4dafe-126">[![AJAX 테이블의 레이아웃](drag-and-drop-via-reorderlist-vb/_static/image2.png)](drag-and-drop-via-reorderlist-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4dafe-126">[![The layout of the AJAX table](drag-and-drop-via-reorderlist-vb/_static/image2.png)](drag-and-drop-via-reorderlist-vb/_static/image1.png)</span></span>

<span data-ttu-id="4dafe-127">AJAX 테이블의 레이아웃 ([클릭 하 여 큰 이미지 보기](drag-and-drop-via-reorderlist-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="4dafe-127">The layout of the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-vb/_static/image3.png))</span></span>


<span data-ttu-id="4dafe-128">다음으로 두 가지 값을 사용 하 여 테이블을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="4dafe-128">Next, fill the table with a couple of values.</span></span> <span data-ttu-id="4dafe-129">`position` 열 요소는 정렬 순서를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dafe-129">Note that the `position` column holds the sort order of the elements.</span></span>


<span data-ttu-id="4dafe-130">[![AJAX 테이블의 초기 데이터](drag-and-drop-via-reorderlist-vb/_static/image5.png)](drag-and-drop-via-reorderlist-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="4dafe-130">[![The initial data in the AJAX table](drag-and-drop-via-reorderlist-vb/_static/image5.png)](drag-and-drop-via-reorderlist-vb/_static/image4.png)</span></span>

<span data-ttu-id="4dafe-131">AJAX 테이블의 초기 데이터 ([클릭 하 여 큰 이미지 보기](drag-and-drop-via-reorderlist-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="4dafe-131">The initial data in the AJAX table ([Click to view full-size image](drag-and-drop-via-reorderlist-vb/_static/image6.png))</span></span>


<span data-ttu-id="4dafe-132">생성 하는 데 필요한 다음 단계는 `SqlDataSource` 새 데이터베이스 및 해당 테이블을 사용 하 여 통신을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dafe-132">The next step requires to generate an `SqlDataSource` control to communicate with the new database and its table.</span></span> <span data-ttu-id="4dafe-133">데이터 원본 지원 해야 합니다 `SELECT` 및 `UPDATE` SQL 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4dafe-133">The data source must support the `SELECT` and `UPDATE` SQL commands.</span></span> <span data-ttu-id="4dafe-134">목록 요소의 순서를 나중에 변경 하는 경우는 `ReorderList` 컨트롤 데이터 소스에 두 값을 자동으로 전송 `Update` 명령: 새 위치와 요소의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="4dafe-134">When the order of the list elements is later changed, the `ReorderList` control automatically submits two values to the data source's `Update` command: the new position and the ID of the element.</span></span> <span data-ttu-id="4dafe-135">따라서 데이터 원본 요구는 `<UpdateParameters>` 이 두 값에 대 한 섹션:</span><span class="sxs-lookup"><span data-stu-id="4dafe-135">Therefore, the data source needs an `<UpdateParameters>` section for these two values:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample1.aspx)]

<span data-ttu-id="4dafe-136">`ReorderList` 제어는 다음 특성을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dafe-136">The `ReorderList` control needs to set the following attributes:</span></span>

- <span data-ttu-id="4dafe-137">`AllowReorder`: 목록 항목 수 다시 배열할 수 여부</span><span class="sxs-lookup"><span data-stu-id="4dafe-137">`AllowReorder`: Whether the list items may be rearranged</span></span>
- <span data-ttu-id="4dafe-138">`DataSourceID`데이터 원본 ID:</span><span class="sxs-lookup"><span data-stu-id="4dafe-138">`DataSourceID`: The ID of the data source</span></span>
- <span data-ttu-id="4dafe-139">`DataKeyField`데이터 원본에 기본 키 열 이름:</span><span class="sxs-lookup"><span data-stu-id="4dafe-139">`DataKeyField`: The name of the primary key column in the data source</span></span>
- <span data-ttu-id="4dafe-140">`SortOrderField`목록 항목에 대 한 정렬 순서를 제공 하는 데이터 원본 열:</span><span class="sxs-lookup"><span data-stu-id="4dafe-140">`SortOrderField`: The data source column that provides the sort order for the list items</span></span>

<span data-ttu-id="4dafe-141">에 `<DragHandleTemplate>` 고 `<ItemTemplate>` 섹션 목록의 레이아웃 세밀 하 게 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dafe-141">In the `<DragHandleTemplate>` and `<ItemTemplate>` sections, the layout of the list can be fine-tuned.</span></span> <span data-ttu-id="4dafe-142">데이터 바인딩 가능 또한를 사용 하 여는 `Eval()` 메서드를 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dafe-142">Also, databinding is possible using the `Eval()` method, as seen here:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample2.aspx)]

<span data-ttu-id="4dafe-143">다음 CSS 스타일 정보 (에서 참조 되는 `<DragHandleTemplate>` 섹션을 `ReorderList` 컨트롤) 끌기 핸들 위로 이동할 때 마우스 포인터를 적절 하 게 변경 하 게:</span><span class="sxs-lookup"><span data-stu-id="4dafe-143">The following CSS style information (referenced in the `<DragHandleTemplate>` section of the `ReorderList` control) makes sure that the mouse pointer changes appropriately when it hovers over the drag handle:</span></span>

[!code-css[Main](drag-and-drop-via-reorderlist-vb/samples/sample3.css)]

<span data-ttu-id="4dafe-144">마지막으로 `ScriptManager` 컨트롤이 페이지에 대 한 ASP.NET AJAX를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dafe-144">Finally, a `ScriptManager` control initializes ASP.NET AJAX for the page:</span></span>

[!code-aspx[Main](drag-and-drop-via-reorderlist-vb/samples/sample4.aspx)]

<span data-ttu-id="4dafe-145">브라우저에서이 예제를 실행 하 고 잠시 목록 항목을 다시 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dafe-145">Run this example in the browser and rearrange the list items a bit.</span></span> <span data-ttu-id="4dafe-146">그런 다음 페이지를 다시 로드 하거나 데이터베이스를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dafe-146">Then, reload the page and/or have a look at the database.</span></span> <span data-ttu-id="4dafe-147">변경된 위치를 유지 관리 되었는지 및 값을 기준으로 반영 됩니다는 `position` 데이터베이스에 열 태그를 사용 하 여 방금 모든 코드 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dafe-147">The altered positions have been maintained and are also reflected by the values in the `position` column in the database and that all without any code, just by using markup.</span></span>


<span data-ttu-id="4dafe-148">[![데이터가 새 목록 항목 순서에 따라 데이터베이스 변경](drag-and-drop-via-reorderlist-vb/_static/image8.png)](drag-and-drop-via-reorderlist-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="4dafe-148">[![The data in the database changes according to the new list item order](drag-and-drop-via-reorderlist-vb/_static/image8.png)](drag-and-drop-via-reorderlist-vb/_static/image7.png)</span></span>

<span data-ttu-id="4dafe-149">새 목록에 따라 데이터베이스 변경에서의 데이터 항목 순서 ([클릭 하 여 큰 이미지 보기](drag-and-drop-via-reorderlist-vb/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="4dafe-149">The data in the database changes according to the new list item order ([Click to view full-size image](drag-and-drop-via-reorderlist-vb/_static/image9.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="4dafe-150">이전</span><span class="sxs-lookup"><span data-stu-id="4dafe-150">Previous</span></span>](using-postbacks-with-reorderlist-vb.md)
