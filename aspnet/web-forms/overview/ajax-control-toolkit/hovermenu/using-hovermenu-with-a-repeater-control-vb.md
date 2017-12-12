---
uid: web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-vb
title: "반복기 컨트롤 (VB) HoverMenu 사용 | Microsoft Docs"
author: wenz
description: "에 들어 HoverMenu 컨트롤은 간단한 팝업 효과 제공:는 specifi에 팝업이 표시 되는 마우스 포인터가 요소 위로 가져가면..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 7f07c112-cd4f-4427-9699-57cfab2791fd
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 77759afe00f341e15ee8e0f52a469d3b7c08ea89
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="using-hovermenu-with-a-repeater-control-vb"></a><span data-ttu-id="91da9-103">반복기 컨트롤 (VB) HoverMenu 사용</span><span class="sxs-lookup"><span data-stu-id="91da9-103">Using HoverMenu with a Repeater Control (VB)</span></span>
====================
<span data-ttu-id="91da9-104">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="91da9-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="91da9-105">[코드를 다운로드](http://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="91da9-105">[Download Code](http://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1VB.pdf)</span></span>

> <span data-ttu-id="91da9-106">에 들어 HoverMenu 컨트롤은 간단한 팝업 효과 제공: 지정된 된 위치에서 팝업이 표시 되는 마우스 포인터가 요소 위로 가져가면 합니다.</span><span class="sxs-lookup"><span data-stu-id="91da9-106">The HoverMenu control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="91da9-107">도 한 반복기 내에서이 컨트롤을 사용 하는 것이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="91da9-107">It is also possible to use this control within a repeater.</span></span>


## <a name="overview"></a><span data-ttu-id="91da9-108">개요</span><span class="sxs-lookup"><span data-stu-id="91da9-108">Overview</span></span>

<span data-ttu-id="91da9-109">`HoverMenu` 들어에서 컨트롤은 간단한 팝업 효과 제공: 지정된 된 위치에서 팝업이 표시 되는 마우스 포인터가 요소 위로 가져가면 합니다.</span><span class="sxs-lookup"><span data-stu-id="91da9-109">The `HoverMenu` control in the AJAX Control Toolkit provides a simple popup effect: When the mouse pointer hovers over an element, a popup appears at a specified position.</span></span> <span data-ttu-id="91da9-110">도 한 반복기 내에서이 컨트롤을 사용 하는 것이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="91da9-110">It is also possible to use this control within a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="91da9-111">단계</span><span class="sxs-lookup"><span data-stu-id="91da9-111">Steps</span></span>

<span data-ttu-id="91da9-112">첫째, 데이터 소스는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="91da9-112">First of all, a data source is required.</span></span> <span data-ttu-id="91da9-113">이 샘플에서는 AdventureWorks 데이터베이스 및 Microsoft SQL Server 2005 Express Edition을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="91da9-113">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="91da9-114">데이터베이스 (express edition 포함)는 Visual Studio 설치의 선택적 부분이 며에서 별도 다운로드로 제공 됩니다 [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)합니다.</span><span class="sxs-lookup"><span data-stu-id="91da9-114">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="91da9-115">AdventureWorks 데이터베이스의 SQL Server 2005 예제 및 예제 데이터베이스의 일부인 (다운로드에서 [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="91da9-115">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="91da9-116">Microsoft SQL Server Management Studio Express를 사용 하는 데이터베이스를 설정 하는 가장 쉬운 방법은 ([https://www.microsoft.com/downloads/details.aspx? FamilyID c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796 =&amp;4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) 및 연결 된 `AdventureWorks.mdf` 데이터베이스 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="91da9-116">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="91da9-117">이 샘플에 대 한 SQL Server 2005 Express Edition 인스턴스 라고 가정 `SQLEXPRESS` 웹 서버와 동일한 컴퓨터에 상주 하 고 기본 설정 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="91da9-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="91da9-118">설정에 다른 경우 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91da9-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="91da9-119">ASP.NET AJAX 및 제어 Toolkit의 기능을 활성화 하는 데는 `ScriptManager` 제어 페이지에서 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):</span><span class="sxs-lookup"><span data-stu-id="91da9-119">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample1.aspx)]

<span data-ttu-id="91da9-120">페이지 데이터 소스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="91da9-120">Then, add a data source to the page.</span></span> <span data-ttu-id="91da9-121">제한 된 양의 데이터를 사용 하려면만 선택 처음 5 개 항목 AdventureWorks 데이터베이스의 Vendor 테이블에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91da9-121">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="91da9-122">Visual Studio 도우미를 데이터 소스를 만드는 데 사용 하는 경우 유의 현재 버전의 버그 테이블 이름이 붙지 않습니다 (`Vendor`)와 `Purchasing`합니다.</span><span class="sxs-lookup"><span data-stu-id="91da9-122">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="91da9-123">다음 태그를 올바른 구문을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="91da9-123">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample2.aspx)]

<span data-ttu-id="91da9-124">다음으로 모달 팝업으로 사용 되는 패널을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="91da9-124">Next, add a panel which serves as the modal popup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample3.aspx)]

<span data-ttu-id="91da9-125">이제는 `HoverMenuExtender` 을 발휘 합니다.</span><span class="sxs-lookup"><span data-stu-id="91da9-125">Now, the `HoverMenuExtender` comes into play.</span></span> <span data-ttu-id="91da9-126">반복기의 내 extender를 넣으십시오 수 있도록 데이터 소스에서 모든 요소는 자체 팝업, `<ItemTemplate>` 섹션.</span><span class="sxs-lookup"><span data-stu-id="91da9-126">So that every element in the data source gets its own popup, the extender must be put within the repeater's `<ItemTemplate>` section.</span></span> <span data-ttu-id="91da9-127">다음은 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="91da9-127">Here is the markup:</span></span>

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample4.aspx)]

<span data-ttu-id="91da9-128">데이터 원본에 있는 모든 항목 오른쪽에는 팝업을 표시 하는 이제 (`PopupPosition` 특성) 50 밀리초의 지연 후 (`PopDelay` 특성).</span><span class="sxs-lookup"><span data-stu-id="91da9-128">Now every item in the data source displays a popup to the right (`PopupPosition` attribute) after a delay of 50 milliseconds (`PopDelay` attribute).</span></span>


<span data-ttu-id="91da9-129">[![반복기의 각 항목 옆에 호버 메뉴 표시](using-hovermenu-with-a-repeater-control-vb/_static/image2.png)](using-hovermenu-with-a-repeater-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="91da9-129">[![The hover menu appears next to each item in the repeater](using-hovermenu-with-a-repeater-control-vb/_static/image2.png)](using-hovermenu-with-a-repeater-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="91da9-130">호버 메뉴 반복기의 각 항목 옆에 나타납니다 ([전체 크기 이미지를 보려면 클릭](using-hovermenu-with-a-repeater-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="91da9-130">The hover menu appears next to each item in the repeater ([Click to view full-size image](using-hovermenu-with-a-repeater-control-vb/_static/image3.png))</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="91da9-131">이전</span><span class="sxs-lookup"><span data-stu-id="91da9-131">Previous</span></span>](using-hovermenu-with-a-repeater-control-cs.md)
