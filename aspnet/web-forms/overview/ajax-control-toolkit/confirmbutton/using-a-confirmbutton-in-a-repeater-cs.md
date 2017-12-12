---
uid: web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-cs
title: "ConfirmButton 반복기 (C#)에서 사용 하 여 | Microsoft Docs"
author: wenz
description: "들어에서 ConfirmButton extender 만듭니다 Yes/사용자가 단추를 클릭할 때 없음 팝업 (LinkButton 컨트롤 포함). 경우에만 예는..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: a973ed3e-400c-4925-ace2-0b086b479301
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-cs
msc.type: authoredcontent
ms.openlocfilehash: 12fd3e4e58e6a73720ade38372caff496f7f2c97
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="using-a-confirmbutton-in-a-repeater-c"></a><span data-ttu-id="36c81-104">ConfirmButton 반복기 (C#)에서 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="36c81-104">Using a ConfirmButton In a Repeater (C#)</span></span>
====================
<span data-ttu-id="36c81-105">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="36c81-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="36c81-106">[코드를 다운로드](http://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="36c81-106">[Download Code](http://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1CS.pdf)</span></span>

> <span data-ttu-id="36c81-107">들어에서 ConfirmButton extender 만듭니다 Yes/사용자가 단추를 클릭할 때 없음 팝업 (LinkButton 컨트롤 포함).</span><span class="sxs-lookup"><span data-stu-id="36c81-107">The ConfirmButton extender in the AJAX Control Toolkit creates a Yes/No popup when the user clicks on a button (including LinkButton control).</span></span> <span data-ttu-id="36c81-108">만 예을 클릭할 경우 단추의 동작이 취소 그렇지 않은 경우 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="36c81-108">Only if Yes is clicked, the button's action is executed, otherwise cancelled.</span></span> <span data-ttu-id="36c81-109">반복기에서 가능한 이기도합니다.</span><span class="sxs-lookup"><span data-stu-id="36c81-109">This is also possible in a repeater.</span></span>


## <a name="overview"></a><span data-ttu-id="36c81-110">개요</span><span class="sxs-lookup"><span data-stu-id="36c81-110">Overview</span></span>

<span data-ttu-id="36c81-111">들어에서 ConfirmButton extender 만듭니다 Yes/사용자가 단추를 클릭할 때 없음 팝업 (LinkButton 컨트롤 포함).</span><span class="sxs-lookup"><span data-stu-id="36c81-111">The ConfirmButton extender in the AJAX Control Toolkit creates a Yes/No popup when the user clicks on a button (including LinkButton control).</span></span> <span data-ttu-id="36c81-112">만 예을 클릭할 경우 단추의 동작이 취소 그렇지 않은 경우 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="36c81-112">Only if Yes is clicked, the button's action is executed, otherwise cancelled.</span></span> <span data-ttu-id="36c81-113">반복기에서 가능한 이기도합니다.</span><span class="sxs-lookup"><span data-stu-id="36c81-113">This is also possible in a repeater.</span></span>

## <a name="steps"></a><span data-ttu-id="36c81-114">단계</span><span class="sxs-lookup"><span data-stu-id="36c81-114">Steps</span></span>

<span data-ttu-id="36c81-115">첫째, 데이터 소스는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="36c81-115">First of all, a data source is required.</span></span> <span data-ttu-id="36c81-116">이 샘플에서는 AdventureWorks 데이터베이스 및 Microsoft SQL Server 2005 Express Edition을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="36c81-116">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="36c81-117">데이터베이스 (express edition 포함)는 Visual Studio 설치의 선택적 부분이 며에서 별도 다운로드로 제공 됩니다 [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)합니다.</span><span class="sxs-lookup"><span data-stu-id="36c81-117">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="36c81-118">AdventureWorks 데이터베이스의 SQL Server 2005 예제 및 예제 데이터베이스의 일부인 (다운로드에서 [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="36c81-118">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="36c81-119">Microsoft SQL Server Management Studio Express를 사용 하는 데이터베이스를 설정 하는 가장 쉬운 방법은 ([https://www.microsoft.com/downloads/details.aspx? FamilyID c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796 =&amp;4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) 및 연결 된 `AdventureWorks.mdf` 데이터베이스 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="36c81-119">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="36c81-120">이 샘플에 대 한 SQL Server 2005 Express Edition 인스턴스 라고 가정 `SQLEXPRESS` 웹 서버와 동일한 컴퓨터에 상주 하 고 기본 설정 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="36c81-120">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="36c81-121">설정에 다른 경우 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36c81-121">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="36c81-122">ASP.NET AJAX 및 제어 Toolkit의 기능을 활성화 하는 데는 `ScriptManager` 제어 페이지에서 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):</span><span class="sxs-lookup"><span data-stu-id="36c81-122">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-cs/samples/sample1.aspx)]

<span data-ttu-id="36c81-123">그런 다음 데이터 소스는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="36c81-123">Then, a data source is required.</span></span> <span data-ttu-id="36c81-124">간단한 설명을 위해 AdventureWorks의 공급 업체 테이블의 처음 5 개 항목만 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="36c81-124">For the sake of simplicity, only the first five entries in AdventureWorks' Vendors table are retrieved.</span></span> <span data-ttu-id="36c81-125">데이터 소스 테이블 이름을 만들려면 Visual Studio 마법사를 사용할 때 (`Vendors`)가 현재 제대로로 시작 하지 않는 `Purchasing`합니다.</span><span class="sxs-lookup"><span data-stu-id="36c81-125">Note that when using the Visual Studio wizard to create the data source, the table name (`Vendors`) is currently not correctly prefixed with `Purchasing`.</span></span> <span data-ttu-id="36c81-126">다음 태그는 가장 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="36c81-126">The following markup is the correct one:</span></span>

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-cs/samples/sample2.aspx)]

<span data-ttu-id="36c81-127">이 데이터 원본은 반복기 내에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36c81-127">This data source can then be used within a repeater.</span></span> <span data-ttu-id="36c81-128">일반적으로 `DataBinder.Eval()` 메서드는 데이터 원본에서 데이터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="36c81-128">As usual, the `DataBinder.Eval()` method retrieves data from the data source.</span></span> <span data-ttu-id="36c81-129">`ConfirmButtonExtender` 다음 내에서 컨트롤을 배치 해야 합니다는 `<ItemTemplate>` 섹션 반복기에 대 한 데이터 원본에서 모든 항목에 표시 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="36c81-129">The `ConfirmButtonExtender` control must then be placed within the `<ItemTemplate>` section of the repeater so that it appears for every entry in the data source.</span></span>

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-cs/samples/sample3.aspx)]


<span data-ttu-id="36c81-130">[![데이터 원본의 각 항목 옆에 확인 단추 표시](using-a-confirmbutton-in-a-repeater-cs/_static/image2.png)](using-a-confirmbutton-in-a-repeater-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="36c81-130">[![The confirm button appears next to each entry from the data source](using-a-confirmbutton-in-a-repeater-cs/_static/image2.png)](using-a-confirmbutton-in-a-repeater-cs/_static/image1.png)</span></span>

<span data-ttu-id="36c81-131">확인 단추가 데이터 원본의 각 항목 옆에 나타납니다 ([전체 크기 이미지를 보려면 클릭](using-a-confirmbutton-in-a-repeater-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="36c81-131">The confirm button appears next to each entry from the data source ([Click to view full-size image](using-a-confirmbutton-in-a-repeater-cs/_static/image3.png))</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="36c81-132">다음</span><span class="sxs-lookup"><span data-stu-id="36c81-132">Next</span></span>](using-a-confirmbutton-in-a-repeater-vb.md)
