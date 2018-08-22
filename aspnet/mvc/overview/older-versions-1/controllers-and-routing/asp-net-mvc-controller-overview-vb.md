---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-controller-overview-vb
title: ASP.NET MVC 컨트롤러 개요 (VB) | Microsoft Docs
author: StephenWalther
description: 이 자습서에서는 Stephen walther가 ASP.NET MVC 컨트롤러를 소개합니다. 새 컨트롤러를 만들고 다양 한 유형의 작업 응답을 반환 하는 방법을 배웁니다.
ms.author: riande
ms.date: 02/16/2008
ms.assetid: 94c3e5d9-a904-445e-a34e-d92fd1ca108a
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-controller-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: 604bf4af2a46e56d9445de141fae1a1651acf47f
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41828016"
---
<a name="aspnet-mvc-controller-overview-vb"></a><span data-ttu-id="e13b0-104">ASP.NET MVC 컨트롤러 개요 (VB)</span><span class="sxs-lookup"><span data-stu-id="e13b0-104">ASP.NET MVC Controller Overview (VB)</span></span>
====================
<span data-ttu-id="e13b0-105">[Stephen walther가](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="e13b0-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="e13b0-106">이 자습서에서는 Stephen walther가 ASP.NET MVC 컨트롤러를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-106">In this tutorial, Stephen Walther introduces you to ASP.NET MVC controllers.</span></span> <span data-ttu-id="e13b0-107">새 컨트롤러를 만들고 다양 한 유형의 작업 결과 반환 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-107">You learn how to create new controllers and return different types of action results.</span></span>


<span data-ttu-id="e13b0-108">이 자습서에서는 ASP.NET MVC 컨트롤러, 컨트롤러 작업 및 작업 결과의 항목을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-108">This tutorial explores the topic of ASP.NET MVC controllers, controller actions, and action results.</span></span> <span data-ttu-id="e13b0-109">이 자습서를 완료 한 후에 컨트롤러 방문자는 ASP.NET MVC 웹 사이트와 상호 작용 하는 방식을 제어를 사용 하는 방법을 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-109">After you complete this tutorial, you will understand how controllers are used to control the way a visitor interacts with an ASP.NET MVC website.</span></span>

## <a name="understanding-controllers"></a><span data-ttu-id="e13b0-110">컨트롤러의 이해</span><span class="sxs-lookup"><span data-stu-id="e13b0-110">Understanding Controllers</span></span>

<span data-ttu-id="e13b0-111">MVC 컨트롤러는 ASP.NET MVC 웹 사이트에 대해 수행 된 요청에 응답 하는 것에 대 한 책임이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-111">MVC controllers are responsible for responding to requests made against an ASP.NET MVC website.</span></span> <span data-ttu-id="e13b0-112">각 브라우저 요청을 특정 컨트롤러에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-112">Each browser request is mapped to a particular controller.</span></span> <span data-ttu-id="e13b0-113">예를 들어 브라우저의 주소 표시줄에 다음 URL을 입력 하는 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-113">For example, imagine that you enter the following URL into the address bar of your browser:</span></span>

`http://localhost/Product/Index/3`

<span data-ttu-id="e13b0-114">이 경우 ProductController 라는 컨트롤러가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-114">In this case, a controller named ProductController is invoked.</span></span> <span data-ttu-id="e13b0-115">ProductController는 브라우저 요청에 대 한 응답을 생성 하는 일을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-115">The ProductController is responsible for generating the response to the browser request.</span></span> <span data-ttu-id="e13b0-116">예를 들어 컨트롤러 브라우저로 특정 보기를 반환할 수 있습니다 또는 컨트롤러 다른 컨트롤러에 사용자를 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-116">For example, the controller might return a particular view back to the browser or the controller might redirect the user to another controller.</span></span>

<span data-ttu-id="e13b0-117">목록 1 ProductController 라는 간단한 컨트롤러가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-117">Listing 1 contains a simple controller named ProductController.</span></span>

<span data-ttu-id="e13b0-118">**Listing1 - Controllers\ProductController.vb**</span><span class="sxs-lookup"><span data-stu-id="e13b0-118">**Listing1 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample1.vb)]

<span data-ttu-id="e13b0-119">목록 1에서 보듯이 컨트롤러 클래스 (Visual Basic.NET 또는 C# 클래스)만 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-119">As you can see from Listing 1, a controller is just a class (a Visual Basic .NET or C# class).</span></span> <span data-ttu-id="e13b0-120">컨트롤러는 기본 System.Web.Mvc.Controller 클래스에서 파생 된 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-120">A controller is a class that derives from the base System.Web.Mvc.Controller class.</span></span> <span data-ttu-id="e13b0-121">컨트롤러를 몇 가지 유용한 메서드를 무료로 상속 컨트롤러를이 기본 클래스에서 상속 하기 때문에 (에서는 이러한 메서드에 대해 잠시 후에).</span><span class="sxs-lookup"><span data-stu-id="e13b0-121">Because a controller inherits from this base class, a controller inherits several useful methods for free (We discuss these methods in a moment).</span></span>

## <a name="understanding-controller-actions"></a><span data-ttu-id="e13b0-122">컨트롤러 작업 이해</span><span class="sxs-lookup"><span data-stu-id="e13b0-122">Understanding Controller Actions</span></span>

<span data-ttu-id="e13b0-123">컨트롤러는 컨트롤러 작업을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-123">A controller exposes controller actions.</span></span> <span data-ttu-id="e13b0-124">작업을 사용 하면 브라우저 주소 표시줄에서 특정 URL을 입력 하면 호출 되는 컨트롤러의 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-124">An action is a method on a controller that gets called when you enter a particular URL in your browser address bar.</span></span> <span data-ttu-id="e13b0-125">예를 들어 다음 URL에 대 한 요청을 수행 하는 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-125">For example, imagine that you make a request for the following URL:</span></span>

`http://localhost/Product/Index/3`

<span data-ttu-id="e13b0-126">이 예에서 index () 메서드는 ProductController 클래스에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-126">In this case, the Index() method is called on the ProductController class.</span></span> <span data-ttu-id="e13b0-127">Index () 메서드는 컨트롤러 동작의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-127">The Index() method is an example of a controller action.</span></span>

<span data-ttu-id="e13b0-128">컨트롤러 동작을 컨트롤러 클래스의 공용 메서드여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-128">A controller action must be a public method of a controller class.</span></span> <span data-ttu-id="e13b0-129">기본적으로 visual Basic.NET 메서드는 공용 메서드.</span><span class="sxs-lookup"><span data-stu-id="e13b0-129">Visual Basic.NET methods, by default, are public methods.</span></span> <span data-ttu-id="e13b0-130">컨트롤러 클래스에 추가한 모든 public 메서드를 컨트롤러 작업으로 자동으로 노출 된다는 것을 실현 (않도록 주의 해야이 대 한 브라우저 주소 표시줄에 올바른 URL을 입력 하면 universe의 모든 사용자가 컨트롤러 작업을 호출할 수 있습니다 때문).</span><span class="sxs-lookup"><span data-stu-id="e13b0-130">Realize that any public method that you add to a controller class is exposed as a controller action automatically (You must be careful about this since a controller action can be invoked by anyone in the universe simply by typing the right URL into a browser address bar).</span></span>

<span data-ttu-id="e13b0-131">컨트롤러 작업에 의해 충족 되어야 하는 몇 가지 추가 요구 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-131">There are some additional requirements that must be satisfied by a controller action.</span></span> <span data-ttu-id="e13b0-132">컨트롤러 작업으로 사용 된 메서드를 오버 로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-132">A method used as a controller action cannot be overloaded.</span></span> <span data-ttu-id="e13b0-133">또한 컨트롤러 작업에는 정적 메서드 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-133">Furthermore, a controller action cannot be a static method.</span></span> <span data-ttu-id="e13b0-134">이외에 컨트롤러 작업으로 거의 모든 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-134">Other than that, you can use just about any method as a controller action.</span></span>

## <a name="understanding-action-results"></a><span data-ttu-id="e13b0-135">작업 결과 이해</span><span class="sxs-lookup"><span data-stu-id="e13b0-135">Understanding Action Results</span></span>

<span data-ttu-id="e13b0-136">컨트롤러 작업 반환 이라는 것을 *작업 결과*합니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-136">A controller action returns something called an *action result*.</span></span> <span data-ttu-id="e13b0-137">작업 결과 브라우저 요청에 대 한 응답에서 컨트롤러 작업을 반환 하는 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-137">An action result is what a controller action returns in response to a browser request.</span></span>

<span data-ttu-id="e13b0-138">ASP.NET MVC 프레임 워크는 여러 유형의 작업 결과 포함 하 여 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-138">The ASP.NET MVC framework supports several types of action results including:</span></span>

1. <span data-ttu-id="e13b0-139">ViewResult-나타내는 HTML 및 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-139">ViewResult - Represents HTML and markup.</span></span>
2. <span data-ttu-id="e13b0-140">EmptyResult-없는 결과를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-140">EmptyResult - Represents no result.</span></span>
3. <span data-ttu-id="e13b0-141">된 RedirectResult-새 URL로 리디렉션을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-141">RedirectResult - Represents a redirection to a new URL.</span></span>
4. <span data-ttu-id="e13b0-142">JsonResult-AJAX 응용 프로그램에서 사용할 수 있는 JavaScript Object Notation 결과를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-142">JsonResult - Represents a JavaScript Object Notation result that can be used in an AJAX application.</span></span>
5. <span data-ttu-id="e13b0-143">JavaScriptResult-JavaScript 스크립트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-143">JavaScriptResult - Represents a JavaScript script.</span></span>
6. <span data-ttu-id="e13b0-144">ContentResult-텍스트 결과를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-144">ContentResult - Represents a text result.</span></span>
7. <span data-ttu-id="e13b0-145">FileContentResult-은 다운로드 가능한 파일을 (이진 콘텐츠)를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-145">FileContentResult - Represents a downloadable file (with the binary content).</span></span>
8. <span data-ttu-id="e13b0-146">FilePathResult-다운로드 한 파일을 (경로로)를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-146">FilePathResult - Represents a downloadable file (with a path).</span></span>
9. <span data-ttu-id="e13b0-147">FileStreamResult-다운로드 한 파일을 (파일 스트림과)를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-147">FileStreamResult - Represents a downloadable file (with a file stream).</span></span>

<span data-ttu-id="e13b0-148">이러한 작업 결과의 모든 기본 ActionResult 클래스에서 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-148">All of these action results inherit from the base ActionResult class.</span></span>

<span data-ttu-id="e13b0-149">대부분의 경우 컨트롤러 작업을 ViewResult를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-149">In most cases, a controller action returns a ViewResult.</span></span> <span data-ttu-id="e13b0-150">예를 들어 인덱스 컨트롤러 작업 목록 2에서는 ViewResult를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-150">For example, the Index controller action in Listing 2 returns a ViewResult.</span></span>

<span data-ttu-id="e13b0-151">**2-Controllers\BookController.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="e13b0-151">**Listing 2 - Controllers\BookController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample2.vb)]

<span data-ttu-id="e13b0-152">액션을 ViewResult 반환 될 때 HTML 브라우저에 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-152">When an action returns a ViewResult, HTML is returned to the browser.</span></span> <span data-ttu-id="e13b0-153">목록 2에서 index () 메서드는 브라우저에 인덱스를 명명 된 뷰를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-153">The Index() method in Listing 2 returns a view named Index to the browser.</span></span>

<span data-ttu-id="e13b0-154">목록 2에서 index () 작업을 ViewResult() 반환 하지 않음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-154">Notice that the Index() action in Listing 2 does not return a ViewResult().</span></span> <span data-ttu-id="e13b0-155">대신, 기본 컨트롤러 클래스의 View() 메서드 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-155">Instead, the View() method of the Controller base class is called.</span></span> <span data-ttu-id="e13b0-156">일반적으로 작업 결과 직접 돌아가지 않으면.</span><span class="sxs-lookup"><span data-stu-id="e13b0-156">Normally, you do not return an action result directly.</span></span> <span data-ttu-id="e13b0-157">대신, 호출 기본 컨트롤러 클래스의 다음 메서드 중 하나:</span><span class="sxs-lookup"><span data-stu-id="e13b0-157">Instead, you call one of the following methods of the Controller base class:</span></span>

1. <span data-ttu-id="e13b0-158">보기-ViewResult 작업 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-158">View - Returns a ViewResult action result.</span></span>
2. <span data-ttu-id="e13b0-159">리디렉션-된 RedirectResult 작업 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-159">Redirect - Returns a RedirectResult action result.</span></span>
3. <span data-ttu-id="e13b0-160">RedirectToAction-RedirectToRouteResult 작업 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-160">RedirectToAction - Returns a RedirectToRouteResult action result.</span></span>
4. <span data-ttu-id="e13b0-161">RedirectToRoute-RedirectToRouteResult 작업 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-161">RedirectToRoute - Returns a RedirectToRouteResult action result.</span></span>
5. <span data-ttu-id="e13b0-162">Json-JsonResult 작업 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-162">Json - Returns a JsonResult action result.</span></span>
6. <span data-ttu-id="e13b0-163">JavaScriptResult-JavaScriptResult를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-163">JavaScriptResult - Returns a JavaScriptResult.</span></span>
7. <span data-ttu-id="e13b0-164">콘텐츠-ContentResult 작업 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-164">Content - Returns a ContentResult action result.</span></span>
8. <span data-ttu-id="e13b0-165">파일-반환 FileContentResult, FilePathResult, 또는 매개 변수에 따라 FileStreamResult 메서드에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-165">File - Returns a FileContentResult, FilePathResult, or FileStreamResult depending on the parameters passed to the method.</span></span>

<span data-ttu-id="e13b0-166">따라서 브라우저에 뷰를 반환 하려는 경우에 View() 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-166">So, if you want to return a View to the browser, you call the View() method.</span></span> <span data-ttu-id="e13b0-167">다른 하나의 컨트롤러 작업에서 사용자를 리디렉션하 하려는 경우 RedirectToAction() 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-167">If you want to redirect the user from one controller action to another, you call the RedirectToAction() method.</span></span> <span data-ttu-id="e13b0-168">예를 들어 목록 3에서 Details() 작업으로 표시 또는 Id 매개 변수 값에 있는지 여부에 따라 index () 작업에 사용자를 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-168">For example, the Details() action in Listing 3 either displays a view or redirects the user to the Index() action depending on whether the Id parameter has a value.</span></span>

<span data-ttu-id="e13b0-169">**3-CustomerController.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="e13b0-169">**Listing 3 - CustomerController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample3.vb)]

<span data-ttu-id="e13b0-170">ContentResult 작업 결과은 특별 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-170">The ContentResult action result is special.</span></span> <span data-ttu-id="e13b0-171">일반 텍스트로 된 작업 결과를 반환할 ContentResult 작업 결과 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-171">You can use the ContentResult action result to return an action result as plain text.</span></span> <span data-ttu-id="e13b0-172">예를 들어, 4에서 index () 메서드는 일반 텍스트와 HTML 아니라 메시지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-172">For example, the Index() method in Listing 4 returns a message as plain text and not as HTML.</span></span>

<span data-ttu-id="e13b0-173">**4-Controllers\StatusController.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="e13b0-173">**Listing 4 - Controllers\StatusController.vb**</span></span>

> <span data-ttu-id="e13b0-174">StatusController</span><span class="sxs-lookup"><span data-stu-id="e13b0-174">StatusController</span></span>
> 
> 
> <span data-ttu-id="e13b0-175">System.Web.Mvc.Controller</span><span class="sxs-lookup"><span data-stu-id="e13b0-175">System.Web.Mvc.Controller</span></span>


[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample4.vb)]

<span data-ttu-id="e13b0-176">StatusController.Index() 작업이 호출 되 면 뷰를 반환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-176">When the StatusController.Index() action is invoked, a view is not returned.</span></span> <span data-ttu-id="e13b0-177">대신 원시 텍스트 "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="e13b0-177">Instead, the raw text "Hello World!"</span></span> <span data-ttu-id="e13b0-178">브라우저에 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-178">is returned to the browser.</span></span>

<span data-ttu-id="e13b0-179">컨트롤러 작업 결과 작업 결과 없습니다-예를 들어, 날짜 또는-정수를 반환 하는 경우 다음 결과에 래핑됩니다 ContentResult를 자동으로.</span><span class="sxs-lookup"><span data-stu-id="e13b0-179">If a controller action returns a result that is not an action result - for example, a date or an integer - then the result is wrapped in a ContentResult automatically.</span></span> <span data-ttu-id="e13b0-180">예를 들어, index () 작업 목록 5에서 WorkController 호출 되 면 날짜도 반환 됩니다 ContentResult를 자동으로.</span><span class="sxs-lookup"><span data-stu-id="e13b0-180">For example, when the Index() action of the WorkController in Listing 5 is invoked, the date is returned as a ContentResult automatically.</span></span>

<span data-ttu-id="e13b0-181">**5-WorkController.vb 나열**</span><span class="sxs-lookup"><span data-stu-id="e13b0-181">**Listing 5 - WorkController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample5.vb)]

<span data-ttu-id="e13b0-182">목록 5에서 index () 작업에는 DateTime 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-182">The Index() action in Listing 5 returns a DateTime object.</span></span> <span data-ttu-id="e13b0-183">ASP.NET MVC 프레임 워크 DateTime 개체를 문자열로 변환 하 고는 ContentResult에 DateTime 값을 자동으로 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-183">The ASP.NET MVC framework converts the DateTime object to a string and wraps the DateTime value in a ContentResult automatically.</span></span> <span data-ttu-id="e13b0-184">브라우저에는 날짜 및 시간을 일반 텍스트로 받습니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-184">The browser receives the date and time as plain text.</span></span>

## <a name="summary"></a><span data-ttu-id="e13b0-185">요약</span><span class="sxs-lookup"><span data-stu-id="e13b0-185">Summary</span></span>

<span data-ttu-id="e13b0-186">이 자습서의 목적은 ASP.NET MVC 컨트롤러, 컨트롤러 작업 및 컨트롤러 작업 결과의 개념을 소개 하는 것 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-186">The purpose of this tutorial was to introduce you to the concepts of ASP.NET MVC controllers, controller actions, and controller action results.</span></span> <span data-ttu-id="e13b0-187">첫 번째 섹션에서는 ASP.NET MVC 프로젝트에 새 컨트롤러를 추가 하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-187">In the first section, you learned how to add new controllers to an ASP.NET MVC project.</span></span> <span data-ttu-id="e13b0-188">다음으로, 컨트롤러의 메서드를 공개 하는 방법을 알아보았습니다 우주 컨트롤러 작업으로 노출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-188">Next, you learned how public methods of a controller are exposed to the universe as controller actions.</span></span> <span data-ttu-id="e13b0-189">마지막으로, 다양 한 컨트롤러 작업에서 반환 될 수 있는 작업 결과 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-189">Finally, we discussed the different types of action results that can be returned from a controller action.</span></span> <span data-ttu-id="e13b0-190">특히 ViewResult 고 RedirectToActionResult, ContentResult 컨트롤러 작업에서 반환 하는 방법에 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e13b0-190">In particular, we discussed how to return a ViewResult, RedirectToActionResult, and ContentResult from a controller action.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e13b0-191">[이전](creating-a-custom-route-constraint-cs.md)
> [다음](creating-custom-routes-vb.md)</span><span class="sxs-lookup"><span data-stu-id="e13b0-191">[Previous](creating-a-custom-route-constraint-cs.md)
[Next](creating-custom-routes-vb.md)</span></span>
