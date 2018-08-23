---
uid: web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-cs
title: Accordion (C#)에 데이터 바인딩 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit의 Accordion 컨트롤 여러 창을 제공 하 고 둘 중 한 번에 표시할 수 있습니다. 일반적으로 패널 w 선언 하는 중...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 9c8f0054-e319-46f8-80c0-35b606d2fbd4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-cs
msc.type: authoredcontent
ms.openlocfilehash: 930392bd33cfeb7dec52a6084a5d401a6134a7ef
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41839087"
---
<a name="databinding-to-an-accordion-c"></a><span data-ttu-id="35b4d-104">Accordion (C#)에 데이터 바인딩</span><span class="sxs-lookup"><span data-stu-id="35b4d-104">Databinding to an Accordion (C#)</span></span>
====================
<span data-ttu-id="35b4d-105">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="35b4d-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="35b4d-106">[코드를 다운로드](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="35b4d-106">[Download Code](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1CS.pdf)</span></span>

> <span data-ttu-id="35b4d-107">AJAX Control Toolkit의 Accordion 컨트롤 여러 창을 제공 하 고 둘 중 한 번에 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35b4d-107">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="35b4d-108">패널은 일반적으로 페이지 자체 내에서 선언 하지만 데이터 소스에 바인딩하는 더 많은 유연성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="35b4d-108">Panels are usually declared within the page itself, but binding to a data source offers more flexibility.</span></span>


## <a name="overview"></a><span data-ttu-id="35b4d-109">개요</span><span class="sxs-lookup"><span data-stu-id="35b4d-109">Overview</span></span>

<span data-ttu-id="35b4d-110">AJAX Control Toolkit의 Accordion 컨트롤 여러 창을 제공 하 고 둘 중 한 번에 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35b4d-110">The Accordion control in the AJAX Control Toolkit provides multiple panes and allows the user to display one of them at a time.</span></span> <span data-ttu-id="35b4d-111">패널은 일반적으로 페이지 자체 내에서 선언 하지만 데이터 소스에 바인딩하는 더 많은 유연성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="35b4d-111">Panels are usually declared within the page itself, but binding to a data source offers more flexibility.</span></span>

## <a name="steps"></a><span data-ttu-id="35b4d-112">단계</span><span class="sxs-lookup"><span data-stu-id="35b4d-112">Steps</span></span>

<span data-ttu-id="35b4d-113">첫째, 데이터 소스는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="35b4d-113">First of all, a data source is required.</span></span> <span data-ttu-id="35b4d-114">이 샘플에서는 AdventureWorks 데이터베이스 및 Microsoft SQL Server 2005 Express Edition을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="35b4d-114">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="35b4d-115">데이터베이스 (express edition 포함)는 Visual Studio 설치의 선택적 부분이 며 아래에 있는 별도 다운로드로도 제공 됩니다 [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)합니다.</span><span class="sxs-lookup"><span data-stu-id="35b4d-115">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="35b4d-116">AdventureWorks 데이터베이스의 SQL Server 2005 샘플 및 예제 데이터베이스의 일부인 (에서 다운로드할 [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="35b4d-116">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="35b4d-117">데이터베이스를 설정 하는 가장 쉬운 방법은 Microsoft SQL Server Management Studio Express를 사용 하는 것 ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) 및 연결 된 `AdventureWorks.mdf` 데이터베이스 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="35b4d-117">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="35b4d-118">이 샘플에서는 SQL Server 2005 Express Edition 인스턴스 라고 가정 `SQLEXPRESS` 웹 서버와 동일한 컴퓨터에 상주 하 고 기본 설정 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="35b4d-118">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="35b4d-119">설정이 다른 경우에 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35b4d-119">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="35b4d-120">ASP.NET AJAX와 Control Toolkit의 기능을 활성화 하기 위해 합니다 `ScriptManager` 컨트롤 페이지의 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):</span><span class="sxs-lookup"><span data-stu-id="35b4d-120">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample1.aspx)]

<span data-ttu-id="35b4d-121">그런 다음 페이지에 데이터 소스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="35b4d-121">Then, add a data source to the page.</span></span> <span data-ttu-id="35b4d-122">제한 된 양의 데이터를 사용 하려면만 선택 처음 5 개 항목을 AdventureWorks 데이터베이스의 Vendor 테이블의 합니다.</span><span class="sxs-lookup"><span data-stu-id="35b4d-122">In order to use a limited amount of data, we only select the first five entries in the Vendor table of the AdventureWorks database.</span></span> <span data-ttu-id="35b4d-123">Visual Studio 도우미를 데이터 소스를 만드는 데 사용 하는 경우 고려해 현재 버전의 버그로 테이블 이름 접두사 하지 않습니다 (`Vendor`)와 `Purchasing`합니다.</span><span class="sxs-lookup"><span data-stu-id="35b4d-123">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="35b4d-124">다음 태그에서는 올바른 구문을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="35b4d-124">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample2.aspx)]

<span data-ttu-id="35b4d-125">데이터 원본 이름 (ID)를 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="35b4d-125">Remember the name (ID) of the data source.</span></span> <span data-ttu-id="35b4d-126">이 매우 식별에 사용 해야 합니다는 `DataSourceID` Accordion 컨트롤의 속성:</span><span class="sxs-lookup"><span data-stu-id="35b4d-126">This very identification must then be used in the `DataSourceID` property of the Accordion control:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample3.aspx)]

<span data-ttu-id="35b4d-127">Accordion 컨트롤 내에서 헤더를 포함 하는 컨트롤의 다양 한 부분에 대 한 서식 파일을 제공할 수 있습니다 (`<HeaderTemplate>`) 및 콘텐츠 (`<ContentTemplate>`).</span><span class="sxs-lookup"><span data-stu-id="35b4d-127">Within the Accordion control, you can provide templates for various parts of the control, including the header (`<HeaderTemplate>`) and the content (`<ContentTemplate>`).</span></span> <span data-ttu-id="35b4d-128">이러한 요소 내에서 출력 데이터의 데이터를 사용 하 여 소스를 `DataBinder.Eval()` 메서드:</span><span class="sxs-lookup"><span data-stu-id="35b4d-128">Within these elements, just output the data from the data source, using the `DataBinder.Eval()` method:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample4.aspx)]

<span data-ttu-id="35b4d-129">페이지가 로드 될 때 데이터 원본은이 서버 쪽 코드를 사용 하 여 accordion에 바인딩되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35b4d-129">When the page is loaded, the data source must be bound to the accordion with this server-side code:</span></span>

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample5.aspx)]

<span data-ttu-id="35b4d-130">이 샘플 되려면 Accordion 컨트롤에서 참조 되는 두 개의 CSS 클래스를 정의 해야 (속성만에서 `HeaderCssClass` 고 `ContentCssClass`).</span><span class="sxs-lookup"><span data-stu-id="35b4d-130">To conclude this sample, you need to define the two CSS classes that are referenced in the Accordion control (in its properties `HeaderCssClass` and `ContentCssClass`).</span></span> <span data-ttu-id="35b4d-131">다음 태그 안에 `<head>` 페이지의 섹션:</span><span class="sxs-lookup"><span data-stu-id="35b4d-131">Put the following markup in the `<head>` section of the page:</span></span>

[!code-css[Main](databinding-to-an-accordion-cs/samples/sample6.css)]


<span data-ttu-id="35b4d-132">[![데이터 원본에서 직접 제공 되는 accordion에 데이터는](databinding-to-an-accordion-cs/_static/image2.png)](databinding-to-an-accordion-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="35b4d-132">[![The data in the accordion comes directly from the data source](databinding-to-an-accordion-cs/_static/image2.png)](databinding-to-an-accordion-cs/_static/image1.png)</span></span>

<span data-ttu-id="35b4d-133">데이터 원본에서 직접 제공 되는 accordion에 데이터 ([클릭 하 여 큰 이미지 보기](databinding-to-an-accordion-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="35b4d-133">The data in the accordion comes directly from the data source ([Click to view full-size image](databinding-to-an-accordion-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="35b4d-134">다음</span><span class="sxs-lookup"><span data-stu-id="35b4d-134">Next</span></span>](dynamically-adding-an-accordion-pane-cs.md)
