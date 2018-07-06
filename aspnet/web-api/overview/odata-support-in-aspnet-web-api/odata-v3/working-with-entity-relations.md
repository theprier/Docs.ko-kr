---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
title: 웹 API 2 OData v3의 엔터티 관계 지원 | Microsoft Docs
author: MikeWasson
description: '엔터티 간의 관계를 정의 하는 대부분의 데이터 집합: 고객은 주문; 온라인 설명서가 작성자; 제품 공급 업체에 있습니다. OData를 사용 하 여 클라이언트를 탐색할 수 있습니다...'
ms.author: aspnetcontent
ms.date: 02/26/2014
ms.assetid: 1e4c2eb4-b6cf-42ff-8a65-4d71ddca0394
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
msc.type: authoredcontent
ms.openlocfilehash: b24e3ca4e3d39b424bec6bb408bb0f85825c6761
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37810746"
---
<a name="supporting-entity-relations-in-odata-v3-with-web-api-2"></a><span data-ttu-id="c3dea-104">웹 API 2 OData v3의 엔터티 관계 지원</span><span class="sxs-lookup"><span data-stu-id="c3dea-104">Supporting Entity Relations in OData v3 with Web API 2</span></span>
====================
<span data-ttu-id="c3dea-105">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c3dea-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="c3dea-106">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="c3dea-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="c3dea-107">엔터티 간의 관계를 정의 하는 대부분의 데이터 집합: 고객은 주문; 온라인 설명서가 작성자; 제품 공급 업체에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-107">Most data sets define relations between entities: Customers have orders; books have authors; products have suppliers.</span></span> <span data-ttu-id="c3dea-108">OData를 클라이언트 엔터티 관계 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-108">Using OData, clients can navigate over entity relations.</span></span> <span data-ttu-id="c3dea-109">제품에 지정 된 공급자를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-109">Given a product, you can find the supplier.</span></span> <span data-ttu-id="c3dea-110">만들기 또는 관계를 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-110">You can also create or remove relationships.</span></span> <span data-ttu-id="c3dea-111">예를 들어, 제품 공급 업체를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-111">For example, you can set the supplier for a product.</span></span>
> 
> <span data-ttu-id="c3dea-112">이 자습서에서는 ASP.NET Web API에서 이러한 작업을 지 원하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-112">This tutorial shows how to support these operations in ASP.NET Web API.</span></span> <span data-ttu-id="c3dea-113">이 자습서를 기반으로 한 자습서 [Web API 2 OData v3 엔드포인트 만들기](creating-an-odata-endpoint.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-113">The tutorial builds on the tutorial [Creating an OData v3 Endpoint with Web API 2](creating-an-odata-endpoint.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="c3dea-114">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="c3dea-114">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="c3dea-115">Web API 2</span><span class="sxs-lookup"><span data-stu-id="c3dea-115">Web API 2</span></span>
> - <span data-ttu-id="c3dea-116">OData 버전 3</span><span class="sxs-lookup"><span data-stu-id="c3dea-116">OData Version 3</span></span>
> - <span data-ttu-id="c3dea-117">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="c3dea-117">Entity Framework 6</span></span>


## <a name="add-a-supplier-entity"></a><span data-ttu-id="c3dea-118">Supplier 엔터티를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-118">Add a Supplier Entity</span></span>

<span data-ttu-id="c3dea-119">먼저 새 엔터티 형식이 OData 피드를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-119">First we need to add a new entity type to our OData feed.</span></span> <span data-ttu-id="c3dea-120">추가할 것을 `Supplier` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-120">We'll add a `Supplier` class.</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample1.cs)]

<span data-ttu-id="c3dea-121">이 클래스는 엔터티 키에 대 한 문자열을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-121">This class uses a string for the entity key.</span></span> <span data-ttu-id="c3dea-122">실제로 정수 키를 사용 하 여 보다는 덜 일반적인 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-122">In practice, that might be less common than using an integer key.</span></span> <span data-ttu-id="c3dea-123">하지만 OData 정수 외에도 다른 키 유형을 처리 하는 방법을 보는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-123">But it's worth seeing how OData handles other key types besides integers.</span></span>

<span data-ttu-id="c3dea-124">다음으로 만들겠습니다 관계를 추가 하 여는 `Supplier` 속성을는 `Product` 클래스:</span><span class="sxs-lookup"><span data-stu-id="c3dea-124">Next, we'll create a relation by adding a `Supplier` property to the `Product` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample2.cs)]

<span data-ttu-id="c3dea-125">새 **DbSet** 에 `ProductServiceContext` 클래스를 Entity Framework에 포함 되도록는 `Supplier` 데이터베이스의 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-125">Add a new **DbSet** to the `ProductServiceContext` class, so that Entity Framework will include the `Supplier` table in the database.</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample3.cs?highlight=9)]

<span data-ttu-id="c3dea-126">WebApiConfig.cs에서 EDM 모델에 "공급 업체" 엔터티를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-126">In WebApiConfig.cs, add a "Suppliers" entity to the EDM model:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample4.cs?highlight=4)]

## <a name="navigation-properties"></a><span data-ttu-id="c3dea-127">탐색 속성</span><span class="sxs-lookup"><span data-stu-id="c3dea-127">Navigation Properties</span></span>

<span data-ttu-id="c3dea-128">제품에 대 한 공급자를 가져오려면 클라이언트는 GET 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-128">To get the supplier for a product, the client sends a GET request:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample5.cmd)]

<span data-ttu-id="c3dea-129">여기 "공급자"은 탐색 속성에는 `Product` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-129">Here "Supplier" is a navigation property on the `Product` type.</span></span> <span data-ttu-id="c3dea-130">이 경우 `Supplier` 참조 속성은 단일 항목을 탐색 하는 컬렉션 (1 대 다 또는 다 대 다 관계)을 반환할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-130">In this case, `Supplier` refers to a single item, but a navigation property can also return a collection (one-to-many or many-to-many relation).</span></span>

<span data-ttu-id="c3dea-131">이 요청을 지원 하려면 다음 메서드를 추가 합니다 `ProductsController` 클래스:</span><span class="sxs-lookup"><span data-stu-id="c3dea-131">To support this request, add the following method to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample6.cs)]

<span data-ttu-id="c3dea-132">합니다 *키* 매개 변수는 제품의 키입니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-132">The *key* parameter is the key of the product.</span></span> <span data-ttu-id="c3dea-133">이 경우 메서드가 반환 관련된 된 엔터티 & amp;#8212는 `Supplier` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="c3dea-133">The method returns the related entity&#8212in this case, a `Supplier` instance.</span></span> <span data-ttu-id="c3dea-134">메서드 이름과 매개 변수 이름 둘 다 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-134">The method name and parameter name are both important.</span></span> <span data-ttu-id="c3dea-135">일반적으로 탐색 속성의 이름이 "X", "GetX" 라는 메서드를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-135">In general, if the navigation property is named "X", you need to add a method named "GetX".</span></span> <span data-ttu-id="c3dea-136">메서드는 라는 매개 변수가 없어야 합니다. "*키*" 부모의 키의 데이터 형식과 일치 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-136">The method must take a parameter named "*key*" that matches the data type of the parent's key.</span></span>

<span data-ttu-id="c3dea-137">포함 하는 일을 해야 이기도 합니다 **[FromOdataUri]** 특성을 *키* 매개 변수.</span><span class="sxs-lookup"><span data-stu-id="c3dea-137">It is also important to include the **[FromOdataUri]** attribute in the *key* parameter.</span></span> <span data-ttu-id="c3dea-138">이 특성은 요청 URI에서에서 키를 구문 분석할 때 OData 구문 규칙을 사용 하는 웹 API에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-138">This attribute tells Web API to use OData syntax rules when it parses the key from the request URI.</span></span>

## <a name="creating-and-deleting-links"></a><span data-ttu-id="c3dea-139">만들기 및 링크 삭제</span><span class="sxs-lookup"><span data-stu-id="c3dea-139">Creating and Deleting Links</span></span>

<span data-ttu-id="c3dea-140">OData는 두 엔터티 간의 관계를 만들거나 제거를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-140">OData supports creating or removing relationships between two entities.</span></span> <span data-ttu-id="c3dea-141">OData 용어 관계의 "링크"입니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-141">In OData terminology, the relationship is a "link."</span></span> <span data-ttu-id="c3dea-142">각 링크에 폼을 사용 하 여 URI *엔터티*/$links /*엔터티*합니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-142">Each link has a URI with the form *entity*/$links/*entity*.</span></span> <span data-ttu-id="c3dea-143">예를 들어, 공급 업체에 대 한 제품에서 링크는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-143">For example, the link from product to supplier looks like this:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample7.cmd)]

<span data-ttu-id="c3dea-144">새 링크를 만들려면 클라이언트 링크 URI에 POST 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-144">To create a new link, the client sends a POST request to the link URI.</span></span> <span data-ttu-id="c3dea-145">요청 본문은 대상 엔터티의 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-145">The body of the request is the URI of the target entity.</span></span> <span data-ttu-id="c3dea-146">예를 들어, "CTSO" 키를 사용 하 여 공급자가 있으며</span><span class="sxs-lookup"><span data-stu-id="c3dea-146">For example, suppose there is a supplier with the key "CTSO".</span></span> <span data-ttu-id="c3dea-147">클라이언트는 "Product(1)"에서 "Supplier('CTSO')"로 링크를 만들려면 다음과 같은 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-147">To create a link from "Product(1)" to "Supplier('CTSO')", the client sends a request like the following:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample8.cmd)]

<span data-ttu-id="c3dea-148">링크를 삭제 하려면 클라이언트가 링크 URI에 DELETE 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-148">To delete a link, the client sends a DELETE request to the link URI.</span></span>

<span data-ttu-id="c3dea-149">**링크 만들기**</span><span class="sxs-lookup"><span data-stu-id="c3dea-149">**Creating Links**</span></span>

<span data-ttu-id="c3dea-150">제품 공급자 링크를 만들려면 클라이언트를 사용 하려면 다음 코드를 추가 합니다 `ProductsController` 클래스:</span><span class="sxs-lookup"><span data-stu-id="c3dea-150">To enable a client to create product-supplier links, add the following code to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample9.cs)]

<span data-ttu-id="c3dea-151">이 메서드는 세 개의 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-151">This method takes three parameters:</span></span>

- <span data-ttu-id="c3dea-152">*키*: 키를 부모 엔터티 (제품)</span><span class="sxs-lookup"><span data-stu-id="c3dea-152">*key*: The key to the parent entity (the product)</span></span>
- <span data-ttu-id="c3dea-153">*navigationProperty*: 탐색 속성의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-153">*navigationProperty*: The name of the navigation property.</span></span> <span data-ttu-id="c3dea-154">이 예제에서는 유효한 탐색 속성이 "공급자"입니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-154">In this example, the only valid navigation property is "Supplier".</span></span>
- <span data-ttu-id="c3dea-155">*링크*: 관련 엔터티의 OData URI입니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-155">*link*: The OData URI of the related entity.</span></span> <span data-ttu-id="c3dea-156">이 값은 요청 본문에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-156">This value is taken from the request body.</span></span> <span data-ttu-id="c3dea-157">예를 들어 링크 URI 않을 "`http://localhost/odata/Suppliers('CTSO')`, 즉 ID 사용 하 여 공급자 'CTSO' =.</span><span class="sxs-lookup"><span data-stu-id="c3dea-157">For example, the link URI might be "`http://localhost/odata/Suppliers('CTSO')`, meaning the supplier with ID = ‘CTSO'.</span></span>

<span data-ttu-id="c3dea-158">메서드는 공급자를 조회 하 링크를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-158">The method uses the link to look up the supplier.</span></span> <span data-ttu-id="c3dea-159">메서드를 설정 하는 일치 하는 공급자가 있으면는 `Product.Supplier` 속성 데이터베이스에 결과 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-159">If the matching supplier is found, the method sets the `Product.Supplier` property and saves the result to the database.</span></span>

<span data-ttu-id="c3dea-160">가장 어려운 부분은 링크 URI를 구문 분석 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-160">The hardest part is parsing the link URI.</span></span> <span data-ttu-id="c3dea-161">기본적으로, URI에 GET 요청을 전송 하는 결과 시뮬레이션 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-161">Basically, you need to simulate the result of sending a GET request to that URI.</span></span> <span data-ttu-id="c3dea-162">다음 도우미 메서드는이 작업을 수행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-162">The following helper method shows how to do this.</span></span> <span data-ttu-id="c3dea-163">메서드는 Web API 라우팅 프로세스를 호출 하 고 다시 가져옵니다는 **ODataPath** 구문 분석 된 OData 경로 나타내는 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-163">The method invokes the Web API routing process and gets back an **ODataPath** instance that represents the parsed OData path.</span></span> <span data-ttu-id="c3dea-164">링크 URI 세그먼트 중 하나의 엔터티 키가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-164">For a link URI, one of the segments should be the entity key.</span></span> <span data-ttu-id="c3dea-165">(그러지 않으면 클라이언트는 잘못 된 URI를 전송 합니다.)</span><span class="sxs-lookup"><span data-stu-id="c3dea-165">(If not, the client sent a bad URI.)</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample10.cs)]

<span data-ttu-id="c3dea-166">**링크 삭제**</span><span class="sxs-lookup"><span data-stu-id="c3dea-166">**Deleting Links**</span></span>

<span data-ttu-id="c3dea-167">링크를 삭제 하려면 다음 코드를 추가 합니다 `ProductsController` 클래스:</span><span class="sxs-lookup"><span data-stu-id="c3dea-167">To delete a link, add the following code to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample11.cs)]

<span data-ttu-id="c3dea-168">이 예제에서는 탐색 속성은 단일 `Supplier` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c3dea-168">In this example, the navigation property is a single `Supplier` entity.</span></span> <span data-ttu-id="c3dea-169">컬렉션 탐색 속성을 사용 하는 경우 링크를 삭제 하려면 URI는 관련된 엔터티에 대 한 키를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-169">If the navigation property is a collection, the URI to delete a link must include a key for the related entity.</span></span> <span data-ttu-id="c3dea-170">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="c3dea-170">For example:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample12.cmd)]

<span data-ttu-id="c3dea-171">이 요청 고객 1에서에서 1을 순서를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-171">This request removes order 1 from customer 1.</span></span> <span data-ttu-id="c3dea-172">이 경우 DeleteLink 메서드는 다음 서명을 가질 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-172">In this case, the DeleteLink method will have the following signature:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample13.cs)]

<span data-ttu-id="c3dea-173">합니다 *relatedKey* 매개 변수는 관련된 엔터티에 대 한 키를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-173">The *relatedKey* parameter gives the key for the related entity.</span></span> <span data-ttu-id="c3dea-174">따라서 프로그램 `DeleteLink` 메서드를 조회 하 여 기본 엔터티는 *키* 매개 변수를 하 여 관련된 엔터티를 찾을 *relatedKey* 매개 변수를 제거한 다음, 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-174">So in your `DeleteLink` method, look up the primary entity by the *key* parameter, find the related entity by the *relatedKey* parameter, and then remove the association.</span></span> <span data-ttu-id="c3dea-175">데이터 모델에 따라서는 버전을 모두 구현 해야 `DeleteLink`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-175">Depending on your data model, you might need to implement both versions of `DeleteLink`.</span></span> <span data-ttu-id="c3dea-176">웹 API는 요청 URI에 따라 올바른 버전을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3dea-176">Web API will call the correct version based on the request URI.</span></span>
