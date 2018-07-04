---
uid: web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
title: 클라이언트 쪽 코드 (C#)를 사용 하 여 애니메이션 변경 | Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 애니메이션을 선택 하십시오.
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 2bfbc5cc-f942-44b7-a62d-a29520f1da9a
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 4bf480401e244661e2c316adcde3cbde647a6dc3
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37393076"
---
<a name="changing-an-animation-using-client-side-code-c"></a><span data-ttu-id="8952a-104">클라이언트 쪽 코드 (C#)를 사용 하 여 애니메이션 변경</span><span class="sxs-lookup"><span data-stu-id="8952a-104">Changing an Animation Using Client-Side Code (C#)</span></span>
====================
<span data-ttu-id="8952a-105">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="8952a-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="8952a-106">[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="8952a-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11CS.pdf)</span></span>

> <span data-ttu-id="8952a-107">ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="8952a-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="8952a-108">애니메이션은 사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8952a-108">The animation can also be changed using custom client-side JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="8952a-109">개요</span><span class="sxs-lookup"><span data-stu-id="8952a-109">Overview</span></span>

<span data-ttu-id="8952a-110">ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="8952a-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="8952a-111">애니메이션은 사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8952a-111">The animation can also be changed using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="8952a-112">단계</span><span class="sxs-lookup"><span data-stu-id="8952a-112">Steps</span></span>

<span data-ttu-id="8952a-113">첫째, 포함 된 `ScriptManager` 페이지 그런 다음 ASP.NET AJAX 라이브러리 로드 되 면 컨트롤 도구 키트를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="8952a-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample1.aspx)]

<span data-ttu-id="8952a-114">그러면 다음과 같은 텍스트 패널에 애니메이션 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8952a-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample2.aspx)]

<span data-ttu-id="8952a-115">패널에 대 한 연결 된 CSS 클래스에 유용한 배경 색을 정의 하 고 패널 고정된 너비를 설정할 수도:</span><span class="sxs-lookup"><span data-stu-id="8952a-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](changing-an-animation-using-client-side-code-cs/samples/sample3.css)]

<span data-ttu-id="8952a-116">실제 애니메이션은 HTML 단추를 통해 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8952a-116">The actual animation is launched by an HTML button:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample4.aspx)]

<span data-ttu-id="8952a-117">그런 다음 추가 `AnimationExtender` 페이지에서 제공 하는 `ID`, `TargetControlID` 특성과 필수 항목 이지만 `runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="8952a-117">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample5.aspx)]

<span data-ttu-id="8952a-118">없습니다 `<Animations>` 내에서 노드를 `AnimationExtender` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="8952a-118">Note that there is no `<Animations>` node within the `AnimationExtender` control.</span></span> <span data-ttu-id="8952a-119">사용자 지정 JavaScript 코드는 컨트롤을 사용 하 여 사용할 애니메이션을 위해 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8952a-119">Custom JavaScript code is used to provide the animations to be used with the control.</span></span>

<span data-ttu-id="8952a-120">서버 API와 마찬가지로 `AnimationExtender`을 extender에 애니메이션을 아직 할당할 간편한 방법이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8952a-120">As with the server API of `AnimationExtender`, there is no easy way to assign an animation to the extender yet.</span></span> <span data-ttu-id="8952a-121">하지만 다양 한 이벤트를 사용 하 여 등록 된 extender는 읽기 및 쓰기 애니메이션 하는 여러 메서드를 노출 하는 (`OnClick`, `OnLoad`등).</span><span class="sxs-lookup"><span data-stu-id="8952a-121">However the extender does expose several methods to read and write animations registered with the various events (`OnClick`, `OnLoad`, and so on).</span></span> <span data-ttu-id="8952a-122">다음은 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="8952a-122">Here are some examples:</span></span>

- `get_OnClick()`
- `set_OnClick()`
- `get_OnLoad()`
- `set_OnLoad()`
- `...`

<span data-ttu-id="8952a-123">반환 값의 형식을 `get_*()` 의 인수 형식과 함수는 `set_*()` 함수는 JSON 문자열 것 XML 태그의 개체 표현을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8952a-123">The format of the return value of the `get_*()` functions and the format of the argument for the `set_*()` functions is a JSON string, providing an object representation of what the XML markup would be.</span></span> <span data-ttu-id="8952a-124">현재, 개체를 전달할 방법이 없기 하지만 지정 된 애니메이션에서 개체를 읽을 수 있습니다 (`get_OnXXXBehavior()` 메서드).</span><span class="sxs-lookup"><span data-stu-id="8952a-124">Currently, there is no way to pass an object in, but it is possible to read an object from a given animation (`get_OnXXXBehavior()` methods).</span></span>

<span data-ttu-id="8952a-125">JSON 문자열은 다음과 같습니다 (구분 따옴표 없이 원활 하 게 서식이 지정) 단추를 트리거한 애니메이션을 나타내는 이지만 패널 크기를 조정 하 여 동시에 페이드아웃 애니메이션 합니다.</span><span class="sxs-lookup"><span data-stu-id="8952a-125">Here is a JSON string (without the delimiting quotes and formatted nicely) representing an animation triggered by the button, but animating the panel by resizing it and fading it out at the same time:</span></span>

[!code-json[Main](changing-an-animation-using-client-side-code-cs/samples/sample6.json)]

<span data-ttu-id="8952a-126">다음 JavaScript 코드를이 JSON descripting 할당 된 `OnClick` 현재 extender의 애니메이션 실행:</span><span class="sxs-lookup"><span data-stu-id="8952a-126">The following JavaScript code assigns this JSON descripting to the `OnClick` animation of the current extender and runs it:</span></span>

[!code-html[Main](changing-an-animation-using-client-side-code-cs/samples/sample7.html)]


<span data-ttu-id="8952a-127">[![마우스 클릭 하지 않고 (및 거의 태그를 사용 하 여)이 애니메이션은 즉시 실행](changing-an-animation-using-client-side-code-cs/_static/image2.png)](changing-an-animation-using-client-side-code-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8952a-127">[![The animation runs immediately, without a mouse click (and with very little markup)](changing-an-animation-using-client-side-code-cs/_static/image2.png)](changing-an-animation-using-client-side-code-cs/_static/image1.png)</span></span>

<span data-ttu-id="8952a-128">마우스 클릭 하지 않고과 거의 태그를 사용 하 여 애니메이션은 즉시 실행 ([클릭 하 여 큰 이미지 보기](changing-an-animation-using-client-side-code-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="8952a-128">The animation runs immediately, without a mouse click (and with very little markup) ([Click to view full-size image](changing-an-animation-using-client-side-code-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8952a-129">[이전](executing-animations-using-client-side-code-cs.md)
> [다음](animating-an-updatepanel-control-cs.md)</span><span class="sxs-lookup"><span data-stu-id="8952a-129">[Previous](executing-animations-using-client-side-code-cs.md)
[Next](animating-an-updatepanel-control-cs.md)</span></span>
