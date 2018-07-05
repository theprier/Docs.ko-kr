---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-vb
title: 마스터/세부 정보 필터링 (VB) DropDownList 한 개로 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 마스터 레코드 DropDownList 컨트롤과 GridView에서 선택한 목록 항목의 세부 정보를 표시 하는 방법을 살펴보겠습니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: ea44717e-ab2e-46cd-a692-e4a9c0de194c
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-vb
msc.type: authoredcontent
ms.openlocfilehash: d15348812abf88fa35485c0d3415b2683225b6b5
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37386697"
---
<a name="masterdetail-filtering-with-a-dropdownlist-vb"></a><span data-ttu-id="6e1d0-103">마스터/세부 정보 (VB) DropDownList 한 개로 필터링</span><span class="sxs-lookup"><span data-stu-id="6e1d0-103">Master/Detail Filtering With a DropDownList (VB)</span></span>
====================
<span data-ttu-id="6e1d0-104">[Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="6e1d0-104">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

<span data-ttu-id="6e1d0-105">[샘플 앱을 다운로드](http://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_7_VB.exe) 또는 [PDF 다운로드](master-detail-filtering-with-a-dropdownlist-vb/_static/datatutorial07vb1.pdf)</span><span class="sxs-lookup"><span data-stu-id="6e1d0-105">[Download Sample App](http://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_7_VB.exe) or [Download PDF](master-detail-filtering-with-a-dropdownlist-vb/_static/datatutorial07vb1.pdf)</span></span>

> <span data-ttu-id="6e1d0-106">이 자습서에서는 마스터 레코드 DropDownList 컨트롤과 GridView에서 선택한 목록 항목의 세부 정보를 표시 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-106">In this tutorial we'll see how to display the master records in a DropDownList control and the details of the selected list item in a GridView.</span></span>


## <a name="introduction"></a><span data-ttu-id="6e1d0-107">소개</span><span class="sxs-lookup"><span data-stu-id="6e1d0-107">Introduction</span></span>

<span data-ttu-id="6e1d0-108">보고서의 일반적인 형식은 합니다 *마스터/세부 정보 보고서*, 일부 "마스터" 레코드 집합을 표시 하 여 시작 하는 보고서에서.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-108">A common type of report is the *master/detail report*, in which the report begins by showing some set of "master" records.</span></span> <span data-ttu-id="6e1d0-109">사용자를 살펴볼 수 아래로 마스터 레코드 중 하나 있으므로 해당 마스터 레코드의 세부 정보를 "." 보기</span><span class="sxs-lookup"><span data-stu-id="6e1d0-109">The user can then drill down into one of the master records, thereby viewing that master record's "details."</span></span> <span data-ttu-id="6e1d0-110">마스터/세부 정보는 보고서와 같은 1 대 다 관계를 시각화에 대 한 이상적인 모든 범주를 표시 및 다음 사용자를 특정 범주를 선택 하 고 연결 된 제품을 표시할 수 있도록 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-110">Master/detail reports are an ideal choice for visualizing one-to-many relationships, such as a report showing all of the categories and then allowing a user to select a particular category and display its associated products.</span></span> <span data-ttu-id="6e1d0-111">또한 마스터/세부 정보 보고서 (많은 열 임) 특히 "와이드" 테이블에서 자세한 정보를 표시 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-111">Additionally, master/detail reports are useful for displaying detailed information from particularly "wide" tables (ones that have a lot of columns).</span></span> <span data-ttu-id="6e1d0-112">예를 들어 마스터/세부 정보 보고서의 "마스터" 수준 데이터베이스에서 제품 이름과 단위 가격만 제품을 표시할 수 있습니다 하 고 특정 제품에 드릴 다운 하면 추가 제품 필드를 표시 됩니다 (범주, 공급자, 단위, quantity 및 등등)입니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-112">For example, the "master" level of a master/detail report might show just the product name and unit price of the products in the database, and drilling down into a particular product would show the additional product fields (category, supplier, quantity per unit, and so on).</span></span>

<span data-ttu-id="6e1d0-113">여러 가지 방법으로는 마스터/세부 정보 보고서를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-113">There are many ways with which a master/detail report can be implemented.</span></span> <span data-ttu-id="6e1d0-114">이 고 다음 세 개의 자습서를 통해 다양 한 마스터/세부 정보 보고서에 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-114">Over this and the next three tutorials we'll look at a variety of master/detail reports.</span></span> <span data-ttu-id="6e1d0-115">이 자습서에서 마스터 레코드를 표시 하는 방법을 알아봅니다를 [DropDownList 컨트롤](https://msdn.microsoft.com/library/dtx91y0z.aspx) 와 GridView에서 선택한 목록 항목의 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-115">In this tutorial we'll see how to display the master records in a [DropDownList control](https://msdn.microsoft.com/library/dtx91y0z.aspx) and the details of the selected list item in a GridView.</span></span> <span data-ttu-id="6e1d0-116">특히이 자습서의 마스터/세부 정보 보고서는 범주 및 제품 정보를 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-116">In particular, this tutorial's master/detail report will list category and product information.</span></span>

## <a name="step-1-displaying-the-categories-in-a-dropdownlist"></a><span data-ttu-id="6e1d0-117">1 단계: DropDownList에 범주를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-117">Step 1: Displaying the Categories in a DropDownList</span></span>

<span data-ttu-id="6e1d0-118">마스터/세부 정보 보고서는 선택한 목록 항목의 제품이 표시를 사용 하 여 DropDownList, 범주 표시 페이지는 GridView에서 더 아래쪽 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-118">Our master/detail report will list the categories in a DropDownList, with the selected list item's products displayed further down in the page in a GridView.</span></span> <span data-ttu-id="6e1d0-119">첫 번째 작업을 미리 한는 DropDownList에 표시 되는 범주를 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-119">The first task ahead of us, then, is to have the categories displayed in a DropDownList.</span></span> <span data-ttu-id="6e1d0-120">열기는 `FilterByDropDownList.aspx` 페이지에 `Filtering` 폴더, DropDownList에 페이지의 디자이너 도구 상자에서 끌어서 설정 해당 `ID` 속성을 `Categories`입니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-120">Open the `FilterByDropDownList.aspx` page in the `Filtering` folder, drag on a DropDownList from the Toolbox onto the page's designer, and set its `ID` property to `Categories`.</span></span> <span data-ttu-id="6e1d0-121">다음으로, DropDownList의 스마트 태그의 데이터 소스 선택 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-121">Next, click on the Choose Data Source link from the DropDownList's smart tag.</span></span> <span data-ttu-id="6e1d0-122">데이터 소스 구성 마법사가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-122">This will display the Data Source Configuration wizard.</span></span>


<span data-ttu-id="6e1d0-123">[![DropDownList의 데이터 소스를 지정 합니다.](master-detail-filtering-with-a-dropdownlist-vb/_static/image2.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6e1d0-123">[![Specify the DropDownList's Data Source](master-detail-filtering-with-a-dropdownlist-vb/_static/image2.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image1.png)</span></span>

<span data-ttu-id="6e1d0-124">**그림 1**: DropDownList의 데이터 원본을 지정 ([큰 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="6e1d0-124">**Figure 1**: Specify the DropDownList's Data Source ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-vb/_static/image3.png))</span></span>


<span data-ttu-id="6e1d0-125">라는 새 ObjectDataSource를 추가 하도록 선택할 `CategoriesDataSource` 를 호출 하는 `CategoriesBLL` 클래스의 `GetCategories()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-125">Choose to add a new ObjectDataSource named `CategoriesDataSource` that invokes the `CategoriesBLL` class's `GetCategories()` method.</span></span>


<span data-ttu-id="6e1d0-126">[![CategoriesDataSource 라는 새 ObjectDataSource를 추가 합니다.](master-detail-filtering-with-a-dropdownlist-vb/_static/image5.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="6e1d0-126">[![Add a New ObjectDataSource Named CategoriesDataSource](master-detail-filtering-with-a-dropdownlist-vb/_static/image5.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image4.png)</span></span>

<span data-ttu-id="6e1d0-127">**그림 2**: 새 ObjectDataSource 라는 추가 `CategoriesDataSource` ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-a-dropdownlist-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="6e1d0-127">**Figure 2**: Add a New ObjectDataSource Named `CategoriesDataSource` ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-vb/_static/image6.png))</span></span>


<span data-ttu-id="6e1d0-128">[![CategoriesBLL 클래스를 사용 하려면 선택 합니다.](master-detail-filtering-with-a-dropdownlist-vb/_static/image8.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="6e1d0-128">[![Choose to Use the CategoriesBLL Class](master-detail-filtering-with-a-dropdownlist-vb/_static/image8.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image7.png)</span></span>

<span data-ttu-id="6e1d0-129">**그림 3**: 사용 하도록 선택 합니다 `CategoriesBLL` 클래스 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-a-dropdownlist-vb/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="6e1d0-129">**Figure 3**: Choose to Use the `CategoriesBLL` Class ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-vb/_static/image9.png))</span></span>


<span data-ttu-id="6e1d0-130">[![GetCategories() 메서드를 사용 하는 ObjectDataSource 구성](master-detail-filtering-with-a-dropdownlist-vb/_static/image11.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="6e1d0-130">[![Configure the ObjectDataSource to Use the GetCategories() Method](master-detail-filtering-with-a-dropdownlist-vb/_static/image11.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image10.png)</span></span>

<span data-ttu-id="6e1d0-131">**그림 4**: ObjectDataSource 사용 하도록 구성 된 `GetCategories()` 메서드 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-a-dropdownlist-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="6e1d0-131">**Figure 4**: Configure the ObjectDataSource to Use the `GetCategories()` Method ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-vb/_static/image12.png))</span></span>


<span data-ttu-id="6e1d0-132">DropDownList에 어떤 데이터 원본 필드를 표시 해야 하 고는 지정 해야 하는 ObjectDataSource를 구성한 후 목록 항목에 대 한 값으로 연결 해야 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-132">After configuring the ObjectDataSource we still need to specify what data source field should be displayed in DropDownList and which one should be associated as the value for the list item.</span></span> <span data-ttu-id="6e1d0-133">있어야 합니다 `CategoryName` 필드를 표시 및 `CategoryID` 각 목록 항목에 대 한 값으로.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-133">Have the `CategoryName` field as the display and `CategoryID` as the value for each list item.</span></span>


<span data-ttu-id="6e1d0-134">[![가 DropDownList 표시를 사용 하 여 CategoryID와 CategoryName 필드 값](master-detail-filtering-with-a-dropdownlist-vb/_static/image14.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="6e1d0-134">[![Have the DropDownList Display the CategoryName Field and Use CategoryID as the Value](master-detail-filtering-with-a-dropdownlist-vb/_static/image14.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image13.png)</span></span>

<span data-ttu-id="6e1d0-135">**그림 5**: DropDownList을 표시 합니다 `CategoryName` 필드 및 사용 `CategoryID` 값으로 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-a-dropdownlist-vb/_static/image15.png))</span><span class="sxs-lookup"><span data-stu-id="6e1d0-135">**Figure 5**: Have the DropDownList Display the `CategoryName` Field and Use `CategoryID` as the Value ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-vb/_static/image15.png))</span></span>


<span data-ttu-id="6e1d0-136">이 시점에서 레코드를 사용 하 여 채워지는 DropDownList 컨트롤이 있습니다를 `Categories` 테이블 (모두 약 6 초 후에 수행).</span><span class="sxs-lookup"><span data-stu-id="6e1d0-136">At this point we have a DropDownList control that's populated with the records from the `Categories` table (all accomplished in about six seconds).</span></span> <span data-ttu-id="6e1d0-137">그림 6 브라우저를 통해 볼 때 지금 진행 상황을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-137">Figure 6 shows our progress thus far when viewed through a browser.</span></span>


<span data-ttu-id="6e1d0-138">[![현재 범주를 나열 하는 드롭다운](master-detail-filtering-with-a-dropdownlist-vb/_static/image17.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="6e1d0-138">[![A Drop-Down Lists the Current Categories](master-detail-filtering-with-a-dropdownlist-vb/_static/image17.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image16.png)</span></span>

<span data-ttu-id="6e1d0-139">**그림 6**:는 드롭다운 목록이 현재 범주 ([큰 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-vb/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="6e1d0-139">**Figure 6**: A Drop-Down Lists the Current Categories ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-vb/_static/image18.png))</span></span>


## <a name="step-2-adding-the-products-gridview"></a><span data-ttu-id="6e1d0-140">2 단계: 추가 제품 GridView</span><span class="sxs-lookup"><span data-stu-id="6e1d0-140">Step 2: Adding the Products GridView</span></span>

<span data-ttu-id="6e1d0-141">마스터/세부 정보 보고서의 마지막 단계는 선택한 범주와 관련 된 제품을 나열 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-141">That last step in our master/detail report is to list the products associated with the selected category.</span></span> <span data-ttu-id="6e1d0-142">이렇게 하려면 페이지에 GridView를 추가 하 고 라는 새로운 ObjectDataSource는 만들 `productsDataSource`합니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-142">To accomplish this, add a GridView to the page and create a new ObjectDataSource named `productsDataSource`.</span></span> <span data-ttu-id="6e1d0-143">가 합니다 `productsDataSource` 컨트롤이 해당 데이터를 가져올 합니다 `ProductsBLL` 클래스의 `GetProductsByCategoryID(categoryID)` 메서드.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-143">Have the `productsDataSource` control cull its data from the `ProductsBLL` class's `GetProductsByCategoryID(categoryID)` method.</span></span>


<span data-ttu-id="6e1d0-144">[![GetProductsByCategoryID(categoryID) 메서드를 선택 합니다.](master-detail-filtering-with-a-dropdownlist-vb/_static/image20.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="6e1d0-144">[![Select the GetProductsByCategoryID(categoryID) Method](master-detail-filtering-with-a-dropdownlist-vb/_static/image20.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image19.png)</span></span>

<span data-ttu-id="6e1d0-145">**그림 7**: 선택 된 `GetProductsByCategoryID(categoryID)` 메서드 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-a-dropdownlist-vb/_static/image21.png))</span><span class="sxs-lookup"><span data-stu-id="6e1d0-145">**Figure 7**: Select the `GetProductsByCategoryID(categoryID)` Method ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-vb/_static/image21.png))</span></span>


<span data-ttu-id="6e1d0-146">이 메서드를 선택한 후 ObjectDataSource 마법사 묻는 메서드의 값 *`categoryID`* 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-146">After choosing this method, the ObjectDataSource wizard prompts us for the value for the method's *`categoryID`* parameter.</span></span> <span data-ttu-id="6e1d0-147">선택한 값을 사용 하도록 `categories` DropDownList 항목으로 매개 변수 원본 컨트롤과를 ControlID `Categories`합니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-147">To use the value of the selected `categories` DropDownList item set the Parameter source to Control and the ControlID to `Categories`.</span></span>


<span data-ttu-id="6e1d0-148">[![CategoryID 매개 변수 범주 DropDownList의 값으로 설정](master-detail-filtering-with-a-dropdownlist-vb/_static/image23.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="6e1d0-148">[![Set the categoryID Parameter to the Value of the Categories DropDownList](master-detail-filtering-with-a-dropdownlist-vb/_static/image23.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image22.png)</span></span>

<span data-ttu-id="6e1d0-149">**그림 8**: 설정 합니다 *`categoryID`* 매개 변수 값으로는 `Categories` DropDownList ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-a-dropdownlist-vb/_static/image24.png))</span><span class="sxs-lookup"><span data-stu-id="6e1d0-149">**Figure 8**: Set the *`categoryID`* Parameter to the Value of the `Categories` DropDownList ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-vb/_static/image24.png))</span></span>


<span data-ttu-id="6e1d0-150">시간을 내어 브라우저에서 진행 상황을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-150">Take a moment to check out our progress in a browser.</span></span> <span data-ttu-id="6e1d0-151">이러한 제품 선택한 범주에 속하는 페이지를 처음 방문 하는 경우 (음료) (그림 9에 표시 됨)으로 표시 되지만 DropDownList 변경 데이터를 업데이트 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-151">When first visiting the page, those products belong to the selected category (Beverages) are displayed (as shown in Figure 9), but changing the DropDownList doesn't update the data.</span></span> <span data-ttu-id="6e1d0-152">업데이트를 GridView에 대 한 포스트백을 발생 해야 하는 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-152">This is because a postback must occur for the GridView to update.</span></span> <span data-ttu-id="6e1d0-153">이렇게 하려면에서는 두 가지 옵션이 (둘 중 필요한 코드를 작성).</span><span class="sxs-lookup"><span data-stu-id="6e1d0-153">To accomplish this we have two options (neither of which requires writing any code):</span></span>

- <span data-ttu-id="6e1d0-154">**범주 DropDownList의 설정**[AutoPostBack 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.listcontrol.autopostback%28VS.80%29.aspx)**True로 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6e1d0-154">**Set the categories DropDownList's**[AutoPostBack property](https://msdn.microsoft.com/library/system.web.ui.webcontrols.listcontrol.autopostback%28VS.80%29.aspx)**to True.**</span></span> <span data-ttu-id="6e1d0-155">(이렇게 하려면 DropDownList의 스마트 태그에 AutoPostBack을 사용 하도록 설정 옵션을 선택 합니다.) DropDownList의 선택할 때마다 포스트백을 트리거하는이 항목은 사용자가 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-155">(You can accomplish this by checking the Enable AutoPostBack option in the DropDownList's smart tag.) This will trigger a postback whenever the DropDownList's selected item is changed by the user.</span></span> <span data-ttu-id="6e1d0-156">따라서 사용자가 드롭다운 목록에서 새 범주를 선택 하면 포스트백 계속 될 것 이라고 및 GridView 새로 선택한 범주에 대 한 제품을 사용 하 여 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-156">Therefore, when the user selects a new category from the DropDownList a postback will ensue and the GridView will be updated with the products for the newly selected category.</span></span> <span data-ttu-id="6e1d0-157">(이 자습서에서 사용한 접근 방식입니다.)</span><span class="sxs-lookup"><span data-stu-id="6e1d0-157">(This is the approach I've used in this tutorial.)</span></span>
- <span data-ttu-id="6e1d0-158">**드롭다운 목록 옆에 있는 단추 웹 컨트롤을 추가 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6e1d0-158">**Add a Button Web control next to the DropDownList.**</span></span> <span data-ttu-id="6e1d0-159">설정의 `Text` 속성 새로 고침을 또는 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-159">Set its `Text` property to Refresh or something similar.</span></span> <span data-ttu-id="6e1d0-160">이 방법을 사용 하면 새 범주를 선택 하 고 다음 단추를 클릭 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-160">With this approach, the user will need to select a new category and then click the Button.</span></span> <span data-ttu-id="6e1d0-161">단추를 클릭 하면 포스트백을 발생 되며 선택한 범주의 제품을 나열 하려면 GridView를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-161">Clicking the Button will cause a postback and update the GridView to list those products of the selected category.</span></span>

<span data-ttu-id="6e1d0-162">그림 9와 10 중인 마스터/세부 정보 보고서를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-162">Figures 9 and 10 illustrate the master/detail report in action.</span></span>


<span data-ttu-id="6e1d0-163">[![먼저 페이지를 방문 하 고, 음료 제품 표시 됩니다.](master-detail-filtering-with-a-dropdownlist-vb/_static/image26.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="6e1d0-163">[![When First Visiting the Page, the Beverage Products are Displayed](master-detail-filtering-with-a-dropdownlist-vb/_static/image26.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image25.png)</span></span>

<span data-ttu-id="6e1d0-164">**그림 9**: 먼저 페이지를 방문 하 고, 음료 제품 표시 됩니다 ([큰 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-vb/_static/image27.png))</span><span class="sxs-lookup"><span data-stu-id="6e1d0-164">**Figure 9**: When First Visiting the Page, the Beverage Products are Displayed ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-vb/_static/image27.png))</span></span>


<span data-ttu-id="6e1d0-165">[![새 제품 (생성)을 선택 하면 자동으로 포스트백을 GridView를 업데이트 하는 중](master-detail-filtering-with-a-dropdownlist-vb/_static/image29.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image28.png)</span><span class="sxs-lookup"><span data-stu-id="6e1d0-165">[![Selecting a New Product (Produce) Automatically Causes a PostBack, Updating the GridView](master-detail-filtering-with-a-dropdownlist-vb/_static/image29.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image28.png)</span></span>

<span data-ttu-id="6e1d0-166">**그림 10**: 새 제품 (생성)을 선택 하면 자동으로 포스트백을 GridView를 업데이트 하는 중 ([큰 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-vb/_static/image30.png))</span><span class="sxs-lookup"><span data-stu-id="6e1d0-166">**Figure 10**: Selecting a New Product (Produce) Automatically Causes a PostBack, Updating the GridView ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-vb/_static/image30.png))</span></span>


## <a name="adding-a----choose-a-category----list-item"></a><span data-ttu-id="6e1d0-167">"-범주-" 선택 목록 항목 추가</span><span class="sxs-lookup"><span data-stu-id="6e1d0-167">Adding a "-- Choose a Category --" List Item</span></span>

<span data-ttu-id="6e1d0-168">먼저 방문할 때는 `FilterByDropDownList.aspx` DropDownList의 첫 번째 목록 항목 (음료)는 선택, 기본적으로 GridView의 음료 제품을 보여 주는 범주 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-168">When first visiting the `FilterByDropDownList.aspx` page the categories DropDownList's first list item (Beverages) is selected by default, showing the beverage products in the GridView.</span></span> <span data-ttu-id="6e1d0-169">선택한 대신 DropDownList 항목이 하려는 경우 첫 번째 범주의 제품을 보여 주는 것이 아니라 "-범주 선택-" 같은 말입니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-169">Rather than showing the first category's products, we may want to instead have a DropDownList item selected that says something like, "-- Choose a Category --".</span></span>

<span data-ttu-id="6e1d0-170">DropDownList에 새 목록 항목을 추가 하려면 속성 창으로 이동 하 고에서 줄임표를 클릭 합니다 `Items` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-170">To add a new list item to the DropDownList, go to the Properties window and click on the ellipses in the `Items` property.</span></span> <span data-ttu-id="6e1d0-171">사용 하 여 새 목록 항목을 추가 합니다 `Text` "-범주 선택-" 및 `Value` `-1`합니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-171">Add a new list item with the `Text` "-- Choose a Category --" and the `Value` `-1`.</span></span>


<span data-ttu-id="6e1d0-172">[![추가--범주--목록 항목 선택](master-detail-filtering-with-a-dropdownlist-vb/_static/image32.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image31.png)</span><span class="sxs-lookup"><span data-stu-id="6e1d0-172">[![Add a -- Choose a Category -- List Item](master-detail-filtering-with-a-dropdownlist-vb/_static/image32.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image31.png)</span></span>

<span data-ttu-id="6e1d0-173">**그림 11**: 추가--범주--목록 항목 선택 ([큰 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-vb/_static/image33.png))</span><span class="sxs-lookup"><span data-stu-id="6e1d0-173">**Figure 11**: Add a -- Choose a Category -- List Item ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-vb/_static/image33.png))</span></span>


<span data-ttu-id="6e1d0-174">또는 드롭다운 목록에 다음 태그를 추가 하 여 목록 항목을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-174">Alternatively, you can add the list item by adding the following markup to the DropDownList:</span></span>


[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-vb/samples/sample1.aspx)]

<span data-ttu-id="6e1d0-175">DropDownList 컨트롤을 설정 해야 뿐만 `AppendDataBoundItems` 범주는 ObjectDataSource의 DropDownList 바인딩할 때 덮어씁니다 수동으로 추가 된 목록 항목 경우 때문에 True로 `AppendDataBoundItems` True 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-175">Additionally, we need to set the DropDownList control's `AppendDataBoundItems` to True because when the categories are bound to the DropDownList from the ObjectDataSource they'll overwrite any manually-added list items if `AppendDataBoundItems` isn't True.</span></span>


![AppendDataBoundItems 속성도 True로 설정](master-detail-filtering-with-a-dropdownlist-vb/_static/image34.png)

<span data-ttu-id="6e1d0-177">**그림 12**: 설정의 `AppendDataBoundItems` 속성을 true로</span><span class="sxs-lookup"><span data-stu-id="6e1d0-177">**Figure 12**: Set the `AppendDataBoundItems` Property to True</span></span>


<span data-ttu-id="6e1d0-178">이러한 변경 이후 먼저 페이지를 방문할 때 "-범주 선택-" 옵션을 선택 하 고 제품이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-178">After these changes, when first visiting the page the "-- Choose a Category --" option is selected and no products are displayed.</span></span>


<span data-ttu-id="6e1d0-179">[![초기 페이지 로드에 제품이 표시 됩니다.](master-detail-filtering-with-a-dropdownlist-vb/_static/image36.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image35.png)</span><span class="sxs-lookup"><span data-stu-id="6e1d0-179">[![On the Initial Page Load No Products are Displayed](master-detail-filtering-with-a-dropdownlist-vb/_static/image36.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image35.png)</span></span>

<span data-ttu-id="6e1d0-180">**그림 13**:에서 초기 페이지 로드 아니요 제품 표시 됩니다 ([큰 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-vb/_static/image37.png))</span><span class="sxs-lookup"><span data-stu-id="6e1d0-180">**Figure 13**: On the Initial Page Load No Products are Displayed ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-vb/_static/image37.png))</span></span>


<span data-ttu-id="6e1d0-181">해당 값은 "-범주-" 선택 목록 항목이 선택 되어 있으므로 제품이 없습니다. 때 표시 되는 이유 이므로 `-1` 데이터베이스에 있는 제품이 및는 `CategoryID` 의 `-1`.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-181">The reason no products are displayed when because the "-- Choose a Category --" list item is selected is because its value is `-1` and there are no products in the database with a `CategoryID` of `-1`.</span></span> <span data-ttu-id="6e1d0-182">이 동작은 하려는 경우이 시점에서 완료 한 다음!</span><span class="sxs-lookup"><span data-stu-id="6e1d0-182">If this is the behavior you want then you're done at this point!</span></span> <span data-ttu-id="6e1d0-183">그러나 표시 하려는 경우 *모든* 범주의 목록 "-"선택 범주-항목을 선택 하면 반환 하는 `ProductsBLL` 클래스 및 사용자 지정 합니다 `GetProductsByCategoryID(categoryID)` 메서드를 호출는 `GetProducts()` 메서드 경우 전달 된에서 *`categoryID`* 매개 변수가 0 보다 작습니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-183">If, however, you want to display *all* of the categories when the "-- Choose a Category --" list item is selected, return to the `ProductsBLL` class and customize the `GetProductsByCategoryID(categoryID)` method so that it invokes the `GetProducts()` method if the passed in *`categoryID`* parameter is less than zero:</span></span>


[!code-vb[Main](master-detail-filtering-with-a-dropdownlist-vb/samples/sample2.vb)]

<span data-ttu-id="6e1d0-184">여기에 사용 되는 방법은 모든 공급 업체 표시를 사용 하는 방법과 비슷한 방법으로 다시 합니다 [선언적 매개 변수](../basic-reporting/declarative-parameters-cs.md) 자습서,이 예제에 대 한 값을 사용 하는 것 이지만 `-1` 모든 레코드를 해야 함을 나타내려면 아닌 사이트별로 검색 `Nothing`합니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-184">The technique used here is similar to the approach we used to display all suppliers back in the [Declarative Parameters](../basic-reporting/declarative-parameters-cs.md) tutorial, although for this example we're using a value of `-1` to indicate that all records should be retrieved as opposed to `Nothing`.</span></span> <span data-ttu-id="6e1d0-185">왜냐하면를 *`categoryID`* 의 매개 변수는 `GetProductsByCategoryID(categoryID)` 반면 선언적 매개 변수 자습서에서 문자열 입력 매개 변수에 전달 된 것에서 전달 된 정수 값으로 메서드에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-185">This is because the *`categoryID`* parameter of the `GetProductsByCategoryID(categoryID)` method expects as integer value passed in, whereas in the Declarative Parameters tutorial we were passing in a string input parameter.</span></span>

<span data-ttu-id="6e1d0-186">그림 14의 스크린 샷을 보여 줍니다 `FilterByDropDownList.aspx` "-범주 선택-" 옵션을 선택한 경우.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-186">Figure 14 shows a screen shot of `FilterByDropDownList.aspx` when the "-- Choose a Category --" option is selected.</span></span> <span data-ttu-id="6e1d0-187">여기에서 기본적으로 표시 되는 모든 제품 및 특정 범주를 선택 하면 사용자 표시를 좁힐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-187">Here, all of the products are displayed by default, and the user can narrow the display by choosing a specific category.</span></span>


<span data-ttu-id="6e1d0-188">[![이제 나열 기본적으로 모든 제품](master-detail-filtering-with-a-dropdownlist-vb/_static/image39.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image38.png)</span><span class="sxs-lookup"><span data-stu-id="6e1d0-188">[![All of the Products are Now Listed By Default](master-detail-filtering-with-a-dropdownlist-vb/_static/image39.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image38.png)</span></span>

<span data-ttu-id="6e1d0-189">**그림 14**: 이제 나열 기본적으로 모든 제품 ([큰 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-vb/_static/image40.png))</span><span class="sxs-lookup"><span data-stu-id="6e1d0-189">**Figure 14**: All of the Products are Now Listed By Default ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-vb/_static/image40.png))</span></span>


## <a name="summary"></a><span data-ttu-id="6e1d0-190">요약</span><span class="sxs-lookup"><span data-stu-id="6e1d0-190">Summary</span></span>

<span data-ttu-id="6e1d0-191">계층적으로 관련 데이터를 표시할 때 종종 사용자 계층의 최상위에서 데이터를 읽는 데 시작 하 고 세부 정보로 드릴 다운 하는 마스터/세부 정보 보고서를 사용 하 여 데이터를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-191">When displaying hierarchically-related data, it often helps to present the data using master/detail reports, from which the user can start perusing the data from the top of the hierarchy and drill down into details.</span></span> <span data-ttu-id="6e1d0-192">이 자습서에서는 선택한 범주의 제품을 표시 하는 간단한 마스터/세부 정보 보고서 작성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-192">In this tutorial we examined building a simple master/detail report showing a selected category's products.</span></span> <span data-ttu-id="6e1d0-193">이 작업은 DropDownList 범주 목록과 선택한 범주에 속하는 제품 GridView를 사용 하 여 수행 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-193">This was accomplished by using a DropDownList for the list of categories and a GridView for the products belonging to the selected category.</span></span>

<span data-ttu-id="6e1d0-194">에 [다음 자습서](master-detail-filtering-with-two-dropdownlists-vb.md) 알아보겠습니다 DropDownList 인터페이스 한 단계 더 Dropdownlist 두를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-194">In the [next tutorial](master-detail-filtering-with-two-dropdownlists-vb.md) we'll take the DropDownList interface one step further, using two DropDownLists.</span></span>

<span data-ttu-id="6e1d0-195">즐거운 프로그래밍!</span><span class="sxs-lookup"><span data-stu-id="6e1d0-195">Happy Programming!</span></span>

## <a name="about-the-author"></a><span data-ttu-id="6e1d0-196">저자 소개</span><span class="sxs-lookup"><span data-stu-id="6e1d0-196">About the Author</span></span>

<span data-ttu-id="6e1d0-197">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-197">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), author of seven ASP/ASP.NET books and founder of [4GuysFromRolla.com](http://www.4guysfromrolla.com), has been working with Microsoft Web technologies since 1998.</span></span> <span data-ttu-id="6e1d0-198">Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-198">Scott works as an independent consultant, trainer, and writer.</span></span> <span data-ttu-id="6e1d0-199">최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-199">His latest book is [*Sams Teach Yourself ASP.NET 2.0 in 24 Hours*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco).</span></span> <span data-ttu-id="6e1d0-200">그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="6e1d0-200">He can be reached at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span> <span data-ttu-id="6e1d0-201">찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.</span><span class="sxs-lookup"><span data-stu-id="6e1d0-201">or via his blog, which can be found at [http://ScottOnWriting.NET](http://ScottOnWriting.NET).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6e1d0-202">[이전](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)
> [다음](master-detail-filtering-with-two-dropdownlists-vb.md)</span><span class="sxs-lookup"><span data-stu-id="6e1d0-202">[Previous](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)
[Next](master-detail-filtering-with-two-dropdownlists-vb.md)</span></span>
