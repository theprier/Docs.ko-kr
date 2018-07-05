---
uid: web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
title: 등급 컨트롤 (C#) 만들기 | Microsoft Docs
author: wenz
description: 전자 상거래 커뮤니티 사이트에서 여러 웹 사이트 비율 문서 또는 항목을 사용자에 게 제공합니다. 이 일반적으로 몇 가지 코딩 작업이 필요 하지만 사항은 합니다...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: 969fb28f-2bff-4fc4-b24a-27f5e2534a37
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 67c66d2a28a247493a0b1ea67e15935c27af80ae
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37830956"
---
<a name="creating-a-rating-control-c"></a><span data-ttu-id="1bd5c-104">등급 컨트롤 (C#) 만들기</span><span class="sxs-lookup"><span data-stu-id="1bd5c-104">Creating a Rating Control (C#)</span></span>
====================
<span data-ttu-id="1bd5c-105">[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="1bd5c-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="1bd5c-106">[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="1bd5c-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0CS.pdf)</span></span>

> <span data-ttu-id="1bd5c-107">전자 상거래 커뮤니티 사이트에서 여러 웹 사이트 비율 문서 또는 항목을 사용자에 게 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1bd5c-107">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="1bd5c-108">이 일반적으로 몇 가지 코딩 작업이 필요 하지만 Control Toolkit 목표인 필요가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bd5c-108">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>


## <a name="overview"></a><span data-ttu-id="1bd5c-109">개요</span><span class="sxs-lookup"><span data-stu-id="1bd5c-109">Overview</span></span>

<span data-ttu-id="1bd5c-110">전자 상거래 커뮤니티 사이트에서 여러 웹 사이트 비율 문서 또는 항목을 사용자에 게 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1bd5c-110">Many websites, from e-commerce to community sites, offer their users to rate articles or items.</span></span> <span data-ttu-id="1bd5c-111">이 일반적으로 몇 가지 코딩 작업이 필요 하지만 Control Toolkit 목표인 필요가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bd5c-111">This usually requires some coding effort, but we do have the Control Toolkit to our disposal.</span></span>

## <a name="steps"></a><span data-ttu-id="1bd5c-112">단계</span><span class="sxs-lookup"><span data-stu-id="1bd5c-112">Steps</span></span>

<span data-ttu-id="1bd5c-113">먼저, (적어도) 두 종류의 이미지 해야: 채워진 프로그램용 등급 항목 및 빈 등급 항목에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bd5c-113">First of all, you need (at least) two kinds of images: one for a filled out rating item, and one for an empty rating item.</span></span> <span data-ttu-id="1bd5c-114">등급 항목은 일반적으로 별 또는 웃는 얼굴을 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bd5c-114">A rating item is usually a star or a smiley.</span></span> <span data-ttu-id="1bd5c-115">이 시나리오에서는 찾아야 세 파일, smiley.png empty.png 및 웃는 done.png이이 자습서에 대 한 소스 코드 다운로드의 일부로.</span><span class="sxs-lookup"><span data-stu-id="1bd5c-115">For this scenario, you find three files, smiley.png and empty.png and smiley-done.png as part of the source code downloads for this tutorial.</span></span>

<span data-ttu-id="1bd5c-116">그런 다음 새 ASP.NET 파일을 만들고 추가 시작을 `ScriptManager` 컨트롤을 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bd5c-116">Then, create a new ASP.NET file and start with adding a `ScriptManager` control to it:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample1.aspx)]

<span data-ttu-id="1bd5c-117">그런 다음 추가 `Rating` ASP.NET AJAX Control Toolkit에서 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bd5c-117">Then, add the `Rating` control from the ASP.NET AJAX Control Toolkit.</span></span> <span data-ttu-id="1bd5c-118">다음 특성을이 예제에 대해 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bd5c-118">The following attributes need to be set for this example:</span></span>

- <span data-ttu-id="1bd5c-119">`CurrentRating` 사용할 초기 등급</span><span class="sxs-lookup"><span data-stu-id="1bd5c-119">`CurrentRating` the initial rating to be used</span></span>
- <span data-ttu-id="1bd5c-120">`MaxRating` 최대 등급</span><span class="sxs-lookup"><span data-stu-id="1bd5c-120">`MaxRating` the maximum rating</span></span>
- <span data-ttu-id="1bd5c-121">`EmptyStarCssClass` 등급 항목이 (별표)를 사용 하는 CSS 클래스 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bd5c-121">`EmptyStarCssClass` the CSS class to use when a rating item ( star ) is empty</span></span>
- <span data-ttu-id="1bd5c-122">`FilledStarCssClass` 등급 항목이 (별표)를 사용 하는 CSS 클래스 작성</span><span class="sxs-lookup"><span data-stu-id="1bd5c-122">`FilledStarCssClass` the CSS class to use when a rating item ( star ) is filled out</span></span>
- <span data-ttu-id="1bd5c-123">`StarCssClass` 표시 상태에 사용할 CSS 클래스</span><span class="sxs-lookup"><span data-stu-id="1bd5c-123">`StarCssClass` the CSS class to use for a visible stat</span></span>
- <span data-ttu-id="1bd5c-124">`WaitingStarCssClass` 별 등급을 서버에 다시 보내는 동안 사용 하는 CSS 클래스</span><span class="sxs-lookup"><span data-stu-id="1bd5c-124">`WaitingStarCssClass` the CSS class to use while a star rating is sent back to the server</span></span>

<span data-ttu-id="1bd5c-125">다음은 등급 컨트롤 5를 사용 하 여 만드는 태그는 none 작성 처음에 항목 (smileys):</span><span class="sxs-lookup"><span data-stu-id="1bd5c-125">And here is the markup which creates a rating control with five items (smileys) of which none is filled out initially:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample2.aspx)]

<span data-ttu-id="1bd5c-126">세 개의 참조 된 CSS 클래스 이제 필요 적절 한 이미지 파일을 표시 하려면 CSS를 사용 하 여 작업을 수행 하는 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bd5c-126">The three referenced CSS classes now need to show the appropriate image files, which is easy to do using CSS:</span></span>

[!code-css[Main](creating-a-rating-control-cs/samples/sample3.css)]

<span data-ttu-id="1bd5c-127">수 있도록 세 개의 이미지의 높이 너비를 제공한 그렇지 않은 경우 표시를 잠시 messed 보일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bd5c-127">Make sure that you provide the width and height of the three images, otherwise the display may look a bit messed up.</span></span>

<span data-ttu-id="1bd5c-128">마지막으로, 등급의 결과 해야 될 사용자에 게 표시 (또는 최소한 데이터베이스에 저장).</span><span class="sxs-lookup"><span data-stu-id="1bd5c-128">Finally, the result of the rating should be displayed to the user (or, at least saved in a database).</span></span> <span data-ttu-id="1bd5c-129">따라서 등급 폼을 서버에 다시 게시 하는 텍스트 메시지 및 전송 단추가의 출력에 대 한 레이블을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bd5c-129">So add a label for the output of a text message and a submit button to post back the rating form to the server:</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample4.aspx)]

<span data-ttu-id="1bd5c-130">서버 쪽 코드를 통해 등급 컨트롤에 액세스할 해당 `ID` 액세스 하면 해당 `CurrentRating` 예제 값을 0에서 5 사이의 등급 선택한 항목을 숫자 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="1bd5c-130">In the server-side code, access the Rating control via its `ID` and then access its `CurrentRating` property which is the number of the selected rating items, in our example a value between 0 and 5.</span></span>

[!code-aspx[Main](creating-a-rating-control-cs/samples/sample5.aspx)]

<span data-ttu-id="1bd5c-131">페이지를 저장 하 고 브라우저에 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bd5c-131">Save the page and load it into your browser.</span></span> <span data-ttu-id="1bd5c-132">JavaScript 효과 발생 (처음에 비어 있음) 등급 항목 위로 마우스를 가져가면: 등급 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bd5c-132">When you hover over the (initially empty) rating items, a JavaScript effect occurs: The rating changes.</span></span> <span data-ttu-id="1bd5c-133">별 집합이 클릭 하면 현재 등급 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1bd5c-133">When you click on the set of stars, the current rating is retained.</span></span> <span data-ttu-id="1bd5c-134">마지막으로 폼을 전송 하면 서버 쪽 코드를 선택한 등급을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bd5c-134">Finally, when you submit the form, the server-side code outputs the selected rating.</span></span>


<span data-ttu-id="1bd5c-135">[![최소한의 코드를 사용 하 여 등급 시스템 만들기](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1bd5c-135">[![Creating a rating system with minimal code](creating-a-rating-control-cs/_static/image2.png)](creating-a-rating-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="1bd5c-136">최소한의 코드를 사용 하 여 등급 시스템 만들기 ([클릭 하 여 큰 이미지 보기](creating-a-rating-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="1bd5c-136">Creating a rating system with minimal code ([Click to view full-size image](creating-a-rating-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="1bd5c-137">다음</span><span class="sxs-lookup"><span data-stu-id="1bd5c-137">Next</span></span>](creating-a-rating-control-vb.md)
