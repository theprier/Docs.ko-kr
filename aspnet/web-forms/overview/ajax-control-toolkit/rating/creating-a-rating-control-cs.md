---
uid: web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
title: 등급 컨트롤 (C#) 만들기 | Microsoft Docs
author: wenz
description: 전자 상거래 커뮤니티 사이트로에서 대부분의 웹 사이트 속도 문서 또는 항목에 사용자에 게 제공할 합니다. 이 일반적으로 일부 코딩 작업 필요 하지만 대 한는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 969fb28f-2bff-4fc4-b24a-27f5e2534a37
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
msc.type: authoredcontent
ms.openlocfilehash: a48cf0ed9402e2875e87ba7bdb76afc5f501a670
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30879597"
---
<a name="creating-a-rating-control-c"></a><span data-ttu-id="76333-104">등급 컨트롤 (C#) 만들기</span><span class="sxs-lookup"><span data-stu-id="76333-104">Creating a Rating Control (C#)</span></span>
====================
<span data-ttu-id="76333-105">으로 [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="76333-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="76333-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="76333-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)</span></span>

> <span data-ttu-id="76333-107">전자 상거래 커뮤니티 사이트로에서 대부분의 웹 사이트 속도 문서 또는 항목에 사용자에 게 제공할 합니다.</span><span class="sxs-lookup"><span data-stu-id="76333-107">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="76333-108">이 일반적으로 일부 코딩 작업 필요 했지만 우리의 받고 제어 도구 키트가 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76333-108">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>


## <a name="overview"></a><span data-ttu-id="76333-109">개요</span><span class="sxs-lookup"><span data-stu-id="76333-109">Overview</span></span>

<span data-ttu-id="76333-110">전자 상거래 커뮤니티 사이트로에서 대부분의 웹 사이트 속도 문서 또는 항목에 사용자에 게 제공할 합니다.</span><span class="sxs-lookup"><span data-stu-id="76333-110">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="76333-111">이 일반적으로 일부 코딩 작업 필요 했지만 우리의 받고 제어 도구 키트가 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76333-111">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>

## <a name="steps"></a><span data-ttu-id="76333-112">단계</span><span class="sxs-lookup"><span data-stu-id="76333-112">Steps</span></span>

<span data-ttu-id="76333-113">(이상)의 두 종류의 이미지를 필요한 우선,: 채워진는 대 한 등급 항목 및 빈 등급 항목에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="76333-113">First of all, you need (at least) two kinds of images: one for a filled out rating item, and one for an empty rating item.</span></span> <span data-ttu-id="76333-114">등급 항목은 일반적으로 별모양 또는 웃는 합니다.</span><span class="sxs-lookup"><span data-stu-id="76333-114">A rating item is usually a star or a smiley.</span></span> <span data-ttu-id="76333-115">이 시나리오에 대 한이 자습서에 대 한 소스 코드 다운로드의 일부로 세 개의 파일, smiley.png empty.png 및 웃는 done.png를 찾을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76333-115">For this scenario, you find three files, smiley.png and empty.png and smiley-done.png as part of the source code downloads for this tutorial.</span></span>

<span data-ttu-id="76333-116">그런 다음 새 ASP.NET 파일을 만들고 추가 작업부터 시작는 `ScriptManager` 를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="76333-116">Then, create a new ASP.NET file and start with adding a `ScriptManager` control to it:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample1.aspx)]

<span data-ttu-id="76333-117">그런 다음 추가 `Rating` ASP.NET AJAX 컨트롤 도구 키트에서 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="76333-117">Then, add the `Rating` control from the ASP.NET AJAX Control Toolkit.</span></span> <span data-ttu-id="76333-118">이 예제에 대 한 설정 해야 하는 다음 특성:</span><span class="sxs-lookup"><span data-stu-id="76333-118">The following attributes need to be set for this example:</span></span>

- <span data-ttu-id="76333-119">`CurrentRating` 사용할 초기 등급</span><span class="sxs-lookup"><span data-stu-id="76333-119">`CurrentRating` the initial rating to be used</span></span>
- <span data-ttu-id="76333-120">`MaxRating` 최대 등급</span><span class="sxs-lookup"><span data-stu-id="76333-120">`MaxRating` the maximum rating</span></span>
- <span data-ttu-id="76333-121">`EmptyStarCssClass` 등급 항목 (별) 비어 있을 때 사용 하는 CSS 클래스</span><span class="sxs-lookup"><span data-stu-id="76333-121">`EmptyStarCssClass` the CSS class to use when a rating item ( star ) is empty</span></span>
- <span data-ttu-id="76333-122">`FilledStarCssClass` 등급 항목 (별)을 채울 때 사용 하는 CSS 클래스</span><span class="sxs-lookup"><span data-stu-id="76333-122">`FilledStarCssClass` the CSS class to use when a rating item ( star ) is filled out</span></span>
- <span data-ttu-id="76333-123">`StarCssClass` 표시 상태에 대 한 사용 하는 CSS 클래스</span><span class="sxs-lookup"><span data-stu-id="76333-123">`StarCssClass` the CSS class to use for a visible stat</span></span>
- <span data-ttu-id="76333-124">`WaitingStarCssClass` 별 등급 서버에 다시 보내는 동안 사용 하는 CSS 클래스</span><span class="sxs-lookup"><span data-stu-id="76333-124">`WaitingStarCssClass` the CSS class to use while a star rating is sent back to the server</span></span>

<span data-ttu-id="76333-125">태그를 5 개 등급 컨트롤을 만드는 것는 none 입력 처음 항목 (smileys):</span><span class="sxs-lookup"><span data-stu-id="76333-125">And here is the markup which creates a rating control with five items (smileys) of which none is filled out initially:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample2.aspx)]

<span data-ttu-id="76333-126">세 개의 참조 된 CSS 클래스 이제 해야 할 적절 한 이미지 파일 보기 CSS를 사용 하 여 작업을 수행 하는 하기가 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="76333-126">The three referenced CSS classes now need to show the appropriate image files, which is easy to do using CSS:</span></span>

[!code-css[Main](creating-a-rating-control-cs/samples/sample3.css)]

<span data-ttu-id="76333-127">세 개의 이미지의 높이 너비를 제공, 그렇지 않으면 디스플레이를 약간 messed 표시 될 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="76333-127">Make sure that you provide the width and height of the three images, otherwise the display may look a bit messed up.</span></span>

<span data-ttu-id="76333-128">마지막으로, 등급의 결과 해야 될 사용자에 게 표시 (또는 이상 데이터베이스에 저장) 합니다.</span><span class="sxs-lookup"><span data-stu-id="76333-128">Finally, the result of the rating should be displayed to the user (or, at least saved in a database).</span></span> <span data-ttu-id="76333-129">따라서 등급 폼을 서버에 다시 게시 하는 문자 메시지 및 전송 단추가의 출력에 대 한 레이블을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="76333-129">So add a label for the output of a text message and a submit button to post back the rating form to the server:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample4.aspx)]

<span data-ttu-id="76333-130">서버 쪽 코드를 통해 등급 컨트롤에 액세스 해당 `ID` 다음 액세스 해당 `CurrentRating` 선택한 등급 항목 예에서 0에서 5 사이의 값 수에 해당 하는 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76333-130">In the server-side code, access the Rating control via its `ID` and then access its `CurrentRating` property which is the number of the selected rating items, in our example a value between 0 and 5.</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample5.aspx)]

<span data-ttu-id="76333-131">페이지를 저장 하 고 브라우저에 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="76333-131">Save the page and load it into your browser.</span></span> <span data-ttu-id="76333-132">JavaScript 효과 발생 (처음 비어 있음) 등급 항목 위로 마우스를 가져가면: 등급 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="76333-132">When you hover over the (initially empty) rating items, a JavaScript effect occurs: The rating changes.</span></span> <span data-ttu-id="76333-133">별점 집합을 클릭할 때 현재 등급 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76333-133">When you click on the set of stars, the current rating is retained.</span></span> <span data-ttu-id="76333-134">마지막으로, 양식을 전송 하면 서버 쪽 코드는 선택한 등급이 출력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76333-134">Finally, when you submit the form, the server-side code outputs the selected rating.</span></span>


<span data-ttu-id="76333-135">[![최소한의 코드를 사용 하 여 등급 시스템 만들기](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="76333-135">[![Creating a rating system with minimal code](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="76333-136">최소한의 코드를 사용 하 여 등급 시스템 만들기 ([전체 크기 이미지를 보려면 클릭](creating-a-rating-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="76333-136">Creating a rating system with minimal code ([Click to view full-size image](creating-a-rating-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="76333-137">다음</span><span class="sxs-lookup"><span data-stu-id="76333-137">Next</span></span>](creating-a-rating-control-vb.md)
