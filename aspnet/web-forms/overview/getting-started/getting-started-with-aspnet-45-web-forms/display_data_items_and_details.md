---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
title: 데이터 표시 항목 및 세부 정보 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈는 웹을 위한 ASP.NET 4.7 및 Microsoft Visual Studio Community 2017을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항 설명
ms.author: riande
ms.date: 1/09/2019
ms.assetid: 64a491a8-0ed6-4c2f-9c1c-412962eb6006
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
msc.type: authoredcontent
ms.openlocfilehash: 73ae1660f5d6e3e28c1c155e745a62936e3502df
ms.sourcegitcommit: cec77d5ad8a0cedb1ecbec32834111492afd0cd2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/10/2019
ms.locfileid: "54207436"
---
<a name="display-data-items-and-details"></a><span data-ttu-id="a0cd4-103">데이터 항목 및 세부 정보</span><span class="sxs-lookup"><span data-stu-id="a0cd4-103">Display data items and details</span></span>
====================
<span data-ttu-id="a0cd4-104">[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="a0cd4-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

> <span data-ttu-id="a0cd4-105">이 자습서 시리즈에서는 웹을 위한 ASP.NET 4.7 및 Microsoft Visual Studio Community 2017을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-105">This tutorial series teaches you the basics of building an ASP.NET Web Forms application with ASP.NET 4.7 and Microsoft Visual Studio Community 2017 for the Web.</span></span>

<span data-ttu-id="a0cd4-106">이 자습서에서는 데이터 항목 및 ASP.NET Web Forms 및 Entity Framework Code First를 사용 하 여 데이터 항목 세부 정보를 표시 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-106">In this tutorial, you learn how to display data items and data item details with ASP.NET Web Forms and Entity Framework Code First.</span></span> <span data-ttu-id="a0cd4-107">이 자습서 Wingtip 장난감 자습서 시리즈의 일부로 이전 "UI 및 탐색" 자습서를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-107">This tutorial builds on the previous "UI and Navigation" tutorial as part of the Wingtip Toy Store tutorial series.</span></span> <span data-ttu-id="a0cd4-108">완성 된 자습서에서는 제품에는 *ProductsList.aspx* 페이지 및 제품의 세부 정보에는 *ProductDetails.aspx* 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-108">In the completed tutorial, products on the *ProductsList.aspx* page and a product's details on the *ProductDetails.aspx* page are displayed.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="a0cd4-109">학습 내용</span><span class="sxs-lookup"><span data-stu-id="a0cd4-109">What you learn</span></span>

- <span data-ttu-id="a0cd4-110">데이터베이스 제품을 표시 하는 데이터 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-110">Add a data control to display database products.</span></span>
- <span data-ttu-id="a0cd4-111">선택한 데이터를 데이터 컨트롤을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-111">Connect a data control to selected data.</span></span>
- <span data-ttu-id="a0cd4-112">제품 세부 정보를 표시 하는 데이터 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-112">Add a data control to display product details.</span></span>
- <span data-ttu-id="a0cd4-113">쿼리 문자열 값을 구문 분석 및 검색된 데이터베이스 데이터를 필터링 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-113">Parse a query string value and use it to filter retrieved database data.</span></span>

<span data-ttu-id="a0cd4-114">이 자습서에 도입 된 기능에는 모델 바인딩 및 값 공급자 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-114">Features introduced in this tutorial include model binding and value providers.</span></span>

## <a name="add-a-data-control-to-display-products"></a><span data-ttu-id="a0cd4-115">제품을 전시 하기 데이터 컨트롤 추가</span><span class="sxs-lookup"><span data-stu-id="a0cd4-115">Add a data control to display products</span></span>
 
<span data-ttu-id="a0cd4-116">서버 컨트롤에 데이터를 바인딩하는 몇 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-116">You have a few options to bind data to a server control.</span></span> <span data-ttu-id="a0cd4-117">가장 일반적인 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-117">The most common include:</span></span>

 * <span data-ttu-id="a0cd4-118">데이터 소스 컨트롤 추가</span><span class="sxs-lookup"><span data-stu-id="a0cd4-118">Adding a data source control</span></span>
 * <span data-ttu-id="a0cd4-119">코드를 직접 추가</span><span class="sxs-lookup"><span data-stu-id="a0cd4-119">Adding code by hand</span></span>
 * <span data-ttu-id="a0cd4-120">모델 바인딩을 구현</span><span class="sxs-lookup"><span data-stu-id="a0cd4-120">Implementing model binding</span></span>

### <a name="use-a-data-source-control-to-bind-data"></a><span data-ttu-id="a0cd4-121">데이터 소스 컨트롤을 사용 하 여 데이터를 바인딩할</span><span class="sxs-lookup"><span data-stu-id="a0cd4-121">Use a data source control to bind data</span></span>

<span data-ttu-id="a0cd4-122">데이터 소스 컨트롤을 추가 데이터를 표시 하는 컨트롤을 데이터 소스 컨트롤을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-122">Adding a data source control links the data source control to the control that displays the data.</span></span> <span data-ttu-id="a0cd4-123">이 접근 방식 대신 수 있습니다 선언적으로 프로그래밍 방식으로 데이터 원본에 서버 쪽 컨트롤을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-123">With this approach, you can declaratively, rather than programmatically, connect server-side controls to data sources.</span></span>

### <a name="code-by-hand-to-bind-data"></a><span data-ttu-id="a0cd4-124">직접 데이터를 바인딩하는 코드</span><span class="sxs-lookup"><span data-stu-id="a0cd4-124">Code by hand to bind data</span></span>

<span data-ttu-id="a0cd4-125">직접 코딩 하는 작업에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-125">Coding by hand involves:</span></span>

1. <span data-ttu-id="a0cd4-126">값 읽기</span><span class="sxs-lookup"><span data-stu-id="a0cd4-126">Reading a value</span></span>
2. <span data-ttu-id="a0cd4-127">Null 인지 확인</span><span class="sxs-lookup"><span data-stu-id="a0cd4-127">Checking if it's null</span></span>
3. <span data-ttu-id="a0cd4-128">적절 한 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="a0cd4-128">Converting it to an appropriate type</span></span>
4. <span data-ttu-id="a0cd4-129">변환이 성공 확인</span><span class="sxs-lookup"><span data-stu-id="a0cd4-129">Checking conversion success</span></span>
5. <span data-ttu-id="a0cd4-130">변환 된 값을 사용 하 여 쿼리를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-130">Making a query with the converted value</span></span> 

<span data-ttu-id="a0cd4-131">이 방법을 사용 하 여 데이터 액세스 논리를 완전히 제어할을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-131">With this approach, you have full control over your data-access logic.</span></span>

### <a name="use-model-binding-to-bind-data"></a><span data-ttu-id="a0cd4-132">모델 바인딩을 사용 하 여 데이터 바인딩</span><span class="sxs-lookup"><span data-stu-id="a0cd4-132">Use model binding to bind data</span></span>

<span data-ttu-id="a0cd4-133">모델 바인딩을 사용 하 여 훨씬 적은 코드를 사용 하 여 결과 바인딩하고 응용 프로그램 전체에서 기능을 재사용할 수 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-133">With model binding, you bind results with far less code and it gives you the ability to reuse the functionality throughout your application.</span></span> <span data-ttu-id="a0cd4-134">풍부 하 고 데이터 바인딩 프레임 워크를 제공 하면서 코드에 초점을 맞춘 데이터 액세스 논리를 사용 하 여 작업을 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-134">It simplifies working with code-focused data-access logic while still providing a rich, data-binding framework.</span></span>

## <a name="display-products"></a><span data-ttu-id="a0cd4-135">제품 표시</span><span class="sxs-lookup"><span data-stu-id="a0cd4-135">Display products</span></span>

<span data-ttu-id="a0cd4-136">이 자습서에서는 모델 바인딩을 사용 하 여 데이터 바인딩.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-136">In this tutorial, you use model binding to bind data.</span></span> <span data-ttu-id="a0cd4-137">컨트롤의 모델 바인딩을 사용 하 여 데이터를 선택 하도록 데이터 컨트롤을 구성 하려면 설정 `SelectMethod` 페이지의 코드에서 메서드를 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-137">To configure a data control to use model binding to select data, you set the control's `SelectMethod` property to a method in the page's code.</span></span> <span data-ttu-id="a0cd4-138">데이터 컨트롤의 페이지 수명 주기의 적절 한 시간에 메서드를 호출 하 고 자동으로 반환된 된 데이터를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-138">The data control calls the method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="a0cd4-139">명시적으로 호출 하지 않아도 됩니다는 `DataBind` 메서드.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-139">There's no need to explicitly call the `DataBind` method.</span></span>

<span data-ttu-id="a0cd4-140">다음 단계를 통해 작업을 수정할 *ProductList.aspx* 제품을 표시 하는 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-140">Working through the following steps, you modify *ProductList.aspx* markup to display products.</span></span>

1. <span data-ttu-id="a0cd4-141">**솔루션 탐색기**오픈 *ProductList.aspx*합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-141">In **Solution Explorer**, open *ProductList.aspx*.</span></span>

2. <span data-ttu-id="a0cd4-142">기존 태그를 다음 태그로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-142">Replace the existing markup with the following markup:</span></span> 

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample1.aspx)]

<span data-ttu-id="a0cd4-143">위의 태그를 사용 하는 **ListView** 라는 컨트롤 `productList` 제품을 전시 하기.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-143">The preceding markup uses a **ListView** control named `productList` to display products.</span></span>

[!code-aspx-csharp[Main](display_data_items_and_details/samples/sample2.aspx)]

<span data-ttu-id="a0cd4-144">템플릿 및 스타일을 사용 하 여 정의 하는 방법을 **ListView** 컨트롤 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-144">With templates and styles, you define how the **ListView** control displays data.</span></span> <span data-ttu-id="a0cd4-145">모든 반복 구조에서 데이터에 대 한 두는 것이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-145">It's useful for data in any repeating structure.</span></span> <span data-ttu-id="a0cd4-146">하지만 이렇게 **ListView** 데이터베이스 데이터를 단순히 표시 하는 예제, 코드를 편집, 삽입 및 데이터를 삭제 하 고 정렬 및 데이터 페이지를 사용 하면 사용자가 없이 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-146">Though this **ListView** example simply displays database data, you can also, without code, enable users to edit, insert, and delete data, and to sort and page data.</span></span>

<span data-ttu-id="a0cd4-147">설정한 경우를 `ItemType` 속성에는 **ListView** 컨트롤을 데이터 바인딩 식을 `Item` 수 컨트롤은 강력한 형식의.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-147">When you set the `ItemType` property in the **ListView** control, the data-binding expression `Item` is available and the control becomes strongly typed.</span></span> <span data-ttu-id="a0cd4-148">이전 자습서에서 설명 했 듯이 지정 하는 등, IntelliSense 사용 하 여 개체 정보 항목을 선택할 수 있습니다는 `ProductName`:</span><span class="sxs-lookup"><span data-stu-id="a0cd4-148">As mentioned in the previous tutorial, you can select Item object details with IntelliSense, such as specifying the `ProductName`:</span></span>

![데이터를 표시할 항목 및 세부 정보-IntelliSense](display_data_items_and_details/_static/image1.png)

<span data-ttu-id="a0cd4-150">모델 바인딩을 사용 하 여 지정 하는 `SelectMethod` 값 (`GetProducts`).</span><span class="sxs-lookup"><span data-stu-id="a0cd4-150">With model binding, you're specifying a `SelectMethod` value (`GetProducts`).</span></span> <span data-ttu-id="a0cd4-151">이 방법은 코드를 추가한 다음 단계에서 제품을 전시 하기 지연 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-151">This is the method you add to the code behind to display products in the next step.</span></span>

### <a name="add-code-to-display-products"></a><span data-ttu-id="a0cd4-152">제품을 표시 하는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-152">Add code to display products</span></span>

<span data-ttu-id="a0cd4-153">이 단계에서는 채우는 코드를 추가 하는 **ListView** 데이터베이스 제품 데이터를 사용 하 여 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-153">In this step, you add code to populate the **ListView** control with database product data.</span></span> <span data-ttu-id="a0cd4-154">코드는 모든 제품 및 개별 범주 제품 표시를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-154">The code supports showing all products and individual category products.</span></span>

1. <span data-ttu-id="a0cd4-155">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *ProductList.aspx* 선택한 후 **코드 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-155">In **Solution Explorer**, right-click *ProductList.aspx* and then select **View Code**.</span></span>
2. <span data-ttu-id="a0cd4-156">기존 코드를 대체 합니다 *ProductList.aspx.cs* 이 사용 하 여 파일:</span><span class="sxs-lookup"><span data-stu-id="a0cd4-156">Replace the existing code in the *ProductList.aspx.cs* file with this:</span></span>   

    [!code-csharp[Main](display_data_items_and_details/samples/sample3.cs)]

<span data-ttu-id="a0cd4-157">이 코드를 보여 줍니다 합니다 `GetProducts` 메서드는 합니다 **ListView** 컨트롤의 `ItemType` 속성에서 참조 *ProductList.aspx*합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-157">This code shows the `GetProducts` method that the **ListView** control's `ItemType` property references in *ProductList.aspx*.</span></span> <span data-ttu-id="a0cd4-158">특정 데이터베이스 범주에 결과 제한 하려면 코드를 설정 하는 `categoryId` 전달할 쿼리 문자열의 값 *ProductList.aspx*합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-158">To limit the results to a specific database category, the code sets the `categoryId` value from the query string passed to *ProductList.aspx*.</span></span> <span data-ttu-id="a0cd4-159">합니다 `QueryStringAttribute` 클래스를 `System.Web.ModelBinding` 네임 스페이스는 쿼리 문자열 변수를 검색 하는 데 사용 됩니다 `id`의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-159">The `QueryStringAttribute` class in the `System.Web.ModelBinding` namespace is used to retrieve the query string variable `id`'s value.</span></span> <span data-ttu-id="a0cd4-160">이렇게 하면 모델 바인딩을, 런타임에 쿼리 문자열 값을 바인딩하는 `categoryId` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-160">This instructs model binding to, at run time, bind a query string value to the `categoryId` parameter.</span></span>

<span data-ttu-id="a0cd4-161">때 올바른 범주 (`categoryId`)가 전달 하면 해당 범주의 데이터베이스 제품에 제한 됩니다. 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-161">When a valid category (`categoryId`) is passed, the results are limited to that category's database products.</span></span> <span data-ttu-id="a0cd4-162">예를 들어 경우는 *ProductsList.aspx* 이것이 페이지 URL:</span><span class="sxs-lookup"><span data-stu-id="a0cd4-162">For instance, if the *ProductsList.aspx* page URL is this:</span></span>

[!code-console[Main](display_data_items_and_details/samples/sample4.cmd)]

<span data-ttu-id="a0cd4-163">페이지에는 제품 데이터만 표시 됩니다. 여기서는 `categoryId` equals `1`합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-163">The page displays only the products where the `categoryId` equals `1`.</span></span>

<span data-ttu-id="a0cd4-164">모든 제품에는 쿼리 문자열이 없으면이 전달 되 면 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-164">All products are displayed if no query string is passed.</span></span>

<span data-ttu-id="a0cd4-165">이러한 메서드에 대 한 값 소스 라고 *공급자 값* (같은 `QueryString`)를 사용 하는 값 공급자를 나타내는 매개 변수 특성 이라고 하 고 *공급자 특성 값* ( 와 같은 `id`).</span><span class="sxs-lookup"><span data-stu-id="a0cd4-165">The value sources for these methods are called *value providers* (such as `QueryString`), and the parameter attributes that indicate which value provider to use are called *value provider attributes* (such as `id`).</span></span> <span data-ttu-id="a0cd4-166">ASP.NET 값 공급자 및 모든 일반적인 Web Forms 응용 프로그램 사용자 입력된 원본에 대 한 특성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-166">ASP.NET includes value providers and attributes for all typical Web Forms application user input sources.</span></span> <span data-ttu-id="a0cd4-167">이러한 쿼리 문자열, 쿠키, 폼 값, 컨트롤, 상태 보기, 세션 상태 및 프로필 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-167">These include the query string, cookies, form values, controls, view state, session state, and profile properties.</span></span> <span data-ttu-id="a0cd4-168">또한 사용자 지정 값 공급자를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-168">You can also write custom value providers.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="a0cd4-169">애플리케이션 실행</span><span class="sxs-lookup"><span data-stu-id="a0cd4-169">Run the application</span></span>

<span data-ttu-id="a0cd4-170">모든 제품 또는 범주의 제품을 보려면 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-170">Run the application now to view all products or a category's products.</span></span>

1. <span data-ttu-id="a0cd4-171">Visual Studio에서 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-171">In Visual Studio, press **F5** to run the application.</span></span>
 <span data-ttu-id="a0cd4-172">브라우저가 열리고 표시 합니다 *Default.aspx* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-172">The browser opens and shows the *Default.aspx* page.</span></span>

2. <span data-ttu-id="a0cd4-173">제품 범주 메뉴에서 선택 **자동차**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-173">From the product category menu, select **Cars**.</span></span>

   <span data-ttu-id="a0cd4-174">*ProductList.aspx* 페이지가 나타나면 제품만 표시를 **자동차** 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-174">The *ProductList.aspx* page appears, showing only products from the **Cars** category.</span></span> <span data-ttu-id="a0cd4-175">이 자습서의 뒷부분에서 제품 세부 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-175">Later in this tutorial, you display product details.</span></span>

    ![데이터를 표시할 항목 및 세부 정보-자동차](display_data_items_and_details/_static/image2.png)

3. <span data-ttu-id="a0cd4-177">선택 **제품** 위쪽 메뉴에서.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-177">Select **Products** from the top menu.</span></span>
 <span data-ttu-id="a0cd4-178">합니다 *ProductList.aspx* 페이지에는 이제 모든 제품이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-178">The *ProductList.aspx* page now displays all products.</span></span> 

    ![데이터를 표시할 항목 및 세부 정보-제품](display_data_items_and_details/_static/image3.png)

4. <span data-ttu-id="a0cd4-180">브라우저를 닫고 Visual Studio로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-180">Close the browser and return to Visual Studio.</span></span>

### <a name="add-a-data-control-to-display-product-details"></a><span data-ttu-id="a0cd4-181">제품 세부 정보를 표시 하는 데이터 컨트롤 추가</span><span class="sxs-lookup"><span data-stu-id="a0cd4-181">Add a Data Control to display product details</span></span>

<span data-ttu-id="a0cd4-182">수정 된 *ProductDetails.aspx* 특정 제품 정보를 표시 하려면 이전 자습서에서 추가한 태그:</span><span class="sxs-lookup"><span data-stu-id="a0cd4-182">Modify the *ProductDetails.aspx* markup that you added in the previous tutorial to display specific product information:</span></span>

1. <span data-ttu-id="a0cd4-183">**솔루션 탐색기**오픈 *ProductDetails.aspx*합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-183">In **Solution Explorer**, open *ProductDetails.aspx*.</span></span>

2. <span data-ttu-id="a0cd4-184">이 태그를 사용 하 여 기존 태그를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-184">Replace the existing markup with this markup:</span></span>

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample5.aspx)] 

<span data-ttu-id="a0cd4-185">이 태그를 사용 하는 **FormView** 컨트롤을 특정 제품 세부 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-185">This markup uses a **FormView** control to display specific product details.</span></span> <span data-ttu-id="a0cd4-186">데이터를 표시 하는 데 사용 하는 것과 같은 메서드를 사용 하 여 *ProductList.aspx*합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-186">It uses methods like those used to display data in *ProductList.aspx*.</span></span> <span data-ttu-id="a0cd4-187">합니다 **FormView** 컨트롤은 데이터 원본에서 한 번에 하나의 레코드를 표시 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-187">The **FormView** control is used to display a single record at a time from a data source.</span></span> <span data-ttu-id="a0cd4-188">사용 하는 경우는 **FormView** 컨트롤을 만든 템플릿을 표시 하 고 데이터 바인딩된 값을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-188">When you use the **FormView** control, you create templates to display and edit data-bound values.</span></span> <span data-ttu-id="a0cd4-189">이러한 템플릿에 컨트롤에 바인딩 식에 포함 하 고 폼의 모양 및 기능 정의 서식 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-189">These templates contain controls, binding expressions, and formatting that define the form's look and functionality.</span></span>

<span data-ttu-id="a0cd4-190">데이터베이스에 이전 태그 연결 추가 코드가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-190">Connecting the previous markup to the database requires additional code.</span></span>

1. <span data-ttu-id="a0cd4-191">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *ProductDetails.aspx* 선택한 후 **코드 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-191">In **Solution Explorer**, right-click *ProductDetails.aspx* and then select **View Code**.</span></span>  
   <span data-ttu-id="a0cd4-192">합니다 *ProductDetails.aspx.cs* 파일이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-192">The *ProductDetails.aspx.cs* file is displayed.</span></span>

2. <span data-ttu-id="a0cd4-193">이 사용 하 여 기존 코드를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-193">Replace the existing code with this:</span></span>   

    [!code-csharp[Main](display_data_items_and_details/samples/sample6.cs)]

<span data-ttu-id="a0cd4-194">이 코드는 검사는 "`productID`" 쿼리 문자열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-194">This code checks for a "`productID`" query string value.</span></span> <span data-ttu-id="a0cd4-195">유효한 값이 있으면 일치 하는 제품이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-195">If a valid value is found, the matching product is displayed.</span></span> <span data-ttu-id="a0cd4-196">쿼리 문자열을 찾을 수 없으면 경우 해당 값에는 유효 하지 않습니다. 제품이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-196">If the query string isn't found, or its value isn't valid, no product is displayed.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="a0cd4-197">애플리케이션 실행</span><span class="sxs-lookup"><span data-stu-id="a0cd4-197">Run the application</span></span>

<span data-ttu-id="a0cd4-198">이제 제품 ID를 기반으로 특정 제품 세부 정보를 보려면 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-198">Now you can run the application to see specific product details based on product ID.</span></span>

1. <span data-ttu-id="a0cd4-199">Visual Studio에서 눌러 **F5** 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-199">In Visual Studio, press **F5** to run the application.</span></span>  
 <span data-ttu-id="a0cd4-200">브라우저가 열리고 *Default.aspx*합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-200">The browser opens to *Default.aspx*.</span></span>

2. <span data-ttu-id="a0cd4-201">범주 메뉴에서 선택 **배**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-201">From the category menu, select **Boats**.</span></span>  
 <span data-ttu-id="a0cd4-202">합니다 *ProductList.aspx* 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-202">The *ProductList.aspx* page is displayed.</span></span>

3. <span data-ttu-id="a0cd4-203">선택 **재벌 용지**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-203">Select **Paper Boat**.</span></span>  
 <span data-ttu-id="a0cd4-204">합니다 *ProductDetails.aspx* 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-204">The *ProductDetails.aspx* page is displayed.</span></span>   

    ![데이터를 표시할 항목 및 세부 정보-제품](display_data_items_and_details/_static/image4.png)

<span data-ttu-id="a0cd4-206">다음 자습서에서는 Wingtip Toys 응용 프로그램에 쇼핑 카트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a0cd4-206">In the next tutorial, you add a shopping cart to the Wingtip Toys application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a0cd4-207">추가 자료</span><span class="sxs-lookup"><span data-stu-id="a0cd4-207">Additional resources</span></span>

[<span data-ttu-id="a0cd4-208">모델 바인딩 및 web forms를 사용 하 여 데이터 검색 및 표시</span><span class="sxs-lookup"><span data-stu-id="a0cd4-208">Retrieving and displaying data with model binding and web forms</span></span>](../../presenting-and-managing-data/model-binding/retrieving-data.md)

> [!div class="step-by-step"]
> <span data-ttu-id="a0cd4-209">[이전](ui_and_navigation.md)
> [다음](shopping-cart.md)</span><span class="sxs-lookup"><span data-stu-id="a0cd4-209">[Previous](ui_and_navigation.md)
[Next](shopping-cart.md)</span></span>
