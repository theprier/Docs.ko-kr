---
uid: web-api/overview/web-api-routing-and-actions/routing-and-action-selection
title: 라우팅 및 ASP.NET Web API에서에서 작업 선택 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2012
ms.topic: article
ms.assetid: bcf2d223-cb7f-411e-be05-f43e96a14015
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-and-action-selection
msc.type: authoredcontent
ms.openlocfilehash: dc0edbdf62ceab1baf441301b47c0293de9a5c5d
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37388616"
---
<a name="routing-and-action-selection-in-aspnet-web-api"></a><span data-ttu-id="ecacb-102">라우팅 및 ASP.NET Web API에서에서 작업 선택</span><span class="sxs-lookup"><span data-stu-id="ecacb-102">Routing and Action Selection in ASP.NET Web API</span></span>
====================
<span data-ttu-id="ecacb-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ecacb-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="ecacb-104">이 문서에서는 ASP.NET Web API 컨트롤러에 특정 작업에 HTTP 요청을 라우트하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-104">This article describes how ASP.NET Web API routes an HTTP request to a particular action on a controller.</span></span>

> [!NOTE]
> <span data-ttu-id="ecacb-105">라우팅의 개괄적인 개요를 참조 하세요 [ASP.NET Web API에서 라우팅](routing-in-aspnet-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-105">For a high-level overview of routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>


<span data-ttu-id="ecacb-106">이 문서에서는 라우팅 프로세스의 세부 정보를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-106">This article looks at the details of the routing process.</span></span> <span data-ttu-id="ecacb-107">Web API 프로젝트를 만들고 일부 요청이 가져올 없는 찾기 예상 대로 라우팅할 바랍니다이 기사의 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-107">If you create a Web API project and find that some requests don't get routed the way you expect, hopefully this article will help.</span></span>

<span data-ttu-id="ecacb-108">라우팅에 세 가지 주요 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-108">Routing has three main phases:</span></span>

1. <span data-ttu-id="ecacb-109">경로 템플릿에 URI를 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-109">Matching the URI to a route template.</span></span>
2. <span data-ttu-id="ecacb-110">컨트롤러를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-110">Selecting a controller.</span></span>
3. <span data-ttu-id="ecacb-111">작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-111">Selecting an action.</span></span>

<span data-ttu-id="ecacb-112">사용자 고유의 사용자 지정 동작을 사용 하 여 프로세스의 일부를 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-112">You can replace some parts of the process with your own custom behaviors.</span></span> <span data-ttu-id="ecacb-113">이 문서에서는 기본 동작에 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-113">In this article, I describe the default behavior.</span></span> <span data-ttu-id="ecacb-114">끝으로 동작을 사용자 지정할 수 있는 위치 언급 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-114">At the end, I note the places where you can customize the behavior.</span></span>

## <a name="route-templates"></a><span data-ttu-id="ecacb-115">경로 템플릿</span><span class="sxs-lookup"><span data-stu-id="ecacb-115">Route Templates</span></span>

<span data-ttu-id="ecacb-116">경로 템플릿을 URI 경로 비슷한 보이지만 중괄호를 사용 하 여 표시 된 자리 표시자 값을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-116">A route template looks similar to a URI path, but it can have placeholder values, indicated with curly braces:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample1.ps1)]

<span data-ttu-id="ecacb-117">경로 만든 경우에 자리 표시자의 일부 또는 전부에 대 한 기본값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-117">When you create a route, you can provide default values for some or all of the placeholders:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample2.cs)]

<span data-ttu-id="ecacb-118">또한 URI 세그먼트를 자리 표시자 수 일치 하는 방법을 제한 하는 제약 조건을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-118">You can also provide constraints, which restrict how a URI segment can match a placeholder:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample3.js)]

<span data-ttu-id="ecacb-119">프레임 워크는 서식 파일의 URI 경로 세그먼트를 일치 시 키 려 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-119">The framework tries to match the segments in the URI path to the template.</span></span> <span data-ttu-id="ecacb-120">템플릿에서 리터럴은 정확 하 게 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-120">Literals in the template must match exactly.</span></span> <span data-ttu-id="ecacb-121">자리 표시자 제약 조건을 지정 하지 않는 한 모든 값과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-121">A placeholder matches any value, unless you specify constraints.</span></span> <span data-ttu-id="ecacb-122">프레임 워크는 호스트 이름 또는 쿼리 매개 변수를 같은 URI의 다른 부분을 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-122">The framework does not match other parts of the URI, such as the host name or the query parameters.</span></span> <span data-ttu-id="ecacb-123">프레임 워크는 URI와 일치 하는 경로 테이블의 첫 번째 경로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-123">The framework selects the first route in the route table that matches the URI.</span></span>

<span data-ttu-id="ecacb-124">두 가지 특수 한 자리 표시 자가: "{컨트롤러}" 및 "{action}".</span><span class="sxs-lookup"><span data-stu-id="ecacb-124">There are two special placeholders: "{controller}" and "{action}".</span></span>

- <span data-ttu-id="ecacb-125">"{컨트롤러}"를 컨트롤러의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-125">"{controller}" provides the name of the controller.</span></span>
- <span data-ttu-id="ecacb-126">"{action}" 작업의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-126">"{action}" provides the name of the action.</span></span> <span data-ttu-id="ecacb-127">Web API "{action}"를 생략 하 일반적인 규칙이입니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-127">In Web API, the usual convention is to omit "{action}".</span></span>

### <a name="defaults"></a><span data-ttu-id="ecacb-128">기본값</span><span class="sxs-lookup"><span data-stu-id="ecacb-128">Defaults</span></span>

<span data-ttu-id="ecacb-129">기본값을 제공 하면 해당 세그먼트가 없는 URI 경로 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-129">If you provide defaults, the route will match a URI that is missing those segments.</span></span> <span data-ttu-id="ecacb-130">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="ecacb-130">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample4.cs)]

<span data-ttu-id="ecacb-131">URI "`http://localhost/api/products`"이이 경로 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-131">The URI "`http://localhost/api/products`" matches this route.</span></span> <span data-ttu-id="ecacb-132">"{범주}" 세그먼트 "all 로" 기본 값이 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-132">The "{category}" segment is assigned the default value "all".</span></span>

### <a name="route-dictionary"></a><span data-ttu-id="ecacb-133">경로 사전</span><span class="sxs-lookup"><span data-stu-id="ecacb-133">Route Dictionary</span></span>

<span data-ttu-id="ecacb-134">프레임 워크는 URI와 일치 하는 찾으면 각 자리 표시자에 대 한 값이 들어 있는 사전을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-134">If the framework finds a match for a URI, it creates a dictionary that contains the value for each placeholder.</span></span> <span data-ttu-id="ecacb-135">키는 중괄호를 포함 하지 않고, 자리 표시자 이름을입니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-135">The keys are the placeholder names, not including the curly braces.</span></span> <span data-ttu-id="ecacb-136">기본값 또는 URI 경로에서 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-136">The values are taken from the URI path or from the defaults.</span></span> <span data-ttu-id="ecacb-137">사전에 저장 되는 **IHttpRouteData** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-137">The dictionary is stored in the **IHttpRouteData** object.</span></span>

<span data-ttu-id="ecacb-138">이 경로 일치 하는 단계 동안 특별 한 "{컨트롤러}" 및 "{action}" 자리 표시자를 다른 자리 표시자와 마찬가지로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-138">During this route-matching phase, the special "{controller}" and "{action}" placeholders are treated just like the other placeholders.</span></span> <span data-ttu-id="ecacb-139">다른 값을 사용 하 여 사전에 저장 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-139">They are simply stored in the dictionary with the other values.</span></span>

<span data-ttu-id="ecacb-140">기본값에는 특수 한 값을 가질 수 **RouteParameter.Optional**합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-140">A default can have the special value **RouteParameter.Optional**.</span></span> <span data-ttu-id="ecacb-141">자리 표시자 가져옵니다이 값을 할당 하는 경우 값 경로 사전에 추가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-141">If a placeholder gets assigned this value, the value is not added to the route dictionary.</span></span> <span data-ttu-id="ecacb-142">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="ecacb-142">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample5.cs)]

<span data-ttu-id="ecacb-143">"Api/제품"의 URI 경로 대 한 경로 사전을 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-143">For the URI path "api/products", the route dictionary will contain:</span></span>

- <span data-ttu-id="ecacb-144">컨트롤러: "제품"</span><span class="sxs-lookup"><span data-stu-id="ecacb-144">controller: "products"</span></span>
- <span data-ttu-id="ecacb-145">범주: "all"</span><span class="sxs-lookup"><span data-stu-id="ecacb-145">category: "all"</span></span>

<span data-ttu-id="ecacb-146">그러나 "Api/제품/toys/123", 경로 사전을 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-146">For "api/products/toys/123", however, the route dictionary will contain:</span></span>

- <span data-ttu-id="ecacb-147">컨트롤러: "제품"</span><span class="sxs-lookup"><span data-stu-id="ecacb-147">controller: "products"</span></span>
- <span data-ttu-id="ecacb-148">범주: "toys"</span><span class="sxs-lookup"><span data-stu-id="ecacb-148">category: "toys"</span></span>
- <span data-ttu-id="ecacb-149">id: "123"</span><span class="sxs-lookup"><span data-stu-id="ecacb-149">id: "123"</span></span>

<span data-ttu-id="ecacb-150">기본값은 경로 템플릿에서 아무 곳 이나 표시 되지 않는 값을 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-150">The defaults can also include a value that does not appear anywhere in the route template.</span></span> <span data-ttu-id="ecacb-151">경로 일치 하는 경우 해당 값이 사전에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-151">If the route matches, that value is stored in the dictionary.</span></span> <span data-ttu-id="ecacb-152">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="ecacb-152">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample6.cs)]

<span data-ttu-id="ecacb-153">URI 경로 "api/루트/8" 인 경우 사전 두 값이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-153">If the URI path is "api/root/8", the dictionary will contain two values:</span></span>

- <span data-ttu-id="ecacb-154">컨트롤러: "customers"</span><span class="sxs-lookup"><span data-stu-id="ecacb-154">controller: "customers"</span></span>
- <span data-ttu-id="ecacb-155">id: "8"</span><span class="sxs-lookup"><span data-stu-id="ecacb-155">id: "8"</span></span>

## <a name="selecting-a-controller"></a><span data-ttu-id="ecacb-156">컨트롤러를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-156">Selecting a Controller</span></span>

<span data-ttu-id="ecacb-157">컨트롤러 선택 하 여 처리 되는 **IHttpControllerSelector.SelectController** 메서드.</span><span class="sxs-lookup"><span data-stu-id="ecacb-157">Controller selection is handled by the **IHttpControllerSelector.SelectController** method.</span></span> <span data-ttu-id="ecacb-158">이 메서드는 **HttpRequestMessage** 인스턴스와 반환은 **HttpControllerDescriptor**합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-158">This method takes an **HttpRequestMessage** instance and returns an **HttpControllerDescriptor**.</span></span> <span data-ttu-id="ecacb-159">기본 구현에서 제공 되는 **DefaultHttpControllerSelector** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-159">The default implementation is provided by the **DefaultHttpControllerSelector** class.</span></span> <span data-ttu-id="ecacb-160">이 클래스는 간단한 알고리즘을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-160">This class uses a straightforward algorithm:</span></span>

1. <span data-ttu-id="ecacb-161">"Controller" 키에 대 한 경로 사전을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-161">Look in the route dictionary for the key "controller".</span></span>
2. <span data-ttu-id="ecacb-162">이 키에 대 한 값을 사용 하 고 컨트롤러 형식 이름을 가져오려면 "Controller" 문자열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-162">Take the value for this key and append the string "Controller" to get the controller type name.</span></span>
3. <span data-ttu-id="ecacb-163">이 형식 이름 사용 하 여 Web API 컨트롤러를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-163">Look for a Web API controller with this type name.</span></span>

<span data-ttu-id="ecacb-164">예를 들어, 경로 사전 키-값 쌍 "controller"가 들어 있으면 = "제품", 컨트롤러 형식 "ProductsController"입니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-164">For example, if the route dictionary contains the key-value pair "controller" = "products", then the controller type is "ProductsController".</span></span> <span data-ttu-id="ecacb-165">일치 하는 형식이 없는 또는 여러 일치 항목이 있으면 클라이언트에 오류를 반환 하는 프레임 워크.</span><span class="sxs-lookup"><span data-stu-id="ecacb-165">If there is no matching type, or multiple matches, the framework returns an error to the client.</span></span>

<span data-ttu-id="ecacb-166">3 단계에 대 한 **DefaultHttpControllerSelector** 사용 하는 **IHttpControllerTypeResolver** 를 Web API 컨트롤러 유형 목록을 가져오는 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-166">For step 3, **DefaultHttpControllerSelector** uses the **IHttpControllerTypeResolver** interface to get the list of Web API controller types.</span></span> <span data-ttu-id="ecacb-167">기본 구현의 **IHttpControllerTypeResolver** (a) 구현 하는 모든 공용 클래스를 반환 **IHttpController**, (b)는 abstract (c) 이름이 "Controller"로 끝나는 없고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-167">The default implementation of **IHttpControllerTypeResolver** returns all public classes that (a) implement **IHttpController**, (b) are not abstract, and (c) have a name that ends in "Controller".</span></span>

## <a name="action-selection"></a><span data-ttu-id="ecacb-168">작업 선택</span><span class="sxs-lookup"><span data-stu-id="ecacb-168">Action Selection</span></span>

<span data-ttu-id="ecacb-169">컨트롤러를 선택 하면 프레임 워크를 호출 하 여 작업을 선택 합니다 **IHttpActionSelector.SelectAction** 메서드.</span><span class="sxs-lookup"><span data-stu-id="ecacb-169">After selecting the controller, the framework selects the action by calling the **IHttpActionSelector.SelectAction** method.</span></span> <span data-ttu-id="ecacb-170">이 메서드는 **HttpControllerContext** 반환 하 고는 **HttpActionDescriptor**합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-170">This method takes an **HttpControllerContext** and returns an **HttpActionDescriptor**.</span></span>

<span data-ttu-id="ecacb-171">기본 구현에서 제공 되는 **ApiControllerActionSelector** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-171">The default implementation is provided by the **ApiControllerActionSelector** class.</span></span> <span data-ttu-id="ecacb-172">작업을 선택 하려면 다음에서 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-172">To select an action, it looks at the following:</span></span>

- <span data-ttu-id="ecacb-173">요청의 HTTP 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-173">The HTTP method of the request.</span></span>
- <span data-ttu-id="ecacb-174">있는 경우 경로 템플릿에서 "{action}" 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-174">The "{action}" placeholder in the route template, if present.</span></span>
- <span data-ttu-id="ecacb-175">컨트롤러에서 작업의 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-175">The parameters of the actions on the controller.</span></span>

<span data-ttu-id="ecacb-176">선택 알고리즘을 살펴보기 전에 컨트롤러 작업에 대 한 몇 가지 작업을 이해 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-176">Before looking at the selection algorithm, we need to understand some things about controller actions.</span></span>

<span data-ttu-id="ecacb-177">**컨트롤러에서 메서드 "작업" 것으로 간주 됩니다.**</span><span class="sxs-lookup"><span data-stu-id="ecacb-177">**Which methods on the controller are considered "actions"?**</span></span> <span data-ttu-id="ecacb-178">작업을 선택 하면 프레임 워크만 살펴봅니다 공용 인스턴스 메서드는 컨트롤러에서.</span><span class="sxs-lookup"><span data-stu-id="ecacb-178">When selecting an action, the framework only looks at public instance methods on the controller.</span></span> <span data-ttu-id="ecacb-179">제외 뿐만 ["특수 한 이름이"](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname) 메서드 (생성자, 이벤트, 연산자 오버 로드 등), 및에서 상속 된 메서드는 **ApiController** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-179">Also, it excludes ["special name"](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname) methods (constructors, events, operator overloads, and so forth), and methods inherited from the **ApiController** class.</span></span>

<span data-ttu-id="ecacb-180">**HTTP 메서드입니다.**</span><span class="sxs-lookup"><span data-stu-id="ecacb-180">**HTTP Methods.**</span></span> <span data-ttu-id="ecacb-181">프레임 워크는만 다음과 같이 결정 요청의 HTTP 메서드를 일치 하는 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-181">The framework only chooses actions that match the HTTP method of the request, determined as follows:</span></span>

1. <span data-ttu-id="ecacb-182">특성을 사용 하 여 HTTP 메서드를 지정할 수 있습니다: **AcceptVerbs**, **HttpDelete**를 **HttpGet**를 **HttpHead**,  **HttpOptions**하십시오 **HttpPatch**, **HttpPost**, 또는 **HttpPut**합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-182">You can specify the HTTP method with an attribute: **AcceptVerbs**, **HttpDelete**, **HttpGet**, **HttpHead**, **HttpOptions**, **HttpPatch**, **HttpPost**, or **HttpPut**.</span></span>
2. <span data-ttu-id="ecacb-183">이 고, 그렇지 컨트롤러 메서드의 이름을 "Get", "Post", "Put", "Delete", "Head", "옵션" 또는 "패치"를 사용 하 여 시작 되 면 다음 규칙에 따라 작업 해당 HTTP 메서드를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-183">Otherwise, if the name of the controller method starts with "Get", "Post", "Put", "Delete", "Head", "Options", or "Patch", then by convention the action supports that HTTP method.</span></span>
3. <span data-ttu-id="ecacb-184">위의 none 인 경우 메서드는 POST를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-184">If none of the above, the method supports POST.</span></span>

<span data-ttu-id="ecacb-185">**매개 변수 바인딩입니다.**</span><span class="sxs-lookup"><span data-stu-id="ecacb-185">**Parameter Bindings.**</span></span> <span data-ttu-id="ecacb-186">매개 변수 바인딩의 경우 Web API는 매개 변수의 값을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="ecacb-186">A parameter binding is how Web API creates a value for a parameter.</span></span> <span data-ttu-id="ecacb-187">다음은 매개 변수 바인딩에 대 한 기본 규칙이입니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-187">Here is the default rule for parameter binding:</span></span>

- <span data-ttu-id="ecacb-188">단순 형식 URI에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-188">Simple types are taken from the URI.</span></span>
- <span data-ttu-id="ecacb-189">요청 본문에서 복합 형식은 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-189">Complex types are taken from the request body.</span></span>

<span data-ttu-id="ecacb-190">단순 형식에 포함할 모든는 [.NET Framework 기본 형식](https://msdn.microsoft.com/library/system.type.isprimitive), plus **DateTime**, **Decimal**, **Guid**, **문자열** , 및 **TimeSpan**합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-190">Simple types include all of the [.NET Framework primitive types](https://msdn.microsoft.com/library/system.type.isprimitive), plus **DateTime**, **Decimal**, **Guid**, **String**, and **TimeSpan**.</span></span> <span data-ttu-id="ecacb-191">각 작업에 대해 최대 하나의 매개 변수는 요청 본문을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-191">For each action, at most one parameter can read the request body.</span></span>

> [!NOTE]
> <span data-ttu-id="ecacb-192">기본 바인딩 규칙을 재정의 하는 것이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-192">It is possible to override the default binding rules.</span></span> <span data-ttu-id="ecacb-193">참조 [내부적 WebAPI 매개 변수 바인딩](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-193">See [WebAPI Parameter binding under the hood](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx).</span></span>


<span data-ttu-id="ecacb-194">배경을 사용 하 여 작업 선택 알고리즘은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-194">With that background, here is the action selection algorithm.</span></span>

1. <span data-ttu-id="ecacb-195">HTTP 요청 메서드 일치 하는 컨트롤러에서 모든 작업의 목록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-195">Create a list of all actions on the controller that match the HTTP request method.</span></span>
2. <span data-ttu-id="ecacb-196">경로 사전을 "작업" 항목이 있으면 제거 작업 이름이이 값과 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-196">If the route dictionary has an "action" entry, remove actions whose name does not match this value.</span></span>
3. <span data-ttu-id="ecacb-197">URI 작업 매개 변수를 다음과 같이 일치 하도록 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-197">Try to match action parameters to the URI, as follows:</span></span> 

    1. <span data-ttu-id="ecacb-198">각 작업에 대 한 매개 변수는 단순 형식의 바인딩을 URI에서 매개 변수를 가져옵니다의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-198">For each action, get a list of the parameters that are a simple type, where the binding gets the parameter from the URI.</span></span> <span data-ttu-id="ecacb-199">선택적 매개 변수를 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-199">Exclude optional parameters.</span></span>
    2. <span data-ttu-id="ecacb-200">이 목록에서를 URI 쿼리 문자열 또는 경로 사전을에서 각 매개 변수 이름에 대해 일치 하는 항목을 찾아 봅니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-200">From this list, try to find a match for each parameter name, either in the route dictionary or in the URI query string.</span></span> <span data-ttu-id="ecacb-201">일치는 대/소문자 구분 및 매개 변수 순서에 종속 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-201">Matches are case insensitive and do not depend on the parameter order.</span></span>
    3. <span data-ttu-id="ecacb-202">모든 매개 변수 목록에 있는 일치 하는 URI에서 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-202">Select an action where every parameter in the list has a match in the URI.</span></span>
    4. <span data-ttu-id="ecacb-203">이러한 조건을 충족 하는 더 이상의 작업을 하는 경우 대부분의 매개 변수 일치를 사용 하 여 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-203">If more that one action meets these criteria, pick the one with the most parameter matches.</span></span>
4. <span data-ttu-id="ecacb-204">사용 하 여 작업을 무시 합니다 **[NonAction]** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-204">Ignore actions with the **[NonAction]** attribute.</span></span>

<span data-ttu-id="ecacb-205">3 단계 아마도 가장 혼동 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-205">Step #3 is probably the most confusing.</span></span> <span data-ttu-id="ecacb-206">기본 개념은 매개 변수는 URI, 요청 본문에서 또는 사용자 지정 바인딩에서 해당 값을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-206">The basic idea is that a parameter can get its value either from the URI, from the request body, or from a custom binding.</span></span> <span data-ttu-id="ecacb-207">URI에서 제공 되는 매개 변수에 대 한 URI (경로 사전)를 통해 경로 또는 쿼리 문자열 매개 변수 값을 실제로 포함 되어 있는지 확인 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-207">For parameters that come from the URI, we want to ensure that the URI actually contains a value for that parameter, either in the path (via the route dictionary) or in the query string.</span></span>

<span data-ttu-id="ecacb-208">예를 들어, 다음 작업을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-208">For example, consider the following action:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample7.cs)]

<span data-ttu-id="ecacb-209">합니다 *id* uri 매개 변수를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-209">The *id* parameter binds to the URI.</span></span> <span data-ttu-id="ecacb-210">따라서이 작업에 "id", 경로 사전을 또는 쿼리 문자열에 대 한 값이 포함 된 URI 에서만 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-210">Therefore, this action can only match a URI that contains a value for "id", either in the route dictionary or in the query string.</span></span>

<span data-ttu-id="ecacb-211">선택적 매개 변수는 선택 사항 이므로 예외.</span><span class="sxs-lookup"><span data-stu-id="ecacb-211">Optional parameters are an exception, because they are optional.</span></span> <span data-ttu-id="ecacb-212">선택적 매개 변수에 대 한 것 확인 바인딩을 URI에서 값을 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-212">For an optional parameter, it's OK if the binding can't get the value from the URI.</span></span>

<span data-ttu-id="ecacb-213">복합 형식에는 다른 이유로 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-213">Complex types are an exception for a different reason.</span></span> <span data-ttu-id="ecacb-214">복합 형식 사용자 지정 바인딩을 통해 URI에만 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-214">A complex type can only bind to the URI through a custom binding.</span></span> <span data-ttu-id="ecacb-215">하지만 경우 프레임 워크를 알 수 없으므로 사전에 매개 변수는 특정 URI에 바인딩하는 것 여부를 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-215">But in that case, the framework cannot know in advance whether the parameter would bind to a particular URI.</span></span> <span data-ttu-id="ecacb-216">에 바인딩을 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-216">To find out, it would need to invoke the binding.</span></span> <span data-ttu-id="ecacb-217">선택 알고리즘의 목표 바인딩을 호출 하기 전에 정적 설명에서 작업을 선택 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-217">The goal of the selection algorithm is to select an action from the static description, before invoking any bindings.</span></span> <span data-ttu-id="ecacb-218">따라서 복잡 한 형식 일치 알고리즘에서 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-218">Therefore, complex types are excluded from the matching algorithm.</span></span>

<span data-ttu-id="ecacb-219">작업을 선택한 후에 모든 매개 변수 바인딩 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-219">After the action is selected, all parameter bindings are invoked.</span></span>

<span data-ttu-id="ecacb-220">요약:</span><span class="sxs-lookup"><span data-stu-id="ecacb-220">Summary:</span></span>

- <span data-ttu-id="ecacb-221">작업 요청의 HTTP 메서드를 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-221">The action must match the HTTP method of the request.</span></span>
- <span data-ttu-id="ecacb-222">작업 이름이 있는 경우 경로 사전에 "작업" 항목이 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-222">The action name must match the "action" entry in the route dictionary, if present.</span></span>
- <span data-ttu-id="ecacb-223">작업의 모든 매개 변수에 대해 매개 변수는 URI에서 가져온 경우 다음 매개 변수 이름 있어야 경로 사전을 또는 URI 쿼리 문자열에서.</span><span class="sxs-lookup"><span data-stu-id="ecacb-223">For every parameter of the action, if the parameter is taken from the URI, then the parameter name must be found either in the route dictionary or in the URI query string.</span></span> <span data-ttu-id="ecacb-224">(선택적 매개 변수 및 복합 형식으로 매개 변수 제외 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="ecacb-224">(Optional parameters and parameters with complex types are excluded.)</span></span>
- <span data-ttu-id="ecacb-225">가장 많은 매개 변수 일치 시 키 려 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-225">Try to match the most number of parameters.</span></span> <span data-ttu-id="ecacb-226">가장 일치 하는 매개 변수 없이 메서드를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-226">The best match might be a method with no parameters.</span></span>

## <a name="extended-example"></a><span data-ttu-id="ecacb-227">확장 된 예제</span><span class="sxs-lookup"><span data-stu-id="ecacb-227">Extended Example</span></span>

<span data-ttu-id="ecacb-228">경로:</span><span class="sxs-lookup"><span data-stu-id="ecacb-228">Routes:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample8.cs)]

<span data-ttu-id="ecacb-229">컨트롤러:</span><span class="sxs-lookup"><span data-stu-id="ecacb-229">Controller:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample9.cs)]

<span data-ttu-id="ecacb-230">HTTP 요청:</span><span class="sxs-lookup"><span data-stu-id="ecacb-230">HTTP request:</span></span>

[!code-console[Main](routing-and-action-selection/samples/sample10.cmd)]

### <a name="route-matching"></a><span data-ttu-id="ecacb-231">경로 일치</span><span class="sxs-lookup"><span data-stu-id="ecacb-231">Route Matching</span></span>

<span data-ttu-id="ecacb-232">URI "DefaultApi" 라는 경로 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-232">The URI matches the route named "DefaultApi".</span></span> <span data-ttu-id="ecacb-233">경로 사전에는 다음 항목이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-233">The route dictionary contains the following entries:</span></span>

- <span data-ttu-id="ecacb-234">컨트롤러: "제품"</span><span class="sxs-lookup"><span data-stu-id="ecacb-234">controller: "products"</span></span>
- <span data-ttu-id="ecacb-235">id: "1"</span><span class="sxs-lookup"><span data-stu-id="ecacb-235">id: "1"</span></span>

<span data-ttu-id="ecacb-236">쿼리 문자열 매개 변수, "version" 및 "details" 경로 사전을 포함 하지 않지만 이러한 세대로 간주 됩니다 작업 선택 중입니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-236">The route dictionary does not contain the query string parameters, "version" and "details", but these will still be considered during action selection.</span></span>

### <a name="controller-selection"></a><span data-ttu-id="ecacb-237">컨트롤러 선택</span><span class="sxs-lookup"><span data-stu-id="ecacb-237">Controller Selection</span></span>

<span data-ttu-id="ecacb-238">경로 사전에서 "controller" 엔트리에서 컨트롤러 형식이 `ProductsController`합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-238">From the "controller" entry in the route dictionary, the controller type is `ProductsController`.</span></span>

### <a name="action-selection"></a><span data-ttu-id="ecacb-239">작업 선택</span><span class="sxs-lookup"><span data-stu-id="ecacb-239">Action Selection</span></span>

<span data-ttu-id="ecacb-240">HTTP 요청은 GET 요청을 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-240">The HTTP request is a GET request.</span></span> <span data-ttu-id="ecacb-241">GET 지 컨트롤러 작업은 `GetAll`, `GetById`, 및 `FindProductsByName`합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-241">The controller actions that support GET are `GetAll`, `GetById`, and `FindProductsByName`.</span></span> <span data-ttu-id="ecacb-242">경로 사전이 되므로 작업 이름과 일치할 필요가 없습니다 "작업"에 대 한 진입점을 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-242">The route dictionary does not contain an entry for "action", so we don't need to match the action name.</span></span>

<span data-ttu-id="ecacb-243">다음으로, 하려고 노력을 작업에 대 한 매개 변수 이름과 일치 GET 작업에만 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-243">Next, we try to match parameter names for the actions, looking only at the GET actions.</span></span>

| <span data-ttu-id="ecacb-244">작업</span><span class="sxs-lookup"><span data-stu-id="ecacb-244">Action</span></span> | <span data-ttu-id="ecacb-245">일치 하는 매개 변수</span><span class="sxs-lookup"><span data-stu-id="ecacb-245">Parameters to Match</span></span> |
| --- | --- |
| `GetAll` | <span data-ttu-id="ecacb-246">없음</span><span class="sxs-lookup"><span data-stu-id="ecacb-246">none</span></span> |
| `GetById` | <span data-ttu-id="ecacb-247">"id"</span><span class="sxs-lookup"><span data-stu-id="ecacb-247">"id"</span></span> |
| `FindProductsByName` | <span data-ttu-id="ecacb-248">"name"</span><span class="sxs-lookup"><span data-stu-id="ecacb-248">"name"</span></span> |

<span data-ttu-id="ecacb-249">다음에 유의 합니다 *버전* 의 매개 변수 `GetById` 선택적 매개 변수 이므로 간주 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-249">Notice that the *version* parameter of `GetById` is not considered, because it is an optional parameter.</span></span>

<span data-ttu-id="ecacb-250">`GetAll` 메서드는 일반적으로 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-250">The `GetAll` method matches trivially.</span></span> <span data-ttu-id="ecacb-251">`GetById` 메서드 일치, "id"를 포함 하는 경로 사전을 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-251">The `GetById` method also matches, because the route dictionary contains "id".</span></span> <span data-ttu-id="ecacb-252">`FindProductsByName` 메서드 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-252">The `FindProductsByName` method does not match.</span></span>

<span data-ttu-id="ecacb-253">합니다 `GetById` 에 대 한 매개 변수 없이와 하나의 매개 변수를 일치 하기 때문에 메서드 wins `GetAll`합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-253">The `GetById` method wins, because it matches one parameter, versus no parameters for `GetAll`.</span></span> <span data-ttu-id="ecacb-254">메서드는 다음 매개 변수 값을 사용 하 여 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-254">The method is invoked with the following parameter values:</span></span>

- <span data-ttu-id="ecacb-255">*id* = 1</span><span class="sxs-lookup"><span data-stu-id="ecacb-255">*id* = 1</span></span>
- <span data-ttu-id="ecacb-256">*버전* 1.5 =</span><span class="sxs-lookup"><span data-stu-id="ecacb-256">*version* = 1.5</span></span>

<span data-ttu-id="ecacb-257">도 있음을 *버전* 사용 되지 않는 선택 알고리즘에서 매개 변수의 URI 쿼리 문자열에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-257">Notice that even though *version* was not used in the selection algorithm, the value of the parameter comes from the URI query string.</span></span>

## <a name="extension-points"></a><span data-ttu-id="ecacb-258">확장점</span><span class="sxs-lookup"><span data-stu-id="ecacb-258">Extension Points</span></span>

<span data-ttu-id="ecacb-259">Web API 라우팅 프로세스의 일부에 대 한 확장 지점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-259">Web API provides extension points for some parts of the routing process.</span></span>

| <span data-ttu-id="ecacb-260">인터페이스</span><span class="sxs-lookup"><span data-stu-id="ecacb-260">Interface</span></span> | <span data-ttu-id="ecacb-261">설명</span><span class="sxs-lookup"><span data-stu-id="ecacb-261">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ecacb-262">**IHttpControllerSelector**</span><span class="sxs-lookup"><span data-stu-id="ecacb-262">**IHttpControllerSelector**</span></span> | <span data-ttu-id="ecacb-263">컨트롤러를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-263">Selects the controller.</span></span> |
| <span data-ttu-id="ecacb-264">**IHttpControllerTypeResolver**</span><span class="sxs-lookup"><span data-stu-id="ecacb-264">**IHttpControllerTypeResolver**</span></span> | <span data-ttu-id="ecacb-265">컨트롤러 형식의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-265">Gets the list of controller types.</span></span> <span data-ttu-id="ecacb-266">합니다 **DefaultHttpControllerSelector** 컨트롤러 형식을이 목록에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-266">The **DefaultHttpControllerSelector** chooses the controller type from this list.</span></span> |
| <span data-ttu-id="ecacb-267">**IAssembliesResolver**</span><span class="sxs-lookup"><span data-stu-id="ecacb-267">**IAssembliesResolver**</span></span> | <span data-ttu-id="ecacb-268">프로젝트 어셈블리의 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-268">Gets the list of project assemblies.</span></span> <span data-ttu-id="ecacb-269">합니다 **IHttpControllerTypeResolver** 인터페이스 컨트롤러 유형을 검색 하는이 목록을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-269">The **IHttpControllerTypeResolver** interface uses this list to find the controller types.</span></span> |
| <span data-ttu-id="ecacb-270">**IHttpControllerActivator**</span><span class="sxs-lookup"><span data-stu-id="ecacb-270">**IHttpControllerActivator**</span></span> | <span data-ttu-id="ecacb-271">새 컨트롤러 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-271">Creates new controller instances.</span></span> |
| <span data-ttu-id="ecacb-272">**IHttpActionSelector**</span><span class="sxs-lookup"><span data-stu-id="ecacb-272">**IHttpActionSelector**</span></span> | <span data-ttu-id="ecacb-273">작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-273">Selects the action.</span></span> |
| <span data-ttu-id="ecacb-274">**IHttpActionInvoker**</span><span class="sxs-lookup"><span data-stu-id="ecacb-274">**IHttpActionInvoker**</span></span> | <span data-ttu-id="ecacb-275">작업을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecacb-275">Invokes the action.</span></span> |

<span data-ttu-id="ecacb-276">사용 하 여 이러한 인터페이스에 대 한 고유한 구현을 제공 합니다는 **Services** 컬렉션에는 **HttpConfiguration** 개체:</span><span class="sxs-lookup"><span data-stu-id="ecacb-276">To provide your own implementation for any of these interfaces, use the **Services** collection on the **HttpConfiguration** object:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample11.cs)]
