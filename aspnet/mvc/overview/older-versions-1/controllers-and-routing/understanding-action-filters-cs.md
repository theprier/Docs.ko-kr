---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
title: 작업 필터 (C#) 이해 | Microsoft Docs
author: microsoft
description: 이 자습서의 목표는 작업 필터를 설명 합니다. 작업 필터는 컨트롤러 작업의 경우-또는 전체 컨트롤러에 적용할 수 있는 특성...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: a94e4e81-40c1-47b7-8613-126a1a6cc93d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
msc.type: authoredcontent
ms.openlocfilehash: 6c7706d8252d5a0271f1b9243fa8eb282f722654
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831878"
---
<a name="understanding-action-filters-c"></a><span data-ttu-id="e62b7-104">작업 필터 (C#) 이해</span><span class="sxs-lookup"><span data-stu-id="e62b7-104">Understanding Action Filters (C#)</span></span>
====================
<span data-ttu-id="e62b7-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="e62b7-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="e62b7-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="e62b7-106">Download PDF</span></span>](http://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_CS.pdf)

> <span data-ttu-id="e62b7-107">이 자습서의 목표는 작업 필터를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-107">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="e62b7-108">작업 필터는 컨트롤러 동작-또는 작업 실행 되는 방식을 수정 하는 전체 controller--에 적용할 수 있는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-108">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span>


## <a name="understanding-action-filters"></a><span data-ttu-id="e62b7-109">작업 필터 이해</span><span class="sxs-lookup"><span data-stu-id="e62b7-109">Understanding Action Filters</span></span>

<span data-ttu-id="e62b7-110">이 자습서의 목표는 작업 필터를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-110">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="e62b7-111">작업 필터는 컨트롤러 동작-또는 작업 실행 되는 방식을 수정 하는 전체 controller--에 적용할 수 있는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-111">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span> <span data-ttu-id="e62b7-112">ASP.NET MVC 프레임 워크에 몇 가지 작업 필터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-112">The ASP.NET MVC framework includes several action filters:</span></span>

- <span data-ttu-id="e62b7-113">OutputCache –이 작업 필터는 지정 된 기간에 대 한 컨트롤러 작업의 출력을 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-113">OutputCache – This action filter caches the output of a controller action for a specified amount of time.</span></span>
- <span data-ttu-id="e62b7-114">HandleError –이 작업 필터는 컨트롤러 작업을 실행 하는 경우 발생 하는 오류를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-114">HandleError – This action filter handles errors raised when a controller action executes.</span></span>
- <span data-ttu-id="e62b7-115">권한 부여-이 작업 필터를 사용 하면 특정 사용자 또는 역할에 대 한 액세스를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-115">Authorize – This action filter enables you to restrict access to a particular user or role.</span></span>

<span data-ttu-id="e62b7-116">사용자 고유의 사용자 지정 작업 필터를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-116">You also can create your own custom action filters.</span></span> <span data-ttu-id="e62b7-117">예를 들어 다음 사용자 지정 인증 시스템을 구현 하기 위해 사용자 지정 작업 필터를 만들려면는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-117">For example, you might want to create a custom action filter in order to implement a custom authentication system.</span></span> <span data-ttu-id="e62b7-118">또는 컨트롤러 작업에 의해 반환 되는 뷰 데이터를 수정 하는 작업 필터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-118">Or, you might want to create an action filter that modifies the view data returned by a controller action.</span></span>

<span data-ttu-id="e62b7-119">이 자습서에서는 처음부터 작업 필터를 작성 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-119">In this tutorial, you learn how to build an action filter from the ground up.</span></span> <span data-ttu-id="e62b7-120">Visual Studio 출력 창에 여러 작업을 처리 하는 단계를 기록 하는 로그 작업 필터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-120">We create a Log action filter that logs different stages of the processing of an action to the Visual Studio Output window.</span></span>

### <a name="using-an-action-filter"></a><span data-ttu-id="e62b7-121">작업 필터를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e62b7-121">Using an Action Filter</span></span>

<span data-ttu-id="e62b7-122">작업 필터 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-122">An action filter is an attribute.</span></span> <span data-ttu-id="e62b7-123">대부분의 작업 필터는 개별 컨트롤러 작업 또는 전체 컨트롤러를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-123">You can apply most action filters to either an individual controller action or an entire controller.</span></span>

<span data-ttu-id="e62b7-124">목록 1의 데이터 컨트롤러 라는 작업을 노출 하는 예를 들어 `Index()` 는 현재 시간을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-124">For example, the Data controller in Listing 1 exposes an action named `Index()` that returns the current time.</span></span> <span data-ttu-id="e62b7-125">이 작업은 데코 레이트 된 `OutputCache` 작업 필터.</span><span class="sxs-lookup"><span data-stu-id="e62b7-125">This action is decorated with the `OutputCache` action filter.</span></span> <span data-ttu-id="e62b7-126">이 필터를 사용 하면 10 초 동안 캐시 되도록 하려면 작업에 의해 반환 되는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-126">This filter causes the value returned by the action to be cached for 10 seconds.</span></span>

<span data-ttu-id="e62b7-127">**목록 1 – `Controllers\DataController.cs`**</span><span class="sxs-lookup"><span data-stu-id="e62b7-127">**Listing 1 – `Controllers\DataController.cs`**</span></span>

[!code-csharp[Main](understanding-action-filters-cs/samples/sample1.cs)]

<span data-ttu-id="e62b7-128">반복적으로 호출 하는 경우는 `Index()` 브라우저의 주소 표시줄에 입력 된 URL 데이터/인덱스 새로 고침에 도달 하는 작업 단추를 여러 번 10 초 동안 동일한 시간을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-128">If you repeatedly invoke the `Index()` action by entering the URL /Data/Index into the address bar of your browser and hitting the Refresh button multiple times, then you will see the same time for 10 seconds.</span></span> <span data-ttu-id="e62b7-129">출력을 `Index()` 작업 (그림 1 참조)는 10 초 동안 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-129">The output of the `Index()` action is cached for 10 seconds (see Figure 1).</span></span>


<span data-ttu-id="e62b7-130">[![캐시 된 시간](understanding-action-filters-cs/_static/image2.png)](understanding-action-filters-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e62b7-130">[![Cached time](understanding-action-filters-cs/_static/image2.png)](understanding-action-filters-cs/_static/image1.png)</span></span>

<span data-ttu-id="e62b7-131">**그림 01**: 캐시 시간 ([큰 이미지를 보려면 클릭](understanding-action-filters-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="e62b7-131">**Figure 01**: Cached time ([Click to view full-size image](understanding-action-filters-cs/_static/image3.png))</span></span>


<span data-ttu-id="e62b7-132">목록 1로 설정 하는 단일 작업 필터 – 합니다 `OutputCache` – 작업 필터에 적용 되는 `Index()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="e62b7-132">In Listing 1, a single action filter – the `OutputCache` action filter – is applied to the `Index()` method.</span></span> <span data-ttu-id="e62b7-133">필요한 경우에 동일한 작업에 여러 작업 필터를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-133">If you need, you can apply multiple action filters to the same action.</span></span> <span data-ttu-id="e62b7-134">둘 다 적용 하려는 하는 예를 들어 합니다 `OutputCache` 및 `HandleError` 동일한 작업에 작업 필터.</span><span class="sxs-lookup"><span data-stu-id="e62b7-134">For example, you might want to apply both the `OutputCache` and `HandleError` action filters to the same action.</span></span>

<span data-ttu-id="e62b7-135">목록 1에서 합니다 `OutputCache` 작업 필터에 적용 되는 `Index()` 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-135">In Listing 1, the `OutputCache` action filter is applied to the `Index()` action.</span></span> <span data-ttu-id="e62b7-136">이 특성을 적용할 수는 `DataController` 클래스 자체입니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-136">You also could apply this attribute to the `DataController` class itself.</span></span> <span data-ttu-id="e62b7-137">이런 경우 10 초 동안 컨트롤러에 의해 노출 된 모든 작업에서 반환 된 결과 캐시할 수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-137">In that case, the result returned by any action exposed by the controller would be cached for 10 seconds.</span></span>

### <a name="the-different-types-of-filters"></a><span data-ttu-id="e62b7-138">다양 한 유형의 필터</span><span class="sxs-lookup"><span data-stu-id="e62b7-138">The Different Types of Filters</span></span>

<span data-ttu-id="e62b7-139">ASP.NET MVC 프레임 워크는 네 가지 유형의 필터를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-139">The ASP.NET MVC framework supports four different types of filters:</span></span>

1. <span data-ttu-id="e62b7-140">권한 부여 필터 – 구현 된 `IAuthorizationFilter` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-140">Authorization filters – Implements the `IAuthorizationFilter` attribute.</span></span>
2. <span data-ttu-id="e62b7-141">작업 필터 – 구현 된 `IActionFilter` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-141">Action filters – Implements the `IActionFilter` attribute.</span></span>
3. <span data-ttu-id="e62b7-142">결과 필터 – 구현 된 `IResultFilter` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-142">Result filters – Implements the `IResultFilter` attribute.</span></span>
4. <span data-ttu-id="e62b7-143">예외 필터 – 구현 된 `IExceptionFilter` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-143">Exception filters – Implements the `IExceptionFilter` attribute.</span></span>

<span data-ttu-id="e62b7-144">필터는 위에 나열 된 순서로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-144">Filters are executed in the order listed above.</span></span> <span data-ttu-id="e62b7-145">예를 들어, 권한 부여 필터는 항상 작업 필터 보다 먼저 실행 및 예외 필터는 필터의 다른 모든 형식 후 항상 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-145">For example, authorization filters are always executed before action filters and exception filters are always executed after every other type of filter.</span></span>

<span data-ttu-id="e62b7-146">권한 부여 필터는 인증 및 컨트롤러 작업에 대 한 권한 부여를 구현 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-146">Authorization filters are used to implement authentication and authorization for controller actions.</span></span> <span data-ttu-id="e62b7-147">예를 들어, 권한 부여 필터는 권한 부여 필터의 예제.</span><span class="sxs-lookup"><span data-stu-id="e62b7-147">For example, the Authorize filter is an example of an Authorization filter.</span></span>

<span data-ttu-id="e62b7-148">작업 필터는 전과 컨트롤러 작업을 실행 한 후 실행 되는 논리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-148">Action filters contain logic that is executed before and after a controller action executes.</span></span> <span data-ttu-id="e62b7-149">예를 들어에 컨트롤러 작업을 반환 하는 뷰 데이터를 수정 하려면 작업 필터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-149">You can use an action filter, for instance, to modify the view data that a controller action returns.</span></span>

<span data-ttu-id="e62b7-150">결과 필터는 뷰 결과 실행 된 후 및 하기 전에 실행 되는 논리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-150">Result filters contain logic that is executed before and after a view result is executed.</span></span> <span data-ttu-id="e62b7-151">보기 결과 수정 하려는 하는 예를 들어 뷰는 브라우저에 렌더링 되기 전에 마우스 오른쪽 단추로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-151">For example, you might want to modify a view result right before the view is rendered to the browser.</span></span>

<span data-ttu-id="e62b7-152">예외 필터는 마지막 형식의 필터를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-152">Exception filters are the last type of filter to run.</span></span> <span data-ttu-id="e62b7-153">컨트롤러 작업 또는 컨트롤러 작업 결과 의해 발생 하는 오류를 처리 하는 예외 필터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-153">You can use an exception filter to handle errors raised by either your controller actions or controller action results.</span></span> <span data-ttu-id="e62b7-154">오류를 기록할 예외 필터를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-154">You also can use exception filters to log errors.</span></span>

<span data-ttu-id="e62b7-155">각 다양 한 유형의 필터는 특정 순서로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-155">Each different type of filter is executed in a particular order.</span></span> <span data-ttu-id="e62b7-156">동일한 형식의 필터가 실행 되는 순서를 제어 하려는 경우 필터의 순서 속성을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-156">If you want to control the order in which filters of the same type are executed then you can set a filter's Order property.</span></span>

<span data-ttu-id="e62b7-157">모든 작업 필터에 대 한 기본 클래스를 `System.Web.Mvc.FilterAttribute` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-157">The base class for all action filters is the `System.Web.Mvc.FilterAttribute` class.</span></span> <span data-ttu-id="e62b7-158">특정 형식의 필터를 구현 하려는 경우 기본 필터 클래스에서 상속 하 고 하나 이상의 구현 하는 클래스를 만들어야 합니다 `IAuthorizationFilter`, `IActionFilter`를 `IResultFilter`, 또는 `IExceptionFilter` 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-158">If you want to implement a particular type of filter, then you need to create a class that inherits from the base Filter class and implements one or more of the `IAuthorizationFilter`, `IActionFilter`, `IResultFilter`, or `IExceptionFilter` interfaces.</span></span>

### <a name="the-base-actionfilterattribute-class"></a><span data-ttu-id="e62b7-159">기본 ActionFilterAttribute 클래스</span><span class="sxs-lookup"><span data-stu-id="e62b7-159">The Base ActionFilterAttribute Class</span></span>

<span data-ttu-id="e62b7-160">사용자 지정 작업 필터를 구현 하려면 하기 쉽게 하기 위해 ASP.NET MVC 프레임 워크는 기본 `ActionFilterAttribute` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-160">In order to make it easier for you to implement a custom action filter, the ASP.NET MVC framework includes a base `ActionFilterAttribute` class.</span></span> <span data-ttu-id="e62b7-161">이 클래스는 둘 다 구현 합니다 `IActionFilter` 및 `IResultFilter` 인터페이스에서 상속 되 고는 `Filter` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-161">This class implements both the `IActionFilter` and `IResultFilter` interfaces and inherits from the `Filter` class.</span></span>

<span data-ttu-id="e62b7-162">이 용어를 완전히 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-162">The terminology here is not entirely consistent.</span></span> <span data-ttu-id="e62b7-163">기술적으로 ActionFilterAttribute 클래스에서 상속 된 클래스는 작업 필터 및 결과 필터.</span><span class="sxs-lookup"><span data-stu-id="e62b7-163">Technically, a class that inherits from the ActionFilterAttribute class is both an action filter and a result filter.</span></span> <span data-ttu-id="e62b7-164">그러나 느슨한 점에서 word 작업 필터는 ASP.NET MVC 프레임 워크에서 필터의 모든 형식을 참조 하도록 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-164">However, in the loose sense, the word action filter is used to refer to any type of filter in the ASP.NET MVC framework.</span></span>

<span data-ttu-id="e62b7-165">기본 `ActionFilterAttribute` 클래스에 메서드를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-165">The base `ActionFilterAttribute` class has the following methods that you can override:</span></span>

- <span data-ttu-id="e62b7-166">OnActionExecuting –이 메서드는 컨트롤러 작업을 실행 하기 전에 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-166">OnActionExecuting – This method is called before a controller action is executed.</span></span>
- <span data-ttu-id="e62b7-167">OnActionExecuted –이 메서드는 컨트롤러 작업이 실행 된 후 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-167">OnActionExecuted – This method is called after a controller action is executed.</span></span>
- <span data-ttu-id="e62b7-168">OnResultExecuting –이 메서드는 컨트롤러 작업 결과가 실행 되기 전에 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-168">OnResultExecuting – This method is called before a controller action result is executed.</span></span>
- <span data-ttu-id="e62b7-169">OnResultExecuted –이 메서드는 컨트롤러 작업 결과가 실행 된 후 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-169">OnResultExecuted – This method is called after a controller action result is executed.</span></span>

<span data-ttu-id="e62b7-170">다음 섹션에서는 각 이러한 다른 메서드를 구현 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-170">In the next section, we'll see how you can implement each of these different methods.</span></span>

### <a name="creating-a-log-action-filter"></a><span data-ttu-id="e62b7-171">로그 작업 필터 만들기</span><span class="sxs-lookup"><span data-stu-id="e62b7-171">Creating a Log Action Filter</span></span>

<span data-ttu-id="e62b7-172">사용자 지정 작업 필터를 구축 하는 방법을 보여 주기를 위해 Visual Studio 출력 창에는 컨트롤러 작업을 처리 하는 단계를 기록 하는 사용자 지정 작업 필터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-172">In order to illustrate how you can build a custom action filter, we'll create a custom action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span> <span data-ttu-id="e62b7-173">우리의 `LogActionFilter` 목록 2에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-173">Our `LogActionFilter` is contained in Listing 2.</span></span>

<span data-ttu-id="e62b7-174">**2 – 나열 `ActionFilters\LogActionFilter.cs`**</span><span class="sxs-lookup"><span data-stu-id="e62b7-174">**Listing 2 – `ActionFilters\LogActionFilter.cs`**</span></span>

[!code-csharp[Main](understanding-action-filters-cs/samples/sample2.cs)]

<span data-ttu-id="e62b7-175">목록 2에서 합니다 `OnActionExecuting()`, `OnActionExecuted()`, `OnResultExecuting()`, 및 `OnResultExecuted()` 모든 메서드를 호출 합니다 `Log()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="e62b7-175">In Listing 2, the `OnActionExecuting()`, `OnActionExecuted()`, `OnResultExecuting()`, and `OnResultExecuted()` methods all call the `Log()` method.</span></span> <span data-ttu-id="e62b7-176">메서드 및 현재 경로 데이터의 이름을 전달 됩니다는 `Log()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="e62b7-176">The name of the method and the current route data is passed to the `Log()` method.</span></span> <span data-ttu-id="e62b7-177">`Log()` 메서드는 Visual Studio 출력 창에 메시지를 씁니다 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="e62b7-177">The `Log()` method writes a message to the Visual Studio Output window (see Figure 2).</span></span>


<span data-ttu-id="e62b7-178">[![Visual Studio 출력 창에 쓰기](understanding-action-filters-cs/_static/image5.png)](understanding-action-filters-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="e62b7-178">[![Writing to the Visual Studio Output window](understanding-action-filters-cs/_static/image5.png)](understanding-action-filters-cs/_static/image4.png)</span></span>

<span data-ttu-id="e62b7-179">**그림 02**: Visual Studio 출력 창에 작성 ([큰 이미지를 보려면 클릭](understanding-action-filters-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="e62b7-179">**Figure 02**: Writing to the Visual Studio Output window ([Click to view full-size image](understanding-action-filters-cs/_static/image6.png))</span></span>


<span data-ttu-id="e62b7-180">보기 3의 Home 컨트롤러 전체 컨트롤러 클래스에 로그 작업 필터를 적용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-180">The Home controller in Listing 3 illustrates how you can apply the Log action filter to an entire controller class.</span></span> <span data-ttu-id="e62b7-181">호출 될 때마다 홈 컨트롤러에서 노출 하는 동작 중 하나는 – 하거나 합니다 `Index()` 메서드 또는 `About()` 메서드-단계의 처리 작업을 Visual Studio 출력 창에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-181">Whenever any of the actions exposed by the Home controller are invoked – either the `Index()` method or the `About()` method – the stages of processing the action are logged to the Visual Studio Output window.</span></span>

<span data-ttu-id="e62b7-182">**3 – 나열 `Controllers\HomeController.cs`**</span><span class="sxs-lookup"><span data-stu-id="e62b7-182">**Listing 3 – `Controllers\HomeController.cs`**</span></span>

[!code-csharp[Main](understanding-action-filters-cs/samples/sample3.cs)]

### <a name="summary"></a><span data-ttu-id="e62b7-183">요약</span><span class="sxs-lookup"><span data-stu-id="e62b7-183">Summary</span></span>

<span data-ttu-id="e62b7-184">이 자습서에서는 ASP.NET MVC 작업 필터를 소개 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-184">In this tutorial, you were introduced to ASP.NET MVC action filters.</span></span> <span data-ttu-id="e62b7-185">네 가지 유형의 필터에 대해 알아보았습니다: 권한 부여 필터, 작업 필터, 결과 필터 및 예외 필터.</span><span class="sxs-lookup"><span data-stu-id="e62b7-185">You learned about the four different types of filters: authorization filters, action filters, result filters, and exception filters.</span></span> <span data-ttu-id="e62b7-186">또한 기본에 대해 알아보았습니다 `ActionFilterAttribute` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-186">You also learned about the base `ActionFilterAttribute` class.</span></span>

<span data-ttu-id="e62b7-187">마지막으로, 간단한 작업 필터를 구현 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-187">Finally, you learned how to implement a simple action filter.</span></span> <span data-ttu-id="e62b7-188">Visual Studio 출력 창에는 컨트롤러 작업을 처리 하는 단계를 기록 하는 로그 작업 필터를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="e62b7-188">We created a Log action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e62b7-189">[이전](asp-net-mvc-routing-overview-cs.md)
> [다음](improving-performance-with-output-caching-cs.md)</span><span class="sxs-lookup"><span data-stu-id="e62b7-189">[Previous](asp-net-mvc-routing-overview-cs.md)
[Next](improving-performance-with-output-caching-cs.md)</span></span>
