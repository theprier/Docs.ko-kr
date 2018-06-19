---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
title: URL 라우팅 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈 것에 대 한 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 구축 하는 기초 알려 드리겠습니다 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/08/2014
ms.topic: article
ms.assetid: 4f4bf092-c400-471f-a876-78fda0417890
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
msc.type: authoredcontent
ms.openlocfilehash: a195b36517bcae4bbeaf43fe7386e7787fd00212
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30886435"
---
<a name="url-routing"></a><span data-ttu-id="7d3ec-103">URL 라우팅</span><span class="sxs-lookup"><span data-stu-id="7d3ec-103">URL Routing</span></span>
====================
<span data-ttu-id="7d3ec-104">으로 [Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="7d3ec-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="7d3ec-105">[Wingtip Toys 샘플 프로젝트 (C#)를 다운로드](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자책 (PDF)를 다운로드 합니다.](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="7d3ec-105">[Download Wingtip Toys Sample Project (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="7d3ec-106">이 자습서 시리즈 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 웹에 대 한 ASP.NET Web Forms 응용 프로그램을 구축 하는 기초 알려 드리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="7d3ec-107">Visual Studio 2013 [C# 소스 코드를 사용 하 여 프로젝트](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 이 자습서 시리즈를 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>


<span data-ttu-id="7d3ec-108">이 자습서에서는 URL 라우팅을 지원 하도록 Wingtip Toys 샘플 응용 프로그램을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-108">In this tutorial, you will modify the Wingtip Toys sample application to support URL routing.</span></span> <span data-ttu-id="7d3ec-109">라우팅 친숙 한, 기억 하기 쉽고 검색 엔진에서 더 잘 지원 되는 Url을 사용 하도록 웹 응용을 프로그램 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-109">Routing enables your web application to use URLs that are friendly, easier to remember, and better supported by search engines.</span></span> <span data-ttu-id="7d3ec-110">이 자습서에서는 이전 자습서 "멤버 자격 및 관리"를 바탕으로 하며 Wingtip Toys 자습서 시리즈의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-110">This tutorial builds on the previous tutorial "Membership and Administration" and is part of the Wingtip Toys tutorial series.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="7d3ec-111">학습 내용:</span><span class="sxs-lookup"><span data-stu-id="7d3ec-111">What you'll learn:</span></span>

- <span data-ttu-id="7d3ec-112">ASP.NET Web Forms 응용 프로그램에 대 한 경로 등록 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-112">How to register routes for an ASP.NET Web Forms application.</span></span>
- <span data-ttu-id="7d3ec-113">웹 페이지에 경로 추가 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-113">How to add routes to a web page.</span></span>
- <span data-ttu-id="7d3ec-114">경로 지원 하기 위해 데이터베이스에서 데이터를 선택 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-114">How to select data from a database to support routes.</span></span>

## <a name="aspnet-routing-overview"></a><span data-ttu-id="7d3ec-115">ASP.NET 라우팅 개요</span><span class="sxs-lookup"><span data-stu-id="7d3ec-115">ASP.NET Routing Overview</span></span>

<span data-ttu-id="7d3ec-116">응용 프로그램을 허용 하도록 구성할 수 있습니다 URL 라우팅 요청 Url에서 물리적 파일에 매핑되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-116">URL routing allows you to configure an application to accept request URLs that do not map to physical files.</span></span> <span data-ttu-id="7d3ec-117">요청 URL은 사용자가 웹 사이트에서 페이지를 찾아야 할 브라우저에 입력 URL 단순히입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-117">A request URL is simply the URL a user enters into their browser to find a page on your web site.</span></span> <span data-ttu-id="7d3ec-118">사용자에 게 의미를 가진 되며 검색 엔진 최적화 (SEO) 도움이 될 수 있는 Url 정의 라우팅을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-118">You use routing to define URLs that are semantically meaningful to users and that can help with search-engine optimization (SEO).</span></span>

<span data-ttu-id="7d3ec-119">기본적으로 Web Forms 템플릿은 포함 [ASP.NET Url](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-119">By default, the Web Forms template includes [ASP.NET Friendly URLs](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/).</span></span> <span data-ttu-id="7d3ec-120">사용 하 여 기본 라우팅 작업의 대부분은 구현 될 *친화적 Url*합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-120">Much of the basic routing work will be implemented by using *Friendly URLs*.</span></span> <span data-ttu-id="7d3ec-121">그러나이 자습서에서는 사용자 지정된 라우팅 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-121">However, in this tutorial you will add customized routing capabilities.</span></span>

<span data-ttu-id="7d3ec-122">URL 라우팅와 사용자 지정 하기 전에 Wingtip Toys 샘플 응용 프로그램은 다음 URL을 사용 하 여 제품을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-122">Before customizing URL routing, the Wingtip Toys sample application can link to a product using the following URL:</span></span>

`https://localhost:44300/ProductDetails.aspx?productID=2`

<span data-ttu-id="7d3ec-123">URL 라우팅를 사용자 지정 Wingtip Toys 샘플 응용 프로그램은 보다 읽기 쉽게 URL을 사용 하 여 동일한 제품에 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-123">By customizing URL routing, the Wingtip Toys sample application will link to the same product using an easier to read URL:</span></span>

`https://localhost:44300/Product/Convertible%20Car`

### <a name="routes"></a><span data-ttu-id="7d3ec-124">경로</span><span class="sxs-lookup"><span data-stu-id="7d3ec-124">Routes</span></span>

<span data-ttu-id="7d3ec-125">경로 처리기에 매핑되는 URL 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-125">A route is a URL pattern that is mapped to a handler.</span></span> <span data-ttu-id="7d3ec-126">처리기는 Web Forms 응용 프로그램에서.aspx 파일 등의 물리적 파일을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-126">The handler can be a physical file, such as an .aspx file in a Web Forms application.</span></span> <span data-ttu-id="7d3ec-127">처리기가 요청을 처리 하는 클래스를 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-127">A handler can also be a class that processes the request.</span></span> <span data-ttu-id="7d3ec-128">경로 정의 하려면 URL 패턴, 처리기 및 필요에 따라 경로 대 한 이름을 지정 하 여 경로 클래스의 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-128">To define a route, you create an instance of the Route class by specifying the URL pattern, the handler, and optionally a name for the route.</span></span>

<span data-ttu-id="7d3ec-129">응용 프로그램에 추가 하 여 경로 추가 `Route` 개체를 정적 `Routes` 의 속성은 `RouteTable` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-129">You add the route to the application by adding the `Route` object to the static `Routes` property of the `RouteTable` class.</span></span> <span data-ttu-id="7d3ec-130">경로 속성은 한 `RouteCollection` 응용 프로그램에 대 한 모든 경로 저장 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-130">The Routes property is a `RouteCollection` object that stores all the routes for the application.</span></span>

### <a name="url-patterns"></a><span data-ttu-id="7d3ec-131">URL 패턴</span><span class="sxs-lookup"><span data-stu-id="7d3ec-131">URL Patterns</span></span>

<span data-ttu-id="7d3ec-132">URL 패턴에는 리터럴 값 및 변수 자리 표시자 (URL 매개 변수 라고 함)이 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-132">A URL pattern can contain literal values and variable placeholders (referred to as URL parameters).</span></span> <span data-ttu-id="7d3ec-133">리터럴 및 자리 표시자는 슬래시로 구분 된 URL의 세그먼트에 있습니다 (`/`) 문자.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-133">The literals and placeholders are located in segments of the URL which are delimited by the slash (`/`) character.</span></span>

<span data-ttu-id="7d3ec-134">에 웹 응용 프로그램에 요청이 수행 될 때에 URL 세그먼트 및 자리 표시자로 구문 분석 되 고 변수 값 요청 처리기에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-134">When a request to your web application is made, the URL is parsed into segments and placeholders, and the variable values are provided to the request handler.</span></span> <span data-ttu-id="7d3ec-135">이 프로세스는 쿼리 문자열의 데이터를 구문 분석 되 고 요청 처리기에 전달 하는 방식과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-135">This process is similar to the way the data in a query string is parsed and passed to the request handler.</span></span> <span data-ttu-id="7d3ec-136">두 경우 모두 변수 정보는 URL에 포함 되어 있으며 키-값 쌍의 형태로 처리기에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-136">In both cases, variable information is included in the URL and passed to the handler in the form of key-value pairs.</span></span> <span data-ttu-id="7d3ec-137">쿼리 문자열에 대 한 키 및 값이 모두 URL에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-137">For query strings, both the keys and the values are in the URL.</span></span> <span data-ttu-id="7d3ec-138">경로 대 한 키는 URL 패턴에 정의 된 자리 표시자 이름 및 값만 URL에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-138">For routes, the keys are the placeholder names defined in the URL pattern, and only the values are in the URL.</span></span>

<span data-ttu-id="7d3ec-139">URL 패턴에 자리 표시자를 정의 중괄호로 묶어 ( `{` 및 `}` ).</span><span class="sxs-lookup"><span data-stu-id="7d3ec-139">In a URL pattern, you define placeholders by enclosing them in braces ( `{` and `}` ).</span></span> <span data-ttu-id="7d3ec-140">둘 이상의 자리 표시자를 세그먼트에 정의할 수 있지만 자리 표시자를 리터럴 값으로 구분 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-140">You can define more than one placeholder in a segment, but the placeholders must be separated by a literal value.</span></span> <span data-ttu-id="7d3ec-141">예를 들어 `{language}-{country}/{action}` 유효한 경로 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-141">For example, `{language}-{country}/{action}` is a valid route pattern.</span></span> <span data-ttu-id="7d3ec-142">그러나 `{language}{country}/{action}` 없는 리터럴 값 또는 자리 표시자 사이의 구분 기호 이므로 유효한 패턴이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-142">However, `{language}{country}/{action}` is not a valid pattern, because there is no literal value or delimiter between the placeholders.</span></span> <span data-ttu-id="7d3ec-143">따라서 라우팅 국가 자리 표시자에 대 한 언어 자리 표시자에 대 한 값에서 값을 구분할 수 있는 위치를 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-143">Therefore, routing cannot determine where to separate the value for the language placeholder from the value for the country placeholder.</span></span>

### <a name="mapping-and-registering-routes"></a><span data-ttu-id="7d3ec-144">매핑 및 경로 등록 하는 중</span><span class="sxs-lookup"><span data-stu-id="7d3ec-144">Mapping and Registering Routes</span></span>

<span data-ttu-id="7d3ec-145">Wingtip Toys 샘플 응용 프로그램의 페이지에 대 한 경로 포함할 수 있습니다, 전에 응용 프로그램이 시작 경로 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-145">Before you can include routes to pages of the Wingtip Toys sample application, you must register the routes when the application starts.</span></span> <span data-ttu-id="7d3ec-146">수정 하는 경로 등록 하려면는 `Application_Start` 이벤트 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-146">To register the routes, you will modify the `Application_Start` event handler.</span></span>

1. <span data-ttu-id="7d3ec-147">**솔루션 탐색기**Visual Studio의 찾기 및 열기는 *Global.asax.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-147">In **Solution Explorer**of Visual Studio, find and open the *Global.asax.cs* file.</span></span>
2. <span data-ttu-id="7d3ec-148">노란색으로 강조 표시 된 코드를 추가 *Global.asax.cs* 다음과 같이 파일:</span><span class="sxs-lookup"><span data-stu-id="7d3ec-148">Add the code highlighted in yellow to the *Global.asax.cs* file as follows:</span></span>   

    [!code-csharp[Main](url-routing/samples/sample1.cs?highlight=30-31,34-46)]

<span data-ttu-id="7d3ec-149">Wingtip Toys 샘플 응용 프로그램 시작 되 면 호출 하는 `Application_Start` 이벤트 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-149">When the Wingtip Toys sample application starts, it calls the `Application_Start` event handler.</span></span> <span data-ttu-id="7d3ec-150">이 이벤트 처리기의 끝에는 `RegisterCustomRoutes` 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-150">At the end of this event handler, the `RegisterCustomRoutes` method is called.</span></span> <span data-ttu-id="7d3ec-151">`RegisterCustomRoutes` 메서드를 호출 하 여 각 경로 추가 `MapPageRoute` 의 메서드는 `RouteCollection` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-151">The `RegisterCustomRoutes` method adds each route by calling the `MapPageRoute` method of the `RouteCollection` object.</span></span> <span data-ttu-id="7d3ec-152">경로 경로 URL 및 실제 URL 경로 이름을 사용 하 여 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-152">Routes are defined using a route name, a route URL and a physical URL.</span></span>

<span data-ttu-id="7d3ec-153">첫 번째 매개 변수 ("`ProductsByCategoryRoute`")의 경로 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-153">The first parameter ("`ProductsByCategoryRoute`") is the route name.</span></span> <span data-ttu-id="7d3ec-154">필요할 때 경로 호출 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-154">It is used to call the route when it is needed.</span></span> <span data-ttu-id="7d3ec-155">두 번째 매개 변수 ("`Category/{categoryName}`") 친숙 한 대체 코드에 따라 동적 일 수 있는 URL을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-155">The second parameter ("`Category/{categoryName}`") defines the friendly replacement URL that can be dynamic based on code.</span></span> <span data-ttu-id="7d3ec-156">데이터를 기반으로 생성 되는 링크와 함께 데이터 컨트롤을 채우는 경우에이 경로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-156">You use this route when you are populating a data control with links that are generated based on data.</span></span> <span data-ttu-id="7d3ec-157">경로 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-157">A route is shown as follows:</span></span>

[!code-csharp[Main](url-routing/samples/sample2.cs)]

<span data-ttu-id="7d3ec-158">중괄호로 지정 된 동적 값을 포함 하는 경로 두 번째 매개 변수 (`{ }`).</span><span class="sxs-lookup"><span data-stu-id="7d3ec-158">The second parameter of the route includes a dynamic value specified by braces (`{ }`).</span></span> <span data-ttu-id="7d3ec-159">이 경우에 `categoryName` 적절 한 라우팅 경로 확인 하는 데 사용 될 하는 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-159">In this case, the `categoryName` is a variable that will be used to determine the proper routing path.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="7d3ec-160">**선택 사항**</span><span class="sxs-lookup"><span data-stu-id="7d3ec-160">**Optional**</span></span>
> 
> <span data-ttu-id="7d3ec-161">이동 하 여 코드를 관리 하는 더 쉽게 진행할 수 있습니다는 `RegisterCustomRoutes` 메서드를 별도 클래스.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-161">You might find it easier to manage your code by moving the `RegisterCustomRoutes` method to a separate class.</span></span> <span data-ttu-id="7d3ec-162">에 *논리* 폴더를 만들려면 별도 `RouteActions` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-162">In the *Logic* folder, create a separate `RouteActions` class.</span></span> <span data-ttu-id="7d3ec-163">위의 이동 `RegisterCustomRoutes` 에서 메서드는 *Global.asax.cs* 새 파일 `RoutesActions` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-163">Move the above `RegisterCustomRoutes` method from the *Global.asax.cs* file into the new `RoutesActions` class.</span></span> <span data-ttu-id="7d3ec-164">사용 하 여는 `RoleActions` 클래스 및 `createAdmin` 메서드를 호출 하는 방법의 예로 `RegisterCustomRoutes` 에서 메서드는 *Global.asax.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-164">Use the `RoleActions` class and the `createAdmin` method as an example of how to call the `RegisterCustomRoutes` method from the *Global.asax.cs* file.</span></span>


<span data-ttu-id="7d3ec-165">또한 단어로 `RegisterRoutes` 사용 하 여 메서드 호출은 `RouteConfig` 맨 앞에 개체는 `Application_Start` 이벤트 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-165">You may also have noticed the `RegisterRoutes` method call using the `RouteConfig` object at the beginning of the `Application_Start` event handler.</span></span> <span data-ttu-id="7d3ec-166">기본 라우팅을 구현 하기 위해 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-166">This call is made to implement default routing.</span></span> <span data-ttu-id="7d3ec-167">Visual Studio Web Forms 템플릿을 사용 하 여 응용 프로그램을 만들 때에 기본 코드와 포함 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-167">It was included as default code when you created the application using Visual Studio's Web Forms template.</span></span>

## <a name="retrieving-and-using-route-data"></a><span data-ttu-id="7d3ec-168">검색 및 경로 데이터를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="7d3ec-168">Retrieving and Using Route Data</span></span>

<span data-ttu-id="7d3ec-169">위에서 설명한 대로 경로 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-169">As mentioned above, routes can be defined.</span></span> <span data-ttu-id="7d3ec-170">에 추가 하는 코드는 `Application_Start` 의 이벤트 처리기는 *Global.asax.cs* 파일 정의할 수 있는 경로 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-170">The code that you added to the `Application_Start` event handler in the *Global.asax.cs* file loads the definable routes.</span></span>

### <a name="setting-routes"></a><span data-ttu-id="7d3ec-171">경로 설정</span><span class="sxs-lookup"><span data-stu-id="7d3ec-171">Setting Routes</span></span>

<span data-ttu-id="7d3ec-172">경로 다른 코드를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-172">Routes require you to add additional code.</span></span> <span data-ttu-id="7d3ec-173">이 자습서를 사용 하 여 모델 바인딩을 검색 하는 `RouteValueDictionary` 데이터 컨트롤에서 데이터를 사용 하 여 경로 생성할 때 사용 되는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-173">In this tutorial, you will use model binding to retrieve a `RouteValueDictionary` object that is used when generating the routes using data from a data control.</span></span> <span data-ttu-id="7d3ec-174">`RouteValueDictionary` 개체에는 제품의 특정 범주에 속하는 제품 이름 목록이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-174">The `RouteValueDictionary` object will contain a list of product names that belong to a specific category of products.</span></span> <span data-ttu-id="7d3ec-175">데이터 및 경로에 따라 각 제품에 대 한 연결이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-175">A link is created for each product based on the data and route.</span></span>

#### <a name="enable-routes-for-categories-and-products"></a><span data-ttu-id="7d3ec-176">범주 및 제품에 대 한 경로 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="7d3ec-176">Enable Routes for Categories and Products</span></span>

<span data-ttu-id="7d3ec-177">다음에 사용 하도록 응용 프로그램 업데이트는 `ProductsByCategoryRoute` 포함할 각 제품 범주 링크에 대 한 올바른 경로를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-177">Next, you'll update the application to use the `ProductsByCategoryRoute` to determine the correct route to include for each product category link.</span></span> <span data-ttu-id="7d3ec-178">도 업데이트는 *ProductList.aspx* 각 제품에 대 한 라우팅된 링크를 포함 하는 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-178">You'll also update the *ProductList.aspx* page to include a routed link for each product.</span></span> <span data-ttu-id="7d3ec-179">링크 표시 됩니다,이 변경 되기 전의 있지만 링크 URL 라우팅을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-179">The links will be displayed as they were before the change, however the links will now use URL routing.</span></span>

1. <span data-ttu-id="7d3ec-180">**솔루션 탐색기**열고는 *Site.Master* 페이지 아직 열지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-180">In **Solution Explorer**, open the *Site.Master* page if it is not already open.</span></span>
2. <span data-ttu-id="7d3ec-181">업데이트는 **ListView** 라는 컨트롤 "`categoryList`" 노란색으로 강조 표시를 변경 하므로 태그를 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-181">Update the **ListView** control named "`categoryList`" with the changes highlighted in yellow, so the markup appears as follows:</span></span>   

    [!code-aspx[Main](url-routing/samples/sample3.aspx?highlight=7-9)]
3. <span data-ttu-id="7d3ec-182">**솔루션 탐색기**열고는 *ProductList.aspx* 페이지.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-182">In **Solution Explorer**, open the *ProductList.aspx* page.</span></span>
4. <span data-ttu-id="7d3ec-183">업데이트는 `ItemTemplate` 의 요소는 *ProductList.aspx* 태그를 다음과 같이 나타나도록 노란색으로 강조 하는 업데이트 된 페이지:</span><span class="sxs-lookup"><span data-stu-id="7d3ec-183">Update the `ItemTemplate` element of the *ProductList.aspx* page with the updates highlighted in yellow, so the markup appears as follows:</span></span>   

    [!code-aspx[Main](url-routing/samples/sample4.aspx?highlight=6-9,14-16)]
5. <span data-ttu-id="7d3ec-184">관련 코드를 열고 *ProductList.aspx.cs* 에 강조 표시 된 노란색으로 다음 네임 스페이스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-184">Open the code-behind of *ProductList.aspx.cs* and add the following namespace as highlighted in yellow:</span></span>  

    [!code-csharp[Main](url-routing/samples/sample5.cs?highlight=9)]
6. <span data-ttu-id="7d3ec-185">대체는 `GetProducts` 코드 숨김의 메서드 (*ProductList.aspx.cs*)를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="7d3ec-185">Replace the `GetProducts` method of the code-behind (*ProductList.aspx.cs*) with the following code:</span></span>   

    [!code-csharp[Main](url-routing/samples/sample6.cs)]

#### <a name="add-code-for-product-details"></a><span data-ttu-id="7d3ec-186">제품 세부 정보에 대 한 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-186">Add Code for Product Details</span></span>

<span data-ttu-id="7d3ec-187">이제, 관련 코드를 업데이트 (*ProductDetails.aspx.cs*)에 대 한는 *ProductDetails.aspx* 경로 데이터를 사용 하는 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-187">Now, update the code-behind (*ProductDetails.aspx.cs*) for the *ProductDetails.aspx* page to use route data.</span></span> <span data-ttu-id="7d3ec-188">새 `GetProduct` 메서드도 이전 비 친화적인, 라우팅되지 않은 URL을 사용 하는 사용자에 책갈피가 표시 된 링크 된 경우에 대 한 쿼리 문자열 값을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-188">Notice that the new `GetProduct` method also accepts a query string value for the case where the user has a link bookmarked that uses the older non-friendly, non-routed URL.</span></span>

1. <span data-ttu-id="7d3ec-189">대체는 `GetProduct` 코드 숨김의 메서드 (*ProductDetails.aspx.cs*)를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="7d3ec-189">Replace the `GetProduct` method of the code-behind (*ProductDetails.aspx.cs*) with the following code:</span></span>   

    [!code-csharp[Main](url-routing/samples/sample7.cs)]

## <a name="running-the-application"></a><span data-ttu-id="7d3ec-190">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="7d3ec-190">Running the Application</span></span>

<span data-ttu-id="7d3ec-191">업데이트 된 경로 볼 수 있는 지금 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-191">You can run the application now to see the updated routes.</span></span>

1. <span data-ttu-id="7d3ec-192">키를 눌러 **F5** Wingtip Toys 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-192">Press **F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="7d3ec-193">브라우저가 열리고 표시는 *Default.aspx* 페이지.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-193">The browser opens and shows the *Default.aspx* page.</span></span>
2. <span data-ttu-id="7d3ec-194">클릭는 **제품** 페이지 맨 아래에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-194">Click the **Products** link at the top of the page.</span></span>  
 <span data-ttu-id="7d3ec-195">모든 제품에 표시 되는 *ProductList.aspx* 페이지.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-195">All products are displayed on the *ProductList.aspx* page.</span></span> <span data-ttu-id="7d3ec-196">(포트 번호를 사용 하 여) 다음 URL은 브라우저에 대해 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-196">The following URL (using your port number) is displayed for the browser:</span></span>  
    `https://localhost:44300/ProductList`
3. <span data-ttu-id="7d3ec-197">그런 다음 클릭는 **자동차** 페이지의 위쪽 범주 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-197">Next, click the **Cars** category link near the top of the page.</span></span>  
 <span data-ttu-id="7d3ec-198">만 자동차에 표시 되는 *ProductList.aspx* 페이지.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-198">Only cars are displayed on the *ProductList.aspx* page.</span></span> <span data-ttu-id="7d3ec-199">(포트 번호를 사용 하 여) 다음 URL은 브라우저에 대해 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-199">The following URL (using your port number) is displayed for the browser:</span></span>  
    `https://localhost:44300/Category/Cars`
4. <span data-ttu-id="7d3ec-200">페이지에 나열 된 첫 번째 자동차의 이름을 포함 하는 링크 클릭 ("**변환 가능 자동차**") 제품 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-200">Click the link containing the name of the first car listed on the page ("**Convertible Car**") to display the product details.</span></span>  
 <span data-ttu-id="7d3ec-201">(포트 번호를 사용 하 여) 다음 URL은 브라우저에 대해 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-201">The following URL (using your port number) is displayed for the browser:</span></span>  
    `https://localhost:44300/Product/Convertible%20Car`
5. <span data-ttu-id="7d3ec-202">다음으로 브라우저에 (포트 번호를 사용 하 여) 다음 라우팅되지 않은 URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-202">Next, enter the following non-routed URL (using your port number) into the browser:</span></span>  
    `https://localhost:44300/ProductDetails.aspx?productID=2`  
 <span data-ttu-id="7d3ec-203">코드는 여전히 사용자가 책갈피가 표시 된 링크의 경우 쿼리 문자열을 포함 하는 URL을 인식 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-203">The code still recognizes a URL that includes a query string, for the case where a user has a link bookmarked.</span></span>

## <a name="summary"></a><span data-ttu-id="7d3ec-204">요약</span><span class="sxs-lookup"><span data-stu-id="7d3ec-204">Summary</span></span>

<span data-ttu-id="7d3ec-205">이 자습서에서는 범주 및 제품에 대 한 경로 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-205">In this tutorial, you have added routes for categories and products.</span></span> <span data-ttu-id="7d3ec-206">모델 바인딩을 사용 하는 데이터 컨트롤과 경로 수 통합 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-206">You have learned how routes can be integrated with data controls that use model binding.</span></span> <span data-ttu-id="7d3ec-207">다음 자습서에서는 전역 오류 처리를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d3ec-207">In the next tutorial, you will implement global error handling.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7d3ec-208">추가 자료</span><span class="sxs-lookup"><span data-stu-id="7d3ec-208">Additional Resources</span></span>

[<span data-ttu-id="7d3ec-209">Asp.net Url</span><span class="sxs-lookup"><span data-stu-id="7d3ec-209">ASP.NET Friendly URLs</span></span>](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)  
[<span data-ttu-id="7d3ec-210">Azure 앱 서비스에 멤버 자격, OAuth, SQL 데이터베이스와 보안 ASP.NET Web Forms 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="7d3ec-210">Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[<span data-ttu-id="7d3ec-211">Microsoft Azure-무료 평가판</span><span class="sxs-lookup"><span data-stu-id="7d3ec-211">Microsoft Azure - Free Trial</span></span>](https://azure.microsoft.com/pricing/free-trial/)

> [!div class="step-by-step"]
> <span data-ttu-id="7d3ec-212">[이전](membership-and-administration.md)
> [다음](aspnet-error-handling.md)</span><span class="sxs-lookup"><span data-stu-id="7d3ec-212">[Previous](membership-and-administration.md)
[Next](aspnet-error-handling.md)</span></span>
