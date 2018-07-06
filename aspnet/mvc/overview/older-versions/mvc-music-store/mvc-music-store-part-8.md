---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
title: '8 부: 쇼핑 카트 Ajax 업데이트를 사용 하 여 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 8 부 Ajax 업데이트와 쇼핑 카트를 설명합니다.
ms.author: aspnetcontent
ms.date: 04/21/2011
ms.assetid: 26b2f55e-ed42-4277-89b0-c941eb754145
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
msc.type: authoredcontent
ms.openlocfilehash: 881d47b5b4df5a4d310a1b3a7eec6ee97b0d42ea
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37823841"
---
<a name="part-8-shopping-cart-with-ajax-updates"></a><span data-ttu-id="b5b4f-104">Ajax 업데이트를 사용 하 여 8 부: 쇼핑 카트</span><span class="sxs-lookup"><span data-stu-id="b5b4f-104">Part 8: Shopping Cart with Ajax Updates</span></span>
====================
<span data-ttu-id="b5b4f-105">[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="b5b4f-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="b5b4f-106">MVC Music Store 자습서 응용 프로그램을 소개 하 고 웹 개발을 위한 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 설명 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="b5b4f-107">MVC Music Store는 온라인 음악 앨범을 판매 하 고 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="b5b4f-108">이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="b5b4f-109">8 부 Ajax 업데이트와 쇼핑 카트를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-109">Part 8 covers Shopping Cart with Ajax Updates.</span></span>


<span data-ttu-id="b5b4f-110">등록 하지 않으면 카트에 앨범을 배치할 수 있게 될 것 이지만 전체를 체크 아웃 게스트로 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-110">We'll allow users to place albums in their cart without registering, but they'll need to register as guests to complete checkout.</span></span> <span data-ttu-id="b5b4f-111">쇼핑 및 체크 아웃 프로세스를 두 명의 컨트롤러도 구분 됩니다: 익명으로 항목을 카트에 추가 허용 하는 ShoppingCart 컨트롤러 및 체크 아웃 프로세스를 처리 하는 체크 아웃 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-111">The shopping and checkout process will be separated into two controllers: a ShoppingCart Controller which allows anonymously adding items to a cart, and a Checkout Controller which handles the checkout process.</span></span> <span data-ttu-id="b5b4f-112">이 섹션에서는 쇼핑 카트를 사용 하 여 시작 하 고 다음 섹션에서 체크 아웃 프로세스를 빌드 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-112">We'll start with the Shopping Cart in this section, then build the Checkout process in the following section.</span></span>

## <a name="adding-the-cart-order-and-orderdetail-model-classes"></a><span data-ttu-id="b5b4f-113">카트, Order 및 OrderDetail 모델 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="b5b4f-113">Adding the Cart, Order, and OrderDetail model classes</span></span>

<span data-ttu-id="b5b4f-114">쇼핑 카트 및 체크 아웃 프로세스를 확인 하는 일부 새 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-114">Our Shopping Cart and Checkout processes will make use of some new classes.</span></span> <span data-ttu-id="b5b4f-115">Models 폴더를 마우스 오른쪽 단추로 클릭 하 고 다음 코드를 사용 하 여 카트 클래스 (Cart.cs)를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-115">Right-click the Models folder and add a Cart class (Cart.cs) with the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample1.cs)]

<span data-ttu-id="b5b4f-116">이 클래스는 여기서 사용한 지금 RecordId 속성에 대 한 [키] 특성을 제외 하 고 다른 사용자에 게 매우 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-116">This class is pretty similar to others we've used so far, with the exception of the [Key] attribute for the RecordId property.</span></span> <span data-ttu-id="b5b4f-117">영구적인 카트 항목 익명 쇼핑 있도록 CartID 라는 문자열 식별자를 갖지만 테이블은 RecordId 라는 정수 기본 키를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-117">Our Cart items will have a string identifier named CartID to allow anonymous shopping, but the table includes an integer primary key named RecordId.</span></span> <span data-ttu-id="b5b4f-118">규칙에 따라 Entity Framework 코드 중심 CartId 또는 ID, 카트 라는 테이블에 대 한 기본 키가 수는 있지만 재정의할 수 있습니다 쉽게 하는 주석 또는 코드를 통해 원하는 경우는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-118">By convention, Entity Framework Code-First expects that the primary key for a table named Cart will be either CartId or ID, but we can easily override that via annotations or code if we want.</span></span> <span data-ttu-id="b5b4f-119">사용 하 여 간단한 규칙에서 Entity Framework Code-first, 우리에 부합 될 때의 예가 되었지만 우리는 제한 되지 이들에 의해 제공 하지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-119">This is an example of how we can use the simple conventions in Entity Framework Code-First when they suit us, but we're not constrained by them when they don't.</span></span>

<span data-ttu-id="b5b4f-120">다음으로, 다음 코드를 사용 하 여 프로그램 Order 클래스 (Order.cs)를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-120">Next, add an Order class (Order.cs) with the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample2.cs)]

<span data-ttu-id="b5b4f-121">이 클래스는 주문에 대 한 요약 및 배달 정보를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-121">This class tracks summary and delivery information for an order.</span></span> <span data-ttu-id="b5b4f-122">**아직 컴파일되지**이므로 해당 속성이 OrderDetails 탐색 아직 만들지 클래스에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-122">**It won't compile yet**, because it has an OrderDetails navigation property which depends on a class we haven't created yet.</span></span> <span data-ttu-id="b5b4f-123">이제 추가 하 여 라는 클래스는 OrderDetail.cs, 다음 코드를 추가 수정 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-123">Let's fix that now by adding a class named OrderDetail.cs, adding the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample3.cs)]

<span data-ttu-id="b5b4f-124">한 번의 마지막 업데이트도 DbSet을 포함 하 여 이러한 새 모델 클래스를 노출 하는 Dbset 포함 MusicStoreEntities 클래스를 만들어 보겠습니다&lt;Artist&gt;합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-124">We'll make one last update to our MusicStoreEntities class to include DbSets which expose those new Model classes, also including a DbSet&lt;Artist&gt;.</span></span> <span data-ttu-id="b5b4f-125">업데이트 된 MusicStoreEntities 클래스 요소로 아래.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-125">The updated MusicStoreEntities class appears as below.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample4.cs)]

## <a name="managing-the-shopping-cart-business-logic"></a><span data-ttu-id="b5b4f-126">쇼핑 카트 비즈니스 논리를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-126">Managing the Shopping Cart business logic</span></span>

<span data-ttu-id="b5b4f-127">다음으로 Models 폴더에서 ShoppingCart 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-127">Next, we'll create the ShoppingCart class in the Models folder.</span></span> <span data-ttu-id="b5b4f-128">ShoppingCart 모델 카트 테이블에 대 한 데이터 액세스를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-128">The ShoppingCart model handles data access to the Cart table.</span></span> <span data-ttu-id="b5b4f-129">또한이 추가 및 장바구니에서 항목을 제거 하기 위한 비즈니스 논리를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-129">Additionally, it will handle the business logic to for adding and removing items from the shopping cart.</span></span>

<span data-ttu-id="b5b4f-130">사용자가 해당 쇼핑 카트에 항목 추가 방금 계정을 등록 하도록 요구 하려고 하지 때문에 할당 됩니다 사용자 임시 고유 식별자 (GUID 또는 전역적으로 고유 식별자를 사용 하 여) 장바구니에 액세스 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-130">Since we don't want to require users to sign up for an account just to add items to their shopping cart, we will assign users a temporary unique identifier (using a GUID, or globally unique identifier) when they access the shopping cart.</span></span> <span data-ttu-id="b5b4f-131">ASP.NET 세션 클래스를 사용 하 여이 ID 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-131">We'll store this ID using the ASP.NET Session class.</span></span>

<span data-ttu-id="b5b4f-132">*참고: ASP.NET 세션은 사이트를 떠난 후에 만료 되는 사용자 관련 정보를 저장 하는 편리한 장소입니다. 세션 상태를 잘못 사용 하면 대규모 사이트에 성능에 미치는 영향을 미칠 수 있습니다, 있지만 밝은 사용 데모 목적 잘 작동 합니다.*</span><span class="sxs-lookup"><span data-stu-id="b5b4f-132">*Note: The ASP.NET Session is a convenient place to store user-specific information which will expire after they leave the site. While misuse of session state can have performance implications on larger sites, our light use will work well for demonstration purposes.*</span></span>

<span data-ttu-id="b5b4f-133">ShoppingCart 클래스는 다음 메서드를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-133">The ShoppingCart class exposes the following methods:</span></span>

<span data-ttu-id="b5b4f-134">**AddToCart** 매개 변수로 앨범을 가져오고 사용자의 장바구니에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-134">**AddToCart** takes an Album as a parameter and adds it to the user's cart.</span></span> <span data-ttu-id="b5b4f-135">카트 표에서 각 앨범에 대 한 수량을 추적 하므로 필요한 경우 새 행 만들기 또는 사용자가 이미 앨범의 사본 하나를 정렬 하는 경우 수량 증가 논리가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-135">Since the Cart table tracks quantity for each album, it includes logic to create a new row if needed or just increment the quantity if the user has already ordered one copy of the album.</span></span>

<span data-ttu-id="b5b4f-136">**RemoveFromCart** 앨범 ID를 가져오고 사용자의 카트에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-136">**RemoveFromCart** takes an Album ID and removes it from the user's cart.</span></span> <span data-ttu-id="b5b4f-137">사용자만 앨범의 복사본 하나에 있으면 해당 카트, 행이 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-137">If the user only had one copy of the album in their cart, the row is removed.</span></span>

<span data-ttu-id="b5b4f-138">**EmptyCart** 사용자의 쇼핑 카트에서 모든 항목을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-138">**EmptyCart** removes all items from a user's shopping cart.</span></span>

<span data-ttu-id="b5b4f-139">**GetCartItems** 표시 또는 처리에 대 한 CartItems 목록을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-139">**GetCartItems** retrieves a list of CartItems for display or processing.</span></span>

<span data-ttu-id="b5b4f-140">**GetCount** 검색을 사용자가 해당 쇼핑 카트에에서 앨범의 총 수입니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-140">**GetCount** retrieves a the total number of albums a user has in their shopping cart.</span></span>

<span data-ttu-id="b5b4f-141">**GetTotal** 바구니에 있는 모든 항목의 총 비용을 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-141">**GetTotal** calculates the total cost of all items in the cart.</span></span>

<span data-ttu-id="b5b4f-142">**CreateOrder** 체크 아웃 단계 동안 쇼핑 카트는 순서로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-142">**CreateOrder** converts the shopping cart to an order during the checkout phase.</span></span>

<span data-ttu-id="b5b4f-143">**GetCart** 카트 개체를 가져오려면이 컨트롤러를 허용 하는 정적 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-143">**GetCart** is a static method which allows our controllers to obtain a cart object.</span></span> <span data-ttu-id="b5b4f-144">사용 합니다 **GetCartId** 는 CartId 사용자의 세션에서 읽기를 처리 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-144">It uses the **GetCartId** method to handle reading the CartId from the user's session.</span></span> <span data-ttu-id="b5b4f-145">GetCartId 메서드 HttpContextBase 필요 하므로 사용자의 CartId 사용자의 세션에서 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-145">The GetCartId method requires the HttpContextBase so that it can read the user's CartId from user's session.</span></span>

<span data-ttu-id="b5b4f-146">전체 다음과 같습니다 **ShoppingCart 클래스**:</span><span class="sxs-lookup"><span data-stu-id="b5b4f-146">Here's the complete **ShoppingCart class**:</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample5.cs)]

## <a name="viewmodels"></a><span data-ttu-id="b5b4f-147">ViewModels</span><span class="sxs-lookup"><span data-stu-id="b5b4f-147">ViewModels</span></span>

<span data-ttu-id="b5b4f-148">쇼핑 카트 컨트롤러는 모델 개체에 완전히 매핑되지 않으므로 해당 보기에 복잡 한 일부 정보를 전달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-148">Our Shopping Cart Controller will need to communicate some complex information to its views which doesn't map cleanly to our Model objects.</span></span> <span data-ttu-id="b5b4f-149">뷰에;에 맞게 모델을 수정 하려고 하지 않습니다. 모델 클래스에는 사용자 인터페이스가 아닌 도메인을 나타내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-149">We don't want to modify our Models to suit our views; Model classes should represent our domain, not the user interface.</span></span> <span data-ttu-id="b5b4f-150">하나의 솔루션 정보 저장소 관리자 드롭다운 정보를 사용 하 여 수행한 있지만 ViewBag을 통해 많은 정보를 전달할 관리 하기가 가져옵니다 ViewBag 클래스를 사용 하 여 뷰를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-150">One solution would be to pass the information to our Views using the ViewBag class, as we did with the Store Manager dropdown information, but passing a lot of information via ViewBag gets hard to manage.</span></span>

<span data-ttu-id="b5b4f-151">이 솔루션을 사용 하는 것은 *ViewModel* 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-151">A solution to this is to use the *ViewModel* pattern.</span></span> <span data-ttu-id="b5b4f-152">이 패턴을 사용 하는 경우 시나리오는 특정 보기에 최적화 된 및 우리의 보기 템플릿에서 필요한 동적 값/콘텐츠에 대 한 속성을 노출 하는 강력한 형식의 클래스 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-152">When using this pattern we create strongly-typed classes that are optimized for our specific view scenarios, and which expose properties for the dynamic values/content needed by our view templates.</span></span> <span data-ttu-id="b5b4f-153">다음 컨트롤러 클래스 채우고 이러한 보기에 최적화 된 클래스를 사용 하 여 보기 템플릿은 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-153">Our controller classes can then populate and pass these view-optimized classes to our view template to use.</span></span> <span data-ttu-id="b5b4f-154">형식 안전성, 컴파일 시간 검사 및 편집기 IntelliSense 템플릿 보기 내에서이 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-154">This enables type-safety, compile-time checking, and editor IntelliSense within view templates.</span></span>

<span data-ttu-id="b5b4f-155">쇼핑 카트 컨트롤러에서 모델 사용에 대 한 두 가지 보기를 만들겠습니다:는 ShoppingCartViewModel 사용자의 쇼핑 카트 내용의 보유할 및 사용자 항목을 제거 하는 경우 확인 정보를 표시 하는 ShoppingCartRemoveViewModel 됩니다 해당 카트에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-155">We'll create two View Models for use in our Shopping Cart controller: the ShoppingCartViewModel will hold the contents of the user's shopping cart, and the ShoppingCartRemoveViewModel will be used to display confirmation information when a user removes something from their cart.</span></span>

<span data-ttu-id="b5b4f-156">구성 고침은 프로젝트의 루트에 새 ViewModels 폴더를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-156">Let's create a new ViewModels folder in the root of our project to keep things organized.</span></span> <span data-ttu-id="b5b4f-157">프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 추가 선택 합니다 / 새 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-157">Right-click the project, select Add / New Folder.</span></span>

![](mvc-music-store-part-8/_static/image1.jpg)

<span data-ttu-id="b5b4f-158">ViewModels 폴더를 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-158">Name the folder ViewModels.</span></span>

![](mvc-music-store-part-8/_static/image1.png)

<span data-ttu-id="b5b4f-159">다음으로, ViewModels 폴더에 ShoppingCartViewModel 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-159">Next, add the ShoppingCartViewModel class in the ViewModels folder.</span></span> <span data-ttu-id="b5b4f-160">두 개의 속성이: 카트 항목 목록과 바구니에 모든 항목에 대 한 총 가격을 저장 하는 10 진수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-160">It has two properties: a list of Cart items, and a decimal value to hold the total price for all items in the cart.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample6.cs)]

<span data-ttu-id="b5b4f-161">이제는 ShoppingCartRemoveViewModel 다음 네 가지 속성을 사용 하 여 ViewModels 폴더에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-161">Now add the ShoppingCartRemoveViewModel to the ViewModels folder, with the following four properties.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample7.cs)]

## <a name="the-shopping-cart-controller"></a><span data-ttu-id="b5b4f-162">쇼핑 카트 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="b5b4f-162">The Shopping Cart Controller</span></span>

<span data-ttu-id="b5b4f-163">쇼핑 카트 컨트롤러는 세 가지 주요 목적이: 항목을 카트에 추가에서 장바구니에 항목을 제거 및 바구니에 항목을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-163">The Shopping Cart controller has three main purposes: adding items to a cart, removing items from the cart, and viewing items in the cart.</span></span> <span data-ttu-id="b5b4f-164">에서는 세 가지 클래스의 사용이 게 방금 만든: ShoppingCartViewModel, ShoppingCartRemoveViewModel, 및 ShoppingCart 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-164">It will make use of the three classes we just created: ShoppingCartViewModel, ShoppingCartRemoveViewModel, and ShoppingCart.</span></span> <span data-ttu-id="b5b4f-165">StoreController, StoreManagerController MusicStoreEntities의 인스턴스를 보관할 필드를 추가 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-165">As in the StoreController and StoreManagerController, we'll add a field to hold an instance of MusicStoreEntities.</span></span>

<span data-ttu-id="b5b4f-166">빈 컨트롤러 템플릿을 사용 하 여 프로젝트에 새 쇼핑 카트 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-166">Add a new Shopping Cart controller to the project using the Empty controller template.</span></span>

![](mvc-music-store-part-8/_static/image2.png)

<span data-ttu-id="b5b4f-167">전체 ShoppingCart 컨트롤러는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-167">Here's the complete ShoppingCart Controller.</span></span> <span data-ttu-id="b5b4f-168">인덱스 및 컨트롤러 추가 작업을 매우 친숙 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-168">The Index and Add Controller actions should look very familiar.</span></span> <span data-ttu-id="b5b4f-169">제거 및 CartSummary 컨트롤러 작업에는 다음 섹션에서 설명 하겠지만 두 가지 특별 한 경우 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-169">The Remove and CartSummary controller actions handle two special cases, which we'll discuss in the following section.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample8.cs)]

## <a name="ajax-updates-with-jquery"></a><span data-ttu-id="b5b4f-170">JQuery 사용 하 여 Ajax 업데이트</span><span class="sxs-lookup"><span data-stu-id="b5b4f-170">Ajax Updates with jQuery</span></span>

<span data-ttu-id="b5b4f-171">쇼핑 카트 인덱스 페이지는 ShoppingCartViewModel를 강력한 형식 이므로 하기 전에 동일한 방법을 사용 하 여 목록 뷰 템플릿을 사용 하는 다음 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-171">We'll next create a Shopping Cart Index page that is strongly typed to the ShoppingCartViewModel and uses the List View template using the same method as before.</span></span>

![](mvc-music-store-part-8/_static/image3.png)

<span data-ttu-id="b5b4f-172">그러나 대신 장바구니에서 항목을 제거 하는 Html.ActionLink 사용에서는 사용 하 여 jQuery "연결" RemoveLink HTML 클래스는이 보기에서 모든 링크의 click 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-172">However, instead of using an Html.ActionLink to remove items from the cart, we'll use jQuery to "wire up" the click event for all links in this view which have the HTML class RemoveLink.</span></span> <span data-ttu-id="b5b4f-173">폼을 게시 하는 대신이 클릭 이벤트 처리기는 RemoveFromCart 컨트롤러 작업에는 AJAX 콜백만 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-173">Rather than posting the form, this click event handler will just make an AJAX callback to our RemoveFromCart controller action.</span></span> <span data-ttu-id="b5b4f-174">RemoveFromCart를 JSON으로 직렬화 된 결과 반환 합니다. jQuery 콜백이 다음 구문 분석 하 고 jQuery를 사용 하 여 네 가지 빠른 업데이트를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-174">The RemoveFromCart returns a JSON serialized result, which our jQuery callback then parses and performs four quick updates to the page using jQuery:</span></span>

- 1. <span data-ttu-id="b5b4f-175">목록에서 삭제 된 앨범을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-175">Removes the deleted album from the list</span></span>
- 2. <span data-ttu-id="b5b4f-176">헤더에 카트 개수를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-176">Updates the cart count in the header</span></span>
- 3. <span data-ttu-id="b5b4f-177">업데이트 메시지를 사용자에 게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-177">Displays an update message to the user</span></span>
- 4. <span data-ttu-id="b5b4f-178">카트 총 가격 업데이트</span><span class="sxs-lookup"><span data-stu-id="b5b4f-178">Updates the cart total price</span></span>

<span data-ttu-id="b5b4f-179">제거 시나리오는 Ajax 콜백 인덱스 뷰 내에서 처리 되 고, 이후 RemoveFromCart 작업에 대 한 자세한 보기를 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-179">Since the remove scenario is being handled by an Ajax callback within the Index view, we don't need an additional view for RemoveFromCart action.</span></span> <span data-ttu-id="b5b4f-180">/ShoppingCart/Index 뷰에 대 한 전체 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-180">Here is the complete code for the /ShoppingCart/Index view:</span></span>

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample9.cshtml)]

<span data-ttu-id="b5b4f-181">이 테스트 하기 위해 당사의 쇼핑 카트에 항목을 추가할 수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-181">In order to test this out, we need to be able to add items to our shopping cart.</span></span> <span data-ttu-id="b5b4f-182">업데이트할 예정 우리의 **저장소 세부 정보** "카트에 추가" 단추를 포함 하는 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-182">We'll update our **Store Details** view to include an "Add to cart" button.</span></span> <span data-ttu-id="b5b4f-183">우리가 하는 동안 일부 추가한는 앨범 추가 정보를 포함할 수 있습니다 것 이므로이 뷰를 마지막으로 업데이트 했습니다: 장르, Artist, 가격 및 앨범 아트.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-183">While we're at it, we can include some of the Album additional information which we've added since we last updated this view: Genre, Artist, Price, and Album Art.</span></span> <span data-ttu-id="b5b4f-184">업데이트 된 코드 저장소 세부 정보 보기에는 아래와 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-184">The updated Store Details view code appears as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample10.cshtml)]

<span data-ttu-id="b5b4f-185">이제 수 스토어를 통해 클릭 하 고 테스트 추가 및 앨범 당사의 쇼핑 카트를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-185">Now we can click through the store and test adding and removing Albums to and from our shopping cart.</span></span> <span data-ttu-id="b5b4f-186">응용 프로그램을 실행 하 고 저장소 인덱스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-186">Run the application and browse to the Store Index.</span></span>

![](mvc-music-store-part-8/_static/image4.png)

<span data-ttu-id="b5b4f-187">장르를 앨범의 목록을 보려면 다음을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-187">Next, click on a Genre to view a list of albums.</span></span>

![](mvc-music-store-part-8/_static/image5.png)

<span data-ttu-id="b5b4f-188">이제는 앨범 제목 클릭 하면 "카트에 추가" 단추를 포함 하 여 업데이트 된 앨범 세부 정보 보기를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-188">Clicking on an Album title now shows our updated Album Details view, including the "Add to cart" button.</span></span>

![](mvc-music-store-part-8/_static/image6.png)

<span data-ttu-id="b5b4f-189">"카트에 추가" 단추를 클릭 하면 쇼핑 카트 요약 목록 사용 하 여 당사의 쇼핑 카트 인덱스 뷰를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-189">Clicking the "Add to cart" button shows our Shopping Cart Index view with the shopping cart summary list.</span></span>

![](mvc-music-store-part-8/_static/image7.png)

<span data-ttu-id="b5b4f-190">쇼핑 카트를 로드 한 후을 쇼핑 카트에 Ajax 업데이트 카트 링크에서 제거를 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-190">After loading up your shopping cart, you can click on the Remove from cart link to see the Ajax update to your shopping cart.</span></span>

![](mvc-music-store-part-8/_static/image8.png)

<span data-ttu-id="b5b4f-191">쇼핑 카트 등록 되지 않은 사용자가 자신의 카트에 항목을 추가할 수 있는 작업을 빌드 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-191">We've built out a working shopping cart which allows unregistered users to add items to their cart.</span></span> <span data-ttu-id="b5b4f-192">다음 섹션에서는 등록 및 체크 아웃 프로세스를 완료 하도록 수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5b4f-192">In the following section, we'll allow them to register and complete the checkout process.</span></span>


> [!div class="step-by-step"]
> <span data-ttu-id="b5b4f-193">[이전](mvc-music-store-part-7.md)
> [다음](mvc-music-store-part-9.md)</span><span class="sxs-lookup"><span data-stu-id="b5b4f-193">[Previous](mvc-music-store-part-7.md)
[Next](mvc-music-store-part-9.md)</span></span>
