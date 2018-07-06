---
uid: mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
title: ASP.NET MVC 응용 프로그램 (C#)에 대 한 단위 테스트 만들기 | Microsoft Docs
author: StephenWalther
description: 컨트롤러 작업에 대 한 단위 테스트를 만드는 방법에 알아봅니다. 이 자습서에서는 Stephen walther가 컨트롤러 작업을 parti 반환 하는지 여부를 테스트 하는 방법에 설명 하는 중...
ms.author: aspnetcontent
ms.date: 08/19/2008
ms.assetid: d3a270b9-d7b1-47f2-8775-fc3beb518b5c
msc.legacyurl: /mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
msc.type: authoredcontent
ms.openlocfilehash: f9e6945a379d37f1539c7135041f50dcc7041750
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37826681"
---
<a name="creating-unit-tests-for-aspnet-mvc-applications-c"></a><span data-ttu-id="439a2-104">ASP.NET MVC 응용 프로그램 (C#)에 대 한 단위 테스트 만들기</span><span class="sxs-lookup"><span data-stu-id="439a2-104">Creating Unit Tests for ASP.NET MVC Applications (C#)</span></span>
====================
<span data-ttu-id="439a2-105">[Stephen walther가](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="439a2-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

[<span data-ttu-id="439a2-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="439a2-106">Download PDF</span></span>](http://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_07_CS.pdf)

> <span data-ttu-id="439a2-107">컨트롤러 작업에 대 한 단위 테스트를 만드는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-107">Learn how to create unit tests for controller actions.</span></span> <span data-ttu-id="439a2-108">이 자습서에서는 Stephen walther가 테스트 컨트롤러 작업을 특정 뷰를 반환, 데이터의 특정 집합을 반환 또는 다른 유형의 작업 결과 반환 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-108">In this tutorial, Stephen Walther demonstrates how to test whether a controller action returns a particular view, returns a particular set of data, or returns a different type of action result.</span></span>


<span data-ttu-id="439a2-109">이 자습서의 목적은 작성 하는 방법의 컨트롤러에 대 한 단위 테스트에서 ASP.NET MVC 응용 프로그램을 보여 주기 위해 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-109">The goal of this tutorial is to demonstrate how you can write unit tests for the controllers in your ASP.NET MVC applications.</span></span> <span data-ttu-id="439a2-110">세 가지 유형의 단위 테스트를 작성 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-110">We discuss how to build three different types of unit tests.</span></span> <span data-ttu-id="439a2-111">컨트롤러 작업에 의해 반환 된 보기를 테스트 하는 방법, 컨트롤러 작업에 의해 반환 되는 뷰 데이터를 테스트 하는 방법 및 하나의 컨트롤러 작업이 두 번째 컨트롤러 작업에 리디렉션됩니다 여부를 테스트 하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-111">You learn how to test the view returned by a controller action, how to test the View Data returned by a controller action, and how to test whether or not one controller action redirects you to a second controller action.</span></span>

## <a name="creating-the-controller-under-test"></a><span data-ttu-id="439a2-112">테스트 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="439a2-112">Creating the Controller under Test</span></span>

<span data-ttu-id="439a2-113">테스트 하려는 컨트롤러를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-113">Let's start by creating the controller that we intend to test.</span></span> <span data-ttu-id="439a2-114">라는 컨트롤러를 `ProductController`, 목록 1에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-114">The controller, named the `ProductController`, is contained in Listing 1.</span></span>

<span data-ttu-id="439a2-115">**목록 1 – `ProductController.cs`**</span><span class="sxs-lookup"><span data-stu-id="439a2-115">**Listing 1 – `ProductController.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample1.cs)]

<span data-ttu-id="439a2-116">합니다 `ProductController` 라는 두 개의 작업 메서드를 포함 `Index()` 고 `Details()`입니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-116">The `ProductController` contains two action methods named `Index()` and `Details()`.</span></span> <span data-ttu-id="439a2-117">두 동작 메서드 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-117">Both action methods return a view.</span></span> <span data-ttu-id="439a2-118">다음에 유의 합니다 `Details()` 작업 id 라는 이름의 매개 변수를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-118">Notice that the `Details()` action accepts a parameter named Id.</span></span>

## <a name="testing-the-view-returned-by-a-controller"></a><span data-ttu-id="439a2-119">컨트롤러에 의해 반환 된 뷰 테스트</span><span class="sxs-lookup"><span data-stu-id="439a2-119">Testing the View returned by a Controller</span></span>

<span data-ttu-id="439a2-120">테스트 한다고 가정해 보겠습니다. 여부는 `ProductController` 오른쪽 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-120">Imagine that we want to test whether or not the `ProductController` returns the right view.</span></span> <span data-ttu-id="439a2-121">있는지 확인 하고자 때는 `ProductController.Details()` 작업을 호출할 세부 정보 보기 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-121">We want to make sure that when the `ProductController.Details()` action is invoked, the Details view is returned.</span></span> <span data-ttu-id="439a2-122">반환 된 뷰의 테스트에 대 한 단위 테스트를 포함 하는 목록 2의 test 클래스는 `ProductController.Details()` 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-122">The test class in Listing 2 contains a unit test for testing the view returned by the `ProductController.Details()` action.</span></span>

<span data-ttu-id="439a2-123">**2 – 나열 `ProductControllerTest.cs`**</span><span class="sxs-lookup"><span data-stu-id="439a2-123">**Listing 2 – `ProductControllerTest.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample2.cs)]

<span data-ttu-id="439a2-124">목록 2에서 클래스 라는 테스트 메서드 포함 `TestDetailsView()`합니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-124">The class in Listing 2 includes a test method named `TestDetailsView()`.</span></span> <span data-ttu-id="439a2-125">이 메서드는 코드의 세 줄을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-125">This method contains three lines of code.</span></span> <span data-ttu-id="439a2-126">코드의 첫 번째 줄의 새 인스턴스를 만듭니다를 `ProductController` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-126">The first line of code creates a new instance of the `ProductController` class.</span></span> <span data-ttu-id="439a2-127">컨트롤러의 호출 하는 두 번째 코드 줄 `Details()` 작업 메서드.</span><span class="sxs-lookup"><span data-stu-id="439a2-127">The second line of code invokes the controller's `Details()` action method.</span></span> <span data-ttu-id="439a2-128">마지막으로, 코드 검사 보기에서 반환 하는 여부의 마지막 줄은 `Details()` 작업 세부 정보 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-128">Finally, the last line of code checks whether or not the view returned by the `Details()` action is the Details view.</span></span>

<span data-ttu-id="439a2-129">`ViewResult.ViewName` 속성 컨트롤러에 의해 반환 된 뷰의 이름을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-129">The `ViewResult.ViewName` property represents the name of the view returned by a controller.</span></span> <span data-ttu-id="439a2-130">이 속성을 테스트 하는 방법에 대 한 하나의 큰 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-130">One big warning about testing this property.</span></span> <span data-ttu-id="439a2-131">두 가지 방법으로 컨트롤러는 보기를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-131">There are two ways that a controller can return a view.</span></span> <span data-ttu-id="439a2-132">컨트롤러는 다음과 같은 보기를 반환할 명시적으로 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-132">A controller can explicitly return a view like this:</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample3.cs)]

<span data-ttu-id="439a2-133">또는 뷰의 이름은 다음과 같이 컨트롤러 작업의 이름에서 유추할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-133">Alternatively, the name of the view can be inferred from the name of the controller action like this:</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample4.cs)]

<span data-ttu-id="439a2-134">이 컨트롤러 작업은 또한 라는 뷰를 반환 `Details`합니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-134">This controller action also returns a view named `Details`.</span></span> <span data-ttu-id="439a2-135">그러나 뷰의 이름은 작업 이름에서 유추 됩니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-135">However, the name of the view is inferred from the action name.</span></span> <span data-ttu-id="439a2-136">뷰 이름을 테스트 하려는 경우 다음 하면 명시적으로 이름을 반환 해야 보기 컨트롤러 작업에서.</span><span class="sxs-lookup"><span data-stu-id="439a2-136">If you want to test the view name, then you must explicitly return the view name from the controller action.</span></span>

<span data-ttu-id="439a2-137">키보드 조합을 입력 하거나 목록 2에서 단위 테스트를 실행할 수 있습니다 **Ctrl + R, A** 클릭 하 여 합니다 **솔루션의 모든 테스트 실행** 단추 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="439a2-137">You can run the unit test in Listing 2 by either entering the keyboard combination **Ctrl-R, A** or by clicking the **Run All Tests in Solution** button (see Figure 1).</span></span> <span data-ttu-id="439a2-138">테스트를 통과 하면 그림 2에서 테스트 결과 창을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-138">If the test passes, you'll see the Test Results window in Figure 2.</span></span>


<span data-ttu-id="439a2-139">[![솔루션의 모든 테스트 실행](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="439a2-139">[![Run All Tests in Solution](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image1.png)</span></span>

<span data-ttu-id="439a2-140">**그림 01**: 솔루션의 모든 테스트 실행 ([큰 이미지를 보려면 클릭](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="439a2-140">**Figure 01**: Run All Tests in Solution ([Click to view full-size image](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image3.png))</span></span>


<span data-ttu-id="439a2-141">[![성공 했습니다.](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="439a2-141">[![Success!](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image4.png)</span></span>

<span data-ttu-id="439a2-142">**그림 02**: 성공!</span><span class="sxs-lookup"><span data-stu-id="439a2-142">**Figure 02**: Success!</span></span> <span data-ttu-id="439a2-143">([클릭 하 여 큰 이미지 보기](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="439a2-143">([Click to view full-size image](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image6.png))</span></span>


## <a name="testing-the-view-data-returned-by-a-controller"></a><span data-ttu-id="439a2-144">컨트롤러에 의해 반환 된 뷰 데이터를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-144">Testing the View Data returned by a Controller</span></span>

<span data-ttu-id="439a2-145">MVC 컨트롤러 이라는 것을 사용 하 여 데이터 뷰로 전달 *`View Data`* 합니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-145">An MVC controller passes data to a view by using something called *`View Data`*.</span></span> <span data-ttu-id="439a2-146">예를 들어, 호출할 때 특정 제품에 대 한 세부 정보를 표시 한다고 가정해 보겠습니다는 `ProductController Details()` 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-146">For example, imagine that you want to display the details for a particular product when you invoke the `ProductController Details()` action.</span></span> <span data-ttu-id="439a2-147">이런 경우의 인스턴스를 만들 수 있습니다는 `Product` (모델에 정의 된) 클래스 인스턴스를 전달 하 고는 `Details` 뷰를 활용 하 여 `View Data`입니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-147">In that case, you can create an instance of a `Product` class (defined in your model) and pass the instance to the `Details` view by taking advantage of `View Data`.</span></span>

<span data-ttu-id="439a2-148">수정 된 `ProductController` 보기 3의 업데이트 된 포함 `Details()` 제품을 반환 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-148">The modified `ProductController` in Listing 3 includes an updated `Details()` action that returns a Product.</span></span>

<span data-ttu-id="439a2-149">**3 – 나열 `ProductController.cs`**</span><span class="sxs-lookup"><span data-stu-id="439a2-149">**Listing 3 – `ProductController.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample5.cs)]

<span data-ttu-id="439a2-150">먼저 합니다 `Details()` 작업의 새 인스턴스를 만듭니다는 `Product` 랩톱 컴퓨터를 나타내는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-150">First, the `Details()` action creates a new instance of the `Product` class that represents a laptop computer.</span></span> <span data-ttu-id="439a2-151">다음, 인스턴스를 `Product` 클래스는 두 번째 매개 변수로 전달 되는 `View()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="439a2-151">Next, the instance of the `Product` class is passed as the second parameter to the `View()` method.</span></span>

<span data-ttu-id="439a2-152">단위 테스트를 작성할 수 예상된 데이터 인지를 테스트 하려면 보기에 데이터가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-152">You can write unit tests to test whether the expected data is contained in view data.</span></span> <span data-ttu-id="439a2-153">랩톱 컴퓨터를 나타내는 제품을 호출할 때 반환 되는 여부 4 테스트에서 단위 테스트는 `ProductController Details()` 작업 메서드.</span><span class="sxs-lookup"><span data-stu-id="439a2-153">The unit test in Listing 4 tests whether or not a Product representing a laptop computer is returned when you call the `ProductController Details()` action method.</span></span>

<span data-ttu-id="439a2-154">**4-목록 `ProductControllerTest.cs`**</span><span class="sxs-lookup"><span data-stu-id="439a2-154">**Listing 4 – `ProductControllerTest.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample6.cs)]

<span data-ttu-id="439a2-155">목록 4에는 `TestDetailsView()` 메서드를 호출 하 여 반환 되는 뷰 데이터를 테스트 합니다 `Details()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="439a2-155">In Listing 4, the `TestDetailsView()` method tests the View Data returned by invoking the `Details()` method.</span></span> <span data-ttu-id="439a2-156">합니다 `ViewData` 에 속성으로 노출 되는 `ViewResult` 호출에서 반환 된를 `Details()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="439a2-156">The `ViewData` is exposed as a property on the `ViewResult` returned by invoking the `Details()` method.</span></span> <span data-ttu-id="439a2-157">`ViewData.Model` 속성 보기에 전달 하는 제품을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-157">The `ViewData.Model` property contains the product passed to the view.</span></span> <span data-ttu-id="439a2-158">테스트는 단순히 데이터 보기에에서 포함 된 제품 이름을 랩톱에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-158">The test simply verifies that the product contained in the View Data has the name Laptop.</span></span>

## <a name="testing-the-action-result-returned-by-a-controller"></a><span data-ttu-id="439a2-159">컨트롤러에서 반환 된 작업 결과 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-159">Testing the Action Result returned by a Controller</span></span>

<span data-ttu-id="439a2-160">더 복잡 한 컨트롤러 작업을 다양 한 컨트롤러 작업에 전달 된 매개 변수의 값에 따라 작업 결과 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-160">A more complex controller action might return different types of action results depending on the values of the parameters passed to the controller action.</span></span> <span data-ttu-id="439a2-161">컨트롤러 작업을 다양 한 유형의 작업 결과 포함 하 여 반환할 수는 `ViewResult`, `RedirectToRouteResult`, 또는 `JsonResult`합니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-161">A controller action can return a variety of types of action results including a `ViewResult`, `RedirectToRouteResult`, or `JsonResult`.</span></span>

<span data-ttu-id="439a2-162">예를 들어 수정 된 `Details()` 목록 5에서 작업을 반환 합니다 `Details` 작업에 올바른 제품 Id를 전달 하는 경우를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-162">For example, the modified `Details()` action in Listing 5 returns the `Details` view when you pass a valid product Id to the action.</span></span> <span data-ttu-id="439a2-163">1--있다면 리디렉션됩니다 미만의 잘못 된 제품 Id-Id 값으로 전달 하는 경우는 `Index()` 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-163">If you pass an invalid product Id -- an Id with a value less than 1 -- then you are redirected to the `Index()` action.</span></span>

<span data-ttu-id="439a2-164">**5-목록 `ProductController.cs`**</span><span class="sxs-lookup"><span data-stu-id="439a2-164">**Listing 5 – `ProductController.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample7.cs)]

<span data-ttu-id="439a2-165">동작을 테스트할 수 있습니다는 `Details()` 목록 6에서 단위 테스트를 사용 하 여 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-165">You can test the behavior of the `Details()` action with the unit test in Listing 6.</span></span> <span data-ttu-id="439a2-166">목록 6에서 단위 테스트의 확인로 리디렉션됩니다 합니다 `Index` -1 값을 사용 하 여 Id로 전달 될 때 보기는 `Details()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="439a2-166">The unit test in Listing 6 verifies that you are redirected to the `Index` view when an Id with the value -1 is passed to the `Details()` method.</span></span>

<span data-ttu-id="439a2-167">**6-목록 `ProductControllerTest.cs`**</span><span class="sxs-lookup"><span data-stu-id="439a2-167">**Listing 6 – `ProductControllerTest.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample8.cs)]

<span data-ttu-id="439a2-168">호출 하는 경우는 `RedirectToAction()` 컨트롤러 작업에서 메서드를 컨트롤러 작업 반환을 `RedirectToRouteResult`입니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-168">When you call the `RedirectToAction()` method in a controller action, the controller action returns a `RedirectToRouteResult`.</span></span> <span data-ttu-id="439a2-169">테스트 검사 하는지 여부를 합니다 `RedirectToRouteResult` 가 명명 된 컨트롤러 작업에 사용자를 리디렉션합니다 `Index`합니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-169">The test checks whether the `RedirectToRouteResult` will redirect the user to a controller action named `Index`.</span></span>

## <a name="summary"></a><span data-ttu-id="439a2-170">요약</span><span class="sxs-lookup"><span data-stu-id="439a2-170">Summary</span></span>

<span data-ttu-id="439a2-171">이 자습서에서는 MVC 컨트롤러 작업에 대 한 단위 테스트를 작성 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-171">In this tutorial, you learned how to build unit tests for MVC controller actions.</span></span> <span data-ttu-id="439a2-172">첫째, 오른쪽 뷰의 컨트롤러 작업에 의해 반환 되는지 여부를 확인 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-172">First, you learned how to verify whether the right view is returned by a controller action.</span></span> <span data-ttu-id="439a2-173">사용 하는 방법과 `ViewResult.ViewName` 뷰의 이름을 확인 하는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-173">You learned how to use the `ViewResult.ViewName` property to verify the name of a view.</span></span>

<span data-ttu-id="439a2-174">내용을 테스트 하는 방법을 검사한 다음으로, `View Data`합니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-174">Next, we examined how you can test the contents of `View Data`.</span></span> <span data-ttu-id="439a2-175">적합 한 제품에서 반환 된 여부를 확인 하는 방법과 `View Data` 컨트롤러 작업을 호출한 후입니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-175">You learned how to check whether the right product was returned in `View Data` after calling a controller action.</span></span>

<span data-ttu-id="439a2-176">마지막으로, 컨트롤러 작업에서 다양 한 유형의 작업 결과 반환 하는지 여부를 테스트 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-176">Finally, we discussed how you can test whether different types of action results are returned from a controller action.</span></span> <span data-ttu-id="439a2-177">컨트롤러를 반환 하는지 여부를 테스트 하는 방법과 `ViewResult` 또는 `RedirectToRouteResult`합니다.</span><span class="sxs-lookup"><span data-stu-id="439a2-177">You learned how to test whether a controller returns a `ViewResult` or a `RedirectToRouteResult`.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="439a2-178">다음</span><span class="sxs-lookup"><span data-stu-id="439a2-178">Next</span></span>](creating-unit-tests-for-asp-net-mvc-applications-vb.md)
