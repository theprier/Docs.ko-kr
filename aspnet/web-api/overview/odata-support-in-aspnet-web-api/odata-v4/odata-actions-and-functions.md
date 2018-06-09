---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
title: 작업 및 ASP.NET Web API 2.2 사용 하 여 OData v4 에서도 | Microsoft Docs
author: MikeWasson
description: OData, 동작 및 함수는 엔터티에 대 한 CRUD 작업으로 쉽게 정의 되어 있지 않은 서버 쪽 동작을 추가 하는 방법입니다. 이 자습서에서는 방법...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/27/2014
ms.topic: article
ms.assetid: 0e6fb03c-b16d-4bb0-ab0b-552bd2b6ece1
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
msc.type: authoredcontent
ms.openlocfilehash: 532362f0c0faaaf0cb0c04726856f0497e5261b5
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2018
ms.locfileid: "26508232"
---
<a name="actions-and-functions-in-odata-v4-using-aspnet-web-api-22"></a><span data-ttu-id="be7d9-104">작업 및 ASP.NET Web API 2.2 사용 하 여 OData v4에 함수</span><span class="sxs-lookup"><span data-stu-id="be7d9-104">Actions and Functions in OData v4 Using ASP.NET Web API 2.2</span></span>
====================
<span data-ttu-id="be7d9-105">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="be7d9-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="be7d9-106">OData, 동작 및 함수는 엔터티에 대 한 CRUD 작업으로 쉽게 정의 되어 있지 않은 서버 쪽 동작을 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-106">In OData, actions and functions are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span> <span data-ttu-id="be7d9-107">이 자습서에서는 웹 API 2.2를 사용 하 여 OData v4 끝점에 동작 및 기능을 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-107">This tutorial shows how to add actions and functions to an OData v4 endpoint, using Web API 2.2.</span></span> <span data-ttu-id="be7d9-108">이 자습서를 기반으로 자습서 [OData v4 Endpoint를 사용 하 여 ASP.NET 웹 API 2 만들기](create-an-odata-v4-endpoint.md)</span><span class="sxs-lookup"><span data-stu-id="be7d9-108">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md)</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="be7d9-109">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="be7d9-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="be7d9-110">Web API 2.2</span><span class="sxs-lookup"><span data-stu-id="be7d9-110">Web API 2.2</span></span>
> - <span data-ttu-id="be7d9-111">OData v4</span><span class="sxs-lookup"><span data-stu-id="be7d9-111">OData v4</span></span>
> - [<span data-ttu-id="be7d9-112">Visual Studio 2013 업데이트 2</span><span class="sxs-lookup"><span data-stu-id="be7d9-112">Visual Studio 2013 Update 2</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs)
> - <span data-ttu-id="be7d9-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="be7d9-113">.NET 4.5</span></span>
> 
> 
> ## <a name="tutorial-versions"></a><span data-ttu-id="be7d9-114">자습서 버전</span><span class="sxs-lookup"><span data-stu-id="be7d9-114">Tutorial versions</span></span>
> 
> <span data-ttu-id="be7d9-115">OData 버전 3에 대 한 참조 [ASP.NET Web API 2에서 OData 작업](../odata-v3/odata-actions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-115">For OData Version 3, see [OData Actions in ASP.NET Web API 2](../odata-v3/odata-actions.md).</span></span>


<span data-ttu-id="be7d9-116">차이 *동작* 및 *함수* 의도 하지 않은 작업 수 고 함수는 그렇지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-116">The difference between *actions* and *functions* is that actions can have side effects, and functions do not.</span></span> <span data-ttu-id="be7d9-117">동작과 함수는 데이터를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-117">Both actions and functions can return data.</span></span> <span data-ttu-id="be7d9-118">작업에 대 한 몇 가지 팁은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-118">Some uses for actions include:</span></span>

- <span data-ttu-id="be7d9-119">복잡 한 트랜잭션에 합니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-119">Complex transactions.</span></span>
- <span data-ttu-id="be7d9-120">한 번에 몇 개의 엔터티를 조작 합니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-120">Manipulating several entities at once.</span></span>
- <span data-ttu-id="be7d9-121">엔터티의 특정 속성에만 업데이트를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-121">Allowing updates only to certain properties of an entity.</span></span>
- <span data-ttu-id="be7d9-122">엔터티를 하지 않은 데이터를 보내는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-122">Sending data that is not an entity.</span></span>

<span data-ttu-id="be7d9-123">함수는 엔터티 또는 컬렉션에 직접 해당 하지 않는 정보를 반환 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-123">Functions are useful for returning information that does not correspond directly to an entity or collection.</span></span>

<span data-ttu-id="be7d9-124">작업 (또는 함수) 대상으로 지정할 수 하나의 엔터티 또는 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-124">An action (or function) can target a single entity or a collection.</span></span> <span data-ttu-id="be7d9-125">이 OData 용어에서는 *바인딩*합니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-125">In OData terminology, this is the *binding*.</span></span> <span data-ttu-id="be7d9-126">할 수도 있습니다 &quot;언바운드&quot; 작업/함수, 서비스에서 정적 작업으로 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-126">You can also have &quot;unbound&quot; actions/functions, which are called as static operations on the service.</span></span>

## <a name="example-adding-an-action"></a><span data-ttu-id="be7d9-127">예: 작업 추가</span><span class="sxs-lookup"><span data-stu-id="be7d9-127">Example: Adding an Action</span></span>

<span data-ttu-id="be7d9-128">제품 평가 하는 작업을 정의 해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-128">Let's define an action to rate a product.</span></span>

> [!NOTE]
> <span data-ttu-id="be7d9-129">이 자습서를 기반으로 한이 자습서 [OData v4 Endpoint를 사용 하 여 ASP.NET 웹 API 2 만들기](create-an-odata-v4-endpoint.md)</span><span class="sxs-lookup"><span data-stu-id="be7d9-129">This tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md)</span></span>


<span data-ttu-id="be7d9-130">먼저 추가 하는 `ProductRating` 등급을 나타내기 위해 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-130">First, add a `ProductRating` model to represent the ratings.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample1.cs)]

<span data-ttu-id="be7d9-131">또한 추가 **DbSet** 에 `ProductsContext` 클래스를 데이터베이스의 EF는 등급 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-131">Also add a **DbSet** to the `ProductsContext` class, so that EF will create a Ratings table in the database.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample2.cs)]

### <a name="add-the-action-to-the-edm"></a><span data-ttu-id="be7d9-132">EDM에 작업 추가</span><span class="sxs-lookup"><span data-stu-id="be7d9-132">Add the Action to the EDM</span></span>

<span data-ttu-id="be7d9-133">WebApiConfig.cs, 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-133">In WebApiConfig.cs, add the following code:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample3.cs)]

<span data-ttu-id="be7d9-134">**EntityTypeConfiguration.Action** 메서드 (EDM)의 엔터티 데이터 모델에 작업을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-134">The **EntityTypeConfiguration.Action** method adds an action to the entity data model (EDM).</span></span> <span data-ttu-id="be7d9-135">**매개 변수** 메서드 동작에 대해 입력된 된 매개 변수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-135">The **Parameter** method specifies a typed parameter for the action.</span></span>

<span data-ttu-id="be7d9-136">또한이 코드는 EDM에 대 한 네임 스페이스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-136">This code also sets the namespace for the EDM.</span></span> <span data-ttu-id="be7d9-137">네임 스페이스 작업에 대 한 URI 동작 정규화 된 이름을 포함 하기 때문에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-137">The namespace matters because the URI for the action includes the fully-qualified action name:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample4.cmd)]

> [!NOTE]
> <span data-ttu-id="be7d9-138">일반적인 IIS 구성에서이 URL에서 점을 404 오류를 반환 하도록 IIS를 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-138">In a typical IIS configuration, the dot in this URL will cause IIS to return error 404.</span></span> <span data-ttu-id="be7d9-139">다음 섹션을 Web.Config 파일에 추가 하 여이 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-139">You can resolve this by adding the following section to your Web.Config file:</span></span>

[!code-xml[Main](odata-actions-and-functions/samples/sample5.xml)]

### <a name="add-a-controller-method-for-the-action"></a><span data-ttu-id="be7d9-140">작업에 대 한 컨트롤러 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-140">Add a Controller Method for the Action</span></span>

<span data-ttu-id="be7d9-141">사용할 수 있도록는 &quot;속도&quot; 동작을 추가 하기 위해 다음 메서드 `ProductsController`:</span><span class="sxs-lookup"><span data-stu-id="be7d9-141">To enable the &quot;Rate&quot; action, add the following method to `ProductsController`:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample6.cs)]

<span data-ttu-id="be7d9-142">메서드 이름이 작업 이름과 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-142">Notice that the method name matches the action name.</span></span> <span data-ttu-id="be7d9-143">**[HttpPost]** HTTP POST 메서드는 특성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-143">The **[HttpPost]** attribute specifies the method is an HTTP POST method.</span></span>

<span data-ttu-id="be7d9-144">클라이언트는 작업을 호출 하려면 다음과 같은 HTTP POST 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-144">To invoke the action, the client sends an HTTP POST request like the following:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample7.cmd)]

<span data-ttu-id="be7d9-145">&quot;속도&quot; 동작이 제품 인스턴스를 바인딩된 작업에 대 한 URI 엔터티 URI에 추가 하는 정식 동작 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-145">The &quot;Rate&quot; action is bound to Product instances, so the URI for the action is the fully-qualified action name appended to the entity URI.</span></span> <span data-ttu-id="be7d9-146">(EDM 네임 스페이스 설정 했으므로 회수 &quot;ProductService&quot;동작 정규화 된 이름이 표시 됩니다, &quot;ProductService.Rate&quot;.)</span><span class="sxs-lookup"><span data-stu-id="be7d9-146">(Recall that we set the EDM namespace to &quot;ProductService&quot;, so the fully-qualified action name is &quot;ProductService.Rate&quot;.)</span></span>

<span data-ttu-id="be7d9-147">요청 본문 JSON 페이로드로 작업 매개 변수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-147">The body of the request contains the action parameters as a JSON payload.</span></span> <span data-ttu-id="be7d9-148">Web API에 JSON 페이로드를 자동으로 변환 된 **ODataActionParameters** 개체 매개 변수 값의 사전 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-148">Web API automatically converts the JSON payload to an **ODataActionParameters** object, which is just a dictionary of parameter values.</span></span> <span data-ttu-id="be7d9-149">이 사전을 사용 하 여 컨트롤러 메서드의 매개 변수를 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-149">Use this dictionary to access the parameters in your controller method.</span></span>

<span data-ttu-id="be7d9-150">클라이언트에서 잘못 된 작업 매개 변수를 보내는 경우, 값의 서식을 **ModelState.IsValid** 은 false입니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-150">If the client sends the action parameters in the wrong format, the value of **ModelState.IsValid** is false.</span></span> <span data-ttu-id="be7d9-151">컨트롤러 메서드의이 플래그를 확인 하 고 오류가 반환 **IsValid** 은 false입니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-151">Check this flag in your controller method and return an error if **IsValid** is false.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample8.cs)]

## <a name="example-adding-a-function"></a><span data-ttu-id="be7d9-152">예: 함수 추가</span><span class="sxs-lookup"><span data-stu-id="be7d9-152">Example: Adding a Function</span></span>

<span data-ttu-id="be7d9-153">이제 가장 비용이 많이 드는 제품을 반환 하는 OData 함수를 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-153">Now let's add an OData function that returns the most expensive product.</span></span> <span data-ttu-id="be7d9-154">로 이전에 첫 번째 단계는 함수를 추가 EDM입니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-154">As before, the first step is adding the function to the EDM.</span></span> <span data-ttu-id="be7d9-155">WebApiConfig.cs, 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-155">In WebApiConfig.cs, add the following code.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample9.cs)]

<span data-ttu-id="be7d9-156">이 경우 함수는 개별 제품 인스턴스가 아닌 제품 컬렉션에 바인딩되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-156">In this case, the function is bound to the Products collection, rather than individual Product instances.</span></span> <span data-ttu-id="be7d9-157">GET 요청을 전송 하 여 함수를 호출 하는 클라이언트:</span><span class="sxs-lookup"><span data-stu-id="be7d9-157">Clients invoke the function by sending a GET request:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample10.cmd)]

<span data-ttu-id="be7d9-158">이 함수에 대 한 컨트롤러 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-158">Here is the controller method for this function:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample11.cs)]

<span data-ttu-id="be7d9-159">메서드 이름이 함수 이름과 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-159">Notice that the method name matches the function name.</span></span> <span data-ttu-id="be7d9-160">**[HttpGet]** HTTP GET이 메서드는 특성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-160">The **[HttpGet]** attribute specifies the method is an HTTP GET method.</span></span>

<span data-ttu-id="be7d9-161">HTTP 응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-161">Here is the HTTP response:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample12.cmd)]

## <a name="example-adding-an-unbound-function"></a><span data-ttu-id="be7d9-162">예: 추가 언바운드 함수</span><span class="sxs-lookup"><span data-stu-id="be7d9-162">Example: Adding an Unbound Function</span></span>

<span data-ttu-id="be7d9-163">앞의 예제 작업은 컬렉션에 바인딩된 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-163">The previous example was a function bound to a collection.</span></span> <span data-ttu-id="be7d9-164">다음 예제에서는 만들어는 *바인딩되지 않은* 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-164">In this next example, we'll create an *unbound* function.</span></span> <span data-ttu-id="be7d9-165">바인딩되지 않은 함수는 정적 서비스 작업으로 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-165">Unbound functions are called as static operations on the service.</span></span> <span data-ttu-id="be7d9-166">이 예제 함수는 지정된 된 우편 번호에 대 한 판매 세금을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-166">The function in this example will return the sales tax for a given postal code.</span></span>

<span data-ttu-id="be7d9-167">경우 WebApiConfig 파일에서 EDM에 함수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-167">In the WebApiConfig file, add the function to the EDM:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample13.cs)]

<span data-ttu-id="be7d9-168">호출 하는 **함수** 에서 직접는 **된**, 엔터티 형식 또는 컬렉션을 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-168">Notice that we are calling **Function** directly on the **ODataModelBuilder**, instead of the entity type or collection.</span></span> <span data-ttu-id="be7d9-169">함수는 바인딩된 모델 작성기 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-169">This tells the model builder that the function is unbound.</span></span>

<span data-ttu-id="be7d9-170">함수를 구현 하는 컨트롤러 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-170">Here is the controller method that implements the function:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample14.cs)]

<span data-ttu-id="be7d9-171">이 메서드를 배치 하는 Web API 컨트롤러는 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-171">It does not matter which Web API controller you place this method in.</span></span> <span data-ttu-id="be7d9-172">빠뜨릴 수 `ProductsController`, 하거나 별도 컨트롤러를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-172">You could put it in `ProductsController`, or define a separate controller.</span></span> <span data-ttu-id="be7d9-173">**[ODataRoute]** 특성은 함수에 대 한 URI 템플릿을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-173">The **[ODataRoute]** attribute defines the URI template for the function.</span></span>

<span data-ttu-id="be7d9-174">다음은 예제 클라이언트 요청이입니다.</span><span class="sxs-lookup"><span data-stu-id="be7d9-174">Here is an example client request:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample15.cmd)]

<span data-ttu-id="be7d9-175">HTTP 응답:</span><span class="sxs-lookup"><span data-stu-id="be7d9-175">The HTTP response:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample16.cmd)]
