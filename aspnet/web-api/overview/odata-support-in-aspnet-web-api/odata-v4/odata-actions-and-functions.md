---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
title: 동작 및 ASP.NET Web API 2.2 사용 하 여 OData v4의 기능 | Microsoft Docs
author: MikeWasson
description: OData에서 동작 및 함수는 엔터티에 대 한 CRUD 작업으로 쉽게 정의 되어 있지 않은 서버 쪽 동작을 추가 하는 방법입니다. 이 자습서에서는 방법...
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 0e6fb03c-b16d-4bb0-ab0b-552bd2b6ece1
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
msc.type: authoredcontent
ms.openlocfilehash: 45b84ec4ee76e83ece99bf6841c28e13c3ab7728
ms.sourcegitcommit: 7890dfb5a8f8c07d813f166d3ab0c263f893d0c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48795269"
---
<a name="actions-and-functions-in-odata-v4-using-aspnet-web-api-22"></a><span data-ttu-id="214ac-104">작업 및 ASP.NET Web API 2.2 사용 하 여 OData v4의 함수</span><span class="sxs-lookup"><span data-stu-id="214ac-104">Actions and Functions in OData v4 Using ASP.NET Web API 2.2</span></span>
====================
<span data-ttu-id="214ac-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="214ac-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="214ac-106">OData에서 동작 및 함수는 엔터티에 대 한 CRUD 작업으로 쉽게 정의 되어 있지 않은 서버 쪽 동작을 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-106">In OData, actions and functions are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span> <span data-ttu-id="214ac-107">이 자습서에는 Web API 2.2를 사용 하 여 OData v4 끝점 동작 및 함수를 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-107">This tutorial shows how to add actions and functions to an OData v4 endpoint, using Web API 2.2.</span></span> <span data-ttu-id="214ac-108">이 자습서를 기반으로 자습서 [OData v4 끝점 사용 하 여 ASP.NET Web API 2 만들기](create-an-odata-v4-endpoint.md)</span><span class="sxs-lookup"><span data-stu-id="214ac-108">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md)</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="214ac-109">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="214ac-109">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="214ac-110">Web API 2.2</span><span class="sxs-lookup"><span data-stu-id="214ac-110">Web API 2.2</span></span>
> - <span data-ttu-id="214ac-111">OData v4</span><span class="sxs-lookup"><span data-stu-id="214ac-111">OData v4</span></span>
> - <span data-ttu-id="214ac-112">Visual Studio 2013 (Visual Studio 2017 다운로드 [여기](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span><span class="sxs-lookup"><span data-stu-id="214ac-112">Visual Studio 2013 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span></span>
> - <span data-ttu-id="214ac-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="214ac-113">.NET 4.5</span></span>
>
> ## <a name="tutorial-versions"></a><span data-ttu-id="214ac-114">자습서 버전</span><span class="sxs-lookup"><span data-stu-id="214ac-114">Tutorial versions</span></span>
>
> <span data-ttu-id="214ac-115">OData 버전 3을 참조 하세요 [ASP.NET Web API 2 OData 작업](../odata-v3/odata-actions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-115">For OData Version 3, see [OData Actions in ASP.NET Web API 2](../odata-v3/odata-actions.md).</span></span>

<span data-ttu-id="214ac-116">차이점 *작업* 하 고 *함수* 작업 부작용이 있을 수 고 함수는 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-116">The difference between *actions* and *functions* is that actions can have side effects, and functions do not.</span></span> <span data-ttu-id="214ac-117">동작과 함수 둘 다 데이터를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-117">Both actions and functions can return data.</span></span> <span data-ttu-id="214ac-118">작업에 대 한 몇 가지 용도 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-118">Some uses for actions include:</span></span>

- <span data-ttu-id="214ac-119">복잡 한 트랜잭션입니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-119">Complex transactions.</span></span>
- <span data-ttu-id="214ac-120">한 번에 여러 엔터티를 조작 합니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-120">Manipulating several entities at once.</span></span>
- <span data-ttu-id="214ac-121">엔터티의 특정 속성에만 업데이트를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-121">Allowing updates only to certain properties of an entity.</span></span>
- <span data-ttu-id="214ac-122">엔터티가 아닌 데이터를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-122">Sending data that is not an entity.</span></span>

<span data-ttu-id="214ac-123">함수는 엔터티 또는 컬렉션에 직접 해당 하지 않는 정보를 반환 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-123">Functions are useful for returning information that does not correspond directly to an entity or collection.</span></span>

<span data-ttu-id="214ac-124">작업 (또는 함수)는 단일 엔터티 또는 컬렉션을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-124">An action (or function) can target a single entity or a collection.</span></span> <span data-ttu-id="214ac-125">OData 용어에서이 합니다 *바인딩*합니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-125">In OData terminology, this is the *binding*.</span></span> <span data-ttu-id="214ac-126">할 수도 있습니다 &quot;바인딩되지 않은&quot; 작업/함수를 서비스에 대 한 정적 작업으로 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-126">You can also have &quot;unbound&quot; actions/functions, which are called as static operations on the service.</span></span>

## <a name="example-adding-an-action"></a><span data-ttu-id="214ac-127">예: 작업 추가</span><span class="sxs-lookup"><span data-stu-id="214ac-127">Example: Adding an Action</span></span>

<span data-ttu-id="214ac-128">제품을 평가 하는 작업을 정의 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-128">Let's define an action to rate a product.</span></span>

> [!NOTE]
> <span data-ttu-id="214ac-129">이 자습서를 기반으로 한이 자습서 [OData v4 끝점 사용 하 여 ASP.NET Web API 2 만들기](create-an-odata-v4-endpoint.md)</span><span class="sxs-lookup"><span data-stu-id="214ac-129">This tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md)</span></span>


<span data-ttu-id="214ac-130">첫째, 추가 `ProductRating` 등급을 나타내는 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-130">First, add a `ProductRating` model to represent the ratings.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample1.cs)]

<span data-ttu-id="214ac-131">추가할 수도 **DbSet** 에 `ProductsContext` 클래스는 EF는 데이터베이스의 등급 테이블이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-131">Also add a **DbSet** to the `ProductsContext` class, so that EF will create a Ratings table in the database.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample2.cs)]

### <a name="add-the-action-to-the-edm"></a><span data-ttu-id="214ac-132">EDM에 작업 추가</span><span class="sxs-lookup"><span data-stu-id="214ac-132">Add the Action to the EDM</span></span>

<span data-ttu-id="214ac-133">WebApiConfig.cs에서 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-133">In WebApiConfig.cs, add the following code:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample3.cs)]

<span data-ttu-id="214ac-134">합니다 **EntityTypeConfiguration.Action** 메서드는 EDM (엔터티 데이터 모델)에 작업을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-134">The **EntityTypeConfiguration.Action** method adds an action to the entity data model (EDM).</span></span> <span data-ttu-id="214ac-135">합니다 **매개 변수** 메서드는 작업에 대 한 형식화 된 매개 변수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-135">The **Parameter** method specifies a typed parameter for the action.</span></span>

<span data-ttu-id="214ac-136">또한이 코드는 EDM에 대 한 네임 스페이스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-136">This code also sets the namespace for the EDM.</span></span> <span data-ttu-id="214ac-137">네임 스페이스 작업에 대 한 URI 작업 정규화 된 이름을 포함 하기 때문에 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-137">The namespace matters because the URI for the action includes the fully-qualified action name:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample4.cmd)]

> [!NOTE]
> <span data-ttu-id="214ac-138">일반적인 IIS 구성에서이 URL에 있는 점을 404 오류를 반환 하는 IIS 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-138">In a typical IIS configuration, the dot in this URL will cause IIS to return error 404.</span></span> <span data-ttu-id="214ac-139">Web.Config 파일에 다음 섹션을 추가 하 여이 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-139">You can resolve this by adding the following section to your Web.Config file:</span></span>

[!code-xml[Main](odata-actions-and-functions/samples/sample5.xml)]

### <a name="add-a-controller-method-for-the-action"></a><span data-ttu-id="214ac-140">작업에 대 한 컨트롤러 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-140">Add a Controller Method for the Action</span></span>

<span data-ttu-id="214ac-141">사용 하도록 설정 합니다 &quot;속도&quot; 작업을 다음 메서드를 추가 `ProductsController`:</span><span class="sxs-lookup"><span data-stu-id="214ac-141">To enable the &quot;Rate&quot; action, add the following method to `ProductsController`:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample6.cs)]

<span data-ttu-id="214ac-142">메서드 이름이 작업 이름과 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-142">Notice that the method name matches the action name.</span></span> <span data-ttu-id="214ac-143">합니다 **[HttpPost]** 특성이 지정 된 메서드는 HTTP POST 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-143">The **[HttpPost]** attribute specifies the method is an HTTP POST method.</span></span>

<span data-ttu-id="214ac-144">클라이언트는 작업을 호출 하려면 다음과 같이 HTTP POST 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-144">To invoke the action, the client sends an HTTP POST request like the following:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample7.cmd)]

<span data-ttu-id="214ac-145">합니다 &quot;속도&quot; 작업 제품 인스턴스에 바인딩되어 않기 때문에 작업에 대 한 URI는 정규화 된 작업 이름을 엔터티 URI에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-145">The &quot;Rate&quot; action is bound to Product instances, so the URI for the action is the fully-qualified action name appended to the entity URI.</span></span> <span data-ttu-id="214ac-146">(EDM 네임 스페이스 설정 하 회수 &quot;ProductService&quot;이므로 작업 정규화 된 이름이 &quot;ProductService.Rate&quot;.)</span><span class="sxs-lookup"><span data-stu-id="214ac-146">(Recall that we set the EDM namespace to &quot;ProductService&quot;, so the fully-qualified action name is &quot;ProductService.Rate&quot;.)</span></span>

<span data-ttu-id="214ac-147">요청 본문 JSON 페이로드로 작업 매개 변수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-147">The body of the request contains the action parameters as a JSON payload.</span></span> <span data-ttu-id="214ac-148">웹 API에 JSON 페이로드를 자동으로 변환 합니다는 **ODataActionParameters** 개체 매개 변수 값의 사전 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-148">Web API automatically converts the JSON payload to an **ODataActionParameters** object, which is just a dictionary of parameter values.</span></span> <span data-ttu-id="214ac-149">컨트롤러 메서드에서 매개 변수에 액세스 하려면이 사전을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-149">Use this dictionary to access the parameters in your controller method.</span></span>

<span data-ttu-id="214ac-150">클라이언트에서 잘못 된 작업 매개 변수를 보내는 경우, 값의 형식을 **ModelState.IsValid** 은 false입니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-150">If the client sends the action parameters in the wrong format, the value of **ModelState.IsValid** is false.</span></span> <span data-ttu-id="214ac-151">컨트롤러 메서드에서이 플래그를 확인 하 고 오류가 반환 **IsValid** 은 false입니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-151">Check this flag in your controller method and return an error if **IsValid** is false.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample8.cs)]

## <a name="example-adding-a-function"></a><span data-ttu-id="214ac-152">예: 함수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-152">Example: Adding a Function</span></span>

<span data-ttu-id="214ac-153">이제 가장 저렴 한 제품을 반환 하는 OData 함수를 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-153">Now let's add an OData function that returns the most expensive product.</span></span> <span data-ttu-id="214ac-154">이전에 첫 번째 단계는 EDM에 함수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-154">As before, the first step is adding the function to the EDM.</span></span> <span data-ttu-id="214ac-155">WebApiConfig.cs에서 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-155">In WebApiConfig.cs, add the following code.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample9.cs)]

<span data-ttu-id="214ac-156">이 경우 함수는 개별 제품 인스턴스가 아닌 제품 컬렉션에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-156">In this case, the function is bound to the Products collection, rather than individual Product instances.</span></span> <span data-ttu-id="214ac-157">클라이언트는 GET 요청을 전송 하 여 함수를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-157">Clients invoke the function by sending a GET request:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample10.cmd)]

<span data-ttu-id="214ac-158">이 함수에 대 한 컨트롤러 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-158">Here is the controller method for this function:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample11.cs)]

<span data-ttu-id="214ac-159">메서드 이름은 함수 이름과 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-159">Notice that the method name matches the function name.</span></span> <span data-ttu-id="214ac-160">합니다 **[HttpGet]** HTTP GET 메서드는 특성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-160">The **[HttpGet]** attribute specifies the method is an HTTP GET method.</span></span>

<span data-ttu-id="214ac-161">HTTP 응답에는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-161">Here is the HTTP response:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample12.cmd)]

## <a name="example-adding-an-unbound-function"></a><span data-ttu-id="214ac-162">예: 바인딩되지 않은 함수를 추가 하기</span><span class="sxs-lookup"><span data-stu-id="214ac-162">Example: Adding an Unbound Function</span></span>

<span data-ttu-id="214ac-163">이전 예제에서 컬렉션에 바인딩된 함수.</span><span class="sxs-lookup"><span data-stu-id="214ac-163">The previous example was a function bound to a collection.</span></span> <span data-ttu-id="214ac-164">다음 예제에서는 만듭니다는 *바인딩되지 않은* 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-164">In this next example, we'll create an *unbound* function.</span></span> <span data-ttu-id="214ac-165">바인딩되지 않은 함수는 서비스에 대 한 정적 작업으로 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-165">Unbound functions are called as static operations on the service.</span></span> <span data-ttu-id="214ac-166">이 예제 함수는 지정 된 우편 번호에 대 한 판매 세금 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-166">The function in this example will return the sales tax for a given postal code.</span></span>

<span data-ttu-id="214ac-167">WebApiConfig 파일에서 EDM에 함수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-167">In the WebApiConfig file, add the function to the EDM:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample13.cs)]

<span data-ttu-id="214ac-168">호출 하는 것입니다 **함수** 에 직접 합니다 **된 ODataModelBuilder**, 엔터티 형식 또는 컬렉션을 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-168">Notice that we are calling **Function** directly on the **ODataModelBuilder**, instead of the entity type or collection.</span></span> <span data-ttu-id="214ac-169">이렇게 하면 함수는 바인딩된 모델 작성기입니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-169">This tells the model builder that the function is unbound.</span></span>

<span data-ttu-id="214ac-170">함수를 구현 하는 컨트롤러 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-170">Here is the controller method that implements the function:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample14.cs)]

<span data-ttu-id="214ac-171">이 메서드를 배치 하는 Web API 컨트롤러는 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-171">It does not matter which Web API controller you place this method in.</span></span> <span data-ttu-id="214ac-172">에 배치할 수 있습니다 `ProductsController`, 또는 별도 컨트롤러를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-172">You could put it in `ProductsController`, or define a separate controller.</span></span> <span data-ttu-id="214ac-173">합니다 **[ODataRoute]** 특성은 함수에 대 한 URI 템플릿을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-173">The **[ODataRoute]** attribute defines the URI template for the function.</span></span>

<span data-ttu-id="214ac-174">클라이언트 요청 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="214ac-174">Here is an example client request:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample15.cmd)]

<span data-ttu-id="214ac-175">HTTP 응답:</span><span class="sxs-lookup"><span data-stu-id="214ac-175">The HTTP response:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample16.cmd)]
