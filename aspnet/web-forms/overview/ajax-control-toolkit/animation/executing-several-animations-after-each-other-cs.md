---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-cs
title: 여러 애니메이션 실행 다른 (C#) | Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 떨어져서를 실행할 수 있도록 하는 중...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 7dc02b18-2b5d-4844-b7c5-cbd818477163
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-cs
msc.type: authoredcontent
ms.openlocfilehash: 60fb7dacfe59eaafef71fcc9cde61b7840624343
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41837371"
---
<a name="executing-several-animations-after-each-other-c"></a><span data-ttu-id="76c45-104">여러 애니메이션 실행 다른 (C#)</span><span class="sxs-lookup"><span data-stu-id="76c45-104">Executing Several Animations after Each Other (C#)</span></span>
====================
<span data-ttu-id="76c45-105">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="76c45-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="76c45-106">[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="76c45-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3CS.pdf)</span></span>

> <span data-ttu-id="76c45-107">ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="76c45-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="76c45-108">다른 여러 애니메이션 하나를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c45-108">It allows to run several animations one after the other.</span></span>


<span data-ttu-id="76c45-109">ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="76c45-109">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="76c45-110">다른 여러 애니메이션 하나를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76c45-110">It allows to run several animations one after the other.</span></span>

## <a name="steps"></a><span data-ttu-id="76c45-111">단계</span><span class="sxs-lookup"><span data-stu-id="76c45-111">Steps</span></span>

<span data-ttu-id="76c45-112">첫째, 포함 된 `ScriptManager` 페이지 그런 다음 ASP.NET AJAX 라이브러리 로드 되 면 컨트롤 도구 키트를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="76c45-112">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample1.aspx)]

<span data-ttu-id="76c45-113">그러면 다음과 같은 텍스트 패널에 애니메이션 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76c45-113">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample2.aspx)]

<span data-ttu-id="76c45-114">패널에 대 한 연결 된 CSS 클래스에 유용한 배경 색을 정의 하 고 패널 고정된 너비를 설정할 수도:</span><span class="sxs-lookup"><span data-stu-id="76c45-114">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-after-each-other-cs/samples/sample3.css)]

<span data-ttu-id="76c45-115">그런 다음 추가 `AnimationExtender` 페이지에서 제공 하는 `ID`, `TargetControlID` 특성과 필수 항목 이지만 `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="76c45-115">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample4.aspx)]

<span data-ttu-id="76c45-116">내 합니다 `<Animations>` 노드를 사용 하 여 `<OnLoad>` 페이지가 완전히 로드 되 면 애니메이션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="76c45-116">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="76c45-117">일반적으로 `<OnLoad>` 만 하나의 애니메이션을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="76c45-117">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="76c45-118">애니메이션 프레임 워크를 사용 하 여 여러 애니메이션을 조인할 수는 `<Sequence>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="76c45-118">The Animation framework allows you to join several animations into one using the `<Sequence>` element.</span></span> <span data-ttu-id="76c45-119">내에서 모든 애니메이션이 `<Sequence>` 다른 하나씩 실행된 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76c45-119">All animations within `<Sequence>` are executed one after the other.</span></span> <span data-ttu-id="76c45-120">다음은에 대 한 가능한 태그를 `AnimationExtender` 컨트롤을 먼저 더 광범위 한 패널을 만들고 다음 높이 감소:</span><span class="sxs-lookup"><span data-stu-id="76c45-120">Here is the a possible markup for the `AnimationExtender` control, first making the panel wider and then decreasing its height:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample5.aspx)]

<span data-ttu-id="76c45-121">실행할 때이 스크립트를 패널 넓거나 다음 작은 첫 번째 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="76c45-121">When you run this script, the panel first gets wider and then smaller.</span></span>


<span data-ttu-id="76c45-122">[![너비는 증가 하는 먼저](executing-several-animations-after-each-other-cs/_static/image2.png)](executing-several-animations-after-each-other-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="76c45-122">[![First the width is increased](executing-several-animations-after-each-other-cs/_static/image2.png)](executing-several-animations-after-each-other-cs/_static/image1.png)</span></span>

<span data-ttu-id="76c45-123">먼저 너비 증가 됩니다 ([클릭 하 여 큰 이미지 보기](executing-several-animations-after-each-other-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="76c45-123">First the width is increased ([Click to view full-size image](executing-several-animations-after-each-other-cs/_static/image3.png))</span></span>


<span data-ttu-id="76c45-124">[![높이 감소 한 다음](executing-several-animations-after-each-other-cs/_static/image5.png)](executing-several-animations-after-each-other-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="76c45-124">[![Then the height is decreased](executing-several-animations-after-each-other-cs/_static/image5.png)](executing-several-animations-after-each-other-cs/_static/image4.png)</span></span>

<span data-ttu-id="76c45-125">높이 감소 한 다음 ([클릭 하 여 큰 이미지 보기](executing-several-animations-after-each-other-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="76c45-125">Then the height is decreased ([Click to view full-size image](executing-several-animations-after-each-other-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="76c45-126">[이전](executing-several-animations-at-the-same-time-cs.md)
> [다음](animation-depending-on-a-condition-cs.md)</span><span class="sxs-lookup"><span data-stu-id="76c45-126">[Previous](executing-several-animations-at-the-same-time-cs.md)
[Next](animation-depending-on-a-condition-cs.md)</span></span>
