---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-controller-overview-vb
title: "ASP.NET MVC 컨트롤러 개요 (VB) | Microsoft Docs"
author: StephenWalther
description: "이 자습서에서는 Stephen Walther ASP.NET MVC 컨트롤러를 소개합니다. 새 컨트롤러를 만들고 다양 한 유형의 작업 res 반환 하는 방법을 배웁니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/16/2008
ms.topic: article
ms.assetid: 94c3e5d9-a904-445e-a34e-d92fd1ca108a
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-controller-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: 452e2cf771e8b1f298ce9693ec2a707e7c1d4dd1
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="aspnet-mvc-controller-overview-vb"></a><span data-ttu-id="e626a-104">ASP.NET MVC 컨트롤러 개요 (VB)</span><span class="sxs-lookup"><span data-stu-id="e626a-104">ASP.NET MVC Controller Overview (VB)</span></span>
====================
<span data-ttu-id="e626a-105">으로 [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="e626a-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="e626a-106">이 자습서에서는 Stephen Walther ASP.NET MVC 컨트롤러를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-106">In this tutorial, Stephen Walther introduces you to ASP.NET MVC controllers.</span></span> <span data-ttu-id="e626a-107">새 컨트롤러를 만들고 다양 한 유형의 작업 결과 반환 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-107">You learn how to create new controllers and return different types of action results.</span></span>


<span data-ttu-id="e626a-108">이 자습서는 ASP.NET MVC 컨트롤러, 컨트롤러 작업 및 작업 결과의 항목을 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-108">This tutorial explores the topic of ASP.NET MVC controllers, controller actions, and action results.</span></span> <span data-ttu-id="e626a-109">이 자습서를 완료 한 후에 컨트롤러는 ASP.NET MVC 웹 사이트와 상호 작용 하는 방문자 방식을 제어 하는 데 사용 하는 방법을 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-109">After you complete this tutorial, you will understand how controllers are used to control the way a visitor interacts with an ASP.NET MVC website.</span></span>

## <a name="understanding-controllers"></a><span data-ttu-id="e626a-110">컨트롤러의 이해</span><span class="sxs-lookup"><span data-stu-id="e626a-110">Understanding Controllers</span></span>

<span data-ttu-id="e626a-111">MVC 컨트롤러는는 ASP.NET MVC 웹 사이트에 대 한 요청에 응답 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-111">MVC controllers are responsible for responding to requests made against an ASP.NET MVC website.</span></span> <span data-ttu-id="e626a-112">각 브라우저 요청은 특정 컨트롤러에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-112">Each browser request is mapped to a particular controller.</span></span> <span data-ttu-id="e626a-113">예를 들어 브라우저의 주소 표시줄에 다음 URL을 입력 같이 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-113">For example, imagine that you enter the following URL into the address bar of your browser:</span></span>

`http://localhost/Product/Index/3`

<span data-ttu-id="e626a-114">이 경우 ProductController 라는 컨트롤러 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-114">In this case, a controller named ProductController is invoked.</span></span> <span data-ttu-id="e626a-115">ProductController는 브라우저 요청에 대 한 응답을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-115">The ProductController is responsible for generating the response to the browser request.</span></span> <span data-ttu-id="e626a-116">예를 들어 컨트롤러 브라우저에 다시 특정 보기를 반환할 수 있습니다 또는 컨트롤러를 다른 컨트롤러 사용자를 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-116">For example, the controller might return a particular view back to the browser or the controller might redirect the user to another controller.</span></span>

<span data-ttu-id="e626a-117">목록 1 ProductController 라는 간단한 컨트롤러를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-117">Listing 1 contains a simple controller named ProductController.</span></span>

<span data-ttu-id="e626a-118">**Listing1-Controllers\ProductController.vb**</span><span class="sxs-lookup"><span data-stu-id="e626a-118">**Listing1 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample1.vb)]

<span data-ttu-id="e626a-119">목록 1 알 수 있듯이 컨트롤러 클래스 (Visual Basic.NET 또는 C# 클래스)만입니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-119">As you can see from Listing 1, a controller is just a class (a Visual Basic .NET or C# class).</span></span> <span data-ttu-id="e626a-120">한 컨트롤러는 기본 System.Web.Mvc.Controller 클래스에서 파생 되는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-120">A controller is a class that derives from the base System.Web.Mvc.Controller class.</span></span> <span data-ttu-id="e626a-121">컨트롤러를 몇 가지 유용한 메서드를 무료로 상속 컨트롤러를이 기본 클래스에서 상속 하기 때문에 (에서는 이러한 메서드 잠시 후에).</span><span class="sxs-lookup"><span data-stu-id="e626a-121">Because a controller inherits from this base class, a controller inherits several useful methods for free (We discuss these methods in a moment).</span></span>

## <a name="understanding-controller-actions"></a><span data-ttu-id="e626a-122">컨트롤러 동작 이해</span><span class="sxs-lookup"><span data-stu-id="e626a-122">Understanding Controller Actions</span></span>

<span data-ttu-id="e626a-123">컨트롤러는 컨트롤러 동작을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-123">A controller exposes controller actions.</span></span> <span data-ttu-id="e626a-124">동작은 브라우저 주소 표시줄에서 특정 URL을 입력 하면 호출 되는 컨트롤러에 대해 메서드를 말합니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-124">An action is a method on a controller that gets called when you enter a particular URL in your browser address bar.</span></span> <span data-ttu-id="e626a-125">예를 들어 다음 URL에 대 한 요청을 수행 같이 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-125">For example, imagine that you make a request for the following URL:</span></span>

`http://localhost/Product/Index/3`

<span data-ttu-id="e626a-126">이 경우 index () 메서드 ProductController 클래스에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-126">In this case, the Index() method is called on the ProductController class.</span></span> <span data-ttu-id="e626a-127">Index () 메서드는 컨트롤러 동작의 예시입니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-127">The Index() method is an example of a controller action.</span></span>

<span data-ttu-id="e626a-128">컨트롤러 동작을 컨트롤러 클래스의 공용 메서드여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-128">A controller action must be a public method of a controller class.</span></span> <span data-ttu-id="e626a-129">기본적으로 visual Basic.NET 메서드는 공용 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-129">Visual Basic.NET methods, by default, are public methods.</span></span> <span data-ttu-id="e626a-130">컨트롤러 클래스에 추가 하는 모든 public 메서드를 컨트롤러 작업으로 자동으로 노출 된다는 것을 실제로 (주의 해야이 대 한 브라우저 주소 표시줄에 올바른 URL을 입력 하면 모든 사용자는 universe에서 컨트롤러 동작을 호출할 수 있으므로).</span><span class="sxs-lookup"><span data-stu-id="e626a-130">Realize that any public method that you add to a controller class is exposed as a controller action automatically (You must be careful about this since a controller action can be invoked by anyone in the universe simply by typing the right URL into a browser address bar).</span></span>

<span data-ttu-id="e626a-131">컨트롤러 동작에 의해 충족 되어야 하는 몇 가지 추가 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-131">There are some additional requirements that must be satisfied by a controller action.</span></span> <span data-ttu-id="e626a-132">컨트롤러 작업으로 사용 되는 메서드를 오버 로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-132">A method used as a controller action cannot be overloaded.</span></span> <span data-ttu-id="e626a-133">또한 컨트롤러 작업에는 정적 메서드 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-133">Furthermore, a controller action cannot be a static method.</span></span> <span data-ttu-id="e626a-134">외에 원하는 거의 모든 메서드를 컨트롤러 작업으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-134">Other than that, you can use just about any method as a controller action.</span></span>

## <a name="understanding-action-results"></a><span data-ttu-id="e626a-135">작업 결과 이해</span><span class="sxs-lookup"><span data-stu-id="e626a-135">Understanding Action Results</span></span>

<span data-ttu-id="e626a-136">이라고 하는 항목을 반환 하는 컨트롤러 작업은 *작업 결과*합니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-136">A controller action returns something called an *action result*.</span></span> <span data-ttu-id="e626a-137">작업 결과 브라우저 요청에 대 한 응답에서 컨트롤러 작업을 반환 하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-137">An action result is what a controller action returns in response to a browser request.</span></span>

<span data-ttu-id="e626a-138">ASP.NET MVC 프레임 워크에서는 여러 유형의 작업 결과 포함 하 여 지원:</span><span class="sxs-lookup"><span data-stu-id="e626a-138">The ASP.NET MVC framework supports several types of action results including:</span></span>

1. <span data-ttu-id="e626a-139">ViewResult-나타내는 HTML 및 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-139">ViewResult - Represents HTML and markup.</span></span>
2. <span data-ttu-id="e626a-140">EmptyResult-없는 결과를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-140">EmptyResult - Represents no result.</span></span>
3. <span data-ttu-id="e626a-141">된 RedirectResult-새 URL로 리디렉션을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-141">RedirectResult - Represents a redirection to a new URL.</span></span>
4. <span data-ttu-id="e626a-142">JsonResult-AJAX 응용 프로그램에서 사용할 수 있는 JavaScript 개체 Object Notation 결과를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-142">JsonResult - Represents a JavaScript Object Notation result that can be used in an AJAX application.</span></span>
5. <span data-ttu-id="e626a-143">JavaScriptResult-는 JavaScript 스크립트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-143">JavaScriptResult - Represents a JavaScript script.</span></span>
6. <span data-ttu-id="e626a-144">ContentResult-텍스트 결과를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-144">ContentResult - Represents a text result.</span></span>
7. <span data-ttu-id="e626a-145">FileContentResult-는 다운로드 가능한 파일을 (이진 콘텐츠)를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-145">FileContentResult - Represents a downloadable file (with the binary content).</span></span>
8. <span data-ttu-id="e626a-146">FilePathResult-는 다운로드 가능한 파일을 (경로)를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-146">FilePathResult - Represents a downloadable file (with a path).</span></span>
9. <span data-ttu-id="e626a-147">FileStreamResult-는 다운로드 가능한 파일을 (파일 스트림)를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-147">FileStreamResult - Represents a downloadable file (with a file stream).</span></span>

<span data-ttu-id="e626a-148">이러한 작업 결과의 모든 기본 ActionResult 클래스에서 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-148">All of these action results inherit from the base ActionResult class.</span></span>

<span data-ttu-id="e626a-149">대부분의 경우 컨트롤러 작업이 ViewResult를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-149">In most cases, a controller action returns a ViewResult.</span></span> <span data-ttu-id="e626a-150">예를 들어 인덱스 컨트롤러 동작 목록 2에는 ViewResult를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-150">For example, the Index controller action in Listing 2 returns a ViewResult.</span></span>

<span data-ttu-id="e626a-151">**2-Controllers\BookController.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="e626a-151">**Listing 2 - Controllers\BookController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample2.vb)]

<span data-ttu-id="e626a-152">작업에는 ViewResult 반환 될 때 HTML 브라우저에 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-152">When an action returns a ViewResult, HTML is returned to the browser.</span></span> <span data-ttu-id="e626a-153">목록 2의 index () 메서드를 브라우저에 인덱스를 명명 된 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-153">The Index() method in Listing 2 returns a view named Index to the browser.</span></span>

<span data-ttu-id="e626a-154">알림 목록 2에서 index () 동작을 ViewResult() 반환 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-154">Notice that the Index() action in Listing 2 does not return a ViewResult().</span></span> <span data-ttu-id="e626a-155">대신 컨트롤러 기본 클래스의 View() 메서드 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-155">Instead, the View() method of the Controller base class is called.</span></span> <span data-ttu-id="e626a-156">일반적으로 반환 하지 않습니다는 작업 결과 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-156">Normally, you do not return an action result directly.</span></span> <span data-ttu-id="e626a-157">대신, 호출 컨트롤러 기본 클래스의 다음 메서드 중 하나:</span><span class="sxs-lookup"><span data-stu-id="e626a-157">Instead, you call one of the following methods of the Controller base class:</span></span>

1. <span data-ttu-id="e626a-158">보기-ViewResult 작업 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-158">View - Returns a ViewResult action result.</span></span>
2. <span data-ttu-id="e626a-159">리디렉션-된 RedirectResult 작업 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-159">Redirect - Returns a RedirectResult action result.</span></span>
3. <span data-ttu-id="e626a-160">RedirectToAction-RedirectToRouteResult 작업 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-160">RedirectToAction - Returns a RedirectToRouteResult action result.</span></span>
4. <span data-ttu-id="e626a-161">RedirectToRoute-RedirectToRouteResult 작업 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-161">RedirectToRoute - Returns a RedirectToRouteResult action result.</span></span>
5. <span data-ttu-id="e626a-162">Json-JsonResult 작업 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-162">Json - Returns a JsonResult action result.</span></span>
6. <span data-ttu-id="e626a-163">JavaScriptResult-는 JavaScriptResult를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-163">JavaScriptResult - Returns a JavaScriptResult.</span></span>
7. <span data-ttu-id="e626a-164">콘텐츠-ContentResult 작업 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-164">Content - Returns a ContentResult action result.</span></span>
8. <span data-ttu-id="e626a-165">파일-반환 FileContentResult, FilePathResult, 또는 매개 변수에 따라 FileStreamResult 메서드에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-165">File - Returns a FileContentResult, FilePathResult, or FileStreamResult depending on the parameters passed to the method.</span></span>

<span data-ttu-id="e626a-166">따라서 브라우저에는 뷰를 반환 하려는 경우에 View() 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-166">So, if you want to return a View to the browser, you call the View() method.</span></span> <span data-ttu-id="e626a-167">다른 한 컨트롤러 작업에서 사용자를 리디렉션할 하려면 RedirectToAction() 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-167">If you want to redirect the user from one controller action to another, you call the RedirectToAction() method.</span></span> <span data-ttu-id="e626a-168">예를 들어 목록 3에서 Details() 작업 보기를 표시 또는 Id 매개 변수 값에 있는지 여부에 따라 index () 작업에는 사용자를 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-168">For example, the Details() action in Listing 3 either displays a view or redirects the user to the Index() action depending on whether the Id parameter has a value.</span></span>

<span data-ttu-id="e626a-169">**3-CustomerController.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="e626a-169">**Listing 3 - CustomerController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample3.vb)]

<span data-ttu-id="e626a-170">ContentResult 작업 결과 특별 합니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-170">The ContentResult action result is special.</span></span> <span data-ttu-id="e626a-171">일반 텍스트로 된 작업 결과를 반환할 ContentResult 작업 결과 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-171">You can use the ContentResult action result to return an action result as plain text.</span></span> <span data-ttu-id="e626a-172">예를 들어 목록 4에 index () 메서드는 HTML 아닌 일반 텍스트로 메시지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-172">For example, the Index() method in Listing 4 returns a message as plain text and not as HTML.</span></span>

<span data-ttu-id="e626a-173">**4-Controllers\StatusController.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="e626a-173">**Listing 4 - Controllers\StatusController.vb**</span></span>

> <span data-ttu-id="e626a-174">StatusController</span><span class="sxs-lookup"><span data-stu-id="e626a-174">StatusController</span></span>


> <span data-ttu-id="e626a-175">System.Web.Mvc.Controller</span><span class="sxs-lookup"><span data-stu-id="e626a-175">System.Web.Mvc.Controller</span></span>


[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample4.vb)]

<span data-ttu-id="e626a-176">StatusController.Index() 동작이 호출 되 면 뷰 반환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-176">When the StatusController.Index() action is invoked, a view is not returned.</span></span> <span data-ttu-id="e626a-177">대신 원시 텍스트 "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="e626a-177">Instead, the raw text "Hello World!"</span></span> <span data-ttu-id="e626a-178">브라우저에 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-178">is returned to the browser.</span></span>

<span data-ttu-id="e626a-179">컨트롤러 작업 결과가 작업 결과 하지-예를 들어 날짜 또는-정수를 반환 하는 경우 다음 결과에 래핑됩니다는 ContentResult 자동으로.</span><span class="sxs-lookup"><span data-stu-id="e626a-179">If a controller action returns a result that is not an action result - for example, a date or an integer - then the result is wrapped in a ContentResult automatically.</span></span> <span data-ttu-id="e626a-180">예를 들어 목록 5의 WorkController의 index () 작업을 호출할 때 날짜 반환 됩니다는 ContentResult으로 자동으로.</span><span class="sxs-lookup"><span data-stu-id="e626a-180">For example, when the Index() action of the WorkController in Listing 5 is invoked, the date is returned as a ContentResult automatically.</span></span>

<span data-ttu-id="e626a-181">**5-WorkController.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="e626a-181">**Listing 5 - WorkController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample5.vb)]

<span data-ttu-id="e626a-182">Index () 동작 목록 5의 DateTime 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-182">The Index() action in Listing 5 returns a DateTime object.</span></span> <span data-ttu-id="e626a-183">ASP.NET MVC 프레임 워크는 DateTime 개체를 문자열로 변환 하 고는 ContentResult에 날짜/시간 값을 자동으로 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-183">The ASP.NET MVC framework converts the DateTime object to a string and wraps the DateTime value in a ContentResult automatically.</span></span> <span data-ttu-id="e626a-184">브라우저에는 날짜 및 시간을 일반 텍스트로 받습니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-184">The browser receives the date and time as plain text.</span></span>

## <a name="summary"></a><span data-ttu-id="e626a-185">요약</span><span class="sxs-lookup"><span data-stu-id="e626a-185">Summary</span></span>

<span data-ttu-id="e626a-186">이 자습서의 목적은 ASP.NET MVC 컨트롤러, 컨트롤러 작업 및 컨트롤러 작업 결과의 개념을 소개 하는 것 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-186">The purpose of this tutorial was to introduce you to the concepts of ASP.NET MVC controllers, controller actions, and controller action results.</span></span> <span data-ttu-id="e626a-187">첫 번째 섹션에서는 ASP.NET MVC 프로젝트에 새 컨트롤러를 추가 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-187">In the first section, you learned how to add new controllers to an ASP.NET MVC project.</span></span> <span data-ttu-id="e626a-188">컨트롤러의 어떻게 공용 메서드를 학습 하는 다음으로 universe 컨트롤러 작업으로 노출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-188">Next, you learned how public methods of a controller are exposed to the universe as controller actions.</span></span> <span data-ttu-id="e626a-189">마지막으로, 다양 한 유형의 컨트롤러 작업에서 반환 될 수 있는 작업 결과 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-189">Finally, we discussed the different types of action results that can be returned from a controller action.</span></span> <span data-ttu-id="e626a-190">특히, ViewResult, RedirectToActionResult, 및 ContentResult 컨트롤러 작업에서 반환 하는 방법에 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e626a-190">In particular, we discussed how to return a ViewResult, RedirectToActionResult, and ContentResult from a controller action.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="e626a-191">[이전](creating-a-custom-route-constraint-cs.md)
[다음](creating-custom-routes-vb.md)</span><span class="sxs-lookup"><span data-stu-id="e626a-191">[Previous](creating-a-custom-route-constraint-cs.md)
[Next](creating-custom-routes-vb.md)</span></span>
