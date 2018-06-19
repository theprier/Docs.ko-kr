---
uid: web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-cs
title: 선택 목록 (C#)에서 애니메이션 | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 프레임 워크 또한 허용...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 06a776fe-7c73-4ca7-8e02-5260a86edc03
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-cs
msc.type: authoredcontent
ms.openlocfilehash: 2d4aac447fcdfbf296560091cfcdf5eb51997a7b
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30871664"
---
<a name="picking-one-animation-out-of-a-list-c"></a><span data-ttu-id="1a001-104">선택 목록 (C#)에서 애니메이션</span><span class="sxs-lookup"><span data-stu-id="1a001-104">Picking One Animation Out Of a List (C#)</span></span>
====================
<span data-ttu-id="1a001-105">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="1a001-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="1a001-106">[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="1a001-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5CS.pdf)</span></span>

> <span data-ttu-id="1a001-107">ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="1a001-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="1a001-108">프레임 워크는 애니메이션 계산 일부 JavaScript 코드에 따라 목록에서 애니메이션을 선택 하는 프로그래머를 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a001-108">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="1a001-109">개요</span><span class="sxs-lookup"><span data-stu-id="1a001-109">Overview</span></span>

<span data-ttu-id="1a001-110">ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="1a001-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="1a001-111">프레임 워크는 애니메이션 계산 일부 JavaScript 코드에 따라 목록에서 애니메이션을 선택 하는 프로그래머를 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a001-111">The framework also allows the programmer to pick one animation out of a list of animations, depending on the evaluation of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="1a001-112">단계</span><span class="sxs-lookup"><span data-stu-id="1a001-112">Steps</span></span>

<span data-ttu-id="1a001-113">우선, 포함 된 `ScriptManager` 페이지; 그런 다음 ASP.NET AJAX 라이브러리 로드 되는 제어 도구 키트를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="1a001-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample1.aspx)]

<span data-ttu-id="1a001-114">그러면 다음과 같은 텍스트의 패널에 애니메이션 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a001-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample2.aspx)]

<span data-ttu-id="1a001-115">패널에 대 한 연결 된 CSS 클래스 좋은 배경색을 정의 하 고도 패널 고정된 폭을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a001-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](picking-one-animation-out-of-a-list-cs/samples/sample3.css)]

<span data-ttu-id="1a001-116">그런 다음 추가 `AnimationExtender` 페이지에 제공 하는 `ID`, `TargetControlID` 특성과 참가 `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="1a001-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample4.aspx)]

<span data-ttu-id="1a001-117">내에서 `<Animations>` 노드를 사용 하 여 `<OnLoad>` 페이지가 완전히 로드 되 면 애니메이션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a001-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="1a001-118">대신 일반 애니메이션 중 하나는 `<Case>` 요소에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a001-118">Instead of one of the regular animations, the `<Case>` element comes into play.</span></span> <span data-ttu-id="1a001-119">해당 SelectScript 특성의 값이 계산 됩니다. 반환 값은 숫자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a001-119">The value of its SelectScript attribute is evaluated; the return value must be numerical.</span></span> <span data-ttu-id="1a001-120">내에서 하위 애니메이션 중 하나는이 수에 따라 &lt;대/소문자&gt; 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a001-120">Depending on this number, one of the subanimations within &lt;Case&gt; is executed.</span></span> <span data-ttu-id="1a001-121">예를 들어, SelectScript 2로 계산 되 면 컨트롤 도구 키트 내에서 세 번째 애니메이션 실행 &lt;대/소문자&gt; (개 0부터 시작)입니다.</span><span class="sxs-lookup"><span data-stu-id="1a001-121">For instance, if SelectScript evaluates to 2, the Control Toolkit runs the third animation within &lt;Case&gt; (counting starts at 0).</span></span>

<span data-ttu-id="1a001-122">태그를 다음 세 하위 애니메이션을 정의: 너비를 크기 조정, 높이 조정 하 고, 페이딩 합니다. JavaScript 코드 (`Math.floor(3 * Math.random())`) 다음 세 애니메이션 중 하나를 실행할 수 있도록 0, 2 사이의 숫자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a001-122">The following markup defines three subanimations: Resizing the width, resizing the height, and fading out. The JavaScript code (`Math.floor(3 * Math.random())`) then picks a number between 0 and 2, so that one of the three animations is run:</span></span>

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample5.aspx)]


<span data-ttu-id="1a001-123">[![가능한 세 가지 애니메이션 중 하나: 패널의 넓은 가져옵니다.](picking-one-animation-out-of-a-list-cs/_static/image2.png)](picking-one-animation-out-of-a-list-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1a001-123">[![One of the possible three animations: The panel gets wider](picking-one-animation-out-of-a-list-cs/_static/image2.png)](picking-one-animation-out-of-a-list-cs/_static/image1.png)</span></span>

<span data-ttu-id="1a001-124">가능한 세 가지 애니메이션 중 하나: 패널의 넓은 가져옵니다 ([전체 크기 이미지를 보려면 클릭](picking-one-animation-out-of-a-list-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="1a001-124">One of the possible three animations: The panel gets wider ([Click to view full-size image](picking-one-animation-out-of-a-list-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1a001-125">[이전](animation-depending-on-a-condition-cs.md)
> [다음](animating-in-response-to-user-interaction-cs.md)</span><span class="sxs-lookup"><span data-stu-id="1a001-125">[Previous](animation-depending-on-a-condition-cs.md)
[Next](animating-in-response-to-user-interaction-cs.md)</span></span>
