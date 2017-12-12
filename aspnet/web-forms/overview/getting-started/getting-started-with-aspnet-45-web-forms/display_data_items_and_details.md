---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
title: "데이터 표시 항목 및 세부 정보 | Microsoft Docs"
author: Erikre
description: "이 자습서 시리즈 것에 대 한 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 구축 하는 기초 알려 드리겠습니다 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/08/2014
ms.topic: article
ms.assetid: 64a491a8-0ed6-4c2f-9c1c-412962eb6006
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
msc.type: authoredcontent
ms.openlocfilehash: 809d7a9c21a3ddf5dfd07d079eb8fe0d1d81712d
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="display-data-items-and-details"></a><span data-ttu-id="e6146-103">데이터 표시 항목 및 세부 정보</span><span class="sxs-lookup"><span data-stu-id="e6146-103">Display Data Items and Details</span></span>
====================
<span data-ttu-id="e6146-104">으로 [Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="e6146-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="e6146-105">[Wingtip Toys 샘플 프로젝트 (C#)를 다운로드](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자책 (PDF)를 다운로드 합니다.](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="e6146-105">[Download Wingtip Toys Sample Project (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="e6146-106">이 자습서 시리즈 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 웹에 대 한 ASP.NET Web Forms 응용 프로그램을 구축 하는 기초 알려 드리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="e6146-107">Visual Studio 2013 [C# 소스 코드를 사용 하 여 프로젝트](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 이 자습서 시리즈를 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>


<span data-ttu-id="e6146-108">이 자습서에서는 데이터 항목 및 ASP.NET Web Forms 및 Entity Framework Code First를 사용 하 여 데이터 항목 정보를 표시 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-108">This tutorial describes how to display data items and data item details using ASP.NET Web Forms and Entity Framework Code First.</span></span> <span data-ttu-id="e6146-109">이 자습서에서는 이전 자습서 "UI 및 탐색"를 바탕으로 하며 Wingtip 장난감 저장소 자습서 시리즈의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-109">This tutorial builds on the previous tutorial "UI and Navigation" and is part of the Wingtip Toy Store tutorial series.</span></span> <span data-ttu-id="e6146-110">이 자습서를 완료 하면 수에 제품을 볼 수는 *ProductsList.aspx* 페이지 및 개별 제품에 대 한 세부 정보는 *ProductDetails.aspx* 페이지.</span><span class="sxs-lookup"><span data-stu-id="e6146-110">When you've completed this tutorial, you'll be able to see products on the *ProductsList.aspx* page and details about an individual product on the *ProductDetails.aspx* page.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="e6146-111">학습 내용:</span><span class="sxs-lookup"><span data-stu-id="e6146-111">What you'll learn:</span></span>

- <span data-ttu-id="e6146-112">데이터베이스에서 제품을 표시 하는 데이터 컨트롤을 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-112">How to add a data control to display products from the database.</span></span>
- <span data-ttu-id="e6146-113">선택한 데이터에 데이터 컨트롤을 연결 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="e6146-113">How to connect a data control to the selected data.</span></span>
- <span data-ttu-id="e6146-114">데이터베이스에서 제품 세부 정보를 표시 하는 데이터 컨트롤을 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-114">How to add a data control to display product details from the database.</span></span>
- <span data-ttu-id="e6146-115">쿼리 문자열에서 값을 검색 값을 사용 하는 데이터베이스에서 검색 된 데이터를 제한 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="e6146-115">How to retrieve a value from the query string and use that value to limit the data that's retrieved from the database.</span></span>

### <a name="these-are-the-features-introduced-in-the-tutorial"></a><span data-ttu-id="e6146-116">다음은 자습서에 도입 된 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-116">These are the features introduced in the tutorial:</span></span>

- <span data-ttu-id="e6146-117">모델 바인딩</span><span class="sxs-lookup"><span data-stu-id="e6146-117">Model Binding</span></span>
- <span data-ttu-id="e6146-118">값 공급자</span><span class="sxs-lookup"><span data-stu-id="e6146-118">Value providers</span></span>

## <a name="adding-a-data-control-to-display-products"></a><span data-ttu-id="e6146-119">제품을 전시 하기 데이터 컨트롤 추가</span><span class="sxs-lookup"><span data-stu-id="e6146-119">Adding a Data Control to Display Products</span></span>

<span data-ttu-id="e6146-120">서버 컨트롤에 데이터를 바인딩할 때 사용할 수는 몇 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-120">When binding data to a server control, there are a few different options you can use.</span></span> <span data-ttu-id="e6146-121">가장 일반적인 옵션에는 데이터 소스 컨트롤을 추가, 코드를 수동으로 추가 또는 모델 바인딩을 사용 하 여 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-121">The most common options include adding a data source control, adding code by hand, or using model binding.</span></span>

### <a name="using-a-data-source-control-to-bind-data"></a><span data-ttu-id="e6146-122">데이터 소스 제어를 사용 하 여 데이터를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-122">Using a Data Source Control to Bind Data</span></span>

<span data-ttu-id="e6146-123">데이터 소스 제어에 추가 데이터를 표시 하는 컨트롤에 데이터 소스 제어를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-123">Adding a data source control allows you to link the data source control to the control that displays the data.</span></span> <span data-ttu-id="e6146-124">이 방법을 프로그래밍 방식을 사용 하지 않고 데이터 원본에 직접 서버 쪽 컨트롤을 선언적으로 연결할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-124">This approach allows you to declaratively connect server-side controls directly to data sources, rather than using a programmatic approach.</span></span>

### <a name="coding-by-hand-to-bind-data"></a><span data-ttu-id="e6146-125">데이터를 바인딩하려면 직접 코딩</span><span class="sxs-lookup"><span data-stu-id="e6146-125">Coding By Hand to Bind Data</span></span>

<span data-ttu-id="e6146-126">추가 코드가 직접 관련 값을 읽기, null 값을 확인, 적절 한 형식으로 변환 하는 동안은 변환이 성공 했는지 여부를 확인 및 마지막으로, 쿼리에서 값을 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-126">Adding code by hand involves reading the value, checking for a null value, attempting to convert it to the appropriate type, checking whether the conversion was successful, and finally, using the value in the query.</span></span> <span data-ttu-id="e6146-127">데이터 액세스 논리에 대 한 모든 권한을 유지 해야 할 경우이 방법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-127">You would use this approach when you need to retain full control over your data-access logic.</span></span>

### <a name="using-model-binding-to-bind-data"></a><span data-ttu-id="e6146-128">데이터를 바인딩하려면 바인딩 모델을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e6146-128">Using Model Binding to Bind Data</span></span>

<span data-ttu-id="e6146-129">모델 바인딩을 사용 하 여 훨씬 더 적은 코드를 사용 하 여 결과 바인딩할 수 있도록 하 고 응용 프로그램 전체에서 기능을 다시 사용할 수 있는 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-129">Using model binding allows you to bind results using far less code and gives you the ability to reuse the functionality throughout your application.</span></span> <span data-ttu-id="e6146-130">모델 바인딩은 풍부한, 데이터 바인딩 프레임 워크의 혜택을 유지 하면서 데이터 액세스 코드 중심 논리로 작업을 단순화 시키기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-130">Model binding aims to simplify working with code-focused data-access logic while still retaining the benefits of a rich, data-binding framework.</span></span>

## <a name="displaying-products"></a><span data-ttu-id="e6146-131">제품 표시</span><span class="sxs-lookup"><span data-stu-id="e6146-131">Displaying Products</span></span>

<span data-ttu-id="e6146-132">이 자습서에서는 데이터를 바인딩할 모델 바인딩을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-132">In this tutorial, you'll use model binding to bind data.</span></span> <span data-ttu-id="e6146-133">컨트롤의 데이터를 선택 하려면 모델 바인딩을 사용 하도록 데이터 제어를 구성 하려면 설정 `SelectMethod` 속성 페이지의 코드에 있는 메서드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-133">To configure a data control to use model binding to select data, you set the control's `SelectMethod` property to the name of a method in the page's code.</span></span> <span data-ttu-id="e6146-134">데이터 컨트롤 페이지 수명 주기의 적절 한 시간에 메서드를 호출 하 고 자동으로 반환된 된 데이터를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-134">The data control calls the method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="e6146-135">명시적으로 호출할 필요가 없습니다는 `DataBind` 메서드.</span><span class="sxs-lookup"><span data-stu-id="e6146-135">There's no need to explicitly call the `DataBind` method.</span></span>

<span data-ttu-id="e6146-136">다음 단계를 사용 하 여에서 태그를 수정 합니다는 *ProductList.aspx* 페이지의 페이지는 제품을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-136">Using the steps below, you'll modify the markup in the *ProductList.aspx* page so that the page can display products.</span></span>

1. <span data-ttu-id="e6146-137">**솔루션 탐색기**열고는 *ProductList.aspx* 페이지.</span><span class="sxs-lookup"><span data-stu-id="e6146-137">In **Solution Explorer**, open the *ProductList.aspx* page.</span></span>
2. <span data-ttu-id="e6146-138">기존 태그를 다음 태그로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-138">Replace the existing markup with the following markup:</span></span>   

    [!code-aspx[Main](display_data_items_and_details/samples/sample1.aspx)]

<span data-ttu-id="e6146-139">사용 하 여이 코드는 **ListView** 는 제품을 전시 하기 "productList" 라는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-139">This code uses a **ListView** control named "productList" to display the products.</span></span>

[!code-aspx[Main](display_data_items_and_details/samples/sample2.aspx)]

<span data-ttu-id="e6146-140">**ListView** 컨트롤 템플릿 및 스타일을 사용 하 여 정의 하는 형식에 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-140">The **ListView** control displays data in a format that you define by using templates and styles.</span></span> <span data-ttu-id="e6146-141">모든 반복 구조에서 데이터에는 것이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-141">It is useful for data in any repeating structure.</span></span> <span data-ttu-id="e6146-142">하지만이 **ListView** 예제 데이터는 데이터베이스, 사용자가 편집, 삽입 및 데이터를 삭제 하 고 정렬에 사용할 수 있습니다 및 코드 없이 모두 페이지 데이터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-142">This **ListView** example simply shows data from the database, however you can enable users to edit, insert, and delete data, and to sort and page data, all without code.</span></span>

<span data-ttu-id="e6146-143">설정 하 여는 `ItemType` 속성에는 **ListView** 제어, 데이터 바인딩 식을 `Item` ´ ï ´ 컨트롤은 강력한 형식의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-143">By setting the `ItemType` property in the **ListView** control, the data-binding expression `Item` is available and the control becomes strongly typed.</span></span> <span data-ttu-id="e6146-144">이전 자습서에서 설명 했 듯이 IntelliSense를 사용 하 여 지정 하는 등 항목 개체의 세부 정보를 선택할 수 있습니다는 `ProductName`:</span><span class="sxs-lookup"><span data-stu-id="e6146-144">As mentioned in the previous tutorial, you can select details of the Item object using IntelliSense, such as specifying the `ProductName`:</span></span>

![데이터 표시 항목 및 세부 정보-IntelliSense](display_data_items_and_details/_static/image1.png)

<span data-ttu-id="e6146-146">모델 바인딩을 사용 하 여 지정할 수는 또한는 `SelectMethod` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-146">In addition, you are using model binding to specify a `SelectMethod` value.</span></span> <span data-ttu-id="e6146-147">이 값 (`GetProducts`) 메서드를 다음 단계에서 제품을 표시 하는 코드 숨김에 추가 합니다에 해당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-147">This value (`GetProducts`) will correspond to the method that you will add to the code behind to display products in the next step.</span></span>

### <a name="adding-code-to-display-products"></a><span data-ttu-id="e6146-148">제품을 표시 하는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-148">Adding Code to Display Products</span></span>

<span data-ttu-id="e6146-149">이 단계에서는 채우는 코드를 추가 합니다는 **ListView** 컨트롤에 데이터베이스에서 제품 데이터.</span><span class="sxs-lookup"><span data-stu-id="e6146-149">In this step, you'll add code to populate the **ListView** control with product data from the database.</span></span> <span data-ttu-id="e6146-150">코드는 모든 제품을 표시 뿐만 아니라 개별 범주에서 보여 주는 제품을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-150">The code will support showing products by individual category, as well as showing all products.</span></span>

1. <span data-ttu-id="e6146-151">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *ProductList.aspx* 클릭 하 고 **코드 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-151">In **Solution Explorer**, right-click *ProductList.aspx* and then click **View Code**.</span></span>
2. <span data-ttu-id="e6146-152">기존 코드는 *ProductList.aspx.cs* 를 다음 코드로 파일:</span><span class="sxs-lookup"><span data-stu-id="e6146-152">Replace the existing code in the *ProductList.aspx.cs* file with the following code:</span></span>   

    [!code-csharp[Main](display_data_items_and_details/samples/sample3.cs)]

<span data-ttu-id="e6146-153">보여 주는이 코드는 `GetProducts` 에서 참조 되는 메서드는 `ItemType` 의 속성은 **ListView** 컨트롤에 *ProductList.aspx* 페이지.</span><span class="sxs-lookup"><span data-stu-id="e6146-153">This code shows the `GetProducts` method that's referenced by the `ItemType` property of the **ListView** control in the *ProductList.aspx* page.</span></span> <span data-ttu-id="e6146-154">데이터베이스의 특정 범주에 결과 제한 하려면이 코드는 다음과 같이 설정 됩니다.는 `categoryId` 전달 되는 쿼리 문자열 값의 값은 *ProductList.aspx* 때 페이지는 *ProductList.aspx* 페이지는 이동 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-154">To limit the results to a specific category in the database, the code sets the `categoryId` value from the query string value passed to the *ProductList.aspx* page when the *ProductList.aspx* page is navigated to.</span></span> <span data-ttu-id="e6146-155">`QueryStringAttribute` 클래스에 `System.Web.ModelBinding` 네임 스페이스는 쿼리 문자열 변수 id의 값을 검색 하는 데 사용 됩니다. 이렇게 하면 모델을 쿼리 문자열에서 값을 연결할 하려고을 바인딩하는 `categoryId` 실행 시 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-155">The `QueryStringAttribute` class in the `System.Web.ModelBinding` namespace is used to retrieve the value of the query string variable id. This instructs model binding to try to bind a value from the query string to the `categoryId` parameter at run time.</span></span>

<span data-ttu-id="e6146-156">쿼리 결과 일치 하는 데이터베이스에서 해당 제품으로 제한 됩니다 올바른 범주에는 페이지에 쿼리 문자열로 전달 되는 `categoryId` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-156">When a valid category is passed as a query string to the page, the results of the query are limited to those products in the database that match the `categoryId` value.</span></span> <span data-ttu-id="e6146-157">예를 들어, 하는 경우 URL은 *ProductsList.aspx* 페이지는 다음:</span><span class="sxs-lookup"><span data-stu-id="e6146-157">For instance, if the URL to the *ProductsList.aspx* page is the following:</span></span>

[!code-console[Main](display_data_items_and_details/samples/sample4.cmd)]

<span data-ttu-id="e6146-158">페이지에는 제품의 데이터만 표시 됩니다. 여기서는 `category` equals `1`합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-158">The page displays only the products where the `category` equals `1`.</span></span>

<span data-ttu-id="e6146-159">탐색 하는 경우 포함 된 쿼리 문자열이 없는 경우는 *ProductList.aspx* 페이지, 모든 제품을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-159">If no query string is included when navigating to the *ProductList.aspx* page, all products will be displayed.</span></span>

<span data-ttu-id="e6146-160">이러한 방법에 대 한 값의 소스는 라고 *값 공급자* (같은 *QueryString*)를 사용 하는 값 공급자를 나타내는 매개 변수 특성 값으로 참조 되 고 공급자 특성 (예: "`id`").</span><span class="sxs-lookup"><span data-stu-id="e6146-160">The sources of values for these methods are referred to as *value providers* (such as *QueryString*), and the parameter attributes that indicate which value provider to use are referred to as value provider attributes (such as "`id`").</span></span> <span data-ttu-id="e6146-161">ASP.NET은 Web Forms 응용 프로그램의 쿼리 문자열, 쿠키, 폼 값, 컨트롤와 같은 뷰 상태, 세션 상태 프로필 속성에 값 공급자 및 모든 사용자 입력의 일반적인 원본에 대 한 해당 특성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-161">ASP.NET includes value providers and corresponding attributes for all of the typical sources of user input in a Web Forms application, such as the query string, cookies, form values, controls, view state, session state, and profile properties.</span></span> <span data-ttu-id="e6146-162">사용자 지정 값 공급자를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-162">You can also write custom value providers.</span></span>

### <a name="running-the-application"></a><span data-ttu-id="e6146-163">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="e6146-163">Running the Application</span></span>

<span data-ttu-id="e6146-164">모든 제품 또는 제품 범주별으로 제한 된 집합에만 볼 수는 어떻게 볼 수 있는 지금 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-164">Run the application now to see how you can view all of the products or just a set of products limited by category.</span></span>

1. <span data-ttu-id="e6146-165">에 **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 *Default.aspx* 페이지로 돌아간 후 선택 **브라우저에서 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-165">In the **Solution Explorer**, right-click the *Default.aspx* page and select **View in Browser**.</span></span>  
 <span data-ttu-id="e6146-166">브라우저가 열리고 표시는 *Default.aspx* 페이지.</span><span class="sxs-lookup"><span data-stu-id="e6146-166">The browser will open and show the *Default.aspx* page.</span></span>
2. <span data-ttu-id="e6146-167">선택 **자동차** 제품 범주 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-167">Select **Cars** from the product category navigation menu.</span></span>  
 <span data-ttu-id="e6146-168">*ProductList.aspx* "Cars" 범주에 포함 된 제품만 표시 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-168">The *ProductList.aspx* page is displayed showing only products included in the "Cars" category.</span></span> <span data-ttu-id="e6146-169">이 자습서의 뒷부분에 나오는 제품 세부 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-169">Later in this tutorial, you will display product details.</span></span>  

    ![데이터 표시 항목 및 세부 정보-자동차](display_data_items_and_details/_static/image2.png)
3. <span data-ttu-id="e6146-171">선택 **제품** 위쪽에 있는 탐색 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-171">Select **Products** from the navigation menu at the top.</span></span>  
 <span data-ttu-id="e6146-172">다시,는 *ProductList.aspx* 페이지가 표시 되어 있지만이 현재 제품의 전체 목록을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-172">Again, the *ProductList.aspx* page is displayed, however this time it shows the entire list of products.</span></span>   

    ![데이터 표시 항목 및 세부 정보-제품](display_data_items_and_details/_static/image3.png)
4. <span data-ttu-id="e6146-174">브라우저를 닫고 Visual Studio로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-174">Close the browser and return to Visual Studio.</span></span>

### <a name="adding-a-data-control-to-display-product-details"></a><span data-ttu-id="e6146-175">제품 세부 정보를 표시 하는 데이터 컨트롤 추가</span><span class="sxs-lookup"><span data-stu-id="e6146-175">Adding a Data Control to Display Product Details</span></span>

<span data-ttu-id="e6146-176">태그를 수정 하면서 간단한 다음으로 *ProductDetails.aspx* 페이지 개별 제품에 대 한 정보를 표시할 수 있도록 이전 자습서에서 추가한 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-176">Next, you'll modify the markup in the *ProductDetails.aspx* page that you added in the previous tutorial so that the page can display information about an individual product.</span></span>

1. <span data-ttu-id="e6146-177">**솔루션 탐색기**열고는 *ProductDetails.aspx* 페이지.</span><span class="sxs-lookup"><span data-stu-id="e6146-177">In **Solution Explorer**, open the *ProductDetails.aspx* page.</span></span>
2. <span data-ttu-id="e6146-178">기존 태그를 다음 태그로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-178">Replace the existing markup with the following markup:</span></span>   

    [!code-aspx[Main](display_data_items_and_details/samples/sample5.aspx)]

<span data-ttu-id="e6146-179">이 코드에서는 사용 된 **FormView** 컨트롤을 개별 제품에 대 한 세부 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-179">This code uses a **FormView** control to display details about an individual product.</span></span> <span data-ttu-id="e6146-180">에 데이터를 표시 하는 데 사용 되는 것과 같은 메서드를 사용 하는이 태그는 *ProductList.aspx* 페이지.</span><span class="sxs-lookup"><span data-stu-id="e6146-180">This markup uses methods like those that are used to display data in the *ProductList.aspx* page.</span></span> <span data-ttu-id="e6146-181">**FormView** 컨트롤은 데이터 원본에서 한 번에 하나의 레코드를 표시 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-181">The **FormView** control is used to display a single record at a time from a data source.</span></span> <span data-ttu-id="e6146-182">사용 하는 경우는 **FormView** 컨트롤을 만들면 템플릿을 표시 하 고 데이터 바인딩된 값을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-182">When you use the **FormView** control, you create templates to display and edit data-bound values.</span></span> <span data-ttu-id="e6146-183">템플릿을 컨트롤을 포함할 바인딩 식 및 서식을 모양 및 폼의 기능을 정의 하는.</span><span class="sxs-lookup"><span data-stu-id="e6146-183">The templates contain controls, binding expressions, and formatting that define the look and functionality of the form.</span></span>

<span data-ttu-id="e6146-184">위의 태그를 데이터베이스에 연결 하려면 추가 코드를 추가 해야는 *ProductDetails.aspx* 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-184">To connect the above markup to the database, you must add additional code to the *ProductDetails.aspx* code.</span></span>

1. <span data-ttu-id="e6146-185">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 *ProductDetails.aspx* 클릭 하 고 **코드 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-185">In **Solution Explorer**, right-click *ProductDetails.aspx* and then click **View Code**.</span></span>  
 <span data-ttu-id="e6146-186">*ProductDetails.aspx.cs* 파일이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-186">The *ProductDetails.aspx.cs* file will be displayed.</span></span>
2. <span data-ttu-id="e6146-187">기존 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-187">Replace the existing code with the following code:</span></span>   

    [!code-csharp[Main](display_data_items_and_details/samples/sample6.cs)]

<span data-ttu-id="e6146-188">이 코드는 검사는 "`productID`" 쿼리 문자열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-188">This code checks for a "`productID`" query-string value.</span></span> <span data-ttu-id="e6146-189">올바른 쿼리 문자열 값이 있으면 일치 하는 제품이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-189">If a valid query-string value is found, the matching product is displayed.</span></span> <span data-ttu-id="e6146-190">쿼리 문자열이 없으면 찾거나 쿼리 문자열 값이 올바르지 않습니다, 제품이 없으므로에 표시 됩니다는 *ProductDetails.aspx* 페이지.</span><span class="sxs-lookup"><span data-stu-id="e6146-190">If no query-string is found, or the query-string value is not valid, no product is displayed on the *ProductDetails.aspx* page.</span></span>

### <a name="running-the-application"></a><span data-ttu-id="e6146-191">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="e6146-191">Running the Application</span></span>

<span data-ttu-id="e6146-192">이제 표시 개별 제품을 확인 하려면 응용 프로그램을 실행할 수 있습니다는 제품의 id를 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-192">Now you can run the application to see an individual product displayed based on the id of the product.</span></span>

1. <span data-ttu-id="e6146-193">키를 눌러 **F5** 응용 프로그램을 실행 하려면 Visual Studio에 있는 동안 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-193">Press **F5** while in Visual Studio to run the application.</span></span>  
 <span data-ttu-id="e6146-194">브라우저가 열리고 표시는 *Default.aspx* 페이지.</span><span class="sxs-lookup"><span data-stu-id="e6146-194">The browser will open and show the *Default.aspx* page.</span></span>
2. <span data-ttu-id="e6146-195">범주 탐색 메뉴에서 "배"를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-195">Select "Boats" from the category navigation menu.</span></span>  
 <span data-ttu-id="e6146-196">*ProductList.aspx* 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-196">The *ProductList.aspx* page is displayed.</span></span>
3. <span data-ttu-id="e6146-197">제품 목록에서 "용지 보트" 제품을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-197">Select the "Paper Boat" product from the product list.</span></span>  
 <span data-ttu-id="e6146-198">*ProductDetails.aspx* 페이지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-198">The *ProductDetails.aspx* page is displayed.</span></span>   

    ![데이터 표시 항목 및 세부 정보-제품](display_data_items_and_details/_static/image4.png)
4. <span data-ttu-id="e6146-200">브라우저를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-200">Close the browser.</span></span>

## <a name="summary"></a><span data-ttu-id="e6146-201">요약</span><span class="sxs-lookup"><span data-stu-id="e6146-201">Summary</span></span>

<span data-ttu-id="e6146-202">이 자습서 시리즈의 태그 및 제품 목록을 표시 하 고 제품 세부 정보를 표시 하는 코드를 추가할 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-202">In this tutorial of the series you have add markup and code to display a product list and to display product details.</span></span> <span data-ttu-id="e6146-203">이 프로세스 중 강력한 형식의 데이터 컨트롤, 모델 바인딩 및 값 공급자에 대해 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-203">During this process you have learned about strongly typed data controls, model binding, and value providers.</span></span> <span data-ttu-id="e6146-204">다음 자습서에서는 쇼핑 카트 Wingtip Toys 샘플 응용 프로그램에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-204">In the next tutorial, you'll add a shopping cart to the Wingtip Toys sample application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e6146-205">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="e6146-205">Additional Resources</span></span>

[<span data-ttu-id="e6146-206">검색 및 모델 바인딩 및 web forms를 사용 하 여 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6146-206">Retrieving and displaying data with model binding and web forms</span></span>](../../presenting-and-managing-data/model-binding/retrieving-data.md)

>[!div class="step-by-step"]
<span data-ttu-id="e6146-207">[이전](ui_and_navigation.md)
[다음](shopping-cart.md)</span><span class="sxs-lookup"><span data-stu-id="e6146-207">[Previous](ui_and_navigation.md)
[Next](shopping-cart.md)</span></span>
