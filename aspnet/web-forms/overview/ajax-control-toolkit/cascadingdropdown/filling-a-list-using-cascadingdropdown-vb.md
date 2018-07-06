---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
title: CascadingDropDown (VB)를 사용 하 여 목록 채우기 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit에서 CascadingDropDown 컨트롤 하나 DropDownList 로드 변경에 관련 된 값이 anoth에 있도록 DropDownList 컨트롤을 확장 하는 중...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: 5236695e-5c70-4887-baee-0bfb0afb3448
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 4a2e2440c0b93fc3945c466a2c60c6560c9e57a4
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37834179"
---
<a name="filling-a-list-using-cascadingdropdown-vb"></a><span data-ttu-id="5f00d-103">CascadingDropDown (VB)를 사용 하 여 목록 채우기</span><span class="sxs-lookup"><span data-stu-id="5f00d-103">Filling a List Using CascadingDropDown (VB)</span></span>
====================
<span data-ttu-id="5f00d-104">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="5f00d-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="5f00d-105">[코드를 다운로드](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="5f00d-105">[Download Code](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)</span></span>

> <span data-ttu-id="5f00d-106">AJAX Control Toolkit에서 CascadingDropDown 컨트롤 하나 DropDownList 로드 변경에 관련 된 값이 다른 DropDownList에 있도록 DropDownList 컨트롤을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f00d-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="5f00d-107">(예를 들어 미국 주 목록을 제공 하는 하나의 목록 및 해당 상태의 주요 도시를 사용 하 여 다음 목록에 다음 채워집니다.) 첫 번째 문제를 해결 하려면 실제로이 컨트롤을 사용 하 여 드롭다운 목록을 채우는 방법은입니다.</span><span class="sxs-lookup"><span data-stu-id="5f00d-107">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>


## <a name="overview"></a><span data-ttu-id="5f00d-108">개요</span><span class="sxs-lookup"><span data-stu-id="5f00d-108">Overview</span></span>

<span data-ttu-id="5f00d-109">AJAX Control Toolkit에서 CascadingDropDown 컨트롤 하나 DropDownList 로드 변경에 관련 된 값이 다른 DropDownList에 있도록 DropDownList 컨트롤을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f00d-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="5f00d-110">(예를 들어 미국 주 목록을 제공 하는 하나의 목록 및 해당 상태의 주요 도시를 사용 하 여 다음 목록에 다음 채워집니다.) 첫 번째 문제를 해결 하려면 실제로이 컨트롤을 사용 하 여 드롭다운 목록을 채우는 방법은입니다.</span><span class="sxs-lookup"><span data-stu-id="5f00d-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="steps"></a><span data-ttu-id="5f00d-111">단계</span><span class="sxs-lookup"><span data-stu-id="5f00d-111">Steps</span></span>

<span data-ttu-id="5f00d-112">ASP.NET AJAX와 Control Toolkit의 기능을 활성화 하기 위해 합니다 `ScriptManager` 컨트롤 페이지의 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):</span><span class="sxs-lookup"><span data-stu-id="5f00d-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample1.aspx)]

<span data-ttu-id="5f00d-113">DropDownList 컨트롤은 그런 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f00d-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample2.aspx)]

<span data-ttu-id="5f00d-114">이 목록에 대해 CascadingDropDown extender 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f00d-114">For this list, a CascadingDropDown extender is added.</span></span> <span data-ttu-id="5f00d-115">이 비동기 요청을 한 다음 목록에 표시할 항목의 목록을 반환 하는 웹 서비스에 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f00d-115">It will send an asynchronous request to a web service which will then return a list of entries to be displayed in the list.</span></span> <span data-ttu-id="5f00d-116">이렇게 하려면 다음 CascadingDropDown 특성 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f00d-116">For this to work, the following CascadingDropDown attributes need to be set:</span></span>

- <span data-ttu-id="5f00d-117">`ServicePath`: 목록 항목을 제공 하는 웹 서비스의 URL</span><span class="sxs-lookup"><span data-stu-id="5f00d-117">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="5f00d-118">`ServiceMethod`합니다: 목록 항목을 제공 웹 메서드</span><span class="sxs-lookup"><span data-stu-id="5f00d-118">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="5f00d-119">`TargetControlID`: 드롭다운 목록의 ID</span><span class="sxs-lookup"><span data-stu-id="5f00d-119">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="5f00d-120">`Category`: 웹 메서드 호출에 제출 된 범주 정보</span><span class="sxs-lookup"><span data-stu-id="5f00d-120">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="5f00d-121">`PromptText`: 비동기적으로 서버에서 목록 데이터를 로드할 때 표시 되는 텍스트</span><span class="sxs-lookup"><span data-stu-id="5f00d-121">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>

<span data-ttu-id="5f00d-122">여기에 대 한 태그는 `CascadingDropDown` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="5f00d-122">Here is the markup for the `CascadingDropDown` element.</span></span> <span data-ttu-id="5f00d-123">C# 및 VB 간의 유일한 차이점은 연결 된 웹 서비스의 이름.</span><span class="sxs-lookup"><span data-stu-id="5f00d-123">The only difference between C# and VB is the name of the associated web service:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample3.aspx)]

<span data-ttu-id="5f00d-124">들어오는 JavaScript 코드는 `CascadingDropDown` extender는 다음 서명 사용 하 여 웹 서비스 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f00d-124">The JavaScript code coming from the `CascadingDropDown` extender calls a web service method with the following signature:</span></span>

[!code-vb[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample4.vb)]

<span data-ttu-id="5f00d-125">중요 한 점은 메서드 형식의 배열을 반환 해야 하므로 `CascadingDropDownNameValue` (ASP.NET AJAX Control Toolkit에서 정의 됨).</span><span class="sxs-lookup"><span data-stu-id="5f00d-125">So the important aspect is that the method needs to return an array of type `CascadingDropDownNameValue` (defined by the ASP.NET AJAX Control Toolkit).</span></span> <span data-ttu-id="5f00d-126">에 `CascadingDropDownNameValue` 생성자를 첫 번째 목록 항목의 텍스트를 가져온 다음 해당 값을 지정 해야 합니다 처럼 `<option value="VALUE">NAME</option>` HTML에서.</span><span class="sxs-lookup"><span data-stu-id="5f00d-126">In the `CascadingDropDownNameValue` contructor, first the list entry's text and then its value must be provided, just as `<option value="VALUE">NAME</option>` would do in HTML.</span></span> <span data-ttu-id="5f00d-127">몇 가지 샘플 데이터는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5f00d-127">Here is some sample data:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample5.aspx)]

<span data-ttu-id="5f00d-128">브라우저에서 페이지 로드 3 개 공급 업체를 사용 하 여 채울 목록을 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f00d-128">Loading the page in the browser will trigger the list to be filled with three vendors.</span></span>


<span data-ttu-id="5f00d-129">[![자동으로 채워집니다.](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5f00d-129">[![The list is filled automatically](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)</span></span>

<span data-ttu-id="5f00d-130">자동으로 채워집니다 ([클릭 하 여 큰 이미지 보기](filling-a-list-using-cascadingdropdown-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="5f00d-130">The list is filled automatically ([Click to view full-size image](filling-a-list-using-cascadingdropdown-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5f00d-131">[이전](using-auto-postback-with-cascadingdropdown-cs.md)
> [다음](using-cascadingdropdown-with-a-database-vb.md)</span><span class="sxs-lookup"><span data-stu-id="5f00d-131">[Previous](using-auto-postback-with-cascadingdropdown-cs.md)
[Next](using-cascadingdropdown-with-a-database-vb.md)</span></span>
