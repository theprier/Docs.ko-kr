---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
title: 데이터 표시 항목 및 세부 정보 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 것에 대 한 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항 설명 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/08/2014
ms.topic: article
ms.assetid: 64a491a8-0ed6-4c2f-9c1c-412962eb6006
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
msc.type: authoredcontent
ms.openlocfilehash: 08efafc1ae076bcf481c5c7d8aea2bbaa704af17
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37379740"
---
<a name="display-data-items-and-details"></a><span data-ttu-id="fe244-103">데이터 표시 항목 및 세부 정보</span><span class="sxs-lookup"><span data-stu-id="fe244-103">Display Data Items and Details</span></span>
====================
<span data-ttu-id="fe244-104">[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="fe244-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="fe244-105">[Wingtip Toys 샘플 프로젝트 (C#)를 다운로드](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자책 (PDF) 다운로드](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="fe244-105">[Download Wingtip Toys Sample Project (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="fe244-106">이 자습서 시리즈는 ASP.NET 4.5와 Microsoft Visual Studio Express 2013 for Web 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="fe244-107">Visual Studio 2013 [C# 소스 코드를 사용 하 여 프로젝트](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 이 자습서 시리즈를 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>


<span data-ttu-id="fe244-108">이 자습서에는 데이터 항목 및 ASP.NET Web Forms 및 Entity Framework Code First를 사용 하 여 데이터 항목 세부 정보를 표시 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-108">This tutorial describes how to display data items and data item details using ASP.NET Web Forms and Entity Framework Code First.</span></span> <span data-ttu-id="fe244-109">이 자습서는 이전 자습서 "UI 및 탐색" 빌드하고 Wingtip 장난감 자습서 시리즈의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-109">This tutorial builds on the previous tutorial "UI and Navigation" and is part of the Wingtip Toy Store tutorial series.</span></span> <span data-ttu-id="fe244-110">이 자습서를 완료 한 경우에에서 제품을 확인할 수 있습니다 합니다 *ProductsList.aspx* 페이지 및 개별 제품에 대 한 세부 정보를 *ProductDetails.aspx* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-110">When you've completed this tutorial, you'll be able to see products on the *ProductsList.aspx* page and details about an individual product on the *ProductDetails.aspx* page.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="fe244-111">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="fe244-111">What you'll learn:</span></span>

- <span data-ttu-id="fe244-112">데이터베이스에서 제품을 전시 하기 데이터 컨트롤을 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-112">How to add a data control to display products from the database.</span></span>
- <span data-ttu-id="fe244-113">선택한 데이터를 데이터 컨트롤을 연결 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="fe244-113">How to connect a data control to the selected data.</span></span>
- <span data-ttu-id="fe244-114">데이터베이스에서 제품 세부 정보를 표시 하는 데이터 컨트롤을 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-114">How to add a data control to display product details from the database.</span></span>
- <span data-ttu-id="fe244-115">쿼리 문자열에서 값을 검색 하 고 해당 값을 사용 하 여 데이터베이스에서 검색 되는 데이터를 제한 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="fe244-115">How to retrieve a value from the query string and use that value to limit the data that's retrieved from the database.</span></span>

### <a name="these-are-the-features-introduced-in-the-tutorial"></a><span data-ttu-id="fe244-116">다음은 자습서에서 도입 된 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-116">These are the features introduced in the tutorial:</span></span>

- <span data-ttu-id="fe244-117">모델 바인딩</span><span class="sxs-lookup"><span data-stu-id="fe244-117">Model Binding</span></span>
- <span data-ttu-id="fe244-118">값 공급자</span><span class="sxs-lookup"><span data-stu-id="fe244-118">Value providers</span></span>

## <a name="adding-a-data-control-to-display-products"></a><span data-ttu-id="fe244-119">제품을 전시 하기 데이터 컨트롤 추가</span><span class="sxs-lookup"><span data-stu-id="fe244-119">Adding a Data Control to Display Products</span></span>

<span data-ttu-id="fe244-120">서버 컨트롤에 데이터를 바인딩할 때 사용할 수는 몇 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-120">When binding data to a server control, there are a few different options you can use.</span></span> <span data-ttu-id="fe244-121">데이터 소스 컨트롤을 추가, 코드를 수동으로 추가 또는 모델 바인딩을 사용 하 여 가장 일반적인 옵션에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-121">The most common options include adding a data source control, adding code by hand, or using model binding.</span></span>

### <a name="using-a-data-source-control-to-bind-data"></a><span data-ttu-id="fe244-122">데이터 소스 컨트롤을 사용 하 여 데이터를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-122">Using a Data Source Control to Bind Data</span></span>

<span data-ttu-id="fe244-123">데이터 소스 컨트롤을 추가 데이터를 표시 하는 컨트롤에 데이터 소스 컨트롤을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-123">Adding a data source control allows you to link the data source control to the control that displays the data.</span></span> <span data-ttu-id="fe244-124">이 방법을 사용 하면 선언적 프로그래밍 방식을 사용 하기 보다는 데이터 원본에 직접 서버 쪽 컨트롤을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-124">This approach allows you to declaratively connect server-side controls directly to data sources, rather than using a programmatic approach.</span></span>

### <a name="coding-by-hand-to-bind-data"></a><span data-ttu-id="fe244-125">데이터를 바인딩할 직접 코딩</span><span class="sxs-lookup"><span data-stu-id="fe244-125">Coding By Hand to Bind Data</span></span>

<span data-ttu-id="fe244-126">수동으로 코드에서는 추가 값을 읽기, null 값을 확인 하는, 적절 한 형식으로 변환 하는 동안, 변환 성공 여부를 확인 및 마지막으로 값을 사용 하 여 쿼리에서</span><span class="sxs-lookup"><span data-stu-id="fe244-126">Adding code by hand involves reading the value, checking for a null value, attempting to convert it to the appropriate type, checking whether the conversion was successful, and finally, using the value in the query.</span></span> <span data-ttu-id="fe244-127">데이터 액세스 논리에 대 한 모든 권한을 유지 해야 하는 경우이 방법을 사용 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-127">You would use this approach when you need to retain full control over your data-access logic.</span></span>

### <a name="using-model-binding-to-bind-data"></a><span data-ttu-id="fe244-128">데이터 바인딩 모델을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="fe244-128">Using Model Binding to Bind Data</span></span>

<span data-ttu-id="fe244-129">모델 바인딩을 사용 하 여 훨씬 적은 코드를 사용 하 여 결과 바인딩할 수 있도록 하 고 기능을 응용 프로그램 전체에서 재사용할 수 있는 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-129">Using model binding allows you to bind results using far less code and gives you the ability to reuse the functionality throughout your application.</span></span> <span data-ttu-id="fe244-130">모델 바인딩 풍부 하 고 데이터 바인딩 프레임 워크의 혜택을 유지 하면서 코드에 초점을 맞춘 데이터 액세스 논리를 사용 하 여 작업을 단순화 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-130">Model binding aims to simplify working with code-focused data-access logic while still retaining the benefits of a rich, data-binding framework.</span></span>

## <a name="displaying-products"></a><span data-ttu-id="fe244-131">제품 표시</span><span class="sxs-lookup"><span data-stu-id="fe244-131">Displaying Products</span></span>

<span data-ttu-id="fe244-132">이 자습서에서는 데이터를 바인딩할 모델 바인딩을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-132">In this tutorial, you'll use model binding to bind data.</span></span> <span data-ttu-id="fe244-133">컨트롤의 모델 바인딩을 사용 하 여 데이터를 선택 하도록 데이터 컨트롤을 구성 하려면 설정 `SelectMethod` 속성 페이지의 코드에 있는 메서드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-133">To configure a data control to use model binding to select data, you set the control's `SelectMethod` property to the name of a method in the page's code.</span></span> <span data-ttu-id="fe244-134">데이터 컨트롤의 페이지 수명 주기의 적절 한 시간에 메서드를 호출 하 고 자동으로 반환된 된 데이터를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-134">The data control calls the method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="fe244-135">명시적으로 호출 하지 않아도 됩니다는 `DataBind` 메서드.</span><span class="sxs-lookup"><span data-stu-id="fe244-135">There's no need to explicitly call the `DataBind` method.</span></span>

<span data-ttu-id="fe244-136">아래 단계를 사용 하는 태그를 수정 하겠습니다 합니다 *ProductList.aspx* 페이지 페이지는 제품을 표시할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-136">Using the steps below, you'll modify the markup in the *ProductList.aspx* page so that the page can display products.</span></span>

1. <span data-ttu-id="fe244-137">**솔루션 탐색기**오픈 합니다 *ProductList.aspx* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-137">In **Solution Explorer**, open the *ProductList.aspx* page.</span></span>
2. <span data-ttu-id="fe244-138">기존 태그를 다음 태그로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-138">Replace the existing markup with the following markup:</span></span>   

    [!code-aspx[Main](display_data_items_and_details/samples/sample1.aspx)]

<span data-ttu-id="fe244-139">이 코드는 사용을 **ListView** 는 제품을 전시 하기 "productList" 라는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-139">This code uses a **ListView** control named "productList" to display the products.</span></span>

[!code-aspx[Main](display_data_items_and_details/samples/sample2.aspx)]

<span data-ttu-id="fe244-140">합니다 **ListView** 컨트롤 템플릿 및 스타일을 사용 하 여 정의 하는 형식으로 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-140">The **ListView** control displays data in a format that you define by using templates and styles.</span></span> <span data-ttu-id="fe244-141">모든 반복 구조에서 데이터에 대 한 두는 것이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-141">It is useful for data in any repeating structure.</span></span> <span data-ttu-id="fe244-142">그러나 이렇게 **ListView** 예제 데이터베이스, 사용자가 편집, 삽입 및 데이터를 삭제 하 고 정렬 설정할 수 있습니다. 및 코드 없이 페이지 데이터를 데이터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-142">This **ListView** example simply shows data from the database, however you can enable users to edit, insert, and delete data, and to sort and page data, all without code.</span></span>

<span data-ttu-id="fe244-143">설정 하 여는 `ItemType` 속성에는 **ListView** 컨트롤을 데이터 바인딩 식을 `Item` 수 컨트롤은 강력한 형식의.</span><span class="sxs-lookup"><span data-stu-id="fe244-143">By setting the `ItemType` property in the **ListView** control, the data-binding expression `Item` is available and the control becomes strongly typed.</span></span> <span data-ttu-id="fe244-144">이전 자습서에서 설명 했 듯이 지정 하는 등, IntelliSense를 사용 하는 항목 개체의 세부 정보를 선택할 수 있습니다는 `ProductName`:</span><span class="sxs-lookup"><span data-stu-id="fe244-144">As mentioned in the previous tutorial, you can select details of the Item object using IntelliSense, such as specifying the `ProductName`:</span></span>

![데이터를 표시할 항목 및 세부 정보-IntelliSense](display_data_items_and_details/_static/image1.png)

<span data-ttu-id="fe244-146">모델 바인딩을 사용 하 여 지정 하는 또한는 `SelectMethod` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-146">In addition, you are using model binding to specify a `SelectMethod` value.</span></span> <span data-ttu-id="fe244-147">이 값 (`GetProducts`) 다음 단계에서 제품을 전시 하기 코드 숨김에 추가 되는 메서드에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-147">This value (`GetProducts`) will correspond to the method that you will add to the code behind to display products in the next step.</span></span>

### <a name="adding-code-to-display-products"></a><span data-ttu-id="fe244-148">제품을 표시 하는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-148">Adding Code to Display Products</span></span>

<span data-ttu-id="fe244-149">이 단계에서는 채우는 코드를 추가 합니다 **ListView** 데이터베이스에서 제품 데이터를 사용 하 여 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-149">In this step, you'll add code to populate the **ListView** control with product data from the database.</span></span> <span data-ttu-id="fe244-150">코드는 모든 제품을 보여 주는 뿐만 아니라 개별 범주를 보여 주는 제품을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-150">The code will support showing products by individual category, as well as showing all products.</span></span>

1. <span data-ttu-id="fe244-151">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *ProductList.aspx* 을 클릭 한 다음 **코드 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-151">In **Solution Explorer**, right-click *ProductList.aspx* and then click **View Code**.</span></span>
2. <span data-ttu-id="fe244-152">기존 코드를 대체 합니다 *ProductList.aspx.cs* 를 다음 코드로 파일:</span><span class="sxs-lookup"><span data-stu-id="fe244-152">Replace the existing code in the *ProductList.aspx.cs* file with the following code:</span></span>   

    [!code-csharp[Main](display_data_items_and_details/samples/sample3.cs)]

<span data-ttu-id="fe244-153">보여 주는이 코드를 `GetProducts` 에서 참조 되는 메서드를 `ItemType` 의 속성을 **ListView** 에서 제어할를 *ProductList.aspx* 페이지.</span><span class="sxs-lookup"><span data-stu-id="fe244-153">This code shows the `GetProducts` method that's referenced by the `ItemType` property of the **ListView** control in the *ProductList.aspx* page.</span></span> <span data-ttu-id="fe244-154">데이터베이스의 특정 범주에 결과 제한 하려면이 코드는 다음과 같이 설정 됩니다.는 `categoryId` 전달할 쿼리 문자열 값에서 값을 *ProductList.aspx* 때 페이지를 *ProductList.aspx* 페이지 탐색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-154">To limit the results to a specific category in the database, the code sets the `categoryId` value from the query string value passed to the *ProductList.aspx* page when the *ProductList.aspx* page is navigated to.</span></span> <span data-ttu-id="fe244-155">합니다 `QueryStringAttribute` 클래스는 `System.Web.ModelBinding` 네임 스페이스는 쿼리 문자열 변수 id의 값을 검색 하는 데 사용 됩니다. 이렇게 하면 모델 바인딩을에 쿼리 문자열에서 값을 바인딩하려는 `categoryId` 런타임에 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-155">The `QueryStringAttribute` class in the `System.Web.ModelBinding` namespace is used to retrieve the value of the query string variable id. This instructs model binding to try to bind a value from the query string to the `categoryId` parameter at run time.</span></span>

<span data-ttu-id="fe244-156">유효한 범주를이 페이지에 쿼리 문자열로 전달 되 면 쿼리 결과가 일치 하는 데이터베이스에서 해당 제품에만 국한 된 `categoryId` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-156">When a valid category is passed as a query string to the page, the results of the query are limited to those products in the database that match the `categoryId` value.</span></span> <span data-ttu-id="fe244-157">예를 들어 경우 URL을 *ProductsList.aspx* 페이지에는 다음과 같습니다:</span><span class="sxs-lookup"><span data-stu-id="fe244-157">For instance, if the URL to the *ProductsList.aspx* page is the following:</span></span>

[!code-console[Main](display_data_items_and_details/samples/sample4.cmd)]

<span data-ttu-id="fe244-158">페이지에는 제품 데이터만 표시 됩니다. 여기서는 `category` equals `1`합니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-158">The page displays only the products where the `category` equals `1`.</span></span>

<span data-ttu-id="fe244-159">탐색 하는 경우 포함 된 쿼리 문자열이 없는 경우는 *ProductList.aspx* 페이지에서 모든 제품 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-159">If no query string is included when navigating to the *ProductList.aspx* page, all products will be displayed.</span></span>

<span data-ttu-id="fe244-160">이러한 메서드에 대 한 값의 원본으로 참조 됩니다 *공급자 값* (같은 *QueryString*)를 사용 하는 값 공급자를 나타내는 매개 변수 특성 값으로 참조 되 고 공급자 특성 (같은 "`id`").</span><span class="sxs-lookup"><span data-stu-id="fe244-160">The sources of values for these methods are referred to as *value providers* (such as *QueryString*), and the parameter attributes that indicate which value provider to use are referred to as value provider attributes (such as "`id`").</span></span> <span data-ttu-id="fe244-161">ASP.NET은 Web Forms 응용 프로그램에서 쿼리 문자열, 쿠키, 폼 값, 컨트롤, 상태 보기, 세션 상태 및 프로필 속성과 같은 값 공급자 및 모든 사용자 입력의 일반적인 원본에 대 한 해당 특성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-161">ASP.NET includes value providers and corresponding attributes for all of the typical sources of user input in a Web Forms application, such as the query string, cookies, form values, controls, view state, session state, and profile properties.</span></span> <span data-ttu-id="fe244-162">또한 사용자 지정 값 공급자를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-162">You can also write custom value providers.</span></span>

### <a name="running-the-application"></a><span data-ttu-id="fe244-163">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="fe244-163">Running the Application</span></span>

<span data-ttu-id="fe244-164">모든 제품 또는 제품 범주별으로 제한 된 집합을 보는 방법을 보려면 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-164">Run the application now to see how you can view all of the products or just a set of products limited by category.</span></span>

1. <span data-ttu-id="fe244-165">에 **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 *Default.aspx* 페이지를 선택 **브라우저에서 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-165">In the **Solution Explorer**, right-click the *Default.aspx* page and select **View in Browser**.</span></span>  
 <span data-ttu-id="fe244-166">브라우저를 열고 표시 합니다 *Default.aspx* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-166">The browser will open and show the *Default.aspx* page.</span></span>
2. <span data-ttu-id="fe244-167">선택 **자동차** 제품 범주 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-167">Select **Cars** from the product category navigation menu.</span></span>  
 <span data-ttu-id="fe244-168">합니다 *ProductList.aspx* "자동차" 범주에 포함 된 제품만 보여 주는 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-168">The *ProductList.aspx* page is displayed showing only products included in the "Cars" category.</span></span> <span data-ttu-id="fe244-169">이 자습서의 뒷부분에서 제품 세부 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-169">Later in this tutorial, you will display product details.</span></span>  

    ![데이터를 표시할 항목 및 세부 정보-자동차](display_data_items_and_details/_static/image2.png)
3. <span data-ttu-id="fe244-171">선택 **제품** 맨 위에 있는 탐색 메뉴에서.</span><span class="sxs-lookup"><span data-stu-id="fe244-171">Select **Products** from the navigation menu at the top.</span></span>  
 <span data-ttu-id="fe244-172">하지만 마찬가지로 합니다 *ProductList.aspx* 이 이번 제품의 전체 목록을 표시 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-172">Again, the *ProductList.aspx* page is displayed, however this time it shows the entire list of products.</span></span>   

    ![데이터를 표시할 항목 및 세부 정보-제품](display_data_items_and_details/_static/image3.png)
4. <span data-ttu-id="fe244-174">브라우저를 닫고 Visual Studio로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-174">Close the browser and return to Visual Studio.</span></span>

### <a name="adding-a-data-control-to-display-product-details"></a><span data-ttu-id="fe244-175">제품 세부 정보를 표시 하는 데이터 컨트롤 추가</span><span class="sxs-lookup"><span data-stu-id="fe244-175">Adding a Data Control to Display Product Details</span></span>

<span data-ttu-id="fe244-176">다음으로 태그를 수정 합니다 *ProductDetails.aspx* 페이지 개별 제품에 대 한 정보를 표시할 수 있도록 이전 자습서에서 추가한 페이지.</span><span class="sxs-lookup"><span data-stu-id="fe244-176">Next, you'll modify the markup in the *ProductDetails.aspx* page that you added in the previous tutorial so that the page can display information about an individual product.</span></span>

1. <span data-ttu-id="fe244-177">**솔루션 탐색기**오픈 합니다 *ProductDetails.aspx* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-177">In **Solution Explorer**, open the *ProductDetails.aspx* page.</span></span>
2. <span data-ttu-id="fe244-178">기존 태그를 다음 태그로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-178">Replace the existing markup with the following markup:</span></span>   

    [!code-aspx[Main](display_data_items_and_details/samples/sample5.aspx)]

<span data-ttu-id="fe244-179">이 코드를 사용 하는 **FormView** 개별 제품에 대 한 세부 정보를 표시 하는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-179">This code uses a **FormView** control to display details about an individual product.</span></span> <span data-ttu-id="fe244-180">이 태그에 데이터를 표시 하는 데 사용 되는 것과 같은 메서드를 사용 합니다 *ProductList.aspx* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-180">This markup uses methods like those that are used to display data in the *ProductList.aspx* page.</span></span> <span data-ttu-id="fe244-181">합니다 **FormView** 컨트롤은 데이터 원본에서 한 번에 하나의 레코드를 표시 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-181">The **FormView** control is used to display a single record at a time from a data source.</span></span> <span data-ttu-id="fe244-182">사용 하는 경우는 **FormView** 컨트롤을 만든 템플릿을 표시 하 고 데이터 바인딩된 값을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-182">When you use the **FormView** control, you create templates to display and edit data-bound values.</span></span> <span data-ttu-id="fe244-183">템플릿 컨트롤을 포함할 바인딩 식 및 서식 지정 모양 및 폼의 기능을 정의 하는.</span><span class="sxs-lookup"><span data-stu-id="fe244-183">The templates contain controls, binding expressions, and formatting that define the look and functionality of the form.</span></span>

<span data-ttu-id="fe244-184">위의 태그는 데이터베이스에 연결 하려면 추가 코드를 추가 해야 합니다 *ProductDetails.aspx* 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-184">To connect the above markup to the database, you must add additional code to the *ProductDetails.aspx* code.</span></span>

1. <span data-ttu-id="fe244-185">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *ProductDetails.aspx* 을 클릭 한 다음 **코드 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-185">In **Solution Explorer**, right-click *ProductDetails.aspx* and then click **View Code**.</span></span>  
   <span data-ttu-id="fe244-186">합니다 *ProductDetails.aspx.cs* 파일이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-186">The *ProductDetails.aspx.cs* file will be displayed.</span></span>
2. <span data-ttu-id="fe244-187">기존 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-187">Replace the existing code with the following code:</span></span>   

    [!code-csharp[Main](display_data_items_and_details/samples/sample6.cs)]

<span data-ttu-id="fe244-188">이 코드는 검사는 "`productID`" 쿼리 문자열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-188">This code checks for a "`productID`" query-string value.</span></span> <span data-ttu-id="fe244-189">유효한 쿼리 문자열 값이 있으면 일치 하는 제품이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-189">If a valid query-string value is found, the matching product is displayed.</span></span> <span data-ttu-id="fe244-190">쿼리 문자열이 없으면 없거나 쿼리 문자열 값이 유효 하지 않습니다, 없는 제품에 표시 됩니다는 *ProductDetails.aspx* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-190">If no query-string is found, or the query-string value is not valid, no product is displayed on the *ProductDetails.aspx* page.</span></span>

### <a name="running-the-application"></a><span data-ttu-id="fe244-191">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="fe244-191">Running the Application</span></span>

<span data-ttu-id="fe244-192">이제 응용 프로그램이 표시 하는 개별 제품을 실행할 수 있습니다 제품의 id에 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-192">Now you can run the application to see an individual product displayed based on the id of the product.</span></span>

1. <span data-ttu-id="fe244-193">키를 눌러 **F5** 응용 프로그램을 실행 하려면 Visual Studio에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-193">Press **F5** while in Visual Studio to run the application.</span></span>  
 <span data-ttu-id="fe244-194">브라우저를 열고 표시 합니다 *Default.aspx* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-194">The browser will open and show the *Default.aspx* page.</span></span>
2. <span data-ttu-id="fe244-195">범주 탐색 메뉴에서 "배"를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-195">Select "Boats" from the category navigation menu.</span></span>  
 <span data-ttu-id="fe244-196">합니다 *ProductList.aspx* 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-196">The *ProductList.aspx* page is displayed.</span></span>
3. <span data-ttu-id="fe244-197">제품 목록에서 "용지 재벌" 제품을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-197">Select the "Paper Boat" product from the product list.</span></span>  
 <span data-ttu-id="fe244-198">합니다 *ProductDetails.aspx* 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-198">The *ProductDetails.aspx* page is displayed.</span></span>   

    ![데이터를 표시할 항목 및 세부 정보-제품](display_data_items_and_details/_static/image4.png)
4. <span data-ttu-id="fe244-200">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-200">Close the browser.</span></span>

## <a name="summary"></a><span data-ttu-id="fe244-201">요약</span><span class="sxs-lookup"><span data-stu-id="fe244-201">Summary</span></span>

<span data-ttu-id="fe244-202">이 자습서 시리즈의 태그 및 제품 목록을 표시 하려면 제품 세부 정보를 표시 하는 코드를 추가할 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-202">In this tutorial of the series you have add markup and code to display a product list and to display product details.</span></span> <span data-ttu-id="fe244-203">이 과정에서 강력한 형식의 데이터 컨트롤, 모델 바인딩 및 값 공급자에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-203">During this process you have learned about strongly typed data controls, model binding, and value providers.</span></span> <span data-ttu-id="fe244-204">다음 자습서에서는 Wingtip Toys 샘플 응용 프로그램에 쇼핑 카트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe244-204">In the next tutorial, you'll add a shopping cart to the Wingtip Toys sample application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fe244-205">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="fe244-205">Additional Resources</span></span>

[<span data-ttu-id="fe244-206">모델 바인딩 및 web forms를 사용 하 여 데이터 검색 및 표시</span><span class="sxs-lookup"><span data-stu-id="fe244-206">Retrieving and displaying data with model binding and web forms</span></span>](../../presenting-and-managing-data/model-binding/retrieving-data.md)

> [!div class="step-by-step"]
> <span data-ttu-id="fe244-207">[이전](ui_and_navigation.md)
> [다음](shopping-cart.md)</span><span class="sxs-lookup"><span data-stu-id="fe244-207">[Previous](ui_and_navigation.md)
[Next](shopping-cart.md)</span></span>
