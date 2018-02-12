---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
title: "DynamicPopulate를 사용 하 여 사용자 정의 컨트롤 및 JavaScript (VB) | Microsoft Docs"
author: wenz
description: "ASP.NET AJAX 컨트롤 도구 키트에서 DynamicPopulate 제어 웹 서비스 (또는 페이지 메서드)를 호출 및 t 대상 컨트롤에 결과 값을 채우는 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 778b9009-76f2-4665-940e-afc0e35bc917
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
msc.type: authoredcontent
ms.openlocfilehash: 495a3917ca5fa28bc833ccc666b1a5e6db7bf7f2
ms.sourcegitcommit: 016f4d58663bcd442930227022de23fb3abee0b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2018
---
<a name="using-dynamicpopulate-with-a-user-control-and-javascript-vb"></a><span data-ttu-id="f512b-103">DynamicPopulate를 사용 하 여 사용자 정의 컨트롤 및 JavaScript (VB)</span><span class="sxs-lookup"><span data-stu-id="f512b-103">Using DynamicPopulate with a User Control And JavaScript (VB)</span></span>
====================
<span data-ttu-id="f512b-104">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="f512b-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="f512b-105">[코드를 다운로드](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="f512b-105">[Download Code](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2VB.pdf)</span></span>

> <span data-ttu-id="f512b-106">ASP.NET AJAX 컨트롤 도구 키트에서 DynamicPopulate 컨트롤은 웹 서비스 (또는 페이지 메서드)를 호출 하 고 없이 페이지 새로 고침 페이지에서 대상 컨트롤에 결과 값을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="f512b-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="f512b-107">사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 모집단을 트리거할 수 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="f512b-107">It is also possible to trigger the population using custom client-side JavaScript code.</span></span> <span data-ttu-id="f512b-108">하지만 특별 한 주의 extender 사용자 정의 컨트롤에 있는 경우 수행할에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f512b-108">However special care has to be taken when the extender resides in a user control.</span></span>


## <a name="overview"></a><span data-ttu-id="f512b-109">개요</span><span class="sxs-lookup"><span data-stu-id="f512b-109">Overview</span></span>

<span data-ttu-id="f512b-110">`DynamicPopulate` 제어는 ASP.NET AJAX 컨트롤 도구 키트에서 웹 서비스 (또는 페이지 메서드)를 호출 하 고 대상 컨트롤 페이지 새로 고침 없이 페이지에 결과 값을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="f512b-110">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="f512b-111">사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 모집단을 트리거할 수 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="f512b-111">It is also possible to trigger the population using custom client-side JavaScript code.</span></span> <span data-ttu-id="f512b-112">하지만 특별 한 주의 extender 사용자 정의 컨트롤에 있는 경우 수행할에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f512b-112">However special care has to be taken when the extender resides in a user control.</span></span>

## <a name="steps"></a><span data-ttu-id="f512b-113">단계</span><span class="sxs-lookup"><span data-stu-id="f512b-113">Steps</span></span>

<span data-ttu-id="f512b-114">ASP.NET 웹 서비스 호출 될 메서드를 구현 하는 우선, 해야는 `DynamicPopulateExtender` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="f512b-114">First of all, you need an ASP.NET Web Service which implements the method to be called by the `DynamicPopulateExtender` control.</span></span> <span data-ttu-id="f512b-115">웹 서비스 메서드를 구현 `getDate()` 인수 이라는 형식 문자열 중 하나 필요로 하 `contextKey`, 이후는 `DynamicPopulate` 컨트롤 각 웹 서비스 호출에 컨텍스트 정보의 한 부분을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f512b-115">The web service implements the method `getDate()` that expects one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="f512b-116">코드는 다음과 같습니다 (파일 `DynamicPopulate.vb.asmx`) 세 가지 형식 중 하나에 현재 날짜를 검색 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f512b-116">Here is the code (files `DynamicPopulate.vb.asmx`) which retrieves the current date in one of three formats:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample1.aspx)]

<span data-ttu-id="f512b-117">다음 단계에서 새 사용자 정의 컨트롤을 만듭니다 (`.ascx` 파일), 그 첫 번째 줄에 다음 선언으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f512b-117">In the next step, create a new user control (`.ascx` file), denoted by the following declaration in its first line:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample2.aspx)]

<span data-ttu-id="f512b-118">A &lt; `label` &gt; 요소는 서버에서 가져온 데이터를 표시 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f512b-118">A &lt;`label`&gt; element will be used to display the data coming from the server.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample3.aspx)]

<span data-ttu-id="f512b-119">또한 사용자 정의 컨트롤 파일 사용 세 개의 라디오 단추, 웹 서비스에서 지 원하는 세 가지 가능한 형식 중 하나를 나타내는 각각.</span><span class="sxs-lookup"><span data-stu-id="f512b-119">Also in the user control file, we will use three radio buttons, each one representing one of the three possible date formats supported by the web service.</span></span> <span data-ttu-id="f512b-120">라디오 단추 중 하나에서 사용자가 브라우저 그러면 다음과 같은 JavaScript 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f512b-120">When the user clicks on one of the radio buttons, the browser will execute JavaScript code which looks like this:</span></span>

[!code-powershell[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample4.ps1)]

<span data-ttu-id="f512b-121">이 코드에 액세스는 `DynamicPopulateExtender` (이상한 ID에 대 한 걱정 하지 마십시오 아직, 나중에 설명 합니다.) 및 데이터와 동적 채우기를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="f512b-121">This code accesses the `DynamicPopulateExtender` (do not worry about the strange ID yet, this will be covered later on) and triggers the dynamic population with data.</span></span> <span data-ttu-id="f512b-122">현재 라디오 단추의 컨텍스트에서 `this.value` 참조 하는 값이 해당 `format1`, `format2` 또는 `format3` 정확 하 게 웹 메서드가 기대 합니다.</span><span class="sxs-lookup"><span data-stu-id="f512b-122">In the context of the current radio button, `this.value` refers to its value which is `format1`, `format2` or `format3` exactly what the web method expects.</span></span>

<span data-ttu-id="f512b-123">아직 사용자 정의 컨트롤에서 누락 된 유일한 항목은 `DynamicPopulateExtender` 컨트롤의 라디오 단추에 웹 서비스에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f512b-123">The only thing missing in the user control yet is the `DynamicPopulateExtender` control which links the radio buttons to the web service.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample5.aspx)]

<span data-ttu-id="f512b-124">컨트롤에 사용 되는 이상한 ID를 발견할 수 있습니다 다시: `mcd1$myDate` 대신 `myDate`합니다.</span><span class="sxs-lookup"><span data-stu-id="f512b-124">Again you may note the strange ID used in the control: `mcd1$myDate` instead of `myDate`.</span></span> <span data-ttu-id="f512b-125">이전에 사용 되는 JavaScript 코드 `mcd1_dpe1` 액세스로는 `DynamicPopulateExtender` 대신 `dpe1`합니다. 이 명명 전략은 특별 한 요구 사항을 사용 하는 경우 `DynamicPopulateExtender` 사용자 정의 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="f512b-125">Previously, the JavaScript code used `mcd1_dpe1` to access the `DynamicPopulateExtender` instead of `dpe1`.This naming strategy is a special requirement when using `DynamicPopulateExtender` within a user control.</span></span> <span data-ttu-id="f512b-126">또한 모든 작업이 이루어지는를 특정 방식으로에 사용자 컨트롤을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f512b-126">Furthermore, you have to embed the user contol in a specific way to make it all work.</span></span> <span data-ttu-id="f512b-127">새 ASP.NET 페이지를 만들고 방금 구현 된 사용자 정의 컨트롤에 대 한 태그 접두사를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f512b-127">Create a new ASP.NET page and register a tag prefix for the user control you have just implemented:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample6.aspx)]

<span data-ttu-id="f512b-128">그런 다음 ASP.NET AJAX 포함 `ScriptManager` 새 페이지에 컨트롤:</span><span class="sxs-lookup"><span data-stu-id="f512b-128">Then, include the ASP.NET AJAX `ScriptManager` control on the new page:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample7.aspx)]

<span data-ttu-id="f512b-129">페이지에 마지막으로, 사용자 정의 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f512b-129">Finally, add the user control to the page.</span></span> <span data-ttu-id="f512b-130">만 설정 해야 해당 `ID` 특성 (및 `runat="server"`물론,), 특정 이름으로 설정 해야 하지만: `mcd1` 이 JavaScript를 사용 하 여 액세스 하는 사용자 정의 컨트롤 내에서 사용 되는 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="f512b-130">You only have to set its `ID` attribute (and `runat="server"`, of course), but you also have to set it to a specific name: `mcd1` since this is the prefix used within the user control to access it using JavaScript.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample8.aspx)]

<span data-ttu-id="f512b-131">됐습니다!</span><span class="sxs-lookup"><span data-stu-id="f512b-131">And that's it!</span></span> <span data-ttu-id="f512b-132">예상 대로 동작 하는 페이지: 라디오 단추 중 하나에 사용자가 클릭, 제어 도구 키트에 웹 서비스를 호출 하 고 원하는 형식으로 현재 날짜를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f512b-132">The page behaves as expected: A user clicks on one of the radio buttons, the control in the Toolkit calls the web service and displays the current date in the desired format.</span></span>


<span data-ttu-id="f512b-133">[![사용자 정의 컨트롤에 있는 라디오 단추](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f512b-133">[![The radio buttons reside in a user control](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image1.png)</span></span>

<span data-ttu-id="f512b-134">사용자 정의 컨트롤에 있는 라디오 단추 ([전체 크기 이미지를 보려면 클릭](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="f512b-134">The radio buttons reside in a user control ([Click to view full-size image](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image3.png))</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="f512b-135">이전</span><span class="sxs-lookup"><span data-stu-id="f512b-135">Previous</span></span>](dynamically-populating-a-control-using-javascript-code-vb.md)
