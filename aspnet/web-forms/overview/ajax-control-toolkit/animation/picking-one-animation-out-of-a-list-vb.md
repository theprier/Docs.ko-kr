---
uid: web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-vb
title: 목록 (VB)에서 애니메이션 하나 선택 | Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 프레임 워크도 허용 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 81ba9116-d485-40c0-8ff6-7e9ae23e0a0c
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-vb
msc.type: authoredcontent
ms.openlocfilehash: 561f05e96888962cfe576963ce3905b171203939
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37387743"
---
<a name="picking-one-animation-out-of-a-list-vb"></a><span data-ttu-id="1af57-104">목록 (VB)에서 애니메이션 하나 선택</span><span class="sxs-lookup"><span data-stu-id="1af57-104">Picking One Animation Out Of a List (VB)</span></span>
====================
<span data-ttu-id="1af57-105">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="1af57-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="1af57-106">[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="1af57-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5VB.pdf)</span></span>

> <span data-ttu-id="1af57-107">ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1af57-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="1af57-108">또한 프레임 워크에는 일부 JavaScript 코드의 평가 따라 애니메이션을 목록에서 애니메이션 하나 선택 하는 프로그래머가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1af57-108">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="1af57-109">개요</span><span class="sxs-lookup"><span data-stu-id="1af57-109">Overview</span></span>

<span data-ttu-id="1af57-110">ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1af57-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="1af57-111">또한 프레임 워크에는 일부 JavaScript 코드의 평가 따라 애니메이션을 목록에서 애니메이션 하나 선택 하는 프로그래머가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1af57-111">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="1af57-112">단계</span><span class="sxs-lookup"><span data-stu-id="1af57-112">Steps</span></span>

<span data-ttu-id="1af57-113">첫째, 포함 된 `ScriptManager` 페이지 그런 다음 ASP.NET AJAX 라이브러리 로드 되 면 컨트롤 도구 키트를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="1af57-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample1.aspx)]

<span data-ttu-id="1af57-114">그러면 다음과 같은 텍스트 패널에 애니메이션 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1af57-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample2.aspx)]

<span data-ttu-id="1af57-115">패널에 대 한 연결 된 CSS 클래스에 유용한 배경 색을 정의 하 고 패널 고정된 너비를 설정할 수도:</span><span class="sxs-lookup"><span data-stu-id="1af57-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](picking-one-animation-out-of-a-list-vb/samples/sample3.css)]

<span data-ttu-id="1af57-116">그런 다음 추가 `AnimationExtender` 페이지에서 제공 하는 `ID`, `TargetControlID` 특성과 필수 항목 이지만 `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="1af57-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample4.aspx)]

<span data-ttu-id="1af57-117">내 합니다 `<Animations>` 노드를 사용 하 여 `<OnLoad>` 페이지가 완전히 로드 되 면 애니메이션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1af57-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="1af57-118">대신 일반 애니메이션 중 하나는 `<Case>` 요소 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1af57-118">Instead of one of the regular animations, the `<Case>` element comes into play.</span></span> <span data-ttu-id="1af57-119">SelectScript 특성 값이 계산 됩니다. 반환 값은 숫자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1af57-119">The value of its SelectScript attribute is evaluated; the return value must be numerical.</span></span> <span data-ttu-id="1af57-120">내에서 하위 애니메이션 중 하나는이 수에 따라 &lt;사례&gt; 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1af57-120">Depending on this number, one of the subanimations within &lt;Case&gt; is executed.</span></span> <span data-ttu-id="1af57-121">예를 들어 SelectScript 2로 계산 되 면 컨트롤 도구 키트 내에서 세 번째 애니메이션 실행 &lt;사례&gt; (0부터 계산).</span><span class="sxs-lookup"><span data-stu-id="1af57-121">For instance, if SelectScript evaluates to 2, the Control Toolkit runs the third animation within &lt;Case&gt; (counting starts at 0).</span></span>

<span data-ttu-id="1af57-122">다음 태그는 세 가지 하위 애니메이션 정의: 너비를 크기 조정, 높이, 크기 조정 및 옅은 색입니다. JavaScript 코드 (`Math.floor(3 * Math.random())`) 다음 세 가지 애니메이션 중 실행 되는 0과 2 사이의 숫자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1af57-122">The following markup defines three subanimations: Resizing the width, resizing the height, and fading out. The JavaScript code (`Math.floor(3 * Math.random())`) then picks a number between 0 and 2, so that one of the three animations is run:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample5.aspx)]


<span data-ttu-id="1af57-123">[![가능한 세 가지 애니메이션 중 하나: 패널 더 광범위 한 가져옵니다.](picking-one-animation-out-of-a-list-vb/_static/image2.png)](picking-one-animation-out-of-a-list-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1af57-123">[![One of the possible three animations: The panel gets wider](picking-one-animation-out-of-a-list-vb/_static/image2.png)](picking-one-animation-out-of-a-list-vb/_static/image1.png)</span></span>

<span data-ttu-id="1af57-124">가능한 세 가지 애니메이션 중 하나: 광범위 한 패널을 가져옵니다 ([클릭 하 여 큰 이미지 보기](picking-one-animation-out-of-a-list-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="1af57-124">One of the possible three animations: The panel gets wider ([Click to view full-size image](picking-one-animation-out-of-a-list-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1af57-125">[이전](animation-depending-on-a-condition-vb.md)
> [다음](animating-in-response-to-user-interaction-vb.md)</span><span class="sxs-lookup"><span data-stu-id="1af57-125">[Previous](animation-depending-on-a-condition-vb.md)
[Next](animating-in-response-to-user-interaction-vb.md)</span></span>
