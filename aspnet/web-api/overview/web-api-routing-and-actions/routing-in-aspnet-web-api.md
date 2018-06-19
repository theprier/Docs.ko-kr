---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: ASP.NET Web API의에서 라우팅 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/11/2012
ms.topic: article
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: aa0ecc96029051fef6a81ac08f7fcf52a24de59c
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
ms.locfileid: "26509262"
---
<a name="routing-in-aspnet-web-api"></a><span data-ttu-id="3b96c-102">ASP.NET Web API의 라우팅</span><span class="sxs-lookup"><span data-stu-id="3b96c-102">Routing in ASP.NET Web API</span></span>
====================
<span data-ttu-id="3b96c-103">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="3b96c-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="3b96c-104">이 문서에서는 ASP.NET Web API 컨트롤러를 HTTP 요청을 라우팅하 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-104">This article describes how ASP.NET Web API routes HTTP requests to controllers.</span></span>

> [!NOTE]
> <span data-ttu-id="3b96c-105">ASP.NET MVC에 익숙한 경우 Web API 라우팅는 MVC 라우팅 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-105">If you are familiar with ASP.NET MVC, Web API routing is very similar to MVC routing.</span></span> <span data-ttu-id="3b96c-106">주요 차이점은 Web API HTTP 메서드를 URI 경로 사용 하 여 작업 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-106">The main difference is that Web API uses the HTTP method, not the URI path, to select the action.</span></span> <span data-ttu-id="3b96c-107">MVC 스타일 라우팅 Web API에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-107">You can also use MVC-style routing in Web API.</span></span> <span data-ttu-id="3b96c-108">이 문서는 ASP.NET MVC에 대 한 정보를 상속 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-108">This article does not assume any knowledge of ASP.NET MVC.</span></span>


## <a name="routing-tables"></a><span data-ttu-id="3b96c-109">라우팅 테이블</span><span class="sxs-lookup"><span data-stu-id="3b96c-109">Routing Tables</span></span>

<span data-ttu-id="3b96c-110">ASP.NET Web API에는 *컨트롤러* 는 HTTP 요청을 처리 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-110">In ASP.NET Web API, a *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="3b96c-111">컨트롤러의 공용 메서드를 라고 *작업 메서드* 또는 단순히 *동작*합니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-111">The public methods of the controller are called *action methods* or simply *actions*.</span></span> <span data-ttu-id="3b96c-112">Web API 프레임 워크는 요청을 받으면 요청을 동작을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-112">When the Web API framework receives a request, it routes the request to an action.</span></span>

<span data-ttu-id="3b96c-113">프레임 워크에서 호출 하는 동작을 확인 하려면 다음을 사용 합니다.는 *라우팅 테이블*합니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-113">To determine which action to invoke, the framework uses a *routing table*.</span></span> <span data-ttu-id="3b96c-114">웹 API에 대 한 Visual Studio 프로젝트 템플릿은 기본 경로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-114">The Visual Studio project template for Web API creates a default route:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="3b96c-115">이 경로 응용 프로그램에 있는 WebApiConfig.cs 파일에 정의 된\_시작 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="3b96c-115">This route is defined in the WebApiConfig.cs file, which is placed in the App\_Start directory:</span></span>

![](routing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="3b96c-116">에 대 한 자세한 내용은 **경우 WebApiConfig** 클래스를 참조 하십시오. [ASP.NET Web API 구성](../advanced/configuring-aspnet-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-116">For more information about the **WebApiConfig** class, see [Configuring ASP.NET Web API](../advanced/configuring-aspnet-web-api.md).</span></span>

<span data-ttu-id="3b96c-117">라우팅 테이블에 직접 설정 해야 자체 웹 API를 호스트 하는 경우는 **HttpSelfHostConfiguration** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-117">If you self-host Web API, you must set the routing table directly on the **HttpSelfHostConfiguration** object.</span></span> <span data-ttu-id="3b96c-118">자세한 내용은 참조 [자체 호스트 하는 Web API](../older-versions/self-host-a-web-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-118">For more information, see [Self-Host a Web API](../older-versions/self-host-a-web-api.md).</span></span>

<span data-ttu-id="3b96c-119">라우팅 테이블의 각 항목을 포함 한 *경로 템플릿을*합니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-119">Each entry in the routing table contains a *route template*.</span></span> <span data-ttu-id="3b96c-120">웹 API에 대 한 기본 경로 서식 파일은 &quot;api / {controller} / {id}&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-120">The default route template for Web API is &quot;api/{controller}/{id}&quot;.</span></span> <span data-ttu-id="3b96c-121">이 서식 파일에서 &quot;api&quot; 은 리터럴 경로 세그먼트 및 {컨트롤러} 및 {id}는 자리 표시자 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-121">In this template, &quot;api&quot; is a literal path segment, and {controller} and {id} are placeholder variables.</span></span>

<span data-ttu-id="3b96c-122">Web API 프레임 워크는 HTTP 요청을 받으면 라우팅 테이블에 경로 템플릿 중 하나에 대 한 URI와 일치 하도록 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-122">When the Web API framework receives an HTTP request, it tries to match the URI against one of the route templates in the routing table.</span></span> <span data-ttu-id="3b96c-123">경로가 없는 일치 하는 경우 클라이언트가 404 오류를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-123">If no route matches, the client receives a 404 error.</span></span> <span data-ttu-id="3b96c-124">예를 들어, 다음 Uri 기본 경로도 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-124">For example, the following URIs match the default route:</span></span>

- <span data-ttu-id="3b96c-125">/ api/연락처</span><span class="sxs-lookup"><span data-stu-id="3b96c-125">/api/contacts</span></span>
- <span data-ttu-id="3b96c-126">/api/contacts/1</span><span class="sxs-lookup"><span data-stu-id="3b96c-126">/api/contacts/1</span></span>
- <span data-ttu-id="3b96c-127">/api/products/gizmo1</span><span class="sxs-lookup"><span data-stu-id="3b96c-127">/api/products/gizmo1</span></span>

<span data-ttu-id="3b96c-128">그러나 다음과 같은 URI와 일치 하지 않으면 없기 때문에 &quot;api&quot; 세그먼트:</span><span class="sxs-lookup"><span data-stu-id="3b96c-128">However, the following URI does not match, because it lacks the &quot;api&quot; segment:</span></span>

- <span data-ttu-id="3b96c-129">/ 연락처/1</span><span class="sxs-lookup"><span data-stu-id="3b96c-129">/contacts/1</span></span>

> [!NOTE]
> <span data-ttu-id="3b96c-130">경로에서 "api"를 사용 하기 위한 이유 ASP.NET mvc 라우팅 충돌을 방지 하기 위해서입니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-130">The reason for using "api" in the route is to avoid collisions with ASP.NET MVC routing.</span></span> <span data-ttu-id="3b96c-131">할 수 있습니다 이런 방식으로 &quot;연결/&quot; 된 MVC 컨트롤러로 이동 하 고 &quot;/api/연락처&quot; Web API 컨트롤러로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-131">That way, you can have &quot;/contacts&quot; go to an MVC controller, and &quot;/api/contacts&quot; go to a Web API controller.</span></span> <span data-ttu-id="3b96c-132">물론,이 규칙을 마음에 들지 않는 경우 기본 경로 테이블을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-132">Of course, if you don't like this convention, you can change the default route table.</span></span>

<span data-ttu-id="3b96c-133">일치 하는 경로가 발견 되 면 Web API 컨트롤러 및 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-133">Once a matching route is found, Web API selects the controller and the action:</span></span>

- <span data-ttu-id="3b96c-134">Web API 컨트롤러를 찾으려면 추가 &quot;컨트롤러&quot; 의 값에는 *{컨트롤러}* 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-134">To find the controller, Web API adds &quot;Controller&quot; to the value of the *{controller}* variable.</span></span>
- <span data-ttu-id="3b96c-135">작업을 찾으려면 Web API HTTP 메서드를 찾은 해당 HTTP 메서드 이름으로 시작 하는 동작을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-135">To find the action, Web API looks at the HTTP method, and then looks for an action whose name begins with that HTTP method name.</span></span> <span data-ttu-id="3b96c-136">예를 들어 GET 요청에서 Web API ()은로 시작 하는 동작에 대 한 &quot;가져오기... &quot;와 같은 &quot;GetContact&quot; 또는 &quot;GetAllContacts&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-136">For example, with a GET request, Web API looks for an action that starts with &quot;Get...&quot;, such as &quot;GetContact&quot; or &quot;GetAllContacts&quot;.</span></span> <span data-ttu-id="3b96c-137">이 규칙 가져오기, POST, PUT, 및 삭제 메서드에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-137">This convention applies only to GET, POST, PUT, and DELETE methods.</span></span> <span data-ttu-id="3b96c-138">컨트롤러에서 특성을 사용 하 여 다른 HTTP 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-138">You can enable other HTTP methods by using attributes on your controller.</span></span> <span data-ttu-id="3b96c-139">예를 들어 나중에 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-139">We'll see an example of that later.</span></span>
- <span data-ttu-id="3b96c-140">경로 템플릿의 다른 자리 표시자 변수와 같은 *{id}* 액션 매개 변수는 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-140">Other placeholder variables in the route template, such as *{id},* are mapped to action parameters.</span></span>

<span data-ttu-id="3b96c-141">예를 살펴 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-141">Let's look at an example.</span></span> <span data-ttu-id="3b96c-142">다음 컨트롤러를 정의 하는 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-142">Suppose that you define the following controller:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="3b96c-143">다음은 각각에 대해 호출 된 동작과 함께 몇 가지 가능한 HTTP 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-143">Here are some possible HTTP requests, along with the action that gets invoked for each:</span></span>

| <span data-ttu-id="3b96c-144">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="3b96c-144">HTTP Method</span></span> | <span data-ttu-id="3b96c-145">URI 경로</span><span class="sxs-lookup"><span data-stu-id="3b96c-145">URI Path</span></span> | <span data-ttu-id="3b96c-146">작업</span><span class="sxs-lookup"><span data-stu-id="3b96c-146">Action</span></span> | <span data-ttu-id="3b96c-147">매개 변수</span><span class="sxs-lookup"><span data-stu-id="3b96c-147">Parameter</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b96c-148">가져오기</span><span class="sxs-lookup"><span data-stu-id="3b96c-148">GET</span></span> | <span data-ttu-id="3b96c-149">api/제품</span><span class="sxs-lookup"><span data-stu-id="3b96c-149">api/products</span></span> | <span data-ttu-id="3b96c-150">GetAllProducts</span><span class="sxs-lookup"><span data-stu-id="3b96c-150">GetAllProducts</span></span> | <span data-ttu-id="3b96c-151">*(없음)*</span><span class="sxs-lookup"><span data-stu-id="3b96c-151">*(none)*</span></span> |
| <span data-ttu-id="3b96c-152">가져오기</span><span class="sxs-lookup"><span data-stu-id="3b96c-152">GET</span></span> | <span data-ttu-id="3b96c-153">api/제품/4</span><span class="sxs-lookup"><span data-stu-id="3b96c-153">api/products/4</span></span> | <span data-ttu-id="3b96c-154">GetProductById</span><span class="sxs-lookup"><span data-stu-id="3b96c-154">GetProductById</span></span> | <span data-ttu-id="3b96c-155">4</span><span class="sxs-lookup"><span data-stu-id="3b96c-155">4</span></span> |
| <span data-ttu-id="3b96c-156">Delete</span><span class="sxs-lookup"><span data-stu-id="3b96c-156">DELETE</span></span> | <span data-ttu-id="3b96c-157">api/제품/4</span><span class="sxs-lookup"><span data-stu-id="3b96c-157">api/products/4</span></span> | <span data-ttu-id="3b96c-158">DeleteProduct</span><span class="sxs-lookup"><span data-stu-id="3b96c-158">DeleteProduct</span></span> | <span data-ttu-id="3b96c-159">4</span><span class="sxs-lookup"><span data-stu-id="3b96c-159">4</span></span> |
| <span data-ttu-id="3b96c-160">올리기</span><span class="sxs-lookup"><span data-stu-id="3b96c-160">POST</span></span> | <span data-ttu-id="3b96c-161">api/제품</span><span class="sxs-lookup"><span data-stu-id="3b96c-161">api/products</span></span> | <span data-ttu-id="3b96c-162">*(일치)*</span><span class="sxs-lookup"><span data-stu-id="3b96c-162">*(no match)*</span></span> |  |

<span data-ttu-id="3b96c-163">다음에 유의 *{id}* URI의 세그먼트가 있는 경우 매핑되는 *id* 동작의 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-163">Notice that the *{id}* segment of the URI, if present, is mapped to the *id* parameter of the action.</span></span> <span data-ttu-id="3b96c-164">이 예제는 컨트롤러에 두 개의 GET 메서드를 정의 *id* 매개 변수 및 매개 변수 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-164">In this example, the controller defines two GET methods, one with an *id* parameter and one with no parameters.</span></span>

<span data-ttu-id="3b96c-165">POST 요청이 실패 하는 컨트롤러에서 정의 하지 않으므로 참고 또한는 &quot;게시물 중... &quot; 메서드.</span><span class="sxs-lookup"><span data-stu-id="3b96c-165">Also, note that the POST request will fail, because the controller does not define a &quot;Post...&quot; method.</span></span>

## <a name="routing-variations"></a><span data-ttu-id="3b96c-166">라우팅 변형</span><span class="sxs-lookup"><span data-stu-id="3b96c-166">Routing Variations</span></span>

<span data-ttu-id="3b96c-167">이전 섹션 ASP.NET Web API에 대 한 기본 라우팅 메커니즘을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-167">The previous section described the basic routing mechanism for ASP.NET Web API.</span></span> <span data-ttu-id="3b96c-168">이 섹션에서는 몇 변형을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-168">This section describes some variations.</span></span>

### <a name="http-methods"></a><span data-ttu-id="3b96c-169">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="3b96c-169">HTTP Methods</span></span>

<span data-ttu-id="3b96c-170">HTTP 메서드에 대 한 명명 규칙을 사용 하는 대신 명시적으로 방법을 지정할 수 있습니다는 HTTP 작업에 대 한 사용 하 여 동작 메서드를 데코레이팅하는 **HttpGet**, **HttpPut**, **HttpPost** , 또는 **HttpDelete** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-170">Instead of using the naming convention for HTTP methods, you can explicitly specify the HTTP method for an action by decorating the action method with the **HttpGet**, **HttpPut**, **HttpPost**, or **HttpDelete** attribute.</span></span>

<span data-ttu-id="3b96c-171">다음 예제에서는 FindProduct 메서드는 GET 요청에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-171">In the following example, the FindProduct method is mapped to GET requests:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="3b96c-172">사용 하 여 작업을 위한 여러 HTTP 메서드가 허용 하거나 이외의 GET, PUT, POST 및 DELETE HTTP 메서드를 허용 하려면는 **AcceptVerbs** 목록이 며 HTTP 메서드는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-172">To allow multiple HTTP methods for an action, or to allow HTTP methods other than GET, PUT, POST, and DELETE, use the **AcceptVerbs** attribute, which takes a list of HTTP methods.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a><span data-ttu-id="3b96c-173">작업 이름으로 라우팅</span><span class="sxs-lookup"><span data-stu-id="3b96c-173">Routing by Action Name</span></span>

<span data-ttu-id="3b96c-174">기본 라우팅 템플릿을 사용 하 여 Web API HTTP 메서드를 사용 하 여 작업 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-174">With the default routing template, Web API uses the HTTP method to select the action.</span></span> <span data-ttu-id="3b96c-175">그러나 URI에 작업 이름이 포함 되어 있는 경로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-175">However, you can also create a route where the action name is included in the URI:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="3b96c-176">이 경로 템플릿에 *{action}* 컨트롤러 동작 메서드 매개 변수 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-176">In this route template, the *{action}* parameter names the action method on the controller.</span></span> <span data-ttu-id="3b96c-177">라우팅의이 스타일으로 허용 된 HTTP 메서드를 지정할 특성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-177">With this style of routing, use attributes to specify the allowed HTTP methods.</span></span> <span data-ttu-id="3b96c-178">예를 들어 컨트롤러에 다음 메서드가 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-178">For example, suppose your controller has the following method:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="3b96c-179">이 경우 "api/제품/세부 정보/1"에 대 한 GET 요청 Details 메서드를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-179">In this case, a GET request for "api/products/details/1" would map to the Details method.</span></span> <span data-ttu-id="3b96c-180">이 스타일 라우팅의 ASP.NET MVC 유사 하며 RPC 스타일 API에 대 한 적합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-180">This style of routing is similar to ASP.NET MVC, and may be appropriate for an RPC-style API.</span></span>

<span data-ttu-id="3b96c-181">작업 이름을 사용 하 여 재정의할 수 있습니다는 **ActionName** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-181">You can override the action name by using the **ActionName** attribute.</span></span> <span data-ttu-id="3b96c-182">다음 예제에서는 두 가지 동작에 매핑되는 &quot;api/제품/축소판 그림/*id*합니다. 도구가 지 원하는 GET 및 POST를 지원:</span><span class="sxs-lookup"><span data-stu-id="3b96c-182">In the following example, there are two actions that map to &quot;api/products/thumbnail/*id*. One supports GET and the other supports POST:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a><span data-ttu-id="3b96c-183">비 작업</span><span class="sxs-lookup"><span data-stu-id="3b96c-183">Non-Actions</span></span>

<span data-ttu-id="3b96c-184">메서드는 동작 호출 되지 않도록 하려면 사용 된 **NonAction** 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-184">To prevent a method from getting invoked as an action, use the **NonAction** attribute.</span></span> <span data-ttu-id="3b96c-185">이 신호 프레임 워크에 메서드가 작업을 하지 않으면 라우팅 규칙과 일치 하는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-185">This signals to the framework that the method is not an action, even if it would otherwise match the routing rules.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a><span data-ttu-id="3b96c-186">추가 정보</span><span class="sxs-lookup"><span data-stu-id="3b96c-186">Further Reading</span></span>

<span data-ttu-id="3b96c-187">이 항목 라우팅의 상위 수준 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-187">This topic provided a high-level view of routing.</span></span> <span data-ttu-id="3b96c-188">자세한 내용은 참조 [라우팅 및 작업 선택](routing-and-action-selection.md)를 정확히 어떻게 프레임 워크 경로 대 한 URI를 일치, 컨트롤러를 선택한 다음 선택 호출할 작업을 설명 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b96c-188">For more detail, see [Routing and Action Selection](routing-and-action-selection.md), which describes exactly how the framework matches a URI to a route, selects a controller, and then selects the action to invoke.</span></span>
