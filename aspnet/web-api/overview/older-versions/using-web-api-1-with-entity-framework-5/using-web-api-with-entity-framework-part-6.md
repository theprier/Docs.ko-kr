---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
title: '6 단계: 제품 및 주문 컨트롤러 만들기 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/04/2012
ms.topic: article
ms.assetid: 91ee29ee-0689-40ee-914a-e7dd733b6622
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
msc.type: authoredcontent
ms.openlocfilehash: 6bd485d29821af12b9ebe31b2d04a2d9ab826731
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="part-6-creating-product-and-order-controllers"></a><span data-ttu-id="b5608-102">6 단계: 제품 만들기 및 순서 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="b5608-102">Part 6: Creating Product and Order Controllers</span></span>
====================
<span data-ttu-id="b5608-103">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b5608-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="b5608-104">완료 된 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-a-products-controller"></a><span data-ttu-id="b5608-105">제품 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="b5608-105">Add a Products Controller</span></span>

<span data-ttu-id="b5608-106">관리 컨트롤러에 대 한 관리자 권한이 있는 사용자는입니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-106">The Admin controller is for users who have administrator privileges.</span></span> <span data-ttu-id="b5608-107">고객 반면에 수 제품 보기 하지만 수 없습니다 만들기, 업데이트 또는 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-107">Customers, on the other hand, can view products but cannot create, update, or delete them.</span></span>

<span data-ttu-id="b5608-108">쉽게 Get 메서드를 열어 둔 채로 Post, Put 및 Delete 메서드 액세스를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-108">We can easily restrict access to the Post, Put, and Delete methods, while leaving the Get methods open.</span></span> <span data-ttu-id="b5608-109">하지만 제품에 대해 반환 되는 데이터를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-109">But look at the data that is returned for a product:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample1.json?highlight=1)]

<span data-ttu-id="b5608-110">`ActualCost` 속성 고객에 게 표시 되지 않음을!</span><span class="sxs-lookup"><span data-stu-id="b5608-110">The `ActualCost` property should not be visible to customers!</span></span> <span data-ttu-id="b5608-111">솔루션 정의 하는 것을 *데이터 전송 개체* 고객에 게 표시 되는 속성의 하위 집합을 포함 하는 (DTO).</span><span class="sxs-lookup"><span data-stu-id="b5608-111">The solution is to define a *data transfer object* (DTO) that includes a subset of properties that should be visible to customers.</span></span> <span data-ttu-id="b5608-112">프로젝트에 LINQ를 사용 합니다 `Product` 인스턴스 `ProductDTO` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="b5608-112">We will use LINQ to project `Product` instances to `ProductDTO` instances.</span></span>

<span data-ttu-id="b5608-113">라는 클래스를 추가 `ProductDTO` 모델 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-113">Add a class named `ProductDTO` to the Models folder.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample2.cs)]

<span data-ttu-id="b5608-114">이제 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-114">Now add the controller.</span></span> <span data-ttu-id="b5608-115">솔루션 탐색기에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-115">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="b5608-116">선택 **추가**을 선택한 후 **컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-116">Select **Add**, then select **Controller**.</span></span> <span data-ttu-id="b5608-117">에 **컨트롤러 추가** 대화 상자에서 컨트롤러 이름 &quot;ProductsController&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-117">In the **Add Controller** dialog, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="b5608-118">아래 **템플릿**선택, **빈 API 컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-118">Under **Template**, select **Empty API controller**.</span></span>

![](using-web-api-with-entity-framework-part-6/_static/image1.png)

<span data-ttu-id="b5608-119">소스 파일의 모든 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-119">Replace everything in the source file with the following code:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample3.cs)]

<span data-ttu-id="b5608-120">컨트롤러 여전히 사용 하 여는 `OrdersContext` 데이터베이스를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-120">The controller still uses the `OrdersContext` to query the database.</span></span> <span data-ttu-id="b5608-121">하지만 반환 하는 대신 `Product` 인스턴스를 직접 이라고 `MapProducts` 으로 프로젝션 할 `ProductDTO` 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="b5608-121">But instead of returning `Product` instances directly, we call `MapProducts` to project them onto `ProductDTO` instances:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample4.cs?highlight=1)]

<span data-ttu-id="b5608-122">`MapProducts` 메서드가 반환 되는 **IQueryable**이므로 결과 다른 쿼리 매개 변수를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-122">The `MapProducts` method returns an **IQueryable**, so we can compose the result with other query parameters.</span></span> <span data-ttu-id="b5608-123">볼 수 있습니다는 `GetProduct` 메서드를 추가 하는 **여기서** 쿼리에 절:</span><span class="sxs-lookup"><span data-stu-id="b5608-123">You can see this in the `GetProduct` method, which adds a **where** clause to the query:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample5.cs?highlight=2)]

## <a name="add-an-orders-controller"></a><span data-ttu-id="b5608-124">Orders 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="b5608-124">Add an Orders Controller</span></span>

<span data-ttu-id="b5608-125">다음으로, 사용자가 만들고 주문 볼 수 있도록 하는 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-125">Next, add a controller that lets users create and view orders.</span></span>

<span data-ttu-id="b5608-126">다른 DTO부터 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-126">We'll start with another DTO.</span></span> <span data-ttu-id="b5608-127">솔루션 탐색기에서 모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 라는 클래스를 추가 `OrderDTO` 다음 구현을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-127">In Solution Explorer, right-click the Models folder and add a class named `OrderDTO` Use the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample6.cs)]

<span data-ttu-id="b5608-128">이제 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-128">Now add the controller.</span></span> <span data-ttu-id="b5608-129">솔루션 탐색기에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-129">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="b5608-130">선택 **추가**을 선택한 후 **컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-130">Select **Add**, then select **Controller**.</span></span> <span data-ttu-id="b5608-131">에 **컨트롤러 추가** 대화 상자에서 다음 옵션을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-131">In the **Add Controller** dialog, set the following options:</span></span>

- <span data-ttu-id="b5608-132">아래 **컨트롤러 이름**, "OrdersController"를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-132">Under **Controller Name**, enter "OrdersController".</span></span>
- <span data-ttu-id="b5608-133">아래 **템플릿**선택, "Entity Framework를 사용 하는 읽기/쓰기 동작이 포함 된 API 컨트롤러"입니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-133">Under **Template**, select "API controller with read/write actions, using Entity Framework".</span></span>
- <span data-ttu-id="b5608-134">아래 **모델 클래스**선택, &quot;순서 (ProductStore.Models)&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-134">Under **Model class**, select &quot;Order (ProductStore.Models)&quot;.</span></span>
- <span data-ttu-id="b5608-135">아래 **데이터 컨텍스트 클래스가**선택, &quot;OrdersContext (ProductStore.Models)&quot;합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-135">Under **Data context class**, select &quot;OrdersContext (ProductStore.Models)&quot;.</span></span>

![](using-web-api-with-entity-framework-part-6/_static/image2.png)

<span data-ttu-id="b5608-136">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-136">Click **Add**.</span></span> <span data-ttu-id="b5608-137">OrdersController.cs 라는 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-137">This adds a file named OrdersController.cs.</span></span> <span data-ttu-id="b5608-138">다음으로, 컨트롤러의 기본 구현을 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-138">Next, we need to modify the default implementation of the controller.</span></span>

<span data-ttu-id="b5608-139">먼저, 삭제는 `PutOrder` 및 `DeleteOrder` 메서드.</span><span class="sxs-lookup"><span data-stu-id="b5608-139">First, delete the `PutOrder` and `DeleteOrder` methods.</span></span> <span data-ttu-id="b5608-140">이 샘플에 대 한 고객을 수정 하거나 기존 주문을 삭제 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-140">For this sample, customers cannot modify or delete existing orders.</span></span> <span data-ttu-id="b5608-141">실제 응용 프로그램에서 이러한 경우를 처리 하는 백 엔드 논리의 많은 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-141">In a real application, you would need lots of back-end logic to handle these cases.</span></span> <span data-ttu-id="b5608-142">(예를 들어 순서 이미 출고)?</span><span class="sxs-lookup"><span data-stu-id="b5608-142">(For example, was the order already shipped?)</span></span>

<span data-ttu-id="b5608-143">변경 된 `GetOrders` 메서드를 사용자에 게 속한 주문은를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-143">Change the `GetOrders` method to return just the orders that belong to the user:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample7.cs)]

<span data-ttu-id="b5608-144">변경 된 `GetOrder` 메서드를 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-144">Change the `GetOrder` method as follows:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample8.cs)]

<span data-ttu-id="b5608-145">म 메서드에 수행한 변경 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-145">Here are the changes that we made to the method:</span></span>

- <span data-ttu-id="b5608-146">반환 값은 한 `OrderDTO` 인스턴스 대신는 `Order`합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-146">The return value is an `OrderDTO` instance, instead of an `Order`.</span></span>
- <span data-ttu-id="b5608-147">사용 하 여 순서에 대 한 데이터베이스를 쿼리 하는 경우는 [DbQuery.Include](https://msdn.microsoft.com/library/gg696395) 관련 인출 하는 메서드 `OrderDetail` 및 `Product` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="b5608-147">When we query the database for the order, we use the [DbQuery.Include](https://msdn.microsoft.com/library/gg696395) method to fetch the related `OrderDetail` and `Product` entities.</span></span>
- <span data-ttu-id="b5608-148">예측을 사용 하 여 결과 결합 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-148">We flatten the result by using a projection.</span></span>

<span data-ttu-id="b5608-149">HTTP 응답에는 제품 수량을의 배열을 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-149">The HTTP response will contain an array of products with quantities:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample9.json)]

<span data-ttu-id="b5608-150">이 형식은 보다 (순서, 정보 및 제품) 중첩 된 엔터티가 포함 된 원본 개체 그래프를 사용 하는 클라이언트에 대 한 더 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-150">This format is easier for clients to consume than the original object graph, which contains nested entities (order, details, and products).</span></span>

<span data-ttu-id="b5608-151">마지막 방법을 이해할 수 `PostOrder`합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-151">The last method to consider it `PostOrder`.</span></span> <span data-ttu-id="b5608-152">현재,이 메서드는 `Order` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="b5608-152">Right now, this method takes an `Order` instance.</span></span> <span data-ttu-id="b5608-153">수행 되는 작업 하는 것이 좋습니다. 하지만 클라이언트가 다음과 같이 요청 본문을 보내는 경우:</span><span class="sxs-lookup"><span data-stu-id="b5608-153">But consider what happens if a client sends a request body like this:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample10.json)]

<span data-ttu-id="b5608-154">이것은 잘 구성 된 순서 및 Entity Framework는 코드에 삽입할 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-154">This is a well-structured order, and Entity Framework will happily insert it into the database.</span></span> <span data-ttu-id="b5608-155">하지만 이전에 존재 하지 않는 제품 엔터티를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-155">But it contains a Product entity that did not exist previously.</span></span> <span data-ttu-id="b5608-156">클라이언트는 데이터베이스에 새 제품을 만들었습니다!</span><span class="sxs-lookup"><span data-stu-id="b5608-156">The client just created a new product in our database!</span></span> <span data-ttu-id="b5608-157">색상의 koala 곰은 주문을 나타날 때 순서 fullfilment 부서에 보안 컨텍스트로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-157">This will be a suprise to the order fullfilment department, when they see an order for koala bears.</span></span> <span data-ttu-id="b5608-158">교훈은, POST 또는 PUT 요청에서 허용 하는 데이터에 대 한 매우 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-158">The moral is, be really careful about the data you accept in a POST or PUT request.</span></span>

<span data-ttu-id="b5608-159">이 문제를 방지 하려면 변경 된 `PostOrder` 수행 하는 메서드는 `OrderDTO` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="b5608-159">To avoid this problem, change the `PostOrder` method to take an `OrderDTO` instance.</span></span> <span data-ttu-id="b5608-160">사용 하 여는 `OrderDTO` 만들려는 `Order`합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-160">Use the `OrderDTO` to create the `Order`.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample11.cs)]

<span data-ttu-id="b5608-161">공지를 사용 하는 `ProductID` 및 `Quantity` 되 고, 속성, 제품 이름 또는 가격에 대 한 클라이언트 전송 하는 모든 값을 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-161">Notice that we use the `ProductID` and `Quantity` properties, and we ignore any values that the client sent for either product name or price.</span></span> <span data-ttu-id="b5608-162">제품 ID 유효 하지 않을 경우 데이터베이스의 외래 키 제약 조건을 위반 하 게 됩니다 하 고 예상 대로 삽입 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-162">If the product ID is not valid, it will violate the foreign key constraint in the database, and the insert will fail, as it should.</span></span>

<span data-ttu-id="b5608-163">다음 전체은 `PostOrder` 메서드:</span><span class="sxs-lookup"><span data-stu-id="b5608-163">Here is the complete `PostOrder` method:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample12.cs)]

<span data-ttu-id="b5608-164">마지막으로 추가 된 **Authorize** 특성을 컨트롤러:</span><span class="sxs-lookup"><span data-stu-id="b5608-164">Finally, add the **Authorize** attribute to the controller:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample13.cs)]

<span data-ttu-id="b5608-165">이제 등록 된 사용자만 만들거나 주문을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5608-165">Now only registered users can create or view orders.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b5608-166">[이전](using-web-api-with-entity-framework-part-5.md)
> [다음](using-web-api-with-entity-framework-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="b5608-166">[Previous](using-web-api-with-entity-framework-part-5.md)
[Next](using-web-api-with-entity-framework-part-7.md)</span></span>
