---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
title: 작업 필터 (C#) 이해 | Microsoft Docs
author: microsoft
description: 이 자습서의 목표 작업 필터를 설명 하는 것입니다. 작업 필터는 컨트롤러 동작-또는 전체 컨트롤러에 적용할 수 있는 특성 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/16/2008
ms.topic: article
ms.assetid: a94e4e81-40c1-47b7-8613-126a1a6cc93d
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
msc.type: authoredcontent
ms.openlocfilehash: d68933297329370e227f524c4b96ed7e259ef833
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="understanding-action-filters-c"></a><span data-ttu-id="8606b-104">작업 필터 (C#) 이해</span><span class="sxs-lookup"><span data-stu-id="8606b-104">Understanding Action Filters (C#)</span></span>
====================
<span data-ttu-id="8606b-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="8606b-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="8606b-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="8606b-106">Download PDF</span></span>](http://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_CS.pdf)

> <span data-ttu-id="8606b-107">이 자습서의 목표 작업 필터를 설명 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-107">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="8606b-108">작업 필터는 컨트롤러 동작-또는 동작이 실행 되는 방법을 수정 하는 전체 controller--에 적용할 수 있는 특성.</span><span class="sxs-lookup"><span data-stu-id="8606b-108">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span>


## <a name="understanding-action-filters"></a><span data-ttu-id="8606b-109">작업 필터 이해</span><span class="sxs-lookup"><span data-stu-id="8606b-109">Understanding Action Filters</span></span>

<span data-ttu-id="8606b-110">이 자습서의 목표 작업 필터를 설명 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-110">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="8606b-111">작업 필터는 컨트롤러 동작-또는 동작이 실행 되는 방법을 수정 하는 전체 controller--에 적용할 수 있는 특성.</span><span class="sxs-lookup"><span data-stu-id="8606b-111">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span> <span data-ttu-id="8606b-112">ASP.NET MVC 프레임 워크에 몇 가지 작업 필터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-112">The ASP.NET MVC framework includes several action filters:</span></span>

- <span data-ttu-id="8606b-113">OutputCache –이 작업 필터는 지정된 된 기간에 대 한 컨트롤러 작업의 출력을 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-113">OutputCache – This action filter caches the output of a controller action for a specified amount of time.</span></span>
- <span data-ttu-id="8606b-114">이 작업 필터 HandleError – 컨트롤러 작업이 실행 될 때 발생 하는 오류를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-114">HandleError – This action filter handles errors raised when a controller action executes.</span></span>
- <span data-ttu-id="8606b-115">권한 부여-이 작업 필터를 사용 하면 특정 사용자 또는 역할에 대 한 액세스를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-115">Authorize – This action filter enables you to restrict access to a particular user or role.</span></span>

<span data-ttu-id="8606b-116">사용자 고유의 사용자 지정 작업 필터를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-116">You also can create your own custom action filters.</span></span> <span data-ttu-id="8606b-117">예를 들어 사용자 지정 인증 시스템을 구현 하기 위해 사용자 지정 작업 필터를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-117">For example, you might want to create a custom action filter in order to implement a custom authentication system.</span></span> <span data-ttu-id="8606b-118">또는 컨트롤러 동작에 의해 반환 되는 뷰 데이터를 수정 하는 작업 필터를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-118">Or, you might want to create an action filter that modifies the view data returned by a controller action.</span></span>

<span data-ttu-id="8606b-119">이 자습서에서는 처음부터 다시 작업 필터 작성 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-119">In this tutorial, you learn how to build an action filter from the ground up.</span></span> <span data-ttu-id="8606b-120">Visual Studio 출력 창에 다른 작업의 처리 단계를 기록 하는 로그 작업 필터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-120">We create a Log action filter that logs different stages of the processing of an action to the Visual Studio Output window.</span></span>

### <a name="using-an-action-filter"></a><span data-ttu-id="8606b-121">작업 필터를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="8606b-121">Using an Action Filter</span></span>

<span data-ttu-id="8606b-122">작업 필터 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-122">An action filter is an attribute.</span></span> <span data-ttu-id="8606b-123">대부분의 작업 필터는 개별 컨트롤러 작업이 나 전체 컨트롤러 중 하나에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-123">You can apply most action filters to either an individual controller action or an entire controller.</span></span>

<span data-ttu-id="8606b-124">목록 1의 데이터 컨트롤러 라는 동작을 노출 하는 예를 들어 `Index()` 하는 현재 시간을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-124">For example, the Data controller in Listing 1 exposes an action named `Index()` that returns the current time.</span></span> <span data-ttu-id="8606b-125">이 작업으로 데코레이팅되 어는 `OutputCache` 작업 필터.</span><span class="sxs-lookup"><span data-stu-id="8606b-125">This action is decorated with the `OutputCache` action filter.</span></span> <span data-ttu-id="8606b-126">이 필터를 사용 하면 10 초 동안 캐시 될 동작에 의해 반환 되는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-126">This filter causes the value returned by the action to be cached for 10 seconds.</span></span>

<span data-ttu-id="8606b-127">**1 – 나열 `Controllers\DataController.cs`**</span><span class="sxs-lookup"><span data-stu-id="8606b-127">**Listing 1 – `Controllers\DataController.cs`**</span></span>

[!code-csharp[Main](understanding-action-filters-cs/samples/sample1.cs)]

<span data-ttu-id="8606b-128">반복적으로 호출 하는 경우는 `Index()` 브라우저의 주소 표시줄에는 URL/데이터/인덱스를 입력 하 고 새로 고침에 도달 하 여 작업 단추를 여러 번 동시 10 초 동안 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-128">If you repeatedly invoke the `Index()` action by entering the URL /Data/Index into the address bar of your browser and hitting the Refresh button multiple times, then you will see the same time for 10 seconds.</span></span> <span data-ttu-id="8606b-129">출력은 `Index()` 작업 (그림 1 참조)는 10 초 동안 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-129">The output of the `Index()` action is cached for 10 seconds (see Figure 1).</span></span>


<span data-ttu-id="8606b-130">[![캐시 된 시간](understanding-action-filters-cs/_static/image2.png)](understanding-action-filters-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8606b-130">[![Cached time](understanding-action-filters-cs/_static/image2.png)](understanding-action-filters-cs/_static/image1.png)</span></span>

<span data-ttu-id="8606b-131">**그림 01**: 캐시 시간 ([전체 크기 이미지를 보려면 클릭](understanding-action-filters-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="8606b-131">**Figure 01**: Cached time ([Click to view full-size image](understanding-action-filters-cs/_static/image3.png))</span></span>


<span data-ttu-id="8606b-132">목록 1로 설정 하는 단일 작업 필터 –는 `OutputCache` 작업 필터 –에 적용 되는 `Index()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="8606b-132">In Listing 1, a single action filter – the `OutputCache` action filter – is applied to the `Index()` method.</span></span> <span data-ttu-id="8606b-133">필요한 경우 동일한 작업에 여러 작업 필터를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-133">If you need, you can apply multiple action filters to the same action.</span></span> <span data-ttu-id="8606b-134">예를 들어 모두를 적용 해야 할 수 있습니다는 `OutputCache` 및 `HandleError` 동일한 작업에 작업 필터.</span><span class="sxs-lookup"><span data-stu-id="8606b-134">For example, you might want to apply both the `OutputCache` and `HandleError` action filters to the same action.</span></span>

<span data-ttu-id="8606b-135">목록 1에서의 `OutputCache` 작업 필터에 적용 되는 `Index()` 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-135">In Listing 1, the `OutputCache` action filter is applied to the `Index()` action.</span></span> <span data-ttu-id="8606b-136">이 특성을 적용할 수는 `DataController` 클래스 자체입니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-136">You also could apply this attribute to the `DataController` class itself.</span></span> <span data-ttu-id="8606b-137">경우 컨트롤러에 의해 노출 되는 모든 작업에 의해 반환 되는 결과 10 초 동안 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-137">In that case, the result returned by any action exposed by the controller would be cached for 10 seconds.</span></span>

### <a name="the-different-types-of-filters"></a><span data-ttu-id="8606b-138">다양 한 유형의 필터</span><span class="sxs-lookup"><span data-stu-id="8606b-138">The Different Types of Filters</span></span>

<span data-ttu-id="8606b-139">ASP.NET MVC 프레임 워크에서는 네 가지 형식의 필터를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-139">The ASP.NET MVC framework supports four different types of filters:</span></span>

1. <span data-ttu-id="8606b-140">권한 부여 필터 – 구현 하는 `IAuthorizationFilter` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-140">Authorization filters – Implements the `IAuthorizationFilter` attribute.</span></span>
2. <span data-ttu-id="8606b-141">작업 필터 – 구현 하는 `IActionFilter` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-141">Action filters – Implements the `IActionFilter` attribute.</span></span>
3. <span data-ttu-id="8606b-142">필터 – 구현 결과 `IResultFilter` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-142">Result filters – Implements the `IResultFilter` attribute.</span></span>
4. <span data-ttu-id="8606b-143">예외 필터 – 구현 하는 `IExceptionFilter` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-143">Exception filters – Implements the `IExceptionFilter` attribute.</span></span>

<span data-ttu-id="8606b-144">필터는 위에 나열 된 순서로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-144">Filters are executed in the order listed above.</span></span> <span data-ttu-id="8606b-145">예를 들어 권한 부여 필터는 항상 작업 필터 전에 실행 되 고 예외 필터 다른 모든 유형의 필터 후 항상 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-145">For example, authorization filters are always executed before action filters and exception filters are always executed after every other type of filter.</span></span>

<span data-ttu-id="8606b-146">권한 부여 필터는 인증 및 컨트롤러 작업에 대 한 권한 부여를 구현 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-146">Authorization filters are used to implement authentication and authorization for controller actions.</span></span> <span data-ttu-id="8606b-147">예를 들어 권한 부여 필터는 권한 부여 필터의 예시입니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-147">For example, the Authorize filter is an example of an Authorization filter.</span></span>

<span data-ttu-id="8606b-148">작업 필터는 before 및 컨트롤러 작업이 실행 된 후 실행 되는 논리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-148">Action filters contain logic that is executed before and after a controller action executes.</span></span> <span data-ttu-id="8606b-149">컨트롤러 동작을 반환 하는 뷰 데이터를 수정 하려면 예를 들어, 작업 필터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-149">You can use an action filter, for instance, to modify the view data that a controller action returns.</span></span>

<span data-ttu-id="8606b-150">결과 필터 전과 뷰 결과 실행 된 후 실행 되는 논리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-150">Result filters contain logic that is executed before and after a view result is executed.</span></span> <span data-ttu-id="8606b-151">예를 들어 뷰 결과 수정 하려면 수 브라우저에 뷰를 렌더링 하기 전에 마우스 오른쪽 단추로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-151">For example, you might want to modify a view result right before the view is rendered to the browser.</span></span>

<span data-ttu-id="8606b-152">예외 필터는 마지막 유형의 필터를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-152">Exception filters are the last type of filter to run.</span></span> <span data-ttu-id="8606b-153">컨트롤러 동작 또는 컨트롤러 작업 결과 의해 발생 하는 오류를 처리 하는 예외 필터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-153">You can use an exception filter to handle errors raised by either your controller actions or controller action results.</span></span> <span data-ttu-id="8606b-154">또한 예외 필터를 사용 하 여 오류를 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-154">You also can use exception filters to log errors.</span></span>

<span data-ttu-id="8606b-155">필터의 각 유형 마다 특정 한 순서로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-155">Each different type of filter is executed in a particular order.</span></span> <span data-ttu-id="8606b-156">같은 유형의 필터가 실행 되는 순서를 제어 하려는 경우 필터의 순서 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-156">If you want to control the order in which filters of the same type are executed then you can set a filter's Order property.</span></span>

<span data-ttu-id="8606b-157">모든 작업 필터에 대 한 기본 클래스는는 `System.Web.Mvc.FilterAttribute` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-157">The base class for all action filters is the `System.Web.Mvc.FilterAttribute` class.</span></span> <span data-ttu-id="8606b-158">특정 형식의 필터를 구현 하려면 다음 기본 필터 클래스에서 상속 하 고 중 하나 이상을 구현 하는 클래스를 만들어야 하는 경우는 `IAuthorizationFilter`, `IActionFilter`, `IResultFilter`, 또는 `IExceptionFilter` 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-158">If you want to implement a particular type of filter, then you need to create a class that inherits from the base Filter class and implements one or more of the `IAuthorizationFilter`, `IActionFilter`, `IResultFilter`, or `IExceptionFilter` interfaces.</span></span>

### <a name="the-base-actionfilterattribute-class"></a><span data-ttu-id="8606b-159">기본 ActionFilterAttribute 클래스</span><span class="sxs-lookup"><span data-stu-id="8606b-159">The Base ActionFilterAttribute Class</span></span>

<span data-ttu-id="8606b-160">ASP.NET MVC 프레임 워크의 기본 포함 사용자 지정 작업 필터를 구현 하기 위한 쉽게 `ActionFilterAttribute` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-160">In order to make it easier for you to implement a custom action filter, the ASP.NET MVC framework includes a base `ActionFilterAttribute` class.</span></span> <span data-ttu-id="8606b-161">이 클래스에서 모두 구현 하는 `IActionFilter` 및 `IResultFilter` 인터페이스를 만들고에서 상속 되는 `Filter` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-161">This class implements both the `IActionFilter` and `IResultFilter` interfaces and inherits from the `Filter` class.</span></span>

<span data-ttu-id="8606b-162">여기에 용어 완전히 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-162">The terminology here is not entirely consistent.</span></span> <span data-ttu-id="8606b-163">기술적으로 ActionFilterAttribute 클래스에서 상속 되는 클래스는 작업 필터와 결과 필터.</span><span class="sxs-lookup"><span data-stu-id="8606b-163">Technically, a class that inherits from the ActionFilterAttribute class is both an action filter and a result filter.</span></span> <span data-ttu-id="8606b-164">그러나 느슨한 의미에서 단어 작업 필터는 ASP.NET MVC 프레임 워크에서 필터의 모든 형식을 참조 하도록 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-164">However, in the loose sense, the word action filter is used to refer to any type of filter in the ASP.NET MVC framework.</span></span>

<span data-ttu-id="8606b-165">기본 `ActionFilterAttribute` 클래스에는 다음과 같은 메서드를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-165">The base `ActionFilterAttribute` class has the following methods that you can override:</span></span>

- <span data-ttu-id="8606b-166">OnActionExecuting –이 메서드는 컨트롤러 작업이 실행 되기 전에 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-166">OnActionExecuting – This method is called before a controller action is executed.</span></span>
- <span data-ttu-id="8606b-167">OnActionExecuted –이 메서드는 컨트롤러 작업이 실행 된 후 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-167">OnActionExecuted – This method is called after a controller action is executed.</span></span>
- <span data-ttu-id="8606b-168">OnResultExecuting –이 메서드는 컨트롤러 작업 결과가 실행 되기 전에 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-168">OnResultExecuting – This method is called before a controller action result is executed.</span></span>
- <span data-ttu-id="8606b-169">OnResultExecuted –이 메서드는 컨트롤러 작업 결과가 실행 된 후 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-169">OnResultExecuted – This method is called after a controller action result is executed.</span></span>

<span data-ttu-id="8606b-170">다음 섹션에서 각 다른 방법을 구현 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-170">In the next section, we'll see how you can implement each of these different methods.</span></span>

### <a name="creating-a-log-action-filter"></a><span data-ttu-id="8606b-171">로그 작업 필터 만들기</span><span class="sxs-lookup"><span data-stu-id="8606b-171">Creating a Log Action Filter</span></span>

<span data-ttu-id="8606b-172">를 사용자 지정 작업 필터를 구축 하는 방법을 보여 주기 위해 Visual Studio 출력 창에는 컨트롤러 동작을 처리 하는 단계를 기록 하는 사용자 지정 작업 필터를 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-172">In order to illustrate how you can build a custom action filter, we'll create a custom action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span> <span data-ttu-id="8606b-173">우리의 `LogActionFilter` 목록 2에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-173">Our `LogActionFilter` is contained in Listing 2.</span></span>

<span data-ttu-id="8606b-174">**2 – 나열 `ActionFilters\LogActionFilter.cs`**</span><span class="sxs-lookup"><span data-stu-id="8606b-174">**Listing 2 – `ActionFilters\LogActionFilter.cs`**</span></span>

[!code-csharp[Main](understanding-action-filters-cs/samples/sample2.cs)]

<span data-ttu-id="8606b-175">목록 2에는 `OnActionExecuting()`, `OnActionExecuted()`, `OnResultExecuting()`, 및 `OnResultExecuted()` 모든 메서드는 호출는 `Log()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="8606b-175">In Listing 2, the `OnActionExecuting()`, `OnActionExecuted()`, `OnResultExecuting()`, and `OnResultExecuted()` methods all call the `Log()` method.</span></span> <span data-ttu-id="8606b-176">메서드 및 현재 경로 데이터의 이름에 전달 되는 `Log()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="8606b-176">The name of the method and the current route data is passed to the `Log()` method.</span></span> <span data-ttu-id="8606b-177">`Log()` 메서드는 Visual Studio 출력 창에 메시지를 씁니다 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="8606b-177">The `Log()` method writes a message to the Visual Studio Output window (see Figure 2).</span></span>


<span data-ttu-id="8606b-178">[![Visual Studio 출력 창에 쓰기](understanding-action-filters-cs/_static/image5.png)](understanding-action-filters-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="8606b-178">[![Writing to the Visual Studio Output window](understanding-action-filters-cs/_static/image5.png)](understanding-action-filters-cs/_static/image4.png)</span></span>

<span data-ttu-id="8606b-179">**그림 02**: Visual Studio 출력 창에 쓰기 ([전체 크기 이미지를 보려면 클릭](understanding-action-filters-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="8606b-179">**Figure 02**: Writing to the Visual Studio Output window ([Click to view full-size image](understanding-action-filters-cs/_static/image6.png))</span></span>


<span data-ttu-id="8606b-180">보기 3의 Home 컨트롤러를 전체 컨트롤러 클래스에는 로그 작업 필터를 적용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-180">The Home controller in Listing 3 illustrates how you can apply the Log action filter to an entire controller class.</span></span> <span data-ttu-id="8606b-181">때마다 Home 컨트롤러에 의해 노출 되는 작업 중에 호출 되 – 하거나는 `Index()` 메서드 또는 `About()` 메서드-단계 처리 작업은 Visual Studio 출력 창에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-181">Whenever any of the actions exposed by the Home controller are invoked – either the `Index()` method or the `About()` method – the stages of processing the action are logged to the Visual Studio Output window.</span></span>

<span data-ttu-id="8606b-182">**3 – 나열 `Controllers\HomeController.cs`**</span><span class="sxs-lookup"><span data-stu-id="8606b-182">**Listing 3 – `Controllers\HomeController.cs`**</span></span>

[!code-csharp[Main](understanding-action-filters-cs/samples/sample3.cs)]

### <a name="summary"></a><span data-ttu-id="8606b-183">요약</span><span class="sxs-lookup"><span data-stu-id="8606b-183">Summary</span></span>

<span data-ttu-id="8606b-184">이 자습서에서는 ASP.NET MVC 동작 필터를 도입 합니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-184">In this tutorial, you were introduced to ASP.NET MVC action filters.</span></span> <span data-ttu-id="8606b-185">네 가지 형식의 필터에 배웠습니다: 권한 부여 필터, 작업 필터, 결과 필터 및 예외 필터.</span><span class="sxs-lookup"><span data-stu-id="8606b-185">You learned about the four different types of filters: authorization filters, action filters, result filters, and exception filters.</span></span> <span data-ttu-id="8606b-186">또한 기본에 대 한 배웠습니다 `ActionFilterAttribute` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-186">You also learned about the base `ActionFilterAttribute` class.</span></span>

<span data-ttu-id="8606b-187">마지막으로, 간단한 작업 필터를 구현 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-187">Finally, you learned how to implement a simple action filter.</span></span> <span data-ttu-id="8606b-188">Visual Studio 출력 창에는 컨트롤러 동작을 처리 하는 단계를 기록 하는 로그 작업 필터를 만들었는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="8606b-188">We created a Log action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8606b-189">[이전](asp-net-mvc-routing-overview-cs.md)
> [다음](improving-performance-with-output-caching-cs.md)</span><span class="sxs-lookup"><span data-stu-id="8606b-189">[Previous](asp-net-mvc-routing-overview-cs.md)
[Next](improving-performance-with-output-caching-cs.md)</span></span>
