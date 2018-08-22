---
uid: web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-vb
title: (VB) Repeater에 ConfirmButton 사용 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit의 ConfirmButton extender 만듭니다 Yes/사용자가 단추를 클릭할 때 팝업 없습니다 (LinkButton 컨트롤 포함). 경우에만 예는...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 18c31709-3f9d-4d93-8b01-f1356bf610b4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-vb
msc.type: authoredcontent
ms.openlocfilehash: 38ac40776c2fdd14af046b5e13df0701c71a4ad0
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41837563"
---
<a name="using-a-confirmbutton-in-a-repeater-vb"></a><span data-ttu-id="3b605-104">(VB) Repeater에 ConfirmButton 사용</span><span class="sxs-lookup"><span data-stu-id="3b605-104">Using a ConfirmButton In a Repeater (VB)</span></span>
====================
<span data-ttu-id="3b605-105">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="3b605-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="3b605-106">[코드를 다운로드](http://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="3b605-106">[Download Code](http://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1VB.pdf)</span></span>

> <span data-ttu-id="3b605-107">AJAX Control Toolkit의 ConfirmButton extender 만듭니다 Yes/사용자가 단추를 클릭할 때 팝업 없습니다 (LinkButton 컨트롤 포함).</span><span class="sxs-lookup"><span data-stu-id="3b605-107">The ConfirmButton extender in the AJAX Control Toolkit creates a Yes/No popup when the user clicks on a button (including LinkButton control).</span></span> <span data-ttu-id="3b605-108">만 예는 단추를 클릭 하면 단추의 작업 취소 그렇지 않은 경우 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b605-108">Only if Yes is clicked, the button's action is executed, otherwise cancelled.</span></span> <span data-ttu-id="3b605-109">Repeater에는이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="3b605-109">This is also possible in a repeater.</span></span>


## <a name="overview"></a><span data-ttu-id="3b605-110">개요</span><span class="sxs-lookup"><span data-stu-id="3b605-110">Overview</span></span>

<span data-ttu-id="3b605-111">AJAX Control Toolkit의 ConfirmButton extender 만듭니다 Yes/사용자가 단추를 클릭할 때 팝업 없습니다 (LinkButton 컨트롤 포함).</span><span class="sxs-lookup"><span data-stu-id="3b605-111">The ConfirmButton extender in the AJAX Control Toolkit creates a Yes/No popup when the user clicks on a button (including LinkButton control).</span></span> <span data-ttu-id="3b605-112">만 예는 단추를 클릭 하면 단추의 작업 취소 그렇지 않은 경우 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b605-112">Only if Yes is clicked, the button's action is executed, otherwise cancelled.</span></span> <span data-ttu-id="3b605-113">Repeater에는이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="3b605-113">This is also possible in a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="3b605-114">단계</span><span class="sxs-lookup"><span data-stu-id="3b605-114">Steps</span></span>

<span data-ttu-id="3b605-115">첫째, 데이터 소스는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b605-115">First of all, a data source is required.</span></span> <span data-ttu-id="3b605-116">이 샘플에서는 AdventureWorks 데이터베이스 및 Microsoft SQL Server 2005 Express Edition을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b605-116">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="3b605-117">데이터베이스 (express edition 포함)는 Visual Studio 설치의 선택적 부분이 며 아래에 있는 별도 다운로드로도 제공 됩니다 [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)합니다.</span><span class="sxs-lookup"><span data-stu-id="3b605-117">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="3b605-118">AdventureWorks 데이터베이스의 SQL Server 2005 샘플 및 예제 데이터베이스의 일부인 (에서 다운로드할 [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="3b605-118">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="3b605-119">데이터베이스를 설정 하는 가장 쉬운 방법은 Microsoft SQL Server Management Studio Express를 사용 하는 것 ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) 및 연결 된 `AdventureWorks.mdf` 데이터베이스 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3b605-119">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="3b605-120">이 샘플에서는 SQL Server 2005 Express Edition 인스턴스 라고 가정 `SQLEXPRESS` 웹 서버와 동일한 컴퓨터에 상주 하 고 기본 설정 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b605-120">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="3b605-121">설정이 다른 경우에 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b605-121">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="3b605-122">ASP.NET AJAX와 Control Toolkit의 기능을 활성화 하기 위해 합니다 `ScriptManager` 컨트롤 페이지의 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):</span><span class="sxs-lookup"><span data-stu-id="3b605-122">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample1.aspx)]

<span data-ttu-id="3b605-123">그런 다음 데이터 소스는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b605-123">Then, a data source is required.</span></span> <span data-ttu-id="3b605-124">간단히 하기 위해 AdventureWorks의 공급 업체 테이블의 처음 5 개 항목만 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b605-124">For the sake of simplicity, only the first five entries in AdventureWorks' Vendors table are retrieved.</span></span> <span data-ttu-id="3b605-125">Visual Studio 마법사를 사용 하 여 데이터 원본에 테이블 이름을 만들려면 때 (`Vendors`)은 현재 올바르게로 시작 하지 않는 `Purchasing`합니다.</span><span class="sxs-lookup"><span data-stu-id="3b605-125">Note that when using the Visual Studio wizard to create the data source, the table name (`Vendors`) is currently not correctly prefixed with `Purchasing`.</span></span> <span data-ttu-id="3b605-126">다음 태그는 올바른 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3b605-126">The following markup is the correct one:</span></span>

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample2.aspx)]

<span data-ttu-id="3b605-127">Repeater 내에서이 데이터 원본을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b605-127">This data source can then be used within a repeater.</span></span> <span data-ttu-id="3b605-128">일반적으로 `DataBinder.Eval()` 메서드 데이터 원본에서 데이터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b605-128">As usual, the `DataBinder.Eval()` method retrieves data from the data source.</span></span> <span data-ttu-id="3b605-129">합니다 `ConfirmButtonExtender` 컨트롤 내에 다음 배치 해야 합니다는 `<ItemTemplate>` 데이터 소스의 모든 항목에 대 한 표시 되도록 반복기 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="3b605-129">The `ConfirmButtonExtender` control must then be placed within the `<ItemTemplate>` section of the repeater so that it appears for every entry in the data source.</span></span>

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample3.aspx)]


<span data-ttu-id="3b605-130">[![데이터 원본의 각 항목 옆에 있는 확인 단추를 표시 됩니다.](using-a-confirmbutton-in-a-repeater-vb/_static/image2.png)](using-a-confirmbutton-in-a-repeater-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3b605-130">[![The confirm button appears next to each entry from the data source](using-a-confirmbutton-in-a-repeater-vb/_static/image2.png)](using-a-confirmbutton-in-a-repeater-vb/_static/image1.png)</span></span>

<span data-ttu-id="3b605-131">데이터 원본의 각 항목 옆에 있는 확인 단추를 표시 됩니다 ([클릭 하 여 큰 이미지 보기](using-a-confirmbutton-in-a-repeater-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="3b605-131">The confirm button appears next to each entry from the data source ([Click to view full-size image](using-a-confirmbutton-in-a-repeater-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="3b605-132">이전</span><span class="sxs-lookup"><span data-stu-id="3b605-132">Previous</span></span>](using-a-confirmbutton-in-a-repeater-cs.md)
