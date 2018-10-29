---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: ASP.NET Web API에서에서 라우팅 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/29/2018
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: a7bc998fc23c0453fc9cd6ac1e7b9af7bd516225
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50207305"
---
<a name="routing-in-aspnet-web-api"></a><span data-ttu-id="2d3dc-102">ASP.NET Web API에서 라우팅</span><span class="sxs-lookup"><span data-stu-id="2d3dc-102">Routing in ASP.NET Web API</span></span>
====================
<span data-ttu-id="2d3dc-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2d3dc-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="2d3dc-104">이 문서에서는 ASP.NET Web API 컨트롤러에 HTTP 요청을 라우팅합니다 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-104">This article describes how ASP.NET Web API routes HTTP requests to controllers.</span></span>

> [!NOTE]
> <span data-ttu-id="2d3dc-105">ASP.NET MVC에 익숙한 경우에 Web API 라우팅는 MVC 라우팅 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-105">If you are familiar with ASP.NET MVC, Web API routing is very similar to MVC routing.</span></span> <span data-ttu-id="2d3dc-106">주요 차이점은 Web API HTTP 동사에 URI 경로 사용 하 여 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-106">The main difference is that Web API uses the HTTP verb, not the URI path, to select the action.</span></span> <span data-ttu-id="2d3dc-107">MVC 스타일 라우팅 Web API에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-107">You can also use MVC-style routing in Web API.</span></span> <span data-ttu-id="2d3dc-108">이 문서는 ASP.NET MVC에 대 한 정보를 가정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-108">This article does not assume any knowledge of ASP.NET MVC.</span></span>

## <a name="routing-tables"></a><span data-ttu-id="2d3dc-109">라우팅 테이블</span><span class="sxs-lookup"><span data-stu-id="2d3dc-109">Routing Tables</span></span>

<span data-ttu-id="2d3dc-110">ASP.NET Web API에는 *컨트롤러* 는 HTTP 요청을 처리 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-110">In ASP.NET Web API, a *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="2d3dc-111">컨트롤러의 공용 메서드 호출 됩니다 *작업 메서드에* 있거나 단순히 *작업*합니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-111">The public methods of the controller are called *action methods* or simply *actions*.</span></span> <span data-ttu-id="2d3dc-112">Web API 프레임 워크는 요청을 받으면 요청을 작업에 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-112">When the Web API framework receives a request, it routes the request to an action.</span></span>

<span data-ttu-id="2d3dc-113">호출 하는 작업을 확인 하려면 프레임 워크를 사용 하는 *라우팅 테이블*합니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-113">To determine which action to invoke, the framework uses a *routing table*.</span></span> <span data-ttu-id="2d3dc-114">Visual Studio 프로젝트 템플릿을 웹 API에 대 한 기본 경로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-114">The Visual Studio project template for Web API creates a default route:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="2d3dc-115">이 경로에 정의 되어는 *WebApiConfig.cs* 에 배치 되는 파일을 *앱\_시작* 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="2d3dc-115">This route is defined in the *WebApiConfig.cs* file, which is placed in the *App\_Start* directory:</span></span>

![](routing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="2d3dc-116">에 대 한 자세한 내용은 합니다 `WebApiConfig` 클래스를 참조 하십시오 [ASP.NET Web API 구성](../advanced/configuring-aspnet-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-116">For more information about the `WebApiConfig` class, see [Configuring ASP.NET Web API](../advanced/configuring-aspnet-web-api.md).</span></span>

<span data-ttu-id="2d3dc-117">라우팅 테이블에서 직접 설정 해야 Web API를 자체 호스트 하는 경우는 `HttpSelfHostConfiguration` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-117">If you self-host Web API, you must set the routing table directly on the `HttpSelfHostConfiguration` object.</span></span> <span data-ttu-id="2d3dc-118">자세한 내용은 [Web API를 자체 호스팅하는](../older-versions/self-host-a-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-118">For more information, see [Self-Host a Web API](../older-versions/self-host-a-web-api.md).</span></span>

<span data-ttu-id="2d3dc-119">라우팅 테이블의 각 항목에 포함 된 *경로 템플릿을*합니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-119">Each entry in the routing table contains a *route template*.</span></span> <span data-ttu-id="2d3dc-120">웹 API에 대 한 기본 경로 템플릿은 &quot;api / {컨트롤러} / {id}&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-120">The default route template for Web API is &quot;api/{controller}/{id}&quot;.</span></span> <span data-ttu-id="2d3dc-121">이 템플릿에서 &quot;api&quot; 리터럴 경로 세그먼트 및 {컨트롤러}, {id}는 자리 표시자 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-121">In this template, &quot;api&quot; is a literal path segment, and {controller} and {id} are placeholder variables.</span></span>

<span data-ttu-id="2d3dc-122">Web API 프레임 워크는 HTTP 요청을 받으면 라우팅 테이블에 경로 템플릿 중 하나에 대 한 URI를 일치 시 키 려 고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-122">When the Web API framework receives an HTTP request, it tries to match the URI against one of the route templates in the routing table.</span></span> <span data-ttu-id="2d3dc-123">경로가 일치 하는 경우 클라이언트는 404 오류를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-123">If no route matches, the client receives a 404 error.</span></span> <span data-ttu-id="2d3dc-124">예를 들어, 다음 Uri는 기본 경로 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-124">For example, the following URIs match the default route:</span></span>

- <span data-ttu-id="2d3dc-125">api 연락처</span><span class="sxs-lookup"><span data-stu-id="2d3dc-125">/api/contacts</span></span>
- <span data-ttu-id="2d3dc-126">/api/contacts/1</span><span class="sxs-lookup"><span data-stu-id="2d3dc-126">/api/contacts/1</span></span>
- <span data-ttu-id="2d3dc-127">/api/products/gizmo1</span><span class="sxs-lookup"><span data-stu-id="2d3dc-127">/api/products/gizmo1</span></span>

<span data-ttu-id="2d3dc-128">그러나 다음 URI와 일치 하지 않으면 포함 하지 않으므로 합니다 &quot;api&quot; 세그먼트:</span><span class="sxs-lookup"><span data-stu-id="2d3dc-128">However, the following URI does not match, because it lacks the &quot;api&quot; segment:</span></span>

- <span data-ttu-id="2d3dc-129">/ contacts/1</span><span class="sxs-lookup"><span data-stu-id="2d3dc-129">/contacts/1</span></span>

> [!NOTE]
> <span data-ttu-id="2d3dc-130">경로에 "api"를 사용 하는 이유는 ASP.NET MVC 라우팅를 사용 하 여 충돌을 방지 하기 위해서입니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-130">The reason for using "api" in the route is to avoid collisions with ASP.NET MVC routing.</span></span> <span data-ttu-id="2d3dc-131">이렇게 할 수 있습니다 &quot;연결/&quot; MVC 컨트롤러로 이동 하 고 &quot;/api/contacts&quot; Web API 컨트롤러를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-131">That way, you can have &quot;/contacts&quot; go to an MVC controller, and &quot;/api/contacts&quot; go to a Web API controller.</span></span> <span data-ttu-id="2d3dc-132">물론,이 규칙을 마음에 들지 않는 경우 기본 경로 테이블을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-132">Of course, if you don't like this convention, you can change the default route table.</span></span>

<span data-ttu-id="2d3dc-133">일치 하는 경로가 발견 되 면 Web API 컨트롤러 및 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-133">Once a matching route is found, Web API selects the controller and the action:</span></span>

- <span data-ttu-id="2d3dc-134">Web API 컨트롤러를 찾으려면 추가 &quot;컨트롤러&quot; 의 값을 *{컨트롤러}* 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-134">To find the controller, Web API adds &quot;Controller&quot; to the value of the *{controller}* variable.</span></span>
- <span data-ttu-id="2d3dc-135">작업을 찾으려면 Web API HTTP 동사를 살펴보고 및 해당 HTTP 동사 이름으로 시작 하는 작업을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-135">To find the action, Web API looks at the HTTP verb, and then looks for an action whose name begins with that HTTP verb name.</span></span> <span data-ttu-id="2d3dc-136">예를 들어 GET 요청을 사용 하 여 웹 API가 접두사로 추가 작업에 대 한 &quot;가져옵니다&quot;와 같은 &quot;GetContact&quot; 하거나 &quot;GetAllContacts&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-136">For example, with a GET request, Web API looks for an action prefixed with &quot;Get&quot;, such as &quot;GetContact&quot; or &quot;GetAllContacts&quot;.</span></span> <span data-ttu-id="2d3dc-137">이 규칙 GET, POST, PUT, DELETE, HEAD, 옵션 및 PATCH 동사에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-137">This convention applies only to GET, POST, PUT, DELETE, HEAD, OPTIONS, and PATCH verbs.</span></span> <span data-ttu-id="2d3dc-138">컨트롤러에서 특성을 사용 하 여 다른 HTTP 동사를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-138">You can enable other HTTP verbs by using attributes on your controller.</span></span> <span data-ttu-id="2d3dc-139">뒷부분의 예제를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-139">We'll see an example of that later.</span></span>
- <span data-ttu-id="2d3dc-140">경로 템플릿에서 다른 자리 표시자 변수가 같은 *{id}* 작업 매개 변수에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-140">Other placeholder variables in the route template, such as *{id},* are mapped to action parameters.</span></span>

<span data-ttu-id="2d3dc-141">예를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-141">Let's look at an example.</span></span> <span data-ttu-id="2d3dc-142">다음 컨트롤러를 정의 하는 것을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-142">Suppose that you define the following controller:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="2d3dc-143">각각에 대해 호출 되는 동작과 함께 몇 가지 가능한 HTTP 요청을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-143">Here are some possible HTTP requests, along with the action that gets invoked for each:</span></span>

| <span data-ttu-id="2d3dc-144">HTTP 동사</span><span class="sxs-lookup"><span data-stu-id="2d3dc-144">HTTP Verb</span></span> | <span data-ttu-id="2d3dc-145">URI 경로</span><span class="sxs-lookup"><span data-stu-id="2d3dc-145">URI Path</span></span> | <span data-ttu-id="2d3dc-146">작업</span><span class="sxs-lookup"><span data-stu-id="2d3dc-146">Action</span></span> | <span data-ttu-id="2d3dc-147">매개 변수</span><span class="sxs-lookup"><span data-stu-id="2d3dc-147">Parameter</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2d3dc-148">가져오기</span><span class="sxs-lookup"><span data-stu-id="2d3dc-148">GET</span></span> | <span data-ttu-id="2d3dc-149">api/제품</span><span class="sxs-lookup"><span data-stu-id="2d3dc-149">api/products</span></span> | <span data-ttu-id="2d3dc-150">GetAllProducts</span><span class="sxs-lookup"><span data-stu-id="2d3dc-150">GetAllProducts</span></span> | <span data-ttu-id="2d3dc-151">*(없음)*</span><span class="sxs-lookup"><span data-stu-id="2d3dc-151">*(none)*</span></span> |
| <span data-ttu-id="2d3dc-152">가져오기</span><span class="sxs-lookup"><span data-stu-id="2d3dc-152">GET</span></span> | <span data-ttu-id="2d3dc-153">api/제품/4</span><span class="sxs-lookup"><span data-stu-id="2d3dc-153">api/products/4</span></span> | <span data-ttu-id="2d3dc-154">GetProductById</span><span class="sxs-lookup"><span data-stu-id="2d3dc-154">GetProductById</span></span> | <span data-ttu-id="2d3dc-155">4</span><span class="sxs-lookup"><span data-stu-id="2d3dc-155">4</span></span> |
| <span data-ttu-id="2d3dc-156">Delete</span><span class="sxs-lookup"><span data-stu-id="2d3dc-156">DELETE</span></span> | <span data-ttu-id="2d3dc-157">api/제품/4</span><span class="sxs-lookup"><span data-stu-id="2d3dc-157">api/products/4</span></span> | <span data-ttu-id="2d3dc-158">DeleteProduct</span><span class="sxs-lookup"><span data-stu-id="2d3dc-158">DeleteProduct</span></span> | <span data-ttu-id="2d3dc-159">4</span><span class="sxs-lookup"><span data-stu-id="2d3dc-159">4</span></span> |
| <span data-ttu-id="2d3dc-160">올리기</span><span class="sxs-lookup"><span data-stu-id="2d3dc-160">POST</span></span> | <span data-ttu-id="2d3dc-161">api/제품</span><span class="sxs-lookup"><span data-stu-id="2d3dc-161">api/products</span></span> | <span data-ttu-id="2d3dc-162">*(일치)*</span><span class="sxs-lookup"><span data-stu-id="2d3dc-162">*(no match)*</span></span> |  |

<span data-ttu-id="2d3dc-163">있음을 합니다 *{id}* URI의 세그먼트가 있는 경우에 매핑되는 *id* 동작의 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-163">Notice that the *{id}* segment of the URI, if present, is mapped to the *id* parameter of the action.</span></span> <span data-ttu-id="2d3dc-164">이 예제에서는 컨트롤러 정의 된 하나 두 개의 GET 메서드를 *id* 매개 변수 및 매개 변수 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-164">In this example, the controller defines two GET methods, one with an *id* parameter and one with no parameters.</span></span>

<span data-ttu-id="2d3dc-165">또한 컨트롤러에서 정의 하지 않으므로 POST 요청은 실패 하는 참고를 &quot;Post 하는 중... &quot; 메서드.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-165">Also, note that the POST request will fail, because the controller does not define a &quot;Post...&quot; method.</span></span>

## <a name="routing-variations"></a><span data-ttu-id="2d3dc-166">라우팅 변형</span><span class="sxs-lookup"><span data-stu-id="2d3dc-166">Routing Variations</span></span>

<span data-ttu-id="2d3dc-167">이전 섹션에서는 ASP.NET Web API에 대 한 기본 라우팅 메커니즘을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-167">The previous section described the basic routing mechanism for ASP.NET Web API.</span></span> <span data-ttu-id="2d3dc-168">이 섹션에서는 일부 변형을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-168">This section describes some variations.</span></span>

### <a name="http-verbs"></a><span data-ttu-id="2d3dc-169">HTTP 동사</span><span class="sxs-lookup"><span data-stu-id="2d3dc-169">HTTP verbs</span></span>

<span data-ttu-id="2d3dc-170">HTTP 동사에 대 한 명명 규칙을 사용 하는 대신 다음과 같은 특성 중 하나를 사용 하 여 동작 메서드를 데코레이팅하여 액션에 대 한 HTTP 동사를 명시적으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-170">Instead of using the naming convention for HTTP verbs, you can explicitly specify the HTTP verb for an action by decorating the action method with one of the following attributes:</span></span>

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

<span data-ttu-id="2d3dc-171">다음 예에서 `FindProduct` 메서드는 GET 요청에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-171">In the following example, the `FindProduct` method is mapped to GET requests:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="2d3dc-172">작업에 대 한 여러 HTTP 동사를 허용 하거나 GET, PUT, POST, DELETE, HEAD, 옵션 및 패치 이외의 HTTP 동사를 허용 하려면 사용 된 `[AcceptVerbs]` HTTP 동사 목록을 사용 하는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-172">To allow multiple HTTP verbs for an action, or to allow HTTP verbs other than GET, PUT, POST, DELETE, HEAD, OPTIONS, and PATCH, use the `[AcceptVerbs]` attribute, which takes a list of HTTP verbs.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a><span data-ttu-id="2d3dc-173">작업 이름으로 라우팅</span><span class="sxs-lookup"><span data-stu-id="2d3dc-173">Routing by Action Name</span></span>

<span data-ttu-id="2d3dc-174">기본 라우팅 템플릿이 Web API를 사용 하 여 HTTP 동사 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-174">With the default routing template, Web API uses the HTTP verb to select the action.</span></span> <span data-ttu-id="2d3dc-175">그러나 작업 이름이 URI에 포함 되어 있는 경로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-175">However, you can also create a route where the action name is included in the URI:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="2d3dc-176">이 경로 템플릿에서 합니다 *{action}* 매개 변수는 컨트롤러에 대 한 작업 메서드 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-176">In this route template, the *{action}* parameter names the action method on the controller.</span></span> <span data-ttu-id="2d3dc-177">라우팅의이 스타일을 사용 하 여 허용 되는 HTTP 동사를 지정 하려면 특성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-177">With this style of routing, use attributes to specify the allowed HTTP verbs.</span></span> <span data-ttu-id="2d3dc-178">예를 들어 컨트롤러에는 다음 메서드도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-178">For example, suppose your controller has the following method:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="2d3dc-179">이 경우 "api/제품/세부 정보/1"에 대 한 GET 요청은 매핑되는 `Details` 메서드.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-179">In this case, a GET request for "api/products/details/1" would map to the `Details` method.</span></span> <span data-ttu-id="2d3dc-180">라우팅의이 스타일은 ASP.NET MVC 유사 하며 RPC 스타일 API에 대 한 적절 한 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-180">This style of routing is similar to ASP.NET MVC, and may be appropriate for an RPC-style API.</span></span>

<span data-ttu-id="2d3dc-181">작업 이름을 사용 하 여 재정의할 수 있습니다는 `[ActionName]` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-181">You can override the action name by using the `[ActionName]` attribute.</span></span> <span data-ttu-id="2d3dc-182">다음 예에 매핑되는 두 가지 작업 &quot;미리 보기 제품/api / /*id*합니다. 도구가 지 원하는 GET 및 POST를 지원:</span><span class="sxs-lookup"><span data-stu-id="2d3dc-182">In the following example, there are two actions that map to &quot;api/products/thumbnail/*id*. One supports GET and the other supports POST:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a><span data-ttu-id="2d3dc-183">비 작업</span><span class="sxs-lookup"><span data-stu-id="2d3dc-183">Non-Actions</span></span>

<span data-ttu-id="2d3dc-184">메서드를 작업으로 호출 되지 않도록 하려면 사용 된 `[NonAction]` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-184">To prevent a method from getting invoked as an action, use the `[NonAction]` attribute.</span></span> <span data-ttu-id="2d3dc-185">이 신호를 프레임 워크 메서드가 작업을 그렇지 않으면 라우팅 규칙과 일치 하는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-185">This signals to the framework that the method is not an action, even if it would otherwise match the routing rules.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a><span data-ttu-id="2d3dc-186">추가 정보</span><span class="sxs-lookup"><span data-stu-id="2d3dc-186">Further Reading</span></span>

<span data-ttu-id="2d3dc-187">이 항목에서는 라우팅의 상위 수준 보기를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-187">This topic provided a high-level view of routing.</span></span> <span data-ttu-id="2d3dc-188">자세한 내용을 참조 하세요 [라우팅 및 작업 선택](routing-and-action-selection.md)는 정확 하 게 하는 방법을 설명 프레임 워크는 경로에 URI와 일치, 컨트롤러를 선택 합니다. 그런 다음 호출할 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2d3dc-188">For more detail, see [Routing and Action Selection](routing-and-action-selection.md), which describes exactly how the framework matches a URI to a route, selects a controller, and then selects the action to invoke.</span></span>
