---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
title: "8 단계: 쇼핑 카트 Ajax 업데이트 | Microsoft Docs"
author: jongalloway
description: "이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 8 부 쇼핑 카트 Ajax 업데이트를 설명합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/21/2011
ms.topic: article
ms.assetid: 26b2f55e-ed42-4277-89b0-c941eb754145
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
msc.type: authoredcontent
ms.openlocfilehash: 75e1dff96f8b56d74c28ff9d522f4766fbad669f
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="part-8-shopping-cart-with-ajax-updates"></a><span data-ttu-id="3c41d-104">Ajax 업데이트와 8 단계: 쇼핑 카트</span><span class="sxs-lookup"><span data-stu-id="3c41d-104">Part 8: Shopping Cart with Ajax Updates</span></span>
====================
<span data-ttu-id="3c41d-105">으로 [Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="3c41d-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="3c41d-106">MVC Music Store는 소개 하 고 웹 개발에 대 한 ASP.NET MVC와 Visual Studio를 사용 하는 방법을 단계별로 설명 하는 자습서 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="3c41d-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="3c41d-107">MVC Music Store는 온라인 음악 앨범 판매 및 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="3c41d-108">이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="3c41d-109">8 부 쇼핑 카트 Ajax 업데이트를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-109">Part 8 covers Shopping Cart with Ajax Updates.</span></span>


<span data-ttu-id="3c41d-110">등록을 하지 않고 카트에 앨범을 배치 하도록 사용자 허용 합니다 하지만 게스트는 완료 체크 아웃으로 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-110">We'll allow users to place albums in their cart without registering, but they'll need to register as guests to complete checkout.</span></span> <span data-ttu-id="3c41d-111">두 컨트롤러에 쇼핑 및 체크 아웃 프로세스를 구분 됩니다: 익명으로 장바구니에 항목을 추가 하도록 허용 하는 ShoppingCart 컨트롤러 및 체크 아웃 프로세스를 처리 하는 체크 아웃 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-111">The shopping and checkout process will be separated into two controllers: a ShoppingCart Controller which allows anonymously adding items to a cart, and a Checkout Controller which handles the checkout process.</span></span> <span data-ttu-id="3c41d-112">이 섹션에서는 쇼핑 카트로 시작 그런 다음 다음 섹션에는 체크 아웃 프로세스를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-112">We'll start with the Shopping Cart in this section, then build the Checkout process in the following section.</span></span>

## <a name="adding-the-cart-order-and-orderdetail-model-classes"></a><span data-ttu-id="3c41d-113">카트, 순서 및 OrderDetail 모델 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-113">Adding the Cart, Order, and OrderDetail model classes</span></span>

<span data-ttu-id="3c41d-114">프로세스 당사의 쇼핑 카트 및 체크 아웃 하면 몇 가지 새로운 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-114">Our Shopping Cart and Checkout processes will make use of some new classes.</span></span> <span data-ttu-id="3c41d-115">모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 다음 코드로 카트 클래스 (Cart.cs)를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-115">Right-click the Models folder and add a Cart class (Cart.cs) with the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample1.cs)]

<span data-ttu-id="3c41d-116">이 클래스는 사용한 지금까지 RecordId 속성에 대 한 [Key] 특성을 제외 하 고 다른 사용자에 게 매우 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-116">This class is pretty similar to others we've used so far, with the exception of the [Key] attribute for the RecordId property.</span></span> <span data-ttu-id="3c41d-117">우리의 카트에 항목 라는 CartID 익명 쇼핑 수 있도록 하는 문자열 식별자 하지만 테이블 RecordId 라는 정수 기본 키가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-117">Our Cart items will have a string identifier named CartID to allow anonymous shopping, but the table includes an integer primary key named RecordId.</span></span> <span data-ttu-id="3c41d-118">규칙에 따라 엔터티 프레임 워크 코드 중심 CartId 또는 ID, 카트 라는 테이블에 대 한 기본 키 됩니다 하지만 म 쉽게 재정의할 수 있는 주석 또는 코드를 통해 원하는 경우 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-118">By convention, Entity Framework Code-First expects that the primary key for a table named Cart will be either CartId or ID, but we can easily override that via annotations or code if we want.</span></span> <span data-ttu-id="3c41d-119">사용 하는 방법을 간단한 규칙에서 Entity Framework 코드 중심 us, 맞게 될 때의 예 이지만 우리는 제한 되지 않으며 타인이 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-119">This is an example of how we can use the simple conventions in Entity Framework Code-First when they suit us, but we're not constrained by them when they don't.</span></span>

<span data-ttu-id="3c41d-120">다음으로, 다음 코드와 함께 Order 클래스 (Order.cs)를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-120">Next, add an Order class (Order.cs) with the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample2.cs)]

<span data-ttu-id="3c41d-121">이 클래스는 주문에 대 한 요약 및 배달 정보를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-121">This class tracks summary and delivery information for an order.</span></span> <span data-ttu-id="3c41d-122">**아직 컴파일되지**는 아직 만들지 클래스에 종속 되어 있는 OrderDetails 탐색 속성에 있기 때문에, 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-122">**It won't compile yet**, because it has an OrderDetails navigation property which depends on a class we haven't created yet.</span></span> <span data-ttu-id="3c41d-123">이제 추가 하 여 라는 클래스는 다음 코드를 추가 OrderDetail.cs 문제 해결 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-123">Let's fix that now by adding a class named OrderDetail.cs, adding the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample3.cs)]

<span data-ttu-id="3c41d-124">또한 한 DbSet을 포함 하 여 이러한 새 모델 클래스를 표시 하는 DbSets 포함 하도록 MusicStoreEntities 클래스를 마지막 업데이트 한 개 만들면 되&lt;아티스트&gt;합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-124">We'll make one last update to our MusicStoreEntities class to include DbSets which expose those new Model classes, also including a DbSet&lt;Artist&gt;.</span></span> <span data-ttu-id="3c41d-125">로 표시 된 업데이트 된 MusicStoreEntities 클래스 아래 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-125">The updated MusicStoreEntities class appears as below.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample4.cs)]

## <a name="managing-the-shopping-cart-business-logic"></a><span data-ttu-id="3c41d-126">쇼핑 카트 비즈니스 논리를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-126">Managing the Shopping Cart business logic</span></span>

<span data-ttu-id="3c41d-127">다음으로, ShoppingCart 클래스를 모델 폴더에서 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-127">Next, we'll create the ShoppingCart class in the Models folder.</span></span> <span data-ttu-id="3c41d-128">ShoppingCart 모델 카트 테이블에 대 한 데이터 액세스를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-128">The ShoppingCart model handles data access to the Cart table.</span></span> <span data-ttu-id="3c41d-129">또한 것은 추가 및 쇼핑 카트에서 항목을 제거 하기 위한 비즈니스 논리를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-129">Additionally, it will handle the business logic to for adding and removing items from the shopping cart.</span></span>

<span data-ttu-id="3c41d-130">사용자가 장바구니에 항목 추가를 계정에 등록 하도록 요구 하 않도록, 하기는 할당 사용자가 임시 고유 식별자 (GUID 또는 전역 고유 식별자를 사용 하 여) 쇼핑 카트를 액세스할 때.</span><span class="sxs-lookup"><span data-stu-id="3c41d-130">Since we don't want to require users to sign up for an account just to add items to their shopping cart, we will assign users a temporary unique identifier (using a GUID, or globally unique identifier) when they access the shopping cart.</span></span> <span data-ttu-id="3c41d-131">ASP.NET 세션 클래스를 사용 하 여이 ID 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-131">We'll store this ID using the ASP.NET Session class.</span></span>

<span data-ttu-id="3c41d-132">*참고: ASP.NET 세션은 사이트를 벗어난 후에 만료 되는 사용자 관련 정보를 저장 하는 편리한 장소입니다. 세션 상태를 잘못 사용 하면 대규모 사이트 성능에 미치는 영향을 있을 수 있지만, 밝은 사용 예시 목적을 위한 잘 작동 합니다.*</span><span class="sxs-lookup"><span data-stu-id="3c41d-132">*Note: The ASP.NET Session is a convenient place to store user-specific information which will expire after they leave the site. While misuse of session state can have performance implications on larger sites, our light use will work well for demonstration purposes.*</span></span>

<span data-ttu-id="3c41d-133">ShoppingCart 클래스는 다음 메서드를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-133">The ShoppingCart class exposes the following methods:</span></span>

<span data-ttu-id="3c41d-134">**AddToCart** 앨범 매개 변수로 사용 하 고 사용자의 장바구니에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-134">**AddToCart** takes an Album as a parameter and adds it to the user's cart.</span></span> <span data-ttu-id="3c41d-135">카트 테이블 각 앨범에 대 한 수량을 추적 하므로 필요한 경우 새 행을 만들 또는 사용자가 이미는 앨범의 복사본이 두 개를 정렬 하는 경우 수량이 증가 하는 논리가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-135">Since the Cart table tracks quantity for each album, it includes logic to create a new row if needed or just increment the quantity if the user has already ordered one copy of the album.</span></span>

<span data-ttu-id="3c41d-136">**RemoveFromCart** 앨범 ID를 사용 하 고 사용자의 카트에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-136">**RemoveFromCart** takes an Album ID and removes it from the user's cart.</span></span> <span data-ttu-id="3c41d-137">사용자는 앨범의 복사본이 두 개 카트에 만으로는, 행이 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-137">If the user only had one copy of the album in their cart, the row is removed.</span></span>

<span data-ttu-id="3c41d-138">**EmptyCart** 사용자의 쇼핑 카트에서 모든 항목을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-138">**EmptyCart** removes all items from a user's shopping cart.</span></span>

<span data-ttu-id="3c41d-139">**GetCartItems** 표시 또는 처리를 위해 CartItems 목록을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-139">**GetCartItems** retrieves a list of CartItems for display or processing.</span></span>

<span data-ttu-id="3c41d-140">**GetCount** 검색 한 앨범을 사용자가 장바구니의 총 수입니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-140">**GetCount** retrieves a the total number of albums a user has in their shopping cart.</span></span>

<span data-ttu-id="3c41d-141">**GetTotal** 바구니에 모든 항목의 총 비용을 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-141">**GetTotal** calculates the total cost of all items in the cart.</span></span>

<span data-ttu-id="3c41d-142">**CreateOrder** 체크 아웃 단계 동안 쇼핑 카트 주문으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-142">**CreateOrder** converts the shopping cart to an order during the checkout phase.</span></span>

<span data-ttu-id="3c41d-143">**GetCart** 카트 개체를 가져오려면 우리의 컨트롤러 수 있는 정적 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-143">**GetCart** is a static method which allows our controllers to obtain a cart object.</span></span> <span data-ttu-id="3c41d-144">사용 하 여는 **GetCartId** 는 CartId 사용자의 세션에서 읽기를 처리 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="3c41d-144">It uses the **GetCartId** method to handle reading the CartId from the user's session.</span></span> <span data-ttu-id="3c41d-145">사용자의 CartId 사용자의 세션에서 읽을 수 있도록 GetCartId 메서드 HttpContextBase를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-145">The GetCartId method requires the HttpContextBase so that it can read the user's CartId from user's session.</span></span>

<span data-ttu-id="3c41d-146">다음 전체은 **ShoppingCart 클래스**:</span><span class="sxs-lookup"><span data-stu-id="3c41d-146">Here's the complete **ShoppingCart class**:</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample5.cs)]

## <a name="viewmodels"></a><span data-ttu-id="3c41d-147">Viewmodel</span><span class="sxs-lookup"><span data-stu-id="3c41d-147">ViewModels</span></span>

<span data-ttu-id="3c41d-148">당사의 쇼핑 카트 컨트롤러는 모델 개체에 완전히 매핑되지 않으면 해당 보기에 복잡 한 일부 정보를 전달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-148">Our Shopping Cart Controller will need to communicate some complex information to its views which doesn't map cleanly to our Model objects.</span></span> <span data-ttu-id="3c41d-149">우리의 뷰만 맞게이 모델을 수정 하지는 않을 모델 클래스는 도메인의 사용자 인터페이스를 나타내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-149">We don't want to modify our Models to suit our views; Model classes should represent our domain, not the user interface.</span></span> <span data-ttu-id="3c41d-150">한 가지 해결 정보를 관리 하기 어려운 가져옵니다 ViewBag을 통해 많은 정보를 전달 하지만 저장소 관리자 드롭다운 정보와 동일한 방식으로 ViewBag 클래스를 사용 하 여이 뷰를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-150">One solution would be to pass the information to our Views using the ViewBag class, as we did with the Store Manager dropdown information, but passing a lot of information via ViewBag gets hard to manage.</span></span>

<span data-ttu-id="3c41d-151">이 해결 방법은 사용 하 여 *ViewModel* 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-151">A solution to this is to use the *ViewModel* pattern.</span></span> <span data-ttu-id="3c41d-152">이 패턴을 사용 하는 경우 강력한 형식의 클래스의 특정 보기 시나리오에 최적화 된 및 우리의 템플릿 보기에 필요한 동적 값/콘텐츠에 대 한 속성을 노출 합니다 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-152">When using this pattern we create strongly-typed classes that are optimized for our specific view scenarios, and which expose properties for the dynamic values/content needed by our view templates.</span></span> <span data-ttu-id="3c41d-153">컨트롤러 클래스 다음 이러한 보기 액세스에 최적화 된 클래스 우리의 뷰 템플릿을 사용 하려면에 전달을 채울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-153">Our controller classes can then populate and pass these view-optimized classes to our view template to use.</span></span> <span data-ttu-id="3c41d-154">이렇게 하면 형식 안전성, 컴파일 타임 검사 및 IntelliSense 템플릿 보기 내에서 편집기.</span><span class="sxs-lookup"><span data-stu-id="3c41d-154">This enables type-safety, compile-time checking, and editor IntelliSense within view templates.</span></span>

<span data-ttu-id="3c41d-155">쇼핑 카트 컨트롤러에서 사용 하기 위해 두 개의 뷰 모델을 만들겠습니다: ShoppingCartViewModel는 사용자의 쇼핑 카트의 내용을 보유 하 고는 ShoppingCartRemoveViewModel에서 사용자 항목을 제거할 때 확인 정보를 표시 하는 데 사용 됩니다 자신의 카트에 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-155">We'll create two View Models for use in our Shopping Cart controller: the ShoppingCartViewModel will hold the contents of the user's shopping cart, and the ShoppingCartRemoveViewModel will be used to display confirmation information when a user removes something from their cart.</span></span>

<span data-ttu-id="3c41d-156">정보 구성 하는 프로젝트의 루트에서 새 Viewmodel 폴더를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-156">Let's create a new ViewModels folder in the root of our project to keep things organized.</span></span> <span data-ttu-id="3c41d-157">프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 추가 선택 합니다 / 새 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-157">Right-click the project, select Add / New Folder.</span></span>

![](mvc-music-store-part-8/_static/image1.jpg)

<span data-ttu-id="3c41d-158">Viewmodel 폴더를 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-158">Name the folder ViewModels.</span></span>

![](mvc-music-store-part-8/_static/image1.png)

<span data-ttu-id="3c41d-159">다음으로 ShoppingCartViewModel 클래스 Viewmodel 폴더에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-159">Next, add the ShoppingCartViewModel class in the ViewModels folder.</span></span> <span data-ttu-id="3c41d-160">다음 두 가지 속성이: 카트 항목과 카트에서 모든 항목에 대 한 총 가격 유지 하기 위해 10 진수 값의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-160">It has two properties: a list of Cart items, and a decimal value to hold the total price for all items in the cart.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample6.cs)]

<span data-ttu-id="3c41d-161">이제 다음 네 가지 속성을 가진 Viewmodel 폴더에는 ShoppingCartRemoveViewModel를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-161">Now add the ShoppingCartRemoveViewModel to the ViewModels folder, with the following four properties.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample7.cs)]

## <a name="the-shopping-cart-controller"></a><span data-ttu-id="3c41d-162">쇼핑 카트 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="3c41d-162">The Shopping Cart Controller</span></span>

<span data-ttu-id="3c41d-163">쇼핑 카트 컨트롤러는 세 가지 주요 목적은:을 카트에 항목을 추가, 항목을 카트에서 제거 및 바구니에 항목을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-163">The Shopping Cart controller has three main purposes: adding items to a cart, removing items from the cart, and viewing items in the cart.</span></span> <span data-ttu-id="3c41d-164">세 개의 클래스에서는 사용 하면 방금 만든: ShoppingCartViewModel, ShoppingCartRemoveViewModel, 및 ShoppingCart 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-164">It will make use of the three classes we just created: ShoppingCartViewModel, ShoppingCartRemoveViewModel, and ShoppingCart.</span></span> <span data-ttu-id="3c41d-165">StoreController 및 StoreManagerController, MusicStoreEntities의 인스턴스를 포함 하는 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-165">As in the StoreController and StoreManagerController, we'll add a field to hold an instance of MusicStoreEntities.</span></span>

<span data-ttu-id="3c41d-166">빈 컨트롤러 템플릿을 사용 하 여 프로젝트에 새 쇼핑 카트 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-166">Add a new Shopping Cart controller to the project using the Empty controller template.</span></span>

![](mvc-music-store-part-8/_static/image2.png)

<span data-ttu-id="3c41d-167">다음은 전체 ShoppingCart 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-167">Here's the complete ShoppingCart Controller.</span></span> <span data-ttu-id="3c41d-168">인덱스 및 컨트롤러 추가 작업 친숙 하 게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-168">The Index and Add Controller actions should look very familiar.</span></span> <span data-ttu-id="3c41d-169">제거 및 CartSummary 컨트롤러 작업에는 다음 섹션에서 설명 하겠지만 두 가지 특별 한 경우 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-169">The Remove and CartSummary controller actions handle two special cases, which we'll discuss in the following section.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample8.cs)]

## <a name="ajax-updates-with-jquery"></a><span data-ttu-id="3c41d-170">JQuery 사용 하 여 Ajax 업데이트</span><span class="sxs-lookup"><span data-stu-id="3c41d-170">Ajax Updates with jQuery</span></span>

<span data-ttu-id="3c41d-171">쇼핑 카트 인덱스 페이지는 ShoppingCartViewModel에 강력한 형식의 하 앞으로 동일한 메서드를 사용 하 여 목록 보기 템플릿을 사용 하 여 다음 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-171">We'll next create a Shopping Cart Index page that is strongly typed to the ShoppingCartViewModel and uses the List View template using the same method as before.</span></span>

![](mvc-music-store-part-8/_static/image3.png)

<span data-ttu-id="3c41d-172">그러나 카트에서 항목을 제거 하는 Html.ActionLink를 사용 하는 대신 사용 합니다 jQuery "를 연결 하" RemoveLink HTML 클래스를 포함 하는이 보기에 있는 모든 연결에 대 한 click 이벤트.</span><span class="sxs-lookup"><span data-stu-id="3c41d-172">However, instead of using an Html.ActionLink to remove items from the cart, we'll use jQuery to "wire up" the click event for all links in this view which have the HTML class RemoveLink.</span></span> <span data-ttu-id="3c41d-173">폼 게시, 대신이 click 이벤트 처리기 설정 됩니다. 바로 AJAX 콜백을에 우리의 RemoveFromCart 컨트롤러 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-173">Rather than posting the form, this click event handler will just make an AJAX callback to our RemoveFromCart controller action.</span></span> <span data-ttu-id="3c41d-174">RemoveFromCart는 JSON으로 직렬화 된 결과 반환 jQuery 콜백이 다음 구문 분석 하 고 jQuery를 사용 하 여 페이지에 대 한 네 가지 빠른 업데이트를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-174">The RemoveFromCart returns a JSON serialized result, which our jQuery callback then parses and performs four quick updates to the page using jQuery:</span></span>

- 1. <span data-ttu-id="3c41d-175">목록에서 삭제 된 앨범을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-175">Removes the deleted album from the list</span></span>
- 2. <span data-ttu-id="3c41d-176">헤더에 카트 개수를 업데이트</span><span class="sxs-lookup"><span data-stu-id="3c41d-176">Updates the cart count in the header</span></span>
- 3. <span data-ttu-id="3c41d-177">사용자에 게 업데이트 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-177">Displays an update message to the user</span></span>
- 4. <span data-ttu-id="3c41d-178">카트 총 가격을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-178">Updates the cart total price</span></span>

<span data-ttu-id="3c41d-179">제거 시나리오는 Ajax 콜백을 인덱스 뷰 내에서 처리 되는, 이후 추가 뷰 RemoveFromCart 동작에 대 한 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-179">Since the remove scenario is being handled by an Ajax callback within the Index view, we don't need an additional view for RemoveFromCart action.</span></span> <span data-ttu-id="3c41d-180">/ShoppingCart/Index 보기에 대 한 전체 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-180">Here is the complete code for the /ShoppingCart/Index view:</span></span>

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample9.cshtml)]

<span data-ttu-id="3c41d-181">Out이 르 테스트 하려면 당사의 쇼핑 카트에 항목을 추가할 수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-181">In order to test this out, we need to be able to add items to our shopping cart.</span></span> <span data-ttu-id="3c41d-182">업데이트 하는 중 우리의 **저장소 세부 정보** "카트에 추가" 단추를 포함 하는 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-182">We'll update our **Store Details** view to include an "Add to cart" button.</span></span> <span data-ttu-id="3c41d-183">추가한 있는 앨범 추가 정보 중 일부 포함 시키려면 현재, 그 동안이 보기에서는 마지막 업데이트 이후: 장르, 아티스트, 가격 및 앨범 아트.</span><span class="sxs-lookup"><span data-stu-id="3c41d-183">While we're at it, we can include some of the Album additional information which we've added since we last updated this view: Genre, Artist, Price, and Album Art.</span></span> <span data-ttu-id="3c41d-184">업데이트 된 코드 저장소 세부 정보 보기에는 다음과 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-184">The updated Store Details view code appears as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample10.cshtml)]

<span data-ttu-id="3c41d-185">이제 스토어를 통해 클릭 하 고 및 추가 / 제거 앨범을 당사의 쇼핑 카트에서 테스트할 수 했습니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-185">Now we can click through the store and test adding and removing Albums to and from our shopping cart.</span></span> <span data-ttu-id="3c41d-186">응용 프로그램을 실행 하 고 저장소 인덱스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-186">Run the application and browse to the Store Index.</span></span>

![](mvc-music-store-part-8/_static/image4.png)

<span data-ttu-id="3c41d-187">다음으로 장르 앨범의 목록을 보려면 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-187">Next, click on a Genre to view a list of albums.</span></span>

![](mvc-music-store-part-8/_static/image5.png)

<span data-ttu-id="3c41d-188">이제 앨범 제목 클릭 하면 "카트에 추가" 단추를 포함 하 여이 업데이트 된 앨범 자세히 보기를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-188">Clicking on an Album title now shows our updated Album Details view, including the "Add to cart" button.</span></span>

![](mvc-music-store-part-8/_static/image6.png)

<span data-ttu-id="3c41d-189">"카트에 추가" 단추를 클릭 하면 쇼핑 카트 요약 목록 함께 당사의 쇼핑 카트 인덱스 뷰가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-189">Clicking the "Add to cart" button shows our Shopping Cart Index view with the shopping cart summary list.</span></span>

![](mvc-music-store-part-8/_static/image7.png)

<span data-ttu-id="3c41d-190">쇼핑 카트에 로드 쇼핑 카트에 Ajax 업데이트 카트 링크에서 제거를 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-190">After loading up your shopping cart, you can click on the Remove from cart link to see the Ajax update to your shopping cart.</span></span>

![](mvc-music-store-part-8/_static/image8.png)

<span data-ttu-id="3c41d-191">쇼핑 카트 등록 되지 않은 사용자가 자신의 카트에 항목을 추가할 수 있는 작업으로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-191">We've built out a working shopping cart which allows unregistered users to add items to their cart.</span></span> <span data-ttu-id="3c41d-192">다음 섹션에 등록 하 고 체크 아웃 프로세스를 완료 하도록 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c41d-192">In the following section, we'll allow them to register and complete the checkout process.</span></span>


>[!div class="step-by-step"]
<span data-ttu-id="3c41d-193">[이전](mvc-music-store-part-7.md)
[다음](mvc-music-store-part-9.md)</span><span class="sxs-lookup"><span data-stu-id="3c41d-193">[Previous](mvc-music-store-part-7.md)
[Next](mvc-music-store-part-9.md)</span></span>
