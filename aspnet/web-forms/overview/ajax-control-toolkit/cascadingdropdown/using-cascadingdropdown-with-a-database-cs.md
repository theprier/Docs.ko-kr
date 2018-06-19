---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
title: CascadingDropDown 데이터베이스 (C#)와 함께 사용 하 여 | Microsoft Docs
author: wenz
description: 변경 내용을 하나의 DropDownList 부하에 관련 된 값이 anoth에 있도록 DropDownList 컨트롤을 확장 하는 AJAX 컨트롤 도구 키트에서 CascadingDropDown 컨트롤 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 684f0c28-a490-4e5b-b5e5-5dfb77464b49
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
msc.type: authoredcontent
ms.openlocfilehash: 1991c26d408e593999288ea6df0467cea0369457
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30879129"
---
<a name="using-cascadingdropdown-with-a-database-c"></a><span data-ttu-id="7484f-103">CascadingDropDown를 사용 하 여 데이터베이스 (C#)</span><span class="sxs-lookup"><span data-stu-id="7484f-103">Using CascadingDropDown with a Database (C#)</span></span>
====================
<span data-ttu-id="7484f-104">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="7484f-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="7484f-105">[코드를 다운로드](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="7484f-105">[Download Code](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1CS.pdf)</span></span>

> <span data-ttu-id="7484f-106">들어에서 CascadingDropDown 컨트롤 변경 내용을 하나의 DropDownList 부하에 관련 된 값이 다른 DropDownList에 있도록 DropDownList 컨트롤을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="7484f-107">이 작업을 위해 특수 한 웹 서비스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-107">In order for this to work, a special web service must be created.</span></span>


## <a name="overview"></a><span data-ttu-id="7484f-108">개요</span><span class="sxs-lookup"><span data-stu-id="7484f-108">Overview</span></span>

<span data-ttu-id="7484f-109">들어에서 CascadingDropDown 컨트롤 변경 내용을 하나의 DropDownList 부하에 관련 된 값이 다른 DropDownList에 있도록 DropDownList 컨트롤을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="7484f-110">(예를 들어, 하나의 목록에는 상태, 우리 목록이 및 다음 목록에는 다음 4 개 주요 도시 해당 상태에 채워집니다.) 이 작업을 위해 특수 한 웹 서비스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) In order for this to work, a special web service must be created.</span></span>

## <a name="steps"></a><span data-ttu-id="7484f-111">단계</span><span class="sxs-lookup"><span data-stu-id="7484f-111">Steps</span></span>

<span data-ttu-id="7484f-112">첫째, 데이터 소스는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-112">First of all, a data source is required.</span></span> <span data-ttu-id="7484f-113">이 샘플에서는 AdventureWorks 데이터베이스 및 Microsoft SQL Server 2005 Express Edition을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-113">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="7484f-114">데이터베이스 (express edition 포함)는 Visual Studio 설치의 선택적 부분이 며에서 별도 다운로드로 제공 됩니다 [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)합니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-114">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="7484f-115">AdventureWorks 데이터베이스의 SQL Server 2005 예제 및 예제 데이터베이스의 일부인 (다운로드에서 [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e &amp;4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="7484f-115">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="7484f-116">Microsoft SQL Server Management Studio Express를 사용 하는 가장 쉬운 방법은 데이터베이스를 설정 하는 ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) 및 연결 된 `AdventureWorks.mdf` 데이터베이스 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-116">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="7484f-117">이 샘플에 대 한 SQL Server 2005 Express Edition 인스턴스 라고 가정 `SQLEXPRESS` 웹 서버와 동일한 컴퓨터에 상주 하 고 기본 설정 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="7484f-118">설정에 다른 경우 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="7484f-119">ASP.NET AJAX 및 제어 Toolkit의 기능을 활성화 하는 데는 `ScriptManager` 제어 페이지에서 아무 곳 이나 배치 해야 합니다 (하지만 내는 &lt; `form` &gt; 요소):</span><span class="sxs-lookup"><span data-stu-id="7484f-119">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the &lt;`form`&gt; element):</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample1.aspx)]

<span data-ttu-id="7484f-120">다음 단계에서는 두 개의 DropDownList 컨트롤은 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-120">In the next step, two DropDownList controls are required.</span></span> <span data-ttu-id="7484f-121">이 샘플에서 AdventureWorks에서 공급 업체와 연락처 정보는 사용, 사용 가능한 공급 업체 및 사용할 수 있는 연락처에 대 한 하나의 목록 따라서 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-121">In this sample, we use the vendor and contact information from AdventureWorks, thus we create one list for the available vendors and one for the available contacts:</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample2.aspx)]

<span data-ttu-id="7484f-122">그런 다음 두 개의 CascadingDropDown extender 페이지에 추가 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-122">Then, two CascadingDropDown extenders must be added to the page.</span></span> <span data-ttu-id="7484f-123">첫 번째 (공급 업체) 목록 하나 채우고 다른 두 번째 (연락처) 목록을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-123">One fills the first (vendors) list, and the other one fills the second (contacts) list.</span></span> <span data-ttu-id="7484f-124">다음과 같은 특성을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-124">The following attributes must be set:</span></span>

- <span data-ttu-id="7484f-125">`ServicePath`: 목록 항목을 제공 하는 웹 서비스의 URL</span><span class="sxs-lookup"><span data-stu-id="7484f-125">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="7484f-126">`ServiceMethod`: 목록 항목을 제공 하는 웹 메서드</span><span class="sxs-lookup"><span data-stu-id="7484f-126">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="7484f-127">`TargetControlID`: ID의 드롭다운 목록</span><span class="sxs-lookup"><span data-stu-id="7484f-127">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="7484f-128">`Category`: 웹 메서드 호출에 제출한 범주 정보</span><span class="sxs-lookup"><span data-stu-id="7484f-128">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="7484f-129">`PromptText`: 서버에서 목록 데이터를 비동기적으로 로드할 때 표시 되는 텍스트</span><span class="sxs-lookup"><span data-stu-id="7484f-129">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>
- <span data-ttu-id="7484f-130">`ParentControlID`: (선택 사항) 부모 드롭다운 목록 현재 목록 해당 트리거 로드</span><span class="sxs-lookup"><span data-stu-id="7484f-130">`ParentControlID`: (optional) parent dropdown list that triggers loading of the current list</span></span>

<span data-ttu-id="7484f-131">사용 되는 프로그래밍 언어에 따라 해당 웹 서비스의 이름 변경 되지만 다른 모든 특성 값이 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-131">Depending on the programming language used, the name of the web service in question changes, but all other attribute values are the same.</span></span> <span data-ttu-id="7484f-132">첫 번째 드롭다운 목록에 대 한 CascadingDropDown 요소는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-132">Here is the CascadingDropDown element for the first dropdown list:</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample3.aspx)]

<span data-ttu-id="7484f-133">두 번째 목록에 대 한 컨트롤 extender를 설정 해야 합니다.는 `ParentControlID` 특성 관련 된 연락처 목록에 있는 요소를 로드 하는 공급 업체 목록 트리거에서 항목을 선택 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-133">The control extenders for the second list need to set the `ParentControlID` attribute so that selecting an entry in the vendors list triggers loading associated elements in the contacts list.</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample4.aspx)]

<span data-ttu-id="7484f-134">다음 다음과 같이 설정 하는 웹 서비스의 실제 작업 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-134">The actual work is then done in the web service, which is set up as follows.</span></span> <span data-ttu-id="7484f-135">`[ScriptService]` 특성은 사용, 그렇지 않으면 ASP.NET AJAX 클라이언트 쪽 스크립트 코드에서 웹 메서드를 액세스 하는 JavaScript 프록시를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-135">Note that the `[ScriptService]` attribute is used, otherwise ASP.NET AJAX cannot create the JavaScript proxy to access the web methods from client-side script code.</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample5.aspx)]

<span data-ttu-id="7484f-136">CascadingDropDown 호출한 웹 메서드의 시그니처는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-136">The signature of the web methods called by CascadingDropDown is as follows:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample6.cs)]

<span data-ttu-id="7484f-137">이므로 반환 값 형식의 배열 이어야 합니다. `CascadingDropDownNameValue` 제어 도구 키트에서 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-137">So the return value must be an array of type `CascadingDropDownNameValue` which is defined by the Control Toolkit.</span></span> <span data-ttu-id="7484f-138">`GetVendors()` 구현할 수 있는 쉬운 방법은: 코드 AdventureWorks 데이터베이스에 연결 하 고 처음 25 명의 공급 업체를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-138">The `GetVendors()` method is quite easy to implement: The code connects to the AdventureWorks database and queries the first 25 vendors.</span></span> <span data-ttu-id="7484f-139">첫 번째 매개 변수는 `CascadingDropDownNameValue` 생성자는 두 번째 목록 항목의 캡션을 해당 값 (HTML의에서 value 특성 &lt; `option` &gt; 요소).</span><span class="sxs-lookup"><span data-stu-id="7484f-139">The first parameter in the `CascadingDropDownNameValue` constructor is the caption of the list entry, the second one its value (value attribute in HTML's &lt;`option`&gt; element).</span></span> <span data-ttu-id="7484f-140">코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-140">Here is the code:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample7.cs)]

<span data-ttu-id="7484f-141">공급 업체에 대 한 연결 된 연락처를 가져오는 (메서드 이름: `GetContactsForVendor()`)는 조금 더 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-141">Getting the associated contacts for a vendor (method name: `GetContactsForVendor()`) is a bit trickier.</span></span> <span data-ttu-id="7484f-142">우선, 첫 번째 드롭다운 목록에서 선택 된 공급 업체를 결정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-142">First of all, the vendor which has been selected in the first dropdown list must be determined.</span></span> <span data-ttu-id="7484f-143">해당 작업에 대 한 도우미 메서드를 정의 하는 컨트롤 Toolkit:는 `ParseKnownCategoryValuesString()` 메서드가 반환 되는 `StringDictionary` 드롭다운 데이터 요소:</span><span class="sxs-lookup"><span data-stu-id="7484f-143">The Control Toolkit defines a helper method for that task: The `ParseKnownCategoryValuesString()` method returns a `StringDictionary` element with the dropdown data:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample8.cs)]

<span data-ttu-id="7484f-144">보안상의 이유로이 데이터를 먼저 확인할 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-144">For security reasons, this data must be validated first.</span></span> <span data-ttu-id="7484f-145">공급 업체 항목이 있는 경우에 따라서 (때문에 `Category` 첫 번째 CascadingDropDown 요소의 속성이로 설정 되어 `"Vendor"`), 선택한 공급 업체의 ID를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-145">So if there is a Vendor entry (because the `Category` property of the first CascadingDropDown element is set to `"Vendor"`), the ID of the selected vendor may be retrieved:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample9.cs)]

<span data-ttu-id="7484f-146">메서드의 나머지 부분은 매우 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-146">The rest of the method is fairly straight-forward, then.</span></span> <span data-ttu-id="7484f-147">공급 업체의 ID는 해당 공급 업체에 대 한 모든 연결 된 연락처를 검색 하는 SQL 쿼리를 매개 변수로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-147">The vendor's ID is used as a parameter for an SQL query that retrieves all associated contacts for that vendor.</span></span> <span data-ttu-id="7484f-148">다시 한 번 메서드 반환 형식의 배열을 `CascadingDropDownNameValue`합니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-148">Once again, the method returns an array of type `CascadingDropDownNameValue`.</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample10.cs)]

<span data-ttu-id="7484f-149">ASP.NET 페이지를 로드 하 고 잠시 후 공급 업체 목록 25 개 항목으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-149">Load the ASP.NET page, and after a short while the vendor list is filled with 25 entries.</span></span> <span data-ttu-id="7484f-150">하나의 항목을 선택 하 고 두 번째 드롭다운 목록 데이터로 채워지는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7484f-150">Pick one entry and notice how the second dropdown list is filled with data.</span></span>


<span data-ttu-id="7484f-151">[![첫 번째 목록이 자동으로 채워질 때](using-cascadingdropdown-with-a-database-cs/_static/image2.png)](using-cascadingdropdown-with-a-database-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7484f-151">[![The first list is filled automatically](using-cascadingdropdown-with-a-database-cs/_static/image2.png)](using-cascadingdropdown-with-a-database-cs/_static/image1.png)</span></span>

<span data-ttu-id="7484f-152">첫 번째 목록을 자동으로 채워집니다 ([전체 크기 이미지를 보려면 클릭](using-cascadingdropdown-with-a-database-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="7484f-152">The first list is filled automatically ([Click to view full-size image](using-cascadingdropdown-with-a-database-cs/_static/image3.png))</span></span>


<span data-ttu-id="7484f-153">[![두 번째 목록에서 첫 번째 목록에서 선택한 옵션에 따라 채워집니다.](using-cascadingdropdown-with-a-database-cs/_static/image5.png)](using-cascadingdropdown-with-a-database-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="7484f-153">[![The second list is filled according to the selection in the first list](using-cascadingdropdown-with-a-database-cs/_static/image5.png)](using-cascadingdropdown-with-a-database-cs/_static/image4.png)</span></span>

<span data-ttu-id="7484f-154">두 번째 목록에서 첫 번째 목록에서 선택한 옵션에 따라 채워집니다 ([전체 크기 이미지를 보려면 클릭](using-cascadingdropdown-with-a-database-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="7484f-154">The second list is filled according to the selection in the first list ([Click to view full-size image](using-cascadingdropdown-with-a-database-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7484f-155">[이전](filling-a-list-using-cascadingdropdown-cs.md)
> [다음](presetting-list-entries-with-cascadingdropdown-cs.md)</span><span class="sxs-lookup"><span data-stu-id="7484f-155">[Previous](filling-a-list-using-cascadingdropdown-cs.md)
[Next](presetting-list-entries-with-cascadingdropdown-cs.md)</span></span>
