---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-cs
title: 반복기 컨트롤 (C#) ModalPopup 사용 | Microsoft Docs
author: wenz
description: 들어에서 ModalPopup 컨트롤을 클라이언트 쪽 방법을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 이 contr.를 사용 하는 것도 가능...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: d686d84a-1c58-492e-8a77-3eb5a0cfe918
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 7124ca3fc346d78c3b235d1756695b008afb47aa
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30872948"
---
<a name="using-modalpopup-with-a-repeater-control-c"></a><span data-ttu-id="93e76-104">반복기 컨트롤 (C#) ModalPopup 사용</span><span class="sxs-lookup"><span data-stu-id="93e76-104">Using ModalPopup with a Repeater Control (C#)</span></span>
====================
<span data-ttu-id="93e76-105">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="93e76-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="93e76-106">[코드를 다운로드](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup2.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="93e76-106">[Download Code](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup2.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup2CS.pdf)</span></span>

> <span data-ttu-id="93e76-107">들어에서 ModalPopup 컨트롤을 클라이언트 쪽 방법을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e76-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="93e76-108">도 한 반복기 내에서이 컨트롤을 사용 하는 것이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e76-108">It is also possible to use this control within a repeater.</span></span>


## <a name="overview"></a><span data-ttu-id="93e76-109">개요</span><span class="sxs-lookup"><span data-stu-id="93e76-109">Overview</span></span>

<span data-ttu-id="93e76-110">들어에서 ModalPopup 컨트롤을 클라이언트 쪽 방법을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e76-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="93e76-111">도 한 반복기 내에서이 컨트롤을 사용 하는 것이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e76-111">It is also possible to use this control within a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="93e76-112">단계</span><span class="sxs-lookup"><span data-stu-id="93e76-112">Steps</span></span>

<span data-ttu-id="93e76-113">첫째, 데이터 소스는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e76-113">First of all, a data source is required.</span></span> <span data-ttu-id="93e76-114">이 샘플에서는 AdventureWorks 데이터베이스 및 Microsoft SQL Server 2005 Express Edition을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e76-114">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="93e76-115">데이터베이스 (express edition 포함)는 Visual Studio 설치의 선택적 부분이 며에서 별도 다운로드로 제공 됩니다 [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)합니다.</span><span class="sxs-lookup"><span data-stu-id="93e76-115">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="93e76-116">AdventureWorks 데이터베이스의 SQL Server 2005 예제 및 예제 데이터베이스의 일부인 (다운로드에서 [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e &amp;4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="93e76-116">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="93e76-117">Microsoft SQL Server Management Studio Express를 사용 하는 가장 쉬운 방법은 데이터베이스를 설정 하는 ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) 및 연결 된 `AdventureWorks.mdf` 데이터베이스 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="93e76-117">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span> <span data-ttu-id="93e76-118">이 샘플에 대 한 SQL Server 2005 Express Edition 인스턴스 라고 가정 `SQLEXPRESS` 웹 서버와 동일한 컴퓨터에 상주 하 고 기본 설정 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e76-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="93e76-119">설정에 다른 경우 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e76-119">If your setup differs, you have to adapt the connection information for the database.</span></span> <span data-ttu-id="93e76-120">ASP.NET AJAX 및 제어 Toolkit의 기능을 활성화 하는 데는 `ScriptManager` 제어 페이지에서 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):</span><span class="sxs-lookup"><span data-stu-id="93e76-120">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample1.aspx)]

<span data-ttu-id="93e76-121">페이지 데이터 소스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e76-121">Then, add a data source to the page.</span></span> <span data-ttu-id="93e76-122">제한 된 양의 데이터를 사용 하려면만 선택 처음 5 개 항목 AdventureWorks 데이터베이스의 Vendor 테이블에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e76-122">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="93e76-123">Visual Studio 도우미를 데이터 소스를 만드는 데 사용 하는 경우 유의 현재 버전의 버그 테이블 이름이 붙지 않습니다 (`Vendor`)와 `Purchasing`합니다.</span><span class="sxs-lookup"><span data-stu-id="93e76-123">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="93e76-124">다음 태그를 올바른 구문을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="93e76-124">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample2.aspx)]

<span data-ttu-id="93e76-125">다음으로 모달 팝업으로 사용 되는 패널을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="93e76-125">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="93e76-126">포함 된 `Button` 컨트롤을 다시 여 팝업을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="93e76-126">It contains a `Button` control to close the popup again:</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample3.aspx)]

<span data-ttu-id="93e76-127">팝업 반복기, 내에서 작업할 수 있도록는 `ModalPopupExtender` 컨트롤 내에 배치 해야 합니다는 `<ItemTemplate>` 반복기의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="93e76-127">In order to make the popup work within the repeater, the `ModalPopupExtender` control must be put within the `<ItemTemplate>` section of the repeater.</span></span> <span data-ttu-id="93e76-128">따라서 패널 반복 벗어나지만 extender는 내부에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e76-128">So the panel is outside the repeater, but the extender is inside.</span></span> <span data-ttu-id="93e76-129">반복기에 대 한 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93e76-129">Here is the markup for the repeater:</span></span>

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample4.aspx)]

<span data-ttu-id="93e76-130">그런 다음 데이터 원본에 있는 모든 항목은 모달 팝업을 트리거하는 단추를 클릭 함께 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93e76-130">Then, every item in the data source is displayed with a button next to it that triggers the modal popup.</span></span>


<span data-ttu-id="93e76-131">[![모든 데이터 원본 항목에 대 한 모달 팝업을 트리거할 수 있습니다.](using-modalpopup-with-a-repeater-control-cs/_static/image2.png)](using-modalpopup-with-a-repeater-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="93e76-131">[![The modal popup can be triggered for every data source entry](using-modalpopup-with-a-repeater-control-cs/_static/image2.png)](using-modalpopup-with-a-repeater-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="93e76-132">모든 데이터 원본 항목에 대 한 모달 팝업을 트리거할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](using-modalpopup-with-a-repeater-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="93e76-132">The modal popup can be triggered for every data source entry ([Click to view full-size image](using-modalpopup-with-a-repeater-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="93e76-133">[이전](launching-a-modal-popup-window-from-server-code-cs.md)
> [다음](handling-postbacks-from-a-modalpopup-cs.md)</span><span class="sxs-lookup"><span data-stu-id="93e76-133">[Previous](launching-a-modal-popup-window-from-server-code-cs.md)
[Next](handling-postbacks-from-a-modalpopup-cs.md)</span></span>
