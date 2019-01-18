---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
title: 데이터 표시 항목 및 세부 정보 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈에서는 ASP.NET 4.7 및 Microsoft Visual Studio 2017을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항
ms.author: riande
ms.date: 1/04/2019
ms.assetid: 64a491a8-0ed6-4c2f-9c1c-412962eb6006
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
msc.type: authoredcontent
ms.openlocfilehash: acc2f8e78375ef0455d467e2af750ecbee623224
ms.sourcegitcommit: 184ba5b44d1c393076015510ac842b77bc9d4d93
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2019
ms.locfileid: "54396227"
---
<a name="display-data-items-and-details"></a><span data-ttu-id="9af42-103">데이터 항목 및 세부 정보</span><span class="sxs-lookup"><span data-stu-id="9af42-103">Display data items and details</span></span>
====================
<span data-ttu-id="9af42-104">[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="9af42-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

> <span data-ttu-id="9af42-105">이 자습서 시리즈에서는 ASP.NET 4.7 및 Microsoft Visual Studio 2017을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-105">This tutorial series teaches you the basics of building an ASP.NET Web Forms application with ASP.NET 4.7 and Microsoft Visual Studio 2017.</span></span>

<span data-ttu-id="9af42-106">이 자습서에서는 데이터 항목 및 ASP.NET Web Forms 및 Entity Framework Code First를 사용 하 여 데이터 항목 세부 정보를 표시 하는 방법에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-106">In this tutorial, you'll learn how to display data items and data item details with ASP.NET Web Forms and Entity Framework Code First.</span></span> <span data-ttu-id="9af42-107">이 자습서 Wingtip 장난감 자습서 시리즈의 일부로 이전 "UI 및 탐색" 자습서를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-107">This tutorial builds on the previous "UI and Navigation" tutorial as part of the Wingtip Toy Store tutorial series.</span></span> <span data-ttu-id="9af42-108">이 자습서를 완료 한 후에 제품이 표시 됩니다는 *ProductsList.aspx* 페이지 및 제품의 세부 정보에는 *ProductDetails.aspx* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-108">After completing this tutorial, you'll see products on the *ProductsList.aspx* page and a product's details on the *ProductDetails.aspx* page.</span></span>

## <a name="youll-learn-how-to"></a><span data-ttu-id="9af42-109">다음을 수행하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-109">You'll learn how to:</span></span>

- <span data-ttu-id="9af42-110">데이터베이스에서 제품을 전시 하기 데이터 컨트롤 추가</span><span class="sxs-lookup"><span data-stu-id="9af42-110">Add a data control to display products from the database</span></span>
- <span data-ttu-id="9af42-111">데이터 컨트롤을 선택한 데이터에 연결</span><span class="sxs-lookup"><span data-stu-id="9af42-111">Connect a data control to the selected data</span></span>
- <span data-ttu-id="9af42-112">데이터베이스에서 제품 세부 정보를 표시 하는 데이터 컨트롤 추가</span><span class="sxs-lookup"><span data-stu-id="9af42-112">Add a data control to display product details from the database</span></span>
- <span data-ttu-id="9af42-113">쿼리 문자열에서 값을 검색 하 고 해당 값을 사용 하 여 데이터베이스에서 검색 되는 데이터 제한</span><span class="sxs-lookup"><span data-stu-id="9af42-113">Retrieve a value from the query string and use that value to limit the data that's retrieved from the database</span></span>

### <a name="features-introduced-in-this-tutorial"></a><span data-ttu-id="9af42-114">이 자습서에 도입 된 기능:</span><span class="sxs-lookup"><span data-stu-id="9af42-114">Features introduced in this tutorial:</span></span>

- <span data-ttu-id="9af42-115">모델 바인딩</span><span class="sxs-lookup"><span data-stu-id="9af42-115">Model binding</span></span>
- <span data-ttu-id="9af42-116">값 공급자</span><span class="sxs-lookup"><span data-stu-id="9af42-116">Value providers</span></span>

## <a name="add-a-data-control"></a><span data-ttu-id="9af42-117">데이터 컨트롤 추가</span><span class="sxs-lookup"><span data-stu-id="9af42-117">Add a data control</span></span>

<span data-ttu-id="9af42-118">서버 컨트롤에 데이터를 바인딩할 몇 가지 다른 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-118">You can use a few different options to bind data to a server control.</span></span> <span data-ttu-id="9af42-119">가장 일반적인 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-119">The most common include:</span></span>

 * <span data-ttu-id="9af42-120">데이터 소스 컨트롤 추가</span><span class="sxs-lookup"><span data-stu-id="9af42-120">Adding a data source control</span></span>
 * <span data-ttu-id="9af42-121">코드를 직접 추가</span><span class="sxs-lookup"><span data-stu-id="9af42-121">Adding code by hand</span></span>
 * <span data-ttu-id="9af42-122">모델 바인딩을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="9af42-122">Using model binding</span></span>

### <a name="use-a-data-source-control-to-bind-data"></a><span data-ttu-id="9af42-123">데이터 소스 컨트롤을 사용 하 여 데이터를 바인딩할</span><span class="sxs-lookup"><span data-stu-id="9af42-123">Use a data source control to bind data</span></span>

<span data-ttu-id="9af42-124">데이터 소스 컨트롤을 추가 데이터를 표시 하는 컨트롤에 데이터 소스 컨트롤을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-124">Adding a data source control allows you to link the data source control to the control that displays the data.</span></span> <span data-ttu-id="9af42-125">이 접근 방식 대신 수 있습니다 선언적으로 프로그래밍 방식으로 데이터 원본에 서버 쪽 컨트롤을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-125">With this approach, you can declaratively,  rather than programmatically, connect server-side controls to data sources.</span></span>

### <a name="code-by-hand-to-bind-data"></a><span data-ttu-id="9af42-126">직접 데이터를 바인딩하는 코드</span><span class="sxs-lookup"><span data-stu-id="9af42-126">Code by hand to bind data</span></span>

<span data-ttu-id="9af42-127">직접 코딩 하는 작업에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-127">Coding by hand involves:</span></span>

1. <span data-ttu-id="9af42-128">값 읽기</span><span class="sxs-lookup"><span data-stu-id="9af42-128">Reading a value</span></span>
2. <span data-ttu-id="9af42-129">Null 인지 확인</span><span class="sxs-lookup"><span data-stu-id="9af42-129">Checking if it's null</span></span>
3. <span data-ttu-id="9af42-130">적절 한 형식으로 변환</span><span class="sxs-lookup"><span data-stu-id="9af42-130">Converting it to an appropriate type</span></span>
4. <span data-ttu-id="9af42-131">변환이 성공 확인</span><span class="sxs-lookup"><span data-stu-id="9af42-131">Checking conversion success</span></span>
5. <span data-ttu-id="9af42-132">쿼리에서 값을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="9af42-132">Using the value in the query</span></span> 

<span data-ttu-id="9af42-133">이 방법을 사용 하면 데이터 액세스 논리를 완벽히 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-133">This approach lets you have full control over your data-access logic.</span></span>

### <a name="use-model-binding-to-bind-data"></a><span data-ttu-id="9af42-134">모델 바인딩을 사용 하 여 데이터 바인딩</span><span class="sxs-lookup"><span data-stu-id="9af42-134">Use model binding to bind data</span></span>

<span data-ttu-id="9af42-135">모델 바인딩 훨씬 적은 코드를 사용 하 여 결과 바인딩할 수 있습니다. 및 기능을 응용 프로그램 전체에서 재사용할 수 있는 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-135">Model binding lets you bind results with far less code and gives you the ability to reuse the functionality throughout your application.</span></span> <span data-ttu-id="9af42-136">풍부 하 고 데이터 바인딩 프레임 워크를 제공 하면서 코드에 초점을 맞춘 데이터 액세스 논리를 사용 하 여 작업을 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-136">It simplifies working with code-focused data-access logic while still providing a rich, data-binding framework.</span></span>

## <a name="display-products"></a><span data-ttu-id="9af42-137">제품 표시</span><span class="sxs-lookup"><span data-stu-id="9af42-137">Display products</span></span>

<span data-ttu-id="9af42-138">이 자습서에서는 데이터를 바인딩할 모델 바인딩을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-138">In this tutorial, you'll use model binding to bind data.</span></span> <span data-ttu-id="9af42-139">컨트롤의 모델 바인딩을 사용 하 여 데이터를 선택 하도록 데이터 컨트롤을 구성 하려면 설정 `SelectMethod` 속성 페이지의 코드에 메서드 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-139">To configure a data control to use model binding to select data, you set the control's `SelectMethod` property to a method name in the page's code.</span></span> <span data-ttu-id="9af42-140">데이터 컨트롤의 페이지 수명 주기의 적절 한 시간에 메서드를 호출 하 고 자동으로 반환된 된 데이터를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-140">The data control calls the method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="9af42-141">명시적으로 호출 하지 않아도 됩니다는 `DataBind` 메서드.</span><span class="sxs-lookup"><span data-stu-id="9af42-141">There's no need to explicitly call the `DataBind` method.</span></span>

1. <span data-ttu-id="9af42-142">**솔루션 탐색기**오픈 *ProductList.aspx*합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-142">In **Solution Explorer**, open *ProductList.aspx*.</span></span>
2. <span data-ttu-id="9af42-143">이 태그를 사용 하 여 기존 태그를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-143">Replace the existing markup with this markup:</span></span>   

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample1.aspx)]

<span data-ttu-id="9af42-144">이 코드를 사용 하는 **ListView** 라는 컨트롤 `productList` 제품을 전시 하기.</span><span class="sxs-lookup"><span data-stu-id="9af42-144">This code uses a **ListView** control named `productList` to display products.</span></span>

[!code-aspx-csharp[Main](display_data_items_and_details/samples/sample2.aspx)]

<span data-ttu-id="9af42-145">템플릿 및 스타일을 사용 하 여 정의 하는 방법을 **ListView** 컨트롤 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-145">With templates and styles, you define how the **ListView** control displays data.</span></span> <span data-ttu-id="9af42-146">모든 반복 구조에서 데이터에 대 한 두는 것이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-146">It's useful for data in any repeating structure.</span></span> <span data-ttu-id="9af42-147">하지만 이렇게 **ListView** 데이터베이스 데이터를 단순히 표시 하는 예제, 코드를 편집, 삽입 및 데이터를 삭제 하 고 정렬 및 데이터 페이지를 사용 하면 사용자가 없이 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-147">Though this **ListView** example simply displays database data, you can also, without code, enable users to edit, insert, and delete data, and to sort and page data.</span></span>

<span data-ttu-id="9af42-148">설정 하 여는 `ItemType` 속성에는 **ListView** 컨트롤을 데이터 바인딩 식을 `Item` 수 컨트롤은 강력한 형식의.</span><span class="sxs-lookup"><span data-stu-id="9af42-148">By setting the `ItemType` property in the **ListView** control, the data-binding expression `Item` is available and the control becomes strongly typed.</span></span> <span data-ttu-id="9af42-149">이전 자습서에서 설명 했 듯이 지정 하는 등, IntelliSense 사용 하 여 개체 정보 항목을 선택할 수 있습니다는 `ProductName`:</span><span class="sxs-lookup"><span data-stu-id="9af42-149">As mentioned in the previous tutorial, you can select Item object details with IntelliSense, such as specifying the `ProductName`:</span></span>

![데이터를 표시할 항목 및 세부 정보-IntelliSense](display_data_items_and_details/_static/image1.png)

<span data-ttu-id="9af42-151">모델 바인딩을 지정 하 여도 되는 `SelectMethod` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-151">You're also using model binding to specify a `SelectMethod` value.</span></span> <span data-ttu-id="9af42-152">이 값 (`GetProducts`) 코드에 추가 된 메서드에 해당 하는 다음 단계에서 제품을 전시 하기 지연 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-152">This value (`GetProducts`) corresponds to the method you'll add to the code behind to display products in the next step.</span></span>

### <a name="add-code-to-display-products"></a><span data-ttu-id="9af42-153">제품을 표시 하는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-153">Add code to display products</span></span>

<span data-ttu-id="9af42-154">이 단계에서는 채우는 코드를 추가 합니다 **ListView** 데이터베이스에서 제품 데이터를 사용 하 여 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-154">In this step, you'll add code to populate the **ListView** control with product data from the database.</span></span> <span data-ttu-id="9af42-155">코드는 모든 제품 및 개별 범주 제품 표시를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-155">The code supports showing all products and  individual category products.</span></span>

1. <span data-ttu-id="9af42-156">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *ProductList.aspx* 선택한 후 **코드 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-156">In **Solution Explorer**, right-click *ProductList.aspx* and then select **View Code**.</span></span>
2. <span data-ttu-id="9af42-157">기존 코드를 대체 합니다 *ProductList.aspx.cs* 이 사용 하 여 파일:</span><span class="sxs-lookup"><span data-stu-id="9af42-157">Replace the existing code in the *ProductList.aspx.cs* file with this:</span></span>   

    [!code-csharp[Main](display_data_items_and_details/samples/sample3.cs)]

<span data-ttu-id="9af42-158">보여 주는이 코드를 `GetProducts` 메서드는 합니다 **ListView** 컨트롤의 `ItemType` 속성에서 참조를 *ProductList.aspx* 페이지.</span><span class="sxs-lookup"><span data-stu-id="9af42-158">This code shows the `GetProducts` method that the **ListView** control's `ItemType` property references in the *ProductList.aspx* page.</span></span> <span data-ttu-id="9af42-159">특정 데이터베이스 범주에 결과 제한 하려면이 코드는 다음과 같이 설정 됩니다.는 `categoryId` 전달할 쿼리 문자열 값에서 값을 *ProductList.aspx* 때 페이지를 *ProductList.aspx* 페이지 탐색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-159">To limit the results to a specific database category, the code sets the `categoryId` value from the query string value passed to the *ProductList.aspx* page when the *ProductList.aspx* page is navigated to.</span></span> <span data-ttu-id="9af42-160">합니다 `QueryStringAttribute` 클래스를 `System.Web.ModelBinding` 네임 스페이스는 쿼리 문자열 변수의 값을 검색 하는 `id`합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-160">The `QueryStringAttribute` class in the `System.Web.ModelBinding` namespace is used to retrieve the value of the query string variable `id`.</span></span> <span data-ttu-id="9af42-161">이렇게 하면 모델 바인딩을에 쿼리 문자열에서 값을 바인딩하려는 `categoryId` 런타임에 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-161">This instructs model binding to try to bind a value from the query string to the `categoryId` parameter at run time.</span></span>

<span data-ttu-id="9af42-162">유효한 범주를이 페이지에 쿼리 문자열로 전달 되 면 쿼리 결과가 일치 하는 데이터베이스에서 해당 제품에만 국한 된 `categoryId` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-162">When a valid category is passed as a query string to the page, the results of the query are limited to those products in the database that match the `categoryId` value.</span></span> <span data-ttu-id="9af42-163">예를 들어 경우는 *ProductsList.aspx* 이것이 페이지 URL:</span><span class="sxs-lookup"><span data-stu-id="9af42-163">For instance, if the *ProductsList.aspx* page URL is this:</span></span>


[!code-console[Main](display_data_items_and_details/samples/sample4.cmd)]

<span data-ttu-id="9af42-164">페이지에는 제품 데이터만 표시 됩니다. 여기서는 `categoryId` equals `1`합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-164">The page displays only the products where the `categoryId` equals `1`.</span></span>

<span data-ttu-id="9af42-165">쿼리 문자열이 없으면이 포함 된 모든 제품 표시 되는 *ProductList.aspx* 페이지 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-165">All products are displayed if no query string is included when the *ProductList.aspx* page is called.</span></span>

<span data-ttu-id="9af42-166">이러한 메서드에 대 한 값의 소스 라고 *공급자 값* (같은 *QueryString*)를 사용 하는 값 공급자를 나타내는 매개 변수 특성 라고하고*공급자 특성 값* (같은 `id`).</span><span class="sxs-lookup"><span data-stu-id="9af42-166">The sources of values for these methods are referred to as *value providers* (such as *QueryString*), and the parameter attributes that indicate which value provider to use are referred to as *value provider attributes* (such as `id`).</span></span> <span data-ttu-id="9af42-167">ASP.NET은 Web Forms 응용 프로그램의 쿼리 문자열, 쿠키, 폼 값, 컨트롤와 같은 뷰 상태, 세션 상태 프로필 속성에서 값 공급자 및 모든 사용자 입력의 일반적인 원본에 대 한 해당 특성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-167">ASP.NET includes value providers and corresponding attributes for all of the typical sources of user input in a Web Forms application such as the query string, cookies, form values, controls, view state, session state, and profile properties.</span></span> <span data-ttu-id="9af42-168">또한 사용자 지정 값 공급자를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-168">You can also write custom value providers.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="9af42-169">애플리케이션 실행</span><span class="sxs-lookup"><span data-stu-id="9af42-169">Run the application</span></span>

<span data-ttu-id="9af42-170">모든 제품 또는 범주의 제품을 보려면 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-170">Run the application now to view all products or a category's products.</span></span>

1. <span data-ttu-id="9af42-171">키를 눌러 **F5** 응용 프로그램을 실행 하려면 Visual Studio에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-171">Press **F5** while in Visual Studio to run the application.</span></span>  
   <span data-ttu-id="9af42-172">브라우저가 열리고 표시 합니다 *Default.aspx* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-172">The browser opens and shows the *Default.aspx* page.</span></span>

2. <span data-ttu-id="9af42-173">선택 **자동차** 제품 범주 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-173">Select **Cars** from the product category navigation menu.</span></span>  
   <span data-ttu-id="9af42-174">합니다 *ProductList.aspx* 페이지에 표시만 표시 됩니다 **자동차** 범주 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-174">The *ProductList.aspx* page displays showing only **Cars** category products.</span></span> <span data-ttu-id="9af42-175">이 자습서의 뒷부분에서 제품 세부 정보를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-175">Later in this tutorial, you'll display product details.</span></span>  

    ![데이터를 표시할 항목 및 세부 정보-자동차](display_data_items_and_details/_static/image2.png)

3. <span data-ttu-id="9af42-177">선택 **제품** 맨 위에 있는 탐색 메뉴에서.</span><span class="sxs-lookup"><span data-stu-id="9af42-177">Select **Products** from the navigation menu at the top.</span></span>  
   <span data-ttu-id="9af42-178">하지만 마찬가지로 합니다 *ProductList.aspx* 이 이번 제품의 전체 목록을 표시 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-178">Again, the *ProductList.aspx* page is displayed, however this time it shows the entire list of products.</span></span>   

    ![데이터를 표시할 항목 및 세부 정보-제품](display_data_items_and_details/_static/image3.png)

4. <span data-ttu-id="9af42-180">브라우저를 닫고 Visual Studio로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-180">Close the browser and return to Visual Studio.</span></span>

### <a name="add-a-data-control-to-display-product-details"></a><span data-ttu-id="9af42-181">제품 세부 정보를 표시 하는 데이터 컨트롤 추가</span><span class="sxs-lookup"><span data-stu-id="9af42-181">Add a data control to display product details</span></span>

<span data-ttu-id="9af42-182">다음으로 태그를 수정 합니다 *ProductDetails.aspx* 특정 제품 정보를 표시 하려면 이전 자습서에서 추가한 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-182">Next, you'll modify the markup in the *ProductDetails.aspx* page that you added in the previous tutorial to display specific product information.</span></span>

1. <span data-ttu-id="9af42-183">**솔루션 탐색기**오픈 *ProductDetails.aspx*합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-183">In **Solution Explorer**, open *ProductDetails.aspx*.</span></span>

2. <span data-ttu-id="9af42-184">이 태그를 사용 하 여 기존 태그를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-184">Replace the existing markup with this markup:</span></span>

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample5.aspx)] 

    <span data-ttu-id="9af42-185">이 코드를 사용 하는 **FormView** 특정 제품 세부 정보를 표시 하는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-185">This code uses a **FormView** control to display specific product details.</span></span> <span data-ttu-id="9af42-186">이 태그에 데이터를 표시 하는 데 사용 하는 메서드와 마찬가지로 메서드를 사용 합니다 *ProductList.aspx* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-186">This markup uses methods like the methods used to display data in the *ProductList.aspx* page.</span></span> <span data-ttu-id="9af42-187">합니다 **FormView** 컨트롤은 데이터 원본에서 한 번에 하나의 레코드를 표시 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-187">The **FormView** control is used to display a single record at a time from a data source.</span></span> <span data-ttu-id="9af42-188">사용 하는 경우는 **FormView** 컨트롤을 만든 템플릿을 표시 하 고 데이터 바인딩된 값을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-188">When you use the **FormView** control, you create templates to display and edit data-bound values.</span></span> <span data-ttu-id="9af42-189">이러한 템플릿에 컨트롤에 바인딩 식에 포함 하 고 폼의 모양 및 기능 정의 서식 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-189">These templates contain controls, binding expressions, and formatting that define the form's look and functionality.</span></span>

<span data-ttu-id="9af42-190">데이터베이스에 이전 태그 연결 추가 코드가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-190">Connecting the previous markup to the database requires additional code.</span></span>

1. <span data-ttu-id="9af42-191">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *ProductDetails.aspx* 을 클릭 한 다음 **코드 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-191">In **Solution Explorer**, right-click *ProductDetails.aspx* and then click **View Code**.</span></span>  
   <span data-ttu-id="9af42-192">합니다 *ProductDetails.aspx.cs* 파일이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-192">The *ProductDetails.aspx.cs* file is displayed.</span></span>

2. <span data-ttu-id="9af42-193">기존 코드를이 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-193">Replace the existing code with this code:</span></span>   

    [!code-csharp[Main](display_data_items_and_details/samples/sample6.cs)]

<span data-ttu-id="9af42-194">이 코드는 검사는 "`productID`" 쿼리 문자열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-194">This code checks for a "`productID`" query-string value.</span></span> <span data-ttu-id="9af42-195">유효한 쿼리 문자열 값이 있으면 일치 하는 제품이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-195">If a valid query-string value is found, the matching product is displayed.</span></span> <span data-ttu-id="9af42-196">쿼리 문자열을 찾을 수 없으면 경우 해당 값에는 유효 하지 않습니다. 제품이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-196">If the query-string isn't found, or its value isn't valid, no product is displayed.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="9af42-197">애플리케이션 실행</span><span class="sxs-lookup"><span data-stu-id="9af42-197">Run the application</span></span>

<span data-ttu-id="9af42-198">제품 ID를 기반으로 이제 표시 된 개별 제품을 보려면 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-198">Now you can run the application to see an individual product displayed based on product ID.</span></span>

1. <span data-ttu-id="9af42-199">키를 눌러 **F5** 응용 프로그램을 실행 하려면 Visual Studio에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-199">Press **F5** while in Visual Studio to run the application.</span></span>  
   <span data-ttu-id="9af42-200">브라우저가 열리고 표시 합니다 *Default.aspx* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-200">The browser opens and shows the *Default.aspx* page.</span></span>

2. <span data-ttu-id="9af42-201">선택 **배** 범주 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-201">Select **Boats** from the category navigation menu.</span></span>  
   <span data-ttu-id="9af42-202">합니다 *ProductList.aspx* 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-202">The *ProductList.aspx* page is displayed.</span></span>

3. <span data-ttu-id="9af42-203">선택 **용지 재벌** 제품 목록에서.</span><span class="sxs-lookup"><span data-stu-id="9af42-203">Select **Paper Boat** from the product list.</span></span>
   <span data-ttu-id="9af42-204">합니다 *ProductDetails.aspx* 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-204">The *ProductDetails.aspx* page is displayed.</span></span>

    ![데이터를 표시할 항목 및 세부 정보-제품](display_data_items_and_details/_static/image4.png)
    
4. <span data-ttu-id="9af42-206">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-206">Close the browser.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="9af42-207">추가 자료</span><span class="sxs-lookup"><span data-stu-id="9af42-207">Additional resources</span></span>

[<span data-ttu-id="9af42-208">모델 바인딩 및 web forms를 사용 하 여 데이터 검색 및 표시</span><span class="sxs-lookup"><span data-stu-id="9af42-208">Retrieving and displaying data with model binding and web forms</span></span>](../../presenting-and-managing-data/model-binding/retrieving-data.md)

## <a name="next-steps"></a><span data-ttu-id="9af42-209">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9af42-209">Next steps</span></span>

<span data-ttu-id="9af42-210">이 자습서에서는 태그 및 제품 및 제품 세부 정보를 표시 하는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-210">In this tutorial, you added markup and code to display products and product details.</span></span> <span data-ttu-id="9af42-211">강력한 형식의 데이터 컨트롤, 모델 바인딩 및 값 공급자에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-211">You learned about strongly typed data controls, model binding, and value providers.</span></span> <span data-ttu-id="9af42-212">다음 자습서에서는 Wingtip Toys 샘플 응용 프로그램에 쇼핑 카트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af42-212">In the next tutorial, you'll add a shopping cart to the Wingtip Toys sample application.</span></span> 

> [!div class="step-by-step"]
> <span data-ttu-id="9af42-213">[이전](ui_and_navigation.md)
> [다음](shopping-cart.md)</span><span class="sxs-lookup"><span data-stu-id="9af42-213">[Previous](ui_and_navigation.md)
[Next](shopping-cart.md)</span></span>
