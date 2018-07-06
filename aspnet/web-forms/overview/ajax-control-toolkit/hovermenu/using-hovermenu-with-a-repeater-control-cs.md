---
uid: web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
title: Repeater 컨트롤 (C#)에 HoverMenu 사용 | Microsoft Docs
author: wenz
description: 'AJAX Control Toolkit에 HoverMenu 컨트롤은 간단한 팝업 효과 제공 합니다: 팝업을 specifi에 표시 되는 요소 위로 마우스 포인터를 가져가면...'
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: e7700e7b-edc3-4183-a713-70e507cc7490
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: f3135eb52bab1550b1c89dd6ce62044640e80198
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37831999"
---
<a name="using-hovermenu-with-a-repeater-control-c"></a><span data-ttu-id="c6fb9-103">Repeater 컨트롤 (C#)에 HoverMenu 사용</span><span class="sxs-lookup"><span data-stu-id="c6fb9-103">Using HoverMenu with a Repeater Control (C#)</span></span>
====================
<span data-ttu-id="c6fb9-104">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="c6fb9-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="c6fb9-105">[코드를 다운로드](http://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="c6fb9-105">[Download Code](http://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)</span></span>

> <span data-ttu-id="c6fb9-106">AJAX Control Toolkit에 HoverMenu 컨트롤은 간단한 팝업 효과 제공 합니다: 지정된 된 위치에 팝업이 표시 되 요소 위로 마우스 포인터를 가져가면 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fb9-106">The HoverMenu control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="c6fb9-107">Repeater 내에서이 컨트롤을 사용 하는 것도 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fb9-107">It is also possible to use this control within a repeater.</span></span>


## <a name="overview"></a><span data-ttu-id="c6fb9-108">개요</span><span class="sxs-lookup"><span data-stu-id="c6fb9-108">Overview</span></span>

<span data-ttu-id="c6fb9-109">`HoverMenu` AJAX Control Toolkit 컨트롤 간단한 팝업 효과 제공: 지정된 된 위치에 팝업이 표시 되 요소 위로 마우스 포인터를 가져가면 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fb9-109">The `HoverMenu` control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="c6fb9-110">Repeater 내에서이 컨트롤을 사용 하는 것도 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fb9-110">It is also possible to use this control within a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="c6fb9-111">단계</span><span class="sxs-lookup"><span data-stu-id="c6fb9-111">Steps</span></span>

<span data-ttu-id="c6fb9-112">첫째, 데이터 소스는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fb9-112">First of all, a data source is required.</span></span> <span data-ttu-id="c6fb9-113">이 샘플에서는 AdventureWorks 데이터베이스 및 Microsoft SQL Server 2005 Express Edition을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fb9-113">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="c6fb9-114">데이터베이스 (express edition 포함)는 Visual Studio 설치의 선택적 부분이 며 아래에 있는 별도 다운로드로도 제공 됩니다 [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fb9-114">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="c6fb9-115">AdventureWorks 데이터베이스의 SQL Server 2005 샘플 및 예제 데이터베이스의 일부인 (에서 다운로드할 [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="c6fb9-115">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="c6fb9-116">데이터베이스를 설정 하는 가장 쉬운 방법은 Microsoft SQL Server Management Studio Express를 사용 하는 것 ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) 및 연결 된 `AdventureWorks.mdf` 데이터베이스 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c6fb9-116">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="c6fb9-117">이 샘플에서는 SQL Server 2005 Express Edition 인스턴스 라고 가정 `SQLEXPRESS` 웹 서버와 동일한 컴퓨터에 상주 하 고 기본 설정 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fb9-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="c6fb9-118">설정이 다른 경우에 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fb9-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="c6fb9-119">ASP.NET AJAX와 Control Toolkit의 기능을 활성화 하기 위해 합니다 `ScriptManager` 컨트롤 페이지의 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):</span><span class="sxs-lookup"><span data-stu-id="c6fb9-119">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample1.aspx)]

<span data-ttu-id="c6fb9-120">그런 다음 페이지에 데이터 소스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fb9-120">Then, add a data source to the page.</span></span> <span data-ttu-id="c6fb9-121">제한 된 양의 데이터를 사용 하려면만 선택 처음 5 개 항목을 AdventureWorks 데이터베이스의 Vendor 테이블의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fb9-121">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="c6fb9-122">Visual Studio 도우미를 데이터 소스를 만드는 데 사용 하는 경우 고려해 현재 버전의 버그로 테이블 이름 접두사 하지 않습니다 (`Vendor`)와 `Purchasing`합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fb9-122">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="c6fb9-123">다음 태그에서는 올바른 구문을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c6fb9-123">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample2.aspx)]

<span data-ttu-id="c6fb9-124">다음으로 모달 팝업으로 사용 되는 패널을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fb9-124">Next, add a panel which serves as the modal popup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample3.aspx)]

<span data-ttu-id="c6fb9-125">이제는 `HoverMenuExtender` 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6fb9-125">Now, the `HoverMenuExtender` comes into play.</span></span> <span data-ttu-id="c6fb9-126">반복기의 내 extender를 넣어야 있도록 데이터 소스의 모든 요소는 자체 팝업, `<ItemTemplate>` 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="c6fb9-126">So that every element in the data source gets its own popup, the extender must be put within the repeater's `<ItemTemplate>` section.</span></span> <span data-ttu-id="c6fb9-127">다음은 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="c6fb9-127">Here is the markup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample4.aspx)]

<span data-ttu-id="c6fb9-128">이제 오른쪽 팝업을 표시 하는 데이터 소스의 모든 항목 (`PopupPosition` 특성) 50 밀리초의 지연 후 (`PopDelay` 특성).</span><span class="sxs-lookup"><span data-stu-id="c6fb9-128">Now every item in the data source displays a popup to the right (`PopupPosition` attribute) after a delay of 50 milliseconds (`PopDelay` attribute).</span></span>


<span data-ttu-id="c6fb9-129">[![호버 메뉴 반복기의 각 항목 옆에 표시 됩니다.](using-hovermenu-with-a-repeater-control-cs/_static/image2.png)](using-hovermenu-with-a-repeater-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c6fb9-129">[![The hover menu appears next to each item in the repeater](using-hovermenu-with-a-repeater-control-cs/_static/image2.png)](using-hovermenu-with-a-repeater-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="c6fb9-130">반복기의 각 항목 옆에 표시 되는 메뉴 ([클릭 하 여 큰 이미지 보기](using-hovermenu-with-a-repeater-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="c6fb9-130">The hover menu appears next to each item in the repeater ([Click to view full-size image](using-hovermenu-with-a-repeater-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="c6fb9-131">다음</span><span class="sxs-lookup"><span data-stu-id="c6fb9-131">Next</span></span>](using-hovermenu-with-a-repeater-control-vb.md)
