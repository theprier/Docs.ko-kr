---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-vb
title: 동적으로 컨트롤 (VB)를 채우기 | Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit에 DynamicPopulate 컨트롤은 웹 서비스 (또는 페이지 메서드)를 호출 하 고 t 대상 컨트롤에 결과 값을 채웁니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 27305347-7b5d-4519-97b7-197a357e7f6e
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-vb
msc.type: authoredcontent
ms.openlocfilehash: fd55b59f9375eb320711ffea8d971a8d86179c43
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37368662"
---
<a name="dynamically-populating-a-control-vb"></a><span data-ttu-id="a5a9b-103">동적으로 채울 컨트롤 (VB)</span><span class="sxs-lookup"><span data-stu-id="a5a9b-103">Dynamically Populating a Control (VB)</span></span>
====================
<span data-ttu-id="a5a9b-104">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="a5a9b-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a5a9b-105">[코드를 다운로드](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="a5a9b-105">[Download Code](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0VB.pdf)</span></span>

> <span data-ttu-id="a5a9b-106">ASP.NET AJAX Control Toolkit에 DynamicPopulate 제어는 웹 서비스 (또는 페이지 메서드)를 호출 하 고 페이지 새로 고침 없이 페이지에서 대상 컨트롤에 결과 값을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9b-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span>


## <a name="overview"></a><span data-ttu-id="a5a9b-107">개요</span><span class="sxs-lookup"><span data-stu-id="a5a9b-107">Overview</span></span>

<span data-ttu-id="a5a9b-108">`DynamicPopulate` ASP.NET AJAX Control Toolkit의 컨트롤을 웹 서비스 (또는 페이지 메서드)를 호출 하 고 페이지 새로 고침 없이 페이지에서 대상 컨트롤에 결과 값을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9b-108">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="a5a9b-109">이 자습서에는이를 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9b-109">This tutorial shows how to set this up.</span></span>

## <a name="steps"></a><span data-ttu-id="a5a9b-110">단계</span><span class="sxs-lookup"><span data-stu-id="a5a9b-110">Steps</span></span>

<span data-ttu-id="a5a9b-111">호출할 메서드를 구현 하는 ASP.NET 웹 서비스 해야 먼저 `DynamicPopulate`합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9b-111">First of all, you need an ASP.NET Web Service which implements the method to be called by `DynamicPopulate`.</span></span> <span data-ttu-id="a5a9b-112">웹 서비스 클래스에 필요 합니다 `ScriptService` 내에 정의 된 특성 `Microsoft.Web.Script.Services`; ASP.NET AJAX에 필요한 웹 서비스에 대 한 클라이언트 쪽 JavaScript 프록시를 만들 수 없습니다이 고, 그렇지 `DynamicPopulate`합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9b-112">The web service class requires the `ScriptService` attribute which is defined within `Microsoft.Web.Script.Services`; otherwise ASP.NET AJAX cannot create the client-side JavaScript proxy for the web service which in turn is required by `DynamicPopulate`.</span></span>

<span data-ttu-id="a5a9b-113">웹 메서드는 문자열 형식의 호출 인수 하나를 예상 해야 합니다 `contextKey`, 이후는 `DynamicPopulate` 컨트롤이 각 웹 서비스 호출을 사용 하 여 한 가지 상황에 맞는 정보를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9b-113">The web method must expect one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="a5a9b-114">표시 형식으로 현재 날짜를 반환 하는 다음 웹 서비스는 `contextKey` 인수:</span><span class="sxs-lookup"><span data-stu-id="a5a9b-114">The following web service returns the current date in a format represented by the `contextKey` argument:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample1.aspx)]

<span data-ttu-id="a5a9b-115">웹 서비스로 저장 됩니다 `DynamicPopulate.vb.asmx`합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9b-115">The web service is then saved as `DynamicPopulate.vb.asmx`.</span></span> <span data-ttu-id="a5a9b-116">구현할 수 있습니다 합니다 `getDate()` 실제 ASP.NET 페이지 내에서 페이지 메서드로 메서드를 `DynamicPopulate` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9b-116">Alternatively, you could implement the `getDate()` method as a page method within the actual ASP.NET page with the `DynamicPopulate` control.</span></span>

<span data-ttu-id="a5a9b-117">다음 단계에서는 새 ASP.NET 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9b-117">In the next step, create a new ASP.NET file.</span></span> <span data-ttu-id="a5a9b-118">포함할 첫 번째 단계는 항상를 `ScriptManager` ASP.NET AJAX 라이브러리를 로드 하 고 컨트롤 도구 키트 작동 하도록 현재 페이지에서:</span><span class="sxs-lookup"><span data-stu-id="a5a9b-118">As always, the first step is to include the `ScriptManager` in the current page to load the ASP.NET AJAX library and to make the Control Toolkit work:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample2.aspx)]

<span data-ttu-id="a5a9b-119">그런 다음 레이블 컨트롤을 추가 (예를 들어 이름이 같은 HTML 컨트롤을 사용 하 여 또는 &lt; `asp:Label`  / &gt; 웹 컨트롤)는 나중에 웹 서비스 호출의 결과 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9b-119">Then, add a label control (for instance using the HTML control of the same name, or the &lt;`asp:Label` /&gt; web control) which will later show the result of the web service call.</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample3.aspx)]

<span data-ttu-id="a5a9b-120">다음 HTML 단추 (컨트롤로 HTML에서는 서버로 다시 게시 하지 않아도 되므로) 동적 채우기를 트리거할 수 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9b-120">An HTML button (as an HTML control, since we do not require a postback to the server) will then be used to trigger the dynamic population:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample4.aspx)]

<span data-ttu-id="a5a9b-121">끝으로 `DynamicPopulateExtender` 실시간 작업을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9b-121">Finally, we need the `DynamicPopulateExtender` control to wire things up.</span></span> <span data-ttu-id="a5a9b-122">다음과 같은 특성 설정이 적용 됩니다 (확실 한 것 외에도 `ID` 하 고 `runat` = `"server"`):</span><span class="sxs-lookup"><span data-stu-id="a5a9b-122">The following attributes will be set (apart from the obvious ones, `ID` and `runat`=`"server"`):</span></span>

- <span data-ttu-id="a5a9b-123">`TargetControlID` 웹 서비스 호출에서 결과 넣을 위치</span><span class="sxs-lookup"><span data-stu-id="a5a9b-123">`TargetControlID` where to put the result from the web service call</span></span>
- <span data-ttu-id="a5a9b-124">`ServicePath` 웹 서비스에 대 한 경로 (페이지 메서드를 사용 하려는 경우 생략)</span><span class="sxs-lookup"><span data-stu-id="a5a9b-124">`ServicePath` path to the web service (omit if you want to use a page method)</span></span>
- <span data-ttu-id="a5a9b-125">`ServiceMethod` 웹 메서드나 페이지 메서드에 이름</span><span class="sxs-lookup"><span data-stu-id="a5a9b-125">`ServiceMethod` name of the web method or page method</span></span>
- <span data-ttu-id="a5a9b-126">`ContextKey` 웹 서비스에 보낼 컨텍스트 정보</span><span class="sxs-lookup"><span data-stu-id="a5a9b-126">`ContextKey` context information to be sent to the web service</span></span>
- <span data-ttu-id="a5a9b-127">`PopulateTriggerControlID` 웹 서비스 호출을 트리거하는 요소</span><span class="sxs-lookup"><span data-stu-id="a5a9b-127">`PopulateTriggerControlID` element which triggers the web service call</span></span>
- <span data-ttu-id="a5a9b-128">`ClearContentsDuringUpdate` 웹 서비스 호출 하는 동안 대상 요소를 빈 것인지</span><span class="sxs-lookup"><span data-stu-id="a5a9b-128">`ClearContentsDuringUpdate` whether to empty the target element during the web service call</span></span>

<span data-ttu-id="a5a9b-129">알 수 있듯이 컨트롤 몇 가지 정보가 필요 이지만 위치에 배치 하는 모든 방법은 매우 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9b-129">As you can see, the control requires some information but putting everything into place is quite straight-forward.</span></span> <span data-ttu-id="a5a9b-130">여기에 대 한 태그는 `DynamicPopulateExtender` 현재 시나리오에는 제어:</span><span class="sxs-lookup"><span data-stu-id="a5a9b-130">Here is the markup for the `DynamicPopulateExtender` control in the current scenario:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-vb/samples/sample5.aspx)]

<span data-ttu-id="a5a9b-131">브라우저에서 ASP.NET 페이지를 실행 하 고 단추 클릭 월-일-연도 형식의 현재 날짜를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5a9b-131">Run the ASP.NET page in the browser and click on the button; you will receive the current date in month-day-year format.</span></span>


<span data-ttu-id="a5a9b-132">[![서버에서 날짜를 검색 하는 단추 클릭](dynamically-populating-a-control-vb/_static/image2.png)](dynamically-populating-a-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a5a9b-132">[![A click on the button retrieves the date from the server](dynamically-populating-a-control-vb/_static/image2.png)](dynamically-populating-a-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="a5a9b-133">서버에서 날짜를 검색 하는 단추 클릭 ([클릭 하 여 큰 이미지 보기](dynamically-populating-a-control-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="a5a9b-133">A click on the button retrieves the date from the server ([Click to view full-size image](dynamically-populating-a-control-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a5a9b-134">[이전](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)
> [다음](dynamically-populating-a-control-using-javascript-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="a5a9b-134">[Previous](using-dynamicpopulate-with-a-user-control-and-javascript-cs.md)
[Next](dynamically-populating-a-control-using-javascript-code-vb.md)</span></span>
