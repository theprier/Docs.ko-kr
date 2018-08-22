---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
title: 상호 배타적인 확인란 (VB) 만들기 | Microsoft Docs
author: wenz
description: '일련의 옵션 중 하나만 선택할 수 있습니다, 라디오 단추는 일반적으로 사용 합니다. 그러나 단점은는: 그룹에 하나의 라디오 단추를 선택 하면...'
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e9dd1d5a-a1db-4114-981d-6a91acb1d709
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
msc.type: authoredcontent
ms.openlocfilehash: fd338b622779b64dd59f9cf6f3e2365ef5cb3ffb
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41823861"
---
<a name="creating-mutually-exclusive-checkboxes-vb"></a><span data-ttu-id="b31ce-104">상호 배타적인 확인란 만들기 (VB)</span><span class="sxs-lookup"><span data-stu-id="b31ce-104">Creating Mutually Exclusive Checkboxes (VB)</span></span>
====================
<span data-ttu-id="b31ce-105">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="b31ce-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="b31ce-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="b31ce-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0VB.pdf)</span></span>

> <span data-ttu-id="b31ce-107">일련의 옵션 중 하나만 선택할 수 있습니다, 라디오 단추는 일반적으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b31ce-107">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="b31ce-108">그러나 단점은는: 그룹에 하나의 라디오 단추를 선택 하면 수 없으면 모든 라디오 단추를 선택 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="b31ce-108">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="b31ce-109">그러나 확인란 선택 취소할 수 있습니다 언제 든 지, 배타적이 지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b31ce-109">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="b31ce-110">이 자습서에는 두 가지 장점을 제공 합니다: 상호 배타적인 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="b31ce-110">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>


## <a name="overview"></a><span data-ttu-id="b31ce-111">개요</span><span class="sxs-lookup"><span data-stu-id="b31ce-111">Overview</span></span>

<span data-ttu-id="b31ce-112">일련의 옵션 중 하나만 선택할 수 있습니다, 라디오 단추는 일반적으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b31ce-112">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="b31ce-113">그러나 단점은는: 그룹에 하나의 라디오 단추를 선택 하면 수 없으면 모든 라디오 단추를 선택 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="b31ce-113">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="b31ce-114">그러나 확인란 선택 취소할 수 있습니다 언제 든 지, 배타적이 지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b31ce-114">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="b31ce-115">이 자습서에는 두 가지 장점을 제공 합니다: 상호 배타적인 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="b31ce-115">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>

## <a name="steps"></a><span data-ttu-id="b31ce-116">단계</span><span class="sxs-lookup"><span data-stu-id="b31ce-116">Steps</span></span>

<span data-ttu-id="b31ce-117">ASP.NET AJAX Control Toolkit MutuallyExclusiveCheckBox extender를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b31ce-117">The ASP.NET AJAX Control Toolkit contains the MutuallyExclusiveCheckBox extender.</span></span> <span data-ttu-id="b31ce-118">이렇게 하면 프로그래머가 모든 확인란 그룹 이름에 할당할 수 있습니다. (`Key` 특성).</span><span class="sxs-lookup"><span data-stu-id="b31ce-118">This enables programmers to assign any checkbox to a group name (`Key` attribute).</span></span> <span data-ttu-id="b31ce-119">동일한 그룹 내 모든 확인 상자에서 하나만 한 번에 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b31ce-119">From all check boxes within the same group, only one may be selected at one time.</span></span>

<span data-ttu-id="b31ce-120">새 ASP.NET 페이지에 확인란이 두 개를 배치로 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b31ce-120">Let's start with putting two check boxes on a new ASP.NET page.</span></span> <span data-ttu-id="b31ce-121">더 많은 될 수 있지만 그 중 두 가지 원칙을 보여 주기 위해 충분 합니다.</span><span class="sxs-lookup"><span data-stu-id="b31ce-121">There can be more, but two of them suffice to demonstrate the principle:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample1.aspx)]

<span data-ttu-id="b31ce-122">두 확인란에 대 한 페이지의 MutuallyExclusiveCheckBoxExtender 컨트롤을 배치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b31ce-122">For both checkboxes, a MutuallyExclusiveCheckBoxExtender control must be put on the page.</span></span> <span data-ttu-id="b31ce-123">두 키 특성은 HTML 라디오 단추 요소의 특성은 자신이 속한 그룹을 나타내는 동일 해야 합니다. 값 처럼 동일한 값을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b31ce-123">Both Key attributes need to have the same value, just as the value attributes of HTML radio button elements must be identical to denote the group they belong to.</span></span> <span data-ttu-id="b31ce-124">Extender의 TargetControlID 속성 확인란의 ID를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="b31ce-124">The TargetControlID property of the extender points to the ID of the check box.</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample2.aspx)]

<span data-ttu-id="b31ce-125">마지막으로, ASP.NET AJAX를 포함 `ScriptManager` ASP.NET AJAX Control Toolkit의 모든 요소에서 필요한:</span><span class="sxs-lookup"><span data-stu-id="b31ce-125">Finally, include the ASP.NET AJAX `ScriptManager` which is required by all elements of the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample3.aspx)]

<span data-ttu-id="b31ce-126">하지만 저장 하 고 페이지를 실행 합니다: 확인을 모두 확인란의 선택을 취소 순식간에 확인란을 모두 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b31ce-126">Save and run the page: You can check and uncheck both check boxes, however at no time can both check boxes be checked.</span></span>


<span data-ttu-id="b31ce-127">[![한 번에 하나씩만 확인할 수 있습니다.](creating-mutually-exclusive-checkboxes-vb/_static/image2.png)](creating-mutually-exclusive-checkboxes-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b31ce-127">[![Only one checkbox can be checked at a time](creating-mutually-exclusive-checkboxes-vb/_static/image2.png)](creating-mutually-exclusive-checkboxes-vb/_static/image1.png)</span></span>

<span data-ttu-id="b31ce-128">한 번에 하나씩만 확인할 수 있습니다 ([클릭 하 여 큰 이미지 보기](creating-mutually-exclusive-checkboxes-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="b31ce-128">Only one checkbox can be checked at a time ([Click to view full-size image](creating-mutually-exclusive-checkboxes-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="b31ce-129">이전</span><span class="sxs-lookup"><span data-stu-id="b31ce-129">Previous</span></span>](creating-mutually-exclusive-checkboxes-cs.md)
