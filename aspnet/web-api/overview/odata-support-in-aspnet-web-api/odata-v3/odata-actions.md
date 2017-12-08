---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
title: "ASP.NET Web API 2 OData 작업을 지 원하는 | Microsoft Docs"
author: MikeWasson
description: "Odata에서 작업은 엔터티에 대 한 CRUD 작업으로 쉽게 정의 되어 있지 않은 서버 쪽 동작을 추가 하는 방법입니다. 작업에 대 한 일부 사용: 구현 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/25/2014
ms.topic: article
ms.assetid: 2d7b3aa2-aa47-4e6e-b0ce-3d65a1c6fe02
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
msc.type: authoredcontent
ms.openlocfilehash: acb369ca8f1bab8d7cad14c15f46cfd44beb9fdd
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="supporting-odata-actions-in-aspnet-web-api-2"></a><span data-ttu-id="d7f82-104">ASP.NET Web API 2 OData 작업을 지 원하는</span><span class="sxs-lookup"><span data-stu-id="d7f82-104">Supporting OData Actions in ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="d7f82-105">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="d7f82-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="d7f82-106">완료 된 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="d7f82-107">Odata에서 *동작* 엔터티에 대 한 CRUD 작업으로 쉽게 정의 되어 있지 않은 서버 쪽 동작을 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-107">In OData, *actions* are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span> <span data-ttu-id="d7f82-108">작업에 대 한 몇 가지 팁은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-108">Some uses for actions include:</span></span>
> 
> - <span data-ttu-id="d7f82-109">복잡 한 트랜잭션에 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-109">Implementing complex transactions.</span></span>
> - <span data-ttu-id="d7f82-110">한 번에 몇 개의 엔터티를 조작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-110">Manipulating several entities at once.</span></span>
> - <span data-ttu-id="d7f82-111">엔터티의 특정 속성에만 업데이트를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-111">Allowing updates only to certain properties of an entity.</span></span>
> - <span data-ttu-id="d7f82-112">엔터티의 정의 되지 않은 서버에 정보를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-112">Sending information to the server that is not defined in an entity.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="d7f82-113">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="d7f82-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="d7f82-114">Web API 2</span><span class="sxs-lookup"><span data-stu-id="d7f82-114">Web API 2</span></span>
> - <span data-ttu-id="d7f82-115">OData 버전 3</span><span class="sxs-lookup"><span data-stu-id="d7f82-115">OData Version 3</span></span>
> - <span data-ttu-id="d7f82-116">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="d7f82-116">Entity Framework 6</span></span>


## <a name="example-rating-a-product"></a><span data-ttu-id="d7f82-117">예: 제품 평가</span><span class="sxs-lookup"><span data-stu-id="d7f82-117">Example: Rating a Product</span></span>

<span data-ttu-id="d7f82-118">이 예제에서는 사용자가 제품을 평가 하 고 그런 다음 각 제품에 대 한 평균 등급을 제공 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-118">In this example, we want to let users rate products, and then expose the average ratings for each product.</span></span> <span data-ttu-id="d7f82-119">다음은 데이터베이스에서의 등급, 제품 키가 지정 된 목록을 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-119">On the database, we will store a list of ratings, keyed to products.</span></span>

<span data-ttu-id="d7f82-120">다음은 Entity Framework의 등급을 나타내기 위해 사용할 것 모델이입니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-120">Here is the model we might use to represent the ratings in Entity Framework:</span></span>

[!code-csharp[Main](odata-actions/samples/sample1.cs)]

<span data-ttu-id="d7f82-121">클라이언트가 POST 않도록 하지만 `ProductRating` "등급" 컬렉션 개체를 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-121">But we don't want clients to POST a `ProductRating` object to a "Ratings" collection.</span></span> <span data-ttu-id="d7f82-122">직관적으로 등급 제품 컬렉션에 연결 되며 클라이언트 해야 등급 값을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-122">Intuitively, the rating is associated with the Products collection, and the client should only need to post the rating value.</span></span>

<span data-ttu-id="d7f82-123">따라서 기본 CRUD 작업을 사용 하는 대신 정의 클라이언트가 호출할 수 있는 동작 제품.</span><span class="sxs-lookup"><span data-stu-id="d7f82-123">Therefore, instead of using the normal CRUD operations, we define an action that a client can invoke on a Product.</span></span> <span data-ttu-id="d7f82-124">작업은 OData 용어로 *바인딩된* 제품 엔터티.</span><span class="sxs-lookup"><span data-stu-id="d7f82-124">In OData terminology, the action is *bound* to Product entities.</span></span>

><span data-ttu-id="d7f82-125">부작용에 서버에 있어야 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-125">Actions have side-effects on the server.</span></span> <span data-ttu-id="d7f82-126">이러한 이유로 HTTP POST 요청을 사용 하 여 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-126">For this reason, they are invoked using HTTP POST requests.</span></span> <span data-ttu-id="d7f82-127">작업 매개 변수 및 서비스 메타 데이터에서 설명 하는 반환 형식을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-127">Actions can have parameters and return types, which are described in the service metadata.</span></span> <span data-ttu-id="d7f82-128">클라이언트 요청 본문에는 매개 변수 보내고 서버 응답 본문에 반환 값을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-128">The client sends the parameters in the request body, and the server sends the return value in the response body.</span></span> <span data-ttu-id="d7f82-129">"속도 제품" 작업을 호출 하려면 클라이언트 다음과 같은 URI에 POST를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-129">To invoke the "Rate Product" action, the client sends a POST to a URI like the following:</span></span>

[!code-console[Main](odata-actions/samples/sample2.cmd)]

<span data-ttu-id="d7f82-130">POST 요청에 대 한 데이터는 단순히 제품 등급:</span><span class="sxs-lookup"><span data-stu-id="d7f82-130">The data in the POST request is simply the product rating:</span></span>

[!code-console[Main](odata-actions/samples/sample3.cmd)]

## <a name="declare-the-action-in-the-entity-data-model"></a><span data-ttu-id="d7f82-131">엔터티 데이터 모델의 작업을 선언</span><span class="sxs-lookup"><span data-stu-id="d7f82-131">Declare the Action in the Entity Data Model</span></span>

<span data-ttu-id="d7f82-132">Web API 구성에서는 엔터티 데이터 모델 (EDM)에 동작을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-132">In your Web API configuration, add the action to the entity data model (EDM):</span></span>

[!code-csharp[Main](odata-actions/samples/sample4.cs)]

<span data-ttu-id="d7f82-133">이 코드는 "RateProduct" 제품 엔터티에 대해 수행할 수 있는 동작으로 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-133">This code defines "RateProduct" as an action that can be performed on Product entities.</span></span> <span data-ttu-id="d7f82-134">또한 동작이 선언는 **int** "등급" 라는 하 고 반환 하는 매개 변수는 **int** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-134">It also declares that the action takes an **int** parameter named "Rating", and returns an **int** value.</span></span>

## <a name="add-the-action-to-the-controller"></a><span data-ttu-id="d7f82-135">컨트롤러에 추가 하는 작업</span><span class="sxs-lookup"><span data-stu-id="d7f82-135">Add the Action to the Controller</span></span>

<span data-ttu-id="d7f82-136">"RateProduct" 동작을 제품 엔터티에 바인딩되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-136">The "RateProduct" action is bound to Product entities.</span></span> <span data-ttu-id="d7f82-137">라는 메서드를 추가 동작을 구현 하려면 `RateProduct` 제품 컨트롤러에:</span><span class="sxs-lookup"><span data-stu-id="d7f82-137">To implement the action, add a method named `RateProduct` to the Products controller:</span></span>

[!code-csharp[Main](odata-actions/samples/sample5.cs)]

<span data-ttu-id="d7f82-138">메서드 이름이 EDM의 동작의 이름과 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-138">Notice that the method name matches the name of the action in the EDM.</span></span> <span data-ttu-id="d7f82-139">메서드에 두 개의 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-139">The method has two parameters:</span></span>

- <span data-ttu-id="d7f82-140">*키*: 등급을 제품에 대 한 키입니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-140">*key*: The key for the product to rate.</span></span>
- <span data-ttu-id="d7f82-141">*매개 변수*: 작업 매개 변수 값의 사전입니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-141">*parameters*: A dictionary of action parameter values.</span></span>

<span data-ttu-id="d7f82-142">기본 라우팅 규칙을 사용 하는 키 매개 변수 이름을 지정 해야 "키"입니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-142">If you are using the default routing conventions, the key parameter must be named "key".</span></span> <span data-ttu-id="d7f82-143">포함 하는 것이 중요 이기도 **[FromOdataUri]** 특성으로 표시 된 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-143">It is also important to include the **[FromOdataUri]** attribute, as shown.</span></span> <span data-ttu-id="d7f82-144">이 특성은 요청 URI에서에서 키를 구문 분석할 때 OData 구문 규칙을 사용 하도록 Web API를 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-144">This attribute tells Web API to use OData syntax rules when it parses the key from the request URI.</span></span>

<span data-ttu-id="d7f82-145">사용 하 여는 *매개 변수* 사전 작업 매개 변수를 가져오려면:</span><span class="sxs-lookup"><span data-stu-id="d7f82-145">Use the *parameters* dictionary to get the action parameters:</span></span>

[!code-csharp[Main](odata-actions/samples/sample6.cs)]

<span data-ttu-id="d7f82-146">클라이언트에서 올바른 작업 매개 변수를 보내는 경우, 값의 서식을 **ModelState.IsValid** 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-146">If the client sends the action parameters in the correct format, the value of **ModelState.IsValid** is true.</span></span> <span data-ttu-id="d7f82-147">이 경우 사용할 수 있습니다는 **ODataActionParameters** 사전 매개 변수 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-147">In that case, you can use the **ODataActionParameters** dictionary to get the parameter values.</span></span> <span data-ttu-id="d7f82-148">이 예제는 `RateProduct` "등급" 라는 단일 매개 변수를 사용 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-148">In this example, the `RateProduct` action takes a single parameter named "Rating".</span></span>

## <a name="action-metadata"></a><span data-ttu-id="d7f82-149">동작 메타 데이터</span><span class="sxs-lookup"><span data-stu-id="d7f82-149">Action Metadata</span></span>

<span data-ttu-id="d7f82-150">서비스 메타 데이터를 보려면 /odata/$ 메타 데이터에 GET 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-150">To view the service metadata, send a GET request to /odata/$metadata.</span></span> <span data-ttu-id="d7f82-151">선언 하는 메타 데이터의 부분입니다. 여기에서 `RateProduct` 동작:</span><span class="sxs-lookup"><span data-stu-id="d7f82-151">Here is the portion of the metadata that declares the `RateProduct` action:</span></span>

[!code-xml[Main](odata-actions/samples/sample7.xml)]

<span data-ttu-id="d7f82-152">**FunctionImport** 요소 작업을 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-152">The **FunctionImport** element declares the action.</span></span> <span data-ttu-id="d7f82-153">대부분의 필드 이름 자체로 설명 되지만 두 가지 주요 데이터:</span><span class="sxs-lookup"><span data-stu-id="d7f82-153">Most of the fields are self-explanatory, but two are worth noting:</span></span>

- <span data-ttu-id="d7f82-154">**Isbindable 인** 는 동작을 호출할 수 대상 엔터티의 이상 의미 일정 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-154">**IsBindable** means the action can be invoked on the target entity, at least some of the time.</span></span>
- <span data-ttu-id="d7f82-155">**IsAlwaysBindable** 동작을 호출 하 여 대상 엔터티의 항상 수를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-155">**IsAlwaysBindable** means the action can always be invoked on the target entity.</span></span>

<span data-ttu-id="d7f82-156">차이가 일부 작업은 항상 클라이언트를 사용할 수 있지만 다른 작업의 엔터티 상태에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-156">The difference is that some actions are always available to clients, but other actions might depend on the state of the entity.</span></span> <span data-ttu-id="d7f82-157">예를 들어, "Purchase" 동작을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-157">For example, suppose you define a "Purchase" action.</span></span> <span data-ttu-id="d7f82-158">만 재고에 있는 항목을 구입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-158">You can only purchase an item that is in stock.</span></span> <span data-ttu-id="d7f82-159">항목이 out of stock 경우 클라이언트가 해당 동작을 호출할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-159">If the item is out of stock, a client cannot invoke that action.</span></span>

<span data-ttu-id="d7f82-160">EDM에 정의 하는 경우는 **동작** 메서드는 항상 바인딩 가능 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-160">When you define the EDM, the **Action** method creates an always-bindable action:</span></span>

[!code-csharp[Main](odata-actions/samples/sample8.cs?highlight=1)]

<span data-ttu-id="d7f82-161">Not 항상-바인딩 가능한 동작에 대 한 하겠습니다 (호출 또한 *일시적인* 작업)이이 항목의 뒷부분에 나오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-161">I'll talk about not-always-bindable actions (also called *transient* actions) later in this topic.</span></span>

## <a name="invoking-the-action"></a><span data-ttu-id="d7f82-162">다음 작업을 호출</span><span class="sxs-lookup"><span data-stu-id="d7f82-162">Invoking the Action</span></span>

<span data-ttu-id="d7f82-163">이제 클라이언트는이 작업을 호출 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-163">Now let's see how a client would invoke this action.</span></span> <span data-ttu-id="d7f82-164">클라이언트 ID 인 제품에 2의 등급을 제공 하려는 경우를 가정해 볼 = 4.</span><span class="sxs-lookup"><span data-stu-id="d7f82-164">Suppose the client wants to give a rating of 2 to the product with ID = 4.</span></span> <span data-ttu-id="d7f82-165">다음은 JSON 형식을 사용 하 여 요청 본문에 대 한 예제 요청 메시지가입니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-165">Here is an example request message, using JSON format for the request body:</span></span>

[!code-console[Main](odata-actions/samples/sample9.cmd)]

<span data-ttu-id="d7f82-166">응답 메시지는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-166">Here is the response message:</span></span>

[!code-console[Main](odata-actions/samples/sample10.cmd)]

## <a name="binding-an-action-to-an-entity-set"></a><span data-ttu-id="d7f82-167">작업 엔터티 집합에 바인딩</span><span class="sxs-lookup"><span data-stu-id="d7f82-167">Binding an Action to an Entity Set</span></span>

<span data-ttu-id="d7f82-168">이전 예에서 동작이 단일 엔터티에 바인딩된: 클라이언트 단일 제품의 등급을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-168">In the previous example, the action is bound to a single entity: The client rates a single product.</span></span> <span data-ttu-id="d7f82-169">또한 엔터티를 컬렉션에 작업을 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-169">You can also bind an action to a collection of entities.</span></span> <span data-ttu-id="d7f82-170">단지 다음과 같이 변경을 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-170">Just make the following changes:</span></span>

<span data-ttu-id="d7f82-171">Edm에서는 동작 엔터티의을 추가 **컬렉션** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-171">In the EDM, add the action to the entity's **Collection** property.</span></span>

[!code-csharp[Main](odata-actions/samples/sample11.cs?highlight=1)]

<span data-ttu-id="d7f82-172">컨트롤러 메서드의 생략는 *키* 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-172">In the controller method, omit the *key* parameter.</span></span>

[!code-csharp[Main](odata-actions/samples/sample12.cs)]

<span data-ttu-id="d7f82-173">이제 클라이언트 제품 엔터티 집합에 대해 작업을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-173">Now the client invokes the action on the Products entity set:</span></span>

[!code-console[Main](odata-actions/samples/sample13.cmd)]

## <a name="actions-with-collection-parameters"></a><span data-ttu-id="d7f82-174">컬렉션 매개 변수를 사용 하 여 작업</span><span class="sxs-lookup"><span data-stu-id="d7f82-174">Actions with Collection Parameters</span></span>

<span data-ttu-id="d7f82-175">작업 값의 컬렉션을 사용 하는 매개 변수를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-175">Actions can have parameters that take a collection of values.</span></span> <span data-ttu-id="d7f82-176">EDM에서 사용 하 여 **CollectionParameter&lt;T&gt;**  를 매개 변수를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-176">In the EDM, use **CollectionParameter&lt;T&gt;** to declare the parameter.</span></span>

[!code-csharp[Main](odata-actions/samples/sample14.cs)]

<span data-ttu-id="d7f82-177">컬렉션을 사용 하는 "등급" 라는 매개 변수를 선언 하는이 **int** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-177">This declares a parameter named "Ratings" that takes a collection of **int** values.</span></span> <span data-ttu-id="d7f82-178">컨트롤러 메서드를 여전히 매개 변수 값을가 가져올는 **ODataActionParameters** 개체가 아니라 이제 값은 한 **ICollection&lt;int&gt;**  값:</span><span class="sxs-lookup"><span data-stu-id="d7f82-178">In the controller method, you still get the parameter value from the **ODataActionParameters** object, but now the value is an **ICollection&lt;int&gt;** value:</span></span>

[!code-csharp[Main](odata-actions/samples/sample15.cs)]

## <a name="transient-actions"></a><span data-ttu-id="d7f82-179">임시 작업</span><span class="sxs-lookup"><span data-stu-id="d7f82-179">Transient Actions</span></span>

<span data-ttu-id="d7f82-180">"RateProduct" 예제에서는 사용자가 항상 평가할 수, 제품 동작은 항상 사용할 수 있도록.</span><span class="sxs-lookup"><span data-stu-id="d7f82-180">In the "RateProduct" example, users can always rate a product, so the action is always available.</span></span> <span data-ttu-id="d7f82-181">하지만 일부 작업의 엔터티 상태에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-181">But some actions depend on the state of the entity.</span></span> <span data-ttu-id="d7f82-182">예를 들어, 비디오 대 여 서비스에서 "체크 아웃" 작업 항상 사용할 수 없는 경우</span><span class="sxs-lookup"><span data-stu-id="d7f82-182">For example, in a video rental service, the "CheckOut" action is not always available.</span></span> <span data-ttu-id="d7f82-183">(종속 해당 비디오의 복사본은 사용할 수 있는지 여부를.) 이러한 종류의 동작은 라고는 *일시적인* 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-183">(It depends whether a copy of that video is available.) This type of action is called a *transient* action.</span></span>

<span data-ttu-id="d7f82-184">일시적인 동작에 서비스 메타 데이터를 **IsAlwaysBindable** false 같음.</span><span class="sxs-lookup"><span data-stu-id="d7f82-184">In the service metadata, a transient action has **IsAlwaysBindable** equal to false.</span></span> <span data-ttu-id="d7f82-185">이므로 실제로 기본 값, 메타 데이터는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-185">That's actually the default value, so the metadata will look like this:</span></span>

[!code-xml[Main](odata-actions/samples/sample16.xml)]

<span data-ttu-id="d7f82-186">여기가 중요 한 이유: 서버가 동작은 사용할 수 있는 클라이언트에 게 알리는 해야 일시적인 작업의 경우.</span><span class="sxs-lookup"><span data-stu-id="d7f82-186">Here's why this matters: If an action is transient, the server needs to tell the client when the action is available.</span></span> <span data-ttu-id="d7f82-187">엔터티에서 작업에 대 한 링크를 포함 하 여 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-187">It does this by including a link to the action in the entity.</span></span> <span data-ttu-id="d7f82-188">영화 엔터티에 대 한 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-188">Here is an example for a Movie entity:</span></span>

[!code-console[Main](odata-actions/samples/sample17.cmd)]

<span data-ttu-id="d7f82-189">"#CheckOut" 속성은 체크 아웃 작업에 대 한 링크를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-189">The "#CheckOut" property contains a link to the CheckOut action.</span></span> <span data-ttu-id="d7f82-190">서버 작업에 사용할 수 없는 경우 링크를 생략 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-190">If the action is not available, the server omits the link.</span></span>

<span data-ttu-id="d7f82-191">EDM의 임시 작업을 선언 하려면 호출는 **TransientAction** 메서드:</span><span class="sxs-lookup"><span data-stu-id="d7f82-191">To declare a transient action in the EDM, call the **TransientAction** method:</span></span>

[!code-csharp[Main](odata-actions/samples/sample18.cs)]

<span data-ttu-id="d7f82-192">또한 특정된 엔터티에 대 한 작업 링크를 반환 하는 함수를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-192">Also, you must provide a function that returns an action link for a given entity.</span></span> <span data-ttu-id="d7f82-193">이 함수를 호출 하 여 설정 **HasActionLink**합니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-193">Set this function by calling **HasActionLink**.</span></span> <span data-ttu-id="d7f82-194">람다 식으로 함수를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-194">You can write the function as a lambda expression:</span></span>

[!code-csharp[Main](odata-actions/samples/sample19.cs)]

<span data-ttu-id="d7f82-195">작업이 사용할 수 있는 경우 람다 식을 작업에 대 한 링크를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-195">If the action is available, the lambda expression returns a link to the action.</span></span> <span data-ttu-id="d7f82-196">엔터티를 serialize 할 때이 링크를 포함 하는 OData 직렬 변환기입니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-196">The OData serializer includes this link when it serializes the entity.</span></span> <span data-ttu-id="d7f82-197">함수를 반환 하는 작업에 사용할 수 없는 경우 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="d7f82-197">When the action is not available, the function returns `null`.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d7f82-198">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="d7f82-198">Additional Resources</span></span>

[<span data-ttu-id="d7f82-199">OData 작업 샘플</span><span class="sxs-lookup"><span data-stu-id="d7f82-199">OData Actions Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v3/ODataActionsSample/)
