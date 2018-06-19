---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
title: CascadingDropDown (VB)를 사용 하는 목록 채우기 | Microsoft Docs
author: wenz
description: 변경 내용을 하나의 DropDownList 부하에 관련 된 값이 anoth에 있도록 DropDownList 컨트롤을 확장 하는 AJAX 컨트롤 도구 키트에서 CascadingDropDown 컨트롤 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 5236695e-5c70-4887-baee-0bfb0afb3448
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: e488a30443970d5e2ce825abd96d8e4a027585d1
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30873055"
---
<a name="filling-a-list-using-cascadingdropdown-vb"></a><span data-ttu-id="f22ca-103">CascadingDropDown (VB)를 사용 하는 목록 채우기</span><span class="sxs-lookup"><span data-stu-id="f22ca-103">Filling a List Using CascadingDropDown (VB)</span></span>
====================
<span data-ttu-id="f22ca-104">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="f22ca-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f22ca-105">[코드를 다운로드](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="f22ca-105">[Download Code](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)</span></span>

> <span data-ttu-id="f22ca-106">들어에서 CascadingDropDown 컨트롤 변경 내용을 하나의 DropDownList 부하에 관련 된 값이 다른 DropDownList에 있도록 DropDownList 컨트롤을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f22ca-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="f22ca-107">(예를 들어, 하나의 목록에는 상태, 우리 목록이 및 다음 목록에는 다음 4 개 주요 도시 해당 상태에 채워집니다.) 첫 번째 문제를 해결 하는 실제로이 컨트롤을 사용 하 여 드롭다운 목록 채우기 되려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f22ca-107">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>


## <a name="overview"></a><span data-ttu-id="f22ca-108">개요</span><span class="sxs-lookup"><span data-stu-id="f22ca-108">Overview</span></span>

<span data-ttu-id="f22ca-109">들어에서 CascadingDropDown 컨트롤 변경 내용을 하나의 DropDownList 부하에 관련 된 값이 다른 DropDownList에 있도록 DropDownList 컨트롤을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f22ca-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="f22ca-110">(예를 들어, 하나의 목록에는 상태, 우리 목록이 및 다음 목록에는 다음 4 개 주요 도시 해당 상태에 채워집니다.) 첫 번째 문제를 해결 하는 실제로이 컨트롤을 사용 하 여 드롭다운 목록 채우기 되려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f22ca-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) The first challenge to solve is to actually fill a dropdown list using this control.</span></span>

## <a name="steps"></a><span data-ttu-id="f22ca-111">단계</span><span class="sxs-lookup"><span data-stu-id="f22ca-111">Steps</span></span>

<span data-ttu-id="f22ca-112">ASP.NET AJAX 및 제어 Toolkit의 기능을 활성화 하는 데는 `ScriptManager` 제어 페이지에서 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):</span><span class="sxs-lookup"><span data-stu-id="f22ca-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample1.aspx)]

<span data-ttu-id="f22ca-113">그런 다음 DropDownList 컨트롤이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f22ca-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample2.aspx)]

<span data-ttu-id="f22ca-114">이 목록에 대해 CascadingDropDown extender 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f22ca-114">For this list, a CascadingDropDown extender is added.</span></span> <span data-ttu-id="f22ca-115">다음 목록에 표시 되는 항목의 목록을 반환 하는 웹 서비스에 대 한 비동기 요청을 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="f22ca-115">It will send an asynchronous request to a web service which will then return a list of entries to be displayed in the list.</span></span> <span data-ttu-id="f22ca-116">이렇게 하려면 다음 CascadingDropDown 특성을 설정할 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f22ca-116">For this to work, the following CascadingDropDown attributes need to be set:</span></span>

- <span data-ttu-id="f22ca-117">`ServicePath`: 목록 항목을 제공 하는 웹 서비스의 URL</span><span class="sxs-lookup"><span data-stu-id="f22ca-117">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="f22ca-118">`ServiceMethod`: 목록 항목을 제공 하는 웹 메서드</span><span class="sxs-lookup"><span data-stu-id="f22ca-118">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="f22ca-119">`TargetControlID`: ID의 드롭다운 목록</span><span class="sxs-lookup"><span data-stu-id="f22ca-119">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="f22ca-120">`Category`: 웹 메서드 호출에 제출한 범주 정보</span><span class="sxs-lookup"><span data-stu-id="f22ca-120">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="f22ca-121">`PromptText`: 서버에서 목록 데이터를 비동기적으로 로드할 때 표시 되는 텍스트</span><span class="sxs-lookup"><span data-stu-id="f22ca-121">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>

<span data-ttu-id="f22ca-122">다음은 대 한 태그는 `CascadingDropDown` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="f22ca-122">Here is the markup for the `CascadingDropDown` element.</span></span> <span data-ttu-id="f22ca-123">C# 및 VB 간의 유일한 차이점은 연결 된 웹 서비스의 이름.</span><span class="sxs-lookup"><span data-stu-id="f22ca-123">The only difference between C# and VB is the name of the associated web service:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample3.aspx)]

<span data-ttu-id="f22ca-124">제공 하는 JavaScript 코드는 `CascadingDropDown` extender 다음 서명 사용 하 여 웹 서비스 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="f22ca-124">The JavaScript code coming from the `CascadingDropDown` extender calls a web service method with the following signature:</span></span>

[!code-vb[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample4.vb)]

<span data-ttu-id="f22ca-125">메서드에 필요한 형식의 배열을 반환 하는 중요 한 요소 이므로 `CascadingDropDownNameValue` (ASP.NET AJAX 컨트롤 도구 키트에서 정의 됨).</span><span class="sxs-lookup"><span data-stu-id="f22ca-125">So the important aspect is that the method needs to return an array of type `CascadingDropDownNameValue` (defined by the ASP.NET AJAX Control Toolkit).</span></span> <span data-ttu-id="f22ca-126">에 `CascadingDropDownNameValue` 있는 생성자, 첫 번째 목록 항목의 텍스트와 해당 값을 지정 해야 합니다 마찬가지로 `<option value="VALUE">NAME</option>` html에서을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f22ca-126">In the `CascadingDropDownNameValue` contructor, first the list entry's text and then its value must be provided, just as `<option value="VALUE">NAME</option>` would do in HTML.</span></span> <span data-ttu-id="f22ca-127">예제 데이터는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f22ca-127">Here is some sample data:</span></span>

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample5.aspx)]

<span data-ttu-id="f22ca-128">브라우저에서 페이지를 로드 3 개 공급 업체와 채울 목록을 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f22ca-128">Loading the page in the browser will trigger the list to be filled with three vendors.</span></span>


<span data-ttu-id="f22ca-129">[![자동으로 채워진 목록](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f22ca-129">[![The list is filled automatically](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)</span></span>

<span data-ttu-id="f22ca-130">목록을 자동으로 채워집니다 ([전체 크기 이미지를 보려면 클릭](filling-a-list-using-cascadingdropdown-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="f22ca-130">The list is filled automatically ([Click to view full-size image](filling-a-list-using-cascadingdropdown-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f22ca-131">[이전](using-auto-postback-with-cascadingdropdown-cs.md)
> [다음](using-cascadingdropdown-with-a-database-vb.md)</span><span class="sxs-lookup"><span data-stu-id="f22ca-131">[Previous](using-auto-postback-with-cascadingdropdown-cs.md)
[Next](using-cascadingdropdown-with-a-database-vb.md)</span></span>
