---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-vb
title: (VB) 데이터베이스에 CascadingDropDown 사용 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit에서 CascadingDropDown 컨트롤 하나 DropDownList 로드 변경에 관련 된 값이 anoth에 있도록 DropDownList 컨트롤을 확장 하는 중...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: 97a3d33c-c856-43f3-8acb-f1ccbc48221a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-vb
msc.type: authoredcontent
ms.openlocfilehash: 48e52fce4e26ec08403c3d86a4c3f85c103baa82
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37824233"
---
<a name="using-cascadingdropdown-with-a-database-vb"></a><span data-ttu-id="435c0-103">CascadingDropDown을 사용 하 여 데이터베이스 (VB)</span><span class="sxs-lookup"><span data-stu-id="435c0-103">Using CascadingDropDown with a Database (VB)</span></span>
====================
<span data-ttu-id="435c0-104">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="435c0-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="435c0-105">[코드를 다운로드](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="435c0-105">[Download Code](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1VB.pdf)</span></span>

> <span data-ttu-id="435c0-106">AJAX Control Toolkit에서 CascadingDropDown 컨트롤 하나 DropDownList 로드 변경에 관련 된 값이 다른 DropDownList에 있도록 DropDownList 컨트롤을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="435c0-107">이 작업을 위해 특수 한 웹 서비스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-107">In order for this to work, a special web service must be created.</span></span>


## <a name="overview"></a><span data-ttu-id="435c0-108">개요</span><span class="sxs-lookup"><span data-stu-id="435c0-108">Overview</span></span>

<span data-ttu-id="435c0-109">AJAX Control Toolkit에서 CascadingDropDown 컨트롤 하나 DropDownList 로드 변경에 관련 된 값이 다른 DropDownList에 있도록 DropDownList 컨트롤을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="435c0-110">(예를 들어 미국 주 목록을 제공 하는 하나의 목록 및 해당 상태의 주요 도시를 사용 하 여 다음 목록에 다음 채워집니다.) 이 작업을 위해 특수 한 웹 서비스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) In order for this to work, a special web service must be created.</span></span>

## <a name="steps"></a><span data-ttu-id="435c0-111">단계</span><span class="sxs-lookup"><span data-stu-id="435c0-111">Steps</span></span>

<span data-ttu-id="435c0-112">첫째, 데이터 소스는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-112">First of all, a data source is required.</span></span> <span data-ttu-id="435c0-113">이 샘플에서는 AdventureWorks 데이터베이스 및 Microsoft SQL Server 2005 Express Edition을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-113">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="435c0-114">데이터베이스 (express edition 포함)는 Visual Studio 설치의 선택적 부분이 며 아래에 있는 별도 다운로드로도 제공 됩니다 [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)합니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-114">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="435c0-115">AdventureWorks 데이터베이스의 SQL Server 2005 샘플 및 예제 데이터베이스의 일부인 (에서 다운로드할 [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="435c0-115">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="435c0-116">데이터베이스를 설정 하는 가장 쉬운 방법은 Microsoft SQL Server Management Studio Express를 사용 하는 것 ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) 및 연결 된 `AdventureWorks.mdf` 데이터베이스 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-116">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="435c0-117">이 샘플에서는 SQL Server 2005 Express Edition 인스턴스 라고 가정 `SQLEXPRESS` 웹 서버와 동일한 컴퓨터에 상주 하 고 기본 설정 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="435c0-118">설정이 다른 경우에 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="435c0-119">ASP.NET AJAX와 Control Toolkit의 기능을 활성화 하기 위해 합니다 `ScriptManager` 컨트롤 페이지의 아무 곳 이나 배치 해야 합니다 (하지만 내 합니다 &lt; `form` &gt; 요소):</span><span class="sxs-lookup"><span data-stu-id="435c0-119">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the &lt;`form`&gt; element):</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample1.aspx)]

<span data-ttu-id="435c0-120">다음 단계에서는 두 DropDownList 컨트롤은 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-120">In the next step, two DropDownList controls are required.</span></span> <span data-ttu-id="435c0-121">이 샘플에서 AdventureWorks에서 공급 업체 및 연락처 정보를 사용 하 여, 따라서 사용 가능한 공급 업체 및 사용 가능한 연락처에 대 한 하나의 목록을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-121">In this sample, we use the vendor and contact information from AdventureWorks, thus we create one list for the available vendors and one for the available contacts:</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample2.aspx)]

<span data-ttu-id="435c0-122">그런 다음 두 CascadingDropDown extender는 페이지에 추가 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-122">Then, two CascadingDropDown extenders must be added to the page.</span></span> <span data-ttu-id="435c0-123">첫 번째 (공급 업체) 목록에서 하나 채우고 다른 두 번째 (연락처) 목록을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-123">One fills the first (vendors) list, and the other one fills the second (contacts) list.</span></span> <span data-ttu-id="435c0-124">다음 특성을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-124">The following attributes must be set:</span></span>

- <span data-ttu-id="435c0-125">`ServicePath`: 목록 항목을 제공 하는 웹 서비스의 URL</span><span class="sxs-lookup"><span data-stu-id="435c0-125">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="435c0-126">`ServiceMethod`합니다: 목록 항목을 제공 웹 메서드</span><span class="sxs-lookup"><span data-stu-id="435c0-126">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="435c0-127">`TargetControlID`: 드롭다운 목록의 ID</span><span class="sxs-lookup"><span data-stu-id="435c0-127">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="435c0-128">`Category`: 웹 메서드 호출에 제출 된 범주 정보</span><span class="sxs-lookup"><span data-stu-id="435c0-128">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="435c0-129">`PromptText`: 비동기적으로 서버에서 목록 데이터를 로드할 때 표시 되는 텍스트</span><span class="sxs-lookup"><span data-stu-id="435c0-129">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>
- <span data-ttu-id="435c0-130">`ParentControlID`: (선택 사항) 부모 드롭다운의 현재 목록 로드 하는 트리거 목록</span><span class="sxs-lookup"><span data-stu-id="435c0-130">`ParentControlID`: (optional) parent dropdown list that triggers loading of the current list</span></span>

<span data-ttu-id="435c0-131">사용 되는 프로그래밍 언어에 따라 해당 웹 서비스의 이름을 변경 하지만 다른 모든 특성 값이 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-131">Depending on the programming language used, the name of the web service in question changes, but all other attribute values are the same.</span></span> <span data-ttu-id="435c0-132">첫 번째 드롭다운 목록에 대 한 CascadingDropDown 요소는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-132">Here is the CascadingDropDown element for the first dropdown list:</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample3.aspx)]

<span data-ttu-id="435c0-133">두 번째 목록에 대 한 컨트롤 extender를 설정 해야 합니다.는 `ParentControlID` 연락처 목록의 요소를 연결 로드 공급 업체 목록 트리거에서 항목을 선택 하는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-133">The control extenders for the second list need to set the `ParentControlID` attribute so that selecting an entry in the vendors list triggers loading associated elements in the contacts list.</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample4.aspx)]

<span data-ttu-id="435c0-134">실제 작업은 다음 다음과 같이 설정 된 웹 서비스에서 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-134">The actual work is then done in the web service, which is set up as follows.</span></span> <span data-ttu-id="435c0-135">`[ScriptService]` 특성은 사용, 그렇지 않으면 ASP.NET AJAX 클라이언트 쪽 스크립트 코드에서 웹 메서드를 액세스 하려면 JavaScript 프록시를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-135">Note that the `[ScriptService]` attribute is used, otherwise ASP.NET AJAX cannot create the JavaScript proxy to access the web methods from client-side script code.</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample5.aspx)]

<span data-ttu-id="435c0-136">CascadingDropDown을 호출한 웹 메서드의 시그니처는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-136">The signature of the web methods called by CascadingDropDown is as follows:</span></span>

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample6.vb)]

<span data-ttu-id="435c0-137">반환 값 형식의 배열 이어야 하므로 `CascadingDropDownNameValue` 컨트롤 도구 키트에서 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-137">So the return value must be an array of type `CascadingDropDownNameValue` which is defined by the Control Toolkit.</span></span> <span data-ttu-id="435c0-138">`GetVendors()` 메서드는 구현 하기가 매우 쉽습니다: AdventureWorks 데이터베이스에 연결 하 고 처음 25 명의 공급 업체를 쿼리 하는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-138">The `GetVendors()` method is quite easy to implement: The code connects to the AdventureWorks database and queries the first 25 vendors.</span></span> <span data-ttu-id="435c0-139">첫 번째 매개 변수를 `CascadingDropDownNameValue` 생성자는 두 번째 목록 항목의 캡션을 그 값 (html의 특성 값 &lt; `option` &gt; 요소).</span><span class="sxs-lookup"><span data-stu-id="435c0-139">The first parameter in the `CascadingDropDownNameValue` constructor is the caption of the list entry, the second one its value (value attribute in HTML's &lt;`option`&gt; element).</span></span> <span data-ttu-id="435c0-140">코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-140">Here is the code:</span></span>

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample7.vb)]

<span data-ttu-id="435c0-141">공급 업체에 대 한 연결 된 연락처를 가져오는 (메서드 이름: `GetContactsForVendor()`)는 조금 더 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-141">Getting the associated contacts for a vendor (method name: `GetContactsForVendor()`) is a bit trickier.</span></span> <span data-ttu-id="435c0-142">먼저 첫 번째 드롭다운 목록에서 선택한는 공급 업체를 결정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-142">First of all, the vendor which has been selected in the first dropdown list must be determined.</span></span> <span data-ttu-id="435c0-143">해당 작업에 대 한 도우미 메서드를 정의 하는 컨트롤 도구 키트: 합니다 `ParseKnownCategoryValuesString()` 메서드가 반환 되는 `StringDictionary` 드롭다운 데이터 요소:</span><span class="sxs-lookup"><span data-stu-id="435c0-143">The Control Toolkit defines a helper method for that task: The `ParseKnownCategoryValuesString()` method returns a `StringDictionary` element with the dropdown data:</span></span>

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample8.vb)]

<span data-ttu-id="435c0-144">보안상의 이유로이 데이터를 먼저 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-144">For security reasons, this data must be validated first.</span></span> <span data-ttu-id="435c0-145">공급 업체 항목이 만약 (때문에 합니다 `Category` 첫 번째 CascadingDropDown 요소의 속성이 `"Vendor"`), 선택한 공급 업체의 ID를 검색할 수 있습니다:</span><span class="sxs-lookup"><span data-stu-id="435c0-145">So if there is a Vendor entry (because the `Category` property of the first CascadingDropDown element is set to `"Vendor"`), the ID of the selected vendor may be retrieved:</span></span>

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample9.vb)]

<span data-ttu-id="435c0-146">메서드의 나머지 이면 매우 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-146">The rest of the method is fairly straight-forward, then.</span></span> <span data-ttu-id="435c0-147">공급 업체의 ID는 해당 공급 업체에 대 한 모든 연결 된 연락처를 검색 하는 SQL 쿼리에 대 한 매개 변수로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-147">The vendor's ID is used as a parameter for an SQL query that retrieves all associated contacts for that vendor.</span></span> <span data-ttu-id="435c0-148">다시 한 번 메서드 반환 형식의 배열을 `CascadingDropDownNameValue`합니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-148">Once again, the method returns an array of type `CascadingDropDownNameValue`.</span></span>

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample10.vb)]

<span data-ttu-id="435c0-149">ASP.NET 페이지를 로드 하 고 잠시 후 공급 업체 목록 25 개 항목으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-149">Load the ASP.NET page, and after a short while the vendor list is filled with 25 entries.</span></span> <span data-ttu-id="435c0-150">하나의 항목을 선택 하 고 두 번째 드롭다운 목록을 데이터로 채워지는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="435c0-150">Pick one entry and notice how the second dropdown list is filled with data.</span></span>


<span data-ttu-id="435c0-151">[![첫 번째 목록은 자동으로 채워집니다.](using-cascadingdropdown-with-a-database-vb/_static/image2.png)](using-cascadingdropdown-with-a-database-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="435c0-151">[![The first list is filled automatically](using-cascadingdropdown-with-a-database-vb/_static/image2.png)](using-cascadingdropdown-with-a-database-vb/_static/image1.png)</span></span>

<span data-ttu-id="435c0-152">첫 번째 목록은 자동으로 채워집니다 ([클릭 하 여 큰 이미지 보기](using-cascadingdropdown-with-a-database-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="435c0-152">The first list is filled automatically ([Click to view full-size image](using-cascadingdropdown-with-a-database-vb/_static/image3.png))</span></span>


<span data-ttu-id="435c0-153">[![두 번째 목록의 첫 번째 목록에서 선택 항목에 따라 채워집니다.](using-cascadingdropdown-with-a-database-vb/_static/image5.png)](using-cascadingdropdown-with-a-database-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="435c0-153">[![The second list is filled according to the selection in the first list](using-cascadingdropdown-with-a-database-vb/_static/image5.png)](using-cascadingdropdown-with-a-database-vb/_static/image4.png)</span></span>

<span data-ttu-id="435c0-154">첫 번째 목록에서 선택 항목에 따라 두 번째 목록 채워집니다 ([클릭 하 여 큰 이미지 보기](using-cascadingdropdown-with-a-database-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="435c0-154">The second list is filled according to the selection in the first list ([Click to view full-size image](using-cascadingdropdown-with-a-database-vb/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="435c0-155">[이전](filling-a-list-using-cascadingdropdown-vb.md)
> [다음](presetting-list-entries-with-cascadingdropdown-vb.md)</span><span class="sxs-lookup"><span data-stu-id="435c0-155">[Previous](filling-a-list-using-cascadingdropdown-vb.md)
[Next](presetting-list-entries-with-cascadingdropdown-vb.md)</span></span>
