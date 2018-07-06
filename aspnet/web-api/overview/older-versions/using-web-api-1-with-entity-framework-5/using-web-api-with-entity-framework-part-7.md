---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
title: '7 부: 만드는 주 페이지 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 07/04/2012
ms.assetid: eb32a17b-626c-4373-9a7d-3387992f3c04
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
msc.type: authoredcontent
ms.openlocfilehash: c5b6cb0f2e48cdea3d6cc5cde72d08a99126f05f
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37825637"
---
<a name="part-7-creating-the-main-page"></a><span data-ttu-id="5594c-102">7 부: 기본 만들기 페이지</span><span class="sxs-lookup"><span data-stu-id="5594c-102">Part 7: Creating the Main Page</span></span>
====================
<span data-ttu-id="5594c-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="5594c-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="5594c-104">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="5594c-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-the-main-page"></a><span data-ttu-id="5594c-105">기본 만들기 페이지</span><span class="sxs-lookup"><span data-stu-id="5594c-105">Creating the Main Page</span></span>

<span data-ttu-id="5594c-106">이 섹션에서는 주요 응용 프로그램 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-106">In this section, you will create the main application page.</span></span> <span data-ttu-id="5594c-107">이 페이지에서는 여러 단계에서 접근 됩니다 있도록 관리 페이지에서 보다 복잡 한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-107">This page will be more complex than the Admin page, so we'll approach it in several steps.</span></span> <span data-ttu-id="5594c-108">이 과정에서 몇 가지 고급 Knockout.js 기술을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-108">Along the way, you'll see some more advanced Knockout.js techniques.</span></span> <span data-ttu-id="5594c-109">페이지의 기본 레이아웃은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-109">Here is the basic layout of the page:</span></span>

![](using-web-api-with-entity-framework-part-7/_static/image1.png)

- <span data-ttu-id="5594c-110">"제품" 제품의 배열을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-110">"Products" holds an array of products.</span></span>
- <span data-ttu-id="5594c-111">"Cart" 수량을 사용 하 여 제품의 배열을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-111">"Cart" holds an array of products with quantities.</span></span> <span data-ttu-id="5594c-112">"Add to Cart"를 클릭 하 여 카트를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-112">Clicking "Add to Cart" updates the cart.</span></span>
- <span data-ttu-id="5594c-113">"Orders" 주문 Id의 배열을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-113">"Orders" holds an array of order IDs.</span></span>
- <span data-ttu-id="5594c-114">"세부 정보" 항목 (제품 수량을 사용 하 여)의 배열 되는 주문 세부 정보를 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-114">"Details" holds an order detail, which is an array of items (products with quantities)</span></span>

<span data-ttu-id="5594c-115">데이터 바인딩이 없거나 스크립트를 사용 하 여 html, 일부 기본 레이아웃을 정의 하 여 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-115">We'll start by defining some basic layout in HTML, with no data binding or script.</span></span> <span data-ttu-id="5594c-116">Views/Home/Index.cshtml 파일을 열고 모든 콘텐츠를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-116">Open the file Views/Home/Index.cshtml and replace all of the contents with the following:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample1.html)]

<span data-ttu-id="5594c-117">다음으로, 스크립트 섹션을 추가 하 고 빈 보기-모델을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-117">Next, add a Scripts section and create an empty view-model:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-7/samples/sample2.cshtml)]

<span data-ttu-id="5594c-118">보기 모델 스케치 이전 디자인에 따라 제품, 카트, 주문 및 세부 정보에 대 한 관찰 가능 개체를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-118">Based on the design sketched earlier, our view model needs observables for products, cart, orders, and details.</span></span> <span data-ttu-id="5594c-119">다음 변수를 추가 합니다 `AppViewModel` 개체:</span><span class="sxs-lookup"><span data-stu-id="5594c-119">Add the following variables to the `AppViewModel` object:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample3.js)]

<span data-ttu-id="5594c-120">사용자가 장바구니에에 제품 목록에서 항목을 추가 하 고 장바구니에서 항목을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-120">Users can add items from the products list into the cart, and remove items from the cart.</span></span> <span data-ttu-id="5594c-121">이러한 함수를 캡슐화 하는 제품을 나타내는 다른 보기 모델 클래스를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-121">To encapsulate these functions, we'll create another view-model class that represents a product.</span></span> <span data-ttu-id="5594c-122">다음 코드를 `AppViewModel`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-122">Add the following code to `AppViewModel`:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample4.js?highlight=4)]

<span data-ttu-id="5594c-123">합니다 `ProductViewModel` 클래스에 카트에서 제품을 이동 하는 데 사용 되는 두 가지 함수가 포함 되어 있습니다.: `addItemToCart` 장바구니에 제품의 단위를 하나 추가 및 `removeAllFromCart` 제품의 수량을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-123">The `ProductViewModel` class contains two functions that are used to move the product to and from the cart: `addItemToCart` adds one unit of the product to the cart, and `removeAllFromCart` removes all quantities of the product.</span></span>

<span data-ttu-id="5594c-124">사용자는 기존 주문을 선택 하 고 주문 세부 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-124">Users can select an existing order and get the order details.</span></span> <span data-ttu-id="5594c-125">이 기능은 다른 보기 모델에 캡슐화 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-125">We'll encapsulate this functionality into another view-model:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample5.js?highlight=4)]

<span data-ttu-id="5594c-126">`OrderDetailsViewModel` 순서를 사용 하 여 초기화 됩니다 및 AJAX 요청을 서버로 전송 하 여 주문 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-126">The `OrderDetailsViewModel` is initialized with an order, and it fetches the order details by sending an AJAX request to the server.</span></span>

<span data-ttu-id="5594c-127">또한 합니다 `total` 속성에는 `OrderDetailsViewModel`합니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-127">Also, notice the `total` property on the `OrderDetailsViewModel`.</span></span> <span data-ttu-id="5594c-128">이 속성은 특수 한 유형의 호출 하는 관찰 가능 개체를 [관찰 가능 개체를 계산](http://knockoutjs.com/documentation/computedObservables.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-128">This property is a special kind of observable called a [computed observable](http://knockoutjs.com/documentation/computedObservables.html).</span></span> <span data-ttu-id="5594c-129">이름에서 알 수 있듯이 계산된 observable 사용 하면 계산 된 값을 데이터 바인딩&#8212;주문의 총 비용이 예제의 경우.</span><span class="sxs-lookup"><span data-stu-id="5594c-129">As the name implies, a computed observable lets you data bind to a computed value&#8212;in this case, the total cost of the order.</span></span>

<span data-ttu-id="5594c-130">이러한 함수를 다음으로, 추가 `AppViewModel`:</span><span class="sxs-lookup"><span data-stu-id="5594c-130">Next, add these functions to `AppViewModel`:</span></span>

- <span data-ttu-id="5594c-131">`resetCart` 카트에서 모든 항목을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-131">`resetCart` removes all items from the cart.</span></span>
- <span data-ttu-id="5594c-132">`getDetails` 주문에 대 한 세부 정보를 가져옵니다 (새 pusing 하 여 `OrderDetailsViewModel` 에 `details` 목록).</span><span class="sxs-lookup"><span data-stu-id="5594c-132">`getDetails` gets the details for an order (by pusing a new `OrderDetailsViewModel` onto the `details` list).</span></span>
- <span data-ttu-id="5594c-133">`createOrder` 새 주문을 만들고 장바구니를 비웁니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-133">`createOrder` creates a new order and empties the cart.</span></span>


[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample6.js?highlight=4)]

<span data-ttu-id="5594c-134">마지막으로, 제품 및 주문에 대 한 AJAX 요청을 만들어 뷰 모델을 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-134">Finally, initialize the view model by making AJAX requests for the products and orders:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample7.js)]

<span data-ttu-id="5594c-135">그렇다면 코드의 많은 하지만 빌드 하였습니다 up 단계별 여러분도 이러한 디자인은의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-135">OK, that's a lot of code, but we built it up step-by-step, so hopefully the design is clear.</span></span> <span data-ttu-id="5594c-136">이제 html 일부 Knockout.js 바인딩을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-136">Now we can add some Knockout.js bindings to the HTML.</span></span>

<span data-ttu-id="5594c-137">**제품**</span><span class="sxs-lookup"><span data-stu-id="5594c-137">**Products**</span></span>

<span data-ttu-id="5594c-138">제품 목록에 대 한 바인딩을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-138">Here are the bindings for the product list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample8.html)]

<span data-ttu-id="5594c-139">이 제품 배열을 반복 하 고 이름과 가격을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-139">This iterates over the products array and displays the name and price.</span></span> <span data-ttu-id="5594c-140">"순서에 추가" 단추를 사용자가 로그인 하는 경우에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-140">The "Add to Order" button is visible only when the user is logged in.</span></span>

<span data-ttu-id="5594c-141">"순서에 추가" 단추 호출 `addItemToCart` 에 `ProductViewModel` 제품에 대 한 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="5594c-141">The "Add to Order" button calls `addItemToCart` on the `ProductViewModel` instance for the product.</span></span> <span data-ttu-id="5594c-142">Knockout.js의 뛰어난 기능을 보여 줍니다: 다른 보기 모델에 포함 되어 있으면 보기-모델 내부 모델에 해당 바인딩을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-142">This demonstrates a nice feature of Knockout.js: When a view-model contains other view-models, you can apply the bindings to the inner model.</span></span> <span data-ttu-id="5594c-143">이 예제에서는 내에서 바인딩에 합니다 `foreach` 각각에 적용 되는 `ProductViewModel` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="5594c-143">In this example, the bindings within the `foreach` are applied to each of the `ProductViewModel` instances.</span></span> <span data-ttu-id="5594c-144">이 방법은 단일 보기-모델에 배치 하는 모든 기능 보다 훨씬 더 명확 합니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-144">This approach is much cleaner than putting all of the functionality into a single view-model.</span></span>

<span data-ttu-id="5594c-145">**카트**</span><span class="sxs-lookup"><span data-stu-id="5594c-145">**Cart**</span></span>

<span data-ttu-id="5594c-146">카트 바인딩을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-146">Here are the bindings for the cart:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample9.html)]

<span data-ttu-id="5594c-147">이 카트 배열을 반복 하 고 이름, 가격 및 수량을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-147">This iterates over the cart array and displays the name, price, and quantity.</span></span> <span data-ttu-id="5594c-148">연결 "제거" 및 "주문 작성" 단추를 뷰 모델 함수에 바인딩되어 있는지 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-148">Note that the "Remove" link and the "Create Order" button are bound to view-model functions.</span></span>

<span data-ttu-id="5594c-149">**주문**</span><span class="sxs-lookup"><span data-stu-id="5594c-149">**Orders**</span></span>

<span data-ttu-id="5594c-150">주문 목록에 대 한 바인딩을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-150">Here are the bindings for the orders list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample10.html)]

<span data-ttu-id="5594c-151">이 주문이 될 때까지 반복 하 고 주문 ID를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-151">This iterates over the orders and shows the order ID.</span></span> <span data-ttu-id="5594c-152">링크의 click 이벤트 바인딩되는 `getDetails` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-152">The click event on the link is bound to the `getDetails` function.</span></span>

<span data-ttu-id="5594c-153">**주문 세부 정보**</span><span class="sxs-lookup"><span data-stu-id="5594c-153">**Order Details**</span></span>

<span data-ttu-id="5594c-154">주문 세부 정보에 대 한 바인딩을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-154">Here are the bindings for the order details:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample11.html)]

<span data-ttu-id="5594c-155">이 순서 대로 항목을 반복 하 고 제품, 가격 및 수량을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-155">This iterates over the items in the order and displays the product, price, and quanity.</span></span> <span data-ttu-id="5594c-156">주변 div 세부 정보 배열 하나 이상의 항목을 포함 하는 경우에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-156">The surrounding div is visible only if the details array contains one or more items.</span></span>

## <a name="conclusion"></a><span data-ttu-id="5594c-157">결론</span><span class="sxs-lookup"><span data-stu-id="5594c-157">Conclusion</span></span>

<span data-ttu-id="5594c-158">이 자습서에서는 ASP.NET Web API 데이터 계층을 기반으로 공용 인터페이스를 제공 하 고 데이터베이스를 사용 하 여 통신 하기 위해 Entity Framework를 사용 하는 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-158">In this tutorial, you created an application that uses Entity Framework to communicate with the database, and ASP.NET Web API to provide a public-facing interface on top of the data layer.</span></span> <span data-ttu-id="5594c-159">ASP.NET MVC 4 렌더링할 HTML 페이지 및 Knockout.js 및 jQuery 페이지를 다시 로드 하지 않고 동적 상호 작용을 제공 하려면 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5594c-159">We use ASP.NET MVC 4 to render the HTML pages, and Knockout.js plus jQuery to provide dynamic interactions without page reloads.</span></span>

<span data-ttu-id="5594c-160">추가 리소스:</span><span class="sxs-lookup"><span data-stu-id="5594c-160">Additional resources:</span></span>

- [<span data-ttu-id="5594c-161">ASP.NET 데이터 액세스 콘텐츠 맵</span><span class="sxs-lookup"><span data-stu-id="5594c-161">ASP.NET Data Access Content Map</span></span>](https://msdn.microsoft.com/library/6759sth4.aspx)
- [<span data-ttu-id="5594c-162">Entity Framework 개발자 센터</span><span class="sxs-lookup"><span data-stu-id="5594c-162">Entity Framework Developer Center</span></span>](https://msdn.microsoft.com/data/ef)

> [!div class="step-by-step"]
> [<span data-ttu-id="5594c-163">이전</span><span class="sxs-lookup"><span data-stu-id="5594c-163">Previous</span></span>](using-web-api-with-entity-framework-part-6.md)
