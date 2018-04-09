---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-cs
title: TextBoxWatermark FormView (C#)에서 사용 하 여 | Microsoft Docs
author: wenz
description: 들어에서 TextBoxWatermark 컨트롤 텍스트 상자 내에서 표시 되도록 입력란을 확장 합니다. 상자에는 사용자가 클릭할 때 그 i...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: e6ee90bf-32a5-4987-a384-15cc7dd30c8a
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-cs
msc.type: authoredcontent
ms.openlocfilehash: 90e532d33756a995a85994254c48889517c5bb8d
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="using-textboxwatermark-in-a-formview-c"></a><span data-ttu-id="27641-104">TextBoxWatermark FormView (C#)에서 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="27641-104">Using TextBoxWatermark in a FormView (C#)</span></span>
====================
<span data-ttu-id="27641-105">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="27641-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="27641-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark1.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="27641-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark1CS.pdf)</span></span>

> <span data-ttu-id="27641-107">들어에서 TextBoxWatermark 컨트롤 텍스트 상자 내에서 표시 되도록 입력란을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="27641-107">The TextBoxWatermark control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="27641-108">상자에 사용자가 클릭, 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27641-108">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="27641-109">사용자가 상자 텍스트를 입력 하지 않고를 완료 하는 경우에 미리 채워진된 텍스트 다시 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="27641-109">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="27641-110">FormView 컨트롤 내에서 가능한 이기도합니다.</span><span class="sxs-lookup"><span data-stu-id="27641-110">This is also possible within a FormView control.</span></span>


## <a name="overview"></a><span data-ttu-id="27641-111">개요</span><span class="sxs-lookup"><span data-stu-id="27641-111">Overview</span></span>

<span data-ttu-id="27641-112">`TextBoxWatermark` 들어에서 컨트롤 텍스트 상자 내에서 표시 되도록 입력란을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="27641-112">The `TextBoxWatermark` control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="27641-113">상자에 사용자가 클릭, 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27641-113">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="27641-114">사용자가 상자 텍스트를 입력 하지 않고를 완료 하는 경우에 미리 채워진된 텍스트 다시 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="27641-114">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="27641-115">내에서 가능한 이기도 한 `FormView` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="27641-115">This is also possible within a `FormView` control.</span></span>

## <a name="steps"></a><span data-ttu-id="27641-116">단계</span><span class="sxs-lookup"><span data-stu-id="27641-116">Steps</span></span>

<span data-ttu-id="27641-117">첫째, 데이터 소스는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="27641-117">First of all, a data source is required.</span></span> <span data-ttu-id="27641-118">이 샘플에서는 AdventureWorks 데이터베이스 및 Microsoft SQL Server 2005 Express Edition을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="27641-118">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="27641-119">데이터베이스 (express edition 포함)는 Visual Studio 설치의 선택적 부분이 며에서 별도 다운로드로 제공 됩니다 [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)합니다.</span><span class="sxs-lookup"><span data-stu-id="27641-119">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="27641-120">AdventureWorks 데이터베이스의 SQL Server 2005 예제 및 예제 데이터베이스의 일부인 (다운로드에서 [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e &amp;4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="27641-120">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="27641-121">Microsoft SQL Server Management Studio Express를 사용 하는 가장 쉬운 방법은 데이터베이스를 설정 하는 ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) 및 연결 된 `AdventureWorks.mdf` 데이터베이스 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="27641-121">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="27641-122">이 샘플에 대 한 SQL Server 2005 Express Edition 인스턴스 라고 가정 `SQLEXPRESS` 웹 서버와 동일한 컴퓨터에 상주 하 고 기본 설정 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="27641-122">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="27641-123">설정에 다른 경우 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27641-123">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="27641-124">ASP.NET AJAX 및 제어 Toolkit의 기능을 활성화 하는 데는 `ScriptManager` 제어 페이지에서 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):</span><span class="sxs-lookup"><span data-stu-id="27641-124">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-textboxwatermark-in-a-formview-cs/samples/sample1.aspx)]

<span data-ttu-id="27641-125">그런 다음 데이터 원본을 지 원하는 페이지에 추가 `DELETE`, `INSERT` 및 `UPDATE` SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="27641-125">Then, add a data source to the page which supports the `DELETE`, `INSERT` and `UPDATE` SQL statements.</span></span> <span data-ttu-id="27641-126">Visual Studio 도우미를 데이터 소스를 만드는 데 사용 하는 경우 유의 현재 버전의 버그 테이블 이름이 붙지 않습니다 (`Vendor`)와 `Purchasing`합니다.</span><span class="sxs-lookup"><span data-stu-id="27641-126">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="27641-127">다음 태그를 올바른 구문을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="27641-127">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-textboxwatermark-in-a-formview-cs/samples/sample2.aspx)]

<span data-ttu-id="27641-128">이름을 기억할 (`ID`)에 사용 되므로 데이터 원본의 `DataSourceID` 의 속성은 `FormView` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="27641-128">Remember the name (`ID`) of the data source, since it will be used in the `DataSourceID` property of the `FormView` control.</span></span> <span data-ttu-id="27641-129">`<InsertItemTemplate>` 의 섹션은 `FormView` 포함 하 여 확장 된 텍스트 상자는 `TextBoxWatermarkExtender` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="27641-129">The `<InsertItemTemplate>` section of the `FormView` contains a textbox which is extended by the `TextBoxWatermarkExtender` control.</span></span> <span data-ttu-id="27641-130">Extender 있는 템플릿의 범위를 벗어나지 않고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="27641-130">Make sure that the extender resides within the template and not outside of it.</span></span>

[!code-aspx[Main](using-textboxwatermark-in-a-formview-cs/samples/sample3.aspx)]

<span data-ttu-id="27641-131">이제 변경 될 때 사용자의 삽입 모드로 `FormView` 컨트롤, 텍스트 필드에 감사 드립니다 미리 채워지는 새 공급 업체는 `TextBoxWatermarkExtender` 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="27641-131">Now when the user changes into the insert mode of the `FormView` control, the text field for the new vendor is prefilled thanks to the `TextBoxWatermarkExtender` control.</span></span> <span data-ttu-id="27641-132">한 번의 클릭 하 고 입력란 내의 필러 텍스트를 사라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27641-132">A click inside the textbox lets the filler text disappear.</span></span>


<span data-ttu-id="27641-133">[![Extender에서 제공 되는 필드에서 워터 마크](using-textboxwatermark-in-a-formview-cs/_static/image2.png)](using-textboxwatermark-in-a-formview-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="27641-133">[![The watermark in the field comes from the extender](using-textboxwatermark-in-a-formview-cs/_static/image2.png)](using-textboxwatermark-in-a-formview-cs/_static/image1.png)</span></span>

<span data-ttu-id="27641-134">Extender에서 제공 되는 필드에서 워터 마크 ([전체 크기 이미지를 보려면 클릭](using-textboxwatermark-in-a-formview-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="27641-134">The watermark in the field comes from the extender ([Click to view full-size image](using-textboxwatermark-in-a-formview-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="27641-135">다음</span><span class="sxs-lookup"><span data-stu-id="27641-135">Next</span></span>](using-textboxwatermark-with-validation-controls-cs.md)
