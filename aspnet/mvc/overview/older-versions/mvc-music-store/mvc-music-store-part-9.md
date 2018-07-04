---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
title: '9 단계: 등록 및 체크 아웃 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 9 부에서는 등록 및 체크 아웃에 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/21/2011
ms.topic: article
ms.assetid: d65c5c2b-a039-463f-ad29-25cf9fb7a1ba
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
msc.type: authoredcontent
ms.openlocfilehash: 935729be0dce790c6fce2e2e982ee063318d64dd
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37367012"
---
<a name="part-9-registration-and-checkout"></a><span data-ttu-id="b162c-104">9 단계: 등록 및 체크 아웃</span><span class="sxs-lookup"><span data-stu-id="b162c-104">Part 9: Registration and Checkout</span></span>
====================
<span data-ttu-id="b162c-105">[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="b162c-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="b162c-106">MVC Music Store 자습서 응용 프로그램을 소개 하 고 웹 개발을 위한 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 설명 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="b162c-107">MVC Music Store는 온라인 음악 앨범을 판매 하 고 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="b162c-108">이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="b162c-109">9 부에서는 등록 및 체크 아웃에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-109">Part 9 covers Registration and Checkout.</span></span>


<span data-ttu-id="b162c-110">이 섹션에서는 만들 것을 CheckoutController 구매자의 주소 및 결제 정보를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-110">In this section, we will be creating a CheckoutController which will collect the shopper's address and payment information.</span></span> <span data-ttu-id="b162c-111">에서는 사용자가이 컨트롤러는 권한 부여가 필요 하므로, 체크 인하기 전에 먼저 사이트를 사용 하 여 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-111">We will require users to register with our site prior to checking out, so this controller will require authorization.</span></span>

<span data-ttu-id="b162c-112">사용자는 "체크 아웃" 단추를 클릭 하 여 시장 바구니에서 체크 아웃 프로세스에 이동 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-112">Users will navigate to the checkout process from their shopping cart by clicking the "Checkout" button.</span></span>

![](mvc-music-store-part-9/_static/image1.jpg)

<span data-ttu-id="b162c-113">사용자가 로그인 하지 않았습니다가 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-113">If the user is not logged in, they will be prompted to.</span></span>

![](mvc-music-store-part-9/_static/image1.png)

<span data-ttu-id="b162c-114">로그인에 성공 하면 사용자 후 주소 및 결제 보기에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-114">Upon successful login, the user is then shown the Address and Payment view.</span></span>

![](mvc-music-store-part-9/_static/image2.png)

<span data-ttu-id="b162c-115">폼 입력 있고 주문 제출, 되 면 주문 확인 화면이 표시 되며 합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-115">Once they have filled the form and submitted the order, they will be shown the order confirmation screen.</span></span>

![](mvc-music-store-part-9/_static/image3.png)

<span data-ttu-id="b162c-116">존재 하지 않는 순서 또는 주문 수에 속하지 않는 보려고 하면 오류 보기가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-116">Attempting to view either a non-existent order or an order that doesn't belong to you will show the Error view.</span></span>

![](mvc-music-store-part-9/_static/image4.png)

## <a name="migrating-the-shopping-cart"></a><span data-ttu-id="b162c-117">장바구니 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="b162c-117">Migrating the Shopping Cart</span></span>

<span data-ttu-id="b162c-118">사용자가 체크 아웃 단추를 클릭할 때 익명으로 쇼핑 프로세스 중일 해야 등록 및 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-118">While the shopping process is anonymous, when the user clicks on the Checkout button, they will be required to register and login.</span></span> <span data-ttu-id="b162c-119">사용자가 해당 쇼핑 카드 정보가 방문할: 등록 또는 로그인을 완료 될 때 사용자를 사용 하 여 쇼핑 카드 정보가 연결 해야 하므로 유지는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-119">Users will expect that we will maintain their shopping cart information between visits, so we will need to associate the shopping cart information with a user when they complete registration or login.</span></span>

<span data-ttu-id="b162c-120">이 ShoppingCart 클래스에는 이미 사용자 이름으로 현재 장바구니에 있는 모든 항목을 연결 하는 하는 방법을 실제로 매우 간단 하 게 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-120">This is actually very simple to do, as our ShoppingCart class already has a method which will associate all the items in the current cart with a username.</span></span> <span data-ttu-id="b162c-121">방금 등록 또는 로그인 사용자 완료 되 면이 메서드를 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-121">We will just need to call this method when a user completes registration or login.</span></span>

<span data-ttu-id="b162c-122">엽니다는 **AccountController** 클래스에서는 멤버 자격 및 권한 부여 설정 된 경우 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-122">Open the **AccountController** class that we added when we were setting up Membership and Authorization.</span></span> <span data-ttu-id="b162c-123">추가 된 다음 MigrateShoppingCart 메서드를 추가한 MvcMusicStore.Models를 참조 하는 문을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="b162c-123">Add a using statement referencing MvcMusicStore.Models, then add the following MigrateShoppingCart method:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample1.cs)]

<span data-ttu-id="b162c-124">다음으로 아래와 같이 사용자를 확인 한 후 MigrateShoppingCart를 호출 하는 로그온 후 작업을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-124">Next, modify the LogOn post action to call MigrateShoppingCart after the user has been validated, as shown below:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample2.cs)]

<span data-ttu-id="b162c-125">동일 하 게 변경 등록 후 사용자 계정을 성공적으로 만든 후에 즉시 작업을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-125">Make the same change to the Register post action, immediately after the user account is successfully created:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample3.cs)]

<span data-ttu-id="b162c-126">이것이-이제 성공적인 등록 또는 로그인 시 사용자 계정에는 익명 쇼핑 카트를 자동으로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-126">That's it - now an anonymous shopping cart will be automatically transferred to a user account upon successful registration or login.</span></span>

## <a name="creating-the-checkoutcontroller"></a><span data-ttu-id="b162c-127">CheckoutController 만들기</span><span class="sxs-lookup"><span data-stu-id="b162c-127">Creating the CheckoutController</span></span>

<span data-ttu-id="b162c-128">Controllers 폴더에서 마우스 CheckoutController 빈 컨트롤러 템플릿을 사용 하 여 프로젝트에 새 컨트롤러를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-128">Right-click on the Controllers folder and add a new Controller to the project named CheckoutController using the Empty controller template.</span></span>

![](mvc-music-store-part-9/_static/image5.png)

<span data-ttu-id="b162c-129">먼저, 사용자가 체크 아웃 하기 전에 등록 해야 컨트롤러 클래스 선언 위에 Authorize 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-129">First, add the Authorize attribute above the Controller class declaration to require users to register before checkout:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample4.cs)]

<span data-ttu-id="b162c-130">*참고:이 변경에서는 이전에 StoreManagerController 비슷합니다 있지만 Authorize 특성의 관리자 역할에서 사용자는 필요한 경우. 체크 아웃 컨트롤러에서에서는 요구는 사용자가 로그인 하지만 관리자가 되도록 요구 되지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="b162c-130">*Note: This is similar to the change we previously made to the StoreManagerController, but in that case the Authorize attribute required that the user be in an Administrator role. In the Checkout Controller, we're requiring the user be logged in but aren't requiring that they be administrators.*</span></span>

<span data-ttu-id="b162c-131">편의상이 자습서의 결제 정보를 사용 하 여 처리에서는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-131">For the sake of simplicity, we won't be dealing with payment information in this tutorial.</span></span> <span data-ttu-id="b162c-132">대신, 프로 모션 코드를 사용 하 여 확인 하는 작업을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-132">Instead, we are allowing users to check out using a promotional code.</span></span> <span data-ttu-id="b162c-133">이 프로 모션 코드 PromoCode를 명명 된 상수를 사용 하 여 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-133">We will store this promotional code using a constant named PromoCode.</span></span>

<span data-ttu-id="b162c-134">StoreController에서와 같이 storeDB 라는 MusicStoreEntities 클래스의 인스턴스를 보관할 필드를 선언 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-134">As in the StoreController, we'll declare a field to hold an instance of the MusicStoreEntities class, named storeDB.</span></span> <span data-ttu-id="b162c-135">있도록 MusicStoreEntities 클래스의 사용, 추가 하 여 해야 MvcMusicStore.Models 네임 스페이스에 대 한 문입니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-135">In order to make use of the MusicStoreEntities class, we will need to add a using statement for the MvcMusicStore.Models namespace.</span></span> <span data-ttu-id="b162c-136">체크 아웃 컨트롤러의 맨 아래에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-136">The top of our Checkout controller appears below.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample5.cs)]

<span data-ttu-id="b162c-137">CheckoutController 다음 컨트롤러 작업을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-137">The CheckoutController will have the following controller actions:</span></span>

<span data-ttu-id="b162c-138">**(GET 메서드) AddressAndPayment** 해당 정보를 입력할 수 있도록 폼에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-138">**AddressAndPayment (GET method)** will display a form to allow the user to enter their information.</span></span>

<span data-ttu-id="b162c-139">**(POST 메서드) AddressAndPayment** 입력의 유효성을 검사 하 고 주문을 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-139">**AddressAndPayment (POST method)** will validate the input and process the order.</span></span>

<span data-ttu-id="b162c-140">**전체** 사용자 체크 아웃 프로세스를 완료 한 후 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-140">**Complete** will be shown after a user has successfully finished the checkout process.</span></span> <span data-ttu-id="b162c-141">이 보기는 사용자의 주문 번호를 확인으로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-141">This view will include the user's order number, as confirmation.</span></span>

<span data-ttu-id="b162c-142">먼저 AddressAndPayment 위해 (하는 컨트롤러를 만들 때 생성 된) 인덱스 컨트롤러 작업의 이름을 합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-142">First, let's rename the Index controller action (which was generated when we created the controller) to AddressAndPayment.</span></span> <span data-ttu-id="b162c-143">이 컨트롤러 작업 모델 정보 필요 하지 않도록 체크 아웃 폼만을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-143">This controller action just displays the checkout form, so it doesn't require any model information.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample6.cs)]

<span data-ttu-id="b162c-144">우리의 AddressAndPayment POST 메서드는 StoreManagerController에서 사용한 동일한 패턴을 따릅니다: 폼 제출을 수락 하 고 순서를 완료 하려고 하며 실패할 경우 폼을 다시 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-144">Our AddressAndPayment POST method will follow the same pattern we used in the StoreManagerController: it will try to accept the form submission and complete the order, and will re-display the form if it fails.</span></span>

<span data-ttu-id="b162c-145">폼 입력 유효성 검사는 주문에 대 한이 유효성 검사 요구 사항을 충족 한 후 직접 PromoCode 형식 값을 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-145">After validating the form input meets our validation requirements for an Order, we will check the PromoCode form value directly.</span></span> <span data-ttu-id="b162c-146">주문 프로세스를 완료 하 고 작업 완료를 리디렉션할 하도록 ShoppingCart 개체에 알리는 가정 하 고 모든 항목이 올바르면는 순서를 사용 하 여 업데이트 된 정보를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-146">Assuming everything is correct, we will save the updated information with the order, tell the ShoppingCart object to complete the order process, and redirect to the Complete action.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample7.cs)]

<span data-ttu-id="b162c-147">체크 아웃 프로세스를 성공적으로 완료 하면 사용자가 전체 컨트롤러 작업으로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-147">Upon successful completion of the checkout process, users will be redirected to the Complete controller action.</span></span> <span data-ttu-id="b162c-148">이 작업 순서는 실제로 속한 로그인 한 사용자 확인으로 주문 번호를 표시 하기 전에 유효성을 검사 하려면 간단한 검사를 수행 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-148">This action will perform a simple check to validate that the order does indeed belong to the logged-in user before showing the order number as a confirmation.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample8.cs)]

<span data-ttu-id="b162c-149">*참고: 오류 보기에 자동으로 만들어진 우리 /Views/Shared 폴더에 프로젝트를 시작할 때입니다.*</span><span class="sxs-lookup"><span data-stu-id="b162c-149">*Note: The Error view was automatically created for us in the /Views/Shared folder when we began the project.*</span></span>

<span data-ttu-id="b162c-150">전체 CheckoutController 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-150">The complete CheckoutController code is as follows:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample9.cs)]

## <a name="adding-the-addressandpayment-view"></a><span data-ttu-id="b162c-151">AddressAndPayment 뷰 추가</span><span class="sxs-lookup"><span data-stu-id="b162c-151">Adding the AddressAndPayment view</span></span>

<span data-ttu-id="b162c-152">이제 AddressAndPayment 보기를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-152">Now, let's create the AddressAndPayment view.</span></span> <span data-ttu-id="b162c-153">AddressAndPayment 컨트롤러 작업 중 하나를 마우스 오른쪽 단추로 클릭 하 고 아래와 같이 AddressAndPayment 주문으로 강력한 형식 이므로 편집 템플릿을 사용 하는 명명 된 뷰를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-153">Right-click on one of the AddressAndPayment controller actions and add a view named AddressAndPayment which is strongly typed as an Order and uses the Edit template, as shown below.</span></span>

![](mvc-music-store-part-9/_static/image6.png)

<span data-ttu-id="b162c-154">이 보기 하 게 StoreManagerEdit 보기를 빌드하는 동안 살펴보았습니다 기술 중 두 개를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-154">This view will make use of two of the techniques we looked at while building the StoreManagerEdit view:</span></span>

- <span data-ttu-id="b162c-155">Html.EditorForModel() 순서 모델에 대 한 양식 필드를 표시 하는 데 사용 하는</span><span class="sxs-lookup"><span data-stu-id="b162c-155">We will use Html.EditorForModel() to display form fields for the Order model</span></span>
- <span data-ttu-id="b162c-156">유효성 검사 규칙을 Order 클래스를 사용 하 여 유효성 검사 특성을 사용 하 여 활용 하 게</span><span class="sxs-lookup"><span data-stu-id="b162c-156">We will leverage validation rules using an Order class with validation attributes</span></span>

<span data-ttu-id="b162c-157">Html.EditorForModel(), 프로 모션 코드는 추가 텍스트 상자를 차례로 사용 하 여 폼 코드를 업데이트 하 여 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-157">We'll start by updating the form code to use Html.EditorForModel(), followed by an additional textbox for the Promo Code.</span></span> <span data-ttu-id="b162c-158">AddressAndPayment 뷰에 대 한 전체 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-158">The complete code for the AddressAndPayment view is shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample10.cshtml)]

## <a name="defining-validation-rules-for-the-order"></a><span data-ttu-id="b162c-159">순서에 대 한 유효성 검사 규칙을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-159">Defining validation rules for the Order</span></span>

<span data-ttu-id="b162c-160">보기를 설정 했으므로에서는 설정 유효성 검사 규칙 순서 모델에 대 한 앨범 모델에 대 한 이전에 수행한 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-160">Now that our view is set up, we will set up the validation rules for our Order model as we did previously for the Album model.</span></span> <span data-ttu-id="b162c-161">Models 폴더에서 마우스 오른쪽 순서 라는 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-161">Right-click on the Models folder and add a class named Order.</span></span> <span data-ttu-id="b162c-162">유효성 검사 특성, 앨범에 대 한 이전에 사용 되는 것 외에 사용 합니다 정규식을 사용자의 전자 메일 주소의 유효성을 검사 하려면.</span><span class="sxs-lookup"><span data-stu-id="b162c-162">In addition to the validation attributes we used previously for the Album, we will also be using a Regular Expression to validate the user's email address.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample11.cs)]

<span data-ttu-id="b162c-163">누락 된 양식을 제출 하거나 잘못 된 정보는 이제 클라이언트 쪽 유효성 검사를 사용 하 여 오류 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-163">Attempting to submit the form with missing or invalid information will now show error message using client-side validation.</span></span>

![](mvc-music-store-part-9/_static/image7.png)

<span data-ttu-id="b162c-164">이제 대부분의 복잡 한 작업이 체크 아웃 프로세스를 수행한 방금 완료 하려면 몇 가지 홀수 and 종료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-164">Okay, we've done most of the hard work for the checkout process; we just have a few odds and ends to finish.</span></span> <span data-ttu-id="b162c-165">두 개의 간단한 뷰를 추가 해야 하 고 로그인 프로세스 중 카트 정보의 핸드 오프 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-165">We need to add two simple views, and we need to take care of the handoff of the cart information during the login process.</span></span>

## <a name="adding-the-checkout-complete-view"></a><span data-ttu-id="b162c-166">체크 아웃 전체 뷰를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-166">Adding the Checkout Complete view</span></span>

<span data-ttu-id="b162c-167">체크 아웃 전체 뷰는 id입니다. 순서를 표시 해야 하는 대로 꽤 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-167">The Checkout Complete view is pretty simple, as it just needs to display the Order ID.</span></span> <span data-ttu-id="b162c-168">전체 컨트롤러 작업 단추로 클릭 하 고 강력한 int 형식으로 형식화 된 완료 라는 뷰를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-168">Right-click on the Complete controller action and add a view named Complete which is strongly typed as an int.</span></span>

![](mvc-music-store-part-9/_static/image8.png)

<span data-ttu-id="b162c-169">이제 아래와 같이 주문 ID를 표시 하는 보기 코드를 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-169">Now we will update the view code to display the Order ID, as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample12.cshtml)]

## <a name="updating-the-error-view"></a><span data-ttu-id="b162c-170">업데이트는 오류 보기</span><span class="sxs-lookup"><span data-stu-id="b162c-170">Updating The Error view</span></span>

<span data-ttu-id="b162c-171">기본 템플릿은 될 수 있도록 다시 사용 되는 다른 곳에서 사이트에 공유 views 폴더에는 오류 보기를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-171">The default template includes an Error view in the Shared views folder so that it can be re-used elsewhere in the site.</span></span> <span data-ttu-id="b162c-172">이 오류 뷰는 매우 간단한 오류를 포함 하 고 업데이트 하 고 있으므로 사이트 레이아웃을 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-172">This Error view contains a very simple error and doesn't use our site Layout, so we'll update it.</span></span>

<span data-ttu-id="b162c-173">일반 오류 페이지 이므로, 콘텐츠를 매우 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-173">Since this is a generic error page, the content is very simple.</span></span> <span data-ttu-id="b162c-174">사용자가 해당 작업을 다시 시도 하려는 경우에 기록의 이전 페이지를 이동할 수는 메시지 및 링크 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b162c-174">We'll include a message and a link to navigate to the previous page in history if the user wants to re-try their action.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample13.cshtml)]


> [!div class="step-by-step"]
> <span data-ttu-id="b162c-175">[이전](mvc-music-store-part-8.md)
> [다음](mvc-music-store-part-10.md)</span><span class="sxs-lookup"><span data-stu-id="b162c-175">[Previous](mvc-music-store-part-8.md)
[Next](mvc-music-store-part-10.md)</span></span>
