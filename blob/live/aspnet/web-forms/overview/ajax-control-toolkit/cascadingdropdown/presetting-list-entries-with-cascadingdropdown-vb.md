---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-vb
title: "목록 항목 CascadingDropDown (VB)으로 미리 설정 | Microsoft Docs"
author: wenz
description: "변경 내용을 하나의 DropDownList 부하에 관련 된 값이 anoth에 있도록 DropDownList 컨트롤을 확장 하는 AJAX 컨트롤 도구 키트에서 CascadingDropDown 컨트롤 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: ec61ced7-bbca-4bdd-aa3b-80878f295181
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: c28c7893c39d9ba9f828c34da7ffdce525ee248e
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="presetting-list-entries-with-cascadingdropdown-vb"></a><span data-ttu-id="07145-103">목록 항목 CascadingDropDown (VB)으로 미리 설정</span><span class="sxs-lookup"><span data-stu-id="07145-103">Presetting List Entries with CascadingDropDown (VB)</span></span>
====================
<span data-ttu-id="07145-104">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="07145-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="07145-105">[코드를 다운로드](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/CascadingDropDown2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="07145-105">[Download Code](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/CascadingDropDown2VB.pdf)</span></span>

> <span data-ttu-id="07145-106">들어에서 CascadingDropDown 컨트롤 변경 내용을 하나의 DropDownList 부하에 관련 된 값이 다른 DropDownList에 있도록 DropDownList 컨트롤을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="07145-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="07145-107">약간의 코드와 불가능 한 데이터를 동적으로 로드 되 면 목록 요소는 미리 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07145-107">With a little bit of code it is possible that a list element is preselected once the data has been dynamically loaded.</span></span>


## <a name="overview"></a><span data-ttu-id="07145-108">개요</span><span class="sxs-lookup"><span data-stu-id="07145-108">Overview</span></span>

<span data-ttu-id="07145-109">들어에서 CascadingDropDown 컨트롤 변경 내용을 하나의 DropDownList 부하에 관련 된 값이 다른 DropDownList에 있도록 DropDownList 컨트롤을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="07145-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="07145-110">(예를 들어, 하나의 목록에는 상태, 우리 목록이 및 다음 목록에는 다음 4 개 주요 도시 해당 상태에 채워집니다.) 약간의 코드와 불가능 한 데이터를 동적으로 로드 되 면 목록 요소는 미리 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07145-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) With a little bit of code it is possible that a list element is preselected once the data has been dynamically loaded.</span></span>

## <a name="steps"></a><span data-ttu-id="07145-111">단계</span><span class="sxs-lookup"><span data-stu-id="07145-111">Steps</span></span>

<span data-ttu-id="07145-112">ASP.NET AJAX 및 제어 Toolkit의 기능을 활성화 하는 데는 `ScriptManager` 제어 페이지에서 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):</span><span class="sxs-lookup"><span data-stu-id="07145-112">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample1.aspx)]

<span data-ttu-id="07145-113">그런 다음 DropDownList 컨트롤이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="07145-113">Then, a DropDownList control is required:</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample2.aspx)]

<span data-ttu-id="07145-114">이 목록에 대 한 웹 서비스 URL과 메서드 정보를 제공 하는 CascadingDropDown extender 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07145-114">For this list, a CascadingDropDown extender is added, providing web service URL and method information:</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample3.aspx)]

<span data-ttu-id="07145-115">CascadingDropDown extender 다음 비동기적으로 호출 다음 메서드 서명 사용 하 여 웹 서비스:</span><span class="sxs-lookup"><span data-stu-id="07145-115">The CascadingDropDown extender then asynchronously calls a web service with the following method signature:</span></span>

[!code-vb[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample4.vb)]

<span data-ttu-id="07145-116">메서드가는 CascadingDropDown 값 형식의 배열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="07145-116">The method returns an array of type CascadingDropDown value.</span></span> <span data-ttu-id="07145-117">목록 항목의 캡션 및 값 형식의 생성자에 먼저 인수가 (HTML `value` 특성).</span><span class="sxs-lookup"><span data-stu-id="07145-117">The type's constructor expects first the list entry's caption and then the value (HTML `value` attribute).</span></span> <span data-ttu-id="07145-118">세 번째 인수를 설정 하는 경우 true, 목록에 요소가 자동으로 선택 됩니다 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="07145-118">If the third argument is set to true, the list element is automatically selected in the browser.</span></span>

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample5.aspx)]

<span data-ttu-id="07145-119">브라우저에서 페이지를 로드를 채워 드롭다운 목록 3 개 공급 업체에 미리 선택 되 고 두 번째 식 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07145-119">Loading the page in the browser will fill the dropdown list with three vendors, the second one being preselected.</span></span>


<span data-ttu-id="07145-120">[![목록 채우기 및 자동으로 미리 선택](presetting-list-entries-with-cascadingdropdown-vb/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="07145-120">[![The list is filled and preselected automatically](presetting-list-entries-with-cascadingdropdown-vb/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-vb/_static/image1.png)</span></span>

<span data-ttu-id="07145-121">목록 채우기 및 자동으로 미리 선택 ([전체 크기 이미지를 보려면 클릭](presetting-list-entries-with-cascadingdropdown-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="07145-121">The list is filled and preselected automatically ([Click to view full-size image](presetting-list-entries-with-cascadingdropdown-vb/_static/image3.png))</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="07145-122">[이전](using-cascadingdropdown-with-a-database-vb.md)
[다음](using-auto-postback-with-cascadingdropdown-vb.md)</span><span class="sxs-lookup"><span data-stu-id="07145-122">[Previous](using-cascadingdropdown-with-a-database-vb.md)
[Next](using-auto-postback-with-cascadingdropdown-vb.md)</span></span>
