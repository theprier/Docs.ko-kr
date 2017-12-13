---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
title: "10 단계: 탐색 및 사이트 설계, 결론에 대 한 최종 업데이트 | Microsoft Docs"
author: jongalloway
description: "이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다. 부 10에서는 탐색 및에 대 한 마지막 업데이트를 다룹니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/21/2011
ms.topic: article
ms.assetid: 0c6e4c2f-fcdb-4978-9656-1990c6f15727
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
msc.type: authoredcontent
ms.openlocfilehash: af08039de2d810948b9ab64974111b0346c7fa0f
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="part-10-final-updates-to-navigation-and-site-design-conclusion"></a><span data-ttu-id="6c2de-104">10 단계: 탐색 및 사이트 설계, 결론에 대 한 마지막 업데이트</span><span class="sxs-lookup"><span data-stu-id="6c2de-104">Part 10: Final Updates to Navigation and Site Design, Conclusion</span></span>
====================
<span data-ttu-id="6c2de-105">으로 [Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="6c2de-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="6c2de-106">MVC Music Store는 소개 하 고 웹 개발에 대 한 ASP.NET MVC와 Visual Studio를 사용 하는 방법을 단계별로 설명 하는 자습서 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="6c2de-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="6c2de-107">MVC Music Store는 온라인 음악 앨범 판매 및 기본 사이트 관리, 사용자 로그인 및 장바구니 기능을 구현 하는 간단한 샘플 저장소 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="6c2de-108">이 자습서 시리즈 모든 ASP.NET MVC Music Store 샘플 응용 프로그램을 작성 하는 데 필요한 단계를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="6c2de-109">10 탐색 및 사이트 설계, 결론에 대 한 마지막 업데이트를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-109">Part 10 covers Final Updates to Navigation and Site Design, Conclusion.</span></span>


<span data-ttu-id="6c2de-110">이 사이트에 대 한 모든 주요 기능을 완료 한 것 하지만 아직 몇 가지 기능이 사이트 탐색, 홈 페이지 및 저장소 찾아보기 페이지에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-110">We've completed all the major functionality for our site, but we still have some features to add to the site navigation, the home page, and the Store Browse page.</span></span>

## <a name="creating-the-shopping-cart-summary-partial-view"></a><span data-ttu-id="6c2de-111">쇼핑 카트 요약 부분 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="6c2de-111">Creating the Shopping Cart Summary Partial View</span></span>

<span data-ttu-id="6c2de-112">전체 사이트 사용자의 쇼핑 카트에 항목 수를 표시 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-112">We want to expose the number of items in the user's shopping cart across the entire site.</span></span>

![](mvc-music-store-part-10/_static/image1.png)

<span data-ttu-id="6c2de-113">우리의 Site.master에 추가 된 부분 뷰를 만들어 쉽게 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-113">We can easily implement this by creating a partial view which is added to our Site.master.</span></span>

<span data-ttu-id="6c2de-114">이전에 표시 된 것 처럼 ShoppingCart 컨트롤러 부분 뷰를 반환 하는 CartSummary 작업 메서드에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-114">As shown previously, the ShoppingCart controller includes a CartSummary action method which returns a partial view:</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample1.cs)]

<span data-ttu-id="6c2de-115">CartSummary 부분 뷰를 만들려면 뷰/ShoppingCart 폴더를 마우스 오른쪽 단추로 클릭 하 고 추가 보기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-115">To create the CartSummary partial view, right-click on the Views/ShoppingCart folder and select Add View.</span></span> <span data-ttu-id="6c2de-116">CartSummary 뷰 이름을 지정 하 고 아래와 같이 "부분 뷰 만들기" 확인란을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-116">Name the view CartSummary and check the "Create a partial view" checkbox as shown below.</span></span>

![](mvc-music-store-part-10/_static/image2.png)

<span data-ttu-id="6c2de-117">CartSummary 부분 뷰는 매우 간단-바구니에 항목의 수를 보여 주는 ShoppingCart 인덱스 뷰를 링크 일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-117">The CartSummary partial view is really simple - it's just a link to the ShoppingCart Index view which shows the number of items in the cart.</span></span> <span data-ttu-id="6c2de-118">CartSummary.cshtml에 대 한 전체 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-118">The complete code for CartSummary.cshtml is as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample2.cshtml)]

<span data-ttu-id="6c2de-119">부분 뷰 Html.RenderAction 메서드를 사용 하 여 사이트 마스터를 비롯 하 여 사이트의 모든 페이지에 포함 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-119">We can include a partial view in any page in the site, including the Site master, by using the Html.RenderAction method.</span></span> <span data-ttu-id="6c2de-120">RenderAction 아래으로 ("ShoppingCart") 컨트롤러 이름 및 작업 이름 ("CartSummary")을 지정할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-120">RenderAction requires us to specify the Action Name ("CartSummary") and the Controller Name ("ShoppingCart") as below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample3.cshtml)]

<span data-ttu-id="6c2de-121">이 레이아웃 사이트에 추가 하기 전에 만듭니다 장르 메뉴 우리의 Site.master 업데이트를 모두 한 번에 내릴 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-121">Before adding this to the site Layout, we will also create the Genre Menu so we can make all of our Site.master updates at one time.</span></span>

## <a name="creating-the-genre-menu-partial-view"></a><span data-ttu-id="6c2de-122">Genre 메뉴 부분 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="6c2de-122">Creating the Genre Menu Partial View</span></span>

<span data-ttu-id="6c2de-123">시나리오에서는 사용자가 스토어에서 사용할 수 있는 모든 장르를 나열 하는 장르 메뉴를 추가 하 여 스토어를 통해 이동에 대 한 훨씬 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-123">We can make it a lot easier for our users to navigate through the store by adding a Genre Menu which lists all the Genres available in our store.</span></span>

![](mvc-music-store-part-10/_static/image3.png)

<span data-ttu-id="6c2de-124">동일한 따르 단계 GenreMenu 부분 뷰를 만들 수도 및 다음을 추가할 수 있습니다를 모두 사이트 마스터 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-124">We will follow the same steps also create a GenreMenu partial view, and then we can add them both to the Site master.</span></span> <span data-ttu-id="6c2de-125">첫째,는 StoreController를 다음 GenreMenu 컨트롤러 동작을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-125">First, add the following GenreMenu controller action to the StoreController:</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample4.cs)]

<span data-ttu-id="6c2de-126">이 작업 장르 다음 만들어집니다 여 부분 뷰를 표시 하는 목록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-126">This action returns a list of Genres which will be displayed by the partial view, which we will create next.</span></span>

<span data-ttu-id="6c2de-127">*참고: 한다는이 작업 부분 뷰에서 사용할 수 있는이 컨트롤러 작업을 [ChildActionOnly] 특성을 추가 했습니다. 이 특성에는 컨트롤러 동작 /Store/GenreMenu로 이동 하 여 실행 되지 않도록 수 없게 됩니다. 부분 뷰 필요 하지 않습니다 이지만 것이 좋습니다 우리의 컨트롤러 작업은 원래의 의도 대로 사용 되도록 하는 데 있습니다. 에서는 또한 반환 하는 경우는 뷰 엔진이 다른 보기에 포함 되는이 보기에 대 한 레이아웃을 사용해 서는 안 것을 알 수 있도록 뷰가 아닌 PartialView 합니다.*</span><span class="sxs-lookup"><span data-stu-id="6c2de-127">*Note: We have added the [ChildActionOnly] attribute to this controller action, which indicates that we only want this action to be used from a Partial View. This attribute will prevent the controller action from being executed by browsing to /Store/GenreMenu. This isn't required for partial views, but it is a good practice, since we want to make sure our controller actions are used as we intend. We are also returning PartialView rather than View, which lets the view engine know that it shouldn't use the Layout for this view, as it is being included in other views.*</span></span>

<span data-ttu-id="6c2de-128">GenreMenu 컨트롤러 작업 단추로 클릭 하 고 아래와 같이 데이터 클래스는 장르 보기를 사용 하 여 강력 하 게 형식화 된 GenreMenu 라는 부분 뷰를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-128">Right-click on the GenreMenu controller action and create a partial view named GenreMenu which is strongly typed using the Genre view data class as shown below.</span></span>

![](mvc-music-store-part-10/_static/image4.png)

<span data-ttu-id="6c2de-129">다음과 같이 정렬 되지 않은 목록을 사용 하 여 항목을 표시 하려면 GenreMenu 부분 뷰에 대 한 코드 보기를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-129">Update the view code for the GenreMenu partial view to display the items using an unordered list as follows.</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample5.cshtml)]

## <a name="updating-site-layout-to-display-our-partial-views"></a><span data-ttu-id="6c2de-130">사이트 우리의 부분 뷰를 표시 하는 레이아웃 업데이트</span><span class="sxs-lookup"><span data-stu-id="6c2de-130">Updating Site Layout to display our Partial Views</span></span>

<span data-ttu-id="6c2de-131">부분 뷰는 사이트 레이아웃에 추가할 수 있습니다 (/ / Shared/뷰에\_Layout.cshtml) Html.RenderAction()를 호출 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-131">We can add our partial views to the Site Layout (/Views/Shared/\_Layout.cshtml) by calling Html.RenderAction().</span></span> <span data-ttu-id="6c2de-132">아래와 같이 몇 가지 추가 태그를 표시할 수 뿐만 아니라 둘을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-132">We'll add them both in, as well as some additional markup to display them, as shown below:</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample6.cshtml)]

<span data-ttu-id="6c2de-133">이제 응용 프로그램을 실행 하면 왼쪽된 탐색 영역에서 장르와 맨 위에 있는 장바구니 요약 표시 됩니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-133">Now when we run the application, we will see the Genre in the left navigation area and the Cart Summary at the top.</span></span>

## <a name="update-to-the-store-browse-page"></a><span data-ttu-id="6c2de-134">저장소 찾아보기 페이지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-134">Update to the Store Browse page</span></span>

<span data-ttu-id="6c2de-135">저장소 찾아보기 페이지 작동 하지만 매우 양호 보이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-135">The Store Browse page is functional, but doesn't look very good.</span></span> <span data-ttu-id="6c2de-136">코드 보기 (/Views/Store/Browse.cshtml에 있음) 다음과 같이 업데이트 하 여 더 나은 레이아웃 앨범 표시 하려면 페이지를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-136">We can update the page to show the albums in a better layout by updating the view code (found in /Views/Store/Browse.cshtml) as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample7.cshtml)]

<span data-ttu-id="6c2de-137">만들어져 여기 사용 Html.ActionLink 것이 아니라 Url.Action 앨범 아트 워크를 포함 하려면 링크에 특수 한 서식을 적용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-137">Here we are making use of Url.Action rather than Html.ActionLink so that we can apply special formatting to the link to include the album artwork.</span></span>

<span data-ttu-id="6c2de-138">*참고: 이러한 앨범에 대 한 일반 앨범 표지를 표시 됩니다. 이 정보는 데이터베이스에 저장 되며 저장소 관리자를 통해 편집할 수 있습니다. 사용자 고유의 아트 워크를 추가 하려면 시작 됩니다.*</span><span class="sxs-lookup"><span data-stu-id="6c2de-138">*Note: We are displaying a generic album cover for these albums. This information is stored in the database and is editable via the Store Manager. You are welcome to add your own artwork.*</span></span>

<span data-ttu-id="6c2de-139">이제는 장르를 찾아, 우리 앨범 아트 워크가 있는 표에 표시 된 앨범 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-139">Now when we browse to a Genre, we will see the albums shown in a grid with the album artwork.</span></span>

![](mvc-music-store-part-10/_static/image5.png)

## <a name="updating-the-home-page-to-show-top-selling-albums"></a><span data-ttu-id="6c2de-140">홈 페이지 위쪽 판매 앨범 표시 하도록 업데이트</span><span class="sxs-lookup"><span data-stu-id="6c2de-140">Updating the Home Page to show Top Selling Albums</span></span>

<span data-ttu-id="6c2de-141">이 가장 많이 판매 되 앨범 판매를 증진 홈 페이지에서 기능 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-141">We want to feature our top selling albums on the home page to increase sales.</span></span> <span data-ttu-id="6c2de-142">처리 하는, 고도 몇 가지 추가 그래픽에 추가할 우리의 HomeController에 일부 업데이트 만들면 되 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-142">We'll make some updates to our HomeController to handle that, and add in some additional graphics as well.</span></span>

<span data-ttu-id="6c2de-143">첫째, EntityFramework 연결 된 것을 알 수 있도록 탐색 속성 앨범 클래스를 추가 합니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-143">First, we'll add a navigation property to our Album class so that EntityFramework knows that they're associated.</span></span> <span data-ttu-id="6c2de-144">마지막 몇 줄의 우리의 **앨범** 클래스는 이제 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-144">The last few lines of our **Album** class should now look like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample8.cs)]

<span data-ttu-id="6c2de-145">*참고: 여기에 필요 합니다를 사용 하 여 추가 System.Collections.Generic 네임 스페이스에는 문입니다.*</span><span class="sxs-lookup"><span data-stu-id="6c2de-145">*Note: This will require adding a using statement to bring in the System.Collections.Generic namespace.*</span></span>

<span data-ttu-id="6c2de-146">첫째, storeDB 필드와는 다른 컨트롤러에서와 같이 문을 사용 하 여 MvcMusicStore.Models 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-146">First, we'll add a storeDB field and the MvcMusicStore.Models using statements, as in our other controllers.</span></span> <span data-ttu-id="6c2de-147">다음으로, OrderDetails에 따라 상위 판매 앨범을 찾으려고 데이터베이스를 쿼리 하는 HomeController를 다음 메서드를 추가 합니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-147">Next, we'll add the following method to the HomeController which queries our database to find top selling albums according to OrderDetails.</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample9.cs)]

<span data-ttu-id="6c2de-148">이것이 전용 메서드를 컨트롤러 작업으로 사용할 수 있도록 않도록 하기입니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-148">This is a private method, since we don't want to make it available as a controller action.</span></span> <span data-ttu-id="6c2de-149">간단한 설명을 위해 HomeController에 포함 하는 것 이지만 적절 하 게 별도 서비스 클래스에 비즈니스 논리를 이동 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-149">We are including it in the HomeController for simplicity, but you are encouraged to move your business logic into separate service classes as appropriate.</span></span>

<span data-ttu-id="6c2de-150">원위치에서에, 앨범 판매 된 상위 5 쿼리하고 보기로 돌려보낼 인덱스 컨트롤러 작업을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-150">With that in place, we can update the Index controller action to query the top 5 selling albums and return them to the view.</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample10.cs)]

<span data-ttu-id="6c2de-151">HomeController 업데이트에 대 한 전체 코드는 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-151">The complete code for the updated HomeController is as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample11.cs)]

<span data-ttu-id="6c2de-152">마지막으로 모델 유형 업데이트 및 앨범 목록 맨 아래에 추가 하 여 앨범 목록이 표시할 수 있습니다 우리의 홈 인덱스 뷰를 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-152">Finally, we'll need to update our Home Index view so that it can display a list of albums by updating the Model type and adding the album list to the bottom.</span></span> <span data-ttu-id="6c2de-153">또한 페이지 머리글과 프로 모션 섹션을 추가 하려면이 기회 해당 메뉴로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-153">We will take this opportunity to also add a heading and a promotion section to the page.</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample12.cshtml)]

<span data-ttu-id="6c2de-154">이제 응용 프로그램을 실행 했습니다에서는 최상위 판매 앨범 판촉 메시지와 업데이트 된 홈 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-154">Now when we run the application, we'll see our updated home page with top selling albums and our promotional message.</span></span>

![](mvc-music-store-part-10/_static/image1.jpg)

## <a name="conclusion"></a><span data-ttu-id="6c2de-155">결론</span><span class="sxs-lookup"><span data-stu-id="6c2de-155">Conclusion</span></span>

<span data-ttu-id="6c2de-156">ASP.NET MVC를 사용 하면 쉽게 버퍼 오버런 등의 데이터베이스 액세스 권한이 있으면 멤버 자격, AJAX 정교한 웹 사이트를 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-156">We've seen that that ASP.NET MVC makes it easy to create a sophisticated website with database access, membership, AJAX, etc.</span></span> <span data-ttu-id="6c2de-157">매우 신속 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c2de-157">pretty quickly.</span></span> <span data-ttu-id="6c2de-158">다행히이 자습서가 제공한 사용자 고유의 ASP.NET MVC 응용 프로그램을 구축 하는 데 필요한 도구!</span><span class="sxs-lookup"><span data-stu-id="6c2de-158">Hopefully this tutorial has given you the tools you need to get started building your own ASP.NET MVC applications!</span></span>


>[!div class="step-by-step"]
[<span data-ttu-id="6c2de-159">이전</span><span class="sxs-lookup"><span data-stu-id="6c2de-159">Previous</span></span>](mvc-music-store-part-9.md)
