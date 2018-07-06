---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs
title: ASP.NET MVC 라우팅 개요 (C#) | Microsoft Docs
author: StephenWalther
description: 이 자습서에서는 Stephen walther가 ASP.NET MVC 프레임 워크에 브라우저 요청이 컨트롤러 작업에 매핑하는 방법 보여 줍니다.
ms.author: aspnetcontent
ms.date: 08/19/2008
ms.assetid: 5b39d2d5-4bf9-4d04-94c7-81b84dfeeb31
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs
msc.type: authoredcontent
ms.openlocfilehash: 2b43c3dca1587d79a60c5a89a451dda989403d56
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37819149"
---
<a name="aspnet-mvc-routing-overview-c"></a><span data-ttu-id="b0f78-103">ASP.NET MVC 라우팅 개요 (C#)</span><span class="sxs-lookup"><span data-stu-id="b0f78-103">ASP.NET MVC Routing Overview (C#)</span></span>
====================
<span data-ttu-id="b0f78-104">[Stephen walther가](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="b0f78-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="b0f78-105">이 자습서에서는 Stephen walther가 ASP.NET MVC 프레임 워크에 브라우저 요청이 컨트롤러 작업에 매핑하는 방법 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-105">In this tutorial, Stephen Walther shows how the ASP.NET MVC framework maps browser requests to controller actions.</span></span>


<span data-ttu-id="b0f78-106">이 자습서에서는 호출 하는 모든 ASP.NET MVC 응용 프로그램의 중요 한 기능에 도입 된 *ASP.NET 라우팅에서*합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-106">In this tutorial, you are introduced to an important feature of every ASP.NET MVC application called *ASP.NET Routing*.</span></span> <span data-ttu-id="b0f78-107">ASP.NET 라우팅 모듈은 들어오는 브라우저 요청을 특정 MVC 컨트롤러 작업에 매핑하는 일을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-107">The ASP.NET Routing module is responsible for mapping incoming browser requests to particular MVC controller actions.</span></span> <span data-ttu-id="b0f78-108">이 자습서를 마치면 표준 경로 테이블 요청 컨트롤러 작업에 매핑하는 방법을 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-108">By the end of this tutorial, you will understand how the standard route table maps requests to controller actions.</span></span>

## <a name="using-the-default-route-table"></a><span data-ttu-id="b0f78-109">기본 경로 테이블을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="b0f78-109">Using the Default Route Table</span></span>

<span data-ttu-id="b0f78-110">새 ASP.NET MVC 응용 프로그램을 만들 때 응용 프로그램이 ASP.NET 라우팅을 사용 하도록 이미 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-110">When you create a new ASP.NET MVC application, the application is already configured to use ASP.NET Routing.</span></span> <span data-ttu-id="b0f78-111">ASP.NET 라우팅이 두 위치에서 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-111">ASP.NET Routing is setup in two places.</span></span>

<span data-ttu-id="b0f78-112">먼저 ASP.NET 라우팅 응용 프로그램의 웹 구성 파일 (web.config)에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-112">First, ASP.NET Routing is enabled in your application's Web configuration file (Web.config file).</span></span> <span data-ttu-id="b0f78-113">라우팅과 관련 된 구성 파일에서 4 개의 섹션이 있습니다: system.web.httpModules 섹션, system.web.httpHandlers 섹션, system.webserver.modules 섹션 및 system.webserver.handlers 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-113">There are four sections in the configuration file that are relevant to routing: the system.web.httpModules section, the system.web.httpHandlers section, the system.webserver.modules section, and the system.webserver.handlers section.</span></span> <span data-ttu-id="b0f78-114">이 섹션에서는 없이 라우팅 더 이상 작동 하기 때문에 이러한 섹션을 삭제 하지 않도록 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-114">Be careful not to delete these sections because without these sections routing will no longer work.</span></span>

<span data-ttu-id="b0f78-115">둘째, 및 무엇 보다도 응용 프로그램의 Global.asax 파일에 경로 테이블을 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-115">Second, and more importantly, a route table is created in the application's Global.asax file.</span></span> <span data-ttu-id="b0f78-116">Global.asax 파일은 ASP.NET 응용 프로그램 수명 주기 이벤트에 대 한 이벤트 처리기를 포함 하는 특수 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-116">The Global.asax file is a special file that contains event handlers for ASP.NET application lifecycle events.</span></span> <span data-ttu-id="b0f78-117">경로 테이블 응용 프로그램 시작 이벤트를 사용 하는 동안 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-117">The route table is created during the Application Start event.</span></span>

<span data-ttu-id="b0f78-118">목록 1에서 파일을 ASP.NET MVC 응용 프로그램에 대 한 기본 Global.asax 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-118">The file in Listing 1 contains the default Global.asax file for an ASP.NET MVC application.</span></span>

<span data-ttu-id="b0f78-119">**1-Global.asax.cs를 나열합니다.**</span><span class="sxs-lookup"><span data-stu-id="b0f78-119">**Listing 1 - Global.asax.cs**</span></span>

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample1.cs)]

<span data-ttu-id="b0f78-120">MVC 응용 프로그램을 처음 시작 되 면 응용 프로그램\_start () 메서드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-120">When an MVC application first starts, the Application\_Start() method is called.</span></span> <span data-ttu-id="b0f78-121">이 메서드는 차례로 RegisterRoutes() 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-121">This method, in turn, calls the RegisterRoutes() method.</span></span> <span data-ttu-id="b0f78-122">RegisterRoutes() 메서드는 경로 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-122">The RegisterRoutes() method creates the route table.</span></span>

<span data-ttu-id="b0f78-123">기본 경로 테이블 (Default 라는)를 단일 경로 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-123">The default route table contains a single route (named Default).</span></span> <span data-ttu-id="b0f78-124">기본 경로 매핑되는 URL의 첫 번째 세그먼트 컨트롤러 이름, 컨트롤러 작업에 대 한 URL의 세그먼트를 두 번째 및 세 번째 세그먼트 라는 매개 변수에 **id**합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-124">The Default route maps the first segment of a URL to a controller name, the second segment of a URL to a controller action, and the third segment to a parameter named **id**.</span></span>

<span data-ttu-id="b0f78-125">Imagine 웹 브라우저의 주소 표시줄에 다음 URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-125">Imagine that you enter the following URL into your web browser's address bar:</span></span>

<span data-ttu-id="b0f78-126">/ 홈/인덱스/3</span><span class="sxs-lookup"><span data-stu-id="b0f78-126">/Home/Index/3</span></span>

<span data-ttu-id="b0f78-127">기본 경로 다음 매개 변수를이 URL을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-127">The Default route maps this URL to the following parameters:</span></span>

- <span data-ttu-id="b0f78-128">컨트롤러 = 홈</span><span class="sxs-lookup"><span data-stu-id="b0f78-128">controller = Home</span></span>

- <span data-ttu-id="b0f78-129">작업 = 인덱스</span><span class="sxs-lookup"><span data-stu-id="b0f78-129">action = Index</span></span>

- <span data-ttu-id="b0f78-130">id = 3</span><span class="sxs-lookup"><span data-stu-id="b0f78-130">id = 3</span></span>

<span data-ttu-id="b0f78-131">URL /Home/인덱스/3을 요청 하면 다음 코드가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-131">When you request the URL /Home/Index/3, the following code is executed:</span></span>

<span data-ttu-id="b0f78-132">HomeController.Index(3)</span><span class="sxs-lookup"><span data-stu-id="b0f78-132">HomeController.Index(3)</span></span>

<span data-ttu-id="b0f78-133">기본 경로 세 매개 변수 모두에 대 한 기본값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-133">The Default route includes defaults for all three parameters.</span></span> <span data-ttu-id="b0f78-134">컨트롤러를 지정 하지 않으면, 다음 컨트롤러 매개 변수 기본값 **홈**합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-134">If you don't supply a controller, then the controller parameter defaults to the value **Home**.</span></span> <span data-ttu-id="b0f78-135">Action 매개 변수 값 작업을 지정 하지 않으면 경우 기본값으로 **인덱스**합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-135">If you don't supply an action, the action parameter defaults to the value **Index**.</span></span> <span data-ttu-id="b0f78-136">마지막으로 id를 제공 하지 않으면 id 매개 변수 기본값은 빈 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-136">Finally, if you don't supply an id, the id parameter defaults to an empty string.</span></span>

<span data-ttu-id="b0f78-137">기본 경로 Url 컨트롤러 작업에 매핑하는 방법의 몇 가지 예를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-137">Let's look at a few examples of how the Default route maps URLs to controller actions.</span></span> <span data-ttu-id="b0f78-138">브라우저 주소 표시줄에 다음 URL을 입력 하는 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-138">Imagine that you enter the following URL into your browser address bar:</span></span>

<span data-ttu-id="b0f78-139">/ 홈</span><span class="sxs-lookup"><span data-stu-id="b0f78-139">/Home</span></span>

<span data-ttu-id="b0f78-140">기본 경로 매개 변수 기본값을 때문에이 URL을 입력 하면 HomeController 클래스의 index () 메서드를 호출할 목록 2.</span><span class="sxs-lookup"><span data-stu-id="b0f78-140">Because of the Default route parameter defaults, entering this URL will cause the Index() method of the HomeController class in Listing 2 to be called.</span></span>

<span data-ttu-id="b0f78-141">**2-HomeController.cs 나열**</span><span class="sxs-lookup"><span data-stu-id="b0f78-141">**Listing 2 - HomeController.cs**</span></span>

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample2.cs)]

<span data-ttu-id="b0f78-142">목록 2 HomeController 클래스 id 라는 이름의 단일 매개 변수를 허용 하는 index () 메서드가 포함 됩니다. URL /Home index () 메서드를 Id 매개 변수 값으로 빈 문자열을 사용 하 여 호출 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-142">In Listing 2, the HomeController class includes a method named Index() that accepts a single parameter named Id. The URL /Home causes the Index() method to be called with an empty string as the value of the Id parameter.</span></span>

<span data-ttu-id="b0f78-143">MVC 프레임 워크 컨트롤러 작업을 호출 하는 방식으로 인해 URL /Home index () 메서드의 목록 3에서 HomeController 클래스와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-143">Because of the way that the MVC framework invokes controller actions, the URL /Home also matches the Index() method of the HomeController class in Listing 3.</span></span>

<span data-ttu-id="b0f78-144">**3-HomeController.cs (매개 변수가 없는 인덱스 작업)를 나열합니다.**</span><span class="sxs-lookup"><span data-stu-id="b0f78-144">**Listing 3 - HomeController.cs (Index action with no parameter)**</span></span>

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample3.cs)]

<span data-ttu-id="b0f78-145">보기 3의 index () 메서드는 매개 변수를 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-145">The Index() method in Listing 3 does not accept any parameters.</span></span> <span data-ttu-id="b0f78-146">URL /Home가 index () 메서드를 호출 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-146">The URL /Home will cause this Index() method to be called.</span></span> <span data-ttu-id="b0f78-147">또한 URL /Home/인덱스/3 (Id 무시 됨)이이 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-147">The URL /Home/Index/3 also invokes this method (the Id is ignored).</span></span>

<span data-ttu-id="b0f78-148">또한 URL /Home 4에서 HomeController 클래스의 index () 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-148">The URL /Home also matches the Index() method of the HomeController class in Listing 4.</span></span>

<span data-ttu-id="b0f78-149">**4-HomeController.cs (nullable 매개 변수를 사용 하 여 인덱스 작업)를 나열합니다.**</span><span class="sxs-lookup"><span data-stu-id="b0f78-149">**Listing 4 - HomeController.cs (Index action with nullable parameter)**</span></span>

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample4.cs)]

<span data-ttu-id="b0f78-150">목록 4 index () 메서드에는 정수에 대 한 매개 변수를 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-150">In Listing 4, the Index() method has one Integer parameter.</span></span> <span data-ttu-id="b0f78-151">매개 변수 (Null 값을 가질 수 있음) nullable 매개 변수 이기 때문에 오류가 발생 하지는 index ()는 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-151">Because the parameter is a nullable parameter (can have the value Null), the Index() can be called without raising an error.</span></span>

<span data-ttu-id="b0f78-152">마지막으로, URL /Home를 사용 하 여 목록 5에서 index () 메서드를 호출 하면 예외가 발생 이후 Id 매개 변수에 *아닙니다* nullable 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-152">Finally, invoking the Index() method in Listing 5 with the URL /Home causes an exception since the Id parameter *is not* a nullable parameter.</span></span> <span data-ttu-id="b0f78-153">Index () 메서드를 호출 하려고 하면 다음 오류가 발생 하면 그림 1에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-153">If you attempt to invoke the Index() method then you get the error displayed in Figure 1.</span></span>

<span data-ttu-id="b0f78-154">**5-HomeController.cs (Id 매개 변수를 사용 하 여 인덱스 작업)를 나열합니다.**</span><span class="sxs-lookup"><span data-stu-id="b0f78-154">**Listing 5 - HomeController.cs (Index action with Id parameter)**</span></span>

[!code-csharp[Main](asp-net-mvc-routing-overview-cs/samples/sample5.cs)]


<span data-ttu-id="b0f78-155">[![매개 변수 값을 필요로 하는 컨트롤러 작업을 호출 합니다.](asp-net-mvc-routing-overview-cs/_static/image1.jpg)](asp-net-mvc-routing-overview-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b0f78-155">[![Invoking a controller action that expects a parameter value](asp-net-mvc-routing-overview-cs/_static/image1.jpg)](asp-net-mvc-routing-overview-cs/_static/image1.png)</span></span>

<span data-ttu-id="b0f78-156">**그림 01**: 매개 변수 값을 필요로 하는 컨트롤러 동작 호출 ([큰 이미지를 보려면 클릭](asp-net-mvc-routing-overview-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="b0f78-156">**Figure 01**: Invoking a controller action that expects a parameter value ([Click to view full-size image](asp-net-mvc-routing-overview-cs/_static/image2.png))</span></span>


<span data-ttu-id="b0f78-157">또한 목록 5에서 인덱스 컨트롤러 작업을 사용 하 여 URL /Home/인덱스/3, 다른 한편으로 잘 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-157">The URL /Home/Index/3, on the other hand, works just fine with the Index controller action in Listing 5.</span></span> <span data-ttu-id="b0f78-158">요청 /Home/Index/3 index () 메서드를 3 값이 있는 Id 매개 변수를 사용 하 여 호출 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-158">The request /Home/Index/3 causes the Index() method to be called with an Id parameter that has the value 3.</span></span>

## <a name="summary"></a><span data-ttu-id="b0f78-159">요약</span><span class="sxs-lookup"><span data-stu-id="b0f78-159">Summary</span></span>

<span data-ttu-id="b0f78-160">이 자습서의 목적은 ASP.NET 라우팅에 대 한 간략 한 소개를 제공 하는 것 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-160">The goal of this tutorial was to provide you with a brief introduction to ASP.NET Routing.</span></span> <span data-ttu-id="b0f78-161">새 ASP.NET MVC 응용 프로그램을 시작 하는 기본 경로 테이블을 검사 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-161">We examined the default route table that you get with a new ASP.NET MVC application.</span></span> <span data-ttu-id="b0f78-162">기본 경로 Url 컨트롤러 작업에 매핑하는 방법 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b0f78-162">You learned how the default route maps URLs to controller actions.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="b0f78-163">다음</span><span class="sxs-lookup"><span data-stu-id="b0f78-163">Next</span></span>](understanding-action-filters-cs.md)
