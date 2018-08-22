---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
title: '5 부: Knockout.js를 사용 하 여 동적 UI 만들기 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 9d9cb3b0-f4a7-434e-a508-9fc0ad0eb813
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
msc.type: authoredcontent
ms.openlocfilehash: d019941700992e173a5812b11b558b6726dfd809
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41828165"
---
<a name="part-5-creating-a-dynamic-ui-with-knockoutjs"></a><span data-ttu-id="acd12-102">5 부: Knockout.js를 사용 하 여 동적 UI 만들기</span><span class="sxs-lookup"><span data-stu-id="acd12-102">Part 5: Creating a Dynamic UI with Knockout.js</span></span>
====================
<span data-ttu-id="acd12-103">[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="acd12-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="acd12-104">완료 된 프로젝트 다운로드</span><span class="sxs-lookup"><span data-stu-id="acd12-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-a-dynamic-ui-with-knockoutjs"></a><span data-ttu-id="acd12-105">Knockout.js를 사용 하 여 동적 UI 만들기</span><span class="sxs-lookup"><span data-stu-id="acd12-105">Creating a Dynamic UI with Knockout.js</span></span>

<span data-ttu-id="acd12-106">이 섹션에서는 관리 보기에 기능을 추가할 Knockout.js 사용 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-106">In this section, we'll use Knockout.js to add functionality to the Admin view.</span></span>

<span data-ttu-id="acd12-107">[Knockout.js](http://knockoutjs.com/) 쉽게 HTML 컨트롤 데이터를 바인딩할 수 있도록 하는 Javascript 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-107">[Knockout.js](http://knockoutjs.com/) is a Javascript library that makes it easy to bind HTML controls to data.</span></span> <span data-ttu-id="acd12-108">Knockout.js-Model-view-viewmodel (MVVM) 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-108">Knockout.js uses the Model-View-ViewModel (MVVM) pattern.</span></span>

- <span data-ttu-id="acd12-109">합니다 *모델* 사례, 제품 및 주문) (에 비즈니스 도메인에 있는 데이터의 서버 쪽 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-109">The *model* is the server-side representation of the data in the business domain (in our case, products and orders).</span></span>
- <span data-ttu-id="acd12-110">합니다 *보기* 는 프레젠테이션 계층 (HTML).</span><span class="sxs-lookup"><span data-stu-id="acd12-110">The *view* is the presentation layer (HTML).</span></span>
- <span data-ttu-id="acd12-111">합니다 *뷰 모델* 는 모델 데이터를 보유 하는 Javascript 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-111">The *view-model* is a Javascript object that holds the model data.</span></span> <span data-ttu-id="acd12-112">보기-모델은 ui 코드 추상화 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-112">The view-model is a code abstraction of the UI.</span></span> <span data-ttu-id="acd12-113">이 HTML 표현의 알지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-113">It has no knowledge of the HTML representation.</span></span> <span data-ttu-id="acd12-114">대신 "항목을 목록"와 같은 뷰의 추상 기능을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-114">Instead, it represents abstract features of the view, such as "a list of items".</span></span>

<span data-ttu-id="acd12-115">뷰는 데이터 바인딩된 뷰 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-115">The view is data-bound to the view-model.</span></span> <span data-ttu-id="acd12-116">보기-모델에 대 한 업데이트 보기에서 자동으로 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-116">Updates to the view-model are automatically reflected in the view.</span></span> <span data-ttu-id="acd12-117">보기-모델은 또한 단추 클릭 같은 보기에서 이벤트를 가져옵니다 하 고 주문 만들기와 같은 모델에 대 한 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-117">The view-model also gets events from the view, such as button clicks, and performs operations on the model, such as creating an order.</span></span>

![](using-web-api-with-entity-framework-part-5/_static/image1.png)

<span data-ttu-id="acd12-118">먼저 보기-모델 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-118">First we'll define the view-model.</span></span> <span data-ttu-id="acd12-119">그런 다음 HTML 태그를 보기-모델에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-119">After that, we will bind the HTML markup to the view-model.</span></span>

<span data-ttu-id="acd12-120">다음 Razor 섹션 Admin.cshtml를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-120">Add the following Razor section to Admin.cshtml:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample1.cshtml)]

<span data-ttu-id="acd12-121">이 섹션에서는 파일에서 아무 곳 이나 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-121">You can add this section anywhere in the file.</span></span> <span data-ttu-id="acd12-122">뷰를 렌더링할 때 HTML 페이지의 맨 아래에 표시 되는 섹션을 닫기 전에 오른쪽 &lt;본문/&gt; 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-122">When the view is rendered, the section appears at the bottom of the HTML page, right before the closing &lt;/body&gt; tag.</span></span>

<span data-ttu-id="acd12-123">이 페이지에 대 한 스크립트의 모든 주석으로 표시 하는 스크립트 태그 내에서 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-123">All of the script for this page will go inside the script tag indicated by the comment:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample2.html)]

<span data-ttu-id="acd12-124">첫째, 보기 모델 클래스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-124">First, define a view-model class:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample3.js)]

<span data-ttu-id="acd12-125">**ko.observableArray** Knockout, 호출의 개체는 특별 한는 *observable*합니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-125">**ko.observableArray** is a special kind of object in Knockout, called an *observable*.</span></span> <span data-ttu-id="acd12-126">[Knockout.js 설명서](http://knockoutjs.com/documentation/observables.html):는 관찰 가능 개체는 "JavaScript 개체 변경 내용에 대 한 구독자에 알릴 수 있는."</span><span class="sxs-lookup"><span data-stu-id="acd12-126">From the [Knockout.js documentation](http://knockoutjs.com/documentation/observables.html): An observable is a "JavaScript object that can notify subscribers about changes."</span></span> <span data-ttu-id="acd12-127">관찰 가능 개체의 내용이 변경 되 면 뷰 일치 하도록 자동 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-127">When the contents of an observable change, the view is automatically updated to match.</span></span>

<span data-ttu-id="acd12-128">채우는 데는 `products` 배열, 웹 API에 AJAX 요청을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-128">To populate the `products` array, make an AJAX request to the web API.</span></span> <span data-ttu-id="acd12-129">뷰 모음에서 API에 대 한 기본 URI를 저장 했습니다 회수 (참조 [4 부](using-web-api-with-entity-framework-part-4.md) 자습서).</span><span class="sxs-lookup"><span data-stu-id="acd12-129">Recall that we stored the base URI for the API in the view bag (see [Part 4](using-web-api-with-entity-framework-part-4.md) of the tutorial).</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample4.js?highlight=5)]

<span data-ttu-id="acd12-130">다음으로, 만들기, 업데이트 및 삭제할 제품 보기-모델 함수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-130">Next, add functions to the view-model to create, update, and delete products.</span></span> <span data-ttu-id="acd12-131">이러한 함수는 웹 API에 대 한 AJAX 호출을 제출 하 고 보기-모델을 업데이트 하는 결과 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-131">These functions submit AJAX calls to the web API and use the results to update the view-model.</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample5.js?highlight=7)]

<span data-ttu-id="acd12-132">가장 중요 한 부분은 이제: 경우 DOM은 fulled 로드를 호출 합니다 **ko.applyBindings** 함수 및의 새 인스턴스를 전달 합니다 `ProductsViewModel`:</span><span class="sxs-lookup"><span data-stu-id="acd12-132">Now the most important part: When the DOM is fulled loaded, call the **ko.applyBindings** function and pass in a new instance of the `ProductsViewModel`:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample6.js)]

<span data-ttu-id="acd12-133">합니다 **ko.applyBindings** 메서드 Knockout을 활성화 하 고 보기 모델 보기에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-133">The **ko.applyBindings** method activates Knockout and wires up the view-model to the view.</span></span>

<span data-ttu-id="acd12-134">보기-모델을 만들었으므로 이제 해당 바인딩을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-134">Now that we have a view-model, we can create the bindings.</span></span> <span data-ttu-id="acd12-135">Knockout.js,이 작업을 수행을 더하여 `data-bind` HTML 요소에 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-135">In Knockout.js, you do this by adding `data-bind` attributes to HTML elements.</span></span> <span data-ttu-id="acd12-136">예를 들어, 배열에 바인딩하는 HTML 목록에 사용 된 `foreach` 바인딩:</span><span class="sxs-lookup"><span data-stu-id="acd12-136">For example, to bind an HTML list to an array, use the `foreach` binding:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample7.html?highlight=1)]

<span data-ttu-id="acd12-137">`foreach` 바인딩 배열에서 반복 및 배열에 있는 자식 각 개체에 대 한 요소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-137">The `foreach` binding iterates through the array and creates child elements for each object in the array.</span></span> <span data-ttu-id="acd12-138">자식 요소에 바인딩을 배열 개체의 속성을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-138">Bindings on the child elements can refer to properties on the array objects.</span></span>

<span data-ttu-id="acd12-139">다음 바인딩 "업데이트 제품" 목록에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-139">Add the following bindings to the "update-products" list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample8.html)]

<span data-ttu-id="acd12-140">합니다 `<li>` 요소가 범위 내에서 발생 합니다 **foreach** 바인딩.</span><span class="sxs-lookup"><span data-stu-id="acd12-140">The `<li>` element occurs within the scope of the **foreach** binding.</span></span> <span data-ttu-id="acd12-141">Knockout 됩니다 의미에서 각 제품에 한 번씩 요소를 렌더링 하는 `products` 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-141">That means Knockout will render the element once for each product in the `products` array.</span></span> <span data-ttu-id="acd12-142">모든 내에서 바인딩에 `<li>` 요소는 제품 인스턴스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-142">All of the bindings within the `<li>` element refer to that product instance.</span></span> <span data-ttu-id="acd12-143">예를 들어 `$data.Name` 가리킵니다는 `Name` 제품에는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-143">For example, `$data.Name` refers to the `Name` property on the product.</span></span>

<span data-ttu-id="acd12-144">텍스트 입력의 값을 설정 하려면 사용 된 `value` 바인딩.</span><span class="sxs-lookup"><span data-stu-id="acd12-144">To set the values of the text inputs, use the `value` binding.</span></span> <span data-ttu-id="acd12-145">모델-뷰, 함수에 바인딩된 단추를 사용 하는 `click` 바인딩.</span><span class="sxs-lookup"><span data-stu-id="acd12-145">The buttons are bound to functions on the model-view, using the `click` binding.</span></span> <span data-ttu-id="acd12-146">Product 인스턴스의 각 함수에 매개 변수로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-146">The product instance is passed as a parameter to each function.</span></span> <span data-ttu-id="acd12-147">자세한 내용은 합니다 [Knockout.js 설명서](http://knockoutjs.com/documentation/observables.html) 다양 한 바인딩의 좋은 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-147">For more information, the [Knockout.js documentation](http://knockoutjs.com/documentation/observables.html) has good descriptions of the various bindings.</span></span>

<span data-ttu-id="acd12-148">그런 다음에 대 한 바인딩을 추가 합니다 **제출** 제품 추가 폼에서 이벤트:</span><span class="sxs-lookup"><span data-stu-id="acd12-148">Next, add a binding for the **submit** event on the Add Product form:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample9.html)]

<span data-ttu-id="acd12-149">이 바인딩 호출을 `create` 새 제품을 만드는 보기 모델에는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-149">This binding calls the `create` function on the view-model to create a new product.</span></span>

<span data-ttu-id="acd12-150">관리 보기에 대 한 전체 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-150">Here is the complete code for the Admin view:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample10.cshtml)]

<span data-ttu-id="acd12-151">응용 프로그램을 실행 하 고 관리자 계정으로 로그인 "Admin" 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-151">Run the application, log in with the Administrator account, and click the "Admin" link.</span></span> <span data-ttu-id="acd12-152">제품의 목록을 보려면를 만들기, 업데이트 또는 제품을 삭제 하는 일을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd12-152">You should see the list of products, and be able to create, update, or delete products.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="acd12-153">[이전](using-web-api-with-entity-framework-part-4.md)
> [다음](using-web-api-with-entity-framework-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="acd12-153">[Previous](using-web-api-with-entity-framework-part-4.md)
[Next](using-web-api-with-entity-framework-part-6.md)</span></span>
