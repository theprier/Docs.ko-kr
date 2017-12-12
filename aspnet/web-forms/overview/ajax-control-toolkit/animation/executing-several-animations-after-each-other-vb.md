---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
title: "여러 개의 애니메이션 서로 (VB) 한 후 실행 | Microsoft Docs"
author: wenz
description: "ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 떨어져서를 실행할 수 있습니다..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 21ece509-79cc-4d9d-892d-7b6e9c4d3502
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
msc.type: authoredcontent
ms.openlocfilehash: e949d181c0b742ee38ebbcc46e0e08efc678a1f8
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="executing-several-animations-after-each-other-vb"></a><span data-ttu-id="800c0-104">여러 개의 애니메이션 서로 (VB) 한 후 실행</span><span class="sxs-lookup"><span data-stu-id="800c0-104">Executing Several Animations after Each Other (VB)</span></span>
====================
<span data-ttu-id="800c0-105">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="800c0-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="800c0-106">[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="800c0-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3VB.pdf)</span></span>

> <span data-ttu-id="800c0-107">ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="800c0-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="800c0-108">다른 몇 개의 애니메이션 하나를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="800c0-108">It allows to run several animations one after the other.</span></span>


## <a name="overview"></a><span data-ttu-id="800c0-109">개요</span><span class="sxs-lookup"><span data-stu-id="800c0-109">Overview</span></span>

<span data-ttu-id="800c0-110">ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="800c0-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="800c0-111">다른 몇 개의 애니메이션 하나를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="800c0-111">It allows to run several animations one after the other.</span></span>

## <a name="steps"></a><span data-ttu-id="800c0-112">단계</span><span class="sxs-lookup"><span data-stu-id="800c0-112">Steps</span></span>

<span data-ttu-id="800c0-113">우선, 포함 된 `ScriptManager` 페이지; 그런 다음 ASP.NET AJAX 라이브러리 로드 되는 제어 도구 키트를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="800c0-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample1.aspx)]

<span data-ttu-id="800c0-114">그러면 다음과 같은 텍스트의 패널에 애니메이션 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="800c0-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample2.aspx)]

<span data-ttu-id="800c0-115">패널에 대 한 연결 된 CSS 클래스 좋은 배경색을 정의 하 고도 패널 고정된 폭을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="800c0-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-after-each-other-vb/samples/sample3.css)]

<span data-ttu-id="800c0-116">그런 다음 추가 `AnimationExtender` 페이지에 제공 하는 `ID`, `TargetControlID` 특성과 참가`runat="server":`</span><span class="sxs-lookup"><span data-stu-id="800c0-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample4.aspx)]

<span data-ttu-id="800c0-117">내에서 `<Animations>` 노드를 사용 하 여 `<OnLoad>` 페이지가 완전히 로드 되 면 애니메이션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="800c0-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="800c0-118">일반적으로 `<OnLoad>` 애니메이션만 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="800c0-118">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="800c0-119">애니메이션 프레임 워크를 수행 하 여에 여러 개의 애니메이션을 조인할 수는 `<Sequence>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="800c0-119">The Animation framework allows you to join several animations into one using the `<Sequence>` element.</span></span> <span data-ttu-id="800c0-120">내에서 모든 애니메이션이 `<Sequence>` 다른 하나씩 실행된 됩니다.</span><span class="sxs-lookup"><span data-stu-id="800c0-120">All animations within `<Sequence>` are executed one after the other.</span></span> <span data-ttu-id="800c0-121">다음은에 대 한 가능한 태그는 `AnimationExtender` 컨트롤을 먼저 넓은 패널을 만들고 다음 높이 감소:</span><span class="sxs-lookup"><span data-stu-id="800c0-121">Here is the a possible markup for the `AnimationExtender` control, first making the panel wider and then decreasing its height:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample5.aspx)]

<span data-ttu-id="800c0-122">실행할 때이 스크립트는 패널 넓고 다음 더 작은 첫 번째 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="800c0-122">When you run this script, the panel first gets wider and then smaller.</span></span>


<span data-ttu-id="800c0-123">[![폭이 증가 하는 먼저](executing-several-animations-after-each-other-vb/_static/image2.png)](executing-several-animations-after-each-other-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="800c0-123">[![First the width is increased](executing-several-animations-after-each-other-vb/_static/image2.png)](executing-several-animations-after-each-other-vb/_static/image1.png)</span></span>

<span data-ttu-id="800c0-124">폭이 증가 하는 먼저 ([전체 크기 이미지를 보려면 클릭](executing-several-animations-after-each-other-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="800c0-124">First the width is increased ([Click to view full-size image](executing-several-animations-after-each-other-vb/_static/image3.png))</span></span>


<span data-ttu-id="800c0-125">[![높이 감소 후](executing-several-animations-after-each-other-vb/_static/image5.png)](executing-several-animations-after-each-other-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="800c0-125">[![Then the height is decreased](executing-several-animations-after-each-other-vb/_static/image5.png)](executing-several-animations-after-each-other-vb/_static/image4.png)</span></span>

<span data-ttu-id="800c0-126">높이 감소 합니다 ([전체 크기 이미지를 보려면 클릭](executing-several-animations-after-each-other-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="800c0-126">Then the height is decreased ([Click to view full-size image](executing-several-animations-after-each-other-vb/_static/image6.png))</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="800c0-127">[이전](executing-several-animations-at-the-same-time-vb.md)
[다음](animation-depending-on-a-condition-vb.md)</span><span class="sxs-lookup"><span data-stu-id="800c0-127">[Previous](executing-several-animations-at-the-same-time-vb.md)
[Next](animation-depending-on-a-condition-vb.md)</span></span>
