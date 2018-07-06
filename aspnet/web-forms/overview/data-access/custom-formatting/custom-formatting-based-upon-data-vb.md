---
uid: web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-vb
title: 사용자 지정 형식 지정 데이터를 기반으로 (VB) | Microsoft Docs
author: rick-anderson
description: GridView, DetailsView 또는 FormView에 바인딩된 데이터를 기반으로 형식을 조정 하는 여러 가지 방법으로 수행할 수 있습니다. 이 자습서에서는 l을 합니다...
ms.author: aspnetcontent
ms.date: 03/31/2010
ms.assetid: df5a1525-386f-4632-972c-57b199870bc3
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-vb
msc.type: authoredcontent
ms.openlocfilehash: d55a9ece22805d7f5d248e81a01d059dbde0ee18
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37809591"
---
<a name="custom-formatting-based-upon-data-vb"></a><span data-ttu-id="08a20-104">사용자 지정 형식 지정 데이터를 기반으로 (VB)</span><span class="sxs-lookup"><span data-stu-id="08a20-104">Custom Formatting Based Upon Data (VB)</span></span>
====================
<span data-ttu-id="08a20-105">[Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="08a20-105">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

<span data-ttu-id="08a20-106">[샘플 앱을 다운로드](http://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_11_VB.exe) 또는 [PDF 다운로드](custom-formatting-based-upon-data-vb/_static/datatutorial11vb1.pdf)</span><span class="sxs-lookup"><span data-stu-id="08a20-106">[Download Sample App](http://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_11_VB.exe) or [Download PDF](custom-formatting-based-upon-data-vb/_static/datatutorial11vb1.pdf)</span></span>

> <span data-ttu-id="08a20-107">GridView, DetailsView 또는 FormView에 바인딩된 데이터를 기반으로 형식을 조정 하는 여러 가지 방법으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-107">Adjusting the format of the GridView, DetailsView, or FormView based upon the data bound to it can be accomplished in multiple ways.</span></span> <span data-ttu-id="08a20-108">이 자습서에서는 데이터 바인딩된 데이터 바인딩 및 RowDataBound 이벤트 처리기를 사용 하 여 서식 지정을 수행 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-108">In this tutorial we'll look at how to accomplish data bound formatting through the use of the DataBound and RowDataBound event handlers.</span></span>


## <a name="introduction"></a><span data-ttu-id="08a20-109">소개</span><span class="sxs-lookup"><span data-stu-id="08a20-109">Introduction</span></span>

<span data-ttu-id="08a20-110">GridView, DetailsView 및 FormView 컨트롤의 모양은 다양 한 스타일 관련 속성을 통해 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-110">The appearance of the GridView, DetailsView, and FormView controls can be customized through a myriad of style-related properties.</span></span> <span data-ttu-id="08a20-111">등의 속성 `CssClass`, `Font`, `BorderWidth`, `BorderStyle`, `BorderColor`를 `Width`, 및 `Height`, 특히 일반 렌더링 된 컨트롤의 모양을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-111">Properties like `CssClass`, `Font`, `BorderWidth`, `BorderStyle`, `BorderColor`, `Width`, and `Height`, among others, dictate the general appearance of the rendered control.</span></span> <span data-ttu-id="08a20-112">속성을 포함 하 여 `HeaderStyle`, `RowStyle`, `AlternatingRowStyle`, 스타일 설정과 특정 섹션에 적용할 수 있도록 다른 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-112">Properties including `HeaderStyle`, `RowStyle`, `AlternatingRowStyle`, and others allow these same style settings to be applied to particular sections.</span></span> <span data-ttu-id="08a20-113">마찬가지로, 다음 스타일 설정은 필드 수준에서 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-113">Likewise, these style settings can be applied at the field level.</span></span>

<span data-ttu-id="08a20-114">대부분의 시나리오에서 그러나 형식 지정 요구 사항에 따라 달라 표시 된 데이터의 값.</span><span class="sxs-lookup"><span data-stu-id="08a20-114">In many scenarios though, the formatting requirements depend upon the value of the displayed data.</span></span> <span data-ttu-id="08a20-115">예를 들어 강조 하기 위해 단순하게 개 제품을 주식형, 제품 정보를 나열 하는 보고서 설정할 수 인 제품에 노란색 배경색 `UnitsInStock` 고 `UnitsOnOrder` 필드는 모두 0입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-115">For example, to draw attention to out of stock products, a report listing product information might set the background color to yellow for those products whose `UnitsInStock` and `UnitsOnOrder` fields are both equal to 0.</span></span> <span data-ttu-id="08a20-116">비용이 많이 드는 products를 강조 하기 위해 굵은 글꼴로 둘 $75.00 비용 해당 제품의 가격을 표시 하려면 원하는 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-116">To highlight the more expensive products, we may want to display the prices of those products costing more than $75.00 in a bold font.</span></span>

<span data-ttu-id="08a20-117">GridView, DetailsView 또는 FormView에 바인딩된 데이터를 기반으로 형식을 조정 하는 여러 가지 방법으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-117">Adjusting the format of the GridView, DetailsView, or FormView based upon the data bound to it can be accomplished in multiple ways.</span></span> <span data-ttu-id="08a20-118">데이터 바인딩된 사용 하 여 서식 지정을 수행 하는 방법을 살펴보겠습니다이 자습서는 `DataBound` 및 `RowDataBound` 이벤트 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-118">In this tutorial we'll look at how to accomplish data bound formatting through the use of the `DataBound` and `RowDataBound` event handlers.</span></span> <span data-ttu-id="08a20-119">다음 자습서에서는 또 다른 방법은 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-119">In the next tutorial we'll explore an alternative approach.</span></span>

## <a name="using-the-detailsview-controlsdataboundevent-handler"></a><span data-ttu-id="08a20-120">DetailsView 컨트롤을 사용 하 여`DataBound`이벤트 처리기</span><span class="sxs-lookup"><span data-stu-id="08a20-120">Using the DetailsView Control's`DataBound`Event Handler</span></span>

<span data-ttu-id="08a20-121">때 데이터에 바인딩되어 DetailsView를 데이터 소스 컨트롤에서 또는 프로그래밍 방식으로 데이터를 컨트롤의 할당을 통해 `DataSource` 속성과 호출 해당 `DataBind()` 메서드에서 다음 일련의 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-121">When data is bound to a DetailsView, either from a data source control or through programmatically assigning data to the control's `DataSource` property and calling its `DataBind()` method, the following sequence of steps occur:</span></span>

1. <span data-ttu-id="08a20-122">데이터 웹 컨트롤의 `DataBinding` 이벤트가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-122">The data Web control's `DataBinding` event fires.</span></span>
2. <span data-ttu-id="08a20-123">데이터를 데이터 웹 컨트롤에 바인딩되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-123">The data is bound to the data Web control.</span></span>
3. <span data-ttu-id="08a20-124">데이터 웹 컨트롤의 `DataBound` 이벤트가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-124">The data Web control's `DataBound` event fires.</span></span>

<span data-ttu-id="08a20-125">1 단계와 3 단계는 이벤트 처리기를 통해 직후 사용자 지정 논리를 주입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-125">Custom logic can be injected immediately after steps 1 and 3 through an event handler.</span></span> <span data-ttu-id="08a20-126">에 대 한 이벤트 처리기를 만들어는 `DataBound` 이벤트 데이터 웹 컨트롤에 바인딩되고 필요에 따라 형식을 조정 된 데이터 프로그래밍 방식으로 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-126">By creating an event handler for the `DataBound` event we can programmatically determine the data that has been bound to the data Web control and adjust the formatting as needed.</span></span> <span data-ttu-id="08a20-127">보겠습니다 보여 주기 위해 제품에 대 한 일반 정보를 표시 하지만 나타납니다 DetailsView 만듭니다는 `UnitPrice` 값을 ***굵게, 기울임꼴 글꼴*** $75.00 초과 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="08a20-127">To illustrate this let's create a DetailsView that will list general information about a product, but will display the `UnitPrice` value in a ***bold, italic font*** if it exceeds $75.00.</span></span>

## <a name="step-1-displaying-the-product-information-in-a-detailsview"></a><span data-ttu-id="08a20-128">1 단계:는 DetailsView에서 제품 정보 표시</span><span class="sxs-lookup"><span data-stu-id="08a20-128">Step 1: Displaying the Product Information in a DetailsView</span></span>

<span data-ttu-id="08a20-129">열기는 `CustomColors.aspx` 페이지에서 `CustomFormatting` 폴더를 디자이너 도구 상자에서 DetailsView 컨트롤을 끌어, 설정 해당 `ID` 속성 값을 `ExpensiveProductsPriceInBoldItalic`를 호출 하는 새 ObjectDataSource 컨트롤을 바인딩할는 `ProductsBLL` 클래스의 `GetProducts()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="08a20-129">Open the `CustomColors.aspx` page in the `CustomFormatting` folder, drag a DetailsView control from the Toolbox onto the Designer, set its `ID` property value to `ExpensiveProductsPriceInBoldItalic`, and bind it to a new ObjectDataSource control that invokes the `ProductsBLL` class's `GetProducts()` method.</span></span> <span data-ttu-id="08a20-130">이 작업을 수행 하는 것에 대 한 자세한 단계는 이전 자습서에서 자세히 검사 하는 이후 간단한 설명을 위해 여기 생략 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-130">The detailed steps for accomplishing this are omitted here for brevity since we examined them in detail in previous tutorials.</span></span>

<span data-ttu-id="08a20-131">ObjectDataSource DetailsView에 바인딩된 했습니다 되 면 잠시 필드 목록을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-131">Once you've bound the ObjectDataSource to the DetailsView, take a moment to modify the field list.</span></span> <span data-ttu-id="08a20-132">제거 하기로 했습니다 합니다 `ProductID`, `SupplierID`, `CategoryID`, `UnitsInStock`, `UnitsOnOrder`, `ReorderLevel`, 및 `Discontinued` BoundFields 이름을 변경 하 고 나머지 BoundFields 서식이 다시 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-132">I've opted to remove the `ProductID`, `SupplierID`, `CategoryID`, `UnitsInStock`, `UnitsOnOrder`, `ReorderLevel`, and `Discontinued` BoundFields and renamed and reformatted the remaining BoundFields.</span></span> <span data-ttu-id="08a20-133">도 삭제 합니다 `Width` 및 `Height` 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-133">I also cleared out the `Width` and `Height` settings.</span></span> <span data-ttu-id="08a20-134">DetailsView 레코드가 하나만 표시 되므로 최종 사용자가 모든 제품을 볼 수 있도록 하기 위해 페이징 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-134">Since the DetailsView displays only a single record, we need to enable paging in order to allow the end user to view all of the products.</span></span> <span data-ttu-id="08a20-135">이렇게 하려면 DetailsView의 스마트 태그의 페이징 사용 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-135">Do so by checking the Enable Paging checkbox in the DetailsView's smart tag.</span></span>


<span data-ttu-id="08a20-136">[![그림 1: 확인란을 사용 하도록 설정 페이징 DetailsView의 스마트 태그](custom-formatting-based-upon-data-vb/_static/image2.png)](custom-formatting-based-upon-data-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="08a20-136">[![Figure 1: Check the Enable Paging Checkbox in the DetailsView's Smart Tag](custom-formatting-based-upon-data-vb/_static/image2.png)](custom-formatting-based-upon-data-vb/_static/image1.png)</span></span>

<span data-ttu-id="08a20-137">**그림 1**: 그림 1: 확인란을 사용 하도록 설정 페이징 DetailsView의 스마트 태그 ([큰 이미지를 보려면 클릭](custom-formatting-based-upon-data-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="08a20-137">**Figure 1**: Figure 1: Check the Enable Paging Checkbox in the DetailsView's Smart Tag ([Click to view full-size image](custom-formatting-based-upon-data-vb/_static/image3.png))</span></span>


<span data-ttu-id="08a20-138">이러한 변경 내용은 다음 DetailsView 태그 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-138">After these changes, the DetailsView markup will be:</span></span>


[!code-aspx[Main](custom-formatting-based-upon-data-vb/samples/sample1.aspx)]

<span data-ttu-id="08a20-139">시간을 내어이 페이지를 브라우저에서 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-139">Take a moment to test out this page in your browser.</span></span>


<span data-ttu-id="08a20-140">[![DetailsView 컨트롤을 한 번에 한 제품 표시](custom-formatting-based-upon-data-vb/_static/image5.png)](custom-formatting-based-upon-data-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="08a20-140">[![The DetailsView Control Displays One Product at a Time](custom-formatting-based-upon-data-vb/_static/image5.png)](custom-formatting-based-upon-data-vb/_static/image4.png)</span></span>

<span data-ttu-id="08a20-141">**그림 2**: The DetailsView 컨트롤 표시 한 제품 번 ([큰 이미지를 보려면 클릭](custom-formatting-based-upon-data-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="08a20-141">**Figure 2**: The DetailsView Control Displays One Product at a Time ([Click to view full-size image](custom-formatting-based-upon-data-vb/_static/image6.png))</span></span>


## <a name="step-2-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a><span data-ttu-id="08a20-142">2 단계: 데이터 바인딩된 이벤트 처리기에서 데이터의 값을 프로그래밍 방식으로 결정</span><span class="sxs-lookup"><span data-stu-id="08a20-142">Step 2: Programmatically Determining the Value of the Data in the DataBound Event Handler</span></span>

<span data-ttu-id="08a20-143">이러한 제품에 대해 굵게, 기울임꼴 글꼴의 가격을 표시 하기 위해 해당 `UnitPrice` 75.00 달러를 초과 하는 값을 프로그래밍 방식으로 결정을 해야는 `UnitPrice` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-143">In order to display the price in a bold, italic font for those products whose `UnitPrice` value exceeds $75.00, we need to first be able to programmatically determine the `UnitPrice` value.</span></span> <span data-ttu-id="08a20-144">DetailsView에 대 한이 수행할 수 있습니다는 `DataBound` 이벤트 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-144">For the DetailsView, this can be accomplished in the `DataBound` event handler.</span></span> <span data-ttu-id="08a20-145">이벤트를 만들면 처리기 디자이너에서 DetailsView 클릭 속성 창으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-145">To create the event handler click on the DetailsView in the Designer then navigate to the Properties window.</span></span> <span data-ttu-id="08a20-146">F4 키를 눌러를 불러오려면 없으면 표시할지 보기 메뉴로 이동 하 고 속성 창 메뉴 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-146">Press F4 to bring it up, if it's not visible, or go to the View menu and select the Properties Window menu option.</span></span> <span data-ttu-id="08a20-147">속성 창에서 DetailsView의 이벤트를 나열 하려면 번개 모양 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-147">From the Properties window, click on the lightning bolt icon to list the DetailsView's events.</span></span> <span data-ttu-id="08a20-148">다음으로 두 번 클릭 합니다 `DataBound` 이벤트 또는 이벤트 처리기를 만들려는 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-148">Next, either double-click the `DataBound` event or type in the name of the event handler you want to create.</span></span>


![DataBound 이벤트에 대 한 이벤트 처리기 만들기](custom-formatting-based-upon-data-vb/_static/image7.png)

<span data-ttu-id="08a20-150">**그림 3**: 만들기에 대 한 이벤트 처리기는 `DataBound` 이벤트</span><span class="sxs-lookup"><span data-stu-id="08a20-150">**Figure 3**: Create an Event Handler for the `DataBound` Event</span></span>


> [!NOTE]
> <span data-ttu-id="08a20-151">또한 ASP.NET 페이지의 코드 부분에서 이벤트 처리기를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-151">You can also create an event handler from the ASP.NET page's code portion.</span></span> <span data-ttu-id="08a20-152">페이지의 맨 위에 있는 두 개의 드롭다운 목록을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-152">There you'll find two drop-down lists at the top of the page.</span></span> <span data-ttu-id="08a20-153">왼쪽된 드롭다운 목록에서 개체를 선택 하 고 오른쪽 드롭다운 목록에서 Visual Studio에 대 한 처리기를 만들려는 이벤트에서 자동으로 적절 한 이벤트 처리기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-153">Select the object from the left drop-down list and the event you want to create a handler for from the right drop-down list and Visual Studio will automatically create the appropriate event handler.</span></span>


<span data-ttu-id="08a20-154">이렇게 자동으로 이벤트 처리기를 만들고 여기서 추가한 코드 부분을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-154">Doing so will automatically create the event handler and take you to the code portion where it has been added.</span></span> <span data-ttu-id="08a20-155">이 시점에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-155">At this point you will see:</span></span>


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample2.vb)]

<span data-ttu-id="08a20-156">DetailsView로 바인딩된 데이터를 통해 액세스할 수 있습니다는 `DataItem` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-156">The data bound to the DetailsView can be accessed via the `DataItem` property.</span></span> <span data-ttu-id="08a20-157">강력한 DataRow 인스턴스의 컬렉션으로 이루어진 강력한 형식화 된 DataTable에이 컨트롤을 바인딩하는 것을 기억 하십시오.</span><span class="sxs-lookup"><span data-stu-id="08a20-157">Recall that we are binding our controls to a strongly-typed DataTable, which is composed of a collection of strongly-typed DataRow instances.</span></span> <span data-ttu-id="08a20-158">첫 번째 DataTable에서 DataRow는 DetailsView에 할당 된 DataTable DetailsView에 바인딩되면 `DataItem` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-158">When the DataTable is bound to the DetailsView, the first DataRow in the DataTable is assigned to the DetailsView's `DataItem` property.</span></span> <span data-ttu-id="08a20-159">특히 합니다 `DataItem` 속성에 할당 되는 `DataRowView` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-159">Specifically, the `DataItem` property is assigned a `DataRowView` object.</span></span> <span data-ttu-id="08a20-160">사용할 수 있습니다는 `DataRowView`의 `Row` 인 기본 DataRow 개체에 대 한 액세스를 가져올 속성을 보면 `ProductsRow` 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="08a20-160">We can use the `DataRowView`'s `Row` property to get access to the underlying DataRow object, which is actually a `ProductsRow` instance.</span></span> <span data-ttu-id="08a20-161">이 있으면 `ProductsRow` 인스턴스 단순히 개체의 속성 값을 검사 하 여이 결정을 내릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-161">Once we have this `ProductsRow` instance we can make our decision by simply inspecting the object's property values.</span></span>

<span data-ttu-id="08a20-162">다음 코드를 확인 하는 방법을 보여 줍니다 여부는 `UnitPrice` DetailsView 컨트롤에 바인딩된 값 $75.00 보다 큽니다.:</span><span class="sxs-lookup"><span data-stu-id="08a20-162">The following code illustrates how to determine whether the `UnitPrice` value bound to the DetailsView control is greater than $75.00:</span></span>


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample3.vb)]

> [!NOTE]
> <span data-ttu-id="08a20-163">이후 `UnitPrice` 있을 수 있습니다를 `NULL` 값 데이터베이스에 먼저 확인을 사용 하 여 총비율 되지 있는지 확인을 `NULL` 값에 액세스 하기 전에 `ProductsRow`의 `UnitPrice` 속성.</span><span class="sxs-lookup"><span data-stu-id="08a20-163">Since `UnitPrice` can have a `NULL` value in the database, we first check to make sure that we're not dealing with a `NULL` value before accessing the `ProductsRow`'s `UnitPrice` property.</span></span> <span data-ttu-id="08a20-164">이 검사는 중요 한 때문에 액세스 하려고 하는 경우는 `UnitPrice` 에 있을 때 속성을 `NULL` 값을 `ProductsRow` 개체를 throw 합니다를 [StrongTypingException 예외](https://msdn.microsoft.com/library/system.data.strongtypingexception.aspx).</span><span class="sxs-lookup"><span data-stu-id="08a20-164">This check is important because if we attempt to access the `UnitPrice` property when it has a `NULL` value the `ProductsRow` object will throw a [StrongTypingException exception](https://msdn.microsoft.com/library/system.data.strongtypingexception.aspx).</span></span>


## <a name="step-3-formatting-the-unitprice-value-in-the-detailsview"></a><span data-ttu-id="08a20-165">3 단계: DetailsView UnitPrice 값 서식 지정</span><span class="sxs-lookup"><span data-stu-id="08a20-165">Step 3: Formatting the UnitPrice Value in the DetailsView</span></span>

<span data-ttu-id="08a20-166">이 시점에서 확인할 수 있습니다 여부는 `UnitPrice` DetailsView에 바인딩된 값 $75.00를 초과 하는 값이 있지만 아직 DetailsView를 프로그래밍 방식으로 조정 하는 방법을 보려면의 서식 지정 적절 하 게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-166">At this point we can determine whether the `UnitPrice` value bound to the DetailsView has a value that exceeds $75.00, but we've yet to see how to programmatically adjust the DetailsView's formatting accordingly.</span></span> <span data-ttu-id="08a20-167">DetailsView에 있는 전체 행의 서식 지정을 수정 하려면 프로그래밍 방식으로 액세스를 사용 하 여 행 `DetailsViewID.Rows(index)`사용 하 여 액세스를 특정 셀을 수정 하려면 `DetailsViewID.Rows(index).Cells(index)`합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-167">To modify the formatting of an entire row in the DetailsView, programmatically access the row using `DetailsViewID.Rows(index)`; to modify a particular cell, access use `DetailsViewID.Rows(index).Cells(index)`.</span></span> <span data-ttu-id="08a20-168">행 또는 셀에 대 한 참조가 있으면 해당 스타일 관련 속성을 설정 하 여 모양을 다음 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-168">Once we have a reference to the row or cell we can then adjust its appearance by setting its style-related properties.</span></span>

<span data-ttu-id="08a20-169">행을 프로그래밍 방식으로 액세스 0부터 시작 하는 행의 인덱스를 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-169">Accessing a row programmatically requires that you know the row's index, which starts at 0.</span></span> <span data-ttu-id="08a20-170">합니다 `UnitPrice` 행은 4의 인덱스를 지정 하 고 프로그래밍 방식으로 액세스할 수 있도록 DetailsView의 다섯 번째 행을 사용 하 여 `ExpensiveProductsPriceInBoldItalic.Rows(4)`입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-170">The `UnitPrice` row is the fifth row in the DetailsView, giving it an index of 4 and making it programmatically accessible using `ExpensiveProductsPriceInBoldItalic.Rows(4)`.</span></span> <span data-ttu-id="08a20-171">이 시점에서 다음 코드를 사용 하 여 굵게, 기울임꼴 글꼴에 표시 되는 전체 행의 콘텐츠가 있을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-171">At this point we could have the entire row's content displayed in a bold, italic font by using the following code:</span></span>


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample4.vb)]

<span data-ttu-id="08a20-172">그러나 그러면 *둘 다* 레이블 (Price) 및 굵게 및 기울임꼴 값입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-172">However, this will make *both* the label (Price) and the value bold and italic.</span></span> <span data-ttu-id="08a20-173">값만 굵게 및 기울임꼴 다음을 사용 하 여 수행할 수 있는 행의 두 번째 셀에 서식을 적용 하기 위해서 필요를 확인 하려면:</span><span class="sxs-lookup"><span data-stu-id="08a20-173">If we want to make just the value bold and italic we need to apply this formatting to the second cell in the row, which can be accomplished using the following:</span></span>


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample5.vb)]

<span data-ttu-id="08a20-174">지금 있으므로 자습서를 명확히 구분 된 렌더링 된 태그 및 스타일 관련 정보를 유지 하기 위해 스타일 시트를 사용 있어야, 있으므로 위와 같이 보겠습니다 대신 특정 스타일 속성을 설정 하는 대신 CSS 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-174">Since our tutorials thus far have used stylesheets to maintain a clean separation between the rendered markup and style-related information, rather than setting the specific style properties as shown above let's instead use a CSS class.</span></span> <span data-ttu-id="08a20-175">엽니다는 `Styles.css` 스타일 시트 라는 새 CSS 클래스를 추가 하 고 `ExpensivePriceEmphasis` 다음 정의 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="08a20-175">Open the `Styles.css` stylesheet and add a new CSS class named `ExpensivePriceEmphasis` with the following definition:</span></span>


[!code-css[Main](custom-formatting-based-upon-data-vb/samples/sample6.css)]

<span data-ttu-id="08a20-176">그런 다음 합니다 `DataBound` 셀의을 설정 하는 이벤트 처리기 `CssClass` 속성을 `ExpensivePriceEmphasis`입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-176">Then, in the `DataBound` event handler, set the cell's `CssClass` property to `ExpensivePriceEmphasis`.</span></span> <span data-ttu-id="08a20-177">다음 코드에서는 `DataBound` 전체에서 이벤트 처리기:</span><span class="sxs-lookup"><span data-stu-id="08a20-177">The following code shows the `DataBound` event handler in its entirety:</span></span>


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample7.vb)]

<span data-ttu-id="08a20-178">가격은 일반 글꼴로 표시 됩니다 Chai 75.00 달러 비용에서 볼 때 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="08a20-178">When viewing Chai, which costs less than $75.00, the price is displayed in a normal font (see Figure 4).</span></span> <span data-ttu-id="08a20-179">그러나 $97.00 가격이 있는 Mishi 산호세 Niku 보기 가격에에서 표시 됩니다 굵게, 기울임꼴 글꼴 (그림 5 참조).</span><span class="sxs-lookup"><span data-stu-id="08a20-179">However, when viewing Mishi Kobe Niku, which has a price of $97.00, the price is displayed in a bold, italic font (see Figure 5).</span></span>


<span data-ttu-id="08a20-180">[![$75.00 보다 적은 가격 보통 글꼴로 표시 됩니다.](custom-formatting-based-upon-data-vb/_static/image9.png)](custom-formatting-based-upon-data-vb/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="08a20-180">[![Prices Less than $75.00 are Displayed in a Normal Font](custom-formatting-based-upon-data-vb/_static/image9.png)](custom-formatting-based-upon-data-vb/_static/image8.png)</span></span>

<span data-ttu-id="08a20-181">**그림 4**: $75.00 보다 적은 가격 보통 글꼴로 표시 됩니다 ([큰 이미지를 보려면 클릭](custom-formatting-based-upon-data-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="08a20-181">**Figure 4**: Prices Less than $75.00 are Displayed in a Normal Font ([Click to view full-size image](custom-formatting-based-upon-data-vb/_static/image10.png))</span></span>


<span data-ttu-id="08a20-182">[![비용이 많이 드는 제품의 가격은 기울임꼴 글꼴을 굵게 표시 됩니다.](custom-formatting-based-upon-data-vb/_static/image12.png)](custom-formatting-based-upon-data-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="08a20-182">[![Expensive Products' Prices are Displayed in a Bold, Italic Font](custom-formatting-based-upon-data-vb/_static/image12.png)](custom-formatting-based-upon-data-vb/_static/image11.png)</span></span>

<span data-ttu-id="08a20-183">**그림 5**: 비용이 많이 드는 제품의 가격은 기울임꼴 글꼴을 굵게 표시 됩니다 ([큰 이미지를 보려면 클릭](custom-formatting-based-upon-data-vb/_static/image13.png))</span><span class="sxs-lookup"><span data-stu-id="08a20-183">**Figure 5**: Expensive Products' Prices are Displayed in a Bold, Italic Font ([Click to view full-size image](custom-formatting-based-upon-data-vb/_static/image13.png))</span></span>


## <a name="using-the-formview-controlsdataboundevent-handler"></a><span data-ttu-id="08a20-184">FormView 컨트롤을 사용 하 여`DataBound`이벤트 처리기</span><span class="sxs-lookup"><span data-stu-id="08a20-184">Using the FormView Control's`DataBound`Event Handler</span></span>

<span data-ttu-id="08a20-185">DetailsView 만들기에 대 한 FormView에 바인딩된 내부 데이터를 확인 하기 위한 단계는 동일 하 게는 `DataBound` 이벤트 처리기를 캐스팅 합니다 `DataItem` 속성을 적절 한 개체 형식 컨트롤에 바인딩되고 진행 하는 방법을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-185">The steps for determining the underlying data bound to a FormView are identical to those for a DetailsView create a `DataBound` event handler, cast the `DataItem` property to the appropriate object type bound to the control, and determine how to proceed.</span></span> <span data-ttu-id="08a20-186">하지만 FormView 및 DetailsView 다 해당 사용자 인터페이스의 모양을 업데이트 되는 방식을에서.</span><span class="sxs-lookup"><span data-stu-id="08a20-186">The FormView and DetailsView differ, however, in how their user interface's appearance is updated.</span></span>

<span data-ttu-id="08a20-187">FormView 모든 BoundFields 포함 하지 않으며 따라서 부족을 `Rows` 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-187">The FormView does not contain any BoundFields and therefore lacks the `Rows` collection.</span></span> <span data-ttu-id="08a20-188">정적 HTML의 혼합을 포함할 수 있는 템플릿의 FormView가 구성 하는 대신 웹 컨트롤 및 데이터 바인딩 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-188">Instead, a FormView is composed of templates, which can contain a mix of static HTML, Web controls, and databinding syntax.</span></span> <span data-ttu-id="08a20-189">FormView의 스타일을 일반적으로 조정 FormView의 템플릿 내에서 웹 컨트롤의 하나 이상의 스타일을 조정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-189">Adjusting the style of a FormView typically involves adjusting the style of one or more of the Web controls within the FormView's templates.</span></span>

<span data-ttu-id="08a20-190">이 예에 표시 해 보겠습니다 목록 제품 FormView 보겠습니다 앞의 예에서 이번에서 같이 사용 하 여 제품 이름 및 단위 10 보다 작거나 경우 빨간색 글꼴로 표시 되는 재고 단위를 사용 하 여 재고.</span><span class="sxs-lookup"><span data-stu-id="08a20-190">To illustrate this, let's use a FormView to list products like in the previous example, but this time let's display just the product name and units in stock with the units in stock displayed in a red font if it is less than or equal to 10.</span></span>

## <a name="step-4-displaying-the-product-information-in-a-formview"></a><span data-ttu-id="08a20-191">FormView에서 제품 정보를 표시 하는 4 단계:</span><span class="sxs-lookup"><span data-stu-id="08a20-191">Step 4: Displaying the Product Information in a FormView</span></span>

<span data-ttu-id="08a20-192">FormView를 추가 합니다 `CustomColors.aspx` 집합과 DetailsView 아래 페이지 해당 `ID` 속성을 `LowStockedProductsInRed`입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-192">Add a FormView to the `CustomColors.aspx` page beneath the DetailsView and set its `ID` property to `LowStockedProductsInRed`.</span></span> <span data-ttu-id="08a20-193">FormView 이전 단계에서 만든 ObjectDataSource 컨트롤에 바인딩하십시오.</span><span class="sxs-lookup"><span data-stu-id="08a20-193">Bind the FormView to the ObjectDataSource control created from the previous step.</span></span> <span data-ttu-id="08a20-194">이렇게 하면 만들어집니다는 `ItemTemplate`, `EditItemTemplate`, 및 `InsertItemTemplate` FormView에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-194">This will create an `ItemTemplate`, `EditItemTemplate`, and `InsertItemTemplate` for the FormView.</span></span> <span data-ttu-id="08a20-195">제거는 `EditItemTemplate` 및 `InsertItemTemplate` 간소화 및 합니다 `ItemTemplate` 포함 하도록만 `ProductName` 및 `UnitsInStock` 자신의 적절 하 게 명명 된 레이블 컨트롤의 각 값입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-195">Remove the `EditItemTemplate` and `InsertItemTemplate` and simplify the `ItemTemplate` to include just the `ProductName` and `UnitsInStock` values, each in their own appropriately-named Label controls.</span></span> <span data-ttu-id="08a20-196">이전 예제에서 DetailsView와 마찬가지로 또한 FormView의 스마트 태그의 페이징 사용 확인란을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-196">As with the DetailsView from the earlier example, also check the Enable Paging checkbox in the FormView's smart tag.</span></span>

<span data-ttu-id="08a20-197">이러한 편집 후 FormView의 태그는 다음과 비슷하게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-197">After these edits your FormView's markup should look similar to the following:</span></span>


[!code-aspx[Main](custom-formatting-based-upon-data-vb/samples/sample8.aspx)]

<span data-ttu-id="08a20-198">`ItemTemplate` 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-198">Note that the `ItemTemplate` contains:</span></span>

- <span data-ttu-id="08a20-199">**정적 HTML** 텍스트를 "제품:" 및 "재고 단위:"와 함께 합니다 `<br />` 및 `<b>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-199">**Static HTML** the text "Product:" and "Units In Stock:" along with the `<br />` and `<b>` elements.</span></span>
- <span data-ttu-id="08a20-200">**웹 컨트롤** 두 레이블 컨트롤 `ProductNameLabel` 고 `UnitsInStockLabel`입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-200">**Web controls** the two Label controls, `ProductNameLabel` and `UnitsInStockLabel`.</span></span>
- <span data-ttu-id="08a20-201">**데이터 바인딩 구문을** 는 `<%# Bind("ProductName") %>` 하 고 `<%# Bind("UnitsInStock") %>` 레이블 컨트롤의 이러한 필드에서 값을 할당 하는 구문은 `Text` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-201">**Databinding syntax** the `<%# Bind("ProductName") %>` and `<%# Bind("UnitsInStock") %>` syntax, which assigns the values from these fields to the Label controls' `Text` properties.</span></span>

## <a name="step-5-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a><span data-ttu-id="08a20-202">5 단계: 데이터 바인딩된 이벤트 처리기에서 데이터의 값을 프로그래밍 방식으로 결정</span><span class="sxs-lookup"><span data-stu-id="08a20-202">Step 5: Programmatically Determining the Value of the Data in the DataBound Event Handler</span></span>

<span data-ttu-id="08a20-203">전체 FormView의 태그를 사용 하 여 프로그래밍 방식으로 확인 하는 경우 다음 단계는는 `UnitsInStock` 10 보다 작거나 같은 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-203">With the FormView's markup complete, the next step is to programmatically determine if the `UnitsInStock` value is less than or equal to 10.</span></span> <span data-ttu-id="08a20-204">DetailsView를 사용 하 여 처럼 FormView와 정확히 동일한 방식으로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-204">This is accomplished in the exact same manner with the FormView as it was with the DetailsView.</span></span> <span data-ttu-id="08a20-205">FormView의에 대 한 이벤트 처리기를 만들어 시작 `DataBound` 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-205">Start by creating an event handler for the FormView's `DataBound` event.</span></span>


![데이터 바인딩된 이벤트 처리기 만들기](custom-formatting-based-upon-data-vb/_static/image14.png)

<span data-ttu-id="08a20-207">**그림 6**: 만들기는 `DataBound` 이벤트 처리기</span><span class="sxs-lookup"><span data-stu-id="08a20-207">**Figure 6**: Create the `DataBound` Event Handler</span></span>


<span data-ttu-id="08a20-208">처리기 FormView의 캐스팅 하는 이벤트 `DataItem` 속성을를 `ProductsRow` 인스턴스를 확인 하는지 여부를 `UnitsInPrice` 값은 빨간색 글꼴로 표시할 필요는 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-208">In the event handler cast the FormView's `DataItem` property to a `ProductsRow` instance and determine whether the `UnitsInPrice` value is such that we need to display it in a red font.</span></span>


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample9.vb)]

## <a name="step-6-formatting-the-unitsinstocklabel-label-control-in-the-formviews-itemtemplate"></a><span data-ttu-id="08a20-209">6 단계: FormView의 ItemTemplate의 UnitsInStockLabel 레이블 컨트롤 서식 지정</span><span class="sxs-lookup"><span data-stu-id="08a20-209">Step 6: Formatting the UnitsInStockLabel Label Control in the FormView's ItemTemplate</span></span>

<span data-ttu-id="08a20-210">표시 서식을 지정 하는 최종 단계입니다 `UnitsInStock` 빨간색 글꼴로 값 10 이하의 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-210">The final step is to format the displayed `UnitsInStock` value in a red font if the value is 10 or less.</span></span> <span data-ttu-id="08a20-211">프로그래밍 방식으로 액세스 해야 하는 것이 `UnitsInStockLabel` 에서 제어할는 `ItemTemplate` 빨간색에서 텍스트 표시 되도록 스타일 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-211">To accomplish this we need to programmatically access the `UnitsInStockLabel` control in the `ItemTemplate` and set its style properties so that its text is displayed in red.</span></span> <span data-ttu-id="08a20-212">템플릿에서 웹 컨트롤에 액세스 하려면 사용 된 `FindControl("controlID")` 다음과 같이 메서드:</span><span class="sxs-lookup"><span data-stu-id="08a20-212">To access a Web control in a template, use the `FindControl("controlID")` method like this:</span></span>


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample10.vb)]

<span data-ttu-id="08a20-213">컨트롤 레이블 액세스 하려는 예제 `ID` 값은 `UnitsInStockLabel`이므로 사용 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-213">For our example we want to access a Label control whose `ID` value is `UnitsInStockLabel`, so we'd use:</span></span>


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample11.vb)]

<span data-ttu-id="08a20-214">웹 컨트롤에 대 한 프로그래밍 방식으로 참조 한 후 필요에 따라 해당 스타일 관련 속성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-214">Once we have a programmatic reference to the Web control, we can modify its style-related properties as needed.</span></span> <span data-ttu-id="08a20-215">CSS 클래스 이전 예에서 만들었습니다 처럼 `Styles.css` 라는 `LowUnitsInStockEmphasis`합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-215">As with the earlier example, I've created a CSS class in `Styles.css` named `LowUnitsInStockEmphasis`.</span></span> <span data-ttu-id="08a20-216">이 스타일 레이블을 웹 컨트롤에 적용할 설정 해당 `CssClass` 속성 적절 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-216">To apply this style to the Label Web control, set its `CssClass` property accordingly.</span></span>


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample12.vb)]

> [!NOTE]
> <span data-ttu-id="08a20-217">프로그래밍 방식으로 사용 하 여 웹 컨트롤에 액세스 하는 템플릿 서식 지정에 대 한 구문을 `FindControl("controlID")` 스타일 관련 속성을 다음 설정도 사용할 수 있습니다 사용 하는 경우 [TemplateFields](https://msdn.microsoft.com/library/system.web.ui.webcontrols.templatefield(VS.80).aspx) DetailsView 또는 GridView 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-217">The syntax for formatting a template programmatically accessing the Web control using `FindControl("controlID")` and then setting its style-related properties can also be used when using [TemplateFields](https://msdn.microsoft.com/library/system.web.ui.webcontrols.templatefield(VS.80).aspx) in the DetailsView or GridView controls.</span></span> <span data-ttu-id="08a20-218">다음 자습서에서 TemplateFields를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-218">We'll examine TemplateFields in our next tutorial.</span></span>


<span data-ttu-id="08a20-219">제품을 볼 때 그림 7 FormView에 나와 있는 `UnitsInStock` 그림 8에 있는 제품에 해당 값이 10 보다 작은 값이 10 보다 큰 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-219">Figures 7 shows the FormView when viewing a product whose `UnitsInStock` value is greater than 10, while the product in Figure 8 has its value less than 10.</span></span>


<span data-ttu-id="08a20-220">[![제품으로는 충분히 큰 Units In Stock, 사용자 지정 서식 없이 적용 됩니다.](custom-formatting-based-upon-data-vb/_static/image16.png)](custom-formatting-based-upon-data-vb/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="08a20-220">[![For Products With a Sufficiently Large Units In Stock, No Custom Formatting is Applied](custom-formatting-based-upon-data-vb/_static/image16.png)](custom-formatting-based-upon-data-vb/_static/image15.png)</span></span>

<span data-ttu-id="08a20-221">**그림 7**:에 대 한 제품으로는 충분히 큰 Units In Stock, 사용자 지정 서식 없이 적용 됩니다 ([큰 이미지를 보려면 클릭](custom-formatting-based-upon-data-vb/_static/image17.png))</span><span class="sxs-lookup"><span data-stu-id="08a20-221">**Figure 7**: For Products With a Sufficiently Large Units In Stock, No Custom Formatting is Applied ([Click to view full-size image](custom-formatting-based-upon-data-vb/_static/image17.png))</span></span>


<span data-ttu-id="08a20-222">[![재고 수 단위 값에 대 한 해당 제품으로 10 개 이하의의 빨간색으로 표시 됩니다.](custom-formatting-based-upon-data-vb/_static/image19.png)](custom-formatting-based-upon-data-vb/_static/image18.png)</span><span class="sxs-lookup"><span data-stu-id="08a20-222">[![The Units in Stock Number is Shown in Red for Those Products With Values of 10 or Less](custom-formatting-based-upon-data-vb/_static/image19.png)](custom-formatting-based-upon-data-vb/_static/image18.png)</span></span>

<span data-ttu-id="08a20-223">**그림 8**: 재고 수의 장치는 해당 제품으로의 값이 10 개 이하의 빨간색으로 표시 됩니다 ([큰 이미지를 보려면 클릭](custom-formatting-based-upon-data-vb/_static/image20.png))</span><span class="sxs-lookup"><span data-stu-id="08a20-223">**Figure 8**: The Units in Stock Number is Shown in Red for Those Products With Values of 10 or Less ([Click to view full-size image](custom-formatting-based-upon-data-vb/_static/image20.png))</span></span>


## <a name="formatting-with-the-gridviewsrowdataboundevent"></a><span data-ttu-id="08a20-224">Gridview의 서식 지정`RowDataBound`이벤트</span><span class="sxs-lookup"><span data-stu-id="08a20-224">Formatting with the GridView's`RowDataBound`Event</span></span>

<span data-ttu-id="08a20-225">이전 DetailsView 단계의 시퀀스를 살펴보았습니다 및 FormView 데이터 바인딩 중 진행을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-225">Earlier we examined the sequence of steps the DetailsView and FormView controls progress through during databinding.</span></span> <span data-ttu-id="08a20-226">살펴보겠습니다 다음이 단계를 통해 다시 한 번으로 쉽게 찾아볼.</span><span class="sxs-lookup"><span data-stu-id="08a20-226">Let's look over these steps once again as a refresher.</span></span>

1. <span data-ttu-id="08a20-227">데이터 웹 컨트롤의 `DataBinding` 이벤트가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-227">The data Web control's `DataBinding` event fires.</span></span>
2. <span data-ttu-id="08a20-228">데이터를 데이터 웹 컨트롤에 바인딩되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-228">The data is bound to the data Web control.</span></span>
3. <span data-ttu-id="08a20-229">데이터 웹 컨트롤의 `DataBound` 이벤트가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-229">The data Web control's `DataBound` event fires.</span></span>

<span data-ttu-id="08a20-230">이러한 세 가지 간단한 단계는 단일 레코드를 표시 하므로 FormView 및 DetailsView를 충분히 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-230">These three simple steps are sufficient for the DetailsView and FormView because they display only a single record.</span></span> <span data-ttu-id="08a20-231">표시 하는 gridview *모든* 바인딩된 레코드 2 단계를 좀 더 복잡 하지만 (첫 번째 뿐 아니라 함).</span><span class="sxs-lookup"><span data-stu-id="08a20-231">For the GridView, which displays *all* records bound to it (not just the first), step 2 is a bit more involved.</span></span>

<span data-ttu-id="08a20-232">GridView 열거 데이터 원본을 만들고, 각 레코드에 대해 2 단계에서 한 `GridViewRow` 인스턴스 및 현재 레코드를 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-232">In step 2 the GridView enumerates the data source and, for each record, creates a `GridViewRow` instance and binds the current record to it.</span></span> <span data-ttu-id="08a20-233">각 `GridViewRow` GridView에 추가 두 이벤트가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-233">For each `GridViewRow` added to the GridView, two events are raised:</span></span>

- <span data-ttu-id="08a20-234">**`RowCreated`** 후 발생 합니다 `GridViewRow` 만들었습니다</span><span class="sxs-lookup"><span data-stu-id="08a20-234">**`RowCreated`** fires after the `GridViewRow` has been created</span></span>
- <span data-ttu-id="08a20-235">**`RowDataBound`** 현재 레코드에 바인딩된 후에 발생 합니다 `GridViewRow`합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-235">**`RowDataBound`** fires after the current record has been bound to the `GridViewRow`.</span></span>

<span data-ttu-id="08a20-236">GridView에 대 한 다음, 데이터 바인딩 보다 정확 하 게에서 설명한 단계의 다음 시퀀스:</span><span class="sxs-lookup"><span data-stu-id="08a20-236">For the GridView, then, data binding is more accurately described by the following sequence of steps:</span></span>

1. <span data-ttu-id="08a20-237">GridView의 `DataBinding` 이벤트가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-237">The GridView's `DataBinding` event fires.</span></span>
2. <span data-ttu-id="08a20-238">데이터를 GridView에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-238">The data is bound to the GridView.</span></span>   
  
   <span data-ttu-id="08a20-239">데이터 소스의 각 레코드에 대 한</span><span class="sxs-lookup"><span data-stu-id="08a20-239">For each record in the data source</span></span> 

    1. <span data-ttu-id="08a20-240">만들기는 `GridViewRow` 개체</span><span class="sxs-lookup"><span data-stu-id="08a20-240">Create a `GridViewRow` object</span></span>
    2. <span data-ttu-id="08a20-241">실행 된 `RowCreated` 이벤트</span><span class="sxs-lookup"><span data-stu-id="08a20-241">Fire the `RowCreated` event</span></span>
    3. <span data-ttu-id="08a20-242">레코드를 바인딩하는 `GridViewRow`</span><span class="sxs-lookup"><span data-stu-id="08a20-242">Bind the record to the `GridViewRow`</span></span>
    4. <span data-ttu-id="08a20-243">실행 된 `RowDataBound` 이벤트</span><span class="sxs-lookup"><span data-stu-id="08a20-243">Fire the `RowDataBound` event</span></span>
    5. <span data-ttu-id="08a20-244">추가 된 `GridViewRow` 에 `Rows` 컬렉션</span><span class="sxs-lookup"><span data-stu-id="08a20-244">Add the `GridViewRow` to the `Rows` collection</span></span>
3. <span data-ttu-id="08a20-245">GridView의 `DataBound` 이벤트가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-245">The GridView's `DataBound` event fires.</span></span>

<span data-ttu-id="08a20-246">GridView의 개별 레코드 형식의 사용자 지정 하려면 다음을 생성 해야에 대 한 이벤트 처리기는 `RowDataBound` 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-246">To customize the format of the GridView's individual records, then, we need to create an event handler for the `RowDataBound` event.</span></span> <span data-ttu-id="08a20-247">이 예에 GridView를 추가 해 보겠습니다는 `CustomColors.aspx` 이름, 범주 및 가격이 미만 $10.00 노란색 배경 색을 사용 하 여 해당 제품을 강조 표시 하는 각 제품에 대 한 가격을 나열 하는 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-247">To illustrate this, let's add a GridView to the `CustomColors.aspx` page that lists the name, category, and price for each product, highlighting those products whose price is less than $10.00 with a yellow background color.</span></span>

## <a name="step-7-displaying-product-information-in-a-gridview"></a><span data-ttu-id="08a20-248">GridView의 제품 정보를 표시 하는 7 단계:</span><span class="sxs-lookup"><span data-stu-id="08a20-248">Step 7: Displaying Product Information in a GridView</span></span>

<span data-ttu-id="08a20-249">이전 예제에서 GridView FormView 아래에 추가 하 고 설정 해당 `ID` 속성을 `HighlightCheapProducts`입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-249">Add a GridView beneath the FormView from the previous example and set its `ID` property to `HighlightCheapProducts`.</span></span> <span data-ttu-id="08a20-250">페이지의 모든 제품을 반환 하는 ObjectDataSource에 이미 있으므로 GridView를 바인딩하십시오.</span><span class="sxs-lookup"><span data-stu-id="08a20-250">Since we already have an ObjectDataSource that returns all products on the page, bind the GridView to that.</span></span> <span data-ttu-id="08a20-251">GridView의 BoundFields 방금: 제품 이름, 범주 및 가격을 포함 하도록 마지막으로 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-251">Finally, edit the GridView's BoundFields to include just the products' names, categories, and prices.</span></span> <span data-ttu-id="08a20-252">이러한 편집 후 GridView의 태그 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-252">After these edits the GridView's markup should look like:</span></span>


[!code-aspx[Main](custom-formatting-based-upon-data-vb/samples/sample13.aspx)]

<span data-ttu-id="08a20-253">그림 9에서는 브라우저를 통해 볼 때이 여태 까지의 진행 상황을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-253">Figure 9 shows our progress to this point when viewed through a browser.</span></span>


<span data-ttu-id="08a20-254">[![이름, 범주 및 각 제품에 대 한 가격을 나열 하는 GridView](custom-formatting-based-upon-data-vb/_static/image22.png)](custom-formatting-based-upon-data-vb/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="08a20-254">[![The GridView Lists the Name, Category, and Price For Each Product](custom-formatting-based-upon-data-vb/_static/image22.png)](custom-formatting-based-upon-data-vb/_static/image21.png)</span></span>

<span data-ttu-id="08a20-255">**그림 9**: 이름, 범주 및 각 제품에 대 한 가격을 나열 하는 GridView ([큰 이미지를 보려면 클릭](custom-formatting-based-upon-data-vb/_static/image23.png))</span><span class="sxs-lookup"><span data-stu-id="08a20-255">**Figure 9**: The GridView Lists the Name, Category, and Price For Each Product ([Click to view full-size image](custom-formatting-based-upon-data-vb/_static/image23.png))</span></span>


## <a name="step-8-programmatically-determining-the-value-of-the-data-in-the-rowdatabound-event-handler"></a><span data-ttu-id="08a20-256">8 단계: RowDataBound 이벤트 처리기에서 데이터의 값을 프로그래밍 방식으로 결정</span><span class="sxs-lookup"><span data-stu-id="08a20-256">Step 8: Programmatically Determining the Value of the Data in the RowDataBound Event Handler</span></span>

<span data-ttu-id="08a20-257">경우는 `ProductsDataTable` GridView에 바인딩됩니다 해당 `ProductsRow` 열거 되 고 각 인스턴스가 `ProductsRow` 는 `GridViewRow` 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-257">When the `ProductsDataTable` is bound to the GridView its `ProductsRow` instances are enumerated and for each `ProductsRow` a `GridViewRow` is created.</span></span> <span data-ttu-id="08a20-258">합니다 `GridViewRow`의 `DataItem` 속성은 특정에 할당 `ProductRow`는 GridView의 `RowDataBound` 이벤트 처리기는 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-258">The `GridViewRow`'s `DataItem` property is assigned to the particular `ProductRow`, after which the GridView's `RowDataBound` event handler is raised.</span></span> <span data-ttu-id="08a20-259">확인 하는 `UnitPrice` GridView에 바인딩된 각 제품에 대 한 값이 다음 GridView의에 대 한 이벤트 처리기를 생성 해야 `RowDataBound` 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-259">To determine the `UnitPrice` value for each product bound to the GridView, then, we need to create an event handler for the GridView's `RowDataBound` event.</span></span> <span data-ttu-id="08a20-260">이 이벤트 처리기에서 검사할 수 있습니다 합니다 `UnitPrice` 현재 값 `GridViewRow` 해당 행에 대 한 서식 지정 의사 결정을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-260">In this event handler we can inspect the `UnitPrice` value for the current `GridViewRow` and make a formatting decision for that row.</span></span>

<span data-ttu-id="08a20-261">FormView 및 DetailsView와 같은 일련의 단계를 사용 하 여이 이벤트 처리기를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-261">This event handler can be created using the same series of steps as with the FormView and DetailsView.</span></span>


![GridView의 RowDataBound 이벤트에 대 한 이벤트 처리기 만들기](custom-formatting-based-upon-data-vb/_static/image24.png)

<span data-ttu-id="08a20-263">**그림 10**: GridView의에 대 한 이벤트 처리기를 만들고 `RowDataBound` 이벤트</span><span class="sxs-lookup"><span data-stu-id="08a20-263">**Figure 10**: Create an Event Handler for the GridView's `RowDataBound` Event</span></span>


<span data-ttu-id="08a20-264">이 방식으로 이벤트 처리기를 만드는 다음 코드를 ASP.NET 페이지의 코드 부분을 자동으로 추가 하면:</span><span class="sxs-lookup"><span data-stu-id="08a20-264">Creating the event hander in this manner will cause the following code to be automatically added to the ASP.NET page's code portion:</span></span>


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample14.vb)]

<span data-ttu-id="08a20-265">경우는 `RowDataBound` 이벤트가 발생 이벤트 처리기 매개 변수로 전달 되는 두 번째 형식의 개체 `GridViewRowEventArgs`에 라는 속성이 있는 `Row`합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-265">When the `RowDataBound` event fires, the event handler is passed as its second parameter an object of type `GridViewRowEventArgs`, which has a property named `Row`.</span></span> <span data-ttu-id="08a20-266">이 속성에 대 한 참조를 반환 합니다.는 `GridViewRow` 바인딩된 데이터 뿐 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-266">This property returns a reference to the `GridViewRow` that was just data bound.</span></span> <span data-ttu-id="08a20-267">액세스 하는 `ProductsRow` 에 바인딩된 인스턴스를 `GridViewRow` 사용 하 여는 `DataItem` 같이 속성:</span><span class="sxs-lookup"><span data-stu-id="08a20-267">To access the `ProductsRow` instance bound to the `GridViewRow` we use the `DataItem` property like so:</span></span>


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample15.vb)]

<span data-ttu-id="08a20-268">작업할 때 합니다 `RowDataBound` GridView 행의 다른 형식으로 구성 된 및 마다이 이벤트가 발생 하는 점에 유의 해야 하는 이벤트 처리기 *모든* 행 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-268">When working with the `RowDataBound` event handler it is important to keep in mind that the GridView is composed of different types of rows and that this event is fired for *all* row types.</span></span> <span data-ttu-id="08a20-269">A `GridViewRow`의 형식을 확인 하 여 해당 `RowType` 속성에 가능한 값 중 하나일 수 있습니다:</span><span class="sxs-lookup"><span data-stu-id="08a20-269">A `GridViewRow`'s type can be determined by its `RowType` property, and can have one of the possible values:</span></span>

- <span data-ttu-id="08a20-270">`DataRow` GridView의에서 레코드에 바인딩되는 행 `DataSource`</span><span class="sxs-lookup"><span data-stu-id="08a20-270">`DataRow` a row that is bound to a record from the GridView's `DataSource`</span></span>
- <span data-ttu-id="08a20-271">`EmptyDataRow` 경우에 표시 되는 행 GridView의 `DataSource` 비어</span><span class="sxs-lookup"><span data-stu-id="08a20-271">`EmptyDataRow` the row displayed if the GridView's `DataSource` is empty</span></span>
- <span data-ttu-id="08a20-272">`Footer` 바닥글 행입니다. 경우에 표시 된 GridView의 `ShowFooter` 속성 `True`</span><span class="sxs-lookup"><span data-stu-id="08a20-272">`Footer` the footer row; shown if the GridView's `ShowFooter` property is set to `True`</span></span>
- <span data-ttu-id="08a20-273">`Header` 머리글 행입니다. GridView의 ShowHeader 속성이로 설정 되어 있으면 표시 `True` (기본값)</span><span class="sxs-lookup"><span data-stu-id="08a20-273">`Header` the header row; shown if the GridView's ShowHeader property is set to `True` (the default)</span></span>
- <span data-ttu-id="08a20-274">`Pager` GridView의에 대 한 구현 하는 페이징, 페이징 인터페이스를 표시 하는 행</span><span class="sxs-lookup"><span data-stu-id="08a20-274">`Pager` for GridView's that implement paging, the row that displays the paging interface</span></span>
- <span data-ttu-id="08a20-275">`Separator` GridView에 대 한 사용 되지 않고 사용한는 `RowType` DataList 및 반복기에 대 한 속성 컨트롤을 두 개의 데이터 웹 컨트롤 하겠습니다 나중에 자습서</span><span class="sxs-lookup"><span data-stu-id="08a20-275">`Separator` not used for the GridView, but used by the `RowType` properties for the DataList and Repeater controls, two data Web controls we'll discuss in future tutorials</span></span>

<span data-ttu-id="08a20-276">하므로 합니다 `EmptyDataRow`, `Header`, `Footer`, 및 `Pager` 행 연관 되지 않습니다는 `DataSource` 레코드를 항상 갖습니다 값 `Nothing` 에 대 한 해당 `DataItem` 속성.</span><span class="sxs-lookup"><span data-stu-id="08a20-276">Since the `EmptyDataRow`, `Header`, `Footer`, and `Pager` rows aren't associated with a `DataSource` record, they will always have a value of `Nothing` for their `DataItem` property.</span></span> <span data-ttu-id="08a20-277">현재 사용 하기 전에 이러한 이유로 `GridViewRow`의 `DataItem` 속성인 것 먼저 확인 해야 사용 하 여 총비율을 `DataRow`입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-277">For this reason, before attempting to work with the current `GridViewRow`'s `DataItem` property, we first must make sure that we're dealing with a `DataRow`.</span></span> <span data-ttu-id="08a20-278">이 확인 하 여 수행할 수 있습니다 합니다 `GridViewRow`의 `RowType` 같이 속성:</span><span class="sxs-lookup"><span data-stu-id="08a20-278">This can be accomplished by checking the `GridViewRow`'s `RowType` property like so:</span></span>


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample16.vb)]

## <a name="step-9-highlighting-the-row-yellow-when-the-unitprice-value-is-less-than-1000"></a><span data-ttu-id="08a20-279">9 단계: $10.00 미만 행 노란색 When the UnitPrice 값을 강조 표시</span><span class="sxs-lookup"><span data-stu-id="08a20-279">Step 9: Highlighting the Row Yellow When the UnitPrice Value is Less than $10.00</span></span>

<span data-ttu-id="08a20-280">프로그래밍 방식으로 전체 강조 표시 하는 마지막 단계입니다 `GridViewRow` 경우는 `UnitPrice` 행이 $10.00 보다 작은 값입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-280">The last step is to programmatically highlight the entire `GridViewRow` if the `UnitPrice` value for that row is less than $10.00.</span></span> <span data-ttu-id="08a20-281">GridView의 행 또는 셀에 액세스 하기 위한 구문은와 동일 하 게 DetailsView `GridViewID.Rows(index)` 전체 행에 액세스 하려면 `GridViewID.Rows(index).Cells(index)` 특정 셀에 액세스 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-281">The syntax for accessing a GridView's rows or cells is the same as with the DetailsView `GridViewID.Rows(index)` to access the entire row, `GridViewID.Rows(index).Cells(index)` to access a particular cell.</span></span> <span data-ttu-id="08a20-282">그러나 경우 합니다 `RowDataBound` 이벤트 처리기 실행 데이터 바인딩된 `GridViewRow` GridView의 추가할 아직 `Rows` 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-282">However, when the `RowDataBound` event handler fires the data bound `GridViewRow` has yet to be added to the GridView's `Rows` collection.</span></span> <span data-ttu-id="08a20-283">따라서 현재 액세스할 수 없습니다 `GridViewRow` 에서 인스턴스는 `RowDataBound` 행 컬렉션을 사용 하 여 이벤트 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-283">Therefore you cannot access the current `GridViewRow` instance from the `RowDataBound` event handler using the Rows collection.</span></span>

<span data-ttu-id="08a20-284">대신 `GridViewID.Rows(index)`, 현재 참조할 수 있습니다 `GridViewRow` 의 인스턴스를 `RowDataBound` 이벤트 처리기를 사용 하 여 `e.Row`입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-284">Instead of `GridViewID.Rows(index)`, we can reference the current `GridViewRow` instance in the `RowDataBound` event handler using `e.Row`.</span></span> <span data-ttu-id="08a20-285">즉, 하려면 현재 강조 표시 `GridViewRow` 에서 인스턴스를 `RowDataBound` 이벤트 처리기를 사용 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-285">That is, in order to highlight the current `GridViewRow` instance from the `RowDataBound` event handler we would use:</span></span>


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample17.vb)]

<span data-ttu-id="08a20-286">설정 하지 않고 합니다 `GridViewRow`의 `BackColor` 속성을 직접 CSS 클래스를 사용 하 여 집중 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-286">Rather than set the `GridViewRow`'s `BackColor` property directly, let's stick with using CSS classes.</span></span> <span data-ttu-id="08a20-287">명명 된 CSS 클래스를 만들었습니다 `AffordablePriceEmphasis` 노란색으로 배경색을 설정 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-287">I've created a CSS class named `AffordablePriceEmphasis` that sets the background color to yellow.</span></span> <span data-ttu-id="08a20-288">완료 된 `RowDataBound` 이벤트 처리기를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-288">The completed `RowDataBound` event handler follows:</span></span>


[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample18.vb)]


<span data-ttu-id="08a20-289">[![가장 저렴 한 제품 노란색 강조 표시 됩니다.](custom-formatting-based-upon-data-vb/_static/image26.png)](custom-formatting-based-upon-data-vb/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="08a20-289">[![The Most Affordable Products are Highlighted Yellow](custom-formatting-based-upon-data-vb/_static/image26.png)](custom-formatting-based-upon-data-vb/_static/image25.png)</span></span>

<span data-ttu-id="08a20-290">**그림 11**: 가장 많이 저렴 한 제품 노란색 강조 표시 됩니다 ([큰 이미지를 보려면 클릭](custom-formatting-based-upon-data-vb/_static/image27.png))</span><span class="sxs-lookup"><span data-stu-id="08a20-290">**Figure 11**: The Most Affordable Products are Highlighted Yellow ([Click to view full-size image](custom-formatting-based-upon-data-vb/_static/image27.png))</span></span>


## <a name="summary"></a><span data-ttu-id="08a20-291">요약</span><span class="sxs-lookup"><span data-stu-id="08a20-291">Summary</span></span>

<span data-ttu-id="08a20-292">이 자습서에서 GridView, DetailsView 및 FormView 컨트롤에 바인딩된 데이터를 기반으로 형식을 지정 하는 방법에 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-292">In this tutorial we saw how to format the GridView, DetailsView, and FormView based on the data bound to the control.</span></span> <span data-ttu-id="08a20-293">이벤트 처리기에 대 한 만든이 수행 하는 `DataBound` 또는 `RowDataBound` 이벤트, 필요한 경우 서식 변경 함께 내부 데이터 검사 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-293">To accomplish this we created an event handler for the `DataBound` or `RowDataBound` events, where the underlying data was examined along with a formatting change, if needed.</span></span> <span data-ttu-id="08a20-294">DetailsView 또는 FormView에 바인딩된 데이터에 액세스 하려면 사용 하 여는 `DataItem` 속성에는 `DataBound` 이벤트 처리기를 GridView에 대 한 각 `GridViewRow` 인스턴스의 `DataItem` 는에서사용할수있는해당행에바인딩된데이터를포함하는속성`RowDataBound` 이벤트 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-294">To access the data bound to a DetailsView or FormView, we use the `DataItem` property in the `DataBound` event handler; for a GridView, each `GridViewRow` instance's `DataItem` property contains the data bound to that row, which is available in the `RowDataBound` event handler.</span></span>

<span data-ttu-id="08a20-295">프로그래밍 방식으로 데이터 웹 컨트롤의 서식 지정을 조정 하는 구문은 웹 컨트롤 및 서식을 지정할 데이터 표시 방법을 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-295">The syntax for programmatically adjusting the data Web control's formatting depends upon the Web control and how the data to be formatted is displayed.</span></span> <span data-ttu-id="08a20-296">GridView 및 DetailsView 컨트롤, 행 및 셀 서 수 인덱스에 의해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-296">For DetailsView and GridView controls, the rows and cells can be accessed by an ordinal index.</span></span> <span data-ttu-id="08a20-297">서식 파일을 사용 하는 FormView에 대 한는 `FindControl("controlID")` 메서드는 일반적으로 템플릿 내에서 웹 컨트롤을 찾는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-297">For the FormView, which uses templates, the `FindControl("controlID")` method is commonly used to locate a Web control from within the template.</span></span>

<span data-ttu-id="08a20-298">다음 자습서에서 GridView 및 DetailsView를 사용 하 여 템플릿을 사용 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-298">In the next tutorial we'll look at how to use templates with the GridView and DetailsView.</span></span> <span data-ttu-id="08a20-299">또한 기본 데이터를 기반으로 서식을 사용자 지정 하기 위한 다른 기법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-299">Additionally, we'll see another technique for customizing the formatting based on the underlying data.</span></span>

<span data-ttu-id="08a20-300">즐거운 프로그래밍!</span><span class="sxs-lookup"><span data-stu-id="08a20-300">Happy Programming!</span></span>

## <a name="about-the-author"></a><span data-ttu-id="08a20-301">저자 소개</span><span class="sxs-lookup"><span data-stu-id="08a20-301">About the Author</span></span>

<span data-ttu-id="08a20-302">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-302">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), author of seven ASP/ASP.NET books and founder of [4GuysFromRolla.com](http://www.4guysfromrolla.com), has been working with Microsoft Web technologies since 1998.</span></span> <span data-ttu-id="08a20-303">Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-303">Scott works as an independent consultant, trainer, and writer.</span></span> <span data-ttu-id="08a20-304">최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-304">His latest book is [*Sams Teach Yourself ASP.NET 2.0 in 24 Hours*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco).</span></span> <span data-ttu-id="08a20-305">그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="08a20-305">He can be reached at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span> <span data-ttu-id="08a20-306">찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-306">or via his blog, which can be found at [http://ScottOnWriting.NET](http://ScottOnWriting.NET).</span></span>

## <a name="special-thanks-to"></a><span data-ttu-id="08a20-307">특별히 감사</span><span class="sxs-lookup"><span data-stu-id="08a20-307">Special Thanks To</span></span>

<span data-ttu-id="08a20-308">이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-308">This tutorial series was reviewed by many helpful reviewers.</span></span> <span data-ttu-id="08a20-309">이 자습서에 대 한 선행 검토자 E.R. 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-309">Lead reviewers for this tutorial were E.R.</span></span> <span data-ttu-id="08a20-310">Gilmore, Dennis Patterson 및 Dan Jagers 합니다.</span><span class="sxs-lookup"><span data-stu-id="08a20-310">Gilmore, Dennis Patterson, and Dan Jagers.</span></span> <span data-ttu-id="08a20-311">내 향후 MSDN 문서를 검토에 관심이 있으십니까?</span><span class="sxs-lookup"><span data-stu-id="08a20-311">Interested in reviewing my upcoming MSDN articles?</span></span> <span data-ttu-id="08a20-312">그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="08a20-312">If so, drop me a line at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="08a20-313">[이전](displaying-summary-information-in-the-gridview-s-footer-cs.md)
> [다음](using-templatefields-in-the-gridview-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="08a20-313">[Previous](displaying-summary-information-in-the-gridview-s-footer-cs.md)
[Next](using-templatefields-in-the-gridview-control-vb.md)</span></span>
