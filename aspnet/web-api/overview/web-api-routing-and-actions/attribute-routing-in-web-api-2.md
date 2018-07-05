---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: ASP.NET Web API 2에에서 대 한 라우팅 특성 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 52164fde1a2277bb9ef07f2a5476ca78b71a8e52
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37802759"
---
<a name="attribute-routing-in-aspnet-web-api-2"></a><span data-ttu-id="25ccf-102">ASP.NET Web API 2에서에서 특성 라우팅</span><span class="sxs-lookup"><span data-stu-id="25ccf-102">Attribute Routing in ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="25ccf-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="25ccf-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="25ccf-104">*라우팅* 는 Web API 작업에 대 한 URI를 일치 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-104">*Routing* is how Web API matches a URI to an action.</span></span> <span data-ttu-id="25ccf-105">Web API 2에는 새 형식을 지 원하는 라우팅의 호출 *특성 라우팅은*합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-105">Web API 2 supports a new type of routing, called *attribute routing*.</span></span> <span data-ttu-id="25ccf-106">이름에서 알 수 있듯이 특성 라우팅을 사용 하 여 특성 경로 정의.</span><span class="sxs-lookup"><span data-stu-id="25ccf-106">As the name implies, attribute routing uses attributes to define routes.</span></span> <span data-ttu-id="25ccf-107">특성 라우팅을 제어할 수 자세한 Uri 통해 web API에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-107">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="25ccf-108">예를 들어, 리소스의 계층 구조를 설명 하는 Uri를 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-108">For example, you can easily create URIs that describe hierarchies of resources.</span></span>

<span data-ttu-id="25ccf-109">호출 규칙 기반 라우팅의 이전 스타일 라우팅 완벽 하 게 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-109">The earlier style of routing, called convention-based routing, is still fully supported.</span></span> <span data-ttu-id="25ccf-110">사실, 동일한 프로젝트에 두 가지 방법을 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-110">In fact, you can combine both techniques in the same project.</span></span>

<span data-ttu-id="25ccf-111">이 항목에서는 특성 라우팅을 사용 하도록 설정 하는 방법을 보여 줍니다 하 고 특성 라우팅에 대 한 다양 한 옵션을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-111">This topic shows how to enable attribute routing and describes the various options for attribute routing.</span></span> <span data-ttu-id="25ccf-112">특성 라우팅을 사용 하는 종단 간 자습서를 참조 하세요 [Web API 2에서 특성 라우팅을 사용 하 여 REST API를 만들고](create-a-rest-api-with-attribute-routing.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-112">For an end-to-end tutorial that uses attribute routing, see [Create a REST API with Attribute Routing in Web API 2](create-a-rest-api-with-attribute-routing.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="25ccf-113">전제 조건</span><span class="sxs-lookup"><span data-stu-id="25ccf-113">Prerequisites</span></span>

<span data-ttu-id="25ccf-114">[Visual Studio 2017](https://www.visualstudio.com/vs/) Community, Professional 또는 Enterprise Edition</span><span class="sxs-lookup"><span data-stu-id="25ccf-114">[Visual Studio 2017](https://www.visualstudio.com/vs/) Community, Professional, or Enterprise Edition</span></span>

<span data-ttu-id="25ccf-115">또는, NuGet 패키지 관리자를 사용 하 여 필요한 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-115">Alternatively, use NuGet Package Manager to install the necessary packages.</span></span> <span data-ttu-id="25ccf-116">**도구** Visual Studio에서 메뉴 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-116">From the **Tools** menu in Visual Studio, select **Library Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="25ccf-117">패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-117">Enter the following command in the Package Manager Console window:</span></span>

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a><span data-ttu-id="25ccf-118">라우팅 특성 이유?</span><span class="sxs-lookup"><span data-stu-id="25ccf-118">Why Attribute Routing?</span></span>

<span data-ttu-id="25ccf-119">사용 되는 웹 API의 첫 번째 릴리스인 *규칙 기반* 라우팅입니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-119">The first release of Web API used *convention-based* routing.</span></span> <span data-ttu-id="25ccf-120">라우팅의 해당 형식에 하나를 정의 하거나 더 많은 경로 템플릿은 기본적으로 문자열을 매개 변수화 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-120">In that type of routing, you define one or more route templates, which are basically parameterized strings.</span></span> <span data-ttu-id="25ccf-121">프레임 워크는 요청을 받으면 경로 템플릿에 대 한 URI와 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-121">When the framework receives a request, it matches the URI against the route template.</span></span> <span data-ttu-id="25ccf-122">(규칙 기반 라우팅에 대 한 자세한 내용은 참조 하십시오 [ASP.NET Web API에서 라우팅](routing-in-aspnet-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-122">(For more information about convention-based routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>

<span data-ttu-id="25ccf-123">규칙 기반 라우팅의 장점 중 하나는 한 곳에 정의 된 템플릿 및 라우팅 규칙은 모든 컨트롤러에서 일관 되 게 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-123">One advantage of convention-based routing is that templates are defined in a single place, and the routing rules are applied consistently across all controllers.</span></span> <span data-ttu-id="25ccf-124">그러나 규칙 기반 라우팅 하기가 어렵습니다 RESTful Api에 공통 되는 특정 URI 패턴을 지원 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-124">Unfortunately, convention-based routing makes it hard to support certain URI patterns that are common in RESTful APIs.</span></span> <span data-ttu-id="25ccf-125">예를 들어 리소스 자식 리소스를 종종 포함: 고객이 주문을 갖고, 영화 행위자, 책 저자 있고 등입니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-125">For example, resources often contain child resources: Customers have orders, movies have actors, books have authors, and so forth.</span></span> <span data-ttu-id="25ccf-126">이러한 관계를 반영 하는 Uri를 만드는 자연 스러운 것:</span><span class="sxs-lookup"><span data-stu-id="25ccf-126">It's natural to create URIs that reflect these relations:</span></span>

`/customers/1/orders`

<span data-ttu-id="25ccf-127">이러한 유형의 URI 규칙 기반 라우팅을 사용 하 여 만드는 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-127">This type of URI is difficult to create using convention-based routing.</span></span> <span data-ttu-id="25ccf-128">수행 될 수 있지만 컨트롤러 많거나 리소스 형식이 있는 경우에 결과 확장 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-128">Although it can be done, the results don't scale well if you have many controllers or resource types.</span></span>

<span data-ttu-id="25ccf-129">특성 라우팅을 사용 하 여이 URI에 대 한 경로 정의 하는 것이 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-129">With attribute routing, it's trivial to define a route for this URI.</span></span> <span data-ttu-id="25ccf-130">단순히 컨트롤러 작업에 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-130">You simply add an attribute to the controller action:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

<span data-ttu-id="25ccf-131">특성 라우팅는 쉽게 몇 가지 다른 패턴 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-131">Here are some other patterns that attribute routing makes easy.</span></span>

<span data-ttu-id="25ccf-132">**API 버전 관리**</span><span class="sxs-lookup"><span data-stu-id="25ccf-132">**API versioning**</span></span>

<span data-ttu-id="25ccf-133">이 예제에서는 "/ 제품/api/v1" 보다 다른 컨트롤러에 게 회람 "/ 제품/api/v2" 것입니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-133">In this example, "/api/v1/products" would be routed to a different controller than "/api/v2/products".</span></span>

`/api/v1/products`  
`/api/v2/products`

<span data-ttu-id="25ccf-134">**오버 로드 된 URI 세그먼트**</span><span class="sxs-lookup"><span data-stu-id="25ccf-134">**Overloaded URI segments**</span></span>

<span data-ttu-id="25ccf-135">이 예제에서는 주문 번호를 "1"은 있지만 컬렉션에 "보류 중"으로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-135">In this example, "1" is an order number, but "pending" maps to a collection.</span></span>

`/orders/1`  
`/orders/pending`

<span data-ttu-id="25ccf-136">**여러 매개 변수 유형**</span><span class="sxs-lookup"><span data-stu-id="25ccf-136">**Multiple parameter types**</span></span>

<span data-ttu-id="25ccf-137">이 예제에서는 주문 번호를 "1"은 있지만 "2013/06/16" 날짜를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-137">In this example, "1" is an order number, but "2013/06/16" specifies a date.</span></span>

`/orders/1`  
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a><span data-ttu-id="25ccf-138">특성 라우팅을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="25ccf-138">Enabling Attribute Routing</span></span>

<span data-ttu-id="25ccf-139">특성 라우팅을 사용, 호출 **MapHttpAttributeRoutes** 구성 중입니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-139">To enable attribute routing, call **MapHttpAttributeRoutes** during configuration.</span></span> <span data-ttu-id="25ccf-140">에 정의 되어이 확장 메서드는 **System.Web.Http.HttpConfigurationExtensions** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-140">This extension method is defined in the **System.Web.Http.HttpConfigurationExtensions** class.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

<span data-ttu-id="25ccf-141">특성 라우팅을 결합할 수 있습니다 [규칙 기반](routing-in-aspnet-web-api.md) 라우팅입니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-141">Attribute routing can be combined with [convention-based](routing-in-aspnet-web-api.md) routing.</span></span> <span data-ttu-id="25ccf-142">규칙 기반 경로 정의 하려면 호출을 **MapHttpRoute** 메서드.</span><span class="sxs-lookup"><span data-stu-id="25ccf-142">To define convention-based routes, call the **MapHttpRoute** method.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

<span data-ttu-id="25ccf-143">Web API를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [ASP.NET Web API 2 구성](../advanced/configuring-aspnet-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-143">For more information about configuring Web API, see [Configuring ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md).</span></span>

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a><span data-ttu-id="25ccf-144">참고: Web API 1에서 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="25ccf-144">Note: Migrating From Web API 1</span></span>

<span data-ttu-id="25ccf-145">Web API 2, 이전에 Web API 프로젝트 템플릿이 다음과 같은 코드 생성:</span><span class="sxs-lookup"><span data-stu-id="25ccf-145">Prior to Web API 2, the Web API project templates generated code like this:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

<span data-ttu-id="25ccf-146">특성 라우팅을 사용 하는 경우이 코드는 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-146">If attribute routing is enabled, this code will throw an exception.</span></span> <span data-ttu-id="25ccf-147">특성 라우팅을 사용 하도록 기존 Web API 프로젝트를 업그레이드 하는 경우이 구성 코드를 다음으로 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-147">If you upgrade an existing Web API project to use attribute routing, make sure to update this configuration code to the following:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> <span data-ttu-id="25ccf-148">자세한 내용은 [ASP.NET 호스트를 사용한 Web API 구성](../advanced/configuring-aspnet-web-api.md#webhost)합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-148">For more information, see [Configuring Web API with ASP.NET Hosting](../advanced/configuring-aspnet-web-api.md#webhost).</span></span>


<a id="add-routes"></a>
## <a name="adding-route-attributes"></a><span data-ttu-id="25ccf-149">경로 특성 추가</span><span class="sxs-lookup"><span data-stu-id="25ccf-149">Adding Route Attributes</span></span>

<span data-ttu-id="25ccf-150">특성을 사용 하 여 정의 하는 경로의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-150">Here is an example of a route defined using an attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

<span data-ttu-id="25ccf-151">문자열 &quot;고객 / {customerId} orders&quot; 경로 대 한 URI 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-151">The string &quot;customers/{customerId}/orders&quot; is the URI template for the route.</span></span> <span data-ttu-id="25ccf-152">Web API 템플릿 요청 URI를 일치 시 키 려 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-152">Web API tries to match the request URI to the template.</span></span> <span data-ttu-id="25ccf-153">이 예제에서는 "customers" 및 "orders"는 리터럴 세그먼트 및 "{customerId}"은 변수 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-153">In this example, "customers" and "orders" are literal segments, and "{customerId}" is a variable parameter.</span></span> <span data-ttu-id="25ccf-154">다음 Uri이이 템플릿을 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-154">The following URIs would match this template:</span></span>

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

<span data-ttu-id="25ccf-155">사용 하 여 일치 하는 것을 제한할 수 있습니다 [제약 조건](#constraints)이 항목의 뒷부분에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-155">You can restrict the matching by using [constraints](#constraints), described later in this topic.</span></span>

<span data-ttu-id="25ccf-156">있음을 합니다 &quot;{customerId}&quot; 경로 템플릿에 매개 변수 이름과 일치 하는 *customerId* 메서드의 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-156">Notice that the &quot;{customerId}&quot; parameter in the route template matches the name of the *customerId* parameter in the method.</span></span> <span data-ttu-id="25ccf-157">Web API 컨트롤러 작업을 호출 하는 경우 경로 매개 변수를 바인딩합니다 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-157">When Web API invokes the controller action, it tries to bind the route parameters.</span></span> <span data-ttu-id="25ccf-158">예를 들어, URI가 `http://example.com/customers/1/orders`, Web API 하려고 "1" 값을 바인딩하는 *customerId* 작업에서 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-158">For example, if the URI is `http://example.com/customers/1/orders`, Web API tries to bind the value "1" to the *customerId* parameter in the action.</span></span>

<span data-ttu-id="25ccf-159">URI 템플릿을 여러 매개 변수를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-159">A URI template can have several parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

<span data-ttu-id="25ccf-160">경로 특성이 없는 컨트롤러 메서드 규칙 기반 라우팅을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-160">Any controller methods that do not have a route attribute use convention-based routing.</span></span> <span data-ttu-id="25ccf-161">이런 방식으로 두 가지 유형의 동일한 프로젝트에서 라우팅을 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-161">That way, you can combine both types of routing in the same project.</span></span>

## <a name="http-methods"></a><span data-ttu-id="25ccf-162">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="25ccf-162">HTTP Methods</span></span>

<span data-ttu-id="25ccf-163">또한 웹 API는 HTTP 메서드 (GET, POST 등) 요청에 따라 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-163">Web API also selects actions based on the HTTP method of the request (GET, POST, etc).</span></span> <span data-ttu-id="25ccf-164">기본적으로 Web API 컨트롤러 메서드 이름의 시작 부분을 사용 하 여 대/소문자 일치 항목을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-164">By default, Web API looks for a case-insensitive match with the start of the controller method name.</span></span> <span data-ttu-id="25ccf-165">예를 들어 컨트롤러 메서드가 `PutCustomers` HTTP PUT 요청을 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-165">For example, a controller method named `PutCustomers` matches an HTTP PUT request.</span></span>

<span data-ttu-id="25ccf-166">재정의할 수 있습니다이 규칙 하나를 사용 하 여 메서드를 데코레이팅하여 다음과 같은 특성.</span><span class="sxs-lookup"><span data-stu-id="25ccf-166">You can override this convention by decorating the method with any the following attributes:</span></span>

- <span data-ttu-id="25ccf-167">**[HttpDelete]**</span><span class="sxs-lookup"><span data-stu-id="25ccf-167">**[HttpDelete]**</span></span>
- <span data-ttu-id="25ccf-168">**[HttpGet]**</span><span class="sxs-lookup"><span data-stu-id="25ccf-168">**[HttpGet]**</span></span>
- <span data-ttu-id="25ccf-169">**[HttpHead]**</span><span class="sxs-lookup"><span data-stu-id="25ccf-169">**[HttpHead]**</span></span>
- <span data-ttu-id="25ccf-170">**[HttpOptions]**</span><span class="sxs-lookup"><span data-stu-id="25ccf-170">**[HttpOptions]**</span></span>
- <span data-ttu-id="25ccf-171">**[HttpPatch]**</span><span class="sxs-lookup"><span data-stu-id="25ccf-171">**[HttpPatch]**</span></span>
- <span data-ttu-id="25ccf-172">**[HttpPost]**</span><span class="sxs-lookup"><span data-stu-id="25ccf-172">**[HttpPost]**</span></span>
- <span data-ttu-id="25ccf-173">**[HttpPut]**</span><span class="sxs-lookup"><span data-stu-id="25ccf-173">**[HttpPut]**</span></span>

<span data-ttu-id="25ccf-174">다음 예제에서는 HTTP POST 요청으로 CreateBook 메서드를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-174">The following example maps the CreateBook method to HTTP POST requests.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

<span data-ttu-id="25ccf-175">다른 모든 HTTP 메서드를 비표준 메서드를 포함 하 여 사용 합니다 **AcceptVerbs** HTTP 메서드 목록을 사용 하는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-175">For all other HTTP methods, including non-standard methods, use the **AcceptVerbs** attribute, which takes a list of HTTP methods.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a><span data-ttu-id="25ccf-176">경로 접두사</span><span class="sxs-lookup"><span data-stu-id="25ccf-176">Route Prefixes</span></span>

<span data-ttu-id="25ccf-177">종종 동일한 접두사로 시작 하는 모든 컨트롤러의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-177">Often, the routes in a controller all start with the same prefix.</span></span> <span data-ttu-id="25ccf-178">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="25ccf-178">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

<span data-ttu-id="25ccf-179">전체 컨트롤러에 대 한 공통 접두사를 사용 하 여 설정할 수 있습니다 합니다 **[RoutePrefix]** 특성:</span><span class="sxs-lookup"><span data-stu-id="25ccf-179">You can set a common prefix for an entire controller by using the **[RoutePrefix]** attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

<span data-ttu-id="25ccf-180">경로 접두사를 재정의 하려면 메서드 특성에 물결표 (~)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-180">Use a tilde (~) on the method attribute to override the route prefix:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

<span data-ttu-id="25ccf-181">경로 접두사는 매개 변수를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-181">The route prefix can include parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a><span data-ttu-id="25ccf-182">경로 제약 조건</span><span class="sxs-lookup"><span data-stu-id="25ccf-182">Route Constraints</span></span>

<span data-ttu-id="25ccf-183">경로 제약 조건은 경로 템플릿에 매개 변수를 일치 시키는 방법을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-183">Route constraints let you restrict how the parameters in the route template are matched.</span></span> <span data-ttu-id="25ccf-184">일반 구문은 &quot;{0} 매개 변수: 제약 조건}&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-184">The general syntax is &quot;{parameter:constraint}&quot;.</span></span> <span data-ttu-id="25ccf-185">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="25ccf-185">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

<span data-ttu-id="25ccf-186">여기에서 첫 번째 경로 경우에 선택할 합니다 &quot;id&quot; URI의 세그먼트는 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-186">Here, the first route will only be selected if the &quot;id&quot; segment of the URI is an integer.</span></span> <span data-ttu-id="25ccf-187">그렇지 않으면 두 번째 경로 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-187">Otherwise, the second route will be chosen.</span></span>

<span data-ttu-id="25ccf-188">다음 표에서 지원 되는 제약 조건을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-188">The following table lists the constraints that are supported.</span></span>

| <span data-ttu-id="25ccf-189">제약 조건</span><span class="sxs-lookup"><span data-stu-id="25ccf-189">Constraint</span></span> | <span data-ttu-id="25ccf-190">설명</span><span class="sxs-lookup"><span data-stu-id="25ccf-190">Description</span></span> | <span data-ttu-id="25ccf-191">예</span><span class="sxs-lookup"><span data-stu-id="25ccf-191">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="25ccf-192">알파</span><span class="sxs-lookup"><span data-stu-id="25ccf-192">alpha</span></span> | <span data-ttu-id="25ccf-193">일치 대문자 또는 소문자로 라틴어 알파벳 문자 (a-z A-z)</span><span class="sxs-lookup"><span data-stu-id="25ccf-193">Matches uppercase or lowercase Latin alphabet characters (a-z, A-Z)</span></span> | <span data-ttu-id="25ccf-194">{x: 알파}</span><span class="sxs-lookup"><span data-stu-id="25ccf-194">{x:alpha}</span></span> |
| <span data-ttu-id="25ccf-195">bool</span><span class="sxs-lookup"><span data-stu-id="25ccf-195">bool</span></span> | <span data-ttu-id="25ccf-196">부울 값과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-196">Matches a Boolean value.</span></span> | <span data-ttu-id="25ccf-197">{x: bool}</span><span class="sxs-lookup"><span data-stu-id="25ccf-197">{x:bool}</span></span> |
| <span data-ttu-id="25ccf-198">datetime</span><span class="sxs-lookup"><span data-stu-id="25ccf-198">datetime</span></span> | <span data-ttu-id="25ccf-199">일치 하는 **날짜/시간** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-199">Matches a **DateTime** value.</span></span> | <span data-ttu-id="25ccf-200">{x:datetime}</span><span class="sxs-lookup"><span data-stu-id="25ccf-200">{x:datetime}</span></span> |
| <span data-ttu-id="25ccf-201">decimal</span><span class="sxs-lookup"><span data-stu-id="25ccf-201">decimal</span></span> | <span data-ttu-id="25ccf-202">10 진수 값과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-202">Matches a decimal value.</span></span> | <span data-ttu-id="25ccf-203">{x:decimal}</span><span class="sxs-lookup"><span data-stu-id="25ccf-203">{x:decimal}</span></span> |
| <span data-ttu-id="25ccf-204">double</span><span class="sxs-lookup"><span data-stu-id="25ccf-204">double</span></span> | <span data-ttu-id="25ccf-205">64 비트 부동 소수점 값과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-205">Matches a 64-bit floating-point value.</span></span> | <span data-ttu-id="25ccf-206">{x:double}</span><span class="sxs-lookup"><span data-stu-id="25ccf-206">{x:double}</span></span> |
| <span data-ttu-id="25ccf-207">float</span><span class="sxs-lookup"><span data-stu-id="25ccf-207">float</span></span> | <span data-ttu-id="25ccf-208">32 비트 부동 소수점 값과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-208">Matches a 32-bit floating-point value.</span></span> | <span data-ttu-id="25ccf-209">{x: float}</span><span class="sxs-lookup"><span data-stu-id="25ccf-209">{x:float}</span></span> |
| <span data-ttu-id="25ccf-210">guid</span><span class="sxs-lookup"><span data-stu-id="25ccf-210">guid</span></span> | <span data-ttu-id="25ccf-211">GUID 값과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-211">Matches a GUID value.</span></span> | <span data-ttu-id="25ccf-212">{x: guid}</span><span class="sxs-lookup"><span data-stu-id="25ccf-212">{x:guid}</span></span> |
| <span data-ttu-id="25ccf-213">int</span><span class="sxs-lookup"><span data-stu-id="25ccf-213">int</span></span> | <span data-ttu-id="25ccf-214">32 비트 정수 값과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-214">Matches a 32-bit integer value.</span></span> | <span data-ttu-id="25ccf-215">{x: int}</span><span class="sxs-lookup"><span data-stu-id="25ccf-215">{x:int}</span></span> |
| <span data-ttu-id="25ccf-216">길이</span><span class="sxs-lookup"><span data-stu-id="25ccf-216">length</span></span> | <span data-ttu-id="25ccf-217">지정된 된 길이 사용 하 여 또는 길이의 지정된 된 범위 내의 문자열과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-217">Matches a string with the specified length or within a specified range of lengths.</span></span> | <span data-ttu-id="25ccf-218">{x: length(6)} {x: length(1,20)}</span><span class="sxs-lookup"><span data-stu-id="25ccf-218">{x:length(6)} {x:length(1,20)}</span></span> |
| <span data-ttu-id="25ccf-219">long</span><span class="sxs-lookup"><span data-stu-id="25ccf-219">long</span></span> | <span data-ttu-id="25ccf-220">64 비트 정수 값과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-220">Matches a 64-bit integer value.</span></span> | <span data-ttu-id="25ccf-221">{x: 장기}</span><span class="sxs-lookup"><span data-stu-id="25ccf-221">{x:long}</span></span> |
| <span data-ttu-id="25ccf-222">max</span><span class="sxs-lookup"><span data-stu-id="25ccf-222">max</span></span> | <span data-ttu-id="25ccf-223">정수 최대값을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-223">Matches an integer with a maximum value.</span></span> | <span data-ttu-id="25ccf-224">{x:max(10)}</span><span class="sxs-lookup"><span data-stu-id="25ccf-224">{x:max(10)}</span></span> |
| <span data-ttu-id="25ccf-225">maxlength</span><span class="sxs-lookup"><span data-stu-id="25ccf-225">maxlength</span></span> | <span data-ttu-id="25ccf-226">최대 길이 사용 하 여 문자열과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-226">Matches a string with a maximum length.</span></span> | <span data-ttu-id="25ccf-227">{x:maxlength(10)}</span><span class="sxs-lookup"><span data-stu-id="25ccf-227">{x:maxlength(10)}</span></span> |
| <span data-ttu-id="25ccf-228">분</span><span class="sxs-lookup"><span data-stu-id="25ccf-228">min</span></span> | <span data-ttu-id="25ccf-229">정수 최소값을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-229">Matches an integer with a minimum value.</span></span> | <span data-ttu-id="25ccf-230">{x:min(10)}</span><span class="sxs-lookup"><span data-stu-id="25ccf-230">{x:min(10)}</span></span> |
| <span data-ttu-id="25ccf-231">minlength</span><span class="sxs-lookup"><span data-stu-id="25ccf-231">minlength</span></span> | <span data-ttu-id="25ccf-232">최소 길이 사용 하 여 문자열과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-232">Matches a string with a minimum length.</span></span> | <span data-ttu-id="25ccf-233">{x: minlength(10)}</span><span class="sxs-lookup"><span data-stu-id="25ccf-233">{x:minlength(10)}</span></span> |
| <span data-ttu-id="25ccf-234">range</span><span class="sxs-lookup"><span data-stu-id="25ccf-234">range</span></span> | <span data-ttu-id="25ccf-235">정수 값의 범위 내에서 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-235">Matches an integer within a range of values.</span></span> | <span data-ttu-id="25ccf-236">{x: range(10,50)}</span><span class="sxs-lookup"><span data-stu-id="25ccf-236">{x:range(10,50)}</span></span> |
| <span data-ttu-id="25ccf-237">정규식</span><span class="sxs-lookup"><span data-stu-id="25ccf-237">regex</span></span> | <span data-ttu-id="25ccf-238">정규식과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-238">Matches a regular expression.</span></span> | <span data-ttu-id="25ccf-239">{x: regex(^\d{3}-\d{3}-\d{4}$)}</span><span class="sxs-lookup"><span data-stu-id="25ccf-239">{x:regex(^\d{3}-\d{3}-\d{4}$)}</span></span> |

<span data-ttu-id="25ccf-240">알림 제약 조건 중 일부는 같은 &quot;min&quot;, 괄호 안에 인수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-240">Notice that some of the constraints, such as &quot;min&quot;, take arguments in parentheses.</span></span> <span data-ttu-id="25ccf-241">콜론으로 구분 된 매개 변수에 여러 제약 조건을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-241">You can apply multiple constraints to a parameter, separated by a colon.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a><span data-ttu-id="25ccf-242">사용자 지정 경로 제약 조건</span><span class="sxs-lookup"><span data-stu-id="25ccf-242">Custom Route Constraints</span></span>

<span data-ttu-id="25ccf-243">구현 하 여 사용자 지정 경로 제약 조건을 만들 수 있습니다 합니다 **IHttpRouteConstraint** 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-243">You can create custom route constraints by implementing the **IHttpRouteConstraint** interface.</span></span> <span data-ttu-id="25ccf-244">예를 들어, 다음 제약 조건이 0이 아닌 정수 값으로 매개 변수를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-244">For example, the following constraint restricts a parameter to a non-zero integer value.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

<span data-ttu-id="25ccf-245">다음 코드에는 제약 조건을 등록 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-245">The following code shows how to register the constraint:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

<span data-ttu-id="25ccf-246">이제 경로에서 제약 조건을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-246">Now you can apply the constraint in your routes:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

<span data-ttu-id="25ccf-247">전체를 바꿀 수도 있습니다 **DefaultInlineConstraintResolver** 구현 하 여 클래스를 **IInlineConstraintResolver** 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-247">You can also replace the entire **DefaultInlineConstraintResolver** class by implementing the **IInlineConstraintResolver** interface.</span></span> <span data-ttu-id="25ccf-248">이렇게 바뀝니다 모든 기본 제약 조건, 하지 않는 한 구현의 **IInlineConstraintResolver** 구체적으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-248">Doing so will replace all of the built-in constraints, unless your implementation of **IInlineConstraintResolver** specifically adds them.</span></span>

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a><span data-ttu-id="25ccf-249">선택적 URI 매개 변수 및 기본 값</span><span class="sxs-lookup"><span data-stu-id="25ccf-249">Optional URI Parameters and Default Values</span></span>

<span data-ttu-id="25ccf-250">선택적 URI 매개 변수를 경로 매개 변수를 매개 변수를 추가 하 여 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-250">You can make a URI parameter optional by adding a question mark to the route parameter.</span></span> <span data-ttu-id="25ccf-251">경로 매개 변수는 선택 사항, 메서드 매개 변수의 기본값을 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-251">If a route parameter is optional, you must define a default value for the method parameter.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

<span data-ttu-id="25ccf-252">이 예에서 `/api/books/locale/1033` 고 `/api/books/locale` 동일한 리소스를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-252">In this example, `/api/books/locale/1033` and `/api/books/locale` return the same resource.</span></span>

<span data-ttu-id="25ccf-253">또는 경로 템플릿 내에서 기본 값을 다음과 같이 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-253">Alternatively, you can specify a default value inside the route template, as follows:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

<span data-ttu-id="25ccf-254">이전 예제와 거의 동일 하지만 기본값 적용 될 때 동작의 약간의 차이점이 있을 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-254">This is almost the same as the previous example, but there is a slight difference of behavior when the default value is applied.</span></span>

- <span data-ttu-id="25ccf-255">첫 번째 예에서 ("{lcid?}") 매개 변수는 정확한 값이 있으므로 1033의 기본값은 메서드 매개 변수를 직접 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-255">In the first example ("{lcid?}"), the default value of 1033 is assigned directly to the method parameter, so the parameter will have this exact value.</span></span>
- <span data-ttu-id="25ccf-256">두 번째 예제에서 ("{lcid 1033 =}"), 기본값인 "1033" 모델 바인딩 프로세스를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-256">In the second example ("{lcid=1033}"), the default value of "1033" goes through the model-binding process.</span></span> <span data-ttu-id="25ccf-257">기본 모델 바인더를 숫자 값 1033 "1033"로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-257">The default model-binder will convert "1033" to the numeric value 1033.</span></span> <span data-ttu-id="25ccf-258">그러나 다른 작업을 수행할 수 있는 사용자 지정 모델 바인더에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-258">However, you could plug in a custom model binder, which might do something different.</span></span>

<span data-ttu-id="25ccf-259">(대부분의 경우에서 파이프라인에서 사용자 지정 모델 바인더 경우가 아니라면 두 형식의 해당 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="25ccf-259">(In most cases, unless you have custom model binders in your pipeline, the two forms will be equivalent.)</span></span>

<a id="route-names"></a>
## <a name="route-names"></a><span data-ttu-id="25ccf-260">경로 이름</span><span class="sxs-lookup"><span data-stu-id="25ccf-260">Route Names</span></span>

<span data-ttu-id="25ccf-261">Web API에서 모든 경로는 이름이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-261">In Web API, every route has a name.</span></span> <span data-ttu-id="25ccf-262">경로 이름은 HTTP 응답의 링크를 포함할 수 있도록 링크를 생성할 때 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-262">Route names are useful for generating links, so that you can include a link in an HTTP response.</span></span>

<span data-ttu-id="25ccf-263">경로 이름을 지정 하려면 설정 합니다 **이름** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-263">To specify the route name, set the **Name** property on the attribute.</span></span> <span data-ttu-id="25ccf-264">다음 예제에서는 경로 이름을 설정 하는 방법 및 링크를 생성 하는 경우 경로 이름을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-264">The following example shows how to set the route name, and also how to use the route name when generating a link.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a><span data-ttu-id="25ccf-265">경로 순서</span><span class="sxs-lookup"><span data-stu-id="25ccf-265">Route Order</span></span>

<span data-ttu-id="25ccf-266">프레임 워크 경로 사용 하 여 URI를 찾으려고 하는 경우에 특정 순서 대로 경로 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-266">When the framework tries to match a URI with a route, it evaluates the routes in a particular order.</span></span> <span data-ttu-id="25ccf-267">순서를 지정 하려면 설정 합니다 **RouteOrder** 속성 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-267">To specify the order, set the **RouteOrder** property on the route attribute.</span></span> <span data-ttu-id="25ccf-268">값이 낮을수록 먼저 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-268">Lower values are evaluated first.</span></span> <span data-ttu-id="25ccf-269">기본 순서 값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-269">The default order value is zero.</span></span>

<span data-ttu-id="25ccf-270">전체 순서를 결정 하는 방법을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-270">Here is how the total ordering is determined:</span></span>

1. <span data-ttu-id="25ccf-271">비교는 **RouteOrder** 경로 특성의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-271">Compare the **RouteOrder** property of the route attribute.</span></span>
2. <span data-ttu-id="25ccf-272">경로 템플릿에 각 URI 세그먼트를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-272">Look at each URI segment in the route template.</span></span> <span data-ttu-id="25ccf-273">각 세그먼트에 대 한 다음과 같은 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-273">For each segment, order as follows:</span></span> 

    1. <span data-ttu-id="25ccf-274">리터럴 세그먼트입니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-274">Literal segments.</span></span>
    2. <span data-ttu-id="25ccf-275">제약 조건으로 경로 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-275">Route parameters with constraints.</span></span>
    3. <span data-ttu-id="25ccf-276">제약 조건 없이 경로 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-276">Route parameters without constraints.</span></span>
    4. <span data-ttu-id="25ccf-277">제약 조건 사용 하 여 와일드 카드 매개 변수 세그먼트입니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-277">Wildcard parameter segments with constraints.</span></span>
    5. <span data-ttu-id="25ccf-278">제약 조건 없이 와일드 카드 매개 변수 세그먼트입니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-278">Wildcard parameter segments without constraints.</span></span>
3. <span data-ttu-id="25ccf-279">동률의 경우 경로 대/소문자는 서 수 문자열 비교로 정렬 됩니다 ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx))의 경로 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-279">In the case of a tie, routes are ordered by a case-insensitive ordinal string comparison ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) of the route template.</span></span>

<span data-ttu-id="25ccf-280">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-280">Here is an example.</span></span> <span data-ttu-id="25ccf-281">다음 컨트롤러를 정의 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-281">Suppose you define the following controller:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

<span data-ttu-id="25ccf-282">이러한 경로 다음과 같이 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-282">These routes are ordered as follows.</span></span>

1. <span data-ttu-id="25ccf-283">주문/세부 정보</span><span class="sxs-lookup"><span data-stu-id="25ccf-283">orders/details</span></span>
2. <span data-ttu-id="25ccf-284">주문 / {id}</span><span class="sxs-lookup"><span data-stu-id="25ccf-284">orders/{id}</span></span>
3. <span data-ttu-id="25ccf-285">orders/{customerName}</span><span class="sxs-lookup"><span data-stu-id="25ccf-285">orders/{customerName}</span></span>
4. <span data-ttu-id="25ccf-286">orders/{\*date}</span><span class="sxs-lookup"><span data-stu-id="25ccf-286">orders/{\*date}</span></span>
5. <span data-ttu-id="25ccf-287">orders/pending</span><span class="sxs-lookup"><span data-stu-id="25ccf-287">orders/pending</span></span>

<span data-ttu-id="25ccf-288">"Details" 리터럴 세그먼트 "{id}" 앞에 나타나는 있지만 "pending" 마지막으로 때문에 표시 됩니다 하는 **RouteOrder** 속성은 1입니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-288">Notice that "details" is a literal segment and appears before "{id}", but "pending" appears last because the **RouteOrder** property is 1.</span></span> <span data-ttu-id="25ccf-289">(이 예에서는 고객이 없는 "details" 라고 가정 있습니다 "보류 중" 또는 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-289">(This example assumes there are no customers named "details" or "pending".</span></span> <span data-ttu-id="25ccf-290">일반적으로 모호한 경로가 것을 방지 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="25ccf-290">In general, try to avoid ambiguous routes.</span></span> <span data-ttu-id="25ccf-291">이 예에 대 한 더 나은 경로 템플릿 `GetByCustomer` 는 "customers / {customerName}")</span><span class="sxs-lookup"><span data-stu-id="25ccf-291">In this example, a better route template for `GetByCustomer` is "customers/{customerName}" )</span></span>
