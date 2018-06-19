---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-vb
title: 자동 다시 게시를 사용 하 여 CascadingDropDown (VB)으로 | Microsoft Docs
author: wenz
description: 변경 내용을 하나의 DropDownList 부하에 관련 된 값이 anoth에 있도록 DropDownList 컨트롤을 확장 하는 AJAX 컨트롤 도구 키트에서 CascadingDropDown 컨트롤 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 0b34f7f6-a0cc-4b9f-9761-643fb0bb3ece
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: e8a48692dd96ee6a647bfb57ce2915b4e85544fe
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30871378"
---
<a name="using-auto-postback-with-cascadingdropdown-vb"></a><span data-ttu-id="55ad8-103">자동 다시 게시를 사용 하 여 CascadingDropDown (VB)으로</span><span class="sxs-lookup"><span data-stu-id="55ad8-103">Using Auto-Postback with CascadingDropDown (VB)</span></span>
====================
<span data-ttu-id="55ad8-104">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="55ad8-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="55ad8-105">[코드를 다운로드](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="55ad8-105">[Download Code](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3VB.pdf)</span></span>

> <span data-ttu-id="55ad8-106">들어에서 CascadingDropDown 컨트롤 변경 내용을 하나의 DropDownList 부하에 관련 된 값이 다른 DropDownList에 있도록 DropDownList 컨트롤을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="55ad8-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="55ad8-107">그러나 ASP CascadingDropDown 컨트롤을 사용 하는 경우. 목록에 데이터를 비동기적으로 로드 자체는 (불필요 한) 포스트백을 생성 하므로 NET의 DropDownList 컨트롤 AutoPostBack 기능이 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="55ad8-107">However when using the CascadingDropDown control, ASP.NET's DropDownList control's AutoPostBack feature does not work, since asynchronously loading data into the list generates an (unnecessary) postback itself.</span></span> <span data-ttu-id="55ad8-108">일부 JavaScript 코드와 함께이 효과 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55ad8-108">With some JavaScript code, this effect can be avoided.</span></span>


## <a name="overview"></a><span data-ttu-id="55ad8-109">개요</span><span class="sxs-lookup"><span data-stu-id="55ad8-109">Overview</span></span>

<span data-ttu-id="55ad8-110">들어에서 CascadingDropDown 컨트롤 변경 내용을 하나의 DropDownList 부하에 관련 된 값이 다른 DropDownList에 있도록 DropDownList 컨트롤을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="55ad8-110">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="55ad8-111">(예를 들어, 하나의 목록에는 상태, 우리 목록이 및 다음 목록에는 다음 4 개 주요 도시 해당 상태에 채워집니다.) 그러나 ASP CascadingDropDown 컨트롤을 사용 하는 경우. 목록에 데이터를 비동기적으로 로드 자체는 (불필요 한) 포스트백을 생성 하므로 NET의 DropDownList 컨트롤 AutoPostBack 기능이 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="55ad8-111">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) However when using the CascadingDropDown control, ASP.NET's DropDownList control's AutoPostBack feature does not work, since asynchronously loading data into the list generates an (unnecessary) postback itself.</span></span> <span data-ttu-id="55ad8-112">일부 JavaScript 코드와 함께이 효과 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55ad8-112">With some JavaScript code, this effect can be avoided.</span></span>

## <a name="steps"></a><span data-ttu-id="55ad8-113">단계</span><span class="sxs-lookup"><span data-stu-id="55ad8-113">Steps</span></span>

<span data-ttu-id="55ad8-114">ASP.NET AJAX 및 제어 Toolkit의 기능을 활성화 하는 데는 `ScriptManager` 제어 페이지에서 아무 곳 이나 배치 해야 합니다 (하지만 내는 &lt; `form` &gt; 요소):</span><span class="sxs-lookup"><span data-stu-id="55ad8-114">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the &lt;`form`&gt; element):</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample1.aspx)]

<span data-ttu-id="55ad8-115">그런 다음 DropDownList 컨트롤이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="55ad8-115">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample2.aspx)]

<span data-ttu-id="55ad8-116">이 목록에 대 한 웹 서비스 URL과 메서드 정보를 제공 하는 CascadingDropDown extender 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55ad8-116">For this list, a CascadingDropDown extender is added, providing web service URL and method information:</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample3.aspx)]

<span data-ttu-id="55ad8-117">CascadingDropDown extender 다음 비동기적으로 호출 다음 메서드 서명 사용 하 여 웹 서비스:</span><span class="sxs-lookup"><span data-stu-id="55ad8-117">The CascadingDropDown extender then asynchronously calls a web service with the following method signature:</span></span>

[!code-vb[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample4.vb)]

<span data-ttu-id="55ad8-118">메서드가는 CascadingDropDown 값 형식의 배열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="55ad8-118">The method returns an array of type CascadingDropDown value.</span></span> <span data-ttu-id="55ad8-119">목록 항목의 캡션 및 값 형식의 생성자에 먼저 인수가 (HTML `value` 특성).</span><span class="sxs-lookup"><span data-stu-id="55ad8-119">The type's constructor expects first the list entry's caption and then the value (HTML `value` attribute).</span></span>

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample5.aspx)]

<span data-ttu-id="55ad8-120">브라우저에서 페이지를 로드를 채워 드롭다운 목록 3 개 공급 업체에 미리 선택 되 고 두 번째 식 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55ad8-120">Loading the page in the browser will fill the dropdown list with three vendors, the second one being preselected.</span></span> <span data-ttu-id="55ad8-121">또한 ASP.NET 정의 `__doPostBack()` JavaScript 메서드.</span><span class="sxs-lookup"><span data-stu-id="55ad8-121">Also, ASP.NET defines the `__doPostBack()` JavaScript method.</span></span> <span data-ttu-id="55ad8-122">페이지가 로드 되 면이 JavaScript 호출만 하는 경우에이 요소가 있지만 드롭다운 목록에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55ad8-122">Once the page has been loaded, this JavaScript call is added to the dropdown list, but only if there are elements in it.</span></span> <span data-ttu-id="55ad8-123">목록에 요소가 있는 경우 제어 도구 키트를 현재 로드, 하므로 JavaScript 코드는 제한 시간을 사용 하 여 하 고 1/2 초 후에 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="55ad8-123">If there are no elements in the list, the Control Toolkit is currently loading them, so the JavaScript code uses a timeout and tries again in a half second.</span></span>

[!code-html[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample6.html)]

<span data-ttu-id="55ad8-124">이러한 방식으로 목록 실제로 요소는이 고 사용자가 항목을 선택할 때 포스트백 실행만 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55ad8-124">This way, a postback is only executed when there are actually elements in the list and the user selects an entry.</span></span>


<span data-ttu-id="55ad8-125">[![포스트백 목록 요소를 선택 하면](using-auto-postback-with-cascadingdropdown-vb/_static/image2.png)](using-auto-postback-with-cascadingdropdown-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="55ad8-125">[![Selecting a list element causes a postback](using-auto-postback-with-cascadingdropdown-vb/_static/image2.png)](using-auto-postback-with-cascadingdropdown-vb/_static/image1.png)</span></span>

<span data-ttu-id="55ad8-126">포스트백 목록 요소를 선택 하면 ([전체 크기 이미지를 보려면 클릭](using-auto-postback-with-cascadingdropdown-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="55ad8-126">Selecting a list element causes a postback ([Click to view full-size image](using-auto-postback-with-cascadingdropdown-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="55ad8-127">이전</span><span class="sxs-lookup"><span data-stu-id="55ad8-127">Previous</span></span>](presetting-list-entries-with-cascadingdropdown-vb.md)
