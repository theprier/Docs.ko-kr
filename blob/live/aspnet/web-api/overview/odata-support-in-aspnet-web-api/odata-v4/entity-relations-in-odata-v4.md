---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
title: "ASP.NET Web API 2.2 사용 하 여 OData v4의 엔터티 관계 | Microsoft Docs"
author: MikeWasson
description: "엔터티 간의 관계를 정의 하는 대부분의 데이터 집합: 고객이 주문을; 갖고 책에는 한 작성자입니다. 제품 공급 업체에는 합니다. OData를 사용 하 여 클라이언트를 탐색할 수 있습니다..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/26/2014
ms.topic: article
ms.assetid: 72657550-ec09-4779-9bfc-2fb15ecd51c7
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 4127fb2fa83f513a4faeb222068ca99f234ece22
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="entity-relations-in-odata-v4-using-aspnet-web-api-22"></a><span data-ttu-id="1a69f-104">ASP.NET Web API 2.2 사용 하 여 OData v4의 엔터티 관계</span><span class="sxs-lookup"><span data-stu-id="1a69f-104">Entity Relations in OData v4 Using ASP.NET Web API 2.2</span></span>
====================
<span data-ttu-id="1a69f-105">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="1a69f-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="1a69f-106">엔터티 간의 관계를 정의 하는 대부분의 데이터 집합: 고객이 주문을; 갖고 책에는 한 작성자입니다. 제품 공급 업체에는 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-106">Most data sets define relations between entities: Customers have orders; books have authors; products have suppliers.</span></span> <span data-ttu-id="1a69f-107">OData를 사용 하 여, 엔터티 관계를 통해 클라이언트를 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-107">Using OData, clients can navigate over entity relations.</span></span> <span data-ttu-id="1a69f-108">제품에 지정 된 경우 공급자를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-108">Given a product, you can find the supplier.</span></span> <span data-ttu-id="1a69f-109">만들 하거나 관계를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-109">You can also create or remove relationships.</span></span> <span data-ttu-id="1a69f-110">예를 들어 제품 공급 업체를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-110">For example, you can set the supplier for a product.</span></span>
> 
> <span data-ttu-id="1a69f-111">이 자습서에는 ASP.NET Web API를 사용 하 여 OData v4에서 이러한 작업을 지 원하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-111">This tutorial shows how to support these operations in OData v4 using ASP.NET Web API.</span></span> <span data-ttu-id="1a69f-112">이 자습서를 기반으로 자습서 [OData v4 Endpoint를 사용 하 여 ASP.NET 웹 API 2 만들](create-an-odata-v4-endpoint.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-112">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="1a69f-113">자습서에서 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="1a69f-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="1a69f-114">Web API 2.1</span><span class="sxs-lookup"><span data-stu-id="1a69f-114">Web API 2.1</span></span>
> - <span data-ttu-id="1a69f-115">OData v4</span><span class="sxs-lookup"><span data-stu-id="1a69f-115">OData v4</span></span>
> - [<span data-ttu-id="1a69f-116">Visual Studio 2013 업데이트 2</span><span class="sxs-lookup"><span data-stu-id="1a69f-116">Visual Studio 2013 Update 2</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs)
> - <span data-ttu-id="1a69f-117">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="1a69f-117">Entity Framework 6</span></span>
> - <span data-ttu-id="1a69f-118">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="1a69f-118">.NET 4.5</span></span>
> 
> 
> ## <a name="tutorial-versions"></a><span data-ttu-id="1a69f-119">자습서 버전</span><span class="sxs-lookup"><span data-stu-id="1a69f-119">Tutorial versions</span></span>
> 
> <span data-ttu-id="1a69f-120">OData 버전 3에 대 한 참조 [OData v 3의 엔터티 관계를 지 원하는](https://asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-120">For the OData Version 3, see [Supporting Entity Relations in OData v3](https://asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations).</span></span>


## <a name="add-a-supplier-entity"></a><span data-ttu-id="1a69f-121">Supplier 엔터티 추가</span><span class="sxs-lookup"><span data-stu-id="1a69f-121">Add a Supplier Entity</span></span>

> [!NOTE]
> <span data-ttu-id="1a69f-122">이 자습서를 기반으로 자습서 [OData v4 Endpoint를 사용 하 여 ASP.NET 웹 API 2 만들](create-an-odata-v4-endpoint.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-122">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md).</span></span>


<span data-ttu-id="1a69f-123">첫째, 관련된 엔터티를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-123">First, we need a related entity.</span></span> <span data-ttu-id="1a69f-124">라는 클래스를 추가 `Supplier` Models 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-124">Add a class named `Supplier` in the Models folder.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample1.cs)]

<span data-ttu-id="1a69f-125">탐색 속성을 추가 하는 `Product` 클래스:</span><span class="sxs-lookup"><span data-stu-id="1a69f-125">Add a navigation property to the `Product` class:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample2.cs?highlight=13-15)]

<span data-ttu-id="1a69f-126">새로 추가 **DbSet** 에 `ProductsContext` 클래스를 Entity Framework 데이터베이스에서 공급자 테이블 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-126">Add a new **DbSet** to the `ProductsContext` class, so that Entity Framework will include the Supplier table in the database.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample3.cs?highlight=10)]

<span data-ttu-id="1a69f-127">WebApiConfig.cs에 추가 &quot;Suppliers&quot; 엔터티 데이터 모델에 엔터티 집합:</span><span class="sxs-lookup"><span data-stu-id="1a69f-127">In WebApiConfig.cs, add a &quot;Suppliers&quot; entity set to the entity data model:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample4.cs?highlight=6)]

## <a name="add-a-suppliers-controller"></a><span data-ttu-id="1a69f-128">공급 업체 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="1a69f-128">Add a Suppliers Controller</span></span>

<span data-ttu-id="1a69f-129">추가 `SuppliersController` 컨트롤러 폴더에는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-129">Add a `SuppliersController` class to the Controllers folder.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="1a69f-130">필자는이 컨트롤러에 대 한 CRUD 작업을 추가 하는 방법을 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-130">I won't show how to add CRUD operations for this controller.</span></span> <span data-ttu-id="1a69f-131">단계는 Products 컨트롤러의 경우와 동일 (참조 [OData v4 끝점을 만드는](create-an-odata-v4-endpoint.md)).</span><span class="sxs-lookup"><span data-stu-id="1a69f-131">The steps are the same as for the Products controller (see [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md)).</span></span>

## <a name="getting-related-entities"></a><span data-ttu-id="1a69f-132">관련된 엔터티를 가져오는 중</span><span class="sxs-lookup"><span data-stu-id="1a69f-132">Getting Related Entities</span></span>

<span data-ttu-id="1a69f-133">공급 업체는 제품에 대 한을 가져오려면 클라이언트는 GET 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-133">To get the supplier for a product, the client sends a GET request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample6.cmd)]

<span data-ttu-id="1a69f-134">이 요청을 지원 하려면 다음 메서드를 추가 `ProductsController` 클래스:</span><span class="sxs-lookup"><span data-stu-id="1a69f-134">To support this request, add the following method to the `ProductsController` class:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample7.cs)]

<span data-ttu-id="1a69f-135">이 메서드는 기본 명명 규칙을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-135">This method uses a default naming convention</span></span>

- <span data-ttu-id="1a69f-136">메서드 이름: GetX, 여기서 X는 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-136">Method name: GetX, where X is the navigation property.</span></span>
- <span data-ttu-id="1a69f-137">매개 변수 이름: *키*</span><span class="sxs-lookup"><span data-stu-id="1a69f-137">Parameter name: *key*</span></span>

<span data-ttu-id="1a69f-138">이 명명 규칙을 따르는 경우 Web API HTTP 요청을 컨트롤러 메서드를 자동으로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-138">If you follow this naming convention, Web API automatically maps the HTTP request to the controller method.</span></span>

<span data-ttu-id="1a69f-139">예제에서는 HTTP 요청:</span><span class="sxs-lookup"><span data-stu-id="1a69f-139">Example HTTP request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample8.cmd)]

<span data-ttu-id="1a69f-140">예제에서는 HTTP 응답:</span><span class="sxs-lookup"><span data-stu-id="1a69f-140">Example HTTP response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample9.cmd)]

### <a name="getting-a-related-collection"></a><span data-ttu-id="1a69f-141">관련된 컬렉션 가져오기</span><span class="sxs-lookup"><span data-stu-id="1a69f-141">Getting a related collection</span></span>

<span data-ttu-id="1a69f-142">이전 예제에서는 제품에는 한 공급 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-142">In the previous example, a product has one supplier.</span></span> <span data-ttu-id="1a69f-143">탐색 속성 컬렉션을 반환할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-143">A navigation property can also return a collection.</span></span> <span data-ttu-id="1a69f-144">다음 코드는 공급자에 대 한 제품을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-144">The following code gets the products for a supplier:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample10.cs)]

<span data-ttu-id="1a69f-145">메서드가 반환 하는 경우에 **IQueryable** 대신는 **SingleResult&lt;T&gt;**</span><span class="sxs-lookup"><span data-stu-id="1a69f-145">In this case, the method returns an **IQueryable** instead of a **SingleResult&lt;T&gt;**</span></span>

<span data-ttu-id="1a69f-146">예제에서는 HTTP 요청:</span><span class="sxs-lookup"><span data-stu-id="1a69f-146">Example HTTP request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample11.cmd)]

<span data-ttu-id="1a69f-147">예제에서는 HTTP 응답:</span><span class="sxs-lookup"><span data-stu-id="1a69f-147">Example HTTP response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample12.cmd)]

## <a name="creating-a-relationship-between-entities"></a><span data-ttu-id="1a69f-148">엔터티 간 관계 만들기</span><span class="sxs-lookup"><span data-stu-id="1a69f-148">Creating a Relationship Between Entities</span></span>

<span data-ttu-id="1a69f-149">OData를 만들거나 기존 두 엔터티 간의 관계 제거를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-149">OData supports creating or removing relationships between two existing entities.</span></span> <span data-ttu-id="1a69f-150">관계는 OData v4 용어에서는 &quot;참조&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-150">In OData v4 terminology, the relationship is a &quot;reference&quot;.</span></span> <span data-ttu-id="1a69f-151">(관계 호출 된 OData v 3는 *링크*합니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-151">(In OData v3, the relationship was called a *link*.</span></span> <span data-ttu-id="1a69f-152">프로토콜 차이이 자습서에 대 한 중요 하지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="1a69f-152">The protocol differences don't matter for this tutorial.)</span></span>

<span data-ttu-id="1a69f-153">참조에 폼과 자체 URI `/Entity/NavigationProperty/$ref`합니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-153">A reference has its own URI, with the form `/Entity/NavigationProperty/$ref`.</span></span> <span data-ttu-id="1a69f-154">예를 들어 다음은 제품과 공급 업체 간의 참조 주소를 지정 하는 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-154">For example, here is the URI to address the reference between a product and its supplier:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample13.cmd)]

<span data-ttu-id="1a69f-155">관계를 추가 하려면 클라이언트는이 주소는 POST 또는 PUT 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-155">To add a relationship, the client sends a POST or PUT request to this address.</span></span>

- <span data-ttu-id="1a69f-156">탐색 속성은 단일 엔터티를 같은 경우 `Product.Supplier`합니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-156">PUT if the navigation property is a single entity, such as `Product.Supplier`.</span></span>
- <span data-ttu-id="1a69f-157">탐색 속성은 컬렉션와 같은 경우 게시 `Supplier.Products`합니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-157">POST if the navigation property is a collection, such as `Supplier.Products`.</span></span>

<span data-ttu-id="1a69f-158">요청 본문은 관계의 다른 엔터티의 URI를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-158">The body of the request contains the URI of the other entity in the relation.</span></span> <span data-ttu-id="1a69f-159">다음은 예제 요청이입니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-159">Here is an example request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample14.cmd)]

<span data-ttu-id="1a69f-160">이 예제에서는 클라이언트 PUT 요청을 보냅니다. `/Products(6)/Supplier/$ref`에 대 한 $ref URI 되는 `Supplier` ID로 제품의 = 6.</span><span class="sxs-lookup"><span data-stu-id="1a69f-160">In this example, the client sends a PUT request to `/Products(6)/Supplier/$ref`, which is the $ref URI for the `Supplier` of the product with ID = 6.</span></span> <span data-ttu-id="1a69f-161">요청이 성공 하면 204 (콘텐츠 없음) 응답을 서버에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-161">If the request succeeds, the server sends a 204 (No Content) response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample15.cmd)]

<span data-ttu-id="1a69f-162">다음은에 대 한 관계를 추가 하려면 컨트롤러 메서드는 `Product`:</span><span class="sxs-lookup"><span data-stu-id="1a69f-162">Here is the controller method to add a relationship to a `Product`:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample16.cs)]

<span data-ttu-id="1a69f-163">*navigationProperty* 어떤 관계를 설정할 매개 변수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-163">The *navigationProperty* parameter specifies which relationship to set.</span></span> <span data-ttu-id="1a69f-164">(더 추가할 수는 엔터티에서 탐색 속성이 둘 이상 있으면 `case` 문.)</span><span class="sxs-lookup"><span data-stu-id="1a69f-164">(If there is more than one navigation property on the entity, you can add more `case` statements.)</span></span>

<span data-ttu-id="1a69f-165">*링크* 매개 변수는 공급자의 URI를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-165">The *link* parameter contains the URI of the supplier.</span></span> <span data-ttu-id="1a69f-166">Web API에는 자동으로이 매개 변수에 대 한 값을 요청 본문 구문 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-166">Web API automatically parses the request body to get the value for this parameter.</span></span>

<span data-ttu-id="1a69f-167">ID (또는 키), 해야 공급자를 조회할의 일부인는 *링크* 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-167">To look up the supplier, we need the ID (or key), which is part of the *link* parameter.</span></span> <span data-ttu-id="1a69f-168">이렇게 하려면 다음 도우미 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-168">To do this, use the following helper method:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample17.cs)]

<span data-ttu-id="1a69f-169">기본적으로,이 메서드는 URI 경로 세그먼트로 분할 키를 포함 하는 세그먼트를 찾고, 키를 올바른 형식으로 변환 하는 OData 라이브러리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-169">Basically, this method uses the OData library to split the URI path into segments, find the segment that contains the key, and convert the key into the correct type.</span></span>

## <a name="deleting-a-relationship-between-entities"></a><span data-ttu-id="1a69f-170">엔터티 간의 관계를 삭제 하면</span><span class="sxs-lookup"><span data-stu-id="1a69f-170">Deleting a Relationship Between Entities</span></span>

<span data-ttu-id="1a69f-171">관계를 삭제 하려면 클라이언트 $ref URI HTTP DELETE 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-171">To delete a relationship, the client sends an HTTP DELETE request to the $ref URI:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample18.cmd)]

<span data-ttu-id="1a69f-172">제품 및 협력 업체 간의 관계를 삭제 하려면 컨트롤러 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-172">Here is the controller method to delete the relationship between a Product and a Supplier:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample19.cs)]

<span data-ttu-id="1a69f-173">이 경우 `Product.Supplier` 는 &quot;1&quot; 설정 하 여 관계를 제거할 수 있는 1 대 다 관계의 끝 `Product.Supplier` 를 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-173">In this case, `Product.Supplier` is the &quot;1&quot; end of a 1-to-many relation, so you can remove the relationship just by setting `Product.Supplier` to `null`.</span></span>

<span data-ttu-id="1a69f-174">에 &quot;많은&quot; 는 관련 엔터티를 제거 하는 클라이언트는 관계의 끝 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-174">In the &quot;many&quot; end of a relationship, the client must specify which related entity to remove.</span></span> <span data-ttu-id="1a69f-175">이렇게 하려면 클라이언트는 관련 엔터티의 URI 요청의 쿼리 문자열에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-175">To do so, the client sends the URI of the related entity in the query string of the request.</span></span> <span data-ttu-id="1a69f-176">예를 들어, "Product 1"에서 제거 하려면 "1" 공급 업체:</span><span class="sxs-lookup"><span data-stu-id="1a69f-176">For example, to remove "Product 1" from "Supplier 1":</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample20.cmd?highlight=1)]

<span data-ttu-id="1a69f-177">에 추가 매개 변수를 포함 하도록 설정 해야이 Web API에서 지원는 `DeleteRef` 메서드.</span><span class="sxs-lookup"><span data-stu-id="1a69f-177">To support this in Web API, we need to include an extra parameter in the `DeleteRef` method.</span></span> <span data-ttu-id="1a69f-178">여기에서 제품을 제거 하려면 컨트롤러 메서드는는 `Supplier.Products` 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-178">Here is the controller method to remove a product from the `Supplier.Products` relation.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample21.cs)]

<span data-ttu-id="1a69f-179">*키* 매개 변수는가 공급 업체에 대 한 키 및 *relatedKey* 매개 변수는에서 제거할 제품에 대 한 키의 `Products` 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-179">The *key* parameter is the key for the supplier, and the *relatedKey* parameter is the key for the product to remove from the `Products` relationship.</span></span> <span data-ttu-id="1a69f-180">웹 API는 쿼리 문자열에서 키를 자동으로 가져옵니다는 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a69f-180">Note that Web API automatically gets the key from the query string.</span></span>
