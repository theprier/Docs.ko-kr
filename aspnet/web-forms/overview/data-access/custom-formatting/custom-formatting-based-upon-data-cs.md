---
uid: web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-cs
title: "데이터 (C#)를 기반으로 사용자 지정 서식을 | Microsoft Docs"
author: rick-anderson
description: "GridView, DetailsView, 또는 데이터를 바인딩할 기반 FormView의 형식이 조정 하는 여러 가지 방법으로 수행할 수 있습니다. 이 자습서에서는 त ु म च l..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: 871a4574-f89c-4214-b786-79253ed3653b
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 606721b01fae34a7bce85d497a442cb110f1b51e
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="custom-formatting-based-upon-data-c"></a><span data-ttu-id="b2652-104">데이터 (C#)를 기반으로 사용자 지정 형식 지정</span><span class="sxs-lookup"><span data-stu-id="b2652-104">Custom Formatting Based Upon Data (C#)</span></span>
====================
<span data-ttu-id="b2652-105">으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="b2652-105">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

<span data-ttu-id="b2652-106">[샘플 앱을 다운로드](http://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_11_CS.exe) 또는 [PDF 다운로드](custom-formatting-based-upon-data-cs/_static/datatutorial11cs1.pdf)</span><span class="sxs-lookup"><span data-stu-id="b2652-106">[Download Sample App](http://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_11_CS.exe) or [Download PDF](custom-formatting-based-upon-data-cs/_static/datatutorial11cs1.pdf)</span></span>

> <span data-ttu-id="b2652-107">GridView, DetailsView, 또는 데이터를 바인딩할 기반 FormView의 형식이 조정 하는 여러 가지 방법으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-107">Adjusting the format of the GridView, DetailsView, or FormView based upon the data bound to it can be accomplished in multiple ways.</span></span> <span data-ttu-id="b2652-108">이 자습서에서는 데이터 바인딩된 데이터 바인딩된 및 RowDataBound 이벤트 처리기를 사용 하 여 서식 지정을 수행 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-108">In this tutorial we'll look at how to accomplish data bound formatting through the use of the DataBound and RowDataBound event handlers.</span></span>


## <a name="introduction"></a><span data-ttu-id="b2652-109">소개</span><span class="sxs-lookup"><span data-stu-id="b2652-109">Introduction</span></span>

<span data-ttu-id="b2652-110">GridView, DetailsView, FormView 컨트롤의 모양은 다양 한 스타일 관련 속성을 통해 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-110">The appearance of the GridView, DetailsView, and FormView controls can be customized through a myriad of style-related properties.</span></span> <span data-ttu-id="b2652-111">같은 속성 `CssClass`, `Font`, `BorderWidth`, `BorderStyle`, `BorderColor`, `Width`, 및 `Height`, 맺음 렌더링 된 컨트롤의 일반적인 모양을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-111">Properties like `CssClass`, `Font`, `BorderWidth`, `BorderStyle`, `BorderColor`, `Width`, and `Height`, among others, dictate the general appearance of the rendered control.</span></span> <span data-ttu-id="b2652-112">포함 하 여 속성 `HeaderStyle`, `RowStyle`, `AlternatingRowStyle`, 스타일 설정과 특정 섹션에 적용 될 수 있도록 다른 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-112">Properties including `HeaderStyle`, `RowStyle`, `AlternatingRowStyle`, and others allow these same style settings to be applied to particular sections.</span></span> <span data-ttu-id="b2652-113">마찬가지로, 이러한 스타일 설정은 필드 수준에서 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-113">Likewise, these style settings can be applied at the field level.</span></span>

<span data-ttu-id="b2652-114">대부분의 시나리오에서 하지만 형식 지정 요구 사항에 따라 달라 표시 된 데이터의 값.</span><span class="sxs-lookup"><span data-stu-id="b2652-114">In many scenarios though, the formatting requirements depend upon the value of the displayed data.</span></span> <span data-ttu-id="b2652-115">예를 들어 하기 위해의 제품을 판매, 제품 정보를 나열 하는 보고서 수 배경색 설정 갖는 해당 제품에 대 한 노란색 `UnitsInStock` 및 `UnitsOnOrder` 필드는 모두 0입니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-115">For example, to draw attention to out of stock products, a report listing product information might set the background color to yellow for those products whose `UnitsInStock` and `UnitsOnOrder` fields are both equal to 0.</span></span> <span data-ttu-id="b2652-116">비용이 많이 드는 products를 강조 표시 굵은 글꼴로 이상 $75.00 비용 계산과 해당 제품의 가격을 표시 하려고 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-116">To highlight the more expensive products, we may want to display the prices of those products costing more than $75.00 in a bold font.</span></span>

<span data-ttu-id="b2652-117">GridView, DetailsView, 또는 데이터를 바인딩할 기반 FormView의 형식이 조정 하는 여러 가지 방법으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-117">Adjusting the format of the GridView, DetailsView, or FormView based upon the data bound to it can be accomplished in multiple ways.</span></span> <span data-ttu-id="b2652-118">이 자습서에서 살펴보게 데이터 연결을 사용 하 여 서식 지정을 수행 하는 방법의 `DataBound` 및 `RowDataBound` 이벤트 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-118">In this tutorial we'll look at how to accomplish data bound formatting through the use of the `DataBound` and `RowDataBound` event handlers.</span></span> <span data-ttu-id="b2652-119">다음 자습서는 대체 접근 방식을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-119">In the next tutorial we'll explore an alternative approach.</span></span>

## <a name="using-the-detailsview-controlsdataboundevent-handler"></a><span data-ttu-id="b2652-120">DetailsView 컨트롤을 사용 하 여`DataBound`이벤트 처리기</span><span class="sxs-lookup"><span data-stu-id="b2652-120">Using the DetailsView Control's`DataBound`Event Handler</span></span>

<span data-ttu-id="b2652-121">경우에 바인딩된 데이터가 DetailsView, 데이터 소스 제어에서 또는 프로그래밍 방식으로 데이터를 컨트롤의 할당을 통해 `DataSource` 속성과 호출 해당 `DataBind()` 메서드를 다음 단계를 순서 대로 발생:</span><span class="sxs-lookup"><span data-stu-id="b2652-121">When data is bound to a DetailsView, either from a data source control or through programmatically assigning data to the control's `DataSource` property and calling its `DataBind()` method, the following sequence of steps occur:</span></span>

1. <span data-ttu-id="b2652-122">데이터 웹 컨트롤의 `DataBinding` 이벤트 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-122">The data Web control's `DataBinding` event fires.</span></span>
2. <span data-ttu-id="b2652-123">데이터는 데이터 웹 컨트롤에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-123">The data is bound to the data Web control.</span></span>
3. <span data-ttu-id="b2652-124">데이터 웹 컨트롤의 `DataBound` 이벤트 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-124">The data Web control's `DataBound` event fires.</span></span>

<span data-ttu-id="b2652-125">1 단계와 3 단계는 이벤트 처리기를 통해 직후 사용자 지정 논리 삽입 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-125">Custom logic can be injected immediately after steps 1 and 3 through an event handler.</span></span> <span data-ttu-id="b2652-126">에 대 한 이벤트 처리기를 만들어서는 `DataBound` 이벤트 데이터 웹 컨트롤에 바인딩되고 서식이 필요에 따라 조정 된 데이터를 프로그래밍 방식으로 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-126">By creating an event handler for the `DataBound` event we can programmatically determine the data that has been bound to the data Web control and adjust the formatting as needed.</span></span> <span data-ttu-id="b2652-127">이 설명 하기 위해 이제 제품에 대 한 일반 정보를 표시 하지만 ½ ֳ µ DetailsView를 만들는 `UnitPrice` 값에 ***굵게, 기울임꼴 글꼴*** $75.00 초과 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="b2652-127">To illustrate this let's create a DetailsView that will list general information about a product, but will display the `UnitPrice` value in a ***bold, italic font*** if it exceeds $75.00.</span></span>

## <a name="step-1-displaying-the-product-information-in-a-detailsview"></a><span data-ttu-id="b2652-128">1 단계: DetailsView에 제품 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-128">Step 1: Displaying the Product Information in a DetailsView</span></span>

<span data-ttu-id="b2652-129">열기는 `CustomColors.aspx` 페이지에 `CustomFormatting` 폴더를 디자이너 도구 상자에서 DetailsView 컨트롤을 끌어, 설정 해당 `ID` 속성 값을 `ExpensiveProductsPriceInBoldItalic`, 고 호출 하는 새 ObjectDataSource 컨트롤에 바인딩하는 `ProductsBLL` 클래스의 `GetProducts()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="b2652-129">Open the `CustomColors.aspx` page in the `CustomFormatting` folder, drag a DetailsView control from the Toolbox onto the Designer, set its `ID` property value to `ExpensiveProductsPriceInBoldItalic`, and bind it to a new ObjectDataSource control that invokes the `ProductsBLL` class's `GetProducts()` method.</span></span> <span data-ttu-id="b2652-130">이 작업을 수행 하는 자세한 단계는 이전 자습서에서 자세히 살펴보고 이러한 이후 편의상 여기 생략 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-130">The detailed steps for accomplishing this are omitted here for brevity since we examined them in detail in previous tutorials.</span></span>

<span data-ttu-id="b2652-131">DetailsView에는 ObjectDataSource를 바인딩된 한 후 필드 목록을 수정 하려면 잠시.</span><span class="sxs-lookup"><span data-stu-id="b2652-131">Once you've bound the ObjectDataSource to the DetailsView, take a moment to modify the field list.</span></span> <span data-ttu-id="b2652-132">제거를 선택한 이유는 `ProductID`, `SupplierID`, `CategoryID`, `UnitsInStock`, `UnitsOnOrder`, `ReorderLevel`, 및 `Discontinued` BoundFields 바뀌고 나머지 BoundFields 다시 포맷 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-132">I've opted to remove the `ProductID`, `SupplierID`, `CategoryID`, `UnitsInStock`, `UnitsOnOrder`, `ReorderLevel`, and `Discontinued` BoundFields and renamed and reformatted the remaining BoundFields.</span></span> <span data-ttu-id="b2652-133">도 취소는 `Width` 및 `Height` 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-133">I also cleared out the `Width` and `Height` settings.</span></span> <span data-ttu-id="b2652-134">DetailsView에 하나의 레코드만 표시, 되므로 최종 사용자를 모든 제품을 볼 수 있도록 하기 위해 페이징 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-134">Since the DetailsView displays only a single record, we need to enable paging in order to allow the end user to view all of the products.</span></span> <span data-ttu-id="b2652-135">DetailsView의 스마트 태그에서 페이징 사용 확인란을 선택 하 여 그렇게 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-135">Do so by checking the Enable Paging checkbox in the DetailsView's smart tag.</span></span>


<span data-ttu-id="b2652-136">[![확인란을 사용 하도록 설정 페이징 DetailsView의 스마트 태그](custom-formatting-based-upon-data-cs/_static/image2.png)](custom-formatting-based-upon-data-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b2652-136">[![Check the Enable Paging Checkbox in the DetailsView's Smart Tag](custom-formatting-based-upon-data-cs/_static/image2.png)](custom-formatting-based-upon-data-cs/_static/image1.png)</span></span>

<span data-ttu-id="b2652-137">**그림 1**: 확인란을 사용 하도록 설정 페이징 DetailsView의 스마트 태그 ([전체 크기 이미지를 보려면 클릭](custom-formatting-based-upon-data-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="b2652-137">**Figure 1**: Check the Enable Paging Checkbox in the DetailsView's Smart Tag ([Click to view full-size image](custom-formatting-based-upon-data-cs/_static/image3.png))</span></span>


<span data-ttu-id="b2652-138">이러한 변경 내용은 다음 DetailsView 태그 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-138">After these changes, the DetailsView markup will be:</span></span>


[!code-aspx[Main](custom-formatting-based-upon-data-cs/samples/sample1.aspx)]

<span data-ttu-id="b2652-139">브라우저에서이 페이지를 테스트해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="b2652-139">Take a moment to test out this page in your browser.</span></span>


<span data-ttu-id="b2652-140">[![DetailsView 컨트롤은 한 번에 제품 중 하나를 표시합니다.](custom-formatting-based-upon-data-cs/_static/image5.png)](custom-formatting-based-upon-data-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="b2652-140">[![The DetailsView Control Displays One Product at a Time](custom-formatting-based-upon-data-cs/_static/image5.png)](custom-formatting-based-upon-data-cs/_static/image4.png)</span></span>

<span data-ttu-id="b2652-141">**그림 2**: The DetailsView 컨트롤 표시 한 제품 한 번에 ([전체 크기 이미지를 보려면 클릭](custom-formatting-based-upon-data-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="b2652-141">**Figure 2**: The DetailsView Control Displays One Product at a Time ([Click to view full-size image](custom-formatting-based-upon-data-cs/_static/image6.png))</span></span>


## <a name="step-2-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a><span data-ttu-id="b2652-142">2 단계: 데이터 바인딩된 이벤트 처리기에 있는 데이터의 값을 프로그래밍 방식으로 결정</span><span class="sxs-lookup"><span data-stu-id="b2652-142">Step 2: Programmatically Determining the Value of the Data in the DataBound Event Handler</span></span>

<span data-ttu-id="b2652-143">이러한 제품에 대 한 굵게, 기울임꼴 글꼴의 가격을 표시 하려면 해당 `UnitPrice` 값 초과 $75.00, 프로그래밍 방식으로 결정을 해야는 `UnitPrice` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-143">In order to display the price in a bold, italic font for those products whose `UnitPrice` value exceeds $75.00, we need to first be able to programmatically determine the `UnitPrice` value.</span></span> <span data-ttu-id="b2652-144">수행할 수이 고 DetailsView에 대 한는 `DataBound` 이벤트 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-144">For the DetailsView, this can be accomplished in the `DataBound` event handler.</span></span> <span data-ttu-id="b2652-145">이벤트를 만들면 처리기 디자이너에서 DetailsView 클릭 속성 창으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-145">To create the event handler click on the DetailsView in the Designer then navigate to the Properties window.</span></span> <span data-ttu-id="b2652-146">F4 키를 눌러를 불러오는 되지 않았으면 표시할지 보기 메뉴로 이동 하 고 속성 창 메뉴 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-146">Press F4 to bring it up, if it's not visible, or go to the View menu and select the Properties Window menu option.</span></span> <span data-ttu-id="b2652-147">속성 창에서 DetailsView의 이벤트를 나열 하려면 번개 모양 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-147">From the Properties window, click on the lightning bolt icon to list the DetailsView's events.</span></span> <span data-ttu-id="b2652-148">다음으로, 두 번 클릭은 `DataBound` 이벤트 또는 이벤트 처리기를 만들려는 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-148">Next, either double-click the `DataBound` event or type in the name of the event handler you want to create.</span></span>


![데이터 바인딩된 이벤트에 대 한 이벤트 처리기 만들기](custom-formatting-based-upon-data-cs/_static/image7.png)

<span data-ttu-id="b2652-150">**그림 3**:에 대 한 이벤트 처리기 만들기는 `DataBound` 이벤트</span><span class="sxs-lookup"><span data-stu-id="b2652-150">**Figure 3**: Create an Event Handler for the `DataBound` Event</span></span>


<span data-ttu-id="b2652-151">이렇게 해도 이벤트 처리기를 만들고 있으며 코드 부분으로 이동 위치에 추가 된 자동으로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-151">Doing so will automatically create the event handler and take you to the code portion where it has been added.</span></span> <span data-ttu-id="b2652-152">이 시점에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-152">At this point you will see:</span></span>


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample2.cs)]

<span data-ttu-id="b2652-153">DetailsView에 바인딩된 데이터를 통해 액세스할 수는 `DataItem` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-153">The data bound to the DetailsView can be accessed via the `DataItem` property.</span></span> <span data-ttu-id="b2652-154">DataRow 인스턴스 강력한 형식의 컬렉션으로 이루어진 강력한 형식의 DataTable에 컨트롤을 바인딩하는 것을 기억 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b2652-154">Recall that we are binding our controls to a strongly-typed DataTable, which is composed of a collection of strongly-typed DataRow instances.</span></span> <span data-ttu-id="b2652-155">DataTable의 첫 번째 DataRow DetailsView의에 할당 된 DataTable DetailsView에 바인딩되면 `DataItem` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-155">When the DataTable is bound to the DetailsView, the first DataRow in the DataTable is assigned to the DetailsView's `DataItem` property.</span></span> <span data-ttu-id="b2652-156">특히,는 `DataItem` 속성에 할당 되는 `DataRowView` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-156">Specifically, the `DataItem` property is assigned a `DataRowView` object.</span></span> <span data-ttu-id="b2652-157">사용할 수는 `DataRowView`의 `Row` 속성은 기본 DataRow 개체에 액세스 하는 실제로 `ProductsRow` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="b2652-157">We can use the `DataRowView`'s `Row` property to get access to the underlying DataRow object, which is actually a `ProductsRow` instance.</span></span> <span data-ttu-id="b2652-158">이 있으면 `ProductsRow` 단순히 개체의 속성 값을 검사 하 여 결정을 위해 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="b2652-158">Once we have this `ProductsRow` instance we can make our decision by simply inspecting the object's property values.</span></span>

<span data-ttu-id="b2652-159">다음 코드를 확인 하는 방법을 보여 줍니다 여부는 `UnitPrice` DetailsView 컨트롤에 바인딩된 값이 $75.00 보다 큽니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-159">The following code illustrates how to determine whether the `UnitPrice` value bound to the DetailsView control is greater than $75.00:</span></span>


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample3.cs)]

> [!NOTE]
> <span data-ttu-id="b2652-160">이후 `UnitPrice` 가질 수 있습니다는 `NULL` 값은 데이터베이스에 먼저 확인을 있는지 지금 하지 다루고 있는 있는지 확인 한 `NULL` 값에 액세스 하기 전에 `ProductsRow`의 `UnitPrice` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-160">Since `UnitPrice` can have a `NULL` value in the database, we first check to make sure that we're not dealing with a `NULL` value before accessing the `ProductsRow`'s `UnitPrice` property.</span></span> <span data-ttu-id="b2652-161">이 검사는 중요 하기 때문에 액세스 하려고 하면는 `UnitPrice` 속성에 있을 때는 `NULL` 값은 `ProductsRow` 개체를 발생 시킵니다는 [StrongTypingException 예외](https://msdn.microsoft.com/library/system.data.strongtypingexception.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-161">This check is important because if we attempt to access the `UnitPrice` property when it has a `NULL` value the `ProductsRow` object will throw a [StrongTypingException exception](https://msdn.microsoft.com/library/system.data.strongtypingexception.aspx).</span></span>


## <a name="step-3-formatting-the-unitprice-value-in-the-detailsview"></a><span data-ttu-id="b2652-162">3 단계: DetailsView에서 UnitPrice 값 서식 지정</span><span class="sxs-lookup"><span data-stu-id="b2652-162">Step 3: Formatting the UnitPrice Value in the DetailsView</span></span>

<span data-ttu-id="b2652-163">이 시점에서 확인할 수 있습니다 여부는 `UnitPrice` DetailsView에 바인딩된 값 $75.00를 초과 하는 값을 갖지만을 프로그래밍 방식으로 DetailsView를 조정 하는 방법을 참조의 서식 지정에 따라 아직 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-163">At this point we can determine whether the `UnitPrice` value bound to the DetailsView has a value that exceeds $75.00, but we've yet to see how to programmatically adjust the DetailsView's formatting accordingly.</span></span> <span data-ttu-id="b2652-164">DetailsView에 있는 전체 행의 서식을 수정 하려면 프로그래밍 방식으로 액세스를 사용 하 여 행 `DetailsViewID.Rows[index]`사용 하 여 액세스를 특정 셀을 수정 하려면 `DetailsViewID.Rows[index].Cells[index]`합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-164">To modify the formatting of an entire row in the DetailsView, programmatically access the row using `DetailsViewID.Rows[index]`; to modify a particular cell, access use `DetailsViewID.Rows[index].Cells[index]`.</span></span> <span data-ttu-id="b2652-165">행 또는 셀에 대 한 참조가 있으면 해당 스타일 관련 속성을 설정 하 여 모양을 다음 조정 수 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-165">Once we have a reference to the row or cell we can then adjust its appearance by setting its style-related properties.</span></span>

<span data-ttu-id="b2652-166">행을 프로그래밍 방식으로 액세스 0에서 시작 하는 행의 인덱스를 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-166">Accessing a row programmatically requires that you know the row's index, which starts at 0.</span></span> <span data-ttu-id="b2652-167">`UnitPrice` 행이 다섯 번째 행 4의 인덱스를 제공 하 고 프로그래밍 방식으로 액세스할 수 있게 DetailsView에서 사용 하 여 `ExpensiveProductsPriceInBoldItalic.Rows[4]`합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-167">The `UnitPrice` row is the fifth row in the DetailsView, giving it an index of 4 and making it programmatically accessible using `ExpensiveProductsPriceInBoldItalic.Rows[4]`.</span></span> <span data-ttu-id="b2652-168">이 시점에서 다음 코드를 사용 하 여 굵게, 기울임꼴 글꼴에 표시 되는 행의 전체 내용을 만들어졌을:</span><span class="sxs-lookup"><span data-stu-id="b2652-168">At this point we could have the entire row's content displayed in a bold, italic font by using the following code:</span></span>


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample4.cs)]

<span data-ttu-id="b2652-169">그러나 이렇게 하면 *둘 다* (Price) 레이블과 굵게 및 기울임꼴 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-169">However, this will make *both* the label (Price) and the value bold and italic.</span></span> <span data-ttu-id="b2652-170">값만 굵게 및 기울임꼴는 다음을 사용 하 여 수행할 수는 행의 두 번째 셀에 서식을 적용 하기 위해서 필요를 확인 하려면:</span><span class="sxs-lookup"><span data-stu-id="b2652-170">If we want to make just the value bold and italic we need to apply this formatting to the second cell in the row, which can be accomplished using the following:</span></span>


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample5.cs)]

<span data-ttu-id="b2652-171">이 자습서 지금까지 스타일 시트를 명확히 구분 된 렌더링 된 태그 및 스타일 관련 정보를 유지 관리를 사용한 이후 위와 같이 보겠습니다 대신 특정 스타일 속성을 설정 하는 대신 CSS 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-171">Since our tutorials thus far have used stylesheets to maintain a clean separation between the rendered markup and style-related information, rather than setting the specific style properties as shown above let's instead use a CSS class.</span></span> <span data-ttu-id="b2652-172">열기는 `Styles.css` 스타일 시트 라는 새 CSS 클래스를 추가 하 고 `ExpensivePriceEmphasis` 다음 정의 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-172">Open the `Styles.css` stylesheet and add a new CSS class named `ExpensivePriceEmphasis` with the following definition:</span></span>


[!code-css[Main](custom-formatting-based-upon-data-cs/samples/sample6.css)]

<span data-ttu-id="b2652-173">그런 다음는 `DataBound` 이벤트 처리기 설정 셀의 `CssClass` 속성을 `ExpensivePriceEmphasis`합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-173">Then, in the `DataBound` event handler, set the cell's `CssClass` property to `ExpensivePriceEmphasis`.</span></span> <span data-ttu-id="b2652-174">다음 코드는 `DataBound` 전체에서 이벤트 처리기.</span><span class="sxs-lookup"><span data-stu-id="b2652-174">The following code shows the `DataBound` event handler in its entirety:</span></span>


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample7.cs)]

<span data-ttu-id="b2652-175">Chai 75.00 $ 비용을 보는 가격 보통 글꼴에 표시 됩니다 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="b2652-175">When viewing Chai, which costs less than $75.00, the price is displayed in a normal font (see Figure 4).</span></span> <span data-ttu-id="b2652-176">그러나, $97.00 가격이 있는 Mishi 산호세 Niku 볼 때 가격에에서 표시 됩니다 굵게, 기울임꼴 글꼴 (그림 5 참조).</span><span class="sxs-lookup"><span data-stu-id="b2652-176">However, when viewing Mishi Kobe Niku, which has a price of $97.00, the price is displayed in a bold, italic font (see Figure 5).</span></span>


<span data-ttu-id="b2652-177">[![$75.00 보다 적은 가격 보통 글꼴로 표시 됩니다.](custom-formatting-based-upon-data-cs/_static/image9.png)](custom-formatting-based-upon-data-cs/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="b2652-177">[![Prices Less than $75.00 are Displayed in a Normal Font](custom-formatting-based-upon-data-cs/_static/image9.png)](custom-formatting-based-upon-data-cs/_static/image8.png)</span></span>

<span data-ttu-id="b2652-178">**그림 4**: $75.00 보다 적은 가격 보통 글꼴로 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](custom-formatting-based-upon-data-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="b2652-178">**Figure 4**: Prices Less than $75.00 are Displayed in a Normal Font ([Click to view full-size image](custom-formatting-based-upon-data-cs/_static/image10.png))</span></span>


<span data-ttu-id="b2652-179">[![비용이 많이 드는 제품의 가격이 굵게, 기울임꼴 글꼴에에서 표시 됩니다.](custom-formatting-based-upon-data-cs/_static/image12.png)](custom-formatting-based-upon-data-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="b2652-179">[![Expensive Products' Prices are Displayed in a Bold, Italic Font](custom-formatting-based-upon-data-cs/_static/image12.png)](custom-formatting-based-upon-data-cs/_static/image11.png)</span></span>

<span data-ttu-id="b2652-180">**그림 5**: 비용이 많이 드는 제품의 가격이 굵게, 기울임꼴 글꼴에에서 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](custom-formatting-based-upon-data-cs/_static/image13.png))</span><span class="sxs-lookup"><span data-stu-id="b2652-180">**Figure 5**: Expensive Products' Prices are Displayed in a Bold, Italic Font ([Click to view full-size image](custom-formatting-based-upon-data-cs/_static/image13.png))</span></span>


## <a name="using-the-formview-controlsdataboundevent-handler"></a><span data-ttu-id="b2652-181">FormView 컨트롤을 사용 하 여`DataBound`이벤트 처리기</span><span class="sxs-lookup"><span data-stu-id="b2652-181">Using the FormView Control's`DataBound`Event Handler</span></span>

<span data-ttu-id="b2652-182">DetailsView 만들기에 대 한 기본 데이터는 FormView에 바인딩된을 결정 하기 위한 단계는 동일 하 게 한 `DataBound` 캐스팅 하는 이벤트 처리기는 `DataItem` 속성을 적절 한 개체 형식에는 컨트롤에 바인딩된 하 고 계속 진행 하는 방법을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-182">The steps for determining the underlying data bound to a FormView are identical to those for a DetailsView create a `DataBound` event handler, cast the `DataItem` property to the appropriate object type bound to the control, and determine how to proceed.</span></span> <span data-ttu-id="b2652-183">그러나 FormView 및 DetailsView 다 해당 사용자 인터페이스의 모양을 업데이트 하는 방법에.</span><span class="sxs-lookup"><span data-stu-id="b2652-183">The FormView and DetailsView differ, however, in how their user interface's appearance is updated.</span></span>

<span data-ttu-id="b2652-184">FormView 모든 BoundFields 포함 하지 않으며 따라서에 게 없는 경우는 `Rows` 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-184">The FormView does not contain any BoundFields and therefore lacks the `Rows` collection.</span></span> <span data-ttu-id="b2652-185">정적 HTML의 혼합을 포함할 수 있는 템플릿의 FormView은 구성 하는 대신, 웹 컨트롤 및 데이터 바인딩 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-185">Instead, a FormView is composed of templates, which can contain a mix of static HTML, Web controls, and databinding syntax.</span></span> <span data-ttu-id="b2652-186">일반적으로 FormView의 스타일을 조정 FormView의 템플릿 내에서 웹 컨트롤 중 하나 이상의 스타일을 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-186">Adjusting the style of a FormView typically involves adjusting the style of one or more of the Web controls within the FormView's templates.</span></span>

<span data-ttu-id="b2652-187">이 설명 하기 보겠습니다 사용할 목록 제품에 FormView 보겠습니다 앞의 예에서 하지만이 이번에서와 같이 표시 제품 이름 및 단위 재고 제품의 재고 10 보다 작거나 경우 빨간색 글꼴로 표시.</span><span class="sxs-lookup"><span data-stu-id="b2652-187">To illustrate this, let's use a FormView to list products like in the previous example, but this time let's display just the product name and units in stock with the units in stock displayed in a red font if it is less than or equal to 10.</span></span>

## <a name="step-4-displaying-the-product-information-in-a-formview"></a><span data-ttu-id="b2652-188">4 단계:는 FormView에 제품 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-188">Step 4: Displaying the Product Information in a FormView</span></span>

<span data-ttu-id="b2652-189">에 FormView 추가 `CustomColors.aspx` 집합과 DetailsView 아래에 있는 페이지의 `ID` 속성을 `LowStockedProductsInRed`합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-189">Add a FormView to the `CustomColors.aspx` page beneath the DetailsView and set its `ID` property to `LowStockedProductsInRed`.</span></span> <span data-ttu-id="b2652-190">FormView의 이전 단계에서 만든 ObjectDataSource 컨트롤에 바인딩하십시오.</span><span class="sxs-lookup"><span data-stu-id="b2652-190">Bind the FormView to the ObjectDataSource control created from the previous step.</span></span> <span data-ttu-id="b2652-191">이렇게 하면 만들어집니다는 `ItemTemplate`, `EditItemTemplate`, 및 `InsertItemTemplate` FormView에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-191">This will create an `ItemTemplate`, `EditItemTemplate`, and `InsertItemTemplate` for the FormView.</span></span> <span data-ttu-id="b2652-192">제거는 `EditItemTemplate` 및 `InsertItemTemplate` 를 빠르고 간편 하는 `ItemTemplate` 포함 하도록 테이블만 `ProductName` 및 `UnitsInStock` 서로 자체 적절 하 게 이름이 지정 된 레이블 컨트롤에 있는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-192">Remove the `EditItemTemplate` and `InsertItemTemplate` and simplify the `ItemTemplate` to include just the `ProductName` and `UnitsInStock` values, each in their own appropriately-named Label controls.</span></span> <span data-ttu-id="b2652-193">앞의 예제에서 DetailsView와 마찬가지로 또한 FormView의 스마트 태그에서 페이징 사용 확인란을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-193">As with the DetailsView from the earlier example, also check the Enable Paging checkbox in the FormView's smart tag.</span></span>

<span data-ttu-id="b2652-194">이 편집 내용을 후 FormView의 태그는 다음과 비슷하게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-194">After these edits your FormView's markup should look similar to the following:</span></span>


[!code-aspx[Main](custom-formatting-based-upon-data-cs/samples/sample8.aspx)]

<span data-ttu-id="b2652-195">`ItemTemplate` 포함:</span><span class="sxs-lookup"><span data-stu-id="b2652-195">Note that the `ItemTemplate` contains:</span></span>

- <span data-ttu-id="b2652-196">**정적 HTML** 텍스트 "제품:" 및 "재고 수량이:"와 함께 `<br />` 및 `<b>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-196">**Static HTML** the text "Product:" and "Units In Stock:" along with the `<br />` and `<b>` elements.</span></span>
- <span data-ttu-id="b2652-197">**웹 컨트롤** 두 Label 컨트롤 `ProductNameLabel` 및 `UnitsInStockLabel`합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-197">**Web controls** the two Label controls, `ProductNameLabel` and `UnitsInStockLabel`.</span></span>
- <span data-ttu-id="b2652-198">**데이터 바인딩된 구문을** 는 `<%# Bind("ProductName") %>` 및 `<%# Bind("UnitsInStock") %>` Label 컨트롤에 이러한 필드에서 값을 할당 하는 구문은 `Text` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-198">**Databinding syntax** the `<%# Bind("ProductName") %>` and `<%# Bind("UnitsInStock") %>` syntax, which assigns the values from these fields to the Label controls' `Text` properties.</span></span>

## <a name="step-5-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a><span data-ttu-id="b2652-199">5 단계: 데이터 바인딩된 이벤트 처리기에 있는 데이터의 값을 프로그래밍 방식으로 결정</span><span class="sxs-lookup"><span data-stu-id="b2652-199">Step 5: Programmatically Determining the Value of the Data in the DataBound Event Handler</span></span>

<span data-ttu-id="b2652-200">다음 단계는 태그로 FormView의 완료를 프로그래밍 방식으로 하는 경우를 확인 하는 `UnitsInStock` 값이 10 보다 작습니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-200">With the FormView's markup complete, the next step is to programmatically determine if the `UnitsInStock` value is less than or equal to 10.</span></span> <span data-ttu-id="b2652-201">이 인해 DetailsView 에서처럼 FormView와 정확히 같은 방식으로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-201">This is accomplished in the exact same manner with the FormView as it was with the DetailsView.</span></span> <span data-ttu-id="b2652-202">FormView의에 대 한 이벤트 처리기를 만들어 시작 `DataBound` 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-202">Start by creating an event handler for the FormView's `DataBound` event.</span></span>


![데이터 바인딩된 이벤트 처리기 만들기](custom-formatting-based-upon-data-cs/_static/image14.png)

<span data-ttu-id="b2652-204">**그림 6**: 만들기는 `DataBound` 이벤트 처리기</span><span class="sxs-lookup"><span data-stu-id="b2652-204">**Figure 6**: Create the `DataBound` Event Handler</span></span>


<span data-ttu-id="b2652-205">이벤트 처리기 캐스팅 FormView의 `DataItem` 속성을는 `ProductsRow` 인스턴스를 확인 여부는 `UnitsInPrice` 값은 빨간색 글꼴로 표시 해야 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-205">In the event handler cast the FormView's `DataItem` property to a `ProductsRow` instance and determine whether the `UnitsInPrice` value is such that we need to display it in a red font.</span></span>


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample9.cs)]

## <a name="step-6-formatting-the-unitsinstocklabel-label-control-in-the-formviews-itemtemplate"></a><span data-ttu-id="b2652-206">6 단계: FormView의 ItemTemplate에 UnitsInStockLabel Label 컨트롤 서식 지정</span><span class="sxs-lookup"><span data-stu-id="b2652-206">Step 6: Formatting the UnitsInStockLabel Label Control in the FormView's ItemTemplate</span></span>

<span data-ttu-id="b2652-207">마지막 단계는 표시 된 형식을 지정 하는 `UnitsInStock` 값이 10 이하인 경우 빨간색 글꼴로 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-207">The final step is to format the displayed `UnitsInStock` value in a red font if the value is 10 or less.</span></span> <span data-ttu-id="b2652-208">프로그래밍 방식으로 액세스 해야이를 위해는 `UnitsInStockLabel` 컨트롤에 `ItemTemplate` 해당 텍스트가 빨간색으로 표시 되도록 스타일 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-208">To accomplish this we need to programmatically access the `UnitsInStockLabel` control in the `ItemTemplate` and set its style properties so that its text is displayed in red.</span></span> <span data-ttu-id="b2652-209">서식 파일에서 웹 컨트롤에 액세스 하려면 사용 된 `FindControl("controlID")` 다음과 같이 메서드:</span><span class="sxs-lookup"><span data-stu-id="b2652-209">To access a Web control in a template, use the `FindControl("controlID")` method like this:</span></span>


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample10.cs)]

<span data-ttu-id="b2652-210">컨트롤 레이블에 액세스 하려는 예제 `ID` 값은 `UnitsInStockLabel`이므로 사용:</span><span class="sxs-lookup"><span data-stu-id="b2652-210">For our example we want to access a Label control whose `ID` value is `UnitsInStockLabel`, so we'd use:</span></span>


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample11.cs)]

<span data-ttu-id="b2652-211">웹 컨트롤에 대 한 프로그래밍 참조 했으므로 필요에 따라 해당 스타일 관련 속성 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-211">Once we have a programmatic reference to the Web control, we can modify its style-related properties as needed.</span></span> <span data-ttu-id="b2652-212">이전 예에서 만들었습니다.이 안에에서 CSS 클래스 처럼 `Styles.css` 라는 `LowUnitsInStockEmphasis`합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-212">As with the earlier example, I've created a CSS class in `Styles.css` named `LowUnitsInStockEmphasis`.</span></span> <span data-ttu-id="b2652-213">이 스타일 웹 컨트롤에 적용할 설정 해당 `CssClass` 속성 적절 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-213">To apply this style to the Label Web control, set its `CssClass` property accordingly.</span></span>


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample12.cs)]

> [!NOTE]
> <span data-ttu-id="b2652-214">프로그래밍 방식으로 사용 하 여 웹 컨트롤에 액세스 하는 서식 파일의 서식을 지정 하기 위한 구문을 `FindControl("controlID")` 스타일 관련 속성을 다음 설정도 사용할 수 있습니다 사용할 때 [TemplateFields](https://msdn.microsoft.com/library/system.web.ui.webcontrols.templatefield(VS.80).aspx) DetailsView 또는 GridView 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-214">The syntax for formatting a template programmatically accessing the Web control using `FindControl("controlID")` and then setting its style-related properties can also be used when using [TemplateFields](https://msdn.microsoft.com/library/system.web.ui.webcontrols.templatefield(VS.80).aspx) in the DetailsView or GridView controls.</span></span> <span data-ttu-id="b2652-215">이 다음 자습서 TemplateFields 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-215">We'll examine TemplateFields in our next tutorial.</span></span>


<span data-ttu-id="b2652-216">그림 7에는 제품을 볼 때 FormView 나와 있는 `UnitsInStock` 그림 8에 있는 제품의 해당 값이 10 보다 작은 값이 10 보다 크고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-216">Figures 7 shows the FormView when viewing a product whose `UnitsInStock` value is greater than 10, while the product in Figure 8 has its value less than 10.</span></span>


<span data-ttu-id="b2652-217">[![제품으로 정도 충분히 큰 Units In Stock, 사용자 지정 서식 없이 적용 됩니다.](custom-formatting-based-upon-data-cs/_static/image16.png)](custom-formatting-based-upon-data-cs/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="b2652-217">[![For Products With a Sufficiently Large Units In Stock, No Custom Formatting is Applied](custom-formatting-based-upon-data-cs/_static/image16.png)](custom-formatting-based-upon-data-cs/_static/image15.png)</span></span>

<span data-ttu-id="b2652-218">**그림 7**:에 대 한 제품으로 정도 충분히 큰 Units In Stock, 사용자 지정 서식 없이 적용 됩니다 ([전체 크기 이미지를 보려면 클릭](custom-formatting-based-upon-data-cs/_static/image17.png))</span><span class="sxs-lookup"><span data-stu-id="b2652-218">**Figure 7**: For Products With a Sufficiently Large Units In Stock, No Custom Formatting is Applied ([Click to view full-size image](custom-formatting-based-upon-data-cs/_static/image17.png))</span></span>


<span data-ttu-id="b2652-219">[![재고 수의 단위는 해당 제품으로의 값이 10 이하의 빨간색으로 표시 됩니다.](custom-formatting-based-upon-data-cs/_static/image19.png)](custom-formatting-based-upon-data-cs/_static/image18.png)</span><span class="sxs-lookup"><span data-stu-id="b2652-219">[![The Units in Stock Number is Shown in Red for Those Products With Values of 10 or Less](custom-formatting-based-upon-data-cs/_static/image19.png)](custom-formatting-based-upon-data-cs/_static/image18.png)</span></span>

<span data-ttu-id="b2652-220">**그림 8**: 재고 수의 장치는 해당 제품으로의 값이 10 이하의 빨간색으로 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](custom-formatting-based-upon-data-cs/_static/image20.png))</span><span class="sxs-lookup"><span data-stu-id="b2652-220">**Figure 8**: The Units in Stock Number is Shown in Red for Those Products With Values of 10 or Less ([Click to view full-size image](custom-formatting-based-upon-data-cs/_static/image20.png))</span></span>


## <a name="formatting-with-the-gridviewsrowdataboundevent"></a><span data-ttu-id="b2652-221">GridView의 서식을`RowDataBound`이벤트</span><span class="sxs-lookup"><span data-stu-id="b2652-221">Formatting with the GridView's`RowDataBound`Event</span></span>

<span data-ttu-id="b2652-222">이전 DetailsView 단계의 순서를 검사 했습니다 하 고 FormView 데이터 바인딩 중 통해 진행 상황을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-222">Earlier we examined the sequence of steps the DetailsView and FormView controls progress through during databinding.</span></span> <span data-ttu-id="b2652-223">살펴보겠습니다 다음이 단계를 통해 다시 한 번으로 쉽게 찾아볼.</span><span class="sxs-lookup"><span data-stu-id="b2652-223">Let's look over these steps once again as a refresher.</span></span>

1. <span data-ttu-id="b2652-224">데이터 웹 컨트롤의 `DataBinding` 이벤트 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-224">The data Web control's `DataBinding` event fires.</span></span>
2. <span data-ttu-id="b2652-225">데이터는 데이터 웹 컨트롤에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-225">The data is bound to the data Web control.</span></span>
3. <span data-ttu-id="b2652-226">데이터 웹 컨트롤의 `DataBound` 이벤트 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-226">The data Web control's `DataBound` event fires.</span></span>

<span data-ttu-id="b2652-227">이러한 세 가지 간단한 단계는 하나의 레코드만 표시 하므로 DetailsView 및 FormView에 대 한 충분 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-227">These three simple steps are sufficient for the DetailsView and FormView because they display only a single record.</span></span> <span data-ttu-id="b2652-228">표시 하는 GridView에 대 한 *모든* 바인딩된 레코드를 (첫 번째 뿐 아니라 함), 2 단계가 약간 더 개입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-228">For the GridView, which displays *all* records bound to it (not just the first), step 2 is a bit more involved.</span></span>

<span data-ttu-id="b2652-229">GridView 데이터 원본 열거 만들고, 각 레코드에 대해 2 단계에서 한 `GridViewRow` 인스턴스를 현재 레코드 어셈블리에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-229">In step 2 the GridView enumerates the data source and, for each record, creates a `GridViewRow` instance and binds the current record to it.</span></span> <span data-ttu-id="b2652-230">각 `GridViewRow` GridView에 추가 된 두 개의 이벤트가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-230">For each `GridViewRow` added to the GridView, two events are raised:</span></span>

- <span data-ttu-id="b2652-231">**`RowCreated`**후에 발생는 `GridViewRow` 만든</span><span class="sxs-lookup"><span data-stu-id="b2652-231">**`RowCreated`** fires after the `GridViewRow` has been created</span></span>
- <span data-ttu-id="b2652-232">**`RowDataBound`**현재 레코드에 바인딩된 후에 발생는 `GridViewRow`합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-232">**`RowDataBound`** fires after the current record has been bound to the `GridViewRow`.</span></span>

<span data-ttu-id="b2652-233">GridView에 대 한 다음, 데이터 바인딩 보다 정확 하 게 설명에서 다음 단계를 순서 대로:</span><span class="sxs-lookup"><span data-stu-id="b2652-233">For the GridView, then, data binding is more accurately described by the following sequence of steps:</span></span>

1. <span data-ttu-id="b2652-234">GridView의 `DataBinding` 이벤트 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-234">The GridView's `DataBinding` event fires.</span></span>
2. <span data-ttu-id="b2652-235">데이터가는 GridView에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-235">The data is bound to the GridView.</span></span>   
  
 <span data-ttu-id="b2652-236">데이터 원본에 있는 각 레코드에 대 한</span><span class="sxs-lookup"><span data-stu-id="b2652-236">For each record in the data source</span></span> 

    1. <span data-ttu-id="b2652-237">만들기는 `GridViewRow` 개체</span><span class="sxs-lookup"><span data-stu-id="b2652-237">Create a `GridViewRow` object</span></span>
    2. <span data-ttu-id="b2652-238">화재는 `RowCreated` 이벤트</span><span class="sxs-lookup"><span data-stu-id="b2652-238">Fire the `RowCreated` event</span></span>
    3. <span data-ttu-id="b2652-239">해당 레코드를 바인딩하는`GridViewRow`</span><span class="sxs-lookup"><span data-stu-id="b2652-239">Bind the record to the `GridViewRow`</span></span>
    4. <span data-ttu-id="b2652-240">화재는 `RowDataBound` 이벤트</span><span class="sxs-lookup"><span data-stu-id="b2652-240">Fire the `RowDataBound` event</span></span>
    5. <span data-ttu-id="b2652-241">추가 `GridViewRow` 에 `Rows` 컬렉션</span><span class="sxs-lookup"><span data-stu-id="b2652-241">Add the `GridViewRow` to the `Rows` collection</span></span>
3. <span data-ttu-id="b2652-242">GridView의 `DataBound` 이벤트 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-242">The GridView's `DataBound` event fires.</span></span>

<span data-ttu-id="b2652-243">GridView의 개별 레코드의 형식의 사용자 지정 하려면 다음을 만들어야 한다는 대 한 이벤트 처리기는 `RowDataBound` 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-243">To customize the format of the GridView's individual records, then, we need to create an event handler for the `RowDataBound` event.</span></span> <span data-ttu-id="b2652-244">이 설명 하기에 GridView를 추가 해 보겠습니다는 `CustomColors.aspx` 이름, 범주 및 해당 제품 가격이 $10.00 보다 작은 노란색 배경색으로 강조 표시 하는 각 제품에 대 한 가격을 나열 하는 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-244">To illustrate this, let's add a GridView to the `CustomColors.aspx` page that lists the name, category, and price for each product, highlighting those products whose price is less than $10.00 with a yellow background color.</span></span>

## <a name="step-7-displaying-product-information-in-a-gridview"></a><span data-ttu-id="b2652-245">7 단계:는 GridView에 제품 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-245">Step 7: Displaying Product Information in a GridView</span></span>

<span data-ttu-id="b2652-246">이전 예제에서 FormView 아래에 GridView를 추가 하 고 설정의 `ID` 속성을 `HighlightCheapProducts`합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-246">Add a GridView beneath the FormView from the previous example and set its `ID` property to `HighlightCheapProducts`.</span></span> <span data-ttu-id="b2652-247">페이지에서 모든 제품을 반환 하는 ObjectDataSource 이미 했기 때문에 바인딩할 GridView입니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-247">Since we already have an ObjectDataSource that returns all products on the page, bind the GridView to that.</span></span> <span data-ttu-id="b2652-248">GridView의 BoundFields 방금: 제품의 이름, 범주 및 가격을 포함 하도록 마지막으로 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-248">Finally, edit the GridView's BoundFields to include just the products' names, categories, and prices.</span></span> <span data-ttu-id="b2652-249">이 편집 내용을 후 GridView의 태그는 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-249">After these edits the GridView's markup should look like:</span></span>


[!code-aspx[Main](custom-formatting-based-upon-data-cs/samples/sample13.aspx)]

<span data-ttu-id="b2652-250">그림 9 브라우저를 통해 표시 될 때 까지의 진행률을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-250">Figure 9 shows our progress to this point when viewed through a browser.</span></span>


<span data-ttu-id="b2652-251">[![이름, 범주 및 각 제품에 대 한 가격을 나열 하는 GridView](custom-formatting-based-upon-data-cs/_static/image22.png)](custom-formatting-based-upon-data-cs/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="b2652-251">[![The GridView Lists the Name, Category, and Price For Each Product](custom-formatting-based-upon-data-cs/_static/image22.png)](custom-formatting-based-upon-data-cs/_static/image21.png)</span></span>

<span data-ttu-id="b2652-252">**그림 9**: 이름, 범주 및 각 제품에 대 한 가격을 나열 하는 GridView ([전체 크기 이미지를 보려면 클릭](custom-formatting-based-upon-data-cs/_static/image23.png))</span><span class="sxs-lookup"><span data-stu-id="b2652-252">**Figure 9**: The GridView Lists the Name, Category, and Price For Each Product ([Click to view full-size image](custom-formatting-based-upon-data-cs/_static/image23.png))</span></span>


## <a name="step-8-programmatically-determining-the-value-of-the-data-in-the-rowdatabound-event-handler"></a><span data-ttu-id="b2652-253">8 단계: RowDataBound 이벤트 처리기에 있는 데이터의 값을 프로그래밍 방식으로 결정</span><span class="sxs-lookup"><span data-stu-id="b2652-253">Step 8: Programmatically Determining the Value of the Data in the RowDataBound Event Handler</span></span>

<span data-ttu-id="b2652-254">경우는 `ProductsDataTable` GridView에 바인딩됩니다 해당 `ProductsRow` 열거 하 고 각 인스턴스는 `ProductsRow` 는 `GridViewRow` 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-254">When the `ProductsDataTable` is bound to the GridView its `ProductsRow` instances are enumerated and for each `ProductsRow` a `GridViewRow` is created.</span></span> <span data-ttu-id="b2652-255">`GridViewRow`의 `DataItem` 하는 특정 속성에 할당 됩니다 `ProductRow`는 GridView의 `RowDataBound` 이벤트 처리기는 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-255">The `GridViewRow`'s `DataItem` property is assigned to the particular `ProductRow`, after which the GridView's `RowDataBound` event handler is raised.</span></span> <span data-ttu-id="b2652-256">확인 하는 `UnitPrice` GridView에 바인딩된 각 제품에 대 한 값이 다음 GridView의에 대 한 이벤트 처리기를 만들어야 한다는 `RowDataBound` 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-256">To determine the `UnitPrice` value for each product bound to the GridView, then, we need to create an event handler for the GridView's `RowDataBound` event.</span></span> <span data-ttu-id="b2652-257">이 이벤트 처리기에서 검사할 수 있습니다는 `UnitPrice` 현재에 대 한 값 `GridViewRow` 있도록 해당 행에 대 한 서식 지정 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-257">In this event handler we can inspect the `UnitPrice` value for the current `GridViewRow` and make a formatting decision for that row.</span></span>

<span data-ttu-id="b2652-258">FormView와 DetailsView 같은 일련의 단계를 사용 하 여이 이벤트 처리기를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-258">This event handler can be created using the same series of steps as with the FormView and DetailsView.</span></span>


![GridView의 RowDataBound 이벤트에 대 한 이벤트 처리기 만들기](custom-formatting-based-upon-data-cs/_static/image24.png)

<span data-ttu-id="b2652-260">**그림 10**: GridView의에 대 한 이벤트 처리기를 만들고 `RowDataBound` 이벤트</span><span class="sxs-lookup"><span data-stu-id="b2652-260">**Figure 10**: Create an Event Handler for the GridView's `RowDataBound` Event</span></span>


<span data-ttu-id="b2652-261">이런이 방식으로 이벤트 처리기를 만들면 다음 코드를 자동으로 ASP.NET 페이지의 코드 부분에 추가 하면:</span><span class="sxs-lookup"><span data-stu-id="b2652-261">Creating the event hander in this manner will cause the following code to be automatically added to the ASP.NET page's code portion:</span></span>


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample14.cs)]

<span data-ttu-id="b2652-262">경우는 `RowDataBound` 이벤트 발생 이벤트 처리기 매개 변수로 전달 되는 두 번째 형식의 개체 `GridViewRowEventArgs`, 라는 속성이 있는 `Row`합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-262">When the `RowDataBound` event fires, the event handler is passed as its second parameter an object of type `GridViewRowEventArgs`, which has a property named `Row`.</span></span> <span data-ttu-id="b2652-263">이 속성에 대 한 참조를 반환 합니다.는 `GridViewRow` 를 바인딩된 데이터 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-263">This property returns a reference to the `GridViewRow` that was just data bound.</span></span> <span data-ttu-id="b2652-264">액세스는 `ProductsRow` 에 바인딩된 인스턴스는 `GridViewRow` 사용 하 여는 `DataItem` 같이 속성:</span><span class="sxs-lookup"><span data-stu-id="b2652-264">To access the `ProductsRow` instance bound to the `GridViewRow` we use the `DataItem` property like so:</span></span>


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample15.cs)]

<span data-ttu-id="b2652-265">작업할 때의 `RowDataBound` GridView 다양 한 유형의 행으로 구성 된 하 고이 이벤트에 대해 발생 하는 점에 유의 해야 하는 이벤트 처리기 *모든* 행 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-265">When working with the `RowDataBound` event handler it is important to keep in mind that the GridView is composed of different types of rows and that this event is fired for *all* row types.</span></span> <span data-ttu-id="b2652-266">A `GridViewRow`의 형식을 확인 하 여 해당 `RowType` 속성을 가능한 값 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-266">A `GridViewRow`'s type can be determined by its `RowType` property, and can have one of the possible values:</span></span>

- <span data-ttu-id="b2652-267">`DataRow`GridView의에서 레코드에 바인딩되는 행`DataSource`</span><span class="sxs-lookup"><span data-stu-id="b2652-267">`DataRow` a row that is bound to a record from the GridView's `DataSource`</span></span>
- <span data-ttu-id="b2652-268">`EmptyDataRow`경우에 표시 되는 행 GridView의 `DataSource` 비어</span><span class="sxs-lookup"><span data-stu-id="b2652-268">`EmptyDataRow` the row displayed if the GridView's `DataSource` is empty</span></span>
- <span data-ttu-id="b2652-269">`Footer`바닥글 행입니다. 경우에 표시 된 GridView의 `ShowFooter` 속성`true`</span><span class="sxs-lookup"><span data-stu-id="b2652-269">`Footer` the footer row; shown if the GridView's `ShowFooter` property is set to `true`</span></span>
- <span data-ttu-id="b2652-270">`Header`머리글 행입니다. GridView의 ShowHeader 속성이로 설정 되어 있으면 표시 `true` (기본값)</span><span class="sxs-lookup"><span data-stu-id="b2652-270">`Header` the header row; shown if the GridView's ShowHeader property is set to `true` (the default)</span></span>
- <span data-ttu-id="b2652-271">`Pager`GridView의에 대 한 구현 하는 페이징, 페이징 인터페이스를 표시 하는 행</span><span class="sxs-lookup"><span data-stu-id="b2652-271">`Pager` for GridView's that implement paging, the row that displays the paging interface</span></span>
- <span data-ttu-id="b2652-272">`Separator`GridView에 대 한 사용 되지 않지만에서 사용 하는 `RowType` DataList와 반복기에 대 한 속성 컨트롤을 두 개의 데이터 웹 컨트롤에 설명 합니다 이후 자습서</span><span class="sxs-lookup"><span data-stu-id="b2652-272">`Separator` not used for the GridView, but used by the `RowType` properties for the DataList and Repeater controls, two data Web controls we'll discuss in future tutorials</span></span>

<span data-ttu-id="b2652-273">이후는 `EmptyDataRow`, `Header`, `Footer`, 및 `Pager` 행 연관 되지 않습니다는 `DataSource` 레코드, 항상 수는 `null` 값을 해당 `DataItem` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-273">Since the `EmptyDataRow`, `Header`, `Footer`, and `Pager` rows aren't associated with a `DataSource` record, they will always have a `null` value for their `DataItem` property.</span></span> <span data-ttu-id="b2652-274">현재 사용 하 려 하기 전에 이러한 이유로 `GridViewRow`의 `DataItem` 속성을 항상 먼저 않도록 해야 것으로 처리 하는 한 `DataRow`합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-274">For this reason, before attempting to work with the current `GridViewRow`'s `DataItem` property, we first must make sure that we're dealing with a `DataRow`.</span></span> <span data-ttu-id="b2652-275">이 확인 하 여 수행할 수 있습니다는 `GridViewRow`의 `RowType` 같이 속성:</span><span class="sxs-lookup"><span data-stu-id="b2652-275">This can be accomplished by checking the `GridViewRow`'s `RowType` property like so:</span></span>


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample16.cs)]

## <a name="step-9-highlighting-the-row-yellow-when-the-unitprice-value-is-less-than-1000"></a><span data-ttu-id="b2652-276">9 단계: $10.00 보다 작은 행 노란색 When the UnitPrice 값을 강조 표시</span><span class="sxs-lookup"><span data-stu-id="b2652-276">Step 9: Highlighting the Row Yellow When the UnitPrice Value is Less than $10.00</span></span>

<span data-ttu-id="b2652-277">마지막 단계는 프로그래밍 방식으로 전체 강조 표시 하는 `GridViewRow` 경우는 `UnitPrice` 행이 $10.00 보다 작은 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-277">The last step is to programmatically highlight the entire `GridViewRow` if the `UnitPrice` value for that row is less than $10.00.</span></span> <span data-ttu-id="b2652-278">GridView의 행 또는 셀에 액세스 하기 위한 구문은 DetailsView와 마찬가지로 동일 `GridViewID.Rows[index]` 전체 행에 액세스 하 `GridViewID.Rows[index].Cells[index]` 특정 셀에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-278">The syntax for accessing a GridView's rows or cells is the same as with the DetailsView `GridViewID.Rows[index]` to access the entire row, `GridViewID.Rows[index].Cells[index]` to access a particular cell.</span></span> <span data-ttu-id="b2652-279">그러나 때는 `RowDataBound` 이벤트 처리기를 데이터 바인딩된 발생 `GridViewRow` GridView의에 추가할 수는 아직 `Rows` 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-279">However, when the `RowDataBound` event handler fires the data bound `GridViewRow` has yet to be added to the GridView's `Rows` collection.</span></span> <span data-ttu-id="b2652-280">현재 액세스할 수 없는 따라서 `GridViewRow` 에서 인스턴스는 `RowDataBound` 행 컬렉션을 사용 하 여 이벤트 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-280">Therefore you cannot access the current `GridViewRow` instance from the `RowDataBound` event handler using the Rows collection.</span></span>

<span data-ttu-id="b2652-281">대신 `GridViewID.Rows[index]`, 현재를 참조할 수 있습니다 `GridViewRow` 인스턴스는 `RowDataBound` 이벤트 처리기를 사용 하 여 `e.Row`합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-281">Instead of `GridViewID.Rows[index]`, we can reference the current `GridViewRow` instance in the `RowDataBound` event handler using `e.Row`.</span></span> <span data-ttu-id="b2652-282">즉, 순서를 현재 강조 표시 `GridViewRow` 에서 인스턴스는 `RowDataBound` 이벤트 처리기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-282">That is, in order to highlight the current `GridViewRow` instance from the `RowDataBound` event handler we would use:</span></span>


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample17.cs)]

<span data-ttu-id="b2652-283">설정 하지 않고는 `GridViewRow`의 `BackColor` 속성을 직접 CSS 클래스를 사용 하 여 집중 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-283">Rather than set the `GridViewRow`'s `BackColor` property directly, let's stick with using CSS classes.</span></span> <span data-ttu-id="b2652-284">명명 된 CSS 클래스를 만들었습니다 `AffordablePriceEmphasis` 노란색으로 명령 프롬프트 창의 배경색을 설정 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-284">I've created a CSS class named `AffordablePriceEmphasis` that sets the background color to yellow.</span></span> <span data-ttu-id="b2652-285">전체 `RowDataBound` 이벤트 처리기가 따르는:</span><span class="sxs-lookup"><span data-stu-id="b2652-285">The completed `RowDataBound` event handler follows:</span></span>


[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample18.cs)]


<span data-ttu-id="b2652-286">[![가장 저렴 한 제품 노란색으로 강조 표시 됩니다.](custom-formatting-based-upon-data-cs/_static/image26.png)](custom-formatting-based-upon-data-cs/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="b2652-286">[![The Most Affordable Products are Highlighted Yellow](custom-formatting-based-upon-data-cs/_static/image26.png)](custom-formatting-based-upon-data-cs/_static/image25.png)</span></span>

<span data-ttu-id="b2652-287">**그림 11**: 가장 저렴 한 제품을 노란색으로 강조 표시 ([전체 크기 이미지를 보려면 클릭](custom-formatting-based-upon-data-cs/_static/image27.png))</span><span class="sxs-lookup"><span data-stu-id="b2652-287">**Figure 11**: The Most Affordable Products are Highlighted Yellow ([Click to view full-size image](custom-formatting-based-upon-data-cs/_static/image27.png))</span></span>


## <a name="summary"></a><span data-ttu-id="b2652-288">요약</span><span class="sxs-lookup"><span data-stu-id="b2652-288">Summary</span></span>

<span data-ttu-id="b2652-289">이 자습서에서는 GridView, DetailsView, 및 컨트롤에 바인딩된 데이터를 기반으로 FormView 서식을 지정 하는 방법에 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-289">In this tutorial we saw how to format the GridView, DetailsView, and FormView based on the data bound to the control.</span></span> <span data-ttu-id="b2652-290">에 대 한 이벤트 처리기에서 만든이를 위해는 `DataBound` 또는 `RowDataBound` 이벤트, 필요한 경우 서식 변경 함께 기본 데이터 검사 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-290">To accomplish this we created an event handler for the `DataBound` or `RowDataBound` events, where the underlying data was examined along with a formatting change, if needed.</span></span> <span data-ttu-id="b2652-291">DetailsView 또는 FormView에 바인딩된 데이터에 액세스 하려면 사용는 `DataItem` 속성에는 `DataBound` 이벤트 처리기는 GridView에 대 한; 각 `GridViewRow` 인스턴스의 `DataItem` 는 에서사용할수있는해당행에바인딩된데이터를포함하는속성`RowDataBound` 이벤트 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-291">To access the data bound to a DetailsView or FormView, we use the `DataItem` property in the `DataBound` event handler; for a GridView, each `GridViewRow` instance's `DataItem` property contains the data bound to that row, which is available in the `RowDataBound` event handler.</span></span>

<span data-ttu-id="b2652-292">프로그래밍 방식으로 데이터 웹 컨트롤의 서식 지정을 조정 하는 구문은 웹 컨트롤 및 서식을 지정할 데이터 표시 방법을 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-292">The syntax for programmatically adjusting the data Web control's formatting depends upon the Web control and how the data to be formatted is displayed.</span></span> <span data-ttu-id="b2652-293">DetailsView 및 GridView에 대 한 컨트롤, 행 및 셀 서 수 인덱스에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-293">For DetailsView and GridView controls, the rows and cells can be accessed by an ordinal index.</span></span> <span data-ttu-id="b2652-294">서식 파일을 사용 하 여 FormView에 대 한는 `FindControl("controlID")` 메서드는 템플릿 내에서 웹 컨트롤을 찾기 위해 일반적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-294">For the FormView, which uses templates, the `FindControl("controlID")` method is commonly used to locate a Web control from within the template.</span></span>

<span data-ttu-id="b2652-295">다음 자습서는 GridView와 DetailsView 템플릿을 사용 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-295">In the next tutorial we'll look at how to use templates with the GridView and DetailsView.</span></span> <span data-ttu-id="b2652-296">또한 기본 데이터에 따라 서식을 사용자 지정 하기 위한 또 다른 방법은 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-296">Additionally, we'll see another technique for customizing the formatting based on the underlying data.</span></span>

<span data-ttu-id="b2652-297">만족도 매우 프로그래밍!</span><span class="sxs-lookup"><span data-stu-id="b2652-297">Happy Programming!</span></span>

## <a name="about-the-author"></a><span data-ttu-id="b2652-298">작성자 정보</span><span class="sxs-lookup"><span data-stu-id="b2652-298">About the Author</span></span>

<span data-ttu-id="b2652-299">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-299">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), author of seven ASP/ASP.NET books and founder of [4GuysFromRolla.com](http://www.4guysfromrolla.com), has been working with Microsoft Web technologies since 1998.</span></span> <span data-ttu-id="b2652-300">Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-300">Scott works as an independent consultant, trainer, and writer.</span></span> <span data-ttu-id="b2652-301">그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-301">His latest book is [*Sams Teach Yourself ASP.NET 2.0 in 24 Hours*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco).</span></span> <span data-ttu-id="b2652-302">에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-302">He can be reached at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) or via his blog, which can be found at [http://ScottOnWriting.NET](http://ScottOnWriting.NET).</span></span>

## <a name="special-thanks-to"></a><span data-ttu-id="b2652-303">특별히 감사</span><span class="sxs-lookup"><span data-stu-id="b2652-303">Special Thanks To</span></span>

<span data-ttu-id="b2652-304">이 자습서 시리즈 많은 유용한 검토자가 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-304">This tutorial series was reviewed by many helpful reviewers.</span></span> <span data-ttu-id="b2652-305">이 자습서에 대 한 선행 검토자 E.R. 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-305">Lead reviewers for this tutorial were E.R.</span></span> <span data-ttu-id="b2652-306">Gilmore, Dennis Patterson 및 Dan Jagers 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2652-306">Gilmore, Dennis Patterson, and Dan Jagers.</span></span> <span data-ttu-id="b2652-307">향후 내 MSDN 문서를 검토에 관심이 있으십니까?</span><span class="sxs-lookup"><span data-stu-id="b2652-307">Interested in reviewing my upcoming MSDN articles?</span></span> <span data-ttu-id="b2652-308">이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="b2652-308">If so, drop me a line at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="b2652-309">다음</span><span class="sxs-lookup"><span data-stu-id="b2652-309">Next</span></span>](using-templatefields-in-the-gridview-control-cs.md)
