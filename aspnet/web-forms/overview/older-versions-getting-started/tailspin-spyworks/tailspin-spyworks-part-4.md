---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
title: '4 부: 제품 나열 | Microsoft Docs'
author: JoeStagner
description: 이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다. 4 부에서는 GridView contr. 제품 목록 설명...
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 4fab47d5-a6ec-4fdc-91f0-651a093a24b9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
msc.type: authoredcontent
ms.openlocfilehash: ca7eccd684473d9a1ec4a8adfd8690b291fe702f
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41838851"
---
<a name="part-4-listing-products"></a><span data-ttu-id="ebf04-104">4 부: 제품 나열</span><span class="sxs-lookup"><span data-stu-id="ebf04-104">Part 4: Listing Products</span></span>
====================
<span data-ttu-id="ebf04-105">[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="ebf04-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="ebf04-106">Tailspin Spyworks.NET 플랫폼에 대 한 강력 하 고 확장 가능한 응용 프로그램을 생성 하는 방법을 매우 단순 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="ebf04-107">해제 쇼핑, 체크 아웃 및 관리를 포함 하는 온라인 상점을 만들려고 ASP.NET 4에서 강력한 새 기능을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="ebf04-108">이 자습서 시리즈 모든 Tailspin Spyworks 샘플 응용 프로그램 빌드를 수행 하는 단계를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="ebf04-109">4 부에서는 GridView 컨트롤을 사용 하 여 제품을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-109">Part 4 covers listing products with the GridView control.</span></span>


## <a id="_Toc260221670"></a>  <span data-ttu-id="ebf04-110">GridView 컨트롤을 사용 하 여 제품을 나열</span><span class="sxs-lookup"><span data-stu-id="ebf04-110">Listing Products with the GridView Control</span></span>

<span data-ttu-id="ebf04-111">솔루션 선택 하 고 "Add" 및 "새 항목"에서 "마우스 오른쪽 단추로 클릭" ProductsList.aspx 페이지 구현를 시작 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-111">Let's begin implementing our ProductsList.aspx page by "Right Clicking" on our solution and selecting "Add" and "New Item".</span></span>

![](tailspin-spyworks-part-4/_static/image1.jpg)

<span data-ttu-id="ebf04-112">"웹 폼 마스터 페이지 사용"을 선택 하 고 ProductsList.aspx 페이지 이름을 입력 "입니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-112">Choose "Web Form Using Master Page" and enter a page name of ProductsList.aspx".</span></span>

<span data-ttu-id="ebf04-113">"추가"를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-113">Click "Add".</span></span>

![](tailspin-spyworks-part-4/_static/image2.jpg)

<span data-ttu-id="ebf04-114">다음 Site.Master 페이지에서는 배치할 "스타일" 폴더를 선택 하 고 "폴더의 내용" 창에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-114">Next choose the "Styles" folder where we placed the Site.Master page and select it from the "Contents of folder" window.</span></span>

![](tailspin-spyworks-part-4/_static/image3.jpg)

<span data-ttu-id="ebf04-115">"확인" 페이지를 만들려면 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-115">Click "Ok" to create the page.</span></span>

<span data-ttu-id="ebf04-116">아래와 같이 데이터베이스에 제품 데이터가 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-116">Our database is populated with product data as seen below.</span></span>

![](tailspin-spyworks-part-4/_static/image4.jpg)

<span data-ttu-id="ebf04-117">가격 페이지 만들어진 후 다시 사용 하 여 엔터티 데이터 소스를 해당 제품 데이터에 액세스 하지만 Product 엔터티를 선택 해야이 인스턴스 및 선택한 범주에 대 한 레코드만 반환 되는 항목을 제한 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-117">After our page is created we'll again use an Entity Data Source to access that product data, but in this instance we need to select the Product Entities and we need to restrict the items that are returned to only those for the selected Category.</span></span>

<span data-ttu-id="ebf04-118">이렇게 하려면 자동 생성 EntityDataSource WHERE 절에 대해 알아봅니다 및 WhereParameter를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-118">To accomplish this we'll tell the EntityDataSource to Auto Generate the WHERE clause and we'll specify the WhereParameter.</span></span>

<span data-ttu-id="ebf04-119">이 "제품 범주 메뉴에서 메뉴 항목을 만들었을 때 동적으로 구축한 링크는 CatagoryID 각 링크에 대 한 QueryString을 추가 하 여 설명한 내용을 기억하실 겁니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-119">You'll recall that when we created the Menu Items in our "Product Category Menu" we dynamically built the link by adding the CatagoryID to the QueryString for each link.</span></span> <span data-ttu-id="ebf04-120">위치 매개 변수는 쿼리 문자열 매개 변수에서 파생 엔터티 데이터 소스를 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-120">We will tell the Entity Data Source to derive the WHERE parameter from that QueryString parameter.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample1.aspx)]

<span data-ttu-id="ebf04-121">다음으로 제품 목록을 표시할 ListView 컨트롤을 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-121">Next, we'll configure the ListView control to display a list of products.</span></span> <span data-ttu-id="ebf04-122">우리의 ListVew에 나타나는 각 개별 제품에 몇 가지 간단한 기능을 압축 됩니다에서는 최적의 쇼핑 환경을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-122">To create an optimal shopping experience we'll compact several concise features into each individual product displayed in our ListVew.</span></span>

- <span data-ttu-id="ebf04-123">제품 이름을 제품의 세부 정보 뷰에 대 한 링크 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-123">The product name will be a link to the product's detail view.</span></span>
- <span data-ttu-id="ebf04-124">제품의 가격이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-124">The product's price will be displayed.</span></span>
- <span data-ttu-id="ebf04-125">제품의 이미지가 표시 되 고 응용 프로그램에서 카탈로그 images 디렉터리에서 이미지를 동적으로 선택 됩니다 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-125">An image of the product will be displayed and we'll dynamically select the image from a catalog images directory in our application.</span></span>
- <span data-ttu-id="ebf04-126">즉시 특정 제품을 쇼핑 카트에 추가에 대 한 링크를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-126">We will include a link to immediately add the specific product to the shopping cart.</span></span>

<span data-ttu-id="ebf04-127">ListView 컨트롤 인스턴스에 대 한 태그는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-127">Here is the markup for our ListView control instance.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample2.aspx)]

<span data-ttu-id="ebf04-128">표시 된 각 제품에 대 한 몇 가지 링크에 동적으로 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-128">We are dynamically building several links for each displayed product.</span></span>

<span data-ttu-id="ebf04-129">또한 직접 새 페이지 테스트 전에 해야 카탈로그 이미지 제품에 대 한 디렉터리 구조를 다음과 같이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-129">Also, before we test own new page we need to create the directory structure for the product catalog images as follows.</span></span>

![](tailspin-spyworks-part-4/_static/image1.png)

<span data-ttu-id="ebf04-130">제품 이미지에 액세스할 수 면 당사의 제품 목록 페이지를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-130">Once our product images are accessible we can test our product list page.</span></span>

![](tailspin-spyworks-part-4/_static/image5.jpg)

<span data-ttu-id="ebf04-131">사이트의 홈 페이지에서 범주 목록 링크 중 하나를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-131">From the site's home page, click on one of the Category List Links.</span></span>

![](tailspin-spyworks-part-4/_static/image6.jpg)

<span data-ttu-id="ebf04-132">이제 ProductDetials.apsx 페이지 및 AddToCart 기능을 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-132">Now we need to implement the ProductDetials.apsx page and the AddToCart functionality.</span></span>

<span data-ttu-id="ebf04-133">사용 하 여 파일-&gt;새 페이지 이름을 ProductDetails.aspx 이전에 수행한 것 처럼 사이트 마스터 페이지를 사용 하 여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-133">Use File-&gt;New to create a page name ProductDetails.aspx using the site Master Page as we did previously.</span></span>

<span data-ttu-id="ebf04-134">다시 사용 하 여 EntityDataSource 컨트롤을 데이터베이스에서 특정 제품 레코드에 액세스 하 고 ASP.NET FormView 컨트롤을 사용 하 여 제품 데이터를 다음과 같이 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-134">We will again use an EntityDataSource control to access the specific product record in the database and we will use an ASP.NET FormView control to display the product data as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample3.aspx)]

<span data-ttu-id="ebf04-135">서식 지정을 거 든 보이는 경우 걱정 하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="ebf04-135">Don't worry if the formatting looks a bit funny to you.</span></span> <span data-ttu-id="ebf04-136">위의 태그를 둡니다 표시 레이아웃의 몇 가지 기능이 나중에 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-136">The markup above leaves room in the display layout for a couple of features we'll implement later on.</span></span>

<span data-ttu-id="ebf04-137">쇼핑 카트는 응용 프로그램에서 더 복잡 한 논리를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-137">The Shopping Cart will represent the more complex logic in our application.</span></span> <span data-ttu-id="ebf04-138">시작 하려면 사용 하 여 파일-&gt;MyShoppingCart.aspx 라는 페이지를 만들려면 새로 만들기.</span><span class="sxs-lookup"><span data-stu-id="ebf04-138">To get started, use File-&gt;New to create a page called MyShoppingCart.aspx.</span></span>

<span data-ttu-id="ebf04-139">이름을 ShoppingCart.aspx 선택 하지 않습니다 것을 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-139">Note that we are not choosing the name ShoppingCart.aspx.</span></span>

<span data-ttu-id="ebf04-140">데이터베이스 "ShoppingCart" 라는 테이블을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-140">Our database contains a table named "ShoppingCart".</span></span> <span data-ttu-id="ebf04-141">엔터티 데이터 모델을 생성할 때 데이터베이스의 각 테이블에 대 한 클래스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-141">When we generated an Entity Data Model a class was created for each table in the database.</span></span> <span data-ttu-id="ebf04-142">따라서 엔터티 데이터 모델 "ShoppingCart" 라는 엔터티 클래스가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-142">Therefore, the Entity Data Model generated an Entity Class named "ShoppingCart".</span></span> <span data-ttu-id="ebf04-143">하지만 대신 않고 단순히 충돌을 방지 하는 이름 선택 하려면 쇼핑 카트 구현에 해당 이름을 사용할 수 없습니다 하거나, 요구 사항에 대 한 확장 모델을 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-143">We could edit the model so that we could use that name for our shopping cart implementation or extend it for our needs, but we will opt instead to simply slect a name that will avoid the conflict.</span></span>

<span data-ttu-id="ebf04-144">쇼핑 카트 표시를 사용 하 여 쇼핑 카트 논리를 포함 하는 우리가 만들 간단한 쇼핑 카트 주목할 만한 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-144">It's also worth noting that we will be creating a simple shopping cart and embedding the shopping cart logic with the shopping cart display.</span></span> <span data-ttu-id="ebf04-145">우리는 완전히 별개의 비즈니스 계층에서 당사의 쇼핑 카트를 구현 하는 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebf04-145">We might also choose to implement our shopping cart in a completely separate Business Layer.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ebf04-146">[이전](tailspin-spyworks-part-3.md)
> [다음](tailspin-spyworks-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="ebf04-146">[Previous](tailspin-spyworks-part-3.md)
[Next](tailspin-spyworks-part-5.md)</span></span>
