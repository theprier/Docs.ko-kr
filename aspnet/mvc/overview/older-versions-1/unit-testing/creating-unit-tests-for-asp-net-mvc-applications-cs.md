---
uid: mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
title: "ASP.NET MVC 응용 프로그램 (C#)에 대 한 단위 테스트 만들기 | Microsoft Docs"
author: StephenWalther
description: "컨트롤러 작업에 대 한 단위 테스트를 만드는 방법에 알아봅니다. 이 자습서에서는 Stephen Walther 컨트롤러 작업에는 parti 반환 하는지 여부를 테스트 하는 방법을 보여 줍니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/19/2008
ms.topic: article
ms.assetid: d3a270b9-d7b1-47f2-8775-fc3beb518b5c
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
msc.type: authoredcontent
ms.openlocfilehash: 56c981363f1905c1c9869dbaf2adb6b5ac1c28a5
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="creating-unit-tests-for-aspnet-mvc-applications-c"></a><span data-ttu-id="a74df-104">ASP.NET MVC 응용 프로그램 (C#)에 대 한 단위 테스트 만들기</span><span class="sxs-lookup"><span data-stu-id="a74df-104">Creating Unit Tests for ASP.NET MVC Applications (C#)</span></span>
====================
<span data-ttu-id="a74df-105">으로 [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="a74df-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

[<span data-ttu-id="a74df-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="a74df-106">Download PDF</span></span>](http://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_07_CS.pdf)

> <span data-ttu-id="a74df-107">컨트롤러 작업에 대 한 단위 테스트를 만드는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-107">Learn how to create unit tests for controller actions.</span></span> <span data-ttu-id="a74df-108">이 자습서에서는 Stephen Walther 테스트 컨트롤러 작업이 특정 보기 반환, 데이터의 특정 집합을 반환 또는 다른 유형의 작업 결과 반환 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-108">In this tutorial, Stephen Walther demonstrates how to test whether a controller action returns a particular view, returns a particular set of data, or returns a different type of action result.</span></span>


<span data-ttu-id="a74df-109">이 자습서의 목표 작성 하는 방법을 단위 테스트는 컨트롤러에 대 한 ASP.NET mvc에서 응용 프로그램을 보여 주기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-109">The goal of this tutorial is to demonstrate how you can write unit tests for the controllers in your ASP.NET MVC applications.</span></span> <span data-ttu-id="a74df-110">세 가지 유형의 단위 테스트를 작성 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-110">We discuss how to build three different types of unit tests.</span></span> <span data-ttu-id="a74df-111">컨트롤러 작업에서 반환 된 보기를 테스트 하는 방법, 컨트롤러 작업에 의해 반환 되는 뷰 데이터를 테스트 하는 방법 및 하나의 컨트롤러 작업 리디렉션합니다 두 번째 컨트롤러 작업에 있는지 여부를 테스트 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-111">You learn how to test the view returned by a controller action, how to test the View Data returned by a controller action, and how to test whether or not one controller action redirects you to a second controller action.</span></span>

## <a name="creating-the-controller-under-test"></a><span data-ttu-id="a74df-112">테스트 대상 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="a74df-112">Creating the Controller under Test</span></span>

<span data-ttu-id="a74df-113">테스트 하 여 사용 하는 컨트롤러를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-113">Let's start by creating the controller that we intend to test.</span></span> <span data-ttu-id="a74df-114">명명 된 컨트롤러는 `ProductController`, 목록 1에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-114">The controller, named the `ProductController`, is contained in Listing 1.</span></span>

<span data-ttu-id="a74df-115">**1 – 나열`ProductController.cs`**</span><span class="sxs-lookup"><span data-stu-id="a74df-115">**Listing 1 – `ProductController.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample1.cs)]

<span data-ttu-id="a74df-116">`ProductController` 라는 두 개의 작업 메서드가 포함 되어 `Index()` 및 `Details()`합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-116">The `ProductController` contains two action methods named `Index()` and `Details()`.</span></span> <span data-ttu-id="a74df-117">두 동작 메서드는 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-117">Both action methods return a view.</span></span> <span data-ttu-id="a74df-118">에 `Details()` 작업 id입니다. 명명 된 매개 변수를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-118">Notice that the `Details()` action accepts a parameter named Id.</span></span>

## <a name="testing-the-view-returned-by-a-controller"></a><span data-ttu-id="a74df-119">컨트롤러에 의해 반환 된 뷰를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-119">Testing the View returned by a Controller</span></span>

<span data-ttu-id="a74df-120">테스트 한다고 가정해 보세요. 여부는 `ProductController` 오른쪽 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-120">Imagine that we want to test whether or not the `ProductController` returns the right view.</span></span> <span data-ttu-id="a74df-121">있는지 확인 하고자 때는 `ProductController.Details()` 동작이 호출 자세히 보기 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-121">We want to make sure that when the `ProductController.Details()` action is invoked, the Details view is returned.</span></span> <span data-ttu-id="a74df-122">테스트에서 반환 된 보기에 대 한 단위 테스트를 포함 하는 목록 2에서 테스트 클래스는 `ProductController.Details()` 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-122">The test class in Listing 2 contains a unit test for testing the view returned by the `ProductController.Details()` action.</span></span>

<span data-ttu-id="a74df-123">**2 – 나열`ProductControllerTest.cs`**</span><span class="sxs-lookup"><span data-stu-id="a74df-123">**Listing 2 – `ProductControllerTest.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample2.cs)]

<span data-ttu-id="a74df-124">목록 2의 클래스는 라는 테스트 메서드를 포함 `TestDetailsView()`합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-124">The class in Listing 2 includes a test method named `TestDetailsView()`.</span></span> <span data-ttu-id="a74df-125">이 메서드는 코드의 세 줄을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-125">This method contains three lines of code.</span></span> <span data-ttu-id="a74df-126">코드의 첫 번째 줄의 새 인스턴스를 만듭니다.는 `ProductController` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-126">The first line of code creates a new instance of the `ProductController` class.</span></span> <span data-ttu-id="a74df-127">코드의 두 번째 줄에는 컨트롤러의 호출 `Details()` 동작 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-127">The second line of code invokes the controller's `Details()` action method.</span></span> <span data-ttu-id="a74df-128">마지막으로, 마지막 줄의 코드 검사 보기에서 반환 되는 여부는 `Details()` 작업에도 자세히 보기.</span><span class="sxs-lookup"><span data-stu-id="a74df-128">Finally, the last line of code checks whether or not the view returned by the `Details()` action is the Details view.</span></span>

<span data-ttu-id="a74df-129">`ViewResult.ViewName` 속성은 컨트롤러에 의해 반환 된 보기의 이름을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-129">The `ViewResult.ViewName` property represents the name of the view returned by a controller.</span></span> <span data-ttu-id="a74df-130">이 속성을 테스트 하는 방법에 대 한 하나의 큰 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-130">One big warning about testing this property.</span></span> <span data-ttu-id="a74df-131">두 가지 방법으로 컨트롤러 보기를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-131">There are two ways that a controller can return a view.</span></span> <span data-ttu-id="a74df-132">컨트롤러는 다음과 같은 보기를 반환할 명시적으로 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-132">A controller can explicitly return a view like this:</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample3.cs)]

<span data-ttu-id="a74df-133">또는 보기 이름은 다음과 같이 컨트롤러 동작의 이름에서 유추할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-133">Alternatively, the name of the view can be inferred from the name of the controller action like this:</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample4.cs)]

<span data-ttu-id="a74df-134">이 컨트롤러 작업에도 라는 이름의 뷰가 반환 `Details`합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-134">This controller action also returns a view named `Details`.</span></span> <span data-ttu-id="a74df-135">그러나 뷰의 이름은 작업 이름에서 유추 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-135">However, the name of the view is inferred from the action name.</span></span> <span data-ttu-id="a74df-136">뷰 이름을 테스트 하려는 경우 다음 명시적으로 반환 해야 뷰 이름을 컨트롤러 동작에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-136">If you want to test the view name, then you must explicitly return the view name from the controller action.</span></span>

<span data-ttu-id="a74df-137">키보드 조합을 입력 하거나 목록 2에서 단위 테스트를 실행할 수 있습니다 **Ctrl-R, A** 클릭 하 여는 **솔루션의 모든 테스트 실행** 단추 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="a74df-137">You can run the unit test in Listing 2 by either entering the keyboard combination **Ctrl-R, A** or by clicking the **Run All Tests in Solution** button (see Figure 1).</span></span> <span data-ttu-id="a74df-138">테스트에 통과 하는 경우에 그림 2에는 테스트 결과 창을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-138">If the test passes, you'll see the Test Results window in Figure 2.</span></span>


<span data-ttu-id="a74df-139">[![솔루션의 모든 테스트 실행](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a74df-139">[![Run All Tests in Solution](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image1.png)</span></span>

<span data-ttu-id="a74df-140">**그림 01**: 솔루션의 모든 테스트 실행 ([전체 크기 이미지를 보려면 클릭](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="a74df-140">**Figure 01**: Run All Tests in Solution ([Click to view full-size image](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image3.png))</span></span>


<span data-ttu-id="a74df-141">[![성공 했습니다!](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="a74df-141">[![Success!](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image4.png)</span></span>

<span data-ttu-id="a74df-142">**그림 02**: 성공!</span><span class="sxs-lookup"><span data-stu-id="a74df-142">**Figure 02**: Success!</span></span> <span data-ttu-id="a74df-143">([전체 크기 이미지를 보려면 클릭](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="a74df-143">([Click to view full-size image](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image6.png))</span></span>


## <a name="testing-the-view-data-returned-by-a-controller"></a><span data-ttu-id="a74df-144">컨트롤러에 의해 반환 된 데이터 보기를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-144">Testing the View Data returned by a Controller</span></span>

<span data-ttu-id="a74df-145">MVC 컨트롤러 라는 것을 사용 하 여 데이터 뷰를 전달  *`View Data`* 합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-145">An MVC controller passes data to a view by using something called *`View Data`*.</span></span> <span data-ttu-id="a74df-146">예를 들어, 호출할 때 특정 제품에 대 한 정보를 표시 하 고 가정은 `ProductController Details()` 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-146">For example, imagine that you want to display the details for a particular product when you invoke the `ProductController Details()` action.</span></span> <span data-ttu-id="a74df-147">인스턴스를 만들 수는 경우에 `Product` (모델에 정의 됨) 하는 클래스 인스턴스를 전달 하 고는 `Details` 뷰를 이용 하 여 `View Data`합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-147">In that case, you can create an instance of a `Product` class (defined in your model) and pass the instance to the `Details` view by taking advantage of `View Data`.</span></span>

<span data-ttu-id="a74df-148">수정 된 `ProductController` 보기 3의 업데이트 된 포함 `Details()` 제품을 반환 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-148">The modified `ProductController` in Listing 3 includes an updated `Details()` action that returns a Product.</span></span>

<span data-ttu-id="a74df-149">**3 – 나열`ProductController.cs`**</span><span class="sxs-lookup"><span data-stu-id="a74df-149">**Listing 3 – `ProductController.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample5.cs)]

<span data-ttu-id="a74df-150">첫째는 `Details()` 동작의 새 인스턴스를 만듭니다.는 `Product` 랩톱 컴퓨터를 나타내는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-150">First, the `Details()` action creates a new instance of the `Product` class that represents a laptop computer.</span></span> <span data-ttu-id="a74df-151">다음으로의 인스턴스는 `Product` 클래스에 대 한 두 번째 매개 변수로 전달 되는 `View()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="a74df-151">Next, the instance of the `Product` class is passed as the second parameter to the `View()` method.</span></span>

<span data-ttu-id="a74df-152">단위 테스트를 작성할 수 필요한 데이터가 있는지 여부를 테스트 보기에 데이터가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-152">You can write unit tests to test whether the expected data is contained in view data.</span></span> <span data-ttu-id="a74df-153">테스트 목록 4에서에서 단위 테스트에 노트북 컴퓨터를 나타내는 제품 호출할 때 반환 되는 여부는 `ProductController Details()` 동작 메서드.</span><span class="sxs-lookup"><span data-stu-id="a74df-153">The unit test in Listing 4 tests whether or not a Product representing a laptop computer is returned when you call the `ProductController Details()` action method.</span></span>

<span data-ttu-id="a74df-154">**4 – 나열`ProductControllerTest.cs`**</span><span class="sxs-lookup"><span data-stu-id="a74df-154">**Listing 4 – `ProductControllerTest.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample6.cs)]

<span data-ttu-id="a74df-155">목록 4에는 `TestDetailsView()` 메서드 호출에서 반환 된 데이터 보기 테스트는 `Details()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="a74df-155">In Listing 4, the `TestDetailsView()` method tests the View Data returned by invoking the `Details()` method.</span></span> <span data-ttu-id="a74df-156">`ViewData` 에 속성으로 노출 되는 `ViewResult` 호출에서 반환 된는 `Details()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="a74df-156">The `ViewData` is exposed as a property on the `ViewResult` returned by invoking the `Details()` method.</span></span> <span data-ttu-id="a74df-157">`ViewData.Model` 속성 뷰에 전달 되는 제품을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-157">The `ViewData.Model` property contains the product passed to the view.</span></span> <span data-ttu-id="a74df-158">이 테스트는 단순히 데이터 보기에에서 포함 된 제품 이름을 랩톱에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-158">The test simply verifies that the product contained in the View Data has the name Laptop.</span></span>

## <a name="testing-the-action-result-returned-by-a-controller"></a><span data-ttu-id="a74df-159">컨트롤러에 의해 반환 된 작업 결과 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-159">Testing the Action Result returned by a Controller</span></span>

<span data-ttu-id="a74df-160">더 복잡 한 컨트롤러 작업 다양 한 유형의 컨트롤러 작업에 전달 된 매개 변수의 값에 따라 작업 결과 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-160">A more complex controller action might return different types of action results depending on the values of the parameters passed to the controller action.</span></span> <span data-ttu-id="a74df-161">컨트롤러 작업에는 다양 한 유형의 작업 결과 포함 하 여 반환할 수 있습니다는 `ViewResult`, `RedirectToRouteResult`, 또는 `JsonResult`합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-161">A controller action can return a variety of types of action results including a `ViewResult`, `RedirectToRouteResult`, or `JsonResult`.</span></span>

<span data-ttu-id="a74df-162">예를 들어 수정 된 `Details()` 목록 5의 동작은 반환는 `Details` 작업에 유효한 제품 Id를 전달 하는 경우를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-162">For example, the modified `Details()` action in Listing 5 returns the `Details` view when you pass a valid product Id to the action.</span></span> <span data-ttu-id="a74df-163">1--합니다는 리디렉션됩니다 보다 작은 잘못 된 제품 Id-Id 값으로 전달 하는 경우는 `Index()` 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-163">If you pass an invalid product Id -- an Id with a value less than 1 -- then you are redirected to the `Index()` action.</span></span>

<span data-ttu-id="a74df-164">**5-나열`ProductController.cs`**</span><span class="sxs-lookup"><span data-stu-id="a74df-164">**Listing 5 – `ProductController.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample7.cs)]

<span data-ttu-id="a74df-165">동작을 테스트할 수 있습니다는 `Details()` 목록 6에서 단위 테스트와 함께 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-165">You can test the behavior of the `Details()` action with the unit test in Listing 6.</span></span> <span data-ttu-id="a74df-166">단위 테스트 목록 6에서 확인으로 리디렉션됩니다는 `Index` 에 전달 된 값-1 Id 보기는 `Details()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="a74df-166">The unit test in Listing 6 verifies that you are redirected to the `Index` view when an Id with the value -1 is passed to the `Details()` method.</span></span>

<span data-ttu-id="a74df-167">**6-나열`ProductControllerTest.cs`**</span><span class="sxs-lookup"><span data-stu-id="a74df-167">**Listing 6 – `ProductControllerTest.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample8.cs)]

<span data-ttu-id="a74df-168">호출 하는 경우는 `RedirectToAction()` 는 컨트롤러 동작 메서드를 컨트롤러 작업 반환는 `RedirectToRouteResult`합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-168">When you call the `RedirectToAction()` method in a controller action, the controller action returns a `RedirectToRouteResult`.</span></span> <span data-ttu-id="a74df-169">테스트 검사 여부는 `RedirectToRouteResult` 는 라는 컨트롤러 작업으로 사용자를 리디렉션합니다 `Index`합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-169">The test checks whether the `RedirectToRouteResult` will redirect the user to a controller action named `Index`.</span></span>

## <a name="summary"></a><span data-ttu-id="a74df-170">요약</span><span class="sxs-lookup"><span data-stu-id="a74df-170">Summary</span></span>

<span data-ttu-id="a74df-171">이 자습서에서는 MVC 컨트롤러 작업에 대 한 단위 테스트를 작성 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-171">In this tutorial, you learned how to build unit tests for MVC controller actions.</span></span> <span data-ttu-id="a74df-172">첫째, 오른쪽 뷰의 컨트롤러 동작에 의해 반환 되는지 여부를 확인 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-172">First, you learned how to verify whether the right view is returned by a controller action.</span></span> <span data-ttu-id="a74df-173">사용 하는 방법을 배웠습니다는 `ViewResult.ViewName` 속성을 보기의 이름이 유효한 지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-173">You learned how to use the `ViewResult.ViewName` property to verify the name of a view.</span></span>

<span data-ttu-id="a74df-174">다음으로의 콘텐츠를 테스트 하는 방법을 검사 했습니다 `View Data`합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-174">Next, we examined how you can test the contents of `View Data`.</span></span> <span data-ttu-id="a74df-175">적합 한 제품에서 반환 된 있는지 여부를 확인 하는 방법을 배웠습니다 `View Data` 컨트롤러 작업을 호출한 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-175">You learned how to check whether the right product was returned in `View Data` after calling a controller action.</span></span>

<span data-ttu-id="a74df-176">마지막으로, 다양 한 유형의 작업 결과 컨트롤러 작업에서 반환 되는 여부를 테스트 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-176">Finally, we discussed how you can test whether different types of action results are returned from a controller action.</span></span> <span data-ttu-id="a74df-177">컨트롤러를 반환 하는지 여부를 테스트 하는 방법을 배웠습니다는 `ViewResult` 또는 `RedirectToRouteResult`합니다.</span><span class="sxs-lookup"><span data-stu-id="a74df-177">You learned how to test whether a controller returns a `ViewResult` or a `RedirectToRouteResult`.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="a74df-178">다음</span><span class="sxs-lookup"><span data-stu-id="a74df-178">Next</span></span>](creating-unit-tests-for-asp-net-mvc-applications-vb.md)
