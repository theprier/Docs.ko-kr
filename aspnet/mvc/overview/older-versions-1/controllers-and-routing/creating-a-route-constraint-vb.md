---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-vb
title: 경로 제약 조건 (VB) 만들기 | Microsoft Docs
author: StephenWalther
description: 이 자습서에서는 Stephen walther가 브라우저 정규식을 사용 하 여 경로 제약 조건을 만들면 일치 경로 요청 하는 방법을 제어 하는 방법을 보여 줍니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/16/2009
ms.topic: article
ms.assetid: b7cce113-c82c-45bf-b97b-357e5d9f7f56
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-vb
msc.type: authoredcontent
ms.openlocfilehash: 74afb5653f01a5291b77da1bc672b362fec118a0
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37364033"
---
<a name="creating-a-route-constraint-vb"></a><span data-ttu-id="ba3f8-103">경로 제약 조건 (VB) 만들기</span><span class="sxs-lookup"><span data-stu-id="ba3f8-103">Creating a Route Constraint (VB)</span></span>
====================
<span data-ttu-id="ba3f8-104">[Stephen walther가](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="ba3f8-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="ba3f8-105">이 자습서에서는 Stephen walther가 브라우저 정규식을 사용 하 여 경로 제약 조건을 만들면 일치 경로 요청 하는 방법을 제어 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ba3f8-105">In this tutorial, Stephen Walther demonstrates how you can control how browser requests match routes by creating route constraints with regular expressions.</span></span>


<span data-ttu-id="ba3f8-106">경로 제약 조건은 사용 하 여 특정 경로 일치 하는 브라우저 요청을 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba3f8-106">You use route constraints to restrict the browser requests that match a particular route.</span></span> <span data-ttu-id="ba3f8-107">경로 제약 조건을 지정 하는 정규식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba3f8-107">You can use a regular expression to specify a route constraint.</span></span>

<span data-ttu-id="ba3f8-108">예를 들어 정의 했다고 경로 목록 1에서 Global.asax 파일에 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba3f8-108">For example, imagine that you have defined the route in Listing 1 in your Global.asax file.</span></span>

<span data-ttu-id="ba3f8-109">**1-Global.asax.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="ba3f8-109">**Listing 1 - Global.asax.vb**</span></span>

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample1.vb)]

<span data-ttu-id="ba3f8-110">목록 1 Product 라는 경로 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba3f8-110">Listing 1 contains a route named Product.</span></span> <span data-ttu-id="ba3f8-111">브라우저 요청 목록 2에 포함 된 ProductController 매핑할 제품 경로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba3f8-111">You can use the Product route to map browser requests to the ProductController contained in Listing 2.</span></span>

<span data-ttu-id="ba3f8-112">**Listing 2 - Controllers\ProductController.vb**</span><span class="sxs-lookup"><span data-stu-id="ba3f8-112">**Listing 2 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample2.vb)]

<span data-ttu-id="ba3f8-113">제품 컨트롤러에 의해 노출 Details() 작업 productId 라는 단일 매개 변수를 허용 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba3f8-113">Notice that the Details() action exposed by the Product controller accepts a single parameter named productId.</span></span> <span data-ttu-id="ba3f8-114">이 매개 변수는 정수 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ba3f8-114">This parameter is an integer parameter.</span></span>

<span data-ttu-id="ba3f8-115">목록 1에 정의 된 경로 다음 Url 중 하나라도 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba3f8-115">The route defined in Listing 1 will match any of the following URLs:</span></span>

- <span data-ttu-id="ba3f8-116">/ 제품/23</span><span class="sxs-lookup"><span data-stu-id="ba3f8-116">/Product/23</span></span>
- <span data-ttu-id="ba3f8-117">/ 제품/7</span><span class="sxs-lookup"><span data-stu-id="ba3f8-117">/Product/7</span></span>

<span data-ttu-id="ba3f8-118">그러나 경로 다음 Url 일치도 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba3f8-118">Unfortunately, the route will also match the following URLs:</span></span>

- <span data-ttu-id="ba3f8-119">/ 제품/아니오</span><span class="sxs-lookup"><span data-stu-id="ba3f8-119">/Product/blah</span></span>
- <span data-ttu-id="ba3f8-120">/ 제품/apple</span><span class="sxs-lookup"><span data-stu-id="ba3f8-120">/Product/apple</span></span>

<span data-ttu-id="ba3f8-121">Details() 작업에서 정수 매개 변수 예상 하기 때문에 정수 이외의 값을 포함 하는 요청을 수행 하면 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba3f8-121">Because the Details() action expects an integer parameter, making a request that contains something other than an integer value will cause an error.</span></span> <span data-ttu-id="ba3f8-122">예를 들어 URL /Product/apple 브라우저에 입력 하는 경우 다음 얻게 됩니다 오류 페이지 그림 1.</span><span class="sxs-lookup"><span data-stu-id="ba3f8-122">For example, if you type the URL /Product/apple into your browser then you will get the error page in Figure 1.</span></span>


<span data-ttu-id="ba3f8-123">[![새 프로젝트 대화 상자](creating-a-route-constraint-vb/_static/image1.jpg)](creating-a-route-constraint-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ba3f8-123">[![The New Project dialog box](creating-a-route-constraint-vb/_static/image1.jpg)](creating-a-route-constraint-vb/_static/image1.png)</span></span>

<span data-ttu-id="ba3f8-124">**그림 01**: 분해 하는 페이지가 표시 ([큰 이미지를 보려면 클릭](creating-a-route-constraint-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="ba3f8-124">**Figure 01**: Seeing a page explode ([Click to view full-size image](creating-a-route-constraint-vb/_static/image2.png))</span></span>


<span data-ttu-id="ba3f8-125">실제로 원하는 작업을 수행 하는 Url에는 적절 한 정수 productId와만 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba3f8-125">What you really want to do is only match URLs that contain a proper integer productId.</span></span> <span data-ttu-id="ba3f8-126">경로 일치 하는 Url을 제한 하는 제약 조건 경로 정의할 때 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba3f8-126">You can use a constraint when defining a route to restrict the URLs that match the route.</span></span> <span data-ttu-id="ba3f8-127">보기 3의 수정 된 제품 경로 정수 일치 하는 정규식 제약 조건을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba3f8-127">The modified Product route in Listing 3 contains a regular expression constraint that only matches integers.</span></span>

<span data-ttu-id="ba3f8-128">**3-Global.asax.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="ba3f8-128">**Listing 3 - Global.asax.vb**</span></span>

[!code-vb[Main](creating-a-route-constraint-vb/samples/sample3.vb)]

<span data-ttu-id="ba3f8-129">정규식 \d+ 정수 하나 이상을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ba3f8-129">The regular expression \d+ matches one or more integers.</span></span> <span data-ttu-id="ba3f8-130">이 제약 조건으로 인해 다음 Url에 맞게 제품 경로:</span><span class="sxs-lookup"><span data-stu-id="ba3f8-130">This constraint causes the Product route to match the following URLs:</span></span>

- <span data-ttu-id="ba3f8-131">/ 제품/3</span><span class="sxs-lookup"><span data-stu-id="ba3f8-131">/Product/3</span></span>
- <span data-ttu-id="ba3f8-132">/ 제품/8999</span><span class="sxs-lookup"><span data-stu-id="ba3f8-132">/Product/8999</span></span>

<span data-ttu-id="ba3f8-133">하지만 다음 Url에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ba3f8-133">But not the following URLs:</span></span>

- <span data-ttu-id="ba3f8-134">/ 제품/apple</span><span class="sxs-lookup"><span data-stu-id="ba3f8-134">/Product/apple</span></span>
- <span data-ttu-id="ba3f8-135">/ 제품</span><span class="sxs-lookup"><span data-stu-id="ba3f8-135">/Product</span></span>

<span data-ttu-id="ba3f8-136">이러한 브라우저 요청을 다른 경로로 처리 또는 일치 하는 경로가 없을 경우는 *리소스를 찾을 수 없습니다* 오류가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba3f8-136">These browser requests will be handled by another route or, if there are no matching routes, a *The resource could not be found* error will be returned.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ba3f8-137">[이전](creating-custom-routes-vb.md)
> [다음](creating-a-custom-route-constraint-vb.md)</span><span class="sxs-lookup"><span data-stu-id="ba3f8-137">[Previous](creating-custom-routes-vb.md)
[Next](creating-a-custom-route-constraint-vb.md)</span></span>
