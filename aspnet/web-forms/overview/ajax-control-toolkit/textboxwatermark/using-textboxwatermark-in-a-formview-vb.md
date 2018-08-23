---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-vb
title: (VB) FormView에서 TextBoxWatermark 사용 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit에서 TextBoxWatermark 컨트롤은 텍스트 상자 내에서 표시 되도록 입력란을 확장 합니다. 상자에 사용자가 클릭 하 고 있나요...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 41497361-7fba-4825-b36c-f58d79522a88
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-vb
msc.type: authoredcontent
ms.openlocfilehash: b9a731be89d0582ebd411809a6bbcbee801fea2a
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829077"
---
<a name="using-textboxwatermark-in-a-formview-vb"></a><span data-ttu-id="f210a-104">(VB) FormView에서 TextBoxWatermark 사용</span><span class="sxs-lookup"><span data-stu-id="f210a-104">Using TextBoxWatermark in a FormView (VB)</span></span>
====================
<span data-ttu-id="f210a-105">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="f210a-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f210a-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark1.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="f210a-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark1.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark1VB.pdf)</span></span>

> <span data-ttu-id="f210a-107">AJAX Control Toolkit에서 TextBoxWatermark 컨트롤은 텍스트 상자 내에서 표시 되도록 입력란을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f210a-107">The TextBoxWatermark control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="f210a-108">사용자가 상자에는 클릭, 비워집니다.</span><span class="sxs-lookup"><span data-stu-id="f210a-108">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="f210a-109">사용자는 텍스트를 입력 하지 않고 상자를 퇴사, 하는 경우에 미리 채워진된 텍스트 다시 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f210a-109">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="f210a-110">FormView 컨트롤 내에서 가능한 이기도합니다.</span><span class="sxs-lookup"><span data-stu-id="f210a-110">This is also possible within a FormView control.</span></span>


## <a name="overview"></a><span data-ttu-id="f210a-111">개요</span><span class="sxs-lookup"><span data-stu-id="f210a-111">Overview</span></span>

<span data-ttu-id="f210a-112">`TextBoxWatermark` AJAX Control Toolkit의 컨트롤을 텍스트 상자 내에서 표시 되도록 입력란을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f210a-112">The `TextBoxWatermark` control in the AJAX Control Toolkit extends a text box so that a text is displayed within the box.</span></span> <span data-ttu-id="f210a-113">사용자가 상자에는 클릭, 비워집니다.</span><span class="sxs-lookup"><span data-stu-id="f210a-113">When a user clicks into the box, it is emptied.</span></span> <span data-ttu-id="f210a-114">사용자는 텍스트를 입력 하지 않고 상자를 퇴사, 하는 경우에 미리 채워진된 텍스트 다시 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f210a-114">If the user leaves the box without entering text, the prefilled text reappears.</span></span> <span data-ttu-id="f210a-115">내에서 가능한도를 `FormView` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="f210a-115">This is also possible within a `FormView` control.</span></span>

## <a name="steps"></a><span data-ttu-id="f210a-116">단계</span><span class="sxs-lookup"><span data-stu-id="f210a-116">Steps</span></span>

<span data-ttu-id="f210a-117">첫째, 데이터 소스는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f210a-117">First of all, a data source is required.</span></span> <span data-ttu-id="f210a-118">이 샘플에서는 AdventureWorks 데이터베이스 및 Microsoft SQL Server 2005 Express Edition을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f210a-118">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="f210a-119">데이터베이스 (express edition 포함)는 Visual Studio 설치의 선택적 부분이 며 아래에 있는 별도 다운로드로도 제공 됩니다 [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)합니다.</span><span class="sxs-lookup"><span data-stu-id="f210a-119">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="f210a-120">AdventureWorks 데이터베이스의 SQL Server 2005 샘플 및 예제 데이터베이스의 일부인 (에서 다운로드할 [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="f210a-120">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="f210a-121">데이터베이스를 설정 하는 가장 쉬운 방법은 Microsoft SQL Server Management Studio Express를 사용 하는 것 ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) 및 연결 된 `AdventureWorks.mdf` 데이터베이스 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f210a-121">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="f210a-122">이 샘플에서는 SQL Server 2005 Express Edition 인스턴스 라고 가정 `SQLEXPRESS` 웹 서버와 동일한 컴퓨터에 상주 하 고 기본 설정 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="f210a-122">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="f210a-123">설정이 다른 경우에 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f210a-123">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="f210a-124">ASP.NET AJAX와 Control Toolkit의 기능을 활성화 하기 위해 합니다 `ScriptManager` 컨트롤 페이지의 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):</span><span class="sxs-lookup"><span data-stu-id="f210a-124">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample1.aspx)]

<span data-ttu-id="f210a-125">그런 다음 데이터 원본을 지 원하는 페이지를 추가 합니다 `DELETE`, `INSERT` 및 `UPDATE` SQL 문입니다.</span><span class="sxs-lookup"><span data-stu-id="f210a-125">Then, add a data source to the page which supports the `DELETE`, `INSERT` and `UPDATE` SQL statements.</span></span> <span data-ttu-id="f210a-126">Visual Studio 도우미를 데이터 소스를 만드는 데 사용 하는 경우 고려해 현재 버전의 버그로 테이블 이름 접두사 하지 않습니다 (`Vendor`)와 `Purchasing`합니다.</span><span class="sxs-lookup"><span data-stu-id="f210a-126">If you are using the Visual Studio assistant to create the data source, mind that a bug in the current version does not prefix the table name (`Vendor`) with `Purchasing`.</span></span> <span data-ttu-id="f210a-127">다음 태그에서는 올바른 구문을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f210a-127">The following markup shows the correct syntax:</span></span>

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample2.aspx)]

<span data-ttu-id="f210a-128">이름을 기억할 (`ID`)에서 사용 되므로 데이터 원본의 합니다 `DataSourceID` 의 속성을 `FormView` 컨트롤.</span><span class="sxs-lookup"><span data-stu-id="f210a-128">Remember the name (`ID`) of the data source, since it will be used in the `DataSourceID` property of the `FormView` control.</span></span> <span data-ttu-id="f210a-129">`<InsertItemTemplate>` 의 섹션을 `FormView` 포함 하 여 확장 된 텍스트 상자는 `TextBoxWatermarkExtender` 컨트롤.</span><span class="sxs-lookup"><span data-stu-id="f210a-129">The `<InsertItemTemplate>` section of the `FormView` contains a textbox which is extended by the `TextBoxWatermarkExtender` control.</span></span> <span data-ttu-id="f210a-130">템플릿 내에서 범위를 벗어나지 extender 상주 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f210a-130">Make sure that the extender resides within the template and not outside of it.</span></span>

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample3.aspx)]

<span data-ttu-id="f210a-131">이제 변경 될 때 사용자의 삽입 모드에는 `FormView` 컨트롤, 텍스트 필드 덕분에 미리 채워지는 새 공급 업체에 대 한는 `TextBoxWatermarkExtender` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="f210a-131">Now when the user changes into the insert mode of the `FormView` control, the text field for the new vendor is prefilled thanks to the `TextBoxWatermarkExtender` control.</span></span> <span data-ttu-id="f210a-132">텍스트 상자 내부를 클릭 한 filler 텍스트가 사라집니다 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f210a-132">A click inside the textbox lets the filler text disappear.</span></span>


<span data-ttu-id="f210a-133">[![필드에 워터 마크 extender에서 제공 됩니다.](using-textboxwatermark-in-a-formview-vb/_static/image2.png)](using-textboxwatermark-in-a-formview-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f210a-133">[![The watermark in the field comes from the extender](using-textboxwatermark-in-a-formview-vb/_static/image2.png)](using-textboxwatermark-in-a-formview-vb/_static/image1.png)</span></span>

<span data-ttu-id="f210a-134">필드에 워터 마크 extender에서 제공 됩니다 ([클릭 하 여 큰 이미지 보기](using-textboxwatermark-in-a-formview-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="f210a-134">The watermark in the field comes from the extender ([Click to view full-size image](using-textboxwatermark-in-a-formview-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f210a-135">[이전](using-textboxwatermark-with-validation-controls-cs.md)
> [다음](using-textboxwatermark-with-validation-controls-vb.md)</span><span class="sxs-lookup"><span data-stu-id="f210a-135">[Previous](using-textboxwatermark-with-validation-controls-cs.md)
[Next](using-textboxwatermark-with-validation-controls-vb.md)</span></span>
