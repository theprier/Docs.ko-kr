---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-vb
title: 클라이언트 쪽 코드 (VB)를 사용 하 여 애니메이션 실행 | Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 애니메이션을 실행 하는 중...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: f7073f50-d765-456d-9957-926ce60f35f6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 9b180ad17e0e3d2dffa6262d10a83a8353e0a1d0
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37811888"
---
<a name="executing-animations-using-client-side-code-vb"></a><span data-ttu-id="a6142-104">클라이언트 쪽 코드 (VB)를 사용 하 여 실행 중인 애니메이션</span><span class="sxs-lookup"><span data-stu-id="a6142-104">Executing Animations Using Client-Side Code (VB)</span></span>
====================
<span data-ttu-id="a6142-105">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="a6142-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a6142-106">[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="a6142-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10VB.pdf)</span></span>

> <span data-ttu-id="a6142-107">ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a6142-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="a6142-108">사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 애니메이션 실행 트리거될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6142-108">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="a6142-109">개요</span><span class="sxs-lookup"><span data-stu-id="a6142-109">Overview</span></span>

<span data-ttu-id="a6142-110">ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a6142-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="a6142-111">사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 애니메이션 실행 트리거될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6142-111">The animation execution may also be triggered using custom client-side JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="a6142-112">단계</span><span class="sxs-lookup"><span data-stu-id="a6142-112">Steps</span></span>

<span data-ttu-id="a6142-113">첫째, 포함 된 `ScriptManager` 페이지 그런 다음 ASP.NET AJAX 라이브러리 로드 되 면 컨트롤 도구 키트를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="a6142-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample1.aspx)]

<span data-ttu-id="a6142-114">그러면 다음과 같은 텍스트 패널에 애니메이션 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6142-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample2.aspx)]

<span data-ttu-id="a6142-115">패널에 대 한 연결 된 CSS 클래스에 유용한 배경 색을 정의 하 고 패널 고정된 너비를 설정할 수도:</span><span class="sxs-lookup"><span data-stu-id="a6142-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-animations-using-client-side-code-vb/samples/sample3.css)]

<span data-ttu-id="a6142-116">그런 다음 추가 `AnimationExtender` 페이지에서 제공 하는 `ID`, `TargetControlID` 특성과 필수 항목 이지만 `runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="a6142-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample4.aspx)]

<span data-ttu-id="a6142-117">내 합니다 `<Animations>` 노드를 사용 하 여 `<OnClick>` 애니메이션 사용자 한 번만 실행 패널에서 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6142-117">Within the `<Animations>` node, use `<OnClick>` to run the animations once the user clicks on the panel.</span></span> <span data-ttu-id="a6142-118">Parallelly 실행할 두 애니메이션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6142-118">Add two animations to be executed parallelly:</span></span>

[!code-xml[Main](executing-animations-using-client-side-code-vb/samples/sample5.xml)]

<span data-ttu-id="a6142-119">데모를 위해이 애니메이션 (컨트롤 도구 키트를 사용 하 여 만든 다른 애니메이션) 실행 되는 페이지가 실행 되 면 JavaScript 코드를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6142-119">For the sake of demonstration, this animation (and any other animation created using the Control Toolkit) is executed using JavaScript code, once the page runs.</span></span> <span data-ttu-id="a6142-120">모든 것에 대 한 액세스는 `AnimationExtender` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6142-120">First of all we need access to the `AnimationExtender` control.</span></span> <span data-ttu-id="a6142-121">ASP.NET AJAX 라이브러리에서 제공 된 `$find()` 이 작업에 대 한 함수:</span><span class="sxs-lookup"><span data-stu-id="a6142-121">The ASP.NET AJAX library provides the `$find()` function for this task:</span></span>

[!code-csharp[Main](executing-animations-using-client-side-code-vb/samples/sample6.cs)]

<span data-ttu-id="a6142-122">합니다 `AnimationExtender` 컨트롤의 XML 태그에 사용 되는 이벤트 처리기에 동일한 이름의 메서드를 포함 하 여 다양 한 API를 노출: `OnClick()`, `OnLoad()`등입니다.</span><span class="sxs-lookup"><span data-stu-id="a6142-122">The `AnimationExtender` control exposes a rich API, including methods with names identical to the event handlers used in the XML markup: `OnClick()`, `OnLoad()`, and so on.</span></span> <span data-ttu-id="a6142-123">예를 들어 호출을 `OnClick()` 메서드 내에서 애니메이션을 실행 합니다 `<OnClick>` 요소의 `AnimationExtender` 컨트롤:</span><span class="sxs-lookup"><span data-stu-id="a6142-123">For instance, a call of the `OnClick()` method executes the animation within the `<OnClick>` element of the `AnimationExtender` control:</span></span>

[!code-javascript[Main](executing-animations-using-client-side-code-vb/samples/sample7.js)]

<span data-ttu-id="a6142-124">페이지가 완전히 로드 되 면 패널에서 클릭을 에뮬레이트하는 전체 클라이언트 쪽 JavaScript 코드를 확인 하는 다음과 같습니다는 `pageLoad()` 함수 이름 이라고 하는 ASP.NET AJAX에서 한 번의 페이지를 사용 하 되 고 모든 포함 된 라이브러리는 JavaScript 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6142-124">Here is the complete client-side JavaScript code that emulates the click on the panel once the page has been fully loaded note that the `pageLoad()` function name is used which is called by ASP.NET AJAX once the page and all included JavaScript libraries have been loaded.</span></span>

[!code-html[Main](executing-animations-using-client-side-code-vb/samples/sample8.html)]


<span data-ttu-id="a6142-125">[![이 애니메이션은 마우스 클릭 하지 않고 즉시 실행](executing-animations-using-client-side-code-vb/_static/image2.png)](executing-animations-using-client-side-code-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a6142-125">[![The animation runs immediately, without a mouse click](executing-animations-using-client-side-code-vb/_static/image2.png)](executing-animations-using-client-side-code-vb/_static/image1.png)</span></span>

<span data-ttu-id="a6142-126">마우스 클릭 하지 않고 애니메이션은 즉시 실행 ([클릭 하 여 큰 이미지 보기](executing-animations-using-client-side-code-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="a6142-126">The animation runs immediately, without a mouse click ([Click to view full-size image](executing-animations-using-client-side-code-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a6142-127">[이전](modifying-animations-from-the-server-side-vb.md)
> [다음](changing-an-animation-using-client-side-code-vb.md)</span><span class="sxs-lookup"><span data-stu-id="a6142-127">[Previous](modifying-animations-from-the-server-side-vb.md)
[Next](changing-an-animation-using-client-side-code-vb.md)</span></span>
