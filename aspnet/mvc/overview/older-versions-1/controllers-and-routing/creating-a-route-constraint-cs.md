---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
title: 경로 제약 조건 (C#) 만들기 | Microsoft Docs
author: StephenWalther
description: 이 자습서에서는 Stephen Walther 브라우저 정규식과 경로 제약 조건을 만들어 일치 경로 요청 하는 방법을 제어 하는 방법을 보여 줍니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/16/2009
ms.topic: article
ms.assetid: 0bfd06b1-12d3-4fbb-9779-a82e5eb7fe7d
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
msc.type: authoredcontent
ms.openlocfilehash: 3159feb6538e3048f4f235f7d549e692604ca4e7
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30871209"
---
<a name="creating-a-route-constraint-c"></a><span data-ttu-id="8278a-103">경로 제약 조건 (C#) 만들기</span><span class="sxs-lookup"><span data-stu-id="8278a-103">Creating a Route Constraint (C#)</span></span>
====================
<span data-ttu-id="8278a-104">으로 [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="8278a-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="8278a-105">이 자습서에서는 Stephen Walther 브라우저 정규식과 경로 제약 조건을 만들어 일치 경로 요청 하는 방법을 제어 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8278a-105">In this tutorial, Stephen Walther demonstrates how you can control how browser requests match routes by creating route constraints with regular expressions.</span></span>


<span data-ttu-id="8278a-106">경로 제약 조건을 사용 하 여 특정 경로 일치 하는 브라우저 요청을 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8278a-106">You use route constraints to restrict the browser requests that match a particular route.</span></span> <span data-ttu-id="8278a-107">경로 제약 조건을 지정 하는 정규식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8278a-107">You can use a regular expression to specify a route constraint.</span></span>

<span data-ttu-id="8278a-108">예를 들어 있는지 정의한 경로 목록 1의 Global.asax 파일에 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8278a-108">For example, imagine that you have defined the route in Listing 1 in your Global.asax file.</span></span>

<span data-ttu-id="8278a-109">**1-Global.asax.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="8278a-109">**Listing 1 - Global.asax.cs**</span></span>

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample1.cs)]

<span data-ttu-id="8278a-110">목록 1 제품을 라는 경로 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8278a-110">Listing 1 contains a route named Product.</span></span> <span data-ttu-id="8278a-111">브라우저 요청 목록 2에 포함 된 ProductController에 매핑할 제품 경로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8278a-111">You can use the Product route to map browser requests to the ProductController contained in Listing 2.</span></span>

<span data-ttu-id="8278a-112">**Listing 2 - Controllers\ProductController.cs**</span><span class="sxs-lookup"><span data-stu-id="8278a-112">**Listing 2 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample2.cs)]

<span data-ttu-id="8278a-113">제품 컨트롤러에 의해 노출 Details() 작업을 허용 하도록 productId 라는 단일 매개 변수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8278a-113">Notice that the Details() action exposed by the Product controller accepts a single parameter named productId.</span></span> <span data-ttu-id="8278a-114">이 매개 변수는 정수 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="8278a-114">This parameter is an integer parameter.</span></span>

<span data-ttu-id="8278a-115">목록 1에 정의 된 경로 다음 Url 중 하 나와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8278a-115">The route defined in Listing 1 will match any of the following URLs:</span></span>

- <span data-ttu-id="8278a-116">/Product/23</span><span class="sxs-lookup"><span data-stu-id="8278a-116">/Product/23</span></span>
- <span data-ttu-id="8278a-117">/ 제품/7</span><span class="sxs-lookup"><span data-stu-id="8278a-117">/Product/7</span></span>

<span data-ttu-id="8278a-118">안타깝게도, 경로 다음 Url 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8278a-118">Unfortunately, the route will also match the following URLs:</span></span>

- <span data-ttu-id="8278a-119">/ 제품/핵심 성과 지표</span><span class="sxs-lookup"><span data-stu-id="8278a-119">/Product/blah</span></span>
- <span data-ttu-id="8278a-120">/Product/apple</span><span class="sxs-lookup"><span data-stu-id="8278a-120">/Product/apple</span></span>

<span data-ttu-id="8278a-121">Details() 작업에서 정수 매개 변수를 기대 하기 때문에 정수 값 이외의 값을 포함 하는 요청을 만드는 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="8278a-121">Because the Details() action expects an integer parameter, making a request that contains something other than an integer value will cause an error.</span></span> <span data-ttu-id="8278a-122">예를 들어 URL /Product/apple 브라우저에 입력 하는 경우 다음 받아볼 수 오류 페이지에는 그림 1에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8278a-122">For example, if you type the URL /Product/apple into your browser then you will get the error page in Figure 1.</span></span>


<span data-ttu-id="8278a-123">[![새 프로젝트 대화 상자](creating-a-route-constraint-cs/_static/image1.jpg)](creating-a-route-constraint-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8278a-123">[![The New Project dialog box](creating-a-route-constraint-cs/_static/image1.jpg)](creating-a-route-constraint-cs/_static/image1.png)</span></span>

<span data-ttu-id="8278a-124">**그림 01**: 분해 페이지가 표시 ([전체 크기 이미지를 보려면 클릭](creating-a-route-constraint-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="8278a-124">**Figure 01**: Seeing a page explode ([Click to view full-size image](creating-a-route-constraint-cs/_static/image2.png))</span></span>


<span data-ttu-id="8278a-125">실제로 필요한 것 작업을 수행 하는 적절 한 정수 productId를 포함 하는 Url만 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8278a-125">What you really want to do is only match URLs that contain a proper integer productId.</span></span> <span data-ttu-id="8278a-126">경로 일치 하는 Url을 제한 하는 제약 조건 경로 정의 하는 경우 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8278a-126">You can use a constraint when defining a route to restrict the URLs that match the route.</span></span> <span data-ttu-id="8278a-127">목록 3에서 수정 된 제품 경로 정수에만 일치 하는 정규식 제약 조건을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8278a-127">The modified Product route in Listing 3 contains a regular expression constraint that only matches integers.</span></span>

<span data-ttu-id="8278a-128">**3-Global.asax.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="8278a-128">**Listing 3 - Global.asax.cs**</span></span>

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample3.cs)]

<span data-ttu-id="8278a-129">정규식 \d+ 하나 이상의 정수 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="8278a-129">The regular expression \d+ matches one or more integers.</span></span> <span data-ttu-id="8278a-130">이 제한 사항으로 인해 다음 Url을 일치 시킬 제품 경로의:</span><span class="sxs-lookup"><span data-stu-id="8278a-130">This constraint causes the Product route to match the following URLs:</span></span>

- <span data-ttu-id="8278a-131">/ 제품/3</span><span class="sxs-lookup"><span data-stu-id="8278a-131">/Product/3</span></span>
- <span data-ttu-id="8278a-132">/Product/8999</span><span class="sxs-lookup"><span data-stu-id="8278a-132">/Product/8999</span></span>

<span data-ttu-id="8278a-133">하지만 다음 Url에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8278a-133">But not the following URLs:</span></span>

- <span data-ttu-id="8278a-134">/Product/apple</span><span class="sxs-lookup"><span data-stu-id="8278a-134">/Product/apple</span></span>
- <span data-ttu-id="8278a-135">/ 제품</span><span class="sxs-lookup"><span data-stu-id="8278a-135">/Product</span></span>

- <span data-ttu-id="8278a-136">다른 경로에서 이러한 브라우저 요청을 처리 되는 일치 하는 경로가 없는 경우 또는 *리소스를 찾을 수* 오류가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8278a-136">These browser requests will be handled by another route or, if there are no matching routes, a *The resource could not be found* error will be returned.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8278a-137">[이전](creating-custom-routes-cs.md)
> [다음](creating-a-custom-route-constraint-cs.md)</span><span class="sxs-lookup"><span data-stu-id="8278a-137">[Previous](creating-custom-routes-cs.md)
[Next](creating-a-custom-route-constraint-cs.md)</span></span>
