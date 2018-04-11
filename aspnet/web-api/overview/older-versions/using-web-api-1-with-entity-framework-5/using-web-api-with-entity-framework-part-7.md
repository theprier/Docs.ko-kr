---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
title: '7 단계: 기본 만들기 페이지 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/04/2012
ms.topic: article
ms.assetid: eb32a17b-626c-4373-9a7d-3387992f3c04
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
msc.type: authoredcontent
ms.openlocfilehash: 2c378e68a1e6600daf655c19afbfe355e89496d4
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2018
---
<a name="part-7-creating-the-main-page"></a><span data-ttu-id="1abdf-102">7 단계: 기본 만들기 페이지</span><span class="sxs-lookup"><span data-stu-id="1abdf-102">Part 7: Creating the Main Page</span></span>
====================
<span data-ttu-id="1abdf-103">으로 [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="1abdf-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="1abdf-104">완료 된 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-the-main-page"></a><span data-ttu-id="1abdf-105">기본 만들기 페이지</span><span class="sxs-lookup"><span data-stu-id="1abdf-105">Creating the Main Page</span></span>

<span data-ttu-id="1abdf-106">이 섹션에서는 기본 응용 프로그램 페이지를 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-106">In this section, you will create the main application page.</span></span> <span data-ttu-id="1abdf-107">이 페이지 몇 개의 단계에서 않아도 됩니다 म 하므로 관리 페이지에서 보다 복잡 한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-107">This page will be more complex than the Admin page, so we'll approach it in several steps.</span></span> <span data-ttu-id="1abdf-108">과정에서 몇 가지 고급 Knockout.js 기법을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-108">Along the way, you'll see some more advanced Knockout.js techniques.</span></span> <span data-ttu-id="1abdf-109">페이지의 기본 레이아웃 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-109">Here is the basic layout of the page:</span></span>

![](using-web-api-with-entity-framework-part-7/_static/image1.png)

- <span data-ttu-id="1abdf-110">제품의 배열을 포함 하는 "products"입니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-110">"Products" holds an array of products.</span></span>
- <span data-ttu-id="1abdf-111">"Cart" 제품 수량을의 배열을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-111">"Cart" holds an array of products with quantities.</span></span> <span data-ttu-id="1abdf-112">"Add to Cart"를 클릭 합니다. 그러면을 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-112">Clicking "Add to Cart" updates the cart.</span></span>
- <span data-ttu-id="1abdf-113">"Orders" 주문 Id의 배열을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-113">"Orders" holds an array of order IDs.</span></span>
- <span data-ttu-id="1abdf-114">"Details" 항목 (제품 수량이)의 배열이 있는 주문 세부 정보를 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-114">"Details" holds an order detail, which is an array of items (products with quantities)</span></span>

<span data-ttu-id="1abdf-115">데이터 바인딩 또는 스크립트 없이 HTML의 몇 가지 기본적인 레이아웃을 정의 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-115">We'll start by defining some basic layout in HTML, with no data binding or script.</span></span> <span data-ttu-id="1abdf-116">Views/Home/Index.cshtml 파일을 열고 모든 내용을 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-116">Open the file Views/Home/Index.cshtml and replace all of the contents with the following:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample1.html)]

<span data-ttu-id="1abdf-117">다음으로 스크립트 섹션을 추가 하 고 빈 뷰 모델을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-117">Next, add a Scripts section and create an empty view-model:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-7/samples/sample2.cshtml)]

<span data-ttu-id="1abdf-118">예제의 보기 모델 이전 스케치 디자인에 따라, 제품, 카트, 주문 및 세부 정보에 대 한 관찰 가능 개체를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-118">Based on the design sketched earlier, our view model needs observables for products, cart, orders, and details.</span></span> <span data-ttu-id="1abdf-119">다음 변수를 추가 `AppViewModel` 개체:</span><span class="sxs-lookup"><span data-stu-id="1abdf-119">Add the following variables to the `AppViewModel` object:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample3.js)]

<span data-ttu-id="1abdf-120">사용자는 장바구니에 제품 목록에서 항목을 추가할 수 있습니다 및 카트에서 항목을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-120">Users can add items from the products list into the cart, and remove items from the cart.</span></span> <span data-ttu-id="1abdf-121">이러한 함수를 캡슐화 하는 제품을 나타내는 다른 뷰 모델 클래스를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-121">To encapsulate these functions, we'll create another view-model class that represents a product.</span></span> <span data-ttu-id="1abdf-122">다음 코드를 `AppViewModel`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-122">Add the following code to `AppViewModel`:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample4.js?highlight=4)]

<span data-ttu-id="1abdf-123">`ProductViewModel` 카트에서 제품을 이동 하는 데 사용 되는 두 개의 함수를 포함 하는 클래스: `addItemToCart` 카트에, 제품의 한 단위를 추가 하 고 `removeAllFromCart` 제품의 수량을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-123">The `ProductViewModel` class contains two functions that are used to move the product to and from the cart: `addItemToCart` adds one unit of the product to the cart, and `removeAllFromCart` removes all quantities of the product.</span></span>

<span data-ttu-id="1abdf-124">사용자가 기존 주문을 선택 하 고 주문 세부 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-124">Users can select an existing order and get the order details.</span></span> <span data-ttu-id="1abdf-125">다른 보기 모델에이 기능을 캡슐화 합니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-125">We'll encapsulate this functionality into another view-model:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample5.js?highlight=4)]

<span data-ttu-id="1abdf-126">`OrderDetailsViewModel` 는 순서를 사용 하 여 초기화는 서버에 AJAX 요청을 전송 하 여 주문 세부 정보를 인출 합니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-126">The `OrderDetailsViewModel` is initialized with an order, and it fetches the order details by sending an AJAX request to the server.</span></span>

<span data-ttu-id="1abdf-127">또한는 `total` 속성에는 `OrderDetailsViewModel`합니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-127">Also, notice the `total` property on the `OrderDetailsViewModel`.</span></span> <span data-ttu-id="1abdf-128">이 속성은 특수 한 유형의 호출 하는 observable는 [observable 계산](http://knockoutjs.com/documentation/computedObservables.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-128">This property is a special kind of observable called a [computed observable](http://knockoutjs.com/documentation/computedObservables.html).</span></span> <span data-ttu-id="1abdf-129">이름에서 알 수 있듯이 계산된 observable 사용 하면 계산된 된 값을 데이터 바인딩할&#8212;총 순서가 경우 비용이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-129">As the name implies, a computed observable lets you data bind to a computed value&#8212;in this case, the total cost of the order.</span></span>

<span data-ttu-id="1abdf-130">다음으로, 이러한 함수를 추가 `AppViewModel`:</span><span class="sxs-lookup"><span data-stu-id="1abdf-130">Next, add these functions to `AppViewModel`:</span></span>

- <span data-ttu-id="1abdf-131">`resetCart` 그러면에서 모든 항목을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-131">`resetCart` removes all items from the cart.</span></span>
- <span data-ttu-id="1abdf-132">`getDetails` 주문에 대 한 세부 정보를 가져옵니다 (새 pusing 여 `OrderDetailsViewModel` 에 `details` 목록).</span><span class="sxs-lookup"><span data-stu-id="1abdf-132">`getDetails` gets the details for an order (by pusing a new `OrderDetailsViewModel` onto the `details` list).</span></span>
- <span data-ttu-id="1abdf-133">`createOrder` 새 주문을 만들고 카트를 비웁니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-133">`createOrder` creates a new order and empties the cart.</span></span>


[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample6.js?highlight=4)]

<span data-ttu-id="1abdf-134">마지막으로, 제품 및 주문에 대 한 AJAX 요청을 수행 하 여 뷰 모델을 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-134">Finally, initialize the view model by making AJAX requests for the products and orders:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample7.js)]

<span data-ttu-id="1abdf-135">물론는 많은 코드, 하지만 빌드 했습니다를 단계별, 여러분도 이러한 디자인은 선택 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-135">OK, that's a lot of code, but we built it up step-by-step, so hopefully the design is clear.</span></span> <span data-ttu-id="1abdf-136">이제 html 일부 Knockout.js 바인딩을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-136">Now we can add some Knockout.js bindings to the HTML.</span></span>

<span data-ttu-id="1abdf-137">**제품**</span><span class="sxs-lookup"><span data-stu-id="1abdf-137">**Products**</span></span>

<span data-ttu-id="1abdf-138">제품 목록에 대 한 바인딩을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-138">Here are the bindings for the product list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample8.html)]

<span data-ttu-id="1abdf-139">이 제품 배열에 대해 반복 하 고 이름과 가격을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-139">This iterates over the products array and displays the name and price.</span></span> <span data-ttu-id="1abdf-140">"순서에 추가" 단추는 사용자가 로그인 하는 경우에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-140">The "Add to Order" button is visible only when the user is logged in.</span></span>

<span data-ttu-id="1abdf-141">"순서에 추가" 단추 호출 `addItemToCart` 에 `ProductViewModel` 제품에 대 한 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="1abdf-141">The "Add to Order" button calls `addItemToCart` on the `ProductViewModel` instance for the product.</span></span> <span data-ttu-id="1abdf-142">이 Knockout.js의 뛰어난 기능을 보여 줍니다: 뷰 모델 다른 뷰 모델을 포함 된 경우 내부 모델에 해당 바인딩을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-142">This demonstrates a nice feature of Knockout.js: When a view-model contains other view-models, you can apply the bindings to the inner model.</span></span> <span data-ttu-id="1abdf-143">이 예제에서는 바인딩 내에서 `foreach` 각에 적용 되는 `ProductViewModel` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="1abdf-143">In this example, the bindings within the `foreach` are applied to each of the `ProductViewModel` instances.</span></span> <span data-ttu-id="1abdf-144">이 방법은 모든 기능이 단일 보기 모델에 배치 하는 것 보다 더 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-144">This approach is much cleaner than putting all of the functionality into a single view-model.</span></span>

<span data-ttu-id="1abdf-145">**카트**</span><span class="sxs-lookup"><span data-stu-id="1abdf-145">**Cart**</span></span>

<span data-ttu-id="1abdf-146">그러면에 대 한 바인딩을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-146">Here are the bindings for the cart:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample9.html)]

<span data-ttu-id="1abdf-147">카트 배열에 대해 반복 하 고 이름, 가격 및 수량이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-147">This iterates over the cart array and displays the name, price, and quantity.</span></span> <span data-ttu-id="1abdf-148">"제거" 링크와 "주문 작성" 단추가 바인딩됨을 뷰 모델 함수 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-148">Note that the "Remove" link and the "Create Order" button are bound to view-model functions.</span></span>

<span data-ttu-id="1abdf-149">**주문**</span><span class="sxs-lookup"><span data-stu-id="1abdf-149">**Orders**</span></span>

<span data-ttu-id="1abdf-150">다음은 orders 목록에 대 한 바인딩을입니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-150">Here are the bindings for the orders list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample10.html)]

<span data-ttu-id="1abdf-151">이 주문에 대해 반복 하 고 주문 ID를 표시</span><span class="sxs-lookup"><span data-stu-id="1abdf-151">This iterates over the orders and shows the order ID.</span></span> <span data-ttu-id="1abdf-152">링크 클릭 이벤트에 바인딩된는 `getDetails` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-152">The click event on the link is bound to the `getDetails` function.</span></span>

<span data-ttu-id="1abdf-153">**주문 세부 정보**</span><span class="sxs-lookup"><span data-stu-id="1abdf-153">**Order Details**</span></span>

<span data-ttu-id="1abdf-154">주문 세부 정보에 대 한 바인딩을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-154">Here are the bindings for the order details:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample11.html)]

<span data-ttu-id="1abdf-155">이 순서 대로 항목을 반복 하 고 제품, 가격 및 수량을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-155">This iterates over the items in the order and displays the product, price, and quanity.</span></span> <span data-ttu-id="1abdf-156">주변 div 세부 정보 배열 하나 이상의 항목을 포함 하는 경우에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-156">The surrounding div is visible only if the details array contains one or more items.</span></span>

## <a name="conclusion"></a><span data-ttu-id="1abdf-157">결론</span><span class="sxs-lookup"><span data-stu-id="1abdf-157">Conclusion</span></span>

<span data-ttu-id="1abdf-158">이 자습서에서는 데이터베이스 및 데이터 계층 위에 공용 인터페이스를 제공 하는 ASP.NET Web API와 통신 하기 위해 Entity Framework를 사용 하는 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-158">In this tutorial, you created an application that uses Entity Framework to communicate with the database, and ASP.NET Web API to provide a public-facing interface on top of the data layer.</span></span> <span data-ttu-id="1abdf-159">ASP.NET MVC 4을 사용 하 여 렌더링 된 HTML 페이지 및 Knockout.js + jQuery 페이지가 다시 로드 하지 않고 동적 상호 작용을 제공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1abdf-159">We use ASP.NET MVC 4 to render the HTML pages, and Knockout.js plus jQuery to provide dynamic interactions without page reloads.</span></span>

<span data-ttu-id="1abdf-160">추가 리소스:</span><span class="sxs-lookup"><span data-stu-id="1abdf-160">Additional resources:</span></span>

- [<span data-ttu-id="1abdf-161">ASP.NET 데이터 액세스 콘텐츠 맵</span><span class="sxs-lookup"><span data-stu-id="1abdf-161">ASP.NET Data Access Content Map</span></span>](https://msdn.microsoft.com/library/6759sth4.aspx)
- [<span data-ttu-id="1abdf-162">Entity Framework 개발자 센터</span><span class="sxs-lookup"><span data-stu-id="1abdf-162">Entity Framework Developer Center</span></span>](https://msdn.microsoft.com/data/ef)

> [!div class="step-by-step"]
> [<span data-ttu-id="1abdf-163">이전</span><span class="sxs-lookup"><span data-stu-id="1abdf-163">Previous</span></span>](using-web-api-with-entity-framework-part-6.md)
