---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-vb
title: 여러 애니메이션 (VB) 동시에 실행 | Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 떨어져서를 실행할 수 있도록 하는 중...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 2469f7ea-1489-42fb-a8e1-414c90141ce9
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-vb
msc.type: authoredcontent
ms.openlocfilehash: 20baa40c34dd8c8907b940764987441bc7a91da9
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831465"
---
<a name="executing-several-animations-at-the-same-time-vb"></a><span data-ttu-id="666d5-104">여러 애니메이션 (VB) 동시에 실행</span><span class="sxs-lookup"><span data-stu-id="666d5-104">Executing Several Animations at The Same Time (VB)</span></span>
====================
<span data-ttu-id="666d5-105">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="666d5-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="666d5-106">[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="666d5-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2VB.pdf)</span></span>

> <span data-ttu-id="666d5-107">ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="666d5-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="666d5-108">병렬 방식으로 여러 애니메이션을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="666d5-108">It allows to run several animations in a parallel fashion.</span></span>


## <a name="overview"></a><span data-ttu-id="666d5-109">개요</span><span class="sxs-lookup"><span data-stu-id="666d5-109">Overview</span></span>

<span data-ttu-id="666d5-110">ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="666d5-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="666d5-111">병렬 방식으로 여러 애니메이션을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="666d5-111">It allows to run several animations in a parallel fashion.</span></span>

## <a name="steps"></a><span data-ttu-id="666d5-112">단계</span><span class="sxs-lookup"><span data-stu-id="666d5-112">Steps</span></span>

<span data-ttu-id="666d5-113">첫째, 포함 된 `ScriptManager` 페이지 그런 다음 ASP.NET AJAX 라이브러리 로드 되 면 컨트롤 도구 키트를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="666d5-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample1.aspx)]

<span data-ttu-id="666d5-114">그러면 다음과 같은 텍스트 패널에 애니메이션 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="666d5-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample2.aspx)]

<span data-ttu-id="666d5-115">패널에 대 한 연결 된 CSS 클래스에 유용한 배경 색을 정의 하 고 패널 고정된 너비를 설정할 수도:</span><span class="sxs-lookup"><span data-stu-id="666d5-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-at-the-same-time-vb/samples/sample3.css)]

<span data-ttu-id="666d5-116">그런 다음 추가 `AnimationExtender` 페이지에서 제공 하는 `ID`, `TargetControlID` 특성과 필수 항목 이지만 `runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="666d5-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample4.aspx)]

<span data-ttu-id="666d5-117">내 합니다 `<Animations>` 노드를 사용 하 여 `<OnLoad>` 페이지가 완전히 로드 되 면 애니메이션을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="666d5-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="666d5-118">일반적으로 `<OnLoad>` 만 하나의 애니메이션을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="666d5-118">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="666d5-119">애니메이션 프레임 워크를 사용 하 여 여러 애니메이션을 조인할 수는 `<Parallel>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="666d5-119">The Animation framework allows you to join several animations into one using the `<Parallel>` element.</span></span> <span data-ttu-id="666d5-120">내에서 모든 애니메이션이 `<Parallel>` 동시에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="666d5-120">All animations within `<Parallel>` are executed at the same time.</span></span>

<span data-ttu-id="666d5-121">다음은에 대 한 가능한 태그를 `AnimationExtender` 제어, 페이드아웃 및 동시 패널 크기 조정:</span><span class="sxs-lookup"><span data-stu-id="666d5-121">Here is the a possible markup for the `AnimationExtender` control, fading out and resizing the panel at the same time:</span></span>

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample5.aspx)]

<span data-ttu-id="666d5-122">및 실제로:이 스크립트를 실행 하면 패널이 표시 되 면이 조정 하는 (threefolding 보다 더 많은 너비와 halfing 높이가) 동시에 페이드 아웃 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="666d5-122">And indeed: when you run this script, the panel is displayed, then resizes (more than threefolding its width and halfing its height) and fades out at the same time.</span></span>


<span data-ttu-id="666d5-123">[![패널 페이드아웃 되며 (해당 콘텐츠를 브라우저의 렌더링 엔진 덕분 포함) 크기 조정](executing-several-animations-at-the-same-time-vb/_static/image2.png)](executing-several-animations-at-the-same-time-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="666d5-123">[![The panel is fading out and resizing (including its content, thanks to the browser's rendering engine)](executing-several-animations-at-the-same-time-vb/_static/image2.png)](executing-several-animations-at-the-same-time-vb/_static/image1.png)</span></span>

<span data-ttu-id="666d5-124">패널 페이드아웃 되며 (해당 콘텐츠를 브라우저의 렌더링 엔진 덕분 포함) 크기 조정 ([클릭 하 여 큰 이미지 보기](executing-several-animations-at-the-same-time-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="666d5-124">The panel is fading out and resizing (including its content, thanks to the browser's rendering engine) ([Click to view full-size image](executing-several-animations-at-the-same-time-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="666d5-125">[이전](adding-animation-to-a-control-vb.md)
> [다음](executing-several-animations-after-each-other-vb.md)</span><span class="sxs-lookup"><span data-stu-id="666d5-125">[Previous](adding-animation-to-a-control-vb.md)
[Next](executing-several-animations-after-each-other-vb.md)</span></span>
