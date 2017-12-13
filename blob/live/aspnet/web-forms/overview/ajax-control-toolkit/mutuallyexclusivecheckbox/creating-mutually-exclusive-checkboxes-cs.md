---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-cs
title: "상호 배타적인 확인란 (C#)를 만드는 | Microsoft Docs"
author: wenz
description: "일련의 옵션 중 하나에만 선택할 수 있습니다, 라디오 단추는 일반적으로 사용 합니다. 그러나 한 가지 단점으로는: 그룹에 하나의 라디오 단추를 선택 하면..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 8e11b813-ba0d-4c29-b0f8-f65db6dbef1e
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-cs
msc.type: authoredcontent
ms.openlocfilehash: e165c3784b246effcaeafc0ad4274bc0ca81a99c
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="creating-mutually-exclusive-checkboxes-c"></a><span data-ttu-id="27cfb-104">상호 배타적인 확인란 (C#) 만들기</span><span class="sxs-lookup"><span data-stu-id="27cfb-104">Creating Mutually Exclusive Checkboxes (C#)</span></span>
====================
<span data-ttu-id="27cfb-105">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="27cfb-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="27cfb-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="27cfb-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0CS.pdf)</span></span>

> <span data-ttu-id="27cfb-107">일련의 옵션 중 하나에만 선택할 수 있습니다, 라디오 단추는 일반적으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cfb-107">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="27cfb-108">그러나 한 가지 단점으로는: 모든 라디오 단추를 선택 취소 수 없는 그룹에 하나의 라디오 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cfb-108">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="27cfb-109">그러나 확인란은 언제 든 지 checked를 취소할 수, 배타적이 지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="27cfb-109">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="27cfb-110">이 자습서에서는 두 방법 모두 환경의 제공: 함께 사용할 수 없는 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cfb-110">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>


## <a name="overview"></a><span data-ttu-id="27cfb-111">개요</span><span class="sxs-lookup"><span data-stu-id="27cfb-111">Overview</span></span>

<span data-ttu-id="27cfb-112">일련의 옵션 중 하나에만 선택할 수 있습니다, 라디오 단추는 일반적으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cfb-112">When only one of a set of options may be selected, radio buttons are usually used.</span></span> <span data-ttu-id="27cfb-113">그러나 한 가지 단점으로는: 모든 라디오 단추를 선택 취소 수 없는 그룹에 하나의 라디오 단추를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cfb-113">There is a drawback, though: Once one radio button in a group is selected, it is not possible to uncheck all radio buttons.</span></span> <span data-ttu-id="27cfb-114">그러나 확인란은 언제 든 지 checked를 취소할 수, 배타적이 지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="27cfb-114">Check boxes can be unchecked at any time, however are not mutually exclusive.</span></span> <span data-ttu-id="27cfb-115">이 자습서에서는 두 방법 모두 환경의 제공: 함께 사용할 수 없는 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cfb-115">This tutorial provides the best of both approaches: check boxes that are mutually exclusive.</span></span>

## <a name="steps"></a><span data-ttu-id="27cfb-116">단계</span><span class="sxs-lookup"><span data-stu-id="27cfb-116">Steps</span></span>

<span data-ttu-id="27cfb-117">ASP.NET AJAX 컨트롤 Toolkit MutuallyExclusiveCheckBox extender를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="27cfb-117">The ASP.NET AJAX Control Toolkit contains the MutuallyExclusiveCheckBox extender.</span></span> <span data-ttu-id="27cfb-118">이렇게 하면 모든 확인란 그룹 이름에 할당 하는 프로그래머 (`Key` 특성).</span><span class="sxs-lookup"><span data-stu-id="27cfb-118">This enables programmers to assign any checkbox to a group name (`Key` attribute).</span></span> <span data-ttu-id="27cfb-119">모든 확인란 동일한 그룹 내의 하나에만 한 번에 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27cfb-119">From all check boxes within the same group, only one may be selected at one time.</span></span>

<span data-ttu-id="27cfb-120">새 ASP.NET 페이지에 배치 하는 확인란이 두 개부터 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="27cfb-120">Let's start with putting two check boxes on a new ASP.NET page.</span></span> <span data-ttu-id="27cfb-121">더 될 수 있지만 그 중 두 요구 사항을 충족 하는 원칙을 보여 주기 위해:</span><span class="sxs-lookup"><span data-stu-id="27cfb-121">There can be more, but two of them suffice to demonstrate the principle:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample1.aspx)]

<span data-ttu-id="27cfb-122">두 확인란이 모두 선택, MutuallyExclusiveCheckBoxExtender 컨트롤이 페이지에 배치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cfb-122">For both checkboxes, a MutuallyExclusiveCheckBoxExtender control must be put on the page.</span></span> <span data-ttu-id="27cfb-123">두 키 특성 값의 HTML 라디오 단추 요소가 특성을 자신이 속한 그룹을 나타내는 동일 해야 합니다. 값과 마찬가지로 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27cfb-123">Both Key attributes need to have the same value, just as the value attributes of HTML radio button elements must be identical to denote the group they belong to.</span></span> <span data-ttu-id="27cfb-124">Extender의 targetcontrolid가 속성 확인란의 ID를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="27cfb-124">The TargetControlID property of the extender points to the ID of the check box.</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample2.aspx)]

<span data-ttu-id="27cfb-125">마지막으로, ASP.NET AJAX 포함 `ScriptManager` ASP.NET AJAX 컨트롤 도구 키트의 모든 요소에 필요한:</span><span class="sxs-lookup"><span data-stu-id="27cfb-125">Finally, include the ASP.NET AJAX `ScriptManager` which is required by all elements of the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample3.aspx)]

<span data-ttu-id="27cfb-126">하지만 저장 하 고 페이지 실행: 확인 하 고 두 확인란의 선택을 취소 순식간에 확인란을 모두 체크 인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27cfb-126">Save and run the page: You can check and uncheck both check boxes, however at no time can both check boxes be checked.</span></span>


<span data-ttu-id="27cfb-127">[![한 번에 하나씩만 확인할 수 있습니다.](creating-mutually-exclusive-checkboxes-cs/_static/image2.png)](creating-mutually-exclusive-checkboxes-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="27cfb-127">[![Only one checkbox can be checked at a time](creating-mutually-exclusive-checkboxes-cs/_static/image2.png)](creating-mutually-exclusive-checkboxes-cs/_static/image1.png)</span></span>

<span data-ttu-id="27cfb-128">한 번에 하나씩만 확인할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](creating-mutually-exclusive-checkboxes-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="27cfb-128">Only one checkbox can be checked at a time ([Click to view full-size image](creating-mutually-exclusive-checkboxes-cs/_static/image3.png))</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="27cfb-129">다음</span><span class="sxs-lookup"><span data-stu-id="27cfb-129">Next</span></span>](creating-mutually-exclusive-checkboxes-vb.md)
