---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
title: 사용자 지정 경로 (C#) 만들기 | Microsoft Docs
author: microsoft
description: ASP.NET MVC 응용 프로그램에 사용자 지정 경로 추가 하는 방법에 알아봅니다. 이 자습서에서는 Global.asax 파일의 기본 경로 테이블을 수정 하는 방법을 알아봅니다.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 3cd08f02-8763-490a-b625-2ac96a24b73f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
msc.type: authoredcontent
ms.openlocfilehash: 1d7a25f9d257320c252408ae251e2f9f620930d8
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829624"
---
<a name="creating-custom-routes-c"></a><span data-ttu-id="799b1-104">사용자 지정 경로 만들기 (C#)</span><span class="sxs-lookup"><span data-stu-id="799b1-104">Creating Custom Routes (C#)</span></span>
====================
<span data-ttu-id="799b1-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="799b1-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="799b1-106">ASP.NET MVC 응용 프로그램에 사용자 지정 경로 추가 하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="799b1-106">Learn how to add custom routes to an ASP.NET MVC application.</span></span> <span data-ttu-id="799b1-107">이 자습서에서는 Global.asax 파일의 기본 경로 테이블을 수정 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="799b1-107">In this tutorial, you learn how to modify the default route table in the Global.asax file.</span></span>


<span data-ttu-id="799b1-108">이 자습서에서는 ASP.NET MVC 응용 프로그램에 사용자 지정 경로 추가 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="799b1-108">In this tutorial, you learn how to add a custom route to an ASP.NET MVC application.</span></span> <span data-ttu-id="799b1-109">사용자 지정 경로 사용 하 여 Global.asax 파일의 기본 경로 테이블을 수정 하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="799b1-109">You learn how to modify the default route table in the Global.asax file with a custom route.</span></span>

<span data-ttu-id="799b1-110">많은 간단한 ASP.NET MVC 응용 프로그램에 대 한 기본 경로 테이블을 문제 없이 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="799b1-110">For many simple ASP.NET MVC applications, the default route table will work just fine.</span></span> <span data-ttu-id="799b1-111">그러나 라우팅 요구를 특수 발견할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="799b1-111">However, you might discover that you have specialized routing needs.</span></span> <span data-ttu-id="799b1-112">이 경우 사용자 지정 경로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="799b1-112">In that case, you can create a custom route.</span></span>

<span data-ttu-id="799b1-113">예를 들어 블로그 응용 프로그램을 빌드하고 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="799b1-113">Imagine, for example, that you are building a blog application.</span></span> <span data-ttu-id="799b1-114">다음과 같은 들어오는 요청을 처리 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="799b1-114">You might want to handle incoming requests that look like this:</span></span>

<span data-ttu-id="799b1-115">월 보관 2009 년 12-25-</span><span class="sxs-lookup"><span data-stu-id="799b1-115">/Archive/12-25-2009</span></span>

<span data-ttu-id="799b1-116">날짜에 해당 하는 블로그 항목을 반환 하려는 사용자가이 요청에 입력 하면 2009 년 12 월 25입니다.</span><span class="sxs-lookup"><span data-stu-id="799b1-116">When a user enters this request, you want to return the blog entry that corresponds to the date 12/25/2009.</span></span> <span data-ttu-id="799b1-117">이 유형의 요청을 처리 하기 위해 사용자 지정 경로를 만들고 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="799b1-117">In order to handle this type of request, you need to create a custom route.</span></span>

<span data-ttu-id="799b1-118">목록 1에서 Global.asax 파일에 블로그, /Archive/ 처럼 보이는 요청을 처리는 명명 된 새 사용자 지정 경로*입력 날짜*합니다.</span><span class="sxs-lookup"><span data-stu-id="799b1-118">The Global.asax file in Listing 1 contains a new custom route, named Blog, which handles requests that look like /Archive/*entry date*.</span></span>

<span data-ttu-id="799b1-119">**1-(사용자 정의 경로)와 함께 Global.asax 나열**</span><span class="sxs-lookup"><span data-stu-id="799b1-119">**Listing 1 - Global.asax (with custom route)**</span></span>

[!code-csharp[Main](creating-custom-routes-cs/samples/sample1.cs)]

<span data-ttu-id="799b1-120">경로 테이블에 추가 하는 경로 순서가 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="799b1-120">The order of the routes that you add to the route table is important.</span></span> <span data-ttu-id="799b1-121">이 새 사용자 지정 블로그 경로 기존 기본 경로 앞에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="799b1-121">Our new custom Blog route is added before the existing Default route.</span></span> <span data-ttu-id="799b1-122">순서 반대로 하는 경우 다음 기본 경로 항상 호출 됩니다는 사용자 지정 경로 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="799b1-122">If you reversed the order, then the Default route always will get called instead of the custom route.</span></span>

<span data-ttu-id="799b1-123">사용자 지정 블로그 경로/보관/로 시작 하는 모든 요청을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="799b1-123">The custom Blog route matches any request that starts with /Archive/.</span></span> <span data-ttu-id="799b1-124">따라서 다음 Url은 모두 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="799b1-124">So, it matches all of the following URLs:</span></span>

- <span data-ttu-id="799b1-125">월 보관 2009 년 12-25-</span><span class="sxs-lookup"><span data-stu-id="799b1-125">/Archive/12-25-2009</span></span>

- <span data-ttu-id="799b1-126">/ 보관/10 2004 년 6 월 일</span><span class="sxs-lookup"><span data-stu-id="799b1-126">/Archive/10-6-2004</span></span>

- <span data-ttu-id="799b1-127">/ 보관/apple</span><span class="sxs-lookup"><span data-stu-id="799b1-127">/Archive/apple</span></span>

<span data-ttu-id="799b1-128">사용자 지정 경로 들어오는 요청 archive 컨트롤러에 매핑되고 Entry() 작업을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="799b1-128">The custom route maps the incoming request to a controller named Archive and invokes the Entry() action.</span></span> <span data-ttu-id="799b1-129">Entry() 메서드가 호출 될 때 입력 날짜 entryDate 명명 된 매개 변수로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="799b1-129">When the Entry() method is called, the entry date is passed as a parameter named entryDate.</span></span>

<span data-ttu-id="799b1-130">목록 2의 컨트롤러를 사용 하 여 블로그 사용자 지정 경로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="799b1-130">You can use the Blog custom route with the controller in Listing 2.</span></span>

<span data-ttu-id="799b1-131">**2-ArchiveController.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="799b1-131">**Listing 2 - ArchiveController.cs**</span></span>

[!code-csharp[Main](creating-custom-routes-cs/samples/sample2.cs)]

<span data-ttu-id="799b1-132">목록 2에서 Entry() 메서드를 DateTime 형식의 매개 변수를 허용 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="799b1-132">Notice that the Entry() method in Listing 2 accepts a parameter of type DateTime.</span></span> <span data-ttu-id="799b1-133">MVC 프레임 워크는 입력 날짜 URL에서 날짜/시간 값으로 자동 변환 하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="799b1-133">The MVC framework is smart enough to convert the entry date from the URL into a DateTime value automatically.</span></span> <span data-ttu-id="799b1-134">URL에서 항목 날짜 매개 변수를 날짜/시간으로 변환할 수 없습니다, 오류 발생 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="799b1-134">If the entry date parameter from the URL cannot be converted to a DateTime, an error is raised (see Figure 1).</span></span>

<span data-ttu-id="799b1-135">**그림 1-매개 변수 변환 오류**</span><span class="sxs-lookup"><span data-stu-id="799b1-135">**Figure 1 - Error from converting parameter**</span></span>


<span data-ttu-id="799b1-136">[![새 프로젝트 대화 상자](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="799b1-136">[![The New Project dialog box](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)</span></span>

<span data-ttu-id="799b1-137">**그림 01**: 매개 변수 변환에서 오류 ([큰 이미지를 보려면 클릭](creating-custom-routes-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="799b1-137">**Figure 01**: Error from converting parameter ([Click to view full-size image](creating-custom-routes-cs/_static/image2.png))</span></span>


## <a name="summary"></a><span data-ttu-id="799b1-138">요약</span><span class="sxs-lookup"><span data-stu-id="799b1-138">Summary</span></span>

<span data-ttu-id="799b1-139">이 자습서의 목표는 사용자 지정 경로 만드는 방법을 보여 주기 위해 했습니다.</span><span class="sxs-lookup"><span data-stu-id="799b1-139">The goal of this tutorial was to demonstrate how you can create a custom route.</span></span> <span data-ttu-id="799b1-140">블로그 항목을 나타내는 Global.asax 파일에 경로 테이블에 사용자 지정 경로 추가 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="799b1-140">You learned how to add a custom route to the route table in the Global.asax file that represents blog entries.</span></span> <span data-ttu-id="799b1-141">블로그 항목에 대 한 요청 ArchiveController 라는 컨트롤러 및 Entry() 라는 컨트롤러 작업에 매핑하는 방법에 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="799b1-141">We discussed how to map requests for blog entries to a controller named ArchiveController and a controller action named Entry().</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="799b1-142">[이전](aspnet-mvc-controllers-overview-cs.md)
> [다음](creating-a-route-constraint-cs.md)</span><span class="sxs-lookup"><span data-stu-id="799b1-142">[Previous](aspnet-mvc-controllers-overview-cs.md)
[Next](creating-a-route-constraint-cs.md)</span></span>
